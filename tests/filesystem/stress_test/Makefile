# SPDX-License-Identifier: CC0-1.0
#
# SPDX-FileContributor: Antonio Niño Díaz, 2023

# Having python3 as a hard dependency of BlocksDS just for this test is a bad
# idea. The Makefile of the parent folder will try to build this test because it
# iterates every child folder, so this Makefile simply skips the build if
# python3 isn't found.

ifeq (`which python3`,)

$(warning "Skipping filesystem stress test because python3 wasn't found")

else

# User config

NAME		:= filesystem_stress_test
GAME_TITLE	:= Filesystem stress test

# Source code paths

SOURCEDIRS	:= source
NITROFATDIR	:= nitrofat

include ../../Makefile.include

nitrofat:
	@echo "  GEN_FILESYSTEM"
	@python3 gen_filesystem.py

clean: clean_nitrofat

clean_nitrofat:
	@echo "  CLEAN NITROFAT"
	@rm -rf nitrofat

endif
