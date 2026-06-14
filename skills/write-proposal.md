Guide the user through writing a Chinese science foundation grant proposal (基金申报书) step by step. The argument ($ARGUMENTS) can be a research direction (one sentence), an existing draft (file path), or a specific section to work on.

## How to use

Work through the phases in order. After each phase, present the output and ask the user if they want to proceed to the next phase or revise. If $ARGUMENTS is a file path, read it first and identify which phase to start from based on what's already written. If $ARGUMENTS is a one-sentence research direction, start from Phase 1.

---

## Phase 1 — 立项依据：三段式框架

Build the opening of Section 1 (研究背景与意义) using this three-paragraph structure:

- **段1**：研究对象的重要性 + 为什么这个区域/场景特别难（结合具体现象或数据）
- **段2**：先肯定现有方法的贡献，再说明其瓶颈（"虽然……但……"逻辑）
- **段3**：收束到本项目核心问题（以"由此，本项目聚焦……"结尾）

Rules:
- Never open with "随着…的发展" or other vague progress statements. Start with the specific research object.
- Paragraph 2 must acknowledge existing methods before criticizing them. Never start with the limitation.
- Paragraph 3 must name the core contradiction in exactly one sentence before the closing line.

---

## Phase 2 — 文献支撑定位

For each key claim in the draft, assign a reference that directly supports it.

Output a markdown table:

| 文献（作者, 年份） | 支撑的核心论断（引用的具体句子） | 文献类型 |
|---|---|---|
| ... | ... | 背景/方法主干/应用验证 |

Rules:
- Every reference must correspond to a specific sentence in the text. Do not list references as "general background."
- Flag any reference you are not confident exists with ⚠️ (potential hallucination — ask user to verify).
- Minimum: one reference per major claim. Ideal: 2–3 per paragraph in Section 1.

---

## Phase 3 — 研究内容：三段递进

Write three research content sections (2.1). Each must follow this template:

> 针对[具体问题]，本研究拟[方法]。[问题背景 2–3句，说明为什么这个问题难]。[方法设计 2–3句，说明怎么解决]。通过该部分研究，[预期作用，呼应下一部分或最终目标]。

The three sections must form a problem chain, not parallel modules:
- **Section 1**：解决预测/建模的核心矛盾（预测主干）
- **Section 2**：在 Section 1 的基础上，解决空间/几何/边界约束问题（区域适配）
- **Section 3**：将 Section 1 + 2 的结果转化为可用的风险/评估/应用输出（风险转化）

Check: The opening of Section 2 must explicitly reference Section 1 ("在形成…基础上"). The opening of Section 3 must reference both Section 1 and 2.

---

## Phase 4 — 研究目标 + 关键科学问题

From the three research sections, derive:

**研究目标 (2.2)**：One goal per section.
Format: "建立[对象]的[方法名称]。通过[核心手段]，突破[瓶颈]，形成[能力]。"
Constraint: ≤130 characters each. Use declarative sentences.

**关键科学问题 (2.3)**：One question per section.
Format: Start with a noun phrase naming the core challenge, then list 3–4 specific sub-questions, end with "？"
Constraint: ≤200 characters each. Use interrogative sentences throughout.

Rules:
- Goals and questions must map 1-to-1 to the three research sections.
- Preferred verbs: 建立、突破、形成、刻画、抑制、转化、约束、校准.
- Do NOT repeat the same verb in goals and questions for the same section.

---

## Phase 5 — 技术路线

Write the technical approach (2.4) for each research section. Use this structure per section:

> **（N）[标题]，回答第 N 个关键科学问题。**
> 在[方面1]方面：[1句问题背景]. [方法 2–3句]. [预期效果1句].
> 在[方面2]方面：[承接方面1，1句]. [方法 2–3句]. [效果1句].
> 在[方面3]方面：[承接方面2，1句]. [方法 2–3句]. [效果1句].

Formula rules (if formulas are included):
- Every formula needs: one setup sentence before it, symbol definitions after it, one closing sentence on its effect.
- Remove any formula that can be explained in words without loss of precision.

Style rules:
- Use "动词驱动叙述": 将…转化为、嵌入、约束、刻画、抑制、校准.
- Do NOT describe model architecture or experimental setup. Focus on why this design choice addresses the stated problem.

---

## Phase 6 — 整体逻辑自查

Review the full draft against this checklist. Output each item as ✓ (pass) or ✗ (issue found), and for each ✗ provide one specific fix.

1. **主线对应**：背景段3的核心矛盾 ↔ 研究内容标题 ↔ 研究目标 ↔ 科学问题，是否一一对应？
2. **递进衔接**：Section 2 开头是否显式引用 Section 1 的输出？Section 3 开头是否引用 Section 1+2？
3. **技术路线问题驱动**：每个"在[方面]方面"是否以问题背景开头，而非直接描述模型？
4. **公式规范**：每个公式是否有引入句 + 符号说明 + 收束句？
5. **大同行可读性**：所有专业缩写是否在首次出现时给出全称？有无口语化或文学化表达？
6. **语气规范**：是否全程保持"针对…，本研究拟…"的申报书语气？有无"我们"或第一人称？

---

## General rules (apply throughout all phases)

- Write in Chinese. Match the grant proposal register: formal, declarative, problem-driven.
- Never use "随着…的发展" or "近年来，…越来越受到关注" as opening sentences.
- Always acknowledge existing methods before stating their limitations.
- Target length: research content sections ≤300 characters each; technical approach aspects ≤500 characters each.
- If the user pastes an existing draft, first identify which phase it is at and state the top 3 issues before suggesting any rewrites.
