MAIN_SOURCES:= main.tex body/intro.tex body/prep-all-ones.tex body/general-method.tex body/final-estimates.tex body/summary.tex bibliography.tex

PDFLATEX = pdflatex

all: cp1251/main.pdf # main.pdf

.PHONY: clean

clean:
	rm -f main.pdf thesis.pdf thesis-cp1251.pdf thesis-cp1251.tex *.aux *.bgl *.blg *.bbl *.out *.log *.toc
	rm -f $(addprefix cp1251/, $(MAIN_SOURCES))
	find -iname '*.aux' -exec rm -f \{\} \;
	find -iname '*.bgl' -exec rm -f \{\} \;
	find -iname '*.blg' -exec rm -f \{\} \;
	find -iname '*.bbl' -exec rm -f \{\} \;
	find -iname '*.out' -exec rm -f \{\} \;
	find -iname '*.log' -exec rm -f \{\} \;
	find -iname '*.toc' -exec rm -f \{\} \;

.PHONY: escape-accented-chars

escape-accented-chars:
	find -iname '*.tex' -exec sed -i 's/ё/\\"е/g' \{\} \;

main.pdf: $(MAIN_SOURCES)
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

cp1251/main.pdf: cp1251/main.toc $(addprefix cp1251/,$(MAIN_SOURCES))
	@echo : Making $@
	cd cp1251 ; $(PDFLATEX) main.tex
	cd cp1251 ; $(PDFLATEX) main.tex
	cd cp1251 ; $(PDFLATEX) main.tex
	touch $@

cp1251/%.tex: %.tex
	@echo : Making $@
	@mkdir -p $(shell dirname $@)
	iconv -f utf8 -t cp1251 $< -o $@

cp1251/%.pdf: cp1251/%.tex cp1251/%.toc 
	@echo : Making $@
	cd cp1251 ; $(PDFLATEX) $*.tex
	cd cp1251 ; $(PDFLATEX) $*.tex
	cd cp1251 ; $(PDFLATEX) $*.tex
	touch $@

cp1251/main.toc: $(addprefix cp1251/,$(MAIN_SOURCES))
	@echo : Making $@
	cd cp1251 ; $(PDFLATEX) main.tex
	touch $@
