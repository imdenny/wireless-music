#
# Copyright (C) 2008-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libconfig
PKG_VERSION:=1.7.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/hyperrealm/libconfig/releases/download/v$(PKG_VERSION)/
PKG_MD5SUM:=15ec701205f91f21b1187f8b61e0d64f

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

PKG_MAINTAINER:=Felix Fietkau <nbd@openwrt.org>
PKG_LICENSE:=LGPL-2.1+

include $(INCLUDE_DIR)/package.mk

define Package/libconfig
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Configuration File Library
  URL:=http://www.hyperrealm.com/libconfig/
endef

define Package/libconfig/description
 Libconfig is a simple library for manipulating structured configuration
 files. This file format is more compact and more readable than XML. And
 unlike XML, it is type-aware, so it is not necessary to do string
 parsing in application code.

 Libconfig is very compact -- just 38K for the stripped C shared
 library (less than one-fourth the size of the expat XML parser library)
 and 66K for the stripped C++ shared library. This makes it well-suited
 for memory-constrained systems like handheld devices.
endef

CONFIGURE_ARGS += \
	--enable-shared \
	--disable-static \
	--disable-cxx

define Build/InstallDev
	$(CP) $(PKG_INSTALL_DIR)/* $(1)/
endef

define Package/libconfig/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libconfig.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libconfig))
