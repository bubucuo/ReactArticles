[TOC]

## 常见插件

这是我的环境装的所有插件，snippets都是代码片段，帮助你快速写代码的。

auto的是自动，如auto import是自动引入。

格式化的是Prettier-Code Formatter。

<img src="https://tva1.sinaimg.cn/large/007S8ZIlly1gf5ua3cewvj30fm11yn1e.jpg" height=800/>



## 自定义snippets

vscode自定义snippets：

打开：code->preferences->User Snippets，选择javascript.json(JavaScript)，或者是javascriptreact.json:

![image-20191104161833234](https://tva1.sinaimg.cn/large/007S8ZIlly1gf5uaadti7j31nk0dw0w2.jpg)



配置javascript.json还是javascriptreact.json，依据你本地选择的是JavaScript还是JavaScript React，

![image-20200526143629503](https://tva1.sinaimg.cn/large/007S8ZIlly1gf5udmszg2j31f80u0e81.jpg)

![image-20200526143851489](https://tva1.sinaimg.cn/large/007S8ZIlly1gf5ug3fnr4j31f80u0kjl.jpg)

![image-20200526144257482](https://tva1.sinaimg.cn/large/007S8ZIlly1gf5ukcfnglj31960rinkw.jpg)



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



我这里完整的配置：

```json
{
  // Place your snippets for javascript here. Each snippet is defined under a snippet name and has a prefix, body and 
  // description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
  // $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
  // same ids are connected.
  // Example:
  // "Print to console": {
  // 	"prefix": "log",
  // 	"body": [
  // 		"console.log('$1');",
  // 		"$2"
  // 	],
  // 	"description": "Log output to console"
  // }
  "Print to console": {
    "prefix": "log",
    "body": [
      "console.log('$1'); //sy-log"
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
      "\t\t\t\t<h3>${1:${TM_FILENAME_BASE}}</h3>",
      "\t\t\t</div>",
      "\t\t)",
      "\t}",
      "}",
      ""
    ],
    "description": "Import React"
  },
  "Import React ": {
    "prefix": "rcche",
    "body": [
      "import React, { Component } from 'react'",
      "",
      "class ${1:${TM_FILENAME_BASE}} extends Component {",
      "\trender() {",
      "\t\treturn (",
      "\t\t\t<div>",
      "\t\t\t\t<h3>${1:${TM_FILENAME_BASE}}</h3>",
      "\t\t\t</div>",
      "\t\t)",
      "\t}",
      "}",
      "export default ${1:${TM_FILENAME_BASE}}"
    ],
    "description": "Import React"
  },
  "Write React": {
    "prefix": "cch",
    "body": [
      "class ${1:${TM_FILENAME_BASE}} extends Component {",
      "\trender() {",
      "\t\treturn (",
      "\t\t\t<div>",
      "\t\t\t\t<h3>${1:${TM_FILENAME_BASE}}</h3>",
      "\t\t\t</div>",
      "\t\t)",
      "\t}",
      "}",
      ""
    ],
    "description": "Import React"
  },
  "Hooks": {
    "prefix": "rfch",
    "body": [
      "import React from 'react';",
      "",
      "export default function ${1:${TM_FILENAME_BASE}}(props) {",
      "\treturn (",
      "\t\t<div>",
      "\t\t\t<h3>${1:${TM_FILENAME_BASE}}</h3>",
      "\t\t</div>",
      "\t);",
      "}",
    ],
    "description": "Import React"
  },
  "import funC": {
    "prefix": "rfche",
    "body": [
      "import React from 'react';",
      "",
      "function ${1:${TM_FILENAME_BASE}}(props) {",
      "\treturn (",
      "\t\t<div>",
      "\t\t\t<h3>${1:${TM_FILENAME_BASE}}</h3>",
      "\t\t</div>",
      "\t);",
      "}",
      "export default  ${1:${TM_FILENAME_BASE}}"
    ],
    "description": "Import React"
  },
  "Hooks no export": {
    "prefix": "fch",
    "body": [
      "function ${1:${TM_FILENAME_BASE}}(props) {",
      "\treturn (",
      "\t\t<div>",
      "\t\t\t<h3>${1:${TM_FILENAME_BASE}}</h3>",
      "\t\t</div>",
      "\t);",
      "}",
    ],
    "description": "Import React"
  },
  "constructor": {
    "prefix": "cst",
    "body": [
      "constructor(props) {",
      "\tsuper(props);",
      "\tthis.state = {};",
      "}",
    ],
    "description": "constructor函数"
  },
  "function-cmp": {
    "prefix": "fc",
    "body": [
      "function $1(props) {",
      "\treturn(<div></div>)",
      "}",
    ],
    "description": "function组件"
  },
  "function": {
    "prefix": "f",
    "body": [
      "function ${1:${TM_FILENAME_BASE}}() {",
      "}",
    ],
    "description": "function函数"
  },
  "export default function": {
    "prefix": "edf",
    "body": [
      "export default function ${1:${TM_FILENAME_BASE}}() {",
      "}",
    ],
    "description": "export default function函数"
  },
  "export function": {
    "prefix": "ef",
    "body": [
      "export function ${1:${TM_FILENAME_BASE}}() {",
      "}",
    ],
    "description": "export and function函数"
  },
  "class": {
    "prefix": "ccmp",
    "body": [
      "class $1 extends Component {",
      "\trender() {",
      "\t\treturn (",
      "\t\t\t(<div></div>)",
      "\t\t)",
      "\t}",
      "}",
    ],
    "description": "class组件"
  },
  "improt": {
    "prefix": "impc",
    "body": [
      "import $1 from './pages/$1' ;",
    ],
    "description": "导入pages"
  },
}
```

