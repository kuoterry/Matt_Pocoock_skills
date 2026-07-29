Quickstart:

```bash
npx skills add mattpocock/skills --skill=codebase-design
```

```bash
npx skills update codebase-design
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/codebase-design)

## What it does

`codebase-design` 給你一套共用、精確的詞彙,用來設計**深 module**(deep module)—— 大量行為藏在一個小介面背後,擺在一個乾淨的接縫(seam)上,可以透過那個介面測試。

它是一套**語言,不是一套流程**。它不會重整你的程式碼結構,也不會給你一份重構計畫 —— 它固定的是用詞(module、interface、depth、seam、adapter、leverage、locality),讓每一場關於設計的對話、每一個碰到設計議題的其他 skill,都講同一種語言。詞彙一致就是重點所在;"component"、"service"、"API"、"boundary" 被刻意禁用,因為它們會模糊掉真正重要的區別。

## When to reach for it

打 `/codebase-design`,或者當任務吻合時 agent 會自動找上它。

當你在設計或改善一個 module 的介面、在找可以加深的機會、在決定接縫該放哪裡,或是想讓程式碼更容易測試、對 AI 更好導覽時,就用它。其他 skill 需要用到深 module 詞彙時,也都會拉它進來用。如果你想磨利的是專案的*domain*用語而不是 module 設計,改用 [domain-modeling](https://aihero.dev/skills-domain-modeling);如果要對既有 codebase 跑一整輪架構檢視,用 [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture)。

## 深,不是淺

一個 module 是**深**的,當大量行為藏在一個小介面背後;是**淺**的,當介面幾乎跟實作一樣複雜。深度是用**槓桿(leverage)**來衡量的 —— 呼叫者(或測試)每學會一單位的介面,能撬動多少行為。關鍵是,深度是*介面*的屬性,不是實作的屬性:一個深 module 內部可以是由一堆小、可替換的零件組成的,只是它們從來不會浮現到呼叫者面前。

有兩個檢查做了大部分的工作。**刪除測試**:想像把這個 module 刪掉 —— 如果複雜度就此消失,它只是個 pass-through;如果它在 N 個呼叫者身上重新冒出來,那它就是有在發揮價值。以及**一個 adapter 只是個假設性的接縫;兩個 adapter 才是真的**—— 沒有東西真的在那個接縫上變化之前,不要先切下去。

## 介面就是測試的表面

呼叫者跟測試穿過的是同一個接縫,所以一個擺對位置的介面能給測試一個穩固的瞄準點,同時底下的程式碼可以自由變動。這就是為什麼這套詞彙堅持用 **seam**(Feathers 提出的用語 —— 一個你不用編輯它就能改變行為的地方),而不是被用爛的 "boundary";也是為什麼這裡的 "interface" 指的是*呼叫者必須知道的每一件事*:當然包括函式簽章,但也包括不變量、順序、錯誤模式,以及效能 —— 不只是型別層級的表面。

## 刻意拆出來

`codebase-design` 是深 module 詞彙的**唯一真相來源**,被拆成獨立的 model-invoked skill,讓任何地方都能用到它。其他 skill 是指向它,而不是自己重講一遍用詞:[tdd](https://aihero.dev/skills-tdd) 借用它來在寫測試前先定位接縫,[improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) 在重整既有程式碼時靠它,[to-spec](https://aihero.dev/skills-to-spec) 在寫 spec 前草擬接縫與加深機會時也用它的語言。

保持它獨立存在的用意是,你也可以單獨拿它來用 —— 當作一份**參考資料**,思考該怎麼設計 module —— 而不會觸發上面那些 skill 各自要求的整套大流程。把用詞固定一次、放在一個地方,每一場設計對話都能繼承它。

## Where it fits

`codebase-design` 是**隨時可以拿來用的獨立工具** —— engineering skill 底下共用的詞彙層。它最近的鄰居是 [domain-modeling](https://aihero.dev/skills-domain-modeling),同樣是詞彙類 skill,但對象是問題領域而不是 module 結構。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
