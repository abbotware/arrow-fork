# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.

CLEANFILES =
DISTCLEANFILES =

EXTRA_DIST =					\
	meson.build

AM_CPPFLAGS =					\
	-I$(top_builddir)			\
	-I$(top_srcdir)

AM_CFLAGS =					\
	$(GLIB_CFLAGS)				\
	$(GARROW_CFLAGS)

# libarrow-glib
lib_LTLIBRARIES =				\
	libarrow-glib.la

libarrow_glib_la_CXXFLAGS =			\
	$(GLIB_CFLAGS)				\
	$(ARROW_CFLAGS)				\
	$(GARROW_CXXFLAGS)

libarrow_glib_la_LDFLAGS =			\
	-version-info $(LT_VERSION_INFO)	\
	-no-undefined

libarrow_glib_la_LIBADD =			\
	$(GLIB_LIBS)				\
	$(ARROW_LIBS)

libarrow_glib_la_headers =			\
	array.h					\
	array-builder.h				\
	arrow-glib.h				\
	basic-array.h				\
	basic-data-type.h			\
	buffer.h				\
	chunked-array.h				\
	codec.h					\
	composite-array.h			\
	composite-data-type.h			\
	data-type.h				\
	decimal128.h				\
	error.h					\
	field.h					\
	gobject-type.h				\
	record-batch.h				\
	schema.h				\
	table.h					\
	table-builder.h				\
	tensor.h				\
	type.h

libarrow_glib_la_headers +=			\
	file.h					\
	file-mode.h				\
	input-stream.h				\
	output-stream.h				\
	readable.h				\
	writable.h				\
	writable-file.h

libarrow_glib_la_headers +=			\
	metadata-version.h			\
	reader.h				\
	writer.h

libarrow_glib_la_headers +=			\
	compute.h

if HAVE_ARROW_ORC
libarrow_glib_la_headers +=			\
	orc-file-reader.h
endif

libarrow_glib_la_generated_headers =		\
	enums.h					\
	version.h

libarrow_glib_la_generated_sources =		\
	enums.c					\
	$(libarrow_glib_la_generated_headers)

libarrow_glib_la_sources =			\
	array-builder.cpp			\
	basic-array.cpp				\
	basic-data-type.cpp			\
	buffer.cpp				\
	chunked-array.cpp			\
	codec.cpp				\
	composite-array.cpp			\
	composite-data-type.cpp			\
	decimal128.cpp				\
	error.cpp				\
	field.cpp				\
	record-batch.cpp			\
	schema.cpp				\
	table.cpp				\
	table-builder.cpp			\
	tensor.cpp				\
	type.cpp				\
	$(libarrow_glib_la_headers)		\
	$(libarrow_glib_la_generated_sources)

libarrow_glib_la_sources +=			\
	file.cpp				\
	file-mode.cpp				\
	input-stream.cpp			\
	output-stream.cpp			\
	readable.cpp				\
	writable.cpp				\
	writable-file.cpp

libarrow_glib_la_sources +=			\
	metadata-version.cpp			\
	reader.cpp				\
	writer.cpp

libarrow_glib_la_sources +=			\
	compute.cpp

if HAVE_ARROW_ORC
libarrow_glib_la_sources +=			\
	orc-file-reader.cpp
endif

libarrow_glib_la_cpp_headers =			\
	array.hpp				\
	array-builder.hpp			\
	arrow-glib.hpp				\
	basic-array.hpp				\
	basic-data-type.hpp			\
	buffer.hpp				\
	chunked-array.hpp			\
	codec.hpp				\
	data-type.hpp				\
	decimal128.hpp				\
	error.hpp				\
	field.hpp				\
	record-batch.hpp			\
	schema.hpp				\
	table.hpp				\
	table-builder.hpp			\
	tensor.hpp				\
	type.hpp

libarrow_glib_la_cpp_headers +=			\
	file.hpp				\
	file-mode.hpp				\
	input-stream.hpp			\
	output-stream.hpp			\
	readable.hpp				\
	writable.hpp				\
	writable-file.hpp

