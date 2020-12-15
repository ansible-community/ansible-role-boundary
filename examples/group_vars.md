# Ansible Role: HashiCorp Boundary group vars example

## Create an inventory file

Create an inventory file with groups for controllers and workers:

```bash
$ cat > inventory <<EOF
[boundary_controllers]
192.168.0.100

[boundary_workers]
192.168.0.101
EOF
```

## Create the group_vars files

```bash
$ echo "---" > group_vars/boundary_workers.yml
$ cat > group_vars/boundary_controllers.yml <<EOF
---
boundary_psql_endpoint: 'pgsql.example.com:5432'
EOF
```

## Database credentials

You'll need to source the username and password for the database from someplace secure.
If you don't have a secrets vault deployed, follow the Ansible guide:

[Encrypting content with Ansible Vault](https://docs.ansible.com/ansible/latest/user_guide/vault.html)

Reference those secrets in the group vars.

## KMS configuration

As KMS configuration is radically different depending on your choice of KMS, refer to one of these examples:

- [GCP CKMS](examples/kms_gcp.md)
- [AWS KMS](examples/kms_aws.md)
- [Hashicorp Vault - Transit secrets engine](examples/kms_transit.md)
- [Static AEAD Keys](examples/kms_aead.md) - not suitable for production use

These values will need to be added to the group vars.
