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

Choose one installation scope:

- **All projects:** Use the global installation below.
- **One project:** Use one of the [project installation options](#install-in-one-project).

Avoid installing both scopes with the same skill name. In Claude Code, a personal
skill takes precedence over a project skill named `technical-writing`, so a global
installation can override the version your team tracks. OpenCode also searches
multiple skill directories; use a single installation to make the source clear.

### Install for all projects

Both tools discover skills in `~/.claude/skills/`. The destination folder must be
named `technical-writing` to match the skill's name. Run:

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/SeverinAlexB/technical-writing-skill.git \
  ~/.claude/skills/technical-writing
```

Cloning installs `SKILL.md` and both reference documents together. Continue to
[Verify installation](#verify-installation).

### Install in one project

Choose one of the following options and run its commands from your project's
root. Both use `.claude/skills/technical-writing`, which both tools discover
when working in that project.

#### Local installation

Use this option for your own working copy. It creates a separate Git checkout
inside the project. To track the skill as part of the project for your team,
choose the team installation below before running any commands.

```bash
mkdir -p .claude/skills
git clone https://github.com/SeverinAlexB/technical-writing-skill.git \
  .claude/skills/technical-writing
```

Continue to [Verify installation](#verify-installation).

#### Team installation

Use this option to track a specific skill version in your project's Git
repository. Add the skill as a submodule. The destination directory must be
available; don't run the local installation commands first.

```bash
git submodule add https://github.com/SeverinAlexB/technical-writing-skill.git \
  .claude/skills/technical-writing
```

Commit `.gitmodules` and the submodule entry in your project. Teammates can fetch
the installed version with `git submodule update --init --recursive`.

### Verify installation

Start a new OpenCode or Claude Code session. For a project installation, start
the session in that project.

- **Claude Code:** Confirm that `/technical-writing` appears in the slash-command
  menu. Invoke it with a request, such as
  `/technical-writing Review README.md for clarity without editing it`.
- **OpenCode:** Ask, “Load the technical-writing skill and summarize its writing
  rules.” Confirm that the agent successfully loads the skill and describes its
  Google and ISO plain-language guidance.

The installed files alone don't confirm discovery. Check that the tool can load
the skill before using it for a documentation task. If it doesn't, see
[The agent doesn't discover the skill](#the-agent-doesnt-discover-the-skill).

## Use the skill

### Claude Code

Invoke the skill explicitly with a request:

```text
/technical-writing Rewrite README.md using the Google and ISO plain-language style.
```

Claude Code can also select the skill automatically when your request matches its
description.

### OpenCode

Ask OpenCode to load the skill for your documentation task:

```text
Use the technical-writing skill to rewrite README.md and the setup guides.
```

Include the skill's name in your request when you want OpenCode to use it
explicitly.

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
  directories. In Claude Code, a personal installation overrides a project
  installation with the same name. Keep the installation you intend to use and
  move other copies to a backup location outside the discovery directories.
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
instructions. OpenCode loads it through its native `skill` tool; Claude Code
supports explicit invocation through `/technical-writing`. Loading requires no
scripts, plugins, or external services.
