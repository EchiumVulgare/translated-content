---
title: Firefox 22 for developers
slug: Mozilla/Firefox/Releases/22
tags:
  - Firefox
  - Firefox 22
translation_of: Mozilla/Firefox/Releases/22
---
Gecko 22 を搭載した Firefox 22 は米国時間 2013 年 6 月 25 日にリリースされました。このページでは、開発者に影響する Firefox 22 の変更点をまとめています。

## Web 開発者向けの変更点一覧

### HTML

- HTML5 の {{HTMLElement("data")}} 要素を実装しました ({{bug(839371)}})。
- {{HTMLElement("input")}} 要素の `range` ステート (`<input type="range">`) を実装しました。設定 `dom.experimental_forms_range` で制御されており、現在は Nightly および Aurora チャンネルのみ既定で有効にしています ({{bug(841948)}}).
- Web component 仕様の一部である {{HTMLElement("template")}} 要素をサポートしました ({{bug(818976)}})。

### JavaScript

- [Asm.js](http://asmjs.org/spec/latest/) の最適化が有効になり、パフォーマンス向上のために C/C++ アプリケーションを JavaScript のサブセットにコンパイルすることが可能になります。
- ES6 の [Arrow Function](/ja/docs/JavaScript/Reference/arrow_functions) 構文を実装しました ({{bug(846406)}})。
- 新しい [Object.is](/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/is) 関数が追加されました ({{bug(839979)}})。

### DOM

- `XMLHttpRequest` の `multipart` プロパティおよび `XMLHttpRequest` の `multipart/x-mixed-replace` レスポンスのサポートを削除しました。これは Gecko だけの機能であり、標準化されませんでした。[Server-Sent Events](/ja/docs/Server-sent_events)、[Web Sockets](/ja/docs/WebSockets)、あるいは progress イベントをもとに `responseText` を調べることを、代わりに使用できます。
- [Web Notifications](http://notifications.spec.whatwg.org/) をサポートしました ({{bug(782211)}})。
- {{domxref("XMLHttpRequest/FormData", "FormData")}} の `append` メソッドが、省略可能な第 3 引数 `filename` を受け入れるようになりました ({{bug(690659)}})。
- {{domxref("Node.isSupported")}} を削除しました ({{bug(801562)}})。
- {{domxref("Node.setUserData")}} および {{domxref("Node.getUserData")}} を web content 向けには削除、chrome content 向けには非推奨としました ({{bug(842372)}})。
- 仕様書で求められたため、{{domxref("Element.attributes")}} プロパティを {{domxref("Node")}} から移転しました ({{bug("844134")}})。
- **Ambient Light Events** の Mac OS X バックエンドを実装しました。
- ローカルネームが {{HTMLElement("bgsound")}}、{{HTMLElement("multicol")}} および {{HTMLElement("image")}} である HTML ネームスペースの要素は、{{domxref("HTMLSpanElement")}} インターフェイスを実装しません。{{HTMLElement("bgsound")}} および {{HTMLElement("multicol")}} は {{domxref("HTMLUnknownElement")}} を、{{HTMLElement("image")}} は {{domxref("HTMLElement")}} を実装します。
- {{ domxref("NodeIterator.detach") }} は何も行わないようになりました ({{bug("823549")}})。
- {{domxref("BlobEvent")}} インターフェイスを実装しました ({{bug("834165")}})。
- それぞれ {{domxref("HTMLMediaElement.crossOrigin")}} および `HTMLInputElement.inputMode` の仕様に合致させるため、`HTMLMediaElement.crossorigin` プロパティおよび `HTMLInputElement.inputmode` プロパティを削除しました ({{bug("847370")}} および {{bug("850346")}})。
- WebRTC: Media Stream API および Peer Connection API をデフォルトでサポートします。
- Web Components: {{domxref("Document.register")}} メソッドを実装しました ({{bug("783129")}})。

### CSS

- [CSS Flexbox layout](/ja/docs/CSS/Tutorials/Using_CSS_flexible_boxes) をデフォルトで有効にしました ({{bug("841876")}})。
- 仕様書の変更に従って、{{cssxref("min-width")}} および {{cssxref("min-height")}} の初期値を flexbox アイテムでも `0` に戻しました ({{bug("848539")}})。
- CSS 条件文 ({{cssxref("@supports")}} および {{domxref("CSS.supports")}}) をデフォルトで有効にしました ({{bug("855455")}})。
- {{cssxref("background")}} 短縮プロパティで {{cssxref("background-clip")}} および {{cssxref("background-origin")}} プロパティをサポートしました ({{bug("570896")}})。

## アドオン開発者と Mozilla 開発者向けの変更点

- `nsITreeView` のメソッド `nsITreeView.getCellProperties`、`nsITreeView.getColumnProperties` および `nsITreeView.getRowProperties` から、引数 `properties` を削除しました。これらのメソッドは空白で区切られたプロパティ名の文字列を返すようになります。({{bug('407956')}})
- `inIDOMUtils.getCSSPropertyNames` メソッドを実装しました。これはサポートしているすべての [CSS プロパティ](/ja/docs/CSS/CSS_Reference "CSS/CSS_Reference")名を返します。
- さらなる変更点については [こちら](https://blog.mozilla.org/addons/2013/06/03/compatibility-for-firefox-22/) ([日本語訳](https://dev.mozilla.jp/2013/06/firefox-22-addon-compatibility/)) をご覧ください。

### Firefox 開発ツール

- [フォントインスペクタ](https://hacks.mozilla.org/2013/04/developer-tools-update-firefox-22/)が、コンピュータ内のどのフォントがページに適用されているかを表示します。
- ハイライト表示によるフィードバックで、ページのどの領域がいつ再描画されたかを示します。
- 開発ツールをブラウザの下側だけでなく、右側にもドッキング可能になりました。
- 開発ツール内の一部ペインを [XUL から HTML](https://bugzilla.mozilla.org/show_bug.cgi?id=875727) に切り替えました。例えば CSS ルールビューアは、`cssruleview.xul` ではなく chrome://browser/content/devtools/cssruleview\.xhtml になりました。load listener を読み込んでこれらの HTML ドキュメントを変更するには、ペインの機能を拡張するために直接オーバーレイを追加するのではなく、外側の XUL ドキュメントにオーバーレイやスクリプトを追加します。
- デバッガで、スタックトレースが上側にパンくずリストのように表示されるようになりました。またスクリプト一覧がパネルの左側に表示されるようになりました。

## 関連情報

- [Firefox 22 リリースノート](http://www.mozilla.jp/firefox/22.0/releasenotes/)
- [Firefox 22 アドオン互換性情報](https://dev.mozilla.jp/2013/06/firefox-22-addon-compatibility/)

### バージョン

{{Firefox_for_developers('21')}}
