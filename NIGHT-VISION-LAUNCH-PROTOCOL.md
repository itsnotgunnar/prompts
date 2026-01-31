## THE NIGHT-VISION LAUNCH PROTOCOL (NVLP)
*A living system for building “impossible” experiences that survive contact with trust, law, and human regret.*

### Prime Directive
You are not shipping a feature. You are shipping a **new social object**: a “moment” that can be captured, replayed, shared, revoked, and remembered.

Social objects either:
- become culture, or
- become scandal.

Your job is to make it the first, by design.

---

# PHASE 1 — SANCTION THE CONFUSION (don’t fix it; name it)
Create a “Confusion Ledger.” Every confusion must be typed. No prose therapy—classification.

**Confusion types (non-optional taxonomy):**
1) **Ontology confusion** — “What is the thing?” (memory? highlight reel? receipt? love letter? artifact?)
2) **Agency confusion** — “Who is doing what to whom?” (capture vs consent vs share vs remix)
3) **Boundary confusion** — “Where does this stop?” (time window, physical boundary, social boundary)
4) **Causality confusion** — “What produced this output?” (telemetry provenance, inference chain)
5) **Value confusion** — “What are we optimizing?” (delight, retention, intimacy, dignity, safety)
6) **Failure confusion** — “How could this go wrong without us noticing?”
7) **Legibility confusion** — “Could a normal person explain this to a friend without sounding evil?”

For each confusion, write:
- the *minimum decision* that would reduce it,
- the *cost* of deciding too early,
- the *cost* of deciding too late.

This ledger becomes your steering wheel. If you can’t type your confusion, you’re not confused—you’re avoiding.

---

# PHASE 2 — DEFINE THE SOCIAL PHYSICS (the product is not the app)
You’re building “warm, seducing memories.” Those are not data objects; they are **social events**.

Define your world in terms of **actors and rights**:

### Actors
- **Subject**: a person appearing in the moment
- **Captor**: device/system that records signals
- **Owner**: account that stores/curates the artifact
- **Witness**: other participant(s) whose devices/signals corroborate
- **Recipient**: someone who views it later
- **Bystander**: someone incidentally captured (high risk)

### Rights (make them explicit, not implied)
For each actor type, specify rights for:
- capture permission
- inclusion permission (“you may show me”)
- distribution permission (“you may share me”)
- monetization permission (“you may profit from me”)
- revocation (and what revocation actually means technically)
- contestability (“this is wrong / harmful / misattributed”)

If you don’t formalize these, your system will default to “whoever has the file wins,” which is how you get destroyed.

---

# PHASE 3 — ARCHITECTURE BY INVARIANTS (the spine that prevents runway fires)
Competitors can copy features. They can’t easily copy invariants that shape everything.

Pick 7–11 invariants that are “true no matter what.” Here’s a high-grade candidate set for your domain:

### Consent + multi-party reality
1) **No silent inclusion**: if a memory depicts a person, that person can discover it exists.
2) **Revocation is real**: revocation propagates; it doesn’t merely hide the UI.
3) **Sharing is downstream-checked**: sharing requires re-checking current consent state, not past state.

### Data minimization + provenance
4) **Minimal raw capture**: prefer on-device feature extraction; raw audio/video is the exception, not default.
5) **Provenance manifests**: every generated memory carries a cryptographically verifiable “ingredients label” (sources, timestamps, consents, transformations).
6) **No hallucinated memories**: the generator cannot invent events; it can only compress/beautify confirmed signals.

### Safety + social integrity
7) **Bystander protection by default**: if the system can’t establish participant status, it degrades output quality rather than increasing capture.
8) **Anti-stalker posture**: the product must be harder to use for coercion than for delight.
9) **Legibility invariant**: a user must be able to answer: “Why did this appear?” in one sentence.

### Time + decay (prevents graveyard hoarding)
10) **Default expiry**: moments decay unless deliberately saved by all required parties.
11) **Contextual integrity**: a memory can’t be transported into new contexts (public, workplace, unknown audiences) without new friction/permissions.

These invariants are what “quality” means in your category.

---

# PHASE 4 — MAP THE SEAMS (unknown unknowns live here)
Now do the seam map, but at “launch pressure” resolution.

