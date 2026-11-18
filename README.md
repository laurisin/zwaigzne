# ZWAIGZNE 6.1 — The Living Circuit

A standalone browser-based experimental drone synthesizer. The application is self-contained in `index.html`; no build step or package installation is required.

## Run locally

Open `index.html` in a modern browser. For best results, serve the folder over HTTP (for example, `python -m http.server 8000`) and open `http://localhost:8000`. Audio starts only after the user interacts with the page.

## Deploy to GitHub Pages

1. Create a new GitHub repository.
2. Upload the contents of this folder to the repository root (not the enclosing ZIP folder).
3. Open **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**.
5. Select `main` and `/ (root)`, then save.
6. Wait for the Pages deployment and open the published URL.

The root `index.html` is the deployment entry point. The standalone `ZWAIGZNE_6_1.html` is included as a second convenient copy.

## Development workflow

- Keep `main` as the stable, deployable branch.
- Make changes on a feature branch, e.g. `fix/gesture-ferment-isolation`.
- Test locally on desktop, iPad and phone; verify audio, touch, gamepad, patch recall and `.zwg` import/export.
- Commit small, focused changes and open a Pull Request into `main`.
- Merge only after testing; GitHub Pages redeploys automatically.
- Tag known-good milestones (for example `v6.1.0`) so a working release can be restored.

## Project contents

- `index.html` — GitHub Pages entry point and complete application.
- `ZWAIGZNE_6_1.html` — named standalone copy.
- `ARCHITECTURE.md` — signal-path and subsystem notes.
- `TEST_REPORT.md` — checks performed and known limitations.
- `DEPLOYMENT.md` — short deployment and contribution workflow.
- `DESIGN_SOURCES.md` — design references used during development.
- `brand-logo.png` — project mark.

## Important

This is a client-side instrument. Patch banks and remembered settings are stored in the browser's local storage; they are not automatically synchronized between devices. Export `.zwg` banks regularly. The sampler's audio buffer is not embedded in patch files.
