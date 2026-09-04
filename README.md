<div align="center">

# 🚗 DriveNow
### Ride-Hailing Platform for Pakistan

A production ride-hailing app — live on Google Play — with real-time fare bidding, live driver tracking, and local payment integration (JazzCash).

[![Platform](https://img.shields.io/badge/Platform-Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#)
[![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)](#)
[![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)](#)
[![Status](https://img.shields.io/badge/Status-Live%20in%20Production-brightgreen?style=for-the-badge)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

</div>

---

> **📌 Note:** This is a portfolio showcase of DriveNow's architecture and my individual contributions. Live production code, secrets, and credentials are not included here. DriveNow is a live app serving real riders and drivers in Faisalabad, Pakistan.

<br>

## 📱 What It Does

DriveNow connects riders and drivers with an **inDriver-style bidding model** — riders propose a fare, nearby drivers accept or counter — plus:

| | |
|---|---|
| 🎯 | Real-time driver location tracking with live map updates |
| 📞 | In-app voice calling between rider and driver (WebRTC) |
| 💳 | Local payment methods — JazzCash MWallet, Easypaisa, in-app wallet |
| 🌆 | City-to-city rides and courier/freight requests |
| ✅ | Driver KYC verification workflow |
| 📊 | Admin dashboard for revenue and operations |

<div align="center">

**🟢 Live in Production on Google Play (Pakistan) · v1.5.15+26**

</div>

<br>

## 🛠 Tech Stack

<div align="center">

![Flutter](https://img.shields.io/badge/Flutter-02569B?style=flat-square&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=flat-square&logo=dart&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=flat-square&logo=firebase&logoColor=black)
![Google Maps](https://img.shields.io/badge/Google_Maps-4285F4?style=flat-square&logo=googlemaps&logoColor=white)
![WebRTC](https://img.shields.io/badge/WebRTC-333333?style=flat-square&logo=webrtc&logoColor=white)
![Riverpod](https://img.shields.io/badge/Riverpod-1B1B1B?style=flat-square&logo=riverpod&logoColor=white)

</div>

| Layer | Tech |
|---|---|
| 📱 Mobile app | Flutter, Riverpod, GoRouter |
| ☁️ Backend | Firebase Cloud Functions, Firestore |
| ⚡ Real-time | WebRTC (calling), Firestore listeners (live tracking) |
| 🗺️ Maps | Google Maps SDK, custom Haversine ETA (cost-optimized) |
| 💳 Payments | JazzCash MWallet v2.0 (server-side HMAC-SHA256 verification) |
| 🔐 Auth | Custom OTP service (SendPK), migrating to backend-issued JWT |
| 🔔 Push | Firebase Cloud Messaging |

<br>

## 🏗 Architecture Highlights

Real engineering problems solved in this project:

### 💳 1. Payment Reliability (JazzCash)
Diagnosed a silent failure where charge requests never reached the server — root-caused to an App Check stub that never activated, combined with a hard block on token readiness. Fixed by making the check advisory (matching the pattern already working in the OTP service) — restored payments in production with **zero downtime**.

### 🗺️ 2. Google Maps Cost Control
A polling loop (8–12s intervals) on live tracking spiked the Routes API bill to **$343 in 9 days**. Replaced with a local Haversine-based ETA calculation (no API call for most updates), throttled route recalculation, and capped the API tier — **cut projected monthly cost by ~90%**.

### 📍 3. Background Location Survival
Location tracking was silently dying when the app was swiped away on aggressive OEM battery managers (ColorOS, MIUI, Vivo). Solved with a native Android foreground service (`START_STICKY` + `AlarmManager` self-restart), OEM-specific autostart prompts, and a WorkManager watchdog as a fallback layer.

### 🔄 4. Firebase Exit Strategy *(in progress)*
Firebase is a single point of failure for a live-revenue app — a billing issue would halt all Cloud Functions. Currently executing a **phased migration**: self-hosted maps (OSRM/MapLibre) → Auth (Laravel Sanctum) → Storage (Cloudflare R2) → Database (PostgreSQL+PostGIS) → business logic — de-risking one layer at a time instead of a risky full rewrite.

<br>

## 📸 Screenshots

<div align="center">

| Rider Home | Bidding Screen | Live Tracking |
|:---:|:---:|:---:|
| <img src="screenshots/01-rider-home.jpg" width="250"/> | <img src="screenshots/02-bidding-screen.jpg" width="250"/> | <img src="screenshots/03-live-tracking.jpg" width="250"/> |

| Driver App | Chat & Call | Payment |
|:---:|:---:|:---:|
| <img src="screenshots/04-driver-app.jpg" width="250"/> | <img src="screenshots/05-chat-call.jpg" width="250"/> | <img src="screenshots/06-payment.jpg" width="250"/> |

| Admin Dashboard |
|:---:|
| <img src="screenshots/07-admin-dashboard.jpg" width="250"/> |

</div>

<br>

## 👤 My Role

**Founder & Lead Developer** — architected and built the app end-to-end (Flutter frontend, Firebase backend, payment integration, maps/tracking system), and currently leading the phased backend migration off Firebase.

<br>

## 📬 Contact

<div align="center">

**Tanosh Parvez**
Full-Stack Developer · Flutter · Firebase · React · Next.js

[![Email](https://img.shields.io/badge/Email-tanoshjutt%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:tanoshjutt@gmail.com)

</div>
