# 02. NodeJSの標準モジュール１
## 1. 標準モジュール
### 標準モジュール
* Node.jsと一緒にインストールされる
* 別途インストール不要
### ドキュメント
https://nodejs.org/api/
### 主要標準モジュール
#### プロセス環境
* os
* process
* cluster
#### ファイルとパス、URL
* fs
* path
* URL
* querystring
* stream
#### ネットワーク
* http
* https
* net
* dgram
* dns
## 2. グローバルオブジェクト
### global
* モジュール読み込みなしで使用可能
* gobal モジュール
```js
global.console.log();
```
* global 省略可能
```js
console.log();
```
### 主要グローバルオブジェクト
* process
* console
* Buffer (クラス)
* require
* __filename, __dirname
* module
* exports
* Timeout 関数
### process
#### アプリケーションプロセス実行情報
process.js
* env : アプリケーション実行環境
* version : Node.js 버전
* arch, platform : CPUとプラットフォーム情報
* argv : 実行命令パラメータ
```
node processAdd.js 3 5
```
#### イベント
* exit : アプリケーション終了イベント
* beforeExit : 終了前に発生するイベント
* uncaughtException : 例外処理されていない例外イベント
#### 関数
* exit : アプリケーション終了
* nextTick : イベントループ内の動作をすべて実行後、コールバック実行
## 3. タイマー
### タイマー関数
* setTimeout : 遅延動作
* setInterval : 反復動作

使い方などは省略します。

## 4. console
console_log.js
```js
console.info();
console.log();
console.warn();
console.error();

console.log('log', 'log message');
console.info('info', 'info message');
console.warn('warn', 'warn message');
console.error('error', 'error message');

let obj = {
    name : 'IU',
    job : 'Singer'
}
console.log('obj : ' + obj);
console.log('obj : ', obj);
```
### カスタム console
console_custom.js
### 実行時間計測
console_timer.js
## 5. util
### 主要機能
* 文字列フォーマット
util.js
* 継承
util_inherit.js
* is関数(deprecated)
## 6. イベント
### イベントモジュール
* EventEmitter
### API レファレンス（例：Readline モジュール）
#### Class : Interface
* rl.close()
* rl.pause()
#### Events
* Event: 'close'
* Event: 'line'
* Event: 'pause'
* Event: 'resume'
* Event: 'SIGCONT'
* Event: 'SIGINT'
### イベントリスナー登録
* emitter.addListener(event, listener)
* emitter.on(event, listener)
* emitter.once(event, listener)
#### 例
```js
process.on('exit', function() {
    console.log('occur exit event');
});
// 一回だけ登録
process.once('exit', function() {
    console.log('occur exit event');
});
```
### イベントリスナー削除
* emitter.removeListener(event, listener)
* emitter.removeAllListeners([event])
### 最大イベントリスナー数
* emitter.setMaxListeners(n)
* emitter.getMaxListeners()

### イベント発生
#### イベント発火(emit)
* emitter.emit(event[, arg1][, arg2][, …])
    * event:イベント名
    * arg: リスナー関数のパラメータ
    * emit 関数呼び出し結果
        * true(イベント処理)
        * false(イベント処理不可)
##### 例
```js
process.emit('exit');
process.emit('exit', 0); // リスナー関数のパラメータへ0を転送
```
### カスタムイベント
### EventEmitter オブジェクトにカスタムイベント
```js
var customEvent = new event.EventEmitter();
    customEvent.on('tick', function() {
    console.log('occur custom event');
});
customEvent.emit('tick');
```
### カスタムイベントの継承
#### util モジュールで継承
```js
var Person = function(){};

// 継承
var util = require('util');
var EventEmitter = require('events').EventEmitter;
util.inherits(Person, EventEmitter);

// オブジェクト
var p = new Person();
p.on('howAreYou', function() {
    console.log('Fine, Thank you and you?')
});

// イベント発火
p.emit('howAreYou');
```
### 全てのイベントリスナーのエラー処理
```js
emitter.on('event', function(error, result) {
    if (error) {
        // エラー処理
    }
    else {
        // 正常処理
    }
}
```
