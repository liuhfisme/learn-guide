---
lang: 'zh-CN'
title: '插件'
description: '这个项目将会记录学习过程中的知识点！'
---
## 社区插件
社区用户创建了很多插件，并将它们发布到了 [NPM](https://www.npmjs.com/search?q=keywords:vuepress-plugin) 上。 VuePress 团队也在 [@vuepress](https://www.npmjs.com/search?q=%40vuepress%20keywords%3Aplugin) Scope 下维护了一些官方插件。查看插件本身的文档可以获取更详细的指引。

一般而言，你需要导入插件并通过配置文件的 [plugins](https://v2.vuepress.vuejs.org/zh/reference/config.html#plugins) 配置项来使用它。举例来说，你可以使用 [@vuepress/plugin-google-analytics](https://v2.vuepress.vuejs.org/zh/reference/plugin/google-analytics.html) 来使用 Google Analytics ：
```ts
import { googleAnalyticsPlugin } from '@vuepress/plugin-google-analytics'

export default {
  plugins: [
    googleAnalyticsPlugin({
      id: 'G-XXXXXXXXXX'
    }),
  ],
}
```
> 大部分插件只能使用一次，如果同一个插件被多次使用，那么只有最后一次会生效。

## 本地插件
如果你想要使用自己的插件，但是又不想发布它，你可以创建一个本地插件。

我们推荐你直接将 [配置文件](https://v2.vuepress.vuejs.org/zh/guide/configuration.html#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6) 作为插件使用，因为 [几乎所有的插件 API 都可以在配置文件中使用](https://v2.vuepress.vuejs.org/zh/reference/config.html#%E6%8F%92%E4%BB%B6-api)，这在绝大多数场景下都更为方便。

但是如果你在配置文件中要做的事情太多了，你可以考虑将它们提取到单独的插件中，然后在你的配置文件中使用它们：
```ts
import myPlugin from './path/to/my-plugin.js'

export default {
  plugins: [
    myPlugin(),
  ],
}
```
前往 [深入 > 开发插件](https://v2.vuepress.vuejs.org/zh/advanced/plugin.html) 学习如何开发你自己的插件。