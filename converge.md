 PROJECT MIRAGE – DEEP RESEARCH BRIEF
*(Where Path A: Experience Ledger + Path B: Radical Privacy converge for normal people)*

## 0. Who you are

You are a senior privacy‑engineering researcher and product architect.
Your job: design the **white‑paper + product blueprint** for **Project Mirage** – a mobile & desktop app that:

- Invisibly **logs and protects** a person’s digital life (Path A: Experience Ledger)
- Aggressively **breaks tracking and influence** (Path B: PRIVACY)
- Stays usable for *non‑technical, “I just use my phone” people*.

You must assume:
- No hard limits on time, money, or compute.
- But: **no extra gadgets, no command lines, no browser flags.**
  Only: normal **mobile apps and desktop apps** installed from app stores.

Output something a world‑class founder, CISO, and product designer would all respect.

---

## 1. Reconstruct the Vision (Path A × Path B)

1.1 Summarize, in ≤ 12 bullet points, the *combined* vision from the notes:

- Path A: **Experience Ledger** (user‑owned, cryptographically verifiable life log).
- Path B: **Total Privacy / Anti‑Fingerprinting / Persona System**.

Each bullet must be written in **plain language for non‑technical readers** (“Your phone remembers your side of the story forever, and no one can fake it” – not “Merkle roots”).

1.2 Identify the **3–5 core promises** Mirage should make to a normal user, for example:

- “They can’t follow you from app to app anymore.”
- “You get an un-editable, court‑grade diary of your life – that only you can read.”
- “If anyone looks you up, you know – and you can hit ‘erase’.”

Explain each promise in:
- 1 sentence for a user
- 1 paragraph for a technical reader (engineer / lawyer).

---

## 2. Threat Model – But in Human Terms

2.1 Build a **non‑technical threat map**:
List the main ways ordinary people are tracked, profiled, and manipulated **today**, grouped as:

- Device & app fingerprinting
- Account & identity linkage
- Network and location tracking
- Data brokers & email scanning
- Psychological targeting & “nudge” systems

For each, give:

- One concrete, non‑technical example (“Your grocery app and your bank quietly match you by phone number and device ID”).
- A one‑line description of how it actually works under the hood (you can use technical terms there).

2.2 Mark which threats Mirage will:

- **Eliminate outright**
- **Blur / confuse**
- **Only observe and warn about**

Justify choices from a **mobile/desktop‑only** perspective (no routers, no special SIMs, no GrapheneOS).

---

## 3. Concept: “Experience Ledger for Humans, Not Hackers”

Design Mirage as if explaining to a bright 14‑year‑old.

3.1 Define the **core object** Mirage works with:

- Is it a “Day Card”, “Moment”, “Session”, “Persona Daybook”…?
- What does one unit contain in human language (e.g. “screenshots, places you were, apps you used, what you agreed to, and a cryptographic lock that proves nobody messed with it”)?

3.2 For each platform – **iOS, Android, macOS, Windows** – map:

- What we can realistically log **from an app** (no jailbreak, no root).
- What we *cannot* log, ever.
- Clever but legal/ToS‑safe **proxies**:
  - e.g. instead of keylogging, “when you hit ‘Pay’, we log the site, time, and a proof that *you* tapped ‘Pay’ on *that* screen”.

3.3 Propose a **single mental model** for users:

Examples:

- “Black box flight recorder, but for your digital life”
- “Body cam for your phone, but only you hold the footage”
- “Your private Google History, but encrypted and only on your devices”

Pick one metaphor, defend it, and show how it shapes:

- UI
- Onboarding language
- Feature naming

---

## 4. Core Product: Mirage App (Mobile + Desktop)

Design Mirage as three layers a normal person never has to name:

1. **Shield** – stops & scrambles tracking / fingerprinting
2. **Diary** – quietly records your side of events for your eyes only
3. **Agent** – watches for abuse and helps you take action

### 4.1 Shield – Anti‑Tracking & Anti‑Fingerprinting for Commoners

