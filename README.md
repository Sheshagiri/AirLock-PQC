# AirLock-PQC

AirLock-PQC is a browser-based demo of a **fully offline, post-quantum key exchange** for air-gapped systems. It uses **ML-KEM-768** from **NIST FIPS 203** for the handshake and moves the exchange data over **animated QR codes** shown on one screen and captured by another device's camera.

The goal is simple: let two devices that must never join a network still establish a **shared quantum-resistant secret** with **no Wi-Fi, no Bluetooth, no cable, and no server**.

## Why it exists

Air-gapped systems already use QR transport for small ECC payloads such as public keys, signatures, and transaction approvals. Post-quantum handshakes are larger, which makes classical one-shot QR transfer impractical. AirLock-PQC extends the existing camera-to-screen pattern to support larger **ML-KEM public keys and ciphertexts**, making PQC viable for:

- industrial control environments
- offline signing infrastructure
- hardware wallets
- high-assurance operational workflows

## What this repository contains today

This repository currently contains a **single-file HTML prototype**:

- `index.html` - complete browser demo UI, bundled cryptography, QR encoding/decoding logic, and exchange flow
- `README.md` - project overview, architecture, and usage
- `.github/copilot-instructions.md` - repository guidance for AI coding agents and GitHub Copilot

The demo is designed to run **entirely client-side**. There is no backend, no account system, and no intended network dependency during the exchange.

## How the exchange works

1. **Device A** generates an ML-KEM-768 keypair locally.
2. The public key is split into QR-friendly fragments and shown as an animated QR sequence.
3. **Device B** scans the sequence, reconstructs the payload, and encapsulates a shared secret.
4. Device B shows the resulting ciphertext as another animated QR sequence.
5. Device A scans the reply and decapsulates the same shared secret.
6. Both devices display a short fingerprint so the operator can verify the match.

## Core properties

- **Offline-first**: intended for environments where the device must never touch a network
- **Post-quantum**: built around ML-KEM rather than classical ECC key agreement
- **Human-operated transport**: screen-to-camera exchange with no cable pairing ceremony
- **Browser-based prototype**: low-friction way to validate UX and exchange timing
- **Client-side privacy**: the current demo is structured so exchange data stays in the browser session

## Technical framing

AirLock-PQC is based on two practical observations:

1. **Animated QR transport is already operationally proven** for air-gapped workflows.
2. **PQC payloads are larger**, so reliable transport needs fragmentation and recovery rather than a single QR frame.

The project direction is to pair:

- **ML-KEM / FIPS 203** for the cryptographic handshake
- **BC-UR-style animated QR transport** for camera-safe transfer
- **Fountain-coded fragmentation** for resilience across shaky scanning conditions

That combination enables transfer of roughly **1-1.5 KB class payloads** quickly enough to remain operationally practical for real air-gapped systems.

## Running the demo

Because the prototype is a static page, the simplest option is to open `index.html` in a modern browser.

For camera access and a more realistic test flow, serving the file through a local static server is usually better. Any minimal static host works as long as the page remains fully client-side.

## Design constraints

Contributions should preserve these assumptions unless the repository explicitly evolves beyond prototype stage:

- no server dependency for the handshake
- no hidden network fallback
- no cloud key material handling
- no replacement of PQC with classical-only exchange
- no transport assumptions beyond screen and camera unless explicitly documented

## Near-term roadmap

- separate bundled libraries from handwritten application code
- make the QR framing and fragmentation layers explicit in code
- document the transport format and state machine
- add repeatable browser-based validation for exchange success and timing
- harden the prototype for real device camera variability

## AI-ready repository guidance

This repository now includes `.github/copilot-instructions.md` so coding agents have project-specific guidance about:

- offline-first constraints
- current single-file architecture
- security expectations
- preferred scope for future refactors

If the codebase grows beyond the current prototype, those instructions should evolve alongside the architecture.
