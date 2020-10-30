---
title: web开发规范之Javascript
date: 2019-10-31 18:09:16
tags:
    - 前端
categories:
    - 前端
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)、[leetcode](https://leetcode-cn.com/u/iplaycodex/)
> 公众号：[FEZONE](http://iplaycodex.com)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 前言

团队内部整理的一份 Javascript 开发规范,供参考

# 2. 写在前面

-   `JavaScript` 作为最常用的前端编程语言，其编码规约是前端规范的重要组成部分。
-   `ECMAScript 6.0`（即 `ES6`/`ES2015`）作为 `JavaScript` 语言的下一代标准，于 2015 年 6 月正式发布。`ES6` 引入了诸多新的语言特性，与之前的 `JS` 版本有很大差异，因此业界通常会以 ES6、ES5 模糊地区别 ES6 之后（包括 ES2016/ES2017..）、之前的 JS 版本，本规约中也会使用这种模糊的叫法。
-   `ES6` 经过几年的普及，已经成为未来使用的大趋势，尤其是新代码库基本都会使用 `ES6` 编码。
-   因此，本规范使用 `ES6` 编写。对于还在使用 `ES5` 及之前版本 `JS` 的同学，本规范的大部分内容也适用。

# 3. 编码风格

## 3.1. 缩进

`【强制】`使用 4 个空格缩进。`eslint: indent`.统一使用 4 个空格缩进，不要使用 2 个空格或 tab 缩进：

```javascript
// bad
function foo() {
∙∙let name;
}
// good
function foo() {
∙∙∙∙let name;
}
```

<!--more-->

## 3.2. 分号

`【强制】`用分号。`eslint: semi`.统一以分号结束语句，可以避免 JS 引擎自动分号插入机制的怪异行为，在语义上也更加明确。

```javascript
// bad - 导致 Uncaught ReferenceError 报错
const luke = {};
const leia = {}[(luke, leia)].forEach((jedi) => {
    jedi.father = "vader";
});

// good
const luke = {};
const leia = {};
[luke, leia].forEach((jedi) => {
    jedi.father = "vader";
});

// bad - 导致 Uncaught ReferenceError 报错
const reaction = "No! That's impossible!"(
    (async function meanwhileOnTheFalcon() {})()
);

// good
const reaction = "No! That's impossible!";
(async function meanwhileOnTheFalcon() {})();

// bad - 函数将返回 `undefined` 而不是换行后的值
function foo() {
    return;
    ("Result want to be returned");
}

// good
function foo() {
    return "Result want to be returned";
}
```

## 3.3. 逗号

1.`【强制】`对于用逗号分隔的多行结构，不使用行首逗号。`eslint:comma-style`

```javascript
// bad
const story = [once, upon, aTime];

// good
const story = [once, upon, aTime];

// bad
const hero = {
    firstName: "Ada",
    lastName: "Lovelace",
    superPower: "computers",
};

// good
const hero = {
    firstName: "Ada",
    lastName: "Loveplace",
    superPower: "computers",
};
```

2.`【强制】`对于用逗号分隔的多行结构，始终加上最后一个逗号。`eslint:comma-dangle`

这样可以使增删行更加容易，也会使 `git diffs` 更清晰。`Babel` 等编译器会在编译后的代码里帮我们去掉最后额外的逗号，因此不必担心在旧浏览器中的问题。

```javascript
// bad - 没有结尾逗号时，新增一行的 git diff 示例
const hero = {
     firstName: 'Florence',
-    lastName: 'Nightingale'
+    lastName: 'Nightingale',
+    inventorOf: ['coxcomb chart', 'modern nursing']
};

// good - 有结尾逗号时，新增一行的 git diff 示例
const hero = {
     firstName: 'Florence',
     lastName: 'Nightingale',
+    inventorOf: ['coxcomb chart', 'modern nursing'],
};

// bad
const hero = {
    firstName: 'Dana',
    lastName: 'Scully'
};

const heroes = [
    'Batman',
    'Superman'
];

function createHero(
    firstName,
    lastName,
    inventorOf
) {
  // ...
}

createHero(
    firstName,
    lastName,
    inventorOf
);

// good
const hero = {
    firstName: 'Dana',
    lastName: 'Scully',
};

const heroes = [
    'Batman',
    'Superman',
];

function createHero(
    firstName,
    lastName,
    inventorOf,
) {
  // ...
}

createHero(
    firstName,
    lastName,
    inventorOf,
);

// good - 需注意，使用扩展运算符的元素后面不能加逗号
function createHero(
    firstName,
    lastName,
    inventorOf,
    ...heroArgs
) {
  // ...
}
```

# 4. 块

1.【推荐】始终使用大括号包裹代码块。`eslint: curly,nonblock-statement-body-position`
多行代码块必须用大括号包裹

```javascript
// bad
if (foo) bar();
baz(); // 这一行并不在 if 语句里

// good
if (foo) {
    bar();
    baz();
}
```

代码块只有一条语句时，可以省略大括号，并跟控制语句写在同一行。但出于一致性和可读性考虑，不推荐这样做：

```javascript
// bad
if (foo) return false;

// bad - 允许但不推荐
if (foo) return false;

// good
if (foo) {
    return false;
}
```

2.【强制】对于非空代码块，大括号的换行方式采用 `Egyptian Brackets` 风格。`eslint: brace-style`
具体规则如下：

-   左大括号 `{` 前面不换行，后面换行
-   右大括号 `}` 前面换行
-   右大括号 `}` 后面是否换行有两种情况：
    -   如果 `}` 终结了整个语句，如条件语句、函数或类的主体，则需要换行
    -   如果 `}` 后面存在 else、catch、while 等语句，或存在逗号、分号、右小括号`（)）`，则不需要换行

```javascript
// bad - else 应与 if 的 } 放在同一行
if (foo) {
    thing1();
}
else
    thing2();
}

// good
if (foo) {
    thing1();
} else {
    thing2();
}
```

3.【推荐】对于空代码块，且不在类似 `if...else...` 或`try..catch..finally..` 的多块结构中时，可以立即将大括号闭合。`eslint:brace-style`

```javascript
// good
function doNothing() {}
```

如果空代码块在多块结构中，则仍需要按上一条非空块的规则换行：

```javascript
// bad
if (condition) {
    // …
} else if (otherCondition) {
} else {
    // …
}

// good
if (condition) {
    // …
} else if (otherCondition) {
} else {
    // …
}

// bad
try {
    // …
} catch (e) {}

// good
try {
    // …
} catch (e) {}
```

4.`【强制】`不要让代码中出现空代码块，这会使阅读者感到困惑。如果必须使用空块，需在块内写明注释。`eslint: no-empty`

```javascript
// bad
if (condition) {
    thing1();
} else {
}

// good
if (condition) {
    thing1();
} else {
    // TODO I haven’t determined what to do.
}
```

## 4.1. 空格

1.`【强制】`块的左大括号 `{` 前有一个空格。`eslint:space-before-blocks`

```javascript
// bad
function test() {
    console.log("test");
}

// good
function test() {
    console.log("test");
}

// bad
dog.set("attr", {
    age: "1 year",
    breed: "Bernese Mountain Dog",
});

// good
dog.set("attr", {
    age: "1 year",
    breed: "Bernese Mountain Dog",
});
```

2.`【强制】`控制语句（if、while 等）的左小括号 ( 前有一个空格。声明函数时，函数名和参数列表之间无空格。`eslint:keyword-spacing`

```javascript
// bad
if (isJedi) {
    fight();
}

// good
if (isJedi) {
    fight();
}

// bad
function fight() {
    console.log("Swooosh!");
}

// good
function fight() {
    console.log("Swooosh!");
}
```

3.`【强制】`小括号内部两侧无空格。`eslint: space-in-parens`

```javascript
// bad
function bar(foo) {
    return foo;
}

// good
function bar(foo) {
    return foo;
}

// bad
if (foo) {
    console.log(foo);
}

// good
if (foo) {
    console.log(foo);
}
```

4.`【强制】`方括号内部两侧无空格。`eslint: array-bracket-spacing`

```javascript
// bad
const foo = [1, 2, 3];
console.log(foo[0]);

// good
const foo = [1, 2, 3];
console.log(foo[0]);
```

5.`【强制】`大括号内部两侧有空格。`eslint: object-curly-spacing`

```javascript
// bad
const foo = { clark: "kent" };

// good
const foo = { clark: "kent" };
```

6.`【强制】`运算符两侧有空格，除了一元运算符。`eslint:space-infix-ops`

```javascript
// bad
const x = y + 5;

// good
const x = y + 5;

// bad
const isRight = result === 0 ? false : true;

// good
const isRight = result === 0 ? false : true;

// bad - 一元运算符与操作对象间不应有空格
const x = !y;

// good
const x = !y;
```

7.`【强制】`定义对象字面量时，不允许所谓的「水平对齐」，即 key、value 之间应该有且只有一个空格。`eslint: key-spacing`

```javascript
// bad
{
  a:            'short',
  looooongname: 'long',
}

// bad
{
  a           : 'short',
  looooongname: 'long',
}

// good
{
  a: 'short',
  looooongname: 'long',
}
```

8.`【强制】`在使用多个（大于两个）方法链式调用时进行换行缩进，把点. 放在前面以强调这是方法调用而不是新语句。`eslint:newline-per-chained-call no-whitespace-before-property`

```javascript
// bad
$("#items").find(".selected").highlight().end().find(".open").updateCount();

// bad
$("#items").find(".selected").highlight().end().find(".open").updateCount();

// good
$("#items").find(".selected").highlight().end().find(".open").updateCount();

// bad
const leds = stage
    .selectAll(".led")
    .data(data)
    .enter()
    .append("svg:svg")
    .classed("led", true)
    .attr("width", (radius + margin) * 2)
    .append("svg:g")
    .attr("transform", `translate(${radius + margin},${radius + margin})`)
    .call(tron.led);

// good
const leds = stage
    .selectAll(".led")
    .data(data)
    .enter()
    .append("svg:svg")
    .classed("led", true)
    .attr("width", (radius + margin) * 2)
    .append("svg:g")
    .attr("transform", `translate(${radius + margin},${radius + margin})`)
    .call(tron.led);

// good - 大于 2 个方法的链式调用才需要进行换行
const leds = stage.selectAll(".led").data(data);
```

## 4.2. 空行

1.`【推荐】`在文件末尾保留一行空行。`eslint: eol-last`.统一在文件末尾保留一行空行，即用一个换行符结束文件：

```javascript
// bad - 文件末尾未保留换行符
import { foo } from './Foo';
// ...
export default foo;
// bad - 文件末尾保留了2个换行符
import { foo } from './Foo';
// ...
export default foo;↵
↵
// good
import { foo } from './Foo';
// ...
export default foo;↵
```

2.`【强制】`块的开始和结束不能是空行。`eslint: padded-blocks`

```javascript
// bad
function bar() {
    console.log(foo);
}

// good
function bar() {
    console.log(foo);
}

// bad
if (baz) {
    console.log(qux);
} else {
    console.log(foo);
}

// good
if (baz) {
    console.log(qux);
} else {
    console.log(foo);
}
```

3.【参考】在块末和新语句间插入一个空行。

```javascript
// bad
if (foo) {
    return bar;
}
return baz;

// good
if (foo) {
    return bar;
}

return baz;

// bad
const obj = {
    foo() {},
    bar() {},
};
return obj;

// good
const obj = {
    foo() {},

    bar() {},
};

return obj;
```

## 4.3. 最大字符数和最大行数

1.【推荐】单行最大字符数：`100`。`eslint: max-len`.过长的单行代码不易阅读和维护，需要进行合理换行。
单行代码最多不能超过 100 个字符，除了以下两种情况： - 字符串和模板字符串 - 正则表达式

```javascript
// bad
const foo =
    jsonData &&
    jsonData.foo &&
    jsonData.foo.bar &&
    jsonData.foo.bar.baz &&
    jsonData.foo.bar.baz.quux &&
    jsonData.foo.bar.baz.quux.xyzzy;

// good
const foo =
    jsonData &&
    jsonData.foo &&
    jsonData.foo.bar &&
    jsonData.foo.bar.baz &&
    jsonData.foo.bar.baz.quux &&
    jsonData.foo.bar.baz.quux.xyzzy;

// bad
$.ajax({ method: "POST", url: "https://foo.com/", data: { name: "John" } })
    .done(() => console.log("Congratulations!"))
    .fail(() => console.log("You have failed this city."));

// good
$.ajax({
    method: "POST",
    url: "https://foo.com/",
    data: { name: "John" },
})
    .done(() => console.log("Congratulations!"))
    .fail(() => console.log("You have failed this city."));
```

2.【推荐】文件最大行数：`1000`。`eslint: max-lines`
过长的文件不易阅读和维护，最好对其进行拆分。 4.【推荐】函数最大行数：`80`。`eslint: max-lines-per-function`
过长的函数不易阅读和维护，最好对其进行拆分。

# 5. 结束语

❤️ 关注 + 点赞 + 收藏 + 评论 + 转发 ❤️ <br/>原创不易，鼓励笔者创作更好的文章~