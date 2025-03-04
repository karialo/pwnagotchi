🔥 WebGPSMap Plugin (v1.4.0) – Full Documentation 🔥  

📌 Overview  

The WebGPSMap plugin provides a real-time GPS-enabled web interface that visually maps detected Wi-Fi networks and their locations. If your Pwnagotchi is connected to a GPS module, this plugin logs and displays access points on a live map, making it useful for wardriving and network analysis.  

✅ Displays Wi-Fi access points on an interactive web map 🗺️  
✅ Uses GPS coordinates to log network locations 📍  
✅ Accessible from any web browser 🌐  
✅ Exports captured data for later analysis  

If you're mapping Wi-Fi networks with Pwnagotchi + GPS, this plugin is essential.  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.4.0`  
- Location: `pwnagotchi/plugins/default/webgpsmap.py`  

---

⚙️ How It Works  

The WebGPSMap plugin collects GPS data and Wi-Fi network information, then serves it on a web interface that displays real-time or logged network locations on a map.  

📌 Access WebGPSMap  
1️⃣ Ensure your GPS module is working (`gpsd` must be installed & running)  
2️⃣ Open a browser and go to:  

	http://pwnagotchi.local:8081  

3️⃣ View a live map of Wi-Fi networks with GPS coordinates  

📌 Example Features in WebGPSMap UI:  
✅ Displays networks detected by Pwnagotchi 📡  
✅ Shows precise GPS locations 📍  
✅ Allows exporting data for further analysis 📊  
✅ Logs historical network locations 🗄️  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it and configure GPS settings.  

1️⃣ Enable the Plugin  

Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the WebGPSMap section:  

	[main.plugins.webgpsmap]
	enabled = true
	port = 8081
	gpsd_host = "localhost"
	gpsd_port = 2947
	map_center = [37.7749, -122.4194]  # Default to San Francisco  

📌 Explanation of Config Options:  
- `enabled`: `true` to activate WebGPSMap  
- `port`: Defines the web server port (`8081` by default)  
- `gpsd_host`: The GPS daemon (`gpsd`) hostname (usually `localhost`)  
- `gpsd_port`: Port used by `gpsd` (`2947` by default)  
- `map_center`: Default map location (latitude, longitude)  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 WebGPSMap Features  

🔥 Live Wi-Fi Mapping with GPS  
When enabled, Pwnagotchi logs network locations and displays them on a web map.  

🔥 Supports GPS Modules (USB, UART, Bluetooth)  
Compatible with most GPS devices supported by `gpsd`.  

🔥 Export Data for Further Analysis  
Captured network locations can be exported for use with Kismet, Wigle, or GIS tools.  

🔥 Adjust Map Center for Custom Locations  
By default, the map centers on San Francisco, but you can change it to your location:  

	map_center = [51.5074, -0.1278]  # London  

🔥 Filter Networks by Signal Strength & Security Type  
WebGPSMap allows sorting and filtering networks by signal strength and security settings.  

---

🚀 Useful Tips & Tricks  

🔥 Check if GPS is Working  
Before using WebGPSMap, ensure your GPS module is detected:  

	gpsmon  

If no GPS data is shown, restart the GPS daemon:  

	sudo systemctl restart gpsd  

🔥 Manually Start WebGPSMap  
To start the plugin manually:  

	pwnagotchi plugins run webgpsmap  

🔥 Enable GPS Logging for Offline Use  
To save GPS data for later, edit your config:  

	log_gps_data = true  

🔥 Change WebGPSMap Port (if 8081 is in use)  
If another service is using port 8081, change it:  

	port = 9091  

Then access it at:  

	http://pwnagotchi.local:9091  

---

🛠️ Debugging & Logs  

If WebGPSMap isn’t showing networks, check logs:  

	tail -f /var/log/pwnagotchi.log | grep webgpsmap  

If GPS isn’t working, check if `gpsd` is running:  

	sudo systemctl status gpsd  

If no networks are appearing, restart the plugin:  

	pwnagotchi plugins run webgpsmap  

---

🔥 Final Thoughts  
The WebGPSMap plugin turns Pwnagotchi into a powerful wardriving tool, allowing users to map, analyze, and export Wi-Fi network locations with GPS data. Whether you're visualizing networks in real-time or logging data for later, this plugin is one of the best tools for GPS-enabled Pwnagotchi setups.  
