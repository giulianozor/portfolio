<div align="center">

# Giuliano Zorzi — Portfolio

<p align="center">
Open-source software built primarily in <strong>Go</strong>: system tooling, media utilities, and developer infrastructure.
</p>

</div>

---

## About

A collection of small, focused, single-purpose tools I build and maintain for real problems I hit in my own
workflow — media library management, self-hosted infrastructure, and everyday CLI utilities. Each project is
deliberately small, well-tested, and documented, with a `Makefile` for easy builds.

---

## Projects

### Media & Video

#### [tomp4](https://github.com/giulianozor/tomp4)
Batch-converts video files to the modern **MP4 (H.264/AAC)** container using FFmpeg.

- **Main features**: recursive directory scanning, skips already-compatible files, preserves audio/subtitles,
  optional **QSV hardware acceleration**, real-time progress table, dry-run/info modes, and source
  cleaning/organising after conversion.
- **Use case**: Standardising a large mixed media library into one universally compatible format.

#### [HandbrakeCLI-QSV](https://github.com/giulianozor/HandbrakeCLI-QSV)
Builds `HandBrakeCLI` from source inside an Alpine container with **Intel QSV** (`--enable-qsv`) encoding support.

- **Main features**: source build with intel-media-driver, oneVPL, x264 and libva; binary extracted straight to the host via
  `docker buildx --output type=local` (no compose or volume mounts); `make build` / `make install` / `make clean` targets
  with `HB_REF`, `OUTPUT_DIR` and `DOCKERFILE` overrides.
- **Use case**: Installing a HandBrakeCLI binary with hardware-accelerated Quick Sync encoding.

#### [AudiobookConverter](https://github.com/giulianozor/AudiobookConverter)
Converts an archive of MP3 chapters (ZIP/7z/RAR or a plain folder) into a **single M4B audiobook**.

- **Main features**: archive extraction, natural-sort chapter ordering, one chapter per MP3, AAC encoding,
  embedded cover art and metadata, live progress line, and bitrate/author/title overrides.
- **Use case**: Turning a multi-file MP3 audiobook or podcast series into one portable, chapter-navigable file.

#### [audio-tagger](https://github.com/giulianozor/audio-tagger)
Organises audio files by their **ID3 metadata** into an `Artist/Album/` folder layout.

- **Main features**: reads ID3 tags from `.mp3`/`.mp4`/`.m4b`, moves files into `output/Artist/Album/Title`,
  strips illegal characters for Windows compatibility.
- **Use case**: Cleaning up a disorganised music library into a browsable artist/album structure.

#### [videoinfo](https://github.com/giulianozor/videoinfo)
Prints detailed **technical metadata** for media files using FFmpeg libraries (libavformat/avcodec via cgo).

- **Main features**: per-stream codec, resolution, fps, bitrate, language, and chapter output.
- **Use case**: Quick inspection of a media file's technical details without opening a GUI editor.

#### [video-server](https://github.com/giulianozor/video-server)
A simple **HTTP file server** that serves a local directory over the network.

- **Main features**: plain HTTP serving, per-file download logging with speed metrics, and an `update.sh` helper.
- **Use case**: Streaming/serving a media library across a LAN or home network.
y tag or search across many sites with resume and dedup support.


---

### Servers and system tools

#### [localCA](https://github.com/giulianozor/localCA)
A **web app** for managing a local Certificate Authority and issuing internal server certificates.

- **Main features**: 100-year CA creation with optional intermediate CA, server, client, 802.1x, code signing certificate issuance with
  DNS/IP SANs, passphrase management, certificate revoke/renew, per-cert and whole-CA encrypted `tar.gz` export,
  CRL generation, and a multi-language UI (EN/IT/JA).
- **Use case**: Running a private CA for self-hosted infrastructure and issuing internal TLS certificates.

#### [unifi-route-table-updater](https://github.com/giulianozor/unifi-route-table-updater)
Lightweight **Go daemon** that keeps a UniFi static route in sync with a dynamic DNS hostname.

- **Main features**: periodic DNS → route comparison, UniFi Network API integration, optional Telegram notification,
  dry-run mode, and an OpenRC service unit for Alpine Linux.
