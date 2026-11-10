# 📱➡️🖥️ Mobile Apps Worth Porting to Desktop

A curated catalog of **open-source mobile apps** (Android + iOS, on GitHub / GitLab / Codeberg / F-Droid) that are worth porting to **Linux and other desktops** — because they're genuinely great, but the phone is the only place you can run them.

> The rule of thumb: a mobile-first UI is nice; a desktop **without any good FOSS option** for the same job is a gap. This list catalogs the gaps — and, now that iOS is in scope, it also catalogs what each platform can and cannot teach us about closing them.

---

## 📚 Contents

- [Selection Criteria](#-selection-criteria)
- [Scoring System](#-scoring-system)
- [📱 Platform Reality — iOS & FOSS](#-platform-reality--ios--foss)
- [🥇 Top Picks (Tier S)](#-top-picks-tier-s)
- [📖 Full Catalog (by category)](#-full-catalog-by-category)
  - [Security & 2FA](#security--2fa)
  - [Wearables & Connected Hardware](#wearables--connected-hardware)
  - [Tasks, Habits & Time](#tasks-habits--time)
  - [Notes & Writing](#notes--writing)
  - [Health & Fitness](#health--fitness)
  - [Maps & Navigation](#maps--navigation)
  - [Personal Finance](#personal-finance)
  - [Podcasts, Music & Media](#podcasts-music--media)
  - [Reading, Comics & RSS](#reading-comics--rss)
  - [Images & Photos](#images--photos)
  - [Utilities & System](#utilities--system)
  - [Games & Emulation](#games--emulation)
- [🚫 Don't Bother — Already Solved on Desktop](#-dont-bother--already-solved-on-desktop)
- [🔒 Device-Bound — Porting Makes No Sense](#-device-bound--porting-makes-no-sense)
- [📚 Lessons From Ports That Already Happened](#-lessons-from-ports-that-already-happened)
- [🛠️ Porting Playbook](#️-porting-playbook)
- [Evaluating a New Candidate](#evaluating-a-new-candidate)
- [🕵️ Discovery Pipeline](#️-discovery-pipeline)
- [❓ FAQ](#-faq)
- [🔗 Handy Resources](#-handy-resources)
- [🤝 Contributing](#-contributing)

---

## ✅ Selection Criteria

An app belongs here when it checks **all** of the following:

1. **Openly licensed** — an OSI-style FOSS license (GPL/MIT/Apache/MPL/AGPL…), source hosted publicly (GitHub / GitLab / Codeberg). Commercial "open-source in name" licenses (personal-use-only etc.) don't qualify.
2. **Mobile-first, desktop-absent** — an Android or iOS app for which no mature, maintained FOSS desktop equivalent does the same job. *(Apps that already ship Linux builds are moved to [solved](#-dont-bother--already-solved-on-desktop).)*
3. **Desktop-valuable** — the core value doesn't depend on phone-only hardware (GPS, camera, cellular). A port should be *useful*, not just *possible*.
4. **Alive** — commits within the last year, or a community big enough to carry a port.
5. **Portable-ish (bonus)** — logic/persistence is reusable: Kotlin/Java → JVM, Flutter → Flutter Linux & macOS, React Native → RN Desktop/Tauri, clean C++ core. Cross-phone apps (Android+iOS) with a shared core score highest here.

## 🧮 Scoring System

Each app is scored **0–3** on three axes — max **9/9**:

| Axis | Meaning |
|---|---|
| **G — Desktop Gap** | 0 = desktop already covers it · 3 = nothing comparable exists on Linux |
| **P — Portability** | 0 = full rewrite · 3 = most of the app transfers (Flutter / KMP / clean core). A shared Android+iOS build (Flutter/KMP/RN) → both phones + desktop from one tree |
| **V — Value** | 0 = nice-to-have · 3 = desktop users would feel this absence daily |

**Tiers:** `7–9` 🥇 Tier S · `5–6` 🥈 Tier A · `3–4` 🥉 Tier B · `<3` ⬜ skip.

**Legend for "Code" columns:** language · license · ⭐ GitHub stars (≈ Nov 2026). A 🤖 after an app name links to its F-Droid page.

---

## 📱 Platform Reality — iOS & FOSS

An honest analysis of what "mobile" means when iOS is in scope. Three structural facts shape this catalog:

### 1. iOS FOSS distribution is thinner by design
| Constraint | Android | iOS |
|---|---|---|
| FOSS-first app store | **F-Droid** (whole philosophy) | none — App Store is the only mainstream channel; [SideStore](https://github.com/SideStore/SideStore)/AltStore do sideloading, but with developer-account and expiry ceilings |
| Sideload freely | yes, since day one | no; EU's DMA now allows alternative marketplaces/notarization, but fees and gatekeeping remain |
| TestFlight builds | n/a | expire after 90 days — FOSS "install from source" is a moving target |
| Background hardware access (BLE, sensors) | generous | tightly restricted (e.g., no continuous background BLE scans — the reason **no Gadgetbridge-equivalent can exist on iOS**) |

Consequence: the catalog skews Android. That's measurement, not bias.

### 2. Stack asymmetry is the real porting border
| Stack typical of | Porting toward desktop | Verdict |
|---|---|---|
| **Android-only Kotlin/Java apps** | Compose for Desktop / GTK shell w/ JVM logic | the classic route — the whole old Android list |
| **Cross-phone FOSS** (Flutter, KMP, React Native — most *modern* iOS FOSS is this) | one tree already serves Android + iOS; adding Linux/macOS is incremental | **the highest-leverage candidates** — a port here benefits every platform at once |
| **SwiftUI/Swift iOS-native apps** | nothing left Apple (SwiftUI cannot target Linux; Catalyst only extends to macOS) | iOS-native FOSS rarely survives the jump — they usually end up as macOS-only twins |

So the honest title of the iOS rule is: **iOS contributes *learnings* and a few cross-phone jewels — not many port targets.**

### 3. Verified iOS-side finds
Genuine cross-phone FOSS with a desktop gap found (so far):

| Score | App | Platforms | What it is | Code | Porting notes |
|:--:|---|---|---|---|---|
| 5 | [Zeus](https://github.com/ZeusLN/zeus) | Android + iOS | Self-custodial Bitcoin/Lightning wallet + remote LND/Core Lightning node manager; reproducible builds | TypeScript · **React Native** · AGPL-3 · ⭐1.4k | One of the few *first-class* FOSS mobile wallets on both stores, F-Droid included. Desktop gap: a tray/CLI dashboard for a self-hosted node is genuinely missing; the shared TypeScript logic can be re-hosted under a Tauri/Electron (Node) shell. ⚠️ Wallet-grade security bar — audit before shipping anything. |

And the two most famous **iOS-native FOSS** apps, both verified to already ship macOS (so they close their own gap partially): [Ice Cubes](https://github.com/Dimillian/IceCubesApp) (Mastodon, AGPL-3, ⭐7.1k — iOS/iPadOS/**macOS**/visionOS) and [Damus](https://github.com/damus-io/damus) (Nostr, GPL-3, ⭐2.1k — iOS/**macOS**). Linux/Windows counterparts aren't their jobs — see the [solved list](#-dont-bother--already-solved-on-desktop).

*The [iOS open-source index](https://github.com/dkhamsing/open-source-ios-apps) is where new candidates get mined — see [Discovery Pipeline](#️-discovery-pipeline).*

---

## 🥇 Top Picks (Tier S)

The crown jewels: real Linux gaps + feasible ports. Highlights from the [full catalog](#-full-catalog-by-category) below, where every row lives in one category.

| Score | App | What it is | Code | Why port it first |
|:--:|---|---|---|---|
| **8** | [**Aegis Authenticator**](https://github.com/beemdevelopment/Aegis) [🤖](https://f-droid.org/packages/com.beemdevelopment.aegis/) | TOTP/2FA vault with encrypted export, groups, icons | ☕ Java · GPL-3 · ⭐13.5k | No good Linux 2FA GUI exists, yet desktop workflows (SaaS logins, admin work) need TOTP daily. Vault + export logic is portable; UI rebuilt around `libsecret`/GNOME Keyring. |
| **8** | [**Gadgetbridge**](https://codeberg.org/Freeyourgadget/Gadgetbridge) [🤖](https://f-droid.org/packages/nodomain.freeyourgadget.gadgetbridge/) | The universal FOSS companion for 100+ smartwatches/bands (PineTime, Amazfit, Mi Band…) | ☕ Java · GPL-3 · ⭐~4k | The *only* FOSS wearable manager worth the name — and Linux has almost nothing ([Watchmate](https://github.com/azymohliad/watchmate) covers PineTime only). Porting the BLE drivers onto `bluez` + a GTK control panel would give Linux a wearable hub. |
| **8** | [**Tasks.org**](https://github.com/tasks/tasks) [🤖](https://f-droid.org/packages/org.tasks/) | Astrid-descendant CalDAV task manager (subtasks, geofences, widgets) | ▲ Kotlin · GPL-3 · ⭐5.7k | CalDAV **VTODO** on Linux is a wasteland: GNOME Tasks is minimal, Thunderbird's task pane feels bolted on. The sync/cal4j logic is plain JVM — very desktop-friendly. |
| **8** | [**My Expenses**](https://github.com/mtotschnig/MyExpenses) [🤖](https://f-droid.org/packages/org.totschnig.myexpenses/) | Mature multi-account finance manager: budgets, CSV import, planning | ▲ Kotlin · GPL-3 · ⭐1.2k | Linux accounting = GnuCash (powerful but dated) or web apps. A modern native FOSS finance app has a clear audience; the data layer (SQLite + CSV) is portable as-is. |
| **7** | [**Organic Maps**](https://github.com/organicmaps/organicmaps) [🤖](https://f-droid.org/packages/app.organicmaps/) | Privacy-first **offline** OSM maps with turn-by-turn routing | C++ core · Apache-2.0 · ⭐16k | Offline routing on Linux genuinely doesn't exist (GNOME Maps needs network). The C++ core is already cross-platform — the port is mostly a new desktop UI shell. Big project, high impact. |
| **7** | [**AntennaPod**](https://github.com/AntennaPod/AntennaPod) [🤖](https://f-droid.org/packages/de.danoeh.antennapod/) | Gold-standard FOSS podcast manager (chapters, speeds, gpodder sync) | ☕ Java · GPL-3 · ⭐8.3k | Linux podcast clients (gPodder, Vocal) lag far behind. Networking + RSS/subscription logic is portable; playback is `gstreamer`/`mpv`-friendly. |
| **7** | [**Loop Habit Tracker**](https://github.com/iSoron/uhabits) [🤖](https://f-droid.org/packages/org.isoron.uhabits/) | Habit streaks with beautiful heatmaps | ▲ Kotlin · GPL-3 · ⭐10k | Nearly pure-Kotlin core (well tested) + no first-class Linux habit app. Begs for a GTK companion + reminders via systemd timers. |
| **7** | [**medTimer**](https://github.com/Futsch1/medTimer) [🤖](https://f-droid.org/packages/com.futsch1.medtimer/) | Privacy-respecting medication reminders & adherence history | ▲ Kotlin · MIT · ⭐650 | Medication adherence is a real daily gap; desktop adds calendar/CalDAV integration and laptop-resident reminders. MIT keeps friction low. Small enough for a first port. |
| **7** | [**Image Toolbox**](https://github.com/T8RIN/ImageToolbox) [🤖](https://f-droid.org/packages/ru.tech.imageresizershrinker/) | Swiss-army image suite: crop, filters, OCR, upscaling, background removal | ▲ Kotlin (Compose) · Apache-2.0 · ⭐15.5k | Between GIMP's mountain and Pinta's basics there's a "do it in two clicks" gap. Built on Compose → the natural road is Compose Multiplatform (official Linux desktop target). |
| **7** | [**Mihon**](https://github.com/mihonapp/mihon) | Manga/webtoon/comics reader — the de-facto successor of Tachiyomi, with a source-plugin ecosystem | ▲ Kotlin (Compose) · Apache-2.0 · ⭐25.2k | **No serious FOSS desktop manga reader exists.** The source-API layer is plain Kotlin + SQLite; UI is Compose → Path B. One of the most-requested community ports anywhere. Keep it content-source-agnostic like upstream. |
| **7** | [**Feeel**](https://gitlab.com/enjoyingfoss/feeel) [🤖](https://f-droid.org/packages/com.enjoyingfoss.feeel/) | Home-workout coach with exercise library (offline, private) | 🐦 Flutter (Dart) · AGPL-3 · ⭐~100 | Flutter has a **first-class Linux target** — the cheapest real port on this list, perfect with a second monitor. ⚠️ Upstream is slow; consider adopting it. |
| **6** | [**Transportr**](https://github.com/grote/Transportr) [🤖](https://f-droid.org/packages/de.grobox.liberario/) | FOSS public-transit assistant (routing + live departures, no tracking) | ▲ Kotlin · GPL-3 · ⭐1.2k | Desktop FOSS transit with live departures is rare; a panel-applet departure board would be lovely. Depends on external timetable backends (fragility risk). |
| **6** | [**GreenStash**](https://github.com/Pool-Of-Tears/GreenStash) [🤖](https://f-droid.org/packages/com.starry.greenstash/) | Goal-based savings planner with transaction log | 🐦 Flutter (Dart) · MIT · ⭐800 | Financial micro-apps ("save for X by date") fill a slot spreadsheets kill with friction. Flutter → Linux is quick. |
| **6** | [**OsmAnd+**](https://github.com/osmandapp/OsmAnd) [🤖](https://f-droid.org/packages/net.osmand.plus/) | Power-user offline maps (plugins, GPX, contour maps) | ☕ Java + native · GPL (core) · ⭐6.1k | Same gap as Organic Maps with an even richer but tangled codebase and mixed licenses — treat as a community port, not a starter one. |

---

## 📖 Full Catalog (by category)

Same analysis as the top picks; rows sorted by score within each category. Tough-call applicants that fail criteria live further below in the [anti-lists](#-dont-bother--already-solved-on-desktop).

### Security & 2FA

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| **8** | [Aegis Authenticator](https://github.com/beemdevelopment/Aegis) [🤖](https://f-droid.org/packages/com.beemdevelopment.aegis/) | #1 FOSS TOTP vault: encrypted backups, groups, icons | ☕ Java · GPL-3 · ⭐13.5k | Rebuild UI; hook secrets into `libsecret`/GNOME Keyring. Its encrypted-backup format is a killer interop feature to keep. |
| 5 | [Keyguard](https://github.com/AChep/keyguard-app) `reference` | Bitwarden-compatible, offline-first password vault | ▲ Kotlin (**Compose Multiplatform**) · ⚠️ source-available (personal-use license, not FOSS) · ⭐3.6k | **Already ships Linux** (Flathub/AUR/AppImage) — cited only as the KMP-architecture gold standard. Its license means it doesn't qualify for the catalog itself. |
| 4 | [2FAS](https://github.com/twofas/2fas-android) | Polished TOTP app + browser-extension pairing flow | ▲ Kotlin (Compose) · GPL-3 · ⭐5k+ | Its browser-extension approach shows what good desktop 2FA UX looks like — study the design even if you port Aegis. |
| 3 | [FreeOTP](https://github.com/freeotp/freeotp-android) [🤖](https://f-droid.org/packages/org.fedorahosted.freeotp/) | Red Hat's minimal TOTP app | ☕ Kotlin · Apache-2.0 | Aegis covers it; only worth a port if you want a deliberately tiny native GTK companion. |

### Wearables & Connected Hardware

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| **8** | [Gadgetbridge](https://codeberg.org/Freeyourgadget/Gadgetbridge) [🤖](https://f-droid.org/packages/nodomain.freeyourgadget.gadgetbridge/) | Companion hub for smartwatches & bands: sync, data export, firmware flashing | ☕ Java · GPL-3 · ⭐~4k | Port device drivers to `bluez`; UI as a GTK/KDE panel. Start device-by-device (PineTime first — [Watchmate](https://github.com/azymohliad/watchmate) is the proof). |
| 4 | [Watchmate](https://github.com/azymohliad/watchmate) `reference` | PineTime InfiniTime companion **for Linux already** | Rust · GPL-3 · ⭐170 (Flathub) | A tiny Rust/GTK4/BlueZ app that proves a desktop wearable companion is viable and wanted — a good blueprint for Gadgetbridge's port. |

### Tasks, Habits & Time

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| **8** | [Tasks.org](https://github.com/tasks/tasks) [🤖](https://f-droid.org/packages/org.tasks/) | CalDAV-native tasks: subtasks, geofences, OAuth sync | ▲ Kotlin · GPL-3 · ⭐5.7k | CalDAV VTODO sync core is JVM-portable; target libadwaita + Thunderbird/calendar interop. |
| **7** | [Loop Habit Tracker](https://github.com/iSoron/uhabits) [🤖](https://f-droid.org/packages/org.isoron.uhabits/) | Habit heatmap app with clean data model | ▲ Kotlin · GPL-3 · ⭐10k | Split core/UI; ship a GTK app + systemd-user-timer reminders. |
| 6 | [Etar Calendar](https://github.com/Etar-Group/Etar-Calendar) [🤖](https://f-droid.org/packages/ws.xsoh.etar/) | Material fork of AOSP Calendar (CalDAV via provider) | ☕ Java · GPL-3 · ⭐2.6k | Desktop partly solved by GNOME Calendar/Thunderbird — mid priority; useful as CalDAV parity reference. |
| 4 | [Suntimes](https://github.com/forrestguice/SuntimesWidget) [🤖](https://f-droid.org/packages/com.forrestguice.suntimeswidget/) | Sun/moon almanac: rises, solstices, golden hour | ☕ Java · GPL-3 · ⭐450 | Small, easy port; nice waybar/GNOME-shell companion. Low urgency. |

### Notes & Writing

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| 6 | [Notally](https://github.com/OmGodse/Notally) [🤖](https://f-droid.org/packages/com.omgodse.notally/) | Minimalist structured notes (checklists, labels, pinned) | ▲ Kotlin (Compose) · GPL-3 · ⭐2.2k | The "fast structured notes" niche between sticky notes and full PKM. Compose Multiplatform is the natural path. |
| 5 | [Saber](https://github.com/saber-notes/saber) `reference` | Handwritten notes with Nextcloud sync | 🐦 Flutter · GPL-3 · ⭐5k | **Already ships Linux** — kept only as a template: proof pen-input Flutter apps port cleanly. |
| 4 | [Markor](https://github.com/gsantner/markor) [🤖](https://f-droid.org/packages/net.gsantner.markor/) | Markdown / todo.txt / plain-text editor | ☕ Java · GPL-3+ (mixed parts) · ⭐6.4k | Desktop text editors are saturated; Markor shines mostly because Android lacks them. License has non-standard parts — verify before reusing code. |

### Health & Fitness

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| **7** | [medTimer](https://github.com/Futsch1/medTimer) [🤖](https://f-droid.org/packages/com.futsch1.medtimer/) | Medication reminders, adherence history, logging | ▲ Kotlin · MIT · ⭐650 | Best "small but daily" port: MIT + Kotlin, and desktop reminders matter even more than phone ones. |
| **7** | [Feeel](https://gitlab.com/enjoyingfoss/feeel) [🤖](https://f-droid.org/packages/com.enjoyingfoss.feeel/) | Home-workout coach, 700+ exercise animations | 🐦 Flutter · AGPL-3 | `flutter build linux` gets you 80%; the workout animations need Lottie/Rive care. Slow upstream — adopt it. |
| 6 | [OpenTracks](https://codeberg.org/OpenTracksApp/OpenTracks) [🤖](https://f-droid.org/packages/de.dennisguse.opentracks/) | Private GPS sport-tracking with dashboards | ☕ Java · Apache-2.0 · ⭐1.4k | Phone-sensor-centric → partial port: track files, stats, and GPX/WebDAV export are the valuable desktop half. |
| 5 | [FitoTrack](https://codeberg.org/jannis/FitoTrack) [🤖](https://f-droid.org/packages/de.tadris.fitness/) | Offline workout logger (runs, cycling, HIIT) | ☕ Java · GPL-3 · ⭐~500 | Same caveat as OpenTracks; the analysis dashboard is the portable half. |

### Maps & Navigation

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| **7** | [Organic Maps](https://github.com/organicmaps/organicmaps) [🤖](https://f-droid.org/packages/app.organicmaps/) | Offline maps + turn-by-turn routing, zero tracking | C++ core · Apache-2.0 · ⭐16k | Core is cross-platform; port = new desktop UI shell (GTK4/Qt6). Big project, big payoff — read their issue tracker for upstream desktop discussions first. |
| 6 | [OsmAnd+](https://github.com/osmandapp/OsmAnd) [🤖](https://f-droid.org/packages/net.osmand.plus/) | Power-user offline maps (plugins, contour maps, GPX) | ☕ Java + native · GPL (core) · ⭐6.1k | Same goal, larger scope, mixed licenses — community-scale port, not a starter one. |
| 6 | [Transportr](https://github.com/grote/Transportr) [🤖](https://f-droid.org/packages/de.grobox.liberario/) | FOSS public-transit routing & live departures | ▲ Kotlin · GPL-3 · ⭐1.2k | Backend (öffi/GTFS wrappers) is portable Kotlin; UI must be rebuilt. |
| 3 | [StreetComplete](https://github.com/streetcomplete/StreetComplete) | Gamified OSM surveying (walk + answer quests) | ▲ Kotlin · GPL-3 · ⭐5.1k | Intrinsically outdoor-mobile — **not** a port target; contribute upstream instead. |

### Personal Finance

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| **8** | [My Expenses](https://github.com/mtotschnig/MyExpenses) [🤖](https://f-droid.org/packages/org.totschnig.myexpenses/) | Multi-account finance manager: budgets, transfers, CSV, sync | ▲ Kotlin · GPL-3 · ⭐1.2k | Strong desktop gap. SQLite + CSV + planning logic sidesteps most Android-isms. |
| 6 | [GreenStash](https://github.com/Pool-Of-Tears/GreenStash) [🤖](https://f-droid.org/packages/com.starry.greenstash/) | Savings-goal tracker with milestones | 🐦 Flutter · MIT · ⭐800 | Fast Flutter port; a tray applet for milestone nudges would complete it. |
| 5 | [Zeus](https://github.com/ZeusLN/zeus) | Self-custodial Bitcoin/Lightning wallet + LND/Core Lightning remote-node manager (Android + iOS) | TypeScript (React Native) · AGPL-3 · ⭐1.4k | The one verified cross-phone FOSS desktop gap (details in [Platform Reality](#-platform-reality--ios--foss)) — desktop node dashboard is the honest target, wallet core stays. |
| 4 | [Counted](https://github.com/counted-labs/counted) [🤖](https://f-droid.org/packages/fr.counted.app/) | Split-expenses with E2E-encrypted groups (no accounts, 150+ currencies) | 🐦 Flutter · AGPL-3 | Desktop helps laptop "split-the-bill" flows. ⚠️ Depends on the non-free counted.fr server (F-Droid anti-feature) — port only with a self-hostable backend story. |
| 3 | [piggybudget](https://github.com/pmiddend/piggybudget) [🤖](https://f-droid.org/packages/de.php_tech.piggybudget/) | Dead-simple expense tracker | ☕ Kotlin · GPL-3 · ⭐~100 | Tiny, last updated 2019 — a good "learn the porting workflow" exercise, nothing more. |

### Podcasts, Music & Media

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| **7** | [AntennaPod](https://github.com/AntennaPod/AntennaPod) [🤖](https://f-droid.org/packages/de.danoeh.antennapod/) | Best-in-class FOSS podcasts: speeds, chapters, gpodder sync | ☕ Java · GPL-3 · ⭐8.3k | Subscription/RSS/network logic is portable; playback shell is `gstreamer`/`mpv`-friendly. |
| 5 | [Voice](https://github.com/PaulWoitaschek/Voice) [🤖](https://f-droid.org/packages/de.ph1b.audiobook/) | Calm, polished audiobook player (speed, sleep timer, bookmarks) | ▲ Kotlin · GPL-3 · ⭐3.2k | Desktop audiobook players are scarce; playback layer is easy, library/db logic portable. |
| 4 | [Gramophone](https://github.com/FoedusProgramme/Gramophone) | Sane local-music player; karaoke-precision synced lyrics (LRC/TTML/SRT) + ReplayGain 2.0 | ▲ Kotlin · GPL-3 · ⭐2.4k | Built strictly on Android plumbing (MediaStore, system codecs) → the port becomes a *fresh* GTK player that reuses its lyrics/replaygain logic. Small but beloved niche. |
| 4 | [Auxio](https://github.com/OxygenCobalt/Auxio) [🤖](https://f-droid.org/packages/org.oxycblt.auxio/) | Beautiful local-music library player | ▲ Kotlin · GPL-3 · ⭐4.4k | Linux has Amberol/Lollypop in this niche — port only if you love the app. |
| 2 | [Seal](https://github.com/JunkFood02/Seal) [🤖](https://f-droid.org/packages/com.junkfood.seal/) | yt-dlp GUI with audio tagging options | ▲ Kotlin (Compose) · GPL-3 · ⭐30k+ | [Parabolic](https://github.com/NickvisionApps/Parabolic) already covers the desktop — listed so nobody ports it twice. |

### Reading, Comics & RSS

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| **7** | [Mihon](https://github.com/mihonapp/mihon) | Manga/webtoon/comics reader with source-plugin ecosystem and tracker sync | ▲ Kotlin (Compose) · Apache-2.0 · ⭐25.2k | Biggest community in this catalog. No serious FOSS desktop manga reader exists; the source-API layer is plain Kotlin networking + SQLite. ⚠️ Keep the app content-source-agnostic like upstream. *(Kotatsu, the other big name, was archived in 2025 — avoid.)* |
| 5 | [Read You](https://github.com/ReadYouApp/ReadYou) [🤖](https://f-droid.org/packages/me.ash.reader/) | Gorgeous Material You RSS client (FreshRSS/Feedly/Local) | ▲ Kotlin (Compose) · GPL-3 · ⭐7.6k | Desktop readers exist (NewsFlash) but nothing this pretty on Linux; Compose Multiplatform could serve both targets. |
| 5 | [Feeder](https://github.com/spacecowboy/Feeder) [🤖](https://f-droid.org/packages/com.nononsenseapps.feeder/) | Offline-first RSS with filters & article-extraction | ▲ Kotlin · GPL-3 · ⭐3.1k | Parsing/extraction logic is portable; pair with a GTK shell. |
| 3 | [Librera Reader](https://github.com/foobnix/LibreraReader) | All-format PDF/EPUB power reader | ☕ Java/C · custom license · ⭐5k | ⚠️ License isn't OSI-clean — skip unless it loosens. |
| 2 | [KOReader](https://github.com/koreader/koreader) `reference` | Runs-everywhere ebook reader (PDF/EPUB/DjVu…) | Lua · AGPL-3 · ⭐31k | **Already runs on Linux desktops** — listed as a cheat code if you want its UX as a starting base. |

### Images & Photos

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| **7** | [Image Toolbox](https://github.com/T8RIN/ImageToolbox) [🤖](https://f-droid.org/packages/ru.tech.imageresizershrinker/) | One-stop image utility: crop, filters, OCR, upscale, bg-removal | ▲ Kotlin (Compose) · Apache-2.0 · ⭐15.5k | Most technically plausible Compose Multiplatform port here. Split the manipulation core into a library first. |
| 3 | [Binary Eye](https://github.com/markusfisch/BinaryEye) | Barcode/QR scanner with history + generator | ▲ Kotlin · MIT · ⭐2.5k | Camera-bound; but the *generator* half could become a small Linux tray tool (`zxing-cpp` bindings exist). |
| 2 | [Open Camera](https://sourceforge.net/p/opencamera/code/) | Full-power FOSS camera | ☕ Java · GPL-3 | Camera pipeline is phone-bound; desktop cameras are a solved niche. |

### Utilities & System

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| 5 | [Neo Store](https://github.com/NeoApplications/Neo-Store) [🤖](https://f-droid.org/packages/com.machiav3lli.fdroid/) | Polished F-Droid client | ▲ Kotlin · GPL-3 · ⭐5.6k | Android-bound (installs APKs) — but its index/metadata logic could power a proper **desktop F-Droid browser** (search, browse, track updates), which is a real gap. |
| 5 | [Material Files](https://github.com/zhanghai/MaterialFiles) | Clean file manager with SFTP | ▲ Kotlin · GPL-3 · ⭐9.4k | Desktop managers exist (Nautilus/Dolphin) — listed as a UX reference, not a port target. |
| 4 | [WiFi Analyzer](https://github.com/VREMSoftwareDevelopment/WiFiAnalyzer) [🤖](https://f-droid.org/packages/com.vrem.wifianalyzer/) | Wi-Fi spectrum analyzer UI | ▲ Kotlin · GPL-3 · ⭐5k | Only meaningful on laptops in monitor mode via `iw`; a GTK+iwlib shell is possible. Niche. |
| 2 | [Obtainium](https://github.com/ImranR98/Obtainium) | "Install apps straight from GitHub releases" | 🐦 Flutter · GPL-3 · ⭐21k | Android-bound; the *tracking* layer would map to a desktop release-notifier — modest value. |

### Games & Emulation

| Score | App | What it is | Code | Porting notes |
|:--:|---|---|---|---|
| 2 | [Lemuroid](https://github.com/Swordfish90/Lemuroid) [🤖](https://f-droid.org/packages/com.swordfish.lemuroid/) | Gorgeous libretro front-end | ▲ Kotlin · GPL-3 · ⭐4.5k | RetroArch already strong on Linux; only a UX-differentiated front-end would matter. |
| 2 | [RetroArch](https://github.com/libretro/RetroArch) `reference` | The emulation standard | C · GPL-3 | Already desktop — listed so nobody "ports" it. |

---

## 🚫 Don't Bother — Already Solved on Desktop

Great apps, but Linux already has a first-class answer. Recorded here so effort goes where it's actually missing.

| Mobile app | Use this on desktop instead |
|---|---|
| NewPipe | [FreeTube](https://github.com/FreeTubeApp/FreeTube) |
| Thunderbird Android (K-9) | Thunderbird desktop |
| FairEmail | Thunderbird desktop |
| Conversations (XMPP) | [Dino](https://github.com/dino/dino), [Gajim](https://dev.gajim.org/gajim/gajim) |
| Element / matrix clients | Element desktop, [Fractal](https://gitlab.gnome.org/GNOME/fractal) |
| SimpleX Chat | SimpleX Desktop (official) |
| Briar | Briar Desktop (official) |
| AnkiDroid | [Anki desktop](https://github.com/ankitects/anki) |
| Bitwarden, KeePassDX | Bitwarden desktop, [KeePassXC](https://github.com/keepassxreboot/keepassxc) |
| Syncthing-Fork | [Syncthing](https://github.com/syncthing/syncthing) (first-class desktop) |
| KDE Connect | KDE Connect desktop (ships with KDE) |
| LocalSend | LocalSend ships Linux |
| Snapdrop / quick file-drip apps | [Warpinator](https://github.com/linuxmint/warpinator), Warp |
| Collabora / OnlyOffice / OpenDocument Reader | LibreOffice, OnlyOffice Desktop |
| Kiwix, Wikipedia app | Kiwix desktop, Wikipedia web |
| Fossify Calendar / Contacts / Etar | GNOME Calendar / Contacts, Thunderbird Calendar |
| Material Files, Fossify Files | Nautilus, Dolphin, Thunar, Nemo |
| Tusky (Fediverse) | [Tuba](https://github.com/GeopJr/Tuba), Mastodon web |
| Obsidian-style PKM (Joplin, Logseq, Notesnook) | Joplin / Logseq / Notesnook all ship desktop |
| Mobile emulators (PPSSPP, Dolphin, RetroArch) | Same devs ship native desktop builds |
| Signal / Session / Delta Chat | Official desktop clients exist |
| YouTube Music clients (InnerTune, Metro) | [th-ch/youtube-music](https://github.com/th-ch/youtube-music) (active, fully FOSS desktop YTM player) |
| KitchenOwl (grocery lists) | KitchenOwl ships native desktop/web builds upstream |
| Ice Cubes (Mastodon, iOS-native) | Ships iOS **and** macOS natively; Linux gets Tuba, Fediverse web covers the rest |
| Damus (Nostr, iOS-native) | Ships iOS **and** macOS natively; Linux has several nostr clients + web clients to fill the remaining gap |
| YouTube downloaders | yt-dlp + [Parabolic](https://github.com/NickvisionApps/Parabolic) |

## 🔒 Device-Bound — Porting Makes No Sense

These depend on phone-only plumbing (VpnService, AccessibilityService, PackageManager, camera/GPS sensors, APK install/Keystore), so a desktop port would hollow them out:

- **Firewalls/trackers:** NetGuard, RethinkDNS, TrackerControl, AFWall+ — desktop firewalls already exist.
- **Automation:** Key Mapper, Easer — live on Accessibility/InputMethod plumbing.
- **App stores & device mgmt:** Neo Store, Droid-ify, Obtainium, App Manager, Neo Backup, Shizuku — they install/manipulate Android packages. *(iOS analogs: [SideStore](https://github.com/SideStore/SideStore), Feather — same verdict, same reasoning.)*
- **Sensor apps:** Sky Map, phyphox, OpenTracks/FitoTrack (GPS), Open Camera, Binary Eye (camera) — the *phone* is the instrument. *(Partials worth extracting are flagged in the [catalog](#-full-catalog-by-category).)*
- **Bridge apps (phone ↔ world) — port the *other* end instead:** [SmsForwarder](https://github.com/pppscn/SmsForwarder) (⭐28.8k, BSD-2 — forwards SMS/calls/notifications to Telegram/email/webhook), KDE Connect, phone-as-webcam tools, tasker-bridges. The Android side should stay; what's missing on Linux is a clean **receiver/server CLI + tray**. If a bridge has no desktop receiver, build that — don't port the phone app.

## 📚 Lessons From Ports That Already Happened

Nobody should argue from first principles. These shipped, and each one leaves a trace of guidance:

| Case | Stack | What actually made it work | Lesson for this list |
|---|---|---|---|
| **[Saber](https://github.com/saber-notes/saber)** (notes) | Flutter | One codebase, `flutter build linux`, pen input *was* the product | Flutter candidates here are weeks, not months, from "ships Linux" |
| **[Keyguard](https://github.com/AChep/keyguard-app)** (passwords) | KMP + Compose MP + Rust | Module-per-platform facade + shared core | Compose Multiplatform is the current bar for "same UI, two worlds" |
| **[KOReader](https://github.com/koreader/koreader)** (ebooks) | Lua + portable base layer | Document/rendering layer kept separate from device plumbing | Write UI against an abstraction — desktop falls out free |
| **[LocalSend](https://github.com/localsend/localsend)** (file drop) | Flutter | Protocol lives in a package; platform transports beneath it | Extract *protocols*, not activities |
| **[Parabolic](https://github.com/NickvisionApps/Parabolic)** (video dl) | GTK libadwaita | Reuses the `yt-dlp` CLI as the brain | Sometimes the right port is a **new app around the same backend**, not moving the Android code |
| **[Organic Maps' trajectory](https://github.com/organicmaps/organicmaps)** (maps) | C++ core + native shells | Kept tiles/routing cross-platform, rebuilt UI per platform | Port D done right at giant scale — check upstream's desktop plan before duplicating |

## 🛠️ Porting Playbook

Pick a candidate by the *route you're able to walk*, not by category. The four routes below each carry a **candidate index** — the same apps from the catalog, grouped by how they would actually be ported.

### Path A — Flutter app → `flutter build linux`

Cheapest ports: same framework, one codebase, official Linux target.

| App | Score | Status |
|---|:--:|---|
| [Feeel](https://gitlab.com/enjoyingfoss/feeel) | 7 | 🟢 ideal first port (upstream slow → adopt) |
| [GreenStash](https://github.com/Pool-Of-Tears/GreenStash) | 6 | 🟢 small, MIT |
| [Counted](https://github.com/counted-labs/counted) | 4 | 🚧 non-free server dependency first |

*Proof it works:* Saber, LocalSend, KitchenOwl — all Flutter apps that already ship Linux.

**Plumbing to polish:** near-native theming, window titlebar, tray/applet, `.desktop` + AppStream metadata. **Ship to:** Flathub first.

### Path B — Kotlin (Compose) app → Compose for Desktop

Same UI language, official multiplatform target, Skia rendering. Production-ready on Linux; networking, serialization, `SQLDelight`/`Ktor`, `jvm-sqlite` all port cleanly.

| App | Score | Status |
|---|:--:|---|
| [Image Toolbox](https://github.com/T8RIN/ImageToolbox) | 7 | 🟡 extract the image-manipulation core first |
| [Mihon](https://github.com/mihonapp/mihon) | 7 | 🟡 biggest community here; keep it source-agnostic |
| [medTimer](https://github.com/Futsch1/medTimer) | 7 | 🟢 small; MIT makes it painless |
| [Notally](https://github.com/OmGodse/Notally) | 6 | 🟢 small Compose surface |
| [Read You](https://github.com/ReadYouApp/ReadYou) | 5 | 🟢 medium; keep phone + desktop twins |

*Proof it works:* Keyguard (KMP/CMP reinforced with Rust) ships Flathub/AUR/AppImage.

**Cost center — Android API replacements:**

| Android | Desktop |
|---|---|
| `Room` | `SQLDelight`, or plain `sqlite-jdbc` |
| `WorkManager` | systemd user timers / cron |
| `SharedPreferences` | JSON store in `~/.config` |
| Keystore / biometrics | `libsecret` / GNOME Keyring |
| Notifications | `libnotify` |
| Intents / deep links | D-Bus activation |

**Distribute:** Gradle `jpackage` or Flatpak.

### Path C — JVM logic reuse + toolkit-native shell (GTK4/libadwaita, Qt6)

These apps are ordinary Java/Kotlin logic underneath: models, SQLite, and the actual "language" of the app (CalDAV, RSS, podcast feeds) port as-is — only the Android UI dies. Extract the Model/Service/Repository layers (they run on the JVM unchanged), then rebuild the UI.

| App | Score | What keeps value |
|---|:--:|---|
| [Aegis](https://github.com/beemdevelopment/Aegis) | 8 | encrypted vault interop |
| [Gadgetbridge](https://codeberg.org/Freeyourgadget/Gadgetbridge) | 8 | device drivers → `bluez` |
| [Tasks.org](https://github.com/tasks/tasks) | 8 | CalDAV VTODO sync core |
| [My Expenses](https://github.com/mtotschnig/MyExpenses) | 8 | account/budget/CSV model |
| [AntennaPod](https://github.com/AntennaPod/AntennaPod) | 7 | feeds/sync/player backend |
| [Loop Habit Tracker](https://github.com/iSoron/uhabits) | 7 | streak data model + stats |
| [Transportr](https://github.com/grote/Transportr) | 6 | timetable-routing wrappers |
| [Etar](https://github.com/Etar-Group/Etar-Calendar) | 6 | CalDAV parity reference |
| [Voice](https://github.com/PaulWoitaschek/Voice) | 5 | library model |
| [Feeder](https://github.com/spacecowboy/Feeder) | 5 | feed parsing/extraction |
| [Suntimes](https://github.com/forrestguice/SuntimesWidget) | 4 | almanac math |
| [WiFi Analyzer](https://github.com/VREMSoftwareDevelopment/WiFiAnalyzer) | 4 | `iw`-layer visuals |

### Path D — C/C++ core + brand-new shell

The heavyweight ring — only when the core is the crown. Keep the computational core (vector tiles, routing, emulators); build a fresh desktop UI over IPC.

| App | Score | Core |
|---|:--:|---|
| [Organic Maps](https://github.com/organicmaps/organicmaps) | 7 | vector tiles + routing |
| [OsmAnd+](https://github.com/osmandapp/OsmAnd) | 6 | same, richer |

**Advice:** check upstream's own desktop plans and contribute momentum instead of forking the maintenance completely.

### Choosing a toolkit

| Toolkit | Best when… | License | Watch out for |
|---|---|---|---|
| **GTK4 + libadwaita** (Vala, Rust/[Relm4](https://github.com/Relm4/Relm4), [PyGObject](https://pygobject.readthedocs.io/)) | You want a GNOME-native look; small/tray apps; Path C logic + shell | LGPL | Build a KDE twin with Qt if you commit to one DE only |
| **Compose for Desktop** | Source app is Compose (Path B); you want identical UI across phone+desktop | Apache-2.0 | Skia draws its own style — not GTK/KDE native; heavier RAM |
| **Flutter** | Source app is Flutter (Path A) | BSD-3 | Desktop widgets are Flutter's least-mature tier; don't expect a GTK-like feel |
| **Qt6 / QML** | C++ core exists (Path D); KDE-first | LGPL (free) | Design the shell around KDE patterns, not Android ones |
| **Tauri / Electron** | The shared logic is Node-friendly (e.g. React Native); you're wrapping, not porting | MIT / permissive | Ship only if a wrapper beats a browser tab: offline mode, tray, global keybinds — otherwise don't |
| **SwiftUI / Swift** | Source app is iOS-native (Catalyst keeps it macOS-only); you want a macOS twin | MIT (tooling) / Swift is open | SwiftUI targets only Apple platforms — a Linux/Win port means a different toolkit + new UI; treat iOS-native apps as macOS-twins, not Linux ports |

**Decision heuristic:** *the source app's framework wins by default* (Path A/B); if the UI must be rebuilt anyway (Path C), prefer native GNOME/KDE for polish and frictionless distribution.

### Universal desktop-extras checklist

- [ ] Tray/`StatusNotifier` icon + app menu
- [ ] `.desktop` file, AppStream metainfo, SVG icon
- [ ] Flathub manifest + reproducible CI build
- [ ] Keyboard shortcuts + basic a11y
- [ ] `xdg-open` / file-manager integration
- [ ] A short doc (or upstream issue) declaring how the port will be maintained

## Evaluating a New Candidate

Verify before adding:

| Question | How to check |
|---|---|
| License still OSI-clean? | `api.github.com/repos/{owner}/{repo}` → `license.spdx_id` |
| Active? | `pushed_at` within ~12 months |
| Android-locked? | Grep the repo for `VpnService`, `AccessibilityService`, `InputMethodService`, `PackageManager`, `BiometricPrompt` |
| Desktop already exists? | Search Flathub + this README's solved-list first |
| Community mass? | Stars are weak signals, but `<100 ⭐` + `<5 forks` = contact upstream before adopting |

## 🕵️ Discovery Pipeline

The catalog decays every month: apps get ports (→ solved), apps get archived (→ drop), new gems appear. Re-run the sweep with these sources:

| Source | What to harvest | Cadence |
|---|---|---|
| **[F-Droid: recently updated](https://f-droid.org/en/packages/)** | New FOSS apps as they're indexed | monthly |
| **[IzzyOnDroid](https://apt.izzysoft.de/fdroid/index.php)** | FOSS apps that haven't reached main F-Droid yet (fastest signal) | monthly |
| **[Fossify org](https://github.com/orgs/FossifyOrg/repositories)** | The Simple Mobile Tools successor suite — watch which expose desktop gaps | each release |
| **GitHub topic search**: [`topic:android language:kotlin license:gpl-3.0`](https://github.com/search?q=topic%3Aandroid+language%3Akotlin+license%3Agpl-3.0&type=repositories) (and `dart`) | Long-tail candidates ranked by stars | quarterly |
| **[dkhamsing/open-source-ios-apps](https://github.com/dkhamsing/open-source-ios-apps)** | The canonical iOS FOSS index — filter for cross-phone frameworks (Flutter/KMP/RN); those are the iOS candidates that can actually reach Linux | quarterly |
| **r/FOSSdroid**, [Lemmy FOSS Android](https://lemmy.world/c/fossdroid) | What users actually *wish* existed on desktop — complaints are candidate signals | ongoing |
| **[Flathub trending](https://flathub.org/apps/collection/trending)** | Android-category apps *arriving* — they graduate from this list the day they ship Linux | monthly |
| **Upstream roadmaps/issues** | Many projects have dormant "desktop?" issues — a nudge plus a PR can flip an app to solved | per candidate |

Keep the sweep budget honest: **add 3, verify 10, drop 2** beats a giant unreviewed dump every time.

## ❓ FAQ

**"Why not just run it in Waydroid/Anbox?"**
Because a container is a whole Android OS per workload: heavier startup, jankier multi-monitor behavior, no DE integration (tray, file dialogs, notifications), and it breaks on Wayland changes nobody upstream controls. This list's premise is *a native app you ship like every other Linux app*.

**"Why not just scrcpy the phone?"**
scrcpy is excellent — for *mirroring a phone you have next to you at that moment*. It doesn't survive the "laptop at a café, phone across town" workflow, nor app-level calendar/player widgets embedded in the desktop shell.

**"The app has a web version — doesn't that count?"**
Only if offline, tray presence, native notifications, keybindings, and file-dialog integration exist. KitchenOwl's desktop builds count; a Nextcloud web UI in a pinned tab does not.

**"Why rebuild the UI at all? Reusing the Compose/Flutter tree is little work."**
It usually is — and that's exactly why those apps are Path A/B. For Java-era apps (Aegis, AntennaPod, Gadgetbridge) the Android Activity/Fragment/Service layer *is* the app; the logic under it outlives it.

**"Scores look subjective."**
They are — deliberately quantized on a 0–3 scale so revision is cheap. Disagree? Open a PR with your `G/P/V` and one sentence of reasoning per axis.

## 🔗 Handy Resources

- [F-Droid](https://f-droid.org/en/packages/) — the FOSS Android app index and its categories
- [IzzyOnDroid](https://apt.izzysoft.de/fdroid/index.php) — pre-F-Droid FOSS apps, great discovery signal
- [Fossify](https://www.fossify.org) — the Simple Mobile Tools successor suite
- [Awesome Android FOSS (offa/android-foss)](https://github.com/offa/android-foss) — companion list: broad Android-FOSS coverage without the port angle
- [iOS open-source apps (dkhamsing)](https://github.com/dkhamsing/open-source-ios-apps) — companion index for the iOS side of this catalog
- [OpenAlternative](https://openalternative.co) / [Linux Alternative Project](https://linuxalt.com) — the desktop side of the comparison
- [Flathub](https://flathub.org) — always confirm a desktop gap exists here *before* starting a port

## 🤝 Contributing

1. **Verify** with the checklist above. Score `G/P/V` honestly — no self-promo inflation.
2. Pin the **primary** source (Codeberg/GitHub/GitLab), not a mirror.
3. ⚠️ Mark stale/archived projects; drop dead ones at the next sweep.
4. One row per app. If a desktop port lands, move the row into the **solved** table with a credit line.
5. Write **Why port / Porting notes** in full sentences — future-you reads this with fresh eyes.

## 📜 License

This catalog's text: [CC0 / Public Domain](https://creativecommons.org/publicdomain/zero/1.0/), same spirit as "awesome" lists. Each listed app keeps its own license — links point home.