libarrow_glib_la_cpp_headers +=			\
	metadata-version.hpp			\
	reader.hpp				\
	writer.hpp

libarrow_glib_la_cpp_headers +=			\
	compute.hpp

if HAVE_ARROW_ORC
libarrow_glib_la_cpp_headers +=			\
	orc-file-reader.hpp
endif

libarrow_glib_la_cpp_internal_headers =		\
	internal-index.hpp

libarrow_glib_la_SOURCES =			\
	$(libarrow_glib_la_sources)		\
	$(libarrow_glib_la_cpp_headers)		\
	$(libarrow_glib_la_cpp_internal_headers)

BUILT_SOURCES =					\
	$(libarrow_glib_la_generated_headers)	\
	$(libarrow_glib_la_generated_sources)	\
	stamp-enums.c				\
	stamp-enums.h

DISTCLEANFILES +=				\
	stamp-enums.c				\
	stamp-enums.h

EXTRA_DIST +=					\
	enums.c.template			\
	enums.h.template

enums.h: stamp-enums.h
	@true
stamp-enums.h: $(libarrow_glib_la_headers) enums.h.template
	$(AM_V_GEN)					\
	  (cd $(srcdir) &&				\
	   $(GLIB_MKENUMS)				\
	     --identifier-prefix GArrow			\
	     --symbol-prefix garrow			\
	     --template enums.h.template		\
	     $(libarrow_glib_la_headers)) > enums.h
	touch $@

enums.c: stamp-enums.c
	@true
stamp-enums.c: $(libarrow_glib_la_headers) enums.c.template
	$(AM_V_GEN)					\
	  (cd $(srcdir) &&				\
	   $(GLIB_MKENUMS)				\
	     --identifier-prefix GArrow			\
	     --symbol-prefix garrow			\
	     --template enums.c.template		\
	     $(libarrow_glib_la_headers)) > enums.c
	touch $@

arrow_glib_includedir = $(includedir)/arrow-glib
arrow_glib_include_HEADERS =			\
	$(libarrow_glib_la_headers)		\
	$(libarrow_glib_la_cpp_headers)		\
	$(libarrow_glib_la_generated_headers)

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA =				\
	arrow-glib.pc

if HAVE_ARROW_ORC
pkgconfig_DATA +=				\
	arrow-orc-glib.pc
endif

if HAVE_INTROSPECTION
-include $(INTROSPECTION_MAKEFILE)
INTROSPECTION_GIRS =
INTROSPECTION_SCANNER_ARGS =
INTROSPECTION_SCANNER_ENV =
INTROSPECTION_COMPILER_ARGS =

Arrow-1.0.gir: libarrow-glib.la
Arrow_1_0_gir_PACKAGES =			\
	gio-2.0
Arrow_1_0_gir_EXPORT_PACKAGES =			\
	arrow-glib
Arrow_1_0_gir_INCLUDES =			\
	Gio-2.0
Arrow_1_0_gir_CFLAGS =				\
	$(AM_CPPFLAGS)
Arrow_1_0_gir_LIBS =
Arrow_1_0_gir_FILES = $(libarrow_glib_la_sources)
Arrow_1_0_gir_SCANNERFLAGS =			\
	--library-path=$(ARROW_LIB_DIR)		\
	--warn-all				\
	--identifier-prefix=GArrow		\
	--symbol-prefix=garrow
if OS_MACOS
Arrow_1_0_gir_LIBS += arrow-glib
Arrow_1_0_gir_SCANNERFLAGS +=			\
	--no-libtool				\
	--library-path=$(abs_builddir)/.libs
else
Arrow_1_0_gir_LIBS += libarrow-glib.la
endif
INTROSPECTION_GIRS += Arrow-1.0.gir

girdir = $(datadir)/gir-1.0
gir_DATA = $(INTROSPECTION_GIRS)

typelibdir = $(libdir)/girepository-1.0
typelib_DATA = $(INTROSPECTION_GIRS:.gir=.typelib)

CLEANFILES +=					\
	$(gir_DATA)				\
	$(typelib_DATA)
endif
