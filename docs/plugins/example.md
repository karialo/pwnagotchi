🔥 Example Plugin (v1.0.0) – Full Documentation 🔥  

📌 Overview  
The Example plugin is a template plugin included with Pwnagotchi to help users understand how to create their own plugins. It provides a basic structure for developers who want to extend Pwnagotchi’s functionality.  

✅ Demonstrates how to create a Pwnagotchi plugin  
✅ Includes placeholder functions for different events  
✅ Serves as a starting point for custom plugin development  

---

👤 Author & Version  
- Author: Pwnagotchi Core Team  
- Version: `1.0.0`  
- Location: `pwnagotchi/plugins/default/example.py`  

---

⚙️ How It Works  
The Example plugin doesn’t perform any real functionality—it simply logs events whenever Pwnagotchi does something.  

It includes empty functions that get triggered on key events, such as:  
✅ On boot – When Pwnagotchi starts  
✅ On handshake capture – When a WPA handshake is collected  
✅ On AI learning step – When Pwnagotchi updates its AI model  

This allows developers to modify the template to build their own custom features.  

---

🛠️ Installation & Setup  
This plugin is disabled by default, but you can enable it for testing.  

1️⃣ Enable the Plugin  
Edit your Pwnagotchi config file:  

	sudo nano /etc/pwnagotchi/config.toml  

Find (or add) the Example plugin section:  

	[main.plugins.example]
	enabled = true  

2️⃣ Restart Pwnagotchi to Apply Changes  

	sudo systemctl restart pwnagotchi  

---

📂 How to Use the Example Plugin  

🔥 Modify Event Functions:  
Inside `example.py`, you’ll see functions like:  

```python
def on_loaded(self):
    logging.info("Example Plugin Loaded!")
```

This function runs when the plugin is loaded. You can replace the `logging.info` line with your own code.  

🔥 Capture Handshake Events:  
Modify `on_handshake`:  

```python
def on_handshake(self, filename):
    logging.info(f"New handshake saved: {filename}")
```

Replace `logging.info` with custom notification or processing code.  

🔥 Trigger Actions When Pwnagotchi Learns:  
Modify `on_ai_step`:  

```python
def on_ai_step(self, agent, _):
    logging.info(f"Pwnagotchi updated its AI! Current reward: {agent.last_reward}")
```

---

🚀 Creating Your Own Plugin  

1️⃣ Copy the Example Plugin  
Make a new plugin file:  

	cp ../../pwnagotchi/plugins/default/example.py ../../pwnagotchi/plugins/user/myplugin.py  

2️⃣ Edit the New Plugin  
Modify `myplugin.py` with your custom code.  

3️⃣ Enable Your Plugin in config.toml  

	[main.plugins.myplugin]
	enabled = true  

4️⃣ Restart Pwnagotchi  

	sudo systemctl restart pwnagotchi  

---

🛠️ Debugging & Logs  
Check if the Example plugin is running:  

	tail -f /var/log/pwnagotchi.log | grep example  

Modify the logging lines to print debugging info for your own plugin.  

---

🔥 Final Thoughts  
The Example plugin is the perfect starting point for custom Pwnagotchi development. If you’re looking to add new functionality, this template gives you everything you need to get started!  

