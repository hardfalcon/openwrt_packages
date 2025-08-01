#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=fuse3
PKG_VERSION:=3.17.3
PKG_RELEASE:=1

PKG_SOURCE:=fuse-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/libfuse/libfuse/releases/download/fuse-$(PKG_VERSION)
PKG_HASH:=de8190448909aa97a222d435bc130aae98331bed4215e9f4519b4b5b285a1d63
PKG_BUILD_DIR:=$(BUILD_DIR)/fuse-$(PKG_VERSION)

PKG_MAINTAINER:=
PKG_CPE_ID:=cpe:/a:fuse_project:fuse

PKG_CONFIG_DEPENDS:=CONFIG_PACKAGE_fuse3-utils

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk

define Package/fuse3/Default
  TITLE:=FUSE
  URL:=https://github.com/libfuse/libfuse
  SUBMENU:=Filesystem
endef

define Package/fuse3/Default/description
 fuse3 (Filesystem in UserSpacE)
endef

define Package/libfuse3
$(call Package/fuse3/Default)
  TITLE+= library
  URL:=https://github.com/libfuse/libfuse
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+kmod-fuse +libpthread
  ABI_VERSION:=3
  LICENSE:=LGPL-2.1-only
  LICENSE_FILES:=LGPL2.txt
endef

define Package/libfuse3/description
$(call Package/fuse3/Default/description)
 This package contains the fuse3 shared libraries, needed by other programs.
 - libfuse3
endef

define Package/fuse3-utils
$(call Package/fuse3/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libfuse3
  TITLE+= (utilities)
  SUBMENU:=Filesystem
  LICENSE:=GPL-2.0-only
  LICENSE_FILES:=GPL2.txt
endef

define Package/fuse3-utils/description
$(call Package/fuse3/Default/description)
 This package contains the FUSE utilities.
 - fusermount3
 - mount.fuse3
endef

MESON_ARGS += \
	-Ddisable-mtab=true \
	-Dudevrulesdir=/dev/null \
	-Dutils=$(if $(CONFIG_PACKAGE_fuse3-utils),true,false) \
	-Dexamples=false \
	-Duseroot=false

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/fuse3
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/fuse3/*.h $(1)/usr/include/fuse3
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libfuse3.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/fuse3.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libfuse3/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libfuse3.so.* $(1)/usr/lib/
endef

define Package/fuse3-utils/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/fusermount3 $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/mount.fuse3 $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,libfuse3))
$(eval $(call BuildPackage,fuse3-utils))
