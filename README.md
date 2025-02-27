# Ludus Juice Shop
Ansible role that installs [OWASP Juice Shop](https://github.com/juice-shop/juice-shop).

## Requirements
Tested templates:
- Ubuntu Server 24.04
- Debian 12

## Role Variables
By default Juice Shop runs as `root` on port `80`. This can be modified with the following variables:
```
ludus_juiceshop_port: 80
ludus_juiceshop_user: "root"
```
> Note 1: If you change the default user make sure you have permissions to listen on the `ludus_juiceshop_port` port.

> Note 2: If the `ludus_juiceshop_user` user does not exist he will be created. 

## Dependencies

None.

## Example Ludus Range Config
With default variables:
```yaml
ludus:
  - vm_name: "{{ range_id }}-juiceshop"
  hostname: "juiceshop"
  template: ubuntu-24.04-x64-server-template
  vlan: 10
  ip_last_octet: 10
  ram_gb: 4
  cpus: 2
  linux: true
  testing:
    snapshot: true
    block_internet: true
  roles:
    - ludus_juiceshop
```

With updated variables:
```yaml
ludus:
  - vm_name: "{{ range_id }}-juiceshop"
  hostname: "juiceshop"
  template: ubuntu-24.04-x64-server-template
  vlan: 10
  ip_last_octet: 10
  ram_gb: 4
  cpus: 2
  linux: true
  testing:
    snapshot: true
    block_internet: true
  roles:
    - ludus_juiceshop
  role_vars:
    ludus_juiceshop_port: 1234
    ludus_juiceshop_user: juicer
```

## License
GPLv3

## Author Information
This role was created by `xurger`, for [Ludus](https://ludus.cloud/).
