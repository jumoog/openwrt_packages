#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=usbutils
PKG_VERSION:=001
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@KERNEL/linux/utils/usb/usbutils
PKG_MD5SUM:=40398698053f9f735550117322430e57

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/usbutils
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libusb-1.0 +zlib
  TITLE:=USB devices listing utilities
  URL:=http://www.linux-usb.org/
endef

define Package/usbutils/postinst
#!/bin/sh
(cd $${IPKG_INSTROOT}/usr/share; $${PKG_ROOT}/usr/sbin/update-usbids.sh)
exit 0
endef

define Package/usbutils/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/lsusb $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/update-usbids.sh $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/usr/share
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/usb.ids.gz $(1)/usr/share/
endef

$(eval $(call BuildPackage,usbutils))
