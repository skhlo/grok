# grok

A portable Agent Skill for **fast, resumable learning branches** while you code, research, or write. When a concept comes up mid-task, `grok` teaches it at your level — grounded in sources it searches, not parametric guesses — without breaking your flow, then, only when you confirm, saves a durable, resumable checkpoint to a global learning vault so the next session (and the agent) can pick up exactly where you left off.

Works with **Claude Code** and **Codex**.

## Quickstart

**Claude Code**

```sh
git clone https://github.com/skhlo/grok.git ~/grok
ln -s ~/grok/skills/grok ~/.claude/skills/grok   # surface the skill
mkdir -p ~/Vault/grok                            # create the vault
```

**Codex** — point your Codex plugin config at this repo; the [`.codex-plugin/plugin.json`](.codex-plugin/plugin.json) manifest exposes `skills/`.

Then invoke with `/grok <concept>`, or just ask to "grok" something.

## How you use it

1. **Fork off the tangent.** A concept worth keeping comes up mid-task. Rather than spend your main thread's context on it, fork the session so the detour is isolated — Claude Code: `/branch`; Codex: `/fork` (or `/side` for a quick, auto-returning detour).
2. **Grok it in the fork.** Run `/grok <concept>`. grok teaches it at your level, grounded in sources it searches — then, if it's worth keeping, checkpoints to `~/Vault/grok/<topic>/` on your confirmation. It never writes without your yes.
3. **Return with context intact.** Jump back to your main session (`/resume`, or just end the `/side` detour). Your original thread is untouched; the knowledge now lives in the vault.
4. **Resume later, anywhere.** Next time you `/grok` that topic — in any session or project — it finds the checkpoint and picks up from it, reading its saved sources first and searching only for what's new.
5. **Stay fresh.** Topics can carry a review date; grok surfaces what's due for a recheck so time-sensitive knowledge doesn't silently rot.

## What a grok looks like

You've forked off the tangent (`/branch` in Claude Code, `/fork` in Codex), then:

```text
you ▸ /grok debounce vs throttle

grok ▸ (searches MDN + Lodash docs)
      Both rate-limit a function, differently:
      • debounce — wait until calls stop, then run once         (search-as-you-type)
      • throttle — run at most once per interval, drop the rest  (scroll/resize)
      Rule of thumb: debounce = "after the storm"; throttle = "once per tick."
      Grounded in: MDN, Lodash docs.

      Save this as a checkpoint in Vault/grok/debounce-vs-throttle/?

you ▸ yes

grok ▸ Saved:
      ~/Vault/grok/debounce-vs-throttle/INDEX.md       what it is + your current handle
      ~/Vault/grok/debounce-vs-throttle/CHECKPOINT.md  where you stopped, open loops
      ~/Vault/grok/debounce-vs-throttle/REFERENCES.md  MDN + Lodash, annotated
      ~/Vault/grok/INDEX.md                            registry updated
```

Then `/resume` back to your main task — context untouched. Next week, `/grok debounce vs throttle` resumes from this checkpoint, reads those saved sources first, and searches only for what's new.

What it wrote is plain Markdown you can read, grep, and edit — the topic's `INDEX.md`:

```md
---
topic: "debounce vs throttle"
type: concept
description: "Both rate-limit a function: debounce runs once after calls stop; throttle at most once per interval."
tags:
  - "javascript"
  - "performance"
status: active
---

## Current Handle
Debounce coalesces a burst into one trailing call; throttle enforces a steady max rate…
```

…plus a derived root registry (`~/Vault/grok/INDEX.md`) with a glanceable row per topic. See [`VAULT-SCHEMA.md`](VAULT-SCHEMA.md) for the full format.

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

## The vault

Plain Markdown under **`~/Vault/grok/`**, one folder per topic, plus a derived root `INDEX.md` registry. Browsable by you, readable by agents. To use a different location, change the `~/Vault/grok` references in [`skills/grok/SKILL.md`](skills/grok/SKILL.md). Timestamps default to **KST**; to use another timezone, change the `TZ`/`KST` values in SKILL.md's timestamp instruction.

## Credits & license

Built on the learning philosophy of [`/teach`](https://github.com/mattpocock/skills) by Matt Pocock. grok is an independent skill — it adapts those principles for fast, resumable, agent-readable learning rather than reusing `/teach`'s code.

MIT — see [LICENSE](LICENSE).
