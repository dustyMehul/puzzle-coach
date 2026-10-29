<div align="center">

# 🧩 Puzzle Coach

**A puzzle interviewer that won't help you.**

Brain-teaser practice for Claude and other AI agents. It sets the puzzle, stays quiet while you think, and then tells you honestly how you did.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Claude Code plugin](https://img.shields.io/badge/Claude%20Code-plugin-d97757)
![Works with](https://img.shields.io/badge/works%20with-Claude%20·%20Codex%20·%20Gemini%20·%20Cursor-555)

</div>

---

Ask a chatbot for a puzzle and it'll cheer you on, drop hints you never asked for, and call a half-answer "great thinking!". A real interviewer won't. They'll sit there, say *"okay, keep going"*, and wait to hear whether you can explain **why**.

Puzzle Coach is that interviewer.

```text
You      > /puzzle

Coach    > Puzzle #2 today · Level 7 · Weighing and optimisation

           Four people must cross a bridge at night with one torch.
           At most two cross at a time, at the slower one's pace.
           Their times: 1, 2, 5 and 10 minutes. What is the fastest
           way to get everyone across?

           Talk me through your thinking.

You      > If 1 escorts everyone, that's 2+1+5+1+10 = 19...
           but what if 5 and 10 cross together?

Coach    > Okay. You want 5 and 10 to cross together. Keep going.

You      > 1 and 2 over, 1 back, 5 and 10 over, 2 back, 1 and 2 over.
           That's 2+1+10+2+2... 16.

Coach    > Is that your final answer?

You      > Wait. That's 17, not 16.

Coach    > ...
```

At the end you get a straight review: the result, what was strong, where your reasoning broke, the clean solution, and how an interviewer would read your answer. Then the next puzzle gets harder, or easier.

## ✨ Why it's different

| Most AI puzzle chats | Puzzle Coach |
|---|---|
| Hints you didn't ask for | **Silent until you ask:** small hint, big hint or the full solution, and each one counts against your score |
| "Great job!" for any answer | **Honest scoring.** Strict mode won't accept a claim as a proof, just like an interviewer |
| The same difficulty every time | **Adapts after every puzzle,** from level 1 to 10 |
| Forgets you when the chat ends | **Remembers:** your level, every puzzle, and your recurring slips, saved as Markdown in your project |
| Repeats the classics | **No repeats,** not even close variants |
| Only gives the answer | **Spots patterns in how you think,** like *"states the pattern but doesn't prove it (seen 4 times)"* |

## 🚀 Get started in 30 seconds

**Claude Code**
```
/plugin marketplace add dustyMehul/puzzle-coach
/plugin install puzzle-coach@puzzle-coach
```
Then type `/puzzle-coach:puzzle`. The first run asks a few quick setup questions (goal, level, topics, daily target), and then you're in.

**Claude.ai (web, desktop, mobile):** download [`puzzle-skill.zip`](https://github.com/dustyMehul/puzzle-coach/releases/latest/download/puzzle-skill.zip) and upload it as a skill in Settings (code execution must be on). Then say *"give me a puzzle"*.

<details>
<summary><b>Other ways to install: plain skill, Codex, Gemini CLI, Cursor, Copilot, ChatGPT…</b></summary>

<br>

| Where | How |
|---|---|
| **Claude Code, as a plain skill** (command: `/puzzle`) | Unzip [`puzzle-skill.zip`](https://github.com/dustyMehul/puzzle-coach/releases/latest/download/puzzle-skill.zip) into `~/.claude/skills/`, so that you have `~/.claude/skills/puzzle/SKILL.md` |
| **Codex CLI, Cursor, GitHub Copilot** (and other `AGENTS.md` readers) | Copy `skills/puzzle/` into your project and add the lines from [`AGENTS.md`](AGENTS.md) to your project's `AGENTS.md` |
| **Gemini CLI** | Copy `skills/puzzle/` into your project and add the lines from [`GEMINI.md`](GEMINI.md) to your `GEMINI.md` |
| **ChatGPT, Gemini, Grok** (chat apps) | Paste [`SKILL.md`](skills/puzzle/SKILL.md) and [`categories.md`](skills/puzzle/references/categories.md) into custom instructions or a project |

**About chat apps:** they can't save files between chats, so after each review the coach prints your updated hub. Save it (a Claude or ChatGPT Project file works well) and the next chat picks up where you left off. **Claude Code on the web** runs on a GitHub repo, so commit your `puzzles/` folder to keep your history.

Outside Claude Code, just say *"puzzle"* wherever `/puzzle` isn't a command.

</details>

## 🎛️ Make it yours

Tell it in plain words (*"only probability from now on"*, *"make it timed, 20 minutes"*), or edit `puzzle-config.yml`:

```yaml
level_mode: adaptive        # or fixed
level_min: 6                # adaptive range
level_max: 10
categories:                 # pick any, or add your own topics
  - probability and expected value
  - strategy and game theory
  - Bayes and base rates    # ← free-text topics work too
category_order: weakest     # rotate · weakest · random
scoring: strict             # strict: say WHY · lenient: right idea is enough
interviewer: silent         # silent: interview mode · coach: nudges you to check your answer
time_limit_minutes: 20
daily_target: 3
```

Ready-made setups:

| Preset | For |
|---|---|
| [🎯 Quant interviews](examples/config-quant-interviews.yml) | Hard, probability-heavy, timed, weakest topics first |
| [🧘 One topic, fixed level](examples/config-fixed-level-one-topic.yml) | Calm practice with coaching and no daily target |
| [🗂️ Obsidian vault](examples/config-obsidian-vault.yml) | Wiki links, plus a line in your daily note for every puzzle |

<details>
<summary><b>All settings</b></summary>

<br>

| Key | Default | Options |
|---|---|---|
| `state_dir` | `puzzles` | folder for the hub and session files |
| `start_level` | `5` | 1–10, used when the hub is first created |
| `level_mode` | `adaptive` | `adaptive` · `fixed` |
| `fixed_level` | `6` | level used in fixed mode |
| `level_min` / `level_max` | `4` / `10` | range for adaptive mode |
| `categories` | all seven | built-ins plus free-text topics |
| `category_order` | `rotate` | `rotate` · `weakest` · `random` |
| `daily_target` | `3` | `0` for no target |
| `scoring` | `strict` | `strict` · `lenient` |
| `interviewer` | `silent` | `silent` · `coach` |
| `time_limit_minutes` | `0` | `0` for untimed |
| `links` | `markdown` | `markdown` · `wiki` (Obsidian) |
| `daily_note` | none | e.g. `daily/{date}.md` |

The config lives in `.claude/puzzle-config.yml` or `puzzle-config.yml` in your project, or in `~/.claude/puzzle-config.yml` to cover all projects.

</details>

## 🕹️ Commands

| Say | What happens |
|---|---|
| `/puzzle` | Resume the open puzzle, or start the next |
| `hint` · `big hint` · `solution` | Ask for help (it costs you) |
| `done` | Get your review |
| `/puzzle level 9 logic` | One-off: next puzzle at level 9, from logic |
| `/puzzle skip` | Drop this one, no penalty |
| `/puzzle status` | Today's count, your level, the open puzzle |
| `/puzzle recap` | Strengths, weak spots, level trend, one habit to try |
| `/puzzle config` | See or change settings |

## 📈 How the level moves

| You… | Strict scoring | Level |
|---|---|---|
| Got it, no hints, **and said why** | ✅ Solved | **+1** |
| Needed a small hint, skipped the argument, or slipped on arithmetic | 🟡 Partial | ±0 |
| Needed a big hint or the solution, or gave a wrong answer | ❌ Not solved | **−1** |

Seven topics: **logic · probability · counting · weighing · strategy · lateral thinking · estimation**. Difficulty runs from *"three switches and a bulb"* (level 4) up to *"blue-eyed islanders, the general case"* (level 10).

## 📁 What it saves

```
puzzles/
├── puzzles.md                              ← your level, every result, your patterns
└── sessions/
    └── puzzle-2026-01-05-1-100-lockers.md  ← puzzle, your thinking trail, solution, review
```

Plain Markdown that you own. Solutions are only written after you finish, so browsing your notes never spoils a puzzle. Want to see one? Look at the [example hub](examples/puzzles.md) and [example session](examples/sessions/puzzle-2026-01-05-1-100-lockers.md).

## 💡 Tips from real use
- **Say the check out loud.** Most good setups that end in a wrong answer fail at the last step. Before you commit, plug in an easy case.
- **"It works" isn't "here's why".** In strict mode, *"as long as B can move, A can move"* is a claim. Explaining why it's true is what gets you to Solved.
- **One puzzle per chat** keeps things snappy. Your progress is in the files, not the chat.
- **Already know a puzzle?** Say so. It swaps it out at no cost, and interviewers respect that too.

## 🤝 Contributing
New puzzle families are very welcome. Add them to [`categories.md`](skills/puzzle/references/categories.md) with a level and a source for the answer. Ideas, bugs and presets: [open an issue](https://github.com/dustyMehul/puzzle-coach/issues).

## License
[MIT](LICENSE). Go practise. 🧠
