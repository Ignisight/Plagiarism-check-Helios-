# Helios — Text Intelligence Skill for Claude

A Claude skill for **plagiarism detection** and **AI-generated content detection**, inspired by the [AEGIS/Helios](https://huggingface.co/spaces/aeras/helios) HuggingFace Space.

## What it does

| Mode | Description |
|------|-------------|
| 🕵️ **Plagiarism Detection** | Searches the web for matching content, analyzes semantic similarity and exact phrase overlap, flags suspicious sentences with source links |
| 🤖 **AI Content Detection** | Analyzes 8 writing fingerprint signals (burstiness, vocabulary diversity, transition words, structural uniformity, etc.) to estimate AI probability |

## Installation

1. Download [`SKILL.md`](./SKILL.md)
2. In Claude.ai, go to **Settings → Skills** and upload the file
3. That's it — Claude will now use this skill automatically when you ask it to check text

## Triggers

Claude will use this skill when you say things like:
- "Check this for plagiarism"
- "Is this AI-written?"
- "Did a human write this?"
- "Scan this essay for copied content"
- "AI detection on this paragraph"

## How it works

Unlike the original Helios app (which used SentenceTransformers + RoBERTa), this skill leverages Claude's native language understanding:

- **Plagiarism**: Claude generates targeted search queries from the text, runs web searches, then evaluates snippet/semantic similarity and exact phrase overlap.
- **AI Detection**: Claude directly assesses 8 stylistic signals known to distinguish AI from human writing, producing a calibrated probability verdict.

## Example output

```
## 🕵️ Plagiarism Check Report
Queries run: 8 | Sources found: 11 | Sentences checked: 14

### Verdict
⚠️ WARNING: Similarity detected

### Source Analysis
| Source          | Similarity | Phrase Overlap | Status |
|-----------------|-----------|----------------|--------|
| Wikipedia: ...  | High       | Yes            | 🚨     |
...

### Flagged Sentences
**Sentence 3** (~87% match): *"The mitochondria is the powerhouse..."*
↳ Source: [Wikipedia](https://en.wikipedia.org/...)
```

## Notes

- Minimum 50 characters of text required
- Results are probabilistic indicators, not proof — always use human judgment
- Plagiarism detection depends on web search availability
