---
lang: 'zh-CN'
title: 'Markdown语法参考'
description: '这个项目将会记录学习过程中的知识点！'
---
## 语法扩展
### 目录
> 目录中的标题将会链接到对应的 标题锚点，因此如果你禁用了标题锚点，可能会影响目录的功能。

如果你想要把当前页面的目录添加到 Markdown 内容中，你可以使用 `[[toc]]` 语法。

**输入**
```md
[[toc]]
```

**输出**
[[toc]]

### Emoji 
你可以在你的 Markdown 内容中输入 `:EMOJICODE:` 来添加 Emoji 表情。前往 [emoji-cheat-sheet](https://github.com/ikatyang/emoji-cheat-sheet) 来查看所有可用的 Emoji 表情和对应代码。

**输入**
```md
技术实践新起点 :tada: !
```

**输出**

技术实践新起点 :tada: !

### 代码块
#### 行高亮
你可以在代码块添加行数范围标记，来为对应代码行进行高亮：

**输入**
````md
```ts{1,6-8}
import { defaultTheme, defineUserConfig } from 'vuepress'

export default defineUserConfig({
title: '你好， VuePress',

theme: defaultTheme({
    logo: 'https://vuejs.org/images/logo.png',
}),
})
```
````

**输出**
```ts{1,6-8}
import { defaultTheme, defineUserConfig } from 'vuepress'

export default defineUserConfig({
  title: '你好， VuePress',

  theme: defaultTheme({
    logo: 'https://vuejs.org/images/logo.png',
  }),
})
```
行数范围标记的例子：
- 行数范围： `{5-8}`
- 多个单行： `{4,7,9}`
- 组合： `{4,7-13,16,23-27,40}`

#### 行号
这个功能是默认启用的，你可以通过配置来禁用它。

你可以在代码块添加 `:line-numbers` / `:no-line-numbers` 标记来覆盖配置项中的设置。

**输入**
````md
```ts
// 行号默认是启用的
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```

```ts:no-line-numbers
// 行号被禁用
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```
````

**输出**
```ts
// 行号默认是启用的
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```

```ts:no-line-numbers
// 行号被禁用
const line2 = 'This is line 2'
const line3 = 'This is line 3'
```

#### 添加 v-pre
为了避免你的代码块被 Vue 编译， VuePress 默认会在你的代码块添加 `v-pre` 指令。这一默认行为可以在配置中关闭

你可以在代码块添加 `:v-pre` / `:no-v-pre` 标记来覆盖配置项中的设置。

**输入**
````md
```md
<!-- 默认情况下，这里会被保持原样 -->
1 + 2 + 3 = {{ 1 + 2 + 3 }}
```

```md:no-v-pre
<!-- 这里会被 Vue 编译 -->
1 + 2 + 3 = {{ 1 + 2 + 3 }}
```

```js:no-v-pre
// 由于 JS 代码高亮，这里不会被正确编译
const onePlusTwoPlusThree = {{ 1 + 2 + 3 }}
```
````

**输出**
```md
<!-- 默认情况下，这里会被保持原样 -->
1 + 2 + 3 = {{ 1 + 2 + 3 }}
```

```md:no-v-pre
<!-- 这里会被 Vue 编译 -->
1 + 2 + 3 = {{ 1 + 2 + 3 }}
```

```js:no-v-pre
// 由于 JS 代码高亮，这里不会被正确编译
const onePlusTwoPlusThree = {{ 1 + 2 + 3 }}
```

#### 导入代码块
你可以使用下面的语法，从文件中导入代码块：
````md
<!-- 最简单的语法 -->
@[code](../foo.js)
````
如果你只想导入这个文件的一部分：
````md
<!-- 仅导入第 1 行至第 10 行 -->
@[code{1-10}](../foo.js)
````
代码语言会根据文件扩展名进行推断，但我们建议你显式指定：
````md
<!-- 指定代码语言 -->
@[code js](../foo.js)
````
实际上，[] 内的第二部分会被作为代码块标记来处理，因此在上面 [代码块](#代码块) 章节中提到的语法在这里都可以支持：
````md
<!-- 行高亮 -->
@[code js{2,4-5}](../foo.js)
````

## 在 Markdown 中使用 Vue
### 模板语法
我们知道：

- Markdown 中允许使用 HTML。
- Vue 模板语法是和 HTML 兼容的。

这意味着， Markdown 中允许直接使用 Vue 模板语法

**输入**
````md
一加一等于： {{ 1 + 1 }}

<span v-for="i in 3"> span: {{ i }} </span>
````

**输出**

一加一等于： {{ 1 + 1 }}

<span v-for="i in 3"> span: {{ i }} </span>

### 组件
你可以在 Markdown 中直接使用 Vue 组件。

**输入**
````md
这是默认主题内置的 `<Badge />` 组件 <Badge text="演示" />
````

**输出**

这是默认主题内置的 `<Badge />` 组件 <Badge text="演示" />