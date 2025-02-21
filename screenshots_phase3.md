# 📸 Phase 3 Screenshots Documentation

This file contains all **Phase 3 screenshots** with descriptions.

---

## 🔥 Security Hardening

- **SELinux Status Verification (`sestatus`)**
  ![SELinux Status - Primary](screenshots/Phase3/selinux_status_primary.png)

- **SELinux HTTP & HTTPS Policies**
  ![SELinux HTTP Services](screenshots/Phase3/selinux_httpservices.png)
  ![SELinux HTTPS Enabled](screenshots/Phase3/selinux_httpsservicesOn.png)

- **SSH Security Hardening**
  ![SSH Security Hardening](screenshots/Phase3/ssh_security_hardening.png)

---

## 🔒 Fail2Ban Configuration

- **Fail2Ban Jail Config (`/etc/fail2ban/jail.local`)**
  ![Fail2Ban Jail Config](screenshots/Phase3/fail2ban_jail_config.png)

- **Fail2Ban Status (`fail2ban-client status sshd`)**
  ![Fail2Ban Status](screenshots/Phase3/fail2ban_status_primary.png)

- **Auditd Logs for Failed Logins**
  ![Auditd Failed Logins](screenshots/Phase3/auditd_failed_logins.png)

---

## ⚙️ Ansible Automation

- **Ansible Ping Test (`ansible all -m ping`)**
  ![Ansible Ping Test](screenshots/Phase3/ansible_ping_nodes.png)
- **Ansible Playbook for Firewall**
  ![Firewall Playbook](screenshots/Phase3/firewall_playbook_yaml.png)

- **Firewall Playbook Execution**
  ![Firewall Playbook Executed](screenshots/Phase3/firewall_playbookRan_yaml.png)

- **Ansible Playbook for User Management**
  ![Ansible Users Playbook](screenshots/Phase3/ansible_users_playbook.png)

- **Ansible Playbook Execution for Users**
  ![Users Playbook Executed] (screenshots/Phase3/ansible_users_playbookRan.png)

- **User Created via Ansible**
  ![Users.yml User Creation](screenshots/Phase3/users_yml_userCreation.png)

- **User Forced to Change Password at Login**
  ![Users.yml Change Login](screenshots/Phase3/users_yml_changeLogin.png)

---

## 📜 Centralized Logging

- **Firewall Ports Open for Logging Server**
  ![Logging Server Firewalld Ports](screenshots/Phase3/loggingserver_firewalld_ports.png)

- **Logging Test Output**
  ![Logging Test Output](screenshots/Phase3/logging_test_output.png)

---
