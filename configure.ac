AC_PREREQ([2.57])
AC_INIT(sde-session-manager,[0.4.6.1])
AM_INIT_AUTOMAKE([1.11 -Wall -Werror foreign])

# Support silent build rules. Disable by either passing --disable-silent-rules
# to configure or passing V=1 to make
AM_SILENT_RULES([yes])
AC_PROG_INTLTOOL(, [no-xml])
AM_MAINTAINER_MODE

AM_CONFIG_HEADER(config.h)
AC_CONFIG_MACRO_DIR([m4])

AC_PROG_CC
AC_PROG_INSTALL
AM_PROG_CC_C_O
AC_PROG_CC_STDC

#Initialize libtool
LT_PREREQ([2.2])
LT_INIT

AC_CHECK_FUNC([mkstemp],
   AC_DEFINE(HAS_MKSTEMP,1,[Define to 1 if you have the 'mkstemp' function.]))

AC_ARG_ENABLE(more_warnings,
       [AC_HELP_STRING([--enable-more-warnings],
               [Add more warnings @<:@default=no@:>@])],
       [enable_more_warnings="${enableval}"],
       [enable_more_warnings=no]
)

if test x"$enable_more_warnings" = x"yes"; then
  ADDITIONAL_FLAGS="-Wall -Werror=all -Werror=format -Werror=implicit-function-declaration -Werror=implicit-int -Werror=missing-braces -Werror=parentheses -Werror=return-type -Werror=strict-aliasing -Werror=switch -Wuninitialized -Werror=unused-label -Werror=unused-value -Wextra -Wno-missing-field-initializers -Wno-unused-parameter -Werror=missing-declarations -Wredundant-decls -Wmissing-noreturn -Wpointer-arith -Wcast-align -Wwrite-strings -Werror=inline -Werror=format-nonliteral -Wformat-nonliteral -Werror=format-security -Wformat-security -Winit-self -Werror=missing-include-dirs -Werror=undef -Werror=aggregate-return -Wmissing-format-attribute -Werror=nested-externs -fno-strict-aliasing -fmessage-length=0 -Wp,-D_FORTIFY_SOURCE=2 -DG_DISABLE_DEPRECATED -DG_DISABLE_SINGLE_INCLUDES -DGDK_DISABLE_DEPRECATED -DGDK_PIXBUF_DISABLE_DEPRECATED -DGDK_PIXBUF_DISABLE_SINGLE_INCLUDES -DGTK_DISABLE_DEPRECATED -DGTK_DISABLE_SINGLE_INCLUDES"
fi
AC_SUBST(ADDITIONAL_FLAGS)

gtk_modules="gtk+-2.0 >= 2.24.0"
PKG_CHECK_MODULES(GTK, [$gtk_modules])
AC_SUBST(GTK_CFLAGS)
AC_SUBST(GTK_LIBS)

PKG_CHECK_MODULES(X11, [x11])
AC_SUBST(X11_CFLAGS)
AC_SUBST(X11_LIBS)

PKG_CHECK_MODULES(GLIB, [glib-2.0 >= 2.6.0])
AC_SUBST(GLIB_CFLAGS)
AC_SUBST(GLIB_LIBS)

AC_ARG_ENABLE(
    [dbus],
    AS_HELP_STRING([--enable-dbus],
                   [Build with Linux D-Bus support for shutdown/reboot/suspend (default: yes)]),
    use_dbus=$enableval, use_dbus="yes")

if test x"$use_dbus" = x"yes"; then
dnl Check DBUS support
    dbus_modules="dbus-1"
    PKG_CHECK_MODULES(DBUS, [$dbus_modules], [have_dbus=yes], [have_dbus=no])

    if test x"$have_dbus" = x"yes"; then
        AC_DEFINE([HAVE_DBUS], [1], [Define to 1 if you have DBUS.])
    else
        AC_MSG_ERROR([To build with DBUS support, you must have the development package for dbus-1, or you can use --disable-dbus to disable DBUS support.])
    fi
fi
AM_CONDITIONAL(USE_DBUS, test "$use_dbus" = "yes")
AC_SUBST(DBUS_CFLAGS)
AC_SUBST(DBUS_LIBS)

# Generate po/LINGUAS on the fly rather than relying on translators
# to maintain it manually. This also overcome the problem that Transifex
# cannot add a language to po/LINGUAS if a new po file is submitted.
rm -f $srcdir/po/LINGUAS
for po_file in `ls $srcdir/po/*.po | sort`;
do
    lang=`echo "$po_file" | sed "s|.*/po/\(.*\)\.po|\1|g"`
    echo $lang >> $srcdir/po/LINGUAS
done

GETTEXT_PACKAGE=sde-session-manager
AC_SUBST(GETTEXT_PACKAGE)
AM_GLIB_GNU_GETTEXT
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE,"$GETTEXT_PACKAGE", [Gettext package.])

AC_OUTPUT([
  Makefile
  sde-session-manager/Makefile
  sde-logout/Makefile
  po/Makefile.in
])

echo
echo SDE Session Manager.......................... : Version $VERSION
echo
echo Prefix....................................... : $prefix
echo Linux DBUS support........................... : $use_dbus
echo
echo The binary will be installed in $prefix/bin
echo
echo
echo Have fun!
echo
