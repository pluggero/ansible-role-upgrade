# Ansible Role: System Upgrade

[![CI](https://github.com/pluggero/ansible-role-upgrade/actions/workflows/ci.yml/badge.svg)](https://github.com/pluggero/ansible-role-upgrade/actions/workflows/ci.yml) [![Ansible Galaxy downloads](https://img.shields.io/ansible/role/d/pluggero/upgrade?label=Galaxy%20downloads&logo=ansible&color=%23096598)](https://galaxy.ansible.com/ui/standalone/roles/pluggero/upgrade)

An Ansible Role that performs a system upgrade on Linux, FreeBSD, and Windows.

## Requirements

Collections:
- `community.general`
- `ansible.windows`
- `chocolatey.chocolatey`

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`).

**General:**

`upgrade_reboot` (default: `false`) - Reboot after upgrade

**APT (Debian/Ubuntu):**

`upgrade_apt_autoremove` (default: `false`) - Run autoremove

`upgrade_apt_type` (default: `dist`) - Upgrade type

`upgrade_apt_cache_valid_time` (default: `1`) - Cache validity in seconds

**Windows:**

`upgrade_windows_update_categories` (default: `['CriticalUpdates', 'SecurityUpdates', 'UpdateRollups', 'DefinitionUpdates']`) - Categories of Windows updates to install

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - pluggero.upgrade
```

## License

MIT / BSD

## Author Information

This role was created in 2025 by Robin Plugge.
