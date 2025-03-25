# OpenStack Deployment Using Ansible

## Overview
This repository provides an automated method to deploy OpenStack using Ansible. OpenStack-Ansible simplifies the process of installing, configuring, and managing an OpenStack cloud environment.

## Prerequisites
Before deploying OpenStack, ensure the following:
- **Operating System**: Ubuntu 20.04 LTS or CentOS 8
- **Hardware Requirements**:
  - At least 3 nodes (Controller, Compute, Storage)
  - Minimum 16GB RAM, 4 vCPUs per node
  - Sufficient storage and network configuration
- **Dependencies**:
  - Ansible (latest stable version)
  - Python3 and required libraries
  - Git installed on all nodes
  
## Deployment Steps

### 1. Install Required Packages
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y git python3-pip
sudo pip3 install ansible
```

### 2. Clone OpenStack-Ansible Repository
```bash
git clone https://opendev.org/openstack/openstack-ansible.git
cd openstack-ansible
```

### 3. Configure Inventory and Variables
Modify the inventory file (`/etc/openstack_deploy`) based on your infrastructure setup.

Example Inventory:
```ini
[controller]
controller-node ansible_host=192.168.1.10

[compute]
compute-node1 ansible_host=192.168.1.11
compute-node2 ansible_host=192.168.1.12

[storage]
storage-node1 ansible_host=192.168.1.13
```

Edit `user_variables.yml` for custom configurations.

### 4. Run Ansible Playbooks
Run a dry-run to check configurations:
```bash
ansible-playbook -i hosts site.yml --check
```

Execute the deployment:
```bash
ansible-playbook -i hosts site.yml
```

### 5. Verify OpenStack Services
Once deployment is completed, verify the services:
```bash
openstack service list
```

Check if the Horizon dashboard is accessible via the browser.

## Post-Deployment Management
- Use Ansible for scaling and managing configurations.
- Regularly update packages and apply security patches.
- Monitor logs and services using OpenStack CLI.

## Troubleshooting
- Check logs in `/var/log/openstack`
- Use Ansible verbosity for debugging:
  ```bash
  ansible-playbook -i hosts site.yml -vvv
  ```

For more details, refer to the [OpenStack-Ansible Documentation](https://docs.openstack.org/openstack-ansible/latest/).

## License
This project is licensed under the MIT License.

