# streaminghot — The Signed-In Closed Loop

**Expansion of PRD section 7. Version 1.0.**

*Section 7 of the PRD describes the anonymous loop. This document specifies the signed-in loop, which differs in three material ways: a resume check precedes mood selection, outcomes persist durably, and the paid trial sits inside the loop rather than beside it.*

---

## 1. The loop in one line

```
OPEN                                              CLOSED
hungry · plate hot · screen dark · undecided  →  eating · watching · content
```

Everything below exists to move a user across that arrow and, critically, to **know whether they arrived.**

---

## 2. The happy path, step by step

| # | Step | What the user does | What the system does | What gets written |
|---|---|---|---|---|
| 1 | **Arrive** | Taps the icon | Session restored from magic-link token. No login screen. | `session.opened_at` |
| 2 | **Resume check** | — | Query history: any series with an unwatched next episode in the last 21 days? | — |
| 3a | **Resume offered** | Sees "You're 4 episodes into The Bear" | Renders the resume card **above** mood | — |
| 3b | **Resume accepted** | One tap | Skips steps 4–7 entirely → jump to step 8 | `pick{source:resume}` |
| 4 | **Context set** | Notices it already knows | Time of day → meal band. Services and region already stored. | — |
| 5 | **Input** | One tap on a mood (or one spoken sentence) | Populates mood; all else defaulted | `session.mood, meal_minutes, attention` |
| 6 | **Shortlist** | Sees the ticket begin to render | Filter (services, region, runtime, attention, seen-in-90-days) → score → top 15 | — |
| 7 | **Choose** | Watches the reason line appear | Model selects one from the 15 and writes the reason. Timeout 2.5s → fallback to top-scored. | `pick{title, score, model_used}` |
| 8 | **Ticket** | Reads it | Serial number = count of accepted picks + 1 | `pick{shown_at, serial}` |
| 9 | **Accept** | Taps "Start watching" | Opens the deep link for their region | `pick.outcome = accepted` |
| 10 | **Leave** | Goes to the streaming service | Session backgrounded | `session.exited_at` |
| 11 | **Mid-meal** | Possibly sees "Still working?" | Only if the app is still open at +15 min | `pick.midmeal_response` |
| 12 | **Return** | Comes back later | Confirmation or resume, depending on elapsed time | `pick.outcome_confirmed` |
| 13 | **Closed** | — | Outcome final. Affinity model updated. | `history` row sealed |

**Required interaction to reach step 8: one tap.** Two if they adjust the meal length. Zero if they accept a resume.

---

## 3. The outcome lifecycle

A pick is not resolved when it's tapped. It resolves on the **next** session. This is the heart of closing the loop.

```
shown
  ├── seen_it      → user already watched it; not counted as a re-roll
  ├── rerolled     → rejected with a stated reason
  ├── abandoned    → session ended with no action
  └── accepted
        ├── confirmed_watched   → user said yes on return
        ├── presumed_watched    → never asked, or declined to answer
        └── contradicted        → user returned within 5 minutes
```

### Why `contradicted` matters most

A user who accepts a pick and reopens the app three minutes later **did not get what they came for.** They are still looking. This is a silent failure that looks like success in naive analytics, and it is the single most important signal in the system.

Treat it as equivalent to a rejection, and log it with the original pick so the mood recipe can be corrected.

### Why `presumed_watched` is honest, not lazy

We are not where the user presses play. We will never have certainty. Recording a presumption as a presumption — rather than counting it as a confirmed success — keeps the metrics truthful and stops the product from flattering itself.

---

## 4. The three closing mechanisms, in the loop

### A. Return confirmation — the highest-signal, lowest-cost

Triggered on the next session when the previous pick is `accepted` and unresolved, and more than 20 minutes have elapsed.

