# HashiCorp Boundary GCP KMS configuration

Based on https://www.boundaryproject.io/docs/configuration/kms/gcpckms

## Requirements

* GCP CKMS Keyring with keys as declared below

## Configuration Steps

Create a group_vars file for boundary controller nodes

### `group_vars/boundary_controllers.yml`

Add the KMS instance details

```YAML
# KMS location and auth
boundary_kms_type: 'gcpckms'
boundary_gcpckms_project: 'foo-bar'
boundary_gcpckms_credentials: '/etc/boundary.d/kms-credentials.json'
boundary_gcpckms_region: 'us-central1'
boundary_gcpckms_keyring: 'bar-foo'
```

Add the KMS key ids for each type

```YAML
# KMS key IDs
boundary_gcpckms_keys:
  root: ''
  worker-auth: ''
  recovery: ''
```
