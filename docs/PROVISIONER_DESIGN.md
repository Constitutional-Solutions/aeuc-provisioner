# Provisioner v2.4.1 Design

Deterministic JS engine for AEUC task provisioning, sovereignty scoring, and phase unlocks.[cite:334][file:336]

## Input Schema

```json
{
  "task": "string",  // e.g. 'app_sovereignty', 'glyph_compress'
  "phase": "1‑7",
  "gaps": ["dep1", "threat2"],
  "glyphs": ["φ‑001", "ψ‑042"]
}
``` [file:322]

## Code Flow

1. **Parse Input** → Validate schema, map glyphs via Registry.
2. **Execute Lenses** → 15 constitutional checks (DEBUG‑1, ARCHITECT‑Q, etc.).
3. **Compute LOVE_OP** → 
   \[ score = 100 \times \left(1 - \frac{|gaps|}{max_gaps} - threat_weight + glyph_bonus\right) \] [file:336]
4. **Gate Check** → confidence ≥90% & score ≥90% → phase unlock.
5. **Hash & Emit** → Blake2b/SHA‑256 deterministic output, Slack/Notion log.

## Lenses (15 total)

- DEBUG‑1: Trace execution.
- VERIFIER‑Q: Reproducibility.
- SECURE‑Q: Threat audit.
- ... (full in GOVERNANCE.md)

## Output

```json
{"task":"app_sovereignty","score":75.8,"unlock":false,"hash":"a7f2e9d1..."}
```

Pipedream workflow: HTTP trigger → provisioner → handlers (Slack tiered alerts).[cite:334]