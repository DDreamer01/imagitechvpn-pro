<div align="center">
  <h1>🚀 IMAGITECH AUTOSCRIPT PRO</h1>
  <p><b>Enterprise-grade VPN &amp; SSH orchestration engine for modern VPS infrastructure.</b></p>
  <p>
    <img alt="Platform" src="https://img.shields.io/badge/platform-Ubuntu%20%7C%20Debian-blue?style=flat-square">
    <img alt="Shell" src="https://img.shields.io/badge/shell-bash%205.x-green?style=flat-square">
    <img alt="Python" src="https://img.shields.io/badge/python-3.10+-yellow?style=flat-square">
    <img alt="License" src="https://img.shields.io/badge/license-Proprietary-red?style=flat-square">
  </p>
</div>

---

Imagitech provisions a multi-protocol proxy environment with real-time session tracking, bandwidth enforcement, multi-login prevention, encrypted backups, a rich terminal dashboard, and full Telegram Bot integration, all from a single installation command.

Built and tested exclusively for **Ubuntu (20.04, 22.04, 24.04)** and **Debian (11, 12)** LTS releases.

---

## 📑 Table of Contents

- [Features](#-features)
- [Installation](#-installation)
- [Dashboard & Menus](#-dashboard--menus)
- [Reality SNI Domain](#reality-sni-domain)
- [CLI Reference](#-cli-reference)
- [Telegram Bot Controller](#-telegram-bot-controller)
- [Background Services](#-background-services)
- [System Architecture](#-system-architecture)
- [Backup & Disaster Recovery](#-backup--disaster-recovery)
- [Disclaimer](#-disclaimer)

---

## 🌟 Features

### 🔌 Multi-Protocol Tunneling

| Protocol | Ports | Description |
|----------|-------|-------------|
| **VLESS Reality (xHTTP)** | 443 | Xray-core with REALITY TLS camouflage and xHTTP transport |
| **VLESS Reality (Vision)** | 443 | Xray-core with XTLS Vision flow for zero-overhead encryption |
| **VLESS WS TLS** | 443 | WebSocket transport over TLS with custom path routing |
| **VMESS WS TLS** | 443 | VMess cipher suite over WebSocket + TLS |
| **Trojan WS TLS** | 443 | Trojan protocol via WebSocket + TLS |
| **XRAY Non-TLS** | 80, 8080 |  WebSocket + Non-TLS |
| **OpenSSH** | 22 | Standard SSH tunneling |
| **Dropbear** | 109, 143 | Lightweight SSH daemon for constrained networks |
| **HAProxy** | 80, 443, 8080, 8443, 8880 | High-performance TCP/HTTP load balancer and SNI router |
| **Async WebSocket Proxy** | 80, 443, 8880 | HTTP Injection and ISP bypass multiplexer |
| **UDP Custom** | 1-65535 | Direct UDP tunneling for gaming and VoIP traffic |
| **DNSTT (SlowDNS)** | 53, 5300 | DNS query encapsulation for deeply restricted networks |
| **Dante SOCKS5** | 1080 | Standalone high-speed SOCKS5 proxy |
| **Nginx Decoy** | 8081 | Decoy web server for camouflage |

### 🛡️ Security & Active Monitoring

- **Real-Time Session Monitor** — Python daemon (`daemon.py`) polls every 30 seconds to enforce max concurrent login limits per user. Violators are instantly locked and notified via Telegram.
- **Bandwidth Accounting** — Granular byte-level tracking via `/proc/io` and Xray's gRPC Stats API. Per-user GB limits enforced with automatic disconnection when quota is reached.
- **Ghost Process Reaper** — Automatically detects and purges Linux OS accounts for expired/locked users. Sends a single Telegram alert per ghost (no spam) and aggressively kills stale sessions.
- **Fail2Ban Integration** — Deploy Fail2Ban directly from the Settings menu to block brute-force SSH attacks.
- **AES-256-CBC Encrypted Backups** — Military-grade encryption with PBKDF2 key derivation for database, TLS certificates, and DNS keys.
- **TCP KeepAlives** — Kernel-level heartbeats prevent Cloudflare and Azure from silently dropping idle connections.
- **License Enforcement** — Centralized license verification via Cloudflare Worker API with automatic service suspension on expiry.

### 🤖 Telegram Bot Controller

- **Full Remote Management** — Create, renew, and delete users (SSH or XRAY) directly from Telegram inline buttons.
- **Account Type Selection** — Explicit SSH vs XRAY selection when adding users through the bot.
- **Free Trial System** — Provision time-limited trial accounts with one tap.
- **Domain & SNI Configuration** — Change host domain, NS domain, and REALITY SNI remotely.
- **Service Restarts** — Restart any managed service without SSH access.
- **Smart Alerts** — Receive Telegram notifications for login violations, expired user cleanup, and bandwidth limit breaches. Alerts are only sent when the Telegram service is actually active (no phantom alerts on unconfigured servers).

### 📊 Rich Terminal Dashboard

- **Live System HUD** — IP, ISP, OS, uptime, RAM/CPU usage, license status, and service health at a glance.
- **Service Health Grid** — Real-time `[ON]`/`[OFF]` status for all 9 managed services (WS-Proxy, HAProxy, Dropbear, Dante, UDP Custom, DNSTT, Xray, Monitor, Telegram).
- **Settings Menu with Live Indicators** — Auto Reboot schedule (`[ON 6H]`, `[ON 03:00]`, `[OFF]`), Fail2Ban status, Telegram Bot status, and active timezone all displayed inline.
- **Backup Menu with Live Indicators** — Telegram Auto-Backup, ImagiTech Cloud Backup, and Google Drive (Rclone) backup statuses shown at a glance.
- **Member List with Columns** — View all users in a formatted table with S/N, Username, Expiry Date, Status, Bandwidth (used/total), and Connection count.

---

## 📦 Installation

### IP Licensing

 - Visit <a href="https://t.me/imagivpnbot">@imagivpnbot</a><br>
 - Enter `/start`
 - Subscribe for 30 days at N3,000
 - Or Get 2-day free trial to test

<p align="center">
  <img src="https://github.com/user-attachments/assets/46134e95-18df-4073-93ee-154af2a60e08" alt="Dashboard & Menus" width="300">
</p>

Ensure you whitelist your IP before installing the script

### Deploy the platform on a fresh Ubuntu or Debian server as `root`:
```bash
sudo su -
```

```bash
apt update && apt upgrade -y
```

```bash
bash <(curl -sL https://vpn.imagitech.online/install.sh)
```

The installer will:
1. Install all system dependencies (HAProxy, Dropbear, Nginx, Dante, SQLite3, Python3, etc.)
2. Deploy and configure Xray-core with REALITY keys
3. Initialize the SQLite database with the full schema
4. Set up systemd services for all daemons
5. Configure firewall rules and TCP optimizations
6. Present the interactive dashboard


---

## 🖥️ Dashboard & Menus

Launch the dashboard at any time by typing `menu` as root.
<p align="center">
  <img src="https://github.com/user-attachments/assets/de8f1646-c8da-4314-9012-6b2f0082e332" alt="Dashboard & Menus" width="300">
</p>

### Menu Breakdown

| # | Menu | Description |
|---|------|-------------|
| 01 | **SSH Panel** | Create, renew, delete SSH accounts. View online users, member list, user credentials, and locked/banned users. |
| 02 | **Xray Panel** | Add users for any Xray protocol (VLESS Reality xHTTP/Vision, VLESS WS, VMESS WS, Trojan WS). View links, bandwidth, and online users. |
| 03 | **Domain & SSL** | Change host domain, NS domain, and REALITY SNI. Renew Let's Encrypt certificates. Generate new SlowDNS keys. |
| 04 | **Monitoring** | Real-time bandwidth usage, top users leaderboard, connection logs, failed login attempts, and system resource usage (htop). |
| 05 | **Service Manager** | Port map overview and one-click restart for all services or individual daemons. |
| 06 | **Backup & Restore** | Create encrypted local backups, restore from archive, send backups to Telegram, configure auto-backups (Telegram/Cloud/Google Drive). Live `[ON]`/`[OFF]` status indicators. |
| 07 | **Settings** | Auto reboot scheduling, SSH banner, Speedtest, Fail2Ban, Telegram bot, timezone. Live status indicators for all configurable services. |
| 08 | **Update Script** | Pull the latest core files from the cloud engine with automatic database schema migrations. |
| 09 | **Reboot Server** | Graceful server reboot with confirmation prompt. |

---

### Reality SNI Domain
<details>
  <summary>Click to expand!</summary>
  
  #### Global Defaults (Big Tech & CDNs)
  - `www.bing.com`
  - `www.apple.com`
  - `www.amazon.com`
  - `www.cloudflare.com`
  - `www.speedtest.net`
  - `www.microsoft.com`
  - `www.nvidia.com`
  - `www.samsung.com`
  - `www.intel.com`
  - `play.google.com`

  #### Regional Presets (Russia / CIS)
  - `storage.yandex.net`
  - `music.yandex.ru`
  - `www.ya.ru`
  - `www.kinopoisk.ru`
  - `www.ozon.ru`
  - `cdn7-02.cdn-vkvideo.com`

  #### Regional Presets (Europe / General)
  - `telegraph.co.uk`
  - `deepl.com`
  - `ikea.com`
  - `parisjetaime.com`
  - `vindobona.org`

  #### Regional Presets (Asia / Others)
  - `www.lovelive-anime.jp`
  - `pl02.launch.tel`
  - `iping.ggff.net`

</details>

If REALITY doesn't work, switch SNIs from **[03] Domain & SSL**

---

## ⌨️ CLI Reference

The `imagitech` command provides a headless API for scripting and automation:

```
imagitech <resource> <action> [args]
```

### User Management

```bash
# Create a user (SSH or XRAY)
imagitech user add <username> <password> <days> [max_logins] [bw_limit_gb] [SSH|XRAY]

# Create a trial account
imagitech user trial <username> <password> <hours> [max_logins] [bw_limit_gb] [SSH|XRAY]

# Renew a user's subscription
imagitech user renew <username> <days>

# Delete a user
imagitech user del <username>
```

### Service Management

```bash
# Restart a specific service or all services
imagitech service restart <service_name|all>
```

### Domain & SSL

```bash
imagitech config host <domain>       # Set primary host domain
imagitech config ns <domain>         # Set NS domain for SlowDNS
imagitech config sni <domain>        # Set REALITY SNI domain
imagitech cert renew [domain]        # Force Let's Encrypt renewal
imagitech cert status                # View certificate status
imagitech dnstt renew                # Generate new SlowDNS key pair
```

### System Administration

```bash
imagitech sys autoreboot <hours|HH:MM|0>   # Schedule auto-reboot (0 = disable)
imagitech sys banner                        # Edit SSH banner
imagitech sys backup                        # Create encrypted backup
imagitech sys backup_telegram               # Send backup to Telegram
imagitech sys autobackup <1|2|0>            # Configure auto-backup cron
imagitech sys rclone                        # Setup Google Drive backup
imagitech sys restore <file_path>           # Restore from backup archive
imagitech sys update                        # Update scripts from cloud
imagitech sys uninstall                     # Complete platform removal
imagitech sys fail2ban                      # Install and configure Fail2Ban
```

---

## 🤖 Telegram Bot Controller

The Telegram Bot Controller provides a complete remote management interface with inline buttons.

### Bot Menu Structure

<p align="center">
  <img src="https://github.com/user-attachments/assets/4075b119-05df-4c0b-8d2c-e2039bf52a5b" alt="Dashboard & Menus" width="300">
</p>

```
🏠 Main Menu
├── ➕ Add User → 🔑 Add SSH User / 🌐 Add XRAY User
├── 🎁 Trial
├── 🔄 Renew
├── ❌ Delete
├── ℹ️ User Info → SSH Info / Xray Links
├── 👥 Online Users
├── 🌐 Domain & SSL → Change Host / Change NS / Change SNI
├── 🔁 Restart Service
└── 📊 Server Status
```

### Setup

1. Open the **Settings** menu (`menu` → `[07]`)
2. Select **Configure Telegram Bot Controller**
3. Enter your Telegram Bot Token and Admin Chat ID
4. The controller starts as a systemd service (`imagitech-telegram`)

---

## ⚙️ Background Services

| Service | Systemd Unit | Description |
|---------|-------------|-------------|
| **Session Monitor** | `imagitech-monitor` | Python daemon enforcing login limits, bandwidth caps, and account expiry |
| **WebSocket Proxy** | `imagitech-ws` | Async WS multiplexer for HTTP injection and ISP bypass |
| **Telegram Controller** | `imagitech-telegram` | Telegram bot polling service for remote management |
| **DNSTT Server** | `imagitech-dnstt` | SlowDNS tunnel server |
| **UDP Custom** | `imagitech-udp-custom` | Direct UDP tunnel service |
| **HAProxy** | `haproxy` | TCP/HTTP load balancer and SNI router |
| **Xray Core** | `xray` | Multi-protocol proxy engine |
| **Dropbear** | `dropbear` | Lightweight SSH daemon |
| **Dante** | `danted` | SOCKS5 proxy server |

---

## 📂 System Architecture

All files are sandboxed under `/opt/imagitech/` to avoid polluting the global system namespace.

```
/opt/imagitech/
├── bin/
│   └── imagitech              # CLI API router (symlinked to /usr/local/sbin/)
├── core/
│   ├── database.db            # SQLite3 database (users, sessions, bandwidth)
│   ├── imagitech.conf         # Primary configuration file
│   ├── telegram.conf          # Telegram bot token and chat ID
│   ├── server_geo.env         # Cached IP geolocation data
│   ├── license.env            # Cached license status
│   ├── online_users.txt       # Live online user snapshot
│   └── keys/
│       ├── dnstt.key          # SlowDNS private key
│       ├── dnstt.pub          # SlowDNS public key
│       ├── reality.key        # REALITY private key
│       ├── reality.pub        # REALITY public key
│       └── reality.sid        # REALITY short ID
├── lib/
│   ├── users.sh               # User CRUD operations
│   ├── system.sh              # System administration functions
│   ├── services.sh            # Service management functions
│   ├── db.sh                  # Database initialization and migrations
│   └── installer_utils.sh     # Installation helper functions
├── menus/
│   ├── main_menu.sh           # Primary TUI dashboard
│   └── xray_menu.sh           # Xray protocol panel
├── services/
│   ├── monitor/
│   │   ├── daemon.py          # Real-time session monitor and bandwidth enforcer
│   │   └── telegram-controller.py  # Telegram bot controller
│   └── routing/
│       ├── ws-proxy.py        # Async WebSocket proxy
│       └── wss-injector.py    # WSS injection proxy
├── xray/
│   ├── xray                   # Xray-core binary
│   └── config.json            # Xray configuration with all inbounds/outbounds
└── backups/
    └── *.tar.gz.enc           # Encrypted backup archives
```

### Database Schema

The SQLite database (`database.db`) stores all user and session data:

| Column | Type | Description |
|--------|------|-------------|
| `username` | TEXT | Unique account identifier |
| `password` | TEXT | Account password |
| `uuid` | TEXT | Xray UUID for proxy protocols |
| `exp_date` | TEXT | Expiration date (YYYY-MM-DD) |
| `max_logins` | INTEGER | Max concurrent sessions allowed |
| `status` | TEXT | Account status (ACTIVE, LOCKED, EXPIRED) |
| `data_usage` | BIGINT | Cumulative bytes used |
| `data_limit` | BIGINT | Bandwidth cap in bytes (0 = unlimited) |
| `account_type` | TEXT | Account type (SSH or XRAY) |

---

## 💾 Backup & Disaster Recovery

### Backup Methods

| Method | Description | Setup |
|--------|-------------|-------|
| **Local Encrypted** | AES-256-CBC encrypted `.tar.gz.enc` saved to `/opt/imagitech/backups/` | Menu → Backup & Restore → [01] |
| **Telegram Bot** | Send unencrypted backup directly to your Telegram chat | Menu → Backup & Restore → [03] |
| **Telegram Auto-Backup** | Scheduled daily/weekly automated backup via cron | Menu → Backup & Restore → [04] |
| **ImagiTech Cloud** | Cloud-based backup with remote storage | Menu → Backup & Restore → [05] |
| **Google Drive (Rclone)** | Automated backup to Google Drive via rclone | Menu → Backup & Restore → [06] |

### Restore

Upload your backup to `/opt/imagitech/backups/` via SFTP, then:

```bash
imagitech sys restore /opt/imagitech/backups/your_backup.tar.gz.enc
```

Or use the interactive menu: **Backup & Restore → [02] Restore from Backup**.

### Extract backup on another machine

```bash
openssl enc -d -aes-256-cbc -pbkdf2 -in imagitech_backup_*.tar.gz.enc | tar xz
```

---

## ⚠️ Disclaimer

This software is intended for educational purposes, privacy enhancement, and legal network administration. Abuse of this service for spam, DDoS, or illegal operations is strictly prohibited. The developer takes no responsibility for misuse.

---

Do not forget to give it a star 🌟

To report bugs or offer suggestions, kindly reach out <a href="https://t.me/DR34_M3R">†hε drεαmεr</a> on Telegram

<div align="center">
  <p>
    <b>Subscribe</b> → <a href="https://t.me/imagivpnbot">@imagivpnbot</a><br>
    <b>Channel</b> → <a href="https://t.me/imagitech001">@imagitech001</a><br>
    <b>Developer</b> → <a href="https://t.me/DR34_M3R">†hε drεαmεr</a>
  </p>
</div>
