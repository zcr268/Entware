#
# Copyright (C) 2008-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lldpd
PKG_VERSION:=1.0.19
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/lldpd/lldpd/releases/download/$(PKG_VERSION)/
PKG_HASH:=4de17fe5137b4d44a7bd57f8dfc80cffe2c8bb3691b4ae3012b5a6ea20d79ee0

PKG_MAINTAINER:=Stijn Tintel <stijn@linux-ipv6.be>
PKG_LICENSE:=ISC
PKG_CPE_ID:=cpe:/a:lldpd_project:lldpd

PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=lto
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/lldpd
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing and Redirection
  TITLE:=Link Layer Discovery Protocol daemon
  URL:=https://lldpd.github.io/
  DEPENDS:=+libcap +libevent2 +USE_GLIBC:libbsd +LLDPD_WITH_JSON:libjson-c +LLDPD_WITH_SNMP:libnetsnmp
  USERID:=lldp=121:lldp=129
  MENU:=1
endef

define Package/lldpd/config
source "$(SOURCE)/Config.in"
endef

define Package/lldpd/description
	LLDP (Link Layer Discovery Protocol) is an industry standard protocol designed
	to supplant proprietary Link-Layer protocols such as
	Extreme's EDP (Extreme Discovery Protocol) and
	CDP (Cisco Discovery Protocol).
	The goal of LLDP is to provide an inter-vendor compatible mechanism to deliver
	Link-Layer notifications to adjacent network devices.
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/liblldpctl.so* $(1)/opt/lib/
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/lldpctl.h $(1)/opt/include/lldpctl.h
	$(CP) $(PKG_INSTALL_DIR)/opt/include/lldp-const.h $(1)/opt/include/lldp-const.h
endef

define Package/lldpd/install
	$(INSTALL_DIR) $(1)/opt/etc/lldpd.d
	$(INSTALL_DIR) $(1)/opt/lib $(1)/opt/sbin
	$(CP) $(PKG_INSTALL_DIR)/opt/sbin/lldp{cli,ctl,d} $(1)/opt/sbin/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/liblldpctl.so* $(1)/opt/lib/
endef

#define Package/lldpd/conffiles
#/etc/config/lldpd
#endef

CONFIGURE_ARGS += \
	$(if $(CONFIG_LLDPD_WITH_PRIVSEP), \
	--with-privsep-user=lldp \
	--with-privsep-group=lldp \
	--with-privsep-chroot=/opt/var/run/lldp \
	,--disable-privsep) \
	--with-readline=no \
	--with-embedded-libevent=no \
	--disable-hardening \
	--without-xml \
	--disable-doxygen-doc \
	--sysconfdir=/opt/etc \
	--enable-oldies \
	$(if $(CONFIG_LLDPD_WITH_CDP),,--disable-cdp) \
	$(if $(CONFIG_LLDPD_WITH_FDP),,--disable-fdp) \
	$(if $(CONFIG_LLDPD_WITH_EDP),,--disable-edp) \
	$(if $(CONFIG_LLDPD_WITH_LLDPMED),,--disable-lldpmed) \
	$(if $(CONFIG_LLDPD_WITH_DOT1),,--disable-dot1) \
	$(if $(CONFIG_LLDPD_WITH_DOT3),,--disable-dot3) \
	$(if $(CONFIG_LLDPD_WITH_CUSTOM),,--disable-custom) \
	$(if $(CONFIG_LLDPD_WITH_SONMP),,--disable-sonmp) \
	$(if $(CONFIG_LLDPD_WITH_JSON),--enable-json0,) \
	$(if $(CONFIG_LLDPD_WITH_SNMP),--with-snmp,) \
	$(if $(CONFIG_USE_GLIBC),,--without-libbsd)

TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

$(eval $(call BuildPackage,lldpd))
