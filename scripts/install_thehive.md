# Description
This script automates the installation of The Hive on Ubuntu 20.04 for setting up a Security Operations Center (SOC) with case management and incident response capabilities.

---

## Prerequisites
- Ubuntu 20.04 installed on a virtual machine.
- A user account with sudo privileges.

---

## Script Content

### Update and upgrade the system
```bash
sudo apt-get update && sudo apt-get upgrade -y
```

### Install prerequisites
```bash
sudo apt install -y wget gnupg apt-transport-https git ca-certificates curl python3-pip
```

### Install Java (Amazon Corretto JDK 11)
```bash
wget -qO- https://apt.corretto.aws/corretto.key | sudo gpg --dearmor -o /usr/share/keyrings/corretto.gpg
echo "deb [signed-by=/usr/share/keyrings/corretto.gpg] https://apt.corretto.aws stable main" | sudo tee /etc/apt/sources.list.d/corretto.list
sudo apt update
sudo apt install -y java-11-amazon-corretto-jdk
export JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto"
```

### Verify Java installation
```bash
java -version
```

### Install Cassandra
```bash
wget -qO - https://downloads.apache.org/cassandra/KEYS | sudo gpg --dearmor -o /usr/share/keyrings/cassandra-archive.gpg
echo "deb [signed-by=/usr/share/keyrings/cassandra-archive.gpg] https://debian.cassandra.apache.org 40x main" | sudo tee /etc/apt/sources.list.d/cassandra.sources.list
sudo apt update
sudo apt install -y cassandra
```

### Verify Cassandra installation
```bash
cassandra -v
```

### Install Elasticsearch
```bash
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
sudo apt-get install apt-transport-https -y
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
sudo apt update
sudo apt install -y elasticsearch
```

### Verify Elasticsearch installation
```bash
dpkg -l | grep elasticsearch
```

### Configure Elasticsearch JVM options
```bash
sudo mkdir -p /etc/elasticsearch/jvm.options.d
sudo cd /etc/elasticsearch/jvm.options.d/
sudo nano jvm.options
-Dlog4j2.formatMsgNoLookups=true
-Xms2g
-Xmx2g
```

### Start and enable Elasticsearch service
```bash
sudo systemctl start elasticsearch
sudo systemctl enable elasticsearch
```

### Add The Hive repository and install The Hive
```bash
wget -O- https://archives.strangebee.com/keys/strangebee.gpg | sudo gpg --dearmor -o /usr/share/keyrings/strangebee-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/strangebee-archive-keyring.gpg] https://deb.strangebee.com thehive-5.2 main" | sudo tee /etc/apt/sources.list.d/strangebee.list
sudo apt-get update
sudo apt-get install -y thehive
```

### Verify The Hive installation
```bash
dpkg -l | grep thehive
```

### Start and enable The Hive service
```bash
sudo systemctl start thehive
sudo systemctl enable thehive
```

### Output completion message
```bash
echo "The Hive installation and setup completed successfully!"
```

---

## Usage Instructions
1. Copy the script content into a file named `install_hive.sh`.
2. Make the script executable:
   ```bash
   chmod +x install_hive.sh
   ```
3. Run the script with sudo:
   ```bash
   sudo ./install_hive.sh
   ```
4. Access The Hive dashboard at `http://<VM_IP>:9000` after the installation.

---

## Notes
- Ensure network connectivity for downloading dependencies and accessing the repositories.
- Update the script if using a different version of Ubuntu or The Hive.

---

## Troubleshooting
- If The Hive service fails to start, check logs:
  ```bash
  sudo journalctl -u thehive
  ```
