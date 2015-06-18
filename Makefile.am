ACLOCAL_AMFLAGS = -I m4 ${ACLOCAL_FLAGS}

NULL=

SUBDIRS=sde-session-manager sde-logout po

imagedir=$(datadir)/sde-session-manager/images
image_DATA= \
	images/system-shutdown.png \
	images/system-log-out.png \
	images/gnome-session-hibernate.png \
	images/gnome-session-reboot.png \
	images/gnome-session-suspend.png \
	images/gnome-session-switch.png

scripts=     sde-lock-screen
bin_SCRIPTS= $(scripts)

EXTRA_DIST = \
	desktop.conf.example \
	$(scripts) \
	$(image_DATA) \
	$(NULL)
