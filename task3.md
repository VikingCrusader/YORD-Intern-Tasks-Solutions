# Task 3 — Future Prague (WebAR) — Test Plan & Report Structure

**Tester:** Yiwen Zhang
**App under test:** Future Prague — WebAR city promotion experience
**Platform notes:** Built on 8th Wall + A-Frame (confirmed via page metadata)

---

## 1. Test Scope

This is a manual functional QA pass on a mobile WebAR experience. No code changes or debugging are involved — the goal is to verify the user journey end-to-end, across the five landmark scenarios, and document anything unexpected.

### Devices / Browsers to cover
| # | Device | Browser | Notes |
|---|--------|---------|-------|
| 1 | _(fill in phone model)_ | Safari | Primary pass |
| 2 | _(same phone)_ | Chrome | Cross-browser check |

### Environment conditions to note per session
- Time of day / lighting (affects camera tracking)
- Weather (rain/glare can affect tracking)
- Network condition (Wi-Fi vs mobile data, signal strength)

---

## 2. Test Cases

### 2.1 Entry Flow
| ID | What to test | How to test | Expected result |
|----|--------------|--------------|------------------|
| T1.1 | QR code scan launches experience | Scan the physical/printed QR code (or open the link directly if no poster available) | Browser opens and loads the experience without errors |
| T1.2 | Camera/location permission prompts | Observe permission dialogs on first load | Clear, standard OS prompts for camera and location; app explains why if needed |
| T1.3 | Permission denial handling | Deny camera or location permission once, then retry | App shows a clear message/fallback instead of a blank screen or crash |
| T1.4 | Load time | Time from link open to interactive experience | Loads within a reasonable time (note actual seconds); loading indicator shown if slow |

### 2.2 Interactive Map / Navigation
| ID | What to test | How to test | Expected result |
|----|--------------|--------------|------------------|
| T2.1 | Map displays all 5 landmarks | Open map view | All 5 locations visible and correctly labeled |
| T2.2 | Current location accuracy | Compare blue dot / marker to actual physical position | Marker position roughly matches real-world location (allow for normal GPS margin) |
| T2.3 | Navigation guidance to next landmark | Follow in-app directions toward a landmark | Guidance updates as you move; doesn't point in the wrong direction |
| T2.4 | Out-of-order visits | Intentionally visit a landmark that isn't "next" in the suggested sequence (e.g., go to landmark 3 before 1 or 2) | App still triggers the correct scenario and updates progress correctly, regardless of order |
| T2.5 | Language / localization | Check default language on load; look for a language switch option if present | Default language is clear; Czech-specific characters (háček, čárka) render correctly if Czech is shown; no obvious mistranslations |

### 2.3 Landmark AR Scenarios (repeat per landmark)
| ID | Landmark | What to test | How to test | Expected result |
|----|----------|--------------|--------------|------------------|
| T3.1 | Staroměstská | Personalized ad generation | Approach the landmark, trigger AR scene | Ad content loads and displays correctly, anchored to the real-world scene |
| T3.2 | Law Faculty | Cooling biotech grass growth | Approach the landmark, trigger AR scene | Grass visual/animation renders correctly, anchored properly, no clipping |
| T3.3 | Náměstí Republiky | Delivery drone tracking | Approach the landmark, trigger AR scene | Drone model tracks/animates as described, doesn't glitch or disappear unexpectedly |
| T3.4 | _(Landmark 4 — TBD on site)_ | | | |
| T3.5 | _(Landmark 5 — TBD on site)_ | | | |
| T3.6 | Trigger radius / edge behavior | Approach each landmark from different angles/distances | AR scene triggers at a consistent, reasonable distance; doesn't trigger too early/late or double-trigger |
| T3.7 | Re-visiting a landmark | Walk away and return to an already-visited landmark | App handles a repeat visit gracefully (re-shows content, or clearly indicates it's already been seen) |
| T3.8 | Tracking stability | Move phone slowly while AR content is displayed | Virtual content stays anchored, doesn't jitter or drift significantly |
| T3.9 | Occlusion / lighting edge cases | Test in direct sunlight, shade, and if possible near reflective surfaces (glass, water) | Tracking degrades gracefully (or shows a prompt) rather than crashing or rendering garbage |

### 2.4 Closing / Call-to-Action
| ID | What to test | How to test | Expected result |
|----|--------------|--------------|------------------|
| T4.1 | Completion state after all 5 landmarks | Finish visiting all landmarks | App clearly indicates completion |
| T4.2 | Call-to-action link to Prahainovační website | Tap the closing CTA | Opens the correct website, in a new tab if applicable, without errors |

### 2.5 General / Cross-Cutting
| ID | What to test | How to test | Expected result |
|----|--------------|--------------|------------------|
| T5.1 | App backgrounding / interruption | Receive a call or switch apps mid-experience, then return | App resumes correctly, doesn't crash or lose progress |
| T5.2 | Poor network conditions | Test with weak signal or airplane mode toggled briefly | Reasonable error handling/loading state, not a silent failure |
| T5.3 | Battery/performance over time | Note phone temperature/battery drain after ~15–20 min of use | No excessive heating or major performance degradation |
| T5.4 | Orientation | Rotate phone between portrait/landscape (if supported) | Layout adapts or is intentionally locked without breaking |
| T5.5 | Re-entering after fully closing the app | Fully close the browser tab, then reopen the link later | Progress is either preserved or the app clearly restarts from a sensible state (not a broken/partial one) |

---

## 3. Report Structure (to fill in after testing)

### Status Update
- Testing scope: which test cases above were executed
- Device/browser combinations used
- Environment conditions during testing (time, weather, lighting)
- Features that performed solidly

### Bug Documentation
For each issue found:

| Field | Description |
|-------|--------------|
| ID | Sequential bug number |
| Title | One-line summary |
| Severity | Critical / High / Medium / Low |
| Steps to Reproduce | Numbered steps |
| Expected Result | What should happen |
| Actual Result | What actually happened |
| Environment | Device, browser, location, conditions |
| Notes/Screenshots | Supporting evidence |

---

## Time Consuming

_(To be filled in with Clockify screenshot after testing.)_