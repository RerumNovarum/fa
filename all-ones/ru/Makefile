all: main.pdf thesis.pdf thesis-cp1251.pdf

.PHONY: clean

clean:
	rm main.pdf thesis.pdf thesis-cp1251.pdf thesis-cp1251.tex *.aux *.bgl *.blg *.bbl *.out *.log *.toc


main.pdf: main.tex main.toc body/intro.tex body/prep-all-ones.tex body/prep-almost-all-ones.tex body/general-method.tex body/final-estimates.tex body/future.tex
	xelatex main.tex
	xelatex main.tex
	xelatex main.tex

main-updown.pdf: main.pdf
	pdftk A=main.pdf shuffle Aodd Aevensouth output main-updown.pdf

style-utf8.tex: style.tex
	iconv -f cp1251 -t utf8 style.tex -o style-utf8.tex

thesis.pdf: thesis.tex style-utf8.tex
	pdflatex thesis.tex

thesis-cp1251.tex: thesis.tex
	sed -e 's/usepackage\[utf8\]/usepackage\[cp1251\]/' -e 's/style-utf8.tex/style.tex/' <thesis.tex | iconv -f utf8 -t cp1251 -o thesis-cp1251.tex

thesis-cp1251.pdf: thesis-cp1251.tex
	pdflatex thesis-cp1251.tex

%.pdf: %.toc %.tex
	xelatex $*.tex
	xelatex $*.tex

%.toc: %.tex
	xelatex $*.tex
