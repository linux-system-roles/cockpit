Changelog
=========

[1.4.8] - 2023-09-08
--------------------

### Other Changes

- ci: Add markdownlint, test_converting_readme, and build_docs workflows (#118)

  - markdownlint runs against README.md to avoid any issues with
    converting it to HTML
  - test_converting_readme converts README.md > HTML and uploads this test
    artifact to ensure that conversion works fine
  - build_docs converts README.md > HTML and pushes the result to the
    docs branch to publish dosc to GitHub pages site.
  - Fix markdown issues in README.md
  
  Signed-off-by: Sergei Petrosian <spetrosi@redhat.com>

- docs: Make badges consistent, run markdownlint on all .md files (#119)

  - Consistently generate badges for GH workflows in README RHELPLAN-146921
  - Run markdownlint on all .md files
  - Add custom-woke-action if not used already
  - Rename woke action to Woke for a pretty badge
  
  Signed-off-by: Sergei Petrosian <spetrosi@redhat.com>

- ci: Remove badges from README.md prior to converting to HTML (#120)

  - Remove thematic break after badges
  - Remove badges from README.md prior to converting to HTML
  
  Signed-off-by: Sergei Petrosian <spetrosi@redhat.com>


[1.4.7] - 2023-07-19
--------------------

### Bug Fixes

- fix: facts being gathered unnecessarily (#116)

### Other Changes

- ci: Add pull request template and run commitlint on PR title only (#113)
- ci: Rename commitlint to PR title Lint, echo PR titles from env var (#114)
- ci: ansible-lint - ignore var-naming[no-role-prefix] (#115)

[1.4.6] - 2023-05-26
--------------------

### Other Changes

- docs: Consistent contributing.md for all roles - allow role specific contributing.md section
- docs: clean up collection requirements section

[1.4.5] - 2023-04-13
--------------------

### Other Changes

- additional ansible-lint fixes (#104)

[1.4.4] - 2023-04-06
--------------------

### Other Changes

- Add README-ansible.md to refer Ansible intro page on linux-system-roles.github.io (#101)
- Fingerprint RHEL System Role managed config files (#102)

[1.4.3] - 2023-01-20
--------------------

### New Features

- none

### Bug Fixes

- ansible-lint 6.x fixes

### Other Changes

- Add check for non-inclusive language
- cleanup non-inclusive words.

[1.4.2] - 2022-11-21
--------------------

### New Features

- none

### Bug Fixes

- ansible-core 2.14 support - remove another warn

### Other Changes

- use fedora.linux_system_roles.certificate role in tests

The dependencies will be installed everywhere, so just use them
in the tests

[1.4.1] - 2022-11-15
--------------------

### New Features

- none

### Bug Fixes

- make role work with ansible-core 2.14 - fix ansible-lint 6.x issues (#81)

### Other Changes

- none

[1.4.0] - 2022-11-01
--------------------

### New Features

- Use the firewall role and the selinux role from the cockpit role (#76)

Since cockpit_port is a public api of the cockpit role, define it
in defaults/main.yml as null.

- Introduce cockpit_manage_firewall to use the firewall role to
  manage the cockpit service.
  Default to false - means the firewall role is not used.

- Add the test check task tasks/check_port.yml for verifying the
  ports status.

- Add meta/collection-requirements.yml.

- Introduce cockpit_manage_selinux to use the selinux role to
  manage the ports in the cockpit service.
  Assign websm_port_t to the cockpit service ports.
  Default to false - means the selinux role is not used.

- Use the certificate role to create the cert and the key (#78)

- Introduce a variable cockpit_certificates to set the certificate_requests.

- Update README so that using the certificate role is recommended.

Add a check and README note for not supporting creating a self-signed
certificate on RHEL/CentOS-7.

### Bug Fixes

- none

### Other Changes

- workflows: Add integration-tests for Ubuntu 22.04 (#68)

The current LTS 22.04 is the more interesting target. This detects bugs
like [1]. Keep 20.04 running as well for the time being.

[1] https://github.com/linux-system-roles/certificate/pull/130

- Clone the certificate role in the temporary dir. (#77)

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

- changelog_to_tag action - github action ansible test improvements

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
