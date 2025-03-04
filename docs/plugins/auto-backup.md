🔥 Auto-Backup Plugin (v1.1.3) – Full Documentation 🔥

📌 Overview
The Auto-Backup plugin automatically backs up critical Pwnagotchi data at regular intervals. This ensures you never lose handshakes, logs, or configuration files if your device crashes or gets corrupted.  

✅ Automates backup creation at set intervals  
✅ Stores backups in a defined location (local or external)  
✅ Supports custom backup frequency  

---

👤 Author & Version
- Author: Pwnagotchi Core Team  
- Version: `1.1.3`  
- Location: `pwnagotchi/plugins/default/auto_backup.py`

---

⚙️ How It Works  
The plugin periodically compresses important files (configs, handshakes, logs) and stores them in a backup directory.  

By default, it:  
- Runs every 24 hours  
- Backs up data to `/var/backups/pwnagotchi/`  
- Archives handshake files, logs, and configuration files

You can change the interval, storage location, and included files via config.

---

🛠️ Installation & Setup
This plugin is built into Pwnagotchi – you just need to enable it in the config.

1️⃣ Enable the Plugin
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml

Find (or add) the Auto-Backup section and configure it:

	[main.plugins.auto-backup]
	enabled = true
	backup_interval = 24  # Backup every 24 hours
	backup_path = "/var/backups/pwnagotchi"
	compress = true  # Save storage space by compressing backups
	max_backups = 5  # Keep only the last 5 backups

📌 Explanation of Config Options:  
- `enabled`: `true` to activate auto-backups  
- `backup_interval`: How often (in hours) a backup is created  
- `backup_path`: Where backups are stored  
- `compress`: Whether to zip backups for storage efficiency  
- `max_backups`: Limits number of saved backups (prevents disk bloat)  

2️⃣ Restart Pwnagotchi to Apply Changes

	sudo systemctl restart pwnagotchi

---

📂 What’s Included in the Backup?

By default, Auto-Backup saves:  
✅ `/etc/pwnagotchi/` → Configuration files  
✅ `/root/handshakes/` → Captured WPA handshakes  
✅ `/var/log/pwnagotchi.log` → Logs  

---

🛠️ Restore a Backup

To restore a backup:
	tar -xzf /var/backups/pwnagotchi/backup-YYYY-MM-DD.tar.gz -C /

Replace `YYYY-MM-DD` with the actual backup date.

---

🚀 Useful Tips & Tricks

🔥 Store Backups Externally:
To back up to an external USB drive, change `backup_path` to:  

	backup_path = "/mnt/usb/pwnagotchi-backups"

Make sure your USB drive is mounted properly.

🔥 Sync with Google Drive (GDriveSync Plugin):  
Combine Auto-Backup with the `gdrivesync` plugin to **upload backups to Google Drive**.

🔥 Manual Backup Anytime:
Run this command to manually trigger a backup:  

	pwnagotchi plugins run auto-backup

---

🛠️ Debugging & Logs
Check if backups are running correctly:  

	tail -f /var/log/pwnagotchi.log | grep auto-backup

If the plugin isn’t working, restart Pwnagotchi and recheck logs.

---

🔥 Final Thoughts
The Auto-Backup plugin is essential if you want to protect your captured handshakes and settings. With custom storage locations, automatic scheduling, and compression support, it ensures you never lose valuable data.  

