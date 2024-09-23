---
layout: post
title: LaTeX Engine - Tectonic
date:   2024-06-27
categories: software
author: Chenguang Xiao
---
Editiing and compiling LaTeX documents locally requires a LaTeX distribution. 
A common choice is [TeX Live](https://www.tug.org/texlive/), which is self-contained and easy to use.
The only downside is that it is large in size as it contains all packages from CTAN.

There are a new LaTeX distribution called [Tectonic](https://tectonic-typesetting.github.io/en-US/).
The pro of Tectonic is that it is a single file program, and it installs packages on demand automatically.

However, there are a few LaTeX tools builtin with TeX Live that are not available in Tectonic.
For those tools, you need to install them manually.

Here are some tools that I found useful and need to install manually:
- Biber: a reference manager (needed for biblatex)
- glossaries: a package for creating glossaries (needed for makeglossaries, acronyms, etc.)
- makeindex: a package for creating index (needed for makeglossaries)

## Biber
you can search and find precompiled binaries for Biber in SourceForge.
[Biber 2.17](https://sourceforge.net/projects/biblatex-biber/files/biblatex-biber/2.17/) is the version that compatible with Tecnotic 0.15.0.
Although the latest version of Biber is 2.21, it is not supported by Tectonic 0.15.0.
Just use the precompiled binary for your platform if available on SourceForge.

## glossaries
Source code and compiled binaries for glossaries can be found on [CTAN](https://ctan.org/pkg/glossaries).
It comes with the package `glossaries` and the script `makeglossaries`.
for linux and macOS, you can move the binary `makeglossaries` to `/usr/local/bin/` or any other directory in your PATH.

## makeindex
`makeindex` is a necessary tool for creating glossaries with index.
Without makeindex installed, you will get an error when running `makeglossaries`.
There are no precompiled binaries for makeindex, but you can make install it from the source code.
The source code can be found on [CTAN](https://ctan.org/pkg/makeindex).
Change directory to the `src` folder and follow the instructions in the `INSTALL` file to install it into your system.

After installing these tools, you can use Tectonic as your LaTeX engine almost same as TeX Live.

Enjoy your LaTeX writing with Tectonic! vscode extension `LaTeX Workshop` is recommended for writing LaTeX documents.
