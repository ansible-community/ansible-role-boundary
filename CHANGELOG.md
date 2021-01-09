# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [v0.2.0]

### Changes

- Boundary version default to 0.1.4
- README markdown format changes
- Added ChangeLog
- Added version file

## Prior to version history

All changes since fork from [arctiqjacob/ansible-role-boundary](https://github.com/arctiqjacob/ansible-role-boundary)

### Added

- Install from package on Debian, RHEL, and macOS
- Ansible 2.10 support
- bash command completion
- ufw firewall support

### Changed

- database_init is now idempotent and configurable
- controller and worker group names have `boundary_` prefix
