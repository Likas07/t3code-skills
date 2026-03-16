# T3 Skills Library

Portable Codex/Claude skill library for use across machines.

## Contents

- `skills/`: managed skill source directories
- `profiles/`: saved active-set profiles
- `categories.yaml`: category/group metadata
- `bin/skills`: local CLI for enabling, disabling, and loading profiles
- `completions/`: shell completion helpers

## Recommended Setup

Clone this repository to `~/.skill-library`:

```bash
git clone git@github.com:Likas07/t3code-skills.git ~/.skill-library
```

Then use the library normally:

```bash
~/.skill-library/bin/skills status
~/.skill-library/bin/skills profile load current
```

The CLI manages active symlinks in `~/.codex/skills` or `~/.claude/skills`.

## Notes

- `skills/.archived/` is intentionally not tracked.
- `.skill-lock.json` is local machine state and is intentionally not tracked.
