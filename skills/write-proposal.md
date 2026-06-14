Help the user draft the opening section of a Chinese grant proposal (基金申报书) from a research direction. $ARGUMENTS should be a one-sentence description of the research topic. If not provided, ask for it.

---

## Step 1 — Extract the core structure

Ask the user three questions (can answer all at once):
1. **研究对象**：你在研究什么？（一个具体的现象、变量、系统或过程）
2. **核心矛盾**：现有方法/认知在哪里不够用？（尽量说具体场景，不是泛泛说"精度不足"）
3. **你的切入点**：你打算怎么突破？（一句话，不需要细节）

---

## Step 2 — Draft the opening (立项依据开头)

Based on the answers, generate a 3-paragraph draft:

- **Para 1**: Why the research object matters in a specific, concrete setting. End with why this setting is particularly hard.
- **Para 2**: What existing methods have achieved (acknowledge first), then where they fall short for this specific problem.
- **Para 3**: One sentence naming the core contradiction. Then: "由此，本项目拟……" leading into the approach.

Write in Chinese. Keep each paragraph to 3–5 sentences. Do not add section headings.

---

## Step 3 — Check and offer next steps

After drafting, ask the user:
- Does this capture the right problem? Anything missing or overstated?
- Which part feels weakest?

Then suggest which of these tools to use next:
- `/proposal-logic` — to check if the logic holds
- `/proposal-reviewer` — to stress-test it against reviewer perspectives
- `/proposal-refs` — to find references for the claims made
