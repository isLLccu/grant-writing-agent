# Grant Writing Agent for Claude Code

Four Claude Code skills for writing and stress-testing Chinese science foundation grant proposals (基金申报书).

Built from real experience iterating a grant proposal across 12 versions over 3 weeks.

---

## Skills

### `/write-proposal` — Draft the opening from scratch
Start from a one-sentence research direction. The skill asks three targeted questions (research object, core contradiction, your angle), then drafts the opening section (立项依据) in the right register. Points you to the next skill to use.

### `/proposal-logic` — Diagnose logical gaps
Paste any section of a draft. The skill identifies which part of the proposal it is, maps the argument as a chain, and flags every jump where a connecting step is missing — with the exact quote, what's missing, and a one-line fix. Works on any section, no fixed structure assumed.

### `/proposal-reviewer` — Simulate three reviewer types
Get independent feedback from three perspectives: a domain expert (technical feasibility, real novelty), an adjacent-field expert (clarity, logical flow, jargon), and a program officer (application value, measurable goals, presentation). Each gives a score and their top deduction. The output highlights "consensus weaknesses" — issues flagged by multiple reviewers — to prioritize fixes.

### `/proposal-refs` — Map references to claims
Two modes: give it papers to learn what each one can and cannot support; or give it a draft to find which claims are unsupported and what to search for. Flags potential reference hallucinations.

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

## Typical workflow

```
/write-proposal 你的研究方向
      ↓
/proposal-logic   ← check if the logic holds
      ↓
/proposal-reviewer ← stress-test against reviewer perspectives
      ↓
/proposal-refs    ← find or verify references for each claim
```

Each skill works independently — use whichever fits where you are in the writing process.

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
