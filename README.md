# 🔋 Battery Alert — Android App

A modern, feature-rich Android battery monitoring app built in Java with a sleek dark UI.

---

## ✨ Features

| Feature | Details |
|---|---|
| 🔴 Low Battery Alert | Fires when battery drops below your custom threshold (5–50%) |
| ✅ Full Charge Alert | Fires when battery reaches your target % while charging |
| 🔊 Custom Ringtone | Uses system alarm/notification ringtone for alerts |
| 📳 Vibration | Custom vibration patterns — distinct for low vs full alerts |
| 🔔 Notifications | High-priority alert notifications + persistent foreground notification |
| 📊 Battery Display | Real-time %, status, temperature, voltage |
| ▶️ Start/Stop | Toggle monitoring on/off with animated button |
| 🎨 Animated UI | Pulse rings, card entrance animations, button press effects |
| 🔧 Background Service | Foreground service survives app close + auto-restarts on boot |
| ⚡ Real-time Updates | Live battery status via BroadcastReceiver |

---

## 📁 Project Structure

```
BatteryAlert/
├── app/src/main/
│   ├── AndroidManifest.xml
│   ├── java/com/batteryalert/
│   │   ├── MainActivity.java          # Main UI + animations
│   │   ├── BatteryMonitorService.java # Background service (core logic)
│   │   └── BootReceiver.java          # Auto-restart on device boot
│   └── res/
│       ├── layout/activity_main.xml   # Modern dark UI layout
│       ├── drawable/                  # Custom shapes, battery icon, pulse rings
│       ├── values/
│       │   ├── colors.xml             # Dark theme palette
│       │   ├── strings.xml
│       │   └── themes.xml             # MaterialComponents dark theme
│       └── color/                     # Button color state lists
└── build.gradle
```

---

## 🚀 How to Build & Run

### Prerequisites
- Android Studio Hedgehog (2023.1.1) or newer
- Android SDK 34
- Java 8+

### Steps
1. Open Android Studio
2. **File → Open** → Select the `BatteryAlert/` folder
3. Wait for Gradle sync to complete
4. Connect an Android device (API 26+) or launch an emulator
5. Click **Run ▶** (or `Shift+F10`)

### Permissions Required
| Permission | Purpose |
|---|---|
| `POST_NOTIFICATIONS` | Show battery alerts (Android 13+) |
| `FOREGROUND_SERVICE` | Run background monitoring service |
| `VIBRATE` | Vibration on alerts |
| `RECEIVE_BOOT_COMPLETED` | Auto-restart after device reboot |
| `WAKE_LOCK` | Keep service alive |

---

## 🎨 UI Design

- **Dark theme** with deep navy `#0D0F14` background
- **Neon green** `#00E676` for healthy battery / active state
- **Amber** `#FFB300` for medium battery
- **Red** `#FF3D00` for low battery
- **Cards** with subtle borders and 8dp elevation
- **Pulse ring animation** while monitoring is active
- **Staggered entrance animations** on cards

---

## ⚙️ How It Works

1. **MainActivity** handles UI, preferences, and broadcasts the service start/stop
2. **BatteryMonitorService** is a foreground service that:
   - Registers a `BroadcastReceiver` for `ACTION_BATTERY_CHANGED`
   - Checks levels against thresholds on every battery event
   - Fires alerts (notification + vibration + sound) only once per event cycle
   - Sends local broadcasts back to the activity for live UI updates
3. **BootReceiver** restores the service on device boot if it was previously running

---

## 🛠 Customization

| Setting | Range | Default |
|---|---|---|
| Low battery threshold | 5–50% | 20% |
| Full charge threshold | 50–100% | 90% |
| Vibration | On/Off | On |
| Low battery alert | On/Off | On |
| Full charge alert | On/Off | On |

All settings are persisted via `SharedPreferences` and survive app restarts.

---

## 📱 Tested On
- Android 8.0 (API 26) — minSdk
- Android 13 (API 33)
- Android 14 (API 34)
