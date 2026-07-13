# DOCX Viewer

A fast, mobile-first, **single-file** Word document viewer. Drag & drop a
`.docx` and read it in your browser — headings, tables, lists, and images
rendered with formatting intact. It's a **viewer, not an editor** — no
toolbars, no accounts, no uploads. Everything runs locally in your browser.

🔗 **Live:** <https://docx-viewer.us/>

![Single file](https://img.shields.io/badge/build-single%20HTML%20file-success) ![No build step](https://img.shields.io/badge/build%20step-none-success) ![License](https://img.shields.io/badge/license-MIT-blue)

> Part of the **[File Viewer](https://file-viewer.us/) family** — HTML, Markdown,
> ePUB, PDF, Data, DOCX, and Sheets each have their own dedicated viewer. Use the
> **☰ menu** in the header to jump between them.

## Features

- 📄 **Faithful rendering** — headings, paragraphs, **bold**/*italic* runs,
  tables, lists, and inline images render with their document formatting.
- 🖼️ **Images inline** — embedded pictures are decoded locally and shown in
  place; nothing is fetched from the network.
- 🔀 **Drop to replace** — drop a new document while one is open and it replaces
  the current view.
- 🧭 **Legacy notice** — older/binary formats (`.doc`, `.rtf`, `.odt`) that have
  no reliable in-browser renderer get a clear "Save As → .docx" note instead of
  a broken page.
- ☰ **Family menu** — a hamburger flyout links to every viewer.
- 🫥 **Distraction-free header** — auto-hides while you read, collapsing to a thin
  handle; hover, tap, or scroll up to bring it back.
- 🎨 **Pick any background color** — remembered across visits.
- 🪶 **One file, no build** — `index.html` is self-contained and works offline,
  even from `file://`.
- 📊 **Privacy-friendly analytics** — self-hosted, cookieless
  [Plausible](https://plausible.io/); your files never leave your device.

## Supported file types

**Rendered in full:** `.docx` `.docm` `.dotx` `.dotm`

**Accepted with a notice** (no reliable in-browser renderer — open in Word or
LibreOffice and use *Save As → .docx*): `.doc` `.dot` `.rtf` `.odt`

## Quick start

**Just open it.** Download [`index.html`](index.html), double-click it — no
server, no build, no internet needed.

```sh
python3 -m http.server 8080   # then open http://localhost:8080
```

## Deploy to Cloudflare Pages

Connect the repo (**Workers & Pages → Create → Pages → Connect to Git**),
framework preset **None**, build command blank, output directory `/`. The
[`_headers`](_headers) file applies a strict CSP automatically. Add the custom
domain **docx-viewer.us** under the project's Custom domains tab.

## How it works

Everything is in [`index.html`](index.html) — app logic plus two inline libraries,
so rendering works offline:

- [**docx-preview**](https://github.com/VolodymyrBaydalka/docxjs) `v0.3.3`
  (Apache-2.0) — renders Office Open XML (`.docx`) into HTML.
- [**JSZip**](https://github.com/Stuk/jszip) `v3.10.1` (MIT) — unzips the
  `.docx` package (a `.docx` is a ZIP of XML parts) in the browser.

Images are inlined as `data:` URLs (`useBase64URL`), so the viewer's CSP stays
strict (`default-src 'none'`, no external assets, no `blob:`).

**Note:** this is a viewer — it shows **content + layout**. Some advanced Word
features (tracked-change markup, comments, complex field codes, macros) are not
rendered; content controls show their current values.

## Credits

| Component | Version | License |
| --- | --- | --- |
| [docx-preview](https://github.com/VolodymyrBaydalka/docxjs) | 0.3.3 | Apache-2.0 |
| [JSZip](https://github.com/Stuk/jszip) | 3.10.1 | MIT |
| [pako](https://github.com/nodeca/pako) (bundled in JSZip) | 1.0.x | MIT |

The file-type icon (favicon and header icon) is from
[vscode-icons](https://github.com/vscode-icons/vscode-icons) (MIT). Analytics by
[Plausible](https://plausible.io/).

## License

[MIT](LICENSE) © 2026 Michal Ferber, aka **TechGuyWithABeard**. Bundled
components retain their own licenses — see [`LICENSE`](LICENSE) and
[Credits](#credits).
