---
title: 【Next.js】並列データフェッチ
tags:
  - 'Next.js'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

以下のように記述すると`getAlbums`は`getArtist`が完了するまで待機するため、2つのデータを取得するまで時間がかかります。

```typescript
export default async function Page({ params }) {
  const { username } = await params
  const artist = await getArtist(username)
  const albums = await getAlbums(username)
  
  return <div>{artist.name}</div>
}
```

これを解決するには`Promise.all`を使用して並列で実行します。

## Promise.allを使った並列実行

```typescript
async function getArtist(username: string) {
  const res = await fetch(`https://api.example.com/artist/${username}`)
  return res.json()
}

async function getAlbums(username: string) {
  const res = await fetch(`https://api.example.com/artist/${username}/albums`)
  return res.json()
}

async function getConcerts(username: string) {
  const res = await fetch(`https://api.example.com/artist/${username}/concerts`)
  return res.json()
}

export default async function ArtistPage({ params }) {
  const { username } = await params
  
  // 3つのAPIを並列実行
  const [artist, albums, concerts] = await Promise.all([
    getArtist(username),
    getAlbums(username),
    getConcerts(username)
  ])
  
  return (
    <div>
      <h1>{artist.name}</h1>
      <Albums list={albums} />
      <Concerts list={concerts} />
    </div>
  )
}
```

## Promise.allの注意点

`Promise.all`は1つでもリクエストが失敗すると全体が失敗します。

```typescript
// より堅牢なエラーハンドリング
const results = await Promise.allSettled([
  getArtist(username),
  getAlbums(username),
  getConcerts(username)
])

const artist = results[0].status === 'fulfilled' ? results[0].value : null
const albums = results[1].status === 'fulfilled' ? results[1].value : []
const concerts = results[2].status === 'fulfilled' ? results[2].value : []
```

## 依存関係がある場合の対処

データに依存関係がある場合は、必要な部分のみ順次実行し、独立した部分は並列実行します。

```typescript
export default async function Page({ params }) {
  const { username } = await params
  
  // 最初にアーティスト情報を取得（他のAPIで必要）
  const artist = await getArtist(username)
  
  // アーティストIDを使って並列実行
  const [albums, concerts, relatedArtists] = await Promise.all([
    getAlbums(artist.id),
    getConcerts(artist.id),
    getRelatedArtists(artist.genre)
  ])
  
  return <ArtistProfile artist={artist} albums={albums} concerts={concerts} related={relatedArtists} />
}
```

