# gif-generator

A browser-based GIF maker. Drop images, a folder, a ZIP or a video into the page, arrange the frames, and export an animated GIF.

**Open it:** https://ibagaturiya.github.io/gif-generator/

- **Example:** on opening, a ball falls in 10 frames, from the top down to a squash on the ground, drawn in code on a transparent background. Boomerang is on, so it bounces back up; turn it off to see why it's there (the ball jumps back to the top). Add your own frames and it is replaced (boomerang goes off with it).
- **Images and video:** drop, paste (⌘V / Ctrl+V) or choose files. Images are sorted by file name.
- **Folders and ZIPs:** drop a whole folder (subfolders included), or add a `.zip`; it is unpacked in the browser by its own reader (no library). Files are sorted by their path; hidden files and `__MACOSX` are skipped. Video frames are pulled out in the browser at the frame rate you pick, with an optional time range.
- **Filmstrip:** an overview of the whole loop (frame widths by duration) with a playhead; click or drag it to scrub. Below it, drag frames to reorder, × to remove, set each frame's duration in ms.
- **Timing:** in the filmstrip header: *Each frame* in ms or fps (GIFs count in 10 ms steps, so 24 fps becomes 25) sets every frame; *Total* stretches all frames to a length. Both apply right away.
- **Timing curve:** under the overview, one dot under each frame (hollow dots: the boomerang's way back), height = duration. Drag up and down to draw the durations; click a dot to select its frame, shift-click for a range, then drawing only changes the selected frames. Right-click or ⋯ on the curve: ease in, ease out, ease in & out, even (same loop length), select all.
- **Range:** shift-click frames to select a range (⌘/Ctrl-click adds one); reverse, remove every 2nd, double, ease, frame duration and Del then work on that range only. Esc clears it.
- **Onion skin:** shows the previous and next frame faintly in the preview, to check the spacing. **Fade:** the first and last frames blend from and to the background.
- **Color:** make a color see-through (e.g. a white background; *Similar* takes close shades too), black & white, contrast, posterize.
- **First steps:** on the first visit the screen darkens, three steps (Add, Length, Export) stay lit with a numbered label and a short arrow each, and a card explains them; pointing at a line in the card lights up only that control; "More" adds frames, layout, layers and the rest; the **?** button next to ⋯ shows them again. Click anywhere or Esc to close.
- **Properties (left) and Layers (right):** foldable side panels. Properties holds Background (transparent, color or image, opacity), Color (remove a color, filters) and Text & images (the selected overlay, with "Shows on: All frames / Only frame N" right under the text). Layers lists everything top to bottom: text and image overlays, the layout, the frames, the background. Each row has a small preview. Drag rows to reorder (e.g. an opaque layout behind the frames), 👁 to hide a layer in preview and export.
- **Dropping files:** with frames already there, the drop area splits: left adds the files as frames, right adds images as layers on top.
- **Text and images:** *+ Add* → Text or Image puts an overlay on the GIF. Drag it, scroll over it to resize, or set X / Y / size in px of the export. Right-click: on every frame or only this frame, duplicate, delete. Fonts: system fonts, ES Klarheit if installed, or your own font file.
- **GIF size:** the resolution is shown under the preview's bottom right corner; with the aspect ratio below it. Click it to set width and height (the chain keeps the aspect ratio; unlinked, the GIF is stretched), or type an aspect ratio (16:9, 1:1, 1.85); leave the width empty for the automatic size.
- **Boomerang:** plays the frames forward, then backward, without repeating the first and last frame.
- **Settings next to their controls:** layout settings open under the Layout toggle (when turning it on, or right-click it); frame tools (reverse, remove every 2nd, double each, fade, onion skin) open from the ⋯ in the filmstrip header or a right-click on a frame; export settings on a right-click of Export.
- **Place into layout:** pick a template (A4 or square, white page with today's date in the bottom right corner; switching Layout on starts with A4), or load your own PNG or PDF with a transparent opening. A PDF is converted in the browser with [pdf.js](https://github.com/mozilla/pdf.js) (page 1, at 177 dpi: A3 → 2070×2929 px); areas with nothing on them stay transparent, so leave the opening empty instead of filling it white. The layout sits on top of the GIF, so title, name and logo stay visible. Drag the preview to move the GIF, drag its corners or scroll to resize. The export is the full layout, animated.
- **Crop:** double-click the preview: the view zooms out, everything outside the frame is dimmed, bold corners mark the frame, a thirds grid shows while dragging. Drag to move the picture, scroll to zoom; with a layout, drag the frame's edges. *Done*, double-click or Esc to finish; *Reset* in the bar on top.
- **Background:** transparent by default, shown as a grey and white checkerboard; the GIF is then exported with a transparent background (every frame stored whole, since GIF can't otherwise clear pixels). Or pick a color, or an image that fills the whole GIF. *Opacity* lets the color or image show through the frames (not with a transparent background: GIF pixels are solid or see-through). Properties → Background, or click the Background row in Layers.
- **Export:** GIF, encoded in the browser by its own encoder (no library). Quality: right-click Export. The menu lists only options that really give a smaller file (Full quality, Balanced, Smaller, Smallest), each with its size; point at one to see the shown frame in that quality. By default the best quality under 15 MB is used. It aims for the best quality within that budget: the layout is stored once at full resolution, and every later frame stores only the pixels that changed, inside the GIF's frame. Before encoding, a few sample frames are test-encoded to pick the settings. The same estimate runs in the background and shows the expected file size on the Export button.

Everything runs locally in your browser; files are not uploaded anywhere. It is a single `index.html` with no build step; open it from disk or from GitHub Pages. PDF layouts need internet to load pdf.js from jsDelivr; everything else works offline.

## Quality settings

Constants at the top of the script in `index.html`:

| Constant | Default | Meaning |
|---|---|---|
| `QCANDS`, `AUTO_BYTES` | ladder steps 0, 2, 5, 7 · 15 MB | quality options (right-click Export) and the automatic budget |
| `MAX_WIDTH` | 2070 | export width in px (A3 at 177 dpi) |
| `COLORS` | 255 | most colors, one palette for all frames |
| `DITHER` | true | ordered dithering (smooth gradients, compresses well, no flicker) |
| `PDF_DPI` | 177 | resolution PDF layouts are rendered at |

When a GIF would be too big, `LADDER` lists the steps the encoder goes down, best quality first: fewer colors, a tolerance for pixels that barely change, the moving picture at lower resolution (the layout always stays sharp), then as a last resort every 2nd or 3rd frame (the loop keeps its length) and a smaller GIF. The export message says which step was used.

## License

- **Code:** © 2026 Ivan Bagaturiya, licensed under the [GNU Affero General Public License v3.0 or later](LICENSE).
- **pdf.js** (Apache-2.0), loaded from jsDelivr, is under its own license.
