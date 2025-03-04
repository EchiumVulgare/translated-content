---
title: Document.createNSResolver()
slug: Web/API/Document/createNSResolver
tags:
  - API
  - DOM
  - DOM Reference
  - Method
  - Reference
translation_of: Web/API/Document/createNSResolver
---
{{ ApiRef("DOM") }}

指定されたノードのスコープで定義を尊重する名前空間を解決する `XPathNSResolver` を生成します。

## 構文

```
nsResolver = document.createNSResolver(node);
```

### 引数

- `node` は名前空間の解決のためのコンテキストとして使用されるノードです。

### 返値

- `nsResolver` は XPathNSResolver オブジェクトです。

## 注

任意の DOM ノードをネームスペースを解決するように修正し、 [XPath](/ja/docs/Web/XPath) 式が文書内に現れたノードのコンテキストに対して容易に評価できるようにします。このアダプターは、 `lookupNamespaceURI` が呼び出されたときにノードの階層で使用可能な現在の情報を使用して、指定された接頭辞から `namespaceURI` を解決する際に、ノード上の DOM Level 3 メソッド `lookupNamespaceURI` のように機能します。 暗黙の `xml` 接頭辞も正しく解決されます。

なお、 XPath は、ヌル名前空間の要素と一致する接頭辞のない QNames を定義します。 XPath には、通常の要素参照に適用される既定の名前空間を選択する方法はありません (例えば `xmlns='http://www.w3.org/1999/xhtml'` における `p[@id='_myid'`])。ヌルではない名前空間の既定の要素を照合するには、 `*namespace-uri()=http://www.w3.org/1999/xhtml and name()=p[@id='_myid']` のような形を使用して特定の要素を参照するか ([このアプローチ](/ja/docs/Web/JavaScript/Introduction_to_using_XPath_in_JavaScript#Using_XPath_functions_to_reference_elements_with_its_default_namespace)は名前空間が分からない可能性がある動的 XPath 式で動作します)、接頭辞付きの名前の条件を使用し、接頭辞と名前空間を対応付ける名前空間リゾルバーを作成するかしてください。後者のアプローチを採りたいと思うのであれば、[ユーザー定義の名前空間リゾルバーの作成方法](/ja/docs/Web/JavaScript/Introduction_to_using_XPath_in_JavaScript#Implementing_a_User_Defined_Namespace_Resolver)をお読みください。

`createNSResolver` は DOM Level 3 で導入されました。

## 仕様書

| 仕様書                                                                                                                                   | 状態                             | 備考 |
| ---------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- | ---- |
| {{SpecName('DOM3 XPath', 'xpath.html#XPathEvaluator-createNSResolver', 'document.createNSResolver')}} | {{Spec2('DOM3 XPath')}} |      |

## ブラウザーの互換性

{{Compat("api.Document.createNSResolver")}}

## 関連情報

- [document.evaluate](/ja/docs/Web/API/Document/evaluate)
- [Javascript での XPath の使用](/ja/docs/Web/JavaScript/Introduction_to_using_XPath_in_JavaScript)
