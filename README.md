# Ansible Role: HashiCorp Boundary

A role to deploy [HashiCorp Boundary](https://www.boundaryproject.io/)

## Requirements

- A PostgreSQL instance that Boundary workers can reach and authenticate to. The database you plan to use must also exist.
- Access to a KMS solution. This role currently only supports Google Cloud KMS.
- Nodes must be in inventory groups with the substring `boundary_controller` or `boundary_worker` in their name to receive configuration for that service.
  A node in both groups is configured to run both services.

## Installation Variables

### Package Installation

On RedHat and Debian family operating systems, it defaults to installing the packages from Hashicorp's official repository.
You can disable this by setting `boundary_install_package` to false.

### Manual Installation

*The following values are only used for manual installation.*

Controls whether a separate account is created or not and what the user and group should be named.

```YAML
boundary_user: 'boundary'
boundary_group: 'boundary'
boundary_create_account: true
```

Controls what is downloaded, and where it is installed.

```YAML
boundary_archive: 'boundary_{{ boundary_version }}_linux_amd64.zip'
boundary_download: 'https://releases.hashicorp.com/boundary/{{ boundary_version }}/{{ boundary_archive }}'
boundary_data_directory: '/opt/boundary'
boundary_install_directory: '{{ boundary_data_directory }}/bin'
```

## Configuration Variables

Ansible variables are listed below, along with the default values (see `default/main.yml`):

Where to place Boundary's configuration data.

```YAML
boundary_version: '0.1.4'
boundary_home_directory: '/etc/boundary.d'
boundary_config_file: '{{ boundary_home_directory }}/worker.hcl'
boundary_server_file: '{{ boundary_home_directory }}/controller.hcl'
```

### Database initialization flags

Boundary can create an example admin account and organization to help bootstrap you.
This is disabled by default since uses will create the initial resources via Ansible.
If you are building a PoC to learn and explore, you may want to remove this value.

```YAML
boundary_db_init_flags: '-skip-initial-login-role-creation'
```

### Key Management

One of the Boundary KMS types from [https://www.boundaryproject.io/docs/configuration/kms]

As these choices are radically different depending on your KMS, refer to one of these examples:

- [GCP CKMS](docs/kms_gcp.md)
- [AWS KMS](docs/kms_aws.md)
- [Hashicorp Vault - Transit secrets engine](docs/kms_transit.md)
- [Static AEAD Keys](docs/kms_aead.md) - not suitable for production use

It defaults to the static AEAD key configuration documented at [https://www.boundaryproject.io/docs/getting-started]

```YAML
boundary_kms_type: 'aead'
```

Any and all supported kms types can work here, whether examples are listed above or not. All values should be placed in
a map named `boundary_kms` under a distinct name for each key type.

## TLS Configuration

Boundary uses its own TLS implementation for all controller<->worker communications,
however communications with the boundary client will be subject to normal public TLS validation.
Best to create or acquire a certificate which will be trusted by the operating system of the client
and supply that key and certificate as documented at [docs/api_tls.md]

## Dependencies

None.

## Instructions

If you are new to Ansible playbooks and group vars, the following examples can guide you:

- Creating [Boundary Playbook](docs/playbook.md)
- Creating [Boundary Group Vars](docs/group_vars.md)

## Author Information

Jacob Mammoliti
Bas Meijer
Jo Rhett
