LANG1=es
LANG2=gl
LANG1a=spa
PREFIX1=$(LANG1)-$(LANG2)
PREFIX2=$(LANG2)-$(LANG1)

BASENAME=apertium-$(PREFIX1)

TARGETS_COMMON =             \
     $(PREFIX1).automorf.bin \
     $(PREFIX1).autobil.bin  \
     $(PREFIX1).autogen.bin  \
     $(PREFIX1).autopgen.bin \
     $(PREFIX2).automorf.bin \
     $(PREFIX2).autobil.bin  \
     $(PREFIX2).autogen.bin  \
     $(PREFIX2).autopgen.bin \
     $(PREFIX1).rlx.bin      \
     $(PREFIX1).t1x.bin      \
     $(PREFIX2).t1x.bin

     # $(PREFIX1).t2x.bin      \
     # $(PREFIX1).t3x.bin      \
     # $(PREFIX2).t2x.bin      \
     # $(PREFIX2).t3x.bin

# This include defines goals for install-modes, .deps/.d and .mode files:
@ap_include@


###############################################################################
## Transducers and rules:
###############################################################################


$(PREFIX1).rlx.bin: $(AP_SRC1)/apertium-$(LANG1a).$(LANG1a).rlx
	cg-comp $< $@

$(PREFIX1).automorf.bin: $(BASENAME).$(LANG1).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX1).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX1).autogen.bin: $(BASENAME).$(LANG2).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

$(PREFIX1).autopgen.bin: $(BASENAME).post-$(LANG2).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX2).automorf.bin: $(BASENAME).$(LANG2).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX2).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

$(PREFIX2).autogen.bin: $(BASENAME).$(LANG1).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

$(PREFIX2).autopgen.bin: $(BASENAME).post-$(LANG1).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX1).t1x.bin: $(BASENAME).$(PREFIX1).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2x.bin: $(BASENAME).$(PREFIX1).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t3x.bin: $(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t1x.bin: $(BASENAME).$(PREFIX2).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2x.bin: $(BASENAME).$(PREFIX2).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t3x.bin: $(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@


###############################################################################
## Distribution
###############################################################################

NOT_YET_MONOLINGUALISED=\
	   $(PREFIX1).prob               \
	   $(PREFIX2).prob               \
	   $(BASENAME).$(LANG1).dix      \
	   $(BASENAME).$(LANG2).dix      \
	   $(BASENAME).post-$(LANG1).dix \
	   $(BASENAME).post-$(LANG2).dix

EXTRA_DIST=$(BASENAME).$(PREFIX1).dix    \
	   $(BASENAME).$(PREFIX1).t1x    \
	   $(BASENAME).$(PREFIX2).t1x    \
	   $(NOT_YET_MONOLINGUALISED)    \
	   modes.xml
#   $(BASENAME).$(PREFIX2).t2x           \
#   $(BASENAME).$(PREFIX1).t2x           \
#   $(BASENAME).$(PREFIX1).t3x           \
#   $(BASENAME).$(PREFIX2).t3x           \
#   $(BASENAME).$(PREFIX1).lrx           \
#   $(BASENAME).$(PREFIX2).lrx

###############################################################################
## Installation
###############################################################################

apertium_es_gldir=$(prefix)/share/apertium/$(BASENAME)/

# Files which should be installed to $(prefix)/share/apertium/$(BASENAME)/:
apertium_es_gl_DATA=$(TARGETS_COMMON) \
	$(BASENAME).$(PREFIX1).t1x    \
	$(BASENAME).$(PREFIX2).t1x    \
	$(PREFIX1).prob               \
	$(PREFIX2).prob
# $(BASENAME).$(PREFIX1).t2x    \
# $(BASENAME).$(PREFIX1).t3x    \
# $(BASENAME).$(PREFIX2).t2x    \
# $(BASENAME).$(PREFIX2).t3x

# All modes are created by the same goal, listing several will just give problems with make -j2
noinst_DATA=modes/$(PREFIX1).mode

install-data-local: install-modes


###############################################################################
## Cleanup
###############################################################################

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes

clean-dicts:
	touch $(BASENAME).$(LANG1).dix $(BASENAME).$(LANG2).dix $(BASENAME).$(PREFIX1).dix
#rm $(BASENAME).$(LANG1).dix
#rm $(BASENAME).$(LANG2).dix
#rm $(BASENAME).$(PREFIX1).dix

###############################################################################
## Test
###############################################################################

test: all
	echo "Mi aerodeslizador está lleno de anguilas" | apertium -d . es-gl | tee .test-mt
	@echo "O meu aerodeslizador está cheo de anguías" > .test-ref
	@diff .test-ref .test-mt
	echo "O meu aerodeslizador esta cheo de anguías" | apertium -d . gl-es | tee .test-mt
	@echo "Mi aerodeslizador esta lleno de anguilas" > .test-ref
	@diff .test-ref .test-mt
	@rm .test-ref .test-mt
