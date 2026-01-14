# whu-thesis Template Quick Guide

This is a short, searchable guide to the current template usage in this repo.
It focuses on the patterns used by `demo.tex` and `pages/chapter1.tex`, plus
the custom chapter command added in `whu-thesis.cls`.

## What Builds demo.pdf

- Entry file: `demo.tex`
- Included content:
  - `\include{pages/chapter1.tex}`
  - `\include{pages/appendix.tex}`
- Bibliography source: `ref/bachelor-refs.bib`

## Build Notes (BibTeX)

Use a recipe that runs BibTeX:

```
xelatex -> bibtex -> xelatex -> xelatex
```

If you see `Citation ... undefined`, check:

- The BibTeX step actually ran and produced a `.bbl`.
- `ref/bachelor-refs.bib` contains only `@...{}` entries (any prose lines must
  be commented with `%`).

## Main File Pattern (demo.tex)

```
\documentclass[type = master,class = academic]{whu-thesis}

\whusetup{
  info = {
    title      = {...},
    title*     = {...},
    department = {...},
    department* = {...},
    author     = {...},
    author*    = {...},
    student-id = {...},
    supervisor = {...},
    supervisor* = {...},
    academic-title = {...},
    academic-title* = {...},
    subject = {...},
    major   = {...},
    major*  = {...},
    research-area  = {...},
    research-area* = {...},
    year = 2026,
    month = 4,
    keywords  = {...},
    keywords* = {...},
  },
  style = {
    font = termes,
    math-font = termes,
    cjk-font = windows,
    bib-backend = bibtex,
    bib-style = numerical,
    cite-style = super,
    bib-resource = {ref/bachelor-refs.bib},
  }
}

\hypersetup{hidelinks}
\whumodule{algorithm2e}
\begin{document}

\tableofcontents
% \listoffigures
% \listoftables

\mainmatter
\include{pages/chapter1.tex}

\printbibliography

\begin{acknowledgements}
  ...
\end{acknowledgements}

\appendix
\include{pages/appendix.tex}
\end{document}
```

## Chapter Usage (Custom)

The template now provides:

```
\whuchapter{1}{绪论}
```

Effect:

- Centered chapter title
- No leading Arabic number printed
- Displays `第一章 绪论`
- Keeps correct numbering for `1.1`, `1.2`, ...
- Writes a matching TOC entry

## Sections / Subsections

Standard LaTeX commands:

```
\section{研究背景与意义}
\subsection{...}
\subsubsection{...}
```

## References / Citations

- Numeric + superscript: set `bib-style = numerical` and `cite-style = super`
- Use:

```
\cite{key1}
\cite*{key1,key2}
```

## Figures / Tables

```
\begin{figure}[ht]
  \centering
  \includegraphics[width=5cm]{whu-logo.pdf}
  \caption{武汉大学校徽}
  \label{fig:whu-logo}
\end{figure}

引用图~\ref{fig:whu-logo}
```

```
\begin{table}[ht]
  \centering
  \caption{简单的表格}
  \label{tab:simple}
  \begin{tabular}{cc}
    \hline
    a & b \\ \hline
    c & d \\ \hline
  \end{tabular}
\end{table}
```

## Equations

```
\begin{equation}
  a^2 + b^2 = c^2.
\end{equation}

\[
  a^2 + b^2 = c^2.
\]
```

## Algorithms (algorithm2e)

```
\begin{algorithm}
\caption{Simulation-optimization heuristic}\label{algorithm}
\KwData{...}
\KwResult{...}
...
\end{algorithm}
```

## Theorem Environments

Available (examples from `pages/chapter1.tex`):

- theorem, definition, example, property, proposition, corollary
- lemma, axiom, counterexample, conjecture, question, claim, remark

Example:

```
\begin{theorem}
  ...
\end{theorem}

\begin{proof}
  ...
\end{proof}
```

## Fonts (CJK)

In `style`:

```
cjk-font = windows   % windows, mac, fandol, sourcehan, none
```

## Common Fixes

- Hyperlink borders in PDF: keep `\hypersetup{hidelinks}` in the preamble.
- `???` citations: ensure BibTeX runs and `.bib` has only entries or commented text.
