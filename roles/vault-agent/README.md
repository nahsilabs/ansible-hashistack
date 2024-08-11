# vault-agent

Install, configure and maintain [vault-agent](https://www.vaultproject.io/docs/agent)

## Role Variables

See
[defaults/](https://github.com/nahsilabs/ansible-hashistack/blob/main/roles/vaultagent/defaults/)
for details and examples.

#### `vault_agent_version`

- version to use

#### `vault_agent_dirs`

- a map of directories to create

#### `vault_agent_config`

- main [configuration](https://www.vaultproject.io/docs/agent#configuration) file

#### `vault_agent_templates`

- map of templates to create in `template.d` directory

#### `vault_agent_user`

- owner of vault-agent process and files

#### `vault_agent_group`

- group of `vault_agent_user`

#### `vault_agent_download_url`

- url to get vault-agent archive from

#### `vault_agent_unit`

- systemd unit file

#### `skip_handlers`

- skip restart/reload - useful when building images with Packer

#### `skip_enable`

- skip enable with systemd - useful when building images with Packer

## Tags

- `config` - update vault-agent unit file and sync configuration files

## Author

- **Anatoly Laskaris** - [nahsi](https://github.com/nahsi)
