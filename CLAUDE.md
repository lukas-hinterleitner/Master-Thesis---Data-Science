# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Master's thesis** (University of Vienna, Data Science) by Lukas Hinterleitner, supervised by Prof. Benjamin Roth. The thesis is titled *"Select or Project? Evaluating Lower-dimensional Vectors for LLM Training Data Explanations"* and investigates whether selecting gradient subsets or projecting full gradients is more effective for instance-based explanations of LLMs.

## Repository Structure

This is a **LaTeX project** synced with Overleaf. There is no code to build/test/lint — only LaTeX compilation.

- `main.tex` — Document root; uses `UniVieCS_Thesis` document class
- `packages_macros.tex` — Additional packages and custom math macros (weight matrices, similarity functions, Iverson brackets)
- `UniVieCS_Thesis.cls` — University of Vienna thesis class used by `main.tex` (do not modify)
- `UniVieCS_Thesis_TexLive19.cls` — unused fallback variant for TeX Live 2019; swap it in only if the main class fails on an old TeX distribution (do not modify)
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

- **Do not commit build artifacts** (`.aux`, `.bbl`, `.blg`, `.glo`, `.gls`, `.log`, `.out`, `.toc`, …) — `.gitignore` is currently empty, so a local compile will show them all as untracked.
- Chapters are pulled in via `\input` (not `\include`), so `\includeonly` cannot be used for partial compiles.
- No `-shell-escape` needed — listings use the `listings` package, not `minted`.

## Key Conventions

- **Language**: British English (`babel` loads `[ngerman, british]`; `british` is the main language, `ngerman` is required for the German abstract in `A) Front Matter/kurzfassung.tex` — do not remove it)
- **Bibliography**: `alpha` style via BibTeX (not biblatex)
- **Glossaries/Acronyms**: Defined in `C) Back Matter/acronyms.tex` and `glossary.tex`, loaded before `\begin{document}`
- **Review comments**: Uses `fixme` package with author `TTW` (green); draft mode is toggled via `\fxsetup{status=draft}` in `main.tex` (currently commented out, so fixme notes are hidden in output)
- **Custom macros** (in `packages_macros.tex`): `\W`, `\Wlk`, `\nWlk`, `\dWlk`, `\vXsi`, `\simcos`, `\Indic`, `\Iverson`, `\BreakHeader` — used extensively in methodology chapters
- **Directory names contain spaces** (e.g., `A) Front Matter/`) — always quote paths in shell commands
- **Overleaf sync**: Commits come from Overleaf. Do not restructure files or rename directories without coordinating with the Overleaf project
