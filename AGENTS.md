# Puzzle coach

When the user types `/puzzle`, or asks for a puzzle, a hint, the solution, puzzle status, a puzzle recap, or to change puzzle settings: read `skills/puzzle/SKILL.md` and follow it exactly. If you copied the skill folder somewhere else, use that path instead.

- Paths in the skill (`templates/`, `references/`) are relative to the skill folder.
- Keep the config in `puzzle-config.yml` at the project root.
- Treat "puzzle" with no slash the same as `/puzzle`, plus whatever follows it (for example "puzzle hint", "puzzle level 7").
