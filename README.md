# Connor Parsons — CV

Personal CV, published as a single-page site with a downloadable PDF.

## Layout

| Path | Purpose |
|------|---------|
| `index.html` | The CV web page (self-contained, no build step) |
| `main.tex` | LaTeX source for the PDF CV ([Simple Hipster CV](https://github.com/latex-ninja/simple-hipster-cv) template) |
| `simplehipstercv.cls` / `simplehipstercv.sty` | Vendored template class/style |
| `portrait-cv.jpg` | Portrait used by the LaTeX CV |
| `assets/portrait.webp` | Portrait used by the web page |
| `Connor-Parsons-CV.pdf` | Committed PDF build (fallback; CI serves a fresh build on deploy) |

## Building the PDF locally

Requires a TeX Live installation with `paracol`, `fontawesome`, `raleway`,
`smartdiagram`, and `titlesec` (on Debian/Ubuntu: `texlive-latex-extra`,
`texlive-pictures`, `texlive-fonts-extra`).

```sh
pdflatex main.tex   # or: latexmk -pdf main.tex
cp main.pdf Connor-Parsons-CV.pdf
```

## CI / deployment

`.github/workflows/build-and-deploy.yml`:

- **Pull requests** — compiles `main.tex` to catch broken LaTeX, and uploads
  the PDF as a workflow artifact for preview.
- **Pushes to `main`** — additionally deploys the site (`index.html`, assets,
  and the freshly built PDF as `Connor-Parsons-CV.pdf`) to GitHub Pages.

The workflow enables/updates GitHub Pages automatically
(`actions/configure-pages` with `enablement: true`). If the deploy job ever
fails with a Pages configuration error, set **Settings → Pages → Source** to
**GitHub Actions** once and re-run it.
