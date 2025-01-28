To configure Cassandra for The Hive, make the following changes in the `cassandra.yaml` file:

1. **Cluster Name**:
   ```yaml
   cluster_name: 'ACR'
   ```

2. **RPC Address**:
   ```yaml
   rpc_address: '<IP address of the Hive server>'
   ```

3. **Listen Address**:
   ```yaml
   listen_address: '<IP address of the Hive server>'
   ```

4. **Seed Nodes**:
   ```yaml
   seeds: '<IP address of the Hive server>:7000'
   ```

5. **Commit Log Directory** (Optional):
   - Ensure proper storage for commit logs.
   ```yaml
   commitlog_directory: '/var/lib/cassandra/commitlog'
   ```

6. **Data File Directories** (Optional):
   - Specify a directory for Cassandra data.
   ```yaml
   data_file_directories:
       - '/var/lib/cassandra/data'
   ```

7. **Hints Directory** (Optional):
   - Set the directory for storing hints.
   ```yaml
   hints_directory: '/var/lib/cassandra/hints'
   ```

After making these changes, restart the Cassandra service:

```bash
sudo systemctl restart cassandra.service
```

Verify the status:

```bash
sudo systemctl status cassandra.service
```
