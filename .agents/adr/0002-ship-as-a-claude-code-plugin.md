# 以原生 Claude Code plugin 出貨這組 skill;暫緩原生 Codex plugin

這些 skill 一直都能透過 [skills.sh](https://skills.sh/mattpocock/skills)(`npx skills add mattpocock/skills`)安裝,它會把可編輯的 skill 檔案複製進使用者的專案,橫跨 Claude Code、Codex,以及其他符合 Agent-Skills 標準的 harness。一個反覆出現的需求是**即插即用**的發佈方式:訂閱這組 skill 當成一個唯讀、隨時最新的包裝,而不是自己擁有的一份 fork。這正是原生 plugin 系統提供的東西。

我們出貨一個原生的 **Claude Code plugin**,原生 **Codex plugin** 則暫時**擱置**。這個拆分是被兩個生態系各自的 plugin manifest 挑選 skill 的方式,對上這個 repo 的 bucket 化結構所逼出來的。

## 限制所在:bucket 化的 skill vs. 單一路徑選擇

skill 放在 `skills/` 底下的 bucket 資料夾裡 —— `engineering/` 與 `productivity/` 是**上架**(有出貨);`misc/`、`personal/`、`in-progress/`、`deprecated/` **沒有**。一個 plugin 必須只曝露上架的那組,而這組橫跨了其中兩個 bucket 資料夾。

- **Claude Code** —— `.claude-plugin/plugin.json` 接受 `skills` 是一組**明確 skill 目錄路徑的陣列**。我們把上架的 skill 一個一個列出來,毫無疑義地排除其他所有東西,再加上 `.claude-plugin/marketplace.json`,讓這個 repo 變成自己的單一 plugin marketplace。已完整驗證過:`claude plugin validate . --strict` 通過,`marketplace add` → `install` 也能解析出所有上架的 skill。

- **Codex** —— `.codex-plugin/plugin.json` 的 `skills` 只接受**單一路徑字串**(給陣列會被拒絕,回傳 `missing or invalid plugin.json`),Codex 會遞迴地在這個路徑底下找 `SKILL.md` 檔案。沒有辦法從一個路徑指定兩個 bucket 資料夾,或是篩出一個子集合。測試過兩種逃生口,都被否決:
  - 指向 `./skills/` 的話,會連 `deprecated/`、`in-progress/`、`personal/`、`misc/` 一起出貨 —— 這些是我們刻意不上架的退役、草稿,以及個人專用 skill。
  - 一個用 **symlink** 指到各 bucket、篩選過的扁平資料夾撐不過安裝過程:Codex 會把 plugin 的目錄樹複製進它的 cache,而且**會把 symlink 丟掉**,結果 skill 到手時是空的。

唯一能穩定給 Codex 一條「只含上架內容」單一路徑的做法是:(a)**重構**,讓 `skills/` 底下只放上架的 skill(把沒上架的 bucket 搬出去 —— 這個改動的波及範圍很大,牽涉 `CLAUDE.md`、`scripts/link-skills.sh`、各 bucket README,以及仰賴 `in-progress/`、`personal/` 的本地開發流程),或是 (b)**提交重複的副本**,把上架的 skill 放進一個扁平資料夾裡(要維護同步、多一個真相來源)。這兩個都是結構性的決定,不該順手包進「出貨 Claude plugin」這件事裡。這很可能就是當初 plugin 一直沒出貨、後來被淡忘的真正原因:這兩種 manifest 格式,原本就沒辦法乾淨地表達「一個 bucket 化 repo 裡篩選過的子集合」。

## 決定

- 現在就出貨 **Claude Code plugin**(`.claude-plugin/plugin.json` + `.claude-plugin/marketplace.json`),篩選到只剩上架的那組,當作 v1.2 的主打交付項目。
- **skills.sh** 繼續當通用安裝器 —— 它現在就已經在服務 Codex 與其他 harness,所以不會有 Codex 使用者因此沒有安裝路徑可用。
- **暫緩**原生 Codex plugin,直到我們在「把 `skills/` 重構成只放上架內容」與「提交一份產生出來的扁平副本」之間做出選擇。等 Codex 支援 `skills` 陣列/include-list,或是安裝時能保留 symlink,再重新考慮。

## 由此產生的不變條件

- 每個上架的 skill,都要在 `.claude-plugin/plugin.json` 的 `skills` 陣列裡有一筆條目(這原本就是 `CLAUDE.md` 裡的規則;現在它也同時把關 plugin 的內容)。
- `.claude-plugin/plugin.json` 的 `version` 要跟著 `package.json` 的版號走 —— 發佈時兩者一起 bump。Claude 是依 plugin 的 `version` 來判斷已安裝的使用者何時該看到更新。
