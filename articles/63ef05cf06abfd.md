---
title: "[Part3] TypeScript, PostgreSQL, Next.js, Prisma & GraphQLã§Appä½æ"
emoji: "ð"
type: "tech" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: ["TypeScript", "PostgreSQL", "Next.js", "Prisma", "GraphQL"]
published: true
---

:::message
æ¬è¨äºã¯ã[@thisismahmoud_](https://twitter.com/thisismahmoud_)æ°ã«ããã[Fullstack App With TypeScript, PostgreSQL, Next.js, Prisma & GraphQL: Authentication](https://www.prisma.io/blog/fullstack-nextjs-graphql-prisma-3-clxbrcqppv?utm_source=Prisma%20Ambassador&utm_medium=Blog%20post&utm_campaign=Prisma%20AP%20Yuuki%20Kanasugi)ãã®æ¥æ¬èªç¿»è¨³ããPrismaããè¨±å¯ãå¾ã¦æ²è¼ãã¦ãããã®ã§ããâ»ç»åããªã³ã¯ã¯å¬å¼ã®Blogãããåããã¦ãã¾ãã
:::

![](https://storage.googleapis.com/zenn-user-upload/2a29873cfaae-20220619.png)

Part1ã¯ãã¡ã
https://zenn.dev/kanasugi/articles/a840e733f8e6a1

Part2ã¯ãã¡ã
https://zenn.dev/kanasugi/articles/e14995bc1c8ad3


# ã¯ããã«
ãã®ã³ã¼ã¹ã§ã¯ãã¦ã¼ã¶ã¼ãã­ã¥ã¬ã¼ã·ã§ã³ããããªã³ã¯ã®ãªã¹ããé²è¦§ãããæ°ã«å¥ãã®ãªã³ã¯ãããã¯ãã¼ã¯ã§ãããã«ã¹ã¿ãã¯ã¢ããªãawesome-linksããæ§ç¯ããæ¹æ³ãå­¦ã³ã¾ãã

ãã¼ã2ã§ã¯ãApollo Serverã¨Nexusãä½¿ç¨ãã¦GraphQL APIãæ§ç¯ãã¾ããããã®å¾ãApollo Client ãä½¿ç¨ãã¦ããã­ã³ãã¨ã³ãã§ GraphQL API ãæ¶è²»ãã¾ããã

# éçºç°å¢
ãã®ãã¥ã¼ããªã¢ã«ã«æ²¿ã£ã¦é²ããã«ã¯ãNode.js ã¨ GraphQL æ¡å¼µãã¤ã³ã¹ãã¼ã«ããã¦ãããã¨ãç¢ºèªãã¦ãã ãããã¾ããPostgreSQLãã¼ã¿ãã¼ã¹ãç¨¼åãã¦ããå¿è¦ãããã¾ãã

ãã¼ã 2 ããç¶ãã¦ããå ´åã¯ããã­ã¸ã§ã¯ãã®ã»ããã¢ãããã¹ã­ãããã¦ãèªè¨¼ã¨ Auth0 ãä½¿ç¨ãã GraphQL API ã®ã»ã­ã¥ãªãã£ã®ã»ã¯ã·ã§ã³ã«ã¸ã£ã³ããããã¨ãã§ãã¾ãã

:::message
æ³¨ï¼PostgreSQLã¯ã­ã¼ã«ã«ã«è¨­å®ãããã¨ããHerokuã®ãã¹ãã£ã³ã°ã¤ã³ã¹ã¿ã³ã¹ã«è¨­å®ãããã¨ãã§ãã¾ããã³ã¼ã¹ã®æå¾ã«ããããã­ã¤ã¡ã³ãã¹ãããã§ã¯ããªã¢ã¼ããã¼ã¿ãã¼ã¹ãå¿è¦ã§ãã
:::

# ã¬ãã¸ããªãã¯ã­ã¼ã³ãã
ãã®ã³ã¼ã¹ã®å®å¨ãªã½ã¼ã¹ã³ã¼ãã¯GitHubã§è¦ããã¨ãã§ãã¾ãã


:::message
æ³¨ï¼åè¨äºã«ã¯å¯¾å¿ãããã©ã³ããããã¾ãããã®ããã«ãé ãè¿½ã£ã¦è¦ã¦ãããã¨ãã§ãã¾ãããã®è¨äºã®ã¹ã¿ã¼ãå°ç¹ã¯ãpart-3 ãã©ã³ãã§ãã§ãã¯ã¢ã¦ããããã¨ã§åãã«ãªãã¾ããåãã©ã³ãã«ã¯ããã¤ãã®éããããããããã¾ããã®ã§ãåé¡ã«é­éããªãããã«ããã®è¨äºã®ãã©ã³ããã¯ã­ã¼ã³ãããã¨ããå§ããã¾ãã
:::

ã¾ããä»»æã®ãã£ã¬ã¯ããªã«ç§»åãã¦ãä»¥ä¸ã®ã³ãã³ããå®è¡ãã¦ããªãã¸ããªãã¯ã­ã¼ã³ãã¾ãã

```shell
git clone -b part-3 https://github.com/prisma/awesome-links.git
```
ã¯ã­ã¼ã³ããã¢ããªã±ã¼ã·ã§ã³ã«ç§»åããä¾å­é¢ä¿ãã¤ã³ã¹ãã¼ã«ãã¾ãã


```shell
cd awesome-links npm install
```

# ãã¼ã¿ãã¼ã¹ã®ã·ã¼ã
PostgreSQLã®ãã¼ã¿ãã¼ã¹ãã»ããã¢ããããããenv.exampleãã¡ã¤ã«ã.envã«ãªãã¼ã ãã¦ããã¼ã¿ãã¼ã¹ã®æ¥ç¶æå­åãè¨­å®ãã¾ãããã®å¾ãä»¥ä¸ã®ã³ãã³ããå®è¡ãããã¼ã¿ãã¼ã¹ã®ãã¼ãã«ãä½æãã¾ãã

æ¥ç¶æå­åã®å½¢å¼ã«ã¤ãã¦ã¯ããPart 1 - Add Prisma to your Projectããåç§ãã¦ãã ããã

```shell
npx prisma db push
```

æ¬¡ã«ãä»¥ä¸ã®ã³ãã³ããå®è¡ãã¦ããã¼ã¿ãã¼ã¹ã®ã·ã¼ããè¡ãã¾ãã
```shell
npx prisma db seed
```

ãã®ã³ãã³ãã¯ã/prisma ãã£ã¬ã¯ããªã«ãã seed.ts ãã¡ã¤ã«ãå®è¡ãã¾ããseed.ts ã¯ãPrisma Client ãä½¿ç¨ãã¦ãã¼ã¿ãã¼ã¹ã« 4 ã¤ã®ãªã³ã¯ã¨ 1 äººã®ã¦ã¼ã¶ã¼ãä½æãã¾ãã


:::message
ããããã¼ã¿ãã¼ã¹ã®seedãã§ããªãå ´åã¯ãpackage.jsonãä»¥ä¸ã®ããã«å¤æ´ãã¦ã¿ã¦ãã ããã

:::

```json
{
  "name": "awesome-links",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start"
  },
  "dependencies": {
    "@apollo/client": "^3.5.10",
    "@prisma/client": "^3.12.0",
    "apollo-server-micro": "^3.6.7",
    "graphql": "^16.3.0",
    "micro-cors": "^0.1.1",
    "next": "11.0.1",
    "nexus": "^1.3.0",
    "react": "17.0.2",
    "react-dom": "17.0.2"
  },
  "devDependencies": {
    "@tailwindcss/forms": "^0.3.3",
    "@tailwindcss/typography": "^0.4.1",
    "@types/node": "^16.11.11",
    "@types/react": "^17.0.14",
    "autoprefixer": "^10.3.1",
    "postcss": "^8.3.5",
    "prisma": "^3.12.0",
    "tailwindcss": "^2.2.4",
    "ts-node": "^10.7.0",
    "typescript": "^4.5.2"
  },
  "prisma": {
    "seed": "ts-node --compiler-options {\"module\":\"CommonJS\"} prisma/seed.ts"
  }
}

```

ããã§ãä»¥ä¸ã®ã³ãã³ããå®è¡ãã¦ãã¢ããªã±ã¼ã·ã§ã³ãµã¼ãã¼ãèµ·åãããã¨ãã§ãã¾ãã
```shell
npm run dev
```

# ãã­ã¸ã§ã¯ãã®æ§æã¨ä¾å­é¢ä¿

ãã­ã¸ã§ã¯ãã®ãã©ã«ãæ§æã¯ä»¥ä¸ã®éãã§ãã
```
awesome-links/
â£ components/
â£ data/
â â links.ts
â£ graphql/
â â£ types/
â â£ context.ts
â â£ schema.graphql
â â schema.ts
â£ lib/
â â£ apollo.ts
â â prisma.ts
â£ pages/
â â£ api/
â â â graphql.ts
â â£ _app.tsx
â â index.tsx
â£ prisma/
â â£ schema.prisma
â â seed.ts
â£ public/
â£ styles/
â â tailwind.css
â£ .babelrc
â£ .env.example
â£ .gitignore
â£ README.md
â£ next-env.d.ts
â£ package-lock.json
â£ package.json
â£ postcss.config.js
â£ tailwind.config.js
â tsconfig.json
```

ãã®ã¢ããªã±ã¼ã·ã§ã³ã¯Next.jsã§ãæ¬¡ã®ã©ã¤ãã©ãªããã¼ã«ãå©ç¨ãã¦ãã¾ãã

- ãã¼ã¿ãã¼ã¹ã¢ã¯ã»ã¹/CRUDæä½ã®ããã®Prisma
- ãã«ã¹ã¿ãã¯ã®Reactãã¬ã¼ã ã¯ã¼ã¯ã§ããNext.js
- ã¹ã¿ã¤ãªã³ã°ã«TailwindCSS
- GraphQLã¹ã­ã¼ãæ§ç¯ã©ã¤ãã©ãªï¼Nexus
- GraphQLãµã¼ãã¼ï¼Apollo Server
- GraphQLã¯ã©ã¤ã¢ã³ãã§ããApollo Client

pagesãã£ã¬ã¯ããªã«ã¯ãä»¥ä¸ã®ãã¡ã¤ã«ãå«ã¾ãã¦ãã¾ãã

- index.tsx: APIãããªã³ã¯ãåå¾ãããã¼ã¸ä¸ã«è¡¨ç¤ºãã¾ããçµæã¯ãã¼ã¸ã³ã°ãããããã«ãªã³ã¯ãåå¾ãããã¨ãã§ãã¾ãã
- _app.tsx: ã«ã¼ãã³ã³ãã¼ãã³ãã§ããã¼ã¸éãç§»åããã¨ãã«ã¬ã¤ã¢ã¦ãã¨ç¶æãæç¶ããããã¨ãã§ãã¾ãã
- /api/graphql.ts: Next.jsã®APIã«ã¼ããä½¿ç¨ããGraphQLã¨ã³ããã¤ã³ãã§ãã

# Auth0ãä½¿ã£ãGraphQL APIã®èªè¨¼ã¨å®å¨æ§ç¢ºä¿
## Auth0ãè¨­å®ãã
ã¢ããªãä¿è­·ããããã«ãèªè¨¼ã¨èªå¯ã®ãã­ããã¤ã³ã½ãªã¥ã¼ã·ã§ã³ã§ãã Auth0 ãä½¿ç¨ãã¾ãã

ã¢ã«ã¦ã³ããä½æããå¾ãå·¦ãµã¤ããã¼ã®ï¼»ã¢ããªã±ã¼ã·ã§ã³ï¼½ãã­ãããã¦ã³ã«ç§»åãããµãã¡ãã¥ã¼ããï¼»ã¢ããªã±ã¼ã·ã§ã³ï¼½ãé¸æãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/af6acc15bc90-20220619.png)

æ¬¡ã«ãã+ Create applicationããã¿ã³ãã¯ãªãã¯ãã¦ãæ°ããã¢ããªã±ã¼ã·ã§ã³ãä½æãã¾ããã¢ããªã®ååãä»ããRegular Web Applicationãé¸æãããã¤ã¢ã­ã°ã®å³ä¸ã«ããCreateãã¿ã³ãé¸æãã¦ã¢ããªã®ä½æãç¢ºå®ãã¾ãã

ã¢ããªã±ã¼ã·ã§ã³ãæ­£å¸¸ã«ä½æããããããè¨­å®ãã¿ãã«ç§»åããä»¥ä¸ã®æå ±ããã­ã¸ã§ã¯ãã® .env ãã¡ã¤ã«ã«ã³ãã¼ãã¦ãã ããã

- ãã¡ã¤ã³
- ã¯ã©ã¤ã¢ã³ãID
- ã¯ã©ã¤ã¢ã³ãã·ã¼ã¯ã¬ãã

```shell
# .env
AUTH0_SECRET='...' # run `openssl rand -hex 32` to generate a 32 bytes value
AUTH0_BASE_URL='http://localhost:3000'
AUTH0_ISSUER_BASE_URL='https://YOUR_APP_DOMAIN'
AUTH0_CLIENT_ID='YOUR_CLIENT_ID'
AUTH0_CLIENT_SECRET='YOUR_CLIENT_SECRET'
```


:::message
ç°å¢å¤æ°ã.envãã¡ã¤ã«ã«ä¿å­ããå¾ãã¢ããªã±ã¼ã·ã§ã³ãåèµ·åãã¾ãã
:::

- AUTH0_SECRET: ã»ãã·ã§ã³ã¯ãã­ã¼ãæå·åããããã«ä½¿ç¨ãããé·ãç§å¯å¤ãã¿ã¼ããã«ã§ `openssl rand -hex 32` ãå®è¡ããã¨ãé©åãªæå­åãçæãããã¨ãã§ãã¾ãã
- AUTH0_BASE_URL: ã¢ããªã±ã¼ã·ã§ã³ã®ãã¼ã¹URLã
- auth0_issuer_base_url: ã¢ããªã±ã¼ã·ã§ã³ã®ãã¼ã¹URLãAuth0 ã®ããã³ããã¡ã¤ã³ã® URLã
- AUTH0_CLIENT_IDï¼ããªãã®Auth0ã¢ããªã±ã¼ã·ã§ã³ã®ã¯ã©ã¤ã¢ã³ãIDã
- AUTH0_CLIENT_SECRET: Auth0ã¢ããªã±ã¼ã·ã§ã³ã®ã¯ã©ã¤ã¢ã³ãã·ã¼ã¯ã¬ããã

æå¾ã«ãAuth0 ããã·ã¥ãã¼ãã§ã¢ããªã±ã¼ã·ã§ã³ã® URI ãããã¤ãè¨­å®ããå¿è¦ãããã¾ãã**Allowed Callback URLs** ã«`http://localhost:3000/api/auth/callback`ãè¿½å ãã**Allowed Logout URLs**ãªã¹ãã«`http://localhost:3000`ãè¿½å ãã¾ãã

ãããã®è¨­å®å¤æ´ãä¿å­ããã«ã¯ããã¼ã¸ä¸é¨ã® **Save Changes** ãã¿ã³ãã¯ãªãã¯ãã¾ãã

ã¢ããªãæ¬çªç°å¢ã«ããã­ã¤ããå ´åãlocalhost ãããã­ã¤ãããã¢ããªã®ãã¡ã¤ã³ã«ç½®ãæãããã¨ãã§ãã¾ããAuth0 ã§ã¯è¤æ°ã® URL ãä½¿ç¨ã§ãããããlocalhost ã¨æ¬çªç¨ URL ã®ä¸¡æ¹ãã«ã³ãã§åºåã£ã¦å«ãããã¨ãã§ãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/af66c32e9f36-20220619.png)

