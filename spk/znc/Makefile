SPK_NAME = znc
SPK_VERS = 1.8.2
SPK_REV = 21
SPK_ICON = src/znc.png
DSM_UI_DIR = app

DEPENDS = cross/$(SPK_NAME)
SPK_DEPENDS = "python310"

MAINTAINER = worstje
DESCRIPTION = Advanced IRC bouncer. An IRC bouncer is nothing more than an IRC proxy. ZNC will always be connected in your chat rooms, and will be the gateway between your clients, and your IRC servers. You can, for instance, consult messages while you were offline or hide your identity.
DESCRIPTION_FRE = Bouncer IRC avancé. Un bouncer IRC n\’est en fait qu\’un proxy IRC. ZNC restera connecté en permanence à vos salons de discussions et fera office de passerelle entre vos clients et vos serveurs IRC. Vous pourrez, par exemple, consultez des messages diffusés en votre absence ou masquer votre identité.
DESCRIPTION_SPN = IRC bouncer avanzado. Un IRC bouncer no es más que un proxy para IRC. ZNC estará siempre conectado a tus canales, y hará de puerta de enlace entre tus clientes y tus servidores IRC. Puedes, por ejemplo, consultar mensajes mientras estuviste desconectado o esconder tu identidad.
DISPLAY_NAME = ZNC
CHANGELOG = "1. Update OpenSSL to v1.1.1m.<br/>2. Now depends on Python 3.10<br/>3. Fix DSM 7 installer to preserve configuration files on updates."

STARTABLE = yes
HOMEPAGE = https://wiki.znc.in/
LICENSE  = Apache License 2.0

# Ensure C++11 compatibility
UNSUPPORTED_ARCHS = $(ARMv5_ARCHS) $(OLD_PPC_ARCHS)

include ../../mk/spksrc.archs.mk

ifeq ($(findstring $(ARCH),$(ARMv7_ARCHS) $(ARMv7L_ARCHS)),$(ARCH))
# bugfix for libicudata error, solution proposed by Steven R. Loomis
# in https://sourceforge.net/p/icu/mailman/message/36666855/
export LIBICU_DATA_PACKAGING_MODE=files
endif

WIZARDS_DIR = src/wizard
CONF_DIR = src/conf

# 'auto' reserved value grabs SPK_NAME
SERVICE_USER = auto
SERVICE_SETUP = src/service-setup.sh

# Service configuration
SERVICE_PORT = 8250
SERVICE_PORT_TITLE = ZNC(HTTP)

# Admin link
ADMIN_PORT = ${SERVICE_PORT}

POST_STRIP_TARGET = znc_extra_install

include ../../mk/spksrc.spk.mk

.PHONY: znc_extra_install
znc_extra_install:
	install -m 755 -d $(STAGING_DIR)/var/modules $(STAGING_DIR)/var/configs
	install -m 644 src/znc.conf $(STAGING_DIR)/var/configs/znc.conf
	install -m 644 src/oidentd.conf ${STAGING_DIR}/var/configs/oidentd.conf
	ln -sf /etc/ssl/certs $(STAGING_DIR)/certs
