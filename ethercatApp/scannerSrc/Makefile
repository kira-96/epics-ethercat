TOP=../..

include $(TOP)/configure/CONFIG

# build a program

SHARED_LIBRARIES=NO
STATIC_BUILD=YES
#HOST_OPT=NO

# work-around for ioc builder's benefit:
# the symbol below moved from $(TOP)/configure/RELEASE
# POSIX_CPPFLAGS = -D_POSIX_C_SOURCE=199506L -D_POSIX_THREADS -D_XOPEN_SOURCE=600

USR_INCLUDES += -I$(ETHERLAB)/include

USR_LDFLAGS += -L$(ETHERLAB)/lib/.libs -Wl,-rpath=$(ETHERLAB)/lib/.libs
USR_INCLUDES += -I$(XML2_HEADERS)
USR_SYS_LIBS += ethercat xml2
ifdef EPICS_HOST_ARCH
USR_LDFLAGS += -L$(ARCH_LD_LIBRARY_PATH) -Wl,-rpath=$(ARCH_LD_LIBRARY_PATH)
USR_SYS_LIBS += lzma z
endif

INC += classes.h parser.h classes.h unpack.h messages.h version.h

LIBRARY += scannerlib
scannerlib_SRCS += parser.c classes.c unpack.c

PROD += scanner
# need private header file to disable errors being sent to stderr
scanner_INCLUDES += -I$(ETHERLAB)/lib
scanner_SRCS += scanner.c simulation.c
scanner_LIBS += rtutils scannerlib Com

PROD += serialtool
# need private header files for the serial number write IOCTL
serialtool_INCLUDES += -I$(ETHERLAB)/master
serialtool_SRCS += serialtool.c slave-types.c slave-list-path.c

PROD += get-slave-revisions 
get-slave-revisions_INCLUDES += -I$(ETHERLAB)/master
get-slave-revisions_SRCS += get-slave-revisions.c

ifeq ($(TEST_SLAVE_TYPES), YES)
    PROD += test
    test_SRCS += test-slave-types.c slave-types.c
endif

PROD += slaveinfo
slaveinfo_SRCS += slaveinfo.c slave-types.c slave-list-path.c

PROD += parsertest
parsertest_SRCS += parsertest.c
parsertest_LIBS += scannerlib Com

include $(TOP)/configure/RULES
