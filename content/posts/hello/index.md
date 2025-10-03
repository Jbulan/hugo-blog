---
title: "开场白"
date: 2025-09-26T23:50:00+08:00
lastmod: 2025-09-26T23:50:00+08:00
author: "嚼不烂" 

slug: "hello" 
description: "嚼不烂的个人博客" 

categories:
  - "日常杂谈" 
tags:
  - "博客"
  - "杂谈" 

draft: false 
showToc: false 
comments: true 
---

```python
def hello_world():
    print("Hello, world!")

hello_world()
```

### 你好世界

说说搭建个人博客的初衷,前段时间发现自己在博客网站上的文章配图没了,感觉很不可思议,就萌生了这样的想法,但真正驱使我去行动起来的原因是,最近有一次我发表了一篇文章,结果还要审核,最后告诉我审核不通过,好吧,我换了一个博客发表,结果给我封号了,封号了,心情一时难以言表.于是愤而起身,决定亲自搭建一个博客.

下面我们看正文.

**一.前言**

如果时间算是成本的话,那我的标题可能起错了.

**1.1.为什么要搭建博客**

相比较CSDN博客园简书而言,个人博客是自由的,你的博客风格,博客模板,内容都由你自己定,还可以自己起名.这是一件很酷的事情.

再想想那满屏的广告,和你精美的文章一对比,顿时就没了兴趣,不论是你自己还是读者.

**1.2.搭建博客难吗?**

我以前认为搭建博客需要进行域名申请,服务器购买,网站备案,所以操作了一次,而且打算自己写个网站出来,后来我失败了.

我前端啥都不懂,让我写网站?那个时候的我肯定是哪里出了问题,这么高大上的事情还是留给更有实力的人来做吧.

就这几天我搭建博客的整个过程来看,其实搭建博客并不难,当然我还在抠官方文档,这个就另说了.

按照我个人的教程来说,搭建一个个人博客花费的时间一个小时不到就可以了.当然你是严格按照教程来做的.

不过有一点得提醒一下蠢蠢欲动的你,如果你想把博客做的好看一点的话,会花费更多的精力,当然,最多再加一小时.

**二.博客采用的技术**

之前我就说过博客完全是依托于GitHub pages来搭建的,不要关闭,且认真看下去.

Github Pages 是面向用户、组织和项目开放的公共静态页面搭建托管服务，站点可以被免费托管在 Github 上，你可以选择使用 Github Pages 默认提供的域名 github.io 或者自定义域名来发布站点。

**2.1.博客采用的选型**

静态博客的选型主要有两种:

①GitHub 上 结合 Jekyll 搭建的博客，Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过一个转换器（如 Markdown）和我们的 Liquid 渲染器转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的。

②本地渲染好 HTML 后，上传到服务端，代表作品就是 hexo。

简单说，第一种方式，就是我们在本地写好 markdown 之后，直接上传到服务端，服务端会自动渲染成 HTML，然后展示给用户，第二种方案则是我们在本地写好 markdown 之后，在本地将 markdown 渲染成 HTML，然后将渲染好的 HTML 上传到服务端。（markdown 小伙伴们应该都了解吧，我就不做过多介绍了）

这里我选用的就是第二种方式,至于为啥选用第二种搭建博客的方式呢,主要原因有Jekyll技术文档是英文的,并且采用翻译全程不准确,而hexo竟然有中文文档.(我能把我看不懂英文文档的事情告诉你?)

其实主要原因是hexo轻便,访问迅速,博客模板支持也很好,而Jekyll的几个博客模板我都不是很喜欢.两者各有优劣,因人而异.

**2.2.所涉及的其他技术**

①git的本地部署

②Node.js的安装(安装时不要忘记添加环境变量)

③阅读中文的能力

注意git的安装和Node的安装网上都有教程,本身安装也基本上都是下一步的操作.有出现问题的可以联系我,这里就不多说了.

在cmd中,测试有版本号则安装成功

**三.开始搭建博客**

**3.1.安装Hexo**

