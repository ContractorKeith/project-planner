# TaskTrail — Tasks

---

## Sprint 1 — Foundation

- [ ] Set up repo: pyproject.toml, src layout, install in editable mode
- [ ] Create SQLite schema: tasks table (id, title, status, priority, tags, created_at, completed_at)
- [ ] Implement `tt add "task title"` — insert a task
- [ ] Implement `tt list` — show open tasks in a table
- [ ] Implement `tt done <id>` — mark a task complete
- [ ] Implement `tt delete <id>` — remove a task
- [ ] Add `--tag` and `--priority` flags to `tt add`
- [ ] Add `--tag` and `--priority` filters to `tt list`
- [ ] Write tests for all commands (pytest)
- [ ] Add shell completion for bash/zsh

## Backlog

- [ ] `tt search <query>` — full-text search across task titles
- [ ] `tt log` — show completed tasks with completion date
- [ ] `tt edit <id>` — modify title, tags, or priority
- [ ] `tt export --format csv` — dump tasks to CSV
- [ ] Color-coded priority levels in `tt list` output

## Done

[Empty until you start building]
