main.pdf: main.tex main.toc intro.tex all-ones.tex perturbation.tex future.tex notation.tex fa-style.sty almost-all-ones.bib
	xelatex main.tex
	bibtex main.aux
	xelatex main.tex
	xelatex main.tex

%.pdf: %.toc %.tex
	xelatex $*.tex
	xelatex $*.tex

%.toc: %.tex
	xelatex $*.tex
