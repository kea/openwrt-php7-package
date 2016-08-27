#
# Copyright (C) 2006-2016 Kea
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=php7-mod-onion-omega
PKG_VERSION:=0.1
PKG_RELEASE:=1

PKG_MAINTAINER:=Manuel Kea Baldassarri <manuel@baldassarri.me>

PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=LICENSE-GPLv2

PKG_SOURCE:=master.zip
PKG_BUILD_DIR:=$(BUILD_DIR)/Onion-Omega-Php-extension-master
PKG_SOURCE_URL:=https://github.com/kea/Onion-Omega-Php-extension/archive/
PKG_MD5SUM:=6316d6a42fc0333b9699fbada946eea0

PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Build/Prepare
	$(Build/Prepare/Default)
	( cd $(PKG_BUILD_DIR)/$(MAKE_PATH); $(STAGING_DIR_HOST)/usr/bin/phpize; rm aclocal.m4 && aclocal && autoconf )
endef

CONFIGURE_VARS+= \
	OMEGA_DIR=$(STAGING_DIR_HOST)/usr/

CONFIGURE_ARGS+= \
	--with-php-config=$(STAGING_DIR_HOST)/usr/bin/php-config

define Package/php7-mod-onion-omega
	SUBMENU:=PHP
	SECTION:=lang
	CATEGORY:=Languages
	TITLE:=Onion Omega PHP 7 extension driver
	URL:=https://github.com/kea/Onion-Omega-Php-extension
	# add lib onion i2c
	DEPENDS:=+php7 +libonionpwmexp +libonionoledexp +libonionrelayexp +libonioni2c
	CONFIGURE_PATH:=src
	MAKE_PATH:=src
endef

define Package/php7-mod-onion-omega/description
	Onion Omega PHP 7 extension driver:
	PWM, Relay, Oled and I2C native PHP functions
endef

define Package/php7-mod-onion-omega/install
	$(INSTALL_DIR) $(1)/usr/lib/php
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(MAKE_PATH)/modules/omega.so $(1)/usr/lib/php/
	$(INSTALL_DIR) $(1)/etc/php7
	echo "extension=omega.so" > $(1)/etc/php7/omega.ini
endef

$(eval $(call BuildPackage,php7-mod-onion-omega))