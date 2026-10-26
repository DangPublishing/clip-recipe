# Clip Recipe

Drop a video or image from ComfyUI or RunningHub and see how it was made: the prompt, seed, model and LoRAs, steps, CFG, resolution, length and the reference images it used. Copy the prompt or the full workflow to rebuild it. Runs in your browser; nothing is uploaded.

**Open the tool:** https://dangpublishing.github.io/clip-recipe/

## What it reads

ComfyUI (and RunningHub, which runs ComfyUI) saves the whole workflow inside the files it renders. Clip Recipe opens that hidden data and lays it out:

- **Prompt**: every text prompt in the graph, with a copy button
- **Seed**: the seed that was actually used, even on a "randomize" run, with a copy button
- **Models**: diffusion model or checkpoint, LoRAs with their strength, text encoder, VAE, upscalers
- **Sampling**: steps, CFG, sampler, scheduler, denoise, shift and similar settings
- **Canvas**: width, height, frame count, frame rate and duration, measured from the video itself
- **References**: the images, audio and video files the workflow loaded
- **Workflow**: copy the full workflow JSON, or save it as a `.json` file, and load it back into ComfyUI

## Supported files

| File | Where it comes from |
|---|---|
| `.mp4` / `.mov` | ComfyUI SaveVideo, Video Helper Suite (VHS) Video Combine, RunningHub downloads |
| `.png` | ComfyUI Save Image |
| `.json` | ComfyUI workflow files (UI or API format) |

You can drop several files at once and switch between them with the tabs.

## Matching reference images

RunningHub renames every uploaded image to a fingerprint of its contents (a SHA-256 hash), so a downloaded clip lists references as long strings like `6c887145…23ea.jpeg`. Drop the images you think you used into **Check reference images**. Clip Recipe fingerprints them in the browser and tells you which file matches each reference, byte for byte. An edited or re-saved copy will not match, which also tells you the wrong version was uploaded.

Local ComfyUI runs keep the original filenames, so those show by name.

## Limits

- The file has to come straight out of ComfyUI or RunningHub. Clips that were re-exported from an editor, re-encoded, or uploaded to a social site lose the embedded workflow.
- The workflow is a recipe, not a guarantee. Rendering it again on different hardware, or a different version of ComfyUI or its custom nodes, can give a different result even with the same seed.
- Values the graph works out while it runs (for example a size picked by a resolution node) are not stored in the file. Clip Recipe reads the real size and length from the video instead.

## Privacy

Everything happens in your browser tab. Files are never uploaded, and there is no server, account or tracking.

## Run it yourself

It is a single `index.html` file with no build step. Download it and open it in a browser, or host it anywhere that serves static files (GitHub Pages works).

## License

MIT. See [LICENSE](LICENSE). Free to use, copy and modify, including the example prompt built into the page.

## More free tools from Dang Publishing

- [Clip Compare](https://dangpublishing.github.io/video-compare/): A/B video comparison with wipe, side-by-side and flip
- [ABC Score Viewer](https://dangpublishing.github.io/abc-viewer/): turn ABC notation into sheet music you can read and print
