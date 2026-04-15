# Makefile for LaTeX CV compilation

# Main target
TARGET = cv

# LaTeX compiler
LATEX = pdflatex
LATEX_FLAGS = -interaction=nonstopmode -file-line-error

# Default target
.PHONY: all
all: $(TARGET).pdf

# Compile PDF (run twice for proper references)
$(TARGET).pdf: $(TARGET).tex structure.tex
	@echo "Compiling CV (first pass)..."
	@$(LATEX) $(LATEX_FLAGS) $(TARGET).tex || true
	@echo "Compiling CV (second pass for references)..."
	@$(LATEX) $(LATEX_FLAGS) $(TARGET).tex

# Quick compile (single pass)
.PHONY: quick
quick:
	@echo "Quick compile (single pass)..."
	@$(LATEX) $(LATEX_FLAGS) $(TARGET).tex

# Clean auxiliary files
.PHONY: clean
clean:
	@echo "Cleaning auxiliary files..."
	@rm -f $(TARGET).aux $(TARGET).log $(TARGET).out $(TARGET).fls $(TARGET).fdb_latexmk $(TARGET).synctex.gz
	@echo "Clean complete."

# Full clean (including PDF)
.PHONY: distclean
distclean: clean
	@echo "Removing PDF..."
	@rm -f $(TARGET).pdf

# Open PDF viewer (cross-platform)
.PHONY: view
view: $(TARGET).pdf
	@if command -v xdg-open > /dev/null; then \
		xdg-open $(TARGET).pdf; \
	elif command -v open > /dev/null; then \
		open $(TARGET).pdf; \
	elif command -v evince > /dev/null; then \
		evince $(TARGET).pdf; \
	else \
		echo "No PDF viewer found. Please open $(TARGET).pdf manually."; \
	fi

# Watch for changes and recompile
.PHONY: watch
watch:
	@echo "Watching for changes (requires inotifywait)..."
	@while true; do \
		inotifywait -e modify $(TARGET).tex structure.tex 2>/dev/null && \
		make --no-print-directory; \
	done

# Help
.PHONY: help
help:
	@echo "Available targets:"
	@echo "  make         - Compile CV (two passes)"
	@echo "  make quick   - Quick compile (single pass)"
	@echo "  make clean   - Remove auxiliary files"
	@echo "  make distclean - Remove all generated files including PDF"
	@echo "  make view    - Compile and open PDF"
	@echo "  make watch   - Auto-recompile on file changes (requires inotifywait)"
	@echo "  make help    - Show this help message"