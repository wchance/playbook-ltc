# Ansible Playbooks

> Ansible Version: >= 4.6.0

If using ssh-password, the machine that runs the ansible-playbook command should have `sshpass` installed.

The `ansible_user` for the remote host should be added to visudo with `NOPASSWD:ALL` or it's always a requirement for the playbook to be run with `-kK` flags.


# Ethereum Node

The role [provision-eth-node](./roles/provision-eth-node) is the one responsible for provisioning/configuring Etherem Nodes. This role has been tested in Ubuntu LTS-18 and LTS-20.

- Installing Geth
```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-geth" -kK -vvv
```

- Upgrading Geth
```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "upgrade-geth" -kK -vvv
```