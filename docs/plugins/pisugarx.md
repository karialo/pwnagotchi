🔥 PiSugarX Plugin (v1.2) – Full Documentation 🔥  

📌 Overview  
The PiSugarX plugin enables seamless integration between Pwnagotchi and PiSugar battery management boards. These boards provide portable power solutions for Raspberry Pi, allowing you to monitor battery status, control power settings, and automate safe shutdowns.  

✅ Monitors battery percentage & voltage 🔋  
✅ Supports PiSugar2 & PiSugar3 power boards  
✅ Provides low-battery warnings & auto shutdown  
✅ Allows manual power control via Pwnagotchi  
✅ Integrates directly with PiSugar web interface  

If you're running Pwnagotchi on battery power, PiSugarX is a must-have plugin to avoid unexpected shutdowns and data loss.  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.2`  
- Location: `pwnagotchi/plugins/default/pisugarx.py`  

---

⚙️ How It Works  

The PiSugarX plugin communicates with the PiSugar hardware via I2C and HTTP APIs, allowing Pwnagotchi to:  

✅ Read battery level & voltage 📊  
✅ Detect charging state 🔌  
✅ Trigger safe shutdowns when battery is low 🚨  
✅ Manually power off/reboot the device  
✅ Control PiSugar settings via Pwnagotchi UI  

📌 Example Battery Monitoring Output:  

	🔋 Battery: 82% (Charging) | Voltage: 4.1V
	⚡ Power Source: USB | Estimated Uptime: 6h 30m


Pwnagotchi displays battery stats on the screen and logs power events for easy monitoring.  

---

🛠️ Installation & Setup  

This plugin is built-in, but you must enable it and configure it for your PiSugar model.  

1️⃣ Enable the Plugin  

Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  


Find (or add) the PiSugarX section:  

	[main.plugins.pisugarx]
	enabled = true
	model = "PiSugar3"  # Change to "PiSugar2" if needed  
	low_battery_shutdown = 10  # Auto shutdown when battery hits 10%  
	update_interval = 30  # Battery status updates every 30 seconds  


📌 Explanation of Config Options:  

- `enabled`: `true` to activate PiSugarX support  
- `model`: `"PiSugar3"` (default) or `"PiSugar2"`  
- `low_battery_shutdown`: Percentage at which Pwnagotchi shuts down to prevent damage  
- `update_interval`: How often (in seconds) the battery status updates  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 PiSugarX Features  

🔥 Monitor Battery Level & Voltage  
Once enabled, check battery status manually:  

	pwnagotchi plugins run pisugarx  

Or via logs:  

	tail -f /var/log/pwnagotchi.log | grep pisugarx  

🔥 Enable Auto Shutdown to Protect Battery  
To prevent deep discharge, set:  

	low_battery_shutdown = 15  

This will power down Pwnagotchi when the battery reaches 15%.  

🔥 Manually Power Off or Reboot  
Run these commands to control power:  

- Power off immediately:  
	`pwnagotchi plugins run pisugarx poweroff`  

- Reboot:  
	`pwnagotchi plugins run pisugarx reboot`  

🔥 Check Power Source (USB vs. Battery)  
To check if your Pwnagotchi is running on battery or USB, use:  

	pwnagotchi plugins run pisugarx status  

🔥 View PiSugar API Data in Browser  
If you’re using PiSugar3, visit:  

	http://pwnagotchi.local:8421  

This opens the PiSugar web interface, where you can:  
✅ View battery health 📊  
✅ Adjust power settings ⚡  
✅ Update PiSugar firmware 🔄  

---

🚀 Useful Tips & Tricks  

🔥 Reduce Power Consumption for Longer Battery Life  
If your Pwnagotchi dies too quickly, limit power usage:  

1️⃣ Lower CPU Speed:  

	sudo nano /boot/config.txt  

Add:  

	arm_freq=800  
	gpu_freq=300  
	over_voltage=-2  

2️⃣ Turn Off HDMI Output (Saves Power on Pi 3/4):  

	vcgencmd display_power 0  

🔥 Manually Charge PiSugar Battery  
To force-charge the battery via SSH:  

	curl -X POST http://pwnagotchi.local:8421/api/charge/start  

🔥 View Advanced Battery Stats  
For full battery details, run:  

	curl http://pwnagotchi.local:8421/api/status  

🔥 Enable Safe Mode for Power Saving  
If your battery is running low, enable safe mode:  

	pwnagotchi plugins run pisugarx safe_mode  

---

🛠️ Debugging & Logs  
If the plugin isn’t detecting PiSugar, check logs:  

	tail -f /var/log/pwnagotchi.log | grep pisugarx  

If power stats aren’t updating, restart the plugin:  

	pwnagotchi plugins run pisugarx  

To check if the I2C interface is detecting PiSugar:  

	sudo i2cdetect -y 1  

If no devices are found, enable I2C in Raspberry Pi settings:  

	sudo raspi-config  

Go to:  
Interfacing Options > I2C > Enable  

Then reboot:  

	sudo reboot  

---

🔥 Final Thoughts  
The PiSugarX plugin is essential for portable Pwnagotchi setups, providing battery monitoring, auto shutdowns, and power management. If you’re using PiSugar2 or PiSugar3, enabling this plugin prevents unexpected shutdowns and extends battery life.  
