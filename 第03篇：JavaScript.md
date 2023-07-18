### 001：如何一次性渲染10万条数据？

1. 虚拟列表
2. 分页加载
3. 延迟渲染：定时器
4. 数据分块加载：requestAnimationFrame、document.createDocumentFragment
5. 使用Web Worker

### 002：如何理解原型链？⭐️

思路：⾸先要说什么是原型，为什么要设计原型（共享属性和⽅法），然后说属性和⽅法查找的顺序，⾃然⽽然就谈到了原型链。原型链可以引申到继承。

回答：每个对象都有原型，对象的原型可以通过其构造函数的 prototype 属性访问，当查找一个对象的属性或⽅法时，首先会在这个对象本身上查找，如果在对象本身上没有，就会去其原型上查找，⽽原型本身也是一个对象，如果在原型上也找不到，就会继续找原型的原型，从而串起一个原型链，原型链的终点是null。

### 003：传值与传址

传值：值传递，基本数据类型（数值、字符串、布尔、null、undefined）

传值：地址传递，对象类型（对象、数组、函数）

### 004：如何准确判断数组类型 ⭐️

- 方法1：`Object.prototype.toString.call(target).slice(8, -1) === 'Array'`（强烈推荐）
- 方法2：`Array.isArray(target)`
- 方法3：`target.constructor === Array`
- 方法4：`target instanceof Array`

### 005：数组常用方法

参考 「第5章·数组对象APIs」

### 006：数组去重

```js
var nums = [1, 2, 3, 1, 3, 4, 5, 4];
// 方法1：利用set特性
console.log(Array.from(new Set(nums)));
// 方法2：遍历(for/forEach...)
var t = [];
nums.forEach((m) => {
  if (!t.includes(m)) {
    t.push(m);
  }
});
console.log(t);
// 方法3：reduce
console.log(
  nums.reduce((t, m) => {
    if (!t.includes(m)) {
      t.push(m);
    }
    return t;
  }, [])
);
// 方法4：filter
console.log(nums.filter((m, i) => nums.indexOf(m) === i));
```

### 007：数组求交集

```js
var a = [1, 2, 3, 4, 5];
var b = [2, 4, 6, 8, 10];

// 方法1：使用双重循环遍历两个数组，将它们的共同元素加入新数组中。时间复杂度为 O(n^2)。
var intersection = [];
for (var i = 0; i < a.length; i++) {
  for (var j = 0; j < b.length; j++) {
    if (a[i] === b[j]) {
      intersection.push(a[i]);
    }
  }
}
console.log(intersection);

// 方法2：filter + includes 过滤出第一个数组中同时也在第二个数组中出现的元素。时间复杂度为 O(n^2)。
var intersection = a.filter((m) => b.includes(m));
console.log(intersection);

// 方法3：set + filter 时间复杂度为 O(n)。
var set = new Set(a);
var intersection = b.filter((item) => set.has(item));
console.log(intersection);

// 方法4：map + filter 时间复杂度为 O(n)。
var map = new Map();
a.forEach((k) => map.set(k, 1));
var intersection = b.filter((k) => map.has(k));
console.log(intersection);

// 方法5：HashMap 时间复杂度为 O(n)。
var hashMap = {};
a.forEach((k) => (hashMap[k] = 1));
var intersection = b.filter((k) => !!hashMap[k]);
console.log(intersection);
```

### 008：清空数组元素

- `arr.length = 0`：没有重新开辟内存（推荐）
- `arr = []`：重新开辟内存

### 009：call/bind/apply 的区别

它们都是用于改变函数执行上下文（`this`）的方法：

1. `call(this, ...args)`：修改 `this` 指针并 **立即执行函数**；
2. `bind(this, ...args)`：修改 `this` 指针但是 **不会立即执行函数**，而是 **返回一个新函数**；

3. `apply(this, [..args])`：修改 `this` 指针并 **立即执行函数**；

### 010：对象继承 ⭐️

