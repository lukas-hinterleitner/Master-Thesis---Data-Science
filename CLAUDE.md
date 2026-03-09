# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Master's thesis** (University of Vienna, Data Science) by Lukas Hinterleitner, supervised by Prof. Benjamin Roth. The thesis is titled *"Select or Project? Evaluating Lower-dimensional Vectors for LLM Training Data Explanations"* and investigates whether selecting gradient subsets or projecting full gradients is more effective for instance-based explanations of LLMs.

## Repository Structure

This is a **LaTeX project** synced with Overleaf. There is no code to build/test/lint — only LaTeX compilation.

- `main.tex` — Document root; uses `UniVieCS_Thesis` document class
- `packages_macros.tex` — Additional packages and custom math macros (weight matrices, similarity functions, Iverson brackets)
- `UniVieCS_Thesis.cls` / `UniVieCS_Thesis_TexLive19.cls` — University of Vienna thesis class files (do not modify)
- `bibliography.bib` — BibTeX references (alpha style)
- `A) Front Matter/` — Title page, metadata, abstracts (English + German), acknowledgements
- `B) Chapters/` — Thesis chapters (01–07): introduction, related work, methodology (model, setup, results), discussion, conclusion
- `C) Back Matter/` — Acronyms, glossary, appendix
- `figures/` — Images and a `results/` subdirectory

## Build

Compile with `pdflatex` (or via Overleaf). The document requires multiple passes for glossaries and bibliography:

```
pdflatex main.tex
bibtex main
makeglossaries main
pdflatex main.tex
pdflatex main.tex
```

## Key Conventions

- **Language**: British English (`babel` with `british` option)
- **Bibliography**: `alpha` style via BibTeX (not biblatex)
- **Glossaries/Acronyms**: Defined in `C) Back Matter/acronyms.tex` and `glossary.tex`, loaded before `\begin{document}`
- **Review comments**: Uses `fixme` package with author `TTW` (green); draft mode is toggled via `\fxsetup{status=draft}` in `main.tex` (currently commented out, so fixme notes are hidden in output)
- **Custom macros** (in `packages_macros.tex`): `\W`, `\Wlk`, `\nWlk`, `\dWlk`, `\vXsi`, `\simcos`, `\Indic`, `\Iverson`, `\BreakHeader` — used extensively in methodology chapters
- **Directory names contain spaces** (e.g., `A) Front Matter/`) — always quote paths in shell commands
- **Overleaf sync**: Commits come from Overleaf. Do not restructure files or rename directories without coordinating with the Overleaf project
