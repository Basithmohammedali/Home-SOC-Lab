# osTicket

## Purpose

This document describes how osTicket was deployed in the Home SOC Lab and integrated with Elastic Security to receive security alerts as incident tickets.

---

# Virtual Machine Configuration

| Setting | Value |
|----------|-------|
| Operating System | Windows Server |
| IP Address | 192.168.50.8 |
| Purpose | Ticket Management |

---

# Software Used

- XAMPP
- Apache
- MySQL
- PHP
- osTicket

---

# Install XAMPP

Download the XAMPP installer.

```
https://www.apachefriends.org/
```

Install XAMPP using the default settings.

After installation, start:

- Apache
- MySQL

---

# Install osTicket

Download the latest osTicket release.

```
https://osticket.com/download/
```

Extract the package.

Copy the `upload` directory into the XAMPP `htdocs` directory.

Complete the installation wizard from the browser.

---

# Configure XAMPP

Update the XAMPP configuration.

```
apache_domainname=192.168.50.8
mysql_host=192.168.50.8
```

Restart:

- Apache
- MySQL

---

# Configure API Access

Open:

```
Admin Panel → Manage → API
```

Create a new API key.

Record the generated API key because it will be used for automation.

---

# Access osTicket

Using VirtualBox Port Forwarding:

| Host Port | Guest Port |
|-----------|------------|
| 8080 | 80 |

Open:

```
http://127.0.0.1:8080/osticket/upload/scp/
```

Log in to the Staff Control Panel.

---

# Verification

Verify that:

- Apache is running.
- MySQL is running.
- osTicket login page loads successfully.
- Staff Control Panel is accessible.
- API key has been created.

---

# Troubleshooting

### Apache does not start

Verify that port 80 is available.

### Cannot access osTicket

Verify the VirtualBox Port Forwarding rule.

### API requests fail

Verify the API key and allowed client IP configuration.

---

# Related Documentation

- [06 - Mythic C2](06-mythic-c2.md)
- [08 - Detection Rules](08-detections.md)
- [09 - Automation](09-automation.md)
