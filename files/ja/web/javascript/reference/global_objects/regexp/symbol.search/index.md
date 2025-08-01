---
title: RegExp.prototype[Symbol.search]()
slug: Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.search
l10n:
  sourceCommit: 6fbdb78c1362fae31fbd545f4b2d9c51987a6bca
---

{{JSRef}}

**`[Symbol.search]()`** は {{jsxref("RegExp")}} インスタンスのメソッドで、 [`String.prototype.search`](/ja/docs/Web/JavaScript/Reference/Global_Objects/String/search) がどのように動作するのかを指定します。

{{InteractiveExample("JavaScript デモ: RegExp.prototype[Symbol.search]()")}}

```js interactive-example
class RegExp1 extends RegExp {
  constructor(str) {
    super(str);
    this.pattern = str;
  }
  [Symbol.search](str) {
    return str.indexOf(this.pattern);
  }
}

console.log("table football".search(new RegExp1("foo")));
// Expected output: 6
```

## 構文

```js-nolint
regexp[Symbol.search](str)
```

### 引数

- `str`
  - : 検索対象の文字列 ({{jsxref("String")}}) です。

### 返値

正規表現で指定された文字列が最初に一致したインデックスの値、または一致する文字列が見つからなかった場合は `-1` を返します。

## 解説

このメソッドは、 {{jsxref("String.prototype.search()")}} の内部で呼び出されます。たとえば、次の 2 つの例は同じ結果を返します。

```js
"abc".search(/a/);

/a/[Symbol.search]("abc");
```

このメソッドは [`Symbol.split`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.split) や [`[Symbol.matchAll]()`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.matchAll) とは異なり、正規表現をコピーしません。しかし、[`[Symbol.match]()`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.match) や [`[Symbol.replace]()`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.replace) とは異なり、実行を始めるときには [`lastIndex`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/lastIndex) を 0 に設定し、終了するときには前回の値に戻すので、一般的に副作用を避けることができます。つまり、このメソッドでは `g` フラグは効果がなく、 `lastIndex` が 0 でない場合でも常に文字列の最初に一致した部分を返します。これは、粘着的正規表現が常に文字列の先頭を厳密に検索することも意味しています。

```js
const re = /[abc]/g;
re.lastIndex = 2;
console.log("abc".search(re)); // 0

const re2 = /[bc]/y;
re2.lastIndex = 1;
console.log("abc".search(re2)); // -1
console.log("abc".match(re2)); // [ 'b' ]
```

`[Symbol.search]()` は常に正規表現の [`exec()`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) を 1 回だけ呼び出し、結果の `index` プロパティを返すか、結果が `null` の場合は `-1` を返します。

このメソッドは、`RegExp` サブクラスで検索動作をカスタマイズするために存在しています。

## 例

### 直接呼出し

このメソッドは、`this` と引数順が異なることを除いて {{jsxref("String.prototype.search()")}} とほぼ同じ方法で使用できます。

```js
const re = /-/g;
const str = "2016-01-02";
const result = re[Symbol.search](str);
console.log(result); // 4
```

### サブクラスでの `[Symbol.search]()` の使用

{{jsxref("RegExp")}} のサブクラスは、動作を修正するために `[Symbol.search]()` メソッドをオーバーライドできます。

```js
class MyRegExp extends RegExp {
  constructor(str) {
    super(str);
    this.pattern = str;
  }
  [Symbol.search](str) {
    return str.indexOf(this.pattern);
  }
}

const re = new MyRegExp("a+b");
const str = "ab a+b";
const result = str.search(re); // String.prototype.search は再定義した [Symbol.search] を呼び出す。
console.log(result); // 3
```

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}

## 関連情報

- [`RegExp.prototype[Symbol.search]` のポリフィル (`core-js`)](https://github.com/zloirock/core-js#ecmascript-string-and-regexp)
- {{jsxref("String.prototype.search()")}}
- [`RegExp.prototype[Symbol.match]()`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.match)
- [`RegExp.prototype[Symbol.matchAll]()`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.matchAll)
- [`RegExp.prototype[Symbol.replace]()`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.replace)
- [`RegExp.prototype[Symbol.split]()`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.split)
- {{jsxref("RegExp.prototype.exec()")}}
- {{jsxref("RegExp.prototype.test()")}}
- {{jsxref("Symbol.search")}}
