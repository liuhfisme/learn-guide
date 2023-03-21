---
lang: 'zh-CN'
title: '部署'
description: '这个项目将会记录学习过程中的知识点！'
---
## 部署
下述的指南基于以下条件：
- Markdown 源文件放置在你项目的 `docs` 目录；
- 使用的是默认的构建输出目录 (`.vuepress/dist`) ；
- 使用 pnpm 作为包管理器，当然也支持使用 npm 或 yarn 。
- VuePress 作为项目依赖安装，并在 `package.json` 中配置了如下脚本：
```json
{
  "scripts": {
    "docs:build": "vuepress build docs"
  }
}
```