# Git Commit Convention

トピックブランチ以外のコミットメッセージは以下の規則に基づいて作成します。  

— **目次** —

- [Format](#format)
  - [type](#type)
  - [subject](#subject)
  - [body](#body)
  - [footer](#footer)
- [BREAKING CHANGE](#breaking-change)

## Format

フォーマットは次のとおりです。

```example
<type>[!]: <subject>

[body]

[footer]
```

`<type>`,`<subject>` は**必須**です。  
`[!]`,`[body]`,`[footer]` は**省略可能**です。  
`[body]`,`[footer]`の前に空行を挿入しなければなりません。  

### type

typeは**必須**です。  
次のいずれかを`lowercase`で記述します。  

| type     | 説明                                 |
| :------- | :----------------------------------- |
| build    | ビルドシステムや外部依存の変更       |
| ci       | CIの設定ファイルやスクリプトの変更   |
| docs     | ドキュメントのみの変更               |
| feat     | 機能の追加・変更・削除               |
| fix      | バグの修正                           |
| perf     | パフォーマンスの改善を目的とした変更 |
| refactor | 動作を変更しないコードの改善         |
| revert   | コミットの取り消し                   |
| test     | テストの追加・変更・削除             |
| chore    | 上記のいずれにも該当しないもの       |

```example
: some message     # bad
foo: some message  # bad
FIX: some message  # bad

fix: some message  # good
```

また破壊的変更の場合にはこれを強調するためにtypeの直後に`!`を記述しなければなりません。  

```example
feat!: some message
```

### subject

subjectは**必須**です。  
変更内容を記述します。  
記述の際には以下を遵守してください。  

- 命令形や現在形の動詞で始める（e.g. `changed`や`changes`ではなく`change`）
- 文頭は小文字にする
- 文末に`.`を記述しない

```example
feat:                # bad
feat: Some Message   # bad
feat: SOME MESSAGE   # bad
feat: some message.  # bad

feat: some message   # good
```

### body

bodyは**省略可能**です。  
bodyには変更の理由などsubjectの詳細情報を記述します。  
記述する場合には直前に1行空行を挿入しなければなりません。  

```example
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.
```

### footer

footerは**省略可能**です。  
footerには[BREAKING CHANGE](#breaking-change)やRevertするコミットのSHA、Issueへの参照などを記述します。  
記述する場合には直前に1行空行を挿入しなければなりません。  

参照を記述する場合には以下のようにします。  

```example
revert: let us never again speak of the noodle incident

Refs: 676104e, a215868
```

Issueをクローズする場合には以下のようにします。  

```example
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Closes: #123
```

複数のIssueをクローズする場合には次のように`Closes:`を繰り返し記述します。  

```example
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Closes: #123
Closes: #456
Closes: #789
```

## BREAKING CHANGE

破壊的変更の場合にはtypeの直後に`!`を記述しなければなりません。  

またfooterを`BREAKING CHANGE:`で始め破壊的変更に関する説明を記述できます。  
`BREAKING CHANGE:` はどのtypeのコミットにも含められます。  

```example
chore!: drop support for Node 6
```

```example
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```
