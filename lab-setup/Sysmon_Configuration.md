# Sysmon Configuration

## Overview
Sysmon (System Monitor) is a powerful Windows system service that logs detailed system activity to the Windows Event Log. It provides critical insights into process creation, network connections, and file changes, which are essential for detecting suspicious activities.

## Steps to Configure Sysmon

### 1. Download Sysmon
1. Visit the [Microsoft Sysinternals Sysmon page](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon).
2. Download the latest Sysmon executable (`Sysmon64.exe` for 64-bit systems).

### 2. Download Configuration File
1. Use a prebuilt configuration file for balanced logging and noise reduction.
2. Recommended source: [Sysmon Modular Configuration](https://github.com/olafhartong/sysmon-modular).
3. Download `sysmonconfig.xml` from the repository.

### 3. Install Sysmon
1. Open PowerShell with administrative privileges.
2. Navigate to the folder containing `Sysmon64.exe` and `sysmonconfig.xml`.
3. Install Sysmon with the configuration file:
   ```powershell
   .\Sysmon64.exe -i sysmonconfig.xml
   ```
4. Verify installation by checking the Sysmon service status:
   ```powershell
   Get-Service -Name Sysmon64
   ```

### 4. Verify Event Logs
1. Open the Windows Event Viewer.
2. Navigate to **Applications and Services Logs > Microsoft > Windows > Sysmon > Operational**.
3. Confirm that events are being logged.

### 5. Integrate with Wazuh
1. Modify the `ossec.conf` file on your Wazuh Manager to include Sysmon logs:
   ```xml
   <localfile>
       <location>Microsoft-Windows-Sysmon/Operational</location>
       <log_format>eventchannel</log_format>
   </localfile>
   ```
2. Restart the Wazuh Manager to apply changes:
   ```bash
   systemctl restart wazuh-manager
   ```

## Additional Tips
- Periodically update the `sysmonconfig.xml` file to ensure coverage of new attack techniques.
- Customize the configuration to suit specific environment requirements.

## Resources
- [Sysmon Documentation](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon)
- [Sysmon Modular GitHub Repository](https://github.com/olafhartong/sysmon-modular)
