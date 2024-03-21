TOP=../..

include $(TOP)/configure/CONFIG

# LIBRARY
LIBRARY_IOC += ecAsyn

USR_INCLUDES += -I$(XML2_HEADERS)
USR_SYS_LIBS += xml2
ifdef EPICS_HOST_ARCH
USR_LDFLAGS += -L$(ARCH_LD_LIBRARY_PATH) -Wl,-rpath=$(ARCH_LD_LIBRARY_PATH)
USR_SYS_LIBS += lzma z
endif

ecAsyn_SRCS += ecAsyn.cpp gadc.cpp
ecAsyn_LIBS += asyn scannerlib rtutils 
ecAsyn_INCLUDES += -I$(ETHERLAB)/include
gadc_INCLUDES += -I$(ETHERLAB)/include

INC += gadc.h

DBD += ecAsyn.dbd

# IOC application
PROD_IOC = ethercatApp
ethercatApp_DBD += base.dbd ecAsyn.dbd
#ethercatApp_DBD += ecAsynIncluded.dbd

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
ethercatApp_LIBS += $(EPICS_BASE_IOC_LIBS)

include $(TOP)/configure/RULES
#----------------------------------------
#  ADD RULES AFTER THIS LINE
