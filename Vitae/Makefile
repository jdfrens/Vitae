LATEX = latex -interaction=nonstopmode
BIBTEX = bibtex
L2H = latex2html
PDFLATEX = ps2pdf
DVIPS = dvips -t letter


RERUN = "(There were undefined references|Rerun to get (cross-references|the bars) right)"
RERUNBIB = "No file.*\.bbl|Citation.*undefined" 


TEXFILES = myvita.tex
DVIFILES = ${TEXFILES:.tex=.dvi}
GOALS = ${TEXFILES:.tex=.ps}

COPY = if test -r $*.toc; then cp $*.toc $*.toc.bak; fi

main: $(DVIFILES)

all: $(GOALS)

print: $(GOALS)
	lpr -Pmcs $(GOALS)

%.dvi: %.tex 
	$(COPY); $(LATEX) $<
	egrep -c $(RERUNBIB) $*.log && ($(BIBTEX) $*;$(COPY);$(LATEX) $<) ; true
	egrep $(RERUN) $*.log && ($(COPY);$(LATEX) $<) ; true
	egrep $(RERUN) $*.log && ($(COPY);$(LATEX) $<) ; true
	if cmp -s $*.toc $*.toc.bak; then . ;else $(LATEX) $< ; fi
	$(RM) $*.toc.bak
# Display relevant warnings
	egrep -i "(Reference|Citation).*undefined" $*.log ; true

%.ps: %.dvi
	$(DVIPS) $< -o $@

%.pdf: %.ps
	$(PDFLATEX) $<

clean: 
	$(RM) -f *.aux *.log *.bbl *.blg *.brf *.cb *.ind *.idx *.ilg  \
	*.inx *.ps *.dvi *.pdf *.toc *.out
