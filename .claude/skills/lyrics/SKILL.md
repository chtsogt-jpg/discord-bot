---
name: lyrics
description: Look up song lyrics by song title and/or artist. Trigger when user asks for lyrics, the words to a song, or "what are the lyrics to X".
---

# Lyrics Skill

Return info about a requested song, a short quoted excerpt (fair-use), and links to full lyrics. Do NOT reproduce full lyrics — they are copyrighted.

## When to trigger

- "Lyrics to [song]"
- "What are the words to [song] by [artist]"
- "Give me the lyrics of [song]"
- Any request mentioning "lyrics" with a song reference

## Instructions

Lyrics are copyrighted — do NOT reproduce full lyrics. Return song info + a short excerpt (chorus or one short verse) + links.

1. Identify **song title** and **artist**. If the title is ambiguous (e.g. "Hello"), ask which one.
2. Use WebSearch to confirm the song and find lyrics sources (Genius, AZLyrics, Musixmatch, Letras).
3. Return:
   - **Title — Artist** (year, album if known)
   - 1-2 sentence description of what the song is about
   - Short quoted excerpt — chorus hook or ~4 lines of one verse
   - 2-3 links to lyrics sites for the full lyrics

## Edge cases

- **Song not found** — say so, ask for spelling or artist.
- **Multiple songs with same title** — list options, ask which.
- **Non-English songs** — describe in the user's language, link to original lyrics.

## Output format

```
**[Title]** — [Artist] ([Year], [Album])

[1-2 sentence description]

Excerpt:
> [short chorus or ~4 verse lines]

Full lyrics: [Genius](link) · [AZLyrics](link)
```
