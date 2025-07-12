
# Ansible Role: ansible-role-systemupdates

[![CI](https://github.com/rroethof/ansible-role-systemupdates/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/rroethof/ansible-role-systemupdates/actions/workflows/ci.yml)
![GitHub last commit](https://img.shields.io/github/last-commit/rroethof/ansible-role-systemupdates)
![GitHub Issues or Pull Requests](https://img.shields.io/github/issues/rroethof/ansible-role-systemupdates)
![Ansible Role](https://img.shields.io/ansible/role/d/rroethof/ansible-role-systemupdates)
[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

[![github](https://img.shields.io/badge/GitHub-rroethof-181717.svg?style=flat&logo=github)](https://github.com/rroethof)
[![twitter](https://img.shields.io/badge/Twitter-@rroethof-00aced.svg?style=flat&logo=twitter)](https://twitter.com/rroethof)
[![website](https://img.shields.io/badge/Website-RonnyRoethof-5087B2.svg?style=flat&logo=telegram)](https://roethof.net)
[![website](https://img.shields.io/badge/Resume-RonnyRoethof-5087B2.svg?style=flat&logo=telegram)](https://ronnyroethof.nl)

> **A reusable Ansible role ansible-role-systemupdates for quickly starting new roles with best practices, CI, and Molecule testing.**

---

## Table of Contents

- [Ansible Role: ansible-role-systemupdates](#ansible-role-ansible-role-systemupdates)
  - [Table of Contents](#table-of-contents)
  - [Supported Platforms](#supported-platforms)
  - [Requirements](#requirements)
  - [Installation](#installation)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
  - [Example Playbook](#example-playbook)
  - [Linting](#linting)
  - [Testing](#testing)
    - [Running Tests Locally](#running-tests-locally)
  - [CI Pipeline](#ci-pipeline)
  - [License](#license)
  - [Changelog](#changelog)
  - [Security](#security)
  - [Contributing](#contributing)
  - [Issues \& Support](#issues--support)

This repository provides a ansible-role-systemupdates for creating new Ansible roles, including:

- A recommended directory structure
- Example Molecule scenarios for testing
- CI integration (GitHub Actions)
- Documentation and best practices

**To customize this ansible-role-systemupdates for your own role, run the provided [`rename.sh`](https://github.com/rroethof/ansible-role-systemupdates/blob/main/rename.sh) script. This will update the role name, author, namespace, and related information throughout the project.**

## Supported Platforms

- **Debian**
  - Debian 12 (Bookworm)
  - Debian 13 (Trixie)
- **Ubuntu**
  - Ubuntu 22.04 LTS (Jammy)
  - Ubuntu 24.04 LTS (Noble)
- **Enterprise Linux**
  - EL 9

## Requirements

- Ansible >= 2.10
- Python 3.x
## Installation

Install this role from Ansible Galaxy:

```
ansible-galaxy install rroethof.ansibleansible-role-systemupdates
```

## Role Variables


Default values are defined in [`defaults/main.yml`](defaults/main.yml):

| Variable | Default | Description |
|----------|---------|-------------|
| systemupdates_enabled | true | Master switch to enable/disable the role |
| systemupdates_reboot | false | Reboot server if required after updates |
| systemupdates_enforce_serial_execution | true | Enforce serial execution (recommended for clusters) |
| systemupdates_upgrade_type | "dist" | Type of upgrade for Debian/Ubuntu |
| systemupdates_cache_valid_time | 3600 | Apt cache validity in seconds |
| systemupdates_only_upgrade | false | Only upgrade specified packages |
| systemupdates_autoclean | true | Run 'apt-get autoclean' after updates |
| systemupdates_security_only | false | Only install security updates (RHEL) |
| systemupdates_bugfix | true | Also install bugfix updates (dnf) |
| systemupdates_autoremove | true | Run autoremove after updates |

See [`defaults/main.yml`](defaults/main.yml) for all available variables and their descriptions.

## Dependencies

See [`meta/main.yml`](meta/main.yml) for dependencies.

## Example Playbook

Example playbook:

```yaml
- hosts: all
  become: yes
  roles:
    - role: rroethof.systemupdates
      vars:
        systemupdates_reboot: true
```
## Linting

Lint je role met [ansible-lint](https://ansible-lint.readthedocs.io/):

```shell
ansible-lint .
```

## Testing

This role is tested using [Molecule](https://molecule.readthedocs.io/) with the following matrix:

- Debian 12
- Ubuntu 22.04

### Running Tests Locally

1. Install Python dependencies:

   ```
   python -m pip install --upgrade -r requirements.txt
   ```

2. Run tests for a specific distribution:

   ```
   # For Debian 12
   $env:MOLECULE_DISTRO="debian12"; molecule test

   # For Ubuntu 22.04
   $env:MOLECULE_DISTRO="ubuntu2404"; molecule test
   ```


The CI pipeline automatically tests all supported distributions on each push and pull request.

## CI Pipeline

Continuous Integration is provided via [GitHub Actions](https://github.com/rroethof/ansible-role-systemupdates/blob/main/.github/workflows/ci.yml):

- **Linting:** Runs yamllint and ansible-lint to check YAML and Ansible code quality.
- **Molecule Testing:** Runs Molecule tests in Docker for each supported distribution (Debian 12, Ubuntu 24.04, etc.).
- **(Optional) Galaxy Import:** The workflow includes a commented-out job to automatically import the role to Ansible Galaxy when changes are pushed to the main branch. To enable this, simply ensure you have set the **`GALAXY_API_KEY`** secret in your repository settings.

All pushes, pull requests, and releases are tested using Molecule. This ensures your role remains linted and tested across supported platforms.

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/rroethof/ansible-role-systemupdates/blob/main/LICENSE) file for details.

## Changelog

See [CHANGELOG.md](https://github.com/rroethof/ansible-role-systemupdates/blob/main/CHANGELOG.md) for a list of all notable changes to this project.

## Security

Please see our [Security Policy](https://github.com/rroethof/ansible-role-systemupdates/blob/main/SECURITY.md) for reporting vulnerabilities.

## Contributing

Contributions are welcome! Please read our [Contributing Guide](https://github.com/rroethof/ansible-role-systemupdates/blob/main/CONTRIBUTING.md) and [Code of Conduct](https://github.com/rroethof/ansible-role-systemupdates/blob/main/CODE_OF_CONDUCT.md) before submitting a Pull Request.

---

## Issues & Support

If you have any questions, feature requests, or find a bug, please [open an issue](https://github.com/rroethof/ansible-role-systemupdates/issues).

---
  
<sub>Author: Ronny Roethof ([ronny@roethof.net](mailto:ronny@roethof.net))</sub>
