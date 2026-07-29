Quickstart:

```bash
npx skills add mattpocock/skills --skill=improve-codebase-architecture
```

```bash
npx skills update improve-codebase-architecture
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/improve-codebase-architecture)

## What it does

`improve-codebase-architecture` 掃描一個 codebase,找出**可以加深的機會** —— 一個淺 module(介面幾乎跟它藏的東西一樣複雜)可以變深的地方 —— 把它們做成一份獨立的視覺化 HTML 報告,然後針對你選的那個繼續往下 grill。

它**不會**丟給你一份扁平的重構清單。每個候選項都得先通過**刪除測試**——刪掉這個 module,是會把複雜度*集中*到一個更小的介面背後,還是只是把它搬來搬去?只有「集中」的情況才會拿到一張卡片。這個過濾條件正是阻止這份報告淪為通用清理建議的關鍵。

除非你指定它去看特定區域,否則它也會把範圍限縮到開發真正在動的地方 —— 讀最近的 commit,偏向你還在改的程式碼。加深一個 module 的價值,在於讓未來對它的變動更容易,所以它會對 repo 裡最近有變動的部分加重權重。

## When to reach for it

你打 `/improve-codebase-architecture` 來觸發它 —— agent 不會自己去找它。

當作週期性的健康檢查來用:每隔幾天,或每當一個 codebase 開始讓人覺得,要搞懂一個概念得在一堆小 module 之間跳來跳去太累的時候。它會讀既有的架構,提出該在哪裡加深。如果你已經知道要重新設計哪個 module,只需要一套詞彙來想清楚,改用 [codebase-design](https://aihero.dev/skills-codebase-design) —— 這個 skill 是找出候選項的那份調查;那個才是設計工作台。

## 加深的機會

整個 skill 繞著一個概念轉:**深度**。一個深 module 把大量功能藏在一個小而穩定的介面背後;一個淺 module 則會透過一個幾乎跟底下程式碼一樣寬的介面,把實作洩漏出來。這份報告在找的是淺薄:純函式只是為了可測試性被抽出來,真正的 bug 卻藏在它們被呼叫的方式裡(沒有**locality**)、module 從自己的**接縫**洩漏出去、要打開五個檔案才能懂的概念 —— 並提出能修正這些問題的加深方式。

它講的是共用的設計詞彙(**module**、**interface**、**depth**、**seam**、**adapter**、**leverage**、**locality**),也講你專案自己從 `CONTEXT.md` 來的 domain 語言,所以一個候選項讀起來會是「把 Order intake module 加深」,而不會是「重構 FooBarHandler」。

## 先報告,再 grill

輸出是一份寫進你作業系統暫存目錄、瀏覽器可以直接開的 HTML 檔 —— repo 裡不會多出任何東西。每個候選項都是一張卡片,列出涉及的檔案、摩擦點、白話的解法、以 locality 與 leverage 表示的好處、一張前後對照圖,以及一個 `Strong` / `Worth exploring` / `Speculative` 的標籤。最後會標出它認為最該優先處理的那一個。

接著它會停下來,問你想深入研究哪一個。選一個之後,它會針對那個設計跑一輪 [grilling](https://aihero.dev/skills-grilling) 迴圈 —— 限制條件、接縫背後藏了什麼、哪些測試能留下來 —— 隨著決策結晶,就地更新 domain model。

## Where it fits

`improve-codebase-architecture` 是**週期性維護** —— 每隔幾天跑一次,不是鏈裡的一個步驟。它的鄰居是 [codebase-design](https://aihero.dev/skills-codebase-design)(每個候選項所用的深度與接縫詞彙都由它擁有)、[grilling](https://aihero.dev/skills-grilling)(你選好候選項後,由它走過決策樹),以及 [domain-modeling](https://aihero.dev/skills-domain-modeling)(在重新設計定案的過程中,讓 `CONTEXT.md` 與 ADR 保持最新)。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
