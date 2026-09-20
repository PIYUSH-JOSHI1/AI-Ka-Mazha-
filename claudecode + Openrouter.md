# 🤖 Claude Code + OpenRouter Setup Guide

> **Kya kiya humne:** Claude Code (Anthropic ka AI coding tool) ko directly Anthropic se disconnect karke OpenRouter se connect kiya.
> Isse fayda yeh hai ki billing ek jagah se manage hogi, models aasani se switch kar sakte ho, aur agar Anthropic down ho toh bhi kaam karta rahega.

---

## 📌 OpenRouter Kya Hai?

OpenRouter ek **AI model gateway** hai — yeh tumhare aur multiple AI providers (Anthropic, OpenAI, Google, etc.) ke beech mein baithta hai.
Anthropic ko directly pay karne ki jagah, tum OpenRouter ko pay karte ho, aur woh sahi model pe request bhejta hai.

**Fayde:**
- 💰 Ek jagah se saari billing manage karo
- 🔄 Agar Anthropic down ho, automatically doosri jagah se kaam karta hai
- 📊 Usage dashboard: https://openrouter.ai/activity
- 🔀 Saikdo models mein se easily switch karo
- 🆓 Free models bhi available hain (kuch limitations ke saath)

---

## ✅ Humne Kya Kiya — Step by Step

### Step 1: OpenRouter API Key Li
- https://openrouter.ai pe sign up / login kiya
- API key mili: `sk-or-v1-xxxxxxxxxxxxxxxxxxxx` — **isko secret rakho!**

---

### Step 2: Environment Variables Set Kiye PowerShell Mein

#### Sirf Current Session ke liye (temporary — terminal band karne pe chali jaayegi):
```powershell
$env:ANTHROPIC_BASE_URL = "https://openrouter.ai/api"
$env:ANTHROPIC_AUTH_TOKEN = "sk-or-v1-APNA_KEY_YAHAN_LIKHO"
$env:ANTHROPIC_API_KEY = ""
$env:CLAUDE_CODE_ENABLE_GATEWAY_MODEL_DISCOVERY = "1"
```

#### Permanently Set Karne ke liye (PC restart ke baad bhi rahega) — PowerShell mein run karo:
```powershell
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "https://openrouter.ai/api", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_AUTH_TOKEN", "sk-or-v1-APNA_KEY_YAHAN_LIKHO", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", "", "User")
[System.Environment]::SetEnvironmentVariable("CLAUDE_CODE_ENABLE_GATEWAY_MODEL_DISCOVERY", "1", "User")
```

> ⚠️ `sk-or-v1-APNA_KEY_YAHAN_LIKHO` ki jagah apni real OpenRouter API key daalo.

---

### Step 3: Purana Anthropic Login Clear Karo (agar pehle se logged in ho)
Agar pehle Claude Code mein Anthropic account se login kiya tha, toh `claude` ke andar yeh type karo:
```
/logout
```
Phir PowerShell band karke nayi kholo.

---

### Step 4: Claude Code Launch Karo
```powershell
claude
```

---

### Step 5: Check Karo Ki Connection Sahi Hua Ya Nahi
Claude Code ke andar type karo:
```
/status
```
Agar sab sahi hai toh dikhega:
```
Auth token: ANTHROPIC_AUTH_TOKEN
Anthropic base URL: https://openrouter.ai/api
```

Aur real-time mein apni requests dekhne ke liye: https://openrouter.ai/activity

---

## 🔀 Model Kaise Switch Karein — 4 Tarike

### ⚡ Tarika 1: Double-Click Script (Sabse Aasaan — Terminal Nahi Chahiye!)

Project folder mein yeh files hain:

```
📁 Hotel Management/
   ├── 🖱️ Switch Model.bat     ← Isko double-click karo!
   └── 📄 switch-model.ps1    (script jo andar se run hoti hai)
```

**Kaise use karein:**
1. `Switch Model.bat` pe double-click karo
2. Ek menu aayega — number type karo aur Enter dabaao
3. **Nayi** PowerShell kholo aur `claude` run karo

