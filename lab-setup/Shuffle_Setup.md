# Shuffle Setup

## Introduction
Shuffle is a Security Orchestration, Automation, and Response (SOAR) platform used to automate security workflows. It integrates with Wazuh and The Hive to streamline incident response and minimize manual intervention.

## Prerequisites
- A working installation of **Wazuh** and **The Hive**.
- An internet connection to access **Shuffler.io**.
- A registered account on [Shuffler.io](https://shuffler.io/).

## Installation Steps

### 1. Register an Account
1. Navigate to [Shuffler.io](https://shuffler.io/).
2. Click **Sign Up** and complete the registration process.
3. Verify your email and log into the platform.

### 2. Create a New Workflow
1. Click **Workflows** in the dashboard.
2. Click **Create New Workflow** and enter a name (e.g., "SOC Automation").
3. Save changes to initialize the workflow.

### 3. Configure Webhook for Wazuh Alerts
1. Click **Triggers** and select **Webhook**.
2. Drag it into the workflow canvas.
3. Copy the **Webhook URL** for later integration with Wazuh.

### 4. Integrate Wazuh with Shuffle
1. SSH into your Wazuh Manager VM.
2. Edit the `ossec.conf` file:
   ```xml
   <integration>
     <name>shuffle</name>
     <hook_url>http://<YOUR_SHUFFLE_URL>/api/v1/hooks/<HOOK_ID></hook_url>
     <alert_format>json</alert_format>
   </integration>
   ```
3. Restart Wazuh Manager:
   ```bash
   systemctl restart wazuh-manager.service
   ```

### 5. Extract SHA256 Hash for VirusTotal Check
1. Add a **Regex Capture Group** action to extract the SHA256 hash.
2. Use the following regex:
   ```regex
   SHA256=([A-Fa-f0-9]{64})
   ```
3. Save and rerun the workflow to verify hash extraction.

### 6. Integrate VirusTotal API
1. Go to **Apps** and activate **VirusTotal v3**.
2. Drag it into the workflow and authenticate with an API key.
3. Set **Action** to `Get a hash report` and input the SHA256 value.

### 7. Send Enriched Alerts to The Hive
1. Activate **The Hive** integration in Shuffle.
2. Enter your Hive API key and instance URL (`http://<HIVE_VM_IP>:9000`).
3. Configure alert details in JSON format:
   ```json
   {
     "type": "Internal",
     "source": "Wazuh",
     "title": "Security Alert: Potential Credential Theft",
     "description": "Detected suspicious activity...",
     "tags": ["T1003"]
   }
   ```

### 8. Notify Analysts via Email
1. Activate the **Email** apps in Shuffle.
2. Enter recipient details and customize the message.
3. Test notifications by triggering a sample alert.

### 9. Testing and Validation
1. Generate a **Mimikatz event** on the Windows VM.
2. Check if Wazuh detects and forwards alerts to Shuffle.
3. Verify enrichment and case creation in The Hive.
4. Ensure email/SMS notifications are received.

### Conclusion
By integrating Shuffle with Wazuh and The Hive, security incidents can be automatically detected, enriched, and assigned to analysts for action, improving SOC efficiency and reducing response times.
