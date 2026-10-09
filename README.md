# WaSanDo CALL

Japanese call-recovery voice agent prototype.

## First milestone
Browser microphone → Japanese transcript → receptionist response → structured call record. This stage deliberately does **not** require NTT CPaaS credentials.

## Run locally
```bash
npm install
npm run dev
```
Open the local Vite URL in Chrome and allow microphone access.

## Architecture
- `src/main.tsx`: local conversation prototype
- Telephony will be isolated behind an adapter in the next stage.
- Client/industry knowledge will be configuration, not hard-coded core logic.
- NTT CPaaS credentials will be environment secrets and never committed.

## Planned next stage
Replace rule-based demo responses with the voice-agent engine; persist recording/transcript/call outcome; add an NTT CPaaS adapter only when local behavior is acceptable.
