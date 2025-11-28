
# 📱 PhoneInfoga – OSINT Tool for Phone Number Reconnaissance

PhoneInfoga is one of the most advanced tools to scan international phone numbers using OSINT techniques.  
This guide documents a **full local installation on Kali Linux**, without Docker, and makes it run as a service on port `8080`.

---

## 🚀 Features
- Scan phone numbers using multiple sources
- Gather basic information (carrier, line type, region)
- Web interface served locally
- CLI commands for automation
- Easy integration with other OSINT tools

---

## 🔧 Prerequisites
Ensure the following are installed:

```bash
sudo apt update
sudo apt install golang-go nodejs npm
```

---

## 📥 Installation

### 1. Clone the repository
```bash
git clone https://github.com/sundowndev/phoneinfoga.git
cd phoneinfoga
```

### 2. Build the frontend
```bash
cd web/client
npm install --legacy-peer-deps
npm run build
```

### 3. Build the backend
```bash
cd ~/phoneinfoga
go build -o phoneinfoga
```

### 4. Install system-wide
```bash
sudo install ./phoneinfoga /usr/local/bin/phoneinfoga
```

---

## ⚙️ Usage

### Check version
```bash
phoneinfoga version
```

### Run a scan
```bash
phoneinfoga scan -n +14155552671
```

### Serve web interface
```bash
phoneinfoga serve -p 8080
```

Open in browser:
```
http://localhost:8080
```

---

## 🛡️ Run as a Service (systemd)

Create a service file:

```ini
# /etc/systemd/system/phoneinfoga.service
[Unit]
Description=PhoneInfoga Service
After=network.target

[Service]
ExecStart=/usr/local/bin/phoneinfoga serve -p 8080
Restart=always
User=kali
WorkingDirectory=/home/kali/phoneinfoga

[Install]
WantedBy=multi-user.target
```

Enable and start:
```bash
sudo systemctl enable phoneinfoga
sudo systemctl start phoneinfoga
```

Check status:
```bash
systemctl status phoneinfoga
```

Now PhoneInfoga runs automatically at boot on port `8080`.

---

## 🧪 Example Workflow
1. Start service or run manually:
   ```bash
   phoneinfoga serve -p 8080
   ```
2. Open browser → `http://localhost:8080`
3. Enter a phone number → get OSINT results.
4. Combine with other tools (GhostTrack, INSTA-OSINT, MedusaPhisher) for deeper analysis.

---

## 🌱 Philosophy – “Hack with Nature”
- **Organic growth**: Treat your OSINT stack like an ecosystem — each tool feeds the next.
- **Resilience**: Automate restarts and logging so it self-heals like nature.
- **Adaptability**: Modular scripts let you swap tools in/out easily.
- **Persistence**: Running as a service makes PhoneInfoga always available, like a living system.

---

## 📚 Resources
- [Official GitHub Repository](https://github.com/sundowndev/phoneinfoga)
- [Documentation](https://github.com/sundowndev/phoneinfoga/wiki)

---

## ✅ Summary
With this setup, PhoneInfoga is:
- Installed system-wide
- Serving a web UI on port `8080`
- Running automatically at boot
- Ready to integrate into your OSINT workflows

```
