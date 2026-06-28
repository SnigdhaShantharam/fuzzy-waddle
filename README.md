# Lean Canvas — Anti-SaaS Custom Software Studio

Interactive lean canvas with shared notes via Supabase. Hosted on GitHub Pages via Jekyll.

## First-time setup (Mac)

### 1. Install dependencies

```bash
gem install bundler
bundle install
```

### 2. Add your credentials

Your `.env` file is already created and ignored by git. It contains your Supabase keys.
To load them into Jekyll when building locally:

```bash
source .env && bundle exec jekyll serve
```

Visit `http://localhost:4000` to preview locally.

### 3. Deploy to GitHub Pages

Push this folder to your `fuzzy-waddle/lean-canvas` repo.
GitHub Pages will build it automatically — no credentials needed in the repo.

**Wait:** GitHub Pages does not run `jekyll-environment-variables` by default.
See the next section.

---

## Passing credentials to GitHub Pages

Since `.env` is not committed, you need to set the Supabase values as
**GitHub Actions secrets** and run a custom build workflow.

### Step 1 — Add secrets to GitHub

Go to: `github.com/fuzzy-waddle/lean-canvas` → Settings → Secrets and variables → Actions → New repository secret

Add these two:
- `SUPABASE_URL` → your Supabase project URL
- `SUPABASE_KEY` → your anon key

### Step 2 — Add the workflow file

Create `.github/workflows/deploy.yml` in your repo with the contents
from the `deploy.yml` file included in this project.

This workflow builds Jekyll with your secrets injected and deploys to Pages automatically on every push.

---

## Local preview

```bash
source .env && bundle exec jekyll serve
```

---

## Notes storage

Notes are saved to Supabase in real time as you type (1 second debounce).
Both founders can have the canvas open simultaneously — notes sync on page load.

The Supabase `anon` key is public by design. Security is enforced via Row Level Security policies on the `notes` table.
