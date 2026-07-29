Quickstart:

```bash
npx skills add mattpocock/skills --skill=handoff
```

```bash
npx skills update handoff
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/productivity/handoff)

## What it does

`handoff` 把目前的對話壓縮成一份**交接文件**——一份單一的說明,讓一個全新的 agent 讀了就能從你留下的地方接手。

它**不會**重述已經活在別的地方的東西。任何已經記錄在 spec、計畫、ADR、issue、commit,或 diff 裡的內容,都用路徑或網址引用,絕不複製。這份文件只承載活著的那條討論串——你在做什麼、為什麼,以及接下來要做什麼——而且它存進你作業系統的暫存目錄,不是存進工作區,所以它絕不會變成另一個要維護的產物。

## When to reach for it

你打 `/handoff` 來觸發它——agent 不會自己去找它。附上一句關於下一個 session 要做什麼的說明,這份文件就會依此量身打造。

當一場對話已經長到 context 有風險——你快到 context 上限了、今天要收工了,或是刻意要把工作交給另一個 agent——而你想保留這條討論串、又不想把整份逐字稿一起拖過去時就用它。

## 文件裡有什麼

- **活著的討論串**——正在進行中的東西,以及為什麼,用這場對話自己的話寫,不包含任何已經記錄在別處的東西。
- **建議的 skill**——指向下一個 agent 該用哪些 skill 來繼續。
- **引用,而不是複製**——連到那些擁有定案細節的 spec、計畫、ADR、issue、diff 的連結與路徑。
- **已清除的機密資訊**——API 金鑰、密碼、個資,在文件寫出來之前就先清掉。

要記住的核心概念是**壓縮(compaction)**:一份交接文件,就是把整場對話擠壓到只剩下可以接續的核心,讓一個全新的 agent 繼承的是動能,不是雜訊。

## Where it fits

`handoff` 是一個隨時可以拿來用的獨立工具——它站在兩場 session 之間的接縫上,而不是身處在某條建置鏈裡面。它自然會跟那些會產出東西、被它拿來引用的 skill 搭配:[to-spec](https://aihero.dev/skills-to-spec),因為一份寫完的 spec,正是交接文件會拿去引用、而不是重述一遍的那種定案細節。不確定當下該用哪個 skill 時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
