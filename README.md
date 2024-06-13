# Charm.js
このページの解説は配布サイトをベースにしています。  
より詳細な情報を入手するには配布サイトにアクセスしてください。  
https://lanama.net/scripts/charm/


## Outline

### Charm.jsとは
Charm.jsは、名前変換小説サイト向けに配布している名前変換スクリプト（JavaScript）です。  
JavaScriptがわからなくてもHTMLがわかれば少しのコードで導入することができます。  
名前変換小説、単語変換小説、夢小説などにどうぞ。

### Charm.jsの特徴
- JavaScriptファイルを読み込んで、変換したいところを特定のタグで囲むだけで使用可能
- 未登録時の名前をhtml側でページ毎に設定して使用
- 未登録時やJavaScript無効時は普通の小説として読める
- スクリプトがhtmlから独立しているので管理が容易
- Charm.js単独でプログラムが完結するので、様々な環境で導入可能
- jQueryなどのライブラリ、WordPressで人気のPHP、他のサーバーサイド言語を併用しても動く
- スクリプトファイルは軽め（19KBくらいのJavaScriptファイル1つだけ）
- モダンブラウザならスマホでも動く
- 登録データはLocalStorageまたはSessionStorage保存

### カスタムを含む名前変換例・機能
- JavaScriptを修正しなくても、入力タグを増やせば登録項目を追加可能
- ボタンを使わずに入力タグだけで自動保存ができるオプションあり※β版です
- 登録ボタンを使う場合は、通常登録と一時登録（ブラウザやタブを閉じると自動削除）を選べる
- カスタム変換はタグにdata属性またはclass属性を設定するだけで使用可能
- ブラウザ設定によりLocalStorageが使えなくても、登録フォームページでは変換可能
- JavaScriptを変更すれば、登録データの簡易暗号化も可能※β版、あくまで元の文字が多少推測されにくい程度の暗号化
- 【カスタム変換】カタカナ（ひらがなで登録した名前をカタカナで表示）
- 【カスタム変換】ひらがな（カタカナで登録した名前をひらがなで表示）
- 【カスタム変換】カタカナひらがなmix（カタカナとひらがなを混合表示）
- 【カスタム変換】省略　例：なまえ、という登録で「なーちゃん」など
- 【カスタム変換】先頭文字スキップ　例：なまえ、という登録で「まえ」
- 【カスタム変換】末尾カット　例：なまえ、という登録で「なま」
- 【カスタム変換】最後の文字　例：みょうじ、という登録で「じ」
- 【カスタム変換】詰まり　例：な、な、なまえ
- 【カスタム変換】区切り　例：な……ま……え　（区切り文字は変更可能　例：なーまーえ）
- 【カスタム変換】響き　例：……え……まえ
- 【カスタム変換】重複　例：ななままええ
- 【カスタム変換】逆順　例：えまな
- 【カスタム変換】母音のばし　例：みょうじいいい、みょうじぃ

### Charm.jsで出来ないこと・ご注意
- InternetExplorer等の一部の環境では動作しません
- タグ打ちとファイルアップロードが必要なので、これらに関する知識は必要です
- サーバにアップロードしないで動作確認をすると、一部の機能は動きません
- 50文字を超える単語の登録（変更は可能ですがJSの修正が必要です）
- 日本語以外の名前変換はカスタムに対応していません
- ディレクトリ区切りのレンタルサーバでは、スクリプト内のstatic storageKeyNameを固有の文字に変更する必要があります
（同じドメインで保存キーが被ると同じ登録データを見てしまうため）

## ご利用条件
  
ライセンス（利用条件等を書いたもの）を確認し、同意できる方のみご利用ください。  
日本語版も英語版も内容は同じです。お好きな方をご確認ください。  
[ライセンス](LICENSE.txt)
  

## Charm.jsを使った名前変換ページ作成の基本

### charm.jsをダウンロード
このリポジトリのarchivesフォルダから、任意のzipファイルを選択  
ダウンロードしたファイルを解凍し、charm.jsをサーバーにアップロード

### 名前登録ページでスクリプト本体を読み込み、指定のタグを入れる

ここでご紹介するのは自動登録・削除機能を使ってボタンレスで実装方法です。（β版）  
従来の登録、一時登録、削除ボタンありのパターンは[Charm.jsをサイトに導入するための詳細手順](Tutorial.md)をご確認ください。

```html
<!-- 名前入力 ※自動保存を使うので登録ボタンレス -->
名前<input type="text" id="charmname1" class="charm charmnow">

<!-- 登録内容表示 -->
<span class="charmname1">名前</span>
```
```html
<!-- スクリプト読み込み -->
<script src="charm.js"></script>
```
### 小説ページでスクリプト本体を読み込み、指定のタグを入れる

```html
<!-- 登録内容表示 -->
<span class="charmname1">名前</span>
```
```html
<!-- スクリプト読み込み -->
<script src="charm.js"></script>
```
これで導入完了です。
詳しい解説は[Charm.jsをサイトに導入するための詳細手順](Tutorial.md)をご覧ください。

文字区切りや母音表示などの特殊な変換は [Charm.jsのカスタム変換](Custom.md) をご覧ください。

利用規約の不明点は [利用条件・その他のQ&A](FandA.md) をご覧ください。


## Special Thanks
  
Charm.jsの開発・改修にあたり大変お世話になりました。ありがとうございました。  
[@takiagari](https://github.com/takiagari)さん - Charm.js v3系移行時の、カスタム変換の判定処理と実行処理の分離


