pkglib_LTLIBRARIES = libexpr.la

libexpr_la_SOURCES = \
 nixexpr.cc eval.cc primops.cc lexer-tab.cc parser-tab.cc \
 get-drvs.cc attr-path.cc value-to-xml.cc common-opts.cc \
 names.cc

pkginclude_HEADERS = \
 nixexpr.hh eval.hh eval-inline.hh lexer-tab.hh parser-tab.hh \
 get-drvs.hh attr-path.hh value-to-xml.hh common-opts.hh \
 names.hh symbol-table.hh value.hh

libexpr_la_LIBADD = ../libutil/libutil.la ../libstore/libstore.la \
 ../boost/format/libformat.la @BDW_GC_LIBS@

BUILT_SOURCES = \
 parser-tab.hh lexer-tab.hh parser-tab.cc lexer-tab.cc

EXTRA_DIST = lexer.l parser.y

AM_CXXFLAGS = \
 -I$(srcdir)/.. \
 -I$(srcdir)/../libutil -I$(srcdir)/../libstore


# Parser generation.

parser-tab.cc parser-tab.hh: parser.y
	$(bison) -v -o parser-tab.cc $(srcdir)/parser.y -d

lexer-tab.cc lexer-tab.hh: lexer.l
	$(flex) --outfile lexer-tab.cc --header-file=lexer-tab.hh $(srcdir)/lexer.l 


# SDF stuff (not built by default).
nix.tbl: nix.sdf
	sdf2table -m Nix -s -i nix.sdf -o nix.tbl

test.ast: test.nix nix.tbl
	sglri -p nix.tbl -i test.nix -o test.ast