[Hexo官方文档](https://hexo.io/zh-cn/docs/)

cmd命令行输入安装命令:

```avrasm
npm install -g hexo-cli
```

安装成功后,在Hexo安装的本地新建一个文件夹,这个文件夹就是你的博客根目录

我是直接在电脑E盘下面进行安装的,所以我在E盘下新建一个文件夹lubians

**3.2开始搭建网站**

进入刚才新建的文件夹lubians,启动命令行工具cmd

输入下面的命令初始化当前文件夹

```csharp
hexo init lubians
```

接下来再输入以下命令安装相关的依赖

```mipsasm
npm install
```

安装完成后这时你的文件夹目录大概是下面这个样子:

```bash
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

我的文件夹图样

![img](https://i.loli.net/2020/01/11/2pxLMfBRZKENn5Y.png)

以上的文件和文件夹中,我们来重点关注两个, _config.yml 文件和 themes 文件夹

_config.yml 文件中，我们可以做网站的一些基本配置，例如网站的 title，描述，关键字、图标等，这些配置大都见名知意。如下：

```avrasm
# Site
title: 鲁边
subtitle: 昨天,今天,明天
description: 本站是鲁边的技术分享博客。
keywords: Hadoop,Hadoop生态圈,Java
author: lubians
email: ftongyu@qq.com
language: zh-Hans
timezone: Asia/Shanghai
```

配置完成后,在lubians文件夹下启动cmd命令行工具,输入:

```undefined
hexo ghexo s
```

就已经启动项目了

这里的hexo g 就类似于打包编译的过程,生成静态的HTML文件,hexo s 则是启动服务的意思.

在浏览器中输入http://localhost:4000 就可以看到网站了,博客效果:

![3585491-7a943c497c5c41b1.png](https://i.loli.net/2020/01/11/XMCJupBzqdj6Fyf.png)

说一下hexo里面的几个命令

| 命令          | 简写   | 中文含义                     |
| ------------- | ------ | ---------------------------- |
| hexo server   | hexo s | 本地启动                     |
| hexo generate | hexo g | 生成静态文件                 |
| hexo deploy   | hexo d | 部署网站                     |
| hexo clean    |        | 清除缓存和已经生成的静态文件 |

这四个是最常用的,其他相关命令可以参考Hexo文档,基本上用不到.

**四.自定义主题**

到这里我们的博客搭建已经告一段落了,但是呢,有人就问了,我的博客界面怎么和刚才的页面展示不一样.这就涉及到自定义主题和上面我们说要关注的另一个文件目录 themes 有关了.

**4.1主题**

Hexo生态是比较丰富的,有很多可供选择的主题,上面展示的界面是默认的主题landscape,我使用的主题是shenyu的作用Ayer,GitHub地址:

```bash
https://github.com/Shen-Yu/hexo-theme-ayer.git
这里再提供两个主题供大家参考
https://github.com/litten/hexo-theme-yilia.git
https://github.com/iissnan/hexo-theme-next.git
```

**4.2配置**

首先进入到themes目录下,这个目录里原本就有一个landscape文件夹,放的是默认的主题.

这里就需要在GitHub上克隆你喜欢的主题到themes目录下,当然也可以直接将主题文件下载后拷贝进来.直接在后台回复 **[Ayer]** 获取主题文件.

以我使用的主题为例,在themes下启动cmd命令行,输入clone命令:

```bash
git clone https://github.com/Shen-Yu/hexo-theme-ayer.git
```

克隆成功后,修改lubians的 _config.yml文件,将主题修改为 Ayer(注意冒号后有空格),如下:

```shell
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: Ayer
```

注意这里有两个_config.yml文件,一个是最外层文件夹下的_config.yml,还有一个是主题文件里的_config.yml.

其中外层_config.yml文件里是我们对整个博客的配置,主题文件里的_config.yml是对主题的一些相关配置,要区分开.

**4.3打包启动**

主题创建好之后，接下来就是对主题的配置了，这个比较容易，直接参考官方文档即可。

配置完成后，执行如下命令，即可看到新的主题效果：

![33f8d61591ba9989f0f678012b52181.jpg](https://i.loli.net/2020/01/11/jQv2awKTLR8ql1p.jpg)

在lubians文件夹下启动cmd命令行输入:

```undefined
hexo clean
hexo g
hexo s
```

**五.发布到GitHub上**

最后一步

**5.1创建GitHub仓库**

以 自己的GitHub ID.github.io 为名创建一个 public 仓库，例如我的 ID 为 lubians，创建的仓库如下：

![img](https://i.loli.net/2020/01/11/gklPbrtcSxp27YB.png)

这里一定注意仓库名字前缀是需要和Owner一致,我的Owner是lubians,那么我的仓库名为lubians.github.io .新建成功后,修改lubians文件夹下的_config.yml 文件,配置刚才创建的GitHub仓库地址,如下,将deploy修改为：

```yaml
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: git@github.com:lubians/lubians.github.io.git
  branch: master
```

**5.2发布**

接下来使用Git bash来进行命令的执行,在lubians文件夹中右键,点击Git bash选项进入Git命令行,执行命令:

```css
npm install hexo-deployer-git --save
```

最后在同文件夹下使用cmd命令行输入命令来发布:

```undefined
hexo clean
hexo g
hexo d
```

执行完成后,你的数据就已经上传到Github了,接下来直接访问

[个人博客地址](https://lubians.github.io/)

就可以看到自己的个人站点了,记住把链接里的lubians换成你自己的github设置的仓库名.

以上就完成了整个个人博客的搭建.

**六.搭建个人博客遇到的问题**

还没完呢,可以先搭建,之后遇到问题,再来这里看看有没有同样的问题

**6.1.没有git环境和Node.js环境**

我因为新入手的一台笔记本,没有相关环境,整个过程需要重新配置,记住一点,安装以上两个环境的时候都可以按照官方文档来,但是一定安装完成后配置环境变量,如果环境变量不会配,那我就没办法了,百度吧

**6.2页面太简陋,不好看**

我是个追求 审美的人,哈哈,再抠了一整天的Hexo的中文文档后,搭建了个人博客,发现贼丑,然后就在网上各种寻找模板,最后使用Ayer主题,主题的使用方式上面已经说过了.

更多主题配置请参阅

[Hexo官方主题文档](https://hexo.io/themes/)

**6.3.模板引入搜索功能**

这里需要使用命令下载安装一个搜索插件,在lubians文件夹中启用cmd命令行,输入:

```sql
npm install hexo-generator-search
```

然后在_config.yml配置文件中配置:

```yaml
search:
  path: search.xml
  field: post
  format: html
```

还有一个网站用户订阅功能,提高自己的博客影响力嘛,同样,下载安装

```mipsasm
npm install hexo-generator-feed
```

_config.yml中配置

```yaml
feed:
    type: atom
    path: atom.xml
    limit: 100
```

**6.4引入博客的评论功能**

我的评论使用的是：Valine,Valine是一款快速、简洁且高效的无后端评论系统.

注意启用Valine必须先创建leancloud应用.

[leancloud地址](https://www.leancloud.cn/)

按步骤操作即可,获取 id 和 key.

填入Ayer主题中的_config.yml配置文件(注意是另一个配置文件)中,位置如下:

```less
# 1、Valine[一款快速、简洁且高效的无后端评论系统](https://github.com/xCss/Valine)
# 启用Valine必须先创建leancloud应用， 获取 id|key 填入即可
leancloud:  
  enable: true
  app_id: ''
  app_key: ''
```

**6.5图片链接问题**

这个是最坑的,因为发表文章都是用Markdown来写的,图片是以链接的形式引入的,我主要使用Typora笔记来写,这样图片就不知道存到哪里了,微信公众号发表文章的图片无法引入,简书,博客园都不行,所以需要使用图床工具.

综合下来,我使用的图床工具是

[SM.MS](https://sm.ms/)

单次上传文件不超过10个,每个不大于5MB,有5G的免费使用空间,操作便捷,建议使用.

**七.废话**

以上博客搭建流程就彻底完结了,还是之前的那句话,欢迎大家订阅和友链.

突然想起李宗盛的一首歌里的一句歌词,**想说却还没说的还很多.**

这会却不知道从何说起了,我的个人博客里还比较空,这段时间我会逐渐把握在其他平台发表的博客和自己以前整理的笔记逐渐全部放到上面去.
