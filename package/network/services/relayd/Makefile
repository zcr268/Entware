#
# Copyright (C) 2010-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=relayd
PKG_RELEASE:=1

PKG_SOURCE_URL=$(PROJECT_GIT)/project/relayd.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2023-01-28
PKG_SOURCE_VERSION:=f646ba40489371e69f624f2dee2fc4e19ceec00e
PKG_MIRROR_HASH:=658a09a1a947c148c2827335c7bbe126f4bcf361d2de6d9de7cca432c9fe04d3

PKG_MAINTAINER:=Felix Fietkau <nbd@nbd.name>
PKG_LICENSE:=GPL-2.0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/relayd
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing and Redirection
  TITLE:=Transparent routing / relay daemon
  DEPENDS:=+libubox
endef

TARGET_CFLAGS += -I$(STAGING_DIR)/opt/include

define Package/relayd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/relayd $(1)/opt/sbin/relayd
	$(INSTALL_DIR) $(1)/opt/etc/init.d
#	$(INSTALL_BIN) ./files/relay.init $(1)/etc/init.d/relayd
endef

$(eval $(call BuildPackage,relayd))
