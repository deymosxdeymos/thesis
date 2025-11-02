# Agent Guidelines for LaTeX Thesis Template

## Build Commands
- **Compile thesis**: Use LaTeX editor (TeXstudio/Overleaf) or run: `pdflatex thesis.tex && bibtex thesis && pdflatex thesis.tex && pdflatex thesis.tex`
- **Quick compile**: `pdflatex thesis.tex` (without bibliography updates)
- Main file: `thesis.tex` (UNESCO format 155x230mm)

## Project Structure
- `thesis.tex` - Main document file
- `chapters/*.tex` - Chapter content files (chapter-1 through chapter-5, abstract, appendix, etc.)
- `config/config.sty` - LaTeX package configurations and custom commands
- `figure/` - Images and diagrams
- `references.bib` - Bibliography in BibTeX format (IEEE citation style)

## LaTeX Style Guidelines
- **Language**: Bahasa Indonesia (primary), English (for abstract-en.tex)
- **Font**: Times New Roman equivalent (newtx package), 12pt body text
- **Spacing**: 1.5 line spacing (`\baselinestretch{1.5}`)
- **Paper format**: UNESCO (155x230mm) with 2cm margins, 0.5cm binding offset
- **Citation**: IEEE style using biblatex with bibtex backend
- **Code blocks**: Use `\begin{lstlisting}...\end{lstlisting}` with language parameter
- **Equations**: Use `\begin{equationcaptioned}{label}{formula}{caption}` for numbered equations
- **Figures**: Caption font size is footnotesize (10pt), separator is space not colon
- **References**: Always use `\label{}` and `\ref{}` or `\nameref{}` for cross-references
- **Chapters**: Roman numerals (BAB I, BAB II), sections use arabic (1.1, 1.2)