## Auth0 SDKã®è¿½å 
Auth0 Next.js SDKãã¤ã³ã¹ãã¼ã«ãããã¨ã«ããããã­ã¸ã§ã¯ãã«Auth0ãè¿½å ãããã¨ãã§ãã¾ãã

```shell
npm install @auth0/nextjs-auth0
```

æ¬¡ã«ãpages/api ãã£ã¬ã¯ããªåã« auth/[...auth0].ts ãã¡ã¤ã«ãä½æããä»¥ä¸ã®ã³ã¼ããè¿½å ãã¦ãã ããã

```ts
// pages/api/auth/[...auth0].ts
import { handleAuth } from '@auth0/nextjs-auth0'

export default handleAuth()
```

ãã®Next.jsã®åçAPIã«ã¼ãã¯ãä»¥ä¸ã®ã¨ã³ããã¤ã³ããèªåçã«ä½æãã¾ãã

- /api/auth/login: Auth0ã®ã­ã°ã¤ã³ã«ã¼ãã«ãªãã¾ãã
- /api/auth/logoutãã¦ã¼ã¶ã¼ãã­ã°ã¢ã¦ããããããã®ã«ã¼ãã
- /api/auth/callbackãAuth0ãã­ã°ã¤ã³æåå¾ã«ã¦ã¼ã¶ã¼ããªãã¤ã¬ã¯ãããã«ã¼ãã
- /api/auth/me: Auth0ããã¦ã¼ã¶ã¼ãã­ãã¡ã¤ã«ãåå¾ããããã®ã«ã¼ãã§ãã

