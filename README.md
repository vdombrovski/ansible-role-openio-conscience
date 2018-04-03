[![Build Status](https://travis-ci.org/open-io/ansible-role-openio-conscience.svg?branch=master)](https://travis-ci.org/open-io/ansible-role-openio-conscience)
# Ansible role `conscience`

An Ansible role for conscience. Specifically, the responsibilities of this role are to:

- Install a namespace's conscience
- Configure a namespace's conscience

## Requirements

- Ansible 2.4+

## Role Variables


| Variable   | Default | Comments (type)  |
| :---       | :---    | :---             |
| `openio_conscience_auto_container` | `false` | ... |
| `openio_conscience_bind_address` | `"{{ ansible_default_ipv4.address }}"` | ... |
| `openio_conscience_bind_port` | `6000` | ... |
| `openio_conscience_chunk_size` | `10485760` | ... |
| `openio_conscience_data_security_custom` | `{}` | ... |
| `openio_conscience_multiple` | `{}` | ... |
| `openio_conscience_namespace` | `"OPENIO"` | ... |
| `openio_conscience_namespace_status` | `"standalone"` | ... |
| `openio_conscience_plugins` | `` | ... |
| `openio_conscience_pools` | `[]` | ... |
| `openio_conscience_server` | `` | ... |
| `openio_conscience_serviceid` | `"0"` | ... |
| `openio_conscience_services` | `` | ... |
| `openio_conscience_storage_policies_custom` | `{}` | ... |
| `openio_conscience_timeout_accepting_connection` | `1000` | ... |
| `openio_conscience_timeout_read_operations` | `1000` | ... |
| `openio_conscience_worm` | `false` | ... |

## Dependencies

No dependencies.

## Example Playbook

```yaml
- hosts: all
  gather_facts: true
  become: true
  roles:
    - role: conscience
      openio_conscience_namespace: "{{ NS }}"
      openio_conscience_pools:
        - name: rawx21
          targets:
            - where: rawx-europe
              type: rawx
              count: 2
            - where: rawx-asia
              type: rawx
              count: 1
          min_dist: 2
      
      openio_conscience_multiple:
        me: "{{ openio_conscience_bind_address }}:18000"
        group:
          - 172.17.0.3:18000
          - 172.17.0.4:18000

```


```ini
[all]
node1 ansible_host=192.168.1.173
```

## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section.

Pull requests are also very welcome.
The best way to submit a PR is by first creating a fork of this Github project, then creating a topic branch for the suggested change and pushing that branch to your own fork.
Github can then easily create a PR based on that branch.

## License

Apache License, Version 2.0

## Contributors

- [Cedric DELGEHIER](https://github.com/cdelgehier) (maintainer)