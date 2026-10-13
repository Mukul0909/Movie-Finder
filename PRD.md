# streaminghot — Product Requirements Document

**Version 1.1 · North star document**

*When a decision feels uncertain, the answer should be in here. If it isn't, add it.*

---

## 1. The one page

| | |
|---|---|
| **Product** | streaminghot |
| **Tagline** | pick before it goes cold |
| **What it is** | A web app that decides what you should watch while you eat |
| **Position** | The meal is the occasion. Decisiveness is the character. |
| **Primary user** | Adults who eat in front of a screen, 25–45, paying for 2–5 streaming services |
| **Core promise** | One confident answer, in under ten seconds, that fits the time your meal takes |
| **Business model** | Free and unlimited forever. Affiliate from day one. Three free tickets, then a one-time $7 unlock. |
| **Platform** | Installable web app. No native apps. |
| **Launch markets** | US, UK, Canada, Australia, New Zealand, Ireland, India |
| **Timeline** | Free tier properly built over a few months |
| **Budget** | Zero. Free tiers only. This is a hard design constraint. |

### The test every decision must pass

> **Does this get a hungry person watching something faster?**

Not "is this a good feature." Not "would users like this." Faster, for someone with a plate in front of them. If the answer is no, it doesn't ship — regardless of how good the idea is.

---

## 2. The problem

Someone sits down with a hot meal. They open a streaming app. Fifteen minutes later the food is lukewarm and they still haven't chosen — or they've defaulted to something they've seen four times.

Three things make this specifically hard, and all three are ignored by existing tools:

**It's time-boxed.** A meal lasts a known, short duration. Most content doesn't fit it. A two-hour film is the wrong answer to a twenty-minute lunch, but nothing asks how long you have.

**Attention is divided.** You're looking down at a plate. Subtitles are unusable. Plot-dense content you can't miss two minutes of is unusable. No existing tool knows this.

**Decision energy is already spent.** It's the end of the day. The user does not want to evaluate options; they want to be told.

### What the problem is not

It is not a discovery problem. The user isn't looking for a hidden gem or building a watchlist for someday. They want to eat, now, while watching something adequate-to-good. "Adequate and immediate" beats "perfect and twenty minutes away."

---

## 3. Competitive landscape

**The honest assessment: this category is crowded.** Any plan premised on "nothing like this exists" is wrong and will lead to bad decisions.

### What already ships, mostly free

| Product | What it does |
|---|---|
| Reelgood Roulette | Spin for a pick based on taste and subscribed services |
| FlickPick | One-tap random picks, filters for genre, rating, runtime, provider; AI summaries |
| The Movie App | Roulette filtered by your services, mood browsing, swipe-matching for couples |
| Movie Roulette | Mood filters (laugh, cry, thrill), genre, runtime, platform |
| Limelight | Quiz across mood, company, time available, genre, era, dealbreakers |
| NightPicks, various web tools | Free, no signup, mood plus runtime plus provider, instant pick |

So: mood filtering, runtime filtering, provider filtering, one-tap picks, reroll, where-to-watch links — **all solved, already free, often without signup.**

### What is genuinely unoccupied

Three things, and the product should be built almost entirely around them:

**1. The meal as the occasion.** Every competitor is positioned around *movie night* — a weekly, planned, higher-stakes event. Nobody owns *mealtime* — daily, unplanned, lower-stakes, higher-frequency. This is the wedge.

**2. The attention dimension.** "Can you look away from the screen?" No competitor asks this. It is the most original mechanic in the product and it only makes sense in an eating context.

**3. Decisiveness as a stance.** Competitors are roulettes — random, playful, reroll guilt-free. streaminghot commits: here is one, I am confident, go eat. Different posture, and the one users actually want even if they don't ask for it.

Supporting differentiator: **TV-first with episode-length matching**, where competitors are film-first.

### Positioning statement

> For people eating in front of a screen, streaminghot ends the scroll with one confident pick sized to the meal in front of them — unlike movie-night roulettes, which hand you another random option to evaluate.

**The meal is the door. Decisiveness is the room.** One is how people find and describe us. The other is why they come back.

### Strategic honesty

Defensibility is not technology or data — competitors have both. It is **the willingness to be decisive and to stay narrow.** Incumbents can't copy the first because their business depends on continued browsing, and won't copy the second because their market is broader. Protect narrowness. It is the only moat.

