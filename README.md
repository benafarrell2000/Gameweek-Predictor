# Penalty Pundit

An arcade-style football quiz. Guess the answer, then take the penalty: the closer your guess, the better your chance of scoring.

**Play it:** https://benafarrell2000.github.io/Gameweek-Predictor/penalty-pundit.html

Built with Claude (Anthropic's AI assistant) in Claude Code, November 2026.

## How to play

1. Press **START**. There are 5 questions, and every answer is a number.
2. Type your guess and press **SHOOT**.
3. The answer is revealed and the scoring-chance meter swings.
4. A pixel-art footballer takes the penalty. It ends in one of GOAL!, SAVED!, OFF THE POST!, OVER THE BAR! or WIDE!
5. After 5 kicks the full-time screen shows your score, a rank, and every question with your guess and the answer.

How close you are decides your chance of scoring:

| Your guess | Result |
| --- | --- |
| Bang on | 100% chance of scoring |
| 1 either side | 75% chance of scoring |
| 2 either side | 50% chance of scoring |
| 3 either side | 25% chance of scoring |
| Further out | Missed penalty |

A perfect quiz always scores 5/5, but being a little off can still score. The aim is to score as many of the 5 penalties as you can.

## How it works

- **One file, no build step.** It's all in `penalty-pundit.html`: plain HTML, CSS and JavaScript, plus two Google Fonts.
- **Graphics.** The stadium, crowd, goal, keeper and big-headed striker (TRUDY 9) are drawn on a 320×180 pixel canvas and scaled up.
- **Fireworks special.** Rockets burst over the London skyline all game, and every goal sets off a volley with bangs and crackles.
- **Sound.** Every sound effect is made in the browser with the Web Audio API, with no audio files. There's a SOUND ON/OFF toggle.
- **Fairness.** The result is decided first, with a random roll against your scoring chance. The meter and the penalty animation are then played to match it.
- **Easy to change.** The questions, answers and scoring bands are listed at the top of the script. Each question can have its own bands.
- **Saved in your browser:** your best score and the sound setting.

## Run it locally

Download `penalty-pundit.html` and open it in a browser. That's all it needs.

## How AI was used

1. **The brief.** I described the game I wanted: 10 number questions, a penalty after each one, and scoring chances based on how close the guess is. Claude designed and built the whole game from that, including the pixel art, the animation and the sound.
2. **Testing.** Claude played full games in a browser to check every part worked: the meter, goals, saves, misses, the full-time screen and the phone layout.
3. **My changes.** I set the final 5 questions and their answers, chose the scoring bands, changed the wording, and had my name taken off the game.
4. **Memory.** Claude kept `MEMORY.md.txt` up to date after every step, so the work could carry on across sessions. The game was even handed from one Claude session to another.

---

## Also in this repository: Gameweek Predictor

A phone-first website for predicting the score of each Premier League match in a gameweek, scored against the real results.

**Try it:** https://benafarrell2000.github.io/Gameweek-Predictor/ (on GitHub Pages, picks and results are saved in your own browser).

| Screen | What you can do |
| --- | --- |
| **Predict** | Enter a score for each of the 10 Gameweek 10 fixtures and save. Each match locks at its real kick-off time. |
| **Results** | Follow each match to full time and see your points and the reason. |
| **Table** | A leaderboard ranked by points, then exact scores, then correct results. |

**Scoring:** an exact score is 5 points, the right result with the wrong score is 2 points, and anything else is 0.

**How it was built with AI:**
- Claude turned my one-paragraph brief (`CLAUDE.md.txt`) into a full product requirements document (`docs/PRD.md`).
- It then built a mock-up and turned it into a working app over several rounds of my feedback.
- On the claude.ai version, picks are saved to the account, and scheduled Claude tasks fill in the real results after each matchday.

**Lesson learned:** the AI invented plausible-looking fixtures until I gave it the real ones. Anything factual now comes from a real source or is clearly labelled as an example.

## Project files

| Path | What it is |
| --- | --- |
| `penalty-pundit.html` | Penalty Pundit: the whole game in one file. |
| `index.html` | Gameweek Predictor as a standalone page, served by GitHub Pages. |
| `mockup/index.html` | Gameweek Predictor as published on claude.ai. |
| `docs/PRD.md` | The Gameweek Predictor product requirements document. |
| `CLAUDE.md.txt` | The original brief given to Claude. |
| `MEMORY.md.txt` | The project log Claude kept: progress, decisions and lessons learned. |

## Next steps

- **Penalty Pundit:** add more questions, with a new random set each game.
- **Gameweek Predictor:** load fixtures from a data API instead of hard-coding each gameweek, and add friends as players.
