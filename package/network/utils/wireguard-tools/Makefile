#
# Copyright (C) 2016-2019 Jason A. Donenfeld <Jason@zx2c4.com>
# Copyright (C) 2016 Baptiste Jonglez <openwrt@bitsofnetworks.org>
# Copyright (C) 2016-2017 Dan Luedtke <mail@danrl.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=wireguard-tools

PKG_VERSION:=1.0.20210914
PKG_RELEASE:=4

PKG_SOURCE:=wireguard-tools-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://git.zx2c4.com/wireguard-tools/snapshot/
PKG_HASH:=97ff31489217bb265b7ae850d3d0f335ab07d2652ba1feec88b734bc96bd05ac

PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

MAKE_PATH:=src
MAKE_VARS += PLATFORM=linux

define Package/wireguard-tools
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=VPN
  URL:=https://www.wireguard.com
  MAINTAINER:=Jason A. Donenfeld <Jason@zx2c4.com>
  TITLE:=WireGuard userspace control program (wg)
  DEPENDS:=+ip @!LINUX_2_6_36
endef

define Package/wireguard-tools/description
  WireGuard is a novel VPN that runs inside the Linux Kernel and utilizes
  state-of-the-art cryptography. It aims to be faster, simpler, leaner, and
  more useful than IPSec, while avoiding the massive headache. It intends to
  be considerably more performant than OpenVPN.  WireGuard is designed as a
  general purpose VPN for running on embedded interfaces and super computers
  alike, fit for many different circumstances. It uses UDP.

  This package provides the userspace control program for WireGuard,
  `wg(8)`, a netifd protocol helper, and a re-resolve watchdog script.
endef

define Package/wireguard-tools/install
	$(INSTALL_DIR) $(1)/opt/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/wg $(1)/opt/bin/
#	$(INSTALL_BIN) ./files/wireguard_watchdog $(1)/usr/bin/
#	$(INSTALL_DIR) $(1)/lib/netifd/proto/
#	$(INSTALL_BIN) ./files/wireguard.sh $(1)/lib/netifd/proto/
	$(INSTALL_DIR) $(1)/opt/etc/wireguard $(1)/opt/var/run/wireguard
endef

$(eval $(call BuildPackage,wireguard-tools))
