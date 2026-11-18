# gif-generator

A browser-based GIF maker. Drop images, a folder, a ZIP or a video into the page, arrange the frames, and export an animated GIF.

**Open it:** https://ibagaturiya.github.io/gif-generator/

- **Example:** on opening, a ball falls in 5 frames, from the top down to a squash on the ground, drawn in code on a transparent background. Boomerang is on, so it bounces back up; turn it off to see why it's there (the ball jumps back to the top). Add your own frames and it is replaced (boomerang goes off with it).
- **Images and video:** drop, paste (⌘V / Ctrl+V) or choose files. Images are sorted by file name.
- **Folders and ZIPs:** drop a whole folder (subfolders included) or choose one, or add a `.zip`; it is unpacked in the browser by its own reader (no library). Files are sorted by their path; hidden files and `__MACOSX` are skipped. Video frames are pulled out in the browser at the frame rate you pick, with an optional time range.
- **Filmstrip:** an overview of the whole loop (frame widths by duration) with a playhead; click or drag it to scrub. Below it, drag frames to reorder, × to remove, set each frame's duration in ms.
- **Timing:** in the filmstrip header: *Each frame* in ms or fps (GIFs count in 10 ms steps, so 24 fps becomes 25) sets every frame; *Whole loop* stretches all frames to a length. Both apply right away.
- **Boomerang:** plays the frames forward, then backward, without repeating the first and last frame.
- **Place into layout:** load a PNG or PDF with a transparent opening. A PDF is converted in the browser with [pdf.js](https://github.com/mozilla/pdf.js) (page 1, at 177 dpi: A3 → 2070×2929 px); areas with nothing on them stay transparent, so leave the opening empty instead of filling it white. The layout sits on top of the GIF, so title, name and logo stay visible. Drag the preview to move the GIF, drag its corners or scroll to resize. The export is the full layout, animated.
- **Crop:** double-click the preview (or press *crop*) to move and zoom the picture inside its frame; with a layout, drag the frame's edges to crop them. Double-click again or Esc to finish. Works with and without a layout.
- **Background:** transparent by default, shown as a grey and white checkerboard; the GIF is then exported with a transparent background (every frame stored whole, since GIF can't otherwise clear pixels). Or pick a color, or an image that fills the whole GIF. *Opacity* lets the color or image show through the frames (not with a transparent background: GIF pixels are solid or see-through). Settings → Picture.
- **Export:** GIF, encoded in the browser by its own encoder (no library). It aims for the best quality under 15 MB: the layout is stored once at full resolution, and every later frame stores only the pixels that changed, inside the GIF's frame. Before encoding, a few sample frames are test-encoded to pick the settings. The same estimate runs in the background and shows the expected file size on the Export button.

Everything runs locally in your browser; files are not uploaded anywhere. It is a single `index.html` with no build step; open it from disk or from GitHub Pages. PDF layouts need internet to load pdf.js from jsDelivr; everything else works offline.

## Quality settings

Constants at the top of the script in `index.html`:

| Constant | Default | Meaning |
|---|---|---|
| `MAX_BYTES` | 15e6 | size budget, 15 MB |
| `MAX_WIDTH` | 2070 | export width in px (A3 at 177 dpi) |
| `COLORS` | 255 | most colors, one palette for all frames |
| `DITHER` | true | ordered dithering (smooth gradients, compresses well, no flicker) |
| `PDF_DPI` | 177 | resolution PDF layouts are rendered at |

When a GIF would be too big, `LADDER` lists the steps the encoder goes down, best quality first: fewer colors, a tolerance for pixels that barely change, the moving picture at lower resolution (the layout always stays sharp), then as a last resort every 2nd or 3rd frame (the loop keeps its length) and a smaller GIF. The export message says which step was used.

## License

- **Code:** © 2026 Ivan Bagaturiya, licensed under the [GNU Affero General Public License v3.0 or later](LICENSE).
- **pdf.js** (Apache-2.0), loaded from jsDelivr, is under its own license.
