include $(TOPDIR)/rules.mk

PKG_NAME:=rohc
PKG_VERSION:=1.6.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://rohc-lib.org/download/rohc-1.6.x/$(PKG_VERSION)/
PKG_MD5SUM:=78e9d34a06f29e94aaa455e2e890e8a4

PKG_MAINTAINER:=Audric Schiltknecht <storm+openwrt@chemicalstorm.org>

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/librohc/Default
	URL:=http://rohc-lib.org
endef

define Package/librohc/Default/description
The ROHC library provides an easy and robust way for applications to reduce their bandwidth usage on network links with limited capacity or expensive costs. Headers of network packets are compressed with the ROHC protocol and algorithms.
endef

define Package/librohc
$(call Package/librohc/Default)
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=RObust Header Compression (ROHC) library
endef

define Package/librohc/description
$(call Package/librohc/Default/description)
This package contains the ROHC library.
endef

define Package/rohc-sniffer
$(call Package/librohc/Default)
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+librohc +libpcap
	TITLE+=ROHC-based sniffer program
endef

define Package/rohc-sniffer/description
$(call Package/librohc/Default/description)
This package contains the ROHC-based sniffer.
endef

CONFIGURE_ARGS += \
    --enable-static=yes \
    --enable-app-sniffer

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/rohc* $(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/librohc_*.{a,so*} $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/rohc.pc $(1)/usr/lib/pkgconfig/
endef


define Package/librohc/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/librohc_*.so* $(1)/usr/lib/
endef

define Package/rohc-sniffer/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/* $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,librohc))
$(eval $(call BuildPackage,rohc-sniffer))
