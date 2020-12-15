# Ansible Playbook: HashiCorp Boundary

The following playbook deploys a single [HashiCorp Boundary](https://www.boundaryproject.io/) controller and worker node using *ansible-boundary-role*.

This assumes you've [created the inventory and group vars files](group_vars.md) as documented.

## Create the Ansible playbook

```bash
$ cat > playbooks/boundary.yml <<EOF
- hosts: boundary_controllers,boundary_workers
  become: yes
  roles:
    - role: boundary
      tags: boundary
```

## Run the playbook

Pass the appropriate arguments for decrypting the database secrets:

```bash
$ ansible-playbook -i inventory playbooks/boundary.yml --ask-vault-pass
```
