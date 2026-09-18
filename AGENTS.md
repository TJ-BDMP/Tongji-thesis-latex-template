# AGENTS.md

## Project

This repository contains a Tongji University doctoral thesis template. The main document is `main.tex`, and the class implementation is `tongjithesis.cls`.

## Build

Always build the thesis with `latexmk` and XeLaTeX. The project uses `fontspec`, `xeCJK`, and font files under `fonts/`, so PDFLaTeX is not supported for `main.tex`.

Use the same options as the LaTeX Workshop `LaTeXmk (XeLaTeX)` recipe:

```sh
latexmk -synctex=1 -interaction=nonstopmode -file-line-error -xelatex -outdir=. --shell-escape main.tex
```

When an output directory is supplied by the environment or editor, replace `.` with that directory. In LaTeX Workshop this corresponds to:

```jsonc
{
  "latex-workshop.latex.tools": [
    {
      "name": "latexmk-xelatex",
      "command": "latexmk",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "-xelatex",
        "-outdir=%OUTDIR%",
        "--shell-escape",
        "%DOC%"
      ]
    },
    {
      "name": "latexmk-pdflatex",
      "command": "latexmk",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "-pdf",
        "-outdir=%OUTDIR%",
        "--shell-escape",
        "%DOC%"
      ]
    }
  ],
  "latex-workshop.latex.recipes": [
    {
      "name": "LaTeXmk (XeLaTeX)",
      "tools": ["latexmk-xelatex"]
    },
    {
      "name": "LaTeXmk (PDFLaTeX)",
      "tools": ["latexmk-pdflatex"]
    }
  ]
}
```

For this repository, select `LaTeXmk (XeLaTeX)`.

After a build, inspect the log for LaTeX errors, unresolved references, and overfull or underfull boxes. Do not treat a generated PDF as sufficient verification when the build log contains relevant warnings.

To remove generated intermediates while preserving the PDF, run:

```sh
latexmk -outdir=. -c main.tex
```

## Project Conventions

- Load Chinese fonts from explicit repository-relative paths under `fonts/`.
- Preserve the A4 page geometry and measured header/footer positions in `tongjithesis.cls` unless requirements change.
- Put chapter content in `contents/`, figures in `figures/`, template assets in `assets/`, and bibliography entries in `references.bib`.
- Do not edit generated files such as `.aux`, `.bbl`, `.bcf`, `.log`, `.out`, `.run.xml`, `.synctex.gz`, `.toc`, or `.xdv` manually.
- Preserve unrelated user changes when modifying the template.
