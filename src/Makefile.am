AM_CFLAGS = -Wall -Wextra -std=c99 -pedantic -Wno-unused-parameter \
-fstrict-aliasing -Wno-missing-field-initializers @GTK_CFLAGS@ @libdbus_CFLAGS@

bin_PROGRAMS = artha

noinst_LIBRARIES = libwni.a
libwni_a_SOURCES = wni.c wni.h

artha_DEPENDENCIES = libwni.a
artha_SOURCES = mod_notify.c mod_notify.h \
		suggestions.c suggestions.h \
		hotkey_editor.c hotkey_editor.h \
		gui.c gui.h addons.h

if POSIX
artha_SOURCES += eggaccelerators.c eggaccelerators.h \
		tomboyutil.c tomboyutil.h instance_handler.c instance_handler.h
else
artha_SOURCES += app_icon.rc
lib_LTLIBRARIES = libnotify.la
libnotify_la_SOURCES = libnotify.c
libnotify_la_CFLAGS = -Wall -Wextra -pedantic -std=c99 \
	-s -Wno-unused-parameter -fstrict-aliasing \
	-Wno-missing-field-initializers @GTK_CFLAGS@ \
	-O2 -DWIN32 -DWINDOWS -DNDEBUG -D_USERDLL -D_WINDLL \
	-D_UNICODE -DUNICODE -DLIBNOTIFY_EXPORTS
libnotify_la_LDFLAGS = -mms-bitfields -mwindows \
	-version-info @dll_ver@ -no-undefined -Xlinker \
	libnotify_ver.o
libnotify_la_DEPENDENCIES = libnotify_ver.o
include_HEADERS = libnotify.h
endif

# @GTK_LIBS@ & libdbus_CFLAGS are not used to avoid unwanted 
# libraries (like -latk, -lrt, etc.) passed to the linker
artha_LDADD = libwni.a $(WORDNET_LIB)

if POSIX
artha_LDADD += -lX11 -ldbus-1 -ldbus-glib-1 -lgtk-x11-2.0 \
		-lgdk-x11-2.0 -lgmodule-2.0 -lgobject-2.0 -lglib-2.0
else
artha_LDADD += @GTK_LIBS@
artha_LDFLAGS = -mms-bitfields -mwindows
endif

.rc.o:
	windres -i $< -o $@ -I$(top_builddir)
