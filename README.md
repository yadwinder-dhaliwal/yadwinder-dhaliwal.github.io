# Portfolio

Personal portfolio site for Yadwinder Dhaliwal, Graphics & Real-Time Simulation Engineer. A single static HTML page with no build step and no dependencies, designed to be scanned by a recruiter in under 10 seconds.

## Features

- Black and white design that follows the visitor's device theme (light or dark), plus a manual toggle that remembers the choice
- Project cards with gameplay / build videos that play only while on screen
- Ambient glow: a playing video's live colours bleed into its own card, then fade back to black and white
- Mobile layout with a menu sheet, 44 px tap targets and inline video playback
- Animated cubic B-spline in the hero, computed in the browser (nod to Project Selene)

## Project layout

```
index.html          # the whole site: markup, styles and script
Yadwinder_Dhaliwal_Resume.pdf  # one-page A4 résumé linked from the hero button
media/
├── headshot.jpg    # 640×640 portrait
├── formula.mp4     # FormulaInfinite gameplay (1280 px, H.264, web-compressed)
├── formula.jpg     # poster frame
├── selene.mp4      # Project Selene current build (Tier 1)
└── selene.jpg      # poster frame
```

## Run locally

Double-click `index.html`, or serve the folder:

```bash
python -m http.server 8000      # then open http://localhost:8000
```

## Deploy (GitHub Pages)

1. Create a repo. Naming it `yadwinder-dhaliwal.github.io` publishes at `https://yadwinder-dhaliwal.github.io`; any other name publishes at `https://yadwinder-dhaliwal.github.io/<repo>/`.
2. Push this folder's contents to the `main` branch.
3. In the repo, go to Settings → Pages → Source: Deploy from a branch → `main` / root.

## Editing content

All copy is plain HTML in `index.html`:

- Hero: `<header class="hero">`
- Projects: one `<article class="card">` per project inside `#projects`; add a `<figure class="media">` with a `<video>` to give a card a video and ambient glow
- Skills and experience: `#skills` and `#experience`
- Colours: the `--bg`, `--ink`, `--mute`, `--line` variables at the top of `<style>` (light values first, dark values in the two blocks below)

To add a video, compress it first so the page stays fast:

```bash
ffmpeg -i input.mp4 -vf "scale=1280:-2" -c:v libx264 -preset veryfast -crf 30 -pix_fmt yuv420p -c:a aac -b:a 96k -movflags +faststart media/name.mp4
ffmpeg -ss 5 -i media/name.mp4 -frames:v 1 -q:v 4 media/name.jpg
```

## To do

- [x] Add the résumé PDF link (hero button)
- [x] Fill in the JDC West IT Specialist description
- [ ] Add RaySense and Anti Smurf media once there is something to show
- [ ] Swap the Selene video as new tiers are finished
