#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libopusenc
PKG_VERSION:=0.3
PKG_RELEASE:=0

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://downloads.xiph.org/releases/opus
PKG_HASH:=f616d3aff9b2034547894ccb8ab56c36cf1a4acb0d922c5d7119f97bbe58642c

PKG_MAINTAINER:=Eduardo Abinader <eduardoabinader@gmail.com>
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libopusenc
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libopus
  TITLE:=OPUS Audio stream files
  URL:=https://opus-codec.org
endef

define Package/libopusenc/description
 Libopusenc provides a high-level API for creating .opus files and streams.
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libopusenc.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libopusenc/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libopusenc))
