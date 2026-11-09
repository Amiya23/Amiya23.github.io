# Amiya23.github.io

Personal portfolio for Dhiandra Pradika, a full-stack developer in East Jakarta.
One page, no build step: `index.html` carries its own CSS and a small inline script.

Live: https://amiya23.github.io

## What is on the page

- Hero with portrait, stack, availability and a bottom rail (five web apps, two Android apps, source).
- **Web** section: five project cards plus one tile linking to the GitHub profile.
- **Mobile** section: two offline-first Kotlin apps.
- Contact band with email, CV download and footer links.

Every project card carries a real screenshot in `images/cards/` and links to its repository.

## Files

```text
index.html                    the whole site, styles inline
DESIGN.md                     design decisions and the reasons behind them
assets/CV_Dhiandra_Pradika.pdf
images/cards/*.jpg            1200x750 previews, one per project
images/1772605278661.jpg      portrait
images/favicon.*              icon set, indigo tile with a cream serif D
images/og-preview.png         1200x630 share card
images/site.webmanifest       PWA manifest
```

## Run locally

No build step. Any static server works:

```bash
python -m http.server 8777
# then open http://127.0.0.1:8777/index.html
```

## Editing a project card

Copy an existing `<li class="card">` block and change four things: the repo URL,
the `src` of the preview image, the title, and the one sentence under it.
Descriptions state a mechanism, not an adjective: "login throttled to 5 tries a minute"
rather than "secure authentication". Keep them traceable to the repository README.

## Deployment

Push to `main`. GitHub Pages serves the repository root as-is.
