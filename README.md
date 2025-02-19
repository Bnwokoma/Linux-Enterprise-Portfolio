
---

## Project Objectives
Phase 1 of this project focused on the **foundational infrastructure setup**, ensuring all systems are ready for enterprise services.  

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

## Phase 1: Configuration & Setup

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

## Next Steps: Phase 2 Service Deployment
With **Phase 1 completed**, I will now deploy **enterprise services** in **Phase 2**:
- **Apache Web Server (httpd)**
- **MariaDB (MySQL) Database**
- **NFS/Samba for Shared Storage**
- **Automation with Ansible (Planned for later)**

This will transform the infrastructure into a **fully functional enterprise-grade system.**

---

## Conclusion
This project demonstrates **hands-on Linux System Administration skills**, covering:
- **Enterprise server deployment**
- **LVM-based storage solutions**
- **Network configuration with static IPs**
- **Secure SSH authentication**
- **VMware virtualization experience**

**This repository will continue to evolve as I deploy services in the upcoming phases.**  
Stay tuned for **Phase 2: Service Deployment!**

---



