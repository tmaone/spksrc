PKG_NAME = fish
PKG_VERS = nightly
PKG_EXT = tar.gz
PKG_DOWNLOAD_METHOD = git
PKG_DIST_SITE = https://github.com/fish-shell/fish-shell.git
PKG_DIST_FILE = $(PKG_NAME)-git.$(PKG_EXT)
PKG_DIR = $(PKG_NAME)-git

UNSUPPORTED_ARCHS = $(ARM_ARCHES) $(PPC_ARCHES) $(x86_ARCHES)

DEPENDS = cross/ncurses

HOMEPAGE = http://fishshell.com
COMMENT  = fish is a smart and user-friendly command line shell for OS X, Linux, and the rest of the family.
LICENSE  = GPLv2

GNU_CONFIGURE = 1
PRE_CONFIGURE_TARGET = customautoconf
CONFIGURE_TARGET = customconfigure
INSTALL_TARGET = custominstall

# ENV += TC_CONFIGURE_ARGS=""
# CONFIGURE_ARGS  = --prefix=$(INSTALL_PREFIX)
# TC_CONFIGURE_ARGS = --host=$(TC_TARGET) --build=$(TC_TARGET)

include ../../mk/spksrc.cross-cc.mk

.PHONY: customautoconf
customautoconf: configure_msg
	$(RUN) autoconf
	cp patches/fallback.cpp $(WORK_DIR)/$(PKG_DIR)/src/fallback.cpp
	$(RUN) rm -rf $(WORK_DIR)/$(PKG_DIR)/autom4te.cache
	cp patches/configure $(WORK_DIR)/$(PKG_DIR)/configure
	cp patches/configure-pcre $(WORK_DIR)/$(PKG_DIR)/pcre2-10.20/configure
	# cp patches/configure.ac $(WORK_DIR)/$(PKG_DIR)/configure.ac

.PHONY: customautoconf
customconfigure: $(PRE_CONFIGURE_TARGET)
	$(RUN) ./configure cross_compiling=no ac_cv_sizeof_wchar_t=4 --prefix=$(INSTALL_PREFIX) --build=x86_64-unknown-linux-gnu --host=x86_64-unknown-linux-gnu
	# --host=x86_64-unknown-linux-gnu
	# $(RUN) ./configure --prefix=$(INSTALL_PREFIX) --help
# --host=$(TC_TARGET) --build=$(TC_TARGET) --target=$(TC_TARGET)

.PHONY: custominstall
custominstall:
	$(RUN) make install DESTDIR=$(INSTALL_DIR)





	# CONFIGURE_ARGS = --prefix=$(INSTALL_PREFIX) -I$(INSTALL_PREFIX)include
