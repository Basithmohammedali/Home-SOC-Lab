# Lab Network

## Network Configuration

| Setting | Value |
|---------|-------|
| Network Type | NAT Network |
| Network Name | basi-soc |
| Network Range | 192.168.50.0/24 |
| DHCP | Enabled |

## Virtual Machines

| Machine | IP Address |
|---------|------------|
| ELK Server | 192.168.50.3 |
| Fleet Server | 192.168.50.4 |
| Windows Server | 192.168.50.5 |
| Ubuntu Endpoint | 192.168.50.6 |
| Mythic C2 | 192.168.50.7 |
| osTicket | 192.168.50.8 |
| Kali Linux | 192.168.50.10 |

## VirtualBox Configuration

1. Open **VirtualBox**
2. Go to **Tools → Network**
3. Create a **NAT Network**
4. Configure:
   - Name: `basi-soc`
   - IPv4 Prefix: `192.168.50.0/24`
   - DHCP: Enabled
5. Connect every VM to the `basi-soc` network.

## Verification

Verify network connectivity:

```bash
ping 192.168.50.3
ping 192.168.50.4
ping 192.168.50.5
```
