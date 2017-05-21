#
# Copyright (C) 2016-2017 Kea
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=php7-mod-onion-omega
PKG_VERSION:=0.2.0
PKG_RELEASE:=1

PKG_MAINTAINER:=Manuel Kea Baldassarri <manuel@baldassarri.me>

PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=LICENSE-GPLv2

PKG_SOURCE:=v$(PKG_VERSION).zip
PKG_BUILD_DIR:=$(BUILD_DIR)/Onion-Omega-Php-extension-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/kea/Onion-Omega-Php-extension/archive/
PKG_MD5SUM:=f408d272b4825ce921c2306fa4bc3af1

PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(INCLUDE_DIR)/autotools.mk

define Build/Prepare
	$(Build/Prepare/Default)
	( cd $(PKG_BUILD_DIR)/$(MAKE_PATH); $(STAGING_DIR)/usr/bin/phpize7; rm -f aclocal.m4 )
	$(autoreconf_target)
endef

CONFIGURE_VARS+= \
        ac_cv_c_bigendian_php=$(if $(CONFIG_BIG_ENDIAN),yes,no)

CONFIGURE_VARS+= \
	OMEGA_DIR=$(STAGING_DIR)/usr/

CONFIGURE_ARGS+= \
	--with-php-config=$(STAGING_DIR)/usr/bin/php7-config

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