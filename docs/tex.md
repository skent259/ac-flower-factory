# Tex

## General

Difference between Engine and Formats. The webpage here makes sense of the different levels of TeX

* https://www.tug.org/levels.html

## Miscellaneous

### Spacing between itemize 

```tex
\begin{itemize}
 \setlength\itemsep{-.5em}
 \item ...
 \item ...
\end{itemize}
```

### Side by Side

```tex
\makebox[\textwidth][c]{%
    \begin{minipage}{.3\linewidth}
        \begin{align*}
            \frac{\mathrm{d} X}{\mathrm{d} t} & = \beta\frac{S}{n}X   \\
            \frac{\mathrm{d} S}{\mathrm{d} t} & = - \beta\frac{S}{n}X
        \end{align*}
    \end{minipage}%
    \begin{minipage}{.3\linewidth}
        \begin{align*}
            \frac{\mathrm{d} x}{\mathrm{d} t} & = \beta sx   \\
            \frac{\mathrm{d} s}{\mathrm{d} t} & = - \beta xs
        \end{align*}
    \end{minipage}
}
```

`\begin{minipage}[tbp]{width_of_page}` - A minipage is a smaller page inside the main page, can control how close things are displayed
`\makebox[\textwidth][c]{%}` - centers the two pages next to each other, as long as it's less than the linewidth


## Title Page

```tex
\documentclass{article}
...
\begin{document}
\begin{titlepage}
    \centering
    {\scshape \Large Math 714 \par}
    \vspace{2cm}
    {\bfseries \huge Homework 1}

    \vfill
    {\Large\itshape Michael Liou\par}
    \vfill
    {\large \today\par}
\end{titlepage}
\end{document}
```

## Bibtex

How bibtex generally works. You have a `.bib` file that is the "database" of all the entries.

In the `.tex` file, this would be a minimal file

```tex
\documentclass{article}
\title{Example of bibtex}
\bibliographystyle{plain}
\begin{document}
This example is from \cite{Kant}.
\bibliography{master}
\end{document}
```

The `.bib` file should look like this 

```bib
@book{durrett2019probability,
  place={Cambridge},
  edition={5},
  series={Cambridge Series in Statistical and Probabilistic Mathematics},
  title={Probability: Theory and Examples},
  DOI={10.1017/9781108591034},
  publisher={Cambridge University Press},
  author={Durrett,
      Rick},
  year={2019},
  collection={Cambridge Series in Statistical and Probabilistic Mathematics}
}
```

The document looks for `master.bib` in the directory of the tex file. You may need to run `pdflatex -> bibtex -> pdflatex -> pdflatex`. I have no idea what's going on in this sequence, but it seems necessary to generate the references correctly. 

`bibtex` from the command line looks at the generated `.aux` file for proper references. There, it will look for a `\bibitem` for the database of references, and use that file to make sure all the references are found. If not the error messages/log will tell you which references in the original `.tex` document are not found.

I'd also recommend using the package `natbib`.

* OverLeaf on [natbib](https://www.overleaf.com/learn/latex/Bibliography_management_with_natbib)


## tlmgr

This is the Tex Live Package Manager

Fixing the error "bbm.sty" not found, we can find the package that it's in.
```
tlmgr search --file bbm.sty --global
sudo tlmgr install NAME_OF_PACKAGE
```

## Installation of additional Packages

Texmf tree, is tex and metafonts. The data file structure is TDS, tex directory structure.

* https://en.wikibooks.org/wiki/LaTeX/Installing_Extra_Packages


## Tables (Booktabs)

This is the package you should be using if you create a table. Here's a helpful reference [Tables](https://inf.ethz.ch/personal/markusp/teaching/guides/guide-tables.pdf)

```tex
     \begin{table*}[!ht]
         \centering
         \begin{tabular}{llllllll}
             \toprule
             \phantom{abc} & \multicolumn{7}{c}{Round}\\
                 & 1  & 2 & 3 & 4 & 5 & 6  & 7 \\
             \midrule
             Arm 1 & 10 &   & 0 & 0 & 0 &        \\
             Arm 2 &    & 0 &   &   &   & 10 & 0    \\
             \bottomrule
         \end{tabular}
     \end{table*}
```

## Algorithms

[Just use Algorithmicx](https://tex.stackexchange.com/questions/229355/algorithm-algorithmic-algorithmicx-algorithm2e-algpseudocode-confused). The syntax is easier than Algorithm2e, and it's fine.


## Mathematical images

* http://ctan.mirrors.hoobly.com/info/lshort/english/lshort.pdf
* http://www.texample.net/tikz/
* http://www.texample.net/tikz/resources/#tools-that-generate-pgftikz-code


## Tikz

Axes

```tex
\draw [{Latex[length=2mm]}-{Latex[length=2mm]}] (1,0) node [below] {$P$} -- (0,0) -- (0,1) node [left] {$\beta (P)$};
```

Curves

```tex
\draw plot [smooth, tension=1] coordinates{(0, .7) (.5, .05) (1, .7)};
\draw [] (0, .7) to[in=180, out=0] (.5, .05) to[in=180, out=0] (1, .7)
```

Dots 

```tex
\node [circle, fill, inner sep=1pt] at (0,1) {};
```

Shapes

```tex
\draw [red, dashed] (0, 0) circle (5);
```

### Graphs

```tex
\usetikzlibrary{graphs, graphdrawing} % graphdrawing makes the graph layout automatic
\usegdlibrary{layered, force} % provides "force" and "layered" layouts
\usetikzlibrary{positioning} % right = of a

\begin{tikzpicture}
    \graph[spring layout, nodes={circle, draw, .5pt}, edges={line width=1pt}] {
        1 -- 2 -- 3 -- 4 -- 1; };
```




## Latex Specific

To comment on proofs, just use the `\tag` macro. `\notag` removes numbering of equations in `align` environments. `\tag*{}` comments without the parentheses.

```
\begin{align*}
1 + (2 * 4) &= 1 + 8    \tag{multiply}
            &= 9        \tag*{addition}
\end{align*}
```