---

## 4. Target user

**Primary:** 25–45, pays for two to five streaming services, eats at least one meal a day in front of a screen, usually alone or with one other person. Decides on a phone or laptop. Has felt the scroll-until-cold experience and finds it mildly absurd.

**Secondary:** couples who negotiate the choice. Higher pain, more valuable, addressed in v2 via household mode.

**Explicitly not the user:** film enthusiasts seeking discovery, watchlist maintainers, people looking for something to watch *someday*, families choosing for children.

---

## 5. Product principles

1. **One answer beats many options.** The value is the removal of choice.
2. **Infer, never ask.** Time of day, meal length defaults, region — derived, not configured.
3. **Never block a hungry person.** No signup wall, no paywall, no form before value.
4. **Speed is the feature.** Measured in seconds from open to play.
5. **Narrow is the strategy.** Every feature must serve someone with a plate in front of them.
6. **Honest over impressive.** Never show data we don't have. Never imply certainty we lack.
7. **Decisive, not random.** We are not a roulette. We have a view.

---

## 6. Scope

### v1 — the free tier (in progress)

- Mood selection: Cozy, Tense, Light, Curious
- Meal-length control, pre-set from time of day
- Attention toggle: on the plate / on the screen
- Origin filter, honestly labelled
- Three differentiated picks: the safe one, the quick one, the wildcard
- Shuffle, capped at two rounds
- Dark and light themes
- Installable, offline-capable, responsive from 320px to 4K
- Local history, no account
- **Continue watching** — next priority, local only
- **Voice input** — single utterance, fills the same form
- Outbound links with affiliate tags where available

### v2 — accounts and the one-pick tier

- Magic-link auth, no passwords
- Durable history, cross-device
- Streaming service selection
- Real availability data and regional deep links
- AI-chosen single pick, presented as the ticket
- Re-roll with the two-strike cap
- Mid-meal rescue

### v3 — the paid proposition

- **Household mode** — two profiles, one pick that satisfies both
- Cross-device memory as part of the same bundle
- Three free tickets, then a one-time $7 unlock
- Ambient pre-pick notifications

### Never

| Excluded | Reason |
|---|---|
| Chatbot | Adds interaction to a product about removing it |
| Watchlists | We solve "what now," not "what someday" |
| Ratings and reviews | Asks the user to work for our algorithm |
| Social feed | Different product, different economics |
| Browse or search | The thing they came here to escape |
| Films | Breaks the meal-fitting promise on every pick |
| Native apps | Store tax on a one-time-fee model |
| More than five moods | Thins each pool, adds taps |

---

## 7. The closed loop

The product's job is to take a user from one state to another. Every design decision should be judged on whether it closes this loop.

```
OPEN STATE                          CLOSED STATE
hungry, plate hot,         →        eating, watching something
screen dark, undecided              they're content with
```

### The loop today

| Step | State | Can we see it? |
|---|---|---|
| 1 | Arrives, undecided | Yes |
| 2 | Picks mood | Yes |
| 3 | Receives options | Yes |
| 4 | Taps one | Yes |
| 5 | Leaves for the streaming service | Partially |
| 6 | **Watches, or returns to scrolling** | **No** |

**The loop is currently open.** Step 6 happens somewhere we cannot observe. We know what we recommended and what was tapped. We do not know whether the user ate while watching something they enjoyed — which is the only outcome that matters.

### How we close it

Three mechanisms, in priority order:

**1. Return confirmation (cheapest, highest signal).**
When a user returns after tapping out, ask one question with two buttons: *did you watch it?* That single data point is worth more than every other metric combined, because it is the only direct measure of whether the product worked.

**2. Continue watching (closes retroactively).**
On the next visit: "you're four episodes into The Bear." If they accept, the previous session is confirmed successful. The loop closes on the following visit.

**3. Mid-meal rescue (closes within the session).**
Fifteen minutes after acceptance: *still working?* Yes closes the loop positively. No tells us the pick failed, and gives one chance to fix it before the meal ends.

### Loop exits, and what each means

