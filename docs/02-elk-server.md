# ELK Server

## VM Configuration

| Setting | Value |
|---------|-------|
| OS | Ubuntu Server 22.04 |
| RAM | 2 GB |
| CPU | 2 vCPU |
| Disk | 25 GB |
| IP Address | 192.168.50.3 |

---

## Configure SSH

```bash
hostname -I
```

Create a VirtualBox port forwarding rule.

Host Port: 2222

Guest Port: 22

---

## Expand Disk

```bash
sudo vgs
sudo lvextend -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
df -h
```

---

## Update Ubuntu

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Install Elasticsearch

```bash
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-9.4.2-amd64.deb
sudo dpkg -i elasticsearch-9.4.2-amd64.deb
```

---

## Configure Elasticsearch

File:

```text
/etc/elasticsearch/elasticsearch.yml
```

```yaml
network.host: 192.168.50.3
http.port: 9200
```

---

## Start Elasticsearch

```bash
sudo systemctl daemon-reload
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
sudo systemctl status elasticsearch
```
