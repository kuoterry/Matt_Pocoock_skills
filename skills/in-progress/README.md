# In Progress

還在開發中的 skill。還沒準備好發佈 —— 會有粗糙的地方、breaking change,以及被放棄的實驗。在畢業到穩定 bucket 之前,不會出現在 plugin 或頂層 README 裡。

- **[loop-me](./loop-me/SKILL.md)** —— 用目前的資料夾當成有狀態的工作區,跨多個 session 把自己 grill 成可實作的工作流程 spec。User-invoked。
- **[wizard](./wizard/SKILL.md)** —— 產生一個互動式 bash wizard,帶著人類走過一套手動流程(設定、一次性 migration、狀態轉換)—— 開啟網址、擷取數值、寫入 `.env` 與 GitHub Actions secrets。User-invoked。
- **[writing-beats](./writing-beats/SKILL.md)** —— 把一篇文章塑造成一段一段 beat 組成的旅程,像「你來決定劇情走向」那樣。選一個起始 beat,只寫那個 beat,再轉往下一個,直到文章自然收尾。
- **[writing-fragments](./writing-fragments/SKILL.md)** —— 一場從你身上挖掘片段的 grilling session —— 各種零散的寫作素材 —— 附加進同一份文件裡,當作未來文章的原始素材。
- **[writing-shape](./writing-shape/SKILL.md)** —— 拿一份原始素材的 markdown 檔,一段一段塑造成一篇文章,每一步都論證格式上的選擇。
- **[claude-handoff](./claude-handoff/SKILL.md)** —— 把目前的對話交接給一個全新的背景 agent,讓它立刻接手,透過 `claude --bg` 帶著交接摘要啟動。User-invoked。
- **[setup-ts-deep-modules](./setup-ts-deep-modules/SKILL.md)** —— 把 dependency-cruiser 接進一個 TypeScript repo,讓每個 package 都是一個深 module —— 實作藏在子資料夾裡,只能透過它的進入點檔案觸及,測試也透過這些進入點來操作它。User-invoked。
- **[to-questionnaire](./to-questionnaire/SKILL.md)** —— 把一個你沒辦法完整回答的決策,轉成一份 Markdown 問卷,讓別人非同步填寫,或在會議上填寫。它盤問你的是「怎麼發送」(給誰、你需要拿回什麼),而不是主題本身。User-invoked。
- **[batch-grill-me](./batch-grill-me/SKILL.md)** —— 一場無情的訪談,一輪一輪走過設計樹,而不是一次問一題 —— 每一輪都會問完所有前置條件已經確定的決策前緣,再依你的回答重新計算。User-invoked。
