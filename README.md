# pandoc-ruby-filter

この[Pandoc](https://pandoc.org/)用フィルターは、文章中のルビ表記を処理して、LaTeXやHTMLなどの出力形式に合わせて変換します。このフィルターを制作するにあたり、[minoki](https://github.com/minoki)さんの[pandoc-aozora-ruby](https://github.com/minoki/pandoc-aozora-ruby)を参照しています。ただし、pandoc-aozora-rubyでサポートされていた省略記法（漢字から始まる文字列に対して｜を省略できる）には対応していません。

## 入力形式

フィルターは、次の形式のルビ表記を認識します。

｜単語《よみがな》

## 出力形式

フィルターは、出力形式に応じて次のようにルビ表記を変換します。

- LaTeXの場合：`\ruby{単語}{よみがな}`
- HTMLの場合：`<ruby>単語<rp>《</rp><rt>よみがな</rt><rp>》</rp></ruby>`
- 上記以外の場合：入力形式と同じまま維持されます。

## 使い方

1. Pandocがインストールされていることを確認してください（[Pandocのインストール方法](https://pandoc.org/installing.html)）。
2. 本リポジトリをダウンロードし、Luaスクリプト（`ruby_filter.lua`）をパスの通っている場所に移動するか、適当な場所に移動してパスを通します。
3. Pandocコマンドで、`--lua-filter`オプションを使用してフィルターを適用します。例：

```sh
pandoc input.md --lua-filter=ruby_filter.lua -o output.html
```

この例では、`input.md`というMarkdownファイルを入力として使用し、フィルターを適用して`output.html`というHTMLファイルを生成しています。

## 注意事項

このフィルターは、Pandocの`Str`要素（文字列）を処理します。そのため、ルビ表記が複数の`Str`要素にまたがっている場合、正しく処理されないことがあります。ルビ表記が正しく認識されるように、適切な場所で改行や空白を挿入してください。

## 備考

本リポジトリのコードおよびREADMEはChatGPT（モデル：GPT-4）との対話を通じて生成したものです。
