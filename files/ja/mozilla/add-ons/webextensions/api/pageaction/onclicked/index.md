---
title: pageAction.onClicked
slug: Mozilla/Add-ons/WebExtensions/API/pageAction/onClicked
---

{{AddonSidebar}}

ページアクションのアイコンがクリックされたときに発火します。ページアクションがポップアップを持っているならこのイベントは発火しません。

右クリックのアクションを定義するには、{{WebExtAPIRef('contextMenus')}} API を"page_action" {{WebExtAPIRef('contextMenus/ContextType', 'context type', '', 'nocode')}}とともに使ってください。

## 書式

```js
browser.pageAction.onClicked.addListener(listener);
browser.pageAction.onClicked.removeListener(listener);
browser.pageAction.onClicked.hasListener(listener);
```

イベントは 3 つの関数を持ちます:

- `addListener(callback)`
  - : このイベントにリスナーを追加します。Adds a listener to this event.
- `removeListener(listener)`
  - : このイベントのリスニングを停止します。引数`listener`は削除するリスナーです。
- `hasListener(listener)`
  - : `listener`がイベントに登録されているかを調べます。リスニング中であれば`true`を、そうれなければ`false`を返します。

## addListener の書式

### パラメーター

- `callback`
  - : イベント発生時に呼び出される関数です。関数は次の引数を渡されます:
    - `tab`
      - : ページアクションがクリックされたタブの{{WebExtAPIRef('tabs.Tab')}}オブジェクト。

## ブラウザーの互換性

{{Compat}}

## 例

ユーザーがページアクションをクリックしたとき、それを隠し、アクティブタブを"<http://chilloutandwatchsomecatgifs.com/>"に誘導します:

```js
var CATGIFS = "http://chilloutandwatchsomecatgifs.com/";

browser.pageAction.onClicked.addListener((tab) => {
  browser.pageAction.hide(tab.id);
  browser.tabs.update({ url: CATGIFS });
});

browser.pageAction.onClicked.addListener(function () {});
```

{{WebExtExamples}}

> [!NOTE]
> This API is based on Chromium's [`chrome.pageAction`](https://developer.chrome.com/extensions/pageAction#event-onClicked) API. This documentation is derived from [`page_action.json`](https://chromium.googlesource.com/chromium/src/+/master/chrome/common/extensions/api/page_action.json) in the Chromium code.

<!--
// Copyright 2015 The Chromium Authors. All rights reserved.
//
// Redistribution and use in source and binary forms, with or without
// modification, are permitted provided that the following conditions are
// met:
//
//    * Redistributions of source code must retain the above copyright
// notice, this list of conditions and the following disclaimer.
//    * Redistributions in binary form must reproduce the above
// copyright notice, this list of conditions and the following disclaimer
// in the documentation and/or other materials provided with the
// distribution.
//    * Neither the name of Google Inc. nor the names of its
// contributors may be used to endorse or promote products derived from
// this software without specific prior written permission.
//
// THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
// "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
// LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
// A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
// OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
// SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
// LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
// DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
// THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
// (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
// OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
-->
