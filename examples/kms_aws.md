# HashiCorp Boundary GCP KMS configuration

Based on https://www.boundaryproject.io/docs/configuration/kms/awskms

## Requirements

* 3 AWS KMS keys
* EC2 node's IAM role must have the following permissions on each KMS key:
  * `kms:Encrypt`
  * `kms:Decrypt`
  * `kms:DescribeKey`

Example Terraform implementation of these requirements:

* https://github.com/hashicorp/boundary-reference-architecture/blob/main/deployment/aws/aws/iam.tf
* https://github.com/hashicorp/boundary-reference-architecture/blob/main/deployment/aws/aws/kms.tf

## Configuration Steps

Create a group_vars file for boundary controller nodes

### `group_vars/boundary_controllers.yml`

Add the KMS instance details

```YAML
# KMS location and auth
boundary_kms_type: 'awskms'
boundary_awskms_region: 'us-east-1'
```

Add the KMS key ids for each type

```YAML
# KMS key IDs
boundary_awskms_keys:
  root: ''
  worker-auth: ''
  recovery: ''
```

## Utilizing a non-default KMS Endpoint

This is useful when connecting to KMS over a VPC Endpoint. If not set, Boundary will use the default API endpoint for your region.

```YAML
boundary_awskms_endpoint: 'https://vpce-Foo-Bar.kms.us-east-1.vpce.amazonaws.com'
```