1. 原型链继承：通过将一个对象实例作为另一个对象的原型来实现继承。优点是简单易懂，缺点是所有子类实例共享同一原型对象，存在属性和方法被共享修改的风险。
2. 构造函数继承：通过在子类构造函数中使用父类构造函数并传递参数来实现继承。优点是可以在子类实例上执行父类构造函数中的代码，缺点是无法继承父类原型链上的属性和方法。
3. 组合继承：结合了原型链继承和构造函数继承的优点，在子类构造函数中调用父类构造函数以及将一个对象实例作为另一个对象的原型来实现继承。优点是既可以继承父类构造函数中的属性和方法，又可以继承父类原型链上的属性和方法，缺点是会调用两次父类构造函数。
4. 寄生继承：在原型式继承的基础上，增强对象，返回新对象。优点是不必为了指定子类的原型而调用父类的构造函数，缺点是由于没有使用严格的语法，可能会给其他开发者带来困扰。
5. ES6 的 class 继承：通过 `class` 关键字和 `extends` 关键字来实现继承。优点是语法简单，易于理解，缺点是需要使用 ES6 中的新特性，不支持旧版浏览器。

综合考虑，ES6 的 class 继承是 JavaScript 中对象继承的最优方案，因为它语法简单、易于理解，同时可以轻松地继承父类构造函数中的属性和方法以及父类原型链上的属性和方法。

### 011：js基本数据类型

基础类型有：Number、String、Boolean、Null、Undefined、Symbol、BigInt。

### 012：typeof 和 instanceof 的区别？

1. typeof 主要用来判断数据类型
2. instanceof 主要用于判断对象是否是某个构造函数的实例

### 013：闭包是什么? 闭包的用途? ⭐️

思路：闭包由词法环境和函数组成。

当一个内部函数引用外部函数的变量时就会形成闭包，如果这个内部函数作为外部函数的返回值，就会形成**词法环境**的引⽤闭环（循环引用），那对应引用的变量就会常驻在内存中，形成⼤家所说的 **闭包内存泄漏**。虽然闭包有内存上的问题，但是却突破了函数作⽤域的限制，使函数内外搭起了沟通的桥梁。闭包也是实现私有⽅法或属性，暴露部分公共⽅法的渠道。

特性：封闭性 / 持久性

用途：

1. 防止全局变量污染；
2. 封装私有化；
3. 模块化开发（实现公有变量）
4. 作缓存

缺陷：内存泄露

### 014：简述事件循环原理 ⭐️

### 015：给出代码的输出顺序

```js
async function async1() {
  console.log('async1 start');
  await async2();
  console.log('async1 end');
}
async function async2() {
  console.log('async2');
}
console.log('script start');

setTimeout(function () {
  console.log('setTimeout');
}, 0)
async1();
new Promise(function (resolve) {
  console.log('promise1');
  resolve();
  console.log('promise2')
}).then(function () {
  console.log('promise3');
});
console.log('script end');
```

主队列：script start → async1 start → async2 → promise1 → promise2 → script end

微任务：async1 end → promise3

宏任务：setTimeout

1. 执行全局代码，打印出 'script start'。
2. 调用 `async1()`，输出 'async1 start'。
3. 在 `async1()` 中遇到 `await async2()`，调用 `async2()`。
4. 在 `async2()` 中打印出 'async2'。
5. 返回到 `async1()`，因为 `await` 等待 `async2()` 的 Promise 完成，所以暂停执行。
6. 打印出 'promise1'。
7. 创建一个 Promise，并立即调用其构造函数中的回调函数。
8. 打印出 'promise2'。
9. 调用 `resolve()`，Promise 进入已解决状态。
10. 打印出 'script end'。
11. 因为 Promise 已解决，继续执行 `.then()` 的回调函数。
12. 打印出 'promise3'。
13. 在宏任务队列中设置一个定时器任务。
14. 当前任务执行完成，事件循环检查到微任务队列中有一个任务，执行该任务，打印出 'async1 end'。
15. 事件循环继续，从宏任务队列中取出定时器任务，打印出 'setTimeout'。

正确顺序：

```js
script start
async1 start
async2
promise1
promise2
script end
async1 end
promise3
setTimeout
```

### 016：输出什么? 为什么?

```js
var b = 10;
(function b(){
    b = 20;
    console.log(b);
})();
```

这段代码将输出 `function b()`。

