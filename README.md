# Ansible Playbooks

> Ansible Version: >= 4.6.0

If using ssh-password, the machine that runs the ansible-playbook command should have `sshpass` installed.

The `ansible_user` for the remote host should be added to visudo with `NOPASSWD:ALL` or it's always a requirement for the playbook to be run with `-kK` flags.


# Ethereum Node

The role [provision-eth-node](./roles/provision-eth-node) is the one responsible for provisioning/configuring Etherem Nodes. This role has been tested in Ubuntu LTS-18 and LTS-20.

:pushpin: Before running the playbooks.yml, make sure to update the `ansible_user` variable in the [inventory](./inventory/all.yml)


- Installing Geth
```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-geth" --private-key <path-to-key> -kK -vvv
```

- Upgrading Geth
```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "upgrade-geth" --private-key <path-to-key> -kK -vvv
```

- Installing Cronjob
```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-eth-node-cronjobs" --private-key <path-to-key> -kK -vvv
```

# Polygon Node

- Installing Dependency
```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-dependency" --private-key <path-to-key> -kK -vvv
```

- Installing Matic
```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-matic" --private-key <path-to-key> -kK -vvv
```