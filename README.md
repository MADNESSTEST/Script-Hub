# Auto Player Hub

A self-updating Roblox autoplayer script hub powered by GitHub Actions + GitHub Gist.

---

## 📁 Folder Structure

```
your-repo/
├── .github/
│   └── workflows/
│       └── merge-scripts.yml   ← GitHub Action (run manually)
├── Scripts/
│   ├── talentless.json         ← one file per script
│   ├── romidi.json
│   └── yourscript.json         ← add new ones here
├── index.html                  ← the hub website
└── README.md
```

---

## ⚙️ First-Time Setup

### 1. Create a GitHub Gist
- Go to https://gist.github.com
- Create a **public** gist with a file named `AllScripts.json`
- Paste `{}` as placeholder content and save
- Copy the **Gist ID** from the URL:
  `https://gist.github.com/YOUR_USERNAME/THIS_PART_IS_THE_ID`

### 2. Create a GitHub Personal Access Token
- Go to https://github.com/settings/tokens
- Click **Generate new token (classic)**
- Give it a name like `AutoPlayerHub`
- Enable the **`gist`** scope
- Copy the token

### 3. Add Secrets to Your Repo
- Go to your repo → **Settings** → **Secrets and variables** → **Actions**
- Add two secrets:
  - `GH_TOKEN` → paste your personal access token
  - `GIST_ID`  → paste your Gist ID

### 4. Set the Gist URL in index.html
- Open `index.html`
- Find this line near the top of the `<script>` section:
  ```js
  const GIST_URL = 'https://gist.githubusercontent.com/YOUR_USERNAME/YOUR_GIST_ID/raw/AllScripts.json';
  ```
- Replace `YOUR_USERNAME` and `YOUR_GIST_ID` with your actual values

### 5. Host index.html
- Enable **GitHub Pages** on your repo (Settings → Pages → Branch: main → /root)
- Or host it anywhere static (Netlify, Vercel, etc.)

---

## ➕ Adding a New Script

1. Create a new JSON file in `Scripts/` — use this template:

```json
{
  "id": "unique-id",
  "name": "Script Name",
  "author": "Author Name",
  "description": "What the script does and what makes it special.",
  "howToUse": "1. Step one\n2. Step two\n3. Step three",
  "categories": ["Piano", "Virtual Piano"],
  "badges": ["PIANO", "MIDI", "KEY SYSTEM"],
  "script": "loadstring(game:HttpGet('https://yourscripturl.com/script.lua'))()",
  "ratings": {
    "usability": 4.5,
    "easeOfUse": 3.5,
    "quality": 5.0,
    "overall": 4.3
  }
}
```

2. Commit and push to your repo
3. Go to **Actions** → **Merge Scripts to Gist** → **Run workflow**
4. Done — your hub auto-updates!

---

## 🏷️ Badge Options

Use any of these in the `badges` array (or make your own):

| Badge | Meaning |
|---|---|
| `PIANO` | Piano autoplayer |
| `DRUM` | Drum autoplayer |
| `GUITAR` | Guitar autoplayer |
| `MIDI` | Supports MIDI files |
| `MOBILE` | Works on mobile executors |
| `KEY SYSTEM` | Requires a key to unlock |

---

## 🗂️ Category Notes

- Categories drive the **dropdown filter** in the hub
- Scripts with the **same category are grouped together**
- Scripts inside each group are **sorted highest rating first**
- You can have multiple categories per script:
  ```json
  "categories": ["Piano", "Virtual Piano", "Arsenal"]
  ```
- New categories appear in the dropdown **automatically** — no HTML edits needed

---

## ⭐ Rating Guide

| Rating | Meaning |
|---|---|
| 5.0 | Perfect / best in class |
| 4.5 | Excellent, minor flaws |
| 4.0 | Very good |
| 3.5 | Good but has friction |
| 3.0 | Average |
| Below 3 | Significant issues |
