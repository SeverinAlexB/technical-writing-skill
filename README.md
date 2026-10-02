# Technical writing skill

An agent skill for writing, editing, and reviewing technical documentation using
ISO 24495-1 plain-language principles and Google's developer documentation style.
Use it with OpenCode or Claude Code for READMEs, setup guides, configuration
references, runbooks, design documents, and release notes.

The skill focuses on reader needs, clear procedures, natural prose, and preserving
technical accuracy. It applies these sources as a practical writing style, not a
formal ISO conformity assessment.

## Install for OpenCode and Claude Code

You need Git and an installed copy of OpenCode or Claude Code. The commands below
use a POSIX shell, such as Bash or Zsh, on macOS, Linux, or WSL.

Both tools discover skills in `~/.claude/skills/`. To install the skill for all
your projects, run:

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/SeverinAlexB/technical-writing-skill.git \
  ~/.claude/skills/technical-writing
```

The destination folder must be named `technical-writing` to match the skill's
name. Cloning installs `SKILL.md` and both reference documents together. No package
manager or custom installer is needed.

Start a new OpenCode or Claude Code session after installation.

### Install in one project

For a project-local installation, run these commands from the project root:

```bash
mkdir -p .claude/skills
git clone https://github.com/SeverinAlexB/technical-writing-skill.git \
  .claude/skills/technical-writing
```

Both tools discover the skill when working in that project. This creates a
separate Git checkout inside the project. To share a versioned installation with
your team, use a Git submodule instead of the project-local clone:

```bash
git submodule add https://github.com/SeverinAlexB/technical-writing-skill.git \
  .claude/skills/technical-writing
```

Commit `.gitmodules` and the submodule entry in your project. Teammates can fetch
the installed version with `git submodule update --init --recursive`.

## Use the skill

### Claude Code

Invoke the skill explicitly with a request:

```text
/technical-writing Rewrite README.md using the Google and ISO plain-language style.
```

Claude Code can also select the skill automatically when your request matches its
description. To confirm it is available, look for `/technical-writing` in the
slash-command menu.

### OpenCode

Ask OpenCode to load the skill for your documentation task:

```text
Use the technical-writing skill to rewrite README.md and the setup guides.
```

OpenCode discovers the skill and can load it through its native `skill` tool.
The skill isn't an OpenCode slash command.

### Example requests

- “Review this setup guide for unclear prerequisites and missing verification.”
- “Rewrite the configuration reference without changing defaults or examples.”
- “Make this runbook easier to follow and organize troubleshooting by symptom.”
- “Improve the release notes while preserving the changelog format.”

## Update the skill

For a global installation, fetch the latest version with:

```bash
git -C ~/.claude/skills/technical-writing pull --ff-only
```

For a project-local clone, run this from the project root:

```bash
git -C .claude/skills/technical-writing pull --ff-only
```

For a submodule installation, run this from the project root, then commit the
updated submodule entry:

```bash
git submodule update --remote -- .claude/skills/technical-writing
```

Start a new agent session to load the updated instructions.

## Troubleshooting

### The installation directory already exists

Git won't clone into a nonempty directory. If the directory is already a checkout
of this repository, use the update command. If it contains another copy of the
skill, move that copy to a backup location before installing. Keep any local
changes you want to preserve.

### The agent doesn't discover the skill

- Check that the installed directory is named `technical-writing` and contains
  `SKILL.md` with that exact capitalization.
- Start a new session after installing.
- For a project-local installation, start the agent in the project.
- Check for another `technical-writing` skill in the tool's other discovery
  directories. Duplicate installations can make it unclear which copy is used.
- In OpenCode, check that your skill permissions allow `technical-writing`.

### Updating fails

Run `git status` in the installed skill directory. A fast-forward update can fail
if you have local commits or conflicting edits. Preserve those changes before
updating; the documented update command doesn't discard them.

## Repository contents

| File | Purpose |
|------|---------|
| [SKILL.md](SKILL.md) | Skill metadata, workflow, writing rules, and final review checklist. |
| [Document patterns](references/document-patterns.md) | Structures for common technical documents. |
| [Writing examples](references/examples.md) | Before-and-after examples for prose and procedures. |

## Sources and compatibility

- [ISO 24495-1:2023 — Plain language](https://www.iso.org/standard/78907.html)
- [Google developer documentation style guide](https://developers.google.com/style)
- [OpenCode skill discovery](https://opencode.ai/docs/skills/)
- [Claude Code skills](https://code.claude.com/docs/en/skills)

The skill uses portable `name` and `description` frontmatter and Markdown
instructions. It doesn't require scripts, plugins, or external services to load.
