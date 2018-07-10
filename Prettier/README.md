# Prettier

个人翻译

## 1. 文档

[在线 demo](https://prettier.io/playground/)

### 什么是 Prettier?

- 一个主观的代码格式化工具
- 支持大量语言
- 可以和多数的编辑器集成
- 少量的配置

它会将原本的样式全部删除然后确保输出的文件都符合一个固定的格式。

如果你的代码在一行里过长，Prettier 将会重新编辑你的代码。

举个例子，让我们看下这个代码：

```js
foo(arg1, arg2, arg3, arg4);
```

它在一行里能全部展示所以它会保持不变。然而我们都遇到过这种情况。

```js
foo(
  reallyLongArg(),
  omgSoManyParameters(),
  IShouldRefactorThis(),
  isThereSeriouslyAnotherOne()
);
```

我们突然发现之前的格式被破坏了因为它太长了，然后 Prettier 就会小心的将它重新编辑成如下的格式。

```js
foo(
  reallyLongArg(),
  omgSoManyParameters(),
  IShouldRefactorThis(),
  isThereSeriouslyAnotherOne()
);
```

Prettier 会强制执行一个代码风格在你的整个代码库中（代码格式化不会影响到 AST）。它通过解析 AST 来忽略原有的代码风格并使用自己的代码风格来重新编辑代码，这些规则考虑了每行最长的长度，并在适合的时候进行代码的包装。

如果你想了解更多，下面的两个演讲将会给予你更多的说明。

[A Prettier Printer](https://www.youtube.com/watch?v=hkfBvpEfWdA)

[Javascript Code Formatting](https://www.youtube.com/watch?v=0Q4kUNx85_4)

### 为什么使用？

- 保存时自动格式化
- code review 时不用进行代码风格的讨论
- 节约你的时间和精力
- 更多...

#### 创建并强制执行一个代码风格规范

目前为止选择 Prettier 的最大原因是为了停止所有关于代码风格的争论。人们普遍认为，有一个共同的代码风格规范对于一个项目和团队来说是有价值的，但是制定的过程是非常痛苦和没有回报的。人们对写代码的特定方式非常个性化，没有人喜欢花时间去写和读辣鸡的代码。

那么，为什么要去选择 "Prettier 代码风格规范" 而不是其他随意的规范呢？因为 Prettier 是唯一的完全自动的规范。即使 Prettier 不能 100%按照您希望的方式格式化所有的代码，但是考虑到 Prettier 独特之处，这样的牺牲是值得的，不是吗？

#### 帮助新人

// TODO

#### 编写代码

// TODO

#### 容易理解

// TODO

#### 清理现有的代码库

// TODO

#### 快速开发

// TODO

### Prettier vs. Linters

Prettier 和 ESLint/TSLint/stylelint 的差别在哪里呢？

Linters 有两种类别的规则：

**格式化规则**：比如：max-len, no-mixed-spaces-and-tabs, keyword-spacing, comma-style...

Prettier 减轻了对于这整个分类下的规则的需求！Prettier 以一致的方式重头编辑了整个程序，所以这不会让开发者再在这里犯错了：）

**代码质量规则**：比如：no-unused-vars, no-extra-bind, no-implicit-globals, prefer-promise-reject-errors...

Prettier 不对这些规则做处理。它们也是 Linters 提供的最重要的功能，它们可以真正的为你发现代码里的 bug。

### 如何使用

#### 命令行

通过脚本使 Prettier 运行在命令行。

对当前文件进行格式化可以使用 `--write`。你可能会考虑在提交代码之前执行这个操作为了以防万一。

```
prettier [opts] [filename ...]
```

真实的环境可能是这样：

```
prettier --single-quote --trailing-comma es5 --write "{app,__{tests,mocks}__}/**/*.js"
```

Prettier 将会忽略所有在 `node_modules` 中的文件。你可以使用 `--with-node-modules` 这个标识来阻止此行为。

##### `--debug-check`

如果您担心 Prettier 会影响你代码的正确性，请添加 `--debug-check` 到命令中。如果检测到代码的正确性发生了变化，Prettier 将会打印出错误消息。请注意 `--write` 不能使用 `--debug-check`。

##### `--find-config-path` 和 `--config`

##### `--ignore-path`

Prettier 会根据 `.prettierignore` 中的文件路径来忽略不需要格式化的文件。

### 你可以对以下语言进行美化

- ES2017
- JSX or TSX
- Flow
- TypeScript
- Vue
- JSON
- CSS3+
- Less
- SCSS
- styled-components
- styled-jsx
- GraphQL
- GraphQL Schemas
- CommonMark
- GitHub Flavored Markdown
- YAML

正在开发中的语言

- Elm (via elm-format)
- Java
- PHP
- PostgreSQL
- Python
- Ruby
- Swift

### 支持的编辑器

- Atom
  - prettier-atom
  - mprettier
  - miniprettier
- Emacs
  - prettier-emacs
- Espresso
  - espresso-prettier
- Sublime Text
  - JsPrettier
- Vim
  - neoformat
  - ale
  - vim-prettier
- Visual Studio
  - JavaScriptPrettier
- VS Code
  - prettier-vscode
- WebStorm
  - Built-in support

## 2. 配置

### Print Width

指定每行最大的字符数，默认 80 个字符。

`printWidth: <int>`

```typescript
// 格式化前
type ButtonProps = IBaseButtonProps & React.ButtonHTMLAttributes<HTMLButtonElement>;
```

```typescript
// 格式化后
type ButtonProps = IBaseButtonProps &
  React.ButtonHTMLAttributes<HTMLButtonElement>;
```

### Tab Width

指定缩进的空格数，默认 2 个空格。

`tabWidth: <int>`

### Tabs

缩进使用 Tab 替代空格。

`useTabs: <bool>`

### Semicolons

语句末尾添加分号。

`semi: <bool>`

参数：

* `true` - 在每一句的语句末尾添加分号。
* `false` - 仅在每一行的开头添加分号可能会引起 [Automatic Semicolon Insertion](https://segmentfault.com/a/1190000002955405) 错误。

### Quotes

使用单引号替代双引号。

`singleQuote: <bool>`

注意：

* 在 JSX 中永远是双引号这条规则将被忽略。
* 如果一种引号的数量大于另一种引号，则数量较少的引号将会用来包括字符串 - 例子：`"I'm double quoted"` 结果是 `"I'm double quoted"` and `"This \"example\" is single quoted"` 结果是 `'This "example" is single quoted'`。

### Trailing Commas

多行结尾添加逗号。

`trailingComma: "<none|es5|all>"`

例子：

```js
// 单行数组不会添加逗号
const arr = [1, 2, 3];
```

```js
// 多行数组会添加逗号
const arr = [
  1,
  2,
  3,
];
```

### Bracket Spacing

在对象的 key-value 前后添加空格。

`bracketSpacing: <bool>`

参数：

* `true` - `{ foo: bar }`
* `false` - `{foo: bar}`

### JSX Brackets

在多行属性的 JSX 元素末尾紧跟一个 `>` 符号而不是单独在新的一行里添加。（不适用于自闭和元素）

`jsxBracketSameLine: <bool>`

参数：

* `true` -

```jsx
<button
  className="prettier-class"
  id="prettier-id"
  onClick={this.handleClick}>
  Click Here
</button>
```

* `false` -

```jsx
<button
  className="prettier-class"
  id="prettier-id"
  onClick={this.handleClick}
>
  Click Here
</button>
```

### Arrow Function Parentheses

单个参数的箭头函数是否要用括号包裹参数。

`arrowParens: "<avoid|always>"`

### Range

对于选中部分的代码进行格式化。（目前不是特别理解，可能类似于鼠标选中的部分代码）

`rangeStart: <int>`

`rangeEnd: <int>`

### Parser

指定使用的解析器。

可以在配置文件中通过 ```overrides``` 来指定不同类型的文件使用不同的解析器。

例子：

```json
{
  "overrides": [
    {
      "files": "*.less",
      "options": {
        "parser": "less"
      }
    }
  ]
}
```

`parser: "<string>"`

`parser: require("./my-parser")`

