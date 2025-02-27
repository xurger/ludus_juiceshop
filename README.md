# Ludus Juice Shop
Ansible role that installs [OWASP Juice Shop](https://github.com/juice-shop/juice-shop).

## Installation
To use this role it must be downloaded & installed first:
```bash
git clone https://github.com/xurger/ludus_juiceshop
ludus ansible role add -d ./ludus_juiceshop
```

> [!NOTE]
> If you want to install the role for a specific user use the `--user <user_id>` parameter. Alternatively, use `-g` to install the role for all users.

## Requirements
At least the following Ludus version (wasn't tested with prior versions):
```
Ludus client 1.8.1+994287e
Ludus Server 1.8.1+994287e
```

Templates:
- **Ubuntu Server 24.04**
- **Debian 12**

The role should work on both! Note that by default, Ludus does not come with the `Ubuntu Server 24.04` template. It must be manually added and installed first - [see the documentation](https://docs.ludus.cloud/docs/templates). You can always try to use the role with different templates, but I haven't tested them.

## Role Variables
By default Juice Shop runs as `root` on port `80`. This can be modified with the following variables:
```
ludus_juiceshop_port: 80
ludus_juiceshop_user: "root"
```

> [!IMPORTANT]
> If you change the default user make sure you have permissions to listen on the `ludus_juiceshop_port` port.

> [!NOTE]
> If the `ludus_juiceshop_user` user does not exist he will be created. 

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
