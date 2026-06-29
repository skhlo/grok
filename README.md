# grok

A portable Agent Skill for **fast, resumable learning branches** while you code, research, or write. When a concept comes up mid-task, `grok` teaches it at your level, then — only when you confirm — saves a durable, resumable checkpoint to a global learning vault so the next session (and the agent) can pick up where you left off.

It works with **Claude Code** and **Codex** (manifests in [`.claude-plugin`](.claude-plugin) and [`.codex-plugin`](.codex-plugin)). The skill source is [`skills/grok`](skills/grok).

## The vault

Learning is stored as plain Markdown under **`~/Vault/grok/`**, one folder per topic, with YAML-frontmatter `INDEX.md` files and a derived root `INDEX.md` registry. It's a dual-audience knowledge base: browsable by you, and machine-readable so an agent can reconstruct what you know. See [`CONTEXT.md`](CONTEXT.md) for the schema vocabulary and [`docs/adr`](docs/adr) for the design decisions.

To use a different location, change the `~/Vault/grok` references in [`skills/grok/SKILL.md`](skills/grok/SKILL.md).

## Install (Claude Code)

```sh
git clone https://github.com/skhlo/grok.git ~/grok
ln -s ~/grok/skills/grok ~/.claude/skills/grok   # surface the skill
mkdir -p ~/Vault/grok                            # create the vault
```

Then invoke it with `/grok <concept>`, or just ask to "grok" something.

## Install (Codex)

Point your Codex plugin config at this repo; the [`.codex-plugin/plugin.json`](.codex-plugin/plugin.json) manifest exposes `skills/`.

## License

MIT — see [LICENSE](LICENSE).
