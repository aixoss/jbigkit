# Unix makefile for the JBIG-KIT library
# $Id: Makefile 1285 2008-08-18 13:36:45Z mgk25 $

# Select an ANSI/ISO C compiler here, GNU gcc is recommended
CC = /usr/vac/bin/xlc_r

# Options for the compiler: A high optimization level is suggested
CFLAGS = -O -I/opt/freeware/include

all: libjbig.a tstcodec tstcodec85

tstcodec: tstcodec.o jbig.o jbig_ar.o
	$(CC) $(CFLAGS) -o tstcodec $+

tstcodec85: tstcodec85.o jbig85.o jbig_ar.o
	$(CC) $(CFLAGS) -o tstcodec85 $+

libjbig.a: jbig.o jbig_ar.o
	rm -f libjbig.a
	ar rc libjbig.a jbig.o jbig_ar.o
	-ranlib libjbig.a

libjbig85.a: jbig85.o jbig_ar.o
	rm -f libjbig85.a
	ar rc libjbig85.a jbig85.o jbig_ar.o
	-ranlib libjbig85.a

jbig.o: jbig.c jbig.h jbig_ar.h
jbig85.o: jbig85.c jbig85.h jbig_ar.h
jbig_ar.o: jbig_ar.c jbig_ar.h
tstcodec.o: tstcodec.c jbig.h
tstcodec85.o: tstcodec85.c jbig85.h

jbig.pot: jbig.c
	xgettext -o$@ -k_ \
	  --copyright-holder='Markus Kuhn' \
	  --msgid-bugs-address='http://www.cl.cam.ac.uk/~mgk25/jbigkit/' $+

test: tstcodec tstcodec85
	./tstcodec
	./tstcodec85

t82test.pbm: tstcodec
	./tstcodec $@

clean:
	rm -f *.{o,gcda,gcno,gcov} *~ core gmon.out dbg_d\=??.pbm t82test.pbm
	rm -f tstcodec tstcodec85
