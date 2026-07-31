# CLAUDE.md

本檔案為 Claude Code(claude.ai/code)在此 repo 中工作時的指引。

## Repo 總覽

Matt Pocock 的 Agent Skills repo —— 一組以 `SKILL.md` 為基礎的 skill 集合(slash command 與 model 主動觸發的行為),涵蓋真實的軟體工程流程:grilling / 訪談、spec/ticket 流程、TDD、code review、domain modeling 等。這裡沒有應用程式碼;交付物就是這些 skill 定義本身與其配套文件。有兩種發佈管道:作為 Claude Code plugin(`.claude-plugin/`),以及透過跨 harness 安裝器 `npx skills add mattpocock/skills`(skills.sh),後者會把可編輯的 skill 檔案複製進使用者的專案。

plugin 管道又有兩條路徑,別搞混:

- **官方 marketplace(README 給一般使用者的那條)**:`claude plugins install mattpocock-skills`,不用先 add 任何 marketplace,更新自動送達。
- **本 repo 自帶的單一 plugin marketplace**:`.claude-plugin/marketplace.json` 讓任何人可以 `/plugin marketplace add <這個 repo 的路徑或 git URL>` 直接裝這份原始碼。**本機路徑(例如 `D:\Git\Matt_Pocoock_skills`)只有這台機器有效**;要給別人裝就得給對方拿得到的 git URL,而這份 working copy 的 `origin` 是 Synology git server,對方需要 NAS 存取權與 SSH key(見最下方「本地狀態」)。

## 常用指令

- `npm run changeset` —— 為待發佈的版本記錄一筆 changeset
- `npm run version` —— 套用累積的 changeset,bump `package.json` 版號,更新 `CHANGELOG.md`
- `claude plugin validate . --strict` —— 動到任一份 manifest 後都要跑。**注意它的輸出只印 `Validating marketplace manifest: ...` 一行**,不要以為 `plugin.json` 內容(尤其 `skills` 陣列裡的路徑是否真的存在)也被深驗過了 —— 那要靠下面第 1 條漂移檢查自己確認
- `scripts/link-skills.sh` —— 把 `deprecated/` 以外的每個 skill symlink 進 `~/.claude/skills` 與 `~/.agents/skills`,供本機測試用(僅限維護者自用的 dev script,不是對外安裝器;檔頭明文寫「修改它、或要求修改它,都不會被核准」—— 不要動這支 script)
- `scripts/list-skills.sh` —— 列出 repo 內所有 `SKILL.md` 路徑

沒有 build、lint 或自動化測試套件 —— 這個 repo 交付的是 markdown skill 定義與文件,不是應用程式碼。唯一可自動驗證的是下面三條漂移檢查(前兩條見「Bucket 結構與上架規則」,第三條見「一個 skill 的解剖結構」),動過 skill 資料夾後跑一次:

```bash
# 1. plugin.json 的 skills 陣列 == engineering/ + productivity/ 實際內容
diff <(node -e "console.log(require('./.claude-plugin/plugin.json').skills.map(s=>s.replace('./skills/','')).join('\n'))" | LC_ALL=C sort) \
     <(find skills/engineering skills/productivity -name SKILL.md | sed 's|^skills/||;s|/SKILL.md$||' | LC_ALL=C sort)

# 2. 每個上架 skill 都有對應 docs 頁,且沒有孤兒 docs 頁
diff <(find skills/engineering skills/productivity -name SKILL.md | sed 's|^skills/||;s|/SKILL.md$||' | LC_ALL=C sort) \
     <(find docs -name '*.md' | sed 's|^docs/||;s|\.md$||' | LC_ALL=C sort)

# 3. 每份 SKILL.md 旁邊都有 agents/openai.yaml(所有 bucket 都適用,不只上架那兩個)
diff <(find skills -name SKILL.md | sed 's|/SKILL.md$||' | LC_ALL=C sort) \
     <(find skills -name openai.yaml | sed 's|/agents/openai.yaml$||' | LC_ALL=C sort)
```

(一定要 `LC_ALL=C sort`,否則 `-` 與字母的排序差異會產生假的 diff。頂層與各 bucket `README.md` 的條目仍需人工核對,沒有自動檢查。)

發版流程實際上由 CI 驅動:`.github/workflows/release.yml` 在 push 到 `main` 時跑 changesets action,自動開一個 `chore: version skills` PR(`npx changeset version`),合併後打 tag(`npx changeset tag`)。所以本機通常只需要 `npm run changeset` 記錄變更,不用自己跑 `npm run version`。

**注意:changesets 只 bump `package.json`,不會動 `.claude-plugin/plugin.json` 的 `version`** —— 那份一律手動維護,慣例是**預先寫上下一次發佈的目標版號**,等 changesets 套用後 `package.json` 才追上來。所以在兩者之間看到落差是正常狀態,不是要修的 bug:`plugin.json` 領先 `package.json` 一個版號,`.changeset/` 裡待套用的那批(含 `minor`)一旦 release 就會把 `package.json` 帶上來,自然收斂。要看當下實際數字自己讀那兩份 JSON 與 `ls .changeset/*.md`,不要相信這裡寫死的快照(2026-07 當時是 plugin 1.2.0 / package 1.1.0 / 10 筆待套用)。

因此**不要**把 `plugin.json` 的版號往下改去「對齊」目前的 `package.json` —— Claude 是靠 plugin `version` 判斷已安裝使用者該不該看到更新,降版會讓裝過該版的人收不到更新訊號。要動版號時只往上加,並確認新值 ≥ `package.json` 套用完 changeset 後的預期版號。

