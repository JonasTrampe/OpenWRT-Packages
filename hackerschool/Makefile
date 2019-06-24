include $(TOPDIR)/rules.mk
PKG_NAME:=hackerschool
PKG_VERSION:=1.4.3d
PKG_RELEASE:=0


PKG_SOURCE:=hucon.run
PKG_SOURCE_URL:=https://github.com/JonasTrampe/hackerschool/releases/download/$(PKG_VERSION)/
PKG_HASH:=18eb398b04d4529c27fb48b837d8271f2fea1ad495ac5d37cba3c6f4edadf0e6

PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

# base hackerschool package
define Package/hackerschool-server
	SECTION:=hackerschool
	CATEGORY:=Hackerschool
	SUBMENU:=hackerschool
	TITLE:=Hucon-Robot Webserver
	DEPENDS:=+python-flask
endef


define Package/hackerschool-server/description
Hucon-Robot Webserver
endef

define Host/Compile
	$(PKG_BUILD_DIR)/deploy.sh ./opt/hucon
endef

define Package/hackerschool-server/install
	$(INSTALL_DIR) $(1)/opt/hucon 
	$(INSTALL_DIR) $(1)/etc/init.d
	$(CP) ./init.d/* $(1)/etc/init.d/
	$(CP) -r ./opt/hucon/__version__ ./opt/hucon/README.md ./opt/hucon/code/ ./opt/hucon/python_lib/ ./opt/hucon/webserver/ ./opt/hucon/i2c_led.sh ./opt/hucon/install.sh ./opt/hucon/start_server.sh ./opt/hucon/uninstall.sh ./opt/hucon/update.sh $(1)/opt/hucon
endef

define Package/hackerschool-server/postinst
#!/bin/sh
# check if we are on real system
if [ -z "$${IPKG_INSTROOT}" ]; then
	/etc/init.d/rpcd restart
fi
exit 0
endef





# calls to build each package
$(eval $(call BuildPackage,hackerschool-server))

