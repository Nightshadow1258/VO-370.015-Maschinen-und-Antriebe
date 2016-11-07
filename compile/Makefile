filename=./../src/main
output=./../output

inputs.tex: $(wildcard dir/../src/bsp/*/*.tex)
	ls ./../src/bsp/*/*.tex | awk '{printf "\\input{%s}\n", $$1}' > ./../src/inputs.tex

pdflatex:
	pdflatex -synctex=1 -interaction=nonstopmode -output-directory='${output}' '${filename}.tex'

latex:
	latex -synctex=1 -halt-on-error -interaction=errorstopmode -output-directory='${output}' '${filename}.tex'
pdf: ps
	ps2pdf ${filename}.ps

pdf-print: ps
	ps2pdf -dColorConversionStrategy=/LeaveColorUnchanged -dPDFSETTINGS=/printer ${filename}.ps

text: html
	html2text -width 100 -style pretty ${filename}/${filename}.html | sed -n '/./,$$p' | head -n-2 >${filename}.txt

ps:	dvi
	dvips -t letter ${filename}.dvi

dvi:
	latex ${filename}
	bibtex ${filename}||true
	latex ${filename}
	latex ${filename}

read:
	evince ${filename}.pdf &

aread:
	acroread ${filename}.pdf

clean:
	rm -f ${output}/main.{ps,pdf,log,aux,out,dvi,bbl,blg,toc}