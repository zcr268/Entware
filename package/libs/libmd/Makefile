include $(TOPDIR)/rules.mk

PKG_NAME:=libmd
PKG_VERSION:=1.1.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://archive.hadrons.org/software/libmd/
PKG_HASH:=1bd6aa42275313af3141c7cf2e5b964e8b1fd488025caf2f971f43b00776b332

PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
	--enable-static

define Package/libmd
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Message Digest functions from BSD systems
  ABI_VERSION:=0
endef

define Package/libmd/description
  This library provides message digest functions found on BSD systems either
  on their libc or libmd libraries and lacking on others like GNU systems,
  thus making it easier to port projects with strong BSD origins, without
  needing to embed the same code over and over again on each project.
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libmd.a $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libmd*.pc $(1)/opt/lib/pkgconfig/
	$(CP) $(PKG_INSTALL_DIR)/opt/include/* $(1)/opt/include/
endef

$(eval $(call BuildPackage,libmd))
