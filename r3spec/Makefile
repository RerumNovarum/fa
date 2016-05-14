SOURCES=*.tex */*.tex

all: main odds.pdf evens.pdf

main: r3spec.pdf toc

r3spec.pdf: $(SOURCES)
	xelatex r3spec.tex

toc: r3spec.pdf $(SOURCES)
	xelatex r3spec.tex

r3spec.ps: main
	pdf2ps r3spec.pdf

r3spec.signatures.ps: r3spec.ps
	psbook r3spec.ps > r3spec.signatures.ps

r3spec.sheets.ps: r3spec.signatures.ps
	psnup -2 r3spec.signatures.ps > r3spec.sheets.ps

odds.pdf: r3spec.sheets.ps
	psselect -o r3spec.sheets.ps | ps2pdf - odds.pdf

evens.pdf: r3spec.sheets.ps
	psselect -e -r r3spec.sheets.ps | ps2pdf - evens.pdf
