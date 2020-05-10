---
title: "JavaScript"
tags: ""
---
# 関数

-   function(関数)は関数宣言・関数式・コンストラクタという3種類の利用方法がある
-   関数名をそのまま利用することで呼び出し(実行)を行うことができる
-   引数を設定することで多彩なケースに対応できる関数を作成できる
-   戻り値(return文)を利用することで何らかの処理を行った結果を返すことができる
-   関数とメソッド内におけるthisはそれぞれ意味が異なる
-   関数が実行される時に自動生成されるargumentsオブジェクトには引数の値が格納されている
-   関数のブロック内で宣言、定義した変数は使用できる範囲に制限がある

## 宣言型

```js
function sample() {
 
    //ここに処理を書いていく
 
}
```

## 関数式（無名関数、匿名関数）

```js
var sample = function() {
 
    //ここに処理を書いていく
 
}
```

## アロー関数

　「function」キーワードを使わない代わりに、「=>」で関数を表現する

```js
var myFunc = function(name) {
  console.log(name);
}
```

↓

```js
var myFunc = (name) => {
  console.log(name);
}
```

```js
var myFunc = (name) => console.log(name);
```

## functionの引数にコールバック関数を設定する

  functionの引数に、別の関数を設定する<br>

  関数の処理が終了したあとに引数へ設定した関数を実行させることができる

```js
function testFunc(callback) {
 
    setTimeout(function() {
        console.log('testFuncが実行されました');
        callback();
    }, 2000)
 
}
```

## functionのthisとは

### 関数とメソッドでthisの意味が異なる

#### 関数内におけるthisの値

```js
function sample1() {
    console.log( this );  //①のthis
    
    function sample2() {
 
        console.log( this );  //②のthis
 
    }
    sample2();
}

 
sample1();

```

[実行結果]thisの中身がどちらもグローバルオブジェクト(windowオブジェクト)

```js
Window {stop: function, open: function, alert: function…}
Window {stop: function, open: function, alert: function…}
```

関数内のthisはデフォルト状態ではグローバルオブジェクトが格納されている

#### メソッド内におけるthisの値

```js
// この例では、objというオブジェクトを作成し、その中に「myObj」という関数（メソッド）を作成
var obj = {
    text: 'hello',
    obj: this,  //①のthis
 
    myObj: function() {
 
        return this;  //②のthis
 
    }
}
 
console.log( obj.obj );
console.log( obj.myObj() );
```

[実行結果] オブジェクト内ではfunction(関数)の中と外でthisの中身が変化する

```js
Window {stop: function, open: function, alert: function…}
Object {text: "hello", obj: Window, myObj...}
```

#### アロー関数におけるthisの値

アロー関数のthisは定義した時点のスコープを引き継ぐ

```js
// この例では、オブジェクトの外と中に「name」という変数を定義している
var name = '太郎さん';
 
var obj = {
  name: '田中さん',
 
  myFunc: function() {
    console.log(this.name);
  },
  
  myFunc2: () => console.log(this.name)
}
 
obj.myFunc();
obj.myFunc2();
```

実行結果

```js
田中さん
 
太郎さん
```

## function(関数)のスコープについて

-   スコープとは変数が利用できる範囲のことで、関数内で宣言した変数と関数外で宣言した変数では扱える範囲が異なる

```js
// 変数「num1」が関数外で宣言されており、変数「num2」が関数内で宣言されている
var num1 = 10;
 
function sample() {
  var num2 = 100;
  
  console.log(num1);
}
 
sample();
 
console.log(num2);

```

実行結果

```js
10
 
num2 is not defined
```

=>関数内で宣言された変数は関数内でしか利用できず、関数外で宣言された変数は関数内でも利用できる

## arguments

-   argumentsは、関数を実行する際に自動で生成されるオブジェクト
-   配列と同じように、添字と値で構成されている
-   argumentsを活用することで、関数の引数を制御できるうえ条件分岐を行うことも可能

```js
// この例では、「sample()」関数の中でargumentsオブジェクトをコンソールログに出力している
function sample( text ) {
    
    console.log( arguments );  // argumentsオブジェクトを出力
 
}
 
sample( 'リンゴ', 'バナナ', 'メロン' );
```

実行結果

```js
Arguments(3) ["リンゴ", "バナナ", "メロン",…...]
```

自動で生成されたargumentsオブジェクトには引数の値が格納されている

### argumentsを使った条件分岐

```js
function sample( text ) {
    
    if( !arguments.length ) {
        console.error( '引数を指定してください！' );
    }
    
}
 
sample();
```

実行結果

```js
引数を指定してください！
```
