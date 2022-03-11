# GNU makefile

PREFIX = /usr

all: info src/hello-atom-gtk

info:
	@echo "CC       = $(CC)"
	@echo "CPPFLAGS = $(CPPFLAGS)"
	@echo "CFLAGS   = $(CFLAGS)"
	@echo "LDCFLAGS = $(LDCFLAGS)"
	@echo "LDFLAGS  = $(LDFLAGS)"
	@echo "DESTDIR  = $(DESTDIR)"
	@echo "PREFIX   = $(PREFIX)"

src/hello-atom-gtk: src/hello.c
	$(CC) $(CPPFLAGS) $(CFLAGS) $(LDCFLAGS) -o $@ $^

install: src/hello-atom-gtk
	install -D src/hello-atom-gtk \
               $(DESTDIR)$(PREFIX)/bin/hello-atom-gtk
	install -m 644 -D man/hello-atom-gtk.1 \
               $(DESTDIR)$(PREFIX)/share/man/man1/hello-atom-gtk.1
	install -m 644 -D share/helloatomgtk.png \
               $(DESTDIR)$(PREFIX)/share/pixmaps/helloatomgtk.png
	install -m 644 -D share/helloatomgtk.desktop \
               $(DESTDIR)$(PREFIX)/share/applications/helloatomgtk.desktop

uninstall:
	-rm -f $(DESTDIR)$(PREFIX)/bin/hello-atom-gtk
	-rm -f $(DESTDIR)$(PREFIX)/share/man/man1/hello-atom-gtk.1
	-rm -f $(DESTDIR)$(PREFIX)/share/pixmaps/helloatomgtk.png
	-rm -f $(DESTDIR)$(PREFIX)/share/applications/helloatomgtk.desktop

clean:
	-rm -f src/hello-atom-gtk

distclean: clean

BANSENAME=$(shell basename $(realpath .))
backup: clean
	tar czf ../hello-atom-gtk-1.0.tar.gz ../$(BANSENAME) 2> /dev/null

debclean:
	@-rm -rf debian

dclean:
	@debuild -- clean

dist: debmake debuild

debmake:
	debmake -p hello-atom-gtk -u 1.0 -r 0 -x 1

debuild:
	debuild

.PHONY: all clean distclean install uninstall dist dclean debmake debuild
