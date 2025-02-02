# SPDX-License-Identifier: CC0-1.0
#
# SPDX-FileContributor: Antonio Niño Díaz, 2023

_MAJOR		:= 1
_MINOR		:= 1
_PATCH		:= 0

# Tools
# -----

CP		:= cp
INSTALL		:= install
PREFIX		:= arm-none-eabi-
CC		:= $(PREFIX)gcc
RM		:= rm -rf

# Verbose flag
# ------------

ifeq ($(VERBOSE),1)
V		:=
else
V		:= @
endif

# Targets
# -------

OBJS		:= ds_arm7_vram_crt0.o ds_arm7_crt0.o ds_arm7_iwram_crt0.o \
			   ds_arm9_crt0.o

.PHONY: all clean install

all: $(OBJS)

clean:
	@echo "  CLEAN"
	$(V)$(RM) $(OBJS)

INSTALLDIR	?= /opt/blocksds/core/sys/crts
INSTALLDIR_ABS	:= $(abspath $(INSTALLDIR))

install: all
	@echo "  INSTALL $(INSTALLDIR_ABS)"
	@test $(INSTALLDIR_ABS)
	$(V)$(RM) $(INSTALLDIR_ABS)
	$(V)$(INSTALL) -d $(INSTALLDIR_ABS)
	$(V)$(CP) -r ./*.o ./*.ld ./*.mem COPYING $(INSTALLDIR_ABS)

# Rules
# -----

ASFLAGS		:= -x assembler-with-cpp
ARCHARM7	:= -mcpu=arm7tdmi -mtune=arm7tdmi
ARCHARM9	:= -march=armv5te -mtune=arm946e-s

ds_arm7_vram_crt0.o: ds_arm7_crt0.s
	@echo "  AS.7    $@"
	$(V)$(CC) $(ASFLAGS) $(ARCHARM7) -DVRAM -c -o $@ $<

# They are the same, but it's more intuitive to have two files than to remember
# that the VRAM crt0 works with the IWRAM linkerscript.
ds_arm7_iwram_crt0.o: ds_arm7_vram_crt0.o
	@echo "  CP      $@"
	$(V)$(CP) $< $@

ds_arm7_crt0.o: ds_arm7_crt0.s
	@echo "  AS.7    $@"
	$(V)$(CC) $(ASFLAGS) $(ARCHARM7) -c -o $@ $<

ds_arm9_crt0.o: ds_arm9_crt0.s
	@echo "  AS.9    $@"
	$(V)$(CC) $(ASFLAGS) $(ARCHARM9) -c -o $@ $<
