# Governance & Lenses

AEUC provisioner enforces **unanimous consent** via 15 Constitutional Lenses. Every run/PR/change must pass **all 15** before phase unlock or merge.[cite:334][file:336]

## Lens Categories

1. **Debug/Trace**: DEBUG‑1 (full execution log, no silent fails).
2. **Architecture**: ARCHITECT‑Q (no magic configs, dep tracking).
3. **Verification**: VERIFIER‑Q (hash reproducibility, glyph audit).
4. **Security**: SECURE‑Q (threat model explicit).
5. **Bias**: BIAS‑1 (no hidden defaults).
6-15: BIOLOGICAL‑1 (salience), ECONOMICS‑1 (cost), FAMILY‑1 (charter align), etc. (full list in lenses/).

## Unanimous Consent Process

1. PR with new lens/test → 5 team leads review.
2. Slack `#aeuc-governance` thread (72h comment).
3. All approve → hash pinned Notion Audit Log.
4. Merge → provisioner accepts.[cite:334]

## Phase Unlock

score ≥90% **AND** confidence ≥90% **AND** lenses unanimous → auto‑unlock next phase.