# VirtualBox Wazuh Setup

## Prerequisites
- Oracle VirtualBox installed.
- Ubuntu 24.04 ISO.

## Steps

### 1. Create a Virtual Machine
1. Open VirtualBox and click **New**.
2. Set the name to **Wazuh**, type to **Linux**, and version to **Ubuntu (64-bit)**.
3. Allocate **8 GB RAM** and create a **50 GB dynamically allocated virtual hard disk**.
4. Attach the Ubuntu 24.04 ISO as the installation media.

### 2. Install Ubuntu 24.04
1. Start the VM and proceed with the Ubuntu installation.
2. Set up a user account and configure network settings.
3. Update system packages after installation:
   ```bash
   sudo apt-get update && sudo apt-get upgrade -y
   ```

### 3. Install Wazuh
1. Download and install Wazuh using the official script:
   ```bash
   curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
   ```
2. Verify Wazuh installation:
   ```bash
   sudo systemctl status wazuh-manager
   ```

### 4. Configure Firewall Rules
1. Open necessary ports:
   ```bash
   sudo ufw allow 1514/tcp
   sudo ufw allow 55000/tcp
   sudo ufw enable
   ```

### 5. Access Wazuh Dashboard
1. Open a browser and navigate to:
   ```
   http://<VM_IP>:5601
   ```
2. Log in with the default credentials and start configuring your monitoring setup.

### Next Steps
- Add agents to monitor endpoints.
- Integrate with The Hive and Shuffle for automated response.
- Customize rules for better threat detection.
