# Basic-Security-Monitoring-and-Incident-Response

Project Overview

This project demonstrates basic security monitoring and incident response by setting up and configuring a Kali Linux VM and an Ubuntu Desktop environment. The goal is to simulate a security monitoring scenario, including running scans, analyzing logs, and handling potential security issues.
Prerequisites

    Kali Linux VM: Used for security testing and vulnerability scanning.
    Ubuntu Desktop: Used for installing and configuring ClamAV and Splunk for security monitoring.

Setup Instructions
1. Kali Linux VM Setup
Downloading and Installing Kali Linux

    Download the Kali Linux ISO from the official Kali website.

    Create a new virtual machine in your VM software (VMware, VirtualBox, etc.):
        Select "Create a New Virtual Machine."
        Choose "Installer disc image file (iso)" and select the downloaded Kali Linux ISO.
        Allocate resources (RAM, CPU, disk space) as needed.
        Complete the VM creation process.

    Install Kali Linux:
        Boot the VM from the ISO.
        Follow the on-screen instructions for installation.
        Select the appropriate language, location, and keyboard layout.
        Configure network settings and create a user account.
        Choose to install the GRUB boot loader if prompted.

    Post-Installation Setup:
        Update and upgrade the system:

        bash

    sudo apt update
    sudo apt upgrade

Install Nmap:

bash

    sudo apt install nmap

2. Ubuntu Desktop Setup
Installing Ubuntu Desktop

    Download the Ubuntu Desktop ISO from the official Ubuntu website.

    Create a new virtual machine:
        Select "Create a New Virtual Machine."
        Choose "Installer disc image file (iso)" and select the downloaded Ubuntu ISO.
        Allocate resources (RAM, CPU, disk space) as needed.
        Complete the VM creation process.

    Install Ubuntu Desktop:
        Boot the VM from the ISO.
        Follow the on-screen instructions for installation.
        Select the appropriate language, time zone, and keyboard layout.
        Set up your user account and password.

    Post-Installation Setup:
        Update and upgrade the system:

        bash

        sudo apt update
        sudo apt upgrade

Installing ClamAV and Splunk Forwarder

    Install ClamAV:

    bash

sudo apt install clamav clamav-daemon
sudo freshclam

Install Splunk Forwarder:

    Download the Splunk Forwarder package from Splunk's website.
    Install the package:

    bash

sudo dpkg -i splunkforwarder-<version>-<architecture>.deb

Start Splunk Forwarder and set up admin credentials:

bash

        sudo /opt/splunkforwarder/bin/splunk start --accept-license
        sudo /opt/splunkforwarder/bin/splunk edit user admin -password <newpassword> -auth admin:changeme

3. Security Monitoring and Testing

    Configure ClamAV:
        Set ClamAV to scan files and directories as needed.

    Configure Splunk Forwarder:
        Ensure Splunk Forwarder is correctly configured to collect and forward logs from ClamAV.

    Simulate a Vulnerability Scan:
        From the Kali VM, run an Nmap scan:

        bash

    nmap -A -Pn 192.168.137.130

Check SSH Connection:

    Test SSH connection from Kali to Ubuntu:

    bash

    ssh cgoetz@192.168.137.130

Review Logs:

    Check ClamAV logs:

    bash

cat /var/log/clamav/clamav.log

Check Splunk logs:

bash

        sudo /opt/splunkforwarder/bin/splunk search "index=_internal sourcetype=clamav" -auth admin:<newpassword>

Issues Encountered and Resolutions

    Kali Linux Installation Issues:
        Problem: Black screen with a blinking cursor during installation.
        Resolution: Re-installed using the ISO image and followed the on-screen instructions carefully.

    ClamAV Issues:
        Problem: ClamAV logs were locked or had permission issues.
        Resolution: Fixed by ensuring ClamAV had the correct permissions and was running properly.

    Splunk Forwarder Authentication Issues:
        Problem: Unable to authenticate using default credentials.
        Resolution: Changed the admin password and ensured Splunk Forwarder was correctly configured.

    Firewall Issues:
        Problem: SSH connection failed due to firewall blocking.
        Resolution: Added SSH to the Ubuntu firewall rules.

Conclusion

This project demonstrates setting up a basic security monitoring and incident response scenario. By configuring ClamAV and Splunk on Ubuntu and running security tests from Kali Linux, you can showcase your understanding of security concepts and incident management.
