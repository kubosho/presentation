## サークル申し込みをする

### サークルとは

- 「同じ趣味や活動を行う集団」
- 海外では通じないらしい
- サークルは一人でも良い(重要)

> サークルとは (サークルとは) [単語記事] - ニコニコ大百科 http://dic.nicovideo.jp/a/%E3%82%B5%E3%83%BC%E3%82%AF%E3%83%AB

### どこで申込書を買うか

- コミケ会場
- 通販(郵便振替 or Web)

通販では1,500円で、コミケ会場で買った場合は1,000円だった記憶があるので、記憶が正しければ会場で買ったほうが安い

### ジャンルの選択

- ジャンルは「240(同人ソフト)」
- 135(評論・情報)もそれっぽいけど、実は違う
- 230(デジタル・その他)も違う

## 同人誌を書く

### ネタの出し方

- 何かに例えて説明する
- Steins;Git は「シュタゲの世界観を使って Git を説明する」という目的だった
- 例えば「ラブライブ！で分かる同人誌の出し方」など…
- 自分の気になっていることや好きなものを書くのが良い
- そうじゃないと気力がもたない

### 進捗管理の方法

- GitHub の Issue と Milestone で管理
- Issue のラベルをこんな感じで作った
- Milestone は〆切を意識する目的で使った
  - Milestones - o2project/steins-git https://github.com/o2project/steins-git/milestones?state=closed

### 校正の方法