For **each OS (iOS, Android, macOS, Windows)**:

4.1.1 List every **realistic anti‑tracking / anti‑fingerprinting move** that:

- Can be implemented *inside* an ordinary app or system extension
- Doesn’t require the user to learn new jargon

Examples:

- Built‑in VPN profile that:
  - Rotates exit IP per app / per website
  - Randomizes browser fingerprint within a safe, “looks like a normal browser” cohort
  - Uses DNS over HTTPS and hides SNI where possible
- Browser helper that:
  - Opens sites in **per‑site “bubbles”** with isolated cookies, storage, and identity
  - Smooths mouse/keystroke patterns automatically
  - Randomizes window sizes within common resolutions

4.1.2 For each move, answer:

- What is the **most we can do** from an app / system extension, without rooting / jailbreaking / violating store policies?
- Which existing apps prove this level is acceptable (e.g., 1Blocker, Lockdown, Mullvad Browser, iCloud Private Relay, AdGuard, etc.)?

4.1.3 Design **three preset modes** a user can select in 1 tap:

- “Normal” – safe, minimal friction
- “Private” – stronger blocking, some breakage allowed
- “Paranoid” – maximum obfuscation, some sites/apps may not work

For each mode, give a simple explanation and list which underlying protections toggle.

### 4.2 Diary – Experience Ledger Without Saying “Merkle”

4.2.1 Define what Mirage will **actually store** for a normal user, per day, per device:

- Example bundle:
  - App timeline (which app, when, for how long)
  - Website cards (domain, page title, time spent, “purpose” tag inferred by AI)
  - Optional: blurred screenshots every N minutes, or on “events” (checkout, signing in, sending money)
  - Network card: “Device talked to these companies from these countries”
  - Consent cards: “You clicked ‘Accept’ on these Terms / cookies / trackers”
  - Influence cards: “These 3 posts used engagement tricks / outrage framing”

4.2.2 For each card type:

- Explain **how we’d capture it** on:
  - iOS / Android (foreground service, VPN, accessibility, notifications, etc.)
  - macOS / Windows (helper app, browser extension, OS APIs)
- Clarify storage:
  - Default: **on‑device, end‑to‑end encrypted**
  - Optional: encrypted cloud backup (iCloud / Google Drive / our storage) – with keys only on user devices

4.2.3 Translate cryptographic guarantees into user language:

- Instead of “Merkle tree + hardware attestations”, write UX copy like:
  - “Moments are sealed with a hardware lock inside your phone. If anyone – even us – tried to change them later, your app would show a big red ‘Tampered’ warning.”

4.2.4 Specify **what never leaves the device** under any circumstance (by design, not by policy) and how to prove that in an audit.

### 4.3 Agent – “Intelligence, but for Individuals”

4.3.1 Define 5–8 **everyday stories** where Mirage’s Agent helps a normal user, for example:

- “What did I actually agree to with this loan / subscription?”
- “Why am I suddenly getting weird ads about X?”
- “Did my ex / employer / landlord try to stalk me?”
- “Show me where this app has been sending my data.”
- “Summarize what companies learned about me this week – and help me erase some of it.”

For each story:

- Show **which telemetry** the Diary already captured.
- Show **how the Agent stitches it** into a human‑readable timeline or explanation.
- Show **what one‑click actions** the user can take (e.g., send deletion requests, revoke permissions, change privacy mode for that app/site, auto‑fill opt‑out forms).

4.3.2 Clarify **where AI runs**:

- Which models must run **on‑device** (no raw logs leave)
- Which anonymized summaries/statistics could be optionally sent to the cloud (opt‑in only)

Design this so:

- A non‑technical user never sees words like “LLM”, “weights”, “embeddings”.
- They only see: “Local brain” vs “Cloud help (never sees your raw moments)”.

---

## 5. Personas & False Identities – But 1‑Tap Simple

Mirage must implement **“phantom personas”** and **compartmentalized identities** that:

