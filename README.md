# gif-generator

A browser-based GIF maker. Drop images or a video into the page, arrange the frames, and export an animated GIF.

**Open it:** https://ibagaturiya.github.io/gif-generator/

- **Images and video:** drop, paste (⌘V / Ctrl+V) or choose files. Images are sorted by file name. Video frames are pulled out in the browser at the frame rate you pick, with an optional time range.
- **Filmstrip:** drag frames to reorder, × to remove, set each frame's duration in ms.
- **Boomerang:** plays the frames forward, then backward, without repeating the first and last frame.
- **Place into layout:** load a PNG with a transparent opening. The layout sits on top of the GIF, so title, name and logo stay visible. Drag the preview to move the GIF, drag its corners or scroll to resize. The export is the full layout, animated.
- **Export:** GIF only, encoded in the browser with [gif.js](https://github.com/jnordberg/gif.js).

Everything runs locally in your browser; files are not uploaded anywhere. It is a single `index.html` with no build step; open it from disk or from GitHub Pages. Export needs internet once to load gif.js from jsDelivr.

## Quality settings

Constants at the top of the script in `index.html`:

| Constant | Default | Meaning |
|---|---|---|
| `MAX_WIDTH` | 480 | export width in px |
| `COLORS` | 32 | palette size (2–256), one palette for all frames |
| `DITHER` | false | `true` for Floyd–Steinberg, or `'Atkinson'`, `'Stucki'`, `'FalseFloydSteinberg'` |

## License

- **Code:** © 2026 Ivan Bagaturiya, licensed under the [GNU Affero General Public License v3.0 or later](LICENSE).
- **gif.js** (loaded from jsDelivr) is under its own MIT license.
