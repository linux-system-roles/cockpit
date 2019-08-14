# cockpit

Installs and configures the Cockpit Web Console for RHEL & Fedora.

## Requirements

If running on RHEL/CentOS 7, please ensure the Extras repository is enabled as
the role does not allow handling of that yet.

## Role Variables

Available variables per distribution are listed below, along with default
values (see `defaults/main.yml`):

### `cockpit_base_packages`

Specify the list of base Cockpit packages to be installed. As default, the list
of base Cockpit packages is:

```yaml
cockpit_base_packages:
  - cockpit
  - cockpit-bridge
  - cockpit-networkmanager
  - cockpit-packagekit
  - cockpit-selinux
  - cockpit-storaged
  - cockpit-system
  - cockpit-ws
```

### `cockpit_extra_packages`

Specify the additional list of Cockpit packages to be installed depending on
what functionality is desired. This list is empty as default. Example of use:

```yaml
# Install additional Cockpit packages for more functionality:
cockpit_extra_packages:
  - cockpit-389-ds
  - cockpit-composer
  - cockpit-dashboard
  - cockpit-doc
  - cockpit-docker
  - cockpit-kdump
  - cockpit-machines
  - cockpit-ostree
  - cockpit-pcp
  - cockpit-podman
  - cockpit-session-recording
  - cockpit-sosreport
  - cockpit-tests
```

### `cockpit_enablerepo`

Specify the repository to enable in case non-standard repository mirror names
are used. The default value of this role variable depends on the used Linux
distribution. The table below summarize possible default values per Linux
distribution:

| Linux Distribution | `cockpit_enablerepo`'s Default Value |
| ------------------ | ------------------------------------ |
| Fedora | `fedora <Fedora version number> - <architecture>` |
| Red Hat Enterprise Linux 7 | `rhel-7-server-extras-rpms` |
| Red Hat Enterprise Linux 8 | `rhel-8-for-<architecture>-appstream-rpms` |
| other | empty string |

To disable this feature, set the `cockpit_enablerepo` to `""` (empty string).

The value of `cockpit_enablerepo` has effect only on Linux distributions with
yum based packaging.

### `cockpit_service`

Specify the name of the Cockpit service as seen by system. The default name
used is `cockpit`.

### `cockpit_restart_delay`

Specify the time interval in seconds between stopping and starting the Cockpit
service when the Cockpit service needs to be restarted. Defaultly, this is set
to 3 seconds.

## Dependencies

RHEL/CentOS 7.x depend on the Extras repository being enabled. Other
considerations include using linux-system-roles.firewall to make the Web
Console available remotely.

## Example Playbook

Run the role with default params:

```yaml
- hosts: all
  become: yes
  roles:
    - linux-system-roles.cockpit
```

Along the base Cockpit packages, install also `podman` and `docker` extra
packages:

```yaml
- hosts: all
  become: yes
  vars:
    cockpit_extra_packages:
      - cockpit-podman
      - cockpit-docker
  roles:
    - linux-system-roles.cockpit
```

Extend Cockpit about `cockpit-MyCoolCockpitExtension` from
`MyCoolCockpitExtensionRepository` (that need to be enabled first). Also, if a
Cockpit service is already installed and it is running, provide 5 seconds time
interval between stopping and starting the service to ensure that things are
going smoothly.

```yaml
- hosts: all
  become: yes
  vars:
    cockpit_extra_packages:
      - cockpit-MyCoolCockpitExtension
    cockpit_enablerepo: "MyCoolCockpitExtensionRepository"
    cockpit_restart_delay: 5
  roles:
    - linux-system-roles.cockpit
```

## License

GPLv3
