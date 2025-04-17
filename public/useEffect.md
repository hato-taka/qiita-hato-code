---
title: useEffectの基本的な使い方を初心者向けに解説！
tags:
  - JavaScript
  - React
  - useEffect
private: true
updated_at: '2025-04-17T22:57:49+09:00'
id: 625460b1845abbb6e6ed
organization_url_name: null
slide: false
ignorePublish: false
---

# useEffectの基本的な使い方を初心者向けに解説！

## はじめに

React を触り始めたばかりの方にとって、`useEffect` は少し分かりにくいフックの一つかもしれません。  
この記事では、**そもそも useEffect とは何か？** から、**どんな時に使うのか？** まで、初学者向けに丁寧に解説します。

---

## 前提知識

この記事は、以下のような方を対象としています：

- JavaScript の基本文法（`const`, `let`, `関数定義`など）がわかる
- React のコンポーネントを作ったことがある（`useState` を使ったことがある）

---

## useEffect とは？

`useEffect` は、React の **副作用（side effects）** を扱うためのフックです。

副作用とは、以下のような処理のことを指します：

- データの取得（APIリクエスト）
- DOM の直接操作
- ログの出力
- タイマーの設定

```js
import React, { useEffect } from 'react';

useEffect(() => {
  console.log("コンポーネントがマウントされたよ！");
}, []);
```

このコードは、コンポーネントが初めて画面に表示（＝マウント）されたときに、`console.log` が一度だけ実行されます。

---

## 基本構文

```js
useEffect(() => {
  // 実行したい処理
}, [依存配列]);
```

### 依存配列（dependency array）とは？

- `[]`：一度だけ実行（マウント時）
- `[count]`：`count` が変わるたびに実行
- `undefined`（省略）：毎回実行（非推奨）

---

## 例：カウントアプリで useEffect を使う

```js
import React, { useState, useEffect } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log(`カウントが ${count} に変わりました`);
  }, [count]);

  return (
    <div>
      <p>{count} 回クリックされました</p>
      <button onClick={() => setCount(count + 1)}>カウントアップ</button>
    </div>
  );
};

export default Counter;
```

この例では、`count` の値が変わるたびに、`useEffect` の中の `console.log` が実行されます。

---

## よくある注意点

- `useEffect` の中で **非同期関数**を直接書くのは NG（関数内で定義して呼び出す）
- **依存配列の漏れ**に注意（使っている変数はすべて書く）
- **クリーンアップ関数**を使えば、アンマウント時の処理もできる

```js
useEffect(() => {
  const timer = setInterval(() => {
    console.log("毎秒実行中...");
  }, 1000);

  return () => {
    clearInterval(timer); // クリーンアップ（アンマウント時）
  };
}, []);
```

---

## まとめ

- `useEffect` は副作用を扱うためのフック
- 依存配列によって「いつ実行されるか」が決まる
- タイマーやAPI通信などに活用される
- クリーンアップ関数で後処理も安全に書ける

---

## 参考リンク

- [React公式ドキュメント（useEffect）](https://ja.reactjs.org/docs/hooks-effect.html)
- [useEffect の使い方とパターンまとめ](https://zenn.dev/)
