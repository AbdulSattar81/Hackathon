# Architecture — Interpreter

## Diagram description (for the Devpost diagram + the slide)

Draw it as a left-to-right flow with two feedback stores underneath. Spoken description for narration follows.

```
                          ┌──────────────────────────────────────────────┐
                          │              DigitalOcean (host)               │
                          │   App Platform: web client + realtime relay    │
                          └──────────────────────────────────────────────┘
                                            │  (low-latency WebSocket)
   ┌──────────┐   English audio   ┌─────────────────┐   text   ┌──────────────────┐
   │  DOCTOR  │ ───────────────▶  │  Speech-to-Text  │ ───────▶ │  Translate +      │
   │ (bedside)│                   │  (Web Speech /   │          │  Emotion analysis │
   └──────────┘                   │   Whisper)       │          └──────────────────┘
                                  └─────────────────┘                   │
                                                                        │ text + tone params
        ┌───────────────────────────────────────────────────┐         ▼
        │  MongoDB Atlas                                      │   ┌──────────────────┐
        │  • patient visit history   • allergies             │──▶│   ElevenLabs TTS  │
        │  • preferred language      • medication glossary    │   │  emotive, multi-  │
        └───────────────────────────────────────────────────┘   │  lingual voice    │
                         ▲ context pulled per consult            └──────────────────┘
                         │                                                │ native-language audio
                         │                                                ▼
                         │                                          ┌──────────┐
                         │                                          │ PATIENT  │
                         │                                          │  hears    │
                         │                                          └──────────┘
        ┌───────────────────────────────────────────────────┐
        │  Snowflake (analytics)                              │ ◀── de-identified consult metadata
        │  language × wait-time × readmission correlations    │     (lang, latency, outcome flag —
        │  → dashboards: which gaps drive readmissions        │      NO PHI)
        └───────────────────────────────────────────────────┘
```

## Component roles
1. **Capture (Speech-to-Text).** The clinician speaks English at the bedside. Audio is transcribed in real time (Web Speech API in the demo; Whisper or a streaming STT service in production).
2. **Understand (Translate + Emotion).** The transcript is translated to the patient's language. In parallel, an emotion/urgency pass classifies the utterance (calm / reassuring / urgent / critical) and emits prosody parameters. This is the core insight: tone is extracted and passed downstream, not discarded.
3. **Context (MongoDB Atlas).** Before speaking, the system enriches the message with the patient's record — preferred language, allergies, current meds — and applies a medication-term glossary so drug names are explained, not transliterated.
4. **Voice (ElevenLabs).** The translated text plus tone parameters render to emotive speech in the patient's language. The patient hears urgency or reassurance, not a monotone.
5. **Delivery (DigitalOcean).** The web client and a realtime relay run on DigitalOcean; the relay keeps round-trip latency low so the translated voice lands before the moment passes.
6. **Learn (Snowflake).** Each consult emits de-identified metadata — language, wait/latency, and outcome flags — to Snowflake. Queries correlate language gaps with readmissions, producing a dashboard that tells the hospital where to staff interpreters.

## Data-flow / privacy notes
- **No PHI to analytics.** Snowflake receives only de-identified metadata (language code, timing, coarse outcome flag). Names, MRNs, and transcripts stay in Atlas under access control.
- **Local audio in the demo.** The browser demo never sends audio off-device; recognition and playback are local.
- **Human fallback.** For high-stakes consent, a qualified human interpreter remains the fallback — Interpreter shortens the gap, it doesn't replace the legal interpreter role.

## Demo vs. production (be honest with judges)
| Stage | Demo today | Production target |
|---|---|---|
| TTS | Browser SpeechSynthesis | ElevenLabs emotive voices |
| STT | Web Speech API | Streaming Whisper |
| Data | In-page mock record | Live Atlas cluster + vector search |
| Analytics | Static mock chart | Live Snowflake query + dashboard |
| Host | Local file | DigitalOcean App Platform |
