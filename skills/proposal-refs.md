Map references to claims in a grant proposal. $ARGUMENTS can be:
- A list of paper titles / abstracts (→ outputs what each reference can and cannot support)
- A draft text file path (→ outputs which claims need references and which are already covered)
- Both combined (→ matches references to uncovered claims)

Read any file paths before proceeding. If $ARGUMENTS is empty, ask the user whether they want to analyze references or a draft.

---

## Mode 1 — Given references: what can each support?

If the input is a list of papers (titles, abstracts, or both), for each paper output:

**[Author, Year] — [Title shortened to ~8 words]**
- Claim type it supports: Background importance / Existing method limitation / Method feasibility / Application value / Evaluation benchmark
- Can support: "[one sentence the paper directly justifies]"
- Cannot support: "[one common misuse — a claim that sounds related but goes beyond what the paper shows]"
- Risk of hallucination: Low / Medium (flag Medium if you are uncertain the paper exists or the content matches)

---

## Mode 2 — Given a draft: which claims need references?

If the input is a draft text, go through each substantive claim and classify it:

| Claim (quoted from text) | Reference status | Action needed |
|---|---|---|
| "..." | ✓ Has reference | — |
| "..." | ✗ Needs reference, none given | Search suggestion: [keywords] |
| "..." | — No reference needed (logical inference / definition) | — |

After the table, output:
- Total unsupported claims: N
- Highest-priority claim to find a reference for: [quote] — because [reason]

---

## Mode 3 — Both draft and references given

Match each unsupported claim from the draft to the most suitable reference from the list. For each match:
- Claim: "..."
- Best match: [Author, Year]
- Fit quality: Strong / Partial / Weak
- If Partial or Weak: explain what the reference supports and what it doesn't

---

## Rules

- Never fabricate paper titles or authors. If uncertain whether a paper exists, flag it with ⚠️.
- A reference "supports" a claim only if its findings directly justify it — not just if the topic is related.
- Keep each entry concise. The goal is actionable mapping, not summaries.
