dnl Licensed to the Apache Software Foundation (ASF) under one or more
dnl contributor license agreements.  See the NOTICE file distributed with
dnl this work for additional information regarding copyright ownership.
dnl The ASF licenses this file to You under the Apache License, Version 2.0
dnl (the "License"); you may not use this file except in compliance with
dnl the License.  You may obtain a copy of the License at
dnl 
dnl   http://www.apache.org/licenses/LICENSE-2.0
dnl 
dnl Unless required by applicable law or agreed to in writing, software
dnl distributed under the License is distributed on an "AS IS" BASIS,
dnl WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
dnl See the License for the specific language governing permissions and
dnl limitations under the License.
dnl run autogen.sh to generate the configure script.

AC_PREREQ(2.59)

AC_INIT(tcpmon-src, 1.7.0)
AC_CANONICAL_SYSTEM
AM_CONFIG_HEADER(config.h)
AM_INIT_AUTOMAKE(AC_PACKAGE_NAME, AC_PACKAGE_VERSION)
AC_PREFIX_DEFAULT(/usr/local/tcpmon)

dnl Checks for programs.
AC_PROG_CC
AC_PROG_CPP
AC_PROG_LIBTOOL
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET


CFLAGS="$CFLAGS -D_LARGEFILE64_SOURCE"
if test "$GCC" = "yes"; then
    CFLAGS="$CFLAGS -ansi -Wall -Wno-implicit-function-declaration -g"
fi


dnl Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([stdio.h stdlib.h string.h])

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

dnl Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_CHECK_FUNCS([memmove])

AC_CHECK_LIB(z, inflate)
dnl AC_CHECK_LIB(cutest, CuTestInit)


AC_MSG_CHECKING(whether to build tests)
AC_ARG_ENABLE(tests,
[  --enable-tests    build tests. default=no],
[ case "${enableval}" in
  no)
    AC_MSG_RESULT(no)
    TESTDIR=""
    ;;
  *)
    AC_MSG_RESULT(yes)
    TESTDIR="test"

    ;;
  esac ],
  AC_MSG_RESULT(no)
  TESTDIR=""
)

GUTHTHILA_LIBS=""

AC_MSG_CHECKING(whether to build guththila xml parser library)
AC_ARG_ENABLE(guththila, [  --enable-guththila
                          build Guththila XML parser library wrapper (default=yes)],
[ case "${enableval}" in
  no)
    AC_MSG_RESULT(no)
    ;;
  *)
    AC_MSG_RESULT(yes)
    CFLAGS="$CFLAGS -DAXIS2_GUTHTHILA_ENABLED"
    CPPFLAGS="$CPPFLAGS -DAXIS2_GUTHTHILA_ENABLED"
    WRAPPER_DIR="guththila"

    ;;
  esac ],
  AC_MSG_RESULT(yes)
  WRAPPER_DIR="guththila"
  CFLAGS="$CFLAGS -DAXIS2_GUTHTHILA_ENABLED"
  CPPFLAGS="$CPPFLAGS -DAXIS2_GUTHTHILA_ENABLED"
  AC_CONFIG_SUBDIRS(guththila)
  GUTHTHILA_LIBS="/guththila/src/"
  GUTHTHILA_DIR="guththila"
)


AC_MSG_CHECKING(whether to build libxml2 xml parser library)
AC_ARG_ENABLE(libxml2, [  --enable-libxml2    
                          build Libxml2 XML parser library wrapper (default=no)],
[ case "${enableval}" in
  no)
    AC_MSG_RESULT(no)
    WRAPPER_DIR=""
    ;;
  *)
    AC_MSG_RESULT(yes)
    WRAPPER_DIR="libxml2"
    PKG_CHECK_MODULES(LIBXML2, libxml-2.0)
    CFLAGS="$CFLAGS -DAXIS2_LIBXML2_ENABLED"
    CPPFLAGS="$CPPFLAGS $PARSER_CFLAGS -DAXIS2_LIBXML2_ENABLED"
    LDFLAGS="$LDFLAGS $PARSER_LIBS"
    ;;
  esac ],
  AC_MSG_RESULT(no)
)


UTILINC=$axis2_utilinc

case $host in
  *mingw* | *msys*)
    VERSION_INFO="-avoid-version"
    CFLAGS="$CFLAGS -DWIN32 -D_WINDOWS -D_MBCS -DAXIS2_DECLARE_EXPORT -D_CRT_SECURE_NO_DEPRECATE -D_CRT_SECURE_NO_WARNINGS"
    LDFLAGS="$LDFLAGS -no-undefined"
  ;;
esac

AC_SUBST(UTILINC)
AC_SUBST(TESTDIR)
AC_SUBST(WRAPPER_DIR)

CFLAGS="$CFLAGS"

AC_CONFIG_FILES([Makefile \
    src/Makefile \
    ])
    
AC_OUTPUT