**Menu kuch aisa dikhta hai:**
```
  ================================================
       Claude Code - OpenRouter Model Switcher
  ================================================

  Currently using: anthropic/claude-opus-5 (default)

  ---- ANTHROPIC MODELS (Claude Code ke liye Best) ---
  [1]  Claude Opus 5           - Sabse powerful       (Paid $$$$)
  [2]  Claude Sonnet (latest)  - Coding ke liye badhiya (Paid $$)
  [3]  Claude Haiku (latest)   - Fast aur sasta        (Paid $)

  ---- OPENROUTER SPECIAL ----------------------------
  [4]  openrouter/auto         - AI khud best model choose karta hai

  ---- FREE MODELS (Claude Code mein kaam nahi kar sakta properly) --
  [5]  DeepSeek V4 Flash       - 1M context            (FREE)
  [6]  NVIDIA Nemotron 3 Ultra - 1M context            (FREE)
  [7]  Poolside Laguna M.1     - Coding focused         (FREE)
  [8]  Cohere North Mini Code  - 256K context           (FREE)

  [9]  Default pe wapas jao (Claude Opus 5)
  [0]  Bahar niklo
```

---

### 🖥️ Tarika 2: Terminal Command (Manual Tarika)

PowerShell kholke yeh mein se jo chahiye woh run karo:

```powershell
# Claude Opus 5 — Sabse powerful (default)
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_SONNET_MODEL", "anthropic/claude-opus-5[1m]", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_OPUS_MODEL", "anthropic/claude-opus-5[1m]", "User")

# Claude Sonnet — Coding ke liye badhiya, thoda sasta
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_SONNET_MODEL", "anthropic/claude-sonnet-latest[1m]", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_OPUS_MODEL", "anthropic/claude-sonnet-latest[1m]", "User")

# Claude Haiku — Fast aur sabse sasta
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_SONNET_MODEL", "anthropic/claude-haiku-latest", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_OPUS_MODEL", "anthropic/claude-haiku-latest", "User")

# OpenRouter Auto — AI khud decide karega best model
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_SONNET_MODEL", "openrouter/auto", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_OPUS_MODEL", "openrouter/auto", "User")

# FREE: DeepSeek V4 Flash (1M context)
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_SONNET_MODEL", "deepseek/deepseek-v4-flash:free", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_OPUS_MODEL", "deepseek/deepseek-v4-flash:free", "User")

# FREE: NVIDIA Nemotron 3 Ultra (1M context)
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_SONNET_MODEL", "nvidia/nemotron-3-ultra-550b-a55b:free", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_OPUS_MODEL", "nvidia/nemotron-3-ultra-550b-a55b:free", "User")

# Default pe wapas — Sab clear karo
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_SONNET_MODEL", "", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_DEFAULT_OPUS_MODEL", "", "User")
```

Phir **nayi** PowerShell kholke `claude` run karo.

---

### 🧠 Tarika 3: Claude Code ke Andar Se (Quick Switch)
Claude Code mein type karo:
```
/model
```
Models ki list aayegi — arrow keys se choose karo aur Enter dabaao. **Restart ki zaroorat nahi!**

---

### 📄 Tarika 4: Project Config File (Team ke liye)
Project ke root mein `.claude/settings.local.json` banao:
```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://openrouter.ai/api",
    "ANTHROPIC_AUTH_TOKEN": "sk-or-v1-APNA_KEY_YAHAN_LIKHO",
    "ANTHROPIC_API_KEY": "",
    "CLAUDE_CODE_ENABLE_GATEWAY_MODEL_DISCOVERY": "1",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "anthropic/claude-sonnet-latest[1m]",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "anthropic/claude-haiku-latest"
  }
}
```

> ⚠️ Isko Git pe commit mat karna — API key expose ho jaayegi!
> `.gitignore` mein add karo: `.claude/settings.local.json`

---

## 🆓 OpenRouter ke Free Models

Yeh models `:free` suffix wale hain — cost $0 hai. **Lekin Claude Code ke andar sahi se kaam nahi karte** (Claude Code ko Anthropic-compatible API chahiye). Inhe seedha OpenRouter website se ya direct API calls mein use karo.

