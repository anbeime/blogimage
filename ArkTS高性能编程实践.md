# OpenHarmony应用TS&JS编程指南

# [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E6%A6%82%E8%BF%B0)概述

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E7%9B%AE%E6%A0%87%E5%92%8C%E9%80%82%E7%94%A8%E8%8C%83%E5%9B%B4)目标和适用范围

本指南适用于在OpenHarmony上使用TypeScript和JavaScript进行系统开发或应用开发编写代码的场景。

本文参考业界标准及实践，结合语言引擎技术特点以及OpenHarmony技术特点，为提高代码的规范、安全、性能提供编码建议。

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E8%A7%84%E5%88%99%E6%9D%A5%E6%BA%90)规则来源

本指南筛选自OpenHarmony JS通用编程规范[1]，结合可发挥OpenHarmony技术特点并且不违反业界认知的规则，包括ESLint、TSC配置等。

ESLint相关规则中的正例反例代码来源于ESLint Rules[2]，标注“参见 @typescript-eslint”。

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E7%AB%A0%E8%8A%82%E6%A6%82%E8%A7%88)章节概览

### [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#openharmony%E5%BA%94%E7%94%A8%E7%8E%AF%E5%A2%83%E9%99%90%E5%88%B6)[OpenHarmony应用环境限制](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#openharmony%E5%BA%94%E7%94%A8%E7%8E%AF%E5%A2%83%E9%99%90%E5%88%B6)

OpenHarmony应用因安全因素的使用限制，均为强制要求。

### [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E8%AF%AD%E8%A8%80%E7%89%B9%E6%80%A7%E5%A3%B0%E6%98%8E%E4%B8%8E%E5%88%9D%E5%A7%8B%E5%8C%96%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E8%BF%90%E7%AE%97%E4%B8%8E%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%87%BD%E6%95%B0%E7%B1%BB%E4%B8%8E%E5%AF%B9%E8%B1%A1%E5%BC%82%E5%B8%B8%E5%BC%82%E6%AD%A5%E7%B1%BB%E5%9E%8B)语言特性：[声明与初始化](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%A3%B0%E6%98%8E%E4%B8%8E%E5%88%9D%E5%A7%8B%E5%8C%96)、[数据类型](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)、[运算与表达式](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E8%BF%90%E7%AE%97%E4%B8%8E%E8%A1%A8%E8%BE%BE%E5%BC%8F)、[函数](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%87%BD%E6%95%B0)、[类与对象](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E7%B1%BB%E4%B8%8E%E5%AF%B9%E8%B1%A1)、[异常](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%BC%82%E5%B8%B8)、[异步](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%BC%82%E6%AD%A5)、[类型](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E7%B1%BB%E5%9E%8B)

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E7%BA%A6%E5%AE%9A)约定

**规则** ：编程时必须遵守的约定

**建议** ：编程时必须加以考虑的约定

无论是“规则”还是“建议”，都必须理解该条目这么规定的原因，并努力遵守。

# [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#openharmony%E5%BA%94%E7%94%A8%E7%8E%AF%E5%A2%83%E9%99%90%E5%88%B6-1)OpenHarmony应用环境限制

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%BD%BF%E7%94%A8%E4%B8%A5%E6%A0%BC%E6%A8%A1%E5%BC%8F)使用严格模式

**【级别】规则**

**【描述】**

严格模式（ECMAScript 5开始引入ECMAScript标准中，通过'use strict'语法开启）是采用具有限制性JavaScript变体的一种方式，从而使代码隐式地脱离“马虎模式/稀松模式/懒散模式”（sloppy）。

1. 严格模式通过**抛出错误**来消除了一些原有**静默错误** ；
2. 严格模式修复了一些导致JavaScript引擎难以执行优化的缺陷——有时候，相同的代码，严格模式可以比非严格模式下**运行得更快** ；
3. 严格模式**禁用了**在ECMAScript的未来版本中可能会定义的一些语法。

**注：OpenHarmony上方舟编译运行时目前只支持严格模式的TS/JS代码**

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E7%A6%81%E6%AD%A2%E4%BD%BF%E7%94%A8eval)禁止使用eval()

**【级别】规则**

**【描述】**

使用eval()会让程序比较混乱，导致可读性较差。

**【反例】**

```javascript
console.log(eval({ a:2 })); // 输出[object Object] 
console.log(eval('"a" + 2')); // 输出'a2' 
console.log(eval('{ a: 2 }')); // 输出2 
console.log(eval('let value = 1 + 1;')); // 输出undefined
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E7%A6%81%E6%AD%A2%E4%BD%BF%E7%94%A8with-)禁止使用with() {}

**【级别】规则**

**【描述】**

使用with让代码在语义上变得不清晰，因为with的对象，可能会与局部变量产生冲突，从而改变程序原本的用义。

**【反例】**

```javascript
const foo = { x: 5 };
with (foo) {
  let x = 3;
  console.log(x);  // x = 3
}
console.log(foo.x);  // x = 3
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E8%A6%81%E5%8A%A8%E6%80%81%E5%88%9B%E5%BB%BA%E5%87%BD%E6%95%B0)不要动态创建函数

**【级别】规则**

**【描述】**

定义函数的方法包括3种：函数声明、Function构造函数和函数表达式。不管用哪种方法定义函数，它们都是Function对象的实例，并将继承Function对象所有默认或自定义的方法和属性。以函数构造器创建函数的方式类似于函数eval()，可以接受任何字符串形式作为它的函数体，这就会有安全漏洞的风险。

**【反例】**

```javascript
let add = new Function('a','b','return a + b');
// Function构造函数也可以只有一个参数，该参数可以为任意的字符串:
let dd = new Function('alert("hello")');
```

**【正例】**

```javascript
// 函数声明
function add(a,b){
  return a+b;
}
// 函数表达式
let add = function(a,b){
  return a+b;
}
```

# [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%A3%B0%E6%98%8E%E4%B8%8E%E5%88%9D%E5%A7%8B%E5%8C%96)声明与初始化

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%A3%B0%E6%98%8E%E5%8F%98%E9%87%8F%E6%97%B6%E8%A6%81%E6%B1%82%E4%BD%BF%E7%94%A8const%E6%88%96let%E8%80%8C%E4%B8%8D%E6%98%AFvar)声明变量时要求使用const或let而不是var

**【级别】规则**

**【描述】**

在ECMAScript 6允许开发者使用let和const关键字在块级作用域而非函数作用域下声明变量。块级作用域在很多其他编程语言中很普遍，能帮助开发者避免错误。只读变量用const定义，其它变量用let定义。

**【反例】**

```javascript
var number = 1;
var count = 1;
if (isOK) {
  count += 1;
}
```

**【正例】**

```javascript
const number = 1;
let count = 1;
if (isOK) {
  count += 1;
}
```

# [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)数据类型

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E8%A6%81%E7%9C%81%E7%95%A5%E6%B5%AE%E7%82%B9%E6%95%B0%E5%B0%8F%E6%95%B0%E7%82%B9%E5%89%8D%E5%90%8E%E7%9A%840)不要省略浮点数小数点前后的0

**【级别】规则**

**【描述】**

