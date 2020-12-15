# HashiCorp Boundary Vault Transit KMS configuration

Based on https://www.boundaryproject.io/docs/configuration/kms/transit

## Requirements

* Hashicorp Vault implementation with Transit secret engine
* `VAULT_TOKEN` environment variable for a session with these permissions https://www.boundaryproject.io/docs/configuration/kms/transit#authentication

## Configuration Steps

Create a group_vars file for boundary controller nodes

### `group_vars/boundary_controllers.yml`

Add the Vault transit keystore details

```YAML
# Required settings
boundary_kms_type: 'transit'
vault_instances:
  - vault.example.com
boundary_transit_mount_path: 'transit/'
boundary_transit_namespace: 'ns1'

# Optional settings - safe to leave these out or blank
boundary_transit_disable_renewal: 'false'   # see https://www.boundaryproject.io/docs/configuration/kms/transit#disable_renewal
boundary_transit_tls_skip_verify: 'false'   # really, don't enable this
boundary_transit_tls_server_name: 'vault.example.com'
boundary_transit_tls_ca_cert: '/etc/ssl/certs/vault-ca.cert'
boundary_transit_tls_ca_cert: '/etc/ssl/certs/vault-ca.cert'
boundary_transit_tls_client_cert: '/etc/ssl/certs/vault-client.cert'
boundary_transit_tls_client_key: '/etc/ssl/private/vault-client.key'
```

Add the key names for each type

```YAML
# KMS key IDs
boundary_transit_keys:
  root: '*change_me*'
  worker-auth: '*change_me*'
  recovery: '*change_me*'
```
