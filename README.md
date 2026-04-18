# DealerDeck marketing site

Static landing page (`index.html` + `assets/`).

## Local preview

```bash
npm install
npm run dev
```

Open [http://localhost:4321](http://localhost:4321).

If that port is busy, `serve` may pick another port; check the terminal output.

## Deploy on Vercel

1. Push this folder to a GitHub repository (see below).
2. In [Vercel](https://vercel.com), **Add New… → Project** and import the repository.
3. Use the defaults: **Framework Preset** “Other”, **Root Directory** `.`, **Build Command** empty, **Output Directory** empty. Vercel serves static files from the repo root.

`vercel.json` is included for optional URL settings; deployment works without a build step.

CLI (optional): from this folder, run `npx vercel` and follow the prompts to link the project.

## GitHub

[GitHub CLI](https://cli.github.com/) (`gh`) is recommended. After [installing `gh`](https://cli.github.com/), sign in once:

```bash
gh auth login
```

Create a new public repo, set `origin`, and push `main` (run from this project folder):

```bash
gh repo create dealerdeck-site --public --source=. --remote=origin --push
```

Use another repo name if `dealerdeck-site` is taken. If the repo already exists on GitHub, add the remote and push instead:

```bash
git remote add origin https://github.com/YOUR_USER/YOUR_REPO.git
git push -u origin main
```
