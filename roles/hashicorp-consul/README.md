# hashicorp-consul

Install and configure HashiCorp Consul.

## Requirements

None

## Role Variables

See `defaults/main.yml`.

## Dependencies

None

## Example Role

This role follows my cluster organization management philosophy, where there are
three types: prime, server, or client. The prime role and server roles are
management nodes for the cluster, with the difference being that server nodes
obtain secrets generated on the prime node. Client nodes register themselves
with one of the server or prime nodes.

```ini
# Machine responsible for generating secrets in consul cluster (also
# participates as a server in the cluster).
[consul_prime]

# Server machines participating in a consul cluster. Will obtain secrets
# directly from consul_prime.
[consul_servers]

# Client machines participating in a consul cluster. Will join the cluster via
# consul_prime, or fallback to joining via one of the consul_servers.
[consul_clients]
```

```yaml
- name: Install and Configure HashiCorp Consul (Prime)
  hosts: consul_prime
  roles:
    - role: hashicorp-consul
  vars:
    cluster_role: prime

- name: Install and Configure HashiCorp Consul (Server)
  hosts: consul_servers
  roles:
    - role: hashicorp-consul
  vars:
    cluster_role: server

- name: Install and Configure HashiCorp Consul (Client)
  hosts: consul_clients
  roles:
    - role: hashicorp-consul
  vars:
    cluster_role: client
```

## License

Apache 2.0
