# The `ocgx2` LaTeX Package

© 2016 Alexander Grahn

**Introduction**

This package serves as a drop-in replacement for the already existing
packages `ocgx` by Paul Gaborit and `ocg-p` by Werner Moshammer for the
creation of PDF Layers.

It re-implements the functionality of the `ocg`, `ocgx` and `ocg-p`
packages and adds support for all known engines and back-ends including:

- LaTeX --> dvips --> ps2pdf/Distiller
- (Xe)LaTeX --> (x)dvipdfmx
- pdfLaTeX, luaLaTeX

To enable dvipdfmx support, pass `dvipdfmx` globally as a class option.

*New features:*

+ layers extending across page breaks
+ grouping layers into Radio Button Groups
+ OCG coloured links for hyperref

Also, it adds some minor improvements and bug fixes, such as package
options, remembering option settings of re-opened ocgs, correct behaviour
of layer switching links that were themselves placed on layers, correct
listing of (nested) ocgs in the layers tab of PDF viewers, compatibility
with the `animate` and `media9` packages.

Coloured links in the PDF viewer that are printed on paper in the default text
colour are enabled with

````latex
\usepackage{hyperref} % do NOT set [ocgcolorlinks] here!
\usepackage[ocgcolorlinks]{ocgx2}
````
`ocgx2` uses code from file `tikzlibraryocgx.code.tex` by P. Gaborit to
enable TikZ styles for creating PDF Layers and clickable layer switching
links in the `tikzpicture` context.

Just say:

````latex
\usepackage[tikz]{ocgx2}
````
instead of
````latex
\usepackage{tikz}
\usetikzlibrary{ocgx}
````
to enable these TikZ styles and read the `ocgx` documentation about
their usage:
````
texdoc ocgx
````
The /tikz/ocg/opts=<ocg options> parameter adds to the list in section
"How to add TikZ scopes into OCGs" in the `ocgx` manual. It allows
passing ocg environment options (see below) to the TikZ scope.


**Usage**
````latex
\usepackage[<options>]{ocgx2}

\begin{ocg}[<options>]{<layer name>}{<layer id>}{<initial visibility>}
  ... material to be put on a PDF layer ...
\end{ocg}
````
With `<initial visibility>` = `( on | true | 1 )  |  ( off | false | 0 )`

and `<options>`:
````
viewocg = always | never | ifvisible
printocg =  always | never | ifvisible
exportocg =  always | never | ifvisible
listintoolbar= always | never | iffirstuse
````
not in `ocgx`, `ocg-p`:

`  showingui` (same as `listintoolbar`)
`  radiobtngrp = <group name>` (string; environment-only option)

`  tikz`  (package-only option, see above)
`  ocgcolorlinks`  (package-only option, see above)

Package options have global scope. Environment options override package
options locally.

Layers can be added to one or several Radio Button Groups using the new
option `radiobtngrp`. From all layers within a Radio Button Group only
one can be enabled at a time. Enabling a layer, e. g. in the Layers tab
of the PDF viewer, automatically hides the previously visible layer.
Option `radiobtngrp` can be used repeatedly for the same OCG in order
to add the layer to more than one Radio Button Group.

`ocg` environments can be nested and span multiple pages.

See the `ocg-p` manual about the environment usage and the meaning of
the remaining options:
````
texdoc ocg-p
````

Clickable links for switching PDF layer visibility are created with:
````latex
\switchocg{<layer IDs to toggle, space separated>}{<link text>}
\showocg{<layer IDs to switch ON, space separated>}{<link text>}
\hideocg{<layer IDs to switch OFF, space separated>}{<link text>}
\actionsocg{<IDs to toggle>}{<IDs to switch ON>}{<IDs to switch OFF>}{<link text>}
````
For details about their usage, read the `ocgx` package manual:
````
texdoc ocgx
````
For compatibility with the `ocg-p` package, the following commands have
been provided:
````latex
\toggleocgs[triggerocg=...]{<layer IDs to toggle, space separated>}{<link text>}
\showocgs[triggerocg=...]{<layer IDs to switch ON, space separated>}{<link text>}
\hideocgs[triggerocg=...]{<layer IDs to switch OFF, space separated>}{<link text>}
\setocgs[triggerocg=...]{<IDs to toggle>}{<IDs to switch ON>}{<IDs to switch OFF>}{<link text>}
````
See the `ocg-p` package manual for the meaning of `triggerocg=...`.


                     * * *


**License**

This material is subject to the [LaTeX Project Public License](LICENSE).
