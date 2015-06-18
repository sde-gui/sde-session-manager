NULL=

bin_PROGRAMS = sde-session-manager

sde_session_manager_CFLAGS = $(GLIB_CFLAGS) $(X11_CFLAGS) \
				$(ADDITIONAL_FLAGS) \
				-DPACKAGE_LOCALE_DIR=\""$(prefix)/$(DATADIRNAME)/locale"\" \
				-Werror-implicit-function-declaration \
				$(NULL)

sde_session_manager_LDADD = $(GLIB_LIBS) $(X11_LIBS)

sde_session_manager_SOURCES = \
	sde-session-manager.c \
	sde-session-manager.h \
	xdg-autostart.c \
	xdg-autostart.h \
	xevent.c \
	xevent.h \
	settings-daemon.c \
	settings-daemon.h \
	xsettings-common.h \
	xsettings-common.c \
	xsettings-manager.h \
	xsettings-manager.c \
	xutils.h \
	xutils.c \
	$(NULL)