在JavaScript中，浮点值会包含一个小数点，没有要求小数点之前或之后必须有一个数字。虽然不是一个语法错误，但这种格式的数字使真正的小数和点操作符变的难以区分。由于这个原因，必须在小数点前面和后面有一个数字，以明确表明是要创建一个小数。

**【反例】**

```javascript
const num = .5;
const num = 2.;
const num = -.7;
```

**【正例】**

```javascript
const num = 0.5;
const num = 2.0;
const num = -0.7;
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%88%A4%E6%96%AD%E5%8F%98%E9%87%8F%E6%98%AF%E5%90%A6%E4%B8%BAnan%E6%97%B6%E5%BF%85%E9%A1%BB%E4%BD%BF%E7%94%A8isnan%E6%96%B9%E6%B3%95)判断变量是否为NaN时必须使用isNaN()方法

**【级别】规则**

**【描述】**

在JavaScript中，NaN是Number类型的一个特殊值。它被用来表示非数值，这里的数值是指在IEEE浮点数算术标准中定义的双精度64位格式的值。 因为在JavaScript中NaN独特之处在于它不等于任何值，包括它本身，与NaN进行比较的结果是令人困惑：NaN !== NaN or NaN != NaN的值都是true。 因此，必须使用Number.isNaN()或全局的isNaN()函数来测试一个值是否是NaN。

**【反例】**

```javascript
if (foo == NaN) {
  // ...
}
if (foo != NaN) {
  // ...
}
```

**【正例】**

```javascript
if (isNaN(foo)) {
  // ...
}
if (!isNaN(foo)) {
  // ...
}
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E6%B5%AE%E7%82%B9%E5%9E%8B%E6%95%B0%E6%8D%AE%E5%88%A4%E6%96%AD%E7%9B%B8%E7%AD%89%E4%B8%8D%E8%A6%81%E7%9B%B4%E6%8E%A5%E4%BD%BF%E7%94%A8%E6%88%96)浮点型数据判断相等不要直接使用==或===

**【级别】规则**

**【描述】**

由于浮点数在计算机表示中存在精度的问题，数学上相等的数字，经过运算后，其浮点数表示可能不再相等，因而不能使用相等运算符==或===判断浮点数是否相等。

**【反例】**

```javascript
0.1 + 0.2 == 0.3; // false
0.1 + 0.2 === 0.3; // false
```

**【正例】**

```javascript
const EPSILON = 1e-6;
const num1 = 0.1;
const num2 = 0.2;
const sum = 0.3;
if(Math.abs(num1 + num2 - sum) < EPSILON) {
  ...
}
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E8%A6%81%E5%9C%A8%E6%95%B0%E7%BB%84%E4%B8%8A%E5%AE%9A%E4%B9%89%E6%88%96%E4%BD%BF%E7%94%A8%E9%9D%9E%E6%95%B0%E5%AD%97%E5%B1%9E%E6%80%A7length%E9%99%A4%E5%A4%96)不要在数组上定义或使用非数字属性（length除外）

**【级别】规则**

**【描述】**

在JavaScript中，数组也是对象，可以往数组上添加属性，但为了处理方便和避免出错，数组只应该用来存储有序（即索引连续）的一组数据。必须要添加属性时，考虑用Map或者Object替代。

**【反例】**

```javascript
const myHash = [];
myHash['key1'] = 'val1';
myHash['key2'] = 'val2';
myHash[0] = '222';
for (const key in myHash) {
  // key的值为 0 key1 key2
  console.log(key);
}
console.log(myHash.length); // 数组长度为1
```

**【正例】**

非数字属性时使用Map、Object

```javascript
const map = new Map();
map.set('key1', 'val1');
map.set('key2', 'val2');
for(const [key, value] of map) {
  console.log('属性：' + key + ', 值：' + value);
}
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E6%95%B0%E7%BB%84%E9%81%8D%E5%8E%86%E4%BC%98%E5%85%88%E4%BD%BF%E7%94%A8array%E5%AF%B9%E8%B1%A1%E6%96%B9%E6%B3%95)数组遍历优先使用Array对象方法

**【级别】规则**

**【描述】**

对于数组的遍历处理，应该优先使用Array对象方法，如：forEach()、map()、every()、filter()、find()、findIndex()、reduce()、some()。 注意：不能使用for-in遍历数组。

**【反例】**

```javascript
const numbers = [1, 2, 3, 4, 5];
let sum = 0;
// 使用for in遍历数组
for (const num in numbers) {
  console.log(num);
  sum += num;
}
// 依赖已有数组来创建新的数组时，通过for遍历，生成一个新数组
const increasedByOne = [];
for (let i = 0; i < numbers.length; i++) {
  increasedByOne.push(numbers[i] + 1);
}
```

**【正例】**

```javascript
const numbers = [1, 2, 3, 4, 5];
// 使用for of遍历求和
let sum = 0;
for (const num of numbers) {
  sum += num;
}
// 使用forEach遍历求和
let sum = 0;
numbers.forEach(num => sum += num);
// better: 使用reduce方法实现求和，是更好的方式
const sum = numbers.reduce((total, num) => total + num, 0);
// 依赖已有数组来创建新的数组，可使用forEach遍历，生成一个新数组
const increasedByOne = [];
numbers.forEach(num => increasedByOne.push(num + 1));
// better: 使用map方法是更好的方式
const increasedByOne = numbers.map(num => num + 1);
```

# [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E8%BF%90%E7%AE%97%E4%B8%8E%E8%A1%A8%E8%BE%BE%E5%BC%8F)运算与表达式

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%88%A4%E6%96%AD%E7%9B%B8%E7%AD%89%E6%97%B6%E5%BA%94%E4%BD%BF%E7%94%A8%E5%92%8C-%E8%80%8C%E4%B8%8D%E6%98%AF%E5%92%8C)判断相等时应使用===和!== ，而不是==和!=

**【级别】规则**

**【描述】**

JavaScript中使用双等==做相等判断时会自动做类型转换，如：[] == false、[] == ![]、3 == '03'都是true，当类型确定时使用全等===做比较可以提高效率。

**【反例】**

```javascript
age == bee
foo == true
bananas != 1
value == undefined
typeof foo == 'undefined'
'hello' != 'world'
0 == 0
true == true
```

**【正例】**

```javascript
age === bee
foo === true
bananas !== 1
value === undefined
typeof foo === 'undefined'
'hello' !== 'world'
0 === 0
true === true
```

**【例外】**

