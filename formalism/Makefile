PAPER           = formalism
LATEX           = pdflatex
UNAME          := $(shell uname)
BUILDDIR	= build
LATEXMK_FLAGS	= -outdir=$(BUILDDIR) -pdf

default: quick
all: paper

quick:
	${LATEX} ${PAPER}.tex
	${MAKE} open

# Build the final PDF:
paper:
	latexmk $(LATEXMK_FLAGS) -pdf ${PAPER} -f
	${MAKE} open

dumb:
	${LATEX} ${PAPER}.tex
	bibtex ${PAPER}
	${LATEX} ${PAPER}.tex
	bibtex ${PAPER}
	${LATEX} ${PAPER}.tex
	${MAKE} open

# ----------------------------------------

# Build with editorial markup rather than the final pdf:
ed: editingmarks
editingmarks:
	touch activateeditingmarks
	${MAKE} paper

plain:
	rm -f activateeditingmarks
	${MAKE} paper

both:
	touch activateeditingmarks
	${LATEX} ${PAPER}.tex
	cp ${PAPER}.pdf wmarks.pdf
	open wmarks.pdf

	rm -f activateeditingmarks
	${LATEX} ${PAPER}.tex
	cp ${PAPER}.pdf plain.pdf
	open plain.pdf

# A little shorthand for Ryan:
grey:
	touch activategreybg.tex
	${MAKE} paper
white:
	rm -f activategreybg.tex
	${MAKE} paper

# Continuous building
continuous:
	latexmk $(LATEXMK_FLAGS) -pdf -pvc ${PAPER}.tex


# Open the PDF in a viewer after building:
open: ${PAPER}.pdf
ifeq (${UNAME}, Darwin)
	open -a skim ${PAPER}.pdf
endif
ifeq (${UNAME}, Linux)
	evince ${PAPER}.pdf &
endif

clean:
	rm -f *.out *.aux *.bbl *.log *.blg ${PAPER}.pdf
	latexmk $(LATEXMK_FLAGS) -C $(PAPER)
