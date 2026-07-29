<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 給真正工程師用的 Skills

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

這是我每天用來做真實工程工作的 agent skills —— 不是 vibe coding。

開發真正的應用程式很難。像 GSD、BMAD、Spec-Kit 這類做法想幫忙,方式是把整個流程接管過去。但這麼做的同時,也把你的掌控權拿走,讓過程中出現的 bug 變得很難處理。

這些 skill 的設計原則是:小、容易調整、可組合。它們適用任何 model。基礎是數十年的工程經驗。歡迎拿去改、拿去變成你自己的東西。玩得開心。

如果想追蹤這些 skill 的變動,以及我之後做的新 skill,可以加入另外約 60,000 個開發者的訂閱名單:

[訂閱電子報](https://www.aihero.dev/s/skills-newsletter)

## 安裝(30 秒搞定)

兩種進場方式,兩種哲學。**[Claude Code plugin](https://code.claude.com/docs/en/plugins)** 把整組 skill 當成一個受管理、唯讀的包裝安裝進去 —— 你訂閱它,而不是 fork 它。**[skills.sh](https://skills.sh/mattpocock/skills)** 則是把可編輯的 skill 檔案複製進你的專案,讓你自己動手改、變成自己的東西。兩者擇一 —— 兩個都裝的話,每個 skill 都會重複一份。

### 1. 取得 skill

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugins install mattpocock-skills
```

或者,在 session 裡面直接下:

```
/plugin install mattpocock-skills
```

它已經在 Claude Code 的官方 marketplace 上,不用先加任何東西,更新也會自動送達。

</details>

<details>
<summary><strong>Codex,以及其他 agent</strong></summary>

```bash
npx skills@latest add mattpocock/skills
```

挑你要的 skill,以及要裝到哪些 coding agent 上。**這個安裝器會讓你選要拿哪些 skill —— 記得把 `setup-matt-pocock-skills` 也選進去。**

原生 Codex plugin 已經在規劃中 —— 見 [`.agents/adr/0002-ship-as-a-claude-code-plugin.md`](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)。

</details>

<details>
<summary><strong>給喜歡動手玩的人</strong></summary>

用同一個安裝器,裝在任何 agent 上 —— 包含 Claude Code:

```bash
npx skills@latest add mattpocock/skills
```

它會把 skill 寫進你的 repo,變成你自己擁有、可以編輯的一般檔案。不會有東西在背後偷偷更新;想拉我最新的變動時,自己下 `npx skills update` 就好。

</details>

### 2. 執行 `/setup-matt-pocock-skills`

在你的 agent 裡,每個 repo 執行一次。它會:

- 問你要用哪個 issue tracker(GitHub、Linear,或本地檔案)
- 問你 triage 分類時要套用哪些標籤(`/triage` 會用到這些標籤)
- 問你要把產生的文件存在哪裡

### 3. 搞定 —— 可以開始用了。

## 為什麼會有這些 Skill

我做這些 skill,是為了修正我在 Claude Code、Codex,以及其他 coding agent 上常見的失敗模式。

### #1:Agent 做的不是我要的

> "No-one knows exactly what they want"(沒有人真正確切知道自己要什麼)
>
> David Thomas & Andrew Hunt, [The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**問題**:軟體開發裡最常見的失敗模式是認知落差。你以為工程師懂你要什麼。然後你看到他做出來的東西 —— 才發現對方根本沒理解你的意思。

在 AI 時代也是一樣。你跟 agent 之間有溝通落差。解法是一場 **grilling session** —— 讓 agent 針對你要做的東西,細細地問你問題。

**解法**是用:

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) —— 給非程式碼的用途
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) —— 跟 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 一樣,但多了一些額外功能(見下方)

這是我最受歡迎的兩個 skill。它們幫你在動手前先跟 agent 對齊,並深入思考你要做的變動。**每次**要做變動,都用它們。

### #2:Agent 太囉嗦

> With a ubiquitous language, conversations among developers and expressions of the code are all derived from the same domain model.(有了共通語言,開發者之間的對話與程式碼的表達方式,都源自同一個 domain model。)
>
> Eric Evans, [Domain-Driven-Design](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)

**問題**:專案初期,工程師跟他們要服務的對象(domain expert)講的常常是不同的語言。

我在跟 agent 合作時也感受到一樣的張力。agent 通常是被丟進一個專案,自己邊做邊搞懂術語。所以它們常常一句話能講完的事,用了 20 個字。

**解法**是有一套共用語言。這是一份文件,幫 agent 解讀專案裡用的術語。

<details>
<summary>
範例
</summary>

這是我 `course-video-manager` repo 裡的一個 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 範例。哪一種比較好讀?

- **之前**:"There's a problem when a lesson inside a section of a course is made 'real' (i.e. given a spot in the file system)"(某個 course 的 section 裡的 lesson 被『實體化』時 —— 也就是在檔案系統裡分配到位置時 —— 會有個問題)
- **之後**:"There's a problem with the materialization cascade"(materialization cascade 有個問題)

這種精簡,一次又一次的 session 下來都划算。

</details>

這已經內建在 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) 裡了。它是一場 grilling session,但同時幫你跟 AI 建立共用語言,並把難以解釋的決策寫進 ADR。

它有多強很難用講的說清楚。這可能是這個 repo 裡最酷的一招。試試看,你就知道。

> [!TIP]
> 共用語言除了減少囉嗦之外還有很多好處:
>
> - **變數、函式、檔案的命名會一致**,都用同一套共用語言
> - 因此 **codebase 對 agent 來說更容易導覽**
> - agent 也會**在思考上花更少 token**,因為它能用的語言更精簡

### #3:程式碼跑不動

> "Always take small, deliberate steps. The rate of feedback is your speed limit. Never take on a task that's too big."(永遠只走小而刻意的一步。回饋的速度就是你的速限。絕不要接下太大的任務。)
>
> David Thomas & Andrew Hunt, [The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**問題**:假設你跟 agent 對於要做什麼已經對齊了。那 agent 產出的東西**還是**很爛,怎麼辦?

該檢查你的回饋迴圈了。沒有關於程式碼實際運作情況的回饋,agent 就是在瞎飛。

**解法**:你需要的是那套老班底 —— 靜態型別、瀏覽器存取、自動化測試。

對自動化測試來說,紅-綠-重構(red-green-refactor)迴圈是關鍵。也就是 agent 先寫一個會失敗的測試,再讓它通過。這能給 agent 穩定的回饋水準,做出來的程式碼品質好非常多。

我做了一個 **[`/tdd`](./skills/engineering/tdd/SKILL.md) skill**,可以放進任何專案用。它鼓勵紅-綠-重構,並針對什麼是好測試、什麼是壞測試給了大量指引。

針對除錯,我還做了一個 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** skill,把最佳除錯實務包成一個簡單的迴圈。

### #4:我們做出了一坨爛泥(Ball Of Mud)

> "Invest in the design of the system _every day_."(每一天都要投資在系統的設計上。)
>
> Kent Beck, [Extreme Programming Explained](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)

> "The best modules are deep. They allow a lot of functionality to be accessed through a simple interface."(最好的 module 是深的。它們讓大量功能可以透過一個簡單的介面被存取。)
>
> John Ousterhout, [A Philosophy Of Software Design](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)

**問題**:多數用 agent 做出來的 app 都很複雜、很難改。因為 agent 能大幅加快寫程式的速度,它們也同時加速了軟體的熵增。codebase 變複雜的速度前所未見。

**解法**是一套對 AI 驅動開發來說很激進的新做法:在乎程式碼的設計。

這套原則貫穿這些 skill 的每一層:

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) 在建立 spec 前,會先針對你要動的是哪些 module 盤問你

而關鍵的是,[`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) 能幫你搶救一個已經變成一坨爛泥的 codebase。我建議每隔幾天就在你的 codebase 上跑一次。

### 總結

軟體工程的基本功,重要性比以往任何時候都高。這些 skill 是我盡力把這些基本功濃縮成可重複實踐做法的成果,希望能幫你做出職涯裡最好的 app。玩得開心。

## 參考

這些 skill 依「誰能觸發」這個軸分成兩種。**User-invoked** 的 skill 只有你自己打出來才能觸發(例如 `/grill-me`);它們的工作是做編排(orchestrate)。**Model-invoked** 的 skill 可以由你觸發,也可以在任務吻合時被 agent 自動找上;它們承載的是可重複使用的紀律。一個 user-invoked skill 可以呼叫 model-invoked skill,但絕不會呼叫另一個 user-invoked skill。

### Engineering

我每天寫程式時用的 skill。

**User-invoked**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)** —— 問你目前的情況該用哪個 skill 或流程。是這個 repo 裡 user-invoked skill 的 router。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)** —— 一場同時會建立你專案 domain model 的 grilling session,把術語磨利,並就地更新 `CONTEXT.md` 與 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)** —— 讓 issue 沿著一套 triage role 的狀態機往前推進。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)** —— 掃描 codebase,找出可以「加深」的機會,做成一份視覺化 HTML 報告,然後針對你選的那項繼續往下 grill。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)** —— 為這個 repo 設定 engineering skill 所需環境(issue tracker、triage 標籤、domain 文件的存放方式)。用其他 engineering skill 之前,每個 repo 先跑一次。
- **[to-spec](./skills/engineering/to-spec/SKILL.md)** —— 把目前的對話整理成一份 spec,發佈到 issue tracker。不會再訪談一次 —— 只是把你們已經討論過的內容整理出來。
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)** —— 把任何計畫、spec,或對話拆成一組 tracer-bullet ticket,每個 ticket 都宣告自己的 blocking 關係 —— 可以寫成本地檔案裡的文字,也可以寫成真實 tracker 上原生的 blocking 連結。
- **[implement](./skills/engineering/implement/SKILL.md)** —— 依照 spec 或一組 ticket 動手把工作做出來,在事先談好的接縫(seam)處驅動 `/tdd`,並在 commit 前用 `/code-review` 收尾。
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)** —— 把一大坨超過一次 agent session 能裝下的工作,規劃成 issue tracker 上一張共用的「調查 ticket」地圖 —— 一次解決一張,直到通往目的地的路都清楚為止。

