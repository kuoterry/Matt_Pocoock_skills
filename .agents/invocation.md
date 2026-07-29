# Model-invoked vs user-invoked

這個 repo 裡每份 `SKILL.md` 都是一個 skill。區分它們的唯一軸線是**觸發方式**(invocation)—— 誰能觸發到它:

- **User-invoked** —— **只有人類打出它的名字**才能觸發。frontmatter 設 `disable-model-invocation: true`(Claude Code)、`agents/openai.yaml` 設 `policy.allow_implicit_invocation: false`(Codex)。`description` 是**寫給人看的**:一句話摘要,給瀏覽 slash command 的人讀。要拿掉觸發清單的寫法(像「Use when the user says…」這種)。
- **Model-invoked** —— **model 或使用者都能**觸發。預設狀態:不寫 `disable-model-invocation`,`agents/openai.yaml` 也不用 `policy` 區塊。`description` 是**寫給 model 看的**,保留豐富的觸發語句(「Use when the user wants…, mentions…, asks for…」),讓自動觸發能夠成立。判斷一個 skill 該不該維持 model-invoked 的測試是:_model 能不能自主地有效用到它?_(可重用性是把某個東西抽成 skill 的理由,不是這個判斷的測試。)

每個 harness 都用自己的方式把 user-invoked skill 排除在 model 觸發範圍外,確保除了人類以外沒有東西能點燃它 —— 也沒有其他 skill 能點燃它。一個 user-invoked skill 可以呼叫 model-invoked skill,但絕不能呼叫另一個 user-invoked skill。

每個 skill 旁邊也都會有一份 `agents/openai.yaml`。裡面裝的是 Codex UI 用的 metadata —— skill picker 用的 `interface.display_name` 與 `interface.short_description`,以及(針對 user-invoked skill)跟 `disable-model-invocation` 配對的 `policy.allow_implicit_invocation: false`。這兩者要保持同步:一個 skill 要嘛在兩個 harness 裡都是 user-invoked,要嘛都不是。

bucket `README.md` 與頂層 `README.md` 都會把條目分成 **User-invoked** 與 **Model-invoked** 兩組。

## 彼此之間的依賴關係

依賴關係一律用**`/skill` 風格的 prose 呼叫**表達(例如「Run the `/grilling` skill」),不用深入的 `../other-skill/FILE.md` 跨檔連結。共用的參考文件放在擁有它的那個 skill 裡面,其他 skill 要用到那份素材時,是去呼叫那個 skill,不是跨資料夾連過去。

## 被動 vs 主動的 domain 工作

單純為了查詞彙而**讀** `CONTEXT.md`,只是一句 prose 指標,不算是 `domain-modeling`。只有主動的建立/磨利紀律(挑戰用語、做邊界案例情境、寫 ADR、就地更新 `CONTEXT.md`)才算是 `domain-modeling`。
