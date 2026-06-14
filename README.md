# Grant Writing Agent for Claude Code

Four Claude Code skills for writing and stress-testing Chinese science foundation grant proposals (基金申报书).

Built from real experience iterating a grant proposal across 12 versions over 3 weeks.

---

## Skills

### `/write-proposal` — Draft the opening from scratch

**When to use**: You have a research direction but no draft yet.

Pass a one-sentence research direction. The skill asks three questions — research object, core contradiction, your angle — then generates a three-paragraph opening (立项依据) in grant proposal register. At the end it recommends which skill to use next.

```
/write-proposal 你的研究方向一句话描述
```

---

### `/proposal-logic` — Diagnose logical gaps

**When to use**: You have a draft section that feels off but you can't pinpoint why.

Paste draft text or pass a file path. The skill determines which part of the proposal it is, traces the argument as a logical chain, and flags every jump where a connecting step is missing — quoting the exact phrase, naming what's absent, and suggesting a one-line fix. Works on any section; no fixed structure is assumed.

```
/proposal-logic ./draft.docx
/proposal-logic    ← then paste text directly
```

---

### `/proposal-reviewer` — Simulate three reviewer types

**When to use**: The draft is mostly complete and you want to know where reviewers will push back.

Paste draft text or pass a file path. Three reviewers evaluate it independently:
- **同行专家** (domain expert): Is the method feasible? Is the novelty real?
- **大同行专家** (adjacent-field expert): Is the problem explained clearly? Does the logic hold for a non-specialist?
- **评审专家** (program officer): Is the application value concrete? Are goals measurable?

Each reviewer outputs a score and their top deductions. The summary highlights **consensus weaknesses** — issues raised by multiple reviewers — so you know what to fix first.

```
/proposal-reviewer ./draft.docx
/proposal-reviewer    ← then paste text directly
```

---

### `/proposal-refs` — Map references to claims

**When to use**: You have papers but aren't sure how to use them, or you have a draft and want to know which claims still need references.

Two modes — the skill detects which one applies based on your input:

- **Give references** → outputs what each paper can and cannot support, prevents misuse
- **Give a draft** → scans every major claim, marks coverage status, suggests search keywords for unsupported claims

Flags any reference it cannot verify with ⚠️ to prevent citation hallucination.

```
/proposal-refs ./papers.txt     ← list of titles/abstracts
/proposal-refs ./draft.docx     ← draft to audit
```

---

## Installation

Copy the skill files to your Claude Code commands directory:

```bash
# macOS / Linux
cp skills/*.md ~/.claude/commands/

# Windows (PowerShell)
Copy-Item skills\*.md $env:USERPROFILE\.claude\commands\
```

Restart Claude Code. All four skills will appear as slash commands.

---

## Typical workflows

**Starting from scratch:**
```
/write-proposal      → get an opening draft
/proposal-logic      → fix logical gaps
/proposal-reviewer   → stress-test against reviewer perspectives
/proposal-refs       → verify or find references for each claim
```

**Polishing an existing draft:**
```
/proposal-logic      → locate the breaks first
/proposal-reviewer   → then check reviewer impact
```

**Working from a pile of papers:**
```
/proposal-refs       → understand what each paper can support
/write-proposal      → then start writing with the right references in mind
```

Each skill works independently — start wherever you are in the process.

---

## Repository structure

```
grant-writing-agent/
├── README.md
├── skills/
│   ├── write-proposal.md      ← draft opening from scratch
│   ├── proposal-logic.md      ← logical gap diagnosis
│   ├── proposal-reviewer.md   ← three-reviewer simulation
│   └── proposal-refs.md       ← reference-to-claim mapping
└── docs/
    └── methodology.md         ← grant writing methodology reference
```

---

## Design notes

**Why four separate skills instead of one?**
Each skill targets a different failure mode at a different stage. A single monolithic skill would force the wrong tool on the right problem. Keeping them separate also means each can be used independently — you don't have to start from scratch to use `/proposal-reviewer` on an existing draft.

**Why does `/proposal-logic` not enforce a fixed structure?**
Most existing tools check against a template. The real problem is logical breaks within whatever structure the author chose. Detecting jumps in the author's own argument is harder and more useful.

**Why does `/proposal-refs` flag hallucinations explicitly?**
LLMs confidently produce plausible-sounding fake citations. The skill treats any reference it cannot verify as medium-risk and surfaces it, rather than silently including it.

---

## Author

Lin Leshan — [@isLLccu](https://github.com/isLLccu)
