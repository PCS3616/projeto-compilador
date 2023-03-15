.PHONY: all clean

LIBGS ?= /usr/lib/libgs.so

all: programa.svg comando.svg expressao.svg

%.svg: %.dvi
	dvisvgm --libgs=$(LIBGS) -o $@ $<

%.dvi: %.tex
	latex $<

clean:
	git clean -Xf
