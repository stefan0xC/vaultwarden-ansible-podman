ansible-vaultwarden
=========

Installs vaultwarden behind an nginx proxy using postgres backend in a (rootfull) podman container.

Requirements
------------

Ansible Collections (especially the [containers.podman](https://docs.ansible.com/ansible/latest/collections/containers/podman/index.html) collection) are required. You should also have a working SMTP server and a domain pointing to your webserver. The firewall ports 80 and 443 should also be open.

Role Variables
--------------

* acme\_account\_email is required to install the necessary Let's Encrypt Domain. Tip: You can change the ACME certificate service by setting a different [vaultwarden\_acme\_directory](https://docs.ansible.com/ansible/latest/collections/community/crypto/acme_certificate_module.html#parameter-acme_directory). 
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
  become: yes
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
