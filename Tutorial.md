# Charm.jsをサイトに導入するための詳細手順  

## charm.jsをダウンロード

### このリポジトリから、お好きなバージョンのcharm.jsをダウンロード
charm.2.X の「2」はバージョン2系という意味です。  
特にこだわりが無いのであればバージョンが新しい方が機能が多いので、新しいものを選んでください。  
zipでダウンロードします。

### ファイルを解凍し、中身を確認
フォルダの中には以下の2ファイルが入っています。
+ charm.js - 名前変換スクリプト圧縮版  
機能は圧縮してないものと全く同じです。ファイル読み込みがこちらの方が軽いのでこちらを使用してください。
+ charm.original.js - 圧縮してない方の名前変換スクリプト  
コードを確認した方向けのファイルです。基本的には導入に必要ありません。

### charm.jsをご自身のサイトにアップロード
夢小説の名前登録ページと小説ページから読み込むので、読み込める場所にアップロードしてください。

## 名前登録ページの設定
### charm.jsファイルを読み込む
```html
<script src="charm.js"></script>
```
特にこだわりがないのであれば、bodyの閉じタグ直前に書いておくがおすすめです。  
スクリプトの保存場所が名前登録ページと違うフォルダの場合はsrcの内容を変更してください。

### 名前登録フォームを設定
+ 入力欄のinputタグ全てにclass「charm」を設定します。
+ 入力欄のinputタグそれぞれに個別のidを設定します。
+ idは各inputが互いに被らないように好きな文字を設定してください。
+ idの文字は小説ページで何度も書くので、わかりやすく長過ぎない文字がおすすめです。

設定例1　漢字に対してふりがなを入力していく並び順
```html
苗字 <input type="text" id="charmname1" class="charm">
みょうじ <input type="text" id="charmname2" class="charm">
名前 <input type="text" id="charmname3" class="charm">
なまえ <input type="text" id="charmname4" class="charm">
```
設定例2　苗字・名前のペアの並び順
```html
苗字 <input type="text" id="charmname1" class="charm">
名前 <input type="text" id="charmname2" class="charm">
みょうじ <input type="text" id="charmname3" class="charm">
なまえ <input type="text" id="charmname4" class="charm">
```
設定例3　項目が少ないサイト向け
```html
名前 <input type="text" id="charmname1" class="charm">
なまえ <input type="text" id="charmname2" class="charm">
```
設定例4　項目が多いサイト向け
```html
名前1 <input type="text" id="charmname1" class="charm">
なまえ1 <input type="text" id="charmname2" class="charm">
名前2 <input type="text" id="charmname3" class="charm">
なまえ2 <input type="text" id="charmname4" class="charm">
名前3 <input type="text" id="charmname5" class="charm">
なまえ3 <input type="text" id="charmname6" class="charm">
名前4 <input type="text" id="charmname7" class="charm">
なまえ4 <input type="text" id="charmname8" class="charm">
```
特にidは連番にしなくてもいいので、あとあと使いやすい名称を設定してください。

### 登録ボタンと削除ボタンを設定

+ 登録ボタンはidが「charmset」のbuttonタグを用意します。
+ 一時登録ボタンはidが「charmsession」のbuttonタグを用意します。
+ 削除ボタンはidが「charmunset」のbuttonタグを用意します。
  
```html
<button type="button" id="charmset">登録</button>
<button type="button" id="charmsession">一時登録</button>
<button type="button" id="charmunset">削除</button>
```
タグ内の「登録」「一時登録」「削除」は「OK」「Del」などの違う言葉に変更しても構いません。  
登録ボタンを使わない、または一時登録ボタンは使わずに導入することも可能です。不要でしたら消してください。

登録ボタンで登録した名前はlocalStorageへ、一時登録ではsessionStorageへ保存します。  
Cookieのように保存内容がサーバへ送信されることはありません。

### 登録内容の表示を設定

+ 登録名を表示したいところに、classを設定したspanタグを追加します。
+ spanタグのclassは、登録inputタグのidと同じものを設定します。
+ inputタグのidが「charmname1」なら、表示するspanタグのclassを「charmname1」にします。

```html
<span class="フォームのid">デフォルト名</span>
```

フォーム例1の場合
```html
<span class="charmname1">苗字</span>
<span class="charmname2">みょうじ</span>
<span class="charmname3">名前</span>
<span class="charmname4">なまえ</span>
```

フォーム例2の場合
```html
<span class="charmname1">苗字</span>
<span class="charmname2">名前</span>
<span class="charmname3">みょうじ</span>
<span class="charmname4">なまえ</span>
```

フォーム例3の場合
```html
<span class="charmname1">名前</span>
<span class="charmname2">なまえ</span>
```

フォーム例4の場合
```html
<span class="charmname1">名前1</span>
<span class="charmname2">なまえ1</span>
<span class="charmname3">名前2</span>
<span class="charmname4">なまえ2</span>
<span class="charmname5">名前3</span>
<span class="charmname6">なまえ3</span>
<span class="charmname7">名前4</span>
<span class="charmname8">なまえ4</span>
```
#### 一時登録の案内
一時登録ボタンを導入している場合、一時登録したときにだけ現れるメッセ―ジを以下のコードで追加できます。  
一時保存をしたときにこのコードがあると、（一時保存しました）という文字が表示されます。  
必要であれば使ってください。
```html
<div id="charmsessionmsg"></div>
```

## 小説ページの設定
### charm.jsファイルを読み込む
```html
<script src="charm.js"></script>
```
特にこだわりがないのであれば、bodyの閉じタグ直前に書いておくがおすすめです。  
スクリプトの保存場所が小説ページと違うフォルダの場合はsrcの内容を変更してください。

### 登録内容の表示を設定

名前変換ページと同じように、登録名を表示したいところにclassを設定したspanタグを追加します。  
spanタグのclassは、登録inputタグのidと同じものを設定します。
```html
<span class="フォームのid">デフォルト名</span>
```

フォーム例1の場合
```html
<span class="charmname1">苗字</span>
<span class="charmname2">みょうじ</span>
<span class="charmname3">名前</span>
<span class="charmname4">なまえ</span>
```
フォーム例2～3も名前登録ページの表示と同じspanタグです。  

名前変換ページと同じく、spanタグの中身は未登録のときに表示される文字です。  
未登録時の文字は他のページに影響しないので、全ページで変更しても問題ありません。

基本的な導入設定は以上です。設定お疲れさまでした。

Charm.jsは様々なカスタム機能があります。もしご興味があれば[Charm.jsのカスタム変換](Custom.md)から使い方をご確認ください。
