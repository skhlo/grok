# grok

AI explanations are useful, but they usually disappear into the chat.

`grok` turns the ones worth keeping into reusable notes. Ask your assistant to explain a concept, get a short answer based on sources it searches, and if you want to keep it, save a plain Markdown note in your personal learning folder.

Next time the same topic comes up, your assistant can read what you already learned and continue from there instead of starting over.

Works with **Claude Code** and **Codex**.

## Why use this?

Use `grok` when you ask your AI assistant to explain something and think:

> I am going to need this again.

Instead of losing the explanation in chat history, `grok` saves:

- what the concept means
- why it came up
- where you stopped
- the sources it used
- how to resume next time

It is for concepts worth revisiting, not one-off facts.

## What it feels like

You are working and hit a concept you half-understand:

```text
you  > /grok AI inference and tokens

grok > AI inference is when an already-trained AI model is being used.

       Training is like teaching the model.
       Inference is the model doing the job.

       Tokens are the small chunks of text the model reads and writes.
       They are not exactly words. They are the AI's text currency.

       Short version:
       inference = the AI doing the work
       tokens = the pieces of text it works with

       Sources: Google Cloud, IBM, OpenAI docs

       Save this in Vault/grok/ai-inference-and-tokens/?

you  > yes

grok > Saved.
```

That saved note is just Markdown. You can read it, search it, edit it, or ignore it until you need it again.

## The basic workflow

1. **Pause the main task.** A concept comes up while you are coding, researching, or writing.
2. **Grok the concept.** Ask `/grok <concept>`.
3. **Get a short explanation.** grok teaches at your level and uses sources it searches.
4. **Save only if useful.** It writes to your vault only after you say yes.
5. **Resume later.** The next time you grok that topic, it finds the saved note first.

If your tool supports session branching, use it to keep the learning detour separate from
your main task:

- Claude Code: use `/branch`
- Codex: use `/fork`, or `/side` for a quick detour

Then return to your original session when the concept is handled.

## What gets saved?

By default, grok uses:

```text
~/Vault/grok/
```

Think of this as your personal learning folder. Each topic gets its own folder:

```text
~/Vault/grok/ai-inference-and-tokens/
  INDEX.md        what it means and your current understanding
  CHECKPOINT.md   where you stopped and how to resume
  HISTORY.md      what happened each time you revisited it
  REFERENCES.md   the sources grok used
```

Some topics may also get:

```text
PRIMER.md        a cleaner reusable explanation
GLOSSARY.md      important terms and definitions
```

Files are created only when they help. A small topic can stay small.

## See a real saved example

This repo includes a sample saved grok:

[examples/ai-inference-and-tokens](examples/ai-inference-and-tokens)

It shows the files a real checkpoint can produce:

- `INDEX.md`: the durable understanding
- `CHECKPOINT.md`: where the user stopped and how to resume
- `PRIMER.md`: a clean explanation worth rereading
- `REFERENCES.md`: the sources searched and why they were useful
- `HISTORY.md`: the learning timeline

The important part is that learning is incremental. You do not need to understand everything
in one pass. grok can save the useful handle you have now, then resume from that point when a
deeper dive becomes useful.

## Why this is different from a normal chat

In a normal chat, explanations are temporary. They live in the scrollback, and they are easy to lose when the session ends, gets compacted, or moves on.

`grok` makes useful explanations durable:

- **It remembers your level.** The saved note says what you currently understand.
- **It keeps the reason.** The note records why the concept came up.
- **It saves sources.** Future answers can build on sources already found.
- **It resumes.** Your assistant can continue from the saved stopping point.
- **It works across projects.** The vault is global, not tied to one repo.

The goal is simple: stop relearning the same thing from scratch.

## Install

### Claude Code

```sh
git clone https://github.com/skhlo/grok.git ~/grok
ln -s ~/grok/skills/grok ~/.claude/skills/grok
mkdir -p ~/Vault/grok
```

Then invoke it with:

```text
/grok <concept>
```

Or just ask to grok something.

### Codex

Point your Codex plugin config at this repo. The [`.codex-plugin/plugin.json`](.codex-plugin/plugin.json) manifest exposes the `skills/` folder.

Then invoke it with:

```text
/grok <concept>
```

Or just ask to grok something.

## For technical readers

`grok` is a portable Agent Skill for fast, resumable learning detours during other work. It searches trusted sources before teaching, writes only after explicit confirmation, and stores learning state as Markdown with YAML frontmatter.

The vault is meant for two readers:

- you, browsing plain Markdown notes
- your AI assistant, reconstructing what you already know before teaching more

Each topic's `INDEX.md` is the source of truth. The root `~/Vault/grok/INDEX.md` is a generated overview of every topic. Do not edit the root index by hand.

To use a different vault location or timezone, update the `~/Vault/grok` and `KST`
instructions in [`skills/grok/SKILL.md`](skills/grok/SKILL.md).

See [`VAULT-SCHEMA.md`](VAULT-SCHEMA.md) for the full file format.

## Origins

`grok` descends from [Matt Pocock's `/teach` skill](https://github.com/mattpocock/skills/tree/main/skills/productivity/teach).

`/teach` is a deeper course-building workflow. `grok` keeps the learning principles but changes the shape: it is for the moment when you are in the middle of something and need to understand a concept now.

| | `/teach` | `grok` |
|---|---|---|
| Moment | Planned deep learning | Mid-task concept detour |
| Output | Course-style workspace | Markdown checkpoint |
| State lives in | Current project workspace | Global learning vault |
| Writes | Builds learning artifacts | Writes only after confirmation |

The principles it keeps:

- teach just beyond your current level
- explain why the concept matters in your current work
- use trusted sources instead of memory alone
- separate "that made sense" from "I will remember this later"
- save misconceptions and corrected assumptions when useful

## License

MIT - see [LICENSE](LICENSE).
