---
title: TypedArray.prototype.subarray()
slug: Web/JavaScript/Reference/Global_Objects/TypedArray/subarray
tags:
  - JavaScript
  - Method
  - Prototype
  - TypedArray
  - TypedArrays
translation_of: Web/JavaScript/Reference/Global_Objects/TypedArray/subarray
---
{{JSRef}}

**`subarray()`** メソッドは、同じ {{jsxref("ArrayBuffer")}} ストアで、この _TypedArray_ オブジェクトと同じ要素の型をもつ新しい _TypedArray_ を返します。先頭のオフセットは**含み**、末尾のオフセットは**含みません**。 _TypedArray_ は[型付き配列型](/ja/docs/Web/JavaScript/Reference/Global_Objects/TypedArray#TypedArray_objects)の一つです。

{{EmbedInteractiveExample("pages/js/typedarray-subarray.html")}}

## 構文

```
typedarray.subarray([begin[, end]])
```

### 引数

- `begin` {{optional_inline}}
  - : 先頭の要素です。この位置は含まれます。この値が指定されていない場合、配列全体が新しいビューに含まれます。
- `end` {{optional_inline}}
  - : 末尾の要素です。この位置は含まれません。この値が指定されていない場合、 `begin` によって指定された要素から配列の最後まですべての要素が新しいビューに含まれます。

### 返値

新しい {{jsxref("TypedArray")}} オブジェクトです。

## 解説

`begin` と `end` によって指定される範囲は、現在の配列に対して有効なインデックスの範囲に丸められます。すなわち、新しい範囲の計算された長さがマイナスなら、ゼロに縮められます。 `begin` か `end` のどちらかがマイナスなら、配列の最初からではなく、最後からインデックスを参照します。

既存のバッファ上に新しいビューを作っていることにも注意して下さい。すなわち、新しいオブジェクトの内容への変更は、元のオブジェクトに強い影響を与えます。逆もまた同様です。

## 例

### subarray() メソッドの使用

```js
var buffer = new ArrayBuffer(8);
var uint8 = new Uint8Array(buffer);
uint8.set([1,2,3]);

console.log(uint8); // Uint8Array [ 1, 2, 3, 0, 0, 0, 0, 0 ]

var sub = uint8.subarray(0,4);

console.log(sub);   // Uint8Array [ 1, 2, 3, 0 ]
```

## 仕様書

| 仕様書                                                                                                                           |
| -------------------------------------------------------------------------------------------------------------------------------- |
| {{SpecName('ESDraft', '#sec-%typedarray%.prototype.subarray', 'TypedArray.prototype.subarray')}} |

## ブラウザーの互換性

{{Compat("javascript.builtins.TypedArray.subarray")}}

## 関連情報

- [JavaScript の型付き配列](/ja/docs/Web/JavaScript/Typed_arrays)
- {{jsxref("TypedArray")}}
- {{jsxref("ArrayBuffer")}}
