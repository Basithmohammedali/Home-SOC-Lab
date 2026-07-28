# Kibana

## Purpose

This document explains how Kibana was installed and configured for the Home SOC Lab. Kibana provides the web interface for Elasticsearch, allowing log analysis, dashboards, Fleet management, and security investigations.

---

# Prerequisites

Before installing Kibana, ensure that:

- Elasticsearch is installed and running.
- The ELK Server has internet connectivity.
- Port **9200** is accessible.
- SSH access is working.

---

# Install Kibana

Download the Debian package.

```bash
wget https://artifacts.elastic.co/downloads/kibana/kibana-9.4.2-amd64.deb
```

Install Kibana.

```bash
sudo dpkg -i kibana-9.4.2-amd64.deb
```

---

# Configure Kibana

Edit the configuration file.

```text
/etc/kibana/kibana.yml
```

Example configuration:

```yaml
server.host: "0.0.0.0"
server.port: 5601
server.publicBaseUrl: "http://192.168.50.3:5601"

elasticsearch.hosts:
  - "http://192.168.50.3:9200"
```

Save the file.

---

# Start Kibana

Reload systemd.

```bash
sudo systemctl daemon-reload
```

Enable Kibana at boot.

```bash
sudo systemctl enable kibana
```

Start Kibana.

```bash
sudo systemctl start kibana
```

Verify the service.

```bash
sudo systemctl status kibana
```

---

# Access Kibana

Open a web browser.

```
http://192.168.50.3:5601
```

Complete the initial setup and connect Kibana to Elasticsearch.

---

# Verification

Verify that Kibana is running.

```bash
curl http://192.168.50.3:5601
```

A successful response indicates that Kibana is available.

---

# Troubleshooting

### Kibana service failed

```bash
sudo journalctl -u kibana
```

---

### Unable to connect to Elasticsearch

Verify Elasticsearch.

```bash
curl http://192.168.50.3:9200
```

---

### Kibana is unreachable

Check listening ports.

```bash
sudo ss -tulpn
```

Verify that port **5601** is listening.

---

# Related Documentation

- [02 - ELK Server](02-elk-server.md)
- [04 - Fleet Server](04-fleet-server.md)