| Model | ID | Context | Best kab use karein |
|-------|-----|---------|---------------------|
| DeepSeek V4 Flash | `deepseek/deepseek-v4-flash:free` | 1M tokens | Bade codebase ke liye |
| NVIDIA Nemotron 3 Ultra | `nvidia/nemotron-3-ultra-550b-a55b:free` | 1M tokens | Reasoning tasks |
| Poolside Laguna M.1 | `poolside/laguna-m.1:free` | — | Software engineering |
| Cohere North Mini Code | `cohere/north-mini-code:free` | 256K tokens | Code generation |
| Auto-select free | `openrouter/free` | varies | General use |

> Saare free models dekhne ke liye: https://openrouter.ai/models — "Free" filter lagao

---

## 💡 Recommended Anthropic Models (OpenRouter ke through Paid)

| Model | ID | Kab use karein | Kitna mahenga |
|-------|-----|----------------|---------------|
| Claude Opus 5 | `anthropic/claude-opus-5` | Complex tasks, best quality | $$$$ |
| Claude Sonnet | `anthropic/claude-sonnet-latest` | Roz ka coding kaam | $$ |
| Claude Haiku | `anthropic/claude-haiku-latest` | Chote quick tasks | $ |

---

## 🔑 Environment Variables Ka Reference

| Variable | Kya karta hai |
|----------|--------------|
| `ANTHROPIC_BASE_URL` | Claude Code ko Anthropic ki jagah OpenRouter pe bhejta hai |
| `ANTHROPIC_AUTH_TOKEN` | Tumhari OpenRouter API key (Bearer token ke roop mein) |
| `ANTHROPIC_API_KEY` | Khali `""` rakhna zaroori hai — conflict na ho isliye |
| `CLAUDE_CODE_ENABLE_GATEWAY_MODEL_DISCOVERY` | Claude Code mein model picker enable karta hai |
| `ANTHROPIC_DEFAULT_OPUS_MODEL` | Complex tasks ke liye kaunsa model use ho |
| `ANTHROPIC_DEFAULT_SONNET_MODEL` | General coding ke liye kaunsa model use ho |
| `ANTHROPIC_DEFAULT_HAIKU_MODEL` | Quick completions ke liye kaunsa model use ho |
| `CLAUDE_CODE_SUBAGENT_MODEL` | Sub-agent tasks ke liye kaunsa model use ho |

---

## 📊 Usage Monitor Karo

- **Dashboard:** https://openrouter.ai/activity
- **Billing / Credits:** https://openrouter.ai/credits
- **API Keys Manage Karo:** https://openrouter.ai/settings/keys
- **Saare Models Dekho:** https://openrouter.ai/models

---

## 🛠️ Problems Aaye Toh Kya Karein

| Problem | Solution |
|---------|----------|
| `model-not-found` error aa raha hai | Claude Code mein `/logout` karo, phir terminal restart karo |
| Auth error aa raha hai | Check karo ki `ANTHROPIC_API_KEY=""` (bilkul khali) hai |
| Changes effect nahi kar rahe | **Nayi** PowerShell window kholke `claude` run karo |
| `/status` galat URL dikh raha hai | Terminal band karo, nayi kholo |
| Context 200K dikh raha hai 1M ki jagah | Model name ke end mein `[1m]` lagao, jaise `anthropic/claude-opus-5[1m]` |

---

## 📝 Quick Re-Setup (Agar PC Reset Ho Gayi / Nayi Machine Pe)

Agar environment variables chali gayi hoon, toh PowerShell mein yeh ek baar run karo:

```powershell
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "https://openrouter.ai/api", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_AUTH_TOKEN", "sk-or-v1-APNA_KEY_YAHAN_LIKHO", "User")
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", "", "User")
[System.Environment]::SetEnvironmentVariable("CLAUDE_CODE_ENABLE_GATEWAY_MODEL_DISCOVERY", "1", "User")
```

Phir **nayi** PowerShell kholke `claude` run karo. Ho gaya! 🎉

---

## 🗂️ Is Folder Mein Kya Hai

```
📁 Hotel Management/
   ├── 🖱️ Switch Model.bat          ← Double-click karke model switch karo
   ├── 📄 switch-model.ps1          ← Switcher script (bat file isko run karti hai)
   └── 📖 CLAUDE_OPENROUTER_SETUP.md ← Yeh file — poora guide!
```

---

*Setup kiya: September 20, 2026*
*OpenRouter Official Docs: https://openrouter.ai/docs/cookbook/coding-agents/claude-code-integration*