```javascript
//当判断对象是否是null的时候，可直接使用如下形式：
obj == null
obj != null
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E8%A6%81%E5%9C%A8%E6%8E%A7%E5%88%B6%E6%80%A7%E6%9D%A1%E4%BB%B6%E8%A1%A8%E8%BE%BE%E5%BC%8F%E4%B8%AD%E6%89%A7%E8%A1%8C%E8%B5%8B%E5%80%BC%E6%93%8D%E4%BD%9C)不要在控制性条件表达式中执行赋值操作

**【级别】规则**

**【描述】**

控制性条件表达式常用于if、while、for、?:等条件判断中。 在控制性条件表达式中执行赋值，常常导致意料之外的行为，且代码的可读性非常差。

**【反例】**

```javascript
// 在控制性判断中赋值不易理解  
if (isFoo = false) {
  ...
}
```

**【正例】**

```javascript
const isFoo = someBoolean; // 在上面赋值，if条件判断中直接使用
if (isFoo) {
  ...
}
```

# [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%87%BD%E6%95%B0)函数

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%BF%85%E9%A1%BB%E4%BD%BF%E7%94%A8%E4%B8%80%E8%87%B4%E7%9A%84return%E8%AF%AD%E5%8F%A5)必须使用一致的return语句

**【级别】规则**

**【描述】**

不像静态类型语言强制要求函数返回一个指定类型的值，JavaScript允许在一个函数中不同的代码路径返回不同类型的值。

而JavaScript在以下情况下函数会返回undefined：

1. 在退出之前没有执行return语句
2. 执行return语句，但没有显式地指定一个值
3. 执行return undefined
4. 执行return void，其后跟着一个表达式 (例如，一个函数调用)
5. 执行return，其后跟着其它等于undefined的表达式

在一个函数中，如果任何代码路径显式的返回一个值，但一些代码路径不显式返回一个值，那么这种情况可能是个书写错误，尤其是在一个较大的函数里。因此，函数内，应使用一致的return语句。

**【反例】**

```javascript
function doSomething(condition) {
  if (condition) {
    ...
    return true;
  } else {
    ...
    return;
  }
}
function doSomething(condition) {
  if (condition) {
    ...
    return true;
  }
}
```

**【正例】**

```javascript
// 保证所有路径都以相同的方式返回值
function doSomething(condition) {
  if (condition) {
    ...
    return true;
  } else {
    ...
    return false;
  }
}

function doSomething(condition) {
  if (condition) {
    ...
    return true;
  }
  ...
  return false;
}
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E8%A6%81%E4%BD%BF%E7%94%A8arguments%E5%8F%AF%E4%BB%A5%E9%80%89%E6%8B%A9rest%E8%AF%AD%E6%B3%95%E6%9B%BF%E4%BB%A3)不要使用arguments，可以选择rest语法替代

**【级别】规则**

**【描述】**

rest参数是一个真正的数组，也就是说能够在它上面直接使用所有的数组方法，比如sort，map，forEach或pop，而arguments是一个类数组。因此，应选择使用rest语法替代arguments。另外，rest参数必须是列表中的最后一个参数。

**【反例】**

```javascript
function concatenateAll() {
  // 因为arguments是类数组，不能直接使用join方法，需要先转换为真正的数组
  const args = Array.prototype.slice.call(arguments);   
  return args.join('');
}
```

**【正例】**

```javascript
function concatenateAll(...args) {
  return args.join('');
}
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E8%A6%81%E5%B0%86this%E8%B5%8B%E5%80%BC%E7%BB%99%E4%B8%80%E4%B8%AA%E5%8F%98%E9%87%8F%E7%BA%A6%E6%9D%9Fthis%E5%9C%A8%E4%B8%80%E4%B8%AAscope%E5%86%85%E4%BD%BF%E7%94%A8)不要将This赋值给一个变量，约束This在一个Scope内使用

**【级别】规则**

**【描述】**

箭头函数提供了更简洁的语法，并且箭头函数中的this对象指向是不变的，this绑定到定义时所在的对象，有更好的代码可读性。而保存this引用的方式，容易让开发人员搞混。

**【反例】**

```javascript
function foo() {
  const self = this;
  return function() {
    console.log(self);
  };
}
```

**【正例】**

```javascript
function foo() {
  return () => {
    console.log(this);
  };
}
```

参见：[@typescript-eslint/no-this-alias](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/no-this-alias.md)

ESLint的描述更加严苛，我们认为this不应该在任何情况下赋值给一个变量。

# [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E7%B1%BB%E4%B8%8E%E5%AF%B9%E8%B1%A1)类与对象

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%BD%BF%E7%94%A8%E7%82%B9%E5%8F%B7%E6%9D%A5%E8%AE%BF%E9%97%AE%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%B1%9E%E6%80%A7%E5%8F%AA%E6%9C%89%E8%AE%A1%E7%AE%97%E5%B1%9E%E6%80%A7%E4%BD%BF%E7%94%A8)使用点号来访问对象的属性，只有计算属性使用[]

**【级别】规则**

**【描述】**

在JavaScript中，可以使用点号 (foo.bar) 或者方括号 (foo['bar'])来访问属性。然而，点号通常是首选，因为它更加易读，简洁，也更适于JavaScript压缩。

**【正例】**

```javascript
const name = obj.name;
const key = getKeyFromDB();
const prop = obj[key]; // 属性名是变量时才使用[]
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E8%A6%81%E4%BF%AE%E6%94%B9%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%8E%9F%E5%9E%8B%E6%88%96%E5%90%91%E5%8E%9F%E5%9E%8B%E6%B7%BB%E5%8A%A0%E6%96%B9%E6%B3%95)不要修改内置对象的原型，或向原型添加方法

**【级别】规则**

**【描述】**

内置对象作为一套公共接口，具有约定俗成的行为方式，若修改其原型，可能破坏接口语义。因此，永远不要修改内置对象的原型，或向原型添加方法。

**【反例】**

```javascript
Array.prototype.indexOf = function () {
  return -1;
}
// 其它地方使用的时候
const arr = [1, 1, 1, 1, 1, 2, 1, 1, 1];
console.log(arr.indexOf(2)); // 输出-1
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E8%A6%81%E5%88%A0%E9%99%A4%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%8F%AF%E8%AE%A1%E7%AE%97%E5%B1%9E%E6%80%A7)不要删除对象的可计算属性

**【级别】规则**

**【描述】**

delete会改变对象的布局，而delete对象的可计算属性会非常危险，而且会大幅约束语言运行时的优化从而影响执行性能。

注意：建议不删除对象的任何属性，如果有需要，建议用map和set。

**【反例】**

```javascript
// Can be replaced with the constant equivalents, such as container.aaa
delete container['aaa'];

// Dynamic, difficult-to-reason-about lookups
const name = 'name';
delete container[name];
delete container[name.toUpperCase()];
```

**【正例】**

```javascript
// 一定程度也会影响优化性能，但比删除可计算属性好一些。
delete container.aaa;

