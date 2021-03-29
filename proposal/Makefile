# Default Makefile. This make file provides feature to split a paper into two
# parts which is often useful to when submitting supplementary material and
# paper separately. Refer to the `split' target below on the syntax.
PROJNAME=proposal

# Prevent Make from deleting pdfs when Ctr-C exiting.
.PRECIOUS: $(PROJNAME).pdf

all: $(PROJNAME).pdf

# -pdf tells latexmk to generate PDF directly (instead of DVI).
# -use-make tells latexmk to call make for generating missing files.
# -pvc : Preview continuous mode, wont' work with Adobe
# -interactive=nonstopmode keeps the pdflatex backend from stopping at a
# missing file reference and interactively asking you for an alternative.

$(PROJNAME).pdf: $(PROJNAME).tex
	#latexmk -pdf -pvc -xelatex	-interaction=nonstopmode $(PROJNAME).tex 
	latexmk -pdf -pvc -interaction=nonstopmode $(PROJNAME).tex 

# Use this for debuggin. i.e. run $ make interactive
interactive: $(PROJNAME).tex
	#latexmk -pdf -pvc -xelatex	$(PROJNAME).tex 
	latexmk -pdf -pvc $(PROJNAME).tex 


# USAGE: make split END=PAGE_NUMBER VER=version
# where PAGE_NUMBER is last page of main (inclusive)
# example: $ make split END=12 VER=3
split:
	cp $(PROJNAME).pdf $(PROJNAME)-$(VER).pdf
	pdftk  $(PROJNAME).pdf  cat 1-$(END) output $(PROJNAME)-$(VER)-main.pdf
	pdftk  $(PROJNAME).pdf  cat $(END)-end output $(PROJNAME)-supp_.pdf
	pdftk  $(PROJNAME)-supp_.pdf cat 2-end output $(PROJNAME)-$(VER)-supp.pdf
	rm $(PROJNAME)-supp_.pdf

# Does not delete PDF
clean:
	latexmk -c
	rm -f *.log *.bbl

# Deletes intermediary bbl file and pdf
cleanall:
	latexmk -C
	rm -f *.log *.bbl *.aux *.fls *.blg *.out
