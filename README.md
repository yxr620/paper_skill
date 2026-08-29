# paper_skill

A Claude skill for writing and revising systems research papers. It builds full-paper context before touching prose, keeps every claim tied to available evidence, and holds the draft in the register of OSDI / SOSP / SIGMOD-style writing rather than blog, tutorial, or marketing prose.

## Install

Claude Code takes the skill's command name from the directory name, so link this repo in as `paper`:

```bash
# personal — available in all projects
mkdir -p ~/.claude/skills
ln -s "$(pwd)" ~/.claude/skills/paper

# or per project
mkdir -p /path/to/project/.claude/skills
ln -s "$(pwd)" /path/to/project/.claude/skills/paper
```

Claude loads it automatically for paper-writing tasks; `/paper` invokes it directly.

Cowork and cloud sessions do not read `~/.claude/skills/`. To use the skill there, enable it for your claude.ai account (Customize in the desktop app sidebar).

## Layout

- `SKILL.md` — always loaded: paper map, workflow, rhetorical control, cross-reference rules, task modes.
- `references/systems-paper.md` — loaded on demand for drafting or substantial revision: section-by-section guidance, claim discipline, emphasis and hedging, style vocabulary, LaTeX rules.
- `agents/openai.yaml` — display metadata for OpenAI-side agent surfaces; unused by Claude.
