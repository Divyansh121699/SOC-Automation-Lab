## Description
This section outlines the modifications required in the `wazuh_ossec.conf` file to integrate Sysmon logs, configure email notifications, and enable Shuffle integration for automated workflows. Make these updates to customize your Wazuh configuration.

## Modifications

### 1. Add Localfile Entry for Sysmon Logs
Include the following under the `<ossec_config>` tag to monitor Sysmon logs:
```xml
<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

### 2. Configure Email Notifications
Ensure email notifications are enabled by adding:
```xml
<email_notification>yes</email_notification>
<email_from>ossec@example.com</email_from>
<email_to>admin@example.com</email_to>
<smtp_server>smtp.example.com</smtp_server>
<smtp_port>25</smtp_port>
```

### 3. Enable Shuffle Integration
Add the integration section to forward specific alerts to Shuffle:
```xml
<integration>
  <name>shuffle</name>
  <hook_url>http://your-shuffle-instance/api/v1/hooks/your-hook-id</hook_url>
  <rule_id>100002</rule_id>
  <alert_format>json</alert_format>
</integration>
```

### 4. Add Custom Rules
Include your custom rule file for detecting Mimikatz activity:
```xml
<rules>
  <include>local_rules.xml</include>
</rules>
```

### 5. Enable Active Response
Enable active response to automate actions on specific rules:
```xml
<active-response>
  <disabled>no</disabled>
  <command>host-deny</command>
  <location>all</location>
  <rules_id>100001,100002</rules_id>
</active-response>
```

## Notes
- Replace placeholders (e.g., `your-shuffle-instance`, `your-hook-id`, `ossec@example.com`) with actual values for your environment.
- Restart the Wazuh manager to apply changes:
  ```bash
  sudo systemctl restart wazuh-manager
  ```
