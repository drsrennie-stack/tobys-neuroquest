# NeuroQuest, Anatomy Mastery Challenge

An adaptive, self-contained study game for BIO 004 Human Anatomy (Week 7 and Week 8: nervous system). One HTML file, no build step, no dependencies beyond Google Fonts.

Built from BIO 004 Week 7 and Week 8 notes. Dr. Sharilyn Rennie, Solano Community College.

## What it does

- 100 questions across three Depth of Knowledge levels (DOK 1 Recall, DOK 2 Apply, DOK 3 Reason) and ten nervous-system topics.
- Adaptive rounds: each round blends fresh questions with your weak spots (about half and half), in a fresh random order every time. Turn this off in Settings for a straight shuffle.
- Weakness dashboard: names your weak topics, counts what is due to remaster, and drills them on demand.
- Study mode, Challenge mode (timed, XP bonus, explanations held to the round summary), timer, sound, XP, streaks, and badges.
- Progress is saved in the browser via localStorage. Nothing leaves the device.

## Files

- `neuroquest.html` , the complete app.
- `compliance-notes.md` , WCAG 2.2 AA accessibility record for this build.

## Run it

Open `neuroquest.html` in any modern browser. That is the whole thing.

## Host on GitHub Pages

With Pages enabled on this repo, the app is served at:

```
https://drsrennie-stack.github.io/Solano-Anatomy-/neuroquest.html
```

(adjust the path if you place the file in a subfolder.)

## Embed in Kajabi

Use an iframe pointing at the Pages URL:

```html
<iframe src="https://drsrennie-stack.github.io/Solano-Anatomy-/neuroquest.html"
        style="width:100%; border:0;" title="NeuroQuest" loading="lazy"></iframe>
```

The page posts its height to the parent window (`postMessage`, type `neuroquest-resize`), so a height-listener on the Kajabi side can size the iframe to the content. Note: browsers may block localStorage inside a cross-origin iframe, in which case the game still runs but progress will not persist. Hosting the page same-origin avoids that.

## Accessibility

WCAG 2.2 AA is the floor, AAA on color contrast where achievable. Full keyboard operation, visible focus, live-region answer feedback, semantic landmarks, and reduced-motion support. See `compliance-notes.md` for the criterion-by-criterion record.

## Editing the question bank

Questions live in the `<script>` block near the top, added with `add(level, topic, question, choices, correctIndex, why, wrongs, trick, clinical)`. `correctIndex` is 0-based into `choices`. `wrongs` holds one explanation per choice. Keep answer text unique within a question.
