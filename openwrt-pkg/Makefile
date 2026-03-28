include $(TOPDIR)/rules.mk

PKG_NAME:=sqm-scripts-nft
PKG_VERSION:=1.0.0
PKG_RELEASE:=2

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/sqm-scripts-nft
  SECTION:=net
  CATEGORY:=Network
  TITLE:=SQM Scripts (Pure nftables)
  DEPENDS:=+tc +kmod-sched-cake +nftables +kmod-ifb
  PKGARCH:=all
endef

define Package/sqm-scripts-nft/description
  A pure nftables implementation of SQM scripts for OpenWrt.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)

	cp -r $(TOPDIR)/package/sqm-scripts-nft/src $(PKG_BUILD_DIR)/
	cp -r $(TOPDIR)/package/sqm-scripts-nft/platform $(PKG_BUILD_DIR)/
	cp $(TOPDIR)/package/sqm-scripts-nft/Makefile.main $(PKG_BUILD_DIR)/Makefile

endef

define Build/Compile
	# Nothing to compile for shell scripts
endef

define Package/sqm-scripts-nft/install
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR=$(1) PLATFORM=openwrt install
endef

$(eval $(call BuildPackage,sqm-scripts-nft))
