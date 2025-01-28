# Description
This script automates the installation of Wazuh on Ubuntu 24.04 for setting up a Security Operations Center (SOC) with monitoring and detection capabilities.

---

## Prerequisites
- Ubuntu 24.04 installed on a virtual machine.
- A user account with sudo privileges.

---

## Script Content

### Update and upgrade the system
```bash
sudo apt-get update && sudo apt-get upgrade -y
```

### Install dependencies
```bash
sudo apt-get install -y curl apt-transport-https lsb-release gnupg
```

### Import Wazuh repository GPG key
```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -
```

### Add Wazuh repository
```bash
echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
```

### Update repository information
```bash
sudo apt-get update
```

### Install Wazuh manager
```bash
sudo apt-get install -y wazuh-manager
```

### Start Wazuh manager service
```bash
sudo systemctl enable wazuh-manager
sudo systemctl start wazuh-manager
```

### Verify Wazuh manager status
```bash
sudo systemctl status wazuh-manager
```

### Install Wazuh API (optional, if needed for integration)
```bash
sudo apt-get install -y wazuh-api
```

### Start Wazuh API service
```bash
sudo systemctl enable wazuh-api
sudo systemctl start wazuh-api
```

### Verify Wazuh API status
```bash
sudo systemctl status wazuh-api
```

### Output completion message
```echo
"Wazuh installation and setup completed successfully!"
```

---

## Usage Instructions
1. Copy the script content into a file named `install_wazuh`.
2. Make the script executable:
   ```bash
   chmod +x install_wazuh.sh
   ```
3. Run the script with sudo:
   ```bash
   sudo ./install_wazuh.sh
   ```
4. Access the Wazuh dashboard at `http://<VM_IP>:5601` after the installation.

---

## Notes
- Ensure network connectivity for downloading dependencies and accessing the Wazuh repository.
- Update the script if using a different version of Ubuntu or Wazuh.

---

## Troubleshooting
- If the Wazuh service fails to start, check logs:
  ```bash
  sudo journalctl -u wazuh-manager
  ```
