# Ray'z Welding site: handoff notes

Single-page static site (index.html + images), to be hosted on GitHub Pages at rayzwelding.ca, same setup as the Home Baked Goodness site.

## What's done
- `index.html`: full page. Scroll-scrubbed weld film at the top, then truck, rates, recent jobs, Google reviews, "Text Ray a photo".
- Photos (`truck.jpg`, `weld.jpg`, `cart.jpg`, `hinge.jpg`) are crops from screenshots Lucas sent (low-res; swap for Ray's originals when available).

## Still to do
1. **Add the film.** Generated on Higgsfield (job `dd365cce-1f0b-4f0f-a060-3d5ca0e80777`, 15s, 1080p, no audio):
   https://d8j0ntlcm91z4.cloudfront.net/user_3ILDUMZDrvLzRCFe8Kri261DDIA/hf_20260930_145248_dd365cce-1f0b-4f0f-a060-3d5ca0e80777.mp4
   Download it and encode for scrubbing (short GOP so seeking is instant), writing next to index.html:
   ```bash
   # ffmpeg: `pip install imageio-ffmpeg` gives a static binary if ffmpeg isn't installed
   ffmpeg -y -i source.mp4 -an -vf "unsharp=5:5:0.8:5:5:0.0" -c:v libx264 -preset slow -crf 20 -pix_fmt yuv420p -g 8 -keyint_min 8 -sc_threshold 0 -movflags +faststart rayz-film.mp4
   ffmpeg -y -i source.mp4 -an -vf "scale=-2:'min(720,ih)',unsharp=5:5:0.6:5:5:0.0" -c:v libx264 -preset slow -crf 23 -pix_fmt yuv420p -g 4 -keyint_min 4 -sc_threshold 0 -movflags +faststart rayz-film-mobile.mp4
   ffmpeg -y -ss 0 -i rayz-film.mp4 -frames:v 1 -q:v 2 film-poster.jpg
   ```
   Keep desktop under ~30 MB and mobile under ~15 MB. Don't commit `source.mp4`.
2. Turn on GitHub Pages (main branch, root) and add a `CNAME` file with `rayzwelding.ca`, then give Lucas the GoDaddy DNS records.
3. Waiting on Ray: his story for the site, real service list, logo file, better job photos, the 2 Google reviews not yet on the page.

## Content facts (from Ray's old GoDaddy site + Google)
- Ray'z Welding Ltd., mobile welding & small-scale fabrication, Saskatoon and area, CWB certified.
- Text 306-313-8281 with photos/drawings. Instagram @rayzwelding.
- Mobile repair $99/hr ($144 deposit out of town). Emergency 5-9pm $144/hr ($150+ deposit). Fabrication $99/hr, deposit covers material + sourcing/handling.
- Google: 5.0 stars, 10 reviews.
- Lucas's style rule: no em dashes in site copy.
