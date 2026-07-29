Quickstart:

```bash
npx skills add mattpocock/skills --skill=setup-matt-pocock-skills
```

```bash
npx skills update setup-matt-pocock-skills
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/setup-matt-pocock-skills)

## What it does

`setup-matt-pocock-skills` 教會一個 repo,engineering skill 在裡面該怎麼運作——issue 放在哪、triage 標籤叫什麼名字、domain 文件擺在哪裡——並把這些答案記錄成其他 skill 會讀的**設定**。

它寫的是設定,不是寫死行為。整條 engineering 鏈假設 `docs/agents/` 底下存在三份檔案;這個 skill 就是那個一次性的 bootstrap,從你實際的 repo 裡(`git remote`、既有的標籤、既有的 `CONTEXT.md`)探查出這些答案,再跟你確認,而不是憑空猜測。它是由 prompt 驅動的——探查、把找到的東西呈現出來、確認、再寫入——不是一套固定死的 scaffold。

## When to reach for it

你打 `/setup-matt-pocock-skills` 來觸發它——agent 不會自己去找它。

**每個 repo,在第一次用到任何其他 engineering skill 之前,用一次**。如果 [triage](https://aihero.dev/skills-triage)、[to-spec](https://aihero.dev/skills-to-spec),或 [to-tickets](https://aihero.dev/skills-to-tickets) 開始瞎猜你的 issue 放在哪、或套用根本不存在的標籤,就代表這裡還沒設定過。只有要換 issue tracker,或想重新來過時才需要重跑;日常的微調只要直接編輯 `docs/agents/*.md` 就好。

## 三個決定

它每一項都會先給一個建議答案,你一個字就能接受,並且能推斷出來的就直接跳過——所以多數執行過程只是幾個快速確認:

- **Issue tracker**——工作追蹤在哪裡,讓 `triage`/`to-spec`/`to-tickets` 知道該呼叫 `gh`、`glab`、把 markdown 寫進 `.scratch/`,還是照你描述的流程走。GitHub、GitLab、本地 markdown,或其他。(它會提議跟你的 `git remote` 相符的那一個。)
- **Triage 標籤**——只有在安裝了 `triage` skill 時才會問,而且只問:要沿用預設標籤嗎(`needs-triage`、`needs-info`、`ready-for-agent`、`ready-for-human`、`wontfix`)?只有在你的 tracker 已經在用別的名字時才回答不要,這樣 `triage` 才會套用真正存在的標籤,而不是建出重複的。
- **Domain 文件**——預設假設是單一 context(根目錄一份 `CONTEXT.md` + `docs/adr/`),這適合幾乎所有 repo;只有偵測到 monorepo 訊號時,才會提出多 context 地圖的選項。

輸出是 `docs/agents/` 底下的一組檔案——`issue-tracker.md`、`domain.md`,以及當 `triage` 有安裝時的 `triage-labels.md`——再加上,在 repo 已經在用的 `CLAUDE.md` 或 `AGENTS.md` 裡,加一個指向它們的 `## Agent skills` 區塊。這些檔案就是整套工具其餘部分站立的共用基礎。

## It's working if

- `issue-tracker.md` 與 `domain.md` 落在 `docs/agents/` 底下(如果有裝 `triage` 就再加上 `triage-labels.md`),你的 `CLAUDE.md` 或 `AGENTS.md` 裡也出現一個 `## Agent skills` 段落。
- 它提議的 tracker 跟你真實的 `git remote` 相符,標籤也跟你 repo 裡已經存在的字串相符。
- 之後,`triage` 與 `to-tickets` 會直接對正確的地方、用正確的標籤動作,而不會再詢問或用猜的。

## Where it fits

`setup-matt-pocock-skills` 是**只跑一次的初始設定**——整套 engineering skill 站立的地基,不是一個你會重複執行的步驟。它的鄰居是那些讀取它寫下內容的 skill:[triage](https://aihero.dev/skills-triage)(因為它套用這裡設定好的標籤詞彙),以及 [to-spec](https://aihero.dev/skills-to-spec) / [to-tickets](https://aihero.dev/skills-to-tickets)(因為它們發佈到這裡設定好的 issue tracker)。先跑這個;下游的一切都假設它已經跑過了。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
