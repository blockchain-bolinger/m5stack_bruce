```markdown
# M5Stack Bruce - No-SD Version

## 📋 Overview
This version runs completely without an SD card. All payloads are stored in the flash memory.

## 🚀 Quick Start
1. **Install VS Code with PlatformIO**
2. **Open the project** in PlatformIO
3. **Connect the M5Stack** via USB
4. **Press Upload** (-> arrow in PlatformIO)

## 📁 Project Structure

## 🔒 Security (Phase 1)
- Web Control is protected via HTTP Basic Auth (`WEB_AUTH_USER` / `WEB_AUTH_PASSWORD`).
- Default user: `admin`, default password corresponds to `AP_PASSWORD` from `include/config.h`.
- Dangerous payloads are disabled by default (`ENABLE_DANGEROUS_PAYLOADS=0`).

### Optional: Intentionally enabling dangerous payloads
Set the build flag in `platformio.ini` to `-D ENABLE_DANGEROUS_PAYLOADS=1` (only in isolated test environments).

## ⚙️ Stability & Performance (Phase 2)
- Payload execution now reports success/error per command (no silent ignoring of unknown commands).
- Delays continue to service the UI/Webserver (`serviceTasksDuringDelay`), keeping the device responsive during longer payload steps.
- Web API delivers deterministic JSON responses for success/error (`status`, `code`, `message`).

## 🛡️ Profiles & Web Allowlist (Phase 3)
- Web execution now uses a fixed allowlist per payload (`payloadWebAllowed`).
- Default profile: Only non-critical Windows utility payloads are executable via web; BT/WiFi/dangerous payloads are blocked via web.
- Sensitive payloads (e.g., `Win: WiFi Passwords`) remain blocked via web by default.

### Build Flags for Profiles
- `-D ENABLE_DANGEROUS_PAYLOADS=0` (Default): dangerous payloads are not included in the build.
- `-D ENABLE_WEB_SENSITIVE_PAYLOADS=0` (Default): sensitive payloads remain blocked via web.
- For lab tests, `ENABLE_WEB_SENSITIVE_PAYLOADS=1` can be set (isolated environments only).
