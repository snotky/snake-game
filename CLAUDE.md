# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the game

```bash
open index.html
```

Or start a local server:

```bash
python3 -m http.server 8080
```

## Architecture

Single-file game (`index.html`) with all CSS and JavaScript inline. No build step, no dependencies.

**Key game state variables:**
- `snake` — array of `{x, y}` segments; index 0 is the head
- `dir` / `nextDir` — current and queued direction `{x, y}`
- `currentQ` — active multiplication question `{a, b, ans}`
- `answers` — array of 5 tiles on the grid (1 correct + 4 wrong), each `{x, y, val, correct}`
- `combo` / `firstBloodDone` — track consecutive correct answers for kill streak logic

**Game loop:** `setInterval(step, speed)` — each tick moves the snake, checks wall/self collision, then checks if the head landed on an answer tile.

**Streak system (`STREAKS` array):** Combo thresholds trigger named announcements (First Blood → Godlike) with Web Audio API sound effects and Web Speech API voice callouts.

**Scoring:** Base 10 pts per correct answer; streak hits award the `points` value defined in `STREAKS` instead.

**Persistence:** Best score saved to `localStorage` key `math_snake_best`.

## Deployed

GitHub Pages: https://snotky.github.io/snake-game/
