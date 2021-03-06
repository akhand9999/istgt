## Copyright © 2018 The OpenEBS Authors
## 
## Licensed under the Apache License, Version 2.0 (the "License");
## you may not use this file except in compliance with the License.
## You may obtain a copy of the License at
## 
##     http://www.apache.org/licenses/LICENSE-2.0
## 
## Unless required by applicable law or agreed to in writing, software
## distributed under the License is distributed on an "AS IS" BASIS,
## WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
## See the License for the specific language governing permissions and
## limitations under the License.

# for doc

top_srcdir = ..
srcdir   = .

prefix   = /usr/local
exec_prefix = ${prefix}
bindir   = ${exec_prefix}/bin
sbindir  = ${exec_prefix}/sbin
sysconfdir = ${prefix}/etc
datarootdir = ${prefix}/share
datadir  = ${datarootdir}
libexecdir = ${exec_prefix}/libexec
mandir   = ${datarootdir}/man

configdir = /usr/local/etc/istgt
mediadir = /var/istgt

SED      = /bin/sed
INSTALL  = /usr/bin/install -c
MKDIR_P  = /bin/mkdir -p

source   = 
header   = 
document = QUICKSTART QUICKSTART.jp istgt.1.in
sample   = 

DISTDIR = $(top_srcdir)/`cat $(top_srcdir)/distdir`
DISTFILES = Makefile.in \
	$(header) $(source) \
	$(document) $(sample)

#########################################################################

.PHONY: all install install-doc install-dirs install-doc-dirs
all: istgt.1

istgt.1:
	$(SED) -e 's:%%PREFIX%%:$(prefix):g' \
		-e 's:%%CONFIGDIR%%:$(configdir):g' \
		-e 's:%%MEDIADIR%%:$(mediadir):g' < istgt.1.in > $@

dist: $(DISTFILES)
	$(MKDIR_P) $(DISTDIR)/$(subdir)
	cd $(srcdir); thisdir=`pwd`; \
	for file in $(DISTFILES); do \
	    cp -p $$thisdir/$$file $(DISTDIR)/$(subdir); \
	done

install: install-dirs
	$(INSTALL) -m 0644 istgt.1 $(DESTDIR)$(mandir)/man1/
	-rm -f $(DESTDIR)$(mandir)/man1/istgt.1.gz
	gzip -9 $(DESTDIR)$(mandir)/man1/istgt.1

install-doc: install-doc-dirs
	$(INSTALL) -m 0644 $(top_srcdir)/README $(DESTDIR)$(datadir)/doc/istgt/
	$(INSTALL) -m 0644 $(top_srcdir)/ChangeLog.jp $(DESTDIR)$(datadir)/doc/istgt/
	$(INSTALL) -m 0644 QUICKSTART $(DESTDIR)$(datadir)/doc/istgt/
	$(INSTALL) -m 0644 QUICKSTART.jp $(DESTDIR)$(datadir)/doc/istgt/

install-dirs:
	$(MKDIR_P) $(DESTDIR)$(mandir)/man1

install-doc-dirs:
	$(MKDIR_P) $(DESTDIR)$(datadir)/doc/istgt

.PHONY: clean distclean depend
clean:
	-rm -f istgt.1
	-rm -f a.out *.o *.core
	-rm -f *~

distclean: clean
	-rm -f Makefile config.status config.cache config.log config.h

depend:

#########################################################################
