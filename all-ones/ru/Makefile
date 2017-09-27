MAIN_SOURCES:= allones.tex body/intro.tex body/prep-all-ones.tex \
			   body/general-method.tex body/final-estimates.tex \
			   body/summary.tex allones.bib
ZIP_CONTENTS:= allones.pdf authors.doc liabilities.doc authors.pdf liabilities.pdf \
	$(addprefix cp1251/,$(MAIN_SOURCES)) \

PDFLATEX = pdflatex

all: currentproblems.zip

currentproblems.zip: $(ZIP_CONTENTS)
	rm -f $@
	zip $@ $(ZIP_CONTENTS)

.PHONY: clean

clean:
	rm -f allones.pdf thesis.pdf thesis-cp1251.pdf thesis-cp1251.tex *.aux *.bgl *.blg *.bbl *.out *.log *.toc
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
	sed -i 's/ё/\\"е/g' allones.tex

allones.pdf: $(MAIN_SOURCES)
	xelatex "\def\XELATEX{}\input{allones.tex}"
	biber allones
	xelatex "\def\XELATEX{}\input{allones.tex}"
	xelatex "\def\XELATEX{}\input{allones.tex}"
	touch $@

%.pdf: %.toc %.tex
	xelatex "\def\XELATEX{} \input{$*.tex}"
	xelatex "\def\XELATEX{} \input{$*.tex}"
	xelatex "\def\XELATEX{} \input{$*.tex}"
	touch $@

%.toc: %.tex
	xelatex "\def\XELATEX{} \input{$*.tex}"
	touch $@

main-updown.pdf: allones.pdf
	pdftk A=allones.pdf shuffle Aodd Aevensouth output main-updown.pdf
	touch $@

cp1251/allones.pdf: cp1251/allones.toc $(addprefix cp1251/,$(MAIN_SOURCES))
	@echo : Making $@
	cd cp1251 ; $(PDFLATEX) allones.tex
	cd cp1251 ; $(PDFLATEX) allones.tex
	cd cp1251 ; $(PDFLATEX) allones.tex
	touch $@

cp1251/%: %
	@echo : Making $@
	@mkdir -p $(shell dirname $@)
	iconv -f utf8 -t cp1251 $< -o $@

cp1251/%.pdf: cp1251/%.tex cp1251/%.toc 
	@echo : Making $@
	cd cp1251 ; $(PDFLATEX) $*.tex
	cd cp1251 ; $(PDFLATEX) $*.tex
	cd cp1251 ; $(PDFLATEX) $*.tex
	touch $@

cp1251/allones.toc: $(addprefix cp1251/,$(MAIN_SOURCES))
	@echo : Making $@
	cd cp1251 ; $(PDFLATEX) allones.tex
	touch $@

%.doc: %.md
	pandoc $< -o $@

%.rtf: %.md
	pandoc $< -o $@

%.pdf: %.md
	pandoc --latex-engine=xelatex -V mainfont='CMU Serif' $< -o $@
