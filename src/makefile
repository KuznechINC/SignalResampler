CC = g++
CFLAGS = -fPIC -O3
LDFLAGS = -L/usr/lib -lboost_program_options

all: libresample.a

libresample.a: resample.o
	ar rcs $@ $^

resample.o: resample.cpp resample.h upfirdn.h
	${CC} ${CFLAGS} ${LDFLAGS} -c -o $@ $<

.PHONY: clean

clean:
	rm -f *.o *.a
