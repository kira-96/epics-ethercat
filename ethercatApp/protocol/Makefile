TOP = ../..
include $(TOP)/configure/CONFIG
#----------------------------------------
#  ADD MACRO DEFINITIONS AFTER THIS LINE

ifdef EPICS_HOST_ARCH
# Copy all protocol files into data directory
DATA += $(patsubst ../%, %, $(wildcard ../*.proto))
endif

include $(TOP)/configure/RULES

