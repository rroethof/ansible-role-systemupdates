# Ansible Role: System Updates

[![CI](https://github.com/rroethof/ansible-role-systemupdates/actions/workflows/ci.yml/badge.svg)](https://github.com/rroethof/ansible-role-systemupdates/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![github](https://img.shields.io/badge/GitHub-rroethof-181717.svg?style=flat&logo=github)](https://github.com/rroethof)
[![twitter](https://img.shields.io/badge/Twitter-@rroethof-00aced.svg?style=flat&logo=twitter)](https://twitter.com/rroethof)
[![website](https://img.shields.io/badge/Website-RonnyRoethof-5087B2.svg?style=flat&logo=telegram)](https://ronnyroethof.nl)

Ensures that servers are up to date.

## Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

```yaml
- hosts: all
  roles:
    - role: rroethof.systemupdates
      become: yes
```

## Role Variables

The default values for the variables are set in `defaults/main.yml`:
```yaml
# Example defaults (edit defaults/main.yml to change)
systemupdates_enabled: true
systemupdates_reboot: false
systemupdates_upgrade_command: "upgrade"
systemupdates_cache_valid_time: 3600
```

**Role variables explained**

| Name                         | Options           | Required | Description                                                                 |
|------------------------------|-------------------|----------|-----------------------------------------------------------------------------|
| systemupdates_enabled        | true, false       | No       | Whether to run system updates.                                              |
| systemupdates_reboot         | true, false       | No       | Whether to reboot the system after updates.                                 |
| systemupdates_upgrade_command| upgrade, dist-upgrade | No   | The upgrade command to use (e.g., `upgrade` or `dist-upgrade`).             |
| systemupdates_cache_valid_time| Integer (seconds)| No       | How long the apt/yum cache is considered valid before updating (in seconds).|

## Dependencies

None, except for `ansible` (e.g. `pip3 install ansible`).

## Example Playbook

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

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

This role was created in 2025 by [Ronny Roethof](https://ronnyroethof.nl).
