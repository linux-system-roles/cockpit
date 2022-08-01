Changelog
=========

[1.3.0] - 2022-07-29
--------------------

### New Features

- Add customization of port (#67)

Introduce a `cockpit_port` variable which changes the default port 9090,
as per https://cockpit-project.org/guide/latest/listen.html#listen-systemd

This requires an extra step with SELinux: It only allows cockpit to own port
9090, so for any other port the user needs to adjust the policy first. As this
is outside of what the cockpit role ought to mess with, only document it and do
that in the tests.

Fixes #63

### Bug Fixes

- none

### Other Changes

- changelog_to_tag action - support other than "master" for the main branch name (#66)

- fix yamllint indentation issue

[1.2.5] - 2022-07-19
--------------------

### New Features

- none

### Bug Fixes

- none

### Other Changes

- make min_ansible_version a string in meta/main.yml (#60)

The Ansible developers say that `min_ansible_version` in meta/main.yml
must be a `string` value like `"2.9"`, not a `float` value like `2.9`.

- Add CHANGELOG.md (#61)

[1.2.4] - 2022-05-06
--------------------

### New Features

- none

### Bug Fixes

- none

### Other Changes

- bump tox-lsr version to 2.11.0; remove py37; add py310

[1.2.3] - 2022-04-19
--------------------

### New Features

- none

### Bug Fixes

- none

### Other Changes

- support gather\_facts: false; support setup-snapshot.yml
- bump tox-lsr version to 2.10.1
- Test "cockpit\_packages: full" scenario

[1.2.2] - 2022-01-20
--------------------

### New Features

- none

### Bug fixes

- Skip/undocument obsolete packages

### Other Changes

- none

[1.2.1] - 2022-01-10
--------------------

### New Features

- none

### Bug Fixes

- none

### Other Changes

- bump tox-lsr version to 2.8.3
- change recursive role symlink to individual role dir symlinks

[1.2.0] - 2021-11-23
--------------------

### New features

- Add option to use an existing certificate

### Bug Fixes

- none

### Other Changes

- update tox-lsr version to 2.8.0
- tests: Run cleanup on failures as well

[1.1.2] - 2021-11-08
--------------------

### New features

- Document how to generate a web server certificate, various small documentation improvements

### Bug fixes

- Don't restart cockpit.socket with cockpit\_started: no; check role options in integration test

### Other Changes

- update tox-lsr version to 2.7.1
- support python 39, ansible-core 2.12, ansible-plugin-scan
- tests: Run Ansible in verbose mode in GitHub workflow integration test
- Test certmonger-generated certificates directly in cockpit/ws-certs.d/
- Test certmonger-generated Cockpit certificates
- Enable the Extras repository on RHEL 7
- tests: Generate self-signed certificate for RHEL \>= 8
- tests: Run integration test in GitHub actions
- tests: Assert some assumptions about the default role behaviour
- Drop cockpit-dashboard from Debian's "full" list

[1.1.1] - 2021-09-21
--------------------

### New Features

- none

### Bug fixes

- Use {{ ansible\_managed | comment }} to fix multi-line ansible\_managed
- use apt-get install -y

### Other Changes

- use tox-lsr version 2.5.1

[1.1.0] - 2021-08-10
--------------------

### New features

- Raise supported Ansible version to 2.9

### Bug Fixes

- none

### Other Changes

- none

[1.0.0] - 2021-07-06
--------------------

### Initial Release
