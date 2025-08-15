# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a LaTeX-based resume/CV repository for Alex Towell. The repository contains a professional academic CV built using a custom LaTeX template with a two-column layout design.

## File Structure

- `cv.tex` - Main resume content file containing personal information, education, experience, and skills
- `structure.tex` - LaTeX template structure and formatting definitions (based on Wenneker template)
- `lex.png` - Profile photo used in the resume
- `cv.pdf` - Compiled PDF output
- `README.md` - Basic repository description

## Architecture

The CV uses a modular LaTeX structure:
- **Main Document**: `cv.tex` imports `structure.tex` and defines content
- **Template Structure**: `structure.tex` defines the two-column layout with sidebar and main content area
- **Layout**: Left column contains photo and contact information, right column contains main CV sections
- **Styling**: Uses XCharter font, RoyalBlue color scheme, and custom commands for consistent formatting

## Common Commands

### Using Makefile (Recommended)

```bash
make            # Compile CV (two passes for proper references)
make quick      # Quick single-pass compilation
make clean      # Remove auxiliary files
make distclean  # Remove all generated files including PDF
make view       # Compile and open PDF viewer
make watch      # Auto-recompile on file changes
make help       # Show all available commands
```

### Direct LaTeX Commands

```bash
# Compile the resume to PDF (run twice for proper references)
pdflatex cv.tex
pdflatex cv.tex  # Second run ensures proper layout rendering

# Alternative: Compile with better error handling
pdflatex -interaction=nonstopmode cv.tex || true

# Clean auxiliary files after compilation
rm -f cv.aux cv.log cv.out cv.fls cv.fdb_latexmk cv.synctex.gz
```

## Template Features

- Two-column layout with sidebar and main content
- Custom commands: `\CVSection{}`, `\CVItem{}{}`, `\aboutme{}{}`
- Photo integration with `\userinformation{}`
- Dotted vertical line separator
- Page breaks handled with `\framebreak` and `\clearpage`

## Key Customization Points

- **Personal Information**: Edit the `\userinformation{}` block in cv.tex:14-26
- **Main Sections**: Modify CV sections starting at cv.tex:49 (About Me, Education, Skills, Publications, etc.)
- **Color Scheme**: Change RoyalBlue color in structure.tex (used throughout for highlighting)
- **Layout Dimensions**: Adjust column widths in structure.tex:44,62 (currently 0.2/0.7 split)
