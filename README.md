# gif-generator

A browser-based GIF maker. Drop images or a video into the page, arrange the frames, and export an animated GIF.

**Open it:** https://ibagaturiya.github.io/gif-generator/

- **Images and video:** drop, paste (⌘V / Ctrl+V) or choose files. Images are sorted by file name. Video frames are pulled out in the browser at the frame rate you pick, with an optional time range.
- **Filmstrip:** an overview of the whole loop (frame widths by duration) with a playhead; click or drag it to scrub. Below it, drag frames to reorder, × to remove, set each frame's duration in ms.
- **Length:** set how long one loop lasts; every frame's duration is scaled to match.
- **Boomerang:** plays the frames forward, then backward, without repeating the first and last frame.
- **Place into layout:** load a PNG or PDF with a transparent opening. A PDF is converted in the browser with [pdf.js](https://github.com/mozilla/pdf.js) (page 1, at 177 dpi: A3 → 2070×2929 px); areas with nothing on them stay transparent, so leave the opening empty instead of filling it white. The layout sits on top of the GIF, so title, name and logo stay visible. Drag the preview to move the GIF, drag its corners or scroll to resize. The export is the full layout, animated.
- **Crop:** double-click the preview (or press *crop*) to move and zoom the picture inside its frame; with a layout, drag the frame's edges to crop them. Double-click again or Esc to finish. Works with and without a layout.
- **Export:** GIF only, encoded in the browser with [gif.js](https://github.com/jnordberg/gif.js).

Everything runs locally in your browser; files are not uploaded anywhere. It is a single `index.html` with no build step; open it from disk or from GitHub Pages. Export and PDF layouts need internet to load gif.js and pdf.js from jsDelivr.

## Quality settings

Constants at the top of the script in `index.html`:

| Constant | Default | Meaning |
|---|---|---|
| `MAX_WIDTH` | 480 | export width in px |
| `COLORS` | 32 | palette size (2–256), one palette for all frames |
| `DITHER` | false | `true` for Floyd–Steinberg, or `'Atkinson'`, `'Stucki'`, `'FalseFloydSteinberg'` |

## License

- **Code:** © 2026 Ivan Bagaturiya, licensed under the [GNU Affero General Public License v3.0 or later](LICENSE).
- **gif.js** (MIT) and **pdf.js** (Apache-2.0), loaded from jsDelivr, are under their own licenses.
