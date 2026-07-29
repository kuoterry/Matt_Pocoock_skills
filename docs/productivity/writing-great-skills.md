Quickstart:

```bash
npx skills add mattpocock/skills --skill=writing-great-skills
```

```bash
npx skills update writing-great-skills
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/productivity/writing-great-skills)

## What it does

`writing-great-skills` 是你寫 skill、改 skill 時要對照的參考資料——讓一個 skill 表現得可預期,所需的共用詞彙與原則。

一個 skill 的工作是從一個隨機的系統裡逼出決定性(determinism),所以目標不是每次跑出同樣的*輸出*,而是每次都是同樣的*流程*。**可預期性(Predictability)**是最根本的美德,每個設計選擇都是拿它來評判——不是看這個 skill 讀起來多聰明、多完整,或多詳盡。

## When to reach for it

你打 `/writing-great-skills` 來觸發它——agent 不會自己去找它。

當你在寫一個新 skill,或改一個既有的 skill,想讓它每次的行為都一樣時就用它:決定觸發方式、寫 description、決定什麼該放進 `SKILL.md`、什麼該放進連結的檔案,或是診斷一個 skill 為什麼觸發失準。

## 認知負擔

整份參考資料繞著一個概念轉:**認知負擔(cognitive load)**——以及它的對照組,**context 負擔(context load)**。每個 skill 都得花掉其中一種:

- 一個 **model-invoked** skill 每一輪都把 description 留在 context 視窗裡,所以它花的是 **context 負擔**,但它能自己觸發。
- 一個 **user-invoked** skill 把那份 description 拿掉;它不花任何 context 負擔,但現在*你*變成必須記得它存在的那個索引——那就是**認知負擔**。

這些 skill 大多是 user-invoked,這正是為什麼認知負擔是整套系統設計來管理的那個壓力:當 user-invoked skill 多到超過你腦子裝得下的量,解法是一個能叫出其他 skill 名字、告訴你何時該用哪個的**router skill**。一旦你開始用這兩種負擔來思考,多數撰寫上的決定——拆或不拆、寫在裡面還是外掛、model-invoked 還是 user-invoked——都變成同一個取捨在不同地方重複發生而已。

## 其他槓桿

參考資料剩下的部分,是把這兩種負擔花得值得的工具箱:

- **領頭字(Leading words)**——一個 model 預訓練裡已經有的精簡概念(_tight_、_red_、_tracer bullet_),agent 執行這個 skill 時會拿它來想。它用最少的 token 同時錨定執行方式*與*觸發方式;去找那些一個字就能取代掉的重述內容。
- **資訊層級(Information hierarchy)**——從 skill 內的步驟,到 skill 內的參考資料,到藏在一個**context 指標**背後的外部參考資料,這一整條階梯。**漸進式揭露(Progressive disclosure)**就是沿著這條階梯往下走的動作,讓最上層保持易讀。
- **修剪(Pruning)**——逐句套用唯一真相來源、相關性,以及「拿掉會不會沒差」測試,對抗**沉積(sediment)**與**蔓延(sprawl)**。
- **失敗模式**——**過早完工(premature completion)**、**重複(duplication)**、**沉積(sediment)**、**蔓延(sprawl)**、**沒差(no-op)**——用來診斷一個表現不對勁的 skill。

## Where it fits

這是一份隨時可以拿來查的獨立參考資料——你在建構其餘 skill 的過程中會諮詢的 meta-skill,不是某條鏈裡的一步。它自然的鄰居是你維護的任何一個 router,因為 router 正是 user-invoked skill 堆起來的認知負擔的直接解藥;不確定某個任務該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航整套系統。
