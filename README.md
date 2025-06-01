# Docker Install

Installs Docker CE on Hosts.

## Requirements

Ansible Version 2.9

## Role Variables

```yaml
#############################
# Docker’s official GPG key #
#############################
# default:
#docker_apt_gpg_key: "https://download.docker.com/linux/ubuntu/gpg"
docker_apt_gpg_key: "https://download.docker.com/linux/ubuntu/gpg"

#################
# `daemon.json` #
#################
## IPv6-Support
# default:
#docker_ipv6: false
#docker_ipv6_network: undefined
docker_ipv6: true
docker_ipv6_network: 2001:db8:1::/64

## private Docker mirrors
# default:
#docker_registry_mirrors: undefined
docker_registry_mirrors:
  - "https://registry.private.com"
  - "https://registry2.private.com"

# internal Docker network
# default:
#docker_network: undefined
docker_network:
  bip: 10.50.0.1/16
  address_pools:
    - base: 10.51.0.1/16
      size: 24
    - base: 10.52.0.1/16
      size: 24

# Default GELF-Logging-Target
# default:
#docker_log: undefined
docker_log:
  gelf_target: "udp://gelf.target.com:12201"

##############################
# Login to Docker Registries #
##############################
# default:
#docker_logins: []
docker_logins:
  - docker_registry_url: "registry.private.com"
    docker_registry_user: "registry-user"
    docker_registry_pass: "registry-user-password"
# the ansible_ssh_user is added to the docker group by default

##################################
# Allow non-sudo usage for users #
##################################
# default:
#docker_users: []
docker_users:
  - user1
  - user2
```

## Dependencies

[Community General Collection](https://galaxy.ansible.com/community/general?sc_cid=701f2000001OH7YAAW) (comes with `ansible`, but not with `ansible-core`)

## Example Playbook

```yaml
---
- hosts: docker
  become: true
  roles:
    - role: role_docker_setup
```

## License

MIT

## Author Information

Paul Wannenmacher, 2022
