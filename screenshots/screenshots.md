# 📸 Screenshots Documentation

This file contains all **Phase 1 screenshots** with descriptions.

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

# 📸 Screenshots Documentation

This file contains all **Phase 2 screenshots** with descriptions.

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

