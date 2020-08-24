.PHONY: debian rpm

ACLOCAL_AMFLAGS = -I m4
#SUBDIRS = doc etc

script_files = atool
script_stamp_files = $(script_files:%=.%-stamp)
script_old_files = $(script_files:%=.%-old)

man_MANS = $(PACKAGE).1

EXTRA_DIST = $(script_files) extra debian/changelog debian/control debian/copyright debian/rules $(man_MANS)
DISTCLEANFILES = $(script_stamp_files)
MAINTAINERCLEANFILES = $(script_old_files)

dist_bin_SCRIPTS = $(script_files)

$(script_stamp_files): .%-stamp: % $(srcdir)/configure.ac
	touch `basename "$<"`
	sed "1s|[^ ]*|$(PERL_SHEBANG)|;/^\\$$::SYSCONFDIR = /s|'.*'|'$(SYSCONFDIR)'|;/^\\$$::PACKAGE = /s/'.*'/'$(PACKAGE)'/;/^\\$$::VERSION = /s/'.*'/'$(PACKAGE_VERSION)'/;/^\\$$::BUG_EMAIL = /s/'.*'/'$(PACKAGE_BUGREPORT)'/" < $< > `basename $<.tmp` \
	  && mv `basename "$<"` .`basename "$<-old"` \
	  && mv `basename "$<.tmp"` `basename "$<"`
	chmod a+x `basename "$<"`
	touch $@

all-local: $(script_stamp_files)

debian:
	cd $(srcdir) && dpkg-buildpackage -rfakeroot -us -uc -sd -b
        
rpm: $(PACKAGE).spec
	rpmbuild -ba --clean $<

install-exec-local:
	mkdir -p $(DESTDIR)$(bindir)
	mkdir -p $(DESTDIR)$(mandir)/man1
	for f in aunpack arepack apack acat als adiff; do \
	  ln -s -f atool $(DESTDIR)$(bindir)/$$f; \
	  ln -s -f atool.1 $(DESTDIR)$(mandir)/man1/$$f.1; \
	done

uninstall-local:
	for f in aunpack arepack apack acat als adiff; do \
	  if [ -L $(DESTDIR)$(bindir)/$$f ]; then \
	    rm $(DESTDIR)$(bindir)/$$f; \
	  fi; \
	  if [ -L $(DESTDIR)$(mandir)/man1/$$f.1 ]; then \
	    rm $(DESTDIR)$(mandir)/man1/$$f.1; \
	  fi; \
	done
