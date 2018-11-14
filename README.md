# Ansible win_domain_users role

This is an [Ansible](http://www.ansible.com) role which manages windows domain users through the [`win_domain_user`](https://docs.ansible.com/ansible/latest/modules/win_domain_user_module.html) module.

## Requirements

[Ansible 2.7.1+](http://docs.ansible.com/ansible/latest/intro_installation.html)

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Dependencies

None.

## Example Playbook

This is an example playbook:

```yaml
---

- hosts: windows_command_host
  roles:
    - amtega.win_domain_users
  vars:
    win_domain_users_defaults:
      path: ou=test,dc=domain,dc=local
      city: Sometown
      state_province: IN
      country: US

    win_domain_users:
      - name: alice
        firstname: Alice
        surname: Carroll
        password: 41c3P4ssw0rd
        state: present

      - name: bob
        firstname: Bob
        surname: Smith
        company: BobCo
        password: B0bP4ssw0rd
        groups:
          - Domain Admins
        street: 123 4th St.
        postal_code: 12345
        attributes:
          telephoneNumber: 555-123456
        state: present
```


## Testing

Tests are based on vagrant virtual machines. You can setup vagrant engine
quickly using the role [amtega.vagrant_engine](https://galaxy.ansible.com/amtega/vagrant_engine).

Once you have vagrant and virtualbox, you can run the tests with the following
commands:

```shell
$ cd amtega.win_domain_users/tests
$ git clone https://github.com/jborean93/ansible-windows.git
# Creating windows domain controler and client
$ cd ansible-windows/vagrant/
$ vim inventory.yml # Comment the following:
        # SERVER2008:
        #   ansible_host: 192.168.56.11
        #   vagrant_box: jborean93/WindowsServer2008-x64
        #   opt_domain_join_is_longhorn: yes
        # SERVER2008R2:
        #   ansible_host: 192.168.56.12
        #   vagrant_box: jborean93/WindowsServer2008R2
        # SERVER2012:
        #   ansible_host: 192.168.56.13
        #   vagrant_box: jborean93/WindowsServer2012
        # SERVER2012R2:
        #   ansible_host: 192.168.56.14
        #   vagrant_box: jborean93/WindowsServer2012R2
$ vagrant up # It takes a while
$ cd ../..
$ ansible-playbook main.yml
```


## License

Copyright (C) 2018 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify
it under the terms of:
GNU General Public License version 3, or (at your option) any later version;
or the European Union Public License, either Version 1.2 or – as soon
they will be approved by the European Commission ­subsequent versions of
the EUPL;

This role is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details or European Union Public License for more details.

## Author Information

- Daniel Sánchez Fábregas
