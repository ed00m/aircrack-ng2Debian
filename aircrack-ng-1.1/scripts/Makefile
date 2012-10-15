AC_ROOT		= ..
include		$(AC_ROOT)/common.mak

SCRIPTS         = airdriver-ng airodump-ng-oui-update

default: all

all:
	@echo Nothing to do
	
install:
	install -m 755 $(SCRIPTS) $(DESTDIR)$(sbindir)
ifeq ($(OSNAME), Linux)
	install -m 755 airmon-ng $(DESTDIR)$(sbindir)/airmon-ng
endif
ifeq ($(filter FreeBSD GNU-kFreeBSD, $(OSNAME)),)
else
	install -m 755 airmon-ng.freebsd $(DESTDIR)$(sbindir)/airmon-ng
endif

uninstall:
	-rm -f $(DESTDIR)$(sbindir)/airmon-ng
	-rm -f $(DESTDIR)$(sbindir)/airdriver-ng
	-rm -f $(DESTDIR)$(sbindir)/airodump-ng-oui-update

clean:
	@echo Nothing to do
