AM_CPPFLAGS = \
	-I$(top_srcdir)/src/libstrongswan

AM_CFLAGS = \
	$(PLUGIN_CFLAGS) \
	@COVERAGE_CFLAGS@

# these file are also used by bliss_huffman
noinst_LTLIBRARIES = libbliss-params.la
libbliss_params_la_SOURCES = \
	bliss_param_set.h bliss_param_set.c \
	bliss_fft_params.h bliss_fft_params.c

# these files are also used by the tests, we can't directly refer to them
# because of the subdirectory, which would cause distclean to fail
noinst_LTLIBRARIES += libbliss.la
libbliss_la_SOURCES = \
	bliss_private_key.h bliss_private_key.c \
	bliss_public_key.h bliss_public_key.c \
	bliss_signature.h bliss_signature.c \
	bliss_utils.h bliss_utils.c \
	bliss_bitpacker.h bliss_bitpacker.c \
	bliss_fft.h bliss_fft.c \
	bliss_huffman_code.h bliss_huffman_code.c \
	bliss_huffman_code_1.c bliss_huffman_code_3.c bliss_huffman_code_4.c \
	bliss_huffman_coder.h bliss_huffman_coder.c \
	bliss_sampler.h bliss_sampler.c
libbliss_la_LIBADD = libbliss-params.la

CLEANFILES = \
	bliss_huffman_code_1.c bliss_huffman_code_3.c bliss_huffman_code_4.c

if MONOLITHIC
noinst_LTLIBRARIES += libstrongswan-bliss.la
else
plugin_LTLIBRARIES = libstrongswan-bliss.la
endif

libstrongswan_bliss_la_SOURCES = \
	bliss_plugin.h bliss_plugin.c

libstrongswan_bliss_la_LDFLAGS = -module -avoid-version

libstrongswan_bliss_la_LIBADD = libbliss.la

noinst_PROGRAMS = bliss_huffman

bliss_huffman_SOURCES = bliss_huffman.c
bliss_huffman_LDADD = -lm libbliss-params.la

bliss_huffman_code_1.c :	bliss_huffman bliss_huffman_code.h
	$(AM_V_GEN) \
	./bliss_huffman 1 8 > $@ 2>/dev/null

bliss_huffman_code_3.c :	bliss_huffman bliss_huffman_code.h
	$(AM_V_GEN) \
	./bliss_huffman 3 16 > $@ 2>/dev/null

bliss_huffman_code_4.c :	bliss_huffman bliss_huffman_code.h
	$(AM_V_GEN) \
	./bliss_huffman 4 32 > $@ 2>/dev/null
