# Portable Server
***Developed by: PHILIP SIMON DEROCK P***

## Project Overview

This project demonstrates how to transform an old laptop into a fully functional *Portable Server*. The server is configured for wireless operation using Wi-Fi and mobile hotspots. It supports services like web hosting, file sharing, and real-time application deployment. This guide provides a comprehensive walkthrough of the server setup process, including installation, configuration, and service deployment.


## Components

### Hardware Components

- **Laptop**: Lenovo E41-25
- **Processor**: AMD PRO A4-4350B, 2.50 GHz
- **RAM**: CRUCIAL DDR4 4GB RAM
- **Storage**: WD Green 240 GB SATA SSD
- **Network Interface**: Realtek PCIe GbE Family Controller
- **Additional Hardware**: RJ45 Cable, Dual Band Fibernet Wi-fi Router

### Software Components

- **Operating System**: Ubuntu Live Server 22.04.2
- **Web Server**: Apache2
- **Containers**: Docker
- **FTP Server**: Vsftpd
- **Java**: JDK 21
- **Network Management Tools**: Network-manager, wpasupplicant
- **Performance Monitoring**: Nload 0.7.4

---

## Key Features

- Compact form factor for mobility.
- Low power consumption with high-efficiency hardware.
- Capabilities include web hosting, file sharing, database management.
- Wireless connectivity using Wi-Fi and mobile hotspots.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Installation and Configuration](#installation-and-configuration)
3. [Initial Server Configuration](#initial-server-configuration)
4. [Server Services](#server-services)
5. [Connecting Server Over Wi-Fi](#connecting-server-over-wi-fi)
6. [Analysis](#analysis)
7. [Figures](#figures)
8. [Conclusion](#conclusion)
9. [References](#references)

---

## Introduction

One might have something in mind that would benefit from having an "always-on, always-available" computer. This project explores repurposing an old Lenovo laptop to act as a Linux server with dual-boot functionality for portability and flexibility.

By installing a lightweight Linux distribution like Ubuntu Server, we maximize resource utilization, extending the laptop's lifespan and versatility. Unique features include wireless server connectivity and minimal installation for reduced footprint and enhanced security.

---

## Installation and Configuration

### 1. Creating a Bootable Device

1. Download the Ubuntu Server ISO.
2. Use tools like Rufus, Etcher, or Startup Disk Creator to create a bootable USB drive.
3. Boot from the USB and follow the installation prompts to set up the server.

### 2. Boot from Install Media

1. Insert the bootable USB.
2. Select "Install Ubuntu Server" from the GRUB menu.
3. Configure network and storage settings:
   - Network settings include setting up DHCP or assigning static IP addresses.
   - Storage settings involve guided or manual partitioning of disks.

### 3. Initial Setup

1. Log in with the username and password created during installation.
2. Update the system:
   ```bash
   sudo apt update && sudo apt full-upgrade
   sudo apt autoremove && sudo apt autoclean
   ```
3. Create necessary partitions and set up user accounts.

---

## Initial Server Configuration

### Setting Up Users and Groups

1. Add a new user:
   ```bash
   sudo adduser <username>
   sudo usermod -aG sudo <username>
   ```

2. Enable SSH for remote access:
   ```bash
   sudo apt install openssh-server
   sudo systemctl enable --now ssh
   sudo ufw allow ssh
   ```

3. Configure secure login and group privileges for better server security.

---

## Server Services

### Apache Web Server Setup

1. Install Apache:
   ```bash
   sudo apt install apache2
   sudo ufw allow 'Apache'
   ```
2. Create a virtual host configuration file:
   ```bash
   sudo nano /etc/apache2/sites-available/your_domain.conf
   ```
3. Restart Apache:
   ```bash
   sudo systemctl restart apache2
   ```

### Additional Services

1. **FTP Server Setup**:
   - Install and configure Vsftpd for file sharing.
   ```bash
   sudo apt install vsftpd
   ```
2. **Docker Installation**:
   - Setup containerized applications for lightweight and efficient services.
   ```bash
   sudo apt install docker.io
   ```

3. **Performance Monitoring Tools**:
   - Use tools like `nload` for real-time network traffic monitoring.

---

## Connecting Server Over Wi-Fi

1. Identify the wireless interface:
   ```bash
   ls -l /sys/class/net
   ```
2. Edit the Netplan configuration:
   ```bash
   sudo nano /etc/netplan/00-installer-config.yaml
   ```
   Add your Wi-Fi credentials:
   ```yaml
   network:
     version: 2
     renderer: networkd
     wifis:
       <interface_name>:
         dhcp4: true
         access-points:
           "<SSID>":
             password: "<password>"
   ```
3. Apply changes:
   ```bash
   sudo netplan apply
   ```
4. Verify the connection by pinging a remote server:
   ```bash
   ping 8.8.8.8
   ```

---

## Analysis

### Key Areas of Evaluation

1. **Hardware Analysis**: Assessing CPU, RAM, and storage for workload suitability.
2. **Operating System**: Chosen for efficiency and hardware compatibility.
3. **Software and Services**: Evaluating compatibility and resource usage.
4. **Networking**: Ensuring secure and reliable configurations.
5. **Security**: Implementing robust firewalls, SSH configurations, and regular updates.
6. **Performance Monitoring**: Utilizing tools to monitor and optimize resource utilization.

---

## Figures

1. **GNU GRUB Installation Page** - Visual reference for the boot menu.
2. **Network Configuration** - Example YAML configuration for Netplan.
3. **Storage Partitioning** - Guided disk setup illustration.
4. **SSH Setup** - Example output for enabling and verifying SSH services.

---

## Conclusion

This project provides a comprehensive guide for setting up a Portable NAS Server using Ubuntu Server. From installation and configuration to advanced service setup and wireless connectivity, the outlined steps ensure a secure and efficient server environment tailored to diverse needs. The PNS demonstrates significant potential for mobility, energy efficiency, and rapid deployment in various scenarios.

---

## References

1. [Ubuntu Documentation](https://ubuntu.com/server/docs)
2.  [Make Use Of](https://www.makeuseof.com/connect-to-wifi-network-on-ubuntu-server/)
3. [Linux For Devices](https://www.linuxfordevices.com/tutorials/ubuntu/connect-wifi-terminal-command-line)
4. [LinuxConfig: Connecting to Wi-Fi](https://linuxconfig.org/ubuntu-20-04-connect-to-wifi-from-command-line)
