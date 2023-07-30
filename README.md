# T3 Stack を使ってブログを作るデモ用リポジトリ

といっても、この中に入ってるものは `create-t3-app` で作成したリポジトリの一部を修正しただけのもの。

## 手順

```sh
git clone
cp .env.example .env
pnpm i
pnpm prisma db push
```

### スキーマ変更

1. `prisma/schema.prisma` を変更する
2. `pnpm prisma migrate dev` を実行する
3. VSCodeを使っている場合はコマンドで `TypeScript: Restart TS Server` を実行する

注: prismaはインストールしているprisma clientを書き換えているので、Restart TS Serverをしないと、更新したことを認識してくれない。

### APIを作る

`src/server/api/routers/example.ts` を元に postRouter を作る

* コードが無い状態で生成しようとすると少し面倒になるので、exampleRouterのコードを活かしたまま、最初のAPIを作ると楽
* tRPCの場合、参照は `query` で更新は `mutation` となっているが、まだ何も覚えてない状態でのCopilotは、更新も `query` にしようとしてくるので `mutation` を覚えさせる必要がある
* `read` とか `create` ってメソッド生やしたら `update` `delete` なども生やしてくれる
* CopilotはPrismaの使い方大体知ってる

### トップページを作る

`src/pages/index.tsx` を書き換える

* いらないモノを削る
* `const { data } = api.list` まで入力するとある程度察してくれる
* `<Link href` で大体察して New Post のコードを書いてくれる
* Next.js の古い書き方をするので `<a>` を削る
* ついでに `flex flex-col gap-10 m-10` で装飾しておく

### 投稿ページを作る

サジェストに従ってたぶん `/posts/new` あたりになると思うので、それに対応するコンポーネントを作る

* `export deafult function ` で大体察してくれるが、関数名がそれっぽくなかったらそれっぽくなるようにする
* この時点ではおそらく `api` を読み込んでないので、読み込むようにしたり `const { data } = api.post.create.` くらいまでは誘導してあげる必要あるかも
* トップページである程度装飾してると、ここでも投稿画面をそれっぽく装飾してくれるのでそれにしたがう
* 戻るリンクをつける

### 詳細ページを作る

投稿ページを作って、投稿したら、トップページにタイトルが出てくるようになってるはず

* 各投稿から、個々の詳細ページに飛べるようにする
* 詳細ページを作成する
