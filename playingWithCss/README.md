# Playing With CSS — Notes for Future Me

This is a short, practical guide for future-you when you come back to revise or extend this tiny experiment.
Put this at the top of your brain: the app demonstrates updating CSS custom properties from JS to change UI styling live (spacing, blur, and base color).

Project entry: [index.html](/home/buetoid/JavaScript30/playingWithCss/index.html)

---

What this is (1 line)

- A minimal interactive demo that uses inputs to update CSS variables (declared on :root) and shows the effect on an image and inline highlight.

Why it exists (reminder)

- Quick playground for CSS variables + JS. Useful when experimenting with themes, live controls, or building a simple visual editor.

Quick start (get back into it fast)

1. Open the file in a browser: double-click [index.html](/home/buetoid/JavaScript30/playingWithCss/index.html) or serve the folder:
   - python -m http.server 8000
   - open http://localhost:8000/playingWithCss/index.html
2. Inspect the controls and the small script at the bottom. The handler updates CSS variables with document.documentElement.style.setProperty.

Files to inspect

- index.html — single-file demo; CSS vars live in :root; tiny inline script handles inputs.

Short technical notes / gotchas

- Range inputs include data-sizing="px" — handler appends that suffix so values become e.g. "10px".
- Color input writes raw hex ("#ffc600") to --base.
- The script listens for both `change` and `mousemove` so sliders update continuously while dragging.
- If scoping is needed later, change document.documentElement to a container element (e.g., `const container = document.querySelector('.demo')`).

Revision checklist (prioritized, bite-sized tasks)

1. Extract JS & CSS (HIGH)
   - Create `script.js` and `styles.css`, move inline code there, update index.html links.
   - Sanity-check in browser.
   - Commit on branch `feat/extract-assets` with message: "Extract inline CSS/JS to files — improves maintainability".

2. Add live labels + presets (MEDIUM)
   - Show numeric values beside sliders (bind input events and update <output> elements).
   - Add a small preset toolbar that sets multiple CSS vars in one click.
   - Branch: `feat/presets-and-labels`.

3. Persist state (MEDIUM)
   - Save the last-used values to localStorage on change; read them on load and apply to inputs and CSS variables.
   - Branch: `feat/persist-settings`.

4. Scope variables to a container (LOW)
   - Wrap the image + controls in a `.demo` container and set variables on that element so multiple widgets can coexist.
   - Branch: `refactor/scoped-variables`.

5. Accessibility pass (LOW)
   - Ensure labels are linked, add aria attributes, keyboard-focus styles, and visible focus outlines.
   - Add contrast warning when base color produces low contrast with text.

6. Optional: Add presets sharing (LOW)
   - Export/import preset JSON or generate shareable URL query string.

Testing / quick validation steps

- After each change, open index.html and verify:
  - Sliders move and update image spacing/blur immediately.
  - Color input updates the highlight and background color.
  - If extracting files, check the console for 404s and correct script order.

Example commands (git)

- Start a feature branch:
  - git checkout -b feat/extract-assets
- Commit changes:
  - git add .
  - git commit -m "Extract inline CSS/JS to files — improves maintainability"
- Push and open a PR as usual.

Changelog template (paste when making changes)

- YYYY-MM-DD — <short summary>
  - Files changed: <list>
  - Notes: <one-line notes about behavior or gotchas>

Notes-to-self: implementation hints

- Persistent settings example (on change):

```js
const settingsKey = "pwcss-settings";
function saveSettings(values) {
  localStorage.setItem(settingsKey, JSON.stringify(values));
}
function loadSettings() {
  try {
    return JSON.parse(localStorage.getItem(settingsKey)) || null;
  } catch (e) {
    return null;
  }
}
```

- Scoping example: replace document.documentElement.setProperty with container.style.setProperty.

- Live labels: use <output for="id"> or a small <span class="value"> and update textContent on input events.

When you revisit — suggested order

1. Run a quick smoke test locally (open the page).
2. If everything works, extract inline assets (this is small and low-risk).
3. Add persistence and live value labels.
4. Add presets and sharing if you want to save configurations.
5. Accessibility and polishing last.

Next immediate action (pick one)

- Extract assets to files (recommended first). Reply "extract" and I'll do it now.
- Or reply with one of: "persist", "presets", "scope", "a11y" and I'll implement that feature next.

Final tiny checklist for the commit

- Use a descriptive branch name.
- Make focused commits for each logical change.
- Add a short changelog entry and update this README with the changelog line.

---

If you want the first action done now, say which one (extract, persist, presets, scope, a11y) and it will be implemented and committed to a branch with a short commit message.
