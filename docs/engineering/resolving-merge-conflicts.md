Quickstart:

```bash
npx skills add mattpocock/skills --skill=resolving-merge-conflicts
```

```bash
npx skills update resolving-merge-conflicts
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/resolving-merge-conflicts)

## What it does

`resolving-merge-conflicts` 一個 hunk 一個 hunk 地處理一個進行中的 git merge 或 rebase 衝突,並把整個操作做完——解決、檢查、commit。

它是依照**意圖**解決,不是依照文字。在動一個 hunk 之前,它會先把雙方各自追溯回它們的**第一手來源**——commit 訊息、PR、原始 issue——搞懂這個變動當初是為什麼做的,然後在兩邊意圖相容的地方把兩者都保留下來。它絕不會為了掩蓋衝突而發明新行為,也絕不會用 `--abort`:merge 永遠會被完成。

## When to reach for it

打 `/resolving-merge-conflicts`,或者當任務吻合時 agent 會自動找上它。

當你正在 merge 或 rebase 到一半,git 因為自己解不開的衝突而停下來時就用它。它是為了處理你眼前這個衝突,不是為了規劃這個 merge,也不是為了除錯 merge 完之後才壞掉的行為。如果 merge 已經做完,但有東西因為看不出原因而開始失敗,改用 [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs)。

## 依意圖解決

衝突裡的陷阱,是把它當成一個文字問題——選「ours」還是「theirs」,把衝突標記弄不見。這個 skill 把它當成一個**意圖**問題來處理。一個 hunk 的每一邊都存在,是因為有人想要某個東西;解法必須在可能的地方尊重兩邊的想法,而在兩者真的無法相容時,選符合這次 merge 明講目標的那一邊,並把這個取捨明講出來。

這就是為什麼第一手來源很重要。你沒辦法保留一個你沒讀過的意圖,所以工作是從歷史紀錄開始——commit、PR、ticket——而不是從 diff 開始。

## It's working if

- 每個解決掉的 hunk 都保留了雙方的行為,或是在做不到的地方把取捨講清楚。
- 沒有出現任何一邊 branch 原本都沒有的新行為。
- 專案自己的檢查——型別檢查、測試、格式——在 commit 前都被找出來並跑成綠燈。
- 這個 merge 或 rebase 一路被推到一個完成的 commit,絕不中途 abort。

## Where it fits

一個隨時可以拿來用的獨立工具:在一個 merge 或 rebase 卡住的當下觸發它,它會還你一棵乾淨、已經 commit 好的樹。它自然的鄰居是 [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs),因為一個乾淨解決但事後行為不對的 merge,是個診斷問題,不是衝突問題。不確定該用哪個 skill 時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
