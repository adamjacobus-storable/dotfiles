# Evidence Unit Format Reference

## Structure

Each evidence unit in the workspace file follows this format:

```markdown
#### EU-[NNN]: [Source Title]

- **Source:** [full URL]
- **Published:** [YYYY-MM-DD or "undated"]
- **Confidence:** [primary / secondary / opinion / anonymous]
- **Key claims:**
  - "[verbatim quote or close paraphrase]"
  - "[additional claim]"
- **Bound to:** [outline node(s), e.g., "1.2, 3.1"]
- **Status:** `active` | `pruned` | `merged into EU-XXX`
```

## Confidence Hierarchy

| Level         | Definition                                         | Example                                                       |
| ------------- | -------------------------------------------------- | ------------------------------------------------------------- |
| **primary**   | Original research, official documents, direct data | Government reports, peer-reviewed papers, company SEC filings |
| **secondary** | Reporting on primary sources, expert analysis      | News articles citing studies, industry analyst reports        |
| **opinion**   | Expert commentary without primary evidence         | Blog posts by domain experts, op-eds, conference talks        |
| **anonymous** | Unattributed claims, unknown authorship            | Forum posts, unsigned articles, aggregator content            |

**Rule:** Claims supported only by `opinion` or `anonymous` sources must have a confidence qualifier in the final report. Claims supported only by `anonymous` sources should be flagged as `[LOW CONFIDENCE]`.

## ID Convention

- IDs are sequential: EU-001, EU-002, EU-003...
- IDs never reuse — pruned units keep their ID (status changes to `pruned`)
- Merged units reference their target: `merged into EU-005`

## Binding Rules

- Every evidence unit MUST be bound to at least one outline node
- An outline node with zero bound evidence units cannot be drafted (flag as gap)
- Multiple units can bind to the same node (strengthens claims)
- One unit can bind to multiple nodes (cross-cutting evidence)

## Key Claims Extraction

**Prefer verbatim quotes** enclosed in quotation marks. When paraphrasing:

- Stay close to the source's language
- Never inject interpretation at extraction time
- Mark as paraphrase: `[paraphrase] The study found approximately 40% improvement`

**Extract:**

- Quantitative data (numbers, percentages, dates)
- Named findings or conclusions
- Methodology details relevant to confidence assessment
- Contradictions with other evidence units

**Do NOT extract:**

- Background context available elsewhere
- Redundant claims already captured in other units
- Speculative statements (unless speculation is the finding)

## Deduplication

When two evidence units contain overlapping claims:

1. Keep the unit with higher confidence level
2. If same confidence, keep the one with more specific claims
3. Move unique claims from the pruned unit to the kept unit
4. Update the pruned unit's status: `merged into EU-XXX`
5. Log in the Deduplication Log table
