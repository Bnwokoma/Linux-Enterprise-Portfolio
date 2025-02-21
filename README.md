# Enterprise RHEL 9 Infrastructure Project

**A real-world, enterprise-grade Linux infrastructure deployment using RHEL 9.**  
This project simulates a **secure, automated, and production-ready environment**, showcasing **Linux System Administration, storage management, and networking.**

---

## 📌 Project Overview

This project is divided into **three key phases**, each focusing on a critical aspect of enterprise Linux infrastructure:

### **🛠 Phase 1: Foundational Setup**
- Installation and configuration of **RHEL 9 virtual machines**  
- **Static IP networking** for stable connectivity  
- **Logical Volume Manager (LVM)** for flexible storage management  
- **Secure SSH access** with key-based authentication  
- Preparation for **service deployment**  

---

### **Phase 2: Service Deployment**
- **Apache Web Server (httpd)** installation and verification  
- **MariaDB (MySQL) database** setup and security hardening  
- **NFS shared storage** configuration using **TrueNAS**  
- **Automated backups** using `rsync` and **cron jobs**  

---

### **🔒 Phase 3: Security Hardening & Automation**
- Implementing **firewall rules** and **SELinux policies**  
- Securing SSH with **fail2ban** and key-based authentication  
- **Automating system updates** and security policies with **Ansible**  
- Configuring **monitoring and logging** for enterprise compliance  

---

Each phase builds upon the previous one, creating a **scalable, secure, and production-ready Linux infrastructure.**
---
# Phase 1: Infrastructure Setup

## Project Objectives
Phase 1 of this project focuses on the **foundational infrastructure setup**, ensuring all systems are ready for enterprise services.  

### Key Deliverables
- **Installation and configuration of RHEL 9 virtual machines.**
- **Static IP networking across multiple servers.**
- **Logical Volume Manager (LVM) configuration for flexible storage management.**
- **Secure SSH access with key-based authentication.**
- **Preparation for service deployment in Phase 2.**

---

## Infrastructure Overview
The project consists of **three RHEL 9 virtual machines** running in **VMware Workstation**, each serving a distinct role.

| **VM**          | **Role**                 | **CPU** | **RAM** | **Disk** |
|---------------|-------------------------|--------|--------|--------|
| `RHEL9-Primary` | Web & Database Server  | 2 vCPU | 4GB    | 30GB   |
| `RHEL9-Client`  | Test Client            | 1 vCPU | 2GB    | 15GB   |
| `RHEL9-Storage` | NFS/Samba Backup Server | 2 vCPU | 2GB    | 20GB   |

---

### 1. Networking: Static IP Assignment
Each VM was assigned a **static IP** to ensure stable connectivity:

| **VM**          | **IP Address**  | **Subnet Mask**  | **Gateway** |
|---------------|---------------|----------------|------------|
| `RHEL9-Primary` | `192.168.1.100` | `255.255.255.0` | `192.168.1.1` |
| `RHEL9-Client`  | `192.168.1.101` | `255.255.255.0` | `192.168.1.1` |
| `RHEL9-Storage` | `192.168.1.102` | `255.255.255.0` | `192.168.1.1` |

Configured using `nmtui`, then verified with:

```bash
ip a
ping -c 3 192.168.1.101  # Test connectivity
```

---

### 2. Storage: LVM-Based Disk Management
To ensure **scalability**, I configured **Logical Volume Manager (LVM).**

| **VM**          | **LVM Volume**  | **Size**  | **Purpose** |
|---------------|---------------|--------|------------|
| `RHEL9-Primary` | `rhel-root`  | 18.6G  | OS Filesystem |
| `RHEL9-Client`  | `rhel-root`  | 11.9G  | OS Filesystem |
| `RHEL9-Storage` | `rhel-root`  | 16.4G  | OS Filesystem |
| `RHEL9-Storage` | `lv_storage` | 5G     | Shared Storage |

Key LVM commands used:
```bash
lsblk  # Verify disk structure
lvcreate -L 5G -n lv_storage rhel 
mkfs.xfs /dev/rhel/lv_storage
mount /dev/rhel/lv_storage /mnt/storage
```

---

### 3. Secure SSH Access: Key-Based Authentication
To allow secure, **passwordless SSH login**, I configured key-based authentication.

#### Steps Taken
1. **Generated SSH keys on `RHEL9-Primary`:**
   ```bash
   ssh-keygen -t rsa -b 4096
   ```
2. **Copied keys to `RHEL9-Client` & `RHEL9-Storage`:**
   ```bash
   ssh-copy-id sysadmin@192.168.1.101
   ssh-copy-id sysadmin@192.168.1.102
   ```
3. **Verified login without password:**
   ```bash
   ssh sysadmin@192.168.1.101
   ssh sysadmin@192.168.1.102
   ```

