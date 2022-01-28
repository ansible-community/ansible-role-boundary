# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [v2.0.0]

### Breaking Changes

- `boundary_psql_*` variables have been combined into the dict `boundary_database` for complete customization
- Boundary will shut down the controllers and migrate the database if the boundary package is updated
- `boundary_tls_disable` is now false by default
- All `boundary_kms_*` parameters have been obsoleted in favor of a map which can hold any documented value.
  The map keys and values should exactly match the Hashicorp documented parameter(s) going forward.

### Added

- `boundary_database` dict can include these previously unavailable keys (plus any more added in the future)
  - `migration_url`
  - `max_open_connections`
- `boundary_start_services` Boolean - defaults to `true` unless Molecule is running
- `boundary_controller_service` String - defaults to `boundary-controller`
- `boundary_controller_parameters` Map - can use used to set other controller params
  - 'public_cluster_addr' is necesssary for AWS nodes with EIP
- `boundary_worker_service` String - defaults to `boundary-worker`
- `boundary_worker_tags` Map[String, Array] - can provide a list of worker tags for directed routing
- `boundary_worker_parameters` Map - can use used to set other worker params
  - 'public_addr' is necesssary for AWS nodes with EIP
- `boundary_worker_controllers` List - IPs to contact controllers on (default: IPs from boundary_controllers node group)
- `boundary_cors_allowed_origins` may be specified
- Node group names can be longer, search is made on substring of group name

## [v1.0.3]

### Fixed

- Always create boundary user and group (if requested) since packages no longer do it
- Ensure `become` is true when adding autocomplete to /etc/profile.d

## [v1.0.2]

### Fixed

- Ensure `become` is true for all required tasks
- Replace deprecated `include` module with `include_tasks` module

## [v1.0.1]

### Fixed

- RedHat installation

## [v1.0.0]

### Breaking Changes

- Boundary cluster TLS is always enabled.
- `boundary_tls_disable` now controls Boundary Controller API TLS
- Configuration variables for Vault transit TLS have changed names.
  *This was required to allow secret-provided key/cert provisioning*

### Added

- Boundary API controller TLS config
- AEAD and AWS KMS types
- Documentation examples for each KMS Type

### Changes

- Boundary config file default paths
- Boundary default KMS `aead` to match Boundary dev deployment
- Start controller before worker

### Removed

- `boundary_tls_*` configuration options

## [v0.2.3]

### Added

- New variables to control Apt and Yum repo locations. Default to Hashicorp, can be overridden now
  - boundary_apt_repo
  - boundary_yum_repo
- YAML lint configuration

## [v0.2.2]

### Fixed

- Fix the flag passed to the database creation, which was wrong in source docs

## [v0.2.1]

### Changes

- Rename boundary_config task to config
- Reverse order of controller and worker config to avoid startup failures
- Fix template to reference unique group name changed earlier

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