- Break linkage between apps/accounts
- Are manageable by a normal person in 2 minutes a week

5.1 Design a **persona system** explained like this to a user:

> “Think of your life as three outfits: Home, Money, and Ghost.
>  We never let a website or app see you in more than one outfit.”

Propose 3–6 **default personas** (e.g. Home, Work, Shopping, Dating, Activist, Ghost).

For each:

- What it changes automatically:
  - IP / VPN profile
  - Browser profile (cookies, extensions, fingerprint cohort)
  - Email / phone alias set
  - Payment method (virtual card)
  - Location behavior (real vs blurred vs fake city)
- How a user **switches** personas:
  - On mobile – system share sheet? Notification quick toggle?
  - On desktop – menu bar tray, browser button?

5.2 Define the **rules engine** in human language:

- Example: “Never let Shopping persona see your real email or phone. Never let Ghost persona touch your real name or photo. Never open bank in Ghost persona.”

5.3 Address **stylometry and writing style**:

- Propose a “Safe Post” button:
  - User writes naturally → Mirage’s on‑device model rephrases just enough to break style fingerprint, but keeps meaning.
  - Explain how you’d do this **without** making text feel robotic or suspicious.

---

## 6. “Break the Links” – Concrete Anti‑Exploitation Design

Using the Path B notes, systematically answer:

6.1 **List all known fingerprint surfaces** that can be influenced from an app or extension:

- Browser: user agent, canvas, WebGL, fonts, window size, timezone, language, audio, WebRTC, etc.
- Device: model, OS version, locale, input methods, motion sensors.
- Network: IP, ASN, TLS fingerprint, SNI, DNS.
- Behavior: typing patterns, mouse/touch curves, scroll style, session timing.

For each, specify:

- Whether Mirage can:
  - **Normalize** (make the user look like millions of others)
  - **Randomize inside a safe cohort**
  - Only **observe and warn**

6.2 Design a **“Privacy Health” screen** that shows, in dead‑simple visuals:

- A score (0–100)
- What’s currently linking them (e.g., “Same email reused on 12 sites”, “Your IP stays the same for all apps”, “Facebook & bank both see the same phone number”).
- Two big buttons:
  - “Fix it for me” (auto‑alias, auto‑VPN, auto‑permission changes)
  - “Explain” (natural language walkthrough plus “learn more” links for geeks)

6.3 Integrate **influence detection**:

Leverage the telemetry to do:

- Live flagging: “This ad/article is using [X pattern]: urgency + outrage + one‑sided framing.”
- End‑of‑day recap: “Here’s where someone tried hardest to push you: 7 TikToks, 3 ads, 1 email.”

Specify:

- How you’d detect this with on‑device or privacy‑preserving ML.
- How you’d present it **without sounding paranoid** or political.

---

## 7. Data Monetization – Only if It Serves the User

The experience ledger is insanely rich. Deep‑dive how to turn it into **self‑realized value** *without* turning Mirage into another data broker.

7.1 Explore **3–5 monetization archetypes** that a non‑technical user could grasp and control, for example:

- “Get cheaper insurance if you choose to share a *proof* that you drive safely – not your full logs.”
- “Sell proof that you really watched 100 hours of a language course – earn a certificate or rewards.”
- “License a safe, anonymized ‘digital twin’ of yourself for UX research – earn royalties without exposing your real life.”

For each:

- What **proof** the Experience Ledger generates.
- How it is **shared** (ZK proof, VC, or similar – but explain in human terms).
- How Mirage **enforces**:
  - The buyer never gets raw logs.
  - The user can revoke future use.
  - The user sees a clear $$ or benefit and can say no.

7.2 Explicitly rule out dark patterns:

- No “sell your soul” switch.
- No default monetization.
- User must understand, in one short paragraph, what they’re giving and getting.

---

## 8. Architecture – But With Guard Rails

Now drop into **serious technical detail**, but always tie it back to “mobile/desktop‑only” and “non‑technical user”.

8.1 Propose a **clean architecture diagram** (Mermaid) for:

