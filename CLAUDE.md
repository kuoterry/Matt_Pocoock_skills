# CLAUDE.md

本檔案為 Claude Code(claude.ai/code)在此 repo 中工作時的指引。

## Repo 總覽

Matt Pocock 的 Agent Skills repo —— 一組以 `SKILL.md` 為基礎的 skill 集合(slash command 與 model 主動觸發的行為),涵蓋真實的軟體工程流程:grilling / 訪談、spec/ticket 流程、TDD、code review、domain modeling 等。這裡沒有應用程式碼;交付物就是這些 skill 定義本身與其配套文件。有兩種發佈管道:作為 Claude Code plugin(`.claude-plugin/`,此 repo 本身也是自己的單一 plugin marketplace),以及透過跨 harness 安裝器 `npx skills add mattpocock/skills`(skills.sh),後者會把可編輯的 skill 檔案複製進使用者的專案。

## 常用指令

- `npm run changeset` —— 為待發佈的版本記錄一筆 changeset
- `npm run version` —— 套用累積的 changeset,bump `package.json` 版號,更新 `CHANGELOG.md`
- `claude plugin validate . --strict` —— 驗證 `.claude-plugin/plugin.json` + `marketplace.json`;動到任一份 manifest 後都要跑
- `scripts/link-skills.sh` —— 把每個 skill 都 symlink 進 `~/.claude/skills` 與 `~/.agents/skills`,供本機測試用(僅限維護者自用的 dev script,不是對外安裝器)
- `scripts/list-skills.sh` —— 列出 repo 內所有 `SKILL.md` 路徑

沒有 build、lint 或自動化測試套件 —— 這個 repo 交付的是 markdown skill 定義與文件,不是應用程式碼。

## 一個 skill 的解剖結構

每個 skill 是一個資料夾,內含:

- `SKILL.md` —— frontmatter(`name`、`description`,user-invoked skill 另加 `disable-model-invocation: true`),後面接 skill 的 prose 指示內容。
- `agents/openai.yaml` —— Codex 端的旁掛 metadata(`interface.display_name`、`interface.short_description`),user-invoked skill 另配對 `policy.allow_implicit_invocation: false`。
- 選用的輔助參考檔(例如 `tdd/SKILL.md` 旁邊的 `tests.md`、`mocking.md`),由 `SKILL.md` 直接連結 —— skill 之間互相引用一律用 prose 呼叫方式(`/other-skill`),不用深入連到別的 skill 資料夾內的檔案。

user-invoked 與 model-invoked 的完整區分、以及兩份 frontmatter 檔要如何保持同步,見 [.agents/invocation.md](./.agents/invocation.md)。

## Bucket 結構與上架規則

skill 依 bucket 資料夾分類在 `skills/` 底下:

- `engineering/` —— 日常寫程式工作
- `productivity/` —— 日常非寫程式的工作流程工具
- `misc/` —— 留著但很少用,未上架
- `personal/` —— 綁定我自己的環境設定,未上架
- `in-progress/` —— 還沒準備好發佈的草稿
- `deprecated/` —— 已不再使用

`engineering/` 或 `productivity/`(**上架** bucket)裡的每個 skill,都必須在頂層 `README.md` 有對應條目,且要出現在 `.claude-plugin/plugin.json` 的 `skills` 陣列裡(Claude Code plugin 只出貨這組上架清單)。`misc/`、`personal/`、`in-progress/`、`deprecated/` 裡的 skill 不得出現在這兩處。

此 repo 同時也是自己的單一 plugin Claude Code marketplace:`.claude-plugin/marketplace.json` 列出唯一的 `mattpocock-skills` plugin。bump 發佈版號時,要讓 `.claude-plugin/plugin.json` 的 `version` 與 `package.json` 的版號保持同步 —— Claude 是依 plugin 的 `version` 來判斷已安裝使用者何時該看到更新。動到任一份 manifest 後跑一次 `claude plugin validate . --strict`。為何選擇 Claude plugin、暫緩 Codex plugin 的理由見 [.agents/adr/0002-ship-as-a-claude-code-plugin.md](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)。

頂層 `README.md` 裡每個 skill 條目都必須把 skill 名稱連結到它的 `SKILL.md`。

每個 bucket 資料夾都有自己的 `README.md`,列出該 bucket 內每個 skill 的一句話說明,並把 skill 名稱連結到其 `SKILL.md`。上架 bucket 的 `README.md` 與頂層 `README.md` 會把條目分成 **User-invoked** 與 **Model-invoked** 兩組;非上架 bucket 的 `README.md`(`misc/`、`personal/`)用平鋪清單即可。

`engineering/` 與 `productivity/` 裡的 skill 另外還有一份面向人類讀者的文件頁,放在 `docs/<bucket>/<skill-name>.md`(docs 目錄樹會鏡射 `skills/` 底下這兩個 bucket 資料夾)。發佈網址一律是 `https://aihero.dev/skills-<skill-name>`,跟 bucket 無關 —— docs 路徑只是 repo 內部組織方式。當你新增、改名,或改變 `engineering/`、`productivity/` 裡某個 skill 的行為時,要依照 [.agents/writing-docs.md](./.agents/writing-docs.md) 建立或重新同步該 skill 的 docs 頁。非上架 bucket(`misc/`、`personal/`、`in-progress/`、`deprecated/`)裡的 skill **不會**有 docs 頁。

每份 `SKILL.md` 不是 user-invoked(`disable-model-invocation: true` 加上 `agents/openai.yaml` 裡的 `policy.allow_implicit_invocation: false`,只有人類能觸發),就是 model-invoked(model 或使用者都能觸發)。詳見 [.agents/invocation.md](./.agents/invocation.md)。

[`ask-matt`](./skills/engineering/ask-matt/SKILL.md) 是幫所有使用者可觸發 skill 畫關係圖的 router。跟重新同步 docs 頁一樣的觸發時機也適用於它:每當你新增、改名、移除,或改變某個使用者可觸發 skill 在整套流程裡的定位時,都要重讀一次 `ask-matt` 的 `SKILL.md` 並更新它,確保這張圖是準的 —— 一個它從沒提過的新 skill,或一個它還在指向的舊 skill,都代表這個 router 在說謊。

要把每個 skill(重新)連結進本機 harness 的 skill 目錄(`~/.claude/skills`、`~/.agents/skills`),執行 `scripts/link-skills.sh`。每一條都是連到這個 repo 的 symlink,所以 `git pull` 就能讓已安裝的 skill 保持最新;新增、移除、改名 skill 之後要重跑這支 script。

## 其他重要參考文件

- [CONTEXT.md](./CONTEXT.md) —— 這個 repo 的 domain glossary(Issue tracker、Issue、Decision ticket、Triage role)—— 命名新概念前先讀這份。
- [.agents/adr/](./.agents/adr/) —— architecture decision record;要重新檢討某個已拍板的結構性決定(例如 bucket 化 skill vs. 扁平 plugin 路徑)前,先查這裡。
- 根目錄的 `AGENTS.md` 指向這份檔案 —— Codex 與 Claude Code 共用同一套指示。
