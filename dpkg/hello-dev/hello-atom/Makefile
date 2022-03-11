# GNU makefile

PREFIX = /usr

all: info src/hello-atom

info:
	@echo "CC       = $(CC)"
	@echo "CPPFLAGS = $(CPPFLAGS)"
	@echo "CFLAGS   = $(CFLAGS)"
	@echo "LDCFLAGS = $(LDCFLAGS)"
	@echo "LDFLAGS  = $(LDFLAGS)"
	@echo "DESTDIR  = $(DESTDIR)"
	@echo "PREFIX   = $(PREFIX)"

src/hello-atom: src/hello.c
	$(CC) $(CPPFLAGS) $(CFLAGS) $(LDCFLAGS) -o $@ $^

install: src/hello-atom
	install -D src/hello-atom \
               $(DESTDIR)$(PREFIX)/bin/hello-atom
	install -m 644 -D man/hello-atom.1 \
               $(DESTDIR)$(PREFIX)/share/man/man1/hello-atom.1
	install -m 644 -D share/helloatom.png \
               $(DESTDIR)$(PREFIX)/share/pixmaps/helloatom.png
	install -m 644 -D share/helloatom.desktop \
               $(DESTDIR)$(PREFIX)/share/applications/helloatom.desktop

uninstall:
	-rm -f $(DESTDIR)$(PREFIX)/bin/hello-atom
	-rm -f $(DESTDIR)$(PREFIX)/share/man/man1/hello-atom.1
	-rm -f $(DESTDIR)$(PREFIX)/share/pixmaps/helloatom.png
	-rm -f $(DESTDIR)$(PREFIX)/share/applications/helloatom.desktop

clean:
	-rm -f src/hello-atom

distclean: clean

BANSENAME=$(shell basename $(realpath .))
backup: clean
	tar czf ../hello-atom-1.0.tar.gz ../$(BANSENAME) 2> /dev/null

debclean:
	@-rm -rf debian

dclean:
	@debuild -- clean

dist: debmake debuild

debmake:
	debmake -p hello-atom -u 1.0 -r 0 -x 1

debuild:
	debuild

.PHONY: all clean distclean install uninstall dist dclean debmake debuild
