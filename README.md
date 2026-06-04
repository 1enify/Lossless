# Echo Music Canvas

Implementing a new way to get beautiful custom canvas background videos for the **Echo Music** app!

This repository acts as the central hub for mapping custom `.m3u8` or `.mp4` background visualizers to specific songs or albums within the Echo Music client. Because it is optimized for Vercel/GitHub Pages, any changes you push to this repository are instantly deployed and served via a global CDN.

---

## How to Add a New Canvas

If you find a cool vertical visualizer or music video clip and want it to display as a dynamic canvas background in Echo Music whenever a specific song plays, follow these steps:

### 1. Upload your Video File
Add your video file into either the `Song/` or `Album/` directories within this repository.
* **Format:** `.m3u8` or `.mp4`
* **Example:** `Song/dracula_visualizer.mp4`

### 2. Update `canvas.json`
Open the `canvas.json` file located in the root of the repository. Add a new item block mapping the exact song name and artist to your new video URL.

Make sure your URL points to your deployed Vercel domain!

**Example entry:**
```json
{
  "items": [
    {
      "song": "Song Title",
      "artist": "Artist Name",
      "url": "https://echomusicanvas.vercel.app/Song/your_video.mp4"
    }
  ]
}
```

### 3. Commit and Push
Once you have uploaded your video and updated `canvas.json`, commit your changes and push them to your repository fork or submit a Pull Request.

> [!IMPORTANT]
> When opening a **Pull Request**, please include the **original song/album link** (YouTube Music, Spotify, or similar) in the description. This helps verify metadata and ensure the canvas matches the correct track.

**Pull Request Example:**
> **Title:** `feat: added canvas for Blinding Lights by The Weeknd`
> **Description:**
> - Added `Song/blinding_lights.mp4`
> - Updated `canvas.json` mapping for "Blinding Lights"
> - **Original Link:** https://music.youtube.com/watch?v=4NRXx6U8ABQ

```bash
git add .
git commit -m "feat: added canvas for Song Title"
git push origin main
```

Your changes will be verified and deployed. Once active, enable **"Enable Canvas"** under **Settings -> Playback Settings** in the Echo Music app, play the song, and watch the visualizer loop!

---

## Continuous Integration

To ensure the integrity of `canvas.json` and prevent broken links, we run an automated **Validation Bot** on every Pull Request:

1. **JSON Syntax**: Ensures the file is correctly formatted JSON.
2. **Schema Check**: Verifies that `song`, `artist`, and `url` fields are present for every entry.
3. **Local File Check**: Verifies that the video file referenced in the URL actually exists in the local `Song/` or `Album/` directories.
4. **No Duplicates**: Ensures that no two entries have the same (song, artist) combination.
5. **Format Check**: Ensures URLs end in `.mp4` or `.m3u8`.

You can run this validation locally prior to committing:
```bash
node scripts/validate_canvas.js
```

---

## License

This project is licensed under the **GNU General Public License v3.0**. See the [LICENSE](LICENSE) file for details.
