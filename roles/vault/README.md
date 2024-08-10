# Vault

Install, configure and maintain [Vault](https://www.vaultproject.io) - a tool
for managing secrets from HashiCorp.

## Role Variables

See [defaults/](https://github.com/nahsilabs/ansible-hashistack/blob/main/roles/vault/defaults/)
for details and examples.

#### `vault_version`

- version to use

#### `vault_dirs`

- a map of directories to create

#### `vault_config`

- main [configuration](https://www.vaultproject.io/docs/configuration) file

#### `vault_configs`

- map of configuration files to create in `config.d` directory. Restart on
  changes

#### `vault_user`

- owner of Vault process and files

#### `vault_group`

- group of `vault_user`

#### `vault_download_url`

- url to get Vault archive from

#### `vault_unit`

- systemd unit file

#### `skip_handlers`

- skip Vault restart/reload - useful when building images with Packer
- default: `false`

#### `skip_enable`

- skip Vault enabling in systemd - useful when building images with Packer
- default: `false`

## Tags

- `config` - update Vault unit/service file and sync configuration files

## Author

- **Anatoly Laskaris** - [nahsi](https://github.com/nahsi)
