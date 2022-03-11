# GNU makefile

PREFIX = /usr/

all: info src/hello

info:
	@echo "CC       = $(CC)"
	@echo "CPPFLAGS = $(CPPFLAGS)"
	@echo "CFLAGS   = $(CFLAGS)"
	@echo "LDCFLAGS = $(LDCFLAGS)"
	@echo "LDFLAGS  = $(LDFLAGS)"
	@echo "DESTDIR  = $(DESTDIR)"
	@echo "PREFIX   = $(PREFIX)"

src/hello: src/hello.c
	$(CC) $(CPPFLAGS) $(CFLAGS) $(LDCFLAGS) -o $@ $^

install: src/hello
	install -D src/hello \
               $(DESTDIR)$(PREFIX)/bin/hello
	install -m 644 -D man/hello.1 \
               $(DESTDIR)$(PREFIX)/share/man/man1/hello.1
	install -m 644 -D share/hello.png \
               $(DESTDIR)$(PREFIX)/share/pixmaps/hello.png
	install -m 644 -D share/hello.desktop \
               $(DESTDIR)$(PREFIX)/share/applications/hello.desktop

uninstall:
	-rm -f $(DESTDIR)$(PREFIX)/bin/hello
	-rm -f $(DESTDIR)$(PREFIX)/share/man/man1/hello.1
	-rm -f $(DESTDIR)$(PREFIX)/share/pixmaps/hello.png
	-rm -f $(DESTDIR)$(PREFIX)/share/applications/hello.desktop

clean:
	-rm -f src/hello

distclean: clean

BANSENAME=$(shell basename $(realpath .))
backup: clean
	tar czf ../hello-1.0.tar.gz ../$(BANSENAME) 2> /dev/null

debclean:
	@-rm -rf debian

dclean:
	@debuild -- clean

dist: debmake debuild

debmake:
	debmake -p hello -u 1.0 -r 0 -x 1

debuild:
	debuild

.PHONY: all clean distclean install uninstall dist dclean
