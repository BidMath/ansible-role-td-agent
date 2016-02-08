# Ansible Role: td-agent

Installs td-agent on RedHat/CentOS or Debian/Ubuntu linux servers.

This role installs and configures the latest/selected version of td-agent from the TreasureData yum repository (on RedHat-based systems) or via apt (on Debian-based systems).

## Requirements

None.

## Role Variables
*See all available variables in [`defaults/main.yml`](https://github.com/trekdemo/ansible-role-td-agent/blob/master/defaults/main.yml).*

### `td_agent_version:`
Define a custom version of the package to install.
To get a list of available package versions visit: http://packages.treasure-data.com

### `td_agent_plugins:`
A list of objects that describe your fluent plugin dependencies. Find plugins at [fluentd.org/plugins](http://www.fluentd.org/plugins)

Example:

```yaml
td_agent_plugins:
  - { name: fluent-plugin-google-cloud, version: 0.4.14 }
  - name: fluent-plugin-secure-forward
    version: 0.3.2
```

### `td_agent_configuration:`
A list of objecgts with name and content as a multiline string with source and match blocks.
[Learn more...](http://docs.fluentd.org/articles/config-file)

```yaml
td_agent_configuration:
  - name: "Add host name to my access log"
    content: |
      <filter myapp.access>
        @type record_transformer
        <record>
          host_param "#{Socket.gethostname}"
        </record>
      </filter>

  - name: "Access log of my app"
    content: |
      <match myapp.access>
        @type file
        path /var/log/fluent/access
      </match>

  - name: "Alternatively you can use lookups to include longer configurations"
    content: {{ lookup('files', 'my-td-agent.conf') }}
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: server
  roles:
    - role: trekdemo.td-agent
  vars:
    td_agent_version: 2.2.1 # (default is 2.3.0)
    td_agent_plugins: # (default: [])
      - name: fluent-plugin-gcloud-storage
        version: 0.1.2
    td_agent_configuration: # (default: [])
      - name: Archive logs to GCS
        content: |
          <match example.publish>
            @type gcloud_storage
            # ...
          </match>
```

## License

MIT

## Author Information

This role was created in 2016 by [Gergo Sulymosi](http://github.com/trekdemo).
