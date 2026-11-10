# Export checks

- H.264 / yuv420p, 1080 x 1920, 30 fps, 1,200 frames, exactly 40.000 seconds.
- AAC stereo narration and soundtrack.
- Full exported video/audio decoded with ffmpeg -xerror: no errors.
- Reviewed one exported frame per second across the entire 40-second timeline, plus full-resolution previews of key poses.
- All seven intended scene intervals present.
- 80 half-second project samples rendered without browser errors or failed asset requests.
- 48 short caption groups, no overlapping subtitle intervals; maximum measured caption width 422 px within the safe-area width of 880 px.
- Narration recognized/aligned against all nine sentences; 72 of 74 tokens matched, with number tokens interpolated.
- Final audio measured at -14.42 LUFS integrated and -1.21 dBTP (no clipping).
- Final pose intentionally held from 39.25 seconds.

Visuals are illustrative alternate history. Narration uses a synthetic English male voice, Kokoro am_michael.
