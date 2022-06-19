---
title: "[Part3] TypeScript, PostgreSQL, Next.js, Prisma & GraphQLでApp作成"
emoji: "🌊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["TypeScript", "PostgreSQL", "Next.js", "Prisma", "GraphQL"]
published: false
---

:::message
本記事は、[@thisismahmoud_](https://twitter.com/thisismahmoud_)氏による「[Fullstack App With TypeScript, PostgreSQL, Next.js, Prisma & GraphQL: Authentication](https://www.prisma.io/blog/fullstack-nextjs-graphql-prisma-3-clxbrcqppv?utm_source=Prisma%20Ambassador&utm_medium=Blog%20post&utm_campaign=Prisma%20AP%20Yuuki%20Kanasugi)」の日本語翻訳を、Prismaから許可を得て掲載しているものです。※画像やリンクは公式のBlogからお借りしています。
:::

![](https://storage.googleapis.com/zenn-user-upload/2a29873cfaae-20220619.png)


# はじめに
このコースでは、ユーザーがキュレーションされたリンクのリストを閲覧し、お気に入りのリンクをブックマークできるフルスタックアプリ「awesome-links」を構築する方法を学びます。

パート2では、Apollo ServerとNexusを使用してGraphQL APIを構築しました。その後、Apollo Client を使用して、フロントエンドで GraphQL API を消費しました。

# 開発環境
このチュートリアルに沿って進めるには、Node.js と GraphQL 拡張がインストールされていることを確認してください。また、PostgreSQLデータベースが稼働している必要があります。

パート 2 から続いている場合は、プロジェクトのセットアップをスキップして、認証と Auth0 を使用した GraphQL API のセキュリティのセクションにジャンプすることができます。

:::message
注：PostgreSQLはローカルに設定することも、Herokuのホスティングインスタンスに設定することもできます。コースの最後にあるデプロイメントステップでは、リモートデータベースが必要です。
:::

# レポジトリをクローンする
このコースの完全なソースコードはGitHubで見ることができます。


:::message
注：各記事には対応するブランチがあります。このように、順を追って見ていくことができます。この記事のスタート地点は、part-3 ブランチでチェックアウトすることで同じになります。各ブランチにはいくつかの違いがあるかもしれませんので、問題に遭遇しないように、この記事のブランチをクローンすることをお勧めします。
:::

まず、任意のディレクトリに移動して、以下のコマンドを実行して、リポジトリをクローンします。

```shell
git clone -b part-3 https://github.com/prisma/awesome-links.git
```
クローンしたアプリケーションに移動し、依存関係をインストールします。


```shell
cd awesome-linksnpm install
```

# データベースのシード
PostgreSQLのデータベースをセットアップしたら、env.exampleファイルを.envにリネームして、データベースの接続文字列を設定します。その後、以下のコマンドを実行し、データベースのテーブルを作成します。

接続文字列の形式については、「Part 1 - Add Prisma to your Project」を参照してください。

```shell
npx prisma db push
```

次に、以下のコマンドを実行して、データベースのシードを行います。
```shell
npx prisma db seed
```

このコマンドは、/prisma ディレクトリにある seed.ts ファイルを実行します。seed.ts は、Prisma Client を使用してデータベースに 4 つのリンクと 1 人のユーザーを作成します。

これで、以下のコマンドを実行して、アプリケーションサーバーを起動することができます。
```shell
npm run dev
```

# プロジェクトの構成と依存関係

このアプリケーションはNext.jsで、次のライブラリやツールを利用しています。

- データベースアクセス/CRUD操作のためのPrisma
- フルスタックのReactフレームワークであるNext.js
- スタイリングにTailwindCSS
- GraphQLスキーマ構築ライブラリ：Nexus
- GraphQLサーバー：Apollo Server
- GraphQLクライアントであるApollo Client

pagesディレクトリには、以下のファイルが含まれています。

- index.tsx: APIからリンクを取得し、ページ上に表示します。結果はページングされ、さらにリンクを取得することができます。
- _app.tsx: ルートコンポーネントで、ページ間を移動するときにレイアウトと状態を持続させることができます。
- /api/graphql.ts: Next.jsのAPIルートを使用したGraphQLエンドポイントです。

# Auth0を使ったGraphQL APIの認証と安全性確保
## Auth0を設定する
アプリを保護するために、認証と認可のドロップインソリューションである Auth0 を使用します。

アカウントを作成した後、左サイドバーの［アプリケーション］ドロップダウンに移動し、サブメニューから［アプリケーション］を選択します。

![](https://storage.googleapis.com/zenn-user-upload/af6acc15bc90-20220619.png)

次に、「+ Create application」ボタンをクリックして、新しいアプリケーションを作成します。アプリの名前を付け、Regular Web Applicationを選択し、ダイアログの右下にあるCreateボタンを選択してアプリの作成を確定します。

アプリケーションが正常に作成されたら、「設定」タブに移動し、以下の情報をプロジェクトの .env ファイルにコピーしてください。

- ドメイン
- クライアントID
- クライアントシークレット

```shell
# .env
AUTH0_SECRET='...' # run `openssl rand -hex 32` to generate a 32 bytes value
AUTH0_BASE_URL='http://localhost:3000'
AUTH0_ISSUER_BASE_URL='https://YOUR_APP_DOMAIN'
AUTH0_CLIENT_ID='YOUR_CLIENT_ID'
AUTH0_CLIENT_SECRET='YOUR_CLIENT_SECRET'
```


:::message
環境変数を.envファイルに保存した後、アプリケーションを再起動します。
:::

- AUTH0_SECRET: セッションクッキーを暗号化するために使用される長い秘密値。ターミナルで openssl rand -hex 32 を実行すると、適切な文字列を生成することができます。
- AUTH0_BASE_URL: アプリケーションのベースURL。
- auth0_issuer_base_url: アプリケーションのベースURL。Auth0 のテナントドメインの URL。
- AUTH0_CLIENT_ID：あなたのAuth0アプリケーションのクライアントID。
- AUTH0_CLIENT_SECRET: Auth0アプリケーションのクライアントシークレット。
最後に、Auth0 ダッシュボードでアプリケーションの URI をいくつか設定する必要があります。**Allowed Callback URLs** に`http://localhost:3000/api/auth/callback`を追加し、**Allowed Logout URLs**リストに`http://localhost:3000`を追加します。

これらの設定変更を保存するには、ページ下部の **Save Changes** ボタンをクリックします。

アプリを本番環境にデプロイする場合、localhost をデプロイされたアプリのドメインに置き換えることができます。Auth0 では複数の URL を使用できるため、localhost と本番用 URL の両方をカンマで区切って含めることができます。

![](https://storage.googleapis.com/zenn-user-upload/af66c32e9f36-20220619.png)

