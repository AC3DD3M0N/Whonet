# Whonet
WHOnet — Windows Desktop App Setup Guide What This Does Runs fully offline from your local hard drive Plays your own video files directly Stores watch progress between sessions Opens like any other Windows app ---
Folder Structure (Required)
You must arrange your files exactly like this. Everything depends on these locations make sure all capitalization is the same. all episode numbering is copied from imdb if that helps when organizing your episodes
```
Whonet(PROTOTYPE)/                          ← This is your root folder │
├── WHOnet-electron/                  ← The app files (this folder, unzipped)
│   ├── electron/
│   │   └── main.js
│   ├── src/
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── index.html
│   ├── package.json
│   ├── vite.config.js
│   ├── setup.bat               ← Run this ONCE to install
│   └── start.bat               ← Run this every time to launch
│
└── media/                       ← Your media files go HERE
    ├── doctors/
    │   ├── ninth.png
    │   ├── tenth.png
    │   ├── eleventh.png
    │   ├── twelfth.png
    │   └── thirteenth.png
    ├── seasons/
    │   ├── season1/
    │   │   ├── s1e1.mp4
    │   │   ├── s1e2.mp4
    │   │   └── ... (continue for all episodes)
    │   ├── season2/
    │   │   ├── s2e0.mp4         ← Christmas special video
    │   │   ├── s2e1.mp4
    │   │   └── ...
    │   ├── season3/  season4/  season5/  season6/  season7/
    │   ├── season8/  season9/  season10/ season11/ season12/ season13/
    │   └── disney/
    │       ├── disney.jpg
    │       ├── specials.jpg
    │       ├── specials/
    │       │   ├── specialse1.mp4
    │       │   └── ...
    │       ├── season1/
    │       └── season2/
> \\\*\\\*Critical:\\\*\\\* The `media` folder must be \\\*\\\*next to\\\*\\\* (a sibling of)
the `WHOnet-electron` folder, not inside it.

\---

## Step 1 — Install Node.js

Node.js is a free tool that runs the app. You only install it once.

1. Go to **https://nodejs.org**
2. Click **"LTS"** (the recommended version, left button)
3. Download the `.msi` installer
4. Run the installer → click **Next** through everything → click **Install**
5. When it asks "Install additional tools" → **check the box** and click Install
6. Wait for it to finish (may take a few minutes)
7. Restart your computer

**To verify it worked:** Press `Win + R`, type `cmd`, press Enter. In the window, type:

```
node --version
```

You should see something like `v20.11.0`. If you do, Node.js is installed correctly.

\---

### Video Files

* Episode videos: `sXeY.mp4`
* Example: Season 1 Episode 3 → `s1e3.mp4`
* Example: Season 11 Episode 7 → `s11e7.mp4`
* Example: Christmas special → `s2e0.mp4`

### Supported Video Formats

Supported formats:

* **MP4 (H.264)** ← Recommended, works with everything
* **WebM (VP8/VP9)** ← Also works great
* MKV and AVI are **NO**W supported natively

\---

## Step 3 — Run Setup (One Time Only)

1. Open your `WHOnet/whonet-app/` folder in File Explorer
2. Double-click **`setup.bat`**
3. A black window will appear and start installing
4. Wait for it to say **"WHOnet is ready!"** (takes 1–5 minutes depending on internet speed)
5. The window will close automatically when done

**What setup.bat does:**

* Checks that Node.js is installed
* Downloads all the app dependencies (`npm install`)
* Builds the React app into fast static files (`npm run build`)

You only need to do this **once**. After that, just use `start.bat`.

\---

## Step 4 — Launch WHOnet

1. Double-click **`start.bat`**
2. A window titled "WHOnet" will open
3. Wait a few seconds for the intro animation
4. You're in!

> If you see a blue spinning light but the app never loads, close it, wait 5 seconds, and try again. This can happen on the first launch.

\---

## File Size Recommendations

|Quality|Resolution|Bitrate|Approx Size per Episode|
|-|-|-|-|
|HD|720p|2-4 Mbps|\~1-2 GB|
|Full HD|1080p|4-8 Mbps|\~2-4 GB|
|4K|2160p|15-25 Mbps|\~8-15 GB|

The app streams directly from your hard drive, so an SSD will give smoother playback.

\---

## Troubleshooting

### Shorts are too small

* go to your settings enable editing mode and you can grab the corner of the shorts and make it bigger and move it around



### The app opens but shows blank/black screen for images

Your media file isn't in the right location or has the wrong name. Check:

* The file is named exactly right (e.g. `s1\\\_03.jpg` not `s1\\\_3.jpg`)
* The `media` folder is **next to** `whonet-app`, not inside it
* The folder structure matches the guide above exactly

### "node is not recognized" error in setup.bat

Node.js isn't installed or didn't install properly:

1. Re-download and reinstall from https://nodejs.org
2. During install, make sure "Add to PATH" is checked
3. Restart your computer and try again

### setup.bat says "npm install failed"

* Check your internet connection
* Try running setup.bat again
* If it keeps failing, open cmd and navigate to `whonet-app` folder and run `npm install` manually

### App opens but is very small or very large

Right-click your desktop → Display Settings → Scale — try setting it to 100% or 125%.

### Watch history disappeared

The watch history is stored in your Windows user profile. It should persist between launches. If it gets reset, check that you're not running the app as a different user.

\---

### Image Files (thumbnails)\*only necesary if any are missing

* Season posters: `seasonX.jpg` (e.g. `season1.jpg`, `season8.jpg`)
* Episode images: `sX\\\\\\\_YY.jpg` with **leading zero** on episode number

  * Example: Season 1 Episode 3 → `s1\\\\\\\_03.jpg`
  * Example: Season 11 Episode 7 → `s11\\\\\\\_07.jpg`
  * Example: Christmas special (episode 0) → `s2\\\\\\\_00.jpg`

\---

## Set Up Your Media File(only if nothing comes up)

open your app settings and click browse and select your media file



\---

## Updating the App

If you receive an updated `App.jsx` file:

1. Replace `Whonet(PROTOTYPE)\\WHOnet-electron\\src/App.jsx` with the new file
2. Run `setup.bat` again (or just open cmd in whonet-app and run `npm run build`)
3. Launch with `start.bat` as normal

\---

## Adding More Media Later

You can add episodes at any time:

1. Drop the image and video files into the correct folder with the correct names
2. Launch the app — it will pick them up automatically (no rebuild needed)

\---

## Technical Details (for the curious)

The app is built with:

* **Electron** — wraps the web app into a desktop window
* **React + Vite** — the UI framework and build tool
* **Custom `media://` protocol** — Electron intercepts `media://` URLs and serves files from your local `media/` folder. This is how the app can play videos from your hard drive without any web server.
* **localStorage** — watch progress is saved in Electron's app data folder

