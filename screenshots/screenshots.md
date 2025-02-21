## 📂 Phase 1: Foundational Setup

- **Primary VM - IP Address Configuration (`ip a`)**  
  ![IP Address - Primary](Phase1/ip_a_primary.png)

- **Primary VM - `nmtui` Interface (Static IP Setup)**  
  ![nmtui - Primary](Phase1/nmtui_primary.png)

- **Primary VM - Disk Layout (`lsblk`)**  
  ![lsblk - Primary](Phase1/lsblk_primary.png)

- **LVM Storage Setup (`lsblk` showing additional storage volumes)**  
  ![LVM Storage](Phase1/lvm_storage.png)

- **Firewall Rules - Allowed Services (`firewall-cmd --list-services`)**  
  ![Firewall Services - Primary](Phase1/firewall_services_primary.png)

- **Successful SSH Login without Password**  
  ![SSH Authentication](Phase1/KeyBased_authentication.png)

---
## 📂 Phase 2: Service Deployment

- **Apache Web Server - Test Page**  
  ![Apache Test Page - Primary](Phase2/apache_test_page_primary.png)

- **MariaDB Connection Verification**  
  ![MariaDB Connection - Primary](Phase2/mariadb_connection_primary.png)

- **MySQL Secure Installation Completed**  
  ![MySQL Secure Installation - Primary](Phase2/mysql_secure_installation_primary.png)

- **NFS Mount Verification on Storage Server**  
  ![NFS Mount - Storage](Phase2/nfs_mount_storage.png)

- **TrueNAS NFS Settings**  
  ![TrueNAS NFS Settings](Phase2/truenas_nfs_settings.png)

- **Automated Backup Configuration (`rsync` + `cronjob`)**  
  ![Rsync Cronjob - Primary](Phase2/rsync_cronjob_primary.png)

---

## 📸 Phase 3 Screenshots Documentation

### 🔐 Security Hardening
- **SELinux Status Check**  
  ![SELinux Status](Phase3/selinux_status_primary.png)

- **Fail2Ban Jail Status**  
  ![Fail2Ban SSH Jail](Phase3/fail2ban_status_primary.png)

### 👥 User Management
- **User Creation with Ansible**  
  ![User Creation Playbook](Phase3/ansible_users_playbook.png)

- **Forced Password Change on Login**  
  ![Password Change Required](Phase3/forced_password_change.png)

### 🔥 Firewall & Security
- **Firewall Rules Configuration**  
  ![Firewall Playbook](Phase3/firewall_playbook_yaml.png)

### 📜 Centralized Logging
- **Logging Test Output**  
  ![Logging Server](Phase3/logging_test_output.png)