If password prompts persisted, **permissions were corrected**:
```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
sudo systemctl restart sshd
```

---
## 📸 Screenshots
All screenshots for **Phase 1** are available [here](screenshots/screenshots.md).

---

## Conclusion
This project demonstrates **hands-on Linux System Administration skills**, covering:
- **Enterprise server deployment**
- **LVM-based storage solutions**
- **Network configuration with static IPs**
- **Secure SSH authentication**
- **VMware virtualization experience**


## Next Steps: Phase 2 Service Deployment
With **Phase 1 completed**, I will now deploy **enterprise services** in **Phase 2**:
- **Apache Web Server (httpd)**
- **MariaDB (MySQL) Database**
- **NFS/Samba for Shared Storage**
- **Automation with Ansible (Planned for later)**

---

**This repository will continue to evolve as I deploy services in the upcoming phases.**  
Stay tuned for **Phase 2: Service Deployment!**

---

# Phase 2: Service Deployment
## Project Objectives


### Key Deliverables
- **Apache Web Server (httpd) installation and verification**
- **MariaDB (MySQL) database setup and security hardening**
- **NFS shared storage configuration using TrueNAS**
- **Automated backups using rsync and cron jobs**

---

### 1. Apache Web Server (httpd)

#### Steps Taken:
1. **Installed Apache**
2. **Enabled and started Apache**
   ```bash
    sudo systemctl enable --now httpd
   ```
3. **Opened firewall ports**
   ```bash
   sudo firewall-cmd --add-service=http --permanent
   sudo firewall-cmd --add-service=https --permanent
   ```
4. **Verified service and tested access**
Visited http://192.168.1.100 in a browser to confirm Apache is running.

---

### 2. MariaDB Database Server

#### Steps Taken:
1. **Installed MariaDB**
2. **Enabled and started MariaDB**
3. **Secured MariaDB**
   ```bash
   sudo mysql_secure_installation
   ```
  - Set root password: Yes
  - Remove anonymous users: Yes
  - Disallow root login remotely: Yes
  - Remove test database: Yes
  - Reload privilege tables: Yes
   
4. **Verified database connection**
   ```bash
   mysql -u root -p
   ```
---

### 3. NFS Shared Storage on TrueNAS

#### Steps Taken:
1. **Configured TrueNAS NFS share via Web Browser UI:**
   
  - Path: /mnt/nas-pool/backups
  - Allowed networks: 192.168.1.0/24
  - Enabled NFSv3 & NFSv4
   
2. **Installed NFS utilities on RHEL9-Storage**
    ```bash
     sudo dnf install nfs-utils -y
    ```
3. **Mounted NFS Share on RHEL9-Storage**
   ```bash
   sudo mkdir -p /mnt/nas-backups
   sudo mount -t nfs 192.168.X.X:/mnt/nas-pool/backups /mnt/nas-backups
   ```
4. **Persisted mount in /etc/fstab**
   ```bash
   sudo nano /etc/fstab
   192.168.X.X:/mnt/nas-pool/backups /mnt/nas-backups nfs defaults,_netdev 0 0
   ```
---

### 4. Automated Backups with rsync and cronjobs

#### Steps Taken:
1. **Created backup directories on RHEL9-Storage**
   ```bash
   sudo mkdir -p /mnt/nas-backups/primary
   sudo mkdir -p /mnt/nas-backups/client
   sudo chown -R sysadmin:sysadmin /mnt/nas-backups/ #### Permissions were preventing backups from taking place
   ```
2. **Scheduled automated backups via cron jobs**
   ```bash
    crontab -e
    0 11 * * * rsync -avz /etc/sysconfig sysadmin@192.168.1.102:/mnt/nas-backups/primary/ #### Runs daily backups at 11am
   ```
3. **Confirmed backup files were successfully transferred to the remote NAS server**
   ```bash
   ls -lah /mnt/nas-backups/primary/
   ```
---
## 📸 Screenshots
All screenshots for **Phase 2** are available [here](screenshots/screenshots.md).

---

## Conclusion
This project demonstrates hands-on Linux System Administration skills, covering:

- **Enterprise server deployment**
- **LVM-based storage solutions**
- **Network configuration with static IPs**
- **Secure SSH authentication**
- **VMware virtualization experience**
- **Automated backup strategies**
---

## Next Steps: Phase 3 - Security Hardening & Automation

With Phase 2 completed, I will now focus on enterprise-grade security enhancements in Phase 3:

- **Implementing firewall rules and SELinux policies**
- **Securing SSH with fail2ban and key-based authentication**
- **Automating system updates and hardening with Ansible**
- **Monitoring and logging configurations for compliance**

This phase will ensure a hardened and resilient infrastructure ready for real-world enterprise use.

---

