include $(TOPDIR)/rules.mk

PKG_NAME:=fossil
PKG_VERSION:=1.22
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-src-20120317175325

PKG_SOURCE:=$(PKG_NAME)-src-20120317175325.tar.gz
PKG_SOURCE_URL:=http://www.fossil-scm.org/download/
PKG_MD5SUM:=a7106450722e8477972d230fa535702f

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/fossil
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Version Control Systems
  TITLE:=Simple, high-reliability, distributed SCM
  URL:=http://fossil-scm.org
  MAINTAINER:=Eduardo Tongson <propolice@gmail.com>
  DEPENDS:=+zlib
endef

define Package/fossil/description
  Fossil is a distributed version control system, bug tracking system 
  and wiki software server for use in software development.
endef

MAKE_FLAGS := \
	TCC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS) -I$(STAGING_DIR)/usr/include -DFOSSIL_ENABLE_JSON" \
	LDFLAGS="$(TARGET_LDFLAGS) -Wl,-rpath=$(TOOLCHAIN_DIR)/lib -L$(STAGING_DIR)/lib -L$(STAGING_DIR)/usr/lib" \
        
undefine Build/Configure

define Build/Compile
	$(call Build/Compile/Default, \
	-f Makefile.classic $(MAKE_FLAGS) \
        all)
endef

undefine Build/Install

define Package/fossil/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/config
	$(CP) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/usr/bin/
	$(CP) ./fossil $(1)/etc/init.d/fossil
	$(CP) ./fossil.config $(1)/etc/config/fossil
endef

$(eval $(call BuildPackage,fossil))