| Exit | Interpretation | Response |
|---|---|---|
| Accepted first pick, confirmed watched | Loop closed. Success. | Reinforce affinity |
| Accepted, never confirmed | Probable success, unverified | Count as soft success |
| Shuffled, then accepted | Loop closed slowly | Log why the first missed |
| Hit the shuffle cap, left | **Loop failed** | Highest-priority failure to investigate |
| Left before any pick | Loop never started | Check load speed, first impression |
| Accepted, then returned within 5 min | **Loop failed silently** | Treat as a reject |

That last row matters most and is easy to miss. A user who accepts a pick and reopens the app three minutes later did not get what they came for.

---

## 8. Functional requirements

### 8.1 Entry

- No signup, no modal, no interstitial. First paint shows the question.
- Time of day sets the context phrase and pre-selects the meal length.
- Region inferred from browser locale, user-correctable.
- If local history exists and a series is in progress, offer continue-watching **before** mood.

### 8.2 Input

- **Mood** — four tiles, one required tap. The only mandatory input.
- **Meal length** — eight bands from 10 to 75 minutes, pre-set, adjustable in one tap.
- **Attention** — two states, defaults to "on the plate" (excludes subtitled).
- **Origin** — optional, defaults to anywhere.
- **Voice** — one utterance populating any of the above; unparsed values fall back to defaults. Never asks a follow-up.

Total required interaction to reach a result: **one tap.**

### 8.3 Selection logic

Mood is expressed as a weighted recipe over the catalogue, not an API filter:

- **Gate** — must carry at least one qualifying genre
- **Veto** — disqualifying genres, applied absolutely
- **Boost** — weighted points per matching genre
- **Type weights** — documentary, scripted, animation
- **Target runtime** — distance from it costs points
- **Overrun penalty** — running past the meal costs the most
- **Attention penalty** — subtitled content, when eyes are down

Free tier fills three slots with distinct jobs:

| Slot | Rule |
|---|---|
| The safe one | Highest-scoring candidate |
| The quick one | Shortest that still qualifies |
| The wildcard | Highest-scoring candidate sharing no genre with the safe pick |

Three *similar* options is paralysis. Three *different* options is a decision. The labels are load-bearing — without them it's just a list.

### 8.4 Results

- Three cards, poster-led, no overlay text on the artwork
- Runtime and genre in monospace
- One-line reason per card
- Network, origin, and subtitled flag
- Outbound link with affiliate tag where available
- Shuffle: two rounds, then locked with a sign-in prompt

### 8.5 Paid tier (v2/v3)

- One pick, presented as the ticket: poster, perforated edge, serial number, personal note
- Serial number is the real count of accepted picks for that user
- Model chooses from a code-supplied shortlist of 15 and writes the reason
- Model may never name a title; invalid responses fall back silently to the top-scored pick
- Re-roll: one question, two options, new ticket immediately. Third attempt refuses to ask and commits.
- **Escape hatch: ship absolute.** No "show me more." Loosen only if reject data demands it — a strict product can be relaxed; a relaxed one can't be tightened without feeling like a takeaway.

---

## 9. Technical architecture

### Constraint: zero budget

This is not a preference, it is a design input. Every component must have a free tier that covers launch volume.

| Need | Choice | Cost |
|---|---|---|
| Catalogue data | TVmaze public API | Free, no key, CORS-enabled |
| Hosting | Netlify / Vercel / Cloudflare Pages | Free tier |
| Domain | Free subdomain at launch | Free (custom domain later, ~$12/yr) |
| Auth (v2) | Supabase magic links | Free tier |
| Database (v2) | Supabase / Neon | Free tier |
| Model calls (v2) | Groq or Gemini free tier | Free within limits |
| Availability (v2) | Deferred — see below | — |
| Payments (v3) | Stripe | ~3% per transaction, no fixed cost |

**The one real cost risk is availability data.** Per-title, per-region lookups across seven markets do not fit a free tier if fetched eagerly. Mitigations, in order:

1. **v1: don't fetch it.** Show network and origin honestly. Link to a JustWatch search, which resolves regionally for free.
2. **v2: fetch lazily**, only for titles about to be shown, cached one week. In practice a small fraction of the catalogue surfaces weekly.
3. Only consider a paid tier of a provider API once revenue exists.

### Pipeline

