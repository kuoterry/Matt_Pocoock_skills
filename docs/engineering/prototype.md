Quickstart:

```bash
npx skills add mattpocock/skills --skill=prototype
```

```bash
npx skills update prototype
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/prototype)

## What it does

`prototype` 建一個小小的、用完即丟的程式,唯一的工作是回答一個設計問題 —— 這個狀態模型感覺對不對,或這個 UI 該長什麼樣子。

這段程式碼**從第一天起就是用完即丟的**,而且會被標明。它不帶測試、除了讓程式跑得起來以外沒有錯誤處理、沒有抽象化,也沒有持久化。重點是快速學到一件事,然後把它刪掉 —— 所以一旦你開始把它「做硬」,你就已經不算在做 prototype 了。

## When to reach for it

打 `/prototype`,或者當任務吻合時 agent 會自動找上它。

當你有一個很難光靠紙上談兵解決的設計問題時就用它 —— 一個有著你腦子裝不下的邊界案例的狀態機,或是一個你得看到幾個版本並排比較才能想像出來的畫面。如果反過來,是已經做好的東西行為不對勁、你需要查出原因,用 [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs);prototype 探索的是要蓋什麼,不是已蓋好的東西為什麼壞了。

## 兩條分支

問題決定形狀,而形狀有兩種:

- **「這個邏輯/狀態模型感覺對不對?」**——一個小小的互動式終端機 app,把狀態機推過那些彆扭的邊界案例,每次動作後都印出完整的狀態,讓你看清楚變了什麼。
- **「這個東西該長什麼樣子?」**——在同一個 route 上做出幾種截然不同的 UI 版本,可以從一個浮動列切換,讓你比較的是真實渲染出來的畫面,而不是憑空想像。

選錯分支會浪費掉整個 prototype,所以問題要先問清楚。兩條分支都把狀態放在記憶體裡,一個指令就能跑起來,每一步都把完整狀態端出來。

## 把 prototype 留成第一手資料

一個做完的 prototype 會留下兩樣東西。**答案**——結論,加上它解決的那個問題——是你要長久保存下來的東西(一則 commit 訊息、一份 ADR、一個 issue)。**prototype 本身是一份第一手資料**——這個答案是從這份可執行的證據推出來的。

這個 prototype 不屬於 main branch:沒有測試、沒有錯誤處理、沒有東西要維護。但這不是把它銷毀的理由。答案捕捉下來之後,把任何驗證過的決定折進真正的程式碼裡,再把這個 prototype 保留在一個用完即丟的 branch 上——不在 main 裡,永遠不 merge——並在對應的實作 issue 上留一個指向它的 context 指標。main branch 保持乾淨;原始的探索過程只要點一下就能讓任何想重跑的人找到。一個爛在 main branch 裡的 prototype 已經失去它的用途;一個以第一手資料的形式保存在旁支 branch 上的,則沒有。

## Where it fits

`prototype` 是一個隨時可以拿來用的獨立工具:你切進去解決一個設計問題,然後再切出來。它的答案常常會餵給下一步 —— 一個驗證過的狀態模型或 UI 方向,會變成 [to-spec](https://aihero.dev/skills-to-spec) 拿去寫成文件的底定輸入,或是一個值得透過 [domain-modeling](https://aihero.dev/skills-domain-modeling) 記錄下來的架構決策。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
