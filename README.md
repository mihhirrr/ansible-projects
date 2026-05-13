# Ansible Projects Repository

A collection of Ansible playbooks and roles for infrastructure automation, configuration management, and cloud deployment.

## 📋 Overview

This repository contains various Ansible projects for automating:
- Container deployment with Docker
- AWS EC2 instance management  
- Web server configuration with Nginx

Each project is self-contained with its own playbooks, roles, and inventory configuration.

## 📁 Directory Structure

### [docker-ansible/](docker-ansible/)
Automates Docker installation and configuration on target hosts.

**Features:**
- Installs Docker using the `bsmeding.docker` Ansible role
- Uses role-based architecture for modularity

**Files:**
- `docker-ansible.yaml` - Main playbook
- `inventory.ini` - Host inventory configuration
- `roles/` - Role dependencies

**Quick Start:**
```bash
cd docker-ansible
ansible-playbook -i inventory.ini docker-ansible.yaml
```

---

### [ec2-manage/](ec2-manage/)
Manages AWS EC2 instances with start, stop, and reboot capabilities.

**Features:**
- Start EC2 instances
- Stop EC2 instances
- Reboot EC2 instances
- Local connection for AWS API interaction

**Roles:**
- `ec2-start/` - Start EC2 instances by instance ID
- `ec2-stop/` - Stop EC2 instances by instance ID
- `ec2-reboot/` - Reboot EC2 instances by instance ID

**Files:**
- `ec2-play.yaml` - Main playbook
- `ansible.cfg` - Ansible configuration
- `roles/` - EC2 management roles

**Quick Start:**
```bash
cd ec2-manage
# Edit ec2-play.yaml to uncomment desired operations
ansible-playbook ec2-play.yaml
```

---

### [nginx/](nginx/)
Installs and configures Nginx web server on target hosts.

**Features:**
- Installs Nginx package
- Starts Nginx service
- Enables auto-start on system boot
- Supports install and uninstall operations

**Files:**
- `install.yml` - Install and configure Nginx
- `uninstall.yml` - Remove Nginx installation
- `inventory` - Host inventory configuration

**Quick Start:**
```bash
cd nginx
# Install Nginx
ansible-playbook -i inventory install.yml

# Uninstall Nginx
ansible-playbook -i inventory uninstall.yml
```

---

## 🚀 Prerequisites

- **Ansible 2.9+** - Core automation tool
- **Python 3.6+** - Required by Ansible
- **SSH access** - To target hosts (with key-based authentication recommended)
- **Boto3** (for ec2-manage) - AWS SDK for Python
- **AWS credentials** (for ec2-manage) - Configured for AWS API access

### Installation

**Install Ansible:**
```bash
pip install ansible
```

**For AWS EC2 management:**
```bash
pip install boto3 botocore
```

---

## 📝 Configuration

### Inventory Setup

Each project includes its own `inventory` or `inventory.ini` file. Update these files with your target hosts:

**Example inventory format:**
```ini
[web]
192.168.1.10 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

[db]
192.168.1.20 ansible_user=admin
```

### SSH Configuration

Make sure your SSH keys have proper permissions:
```bash
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
```

---

## 💡 Usage Examples

### Example 1: Deploy Docker to multiple hosts
```bash
cd docker-ansible
ansible-playbook -i inventory.ini docker-ansible.yaml
```

### Example 2: Install Nginx with specific variables
```bash
cd nginx
ansible-playbook -i inventory install.yml -e "nginx_state=present"
```

### Example 3: Ensure EC2 instance is running
```bash
cd ec2-manage
ansible-playbook ec2-play.yaml --tags "ec2-start"
```

---

## 🔧 Common Ansible Commands

```bash
# Check connectivity to all hosts
ansible all -i inventory -m ping

# Run playbook in check mode (dry-run)
ansible-playbook playbook.yml --check

# Run playbook with verbose output
ansible-playbook playbook.yml -v

# Run specific tags
ansible-playbook playbook.yml --tags "tag-name"

# Run with additional variables
ansible-playbook playbook.yml -e "var1=value1 var2=value2"
```

---

## 📚 Project Dependencies

- **docker-ansible**: Requires `bsmeding.docker` role (can be installed via Ansible Galaxy)
- **ec2-manage**: Requires boto3 and AWS credentials
- **nginx**: Standard Ubuntu/Debian packages

---

## 🛠️ Customization

Each playbook and role can be customized by:

1. **Modifying inventory files** - Change hostnames, SSH keys, users
2. **Updating variables** - Edit group_vars or host_vars files
3. **Adjusting roles** - Modify role tasks, handlers, and defaults
4. **Creating new roles** - Extend playbooks with custom roles

---

## 📄 License

Each subproject may have its own license. Check individual directories for LICENSE files.