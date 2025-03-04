🔥 Grid Plugin (v1.1.0) – Full Documentation 🔥  

📌 Overview  
The Grid plugin enables Pwnagotchi to connect to and interact with the PwnGrid network, a decentralized system where Pwnagotchi devices share Wi-Fi handshakes and network data. This allows collaborative data collection across multiple devices, making Pwnagotchi more effective in larger environments.  

✅ Shares captured handshakes with other Pwnagotchi devices  
✅ Syncs data between multiple Pwnagotchis over the internet  
✅ Uses peer-to-peer communication via the PwnGrid network  
✅ Can function as a node in the grid, helping others find networks  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.1.0`  
- Location: `pwnagotchi/plugins/default/grid.py`  

---

⚙️ How It Works  
The Grid plugin connects Pwnagotchi to a global network of other Pwnagotchis.  
- Each device that joins the grid uploads captured handshakes.  
- Other devices download and share network information.  
- The system uses peer-to-peer syncing for decentralization.  

📌 Example:  
If you walk through a city and collect Wi-Fi handshakes, your device syncs the data with others in the PwnGrid network. Someone else on the grid can retrieve and analyze that data later.  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it and configure your PwnGrid credentials.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the Grid section:  

	[main.plugins.grid]
	enabled = true
	username = "your_pwngrid_username"
	password = "your_pwngrid_password"
	api = "https://api.pwngrid.com"
	share_handshakes = true  
	share_metadata = true  

📌 Explanation of Config Options:  
- `enabled`: `true` to enable the grid connection  
- `username`: Your PwnGrid account username  
- `password`: Your PwnGrid account password  
- `api`: The PwnGrid API endpoint  
- `share_handshakes`: `true` to share collected handshakes  
- `share_metadata`: `true` to share network metadata (AP names, BSSIDs, etc.)  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 How to Join the PwnGrid Network  

🔥 Step 1: Create a PwnGrid Account  
1️⃣ Visit [PwnGrid](https://pwngrid.com/) and register.  
2️⃣ Copy your username and password into `config.toml`.  

🔥 Step 2: Enable Grid Plugin  
Update `config.toml` and set `enabled = true`.  

🔥 Step 3: Check Grid Connection  
Run:  

	tail -f /var/log/pwnagotchi.log | grep grid  

If successful, you’ll see logs confirming the PwnGrid connection.  

🔥 Step 4: Verify Handshake Sharing  
After collecting handshakes, check if they’re uploaded:  

	ls /root/handshakes/  

If `share_handshakes = true`, your handshakes will sync to the grid.  

---

🚀 Useful Tips & Tricks  

🔥 Manually Force a Grid Sync  
To immediately sync your latest handshakes:  

	pwnagotchi plugins run grid  

🔥 Disable Metadata Sharing for Privacy  
If you want to share only handshakes (without network metadata), set:  

	share_metadata = false  

🔥 Check Your Grid Stats  
To see how many handshakes have been uploaded:  

	cat /var/log/pwnagotchi.log | grep "Uploaded handshake"  

🔥 Use Grid with GDriveSync  
If you don’t trust public PwnGrid servers, store handshakes on Google Drive instead using:  

	[main.plugins.gdrivesync]
	enabled = true  

🔥 Only Sync When on Wi-Fi  
If you’re on mobile data and want to avoid large uploads, set:  

	upload_only_on_wifi = true  

---

🛠️ Debugging & Logs  
Check if Pwnagotchi is connected to PwnGrid:  

	tail -f /var/log/pwnagotchi.log | grep grid  

If handshakes aren’t uploading, restart the plugin:  

	pwnagotchi plugins run grid  

If login fails, re-enter your credentials in `config.toml` and restart.  

---

🔥 Final Thoughts  
The Grid plugin makes Pwnagotchi more powerful by enabling data sharing across devices. Whether you're collecting handshakes solo or collaborating with a global network, PwnGrid makes wardriving easier and more effective.  
