---
title: 【React】useEffectで非同期処理を行う方法
tags:
  - React
private: false
updated_at: '2024-01-04T00:02:55+09:00'
id: 9d8ffdaf57e0ac11a98c
organization_url_name: null
slide: false
ignorePublish: false
---
## 無名async関数

```react
useEffect(() => {
  (async () => {
    await sampleFunc()
  })()
}, [])
```

## async関数

```react
useEffect(() => {
  const sample = async() => {
    await sampleFunc()
  };
  sample()
}, [])
```
