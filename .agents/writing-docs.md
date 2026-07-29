# 撰寫 docs 頁面

`engineering/` 與 `productivity/` 裡的每個 skill,都有一份面向人類讀者的 **docs 頁**,放在 `docs/<bucket>/<skill-name>.md` —— docs 目錄樹鏡射 `skills/` 底下這兩個 bucket 資料夾。它發佈在 `https://aihero.dev/skills-<skill-name>`;網址一律是 `skills-<skill-name>`,跟 bucket 無關,所以 docs 路徑只是 repo 內部組織方式。這個頁面不是 skill 本身,也不是 `SKILL.md` 的副本。只有這兩個 bucket 有上架;其餘的(`misc/`、`personal/`、`in-progress/`、`deprecated/`)不出 docs 頁。

多數這些 skill 都是 **user-invoked**:agent 不會替你觸發它,所以*你*才是那個必須記得它們存在、何時該用的索引。這份記憶就是**認知負擔**。docs 頁的工作就是減輕它 —— 讓一個讀者能繞著一個 skill 定向,把它裝進腦子裡,知道何時該用它,也看清它在整個系統裡的位置。這些頁面合起來是一個分散式的 router;每一頁都是一個節點。

每當一個上架的 skill 被新增、改名,或行為有變動時就要動手:建立或重新同步它的 docs 頁。改名時檔案也要跟著搬(`docs/<bucket>/<舊名>.md` → `docs/<bucket>/<新名>.md`),因為發佈網址是跟著名稱走的;一個 skill 在 `engineering/` 與 `productivity/` 之間搬家時,它的 docs 檔也要搬到對應的資料夾。`misc/`、`personal/`、`in-progress/`、`deprecated/` 裡的 skill 沒有頁面 —— 這些 bucket 都沒有上架。一個 skill 從這些 bucket*搬出*到 `engineering/` 或 `productivity/` 時會拿到頁面;反過來搬就會失去頁面。

因為這些頁面是發佈在 `aihero.dev` 上,**每個連結都要是絕對路徑** —— 絕不用 repo 相對路徑。連到另一個 skill 的連結要指向 `https://aihero.dev/skills-<name>`;連進 repo 的連結要用完整的 `https://github.com/mattpocock/skills/...` 網址。在 repo 裡能用的相對連結,發佈出去就會壞掉。

不寫 H1 —— 發佈出去的頁面標題是從 slug 取的。

## 頁面結構

依下面的模板填。**固定框架**(Quickstart 區塊、來源連結、`## What it does`、`## When to reach for it`、`## Where it fits`)每一頁都要有。**可調整的中段** —— `## Prerequisites` 與自由發揮的內容段落 —— 只放這個 skill 自己該有的東西;其餘刪掉。

<page-template>

Quickstart:

```bash
npx skills add mattpocock/skills --skill=<name>
```

