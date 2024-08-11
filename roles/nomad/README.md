# Nomad

Install, configure and maintain [Nomad](https://www.nomadproject.io) - a
workload orchestrator from HashiCorp.

## Role Variables

See [defaults/](https://github.com/nahsilabs/ansible-hashistack/blob/main/roles/nomad/defaults/)
for details and examples.

#### `nomad_version`

- version to use

#### `nomad_dirs`

- a map of directories to create

#### `nomad_config`

- main [configuration](https://www.nomadproject.io/docs/configuration) file

#### `nomad_configs`

- map of configuration files to create in `config.d` directory

#### `nomad_user`

- owner of nomad process and files. Set to `nomad` on server hosts. On client
  hosts `root` is required.

#### `nomad_grop`

- group of `nomad_user`. Set to `nomad` on server hosts.

#### `nomad_download_url`

- url to get nomad archive from
- default: `https://releases.hashicorp.com`

#### `nomad_unit`

- systemd unit file

#### `skip_handlers`

- skipt nomad restart/reload - useful when building images with packer

#### `skip_enable`

- skip enabling service - useful when building images with packer

## Tags

- `config` - update Nomad unit file and sync configuration files

## Author

- **Anatolios Laskaris** - [nahsi](https://github.com/nahsi)
