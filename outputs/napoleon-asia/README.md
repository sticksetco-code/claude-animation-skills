# What If Napoleon Discovered Asia Before America?

An original 40-second, 1080 x 1920, 30 fps, seven-scene animated alternate-history reel. All graphics are drawn deterministically in Canvas. The voice is synthetic English male narration (Kokoro `am_michael`), and the music and sound effects are generated programmatically. No stock footage or commercial music is used.

## Historical framing

This is fiction. Asia was already inhabited by advanced civilizations with powerful states and long-established international trade. “Discovered” is the fictional European explorer's perspective, not a claim of actual discovery. The opening explicitly labels the story fictional alternate history. The maps and hybrid port/royal architecture are illustrative rather than exact reconstructions. Napoleon's familiar bicorne and uniform are intentional anachronisms for recognition.

Background references checked during production:
- https://en.wikipedia.org/wiki/Napoleon — born 15 August 1769; the earlier explorer is fictional.
- https://en.wikipedia.org/wiki/Ming_dynasty — dynasty dated 1368–1644.
- https://en.wikipedia.org/wiki/Malacca_Sultanate — established international trading port in the region.

No particular conquest, military encounter, or alliance in this film is presented as historical fact.

## Files

- `web/visuals.js`: original shared Napoleon/supporting-character rig, expressions, costumes, globe, map, harbor, trade goods, army and effects.
- `web/shots.js`: all seven scenes at 0–5, 5–10, 10–16, 16–22, 22–29, 29–35 and 35–40 seconds.
- `web/main.js`: the skill's compositor, captions, transitions, grain and camera motion.
- `web/lib.js`, `web/env.js`, `web/chars.js`: skill framework helpers (MIT); bundled font licenses are in `web/fonts`.
- `tools/render.js`: skill renderer adapted to serve local assets over HTTP; uses system Chrome through `CHROME`.
- `script.json`: the requested English narration; “1490” is spelled out for pronunciation.
- `audio/scene_timing.json`: sentence placement within the storyboard.
- `audio/vo.wav`, `audio/music.wav`, `audio/sfx.wav`, `audio/mix.wav`: separate voice, score, effects and stereo mix.
- `audio/words_new.json`, `web/words.js`, `narration.srt`: synchronized caption timings. ASR matched 72/74 tokens, with the two written-number tokens interpolated by the skill's aligner.
- `audio.py`: editable original score and sound-effect cues using the skill's synthesis functions.
- `tools/time_voice.py`: sentence placement and duration fitting from the original TTS takes.
- `build.sh`: repeatable seven-scene render, concatenation and final H.264/AAC export.
- `verification.json`: measured metadata of the delivered MP4.

## Rebuild using the included narration

Requires Node 18+, Python 3.9+, ffmpeg/ffprobe and Chrome/Chromium. No model downloads are needed to render the supplied narration and mixed soundtrack.

```bash
npm ci --no-audit --no-fund
ANIMATION_KIT="$PWD" CHROME=/usr/bin/chromium bash build.sh
```

On a Mac with Google Chrome installed:

```bash
ANIMATION_KIT="$PWD" CHROME='/Applications/Google Chrome.app/Contents/MacOS/Google Chrome' bash build.sh
```

This uses three render workers with one ffmpeg encoding thread each. The render generates `seg/`, `silent.mp4`, and `napoleon-asia.mp4`. The final video uses H.264/yuv420p, 30 fps, AAC stereo, and faststart. Exact duration is 40 seconds / 1,200 video frames.

To regenerate the procedural score, install NumPy, SciPy and SoundFile, then run `python audio.py` from this folder. To regenerate narration, use the repository's `skills/stick-figure/engine/tools/tts_kokoro.py` and `align.py`, with its optional voice setup. Original per-line takes are included for retiming. The production environment's Python package versions are in `requirements-voice.txt`; models are not bundled.

To preview selected times:

```bash
NODE_PATH="$PWD/node_modules" CHROME=/usr/bin/chromium node tools/render.js stills 1,6,12,18,24,31,39.4
```

The final pose is held from 39.25 seconds; grain remains subtly animated as a film finish. The scene files are fully editable, with no external asset requests at render time.
