---
name: ste-writing
description: Rewrite prose (docs, READMEs, Linear tasks, PR descriptions, error messages, release notes, comments — never code) into ASD-STE100 Simplified Technical English to remove AI slop. Use when writing or rewriting SOPs, runbooks, Linear issues, acceptance criteria, developer handoffs, bug reproduction steps, or technical documentation. Three modes — strict (procedures/safety), clear (general technical prose), no-STE (exclusions). For teammate docs also load references/team-simple-words.md. Do not use for marketing, sales copy, or client relationship messages.
user-invocable: true
---

# ste-writing

Write prose in ASD-STE100 Simplified Technical English. This applies to documentation, Linear tasks, READMEs, pull-request text, error messages, release notes, and comments. It does not apply to code, identifiers, or command syntax. It is not for marketing copy, essays, or anything that needs a voice. STE strips voice on purpose.

## Rules

WORDS
- Use one name for one thing. Do not call the same item by two different names.
- For teammate SOPs, Notion, wiki notes, and Linear team text, also load [team-simple-words.md](references/team-simple-words.md). Use those preferred names. Put a Words on this page box near the top when the page uses more than two of those terms.
- Use the short common word: start (not begin/commence/initiate), use (not utilize/leverage), help (not facilitate), make sure (not ensure), before (not prior to), after (not subsequent to), about (not regarding/concerning), get (not obtain/acquire), show (not demonstrate), also (not additionally/furthermore/moreover).
- Give each word one meaning. "fall" means to move down, not to decrease.
- No marketing adjectives: seamless, robust, powerful, cutting-edge, effortless, world-class, next-generation, revolutionary.
- American spelling.

VERBS
- Active voice. "the parser reads the file", not "the file is read by the parser".
- Use a verb for an action. "analyze the log", not "perform an analysis of the log".
- No stacked auxiliaries. Not "it is important to note that this may help to improve". Write "this improves X".
- No "-ing" main verb where a simple tense works.

SENTENCES
- One instruction per sentence.
- **strict:** max 20 words (instruction), max 25 (descriptive).
- **clear:** max 25 words; allow normal technical vocabulary (GTM, GA4, WP-CLI, etc.).
- No contractions. Use articles: a, an, the, this, these.

PUNCTUATION
- No semicolons. Write two sentences. (The em dash is not banned by STE, only the semicolon is.)

STRUCTURE
- One topic per paragraph, max six sentences. For steps, use a numbered vertical list, one action per item, imperative form. Put a condition before its command.
- For teammate docs, prefer a picture, a two-column example, or a three-step diagram over a long paragraph. Cut each idea to one short sentence plus one Do this line when you can.

## Team documents (required)

Readers include non-native English speakers. They often paste long pages into AI. A short page with a word box and one picture is easier to keep.

Apply [team-simple-words.md](references/team-simple-words.md) to:

- Canonical SOP Markdown that teammates will read
- Notion process pages
- Linear team issues, comments, and Linear documents
- Development wiki notes for humans
- Other shared process pages

Keep product names (Linear, Notion). Do not rename those tools.

Forward-only: do not bulk-rewrite old SOPs unless you already edit that file.

## Output behavior

When producing a finished technical artifact, return only the requested artifact.

When reviewing or advising, explain important decisions before the finished artifact.

## Modes

### strict

Use for: runbooks, deployment steps, security procedures, bug reproduction, acceptance criteria, agent tool instructions, error messages, SOP developer sections.

Apply every rule and both length caps (20 / 25 words).

### clear

Use for: Linear tasks, READMEs, architecture notes, notes that pass the work, technical summaries, SOP overview sections, change-history bullets.

Apply active voice, one action per sentence, no marketing words, sentence/paragraph discipline. Max 25 words. Allow normal technical vocabulary.

### no-STE

Do **not** load this skill for:

- Proposals (except technical scope, deliverables, assumptions, exclusions)
- Brand copy, website marketing, social posts
- Client relationship emails, outreach
- Thought leadership, personal blog posts, stories

Preserve natural voice for those.

## Document section routing

| Section | Mode |
|---|---|
| Overview / why | clear |
| Project manager notes | clear |
| Developer steps | strict |
| Change history | clear (factual bullets) |

## Prompt recipes

**Client request → Linear task (clear):**
Convert this client request into a Linear task. Use clear mode. Include: objective, required changes, acceptance criteria, test steps, exclusions, unresolved questions. Use one action per sentence. Do not invent requirements.

**SOP from notes (strict + clear):**
Create an SOP from these notes. Use strict mode for developer steps. Use clear mode for overview sections. Use numbered steps. Put each condition before its action. Include verification and rollback steps.

**Pass the work (clear):**
Rewrite this for the next person. Use clear mode. Preserve every technical requirement. Remove filler and business language. Separate requirements from background information. Use preferred names from team-simple-words.md.

**Doc review (clear + linter):**
Review this document with the STE linter criteria. First identify: ambiguous nouns, inconsistent names, passive voice, long sentences, hidden assumptions, multiple actions in one step. Then provide a corrected version.

## Self-lint (run before returning finished artifacts)

### Mechanical checklist

1. Any sentence over the mode length cap? Split it.
2. Any semicolon? Replace with a period.
3. Any contraction? Expand it.
4. Any passive voice with a known actor? Make it active.
5. Any "-ing" main verb, nominalization ("perform an analysis"), or phrasal verb ("spin up")? Replace with a plain verb.
6. Same thing named two ways? Pick one name.
7. Teammate page missing a word box when it uses more than two terms from team-simple-words.md? Add the box.

### Python linter (when available)

Write the draft to a temp file. Then run the [STE linter](./ste-lint.py) from this skill folder:

```bash
python3 ./ste-lint.py /path/to/draft.md
```

If this skill is installed as a user skill, this also works:

```bash
python3 "$HOME/.copilot/skills/ste-writing/ste-lint.py" /path/to/draft.md
python3 "$HOME/.claude/skills/ste-writing/ste-lint.py" /path/to/draft.md
python3 "$HOME/.cursor/skills/ste-writing/ste-lint.py" /path/to/draft.md
```

On Windows PowerShell:

```powershell
python "$env:USERPROFILE\.copilot\skills\ste-writing\ste-lint.py" path\to\draft.md
```

Score is violations per 100 words. Lower is cleaner. Compare original vs revised. Do not treat the score as absolute quality. The linter uses regex heuristics. It can flag valid writing and miss unclear writing.

If Python is unavailable, use the mechanical checklist only.

This skill fixes the FORM of slop. It cannot make a hollow paragraph true.

## Attribution

Based on [The cure for AI slop — STE writing kit](https://github.com/woosal1337/blog/tree/main/videos/ep01-the-cure-for-ai-slop) by woosal1337. This version adds three modes and document routing. ASD-STE100 spec: https://asd-ste100.org (do not paste the standard in full; it is copyrighted).

Reference samples: [before-after-samples.md](./before-after-samples.md)

