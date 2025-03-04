🔥 Fix-Services Plugin (v1.0) – Full Documentation 🔥  

📌 Overview  
The Fix-Services plugin ensures that critical services required by Pwnagotchi are running properly. If something crashes or stops working, this plugin automatically restarts it, preventing downtime and keeping your device functional.  

✅ Monitors essential services like networking, Bluetooth, and logging  
✅ Automatically restarts services if they crash  
✅ Ensures stable operation of Pwnagotchi  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.0`  
- Location: `pwnagotchi/plugins/default/fix_services.py`  

---

⚙️ How It Works  
The Fix-Services plugin continuously checks whether essential system services are running. If it detects a failure, it will restart the affected service automatically.  

By default, it monitors:  
✅ Networking Services (`wpa_supplicant`, `dhcpcd`, `NetworkManager`)  
✅ Bluetooth Services (`bluetooth`, `bt-tether`)  
✅ Pwnagotchi Core Processes (`pwnagotchi-agent`, logging, UI updates)  

📌 Example:  
If `wpa_supplicant` (which handles Wi-Fi connections) crashes, Fix-Services will automatically restart it, preventing a loss of connectivity.  

---

🛠️ Installation & Setup  
This plugin is built-in, but you need to enable it to keep Pwnagotchi running smoothly.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the Fix-Services section:  

	[main.plugins.fix-services]
	enabled = true  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 What Services Does It Fix?  

🔥 Network Services (Wi-Fi / Ethernet):  
If networking crashes, the plugin restarts:  
✅ `wpa_supplicant` – Manages Wi-Fi connections  
✅ `dhcpcd` – Handles DHCP and IP assignment  
✅ `NetworkManager` – Manages all network interfaces  

🔥 Bluetooth Services:  
If Bluetooth tethering stops working, it restarts:  
✅ `bluetooth.service` – Main Bluetooth service  
✅ `bt-tether` – Pwnagotchi’s Bluetooth tethering plugin  

🔥 Pwnagotchi Core Processes:  
If Pwnagotchi itself crashes, it attempts to restart:  
✅ `pwnagotchi-agent` – The core AI process  
✅ `log services` – Ensures logs are being written  

---

🚀 Useful Tips & Tricks  

🔥 Manually Restart a Service:  

If you suspect something is broken, restart it manually:  

	sudo systemctl restart wpa_supplicant  


🔥 Check If a Service is Running:  

To verify that a service is active:  

	sudo systemctl status bluetooth  


🔥 Force Fix-Services to Run a Check:  
Instead of waiting for automatic detection, force a check:  

	pwnagotchi plugins run fix-services  


🔥 Disable Specific Service Monitoring:  

If you don’t want Bluetooth services restarted, disable them:  

	[main.plugins.fix-services]
	enabled = true
	monitor_bluetooth = false  

---

🛠️ Debugging & Logs  

Check logs to see if Fix-Services is working:  

	tail -f /var/log/pwnagotchi.log | grep fix-services  

If something keeps crashing repeatedly, check the service logs:  

	sudo journalctl -u wpa_supplicant --no-pager | tail -n 20  

---

🔥 Final Thoughts  
The Fix-Services plugin is a lifesaver when running Pwnagotchi unattended. By monitoring and auto-restarting critical services, it ensures that your device doesn’t randomly stop working.  
