# Copyright (C) 2020 Cascoda Ltd.

include $(TOPDIR)/rules.mk

PKG_NAME:=cascoda-sdk
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Cascoda/cascoda-sdk.git
PKG_SOURCE_DATE:=2022-06-23
PKG_SOURCE_VERSION:=00cd19cfe14c6d5a38d60c057d746285f64e40ba

PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_MIRROR_HASH:=144cc59bcc5798390217fe88a5e0fc96ea12cea39690fd1c29e144fd126d9d46

PKG_MAINTAINER:=Elie El Khoury <e.khoury@cascoda.com>, Ciaran Woodward <c.woodward@cascoda.com>

PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_CHECK_FORMAT_SECURITY:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/cascoda-sdk
  SECTION:=cascoda-sdk
  DEPENDS:=+libpthread +libstdcpp +hidapi +kmod-usb-hid
  CATEGORY:=Utilities
  TITLE:=Cascoda utilities
endef

define Package/cascoda-sdk/description
  Cascoda Utilities: This package installs the following utilities

	ca-ot-cli-ftd           - A command line interface to the OpenThread stack, acting as a Full Thread Device
	ca-ot-cli-mtd           - The OpenThread CLI, acting as a Minimal Thread Device
	ca-sniffer              - An example program for sniffing 802.15.4 traffic on a specific channel.
	ca-ot-ncp               - Network Co-Processor for interacting with openthread wpantund.
	ca-ot-sensordemo-server - A server program able to connect to thread devices and interpret sensor data.
	ca-serial-adapter       - A useful program for interacting with a serial application running on baremetal.
	ca-evbme-get            - Prints information about connected Cascoda devices
endef

CMAKE_OPTIONS += -DBUILD_TESTING:Bool=OFF

define Build/Configure
  $(call Build/Configure/Default,--with-linux-headers=$(LINUX_DIR))
	sed -i '/MBEDTLS_HAVE_ASM/d' $(PKG_BUILD_DIR)/_deps/openthread-src/third_party/mbedtls/mbedtls-config.h
endef

define Package/cascoda-sdk/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/bin/ot-cli-posix-ftd $(1)/usr/bin/ca-ot-cli-ftd
	$(CP) $(PKG_BUILD_DIR)/bin/ot-cli-posix-mtd $(1)/usr/bin/ca-ot-cli-mtd
	$(CP) $(PKG_BUILD_DIR)/bin/sniffer $(1)/usr/bin/ca-sniffer
	$(CP) $(PKG_BUILD_DIR)/bin/ot-ncp-posix $(1)/usr/bin/ca-ot-ncp
	$(CP) $(PKG_BUILD_DIR)/bin/ot-sensordemo-server $(1)/usr/bin/ca-ot-sensordemo-server
	$(CP) $(PKG_BUILD_DIR)/bin/serial-adapter $(1)/usr/bin/ca-serial-adapter
	$(CP) $(PKG_BUILD_DIR)/bin/evbme-get $(1)/usr/bin/ca-evbme-get
endef

$(eval $(call BuildPackage,cascoda-sdk))
