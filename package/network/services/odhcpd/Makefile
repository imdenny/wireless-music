#
# Copyright (C) 2013-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=odhcpd
PKG_VERSION:=2015-11-19
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://kkgithub.com/sbyx/odhcpd.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=01d3f9d64486ac1daa144848944e877e7f0cb762

PKG_MAINTAINER:=Steven Barth <steven@midlink.org>
PKG_LICENSE:=GPL-2.0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS += -DUBUS=1

ifneq ($(CONFIG_PACKAGE_odhcpd_ext_cer_id),0)
  CMAKE_OPTIONS += -DEXT_CER_ID=$(CONFIG_PACKAGE_odhcpd_ext_cer_id)
endif


define Package/odhcpd
  SECTION:=net
  CATEGORY:=Network
  TITLE:=OpenWrt DHCP/DHCPv6(-PD)/RA Server & Relay
  DEPENDS:=+libubox +libuci +libubus
endef

define Package/odhcpd/config
  config PACKAGE_odhcpd_ext_cer_id
    int "CER-ID Extension ID (0 = disabled)"
    depends on PACKAGE_odhcpd
    default 0
endef

define Package/odhcpd/description
 odhcpd is a daemon for serving and relaying IP management protocols to
 configure clients and downstream routers. It tries to follow the RFC 6204
 requirements for IPv6 home routers.
 
 odhcpd provides server services for DHCP, RA, stateless and stateful DHCPv6,
 prefix delegation and can be used to relay RA, DHCPv6 and NDP between routed
 (non-bridged) interfaces in case no delegated prefixes are available.
endef

define Package/odhcpd/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/odhcpd $(1)/usr/sbin/
	$(INSTALL_BIN) ./files/odhcpd-update $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/odhcpd.init $(1)/etc/init.d/odhcpd
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/odhcpd.defaults $(1)/etc/uci-defaults
endef

$(eval $(call BuildPackage,odhcpd))
