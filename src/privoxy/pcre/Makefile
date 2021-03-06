# Generated automatically from Makefile.in by configure.

# Makefile.in for PCRE (Perl-Compatible Regular Expression) library.

#---------------------------------------------------------------------------#
# To build mingw32 DLL uncomment the next two lines. This addition for      #
# mingw32 was contributed by <Paul.Sokolovsky@technologist.com>. I (Philip  #
# Hazel) don't know anything about it! There are some additional targets at #
# the bottom of this Makefile.                                              #
#---------------------------------------------------------------------------#
#
# include dll.mk
# DLL_LDFLAGS=-s


#---------------------------------------------------------------------------#
# The next few lines are modified by "configure" to insert data that it is  #
# given in its arguments, or which it finds out for itself.                 #
#---------------------------------------------------------------------------#

# BINDIR is the directory in which the pcregrep command is installed.
# INCDIR is the directory in which the public header file pcre.h is installed.
# LIBDIR is the directory in which the libraries are installed.
# MANDIR is the directory in which the man pages are installed.
# The pcretest program, as it is a test program, does not get installed
# anywhere.

prefix = /usr/local/opt/pcre
exec_prefix = ${prefix}

BINDIR = ${exec_prefix}/bin
LIBDIR = ${exec_prefix}/lib
INCDIR = ${prefix}/include
MANDIR = ${prefix}/man

CC = gcc
CFLAGS = -g -O2
RANLIB = ranlib
UTF8   = 

# LIBTOOL defaults to "./libtool", which enables the building of shared
# libraries. If "configure" is called with --disable-shared-libraries, LIBTOOL
# is set to "", which stops shared libraries from being built, and LIBSUFFIX
# is set to "a" instead of "la", which causes the shared libraries not to be
# installed.

LIBTOOL = ./libtool
LIBSUFFIX = la

# These are the version numbers for the shared libraries

PCRELIBVERSION = 0:1:0
PCREPOSIXLIBVERSION = 0:0:0


#---------------------------------------------------------------------------#
# A copy of install-sh is in this distribution and is used by default.      #
#---------------------------------------------------------------------------#

INSTALL = ./install-sh -c
INSTALL_DATA = ${INSTALL} -m 644


#---------------------------------------------------------------------------#
# For almost all systems, the command to create a library is "ar cq", but   #
# there is at least one where it is different, so this command must be      #
# configurable. However, I haven't got round to learning how to make        #
# "configure" find this out for itself. It is necessary to use a command    #
# such as "make AR='ar -rc'" if you need to vary this. The setting of AR is #
# *not* passed over to ./ltconfig, because it does its own setting up.      #
#---------------------------------------------------------------------------#

AR = ar cq


##############################################################################


OBJ = maketables.o get.o study.o pcre.o
LOBJ = maketables.lo get.lo study.lo pcre.lo

all:            libtool libpcre.$(LIBSUFFIX) libpcreposix.$(LIBSUFFIX) pcretest pcregrep

libtool:        config.guess config.sub ltconfig ltmain.sh
		@if test "$(LIBTOOL)" = "./libtool"; then \
		  echo '--- Building libtool ---'; \
		  CC=$(CC) CFLAGS='$(CFLAGS)' RANLIB='$(RANLIB)' ./ltconfig ./ltmain.sh; \
		  echo '--- Built libtool ---'; fi

pcregrep:       libpcre.$(LIBSUFFIX) pcregrep.o
		  @echo ' '
		  @echo '--- Building pcregrep utility'
		  @echo ' '
		$(LIBTOOL) $(CC) $(CFLAGS) -o pcregrep pcregrep.o libpcre.$(LIBSUFFIX)

pcretest:       libpcre.$(LIBSUFFIX) libpcreposix.$(LIBSUFFIX) pcretest.o
		  @echo ' '
		  @echo '--- Building pcretest testing program'
		  @echo ' '
		$(LIBTOOL) $(PURIFY) $(CC) $(CFLAGS) -o pcretest pcretest.o \
		  libpcre.$(LIBSUFFIX) libpcreposix.$(LIBSUFFIX)

libpcre.a:      $(OBJ)
		@echo ' '
		@echo '--- Building static library: libpcre'
		@echo ' '
		-rm -f libpcre.a
		$(AR) libpcre.a $(OBJ)
		$(RANLIB) libpcre.a

libpcre.la:     $(OBJ)
		@echo ' '
		@echo '--- Building shared library: libpcre'
		@echo ' '
		-rm -f libpcre.la
		./libtool $(CC) -version-info '$(PCRELIBVERSION)' -o libpcre.la -rpath $(LIBDIR) $(LOBJ)

libpcreposix.a: pcreposix.o
		@echo ' '
		@echo '--- Building static library: libpcreposix'
		@echo ' '
		-rm -f libpcreposix.a
		$(AR) libpcreposix.a pcreposix.o
		$(RANLIB) libpcreposix.a

