<div align="center">
  <img src="https://github.com/renzullicarmine-ai/DuoGrab-Architecture/blob/main/assets/DuoGrab_Logo-Blue_v2.png" alt="DuoGrab Logo" width="350"/>

  # Architecture
  **Secure, ephemeral, real-time P2P file sharing built with AI.**

  [![Website](https://img.shields.io/badge/Live_Beta-duograb.com-0052FF?style=for-the-badge)](https://duograb.com)
  [![Methodology](https://img.shields.io/badge/Methodology-Vibe_Coding-8A2BE2?style=for-the-badge)]()
  [![Architecture](https://img.shields.io/badge/Architecture-Zero_Knowledge-success?style=for-the-badge)]()
</div>

---

> **Note:** This repository does not contain the source code of DuoGrab. It serves as a technical whitepaper and architectural documentation of the platform, built to demonstrate the capabilities of **AI-Driven Product Management (Vibe Coding)**.

## 📖 Table of Contents
- [The Philosophy: The Cloud Paradox](#-the-philosophy-the-cloud-paradox)
- [Core Technology Stack](#️-core-technology-stack)
- [The Security Architecture (Visual 2FA)](#-the-security-architecture)
- [Network Traversal & "The Watchdog"](#️-network-traversal--the-watchdog)
- [Data Transfer Mechanics (RAM Protection)](#-data-transfer-mechanics-ram-protection)

---

## 💡 The Philosophy: The Cloud Paradox
Why use permanent cloud storage for temporary files? 

Corporate IT departments waste budgets and expose sensitive data to breach risks by using third-party clouds as "transit areas" for ephemeral files. 

DuoGrab bypasses the *upload-then-download* paradigm. It connects point A to point B directly. **No server storage, no database limits, zero-knowledge by design.**

<div align="center">
  <img src="https://github.com/renzullicarmine-ai/DuoGrab-Architecture/blob/main/assets/DuoGrab_05_Transfer_alpha.png" alt="DuoGrab Dashboard" width="800" style="border-radius: 10px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);"/>
  <br>
  <em>Simultaneous bidirectional transfer at LAN speed.</em>
</div>

---

## 🛠️ Core Technology Stack
The stack was architected for absolute minimum latency and maximum browser performance, entirely guided by LLM orchestration.

| Layer | Technology | Rationale |
| :--- | :--- | :--- |
| **Frontend** | Vanilla JS, HTML5, CSS3 | Zero-Dependencies. No frameworks (React/Vue) to guarantee raw DOM manipulation speed. |
| **P2P Engine** | WebRTC API | Direct `RTCPeerConnection` and `RTCDataChannel` for E2EE data transfer. |
| **File Handling** | HTML5 File API | `FileReader` API (ArrayBuffer chunking) to manage gigabyte-scale files without crashing. |
| **Signaling** | Node.js + Socket.io | Ephemeral room creation and SDP (Session Description Protocol) exchange. |
| **Telemetry** | PostgreSQL | Strictly anonymized, GDPR-compliant analytical logs for network diagnostics. |

---

## 🔐 The Security Architecture

### Asymmetric Visual 2FA (No Passwords)
DuoGrab relies on a deterministic, ephemeral handshake to prevent Man-in-the-Middle (MITM) attacks, ensuring the person receiving the file is exactly who you expect.

<div align="center">
  <img src="https://github.com/renzullicarmine-ai/DuoGrab-Architecture/blob/main/assets/DuoGrab_03_Emoji-2FA_alpha.png" alt="Visual 2FA Emoji Handshake" width="800" style="border-radius: 10px;"/>
</div>

1. The server selects 3 random emojis.
2. It sends exactly **ONE target emoji** to the Host.
3. It sends **all THREE emojis** as clickable buttons to the Guest.
4. The Host communicates the correct emoji; the Guest clicks it. 
*A match authorizes the WebRTC handshake. A failure instantly collapses the room.*

---

## 🕸️ Network Traversal & "The Watchdog"
Establishing P2P connections behind strict corporate NATs is notoriously difficult. Instead of forcing unauthorized connections (Shadow IT), DuoGrab respects corporate topology.

*   **STUN/TURN Integration:** Uses public STUN to bypass standard NATs and detects CGNAT (IPv4/IPv6 compatibility).
*   **The Watchdog Engine:** If the P2P tunnel fails to establish within 2000ms, a background diagnostic script runs to determine if the block is due to strict firewalls (Symmetric NAT), providing transparent logs instead of failing silently.
*   **LAN-to-LAN Acceleration:** If both users are on the same office network, data routes locally at maximum Wi-Fi speed, never touching the internet.

---

## ⚡ Data Transfer Mechanics (RAM Protection)
Sending extremely large files via WebRTC requires strict memory management to prevent the browser from crashing.

*   **Chunking:** The `FileReader` slices files into exact `16KB` chunks.
*   **Buffer Management:** The system actively monitors `dataChannel.bufferedAmount`. If it exceeds 1MB, it pauses the `FileReader` until the network buffer drains.
*   **Garbage Collection:** Received files are held in RAM via `Blob`. A dedicated UI warns the user if RAM usage exceeds limits, allowing instant cleanup via `URL.revokeObjectURL()`.

---

https://github.com/user-attachments/assets/e0ca8f90-5533-4346-89ac-bdd140c2229a

<div align="center">
  <h3>Ready to test the Zero-Knowledge transfer?</h3>
  <a href="https://duograb.com"><img src="https://img.shields.io/badge/Open_DuoGrab.com-0052FF?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Open DuoGrab"/></a>
</div>
<div align="center">
  <a href="https://duograb.com"><img src="https://github.com/renzullicarmine-ai/DuoGrab-Architecture/blob/main/assets/DuoGrab_Favicon-Blue_v2.png" alt="DuoGrab Logo" width="70"/>
