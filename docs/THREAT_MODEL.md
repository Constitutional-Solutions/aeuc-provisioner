# Threat Model & Sovereignty Score

Tracks deps/threats to compute LOVE_OP score.[cite:334][file:336]

## Formula

\[ score = 100 \times \left( base - dep_penalty - threat_weight + glyph_bonus \right) \]

- **dep_penalty**: |gaps| / max_gaps × 20
- **threat_weight**: active_threats × 10 (e.g. external API=5, unhashed input=15)
- **glyph_bonus**: completed_glyphs / total × 15

## Current Map

| Threat | Weight | Mitigation |
|--------|--------|------------|
| npm deps | 8 | Lockfile + audit |
| External API | 12 | Mock + timeout |
| Slack/Notion | 5 | Token rotation |

Target: 100% (zero external deps).