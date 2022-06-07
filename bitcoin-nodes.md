# Playbooks for **BITCOIN** based blockchains

[**RETURN TO MAIN PAGE**](./README.md)

&nbsp;

> Ansible Version: >= 4.6.0

If using ssh-password, the machine that runs the ansible-playbook command should
have `sshpass` installed.

The `ansible_user` for the remote host should be added to visudo with
`NOPASSWD:ALL` or it's always a requirement for the playbook to be run with
`-kK` flags.


![BTC](./images/btc%402x.png)
## **Bitcoin (BTC) Node**


The role [provision-btc-node](./roles/provision-btc-node) is the one responsible
for provisioning/configuring BTC Nodes. This role has been tested in Ubuntu
LTS-18 abd LTS-20.

:pushpin: Before running the playbooks.yml, make sure to update the
`ansible_user` variable in the [inventory](./inventory/all.yml)

- Installing Bitcoin Core

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-btccore" -u <user> --private-key <path-to-key> -kK -vvv
```

- Checking Blocks

```
ANSIBLE_STDOUT_CALLBACK=unixy ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "btc-block-checker" -u <user> --private-key <path-to-key> -kK
```

- Install Electrum

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-dependency-electrum-btc" -u <user> --private-key <path-to-key> -kK -vvv

ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-btc-electrum" -u <user> --private-key <path-to-key> -kK -vvv
```
![LTC](./images/ltc@2x.png)
## **Litecoin (LTC) Node**

The role [provision-ltc-node](./roles/provision-ltc-node) is the one responsible
for provisioning/configuring LTC Nodes. This role has been tested in Ubuntu
LTS-18 abd LTS-20.

:pushpin: Before running the playbooks.yml, make sure to update the
`ansible_user` variable in the [inventory](./inventory/all.yml)

- Installing Litecoin Core

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-ltccore" -u <user> --private-key <path-to-key> -kK -vvv
```

- Install Electrum

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-dependency-electrum-ltc" -u <user> --private-key <path-to-key> -kK -vvv

ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-ltc-electrum" -u <user> --private-key <path-to-key> -kK -vvv
```

![BCH](./images/bch@2x.png)
## **Bitcoin Cash (BCH) Node**

The role [provision-bch-node](./roles/provision-bch-node) is the one responsible
for provisioning/configuring BCH Nodes. This role has been tested in Ubuntu
LTS-18 abd LTS-20.

:pushpin: Before running the playbooks.yml, make sure to update the
`ansible_user` variable in the [inventory](./inventory/all.yml)

- Installing BitcoinCash Core

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-bchcore" -u <user> --private-key <path-to-key> -kK -vvv
```

- Install Electrum

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-dependency-electrum-bch" -u <user> --private-key <path-to-key> -kK -vvv

ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-bch-electrum" -u <user> --private-key <path-to-key> -kK -vvv
```

&nbsp;

[**RETURN TO MAIN PAGE**](./README.md)