# Enterprise RHEL 9 Infrastructure Project
This phase focuses on **security hardening and automation**, ensuring a **resilient, secure, and manageable** enterprise environment.

---
# Phase 3: Security Hardening & Automation
## Project Objectives
### Key Deliverables
- **Configured Fail2Ban to prevent unauthorized SSH access.**
- **Implemented firewall rules to restrict network access.**
- **Enabled SELinux policies for enhanced security.**
- **Set up centralized logging with a dedicated logging server.**
- **Automated user account management with Ansible.**
- **Implemented system-wide updates and security configurations with Ansible playbooks.**

---

## Infrastructure Overview
Phase 3 introduced a **centralized logging server** while enhancing **security across all VMs**.

| **VM**            | **Role**                         | **CPU** | **RAM** | **Disk** |
|------------------|---------------------------------|--------|--------|--------|
| `logging-server` | Centralized Log Server         | 2 vCPU | 4GB    | 20GB   |
---
### 1. Fail2Ban: SSH Intrusion Prevention
Fail2Ban was installed to **protect SSH from brute-force attacks**. Since Fail2Ban isn’t a dedicated RHEL product, needed to download the epel-release rpm in order to gain access to Fail2Ban

#### Steps Taken
- **Installed Fail2Ban:**
  ```bash
  subscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms
  dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
  sudo dnf install -y fail2ban
  ```
- **Configured SSH jail by modifying `/etc/fail2ban/jail.local`:**
  ```bash
  [sshd]
  enabled = true
  port = ssh
  filter = sshd
  logpath = /var/log/secure
  maxretry = 5
  bantime = 600
  ```
- **Restarted the service and verified it was running:**
  ```bash
  sudo systemctl enable --now fail2ban
  sudo fail2ban-client status sshd
  ```

---

### 2. Firewall Hardening: Restricting Network Access
To ensure only necessary services are accessible, **firewalld rules** were enforced across all VMs. We added http,https,ssh, and nfs in our initial phase. So here I just wanted to verify those services were still accessible.

#### Verified settings:
```bash
sudo firewall-cmd --list-all
```
---
### 3. SELinux Enforcement
By default, SELinux is set to Enforcing. However, nothing beats actually verifying. In this environment, assuming could be a vulnerability on its own.

#### Steps Taken
- **Verified SELinux status:**
  ```bash
  sestatus
  ```
- **Applied SELinux policies for Apache,SSH & NFS:**
  ```bash
	sudo setsebool -P httpd_can_network_connect on
	sudo setsebool -P httpd_can_network_connect_db on
	sudo setsebool -P nfs_export_all_rw on
	sudo setsebool -P ssh_chroot_rw_homedirs on
  ```
---

### 4. Centralized Logging
A new server, Logging Serer,was deployed to **collect logs from all VMs**.
I wanted to centralize the log data and isoloate the critical log data from potential disruptions on production servers.

#### Steps Taken
- **Configured `/etc/rsyslog.conf` on `logging-server`:**
  ```bash
  module(load="imudp")
  input(type="imudp" port="514")
  module(load="imtcp")
  input(type="imtcp" port="514")
  ```
- **Enabled log forwarding from all VMs:**
  ```bash
  echo "*.* @192.168.1.103:514" | sudo tee -a /etc/rsyslog.conf #192.168.1.103 = ip of Log Server
  sudo systemctl restart rsyslog
  ```
- **Verified log collection:**
  ```bash
  sudo tail -f /var/log/messages
  ```
---

### 5. Automating Security with Ansible. 
Ansible was used to **automate user management, system updates, and security policies**.
You can find the remaining playbooks here.

#### Ansible Playbooks Implemented

**Automated User Creation (`users.yml`):**
```yaml
---
- name: Create a new employee account
  hosts: all
  become: yes

  vars_prompt:
    - name: "new_user"
      prompt: "Enter the new employee's username"
      private: no

    - name: "new_password"
      prompt: "Enter a default password for the employee"
      private: yes

  tasks:
    - name: Create a new user
      ansible.builtin.user:
        name: "{{ new_user }}"
        groups: allemployees
        shell: /bin/bash
        password: "{{ 'new_password' | password_hash('sha512') }}"

    - name: Force password change on first login
      ansible.builtin.command:
        cmd: "chage -d 0 {{ new_user }}"
```

---
## 📸 Screenshots
All screenshots for **Phase 3** are available [here](screenshots/screenshots.md).

## Conclusion
This phase successfully implemented enterprise security hardening and automation across multiple RHEL 9 VMs:
- **Fail2Ban for SSH protection**
- **Firewall rules for network security**
- **SELinux for access control**
- **Centralized logging for system monitoring**
- **Ansible automation for user and system management**

This infrastructure is now hardened, automated, and production-ready.


