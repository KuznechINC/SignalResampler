CC = g++
CFLAGS = -fPIC -O3
LDFLAGS = -L/usr/lib -lboost_program_options

all: example libresample.a

example: example.cpp resample.cpp resample.h upfirdn.h
	${CC} example.cpp resample.cpp  ${CFLAGS} ${LDFLAGS} -o example

libresample.a: resample.o
	ar rcs $@ $^

resample.o: resample.cpp resample.h upfirdn.h
	${CC} ${CFLAGS} ${LDFLAGS} -c -o $@ $<

.PHONY: clean

clean:
	rm -f *.o *.a example
