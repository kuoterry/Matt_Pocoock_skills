Quickstart:

```bash
npx skills add mattpocock/skills --skill=teach
```

```bash
npx skills update teach
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/productivity/teach)

## What it does

`teach` 把目前的資料夾變成一個常駐的教學工作區,跨越多個 session 教你一個主題——設計出簡短、漂亮、互動式的課程,並緊扣著你*為什麼*想學這個。

它**不會**光靠 model 自己的記憶來教。model 自身的參數知識被當成不可信;在能開始教之前,它會先蒐集高可信度的資源,並讓每個論點都有引用來源做根據。而且它是有狀態的——這個工作區記得你已經學過什麼,所以每次 session 都從上次結束的地方接續,而不是每次都從零開始。

## When to reach for it

你打 `/teach` 來觸發它——agent 不會自己去找它。

當你想長期*學習*一個主題——一種語言、一個框架、瑜伽、理論物理——而且希望每次 session 的成果能累積起來、而不是學完就蒸發時就用它。它不是用來做一次性的解釋的;如果你只是當下需要把某件事講清楚,直接問就好。當學習本身是一個專案時,才用 `teach`。

## Prerequisites

`teach` 會就地蓋出一整個資料夾,所以要在一個你願意當成專屬工作區留下來的地方執行它。隨著時間,它會寫出:

- `MISSION.md`——你學這個的理由,是其他一切的根基。如果它是空的,`teach` 的第一項工作就是盤問你,直到它不再是空的。
- `RESOURCES.md`——它教學時所用、經過篩選的高可信度來源。
- `./lessons/*.html`——編號過、各自獨立完整的課程(教學的基本單位)。
- `./reference/*.html`——濃縮過的小抄、演算法、詞彙表,供你之後回頭查。
- `./learning-records/*.md`——你已經學過的東西,ADR 風格,用來判斷接下來該教什麼。
- `./assets/*`——可重複使用的元件(首先是一份共用的樣式表),讓所有課程看起來像同一門課。
- `NOTES.md`——你的教學偏好。

## Mission,以及最近發展區

每一堂課都掛在**mission(使命)**上。沒有它,知識就沒有東西可以附著,課程也會感覺很抽象——所以 mission 是 `teach` 第一件要釘死、並隨著你的成長持續更新的事。它會從 mission 跟你的學習紀錄,算出你的**最近發展區(zone of proximal development)**:下一堂課該挑戰你到*剛剛好*的程度,不多也不少。

## 儲存強度,不是流暢度

要拿來想的字是**儲存強度(storage strength)**——長期記憶保留——跟**流暢度(fluency)**相對,後者是那種當下感覺很熟練、實際上不是的即時回憶。`teach` 刻意透過「有益的困難」來建立前者:提取練習(retrieval practice)、間隔(spacing),以及交錯(interleaving)。知識先被教(困難在這裡是敵人),然後透過一個緊迴圈的回饋來反覆操練技能(困難在這裡是工具)。

## Where it fits

`teach` 是一個隨時可以拿來用的獨立工具——一個你一次 session 接一次 session 推進的長期學習專案,不是建置鏈裡的一步。它跟其他 productivity skill 不共用任何流程;它就只是擁有自己的工作區資料夾,住在那裡。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
