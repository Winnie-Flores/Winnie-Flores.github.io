### 一、全局环境中的 `this`
###### 在全局环境中，`this` 指向全局对象。
**在浏览器中，全局对象是 `window`；在 Node.js 中，全局对象是 `global`。

> `console.log(this); // 浏览器中输出：window`

**在严格模式下，`this` 的值为 `undefined`。

>`"use strict";`
> `console.log(this); // 输出：undefined`

普通函数也指向全局，比如setTimeOut

### 二、对象方法中的 `this`

**当 this 出现在对象的方法中时，它指向调用该方法的对象。

> `const person = {
        `name: "Alice",
        `greet: function() {
            `console.log(this.name);
        `}
    `};
   `person.greet(); // 输出：Alice

在上述代码中，this.name 的值为 person 对象的 name 属性。

### 三、构造函数中的 this

**在构造函数中，this 指向新创建的实例对象。

> `function Person(name) {
        `this.name = name;
    `}
> `const alice = new Person("Alice");
>` console.log(alice.name); // 输出：Alice


在上述代码中，this 指向新创建的 Person 实例对象 alice。

### 四、事件处理程序中的 this

**在事件处理程序中，this 通常指向触发事件的 DOM 元素。

> `const button = document.querySelector("button");
    `button.addEventListener("click", function() {
        `console.log(this); // 输出：button 元素
    `});

在上述代码中，事件处理程序中的 this 指向触发点击事件的 button 元素。

### 五、箭头函数中的 this

**箭头函数没有自己的 this 绑定，this 的值由上下文决定。个人认为，就是往上找有this绑定的东西。

> `const person = {
        `name: "Alice",
        `greet: function() {
            `const innerFunction = () => {
                `console.log(this.name);
            `};
            `innerFunction();
        `}
    `};
> `person.greet(); // 输出：Alice


这里，innerFunction 是一个箭头函数，没有this绑定，所以它的 this 继承自 greet 方法中的 this，即 person 对象。

### 六、call、apply 和 bind 方法

我们可以使用 call、apply 和 bind 方法来显式地设置 this 的值。
##### 1. call 方法

**call 方法可以显式地指定 this 的值并立即调用函数。

> `function greet() {
        `console.log(this.name);
    `}
> 
> `const person = { name: "Alice" };
>` greet.call(person); // 输出：Alice

##### 2. apply 方法

**apply 方法与 call 类似，但它接受一个参数数组。

> `function greet(greeting) {
        `console.log(`${greeting}, ${this.name}`);
    `}
>  
> `const person = { name: "Alice" };
> `greet.apply(person, ["Hello"]); // 输出：Hello, Alice

##### 3. bind 方法

**bind 方法会返回一个新的函数，并且永久性地绑定 this 到指定的值。

> `function greet() {
        `console.log(this.name);
    `}
> 
> `const person = { name: "Alice" };
>` const boundGreet = greet.bind(person);
>` boundGreet(); // 输出：Alice


### 七、sum

JavaScript 中 this 的值取决于它的调用位置和上下文环境。