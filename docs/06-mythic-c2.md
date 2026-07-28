# Mythic C2

## Purpose

This document explains how Mythic C2 was deployed in the Home SOC Lab to simulate adversary activity. The generated telemetry is collected by Elastic Agent and analyzed in Kibana for detection and investigation.

---

# Prerequisites

Before deploying Mythic C2, ensure that:

- Elasticsearch is running.
- Kibana is running.
- Fleet Server is operational.
- Endpoints are enrolled in Fleet.
- Docker is installed.
- Network connectivity is available.

---

# Virtual Machine Configuration

| Setting | Value |
|----------|-------|
| Operating System | Ubuntu Server |
| IP Address | 192.168.50.7 |
| Purpose | Command and Control Server |

---

# Install Mythic

Clone the Mythic repository.

```bash
git clone https://github.com/its-a-feature/Mythic.git
```

Navigate to the project directory.

```bash
cd Mythic
```

Start Mythic.

```bash
sudo ./mythic-cli start
```

---

# Access Mythic

Open a web browser and access the Mythic web interface.

```
https://192.168.50.7
```

Log in using the credentials configured during deployment.

---

# Deploy an Agent

1. Create a payload.
2. Transfer the payload to the endpoint.
3. Execute the payload.
4. Verify that the callback appears in Mythic.

---

# Detection Workflow

The simulated attacker activity generates telemetry collected by Elastic Agent.

The workflow is:

```
Mythic
      │
      ▼
Elastic Agent
      │
      ▼
Fleet Server
      │
      ▼
Elasticsearch
      │
      ▼
Kibana
```

---

# Verification

Verify that:

- Mythic is accessible.
- Payload callbacks are received.
- Endpoint telemetry appears in Kibana.
- Detection rules generate alerts.

---

# Troubleshooting

### Mythic does not start

```bash
sudo ./mythic-cli status
```

---

### Docker Containers

```bash
docker ps
```

---

### Callback Not Received

- Verify network connectivity.
- Verify endpoint execution.
- Verify firewall configuration.

---

# Related Documentation

- [05 - Endpoints](05-endpoints.md)
- [07 - osTicket](07-osticket.md)
