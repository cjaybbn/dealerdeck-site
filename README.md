# DealerDeck marketing site

Static landing page (`index.html` + `assets/`).

## Local preview

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## Deploy on Vercel

1. Push this folder to a GitHub repository.
2. In [Vercel](https://vercel.com), import the repository.
3. Use the defaults: **Framework Preset** “Other”, **Root Directory** `.`, no build command. Vercel serves the static files from the repo root.

`vercel.json` is included for optional URL settings; deployment works without a build step.

## GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USER/YOUR_REPO.git
git push -u origin main
```

Replace `YOUR_USER` and `YOUR_REPO` with your GitHub account and repository name.
