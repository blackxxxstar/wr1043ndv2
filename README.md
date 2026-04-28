# 🚀 OpenWrt 19.07.10 Image Builder (TL-WR1043ND v2)

Automated GitHub Actions workflow to build **custom minimal OpenWrt firmware** for **TP-Link TL-WR1043ND v2** using ImageBuilder.

> ⚠️ Note: OpenWrt 19.07.10 is already **End-of-Life (EOL)** and no longer receives security updates ([OpenWrt][1])
> Use at your own risk or for legacy devices only.

---

## ✨ Features

* ⚙️ Fully automated build via GitHub Actions
* 📦 Uses OpenWrt ImageBuilder (fast, no full compile needed)
* 🧩 Minimal package set (optimized for low flash devices)
* 📡 Default configuration:

  * WAN: DHCP
  * Wi-Fi: Enabled (Open / no password)
* 🐍 Includes Python 2.7 compatibility (required by legacy ImageBuilder)

---

## 📦 Included Packages

Default build includes:

* `luci` – Web UI
* `dnsmasq` – DHCP & DNS
* `firewall`
* `wpad-basic` – Wi-Fi support

Removed (to save space):

* PPP (pppoe, pptp, etc)
* IPv6
* USB support

---

## 🧠 Why ImageBuilder?

OpenWrt ImageBuilder lets you create custom firmware **without compiling from source**, making it:

* ⚡ Faster
* 💡 Easier to customize packages
* 🧪 Ideal for CI/CD pipelines

> ImageBuilder works by combining precompiled packages into a flashable image ([OpenWrt][2])

---

## 🏗️ How It Works

Workflow steps:

1. Install build dependencies
2. Build Python 2.7 (required by old OpenWrt tools)
3. Download OpenWrt ImageBuilder (19.07.10)
4. Inject custom configuration (WAN + Wi-Fi)
5. Build firmware image
6. Upload artifact

---

## ▶️ How to Use

### 1. Run the Workflow

* Go to **Actions tab**
* Select: `Build OpenWrt 19.07.10 TL-WR1043ND v2 Minimal Router`
* Click **Run workflow**

---

### 2. Download Firmware

After build finishes:

* Open workflow run
* Download artifact:

  ```
  openwrt-19.07.10-tl-wr1043nd-v2
  ```

---

### 3. Flash to Router

#### Via Web UI (recommended)

1. Login to router (usually `192.168.0.1` or `192.168.1.1`)
2. Go to:

   ```
   System → Firmware Upgrade
   ```
3. Upload `.bin` file
4. Flash and wait reboot

---

## 📡 Default Configuration

After flashing:

| Setting    | Value                 |
| ---------- | --------------------- |
| WAN        | DHCP                  |
| Wi-Fi SSID | `TP-Link TL-WR1043ND` |
| Encryption | None (Open)           |

> ⚠️ Change Wi-Fi security immediately after first login!

---

## 🛠️ Customization

Edit this part in workflow:

```bash
PACKAGES="luci wpad-basic dnsmasq firewall ..."
```

Examples:

* Add VPN:

  ```
  wireguard luci-app-wireguard
  ```
* Remove LuCI:

  ```
  -luci
  ```

---

## 🐍 Python 2 Note

OpenWrt 19.07 ImageBuilder requires **Python 2**, which is no longer available by default.

This workflow:

* Builds Python 2.7.18 manually
* Links it as `python` and `python2`

---

## ⚠️ Disclaimer

* This firmware is for **legacy hardware**
* No security updates (EOL)
* Use behind firewall or for lab/testing

---

## 🙌 Credits

* OpenWrt Project
* GitHub Actions

---

## ⭐ Support

If this repo helps you:

* ⭐ Star the repo
* 🍴 Fork it
* 🧠 Improve it

---


[1]: https://openwrt.org/releases/19.07/notes-19.07.10 "[OpenWrt Wiki] OpenWrt 19.07.10 - Service Release - 20 April 2022"
[2]: https://openwrt.org/docs/guide-user/additional-software/imagebuilder "[OpenWrt Wiki] Using the Image Builder"
