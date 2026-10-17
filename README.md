# DuoGrab 🔗
**Secure, ephemeral, real-time P2P file sharing built with AI.**

[![Website](https://img.shields.io/badge/Website-duograb.com-blue?style=for-the-badge)](https://duograb.com)
[![Methodology](https://img.shields.io/badge/Methodology-Vibe_Coding-purple?style=for-the-badge)]()
[![Status](https://img.shields.io/badge/Status-Live_Beta-success?style=for-the-badge)]()

> **Note:** This repository does not contain the source code of DuoGrab. It serves as a technical whitepaper and architectural documentation of the platform, built to demonstrate the capabilities of AI-Driven Product Management (Vibe Coding).

## 💡 The Philosophy: The Cloud Paradox
Why use cloud storage for temporary files? DuoGrab bypasses the "upload-then-download" paradigm. It connects point A to point B directly. No server storage, no database limits, zero-knowledge by design.[cite: 17]

## 🛠️ Core Technology Stack
The stack was architected for absolute minimum latency and maximum browser performance, entirely guided by LLM orchestration[cite: 17].

*   **Frontend (Zero-Dependencies):** Pure HTML5, Vanilla JavaScript, Vanilla CSS. No frameworks (React/Vue) to guarantee raw DOM manipulation speed[cite: 17].
    *   **P2P Engine:** Native WebRTC API (`RTCPeerConnection`, `RTCDataChannel`)[cite: 17].
    *   **File Handling:** HTML5 File API, `FileReader` API (ArrayBuffer chunking)[cite: 17].
*   **Backend (Signaling & Telemetry):** Node.js & `Socket.io` for room creation and SDP exchange[cite: 17]. PostgreSQL for strictly anonymized, GDPR-compliant analytical logs[cite: 17].

## 🔐 The Security Architecture

### Asymmetric Visual 2FA
DuoGrab doesn't use passwords. It relies on a deterministic, ephemeral handshake to prevent MITM attacks[cite: 17]:
1. The server selects 3 random emojis[cite: 17].
2. It sends exactly ONE target emoji to the Host (e.g., 🚀)[cite: 17].
3. It sends all THREE emojis as clickable buttons to the Guest[cite: 17].
4. The Host communicates the emoji; the Guest clicks it. A match authorizes the WebRTC handshake. A failure instantly collapses the room[cite: 17].

## 🕸️ Network Traversal & "The Watchdog"
Establishing P2P connections behind strict corporate NATs is notoriously difficult.
*   **STUN/TURN Integration:** Uses STUN to bypass standard NATs and detects CGNAT (IPv4/IPv6 compatibility)[cite: 17].
*   **The Watchdog Engine:** If the P2P tunnel fails to establish within 2000ms, a background diagnostic script runs to determine if the block is due to strict firewalls, providing transparent logs instead of failing silently[cite: 17].

## ⚡ Data Transfer Mechanics (RAM Protection)
Sending large files via WebRTC requires strict memory management.
*   **Chunking:** The `FileReader` slices files into exact 16KB chunks[cite: 17].
*   **Buffer Management:** The system monitors `dataChannel.bufferedAmount`. If it exceeds 1MB, it pauses the `FileReader` until the network buffer drains, preventing browser RAM crashes on gigabit connections[cite: 17].

## 🧠 The "Vibe Coding" Experiment
DuoGrab is an exercise in AI-Driven development. The entire architecture, from the signaling logic to the CSS variables for Dark Mode, was developed by orchestrating Large Language Models, focusing on robust logic rather than manual syntax typing[cite: 17].

---

**Try the live platform:** [duograb.com](https://duograb.com)

*We welcome discussions! Open an Issue if you want to talk about WebRTC traversal, AI-driven development, or suggest architectural improvements.*
