#
# Copyright (C) 2013-2015 NDM Systems, Inc. http://www.ndmsystems.com/
#
include $(TOPDIR)/rules.mk

PKG_NAME:=opt-stdlib
PKG_RELEASE:=1
PKG_VERSION:=1.7.0-12
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

ifeq ($(CONFIG_mipsel),y)
  PKG_SOURCE:=toolchain-embtoolkit-$(PKG_VERSION)-mipsel-linux-gcc-4.9.2-uclibc-0.9.33-ndm-3-150615.tar.bz2
  PKG_MD5SUM:=1bf339e6fb8eae2772df0eb53ee5513e
else ifeq ($(CONFIG_mips),y)
  PKG_SOURCE:=toolchain-embtoolkit-$(PKG_VERSION)-mips-linux-gcc-4.9.2-uclibc-0.9.33-ndm-3-150615.tar.bz2
  PKG_MD5SUM:=de369ece2bf38c8c7966588ca27086b1
endif

PKG_SOURCE_URL:=https://github.com/ndmsystems/embtoolkit/releases/download/embtoolkit-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=Optware
  CATEGORY:=Optware
  TITLE:=Optware standart library
  MAINTAINER:=NDMS Developers Team <support@ndmsystems.com>
  DEFAULT:=m
endef

UCLIBC_LIB_LIST:=libc.so.0 ld-uClibc.so.0 libcrypt.so.0 \
                 libdl.so.0 libm.so.0 libutil.so.0 libresolv.so.0 \
                 librt.so.0 libpthread.so.0 libgcc_s.so.1

define Build/Prepare
	$(HOST_TAR) -xf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR)
endef

define Build/Configure
	#nothing to do
endef

define Build/Compile
	#nothing to do
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/opt/lib

	for lib in $(UCLIBC_LIB_LIST); do \
		find $(PKG_BUILD_DIR)/sysroot-* -name $$$${lib} -exec cp {} $(1)/opt/lib/ \; ;\
	done

	ln -sf libgcc_s.so.1 $(1)/opt/lib/libgcc_s.so
endef

$(eval $(call BuildPackage,$(PKG_NAME)))

