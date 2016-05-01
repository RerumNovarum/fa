SOURCES=*.tex */*.tex

all: r3spec.pdf toc


r3spec.pdf: $(SOURCES)
	xelatex r3spec.tex

toc: r3spec.pdf $(SOURCES)
	xelatex r3spec.tex