æå¾ã«ãpages/_app.tsx ãã¡ã¤ã«ã«ç§»åããä»¥ä¸ã®ã³ã¼ãã§æ´æ°ãã¾ãããã®ã³ã¼ãã¯ãAuth0 ã® UserProvider ã³ã³ãã¼ãã³ãã§ã¢ããªãã©ãããã¾ãã

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

MyAppã³ã³ãã¼ãã³ããUserProviderã³ã³ãã¼ãã³ãã§ã©ããã³ã°ãããã¨ã§ããã¹ã¦ã®ãã¼ã¸ã§ã¦ã¼ã¶ã¼ã®èªè¨¼ç¶æã«ã¢ã¯ã»ã¹ã§ããããã«ãªãã¾ãã

## GraphQL APIã®ã»ã­ã¥ãªãã£ç¢ºä¿
API ã«ã¯ã¨ãªã¼ããã¥ã¼ãã¼ã·ã§ã³ãéä¿¡ããéãã¦ã¼ã¶ã¼æå ±ãå«ãããã¨ã§ãªã¯ã¨ã¹ããèªè¨¼ãããã¨ãã§ãã¾ãããããè¡ãã«ã¯ãã¦ã¼ã¶ã¼ãªãã¸ã§ã¯ãï¼Auth0ããï¼ãGraphQLã³ã³ãã­ã¹ãã«ã¢ã¿ãããã¾ãã

