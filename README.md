<div align="center">

# Pocket AI

**A lightweight native Android assistant powered by Google Gemini: chat and real-time voice conversation.**

**[Download APK](https://github.com/KSURitam/Pocket_AI/releases/tag/Apk)**


## Requirements
- Android 10 or Android 11 (minSdk 29, targetSdk 30)
- A free **[Google AI Studio](https://aistudio.google.com/apikey) API key**
- Internet connection

## Credits

- **Main developer:** **[KSURitam](https://github.com/KSURitam)**
- **AI engine:** **[Google Gemini API](https://ai.google.dev/)**

## Overview

Pocket AI is a fully native Android app written in Java with **no AndroidX and a single dependency (OkHttp)**, so it stays small and runs smoothly on low-RAM phones. It has two main modes: a text **Chat** and a **Live Voice** conversation.

## Features

### Chat mode
- Streaming replies from Gemini with Markdown rendering (code blocks, lists, bold)
- Works in **English, Bengali, Hindi and Hinglish**
- Full **chat history** stored locally (SQLite), searchable and resumable
- 🔊 **Speaker button on every AI reply** to read that reply aloud, with Play and Stop
- Optional automatic read-aloud (Settings)
- Say or type **"open YouTube"** or **"search Android ROM"** to launch real installed apps or run a browser search
- Long-press a message to copy it

### Live Voice mode
- Real-time two-way voice conversation using the **Gemini Live API** (WebSocket, 16 kHz microphone in, 24 kHz voice out)
- Clean animated **voice orb** that pulses with the AI voice and shows when it is connecting, listening or speaking
- Clear, balanced AI voice: plays on the media volume stream with a loudness stage and soft limiter (no clipping, phone master volume untouched)
- Keeps working while another app is in front (foreground service with a visible notification)
- Polite inactivity check-in: after 60 seconds of silence the assistant asks once, then stays quiet until you speak again
- Echo protection on the phone speaker; interrupt the assistant naturally when using headphones
- Voice commands to open apps and search the web

### Daily tokens
- Every user gets **100 tokens per day**; each AI answer (a chat reply or a Live voice turn) uses 1 token
- Balance, a progress bar and the time of the next refill are shown on the home screen, in Chat and in Live Voice
- When the balance reaches zero, AI chat and Live voice pause until the automatic refill at **12:00 AM IST**
- The balance is kept on the device, and moving the phone clock backwards does not refill it

### Phone actions
- Opens real installed apps through Android launch intents (matches names in English, Bengali and Hinglish)
- Browser search with proper URL encoding, with a choice of installed browser
- Optional **"no permission popup"** mode for instant actions, or ask-first mode

### Screen vision (view only)
- With your explicit permission (official Android screen-capture dialog) the assistant can look at your screen and answer questions about it
- The app only views the screen. It never taps, types or controls other apps

### Settings
- Gemini API key stored **encrypted with the Android Keystore (AES-GCM)**
- Text and live model selection, language, graphics quality, read-aloud toggle
- Check key and model, remove key, clear conversation history
- First launch walks you through adding your API key with a one-tap **Get API key** link

### Built for low-end devices
- Rendering and background work are throttled by the graphics setting
- The voice orb draws at a lower frame rate on the Low graphics setting
- Small APK, no heavy libraries, no analytics

## Models

| Purpose | Model |
|---|---|
| Text chat | `gemini-3.5-flash` |
| Live voice | `gemini-3.1-flash-live-preview` |

Models can be changed in Settings. The app never silently substitutes a different model.

## Install
1. Press **Download APK** above (opens the latest release).
2. Open the downloaded file and allow installing from your browser or file manager if Android asks.
3. Launch Pocket AI, paste your Gemini API key and start chatting.

## Permissions

| Permission | Why |
|---|---|
| Internet | Talk to the Gemini API |
| Microphone | Live Voice conversation |
| Foreground service | Keep Live Voice running while you use other apps |
| Screen capture (on request) | Optional screen vision, granted through the Android system dialog |

No broad "all apps" permission is used; app launching relies on targeted package visibility queries.

## Privacy
- Your API key never leaves the device except in requests to Google's Gemini API, and it is stored encrypted
- Chat history stays in a local database on your phone
- No ads, no tracking, no third-party analytics

## Project structure

```
app/src/main/
├── java/com/ksuritam/pocketai/
│   ├── HomeActivity / ChatActivity / LiveVoiceActivity / SettingsActivity ...
│   ├── VoiceOrb.java            Live voice indicator
│   ├── Tokens.java / TokenCard  Daily token balance + UI
│   ├── LiveClient.java          Gemini Live WebSocket client
│   ├── GeminiClient.java        Streaming REST client
│   └── logic/                   Pure-Java logic (commands, app matching,
│                                audio loudness, daily token rules)
└── res/
tests/LogicTests.java            JVM unit tests
```

## Developer

Made by **[KSURitam](https://github.com/KSURitam)**.

## Notes
- Daily tokens are counted on the device; they are a usage allowance, not a billing system.
- Gemini Live is a preview service; availability and behaviour depend on Google.

- ## Credits

- **Main developer:** **[KSURitam](https://github.com/KSURitam)**
- **AI engine:** **[Google Gemini API](https://ai.google.dev/)**