**Model-invoked**

- **[prototype](./skills/engineering/prototype/SKILL.md)** —— 做一個用完即丟的 prototype,來回答一個設計上的問題 —— 針對狀態/邏輯問題做一個可執行的終端機 app,或是針對 UI 做出幾種截然不同、可以在同一個 route 切換的版本。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)** —— 針對難搞的 bug 與效能退化,提供一套有紀律的診斷迴圈:重現 → 最小化 → 假設 → 埋測 → 修復 → 回歸測試。
- **[research](./skills/engineering/research/SKILL.md)** —— 針對一個問題,依照高可信度的第一手資料做調查,把結果寫成一份附引用的 Markdown 檔存進 repo,以背景 agent 的方式執行。
- **[tdd](./skills/engineering/tdd/SKILL.md)** —— 用紅-綠-重構迴圈做 test-driven development。一次一個垂直切片(vertical slice)地建構功能或修 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)** —— 主動建立並磨利一個專案的 domain model —— 拿詞彙表去挑戰用語、用邊界案例做壓力測試,並就地更新 `CONTEXT.md` 與 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)** —— 設計「深」module 的共用紀律與詞彙:一個小介面背後藏著大量行為,擺在一個乾淨的接縫(seam)上,可以透過那個介面測試。
- **[code-review](./skills/engineering/code-review/SKILL.md)** —— 針對從某個固定點開始的 diff 做雙軸審查:**Standards**(是否符合 repo 的程式碼規範,加上 Fowler 的程式碼異味基準?)與 **Spec**(是否忠實實作了原始的 issue/PRD?),以平行 sub-agent 執行,避免兩者互相污染。
- **[resolving-merge-conflicts](./skills/engineering/resolving-merge-conflicts/SKILL.md)** —— 針對進行中的 git merge 或 rebase 衝突,一個 hunk 一個 hunk 處理,依照雙方各自的原始來源追溯意圖來解決,最後完成整個操作 —— 絕不 `--abort`。

### Productivity

一般工作流程工具,跟寫程式無關。

**User-invoked**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)** —— 針對一個計畫或設計被無情地訪談,直到決策樹上每一個分支都被解決為止。
- **[handoff](./skills/productivity/handoff/SKILL.md)** —— 把目前的對話壓縮成一份交接文件,讓另一個 agent 能接手繼續做。
- **[teach](./skills/productivity/teach/SKILL.md)** —— 用目前的資料夾當成一個有狀態的教學工作區,跨多個 session 教使用者一項新技能或概念。
- **[writing-great-skills](./skills/productivity/writing-great-skills/SKILL.md)** —— 寫好、改好 skill 的參考資料:讓一個 skill 行為可預期所需的詞彙與原則。

**Model-invoked**

- **[grilling](./skills/productivity/grilling/SKILL.md)** —— 針對一個計畫、決策,或想法無情地訪談使用者,直到決策樹上每一個分支都被解決為止。是 `grill-me` 與 `grill-with-docs` 背後可重複使用的核心迴圈。
