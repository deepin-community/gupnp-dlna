ACLOCAL_AMFLAGS = -I m4 ${ACLOCAL_FLAGS}

SUBDIRS = libgupnp-dlna tools tests data doc vala

pkgconfig_DATA = gupnp-dlna-2.0.pc gupnp-dlna-metadata-2.0.pc
pkgconfigdir = $(libdir)/pkgconfig

if GSTREAMER_METADATA_BACKEND_ENABLED
pkgconfig_DATA += gupnp-dlna-gst-2.0.pc
endif

if GSTREAMER_LEGACY_METADATA_BACKEND_ENABLED
pkgconfig_DATA += gupnp-dlna-gst-legacy-2.0.pc
endif

DISTCHECK_CONFIGURE_FLAGS = --enable-gtk-doc --enable-introspection

# Extra clean files so that maintainer-clean removes *everything*
MAINTAINERCLEANFILES = aclocal.m4 compile config.guess config.sub configure depcomp install-sh ltmain.sh Makefile.in missing config.h.in

dist-hook:
	@if test -d "$(srcdir)/.git"; \
	then \
		echo Creating ChangeLog && \
		( cd "$(top_srcdir)" && \
		  echo '# Generated by Makefile. Do not edit.'; echo; \
		  $(top_srcdir)/build-aux missing --run git log --stat ) > ChangeLog.tmp \
		&& mv -f ChangeLog.tmp $(top_distdir)/ChangeLog \
		|| ( rm -f ChangeLog.tmp ; \
		     echo Failed to generate ChangeLog >&2 ); \
	else \
		echo A git clone is required to generate a ChangeLog >&2; \
	fi
