# 网站结构说明

> 记录日期：2026-09-21  
> 网站地址：<https://fenixzhao1.github.io/>  
> 代码仓库：`fenixzhao1/fenixzhao1.github.io`

## 1. 总体架构

本网站是一个由 GitHub Pages 托管的 Jekyll 静态学术网站，基于 Academic Pages / Minimal Mistakes 3.4.2 的较早版本改造。当前工作分支为 `master`，远端仓库为 `https://github.com/fenixzhao1/fenixzhao1.github.io`。仓库中没有额外的 GitHub Actions 工作流，因此网站应由 GitHub Pages 的原生 Jekyll 流程构建和发布。

主要技术组成如下：

- 内容与配置：Markdown、HTML、YAML
- 模板：Liquid
- 样式：Sass/SCSS，经 `assets/css/main.scss` 汇总
- 脚本：JavaScript；最终站点加载 `assets/js/main.min.js`
- Ruby 依赖：`Gemfile` 中的 `github-pages`、`jekyll-feed`、`jekyll-sitemap` 等
- 前端主题：Minimal Mistakes 3.4.2

核心渲染关系为：

```text
_config.yml + _data/
        │
        ├── _pages/          → 首页及一级页面
        ├── _research/       → Research 页面列表及论文详情页
        ├── _teaching/       → Teaching 页面列表及课程详情页
        ├── _talks/          → Talks 内容（当前未加入主导航）
        └── _portfolio/      → Portfolio 内容（当前未加入主导航）
                    │
                    ▼
_layouts/ + _includes/ + _sass/
                    │
                    ▼
              GitHub Pages
```

## 2. 主要页面与路由

| 页面 | 源文件 | 网址 | 内容来源 |
|---|---|---|---|
| Home | `_pages/about.md` | `/` | 页面正文及 `_config.yml` 中的作者资料 |
| CV | `_pages/cv.md` | `/cv/` | 指向静态 CV PDF |
| Research | `_pages/research.md` | `/research/` | 遍历 `_research/` 集合，并按 `status` 分组 |
| Teaching | `_pages/teaching.html` | `/teaching/` | 遍历 `_teaching/` 集合 |
| Talks | `_pages/talks.html` | `/talks/` | 遍历 `_talks/` 集合；主导航目前关闭 |

主导航由 `_data/navigation.yml` 控制，目前仅显示：

1. CV
2. Research
3. Teaching

## 3. 核心目录与文件职责

```text
Website/
├── _config.yml              # 全站配置、作者资料、集合、默认布局、插件及网址
├── _config.dev.yml          # 开发环境补充配置
├── _data/
│   └── navigation.yml       # 顶部主导航
├── _pages/                  # 首页、CV、Research、Teaching 等聚合页面
├── _research/               # 每篇论文一个 Markdown 文件
├── _teaching/               # 每门课程或教学记录一个 Markdown 文件
├── _talks/                  # 报告与会议记录
├── _portfolio/              # 作品集条目；当前不在主导航中
├── _posts/                  # 主题自带或旧博客文章；当前不属于核心学术页面
├── _layouts/                # 页面骨架
├── _includes/               # 导航、侧栏、作者资料、论文列表项、页脚、SEO 等组件
├── _sass/                   # 站点样式模块
├── assets/
│   ├── css/main.scss        # Sass 总入口
│   └── js/main.min.js       # 站点加载的合并压缩脚本
├── images/                  # 头像及网站图片
├── files/                   # 可下载的论文、CV 等静态文件的推荐存放位置
├── markdown_generator/      # 批量生成内容文件的旧辅助工具
├── talkmap/                 # 报告地图相关资源；当前功能关闭
├── Gemfile                  # Jekyll / GitHub Pages Ruby 依赖
└── package.json             # 旧版主题的 JavaScript 构建配置
```

## 4. 模板与组件关系

- `_layouts/compress.html`：最外层 HTML 压缩包装。
- `_layouts/default.html`：全站基础页面，加载页头、导航、正文、页脚和 JavaScript。
- `_layouts/archive.html`：Home 以外的聚合列表页常用布局，包含左侧作者资料栏。
- `_layouts/single.html`：一般正文与单条内容详情页。
- `_layouts/talk.html`：报告详情页。
- `_includes/author-profile.html`：生成头像、姓名、简介与社交链接。
- `_includes/archive-single.html`：生成 Research 与 Teaching 中的单个列表项目。
- `_includes/masthead.html`：顶部导航。
- `_includes/head.html` 与 `_includes/seo.html`：页面元数据和 SEO。

