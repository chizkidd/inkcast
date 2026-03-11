# Inkcast 🎙️

A lightweight, privacy-first epub and PDF audiobook player that runs entirely in your browser — no server, no account, no uploads. Built for iPhone but works anywhere.

---

## Features

- **Drop any `.epub` or `.pdf`** and start listening immediately
- **Chapter / page navigation** with a slide-out sidebar
  - EPUBs use the table of contents for chapter titles
  - PDFs use bookmarks/outline when available, or smart page grouping as fallback
- **Speed control** — 0.75× to 2×
- **Resume where you left off** — per book, stored locally
- **Voice picker** — uses your device's built-in text-to-speech voices
- **iOS Home Screen app** — works offline after first load
- **iOS Shortcut** — open Inkcast directly from your share sheet or home screen
- 100% on-device. Your books never leave your phone.

---

## Quickstart

### Option A — Use it right now (no install)

If this repo has GitHub Pages enabled, visit:

```
https://<your-username>.github.io/inkcast/
```

Open that URL in Safari on your iPhone, tap **Share → Add to Home Screen**.

### Option B — Host it yourself (2 minutes)

```bash
git clone https://github.com/<your-username>/inkcast.git
cd inkcast
# Open index.html in any browser, or serve it:
npx serve .
```

No build step. No dependencies. It's one HTML file.

---

## GitHub Pages Setup

1. Go to your repo **Settings → Pages**
2. Set Source to `main` branch, `/ (root)` folder
3. Save — your site will be live at `https://<your-username>.github.io/inkcast/`

---

## iOS Shortcut

The shortcut opens Inkcast in Safari with one tap (or via the share sheet).

### Install

1. Open the **Shortcuts** app on your iPhone
2. Tap **+** to create a new shortcut
3. Add these actions in order:

```
1. [Open URLs]
   URL: https://<your-username>.github.io/inkcast/

2. [Wait]
   1 second

3. [Show Result]  ← optional, remove if you want it silent
   "Inkcast opened"
```

4. Tap the shortcut name at the top → rename it **"Inkcast"**
5. Tap the icon → pick 🎙️ or 📖
6. Tap **Done**

Add it to your Home Screen via **Share → Add to Home Screen** from inside Shortcuts, or run it from the Shortcuts widget.

See [`docs/shortcut-setup.md`](docs/shortcut-setup.md) for detailed instructions including Siri launch and Lock Screen setup.

---

## File structure

```
inkcast/
├── index.html              # The entire app (self-contained)
├── README.md
├── LICENSE
├── .gitignore
├── docs/
│   └── shortcut-setup.md   # Detailed iOS shortcut instructions
│   └── index.html
└── .github/
    └── FUNDING.yml
```

---

## How it works

- **EPUB parsing** uses [JSZip](https://stuk.github.io/jszip/) to unzip the epub in-browser, reads `META-INF/container.xml` to find the OPF manifest, then extracts spine items in reading order. Chapter titles come from the NCX table of contents (EPUB2) or `nav.xhtml` (EPUB3).
- **PDF parsing** uses [PDF.js](https://mozilla.github.io/pdf.js/) to extract text page by page. If the PDF has a bookmark outline, those become chapter sections. Otherwise pages are grouped into sensible chunks automatically.
- **Text-to-speech** uses the Web Speech API (`SpeechSynthesisUtterance`), built into Safari, Chrome, Firefox, and Edge — no external API needed.
- **Resume** is stored in `localStorage` keyed by filename + filesize, so it works per-book automatically.

> Note: scanned PDFs (image-only, no text layer) won't have readable text. Most ebooks and modern documents work fine.

---

## Browser support

| Browser | Works | Notes |
|---|---|---|
| Safari (iOS) | ✅ | Best experience, add to Home Screen |
| Safari (macOS) | ✅ | |
| Chrome (Android/Desktop) | ✅ | |
| Firefox | ✅ | |
| Samsung Internet | ✅ | |

---

## Roadmap (Next Steps)

- [ ] Swap to ElevenLabs/OpenAI/Google Cloud TTS API
- [ ] Bookmarks within chapters
- [ ] Sleep timer
- [ ] Font size / reading view toggle
- [ ] PWA manifest for better installability
- [ ] Password-protected PDF support
- [ ] Inkcast Pro (premium features)

---

## Contributing

PRs welcome. Open an issue first for big changes.

---

## License

MIT — do whatever you want with it.
