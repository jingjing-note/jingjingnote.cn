# 精神殿堂：体验人间百味图书馆

> 个人博客 — 记录足迹、阅读、AI洞察与生活手记

## 🌟 项目简介

这是一个基于 [Hugo](https://gohugo.io/) 静态站点生成器搭建的个人博客，使用 [PaperMod](https://github.com/adityatelange/hugo-PaperMod) 主题，配备 [Decap CMS](https://decapcms.org/) 网页端编辑器，部署在 [Cloudflare Pages](https://pages.cloudflare.com/)。

## 📁 项目结构

```
blog-project/
├── hugo.toml                  # Hugo 主配置文件
├── content/
│   ├── _index.md              # 首页
│   ├── search/_index.md       # 搜索页
│   ├── archives/_index.md     # 归档页
│   └── posts/
│       ├── 足迹角/            # 游记、见闻、地域文化
│       ├── 阅读角/            # 书籍、电影、人物感悟
│       ├── ai发现室/          # AI串联体验与思考
│       └── 生活手记/          # 工作/生活真实记录
├── static/
│   ├── admin/
│   │   ├── index.html         # Decap CMS 入口
│   │   └── config.yml         # Decap CMS 配置
│   └── images/uploads/        # 上传图片目录
├── themes/PaperMod/           # PaperMod 主题（git submodule）
└── README.md                  # 本文件
```

## 📌 四个内容板块

| 板块 | 说明 | 分类名 |
|------|------|--------|
| 📌 足迹角 | 游记、见闻、地域文化 | 足迹角 |
| 📖 阅读角 | 读过的书、电影、人物感悟 | 阅读角 |
| 🤖 AI发现室 | 用AI串联足迹与阅读的新洞察 | ai发现室 |
| ✍️ 生活手记 | 工作/生活真实记录 | 生活手记 |

## 🚀 Cloudflare Pages 部署步骤

### 1. 推送代码到 GitHub

```bash
cd blog-project
git remote add origin https://github.com/jingjing-note/jingjingnote.cn.git
git add .
git commit -m "init: 精神殿堂博客项目"
git branch -M main
git push -u origin main
```

### 2. 在 Cloudflare Pages 创建项目

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. 进入 **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**
3. 选择 GitHub 仓库 `jingjing-note/jingjingnote.cn`
4. 配置构建设置：
   - **Framework preset**: `Hugo`
   - **Build command**: `hugo`
   - **Build output directory**: `public`
   - **Environment variables**: 添加 `HUGO_VERSION` = `0.147.8`
5. 点击 **Save and Deploy**

### 3. 绑定自定义域名（可选）

1. 在 Cloudflare Pages 项目设置中 → **Custom domains**
2. 添加 `jingjingnote.cn`
3. 按提示在 DNS 设置中添加 CNAME 记录

## ✏️ 使用 Decap CMS 写文章

### 首次配置 GitHub OAuth

Decap CMS 使用 GitHub 后端，需要配置 OAuth App：

1. 前往 GitHub → **Settings** → **Developer settings** → **OAuth Apps** → **New OAuth App**
2. 填写：
   - **Application name**: `精神殿堂 CMS`
   - **Homepage URL**: `https://jingjingnote.cn`
   - **Authorization callback URL**: `https://api.netlify.com/auth/done`
3. 获取 **Client ID** 和 **Client Secret**

> **注意**：如果部署在 Cloudflare Pages（非 Netlify），需要额外部署一个 OAuth 认证服务。推荐使用 [Decap CMS OAuth Server](https://github.com/sveltia/sveltia-cms-auth) 部署到 Cloudflare Workers，或切换使用 Sveltia CMS（兼容 Decap CMS 配置的替代方案，内置 OAuth 支持）。

### 使用 Sveltia CMS（推荐替代方案）

如果不想配置 OAuth 服务器，可以将 `static/admin/index.html` 替换为：

```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>内容管理 - 精神殿堂</title>
</head>
<body>
  <script src="https://unpkg.com/@sveltia/cms/dist/sveltia-cms.js"></script>
</body>
</html>
```

Sveltia CMS 兼容 Decap CMS 的 `config.yml`，且内置 GitHub OAuth 支持，无需额外部署认证服务。

### 写文章

1. 访问 `https://jingjingnote.cn/admin/`
2. 使用 GitHub 账号登录
3. 选择对应的板块（足迹角/阅读角/AI发现室/生活手记）
4. 点击 **新建** 开始写作
5. 写完点击 **发布**，会自动提交到 GitHub 仓库
6. Cloudflare Pages 检测到提交后自动重新构建部署

## 🔧 本地开发

### 前置要求

- [Hugo Extended](https://gohugo.io/installation/) v0.147.8+
- [Git](https://git-scm.com/)

### 启动本地服务器

```bash
# 克隆仓库（含子模块）
git clone --recurse-submodules https://github.com/jingjing-note/jingjingnote.cn.git
cd jingjingnote.cn

# 启动开发服务器
hugo server -D

# 浏览器访问 http://localhost:1313/
```

### 新建文章

```bash
# 足迹角
hugo new content posts/足迹角/文章标题.md

# 阅读角
hugo new content posts/阅读角/文章标题.md

# AI发现室
hugo new content posts/ai发现室/文章标题.md

# 生活手记
hugo new content posts/生活手记/文章标题.md
```

### 构建生产版本

```bash
hugo
# 输出在 public/ 目录
```

## 📝 文章模板

每篇文章的 front matter 格式：

```yaml
---
title: "文章标题"
date: 2026-06-26
draft: false
description: "文章摘要"
categories: ["足迹角"]   # 对应板块：足迹角 / 阅读角 / ai发现室 / 生活手记
tags: ["标签1", "标签2"]
---

正文内容...
```

## 🔄 更新主题

```bash
git submodule update --remote themes/PaperMod
```

## 📄 许可

博客内容版权归作者所有。
