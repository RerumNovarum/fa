main.pdf: main.tex main.toc intro.tex all-ones.tex perturbation.tex future.tex notation.tex fa-style.sty almost-all-ones.bib
	pdflatex main.tex
	bibtex main.aux
	pdflatex main.tex
	pdflatex main.tex

%.pdf: %.toc %.tex
	pdflatex $*.tex
	pdflatex $*.tex

%.toc: %.tex
	pdflatex $*.tex
