# Setup Guide

This repo is a **GitHub profile README** — it only works if the repo name matches your username exactly: `hopcofficial/hopcofficial`. If you haven't created it yet: create a new *public* repo named `hopcofficial` on your account, GitHub will auto-detect it as your profile repo.

## 1. Push the project

```bash
cd hopcofficial-profile
git remote add origin https://github.com/hopcofficial/hopcofficial.git
git add .
git commit -m "init: profile v1"
git branch -M main
git push -u origin main
```

## 2. Enable Actions permissions

Both workflows commit files back to the repo, so Actions needs write access:

1. Go to **Settings → Actions → General**
2. Under **Workflow permissions**, select **Read and write permissions**
3. Save

Without this step, `snake.yml` and `metrics.yml` will run but fail silently on the push/commit step.

## 3. Add the `METRICS_TOKEN` secret

`metrics.yml` (the activity graph + stats workflow) needs a personal access token with `repo` and `read:user` scopes — the default `GITHUB_TOKEN` doesn't have enough permission for cross-account stats.

1. Go to **github.com/settings/tokens** → **Generate new token (classic)**
2. Scopes: `repo`, `read:user`
3. Copy the token
4. Go to your repo → **Settings → Secrets and variables → Actions → New repository secret**
5. Name: `METRICS_TOKEN`, value: the token you copied

`snake.yml` does **not** need this — it uses the default `GITHUB_TOKEN`.

## 4. First run

Both workflows also run on `workflow_dispatch`, so you don't have to wait for the schedule:

- Go to **Actions** tab → select **Generate Snake Animation** → **Run workflow**
- Go to **Actions** tab → select **Generate Activity Graph & Dynamic Stats** → **Run workflow**

The snake workflow publishes to an `output` branch (created automatically) — that's why the README points to:
```
https://raw.githubusercontent.com/hopcofficial/hopcofficial/output/dist/snake-dark.svg
```

The metrics workflow commits directly to `assets/activity-graph.svg` on `main`.

## 5. Swap the project cards

`assets/project-card-1.svg` and `assets/project-card-2.svg` are placeholders. Each is a plain SVG — open it in a text editor and change:

- `FILE_01 · REPLACE ME` label
- Project name (large text)
- Description lines
- Tech stack tags
- Status line + status dot color (`#C81E3A` = active, `#4C9A5A` = shipped, `#B8933E` = paused)

Keep the same `viewBox` (`430 220`) if you want new cards to line up in the two-column table in `README.md`.

To add a third card, duplicate one of the SVGs, then extend the `<table>` in `README.md` with another `<td>`, or start a new row.

## 6. Update contact info

In `README.md`, update:
- The Discord invite link (currently a placeholder `https://discord.gg/`)
- The X/Twitter badge link if the handle ever changes

## 7. Optional: color tuning

The palette used throughout:

| Token | Hex | Use |
|---|---|---|
| `bg` | `#0A0A0C` | Background |
| `bg-alt` | `#131316` | Card background |
| `text` | `#EDEAE3` | Primary text |
| `muted` | `#6B6B72` | Secondary text |
| `line` | `#1A1A1E` | Borders / dividers |
| `crimson` | `#C81E3A` | Primary accent |
| `gold` | `#B8933E` | Secondary accent |

If you change these, update them consistently across `assets/*.svg` and the query-string colors in the `github-readme-stats` / `streak-stats` image URLs in `README.md`.