## 一個 skill 的解剖結構

每個 skill 是一個資料夾,內含:

- `SKILL.md` —— frontmatter(`name`、`description`,user-invoked skill 另加 `disable-model-invocation: true`),後面接 skill 的 prose 指示內容。
- `agents/openai.yaml` —— Codex 端的旁掛 metadata(`interface.display_name`、`interface.short_description`),user-invoked skill 另配對 `policy.allow_implicit_invocation: false`。這是**所有** bucket 的硬性規定,不只上架的那兩個 —— 現況是每一份 `SKILL.md` 旁邊都有一份 `openai.yaml`(含 `misc/`、`personal/`、`in-progress/`、`deprecated/`),新增 skill 時別漏掉 —— 用「常用指令」裡的第 3 條漂移檢查驗證。
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

六個 bucket 資料夾都有自己的 `README.md`(含 `in-progress/`、`deprecated/`),列出該 bucket 內每個 skill 的一句話說明,並把 skill 名稱連結到其 `SKILL.md`。上架 bucket 的 `README.md` 與頂層 `README.md` 會把條目分成 **User-invoked** 與 **Model-invoked** 兩組;非上架 bucket 的 `README.md` 用平鋪清單即可。

skill 名稱在整個 repo 內是**扁平的全域命名空間**,不是 per-bucket:`link-skills.sh` 用 `basename` 當 symlink 名,`~/.claude/skills/<name>` 只有一個位置。兩個不同 bucket 出現同名 skill 時不會報錯,後跑到的那個會靜默蓋掉前一個。所以新增或改名 skill 前先確認名稱在 `scripts/list-skills.sh` 的輸出裡是唯一的。

`engineering/` 與 `productivity/` 裡的 skill 另外還有一份面向人類讀者的文件頁,放在 `docs/<bucket>/<skill-name>.md`(docs 目錄樹會鏡射 `skills/` 底下這兩個 bucket 資料夾)。發佈網址一律是 `https://aihero.dev/skills-<skill-name>`,跟 bucket 無關 —— docs 路徑只是 repo 內部組織方式。當你新增、改名,或改變 `engineering/`、`productivity/` 裡某個 skill 的行為時,要依照 [.agents/writing-docs.md](./.agents/writing-docs.md) 建立或重新同步該 skill 的 docs 頁。非上架 bucket(`misc/`、`personal/`、`in-progress/`、`deprecated/`)裡的 skill **不會**有 docs 頁。

每份 `SKILL.md` 不是 user-invoked(`disable-model-invocation: true` 加上 `agents/openai.yaml` 裡的 `policy.allow_implicit_invocation: false`,只有人類能觸發),就是 model-invoked(model 或使用者都能觸發)。詳見 [.agents/invocation.md](./.agents/invocation.md)。

[`ask-matt`](./skills/engineering/ask-matt/SKILL.md) 是幫所有使用者可觸發 skill 畫關係圖的 router。跟重新同步 docs 頁一樣的觸發時機也適用於它:每當你新增、改名、移除,或改變某個使用者可觸發 skill 在整套流程裡的定位時,都要重讀一次 `ask-matt` 的 `SKILL.md` 並更新它,確保這張圖是準的 —— 一個它從沒提過的新 skill,或一個它還在指向的舊 skill,都代表這個 router 在說謊。

要把 skill(重新)連結進本機 harness 的 skill 目錄(`~/.claude/skills`、`~/.agents/skills`),執行 `scripts/link-skills.sh` —— 它連結 `deprecated/` 以外的所有 bucket(包含 `misc/`、`personal/`、`in-progress/`),不只上架的那兩個。每一條都是連到這個 repo 的 symlink,所以 `git pull` 就能讓已安裝的 skill 保持最新;新增、移除、改名 skill 之後要重跑這支 script(它只會新增/覆寫,**不會**清掉已改名或已刪除 skill 留下的舊 symlink,那些要自己 `rm`)。

## 其他重要參考文件

- [CONTEXT.md](./CONTEXT.md) —— 這個 repo 的 domain glossary(Issue tracker、Issue、Decision ticket、Triage role)—— 命名新概念前先讀這份。
- [.agents/adr/](./.agents/adr/) —— architecture decision record;要重新檢討某個已拍板的結構性決定(例如 bucket 化 skill vs. 扁平 plugin 路徑)前,先查這裡。
- `.out-of-scope/` —— **已明確判定不做**的需求,每份寫明理由與對應的 upstream issue 編號(例如 grilling 不設問題數量上限、只支援主流 issue tracker)。實作任何看起來合理的新功能前先掃這裡 —— 已經被拒絕過的東西不要再做一次。
- 根目錄的 `AGENTS.md` 指向這份檔案 —— Codex 與 Claude Code 共用同一套指示。

## 這份 working copy 的本地狀態

這不是 upstream 的乾淨 clone:

- `origin` 指向使用者自己的 Synology git server(`kcc3713.synology.me:/volume1/Git_Server/Matt_Pocoock_skills.git`),**不是** `github.com/mattpocock/skills`。要拉 upstream 得自己另加 remote。
- `CLAUDE.md`、`README.md`、`CONTEXT.md`、`.agents/`、`docs/`、各 bucket `README.md` 都已被本地 commit 翻成繁體中文(分支 `feature/zh-tw-translation`,同內容也在 `main`)。skill 本體(`SKILL.md`)維持英文。之後合併 upstream 變更時,這些檔案幾乎必然衝突。
- `使用手冊.html`、`本地翻譯版怎麼用.pdf` 是本地新增的中文使用說明,upstream 沒有。
