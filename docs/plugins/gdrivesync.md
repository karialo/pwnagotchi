🔥 GDriveSync Plugin (v1.4) – Full Documentation 🔥  

📌 Overview  
The GDriveSync plugin automatically uploads Pwnagotchi data to Google Drive, ensuring that your handshakes, logs, and configurations are safely stored in the cloud. This prevents data loss due to SD card corruption or unexpected shutdowns.  

✅ Automatically uploads WPA handshakes & logs to Google Drive  
✅ Ensures backups are available even if your Pwnagotchi fails  
✅ Uses Google Drive API for seamless syncing  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.4`  
- Location: `pwnagotchi/plugins/default/gdrivesync.py`  

---

⚙️ How It Works  
The GDriveSync plugin runs at scheduled intervals, scans for new WPA handshakes and logs, and uploads them to a dedicated Google Drive folder.  

By default, it:  
- Uploads handshakes stored in `/root/handshakes/`  
- Uploads log files from `/var/log/pwnagotchi.log`  
- Runs every hour to check for new files  
- Uses OAuth authentication for secure access  

📌 Example:  
If Pwnagotchi captures a new WPA handshake, GDriveSync will automatically upload it to Google Drive, making it available from anywhere.  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must configure Google Drive access before using it.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the GDriveSync section:  

	[main.plugins.gdrivesync]
	enabled = true
	interval = 60  # Sync every 60 minutes
	folder_id = "YOUR_GOOGLE_DRIVE_FOLDER_ID"  # Replace with your actual Google Drive folder ID  

📌 Explanation of Config Options:  
- `enabled`: `true` to activate syncing  
- `interval`: How often (in minutes) to sync new files  
- `folder_id`: The Google Drive folder ID where files are uploaded  

---

🔑 Setting Up Google Drive Authentication  

Since Pwnagotchi doesn’t come pre-authenticated for Google Drive, you must create API credentials and authorize access.  

1️⃣ Install Google Drive API dependencies:  

	sudo apt update && sudo apt install python3-pip
	pip3 install --upgrade google-auth google-auth-oauthlib google-auth-httplib2 google-api-python-client  

2️⃣ Create Google Drive API Credentials:  
- Go to [Google Cloud Console](https://console.cloud.google.com/)  
- Create a new project  
- Enable Google Drive API  
- Go to Credentials > Create Credentials > OAuth 2.0 Client ID  
- Download the client_secret.json file  

3️⃣ Move `client_secret.json` to Pwnagotchi:  

	sudo mv client_secret.json /etc/pwnagotchi/client_secret.json  

4️⃣ Authenticate Pwnagotchi:  

	pwnagotchi plugins run gdrivesync --auth  

This will generate a link to authorize your device. Follow the instructions and paste the verification code.  

---

📂 What Gets Synced?  

✅ Captured Handshakes – `/root/handshakes/*.pcap`  
✅ Pwnagotchi Logs – `/var/log/pwnagotchi.log`  
✅ Configuration Backups – `/etc/pwnagotchi/config.toml` (optional)  

📌 To add more files to sync, modify the plugin script inside:  
`pwnagotchi/plugins/default/gdrivesync.py`  

---

🚀 Useful Tips & Tricks  

🔥 Force a Manual Sync  
If you want to upload files immediately, run:  

	pwnagotchi plugins run gdrivesync  

🔥 Use a Different Drive Folder  
To upload files to a specific folder in Google Drive, find your folder ID and update `config.toml`:  

	[main.plugins.gdrivesync]
	folder_id = "YOUR_NEW_FOLDER_ID"  

🔥 Check Sync Logs  
To see if syncing is working:  

	tail -f /var/log/pwnagotchi.log | grep gdrivesync  

🔥 Upload Only Handshakes (No Logs)  
Modify your config to exclude log files:  

	[main.plugins.gdrivesync]
	upload_logs = false  

---

🛠️ Debugging & Logs  
Check if GDriveSync is running:  

	ps aux | grep gdrivesync  

If files aren’t uploading, restart the plugin:  

	sudo systemctl restart pwnagotchi  

If authentication fails, re-run the authorization:  

	pwnagotchi plugins run gdrivesync --auth  

---

🔥 Final Thoughts  
The GDriveSync plugin ensures that your captured WPA handshakes are securely backed up in the cloud. With automatic uploads, manual sync options, and full Google Drive API support, this plugin is essential for keeping your data safe.  

