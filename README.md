# Request Let's Encrypt certificate

This role requests a certificate from Let's Encrypt, setting up the auto
renewal configuration file.

## Requirements

In your local machine:

```bash
pip install -r requirements.txt
```

## Role Variables

* `domain`: Domain name of the requested certificate.
* `web_path_letsencrypt`: path where to store the ACME challenges.
* `letsencrypt_renewal_conf`: For configuring the autorenewal settings, used
   only if `letsencrypt_renew_hook` is defined.
* `letsencrypt_renew_hook`: Command to execute when a successful renewal of the
   `domain` happens. For example: `/usr/sbin/service nginx restart`
* `letsencrypt_method`: Method to use when requesting the certificate the first
   time. `standalone` or `webroot` (default).

## Dependencies

* `sudo` and `python` in the target host(s).
* certbot
  It also needs to have a web directory and a web server/proxy configured for the
  ACME challenge. You can use this configuration for example
  [nginx](https://www.nginx.com/blog/free-certificates-lets-encrypt-and-nginx/).

## Example Playbook

```yaml
- name: Request Let's Encrypt
  hosts: all
  vars:
    domain: sub.domain.tld
    letsencrypt_renew_hook: /usr/sbin/service nginx restart
  roles:
    - role: letsencrypt_request
```

## Testing

To test the role you need [molecule](http://molecule.readthedocs.io/en/latest/),
**docker** and some python requirements that can be installed wwith
`pip install -r requirements-dev.txt`.

```bash
molecule test
```

or

```bash
make test
```

## License

GPLv3

## Author Information

* m0wer (at) autistici (dot) org
