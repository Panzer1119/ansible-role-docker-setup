# Ansible Role: Docker Setup

This Ansible role installs and configures Docker with optional ZFS and logging configurations.

## Variables

### Logging

- `use_gelf_logging`: Whether to use GELF logging driver (default: `false`)
- `gelf_address`: Address for GELF logging driver (default: `"tcp://graylog:12201"`)
- `use_full_container_id`: Whether to use full container ID in Docker log messages (default: `false`)

### ZFS

- `zfs_pool_name`: ZFS pool name (default: `"docker"`)

#### ZFS Storage Driver

- `use_zfs_storage_driver`: Whether to use ZFS as Docker storage driver (default: `false`)
- `zfs_docker_storage_driver_dataset`: ZFS dataset for Docker storage (default: `"docker/storage"`)

#### ZFS Volume Plugin

- `use_zfs_volume_plugin`: Whether to use ZFS as Docker volume plugin (default: `false`)
- `docker_zfs_plugin_version`: Version of the Docker volume plugin (default: `v1.0.5`)
- `docker_zfs_plugin_github_repo`: GitHub user/repository for the Docker ZFS plugin (default: `TrilliumIT/docker-zfs-plugin`)
- `zfs_docker_volume_plugin_dataset`: ZFS dataset for Docker volumes (default: `"docker/volumes"`)

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
