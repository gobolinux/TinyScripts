CC = gcc
CFLAGS = -Wall
LDFLAGS =

TARGETS = List RemoveBroken SymlinkProgram
SVN_REPO  = http://svn.gobolinux.org/tools/trunk/Scripts/src
SVN_FILES = $(SVN_REPO)/LinkOrExpandAll.c $(SVN_REPO)/List.c $(SVN_REPO)/List.h


all: SymlinkProgram.o LinkOrExpandAll.o List.o RemoveBroken.o
	$(CC) $(LDFLAGS) SymlinkProgram.o LinkOrExpandAll.o -o SymlinkProgram
	$(CC) $(LDFLAGS) List.o -o List
	$(CC) $(LDFLAGS) RemoveBroken.o -o RemoveBroken
	@mv $(TARGETS) ../bin && chmod +x ../bin/*
	@ln -sf List ../bin/l

clean:
	@rm -Rf *.o *~
	@cd ../bin; rm -f $(TARGETS) l

distclean: clean
	@rm LinkOrExpandAll.c List.c List.h

LinkOrExpandAll.o: LinkOrExpandAll.c
	@GrepReplace "int main(" "int link_or_expand_all_main(" LinkOrExpandAll.c
	$(CC) $(CFLAGS) -c LinkOrExpandAll.c -std=c99

List.c LinkOrExpandAll.c:
	@for i in $(SVN_FILES); do svn export $$i; done
	@rm -Rf tools/

%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $<
