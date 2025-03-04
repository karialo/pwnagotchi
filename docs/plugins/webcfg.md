🔥 WebConfig Plugin (v1.0.0) – Full Documentation 🔥  

📌 Overview  
The WebConfig (webcfg) plugin provides a web-based configuration interface for Pwnagotchi, allowing you to manage settings, enable/disable plugins, and tweak network parameters directly from your browser.  

✅ Edit Pwnagotchi’s config file without SSH  
✅ Enable/disable plugins easily  
✅ Modify network settings, AI tuning, and logging  
✅ User-friendly interface, accessible via web browser  

This plugin is ideal for users who prefer a GUI over editing `config.toml` manually.  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.0.0`  
- Location: `pwnagotchi/plugins/default/webcfg.py`  

---

⚙️ How It Works  
The WebConfig plugin launches a web server on Pwnagotchi, accessible from any device on the same network.  

📌 Access WebConfig  
1️⃣ Connect to Pwnagotchi’s network (either Wi-Fi or via USB tethering)  
2️⃣ Open a browser and go to:  

	http://pwnagotchi.local:8080  

3️⃣ Modify settings & save changes  
4️⃣ Reboot Pwnagotchi for the new settings to apply  

📌 Example Features in WebConfig UI:  
✅ Enable/Disable Plugins 📌  
✅ Edit Wi-Fi & network settings 📡  
✅ Modify AI learning parameters 🧠  
✅ Change screen display settings 🖥️  
✅ View logs & system info 📜  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it to start the web interface.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the WebConfig section:  

	[main.plugins.webcfg]
	enabled = true
	bind_address = "0.0.0.0"
	port = 8080
	allowed_ips = ["0.0.0.0/0"]  

📌 Explanation of Config Options:  
- `enabled`: `true` to activate the WebConfig UI  
- `bind_address`: `"0.0.0.0"` allows access from any IP  
- `port`: Defines the web server port (`8080` by default)  
- `allowed_ips`: Restricts access to specific IP ranges  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 WebConfig Features  

🔥 Easily Edit Config Without SSH  
Instead of running `nano /etc/pwnagotchi/config.toml`, just use the web UI.  

🔥 Enable & Disable Plugins in One Click  
No need to modify config files—just toggle plugins on/off via WebConfig.  

🔥 Modify Network Settings (Wi-Fi, Tethering, AP Mode)  
Configure wireless connectivity directly in the UI.  

🔥 Adjust AI Learning & Handshake Capture Parameters  
Fine-tune how Pwnagotchi interacts with networks and optimizes WPA handshakes.  

🔥 View Logs & Debugging Information  
Easily check logs for plugin activity, network scans, and system events.  

---

🚀 Useful Tips & Tricks  

🔥 Access WebConfig from Any Device  
If Pwnagotchi is connected to Wi-Fi, find its IP:  

	ip a  

Then access WebConfig using:  

	http://[pwnagotchi-ip]:8080  

🔥 Make WebConfig More Secure  
By default, WebConfig allows access from any IP. To restrict access:  

	allowed_ips = ["192.168.1.0/24"]  # Only allow devices in 192.168.1.x range  

🔥 Use a Custom Port  
Change the `port` setting if 8080 is blocked:  

	port = 9090  

Then access WebConfig at:  

	http://pwnagotchi.local:9090  

🔥 Restart Pwnagotchi from WebConfig  
There’s an option in WebConfig to restart the device safely after changes.  

---

🛠️ Debugging & Logs  
If WebConfig isn’t accessible, check logs:  

	tail -f /var/log/pwnagotchi.log | grep webcfg  

If the web interface isn’t starting, manually restart the plugin:  

	pwnagotchi plugins run webcfg  

To check if WebConfig is running, list active processes:  

	ps aux | grep webcfg  

---

🔥 Final Thoughts  
The WebConfig plugin makes managing Pwnagotchi easier than ever, eliminating the need for SSH and manual file edits. Whether you’re tweaking AI settings, enabling plugins, or adjusting networking, WebConfig provides a user-friendly, browser-based solution.  
