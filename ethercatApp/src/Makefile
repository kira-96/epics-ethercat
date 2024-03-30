TOP=../..

include $(TOP)/configure/CONFIG

# LIBRARY
LIBRARY_IOC += ecAsyn

USR_SYS_LIBS += xml2
ifdef EPICS_HOST_ARCH
USR_LDFLAGS += -L$(ARCH_LD_LIBRARY_PATH) -Wl,-rpath=$(ARCH_LD_LIBRARY_PATH)
USR_SYS_LIBS += lzma z
endif

ecAsyn_SRCS += ecAsyn.cpp gadc.cpp
ecAsyn_LIBS += asyn scannerlib rtutils 
USR_INCLUDES += -I$(XML2_HEADERS)
ecAsyn_INCLUDES += -I$(ETHERLAB)/include
gadc_INCLUDES += -I$(ETHERLAB)/include

INC += gadc.h

DBD += ecAsyn.dbd

# IOC application
PROD_IOC = ethercatApp
ethercatApp_DBD += base.dbd ecAsyn.dbd

ifdef MCOREUTILS
ethercatApp_DBD += mcoreutils.dbd
endif

# iocStats
ifdef IOCADMIN
ethercatApp_DBD += devIocStats.dbd
ethercatApp_DBD += iocAdmin.dbd
endif

DBD += ethercatApp.dbd

# <name>_registerRecordDeviceDriver.cpp will be created from <name>.dbd
ethercatApp_SRCS += ethercatApp_registerRecordDeviceDriver.cpp

# These two lines are needed for non-vxWorks builds, such as Linux
ethercatApp_SRCS_DEFAULT += ethercatMain.cpp
ethercatApp_SRCS_vxWorks += -nil-

# Add locally compiled object code
# ethercatApp_SRCS +=

# The following adds object code from base/src/vxWorks
ethercatApp_OBJS_vxWorks += $(EPICS_BASE_BIN)/vxComLibrary

#ethercatApp_LDFLAGS += -L$(ECASYN)/lib/$(EPICS_HOST_ARCH) -Wl,-rpath=$(ECASYN)/lib/$(EPICS_HOST_ARCH)
ethercatApp_LIBS += ecAsyn asyn
ifdef MCOREUTILS
ethercatApp_LIBS += mcoreutils
endif
ifdef IOCADMIN
ethercatApp_LIBS += devIocStats
endif
ethercatApp_LIBS += $(EPICS_BASE_IOC_LIBS)

# iocStats
ifdef IOCADMIN
DB_INSTALLS += $(IOCADMIN)/db/iocAdminVxWorks.db
DB_INSTALLS += $(IOCADMIN)/db/iocAdminRTEMS.db
DB_INSTALLS += $(IOCADMIN)/db/iocAdminSoft.db
DB_INSTALLS += $(IOCADMIN)/db/access.db
DB_INSTALLS += $(IOCADMIN)/db/iocAdminScanMon.db
IOCRELEASE_DB += iocRelease.db
endif

include $(TOP)/configure/RULES
#----------------------------------------
#  ADD RULES AFTER THIS LINE
