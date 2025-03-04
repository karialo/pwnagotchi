🔥 Switcher Plugin (v0.0.1) – Full Documentation 🔥  

📌 Overview  
The Switcher plugin allows Pwnagotchi to toggle between multiple network modes dynamically, based on pre-configured conditions. It is useful for automatically switching between network profiles, such as:  

✅ Changing between access point (AP) mode and client mode  
✅ Connecting to a preferred Wi-Fi network when available  
✅ Reverting to an offline or monitoring mode when no networks are found  
✅ Automatically enabling/disabling Wi-Fi tethering based on connection state  

This is especially useful if you're running Pwnagotchi in multiple environments where network availability varies.  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `0.0.1`  
- Location: `pwnagotchi/plugins/default/switcher.py`  

---

⚙️ How It Works  
The Switcher plugin continuously monitors Wi-Fi connections and automatically switches network modes based on:  

✅ If a preferred Wi-Fi network is available → Pwnagotchi connects automatically  
✅ If no preferred network is found → Switch to AP mode for remote access  
✅ If a wired Ethernet connection is detected → Disable AP mode to save power  
✅ If in offline mode too long → Enable tethering to provide internet access  

📌 Example Use Case:  
1️⃣ At home – Pwnagotchi connects to `HomeWiFi` automatically  
2️⃣ At work – If `OfficeWiFi` is found, it switches profiles  
3️⃣ In the field – If no Wi-Fi is available, it enables AP mode for remote SSH access  
4️⃣ If Ethernet is plugged in – It disables Wi-Fi to save power  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it and configure network rules.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the Switcher section:  

	[main.plugins.switcher]
	enabled = true  
	default_mode = "client"  # Default mode when booting up  
	switch_interval = 30  # Check every 30 seconds  
	ap_mode_networks = ["PwnAP"]  # If no networks found, enable AP mode  
	preferred_networks = ["HomeWiFi", "OfficeWiFi"]  # Auto-connect to these  

📌 Explanation of Config Options:  
- `enabled`: `true` to activate automatic mode switching  
- `default_mode`: Initial mode (`"client"`, `"ap"`, `"monitor"`, etc.)  
- `switch_interval`: How often (in seconds) to check Wi-Fi status  
- `ap_mode_networks`: If no known Wi-Fi is found, switch to these  
- `preferred_networks`: List of preferred networks to auto-connect to  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 Example Use Cases  

🔥 Automatically Switch Between Home & Mobile Networks  
If you regularly move your Pwnagotchi between home and field deployments, set:  

	[main.plugins.switcher]
	preferred_networks = ["HomeWiFi", "PhoneHotspot"]  
	ap_mode_networks = ["PwnAP"]  

🔥 Enable AP Mode When No Networks Are Available  
Useful for enabling remote SSH access when in the field:  

	default_mode = "ap"  

🔥 Disable Wi-Fi When Ethernet is Connected  
If you want Pwnagotchi to disable Wi-Fi when Ethernet is plugged in (to save power), set:  

	disable_wifi_on_ethernet = true  

🔥 Use Tethering When No Internet is Available  
If Pwnagotchi loses internet access, enable Bluetooth tethering:  

	enable_bt_tether_on_disconnect = true  

---

🚀 Useful Tips & Tricks  

🔥 Manually Switch Modes via SSH  
To force a mode switch:  

	pwnagotchi plugins run switcher  

🔥 Force AP Mode (Useful for Remote Access)  
If you need AP mode immediately, disable switching temporarily:  

	sudo nmcli radio wifi off  
	sudo systemctl restart pwnagotchi  

🔥 Check Current Network Mode  
Run:  

	pwnagotchi plugins status switcher  

🔥 Reduce Power Consumption in Offline Mode  
If you want Pwnagotchi to shut down Wi-Fi when idle, add:  

	disable_wifi_when_idle = true  

🔥 View Current Wi-Fi Connections  
To see which network Pwnagotchi is using:  

	nmcli device status  

---

🛠️ Debugging & Logs  
If Switcher isn’t toggling network modes correctly, check logs:  

	tail -f /var/log/pwnagotchi.log | grep switcher  

If it’s not detecting networks, verify:  

	iw dev  

If manual switching fails, restart the plugin:  

	pwnagotchi plugins run switcher  

---

🔥 Final Thoughts  
The Switcher plugin is essential for users who move Pwnagotchi between locations, ensuring seamless connectivity without constant manual reconfiguration. Whether you're automating tethering, switching between multiple Wi-Fi networks, or enabling AP mode when offline, this plugin keeps Pwnagotchi online without hassle.  

---

✅ Next plugin? Drop the name and I’ll document it! 🚀🔥
