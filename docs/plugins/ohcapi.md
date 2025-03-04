🔥 OHCAPI Plugin (v1.1.0) – Full Documentation 🔥  

📌 Overview  
The OHCAPI (Open Handshake Capture API) plugin provides a REST API that allows external tools to interact with Pwnagotchi's captured handshakes and network data. This means you can remotely access your handshakes, metadata, and other useful statistics via HTTP requests, making automation and integration with other tools much easier.  

✅ Exposes a REST API for external access  
✅ Retrieve captured handshakes remotely  
✅ Access live scan results, metadata, and device stats  
✅ Useful for automation, scripting, and third-party integrations  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.1.0`  
- Location: `pwnagotchi/plugins/default/ohcapi.py`  

---

⚙️ How It Works  
The OHCAPI plugin runs a lightweight HTTP server on your Pwnagotchi, allowing you to query network data and handshake captures from another device.  

📌 Example Use Case:  
- You run a Python script on your laptop to fetch new handshakes from Pwnagotchi  
- You automate Wi-Fi recon by polling scan results over the API  
- You integrate Pwnagotchi with a dashboard or monitoring tool  

📌 API Endpoints (Examples)  
1️⃣ List captured handshakes  

	GET http://pwnagotchi.local:8080/handshakes  

2️⃣ Retrieve Pwnagotchi status  

	GET http://pwnagotchi.local:8080/status  

3️⃣ Get scan results  

	GET http://pwnagotchi.local:8080/networks  

The API returns JSON responses, making it easy to parse and automate tasks.  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it and configure an API port.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the OHCAPI section:  

	[main.plugins.ohcapi]
	enabled = true
	port = 8080  
	address = "0.0.0.0"  # Allow connections from any device  

📌 Explanation of Config Options:  
- `enabled`: `true` to start the API server  
- `port`: The HTTP port to serve the API (default: 8080)  
- `address`:  
  - `"0.0.0.0"` = Accept connections from any device  
  - `"127.0.0.1"` = Only allow local access  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 API Usage Examples  

🔥 List All Captured Handshakes  
Run this command on another device:  

	curl http://pwnagotchi.local:8080/handshakes  

📌 Example Response:  

json:
{
  "handshakes": [
    {"ssid": "Starbucks-WiFi", "bssid": "AA:BB:CC:DD:EE:FF", "file": "starbucks.pcap"},
    {"ssid": "HomeNetwork", "bssid": "11:22:33:44:55:66", "file": "home.pcap"}
  ]
}
  

🔥 Download a Specific Handshake  
To retrieve a handshake file, use:  

	curl -O http://pwnagotchi.local:8080/handshakes/starbucks.pcap  

🔥 Monitor Active Network Scans  
Get live Wi-Fi scan results:  

	curl http://pwnagotchi.local:8080/networks  

📌 Example Response: 
 
json:
{
  "networks": [
    {"ssid": "McDonalds-WiFi", "bssid": "DE:AD:BE:EF:01:02", "signal": -45},
    {"ssid": "FreeAirportWiFi", "bssid": "CA:FE:BA:BE:03:04", "signal": -60}
  ]
}
  

🔥 Check Pwnagotchi Status  
Get system stats like uptime, mode, and battery:  

	curl http://pwnagotchi.local:8080/status  

📌 Example Response:  

json:
{
  "status": "AI Mode",
  "uptime": "3h 42m",
  "battery": "85%",
  "current_handshakes": 5
}
  

---

🚀 Useful Tips & Tricks  

🔥 Access API from a Phone or Tablet  
If you want to view Pwnagotchi’s handshakes and scans on mobile, just open:  

	http://pwnagotchi.local:8080/  

🔥 Secure the API with a Firewall  
To prevent unauthorized access, only allow your device to connect:  

	sudo ufw allow from 192.168.1.100 to any port 8080  

🔥 Use a Python Script for Automation  
Example: Fetch handshakes programmatically:  

python
import requests

response = requests.get("http://pwnagotchi.local:8080/handshakes")
data = response.json()

for handshake in data["handshakes"]:
    print(f"Captured: {handshake['ssid']} - {handshake['file']}")
  

🔥 Integrate with WiGLE or Other Mapping Tools  
By pairing this API with WiGLE or Kismet, you can:  
✅ Automate Wi-Fi tracking & mapping  
✅ Download handshakes remotely without SSH  

🔥 Run the API on a Custom Port  
To avoid conflicts, change the port:  

	port = 9090  

Then restart Pwnagotchi:  

	sudo systemctl restart pwnagotchi  

---

🛠️ Debugging & Logs  
If the API isn’t responding, check logs:  

	tail -f /var/log/pwnagotchi.log | grep ohcapi  

If the API fails to start, check if another process is using port 8080:  

	sudo netstat -tulnp | grep 8080  

Change the port if necessary and restart the service.  

---

🔥 Final Thoughts  
The OHCAPI plugin is one of the most powerful plugins for remote control, automation, and data retrieval. Whether you're scripting custom tools, integrating with WiGLE, or monitoring from a browser, this plugin makes Pwnagotchi fully accessible via REST API.  
