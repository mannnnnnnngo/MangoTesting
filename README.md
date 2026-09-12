<div align="center">

<img src="Icon/mango%20test.png" width="140" alt="Mango Testing icon">

# 🥭 Mango Testing

**A vocabulary and geography trainer that runs entirely on your own computer. Six ways to drill words, fourteen maps, and nothing that leaves the machine.**

Made by Mingyu 🧑‍💻

<br>

![macOS](https://img.shields.io/badge/macOS-11%2B-202020?style=for-the-badge&logo=apple&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-10%2B-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![Version](https://img.shields.io/badge/version-1.0.0-7C5CFF?style=for-the-badge)
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
> **A fresh install is empty.** 📭 No word list, no history, no streak and no stats — everything
> you build up is written to a single file in your own Documents folder, and it never leaves your
> computer.

---

## 📖 Contents

| | | |
| --- | --- | --- |
| [🎁 What it is](#-what-it-is) | [📥 Install](#-install) | [🍎 macOS](#-macos) |
| [🪟 Windows](#-windows) | [🔤 Words](#-words) | [🌍 Geo](#-geo) |
| [🗺️ Where the maps come from](#️-where-the-maps-come-from) | [🕘 History and stats](#-history-and-stats) | [📡 Share](#-share) |
| [🗂️ Where things live](#️-where-things-live) | [🔔 Updates](#-updates) | [⚖️ Licence](#️-licence) |

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

Everything is on **[the Releases page](https://github.com/mannnnnnnngo/MangoTesting/releases)** —
a `.dmg` for Macs and a `.zip` for Windows.

### 🍎 macOS

Double-click the `.dmg`, drag the mango into Applications, then open it from Launchpad. It runs
as a real Mac app — its own window, Dock icon, menu bar and Cmd+Q — not a browser tab. Under the
hood a small local server runs as an invisible child process and the window is a `WKWebView`
pointed at it; quitting the app stops the server. Your data lives in
`~/Documents/Mango Testing/data.json`.

The app is a universal binary (Apple silicon + Intel, macOS 11+) and is ad-hoc signed. It is
*not* signed with a Developer ID — that needs a paid Apple account — so the first launch shows
the unidentified-developer warning. **Right-click the app → Open → Open** clears it permanently. 🔓

> [!TIP]
> The app needs Python, which every Mac has once Apple's free Command Line Tools are installed.
> If they aren't, opening the app shows a dialog explaining that and offering an **Install
> Python** button that kicks off Apple's installer — no Terminal, no Apple account. If that
> dialog can't be shown for any reason, the instructions open in TextEdit instead, so a missing
> Python never looks like an app that just does nothing. 🐍

A Mac missing the tools still *has* a file at `/usr/bin/python3` — a stub whose only job is to
prompt for them — so the app tests that the interpreter actually runs, rather than that the path
exists.

### 🪟 Windows

Download `Mango Testing (Portable).zip` (~12 MB), extract it, and double-click
**`Mango Testing.bat`**. Nothing is installed, and **you don't need Python** — the zip carries
its own interpreter. Your data lives in `%USERPROFILE%\Documents\Mango Testing\data.json`,
mirroring the Mac, so the two are interchangeable on one PC.

You get a real app here too: its own window, no address bar, no tabs, its own taskbar button,
close-to-quit. The window is Edge started in Chromium's chromeless mode; Chrome and Brave are
picked up as fallbacks, and a PC with no Chromium at all opens the default browser instead.

> [!TIP]
> **Right-click the zip → Properties → tick Unblock** *before* extracting. That clears the Mark of
> the Web from everything inside in one go and Windows stays completely quiet. Skip it and you get
> one "are you sure" on the `.bat` — an annoyance, nothing more. 🧯

First launch raises a Windows Firewall prompt. Tick **Private networks** and allow it, or the PC
stays invisible to [Share](#-share).

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

Typed answers are graded forgivingly: typos, plural and suffix variation, and reworded
definitions all still count. ✅

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
spelling slip rather than a wrong answer, using the same threshold as word tests. Grading happens
in the browser, because a map game can't wait on a round trip per question.

Running out of chances puts the right answer up in orange for a beat before moving on, and the end
of a run offers **Drill the misses** — just the ones you got wrong, again. Best score per map is
remembered.

> [!NOTE]
> Geo runs are kept separately from the word tests: they don't touch the perfect-test streak, the
> accuracy rings or the history list. Naming every country in Africa says nothing about how the
> vocabulary is going.

### 🗺️ Where the maps come from

The maps are built from [Natural Earth](https://www.naturalearthdata.com) (public domain) and
[us-atlas](https://github.com/topojson/us-atlas). They ship already projected — each map is a list
of SVG path strings and a viewBox, so the browser draws it with no projection maths, no GeoJSON
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

One JSON file, editable by hand and easy to back up: the word list, the history, the streak, the
stats, the cached sentences and the geo records.

Nothing is ever sent anywhere. There is no account, no telemetry and no network call at all
except **Share**, which only talks to the other computer you point it at. 🔒

---

## 🔔 Updates

Mango Testing checks [`updates/latest.json`](updates/latest.json) on this repository and tells you
when a newer version is out. It carries nothing about you, and the download is whatever is
attached to the matching release. 📡

---

## ⚖️ Licence

Mango Testing is **free to use** but **not open source**. It may not be redistributed, modified,
resold, reverse engineered, or presented as anyone else's work. The full terms are in
[`LICENSE`](LICENSE).

Map data is not mine and is not covered by that: Natural Earth is public domain, and us-atlas
carries its own licence.

Copyright © 2026 Mingyu. All rights reserved.

---

<div align="center">

**Made with 🥭 by Mingyu**

🆓 Free forever · 🔒 Nothing leaves your computer · 🍎🪟 macOS & Windows

</div>
