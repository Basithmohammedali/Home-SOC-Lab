# ELK Server

## Purpose

This document explains how the ELK Server was deployed for the Home SOC Lab. The server hosts Elasticsearch and Kibana, which provide centralized log collection, search, visualization, and security monitoring.

---

# Prerequisites

Before installing the ELK Stack, ensure that:

- Ubuntu Server is installed.
- The server is connected to the `basi-soc` NAT Network.
- Internet connectivity is available.
- SSH access is working.
- The server has sufficient disk space.

---

# Virtual Machine Configuration

| Setting | Value |
|----------|-------|
| Operating System | Ubuntu Server 22.04 |
| RAM | 2 GB |
| CPU | 2 vCPU |
| Disk | 25 GB |
| IP Address | 192.168.50.3 |

---

# Configure SSH

Check the assigned IP address.

```bash
hostname -I
```

Configure a VirtualBox Port Forwarding rule.

| Setting | Value |
|----------|-------|
| Host Port | 2222 |
| Guest Port | 22 |
| Protocol | TCP |

Connect from the host machine:

```bash
ssh -p 2222 basi@127.0.0.1
```

---

# Expand the Disk

Verify available volume space.

```bash
sudo vgs
```

Extend the logical volume.

```bash
sudo lvextend -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
```

Resize the filesystem.

```bash
sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
```

Verify the new disk size.

```bash
df -h
```

---

# Update Ubuntu

Update package information.

```bash
sudo apt update
```

Upgrade installed packages.

```bash
sudo apt upgrade -y
```

---

# Install Elasticsearch

Download the package.

```bash
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-9.4.2-amd64.deb
```

Install Elasticsearch.

```bash
sudo dpkg -i elasticsearch-9.4.2-amd64.deb
```

---

# Configure Elasticsearch

Edit the configuration file.

```text
/etc/elasticsearch/elasticsearch.yml
```

Example configuration:

```yaml
network.host: 192.168.50.3
http.port: 9200
```

Save the file.

---

# Start Elasticsearch

Reload the systemd configuration.

```bash
sudo systemctl daemon-reload
```

Enable Elasticsearch at boot.

```bash
sudo systemctl enable elasticsearch
```

Start the service.

```bash
sudo systemctl start elasticsearch
```

Check the service status.

```bash
sudo systemctl status elasticsearch
```

---

# Verification

Verify that Elasticsearch is listening on port **9200**.

```bash
curl http://192.168.50.3:9200
```

A JSON response indicates that Elasticsearch is running correctly.

---

# Troubleshooting

### Elasticsearch service failed

Check the service logs.

```bash
sudo journalctl -u elasticsearch
```

---

### Configuration error

Validate the configuration file.

```bash
sudo cat /etc/elasticsearch/elasticsearch.yml
```

---

### Port 9200 is unreachable

Verify that Elasticsearch is running.

```bash
sudo systemctl status elasticsearch
```

Check listening ports.

```bash
sudo ss -tulpn
```

---

# Related Documentation

- [01 - Lab Network](01-lab-network.md)
- [03 - Kibana](03-kibana.md)
