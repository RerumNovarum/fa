MAIN_SRCS = main.tex main.toc body/intro.tex body/prep-all-ones.tex body/general-method.tex body/final-estimates.tex body/summary.tex bibliography.tex

all: cp1251/main.pdf # main.pdf

.PHONY: clean

clean:
	rm main.pdf thesis.pdf thesis-cp1251.pdf thesis-cp1251.tex *.aux *.bgl *.blg *.bbl *.out *.log *.toc


main.pdf: $(MAIN_SRCS)
	xelatex "\def\XELATEX{}\input{main.tex}"
	xelatex "\def\XELATEX{}\input{main.tex}"
	xelatex "\def\XELATEX{}\input{main.tex}"
	touch $@

%.pdf: %.toc %.tex
	xelatex "\def\XELATEX{} \input{$*.tex}"
	xelatex "\def\XELATEX{} \input{$*.tex}"
	xelatex "\def\XELATEX{} \input{$*.tex}"
	touch $@

%.toc: %.tex
	xelatex "\def\XELATEX{} \input{$*.tex}"
	touch $@

main-updown.pdf: main.pdf
	pdftk A=main.pdf shuffle Aodd Aevensouth output main-updown.pdf
	touch $@

cp1251/main.pdf: $(addprefix cp1251/, $(MAIN_SRCS))
	cd cp1251 ; pdflatex main.tex
	cd cp1251 ; pdflatex main.tex
	cd cp1251 ; pdflatex main.tex
	touch $@

cp1251/%: %
	@mkdir -p $(shell dirname $@)
	iconv -f utf8 -t cp1251 $< -o $@

cp1251/%.pdf: %.tex %.toc 
	cd cp1251 ; pdflatex $<
	cd cp1251 ; pdflatex $<
	cd cp1251 ; pdflatex $<
	touch $@

cp1251/%.toc: %.tex
	cd cp1251 ; pdflatex $<
	touch $@
