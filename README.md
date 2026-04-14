# Such a Gem! — Rally Royale: Battle of the Chat

A Twitch Video Component extension that turns your stream into a live physics battleground. Viewers buy gem drops (Bits) to spawn gems into a Holographic Prism Arena. Gems stack, shatter, link with chain lightning, and push the Rally Meter toward chaotic Royale phases. Streamers can trigger boss events and control arena parameters.

## Repository layout

- **extension-src/** — static frontend files for the Video Component, Config, and Live Config pages.
- **ebs/** — production-ready Extension Backend Service (EBS) with EventSub verification, WebSocket broadcasting, OAuth scaffolding, and admin endpoints.
- **packaging/** — ZIP packaging script to create the uploadable extension ZIP.
- **Dockerfile** — minimal container for the EBS.
- **.github/workflows/ci.yml** — CI workflow to build and produce the ZIP artifact.

## Quick local dev (minimal)

### Prerequisites
- Node.js 18+
- npm 9+
- Python 3.8+ (for local static hosting)

### 1) Install EBS dependencies
```bash
cd ebs
npm install
```

### 2) Run the EBS
```bash
npm run dev
```

### 3) Serve extension frontend files (new terminal)
```bash
cd extension-src
python3 -m http.server 8080
```

### 4) Configure local Twitch extension settings
Point your Twitch extension config (or tunnel URLs) to your local EBS and frontend hosts.

## Packaging

Create the uploadable extension ZIP:

```bash
cd packaging
./build-extension-zip.sh
```

## CI

GitHub Actions builds the project and publishes the extension ZIP artifact for each workflow run.

## Security note

Never commit API keys, OAuth secrets, or private tokens into this repository.
