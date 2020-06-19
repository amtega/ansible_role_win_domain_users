# Ansible win_domain_users role

This is an [Ansible](http://www.ansible.com) role which manages windows domain users through the [`win_domain_user`](https://docs.ansible.com/ansible/latest/modules/win_domain_user_module.html) module.

## Requirements

[pywinrm 0.3.0+](https://pypi.org/project/pywinrm) on the control host.
[requests-credssp 1.0.2+](https://pypi.org/project/requests-credssp) on the control host.

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Example Playbook

This is an example playbook:

```yaml
---

- hosts: windows_ad
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

Tests are based on [molecule with vagrant virtual machines](https://molecule.readthedocs.io/en/latest/installation.html).

```shell
cd amtega.win_domain_users

molecule test
```

## License

Copyright (C) 2020 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify it under the terms of:

GNU General Public License version 3, or (at your option) any later version; or the European Union Public License, either Version 1.2 or – as soon they will be approved by the European Commission ­subsequent versions of the EUPL.

This role is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details or European Union Public License for more details.

## Author Information

- Daniel Sánchez Fábregas
