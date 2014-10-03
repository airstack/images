################################################################################
# CUSTOMIZATIONS

# DEBUG LEVELS
# 0 - no output
# 1 - print info
# 2 - print info, stdout, and stderr
# 3 - verbose
# 4 - very verbose
# DEBUG_LEVEL ?= 2

AIRSTACK_BUILD_TEMPLATES_COMMON := Dockerfile.packages Dockerfile.services
AIRSTACK_BUILD_TEMPLATES_PRODUCTION := Dockerfile.from.production $(AIRSTACK_BUILD_TEMPLATES_COMMON)
AIRSTACK_BUILD_TEMPLATES_DEVELOPMENT := Dockerfile.from.development $(AIRSTACK_BUILD_TEMPLATES_COMMON)
AIRSTACK_BUILD_TEMPLATES_TEST := Dockerfile.from.test $(AIRSTACK_BUILD_TEMPLATES_COMMON)

# TODO add common settings makefile
# include $(AIRSTACK_HOME)/.airstack.mk

.PHONY: build-all-j5
build-all-j5:
	$(MAKE) -j5 build-all

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
