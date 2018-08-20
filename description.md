Filename: discription.md  
Author: Trae Elmore  
Date: 2018-08-20  

*Term: RHEL stands for RedHat Enterprise Linux* 

# How To Use the RHEL Kickstart DVDs For a Fresh Installation  

### Overview:
> The RHEL 7.5 Server and Workstation kickstart DVDs are provided to enable quick and repeatable standardized systems that are approximately 85% DISA STIG-compliant.  

#### Prerequisites:  
> Each installation requires a minimum of 40GB of local storage.  Workstation installations require 2GB RAM while Server installations required 1GB, minimum.  

Kickstart will request the following information:  

- Hostname: The friendly name of the computer. Provide the fully-qualified domain name here (e.g., rhel7.example.com).
- IP Address: The internal IP address of the system. (e.g.., 192.168.1.1)
- Prefix: The subnet mask in decimal format (e.g., 255.255.255.0 = 24)  
- Subnet in CIR Notation: The IP plus prefix in the format x.x.x.x/xx. The slash is required!  
- Gateway IP: The IP address of your network (or VLAN) default gateway  
- NTP Source: The IP address of your authoritative NTP server  
- Primary DNS Server: The IP of your primary authoritative DNS server  
- Secondary DNS Server: The IP of your secondary authoritative DNS server  

#### Accounts created:  
> The kickstart will create and set the "root" and "grub" passwords to "Pa33word" (without the quotes). It will also create an administrative user, ladmin, with the same password.  
> You are required to IMMEDIATELY change all passwords that are preset to meet STIG and IA compliance after the kickstart is complete.  

#### Usage: 
1. Insert the appropriate DVD into the system and boot directly to it.  
2. Select "Install RHEL 7.5 Server CLI for DISA" or "Install RHEL 7.5 Workstation for DISA", depending on the DVD you installed.  
3. You will be prompted for each item listed in "Prerequisites."  
4. Wait for the kickstart to complete and reboot to complete.  

**Installations typically take 30 minutes or less.**

#### System Hardening and STIGs:  
> To finish hardening these systems and maintain STIG compliance, other external requirements will need to be met including: centralized external syslog servers, centralized audit servers, DoD-approved Anti-Virus software and scan scripts, installing DoD Certificates, configuring PKI, SSSD, and other services as required by your environment.

#### example of using the kickstart file with KVM on linux   

` sudo virt-install --connect=qemu:///system --network bridge:virbr1 --ram 512 --vcpus=1 --initrd-inject=/var/lib/libvirt/images/isos/server-ks.cfg --extra-args="ks=file:/server-ks.cfg console=tty0 console=ttyS0,115200" --name=server1 --disk pool=default,size=40 --location /var/lib/libvirt/images/isos/rhel7-server.iso"`

