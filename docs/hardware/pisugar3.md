🔥 **PiSugar3 Setup for Pwnagotchi – The Ultimate Guide** 🔥  
**By Batesy – Refined & Enhanced for Maximum Idiot-Proofing**  

---

## **📌 Overview**  
The **PiSugar3** is an advanced power management module designed for Raspberry Pi, offering:  
✅ **Soft power on/off controls**  
✅ **Battery monitoring & power profiles**  
✅ **Web-based UI for customization**  
✅ **Integration with Pwnagotchi via the `pisugarx` plugin**  

This guide walks you through **installation, setup, and troubleshooting**, making sure **you get everything working properly**.

---

## **🛠️ Step 1: Check I2C Communication**
The **PiSugar3 connects via pogo pins**, so first, **make sure they’re making proper contact.**  

### **1️⃣ Install I2C Tools**
Run this command to install `i2c-tools`:
```bash
sudo apt-get install i2c-tools
```

### **2️⃣ Check for PiSugar3 on I2C Bus**
Run:
```bash
i2cdetect -y 1
```

You should see **57 and 68** in the output.  

🔥 **If you don’t see them:**  
- Your pogo pins **might not be making good contact.**  
- **Tighten the screws** on the PiSugar3 unit to ensure the pogo pins are firmly pressing against the Pi.  
- If that doesn’t work, **add a small blob of solder** to the header pins on your Raspberry Pi for better electrical contact.  
- **Double-check alignment** – if the pins aren’t properly seated, the PiSugar3 won’t function correctly.  

---

## **📥 Step 2: Install the PiSugar Power Manager**
🔥 **DO NOT** copy-paste the command from the PiSugar website—it won’t work as expected!  
Instead, run **each command separately** with `sudo`.

### **1️⃣ Download the Installer**
```bash
sudo wget https://cdn.pisugar.com/release/pisugar-power-manager.sh
```

### **2️⃣ Run the Installer**
```bash
bash pisugar-power-manager.sh -c release
```

🔥 **What Happens Next?**  
- A menu pops up asking you to **select your PiSugar version** → Choose **PiSugar3**.  
- You’ll **set up a web UI login (user/password).**  
- The script will also **install a shutdown management component**.

---

## **⚙️ Step 3: Configure Power Management**
Once installed, you can **access the PiSugar3 web UI** to fine-tune power settings.

### **📍 Open the PiSugar3 Web UI**
- **Find your Pwnagotchi’s IP address** (check your router or run `ip a`).  
- **Go to:**  
  ```
  http://<YOUR_PWNAGOTCHI_IP>:8421
  ```
- **Login using the credentials you just created.**  
- You can now **configure button actions, auto-shutdown settings, and power behavior.**

---

## **🔌 Step 4: Enable the PiSugarX Plugin**
The **PiSugarX plugin is included** in the **Jayofelony 2.9.5.3 image**, but **you need to enable it**.

### **Option 1: Enable via Web UI**
1️⃣ Open the **Pwnagotchi web interface**.  
2️⃣ Go to **Plugins**.  
3️⃣ Find **PiSugarX** and enable it.  
4️⃣ Restart Pwnagotchi.

### **Option 2: Enable via Config File**
1️⃣ Edit the config file:
```bash
sudo nano /etc/pwnagotchi/config.toml
```
2️⃣ Add/modify this section:
```toml
[main.plugins.pisugarx]
enabled = true
```
3️⃣ Save and exit (`CTRL + X`, then `Y`).  
4️⃣ Restart Pwnagotchi:
```bash
sudo systemctl restart pwnagotchi
```

---

## **🎮 Customizing Button Actions**
🔥 You can configure **button presses** to trigger specific actions. Here’s a common setup:

| **Action**               | **Button Press** | **Command** |
|--------------------------|-----------------|-------------|
| Clean Shutdown          | Double Tap Left | Runs a **safe shutdown script** |
| Restart Pwnagotchi      | Long Press Left | `sudo systemctl restart pwnagotchi.service` |
| Safe Power-Off          | Hold Right Button | Shuts down safely |
| Power On               | Double Tap & Hold Right | Turns device back on |

Set these actions in the **PiSugar3 Web UI** under **Button Settings**.

---

## **🚨 Troubleshooting & Common Fixes**
💡 **If the PiSugar3 isn’t detected (`i2cdetect` shows nothing):**  
✅ **Check pogo pin alignment** – Ensure the PiSugar3 is seated correctly on the Raspberry Pi.  
✅ **Tighten the screws** – Loose connections can prevent proper contact.  
✅ **Add a bit of solder** to the header pins to improve connectivity.  
✅ **Reboot and try again** – Sometimes a simple restart solves detection issues.  

💡 **If the buttons don’t work as expected:**  
✅ Ensure the `pisugarx` plugin is **enabled and running**.  
✅ Try reconfiguring button actions in the **PiSugar3 Web UI**.  
✅ Run this command to check logs for errors:
```bash
journalctl -u pisugar.service --no-pager --no-hostname -n 50
```

💡 **If you want to use Bluetooth tethering:**  
✅ **Power on your PiSugar3 first before enabling tethering**, otherwise, it might not connect properly.

---

## **🔥 Final Thoughts**
This guide ensures your **PiSugar3 is correctly installed, configured, and fully operational** with Pwnagotchi.  

Shoutout to **Batesy** for sharing these insights! 🎉  

