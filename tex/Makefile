.PHONY: all silent

all: main.pdf

%.pdf: %.tex ../tex/main.bib
	cat ../tex/genericHeaders.tex $< ../tex/genericFooters.tex > tmp.tex
	pdflatex tmp $(PDFOPTIONS)
	pdflatex tmp $(PDFOPTIONS)
	# I cannot figure out Make conditional syntax for the life of me
	$(shell if [[ $(grep cite *.tex) == *cite* ]]; then bibtex tmp $(BIBOPTIONS); fi)
	pdflatex tmp $(PDFOPTIONS)
	pdflatex tmp $(PDFOPTIONS)
	mv tmp.pdf $@
	rm -f tmp.*

onlybib: PDFOPTIONS=>/dev/null
onlybib: all

silent: PDFOPTIONS=>/dev/null
silent: BIBOPTIONS=>/dev/null
silent: all

%.tar.gz: %.pdf
	mv $*.tex doNotDelete.tex
	cat ../tex/genericHeaders.tex doNotDelete.tex ../tex/genericFooters.tex > $*.tex
	tar czvf $@ $< $*.tex headers.tex
	rm -f $*.tex
	mv doNotDelete.tex $*.tex

clean:
	rm -f *.blg *.bbl *.aux *.log *.out *~ *.tdo

cleanPDFs:
	rm -f *.pdf *.tar.gz

clear: clean cleanPDFs

