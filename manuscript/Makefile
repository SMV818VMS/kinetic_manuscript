# sourcefile = main
sourcefile = main_plos
# merged_sourcefile = biochem_merged

# CLEAN_FILES+= *.log *.aux *.toc *.blg ${sourcefile}.pdf ${merged_sourcefile}.* *.xml *.bcf *.bbl *.lof
CLEAN_FILES+= *.log *.aux *.toc *.blg ${sourcefile}.pdf *.xml *.bcf *.bbl *.lof

RM = rm -f

default : pdf

$(sourcefile).pdf : $(sourcefile).tex

	pdflatex $(sourcefile)
	@if(grep "There were undefined references" $(sourcefile).log > /dev/null);\
	then \
		bibtex $(sourcefile); \
		pdflatex $(sourcefile); \
	fi
	
	@if(grep "Rerun" $(sourcefile).log > /dev/null);\
	then \
		pdflatex $(sourcefile);\
	fi
	# XXX Leave this out until the end
	# Finally flatten the file for submission to journals
	# python flatex.py $(sourcefile).tex $(merged_sourcefile).tex
	# Then make sure you get a fully functional pdf
	# pdflatex $(merged_sourcefile)
	# bibtex $(merged_sourcefile)
	# pdflatex $(merged_sourcefile)

pdf : $(sourcefile).pdf

plos: 

	latex $(sourcefile)
	bibtex $(sourcefile)
	latex $(sourcefile)
	latex $(sourcefile)
	dvipdfm $(sourcefile)


.PHONY : clean
clean :
	$(RM) ${CLEAN_FILES}