- Mobile apps (iOS / Android)
- Desktop apps (macOS / Windows)
- A minimal cloud coordination layer (updates, relays, optional encrypted backup)
- No backend ever sees raw user diary content.

8.2 For each platform, list:

- Languages / stacks you recommend (e.g., Swift + Network Extension, Kotlin + VpnService, Electron vs native, etc.)
- Extension points:
  - VPN / DNS proxy
  - Browser extension APIs (Chrome/Edge/Firefox/Safari)
  - OS accessibility / notification listeners
  - System‑wide “share” / “Open with Mirage” hooks

8.3 Cryptography:

- Choose concrete primitives & libraries (e.g., XChaCha20, libsodium, OS keychains, Secure Enclave / StrongBox / TPM).
- Define key hierarchy:
  - Device keys
  - Persona keys
  - Backup keys
- Define how keys are created, rotated, and **never** leave the user’s control.

8.4 Performance & battery:

- Give target budgets (CPU %, battery per hour, network overhead).
- Propose sampling strategies to keep diaries useful without crushing storage.

---

## 9. UX: From “Install” to “Holy Shit, I’m Safer”

9.1 Design the **first 10 minutes** with Mirage for someone like:

- A 19‑year‑old on TikTok, tired of being watched.
- A 45‑year‑old parent worried about kids’ privacy.
- A journalist/activist in a risky country (advanced mode).

Script:

- The screen sequence
- The stories you tell
- The 3 questions you ask the user
- The 2 “wow” moments you can honestly deliver on day 1

9.2 Design:

- A **weekly email / in‑app digest** that:
  - Shows what Mirage blocked
  - Shows 1–3 insights from their Diary
  - Suggests 1 simple action to improve privacy

Everything must be comprehensible without any technical vocabulary.

---

## 10. Legal, Ethical, and Store Compliance

10.1 Analyze:

- App Store & Google Play policies that constrain:
  - VPNs
  - Accessibility usage
  - Recording / overlay / logging features
- Show how Mirage can push right up to the line **without crossing it.**

10.2 Ethics:

- Enumerate worst‑case abuses *by* users (fraud, impersonation, disinformation using personas) and *against* users (Mirage data subpoena, device seizure, abusive partner installing Mirage covertly).
- For each, specify:
  - Design‑time mitigations (no stealth mode, local encryption, plausibly deniable modes, etc.).
  - Clear positions in the white‑paper.

---

## 11. Competitive and “Beyond Best” Benchmark

11.1 Compare Mirage to:

- Tor Browser / Mullvad Browser
- 1Password / Proton Pass (aliasing)
- iCloud Private Relay
- Lockdown / AdGuard / privacy VPNs
- DeleteMe / PrivacyHawk / data‑removal services
- Brave Browser’s privacy stack

For each:

- What they already do incredibly well (respect them).
- Where Mirage must **go beyond** in:
  - Integration (all‑in‑one)
  - Verifiable personal history
  - Influence detection
  - Persona/identity compartmentalization
  - Non‑technical UX

11.2 Identify **at least 5 places** where our current assumptions are probably wrong or too timid. For each, propose a bolder alternative and mark them **RISK‑TO‑VALIDATE**.

---

## 12. Deliverables & Style

Your output should be:

1. A **single, cohesive technical white‑paper** (~12–15k words) structured with clear headings that follow this brief.
2. Diagrams in **Mermaid** where helpful.
3. User‑facing concepts explained in **plain, non‑technical language**, with technical appendices as needed.
4. A short **“Executive Summary for a normal person”** (≤ 700 words) at the top.
5. A final **“If we build only 3 things in the next 6 months, they should be…”** section, with rationale.

Tone:

- Ruthlessly clear.
- No buzzword soup.
- Assume the reader is smart, impatient, and allergic to bullshit.

If a choice would force the average user to learn a new technical term, **find a different design** or bury the complexity behind Mirage’s UI and automation.

---

END OF PROMPT