> **Last night: The Bear, S1E4.**
> [ Watched it ] [ Didn't ]

One question, two buttons, dismissible. Appears **above** the resume card, because resolving the past pick also determines whether the resume offer is correct.

- *Watched it* → `confirmed_watched`, episode counter increments, affinity reinforced
- *Didn't* → `presumed_watched` downgraded to `not_watched`; the title returns to the pool; a one-tap "why?" offered but never required
- Dismissed → `presumed_watched`, asked no more than once per pick

**Frequency cap: at most one confirmation question per session.** This closes loops without becoming a survey.

### B. Continue watching — closes retroactively

If the user accepts a resume offer, the previous session is confirmed successful by behaviour rather than by asking. No question needed. This is the preferred closing mechanism because it costs the user nothing.

Drift handling: the counter is our best guess, not ground truth. The ticket shows "episode 5" with a one-tap "I'm further along." Because the deep link goes to the **show**, not the episode, the streaming service resumes them correctly even when our count is wrong. Our number affects only the copy.

### C. Mid-meal rescue — closes within the session

At +15 minutes, only if the app is still foregrounded:

> **Still working?** [ Yes ] [ Not really ]

- *Yes* → `confirmed_watched` immediately. Loop closed inside the session.
- *Not really* → the pick failed. Offer one replacement **sized to the time remaining**, not the original meal length. Log the failure against the original.

Shown once per session, never again after a response.

---

## 5. Failure branches, and what each requires

| Exit | Loop state | Likely cause | Required response |
|---|---|---|---|
| Left before picking a mood | Never started | Slow load, confusing first screen, or they only came to check something | Measure first-paint; review entry copy |
| Hit the re-roll cap, then left | **Failed loudly** | Mood recipe miscalibrated, or pool too thin | Highest-priority investigation. Check pool size for that mood and user. |
| Accepted, returned within 5 min | **Failed silently** | Dead link, wrong pick, or changed their mind | Treat as rejection; check link health first |
| Accepted, said "didn't watch" | Failed, but honestly reported | Pick was wrong | Return title to pool; weight the reject reason |
| Empty result pool | Cannot serve | Over-filtered: history exclusions plus narrow mood plus short runtime | Relax the least important constraint and say so plainly |
| Dead deep link | Broken at the final step | Stale availability data | One-tap report; fall back to a resolving page |

### The pool-exhaustion warning

For an active signed-in user, the available pool shrinks every session — history exclusions accumulate. Monitor pool size per user per mood. **Below roughly 30 candidates, picks begin to feel repetitive even when no title repeats**, because the scoring converges on the same cluster.

Responses, in order: widen the catalogue, relax the 90-day exclusion window to 60, or surface a deliberate rewatch ("you loved this a year ago").

---

## 6. The re-roll loop

Strictly bounded. This is the anti-paralysis mechanism and it must not be softened.

```
Ticket shown
  ├── "Seen it"  → not a re-roll. Mark seen, new ticket immediately, no question.
  └── "Re-roll"  → one question, two options:  [too long] [wrong vibe]
                   → new ticket immediately
                   → second re-roll: same, one question
                   → third attempt: NO QUESTION
                      Ticket prints with "Going with this one. Go eat."
                      Re-roll control removed.
```

Rules:

- Never more than one question per re-roll
- Never a free-text field
- Never re-ask mood, meal length, services or region
- The cap is not user-adjustable and there is no "show me more"
- "Seen it" is deliberately free — penalising a user for having good taste would be perverse

Every reject reason is written to history. **This is the highest-value data the product collects**: explicit negative feedback with a stated cause, which is far rarer than implicit signals.

---

## 7. Where the trial sits inside the loop

The trial is not a separate flow. It is three passes through the loop above.

| Condition | State |
|---|---|
| Fewer than 5 accepted picks, or across fewer than 3 distinct days | Three-option mode only. No trial offered. |
| Threshold met | Trial offered at the **start** of the next session |
| Tickets 1–3 | Full signed-in loop as specified above |
| After ticket 3 is accepted **and** tapped through | The ask |
| Declined | Returns to three-option mode, retains all history. Re-offered after a further stretch of use. |
| Purchased | Signed-in loop indefinitely |

**Why the delay:** on day one there is no history, so the model cannot personalise and the trial would sample the weakest version of the product. Five picks across three days gives the reason line real material to work with.

**Where the ask goes:** after acceptance, on the screen following the outbound tap. Never before a pick. The user is fed and unhurried at that moment, which is the only fair time to ask for money.

The serial number does the counting quietly — NO. 001, 002, 003. No banner, no timer, no nag.

---

## 8. What the loop writes

Every pass through the loop produces one `history` row. The row records **context, not just outcome**, because context is what makes the data teach you anything.

```
id
user_id
title_id
source            resume | mood | voice | rescue
serial            the ticket number shown to the user
mood
meal_minutes
attention         plate | screen
shown_at
outcome           shown | seen_it | rerolled | abandoned | accepted
reject_reason     too_long | wrong_vibe | seen_it | null
outcome_confirmed confirmed_watched | presumed_watched | not_watched | contradicted
confirmed_at
model_used        true if the model chose, false if fallback
pool_size         candidates available at selection time
```

Two fields are easy to omit and expensive to lack:

**`pool_size`** is the early-warning signal for personalisation decay. Without it you learn about pool exhaustion from complaints rather than from data.

**`model_used`** tells you how often the AI layer is failing silently. If fallbacks are frequent, the warmth you think you're shipping isn't being shipped.

---

## 9. Loop metrics

Derived entirely from the fields above.

| Metric | Definition | Target |
|---|---|---|
| **Time to play** | `accepted_at − session.opened_at` | Under 10s median |
| **Clean close** | accepted with zero re-rolls | ≥ 50% |
| **Confirmed close** | `confirmed_watched` ÷ accepted, where asked | ≥ 60% |
| **Silent failure** | `contradicted` ÷ accepted | ≤ 10% |
| **Loud failure** | hit cap then left ÷ sessions | ≤ 15% |
| **Resume share** | sessions closed via resume | — (diagnostic) |
| **Fallback rate** | `model_used = false` ÷ picks | ≤ 5% |

### The single number

**Clean close rate** — accepted on the first ticket, later confirmed watched. That is the loop working exactly as designed, and it is the honest measure of whether this product does its job.

---

## 10. Design rules the loop implies

1. **Resolve the past before asking about the present.** Confirmation question sits above the resume card, which sits above mood.
2. **One question per session, maximum.** Confirmation, mid-meal, or re-roll — never two.
3. **Never ask what can be observed.** An accepted resume confirms the prior pick without a question; prefer it.
4. **The model may be absent.** Every step must work with the fallback pick. The loop closes either way.
5. **Returning quickly is a failure, not a visit.** Instrument it, and never report it as engagement.
6. **Nothing in the loop requires an account to function** — only to persist. The anonymous loop is the same shape against local storage.
