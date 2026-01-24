# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

LaTeX research paper on sentiment analysis for comments. This is a Vietnamese academic paper with modular structure for easy collaboration and editing.

## Development Commands

### Compile the paper:
```bash
# XeLaTeX (recommended for Vietnamese support)
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex

# Or use latexmk (Linux/Mac)
latexmk -xelatex main.tex
```

### Clean auxiliary files:
```bash
# Remove LaTeX build artifacts
rm -f *.aux *.log *.out *.toc *.bbl *.blg *.bcf *.run.xml *.fls *.fdb_latexmk
```

## Architecture

The paper follows a modular LaTeX structure:

- **main.tex**: Main document file that includes all sections
- **packages.tex**: All package imports and configuration
- **sections/*.tex**: Individual chapters (01-introduction, 02-related-work, etc.)
- **references.bib**: BibTeX bibliography database

### File naming conventions:
- Section files: `NN-title.tex` where NN is a two-digit number
- Figures: Place in `figures/` directory
- Images: Place in `images/` directory

### Important notes:
- Use `XeLaTeX` compiler for proper Vietnamese font support
- Cross-references require multiple compilation passes
- New sections must be added to main.tex via `\include{sections/filename}`
