# MyPhone

**The world's first voice-orchestrated agentic smartphone.**

MyPhone is a security-first mobile computing platform built from the ground up on a formally verified microkernel. It is designed to resist advanced persistent threats while remaining genuinely usable as a daily driver.

<img width="1024" height="1024" alt="MyPhone" src="https://github.com/user-attachments/assets/94af0190-ab6d-4d56-bf38-d8abbd813f31" />

---

## Why MyPhone Exists

Every other smartphone is built on tens of millions of lines of code that cannot be audited, formally verified, or meaningfully secured. MyPhone starts over.

```
< 100,000 lines of trusted code.
A formally verified microkernel.
From zero to practical invulnerability.
```

The seL4 microkernel at the core of MyPhone carries a mathematical proof of memory isolation and access control. Security-critical services run in isolated compartments that a compromised application layer cannot reach.

---

## At a Glance

```
🚫 No SIM Required       |   🔐 Formally Verified Microkernel
🌐 Global Compatibility  |   🧠 Voice Orchestrator
📵 Offline-First         |   ₿  Quantum-Resilient Bitcoin Custody
🛠️ Repairable Design     |   📞 Encrypted Wi-Fi Calling & Messaging
🆓 No Telemetry          |   🛡️ State-of-the-Art Threat Resistance
```

---

## Security Architecture

MyPhone treats the application layer as permanently compromised. Wallet keys, biometric templates, and cryptographic operations live in hardware-isolated compartments that no app, no exploited driver, and no compromised OS can reach.

| Layer                       | Component                                | Security property                                                                         |
|-----------------------------|------------------------------------------|-------------------------------------------------------------------------------------------|
| **Hardware root of trust**  | Qualcomm SPU + Infineon OPTIGA TPM EAL4+ | Keys never leave secure silicon. Dual-chip redundancy. Post-quantum firmware update path. |
| **Microkernel**             | seL4 (~10K lines)                        | Mathematical proof of memory isolation and access control. AArch64 proof completed 2024.  |
| **Hypervisor isolation**    | seL4 as Type-1 hypervisor                | Security compartments (wallet, biometrics, crypto) provably isolated from the Linux VM.   |
| **No baseband**             | No integrated modem in v1                | Entire baseband attack surface eliminated. All voice over SIP/Matrix on Wi-Fi.            |
| **3-Factor Authentication** | Face + fingerprint + image recognition   | All three factors verified inside the SPU. Nothing passes through the OS.                 |
| **KYC device binding**      | Socure Predictive DocV                   | Only the identity-verified purchaser can activate the physical device.                    |

---

## Voice Orchestration

Every function on MyPhone is accessible by voice. The voice orchestrator runs entirely on-device — no audio reaches any server, ever.

```
[ You      ] "Navigate to the nearest hardware store."
[ MyPhone  ] Opens offline maps → routes via GPS, no internet required.

[ You      ] "Send an encrypted message to Alex."
[ MyPhone  ] Routes via Matrix E2EE → green lock confirmed.

[ You      ] "Transfer funds to my hot wallet."
[ MyPhone  ] Vault mode → 3FA required → signs offline → broadcasts on confirmation.

[ You      ] "Invite Jordan to play."
[ MyPhone  ] Sends Netplay session link via Matrix E2EE → Jordan's device auto-connects.
```

---

## MyCryptoWallet

The only Bitcoin custody system built into a smartphone that treats the OS as an adversary.

MyCryptoWallet uses a Cold Vault / Hot Wallet architecture where your public key is never exposed on-chain while funds are at rest. 

### How it works

- 🔐 **Hash-Locked Vaults** — Funds rest behind hashed public keys. The raw public key is never on-chain until a spend is in motion.
- 🔁 **One-Time Sweep Keys** — Every spend moves to a fresh address. No address reuse, ever.
- ⏱️ **Minimal Exposure Window** — Public keys exist on-chain only while funds are already moving (~10 minutes).
- 🧬 **Post-Quantum Recovery** — ML-KEM-1024 + ML-DSA-87 recovery path via the OPTIGA TPM. Hash-based SPHINCS+-256f for long-term recovery keys.
- 📵 **Offline Signing** — Vault mode disables all radios. Transactions are prepared air-gapped and broadcast only when you choose.
- 🛡️ **Pegasus-Proof** — Transaction signing happens inside the Qualcomm SPU, isolated from the OS by seL4's mathematical proof. A fully compromised OS cannot authorise a spend.

### Social Recovery

