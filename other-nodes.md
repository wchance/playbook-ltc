# # Playbooks for OTHER based blockchains

[**RETURN TO MAIN PAGE**](./README.md)

&nbsp;

> Ansible Version: >= 4.6.0

If using ssh-password, the machine that runs the ansible-playbook command should
have `sshpass` installed.

The `ansible_user` for the remote host should be added to visudo with
`NOPASSWD:ALL` or it's always a requirement for the playbook to be run with
`-kK` flags.

![AVAX](./images/avax@2x.png)
## Avalanche Node

The role [provision-avax-node](./roles/provision-avax-node) is the one
responsible for provisioning/configuring Avalanche Nodes.

- Install Avalanche

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-dependency-avax" -u <user> --private-key <path-to-key> -kK -vvv

ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-avax" -u <user> --private-key <path-to-key> -kK -vvv
```

![ADA](./images/ada@2x.png)
## Cardano Node

The role [provision-ada-node](./roles/provision-ada-node) is the one responsible
for provisioning/configuring Cardano Nodes.

- Install Avalanche

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-dependency-ada" -u <user> --private-key <path-to-key> -kK -vvv

ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-ada" -u <user> --private-key <path-to-key> -kK -vvv

ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-ogmios" -u <user> --private-key <path-to-key> -kK -vvv
```

&nbsp;

[**RETURN TO MAIN PAGE**](./README.md)