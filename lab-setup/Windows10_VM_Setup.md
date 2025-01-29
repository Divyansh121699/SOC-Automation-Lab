## Setting Up Windows 10 VM in VirtualBox

### Prerequisites
1. Oracle VirtualBox installed on your machine.
2. Windows 10 ISO file available for installation.
3. Sufficient disk space (minimum 50GB recommended).

### Steps to Set Up the VM

#### 1. Create the Virtual Machine
1. Open VirtualBox and click on **New**.
2. Name the VM (e.g., `Windows10`), set **Type** to `Microsoft Windows`, and **Version** to `Windows 10 (64-bit)`.
3. Allocate at least 4GB of memory (recommended: 8GB).
4. Choose **Create a virtual hard disk now** and click **Create**.
5. Select **VDI (VirtualBox Disk Image)** and **Dynamically Allocated**.
6. Set the disk size to at least 50GB and click **Create**.

#### 2. Install Windows 10
1. Select the created VM and click **Settings**.
2. Go to **Storage** > **Empty** (under Controller: IDE) > click **Disk Icon** > **Choose a disk file**.
3. Browse and select the Windows 10 ISO file.
4. Click **OK** to save settings.
5. Start the VM and follow the Windows installation wizard:
   - Choose the language, time, and keyboard input.
   - Enter the product key or skip if not available.
   - Select the installation type (custom recommended).
   - Partition the allocated disk and proceed with installation.
6. Complete the setup and create a user account.

#### 3. Install Guest Additions
1. Start the Windows VM and log in.
2. From the VirtualBox menu, go to **Devices** > **Insert Guest Additions CD Image**.
3. Open the CD drive in File Explorer and run `VBoxWindowsAdditions.exe`.
4. Follow the installation steps and restart the VM.

### Configuring the Windows 10 VM

#### 1. Network Configuration
1. Ensure the VM network adapter is set to **Bridged Adapter** or **NAT** with port forwarding to enable communication with other VMs.
2. Test connectivity to other VMs in the lab using `ping`.

### Snapshot the VM
Once the VM is fully configured, create a snapshot in VirtualBox to save the current state. This allows easy rollback if needed.

---

Your Windows 10 VM is now ready for use in the SOC Automation Lab setup.
