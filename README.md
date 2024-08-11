# Ansible Collection - nahsilabs.hashistack

## Roles

- [nomad](https://github.com/nahsilabs/ansible-hashistack/tree/main/roles/nomad)
- [consul](https://github.com/nahsilabs/ansible-hashistack/tree/main/roles/consul)
- [vault](https://github.com/nahsilabs/ansible-hashistack/tree/main/roles/vault)
- [vaultagent](https://github.com/nahsilabs/ansible-hashistack/tree/main/roles/vaultagent)

## Roles Philosophy

Instead of duplicating every single configuration option as an Ansible variable
Consul configuration is stored in Ansible inventory in `yaml` format:

```yml
consul_config:
  data_dir: "/var/lib/consul/"

  enable_syslog: true
  # "trace", "debug", "info", "warn", "err"
  log_level: "info"
  syslog_facility: "LOCAL5"

  rejoin_after_leave: true

  bind_addr: !unsafe '{{ GetInterfaceIP "eth0" }}'

  telemetry:
    disable_hostname: true
    prometheus_retention_time: "30s"

  server: false
```

And then copied to host using `to_nice_json` filter:

```yml
- name: copy consul config
  copy:
    content: "{{ consul_config | to_nice_json }}"
    dest: "/opt/consul/consul.json"
    validate: "consul validate -config-format=json %s"
```

When variable is a map (`consul_services` for example) every key of a map will
be copied as file with value as a content.

The following map

```yml
consul_services:
  consul:
    service:
      id: "consul-api"
      name: "consul-api"
      port: 8500
      tags:
        - "traefik.enable=true"
        - "traefik.http.routers.consul.entrypoints=https"
        - "traefik.http.routers.consul.rule=Host(`consul.example.com`)"
      meta:
        external-source: "consul"
      check:
        id: "consul-api-health"
        name: "consul-api-health"
        http: "http://localhost:8500/v1/agent/self"
        interval: "20s"
        timeout: "2s"

  telegraf:
    service:
      id: "telegraf-exporter"
      name: "telegraf-exporter"
      port: 9271
      meta:
        external-source: "consul"
      check:
        id: "telegraf-exporter-health"
        name: "telegraf-exporter-health"
        http: "http://localhost:9270"
        interval: "20s"
        timeout: "2s"
```

will produce files `consul.json` and `telegraf.json` in
`/opt/consul/service.d/`.

Files that are not present in the map will be deleted, thus allowing to maintain
a state with Ansible inventory.
