# Inkcast 🎙️

A lightweight, privacy-first audiobook player that runs entirely in your browser. Drop in an epub or PDF, paste any article URL, and start listening immediately; no installs needed, no account required, no files ever leave your device. Built for iPhone but works anywhere.

---

## Features

- **Drop any `.epub` or `.pdf`** and start listening immediately
  - EPUB footnotes and endnotes are automatically stripped so they don't interrupt the reading
- **Paste any URL**: listen to articles, essays, and blog posts from any webpage
  - Index pages (e.g. `paulgraham.com/articles.html`) load all articles into the sidebar so you can tap any one to play
  - Strips ads, navigation, and clutter automatically
- **Chapter / page navigation** with a slide-out sidebar
- **Estimated listen time** shown per chapter alongside word count
- **Speed control**: 0.75× to 2× (remembered across sessions)
- **Resume where you left off**: per book, stored locally
- **Smart voice selector**: organized by region (US, UK, AU). Greys out voices not installed on your device. Remembers your choice.
- **iOS Home Screen app**: add to Home Screen for an app-like experience
- **iOS Shortcut**: open Inkcast directly from your home screen or via Siri
- Your books and files never leave your device.

---

## Live App

**[chizkidd.github.io/inkcast](https://chizkidd.github.io/inkcast/)**

Open in Safari on iPhone → Share → Add to Home Screen for the best experience.

---

## Self-hosting (2 minutes)

```bash
git clone https://github.com/chizkidd/inkcast.git
cd inkcast
# Open docs/index.html in any browser, or serve locally:
npx serve docs
```

No build step. No dependencies. The entire app is one HTML file in `docs/`.

---

## iOS Shortcut

Say "Hey Siri, Inkcast" or tap a home screen icon to open it instantly.

1. Open the **Shortcuts** app → tap **+**
2. Add action: **Open URLs** → `https://chizkidd.github.io/inkcast/`
3. Rename to **Inkcast** → pick an icon → tap **Done**
4. Long-press the shortcut → **Add to Home Screen**

See [`docs/shortcut-setup.md`](docs/shortcut-setup.md) for Lock Screen and Siri setup.

---

## Improving voice quality (free)

The default system voices can sound robotic. On iPhone:

**Settings → Accessibility → Spoken Content → Voices → English**

Recommended downloads:
- **Siri Voice 1 or 2**: most natural, best for long-form listening
- **Daniel** (UK Male): excellent for fiction
- **Karen** (AU Female): clear and warm

Downloaded voices appear automatically in Inkcast's voice selector.

---

## Upgrading to OpenAI TTS

When you want podcast-quality voices, the upgrade path is already stubbed in the code. Search for `TODO: UPGRADE TO OPENAI TTS` in `docs/index.html` for a full drop-in replacement including chunking and all voice options.

Available voices: `onyx` (deep male), `nova` (warm female), `shimmer` (expressive female), `alloy`, `echo`, `fable`.

---

## How it works

- **EPUB parsing**: JSZip unpacks the file in-browser. Chapter titles come from the NCX (EPUB2) or `nav.xhtml` (EPUB3).
- **PDF parsing**: PDF.js extracts text page by page. Bookmark outlines become chapters; otherwise pages are grouped automatically.
- **URL fetching**: a Cloudflare Worker fetches pages server-side to bypass CORS. The HTML is cleaned in the browser. Index pages populate the sidebar TOC automatically; articles load on demand when tapped.
- **Text-to-speech**: Web Speech API, built into Safari, Chrome, Firefox, and Edge. No external API needed.
- **Voice selection**: matches installed voices against a curated list by region. Preference saved in `localStorage`.
- **Resume & speed**: stored in `localStorage` per book. Speed persists globally.

> Scanned PDFs (image-only, no text layer) won't work. Most ebooks and modern PDFs are fine.

---

## File structure

```
inkcast/
├── docs/
│   ├── index.html          # The entire app
│   ├── shortcut-setup.md   # iOS shortcut instructions
│   ├── robots.txt
│   ├── sitemap.xml
│   └── 404.html
├── .github/
│   └── FUNDING.yml
├── .gitignore
├── LICENSE
└── README.md
```

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

## Roadmap

- [ ] OpenAI TTS integration (premium voices)
- [ ] Bookmarks within chapters
- [ ] Sleep timer
- [ ] Font size / reading view toggle
- [ ] PWA manifest for better installability
- [ ] Password-protected PDF support

---

## Contributing

PRs welcome. Open an issue first for big changes.

---

## License

MIT