Lost your device? Recovery uses Shamir's Secret Sharing (default 3-of-5). Shares are exported to trusted parties, each encrypted with their own ML-KEM-1024 public key. Recovery requires three shares plus a 90-day timelock — giving the legitimate owner a full window to detect and cancel any unauthorised recovery attempt.

---

## Offline-First Navigation

```
📶  Download maps over Wi-Fi before you go
📡  Navigate anywhere with GPS + preloaded vector tiles
🗺️  Full offline routing via Valhalla — no cell signal needed
🔄  Intelligent prefetch of regions around frequent destinations
```

OpenStreetMap vector tiles. No tracking. No location data sent to any server. Your maps, on your device, forever.

---

## Media Center

A unified offline library covering every media type in a single voice-searchable collection. No streaming required.

|    | Feature             | Description                                                                                                    |
|----|---------------------|----------------------------------------------------------------------------------------------------------------|
| 🎵 | **Audio Player**    | Music, podcasts, audiobooks. Gapless playback, smart playlists, background playback with lock-screen controls. |
| 🎬 | **Video Player**    | Hardware-decoded video. Subtitles, A-B repeat, picture-in-picture, chapter navigation.                         |
| 🖼️ | **Photo Gallery**   | Timeline view, RAW editing, EXIF strip on share, secure delete.                                                |
| 📄 | **Document Viewer** | PDF, EPUB, MOBI, Markdown, code files. Full-text search across your entire library.                            |

---

<!--
## Gaming

Three non-overlapping gaming modes. No third-party gaming accounts. No cloud gaming services.

| Mode               | How it works                                                                                                                         |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| **Solo Retro**     | On-device retro emulation from a built-in library. Landscape lock, controller overlay, performance mode.                             |
| **Phone-to-Phone** | P2P mesh via Wi-Fi Direct. Up to 8 players. AES-256-GCM encrypted. No internet required.                                             |
| **Cross-Device**   | RetroArch Netplay with a paired large-screen device. Controller input only — no video streaming. Session invitation via Matrix E2EE. |

<img width="1536" height="1024" alt="controller_layout" src="https://github.com/user-attachments/assets/8c21d736-5842-45ba-be43-a96ce426fcab" />
<img width="1536" height="1024" alt="controller_layout_2" src="https://github.com/user-attachments/assets/230d445e-59eb-4628-91b7-df7c12291588" />

---
-->
## Secure Browser

A hardened Firefox ESR fork following the GrapheneOS/Vanadium model.

|                  | Standard browser                   | MyPhone browser                                                   |
|------------------|------------------------------------|-------------------------------------------------------------------|
| **JIT engine**   | Enabled (JIT spray attack surface) | Disabled by default · allowlist-based                             |
| **WebGL**        | Enabled                            | Disabled by default                                               |
| **DNS**          | Plaintext                          | DNS-over-HTTPS + Encrypted Client Hello                           |
| **WebRTC**       | IP leak risk                       | IP leak prevention enforced                                       |
| **Tracking**     | Extensive                          | Certificate pinning · HTTPS-only · no autoplay · no link previews |
| **Breach scope** | Full OS access                     | Isolated in Linux VM · wallet and biometrics unreachable          |

---

## SIM-Free Telephony

MyPhone uses your Wi-Fi connection for all calls and messages. No carrier required.

- **Primary number** — A Telnyx mobile-classified number. Treated as wireless by carrier databases. E911 with dynamic GPS location. TLS + SRTP encrypted to the Telnyx backbone.
- **MyPhone-to-MyPhone** — Calls and messages route automatically via Matrix E2EE. Zero PSTN exposure. Free and unlimited.
- **Burner numbers** — Disposable Telnyx SIP numbers for temporary use, managed in a standalone app. Up to 3 active at once.

Every call displays a clear encryption indicator so you always know what protection is in effect.

---

## Tech Specs

```yaml
Processor:    Qualcomm QCS8550 (Snapdragon 8 Gen 2 silicon)
              No integrated modem — baseband attack surface eliminated

Security:     Qualcomm SPU (FIPS 140-2 validated)
              Infineon OPTIGA TPM SLB 9672 (EAL4+, post-quantum)

Memory:       12GB LPDDR5X RAM
Storage:      512GB UFS 4.0 · expandable via 2TB MicroSD (FDE required)

Display:      6.5" IPS FHD+ 120Hz · Gorilla Glass 5

Camera:       Front - 50MP Sony IMX766 · 3D structured-light face recognition
              Rear - 50MP Sony IMX586

Biometrics:   3D structured-light face + Qualcomm 3D Sonic Max ultrasonic fingerprint
              All processing in seL4-isolated compartments · templates in SPU

Battery:      4500mAh · 45W USB-C PD fast charge

Connectivity: Wi-Fi 6E (802.11ax 6GHz) · Bluetooth 5 · GPS
              True electrical radio disconnect via hardware switch

Accessories:  Wi-Fi Direct headphones · protective case
```