graphql/context.ts ãã¡ã¤ã«ãä»¥ä¸ã®ã³ã¼ãã§æ´æ°ãã¦ãã ããã

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
Auth0ã®getSession()é¢æ°ã¯ãã­ã°ã¤ã³ãã¦ããã¦ã¼ã¶ã¼ã¨ã¢ã¯ã»ã¹ãã¼ã¯ã³ã®æå ±ãè¿ãã¾ãããã®ãã¼ã¿ã¯ GraphQL ã³ã³ãã­ã¹ãã«å«ã¾ãã¾ããããã§ãã¯ã¨ãªã¼ããã¥ã¼ãã¼ã·ã§ã³ãèªè¨¼ç¶æã«ã¢ã¯ã»ã¹ã§ããããã«ãªãã¾ãã

æå¾ã«ãã¢ããªã®ãããã¼ã«ã¯ã¦ã¼ã¶ã¼ã®èªè¨¼ç¶æã«å¿ãã¦ã­ã°ã¤ã³/ã­ã°ã¢ã¦ããã¿ã³ãè¡¨ç¤ºãããã¯ãã§ããcomponents/Layout/Header.tsx ã«ãã Header ã³ã³ãã¼ãã³ããæ¬¡ã®ã³ã¼ãã§æ´æ°ãã¾ãã

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

Auth0 ã® useUser ããã¯ã¯ãã¦ã¼ã¶ãèªè¨¼ããã¦ãããã©ããããã§ãã¯ãã¾ãããã®ããã¯ã¯ã¯ã©ã¤ã¢ã³ããµã¤ãã§å®è¡ããã¾ãã

ããã¾ã§ã®æé ããã¹ã¦æ­£ããè¡ããã¦ããã°ãã¢ããªã¸ã®ãµã¤ã³ã¢ããã¨ã­ã°ã¤ã³ãã§ããã¯ãã§ã

![](https://storage.googleapis.com/zenn-user-upload/8ed472be22e5-20220619.png)

:::message
æ³¨ï¼GraphQL APIã¸ã®èªè¨¼æ¸ã¿ãªã¯ã¨ã¹ãã®ã¿ãè¨±å¯ãããå ´åã¯ãAuth0ã®withApiAuthRequiredé¢æ°ãä½¿ç¨ãã¦ã»ã­ã¥ã¢ã«ãããã¨ãã§ãã¾ãã
:::

## Auth0ã¦ã¼ã¶ã¼ã¨ã¢ããªã®ãã¼ã¿ãã¼ã¹ãåæããã
Auth0ã¯ã¦ã¼ã¶ã¼ã®ç®¡çãä»£è¡ããã ãã§ãããã¦ã¼ã¶ã¼ã®èªè¨¼æå ±ä»¥å¤ã®ãã¼ã¿ãä¿å­ãããã¨ã¯ã§ãã¾ããããã®ãããã¦ã¼ã¶ã¼ãåãã¦ã¢ããªã±ã¼ã·ã§ã³ã«ã­ã°ã¤ã³ãããã³ã«ããã¼ã¿ãã¼ã¹ã«ã¦ã¼ã¶ã¼æå ±ãå«ãæ°ããã¬ã³ã¼ããä½æããå¿è¦ãããã¾ãã

ãããå®ç¾ããããã«ãAuth0 Actionsãæ´»ç¨ãã¾ããAuth0 Actionsã¯ãAuth0ã©ã³ã¿ã¤ã ä¸­ã®ç¹å®ã®ãã¤ã³ãã§å®è¡ã§ãããµã¼ãã¼ã¬ã¹é¢æ°ã§ãã

ã­ã°ã¤ã³æã«Auth0 Actionããéä¿¡ãããæå ±ãåãåãããã¼ã¿ãã¼ã¹ã«ä¿å­ããAPIã«ã¼ããå®ç¾©ãã¾ãããã®ããã«ããµã¼ããã¼ãã£ã¼ã®ãµã¼ãã¹ããã®ã¤ãã³ãããªãã¹ã³ããAPIã¨ã³ããã¤ã³ããä½æãããã¿ã¼ã³ããwebhookã¨å¼ã³ã¾ãã

Auth0 Action ãä½¿ãå§ããã«ã¯ãå·¦ãµã¤ããã¼ã«ãã Actions ãã­ãããã¦ã³ã«ç§»åããFlows ãé¸æãã¦ Login ãé¸æãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/9c4b7fbc7fa7-20220619.png)

