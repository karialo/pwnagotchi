🔥 Auto-Update Plugin (v1.1.1) – Full Documentation 🔥  

📌 Overview  
The Auto-Update plugin ensures that Pwnagotchi, Bettercap, and PwnGrid stay up to date automatically. Instead of manually updating system components, this plugin fetches the latest releases and updates them as needed.  

✅ Checks for updates to Pwnagotchi, Bettercap, and PwnGrid  
✅ Automatically installs updates when available  
✅ Reduces the risk of running outdated security tools  
✅ Keeps the system running with the latest patches and improvements  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.1.1`  
- Location: `pwnagotchi/plugins/default/auto-update.py`  

---

⚙️ How It Works  
Auto-Update periodically checks for new versions of:  
✅ Pwnagotchi (the main software)  
✅ Bettercap (the network attack tool)  
✅ PwnGrid (if enabled, for sharing WPA handshakes)  

It pulls update information from the official GitHub repositories and compares the installed version to the latest available version. If an update is detected, it attempts to download and install it.  

By default, Auto-Update:  
- Runs once per day  
- Checks for updates to Bettercap, PwnGrid, and Pwnagotchi  
- Installs updates automatically  

---

🛠️ Installation & Setup  
This plugin comes pre-installed, but you need to enable it.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the Auto-Update section:  

	[main.plugins.auto-update]
	enabled = true
	check_interval = 24  # Check for updates every 24 hours
	update_bettercap = true  # Auto-update Bettercap
	update_pwngrid = true  # Auto-update PwnGrid
	update_pwnagotchi = true  # Auto-update Pwnagotchi itself  

📌 Explanation of Config Options:  
- `enabled`: `true` to enable Auto-Update  
- `check_interval`: How often (in hours) Pwnagotchi checks for updates  
- `update_bettercap`: If `true`, Bettercap updates automatically  
- `update_pwngrid`: If `true`, PwnGrid updates automatically  
- `update_pwnagotchi`: If `true`, Pwnagotchi updates automatically  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 Update Process  
When an update is available, Auto-Update follows this process:  
✅ Checks current versions of Pwnagotchi, Bettercap, and PwnGrid  
✅ Fetches the latest versions from their respective GitHub repositories  
✅ Downloads and installs updates if needed  
✅ Restarts services automatically to apply changes  

---

🛠️ Manually Trigger an Update  
If you want to check for updates manually, run:  

	pwnagotchi plugins run auto-update  

To force a full update, use:  

	sudo pwnagotchi-update  

To check installed versions:  

	bettercap -version  
	pwngrid -version  
	pwnagotchi --version  

---

🚀 Useful Tips & Tricks  

🔥 Disable Specific Updates  
If you only want to update Pwnagotchi but not Bettercap, disable Bettercap updates:  

	[main.plugins.auto-update]
	update_bettercap = false  

🔥 Check Updates Without Installing  
If you only want to check for updates without installing, set:  

	[main.plugins.auto-update]
	enabled = true
	check_only = true  

🔥 Use a Custom Update Server  
If you want custom update sources, modify the repository settings inside the plugin script.  

---

🛠️ Debugging & Logs  
Check update logs:  

	tail -f /var/log/pwnagotchi.log | grep auto-update  

If something goes wrong, restart Pwnagotchi:  

	sudo systemctl restart pwnagotchi  

---

🔥 Final Thoughts  
The Auto-Update plugin ensures that Pwnagotchi and its key components remain up to date with the latest features and security fixes. It’s an essential tool for keeping your hacking gear fresh and effective.  

---

✅ Next plugin? Drop the name and I’ll document it! 🚀🔥
