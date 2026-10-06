# Umesh Linga — Cinematic Portfolio (v15)

Professional hero built from Umesh's real face, with an AI guided voice introduction.

## Run it

```
python3 -m http.server 5173
```

Then open http://localhost:5173 — any static file server works; there is nothing to compile.

## Structure

- `index.html` — the whole site (opening wordmark scene, project universe, 2021–2026 timeline, finale)
- `assets/hero-face-pro.webp` — professional face/body hero plate (generated from his face reference; not his plaid/brick-wall recording look)
- `assets/umesh-ai-intro.mp3` — AI guided introduction touring the portfolio; plays when a visitor presses Play (browsers require that click for sound). Umesh's own recorded audio is deliberately NOT used.
- `assets/umesh-face-reference.jpg` — source face reference kept for future regenerations

## Swap in a real walking clip later

Shoot 5–10 seconds walking toward camera on a plain light background, save it as `assets/walking.mp4`, and replace the hero `<img>` with a `<video autoplay muted loop playsinline>` pointing at it. No other wiring changes.


---
Previous build notes:
# Umesh Linga — Cinematic Portfolio (v14)

A single-page cinematic portfolio for **Umesh Linga, Bioinformatics Engineer** (Indianapolis).
The hero uses Umesh's **real face and real voice** — his own recorded introduction video —
not an avatar, not a cartoon, and no generated face.

- Live contact: +1 (317) 427-5601 · umesh.linga25@gmail.com
- GitHub: https://github.com/umeshlinga
- LinkedIn: https://www.linkedin.com/in/umesh-linga-aa8321293/

## Run it

Any static file server works — there is nothing to compile.

```bash
# from this folder
python3 -m http.server 5173
# then open http://localhost:5173
```

Or simply open `index.html` in a browser (video playback works from file:// in most browsers;
a local server is recommended).

> **Sound note:** browsers block autoplay with sound. The big
> **“▶ Play my introduction”** button is the click that lets the video play
> with `muted = false` — that's deliberate, not a bug.

## Structure

```
index.html              the whole site (markup, styles, and one inline <script>)
assets/
  umesh-intro.mp4       Umesh's real intro video — 720×1280 portrait, ~19s, H.264/AAC
  umesh-poster.jpg      poster frame shown before the video plays
README.md               this file
```

No frameworks, no build step, no external CSS/JS dependencies.
The only remote asset is Umesh's GitHub avatar image in the finale.

## What each scene does

1. **Scene 1 — Opening.** Dark cinematic hero: giant UMESH LINGA wordmark,
   skill chips, film grain + vignette, and a parallax background on scroll.
   The intro video panel *walks in* from the left (slide + step-bob animation,
   settling to scale 1), followed by a “steps” progress bar that fills as the
   video plays. The caption under it says, plainly: *“This is me — my real
   face and voice.”*
2. **Scene 2 — Project universe.** Six real projects as cards at different
   depths; moving the pointer parallaxes them (desktop only), and clicking a
   card opens its GitHub link. A full accessible list of the same projects
   follows in the “Projects that ship answers” section.
3. **Scene 3 — Time machine.** Interactive 2021–2026 timeline
   (Cipla → IU Indianapolis ×2 → Translation Commons → Karyon Bio).
   Tap a year and the detail panel switches.
4. **Finale.** Black closing scene with Umesh's GitHub avatar, a big closing
   line, and contact buttons (GitHub, LinkedIn, email, phone).

## Swapping in a future walking clip

When a real walking/talking clip of Umesh exists (phone video is fine —
vertical, plain light background, subject roughly centred, 10–20 seconds):

1. Re-encode it to a web-friendly MP4 (H.264 video + AAC audio, faststart):

   ```bash
   ffmpeg -i walking.mp4 -c:v libx264 -pix_fmt yuv420p -c:a aac -movflags +faststart assets/umesh-intro.mp4
   ```

2. Grab a poster frame from a clear moment:

   ```bash
   ffmpeg -ss 2 -i assets/umesh-intro.mp4 -frames:v 1 assets/umesh-poster.jpg
   ```

3. Reload the page. Nothing else to wire — the `<video>` element, walk-in
   animation, play button, and progress bar all point at those two filenames.
   If the new clip is landscape instead of portrait, also change
   `aspect-ratio: 9/16` on `.vframe video` in `index.html` to match.

## Notes

- This is a **local, unpublished build**. No remote GitHub repo has been
  created and nothing has been pushed.
- All copy is Umesh's real background: projects from his GitHub, employers and
  dates from his resume (Karyon Bio title: **Bioinformatics Engineer**,
  Apr–Sep 2026).
