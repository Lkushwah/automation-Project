# HomieAuto Pro 🏠⚡

A commercial-grade, end-to-end IoT Smart Home ecosystem. This project features a fully autonomous ESP32 hardware hub and a real-time, multi-tenant cloud dashboard powered by Firebase.



## 🌟 Key Features

### Hardware (ESP32 C++ Firmware)
* **Zero-Lag Physical Sync:** Hardware switch state changes are instantly broadcasted to local and cloud interfaces.
* **Non-Blocking Emergency Mode:** Hardware operations (physical switches, offline schedules) function flawlessly even during Wi-Fi outages.
* **Offline Scheduling Engine:** Automations execute directly on the silicon via NTP time sync, completely independent of the cloud.
* **Secure Captive Provisioning:** Users input their Wi-Fi and Firebase credentials via a local setup portal (`HomieAuto-Setup`). No hardcoded secrets.
* **Embedded Local Dashboard:** A baked-in, password-protected local HTML web server accessible via `http://home-Auto.local` or raw IP, featuring Server-Sent Events (SSE) for real-time UI updates.
* **Voice Control Integration:** Native local Alexa support (emulating a Philips Hue bridge).

### Cloud & Frontend (Firebase & JavaScript)
* **Multi-Tenant Architecture:** Firebase Security Rules rigidly isolate individual user data environments.
* **Real-Time Analytics Matrix:** Live power draw (Watts) and uptime tracking visualized with Chart.js.
* **Global CI/CD Pipeline:** Automated GitHub Actions workflow deploys frontend updates directly to Firebase Hosting.
* **Glassmorphism UI:** Responsive, dark-mode Single Page Application built with Tailwind CSS.

---

## 🛠️ Tech Stack

* **Hardware:** ESP32, C++, AsyncWebServer, WiFiManager, ArduinoOTA
* **Frontend:** HTML5, Vanilla JavaScript, Tailwind CSS, Chart.js, FontAwesome
* **Backend:** Firebase Realtime Database, Firebase Authentication, Firebase Hosting
* **CI/CD:** GitHub Actions

---

## 🚀 Setup & Installation

### 1. Web Dashboard Deployment
1. Install the Firebase CLI: `npm install -g firebase-tools`
2. Initialize the project: `firebase init hosting`
3. Place the frontend code in the `/public` directory.
4. Deploy to the global CDN: `firebase deploy`

### 2. Hardware Provisioning
1. Flash the firmware to an ESP32 using the Arduino IDE.
2. Power on the ESP32 and connect your device to the `HomieAuto-Setup` Wi-Fi network.
3. Enter your home Wi-Fi credentials, your HomieAuto Web Dashboard Email, Password, and your unique Provisioning Key (UID).
4. Click Save. The ESP32 will reboot, lock the credentials into flash memory, and securely connect to your specific cloud node.

### 3. Factory Reset
To transfer ownership or clear network settings, press and hold the physical `BOOT` button (Pin 0) on the ESP32 for exactly 3 seconds. The device will wipe its non-volatile memory and re-enter provisioning mode.

---

## 🔒 Security Architecture
* **No Hardcoded Keys:** Firmware is generic and safe for mass distribution.
* **Database Lockdown:** Devices authenticate as end-users. Firebase actively rejects unauthorized database reads/writes at the edge.