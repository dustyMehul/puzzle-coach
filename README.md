# puzzle-coach

Interview-puzzle practice for [Claude Code](https://claude.com/claude-code) and other AI agents. Type `/puzzle` and Claude sets a puzzle at your level, then listens the way a real interviewer does while you think out loud: no hints unless you ask, no "you're on the right track". When you finish, you get an honest review and the difficulty moves up or down.

Everything is saved as plain Markdown in your project, so you can stop mid-puzzle, close the chat, and pick it up later with `/puzzle`.

## What it does
- **Adaptive difficulty.** Levels go from 1 to 10. Solve a puzzle and the next one is a level harder; miss one and it eases off. Or fix the level.
- **Your topics.** Seven built-in categories (logic, probability, counting, weighing, strategy, lateral thinking, estimation). Turn some off, or add your own free-text topics.
- **A quiet interviewer.** It reflects back what you said and asks "Is that your final answer?" every time, whether you're right or wrong. It won't steer you.
- **Hints only on request**, in three sizes: small, big, or the full solution. Each one is recorded and affects the score.
- **Honest reviews.** You get the result, what was strong, where your reasoning broke, the clean solution, and how an interviewer would read your answer.
- **Patterns over time.** The hub notes strengths and repeated slips (such as "doesn't sense-check the final number"), and `/puzzle recap` sums them up.
- **No repeats.** A puzzle in your log, or a close variant of one, never comes back.

## Install
**As a plugin** (the command becomes `/puzzle-coach:puzzle`):
```
/plugin marketplace add dustyMehul/puzzle-coach
/plugin install puzzle-coach@puzzle-coach
```

**As a plain skill** (the command is `/puzzle`). Clone the repo, then copy the skill folder into your user skills, or into one project's `.claude/skills/`:
```bash
git clone https://github.com/dustyMehul/puzzle-coach.git
cp -r puzzle-coach/skills/puzzle ~/.claude/skills/puzzle
```

## Other agents
The skill is plain Markdown, so any agent that can read and write files can run it.

| Tool | Setup |
|---|---|
| **OpenAI Codex CLI, Cursor, GitHub Copilot and other `AGENTS.md` readers** | Copy `skills/puzzle/` into your project and add the lines from [`AGENTS.md`](AGENTS.md) to your project's `AGENTS.md` |
| **Gemini CLI** | Copy `skills/puzzle/` into your project and add the lines from [`GEMINI.md`](GEMINI.md) to your project's `GEMINI.md` |
| **Tools that read `SKILL.md` directly** | Put `skills/puzzle/` wherever the tool looks for skills |

Outside Claude Code, say "puzzle" (or "give me a puzzle") if `/puzzle` isn't a command in your tool. The config goes in `puzzle-config.yml` at your project root.

You can also open a clone of this repo in any of these tools and practise right there: the root `AGENTS.md` and `GEMINI.md` already point to the skill, and your practice files are git-ignored.

**Claude.ai on the web, desktop or mobile.** Download [`puzzle-skill.zip`](https://github.com/dustyMehul/puzzle-coach/releases/latest/download/puzzle-skill.zip) from the latest release (or zip the `skills/puzzle` folder yourself) and upload it as a skill (in Settings, under Skills; code execution must be on). Then say "puzzle" in any chat. Files made in a chat don't carry over to the next one, so the same rule applies as for other chat apps: save the hub the agent prints after each review, and paste it in next time. Or keep it in a Claude Project's files. **Claude Code on the web** runs on a GitHub repo, so it works exactly like the desktop version, and committing your `puzzles/` folder keeps your history.

**Other chat apps (ChatGPT, Gemini, Grok).** Paste the contents of [`skills/puzzle/SKILL.md`](skills/puzzle/SKILL.md) into the app's custom instructions, or into a project, along with [`references/categories.md`](skills/puzzle/references/categories.md). Puzzles, hints and reviews work the same way. Chat apps can't save files, though, so after each review the agent prints the updated hub. Save it, and paste it into your next chat to keep your level and history.

## Quick start
1. Open Claude Code in the folder where you want your practice notes to live.
2. Type `/puzzle`. The first time, it asks a few setup questions: your goal, starting level, adaptive or fixed level, topics, and daily target. Then it writes the config.
3. Think out loud. Ask for a hint if you need one. Say when you're done, or give a final answer.
4. Read the review, then type `/puzzle` again for the next one (in the same chat or a new one).

## Commands
| Command | What it does |
|---|---|
| `/puzzle` | Resume the open puzzle, or start the next |
| `/puzzle hint` · `big hint` · `solution` | Ask for help (plain words work too) |
| `/puzzle done` | You've finished; get the review |
| `/puzzle skip` | Drop the open puzzle with no level change |
| `/puzzle level 8` | Next puzzle only, at level 8 |
| `/puzzle probability` | Next puzzle only, from that topic |
| `/puzzle level 7 logic` | Both at once |
| `/puzzle status` | Today's count, current level, open puzzle |
| `/puzzle recap` | Strengths, weak topics, level trend |
| `/puzzle config` | Show settings; change one with `/puzzle config scoring lenient` or plain words |
| `/puzzle setup` | Run setup again |

## Configuration
Settings live in `puzzle-config.yml`: in your project's `.claude/` folder or root (for this project), or in `~/.claude/` (for all projects). The project file wins. Edit the file directly, or just tell the agent ("only probability and counting from now on", "make it fixed at level 6").

| Key | Default | Options |
|---|---|---|
| `state_dir` | `puzzles` | folder for the hub and session files |
| `start_level` | `5` | 1–10, used when the hub is first created |
| `level_mode` | `adaptive` | `adaptive` · `fixed` |
| `fixed_level` | `6` | level used in fixed mode |
| `level_min` / `level_max` | `4` / `10` | range for adaptive mode |
| `categories` | all seven | any subset of the built-ins, plus free-text topics |
| `category_order` | `rotate` | `rotate` (balanced) · `weakest` (practise what you miss) · `random` |
| `daily_target` | `3` | `0` for no target |
| `scoring` | `strict` | `strict`: the key "why" must be said aloud · `lenient`: right answer + sound core idea |
| `interviewer` | `silent` | `silent`: interview simulation · `coach`: also prompts you to check your answer |
| `time_limit_minutes` | `0` | `0` for untimed |
| `links` | `markdown` | `markdown` · `wiki` (Obsidian `[[links]]`) |
| `daily_note` | none | e.g. `daily/{date}.md`: adds a line per puzzle to your daily note |

Ready-made configs are in [`examples/`](examples/):
- [quant interviews](examples/config-quant-interviews.yml): hard, probability-heavy, timed
- [one topic at a fixed level](examples/config-fixed-level-one-topic.yml): coach mode, no target
- [Obsidian vault](examples/config-obsidian-vault.yml): wiki links and daily notes

## Scoring
| Result | Strict (default) | Lenient | Level |
|---|---|---|---|
| Solved | right answer, no hints, and the reasoning said aloud | right answer and a sound core idea, no hints | +1 |
| Partial | small hint, a missing argument, or an arithmetic slip | small hint or an arithmetic slip | 0 |
| Not solved | big hint, solution, or a wrong final answer | same | −1 |

Strict mode scores what you actually said, as an interviewer would. In a real interview, "as long as B can move, A can move" is a claim, not a proof. Pick lenient if you'd rather practise spotting the idea.

## Files it creates
```
puzzles/
├── puzzles.md            # hub: current level, log, patterns
└── sessions/
    └── puzzle-2026-01-05-1-100-lockers.md   # one per puzzle: statement, thinking trail, solution, review
```
Solutions are only written at review time, so you won't see them by accident while browsing your notes. See [`examples/`](examples/) for a sample hub and session.

## Tips
- **One puzzle per chat** works well: `/puzzle`, solve, review, close. The files carry the state.
- **Say the check out loud** before you commit: test an easy case, or compare against your first step. It's the most common way solid setups end in wrong answers.
- If you already know a puzzle, say so and it'll pick another.

## Contributing
Issues and pull requests are welcome, especially new puzzle families for `skills/puzzle/references/categories.md`, with a level and a source for the answer.

## License
[MIT](LICENSE)