delete container[7];
```

参见：[@typescript-eslint/no-dynamic-delete](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/no-dynamic-delete.md)

# [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%BC%82%E5%B8%B8)异常

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E8%A6%81%E4%BD%BF%E7%94%A8returnbreakcontinue%E6%88%96%E6%8A%9B%E5%87%BA%E5%BC%82%E5%B8%B8%E4%BD%BFfinally%E5%9D%97%E9%9D%9E%E6%AD%A3%E5%B8%B8%E7%BB%93%E6%9D%9F)不要使用return、break、continue或抛出异常使finally块非正常结束

**【级别】规则**

**【描述】**

在finally代码块中，直接使用return、break、continue、throw语句，或由于调用方法的异常未处理，会导致finally代码块无法正常结束。非正常结束的finally代码块会影响try或catch代码块中异常的抛出，也可能会影响方法的返回值。所以要保证finally代码块正常结束。

**【反例】**

```javascript
function foo() {
  try {
    ...
    return 1;
  } catch(err) {
    ...
    return 2;
  } finally {
    return 3;
 }
}
```

**【正例】**

```javascript
function foo() {
  try {
    ...
    return 1;
  } catch(err) {
    ...
    return 2;
  } finally {
    console.log('XXX!');
  }
}
```

# [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%BC%82%E6%AD%A5)异步

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E7%A6%81%E7%94%A8%E4%B8%8D%E5%BF%85%E8%A6%81%E7%9A%84return-await)禁用不必要的return await

**【级别】规则**

**【描述】**

因为async function的返回值总是封装在Promise.resolve，return await实际上并没有做任何事情，只是在Promise resolve或reject之前增加了额外的时间。唯一有效的情况是，在try/catch语句中使用return await来捕获另一个基于Promise的函数的错误。

**【反例】**

```javascript
async function foo() {
  return await bar();
}
```

**【正例】**

```javascript
async function foo() {
  return bar();
}
async function foo() {
  await bar();
  return;
}
async function foo() {
  const baz = await bar();
  return baz;
}
async function foo() {
  try {
    return await bar();
  } catch (error) {
    // here can be executed, go on
  }
}
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E5%85%81%E8%AE%B8%E7%AD%89%E5%BE%85%E9%9D%9Ethenable%E7%9A%84%E5%80%BC)不允许等待非Thenable的值

**【级别】规则**

**【描述】**

如果await一个非Thenable的值，await会把该值转换为已正常处理的Promise，然后等待其处理结果。此时await反而会影响代码性能。

**【反例】**

```javascript
async function f3() {
  const y = await 20;
  console.log(y); // 20
}

f3();
console.log(30);

// output
// 30
// 20
```

**【正例】**

```javascript
async function f3() {
  const y = 20;
  console.log(y); // 20
}

f3();
console.log(30);

// output
// 20
// 30
```

参见：[@typescript-eslint/await-thenable](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/await-thenable.md)

# [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E7%B1%BB%E5%9E%8B)类型

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%BC%BA%E5%88%B6%E5%B0%86null%E5%92%8Cundefined%E4%BD%9C%E4%B8%BA%E7%8B%AC%E7%AB%8B%E7%B1%BB%E5%9E%8B%E6%A0%87%E6%B3%A8)强制将Null和Undefined作为独立类型标注

**【级别】规则**

**【描述】**

Null和Undefined作为独立类型标注，可以提高代码的安全性，避免空指针异常。

**【反例】**

```javascript
let userName: string;
userName = 'hello';
userName = undefined;
```

**【正例】**

```javascript
let userName: string | undefined;
userName = 'hello';
userName = undefined;
```

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%BF%85%E9%A1%BB%E6%98%BE%E5%BC%8F%E5%A3%B0%E6%98%8E%E5%87%BD%E6%95%B0%E5%8F%8A%E7%B1%BB%E6%96%B9%E6%B3%95%E7%9A%84%E8%BF%94%E5%9B%9E%E5%80%BC%E7%B1%BB%E5%9E%8B)必须显式声明函数及类方法的返回值类型

**【级别】规则**

**【描述】**

显式声明返回类型，这可确保返回值被分配给正确类型的变量；或者在没有返回值的情况下，调用代码不会尝试把undefined分配给变量。

**【反例】**

```javascript
// 没有返回值时，没有声明返回值类型为void
function test() {
  return;
}
// 没有声明返回值类型为number
function fn() {
  return 1;
};
// 没有声明返回值类型为string
let arrowFn = () => 'test';
class Test {
  // 没有返回值时，没有声明返回值类型为void
  method() {
    return;
  }
}
```

**【正例】**

```javascript
// 函数没有返回值时，显式声明返回值类型为void
function test(): void {
  return;
}
// 显式声明返回值类型为number
function fn(): number {
  return 1;
};
// 显式声明返回值类型为 string
let arrowFn = (): string => 'test';
class Test {
  // 没有返回值时，显式声明返回值类型为void
  method(): void {
    return;
  }
}
```

参见：[@typescript-eslint/explicit-function-return-type](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/explicit-function-return-type.md)

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%BC%BA%E5%88%B6%E4%BD%BF%E7%94%A8%E7%B1%BB%E5%9E%8B%E5%AF%BC%E5%87%BA%E7%9A%84%E4%B8%80%E8%87%B4%E6%80%A7)强制使用类型导出的一致性

**【级别】规则**

**【描述】**

如果导出类型（type），将导出类型和导出其他对象分开写。

**【反例】**

```javascript
interface ButtonProps {
  onClick: () => void;
}
class Button implements ButtonProps {
  onClick() {
    console.log('button!');
  }
}
export { Button, ButtonProps };
```

**【正例】**

```javascript
interface ButtonProps {
  onClick: () => void;
}
class Button implements ButtonProps {
  onClick() {
    console.log('button!');
  }
}
export { Button };
export type { ButtonProps };
```

参见：[@typescript-eslint/consistent-type-exports](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/consistent-type-exports.md)

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%BC%BA%E5%88%B6%E4%BD%BF%E7%94%A8%E7%B1%BB%E5%9E%8B%E5%AF%BC%E5%85%A5%E7%9A%84%E4%B8%80%E8%87%B4%E6%80%A7)强制使用类型导入的一致性

**【级别】规则**

**【描述】**

如果导入类型（type），将导入类型和导入其他对象分开写。

**【反例】**

```javascript
import { Foo } from 'Foo';
import Bar from 'Bar';
type T = Foo;
const x: Bar = 1;
```

**【正例】**

```javascript
import type { Foo } from 'Foo';
import type Bar from 'Bar';
type T = Foo;
const x: Bar = 1;
```

参见：[@typescript-eslint/consistent-type-imports](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/consistent-type-imports.md)

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E9%81%BF%E5%85%8D%E4%BD%BF%E7%94%A8any)避免使用any

**【级别】规则**

**【描述】**

使用了`any`类型会使所有编译时的类型检查被忽略。一般来说，这个行为不是必需的，也不符合期望。如果类型未知，要求使用`unknown` 。 当引入的三方件不是使用TS语言或者没有提供TS类型声明时，可以使用`any`来声明相关的三方件对象。

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E5%85%81%E8%AE%B8%E5%AE%9A%E4%B9%89any%E7%B1%BB%E5%9E%8B)不允许定义any类型

**【级别】规则**

**【描述】**

不允许定义any类型。它的目的是为了让类型在TS中尽量明确，帮助语言运行时优化。

**【反例】**

```javascript
const age: any = 'seventeen';
function greet(): any {}
function greet(param: Array<any>): string {}
```

**【正例】**

```javascript
const age: number = 17;
function greet(): string {}
function greet(param: Array<string>): string {}
```

参见：[@typescript-eslint/no-explicit-any](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/no-explicit-any.md)

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E5%85%81%E8%AE%B8%E4%BD%BF%E7%94%A8any%E4%BD%9C%E4%B8%BA%E5%8F%82%E6%95%B0%E4%BC%A0%E9%80%92)不允许使用any作为参数传递

