#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ebtables
PKG_VERSION:=2.0.10-4
PKG_RELEASE:=5

PKG_SOURCE:=$(PKG_NAME)-v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/ebtables
PKG_HASH:=dc6f7b484f207dc712bfca81645f45120cb6aee3380e77a1771e9c34a9a4455d

PKG_BUILD_DIR:=$(BUILD_DIR)/ebtables-v$(PKG_VERSION)
PKG_LICENSE:=GPL-2.0

include $(INCLUDE_DIR)/package.mk

define Package/ebtables
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Firewall
  DEPENDS:=+kmod-ebtables
  TITLE:=Ethernet bridge firewall administration utility
  URL:=http://ebtables.sourceforge.net/
endef

define Package/ebtables-utils
  $(call Package/ebtables)
  DEPENDS += ebtables
  TITLE:=ebtables save/restore utilities
endef

define Package/ebtables/description
	The ebtables program is a filtering tool for a bridging firewall. The
	filtering is focussed on the Link Layer Ethernet frame fields. Apart
	from filtering, it also gives the ability to alter the Ethernet MAC
	addresses and implement a brouter.
endef

define Package/ebtables-utils/description
	$(call Package/ebtables/description)
endef

MAKE_VARS += EXT_LIBSI="$(LIBGCC_S)"

MAKE_FLAGS += \
	CFLAGS="$(TARGET_CFLAGS)" \
	LIBDIR="/usr/lib/ebtables"

define Package/ebtables/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/ethertypes $(1)/etc/
	$(INSTALL_DIR) $(1)/usr/lib/ebtables
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib*.so $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/extensions/*.so $(1)/usr/lib/ebtables/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ebtables $(1)/usr/sbin/
endef

define Package/ebtables-utils/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ebtables-save $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ebtables-restore $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,ebtables))
$(eval $(call BuildPackage,ebtables-utils))
