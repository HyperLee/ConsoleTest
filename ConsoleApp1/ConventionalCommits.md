
# Conventional Commits 1.0.0（傳統提交訊息格式）

## 摘要

Conventional Commits（傳統提交）規範是在提交訊息上的一套輕量級約定。它提供了一組簡單的規則，用來建立明確的提交歷史，使得撰寫自動化工具變得更簡單。這個約定與 [SemVer（語意化版本）](http://semver.org/) 相輔相成，透過提交訊息來描述功能、修復與重大變更。

提交訊息應遵循以下格式：

```
<類型>[可選的範疇]: <描述>

[可選的主體內容]

[可選的附註區（footer）]
```

提交訊息包含以下結構元素，用以向你的函式庫使用者傳達意圖：

1. `fix:` 類型的提交會修復程式碼中的錯誤（對應語意化版本中的 [`PATCH`](http://semver.org/#summary)）。
2. `feat:` 類型的提交會為程式碼庫新增功能（對應語意化版本中的 [`MINOR`](http://semver.org/#summary)）。
3. `BREAKING CHANGE:` 在附註區中使用此字串，或是在類型/範疇後加上 `!`，代表引入了破壞性 API 變更（對應 [`MAJOR`](http://semver.org/#summary)）。
4. 除了 `fix:` 和 `feat:`，也可使用其他類型，例如 [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)（基於 [Angular 規範](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)）推薦的類型有：`build:`、`chore:`、`ci:`、`docs:`、`style:`、`refactor:`、`perf:`、`test:` 等。
5. 附註區除了 `BREAKING CHANGE: <描述>` 外，也可以遵循類似 [Git trailer 格式](https://git-scm.com/docs/git-interpret-trailers) 的其他格式。

其他類型不在規範中強制要求，對語意化版本也不會有隱含效果（除非包含 BREAKING CHANGE）。提交類型後可加上範疇（scope）以提供更多上下文資訊，例如：`feat(parser): add ability to parse arrays`。

## 範例

### 包含描述與 BREAKING CHANGE 附註的提交訊息

```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

### 使用 `!` 表示破壞性變更

```
feat!: send an email to the customer when a product is shipped
```

### 包含範疇並使用 `!` 的提交訊息

```
feat(api)!: send an email to the customer when a product is shipped
```

### 同時使用 `!` 與 BREAKING CHANGE 附註的提交訊息

```
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

### 沒有主體內容的提交訊息

```
docs: correct spelling of CHANGELOG
```

### 有範疇的提交訊息

```
feat(lang): add Polish language
```

### 含有多段主體內容與多個附註的提交訊息

```
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

Reviewed-by: Z
Refs: #123
```

## 規範條文

關鍵字如「MUST（必須）」、「SHALL NOT（不得）」等應依據 [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt) 的定義解釋。

1. 提交訊息 **必須** 以類型開頭，類型為名詞（如 `feat`、`fix` 等），後接可選的範疇、可選的 `!`，最後是必要的冒號與空格。
2. 若提交為新增功能，**必須** 使用 `feat`。
3. 若提交為修正錯誤，**必須** 使用 `fix`。
4. 類型後可加上範疇，**必須** 是描述程式碼區塊的名詞，並用括號包住，例如：`fix(parser):`。
5. 描述 **必須** 緊跟在類型與冒號空格之後，為此次程式碼變更的簡要摘要。
6. 描述後 **可以** 接續更長的主體內容，用來補充程式碼變更背景。主體內容 **必須** 在描述後隔一行空白行。
7. 主體內容格式自由，**可以** 是多段落，每段間以空行分隔。
8. 主體內容後 **可以** 再加上一行空白行，接續一個或多個附註區（footer）。每個 footer **必須** 由一個關鍵詞開頭，接冒號與空格或空格與 `#`，再接上文字值（參考 [Git trailer](https://git-scm.com/docs/git-interpret-trailers)）。
9. footer 的關鍵詞中的空白字元 **必須** 用 `-` 替代，如 `Acked-by`。但 `BREAKING CHANGE` 是例外，**可以** 使用空格。
10. footer 的值 **可以** 包含空格與換行，若遇到下一組有效的 footer 開頭，即視為結束。
11. 破壞性變更 **必須** 透過在類型/範疇中使用 `!` 或於 footer 中列出來表示。
12. 若寫在 footer，破壞性變更 **必須** 使用大寫 `BREAKING CHANGE:`，接著空格與描述文字。
13. 若寫在類型/範疇中，**必須** 在冒號前加上 `!`。這時 footer 可省略 `BREAKING CHANGE:`，其描述可直接寫在描述文字中。
14. 類型除了 `feat` 與 `fix` 外，也 **可以** 使用其他類型，如 `docs: update ref docs.`。
15. 對於實作者來說，Conventional Commit 的各個單元 **不應** 區分大小寫，但 `BREAKING CHANGE` 除外，**必須** 使用全大寫。
16. `BREAKING-CHANGE` 在 footer 中等同於 `BREAKING CHANGE`。
17. 描述（Description）部分請使用中文撰寫。
