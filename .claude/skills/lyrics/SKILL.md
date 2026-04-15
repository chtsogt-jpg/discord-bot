---
name: lyrics
description: Look up song lyrics by song title and/or artist. Trigger when user asks for lyrics, the words to a song, or "what are the lyrics to X".
---

# Lyrics Skill

Fetch lyrics for a requested song and return them cleanly formatted.

## When to trigger

- "Lyrics to [song]"
- "What are the words to [song] by [artist]"
- "Give me the lyrics of [song]"
- Any request mentioning "lyrics" with a song reference

## Instructions

1. Identify **song title** and **artist** from the user's message. If the artist is missing and the song title is ambiguous (e.g. "Hello" — could be Adele, Lionel Richie, etc.), ask the user which one.
2. Use WebSearch to find the lyrics. Good sources:
   - Genius.com
   - AZLyrics.com
   - Musixmatch
3. Use WebFetch to pull the lyrics page, then extract the lyrics text.
4. Return:
   - **Title — Artist** on the first line (bold)
   - Lyrics below, preserving verse/chorus line breaks
   - Source link at the end
5. If the song is very long, return the first 2-3 verses + chorus and offer to continue.

## Edge cases

- **Song not found** — say so directly, suggest the user check spelling or provide the artist.
- **Multiple songs with same title** — list options, ask which one.
- **Non-English songs** — return the lyrics in their original language. Offer translation only if asked.
- **Explicit content** — return as-is; don't censor.

## Output format

```
**[Title]** — [Artist]

[Verse 1 lyrics]
...

[Chorus]
...

Source: [link]
```
