# Engineering

我每天寫程式時用的 skill。

## User-invoked

只有你自己打出來才能觸發(Claude Code:`disable-model-invocation: true`;Codex:`agents/openai.yaml` 裡的 `policy.allow_implicit_invocation: false`)。

- **[ask-matt](./ask-matt/SKILL.md)** —— 問你目前的情況該用哪個 skill 或流程。是這個 repo 裡 user-invoked skill 的 router。
- **[grill-with-docs](./grill-with-docs/SKILL.md)** —— 一場同時會建立你專案 domain model 的 grilling session,把術語磨利,並就地更新 `CONTEXT.md` 與 ADR。
- **[triage](./triage/SKILL.md)** —— 讓 issue 沿著一套 triage role 的狀態機往前推進。
- **[improve-codebase-architecture](./improve-codebase-architecture/SKILL.md)** —— 掃描 codebase,找出可以「加深」的機會,做成一份視覺化 HTML 報告,然後針對你選的那項繼續往下 grill。
- **[setup-matt-pocock-skills](./setup-matt-pocock-skills/SKILL.md)** —— 為這個 repo 設定 engineering skill 所需環境(issue tracker、triage 標籤、domain 文件的存放方式)。每個 repo 跑一次。
- **[to-spec](./to-spec/SKILL.md)** —— 把目前的對話整理成一份 spec,發佈到 issue tracker。
- **[to-tickets](./to-tickets/SKILL.md)** —— 把任何計畫、spec,或對話拆成一組 tracer-bullet ticket,每個 ticket 都宣告自己的 blocking 關係 —— 可以是本地檔案裡的文字,也可以是真實 tracker 上原生的 blocking 連結。
- **[implement](./implement/SKILL.md)** —— 依照 spec 或一組 ticket 動手把工作做出來,在事先談好的接縫(seam)處驅動 `/tdd`,並在 commit 前用 `/code-review` 收尾。
- **[wayfinder](./wayfinder/SKILL.md)** —— 把一大坨超過一次 agent session 能裝下的工作,規劃成 issue tracker 上一張共用的 decision ticket 地圖,一次解決一張,直到通往目的地的路都清楚為止。

## Model-invoked

model 或使用者都能觸發(有豐富的觸發語句描述,讓 model 能自己找上門)。

- **[prototype](./prototype/SKILL.md)** —— 做一個用完即丟的 prototype 來回答一個設計問題:針對狀態/邏輯做一個可執行的終端機 app,或是做出幾種可切換的 UI 版本。

- **[diagnosing-bugs](./diagnosing-bugs/SKILL.md)** —— 針對難搞的 bug 與效能退化,提供一套有紀律的診斷迴圈:重現 → 最小化 → 假設 → 埋測 → 修復 → 回歸測試。
- **[research](./research/SKILL.md)** —— 針對一個問題,依照高可信度的第一手資料做調查,把結果寫成一份附引用的 Markdown 檔存進 repo,以背景 agent 的方式執行。
- **[tdd](./tdd/SKILL.md)** —— 用紅-綠-重構迴圈做 test-driven development。一次一個垂直切片地建構功能或修 bug。
- **[domain-modeling](./domain-modeling/SKILL.md)** —— 主動建立並磨利一個專案的 domain model —— 挑戰用語、用情境做壓力測試、就地更新 `CONTEXT.md` 與 ADR。
- **[codebase-design](./codebase-design/SKILL.md)** —— 設計「深」module 的共用紀律與詞彙:小介面、乾淨的接縫,可以透過介面測試。
- **[code-review](./code-review/SKILL.md)** —— 針對從某個固定點開始的 diff 做雙軸審查:**Standards**(是否符合 repo 的程式碼規範,加上 Fowler 的程式碼異味基準?)與 **Spec**(是否忠實實作了原始的 issue/PRD?),以平行 sub-agent 執行。
- **[resolving-merge-conflicts](./resolving-merge-conflicts/SKILL.md)** —— 針對進行中的 git merge 或 rebase 衝突,一個 hunk 一個 hunk 處理,依照雙方各自的原始來源追溯意圖來解決,最後完成整個操作 —— 絕不 `--abort`。
