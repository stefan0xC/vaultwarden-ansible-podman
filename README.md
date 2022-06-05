ansible-vaultwarden
=========

Installs vaultwarden behind an nginx proxy using postgres backend in a (rootless) podman container.

Requirements
------------

Ansible Collections (especially the [containers.podman](https://docs.ansible.com/ansible/latest/collections/containers/podman/index.html) collection) are required. You should also have a working SMTP server and a domain pointing to your webserver.

WIP: systemd/user unit files for automatic startup of rootless containers after reboot (and/or rewriting the role for running the container rootfull).

Role Variables
--------------

* acme\_account\_email is required to install the necessary Let's Encrypt Domain 
* vaultwarden\_fqdn is the required full qualified domain name.
* vaultwarden\_smtp\_{from,host,user,password} are required for SMTP configuration.
* vaultwarden\_admin\_token can be set to enable the Vaultwarden Admin Panel.
* the rest should be reasonable defaults but YMMV (you can adapt the playbook to your needs)

Example Playbook
----------------

```
---
- name: install vaultwarden
  hosts: vaultwarden
  vars:
    acme_account_email: vaultwarden@example.com
    vaultwarden_admin_token: "VAULTWARDEN_ADMIN_TOKEN"
    vaultwarden_fqdn: "vaultwarden.example.com"
    vaultwarden_smtp_from: vaultwarden@example.com
    vaultwarden_smtp_host: mail.example.com
    vaultwarden_smtp_password: SMTP_PASSWORD
    vaultwarden_smtp_user: vaultwarden
  roles:
    - ansible-vaultwarden
```


License
-------

MIT

Author Information
------------------

Stefan Melmuk