æ¬¡ã«ãæ°ããActionãä½æããããã«ã+ã¢ã¤ã³ã³ãã¯ãªãã¯ããBuild customãé¸æãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/707a116178d0-20220619.png)

ã«ã¹ã¿ã ã¢ã¯ã·ã§ã³ã®ååï¼ä¾ï¼ãCreate DB Userãï¼ãæ±ºããCreateãé¸æãã¦å®äºã§ãã

![](https://storage.googleapis.com/zenn-user-upload/e7167ed93c7e-20220619.png)

åã®æé ãå®äºããã¨ãæ°ããä½æããã¢ã¯ã·ã§ã³ãç®¡çã§ããããã«ãªãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/a9844741c996-20220619.png)

ããã§ã¯ãAuth0 Actionsã®UIãåè§£ãã¦èª¬æãã¾ãã

- 1 - ã¢ã¯ã·ã§ã³ã®ãã¹ã
- 2 - ã³ã¼ãã§ä½¿ç¨ãããç°å¢å¤æ°/ç§å¯éµãå®ç¾©ããã
- 3 - ã¢ã¯ã·ã§ã³ã®ã³ã¼ãã§ä½¿ç¨ãããã¢ã¸ã¥ã¼ã«ãã¤ã³ã¯ã«ã¼ããã
æåã®ã¹ãããã¯ãnode-fetchã¢ã¸ã¥ã¼ã«ï¼ãã¼ã¸ã§ã³2.6.1ï¼ãã¤ã³ã¯ã«ã¼ããããã¨ã§ããAPIã¨ã³ããã¤ã³ãã«ãªã¯ã¨ã¹ããéãããã«ãActionã§ãããä½¿ç¨ãããã¨ã«ãªãã¾ãããã®ã¨ã³ããã¤ã³ãã¯ããã¼ã¿ãã¼ã¹ã«ã¦ã¼ã¶ã¼ã¬ã³ã¼ããä½æããã­ã¸ãã¯ãå¦çãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/270b0b2bfb85-20220619.png)

æ¬¡ã«ãAction ãã¨ã³ããã¤ã³ãã«éä¿¡ãããã¹ã¦ã®ãªã¯ã¨ã¹ãã«å«ã¾ããç§å¯ãå®ç¾©ãã¾ãããã®ç§å¯ã¯ããªã¯ã¨ã¹ããä»ã®ä¿¡é ¼ã§ããªããµã¼ããã¼ãã£ããã§ã¯ãªããAuth0 Action ããéããã¦ãããã®ã§ãããã¨ãä¿è¨¼ãããã®ã§ãã

ç«¯æ«ã§æ¬¡ã®ã³ãã³ããå®è¡ããã¨ãã©ã³ãã ãªç§å¯ãçæããã¾ãã

```shell

openssl rand -hex 32

```

ã¾ãããã®ã·ã¼ã¯ã¬ãããAuth0ããã·ã¥ãã¼ãã«AUTH0_HOOK_SECRETã¨ããã­ã¼ã§ä¿å­ãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/f02bdfd6670c-20220619.png)

ããã§ã.envãã¡ã¤ã«ã«ç§å¯ãä¿å­ãã¦ãã¢ããªã±ã¼ã·ã§ã³ãåèµ·åãã¦ãã ããã

```shell
AUTH0_HOOK_SECRET= ""   # same secret goes here

```

æå¾ã«ãä»¥ä¸ã®ã³ã¼ãã§Actionãæ´æ°ãã¾ãã

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

1. ç°å¢å¤æ°AUTH0_HOOK_SECRETãåå¾ãã
2. ã¦ã¼ã¶ã¼ã®app_metadataã«localUserCreatedãã­ããã£ããããã©ããããã§ãã¯ãã¾ãã
3. ã­ã°ã¤ã³ã¤ãã³ãããã¦ã¼ã¶ã®ã¡ã¼ã«ã¢ãã¬ã¹ãåå¾ãã¾ã - Auth0ãæä¾ãã¾ã
4. API ã«ã¼ãã« POST ãªã¯ã¨ã¹ããéä¿¡ - http://localhost:3000/api/auth/hook
5. ã¦ã¼ã¶ã¼ã® app_metadata ã« localUserCreated ãã­ããã£ãè¿½å ãã¾ãã

6. api.user.setAppMetadata é¢æ°ãä½¿ç¨ããã¨ãã¦ã¼ã¶ã¼ã®ãã­ãã¡ã¤ã«ã«è¿½å ã®ãã­ããã£ãè¿½å ãããã¨ãã§ãã¾ãã

ãã®ã¢ã¯ã·ã§ã³ãããã­ã¤ããåã«ããã1ã¤ããã¹ããã¨ãæ®ã£ã¦ãã¾ãã

## Ngrokãä½¿ã£ã¦localhost:3000ãå¬éãã
ä½æããActionã¯Auth0ã®ãµã¼ãä¸ã§åä½ãã¾ããããªãã®ã³ã³ãã¥ã¼ã¿ã¼ã§åä½ãã¦ããlocalhost:3000ã«æ¥ç¶ãããã¨ã¯ã§ãã¾ãããããããNgrok ã¨ãããã¼ã«ãä½¿ã£ã¦ localhost:3000 ãã¤ã³ã¿ã¼ãããã«å¬éããAuth0 ã®ãµã¼ãã¼ãããªã¯ã¨ã¹ããåãåããããã«ãããã¨ãã§ãã¾ãã

