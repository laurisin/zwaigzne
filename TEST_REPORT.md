# ZWAIGZNE 6.1 — Test report

## Automated checks

| Check | Result |
|---|---|
| Inline JavaScript syntax (`node --check`) | PASS |
| HTML element IDs | 220 unique; no duplicates |
| CSS parsing | 710 rules; no parse errors |
| Runtime top-navigation model | PASS: PLAY, FLOW, SEED, ORACLE, VEIL, GRIMOIRE, RELIQUARY, WITNESS |
| FLOW inspector targets | 55 target references; none missing from source DOM |
| FLOW range/select/toggle support | PASS by static inspection |
| PLAY gesture writes to FERMENT | Removed; gesture writes WIDTH and DRIFT only |
| ORACLE XY pointer routing | Verified statically; root and cutoff updated from the full-size surface |
| LOOP TRIM curve endpoints | -100 = 0; 0 = 1; +100 = 2.8 before stage caps |
| Drive headroom response | High FERMENT/FOLD and high live sampler stress lower the feedback scale |
| Recursive-path integration | Verified for tank cross-returns, diffuser loops, shimmer returns, sample modulation and Afterroom |
| Blend/sub/sample-gain updates | Recompute feedback headroom |
| `.zwg` schema | Remains v3; legacy import routes retained |

## Numeric spot checks

The feedback-drive factor was evaluated using a small Node harness against the implemented function:

- Baseline source/loading example: approximately `0.719`
- FERMENT 100 with FOLD selected: approximately `0.399`
- Live sampler at high gain/crush/entangle/sample CV: approximately `0.366`

These values are implementation outputs for the test conditions, not calibrated acoustic measurements.

## Not verified in this environment

Chromium headless startup timed out before a DOM dump could be produced. Therefore the following remain unverified here:

- Actual browser interaction and rendering
- Live Web Audio playback and sound quality
- Physical iPad/tablet and phone layout
- Physical touch and stylus behavior
- Gamepad hardware behavior
- Long-session CPU/battery performance

The build should be tested on the target devices before treating these behaviors as hardware-verified.