**【级别】规则**

**【反例】**

```javascript
declare function foo(arg1: string, arg2: number, arg3: string): void;

const anyTyped = 1 as any;

foo(...anyTyped);
foo(anyTyped, 1, 'a');

const tuple1 = ['a', anyTyped, 'b'] as const;
foo(...tuple1);
```

**【正例】**

```javascript
declare function foo(arg1: string, arg2: number, arg3: string): void;

foo('a', 1, 'b');

const tuple1 = ['a', 1, 'b'] as const;
foo(...tuple1);
```

参见：[@typescript-eslint/no-unsafe-argument](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/no-unsafe-argument.md)

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E5%85%81%E8%AE%B8%E5%9C%A8%E8%B5%8B%E5%80%BC%E4%B8%AD%E4%BD%BF%E7%94%A8any)不允许在赋值中使用any

**【级别】规则**

**【反例】**

```javascript
const x = 1 as any,

const x: Set<string> = new Set<any>();
```

**【正例】**

```javascript
const x = 1;

const x: Set<string> = new Set<string>();
```

参见：[@typescript-eslint/no-unsafe-assignment](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/no-unsafe-assignment.md)

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E5%85%81%E8%AE%B8call%E7%B1%BB%E5%9E%8B%E4%B8%BAany%E7%9A%84%E5%8F%98%E9%87%8F)不允许call类型为any的变量

**【级别】规则**

**【反例】**

```javascript
declare const anyVar: any;
declare const nestedAny: { prop: any };

anyVar();
anyVar.a.b();

nestedAny.prop();
nestedAny.prop['a']();
```

**【正例】**

```javascript
declare const typedVar: () => void;
declare const typedNested: { prop: { a: () => void } };

typedVar();
typedNested.prop.a();
```

参见：[@typescript-eslint/no-unsafe-call](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/no-unsafe-call.md)

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E5%85%81%E8%AE%B8%E8%AE%BF%E9%97%AE%E7%B1%BB%E5%9E%8B%E4%B8%BAany%E7%9A%84%E5%AF%B9%E8%B1%A1%E7%9A%84%E6%88%90%E5%91%98)不允许访问类型为any的对象的成员

**【级别】规则**

**【反例】**

```markup
declare const anyVar: any;
declare const nestedAny: { prop: any };

anyVar.a;
anyVar.a.b;

nestedAny.prop.a;
nestedAny.prop['a'];
```

**【正例】**

```javascript
declare const properlyTyped: { prop: { a: string } };

properlyTyped.prop.a;
properlyTyped.prop['a'];
```

参见：[@typescript-eslint/no-unsafe-member-access](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/no-unsafe-member-access.md)

## [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E4%B8%8D%E5%85%81%E8%AE%B8%E5%A3%B0%E6%98%8E%E5%87%BD%E6%95%B0%E8%BF%94%E5%9B%9E%E5%80%BC%E7%B1%BB%E5%9E%8B%E4%B8%BAany%E6%88%96%E8%80%85any)不允许声明函数返回值类型为any或者any[]

**【级别】规则**

**【反例】**

```javascript
function foo1() {
  return 1 as any;
}
```

**【正例】**

```javascript
function foo1() : number {
  return 1;
}
```

参见：[@typescript-eslint/no-unsafe-return](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/no-unsafe-return.md)

# [](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md#%E5%8F%82%E8%80%83)参考