Ngrok ã¯ãAuth0 Action ã§ä½¿ç¨å¯è½ãª localhost ãµã¼ãã¼ã¸ã® URL ãçæãã¾ãã

ã¢ããªã®å®è¡ä¸­ã«ãä»¥ä¸ã®ã³ãã³ããå®è¡ãã¦ localhost:3000 ãå¬éãã¾ãã

```shell
npx ngrok http 3000
```

è»¢éåURLãã³ãã¼ããã¢ã¯ã·ã§ã³ã®è»¢éåURLãlocalhost:3000ã«ç½®ãæãã¦ã[ããã­ã¤]ãã¯ãªãã¯ãã¾ãã

ã¢ã¯ã·ã§ã³ãããã­ã¤ãããã®ã§ã[Back to flow]ãã¿ã³ãæ¼ãã¦ãLoginãã­ã¼ã«æ»ãã¾ãã

æå¾ã«ãæ°ããä½æããã¢ã¯ã·ã§ã³ãLoginãã­ã¼ã«è¿½å ããå¿è¦ãããã¾ããã¢ã¯ã·ã§ã³ã¯ã[Custom]ã¿ãã®ä¸ã«è¡¨ç¤ºããã¾ããã¢ã¯ã·ã§ã³ããã­ã¼ã«è¿½å ããã«ã¯ããStartãã¨ãCompleteãã®éã«ã¢ã¯ã·ã§ã³ãããã¦ã[Apply]ãã¯ãªãã¯ãã¦å¤æ´ãä¿å­ãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/7e55e5e27ab7-20220619.png)

## æ°è¦ã¦ã¼ã¶ã¼ä½æç¨ã® API ã«ã¼ããå®ç¾©ãã
pages/api/auth/ãã©ã«ãã«hook.tsãã¡ã¤ã«ãä½æããä»¥ä¸ã®ã³ã¼ããè¿½å ãã¦ãã ããã

```ts
// pages/api/auth/hook
import  prisma from '../../../lib/prisma';
import type { NextApiRequest, NextApiResponse } from 'next';

const handler = async (req: NextApiRequest, res: NextApiResponse) => {
  const { email, secret } = req.body;
  // 1
  if (req.method !== 'POST') {
    return res.status(403).json({ message: 'Method not allowed' });
  }
  // 2
  if (secret !== process.env.AUTH0_HOOK_SECRET) {
    return res.status(403).json({ message: `You must provide the secret ð¤«` });
  }
  // 3
  if (email) {
    // 4
    await prisma.user.create({
      data: { email },
    });
    return res.status(200).json({
      message: `User with email: ${email} has been created successfully!`,
    });
  }
};

export default handler;
```

ãã®ã¨ã³ããã¤ã³ãã¯ãä»¥ä¸ã®ãã¨ãè¡ãã¾ãã

1. ãªã¯ã¨ã¹ãã POST ãªã¯ã¨ã¹ãã§ãããã¨ãæ¤è¨¼ãã¾ãã
2. ãªã¯ã¨ã¹ãããã£ã«ãã AUTH0_HOOK_SECRET ãæ­£ãããã©ãããæ¤è¨¼ãã¾ãã
3. ãªã¯ã¨ã¹ãããã£ã§æä¾ãããé»å­ã¡ã¼ã«ãæ­£ãããã©ããæ¤è¨¼ãã
4. æ°ããã¦ã¼ã¶ã¼ã¬ã³ã¼ããä½æãã

ã¦ã¼ã¶ã¼ãã¢ããªã±ã¼ã·ã§ã³ã«ãµã¤ã³ã¢ããããã¨ããã®ã¦ã¼ã¶ã¼ã®æå ±ã¯ãã¼ã¿ãã¼ã¹ã«åæããã¾ããæ°ããä½æãããã¦ã¼ã¶ã¼ã¯ãPrisma Studioã§ãã¼ã¿ãã¼ã¹ã«è¡¨ç¤ºãããã¨ãã§ãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/430f4966293d-20220619.png)

## ãªã³ã¯ã®ä½æ - èªè¨¼ä¿è­·ããããã¼ã¸
graphql/types/Link.tsãæ´æ°ãããªã³ã¯ãä½æããæ©è½ãè¿½å ããä»¥ä¸ã®ãã¥ã¼ãã¼ã·ã§ã³ãè¡ãã¾ãã

```ts
// graphql/types/Link.ts
export const CreateLinkMutation = extendType({
  type: 'Mutation',
  definition(t) {
    t.nonNull.field('createLink', {
      type: Link,
      args: {
        title: nonNull(stringArg()),
        url: nonNull(stringArg()),
        imageUrl: nonNull(stringArg()),
        category: nonNull(stringArg()),
        description: nonNull(stringArg()),
      },
      async resolve(_parent, args, ctx) {

        if (!ctx.user) {
          throw new Error(`You need to be logged in to perform an action`)
        }

        const newLink = {
          title: args.title,
          url: args.url,
          imageUrl: args.imageUrl,
          category: args.category,
          description: args.description,
        }

        return await ctx.prisma.link.create({
          data: newLink,
        })
      },
    })
  },
})
```

args ãã­ããã£ã¯ãæ°ãããªã³ã¯ãä½æããããã«å¿è¦ãªå¥åãå®ç¾©ãã¾ããã¾ãããã¥ã¼ãã¼ã·ã§ã³ã¯ã¦ã¼ã¶ãã­ã°ã¤ã³ãã¦ãããã©ããããã§ãã¯ããã®ã§ãèªè¨¼ãããã¦ã¼ã¶ã®ã¿ããªã³ã¯ãä½æãããã¨ãã§ãã¾ããæå¾ã«ãPrismaã®create()é¢æ°ãæ°ãããã¼ã¿ãã¼ã¹ã¬ã³ã¼ããä½æãã¾ãã

