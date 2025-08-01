Changelog
=========

[1.7.1] - 2025-08-01
--------------------

### Other Changes

- test: Use post quantum encryption where available (#229)

[1.7.0] - 2025-07-02
--------------------

### New Features

- feat: add sles 16 support (#227)

### Other Changes

- refactor: fix ansible-lint indentation (#226)

[1.6.1] - 2025-06-16
--------------------

### Other Changes

- tests: Fix check_port.yml invocation, check permanent firewall configuration (#219)
- tests: Enable firewall management tests in container builds (#222)
- tests: Update tests_port to do bootc end-to-end validation (#223)
- ci: Use ansible 2.19 for fedora 42 testing; support python 3.13 (#224)

[1.6.0] - 2025-05-21
--------------------

### New Features

- feat: Support this role in container builds (#212)

### Bug Fixes

- fix: Ignore extra lines in dnf repoquery parsing (#214)
- fix: Consider "degraded" systemd state as booted (#217)

### Other Changes

- ci: Update to tox-lsr 3.7.0 (#213)
- ci: bump sclorg/testing-farm-as-github-action from 3 to 4 (#215)
- ci: bump tox-lsr to 3.8.0; rename qemu/kvm tests (#216)
- ci: Add Fedora 42; use tox-lsr 3.9.0; use lsr-report-errors for qemu tests (#218)

[1.5.16] - 2025-04-23
--------------------

### Bug Fixes

- fix: Ignore cockpit-pcp on RedHat 9 (#204)
- fix: Run Fedora 42 with dnf instead of default setup (#205)
- fix: Dynamically ignore cockpit-pcp (#206)

### Other Changes

- ci: Check spelling with codespell (#196)
- ci: Add test plan that runs CI tests and customize it for each role (#197)
- ci: In test plans, prefix all relate variables with SR_ (#198)
- ci: Fix bug with ARTIFACTS_URL after prefixing with SR_ (#199)
- test: Remove all cockpit packages in cleanup (#201)
- ci: Remove EOL ubuntu-20.04 runner, add 24.04 (#207)
- ci: several changes related to new qemu test, ansible-lint, python versions, ubuntu versions (#208)
- ci: use tox-lsr 3.6.0; improve qemu test logging (#209)
- ci: skip storage scsi, nvme tests in github qemu ci (#210)

[1.5.15] - 2025-02-03
--------------------

### Other Changes

- ci: ansible-plugin-scan is disabled for now (#190)
- ci: bump ansible-lint to v25; provide collection requirements for ansible-lint (#193)
- test: cockpit-composer is deprecated, so use storaged for test (#194)

[1.5.14] - 2024-12-13
--------------------

### Other Changes

- ci: Use Fedora 41, drop Fedora 39 (#185)
- ci: Use Fedora 41, drop Fedora 39 - part two (#186)
- test: Drop cockpit-ws* groups (#187)

[1.5.13] - 2024-11-20
--------------------

### Other Changes

- test: full test uses cockpit-composer or cockpit-machines (#183)

[1.5.12] - 2024-11-19
--------------------

### Other Changes

- test: cockpit-pcp is deprecated - use cockpit-machines (#181)

[1.5.11] - 2024-10-30
--------------------

### Other Changes

- ci: Add tags to TF workflow, allow more [citest bad] formats (#175)
- ci: ansible-test action now requires ansible-core version (#176)
- ci: add YAML header to github action workflow files (#177)
- refactor: Use vars/RedHat_N.yml symlink for CentOS, Rocky, Alma wherever possible (#179)

[1.5.10] - 2024-08-21
--------------------

### Other Changes

- ci: Add tft plan and workflow (#167)
- ci: Update fmf plan to add a separate job to prepare managed nodes (#169)
- ci: Bump sclorg/testing-farm-as-github-action from 2 to 3 (#170)
- ci: Add workflow for ci_test bad, use remote fmf plan (#171)
- ci: Fix missing slash in ARTIFACTS_URL (#172)
- test: skip check for excluded packages on ostree (#173)

[1.5.9] - 2024-07-23
--------------------

### Other Changes

- ci: Handle reboot for transactional update systems (#165)

[1.5.8] - 2024-07-02
--------------------

### Bug Fixes

- fix: wildcard package installation not working with dnf module (#161)
- fix: add support for EL10 (#163)

### Other Changes

- test: find cockpit test group dynamically (#160)
- ci: ansible-lint action now requires absolute directory (#162)

[1.5.7] - 2024-06-11
--------------------

### Other Changes

- ci: use tox-lsr 3.3.0 which uses ansible-test 2.17 (#155)
- ci: tox-lsr 3.4.0 - fix py27 tests; move other checks to py310 (#157)
- ci: Add supported_ansible_also to .ansible-lint (#158)

[1.5.6] - 2024-04-04
--------------------

### Other Changes

- ci: Bump ansible/ansible-lint from 6 to 24 (#152)
- ci: Bump mathieudutour/github-tag-action from 6.1 to 6.2 (#153)

[1.5.5] - 2024-02-26
--------------------

### Other Changes

- test: Ensure cleanup and proper service state on ostree (#150)

[1.5.4] - 2024-02-14
--------------------

### Other Changes

- ci: fix python unit test - copy pytest config to tests/unit (#147)
- test: Add python_version to test facts gather ansible_python_version (#148)

[1.5.3] - 2024-01-23
--------------------

### Other Changes

- ci: Remove redundant task (#145)

[1.5.2] - 2024-01-16
--------------------

### Other Changes

- ci: Fix implicit octal values (#139)
- ci: Use supported ansible-lint action; run ansible-lint against the collection (#140)
- ci: Add ALP-Dolomite var file (#141)
- ci: Use supported ansible-lint action; run ansible-lint against the collection (#142)
- ci: Add check for Cockpit package installation status in reboot condition (#143)

[1.5.1] - 2023-12-08
--------------------

### Other Changes

- ci: bump actions/github-script from 6 to 7 (#136)
- refactor: get_ostree_data.sh use env shebang - remove from .sanity* (#137)

[1.5.0] - 2023-11-29
--------------------

### New Features

- feat: support for ostree systems (#133)

### Other Changes

- docs: Use FQCN for scenarios that use other linux system roles (#122)
- Bump actions/checkout from 3 to 4 (#123)
- ci: ensure dependabot git commit message conforms to commitlint (#126)
- ci: tox-lsr version 3.1.1 (#131)

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
