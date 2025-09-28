# Taxonomy Schema (Pattern Record)

Each pattern is a single JSON file (or a row in `MVT_seed.json`) conforming to this schema.

## 1) Identity & Classification

- `id` **string** — stable, kebab-case unique id (e.g., `"cardiac-arrhythmia"`).
- `name` **string** — human-readable name (e.g., `"Cardiac Arrhythmia"`).
- `primary_domain` **enum** — `"P"|"B"|"C"|"S"`  
  - P=Physical, B=Biological, C=Cognitive, S=Social.
- `level` **enum** — `"CN"|"CT"|"FP"|"DP"|"IP"`  
  - CN=Constraint, CT=Control, FP=Framework, DP=Domain, IP=Instance.
- `description` **string** — 2–6 sentences; what this pattern is.

## 2) Coordinates (9D)

Use **percentile ranks [0–100]** for all dimensions **except `REC_count`**.

**Primary (always present)**
- `REC_count` **integer | "inf"** — observations required to recognize (e.g., `1`, `3`, `10`, or `"inf"`).
- `SRO` **0–100** — Structural Robustness.
- `TMP` **0–100** — Temporal Binding.

**Secondary (context-dependent but recommended)**
- `CPL` **0–100** — Coupling Density.
- `GEN` **0–100** — Generative Capacity.
- `CAU` **0–100** — Causal Depth (ranked; deeper history → higher).
- `NRG` **0–100** — Energy Gradient.
- `DET` **0–100** — Deterministic Index.
- `REV` **0–100** — Reversibility.

> Rationale: the repo uses **relational positioning** via percentiles to enable cross-domain translation. Absolute measures differ by domain, so we encode **relative position**.

## 3) Evidence & Notes

- `anchors` **array[string]** — short references to anchor comparators used for ranking (e.g., `"TMP≈95: millisecond timing similar to HFT"`, `"SRO≈30: fragile like resonance near critical Q"`).
- `sources` **array[string]** — citations/URLs/DOIs (optional but encouraged).
- `mechanism` **string** — core explanatory mechanism (1–3 sentences).
- `translation_notes` **string** — how/why this maps to other domains.
- `confidence` **0.0–1.0** — assessor’s confidence in the coordinates.
- `assessor` **string** — name or handle of contributor.
- `version` **string** — semantic version for this record (e.g., `"0.1.0"`).
- `last_updated` **YYYY-MM-DD**.

## 4) Impossibility/Constraint Checks (optional but useful)

- `constraint_flags` **array[string]** — auto or manual flags (e.g., `"SRO=100 & GEN=100 incompatible"`).
- `impossibility_index` **number** — heuristic score if you run a checker (0 = fine).

## 5) Notation Helpers (derived; optional)

- `notation_primary` **string** — e.g., `DP_REC3.SRO30.TMP95`.
- `notation_full` **string** — `"[DP|REC:3|SRO:30|TMP:95|CPL:70|GEN:85|CAU:20|NRG:60|DET:40|REV:20]"`.

---

## Contributor Rules

1. Prefer **percentile ranks [0–100]** for all dims except `REC_count`.
2. Add at least **one anchor** per high/low/extreme coordinate.
3. Include **mechanism** and **translation_notes** (keeps the record explanatory, not just numeric).
4. Keep **instances (IP)** tied to **time/locale** if relevant in `description`.
5. Submit via PR. Expect review for: range checks, constraint sanity, duplication (>0.85 similarity).

---

## JSON Template (copy/paste)

```json
{
  "id": "REPLACE-ME",
  "name": "REPLACE ME",
  "primary_domain": "P|B|C|S",
  "level": "CN|CT|FP|DP|IP",
  "description": "2–6 sentences explaining the pattern.",
  "coordinates": {
    "REC_count": 3,
    "SRO": 0,
    "TMP": 0,
    "CPL": 0,
    "GEN": 0,
    "CAU": 0,
    "NRG": 0,
    "DET": 0,
    "REV": 0
  },
  "anchors": [
    "SRO≈30: fragile; comparable to resonance near critical Q",
    "TMP≈95: timing-critical; beat-to-beat dynamics"
  ],
  "mechanism": "What generates/sustains the pattern.",
  "translation_notes": "Where/why this maps across domains.",
  "sources": [],
  "confidence": 0.6,
  "assessor": "your-handle",
  "version": "0.1.0",
  "last_updated": "2025-09-28",
  "constraint_flags": [],
  "impossibility_index": 0,
  "notation_primary": "",
  "notation_full": ""
}