```
Scheduled (weekly)
   TVmaze full index → quality floor → catalogue

Request (instant, local)
   inputs + local history
     → filter: runtime, attention, seen
     → score: mood recipe
     → three slots (free) / top 15 (paid)

Request (paid only, ~1.5s)
     → model picks one from the 15, writes the reason
     → fallback to top-scored on any failure
```

**The boundary is the point:** code decides what is possible, the model decides what is best, code decides what is shown. The model never touches the catalogue and never names a title. The product must remain correct, if slightly less warm, with the model removed entirely.

### Catalogue

- Source: TVmaze full index, walked newest-first
- Quality floor: rating ≥ 7.4, popularity ≥ 88, runtime 8–90 min, has poster, has genres
- Expected survivors: 3,000–6,000 titles
- Stored client-side for v1; server-side cache from v2
- Rebuilt weekly; it is a cache, not user data, and may be dropped freely

### Data model (v2)

`users` — region, services, tier
`catalogue` — rebuildable cache
`history` — **one row per pick shown, with full context**: mood, meal length, attention, outcome, reject reason
`availability` — title, region, provider, deep link, fetched_at
`payments` — local mirror of Stripe

History must record *context*, not just titles. "Rejected Severance" teaches nothing. "Rejected Severance with 22 minutes" is a signal.

### Security and privacy

- **No passwords, ever.** Magic links or OAuth. Nothing to hash, nothing to leak.
- Watch history is sensitive personal data. Encrypt at rest, offer export and delete, retain 90 days of detail.
- GDPR applies if any EU or UK user touches it. Privacy policy before launch, not after.
- Stripe holds all card data. We never touch it.

---

## 10. Monetisation

### The model

**Free tier: unlimited, forever. Paid tier: sampled, then purchased.**

The limit is never placed on the free product. It is placed on the *premium experience*. Nothing is ever taken away from a user — they simply get to feel the better thing a few times before deciding whether to keep it.

| Mode | Access |
|---|---|
| Three-option mode | Unlimited, free, forever, no account |
| One-pick ticket mode | **Three free tickets**, then a one-time payment |

### Why not gate the free tier

**Rejected: limiting searches (three, five, or any number).**

The failure mode is specific and fatal. A user hits the wall, searches the web, and lands on NightPicks, Reelgood or any of a dozen free no-signup tools within thirty seconds. We would be spending acquisition effort to hand users to competitors. In a market with abundant free substitutes, the free tier is the only growth engine we have.

**Rejected: subscription.** Recurring revenue requires daily indispensable value. The user already pays for several streaming services; a further monthly charge to help them use those is a hard sell.

**Accepted: affiliate revenue from day one.** Outbound links carry affiliate tags where programmes exist. Invisible, frictionless, scales with usage rather than conversion.

### What the paid tier actually is

"One pick instead of three" undersells it. Four things change, and only the first concerns quantity:

| Change | What the user notices |
|---|---|
| **It decides** | One ticket, printed. No slots, no comparing, no labels. |
| **It knows them** | The reason references what they've watched, not a template |
| **It never repeats** | Durable history, across devices |
| **It only shows what they can watch** | Services declared once, respected forever |

The personalised reason line is the thing people will describe to a friend. Everything else is table stakes by comparison.

### When the trial is offered — and why not on day one

**Problem:** on first use there is no history, so the personalisation cannot be demonstrated. Offering the trial immediately would sample the weakest version of the thing being sold.

**Rule:** the trial is offered only once local history is substantial enough for the model to say something specific — a minimum of **five accepted picks across at least three separate days.**

Framing at that moment:

> *"You've let me pick five times. Want me to just decide instead? Three on the house."*

Now the first ticket can reference what they actually watched. That is the moment the product becomes impressive rather than merely functional.

### The three tickets

- Full experience, no degradation, no expiry date
- The serial number does the counting quietly: NO. 001, NO. 002, NO. 003
- **No countdown banner, no urgency timer, no nag.** This is a product about reducing pressure; manufacturing pressure is off-brand.

### The ask

Placed **after** the third pick is accepted and the user has tapped through to watch. Never before a pick, never while they are waiting to eat.

The screen states plainly what the unlock provides:

> **That's three nights sorted.**
>
> Keep the ticket and I'll also:
> - Never offer you something you've already seen
> - Only pick from services you actually pay for
> - Remember where you left off in every series
> - Work the same on your phone and your laptop
> - Decide for two of you, when you want that
>
> **One payment. No subscription. $7.**

