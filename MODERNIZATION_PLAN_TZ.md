# Modernization Plan by Technical Requirements

Date: 2026-04-16
Planning mode: detailed implementation roadmap for rebuilding this codebase into the hackathon project.

## 1. Target Product Definition
Create an interactive VR/3D simulation that clearly explains blockchain through 4 mandatory scenes:
- Scene 1: centralized vs decentralized architecture;
- Scene 2: block structure and chain integrity;
- Scene 3: cryptographic keys and access decisions;
- Scene 4: consensus mechanics (PoW and PoS).

Mandatory visual entities:
- Blockchain Node;
- Block with transaction internals;
- Network Connection;
- Digital City in two modes (centralized/decentralized);
- Crypto Vault;
- Consensus Arena.

Mandatory status indicators:
- Valid;
- Invalid.

## 2. Current Baseline and Cleanup Direction
Current baseline contains full upstream three.js-style repository structure.

Use strategy:
- Keep working engine/source folders to avoid breaking runtime.
- Build the new experience in dedicated project modules.
- Avoid editing core engine files unless strictly required.

Primary implementation path:
- app root entry in examples/ (fastest hackathon path),
or
- isolated app folder apps/vr-blockchain-demo/ (clean architecture path).

Recommended for this repository state:
- Start in examples/ to ship MVP faster.
- Move to isolated app folder only if time allows.

## 3. Architecture Blueprint

## 3.1 Runtime Modules
- app/bootstrap: renderer, camera, scene, controls, resize, XR entry.
- app/router: scene switching and transition state machine.
- systems/network: node graph, link status, failure simulation.
- systems/blockchain: block model, hash links, validity propagation.
- systems/keys: public/private key validation logic.
- systems/consensus: PoW and PoS simulation states.
- ui/hud: state labels, controls, Valid/Invalid indicators.
- fx/visual: data-flow lines, invalid-chain effect, arena effects.
- audio/engine: event-based SFX and narrator triggers.

## 3.2 Data Contracts
Define strict object contracts early:
- NodeState: id, online, role, load, stake.
- BlockState: index, tx, hash, prevHash, valid.
- KeyAction: actor, keyType, result, reason.
- ConsensusTick: mode, latency, energy, validatorId.

## 4. Detailed Implementation Backlog

## 4.1 Phase A - Project Skeleton (1 day)
Tasks:
- Create scene bootstrap and render loop.
- Add global event bus for cross-module state updates.
- Add minimal HUD shell and panel containers.
- Add shared color tokens for Valid/Invalid and scene accents.
Deliverable:
- Empty but navigable app with debug labels and scene switch buttons.

## 4.2 Phase B - Scene 1 Architecture Comparison (1 to 1.5 days)
Tasks:
- Build Bank City layout with one central server node.
- Build Blockchain City layout with many distributed nodes.
- Animate packet transfer along links.
- Implement interactive toggles:
  - disable central server -> system halt;
  - disable one blockchain node -> system remains active.
Deliverable:
- Clear visual proof of single point of failure vs resilience.

## 4.3 Phase C - Scene 2 Block Structure (1 to 1.5 days)
Tasks:
- Render block chain line with block cards.
- Show transaction/hash/previous hash fields.
- Allow transaction edit in one block.
- Recompute validity down-chain and paint invalid blocks red.
- Add distortion/glitch effect to highlight broken chain.
Deliverable:
- User can break one transaction and instantly see cascade invalidation.

## 4.4 Phase D - Scene 3 Keys (1 day)
Tasks:
- Build Crypto Vault zone with key interaction console.
- Model public key as visible/open info.
- Model private key as owner-only credential.
- Implement outcomes:
  - wrong private key -> Access Denied;
  - correct private key -> Transaction Approved.
Deliverable:
- Interactive key workflow with explicit access decision visuals.

## 4.5 Phase E - Scene 4 Consensus (1.5 to 2 days)
Tasks:
- Build Consensus Arena and mode selector.
- PoW mode:
  - long validation timer;
  - high compute meter;
  - high energy meter.
- PoS mode:
  - validator chosen by stake;
  - shorter validation timer;
  - lower energy meter.
- Add side-by-side metric panel (latency, energy, throughput).
Deliverable:
- User can switch PoW/PoS and observe measurable behavioral differences.

## 4.6 Phase F - UX, Audio, Demo Polish (1.5 to 2 days)
Tasks:
- Add guided step-by-step tour for presentation flow.
- Integrate status color language (Valid/Invalid) across all scenes.
- Add SFX events: success, error, alert.
- Add optional voice-over clips for scene intros.
- Optimize camera paths and transitions.
Deliverable:
- Presentation-ready guided demo for judges.

## 4.7 Phase G - Stabilization and QA (1 to 1.5 days)
Tasks:
- Validate all interactive branches in scenes 1-4.
- Add automated logic tests where practical:
  - chain validity propagation;
  - key access conditions;
  - PoW/PoS metric switching.
- FPS checks and draw-call cleanup.
- Final regression pass for desktop + VR entry.
Deliverable:
- Stable build with known-risk list and fallback mode.

## 5. Time Estimate Summary
- MVP implementation: 7 to 9 working days.
- Polished hackathon version: 10 to 14 working days.
- Risk buffer (devices/performance/assets): +2 to 3 days.

Recommended planning envelope:
- 12 to 16 working days total.

## 6. Scope Reduction Plan (If Deadline Is Tight)
Cut in this order:
1. Reduce model complexity (low-poly and primitives).
2. Keep one environment and switch labels/material states instead of separate worlds.
3. Simplify voice-over to text prompts + minimal SFX.
4. Keep only one strong visual effect per scene.

Do not cut:
- 4 mandatory scenes;
- Valid/Invalid state indicators;
- interactive failure/success logic from the requirements.

## 7. Acceptance Criteria Checklist
A release is considered ready when:
- Scene 1 demonstrates central failure and decentralized resilience.
- Scene 2 demonstrates block tampering and invalid chain propagation.
- Scene 3 demonstrates private key validation with deny/approve outcomes.
- Scene 4 demonstrates PoW vs PoS with observable metric differences.
- Mandatory 3D entities are visible and interactive where required.
- Valid/Invalid indicators are consistent and always readable.
- Demo script can be completed end-to-end without manual code intervention.

## 8. Execution Order for Next Work Session
1. Create app skeleton and routing.
2. Implement Scene 2 first (highest educational impact).
3. Implement Scene 1.
4. Implement Scene 3.
5. Implement Scene 4.
6. Add UI/audio polish.
7. Run stabilization pass and freeze demo build.
