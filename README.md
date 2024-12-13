# Portable-Server
***Developed by: PHILIP SIMON DEROCK P***



## Wireless Server Using an Old Laptop

This project demonstrates how to transform an old laptop into a fully functional **Portable Server**. The server is configured for wireless operation using Wi-Fi and mobile hotspots. It supports services like web hosting, file sharing, and real-time application deployment. This guide provides a comprehensive walkthrough of the server setup process, including installation, configuration, and service deployment.

---

## Features
- **Cost-Effective Solution**: Utilizes an old laptop, reducing the need for new hardware.
- **Dual-Boot Support**: Provides flexibility by enabling Ubuntu Server alongside an existing OS.
- **Wireless Operation**: Fully functional without Ethernet cables.
- **Web Hosting**: Includes Apache web server for hosting websites and applications.
- **Remote Administration**: Configured for secure SSH access.
- **Extensible**: Supports additional services like Docker,JDK,FTP, and SFTP.

---

## Contents
[Introduction](#introduction)

[Components Used](#components-used)
   - [Hardware Components](#hardware-components)
   
   - [Software Components](#software-components)
    
 [Installation and Configuration](#installation-and-configuration)

   - [Creating a Bootable Device](#creating-a-bootable-device)
     
   - [Booting from Install Media](#booting-from-install-media)
     
   - [Initial Setup](#initial-setup)
     
 [Initial Server Configuration](#initial-server-configuration)

   - [Setting Up Users and Groups](#setting-up-users-and-groups)
     
   - [Configuring SSH Access](#configuring-ssh-access)
     
 [Server Services](#server-services)

   - [Apache Web Server](#apache-web-server)
     
 [Connecting Server Over Wi-Fi](#connecting-server-over-wi-fi)

 [Conclusion](#conclusion)
 
 [References](#references)

---

## Introduction
This project explores the transformation of an old **Lenovo E41-25** laptop into a **Portable NAS Server**. With Ubuntu Live Server 22.04.2 installed, the server is optimized for wireless operation and tailored for diverse use cases such as file sharing, web hosting, and development. The use of lightweight Linux distributions extends the life and utility of older hardware.

Key benefits include:
- Cost-effectiveness by reusing existing hardware.
- A built-in UPS with the laptop battery.
- Dual-boot support for flexibility.
- Wireless operation using Wi-Fi and mobile hotspots.

---

## Components Used

### Hardware Components
- **Laptop**: Lenovo E41-25  
- **Processor**: AMD PRO A4-4350B, 2.50 GHz  
- **RAM**: CRUCIAL DDR4, 4 GB  
- **Storage**: WD Green 240 GB SATA SSD  
- **NIC**: Realtek PCIe GbE Family Controller (1.0 Gbps)  
- **Router**: NEET Link HG323DAC (Dual Band, 5 GHz + 2.4 GHz)  
- **RJ45 Cable**: CAT 6E RJ45, 10 Gbps  

### Software Components
- **Operating System**: Ubuntu Live Server 22.04.2  
- **Web Server**: Apache2  
- **Containers**: Docker  
- **FTP Server**: Vsftpd  
- **SFTP Server**: SFTP Drive 2022  
- **Utilities**: Network-Manager CLI, WPA Supplicant, Nload  

---

## Installation and Configuration

### Creating a Bootable Device
1. Download the Ubuntu Server ISO from the [official website](https://ubuntu.com/download/server).
2. Use tools like Rufus, Startup Disk Creator, or Unetbootin to create a bootable USB device.
3. Burn the ISO to the USB drive:
   ```bash
   sudo dd if=/path/to/iso of=/dev/sdX bs=4M status=progress
   ```

### Booting from Install Media
1. Insert the bootable USB into the laptop.
2. Power on and boot from the USB.
3. Follow the installation prompts:
   - Select language and time zone.
   - Configure network connections.
   - Partition the storage (guided or manual).
   - Set up a hostname and create a user account.

### Initial Setup
1. Log in to the server:
   ```bash
   ssh username@server_ip
   ```
   
   
2. Update the system:
   ```bash
   sudo apt update && sudo apt full-upgrade
   sudo apt autoremove && sudo apt autoclean
   ```

---

## Initial Server Configuration

### Setting Up Users and Groups
1. Add a new user:
   ```bash
   sudo adduser username
   sudo usermod -aG sudo username
   ```

### Configuring SSH Access


1. Install and enable SSH server:
   ```bash
   sudo apt install openssh-server
   sudo systemctl enable ssh --now
   sudo ufw allow ssh
   ```
2. Connect remotely via SSH:
   ```bash
   ssh username@server_ip
   ```

---

## Server Services

### Apache Web Server
   




1. Install Apache:
   ```bash
   sudo apt install apache2
   ```
2. Enable and start the service:
   ```bash
   sudo systemctl enable apache2 --now
   ```
3. Test the server:
   - Retrieve the server's IP:
     ```bash
     hostname -I
     ```
   - Access the default Apache page in your browser:
     ```
     http://server_ip
     ```

---

## Connecting Server Over Wi-Fi

The server is configured for wireless connectivity via Wi-Fi or mobile hotspots.



1. **Identify the Wi-Fi Interface**:
   ```bash
   sudo ls -l /sys/class/net
   ```
2. **Edit the Netplan Configuration File**:
   ```bash
   sudo vim /etc/netplan/00-installer-config.yaml
   ```
   Replace the content with:
   ```yaml
   network:
     version: 2
     wifis:
       wlp0s20f3:
         access-points:
           "YourWiFiName":
             password: "YourWiFiPassword"
         dhcp4: true
   ```
3. **Apply the Changes**:
   ```bash
   sudo netplan apply
   ```
4. **Verify the Connection**:
   ```bash
   ping 8.8.8.8
   ```

---

## Conclusion
This project demonstrates the feasibility of converting an old laptop into a **Portable NAS Server**. The setup offers flexibility, portability, and cost-effectiveness while enabling modern functionalities like wireless operation and web hosting. By following the guide, users can extend the life of older hardware and create a robust server environment.

---

## References
- [Ubuntu Documentation](https://ubuntu.com/server/docs)
- [LinuxConfig: Connecting to Wi-Fi](https://linuxconfig.org/ubuntu-20-04-connect-to-wifi-from-command-line)
- [Apache Web Server Setup](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04)
- [Netplan Configuration](https://netplan.io/reference)
