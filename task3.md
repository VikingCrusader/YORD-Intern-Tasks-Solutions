# Task 3 — Future Prague (WebAR) — Test Plan & Report Structure

**Tester:** Yiwen Zhang
**App under test:** Future Prague — WebAR city promotion experience
**Link:** https://xrview.8thwall.app/future-prague/
**Platform notes:** Built on 8th Wall + A-Frame (confirmed via page metadata)

---

## 1. Test Scope

This is a manual functional QA pass on a mobile WebAR experience. No code changes or debugging are involved — the goal is to verify the user journey end-to-end, across the five landmark scenarios, and document anything unexpected.

### Devices / Browsers to cover

| #   | Device                  | Browser | Notes               |
| --- | ----------------------- | ------- | ------------------- |
| 1   | _(fill in phone model)_ | Safari  | Primary pass        |
| 2   | _(same phone)_          | Chrome  | Cross-browser check |

### Environment conditions to note per session

- Time of day / lighting (affects camera tracking)
- Weather (rain/glare can affect tracking)
- Network condition (Wi-Fi vs mobile data, signal strength)

---

## 2. Test Cases

### 2.1 Entry Flow

| ID   | What to test                       | How to test                                                                          | Expected result                                                                       |
| ---- | ---------------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------- |
| T1.1 | QR code scan launches experience   | Scan the physical/printed QR code (or open the link directly if no poster available) | Browser opens and loads the experience without errors                                 |
| T1.2 | Camera/location permission prompts | Observe permission dialogs on first load                                             | Clear, standard OS prompts for camera and location; app explains why if needed        |
| T1.3 | Permission denial handling         | Deny camera or location permission once, then retry                                  | App shows a clear message/fallback instead of a blank screen or crash                 |
| T1.4 | Load time                          | Time from link open to interactive experience                                        | Loads within a reasonable time (note actual seconds); loading indicator shown if slow |

### 2.2 Interactive Map / Navigation

| ID   | What to test                         | How to test                                                                                                       | Expected result                                                                                                                    |
| ---- | ------------------------------------ | ----------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| T2.1 | Map displays all 5 landmarks         | Open map view                                                                                                     | All 5 locations visible and correctly labeled                                                                                      |
| T2.2 | Current location accuracy            | Compare blue dot / marker to actual physical position                                                             | Marker position roughly matches real-world location (allow for normal GPS margin)                                                  |
| T2.3 | Navigation guidance to next landmark | Follow in-app directions toward a landmark                                                                        | Guidance updates as you move; doesn't point in the wrong direction                                                                 |
| T2.4 | Out-of-order visits                  | Intentionally visit a landmark that isn't "next" in the suggested sequence (e.g., go to landmark 3 before 1 or 2) | App still triggers the correct scenario and updates progress correctly, regardless of order                                        |
| T2.5 | Language / localization              | Check default language on load; look for a language switch option if present                                      | Default language is clear; Czech-specific characters (háček, čárka) render correctly if Czech is shown; no obvious mistranslations |

### 2.3 Landmark AR Scenarios (repeat per landmark)

> **Note:** The task brief's example scenarios (Staroměstská personalized ads, Law Faculty cooling biotech grass, Náměstí Republiky delivery drones) don't fully match what's actually in the live app. The five landmarks confirmed in the app itself are: **Náměstí Republiky, Na Příkopě, Václavské náměstí, Palackého náměstí, and Výtoň.** Test cases below are updated to match the real app; the mismatch with the brief is also logged as a question (see Assumptions & Questions).