libpcreposix.la: pcreposix.o
		@echo ' '
		@echo '--- Building shared library: libpcreposix'
		@echo ' '
		-rm -f libpcreposix.la
		./libtool $(CC) -version-info '$(PCREPOSIXLIBVERSION)' -o libpcreposix.la -rpath $(LIBDIR) pcreposix.lo

pcre.o:         chartables.c pcre.c pcre.h internal.h config.h Makefile
		$(LIBTOOL) $(CC) -c $(CFLAGS) $(UTF8) pcre.c

pcreposix.o:    pcreposix.c pcreposix.h internal.h pcre.h config.h Makefile
		$(LIBTOOL) $(CC) -c $(CFLAGS) pcreposix.c

maketables.o:   maketables.c pcre.h internal.h config.h Makefile
		$(LIBTOOL) $(CC) -c $(CFLAGS) maketables.c

get.o:          get.c pcre.h internal.h config.h Makefile
		$(LIBTOOL) $(CC) -c $(CFLAGS) get.c

study.o:        study.c pcre.h internal.h config.h Makefile
		$(LIBTOOL) $(CC) -c $(CFLAGS) $(UTF8) study.c

pcretest.o:     pcretest.c pcre.h config.h Makefile
		$(CC) -c $(CFLAGS) $(UTF8) pcretest.c

pcregrep.o:     pcregrep.c pcre.h Makefile config.h
		$(CC) -c $(CFLAGS) $(UTF8) pcregrep.c

# An auxiliary program makes the default character table source

chartables.c:   dftables
		./dftables >chartables.c

dftables:       dftables.c maketables.c pcre.h internal.h config.h Makefile
		$(CC) -o dftables $(CFLAGS) dftables.c

install:        all
		$(LIBTOOL) $(INSTALL_DATA) libpcre.$(LIBSUFFIX) $(DESTDIR)/$(LIBDIR)/libpcre.$(LIBSUFFIX)
		$(LIBTOOL) $(INSTALL_DATA) libpcreposix.$(LIBSUFFIX) $(DESTDIR)/$(LIBDIR)/libpcreposix.$(LIBSUFFIX)
		$(INSTALL_DATA) pcre.h $(DESTDIR)/$(INCDIR)/pcre.h
		$(INSTALL_DATA) pcreposix.h $(DESTDIR)/$(INCDIR)/pcreposix.h
		$(INSTALL_DATA) doc/pcre.3 $(DESTDIR)/$(MANDIR)/man3/pcre.3
		$(INSTALL_DATA) doc/pcreposix.3 $(DESTDIR)/$(MANDIR)/man3/pcreposix.3
		$(INSTALL_DATA) doc/pcregrep.1 $(DESTDIR)/$(MANDIR)/man1/pcregrep.1
		@if test "$(LIBTOOL)" = "./libtool"; then \
		  echo ' '; \
		  echo '--- Rebuilding pcregrep to use installed shared library ---'; \
		  echo $(CC) $(CFLAGS) -o pcregrep pcregrep.o -L$(DESTDIR)/$(LIBDIR) -lpcre; \
		  $(CC) $(CFLAGS) -o pcregrep pcregrep.o -L$(DESTDIR)/$(LIBDIR) -lpcre; \
		  echo '--- Rebuilding pcretest to use installed shared library ---'; \
		  echo $(CC) $(CFLAGS) -o pcretest pcretest.o -L$(DESTDIR)/$(LIBDIR) -lpcre -lpcreposix; \
		  $(CC) $(CFLAGS) -o pcretest pcretest.o -L$(DESTDIR)/$(LIBDIR) -lpcre -lpcreposix; \
		fi
		$(INSTALL)	pcregrep $(DESTDIR)/$(BINDIR)/pcregrep
		$(INSTALL)	pcre-config $(DESTDIR)/$(BINDIR)/pcre-config

# We deliberately omit dftables and chartables.c from 'make clean'; once made
# chartables.c shouldn't change, and if people have edited the tables by hand,
# you don't want to throw them away.

clean:;         -rm -rf *.o *.lo *.a *.la .libs pcretest pcregrep testtry

# But "make distclean" should get back to a virgin distribution

distclean:      clean
		-rm -f chartables.c libtool pcre-config pcre.h \
		Makefile config.h config.status config.log config.cache

check:          runtest

test:           runtest

runtest:        all
		./RunTest

######## MINGW32 ############### MINGW32 ############### MINGW32 #############

# This addition for mingw32 was contributed by  Paul Sokolovsky
# <Paul.Sokolovsky@technologist.com>. I (PH) don't know anything about it!

dll:            _dll libpcre.dll.a pcregrep_d pcretest_d

_dll:
		$(MAKE) CFLAGS=-DSTATIC pcre.dll

pcre.dll:       $(OBJ) pcreposix.o pcre.def
libpcre.dll.a:  pcre.def

pcregrep_d:     libpcre.dll.a pcregrep.o
		$(CC) $(CFLAGS) -L. -o pcregrep pcregrep.o -lpcre.dll

pcretest_d:     libpcre.dll.a pcretest.o
		$(PURIFY) $(CC) $(CFLAGS) -L. -o pcretest pcretest.o -lpcre.dll

# End
