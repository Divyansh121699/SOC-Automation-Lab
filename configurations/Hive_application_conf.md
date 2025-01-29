# Hive_application.conf

## Changes to Make in `application.conf`

1. **Set the Hostname:**
   ```
   hostname = ["<IP address of the Hive server>"]
   ```
   Replace `<IP address of the Hive server>` with the actual IP address of your Hive server.

2. **Configure Cluster Name:**
   ```
   cluster-name = ACR
   ```
   Replace `ACR` with your desired cluster name to ensure it matches the Cassandra cluster configuration.

3. **Set Index Hostname:**
   ```
   index.search.hostname = ["<IP address of the Hive server>"]
   ```
   Replace `<IP address of the Hive server>` with the same IP as above.

4. **Application Base URL:**
   ```
   application.baseUrl = "http://<IP address of the Hive server>:9000"
   ```
   Replace `<IP address of the Hive server>` with the actual IP address. Ensure the port `9000` is open and configured.

5. **Enable Elasticsearch Security:**
   If Elasticsearch requires authentication, add the credentials:
   ```
   index.elasticsearch.auth.username = "<elasticsearch-username>"
   index.elasticsearch.auth.password = "<elasticsearch-password>"
   ```
   Replace `<elasticsearch-username>` and `<elasticsearch-password>` with your Elasticsearch credentials.

6. **Enable TLS for Secure Communication (Optional):**
   ```
   http.ssl.enabled = true
   http.ssl.keystore.path = "/path/to/keystore"
   http.ssl.keystore.password = "<keystore-password>"
   ```
   Replace `/path/to/keystore` with the location of your keystore file and `<keystore-password>` with the password.

## Notes:
- Ensure the IP addresses and port numbers are consistent across all configurations (Cassandra, Elasticsearch, Hive).
- Restart The Hive service after making changes:
  ```bash
  sudo systemctl restart thehive
  ```
