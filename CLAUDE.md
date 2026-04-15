# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

LaTeX-based resume/CV repository with two variants:
- `original/` - General-purpose academic CV
- `ai-focused/` - CV tailored for AI safety and alignment positions

Both variants use identical template structures and build systems.

## Build Commands

Each variant has its own Makefile. Run commands from within the variant directory:

```bash
cd original/   # or cd ai-focused/
make           # Compile CV (two pdflatex passes for proper references)
make quick     # Single-pass compile for fast iteration
make clean     # Remove auxiliary files (.aux, .log, .out, etc.)
make distclean # Remove all generated files including PDF
make view      # Build and open PDF viewer
make watch     # Auto-recompile on changes (requires inotifywait)
```

Prerequisite: `pdflatex` available in `PATH` (TeX Live/MacTeX).

## Architecture

Each variant contains:
- `cv.tex` - Main content (personal info, sections, experience)
- `structure.tex` - Two-column layout template (Wenneker-based), macros, styling
- `lex.png` - Profile photo
- `cv.pdf` - Compiled output

Layout: Left sidebar (photo + contact info) with dotted separator, right main content area. Uses XCharter font and RoyalBlue color scheme.

## Key Macros

- `\userinformation{}` - Sidebar content block
- `\CVSection{}` - Section headings
- `\CVItem{}{}` - Titled content items
- `\aboutme{}{}` - About me section
- `\framebreak` - End column, `\clearpage` - Page break
- `\Sep` - Vertical spacing between items

## Content Organization

For multi-page CVs, redefine `\userinformation{}` after `\clearpage` to omit the photo on subsequent pages (see `cv.tex` for examples).

## Validation

- Build must complete with zero LaTeX errors
- Check PDF for overfull boxes, proper spacing, and working hyperlinks
- Run two passes after macro changes to ensure layout stability
