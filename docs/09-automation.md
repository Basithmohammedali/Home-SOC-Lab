# SOC Automation

## Purpose

This document explains the automation workflow used in the Home SOC Lab to create osTicket incidents from Elastic Security alerts.

Instead of using the Elastic Webhook connector, a Python service was implemented after the trial license expired.

---

# Architecture

```
Elastic Security Alerts
            │
            ▼
Python Automation Script
            │
            ▼
osTicket API
            │
            ▼
Incident Ticket
```

---

# Components

| Component | Purpose |
|----------|---------|
| Elasticsearch | Stores security alerts |
| Python Script | Monitors active alerts |
| osTicket API | Creates incident tickets |
| systemd Service | Runs the automation continuously |

---

# Automation Workflow

1. Query Elastic Security for active alerts.
2. Check alerts generated during the last 5 minutes.
3. Extract important alert details.
4. Build an XML request.
5. Send the request to the osTicket API.
6. Create a new incident ticket.
7. Repeat every five minutes.

---

# Python Service

The automation script runs on the ELK server.

Example location:

```
/home/elk/osticket-alert.py
```

The script authenticates to Elasticsearch, retrieves active alerts, and submits new tickets to the osTicket API.

---

# systemd Service

A dedicated systemd service starts the automation automatically.

Example service:

```
/etc/systemd/system/osticket-alert.service
```

Useful commands:

```bash
sudo systemctl daemon-reload
sudo systemctl enable osticket-alert
sudo systemctl start osticket-alert
sudo systemctl status osticket-alert
```

---

# Verification

Verify that:

- The Python service is running.
- Elastic Security generates an alert.
- A new incident appears in osTicket.
- The service automatically starts after a reboot.

---

# Benefits

- No commercial Webhook license required.
- Fully automated incident creation.
- Runs continuously using systemd.
- Easy to maintain and customize.

---

# Related Documentation

- [07 - osTicket](07-osticket.md)
- [08 - Detection Rules](08-detections.md)
