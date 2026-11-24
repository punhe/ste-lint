# ste-lint

A small Python script that checks English text against Simplified Technical English style rules. It needs Python 3 only.

## Use

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

This is an early version (score v1) of the linter from [The cure for AI slop](https://github.com/woosal1337/blog/tree/main/videos/ep01-the-cure-for-ai-slop) by Ege Chelebi, under the MIT License. The upstream project has a newer version.

This project is unofficial and is not affiliated with ASD. ASD-STE100 is a registered trademark of ASD.
