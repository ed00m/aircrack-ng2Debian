AC_ROOT         = ../..
SRC_DIR		= $(AC_ROOT)/src
include $(AC_ROOT)/common.mak
CFLAGS          += -I$(SRC_DIR) -I$(SRC_DIR)/include

ifeq ($(gcrypt), true)
        LIBSSL          =  -lgcrypt $(LDFLAGS)
        CFLAGS          += -DUSE_GCRYPT
else
        LIBSSL          = -lssl -lcrypto $(LDFLAGS)
endif

all:	check

SRC_CRYPTO	  = $(AC_ROOT)/src/crypto.c $(AC_ROOT)/src/sha1-git.c

TESTFILES        = test-encrypt-wep$(EXE) test-calc-pmk$(EXE) test-calc-mic$(EXE) test-calc-ptk$(EXE) test-decrypt-ccmp$(EXE) test-calc-4pmk$(EXE)


OBJS_TEST_EWEP  = test-encrypt-wep.c $(SRC_CRYPTO)
OBJS_TEST_CPMK  = test-calc-pmk.c $(SRC_CRYPTO)
OBJS_TEST_4PMK  = test-calc-4pmk.c $(SRC_CRYPTO)
OBJS_TEST_CMIC  = test-calc-mic.c $(SRC_CRYPTO)
OBJS_TEST_CPTK  = test-calc-ptk.c $(SRC_CRYPTO)
OBJS_TEST_DCMP  = test-decrypt-ccmp.c $(SRC_CRYPTO)

test-encrypt-wep$(EXE): $(OBJS_TEST_EWEP)
	$(CC) $(CFLAGS) $(OBJS_TEST_EWEP) -o $(@) $(LIBSSL)

test-calc-pmk$(EXE): $(OBJS_TEST_CPMK)
	$(CC) $(CFLAGS) $(OBJS_TEST_CPMK) -o $(@) $(LIBSSL)

test-calc-4pmk$(EXE): $(OBJS_TEST_4PMK)
	$(CC) $(CFLAGS) $(OBJS_TEST_4PMK) $(AC_ROOT)/src/sha1-sse2.S -o $(@) $(LIBSSL)

test-calc-mic$(EXE): $(OBJS_TEST_CMIC)
	$(CC) $(CFLAGS) $(OBJS_TEST_CMIC) -o $(@) $(LIBSSL)

test-calc-ptk$(EXE): $(OBJS_TEST_CPTK)
	$(CC) $(CFLAGS) $(OBJS_TEST_CPTK) -o $(@) $(LIBSSL)

test-decrypt-ccmp$(EXE): $(OBJS_TEST_DCMP)
	$(CC) $(CFLAGS) $(OBJS_TEST_DCMP) -o $(@) $(LIBSSL)


default: check

sslcheck: check


check: $(TESTFILES)
	$(foreach TEST,$(TESTFILES), \
		./$(TEST) || exit 1; \
	)

valgrind: $(TESTFILES)
	$(foreach TEST,$(TESTFILES), \
		echo "Testing $$test for memory leaks with valgrind ..." ; \
		valgrind -q --error-exitcode=1 --leak-check=yes ./$(TEST) || exit 1; \
	)


clean:
	rm -f $(TESTFILES)
	rm -f vgcore*


