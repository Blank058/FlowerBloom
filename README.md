# A flower, for him

**Live:** https://blank058.github.io/FlowerBloom/

A single-page web app: a bud opens into a flower, and a few words appear underneath.
No build step, no dependencies, no internet needed — one file you can open by double-clicking.

```bash
open index.html
```

## Making it yours

Everything personal lives in one `CONFIG` object near the bottom of [index.html](index.html) —
scroll to `EDIT ME`:

```js
const CONFIG = {
  name:  "",     // his name → shows as "For Sam"; leave blank for "For you"
  from:  "",     // your name, appended to the last line
  lines: [ ... ] // the main verse, one string per line
  note:  "...",  // the quieter italic thought
  closing: "..." // the small-caps last line
};
```

Each entry in `lines` is its own line on screen, so break them where you'd pause if you
were saying it out loud. Three or four lines feels right; more and the flower gets crowded.

You can also set the name without touching the code, which is handy if you want one file
for more than one person:

```
index.html?name=Sam
```

## Sending it to him

Send him the link: **https://blank058.github.io/FlowerBloom/**

Or attach `index.html` directly — it's self-contained, so it works offline with no host at all.

### Publishing an edit

Pages rebuilds from `main` on every push, so updating the words is three commands and
about a minute's wait:

```bash
git commit -am "Update the words" && git push
```

## How the bloom is put together

The flower is one inline SVG. The petals are 22 copies of a single path, rotated around the
flower's heart and animated from `scale(.04)` outward on staggered delays, so the bloom
travels from the outer ring inward. The stem draws itself with `stroke-dashoffset`, the
leaves unfurl from the point where they meet it, and a `sway` animation starts once
everything has opened.

The whole sequence is driven by one `bloomed` class on `<body>` — the flower, the words, and
the buttons all read from that single class, which is why "Again" can restart everything by
removing it and adding it back.

`prefers-reduced-motion` is respected: the page arrives at exactly the same final state
without the travel.

## Files

| File | |
|---|---|
| `index.html` | the whole app — markup, styles, script |
| `.claude/launch.json` | local preview server config (`python3 -m http.server 4321`); not needed to run the page |
