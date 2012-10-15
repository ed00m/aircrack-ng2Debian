AC_ROOT		= ..
include		$(AC_ROOT)/common.mak

MP_FILES        = aircrack-ng.1 airdecap-ng.1 ivstools.1 kstats.1 makeivs-ng.1 \
                  packetforge-ng.1 airdecloak-ng.1

SMP_FILES       = airdriver-ng.8 aireplay-ng.8 airmon-ng.8 airodump-ng.8 \
                  airserv-ng.8 airtun-ng.8 airbase-ng.8 airodump-ng-oui-update.8

ifeq ($(SQLITE), true)
	MP_FILES += airolib-ng.1
else
	ifeq ($(sqlite), true)
		MP_FILES += airolib-ng.1
	else
		ifeq ($(SQLITE), TRUE)
			MP_FILES += airolib-ng.1
		else
			ifeq ($(sqlite), TRUE)
				MP_FILES += airolib-ng.1
			endif
		endif
	endif
endif


ifeq ($(UNSTABLE), true)
	MP_FILES        += buddy-ng.1
	SMP_FILES	+= easside-ng.8 tkiptun-ng.8 wesside-ng.8
else
	ifeq ($(unstable), true)
		MP_FILES        += buddy-ng.1
		SMP_FILES	+= easside-ng.8 tkiptun-ng.8 wesside-ng.8
	else
		ifeq ($(UNSTABLE), TRUE)
			MP_FILES        += buddy-ng.1
			SMP_FILES	+= easside-ng.8 tkiptun-ng.8 wesside-ng.8
		else
			ifeq ($(unstable), TRUE)
				MP_FILES        += buddy-ng.1
				SMP_FILES	+= easside-ng.8 tkiptun-ng.8 wesside-ng.8
			endif
		endif
	endif
endif


default: all

all:
	@echo Nothing to do
	
install: uninstall
	install -d $(DESTDIR)$(mandir)
	install -d $(DESTDIR)$(smandir)
	install -m 644 $(MP_FILES) $(DESTDIR)$(mandir)
	install -m 644 $(SMP_FILES) $(DESTDIR)$(smandir)

uninstall:
	@-$(foreach CUR_MP,$(MP_FILES), rm -f $(DESTDIR)$(mandir)/$(CUR_MP); echo rm -f $(DESTDIR)$(mandir)/$(CUR_MP); ) 
	@-$(foreach CUR_SMP,$(SMP_FILES), rm -f $(DESTDIR)$(smandir)/$(CUR_SMP); echo rm -f $(DESTDIR)$(smandir)/$(CUR_SMP); )
