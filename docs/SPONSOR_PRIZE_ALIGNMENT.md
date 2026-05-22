# Sponsor-Prize Alignment Audit

Each sponsor almost always runs its own prize track judged on **depth of use**, not name-drops. Below: how deep we are right now, why it won't win as-is, and the highest-ROI way to deepen — in the order I'd spend hours.

**Reality check:** the demo *works*, but "it works" is hiding shallow sponsor usage. Browser TTS is not ElevenLabs. A mock chart is not Snowflake. Judges on those tracks will see through it. Fixing this is where the prize money is.

---

## 1. ElevenLabs — HIGHEST ROI, do first
**Current depth:** 🔴 Shallow. Demo uses the browser's built-in SpeechSynthesis. ElevenLabs is named but not called.
**Why it won't win:** The ElevenLabs track rewards using *their* voice tech. Right now you're using zero ElevenLabs. And it's also the heart of your pitch ("voice that conveys tone") — so the gap is both a prize miss and a credibility risk on stage.
**Deepen:**
- Call the ElevenLabs TTS API for the patient-language playback. Even one language live is a massive jump from zero.
- Use **voice settings** (stability / similarity / style) driven by your emotion classifier so calm vs. urgent actually sound different. That *is* "voice that conveys tone" — demo it side-by-side with a flat reading.
- Bonus: ElevenLabs multilingual model so one voice handles many of Houston's languages consistently.
**Time:** ~1–2h for one-language live + emotion-mapped settings. Biggest single score jump available.

## 2. Snowflake — strong differentiator, do second
**Current depth:** 🔴 Shallow. The analytics panel is a hardcoded chart.
**Why it won't win:** "Anonymized analytics on language gaps → readmissions" is a genuinely good Snowflake story — but only if real data hits a real warehouse. A static SVG won't.
**Deepen:**
- Load a few hundred rows of synthetic de-identified consult metadata (language, wait time, readmit flag) into a Snowflake table.
- Write **one real query** that correlates language + interpreter delay with readmission, and show the SQL on a slide. Judges love seeing the actual query.
- Stretch: Streamlit-in-Snowflake or Snowflake Cortex for the dashboard/insight — that reads as "native to the platform."
**Time:** ~2h. Synthetic data + one query is enough to be legitimate.

## 3. MongoDB Atlas — medium, do third
**Current depth:** 🟡 Medium-shallow. Patient panel is a believable mock, schema is sensible, but it's in-page JSON, not Atlas.
**Why it won't win as-is:** Storing JSON in a variable isn't using Atlas. The data model is good though, so the lift is small.
**Deepen:**
- Stand up a free Atlas cluster, load the patient record(s), query live from the app.
- Killer feature for the track: **Atlas Vector Search** on the medication/phrase glossary — semantic match so "the sugar pill" finds "Metformin / diabetes." That's a real, on-theme use of an Atlas-specific capability, not just CRUD.
- Stretch: Atlas Change Streams to push consult events toward the Snowflake pipeline — ties two sponsors together.
**Time:** ~1.5h for live cluster + reads; +1h for vector search.

## 4. DigitalOcean — medium, do fourth (or hand to whoever's free)
**Current depth:** 🟡 Claimed in docs, not deployed.
**Why it won't win as-is:** "We'd host on DO" isn't using DO. Easiest fix on the list, though.
**Deepen:**
- Deploy the relay/API (and the demo page) to **DigitalOcean App Platform**. A live `*.ondigitalocean.app` URL is concrete proof.
- Capture a real **latency number** ("translation round-trip < X ms on DO") and put it in the pitch — latency is literally your value prop, so this doubles as a product point.
- Stretch: DO Gradient/GenAI or a managed DB if you want more surface area on the track.
**Time:** ~1h to deploy + grab latency.

---

## If you only have time for one
Do **ElevenLabs**. It's the prize track most aligned with your core idea, and a flat browser voice actively undercuts the "we preserve tone" pitch in front of judges.

## If you have time for two
ElevenLabs **+** Snowflake. Those two carry the strongest, most differentiated stories for TMC judges (emotive patient care + data-driven readmission reduction).

## Cross-sponsor combo that scores extra
Atlas **Change Streams → Snowflake** (consult events flow from operational store to analytics) shows architectural maturity and touches two tracks with one build. Worth it only after #1 and #2 are live.
