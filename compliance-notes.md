# Accessibility compliance notes

**Project:** NeuroQuest, Anatomy Mastery Challenge (BIO 004)
**Files covered:** neuroquest.html
**Date:** 2026-08-01
**Reviewer:** Dr. Sharilyn Rennie

## 1. Scope

Single self-contained HTML study game. Runs standalone or embedded in a Kajabi or GitHub Pages iframe. This build fixes the accessibility gaps found in the prior audit and adds an adaptive question engine. Notes below reflect the corrected build.

## 2. WCAG version and target level

Target: WCAG 2.2 Level AA as the floor, Level AAA for color contrast where achievable.

| Criterion | Level | Status |
|-----------|-------|--------|
| 1.3.1 Info and Relationships (semantic landmarks, headings, roles) | A | Pass |
| 1.4.3 Contrast (Minimum) | AA | Pass |
| 1.4.6 Contrast (Enhanced) | AAA | Pass on all primary text, near-pass on two small-text pairs (see section 3) |
| 1.4.11 Non-text Contrast (controls, focus) | AA | Pass |
| 2.1.1 Keyboard | A | Pass |
| 2.1.2 No Keyboard Trap | A | Pass |
| 2.4.1 Bypass Blocks (skip link) | A | Pass |
| 2.4.7 Focus Visible | AA | Pass |
| 2.5.5 Target Size | AAA | Pass (all controls at least 44px in the smaller dimension or with adequate spacing) |
| 3.2.2 On Input | A | Pass |
| 4.1.2 Name, Role, Value (switches, tabs, buttons) | A | Pass |
| 4.1.3 Status Messages (aria-live feedback) | AA | Pass |
| 2.3.3 Animation from Interactions (reduced motion) | AAA | Pass |

## 3. Color contrast audit

Palette is the existing NeuroQuest neon set on near-black. Ratios computed with the WCAG relative-luminance formula.

| Foreground | Background | Ratio | Normal-text result |
|-----------|-----------|-------|--------------------|
| Body text #e9edf7 | Page #080b14 | 16.78 | AAA |
| Body text #e9edf7 | Card #111827 | 15.14 | AAA |
| Body text #e9edf7 | Choice #161f33 | 14.02 | AAA |
| Muted #8b93ac | Page #080b14 | 6.43 | AA |
| Muted #8b93ac | Card #111827 | 5.80 | AA |
| Muted #8b93ac | Choice #161f33 | 5.37 | AA |
| Teal #49e0d8 | Page #080b14 | 12.11 | AAA |
| Teal #49e0d8 | Choice #161f33 | 10.12 | AAA |
| Amber #f5a623 | Card #111827 | 8.75 | AAA |
| Correct #5fe6a0 | Card #111827 | 11.25 | AAA |
| Incorrect #ff6b7a | Card #111827 | 6.45 | AA |
| Button text #052321 | Teal button #49e0d8 | 10.20 | AAA |
| XP chip text #241500 | Amber chip #f5a623 | 8.76 | AAA |

Every text pair clears AA. The muted-gray and the incorrect-red small-text pairs clear AA but sit below the 7:1 AAA line. They are used only for secondary or decorative labels, never for primary reading content, so the AA pass is sufficient. No changes needed.

## 4. Keyboard navigation flow verified

All interactive elements are native buttons, links, or ARIA controls, reachable by Tab and operable with Enter or Space.

- Skip link is the first focusable element and jumps to the main content region.
- Top bar: Home, Back, Restart, Sound toggle.
- Home menu: six cards, each a button.
- Level select: three level tabs (role=tab, aria-selected), a length segmented control, and Start.
- Question screen: four answer buttons, then Next. Focus moves to the question text when a new question loads, so a keyboard or screen-reader user lands on the prompt.
- Settings: five switches (role=switch, aria-checked) plus Reset.
- Round summary: expandable Full explanations disclosure (native details/summary, keyboard operable), Play again, Home.

No keyboard traps. Focus indicators are visible on every control (2px outline).

## 5. Screen reader testing

Verified programmatically (headless DOM plus ARIA-tree inspection) and by code review:

- Landmarks present: banner (top bar), navigation, main, contentinfo (footer).
- Heading order is correct: one h1 on Home, one h2 per screen, question text is an h2.
- The sound button, tabs, and switches expose correct name, role, and state (aria-pressed, aria-selected, aria-checked update on interaction).
- Answer results announce through an assertive aria-live region ("Correct. Plus 10 XP." or "Incorrect. Correct answer: ...").
- Icon-only sound button has an accessible name that updates with state.

Recommended before wide release: one manual pass with VoiceOver (Safari) and NVDA (Firefox) to confirm announcement timing feels natural. Automated checks cannot fully judge that.

## 6. Known limitations and remediation plan

1. Timer mode is visual only. A screen-reader user in timed or challenge mode gets the result announcement but not a live countdown. Timer is off by default. Remediation if needed: announce the countdown at the 10-second and 5-second marks, or offer an untimed accommodation. Low priority since the mode is optional.
2. The ambient neuron canvas is decorative and marked aria-hidden. Under prefers-reduced-motion it renders one static frame and does not animate.
3. localStorage in a third-party iframe (for example GitHub Pages embedded in Kajabi) may be blocked by browser storage partitioning. The app degrades gracefully (no crash) but progress will not persist in that case. Test in the real embed. If it fails, host the page same-origin or accept session-only progress.

## 7. Reviewer

Dr. Sharilyn Rennie
