
SVG_FILES=$(wildcard *.svg)

PDF_FILES=$(patsubst %.svg, %.pdf, $(SVG_FILES))

PNG_FILES=$(patsubst %.svg, %.png, $(SVG_FILES))

default: all

all: $(PDF_FILES)

.PHONY: all png

$(PDF_FILES): %.pdf:%.svg
	inkscape $< --export-pdf $@ -d 320
	pdfcrop $@ $@

png: $(PNG_FILES)
$(PNG_FILES): %.png:%.pdf
	pdftocairo -png -r 320 $< $@
	mv $@-1.png $@

clean:
	-rm $(PDF_FILES) $(PNG_FILES)

.PHONY: clean
