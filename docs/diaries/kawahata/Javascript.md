20210202
# this(javascript)

## this

thisはそのときのオブジェクトを参照する

20210906
# JSに必須のオブジェクト
## window, document, object

20210917
# 宣言タイミングについて
グローバルに変数を使用したいときは、変数宣言を関数やループの外で行う必要がある。
```Javascript
//エラーが出る例
const startBtn = document.getElementById("start-btn");
const stopBtn = document.getElementById("stop-btn");

let a = function() {
    console.log("a");
}

startBtn.addEventListener("click", function() {
    let timer = setInterval(a, 1000);
});

startBtn.addEventListener("click", function() {
    clearInterval(timer); //ここでエラー
});

```
timer変数がある関数内でしか定義されていないので、外では使えない。正しくは以下。
```Javascript
//正しい例
const startBtn = document.getElementById("start-btn");
const stopBtn = document.getElementById("stop-btn");
let timer;

let a = function() {
    console.log("a");
}

startBtn.addEventListener("click", function() {
    timer = setInterval(a, 1000);
});

startBtn.addEventListener("click", function() {
    clearInterval(timer);
});

```