```bash
npx skills update <name>
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/<bucket>/<name>)

## What it does

一到兩段白話文字。先講 skill 的一句話工作內容,再講**定義性限制**(defining constraint)—— 那個讓這個 skill 表現得跟顯而易見的預設做法不一樣的單一事實(以 `to-spec` 來說:它不會再訪談使用者一次,而是把已知的內容整理出來)。用一句平舖直敘的陳述句寫 —— 不要用「The defining constraint:」這種掛標籤式的寫法;這種公式讀起來像贅字。這行是整頁最有價值的一行 —— 絕不省略。

## When to reach for it

如何、何時要用到這個 skill,兩個重點,幾乎每個 skill 都會有:

- **觸發方式(Invocation mode)。** 說明是你自己打出來,還是 agent 觸發。user-invoked skill:「你打 `/<name>` 來觸發它 —— agent 不會自己去找它。」model-invoked skill:「打 `/<name>`,或者當任務吻合時 agent 會自動找上它。」
- **觸發邊界(Trigger boundary)。** 索引條目式的句子:「當……時就用這個。」如果這個 skill 容易跟旁邊的親戚搞混,補上另一半:「至於 <X>,改用 [<sibling>](https://aihero.dev/skills-<sibling>)。」

## Prerequisites

選用 —— 只有當這個 skill 需要某個東西先就位才能運作時才寫;否則整個標題都拿掉。涵蓋:一個**它會寫入的工作區**(像 `grill-with-docs` 這種有狀態的 skill 會寫 `CONTEXT.md` 與 ADR;`teach` 會蓋出整個資料夾 —— 說清楚它寫什麼、寫在哪),**事前設定**(`triage`/`to-spec`/`to-tickets` 需要 `setup-matt-pocock-skills` 先設定好 issue tracker),或是**repo 專屬的工具**。一個無狀態、到哪都能跑的 skill 沒有前置條件 —— 拿掉這節。

## <自由發揮的中段>

一到三個簡短段落,用這個 skill *自己的詞彙*,讓它一看就懂 —— 選最適合這個 skill 的標題:它跑的迴圈、它產出的產物、它做的分岔、它殺掉的那一個反模式。沒有規定的標題 —— 這些 skill 太不一樣了,沒辦法用同一套。

唯一不能妥協的一件事:**把 skill 的領頭字/定義性概念端出來** —— `tight` feedback loop、`deep module`、用完即丟的程式碼回答一個問題、red-green。這麼做有雙重效果:讀者學到這個 skill *是什麼*,也學到之後要拿來*想到、找到*它的那個字。

## It's working if

選用。一份簡短、可核對的清單,列出能告訴讀者「這個 skill 確實在做它該做的事」的可觀察訊號 —— 它觸發時你該看到什麼,以及反過來,沒觸發時的樣子。當一個 skill 有明確的訊號時就寫(例如 `to-spec` 不會再訪談你一次就直接寫;trace 裡再次出現的領頭字);訊號模糊時就把這個標題整個拿掉。幾個 bullet 就好,不用多。

## Where it fits

一定要有。用一兩句話把這個 skill 放進整個系統裡定位:

- **角色。** 幫它命名:是**流程裡的一個環節**(`grill-with-docs → to-spec → to-tickets → implement → code-review`)、**只跑一次的初始設定**(`setup-matt-pocock-skills`)、**週期性維護**(`improve-codebase-architecture`,「每隔幾天」),還是**隨時可以拿來用的獨立工具**(`diagnosing-bugs`、`prototype`、`handoff`)。獨立工具的定位就一句老實話 —— 比整節不寫好太多。
- **鄰居。** 一兩個真正重要的手足 skill,各自附上原因子句,用絕對連結連過去。
- **地圖。** 指向 [ask-matt](https://aihero.dev/skills-ask-matt),整套系統的 router,讓這一頁繼續當一個節點,不用自己重畫整張圖。

</page-template>

## 慣例

- 解釋**為什麼**,不是流程。這頁的工作是幫這個 skill 定向、定位,絕不重述 `SKILL.md` 裡的步驟或模板內容 —— 一個在挑工具的人不需要操作手冊。
- 用這個 skill 的**領頭字**(_seam_、_deep module_、_tracer bullet_),讓頁面跟 skill 講同一種語言。
- 讓頁面本身保持低負擔。它是在寫*低認知負擔*的 skill 的文件;多餘的裝飾(多出來的標題、重複貼的連結)正是它在反對的那件事。

## Done when

- 頁面存在於 `docs/<bucket>/<name>.md`,改名或搬 bucket 之後不留下舊頁面。
- Quickstart 區塊與來源連結寫的 bucket 跟 skill 名稱正確;update 那行寫對 skill 名稱。
- `## What it does` 用平舖直敘的散文陳述出定義性限制,不是掛標籤的寫法。
- `## When to reach for it` 講清楚觸發方式與觸發邊界。
- `## Where it fits` 講清楚角色,並連到 `ask-matt`。
- 有前置條件的地方(工作區、事前設定、工具)要寫出來,沒有的地方就不寫這節。
- 中段有把領頭字端出來。
- 每個連結都是絕對路徑,且每一個都能連得到。
