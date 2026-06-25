# VR-DAgger — Project Page

Standalone GitHub Pages site for **VR-DAgger: Immersive VR for Dexterous Data Collection
and Uncertainty-Guided On-Policy Correction** (Robotics Systems Lab, ETH Zürich — IROS 2026).

The site is a single static `index.html` with no build step and no external runtime
dependencies (only the Inter web font and the page's own CSS/JS).

## Structure

```
index.html              # the full page
assets/css/style.css    # ETH-blue theme, layout, responsive
assets/js/main.js        # sticky-nav highlighting, copy-BibTeX, lazy clip playback
assets/img/             # figures (from the paper PDFs) + poster / og / favicon
assets/video/           # web-encoded supplementary video + short looping clips
raw_mat/                # source material (LaTeX, figures, raw 278 MB video) — see note
```

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Deployment

Push to the default branch of the `vr-dagger.github.io` repository; GitHub Pages serves
`index.html` from the repo root automatically.

## Asset pipeline (how the media was generated)

- Figures: `pdftoppm -png -r 200 <fig>.pdf` then `convert -trim` (from `raw_mat/latex_source/figures`).
- Hero video: `ffmpeg -i raw_mat/snippets.mp4 -c:v libx264 -crf 28 -vf scale=1280:-2 -movflags +faststart` → `assets/video/supp.mp4` (~28 MB).
- Clips: 6–8 s muted, looping, `-an`, `crf 30`, `scale=960` → `assets/video/clip_*.mp4`.

## Note on `raw_mat/`

`raw_mat/snippets.mp4` is **278 MB**, which exceeds GitHub's 100 MB per-file limit, so it is
git-ignored. The site uses the re-encoded `assets/video/supp.mp4` instead. To regenerate
media, keep `raw_mat/` locally and rerun the commands above.

## To finalize

- Replace the `href="#"` placeholders on the **Paper / arXiv** and **Code** buttons in
  `index.html` with real URLs (search for `data-placeholder`).
- Update the BibTeX block once publication details are confirmed.
