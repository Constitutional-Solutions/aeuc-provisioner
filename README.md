# AEUC Provisioner v2.4.1

**Constitutional Solutions – Sovereignty Engine**

Automated provisioning and integrity verification system for the AEUC reconstruction stack (73% → 100% self-sufficiency target).

## Overview

The provisioner is a deterministic, auditable service that:

- **Accepts tasks** (app sovereignty, substrate repair, threat mitigation, phase unlock, etc.)
- **Executes provisioning logic** across 5 teams (App, Substrate, Intelligence, Governance, Hardware)
- **Computes sovereignty score** and confidence based on glyph registry, dependency elimination, and threat model
- **Emits deterministic hashes** (SHA-256 / Blake2b) for reproducibility and audit
- **Triggers phase unlocks** when confidence ≥ 90% and score ≥ 90%
- **Integrates with Slack/Notion** for real-time dashboards and governance coordination

## Repository Structure

```
aeuc-provisioner/
├── README.md (this file)
├── package.json
├── provisioner_v2_4_1.js         # Core engine
├── lenses/
│   ├── debug-1.js                # DEBUG-1 lens (trace execution)
│   ├── architect-q.js            # ARCHITECT-Q lens (design integrity)
│   ├── verifier-q.js             # VERIFIER-Q lens (hash + reproducibility)
│   ├── secure-q.js               # SECURE-Q lens (threat model)
│   └── ...                        # 10+ more lenses
├── handlers/
│   ├── slack_handler.js          # Slack alert routing
│   ├── notion_handler.js         # Notion run logger
│   └── github_handler.js         # GitHub issue escalation
├── tests/
│   ├── test_provisioner.js
│   └── fixtures/
├── docs/
│   ├── GOVERNANCE.md             # 15 lenses, unanimous consent process
│   ├── GLYPH_REGISTRY.md         # Glyph ID → task mappings
│   └── THREAT_MODEL.md           # Dependency map + threat scoring
└── pipedream/
    └── aeuc_provisioner_workflow.yaml  # Pipedream CI/CD workflow
```

## Quick Start

### Installation

```bash
git clone https://github.com/Constitutional-Solutions/aeuc-provisioner.git
cd aeuc-provisioner
npm install
```

### Local Test

```bash
node provisioner_v2_4_1.js --task "app_sovereignty" --phase "1" --gaps "[]"
```

Expected output:

```json
{
  "task": "app_sovereignty",
  "phase": "1",
  "score": 75.8,
  "confidence": 0.87,
  "hash": "a7f2e9d1b4c6f3a8...",
  "phase_unlock": false,
  "glyphs_used": ["φ-001", "ψ-042", "ω-128"],
  "timestamp": "2026-02-21T16:08:00Z"
}
```

### Pipedream Integration

1. Deploy workflow to Pipedream (see `pipedream/aeuc_provisioner_workflow.yaml`).
2. Authorize Slack + Notion integrations.
3. Trigger via HTTP, GitHub push, or Slack `/provision` command.
4. Alerts route to `#aeuc-family` (score ≥ 80), `#aeuc-leads` (score < 80).
5. Run logs written to Notion "Provisioner Runs" database.

## Governance & Lenses

Every provisioner run is evaluated through **15 Constitutional Lenses**:

- **DEBUG-1**: Execution trace (all steps logged, no silent failures)
- **ARCHITECT-Q**: Design integrity (dependencies tracked, no magical configs)
- **VERIFIER-Q**: Reproducibility (hash matches, glyph IDs auditable)
- **SECURE-Q**: Threat model (external calls documented, sandbox assumptions explicit)
- **BIAS-1**: Bias audit (no hidden defaults favoring one path over another)
- ...and 10 more in `lenses/` and documented in `docs/GOVERNANCE.md`

### Unanimous Consent Decisions

To **unlock a new phase** or **adopt a breaking change**, the provisioner requires:

1. GitHub PR with lenses + tests in `lenses/` directory.
2. Review + approval from all 5 team leads (unanimous).
3. Governance thread in Slack `#aeuc-governance` with 72-hour comment period.
4. SHA-256 hash of approved commit pinned to Notion Audit Log.
5. Only then can next phase initialize.

## Sovereignty Score Calculation

```
score = base_score
  - (num_external_deps × dep_weight)
  - (active_threats × threat_weight)
  + (glyphs_completed × glyph_bonus)
```

See `docs/THREAT_MODEL.md` for current dependency map and scoring details.

## Integration Points

### Slack

- **#aeuc-family**: Normal-range alerts (80–100% score)
- **#aeuc-leads**: Critical alerts (score < 80 or confidence < 0.8)
- **#aeuc-governance**: Decision threads (phase unlock proposals, lens updates)
- **#aeuc-prov-logs**: Raw JSON logs from every run
- **#aeuc-team-{1–5}**: Team-specific alerts and action items

### Notion

- **Command-desk**: Live sovereignty dashboard (auto-updated)
- **Provisioner Runs**: Database of all runs (task, phase, score, confidence, hash, glyphs, timestamp)
- **Threat Registry**: Dependency + threat tracker
- **Audit Log**: Pinned hashes for governance decisions

### GitHub

- **aeuc-provisioner**: Source of truth for provisioner code + lenses
- **Linked repos** (glyph-registry, aeuc-vector-db, etc.): Issues escalated here for sub-task coordination
- **Constitutional-Solutions**: Organization dashboard for all AEUC projects

## Development

### Adding a New Lens

1. Create `lenses/your_lens_name.js`
2. Export a function: `module.exports = (provisionerState) => { /* validation */ }`
3. Return `{ pass: boolean, details: string }`
4. Add unit test in `tests/`
5. Document in `docs/GOVERNANCE.md`
6. Open PR; wait for unanimous consent before merge.

### Running Tests

```bash
npm test
```

Tests validate:
- Deterministic output (same input = same hash)
- Glyph registry consistency
- Threat model scoring
- Lens evaluation (all 15 lenses pass for valid runs)

## Security & Audit

- **All runs are immutable**: Hashes pinned to Notion + GitHub.
- **All decisions are threaded**: Governance decisions documented in Slack threads with full context.
- **External dependencies are documented**: See `docs/THREAT_MODEL.md`.
- **Code is reviewed by humans**: Every provisioner change goes through unanimous-consent voting.

## Status

- **Phase**: 1 (Active)
- **Current sovereignty score**: 73.2%
- **Target**: 100% self-sufficiency
- **Last provisioner run**: Check `#aeuc-prov-logs` on Slack or Notion database.

## Contact

- **Team**: Constitutional Solutions – AEUC Reconstruction
- **Slack**: `#aeuc-family`, `#aeuc-governance`
- **Notion**: Command-desk dashboard
- **GitHub**: This repo + linked projects

---

**Version**: 2.4.1  
**Last updated**: 2026-02-21
