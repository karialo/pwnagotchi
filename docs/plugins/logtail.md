🔥 LogTail Plugin (v0.1.0) – Full Documentation 🔥  

📌 Overview  
The LogTail plugin allows you to monitor Pwnagotchi’s logs in real-time directly from its display. Instead of SSHing into the device to check logs, LogTail streams log entries onto the Pwnagotchi screen, helping you quickly diagnose issues or monitor activity.  

✅ Live log streaming directly on Pwnagotchi’s screen  
✅ Displays critical events such as handshake captures, AI training, and network scans  
✅ Helps with debugging and performance monitoring  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `0.1.0`  
- Location: `pwnagotchi/plugins/default/logtail.py`  

---

⚙️ How It Works  
The LogTail plugin reads the Pwnagotchi log file (`/var/log/pwnagotchi.log`) and displays the latest log entries on the e-ink screen.  

By default, it:  
✅ Updates every few seconds  
✅ Displays a fixed number of recent log lines  
✅ Automatically scrolls as new logs are generated  

📌 Example Log Display on Pwnagotchi Screen:  
```
[INFO]  Captured handshake: Starbucks-WiFi.pcap  
[DEBUG]  GPS coordinates logged: 37.7749, -122.4194  
[WARNING]  Low battery: 15% remaining  
[INFO]  Switching to manual mode  
```

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it and configure its display settings.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the LogTail section:  

	[main.plugins.logtail]
	enabled = true
	max_lines = 5  
	update_interval = 10  

📌 Explanation of Config Options:  
- `enabled`: `true` to activate live log display  
- `max_lines`: Number of log lines to show at a time  
- `update_interval`: Time in seconds between log updates  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 What Logs Does It Display?  
By default, LogTail shows logs from `/var/log/pwnagotchi.log`.  

Common log entries include:  
✅ Captured handshakes  
✅ Wi-Fi scanning results  
✅ AI training progress  
✅ Battery status  
✅ Mode changes (AI ↔ Manual)  

If you need more logs on-screen, increase `max_lines`.  

---

🚀 Useful Tips & Tricks  

🔥 Manually Check the Logs in SSH  
If the log display isn’t updating, check manually via SSH:  

	tail -f /var/log/pwnagotchi.log  

🔥 Show More Log Lines on Screen  
If 5 lines aren’t enough, increase the display buffer:  

	[main.plugins.logtail]
	max_lines = 10  

🔥 Speed Up Log Updates  
If logs take too long to refresh, lower the interval:  

	update_interval = 5  

🔥 Log Only Specific Events  
If you only want to display errors and warnings, modify `pwnagotchi.log`:  

	grep -E "(ERROR|WARNING)" /var/log/pwnagotchi.log  

🔥 Combine with Auto-Backup for Log Storage  
If you need to save logs regularly, enable the `auto-backup` plugin:  

	[main.plugins.auto-backup]
	enabled = true  

🔥 View Logs on an External Screen  
For bigger display output, forward logs to an external OLED or HDMI screen with:  

	tail -f /var/log/pwnagotchi.log > /dev/tty1  

---

🛠️ Debugging & Logs  
If the plugin isn’t displaying logs, check the logs for errors:  

	tail -f /var/log/pwnagotchi.log | grep logtail  

If LogTail isn’t running, manually start it:  

	pwnagotchi plugins run logtail  

---

🔥 Final Thoughts  
The LogTail plugin is an essential tool for live debugging, allowing you to monitor Pwnagotchi activity without needing SSH. Whether you're capturing handshakes or troubleshooting, this plugin keeps you informed in real-time.  
