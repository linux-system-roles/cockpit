# Cockpit

[![ansible-lint.yml](https://github.com/linux-system-roles/cockpit/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/linux-system-roles/cockpit/actions/workflows/ansible-lint.yml) [![ansible-test.yml](https://github.com/linux-system-roles/cockpit/actions/workflows/ansible-test.yml/badge.svg)](https://github.com/linux-system-roles/cockpit/actions/workflows/ansible-test.yml) [![codespell.yml](https://github.com/linux-system-roles/cockpit/actions/workflows/codespell.yml/badge.svg)](https://github.com/linux-system-roles/cockpit/actions/workflows/codespell.yml) [![integration-tests.yml](https://github.com/linux-system-roles/cockpit/actions/workflows/integration-tests.yml/badge.svg)](https://github.com/linux-system-roles/cockpit/actions/workflows/integration-tests.yml) [![markdownlint.yml](https://github.com/linux-system-roles/cockpit/actions/workflows/markdownlint.yml/badge.svg)](https://github.com/linux-system-roles/cockpit/actions/workflows/markdownlint.yml) [![tft.yml](https://github.com/linux-system-roles/cockpit/actions/workflows/tft.yml/badge.svg)](https://github.com/linux-system-roles/cockpit/actions/workflows/tft.yml) [![tft_citest_bad.yml](https://github.com/linux-system-roles/cockpit/actions/workflows/tft_citest_bad.yml/badge.svg)](https://github.com/linux-system-roles/cockpit/actions/workflows/tft_citest_bad.yml) [![woke.yml](https://github.com/linux-system-roles/cockpit/actions/workflows/woke.yml/badge.svg)](https://github.com/linux-system-roles/cockpit/actions/workflows/woke.yml)

Installs and configures the Cockpit Web Console for distributions that support it, such as RHEL, CentOS, Fedora, Debian, and Ubuntu.

## Requirements

RHEL/CentOS 7.x depend on the Extras repository being enabled.

### Collection requirements

The role requires the `firewall` role and the `selinux` role from the
`fedora.linux_system_roles` collection, if `cockpit_manage_firewall` and
`cockpit_manage_selinux` are set to `true`, respectively. Please see also
`cockpit_manage_firewall` and `cockpit_manage_selinux` in
[`Role Variables`](#role-variables).

If `cockpit` is a role from the `fedora.linux_system_roles` collection
or from the Fedora RPM package, the requirement is already satisfied.

If you want to manage `rpm-ostree` systems with this role, you will need to
install additional collections.  Please run the following command line to
install the collection.

```bash
ansible-galaxy collection install -vv -r meta/collection-requirements.yml
```

## Role Variables

Available variables per distribution are listed below, along with default values (see `defaults/main.yml`):

### cockpit_packages

The primary variable is `cockpit_packages` which allows you to specify your own selection of cockpit packages you want to install, or allows you to choose one of three predefined package sets: `default, minimal, or full`.  Obviously `default` is selected if you do not define this variable.  Not that the packages installed may vary depending on the distribution and version as different packages of cockpit functionality have been provided over time.  Also, some may not be available on all distributions, such as `cockpit-docker` which was deprecated on RHEL in favor of `cockpit-podman`.

Example of explicit cockpit packages to install.  Dependencies should pull in the minimal cockpit packages so that they work.

```yaml
cockpit_packages:
  - cockpit-storaged
  - cockpit-podman
```

Example of using the predefined package sets.  This is the recommended method for installation.

```yaml
cockpit_packages: default
    # equivalent to
    #  - cockpit
    #  - cockpit-networkmanager
    #  - cockpit-packagekit
    #  - cockpit-selinux
    #  - cockpit-storaged

cockpit_packages: minimal
    # equivalent to
    #  - cockpit-system
    #  - cockpit-ws

cockpit_packages: full
    # equivalent to repoquery for 'cockpit-*'
    # This is will pull in many packages such as
        #  - cockpit    ## Default list
        #  - cockpit-bridge
        #  - cockpit-networkmanager
        #  - cockpit-packagekit
        #  - cockpit-selinux
        #  - cockpit-storaged
        #  - cockpit-system
        #  - cockpit-ws
        ## and all the rest
        #  - cockpit-389-ds
        #  - cockpit-composer
        #  - cockpit-dashboard
        #  - cockpit-doc
        #  - cockpit-kdump
        #  - cockpit-machines
        #  - cockpit-pcp
        #  - cockpit-podman
        #  - cockpit-session-recording
        #  - cockpit-sosreport
```

### cockpit_enabled

```yaml
cockpit_enabled: true
```

Boolean variable to control if Cockpit is enabled to start automatically at boot (default `true`).

### cockpit_started

```yaml
cockpit_started: true
```

Boolean variable to control if Cockpit should be started/running (default `true`).

### cockpit_config

```yaml
cockpit_config:                               #Configure /etc/cockpit/cockpit.conf
  WebService:                                 #Specify "WebService" config section
    LoginTitle: "custom login screen title"   #Set "LoginTitle" in "WebService" section
    MaxStartups: 20                           #Set "MaxStartups" in "WebService" section
  Session:                                    #Specify "Session" config section
    IdleTimeout: 15                           #Set "IdleTimeout" in "Session" section
    Banner: "/etc/motd"                       #Set "Banner" in "Session" section
```

Configure settings in the /etc/cockpit/cockpit.conf file.  See [`man cockpit.conf`](https://cockpit-project.org/guide/latest/cockpit.conf.5.html) for a list of available settings.  Previous settings will be lost, even if they are not specified in the role variable (no attempt is made to preserve or merge the previous settings, the configuration file is replaced entirely).

### cockpit_port

```yaml
cockpit_port: 9090
```

Cockpit runs on port 9090 by default. You can change the port with this option.

### cockpit_manage_firewall

```yaml
cockpit_manage_firewall: false
```

Boolean variable to control the `cockpit` firewall service with the `firewall` role.
If the variable is set to `false`, the `cockpit` role does not manage the firewall.
Default to `false`.

NOTE: `cockpit_manage_firewall` is limited to *adding* ports.
It cannot be used for *removing* ports.
If you want to remove ports, you will need to use the firewall system
role directly.

NOTE: This functionality is supported only when the managed host's `os_family`
is `RedHat`.

### cockpit_manage_selinux

```yaml
cockpit_manage_selinux: false
```

Boolean flag allowing to configure selinux using the selinux role.
The default SELinux policy does not allow Cockpit to listen to anything else
than port 9090. If you change the port, enable this to use the selinux role
to set the correct port permissions (websm_port_t).
If the variable is set to `false`, the `cockpit` role does not manage the
SELinux permissions of the cockpit port.

NOTE: `cockpit_manage_selinux` is limited to *adding* policy.
It cannot be used for *removing* policy.
If you want to remove policy, you will need to use the selinux system
role directly.

NOTE: This functionality is supported only when the managed host's `os_family`
is `RedHat`.

See also the [Cockpit guide](https://cockpit-project.org/guide/latest/listen.html#listen-systemd) for details.

### cockpit_transactional_update_reboot_ok

```yaml
cockpit_transactional_update_reboot_ok: true
```

This variable is used to handle reboots required by transactional updates. If a transactional update requires a reboot, the role will proceed with the reboot if cockpit_transactional_update_reboot_ok is set to true. If set to false, the role will notify the user that a reboot is required, allowing for custom handling of the reboot requirement. If this variable is not set, the role will fail to ensure the reboot requirement is not overlooked.

## Certificate setup

By default, Cockpit creates a self-signed certificate for itself on first startup. This should [be customized](https://cockpit-project.org/guide/latest/https.html) for environments which use real certificates.

### Use an existing certificate

If your server already has some certificate which you want Cockpit to use as well, point the `cockpit_cert` and `cockpit_private_key` role options to it:

```yaml
cockpit_cert: /path/to/server.crt
cockpit_private_key: /path/to/server.key
```

This will create `/etc/cockpit/ws-certs.d/50-system-role.{crt,key}` symlinks.

Note that this functionality requires at least Cockpit version 257, i.e. RHEL ≥ 8.6 or ≥ 9.0, or Fedora ≥ 34.

### Generate a new certificate

For generating a new certificate for Cockpit it is recommended to set the
`cockpit_certificates` variable. The value of `cockpit_certificates` is passed
on to the `certificate_requests` variable of the `certificate` role called
internally in the `cockpit` role and it generates the private key and certificate.
For the supported parameters of `cockpit_certificates`, see the
[`certificate_requests` role documentation section](https://github.com/linux-system-roles/certificate/#certificate_requests).

When you set `cockpit_certificates`, you must not set `cockpit_private_key`
and `cockpit_cert` variables because they are ignored.

This example installs Cockpit with an IdM-issued web server certificate
assuming your machines are joined to a FreeIPA domain.

```yaml
    - name: Install cockpit with Cockpit web server certificate
      include_role:
        name: linux-system-roles.cockpit
      vars:
        cockpit_certificates:
          - name: monger-cockpit
            dns: ['localhost', 'www.example.com']
            ca: ipa
            # with Cockpit < 257 (RHEL 7) you need:
            # group: cockpit-ws
```

Note: Generating a new certificate using the `certificate` system role in the playbook remains supported.

This example also installs Cockpit with an IdM-issued web server certificate.

```yaml
    # This step is only necessary for Cockpit version < 255; in particular on RHEL/CentOS 8
    - name: Allow certmonger to write into Cockpit's certificate directory
      file:
        path: /etc/cockpit/ws-certs.d/
        state: directory
        setype: cert_t

    - name: Generate Cockpit web server certificate
      include_role:
        name: fedora.linux_system_roles.certificate
      vars:
        certificate_requests:
          - name: /etc/cockpit/ws-certs.d/monger-cockpit
            dns: ['localhost', 'www.example.com']
            ca: ipa
            # with Cockpit < 257 (RHEL 7) you need:
            # group: cockpit-ws
```

NOTE: The `certificate` role, unless using IPA and joining the systems to an IPA domain,
creates self-signed certificates, so you will need to explicitly configure trust,
which is not currently supported by the system roles. To use `ca: self-sign` or
`ca: local`, depending on your certmonger usage, see the
[linux-system-roles.certificate documentation](https://github.com/linux-system-roles/certificate/#cas-and-providers) for details.

NOTE: This creating a self-signed certificate is not supported on RHEL/CentOS-7.

## Example Playbooks

The most simple example.

```yaml
---
- name: Manage cockpit
  hosts: fedora, rhel7, rhel8
  become: true
  roles:
    - linux-system-roles.cockpit
```

Another example, including the role as a task to control when the action is performed.  It is also recommended to configure the firewall using the fedora.linux_system_roles.firewall role to make the service accessible.

```yaml
---
tasks:
  - name: Install RHEL/Fedora Web Console (Cockpit)
    include_role:
      name: linux-system-roles.cockpit
    vars:
      cockpit_packages: default
      #cockpit_packages: minimal
      #cockpit_packages: full

  - name: Configure Firewall for Web Console
    include_role:
      name: fedora.linux_system_roles.firewall
    vars:
      firewall:
        service: cockpit
        state: enabled
```

## rpm-ostree

See README-ostree.md

## License

GPLv3