---

## MyCloud Subscription

MyPhone is fully functional with no account. The MyCloud subscription unlocks internet-dependent services at a single flat rate, covering all features across all your enrolled devices.

| Feature                                   | Without subscription | With MyCloud subscription |
|-------------------------------------------|----------------------|---------------------------|
| Local media, voice control, retro gaming  | ✅                   | ✅                        |
| Screen cast and local network features    | ✅ Local network     | ✅                        |
| Matrix E2EE video calling (1:1 and group) | —                    | ✅                        |
| MyCloud media sync (client-side E2EE)     | —                    | ✅                        |
| Cross-device Netplay via internet relay   | —                    | ✅                        |
| Encrypted settings and profile backup     | —                    | ✅                        |
| MyCloud App Store                         | —                    | ✅                        |
| OTA updates via MyCloud CDN               | Public repository    | MyCloud CDN               |

See [MyCloud](https://github.com/ccnfac/MyCloud) for more info.
<!--
# MyPhone
**The World’s First Voice Orchestrated Agentic Smartphone**

MyPhone is a mobile computing platform powered by open source Linux, designed for privacy, offline navigation, and peer-to-peer gaming.

<img width="1024" height="1024" alt="ChatGPT Image Jun 20, 2025, 05_24_59 PM" src="https://github.com/user-attachments/assets/94af0190-ab6d-4d56-bf38-d8abbd813f31" />

## Features


```
🚫 No SIM Required      |    🆓 Secure Wifi Calling & Messaging
🌐 Global Compatibility |    📦 Works Right Out of the Box
🛠️ Repairable design    |    🧠 Voice Orchestrator  
```

## Offline First Navigation

* 📶 Download maps over Wi-Fi before you need them
* 📡 Navigate anywhere with GPS + preloaded maps (no internet needed)

## Media Center

| Feature            | Description                          | ✅ |
| ------------------ | ------------------------------------ | -  |
| 🎵 Audio Player    | Music, podcasts, and voice playback  | ✅ |
| 🎬 Video Player    | Watch movies and clips offline       | ✅ |
| 🖼️ Photo Gallery   | Organize and view photos             | ✅ |
| 📄 Document Viewer | Open PDFs, text, and docs            | ✅ |

## Gaming Powerhouse

| Feature           | Description          | ✅ |
| ----------------- | -------------------- | -  |
| 🎯 P2P Gaming     | Wi-Fi / Direct       | ✅ |
| 🔄 Landscape Mode | Console like play    | ✅ |
| 👾 Retro Library  | Classics built-in    | ✅ |

## Secure Browser

| Feature    | Traditional      | MyPhone         |
| ---------- | ---------------- | --------------- |
| Banking    | 🔴 Multiple Apps | 🟢 All-in-One   |
| Privacy    | 🔴 Tracked       | 🟢 No Tracking  |
| Utilities  | 🔴 Multiple Apps | 🟢 Agentic      |

## MyCryptoWallet

MyCryptoWallet is a quantum resilient vault grade Bitcoin custody system built directly into MyPhone. It uses an offline first signing model, one time sweep keys, and post quantum recovery paths to minimize exposure to future quantum attacks. No address reuse. No exposed resting keys. No custodians.

### Key Principles

- 🔐 **Hash‑Locked Vaults** — Funds rest behind hashed public keys (no exposed pubkeys at rest)
- 🔁 **One‑Time Sweep Keys** — Every spend moves through an ephemeral address
- ⏱️ **Minimal Exposure Window** — Pubkeys exist on‑chain only while funds are already moving
- 🧬 **Post‑Quantum Recovery** — PQ signature path with timelock fallback
- 📵 **Offline Signing** — Vault mode disables radios, QR transfer only

## Tech Specs

```yaml
Processor:
  Qualcomm QCS8550 Snapdragon

Memory:
  RAM: 12GB
  Storage: 512GB
  Expandable: 2TB MicroSD

Display:
  6.5" FHD+ (2400x1080)
  IPS, 120Hz, Gorilla Glass 5

Camera:
  Front: 50MP Sony IMX766 Camera CMOS
  Rear:  50MP Sony IMX586 MIPI FPC Camera Module

Battery:
  4500mAh, 45W fast charge USB-C PD

Connectivity:
  WiFi 6, GPS, Single SIM
  3.5mm Jack, Stereo Speakers

Accesories:
  WiFi Direct Headphones, Protective Case
```
-->

