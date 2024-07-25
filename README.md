# Ansible Role: Docker Setup

This Ansible role installs and configures Docker with optional ZFS storage driver and logging configurations.
And it can also install the ZFS volume plugin and Sanoid for ZFS snapshots.

## Installation

```bash
ansible-galaxy role install Panzer1119.docker-setup
```

## Variables

### Logging

- `use_gelf_logging`: Whether to use GELF logging driver (default: `false`)
- `use_full_container_id`: Whether to use full container ID in Docker log messages (default: `false`)
- `gelf_address`: Address for GELF logging driver (default: `"tcp://graylog:12201"`)

### ZFS

- `docker_zfs_pool_name`: ZFS pool name (default: `"docker"`)

#### ZFS Storage Driver

- `use_zfs_storage_driver`: Whether to use ZFS as Docker storage driver (default: `true`)
- `docker_storage_driver_zfs_dataset_name`: ZFS dataset for Docker storage (default: `"layers"`)

#### ZFS Volume Plugin

- `use_zfs_volume_plugin`: Whether to use ZFS as Docker volume plugin (default: `true`)
- `docker_zfs_plugin_version`: Version of the Docker volume plugin (default: `1.1.1`)
- `docker_zfs_plugin_github_repo`: GitHub user/repository for the Docker ZFS plugin (default: `Panzer1119/docker-zfs-plugin`)
- `docker_volume_plugin_zfs_dataset_name`: ZFS dataset for Docker volumes (default: `"volumes"`)
- `docker_volume_parent_zfs_dataset_names`: List of ZFS dataset names for Docker volume parents (default: `["cache", "config", "data"]`)

#### Sanoid

- `use_sanoid`: Whether to use Sanoid for ZFS snapshots (default: `true`)
- `sanoid_version`: Version of Sanoid (default: `2.3.1`)
- `sanoid_github_repo`: GitHub user/repository for Sanoid (default: `Panzer1119/sanoid`)

## Example Playbook

```yaml
- hosts: all
  become: yes
  vars:
    use_gelf_logging: true
    use_full_container_id: true
    use_zfs_storage_driver: true
    use_zfs_volume_plugin: true
  roles:
    - ansible-role-docker-setup
```

Test it with the following command:

```bash
ansible-playbook -i inventory playbook.yml -CD
```
