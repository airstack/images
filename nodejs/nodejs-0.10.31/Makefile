################################################################################
# CONFIG VARS
################################################################################

.PHONY: all build

# Deriving names from directory structure.
NAME := airstack/nodejs
DOCKER_IMAGE := $(NAME):latest

ROOTDIR := $(realpath .)

# Detecting OS
uname_S := $(shell sh -c 'uname -s 2>/dev/null || echo not')

CMD := /bin/bash
CMD_CONSOLE := sh -c "{ /etc/runit/2 &}; chpst -u airstack bash"

USERDIR := airstack
USERNAME := $(USERDIR)
USERFLAG := --user $(USERNAME)
USERFLAG_CONSOLE := --user root
COMMON_RUNFLAGS := --publish-all --workdir /home/$(USERDIR) -e HOME=$(USERDIR) $(NAME):$(VERSION)
LINUX_RUNFLAGS := --volume $(USERDIR)/output:/home/$(USERDIR)/output --volume $(ROOTDIR)/input:/home/$(USERDIR)/input:ro
OSX_RUNFLAGS := --volume $(ROOTDIR)/output:/home/$(USERDIR)/output --volume /home/docker/base0:/home/$(USERDIR)/base0 --volume $(ROOTDIR)/input:/home/$(USERDIR)/input:ro

ifeq ($(uname_S),Darwin)
	OS_SPECIFIC_RUNFLAGS = $(OSX_RUNFLAGS)
else
	OS_SPECIFIC_RUNFLAGS = $(LINUX_RUNFLAGS)
endif


################################################################################
# COMMANDS
################################################################################

all: build

build:
	docker build -t "$(DOCKER_IMAGE)" .

init:
ifeq ($(uname_S),Darwin)
ifneq ($(shell boot2docker status),running)
	@boot2docker up
endif
export DOCKER_HOST=tcp://$(shell boot2docker ip 2>/dev/null):2375
endif

console:
	docker run --rm -i -t $(OS_SPECIFIC_RUNFLAGS) $(USERFLAG_CONSOLE) $(COMMON_RUNFLAGS) $(CMD_CONSOLE)

debug: init
	@if [ `boot2docker ssh 'ifconfig docker0 | grep -io multicast | wc -w'` -lt 1 ]; \
		then ifconfig docker0 -multicast && ifconfig docker0 multicast; fi
	docker run --rm -i -t $(OS_SPECIFIC_RUNFLAGS) $(USERFLAG) $(COMMON_RUNFLAGS) $(CMD)
