lib_LTLIBRARIES = libsavan_subs_mgr.la

libsavan_subs_mgr_la_SOURCES = subs_mgr.c sqlite3.c

libsavan_subs_mgr_la_LIBADD = ../../../../axis2c/src/core/engine/libaxis2_engine.la \
                          ../../../../axis2c/util/src/libaxutil.la \
                          ../../../../axis2c/axiom/src/om/libaxis2_axiom.la \
			  ../../subscribers/libsavan_subscribers.la \
			  ../../util/libsavan_util.la \
                          ../common/libsavan_common_subs_mgr.la

INCLUDES = -I$(top_builddir)/include \
			-I$(top_builddir)/include/savan \
			-I. \
			@AXIS2INC@ \
		   	@AXIOMINC@ \
		   	@NEETHIINC@ \
		   	@UTILINC@

EXTRA_DIST=
