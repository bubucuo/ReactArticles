[TOC]

## 常见插件

这是我的环境装的所有插件，snippets都是代码片段，帮助你快速写代码的。

auto的是自动，如auto import是自动引入。

格式化的是Prettier-Code Formatter。

<img src="https://tva1.sinaimg.cn/large/006y8mN6ly1g96nufkjvgj30fm11ynge.jpg" height=800/>



## 自定义snippets

vscode自定义snippets：

打开：code->preferences->User Snippets，选择javascript.json(JavaScript):

![image-20191104161833234](https://tva1.sinaimg.cn/large/006y8mN6ly1g8m2wzk1caj31nk0dw439.jpg)

json格式可参考**[vscode-es7-javascript-react-snippets](https://github.com/dsznajder/vscode-es7-javascript-react-snippets/blob/master/snippets/snippets.json)**、**[simple-react-snippets]()**

可自行扩展出log和rcch：

（扩展前建议安装上面两个比较好用的snippets插件，查看没有符合自己需要的再去扩展呀:）

```json
{
  "Print to console": {
    "prefix": "log",
    "body": [
      "console.log('$1');",
      "$2"
    ],
    "description": "Log output to console"
  },
  "Import React": {
    "prefix": "rcch",
    "body": [
      "import React, { Component } from 'react'",
      "",
      "export default class ${1:${TM_FILENAME_BASE}} extends Component {",
      "\trender() {",
      "\t\treturn (",
      "\t\t\t<div>",
      "\t\t\t\t<h1>${1:${TM_FILENAME_BASE}}</h1>",
      "\t\t\t</div>",
      "\t\t)",
      "\t}",
      "}",
      ""
    ],
    "description": "Import React"
  },
}
```

效果如下图：

![image-20191104162320014](https://tva1.sinaimg.cn/large/006y8mN6ly1g8m31x6mhcj30q60fwn3a.jpg)