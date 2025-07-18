---
title: "HTMLElement: dragleave イベント"
short-title: dragleave
slug: Web/API/HTMLElement/dragleave_event
l10n:
  sourceCommit: ea4425b74ae0dc1ec17737b4e28d8df2b73f1eae
---

{{APIRef}}

`dragleave` イベントは、ドラッグしている要素や選択中のテキストが妥当なドロップターゲットを離れたときに発生します。

このイベントはキャンセル不可で、{{domxref("Document")}} オブジェクトと {{domxref("Window")}} オブジェクトまでバブルアップする可能性があります。

## 構文

このイベント名を {{domxref("EventTarget.addEventListener", "addEventListener()")}} のようなメソッドで使用するか、イベントハンドラープロパティを設定するかします。

```js
addEventListener("dragleave", (event) => {});

ondragleave = (event) => {};
```

## イベント型

{{domxref("DragEvent")}} です。 {{domxref("Event")}} を継承しています。

{{InheritanceDiagram("DragEvent")}}

## イベントプロパティ

_以下に挙げたプロパティに加えて、親である {{domxref("Event")}} から継承したプロパティもあります。_

- {{domxref('DragEvent.dataTransfer')}} {{ReadOnlyInline}}
  - : ドラッグ＆ドロップ操作の間に転送されるデータです。

## 例

### dragleave 時にドロップゾーンのスタイルをリセット

この例では、コンテナーの中にドラッグ可能な要素を入れています。要素を掴んで、他のコンテナーの上にドラッグし、そして放してみましょう。

ドラッグ可能な要素がコンテナーの上にある間は、もう一方のコンテナーの背景を紫色にし、ドラッグ可能な要素がコンテナーの上にドロップされる可能性があることを知らせます。 `dragleave` イベントを待ち受けて、ドラッグ可能な要素がコンテナーからドラッグされたときにコンテナーの背景をリセットするようにします。

しかし、この例ではドロップは実装していません。ドラッグ＆ドロップの完全な例については、[`drag`](/ja/docs/Web/API/HTMLElement/drag_event) イベントのページを参照してください。

#### HTML

```html
<div class="dropzone">
  <div id="draggable" draggable="true">この div はドラッグ可</div>
</div>
<div class="dropzone" id="droptarget"></div>
```

#### CSS

```css
body {
  /* 例でユーザーがテキストを選択するのを防ぐ */
  user-select: none;
}

#draggable {
  text-align: center;
  background: white;
}

.dropzone {
  width: 200px;
  height: 20px;
  background: blueviolet;
  margin: 10px;
  padding: 10px;
}

.dropzone.dragover {
  background-color: purple;
}
```

#### JavaScript

```js
const target = document.getElementById("droptarget");
target.addEventListener("dragenter", (event) => {
  // ドラッグ可能な要素がドロップ先に入ったときに、ドロップ先の候補を強調表示する。
  if (event.target.classList.contains("dropzone")) {
    event.target.classList.add("dragover");
  }
});

target.addEventListener("dragleave", (event) => {
  // ドラッグ可能な要素がドロップ先から離れたときに、ドロップ先の候補の背景をリセットする
  if (event.target.classList.contains("dropzone")) {
    event.target.classList.remove("dragover");
  }
});
```

#### 例

{{EmbedLiveSample('Resetting drop zone styles on dragleave')}}

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}

## 関連情報

- その他のドラッグ＆ドロップイベント:
  - {{domxref("HTMLElement/drag_event", "drag")}}
  - {{domxref("HTMLElement/dragstart_event", "dragstart")}}
  - {{domxref("HTMLElement/dragend_event", "dragend")}}
  - {{domxref("HTMLElement/dragover_event", "dragover")}}
  - {{domxref("HTMLElement/dragenter_event", "dragenter")}}
  - {{domxref("HTMLElement/drop_event", "drop")}}
