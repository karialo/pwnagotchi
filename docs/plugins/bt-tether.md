🔥 BT-Tether Plugin (v1.4) – Full Documentation 🔥  

📌 Overview  
The BT-Tether plugin allows Pwnagotchi to connect to your phone via Bluetooth and use its internet connection for updates, reporting, or syncing data. This is especially useful when running Pwnagotchi without Wi-Fi or when you want to monitor it remotely.  

✅ Tethers Pwnagotchi to your phone’s internet via Bluetooth  
✅ Supports both Android and iOS devices  
✅ Allows SSH access over Bluetooth  
✅ Enables remote updates and data syncing without Wi-Fi  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.4`  
- Location: `pwnagotchi/plugins/default/bt-tether.py`  

---

⚙️ How It Works  
The BT-Tether plugin pairs your phone to Pwnagotchi via Bluetooth and enables Bluetooth-based network sharing.  
It can be used for:  
✅ Remote SSH Access – Connect to Pwnagotchi without needing Wi-Fi  
✅ Internet Access – Use your phone’s data for updates & cloud sync  
✅ Remote Control – Monitor your Pwnagotchi from a Bluetooth-connected device  

By default, it:  
- Connects to a paired phone when Bluetooth is available  
- Uses NetworkManager to establish an internet connection  
- Automatically reconnects if disconnected  

---

🛠️ Installation & Setup  
This plugin comes pre-installed, but you need to enable it and configure pairing.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the BT-Tether section:  

	[main.plugins.bt-tether]
	enabled = true
	phone = "XX:XX:XX:XX:XX:XX"  # Replace with your phone’s Bluetooth MAC address
	interval = 60  # Check connection every 60 seconds
	max_retries = 5  # Retry 5 times if disconnected
	share_internet = true  # Use phone’s internet connection  

📌 Explanation of Config Options:  
- `enabled`: `true` to enable Bluetooth tethering  
- `phone`: Your phone’s Bluetooth MAC address (get it from `bluetoothctl scan on`)  
- `interval`: How often (in seconds) Pwnagotchi checks if the phone is still connected  
- `max_retries`: Number of connection attempts before giving up  
- `share_internet`: If `true`, allows Pwnagotchi to use the phone’s mobile data  

2️⃣ Pair Pwnagotchi with Your Phone  
Run the following:  

	sudo bluetoothctl  
	agent on  
	scan on  

Wait for your phone’s MAC address to appear, then pair:  

	pair XX:XX:XX:XX:XX:XX  
	trust XX:XX:XX:XX:XX:XX  
	connect XX:XX:XX:XX:XX:XX  

Once connected, exit Bluetooth control:  

	exit  

3️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 Using Bluetooth Tethering  

🔥 Check Connection Status:  
To see if Bluetooth tethering is active:  

	nmcli device status  

If connected, you should see an interface like bnep0 (Bluetooth Network Encapsulation Protocol).  

🔥 Manually Start a Connection:  
If the plugin doesn’t connect automatically:  

	sudo systemctl restart bluetooth  
	sudo bt-pan client XX:XX:XX:XX:XX:XX  

🔥 Set Up Bluetooth SSH Access:  
Find your Bluetooth network interface:  

	ifconfig  

Use the IP address to SSH into Pwnagotchi over Bluetooth:  

	ssh pi@<bluetooth-ip>  

---

🚀 Useful Tips & Tricks  

🔥 Enable Bluetooth Tethering Automatically on Android:  
Go to Settings > Tethering & portable hotspot > Bluetooth tethering and enable it.  

🔥 Use Bluetooth Instead of Wi-Fi for Low Profile Mode:  
For stealth operations, disable Wi-Fi and use only Bluetooth SSH to access Pwnagotchi:  

	[main.plugins.bt-tether]
	enabled = true
	share_internet = false  # No internet, just Bluetooth access  

🔥 Reconnect Automatically if Disconnected:  
If Bluetooth disconnects often, increase `max_retries`:  

	max_retries = 10  

---

🛠️ Debugging & Logs  
Check if Bluetooth tethering is working:  

	tail -f /var/log/pwnagotchi.log | grep bt-tether  

Restart Bluetooth services if needed:  

	sudo systemctl restart bluetooth  

---

🔥 Final Thoughts  
The BT-Tether plugin is essential for remote access when Wi-Fi isn’t an option. Whether you need internet sharing, Bluetooth SSH, or low-profile control, this plugin makes it easy to connect on the go.  

