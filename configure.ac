# Copyright (c) 2008, 2009 The Board of Trustees of The Leland Stanford
# Junior University
#
# We are making the OpenFlow specification and associated documentation
# (Software) available for public use and benefit with the expectation
# that others will use, modify and enhance the Software and contribute
# those enhancements back to the community. However, since we would
# like to make the Software available for broadest use, with as few
# restrictions as possible permission is hereby granted, free of
# charge, to any person obtaining a copy of this Software to deal in
# the Software under the copyrights without restriction, including
# without limitation the rights to use, copy, modify, merge, publish,
# distribute, sublicense, and/or sell copies of the Software, and to
# permit persons to whom the Software is furnished to do so, subject to
# the following conditions:
#
# The above copyright notice and this permission notice shall be
# included in all copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
# EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
# MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
# NONINFRINGEMENT.  IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS
# BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN
# ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
# CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
#
# The name and trademarks of copyright holder(s) may NOT be used in
# advertising or publicity pertaining to the Software or any
# derivatives without specific, written prior permission.

AC_PREREQ(2.60)
AC_INIT([openflow], [1.3.0], [openflow-discuss@openflowswitch.org])
NX_BUILDNR
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_HEADERS([config.h])
AM_INIT_AUTOMAKE

AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_CPP
AC_PROG_RANLIB
AC_PROG_MKDIR_P

AC_ARG_VAR([PERL], [path to Perl interpreter])
AC_PATH_PROG([PERL], perl, no)
if test "$PERL" = no; then
   AC_MSG_ERROR([Perl interpreter not found in $PATH or $PERL.])
fi

OFP_CHECK_LIBOPENFLOW
OFP_CHECK_IF_PACKET
OFP_CHECK_HWTABLES
OFP_CHECK_HWLIBS
AC_SYS_LARGEFILE

AC_CHECK_FUNCS([strsignal])

AC_ARG_VAR(KARCH, [Kernel Architecture String])
AC_SUBST(KARCH)

# Add skiptrill argument to configure script
AC_MSG_CHECKING(--enable-skiptrill argument)
AC_ARG_ENABLE(skiptrill,
    [  --enable-skiptrill         Enable skipping of TRILL protocol.],
    [enable_skiptrill=$enableval],
    [enable_skiptrill="no"])
AC_MSG_RESULT($enable_skiptrill)
if test "$enable_skiptrill" = "yes"; then
  AC_DEFINE(SKIP_TRILL, [], [Skip TRILL protocol])
fi

# BEBA options

AC_DEFINE(BEBA_USE_LIBPCAP,         1,   [BEBA pcap packet I/O acceleration])
AC_DEFINE(BEBA_USE_LIBPCAP_ZEROCOPY,1,   [BEBA zero-copy using pcap buffers])
AC_DEFINE(BEBA_WORK_BUDGET,         128, [BEBA work budget for batch I/O acceleration])
AC_DEFINE(BEBA_CTRL_PLANE_RELAX,    12,  [BEBA control-plane relax factor (power of 2)])
AC_DEFINE(BEBA_MATCH_POOL_SIZE,     16,  [BEBA size of pool for small TLV node])
AC_DEFINE(BEBA_MATCH_VALUE_SIZE,    16,  [BEBA size of TLV value])
AC_DEFINE(BEBA_HMAP_INIT_SIZE,      8,   [BEBA size of init hmap])


#OFP_CHECK_LINUX(l26, 2.6, KBLD26, KSRC26, L26_ENABLED)

OFP_CHECK_DPKG_BUILDPACKAGE

OFP_ENABLE_OPTION([-Wall])
OFP_ENABLE_OPTION([-Wextra])
OFP_ENABLE_OPTION([-Wno-free-nonheap-object])
OFP_ENABLE_OPTION([-Wno-sign-compare])
OFP_ENABLE_OPTION([-Wpointer-arith])
OFP_ENABLE_OPTION([-Wdeclaration-after-statement])
OFP_ENABLE_OPTION([-Wformat-security])
#OFP_ENABLE_OPTION([-Wswitch-enum])
OFP_ENABLE_OPTION([-Wunused-parameter])
OFP_ENABLE_OPTION([-Wstrict-aliasing])
OFP_ENABLE_OPTION([-Wbad-function-cast])
OFP_ENABLE_OPTION([-Wcast-align])
OFP_ENABLE_OPTION([-Wstrict-prototypes])
OFP_ENABLE_OPTION([-Wold-style-definition])
OFP_ENABLE_OPTION([-Wmissing-prototypes])
OFP_ENABLE_OPTION([-Wmissing-field-initializers])
OFP_ENABLE_OPTION([-Wno-override-init])

AC_CONFIG_FILES([Makefile 
])

#AC_CONFIG_FILES([Makefile
#datapath/Makefile
#datapath/linux-2.6/Kbuild
#datapath/linux-2.6/Makefile
#datapath/linux-2.6/Makefile.main
#])

AC_CHECK_LIB([pcap],[pcap_create])
AC_CHECK_HEADERS([linux/pf_q.h])

AC_OUTPUT
