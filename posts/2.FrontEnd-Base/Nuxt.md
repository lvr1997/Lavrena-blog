## 为什么要学？

一、提升技术面；二、😏

## NUXT是什么？

Nuxt 框架提供了一种基于 Node.js 的**服务端渲染方案 SSR（Server Side Rendering）**，可以让 Vue 应用在服务器端进行渲染，从而提高页面的加载速度和 SEO。

### 服务端渲染

什么是SSR？服务器端渲染，在**服务器端**生成 HTML 页面并发送给客户端。 什么是SPA? SPA（Single Page Application）单页面应用，在**客户端**通过 JS 动态地构建页面。

- SPA 的特点是页面切换流畅，动态渲染变化的部分，**用户体验好**，但是对搜索引擎的支持不够友好。
- SSR 的特点是对搜索引擎友好，可以提高页面**首次加载速度** 和 **SEO**，但是页面切换可能不够流畅，因为每次都是请求一个完整的 HTML 页面。

**开启或关闭服务端渲染** Nuxt 默认开启 SSR 服务端渲染，推荐开启，从而兼顾了 SSR 和 SPA 的优点，也利于 SEO 搜索引擎优化。

```tsx
// nuxt.config.ts
export default defineNuxtConfig({
  // 是否开启 ssr 服务端渲染  
  ssr: true
})
```

## 优点

**Nuxt 框架优势**

- Nuxt 采用了**混合的架构模式**，同时支持 SSR 和 SPA。
- SSR 服务端渲染： 首次访问页面 ，Nuxt.js 在服务器端执行 Vue 组件的渲染过程，并生成初始 HTML。
- SPA 客户端激活：一旦初始 HTML 被发送到浏览器，Vue.js 会接管页面，后续的页面切换则使用 SPA 的方式进行。
- Nuxt 框架优势：**兼顾了 SSR 和 SPA 的优点**。

## NUXT适用场景（可以用来做什么？）

企业网站、商品展示 等 C 端网站，对 SEO 搜索更友好，且页面切换流畅，用户体验更好。

## NUXT怎么用？

很简单~ 就三步🤭

### ①选择构建工具

我这里使用`pnpm`包管理器（因为没用过，所以想尝试）[[pnpm#pnpm安装|pnpm的安装]]

### ②创建 Nuxt3 项目

> 参考Nuxt官网 一步步安装 安装 · 快速入门 Nuxt

### ③安装依赖&启动

1. 进入项目目录，并安装项目依赖 `pnpm install`。
2. 启动项目，`pnpm dev`。
3. ✨ 浏览器访问 [](http://127.0.0.1:3000/)[http://localhost:3000](http://localhost:3000)

## Nuxt的路由系统

### 项目的目录结构

我们先来认识 Nuxt3 项目的目录结构。

```bash
├─.nuxt              非工程代码，存放运行或发行的编译结果
├─node_modules       项目依赖
├─public             网站资源目录
├─server             接口服务器目录 可以写后端接口在里面
├─.gitignore         git 忽略文件
├─.npmrc             npm 配置文件
├─app.vue            根组件
├─nuxt.config.ts     nuxt 配置文件
├─package.json       项目配置文件
├─README.md          项目说明文件
└─tsconfig.json      ts 配置文件
```

### 基于文件的路由系统

nuxt 有一些**约定的目录**，有特殊功能，如 **pages** 目录的 vue 文件会自动注册路由。

```bash
├─ pages             页面目录，自动注册路由
```

Nuxt.js 自带基于文件的路由系统，无需安装 **vue-router**，无需额外配置。

### 一个简单的路由案例

**参考目录**

```bash
├─ pages                   页面目录，自动注册路由
│  └─index/index.vue      主页
│  └─video/index.vue      视频页
├─app.vue                  根组件
```

**参考代码**
```html {3-4,6}
<template> 
	<!-- 路由链接 --> 
	<NuxtLink to="/">首页</NuxtLink> 
	<NuxtLink to="/video">视频页</NuxtLink> 
	<!-- 页面路由 --> 
	<NuxtPage /> 
</template>
```

- 页面路由 `<NuxtPage>` 相当于 `<RouterView>`
- 页面跳转 `<NuxtLink>` 相当于 `<RouterLink>`

## Nuxt实战

[[Nuxt3实现哔哩哔哩移动端实战]]