- **Use case**: Automatically updating a DynDNS hostname route on UniFi gear as the public IP changes.

#### [TelegramAlert](https://github.com/giulianozor/TelegramAlert)
A lightweight **Go daemon** that monitors a folder for files and sends a Telegram alert when matching files are found.

- **Main features**: configurable age window for file detection, formatted Telegram messages via the Bot API, init.d service support, custom config file path, and configurable check interval.
- **Use case**: Notifying a Telegram chat when new or recently modified files appear in a monitored directory.

#### [luks-mount](https://github.com/giulianozor/luks-mount)
A **Go CLI** took that mounts, unmounts, creates and expands LUKS-encrypted devices and file-backed containers.

- **Main features**: automatic LUKS detection (`luksOpen`/`luksClose` for encrypted sources, direct mount for plain ones), passphrase or key-file unlocking, container creation with `luksFormat` + ext4, container expansion (`truncate` + `resize2fs`), and clear validation of sources, mount points, and key files.
- **Use case**: Managing encrypted drives and file-backed LUKS containers from the command line.

#### [filex](https://github.com/giulianozor/filex)
A fast, self-hosted web-based **file browser** with a dark theme, built in Go with zero external runtime dependencies.

- **Main features**: drag-and-drop multi-file upload manager with per-file progress/speed/ETA/cancel, in-browser text
  editor, inline previews (images/video/audio/text), video editor with thumbnail timeline and start/end marks,
  lossless interval clipping via ffmpeg stream copy (`-c copy`) streamed with live progress, per-video interval presets,
  thumbnail cache with batch generation, rename/delete/move (single or bulk), protected paths, favourite folder
  bookmarks, per-user path jails with bcrypt login, per-user UID/GID `chown`, and a mobile-responsive dark UI — all in
  a single binary with embedded assets.
- **Use case**: Running a private, multi-user file browser with per-user jails and lossless video clipping.

---

### Productivity & System Tools

#### [regex-renamer](https://github.com/giulianozor/regex-renamer)
Batch-renames files and folders using a chain of regex rules defined in **YAML**.

- **Main features**: multi-rule chaining, dry-run preview tables, interactive confirmation, recursive mode, per-rule
  `apply_to` (files/folders/both), and a summary output.
- **Use case**: Normalising filenames or applying consistent naming across a library.

#### [random-mover](https://github.com/giulianozor/random-mover)
Randomly selects and moves **N files** from one directory to another.

- **Main features**: random selection after shuffle, optional extension filter (`-ext`), and fast `os.Rename` with
  cross-filesystem fallback.
- **Use case**: Picking a random sample of files (e.g., a random subset of photos from a large set).

---

### Development Environment

#### [opencode-dev](https://github.com/giulianozor/opencode-dev)
A **Docker-based development container** for Go and OpenCode development, with VPN connectivity.

- **Main features**: builds a `golang:latest` image with git, wireguard-tools, ffmpeg, chromium, `gh` CLI, and
  OpenCode; mounts SSH keys, git config, and OpenCode config; grants VPN networking via `/dev/net/tun` and
  `NET_ADMIN`.
- **Use case**: A disposable, VPN-enabled dev environment for isolated remote development.

