# Boundary Vault Transit KMS configuration

All values used here are documented at [Boundary /docs/configuration/kms/transit](https://www.boundaryproject.io/docs/configuration/kms/transit)

## Requirements

* Hashicorp Vault implementation with Transit secret engine
* `VAULT_TOKEN` environment variable for a session with permissions described at
  [https://www.boundaryproject.io/docs/configuration/kms/transit#authentication]

## Configuration Steps

Create a group_vars file for boundary controller nodes

### `group_vars/boundary_controllers.yml`

Add the Vault transit keystore details

```YAML
boundary_kms_type: 'transit'
boundary_kms:
  root:
    address: 'vault.example.com'
    mount_path: 'transit/'
    namespace: 'ns1'
    key_name: 'transit_root'
  worker-auth:
    ...same...
  recovery:
    ...sames...
```

Any of the values documented at [Boundary /docs/configuration/kms/transit](https://www.boundaryproject.io/docs/configuration/kms/transit) can be used.
