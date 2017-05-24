Ansible GNOME Role - ansible-role-gnome
============================================

**Ansible role that manages a GNOME installation and associated services.**

This will install a full GNOME desktop, using the Gnome Shell. The packages
used for this are all customizable.

Additional things this role will do:

- Enable the Gnome Display Manager.
- Set default dconf values for all users.
- Install and enable gnome shell extensions.

Requirements
------------

This role was developed and tested on Ansible 2.2.0 and higher.
It may work on lower versions but that is currently unsupported.

Currently Arch Linux is a requirement although it may become more generic
in the future.

Role Variables
--------------

| **Name**                | **Type** | **Default**                   | **Choices**     | **Description**                                                                               |
|-------------------------|----------|-------------------------------|-----------------|-----------------------------------------------------------------------------------------------|
| gnome_aur_helper        | string   |                               | pacaur / yaourt | AUR helper utility to use with "Arch Linux Updates Indicator" (if installed).                 |
| gnome_input_sources     | list     | ['xkb','se']                  |                 | Input source, or keyboard layout that Gnome will use. This is a list within a list.           |
| gnome_packages          | list     | *(big list of packages)*      |                 | Packages that will form the basis of the Gnome desktop.                                       |

    # A list of dictionaries is used to define what extensions to install
    # and for which users it should be enabled.
    gnome_shell_extensions:
      - id: '1010'
        users: ['username']

Dependencies
------------

None

Example Playbook
----------------

Set the keyboard layout to **us** by default, while leaving **se** enabled.

    - hosts: all
      roles:
        - role: AsavarTzeth.gnome
          gnome_input_sources:
            - ['xkb','us']
            - ['xkb','se']

Use all core gnome packages and nothing else. Note that meta package names vary
between distributions.

    - hosts: all
      roles:
        - role: AsavarTzeth.gnome
          gnome_packages: ['gnome']

Install the [Arch Linux Updates Indicator](https://extensions.gnome.org/extension/1010/archlinux-updates-indicator/)
extension and use [pacaur](https://github.com/rmarquis/pacaur) to enable
updates for AUR packages. Changes will be limited to the foobar user.

    - hosts: all
      roles:
        - role: AsavarTzeth.gnome
          gnome_aur_helper: pacaur
          gnome_shell_extensions:
            - id: '1010'
              users: ['foobar']

License
-------

BSD-2-Clause

Author Information
------------------

Patrik Nilsson
