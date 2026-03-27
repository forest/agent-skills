# Agent Skills

Opinionated Claude Code plugins for Elixir development and session management. Packaged as installable plugins following the [Agent Skills](https://agentskills.io/) format.

---

## Skills

| Plugin | What it does |
|--------|-------------|
| `req-api-client` | Patterns for building Elixir HTTP API clients with Req: module wrappers, plugin architecture, `Req.Test` stubs, webhook signature verification |
| `session-handoff` | Generates deterministic session summaries for handoff between Claude sessions — preserves decisions, rationale, and rejected options without auto-compact inference |
| `tidewave-tools-usage` | Prioritizes Tidewave MCP tools over file system ops for Elixir/Phoenix/Ash work: live code evaluation, module navigation, SQL execution, schema introspection |
| `web-cli` | Browser CLI (`web`) for verifying web pages during development: JS rendering, form submission, session persistence, Phoenix LiveView support |

---

## Installation

### Claude Code

Register this repo as a plugin marketplace:

```
/plugin marketplace add forest/agent-skills
```

Then install individual plugins:

```
/plugin install req-api-client@forest-claude-tools
/plugin install session-handoff@forest-claude-tools
/plugin install tidewave-tools-usage@forest-claude-tools
/plugin install web-cli@forest-claude-tools
```

### Other Agents (Codex, Cursor, etc.)

```bash
npx skills add forest/agent-skills
```

---

## Skill Structure

Each plugin contains a `SKILL.md` with YAML frontmatter (`name`, `description`) used for agent discovery, and the skill content itself.

```
plugins/
  skill-name/
    .claude-plugin/
      plugin.json          # Plugin manifest (name, description, version)
    skills/
      skill-name/
        SKILL.md           # Agent instructions with YAML frontmatter
```

---

## Contributing

1. Follow the [Agent Skills](https://agentskills.io/) format
2. Add a `plugin.json` manifest under `.claude-plugin/`
3. Add `name` and `description` YAML frontmatter to `SKILL.md` — the `description` field drives agent discovery, so make it specific

---

## Links

- [Agent Skills Format](https://agentskills.io/)
- [Claude Code Documentation](https://docs.anthropic.com/claude/docs)
