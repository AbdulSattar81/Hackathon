# Sponsor Tech — What We Used and How

This is the Devpost "which sponsor tech and how" section. One short paragraph per sponsor — concrete, no fluff.

## ElevenLabs — the voice that carries tone
Interpreter's core thesis is that *how* something is said is clinical information. We use ElevenLabs' emotive, multilingual text-to-speech to speak the translated message in the patient's language while preserving the urgency or reassurance of the doctor's original delivery. An emotion/urgency pass on the doctor's speech (calm / reassuring / urgent / critical) drives the voice parameters, so "we need to do this now" lands as urgent-but-controlled and "you're going to be okay" lands as warm and slow — instead of a flat robot that strips the meaning a frightened patient relies on.

## MongoDB Atlas — patient context at the bedside
Atlas stores each patient's record: preferred language, allergies, current medications, and visit history. During a consult, Interpreter pulls this context and applies a medication-term glossary so drug names are explained in plain language ("Lisinopril" → "your blood-pressure medicine") rather than transliterated into nonsense. Atlas is the system of record; it also feeds the de-identified metadata stream into analytics.

## Snowflake — turning consults into staffing signal
Every consult emits de-identified metadata — language, interpreter wait/latency, and an outcome flag — to Snowflake. We correlate language gaps with 30-day readmissions to answer a question hospitals currently can't: *which language gaps are quietly costing us the most?* The output is a dashboard that tells a hospital where to put interpreter resources, backed by data instead of anecdote.

## DigitalOcean — low-latency delivery
The web client and the realtime relay run on DigitalOcean. Latency is not a nice-to-have here — the entire value of Interpreter is that the translated voice arrives before the moment passes — so we host the relay close to the request path and keep the round trip tight.

---

> **Status flag for the team:** the demo currently stands in browser APIs for ElevenLabs (TTS) and uses mock data for Atlas/Snowflake. To actually place in each sponsor's prize track, see `docs/SPONSOR_PRIZE_ALIGNMENT.md` — shallow usage will not win, and there's a clear order to deepen.
