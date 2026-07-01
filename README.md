# grok

A portable Agent Skill for **fast, resumable learning branches** while you code, research, or write. When a concept comes up mid-task, `grok` teaches it at your level — grounded in sources it searches, not parametric guesses — without breaking your flow, then, only when you confirm, saves a durable, resumable checkpoint to a global learning vault so the next session (and the agent) can pick up exactly where you left off.

Works with **Claude Code** and **Codex**.

## Why a learning branch

grok is for concepts and terms worth saving and revisiting — not trivial lookups. When one of those comes up mid-task and you just explain it inline, two things quietly cost you:

1. **It burns your context window.** The tangent crowds out the work you were actually doing — by the time you're back, the model's working memory is half side-quest and your real task has been pushed out.
2. **The explanation is throwaway.** It lives only in that session's scrollback. Compact or clear the context, or close the session, and it's gone — hit the same concept next week and you re-derive it from scratch.

grok treats the detour as a **branch** off your session: fork away to understand the thing, let grok save the understanding to the vault — durable, retrievable, agent-readable — then resume your main thread with your context intact. Next time the concept comes up, the knowledge is already there to build on, in *and* across sessions.

And it grounds as it goes: each answer comes from an active search of high-trust sources, and those sources are saved alongside the checkpoint. So the *first* time you grok something you pay the search once — every revisit reads what's already captured and searches only to fill the gaps. The grounding compounds instead of being re-paid.

## Origins

grok descends from [Matt Pocock's `/teach` skill](https://github.com/mattpocock/skills/tree/main/skills/productivity/teach). `/teach` is a full, multi-session *course builder*: you give it a topic, and it stands up a teaching workspace — a mission, beautiful HTML lessons, reusable components, reference docs, and learning records — to take you deep over time.

grok keeps `/teach`'s learning *principles* but throws out the workspace machinery, because it's built for a different moment: not "sit down and learn this topic," but "I'm in the middle of something and just need to understand this *now*."

## The learning principles it inherits

From `/teach`, grok carries forward the parts that make learning actually stick:

- **Zone of proximal development** — teach *just beyond* your current level, not from first principles. grok estimates this from your prompt, your follow-ups, and prior vault material.
- **Fluency vs. storage strength** — a smooth explanation feels like mastery but isn't retention. grok separates the two and, at checkpoint time, can ask a single lightweight retrieval question to strengthen what you'll actually remember.
- **Ground everything in *why*** — teaching is tied to the real reason the concept came up in your work, never abstract.
- **Trust real sources, not parametric memory** — grok grounds its answers in active search of high-trust sources and records them, so revisits build on citations rather than re-derived guesses.
- **Glossary discipline** — compressing a concept into a tight, opinionated definition is itself evidence of understanding; durable terms get saved.
- **Capture misconceptions** — corrected assumptions are recorded, because what you got *wrong* shapes what to revisit.

## How grok is different

| | `/teach` | `grok` |
|---|---|---|
| Moment | "Teach me this topic" (planned, deep) | "Grok this *now*" (inline, mid-task) |
| Output | Beautiful HTML lessons + course | Grounded inline explanation + Markdown checkpoint |
| State lives in | A per-topic workspace in the current dir | One **global vault** (`~/Vault/grok`) |
| Speed | Deliberate, lesson-paced | Speed-first; no quizzing mid-answer |
| Writes | Produces lesson artifacts | **Only on your confirmation** — never litters your repo |

grok also adds something `/teach` doesn't: the vault is a **dual-audience knowledge base**. Each topic carries machine-readable frontmatter (a typed classification, cross-cutting tags, a directed "builds-on / contrasts-with" knowledge graph), and a derived root index. That means an agent can *read your vault to reconstruct what you already know* — and teach accordingly — instead of starting from scratch every session. See [`VAULT-SCHEMA.md`](VAULT-SCHEMA.md) for exactly how that's stored.

## How you use it

1. **Branch in.** Mid-task, run `/grok <concept>` or just ask to "grok" something. grok teaches it at your level — grounded in why it came up and in sources it searches — then you're back to work.
2. **Checkpoint (optional).** If the detour was substantial, grok asks whether to save. On your yes, it writes `~/Vault/grok/<topic>/` — your current understanding, a resume point, open loops, and the sources it grounded in. It never writes without confirmation.
3. **Resume.** Next time you `/grok` a known topic, it finds it and picks up from the checkpoint — across sessions and projects.
4. **Stay fresh.** Topics can carry a review date; grok surfaces what's due for a recheck so time-sensitive knowledge doesn't silently rot.

## The vault

Plain Markdown under **`~/Vault/grok/`**, one folder per topic, plus a derived root `INDEX.md` registry. Browsable by you, readable by agents. To use a different location, change the `~/Vault/grok` references in [`skills/grok/SKILL.md`](skills/grok/SKILL.md). Timestamps default to **KST**; to use another timezone, change the `TZ`/`KST` values in SKILL.md's timestamp instruction.

## Install (Claude Code)

```sh
git clone https://github.com/skhlo/grok.git ~/grok
ln -s ~/grok/skills/grok ~/.claude/skills/grok   # surface the skill
mkdir -p ~/Vault/grok                            # create the vault
```

Then invoke with `/grok <concept>`, or just ask to "grok" something.

## Install (Codex)

Point your Codex plugin config at this repo; the [`.codex-plugin/plugin.json`](.codex-plugin/plugin.json) manifest exposes `skills/`.

## Credits & license

Built on the learning philosophy of [`/teach`](https://github.com/mattpocock/skills) by Matt Pocock. grok is an independent skill — it adapts those principles for fast, resumable, agent-readable learning rather than reusing `/teach`'s code.

MIT — see [LICENSE](LICENSE).
