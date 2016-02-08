# Ansible Role: td-agent

Installs td-agent on RedHat/CentOS or Debian/Ubuntu linux servers.

This role installs and configures the latest/selected version of td-agent from the TreasureData yum repository (on RedHat-based systems) or via apt (on Debian-based systems).

## Requirements

None.

## Role Variables


## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - { role: trekdemo.td-agent }

## License

MIT / BSD

## Author Information

This role was created in 2016 by [Gergo Sulymosi](http://github.com/trekdemo).