这段代码展示了函数名与变量名冲突的情况，由于**函数声明具有较高的优先级**，函数名 `b` 优先被解析为函数而不是变量。

### 017：延迟加载JS有哪些方式？

1. \<script async />
2. \<script defer />
3. 动态导入脚本
4. 模块化加载

### 018：null和undefined的区别？

- null：空值
- undefined：未定义

### 019：箭头函数和普通函数有什么区别？⭐️

1. 箭头函数语法更加简洁
2. 箭头函数没有this
3. 箭头函数使用剩余参数（...args）替代普通函数中的 arguments
4. 箭头函数不能作为构造函数

### 020：JavaScript 和 TypeScript的区别？⭐️

### 021：为什么说Symbol是基本数据类型？

因为Symbol 是没有构造函数（*constructor*） 的，不能通过 `new Symbol()` 获得实例。

### 022：基本类型为什么也可以调⽅法，⽐如.toFixed() ？ 

基本类型都有对应的包装类，可以调⽅法是因为进⾏了⾃动装箱。 

### 023：['1', '2', '3'].map(parseInt) 输出什么？为什么？

输出：`[1, NaN, NaN]`

解析：

map回调函数：`(value, index,  array)`

parseInt语法：`parseInt(string, radix)`

第1次遍历：`parseInt("1", 0)`，将1解析为十进制，结果为1

第2次遍历：`parseInt("2", 1)`，将2解析为一进制，由于一进制没有数字2，所以返回NaN。

地3次遍历：`parseInt("3", 2)`，将3解析为二进制，由于二进制没有数字2，所以返回NaN。

### 024：变量提升 ⭐️

JS 分为词法分析阶段和代码执⾏阶段。在词法分析阶段，变量和函数会被提升（*注意：let和const不会提升*），⽽赋值操作以及函数表达式是不会被提升的。 

出现变量声明和函数声明重名的情况时，**函数声明优先级⾼**，会覆盖掉同名的变量声明！为了降低出错的⻛险，尽量避免使⽤提升。

### 025：为什么 0.1+0.2 ! == 0.3，如何让其相等 ？

这是因为js使用的是IEEE 754标准中的双精度浮点数表示法（*即使用64位的浮点数形式存储数值*），使其无法精确表示某些小数。

解决方案：

1. 将小数转换为整数进行计算：可以将小数乘以一个倍数，使其变为整数，然后进行计算。最后再将结果除以倍数得到小数形式。
2. 使用库或函数处理精度问题：Big.js/math.js/Decimal.js

### 026：如何确保undefined的可靠性？

由于 undefined 是一个，void(0)

### 027：LHS 和 RHS 是什么？会造成什么影响？

LHS（Left-Hand Side）和RHS（Right-Hand Side）是js对变量进行赋值和读取操作时的两种不同类型的引用。

- LHS 引用出现在赋值操作符左侧，用于设置变量的值，如果变量不存在，且在⾮严格模式下，就会创建一个全局变量。
- RHS 引用出现在赋值操作符右侧，用于获取变量的值，如果变量不存在，就会报错 ReferenceError。 

### 028：常⻅的 JS 语法错误类型有哪些？举⼏个例⼦？

1. ReferenceError：引⽤了不存在的变量 

2. TypeError：类型错误，⽐如对数值类型调⽤了⽅法。 

3. SyntaxError：语法错误，词法分析阶段报错。 

4. RangeError：数值越界。 

5. URIError
6. EvalError 

### 030：js 中如何确定 this 的值？

如果是在全局作⽤域下，this 的值是全局对象，浏览器环境下是 window。 

函数中 this 的指向取决于函数的调⽤形式，在一些情况下也受到严格模式的影响。

1. 作为普通函数调⽤：严格模式下，this 的值是 undefined，⾮严格模式下，this 指向全局对象。 
2. 作为⽅法调⽤：this 指向所属对象。
3. 作为构造函数调⽤：this 指向实例化的对象。 
4. 通过 call, apply, bind 调⽤：如果指定了第一个参数 thisArg，this 的值就是 thisArg 的值（如果是原始值，会包装为对象）；如果不传 thisArg，要判断严格模式，严格模式下 this 是 undefined，⾮严格模式下 this 指向全局对象。 