æ¬¡ã«ãpages/admin.tsxãã¼ã¸ãä½æããä»¥ä¸ã®ã³ã¼ããè¿½å ãã¾ãããã®ã³ã¼ãã«ãããæ°ãããªã³ã¯ã®ä½æãå¯è½ã«ãªãã¾ãã

```tsx
// pages/admin.tsx
import React from 'react'
import { useForm } from 'react-hook-form'
import { gql, useMutation } from '@apollo/client'
import toast, { Toaster } from 'react-hot-toast'
import { getSession } from '@auth0/nextjs-auth0'
import prisma from '../lib/prisma'

const CreateLinkMutation = gql`
  mutation($title: String!, $url: String!, $imageUrl: String!, $category: String!, $description: String!) {
    createLink(title: $title, url: $url, imageUrl: $imageUrl, category: $category, description: $description) {
      title
      url
      imageUrl
      category
      description
    }
  }
`

const Admin = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
    reset,
  } = useForm()

  const [createLink, { loading, error }] = useMutation(CreateLinkMutation, {
    onCompleted: () => reset()
  })

  const onSubmit = async data => {
    const { title, url, category, description } = data
    const imageUrl = `https://via.placeholder.com/300`
    const variables = { title, url, category, description, imageUrl }
    try {
      toast.promise(createLink({ variables }), {
        loading: 'Creating new link..',
        success: 'Link successfully created!ð',
        error: `Something went wrong ð¥ Please try again -  ${error}`,
      })

    } catch (error) {
      console.error(error)
    }
  }

  return (
    <div className="container mx-auto max-w-md py-12">
      <Toaster />
      <h1 className="text-3xl font-medium my-5">Create a new link</h1>
      <form className="grid grid-cols-1 gap-y-6 shadow-lg p-8 rounded-lg" onSubmit={handleSubmit(onSubmit)}>
        <label className="block">
          <span className="text-gray-700">Title</span>
          <input
            placeholder="Title"
            name="title"
            type="text"
            {...register('title', { required: true })}
            className="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
          />
        </label>
        <label className="block">
          <span className="text-gray-700">Description</span>
          <input
            placeholder="Description"
            {...register('description', { required: true })}
            name="description"
            type="text"
            className="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
          />
        </label>
        <label className="block">
          <span className="text-gray-700">Url</span>
          <input
            placeholder="https://example.com"
            {...register('url', { required: true })}
            name="url"
            type="text"
            className="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
          />
        </label>
        <label className="block">
          <span className="text-gray-700">Category</span>
          <input
            placeholder="Name"
            {...register('category', { required: true })}
            name="category"
            type="text"
            className="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
          />
        </label>

        <button
          disabled={loading}
          type="submit"
          className="my-4 capitalize bg-blue-500 text-white font-medium py-2 px-4 rounded-md hover:bg-blue-600"
        >
          {loading ? (
            <span className="flex items-center justify-center">
              <svg
                className="w-6 h-6 animate-spin mr-1"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path d="M11 17a1 1 0 001.447.894l4-2A1 1 0 0017 15V9.236a1 1 0 00-1.447-.894l-4 2a1 1 0 00-.553.894V17zM15.211 6.276a1 1 0 000-1.788l-4.764-2.382a1 1 0 00-.894 0L4.789 4.488a1 1 0 000 1.788l4.764 2.382a1 1 0 00.894 0l4.764-2.382zM4.447 8.342A1 1 0 003 9.236V15a1 1 0 00.553.894l4 2A1 1 0 009 17v-5.764a1 1 0 00-.553-.894l-4-2z" />
              </svg>
              Creating...
            </span>
          ) : (
            <span>Create Link</span>
          )}
        </button>
      </form>
    </div>
  )
}

export default Admin

export const getServerSideProps = async ({ req, res }) => {
  const session = getSession(req, res)

  if (!session) {
    return {
      redirect: {
        permanent: false,
        destination: '/api/auth/login',
      },
      props: {},
    }
  }

  return {
    props: {},
  }
}
```

onSubmit é¢æ°ã¯ããã©ã¼ã ã®å¤ã createLink ãã¥ã¼ãã¼ã·ã§ã³ã«æ¸¡ãã¾ãããã¥ã¼ãã¼ã·ã§ã³ãå®è¡ãããã¨ãæåãã­ã¼ããã¨ã©ã¼ã®ããããã®ãã¼ã¹ããè¡¨ç¤ºããã¾ãã

getServerSidePropsã§ã¯ãã»ãã·ã§ã³ããªãå ´åãã¦ã¼ã¶ãã­ã°ã¤ã³ãã¼ã¸ã«ãªãã¤ã¬ã¯ããã¦ãã¾ããã­ã°ã¤ã³ããã¦ã¼ã¶ã¼ã®é»å­ã¡ã¼ã«ã¨ä¸è´ããã¦ã¼ã¶ã¼ã¬ã³ã¼ããè¦ã¤ãã£ãå ´åã/admin ãã¼ã¸ãã¬ã³ããªã³ã°ããã¾ãã

èªè¨¼ãããã¦ã¼ã¶ã¼ããªã³ã¯ãä½æããããã«ä½¿ç¨ã§ãã+ä½æãã¿ã³ãè¿½å ãã¦ãHeader.tsxãã¡ã¤ã«ãæ´æ°ãã¾ãã

```tsx
// components/Layout/Header.tsx
/** imports */

