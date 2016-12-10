all: main.pdf thesis.pdf


main.pdf: main.tex main.toc body/intro.tex body/prep-all-ones.tex body/prep-almost-all-ones.tex body/general-method.tex body/final-estimates.tex body/future.tex my-style.sty almost-all-ones.bib
	xelatex main.tex
	bibtex main.aux
	xelatex main.tex
	xelatex main.tex

thesis.pdf: thesis.tex
	pdflatex thesis.tex

%.pdf: %.toc %.tex
	xelatex $*.tex
	xelatex $*.tex

%.toc: %.tex
	xelatex $*.tex
