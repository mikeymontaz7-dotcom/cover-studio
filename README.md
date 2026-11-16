# Cover Studio

[![Made with pollinations.ai](https://raw.githubusercontent.com/pollinations/pollinations/main/packages/ui/src/brand/badge-made-with.svg)](https://pollinations.ai/?ref=badge)

A finished 2:3 book cover from one line of premise. Type a title, an author and one
sentence; Cover Studio asks [Pollinations](https://pollinations.ai) for the artwork and
sets the type in the browser, then hands you a 1600x2400 PNG.

Live: **https://polli-cover-studio.surge.sh**

## Why it exists

Image models cannot spell. Ask one for a title and the lettering comes back mangled or
half-painted. Cover Studio splits the job: the model paints, the page types. Every word
you see on the finished cover is real text, so it is crisp, correct and editable.

## How it works

1. You paste your own Pollinations key. It is kept in `localStorage` on your device and
   sent only to `gen.pollinations.ai`, never to a server of ours.
2. The premise plus a style preset becomes the image prompt:
   `GET https://gen.pollinations.ai/image/{prompt}?model=flux&width=1024&height=1536&nologo=true`
   with `Authorization: Bearer <your key>`.
3. The artwork is drawn onto a 1600x2400 canvas, a scrim is laid over it, and the title
   and author are set in the chosen typeface with wrapping and fit-to-width.
4. Your browser encodes the canvas to PNG and downloads it. Nothing is uploaded or stored.

## Bring your own key

Pollinations requires a key for every image. Every visitor brings their own, so the app
costs its author nothing to run and each user pays for their own renders. Get a free key
at <https://enter.pollinations.ai/keys>.

## Run it yourself

There is no build step and no dependencies. Any static host will do:

```sh
git clone <this repo>
cd cover-studio
python3 -m http.server 8080
# open http://127.0.0.1:8080
```

## Limits, stated honestly

- The render comes back at 704x1024 (Pollinations normalises to about 1MP at the
  requested aspect ratio) and is upscaled to 1600x2400. Crisp on screen, not native
  print resolution.
- The model sometimes paints incidental lettering into the artwork despite the
  "no text, no lettering" instruction. The app cannot control what it draws; it controls
  only the type it sets on top.

## Licence

MIT. Artwork generated through Pollinations is subject to their terms.
