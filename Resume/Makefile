LATEX_FILES=$(wildcard *.tex)

include latex.mk

rtf: my-resume.rtf

my-resume.rtf: my-resume.tex
	latex2rtf my-resume.tex
