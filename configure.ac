AC_PREREQ(2.52)

AC_INIT([Apertium Spanish-Galician], [1.0.9], [apertium-stuff@lists.sourceforge.net], [apertium-es-gl], [https://wiki.apertium.org/wiki/Apertium-es-gl])
AM_INIT_AUTOMAKE
AC_PROG_AWK

PKG_CHECK_MODULES(APERTIUM,   apertium >= 3.7.1)
PKG_CHECK_MODULES(LTTOOLBOX, lttoolbox >= 3.5.3)
PKG_CHECK_MODULES(CG3, cg3 >= 1.3.1)

m4_ifdef([AP_CHECK_LING],[],[AC_MSG_ERROR([AP_CHECK_LING not defined, is apertium.m4 in ACLOCAL_PATH? See: http://wiki.apertium.org/wiki/Installation_troubleshooting])])

AP_CHECK_LING([1], [apertium-spa], [1.2.1])
dnl AP_CHECK_LING([2], [apertium-glg])

AP_MKINCLUDE

AC_OUTPUT([Makefile])
