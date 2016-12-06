all: main.pdf thesis.pdf


main.pdf: main.tex main.toc intro.tex all-ones.tex perturbation.tex future.tex notation.tex my-style.sty almost-all-ones.bib
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