const Header = () => {
  const { user } = useUser()
  return (
    <header className="text-gray-600 body-font">
         {/* the rest of the header... */}
        <nav className="...">
          {user && (
            <div className="flex itemx-center justify-center mr-5 capitalize bg-blue-500 py-1 px-3 rounded-md text-white">
              <Link href="/admin">
                <a>
                  + Create
                </a>
              </Link>
            </div>
          )}
           {/* Login/ Logout button... */}
        </nav>
      </div>
    </header>
  )
}

export default Header
```

ããã§ããªã³ã¯ã®ä½æãã§ããããã«ãªãã¯ãã§ã ð

## ãã¼ãã¹ï¼ã¦ã¼ã¶ã¼ã®å½¹å²ã«å¿ãããã¼ã¸ã®ä¿è­·

ç®¡çèã¦ã¼ã¶ã®ã¿ããªã³ã¯ãä½æã§ããããã«ãããã¨ã§ãèªè¨¼ãå¼·åãããã¨ãã§ãã¾ãã

ã¾ããã¦ã¼ã¶ã¼ã®ã­ã¼ã«ããã§ãã¯ããããã«ãcreateLinkãã¥ã¼ãã¼ã·ã§ã³ãæ´æ°ãã¦ãã ããã

```ts
// graphql/types/Link.ts
export const CreateLinkMutation = extendType({
  type: 'Mutation',
  definition(t) {
    t.nonNull.field('createLink', {
      type: Link,
      args: {
        title: nonNull(stringArg()),
        url: nonNull(stringArg()),
        imageUrl: nonNull(stringArg()),
        category: nonNull(stringArg()),
        description: nonNull(stringArg()),
      },
      async resolve(_parent, args, ctx) {
        if (!ctx.user) {
          throw new Error(`You need to be logged in to perform an action`)
        }

        const user = await ctx.prisma.user.findUnique({
          where: {
            email: ctx.user.email,
          },
        });

         if (user.role !== 'ADMIN') {
          throw new Error(`You do not have permission to perform action`);
        }

        const newLink = {
          title: args.title,
          url: args.url,
          imageUrl: args.imageUrl,
          category: args.category,
          description: args.description,
        };

        return await ctx.prisma.link.create({
          data: newLink,
        });
      },
    });
  },
});
```

admin.tsxãã¼ã¸ãæ´æ°ããgetServerSidePropsã«ã­ã¼ã«ãã§ãã¯ãè¿½å ãã¦ãadminsã§ãªãã¦ã¼ã¶ããªãã¤ã¬ã¯ããã¾ããADMINã­ã¼ã«ãæããªãã¦ã¼ã¶ã¼ã¯ã/404ãã¼ã¸ã«ãªãã¤ã¬ã¯ãããã¾ãã

```tsx
// pages/admin.tsx
export const getServerSideProps = async ({ req, res }) => {
  const session = getSession(req, res);

  if (!session) {
    return {
      redirect: {
        permanent: false,
        destination: '/api/auth/login',
      },
      props: {},
    };
  }

  const user = await prisma.user.findUnique({
    select: {
      email: true,
      role: true,
    },
    where: {
      email: session.user.email,
    },
  });

  if (user.role !== 'ADMIN') {
    return {
      redirect: {
        permanent: false,
        destination: '/404',
      },
      props: {},
    };
  }

  return {
    props: {},
  };
};
```

ãµã¤ã³ã¢ããæã«ã¦ã¼ã¶ã¼ã«å²ãå½ã¦ãããããã©ã«ãã®ã­ã¼ã«ã¯USERã§ãããã®ããã/adminãã¼ã¸ã«ç§»åãããã¨ãã¦ãããã¯ãæ©è½ãã¾ããã

ãããå¤æ´ããã«ã¯ããã¼ã¿ãã¼ã¹åã®ã¦ã¼ã¶ã¼ã®ã­ã¼ã«ãã£ã¼ã«ããå¤æ´ãã¾ããããã¯Prisma Studioã§éå¸¸ã«ç°¡åã«è¡ãã¾ãã

ã¾ããã¿ã¼ããã«ã§npx prisma studioãå®è¡ããPrisma Studioãèµ·åãã¾ããæ¬¡ã«ãã¦ã¼ã¶ã¼ã¢ãã«ãã¯ãªãã¯ããç¾å¨ã®ã¦ã¼ã¶ã¼ã¨ä¸è´ããã¬ã³ã¼ããæ¢ãã¾ããããã§ãã¦ã¼ã¶ã¼ã®ã­ã¼ã«ãUSERããADMINã«æ´æ°ãã¦ãã ãããSave 1 change ãã¿ã³ãæ¼ãã¦ãå¤æ´ãä¿å­ãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/a36b9bfa50ec-20220619.png)

ã¢ããªã±ã¼ã·ã§ã³ã® /admin ãã¼ã¸ã«ç§»åãã¦ãåºæ¥ä¸ããã§ããããã§ãåã³ãªã³ã¯ãä½æãããã¨ãã§ãã¾ãã

# ã¾ã¨ãã¨æ¬¡ã®ã¹ããã
ãã®ãã¼ãã§ã¯ãAuth0ãä½¿ç¨ãã¦Next.jsã¢ããªã«èªè¨¼ã¨èªå¯ãè¿½å ããæ¹æ³ã¨ãAuth0 Actionsãä½¿ç¨ãã¦ãã¼ã¿ãã¼ã¹ã«ã¦ã¼ã¶ã¼ãè¿½å ããæ¹æ³ã«ã¤ãã¦å­¦ã³ã¾ããã

æ¬¡åã¯ãAWS S3ãä½¿ã£ãç»åã¢ããã­ã¼ãã®æ¹æ³ãå­¦ã³ã¾ãã®ã§ããæ¥½ãã¿ã«ã