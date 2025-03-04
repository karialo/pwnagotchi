🔥 GPS Plugin (v1.0.1) – Full Documentation 🔥  

📌 Overview  
The GPS plugin allows Pwnagotchi to use a GPS module to log the exact location of captured Wi-Fi handshakes. This enables wardriving, mapping, and geotagging your hacking sessions.  

✅ Integrates with GPS modules (serial or USB)  
✅ Stores GPS coordinates with every captured handshake  
✅ Supports AP tracking and movement logging  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.0.1`  
- Location: `pwnagotchi/plugins/default/gps.py`  

---

⚙️ How It Works  
The GPS plugin connects to a serial GPS receiver (like the u-blox NEO-6M) or a USB GPS dongle. It continuously reads:  
✅ Latitude / Longitude – Exact GPS position  
✅ Altitude – Elevation above sea level  
✅ Speed – Movement speed  
✅ Timestamp – Accurate time sync  

When Pwnagotchi captures a Wi-Fi handshake, it records the GPS coordinates alongside it.  

📌 Example:  
Captured handshake from "Starbucks-WiFi"  
→ Location: `Lat: 37.7749, Lon: -122.4194`  
→ Saved to: `/root/handshakes/Starbucks-WiFi.pcap`  

---

🛠️ Installation & Setup  
This plugin is built-in, but you need to enable it and configure the GPS device.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the GPS section:  

	[main.plugins.gps]
	enabled = true
	port = "/dev/serial0"  # Change if using USB GPS
	baudrate = 9600  # Standard GPS baud rate
	timeout = 0.5  # Time before Pwnagotchi gives up on a GPS read  

📌 Explanation of Config Options:  
- `enabled`: `true` to enable GPS logging  
- `port`: Serial port of the GPS module (`/dev/serial0` for GPIO, `/dev/ttyUSB0` for USB)  
- `baudrate`: Speed of data transmission (most GPS modules use `9600`)  
- `timeout`: How long to wait for a GPS signal before giving up  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 GPS Hardware Setup  

🔥 Using a Serial GPS Module (u-blox NEO-6M)  
1️⃣ Connect the GPS module to Raspberry Pi’s GPIO:  

| GPS Pin | Raspberry Pi Pin |
|---------|-----------------|
| VCC | 3.3V (Pin 1) |
| GND | GND (Pin 6) |
| TX | GPIO 15 (Pin 10) |
| RX | GPIO 14 (Pin 8) |

2️⃣ Enable Serial Port on Raspberry Pi  

	sudo raspi-config  

- Go to Interfacing Options > Serial  
- Disable console login over serial  
- Enable serial hardware  

3️⃣ Reboot Pwnagotchi  

	sudo reboot  

🔥 Using a USB GPS Dongle  
If using a USB GPS receiver, plug it in and find its port:  

	ls /dev/ttyUSB*  

Update config.toml with the correct port:  

	[main.plugins.gps]
	port = "/dev/ttyUSB0"  

---

🚀 Useful Tips & Tricks  

🔥 Test GPS Signal Strength  
To check if GPS is working, install `gpsd`:  

	sudo apt install gpsd gpsd-clients  

Run `cgps` to see real-time GPS data:  

	cgps -s  

🔥 Enable GPS Debugging  
To log GPS activity, add this to config.toml:  

	[main.plugins.gps]
	debug = true  

Then, check logs:  

	tail -f /var/log/pwnagotchi.log | grep gps  

🔥 Upload GPS Data to Wigle.net  
Combine GPS with Wigle plugin for full Wi-Fi mapping:  

	[main.plugins.wigle]
	enabled = true  

🔥 Store GPS Data with Handshakes  
By default, GPS coordinates are logged in:  

	/root/handshakes/handshake_log.json  

To extract GPS-tagged handshakes, use:  

	jq '. | select(.gps != null)' /root/handshakes/handshake_log.json  

---

🛠️ Debugging & Logs  
Check if GPS data is being received:  

	tail -f /var/log/pwnagotchi.log | grep gps  

If no GPS signal, restart the GPS daemon:  

	sudo systemctl restart gpsd  

To check if Pwnagotchi sees the GPS device:  

	ls /dev/serial0  

or  

	ls /dev/ttyUSB*  

---

🔥 Final Thoughts  
The GPS plugin transforms Pwnagotchi into a powerful wardriving tool, allowing location-based tracking of Wi-Fi handshakes. With USB or serial GPS support, it’s perfect for mapping networks while staying mobile.  
