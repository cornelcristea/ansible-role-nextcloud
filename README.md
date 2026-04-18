# Ansible Role: NextCloud

## Description

Ansible role to deploy **NextCloud** as docker container to have a self-hosted back-up storage solution.

## Requirements

* Docker (must be installed on the target hosts)

## Installation

```bash
ansible-galaxy install cornelcristea.immich
```

## Variables

The role uses the following variables:

| Name | Description | Default |
|---------|-------------|---------|
| `nextcloud_timezone` | Timezone for the Nextcloud and MariaDB services | `UTC` |
| `nextcloud_version` | 	Version tag for the Nextcloud Docker image from linuxserver.io | `33.0.2-ls425` |
| `nextcloud_https_port` | External HTTPS port to expose Nextcloud | `443` |
| `nextcloud_http_port` | External HTTP port to expose Nextcloud | `80` |
| `nextcloud_data_volume` | Path to the Nextcloud data volume on the host | `/opt/nextcloud/data` |
| `nextcloud_mariadb_version` | Version tag for the MariaDB Docker image from linuxserver.io | `11.4.9-r0-ls212` |
| `nextcloud_mariadb_port` | External port to expose MariaDB | `3306` |
| `nextcloud_mariadb_root_password` | Root password for the MariaDB database | *empty* |
| `nextcloud_mariadb_database` | Name of the MariaDB database | `nextcloud_database` |
| `nextcloud_mariadb_username	` | Username for MariaDB database | *empty* |
| `nextcloud_mariadb_database` | Password for the MariaDB database user | *empty* |
| `nextcloud_redis_version` | Version tag for the Redis image from docker.io | `8.4.2-alpine3.22` |

## Playbook example

```yaml
- name: Deploy NextCloud
  hosts: servers
  gather_facts: true
  vars:
    nextcloud_timezone: "America/New York"
  roles:
    - cornelcristea.nextcloud
```

## How to contribute

We welcome contributions! Here’s how you can help improve this role:

1. **Fork the repository**    
  Click the `Fork` button at the top of the repository.

2. **Clone your fork locally**

  ```bash
  git clone https://github.com/cornelcristea/ansible-role-immich.git
  cd ansible-role-immich
  ```

3. **Create a new branch**

  ```bash
  git checkout -b my-feature-branch
  ```

  * Make your changes following Ansible best practices.
  * Add or update tests if applicable.
  * Update the README for any new variables or features.
  * Test your changes:
```bash
ansible-playbook -i test/inventory test/test.yml 
```
 * Run molecule test:
```bash
molecule test
```

4. **Commit and push your changes**

  ```bash
  git add .
  git commit -m "Add feature XYZ"
  git push origin my-feature-branch
  ```

5. **Open a Pull Request (PR)**   
Submit a PR from your branch. Include a clear description of your changes and why they’re needed.

**We appreciate your contributions!**
