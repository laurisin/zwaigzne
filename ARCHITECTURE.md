# ZWAIGZNE 6.1 — Signal and interaction notes

## Audio path model

The instrument has parallel source branches and regenerative effects; it is not a single straight serial chain.

```text
OSCILLATOR BANK ──> SOURCE / FILTER ──> FERMENT ──┬──> DRY / MAIN MIX ──┐
                                                  │                    │
                                                  └──> TANK INPUT       │
                                                       │                │
                         ┌─────────────────────────────┘                │
                         v                                              │
              4-LINE CROSS-FED TANK                                    │
              + 8 DIFFUSER LOOPS                                       │
                         │                                              │
              SHIMMER / PARTIAL RETURNS                                 │
                         │                                              │
              WET RETURN ───────────────────────────────────────────────┤
                                                                        v
RELIQUARY SAMPLE ──> SAMPLE GAIN ──> DRY / TANK SEND ───────────────> MAIN MIX
                                                                        │
                                                                        v
                                              AFTERROOM (optional; final repeats)
                                                                        │
                                                                        v
                                                CANOPY / SKIN / GLUE / MASTER
                                                                        │
                                                                        v
                                                               AUDIO OUTPUT
```

The diagram is conceptual: source, sample and modulation branches feed shared buses, and several effect returns are recursive. It deliberately distinguishes audio flow from modulation and regeneration.

## LOOP TRIM calculation

`effectiveLoopScale = feedbackBiasCurve(LOOP_TRIM) × feedbackDriveFactor()`

The bipolar trim curve provides a smooth but decisive negative region, nominal unity at zero, and a bounded positive region. The second factor estimates headroom pressure from nonlinear drive and source/effect loading. It scales only recursive paths, not the main dry mix.

The scale reaches the four tank cross-returns, eight all-pass diffuser feedback gains, shimmer regeneration, sample-driven feedback modulation and Afterroom feedback. Individual feedback coefficients are still clamped by their own safety limits.

`TAIL` is intentionally not multiplied into the feedback scale. TAIL controls delay-line length/decay character; LOOP TRIM controls regenerative gain. Keeping these distinct makes each control's job predictable.

## Control ownership

- PLAY gesture: WIDTH + DRIFT only.
- ORACLE XY: ROOT + FILTER CUTOFF.
- ORACLE modulation routes: four separate LFO source-to-destination assignments.
- FERMENT: dedicated drive amount and drive-character controls; not linked to gesture position.
- WITNESS: final Afterroom, final compressor and master output.
- FLOW: signal-stage inspector; it edits the same underlying controls as the detailed panels.
- Grimoire: recallable patch state; master output and LOOP TRIM remain global.

## Navigation

The top bar contains eight top-level targets. The former CHAMBERS tab is removed at runtime; SEED, ORACLE, VEIL, GRIMOIRE and RELIQUARY become top-level pages alongside PLAY, FLOW and WITNESS. Phone layouts keep one horizontally scrollable navigation strip rather than wrapping into additional rows.
