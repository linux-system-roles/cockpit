# Role Name

Installs and configures the Cockpit Web Console RHEL & Fedora.

## Requirements

If running on RHEL/CentOS 7, please ensure the Extras repository is enabled as the role does not allow handling of that yet.

## Role Variables

Available variables per distribution are listed below, along with default values (see `vars/<distro>.yml`):

Specify the list of Cockpit packages to be installed depending on what functionality is desired.

```yaml
cockpit_packages: 
  - cockpit		## Default list installed.
  - cockpit-bridge
  - cockpit-networkmanager
  - cockpit-packagekit
  - cockpit-selinux
  - cockpit-storaged
  - cockpit-system
  - cockpit-ws

  - cockpit-389-ds	## More functionality can be added
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


## Dependencies

RHEL/CentOS 7.x depend on the Extras repository being enabled.  Other considerations include using linux-system-roles.firewall to make the Web Console available remotely.

## Example Playbook

```yaml
- hosts: fedora, rhel7, rhel8
  become: yes
  roles:
    - linux-system-roles.cockpit
```

## License

GPLv3

