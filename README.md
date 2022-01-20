# Cockpit
![CI Testing](https://github.com/linux-system-roles/cockpit/workflows/tox/badge.svg)

Installs and configures the Cockpit Web Console for distributions that support it, such as RHEL, CentOS, Fedora, Debian, and Ubuntu.

## Requirements

  - RHEL/CentOS 7.x depend on the Extras repository being enabled.
  - Recommended to use [`linux-system-roles.firewall`](https://github.com/linux-system-roles/firewall/) to make the Web Console available remotely.

## Role Variables

Available variables per distribution are listed below, along with default values (see `defaults/main.yml`):

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
    # equivalent to globbing all of them
    #  - cockpit-*
    # This is will pull in many packages such as
        #  - cockpit		## Default list
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

    cockpit_enabled: yes
Boolean variable to control if Cockpit is enabled to start automatically at boot (default yes).

    cockpit_started: yes
Boolean variable to control if Cockpit should be started/running (default yes).


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

For generating a new certificate for Cockpit it is recommended to use the [linux-system-roles.certificate role](https://github.com/linux-system-roles/certificate/). If your machines are joined to a FreeIPA domain, or you use certmonger in a different mode already, generate a certificate with:

```yaml
    # This step is only necessary for Cockpit version < 255; in particular on RHEL/CentOS 8
    - name: Allow certmonger to write into Cockpit's certificate directory
      file:
        path: /etc/cockpit/ws-certs.d/
        state: directory
        setype: cert_t

    - name: Generate Cockpit web server certificate
      include_role:
        name: linux-system-roles.certificate
      vars:
        certificate_requests:
          - name: /etc/cockpit/ws-certs.d/monger-cockpit
            dns: ['localhost', 'www.example.com']
            ca: ipa
            group: cockpit-ws
```

You can also use `ca: self-sign` or `ca: local` depending on your certmonger usage, see the [linux-system-roles.certificate documentation](https://github.com/linux-system-roles/certificate/#cas-and-providers) for details.

Note that this does *not* work on RHEL/CentOS 7.

## Example Playbooks
The most simple example.
```yaml
---
- hosts: fedora, rhel7, rhel8
  become: yes
  roles:
    - linux-system-roles.cockpit
```
Another example, including the role as a task to control when the action is performed.  It is also recommended to configure the firewall using the linux-system-roles.firewall role to make the service accessible.
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
      name: linux-system-roles.firewall
    vars:
      firewall:
        service: cockpit
        state: enabled
```
## License
GPLv3
