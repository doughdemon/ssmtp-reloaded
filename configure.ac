dnl Process this file with autoconf to produce a configure script.
AC_INIT([ssmtp], [0.9.2])
AC_CONFIG_SRCDIR(ssmtp.c)

dnl Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_SED
AC_PATH_PROG([GROUPADD], [groupadd])

dnl Checks for libraries.

dnl Checks for header files.
AC_CHECK_HEADERS(syslog.h)


AC_CACHE_CHECK([for obsolete openlog],ssmtp_cv_obsolete_openlog,
	[ AC_TRY_COMPILE([#include <syslog.h> ] , [ openlog("xx",1); ] , 
	ssmtp_cv_obsolete_openlog=yes, ssmtp_cv_obsolete_openlog=no)]
)


dnl Checks for typedefs, structures, and compiler characteristics.

dnl Checks for libraries.
AC_SEARCH_LIBS(gethostname, nsl)
AC_SEARCH_LIBS(socket, socket)

dnl Checks for library functions.
AC_CHECK_FUNCS(strndup)

dnl Check for optional features
AC_ARG_ENABLE(logfile, 
[  --enable-logfile        additional logging over and above syslog])
if test x$enableval = xyes ; then
	AC_DEFINE(LOGFILE)
fi
enableval=""

AC_ARG_ENABLE(rewrite-domain,
[  --disable-rewrite-domain
                          support for rewriting the sending domain])
if test x$enableval != xno ; then
	AC_DEFINE(REWRITE_DOMAIN)
fi
enableval=""

AC_ARG_ENABLE(ssl,
[  --enable-ssl           support for secure connection to mail server])
AC_ARG_WITH([gnutls],
  AS_HELP_STRING([--with-gnutls], [Use GnuTLS for SSL support]))
if test x$enable_ssl = "xyes" ; then
       	AC_DEFINE(HAVE_SSL)
        if test "x$with_gnutls" != "xyes"; then
        	LIBS="$LIBS -lssl -lcrypto"
        else
                AC_DEFINE([HAVE_GNUTLS])
                LIBS="$LIBS -lgnutls-openssl"
        fi
fi

AC_ARG_ENABLE(inet6,
[  --enable-inet6         support for IPv6 transport])
if test x$enableval = xyes ; then
	AC_DEFINE(INET6)
fi
enableval=""

AC_ARG_ENABLE(md5auth,
[  --enable-md5auth         support for MD5 authentication])
if test x$enableval = xyes ; then
	AC_DEFINE(MD5AUTH)
	SRCS="$SRCS md5auth/md5c.c md5auth/hmac_md5.c"
fi
enableval=""

AC_SUBST(SRCS)

AC_CONFIG_FILES(Makefile)
AC_OUTPUT
