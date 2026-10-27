# Clip Recipe

Drop a video or image and see how it was made. ComfyUI and RunningHub files give the full recipe: the prompt, seed, model and LoRAs, steps, CFG, resolution, length and the reference images it used, and you can copy the prompt or the whole workflow to rebuild it. Files from other AI tools show whatever they carry: Content Credentials, China's AIGC label, CapCut export info, or the prompt and settings image generators save. Runs in your browser; nothing is uploaded.

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

## Files from other AI tools

Most other tools don't save a recipe, but many leave a label. Clip Recipe reads these:

| What | Found in | What it shows |
|---|---|---|
| **Content Credentials (C2PA)** | Grok Imagine, Google (Gemini / Omni / Veo), OpenAI, Adobe Firefly and others | Which app made it, the company that signed it, whether it's AI-generated, a time stamp, the edit history (for example "Added imperceptible SynthID watermark") and whether it was made from an input file |
| **AIGC label** (China, GB 45438-2025) | RunningHub clips, and Chinese AI services such as Seedance, Kling and Hailuo when downloaded from their own apps | The AI-generated flag, the service's registration code and the content ID |
| **CapCut export info** | Videos exported from CapCut | Desktop or phone, the project ID, and which CapCut AI features were used in the edit |
| **Image generator text** | AUTOMATIC1111 / Forge, Fooocus, NovelAI, InvokeAI, Midjourney | Prompt, negative prompt, seed, steps, sampler, model and other settings |
| **XMP and other tags** | Anything | Every readable tag left in the file, so you can tell "nothing there" from "something there" |

Tested on real files: ComfyUI, RunningHub (recipe and AIGC label), Grok Imagine videos and images, Google Omni videos, CapCut exports. The image-generator readers follow those tools' published formats.

Some things can't be read: invisible watermarks hidden in the picture itself (such as Google's SynthID), and labels that were stripped when a file was re-saved, edited or sent through some APIs. Clip Recipe reads Content Credentials but doesn't verify their signatures; use [contentcredentials.org/verify](https://contentcredentials.org/verify) for that.

## Supported files

| File | Where it comes from |
|---|---|
| `.mp4` / `.mov` | ComfyUI SaveVideo, Video Helper Suite (VHS) Video Combine, RunningHub downloads, and videos from other AI tools |
| `.png` / `.jpg` / `.webp` | ComfyUI Save Image, and images from other AI tools |
| `.json` | ComfyUI workflow files (UI or API format) |

You can drop several files at once. Each one shows as a preview in the drop box (videos play when you hover). Click a preview to see its recipe, or click its × to remove it.

## Matching reference images

RunningHub renames every uploaded image to a fingerprint of its contents (a SHA-256 hash), so a downloaded clip lists references as long strings like `6c887145…23ea.jpeg`.

Each reference in the **References** section has its own tile. Drop the image you think you used on that tile, or click the tile to choose it. Clip Recipe fingerprints your file in the browser and shows:

- **✓ Match**: the exact file the clip used, byte for byte
- **✗ Not the same file**: a different image, or an edited or re-saved copy (so you know the wrong version was uploaded)

Click the small × on a tile to clear it and try another file.

Local ComfyUI runs keep the original filenames instead of fingerprints, so for those the tile compares by name and notes that the exact version can't be proven.

## Limits

- For a recipe, the file has to come straight out of ComfyUI or RunningHub. Clips that were re-exported from an editor, re-encoded, or uploaded to a social site lose the embedded workflow.
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