1. 《OpenHarmony JS通用编程规范》：[https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-JavaScript-coding-style-guide.md](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-JavaScript-coding-style-guide.md)
2. ESLint Rules：[https://github.com/typescript-eslint/typescript-eslint/tree/main/packages/eslint-plugin/docs/rules](https://github.com/typescript-eslint/typescript-eslint/tree/main/packages/eslint-plugin/docs/rules)
3. 《高性能JavaScript》

## 概述

本文提供应用性能敏感场景下的高性能编程建议，帮助开发者编写高性能应用。高性能编程实践是在开发过程中总结的一些高性能写法和建议。在实现业务功能时，应同步思考并理解高性能写法的原理，并将其应用于代码逻辑中。关于ArkTS编程规范，请参考[ArkTS编程规范](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-coding-style-guide)。
# ArkTS编程规范

更新时间: 2025-12-11 11:43

## 目标和适用范围

本文参考业界标准和实践，结合ArkTS语言特点，提供编码指南，以提高代码的规范性、安全性和性能。

本文适用于使用ArkTS编写的开发场景。

## 规则来源

ArkTS在保持TypeScript基本语法风格的基础上，进一步强化静态检查和分析。本文部分规则筛选自《[OpenHarmony应用TS&JS编程指南](https://gitcode.com/openharmony/docs/blob/master/zh-cn/contribute/OpenHarmony-Application-Typescript-JavaScript-coding-guide.md)》，为ArkTS语言新增的语法添加了规则，旨在提高代码可读性、执行性能。

## 章节概览

### 代码风格

包含命名和格式。

### 编程实践

包含声明与初始化、数据类型、运算与表达式、异常等。

参考了《OpenHarmony应用TS&JS编程指南》中的规则，去除了ArkTS语言不涉及的部分，并为新增的语法添加了规则。

## 术语和定义

|术语|缩略语|中文解释|
|:--|:--|:--|
|ArkTS|无|ArkTS编程语言|
|TypeScript|TS|TypeScript编程语言|
|JavaScript|JS|JavaScript编程语言|
|ESObject|无|在ArkTS跨语言调用的场景中，用以标注JS/TS对象的类型|

## 总体原则

规则分为两个级别：要求和建议。

**要求**：表示原则上应该遵从。本文所有内容目前均为针对ArkTS的要求。

**建议**：表示该条款属于最佳实践，可结合实际情况考虑是否纳入。

## 命名

### 为标识符取一个好名字，提高代码可读性

**【描述】**

好的标识符命名应遵循以下原则：

- 清晰表达意图，避免使用单个字母或非标准缩写命名。
- 使用正确的英文单词并符合英文语法，不要使用中文拼音。
- 确保语句清晰，避免歧义。

### 类名、枚举名、命名空间名采用UpperCamelCase风格

**【级别】建议**

**【描述】**

类采用首字母大写的驼峰命名法。

类名通常是名词或名词短语，例如Person、Student、Worker。不应使用动词，也应该避免类似Data、Info这样的模糊词。

**【正例】**

1. // 类名
2. class User {
3.   username: string

4.   constructor(username: string) {
5.     this.username = username;
6.   }

7.   sayHi() {
8.     console.info('hi' + this.username);
9.   }
10. }

11. // 枚举名
12. enum UserType {
13.   TEACHER = 0,
14.   STUDENT = 1
15. };

16. // 命名空间
17. namespace Base64Utils {
18.   function encrypt() {
19.     // todo encrypt
20.   }

21.   function decrypt() {
22.     // todo decrypt
23.   }
24. };

### 变量名、方法名、参数名采用lowerCamelCase风格

**【级别】建议**

**【描述】**

函数的命名通常是动词或动词短语，采用小驼峰命名。示例如下：

1. load + 属性名()
2. put + 属性名()
3. is + 布尔属性名()
4. has + 名词/形容词()
5. 动词()
6. 动词 + 宾语()
    
    变量名通常是名词或名词短语，采用小驼峰命名，便于理解。
    

**【正例】**

1. let msg = 'Hello world';

2. function sendMsg(msg: string) {
3.   // todo send message
4. }

5. let userName = 'Zhangsan';

6. function findUser(userName: string) {
7.   // todo find user by user name
8. }

### 常量名、枚举值名采用全部大写，单词间使用下划线隔开

**【级别】建议**

**【描述】**

常量命名，应该由全大写单词与下划线组成，单词间用下划线分割。常量命名要尽量表达完整的语义。

**【正例】**

1. const MAX_USER_SIZE = 10000;

2. enum UserType {
3.   TEACHER = 0,
4.   STUDENT = 1
5. };

### 避免使用否定的布尔变量名，布尔型的局部变量或方法需加上表达是非意义的前缀

**【级别】建议**

**【描述】**

布尔型的局部变量建议加上表达是非意义的前缀，比如is，也可以是has、can、should等。但是，当使用逻辑非运算符，并出现双重否定时，会出现理解问题，比如!isNotError，难以理解。因此，应避免定义否定的布尔变量名。

**【反例】**

1. let isNoError = true;
2. let isNotFound = false;

3. function empty() {}
4. function next() {}

**【正例】**

1. let isError = false;
2. let isFound = true;

3. function isEmpty() {}
4. function hasNext() {}

## 格式

### 使用空格缩进，禁止使用tab字符

**【级别】建议**

**【描述】**

只允许使用空格(space)进行缩进。

建议大部分场景优先使用2个空格，换行导致的缩进优先使用4个空格。

不允许插入制表符Tab。当前几乎所有的集成开发环境（IDE）和代码编辑器都支持配置将Tab键自动扩展为2个空格输入，应在代码编辑器中配置使用空格进行缩进。

**【正例】**

1. class DataSource {
2.   id: number = 0
3.   title: string = ''
4.   content: string = ''
5. }

6. const dataSource: DataSource[] = [
7.   {
8.     id: 1,
9.     title: 'Title 1',
10.     content: 'Content 1'
11.   },
12.   {
13.     id: 2,
14.     title: 'Title 2',
15.     content: 'Content 2'
16.   }

17. ];

18. function test(dataSource: DataSource[]) {
19.   if (!dataSource.length) {
20.     return;
21.   }

22.   for (let data of dataSource) {
23.     if (!data || !data.id || !data.title || !data.content) {
24.       continue;
25.     }
26.     // some code
27.   }

28.   // some code
29. }

### 行宽不超过120个字符

**【级别】建议**

**【描述】**

代码行宽不宜过长，否则不利于阅读。

控制行宽可以间接引导程序员缩短函数和变量的命名，减少嵌套层数，精炼注释，从而提升代码可读性。

建议每行字符数不超过120个，除非需要显著增加可读性（超过120个），且不会隐藏信息。

例外：如果一行注释包含了超过120个字符的命令或URL，则可以保持一行，以方便复制、粘贴和通过grep查找；预处理的error信息在一行便于阅读和理解，即使超过120个字符。

### 条件语句和循环语句的实现建议使用大括号

**【级别】建议**

**【描述】**

在if、for、do、while等语句的执行体加大括号{}是一种最佳实践，因为省略大括号可能导致错误，并且降低代码的清晰度。

**【反例】**

1. let condition = true;
2. if (condition)
3.   console.info('success');
4. for (let idx = 0; idx < 5; ++idx)
5.   console.info('', idx);

**【正例】**

1. let condition = true;
2. if (condition) {
3.   console.info('success');
4. }
5. for (let idx = 0; idx < 5; ++idx) {
6.   console.info('', idx);
7. }

### switch语句的case和default需缩进一层

**【级别】建议**

**【描述】**

switch的case和default要缩进一层（2个空格）。开关标签之后换行的语句，需再缩进一层（2个空格）。

**【正例】**

1. switch (condition) {
2.   case 0: {
3.     doSomething();
4.     break;
5.   }
6.   case 1: {
7.     doOtherthing();
8.     break;
9.   }
10.   default:
11.     break;
12. }

### 表达式换行需保持一致性，运算符放行末

**【级别】建议**

**【描述】**

当语句过长或可读性不佳时，需要在合适的地方进行换行。

换行时将操作符放在行末，表示“未结束，后续还有”，保持与常用的格式化工具的默认配置一致。

**【正例】**

1. // 假设条件语句超出行宽
2. if (userCount > MAX_USER_COUNT ||
3.   userCount < MIN_USER_COUNT) {
4.   doSomething();
5. }

### 多个变量定义和赋值语句不允许写在一行

**【级别】要求**

**【描述】**

每个语句的变量声明都应只声明一个变量。

这种方式更便于添加变量声明，无需考虑将分号改为逗号，以免引入错误。此外，每个语句只声明一个变量，使用调试器逐个调试也很方便，而不是一次跳过所有变量。

**【反例】**

1. let maxCount = 10, isCompleted = false;
2. let pointX, pointY;
3. pointX = 10; pointY = 0;

**【正例】**

1. let maxCount = 10;
2. let isCompleted = false;
3. let pointX = 0;
4. let pointY = 0;

### 空格应该突出关键字和重要信息，避免不必要的空格

**【级别】建议**

**【描述】**

空格应该突出关键字和重要信息。总体建议如下：

1. if, for, while, switch等关键字与左括号(之间加空格。
2. 在函数定义和调用时，函数名称与参数列表的左括号(之间不加空格。
3. 关键字else或catch与其之前的大括号}之间加空格。
4. 任何打开大括号({)之前加空格，有两个例外：
    
    a) 在作为函数的第一个参数或数组中的第一个元素时，对象之前不用加空格，例如：foo({ name: 'abc' })。
    
    b) 在模板中，不用加空格，例如：abc${name}。
    
5. 二元操作符(+ - * = < > <= >= === !== && ||)前后加空格；三元操作符(? :)符号两侧均加空格。
6. 数组初始化中的逗号和函数中多个参数之间的逗号后加空格。
7. 在逗号(,)或分号(;)之前不加空格。
8. 数组的中括号([])内侧不要加空格。
9. 不要出现多个连续空格。在某行中，多个空格若不是用来作缩进的，通常是个错误。

**【反例】**

1. // if 和左括号 ( 之间没有加空格
2. if(isJedi) {
3.   fight();
4. }

5. // 函数名fight和左括号 ( 之间加了空格
6. function fight (): void {
7.   console.info('Swooosh!');
8. }

**【正例】**

1. // if 和左括号之间加一个空格
2. if (isJedi) {
3.   fight();
4. }

5. // 函数名fight和左括号 ( 之间不加空格
6. function fight(): void {
7.   console.info('Swooosh!');
8. }

**【反例】**

1. if (flag) {
2.   // ...
3. }else {  // else 与其前面的大括号 } 之间没有加空格
4.   // ...
5. }

**【正例】**

1. if (flag) {
2.   // ...
3. } else {  // else 与其前面的大括号 } 之间增加空格
4.   // ...
5. }

**【正例】**

1. function foo() {  // 函数声明时，左大括号 { 之前加个空格
2.   // ...
3. }

4. bar('attr', {  // 左大括号前加个空格
5.   age: '1 year',
6.   sbreed: 'Bernese Mountain Dog',
7. });

**【正例】**

1. const arr = [1, 2, 3];  // 数组初始化中的逗号后面加个空格，逗号前面不加空格
2. myFunc(bar, foo, baz);  // 函数的多个参数之间的逗号后加个空格，逗号前面不加空格

### 建议字符串使用单引号

**【级别】建议**

**【描述】**

为了保持代码一致性和可读性，建议使用单引号。

**【反例】**

1. let message = "world";
2. console.info(message);

**【正例】**

1. let message = 'world';
2. console.info(message);

### 对象字面量属性超过4个，需要都换行

**【级别】建议**

**【描述】**

对象字面量的属性应保持一致的格式：要么每个属性都换行，要么所有属性都在同一行。当对象字面量的属性超过4个时，建议统一换行。

**【反例】**

1. interface I {
2.   name: string
3.   age: number
4.   value: number
5.   sum: number
6.   foo: boolean
7.   bar: boolean
8. }

9. let obj: I = { name: 'tom', age: 16, value: 1, sum: 2, foo: true, bar: false }

**【正例】**

1. interface I {
2.   name: string
3.   age: number
4.   value: number
5.   sum: number
6.   foo: boolean
7.   bar: boolean
8. }

9. let obj: I = {
10.   name: 'tom',
11.   age: 16,
12.   value: 1,
13.   sum: 2,
14.   foo: true,
15.   bar: false
16. }

### 把else/catch放在if/try代码块关闭括号的同一行

**【级别】建议**

**【描述】**

编写条件语句时，建议将else放在if代码块关闭括号的同一行。同样，编写异常处理语句时，建议将catch放在try代码块关闭括号的同一行。

**【反例】**

1. if (isOk) {
2.   doThing1();
3.   doThing2();
4. }
5. else {
6.   doThing3();
7. }

**【正例】**

1. if (isOk) {
2.   doThing1();
3.   doThing2();
4. } else {
5.   doThing3();
6. }

**【反例】**

1. try {
2.   doSomething();
3. }
4. catch (err) {
5.   // 处理错误
6. }

**【正例】**

1. try {
2.   doSomething();
3. } catch (err) {
4.   // 处理错误
5. }

### 大括号{和语句在同一行

**【级别】建议**

**【描述】**

应保持一致的大括号风格。建议将大括号置于控制语句或声明语句的同一行。

**【反例】**

1. function foo()
2. {
3.   // ...
4. }

**【正例】**

1. function foo() {
2.   // ...
3. }

## 编程实践

### 建议添加类属性的可访问修饰符

**【级别】建议**

**【描述】**

ArkTS提供了private, protected和public可访问修饰符。默认情况下，属性的可访问修饰符为public。选取适当的可访问修饰符可以提升代码的安全性和可读性。注意：如果类中包含private属性，无法通过对象字面量初始化该类。

**【反例】**

1. class C {
2.   count: number = 0

3.   getCount(): number {
4.     return this.count
5.   }
6. }

**【正例】**

1. class C {
2.   private count: number = 0

3.   public getCount(): number {
4.     return this.count
5.   }
6. }

### 不建议省略浮点数小数点前后的0

**【级别】建议**

**【描述】**

ArkTS中，浮点值包含一个小数点，不要求小数点之前或之后必须有一个数字。在小数点前面和后面都添加数字可以提高代码的可读性。

**【反例】**

1. const num = .5;
2. const num = 2.;
3. const num = -.7;

**【正例】**

1. const num = 0.5;
2. const num = 2.0;
3. const num = -0.7;

### 判断变量是否为Number.NaN时必须使用Number.isNaN()方法

**【级别】要求**

**【描述】**

在ArkTS中，Number.NaN是Number类型的一个特殊值。它被用来表示非数值，这里的数值是指在IEEE浮点数算术标准中定义的双精度64位格式的值。

在ArkTS中，Number.NaN的独特之处在于它不等于任何值，包括其本身。与Number.NaN进行比较时，结果是令人困惑的：Number.NaN !== Number.NaN 和 Number.NaN != Number.NaN 的值都是 true。

因此，必须使用Number.isNaN()函数来测试一个值是否是Number.NaN。

**【反例】**

1. if (foo == Number.NaN) {
2.   // ...
3. }

4. if (foo != Number.NaN) {
5.   // ...
6. }

**【正例】**

1. if (Number.isNaN(foo)) {
2.   // ...
3. }

4. if (!Number.isNaN(foo)) {
5.   // ...
6. }

### 数组遍历优先使用Array对象方法

**【级别】要求**

**【描述】**

对于数组遍历，应该优先使用Array对象方法，如：forEach(), map(), every(), filter(), find(), findIndex(), reduce(), some()。

**【反例】**

1. const numbers = [1, 2, 3, 4, 5];
2. // 依赖已有数组来创建新的数组时，通过for遍历，生成一个新数组
3. const increasedByOne: number[] = [];
4. for (let i = 0; i < numbers.length; i++) {
5.   increasedByOne.push(numbers[i] + 1);
6. }

**【正例】**

1. const numbers = [1, 2, 3, 4, 5];
2. // better: 使用map方法是更好的方式
3. const increasedByOne: number[] = numbers.map(num => num + 1);

### 不要在控制性条件表达式中执行赋值操作

**【级别】要求**

**【描述】**

控制性条件表达式用于 if、while、for 以及 ?: 等条件判断语句中。

在控制性条件表达式中执行赋值容易导致意外行为，且降低代码的可读性。

**【反例】**

1. // 在控制性判断中赋值不易理解
2. if (isFoo = false) {
3.   // ...
4. }

**【正例】**

1. const isFoo = false; // 在上面赋值，if条件判断中直接使用
2. if (isFoo) {
3.   // ...
4. }

### 在finally代码块中，不要使用return、break、continue或抛出异常，避免finally块非正常结束

**【级别】要求**

**【描述】**

在finally代码块中，直接使用return、break、continue、throw语句或调用方法时未处理异常，会导致finally代码块无法正常结束。finally代码块异常结束会影响try或catch代码块中异常的抛出，也可能影响方法的返回值。因此，必须确保finally代码块正常结束。

**【反例】**

1. function foo() {
2.   try {
3.     // ...
4.     return 1;
5.   } catch (err) {
6.     // ...
7.     return 2;
8.   } finally {
9.     return 3;
10.  }
11. }

**【正例】**

1. function foo() {
2.   try {
3.     // ...
4.     return 1;
5.   } catch (err) {
6.     // ...
7.     return 2;
8.   } finally {
9.     console.info('XXX!');
10.   }
11. }

### 避免使用ESObject

**【级别】建议**

**【描述】**

ESObject主要用于ArkTS和TS/JS的跨语言调用场景中的类型标注。在非跨语言调用场景中使用ESObject标注类型，会引入不必要的跨语言调用，导致额外的性能开销。

**【反例】**

1. // lib.ets
2. export interface I {
3.   sum: number
4. }

5. export function getObject(value: number): I {
6.   let obj: I = { sum: value };
7.   return obj
8. }

9. // app.ets
10. import { getObject } from 'lib'
11. let obj: ESObject = getObject(123);

**【正例】**

1. // lib.ets
2. export interface I {
3.   sum: number
4. }

5. export function getObject(value: number): I {
6.   let obj: I = { sum: value };
7.   return obj
8. }

9. // app.ets
10. import { getObject, I } from 'lib'
11. let obj: I = getObject(123);

### 使用T[]表示数组类型

**【级别】建议**

**【描述】**

ArkTS提供了两种数组类型的表示方式：T[]和Array<T>。建议所有数组类型均使用T[]表示，以提高代码可读性。

**【反例】**

1. let x: Array<number> = [1, 2, 3];
2. let y: Array<string> = ['a', 'b', 'c'];

**【正例】**

1. // 统一使用T[]语法
2. let x: number[] = [1, 2, 3];
3. let y: string[] = ['a', 'b', 'c'];
## 声明与表达式

### 使用const声明不变的变量

不变的变量推荐使用const声明。

1. const index = 10000; // 该变量在后续过程中未发生改变，建议声明成常量

### number类型变量避免整型和浮点型混用

针对number类型，运行时在优化时会区分整型和浮点型数据。建议避免在初始化后改变数据类型。

1. let intNum = 1;
2. intNum = 1.1;  // 该变量在声明时为整型数据，建议后续不要赋值浮点型数据

3. let doubleNum = 1.1;
4. doubleNum = 1;  // 该变量在声明时为浮点型数据，建议后续不要赋值整型数据

### 数值计算避免溢出

常见的可能导致溢出的数值计算包括如下场景，溢出之后，会导致引擎走入慢速的溢出逻辑分支处理，影响后续的性能。

- 针对加法、减法、乘法、指数运算等运算操作，应避免数值大于INT32_MAX（2147483647）或小于INT32_MIN（-2147483648）。
    
- 针对&（and）、>>>（无符号右移）等运算操作，应避免数值大于INT32_MAX。
    

### 循环中常量提取，减少属性访问次数

如果常量在循环中不会改变，可以将其提取到循环外部，减少访问次数。

1. class Time {
2.   static start: number = 0;
3.   static info: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
4. }

5. function getNum(num: number): number {
6.   let total: number = 348;
7.   for (let index: number = 0x8000; index > 0x8; index >>= 1) {
8.     // 此处会多次对Time的info及start进行查找，并且每次查找出来的值是相同的
9.     total += ((Time.info[num - Time.start] & index) !== 0) ? 1 : 0;
10.   }
11.   return total;
12. }

优化后的代码如下，可以将Time.info[num - Time.start]提取为常量，这样可以显著减少属性访问次数，提升性能。

1. class Time {
2.   static start: number = 0;
3.   static info: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
4. }

5. function getNum(num: number): number {
6.   let total: number = 348;
7.   const info = Time.info[num - Time.start];  // 从循环中提取不变量
8.   for (let index: number = 0x8000; index > 0x8; index >>= 1) {
9.     if ((info & index) != 0) {
10.       total++;
11.     }
12.   }
13.   return total;
14. }

## 函数

### 建议使用参数传递函数外的变量

使用闭包会造成额外的开销。在性能敏感场景中，建议使用参数传递函数外的变量替代。

1. let arr = [0, 1, 2];

2. function foo(): number {
3.   return arr[0] + arr[1];
4. }

5. foo();

建议使用参数传递函数外部的变量，以替代使用闭包。

1. let arr = [0, 1, 2];

2. function foo(array: number[]): number {
3.   return array[0] + array[1];
4. }

5. foo(arr);

### 避免使用可选参数

函数的可选参数表示参数可能为undefined，在函数内部使用该参数时，需要进行非空值的判断，造成额外的开销。

1. function add(left?: number, right?: number): number | undefined {
2.   if (left != undefined && right != undefined) {
3.     return left + right;
4.   }
5.   return undefined;
6. }

根据业务需求，将函数参数声明为必选参数。考虑使用默认参数。

1. function add(left: number = 0, right: number = 0): number {
2.   return left + right;
3. }

## 数组

### 数值数组推荐使用TypedArray

涉及纯数值计算时，推荐使用TypedArray数据结构。

优化前的代码示例：

1. const arr1 = new Array<number>(1, 2, 3);
2. const arr2 = new Array<number>(4, 5, 6);
3. let res = new Array<number>(3);
4. for (let i = 0; i < 3; i++) {
5.   res[i] = arr1[i] + arr2[i];
6. }

优化后的代码示例：

1. const typedArray1 = Int8Array.from([1, 2, 3]);
2. const typedArray2 = Int8Array.from([4, 5, 6]);
3. let res = new Int8Array(3);
4. for (let i = 0; i < 3; i++) {
5.   res[i] = typedArray1[i] + typedArray2[i];
6. }

### 避免使用稀疏数组

运行时在分配超过1024大小的数组或稀疏数组时，会采用hash表来存储元素。在该模式下，访问数组元素速度较慢。代码开发时应避免数组变成稀疏数组。

1. // 直接分配100000大小的数组，运行时会处理成用hash表来存储元素
2. let count = 100000;
3. let result: number[] = new Array(count);

4. // 创建数组后，直接在9999处赋值，会变成稀疏数组
5. let result: number[] = new Array();
6. result[9999] = 0;

### 避免使用联合类型数组

避免使用联合类型数组。避免在数值数组中混合使用整型数据和浮点型数据。

1. let arrNum: number[] = [1, 1.1, 2];  // 数值数组中混合使用整型数据和浮点型数据

2. let arrUnion: (number | string)[] = [1, 'hello'];  // 联合类型数组

根据业务需求，将相同类型的数据放在同一数组中。

1. let arrInt: number[] = [1, 2, 3];
2. let arrDouble: number[] = [0.1, 0.2, 0.3];
3. let arrString: string[] = ['hello', 'world'];

## 异常

### 避免频繁抛出异常

创建异常时会构造异常的栈帧，造成性能损耗。在性能敏感场景下，如for循环语句中，应避免频繁抛出异常。

优化前的代码示例：

1. function div(a: number, b: number): number {
2.   if (a <= 0 || b <= 0) {
3.     throw new Error('Invalid numbers.');
4.   }
5.   return a / b;
6. }

7. function sum(num: number): number {
8.   let sum = 0;
9.   try {
10.     for (let t = 1; t < 100; t++) {
11.       sum += div(t, num);
12.     }
13.   } catch (e) {
14.     console.info(e.message);
15.   }
16.   return sum;
17. }

优化后的代码示例：

1. function div(a: number, b: number): number {
2.   if (a <= 0 || b <= 0) {
3.     return NaN;
4.   }
5.   return a / b;
6. }

7. function sum(num: number): number {
8.   let sum = 0;
9.   for (let t = 1; t < 100; t++) {
10.     // 直接拦截异常场景，避免频繁抛出异常
11.     if (num <= 0) {
12.       console.info('Invalid numbers.');
13.     }
14.     sum += div(t, num);
15.   }
16.   return sum;
17. }