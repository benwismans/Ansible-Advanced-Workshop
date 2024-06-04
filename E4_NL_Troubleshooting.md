## Extra - Troubleshooting
In dit (extra) lab staan playbooks met fouten. Vind de fout en los het probleem op!

* ``git.yml``
```
---
- hosts: all

  tasks:
  - name: "Ensure git is installed"
    yum:
      name: git
      state: latest
```

* ``firewall.yml``
```
---
- hosts: all
  become: true
  become_method: sudo

  tasks:
  - name: "Ensure firewall is configured"
    firewalld:
      service: "{{ SERVICE }}"
      permanent: yes
      immediate: yes
      state: enabled
      with_items:
        - http
        - https
```

* ``user.yml``
```
---
- hosts: all

  tasks:
  - name: "Ensure authorized key is installed for user {{ ANSIBLE_USER }}"
    authorized_key:
      user: {{ ANSIBLE_USER }}
      state: present
      key: "~/.ssh/id_rsa.pub"
```

* ``role.yml``
```
---
- hosts: workshop
  become: true
  become_method: sudo

  vars:
    account_groups:
    - name: "workshop"
    account_users:
    - name: "workshop"
      password: "$6$SnJIieK.VI.lc4wd$KsK.U12WQUWyxr2yqMh5ntN9pLs8EkRyEFStBvB2xDUv3xHr4iqjlqNCbgfCDGnYr9J3PQWPNKBPZPCwi/8l90"

    roles:
    - role: ontic.account
```
