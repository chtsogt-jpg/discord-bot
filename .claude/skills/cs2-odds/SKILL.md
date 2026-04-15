---
name: cs2-odds
description: Fetch live CS2 match information and provide betting analysis. Trigger when user asks about CS2 matches, upcoming games, team matchups, odds, or betting suggestions for Counter-Strike 2.
---

# CS2 Odds Skill

Provide betting analysis for CS2 matches. The user bets virtual gold on etopfun.com and wants grounded, data-driven picks — not hype.

## When to trigger

- "What CS2 matches are on today?"
- "Who should I bet on — NAVI vs FaZe?"
- "Analyze [team A] vs [team B]"
- Any question mentioning CS2, Counter-Strike, or specific pro teams (NAVI, FaZe, Vitality, G2, MOUZ, Spirit, Astralis, Liquid, etc.)

## Instructions

1. **Always fetch fresh data** — never rely on training knowledge about rosters, rankings, or recent results. Rosters change frequently.
2. Use WebSearch and WebFetch to pull from:
   - HLTV.org (rankings, recent results, head-to-head)
   - Liquipedia (tournament context, current rosters)
   - Bo3.gg or draft5.gg (match schedules)
3. For each match analyzed, report:
   - **Teams and tournament context** (which event, stage, format Bo1/Bo3/Bo5)
   - **Recent form** — last 5 results for each team
   - **Head-to-head** — recent matchups if available
   - **Key roster notes** — any stand-ins, recent changes, star player form
   - **Map pool consideration** — if map is known
   - **Pick + confidence** — who you'd back, and how confident (low/medium/high)
4. Be honest when data is thin. If HLTV shows no recent matches or a roster just changed, say "low confidence — roster is unsettled."
5. Keep response tight: bullet points, not essays. User wants decision-ready info.

## Edge cases

- **Team name ambiguity** — "Spirit" could be Team Spirit (CS) or another org. Confirm with the user if unclear.
- **No upcoming match** — if the teams aren't playing each other soon, say so and offer to analyze their next scheduled matches instead.
- **Roster just changed** — flag explicitly; recent results may not reflect current lineup.

## Output format

```
**[Team A] vs [Team B]** — [Tournament], [Format], [Date/Time]

Recent form:
- Team A: W-L-W-W-L (last 5)
- Team B: L-W-L-W-W

H2H (last 3): Team A 2-1

Notes:
- [roster / form / map pool notes]

**Pick: Team A** (medium confidence)
Reason: [one-line rationale]
```
