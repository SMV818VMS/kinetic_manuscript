sourcefile_main = main
sourcefile_plos = main_plos
# merged_sourcefile = biochem_merged

# CLEAN_FILES+= *.log *.aux *.toc *.blg ${sourcefile}.pdf ${merged_sourcefile}.* *.xml *.bcf *.bbl *.lof
# CLEAN_FILES+= *.log *.aux *.toc *.blg ${sourcefile_main}.pdf ${sourcefile_plos}.pdf *.xml *.bcf *.bbl *.lof *.dvi *.dep *.out
CLEAN_FILES+= *.log *.aux *.toc *.blg *.xml *.bcf *.bbl *.lof *.dvi *.dep *.out

RM = rm -f

default : pdf

$(sourcefile_main).pdf : $(sourcefile_main).tex

	pdflatex $(sourcefile_main)
	@if(grep "There were undefined references" $(sourcefile_main).log > /dev/null);\
	then \
		bibtex $(sourcefile_main); \
		pdflatex $(sourcefile_main); \
	fi
	
	@if(grep "Rerun" $(sourcefile_main).log > /dev/null);\
	then \
		pdflatex $(sourcefile_main);\
	fi
	# XXX Leave this out until the end
	# Finally flatten the file for submission to journals
	# python flatex.py $(sourcefile).tex $(merged_sourcefile).tex
	# Then make sure you get a fully functional pdf
	# pdflatex $(merged_sourcefile)
	# bibtex $(merged_sourcefile)
	# pdflatex $(merged_sourcefile)

$(sourcefile_plos).pdf : $(sourcefile_plos).tex

	latex $(sourcefile_plos)
	bibtex $(sourcefile_plos)
	latex $(sourcefile_plos)
	latex $(sourcefile_plos)
	dvipdfm $(sourcefile_plos)

pdf : $(sourcefile_main).pdf

plos: $(sourcefile_plos).pdf


.PHONY : clean
clean :
	$(RM) ${CLEAN_FILES}


