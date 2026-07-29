Quickstart:

```bash
npx skills add mattpocock/skills --skill=grilling
```

```bash
npx skills update grilling
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)

## What it does

`grilling` 是在你動手蓋東西之前,對一個計畫或設計做壓力測試的無情訪談。它一個分支一個分支地走過決策樹,一次解決一個決策之間的依賴關係,直到你跟 agent 有了共同的理解。

它**一次問一個問題**,等你回答完才問下一個——絕不是一口氣列一整批,那樣只會讓人不知所措。每個問題都會附上 agent 自己建議的答案,任何 codebase 能解決的問題,它會自己去查,不會拿去問你。在你確認共同理解已經達成之前,它不會開始動手執行這個計畫。

## When to reach for it

打 `/grilling`,或者當任務吻合時 agent 會自動找上它——這是底層的原始元件,不是只給使用者用的進入點。

當一個計畫或設計還有軟肋、你想在寫程式碼之前先把它們揪出來時就用它。實務上你通常是透過它的兩個包裝 skill 來用它,而不是直接叫它的名字:單純的訪談 session 用 [grill-me](https://aihero.dev/skills-grill-me);想讓同一場 session 同時寫出 ADR 跟詞彙表,用 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)。

## 決策樹

它的心智模型是一棵**決策樹**:每個計畫都會分岔成一堆決策,決策之間又互相依賴。`grilling` 一次下探一個節點,所以一個早期的答案可能會改變接下來該問什麼問題。這就是為什麼問題是一個一個、依照依賴順序來的——一次丟出一堆平行問題,會讓訪談失去那個能收斂成共同理解的結構。

## 刻意拆出來

`grilling` 是這套訪談技巧的**唯一真相來源**,被拆成一個 model-invoked 的**原始元件**,讓任何需要訪談的 skill 都能用它,不用自己重新發明一套。[grill-me](https://aihero.dev/skills-grill-me) 與 [grill-with-docs](https://aihero.dev/skills-grill-with-docs) 是它兩個 user-invoked 的前門,但 [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) 與 [triage](https://aihero.dev/skills-triage) 也靠它來對自己的決策做壓力測試。

把這套技巧統一放在一個地方,代表你也可以在只想要訪談本身、不需要它的包裝 skill 額外附加的寫 ADR 或整理 ticket 功能時,直接用它。

## Where it fits

`grilling` 是主要建置鏈底下的訪談**原始元件**:[grill-with-docs](https://aihero.dev/skills-grill-with-docs) 跑它來把 context 磨利,然後 [to-spec](https://aihero.dev/skills-to-spec) 才寫 spec。不確定該用哪個進入點時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
