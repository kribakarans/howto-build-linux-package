# GNU makefile

PREFIX = /usr

all: info src/hello-gtk

info:
	@echo "CC       = $(CC)"
	@echo "CPPFLAGS = $(CPPFLAGS)"
	@echo "CFLAGS   = $(CFLAGS)"
	@echo "LDCFLAGS = $(LDCFLAGS)"
	@echo "LDFLAGS  = $(LDFLAGS)"
	@echo "DESTDIR  = $(DESTDIR)"
	@echo "PREFIX   = $(PREFIX)"

src/hello-gtk: src/hello.c
	$(CC) $(CPPFLAGS) $(CFLAGS) $(LDCFLAGS) -o $@ $^

install: src/hello-gtk
	install -D src/hello-gtk \
               $(DESTDIR)$(PREFIX)/bin/hello-gtk
	install -m 644 -D man/hello-gtk.1 \
               $(DESTDIR)$(PREFIX)/share/man/man1/hello-gtk.1
	install -m 644 -D share/hellogtk.png \
               $(DESTDIR)$(PREFIX)/share/pixmaps/hellogtk.png
	install -m 644 -D share/hellogtk.desktop \
               $(DESTDIR)$(PREFIX)/share/applications/hellogtk.desktop

uninstall:
	-rm -f $(DESTDIR)$(PREFIX)/bin/hello-gtk
	-rm -f $(DESTDIR)$(PREFIX)/share/man/man1/hello-gtk.1
	-rm -f $(DESTDIR)$(PREFIX)/share/pixmaps/hellogtk.png
	-rm -f $(DESTDIR)$(PREFIX)/share/applications/hellogtk.desktop

clean:
	-rm -f src/hello-gtk

distclean: clean

BANSENAME=$(shell basename $(realpath .))
backup: clean
	tar czf ../hello-gtk-1.0.tar.gz ../$(BANSENAME) 2> /dev/null

debclean:
	@-rm -rf debian

dclean:
	@debuild -- clean

dist: debmake debuild

debmake:
	debmake -p hello-gtk -u 1.0 -r 0 -x 1

debuild:
	debuild

.PHONY: all clean distclean install uninstall dist dclean
