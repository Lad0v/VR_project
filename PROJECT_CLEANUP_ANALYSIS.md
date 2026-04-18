# Project Cleanup Analysis

Date: 2026-04-18

## Current Active Scenes
From examples/files.json:
- webxr_vr_blockchain_architecture
- webxr_vr_block_structure_integrity

## Requested Cleanup Action (Done)
- Removed examples/legacy_scenes from workspace.
- Git now tracks this as deletions of archived example HTML files.

## Why Unrelated Build Changes Appeared Before
Root cause:
- npm run dev previously executed utils/build/dev.js first.
- utils/build/dev.js removes and recreates build/ as tiny dev stubs.

Prevention applied:
- package.json script `dev` changed to server-only.
- old behavior preserved as separate script `dev-build`.

## Folder Role Map (Root)
- build/: built distributable bundles used by import map in scenes.
- devtools/: browser extension/devtools integration for three.js debugging.
- docs/: API docs site and generated docs data.
- editor/: three.js editor app.
- examples/: live example pages and assets (your active scenes are here).
- files/: shared site-level assets (icons, css, fonts) used by examples/index.html.
- manual/: manual pages and educational content assets.
- node_modules/: installed dependencies.
- src/: engine source code.
- test/: unit/e2e test suites.
- utils/: build server scripts and tooling.

## Direct Dependencies of Current Scenes
For active scene HTML files:
- ../build/three.module.js
- ./jsm/
- main.css

If launching via examples/index.html:
- files.json
- tags.json
- screenshots/<scene>.jpg
- ../files/main.css and icon assets from /files

## Safe/Unsafe Deletion Guidance (For Current Scene-Only Goal)

Do not delete:
- build/
- examples/jsm/
- examples/main.css
- examples/files.json
- examples/webxr_vr_blockchain_architecture.html
- examples/webxr_vr_block_structure_integrity.html
- utils/ (if using npm run dev)
- package.json

Can delete with minimal impact on your current scenes:
- devtools/
- docs/
- editor/
- manual/
- test/

Conditional delete:
- node_modules/ (safe to remove, but npm install required later)
- src/ (current scenes may still run, but project build/development capabilities degrade)

## Large Candidates Inside examples/ (from measured size)
- examples/models ~275.52 MB
- examples/textures ~99.29 MB
- examples/screenshots ~18.63 MB
- examples/sounds ~14.43 MB
- examples/jsm ~13.77 MB
- examples/fonts ~7.62 MB
- examples/luts ~4.86 MB

## Recommended Next Cleanup Mode
Use whitelist cleanup:
- Keep only active scene HTML + index + files.json + needed screenshots + jsm + main.css.
- Remove unused examples/screenshots first (easy and low risk).
- Remove heavy folders only after checking no runtime references from active scenes.

## Notes
- XRControllerModelFactory fetches controller profiles from CDN by default; local model assets are not strictly required for basic controller rendering in this setup.
- Keep this file as snapshot and continue cleanup in controlled commits.
