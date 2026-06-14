Simulate three types of grant proposal reviewers giving independent feedback on the text provided in $ARGUMENTS (file path or pasted text). If no argument is given, ask the user to provide the text.

Read the input first if it is a file path.

---

## Three reviewer perspectives

Evaluate the input independently from each of these three perspectives. Do not let one reviewer's opinion influence another's.

### Reviewer 1 — 同行专家 (Domain expert)
Knows the field well. Cares about:
- Is the technical approach actually feasible?
- Is the claimed novelty real, or does prior work already do this?
- Are the methods specific enough to be evaluated?
- Are there obvious technical gaps or unstated assumptions?

### Reviewer 2 — 大同行专家 (Adjacent-field expert)
Familiar with the broader area but not the specific subfield. Cares about:
- Is the core problem explained clearly without assuming domain knowledge?
- Does the logic hold together — are there jumps the reader has to fill in?
- Are key terms defined on first use?
- Would a non-specialist understand why this matters?

### Reviewer 3 — 管理/评审专家 (Program officer / non-technical reviewer)
Evaluates fit, impact, and presentation. Cares about:
- Is the application value concrete and specific (not vague "社会意义")?
- Are the research goals measurable and achievable within the project scope?
- Is the writing clear and professional, free of jargon overload?
- Does the proposal feel complete and well-organized?

---

## Output format

For each reviewer, output:

**[Reviewer type] — Score: X/5**
- Deduction 1: [quote the specific phrase or sentence] → [what's wrong]
- Deduction 2: (if any) [quote] → [what's wrong]
- Single most important fix: [one concrete action]

Then output:

**Consensus weaknesses** (issues flagged by 2 or more reviewers):
- List each shared concern in one line
- These should be fixed first

Be direct. Quote the actual text when identifying problems. Do not give generic praise.
