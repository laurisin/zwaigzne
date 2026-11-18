# ZWAIGZNE 6.0 — Design sources and implementation rationale

This release is a practical design pass, not a claim that a single external product or guideline dictates every control. The sources below informed the interaction and signal-engine decisions.

## Touch and tablet interaction

1. **Apple Human Interface Guidelines — Accessibility / Touch targets**  
   https://developer.apple.com/design/human-interface-guidelines/accessibility/  
   Informed the larger primary action surfaces, clear control labels, and keeping standard slider interactions familiar while adding exact-value editing as a secondary method.

2. **MDN — PointerEvent.pressure**  
   https://developer.mozilla.org/en-US/docs/Web/API/PointerEvent/pressure  
   Pointer pressure is a normalized value, but a browser/device may provide a constant fallback when actual pressure is unavailable. This is why the gesture surface only switches to pressure control after observing a varying signal; it does not assume that every finger touchscreen is force-sensitive.

3. **Android Developers — Advanced stylus features**  
   https://developer.android.com/develop/ui/views/touch-and-input/stylus-input/advanced-stylus-features  
   Informed the pen-pressure path and the explicit distinction between stylus capability and generic finger touch. Physical pressure availability remains device- and browser-dependent.

## Signal routing, feedback and dynamics

4. **W3C — Web Audio API 1.1**  
   https://www.w3.org/TR/webaudio/  
   Informed the explicit node-graph design, separate send/return paths, AudioParam modulation routing, and use of a DynamicsCompressorNode with measurable gain reduction.

5. **MDN — AudioParam**  
   https://developer.mozilla.org/en-US/docs/Web/API/AudioParam  
   Informed the modulation matrix: LFO source nodes are routed to actual AudioParams, and the tank destination fans out to all four delay-time parameters.

6. **MDN — DynamicsCompressorNode constructor and controls**  
   https://developer.mozilla.org/en-US/docs/Web/API/DynamicsCompressorNode/DynamicsCompressorNode  
   Informed the final GLUE stage and its threshold, knee, ratio, attack and release choices. The compressor is used for modest dynamics control, not as a claim of analogue emulation.

## Partial and harmonic design

7. **Cambridge University Press — Structuring Spectra in Electroacoustic Music**  
   https://www.cambridge.org/core/journals/organised-sound/article/structuring-spectra-in-electroacoustic-music/D466FF966D96AC1D04B02717964C7707  
   Informed the inclusion of fractional and inharmonic partial ratios instead of limiting the shimmer bank to octave/fifth relationships.

8. **Csound FLOSS Manual — Additive Synthesis**  
   https://www.csound-tutorial.net/floss_manual/Release06/Cs_FM_06.pdf  
   Informed the four independently selectable partial frequencies and amplitudes, plus slow frequency modulation to keep the spectrum moving.

## Mapping from research to 6.0 changes

| Change | Source basis | Implementation |
|---|---|---|
| Larger, clearer touch actions | Apple HIG | Increased primary button and selector target heights; retained native-like range behavior and exact entry |
| Pressure-aware gesture field | MDN PointerEvent + Android stylus guidance | Detect actual varying pressure; pen pressure path; contact-area proxy only when exposed; no fake pressure when unsupported |
| Editable Oracle routes | Web Audio API + AudioParam | Four LFOs each connect to a chosen AudioParam destination; tank route fans out to four delay times |
| Stronger, legible LOOP TRIM | Web Audio graph principles | One explicit multiplier applied to every regenerative path, with separate local controls for send, wet level, delay length and local regeneration |
| Four selectable weird partials | Cambridge spectral-structure research + Csound additive synthesis | Four dual-oscillator voices with independently selectable ratios and levels; dedicated slow pitch LFO |
| Optional final GLUE stage | W3C / MDN DynamicsCompressorNode | Soft-knee compressor, bypassable in the final output graph, with live reduction readout |
| Optional AFTERROOM | Web Audio delay/gain/filter graph model | Four cross-fed, filtered, panned delay lines; feedback hard-capped and governed by LOOP TRIM |

The implementation deliberately avoids expensive convolution or per-partial banks with dozens of oscillators. The Afterroom is a bounded delay-field experiment, not a high-CPU convolution reverb. The partial system uses four dual-oscillator voices to keep its CPU cost predictable.
