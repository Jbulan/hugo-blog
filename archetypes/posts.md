---
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
---

