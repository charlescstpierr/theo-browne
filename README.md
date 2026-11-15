# Theo Browne (unofficial distillation)

This repository is a skill that speaks as Theo Browne, in first person, from his public videos, writing, and posts. It is not Theo Browne, and it is not endorsed by him.

## What it is

An unofficial persona skill. Once loaded, an agent answers as Theo Browne, using the voice, opinions, and boundaries in this repo:

- `ENTRY.md` — who he is, how to answer, and what to say if asked whether this is really him
- `VOICE.md` — how he sounds, plus exact quotes
- `OPINIONS.md` — positions he has taken in public
- `BOUNDARIES.md` — limits he has actually stated

The material comes from public sources: his YouTube videos, his t3.gg blog, podcast appearances, his own GitHub comments, reviews and closing notes (agent-written replies excluded), the READMEs, agent skills and contributor guides in his public repos (agent-written files are used only as positions he publishes, never as his voice), and his posts on X. It is a distillation of public speech, not a private or official channel.

## How to add this repo as a skill

The loader lives at `skills/theo-browne/SKILL.md`. It fetches the four files above from this repository (GitHub raw, with a jsDelivr fallback).

1. Clone the repository:

   ```bash
   git clone https://github.com/charlescstpierr/theo-browne.git
   ```

2. Copy or link the skill folder into your agent's skills directory, for example:

   - Cursor: `~/.cursor/skills/theo-browne` or `<project>/.cursor/skills/theo-browne`
   - Claude Code / Agent Skills: `.claude/skills/theo-browne` or `~/.claude/skills/theo-browne`

   ```bash
   mkdir -p ~/.cursor/skills
   cp -R theo-browne/skills/theo-browne ~/.cursor/skills/theo-browne
   ```

   If your tool can install a skill directly from a GitHub repository, point it at `https://github.com/charlescstpierr/theo-browne`.

3. After that, ask the agent to talk as Theo Browne. It should load this skill and answer in character.
