# Interpreter — Real-Time ER Medical Translator

Doctor speaks English. The patient instantly hears their native language in a calm voice that preserves the urgency and emotion of the original — cutting the "wait for an interpreter" delay that costs ER patients time and outcomes. Built for HackHCC CodeRunners, aimed at the ~145 languages spoken across Houston and the Texas Medical Center.

## What it does
- Listens to the clinician in English (speech-to-text) and speaks the translation aloud in the patient's language (text-to-speech).
- Detects urgency/emotion in the doctor's speech and shapes the spoken voice — calm, reassuring, urgent, or critical — so tone survives translation.
- Pulls the patient's record (preferred language, allergies, current meds, visit history) and auto-glosses medication terms for the interpreter.
- Streams anonymized consult metadata to analytics that flag which language gaps drive the most readmissions.

## Try the demo (no install)
1. Open `demo-assets/interpreter-demo.html` in **Chrome or Edge** (Web Speech API support).
2. Pick the patient's language.
3. Tap the mic and speak an English sentence, **or** type one and press Send, **or** tap a quick ER phrase.
4. The patient pane shows the translation and speaks it aloud; the emotion meter shows the detected tone.

The demo runs entirely in the browser. Speech recognition and voice playback are local (no audio leaves the device). Translation uses a live API with an offline ER-phrasebook fallback, so the core phrases work even with no network on stage.

## Full stack (production)
| Layer | Tech | Role |
|---|---|---|
| Voice | **ElevenLabs** | Emotive, multilingual TTS that carries tone, not just words |
| Speech-in | Web Speech API / Whisper | Doctor's English → text |
| Data | **MongoDB Atlas** | Per-patient visit history, allergies, medication-term glossary |
| Analytics | **Snowflake** | De-identified language-gap → readmission analytics |
| Hosting | **DigitalOcean** | Realtime relay + API, low-latency delivery |

## Local setup (production app)
> Code lives in `/src` (owned by the team). The demo above needs no setup.

```bash
# 1. clone
git clone <repo-url> && cd interpreter

# 2. env
cp .env.example .env
#   ELEVENLABS_API_KEY=...
#   MONGODB_URI=...            # Atlas connection string
#   SNOWFLAKE_ACCOUNT=...      # + user / password / warehouse / db
#   DO_APP_URL=...

# 3. install + run
npm install
npm run dev        # serves the app locally
```

## Repo layout
```
/demo-assets   live browser demo (interpreter-demo.html)
/docs          architecture, sponsor-prize alignment
/submission    Devpost materials (this file, problem statement, demo script, sponsor tech)
/src           application code (team-owned)
```

## Safety note
Prototype, not a certified medical device. Production use requires clinical validation, a human interpreter fallback for high-stakes consent, and compliance review (HIPAA, qualified-interpreter regulations).