| ID   | Landmark                        | What to test                                                                                                                             | How to test                                                                                              | Expected result                                                                                            |
| ---- | ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| T3.1 | Náměstí Republiky               | "Aerospace" — delivery drone overhead (button: "Start AR")                                                                               | Approach the landmark, trigger AR scene, tilt phone toward the sky as prompted                           | Drone model with delivery box tracks/animates correctly overhead, doesn't glitch or disappear unexpectedly |
| T3.2 | Na Příkopě                      | "Culture & Creativity" — camera reveals a historic photo of Na Příkopě to compare with today's view (button: "Start AR")                 | Approach the landmark, trigger AR scene, hold camera up as prompted                                      | Historic photo overlay aligns reasonably with the real street view; no major misalignment or missing image |
| T3.3 | Václavské náměstí               | "Urban Innovation" — 360° reimagined view of Můstek (button: "Start 360° View" — different button label from the others, not "Start AR") | Approach the landmark, trigger the 360° scene                                                            | 360° environment loads and can be looked around fully; no gaps/seams in the panorama                       |
| T3.4 | Palackého náměstí               | "AI" — pick a mood emoji, AI generates a personalized ad (button: "Start AI" — also a distinct button label)                             | Approach the landmark, trigger scene, select an emoji                                                    | A personalized ad is generated and displayed based on the chosen emoji; reasonable response time           |
| T3.5 | Výtoň                           | "Biotech" — tap the floor to grow AR grass patches that "lower temperature" (button: "Start AR")                                         | Approach the landmark, trigger AR scene, tap floor repeatedly                                            | Grass patches appear at tapped locations, anchored to the floor plane, no clipping through real surfaces   |
| T3.6 | Trigger radius / edge behavior  | Approach each landmark from different angles/distances                                                                                   | AR scene triggers at a consistent, reasonable distance; doesn't trigger too early/late or double-trigger |
| T3.7 | Re-visiting a landmark          | Walk away and return to an already-visited landmark                                                                                      | App handles a repeat visit gracefully (re-shows content, or clearly indicates it's already been seen)    |
| T3.8 | Tracking stability              | Move phone slowly while AR content is displayed                                                                                          | Virtual content stays anchored, doesn't jitter or drift significantly                                    |
| T3.9 | Occlusion / lighting edge cases | Test in direct sunlight, shade, and if possible near reflective surfaces (glass, water)                                                  | Tracking degrades gracefully (or shows a prompt) rather than crashing or rendering garbage               |

### 2.4 Closing / Call-to-Action

| ID   | What to test                                 | How to test                   | Expected result                                                       |
| ---- | -------------------------------------------- | ----------------------------- | --------------------------------------------------------------------- |
| T4.1 | Completion state after all 5 landmarks       | Finish visiting all landmarks | App clearly indicates completion                                      |
| T4.2 | Call-to-action link to Prahainovační website | Tap the closing CTA           | Opens the correct website, in a new tab if applicable, without errors |

### 2.5 General / Cross-Cutting

| ID   | What to test                            | How to test                                                  | Expected result                                                                                           |
| ---- | --------------------------------------- | ------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------- |
| T5.1 | App backgrounding / interruption        | Receive a call or switch apps mid-experience, then return    | App resumes correctly, doesn't crash or lose progress                                                     |
| T5.2 | Poor network conditions                 | Test with weak signal or airplane mode toggled briefly       | Reasonable error handling/loading state, not a silent failure                                             |
| T5.3 | Battery/performance over time           | Note phone temperature/battery drain after ~15–20 min of use | No excessive heating or major performance degradation                                                     |
| T5.4 | Orientation                             | Rotate phone between portrait/landscape (if supported)       | Layout adapts or is intentionally locked without breaking                                                 |
| T5.5 | Re-entering after fully closing the app | Fully close the browser tab, then reopen the link later      | Progress is either preserved or the app clearly restarts from a sensible state (not a broken/partial one) |

---

## 2.6 Field Notes (in progress — first session)

**Session 1 — late night, indoor, remote from actual landmarks**

- Confirmed language toggle exists on the location detail page ("en" button) — T2.5 partially verified (toggle present; haven't yet checked actual translation quality/Czech character rendering).
- Opened the "Aerospace" scenario (location: Náměstí Republiky, drone delivery). Tapped "Start AR" while physically located far from Náměstí Republiky (per in-app map, tester was in the Chýnovská/Novodvorská area of Prague 4, well outside the cluster of landmark markers near the river) and indoors, at night.
- **Observation:** The app allowed "Start AR" to proceed and successfully rendered the drone/delivery-box AR scene, with the "Tilt your phone toward the sky" prompt, despite the tester being nowhere near the actual landmark and indoors in low light.
- This raises an open question about intended behavior — see bug/question log below.
- AR rendering itself (drone model, tracking) appeared stable and did not visibly glitch during this test, even indoors at night — worth re-verifying outdoors in daylight at the real location.

**Testing to continue on-site at the actual landmarks (planned for tomorrow).**

### Session 2 — reviewed all 5 landmark detail pages (still remote from the actual sites)

Confirmed the real scenario for each landmark (see updated table in 2.3 above). One notable finding: **the "start" button label is not consistent across landmarks** —

- Náměstí Republiky, Na Příkopě, and Výtoň use **"Start AR"**
- Václavské náměstí uses **"Start 360° View"**
- Palackého náměstí uses **"Start AI"**

This is worth flagging as a UX consistency question rather than a hard bug: if these are genuinely different experience types (AR vs. 360° panorama vs. an AI-driven ad generator), distinct labels may be intentional and helpful. But it's inconsistent enough (3 different verbs/labels across 5 stops) that it's worth confirming with the team whether this is by design or something that drifted during development.

Also confirmed: the task brief's example scenarios (Staroměstská personalized ads, Law Faculty cooling grass) don't match the app at all — in the live app, the personalized-ad scenario is at **Palackého náměstí** (not Staroměstská), and the cooling-grass scenario is at **Výtoň** (not the Law Faculty). Neither Staroměstská nor the Law Faculty appear among the app's 5 actual landmarks. This should be raised as a clarifying question — likely just an outdated brief, but worth confirming rather than assuming.

### Preliminary Bug / Question Log

| ID  | Title                                                       | Severity                            | Steps to Reproduce                                                                                                                                                   | Expected Result                                                                                                                                                                       | Actual Result                                                | Notes                                                                                                                             |
| --- | ----------------------------------------------------------- | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| B1  | AR scenario can be started far from its associated landmark | Medium–High (pending clarification) | 1. Open the "Aerospace" (Náměstí Republiky) scenario detail page while physically located elsewhere (tested from Prague 4, ~far from the landmark) 2. Tap "Start AR" | If proximity to the landmark is intended to be required: app should block/warn instead of starting AR. If a "preview from anywhere" mode is intentional: current behavior is correct. | AR scene launched normally with no location check or warning | Flagging as a question for the team rather than a confirmed bug — need to confirm intended behavior (see Assumptions & Questions) |

---

## 3. Report Structure (to fill in after testing)

### Status Update

- Testing scope: which test cases above were executed
- Device/browser combinations used
- Environment conditions during testing (time, weather, lighting)
- Features that performed solidly

### Bug Documentation

For each issue found:

| Field              | Description                           |
| ------------------ | ------------------------------------- |
| ID                 | Sequential bug number                 |
| Title              | One-line summary                      |
| Severity           | Critical / High / Medium / Low        |
| Steps to Reproduce | Numbered steps                        |
| Expected Result    | What should happen                    |
| Actual Result      | What actually happened                |
| Environment        | Device, browser, location, conditions |
| Notes/Screenshots  | Supporting evidence                   |

---

## Time Consuming

_(To be filled in with Clockify screenshot after testing.)_
