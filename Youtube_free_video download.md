# 🎥 YouTube Members-Only Video Downloader

![GitHub stars](https://img.shields.io/github/stars/yourusername/youtube-members-downloader?style=for-the-badge&logo=github)
![GitHub forks](https://img.shields.io/github/forks/yourusername/youtube-members-downloader?style=for-the-badge&logo=github)
![GitHub issues](https://img.shields.io/github/issues/yourusername/youtube-members-downloader?style=for-the-badge&logo=github)
![License](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)

> 📥 **Download YouTube Members-Only videos** using `yt-dlp` — **No cookies.txt file needed!**  
> Works with **Engineering Digest** (DevMinds Pro) and any other YouTube membership channel.

---

## ✨ Features

- ✅ **No cookies.txt file needed** — Direct browser extraction
- ✅ **Bypass Chrome database lock errors** — Uses Microsoft Edge
- ✅ **Full HD (1080p) download support**
- ✅ **Audio-only MP3 download**
- ✅ **Playlist support**
- ✅ **Subtitle & thumbnail download**
- ✅ **Cross-platform** (Windows, macOS, Linux)

---

## 📋 Table of Contents

- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
  - [Phase 1: Install Node.js](#phase-1-install-nodejs-)
  - [Phase 2: Update yt-dlp](#phase-2-update-yt-dlp-)
  - [Phase 3: Setup Microsoft Edge](#phase-3-setup-microsoft-edge-)
  - [Phase 4: Clear Browser Locks](#phase-4-clear-browser-locks-)
  - [Phase 5: Download Video](#phase-5-download-video-)
  - [Phase 6: (Optional) FFmpeg Setup](#phase-6-optional-ffmpeg-setup-)
- [Quick Cheat Sheet](#-quick-cheat-sheet)
- [Troubleshooting](#-troubleshooting)
- [Pro Tips](#-pro-tips)
- [Disclaimer](#-disclaimer)
- [License](#-license)

---

## 🎯 Prerequisites

Before you start, make sure you have:

| Requirement | Details |
|-------------|---------|
| 🎫 **Active Membership** | DevMinds Pro or higher on Engineering Digest (or any channel) |
| 💻 **Windows 10/11** | (macOS/Linux also supported with minor changes) |
| 🌐 **Microsoft Edge** | Pre-installed on Windows |
| 🐍 **Python 3.8+** | For yt-dlp (optional if using .exe) |

---

## 🔧 Installation

### Phase 1: Install Node.js 🟢

**Why?** YouTube requires a JavaScript runtime for yt-dlp to work properly.

**Steps:**

1. Download **Node.js LTS** from: https://nodejs.org/en/download
2. Run the installer → **Next → Next → Finish**
3. ✅ Make sure **"Add to PATH"** is checked
4. **Restart Command Prompt**
5. Verify installation:

```cmd
node -v
```

**Expected Output:**
```
v22.12.0
```

> 💡 **Alternative:** Download `deno.exe` from https://deno.land/download and place it in the same folder as `yt-dlp.exe`.

---

### Phase 2: Update yt-dlp 🟢

**Why?** YouTube changes encryption weekly. Old yt-dlp = errors.

```cmd
yt-dlp -U
```

**Expected Output:**
```
Latest version: 2025.01.15
yt-dlp is up to date (2025.01.15)
```

**If update fails**, manually download:
```
https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp.exe
```

Place it in: `C:\Users\<YourName>\Downloads\`

---

### Phase 3: Setup Microsoft Edge 🟡

**Why Edge?** Chrome locks its cookie database, causing `Permission Denied` errors.

**Steps:**

1. Open **Microsoft Edge**
2. Go to https://www.youtube.com and **login** with your paid account
3. Verify membership by opening a members-only video
4. **Close Edge completely** (not just minimize)

---

### Phase 4: Clear Browser Locks 🟡

**Why?** Edge runs background processes that lock the database.

```cmd
taskkill /IM msedge.exe /F
```

**Expected Output:**
```
SUCCESS: The process "msedge.exe" with PID 12345 has been terminated.
```

> 💡 If you see `ERROR: The process "msedge.exe" not found`, that's fine — Edge is already closed!

---

### Phase 5: Download Video 🟢

#### 🚀 Main Command

```cmd
yt-dlp --cookies-from-browser edge "https://www.youtube.com/watch?v=92k5uokmW9o"
```

#### 📖 Command Breakdown

| Part | Purpose |
|------|---------|
| `yt-dlp` | The tool |
| `--cookies-from-browser edge` | Extract cookies directly from Edge |
| `"https://..."` | Video URL |

#### ✅ Expected Output

```
[youtube] Extracting URL: https://www.youtube.com/watch?v=92k5uokmW9o
[youtube] 92k5uokmW9o: Downloading webpage
[youtube] 92k5uokmW9o: Downloading player 4fd832e7-main
[info] 92k5uokmW9o: Downloading 1 format(s): 137+140
[download] Destination: Java Executor Framework Mastery [92k5uokmW9o].f137.mp4
[download] 100% of 150.00MiB in 00:30
[download] Destination: Java Executor Framework Mastery [92k5uokmW9o].f140.m4a
[download] 100% of 5.00MiB in 00:02
[Merging] Merging formats into "Java Executor Framework Mastery [92k5uokmW9o].mp4"
```

🎉 **Video downloaded successfully!**

---

### Phase 6: (Optional) FFmpeg Setup 🔴

**Why?** YouTube serves video and audio separately. FFmpeg merges them.

**Steps:**

1. Download FFmpeg: https://www.gyan.dev/ffmpeg/builds/ffmpeg-release-essentials.zip
2. Extract the ZIP
3. Copy `ffmpeg.exe` to `C:\Users\<YourName>\Downloads\`

**Folder structure:**
```
C:\Users\<YourName>\Downloads\
├── yt-dlp.exe
├── deno.exe      (optional)
└── ffmpeg.exe    (recommended)
```

---

## 📋 Quick Cheat Sheet

```cmd
:: 1. Check Node.js version
node -v

:: 2. Update yt-dlp
yt-dlp -U

:: 3. Kill Edge background processes
taskkill /IM msedge.exe /F

:: 4. Basic download (best quality)
yt-dlp --cookies-from-browser edge "VIDEO_URL"

:: 5. List available formats
yt-dlp -F --cookies-from-browser edge "VIDEO_URL"

:: 6. Download specific quality (1080p)
yt-dlp -f 137+140 --cookies-from-browser edge "VIDEO_URL"

:: 7. Download audio only (MP3)
yt-dlp -x --audio-format mp3 --cookies-from-browser edge "VIDEO_URL"

:: 8. Download entire playlist
yt-dlp --cookies-from-browser edge "PLAYLIST_URL"

:: 9. Download with subtitles
yt-dlp --write-subs --sub-langs en --cookies-from-browser edge "VIDEO_URL"

:: 10. Download thumbnail
yt-dlp --write-thumbnail --cookies-from-browser edge "VIDEO_URL"
```

---

## 🛠️ Troubleshooting

### ❌ Error 1: "No supported JavaScript runtime"

**Solution:**
```cmd
node -v
```
If no version shows, install **Node.js** (Phase 1).

---

### ❌ Error 2: "Could not copy Chrome cookie database"

**Solution:**
```cmd
taskkill /IM chrome.exe /F
```
Then use **Edge** instead of Chrome.

---

### ❌ Error 3: "This video is available to this channel's members"

**Possible Causes:**
- ❌ Membership expired → Renew
- ❌ yt-dlp outdated → `yt-dlp -U`
- ❌ Wrong browser profile → `--cookies-from-browser edge:Default`
- ❌ Not logged in on Edge → Login on YouTube

---

### ❌ Error 4: "Permission denied" / "Access is denied"

**Solution:**
```cmd
taskkill /IM msedge.exe /F
taskkill /IM chrome.exe /F
```

---

### ❌ Error 5: "ffmpeg is not installed"

**Solution:** Follow **Phase 6** (FFmpeg Setup).

---

### ❌ Error 6: "Sign in to confirm you're not a bot"

**Solution:** Use **Edge** instead of Chrome:
```cmd
yt-dlp --cookies-from-browser edge "VIDEO_URL"
```

---

## 💡 Pro Tips

### 🎬 Custom Filename
```cmd
yt-dlp -o "%(title)s.%(ext)s" --cookies-from-browser edge "VIDEO_URL"
```

### 📁 Custom Output Folder
```cmd
yt-dlp -o "D:\Videos\%(title)s.%(ext)s" --cookies-from-browser edge "VIDEO_URL"
```

### 🔢 Download Range (Episodes 1-10)
```cmd
yt-dlp --playlist-start 1 --playlist-end 10 --cookies-from-browser edge "PLAYLIST_URL"
```

### ⚡ Faster Downloads (Concurrent Fragments)
```cmd
yt-dlp -N 4 --cookies-from-browser edge "VIDEO_URL"
```

### 📊 Quality Selection Reference

| Resolution | Format Code | Size (Approx) |
|------------|-------------|---------------|
| 4K (2160p) | `313+140` | ~500 MB |
| 1080p | `137+140` | ~150 MB |
| 720p | `136+140` | ~75 MB |
| 480p | `135+140` | ~40 MB |
| Audio Only | `140` | ~5 MB |

---

## 📁 Recommended Folder Structure

```
C:\Users\<YourName>\Downloads\
│
├── yt-dlp.exe              ← Main tool
├── deno.exe                ← JS runtime (optional)
├── ffmpeg.exe              ← Video/audio merger (recommended)
│
└── Videos\                 ← Output folder
    ├── Video 1.mp4
    ├── Video 2.mp4
    └── ...
```

---

## ⚠️ Disclaimer

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                                                                              ║
║   ⚠️  WARNING: This guide is ONLY for users with an ACTIVE PAID             ║
║       SUBSCRIPTION!                                                          ║
║                                                                              ║
║   • Downloading without a subscription violates YouTube's Terms of Service. ║
║   • This guide is for PERSONAL OFFLINE VIEWING only.                        ║
║   • Do NOT redistribute downloaded content.                                 ║
║   • Support content creators — buy the subscription! 💪                     ║
║                                                                              ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

---

## 🤝 Contributing

Contributions are welcome! 🎉

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/AmazingFeature`
3. Commit your changes: `git commit -m 'Add some AmazingFeature'`
4. Push to the branch: `git push origin feature/AmazingFeature`
5. Open a Pull Request

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## ⭐ Show Your Support

Give a ⭐️ if this guide helped you!

---

## 📞 Contact & Support

- 🐛 **Found a bug?** [Open an issue](https://github.com/yourusername/youtube-members-downloader/issues)
- 💬 **Need help?** [Start a discussion](https://github.com/yourusername/youtube-members-downloader/discussions)

---

<div align="center">

**Made with ❤️ for the YouTube community**

```
     ██████╗  ██████╗  ██████╗ ██████╗     ██╗     ██╗   ██╗ ██████╗██╗  ██╗
    ██╔════╝ ██╔═══██╗██╔═══██╗██╔══██╗    ██║     ██║   ██║██╔════╝██║ ██╔╝
    ██║  ███╗██║   ██║██║   ██║██║  ██║    ██║     ██║   ██║██║     █████╔╝ 
    ██║   ██║██║   ██║██║   ██║██║  ██║    ██║     ██║   ██║██║     ██╔═██╗ 
    ╚██████╔╝╚██████╔╝╚██████╔╝██████╔╝    ███████╗╚██████╔╝╚██████╗██║  ██╗
     ╚═════╝  ╚═════╝  ╚═════╝ ╚═════╝     ╚══════╝ ╚═════╝  ╚═════╝╚═╝  ╚═╝
```

</div>