Seams you must draw as first-class objects:
- **Device sensors ↔ permissions** (what the OS actually allows, not what you wish)
- **Signal ↔ inference** (what you infer from proximity/audio/motion)
- **Inference ↔ narrative** (how the system turns signals into story)
- **Narrative ↔ truth** (how it avoids false implication)
- **Truth ↔ intimacy** (how it stays warm without becoming manipulative)
- **Storage ↔ deletion** (backups, caches, CDN copies, ML training sets—everything)
- **Identity ↔ pseudonymity** (what “being in the moment” means)
- **Sharing ↔ screenshotting/recording** (the “you can’t control the recipient” seam)
- **Legal compliance ↔ product experience** (consent flows that don’t kill magic)

For each seam:
- failure mode (specific)
- detection mechanism (telemetry/logging/alerts)
- mitigation strategy (design + technical)
- “PR headline if we screw this up” (write it; don’t flinch)

If you can’t write the headline, you’re not looking.

---

# PHASE 5 — THE MEMORY ENGINE AS A COMPILER (buildable magic)
Treat generation as compilation with strict typing and permissions.

### Inputs (typed and permissioned)
- **Event signals**: timestamp, duration, location category (not exact), motion rhythm, co-presence graph
- **Media (optional)**: photos/videos/audio only with explicit per-event consent
- **Confirmations**: “this mattered” taps, post-event prompts, mutual “yes”
- **Witness corroborations**: “I was there” acknowledgments or cryptographic co-presence proofs
- **Context**: event type chosen by user (“dinner,” “show,” “walk,” “afterparty”), not inferred unless confirmed

### The compiler stages
1) **Acquire** (collect minimal signals)
2) **Normalize** (clean noise; remove high-risk fields)
3) **Validate** (are required consents present?)
4) **Corroborate** (does the system have enough mutuality to claim “togetherness”?)
5) **Render** (generate artifact: montage, caption, timeline, “warm note”)
6) **Attach manifest** (provenance + rights + expiry + revocation pointers)
7) **Gate** (sharing rules based on audience/context)

### Output artifacts (plural, not one)
A single “memory” should have **levels**:
- **Private draft**: only you; low certainty; no sharing
- **Mutual memory**: participants validated; shareable within group
- **Public story**: requires extra consent + extra friction + extra expiry rules

This tiering prevents a ton of disasters.

---

# PHASE 6 — LAUNCH READINESS IS A SET OF PROOFS (not a feeling)
You don’t “feel ready.” You prove readiness with adversarial tests.

## The Five Proofs
1) **Consent proof**: we can demonstrate who consented to what, when, and how it was used.
2) **Revocation proof**: we can revoke and prove removal across caches/indexes/shares within a defined SLA.
3) **Misattribution proof**: we can detect and correct “false implication” memories (e.g., implying closeness that wasn’t real).
4) **Bystander proof**: we can show the system degrades gracefully when uncertain—no stealth capture escalation.
5) **Abuse proof**: we have specific mitigations for stalking/coercion/blackmail dynamics and a pipeline for rapid response.

If any proof is missing, you are not late—you are unfinished.

---

# PHASE 7 — THE DELIGHT WITHOUT ADDICTION RULESET (your “feverish demand” needs discipline)
You want demand. Fine. But demand can be created by:
- **beauty**, or
- **compulsion**.

If you choose compulsion, the system becomes ugly and fragile.

So set a hard rule:
- **We optimize for “mutual longing,” not “individual craving.”**

That means the product should increase:
- group closeness
- shared reflection
- coordinated future plans

Not:
- jealousy loops
- insecurity farming
- parasocial manipulation
- “prove you were there” status weapons

This is not ethics theater. It’s anti-fragility.

---

# PHASE 8 — THE DANGEROUS QUESTION (the one you must answer)
Your last paragraph implies a huge, volatile claim:

> “By way of a myriad of telemetry vectors … we capture forgotten moments … transform them into warm memories that fuel the next moment.”

The dangerous question is:

**What telemetry is permissible to interpret as intimacy, and who gets to decide?**

If the system answers that silently, it becomes an intimacy machine that *asserts* relationships. That’s where lawsuits, breakups, and headlines live.

So: intimacy must be **co-authored**.
- the system can *suggest*
- people must *confirm*
- and any involved person must be able to *veto*

Design that into the compiler.
