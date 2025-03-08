RE2_LIB=/opt/re2/lib
RE2_INC=/opt/re2/include

PCRE_LIB=/opt/pcre/lib
PCRE_INC=/opt/pcre/include

CFLAGS= -c -Wall -Werror -O3 -g
CXXFLAGS= -c -Wall -Werror -O3 -g
REGEX1=
FILE1=abc.txt

.PHONY: all test

all: sregex pcre re2

sregex: sregex.o ../libsregex.a
	$(CC) -o $@ -Wl,-rpath,.. -L.. $< -lsregex -lrt

re2: re2.o
	$(CXX) -o $@ -Wl,-rpath,$(RE2_LIB) -L$(RE2_LIB) $< -lre2 -lrt

pcre: pcre.o
	$(CC) -o $@ -Wl,-rpath,$(PCRE_LIB) -L$(PCRE_LIB) $< -lpcre -lrt

%.o: %.c
	$(CC) $(CFLAGS) -I../src -I$(PCRE_INC) $<

%.o: %.cc
	$(CXX) $(CXXFLAGS) -I$(RE2_INC) $<

test: all $(FILE1)
	./bench '(?:a|b)aa(?:aa|bb)cc(?:a|b)' $(FILE1)

clean:
	rm -rf *.o sregex

$(FILE1):
	perl gen-data.pl

