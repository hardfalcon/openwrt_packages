#
# Copyright (C) 2015-2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libuv
PKG_VERSION:=1.51.0
PKG_RELEASE:=0

PKG_SOURCE:=$(PKG_NAME)-v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://dist.libuv.org/dist/v$(PKG_VERSION)/
PKG_HASH:=5f0557b90b1106de71951a3c3931de5e0430d78da1d9a10287ebc7a3f78ef8eb
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-v$(PKG_VERSION)

PKG_MAINTAINER:=Marko Ratkaj <markoratkaj@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE
PKG_CPE_ID:=cpe:/a:libuv:libuv

CMAKE_BINARY_SUBDIR:=out/cmake

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libuv
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Cross-platform asychronous I/O library
  URL:=https://libuv.org/
  DEPENDS:=+libpthread +librt
  ABI_VERSION:=1
endef

define Package/libuv/description
 libuv is a multi-platform support library with a focus on asynchronous I/O. It
 was primarily developed for use by Node.js, but it's also used by Luvit, Julia,
 pyuv, and others.
endef

CMAKE_OPTIONS += -DBUILD_TESTING=OFF

define Build/InstallDev
	$(call Build/InstallDev/cmake,$(1))
	$(SED) 's,/usr/include,$$$${prefix}/include,g' $(1)/usr/lib/pkgconfig/libuv.pc
	$(SED) 's,/usr/lib,$$$${prefix}/lib,g' $(1)/usr/lib/pkgconfig/libuv.pc
	$(SED) 's,/usr/include,$$$${prefix}/include,g' $(1)/usr/lib/pkgconfig/libuv-static.pc
	$(SED) 's,/usr/lib,$$$${prefix}/lib,g' $(1)/usr/lib/pkgconfig/libuv-static.pc
endef

define Package/libuv/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libuv.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libuv))
