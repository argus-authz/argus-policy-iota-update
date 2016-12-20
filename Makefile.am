#
# Copyright 2016- Stichting Fundamenteel Onderzoek der Materie (FOM-Nikhef)
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Authors:
#      Mischa Salle
#      NIKHEF Amsterdam, the Netherlands
#      grid-mw-security-support@nikhef.nl

# Install script in sbin
sbin_SCRIPTS = argus-policy-iota-update

# Config file and conf.d type directory
dist_sysconf_DATA = argus-policy-iota-update.conf
confdir = $(sysconfdir)/argus-policy-iota-update.d

# Documentation
docdir = $(datadir)/doc/@PACKAGE@-@VERSION@
dist_doc_DATA = \
	README.md \
	AUTHORS \
	LICENSE \
	argus-policy-iota-update.d_example \
	example_policy_before \
	example_policy_after

# Man pages, set mandir
mandir = $(datadir)/man
man_MANS = argus-policy-iota-update.8 argus-policy-iota-update.conf.5

# Script and man page are created from template
argus-policy-iota-update: argus-policy-iota-update.src
	$(edit) $< > $@

argus-policy-iota-update.8: argus-policy-iota-update.8.src
	$(edit) $< > $@

argus-policy-iota-update.conf.5: argus-policy-iota-update.conf.5.src
	$(edit) $< > $@

# Make sure created files are cleaned
CLEANFILES = $(man_MANS) $(sbin_SCRIPTS)

# Also ship sources and bootstrap
EXTRA_DIST = \
	bootstrap \
	argus-policy-iota-update.src \
	argus-policy-iota-update.8.src \
	argus-policy-iota-update.conf.5.src

# Need hooks for creating the conf.d directory
install-data-hook:
	$(MKDIR_P) $(DESTDIR)$(confdir)

uninstall-hook:
	rmdir $(DESTDIR)$(confdir)


edit = sed \
        -e 's|@sysconfdir[@]|$(sysconfdir)|g' \
	-e 's|@PACKAGE_NAME[@]|$(PACKAGE_NAME)|g' \
        -e 's|@PACKAGE[@]|$(PACKAGE)|g' \
        -e 's|@VERSION[@]|$(VERSION)|g'
