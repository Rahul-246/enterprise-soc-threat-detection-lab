# SOC Lab Architecture

```text
Windows Host / Analyst Browser
             |
             | HTTPS (private lab network)
             v
VM1 — Ubuntu Server 24.04
  - Wazuh Dashboard
  - Wazuh Indexer
  - Wazuh Manager
             ^
             | Wazuh Agent communication
             |
VM2 — Ubuntu Endpoint
  - Wazuh Agent
  - SSH authentication events
  - Controlled failed-login test
```

## Network notes

Record the actual private lab addresses in your private notes. Avoid publishing addresses if you consider them sensitive. Keep the dashboard and agent communication restricted to the lab network; do not expose them directly to the public internet.
