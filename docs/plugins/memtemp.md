🔥 MemTemp Plugin (v1.0.2) – Full Documentation 🔥  

📌 Overview  
The MemTemp plugin displays real-time memory usage and CPU temperature on your Pwnagotchi’s screen. This helps you monitor system performance, detect overheating, and prevent crashes caused by low memory.  

✅ Shows live RAM and CPU temperature  
✅ Helps prevent overheating and memory-related crashes  
✅ Ideal for monitoring Pi Zero’s limited resources  

⚠️ Better Alternative: 🔥 MemTemp-Plus 🔥  
Instead of using MemTemp, it’s recommended to install MemTemp-Plus, which provides more accurate readings and additional system metrics.  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.0.2`  
- Location: `pwnagotchi/plugins/default/memtemp.py`  

---

⚙️ How It Works  
The MemTemp plugin retrieves system memory and CPU temperature every few seconds and displays the stats on the Pwnagotchi screen.  

📌 Example Display on Pwnagotchi:  
```
🔥 CPU: 54°C  |  RAM: 72MB Free  
```
When the temperature gets too high, Pwnagotchi will show a warning to prevent overheating.  

📌 Temperature Thresholds:  
- Below 60°C → Normal operation ✅  
- 60-75°C → Moderate heat warning ⚠️  
- Above 75°C → Critical overheating alert 🚨  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it to start monitoring system performance.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the MemTemp section:  

	[main.plugins.memtemp]
	enabled = true
	update_interval = 10  # Update every 10 seconds  

📌 Explanation of Config Options:  
- `enabled`: `true` to display CPU/RAM stats  
- `update_interval`: How often (in seconds) MemTemp refreshes data  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 What It Monitors  
✅ CPU Temperature – Helps prevent overheating  
✅ RAM Usage – Ensures system stability  
✅ Swap Usage – If enabled, tracks swap memory  

🔥 Upgrade to MemTemp-Plus for More Metrics  
- Adds CPU load percentage 📊  
- Includes network traffic stats 🌐  
- More accurate temperature readings 🌡️  

Install MemTemp-Plus:  

	cd /etc/pwnagotchi/plugins
	git clone https://github.com/jayofelony/memtemp-plus.git
	cp memtemp-plus/memtemp-plus.py /usr/local/lib/python3.7/dist-packages/pwnagotchi/plugins/default/
	sudo systemctl restart pwnagotchi  

Then enable it in `config.toml`:  

	[main.plugins.memtemp-plus]
	enabled = true  

---

🚀 Useful Tips & Tricks  

🔥 Monitor CPU Usage Over SSH  
For real-time system monitoring, run:  

	watch -n 1 vcgencmd measure_temp && free -h  

🔥 Lower the Update Interval for Faster Readings  
If you want updates every 5 seconds instead of 10:  

	update_interval = 5  

🔥 Enable Logging for Debugging  
To track MemTemp stats over time, enable logging:  

	[main.plugins.memtemp]
	logging = true  

Check logs:  

	tail -f /var/log/pwnagotchi.log | grep memtemp  

🔥 Reduce Overheating by Lowering CPU Speed  
To prevent high temperatures, underclock the CPU:  

	sudo nano /boot/config.txt  

Add:  

	arm_freq=900  
	core_freq=250  
	gpu_freq=300  
	over_voltage=-2  

Reboot for changes to take effect.  

---

🛠️ Debugging & Logs  
If MemTemp isn’t displaying data, check logs:  

	tail -f /var/log/pwnagotchi.log | grep memtemp  

If the temperature isn’t updating, restart the plugin:  

	pwnagotchi plugins run memtemp  

To manually check CPU temp via SSH:  

	vcgencmd measure_temp  

---

🔥 Final Thoughts  
The MemTemp plugin is great for basic system monitoring, but MemTemp-Plus is strongly recommended for better performance tracking and additional metrics. If you're serious about keeping your Pwnagotchi running smoothly, make the switch today!  
