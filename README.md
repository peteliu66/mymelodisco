# Melodisco

AI Music Player by [melodis.co](https://melodis.co)

## Live Demo

[https://melodis.co](https://melodis.co)

![dark](./public/previews/dark.png)

# Previews

![light](./public/previews/light.png)

![list](./public/previews/list.png)

![detail](./public/previews/detail.png)

## Deploy with Vercel

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fall-in-aigc%2Fmelodisco&env=POSTGRES_URL,STRIPE_PUBLIC_KEY,STRIPE_PRIVATE_KEY,NEXT_PUBLIC_SHARE_BASE_URL,NEXT_PUBLIC_GOOGLE_CLIENT_ID,GOOGLE_CLIENT_SECRET,NEXTAUTH_URL,NEXTAUTH_SECRET,NEXT_PUBLIC_WEB_BASE_URL,SENSITIVE_KEYWORDS&envDescription=POSTGRES_URL%20needed%20for%20the%20application&project-name=my-ai-music-project&repository-name=my-ai-music-project&redirect-url=https%3A%2F%2Fmelodis.co&demo-title=Melodisco&demo-description=AI%20Music%20Player&demo-url=https%3A%2F%2Fmelodis.co&demo-image=https%3A%2F%2Fraw.githubusercontent.com%2Fall-in-aigc%2Fmelodisco%2Fmain%2Fpublic%2Fpreviews%2Flight.png)

## Deploy with Docker

- build image

```shell
sudo docker build -f deploy/Dockerfile -t melodisco:latest .
```

- run server

```shell
sudo docker run -itd -p 127.0.0.1:8023:8080 --restart=always melodisco:latest
```

- nginx conf

```txt
server {
    listen 80;

    location / {
        proxy_pass http://127.0.0.1:8023/;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    error_log /var/log/nginx/melodisco.error;
}
```

## Local Development

1. clone project

```shell
git clone https://github.com/all-in-aigc/melodisco
```

2. install dependencies

```shell
cd melodisco
pnpm install
```

3. init database

create your database use [local postgres](https://wiki.postgresql.org/wiki/Homebrew) or [vercel-postgres](https://vercel.com/docs/storage/vercel-postgres) or [supabase](https://supabase.com/)

create tables from sql at `data/install.sql`

4. set environmental values

put `.env.local` under `melodisco` root dir with values list below

```
SENSITIVE_KEYWORDS=xxx,xxx,xxx

POSTGRES_URL=postgres://USERNAME:PASSWORD@HOST:PORT/melodisco

STRIPE_PUBLIC_KEY=pk_test_xxx
STRIPE_PRIVATE_KEY=sk_test_xxx

NEXT_PUBLIC_SHARE_BASE_URL=http://localhost:8023

NEXT_PUBLIC_GOOGLE_CLIENT_ID=xxx.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=GOCSPX-xxx

NEXTAUTH_URL=http://localhost:8023
NEXTAUTH_SECRET=xxx

NEXT_PUBLIC_WEB_BASE_URL=http://localhost:8023
```

5. local development

```shell
pnpm dev --port 8023
```

open `http://localhost:8023` for preview

## 简介

立项当初是想做 AI 版网易云音乐，收录了 30 万首 AI 歌曲。

实现了歌曲发现榜 / 流行榜 / 新歌榜 / 随机漫游 / 歌曲收藏 / 最近播放 / 歌曲导入 / 歌曲分享等功能。

原创音乐播放器组件，支持顺序播放 / 随机播放 / 单曲循环三种播放模式，可控制播放进度，可控制音量。

支持暗黑主题 / 多语言 / 谷歌登录 / Stripe 支付。

服务端渲染歌曲详情构建海量页面，关键词覆盖密度大，SEO 友好。

## 技术栈包含：

- nextjs + typescript 全栈开发
- tailwindcss + shadcn 前端组件
- google-one-tap 谷歌快捷登录
- next-auth 用户鉴权
- next-intl 多语言
- supabase + pg 数据读写
- stripe-js 网页支付

可一键部署到 Vercel，可通过 Docker 部署。

## Credit to

- [aiwallpaper](https://aiwallpaper.shop) for code reference
- [nextjs](https://nextjs.org/docs) for full-stack development
- [tailwindcss](https://tailwindcss.com/) for page building
- [shadcn/ui](https://ui.shadcn.com/docs/installation/next) for ui component
- [next-auth](https://next-auth.js.org/getting-started/example) for auth
- [next-intl](https://next-intl-docs.vercel.app/docs/getting-started) for multiple languages
- [stripe](https://stripe.com/docs/development) for payment
- [node-postgres](https://node-postgres.com/) for data processing

## See also

- [ThinkAny](https://thinkany.ai) AI Search Engine
- [HeyBeauty](https://heybeauty.ai) AI Virtual Try-On
- [GPTs Works](https://gpts.works) Third-Party GPTs Store

## Who am I

[I'm idoubi, a Full-stack-engineer](https://bento.me/idoubi)

if this project is helpful to you, buy me a coffee.

<a href="https://www.buymeacoffee.com/idoubi" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>
