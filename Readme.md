# LGTM-KubeSage Grafana Configuration Restore Guide

This guide helps you **restore your Grafana configuration and dashboards from a backup**.

---

## 📋 Prerequisites

- LGTM stack installed on your system.
- Backup folder containing:
  ```
  grafana-backup/
  ├── grafana.ini
  ├── provisioning/
  │   ├── dashboards/
  │   └── datasources/
  └── dashboards/
      ├── dashboard-1.json
      ├── dashboard-2.json
      └── ...
  ```

---

## 🔧 Step-by-Step Restore Instructions

### 1️⃣ Extract the Backup

If your backup is in `.tar` format:

```bash
tar -xvf grafana-backup.tar .
```

This will extract into a folder named `grafana-backup`.

---

### 2️⃣ Stop Grafana Service

Before making changes:

```bash
sudo systemctl stop grafana-server
```

---

### 3️⃣ Replace Configuration Files

#### 🔸 Copy `grafana.ini`

```bash
sudo cp grafana-backup/etc/grafana/grafana.ini /etc/grafana/grafana.ini
```

#### 🔸 Copy `provisioning/` Folder

```bash
sudo cp -r grafana-backup/etc/grafana/provisioning/* /etc/grafana/provisioning/
```

✅ **Optional backup (recommended):**

```bash
sudo cp -r /etc/grafana/provisioning /etc/grafana/provisioning.bak
```

#### 🔸 Copy Dashboards to Data Directory

```bash
sudo cp -r grafana-backup/var/lib/grafana/dashboards /var/lib/grafana/
```

---

### 4️⃣ Set Proper Permissions

Make sure the Grafana user owns the files:

```bash
sudo chown -R grafana:grafana /etc/grafana/
sudo chown -R grafana:grafana /var/lib/grafana/
```

Check file permissions:

```bash
sudo chmod -R 755 /etc/grafana/
sudo chmod -R 755 /var/lib/grafana/
```

---

### 5️⃣ Start Grafana Service

```bash
sudo systemctl start grafana-server
```

---

✅ **Done!** Your Grafana instance should now be restored with all dashboards and configurations.
