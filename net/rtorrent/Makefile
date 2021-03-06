#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rtorrent
PKG_REV:=1189
PKG_VERSION:=0.8.6_r$(PKG_REV)
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=svn://rakshasa.no/libtorrent/trunk/rtorrent
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_PROTO:=svn

PKG_FIXUP:=libtool
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/rtorrent
  SUBMENU:=BitTorrent
  SECTION:=net
  CATEGORY:=Network
  TITLE:=BitTorrent client for ncurses
  URL:=http://libtorrent.rakshasa.no/
  DEPENDS:=+libcurl +libtorrent +libncurses +libsigcxx +xmlrpc-c-server +libpthread
endef

define Package/rtorrent/description
 rTorrent is a BitTorrent client for ncurses, using the libtorrent library.
 The client and library are written in C++ with emphasis on speed and
 efficiency, while delivering equivalent features to those found in GUI
 based clients in an ncurses client.
endef

ifneq ($(CONFIG_GCC_VERSION_3_4)$(CONFIG_GCC_VERSION_4_1),)
TARGET_CPPFLAGS += -fno-strict-aliasing
endif

TARGET_LDFLAGS += -lpthread -Wl,-rpath-link=$(STAGING_DIR)/usr/lib

CONFIGURE_ARGS+= \
	--enable-shared \
	--disable-static \
	--disable-debug \
	--with-xmlrpc-c

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh );
	$(call Build/Configure/Default)
endef

define Package/rtorrent/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/rtorrent $(1)/usr/bin/
endef

$(eval $(call BuildPackage,rtorrent))
