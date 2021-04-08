#
# arch/arm64/boot/Makefile
#
# This file is included by the global makefile so that you can add your own
# architecture-specific flags and dependencies.
#
# This file is subject to the terms and conditions of the GNU General Public
# License.  See the file "COPYING" in the main directory of this archive
# for more details.
#
# Copyright (C) 2012, ARM Ltd.
# Author: Will Deacon <will.deacon@arm.com>
#
# Based on the ia64 boot/Makefile.
#

include $(srctree)/arch/arm64/boot/dts/Makefile

targets := Image Image.gz

DTB_OBJS += $(shell find -L $(obj)/dts/ -name \*.dtb)

DTBO_OBJS := $(shell find $(obj)/dts/ -name \*.dtbo)

ifeq ($(CONFIG_MACH_EXYNOS7885_A30_GLOBAL),y)
targets += dtb.img dtbo.img

$(obj)/dtb.img: $(DTB_OBJS) FORCE
	$(call if_changed,mkdtimg)

$(obj)/dtbo.img: $(DTBO_OBJS) FORCE
	$(call if_changed,mkdtimg)
endif

ifeq ($(CONFIG_MACH_EXYNOS7885_A30S_GLOBAL),y)
targets += dtb.img dtbo.img

$(obj)/dtb.img: $(DTB_OBJS) FORCE
	$(call if_changed,mkdtimg)

$(obj)/dtbo.img: $(DTBO_OBJS) FORCE
	$(call if_changed,mkdtimg)
endif

ifeq ($(CONFIG_MACH_EXYNOS7885_A40_GLOBAL),y)
targets += dtb.img dtbo.img

$(obj)/dtb.img: $(DTB_OBJS) FORCE
	$(call if_changed,mkdtimg)

$(obj)/dtbo.img: $(DTBO_OBJS) FORCE
	$(call if_changed,mkdtimg)
endif

ifeq ($(CONFIG_MACH_EXYNOS7885_M20_GLOBAL),y)
targets += dtb.img

$(obj)/dtb.img: $(DTB_OBJS) FORCE
	$(call if_changed,dtbtool_exynos)
endif

ifeq ($(CONFIG_MACH_EXYNOS7885_M30_GLOBAL),y)
targets += dtb.img

$(obj)/dtb.img: $(DTB_OBJS) FORCE
	$(call if_changed,dtbtool_exynos)
endif

$(obj)/Image: vmlinux FORCE
	$(call if_changed,objcopy)

$(obj)/Image.bz2: $(obj)/Image FORCE
	$(call if_changed,bzip2)

$(obj)/Image-dtb: $(obj)/Image $(DTB_OBJS) FORCE
	$(call if_changed,cat)

$(obj)/Image.gz: $(obj)/Image FORCE
	$(call if_changed,gzip)

$(obj)/Image.lz4: $(obj)/Image FORCE
	$(call if_changed,lz4)

$(obj)/Image.lzma: $(obj)/Image FORCE
	$(call if_changed,lzma)

$(obj)/Image.lzo: $(obj)/Image FORCE
	$(call if_changed,lzo)

$(obj)/Image.gz-dtb: $(obj)/Image.gz $(DTB_OBJS) FORCE
	$(call if_changed,cat)


install: $(obj)/Image
	$(CONFIG_SHELL) $(srctree)/$(src)/install.sh $(KERNELRELEASE) \
	$(obj)/Image System.map "$(INSTALL_PATH)"

zinstall: $(obj)/Image.gz
	$(CONFIG_SHELL) $(srctree)/$(src)/install.sh $(KERNELRELEASE) \
	$(obj)/Image.gz System.map "$(INSTALL_PATH)"
