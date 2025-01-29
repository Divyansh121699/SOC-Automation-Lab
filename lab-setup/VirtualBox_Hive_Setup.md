# Setting Up The Hive in VirtualBox

## Overview
This guide provides a basic understanding of setting up The Hive on an on-premise virtual machine using Oracle VirtualBox. The Hive is a Security Incident Response Platform (SIRP) that helps SOC analysts manage and investigate security incidents effectively.

## Prerequisites
- Oracle VirtualBox installed.
- Ubuntu 20.04 ISO file.
- At least 8GB RAM and 50GB disk space allocated for the VM.
- Network configured to allow communication between The Hive, Wazuh, and Shuffle.

## Steps
1. **Create a Virtual Machine in VirtualBox**
   - Open VirtualBox and create a new VM.
   - Set the name as "The Hive" and select Ubuntu (64-bit) as the OS.
   - Allocate 8GB RAM and at least 50GB of dynamically allocated storage.

2. **Install Ubuntu 20.04**
   - Boot the VM using the Ubuntu ISO.
   - Follow the installation prompts to complete the setup.
   - Configure a static IP address to ensure consistent connectivity.

3. **Post-Installation Configuration**
   - Update and upgrade the system:
     ```bash
     sudo apt-get update && sudo apt-get upgrade -y
     ```
   - Install necessary system utilities such as wget, curl, and git.

4. **Configure System Settings**
   - Ensure the firewall allows necessary ports for communication.
   - Set up hostname resolution to enable connectivity between The Hive and other SOC components.

5. **Verify Network Connectivity**
   - Ensure the VM can communicate with Wazuh and Shuffle.
   - Use `ping` or `curl` to test connectivity between the systems.

## Next Steps
After completing the basic setup, install The Hive by following the [install_hive.md](https://github.com/Divyansh121699/SOC-Automation-Lab/blob/main/scripts/install_thehive.md) script provided in this repository's `scripts/` directory.

For further configuration, refer to [hive_application.conf](https://github.com/Divyansh121699/SOC-Automation-Lab/blob/main/configurations/Hive_application_conf.md) in the `configurations/` directory.
