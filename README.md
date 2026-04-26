# Ansible Role: NextCloud

## Table of Contents

- [Description](#description)
- [Requirements](#requirements)
- [Variables](#variables)
- [Tags](#tags)
- [Playbook example](#playbook-example)
- [How to contribute](#how-to-contribute)

## Description

Ansible role to deploy **NextCloud** as docker container to have a self-hosted back-up storage solution.

## Requirements

* Docker (must be installed on the target hosts)

## Installation

```bash
ansible-galaxy install cornelcristea.nextcloud
```

## Variables

The role uses the following variables:

| Name | Description | Default |
|---------|-------------|---------|
| `nextcloud_timezone` | Timezone for Nextcloud | `UTC` |
| `nextcloud_version` | Version tag for the Nextcloud Docker image from linuxserver.io | `33.0.2-ls425` |
| `nextcloud_http_port` | External HTTP port to expose Nextcloud | `7070` |
| `nextcloud_https_port` | External HTTPS port to expose Nextcloud | `7071` |
| `nextcloud_data_volume` | Path to the Nextcloud data volume on the host | *check defaults* |
| `nextcloud_trusted_domains` | Trusted domains for Nextcloud (should match URLs used to access Nextcloud) | *empty* |
| `nextcloud_admin_password` | Admin password for the initial Nextcloud setup | `admin` |
| `nextcloud_password_policy_enabled` | Enable or disable password policy (checking password strength) | `false` |
| `nextcloud_users` | List of Nextcloud users to create | *check defaults* |
| `nextcloud_applications` | Dictionary of Nextcloud apps to enable by default | *check defaults* |
| `nextcloud_smtp_host` | SMTP server hostname or IP address used by Nextcloud to send emails | `smtp.example.com` |
| `nextcloud_smtp_port` | SMTP port number (587 for TLS, 465 for SSL, 25 for plain) | `587` |
| `nextcloud_smtp_encryption` | Encryption method for SMTP (tls, ssl, or none) | `tls` |
| `nextcloud_smtp_user` | Username for authenticating to the SMTP server | `user@example.com` |
| `nextcloud_smtp_password` | Password for the SMTP user account | `yourpassword` |
| `nextcloud_smtp_from_address` | Local part of the "From" email address (before @) | `no-reply` |
| `nextcloud_smtp_domain` | Domain part of the "From" email address (after @) | `example.com` |
| `nextcloud_db_type` | Database type for Nextcloud (sqlite3, mysql, or pgsql) | `mysql` |
| `nextcloud_mariadb_version` | Version tag for the MariaDB Docker image (if db_type is mysql) | `11.4.9-r0-ls212` |
| `nextcloud_postgres_version` | Version tag for the PostgreSQL Docker image (if db_type is pgsql) | `14.22-trixie` |
| `nextcloud_db_name` | Name of database | `database` |
| `nextcloud_db_port` | External port to expose database service (MariaDB or PostgreSQL) | `3306` |
| `nextcloud_db_username` | Username for MariaDB database | `nextcloud` |
| `nextcloud_db_password` | Password for the MariaDB database user | `dbpass123` |
| `nextcloud_db_root_password` | Root password for the MariaDB database | `mysecretrootpassword` |
| `nextcloud_redis_version` | Version tag for the Redis Docker image | `8.4.2-alpine3.22` |
| `nextcloud_redis_port` | Port to expose Redis | `6379` |

## Tags

When running the playbook to deploy the NextCloud service, specific tags can be used to perform targeted actions.

| Name | Description |
|---------|-------------|
| `update_docker_compose` | Regenerates and applies Docker Compose configuration (env file, docker-compose.yml, and container orchestration) |
| `update_trusted_domains` | Manages Nextcloud trusted domains configuration (add, remove, and sync) |
| `update_apps` | Manages Nextcloud applications (enable/disable apps and configure SMTP server) |
| `update_users` | Manages Nextcloud users (enable/disable password policy, create users, and delete unused users) |

## Playbook example

```yaml
- name: Deploy NextCloud
  hosts: servers
  gather_facts: true
  vars:
    nextcloud_timezone: "America/New York"
    nextcloud_trused_domains:
      - nextcloud.homelab.internal
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
