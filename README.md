# Ansible Role: System Updates

[![CI](https://github.com/rroethof/ansible-role-systemupdates/actions/workflows/ci.yml/badge.svg)](https://github.com/rroethof/ansible-role-systemupdates/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![github](https://img.shields.io/badge/GitHub-rroethof-181717.svg?style=flat&logo=github)](https://github.com/rroethof)
[![twitter](https://img.shields.io/badge/Twitter-@rroethof-00aced.svg?style=flat&logo=twitter)](https://twitter.com/rroethof)
[![website](https://img.shields.io/badge/Website-RonnyRoethof-5087B2.svg?style=flat&logo=telegram)](https://ronnyroethof.nl)

Ensures that servers are up to date on Debian/Ubuntu and RedHat-based systems.

## Requirements

No special requirements; this role requires root access. Run it in a playbook with a global `become: true`, or invoke the role with `become: true`:

```yaml
- hosts: all
  roles:
    - role: rroethof.systemupdates
      become: true
```

## Role Variables

Default values are set in `defaults/main.yml`:

```yaml
systemupdates_enabled: true
systemupdates_reboot: false
systemupdates_enforce_serial_execution: true

# Debian/Ubuntu
systemupdates_upgrade_type: "dist"
systemupdates_cache_valid_time: 3600
systemupdates_only_upgrade: false
systemupdates_autoclean: true

# RedHat/CentOS/Fedora
systemupdates_security_only: false
systemupdates_bugfix: true

# General
systemupdates_autoremove: true

# Telegram Notification
systemupdates_telegram_notification: false
systemupdates_telegram_api_token: ""
systemupdates_telegram_chat_id: ""
```

**Role variables explained**

| Name                              | Options                | Required | Description                                                                 |
|------------------------------------|------------------------|----------|-----------------------------------------------------------------------------|
| systemupdates_enabled              | true, false            | No       | Whether to run system updates.                                              |
| systemupdates_reboot               | true, false            | No       | Whether to reboot the system after updates.                                 |
| systemupdates_enforce_serial_execution | true, false        | No       | Enforce serial execution for clustered services.                            |
| systemupdates_upgrade_type         | upgrade, dist          | No       | The upgrade type for apt (`upgrade` or `dist`).                             |
| systemupdates_cache_valid_time     | Integer (seconds)      | No       | How long the apt/yum cache is considered valid before updating.             |
| systemupdates_only_upgrade         | true, false            | No       | Only upgrade specified packages (Debian/Ubuntu).                            |
| systemupdates_autoclean            | true, false            | No       | Run `apt-get autoclean` after updates (Debian/Ubuntu).                      |
| systemupdates_security_only        | true, false            | No       | Only install security updates (RedHat/CentOS/Fedora).                       |
| systemupdates_bugfix               | true, false            | No       | Also install bugfix updates (RedHat/CentOS/Fedora, dnf only).               |
| systemupdates_autoremove           | true, false            | No       | Run autoremove after updates.                                               |
| systemupdates_telegram_notification| true, false            | No       | Send a Telegram notification after updates.                                 |
| systemupdates_telegram_api_token   | string                 | No       | Telegram bot API token.                                                     |
| systemupdates_telegram_chat_id     | string                 | No       | Telegram chat ID to send notifications to.                                  |

## Dependencies

None, except for `ansible` (e.g. `pip install ansible`).

## Example Playbook

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request, and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true

  roles:
    - role: rroethof.systemupdates
```

## Setup for development

```sh
python -m pip install --upgrade -r requirements.txt
```
or
```sh
pip install -r requirements.txt
```

## License

MIT / BSD

## Author Information

This role was created in 2025 by [Ronny Roethof](https://ronnyroethof.nl)
