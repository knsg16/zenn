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

## Auth0 SDKの追加
Auth0 Next.js SDKをインストールすることにより、プロジェクトにAuth0を追加することができます。

```shell
npm install @auth0/nextjs-auth0
```

次に、pages/api ディレクトリ内に auth/[...auth0].ts ファイルを作成し、以下のコードを追加してください。

```ts
// pages/api/auth/[...auth0].ts
import { handleAuth } from '@auth0/nextjs-auth0'

export default handleAuth()
```

このNext.jsの動的APIルートは、以下のエンドポイントを自動的に作成します。

- /api/auth/login: Auth0のログインルートになります。
- /api/auth/logout。ユーザーをログアウトさせるためのルート。
- /api/auth/callback。Auth0がログイン成功後にユーザーをリダイレクトするルート。
- /api/auth/me: Auth0からユーザープロファイルを取得するためのルートです。

最後に、pages/_app.tsx ファイルに移動し、以下のコードで更新します。このコードは、Auth0 の UserProvider コンポーネントでアプリをラップします。

```tsx
// pages/_app.tsx
import '../styles/tailwind.css'
import { UserProvider } from '@auth0/nextjs-auth0'
import Layout from '../components/Layout'
import { ApolloProvider } from '@apollo/client'
import { client } from '../lib/apollo'

function MyApp({ Component, pageProps }) {
  return (
    <UserProvider>
      <ApolloProvider client={client}>
        <Layout>
          <Component {...pageProps} />
        </Layout>
      </ApolloProvider>
    </UserProvider>
  )
}

export default MyApp

```

MyAppコンポーネントをUserProviderコンポーネントでラッピングすることで、すべてのページでユーザーの認証状態にアクセスできるようになります。

## GraphQL APIのセキュリティ確保
API にクエリーやミューテーションを送信する際、ユーザー情報を含めることでリクエストを認証することができます。これを行うには、ユーザーオブジェクト（Auth0から）をGraphQLコンテキストにアタッチします。

graphql/context.ts ファイルを以下のコードで更新してください。

```ts
// graphql/context.ts
import { PrismaClient } from '@prisma/client'
import prisma from '../lib/prisma';
import { Claims, getSession } from '@auth0/nextjs-auth0'

export type Context = {
  user?: Claims
  accessToken?: string
  prisma: PrismaClient
}

export async function createContext({ req, res }): Promise<Context> {
  const session = getSession(req, res)

  // if the user is not logged in, omit returning the user and accessToken 
  if (!session) return { prisma }

  const { user, accessToken } = session

  return {
    user,
    accessToken,
    prisma,
  }
}
```
Auth0のgetSession()関数は、ログインしているユーザーとアクセストークンの情報を返します。このデータは GraphQL コンテキストに含まれます。これで、クエリーやミューテーションが認証状態にアクセスできるようになります。

最後に、アプリのナビバーにはユーザーの認証状態に応じてログイン/ログアウトボタンが表示されるはずです。components/Layout/Header.tsx にある Header コンポーネントを次のコードで更新します。

```tsx

// components/Layout/Header.tsx
import React from 'react'
import Link from 'next/link'
import { useUser } from '@auth0/nextjs-auth0'

const Header = () => {
  const { user } = useUser()
  return (
    <header className="text-gray-600 body-font">
      <div className="container mx-auto flex flex-wrap p-5 flex-col md:flex-row items-center">
        <Link href="/">
          <a className="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0">
            <svg
              className="w-10 h-10 text-white p-2 bg-blue-500 rounded-full"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth="2"
                d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.101m-.758-4.899a4 4 0 005.656 0l4-4a4 4 0 00-5.656-5.656l-1.1 1.1"
              ></path>
            </svg>
          </a>
        </Link>
        <nav className="md:ml-auto flex flex-wrap items-center text-base justify-center">
          {user ? (
            <div className="flex items-center space-x-5">
              <Link href="/api/auth/logout">
                <a className="inline-flex items-center bg-gray-100 border-0 py-1 px-3 focus:outline-none hover:bg-gray-200 rounded text-base mt-4 md:mt-0">
                  Logout
                </a>
              </Link>
              <img alt="profile" className="rounded-full w-12 h-12" src={user.picture} />
            </div>
          ) : (
            <Link href="/api/auth/login">
              <a className="inline-flex items-center bg-gray-100 border-0 py-1 px-3 focus:outline-none hover:bg-gray-200 rounded text-base mt-4 md:mt-0">
                Login
              </a>
            </Link>
          )}
        </nav>
      </div>
    </header>
  )
}

export default Header
```

Auth0 の useUser フックは、ユーザが認証されているかどうかをチェックします。このフックはクライアントサイドで実行されます。

これまでの手順がすべて正しく行われていれば、アプリへのサインアップとログインができるはずです

