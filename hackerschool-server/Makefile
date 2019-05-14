include $(TOPDIR)/rules.mk
PKG_NAME:=hackerschool-server
PKG_VERSION:=1.4.3d
PKG_RELEASE:=0


PKG_SOURCE:=hucon.run
PKG_SOURCE_URL:=http://github.com/JonasTrampe/hackerschool/releases/download/$(PKG_VERSION)/
PKG_HASH:=e4648b8cdcc4800858635a1ef7550d877bef0a8959d7ea03c397c90de3bee92d
#PKG_SOURCE_SUBDIR:=$(PKG_NAME)
#PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

# base hackerschool package
define Package/$(PKG_NAME)
	SECTION:=hackerschool
	CATEGORY:=Hackerschool
	SUBMENU:=hackerschool
	TITLE:=Hucon-Robot Webserver
	DEPENDS:=+python-flask
endef


define Package/$(PKG_NAME)/description
Hucon-Robot Webserver
endef

UNPACK_CMD:=$(CP) $(DL_DIR)/$(PKG_SOURCE) $(PKG_BUILD_DIR)

define Package/$(PKG_NAME)/prepare
        (cd $(PKG_BUILD_DIR))
endef

define Build/Compile
        chmod +x $(PKG_BUILD_DIR)/hucon.run
	mkdir -p $(PKG_BUILD_DIR)/opt/hucon
	mkdir -p $(PKG_BUILD_DIR)/etc/init.d
	mkdir -p $(PKG_BUILD_DIR)/usr/lib/python2.7/site-packages/
	$(PKG_BUILD_DIR)/hucon.run $(PKG_BUILD_DIR)/opt/hucon
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/opt/hucon 
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./init.d/* $(1)/etc/init.d/
	$(CP) -r ./opt/hucon/__version__ ./opt/hucon/README.md ./opt/hucon/code/ ./opt/hucon/python_lib/ ./opt/hucon/webserver/ ./opt/hucon/i2c_led.sh ./opt/hucon/install.sh ./opt/hucon/start_server.sh ./opt/hucon/uninstall.sh ./opt/hucon/update.sh $(1)/opt/hucon
endef

define Package/$(PKG_NAME)/postinst
#!/bin/sh
# check if we are on real system
if [ -z "$${IPKG_INSTROOT}" ]; then
fi
exit 0
endef





# calls to build each package
$(eval $(call BuildPackage,$(PKG_NAME)))

