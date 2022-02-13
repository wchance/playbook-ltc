# Ansible Playbooks

> Ansible Version: >= 4.6.0

If using ssh-password, the machine that runs the ansible-playbook command should
have `sshpass` installed.

The `ansible_user` for the remote host should be added to visudo with
`NOPASSWD:ALL` or it's always a requirement for the playbook to be run with
`-kK` flags.

# Ethereum Node

The role [provision-eth-node](./roles/provision-eth-node) is the one responsible
for provisioning/configuring Etherem Nodes. This role has been tested in Ubuntu
LTS-18 and LTS-20.

:pushpin: Before running the playbooks.yml, make sure to update the
`ansible_user` variable in the [inventory](./inventory/all.yml)

- Installing Geth

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-geth" -u <user> --private-key <path-to-key> -kK -vvv
```

- Upgrading Geth

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "upgrade-geth" -u <user> --private-key <path-to-key> -kK -vvv
```

- Updating Geth

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "update-geth" -u <user> --private-key <path-to-key> -kK -vvv
```

- Installing Cronjob

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-eth-node-cronjobs" --private-key <path-to-key> -kK -vvv
```

# Polygon Node

The role [provision-matic-node](./roles/provision-matic-node) is the one
responsible for provisioning/configuring Polygoin Nodes. This role has been
tested in Ubuntu LTS-18 and LTS-20.

:pushpin: Before running the playbooks.yml, make sure to update the
`ansible_user` variable in the [inventory](./inventory/all.yml)

- Installing Dependency

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-dependency-matic" --private-key <path-to-key> -kK -vvv
```

- Installing Matic

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-matic" -u <user> --private-key <path-to-key> -kK -vvv
```

:warning: After running the install-matic tasks, stop `bor.service`. Only start
bor when heimdall is synced. Stop bor by running `systemctl stop bor.service`.
Check if heimdall is sync by running `curl localhost:26657/status`

:pushpin: Check heimdall logs `journalctl -u heimdalld.service -f`

:pushpin: Check heimdall rest-server logs
`journalctl -u heimdalld-rest-server.service -f`

:pushpin: Check bor logs `journalctl -u bor.service -f`

- Installing Snaphots - Matic

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-snapshot-matic" -u <user> --private-key <path-to-key> -kK -vvv
```

- Checking Snapshot installation - Matic

```
ANSIBLE_STDOUT_CALLBACK=unixy ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "matic-snapshot-checker" -u <user> --private-key <path-to-key> -kK
```

- Upgrading Matic

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "upgrade-matic" -u <user> --private-key <path-to-key> -kK -vvv
```

- Installing Cronjob

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-matic-node-cronjobs" --private-key <path-to-key> -kK -vvv
```

# Bitcoin Node

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

# Litecoin Node

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

# Gateway Node

The role [provision-gateway-node](./roles/provision-gateway-node) is the one
responsible for provisioning/configuring Gateway Nodes or the reverse-proxy
servers.

- Install MIA Gateway

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-mia-gateway" -u <user> --private-key <path-to-key> -kK -vvv
```

- Install SJO Gateway

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-sjo-gateway" -u <user> --private-key <path-to-key> -kK -vvv
```

# Avalanche Node

The role [provision-avax-node](./roles/provision-avax-node) is the one
responsible for provisioning/configuring Avalanche Nodes.

- Install Avalanche

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-dependency-avax" -u <user> --private-key <path-to-key> -kK -vvv

ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-avax" -u <user> --private-key <path-to-key> -kK -vvv
```

# Cardano Node

The role [provision-ada-node](./roles/provision-ada-node) is the one responsible
for provisioning/configuring Cardano Nodes.

- Install Avalanche

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-dependency-ada" -u <user> --private-key <path-to-key> -kK -vvv

ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-ada" -u <user> --private-key <path-to-key> -kK -vvv
```

:pushpin: After the `/tmp/build.log` shows "cardano-full-node can now be
started", run the command `sudo systemctl restart cardano.service` to for the
cardano service to be activated.
