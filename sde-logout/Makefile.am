bin_PROGRAMS = sde-logout

sde_logout_CFLAGS =  $(GTK_CFLAGS) $(SM_CFLAGS) $(DBUS_CFLAGS) \
			$(ADDITIONAL_FLAGS) \
			-DPACKAGE_LOCALE_DIR=\"$(datadir)/locale\" \
			-DPACKAGE_DATA_DIR=\"$(datadir)\"

sde_logout_LDADD = $(GTK_LIBS) $(SM_LIBS) $(DBUS_LIBS) $(X11_LIBS)

sde_logout_SOURCES= \
	dbus-interface.c \
	dbus-interface.h \
	sde-logout.c
