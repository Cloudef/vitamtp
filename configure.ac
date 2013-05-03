#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT(vitamtp, 1.0, support@yifanlu.com)
AC_OUTPUT(Makefile src/Makefile)
AC_CONFIG_SRCDIR([src/vitamtp.c])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_FILES([libvitamtp.pc])
AM_INIT_AUTOMAKE

# Checks for programs.
AC_PROG_CC
AC_PROG_LIBTOOL
AM_PROG_CC_C_O
AC_PROG_INSTALL
AM_ICONV

# Optionally enable and check for doxygen
AC_ARG_ENABLE([doxygen],
    AS_HELP_STRING([--enable-doxygen], [Build API documentation using Doxygen [default=no]]),
    [ac_enable_doxygen=$enableval], [ac_enable_doxygen=auto])
if test "x$ac_enable_doxygen" == "xyes"; then
    AC_CHECK_PROG(HAVE_DOXYGEN, doxygen, true, false)
    if test "x$HAVE_DOXYGEN" = "xfalse" -a "x$ac_enable_doxygen" = "xyes"; then
        AC_MSG_ERROR([*** API documentation explicitly requested but Doxygen not found])
    fi
    AC_MSG_NOTICE([API documentation will be generated using Doxygen])
else
    HAVE_DOXYGEN=false
    AC_MSG_NOTICE([API documentation will not be generated])
fi
AM_CONDITIONAL(HAVE_DOXYGEN,$HAVE_DOXYGEN)

# Check for Darwin
AC_MSG_CHECKING([if the host operating system is Darwin])
case "$host" in
  *-darwin*)
    AC_MSG_RESULT([yes])
    CFLAGS="$CFLAGS -DUSE_DARWIN"
    OSFLAGS="-framework IOKit -framework CoreFoundation"
    ;;
  *) AC_MSG_RESULT([no]) ;;
esac
AC_SUBST(OSFLAGS)

# Checks for libraries.
AC_CHECK_FUNC([pthread_create], [], [AC_MSG_ERROR([pthread not found])])
AC_CHECK_HEADERS([pthread.h semaphore.h], [], [AC_MSG_ERROR([Cannot find pthread header])])
AC_CHECK_LIB([xml2], [xmlReadMemory], [], [AC_MSG_ERROR([libxml2 not found])])
AC_CHECK_HEADERS([libxml/parser.h libxml/xmlmemory.h libxml/xmlwriter.h], [], [AC_MSG_ERROR([Cannot find libxml2 header])])
AC_CHECK_LIB([usb-1.0], [libusb_init], [], [AC_MSG_ERROR([libusb-1.0 not found])])
AC_CHECK_HEADERS([libusb-1.0/libusb.h], [], [AC_MSG_ERROR([Cannot find libusb-1.0 header])])
#PKG_CHECK_MODULES(MTP, libmtp, found_libmtp=yes, found_libmtp=no)
#AC_SUBST(MTP_CFLAGS)
#AC_SUBST(MTP_LIBS)
#AC_SUBST(MTP_STATIC_LIBS)
#if test x"$found_libmtp" = "xno" ; then
#    AC_MSG_ERROR([Cannot find libmtp, please install it and make sure pkg-config can see it.])
#else
#    MTP_STATIC_LIBS="`pkg-config --static --libs libmtp`"
#fi

# Checks for additional headers
AC_CHECK_HEADERS([errno.h fcntl.h iconv.h limits.h stdarg.h stdlib.h string.h sys/statvfs.h time.h unistd.h], [], [AC_MSG_ERROR([Cannot find required header.])])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_INLINE
AC_TYPE_OFF_T
AC_TYPE_SIZE_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T
AC_TYPE_UINT8_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_MEMCMP
AC_FUNC_MKTIME
AC_FUNC_STAT
AC_CHECK_FUNCS([getcwd memset mkdir strchr strcspn strdup strrchr strstr strtol], [], [AC_MSG_ERROR([Cannot find required function.])])

# Output
# Required for gphoto-ptp2
AX_NEED_STDINT_H([src/_stdint.h])
AC_NEED_BYTEORDER_H(src/gphoto2-endian.h)

AC_OUTPUT