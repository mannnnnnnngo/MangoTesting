<div align="center">

<img src="mango%20test.png" width="140" alt="Mango Testing icon">

# 🥭 Mango Testing

**A vocabulary and geography trainer that runs entirely on your own computer. Six ways to drill words, fourteen maps, and nothing that leaves the machine.**

Made by Mingyu 🧑‍💻

<br>

![macOS](https://img.shields.io/badge/macOS-11%2B-202020?style=for-the-badge&logo=apple&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-10%2B-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![Python](https://img.shields.io/badge/Python-Flask-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Version](https://img.shields.io/badge/version-1.1.0-7C5CFF?style=for-the-badge)
![Price](https://img.shields.io/badge/price-free-2EA043?style=for-the-badge)
![Privacy](https://img.shields.io/badge/data%20sent%20anywhere-none-0EA5E9?style=for-the-badge)

</div>

---

> [!NOTE]
> **Mango Testing is completely free, and it runs on both macOS and Windows.** 🆓 It looks like a
> browser app because it is one — a small local server plus a chromeless window — but it behaves
> like a real app: its own window, its own Dock or taskbar button, close to quit, no address bar.
> Nothing is uploaded anywhere. 🔒

> [!IMPORTANT]
> **This repository is the app, not your data.** 📭 A fresh clone starts with an empty word list,
> no history, no streak and no stats — `data/store.py` writes the defaults on first run. Your own
> `data.json` is deliberately untracked, so cloning this never hands anyone your word list or
> your test results.

---

## 📖 Contents

| | | |
| --- | --- | --- |
| [📥 Install](#-install) | [🍎 macOS](#-macos) | [🪟 Windows](#-windows) |
| [🔤 Words](#-words) | [🌍 Geo](#-geo) | [🗺️ Where the maps come from](#️-where-the-maps-come-from) |
| [🕘 History and stats](#-history-and-stats) | [📡 Share](#-share) | [🗂️ Where things live](#️-where-things-live) |
| [🧱 Source layout](#-source-layout) | [🔨 Running from source](#-running-from-source) | [⚖️ Licence](#️-licence) |

---

## 🎁 What it is

A trainer with two things to learn and one tab for each:

| Tab | What's in it |
|---|---|
| 🔤 **Words** | your word list, and all six ways of testing it |
| 🌍 **Geo** | fourteen maps, four ways of testing those, three difficulties |

Everything else is shared: **History** is one list for every test you take, **Share** sends your
words to another machine on the Wi-Fi, and the dashboard adds up the streak and the totals.

---

## 📥 Install

### 🍎 macOS

Two installers get built, both into `dist/`:

| Installer | Who it's for | Word list |
|---|---|---|
| `Mango Testing (Mine) Installer.dmg` | you | your current list is already inside |
| `Mango Testing Installer.dmg` | anyone you hand it to | starts empty |

Both keep their data in `~/Documents/Mango Testing/data.json`. Send people the **second** one —
the first has a word list, history and stats baked into it.

Double-click the `.dmg`, drag the mango into Applications, then open it from Launchpad. It runs
as a real Mac app — its own window, Dock icon, menu bar and Cmd+Q — not a browser tab. Under the
hood a small local server runs as an invisible child process and the window is a `WKWebView`
pointed at it; quitting the app stops the server.

The executable is a universal binary (Apple silicon + Intel, macOS 11+) and is ad-hoc signed. It
is *not* signed with a Developer ID — that needs a paid Apple account — so first launch shows the
unidentified-developer warning. Right-click the app → **Open** → **Open** clears it permanently.

> [!TIP]
> The app needs Python, which every Mac has once Apple's free Command Line Tools are installed.
> If they aren't, opening the app shows a dialog explaining that and offering an **Install
> Python** button that kicks off Apple's installer — no Terminal, no Apple account. If that
> dialog can't be shown for any reason, the instructions open in TextEdit instead, so a missing
> Python never looks like an app that just does nothing. 🐍

A Mac missing the tools still *has* a file at `/usr/bin/python3` — a stub whose only job is to
prompt for them — so the launcher tests that the interpreter actually runs, rather than that the
path exists.

### 🪟 Windows

Two builds, and **the portable one is the one to hand out** — it's the only one Windows doesn't
put a scare screen in front of.

| Build | What you get | SmartScreen |
|---|---|---|
| `scripts/build_windows_portable.py` | a `.zip` — extract and run | says nothing |
| `scripts/build_windows.py` | a `Setup.exe` installer | blocks it unless you sign it |

Both give a real app: its own window, no address bar, no tabs, its own taskbar button,
close-to-quit. Data lives in `%USERPROFILE%\Documents\Mango Testing\data.json`, mirroring the
Mac, so the two are interchangeable on one PC.

#### Portable (recommended)

```bat
py scripts\build_windows_portable.py            :: both variants -> dist\
py scripts\build_windows_portable.py personal   :: or just one
```

Out comes `Mango Testing (Portable).zip` (~12 MB) holding the app's `.py` files, Flask, and the
python.org embeddable interpreter. Whoever you send it to extracts it and double-clicks
`Mango Testing.bat`; nothing is installed and no Python is needed.

The window is Edge started with `--app=`, Chromium's chromeless mode — the same engine WebView2
uses, so it looks like the frozen build does. Chrome and Brave are picked up as fallbacks, and a
PC with no Chromium at all opens the default browser instead.

Unlike the `.exe` build this **doesn't have to run on Windows** — it only copies files and asks
pip for wheels built for another platform, so a Mac can produce the Windows zip. It needs the
network the first time, to fetch the interpreter and the Flask wheels; both are then cached in
`build/`.

> [!TIP]
> Tell whoever gets the zip to **right-click it → Properties → tick Unblock** *before* extracting.
> That clears the Mark of the Web from everything inside in one go, and Windows stays completely
> quiet. Skip it and they get one "are you sure" on the `.bat` — an annoyance, not the wall the
> unsigned `.exe` hits. 🧯

#### Installer

Building this one has to happen **on a Windows PC** — PyInstaller freezes for the platform it
runs on, so a `.exe` can't be produced from macOS:

```bat
py -m pip install -r requirements-windows.txt
py scripts\build_windows.py            :: both variants -> dist\
py scripts\build_windows.py personal   :: or just one
```

That gives `Mango Testing Setup.exe` and `Mango Testing (Mine) Setup.exe` if
[Inno Setup](https://jrsoftware.org/isinfo.php) is on PATH, and a portable `.zip` of the same
thing if it isn't.

What comes out is unsigned, and Defender SmartScreen stops unsigned executables that arrive from
the internet: *"Windows protected your PC"*, with Run hidden behind **More info**. Fine on your
own machine, awkward to talk someone else through. Two ways past it and only two — ship the
portable build instead, or sign this one. For signing, set `MANGO_SIGN_PFX` (plus
`MANGO_SIGN_PASSWORD`), or `MANGO_SIGN_SHA1` for a certificate already in your store, and the
build runs `signtool` over the app and the installer. It has to be a real certificate from a CA;
a self-signed one changes nothing here, because SmartScreen judges reputation, not encryption. An
OV certificate earns that reputation over a few weeks of downloads, an EV one has it from day one.

First launch on either build raises a Windows Firewall prompt. Tick **Private networks** and
allow it, or the PC stays invisible to [Share](#-share).

---

## 🔤 Words

Everything word-shaped is on the **Words** page: the six test modes across the top, then
**Add Words** / **New List** and the list itself underneath, each row editable in place.
**Word Accuracy** (results by date range) and **Test History** are linked from there.

| Mode | What it asks |
|---|---|
| Definition | see the word, type its meaning |
| Word | see the meaning, recall the word |
| Memory | flashcards you grade yourself |
| Sentence | fill in the blank |
| Custom | a mix of the modes you pick, up to two per word |
| Every | all four modes over every word |

Typed answers are graded by `services/grading_service.py`, which forgives typos, plural and
suffix variation, and reworded definitions.

---

## 🌍 Geo

The **Geo** page drills maps the way Words drills vocabulary. Pick one of fourteen maps, pick how
you want to be asked, and go:

| | |
|---|---|
| **Everything** | the whole world — every sovereign country, 194 of them |
| **Continents** | Africa · Asia · Europe · North America · South America · Oceania |
| **Regions** | the Middle East · Southeast Asia · the Caribbean · Central America · Northern Europe · West Africa |
| **United States** | all 50 states, Alaska and Hawaii inset |

Four ways to be asked, the same four ideas the word tests use:

| Mode | What it asks |
|---|---|
| Find it | you get a name, you click it on the map |
| Name it | one lights up, you pick its name out of four (number keys work) |
| Type it | one lights up, you type its name |
| Memory | one lights up, you recall it, reveal, and grade yourself |

And three difficulties, which decide how many stabs you get at a single question and how much
help a miss gives you:

| | Chances | On a miss |
|---|---|---|
| Easy | five | names what you actually hit, and points you at the answer ("head north-east") |
| Normal | three | names what you actually hit |
| Hard | one | nothing — the question is already over |

A question only counts as wrong once the chances run out; until then the board stays exactly as
it was and you go again. Memory mode ignores all this, since you grade yourself there.

Everything you do get **stays on the map**, filled in with its name, until the run ends — so a run
of the whole world fills the map in as you go rather than wiping it every question. The header
carries a live accuracy figure next to the score, and the end of a run breaks it down: accuracy,
how many you got first time, how many answers it took in total, and the clock.

Each name is also **read out loud** when it is asked (or, in the modes that hide it, when the
answer is revealed). The speaker button in the header mutes it, and the choice is remembered; in
Find mode, clicking the name reads it again. 🔊

Rounds are 10, 20, or the whole set. Scroll to zoom and drag to pan — worth it for the Caribbean.
Anything too small to click, from Monaco to Tuvalu, gets a dot to aim at, and in the modes that
light a country up, anything that small gets zoomed to and pulses.

**Type it** forgives what the word tests forgive. Case, accents and a leading "the" don't matter
(`cote divoire`, `the gambia`), alternate names are accepted — `USA`, `Holland`, `Burma`,
`Czechia`, `Zaire`, and every formal name Natural Earth carries — and a near miss is marked as a
spelling slip rather than a wrong answer, using the same threshold as word tests
(`WORD_TYPO_SIMILARITY_THRESHOLD` in `config.py`). Grading happens in the browser, because a map
game can't wait on a round trip per question.

Running out of chances puts the right answer up in orange for a beat before moving on, and the end
of a run offers **Drill the misses** — just the ones you got wrong, again. Best score per map is
remembered.

> [!NOTE]
> Geo runs are kept separately from the word tests: they don't touch the perfect-test streak, the
> accuracy rings or the history list. Naming every country in Africa says nothing about how the
> vocabulary is going.

### 🗺️ Where the maps come from

`static/data/geo/` holds one file per map, built by `scripts/vendor_geo.py` from
[Natural Earth](https://www.naturalearthdata.com) (public domain) and
[us-atlas](https://github.com/topojson/us-atlas). They are already projected — each file is a list
of SVG path strings and a viewBox, so the browser draws a map with no projection maths, no GeoJSON
parsing and no mapping library. Every map is equal-area: Equal Earth for the globe, Lambert
azimuthal for a region, Albers for the states.

---

## 🕘 History and stats

**History** is one list for every test you take, of either kind, with the questions kept so a
result can be reopened rather than just totalled. The dashboard adds up the streak (perfect word
tests in a row), the lifetime totals and the accuracy rings.

The lifetime word ledger is deliberately separate from the active list: replacing the list with
**New List** or deleting a word never shrinks the count of what you have learned. The two answer
different questions and are stored apart for that reason.

---

## 📡 Share

**Share** sends your word list to another machine on the same Wi-Fi — no account, no server in
the middle, nothing leaving the local network. The receiving copy gets the words only; history,
streaks and stats stay where they are.

---

## 🗂️ Where things live

| Where | What |
|---|---|
| `~/Documents/Mango Testing/data.json` | 🍎 macOS — everything you have done |
| `%USERPROFILE%\Documents\Mango Testing\data.json` | 🪟 Windows — the same file |
| `./data.json` | 🔨 running from source — the dev copy, untracked by git |

One JSON file, editable by hand and easy to back up: the word list, the history, the streak, the
stats, the cached sentences and the geo records. The packaged app sets `MANGO_DATA_FILE` to point
at the Documents copy, because a file inside an `.app` bundle isn't a place to write.

Nothing is ever sent anywhere. There is no account, no telemetry and no network call at all
except **Share**, which only talks to the other computer you point it at. 🔒

---

## 🧱 Source layout

Flask, layered so a route never touches a file and a service never renders anything:

```
app.py          the Flask app + window/launcher glue
config.py       every tunable, including the typo threshold
launcher.py     starts the server and opens the chromeless window
routes/         one module per page: words · test · geo · history · accuracy · share · dashboard
services/       the logic: grading · sentences · stats · streaks · history · geo · share
data/store.py   the only module that touches data.json
static/         css · js · fonts · img · data/geo (the projected maps)
scripts/        the build scripts: macOS app, Windows exe, Windows portable, asset vendoring
```

| 📄 File | Purpose |
| --- | --- |
| `data/store.py` | Load and save, with the defaults a fresh install starts from. The storage backend can change here without touching anything else |
| `services/grading_service.py` | What counts as right — typos, plurals, suffixes, reworded definitions |
| `services/streak_service.py` | The perfect-test streak, kept apart from the geo records on purpose |
| `scripts/vendor_geo.py` | Turns Natural Earth and us-atlas into pre-projected SVG paths |
| `scripts/build_app.py` | The macOS `.app` and both `.dmg` installers |
| `scripts/build_windows_portable.py` | The zip that needs no Python and no install |
| `config.py` | Thresholds and paths, including `MANGO_DATA_FILE` |

---

## 🔨 Running from source

```bash
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/python launcher.py
```

First run writes a `data.json` next to the source with an empty list in it. That file is in
`.gitignore` — it is your data, not the app's.

---

## ⚖️ Licence

Mango Testing is **free to use** but **not open source**. The source is published here to be
read, not reused: it may not be redistributed, resold, built upon, or presented as anyone else's
work. The full terms are in [`LICENSE`](LICENSE).

Map data is not mine and is not covered by that: Natural Earth is public domain, and us-atlas
carries its own licence.

Copyright © 2026 Mingyu. All rights reserved.

---

<div align="center">

**Made with 🥭 by Mingyu**

🆓 Free forever · 🔒 Nothing leaves your computer · 🍎🪟 macOS and Windows

Part of [🥭 MangoApps](https://github.com/mannnnnnnngo/MangoApps)

</div>
