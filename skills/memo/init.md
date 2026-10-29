# init

Project-scoped only — does not touch global files.

1. If `~/.claude/memory/projects/{mapped-path}/memory.md` already exists (see SKILL.md for
   how `{mapped-path}` is derived), stop.
2. Otherwise create the scope root **inside the project** at `{project}/memory/` (if the
   project already has its own `memory/` index of the same shape, reuse it), then symlink
   `~/.claude/memory/projects/{mapped-path}` -> `{project}/memory`. Project memory lives in the
   project, never as real files in the global repo (its `projects/*` is git-ignored).
   Git: own private repo → commit `memory/` with the project; public or third-party repo → add
   `/memory/` to `.git/info/exclude` instead (never publish memory). Files:

`general.md`:
```
# {Project Name} - General

(Populated as you work in this project)
```

`memory.md`:
```
# {Project Name} - Memory Index

| File | Description | Last updated |
|------|-------------|--------------|
| `general.md` | Cross-topic project notes | {today's date} |
```

Don't create a `domain/` dir upfront — `domain/{topic}.md` files get created by `update` only
when a fact clusters around a nameable subject (see `update.md`).
