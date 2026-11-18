# GitHub deployment — quick guide

### First deployment
1. Create a **public** GitHub repository named `zwaigzne` (or another name you prefer).
2. Upload every file in this package to the repository root.
3. Go to **Settings → Pages**.
4. Select **Deploy from a branch → main → /(root)** and save.
5. Open the URL GitHub Pages provides.

### How we develop from here
1. Keep `main` as the working stable version.
2. Create a branch for each change (`fix/...`, `feature/...`).
3. Make and test changes in the branch.
4. Commit and open a Pull Request.
5. Review and test on desktop, iPad and phone, then merge to `main`.
6. Tag each tested milestone (`v6.1.1`, `v6.2.0`, etc.).

### For feedback
Report the version, device/browser, page, exact steps, expected result and actual result. Include a screenshot or short screen recording where useful. Do not overwrite `main` with an untested experiment.

### Local preview
Run `python -m http.server 8000` in the repository folder and visit `http://localhost:8000`.
