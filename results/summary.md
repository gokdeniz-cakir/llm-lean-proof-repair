# Results Summary

## Overall Performance

| Model | Success Rate | Notes |
|-------|:------------:|-------|
| ChatGPT 5.1 Thinking (Extended) | **4.5/5** | Best overall, one minor typo fix needed |
| Claude 4.5 Sonnet | **3.5/5** | Decent performance, occasional syntax issues |
| Gemini 3.0 Pro | **3/5** | Good identification, execution needs work |
| Grok 4 Fast | **3/5** | Consistently skipped explanations but identification when provided is decent |
| DeepSeek V3.2 DeepThink | **2/5** | Overly general explanations, poor execution |

## Bug Types Tested

| Category | Examples |
|----------|----------|
| Variable Misuse | Wrong membership proofs, undefined identifiers |
| Arithmetic Errors | Reversed signs, wrong ε selection |
| Tactic Misuse | `linarith` on multiplicative goals, wrong lemma versions |
| Structural Issues | Missing introductions, swapped arguments |
| Rewrite Errors | Wrong direction, irrelevant patterns |

## Key Observations


1. **Identification ≠ Repair** - Several models correctly diagnosed bugs but failed to fix them
2. **Lean 4 syntax is challenging** - Common failures involved `calc` blocks and indentation
3. **Explanation quality varies widely** - From no explanation (Grok) to overly verbose (DeepSeek) to fairly excellent (ChatGPT)

## Per-File Difficulty

| File | Pass Rate | Primary Challenge |
|------|:---------:|-------------------|
| 00FirstProofs | 2.5/5 | Mixed: arithmetic, limits, bounds |
| 01EqualityRewriting | 4/5 | Straightforward rewrite bugs |
| 02IffIfAnd | 3/5 | Direction/side lemma confusion |
| 03ForallOr | 3/5 | Composition and case splits |
| 04Exists | 3.5/5 | Witness selection |


See [detailed_analysis.md](detailed_analysis.md) for full per-bug breakdown.
