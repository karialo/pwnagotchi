🔥 GPIO-Buttons Plugin (v1.0.0) – Full Documentation 🔥  

📌 Overview  
The GPIO-Buttons plugin allows you to use physical buttons connected to the Raspberry Pi’s GPIO (General Purpose Input/Output) pins to trigger various Pwnagotchi actions. This enables quick manual control without needing SSH or a touchscreen.  

✅ Assigns functions like shutdown, mode switching, screen refresh to physical buttons  
✅ Supports multiple buttons for different actions  
✅ Works with custom GPIO pin configurations  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.0.0`  
- Location: `pwnagotchi/plugins/default/gpio_buttons.py`  

---

⚙️ How It Works  
The GPIO-Buttons plugin listens for button presses on specific Raspberry Pi GPIO pins. When a button is pressed, Pwnagotchi performs the assigned action.  

By default, the plugin can:  
✅ Shutdown Pwnagotchi with a long press  
✅ Change modes (manual, AI, learning)  
✅ Refresh the screen  

📌 Example:  
If you connect a physical push button to GPIO pin 17, pressing it switches Pwnagotchi between AI and manual mode.  

---

🛠️ Installation & Setup  
This plugin is built-in, but you must enable it and configure the button mappings.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the GPIO-Buttons section:  

	[main.plugins.gpio-buttons]
	enabled = true
	buttons = [
	    { pin = 17, action = "mode" },  # Button on GPIO 17 switches modes
	    { pin = 27, action = "shutdown" },  # Button on GPIO 27 shuts down Pwnagotchi
	    { pin = 22, action = "refresh" }  # Button on GPIO 22 refreshes the screen
	]  

📌 Explanation of Config Options:  
- `enabled`: `true` to enable the GPIO button functionality  
- `buttons`: List of button configurations, specifying:  
  - `pin`: The GPIO pin number  
  - `action`: The function triggered by pressing the button  

Supported Actions:  
✅ `"mode"` → Switch between AI/manual mode  
✅ `"shutdown"` → Shut down Pwnagotchi safely  
✅ `"refresh"` → Refresh the e-ink display  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 Wiring & Hardware Setup  

🔥 Basic Wiring Example:  
1️⃣ Get a push button switch  
2️⃣ Connect one leg of the button to GPIO 17  
3️⃣ Connect the other leg to Ground (GND)  

📌 Example Wiring for a Single Button (Mode Switch):  
```
GPIO 17  --- Button --- GND
```

📌 Example Wiring for Multiple Buttons:  
```
GPIO 17  --- Button 1 --- GND  (Mode Switch)
GPIO 27  --- Button 2 --- GND  (Shutdown)
GPIO 22  --- Button 3 --- GND  (Screen Refresh)
```

You can check which GPIO pins are available using:  

	pinout  

---

🚀 Useful Tips & Tricks  

🔥 Use a Different GPIO Pin Layout  
If GPIO 17, 27, and 22 are in use, change the pin numbers in config.toml:  

	buttons = [
	    { pin = 5, action = "mode" },
	    { pin = 6, action = "shutdown" },
	    { pin = 13, action = "refresh" }
	]  

🔥 Debounce Button Presses  
If button presses trigger multiple actions at once, adjust the debounce timing in `gpio_buttons.py`.  

🔥 Enable Safe Shutdown Without SSH  
If you want a dedicated button for safe shutdown, connect one to GPIO 27 and add:  

	{ pin = 27, action = "shutdown" }  

🔥 Check Button Presses in Logs  
To verify button presses are being detected:  

	tail -f /var/log/pwnagotchi.log | grep gpio-buttons  

🔥 Manually Trigger an Action  
If a button isn’t working, you can test the action manually:  

	pwnagotchi plugins run gpio-buttons --action mode  

---

🛠️ Debugging & Logs  
Check if GPIO buttons are being detected:  

	dmesg | grep gpio  

To manually check button press events, run:  

	cat /sys/class/gpio/gpio17/value  

If the value changes from 0 to 1 when pressing the button, the wiring is correct.  

---

🔥 Final Thoughts  
The GPIO-Buttons plugin is perfect for quick physical control of Pwnagotchi, allowing you to switch modes, shut down safely, or refresh the screen with a simple button press. It’s easy to set up and a must-have for headless Pwnagotchis.  
