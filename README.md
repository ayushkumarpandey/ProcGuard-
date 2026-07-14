# 🛡️ ProcGuard — Monitor Smart. Control Fast. Stay Secure.

> A powerful full-stack system administration tool for real-time monitoring, intelligent process management, and web-based control on Linux systems.

---

## 📌 About the Project

**ProcGuard** is a dual-interface system monitoring and process control utility built for Linux (Ubuntu/Lubuntu/Debian). It combines a **high-performance Bash CLI engine** with a **Flask-powered Web Dashboard** to give you complete visibility and control over your system's resources and running processes.

Whether you need real-time CPU/RAM tracking, automatic process termination, or downloadable performance reports — ProcGuard handles it all from a single tool.

---

## ✨ Features

### 🖥️ Real-Time Web Dashboard
- Live CPU, RAM, Disk, and Network (Upload/Download KB/s) metrics
- Interactive historical charts (last 20 data points)
- Toast notifications for new process detections and kill events
- Global alert banner when any resource exceeds configured thresholds

### ⚙️ Intelligent Process Control
- **Manual Kill** — Terminate any process by PID directly from the UI
- **Auto-Kill** — Automatically terminates processes exceeding a user-defined threshold
- **Auto-Optimization Mode** — Background engine that cleans up heavy idle processes to keep the system lean

### 📡 Global Process Watcher
- Fast-polling (0.5s) watcher that catches *every* new process as it starts
- Watchlist alerts for apps like Chrome, Firefox, VLC, VS Code, and Spotify
- Last 10 system events shown as live interactive toasts in the dashboard

### 🔐 Security & Protection
- **Critical Process Guard** — Protects systemd, init, sshd, Xorg, and other essential services from accidental termination
- **Privileged Escalation** — On `AccessDenied`, automatically attempts non-interactive `sudo -n kill`
- **XSS & Path Traversal Protection** — All outputs are HTML-escaped and download paths are strictly sanitized

### 📈 Reports & Logs
- Generates structured performance summaries with uptime, resource usage, and termination history
- Download current or archived reports as `.txt` files directly from the browser
- Live log viewer with level filters, automatic log rotation at 1MB, and archive browser

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3.12, Flask |
| System Interface | Bash 4+, psutil |
| Frontend | HTML5, CSS3, JavaScript |
| Automation | Cron, Shell scripting |
| Platform | Linux (Ubuntu / Lubuntu / Debian) |

---

## 🚀 Local Setup

### Prerequisites
- Linux (Ubuntu / Lubuntu / Debian)
- Python 3.8+
- Bash 4+

### Step-by-Step Installation

**1. Clone the repository:**
```bash
git clone https://github.com/ayushkumarpandey/ProcGuard-.git
cd ProcGuard-/ProcGuard/ProcGuard
```

**2. Set up the Python virtual environment:**
```bash
python3 -m venv venv
source venv/bin/activate
pip install flask psutil
```

**3. Set script permissions:**
```bash
chmod +x main.sh modules/*.sh
```

**4. Run the Web Dashboard:**
```bash
source venv/bin/activate
python3 app.py
```
Open in your browser: 👉 `http://localhost:5000`

**5. Or run CLI Mode:**
```bash
./main.sh
```

**6. Automated Mode (Cron) — auto-kill every 5 minutes:**
```bash
*/5 * * * * /path/to/ProcGuard/main.sh --automate
```

---

## 🗂️ Project Structure

```text
ProcGuard/
├── app.py                  # Flask Web Server, API Endpoints & Background Threads
├── main.sh                 # Bash CLI Entry Point & Interactive Menu
├── config.conf             # Central Configuration (Thresholds, Paths, Watchlists)
├── README.md               # Project Documentation
├── modules/
│   ├── monitor.sh          # Resource metrics collection (Bash)
│   ├── process_manager.sh  # Detection and termination logic (Bash)
│   ├── process_watcher.sh  # Real-time process detection loop (Bash)
│   ├── logger.sh           # Logging, rotation, and directory management (Bash)
│   └── report.sh           # Performance report generation (Bash)
├── templates/
│   └── index.html          # Responsive Web Dashboard (6-tab UI)
├── logs/                   # Active logs and archives
└── reports/                # Performance summaries and archives
```

---

## 🔌 API Reference

| Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `/api/stats` | System metrics, network speed, and threshold alerts |
| `GET` | `/api/processes` | List of top processes (supports `?all=true`) |
| `POST` | `/api/kill` | Kill a process by PID (Manual) |
| `POST` | `/api/autokill` | Kill all processes above a specific threshold |
| `POST` | `/api/optimize/toggle` | Enable/Disable the Auto-Optimization engine |
| `GET` | `/api/report/download` | Download the latest performance report as `.txt` |
| `GET` | `/api/report/archive/download/<file>` | Download a specific archived report |
| `GET` | `/api/logs` | Fetch log lines with optional level filtering |
| `GET` | `/api/critical` | Status of critical system processes |

---

## ⚙️ Configuration

Tune ProcGuard by editing the [`config.conf`](ProcGuard/ProcGuard/config.conf) file:

| Setting | Description |
|---|---|
| `CPU_THRESHOLD` | CPU % that triggers alerts and auto-kill (default: `80`) |
| `RAM_THRESHOLD` | RAM % that triggers alerts and auto-kill (default: `80`) |
| `AUTO_OPTIMIZE` | Set to `true` to enable background resource reclamation by default |
| `WATCHED_PROCESSES` | Comma-separated list of app names to monitor specifically (e.g. `chrome,vlc,code`) |
| `LOG_MAX_SIZE` | Maximum log file size in bytes before it is auto-archived (default: `5242880` = 5MB) |
| `IDLE_OPTIMIZE_CPU` | CPU % threshold for "heavy idle" process cleanup (default: `10.0`) |
| `IDLE_OPTIMIZE_RAM` | RAM % threshold for "heavy idle" process cleanup (default: `5.0`) |

---

## 🧪 Troubleshooting

| Problem | Fix |
|---|---|
| **Permission Denied on scripts** | Run `chmod +x main.sh modules/*.sh` |
| **Sudo Kill Fails** | Ensure your user is in the sudoers group or configure `sudo -n` for non-interactive use |
| **Port 5000 already in use** | Run `fuser -k 5000/tcp` to free the port |
| **Missing psutil / flask** | Always activate your virtual environment first: `source venv/bin/activate` |

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

## 📬 Contact

**Ayush Kumar Pandey**  
📧 Reach out via GitHub: [@ayushkumarpandey](https://github.com/ayushkumarpandey)

---

<div align="center">
  <strong>Made with ❤️ by Ayush Kumar Pandey</strong>
</div>
