Quickstart:

```bash
npx skills add mattpocock/skills --skill=grill-me
```

```bash
npx skills update grill-me
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me)

## What it does

`grill-me` 針對一個計畫或設計跑一場無情的訪談,走過決策樹上的每一個分支,直到你跟 agent 達成**共同的理解**。

它**一次問一個問題**然後等待。它絕不會一口氣丟一批問題給你——那樣只會讓人不知所措——而且只要一個問題能靠讀 codebase 回答,它就會自己去讀,不會拿去問你。每個問題都附上 agent 自己建議的答案,所以你是在回應一個提案,不是盯著一片空白發呆。

## When to reach for it

你打 `/grill-me` 來觸發它——agent 不會自己去找它。

在動手蓋之前,當一個計畫感覺大致對了,但你能感覺到裡面藏著還沒解決的決策時就用它——這正是你想把那些軟肋找出來、逼它們浮上檯面的時刻。如果你想讓同一場盤問同時留下 ADR 跟詞彙表這種紙本紀錄,改用 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)。而如果這件事大到一次 session 裝不下、通往目標的路線還很模糊——一個全新的專案、一個巨大的功能建置——從更上游的 [wayfinder](https://aihero.dev/skills-wayfinder) 開始,它會先把這件事畫成一張決策地圖,再併回這條流程。

## 決策樹

這場 session 把計畫走成一棵決策樹,一個一個解決它們之間的依賴關係——父決策先定案,才輪到掛在它底下的選擇。重點不是快速達成共識;而是讓每一個隱含的判斷都變得明講,不留下任何被默默假設的重要事項。走完之後,你手上會有一個每個分支都被走過一遍的計畫。

`grill-me` 是**無狀態的**:它什麼都不寫,也不留下任何工作區。它可以在任何地方跑,唯一的產物就是這場對話本身裡被磨利過的理解。這正是它跟 [grill-with-docs](https://aihero.dev/skills-grill-with-docs) 刻意形成的對比——後者跑同一場訪談,但額外把結果記成長久保存的 ADR 跟詞彙表。

## Where it fits

`grill-me` 是一個隨時可以拿來用的獨立工具——每當一個計畫需要被鍛鍊得更扎實時,你就跑一次的建置前壓力測試。它是 [grilling](https://aihero.dev/skills-grilling) 這個原始元件的無狀態、user-invoked 前門;它最近的鄰居是 [grill-with-docs](https://aihero.dev/skills-grill-with-docs),那個手足跑同一場訪談,但額外把決策記成 ADR 與詞彙表。如果結果是一份你想寫下來的 spec,交接給 [to-spec](https://aihero.dev/skills-to-spec),它會把定案的理解整理成一份 spec,不用再訪談你一次。不確定該用哪個流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