The honest number does the persuading. "Three nights sorted" is verifiable against the user's own memory, which no marketing claim can match.

### Price

**$7, one time.** Low enough to be an impulse, high enough not to read as disposable. $5 reads trivial; $9 invites comparison with a month of a real streaming service.

### If they decline

They return to three-option mode and **keep everything** — history, continue-watching, preferences. Nothing is removed.

The offer returns after a further stretch of use, worded differently. A hard wall converts a few and loses the rest; a soft wall keeps users in the product, and a meaningful share convert on a later ask once the habit is deeper.

### Payment rails

| Platform | Mechanism | Cost |
|---|---|---|
| Web (primary) | Stripe Checkout | ~3% |
| Native, if ever | Purchase on the web only, app reads entitlement | 0% |

**Web is the cheapest place to charge, not the hardest.** Stripe works without approval processes or fixed fees, and we keep roughly 97%.

Native app stores are the restriction, not the web. External payment links are permitted only in the US (currently 0%), the EU (20%), Japan (21%) and South Korea (26%). Everywhere else they are prohibited and in-app purchase applies at 30%, or 15% under the Small Business Program.

**Five of our seven launch markets — UK, Canada, Australia, New Zealand, India — fall under "everywhere else."** Native in-app purchase would cost $1–2 on a $7 unlock versus roughly 20 cents on the web. The US 0% rate is also unstable: Apple has proposed a 15% link-out fee and the matter is before the Supreme Court. It should not be planned around.

Developer accounts also break the zero-budget constraint: $99/year for Apple, $25 once for Google.

### If native apps are wanted later

Use **web-first billing**, the model Netflix and Spotify operate. Accounts are created and paid for on the website; the app never mentions payment and simply reads entitlement. Legal in every market, zero commission, no in-app purchase integration required.

The honest cost is conversion friction — no impulse upgrades, since the user must leave the app and return. Acceptable for a large service, more noticeable for a $7 utility. This is a distribution decision, not a revenue one, and should only be taken once retention is proven.

### Honest expectation

Conversion on a one-time unlock in a free utility is typically low single digits. The structure above is deliberately optimised for **retention over conversion**, because in a crowded market with free substitutes, keeping users is worth more than converting a small number of them.

This is more likely to become a well-loved free tool with modest affiliate income than a business. That is a legitimate outcome. Building the paywall before proving retention would be the expensive mistake.

## 11. Regions

Launch markets: **US, UK, CA, AU, NZ, IE, IN.** English-language interface only.

Implications:

- Catalogue quality floor must not over-index on US content
- Origin filter covers these markets plus Japan
- Availability, when added, must be keyed per region — seven markets is the cost driver
- Time-of-day inference uses the device clock, so it works everywhere with no configuration
- Date, time and number formats follow locale

Not in scope: interface translation, non-English content as a primary offering.

---

## 12. Non-functional requirements

**Performance**
- First paint under 1.5s on a mid-range phone over 4G
- Free-tier result: instant, no network call
- Paid-tier result: ticket renders immediately, reason streams in; model timeout 2.5s then fallback
- Works offline once installed

**Responsiveness**
- 320px to 4K, no horizontal scroll at any width
- No fixed pixel widths in layout
- Touch targets minimum 40px
- Safe-area insets respected
- Must survive the longest title in the catalogue at the narrowest viewport

**Accessibility**
- Keyboard navigable throughout
- Visible focus states
- Minimum 11px type, adequate contrast in both themes
- Reduced-motion respected
- Screen-reader labels on all controls

**Resilience**
- Catalogue unavailable → clear message, no blank screen
- Model fails → silent fallback to top-scored pick
- Availability stale → link to a page that resolves, plus one-tap report
- Thin result pool → relax the least important constraint and say so

---

## 13. Success metrics

### The one number

**Time from open to pressing play.** This is the promise, expressed in seconds. Everything else is diagnostic.

### Gates

Each phase has a threshold. Do not pass a gate on enthusiasm.

| Metric | Target | Gate for |
|---|---|---|
| Day-7 return rate | ≥ 25% | Building accounts |
| Returns 3+ times per week | ≥ 15% of actives | Building the paid tier |
| Picks accepted with zero shuffles | ≥ 50% | Shipping one-pick mode |
| Shuffle-cap-then-leave | ≤ 15% | Keeping the cap at two |
| Confirmed-watched, when asked | ≥ 60% | Charging anything |

