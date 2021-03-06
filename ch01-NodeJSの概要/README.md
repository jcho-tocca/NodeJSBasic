# 01. NodeJSの概要
## 1. Node.jsの紹介
### Node.js
* 2009年 Ryan Dahl
* JavaScript
* Chrome v8
### Node.jsの特徴
* シングルスレッド
* I/O が非同期
* イベント基盤(event driven)
### 非同期 I/O
* 時間がかかる I/O
  * ハードディスク
  * DB
  * ネットワーク
* I/O 動作か終わるまで待機する：同期式
* I/O 動作か終わるまで待機しない：非同期式
### 非同期 I/O のメリット
* Apache vs Nginx
### Node.jsのメリット
* シングルスレッド
* I/O が非同期
* 簡単な構造の軽量フレームワークと豊富なライブラリ
* サーバーとクライアントで使用する言語が同様
### Node.js 推奨分野
* ソーシャルネットワーク
* データ中心のサービス
* IoT 機器連動
### アーキテクチャ
* 上位レベル - JavaScript
* 下位レベル - C
  * Node bindings
  * v8
  * libev:Event
  * libeio:I/O
## 2. プログラミングモデル
### 同期式
#### ファイル読み込み
```js
let fs = require('fs');
let content = fs.readFileSync("readme.txt", "utf8"); // Syncというキーワードがあると同期式
console.log(content);
console.log('Reading file...');
```
### 非同期式
#### ファイル読み込み
```js
let fs = require('fs');
fs.readFile("readme.txt", "utf8", function(err, content) { // コールバック関数があると非同期式
  console.log(content);
});
console.log('Reading file...');
```

### 同期/非同期式のコードの違い
#### 同期式
```js
function add(i, j) {
  return i + j; // リターンする
}

let result = add(1, 2);
console.log(‘Result : ‘, result);
```
#### 非同期式
```js
// コールバック関数を使用する
function add(i, j, callback) {
  let result = i + j;
  callback(result);
}

add(1, 2, function(result) {
  console.log(‘Result : ‘, result);
});
```
### 非同期のAPIの例
#### コールバックを利用したファイル読み込み
```js
fs.readFile('textfile.txt', 'utf8', function(err, text) {
  console.log('Read File Async', text);
});
```
### 殆どのコールバック関数のエラー処理
```js
// 殆どのコールバック関数の第一引数はerrorが入っている
callbackFunc(arg1, arg2, function(error, result) {
  if (error) {
    // エラー処理
    return;
  }
  // 正常処理
}
```
## 3. Node.js 開発環境
### Node.jsコマンド
node [SOURCE.JS] [ARGS]
* v : バージョン
* e、p : ストリップト評価
* c : 実行せず文法チェック
* r : モジュールを前もってロード

### 4. Hello World
```sh
node helloWorld.js
node helloWorld2.js
```
#### ブラウザで確認
127.0.0.1:3000
## 5. ドキュメント
### モジュール
* Node.jsのライブラリ
### ドキュメント
https://nodejs.org/ja/docs/

* [API リファレンス](https://nodejs.org/api/)
* [ES6 の機能](https://nodejs.org/ja/docs/es6/)
* [ガイド](https://nodejs.org/ja/docs/guides/)

### API リファレンス
#### Stability(API 安定度)
* 0 : Deprecated
* 1 : Experimental
* 2 : Stable
* 3 : Locked
#### モジュール
* クラス：Interface
* メソッド
* イベント
* モジュール関数
#### モジュール読み込み
* rerequire（「モジュール名」）
* 絶対パスあるいは相対パス 
```js
var readline = require（'readline'）;
```
#### モジュール種類
* 標準モジュール : インストール不要
* 拡張モジュール : npmでインストール必要

#### モジュール場所
* 標準モジュール : Node.jsのライブラリディレクトリ
* 拡張モジュール : node_modulesフォルダ
#### クラス：Interface
##### モジュール読み込みとオブジェクト生成が基本
```js
var readline = require('readline');
var rl = readline.createInterface();
```
#####  オブジェクト生成関数のオプション
```js
var rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});
```
#### メソッド
##### モジュール読み込みとオブジェクト生成後、使用
```js
var readline = require('readline');
var rl = readline.createInterface();
rl.setPrompt(‘>>’);
```
#### イベント
##### オブジェクト.on([イベント名], [イベントリスナー])
```js
rl.on('line', function (cmd) {
  console.log('You just typed: '+ cmd);
});
```
#### モジュール関数
##### オブジェクト生成なしで直接モジュールを使用
```js
var readline = require('readline');
readline.cursorTo(process.stdout, 60, 30);
```





