# 文献情報の更新

文献情報は `_data/publications.json` で管理します。HTMLへの転記は不要です。

- `index.html`: 全論文とデモ論文を表示します。
- `jp.html`: ICML・NeurIPS・AAAI・IJCAI・ACL・EMNLPの論文を「主要業績」として表示します（Findings・Short paperを含み、Demoは除きます）。
- `_includes/`: 共通の表示テンプレートです。

## 論文を追加する

`_data/publications.json` の配列に次の形式で追加します。全論文一覧はファイルに記載した順序で表示されます。

```json
{
  "id": "unique-paper-id",
  "title": "Paper title",
  "authors": "First Author, Akifumi Wachi",
  "venue": "Conference name, 2026.",
  "links": [{ "label": "arXiv", "url": "https://arxiv.org/abs/..." }],
  "type": "paper",
  "conference": "ICML"
}
```

デモ論文は `type` を `demo` にします。リンクがなければ `links` を空配列にできます。
`note` はリンク欄の注記、`award` は受賞情報です。会議名と同じ行に受賞情報を表示する場合は `award_inline` を `true` にします。

## 日本語の主要業績への掲載

`conference` に会議の略称（`ICML`、`NeurIPS`、`AAAI`、`IJCAI`、`ACL`、`EMNLP`）を指定すると、日本語ページにも自動で掲載されます。
会議名の部分一致ではなく、このフィールドの完全一致で抽出します。たとえば `ACML` や `CoNLL` は含まれません。
対象会議のリストは `jp.html` の `major_conferences` で管理します。

通常論文はファイルに記載した順序で表示します。Demoは英語ページだけで、末尾に分けて表示します。
Findings・Short paperなどの区分は `venue` に記載した表記をそのまま表示します。
ジャーナル論文など会議に該当しない文献は `conference` を省略できます。

## プレビューと公開

この2ページはJekyllで生成します。GitHub PagesではブランチからのJekyllビルド、またはJekyllを実行するActionsが必要です。
HTMLを直接開いたり、ソースを `python3 -m http.server` で配信するだけでは、共通データは展開されません。

RubyとBundlerが利用可能な環境で、次を実行します（macOS標準の古いRubyでは依存ライブラリのインストールに失敗することがあります）。

```sh
bundle install
bundle exec jekyll serve
```

表示されたローカルURLで確認します。`bundle exec jekyll build` の出力先は `_site/` です。
