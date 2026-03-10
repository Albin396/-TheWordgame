# the.word.game

A browser-based multiplayer word chain game built as a single self-contained HTML file. No server, no dependencies to install — just open the file and play.

---

## What It Is

Players take turns building a word chain where each new word must start with the last letter of the previous word. Every submitted word is validated against a live dictionary API, so made-up words won't fly. The player with the most accepted words at the end wins.

---

## Features

### Authentication
- **Register** a new account with a username, password, and emoji avatar
- **Login** to an existing account (stored in-memory for the session)
- **Guest mode** — jump straight in with a randomly assigned guest name
- Logout button available from the game header

### Game Setup
- Add or remove players (2–6 supported)
- Choose a **game mode**:
  - **Classic** — play until someone can't continue
  - **Timed** — each player has a countdown timer per turn (10s, 20s, or 30s)
  - **Score** — first to reach a target score wins (5, 10, or 20 points)
- **Game clock** toggle — optional overall session timer
- **AI opponent** toggle — adds a CPU player that picks words from a built-in word list

### Gameplay
- Word input is validated in real time:
  - Must use only letters
  - Must start with the required letter (last letter of the previous word)
  - Cannot reuse any word already played in the session
  - Must be a real English word (checked via the [Free Dictionary API](https://dictionaryapi.dev/))
- The word chain is displayed visually with connecting letters highlighted
- Turn indicator shows whose turn it is, with per-player color coding
- Live scoreboard updates after each accepted word

### Results
- Final scores sorted by rank
- Winner announced with animated confetti
- Tie detection
- "Play Again" resets scores and returns to setup (keeping the same players)

---

## How to Run

1. Open `word-game.html` in any modern web browser
2. Register an account or continue as a guest
3. Configure players and game options
4. Click **Start Game**

No build step, no npm, no server required.

---

## Technical Notes

| Detail | Value |
|---|---|
| File type | Single-file HTML (HTML + CSS + JS) |
| External fonts | Google Fonts — Space Mono, Syne |
| Dictionary API | `https://api.dictionaryapi.dev/api/v2/entries/en/<word>` |
| User data storage | In-memory only (resets on page refresh) |
| AI word pool | Hardcoded list of ~50 common words |
| Browser support | All modern browsers (uses `async/await`, CSS variables, Canvas API) |

---

## File Structure

Everything lives in one file (`word-game.html`), organized in this order:

1. **`<head>`** — meta tags, font imports
2. **`<style>`** — all CSS, including dark theme variables, layout, animations, and responsive rules
3. **`<body>`** — four view panels:
   - `#login-view` — shown on load
   - `#setup-view` — game configuration
   - `#game-view` — active gameplay
   - `#results-view` — end-of-game summary
4. **`<script>`** — all game logic:
   - Player and game state management
   - Timer logic (per-turn and global clock)
   - Dictionary API call with caching
   - AI turn logic
   - Confetti animation (Canvas API)
   - Login / register / guest auth flows

---

## Known Limitations

- User accounts and scores do **not** persist across page refreshes (no backend or localStorage)
- The AI opponent uses a fixed word list and is not very challenging
- Single-device multiplayer only (players share the same screen and take turns)
