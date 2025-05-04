---
title: 【VSCode】特定のフォルダやファイルを非表示にする方法
tags:
  - VSCode
  - 初学者
private: false
updated_at: '2022-11-05T20:16:02+09:00'
id: faa5bd1dbe87bb128a51
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

設定前は以下のように表示されています。  

![E0BC8A3C-B39F-4F04-95BA-66B51372278A.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/1cbdf52d-5746-1a79-be6c-a58858f37622.png)

VSCodeで設定を開きます。  

設定画面で`files.exclude`を検索します。  

![C556903D-7CA5-4FB3-BC16-85596EF1A4BA.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/5a77dead-4e6b-de05-265c-c7b25ad10fee.png)

「Files: Exclude」の「パターンを追加」をクリックして`**/example`を入力します。  

![C556903D-7CA5-4FB3-BC16-85596EF1A4BAのコピー.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/e0c9747d-4dd6-e3ed-8aa3-6a74d07d5316.png)

すると`example`フォルダが表示されなくなります。  

![A9A32C7B-C8C7-410C-A727-BE5CCF1B9FAB.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/ca5910ce-1b83-6d89-73d0-e187fe8a20bf.png)

また「Files: Exclude」に`**/test.txt`を追加すると`test.txt`が非表示になります。  

![59730607-424B-470C-8A39-6A04B2B5F8EE.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/7a115adb-977b-d25c-cf75-33f6fe1c5f77.png)

