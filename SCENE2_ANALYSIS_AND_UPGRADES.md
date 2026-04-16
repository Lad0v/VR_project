# Scene 2 Analysis and Upgrade Proposal

Date: 2026-04-16
Scope: Analysis only. No implementation in this document.

## 1. Scene 2 Goal (From Technical Requirements)
Scene 2 must demonstrate blockchain block structure and chain integrity.

Mandatory educational behavior:
- Show block fields: Transaction, Hash, Previous Block Hash.
- Let user modify one transaction.
- Show that all next blocks become Invalid after tampering.
- Highlight chain break with a strong visual effect.

## 2. Core Learning Loop (Recommended)
1. User sees a valid chain (all blocks Valid).
2. User selects a target block and edits transaction data.
3. Hash for edited block changes immediately.
4. All downstream blocks turn Invalid due to prevHash mismatch.
5. User can recover chain by restoring transaction or reminting hashes in sequence.

## 3. Suggested Data Model for Scene Logic
Use a minimal state contract per block:
- index
- tx
- prevHash
- hash
- valid

Additional scene state:
- selectedBlockIndex
- editBuffer
- replaySnapshots[]
- mode: live or replay

## 4. Visual Upgrade Recommendations
- Replace flat cards with layered 3D blocks:
  - header plate (index + hash)
  - transaction chamber (editable content)
  - chain connector socket (prevHash link)
- Show hash links as glowing conduits between block sockets.
- Invalid state effects:
  - red crack overlay on block shell
  - connector flicker and noise pulse
  - subtle geometry distortion/glitch on broken segment
- Add before/after ghost projection for changed block to make cause and effect explicit.

## 5. VR Interaction Recommendations
- Laser select block core to open edit panel in world-space.
- Virtual keypad or token drag input for transaction value editing.
- Trigger action button: Apply Tamper.
- Haptic pulse when chain becomes Invalid.
- Replay slider in VR panel to scrub from valid state to broken state.

## 6. Advanced Interaction Options (Optional)
- Guided tutorial mode with 4 short steps and success checks.
- Challenge mode: break only one block and recover under time limit.
- Multi-tamper mode: user edits two different blocks and compares invalidation ranges.
- Inspector lens: point at block and see exact mismatch reason.

## 7. UX/Teaching Improvements
- Keep one clear color language across scene:
  - Valid = green
  - Invalid = red
- Show one-line causal status text at all times.
- Add side metrics panel:
  - total blocks
  - valid blocks
  - invalid blocks
  - first broken index

## 8. Technical Risks and Mitigation
Risk: User does not understand why later blocks are invalid.
Mitigation: Always show prevHash mismatch message on first broken edge.

Risk: VR interaction overload.
Mitigation: Keep one primary interaction path (select -> edit -> apply).

Risk: Performance drops with heavy effects.
Mitigation: Use cheap emissive/fresnel/glitch shaders and avoid expensive post stacks.

## 9. Acceptance Criteria for Scene 2
- User can edit one transaction in a chosen block.
- Edited block hash updates.
- Downstream invalidation is visible and deterministic.
- Valid/Invalid indicators are readable in desktop and VR.
- User can return to valid chain state.

## 10. Recommended Implementation Order (Next Step)
1. Build deterministic block/chain state model.
2. Add block visuals and connectors.
3. Add tamper UI and invalidation propagation.
4. Add replay timeline and recovery actions.
5. Add final FX polish and tutorial prompts.
