# HashiCorp Boundary AEAD KMS configuration

From: https://www.boundaryproject.io/docs/configuration/kms/aead
> This is mostly used for dev workflows or testing. The key will be exposed to anyone that can view the configuration file.

## Requirements

* 3 unique base64-encoded AEAD keys

## Configuration Steps

Create a group_vars file for boundary controller nodes

### `group_vars/boundary_controllers.yml`

Add the base64-encoded AEAD keys for each type

```YAML
boundary_kms_type: 'aead'
boundary_aead_keys:
  root: '*REPLACE*ME*'
  worker-auth: '*REPLACE*ME*'
  recovery: '*REPLACE*ME*'
```
