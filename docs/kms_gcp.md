# Boundary GCP CKMS configuration

All values used here are documented at [Boundary /docs/configuration/kms/gcpckms](https://www.boundaryproject.io/docs/configuration/kms/gcpckms).

## Requirements

* GCP CKMS Keyring with keys as declared below

## Configuration Steps

Create a group_vars file for boundary controller nodes

### `group_vars/boundary_controllers.yml`

Add the KMS instance details and the KMS key ids for each type

```YAML
boundary_kms_type: 'gcpckms'
boundary_kms:
  root:
    project: 'foo-bar'
    credentials: '/etc/boundary.d/kms-credentials.json'
    region: 'us-central1'
    key_ring: 'bar-foo'
    crypto_key: '--Cloud KMS resource ID--'
  worker-auth:
    *REPLACE*ME*
  recovery:
    *REPLACE*ME*
```

Use appropriate values for the worker and recovery keys. Any valid value from
[Boundary /docs/configuration/kms/gcpckms](https://www.boundaryproject.io/docs/configuration/kms/gcpckms) can be used here.
