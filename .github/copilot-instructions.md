# Copilot instructions for AirLock-PQC

## Project purpose

AirLock-PQC is an offline-first prototype for **post-quantum key exchange over animated QR codes**. The current experience is a browser demo where two devices use their screens and cameras to complete an **ML-KEM-768** handshake without any network connection.

## Current repository shape

- `index.html` contains the complete demo: UI, exchange flow, bundled crypto, and QR logic.
- `README.md` is the main human-readable source of truth for project framing and constraints.
- There is currently **no backend** and **no build pipeline** in this repository.

## Non-negotiable constraints

- Keep the handshake **fully offline**.
- Do not introduce network-dependent fallbacks for the exchange path.
- Do not move key material handling to a remote service.
- Preserve the post-quantum design goal; do not replace ML-KEM with classical-only agreement.
- Favor changes that keep the demo understandable and inspectable in the browser.

## Preferred engineering direction

- If code grows, split `index.html` into logical modules without changing behavior.
- Keep cryptographic and transport logic clearly separated from UI code.
- Prefer explicit state machines and documented payload formats over implicit UI-driven state.
- Treat camera-link reliability as a first-class requirement when touching QR transport behavior.

## Documentation expectations

When changing behavior, update `README.md` if the change affects:

- the handshake flow
- transport assumptions
- security/privacy guarantees
- setup or execution guidance

## Validation focus

When making changes, prioritize:

- preserving client-side execution
- avoiding accidental network access
- keeping the initiator/responder flow understandable
- maintaining consistent shared-secret verification behavior
