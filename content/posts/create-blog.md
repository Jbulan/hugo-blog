---
title: "创建一个博客" # 根据文件名自动生成标题
date: 2025-10-23T21:50:42+08:00 # 自动插入当前日期
lastmod: 2026-03-25T21:50:42+08:00 # 自动插入当前日期
author: "嚼不烂" # 预设的作者名

slug: "create-blog" # 为文章设置一个简短的英文 URL 片段
description: "创建一个简单的个人博客" # 文章摘要，用于 SEO 和社交分享

categories:
  - "技术教程" # 文章的主要分类
tags:
  - "博客" # 文章的关键词标签
  - "Hugo"
  - "Cloudflare"
  - "giscus"

draft: false # 默认发布状态
showToc: true # 默认显示目录
comments: true # 默认允许评论

cover:
  image: "https://img.jiaobulan.com/img/2025/10/0ffd7cb739f546a96611fb6a1d44239e.jpeg" # 封面图片 URL
  alt: "封面" # 图片的替代文本
  relative: false # 使用图床等外部图片时，此项必须为 false
  hiddenInList: false
  hiddenInSingle: false
---

**创建、部署一个属于自己的博客是有趣的并且是有意义的。** 之所以这么说，是因为在创建个人博客的过程中，你会学习到各种常见平台、工具，这其中就包括支撑本博客的 [Hugo](https://gohugo.io/)、[Cloudflare](https://www.cloudflare.com/) 以及 [Giscus](https://giscus.app/)（~~当然以上都是在没有充足资金下的暂时选择~~），此外还要感谢 Gemini 对本项目的大力支持🫡🫡。

## 一、博客的基本构成

博客，或者说网站主要分为静态和动态两种。

其中**动态网站**是指，在服务器后端运行有代码和数据库来实时生成页面，以此完成与浏览器的交互。搭建一个动态网站通常需要一个**内容管理系统 CMS**，例如 WordPress (PHP)、Ghost (Node.js)、Drupal (PHP)；选择一种 **Web 框架**，例如 Django (Python)、Ruby on Rails (Ruby)、Laravel (PHP)；部署一个**数据库**，如 MySQL、PostgreSQL、MongoDB；配置各种**服务器环境**，像是常见的 **LAMP/LNMP:** Linux (操作系统)、Nginx/Apache (Web 服务器)、MySQL (数据库)、PHP/Python/Node.js (后端语言)；除此之外，还有以上软件运行的基础 --- **主机/服务器:** 虚拟主机 (Shared Hosting) 或者 **VPS** (如 DigitalOcean, Vultr) 以及 PaaS (如 Heroku)。以上的这些都是初步需要准备的，自己动手搭建一个动态博客最难的还是后期维护，因此即使动态网站有着强大的功能和高自由度，它还是不适合作为个人博客，至少是不适合技术小白的。

与之相对的，**静态网站**就显得“亲民”了许多：轻量、极速、安全、廉价（~~最重要的还是廉价~~）。静态博客的工作流程是：开发者在本地编写文章 -> 博客生成器将你的文章套入预设的主题模板 -> 托管平台将完整的网站呈现在网络上 -> 用户通过链接访问，在这其中需要的费用以及精力是无限接近于零的（甚至可以做到完全免费）。

### 静态博客

与动态博客相似，静态博客也需要**内容**、**模板/主题**、**生成/管理系统**、**托管/部署**、**互动功能**。其中常见的工具包括：**SSG (静态站点生成器):** **Hugo** (Go)、Jekyll (Ruby)、Hexo (Node.js)、Next.js / Gatsby (React) 来进行内容管理，**文件系统 (File System):** 即 Markdown (`.md`) 文件或是 HTML 文件来存储内容，**静态托管平台 (JAMstack):** **Cloudflare Pages**、GitHub Pages、Netlify / Vercel、AWS S3 / 阿里云 OSS 来部署你的博客，除此之外还有 **Giscus** (GitHub Discussions)、Gitalk (GitHub Issues)、Disqus、Valine 来提供评论，**Cloudflare R2**、AWS S3 提供图床，以及等等其他的软件、平台、组件来丰富你的博客（~~个人博客的一大乐趣就在于此：永远没有止境，你可以无限地丰富你的博客~~）。

## 二、搭建一个简单的个人博客

一个个人博客的起点通常是**静态站点生成器 (Static Site Generator, SSG)。**

### Hugo

![Hugo](https://blog.dejavu.moe/posts/how-i-built-my-personal-blog/hugo-logo-wide.svg)

静态站点生成器有很多种，像是插件丰富的 Hexo、创新性的 Astro、以及经典的 Jekyll，但是最受欢迎的仍然是 Hugo：

* **构建快:** Hugo 是用 Go (Golang) 语言编写的，Go 是编译型语言，执行效率远高于 Jekyll (Ruby) 和 Hexo (Node.js) 这样的脚本语言；
* **安装简单:** Hugo 编译后是一个单一的二进制可执行文件，而不像 Jekyll 和 Hexo 需要先安装一个完整的环境（如 Ruby + RubyGems 或 Node.js + npm）；
* **内置功能:** Hugo 内部集成了许多高级功能，像是**图片处理**、**多语言支持(i18n)**、**Shortcodes** 等等，高效、轻量。

| **特性/SSG**   | **Hugo**                                                     | **Hexo**                                                     | **Astro**                                                    |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **核心技术**   | **Go 语言**                                                  | **Node.js**                                                  | **Node.js**                                                  |
| **构建速度**   | **极快 (Blazing Fast)**。这是 Hugo 最著名的优点。对于拥有数千篇文章的大型网站，构建时间也通常在秒级。 | **较慢**。由于基于 Node.js，在处理大量文件时，其 I/O 和处理速度远不及 Hugo。项目变大后构建速度会明显变慢。 | **快**。构建速度优于 Hexo，但通常仍慢于 Hugo。它的优化重点在于前端加载性能而非纯粹的构建速度。 |
| **依赖与安装** | **无依赖**。下载一个二进制可执行文件即可运行，跨平台部署非常简单。 | **需要 Node.js 环境**和 npm/yarn 包管理器，需要安装一系列 `node_modules`。 | **需要 Node.js 环境**，通过 npm/yarn/pnpm 进行项目初始化和管理。 |
| **学习曲线**   | **较陡峭**。其模板语法 (Go Templates) 功能强大但与其他主流模板引擎差异较大，需要专门学习。 | **平缓**。对于熟悉 JavaScript 和 Node.js 的开发者非常友好，插件系统也易于上手。 | **中等**。如果了解现代前端框架 (React, Vue, Svelte 等)，学习 Astro 会非常快。它允许在 Astro 组件中使用熟悉的框架语法。 |
| **灵活性**     | **高**。提供了强大的分类系统 (Taxonomies)、图片处理 (Hugo Pipes) 等内置功能，但扩展通常需要深入理解其模板系统。 | **极高**。拥有庞大的插件生态系统，可以通过 npm 安装各种插件来快速扩展功能，定制性很强。 | **非常高**。其“组件岛 (Islands)”架构是核心亮点，允许在静态页面中嵌入独立的、按需加载的交互式组件，完美结合了静态站的速度和动态应用的交互性。 |

#### 安装部署 Hugo

1. **安装 Hugo**  
   Hugo 有两种安装方式：

   * **使用包管理器安装（推荐)**  
     前提：Windows 电脑上安装了 `winget`（Windows 11/10 自带）或 `Chocolatey`。

     * 使用 **winget（推荐) :** 打开 `PowerShell` 或 `Windows 终端`，执行：

       ```powershell
       winget install Hugo.Hugo.Extended
       ```

     * 使用 **Chocolatey:** 打开 `PowerShell` (管理员权限)，执行：

       ```powershell
       choco install hugo-extended
       ```

   * **手动下载**
     1. 前往 Hugo 的 [GitHub Releases 页面](https://github.com/gohugoio/hugo/releases)。
     2. 找到最新的版本，在 "Assets" 里下载名为 `hugo_extended_..._windows-amd64.zip` 的压缩包。
     3. 解压它，得到一个 `hugo.exe` 文件。
     4. 在合适的地方创建一个文件夹（例如 `D:\Hugo\bin`），把 `hugo.exe` 放进去。
     5. **重要：**  
        将这个文件夹 (`D:\Hugo\bin`) 添加到系统**环境变量 (PATH)** 中。
        * *方法：* 搜索 "编辑系统环境变量" -> "环境变量" -> 在 "系统变量" 或 "用户变量" 里找到 `Path` -> "编辑" -> "新建" -> 粘贴文件夹路径 `D:\Hugo\bin`。

    **验证安装：** 打开一个新的 `PowerShell` 终端，输入：

    ```powershell
    hugo version
    ```

    如果看到类似 `hugo v0.15x.x ... extended ...` 的输出，说明安装成功。

1. **创建你的博客站点**
   1. 打开 `PowerShell` 终端。
   2. `cd` 到预计存放博客的目录（例如 `D:\Web`）。
   3. 运行命令，创建一个名为 `Blog` 的新站点：

      ```powershell
      hugo new site Blog --format yaml
      ```

   4. 进入这个新创建的目录：

      ```powershell
      cd Blog
      ```

> **备注：** 创建 Hugo 新站点的完整命令是 `hugo new site <path> [flags]` ，其中在 `flags` 处可以指定三种配置格式：**YAML**, **TOML**, **JSON**

* **TOML (Tom's Obvious, Minimal Language)**  
  TOML 是 Hugo **传统上的默认格式**。它被设计为一种极简的、易于人类阅读的配置文件格式。  
  **语法核心：** 键值对 (`key = "value"`) 和“表” (sections，使用 `[tables]`)。
* **YAML (YAML Ain't Markup Language)**  
  YAML 是一种以**缩进**为中心的配置语言。它在云原生（如 Kubernetes, Docker Compose）和自动化（如 Ansible）领域非常流行。  
  **语法核心：** 键值对 (`key: value`)、缩进（表示层级）和短横线 (`-`)（表示列表）。
* **JSON (JavaScript Object Notation)**  
  JSON 是一种主要为**机器间通信**设计的数据交换格式。虽然 Hugo 支持它，但它几乎不被用作手动的配置文件。  
  **语法核心：** 大括号 `{}` (对象)、方括号 `[]` (数组)、严格的键值对 (`"key": "value"`)。

#### 添加博客主题

博客的外观由主题决定。需要先初始化 Git，然后以“子模块”的方式添加主题（这是最佳实践，方便未来更新）。

1. **初始化 Git 仓库**

   ```powershell
   git init
   ```

2. **添加主题**  
   这里以我目前的主题 `PaperMod` 为例。你可以在 [Hugo 官网主题页](https://themes.gohugo.io/) 找到你喜欢的。

   ```powershell
   git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
   ```

3. **配置主题**  
   打开博客根目录下的 `hugo.yaml` 文件，用 VSCode 等代码编辑器打开。  
   在文件末尾添加一行，告诉 Hugo 使用这个主题：

   ```yaml
   theme: "PaperMod"
   ```

> **备注：** [PaperMod](https://github.com/adityatelange/hugo-PaperMod/) 是 Hugo 静态网站生成器中一个广受欢迎的主题。它以其简洁、快速和功能丰富的特点，成为了许多博客作者和技术爱好者的首选。

通过访问 **PaperMod** 的官方网站可以了解到 PaperMod 主题的一些特性以及基本用法：<https://adityatelange.github.io/hugo-PaperMod/>

![Hugo PaperMod](https://adityatelange.github.io/hugo-PaperMod/images/papermod-cover_hu_60d477562c9e7700.png)
简而言之，**PaperMod** 有以下的几个主要优点：

  1. **卓越的性能与速度**
     * **轻量级：** 主题本身非常轻量，没有臃肿的 JavaScript 或 CSS，加载速度极快。
     * **高分表现：** 在 Google PageSpeed Insights 和 Lighthouse 等性能评测工具中，PaperMod 搭建的网站通常能获得近乎满分的成绩，这对用户体验和 SEO 都至关重要。
  2. **简洁现代的响应式设计**
     * **极简主义：** 遵循“内容为王”的原则，界面干净、排版优雅，使读者能专注于内容本身。
     * **响应式：** 完美适配桌面、平板和移动设备，在所有屏幕尺寸上均有良好表现。
  3. **丰富且实用的内置功能**
     * **明暗模式 (Dark Mode)：** 内置一键切换的明暗主题，并且可以根据访问者的系统设置自动选择，这是现代网站的标配功能。
     * **内置搜索：** 支持基于 [Fuse.js](https://fusejs.io/) 的离线全文搜索，无需依赖第三方服务，响应迅速。
     * **SEO 优化：** 自动生成对搜索引擎友好的元标签（Meta Tags）、Open Graph 协议、Twitter Cards 以及 JSON-LD 结构化数据，有助于提高网站的搜索排名。
     * **代码高亮：** 支持服务端（Hugo 内置）和客户端（highlight.js）两种代码高亮方式，对技术博客非常友好。
     * **目录 (ToC)：** 可以为文章自动生成浮动或静态的目录，方便读者快速导航。
     * **归档与分类：** 自动生成漂亮的归档页面、标签（Tags）页面和分类（Categories）页面。
  4. **高度可配置与可扩展**
     * **社交链接：** 轻松在页眉或页脚配置指向 GitHub, LinkedIn, Twitter 等社交平台的图标链接。
     * **评论系统：** 支持集成 Giscus, utterances, Disqus, Commento 等多种第三方评论系统。
     * **自定义：** 允许用户通过自定义 CSS 和 JavaScript 轻松进行个性化调整，或通过覆盖模板 (template overrides) 来实现更深度的定制。
     * **多语言支持：** 良好地支持 Hugo 的多语言模式。
  5. **活跃的社区与维护**
     * PaperMod 是从已停止维护的 `paper` 主题复刻（fork）而来，并由其维护者 [Aditya Telange](https://github.com/adityatelange) 持续活跃地开发和维护，能及时修复问题并增加新功能。

#### 编写博客文章

1. **创建第一篇文章**
   1. 在 `PowerShell` 中运行命令：

      ```powershell
      hugo new content posts/hello/index.md
      ```

   2. 这会在 `content/posts/` 目录下创建一个 `hello/index.md` 文件。
   3. 用 VSCode 或其他编辑器打开这个文件，可以看到：

      ```powershell
      ---
      title: "Hello"
      date: 2025-10-24T12:30:00+09:00
      draft: true
      ---

      在这里开始写你的正文...
      ```

   4. **注意 `draft: true`**：`draft`（草稿）状态的文章默认不会显示。

> **备注：** 在这里提到了两个相关概念：Hugo 的 [Page Bundle](https://gohugo.io/content-management/page-bundles/) 模式，以及文章的默认模板（Front Matter 字段）。

* **Front Matter 字段**  
   **Front Matter** 是在 Markdown 内容文件（如一篇文章）**最顶部**编写的，用于**定义页面元数据 (Metadata)** 的配置块。可以将其理解为“关于内容的数据”，Hugo 读取这些字段，以决定如何渲染页面、在列表中的显示方式、页面的 SEO 信息、是否为草稿等。  
   在 PaperMod 的官方站点可以查看所有支持的 Front Matter 配置：<https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-variables/>

  * **格式：** Front Matter 可以使用三种格式：
     1. **YAML:**  
        使用 `---`作为分隔符（在创建 Hugo 新站点时设置）。
     2. **TOML:**  
        使用 `+++`作为分隔符（Hugo 默认配置文件的格式）。
     3. **JSON:**  
        使用 `{` 和 `}` 作为分隔符。

  * **作用：** 它存储了所有无法（或不适合）放在正文内容 (Markdown) 中的信息。
  * **示例：** `title` (标题), `date` (日期), `draft` (是否为草稿), `tags` (标签) 都是 Front Matter 字段。主题（如 PaperMod）也会定义许多它们自己独有的字段（如 `cover`, `showToc`）。
* **文章的默认模板 (Archetype)**  
   **Archetype**（直译为“原型”，在 Hugo 中常称为“内容模板”）是一个**预定义的内容文件模板**。  
   使用 `hugo new <路径>/<文件名>.md` 命令创建新文章时，Hugo 会在 `D:\Web\Blog\archetypes` 查找一个对应的 Archetype 文件，并使用它来**自动填充新文件的 Front Matter**。

  * **目的：** 确保内容的一致性、标准化，并省去每次都手动输入相同字段（如 `author`, `comments: true`）的麻烦。
* **自定义文章默认模板**
  * Hugo 自带有一个默认模板 `default.md`：

     ```markdown
     ---
     date: '{{ .Date }}'
     draft: true
     title: '{{ replace .File.ContentBaseName "-" " " | title }}'
     ---
     ```

     这是 Hugo 最基础的 Archetype。

    * `date: '{{ .Date }}'`: 自动插入当前日期和时间。
    * `title: '{{ ... }}'`: 这是一个 Hugo 模板函数。它会获取创建文章命令中的文件名（例如 `hello`），将其中的连字符 `-` 替换为空格，然后将每个单词的首字母大写（例如 `Hello`），并将其设为标题。
    * `draft: true`: 默认情况下，所有新内容都被设为“草稿”。这意味着在运行 `hugo`（生产环境构建）时，这篇文章**不会**被包含在网站中，必须在文章中手动将其改为 `draft: false` 才能发布。这是一个安全机制，防止未完成的文章被意外发布。
  * 但是这个模板有些过于简单，PaperMod 的许多特性都未被配置。我们可以在 `D:\Web\Blog\archetypes` 下新建一个 `posts.md` 来自定义文章模板：

     ```markdown
     title: "{{ replace .Name "-" " " | title }}" # 根据文件名自动生成标题
     date: {{ .Date }} # 自动插入当前日期
     lastmod: {{ .Date }} # 自动插入当前日期
     author: "嚼不烂" # 预设的作者名

     slug: "" # 为文章设置一个简短的英文 URL 片段
     description: "" # 文章摘要，用于 SEO 和社交分享

     categories:
       - "" # 文章的主要分类
     tags:
       - "" # 文章的关键词标签

     draft: false # 默认发布状态
     showToc: false # 默认不显示目录
     comments: true # 默认允许评论

     cover:
       image: "" # 封面图片 URL
       alt: "" # 图片的替代文本
       caption: "" # 填写图片的说明（可选）
       relative: false # 使用图床等外部图片时，此项必须为 false
     ```

     当然，你完全可以参考[PaperMod 的官方站点](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-variables/)来决定是否配置这些 Front Matter。  
     此外，还需要特别说明的是，Archetype 模板中有一些特性是需要和 hugo 的配置文件 `hugo.yaml` 相互配合的，这部分内容将会在后面的章节详细说明。

* **Page Bundle (页面包)**  
   **Page Bundle (页面包)** 是一种内容组织方式，它将一篇文章的 Markdown 文件与其**相关资源**（如图片、附件、数据文件）**组织在同一个目录中**。这与传统的“扁平”模式（所有图片放在 `/static/images/`，所有文章放在 `/content/posts/`）相对。  
   **Page Bundle 的类型：**

   1. **Leaf Bundle (叶子包)**:
      * **结构：** 一个目录，其中**必须包含**一个 `index.md` 文件。
      * **示例：** `content/posts/hello/index.md`
      * **用途：** 用于**单篇文章**。目录 `hello` 中包含的任何其他文件（如 `image1.jpg`, `chart.png`）都会成为该页面的“页面资源”。
   2. **Branch Bundle (分支包)**:
      * **结构：** 一个目录，其中**必须包含**一个 `_index.md` 文件。
      * **示例：** `content/posts/_index.md`
      * **用途：** 用于**列表页/分区页**（例如，显示所有文章的列表页）。

   对于文章而言，我们主要关注 **Leaf Bundle** 。在前面的章节中，我们创建新文章时使用的就是 Leaf Bundle 结构。  
   使用 Page Bundle（特别是 Leaf Bundle）模式有很多好处，它被认为是 Hugo 的现代最佳实践：

   1. **资源共置 (Co-location) 和便携性**
      * **优点：** 文章中引用的所有图片都和 `index.md` 文件放在一起。当重命名、移动或删除一篇文章时，只需操作**一个文件夹**即可。
      * **对比：** 在传统模式下，如果删除了 `content/posts/hello.md`，还必须记得到 `/static/images/` 目录中去删除 `image.jpg`，否则它会成为“孤儿”文件。
   2. **清晰的内容感知链接**
      * **优点：** 在 `index.md` 中，可以直接使用相对路径引用资源，非常直观。
      * **示例：** `![我的图片](./image1.jpg)`
   3. **启用 Hugo 强大的图像处理功能**
      * **这是最大的好处。** 放在 `/static` 目录下的图片是“静态”的，Hugo 不会处理它们。
      * **优点：** 只有当图片作为 **Page Resource**（即放在 Page Bundle 目录中）时，Hugo 才能对其进行动态处理。
      * **功能：** 可以在模板中对 `image1.jpg` 进行裁切 (Crop)、缩放 (Resize)、转换为 WebP 格式、获取 EXIF 数据、调整质量等。这对于优化网站性能和实现复杂的图片布局（如相册）至关重要。
   4. **内容范围限定 (Scoping)**
      * **优点：** `hello` 目录下的 `image.jpg` 只属于该文章。可以在另一篇文章 `create-blog` 目录下也放一个 `image.jpg`，它们不会冲突。
      * **对比：** 在 `/static` 模式下，所有图片共享一个全局命名空间，容易发生文件名冲突。

   **总结：** Page Bundle 模式让内容管理更像一个个独立的“项目”，使资源管理（尤其是图片）变得极其方便，并且解锁了 Hugo 强大的内置图像处理能力。  
   (~~在后面配置图床服务后，这种资源完全存储在本地的做法又会被抛弃，毕竟还是会占用一定的空间~~)

1. **启动本地服务器 (预览)**
   1. 在博客根目录 (`Blog`) 下，运行：

      ```powershell
      hugo server -D
      ```

      * `hugo server`：启动 Hugo 内置的 web 服务器。
      * **`-D`** 或 `--buildDrafts`：一个附加的参数，意思是“**包括草稿**”。(因为新文章默认是草稿，不加 `-D` 就看不到它)。
   2. `PowerShell` 会显示：

       ```powershell
       Built in 1220 ms
       Environment: "development"
       Serving pages from disk
       Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
       Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
       Press Ctrl+C to stop
       ```

   3. 打开浏览器，访问 `http://localhost:1313/`，就能看到你的博客和创建的文章了。

   **在写作时，保持这个 `hugo server -D` 窗口打开。每次修改并保存 Markdown 文件，Hugo 都会自动重新构建，浏览器也会自动刷新，实现实时预览。**

2. **正式构建**  
   当你写完文章后，就需要**正式构建**。

   1. 将文章 `index.md` 里的 `draft: true` 改成 `draft: false` (前面已经默认设置为 false 了)。
   2. 运行构建命令：

      ```powershell
      hugo
      ```

   3. Hugo 会生成一个 `public/` 文件夹，这里面就是个人博客的全部静态文件 (HTML/CSS/JS)。

> **备注：** 到这一步，Hugo 个人博客就算正式搭建成功了。未来你只需要专注于编写博客文章：写作时运行 `hugo server -D` 进行实时预览，写完后运行 `hugo` 正式构建即可。不过，这时的博客还比较粗糙，没有精美的页面、没有方便的交互，也没有一个可直接访问的域名。接下来的部分，就是一步步将它完善成一个更完整的网站。

#### 丰富博客功能

1. **hugo.yaml**  
   在 Hugo 站点目录下默认存在一个控制整个博客的配置文件 `hugo.yaml` (不同的 hugo 站点格式有不同的配置文件，上文已经说明过）  
   这是我目前的配置：

   ```yaml
   # =====================================================================================
   # 站点核心配置 (Core Site Configuration)
   # =====================================================================================

   baseURL: "https://jiaobulan.com/" # 站点域名
   title: "嚼不烂的个人博客" # 网站标题
   theme: PaperMod # 主题名称

   # 分页设置 (Hugo v0.128.0+ 使用新格式)
   pagination:
     pagerSize: 10 # 每页显示的文章数量

   # 语言与内容设置
   languageCode: "zh-cn" # 网站语言
   defaultContentLanguage: "zh-cn" # 默认内容语言
   # 完整启用中文翻译
   languages:
     zh-cn:
       languageName: "简体中文"
       languageDirection: "ltr"
       weight: 1
   hasCJKLanguage: true # 自动检测中日韩语言，优化字数统计和摘要
   enableEmoji: true # 启用 Emoji 表情支持
   enableGitInfo: true # 是否启用 Git 信息（如最后更新时间）

   # 构建行为设置
   enableRobotsTXT: true # 允许生成 robots.txt，引导搜索引擎抓取
   buildDrafts: false # 是否构建草稿
   buildFuture: false # 是否构建未来的文章
   buildExpired: false # 是否构建过期的文章

   # 永久链接配置
   permalinks:
     posts: "/posts/:slug/" # 为 posts 分区下的文章指定 URL 格式

   # =====================================================================================
   # 输出与性能 (Output & Performance)
   # =====================================================================================

   # 静态文件压缩
   minify:
     disableXML: true # 不压缩 XML 文件
     minifyOutput: true # 压缩最终输出的 HTML/CSS/JS 文件

   # 定义输出格式，为 RSS 和 JSON 搜索索引做准备
   outputs:
     home:
       - HTML
       - RSS
       - JSON # 为搜索功能生成索引
     section:
       - HTML
       - RSS

   # =====================================================================================
   # 主题参数配置 (Theme `params` Configuration)
   # =====================================================================================

   params:
     # --- 常规信息 ---
     env: production # 设置为 "production" 以启用 SEO、社交分享等功能
     title: "嚼不烂的个人博客" # 网站标题（可与顶层 title 保持一致）
     description: "人间有味是清欢。" # 网站描述，用于 SEO
     author: "嚼不烂" # 网站作者
     # keywords: [技术, 博客, 杂谈, Linux, 网络安全] # 关键词，大部分搜索引擎已不重视
     images: ["/img/website-cover.jpeg"] # 社交媒体分享时显示的预览图 (需将图片放在 /assets 目录下)
     DateFormat: "2006-01-02" # 全站日期格式

     # --- UI/UX 界面与功能 ---
     defaultTheme: auto # 默认主题模式: auto, dark, light
     disableThemeToggle: false # 是否显示主题切换按钮
     ShowReadingTime: true # 是否显示文章阅读时间
     ShowShareButtons: true # 是否显示社交分享按钮
     ShowPostNavLinks: true # 是否显示文章末尾的“上一篇/下一篇”导航
     ShowBreadCrumbs: true # 是否显示面包屑导航
     ShowCodeCopyButtons: true # 是否显示代码块的“复制”按钮
     ShowWordCount: true # 是否显示文章字数
     disableScrollToTop: false # 是否禁用“返回顶部”按钮
     comments: true # 是否全局启用评论系统 (可被文章页的设置覆盖)

     # --- 网站图标 (Favicon) ---
     # 图标在 static 目录下
     # assets:
     #   favicon: "/favicon.ico"
     #   favicon16x16: "/favicon-16x16.png"
     #   favicon32x32: "/favicon-32x32.png"
     #   apple_touch_icon: "/apple-touch-icon.png"

     # --- 网站左上角 Logo 或文字 ---
     label:
       text: "嚼不烂的个人博客" # 不使用图片 Logo，将显示此文字
       # icon: "/img/logo.png" # 图片 Logo 路径 (需放在 /assets 目录下)
       # iconHeight: 35

     # --- 主页样式 ---
     # homeInfoParams 模式 (默认启用)
     homeInfoParams:
       Title: "斯文在兹。"
       Content: "这里是「嚼不烂的个人博客」，一个记录技术探索、学习笔记和奇思妙想的地方。"

     # profileMode 模式 (个人简介卡片模式，如需使用将 enabled 设为 true)
     profileMode:
       enabled: false
       title: "嚼不烂"
       subtitle: "技术探索 | 学习笔记 | 奇思妙想"
       imageUrl: "/img/avatar.png" # 头像路径 (需放在 /assets 目录下)
       imageWidth: 120
       imageHeight: 120
       buttons:
         - name: 文章
           url: "/archives"
         - name: 关于
           url: "/about"

     # --- 社交链接 ---
     socialIcons:
       - name: github
         url: "https://github.com/Jbulan"
       - name: email
         url: "mailto:yourname@example.com"
       - name: bilibili
         url: "https://space.bilibili.com"
       # - name: x
       #   url: "https://x.com/<你的用户名>"

     # --- 文章与 SEO ---
     cover: # 文章封面图设置
       hidden: true # 在列表中和文章页隐藏封面图，但为 SEO 保留
       hiddenInList: true # 在列表页隐藏封面图
       hiddenInSingle: true # 在文章页隐藏封面图

     # editPost: # 在文章页显示“编辑此页”的链接
     #   URL: "https://github.com/Jbulan/Hugo-Blog/content"
     #   Text: "在 GitHub 上编辑"
     #   appendFilePath: true

     # --- 搜索功能 (Fuse.js) ---
     fuseOpts:
       isCaseSensitive: false # 搜索时是否区分大小写
       shouldSort: true # 是否根据匹配度对搜索结果进行排序
       location: 0 # 控制“模糊搜索”的程度
       distance: 1000
       threshold: 0.4
       minMatchCharLength: 0 # 最小匹配字符数
       keys: ["title", "permalink", "summary", "content"] # 在文章的哪些字段里进行搜索

   # =====================================================================================
   # 导航菜单 (Navigation Menu)
   # =====================================================================================

   menu:
     main:
       - identifier: archives
         name: 归档
         url: /archives/
         weight: 10
       - identifier: tags
         name: 标签
         url: /tags/
         weight: 20
       - identifier: search
         name: 搜索
         url: /search/
         weight: 30
       - identifier: about
         name: 关于
         url: /about/
         weight: 40

   # =====================================================================================
   # Markdown 与代码高亮 (Markdown & Syntax Highlighting)
   # =====================================================================================

   markup:
     # Hugo 内置的 Chroma 代码高亮配置
     highlight:
       noClasses: false # 建议为 false，以便使用 CSS 主题
       # codeFences: true # 启用通过 ``` (三个反引号) 来创建代码块的功能
       # guessSyntax: true # 没有指定代码语言时是否让 Hugo 尝试猜测语言
       lineNos: true # 是否在代码块左侧显示行号
       style: monokai # 代码高亮的颜色主题

     # Markdown 渲染器配置
     goldmark:
       renderer:
         unsafe: true # 允许在 Markdown 中使用原始 HTML

     # 目录 (Table of Contents) 配置
     tableOfContents:
       startLevel: 2 # 从 H2 标题开始生成目录
       endLevel: 4 # 到 H4 标题结束
       ordered: false # 使用无序列表 (圆点)

   # =====================================================================================
   # 隐私与服务 (Privacy & Services)
   # =====================================================================================
   # 增强隐私保护，禁用可能追踪用户的第三方服务

   privacy:
     vimeo:
       disabled: true
     twitter:
       disabled: true
     instagram:
       disabled: true
     youtube:
       disabled: true
   ```

> **备注：**
>
> * **baseURL** 是博客的主域名，在后文购买域名后可以为站点配置合适的域名。
> * **enableGitInfo** 在后文将博客部署到 GitHub 后将会起作用。
> * **posts** 配合前文配置的文章默认 Front Matter 中的 **slug**，可以实现自定义文章链接，而不是默认的文章标题链接，方便以后修改。
> * **outputs** 中的 `JSON` 负责让 Hugo 在构建时生成一个包含所有文章数据的 `index.json` 索引文件。后面的 **params.fuseOpts** 则是告诉 PaperMod 主题的搜索脚本（Fuse.js）如何使用这个 `index.json` 文件，例如搜索哪些字段、模糊匹配的程度等。两者配合实现搜索功能。
> * **comments** 以及文章 Front Matter 中的 **comments** 项控制开启评论功能，后续还要额外配置评论工具。

1. **菜单项**  
   在 `hugo.yaml` 中已经定义了各个菜单项，但 Hugo 需要知道当用户点击这些链接时该显示什么，也就是要创建相对应的页面文件。

   * 在 hugo 站点目录的 `content` 目录下创建 **markdown** 文件 `about.md`、`archives.md`、`search.md` 来作为各个菜单页面
   * `url: /about/` (常规内容页)
     * **对应文件：** `content/about.md`
     * **目的：** 一个标准的“关于我”页面。
     * **文件内容：** 这是最简单的页面。只需在 Front Matter 中设置标题，然后在下面直接编写 Markdown 内容即可。

       ```yaml
       ---
       title: "关于我"
       layout: "page"
       url: "/about/"
       ---

       你好，我是嚼不烂。

       一名计算机科学与技术专业的学生...
       ```

   * `url: /archives/` (PaperMod 特殊布局)
     * **对应文件：** `content/archives.md`
     * **目的：** 显示一个包含所有文章的、按年份归档的列表。
     * **文件内容：** 这个文件**不需要正文**。只需要在 Front Matter 中使用 `layout: "archives"` 来告诉 PaperMod 主题该页面为“归档”页面。

       ```yaml
       ---
       title: "文章归档"
       layout: "archives"
       url: "/archives/"
       summary: archives
       ---
       ```

   * `url: /search/` (PaperMod 特殊布局)
     * **对应文件：** `content/search.md`
     * **目的：** 显示一个搜索框和结果区域。
     * **文件内容：** 与 `archives.md` 类似，这个页面也依赖 PaperMod 的特殊布局。

       ```yaml
       ---
       title: "搜索"
       layout: "search"
       url: "/search/"
       summary: search
       ---
       ```

   * `url: /tags/` (Hugo 自动生成)
     * **对应文件：** **不需要创建文件**
     * **目的：** 显示一个包含所有“标签”的列表（或云）。
     * **工作原理：**
       * `tags` (标签) 和 `categories` (分类) 是 Hugo 的 **Taxonomy (分类法)**。
       * 只要在任何一篇文章的 Front Matter 中使用了 `tags: ["技术", "Linux"]`，Hugo 就会**自动**创建 `/tags/` 页面和 `/tags/技术/`、`/tags/linux/` 等子页面。
       * **注意：** **不要**创建 `content/tags.md` 文件。如果创建了该文件，它将**覆盖** Hugo 自动生成的标签列表页，导致功能失效。

> **备注：** 此时 `content` 目录下应该为这样的结构：

```text
content/
├── about.md
├── archives.md
├── search.md
└── posts/
    ├── create-blog.md
    └── hello/
        └── index.md
```

1. **图标**  
   一个完整的网站需要图标：浏览器标签栏的图标、作为软件安装时的应用图标、苹果系统中的图标。图标有时是一个网站的象征或名片，一个具有代表性的图标能让他人快速分辨出你的网站。  
   或许制作一个完美的图标很难，并且不是人人都有设计能力，但是我们可以简单借助 [realfavicongenerator](https://realfavicongenerator.net/) 这样的工具来设计、生成出许多简易的图标。

   1. 在 `Drop your favicon image here` 框中选择 **Create a logo**
   2. 在 `logo maker` 选择一个合适的图标颜色带作为图标的主要文字和背景颜色
   3. 在图标中输入想显示的文字，也可以更改配色和大小
   4. 点击 `Prepare your favicon` 的 **Generate favicon** 按钮预览图标
   5. 在预览界面你可以看到设计的图标在各种场合下的效果（Browser、Google Result Page、Apple Touch Icon、Web App Manifest），并且可以设定背景颜色等要素。
   6. 在设定合适后选择 **Next**，看到 RealFaviconGenerator 为你提供了各种格式的详细图标配置说明（包括 HTML、React、Next.js、Ruby、Node CLI、Node、Gulp、Grunt、ASP.NET），一般选择 `HTML` 即可。在详细配置说明中，提供了图标包压缩包下载选项，以及 `extend_head` ，这些都是需要的。

   > 在图标包里有几个图片文件和配置文件，分别有不同的作用：
     * `favicon.ico`：**传统图标**。所有桌面浏览器都支持的最经典格式。
     * `favicon.svg`：**矢量图标**。现代浏览器（如 Firefox, Chrome）会优先使用它。它是矢量图，无限放大不失真，且可以支持深色/浅色模式。
     * `favicon-96x96.png`：**PNG 备用图标**。为不支持 `.ico` 或 `.svg` 的地方提供一个标准 PNG。
     * `apple-touch-icon.png`：**iOS 主屏幕图标**。当 iPhone 或 iPad 用户将你的网站“添加到主屏幕”时，显示的就是这个图标。
     * `web-app-manifest-*.png`：**Android 主屏幕图标**。与 `apple-touch-icon` 类似，但这是由 `site.webmanifest` 文件调用的，供 Android/Chrome “添加到主屏幕”时使用。
     * `site.webmanifest`：**Web 应用清单**。这是一个 JSON 配置文件 ，它告诉浏览器你的网站是一个“应用”，定义了它的名称、颜色、启动 URL 以及使用哪些图标（`192x192`, `512x512` 等）。

       ```json

         {
         "name": "MyBlog",
         "short_name": "Blog",
         "start_url": "/",
         "icons": [
           {
             "src": "/web-app-manifest-192x192.png",
             "sizes": "192x192",
             "type": "image/png",
             "purpose": "any"
           },
           {
             "src": "/web-app-manifest-192x192.png",
             "sizes": "192x192",
             "type": "image/png",
             "purpose": "maskable"
           },
           {
             "src": "/web-app-manifest-512x512.png",
             "sizes": "512x512",
             "type": "image/png",
             "purpose": "any"
           },
           {
             "src": "/web-app-manifest-512x512.png",
             "sizes": "512x512",
             "type": "image/png",
             "purpose": "maskable"
           }
         ],
         "screenshots": [
           {
             "src": "/img/screenshots/screenshot-desktop.png",
             "sizes": "1280x720",
             "type": "image/png",
             "form_factor": "wide",
             "label": "博客桌面版截图"
           },
           {
             "src": "/img/screenshots/screenshot-mobile.png",
             "sizes": "540x720",
             "type": "image/png",
             "form_factor": "narrow",
             "label": "博客移动版截图"
           }
         ],
         "theme_color": "#ffffff",
         "background_color": "#ffffff",
         "display": "standalone"
       }
       ```

       上面是我的 `site.webmanifest` 文件内容，其中各项解释为：

       ```json
       {
         "name": "MyBlog",
         "short_name": "Blog",
         /* "name"  是安装时显示的全名。
           "short_name"  是在主屏幕图标下方显示的短名称。
         */

         "start_url": "/",
         /* 当用户从主屏幕启动“应用”时，打开的页面 。*/

         "icons": [ ... ],
         /* 一个图标列表 。Android 等系统会根据需要选择最合适的图标。
           "purpose": "maskable" 意味着图标可以被安全地裁剪成圆形或圆角矩形。
           定义了 192x192 和 512x512 两种尺寸 。
         */

         "screenshots": [ ... ],
         /* 截图列表 ，用于在安装提示中向用户展示您的“应用”外观。
           定义了 "wide" (桌面版)  和 "narrow" (移动版)。
         */

         "theme_color": "#ffffff",
         "background_color": "#ffffff",
         /* "theme_color"  定义了浏览器 UI (如地址栏) 的颜色。
           "background_color"  定义了应用启动时“闪屏”的背景色。
         */

         "display": "standalone"
         /* "standalone"  告诉系统，当从主屏幕启动时，
           应在没有浏览器地址栏和按钮的“独立窗口”中打开，使其看起来像一个原生 App。
         */
       }
       ```

       * 其中 `screenshots` 项需要在电脑端以及移动端分别为博客网站截图，将截图放在 `static` 目录下合适的位置，例如 `/img/screenshots/screenshot-mobile.png` 和 `/img/screenshots/screenshot-desktop.png` 。
       * 在 `icons` 项配置了两次 web-app-manifest 图标，是为了满足 Web APP 图标的不同要求。
       * 在浏览器按 `F12` 打开开发人员模式，选择 `应用程序` 页面可以查看预览你的 site.webmanifest 是否配置合适。

    > 将所有这些图标文件 和 `site.webmanifest`  放在 `static/` 根目录下，这是 Hugo 的标准做法。在 Hugo 构建网站时，它会将 `static/` 目录下的所有内容**原封不动**地复制到网站的**根目录**（例如 `public/`）。

   * 在 `layouts/partials` 目录下创建 `extend_head.html` 文件，将你在 RealFaviconGenerator 复制的 extend_head 粘贴进去：

     ```html
     <link rel="icon" type="image/png" href="/favicon-96x96.png" sizes="96x96" />
     <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
     <link rel="shortcut icon" href="/favicon.ico" />
     <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png" />
     <meta name="apple-mobile-web-app-title" content="Blog" />
     <link rel="manifest" href="/site.webmanifest" />
     ```

     这个文件的内容是标准的 HTML `<link>` 和 `<meta>` 标签。PaperMod 主题会**自动**在 `layouts/partials/` 目录下寻找一个名为 `extend_head.html` 的文件，如果找到了，就会将其内容**注入**到网站每个页面的 `<head>` 标签的末尾。

     * `layouts/` 文件夹
       * **作用：模板蓝图 (Blueprints)**
       * `layouts` 文件夹决定了网站**如何被渲染成 HTML**。
       * **覆盖机制：** 当使用一个主题（如 PaperMod）时，Hugo 默认使用主题内部的 `layouts` 文件夹。
       * 如果在**自己**的网站根目录下创建一个 `layouts` 文件夹（例如 `Blog/layouts/`），可以**覆盖**主题的模板。
       * 例如：如果 PaperMod 有一个 `themes/PaperMod/layouts/posts/single.html` (文章页模板)，你可以在 `Blog/layouts/posts/single.html` 创建一个同名文件，Hugo 就会优先使用您创建的这个，从而实现对主题的深度定制。
     * `layouts/partials/` 文件夹
       * **作用：可重用的 HTML 片段 (Snippets)**
       * `partials` (中文意为“部分”) 文件夹存放的是**可重用的 HTML 代码片段**。
       * **目的：** 避免重复。例如，网站的页眉 (`header.html`) 和页脚 (`footer.html`) 在每个页面上都是一样的。你不必在 `single.html` (文章页) 和 `list.html` (列表页) 中重复编写页脚代码。
       * 相反，你只在 `layouts/partials/footer.html` 中编写一次页脚，然后在 `single.html` 和 `list.html` 中通过一行代码（如 `{{ partial "footer.html" . }}`）来“调用”它。

> **备注：** 配置好后的网站可以在 [RealFaviconGenerator](https://realfavicongenerator.net/) 的 Favicon checker 来检查是否完全配置合适。此外，你还可以在 [Meta Tags](https://metatags.io/) 和 [HEY META](https://www.heymeta.com/) 这样的 META 查询网站查看前面你为网站配置的社交媒体分享预览图images: ["/img/website-cover.jpeg"]、网站的描述description: "一个记录技术探索、学习笔记和奇思妙想的地方。" ，以及谷歌搜索显示的图标。

### 托管个人博客

前面的部分还只是配置了 **Hugo / PaperMod** 的最基础部分，如果想要你的博客更加完整，比如可以通过域名来随时随地访问，你还需要使用 Cloudflare 这样的网站托管服务平台。

#### 静态网站托管平台

**静态网站托管平台**（Static Site Hosting Platform）是一种专门用于存储、分发和服务**静态网站**的网络服务。

* **静态网站托管平台的核心特性**  
  静态网站托管平台正是利用了静态网站“预先构建”的特性，提供了与传统虚拟主机截然不同的服务。后面将要配置的 **Cloudflare Pages** 就是这类平台的典型代表。  
  其核心特性包括：

  1. **深度集成的 Git 工作流（CI/CD）**  
     这是现代静态托管平台**最核心**的功能。

     * **传统托管：** 需要手动运行 `hugo`，然后使用 FTP/SFTP 将生成的 `/public` 文件夹上传到服务器。
     * **静态托管平台：** 只需将**源代码**（Markdown 和模板）`git push` 到 GitHub。平台会自动检测到更新，然后在云端服务器上运行 `hugo` 构建命令，最后将构建产物（`/public` 目录）自动部署到其全球网络上。
  2. **全球内容分发网络 (CDN)**  
     由于网站文件是静态且不会改变的，平台可以将这些文件（HTML, CSS, 图片）缓存到全球上百个数据中心。

     * 当访客访问网站时，他们会从**物理上最近**的服务器获取数据。
     * **结果：** 无论用户在世界何处，网站的加载速度都极快。
  3. **极高的安全性**  
     静态网站没有正在运行的服务器端脚本（如 PHP），也没有暴露在外的数据库。

     * 黑客无法利用常见的 WordPress 插件漏洞或 SQL 注入等手段来攻击你的网站。
  4. **强大的可扩展性与低成本**
     * **可扩展性：** 向全球数百万用户分发一个静态 HTML 文件，远比为每个用户都动态生成一次页面要容易得多。平台可以轻松应对巨大的流量洪峰。
     * **成本：** 由于托管静态文件的资源消耗极低，这些平台（如 Cloudflare Pages, Netlify, Vercel, GitHub Pages）通常提供极其慷慨的**免费套餐**，足以满足绝大多数个人博客的需求。
  5. **易于管理的自定义域名与SSL**  
     这些平台通常一键提供免费的 SSL 证书（HTTPS），并简化了自定义域名的配置流程。

* **部署/托管平台**  
  现在热门的静态网站托管平台有很多，像是 **[Cloudflare](https://pages.cloudflare.com/)**、**[Vercel](https://vercel.com)**、**[Netlify](https://www.netify.com)** 和 **[Github Pages](https://pages.github.com)**。

  | **特性/平台**    | **Cloudflare Pages**                                         | **Vercel**                                                   | **Netlify**                                                  | **GitHub Pages**                                             |
  | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | **核心优势**     | **全球网络性能与统一生态**。 利用 Cloudflare 遍布全球的庞大**边缘网络 (Edge)** 交付内容，延迟极低。与 DNS、R2 存储、Workers、安全 (DDoS/WAF) 等自家产品无缝集成，提供一站式解决方案。 | **极致的开发者体验 (DX)**。 由 **Next.js 框架的创造者**打造，与其深度绑定。其**即时预览部署**功能（为每个 Git 提交和 PR 自动生成预览链接）被认为是行业标杆。 | **功能全面的“一体机”**。 开创了 JAMstack 部署模式。提供了**构建插件 (Build Plugins)**、开箱即用的**表单处理、身份认证、A/B 测试**等多种“后端即服务”功能，非常全面。 | **简单、免费、Git 原生**。 与 GitHub 仓库**原生集成**，无需任何额外配置即可托管。是开源项目文档、个人简历和简单静态页面的首选，稳定且完全免费。 |
  | **免费套餐**     | **极其慷慨 (最强)**。 无限站点、**无限请求、无限带宽**、每月 500 次构建、**无限协作者**。对于流量大的静态博客而言，无带宽限制是巨大优势。 | **慷慨 (有条件)**。 每月 100 GB 带宽、**6000 分钟**构建时长。功能与付费版几乎一致，但严格限制为**“非商业”**用途。 | **慷慨 (有取舍)。** 每月 100 GB 带宽、300 分钟构建时长、100 万次 Serverless 函数调用。300 分钟的构建时长对于大型或频繁更新的站点**可能成为瓶颈**。 | **完全免费**。 每个账户一个用户/组织站点，每个仓库一个项目站点。有 1GB 存储和每月 100GB 带宽的**软限制**。专为公共项目设计。 |
  | **构建与CI/CD**  | **内置 CI/CD**。 直接连接 GitHub/GitLab。构建速度快（免费版 1 个并发构建）。支持 Hugo 版本等环境变量配置。 | **内置 CI/CD (最快)**。 构建速度极快，拥有**增量构建**和强大的缓存机制。自动为每个 PR 创建可交互的预览部署。 | **内置 CI/CD (最灵活)**。 功能成熟稳定。其**插件生态**允许在构建流程中注入各种任务（如图像优化、SEO 检查等）。 | **不直接提供 (需 DIY)**。 **不提供内置构建**。对于 Hugo/Hexo 等需要“编译”的站点，必须**自行配置 GitHub Actions** 来自动化构建和部署流程。 |
  | **Serverless**   | **Cloudflare Workers**。 功能极其强大，运行在**全球边缘网络**（非特定区域），延迟极低，按需启动速度（冷启动）最快。 | **Vercel Functions**。 基于 AWS Lambda。支持 Node.js, Go, Python 等。与 Next.js 的 API Routes **无缝集成**。 | **Netlify Functions**。 基于 AWS Lambda。易于使用，有丰富的模板和事件触发器，对新手友好。 | **不支持**。 只能托管纯静态文件 (HTML/CSS/JS)，没有任何后端计算能力。 |
  | **生态集成**     | **完美 (闭环生态)**。 与 Cloudflare DNS, R2 存储, KV 存储, Analytics, Turnstile 安全验证等**自家产品**深度集成，全部在同一控制面板管理。 | **优秀 (应用中心)**。 以“应用”为中心，可以方便地集成各种**第三方数据库** (如 Vercel Storage)、Headless CMS 和其他后端服务。 | **优秀 (插件市场)**。 拥有丰富的插件市场和第三方服务集成。其内置的 **Netlify Forms** 和 **Netlify Identity** 极大简化了简单后端功能的实现。 | **基础 (GitHub 原生)**。 生态**就是 GitHub 本身**。与 GitHub Actions, Packages, Issues, Discussions 等紧密集成。 |
  | **最佳使用场景** | **性能优先的静态站点**、个人博客 (如 Hugo/Jekyll)、希望**统一管理域名/DNS/安全/托管**的用户、流量可能较大的项目。 | **React (Next.js) 应用**、需要频繁预览和协作的前端项目、复杂的 Web 应用 (App)。 | **功能驱动的静态站点**、需要表单/登录等轻量后端功能的项目、希望通过插件扩展构建流程的开发者。 | **开源项目文档**、个人主页、简历页面、**纯静态**的简单网站、预算为零且不介意 DIY 构建流程的用户。 |

* **总结对比**  
  上面几个托管平台各有各的优势与不足，但是结合我目前的情况，我还是选择了 **Cloudflare**。

  1. **极致的全球性能**  
     对于 Hugo 博客这样的网站，通常它被**构建一次**（`hugo` 命令），然后就**不再变动**（直到下次写文章）。这种纯静态文件的最佳归宿就是 **CDN**。Vercel 和 Netlify *使用* CDN；而 Cloudflare *就是*全球最大的 CDN 之一。Pages 部署在 CF 的边缘网络上，这意味着博客在**全球任何地方**的访问速度都是第一梯队的。
  2. **免费且慷慨的套餐**
     * **无限带宽 + 无限请求 + 允许商用**。
     * 这意味着博客**永远不必担心流量激增**。如果未来博客达到百万次访问（~~当然是不可能的~~），Cloudflare 会从容应对，而**无需一分钱**。
     * `每月 500 次构建` 对于个人博客来说绰绰有余（意味着每天可以 `git push` 更新 16 次）。

  此外，其他平台也有一些看得到的缺点：

* **Vercel 的缺点：**
  * **免费套餐严禁商用**：也许博客现在不盈利，但如果未来想挂载 Google AdSense 或任何形式的广告，Vercel 有权关停服务。反观 Cloudflare 则允许这样做。
  * **优势错配**：Vercel 的核心优势（如增量构建、预览部署）是为 **Next.js (React)** 这样的动态前端框架设计的。用它来托管 Hugo 博客虽然能行，但其最强大的功能根本用不上。
* **Netlify 的缺点：**
  * **每月 300 分钟构建时长**：这是**未来最大的潜在瓶颈**。博客文章越多，`hugo` 构建所需的时间就越长。当博客有几百上千篇文章时，一次构建可能需要 1-2 分钟。如果每天写点东西 `push` 几次，这个额度会非常快地耗尽。
  * **附加功能（表单等）的意义**：Netlify 的“一体机”优势在于它提供了 Netlify Forms, Identity 等功能。但 Hugo 博客（尤其是 PaperMod）通常使用 Giscus (基于 GitHub) 评论，也不需要表单。这些优势对通常是多余的。
* **GitHub Pages 的缺点：**
  * **功能过于简陋**：它**不会自动构建 Hugo 站点**。必须自己编写一个 `GitHub Actions` 工作流 (YAML 文件) 来实现：`checkout` 代码 -> `setup-hugo` -> `hugo` 构建 -> `deploy` 到 `gh-pages` 分支。

#### Cloudflare 简介

![Cloudflare](https://cf-assets.www.cloudflare.com/slt3lc6tev37/6EYsdkdfBcHtgPmgp3YtkD/0b203affd2053988264b9253b13de6b3/logo-thumbnail.png)

**Cloudflare（CF）** 是一家全球知名的网络基础设施和网站安全公司。  
可以将其理解为一个巨大的、分布在全球的智能网络，它位于**访客**和**服务器**（或 Pages）之间。  
它的核心服务包括：

* **安全保护（Security）**  
  这是 Cloudflare 最出名的领域

  * **DDoS 防护：** 当黑客利用大量僵尸电脑攻击一个网站（试图通过巨大的流量把网站“挤爆”）时，Cloudflare 会吸收并清洗这些恶意流量，确保正常用户还能访问网站。
  * **WAF (Web 应用程序防火墙)：** 它可以拦截常见的网络攻击，比如 SQL 注入或跨站脚本攻击，保护网站数据不被窃取。
  * **隐藏真实 IP：** 它可以隐藏网站服务器的真实 IP 地址，让攻击者找不到直接攻击的目标。
* **性能加速（Performance/CDN）**
  * **CDN (内容分发网络)：** Cloudflare 在全球 300 多个城市设有服务器节点。它会把你网站的图片、CSS、JS 文件等“缓存”到这些节点上。
  * **代码压缩：** 它可以自动压缩网站文件，减少传输数据量，让网页打开更快。
* **可靠性与 DNS (Reliability)**
  * **DNS 解析：** Cloudflare 提供世界上最快的 DNS 服务之一。它还推出了著名的公共 DNS **1.1.1.1**，主打隐私保护和速度。
  * **Always Online™：** 如果你的原始服务器突然宕机了，Cloudflare 可以展示它之前缓存的网页版本，让用户感觉网站依然在线。

除此之外，Cloudflare 还有一些在业界独树一帜的特点：

* **无服务器计算 (Serverless / Workers)：** 它允许开发者直接在全球边缘节点上运行代码（Cloudflare Workers），而不需要自己维护服务器。这对现代全栈开发非常重要。
* **Zero Trust (零信任安全)：** 这是它近年来发力的重点，帮助企业替代传统的 VPN，让员工无论在哪里都能安全地访问公司内网资源。

#### GitHub 远程仓库

将本地网站部署到托管平台的前提是同步本地仓库与 [github](https://github.com) 远程仓库。

* **Git**  
  **Git 是一个分布式版本控制系统 (Version Control System)。**

  * **作用：** 它安装在**本地电脑**上，会记录你对文件所做的每一次修改（增加、删除、修改代码）。
  * **核心功能：**
    * **版本回退：** 如果你把代码改崩了，可以随时回退到之前的任意版本。
    * **分支管理 (Branching)：** 你可以从主线复制出一个平行的分支来尝试新功能，如果失败了可以直接删除分支而不会影响主程序；如果成功了，可以再合并回去。
    * **离线工作：** Git 不需要网络，它可以在硬盘上离线工作。
* **GitHub**  
  **GitHub 是一个基于云端的代码托管平台。**

  * **作用：** 它是一个**网站**，可以将你本地 Git 仓库里的代码上传（Push）到这里。
  * **核心功能：**
    * **云端备份：** 如果你的电脑坏了，代码在 GitHub 上还有备份。
    * **团队协作：** 你的同事可以在这里下载你的代码，修改后再上传，GitHub 会帮助合并大家的工作。
    * **开源社区：** 全世界最优秀的开源项目（如 Linux, React, VS Code）都托管在这里，你可以查看、学习甚至参与修改。
* **本地仓库与 GitHub 远程仓库**  
  **本地仓库 (Local Repository)** 是电脑上的文件夹（由 Git 管理），而**远程仓库 (Remote Repository)** 是 GitHub 服务器上的文件夹。它们之间的关系通过 **“推 (Push)”** 和 **“拉 (Pull)”** 来维持同步。

  ```Plaintext
  [电脑 / 本地工作区]             [Git 本地仓库]               [GitHub 远程仓库]
  (写代码、修改文件)               (.git 文件夹)                  (云端服务器)
          |                            |                           |
          |  1. git add (暂存)          |                           |
          V                            |                           |
  [暂存区 Staging Area]                 |                           |
          |                            |                           |
          |  2. git commit (存档)       |                           |
          |--------------------------> |                           |
                                       |   3. git push (上传)       |
                                       |-------------------------> |
                                       |                           |
                                       |   4. git pull (下载)       |
                                       |<------------------------- |
  ```

  1. **工作区 (Working Directory)：**  
     在编辑器里写代码的地方。
  2. **暂存 (Stage - `git add`)：**  
     使用 Git 来计划将一些文件的修改放入下一次存档，这就像是挑选要放进购物车的商品。
  3. **提交 (Commit - `git commit`)：**  
     在**本地仓库**生成一个永久的快照（存档）。
  4. **推送 (Push - `git push`)：**  
     把本地的这些“存档”上传到 GitHub。此时，远程仓库才有了更新，别人才能看到。
  5. **拉取 (Pull - `git pull`)：**  
     如果同事上传了新代码到 GitHub，就需要把它“拉”回到本地电脑，保持同步。

* **常用命令**

  | **动作**   | **命令**               | **解释**                                 | **发生位置** |
  | ---------- | ---------------------- | ---------------------------------------- | ------------ |
  | **初始化** | `git init`             | 在当前文件夹创建一个新的 Git 本地仓库。  | 本地         |
  | **克隆**   | `git clone [url]`      | 把 GitHub 上的项目完整下载到本地电脑上。 | 远程到本地   |
  | **暂存**   | `git add .`            | 把所有修改过的文件标记，准备存档。       | 本地         |
  | **提交**   | `git commit -m "备注"` | 正式存档，生成版本号。                   | 本地         |
  | **推送**   | `git push`             | 把本地的新存档上传到 GitHub。            | 本地到远程   |
  | **拉取**   | `git pull`             | 把 GitHub 上的新内容下载并合并到本地。   | 远程到本地   |

* **创建 GitHub 空仓库**  
  首先需要在 GitHub 创建好一个用来同步本地 Hugo 博客的仓库。

  1. 登录 GitHub。
  2. 点击右上角的 **+** 号，选择 **New repository**。
  3. **Repository name**  
     为仓库名称，例如 `hugo-blog`。
  4. **Description**  
     为仓库描述，例如：Hugo 个人博客：`嚼不烂的个人博客`
  5. **Visibility**  
     选择 **Public**（Private 也可以，但后面的评论区工具需要仓库为 Public）。
  6. **不要**勾选 "Add a README file" 或 ".gitignore"。需要创建一个纯净的空仓库，避免后续合并冲突。
  7. 点击 **Create repository**。
* **初始化本地项目仓库**  
  将本地电脑的 Hugo 站点 **Blog** 初始化为 git 仓库。  
  以下操作均在 **Blog** 目录下进行。

  1. **初始化本地 Git 仓库**（前面配置主题时已经运行）

     ```bash
     git init
     ```

  2. **将当前分支重命名为 main**  
     （现在的标准做法）

     ```bash
     git branch -M main
     ```

  3. **编辑 `.gitignore` 文件**  
     `.gitignore` 中的目录在提交时会自动排除 。

     ```bash
     # Hugo build output
     /public/
     /resources/

     # Hugo server lock file
     .hugo_build.lock

     # OS generated files
     .DS_Store
     .DS_Store?
     ._*
     .Spotlight-V100
     .Trashes
     ehthumbs.db
     Thumbs.db

     # IDE configuration files
     .idea/
     ```

     * `/public/` ：这是 `hugo` 命令生成的静态网站（HTML, CSS, JS）。**绝不**应该将这个文件夹提交到 Git。部署服务（如 Cloudflare Pages）会从网站的**源代码**（Markdown 和模板）自动构建它。
     * `/resources/` ：这是 Hugo 用于缓存（如 SASS 编译、图片处理）的目录。它会按需自动生成，提交它只会徒增仓库体积。
     * `.hugo_build.lock` ：这是 `hugo server` 运行时使用的锁文件。
     * OS / IDE 文件 ：`Thumbs.db` (Windows) 和 `.idea/` (JetBrains IDEs) 都是本地环境文件，与项目代码无关。
* **链接本地仓库到 GitHub 远程仓库**
  * **添加所有文件到暂存区**

    ```bash
    git add .
    ```

  * **创建第一个提交（Commit)**

    ```bash
    git commit -m "Initial commit of Hugo blog"
    ```

  * **链接到 GitHub 远程仓库**

    ```bash
    git remote add origin https://github.com/Jbulan/hugo-blog.git
    ```

  * **推送本地提交到 GitHub**

    ```bash
    git push -u origin main
    ```

    `-u` (或 `--set-upstream`) 会将本地 `main` 分支与远程 `origin/main` 分支关联，之后只需运行 `git push` 即可。

> **注意：** 由于仓库是公开的，切勿将含有密码、API Key（如 OpenAI Key、R2 密钥）的 `.env` 文件或私有配置文件上传到 GitHub！请务必检查 `.gitignore` 配置。

#### Cloudflare Pages / Workers

Cloudflare Pages / Workers 的基础是 **Serverless (无服务器计算)与 Edge (边缘网络/边缘计算)**。

* **Serverless (无服务器架构)**  
  Serverless 并非指“不存在服务器”，而是一种云计算执行模型。在这种模型中，云提供商动态管理机器资源的分配。开发者只需编写代码（通常以函数的形式），而无需关心底层基础设施（如服务器配置、补丁更新、负载均衡或操作系统维护）。  
  **核心特征：**

  * **抽象化 (Abstraction)**：基础设施完全不可见，开发者仅关注业务逻辑。
  * **弹性伸缩 (Auto-scaling)**：系统根据请求流量自动扩容（Scale-up）或缩容（Scale-down），甚至可以缩减到零。
  * **按量付费 (Pay-as-you-go)**：计费通常基于执行次数和运行时间（毫秒级），而非预留的服务器容量。
  * **无状态 (Stateless)**：计算单元通常是短暂且无状态的，数据需持久化到外部数据库或存储中。
* **Edge / Edge Network (边缘网络与边缘计算)**  
  传统的云计算通常是“中心化”的（例如，服务器位于AWS的弗吉尼亚数据中心）。而 **Edge (边缘)** 是指将计算能力和数据存储推向离用户物理位置最近的网络节点。  
  **核心逻辑：**

  * **降低延迟 (Latency Reduction)**：通过在地理上分布广泛的CDN（内容分发网络）节点上运行代码，数据传输的物理距离被缩短，从而显著降低RTT（往返时间）。
  * **去中心化 (Decentralization)**：请求不再集中涌向单一数据中心，而是由全球各地的数百个节点分担。

  **总结**：**Serverless** 解决了“如何运维”的问题，而 **Edge** 则解决了“在哪运行”的问题。  
  Cloudflare 的核心竞争力正是将这两者结合：**在边缘节点上运行无服务器代码**。

* **Cloudflare Works**  
  **定位：** 基于边缘的 FaaS (Function-as-a-Service) 平台。  
  **技术原理：** 传统的 Serverless（如 AWS Lambda）通常基于 **容器 (Container)** 技术，每次冷启动需要加载完整的运行时环境，速度较慢。 而 Cloudflare Workers 基于 Google Chrome V8 引擎的 **Isolates (隔离)** 技术。

  * **轻量级**：Isolates 是 V8 中的轻量级上下文，启动时间为毫秒级。
  * **资源开销低**：可以在单个进程中运行成千上万个 Isolates，内存开销极低。
  * **语言支持**：原生支持 JavaScript/TypeScript，并支持通过 WebAssembly (Wasm) 运行 Rust、C++ 等编译语言。

  **典型应用场景：**
  * **HTTP 请求处理**：修改 HTTP头、重定向、A/B 测试。
  * **API 聚合与代理**：作为 API Gateway，将请求转发到不同后端并聚合结果。
  * **安全验证**：在边缘进行 JWT 校验，拦截恶意请求，减轻源站压力。
* **Cloudflare Pages**  
  **定位：** 面向前端开发者的 JAMstack 部署平台（类似于 Vercel 或 Netlify)。  
  **工作流程：**

  1. **Git 集成：**  
     连接 GitHub/GitLab 仓库。
  2. **自动构建**：推送代码后，Cloudflare 会自动拉取代码，运行构建命令（如 `hugo --minify` 或 `npm run build`）。
  3. **全球分发**：构建生成的静态文件（HTML/CSS/JS）会被分发到 Cloudflare 的边缘网络。

  **核心优势：**
  * **Pages Functions**：它允许在 Pages 项目中直接编写后端逻辑（本质上是集成了 Workers）。这意味着可以只用一个仓库就部署全栈应用（前端静态资源 + 后端动态 API）。
  * **预览部署 (Preview Deployments)**：每次 Pull Request 都会生成一个独立的预览 URL，便于测试和协作。

  接下来将要使用的就是 **Cloudflare Pages**。

* **部署到 Cloudflare Pages**
  1. **登录 Cloudflare：**
     * 登录 [Cloudflare](https://dash.cloudflare.com/login) 账户。
     * 在仪表板中，展开 "计算和 AI"菜单。
     * 转到 "Workers 和 Pages" 页面。
  2. **创建 Pages 项目：**
     * 点击 "创建应用程序 (Create application)" -> "Pages" -> "导入现有 Git 存储库 (Connect to Git)"。
     * 授权 Cloudflare 访问你的 GitHub 账户，并选择先前创建的 Hugo 博客仓库，例如 `Jbulan/hugo-blog` 。
  3. **配置构建设置：**
     * 在 "项目名称" 中填入名称，例如 `jiaobulan`。
     * 选择 `main` 作为生产分支。
     * **Framework preset (框架预设)：** 选择 **Hugo**。
     * **Build command (构建命令)：** Cloudflare 会自动填入 `hugo`。也可以使用 `hugo --gc --minify` 来进行额外优化。
     * **Build output directory (构建输出目录)：** Cloudflare 会自动填入 `public`。
     * **环境变量：** 点击 "环境变量 (Environment variables)" -> "添加变量 (Add variable)"。
       * 变量名称: `HUGO_VERSION`
       * 值：本地正在使用的 `hugo version`，例如 `0.150.0`。**这可以防止版本不匹配导致的构建失败**。
  4. **保存并部署：**
     * 点击 "保存并部署 (Save and Deploy)"
     * Cloudflare 会开始第一次构建。完成后，你的博客将部署到一个免费的 `*.pages.dev` 域名上（例如 `jiaobulan.pages.dev`）。

     现在就完成部署了，可以临时用 Cloudflare Pages 分配的免费域名来访问你的个人博客。

#### Cloudflare 个人域名

> **付费提醒：** 以下部分涉及域名购买与付费服务。

在前面部署好博客后，你会发现通过 Cloudflare Pages 免费域名访问你的网站经常甚至完全受阻。放心，这并不是你的网络问题，也不是 Cloudflare 的问题，其主要原因在于我们中国大陆的特殊网络环境，也就是防火长城，即 **GFW**。

关于 GFW 的问题，这里不作展开说明。你可以在本博客的另一篇文章《魔法学院》中找到更具体的介绍，以及一种常见的解决办法（也就是所谓的“翻墙”）。

* 但是对于 Cloudflare Pages ，又需要另外分析：
  * **连坐效应（Collateral Damage）：** Cloudflare Pages 的默认域名（`xxx.pages.dev`）是一个公共后缀。因为任何人都可以免费注册并部署内容，导致大量滥用者利用它搭建违规（如博彩、色情、诈骗）或敏感政治内容的网站。
  * **GFW 的封锁策略：** 中国国家防火墙（GFW）为了省事和高效，通常会直接通过 **DNS 污染** 或 **SNI 阻断** 的方式，屏蔽整个 `*.pages.dev` 甚至 `*.workers.dev` 泛域名。

  对于这种情况，我们可以通过绑定个人域名，让 DNS 解析请求不再经过被污染的 `pages.dev` 列表。**只要你的域名本身没有被 GFW 拉黑，** 通过自定义域名指向 Cloudflare 的服务器，通常是可以正常访问的。  
  这种访问可能不如国内服务器稳定，但对于个人博客或文档站来说，通常是够用的。

* **域名服务商**  
  **域名服务商 (Registrar)**： 互联网名称与数字地址分配机构（ICANN）管理域名总库，但它不直接卖给个人。而 Godaddy、Cloudflare、阿里云等公司获得授权，向你出售域名的使用权（通常按年付费）。  
  域名服务商通常提供以下服务：

  1. **域名注册与续费：**  
     卖给你域名的使用权。
  2. **DNS 解析管理：**  
     提供一个后台，让你设置这个域名指向哪台服务器（IP 地址）。
  3. **隐私保护（WHOIS Privacy）：**  
     隐藏你的真实姓名、邮箱和住址，防止骚扰。
  4. **域名转移：**  
     允许你把域名从一家服务商转到另一家。

  购买、使用域名的流程便是：
  1. **购买：**  
     在服务商处搜索喜欢的名字并付款。
  2. **解析（DNS）：**  
     在服务商后台添加记录。
  3. **验证：**  
     为网站、应用等绑定你的域名，等待系统验证握手成功。

  域名服务商有很多，像是国外的 **[Namecheap](https://namecheap.com)**、**[Namesilo](https://www.namesilo.com)**，国内的 **[阿里云](https://www.aliyun.com)**、**[腾讯云](https://cloud.tencent.com)** 。  
  他们一样都各有优缺点：
  * **Namecheap (老牌稳定)**  
    非常老牌且知名的服务商，服务稳定，客户支持响应快。

    * **特点：** 经常有首年极低价的促销活动（比如 $0.99 注册 .xyz 或 .top）。
    * **优点：**
      * **客服给力：** 24/7 在线聊天客服，解决问题很快。
      * **功能丰富：** 提供免费的 Logo 设计工具、简单的托管服务等。
    * **缺点：** 续费价格通常比首年贵，接近市场平均水平。
  * **Namesilo (批量注册首选)**
    * **特点：** 界面虽然看起来非常简陋，但是价格实惠，API 完善。
    * **优点：** 价格透明，没有隐形消费，免费隐私保护。
    * **适用人群：** 域名投资人或需要批量管理大量域名的用户。
  * **阿里云 (Aliyun / 万网)**
    * **地位：** 国内最大的域名注册商（收购了万网）。
    * **优点：**
      * **备案方便：** 如果使用阿里云的服务器，域名在这里注册可以“一站式”备案，流程衔接最好。
      * **解析稳定：** 国内 DNS 解析速度快。
      * **交易活跃：** 拥有国内最大的域名交易平台，方便后续出售或购买二手域名。
  * **腾讯云 (Tencent Cloud / DNSPod)**
  * **地位：** 国内第二大巨头，整合了 DNSPod。
  * **优点：**
    * **微信生态：** 如果业务涉及微信小程序或公众号，腾讯云的整合度很高。
    * **DNSPod 解析：** 即使域名不在腾讯云，很多人也会专门用 DNSPod 做解析，在国内速度极快且抗攻击能力强。

  ***注意：*** 在国内服务商购买的域名以及服务商都需要进行 **ICP 备案**，而国外的服务商则没有要求。  
  以上这些服务商都很不错，但是 Cloudflare 依然是目前的首选，理由如下：

  * **批发价（零加价）：** Cloudflare 承诺**不赚取差价**。如果不含 ICANN 税费，他们进价多少就卖多少。很多 `.com` 域名在其他地方首年便宜，但续费要 $15-$20，Cloudflare 始终保持在 $9-$10 左右。
  * **顶级解析速度：** 它的主业是 CDN 和安全，域名的 DNS 解析速度全球最快之一，且生效极快。
  * **生态整合：** 本来就在用 Cloudflare Pages，域名也在它家买，可以实现“一键配置”，自动管理 SSL 证书（HTTPS），无需手动改 DNS 服务器。
  * **免费隐私保护：** 默认开启，永久免费。
* **购买并配置 Cloudflare 域名**
  * **在 Cloudflare 购买域名**
    1. 在 Cloudflare 仪表板，展开 "域注册"，转到 "注册域" 界面。
    2. 在注册域界面搜索想购买的域名，例如 `jiaobulan.com`。
    3. 如果该域名未被注册，可以按照提示购买。
    4. 在完成注册页面，看到是需要用支持 **VISA** 或是 **MasterCard** 的银行卡支付，而国内办理的**银联**卡是不被接受的。这里又是另一个我们国家的“特殊国情”导致的常见问题。但是目前还是有解决办法的，本博客的《自由贸易》文章中将会详细介绍。
  * **绑定域名到 Cloudflare Pages**
    1. 回到你的 Cloudflare Pages 项目（在 "Workers 和 Pages" 找到并点击你的项目，如 `jiaobulan` ）。
    2. 转到 "Custom domains" (自定义域) 选项卡。
    3. 点击 "设置自定义域"。
    4. 输入刚刚购买的域名，如 `jiaobulan.com` ，点击 "继续"。
    5. **自动配置：**
       * 由于绑定的域名**已经**在 Cloudflare 上了，Cloudflare 会弹出窗口提示：“检测到这个域名在 Cloudflare 上，可以自动添加 DNS 记录。”
       * 点击确认后 Cloudflare 会自动创建一条 `CNAME` 记录，将 `jiaobulan.com` 指向 `jiaobulan.pages.dev`。
    6. **验证与 SSL：**
       * Cloudflare 会立即开始验证 DNS 记录并自动部署 SSL 证书。
       * 几分钟后，你的域名就可以访问了，并且自动启用了 HTTPS。

现在世界各地的人们都能通过这一串域名来访问你的博客，阅读你的文章了，这会是一个极大的进步。

## 三、配置额外功能

### 图床

#### 图床服务

**图床 (Image Host)** 是指专门用来**存储图片**并提供**直链 (Direct URL)** 的服务器或云服务。

* **工作原理：** 将图片上传到图床，图床返回一个链接（如 `https://img.example.com/photo.jpg`）。然后就可以在 Markdown 文章中引用这个链接，而不是把图片文件直接放在博客项目的 `content` 或 `static` 文件夹里。
* **优点：**
  1. **写作便捷：**  
     配合 PicGo 等客户端，截图后自动上传并生成 Markdown 链接，直接粘贴即可，无需手动复制文件到项目目录。
  2. **仓库瘦身：**  
     避免 Git 仓库因存放大量图片而变得巨大（Git 不擅长管理二进制大文件），加快 `git clone` 和 `git push` 的速度。
  3. **加载加速：**  
     优秀的图床（如 R2）自带 CDN，图片加载速度通常比直接从 GitHub Pages 加载要快。
  4. **数据分离：**  
     如果以后想把博客从 Hugo 迁移到其他平台，由于图片链接是独立的，文章内容可以无缝迁移，无需重新处理图片路径。

目前主流的图床有许多，以下是其中的一些，以及他们的优缺点：

1. **云厂商对象存储**  
   各大云厂商的对象存储服务，虽然需要付费，但对于个人用户来说，费用通常非常低（甚至接近免费）。

   * **阿里云 OSS / 腾讯云 COS / 七牛云 Kodo / 又拍云**
     * **优点：** 全球（特别是国内）访问速度极快，数据持久性最高，几乎不可能倒闭，支持强大的图片处理（缩放、水印）。
     * **缺点：** 配置稍显复杂；**国内使用自定义域名通常需要 ICP 备案**；若遭受恶意攻击（刷流量），可能会产生较高费用。
     * **适用：** 长期博客作者、对速度要求高的用户。
   * **Cloudflare R2**
     * **优点：** **免流量费（Egress fees）**，这一点完胜 AWS S3 和国内云厂商；兼容 S3 API（现有工具大多通用）；全球 CDN 速度不错。
     * **缺点：** 在中国大陆的访问速度不如阿里云/腾讯云稳定（偶尔会被阻断）。
     * **适用：** 主要受众在海外或对国内速度要求不严苛的用户。
   * **Backblaze B2**
     * **优点：** 存储费用极低，属于带宽联盟，配合 Cloudflare CDN 可以实现流量免费。
     * **适用：** 数据量巨大的归档存储。
2. **专用图床服务**  
   这类服务专门为图片托管设计，通常提供免费版和付费版，无需复杂的服务器配置。

   * **SM.MS**
     * **优点：** 老牌图床，运营时间长，有免费版（5GB空间），无需配置即可上传。
     * **缺点：** 免费版不再提供香港 CDN，国内访问速度较慢；晚上高峰期上传可能不稳定。
     * **适用：** 临时分享图片、对访问速度要求不高的场景。
   * **Imgur**
     * **优点：** 全球最大的图片分享社区，完全免费，无限流量。
     * **缺点：** **在中国大陆无法直接访问**（被墙），图片会被压缩。
     * **适用：** 仅面向海外受众的内容。
3. **代码托管平台**  
   利用 GitHub 或 GitLab 的仓库存储图片，配合 CDN 加速。

   * **GitHub + jsDelivr (慎用)**
     * **优点：** 完全免费，版本控制。
     * **缺点：** **jsDelivr 的国内域名备案近期经常出问题**，导致图片经常挂掉；GitHub 仓库有大小限制（建议 1GB 以内）；违反了 GitHub 的使用协议（非代码仓库），有封号风险。
     * **现状：** 曾经最流行，现在**不再推荐**作为主力图床，风险较高。
4. **自建图床**  
    如果有一台 VPS 服务器（云服务器），可以自己搭建图床程序。

   * **Lsky Pro (兰空图床)**
     * **特点：** 界面美观，功能强大，支持多用户，支持对接多种外部存储（如 AWS S3、阿里云 OSS）。
   * **Chevereto**
     * **特点：** 可能是世界上最流行的自建图床程序，功能极其完善，有免费版和付费版。
   * **MinIO**
     * **特点：** 高性能的对象存储，兼容 S3 协议，适合极客和企业内部使用。

从以上的对比分析不难看出，目前最佳的图床服务是 **Cloudflare R2** 。

#### Cloudflare R2：对象存储与计费

对象存储是一种用于处理大量非结构化数据的存储架构。与传统的文件存储（有文件夹层级）或块存储（像硬盘一样分区）不同，对象存储将数据作为“对象”进行管理。

* **核心特点**：
  * **扁平结构**：数据存储在“存储桶”（Bucket）中，没有复杂的文件夹层级，通过唯一的 ID（Key）来访问。
  * **元数据丰富**：每个对象可以包含丰富的自定义元数据（标签），方便管理和检索。
  * **通过 API 访问**：通常通过 HTTP/HTTPS 协议（RESTful API）进行存取，可以在互联网的任何地方访问数据。
  * **无限扩展**：设计之初就是为了存储 PB 级甚至 EB 级的数据。

几乎所有主流云厂商都提供对象存储服务，以下是行业内的几大标杆：

* **AWS S3 (Amazon Simple Storage Service)**：
  * **地位**：行业的先驱和事实标准。大多数对象存储工具和 SDK 都兼容 "S3 协议"。
  * **特点**：功能极其丰富，提供多种存储层级（标准、智能分层、冰川归档等），生态系统最完善。
* **Google Cloud Storage (GCS)**：
  * **特点**：与 Google 的大数据和 AI 服务集成紧密，网络性能优异（依托 Google 的全球光纤网）。
* **Azure Blob Storage**：
  * **特点**：微软 Azure 生态的核心，对于使用 Windows Server 或 .NET 架构的企业非常友好。
* **阿里云 OSS (Object Storage Service)**：
  * **特点**：在中国及亚太地区覆盖极广，针对中国网络环境有特别优化，也是国内用户的首选之一。

以上的都很不错，但是和 Cloudflare R2 相比，**Cloudflare R2** 才是个人博客的最优解。  
Cloudflare R2 也是一个对象存储服务（Object Storage），它的 API 与 AWS S3 兼容（可以直接使用大多数支持 S3 的工具或代码库）。它主打的特点是 **“零出口流量费”（Zero Egress Fees）**。  
**R2 的核心计费结构：**

* **存储费用**：
  * **免费额度**：每月 10 GB 。
  * **超出价格**：$0.015 / GB / 月 。
  * 对于个人博客图床，10 GB 的起步容量非常大，初期基本无需担心费用 。
* **A 类操作（写操作：上传、删除等）**：
  * **免费额度**：每月 100 万次 。
  * **超出价格**：$4.50 / 100 万次 。
  * 上传一张图片算一次操作，100 万次对于个人或中小型项目几乎是用不完的 。
* **B 类操作（读操作：加载、查看）**：
  * **免费额度**：每月 1000 万次 。
  * **超出价格**：$0.36 / 100 万次 。
  * 如果使用公共开发 URL (`.r2.dev`)，每次访问都会消耗此额度，流量大时容易产生费用 。但是可以用前面购买的域名分配一个子域名来免费使用。

**无限免费读取：**  
如果绑定并使用 **自定义域名** 来访问图片/文件，Cloudflare 会通过其 CDN 提供服务，此时 **所有的 B 类操作（读取/下载流量）将完全免费** 。这意味着几乎完全消除了“流量费”这个不可控的成本。  
虽然没有必要，但还是给出一个 Cloudflare R2 与其他对象存储服务的简单对比：

| **特性**                     | **Cloudflare R2**       | **AWS S3 (标准层)**                        | **Google GCS / Azure Blob**     |
| ---------------------------- | ----------------------- | ------------------------------------------ | ------------------------------- |
| **出口流量费 (Egress Fees)** | **$0 (免费)**           | **非常昂贵** (约 $0.09/GB)                 | **昂贵** (类似 AWS)             |
| **存储单价**                 | **$0.015 / GB**         | 约 $0.023 / GB                             | 约 $0.020 - $0.026 / GB         |
| **API 兼容性**               | S3 兼容 (支持大部分)    | 原生 S3 API (行业标准)                     | 各自的 API (S3 兼容性需适配)    |
| **分层存储 (冷/热数据)**     | 较简单 (主要是热存储)   | 非常成熟 (Intelligent Tiering, Glacier 等) | 非常成熟 (Archive, Coldline 等) |
| **全球 CDN 集成**            | 原生集成 Cloudflare CDN | 需配合 CloudFront (额外付费)               | 需配合 Cloud CDN (额外付费)     |
| **主要痛点**                 | 生态集成不如 AWS 丰富   | **流量费刺客**，账单不可控                 | **流量费刺客**                  |

**详细差异点**：

1. **成本控制：**
   * 使用 AWS S3 或 GCS 时，最大的痛点不是存储费，而是 **带宽费（Data Transfer Out）**。如果存储的图片或文件被大量下载，账单会非常惊人。
   * R2 彻底免除了这部分费用。特别是配合自定义域名后，读取完全免费 。
2. **性能与网络**：
   * R2 依托于 Cloudflare 庞大的全球边缘网络。对于分发静态资源（图片、JS、CSS），它的速度通常优于没有配置 CDN 的 S3。
3. **功能深度：**
   * 如果需要极其复杂的生命周期管理（例如：30天后自动转入深度冷存储，1年后删除），或者需要与 AWS Lambda、Athena 进行深度内网数据分析，S3 的功能更强大。R2 目前主要适合作为“存储桶”使用。

总结一下，对于个人博客，直接使用 **Cloudflare R2** 是最明智的选择。

#### Cloudflare R2：图床配置

> **付费提醒：** 以下部分涉及付费服务。

将 Cloudflare R2 作为图床首先需要创建存储桶，并将其绑定到个人域名，最后配置图床管理客户端。

* **创建 R2 存储桶 (Bucket)**
  1. 登录 Cloudflare 仪表板。
  2. 展开 "存储和数据库" 菜单，转到 "R2 对象存储"。
  3. 首次使用需要绑定银行卡（同样需要支持 **VISA** 或 **MasterCard**）。
  4. 点击 **Create bucket (创建存储桶)**。
  5. 在**存储桶名称**处输入名称，例如 `blog-assets`。
  6. **Location (位置)**：保持默认的 `Automatic` (自动) 即可，Cloudflare 会智能分配。
  7. **默认存储类**选择标准
  8. 点击 "创建存储桶"。
* **配置公开访问 (自定义域名)**  
  默认情况下，存储桶是私有的。图床服务需要让它可以通过互联网访问。

  1. 进入刚创建的 `blog-assets` 存储桶页面。
  2. 点击顶部的 **Settings (设置)** 选项卡。
  3. 向下滚动找到 **自定义域** 部分。
  4. 点击 "添加" 来绑定域名。
  5. 输入一个专用的二级域名，例如 `img.jiaobulan.com`。最低 TLS 版本可以选择 `TLS1.3`。
  6. 点击 "继续" 后连接域名，Cloudflare 会自动添加 DNS 记录。等待约 1 分钟，状态变为 "Active" 即可。
* **获取 R2 API 密钥 (用于客户端连接)**
  1. 回到 Cloudflare R2 的主界面（点击左侧菜单的 R2，看到所有存储桶的那个列表页）。
  2. 在右侧找到 **Manage API Tokens (管理 R2 API 令牌)** 并点击。
  3. 点击 **Create  Account API token (创建 Account API 令牌)**。
  4. **Token name (令牌名称)**：填写名称，例如 `picgo-uploader`。
  5. **Permissions (权限)**：**必须选择** `Object Read & Write` (对象读写)，否则客户端无法上传。
  6. **Specify bucket(指定存储桶)**：选择 `Apply to specific bucket(仅应用于特定存储桶)`，然后选择 `blog-assets`。
  7. 点击 **Create API Token (更新 Account API)**。
  8. ⚠️创建 API 后屏幕上会显示密钥信息，**需要立即复制并保存到记事本**，因为离开此页面后将永远无法再次查看。需要保存：
     * **Access Key ID (访问密钥 ID)**
     * **Secret Access Key (机密访问密钥)**
     * **Endpoint (终结点)** (格式通常是 `https://<账户ID>.r2.cloudflarestorage.com`)
* **配置对象存储管理客户端**  
  目前最常用的客户端是 **[PicGo](https://github.com/Molunerfinn/PicGo)** 。

  1. **下载并安装 PicGo**
     * 请前往 PicGo 的 GitHub 发布页下载 Windows 安装包 (`.exe`)：[PicGo Releases](https://github.com/Molunerfinn/PicGo/releases)
     * 安装并打开。
  2. **安装 S3 插件**  
     PicGo 本体默认支持如下图床：

     * `七牛图床`
     * `腾讯云 COS v4\v5 版本`
     * `又拍云`
     * `GitHub`
     * `SM.MS V2`
     * `阿里云 OSS`
     * `Imgur`

     因此需要安装第三方的 `Amazon S3` 插件。
     * 在 PicGo 左侧点击“插件设置”，搜索 `amazon s3`，找到并安装 WayJam So 版本的 `s3 : picgo amazon s3 uploader` 。
  3. **配置图床**
     * 在 PicGo 左侧点击 **图床设置** -> **Amazon S3**。
     * 根据前面保存的 Cloudflare R2 API 配置信息修改默认配置。

       | **配置项**                | **填写内容**                             | **说明**                                        |
       | ------------------------- | ---------------------------------------- | ----------------------------------------------- |
       | **图床配置名**            | `Cloudflare R2`                          | 图床名称                                        |
       | **应用密钥 ID**           | Cloudflare R2 提供的 `Access Key ID`     |                                                 |
       | **应用密钥**              | Cloudflare R2 提供的 `Secret Access Key` |                                                 |
       | **桶名**                  | `blog-assets`                            | 创建的存储桶名称                                |
       | **上传路径**              | `img/{year}/{month}/{md5}.{extName}`     | 文件在桶内的路径结构，这是推荐的默认设置        |
       | **地区**                  | `auto`                                   | R2 自动处理，填 auto 即可                       |
       | **自定义节点**            | Cloudflare R2 提供的 `Endpoint` 链接     |                                                 |
       | **拒绝无效 TLS 证书连接** | `yes`                                    | 更安全的传输连接                                |
       | **ACL 访问控制列表**      | `public-read`                            |                                                 |
       | **设定输出图片 URL 前缀** | `https://img.jiaobulan.com`              | 填写前面绑定存储桶的域名，**必须带上 https://** |
       | **其他选项**              | 保持默认/留空                            | (如 ForcePathStyle 等一般不需要开启)            |

  4. 点击**确定**保存配置。可以在 `PicGo 设置`页面进行简单的设置：
     * **启动模式：** 打开主窗口
     * **上传前重命名：** 开
     * **上传后自动复制 URL：** 开
  5. **上传使用**
     1. 在 PicGo 主界面，点击”上传区“。
     2. 拖入一张图片或者剪贴板截图上传。
     3. PicGo 上传进度条完成，显示”上传成功“。
     4. 在浏览器打开图片链接，显示出上传的图片并且在 Cloudflare R2 存储桶内找到上传的图片。
     5. 完成上传。

### Giscus

博客不能缺少评论区，就像西方不能缺少耶路撒冷。评论区可以让一篇冷冰冰的文章活过来，不仅如此，评论区还起到了交流分享以及指正的重要作用。

#### 评论系统

目前评论系统的最佳实践主要分为两类：**基于 GitHub 的评论系统** 和 **基于 Serverless 的评论系统**。

1. **Giscus (GitHub 驱动的首选)**  
   Giscus 是目前技术博客圈最流行的评论系统，它是 Utterances 的继任者。它利用 **GitHub Discussions (讨论区)** 功能来存储评论。

   * **工作原理：** 当有人评论时，Giscus 会自动在指定的 GitHub 仓库的 Discussions 中创建一条回复。
   * **优点：**
     * **零成本 & 零数据库：** 直接借用 GitHub 的数据库，不需要自己买数据库。
     * **极佳的隐私：** 没有广告，不追踪用户数据。
     * **PaperMod 原生支持：** Hugo 博客配置极其简单。
     * **界面美观：** 支持多种主题（跟随 GitHub 的亮色/暗色），与博客风格完美融合。
   * **缺点：**
     * **门槛：** 评论者**必须**拥有 GitHub 账号并登录才能评论。这对于非技术背景的读者是一个巨大的门槛。
2. **Waline (功能最强且支持匿名)**  
   Waline 是一款简洁、安全的评论系统。它基于 Valine 衍生而来，修复了 Valine 的安全漏洞（IP 泄露等）并增加了后端管理。

   * **工作原理：** 这是一个前后端分离的程序。前端嵌入博客，后端运行在 Serverless 平台（如 **Cloudflare Workers**），数据存储在 LeanCloud、MongoDB 或 Cloudflare D1 中。
   * **优点：**
     * **支持匿名评论：** 不需要登录账号即可评论（这是相比 Giscus 最大的优势）。
     * **完美适配 Cloudflare：** 可以直接将 Waline 后端部署在 **Cloudflare Workers** 上，速度极快且免费。
     * **功能丰富：** 支持表情包、文章阅读量统计 (PV)、Markdown、评论审核后台、邮件通知。
   * **缺点：**
     * **配置稍繁琐：** 需要分别配置后端（Workers）和数据库（如 LeanCloud 或 D1），比 Giscus 麻烦一步。
3. **Twikoo (轻量级 Serverless)**  
  Twikoo 是另一款非常流行的 Serverless 评论系统，和 Waline 很像，但更加轻量。

   * **优点：**
     * **部署灵活：** 支持 Vercel、腾讯云开发、Docker 等多种部署方式。
     * **特色功能：** 支持微信/QQ/钉钉消息推送通知，支持嵌入自定义代码。
     * **轻量：** JS 文件非常小，加载速度快。
   * **缺点：**
     * 同样需要配置后端和数据库。

  | **特性**          | **Giscus**               | **Waline**                    | **Twikoo**              | **Disqus**        |
  | ----------------- | ------------------------ | ----------------------------- | ----------------------- | ----------------- |
  | **数据存储**      | GitHub Discussions       | LeanCloud / MySQL / D1        | MongoDB / CloudBase     | Disqus 服务器     |
  | **部署难度**      | ⭐ (极简)                 | ⭐⭐⭐ (中等)                    | ⭐⭐⭐ (中等)              | ⭐ (简单)          |
  | **评论门槛**      | **需 GitHub 账号**       | **支持匿名** / 社交登录       | **支持匿名** / 社交登录 | 需注册 / 社交登录 |
  | **隐私性**        | ⭐⭐⭐⭐⭐ (极好)             | ⭐⭐⭐⭐⭐ (自托管)                | ⭐⭐⭐⭐⭐ (自托管)          | ⭐ (差，有追踪)    |
  | **国内访问**      | 偶尔不稳定 (依赖 GitHub) | **极快** (若部署在 CF/Vercel) | **极快**                | **无法访问**      |
  | **PaperMod 支持** | **原生内置**             | 需修改模板 / 注入 HTML        | 需修改模板 / 注入 HTML  | 原生内置          |
  | **主要特色**      | 开发者友好，零维护       | 功能全，自带阅读量统计        | 轻量，推送通知好用      | 只有知名度高      |

从上面的对比来看，如果有能力折腾一下，**Waline** 是一个兼顾了功能性与隐私安全的选择。但是考虑到与 Hugo 的兼容性，目前还是选择了 **Giscus**。如果未来还想要更多功能，可能会重新配置为 **Waline**。

#### Giscus 评论系统

* **配置 GitHub 仓库环境**  
  Giscus 依赖于 GitHub Discussions 功能。

  1. **启用 Discussions**：
     * 打开你的 GitHub Hugo 博客仓库页面
     * 点击顶部菜单栏的 **Settings**。
     * 在 **General** 向下滚动找到 **Features** 区域。
     * 勾选 **Discussions** 复选框。
  2. **添加 Discussions 类别：**
     * 打开 Hugo 博客仓库的 **Discussions** 页面。
     * 点击 **Categories (类别)** 旁边的铅笔符号添加类别。
     * 点击 **New category** 新建类别。
     * 在编辑页面填入 **Category name (类别名)** ，如 `Comments` 。
     * 在 **Description** 内选填该类别描述。
     * **Discussion Format** 选择 **Open-ended discussion** (开放式讨论) 。
     * 点击 **Save changes** 完成创建。
  3. **安装 Giscus App**  
     需要为 Hugo 博客仓库安装 **[Giscus App](https://github.com/apps/giscus)** 来启用 Giscus 机器人功能。

     1. 首先需要确保仓库权限为 **Public (公开)** 而不是 Private (个人)。如果不是，在仓库的 **Settings** 中 **General** 页面下滑找到 **Danger Zone** 区域，点击 **Change repository visibility** 项的 **Change visibility** 来修改权限。
     2. 访问 GitHub App 页面： **<https://github.com/apps/giscus>**
     3. **点击安装**:  
        在打开的 GitHub 页面右上角，点击绿色的 **"Install"** 按钮。
     4. **选择账户**:  
        选择你的 GitHub 个人账户。
     5. **选择仓库：**
        * 在 **Repository access** 选择 **Only select repositories** 。
        * 在 **Select repositories** 下拉框中选择 Hugo 博客仓库。
     6. **授权 (Install & Authorize)**:  
        点击底部的安装按钮确认。

  4. **获取 Giscus 配置参数**  
     需要访问 Giscus 官网获取 Hugo 博客的仓库 ID (`repo-id`) 和分类 ID (`category-id`)。

     1. 访问 [Giscus.app](https://giscus.app/zh-CN)。
     2. **仓库**：输入 GitHub 账号/Hugo 仓库，例如 `Jbulan/hugo-blog`，确保通过验证。
     3. **页面与 discussion 映射关系**：推荐选择 **"Discussion 的标题包含页面的 pathname"** 。
        * **`pathname`**:
          * **含义**: 使用 URL 中域名之后的部分作为唯一标识。例如对于 `https://jiaobulan.com/posts/hello/`，它的 pathname 是 `/posts/hello/`。
          * **优点**: 如果以后更换了域名（比如从 `.com` 换成 `.net`），或者在本地 `localhost` 测试，只要文章的文件名和路径没变，评论依然能找回来。
          * **缺点**: 如果重构了博客目录结构（修改了 URL 路径），评论会丢失（此时需要手动迁移）。
        * **`URL`**:
          * **含义**: 使用完整的网址（包括 `https://` 和域名）。
          * **缺点**: **非常不灵活**。一旦更换了域名，或者从 HTTP 变成 HTTPS，Giscus 就会认为这是一篇新文章，旧评论就“消失”了。
        * **`<title>`**:
          * **含义**: 使用文章的标题。
          * **缺点**: **容易冲突**。如果写了两篇标题一样的文章（或者以后更新文章时改了标题），评论系统会混淆，导致评论张冠李戴或者丢失。
        * **`og:title`**:
          * 与 `<title>` 类似，使用的是 Open Graph 协议的标题，同样存在标题修改或重复带来的风险。
        * **`特定字符串` / `特定 discussion 号`**:
          * 这两项通常用于非常特殊的手动集成场景，不适合博客的自动化生成。
     4. **Discussion 分类：**  
        选择前面创建的 **Comments**，勾选**只搜索该分类中的 discussion**。
     5. **特性**：
        * 勾选**启用主帖子上的反应 (Enable reactions on main post)**，在评论区顶部显示一套 Emoji 表情。可以增加互动性。
        * 勾选**将评论框放在评论列表上方**，这样用户可以在不滚动到讨论底部的情况下发表评论。
        * 勾选**懒加载评论 (Lazy load comments)**，只有当读者滚动到页面底部（看到评论区）时，才会加载 Giscus 脚本。这能大幅提升博客首屏的打开速度。
     6. **主题：**  
        根据自己的喜好来选择，默认的“用户偏好的颜色方案”就很好。

  5. **创建评论布局文件**
     1. 复制前面 [Giscus.app](https://giscus.app/zh-CN) 提供的 `<script>` 标签代码。
     2. 在本地 Hugo 站点的 `layouts/partials` 目录下，新建一个 `comments.html` 文件。
     3. 将复制的代码完整粘贴进文件。
  6. **修改 Hugo 配置**
     * 确保 `hugo.yaml` 中 `params` 块下的 `comments:` 设置为 `true` 。
     * 确保 Hugo 文章的 `Front Matter` 中 `comments:` 项为 `true` 。
     * **hugo.yaml** 和 **Front Matter** 共同控制评论区的开启与关闭，其中 **Front Matter** 优先级高于 **hugo.yaml** 。

## 四、博客站点文件结构

在跟着本博客一步步配置后，你的本地 Hugo 博客站点目录应该是类似于：

```text
Blog/
├── hugo.yaml                     # [核心] 站点主配置文件
├── .gitmodules                   # Git 子模块配置（用于管理 PaperMod 主题）
├── .gitignore                    # Git 忽略规则
│
├── archetypes/                   # [模板] 内容原型（新建文章的 Front Matter 模板）
│   ├── default.md
│   └── posts.md                  # 自定义的博文模板
│
├── assets/                       # [资源] 需经 Hugo Pipes 处理的资源（如压缩、指纹）
│   └── img/
│       ├── avatar.png
│       └── website-cover.jpeg
│
├── content/                      # [内容] 存放 Markdown 源码的地方
│   ├── about.md                  # 单页：关于页面
│   ├── archives.md               # 单页：归档页面
│   ├── search.md                 # 单页：搜索索引页面
│   └── posts/                    # 分区：博客文章主目录
│       ├── create-blog.md        # 单文件文章
│       └── hello/                # Page Bundle（页面包）形式的文章
│           └── index.md
│
├── layouts/                      # [布局] 用于覆盖主题默认样式的 HTML 模板
│   └── partials/
│       ├── comments.html         # Giscus 评论模块
│       └── extend_head.html      # 网站图标的配置模块
│
├── static/                       # [静态] 原样复制到 public 的静态文件
│   ├── favicon.ico               # 网站图标
│   ├── site.webmanifest          # PWA 配置文件
│   ├── css/
│   └── img/                      # 通过相对路径直接引用的图片
│
├── themes/                       # [主题] 第三方主题存放目录
│   └── PaperMod/                 # 当前使用的 PaperMod 主题源码
│
└── public/                       # [构建] 运行 hugo 命令后生成的最终静态网站
```

1. `hugo.yaml`  
   这是整个网站的控制中心。

   * **作用**：定义网站的全局参数，如 `baseURL`（域名）、`languageCode`（语言）、导航菜单 (`menu`)、PaperMod 主题的特有参数 (`params`) 。
   * **注意**：Hugo 支持 TOML, YAML, JSON 格式，不同的格式编写要求不同。
2. `archetypes/` (内容原型)  
   运行 `hugo new posts/my-new-post.md` 时，Hugo 不会凭空创建一个空文件，而是会从这里读取模板。

   * **`default.md`**：默认模板。
   * **`posts.md`**：专为 `posts` 目录定制的模板。可以在这里预设 `categories: []`、`tags: []` 或者 `comment: true`，这样每次新建文章时就不用手动重复输入这些字段了。
3. `content/`  
   这是你日常写作的目录。

   * **单文件文章 (`create-blog.md`)**：适用于使用图床服务的文章。
   * **Page Bundle 页面束 (`hello/index.md`)**：
     * **概念**：创建一个文章文件夹 ，在里面放一个 `index.md`。
     * **使用**：可以将该文章专属的图片（如 `image.png`）直接放在文章文件夹内，并在文章中通过 `![图](image.png)` 引用。
   * **特殊页面**：`archives.md` 和 `search.md` 等为博客菜单页面配置。
4. `static/` 和 `assets/` (静态资源)  
   这两个目录都用来放图片、CSS 等，但机制不同：

   * **`static/`**：**“原样复制”**。放在这里的 `favicon.ico`，构建后会直接出现在 `public/favicon.ico`。适合存放 robots.txt、CNAME、网站图标等不需要处理的文件。
   * **`assets/`**：**“加工处理”**。这里的文件可以被 Hugo Pipes 管道处理（例如：将 SCSS 编译为 CSS，压缩图片，或者生成指纹哈希以防止缓存）。PaperMod 的封面图通常建议放在这里以便处理。
5. `layouts/` (覆盖机制)  
   这是 Hugo 的**Lookup Order (查找顺序)**功能。

   * **原理**：当 Hugo 渲染页面时，它会优先在你的 `layouts/` 目录下寻找模板。如果找不到，才会去 `themes/PaperMod/layouts/` 下寻找。
6. `public/` (构建产物)
   * **作用**：运行 `hugo` 命令时，生成的完整 HTML/CSS/JS 静态网站都在这里。
   * **注意**：**不要手动编辑这里的文件**。因为下次运行 `hugo` 时，这里的更改会被瞬间覆盖。
   * **Git 策略**：通常建议将 `public/` 加入 `.gitignore`，因为它是生成物，不需要存入源码库（除非通过将 public 推送到 gh-pages 分支来部署）。
7. `themes/PaperMod/` (第三方代码)
   * **状态**：这是一个 Git Submodule（子模块）。它指向 GitHub 上的 PaperMod 仓库。
   * **操作建议**：**只读**。不要直接修改里面的文件，因为一旦运行 `git submodule update --remote` 升级主题，你的修改就会丢失。如果想改样式，需要在根目录的 `layouts` 或 `assets` 中进行“覆盖”。

## 总结

读万卷书，行千里路。以上的所有内容只不过是在完善各种前置条件，最重要的还是要下笔去写。如果你的博客一篇文章都没有，那就不能称之为“博客”。
