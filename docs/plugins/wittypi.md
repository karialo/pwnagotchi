🔥 WittyPi Plugin (v1.0.0) – Full Documentation 🔥  

📌 Overview  
The WittyPi plugin provides integration with the WittyPi power management board, allowing your Pwnagotchi to schedule automatic startups, safe shutdowns, and manage power efficiently. This is especially useful for battery-powered and solar-powered setups where power conservation is critical.  

✅ Schedules automatic boot-up and shutdown times ⏰  
✅ Safely powers off Pwnagotchi to prevent SD card corruption 🔋  
✅ Extends battery life by reducing unnecessary runtime  
✅ Works with WittyPi 2, WittyPi 3, and WittyPi Mini  

If you need scheduled power management for remote Pwnagotchi deployments, this plugin is a must-have.  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.0.0`  
- Location: `pwnagotchi/plugins/default/wittypi.py`  

---

⚙️ How It Works  
The WittyPi board connects via I2C and RTC (Real-Time Clock), allowing Pwnagotchi to:  

✅ Schedule periodic power ON/OFF cycles 🔄  
✅ Monitor voltage & temperature data 📊  
✅ Automatically shut down when battery is low 🚨  
✅ Wake up on a preset schedule  

📌 Example Use Case:  
- Pwnagotchi turns on every morning at 6 AM ☀️  
- It runs for 3 hours, capturing handshakes 🏴‍☠️  
- It automatically shuts down at 9 AM to conserve battery 🔋  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it and configure the schedule.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the WittyPi section:  

	[main.plugins.wittypi]
	enabled = true
	power_on_time = "06:00"  # Auto power-on at 6 AM  
	power_off_time = "09:00"  # Auto shutdown at 9 AM  
	low_battery_shutdown = 3.5  # Shutdown when battery voltage < 3.5V  

📌 Explanation of Config Options:  
- `enabled`: `true` to activate WittyPi integration  
- `power_on_time`: Time when Pwnagotchi will automatically start  
- `power_off_time`: Time when Pwnagotchi will shut down  
- `low_battery_shutdown`: Shutdown voltage threshold (prevents SD card corruption)  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 WittyPi Features  

🔥 Automatic Power Scheduling  
- Set specific boot & shutdown times to optimize battery life  
- Useful for automated, time-based Wi-Fi monitoring  

🔥 Low Battery Auto-Shutdown  
- Prevents damaging your SD card by shutting down at low voltage  
- Avoids unexpected power loss  

🔥 Temperature & Voltage Monitoring  
- WittyPi reports real-time voltage and temperature  
- Helps diagnose battery or overheating issues  

🔥 Manual Power Control via CLI  
To manually power off your Pwnagotchi:  

	pwnagotchi plugins run wittypi poweroff  

To check current voltage and status:  

	pwnagotchi plugins run wittypi status  

🔥 Wake-on-Voltage for Solar-Powered Pwnagotchis  
If running on solar power, you can wake Pwnagotchi when battery reaches a certain voltage:  

	wake_on_voltage = 3.8  # Power on when voltage reaches 3.8V  

---

🚀 Useful Tips & Tricks  

🔥 Change Boot & Shutdown Times Dynamically  
To update power schedules without editing `config.toml`:  

	pwnagotchi plugins run wittypi set_schedule "07:30" "11:00"  

🔥 Manually Restart Pwnagotchi  
To reboot manually instead of shutting down:  

	pwnagotchi plugins run wittypi reboot  

🔥 Use With a UPS for Continuous Power  
If you combine WittyPi with a UPS (like UPS-Lite), you get:  
✅ Scheduled auto-power management  
✅ Battery monitoring  
✅ Uninterrupted operation when switching power sources  

🔥 Enable Safe Shutdown for Better SD Card Longevity  
If your SD card keeps getting corrupted, enable:  

	safe_shutdown = true  

This prevents sudden power loss issues.  

🔥 Monitor Battery & Temperature in Logs  
Check logs for voltage and temperature readings:  

	tail -f /var/log/pwnagotchi.log | grep wittypi  

---

🛠️ Debugging & Logs  
If WittyPi isn’t controlling power correctly, check logs:  

	tail -f /var/log/pwnagotchi.log | grep wittypi  

If Pwnagotchi isn’t waking up at the scheduled time, check RTC settings:  

	sudo i2cdetect -y 1  

If WittyPi isn’t detected, try:  

	sudo systemctl restart wittypi  

---

🔥 Final Thoughts  
The WittyPi plugin is essential for power-conscious Pwnagotchi setups, allowing users to schedule automatic power management, extend battery life, and prevent SD card corruption. Whether you're running on battery, solar, or UPS, this plugin helps you manage power efficiently.  
