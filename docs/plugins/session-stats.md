🔥 Session-Stats Plugin (v0.1.0) – Full Documentation 🔥  

📌 Overview  
The Session-Stats plugin tracks real-time Pwnagotchi performance data during each session, helping users analyze efficiency, performance trends, and captured data over time. It provides detailed statistics on handshakes, networks discovered, uptime, and more.  

✅ Tracks session performance (networks, handshakes, uptime)  
✅ Helps analyze long-term efficiency of Pwnagotchi  
✅ Provides insights on signal strength, AI mode effectiveness, and activity  
✅ Useful for optimizing Pwnagotchi's performance over time  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `0.1.0`  
- Location: `pwnagotchi/plugins/default/session-stats.py`  

---

⚙️ How It Works  
The Session-Stats plugin collects and stores detailed session data, allowing users to track:  

✅ Total session uptime ⏳  
✅ Number of networks discovered 📡  
✅ Number of handshakes captured 🤝  
✅ AI mode performance 🧠  
✅ Average signal strength of networks detected 📶  

📌 Example Output in Logs:  

📊 Session Stats:
- Uptime: 3h 45m
- Networks Discovered: 267
- Handshakes Captured: 14
- AI Mode Accuracy: 92%
- Avg Signal Strength: -52 dBm


Session data is logged at the end of each session and can be retrieved for analysis.  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it to start tracking session data.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the Session-Stats section:  

	[main.plugins.session-stats]
	enabled = true  
	save_interval = 10  # Save stats every 10 minutes  

📌 Explanation of Config Options:  
- `enabled`: `true` to activate session tracking  
- `save_interval`: How often (in minutes) stats are saved  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 What Stats Does It Track?  

🔥 Session Uptime ⏳  
- Measures how long Pwnagotchi has been active during each session  

🔥 Networks Discovered 📡  
- Tracks the total number of unique SSIDs detected  

🔥 Handshakes Captured 🤝  
- Records every successful handshake capture  

🔥 AI Mode Performance 🧠  
- Monitors how well AI learning mode is detecting networks  

🔥 Average Signal Strength 📶  
- Logs the signal strength of detected networks, useful for placement optimization  

---

🚀 Useful Tips & Tricks  

🔥 View Session Stats Anytime  
Run this command to check stats on demand:  

	pwnagotchi plugins run session-stats  

🔥 Log Stats to a File for Long-Term Tracking  
To keep a record of past session stats, edit your config:  

	[main.plugins.session-stats]
	save_to_file = "/root/session_logs.txt"  

View past session data:  

	cat /root/session_logs.txt  

🔥 Optimize AI Learning Based on Stats  
If AI isn’t performing well, adjust learning parameters based on captured data.  

🔥 Combine with Web Dashboard for Live Stats  
If using Pwnagotchi’s Web UI, session stats can be displayed in real-time.  

---

🛠️ Debugging & Logs  
If the plugin isn’t logging session data, check logs:  

	tail -f /var/log/pwnagotchi.log | grep session-stats  

If stats aren’t updating, restart the plugin:  

	pwnagotchi plugins run session-stats  

---

🔥 Final Thoughts  
The Session-Stats plugin is essential for tracking Pwnagotchi’s efficiency over time, helping users analyze performance trends and optimize AI learning. If you want long-term insights into network captures and handshake success, enabling this plugin is a no-brainer.  
