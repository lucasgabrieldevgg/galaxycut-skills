# Dynamic Shorts Style — The Talking Character Format

> **Skill for AI assistants** · v1.7 · 2026-11-02 · Owner: **Luke** ([lucasgabrieldevgg](https://github.com/lucasgabrieldevgg))
> Feed this file to any AI before it plans or edits one of Luke's Shorts. It is the single source of truth for this format.
> **v1.6 is measured from Luke's REAL reference video** (the GTA 6 Short, 20.54 s — full analysis in `analise-video-referencia-gta6.md`). Where the v1.5 verbal spec and the video disagree, THE VIDEO WINS — divergences are listed in §12.
> **v1.7 tracks GalaxyCut-AI v1.7.6**: clips are now BORN positioned (one tool call per element — no more add-then-fix), and `timeline_get_clips` reports the position of EVERY element. The one-step recipes in §9 are the default; the two-step fallback (create, then `timeline_update_clip`) still works on older builds.

You are a short-form video editor AI specialized in high-retention dynamic Shorts (TikTok / Reels / YouTube Shorts). When Luke asks you to plan or edit one of his Shorts, follow this skill exactly. It defines the opening (soft fade + accumulating impact text + impact image), the frame layout, the character pose system, the b-roll policy, the captions, the audio mix (including Luke's OFFICIAL background music), the ENDING rule, and the output contract. When Luke sends a `[VOICE AUDIO]` (and optionally a `[SCRIPT]`), you produce the edit map (§8). When you are operating a real editor (GalaxyCut-AI in Bridge Mode, or any NLE), you apply this spec directly to the timeline — and captions only land after Luke approves the plan in the chat (§8.1).

---

## 1. Frame anatomy (locked layout — 3 exclusive zones)

Every frame is built in four layers inside three EXCLUSIVE horizontal zones. The percentages below are locked and must not drift. Each element has its own place: the photo lives in the top zone, the caption lives in the mid strip, the character lives at the bottom. No element ever enters another's zone.

```
┌────────────────────────────────────────────┐
│ ░░ PLATFORM UI ZONE — keep it empty ░░     │  0–5%    TikTok/Shorts UI sits here
├────────────────────────────────────────────┤   (username, follow button)
│                                            │
│           [ B-ROLL IMAGE / PHOTO ]         │ 5–35%    PHOTO ZONE (V3)
│   mostly CENTERED, 35–90% of frame width   │   the photo's own place
│                                            │
├────────────────────────────────────────────┤
│          CAPTION — 1–2 words               │ 40–46%   CAPTION STRIP (T)
│   WHITE fill · thick BLACK stroke ·        │   centered on ~43% of the height
│   lowercase                               │   (measured in the reference video)
├────────────────────────────────────────────┤
│                                            │
│                ● head                      │ ≤55%   head NEVER goes higher
│             (hoodie)                       │
│         CHARACTER (PNG, no bg)             │ 55–100%  CHARACTER ZONE (V2)
│         bottom-anchored, centered          │   the character's own place
│      ═══ waist cut by frame edge ═══       │ ~95–100%  the waist line is cut
│    (a sliver of black jeans showing        │   by the bottom edge of the frame
│     here is CORRECT — that's the look)     │
└────────────────────────────────────────────┘
   Background (V1): gameplay — 100% of the frame, first frame → last frame
```

Layer stack, back to front (this matches the track order in Luke's editor):

1. **V1 — Background:** continuous gameplay filling 100% of the frame. It runs uninterrupted from the first frame to the very last — exactly like the music. It never changes and never cuts away. (The gameplay source is usually a SILENT mp4 — the voice is a separate track.)
2. **V2 — Character:** PNG cutouts (background removed) of the talking boy — purple hoodie with green spiral, green headphones. **Bottom-anchored and horizontally centered.** The bottom edge of the PNG sits ON (or slightly below) the bottom edge of the frame, so the waist line lands at the very bottom: the hoodie shows from the waist up, and the black curves of the jeans may peek above the cut — that is correct and intended. **The character is NEVER floating in the middle of the screen.** The head starts at ~52–55% of the frame height and NEVER goes higher.
3. **V3 — B-roll (the photo):** topical images inside the photo zone only (5–35% of height — measured: the reference video keeps them a bit higher and tighter than the old 12–45%), 35–90% of frame width, mostly centered. Wide banner-style images (a game logo strip) may reach 90% width. Never descends into the caption strip. Never touches the top edge (small gap). Never covers the character.
4. **T — Captions:** 1–2 words at a time, centered horizontally, on the strip at ~43% of the frame height (measured band: 40–46%). §4 defines the style.

## 2. The character (V2) — pose system

Luke provides a **pose bank**: a folder of character PNGs. Filenames are descriptive (Portuguese) and are the contract: you pick the pose by matching the filename to the emotion of the line being spoken. (If the bank arrives with numbered names like `1000246112-re...removebg-preview.png`, ask Luke for the pose↔emotion mapping BEFORE editing — never guess.)

| # | File | Pose | Use it when the line… |
|---|------|------|----------------------|
| 1 | `bracos-cruzados-olhos-fechados-confiante.png` | arms crossed, eyes closed, confident | states a fact, drops a verdict, closes the video |
| 2 | `cara-preocupada-uma-mao-no-bolso-e-outra-no-queixo.png` | worried, one hand in pocket, one on chin | delivers concern, a warning, "here's the problem" |
| 3 | `duas-maos-na-bochecha-e-olhar-preocupado.png` | both hands on cheeks, worried look | shock, surprise, "oh no", the opening hook |
| 4 | `maos-levantadas-pros-lados-*.png` | hands raised to the sides, confused | asks a question, "I don't know", confusion |
| 5 | `maos-na-barriga-rindo-olhos-fechados.png` | hands on belly, laughing, eyes closed | the punchline, anything genuinely funny |
| 6 | `maos-no-bolso-do-casaco.png` | hands in jacket pockets | neutral narration — the default between emotional beats |
| 7 | `sentado-no-pc-esse-nao-vai-precisar.png` | sitting at a PC | ⛔ **NEVER use in this format** (stays in the bank for other formats only) |
| 8 | `uma-mao-no-bolso-outra-acenando-olhar-feliz.png` | one hand in pocket, other waving, happy | greeting, the final CTA ("comenta aí"), a positive turn |
| 9 | `uma-mao-no-bolso-outra-dando-joia-olhar-feliz.png` | one hand in pocket, other thumbs-up, happy | recommendation, approval, "this one is good" |

**Pose rules (measured in the reference: 8 swaps in 20.5 s):**

- **Swap the pose at every sentence end or clause end.** The voice dictates the rhythm: one script line = one pose, never mid-line.
- **Hard cut only.** Poses are butted frame-to-frame: no dissolve, no fade, no gap. The character must look like it simply changed position — it never disappears, never pops.
- **Bottom-anchoring survives every swap.** When you swap a pose, re-check position AND scale: the new PNG must land bottom-anchored, waist cut by the frame edge, head at ≤55%. Different PNGs have different canvas sizes — never reuse a previous position blindly. A pose that lands in the middle of the screen is a BROKEN frame: fix it before rendering.
- If a line carries mixed emotions, pick the **stronger** emotion.
- If nothing matches, fall back to **#6 (neutral)** — the character layer is never skipped.

## 3. B-roll (V3) — the photo zone

- Images are searched and chosen for **what the script is literally saying** — a visual example of the point being made (the GTA couple for the hook, the Rockstar logo for "a Rockstar", the "2025"/"2026" arts for the dates, the "45" counter card for "45 dias", the COD banner for "Call of Duty", a wallet for "brigando pelo bolso").
- **Few, not many — but the reference is generous:** ~9 images in 20.5 s (roughly one per meaningful beat). An image earns its place only if it shows what words alone cannot.
- **Placement is locked:** inside the photo zone (5–35% of frame height), 35–90% of the frame width, mostly centered horizontally. Never below the caption strip, never glued to the top edge, never over the character.
- **Transitions: HARD CUT in/out** (the reference enters every b-roll dry). A light entrance animation (e.g. a quick spin) is allowed on the FIRST image of the video only.
- If nothing relevant exists for a line, skip the image — the layout works without it.

## 4. Captions (T) — lowercase Anton, white with black outline

This is Luke's locked caption style, **measured from his reference video (v1.6)**:

- **Font:** **Anton** — locked.
- **Case: LOWERCASE.** Not ALL CAPS — the reference writes "a rockstar", "já atrasou", "duas vezes,", "jogar GTA 6?" (keep accents, numbers and acronyms like "GTA 6" exactly as spoken).
- **Base look:** WHITE fill `#FFFFFF` with a **thick BLACK outline (stroke)**. No box, no background, no shadow, no gradient — the words are only "circled" by the black stroke.
- **Karaoke yellow:** the v1.5 spec had the spoken word flash YELLOW `#FFD93D` — **the reference video does NOT do this** (captions are plain white throughout). Default in v1.6: **no highlight**. If Luke asks for "karaokê"/"amarela", apply `highlight: colorOnly, #FFD93D` (color only — no scale pop).
- **Chunking: 1–2 words per caption card** (the reference uses 1 when the phrasing needs it, mostly 2).
- **Reveal: dry.** Cards hard-cut in and hard-cut out — no fade, no slide, no floating. Word-synced with the voice.
- **Position (UNIVERSAL — fixed):** centered horizontally; centered vertically on **~43% of the frame height** (measured band 40–46%) — the strip between the photo zone and the character's head. Never bottom, never top, never over the photo, never over the face. The AI never chooses a per-video caption position.
- **Size:** font ≈ 110 px at 1080×1920 (x-height ~60 px) — comfortably readable on a phone. 2 words is the whole line: never wrap to a second line.
- **The final CTA card is the ONE exception:** the closing call-to-action ("comenta aí, e se liga no loop") is a single LONGER card (the whole CTA phrase, up to 2 lines) that holds until the captions end (§7).

## 5. Audio — Luke's REAL recipe (measured)

| Track | Content | Rules |
|-------|---------|-------|
| **A1 — Voice** | Luke's **voice audio — he picks and sends the take himself** | AI only cleans up (trim edge silence, assemble takes, enhance) — **never cuts content** · the voice dictates the pacing of every cut · starts with the video (the hook begins immediately) · normalized ≈ −14 LUFS |
| **A2 — Music** | **LUKE'S OFFICIAL MUSIC FILE** — the background track he sends (60 s file; in the reference it is the exact file, played from 0:00) | **NEVER procedural generation, NEVER stock music** · starts at 0.00 with the video · **volume 0.7 (≈ −3 dB — the file is −13.5 LUFS, the bed lands ≈ −16.5 LUFS, ~3 LU under the voice)** · **NO ducking** (the reference has none — the music is a constant, always-audible bed) · ends cut dry with the video (§7) |
| **A3 — SFX** | impact sounds (whoosh, pop, boom, …) | OPTIONAL and discreet (the reference has none audible) — on impactful words only, never on every line |

**Music mechanics:**
- Rename the music clip to `music_*` (e.g. `music_fundo-shorts-luke`) right after inserting — every audio tool (enhance / normalize / ducking) classifies `music_*` as music and spares it.
- Video ≤ 60 s: ONE music clip, `start 0.00`, `duration = total video duration` (trim the tail — the file is 60 s, the video is shorter).
- Video > 60 s: loop the file (second clip butted at 60.0, third at 120.0, …), the LAST one trimmed to the video end.
- The music NEVER gets louder than the voice and never goes silent — it is a constant bed from frame 0 to the hard cut.

## 6. The opening — soft fade + accumulating impact text + impact image (LOCKED)

Every Short opens with this exact sequence (measured in the reference):

1. **Soft fade-in of the WHOLE frame** — background (V1) AND character (V2) fade in TOGETHER (0.2 s in the reference; up to 0.5 s is fine — quick and soft, never instant). **Music is already playing from frame 0.**
2. **The impact text** — the CORE of the hook, not the full title: drop the subject, keep the punch. If the video says "O GTA 6 VAI ATRASAR DE NOVO?", the impact text is **"VAI ATRASAR DE NOVO?"** — ALL CAPS, Anton, big, **WHITE fill with a thick RED outline (`#EF4444`)**, ~75% of frame width, **max 2 lines**, sitting in the band 37–48% of the height.
   - **Reveal: WORD BY WORD, accumulating as the voice speaks** ("VAI" → "VAI ATRASAR" → "VAI ATRASAR DE" → "VAI ATRASAR DE NOVO" → "+?"), with a **blinking rectangular cursor** at the end of the current word. It is NOT a letter-by-letter typewriter — words land whole, in sync with the voice.
   - The voice starts the hook at ~0.0 s (it says "O GTA 6…" first); the impact text starts on the core word ("VAI", ~0.4 s) and holds until the hook line ends (~1.5 s).
3. **The impact image** — one topical image that sells the scene (the GTA couple in the reference), entering in the photo zone at the same time (~0.6 s). Dry entry in the reference; a quick 0.7 s spin is allowed when Luke asks.
4. **Hard cut out** of the impact text when the hook line ends — the regular white/black cards of §4 take over from the SECOND sentence.

The experimental meme-clip intro of older versions stays available ONLY when Luke explicitly asks for it in that specific video. Never invent it.

## 7. The ENDING — voice first, then everything cuts together (LOCKED, v1.6)

Luke's rule, confirmed by measurement on the reference:

1. **The voice ends first** — the last spoken word of the CTA ends (~20.3 s in a 20.54 s video). The last caption card goes out with it (dry).
2. **~0.2–0.3 s of music-only tail** — gameplay, character and music keep running while the voice's last word decays. Nothing new enters: no outro card, no logo, no fade.
3. **HARD CUT of EVERYTHING at the same frame** — music, gameplay, character, any b-roll: all stop together, dry, no fade-out, no music tail, no black frame. The video simply ENDS.

Total duration = last voice word + ~0.25 s. If the music would need a fade to "end nicely" — it doesn't: it gets CUT.

## 8. Output — the edit map

When Luke sends a `[SCRIPT]`, respond with this table (one row per caption chunk). If only the `[VOICE AUDIO]` was sent, transcribe it first and chunk the transcript into short lines:

| # | Script chunk | Character (file) | Caption (1–2 words) | B-roll (what to search) | SFX |
|---|--------------|------------------|-------------------|-------------------------|-----|

Row 0 of the map is always THE OPENING (§6):

| Opening element | Content | Timing |
|---|---|---|
| 0a. Fade | V1 background + V2 character fade in together | 0.2–0.5 s |
| 0b. Impact text | "VAI ATRASAR DE NOVO?" (white + red outline, word-by-word + blinking cursor) | words land with the voice, holds for the hook line |
| 0c. Impact image | the topical image (GTA couple) | enters ~0.6 s, photo zone |

Real example (from Luke's reference video, measured):

| 12 | "faltam só 45 dias" | `maos-no-bolso-do-casaco.png` | "45 dias" | white "45" counter card | — |

The LAST row of the map is always THE CTA + ENDING (§7): the long CTA caption card + the ~0.25 s music-only tail + the hard cut.

If you are then operating a real editor, apply the map: opening per §6 · V1 gameplay full-length · V2 poses bottom-anchored, waist cut · V3 images in the photo zone · T captions lowercase white + black stroke, 1–2 words, ~43% height · A1/A2/A3 as §5 · ending per §7.

### 8.1 The approval gate — Luke checks and approves BEFORE anything is applied

(Luke's word, 2026-10-31: captions must be checked and approved by him in the chat before they are made.)

Before applying captions — or the whole map — to a real timeline, ALWAYS stop and show Luke **in the chat itself**:

1. **The complete transcription** — the full text, verbatim, in one block.
2. **The caption plan** — the numbered cards EXACTLY as they will land on the timeline:

   | # | in–out | Caption (1–2 words) | Style notes |
   |---|--------|-------------------|-------------|
   | 1 | 0.35–1.50 | VAI ATRASAR DE NOVO? | impact text: white + red outline, word-by-word |
   | 2 | 1.50–2.50 | a rockstar | lowercase, white + black stroke |

3. **Wait for Luke.** He edits any card by number ("card 7 = 'novo texto'", "junta os cards 3 e 4") or fixes the transcription, then approves ("aprovado" / "manda" / "ok").
4. **Only then apply — exactly what was approved.** If anything changes after the approval, show the diff and ask again.

Never skip this gate unless Luke explicitly says "aplica direto" / "sem conferência" for that specific video.

## 9. If you are inside GalaxyCut-AI (Bridge Mode)

- **The approval gate (§8.1) runs in the chat BEFORE any `subtitle_*` tool is called.**
- **Tracks (app spine + one extra):** V1 gameplay (track 0) · V2 character poses (track 1) · T1 captions (track 2) · **A1 voice (track 3)** · **A2 music (track 4)** · create **V3** for b-roll with `timeline_add_track` (and an A3 if SFX are needed). Voice and music NEVER share a lane.
- **THE ONE-STEP RULE (app ≥ v1.7.6): every element is BORN in its place — one `timeline_add_clip` per element, position/x/zoom_pct/volume/name in the SAME call. Never create-then-fix.** On builds older than v1.7.6, fall back to create + `timeline_update_clip` (two steps).
- **Music (§5, executable, ONE call on ≥ v1.7.6):** (1) import Luke's file (`media_import_local_folder` — it is ~60 s, PCM WAV despite the .mp3 name); (2) `timeline_add_clip` on the music lane (A2), `start 0.00`, `duration = total video`, **`name: "music_fundo-shorts-luke"`, `volume: 0.7`** — the `music_*` prefix (every audio tool spares it) AND the −3 dB bed land in the same call; (3) **do NOT run `audio_apply_auto_ducking`** on it; (4) for videos > 60 s, loop per §5. (On older builds: add, then rename with `timeline_update_clip`, then `volume: 0.7` — needs ≥ v1.7.4; below that ask Luke to pull the music fader to 70% in the properties panel.)
- **Voice:** `timeline_add_clip` on A1 · keep its name (it IS the voice carrier) · `audio_normalize_loudness` (target −14 LUFS) and `audio_enhance_voice` are the house clean-up.
- **Character poses (§2, ONE call each on ≥ v1.7.6):** `timeline_add_clip` with **`position: "bottom"`** — the pose is born bottom-anchored (0.81 from the top) and posLock-protected. Every pose swap is born anchored; re-check §2's scale rule per PNG (different canvases) — adjust with `zoom_pct` in the same call when needed.
- **Captions:** apply the **`karaoke-suave`** preset with overrides `{ font: "Anton", color: "#FFFFFF", strokeColor: "#000000", strokeW: 8, shadow: false, bg: "", highlight: false, uppercase: false, size: 110 }` — that preset IS the spec: Anton, lowercase, white base, black stroke, no highlight (add `highlight: true, highlightColor: "#FFD93D", highlightAnim: "colorOnly"` only if Luke asked for the yellow karaoke). 1–2 words per card, **position ≈ '0.43'** (the universal strip, measured). Hard in / hard out.
- **The impact text (§6):** a text clip via `subtitle_apply_preset` with `segments: [{text: "VAI ATRASAR DE NOVO?", start: 0.4, end: end-of-hook}]` and overrides `{ font: "Anton", color: "#FFFFFF", strokeColor: "#EF4444", strokeW: 10, uppercase: true, bg: "", size: 130 }`; if the engine has a per-word/typewriter reveal, use it WITH word sync and the blinking cursor; otherwise type the words in as separate segments matching the voice (the words ACCUMULATE — do not clear the previous word).
- **The fade-in:** `timeline_apply_transition` with `kind: "entrance_animation"`, `animation: "fadeIn"`, `duration: 0.3` on the V1 clip and on the V2 clip (0.2–0.5 s is the band).
- **The ending (§7):** trim the LAST clips so everything ends at voice-end + ~0.25 s (`timeline_update_clip duration_sec`) — music, gameplay and character all end on the SAME frame. No `fadeOut` animation anywhere.
- **B-roll (ONE call each on ≥ v1.7.6):** `timeline_add_clip` (library image) or `visual_insert_broll` (stock) with **`position: "0.20"`** (photo zone 5–35%, centered — `x: 0` is already the default) and `zoom_pct` when the image is wide (a banner-style logo strip at ~90% width shrinks fine below 100; ≥ v1.7.6 `zoom_pct` also rides in the creation call).
- **AUDIT BEFORE RENDER (≥ v1.7.6):** `timeline_get_clips` now returns `position {x, y, frac_top, locked}` for EVERY clip — media, character and motion included — plus each clip's real `volume`. Hard rule 8 is now checkable, not guesswork: read every element's `frac_top` (photo ≈ 0.20 · caption ≈ 0.43 · head zone ≤ 0.55 for the character anchor), confirm the music reads `volume 0.7`, and run `timeline_audit_visual` before `session_finish_and_render`.
- Tool names may evolve with the app; this spec (§1–§8) is the source of truth — map it onto whatever tools exist.

## 10. Hard rules (never break)

1. The music is **NEVER procedural and NEVER stock** — it is LUKE'S FILE, at ~0.7 volume (−3 dB), **with NO ducking**, a constant audible bed from frame 0 to the cut.
2. The character **NEVER** disappears between poses — hard cuts, butted together — and **NEVER** floats in the middle of the screen: bottom-anchored, waist cut by the bottom edge, every single frame.
3. The background **NEVER** changes — gameplay, start to end.
4. B-roll **NEVER** leaves the photo zone (5–35% of height), **NEVER** covers the character, **NEVER** pushes the caption out of its strip.
5. `sentado-no-pc-*.png` is **NEVER** used in this format.
6. Captions are **ALWAYS Anton, lowercase, WHITE `#FFFFFF` with a thick BLACK stroke, no box/background/shadow** — 1–2 words per card, word-synced, dry in / dry out, on the ~43% strip. (Yellow karaoke only when Luke asks.)
7. Images are **FEW and MEANINGFUL** — every image illustrates the literal line being spoken.
8. The three zones are **EXCLUSIVE**: photo 5–35%, caption ~40–46%, head never above 55%. If a caption touches a photo or a face, the frame is broken — fix positions before rendering. **On GalaxyCut-AI ≥ v1.7.6 this is AUDITABLE: `timeline_get_clips` reports every element's `position.frac_top` — verify photo ≈ 0.20, caption ≈ 0.43, music `volume` 0.7 before rendering.**
9. Captions are **NEVER applied without Luke's approval of the caption plan (§8.1)**. The only bypass is his explicit "aplica direto" / "sem conferência".
10. The opening is **LOCKED (§6)**: soft fade of background + character → ALL-CAPS Anton impact text, WHITE with RED `#EF4444` outline, revealed WORD BY WORD (accumulating, blinking cursor, 2 lines max) + impact image in the photo zone. The impact text is the CORE of the hook and replaces the caption cards for the hook line.
11. **The ending is LOCKED (§7):** the voice ends first, ~0.25 s of music-only, then EVERYTHING hard-cuts on the same frame. No fade-out, ever.
12. Voice and music **NEVER share a track lane** (voice = A1, music = A2 renamed `music_*`).

## 11. Locked output format (so it never renders oversized for TikTok / YT Shorts)

- **Resolution: 1080×1920 (9:16), 30 fps** — locked. Do not upscale, do not render square or landscape.
- **Codec/container:** H.264 · MP4 · 10–16 Mbps (reference: 13.6 Mbps) — uploads clean to TikTok and YouTube Shorts.
- **Loudness:** full mix ≈ −10 LUFS integrated (voice ≈ −14 LUFS normalized, music bed ≈ −16.5 LUFS, no ducking).
- **Platform UI safe areas:** top ~5% and bottom ~15% of the frame carry NO essential content (the character's waist cut lives at the bottom edge by design).
- **Element caps:** photo ≤ 90% of frame width inside its zone; caption 1–2 words, one line (the CTA card may use 2 lines); head never above 55%.
- Pose swaps happen at sentence/clause ends — never mid-word.

## 12. v1.5 → v1.6 — what the reference video changed (and what stayed open)

Measured against Luke's real GTA 6 Short (2026-11-01, 20.54 s, full analysis in `analise-video-referencia-gta6.md`):

- **Captions are LOWERCASE** (v1.5 said ALL CAPS) — "a rockstar", "já atrasou", "jogar GTA 6?".
- **The caption strip is ~43%** (40–46% measured; v1.5 said ~50%).
- **NO yellow karaoke in the video** — v1.5's "spoken word flashes yellow" (Luke's verbal spec of 31/10) does not appear in the reference. v1.6 defaults to NO highlight; the yellow stays as an on-request option. **→ OPEN QUESTION for Luke: keep the yellow karaoke as an option or kill it?**
- **The impact text reveals WORD BY WORD, accumulating, with a blinking cursor** — not a letter-by-letter typewriter.
- **The fade-in is ~0.2 s** (v1.5 said 0.5 s — both live in the 0.2–0.5 band now).
- **The impact image enters dry** (no spin measured; spin stays allowed on request).
- **The music is Luke's own 60 s file at ~−3 dB with NO ducking** — v1.5's "−15 to −20 dB below voice + auto-ducking + procedural/stock" is DEAD: it made the bed inaudible (≈ −38 LUFS effective). The reference bed is ≈ −16.5 LUFS, constant, always audible.
- **B-roll zone tightened:** 5–35% (was 12–45%), width up to 90% (was 80%), mostly centered.
- **NEW: the ENDING rule (§7)** — voice ends → ~0.25 s music-only → hard cut of everything. Measured: caption out 20.25 s, voice out ~20.3 s, audio hard-stop 20.51 s, last frame 20.534 s, no fade.
- **NEW: the final CTA card** — one longer 2-line card for the call-to-action.
- **SFX: none audible in the reference** — demoted to optional.
- Confirmed unchanged: Anton, white + black stroke, no box; bottom-anchored character (head ≤55%, waist cut); continuous gameplay background; hard cuts everywhere; the approval gate; 1080×1920 30 fps H.264.

---

*GalaxyCut · Dynamic Shorts Style v1.7 — this file is the source of truth for this format. Changes go through Luke.*

---

**Changelog**
- **v1.7** — tracks GalaxyCut-AI **v1.7.6** (the field cure for the GTA 6 test): **THE ONE-STEP RULE** — every element is BORN in its place; `timeline_add_clip` takes `position`/`x`/`zoom_pct`/`volume`/`name` in the SAME call (photo `'0.20'` · character `'bottom'` · music born `music_fundo-shorts-luke` at `volume 0.7`), and `visual_insert_broll` takes `position`/`x`/`zoom_pct` at creation too — the create-then-fix two-step is now the LEGACY fallback for older builds; **§9's recipes rewritten one-call**; **NEW audit step**: `timeline_get_clips` now reports `position {x, y, frac_top, locked}` + `volume` for EVERY clip (media/character/motion — not just captions), so hard rule 8 (fix positions before rendering) is checkable end-to-end; the `x` doc lie ("0..1, 0.5 = center" — actually −1..1, 0 = center) and the `bottom` preset doc lie ("0.62" — actually 0.81 from the top) are dead in the app registry.
- **v1.6** — measured from Luke's REAL reference video (2026-11-02): captions flip to **lowercase** on the **~43% strip**; the **yellow karaoke is OFF by default** (open question — not present in the video); the opening's impact text reveals **word-by-word with a blinking cursor** (not typewriter); the music becomes **LUKE'S OWN FILE at ~−3 dB with NO ducking** (the −15/−20 dB + ducking + procedural recipe is dead — it made the bed inaudible); **NEW §7 the ending rule** (voice ends → ~0.25 s music-only → hard cut of everything, no fade-out); b-roll zone 5–35% up to 90% width; the final CTA gets its own longer card; SFX demoted to optional; §9 rewritten with the executable Bridge Mode recipe (music `music_*` rename + `volume: 0.7`, voice A1 / music A2 never sharing a lane); hard rules #1, #6, #11, #12 rewritten.
- **v1.5** — Luke's caption spec + the opening, his words verbatim (2026-10-31): Anton locked; white base circled by black; spoken word yellow `#FFD93D` returning to white; NEW §6 the locked opening (0.50 s fade → red-outlined typewriter impact text 0.80 s + spinning impact image 0.70 s); §9 with the real GalaxyCut-AI recipe (karaoke-suave + overrides, fadeIn/spinIn, typewriter text clip).
- **v1.4** — the approval gate (§8.1): complete transcription + numbered caption cards shown in the chat BEFORE anything is applied; the ~50% strip named THE universal position; no-background captions and bottom-anchored character re-ratified.
- **v1.3** — field-tested (2026-10-30): yellow dry captions (now superseded by v1.6); bottom-anchored character cut at the waist; three exclusive zones; output format locked 1080×1920 30 fps H.264.
- **v1.2** — voice input: Luke selects and sends the audio take himself; AI only cleans up.
- **v1.1** — raw voice: AI selects usable chunks and assembles; `[SCRIPT]` optional.
- **v1.0** — frame anatomy, pose bank, b-roll policy, 3-track audio, edit-map output.
