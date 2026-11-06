# Gameweek Predictor

A phone-first website for predicting the scores of each weekend's Premier League matches, scored against the real results.

Built by Ben Farrell with Claude (Anthropic's AI assistant) in Claude Code, November 2026.

**Try it:** https://benafarrell2000.github.io/Gameweek-Predictor/ (on GitHub Pages, picks and results are saved in your own browser).

**Also in this repository:** [Play Penalty Pundit ⚽](https://benafarrell2000.github.io/Gameweek-Predictor/penalty-pundit.html), an arcade football quiz where how close your guess is decides whether you score the penalty. [More about it below](#penalty-pundit).

## What it does

The site has three screens, switched from a tab bar at the bottom.

| Screen | What you can do |
| --- | --- |
| **Predict** | Type a home and away score for each of the 10 Gameweek 10 fixtures, then press **Save picks**. A countdown shows the next kick-off. Each match locks at its own real kick-off time, after which its pick can't be changed. |
| **Results** | Follow each match from Not started to In play to Full time. Once a full-time score is in, you see your points for that match and the reason. The owner can type in or correct full-time scores. |
| **Table** | A leaderboard of every player with saved picks: position, exact scores, correct results and total points. |

### Scoring

| Prediction vs result | Points |
| --- | --- |
| Exact score (predict 2-1, finishes 2-1) | 5 |
| Right result, wrong score (predict 2-1, finishes 3-1) | 2 |
| Wrong result, or no prediction | 0 |

Points don't stack, so an exact score is worth 5, not 7. Players level on points are separated by exact scores, then correct results. If they're still level, they share the position (shown as `=`).

## Project files

| Path | What it is |
| --- | --- |
| `mockup/index.html` | The whole app: HTML, CSS and JavaScript in one file, with no build step. This is the version published on claude.ai. |
| `index.html` | The same app as a standalone web page, served by GitHub Pages. |
| `penalty-pundit.html` | Penalty Pundit, a separate arcade quiz game in one self-contained file. |
| `docs/PRD.md` | The product requirements document: goals, user stories, scoring rules, design, technical plan, risks. |
| `CLAUDE.md.txt` | The original brief given to Claude at the start of the project. |
| `MEMORY.md.txt` | The project log Claude kept: progress, decisions and lessons learned, session by session. |

## How it works

- **No framework.** It's plain JavaScript: the screens are drawn from a small state object, and the scoring rules are a pure `points(pick, actual)` function.
- **Hosting and storage.** The live version is hosted as a Claude Artifact on claude.ai.
  - Picks are saved in the artifact's database: `picks/<user id>`, holding `{ "gw10": { "EVE-COV": "2-1", … } }`.
  - Full-time scores are saved under `results/gw10`.
  - Access rules let each person write only their own picks, and only the owner (or an editor) write results.
- **Offline fallback.** Opened anywhere else, for example straight from this repository, the page still works but saves to the browser's `localStorage`. The header then shows "This device" instead of "Synced".
- **Kick-off locking.** Each match locks when the browser clock passes its kick-off time, given in UTC (UK time in November).
- **Results.** Scheduled Claude tasks run after each matchday. They look up the official full-time scores and write any that are missing, never overwriting a score that's already been entered.

## Run it locally

Download `mockup/index.html` and open it in a browser. That's all it needs.

## How AI was used

1. **Requirements.** Claude turned a one-paragraph brief (`CLAUDE.md.txt`) into a full PRD (`docs/PRD.md`).
2. **Design and build.** Claude built a clickable mock-up in Premier League colours, then turned it into a working app over several rounds of feedback.
3. **Human corrections.** Ben made the key calls along the way:
   - replacing invented fixtures with the real Gameweek 10 fixtures
   - removing pre-filled example scores
   - making picks save for real and results appear through the week
4. **Memory.** Claude kept `MEMORY.md.txt` up to date after every step, so each new session could pick up where the last one left off.
5. **Automation.** Claude scheduled tasks to fetch and enter the real results after each matchday.

**Lesson learned:** the AI made up plausible-looking fixtures until it was given real data. Anything factual (fixtures, results) now comes from a real source or is clearly labelled as an example.

## Penalty Pundit

**Play:** https://benafarrell2000.github.io/Gameweek-Predictor/penalty-pundit.html

An arcade-style football quiz with 5 questions, each with a number for an answer. After each guess the answer is revealed. Then a pixel-art footballer takes a penalty, and how close you were decides your chance of scoring:

| Your guess | Result |
| --- | --- |
| Bang on | 100% chance of scoring |
| 1 either side | 75% chance of scoring |
| 2 either side | 50% chance of scoring |
| 3 either side | 25% chance of scoring |
| Further out | Missed penalty |

A perfect quiz always scores 5/5, but being a little off can still score. The aim is to score as many of the 5 penalties as you can.

- **Built with:** plain HTML, CSS and JavaScript. The stadium and players are drawn on a 320×180 canvas, and the sound effects are made with the Web Audio API, with no audio files.
- **Changing it:** the questions, answers and scoring bands are listed at the top of the script in `penalty-pundit.html`. Each question can have its own bands.

## Next steps

- Load fixtures from a data API instead of hard-coding each gameweek.
- Add friends as players (each needs Contributor access to the page).
- Build the full version from the PRD: Next.js, Supabase and football-data.org.
