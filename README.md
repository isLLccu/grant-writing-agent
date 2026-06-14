# Grant Writing Agent for Claude Code

A Claude Code skill that guides researchers through writing Chinese national/provincial science foundation grant proposals (基金申报书) step by step — from blank page to submission-ready draft.

Built from real experience: the skill encodes a complete methodology extracted from iterating a real grant proposal across 12 versions over 3 weeks.

---

## What problem this solves

Writing a Chinese grant proposal is hard in a specific way: reviewers expect a precise logical structure (problem chain, three-part research content, goals mapped 1-to-1 to scientific questions), but there's no widely-available tool that enforces this structure interactively.

The typical failure modes:
- Research content reads like a list of technical modules, not a problem chain
- Existing methods are criticized before being acknowledged (breaks reviewer trust)
- Formulas appear without setup sentences or symbol definitions
- Technical jargon without full names on first use
- Goals and scientific questions don't correspond to each other

This skill catches all of the above — phase by phase, with explicit checklist output.

---

## How it works

The skill runs as a **6-phase interactive workflow** inside Claude Code:

```
Phase 1 — 立项依据：三段式框架
         Build the three-paragraph opening (background → existing method limitations → core contradiction)

Phase 2 — 文献支撑定位
         Map each key claim to a specific reference. Flag potential hallucinations.

Phase 3 — 研究内容：三段递进
         Write three research sections as a problem chain (not parallel modules).
         Each section must explicitly build on the previous one.

Phase 4 — 研究目标 + 关键科学问题
         Derive goals (≤130 chars, declarative) and scientific questions (≤200 chars, interrogative).
         Verified to map 1-to-1 with the three research sections.

Phase 5 — 技术路线
         Write the technical approach with problem-first structure per aspect.
         Formula rules enforced: setup sentence → formula → symbol definitions → closing effect.

Phase 6 — 整体逻辑自查
         6-point checklist: main thread consistency, section linkage, formula completeness,
         abbreviation coverage, and register compliance.
```

The agent stops at each phase boundary and waits for user approval before proceeding.

---

## Installation

Copy the skill file to your Claude Code commands directory:

```bash
# macOS / Linux
cp skills/write-proposal.md ~/.claude/commands/write-proposal.md

# Windows (PowerShell)
Copy-Item skills\write-proposal.md $env:USERPROFILE\.claude\commands\write-proposal.md
```

Restart Claude Code. The skill will appear as `/write-proposal`.

---

## Usage

**Start from scratch:**
```
/write-proposal 你的研究方向一句话描述
```

**Continue from an existing draft:**
```
/write-proposal ./my-draft.docx
```
Claude will read the draft, identify which phase it's at, and list the top 3 issues before suggesting any rewrites.

**Work on a specific section:**
```
/write-proposal 帮我检查研究内容三部分的衔接逻辑
```

---

## Repository structure

```
grant-writing-agent/
├── README.md
├── skills/
│   └── write-proposal.md    ← The skill file (install this)
└── docs/
    └── methodology.md       ← Full grant writing methodology reference
```

---

## Design notes

**Why phase-based?**
Grant proposals fail at the logic level, not the sentence level. Splitting the work into 6 phases forces the user to validate the logical structure (problem chain, goal mapping) before polishing language — the opposite of what most LLM writing assistants do.

**Why explicit checklist output in Phase 6?**
Reviewers are busy. A ✓/✗ checklist with one specific fix per ✗ is more actionable than a paragraph of suggestions. It also makes it easy to re-run the check after edits.

**Why $ARGUMENTS supports both directions and file paths?**
Most grant writing sessions aren't start-from-scratch. The skill detects which phase a draft is at and picks up from there, which matches how real revision cycles work.

---

## Author

Lin Leshan — [@isLLccu](https://github.com/isLLccu)
