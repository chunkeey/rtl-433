include $(TOPDIR)/rules.mk

PKG_NAME:=softoff
PKG_RELEASE=1
PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=Christian Lamparter <chunkeey@gmail.com>

include $(INCLUDE_DIR)/package.mk

define Package/softoff
	PKGARCH:=all
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=softoff utilities
	DEPENDS:=+busybox
endef

define Package/softoff/description
  the softoff package replaces the poweroff and reboot commands with scripts that
  utilize the sysupgrade code to perform a "softer" poweroff or reboot.
  it will try to close any running application, unmount any active partition as
  well as putting any connected HDD to standby (for shutdown).
  It allows embedded devices without a working poweroff method to become unavailable.
endef

define Build/Compile
        true
endef

define Package/softoff/postinst
	# When this package is built-in (=y), opkg's default postinst
	# in functions.sh default_postinst() will follow (cp does that)
	# the existing symlink of /sbin/poweroff and write the script
	# into /bin/busybox! This leads to a unuseable system.
	[ -L ./sbin/poweroff ] && rm ./sbin/poweroff
	[ -L ./sbin/reboot ] && rm ./sbin/reboot
	true
endef

define Package/softoff/install-overlay
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) ./files/softoff.sh	$(1)/sbin/poweroff
	$(INSTALL_BIN) ./files/softreboot.sh	$(1)/sbin/reboot
endef

$(eval $(call BuildPackage,softoff))
