################################################################################
# CUSTOMIZATIONS


AIRSTACK_BUILD_TEMPLATES_COMMON := Dockerfile.packages Dockerfile.services
AIRSTACK_BUILD_TEMPLATES_PRODUCTION := Dockerfile.from.production $(AIRSTACK_BUILD_TEMPLATES_COMMON)
AIRSTACK_BUILD_TEMPLATES_DEVELOPMENT := Dockerfile.from.development $(AIRSTACK_BUILD_TEMPLATES_COMMON)
AIRSTACK_BUILD_TEMPLATES_TEST := Dockerfile.from.test $(AIRSTACK_BUILD_TEMPLATES_COMMON)



################################################################################
# BOOTSTRAP MAKEFILE: DO NOT EDIT BELOW THIS LINE
AIRSTACK_HOME ?= ~/.airstack
ifeq ($(shell test -d $(AIRSTACK_HOME)/package/airstack/bootstrap && echo y),y)
include $(AIRSTACK_HOME)/package/airstack/bootstrap/Makefile
else
.PHONY: init
init:
	curl -s https://raw.githubusercontent.com/airstack/bootstrap/master/install | sh -e
	@$(MAKE) init
.DEFAULT:
	@echo Please run \'make init\' to initialize Airstack
endif
