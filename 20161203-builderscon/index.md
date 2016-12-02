# CSS設計を破綻させない

builderscon tokyo 2016 [@kubosho_](https://twitter.com/kubosho_)

-----
## 自己紹介

- kubosho_
- フロントエンドデベロッパー
- [Goodpatch](http://goodpatch.com/jp)所属
- [https://github.com/kubosho](https://github.com/kubosho/)
- [https://twitter.com/kubosho_](https://twitter.com/kubosho_)
- [http://blog.kubosho.com](http://blog.kubosho.com/)

-----
## 話すこと

- CSS設計はなぜ破綻するのか？
- CSS設計が破綻していないかツールを使って検知する

-----
## CSS設計、破綻させたことありますか？

---

ここで挙手を求める

-----
<!--code-->
## CSS設計はなぜか破綻する

定義の重複が複数ある

```css
.button {
  border: 1px solid #ccc;
}

/* ...長いコードの後や別ファイルなど... */

.button {
  border: 1px solid #666;
}
```

-----
<!--code-->
## CSS設計はなぜか破綻する

前に書いたセレクタの詳細度が高い

```css
 /* 詳細度は a=0, b=4, c=0 なので、0.4.0となる */
.container .form .form-group .form-submit-button {}

/*
  詳細度は a=0, b=1, c=0 なので、0.1.0となる
  上書きできない！
*/
.form__submit-button {}
```

-----
## CSS設計が破綻したという定義

- 詳細度が管理されていない
- スタイルの定義場所が明確でない
- 命名規則が決まっていない

-----
## CSS設計はなぜ破綻するのか？

- CSS設計についての方針がない
- デザイナーと意識合わせをしていない

-----
## CSS設計についての方針がない

-----

![ヘッダー内のドロップダウン](img/navbar.png)

---

Bootstrapでヘッダーらしきものを作るとこんな見た目になります。

-----

<iframe height='536' scrolling='no' title='Bootstrap overwrite sample' src='//codepen.io/kubosho_/embed/RoxOgB/?height=536&theme-id=0&default-tab=html&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='http://codepen.io/kubosho_/pen/RoxOgB/'>Bootstrap overwrite sample</a> by Shota Kubota (<a href='http://codepen.io/kubosho_'>@kubosho_</a>) on <a href='http://codepen.io'>CodePen</a>.
</iframe>

-----
😊ドロップダウンを開いたときの影をなくそう<br>
😊ドロップダウンの項目の下に線をつけよう

-----
## 修正前

![ドロップダウンを開いたとき](img/dropdown-open.png)

-----
## 修正後
![ドロップダウンを開いたとき](img/dropdown-improvement-1.png)

-----
<!--code-->
```css
.dropdown-menu {
  padding: 0;
  box-shadow: none;
}

.dropdown-menu li {
  border-bottom: 1px solid #ccc;
}

.dropdown-menu li:last-child {
  border-bottom: 0;
}
```

-----
😉ドロップダウンの項目の背景色をヘッダーと同じにしたいなー<br>
😉ドロップダウンの上の線消したいなー<br>
😉ドロップダウンの下の丸みも消したいなー

-----
![ドロップダウンを開いたとき: 改善版](img/dropdown-improvement-2.png)

-----
<!--code-->
```css
.dropdown-menu {
  padding: 0;
  border-top: 0;
  border-radius: 0;
  box-shadow: none;
  background-color: #f8f8f8;
}

.dropdown-menu li {
  border-bottom: 1px solid #e7e7e7;
}

.dropdown-menu li:last-child {
  border-bottom: 0;
}
```

-----
😣Dropdown2というラベルが付いたところの横幅が足りていないのが気になる…<br>
😣Bootstrapの見た目から脱却したい…

-----
## そして破綻へ…

-----
## なにが問題か？

- ドロップダウンの見た目を改造するために値の上書きを多くしていた
- Bootstrapが提供する見た目から脱却しようとした

-----
## 「CSS設計についての方針がない」を解決するためには

- CSS設計の方針を定める
- CSSフレームワークを使う場合は改造を最小限にする

-----
## CSS設計はデザイナーと意識合わせをしよう

-----
## CSS設計が破綻していないかツールを使って検知しよう

-----
## 意図していないデザインの変更が頻繁におこなわれる

-----

- CSSフレームワークを使うのならそのレールから外れない
    - 上書きが多く発生すると破綻する

-----
## デザインの意図を正しく理解するとは？

たとえばタイトルと内容を区切る線

-----
![はてなブログの個別記事](img/blog-single.png)

-----
## CSS設計

- 「CSS設計」は何から何までを指すのか？
    - HTMLのマークアップも含まれる
    - HTMLの要素で意味を持たせることにより、セレクタの名前も意味のある名前にできる
- OOCSS, MindBEMding, SMACSS, Suit CSS, FLOCSS, ECSS...
  - いろいろある
  - 望むのは詳細度の低さ、プロパティと値をできるだけ定義しないこと

-----

## セレクタ設計の破綻を検知する

- css-stats
- stylestats
- CSS Specificity Graph Generator

-----

HTMLはBEMツリーで説明するだけに止めて、CSSコンポーネントはSassのplaceholderで秘匿するのがいい気がしてる。HTMLからは何もCSS設計してないように見えるけど、Sassでやってる、的な。placeholderでなくコピペしたらECSSっぽくなる。

CSSルールセットは未来を予測できないから、クラス名にスタイルの仕事を任せると.c-だの.p-だの.u-だの揉める。仮に
衝突しないように組めたとしても似て非なるデザインが出た時に差分をどこに吸収させるかで揉める。結果ヘルパークラスW杯になると思う。

JSでコンポーネント開発がうまくいくのはJSは見た目と切り離されているからで、CSSはコンポーネント化しても親や前後の要素によって見た目を変えざるをえない。CSSコンポーネントを構造依存から切り離すにはスタイル宣言の少ないルールセット＋ヘルパークラスW杯しかないんだろうか？

共通化して使いまわせる閾値が案件ごとにあって、コンポーネント（っぽいもの）の数とかページ数とかそもそものデザインとかいろいろあるから、つまりCSSとは人生をかけた戦いなのである

似たようなデザインにおいて同じルールセットを使いまわすという手法が、たとえそれでうまくいったシーンがあったとしても、根本的には幻想なのではないか、と思っている

とりあえずCSS設計はフロントだけでやるものじゃないのは間違いないけど、CSSがデザインを制約してはいけないとも思う。

-----
## まとめ

- CSS設計の方針を定めよう
- CSS設計はデザイナーと意識合わせをしよう
- CSS設計が破綻していないかツールを使って検知しよう

---

## 想定Q&A

- テストはどうするのか？たとえばプロパティを無くしたり上書きしたときはレイアウトが崩れていないことをどうやって見るのか？
- すでに破綻しているCSS（プロジェクトに途中から入ってそこのCSSが破綻している）はどうやって改善していけるのか？

-----

## 参考資料

- [9. セレクタの詳細度計算 - セレクタ Level 3](http://standards.mitsue.co.jp/resources/w3c/TR/css3-selectors/#specificity)
- [僕はCSSを見殺しにした - dskd](http://dskd.jp/archives/54.html)
- [morishitterのCSSの書き方（2016年夏） - morishitter blog](http://morishitter.hatenablog.com/entry/2016/07/29/204642)
- [昔ながらの「片手間に書くJavaScript」の限界 \- mizchi's blog](http://mizchi.hatenablog.com/entry/2014/06/30/123535)
