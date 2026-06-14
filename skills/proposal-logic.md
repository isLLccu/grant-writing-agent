Diagnose logical gaps in the grant proposal text provided in $ARGUMENTS (file path or pasted text). If no argument is given, ask the user to provide the text.

Read the input first if it is a file path.

---

## Process

**Step 1 — Identify the section**
Determine which part of a grant proposal this text is from:
- 研究背景与意义 (background & significance)
- 研究现状 (literature review)
- 研究内容 (research content)
- 研究目标 (objectives)
- 关键科学问题 (key scientific questions)
- 技术路线 (technical approach)
- Other / unclear

State your determination in one line before proceeding.

**Step 2 — Map the logical chain**
Trace the argument the text is trying to make. Write it as a chain:
> Claim A → Claim B → Claim C → Conclusion

Do this for the text as written — include gaps if they exist.

**Step 3 — Find the breaks**
For each place where the chain jumps without a bridge, output:

```
[Gap N] "...exact quote where the jump happens..."
→ Missing link: the text goes from [X] to [Y] without establishing [Z]
→ Fix: add a sentence that [specific action — e.g. "explains why X leads to Y" or "defines the term before using it"]
```

Only flag real logical gaps — missing causal connections, undefined terms used as if known, conclusions that don't follow from the premises. Do not flag style issues or word choice.

**Step 4 — Overall verdict**
- Logic completeness: Strong / Moderate / Weak
- Most critical gap to fix first (one sentence)
- Estimated number of sentences needed to close all gaps: [N]

---

## Rules

- Always quote the exact text when identifying a gap. Never describe it vaguely.
- If the logic is actually sound, say so clearly — do not invent problems.
- If the text is too short to evaluate (under ~100 characters), say so and ask for more context.
