Quickstart:

```bash
npx skills add mattpocock/skills --skill=to-spec
```

```bash
npx skills update to-spec
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-spec)

## What it does

`to-spec` 把目前的對話跟你對 codebase 的理解,整理成一份 spec(你可能知道這種文件叫 PRD),再發佈到你的 issue tracker。

它**不會**再訪談你一次。等你用到它的時候,對齊的工作已經做完了——`to-spec` 是把已經知道的東西整理出來,而不是再問一輪新的問題。

## When to reach for it

你打 `/to-spec` 來觸發它——agent 不會自己去找它。

當一項變動已經談過、domain 用語也定案了,而你想在任何程式碼寫出來之前,把這份共同理解寫下來時就用它。如果你*還沒*對齊,先 grill——用 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)。要把寫好的 spec 拆成 ticket,用 [to-tickets](https://aihero.dev/skills-to-tickets)。

## Prerequisites

`to-spec` 會發佈進你的 issue tracker,所以 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) 必須已經先幫這個 repo 設定好 tracker 與 triage 標籤。它會自己套用 `ready-for-agent` 標籤——不需要另外跑一次 triage。

## Spec 包含什麼

- **問題陳述**——什麼壞了或缺了什麼,以及為什麼值得解決,用專案自己的詞彙寫。
- **解法**——修復方式的高層形狀,還沒進到任何實作細節。
- **User story**——一份詳盡、編號過的清單,列出這次變動必須支援的具體行為,每一條都能獨立核對。
- **實作決策**——對話中已經定案的選擇,讓它們之後不會被重新翻案。
- **測試決策**——這個功能會在哪些接縫上被測試,以及「完成」長什麼樣子。
- **範圍外項目**——這次變動刻意*不*涵蓋的東西,讓這張 ticket 保持有界限。
- **其他備註**——任何其他值得往下傳、但不屬於上面任何一節的東西。

## 深 module

在寫 spec 之前,`to-spec` 會先草擬這個功能會被測試的**接縫**,並找尋**深 module** 的機會——大量功能藏在一個小而穩定的介面背後。它偏好用既有的接縫而不是新開一個,而且盡量選最高層的接縫,理想狀況是整個變動只用一個接縫。

這對 agent 驅動的開發很重要:一個好介面能給測試一個穩固的瞄準點,讓底下的程式碼可以變動,測試不用跟著動。

## It's working if

- 它直接動手寫 spec,而不是再問你一輪新問題。
- 它會在寫之前跟你核對接縫,並盡量提出最少數量的接縫。
- 寫出來的 spec 用的是你專案的 domain 詞彙,不是通用的樣板文字。

## Where it fits

`to-spec` 是主要建置鏈裡的一步:

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

在計畫與 domain 用語都定案之後、把工作拆成實作 ticket 之前用它。它的重要鄰居是 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)(它把 context 磨利,讓 spec 寫得精準),以及 [to-tickets](https://aihero.dev/skills-to-tickets)(把 spec 變成一組給 [implement](https://aihero.dev/skills-implement) 建構的 ticket)。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
