## Process this file with automake to produce Makefile.in
## ------------------------------------------------------------------------
## Makefile.am (toplevel)
## autotools build system for YAF
## ------------------------------------------------------------------------
## Copyright (C) 2006-2015 Carnegie Mellon University. All Rights Reserved.
## ------------------------------------------------------------------------
## Authors: Brian Trammell
## ------------------------------------------------------------------------
## GNU General Public License (GPL) Rights pursuant to Version 2, June 1991
## Government Purpose License Rights (GPLR) pursuant to DFARS 252.227-7013
## ------------------------------------------------------------------------


AUTOMAKE_OPTIONS = check-news subdir-objects

ACLOCAL_AMFLAGS = -I m4

# Avoid picking up MacOS X resource forks in "make dist"
am__tar = COPY_EXTENDED_ATTRIBUTES_DISABLE=1 COPYFILE_DISABLE=1 ${AMTAR} cof - "$$tardir"

SUBDIRS = airframe libltdl src include etc scripts

include doxygen.am

MOSTLYCLEANFILES = $(DX_CLEANFILES)

utils-doc:
	(cd $(top_builddir)/src && $(MAKE) docs)
	(cd $(top_builddir)/scripts && $(MAKE) docs)
	(cd $(top_builddir)/airframe/doc && $(MAKE) docs)

release-note-doc: NEWS
	$(top_srcdir)/doc/news2xhtml.pl yaf gpl 16 < $(top_srcdir)/NEWS > doc/releases.xml

make-doc-path:
	mkdir -p $(top_builddir)/doc/html

copy-doxygen-doc:
	cp -pr doc/html $(distdir)/doc

dist-hook: docs copy-doxygen-doc
	find $(distdir) -name .svn -type d -prune -exec rm -rf '{}' ';'

distclean-local:
	rm -f $(top_builddir)/doc/releases.xml

docs: make-doc-path doxygen-doc utils-doc release-note-doc

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libyaf.pc

DISTCLEANFILES = $(YAF_SUMMARY_FILE)

EXTRA_DIST = \
    Doxyfile.in \
    DoxygenLayout.xml \
    yaf.spec \
    yaf.spec.in \
    doc/add-header.pl \
    doc/Doxyhead.html \
    doc/Doxyfoot.html \
    doc/doxygen.css \
    doc/news2xhtml.pl \
    doc/howto/yaf_pcap.md \
    doc/howto/yaf_pcap2.md \
    doc/howto/yaf_super_silk.md \
    doc/howto/yaf_silk.md \
    doc/howto/yaf_orcus.md \
    doc/LICENSE.txt

