🔥 Cache Plugin (v1.0.0) – Full Documentation 🔥  

📌 Overview  
The Cache plugin improves Pwnagotchi’s efficiency by caching frequently accessed data. This reduces redundant computations and improves performance during Wi-Fi scanning and handshake collection.  

✅ Speeds up repetitive tasks by storing temporary data  
✅ Reduces CPU usage by avoiding unnecessary recalculations  
✅ Improves responsiveness when accessing saved networks  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.0.0`  
- Location: `pwnagotchi/plugins/default/cache.py`  

---

⚙️ How It Works  
The Cache plugin creates an in-memory storage for frequently accessed data. Instead of scanning and processing the same networks over and over, Pwnagotchi stores previous scan results and reuses them for faster decision-making.  

By default, it:  
- Stores previously seen networks in memory  
- Speeds up handshake verification  
- Reduces unnecessary SSID lookups  

📌 Example:  
If Pwnagotchi encounters the same Wi-Fi network multiple times, it doesn’t waste time re-scanning it from scratch. Instead, it retrieves cached details instantly, making it more efficient.  

---

🛠️ Installation & Setup  
This plugin is enabled by default, but you can configure its behavior.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the Cache section:  

	[main.plugins.cache]
	enabled = true
	cache_size = 1000  # Max number of cached entries
	cache_timeout = 300  # Remove old entries after 300 seconds  

📌 Explanation of Config Options:  
- `enabled`: `true` to enable caching  
- `cache_size`: The maximum number of Wi-Fi networks that can be stored in cache  
- `cache_timeout`: The duration (in seconds) before old entries are removed  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 How Cached Data is Used  

✅ Handshake Storage: Caches network handshakes to avoid unnecessary reprocessing  
✅ SSID Lookups: Remembers previously seen SSIDs to avoid redundant scans  
✅ Deauthentication Targets: Keeps a list of clients already attacked, preventing repeated deauths  

📌 Example:  
If Pwnagotchi deauths a specific AP and client, it remembers that for a short time so it doesn’t re-attack the same client multiple times unnecessarily.  

---

🚀 Useful Tips & Tricks  

🔥 Increase Cache for High-Density Areas:  
If you’re operating Pwnagotchi in an area with many networks, increase the cache size:  

	cache_size = 5000  

🔥 Lower Timeout for Faster Data Refresh:  
If you move around frequently and want a more dynamic cache, reduce the timeout:  

	cache_timeout = 60  

🔥 Disable Cache for Debugging:  
If you suspect Pwnagotchi is not detecting new networks properly, disable caching to force fresh scans:  

	[main.plugins.cache]
	enabled = false  

---

🛠️ Debugging & Logs  
Check cache usage in the logs:  

	tail -f /var/log/pwnagotchi.log | grep cache  

To manually clear the cache:  

	pwnagotchi plugins run cache --clear  

If you notice outdated data being reused, restart Pwnagotchi:  

	sudo systemctl restart pwnagotchi  

---

🔥 Final Thoughts  
The Cache plugin is a small but powerful optimization that speeds up Wi-Fi scanning and reduces redundant work. It’s recommended to keep enabled, but you can fine-tune cache size and timeout for your specific needs.  

