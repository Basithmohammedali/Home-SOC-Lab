# Lab Network

## Purpose

This document describes the network configuration used in the Home SOC Lab. The environment is built using an isolated VirtualBox NAT Network to allow secure communication between all virtual machines while maintaining internet access.

---

# Network Configuration

| Setting | Value |
|----------|-------|
| Network Type | NAT Network |
| Network Name | basi-soc |
| Network Range | 192.168.50.0/24 |
| DHCP | Enabled |

---

# Virtual Machines

| Virtual Machine | Operating System | IP Address | Purpose |
|-----------------|------------------|------------|---------|
| ELK Server | Ubuntu Server | 192.168.50.3 | Elasticsearch and Kibana |
| Fleet Server | Ubuntu Server | 192.168.50.4 | Elastic Agent Management |
| Windows Server | Windows Server 2022 | 192.168.50.5 | Active Directory Domain Controller |
| Ubuntu Endpoint | Ubuntu Desktop | 192.168.50.6 | Linux Endpoint |
| Mythic C2 | Ubuntu Server | 192.168.50.7 | Command and Control |
| osTicket | Ubuntu Server | 192.168.50.8 | Ticket Management |
| Kali Linux | Kali Linux | 192.168.50.10 | Attack Simulation |

---

# VirtualBox Network Setup

1. Open **Oracle VirtualBox**.
2. Navigate to **Tools → Network**.
3. Click **Create** to create a new NAT Network.
4. Configure the network using the following settings:

| Setting | Value |
|----------|-------|
| Name | basi-soc |
| IPv4 Prefix | 192.168.50.0/24 |
| DHCP | Enabled |

5. Save the configuration.
6. Open each virtual machine.
7. Go to **Settings → Network**.
8. Select:
   - **Attached To:** NAT Network
   - **Name:** basi-soc
9. Start all virtual machines.

---

# Verify Network Connectivity

After all virtual machines are powered on, verify that they can communicate with each other.

Example:

```bash
ping 192.168.50.3
ping 192.168.50.4
ping 192.168.50.5
```

Successful replies indicate that the network has been configured correctly.

---

# Port Forwarding

To access virtual machines from the host operating system, configure VirtualBox Port Forwarding.

Example:

| VM | Host Port | Guest Port | Service |
|----|-----------|------------|---------|
| ELK Server | 2222 | 22 | SSH |
| Fleet Server | 2223 | 22 | SSH |
| Mythic C2 | 2224 | 22 | SSH |

Example SSH connection:

```bash
ssh -p 2222 basi@127.0.0.1
```

---

# Network Verification Checklist

- NAT Network created successfully.
- All virtual machines are connected to the `basi-soc` network.
- Each virtual machine has a unique IP address.
- Internet connectivity is available.
- Virtual machines can communicate with each other.
- SSH access works through Port Forwarding.

---

# Troubleshooting

### Virtual machine cannot access the network

- Verify that the VM is connected to the `basi-soc` NAT Network.
- Ensure the network adapter is enabled.
- Restart the virtual machine.

### IP address is incorrect

Run:

```bash
ip addr
```

or

```bash
hostname -I
```

Verify that the assigned IP address belongs to the `192.168.50.0/24` network.

### Unable to connect using SSH

- Verify the Port Forwarding rule.
- Confirm that the SSH service is running.
- Verify the Host Port and Guest Port configuration.

---

# Related Documentation

- [02 - ELK Server](02-elk-server.md)
- [03 - Kibana](03-kibana.md)
- [04 - Fleet Server](04-fleet-server.md)
