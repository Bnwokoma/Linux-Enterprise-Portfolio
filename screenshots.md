# 📸  Phase 1 Screenshots Documentation

---

## 1️⃣ Network Configuration
- **Primary VM - IP Address Configuration (`ip a`)**  
  ![IP Address - Primary](ip_a_primary.png)

- **Primary VM - `nmtui` Interface (Static IP Setup)**  
  ![nmtui - Primary](nmtui_primary.png)

---

## 2️⃣ Disk & Storage Configuration
- **Primary VM - Disk Layout (`lsblk`)**  
  ![lsblk - Primary](lsblk_primary.png)

- **Client VM - Disk Layout (`lsblk`)**  
  ![lsblk - Client](lsblk_client.png)

- **Storage VM - Disk Layout (`lsblk`)**  
  ![lsblk - Storage](lsblk_storage.png)

- **LVM Storage Setup (`lsblk` showing additional storage volumes)**  
  ![LVM Storage](lvm_storage.png)

---

## 3️⃣ Network Connectivity Testing
- **Ping Test - Verifying VM Connectivity**  
  ![Ping Test](ping_testing.png)

---

## 4️⃣ Firewall Configuration
- **Firewall Rules - Allowed Services (`firewall-cmd --list-services`)**  
  ![Firewall Services - Primary](firewall_services_primary.png)

## 5️⃣ SSH Key-Based Authentication
- **Successful SSH Login Without Password**  
  ![SSH Authentication](KeyBased_authentication.png)

# 📸 Phase 2 Screenshots Documentation

---

## 1️⃣ Apache Web Server Setup (Primary VM)
- **Apache Status**  
  ![Apache Status](../screenshots/apache_test_page_primary.png)
- **Firewall HTTP/HTTPS Rules**  
  ![Firewall Rules](../screenshots/firewall_http_https_primary.png)

---

## 2️⃣ MariaDB Installation & Configuration (Primary VM)
- **MariaDB Connection Test**  
  ![MariaDB Connection](../screenshots/mariadb_connection_primary.png)
- **MariaDB Secure Installation**  
  ![MariaDB Secure Installation](../screenshots/mysql_secure_installation_primary.png)

---

## 3️⃣ NFS Shared Storage Configuration (Storage VM & TrueNAS)
- **TrueNAS NFS Settings**  
  ![TrueNAS NFS Settings](../screenshots/truenas_nfs_settings.png)
- **Mounted NFS Storage**  
  ![NFS Mount on Storage](../screenshots/nfs_mount_storage.png)

---

## 4️⃣ Automated Backup with `rsync` (Primary & Storage VMs)
- **Cronjob Setup (Primary VM)**  
  ![rsync Cronjob - Primary](../screenshots/rsync_cronjob_primary.png)
- **Backup Files Verified on TrueNAS**  
  ![Backup Verified](../screenshots/truenas_backup_verified.png)
- **Backup Files Verified on Storage VM**  
  ![Backup Verified - Storage](../screenshots/backup_files_verified_storage.png)

---

# 📸 Phase 3 Screenshots Documentation

This file contains all **Phase 3 screenshots** with descriptions.

---

## 🔥 Security Hardening

- **SELinux Status Verification (`sestatus`)**
  ![SELinux Status - Primary](Phase3/selinux_status_primary.png)

- **SELinux HTTP & HTTPS Policies**
  ![SELinux HTTP Services](Phase3/selinux_httpservices.png)
  ![SELinux HTTPS Enabled](Phase3/selinux_httpsservices.png)

- **SSH Security Hardening**
  ![SSH Security Hardening](Phase3/ssh_security_hardening.png)

---

## 🔒 Fail2Ban Configuration

- **Fail2Ban Jail Config (`/etc/fail2ban/jail.local`)**
  ![Fail2Ban Jail Config](Phase3/fail2ban_jail_config.png)

- **Fail2Ban Status (`fail2ban-client status sshd`)**
  ![Fail2Ban Status](Phase3/fail2ban_status_primary.png)

- **Auditd Logs for Failed Logins**
  ![Auditd Failed Logins](Phase3/auditd_failed_logins.png)

---

## ⚙️ Ansible Automation

- **Ansible Ping Test (`ansible all -m ping`)**
  ![Ansible Ping Test](Phase3/ansible_ping_nodes.png)

- **Ansible Playbook for Firewall**
  ![Firewall Playbook](Phase3/firewall_playbook_yaml.png)

- **Firewall Playbook Execution**
  ![Firewall Playbook Ran](Phase3/firewall_playbookRan_yaml.png)

- **Ansible Playbook for User Management**
  ![Ansible Users Playbook](Phase3/ansible_users_playbook.png)

- **Ansible Playbook Execution for Users**
  ![Users Playbook Ran](Phase3/ansible_users_playbookRan.png)

- **User Created via Ansible**
  ![Users.yml User Creation](Phase3/users_yml_userCreation.png)

- **User Forced to Change Password at Login**
  ![Users.yml Change Login](Phase3/users_yml_changeLogin.png)

---

## 📜 Centralized Logging

- **Firewall Ports Open for Logging Server**
  ![Logging Server Firewalld Ports](Phase3/loggingserver_firewalld_ports.png)

- **Logging Test Output**
  ![Logging Test Output](Phase3/logging_test_output.png)

