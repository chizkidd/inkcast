# Inkcast 🎙️

A lightweight, privacy-first epub and PDF audiobook player that runs entirely in your browser — no server, no account, no uploads. Built for iPhone but works anywhere.

---

## Features

- **Drop any `.epub` or `.pdf`** and start listening immediately
- **Chapter / page navigation** with a slide-out sidebar
  - EPUBs use the table of contents for chapter titles
  - PDFs use bookmarks/outline when available, or smart page grouping as fallback
- **Speed control** — 0.75× to 2× (remembered across sessions)
- **Resume where you left off** — per book, stored locally
- **Smart voice selector** — organized by region (US, UK, AU) with named voices like Samantha, Daniel, Karen, Siri Voice 1/2. Greys out voices not installed on your device. Remembers your choice.
- **Voice quality guide** — built-in tip showing exactly where to download better voices on iOS
- **OpenAI TTS ready** — a drop-in code hook is already in the source for when you want to upgrade to podcast-quality voices
- **iOS Home Screen app** — add to Home Screen for an app-like experience
- **iOS Shortcut** — open Inkcast directly from your home screen or via Siri
- 100% on-device. Your books never leave your phone.

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
- **Siri Voice 1 or 2** — most natural, best for long-form listening
- **Daniel** (UK Male) — excellent for fiction
- **Karen** (AU Female) — clear and warm

Downloaded voices appear automatically in Inkcast's voice selector.

---

## Upgrading to OpenAI TTS

When you want podcast-quality voices, the upgrade path is already stubbed in the code. Search for `TODO: UPGRADE TO OPENAI TTS` in `docs/index.html` for a full drop-in replacement including chunking and all voice options.

Available voices: `onyx` (deep male), `nova` (warm female), `shimmer` (expressive female), `alloy`, `echo`, `fable`.

---

## How it works

- **EPUB parsing** — JSZip unpacks the file in-browser. Chapter titles come from the NCX (EPUB2) or `nav.xhtml` (EPUB3).
- **PDF parsing** — PDF.js extracts text page by page. Bookmark outlines become chapter sections; otherwise pages are grouped automatically.
- **Text-to-speech** — Web Speech API (`SpeechSynthesisUtterance`), built into Safari, Chrome, Firefox, and Edge. No external API needed.
- **Voice selection** — matches installed voices against a curated list by region. Preference saved in `localStorage`.
- **Resume & speed** — stored in `localStorage` keyed by filename + filesize per book. Speed persists globally.

> Scanned PDFs (image-only, no text layer) won't have readable text. Most ebooks and modern PDFs work fine.

---

## File structure

```
inkcast/
├── docs/
│   ├── index.html          # The entire app (self-contained)
│   ├── shortcut-setup.md   # Detailed iOS shortcut instructions
│   ├── robots.txt          # SEO — tells Google to index the site
│   ├── sitemap.xml         # SEO — canonical URL for Google
│   └── 404.html            # Custom not-found page with auto-redirect
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

MIT — do whatever you want with it.