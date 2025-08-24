# Schliemann’s Way（シュリーマンの道）

> A lightweight, purely client‑side **practice tool for language learners following the Schliemann method** (Heinrich Schliemann, the archaeologist).  
> Focus: **parallel reading**, **sentence‑by‑sentence back‑translation**, **reading aloud** — with **Furigana**, **Focus Mode**, and **Dark Mode**.

---

## Table of Contents

- [Purpose & Learning Principle](#purpose--learning-principle)
  - [Why the “Schliemann Method”?](#why-the-schliemann-method)
  - [How the app supports the method](#how-the-app-supports-the-method)
  - [Suggested practice routine (10–20 min)](#suggested-practice-routine-1020-min)
- [Features](#features)
- [Quick Start](#quick-start)
- [Usage](#usage)
  - [Reading & Navigation](#reading--navigation)
  - [Focus Mode](#focus-mode)
  - [Dark Mode](#dark-mode)
  - [Furigana](#furigana)
  - [Generate / Translate / Annotate](#generate--translate--annotate)
  - [Admin Tab (Settings)](#admin-tab-settings)
- [Installation & Deployment](#installation--deployment)
- [Privacy & Security](#privacy--security)
- [Tech & Architecture](#tech--architecture)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [Known Limitations](#known-limitations)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)
- [Changelog](#changelog)

---

## Purpose & Learning Principle

**Schliemann’s Way** is intentionally minimal: no course, no gamification — a **tool** for working efficiently with **your own texts** or **parallel sentences**. It targets learners who want to work **actively**: read, compare, **translate sentence by sentence**, repeat, and speak out loud.

### Why the “Schliemann Method”?

Heinrich Schliemann (archaeologist, 1822–1890) described how he learned languages through **intensive reading**, **parallel texts**, especially **back‑translation** (from the target language back into the source), and **daily repetition**. This app is **inspired by that workflow**:

- **Parallelism:** source ↔︎ target displayed side by side  
- **Sentence fidelity:** one sentence on the left corresponds to exactly one on the right  
- **Back‑translation:** deliberately convert the active sentence into the other language  
- **Reading aloud & focus:** keep one sentence in view, articulate clearly, repeat rhythmically  
- **Repetition:** navigate quickly and target difficult spots

> The goal is **active production** and **precise understanding** — not passive scrolling.

### How the app supports the method

- **Two‑column reader** with **sentence‑level synchronization**  
- **Focus lines:** the active sentence in both languages is prominently centered  
- **Focus Mode (fullscreen):** hide distractions — keep only the **two focus lines**  
- **Furigana support** for Japanese via HTML `<ruby><rt>`  
- **Sentence‑preserving translation** (both directions) for 1:1 alignment practice  
- **Reading aloud:** zoom/highlight makes speaking comfortable  
- **Persistence:** everything stays local for fast daily sessions

### Suggested practice routine (10–20 min)

1. **Load/paste text** (parallel or single‑sided) and **Render**.  
2. **Pick a sentence**, read it aloud in **Focus Mode**.  
3. **Back‑translate** (e.g., JA → EN/DE or EN/DE → JA) — do it yourself first, then verify with the **Translate** button if needed.  
4. **Toggle Furigana** to reinforce kanji as needed.  
5. **Next sentence (→)** — repeat difficult ones several times.  
6. **Reflect briefly:** which structures were hard? Start with them next session.

---

## Features

- 📖 **Two‑column reader:** native language on the left, Japanese on the right — sentence‑synchronized  
- 🎯 **Focus Mode (overlay):** fullscreen with only **two focus lines** + prev/next + zoom  
- 🌓 **Dark Mode:** toggleable, persisted locally  
- 🈶 **Furigana:** full `<ruby><rt>` support + automatic annotation of existing Japanese text  
- 🔁 **Sentence‑preserving translation:** keeps sentence count in both directions  
- 🧠 **Generate:** create practice texts in Japanese (with Furigana) or in your native language  
- ⚙️ **OpenAI‑compatible:** configurable API base & models (OpenAI, vLLM, proxies, etc.)  
- 💾 **Local persistence (`localStorage`):** texts, UI state, models & prompts  
- 🧰 **Clean Admin tab:** stacked fields, clear sections

---

## Quick Start

1. **Open the file**  
   ```text
   schliemanns_weg.html
   ```
   Open directly in your browser (Chrome/Edge/Firefox) **or** serve it quickly:
   ```bash
   # Python
   python -m http.server 8080
   # Then: http://localhost:8080/schliemanns_weg.html
   ```

2. **(Optional) Configure the API**  
   In the **Admin** tab, fill in `API Base` & `API Key` if you want to use Generate/Translate/Annotate. The application has been tested with openai llms. Other models will follow. 

3. **Paste your own texts**  
   Left (native language) and/or right (Japanese) → **Render**.  
   Tip: Using **“Remove line breaks”** (left side) helps keep sentence alignment clean.

---

## Usage

### Reading & Navigation
- Click a sentence in the reading pane to make it **active** (both sides sync).  
- Navigate with the arrow buttons or the **← / →** keys.  
- The **focus lines** (under the editors) always mirror the active sentence.

### Focus Mode
- Toggle **“Focus”** at the top left.  
- Fullscreen overlay with **only two lines** (native | 日本語), ideal for **reading aloud**.  
- In the overlay:
  - **A‑ / A+**: zoom
  - **← / →**: switch sentence
  - **Focus toggle** or **Esc**: exit

### Dark Mode
- Toggle **“Dark”** at the top left; stored in `localStorage`.

### Furigana
- **“Show Furigana”** checkbox in the JP reader.  
- **“Add Furigana”** annotates an existing JP text (`<ruby><rt>`).

### Generate / Translate / Annotate
- **Generate:** enter a prompt at the top → click **Generate**  
  - Mode “Target language 日本語” produces Japanese with Furigana  
  - Mode “Native language” produces text in your chosen native language
- **Translate → 日本語:** left‑side button (sentence‑preserving, with Furigana)  
- **Translate ← Native:** right‑side button (sentence‑preserving)  
- **Annotate:** add Furigana to an existing JP text

### Admin Tab (Settings)
- **Access:** `API Base`, `API Key`  
- **Models:** generation, translation, annotation/Furigana  
- **Parameters:** temperature & max tokens per area  
- **Prompts:** editable system prompts  
- **Other:** `Native language`, **Save**, **Test connection**  
> All values are stored **locally**.

---

## Installation & Deployment

- **Local:** double‑click the file or serve it with a simple web server.  
- **GitHub Pages:**
  1. Publish the repository  
  2. In **Settings → Pages**, select branch/folder  
  3. Place the file in the selected path and open the URL
- **Static hosting:** Netlify, Vercel, Nginx/Apache — no build tools required.

---

## Privacy & Security

- **Stored locally:** API key, texts & settings remain in the browser (`localStorage`), no server DB.  
- **API key in the client:** if used directly in the browser, your key is technically visible.  

---

## Tech & Architecture

- **Single‑file app:** HTML + CSS + vanilla JS  
- **State:**  
  - `settings` (models, parameters, prompts)  
  - `state` (texts, focus, UI flags)  
  - persistence via `localStorage` (`sw_*`)
- **Sentence segmentation:**
  - Native language: regex on `. ! ? … ; :`  
  - Japanese: regex on `。！？` + `\n` as paragraph marker  
- **Safe `<ruby>`:** sanitization allows only `RUBY/RB/RT/RP/BR/SPAN`  
- **OpenAI‑compatible:** `/v1/chat/completions` (works with compatible proxies)

---

## Keyboard Shortcuts

- `←` / `→` — switch active sentence  
- `Esc` — exit Focus Mode

---

## Known Limitations

- **Sentence splitting:** robust heuristics, but not perfect (abbreviations, edge cases).  
- **Model limits:** very long inputs may hit token limits (configurable).
- **Costs:** depending on the model used costs may vary. A future version will implement local furigana support. 
- **Client key:** prefer a proxy for production use.

---

## Roadmap

- [ ] Export/Import sessions (JSON)
- [ ] Multilanguage Support for the interface
- [ ] Local Furigana Annotations
- [ ] Hotkeys for Generate/Translate/Annotate  
- [ ] Swap columns (JP ↔︎ native)  
- [ ] TTS option for reading the focus lines  
- [ ] Customizable sentence‑splitting profiles per language  
- [ ] Print/handout layout
- [ ] MCP connectivity

---

## Contributing

Contributions are welcome!

1. Fork the repo  
2. Create a branch: `feature/my-idea`  
3. Commit with clear messages  
4. Open a pull request (include context, screenshots, examples)

**Please:** keep vanilla JS, clear function names, comments for regex/heuristics, and avoid unnecessary dependencies.

---

## License

This project is licensed under the [MIT License](LICENSE).  
You are free to use, modify, and distribute this software for any purpose, including commercial use, provided that the original license text is included in all copies or substantial portions of the software.

---

## Changelog

### v1.1 – Dark & Focus
- 🌓 **Dark Mode** (persisted)  
- 🎯 **Focus Mode** (overlay, zoom, nav, Esc)  
- 🧰 **Admin reorganized** (stacked fields, clear sections)

### v1.0 – Initial Release
- Two‑column reader, focus lines, Furigana, generate/translate/annotate, persistence

---

> **In short:**  
> This tool puts the **Schliemann method** into practice: **one sentence — two languages — active back‑translation — reading aloud**.  
> Train **accuracy**, **fluency**, and **formulaic language** — focused, fast, and distraction‑free.
