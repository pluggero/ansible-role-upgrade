# Ansible Role: System Upgrade

[![CI](https://github.com/pluggero/ansible-role-upgrade/actions/workflows/ci.yml/badge.svg)](https://github.com/pluggero/ansible-role-upgrade/actions/workflows/ci.yml) [![Ansible Galaxy downloads](https://img.shields.io/ansible/role/d/pluggero/upgrade?label=Galaxy%20downloads&logo=ansible&color=%23096598)](https://galaxy.ansible.com/ui/standalone/roles/pluggero/upgrade)

An Ansible Role that performs a system upgrade.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`).

**General:**

`upgrade_reboot` (default: `false`) - Reboot after upgrade, only if actually required (not supported on FreeBSD). The reboot happens immediately after the upgrade step, in the same play, rather than being deferred to the end of the playbook - this avoids later roles/tasks running against a stale, un-rebooted kernel.

`upgrade_interactive` (default: `false`) - Ask for confirmation before rebooting instead of rebooting automatically. If confirmed, the reboot still happens immediately (not deferred to the end of the playbook).

**Unattended Upgrades (Debian/Ubuntu only):**

Background security patching via `unattended-upgrades`, independent of this role's main upgrade task. No-op on Arch, Alpine, FreeBSD, Windows.

| Variable | Default | Description |
| --- | --- | --- |
| `upgrade_unattended_enabled` | `false` | Install and configure `unattended-upgrades` |
| `upgrade_unattended_origins` | `["${distro_id}:${distro_codename}-security"]` | Allowed origins for automatic installation |
| `upgrade_unattended_remove_unused_dependencies` | `true` | Remove unused dependencies after an unattended upgrade |
| `upgrade_unattended_mail_to` | `""` | Mail address for upgrade notifications; empty disables mail |
| `upgrade_unattended_reboot` | `false` | Automatically reboot if required after an unattended upgrade |
| `upgrade_unattended_reboot_time` | `"02:00"` | Daily time to perform the automatic reboot, if required |
| `upgrade_unattended_reboot_with_users` | `false` | Reboot even if users are currently logged in |

**APT (Debian/Ubuntu):**

`upgrade_apt_autoremove` (default: `false`) - Run autoremove

`upgrade_apt_type` (default: `dist`) - Upgrade type

`upgrade_apt_cache_valid_time` (default: `1`) - Cache validity in seconds

`upgrade_apt_dpkg_options` (default: `force-confdef,force-confold`) - dpkg options passed to apt

**Windows:**

`upgrade_windows_update_categories` (default: `[CriticalUpdates, SecurityUpdates, UpdateRollups, DefinitionUpdates]`) - Update categories to install

`upgrade_windows_update_retries` (default: `3`) - Retries for `win_updates`

`upgrade_windows_update_retry_delay` (default: `30`) - Delay in seconds between retries

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - pluggero.upgrade
```

With unattended upgrades and a scheduled reboot:

```yaml
- hosts: all
  roles:
    - role: pluggero.upgrade
      vars:
        upgrade_unattended_enabled: true
        upgrade_unattended_reboot: true
        upgrade_unattended_reboot_time: "03:00"
```

## License

MIT / BSD

## Author Information

This role was created in 2025 by Robin Plugge.