#### [opencode-alpine](https://github.com/giulianozor/opencode-alpine)
Builds a **static musl binary** of [opencode](https://github.com/anomalyco/opencode) for Alpine Linux using Docker `buildx`.

- **Main features**: source build from any git ref/version, patched build script so only the `linux x64 (musl)` target
  is produced, `scratch` stage that extracts just the binary via `--output type=local`, and `make build` / `make install` /
  `make clean` targets with `OUTPUT_DIR`, `OPENCODE_REF` and `OPENCODE_VERSION` overrides.
- **Use case**: Running opencode natively on Alpine and other musl-based environments where GLIBC binaries won't work.

---

### Games

#### [dungeon](https://github.com/giulianozor/dungeon)
A tile-based **dungeon maze game** with a web interface — roll the dice, traverse a randomly
generated grid of corridor tiles, and race to catch the goal before the other players.

- **Main features**: single player and multiplayer (2–4 players) modes, turn-based dice rolling with
  row/column slides, shared 9×6 board with distinct player tokens, goal teleport scoring with leaderboard,
  slideable rows/columns that change every turn, lobby/chat, and procedurally rendered stone-brick PNG tiles.
- **Use case**: Casual multiplayer party game over the network.

---

## Zenn Articles

In-depth technical write-ups — long-form,
run-an-example-first tutorials on Go systems programming, networking, and security. Each repo pairs a full article
with complete, runnable sample code.

#### [low-level-networking](https://github.com/gz-zenn/low-level-networking)
**Low-Level Networking in Go: Forging Packets, Decoding Bytes, and Building Custom Protocols**
Goes below `net.Conn` — encoding custom binary protocols over UDP/TCP, reading raw Ethernet frames with
`x/net/ipv4`, and hand-crafting IP/ICMP packets (including checksums) with `gopacket`.

#### [wasm](https://github.com/gz-zenn/wasm)
**Hardening Web Applications with WebAssembly: A Practical Security Approach**
Makes the case for WebAssembly as a security tool (not just a performance one): sandboxing untrusted code,
isolating memory, and running the same Go validator compiled to Wasm on both client and server.

#### [struct-tags](https://github.com/gz-zenn/struct-tags)
**Building Custom Struct Tags in Go: A Practical Guide**
Explains how struct tags work under the hood via `reflect`, then builds a working reflection-based `validate` tag
library for API request validation.

#### [tls-renew](https://github.com/gz-zenn/tls-renew)
**Automating TLS Certificate Renewal in Go with Cloudflare DNS-01 Validation**
Builds a Go ACME client with `go-acme/lego` that obtains and auto-renews (wildcard) Let's Encrypt certificates
using Cloudflare DNS-01 validation, with a daily expiry-check background loop.

#### [http3](https://github.com/gz-zenn/http3)
**Building HTTP/3 Services in Go**
Covers why HTTP/3/QUIC matters (0-RTT handshakes, no head-of-line blocking, connection migration) and stands up
production `http3` servers and clients with `quic-go`.

#### [p2p](https://github.com/gz-zenn/p2p)
**Building a Simple P2P / Multi-Node Service with LAN Auto-Discovery in Go**
Implements UDP multicast discovery (`239.0.0.0/8`) for nodes to find each other on a LAN, then TCP for reliable
messaging — complete, runnable, dependency-free example.

#### [pgp](https://github.com/gz-zenn/pgp)
**Using PGP with Go**
A history of PGP / OpenPGP and a practical guide using the maintained `ProtonMail/go-crypto` package — key-pair
generation, encryption, and signature verification across runnable `examples/` modules.

#### [feature-flags](https://github.com/gz-zenn/feature-flags)
**Real-Time Feature Flags in Go: How and Why**
Shows why flag toggling must be real-time (kill switches, progressive rollouts, targeting, A/B tests) and builds a
thread-safe in-memory store with streaming sync — from simple `atomic.Value` to production-grade setups.

#### [newbie-vs-pro-code](https://github.com/gz-zenn/newbie-vs-pro-code)
**Newbie vs. Pro vs. Enterprise Go: How Code Evolves as Skill Grows**
Walks the same problem (reading users and fetching profile data) at three maturity levels, demonstrating how error
handling, package structure, concurrency, and maintainability improve with experience.

#### [chromedp](https://github.com/gz-zenn/chromedp)
**Browser Automation in Go with chromedp**
Drives Chrome via the Chrome DevTools Protocol from pure Go — no Selenium or WebDriver — covering contexts,
actions/tasks, scraping JavaScript-heavy sites, screenshots, PDFs, and end-to-end tests.

#### [videoinfo](https://github.com/gz-zenn/videoinfo)
**Using C Libraries in Go**
A primer on **cgo**, then builds an MP4 inspector that uses FFmpeg's C libraries (libavformat/avcodec/avutil) to
list video, audio, and subtitle streams plus chapters.

---

---

<div align="center">

<sub>Maintained by [@giulianozor](https://github.com/giulianozor) · All projects are available at
[github.com/giulianozor](https://github.com/giulianozor) · Articles at [github.com/gz-zenn](https://github.com/gz-zenn)</sub>

</div>
