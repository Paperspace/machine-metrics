# Paperspace Metrics
This repo contains an Ansible playbook and associated roles for deploying Prometheus Node Exporter, DCGM Exporter, PS Agent, and (optionally) New Relic Openmetrics Integration on a Paperspace machine.

## Requirements
* Python 2.7 or 3.5+
* Ansible

## Operation

### Basic
1. Clone this repository.
2. Create an inventory file `inventory` with the IPs of the target machines.
3. Run the playbook: `ansible-playbook -i inventory metrics.yml`

### Ansible Primer
Depending on how you have your Ansible environment configured, you may need to specify the SSH user and/or SSH key to use when connecting to the target machines. This can be done by adding the following to the `ansible-playbook` command:
* `-u <username>` to specify the SSH user
* `-k` to prompt for the SSH password
* `-K` to prompt for the sudo password
* `-i <path>` to specify the inventory file
* `-e <key>=<value>` to specify extra variables
*  `--private-key <path>` to specify the SSH key

### Extra Variables
The playbook can be configured using the following extra variables:
| Name                     | Description                                                                                                                                                                       | Default |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| `docker_install`         | Whether to install Docker on the target machine. If set to False, the playbook will assume that Docker is already installed and will skip the installation step.                  | True    |
| `node_exporter_install`  | Whether to install Prometheus Node Exporter on the target machine.                                                                                                                | True    |
| `dcgm_exporter_install`  | Whether to install DCGM Exporter on the target machine.                                                                                                                           | True    |
| `ps_agent_install`       | Whether to install the Paperspace Agent on the target machine.                                                                                                                    | True    |
| `nri_prometheus_install` | Whether to install the New Relic Openmetrics Integration on the target machine.                                                                                                   | False   |
| `restart_docker`         | Whether to restart the Docker service on the target machine after installing the DCGM Exporter. This may be necessary for the DCGM Exporter to be able to access the GPU metrics. | False   |
