# merlan's birthday card

A single-file interactive birthday card. Vanilla HTML, CSS and JS — no build step, no dependencies. Everything lives in `index.html`.

Open the cover, read the letter, then blow into your mic to put the candles out.

## Put it online (GitHub Pages)

The microphone only works over `https`, so opening `index.html` by double-clicking it will not let you blow out the candles. Host it instead — it takes about two minutes and it's free.

1. Go to github.com and click **New repository**. Name it something like `merlan-birthday-card`. Set it to **Public**. Create it.
2. On the empty repo page, click **uploading an existing file**, drag `index.html` in, and click **Commit changes**.
3. Go to **Settings → Pages** in that repo.
4. Under **Source**, pick **Deploy from a branch**. Branch: `main`, folder: `/ (root)`. Save.
5. Wait about a minute, then refresh. GitHub shows the live link at the top — it'll look like `https://yourusername.github.io/merlan-birthday-card/`.

That link is what you send her. It works on phones.

## Changing things

Everything editable is in the `CONFIG` block at the top of the `<script>` tag near the bottom of `index.html`:

```js
const CONFIG = {
  name: "merlan",          // cover, the "for ___" tag, and the wish message
  letterBody: [ ... ],     // one string per paragraph
  letterSign: "love, me",
  art: { cover:"", cake:"", flame:"" }
};
```

### The cover photo

`art.cover` takes an image as a base64 data URI, so the photo travels inside the file and there's nothing extra to host:

```js
art: { cover: "data:image/jpeg;base64,/9j/4AAQSkZJRg...", cake:"", flame:"" }
```

To convert a photo, search for any "image to base64" converter, paste the whole result string in, and keep the quotes. A photo around 800px on its long side is plenty — anything bigger just makes the file slow to load.

There's also an **add cover photo** button under the card. That's a local preview only; it doesn't save into the file.

### Optional: your own painted art

`art.cake` and `art.flame` accept data URIs too. If you use them, the cake image needs the flames erased, and the flame needs to be its own transparent PNG — the flames are separate elements so they can bend and blow out.

## How the blowing works

The Web Audio API reads the mic, weights the low frequencies (blowing is a low rumble, not a tone), and counts sustained level above a threshold. Half a second of that and the candles go out. If the mic is blocked or unavailable, press and hold the "blow the candles" label, or hold the spacebar.
