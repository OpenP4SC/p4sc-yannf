# Copyright 2017 Intel Corporation. 
# Use of this source code is governed by a BSD-style
# license that can be found in the LICENSE file.

PATH_TO_MK = ../mk
IMAGENAME = yanff-pktgen

# Pktgen variables
NOCHECK_PKTGEN = yes
PKTGEN_VERSION=3.4.0
PKTGEN_DIR=pktgen-$(PKTGEN_VERSION)

include $(PATH_TO_MK)/leaf.mk

# Main DPDK variables
DPDK_INSTALL_DIR=$(RTE_TARGET)-install
export WORKDIR=/workdir
# Uncomment to build DEBUG DPDK
# EXTRA_CFLAGS = -g -O0

all: pktgen
	cp $(PKTGEN_DIR)/Pktgen.lua .

$(DPDK_DIR):
	curl http://fast.dpdk.org/rel/dpdk-$(DPDK_VERSION).tar.xz | tar xJ

$(DPDK_DIR)/$(DPDK_INSTALL_DIR): $(DPDK_DIR)
	$(MAKE) -C $(DPDK_DIR) config T=$(RTE_TARGET)
	$(MAKE) -C $(DPDK_DIR) install T=$(RTE_TARGET) DESTDIR=$(DPDK_INSTALL_DIR)

$(PKTGEN_DIR):
	curl http://dpdk.org/browse/apps/pktgen-dpdk/snapshot/pktgen-$(PKTGEN_VERSION).tar.xz | tar xJ

$(PKTGEN_DIR)/app/$(RTE_TARGET)/pktgen: $(DPDK_DIR)/$(DPDK_INSTALL_DIR) $(PKTGEN_DIR)
	$(MAKE) -j1 -C $(PKTGEN_DIR)

pktgen: $(PKTGEN_DIR)/app/$(RTE_TARGET)/pktgen
	cp $(PKTGEN_DIR)/app/$(RTE_TARGET)/pktgen .

clean:
	-rm pktgen Pktgen.lua
	-rm -rf $(DPDK_DIR)
	-rm -rf $(PKTGEN_DIR)
