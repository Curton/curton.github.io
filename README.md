# curton.github.io

Personal page for [github.com/curton](https://github.com/curton), live at
**https://curton.github.io/**. Shows the profile header and pinned projects
in light/dark themes (follows the system setting; toggle in the top-right).

## How it stays fresh

`index.html` is generated from live GitHub data by `scripts/build-page.mjs`
(profile: name, bio, location, counts; each pinned repo: description,
language + color, stars, topics). The [workflow](.github/workflows/refresh-page.yml)
regenerates it every Monday 00:00 UTC and commits the result if anything
changed — a push then rebuilds GitHub Pages automatically. It can also be
triggered manually from the repo's **Actions** tab ("Refresh page data" →
**Run workflow**).

The script uses the workflow's built-in `GITHUB_TOKEN`, so no personal access
token is stored anywhere. Repo descriptions that read poorly as plain text
(null, or containing markdown) are replaced via the `OVERRIDES` map in the
script; everything else comes straight from the API.

## Local development

```bash
GH_TOKEN=$(gh auth token) node scripts/build-page.mjs   # regenerate index.html
# edit, commit, push — Pages rebuilds in ~1 min
```

The theme toggle cycles **follow system → light → dark** and remembers the
choice in `localStorage` (key `theme-mode`).
