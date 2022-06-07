# Playbooks for non blockchain nodes

[**RETURN TO MAIN PAGE**](./README.md)

&nbsp;

> Ansible Version: >= 4.6.0

If using ssh-password, the machine that runs the ansible-playbook command should
have `sshpass` installed.

The `ansible_user` for the remote host should be added to visudo with
`NOPASSWD:ALL` or it's always a requirement for the playbook to be run with
`-kK` flags.

![NGINX](./images/nginx.png)
## Gateway Node

The role [provision-gateway-node](./roles/provision-gateway-node) is the one
responsible for provisioning/configuring Gateway Nodes or the reverse-proxy
servers.

SPECIAL NEED: Create the following files in order for the Nginx Basic Auth to work for all HTTP access.
Note that if there's a new endpoint added to the gateway config, it's expected that the htpasswd file for it exists.

```
sudo htpasswd -c /etc/htconfig/ada_htpasswd YOUR_USER
sudo htpasswd -c /etc/htconfig/avax_htpasswd YOUR_USER
sudo htpasswd -c /etc/htconfig/bch_htpasswd YOUR_USER
sudo htpasswd -c /etc/htconfig/matic_htpasswd YOUR_USER
sudo htpasswd -c /etc/htconfig/ltc_htpasswd YOUR_USER
sudo htpasswd -c /etc/htconfig/eth_htpasswd YOUR_USER
sudo htpasswd -c /etc/htconfig/btc_htpasswd YOUR_USER
```

- Install MIA Gateway

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-mia-gateway" -u <user> --private-key <path-to-key> -kK -vvv
```

- Install SJO Gateway

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-sjo-gateway" -u <user> --private-key <path-to-key> -kK -vvv
```
![Prometheus](./images/prometheus.png)
##  Monitoring Node

The role [provision-monitoring-node](./roles/provision-monitoring-node/) is the one 
responsible for provisioning/configuring Promethues, Grafana, Node Exporter, Blackbox Exporter, Alert Manager

- Install Prometheus
> Note: Prometheus only needs to be installed to the monitoring node.

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-prometheus" -u <user> --private-key <path-to-key> -kK -vvv
```

- Install Grafana
> Note: Grafana only needs to be installed to the monitoring node running Prometheus.

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-grafana" -u <user> --private-key <path-to-key> -kK -vvv
```

- Install AlertManager
> Note: AlertManager only needs to be installed to the monitoring node running Prometheus.

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-alertmanager" -u <user> --private-key <path-to-key> -kK -vvv
```

- Install Blackbox Exporter
> Note: Blackbox Exporter only needs to be installed to the monitoring node running Prometheus.

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-blackbox-exporter" -u <user> --private-key <path-to-key> -kK -vvv
```

- Install Node Exporter
> Note: Node Exporter needs to be installed to every host you want to monitor with Prometheus.

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-node-exporter" -u <user> --private-key <path-to-key> -kK -vvv
```

- Install Nginx Proxy
> Note: Nginx only needs to be installed to the monitoring node running Prometheus. SSL Cert is managed by Certbot. Make sure to create the htpasswd for /etc/htconfig/prometheus_htpasswd.

```
ansible-playbook playbooks.yml -i inventory/all.yml -l <host-name> --tags "install-nginx-proxy" -u <user> --private-key <path-to-key> -kK -vvv
```

![Teleport](./images/teleport.webp)
## Teleport Access Server
The role [provision-teleport](./roles/provision-teleport/) is the one 
responsible for provisioning/configuring Teleport Access Server

&nbsp;

[**RETURN TO MAIN PAGE**](./README.md)