### Diagnostics

- Which slot wins in the free tier — does the wildcard ever get picked?
- Reject reason distribution per mood — tells you which recipe is miscalibrated
- Share of sessions resolved by continue-watching
- Voice adoption where supported
- Model fallback rate
- Dead link reports

### The honest threshold

**If users are not returning three times a week, no pricing model, feature, or redesign saves this.** Fix retention or stop. Everything from v3 onward depends on this being true.

---

## 14. Roadmap

| Phase | Build | Gate to proceed |
|---|---|---|
| 0 | Free tier deployed, analytics in place | Real users, real sessions |
| 1 | Continue watching (local) | Measurable drop in time-to-watch |
| 2 | Voice input | Any meaningful adoption |
| 3 | Return confirmation ("did you watch it?") | Confirmed-watched ≥ 60% |
| 4 | Accounts, durable history | Day-7 ≥ 25% |
| 5 | Availability and regional deep links | Links working in top three markets |
| 6 | One pick, the ticket, re-roll cap | Zero-shuffle acceptance ≥ 50% |
| 7 | Ticket trial + Stripe + household mode | 3×/week returns ≥ 15% |
| 8 | Ambient pre-picks | Prediction accuracy acceptable |

Phases 1 to 3 need no accounts, no server, and no money. They are the highest-value work available and should be done before anything requiring infrastructure.

---

## 15. Risks

**Retention is unproven.** Every plan here assumes people come back. That is an assumption, not a finding, and it is the only one that matters.

**The category is crowded with free alternatives.** Differentiation rests on positioning and discipline, not capability. If the meal frame doesn't resonate, there is no fallback differentiator.

**The meal frame may be a gimmick.** Users may have a general indecision problem that merely occurs at mealtimes. Test whether people describe the product back to you in meal terms. If they don't, the position is decoration.

**One pick means nowhere to hide.** A weak recommendation in the free tier is one of three. In the paid tier it is the entire product.

**Catalogue depth limits personalisation.** A few thousand titles, minus history, thins fast. Monitor per-user pool size; below ~30 the picks start feeling repetitive even when titles don't repeat.

**Zero budget limits availability data**, which is the weakest part of the core promise. "Watch this now" is only fully true with reliable regional availability.

**Solo non-technical founder.** The chokepoint is not getting code written, it is owning something you cannot fix at 11pm. Phases 4 onward need either a technical partner or genuine comfort with AI-assisted debugging.

**Licensing.** TVmaze is CC BY-SA 4.0 with attribution; confirm commercial use before taking money. Same for any availability provider.

---

## 16. Decision log

Settled, with reasons. Revisit only with new evidence.

| Decision | Choice | Why |
|---|---|---|
| Platform | Installable web app | Store tax, speed to ship, shareable links |
| Content type | TV only | Films break meal-fitting on every pick |
| Data source | TVmaze | Free, no key, TV-first, CORS-enabled |
| Mood count | Four | More thins each pool and adds taps |
| Paid model | One-time $7, not subscription | Users already pay for several services |
| Free tier limit | None, ever | Free substitutes abundant; bouncing users feeds competitors |
| Paid trial | 3 tickets, offered after 5 picks over 3+ days | Personalisation can't be demonstrated with no history |
| Payment rail | Stripe on web; web-first billing if native | 3% vs 15–30% store commission |
| Paid escape hatch | None at launch | Can loosen later; can't tighten |
| Chatbot | No | Inverts the thesis; competes with free assistants |
| Voice | Yes | Correct input mode for busy hands |
| Passwords | Never stored | Magic links are less work and safer |
| Accent colour | Green (dark), blue (light) | Green reads restaurant, not tech |
| Logo | Single film-strip wisp over a plate | Plate avoids the Java/coffee read |

### Still open

1. Fifth mood, or does the attention toggle cover the gap
3. Re-roll cap: two or three
4. Whether to pursue this as a business at all — deliberately deferred until retention data exists

---

*Version 1.1 — monetisation structure and payment rails revised.*

*Written collaboratively, October 2026. Revise when evidence contradicts it, not when enthusiasm suggests it.*
