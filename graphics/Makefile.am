# Copyright (C) 2017 Roland Lutz

texsources = tiles-386.tex tiles-1k.tex tiles-8k.tex tiles-common.tex
txtsources = tiles-386.txt tiles-1k.txt tiles-8k.txt
sources = $(texsources) $(txtsources)

pdfoutput = tiles-386.pdf tiles-1k.pdf tiles-8k.pdf
epsoutput = tiles-386.eps tiles-1k.eps tiles-8k.eps
jpgoutput = tiles-386.jpg tiles-1k.jpg tiles-8k.jpg
output = $(pdfoutput) $(epsoutput) $(jpgoutput)

all-local: $(jpgoutput)
pdf-local: $(pdfoutput)
dvi-local: $(epsoutput)
ps-local: $(epsoutput)
html-local: $(jpgoutput)

MAINTAINERCLEANFILES = $(output)

EXTRA_DIST = $(sources) $(output)

tiles-386.pdf: tiles-386.tex tiles-common.tex
tiles-1k.pdf: tiles-1k.tex tiles-common.tex
tiles-8k.pdf: tiles-8k.tex tiles-common.tex

.tex.pdf:
	mkdir -p run.$$$$ && (cd "$(srcdir)" && pdflatex -output-directory "$(abs_builddir)/run.$$$$" `basename "$<"`) && mv run.$$$$/`basename "$@"` . && rm -rf run.$$$$

.pdf.eps:
	pdf2ps $< $@

.pdf.jpg:
	gimp --new-instance --no-interface --no-data --no-fonts --console-messages --batch '(let ((image (car (file-pdf-load RUN-NONINTERACTIVE "$<" "$<")))) (file-jpeg-save RUN-NONINTERACTIVE image (car (gimp-image-get-active-drawable image)) "$@" "$@" .9 0. TRUE TRUE "" 2 FALSE 0 0)) (gimp-quit TRUE)'

mostlyclean-local:
	rm -rf run.*
