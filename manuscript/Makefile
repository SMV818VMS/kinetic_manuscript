sourcefile_main = main
sourcefile_plos = main_plos
sourcefile_bmc = bmc_article
# merged_sourcefile = biochem_merged

# CLEAN_FILES+= *.log *.aux *.toc *.blg ${sourcefile}.pdf ${merged_sourcefile}.* *.xml *.bcf *.bbl *.lof
CLEAN_FILES+= *.log *.aux *.toc *.blg ${sourcefile_main}.pdf ${sourcefile_plos}.pdf *.xml *.bcf *.bbl *.lof *.dvi *.dep *.out ${sourcefile_bmc}.pdf
# CLEAN_FILES+= *.log *.aux *.toc *.blg *.xml *.bcf *.bbl *.lof *.dvi *.dep *.out

RM = rm -f

# default : pdf
default : bmc

$(sourcefile_main).pdf : $(sourcefile_main).tex

	pdflatex --shell-escape $(sourcefile_main)
	@if(grep "There were undefined references" $(sourcefile_main).log > /dev/null);\
	then \
		bibtex $(sourcefile_main); \
		pdflatex --shell-escape $(sourcefile_main); \
	fi
	
	@if(grep "Rerun" $(sourcefile_main).log > /dev/null);\
	then \
		pdflatex --shell-escape $(sourcefile_main);\
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


$(sourcefile_bmc).pdf : $(sourcefile_bmc).tex

	latex $(sourcefile_bmc)
	bibtex $(sourcefile_bmc)
	latex $(sourcefile_bmc)
	latex $(sourcefile_bmc)
	dvipdfm $(sourcefile_bmc)

	# pdflatex --shell-escape $(sourcefile_bmc)
	# @if(grep "There were undefined references" $(sourcefile_bmc).log > /dev/null);\
	# then \
		# bibtex $(sourcefile_bmc); \
		# pdflatex --shell-escape $(sourcefile_bmc); \
	# fi
	# 
	# @if(grep "Rerun" $(sourcefile_bmc).log > /dev/null);\
	# then \
		# pdflatex --shell-escape $(sourcefile_bmc);\
	# fi

pdf : $(sourcefile_main).pdf

plos: $(sourcefile_plos).pdf

bmc: $(sourcefile_bmc).pdf


.PHONY : clean
clean :
	$(RM) ${CLEAN_FILES}


