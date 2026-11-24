# ste-lint

A writing skill for AI agents and a small Python script. Both help you write Simplified Technical English. The script needs Python 3 only.

| File | Use |
|---|---|
| `SKILL.md` | The skill: rules and three modes |
| `references/team-simple-words.md` | Short words to use with a team |
| `before-after-samples.md` | Samples |
| `ste-lint.py` | The linter |

## Install the skill

```bash
git clone https://github.com/punhe/ste-lint ~/.claude/skills/ste-writing
```

## Use the linter

```bash
python ste-lint.py draft.md
python ste-lint.py "docs/*.md"
cat draft.md | python ste-lint.py
```

The script reports the violations per 100 words. A lower score is cleaner.

On Windows, set UTF-8 mode if the file has non-English characters:

```powershell
$env:PYTHONUTF8 = "1"
python ste-lint.py draft.md
```

## What it counts

Long sentences, semicolons, contractions, passive voice, "-ing" main verbs, nominalizations, phrasal verbs, banned words, marketing adjectives, hedges and long paragraphs.

The script uses regular expressions. It can flag good text and miss bad text.

## Credit

The skill and the linter (score v1) come from [The cure for AI slop](https://github.com/woosal1337/blog/tree/main/videos/ep01-the-cure-for-ai-slop) by Ege Chelebi, under the MIT License. The upstream project has a newer version.

This project is unofficial and is not affiliated with ASD. ASD-STE100 is a registered trademark of ASD.
