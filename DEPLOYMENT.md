# ZWAIGZNE 6.2 deployment

This package contains a standalone `index.html` and a GitHub Actions workflow at `.github/workflows/deploy-pages.yml`.

## One-time setup

1. Upload the extracted package contents to the root of `laurisin/zwaigzne` (preserve the `.github/workflows/` folder).
2. In GitHub, open **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **GitHub Actions** (not “Deploy from a branch”).
4. Commit the files to `main`.
5. Open the **Actions** tab and check that **Deploy ZWAIGZNE to GitHub Pages** completes successfully.
6. The public site remains `https://laurisin.github.io/zwaigzne/`.

## Future releases

Replace the root `index.html` (and `brand-logo.png` if changed) with the new release and commit to `main`. The workflow automatically builds and deploys the site. You can also run it manually from **Actions → Deploy ZWAIGZNE to GitHub Pages → Run workflow**.

The workflow publishes only `index.html` and `brand-logo.png`; documentation and ZIP files are not copied to the public site.
