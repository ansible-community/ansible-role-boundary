# Boundary AEAD KMS configuration

From: [Boundary /docs/configuration/kms/aead](https://www.boundaryproject.io/docs/configuration/kms/aead)
> This is mostly used for dev workflows or testing. The key will be exposed to anyone that can view the configuration file.

## Requirements

* 3 unique base64-encoded AEAD keys

## Configuration Steps

Create a group_vars file for boundary controller nodes

### `group_vars/boundary_controllers.yml`

Replicate the entire default block for 'boundary_kms' from `defaults/main.yml', and add your own base64-encoded AEAD keys for each type

```YAML
boundary_kms_type: 'aead'
boundary_kms:
  root:
    aead_type: 'aes-gcm'
    key_id: 'global_root'
    key: 'sP1fnF5Xz85RrXyELHFeZg9Ad2qt4Z4bgNHVGtD6ung='
  worker-auth:
    *REPLACE*ME*
  recovery:
    *REPLACE*ME*
```
