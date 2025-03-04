🔥 UPS-Lite Plugin (v1.3.0) – Full Documentation 🔥  

📌 Overview  
The UPS-Lite plugin adds support for the UPS-Lite battery management board, which provides an uninterruptible power supply (UPS) for Raspberry Pi-based Pwnagotchi setups.  

✅ Monitors battery level & voltage 🔋  
✅ Provides real-time charging & discharging status 🔄  
✅ Triggers safe shutdowns when battery is critically low 🚨  
✅ Prevents unexpected power loss that could corrupt data  

This is essential for portable Pwnagotchi setups that need reliable power management to avoid losing handshakes or damaging SD cards.  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.3.0`  
- Location: `pwnagotchi/plugins/default/ups_lite.py`  

---

⚙️ How It Works  
The UPS-Lite plugin communicates with the UPS-Lite hardware via I2C, allowing Pwnagotchi to:  

✅ Read battery level & voltage 📊  
✅ Detect charging/discharging state 🔌  
✅ Trigger automatic shutdowns when the battery is low  
✅ Provide real-time battery info on the screen  

📌 Example Output:  

🔋 Battery: 78% (Charging) | Voltage: 3.95V
⚡ Power Source: Battery | Estimated Uptime: 5h 20m


Pwnagotchi displays battery status in real-time and logs power events.  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it and configure it.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the UPS-Lite section:  

	[main.plugins.ups-lite]
	enabled = true
	low_battery_shutdown = 10  # Shutdown when battery reaches 10%  
	update_interval = 30  # Battery status updates every 30 seconds  

📌 Explanation of Config Options:  
- `enabled`: `true` to activate UPS-Lite monitoring  
- `low_battery_shutdown`: Percentage at which Pwnagotchi safely shuts down  
- `update_interval`: How often (in seconds) battery data updates  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 UPS-Lite Features  

🔥 Monitor Battery Level & Voltage  
To check the current battery status:  

	pwnagotchi plugins run ups-lite  

🔥 Enable Auto Shutdown to Prevent Battery Drain  
To protect the battery, set:  

	low_battery_shutdown = 15  

This shuts down Pwnagotchi when the battery reaches 15%.  

🔥 Manually Power Off or Reboot  
Run these commands to control power manually:  

- Power off immediately:  
	`pwnagotchi plugins run ups-lite poweroff`  

- Reboot:  
	`pwnagotchi plugins run ups-lite reboot`  

🔥 Check Power Source (Battery vs. USB)  
To check if Pwnagotchi is running on battery or USB, use:  

	pwnagotchi plugins run ups-lite status  

🔥 View Advanced Battery Stats  
For full battery details, run:  

	cat /sys/class/power_supply/ups_lite/uevent  

---

🚀 Useful Tips & Tricks  

🔥 Reduce Power Consumption for Longer Battery Life  
If your Pwnagotchi battery drains too quickly, adjust power settings:  

1️⃣ Lower CPU Speed:  

	sudo nano /boot/config.txt  

Add these lines:  

	arm_freq=800  
	gpu_freq=300  
	over_voltage=-2  

2️⃣ Turn Off HDMI Output (Saves Power on Pi 3/4):  

	vcgencmd display_power 0  

🔥 View Current Power Consumption  
To check how much power Pwnagotchi is using:  

	cat /sys/class/power_supply/ups_lite/voltage_now  

🔥 Manually Charge UPS-Lite Battery  
If the battery isn’t charging properly, plug into USB and restart Pwnagotchi.  

---

🛠️ Debugging & Logs  
If UPS-Lite isn’t detecting the battery, check logs:  

	tail -f /var/log/pwnagotchi.log | grep ups-lite  

If power stats aren’t updating, restart the plugin:  

	pwnagotchi plugins run ups-lite  

To check if the I2C interface is detecting the UPS-Lite board:  

	sudo i2cdetect -y 1  

If no devices appear, enable I2C:  

	sudo raspi-config  

Go to:  
Interfacing Options > I2C > Enable  

Then reboot:  

	sudo reboot  

---

🔥 Final Thoughts  
The UPS-Lite plugin is crucial for protecting your Pwnagotchi from unexpected shutdowns. It ensures safe battery monitoring, auto shutdowns, and power tracking, making it a must-have for portable deployments.  

---

✅ Next plugin? Drop the name and I’ll document it! 🚀🔥
