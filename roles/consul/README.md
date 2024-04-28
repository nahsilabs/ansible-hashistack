# Consul

Install, configure and maintain [Consul](https://www.consul.io) - a service mesh
from HashiCorp.

## Role Variables

See [defaults/](https://github.com/nahsi/ansible-consul/blob/master/defaults/)
for details and examples.

#### `consul_version`

- version to use

#### `consul_dirs`

- a map of directories to create
- default:

```yml
consul_dir: "/opt/consul"
consul_dirs:
  main:
    path: "{{ consul_dir }}"
  configs:
    path: "{{ consul_dir }}/config.d"
  services:
    path: "{{ consul_dir }}/service.d"
  certs:
    path: "{{ consul_dir }}/certs"
    mode: "u=rwX,g=rX,o="
  scripts:
    path: "{{ consul_dir }}/script.d"
  logs:
    path: "/var/log/consul"
  data:
    path: "/var/lib/consul"
    mode: "u=rwX,g=rX,o="
```

#### `consul_config`

- main [configuration](https://www.consul.io/docs/agent/options) file
- example: please see
  [defaults/example.yml](https://github.com/nahsi/ansible-consul/blob/master/defaults/example.yml)

#### `consul_configs`

- map of configuration files to create in `config.d` directory. Restart on
  changes

#### `consul_services`

- map of [service](https://www.consul.io/docs/discovery/services) files to
  create in `service.d` directory. Reload on changes

#### `consul_scripts`

- map of scripts to create in `scripts.d` directory

#### `consul_user`

- owner of Consul process and files
- default: `consul`

#### `consul_group`

- group of `consul_user`
- default: `consul`

#### `consul_download_url`

- url to get Consul archive from
- default: `https://releases.hashicorp.com`

#### `consul_service`

- openrc service file
- default: see
  [defaults/main.yml](https://github.com/nahsi/ansible-consul/blob/master/defaults/main.yml)

#### `consul_unitfile`

- systemd unit file
- default: see
  [defaults/main.yml](https://github.com/nahsi/ansible-consul/blob/master/defaults/main.yml)

#### `skip_handlers`

- skip consul restart/reload - useful when building images with packer
- default: `false`

#### `skip_enable`

- skip enabling service - useful when building images with packer
- default: `false`

## Tags

- `config` - update Consul unit/service file and sync configuration files
- `services` - sync Consul services
- `scripts` - sync Consul scripts

## Author

- **Anatoly Laskaris** - [nahsi](https://github.com/nahsi)
