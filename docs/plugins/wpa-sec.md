🔥 WPA-SEC Plugin (v2.1.1) – Full Documentation 🔥  

📌 Overview  
The WPA-SEC plugin automatically uploads captured WPA handshakes from your Pwnagotchi to wpa-sec.stanev.org, a public WPA handshake verification and cracking service. This allows you to:  

✅ Check if captured handshakes are valid  
✅ Leverage a cloud-based cracking service  
✅ Help contribute to a global WPA password database  

If you're using Pwnagotchi to collect WPA handshakes, this plugin automates verification and potential cracking attempts.  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `2.1.1`  
- Location: `pwnagotchi/plugins/default/wpa-sec.py`  

---

⚙️ How It Works  
Whenever Pwnagotchi captures a valid WPA handshake, this plugin:  

✅ Uploads it to [wpa-sec.stanev.org](https://wpa-sec.stanev.org/)  
✅ Checks if the handshake is valid  
✅ Attempts to crack it using pre-existing databases  
✅ Notifies you if a successful crack occurs  

📌 Example Workflow:  
1️⃣ Pwnagotchi detects and captures a WPA handshake  
2️⃣ Handshake file is automatically uploaded  
3️⃣ WPA-SEC verifies if the handshake is valid  
4️⃣ If the network password is known, WPA-SEC sends it back  
5️⃣ You can retrieve cracked passwords from WPA-SEC  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it and configure your WPA-SEC API key.  

1️⃣ Get Your WPA-SEC API Key  
- Visit [wpa-sec.stanev.org](https://wpa-sec.stanev.org/?register)  
- Sign up for an account  
- Copy your WPA-SEC API key  

2️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the WPA-SEC section:  

	[main.plugins.wpa-sec]
	enabled = true
	api_key = "your-wpa-sec-api-key"
	upload = true
	upload_interval = 30  # Upload every 30 minutes  

📌 Explanation of Config Options:  
- `enabled`: `true` to activate WPA-SEC integration  
- `api_key`: Your WPA-SEC API key  
- `upload`: `true` to automatically upload handshakes  
- `upload_interval`: Defines how often handshakes are uploaded (in minutes)  

3️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 WPA-SEC Features  

🔥 Automatic Handshake Uploading  
- Every captured WPA handshake is uploaded automatically  
- No need to manually extract and upload handshakes  

🔥 Verify Handshakes for Validity  
- Check if your handshake captures are valid  
- Avoid wasting time on invalid network handshakes  

🔥 Cloud-Based Cracking Assistance  
- WPA-SEC cross-checks against its database  
- If the password is already cracked, you get it back instantly  

🔥 Filter Out Personal or Trusted Networks  
To exclude specific SSIDs from uploading, add them to a blocklist:  

	ignore_networks = ["MyHomeWiFi", "MyWorkWiFi"]  

🔥 Offline Mode – Store Handshakes & Upload Later  
If your Pwnagotchi doesn’t have internet, it will store handshakes locally and upload them later.  

---

🚀 Useful Tips & Tricks  

🔥 Manually Upload Handshakes  
If you prefer to upload handshakes yourself, disable automatic uploads:  

	upload = false  

Then manually upload handshakes with:  

	pwnagotchi plugins run wpa-sec  

🔥 Retrieve Cracked Passwords  
Once WPA-SEC processes your handshakes, you can check cracked passwords at:  

	https://wpa-sec.stanev.org/?mycracks  

🔥 Manually Verify a Handshake File  
If you're unsure whether a handshake is valid, check with:  

	wpa-sec -check /root/handshakes/example.cap  

🔥 Reduce Upload Frequency to Avoid Rate Limits  
If you’re uploading too frequently, increase the `upload_interval`:  

	upload_interval = 120  # Upload every 2 hours  

🔥 Save Handshakes to a USB Drive Instead of Uploading  
If you want to store handshakes but not upload them, set:  

	upload = false  
	handshake_path = "/mnt/usb/handshakes"  

🔥 Use Hashcat or Aircrack-NG for Local Cracking  
For offline password cracking, export handshakes and use:  

	hashcat -m 2500 example.cap rockyou.txt  

or  

	aircrack-ng -w rockyou.txt -b AA:BB:CC:DD:EE:FF example.cap  

---

🛠️ Debugging & Logs  
If WPA-SEC uploads aren’t working, check logs:  

	tail -f /var/log/pwnagotchi.log | grep wpa-sec  

If handshakes aren’t being uploaded, restart the plugin:  

	pwnagotchi plugins run wpa-sec  

To see pending handshake uploads, check:  

	/var/lib/pwnagotchi/wpa-sec-uploads.json  

---

🔥 Final Thoughts  
The WPA-SEC plugin is a powerful automation tool that eliminates manual work in verifying & cracking WPA handshakes. By integrating with wpa-sec.stanev.org, it allows Pwnagotchi users to instantly validate captures, submit them to the cloud, and retrieve cracked passwords when available.  

Whether you're a Wi-Fi security researcher or just experimenting with WPA handshake cracking, this plugin makes the process faster, easier, and fully automated.  
