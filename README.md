# Agent Skills

Opinionated skills for improving daily work efficiency with Claude, etc. Skills are packaged instructions and scripts that extend agent capabilities across development, documentation, planning, and professional workflows.

Skills follow the [Agent Skills](https://agentskills.io/) format.

---

## 🧭 Quick Navigation

**[🚀 Installation](#-installation)** • **[📖 Skill Structure](#-skill-structure)** • **[🤝 Contributing](#-contributing)** • **[🔗 Links](#-links)**

---

## 🚀 Installation

### Quick Install (Recommended)

```bash
npx skills add forest/agent-skills
```

This method works with multiple AI coding agents (Claude Code, Codex, Cursor, etc.)

### Register as Plugin Marketplace

Run the following commands in Claude Code:

```bash
/plugin marketplace add forest/agent-skills
/plugin
```

### Install Plugins

**Option 1: Via Browse UI**

1. Switch to **Marketplaces** tab (use arrow keys or Tab)
2. Select **agent-skills**, press Enter
3. Browse and select the plugin(s) you want to install
4. Select **Install now**

**Option 2: Direct Install**

```bash
# Install specific skill
/plugin install skills@agent-skills
```

## 📖 Skill Structure

Each skill contains:

- `SKILL.md` - Detailed instructions for the agent (with YAML frontmatter)
- `README.md` - User-friendly documentation with examples
- `scripts/` - Helper scripts for automation (optional)
- `references/` - Supporting documentation (optional)

---

## 🤝 Contributing

Contributions are welcome! When adding new skills:

1. Follow the [Agent Skills](https://agentskills.io/) format
2. Include both `SKILL.md` (for agents) and `README.md` (for users)
3. Add YAML frontmatter to `SKILL.md` with `name:` and `description:` fields

---

## 🔗 Links

- [Agent Skills Format](https://agentskills.io/)
- [Claude Code Documentation](https://docs.anthropic.com/claude/docs)
- [GitHub Repository](https://github.com/forest/agent-skills)
