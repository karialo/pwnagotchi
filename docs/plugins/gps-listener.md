🔥 GPS-Listener Plugin (v1.0.0) – Full Documentation 🔥  

📌 Overview  
The GPS-Listener plugin extends the GPS plugin by allowing Pwnagotchi to listen for external GPS data streams instead of directly interfacing with a GPS module. This is useful for setups where GPS data is coming from another device, such as a phone, external Raspberry Pi, or a remote GPS daemon.  

✅ Supports external GPS data sources  
✅ Reads NMEA GPS data from networked sources  
✅ Works with TCP, UDP, or serial connections  
✅ Pairs with GPS & Wigle plugins for full Wi-Fi geolocation  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.0.0`  
- Location: `pwnagotchi/plugins/default/gps_listener.py`  

---

⚙️ How It Works  
Unlike the standard GPS plugin, which communicates directly with a GPS module via serial or USB, the GPS-Listener plugin listens for incoming GPS data streams from an external source.  

Supported GPS data sources:  
✅ GPSD (over network or local device)  
✅ UDP GPS Feeds (e.g., from a mobile phone)  
✅ TCP GPS Streams  
✅ Remote Raspberry Pi GPS modules  

📌 Example:  
If your smartphone is running a GPS-to-UDP app, Pwnagotchi can listen for the GPS data and use it for logging Wi-Fi handshakes with exact locations.  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it and configure the GPS source.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the GPS-Listener section:  

	[main.plugins.gps_listener]
	enabled = true
	host = "192.168.1.100"  # Change to your GPS data source IP
	port = 2947  # GPSD default port
	protocol = "gpsd"  # Supports "gpsd", "udp", or "tcp"  

📌 Explanation of Config Options:  
- `enabled`: `true` to activate GPS listening  
- `host`: The IP address of the GPS data source  
- `port`: The network port where GPS data is streamed  
- `protocol`: Choose `"gpsd"` (for GPSD daemon), `"udp"`, or `"tcp"`  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 Setting Up GPS Data Sources  

🔥 Option 1: Use a Mobile Phone as GPS Source  
1️⃣ Install a GPS sharing app (e.g., [GPS2IP](https://www.gps2ip.com/) for iOS, [ShareGPS](https://play.google.com/store/apps/details?id=googoo.android.btgps) for Android).  
2️⃣ Configure the app to broadcast GPS data over UDP or TCP.  
3️⃣ Find your phone’s IP on the same network as Pwnagotchi.  
4️⃣ Update config.toml:  

	[main.plugins.gps_listener]
	host = "192.168.1.50"  # Your phone's IP
	port = 12345  # Port set in the app
	protocol = "udp"  

🔥 Option 2: Use a Remote Raspberry Pi GPS  
If you have another Raspberry Pi running GPSD, you can use it as a GPS server:  

1️⃣ Install GPSD on the remote Pi:  

	sudo apt install gpsd gpsd-clients  

2️⃣ Start GPSD and bind it to the network:  

	sudo gpsd /dev/ttyUSB0 -F /var/run/gpsd.sock -G  

3️⃣ Update Pwnagotchi's config to listen for GPS data:  

	[main.plugins.gps_listener]
	host = "192.168.1.150"  # Remote Pi's IP
	port = 2947  # GPSD default port
	protocol = "gpsd"  

🔥 Option 3: Connect to an Online GPS Service  
Some online services provide real-time GPS feeds over the internet.  
Simply enter the host IP and port of the service into `config.toml`.  

---

🚀 Useful Tips & Tricks  

🔥 Manually Check GPS Data  
If GPS isn't working, manually test it:  

	nc -u 192.168.1.100 2947  

If you see NMEA sentences (`$GPGGA, $GPRMC`), the GPS stream is active.  

🔥 Force GPS-Listener to Refresh  
If Pwnagotchi isn’t picking up GPS data, restart the listener manually:  

	pwnagotchi plugins run gps_listener  

🔥 Debug GPS Data Stream  
Enable debug mode in config.toml:  

	[main.plugins.gps_listener]
	debug = true  

Then check logs:  

	tail -f /var/log/pwnagotchi.log | grep gps_listener  

🔥 Pair GPS-Listener with Wigle Plugin for Full Wi-Fi Mapping  
Enable both plugins for geotagged Wi-Fi data uploads to Wigle.net:  

	[main.plugins.wigle]
	enabled = true  

---

🛠️ Debugging & Logs  
Check if Pwnagotchi is receiving GPS data:  

	tail -f /var/log/pwnagotchi.log | grep gps_listener  

To manually restart GPSD on a remote system:  

	sudo systemctl restart gpsd  

Check if the network GPS source is reachable:  

	ping 192.168.1.100  

---

🔥 Final Thoughts  
The GPS-Listener plugin is perfect for wardriving setups where Pwnagotchi needs live GPS data from a remote source. Whether you're using a smartphone, a second Raspberry Pi, or a networked GPS daemon, this plugin ensures your captured handshakes are geotagged and ready for mapping.  
