---
title: 【React】import * as React と import React の違い
tags:
  - React
  - 初学者
private: false
updated_at: '2022-01-17T05:05:09+09:00'
id: a3dfbbf3f462b1af232f
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに
　本記事は、プログラミング初学者が、学習を進めていて疑問に思った点について調べた結果を備忘録も兼ねてまとめたものです。
　そのため、記事の内容に誤りが含まれている可能性があります。ご容赦ください。
　間違いを見つけた方は、お手数ですが、ご指摘いただけますと幸いです。

##`import * as React` と `import React` の違い
Reactでコンポーネントをインポートする際に以下の2通りの記述をよく見かけます。

```.js

import * as React from 'react';

import React from 'react';

```


###`import * as React from 'react';`
`import * as React from 'react';`は`react`でexportされているもの全てをimportして`React`という変数に格納する記述です。
以下のようになります。

```Sample.js
// named export
export const test = "Hoge";

// default import
const Default = "Fuga";

export default Default;

```

```App.js
import * as Sample from './Sample';

console.log(Sample); 
/*
  {
    test: "Hoge",
    default: "Default"
  }
*/

```


###`import React from 'react';`
`import * as React from 'react';`は`react`でexportされているもの全てをimportして`React`という変数に格納する記述です。
以下のようになります。

```Sample.js
// named export
export const test = "Hoge";

// default import
const Default = "Fuga";

export default Default;

```

```App.js
// default import
import Sample from './Sample';

console.log(Sample); 
/*
  {
    test: "Hoge",
    default: "Default"
  }
*/

```
##まとめ
`import * as ～`は、バンドラーを使用した際にビルドファイルが肥大化する恐れがあります。
ビルドファイルの肥大化をため、なるべくdefault importもしくは、named importを使用しましょう。
なお、default importは、各自が名前を決められてしまうため、named exportとnamed importを使用するのが良いようです。
