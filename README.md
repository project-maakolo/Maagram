# 🛡️ Maagram - Hardened Anti-Forensics Telegram Fork

[![License: GPLv3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://opensource.org/licenses/GPL-3.0)
[![Platform](https://img.shields.io/badge/Platform-Android-green.svg)]()
[![Status](https://img.shields.io/badge/Status-Active_Development-critical.svg)]()

Maagram is a highly hardened, privacy-focused, and serverless fork of the Telegram client (Android). It is built strictly for cybersecurity researchers, journalists, and users operating in heavily censored environments. 

The core philosophy of Maagram is **Zero-Infrastructure** and **Absolute Local Control**. It relies on zero proprietary backend servers, strips all telemetry, and utilizes local database manipulation to bypass server-side restrictions.

## 🚀 Core Features & Architecture

### 1. De-Google & Anti-Forensics Operations
* **Auto EXIF-Stripper:** Automatically scrubs all metadata (geolocation, device models, EXIF tags) from photos, videos, and documents locally before any packet is sent to the MTProto server.
* **Zero Telemetry & No GMS:** Completely disconnected from Google Mobile Services. Firebase Cloud Messaging (FCM) is replaced by an optimized background WebSocket implementation / UnifiedPush.
* **Independent Mapping:** Replaces Google Maps API with OpenStreetMap (OSM/osmdroid) for secure geolocation sharing.
* **Encrypted Storage:** Enforces hardware-accelerated SQLCipher for all local databases to prevent local extraction of cached messages.

### 2. Client-Side "Spy" Engine (Local Database Manipulation)
* **Smart Ghost Mode:** Blocks `messages.setTyping` and `messages.readHistory` packets. Includes a manual "Mark as Read" override to prevent MTProto API shadow-bans for anomalous read behavior.
* **Anti-Delete & Anti-Edit:** Intercepts `updateDeleteMessages` packets. Original messages are retained in the local database and marked with a 🗑️ tag instead of being removed from the UI.
* **Stealth Forwarding:** Bypasses "Forwarded from" tags by caching media locally and uploading it as fresh content.
* **Bypass Restrictions:** Ignores the server `no_forwards` flag and forces removal of Android's `FLAG_SECURE` to allow screen capturing and media saving in Restricted Channels and Secret Chats.
* **Hidden Vaults:** Specific chats can be completely purged from the UI thread and accessed only by injecting a cryptographic PIN into the global search bar.

### 3. Serverless Anti-Censorship (Zero Infrastructure)
* **Cloudflare Workers Distribution:** Uses edge-computing to generate dynamic, expiring 10-minute hash URLs (e.g., `maagram.club/get/hash`) that transparently 302-redirect to GitHub Releases. This prevents DPI/Censorship firewalls from blocking static download mirrors.
* **Automated Proxy Rotation:** Implements a background parser that silently fetches MTProto and V2Ray nodes from public GitHub repositories and unblocked Telegram web-channels.
* **Smart Latency Switching:** Automatically pings and shifts to the lowest-latency proxy node without user intervention.

## 🛠 Compilation & Reproducible Builds
*(Instructions for reproducible builds and JNI compilation will be published in upcoming commits).*

---
*Disclaimer: This project is a security research tool. The developers assume no responsibility for how this software is used.*
