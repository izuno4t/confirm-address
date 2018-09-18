# Confirm Address

This add-on changes Thunderbird that shows the confirm-address dialog when you send a mail.
Once you register YOUR DOMAIN (ex."mycompany.com"), you will see Confirm-Address dialog with highlighted mail addresses when you send mail to other domain.
And so, you can raise awareness of security and information leak.
This is forked from https://github.com/Meatian/confirm-address and works with Thunderbird 60.

Add-on package is available on [AMO](https://addons.thunderbird.net/en-US/thunderbird/addon/confirm-address2/).

# リリースパッケージ作成方法

## antを使ってビルド
- build.propertiesを、リリースバージョンに合わせて書き換える
- install.rdfを、リリースバージョンに合わせて書き換える
- antを実行する
- release以下にリリースパッケージが生成される

## 手作業でビルド
- ソースをzipで固めてバージョンに合わせて名前を変更するだけです

# 開発方法

- githubのsource codeをcloneします
- TunderbirdのAdd-ons Managerの歯車アイコンのメニューでDebug Add-onsをクリックします
- Load Temporary Add-onボタンをクリックして、source codeの `install.rdf` ファイルを選択すると読み込まれます
- デバッグの方法は [about:debugging](https://developer.mozilla.org/docs/Tools/about:debugging#Add-ons) を参照

# デバッグ出力方法

- Profileフォルダにuser.jsというファイルを作り、以下の一行を追加します

```javascript
user_pref("browser.dom.window.dump.enabled",true);
```


- ソース中にdump("hoge");のように記述します
- 起動時オプション"-console"をつけてTBを起動します
- Macの場合は、以下のように起動します

```sh
$ /Applications/Thunderbird.app/Contents/MacOS/thunderbird-bin -console
```

- コンソールに"hoge"と表示されます

# 単体テストの実行/作成方法

## 実行方法
- `confirm-address/chrome/content/unittest/testRunner.html` をwebブラウザで開けば
 単体テストを実行できます。
- テスト成功なら、「N test success!!」というダイアログが表示されます
- 失敗なら、失敗理由を表すメッセージがダイアログ表示されます

## 作成方法
- たとえば/chrome/content/hello.js をテストしたいとします
- /chrome/content/unittest/hello-test.jsを作成します
- testRunner.htmlに、上記二つのjsを`<script>`を使ってインクルードします
- hello.jsには、メソッド名がtestから始まるテストメソッドを定義し、その中でhello.jsのメソッドなどを呼び出して、テストを記述します
- テストコード内では、assertEqualsメソッドが使えます
- テストコードでは、メソッド名がtestからはじまるグローバルなメソッドを定義します