![](https://storage.googleapis.com/zenn-user-upload/8ed472be22e5-20220619.png)

:::message
注：GraphQL APIへの認証済みリクエストのみを許可したい場合は、Auth0のwithApiAuthRequired関数を使用してセキュアにすることができます。
:::

## Auth0ユーザーとアプリのデータベースを同期させる
Auth0はユーザーの管理を代行するだけであり、ユーザーの認証情報以外のデータを保存することはできません。そのため、ユーザーが初めてアプリケーションにログインするたびに、データベースにユーザー情報を含む新しいレコードを作成する必要があります。

これを実現するために、Auth0 Actionsを活用します。Auth0 Actionsは、Auth0ランタイム中の特定のポイントで実行できるサーバーレス関数です。

ログイン時にAuth0 Actionから送信された情報を受け取り、データベースに保存するAPIルートを定義します。このように、サードパーティーのサービスからのイベントをリッスンするAPIエンドポイントを作成するパターンを、webhookと呼びます。

Auth0 Action を使い始めるには、左サイドバーにある Actions ドロップダウンに移動し、Flows を選択して Login を選択します。

![](https://storage.googleapis.com/zenn-user-upload/9c4b7fbc7fa7-20220619.png)

次に、新しいActionを作成するために、+アイコンをクリックし、Build customを選択します。

![](https://storage.googleapis.com/zenn-user-upload/707a116178d0-20220619.png)

カスタムアクションの名前（例：「Create DB User」）を決め、Createを選択して完了です。

![](https://storage.googleapis.com/zenn-user-upload/e7167ed93c7e-20220619.png)

前の手順が完了すると、新しく作成したアクションを管理できるようになります。

![](https://storage.googleapis.com/zenn-user-upload/a9844741c996-20220619.png)

ここでは、Auth0 ActionsのUIを分解して説明します。

- 1 - アクションのテスト
- 2 - コードで使用される環境変数/秘密を定義する。
- 3 - アクションのコードで使用されるモジュールをインクルードする
最初のステップは、node-fetchモジュール（バージョン2.6.1）をインクルードすることです。APIエンドポイントにリクエストを送るために、Actionでこれを使用することになります。このエンドポイントは、データベースにユーザーレコードを作成するロジックを処理します。

![](https://storage.googleapis.com/zenn-user-upload/270b0b2bfb85-20220619.png)

次に、Action がエンドポイントに送信するすべてのリクエストに含まれる秘密を定義します。この秘密は、リクエストが他の信頼できないサードパーティからではなく、Auth0 Action から送られてきたものであることを保証するものです。

端末で次のコマンドを実行すると、ランダムな秘密が生成されます。

```shell

openssl rand -hex 32

```

まず、このシークレットをAuth0ダッシュボードにAUTH0_HOOK_SECRETというキーで保存します。

![](https://storage.googleapis.com/zenn-user-upload/f02bdfd6670c-20220619.png)

ここで、.envファイルに秘密も保存して、アプリケーションを再起動してください。

```shell
AUTH0_HOOK_SECRET= ""   # same secret goes here

```

最後に、以下のコードでActionを更新します。

```ts
const fetch = require('node-fetch')

exports.onExecutePostLogin = async (event, api) => {
  // 1.  
  const SECRET = event.secrets.AUTH0_HOOK_SECRET
  
  // 2.
  if (event.user.app_metadata.localUserCreated) {
    return
  }

  // 3.
  const email = event.user.email

  // 4.
  const request = await fetch('http://localhost:3000/api/auth/hook', {   // "localhost:3000" will be replaced before deploying this Action
    method: 'post',
    body: JSON.stringify({ email, secret: SECRET }),
    headers: { 'Content-Type': 'application/json' },
  })
  const response = await request.json()

  // 5.
  api.user.setAppMetadata('localUserCreated', true)
}
```

1. 環境変数AUTH0_HOOK_SECRETを取得する
2. ユーザーのapp_metadataにlocalUserCreatedプロパティがあるかどうかをチェックします。
3. ログインイベントからユーザのメールアドレスを取得します - Auth0が提供します
4. API ルートに POST リクエストを送信 - http://localhost:3000/api/auth/hook
5. ユーザーの app_metadata に localUserCreated プロパティを追加します。

6. api.user.setAppMetadata 関数を使用すると、ユーザーのプロファイルに追加のプロパティを追加することができます。

このアクションをデプロイする前に、もう1つやるべきことが残っています。

# Ngrokを使ってlocalhost:3000を公開する
作成したActionはAuth0のサーバ上で動作します。あなたのコンピューターで動作しているlocalhost:3000に接続することはできません。しかし、Ngrok というツールを使って localhost:3000 をインターネットに公開し、Auth0 のサーバーからリクエストを受け取れるようにすることができます。

Ngrok は、Auth0 Action で使用可能な localhost サーバーへの URL を生成します。

アプリの実行中に、以下のコマンドを実行して localhost:3000 を公開します。

```shell
npx ngrok http 3000
```

転送先URLをコピーし、アクションの転送先URLをlocalhost:3000に置き換えて、[デプロイ]をクリックします。

アクションがデプロイされたので、[Back to flow]ボタンを押して、Loginフローに戻ります。

最後に、新しく作成したアクションをLoginフローに追加する必要があります。アクションは、[Custom]タブの下に表示されます。アクションをフローに追加するには、「開始」と「完了」の間にアクションをそして、[Apply]をクリックして変更を保存します。

![](https://storage.googleapis.com/zenn-user-upload/7e55e5e27ab7-20220619.png)

