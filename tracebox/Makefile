include $(TOPDIR)/rules.mk

PKG_NAME:=tracebox
PKG_VERSION:=0.4.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=git@github.com:tracebox/tracebox.git
PKG_MAINTAINER:=Gregory Detal <gregory.detal@uclouvain.be>

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v0.4.4

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/tracebox
  SECTION:=net
  CATEGORY:=Network
  TITLE:=tracebox
  DEPENDS:=+liblua +libpcap +libpthread +librt +curl +libjson-c +libnetfilter-queue +libstdcpp
endef

define Package/tracebox/description
  Tracebox is a tool that allows to detect middleboxes on any paths, i.e.,
between a source and any destination. Tracebox can be viewed as a tool similar
to traceroute as it uses ICMP replies to identify changes in the packets.
endef

CONFIGURE_VARS += \
	ac_cv_header_lua_h=no \
	ax_header_version_match=yes

CONFIGURE_ARGS += \
	--enable-sniffer --enable-curl --with-libpcap="$(STAGING_DIR)/usr/include/"

EXTRA_CPPFLAGS += \
	-fpermissive -Wno-variadic-macros

TARGET_CFLAGS += \
	-D_GNU_SOURCE

define Package/tracebox/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/tracebox/tracebox $(1)/usr/sbin/tracebox
endef

$(eval $(call BuildPackage,tracebox))