`_config.yml` 的 `defaults` 会为不同内容类型自动指定布局和作者侧栏，因此多数 Markdown 文件只需维护 front matter 和正文。

## 5. 内容集合及字段

### Research

`_research/` 中每篇论文对应一个 Markdown 文件。现有文件通常包含：

```yaml
title: "Paper title"
collection: research
permalink: /research/stable-slug
date: 2026-01-01
venue: "Journal or status"
paperurl: "https://..."
author: Author list
status: published   # 或 working
```

`_pages/research.md` 先列出 `status: published`，再列出 `status: working`。每个条目的标题、作者、期刊或状态、年份及链接由 `_includes/archive-single.html` 统一渲染。

### Teaching

`_teaching/` 中每项课程记录对应一个 Markdown 文件。现有字段通常包括：

```yaml
title: "Course title"
collection: teaching
type: "Undergraduate course"
permalink: /teaching/stable-slug
venue: "Institution"
date: 2026-01-01
location: "City, Country"
```

`_pages/teaching.html` 会按集合顺序输出全部教学记录。

## 6. 当前内容清单

截至记录日，主要目录的文件数量如下：

| 目录 | 文件数 | 说明 |
|---|---:|---|
| `_pages/` | 19 | 包含核心页面及若干主题示例/旧页面 |
| `_research/` | 11 | 8 个公开条目：4 篇 Publications、4 篇 Working Papers；另保留 3 个不再发布的旧条目 |
| `_teaching/` | 6 | 东财主讲课程，已更新至 2026 年；不包含 UCSC TA 课程 |
| `_talks/` | 7 | 主导航未启用 |
| `_portfolio/` | 2 | 非核心内容 |
| `_posts/` | 5 | 非核心内容 |

网站内容已于 2026-09-21 按 2026 年 9 月版 CV 更新：

- Home 页已更新职位、研究领域、教育背景和联系方式。
- Research 页面仅显示 CV 中的 4 篇 Publications 和 4 篇 Working Papers，不显示 Work in Progress。
- Teaching 页面仅列出在东财担任主讲教师的课程，不列入 UCSC TA 课程。
- CV 页面指向 `files/Shuchen_Zhao_CV.pdf`。

## 7. 静态文件位置

- 当前头像：`images/Avatar.jpg`
- 当前 CV：`files/Shuchen_Zhao_CV.pdf`
- 2024 年旧版 CV 已从网站目录移除，可通过 Git 历史恢复。
- 论文或其他下载文件：`files/`

新版 CV 固定存放为 `files/Shuchen_Zhao_CV.pdf`，并由 `_pages/cv.md` 使用站点路径 `/files/Shuchen_Zhao_CV.pdf` 引用。这样可以避免文件名空格和相对路径带来的问题。

头像可直接覆盖 `images/Avatar.jpg`；若以后更换文件名，则需同时修改 `_config.yml` 中的 `author.avatar`。

## 8. 样式位置

- 全局样式入口：`assets/css/main.scss`
- 字体与尺寸变量：`_sass/_variables.scss`
- 作者侧栏及头像：`_sass/_sidebar.scss`
- Research / Teaching 列表项：`_sass/_archive.scss`
- 普通页面正文：`_sass/_page.scss`
- 本站局部定制：`_sass/_custom.scss`

当前头像源文件为 3024 × 4032 像素的纵向图片。`_sass/_custom.scss` 以原始比例显示桌面端肖像，并为移动端设置紧凑的纵向裁切，不直接拉伸图片。

Research 与 Teaching 的字号调整应限定在这两个页面或相应列表容器内，不宜修改全站基础字号，否则 Home、CV 和移动端阅读体验会一并受到影响。

## 9. 维护注意事项

- 保持现有页面层级和主导航结构；更新以内容与局部样式为主。
- 更新论文时尽量保留已有稳定 permalink，避免旧链接失效。
- 论文题目、作者顺序、状态、期刊信息和年份以最新 CV 为准；摘要和外部链接需另行核对。
- Work in Progress 不进入 Research 页面。
- `_posts/`、`_portfolio/` 和部分 `_pages/` 含有主题示例或旧内容，虽然未出现在主导航中，但可能被 sitemap 收录；后续可单独清理或设置为不输出。
- `_config.yml` 当前时区为 `America/Los_Angeles`，与现工作地点不一致；如无历史依赖，可改为 `Asia/Shanghai`。
- Google Universal Analytics 配置为空且已过时，可在后续清理。
- 本地环境当前未检测到可直接使用的 Ruby/Bundler，因此正式修改后至少应执行 YAML/front matter、内部链接和 Git diff 检查；如需本地完整预览，应先补齐 Jekyll 构建环境。
