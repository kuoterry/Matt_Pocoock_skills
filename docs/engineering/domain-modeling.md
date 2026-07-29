Quickstart:

```bash
npx skills add mattpocock/skills --skill=domain-modeling
```

```bash
npx skills update domain-modeling
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/domain-modeling)

## What it does

`domain-modeling` 在你設計的同時,建立並磨利一個專案的 **ubiquitous language**(通用語言)—— 挑戰模糊的用語、用具體情境對關係做壓力測試,並在概念一結晶就立刻寫下詞彙表與決策。

這是**主動**的紀律,不是被動的。單純讀 `CONTEXT.md` 借用它的詞彙,是任何 skill 都能做的一句話習慣;這個 skill 是給你在*改動*這個模型的時候用的 —— 造一個標準用語、抓出程式碼跟你剛講的話之間的矛盾、記下一個難以回頭的決定。它也讓詞彙表保持乾淨:`CONTEXT.md` 就只是一份詞彙表,不多不少 —— 沒有實作細節,沒有 spec,不是草稿紙。

## When to reach for it

打 `/domain-modeling`,或者當任務吻合時 agent 會自動找上它 —— 當你在確定用語、解決一個被過度使用的字,或記錄一個架構決策時。

當問題出在*用詞*本身時就用它:兩個人講「cancellation」意思不一樣、"account" 這個字身兼三職、或是一場設計對話一直卡在一個從沒被精確命名過的概念上。如果問題出在 module 的*形狀*上 —— 接縫該放哪、介面該有多深 —— 用 [codebase-design](https://aihero.dev/skills-codebase-design)。如果你想在動手蓋之前先讓整個計畫本身被盤問一遍,用 [grilling](https://aihero.dev/skills-grilling)。

## Prerequisites

這個 skill 會寫進兩個地方,都是懶惰式建立的 —— 只有真的有東西要記錄時才會建立。確定下來的用語會寫進根目錄的 `CONTEXT.md`(或者,在被 `CONTEXT-MAP.md` 標記為多 context 的 repo 裡,寫進各自 context 的 `CONTEXT.md`)。決策會寫進 `docs/adr/`。事前什麼都不用先準備好;第一個確定下來的用語會建立詞彙表,第一個真正的取捨會建立 ADR。

## Glossary vs. ADR

兩種產物,兩種不同的門檻:

- **詞彙表**(`CONTEXT.md`)捕捉的是語言。每次一個模糊的用語被確定為標準用語,就立刻就地寫下來 —— 不是累積到最後才批次寫 —— 讓共用詞彙跟對話同步更新。它要徹底不含任何實作細節。
- **一份 ADR** 捕捉的是一個決策,而且門檻很高:只有在這個選擇**難以回頭**、**沒有背景脈絡會讓人意外**,而且**是真正取捨後的結果**時才會寫。三項少一項就不寫 ADR。這正是讓 `docs/adr/` 保持是「重大分岔的紀錄」,而不是一本日記的原因。

真正讓它發揮效果的動作是:當你陳述某件事怎麼運作時,這個 skill 會去跟程式碼做交叉比對,把矛盾點端出來 —— 「你的程式碼是整張 Order 一次取消,但你剛剛說可以部分取消 —— 哪個才對?」語言跟程式碼會被強迫達成一致。

## 刻意拆出來

`domain-modeling` 是建立專案 ubiquitous language 的**唯一真相來源**,被拆成獨立的 model-invoked skill,讓任何其他 skill 都能用到它。[grill-with-docs](https://aihero.dev/skills-grill-with-docs) 靠它在 grilling session 進行時記錄用語與決策,[triage](https://aihero.dev/skills-triage) 用它讓 ticket 維持用專案自己的話寫,[improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) 在運作時也會用到它。

保持它獨立存在,代表你也可以直接拿它來用 —— 當作**參考資料**,思考怎麼磨利一個模型 —— 不用被綁進上面那些 skill 各自要求的步驟裡。這套語言就住在一個地方,任何需要它的東西都指向那裡。

## Where it fits

`domain-modeling` 是**隨時可以拿來用的獨立工具**,它跑在其他 skill*底下*的頻率,跟它作為固定一步被使用的頻率一樣高。它最近的鄰居是 [codebase-design](https://aihero.dev/skills-codebase-design),因為有共用語言,你才能精確地為一個深 module 跟它的接縫命名;往下游看,一份底定的詞彙表正是 [to-spec](https://aihero.dev/skills-to-spec) 整理成 spec 時,拿來用專案自己的話寫的原料。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
