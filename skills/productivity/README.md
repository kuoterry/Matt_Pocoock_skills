# Productivity

一般工作流程工具,跟寫程式無關。

## User-invoked

只有你自己打出來才能觸發(Claude Code:`disable-model-invocation: true`;Codex:`agents/openai.yaml` 裡的 `policy.allow_implicit_invocation: false`)。

- **[grill-me](./grill-me/SKILL.md)** —— 針對一個計畫或設計被無情地訪談,直到決策樹上每一個分支都被解決為止。
- **[handoff](./handoff/SKILL.md)** —— 把目前的對話壓縮成一份交接文件,讓另一個 agent 能接手繼續做。
- **[teach](./teach/SKILL.md)** —— 用目前的資料夾當成一個有狀態的教學工作區,跨多個 session 教使用者一項新技能或概念。
- **[writing-great-skills](./writing-great-skills/SKILL.md)** —— 寫好、改好 skill 的參考資料:讓一個 skill 行為可預期所需的詞彙與原則。

## Model-invoked

model 或使用者都能觸發(有豐富的觸發語句描述,讓 model 能自己找上門)。

- **[grilling](./grilling/SKILL.md)** —— 針對一個計畫、決策,或想法無情地訪談使用者,直到決策樹上每一個分支都被解決為止。
