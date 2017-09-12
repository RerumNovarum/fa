MAIN_SOURCES:= main.tex body/intro.tex body/prep-all-ones.tex \
			   body/general-method.tex body/final-estimates.tex \
			   body/summary.tex bibliography.tex
ZIP_CONTENTS:= main.pdf \
	$(MAIN_SOURCES)

PDFLATEX = pdflatex

all: allones.zip

allones.zip: $(ZIP_CONTENTS)
	rm -f allones.zip
	zip allones.zip $(ZIP_CONTENTS)

.PHONY: clean

clean:
	rm -f main.pdf
	find -iname '*.aux' -exec rm -f \{\} \;
	find -iname '*.bgl' -exec rm -f \{\} \;
	find -iname '*.blg' -exec rm -f \{\} \;
	find -iname '*.bbl' -exec rm -f \{\} \;
	find -iname '*.out' -exec rm -f \{\} \;
	find -iname '*.log' -exec rm -f \{\} \;
	find -iname '*.toc' -exec rm -f \{\} \;

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

%.doc: %.md
	pandoc $< -o $@

%.rtf: %.md
	pandoc $< -o $@

%.pdf: %.md
	pandoc --latex-engine=xelatex -V mainfont='CMU Serif' $< -o $@
