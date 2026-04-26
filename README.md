# Raspberry Pi Infrastructure

Real-world Raspberry Pi 5 infrastructure: NVMe storage, Docker services, and automated backups.

---

## 🧱 Environment

* Raspberry Pi 5
* Ubuntu Server
* NVMe SSD (primary data storage)
* SD card (OS)
* Docker (Nextcloud, Immich, Navidrome, etc.)
* External NAS (backup target)

---

## 🎯 Purpose

This repository documents real-world infrastructure work on a self-hosted Raspberry Pi system.

Focus areas:

* Storage architecture (SD → NVMe migration)
* Data safety (snapshot backups)
* Service reliability (Docker-based stack)
* Operational validation (health checks, monitoring)

---

## 📦 Cases

### Case 01 – Automated backups (SSH + rsync)

Reliable snapshot-based backup system to external NAS with retention and notifications.

➡️ `docs/case-01-backup-system.md`

---

### Case 02 – NVMe storage migration

Migrating all persistent data from SD card to NVMe with zero data loss and full service recovery.

➡️ `docs/case-02-nvme-migration.md`

---

## 🧠 Architecture Overview

```text
SD card:
  OS / boot

NVMe:
  /srv/docker   (all services)
  /home         (user data)

NAS:
  snapshot backups
```

---

## 🔐 Key Design Principles

* Never migrate live data without rollback
* Validate every step before committing
* Separate OS and data layers
* Automate backups early
* Monitor hardware health

---

## 📸 NVMe health monitoring with smartctl

![NVMe health monitoring](../screenshots/nvme-health-smartctl.png)

NVMe drive runs at ~50°C idle and ~80°C sensor peak without active cooling → airflow recommended for sustained workloads.

---

## Lessons learned

- Raspberry Pi 5 NVMe HAT supports only 2230/2242 → wrong SSD purchase initially
- SSH-based backup proved more reliable than NFS in this setup
- Bind mounts allow safe migration without breaking Docker
- SMART monitoring is essential for NVMe health visibility

---

## 🔮 Future Work

* NVMe SMART monitoring + alerting
* Docker-level backups (database dumps)
* Log analysis dashboard
* Security event monitoring (Fail2ban + alerts)

---
