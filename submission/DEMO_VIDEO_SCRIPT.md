# 3-Minute Demo Video Script — Interpreter

**Total: 3:00. Format: [TIME] — ON SCREEN — SPOKEN.** Keep it tight; don't overrun, judges stop watching.

---

### [0:00–0:18] — Hook
**ON SCREEN:** Black slide, white text: "An ER patient who doesn't speak English waits minutes to over an hour for an interpreter." Then: "Houston speaks ~145 languages."
**SPOKEN:** "In an emergency room, the most dangerous gap isn't always medical — it's language. A patient who doesn't speak English can wait minutes, sometimes an hour, for an interpreter. In Houston, where 145 languages are spoken, that wait happens every shift. And in an ER, the moment passes before the words arrive."

### [0:18–0:38] — The stakes
**ON SCREEN:** Patient record panel (Maria G.), highlight the prior visit: "No interpreter on shift → left against advice."
**SPOKEN:** "This is the kind of record we built around. Maria came in with chest tightness, no interpreter was free, and she left against medical advice. That's not a translation problem — that's an outcomes problem. So we built Interpreter."

### [0:38–1:45] — Live demo (the core — do NOT rush this)
**ON SCREEN:** The app. Doctor side English, patient side Spanish.
**SPOKEN + DO:**
- "The doctor just speaks English." → Tap mic, say: **"Where does it hurt?"** → patient pane shows Spanish and speaks it aloud.
- "The patient hears their own language — and listen to the voice." → Say: **"We need to do this now."** → point at the emotion meter jumping to **Urgent**. "It caught the urgency and carried it into the voice. Tone is clinical information — a scared patient reads how you say it, not just what you say."
- "And it reassures." → Say: **"You are going to be okay, take a deep breath."** → meter shifts to **Reassuring**, voice softens.
- "145 languages, one tap." → Switch dropdown to **Vietnamese**, say **"Are you allergic to any medication?"** → it speaks Vietnamese.

### [1:45–2:20] — Under the hood (sponsor tech)
**ON SCREEN:** Architecture diagram.
**SPOKEN:** "Four pieces. **ElevenLabs** gives us a voice that conveys emotion, not a flat robot. **MongoDB Atlas** holds each patient's history, allergies, and a medication glossary — so 'Lisinopril' becomes 'your blood-pressure medication,' not a confusing brand name. **Snowflake** takes anonymized consult data and tells the hospital which language gaps drive the most readmissions. And it all runs low-latency on **DigitalOcean**, because latency is the whole point."

### [2:20–2:45] — Why it matters / why TMC cares
**ON SCREEN:** Snowflake panel: "+38% 30-day readmission lift when no interpreter reaches the patient in time."
**SPOKEN:** "Limited-English patients have longer stays and higher readmissions for the same conditions. Interpreter closes the gap at the bedside in seconds, and turns every consult into data that tells a hospital where to staff. For the Texas Medical Center, that's safer care and lower readmissions across 145 languages."

### [2:45–3:00] — Close
**ON SCREEN:** Logo + line: "Interpreter — the words arrive in time."
**SPOKEN:** "We remove the wait that costs patients their outcomes. The doctor speaks. The patient understands. Immediately. That's Interpreter."

---

## Recording notes
- Record the live demo in **one unbroken take** if you can — judges trust live over edited.
- Have the offline phrasebook path ready in case venue wifi dies (those exact phrases above are in the fallback dictionary).
- Mic up close; the patient-voice playback must be audible in the recording.
- If you wire real ElevenLabs before recording, **re-record the [1:45] line** to say "you're hearing ElevenLabs right now" — that's worth points.
