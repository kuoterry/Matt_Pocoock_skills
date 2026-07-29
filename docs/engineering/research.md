Quickstart:

```bash
npx skills add mattpocock/skills --skill=research
```

```bash
npx skills update research
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/research)

## What it does

`research` 透過閱讀擁有答案的來源來回答一個問題,並留下一份附引用的 Markdown 檔。它只從**第一手來源**下手——官方文件、原始碼、規格、第一方 API——絕不用別人對它們的二手整理,所以它存下來的東西可以追溯回一個權威來源,而不是「摘要的摘要」。

## When to reach for it

打 `/research`,或者當一個任務變成需要大量閱讀的苦工時,agent 會自動找上它。

當下一步是*去查一件事*——一個 API 實際行為怎樣、一份規格到底寫了什麼、一個說法站不站得住腳——而你不想讓這件事卡住自己手上這條線時就用它。想用訪談的方式而不是閱讀來磨利一個計畫,用 [grilling](https://aihero.dev/skills-grilling);想用用完即丟的程式碼探索要蓋什麼,用 [prototype](https://aihero.dev/skills-prototype)。

## 委派出去的苦工

它的核心動作是:閱讀這件事以**背景 agent** 的方式執行。你繼續手上的工作;它自己跑去把每個說法追溯回第一手來源,再把一份附引用的 Markdown 檔丟進 repo 存放這類筆記的地方。research 是你委派出去的苦工,不是外包出去的思考——你拿回來的是一份可以回應的文件,附上它的來源。

## Where it fits

一個隨時可以拿來用的獨立工具,餵給那些負責思考的 skill:它產出的檔案是拿去 grill、規劃,或做設計依據用的東西,所以它排在 [grilling](https://aihero.dev/skills-grilling) 與 [to-prd](https://aihero.dev/skills-to-prd) 這類工作的上游,而不是身處建置鏈裡面。完整地圖見 [ask-matt](https://aihero.dev/skills-ask-matt)。
