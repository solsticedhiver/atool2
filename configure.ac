AC_INIT(atool, 0.39.0, oskar@osk.mine.nu)
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_SRCDIR([atool])
AC_CONFIG_AUX_DIR([build-aux])
AM_INIT_AUTOMAKE

AC_DEFINE_DIR(SBINDIR, sbindir)
AC_DEFINE_DIR(SYSCONFDIR, sysconfdir)
AC_DEFINE_DIR(LOCALSTATEDIR, localstatedir)

dnl Perl stuff
AC_PATH_PROG([PERL], [perl])
eval `$PERL -V:startperl`
if test "${startperl:0:1}" = "#" ; then
  startperl="\\$startperl"
fi
AC_SUBST(PERL_SHEBANG, $startperl)
eval `$PERL -V:sitelib`
AC_SUBST(PERL_SITELIB, $sitelib)

AC_CONFIG_FILES([
  atool.1
  atool.spec
  Makefile
])
AC_CONFIG_COMMANDS([acat-link], [ln -f -s atool acat])
AC_CONFIG_COMMANDS([adiff-link], [ln -f -s atool adiff])
AC_CONFIG_COMMANDS([als-link], [ln -f -s atool als])
AC_CONFIG_COMMANDS([apack-link], [ln -f -s atool apack])
AC_CONFIG_COMMANDS([aunpack-link], [ln -f -s atool aunpack])
AC_CONFIG_COMMANDS([arepack-link], [ln -f -s atool arepack])
AC_OUTPUT
