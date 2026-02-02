# Neuro-Symbolic AI Slides Repository Guide

This repository contains LaTeX source code for the "Neuro-Symbolic AI" course slides. This guide provides instructions for AI agents and developers working on this codebase.

## 1. Environment & Build Instructions

### Environment
- **Platform:** Linux (assumed based on file paths)
- **Primary Language:** LaTeX (TeX Live distribution recommended)
- **Project Structure:**
  - Root directory contains numbered `.tex` files (e.g., `01-introduction.tex`, `02-ltn.tex`) representing individual slide decks.
  - Image files (PNG, PDF, GIF) are stored directly in the root directory.
  - `notes/` directory contains supplementary notes.

### Build Commands
To build the PDF for a specific slide deck, use `pdflatex`.

**Build a Single Slide Deck:**
```bash
# Example: Building the Introduction slides
pdflatex 01-introduction.tex
```
*Note: You may need to run `pdflatex` multiple times (usually 2-3) to resolve cross-references, table of contents, and navigation elements properly.*

**Build All Slides:**
There is no central makefile. To build all slides, iterate through the `.tex` files:
```bash
for f in [0-9]*.tex; do pdflatex "$f"; done
```

**Clean Up Auxiliary Files:**
LaTeX generates many intermediate files (`.aux`, `.log`, `.nav`, `.out`, `.snm`, `.toc`). To clean them:
```bash
rm *.aux *.log *.nav *.out *.snm *.toc *.vrb
```

### Testing
There are no formal unit tests. "Testing" in this context means:
1.  **Compilation Success:** The `.tex` file compiles to PDF without fatal errors.
2.  **Visual Verification:** The generated PDF renders correctly (layout, images, fonts).

**Run a "Test" (Check Compilation):**
```bash
pdflatex -interaction=nonstopmode 01-introduction.tex
if [ $? -eq 0 ]; then echo "Build Successful"; else echo "Build Failed"; fi
```

### Linting
There are no configured linters. However, ensure:
-   Braces `{}` are balanced.
-   Environments `\begin{...} \end{...}` are properly closed.
-   File paths in `\includegraphics` are correct.

---

## 2. Code Style & Conventions

### File Structure & Naming
-   **File Names:** Use the convention `XX-topic.tex` (e.g., `01-introduction.tex`, `06-neural-asp.tex`).
-   **Preamble:** Keep standard packages (`beamer`, `tikz`, etc.) at the top.
-   **Theme:** The project uses `\usetheme{Madrid}`. Do not change the theme unless explicitly requested.
-   **Emacs Locals:** Preserve the "Local Variables" block at the end of files if present.

### Formatting
-   **Indentation:** Use 2 spaces for indentation within environments (`itemize`, `enumerate`, `frame`).
-   **Line Length:** Soft wrap lines; do not hard wrap paragraphs unless necessary for specific LaTeX formatting.
-   **Spacing:** Use blank lines to separate frames and logical sections.

**Example Frame Structure:**
```latex
\begin{frame}
  \frametitle{Slide Title}
  \begin{itemize}
  \item Main point
    \begin{itemize}
    \item Sub-point details
    \item Another detail
    \end{itemize}
  \item Secondary point
  \end{itemize}
\end{frame}
```

### LaTeX Best Practices
-   **Images:**
    -   Use `\includegraphics[width=\textwidth]{filename.png}` (or relative width like `.75\textwidth`) to ensure images fit the slide.
    -   Ensure image files exist in the same directory or provide a correct relative path.
-   **Math:**
    -   Use `$` for inline math (e.g., $O(n \cdot \log{n})$).
    -   Use `\[ ... \]` or `equation` environment for display math.
-   **TikZ:**
    -   Keep TikZ diagrams self-contained or use `\usetikzlibrary` in the preamble if new libraries are needed.
-   **Beamer Specifics:**
    -   Use `\pause` for stepwise uncovering of bullet points.
    -   Use `\frametitle{...}` for slide titles.

### Error Handling
-   If compilation fails, check the `.log` file (e.g., `01-introduction.log`) for error messages.
-   Common errors include missing `}` or `\end{...}`.
-   "File not found" errors usually refer to missing images or included `.tex` files.

---

## 3. Workflow for Agents

1.  **Read Context:** Always read the relevant `.tex` file to understand the current structure and packages.
2.  **Verify Images:** Before adding an `\includegraphics` command, check if the image file exists using `ls`.
3.  **Atomic Changes:** When modifying a slide, try to keep the change contained within the `\begin{frame}...\end{frame}` block.
4.  **Verification:** After editing, attempt to compile the file using `pdflatex -interaction=nonstopmode <filename>` to ensure no syntax errors were introduced.
5.  **No Hallucinations:** Do not invent LaTeX packages. Use standard ones available in TeX Live (e.g., `amsmath`, `graphicx`, `tikz`).

## 4. Specific Rule Definitions

### Cursor / Copilot Rules
*No specific `.cursorrules` or `.github/copilot-instructions.md` were found in this repository.*

However, apply the following implicit rules:
-   **Context Awareness:** Analyze the existing slides (like `01-introduction.tex`) to mimic the writing style and bullet point density.
-   **Conciseness:** Slide content should be concise. Avoid long paragraphs; prefer bullet points.
-   **Visuals:** Suggest or insert placeholders for diagrams where complex concepts are explained.

### Todo Checklist for New Slides
When creating a new slide deck:
- [ ] Set `\documentclass{beamer}`.
- [ ] Import `\usetheme{Madrid}`.
- [ ] Add Title, Author, and Date.
- [ ] Create an "Overview" or "Outline" frame.
- [ ] Ensure all referenced images are present.
- [ ] Verify compilation.
