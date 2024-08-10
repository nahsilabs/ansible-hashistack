# Consul

Install, configure and maintain [Consul](https://www.consul.io) - a service mesh
from HashiCorp.

## Role Variables

See [defaults/](https://github.com/nahsilabs/ansible-hashistack/blob/main/roles/consul/defaults/)
for details.

#### `consul_version`

- version to use

#### `consul_dirs`

- a map of directories to create

#### `consul_config`

- main [configuration](https://www.consul.io/docs/agent/options) file

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

#### `consul_group`

- group of `consul_user`

#### `consul_download_url`

- url to get Consul archive from

#### `consul_unit`

- systemd unit file

#### `skip_handlers`

- skip consul restart/reload - useful when building images with packer

#### `skip_enable`

- skip enabling service - useful when building images with packer

## Tags

- `config` - update Consul unit/service file and sync configuration files
- `services` - sync Consul services
- `scripts` - sync Consul scripts

## Author

- **Anatoly Laskaris** - [nahsi](https://github.com/nahsi)
