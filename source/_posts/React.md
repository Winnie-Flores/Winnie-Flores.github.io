## 创建和嵌套组件
React 应用程序是由 **组件** 组成的。一个组件是 UI（用户界面）的一部分，它拥有自己的逻辑和外观。组件可以小到一个按钮，也可以大到整个页面。
React 组件是返回标签的 JavaScript 函数
React 组件必须以大写字母开头，而 HTML 标签则必须是小写字母。
`export default` 关键字指定了文件中的主要组件。
## 使用 JSX 编写标签
JSX 比 HTML 更加严格。你必须闭合标签，如 `<br />`。你的组件也不能返回多个 JSX 标签。你必须将它们包裹到一个共享的父级中，比如 `<div>...</div>` 或使用空的 `<>...</>` 包裹：
大量转化用[在线转换器](https://transform.tools/html-to-jsx)
## 添加样式
在 React 中，你可以使用 `className` 来指定一个 CSS 的 class。它与 HTML 的 [`class`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes/class) 属性的工作方式相同。然后，可以在一个单独的 CSS 文件中为它编写 CSS 规则
## 显示数据
JSX 会让你把标签放到 JavaScript 中。而大括号会让你 “回到” JavaScript 中，这样你就可以从你的代码中嵌入一些变量并展示给用户。
`style={{}}` 并不是一个特殊的语法，而是 `style={ }` JSX 大括号内的一个普通 `{}` 对象。

## 使用 Hook
以 `use` 开头的函数被称为 **Hook**。`useState` 是 React 提供的一个内置 Hook。[React API 参考](https://zh-hans.react.dev/reference/react)
Hook 比普通函数更为严格。你只能在你的组件（或其他 Hook）的 **顶层** 调用 Hook。
？如果你想在一个条件或循环中使用 `useState`，请提取一个新的组件并在组件内部使用它。
## 组件间共享数据
prop：从父组件向子组件传递数据的一种方式
“状态提升”：动态
## 默认导出 vs 具名导出
| 语法  | 导出语句                                  | 导入语句                                    |
| --- | ------------------------------------- | --------------------------------------- |
| 默认  | `export default function Button() {}` | `import Button from './Button.js';`     |
| 具名  | `export function Button() {}`         | `import { Button } from './Button.js';` |
当使用默认导入时，你可以在 `import` 语句后面进行任意命名。比如 `import Banana from './Button.js'`，如此你能获得与默认导出一致的内容。相反，对于具名导入，导入和导出的名字必须一致。这也是称其为 **具名** 导入的原因！
**通常，文件中仅包含一个组件时，人们会选择默认导出，而当文件中包含多个组件或某个值需要导出时，则会选择具名导出。**
**同一文件中，有且仅有一个默认导出，但可以有多个具名导出！**
## 使用 JSX 书写标签语言
[JSX and React 是相互独立的](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html#whats-a-jsx-transform) 东西。但它们经常一起使用，但你 **可以** 单独使用它们中的任意一个，JSX 是一种语法扩展，而 React 则是一个 JavaScript 的库
### JSX规则
1. 只能返回一个根元素：如果想要在一个组件中包含多个元素，**需要用一个父标签把它们包裹起来**。  
why：JSX 虽然看起来很像 HTML，但在底层其实被转化为了 JavaScript 对象，你不能在一个函数中返回多个对象，除非用一个数组把他们包装起来。这就是为什么多个 JSX 标签必须要用一个父元素或者 Fragment 来包裹。
2. 标签必须闭合：
3.  使用驼峰式命名法给 ~~所有~~ 大部分属性命名：
· 由于 `class` 是一个保留字，所以在 React 中需要用 `className` 来代替
## 在 JSX 中通过大括号使用 JavaScript
如果你想要动态地指定 `src` 或 `alt` 的值,可以 **用 `{` 和 `}` 替代 `"` 和 `"` 以使用 JavaScript 变量**

在 JSX 中，只能在以下两种场景中使用大括号：
1. 用作 JSX 标签内的**文本**：`<h1>{name}'s To Do List</h1>` 是有效的，但是 `<{tag}>Gregorio Y. Zara's To Do List</{tag}>` 无效。
2. 用作紧跟在 `=` 符号后的 **属性**：`src={avatar}` 会读取 `avatar` 变量(此时需要先声明avatar变量），但是 `src="{avatar}"` 只会传一个字符串 `{avatar}`。
### 使用 “双大括号”：JSX 中的 CSS 和 对象
除了字符串、数字和其它 JavaScript 表达式，你甚至可以在 JSX 中传递对象。对象也用大括号表示
```
<ul style={  {    backgroundColor: 'black',    color: 'pink'  }}>
```
内联 `style` 属性 使用**驼峰命名法**编写
你可以把它写成 `src={baseUrl + person.imageId + person.imageSize + '.jpg'}` 这样。

1. `{` 开启 JavaScript 表达式
2. `baseUrl + person.imageId + person.imageSize + '.jpg'` 会生成正确的 URL 字符串
3. `}` 结束 JavaScript 表达式

## 将 Props 传递给组件
Props 是你传递给 JSX 标签的信息。例如，`className`、`src`、`alt`、`width` 和 `height` 便是一些可以传递给 `<img>` 的 props
### 向组件传递 props

在这段代码中， `Profile` 组件没有向它的子组件 `Avatar` 传递任何 props ：
```
export default function Profile() {  return (    <Avatar />  );}
```
你可以分两步给 `Avatar` 一些 props。
#### 步骤 1: 将 props 传递给子组件
首先，将一些 props 传递给 `Avatar`。例如，让我们传递两个 props：`person`（一个对象）和 `size`（一个数字）：
```
export default function Profile() {
  return (    
    <Avatar      
      person={{ name: 'Lin Lanying', imageId: '1bX5QH6' }}        
      size={100}    
    />  
   );
}
```
现在，你可以在 `Avatar` 组件中读取这些 props 了。
#### 步骤 2: 在子组件中读取 props
你可以通过在 `function Avatar` 之后直接列出它们的名字 `person, size` 来读取这些 props。这些 props 在 `({` 和 `})` 之间，并由逗号分隔。这样，你可以在 `Avatar` 的代码中使用它们，就像使用变量一样。
```
function Avatar({ person, size }) {  
  // 在这里 person 和 size 是可访问的
}
```
向使用 `person` 和 `size` props 渲染的 `Avatar` 添加一些逻辑，你就完成了。

Props 使你独立思考父组件和子组件。
### 给 prop 指定一个默认值
如果你想在没有指定值的情况下给 prop 一个默认值，你可以通过在参数后面写 `=` 和默认值来进行解构
```
function Avatar({ person, size = 100 }) {  
  // ...
}
```
默认值仅在缺少 `size` prop 或 `size={undefined}` 时生效。 但是如果你传递了 `size={null}` 或 `size={0}`，默认值将 **不** 被使用。

### 使用 JSX 展开语法传递 props
你可以使用 `<Avatar {...props} />` JSX 展开语法转发所有 props，但不要过度使用它！

### 将 JSX 作为子组件传递
像 `<Card><Avatar /></Card>` 这样的嵌套 JSX，将被视为 `Card` 组件的 `children` prop。

### Props 如何随时间变化
**一个组件可能会随着时间的推移收到不同的 props。**
然而，props 是 不可变的.
**不要尝试“更改 props”。** 当你需要响应用户输入（例如更改所选颜色）时，你可以“设置 state”.

## 条件渲染
- 在 JSX 中，`{cond ? <A /> : <B />}` 表示 _“当 `cond` 为真值时, 渲染 `<A />`，否则 `<B />`”_。
- 在 JSX 中，`{cond && <A />}` 表示 _“当 `cond` 为真值时, 渲染 `<A />`，否则不进行渲染”_。
### 三目运算符（`? :`）
一种紧凑型语法来实现条件判断表达式——条件运算符

如果你之前是习惯面向对象开发的，你可能会认为上面的两个例子略有不同，因为其中一个可能会创建两个不同的 `<li>` “实例”。但 JSX 元素不是“实例”，因为它们没有内部状态也不是真实的 DOM 节点。它们只是一些简单的描述，就像图纸一样。所以上面这两个例子事实上是完全相同的。

用 `<del>` 来显示删除线
<li className="item">
      {isPacked ? (
        <del>
          {name + ' ✅'}
        </del>
      ) : (
        name
      )}
    </li>

### 与运算符（`&&`)
```
  <li className="item">    {name} {isPacked && '✅'}  </li>
```
_当 `isPacked` 为真值时，则（`&&`）渲染勾选符号，否则，不渲染。_

当 [JavaScript && 表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Logical_AND) 的左侧（我们的条件）为 `true` 时，它则返回其右侧的值（在我们的例子里是勾选符号）。但条件的结果是 `false`，则整个表达式会变成 `false`。在 JSX 里，React 会将 `false` 视为一个“空值”，就像 `null` 或者 `undefined`，这样 React 就不会在这里进行任何渲染。
#### 陷阱
**切勿将数字放在 `&&` 左侧.**
JavaScript 会自动将左侧的值转换成布尔类型以判断条件成立与否。然而，如果左侧是 `0`，整个表达式将变成左侧的值（`0`），React 此时则会渲染 `0` 而不是不进行渲染。
例如，一个常见的错误是 `messageCount && <p>New messages</p>`。其原本是想当 `messageCount` 为 0 的时候不进行渲染，但实际上却渲染了 `0`。
为了更正，可以将左侧的值改成布尔类型：`messageCount > 0 && <p>New messages</p>`。

### 选择性地将 JSX 赋值给变量
使用 `if` 语句和变量,let

## 渲染列表
map
```
const listItems = people.map(person => <li>{person}</li>);
```
filter
```
const chemists = people.filter(person =>  person.profession === '化学家');
```

#### 陷阱
因为箭头函数会隐式地返回位于 `=>` 之后的表达式，所以你可以省略 `return` 语句。
```
const listItems = chemists.map(person =>  <li>...</li> // 隐式地返回！);
```
不过，**如果你的 `=>` 后面跟了一对花括号 `{` ，那你必须使用 `return` 来指定返回值！**
```
const listItems = chemists.map(person => { // 花括号  return <li>...</li>;});
```
箭头函数 `=> {` 后面的部分被称为 [“块函数体”](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions#function_body)，块函数体支持多行代码的写法，但要用 `return` 语句才能指定返回值。假如你忘了写 `return`，那这个函数什么都不会返回！

### 用 `key` 保持列表项的顺序
你必须给数组中的每一项都指定一个 `key`——它可以是字符串或数字的形式，只要能唯一标识出各个数组项就行：
```
<li key={person.id}>...</li>
```
直接放在 `map()` 方法里的 JSX 元素一般都需要指定 `key` 值！
用作 key 的值应该在数据中提前就准备好，而不是在运行时才随手生成

Fragment 语法的简写形式 `<> </>` 无法接受 key 值，所以你只能要么把生成的节点用一个 `<div>` 标签包裹起来，要么使用长一点但更明确的 `<Fragment>` 写法：
```
import { Fragment } from 'react';
// ...
const listItems = people.map(person =>  
  <Fragment key={person.id}>    
    <h1>{person.name}</h1>    
    <p>{person.bio}</p>  
  </Fragment>
);
```
这里的 Fragment 标签本身并不会出现在 DOM 上，这串代码最终会转换成 `<h1>`、`<p>`、`<h1>`、`<p>`…… 的列表.

### 设定key值：
1. 来自数据库的数据
2. 本地产生数据：使用自增计数器or类似uuid的库

不要把索引拿来当key值，不要在运行过程动态地产生key

有一点需要注意，组件不会把 `key` 当作 props 的一部分。Key 的存在只对 React 本身起到提示作用。如果你的组件需要一个 ID，那么请把它作为一个单独的 prop 传给组件： `<Profile key={id} userId={id} />`

## 保持组件纯粹
### 纯函数：组件作为公式
- **只负责自己的任务**。它不会更改在该函数调用前就已存在的对象或变量。
- **输入相同，则输出相同**。给定相同的输入，纯函数应总是返回相同的结果。

### 副作用：（不符合）预期的后果
React 的渲染过程必须自始至终是纯粹的。组件应该只 **返回** 它们的 JSX，而不 **改变** 在渲染前，就已存在的任何对象或变量 — 这将会使它们变得不纯粹！

尽管你可能还没使用过，但在 React 中，你可以在渲染时读取三种输入：[props](https://zh-hans.react.dev/learn/passing-props-to-a-component)，[state](https://zh-hans.react.dev/learn/state-a-components-memory) 和 [context](https://zh-hans.react.dev/learn/passing-data-deeply-with-context)。你应该始终将这些输入视为只读。
当你想根据用户输入 _更改_ 某些内容时，你应该 [设置状态](https://zh-hans.react.dev/learn/state-a-components-memory)，而不是直接写入变量。当你的组件正在渲染时，你永远不应该改变预先存在的变量或对象。
React 提供了 “严格模式”，在严格模式下开发时，它将会调用每个组件函数两次。**通过重复调用组件函数，严格模式有助于找到违反这些规则的组件**。
严格模式在生产环境下不生效，因此它不会降低应用程序的速度。如需引入严格模式，你可以用 `<React.StrictMode>` 包裹根组件。一些框架会默认这样做。

### 局部 mutation：组件的小秘密
上述示例的问题出在渲染过程中，组件改变了 **预先存在的** 变量的值。为了让它听起来更可怕一点，我们将这种现象称为 **突变（mutation）** 。
纯函数不会改变函数作用域外的变量、或在函数调用前创建的对象——这会使函数变得不纯粹
但是，**你完全可以在渲染时更改你 _刚刚_ 创建的变量和对象**。

努力在你返回的 JSX 中表达你的组件逻辑。当你需要“改变事物”时，你通常希望在事件处理程序中进行。作为最后的手段，你可以使用 `useEffect`。

## 将 UI 视为树
渲染树仅由 React [组件](https://zh-hans.react.dev/learn/your-first-component#components-ui-building-blocks) 组成，没有提到每个组件渲染的 HTML 标签