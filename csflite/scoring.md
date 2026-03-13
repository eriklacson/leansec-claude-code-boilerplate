# CSFLite Scoring Methodology

## Coverage Scoring

CSFLite scores represent **coverage** — does this capability exist? — not maturity, effectiveness, or risk.

Each control is scored:
- **Yes** (1.0) — the capability exists in intentional, documented form
- **Partial** (0.5) — some evidence exists but incomplete or informal
- **No** (0.0) — no evidence the capability exists

## Weighted Calculation

Each control carries a weight reflecting its relative importance (1.0 = foundational, 1.2 = important, 1.5 = critical).

- **Assessment score** = response score × weight
- **Gap score** = weight − assessment score
- **Overall coverage** = sum of assessment scores / sum of all weights

## What Scores Mean

A coverage score of 75% means: "75% of assessed governance outcomes exist in some intentional form."

It does NOT mean: the organization is 75% secure, 75% compliant, or has mitigated 75% of risk.

## What Scores Are Useful For

- Tracking progress over time within the same organization
- Identifying which CSF Functions have the largest coverage gaps
- Communicating coverage status to leadership in aggregate form
- Prioritizing remediation by gap score (highest gap = most impactful fix)

## What Scores Are NOT Useful For

- Comparing organizations against each other
- Claiming compliance with any standard or regulation
- Representing overall cybersecurity health or risk posture
- Replacing professional risk assessment or penetration testing
