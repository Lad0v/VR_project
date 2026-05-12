# VR Blockchain Simulator

This repository is prepared as a standalone project for a hackathon task: an interactive VR/WebXR simulation that explains blockchain architecture.

## Project Goal
Build an educational 3D/VR experience that demonstrates:
- centralized vs decentralized architecture;
- blockchain block structure;
- public/private key mechanics;
- consensus algorithms (PoW and PoS).

## Functional Scenes
- Scene 1: Architecture comparison (Bank City vs Blockchain City).
- Scene 2: Block structure and chain invalidation after transaction tampering.
- Scene 3: Cryptographic keys (Access Denied vs Transaction Approved).
- Scene 4: Consensus arena (PoW vs PoS behavior differences).

## Current Technology Base
- Three.js + WebXR-compatible stack.
- Node.js and npm scripts from current project setup.

## Quick Start
1. Install dependencies:
   npm install
2. Run local development server:
   npm run dev

## Internationalization (i18n)
The project supports English (EN) and Russian (RU) languages.

- **Language Toggle**: Use the "Language" button in the UI to switch between EN and RU in real-time.
- **Persistent Language**: Your language preference is saved in localStorage and persists across sessions.
- **Auto-Detection**: The app automatically detects your browser language on first visit (fallback to EN).
- **Fallback**: If a translation is missing, it falls back to English.

Translation files are located in `locales/en.json` and `locales/ru.json`.

## Repository Notes
- This project was detached from the previous upstream repository metadata.
- Source folders are kept intact to avoid breaking functionality.
- Detailed modernization roadmap is in MODERNIZATION_PLAN_TZ.md.
