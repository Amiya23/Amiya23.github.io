# amiya23.github.io

Personal portfolio site for Dhiandra Pradika, an informatics student and software developer. Static HTML and CSS with a small inline script, published with GitHub Pages.

Live: https://amiya23.github.io/

## Contents

| Path | Purpose |
|---|---|
| `index.html` | single page portfolio: about, skills, featured project, project grid, contact |
| `style.css` | all styling |
| `assets/CV_Dhiandra_Pradika.pdf` | downloadable CV |
| `images/` | portrait, project preview, favicons, Open Graph image, web manifest |

## How the project grid works

The project cards are not hardcoded. The inline script at the bottom of `index.html` calls the GitHub API for the `Amiya23` account, then renders cards for the repositories listed in the `featuredRepos` array. Two lookup objects next to it control what each card shows:

- `repoTech` maps a repository name to a category and a technology list.
- `repoImages` maps a repository name to a preview image URL.

To feature a different repository, add its name to `featuredRepos` and, if you want a category, a technology list, or a custom preview, add matching entries to `repoTech` and `repoImages`.

## Local preview

No build step and no dependencies. Open `index.html` directly, or serve the folder:

```bash
python -m http.server 8000
```

Then open http://localhost:8000. The project grid needs internet access because it reads the GitHub API.

## Deployment

The repository is named `amiya23.github.io`, so GitHub Pages serves the `main` branch at the root domain. Push to `main` and the site updates. There is no workflow file and nothing to build.

## Editing notes

- Keep the Open Graph and Twitter tags in `index.html` in sync when the title, description, or `images/og-preview.png` changes.
- Fonts come from Google Fonts and icons from the Font Awesome CDN, so both need network access.
- The `?v=` cache busting suffix is not used here, so a hard refresh may be needed after editing `style.css`.
