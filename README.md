Request Let's Encrypt certificate
=================================

This role requests a certificate from Let's Encrypt, setting up the auto
renewal configuration file.

Requirements
------------

* certbot

It also needs to have a web directory and a web server/proxy configured for the
ACME challenge. You can use this configuration for example
[nginx](https://www.nginx.com/blog/free-certificates-lets-encrypt-and-nginx/).

If you want an automatic renewal, you must setup a **cron** of
`certbot -q renew`.

Role Variables
--------------

* `domain`: Domain name of the requested certificate.
* `web_path_letsencrypt`: path where to store the ACME challenges.
* `letsencrypt_webroot_conf`: Block of lines to setup the auto renewal via the
http-01 challenge using the specified web path.

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- name: Request Let's Encrypt
  hosts: all
  vars:
  	domain: sub.domain.tld
  roles:
    - role: letsencrypt-request
```

License
-------

GPLv3

Author Information
------------------

m0wer [ at ] autistici.org
