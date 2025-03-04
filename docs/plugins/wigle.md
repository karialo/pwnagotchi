🔥 Wigle Plugin (v4.1.0) – Full Documentation 🔥  

📌 Overview  
The Wigle plugin integrates Pwnagotchi with [Wigle.net](https://wigle.net), a crowdsourced wireless network mapping platform. This allows Pwnagotchi to automatically upload detected Wi-Fi networks to Wigle’s global database, contributing to open-source wardriving efforts.  

✅ Uploads Wi-Fi network data to Wigle.net 🌍  
✅ Helps improve the global wireless mapping database 📡  
✅ Automates submissions using your Wigle API key 🔑  
✅ Supports GPS-based network tracking 📍  

If you're mapping networks with Pwnagotchi, this plugin automates Wigle submissions, making it easier than ever to contribute to the community.  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `4.1.0`  
- Location: `pwnagotchi/plugins/default/wigle.py`  

---

⚙️ How It Works  
The Wigle plugin runs in the background, collecting:  

✅ Wi-Fi SSIDs and BSSIDs (MAC addresses)  
✅ GPS coordinates (if available)  
✅ Signal strength & security type  

It then automatically uploads this data to Wigle using your Wigle API credentials.  

📌 Example Workflow:  
1️⃣ Pwnagotchi scans Wi-Fi networks  
2️⃣ GPS (if enabled) logs the exact location  
3️⃣ Data is collected and formatted  
4️⃣ Pwnagotchi submits to Wigle via the API  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it and set up your Wigle API credentials.  

1️⃣ Get Your Wigle API Key  
- Sign up at [Wigle.net](https://wigle.net)  
- Go to "My Account" > "API"  
- Copy your Wigle API Username & Key  

2️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the Wigle section:  

	[main.plugins.wigle]
	enabled = true
	username = "your_wigle_username"
	api_key = "your_wigle_api_key"
	upload_interval = 60  # Uploads every 60 minutes  

📌 Explanation of Config Options:  
- `enabled`: `true` to activate Wigle uploads  
- `username`: Your Wigle.net account username  
- `api_key`: Your Wigle API key (NOT your password)  
- `upload_interval`: How often (in minutes) Pwnagotchi uploads new networks  

3️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 Wigle Plugin Features  

🔥 Automatic Wi-Fi Network Uploads  
Pwnagotchi scans networks and submits them to Wigle automatically.  

🔥 Works With GPS for Location-Based Mapping  
If you have a GPS module enabled, Pwnagotchi logs exact network locations.  

🔥 Filter Out Your Own Networks  
To avoid uploading your personal Wi-Fi, add it to a blocklist:  

	ignore_networks = ["MyHomeWiFi", "MyWorkWiFi"]  

🔥 Offline Mode – Store Data & Upload Later  
If your Pwnagotchi doesn’t have internet, it will store data locally and upload when a connection is available.  

---

🚀 Useful Tips & Tricks  

🔥 Verify Uploaded Networks on Wigle.net  
After Pwnagotchi uploads data, check your Wigle profile:  

	https://wigle.net/account  

🔥 Use a GPS Module for Better Mapping  
To enable GPS logging, install & configure `gpsd`:  

	sudo apt install gpsd gpsd-clients  
	sudo systemctl enable gpsd  

🔥 View Collected Network Data Before Uploading  
Check pending uploads in:  

	/var/lib/pwnagotchi/wigle.json  

🔥 Manually Force an Upload  
To immediately upload stored networks:  

	pwnagotchi plugins run wigle  

🔥 Reduce Upload Frequency to Avoid Rate Limits  
Wigle limits excessive API requests—increase `upload_interval` if needed:  

	upload_interval = 120  # Upload every 2 hours  

🔥 Use a Secondary Account for Testing  
If you don’t want to submit real data to your main Wigle account, create a test account.  

---

🛠️ Debugging & Logs  
If Wigle uploads aren’t working, check logs:  

	tail -f /var/log/pwnagotchi.log | grep wigle  

If Pwnagotchi isn’t collecting network data, restart the plugin:  

	pwnagotchi plugins run wigle  

If GPS data isn’t being added, verify GPS is working:  

	gpsmon  

---

🔥 Final Thoughts  
The Wigle plugin is a must-have for wardriving enthusiasts, enabling seamless Wi-Fi mapping and automatic uploads to Wigle.net. Whether you’re mapping networks in your city or contributing to global open-source Wi-Fi research, this plugin makes it effortless to collect & submit data.  
