IMG_OBJECTS = 
FIG_OBJECTS = 
DOT_OBJECTS = bi-tree-sequence clist clist1 ftr-empty ftr-leaf ftr-ab \
ftr-abcde ftr-abcdef bralst-1 bralst-2 bralst-3 bralst-4 bralst-5 bralst-6 \
bralst-4l bralst-4lr ftr-10 ftr-9 ftr-8 palist ftr-illed-1 ftr-illed-2 \
ftr-illed-i
DOT_SOURCES = $(foreach file, $(DOT_OBJECTS), $(file).dot)

#suffix replacement, replace .dot with .png
PNG_OBJECTS = $(DOT_SOURCES:.dot=.png)
EPS_OBJECTS = $(IMG_OBJECTS:.png=.eps)

.SUFFIXES: .eps .jpg .png .dot .ps

.PHONY: all

all: convert dot

convert: $(IMG_OBJECTS)

# If there is xfig installed
#    user can run 'make xfig' to generate eps file from fig source.
#    However, in order to minimize the tool-chain, we exclude xfig.
xfig: $(FIG_OBJECTS)

$(FIG_OBJECTS): % : %.eps

# for details, refer to: 
#    http://www.gnu.org/software/autoconf/manual/make/
# Makefile syntax, replace each '%' to 'eps
$(IMG_OBJECTS): % : %.eps

# pattern rule matching
# Makefile auto variable: $< first prerequisite, $@ target
%.eps : %.png
	convert $< $@

dot: $(DOT_OBJECTS)

$(DOT_OBJECTS): % : %.ps

# Makefile auto variable: $< first prerequisite, $@ target
%.ps : %.dot
	dot -Tps -o $@ $<

png: $(PNG_OBJECTS)

%.png : %.dot
	dot -Tpng -o $@ $<

%.eps : %.fig
	fig2dev -L eps -m 1.00 -c $< $@

clean:
	rm -f *.ps *.pdf *~
	rm -f $(PNG_OBJECTS)
	rm -f $(EPS_OBJECTS)