- まずは書いたら自分で三度くらい読む
- できれば違う日にちにやるのが良い
- 今回は Git が分からない人でも読めるようにしたので、実際に Git があまり分かってない人に見てもらった
- 自動校正ツールを使う
  - [RedPen](http://redpen.cc/) を使ったりする

## 執筆環境

### Asciidoctor とは

- AsciiDoc 形式で書かれた文章を HTML や DocBook 形式などに変換してくれる Ruby 製のツール
- 見た目の調整は XSLT でおこなう (HTML 側は別途 CSS が使える)
- ドキュメント化されていない箇所が多々見受けられて辛い

### なぜ Asciidoctor を選んだのか

- azuさんの JavaScript Promise の本が Asciidoctor で作られていたから
  - https://github.com/azu/promises-book
- 何か困ったところがあったら参考にできると思った(実際かなり参考になった)
- ドキュメント代わりの利用例があったから
- Re:VIEW 形式を理解して使うには時間がなかった

### CI (Travis CI) で自動的にテストする

- 現状は正しく HTML に変換できるかどうかだけテスト
  - https://github.com/o2project/steins-git/blob/master/.travis.yml#L22
- PDF も正しく変換できるかテストしたい
- 後述の RedPen を使って文章構成が正しいかもテストしたい

### RedPen を使って校正する

- http://redpen.cc/
- gihyo.jp にも連載がある http://gihyo.jp/lifestyle/serial/01/redpen
- 対応フォーマットはテキスト形式、Wiki 形式、Markdown 形式
  - master を使えば asciidoc 形式も使える

## 印刷について

### Asciidoctor での紙のサイズの設定方法

- 設定は PDF 用の XSLT ファイルでおこなう
- https://github.com/o2project/steins-git.styles/blob/8187848cc0e724a6489dab590ad7584d5ecc7cc0/fo-pdf.xsl#L246
- 紙のサイズ基準が ISO 216 基準なので JIS 基準と比べて少し小さくなってしまう
  - ここは印刷業者によしなに調整してもらった

### PDF の出力方法

- 現状は https://github.com/asciidoctor/asciidoctor-fopub を使う
- 将来的には https://github.com/asciidoctor/asciidoctor-pdf
- asciidoctor-pdf は現状 CJK 対応がされていない
  - Issue は上がっている https://github.com/asciidoctor/asciidoctor-pdf/issues/82
  - TODO にもある https://github.com/asciidoctor/asciidoctor-pdf/blob/master/WORKLOG.adoc

### ePub の出力方法

- https://github.com/asciidoctor/asciidoctor-epub3 を使う
- ヘッダー部分の著者情報をどうやって消すのか分からなかったりレイアウト調整が難しかったりして ePub は断念…

### 印刷業者の選定方法

- 日光企画
- TechBooster も使っていると「はじめての ReVIEW」に書いてあった
- 使ってみたら、入稿時にこちらのミスを丁寧に教えていただいたり、ブースまで挨拶してきてくれたり神対応だった

## 宣伝の方法

### ランディングページの作成

- http://sg.o2p.jp/
  - 使ったのはこのテンプレート Tokusetsu 2 - 同人音楽CD特設サイトが一瞬で作れるTumblrテンプレート http://sanographix.github.io/tumblr/tokusetsu2/
- 他にもテンプレートはいろいろある
  - 同人音楽特設用テンプレートOzoneAsterisk WORKS http://works.o3asterisk.com/template/
- 特設サイトを凝ると SNS 上やブログなどで話題になるかも？
  - ひさかたの » 同人サイトとは思えないクオリティ！コミックマーケット84新刊特設サイトまとめ http://hisakatano.raindrop.jp/310
- Twitter
  - 邪魔にならないように宣伝
  - 一ヶ月前、二週間前、一週間前、三日前、二日前、前日、当日という感じで頻度を上げていった
  - 一週間前までは一日に一回ツイート、それ以降は一日に二回ツイート、前日は一日に三回ツイート、当日は宣伝というよりかは実況
  - ハッシュタグを事前に決めておく
- Facebook
  - 告知しておくと知り合いが来たりする
  - 同人活動を知り合いの間でも公にして良い場合はありかも

## 当日までにしておいたほうが良い準備

- サークルチケット
- ポスター
- 値札
- 釣り銭
- 机の上に敷く用の布
  - 無印良品だと店によっては少し高めの布しかなかったりする

### 東急ハンズで揃うもの

- ガムテープ
- カッター
- はさみ
- ボールペン
- 油性ペン(コピック)
- ビニール袋
- マスキングテープ
- ポスタースタンド

## 会場についたら何をするか

### 準備

- だいたい机の下にダンボールが置いてあるので、中から本を取り出して並べる
- 本は(多分乱丁対策で)数冊多めに入っている
- あとはポスターをスタンドに取り付けたり、机の上にあるチラシを見てみたりする

### 挨拶

- 近隣のサークルに挨拶する
  - 自分は両隣や後ろのサークルに挨拶した
- 一日を同じ場所で過ごす人達なので挨拶しておいたほうがお互いいい気分になれるかも？
  - 運が良ければ同人誌などがもらえたりする

## その他

### 版を更新するタイミング (自分の考える semver の応用)

- 本や章のタイトルを変更した場合はメジャーバージョンを上げる
- 章や何か機能を追加した場合はマイナーバージョンを上げる
- 校正した場合はパッチバージョンを上げる

## 参考資料

- コミックマーケット８８ サークル参加申込書セット通販のご案内 http://www.comiket.co.jp/info-c/C88/C88Appset.html
- Happy my life | コミケで技術系同人誌を売る方法 http://blog.cnu.jp/2015/01/12/c88-attending-comiket/
- ニッチでエッジな技術本をゲットしよう！ 　～IT技術者向けコミケ 初心者ガイド（2014年冬版） （1/3）：CodeZine http://codezine.jp/article/detail/8346
- ニッチでエッジな技術本をゲットしよう！ 第2弾　～IT技術者向けコミケ 気になるサークル編（2014年冬版） （1/4）：CodeZine http://codezine.jp/article/detail/8375
- ニッチでエッジな技術本をゲットしよう！ 第3弾　～IT技術者向けコミケ 実際に買ってきた編（2014年冬版） （1/8）：CodeZine http://codezine.jp/article/detail/8417
- ISO 216 - Wikipedia https://ja.wikipedia.org/wiki/ISO_216
