# 适配指导案例

更新时间: 2025-12-16 16:34

本文通过具体应用场景中的案例，提供在ArkTS语法规则下将TS代码适配成ArkTS代码的建议。各章以ArkTS语法规则的英文名称命名，每个案例展示适配前的TS代码和适配后的ArkTS代码。

## arkts-identifiers-as-prop-names

当属性名是有效的标识符（即不包含特殊字符、空格等，并且不以数字开头），可以直接使用而无需引号。

**应用代码**

1. interface W {
2.   bundleName: string
3.   action: string
4.   entities: string[]
5. }

6. let wantInfo: W = {
7.   'bundleName': 'com.huawei.hmos.browser',
8.   'action': 'ohos.want.action.viewData',
9.   'entities': ['entity.system.browsable']
10. }

**建议改法**

1. interface W {
2.   bundleName: string
3.   action: string
4.   entities: string[]
5. }

6. let wantInfo: W = {
7.   bundleName: 'com.huawei.hmos.browser',
8.   action: 'ohos.want.action.viewData',
9.   entities: ['entity.system.browsable']
10. }

## arkts-no-any-unknown

### 按照业务逻辑，将代码中的any, unknown改为具体的类型

1. function printObj(obj: any) {
2.   console.info(obj);
3. }

4. printObj('abc'); // abc

**建议改法**

1. function printObj(obj: string) {
2.   console.info(obj);
3. }

4. printObj('abc'); // abc

### 标注JSON.parse返回值类型

**应用代码**

1. class A {
2.   v: number = 0
3.   s: string = ''

4.   foo(str: string) {
5.     let tmpStr = JSON.parse(str);
6.     if (tmpStr.add != undefined) {
7.       this.v = tmpStr.v;
8.       this.s = tmpStr.s;
9.     }
10.   }
11. }

**建议改法**

1. class A {
2.   v: number = 0
3.   s: string = ''

4.   foo(str: string) {
5.     let tmpStr: Record<string, Object> = JSON.parse(str);
6.     if (tmpStr.add != undefined) {
7.       this.v = tmpStr.v as number;
8.       this.s = tmpStr.s as string;
9.     }
10.   }
11. }

### 使用Record类型

**应用代码**

1. function printProperties(obj: any) {
2.   console.info(obj.name);
3.   console.info(obj.value);
4. }

**建议改法**

1. function printProperties(obj: Record<string, Object>) {
2.   console.info(obj.name as string);
3.   console.info(obj.value as string);
4. }

## arkts-no-call-signature

使用函数类型进行替代。

**应用代码**

1. interface I {
2.   (value: string): void;
3. }

4. function foo(fn: I) {
5.   fn('abc');
6. }

7. foo((value: string) => {
8.   console.info(value);
9. })

**建议改法**

1. type I = (value: string) => void

2. function foo(fn: I) {
3.   fn('abc');
4. }

5. foo((value: string) => {
6.   console.info(value);
7. })

## arkts-no-ctor-signatures-type

使用工厂函数（() => Instance）替代构造函数签名。

**应用代码**

1. class Controller {
2.   value: string = ''

3.   constructor(value: string) {
4.     this.value = value;
5.   }
6. }

7. type ControllerConstructor = {
8.   new (value: string): Controller;
9. }

10. class testMenu {
11.   controller: ControllerConstructor = Controller
12.   createController() {
13.     if (this.controller) {
14.       return new this.controller('123');
15.     }
16.     return null;
17.   }
18. }

19. let t = new testMenu();
20. console.info(t.createController()!.value);

**建议改法**

1. class Controller {
2.   value: string = ''

3.   constructor(value: string) {
4.     this.value = value;
5.   }
6. }

7. type ControllerConstructor = () => Controller;

8. class testMenu {
9.   controller: ControllerConstructor = () => {
10.     return new Controller('abc');
11.   }

12.   createController() {
13.     if (this.controller) {
14.       return this.controller();
15.     }
16.     return null;
17.   }
18. }

19. let t: testMenu = new testMenu();
20. console.info(t.createController()!.value);

## arkts-no-indexed-signatures

使用Record类型进行替代。

**应用代码**

1. function foo(data: { [key: string]: string }) {
2.   data['a'] = 'a';
3.   data['b'] = 'b';
4.   data['c'] = 'c';
5. }

**建议改法**

1. function foo(data: Record<string, string>) {
2.   data['a'] = 'a';
3.   data['b'] = 'b';
4.   data['c'] = 'c';
5. }

## arkts-no-typing-with-this

使用具体类型替代this。

**应用代码**

1. class C {
2.   getInstance(): this {
3.     return this;
4.   }
5. }

**建议改法**

1. class C {
2.   getInstance(): C {
3.     return this;
4.   }
5. }

## arkts-no-ctor-prop-decls

显式声明类属性，并在构造函数中手动赋值。

**应用代码**

1. class Person {
2.   constructor(readonly name: string) {}

3.   getName(): string {
4.     return this.name;
5.   }
6. }

**建议改法**

1. class Person {
2.   name: string
3.   constructor(name: string) {
4.     this.name = name;
5.   }

6.   getName(): string {
7.     return this.name;
8.   }
9. }

## arkts-no-ctor-signatures-iface

使用type定义工厂函数或普通函数类型。

**应用代码**

1. class Controller {
2.   value: string = ''

3.   constructor(value: string) {
4.     this.value = value;
5.   }
6. }

7. interface ControllerConstructor {
8.   new (value: string): Controller;
9. }

10. class testMenu {
11.   controller: ControllerConstructor = Controller
12.   createController() {
13.     if (this.controller) {
14.       return new this.controller('abc');
15.     }
16.     return null;
17.   }
18. }

19. let t = new testMenu();
20. console.info(t.createController()!.value);

**建议改法**

1. class Controller {
2.   value: string = ''

3.   constructor(value: string) {
4.     this.value = value;
5.   }
6. }

7. type ControllerConstructor = () => Controller;

8. class testMenu {
9.   controller: ControllerConstructor = () => {
10.     return new Controller('abc');
11.   }

12.   createController() {
13.     if (this.controller) {
14.       return this.controller();
15.     }
16.     return null;
17.   }
18. }

19. let t: testMenu = new testMenu();
20. console.info(t.createController()!.value);

## arkts-no-props-by-index

可以将对象转换为Record类型，以便访问其属性。

**应用代码**

1. function foo(params: Object) {
2.     let funNum: number = params['funNum'];
3.     let target: string = params['target'];
4. }

**建议改法**

1. function foo(params: Record<string, string | number>) {
2.     let funNum: number = params['funNum'] as number;
3.     let target: string = params['target'] as string;
4. }

## arkts-no-inferred-generic-params

所有泛型调用都应显式标注泛型参数类型，如 Map<string, T>、.map<T>()。

**应用代码**

1. class A {
2.   str: string = ''
3. }
4. class B extends A {}
5. class C extends A {}

6. let arr: Array<A> = [];

7. let originMenusMap:Map<string, C> = new Map(arr.map(item => [item.str, (item instanceof C) ? item: null]));

**建议改法**

1. class A {
2.   str: string = ''
3. }
4. class B extends A {}
5. class C extends A {}

6. let arr: Array<A> = [];

7. let originMenusMap: Map<string, C | null> = new Map<string, C | null>(arr.map<[string, C | null]>(item => [item.str, (item instanceof C) ? item: null]));

**原因**

(item instanceof C) ? item: null 需要声明类型为C | null，由于编译器无法推导出map的泛型类型参数，需要显式标注。

## arkts-no-regexp-literals

使用new RegExp(pattern, flags) 构造函数替代RegExp字面量。

**应用代码**

1. let regex: RegExp = /\s*/g;

**建议改法**

1. let regexp: RegExp = new RegExp('\\s*','g');

**原因**

如果正则表达式中使用了标志符，需要将其作为new RegExp()的参数。

## arkts-no-untyped-obj-literals

### 从SDK中导入类型，标注object literal类型

**应用代码**

1. const area = { // 没有写明类型 不方便维护
2.   pixels: new ArrayBuffer(8),
3.   offset: 0,
4.   stride: 8,
5.   region: { size: { height: 1,width:2 }, x: 0, y: 0 }
6. }

**建议改法**

1. import { image } from '@kit.ImageKit';

2. const area: image.PositionArea = { // 写明具体类型
3.   pixels: new ArrayBuffer(8),
4.   offset: 0,
5.   stride: 8,
6.   region: { size: { height: 1, width: 2 }, x: 0, y: 0 }
7. }

### 用class为object literal标注类型，要求class的构造函数无参数

**应用代码**

1. class Test {
2.   value: number = 1
3.   // 有构造函数
4.   constructor(value: number) {
5.     this.value = value;
6.   }
7. }

8. let t: Test = { value: 2 };

**建议改法1**

1. // 去除构造函数
2. class Test {
3.   value: number = 1
4. }

5. let t: Test = { value: 2 };

**建议改法2**

1. // 使用new
2. class Test {
3.   value: number = 1

4.   constructor(value: number) {
5.     this.value = value;
6.   }
7. }

8. let t: Test = new Test(2);

**原因**

1. class C {
2.   value: number = 1

3.   constructor(n: number) {
4.     if (n < 0) {
5.       throw new Error('Negative');
6.     }
7.     this.value = n;
8.   }
9. }

10. let s: C = new C(-2);     //抛出异常
11. let t: C = { value: -2 };    //ArkTS不支持

如果允许使用C来标注object literal的类型，变量t会导致行为的二义性。ArkTS禁止通过object literal绕过这一行为。

### 用class/interface为object literal标注类型，要求使用identifier作为object literal的key

**应用代码**

1. class Test {
2.   value: number = 0
3. }

4. let arr: Test[] = [
5.   {
6.     'value': 1
7.   },
8.   {
9.     'value': 2
10.   },
11.   {
12.     'value': 3
13.   }
14. ]

**建议改法**

1. class Test {
2.   value: number = 0
3. }
4. let arr: Test[] = [
5.   {
6.     value: 1
7.   },
8.   {
9.     value: 2
10.   },
11.   {
12.     value: 3
13.   }
14. ]

### 使用Record类型为object literal标注类型，要求使用字符串作为object literal的key

**应用代码**

1. let obj: Record<string, number | string> = {
2.   value: 123,
3.   name: 'abc'
4. }

**建议改法**

1. let obj: Record<string, number | string> = {
2.   'value': 123,
3.   'name': 'abc'
4. }

### 函数参数类型包含index signature

**应用代码**

1. function foo(obj: { [key: string]: string}): string {
2.   if (obj != undefined && obj != null) {
3.     return obj.value1 + obj.value2;
4.   }
5.   return '';
6. }

**建议改法**

1. function foo(obj: Record<string, string>): string {
2.   if (obj != undefined && obj != null) {
3.     return obj.value1 + obj.value2;
4.   }
5.   return '';
6. }

### 函数实参使用了object literal

**应用代码**

1. (fn) => {
2.   fn({ value: 123, name:'' });
3. }

**建议改法**

1. class T {
2.   value: number = 0
3.   name: string = ''
4. }

5. (fn: (v: T) => void) => {
6.   fn({ value: 123, name: '' });
7. }

### class/interface 中包含方法

**应用代码**

1. interface T {
2.   foo(value: number): number
3. }

4. let t:T = { foo: (value) => { return value } };

**建议改法1**

1. interface T {
2.   foo: (value: number) => number
3. }

4. let t:T = { foo: (value) => { return value } };

**建议改法2**

1. class T {
2.   foo: (value: number) => number = (value: number) => {
3.     return value;
4.   }
5. }

6. let t:T = new T();

**原因**

class/interface中声明的方法应被所有实例共享。ArkTS不支持通过object literal改写实例方法。ArkTS支持函数类型的属性。

### export default对象

**应用代码**

1. export default {
2.   onCreate() {
3.     // ...
4.   },
5.   onDestroy() {
6.     // ...
7.   }
8. }

**建议改法**

1. class Test {
2.   onCreate() {
3.     // ...
4.   }
5.   onDestroy() {
6.     // ...
7.   }
8. }

9. export default new Test()

### 通过导入namespace获取类型

**应用代码**

1. // test.d.ets
2. declare namespace test {
3.   interface I {
4.     id: string;
5.     type: number;
6.   }

7.   function foo(name: string, option: I): void;
8. }

9. export default test;

10. // app.ets
11. import test from 'test';

12. let option = { id: '', type: 0 };
13. test.foo('', option);

**建议改法**

1. // test.d.ets
2. declare namespace test {
3.   interface I {
4.     id: string;
5.     type: number;
6.   }

7.   function foo(name: string, option: I): void;
8. }

9. export default test;

10. // app.ets
11. import test from 'test';

12. let option: test.I = { id: '', type: 0 };
13. test.foo('', option);

**原因**

对象字面量缺少类型，根据test.foo分析可以得知，option的类型来源于声明文件，那么只需要将类型导入即可。

在test.d.ets中，I定义在namespace中。在ets文件中，先导入namespace，再通过名称获取相应的类型。

### object literal传参给Object类型

**应用代码**

1. function emit(event: string, ...args: Object[]): void {}

2. emit('', {
3.   'action': 11,
4.   'outers': false
5. });

**建议改法**

1. function emit(event: string, ...args: Object[]): void {}

2. let emitArg: Record<string, number | boolean> = {
3.    'action': 11,
4.    'outers': false
5. }

6. emit('', emitArg);

## arkts-no-obj-literals-as-types

使用interface显式定义结构类型。

**应用代码**

1. type Person = { name: string, age: number }

**建议改法**

1. interface Person {
2.   name: string,
3.   age: number
4. }

## arkts-no-noninferrable-arr-literals

显式声明数组元素的类型（使用interface或class），并为数组变量添加类型注解。

**应用代码**

1. let permissionList = [
2.   { name: '设备信息', value: '用于分析设备的续航、通话、上网、SIM卡故障等' },
3.   { name: '麦克风', value: '用于反馈问题单时增加语音' },
4.   { name: '存储', value: '用于反馈问题单时增加本地文件附件' }
5. ]

**建议改法**

为对象字面量声明类型。

1. class PermissionItem {
2.   name?: string
3.   value?: string
4. }

5. let permissionList: PermissionItem[] = [
6.   { name: '设备信息', value: '用于分析设备的续航、通话、上网、SIM卡故障等' },
7.   { name: '麦克风', value: '用于反馈问题单时增加语音' },
8.   { name: '存储', value: '用于反馈问题单时增加本地文件附件' }
9. ]

## arkts-no-method-reassignment

使用函数类型的类字段（class field）代替原型方法。

**应用代码**

1. class C {
2.   add(left: number, right: number): number {
3.     return left + right;
4.   }
5. }

6. function sub(left: number, right: number): number {
7.   return left - right;
8. }

9. let c1 = new C();
10. c1.add = sub;

**建议改法**

1. class C {
2.   add: (left: number, right: number) => number =
3.     (left: number, right: number) => {
4.       return left + right;
5.     }
6. }

7. function sub(left: number, right: number): number {
8.   return left - right;
9. }

10. let c1 = new C();
11. c1.add = sub;

## arkts-no-polymorphic-unops

使用 Number.parseInt()、new Number() 等显式转换函数。

**应用代码**

1. let a = +'5'; // 使用操作符隐式转换
2. let b = -'5';
3. let c = ~'5';
4. let d = +'string';

**建议改法**

1. let a = Number.parseInt('5'); // 使用Number.parseInt显示转换
2. let b = -Number.parseInt('5');
3. let c = ~Number.parseInt('5');
4. let d = new Number('123');

## arkts-no-type-query

使用类、接口或类型别名替代typeof，避免依赖变量做类型推导。

**应用代码**

1. // module1.ts
2. class C {
3.   value: number = 0
4. }

5. export let c = new C()

6. // module2.ts
7. import { c } from './module1'
8. let t: typeof c = { value: 123 };

**建议改法**

1. // module1.ts
2. class C {
3.   value: number = 0
4. }

5. export { C }

6. // module2.ts
7. import { C } from './module1'
8. let t: C = { value: 123 };

## arkts-no-in

### 使用Object.keys判断属性是否存在

**应用代码**

1. function test(str: string, obj: Record<string, Object>) {
2.   return str in obj;
3. }

**建议改法**

1. function test(str: string, obj: Record<string, Object>) {
2.   for (let i of Object.keys(obj)) {
3.     if (i == str) {
4.       return true;
5.     }
6.   }
7.   return false;
8. }

## arkts-no-destruct-assignment

使用索引访问元素或手动赋值代替解构赋值。

**应用代码**

1. let map = new Map<string, string>([['a', 'a'], ['b', 'b']]);
2. for (let [key, value] of map) {
3.   console.info(key);
4.   console.info(value);
5. }

**建议改法**

使用数组。

1. let map = new Map<string, string>([['a', 'a'], ['b', 'b']]);
2. for (let arr of map) {
3.   let key = arr[0];
4.   let value = arr[1];
5.   console.info(key);
6.   console.info(value);
7. }

## arkts-no-types-in-catch

使用无类型 catch (error)，然后通过类型断言处理。

**应用代码**

1. import { BusinessError } from '@kit.BasicServicesKit'

2. try {
3.   // ...
4. } catch (e: BusinessError) {
5.   console.error(e.message, e.code);
6. }

**建议改法**

1. import { BusinessError } from '@kit.BasicServicesKit'

2. try {
3.   // ...
4. } catch (error) {
5.   let e: BusinessError = error as BusinessError;
6.   console.error(e.message, e.code);
7. }

## arkts-no-for-in

使用 Object.entries(obj) + for of 替代 for in。

**应用代码**

1. interface Person {
2.   [name: string]: string
3. }
4. let p: Person = {
5.   name: 'tom',
6.   age: '18'
7. };

8. for (let t in p) {
9.   console.info(p[t]);  // info: "tom", "18"
10. }

**建议改法**

1. let p: Record<string, string> = {
2.   'name': 'tom',
3.   'age': '18'
4. };

5. for (let ele of Object.entries(p)) {
6.   console.info(ele[1]);  // info: "tom", "18"
7. }

## arkts-no-mapped-types

使用 Record<K, T> 替代映射类型。

**应用代码**

1. class C {
2.   a: number = 0
3.   b: number = 0
4.   c: number = 0
5. }
6. type OptionsFlags = {
7.   [Property in keyof C]: string
8. }

**建议改法**

1. class C {
2.   a: number = 0
3.   b: number = 0
4.   c: number = 0
5. }

6. type OptionsFlags = Record<keyof C, string>

## arkts-limited-throw

将对象转换为Error，或创建新的Error实例抛出。

**应用代码**

1. import { BusinessError } from '@kit.BasicServicesKit'

2. function ThrowError(error: BusinessError) {
3.   throw error;
4. }

**建议改法**

1. import { BusinessError } from '@kit.BasicServicesKit'

2. function ThrowError(error: BusinessError) {
3.   throw error as Error;
4. }

**原因**

throw语句中值的类型必须为Error或者其继承类，如果继承类是一个泛型，会有编译期报错。建议使用as将类型转换为Error。

## arkts-no-standalone-this

### 函数内使用this

**应用代码**

1. function foo() {
2.   console.info(this.value);
3. }

4. let obj = { value: 'abc' };
5. foo.apply(obj);

**建议改法1**

使用类的方法实现,如果该方法被多个类使用,可以考虑采用继承的机制。

1. class Test {
2.   value: string = ''
3.   constructor (value: string) {
4.     this.value = value
5.   }

6.   foo() {
7.     console.info(this.value);
8.   }
9. }

10. let obj: Test = new Test('abc');
11. obj.foo();

**建议改法2**

将this作为参数传入。

1. function foo(obj: Test) {
2.   console.info(obj.value);
3. }

4. class Test {
5.   value: string = ''
6. }

7. let obj: Test = { value: 'abc' };
8. foo(obj);

**建议改法3**

将属性作为参数传入。

1. function foo(value: string) {
2.   console.info(value);
3. }

4. class Test {
5.   value: string = ''
6. }

7. let obj: Test = { value: 'abc' };
8. foo(obj.value);

### class的静态方法内使用this

**应用代码**

1. class Test {
2.   static value: number = 123
3.   static foo(): number {
4.     return this.value
5.   }
6. }

**建议改法**

1. class Test {
2.   static value: number = 123
3.   static foo(): number {
4.     return Test.value
5.   }
6. }

## arkts-no-spread

使用Object.assign()、手动赋值或数组方法替代扩展运算符。

**应用代码**

1. // test.d.ets
2. declare namespace test {
3.   interface I {
4.     id: string;
5.     type: number;
6.   }

7.   function foo(): I;
8. }

9. export default test

10. // app.ets
11. import test from 'test';

12. let t: test.I = {
13.   ...test.foo(),
14.   type: 0
15. }

**建议改法**

1. // test.d.ets
2. declare namespace test {
3.   interface I {
4.     id: string;
5.     type: number;
6.   }

7.   function foo(): I;
8. }

9. export default test

10. // app.ets
11. import test from 'test';

12. let t: test.I = test.foo();
13. t.type = 0;

**原因**

ArkTS中，对象布局在编译期是确定的。如果需要将一个对象的所有属性展开赋值给另一个对象可以通过逐个属性赋值语句完成。在本例中，需要展开的对象和赋值的目标对象类型恰好相同，可以通过改变该对象属性的方式重构代码。

## arkts-no-ctor-signatures-funcs

在class内声明属性，而不是在构造函数上。

**应用代码**

1. class Controller {
2.   value: string = ''
3.   constructor(value: string) {
4.     this.value = value
5.   }
6. }

7. type ControllerConstructor = new (value: string) => Controller;

8. class testMenu {
9.   controller: ControllerConstructor = Controller
10.   createController() {
11.     if (this.controller) {
12.       return new this.controller('abc');
13.     }
14.     return null;
15.   }
16. }

17. let t = new testMenu()
18. console.info(t.createController()!.value)

**建议改法**

1. class Controller {
2.   value: string = ''
3.   constructor(value: string) {
4.     this.value = value;
5.   }
6. }

7. type ControllerConstructor = () => Controller;

8. class testMenu {
9.   controller: ControllerConstructor = () => { return new Controller('abc') }
10.   createController() {
11.     if (this.controller) {
12.       return this.controller();
13.     }
14.     return null;
15.   }
16. }

17. let t: testMenu = new testMenu();
18. console.info(t.createController()!.value);

## arkts-no-globalthis

ArkTS不支持globalThis。一方面无法为globalThis添加静态类型，只能通过查找方式访问其属性，导致额外性能开销。另一方面，无法为globalThis的属性标记类型，无法保证操作的安全性和高性能。

1. 建议按照业务逻辑根据import/export语法实现数据在不同模块的传递。
    
2. 必要情况下，可以通过构造的**单例对象**来实现全局对象的功能。(**说明：** 不能在har中定义单例对象，har在打包时会在不同的hap中打包两份，无法实现单例。)
    

**构造单例对象**

1. // 构造单例对象
2. export class GlobalContext {
3.   private constructor() {}
4.   private static instance: GlobalContext;
5.   private _objects = new Map<string, Object>();

6.   public static getContext(): GlobalContext {
7.     if (!GlobalContext.instance) {
8.       GlobalContext.instance = new GlobalContext();
9.     }
10.     return GlobalContext.instance;
11.   }

12.   getObject(value: string): Object | undefined {
13.     return this._objects.get(value);
14.   }

15.   setObject(key: string, objectClass: Object): void {
16.     this._objects.set(key, objectClass);
17.   }
18. }

**应用代码**

1. // file1.ts

2. export class Test {
3.   value: string = '';
4.   foo(): void {
5.     globalThis.value = this.value;
6.   }
7. }

8. // file2.ts

9. globalThis.value;

**建议改法**

1. // file1.ts

2. import { GlobalContext } from '../GlobalContext'

3. export class Test {
4.   value: string = '';
5.   foo(): void {
6.     GlobalContext.getContext().setObject('value', this.value);
7.   }
8. }

9. // file2.ts

10. import { GlobalContext } from '../GlobalContext'

11. GlobalContext.getContext().getObject('value');

## arkts-no-func-apply-bind-call

### 使用标准库中接口

**应用代码**

1. let arr: number[] = [1, 2, 3, 4];
2. let str = String.fromCharCode.apply(null, Array.from(arr));

**建议改法**

1. let arr: number[] = [1, 2, 3, 4];
2. let str = String.fromCharCode(...Array.from(arr));

### bind定义方法

**应用代码**

1. class A {
2.   value: string = ''
3.   foo: Function = () => {}
4. }

5. class Test {
6.   value: string = '1234'
7.   obj: A = {
8.     value: this.value,
9.     foo: this.foo.bind(this)
10.   }

11.   foo() {
12.     console.info(this.value);
13.   }
14. }

**建议改法1**

1. class A {
2.   value: string = ''
3.   foo: Function = () => {}
4. }

5. class Test {
6.   value: string = '1234'
7.   obj: A = {
8.     value: this.value,
9.     foo: (): void => this.foo()
10.   }

11.   foo() {
12.     console.info(this.value);
13.   }
14. }

**建议改法2**

1. class A {
2.   value: string = ''
3.   foo: Function = () => {}
4. }

5. class Test {
6.   value: string = '1234'
7.   foo: () => void = () => {
8.     console.info(this.value);
9.   }
10.   obj: A = {
11.     value: this.value,
12.     foo: this.foo
13.   }
14. }

### 使用apply

**应用代码**

1. class A {
2.   value: string;
3.   constructor (value: string) {
4.     this.value = value;
5.   }

6.   foo() {
7.     console.info(this.value);
8.   }
9. }

10. let a1 = new A('1');
11. let a2 = new A('2');

12. a1.foo();
13. a1.foo.apply(a2);

**建议改法**

1. class A {
2.   value: string;
3.   constructor (value: string) {
4.     this.value = value;
5.   }

6.   foo() {
7.     this.fooApply(this);
8.   }

9.   fooApply(a: A) {
10.     console.info(a.value);
11.   }
12. }

13. let a1 = new A('1');
14. let a2 = new A('2');

15. a1.foo();
16. a1.fooApply(a2);

## arkts-limited-stdlib

### Object.fromEntries()

**应用代码**

1. let entries = new Map([
2.   ['foo', 123],
3.   ['bar', 456]
4. ]);

5. let obj = Object.fromEntries(entries);

**建议改法**

1. let entries = new Map([
2.   ['foo', 123],
3.   ['bar', 456]
4. ]);

5. let obj: Record<string, Object> = {};
6. entries.forEach((key, value) => {
7.   if (key != undefined && key != null) {
8.     obj[key] = value;
9.   }
10. })

## 严格模式检查(StrictModeError)

### strictPropertyInitialization

**应用代码**

1. interface I {
2.   name:string
3. }

4. class A {}

5. class Test {
6.   a: number;
7.   b: string;
8.   c: boolean;
9.   d: I;
10.   e: A;
11. }

**建议改法**

1. interface I {
2.   name:string
3. }

4. class A {}

5. class Test {
6.   a: number;
7.   b: string;
8.   c: boolean;
9.   d: I = { name:'abc' };
10.   e: A | null = null;
11.   constructor(a:number, b:string, c:boolean) {
12.     this.a = a;
13.     this.b = b;
14.     this.c = c;
15.   }
16. }

### Type *** | null is not assignable to type ***

**应用代码**

1. class A {
2.   bar() {}
3. }
4. function foo(n: number) {
5.   if (n === 0) {
6.     return null;
7.   }
8.   return new A();
9. }
10. function getNumber() {
11.   return 5;
12. }
13. let a:A = foo(getNumber());
14. a.bar();

**建议改法**

1. class A {
2.   bar() {}
3. }
4. function foo(n: number) {
5.   if (n === 0) {
6.     return null;
7.   }
8.   return new A();
9. }
10. function getNumber() {
11.   return 5;
12. }

13. let a: A | null = foo(getNumber());
14. a?.bar();

### 严格属性初始化检查

在class中，如果一个属性没有初始化，且没有在构造函数中被赋值，ArkTS将报错。

**建议改法**

1.一般情况下，**建议按照业务逻辑**在声明时初始化属性，或者在构造函数中为属性赋值。如：

1. //code with error
2. class Test {
3.   value: number
4.   flag: boolean
5. }

6. //方式一，在声明时初始化
7. class Test {
8.   value: number = 0
9.   flag: boolean = false
10. }

11. //方式二，在构造函数中赋值
12. class Test {
13.   value: number
14.   flag: boolean
15.   constructor(value: number, flag: boolean) {
16.     this.value = value;
17.     this.flag = flag;
18.   }
19. }

2.对于对象类型（包括函数类型）A，如果不确定如何初始化，建议按照以下方式之一进行初始化：

​ 方式(i) prop: A | null = null

​ 方式(ii) prop?: A

​ 方式三(iii) prop： A | undefined = undefined

- 从性能角度看，null类型仅用于编译期的类型检查，不会影响虚拟机性能。而undefined | A被视为联合类型，运行时可能产生额外开销。
- 从代码可读性、简洁性的角度来说，prop?:A是prop： A | undefined = undefined的语法糖，**推荐使用可选属性的写法**。

### 严格函数类型检查

**应用代码**

1. function foo(fn: (value?: string) => void, value: string): void {}

2. foo((value: string) => {}, ''); //error

**建议改法**

1. function foo(fn: (value?: string) => void, value: string): void {}

2. foo((value?: string) => {}, '');

**原因**

例如，在以下的例子中，如果编译期不开启严格函数类型的检查，那么该段代码可以编译通过，但是在运行时会产生非预期的行为。具体来看，在foo的函数体中，一个undefined被传入fn（这是可以的，因为fn可以接受undefined），但是在代码第6行foo的调用点，传入的(value: string) => { console.info(value.toUpperCase()) }的函数实现中，始终将参数value当做string类型，允许其调用toUpperCase方法。如果不开启严格函数类型的检查，那么这段代码在运行时，会出现在undefined上无法找到属性的错误。

1. function foo(fn: (value?: string) => void, value: string): void {
2.   let v: string | undefined = undefined;
3.   fn(v);
4. }

5. foo((value: string) => { console.info(value.toUpperCase()) }, ''); // Cannot read properties of undefined (reading 'toUpperCase')

为了避免运行时的非预期行为，开启严格类型检查时，这段代码将无法编译通过，需要提醒开发者修改代码，确保程序安全。

### 严格空值检查

**应用代码**

1. class Test {
2.   private value?: string;

3.   public printValue () {
4.     console.info(this.value.toLowerCase());
5.   }
6. }

7. let t = new Test();
8. t.printValue();

**应用代码运行时错误原因**

编译期不开启严格空值检查，应用代码可以通过编译，但是在运行时会报错。

因为t的属性value为undefined，在调用printValue方法时，由于在该方法内未对this.value的值进行空值检查，直接按照string类型访问其属性，导致了运行时的错误。

**建议改法**

在编写代码时，建议减少可空类型的使用。如果对变量、属性标记了可空类型，那么在使用它们之前，需要进行空值的判断，根据是否为空值处理不同的逻辑。

1. class Test {
2.   private value?: string;

3.   public printValue () {
4.     if (this.value) {
5.       console.info(this.value.toLowerCase());
6.     }
7.   }
8. }

9. let t = new Test();
10. t.printValue();

### 函数返回类型不匹配

**应用代码**

1. class Test {
2.   handleClick: (action: string, externInfo?: string) => void | null = null;
3. }

**建议改法**

在这种写法下，函数返回类型被解析为 void | undefined，需要添加括号用来区分union类型。

1. class Test {
2.   handleClick: ((action: string, externInfo?: string) => void) | null = null;
3. }

### Type '*** | null' is not assignable to type '***'

**应用代码**

1. class A {
2.   value: number
3.   constructor(value: number) {
4.     this.value = value;
5.   }
6. }

7. function foo(v: number): A | null {
8.   if (v > 0) {
9.     return new A(v);
10.   }
11.   return null;
12. }

13. let a: A = foo();

**建议改法1**

修改变量a的类型：let a: A | null = foo()。

1. class A {
2.   value: number
3.   constructor(value: number) {
4.     this.value = value;
5.   }
6. }

7. function foo(v: number): A | null {
8.   if (v > 0) {
9.     return new A(v);
10.   }
11.   return null;
12. }

13. let a: A | null = foo(123);

14. if (a != null) {
15.   // 非空分支
16. } else {
17.   // 处理null
18. }

**建议改法2**

如果确定此处调用foo一定返回非空值，可以使用非空断言!。

1. class A {
2.   value: number
3.   constructor(value: number) {
4.     this.value = value;
5.   }
6. }

7. function foo(v: number): A | null {
8.   if (v > 0) {
9.     return new A(v);
10.   }
11.   return null;
12. }

13. let a: A = foo(123)!;

### Cannot invoke an object which is possibly 'undefined'

**应用代码**

1. interface A {
2.   foo?: () => void
3. }

4. let a:A = { foo: () => {} };
5. a.foo();

**建议改法1**

1. interface A {
2.   foo: () => void
3. }
4. let a: A = { foo: () => {} };
5. a.foo();

**建议改法2**

1. interface A {
2.   foo?: () => void
3. }

4. let a: A = { foo: () => {} };
5. if (a.foo) {
6.   a.foo();
7. }

**原因**

在原先代码的定义中，foo是可选属性，可能为undefined，对undefined的调用会导致报错。建议根据业务逻辑判断是否需要将foo设为可选属性。如果确实需要，那么在访问该属性后需要进行空值检查。

### Variable '***' is used before being assigned

**应用代码**

1. class Test {
2.   value: number = 0
3. }

4. let a: Test
5. try {
6.   a = { value: 1};
7. } catch (e) {
8.   a.value;
9. }
10. a.value;

**建议改法**

1. class Test {
2.   value: number = 0
3. }

4. let a: Test | null = null;
5. try {
6.   a = { value:1 };
7. } catch (e) {
8.   if (a) {
9.     a.value;
10.   }
11. }

12. if (a) {
13.   a.value;
14. }

**原因**

对于primitive types，可以根据业务逻辑赋值，例如0，''，false。

对于对象类型，可以将其类型修改为与null的联合类型，并赋值为null。使用时需要进行非空检查。

### Function lacks ending return statement and return type does not include 'undefined'.

**应用代码**

1. function foo(a: number): number {
2.   if (a > 0) {
3.     return a;
4.   }
5. }

**建议改法1**

根据业务逻辑，在else分支中返回合适的数值。

**建议改法2**

1. function foo(a: number): number | undefined {
2.   if (a > 0) {
3.     return a;
4.   }
5.   return
6. }

## arkts-strict-typing-required

删除忽略注释，为所有变量显式声明类型。

**应用代码**

1. // @ts-ignore
2. var a: any = 123;

**建议改法**

1. let a: number = 123;

**原因**

ArkTS不支持通过注释的方式绕过严格类型检查。首先将注释（// @ts-nocheck或者// @ts-ignore）删去，再根据报错信息修改其他代码。

## Importing ArkTS files to JS and TS files is not allowed

## arkts-no-tsdeps

不允许.ts、.js文件import.ets文件源码。

**建议改法**

方式1.将.ts文件的后缀修改为ets，并按ArkTS语法规则适配代码。

方式2.将.ets文件中被.ts文件依赖的代码单独抽取到.ts文件中。

## arkts-no-special-imports

改为使用普通import { ... } from '...' 导入类型。

**应用代码**

1. import type {A, B, C, D } from '***'

**建议改法**

1. import {A, B, C, D } from '***'

## arkts-no-classes-as-obj

### 使用class构造实例

**应用代码**

1. class Controller {
2.   value: string = ''
3.   constructor(value: string) {
4.     this.value = value
5.   }
6. }

7. interface ControllerConstructor {
8.   new (value: string): Controller;
9. }

10. class TestMenu {
11.   controller: ControllerConstructor = Controller
12.   createController() {
13.     if (this.controller) {
14.       return new this.controller('abc');
15.     }
16.     return null;
17.   }
18. }

19. let t = new TestMenu();
20. console.info(t.createController()!.value);

**建议改法**

1. class Controller {
2.   value: string = ''

3.   constructor(value: string) {
4.     this.value = value;
5.   }
6. }

7. type ControllerConstructor = () => Controller;

8. class TestMenu {
9.   controller: ControllerConstructor = () => {
10.     return new Controller('abc');
11.   }

12.   createController() {
13.     if (this.controller) {
14.       return this.controller();
15.     }
16.     return null;
17.   }
18. }

19. let t: TestMenu = new TestMenu();
20. console.info(t.createController()!.value);

### 访问静态属性

**应用代码**

1. class C1 {
2.   static value: string = 'abc'
3. }

4. class C2 {
5.   static value: string = 'def'
6. }

7. function getValue(obj: any) {
8.   return obj['value'];
9. }

10. console.info(getValue(C1));
11. console.info(getValue(C2));

**建议改法**

1. class C1 {
2.   static value: string = 'abc'
3. }

4. class C2 {
5.   static value: string = 'def'
6. }

7. function getC1Value(): string {
8.   return C1.value;
9. }

10. function getC2Value(): string {
11.   return C2.value;
12. }

13. console.info(getC1Value());
14. console.info(getC2Value());

## arkts-no-side-effects-imports

改用动态import。

**应用代码**

1. import 'module'

**建议改法**

1. import('module')

## arkts-no-func-props

使用class来组织多个相关函数。

**应用代码**

1. function foo(value: number): void {
2.   console.info(value.toString());
3. }

4. foo.add = (left: number, right: number) => {
5.   return left + right;
6. }

7. foo.sub = (left: number, right: number) => {
8.   return left - right;
9. }

**建议改法**

1. class Foo {
2.   static foo(value: number): void {
3.     console.info(value.toString());
4.   }

5.   static add(left: number, right: number): number {
6.     return left + right;
7.   }

8.   static sub(left: number, right: number): number {
9.     return left - right;
10.   }
11. }

## arkts-limited-esobj

使用具体类型（如number, string）或接口代替不明确的ESObject。

**应用代码**

1. // testa.ts
2. export function foo(): any {
3.   return null;
4. }

5. // main.ets
6. import {foo} from './testa'
7. let e0: ESObject = foo();

8. function f() {
9.   let e1 = foo();
10.   let e2: ESObject = 1;
11.   let e3: ESObject = {};
12.   let e4: ESObject = '';
13. }

**建议改法**

1. // testa.ts
2. export function foo(): any {
3.   return null;
4. }

5. // main.ets
6. import {foo} from './testa'
7. interface I {}

8. function f() {
9.   let e0: ESObject = foo();
10.   let e1: ESObject = foo();
11.   let e2: number = 1;
12.   let e3: I = {};
13.   let e4: string = '';
14. }

## 拷贝

### 浅拷贝

**TypeScript**

1. function shallowCopy(obj: object): object {
2.   let newObj = {};
3.   Object.assign(newObj, obj);
4.   return newObj;
5. }

**ArkTS**

1. function shallowCopy(obj: object): object {
2.   let newObj: Record<string, Object> = {};
3.   for (let key of Object.keys(obj)) {
4.     newObj[key] = obj[key];
5.   }
6.   return newObj;
7. }

### 深拷贝

**TypeScript**

1. function deepCopy(obj: object): object {
2.   let newObj = Array.isArray(obj) ? [] : {};
3.   for (let key in obj) {
4.     if (typeof obj[key] === 'object') {
5.       newObj[key] = deepCopy(obj[key]);
6.     } else {
7.       newObj[key] = obj[key];
8.     }
9.   }
10.   return newObj;
11. }

**ArkTS**

1. function deepCopy(obj: object): object {
2.   let newObj: Record<string, Object> | Object[] = Array.isArray(obj) ? [] : {};
3.   for (let key of Object.keys(obj)) {
4.     if (typeof obj[key] === 'object') {
5.       newObj[key] = deepCopy(obj[key]);
6.     } else {
7.       newObj[key] = obj[key];
8.     }
9.   }
10.   return newObj;
11. }

## 状态管理使用典型场景

### Struct组件外使用状态变量

由于struct和class的不同，不建议将this作为参数传递到struct外部使用，以避免实例引用无法释放，导致内存泄露。建议传递状态变量对象到struct外部使用，通过修改对象的属性来触发UI刷新。

**不推荐用法**

1. export class MyComponentController {
2.   item: MyComponent = null;

3.   setItem(item: MyComponent) {
4.     this.item = item;
5.   }

6.   changeText(value: string) {
7.     this.item.value = value;
8.   }
9. }

10. @Component
11. export default struct MyComponent {
12.   public controller: MyComponentController = null;
13.   @State value: string = 'Hello World';

14.   build() {
15.     Column() {
16.       Text(this.value)
17.         .fontSize(50)
18.     }
19.   }

20.   aboutToAppear() {
21.     if (this.controller)
22.       this.controller.setItem(this); // 不建议把this作为参数传递到struct外部使用
23.   }
24. }

25. @Entry
26. @Component
27. struct ObjThisOldPage {
28.   controller = new MyComponentController();

29.   build() {
30.     Column() {
31.       MyComponent({ controller: this.controller })
32.       Button('change value').onClick(() => {
33.         this.controller.changeText('Text');
34.       })
35.     }
36.   }
37. }

**推荐用法**

1. class CC {
2.   value: string = '1';

3.   constructor(value: string) {
4.     this.value = value;
5.   }
6. }

7. export class MyComponentController {
8.   item: CC = new CC('1');

9.   setItem(item: CC) {
10.     this.item = item;
11.   }

12.   changeText(value: string) {
13.     this.item.value = value;
14.   }
15. }

16. @Component
17. export default struct MyComponent {
18.   public controller: MyComponentController | null = null;
19.   @State value: CC = new CC('Hello World');

20.   build() {
21.     Column() {
22.       Text(`${this.value.value}`)
23.         .fontSize(50)
24.     }
25.   }

26.   aboutToAppear() {
27.     if (this.controller)
28.       this.controller.setItem(this.value);
29.   }
30. }

31. @Entry
32. @Component
33. struct StyleExample {
34.   controller: MyComponentController = new MyComponentController();

35.   build() {
36.     Column() {
37.       MyComponent({ controller: this.controller })
38.       Button('change value').onClick(() => {
39.         this.controller.changeText('Text');
40.       })
41.     }
42.   }
43. }

### Struct支持联合类型的方案

下面这段代码有arkts-no-any-unknown的报错，由于struct不支持泛型，建议使用联合类型，实现自定义组件类似泛型的功能。

**不推荐用法**

1. class Data {
2.   aa: number = 11;
3. }

4. @Entry
5. @Component
6. struct DatauionOldPage {
7.   @State array: Data[] = [new Data(), new Data(), new Data()];

8.   @Builder
9.   componentCloser(data: Data) {
10.     Text(data.aa + '').fontSize(50)
11.   }

12.   build() {
13.     Row() {
14.       Column() {
15.         ForEachCom({ arrayList: this.array, closer: this.componentCloser })
16.       }
17.       .width('100%')
18.     }
19.     .height('100%')
20.   }
21. }

22. @Component
23. export struct ForEachCom {
24.   arrayList: any[]; // struct不支持泛型，有arkts-no-any-unknown报错
25.   @BuilderParam closer: (data: any) => void = this.componentCloser; // struct不支持泛型，有arkts-no-any-unknown报错

26.   @Builder
27.   componentCloser() {
28.   }

29.   build() {
30.     Column() {
31.       ForEach(this.arrayList, (item: any) => { // struct不支持泛型，有arkts-no-any-unknown报错
32.         Row() {
33.           this.closer(item)
34.         }.width('100%').height(200).backgroundColor('#eee')
35.       })
36.     }
37.   }
38. }

**推荐用法**

1. class Data {
2.   aa: number = 11;
3. }

4. class Model {
5.   aa: string = '11';
6. }

7. type UnionData = Data | Model;

8. @Entry
9. @Component
10. struct DatauionPage {
11.   array: UnionData[] = [new Data(), new Data(), new Data()];

12.   @Builder
13.   componentCloser(data: UnionData) {
14.     if (data instanceof Data) {
15.       Text(data.aa + '').fontSize(50)
16.     }
17.   }

18.   build() {
19.     Row() {
20.       Column() {
21.         ForEachCom({ arrayList: this.array, closer: this.componentCloser })
22.       }
23.       .width('100%')
24.     }
25.     .height('100%')
26.   }
27. }

28. @Component
29. export struct ForEachCom {
30.   arrayList: UnionData[] = [new Data(), new Data(), new Data()];
31.   @BuilderParam closer: (data: UnionData) => void = this.componentCloser;

32.   @Builder
33.   componentCloser() {
34.   }

35.   build() {
36.     Column() {
37.       ForEach(this.arrayList, (item: UnionData) => {
38.         Row() {
39.           this.closer(item)
40.         }.width('100%').height(200).backgroundColor('#eee')
41.       })
42.     }
43.   }
44. }
# ArkTS高性能编程实践

更新时间: 2025-12-16 16:34

## 概述

本文提供应用性能敏感场景下的高性能编程建议，帮助开发者编写高性能应用。高性能编程实践是在开发过程中总结的一些高性能写法和建议。在实现业务功能时，应同步思考并理解高性能写法的原理，并将其应用于代码逻辑中。关于ArkTS编程规范，请参考[ArkTS编程规范](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-coding-style-guide)。

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
# 从Java到ArkTS的迁移指导

更新时间: 2025-12-16 16:34

对于熟悉Java的开发者而言，ArkTS作为新的开发语言，带来了全新的开发体验与机遇。ArkTS在语法和编程范式上不仅继承了现代语言的特性，还针对生态进行了深度优化。理解Java与ArkTS的差异和共性，能够帮助开发者快速上手应用开发，避开常见的编程误区。

本文档基于Java语言对ArkTS语言进行对比和介绍。如需更详细的了解，可参考[ArkTS语言介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/introduction-to-arkts)。

## 探索Java与ArkTS的差异

本文档将帮助Java开发者梳理在转向ArkTS开发过程中会遇到的误解和陷阱。ArkTS的语法、类型系统以及应用开发模式与Java存在差异，在学习过程中需特别注意这些关键区别。建议先掌握ArkTS的基础语法和运行时行为，再重点对比其与Java的不同之处。

## 基础语法

### 变量声明

**ArkTS示例：**

1. // 类型注解（类似Java）。
2. let age: number = 20;
3. const program: string = 'ArkTS';

4. // 类型推断（类似Java的局部变量类型推断）。
5. let version = 5.0;

### 基础数据类型

|Java类型|ArkTS类型|示例代码|核心差异说明|
|:--|:--|:--|:--|
|boolean|boolean|let isDone: boolean = false;|定义方式相似，均用于逻辑判断，无运行时装箱拆箱操作。|
|byte|number|let b: number = 100;|Java中的byte为8位整数。<br><br>ArkTS统一用number表示小整数类型。|
|short|number|let s: number = 300;|Java中的short为16位整数。<br><br>ArkTS统一用number表示小整数类型。|
|int|number|let count: number = 10;|Java的int为32位整数。<br><br>ArkTS的number是双精度浮点型，可存储整数和浮点数。|
|long|number|let largeNum: number = 9007199254740991;|Java需加L后缀（如9007199254740991L）。<br><br>ArkTS用同一类型表示。|
|float|number|let pi: number = 3.14;|Java需加f后缀（如3.14f）。<br><br>ArkTS直接使用number，无需特殊标识。|
|double|number|let e: number = 2.71828;|Java区分float和double。<br><br>ArkTS统一用number表示所有数值类型。|
|char|string|let c: string = 'a';|ArkTS无char类型，单字符场景使用string。|
|String|string|let message: string = 'Hello';|定义方式类似，但ArkTS字符串支持模板字面量（如${name}）和更灵活的操作。|

### 复杂数据类型

|Java类型体系|ArkTS类型体系|ArkTS示例代码|核心差异说明|
|:--|:--|:--|:--|
|**数组**：int[] arr = new int[5];|**Array**：let arr: Array<number> = [1, 2, 3];|// 固定长度初始化（类似Java）<br><br>let fixedArr: number[] = new Array<number>(5);<br><br>// 动态长度语法糖<br><br>let dynamicArr = [4, 5, 6];|Java数组长度固定。<br><br>ArkTS的Array是动态数组，支持push/pop等操作；可直接用[]简化初始化。数组不会越界，当数组下标超过数组长度时会得到undefined。|
|**集合 - List**：List<String> list = new ArrayList<>();|**Array**：let strList: Array<string> = ['a', 'b'];|strList.push('c'); // 向数组末尾添加元素<br><br>let firstItem = strList[0]; // 索引访问|Java集合通过接口（如List）与实现类（如ArrayList）分离。<br><br>ArkTS数组兼具基础类型与集合特性，语法更简洁。|
|**集合 - Map**：Map<String, Integer> map = new HashMap<>();|**Map**：let map: Map<string, number> = new Map();|map.set('key', 1); // 添加键值对<br><br>let value = map.get('key'); // 获取值<br><br>map.has('key'); // 检查键是否存在|Java的Map需显式声明泛型类型。<br><br>ArkTS的Map操作更直接，支持链式调用（如map.set('a', 1).set('b', 2)）。|
|**接口**：interface Shape { double area(); }|**interface**：interface Shapes { area(): number; }|class Rectangles implements Shapes {<br><br>public width: number = 0;<br><br>public height: number = 0;<br><br>area(): number { return this.width * this.height; }<br><br>}|语法结构相似，但ArkTS接口实现无需显式修饰符（如Java的public），且支持可选属性（如name?: string）。|
|**类**：class Circle implements Shape { /* 类定义 */ }|**class**：class Circles implements Shape { /* 类定义 */ }|class Circles {<br><br>radius: number;<br><br>constructor(radius: number = 10) { // 支持参数默认值<br><br>this.radius = radius;<br><br>}<br><br>}|ArkTS类支持属性默认值、可选参数，构造函数参数可直接声明为类属性（如constructor(public name: string)），语法更简洁。|
|**枚举**：enum Color { RED, GREEN, BLUE; }|**enum**：enum Colors { Red, Green, Blue }|enum Colors { Red = 1, Green, Blue };<br><br>let color = Colors.Green; // 值为2（自动递增）|基本概念一致，但ArkTS枚举不支持Java中的自定义构造函数和方法，仅支持简单的数值或字符串枚举。|

### 函数

**ArkTS示例：**

1. // 常规函数定义。
2. function add(x: number, y: number): number {
3.     return x + y;
4. }

5. // 简洁的箭头函数形式。
6. const multiply = (a: number, b: number): number => a * b;

### 函数重载

Java在编译时多态，允许同一类中存在多个同名方法，通过参数列表（数量、类型、顺序）来进行区分。

- 通过多个具体方法实现重载，每个重载方法有独立的方法体。
    
- 参数列表（类型、数量、顺序）必须不同，返回值类型可以相同或不同。
    
- 编译时根据参数类型选择具体方法。
    

**Java示例：** Java函数重载

1. class Example {
2.     // 方法1：接受int参数。
3.     void print(int value) {
4.         System.out.println("Integer: " + value);
5.     }

6.     // 方法2：接受String参数。
7.     void print(String value) {
8.         System.out.println("String: " + value);
9.     }
10. }

ArkTS提供类型声明层面的多态，仅用于类型检查和文档提示，实际只有一个实现函数。

- 通过类型声明重载签名，但仅有一个实现函数。
    
- 实现函数需兼容所有重载签名，通常需要在函数体内手动判断参数类型。
    
- 类型检查器根据调用时的参数匹配声明，但运行时只有单一函数。
    

**ArkTS示例：** ArkTS函数重载

1. function foo(x: number): void;            /* 第一个函数定义 */
2. function foo(x: string): void;            /* 第二个函数定义 */
3. function foo(x: number | string): void {  /* 函数实现 */
4. }

5. foo(123);     //  OK，使用第一个定义。
6. foo('aa'); // OK，使用第二个定义。

### 基础类库

ArkTS基础类库和容器类库增强了语言的基础功能，包括高精度浮点运算、二进制Buffer、XML生成解析转换和多种容器库等能力，协助开发者简化开发工作，提升开发效率。详细介绍可见[ArkTS基础类库概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-utils-overview)。

## 语言结构

Java是一种典型的面向对象的编程语言，即一切围绕类和对象展开。

ArkTS采用更为灵活的语言结构，融合了面向对象编程和函数式编程等多种范式。

### 模块与包管理

在Java中，开发者使用包（package）来组织代码，通过import语句引入其他包中的类。ArkTS也有自己的模块和包管理机制，同样通过import语句引入其他模块中的功能。

**ArkTS示例：**

1. // 引入ArkTS标准库中的ArkTS容器集。

2. import { collections } from '@kit.ArkTS';

由于ArkTS的模块系统更注重模块化开发和代码复用，能够更便捷地管理不同功能模块之间的依赖关系，所以在使用方式上，与Java的包管理会有所区别。

### 类与命名空间特性

ArkTS的类系统在语法层面与Java相似，但在高阶特性上展现出更现代的设计理念。

|特性|Java实现方式|ArkTS实现方式|说明|
|:--|:--|:--|:--|
|命名空间组织|静态嵌套类/内部类|namespace关键字或模块文件结构。|支持显式命名空间与模块化组织的混合模式。|
|类继承机制|基于类的继承体系|基于原型链的继承机制。|语法相似但底层机制不同。|
|类成员可见性|public/private/protected|同Java，但支持[模块级](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-principle)可见性控制。|增加了模块导出控制的维度。|

**命名空间管理**

ArkTS支持显式命名空间（namespace）和模块化组织。

**ArkTS示例：**

1. namespace Models {
2.     export class User {
3.         // 实现细节。
4.     }

5.     export interface Repository {
6.         // 接口定义。
7.     }
8. }

相比Java的package+static class组合，ArkTS的命名空间能更直观地实现代码分层。

### 异步编程模型

**单线程vs多线程**

Java依赖多线程和Future/CompletableFuture实现并发。

ArkTS基于事件循环，使用Promise/async/await处理异步，避免阻塞主线程。

**错误处理**

Java的同步代码通过try/catch捕获异常，异步异常需特殊处理（如Future.get()）。

ArkTS中未捕获的Promise错误可能导致静默失败，需显式使用try/catch或.catch。

### this的绑定

Java的this始终指向当前类的实例对象，由代码结构在编译时确定。在方法中，this指向调用该方法的对象实例，无法通过调用方式改变this的指向。

**Java示例：**

1. class MyClass {
2.   void method() {
3.     System.out.println(this); // 始终指向MyClass的实例。
4.   }
5. }

ArkTS的this指向取决于函数调用时的上下文。

**ArkTS示例：**

1. class A {
2.   bar: string = 'I am A';

3.   foo() {
4.     console.info(this.bar);
5.   }
6. }

7. class B {
8.   bar: string = 'I am B';

9.   callFunction(fn: () => void) {
10.     fn();
11.   }
12. }

13. function callFunction(fn: () => void) {
14.   fn();
15. }

16. let a: A = new A();
17. let b: B = new B();

18. callFunction(a.foo); // 程序crash。this的上下文发生了变化。
19. b.callFunction(a.foo); // 程序crash。this的上下文发生了变化。
20. b.callFunction(a.foo.bind(b)) // 输出'I am B'。

## 类型系统

ArkTS与Java的类型系统也存在差异。

### 类型推断与可选类型

相较于Java需要显式类型声明和严格的null检查，ArkTS的类型系统提供了更灵活的表达方式。

ArkTS具有强大的类型推断能力，编译器能够根据上下文自动推断出变量的类型，所以很多时候不需要显式声明变量的类型。

**ArkTS示例：**

1. let num = 10; // 编译器自动推断num为number类型。

同时，ArkTS支持可选类型，通过在类型后面添加问号（?）来表示该变量可以为null或undefined。

**ArkTS示例：**

1. interface Person {
2.   name: string;
3.   age?: number;  // age 是可选属性。
4. }

5. const person: Person = {
6.   name: "Alice",
7. };

### 联合类型

联合类型这种类型组合能力为复杂场景提供了更强的表达力，是ArkTS类型系统的重要创新点。

ArkTS支持联合类型（|）。联合类型表示一个值可以是多种类型中的一种。

**ArkTS示例：**

1. // 联合类型示例。

2. let value: string | number;
3. value = 'hello';
4. value = 123;
# XML概述

更新时间: 2025-12-16 16:38

XML（可扩展标记语言）是一种用于描述数据的标记语言，提供通用的数据传输和存储方式。XML不预定义标记，因此更加灵活，适用于广泛的应用领域。

XML文档由元素（element）、属性（attribute）和内容（content）组成。

- 元素指的是标记对，包含文本、属性或其他元素。
    
- 属性提供了有关元素的其他信息。
    
- 内容则是元素包含的数据或子元素。
    

XML使用XML Schema或DTD（文档类型定义）定义文档结构，开发人员可以利用这些机制创建自定义规则，以验证XML文档的格式是否符合预期规范。

XML支持命名空间、实体引用、注释和处理指令，灵活适应各种数据需求。

语言基础类库提供了XML相关的基础能力，包括：[XML的生成](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/xml-generation)、[XML的解析](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/xml-parsing)和[XML的转换](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/xml-conversion)。

以下是一个简单的XML样例及对应说明，更多XML的接口和具体使用，请见[@ohos.xml](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-xml)。

1. <!-- 声明 -->
2. <?xml version="1.0" encoding="utf-8"?>
3. <!-- 处理指令 -->
4. <?xml-stylesheet type="text/css" href="style.css"?>
5. <!-- 元素、属性及属性值 -->
6. <note importance="high">
7.     <title>Happy</title>
8.     <!-- 实体引用 -->
9.     <todo>&amp;</todo>
10.     <!-- 命名空间的声明及统一资源标识符 -->
11.     <h:table xmlns:h="http://www.w3.org/TR/html4/">
12.         <h:tr>
13.             <h:td>Apples</h:td>
14.             <h:td>Bananas</h:td>
15.         </h:tr>
16.     </h:table>
17. </note>

# XML生成

更新时间: 2025-12-16 16:39

XML可以作为数据交换格式，被各种系统和应用程序支持。例如Web服务，可以将结构化数据以XML格式进行传递。

XML还可以作为消息传递格式，用于分布式系统中不同节点的通信。

## 注意事项

- XML标签必须成对出现，生成开始标签就要生成结束标签。
    
- XML标签对大小写敏感，开始标签与结束标签大小写要一致。
    

## 开发步骤

XML模块提供XmlSerializer及XmlDynamicSerializer类来生成XML数据，使用XmlSerializer需传入固定长度的ArrayBuffer或DataView对象作为输出缓冲区，用于存储序列化后的XML数据。

XmlDynamicSerializer类动态扩容，程序根据实际生成的数据大小自动创建ArrayBuffer。

调用不同的方法写入不同的内容，如startElement(name: string)写入元素开始标记，setText(text: string)写入标签值。

XML模块的API接口可以参考[@ohos.xml](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-xml)的详细描述，按需求调用相应的函数可以生成一份完整的XML数据。

使用XmlSerializer生成XML示例如下：

1. 引入模块。
    
    1. import { xml, util } from '@kit.ArkTS';
    
2. 创建缓冲区，构造XmlSerializer对象。可以基于ArrayBuffer构造XmlSerializer对象，也可以基于DataView构造XmlSerializer对象。
    
    方式1：基于ArrayBuffer构造XmlSerializer对象
    
    1. let arrayBuffer: ArrayBuffer = new ArrayBuffer(2048); // 创建一个2048字节的缓冲区
    2. let serializer: xml.XmlSerializer = new xml.XmlSerializer(arrayBuffer); // 基于ArrayBuffer构造XmlSerializer对象
    
    方式2：基于DataView构造XmlSerializer对象
    
    1. let arrayBuffer: ArrayBuffer = new ArrayBuffer(2048); // 创建一个2048字节的缓冲区
    2. let dataView: DataView = new DataView(arrayBuffer); // 创建一个DataView
    3. let serializer: xml.XmlSerializer = new xml.XmlSerializer(dataView); // 基于DataView构造XmlSerializer对象
    
3. 调用XML元素生成函数。
    
    1. serializer.setDeclaration(); // 写入XML的声明
    2. serializer.startElement('bookstore'); // 写入元素开始标记
    3. serializer.startElement('book'); // 嵌套元素开始标记
    4. serializer.setAttributes('category', 'COOKING'); // 写入属性及其属性值
    5. serializer.startElement('title');
    6. serializer.setAttributes('lang', 'en');
    7. serializer.setText('Everyday'); // 写入标签值
    8. serializer.endElement(); // 写入结束标记
    9. serializer.startElement('author');
    10. serializer.setText('Giana');
    11. serializer.endElement();
    12. serializer.startElement('year');
    13. serializer.setText('2005');
    14. serializer.endElement();
    15. serializer.endElement();
    16. serializer.endElement();
    
4. 使用Uint8Array操作ArrayBuffer，并调用TextDecoder对Uint8Array解码后输出。
    
    1. let uint8Array: Uint8Array = new Uint8Array(arrayBuffer); // 使用Uint8Array读取arrayBuffer的数据
    2. let textDecoder: util.TextDecoder = util.TextDecoder.create(); // 调用util模块的TextDecoder类
    3. let result: string = textDecoder.decodeToString(uint8Array); // 对uint8Array解码
    4. console.info(result);
    
    输出结果如下：
    
    1. <?xml version="1.0" encoding="utf-8"?><bookstore>
    2.   <book category="COOKING">
    3.     <title lang="en">Everyday</title>
    4.     <author>Giana</author>
    5.     <year>2005</year>
    6.   </book>
    7. </bookstore>
    

使用XmlDynamicSerializer生成XML示例如下：

1. 引入模块。
    
    1. import { xml, util } from '@kit.ArkTS';
    
2. 调用XML元素生成函数。
    
    1. let DySerializer = new xml.XmlDynamicSerializer('utf-8');
    2. DySerializer.setDeclaration(); // 写入XML的声明
    3. DySerializer.startElement('bookstore'); // 写入元素开始标记
    4. DySerializer.startElement('book'); // 嵌套元素开始标记
    5. DySerializer.setAttributes('category', 'COOKING'); // 写入属性及其属性值
    6. DySerializer.startElement('title');
    7. DySerializer.setAttributes('lang', 'en');
    8. DySerializer.setText('Everyday'); // 写入标签值
    9. DySerializer.endElement(); // 写入结束标记
    10. DySerializer.startElement('author');
    11. DySerializer.setText('Giana');
    12. DySerializer.endElement();
    13. DySerializer.startElement('year');
    14. DySerializer.setText('2005');
    15. DySerializer.endElement();
    16. DySerializer.endElement();
    17. DySerializer.endElement();
    18. let arrayBuffer = DySerializer.getOutput();
    
3. 使用Uint8Array操作ArrayBuffer，并调用TextDecoder对Uint8Array解码后输出。
    
    1. let uint8Array: Uint8Array = new Uint8Array(arrayBuffer);
    2. let result: string = util.TextDecoder.create().decodeToString(uint8Array);
    3. console.info(result);
    
    输出结果如下：
    
    4. <?xml version="1.0" encoding="utf-8"?>
    5. <bookstore>
    6.   <book category="COOKING">
    7.     <title lang="en">Everyday</title>
    8.     <author>Giana</author>
    9.     <year>2005</year>
    10.   </book>
    11. </bookstore>
    # XML解析

更新时间: 2025-12-16 16:39

对于以XML作为载体传递的数据，实际使用中需要对相关的元素进行解析，一般包括[解析XML标签和标签值](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/xml-parsing#%E8%A7%A3%E6%9E%90xml%E6%A0%87%E7%AD%BE%E5%92%8C%E6%A0%87%E7%AD%BE%E5%80%BC)、[解析XML属性和属性值](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/xml-parsing#%E8%A7%A3%E6%9E%90xml%E5%B1%9E%E6%80%A7%E5%92%8C%E5%B1%9E%E6%80%A7%E5%80%BC)、[解析XML事件类型和元素信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/xml-parsing#%E8%A7%A3%E6%9E%90xml%E4%BA%8B%E4%BB%B6%E7%B1%BB%E5%9E%8B%E5%92%8C%E5%85%83%E7%B4%A0%E4%BF%A1%E6%81%AF)三类操作。如在Web服务中，XML是SOAP（Simple Object Access Protocol）协议的基础，SOAP消息通常以XML格式封装，包含请求和响应参数，通过解析这些XML消息，Web服务可以处理来自客户端的请求并生成相应的响应。

XML模块提供XmlPullParser类用于解析XML文本，输入为包含XML数据的ArrayBuffer或DataView，输出为结构化的解析结果。

**表1** XML解析选项，其详细介绍请参见[ParseOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-xml#parseoptions)。

|名称|类型|必填|说明|
|:--|:--|:--|:--|
|supportDoctype|boolean|否|是否解析文档类型，false表示不解析文档类型，true表示解析文档类型，默认false。|
|ignoreNameSpace|boolean|否|是否忽略命名空间，忽略命名空间后，将不会对其进行解析。true表示忽略命名空间，false表示不忽略命名空间，默认false。|
|tagValueCallbackFunction|(name: string, value: string) => boolean|否|获取tagValue回调函数，打印XML标签及标签值。默认为undefined，表示不解析XML标签和标签值。|
|attributeValueCallbackFunction|(name: string, value: string) => boolean|否|获取attributeValue回调函数，打印XML属性及属性值。默认为undefined，表示不解析XML属性和属性值。|
|tokenValueCallbackFunction|(eventType: EventType, value: ParseInfo) => boolean|否|获取tokenValue回调函数，打印XML事件类型及parseInfo对应属性。默认为undefined，表示不解析XML事件类型。|

## 注意事项

- 确保传入的XML数据符合标准格式。
    
- 目前不支持解析指定节点的值。
    

## 解析XML标签和标签值

1. 引入模块。
    
    1. import { xml, util } from '@kit.ArkTS'; // 需要使用util模块函数对文本编码
    
2. 对XML文本编码后调用XmlPullParser。
    
    可以基于ArrayBuffer创建XmlPullParser对象，也可以基于DataView创建XmlPullParser对象（两种创建方式返回结果无区别）。
    
    1. let strXml: string =
    2. '<?xml version="1.0" encoding="utf-8"?>' +
    3.   '<note importance="high" logged="true">' +
    4.   '<title>Play</title>' +
    5.   '<lens>Work</lens>' +
    6.   '</note>';
    7. let textEncoder: util.TextEncoder = new util.TextEncoder();
    8. let arrBuffer: Uint8Array = textEncoder.encodeInto(strXml); // 对数据进行编码，防止中文字符乱码
    9. // 方式1：基于ArrayBuffer构造XmlPullParser对象
    10. let xmlParser: xml.XmlPullParser = new xml.XmlPullParser(arrBuffer.buffer as object as ArrayBuffer, 'UTF-8');
    
    11. // 方式2：基于DataView构造XmlPullParser对象
    12. // let dataView: DataView = new DataView(arrBuffer.buffer as object as ArrayBuffer);
    13. // let xmlParser: xml.XmlPullParser = new xml.XmlPullParser(dataView, 'UTF-8');
    
3. 自定义回调函数，本例直接打印出标签及标签值。
    
    1. function func(name: string, value: string): boolean {
    2.   if (name == 'note') {
    3.     console.info(name);
    4.   }
    5.   if (value == 'Play' || value == 'Work') {
    6.     console.info('    ' + value);
    7.   }
    8.   if (name == 'title' || name == 'lens') {
    9.     console.info('  ' + name);
    10.   }
    11.   return true; //true:继续解析 false:停止解析
    12. }
    
4. 设置解析选项，调用parseXml函数。
    
    1. let options: xml.ParseOptions = {supportDoctype:true, ignoreNameSpace:true, tagValueCallbackFunction:func};
    2. xmlParser.parseXml(options);
    
    输出结果如下所示：
    
    1. note
    2.   title
    3.     Play
    4.   title
    5.   lens
    6.     Work
    7.   lens
    8. note
    

## 解析XML属性和属性值

1. 引入模块。
    
    1. import { xml, util } from '@kit.ArkTS'; // 使用util模块对文本编码
    
2. 对XML文本编码后调用XmlPullParser。
    
    1. let strXml: string =
    2.   '<?xml version="1.0" encoding="utf-8"?>' +
    3.     '<note importance="high" logged="true">' +
    4.     '    <title>Play</title>' +
    5.     '    <title>Happy</title>' +
    6.     '    <lens>Work</lens>' +
    7.     '</note>';
    8. let textEncoder: util.TextEncoder = new util.TextEncoder();
    9. let arrBuffer: Uint8Array = textEncoder.encodeInto(strXml); // 对数据进行编码，防止中文字符乱码
    10. let xmlParser: xml.XmlPullParser = new xml.XmlPullParser(arrBuffer.buffer as object as ArrayBuffer, 'UTF-8');
    
3. 自定义回调函数，示例直接打印出属性及属性值。
    
    1. let str: string = '';
    2. function func(name: string, value: string): boolean {
    3.   str += name + ' ' + value + ' ';
    4.   return true; // true:继续解析 false:停止解析
    5. }
    
4. 设置解析选项，调用parseXml函数。
    
    1. let options: xml.ParseOptions = {supportDoctype:true, ignoreNameSpace:true, attributeValueCallbackFunction:func};
    2. xmlParser.parseXml(options);
    3. console.info(str); // 打印所有属性及其值
    
    输出结果如下所示：
    
    4. importance high logged true // note节点的属性及属性值
    

## 解析XML事件类型和元素信息

1. 引入模块。
    
    1. import { xml, util } from '@kit.ArkTS'; // 使用util模块函数对文本编码
    
2. 对XML文本编码后调用XmlPullParser。
    
    1. let strXml: string =
    2.   '<?xml version="1.0" encoding="utf-8"?>' +
    3.   '<note importance="high" logged="true">' +
    4.   '<title>Play</title>' +
    5.   '</note>';
    6. let textEncoder: util.TextEncoder = new util.TextEncoder();
    7. let arrBuffer: Uint8Array = textEncoder.encodeInto(strXml); // 对数据进行编码，防止中文字符乱码
    8. let xmlParser: xml.XmlPullParser = new xml.XmlPullParser(arrBuffer.buffer as object as ArrayBuffer, 'UTF-8');
    
3. 自定义回调函数，示例直接打印元素事件类型及元素深度。
    
    1. let str: string = '';
    2. function func(name: xml.EventType, value: xml.ParseInfo): boolean {
    3.   str = name + ' ' + value.getDepth(); // getDepth 获取元素在XML文档中的当前深度
    4.   console.info(str);
    5.   return true; // true:继续解析 false:停止解析
    6. }
    
4. 设置解析选项，调用parseXml函数。
    
    1. let options: xml.ParseOptions = {supportDoctype:true, ignoreNameSpace:true, tokenValueCallbackFunction:func};
    2. xmlParser.parseXml(options);
    
    输出结果如下所示：
    
    1.  0 0 // 0：<?xml version="1.0" encoding="utf-8"?> 对应事件类型START_DOCUMENT值为0  0：起始深度为0
    2.  2 1 // 2：<note importance="high" logged="true"> 对应事件类型START_TAG值为2  1：深度为1
    3.  2 2 // 2：<title>对应事件类型START_TAG值为2  2：深度为2
    4.  4 2 // 4：Play对应事件类型TEXT值为4  2：深度为2
    5.  3 2 // 3：</title>对应事件类型END_TAG值为3  2：深度为2
    6.  3 1 // 3：</note>对应事件类型END_TAG值为3  1：深度为1（与<note对应>）
    7.  1 0 // 1：对应事件类型END_DOCUMENT值为1  0：深度为0
    

## 场景示例

此处以调用所有解析选项为例，提供解析XML标签、属性和事件类型的开发示例。

1. import { xml, util } from '@kit.ArkTS';

2. let strXml: string =
3.   '<?xml version="1.0" encoding="UTF-8"?>' +
4.     '<book category="COOKING">' +
5.     '<title lang="en">Everyday</title>' +
6.     '<author>Giana</author>' +
7.     '</book>';
8. let textEncoder: util.TextEncoder = new util.TextEncoder();
9. let arrBuffer: Uint8Array = textEncoder.encodeInto(strXml);
10. let xmlParser: xml.XmlPullParser = new xml.XmlPullParser(arrBuffer.buffer as object as ArrayBuffer, 'UTF-8');
11. let str: string = '';

12. function tagFunc(name: string, value: string): boolean {
13.   str = name + value;
14.   console.info('tag-' + str);
15.   return true;
16. }

17. function attFunc(name: string, value: string): boolean {
18.   str = name + ' ' + value;
19.   console.info('attri-' + str);
20.   return true;
21. }

22. function tokenFunc(name: xml.EventType, value: xml.ParseInfo): boolean {
23.   str = name + ' ' + value.getDepth();
24.   console.info('token-' + str);
25.   return true;
26. }

27. let options: xml.ParseOptions = {
28.   supportDoctype: true,
29.   ignoreNameSpace: true,
30.   tagValueCallbackFunction: tagFunc,
31.   attributeValueCallbackFunction: attFunc,
32.   tokenValueCallbackFunction: tokenFunc
33. };
34. xmlParser.parseXml(options);

输出结果如下所示：

1. tag-
2. token-0 0
3. tag-book
4. token-2 1
5. attri-category COOKING
6. tag-title
7. token-2 2
8. attri-lang en
9. tag-Everyday
10. token-4 2
11. tag-title
12. token-3 2
13. tag-author
14. token-2 2
15. tag-Giana
16. token-4 2
17. tag-author
18. token-3 2
19. tag-book
20. token-3 1
21. tag-
22. token-1 0
# XML转换

更新时间: 2025-12-16 16:39

将XML文本转换为JavaScript对象，便于处理和操作数据，适用于JavaScript应用程序。

语言基础类库提供ConvertXML类，将XML文本转换为JavaScript对象，输入为待转换的XML字符串及转换选项，输出为转换后的JavaScript对象。具体转换选项可见[API参考@ohos.convertxml](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-convertxml)。

## 注意事项

XML解析及转换需要确保传入的XML数据符合XML标准格式。

## 开发步骤

以XML转换为JavaScript对象为例，说明如何获取标签值。

1. 引入所需的模块。
    
    1. import { convertxml } from '@kit.ArkTS';
    
2. 输入待转换的XML，设置转换选项。支持的转换选项及含义，请参见[ConvertOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-convertxml#convertoptions)。
    
    说明
    
    请确保传入的XML文本符合标准格式，若包含“&”字符，请使用实体引用“&amp;”替换。
    
    1. let xml: string =
    2.  '<?xml version="1.0" encoding="utf-8"?>' +
    3.  '<note importance="high" logged="true">' +
    4.  '    <title>Happy</title>' +
    5.  '    <todo>Work</todo>' +
    6.  '    <todo>Play</todo>' +
    7.  '</note>';
    8. let options: convertxml.ConvertOptions = {
    9.   // trim: false 转换后是否删除文本前后的空格，否
    10.   // declarationKey: "_declaration" 转换后文件声明使用_declaration来标识
    11.   // instructionKey: "_instruction" 转换后指令使用_instruction标识
    12.   // attributesKey: "_attributes" 转换后属性使用_attributes标识
    13.   // textKey: "_text" 转换后标签值使用_text标识
    14.   // cdataKey: "_cdata" 转换后未解析数据使用_cdata标识
    15.   // docTypeKey: "_doctype" 转换后文档类型使用_doctype标识
    16.   // commentKey: "_comment" 转换后注释使用_comment标识
    17.   // parentKey: "_parent" 转换后父类使用_parent标识
    18.   // typeKey: "_type" 转换后元素类型使用_type标识
    19.   // nameKey: "_name" 转换后标签名称使用_name标识
    20.   // elementsKey: "_elements" 转换后元素使用_elements标识
    21.   trim: false,
    22.   declarationKey: "_declaration",
    23.   instructionKey: "_instruction",
    24.   attributesKey: "_attributes",
    25.   textKey: "_text",
    26.   cdataKey: "_cdata",
    27.   doctypeKey: "_doctype",
    28.   commentKey: "_comment",
    29.   parentKey: "_parent",
    30.   typeKey: "_type",
    31.   nameKey: "_name",
    32.   elementsKey: "_elements"
    33. }
    
3. 调用fastConvertToJSObject函数并打印结果。
    
    1. let conv: convertxml.ConvertXML = new convertxml.ConvertXML();
    2. let result: object = conv.fastConvertToJSObject(xml, options);
    3. let strRes: string = JSON.stringify(result); // 将js对象转换为json字符串，用于显式输出
    4. console.info(strRes);
    
    输出结果如下所示：
    
    1. strRes:
    2. {"_declaration":{"_attributes":{"version":"1.0","encoding":"utf-8"}},"_elements":[{"_type":"element","_name":"note",
    3.  "_attributes":{"importance":"high","logged":"true"},"_elements":[{"_type":"element","_name":"title","_parent":"note",
    4.  "_elements":[{"_type":"text","_text":"Happy"}]},{"_type":"element","_name":"todo","_parent":"note","_elements":
    5.  [{"_type":"text","_text":"Work"}]},{"_type":"element","_name":"todo","_parent":"note","_elements":[{"_type":"text",
    6.  "_text":"Play"}]}]}]}
    # JSON扩展库

更新时间: 2025-12-16 16:38

## 场景介绍

该库扩展了原生JSON功能，提供了额外的错误处理、循环引用检测、BigInt处理以及对不同输入类型的严格检查。代码中底层依赖于原生JSON.parse和JSON.stringify，但在此基础上加入了多种自定义逻辑并提供额外的has和remove接口，具体可见[@arkts.json](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-json)。

JSON扩展库主要适用于以下场景：

- 需要处理BigInt的JSON解析或序列化。
    
- 需要更严格的参数校验和错误处理。
    
- 需要在序列化对象时检测循环引用。
    
- 需要安全的对象操作（has/remove）。
    

该库适用于需要增强JSON功能的场景，特别是在处理BigInt和严格的参数校验时。

## JSON扩展说明

### parse

parse(text: string, reviver?: Transformer, options?: ParseOptions): Object | null

解析JSON字符串，支持BigInt模式。

**与原生的区别：**

|特性|原生parse|本库parse|
|:--|:--|:--|
|BigInt支持|不支持（抛出TypeError）|支持（通过parseBigInt扩展）|
|参数校验|弱校验|强校验（抛出BusinessError）|
|错误信息|原生错误（如SyntaxError）|自定义BusinessError|
|reviver参数|支持|支持，但强制类型检查|

### stringify

stringify(value: Object, replacer?: (number | string)[] | null, space?: string | number): string

将对象转换为JSON字符串，支持BigInt模式。

**与原生的区别：**

|特性|原生stringify|本库stringify|
|:--|:--|:--|
|BigInt支持|不支持（抛出TypeError）|支持（通过stringifyBigInt扩展）|
|循环引用检测|抛出TypeError|检测并抛出BusinessError|
|参数校验|弱校验|强校验（replacer必须是函数或数组）|
|错误信息|原生错误|自定义BusinessError|

### has

has(obj: object, property: string): boolean

检查对象是否包含指定的属性，确保传入的值是一个对象，并且属性键是有效的字符串。

**与原生的区别：**

|特性|原生方式（obj.hasOwnProperty）|本库has|
|:--|:--|:--|
|参数校验|无校验（可能误用）|强制检查obj是普通对象，property是非空字符串|
|错误处理|可能静默失败|抛出BusinessError|

### remove

remove(obj: object, property: string): void

从对象中删除指定的属性。

|特性|原生方式（delete obj.key）|本库remove|
|:--|:--|:--|
|参数校验|无校验（可能误删）|强制检查obj是普通对象，property是非空字符串|
|错误处理|可能静默失败|抛出BusinessError|

### 总结

|功能|原生JSON|本库|
|:--|:--|:--|
|严格参数校验|不支持|支持|
|循环引用检测|不支持|支持|
|BigInt处理|不支持|支持|
|增强的错误处理（BusinessError）|不支持|支持|
|额外方法（has/remove）|不支持|支持|

## 开发场景

### 解析包含嵌套引号的JSON字符串场景

JSON字符串中的嵌套引号会破坏其结构，将导致解析失败。

1. // 比如以下JSON字符串，由于嵌套引号导致结构破坏，执行JSON.parse将会抛异常。
2. // let jsonStr = `{"info": "{"name": "zhangsan", "age": 18}"}`;

以下提供两种方式解决该场景问题：

方式1：避免出现嵌套引号的操作。

1. import { JSON } from '@kit.ArkTS';

2. interface Info {
3.   name: string;
4.   age: number;
5. }

6. interface TestObj {
7.   info: Info;
8. }

9. interface TestStr {
10.   info: string;
11. }

12. /*
13.  * 将原始JSON字符串`{"info": "{"name": "zhangsan", "age": 18}"}`
14.  * 修改为`{"info": {"name": "zhangsan", "age": 18}}`。
15.  * */
16. let jsonStr = `{"info": {"name": "zhangsan", "age": 18}}`;
17. let obj1  = JSON.parse(jsonStr) as TestObj;
18. console.info(JSON.stringify(obj1));    //{"info":{"name":"zhangsan","age":18}}
19. // 获取JSON字符串中的name信息
20. console.info(obj1.info.name); // zhangsan

方式2：将JSON字符串中嵌套的引号进行双重转义，恢复JSON的正常结构。

1. import { JSON } from '@kit.ArkTS';

2. interface Info {
3.   name: string;
4.   age: number;
5. }

6. interface TestObj {
7.   info: Info;
8. }

9. interface TestStr {
10.   info: string;
11. }

12. /*
13.  * 将原始JSON字符串`{"info": "{"name": "zhangsan", "age": 18}"}`进行双重转义，
14.  * 修改为`{"info": "{\\"name\\": \\"zhangsan\\", \\"age\\": 18}"}`。
15.  * */
16. let jsonStr = `{"info": "{\\"name\\": \\"zhangsan\\", \\"age\\": 18}"}`;
17. let obj2 = JSON.parse(jsonStr) as TestStr;
18. console.info(JSON.stringify(obj2));    // {"info":"{\"name\": \"zhangsan\", \"age\": 18}"}
19. // 获取JSON字符串中的name信息
20. let obj3 = JSON.parse(obj2.info) as Info;
21. console.info(obj3.name); // zhangsan

### 解析包含大整数的JSON字符串场景

当JSON字符串中存在小于-(2^53-1)或大于(2^53-1)的整数时，解析后数据会出现精度丢失或不正确的情况。该解析场景需要指定BigIntMode，将大整数解析为BigInt。

1. import { JSON } from '@kit.ArkTS';

2. let numberText = '{"number": 10, "largeNumber": 112233445566778899}';

3. let numberObj1 = JSON.parse(numberText) as Object;
4. console.info((numberObj1 as object)?.["largeNumber"]);    // 112233445566778900

5. // 使用PARSE_AS_BIGINT的BigInt模式进行解析，避免出现大整数解析错误。
6. let options: JSON.ParseOptions = {
7.   bigIntMode: JSON.BigIntMode.PARSE_AS_BIGINT,
8. }

9. let numberObj2 = JSON.parse(numberText, null, options) as Object;

10. console.info(typeof (numberObj2 as object)?.["number"]);   // number
11. console.info((numberObj2 as object)?.["number"]);    // 10

12. console.info(typeof (numberObj2 as object)?.["largeNumber"]);    // bigint
13. console.info((numberObj2 as object)?.["largeNumber"]);    // 112233445566778899

### 序列化BigInt对象场景

为弥补原生JSON无法序列化BigInt对象的缺陷，本库提供以下两种JSON序列化方式：

方式1：不使用自定义转换函数，直接序列化BigInt对象。

1. import { JSON } from '@kit.ArkTS';

2. let bigIntObject = BigInt(112233445566778899n)

3. console.info(JSON.stringify(bigIntObject)); // 112233445566778899

方式2：使用自定义转换函数，需预处理BigInt对象进行序列化操作。

1. import { JSON } from '@kit.ArkTS';

2. let bigIntObject = BigInt(112233445566778899n)

3. // 错误序列化用法：自定义函数中直接返回BigInt对象
4. // JSON.stringify(bigIntObject, (key: string, value: Object): Object =>{ return value; });

5. // 正确序列化用法：自定义函数中将BigInt对象预处理为string对象
6. let result: string = JSON.stringify(bigIntObject, (key: string, value: Object): Object => {
7.   if (typeof value === 'bigint') {
8.     return value.toString();
9.   }
10.   return value;
11. });
12. console.info("result:", result); // result: "112233445566778899"

### 序列化浮点数number场景

在JSON序列化中，浮点数处理存在一个特殊行为：当小数部分为零时，为保持数值的简洁表示，序列化结果会自动省略小数部分。这可能导致精度信息丢失，影响需要精确表示浮点数的场景（如金融金额、科学计量）。以下示例提供解决该场景的方法：

1. import { JSON } from '@kit.ArkTS';

2. // 序列化小数部分不为零的浮点数，可以正常序列化。
3. let floatNumber1 = 10.12345;
4. console.info(JSON.stringify(floatNumber1)); // 10.12345

5. // 序列化小数部分为零的浮点数，为保持数值的简洁表示，会丢失小数部分的精度。
6. let floatNumber2 = 10.00;
7. console.info(JSON.stringify(floatNumber2)); // 10

8. // 以下是防止浮点数精度丢失的方法：
9. let result = JSON.stringify(floatNumber2, (key: string, value: Object): Object => {
10.   if (typeof value === 'number') {
11.     // 按照业务场景需要，定制所需的固定精度。
12.     return value.toFixed(2);
13.   }
14.   return value;
15. });
16. console.info(result); // "10.00"
# 线性容器

更新时间: 2025-12-16 16:39

线性容器实现能按顺序访问的数据结构，其底层主要通过数组实现，包括ArrayList、Vector、List、LinkedList、Deque、Queue和Stack。

线性容器优化了数据访问速度，运行时（Runtime）通过一条字节码指令即可完成增、删、改、查等操作。

## 各线性容器类型特征对比

|类名|特征及建议使用场景|
|:--|:--|
|ArrayList|动态数组，占用一片连续的内存空间。需要频繁读取元素时推荐使用。|
|List|单向链表，占用的空间可以不连续。推荐在需要频繁插入和删除元素，且需要使用单向链表时使用。|
|LinkedList|双向链表，占用的空间可以不连续。推荐在需要频繁插入和删除元素，且需要使用双向链表时使用。|
|Deque|双端队列，支持从头尾两端进行元素的插入和删除操作，占用连续的内存空间。推荐在需要频繁访问和操作头尾元素时使用。|
|Queue|队列，是一种从尾部插入元素、从头部移除元素的数据结构，占用连续的内存空间，适用于先进先出的场景。|
|Stack|栈，只能从一端进行插入和删除操作，占用连续的内存空间。适用于先进后出的场景。|
|Vector|动态数组，占用连续的内存空间。已不再维护，推荐使用ArrayList。|

## ArrayList

[ArrayList](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arraylist)即动态数组，可用来构造全局的数组对象。需要频繁读取集合元素时，推荐使用ArrayList。

ArrayList依据泛型定义，存储位置为连续的内存空间，初始容量为10，支持动态扩容，每次扩容为原始容量的1.5倍。

ArrayList支持增、删、改、查操作，常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|add(element: T)|在数组尾部增加一个元素。|
|增加元素|insert(element: T, index: number)|在指定位置插入一个元素。|
|访问元素|arr[index: number]|获取指定index对应的value值。|
|访问元素|forEach(callbackFn: (value: T, index?: number, arrlist?: ArrayList<T>) => void, thisArg?: Object)|访问整个ArrayList容器的元素，其中callbackFn是forEach方法中用于处理每个元素的回调函数，它接收当前元素、索引和原列表作为参数。|
|访问元素|[Symbol.iterator]():IterableIterator<T>|创建迭代器以进行数据访问。|
|修改元素|arr[index] = xxx|修改指定index位置对应的value值。|
|删除元素|remove(element: T)|删除第一个匹配到的元素。|
|删除元素|removeByRange(fromIndex: number, toIndex:number)|删除指定范围内的元素。|

## List

[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-list)可用来构造一个单向链表对象，若需要查找List中某一个元素，只能从头结点开始遍历。List依据泛型定义，存储的元素在内存中的存储位置可以不连续。

List和[LinkedList](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-linkedlist)相比，LinkedList是双向链表，支持在头部和尾部快速增删操作。List则是单向链表，不支持双向操作。

当需要频繁插入和删除元素，并且使用单向链表时，推荐使用List进行高效操作。

可以通过get/set等接口修改存储的元素，List支持增、删、改、查操作，常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|add(element: T)|在数组尾部增加一个元素。|
|增加元素|insert(element: T, index: number)|在指定位置增加一个元素。|
|访问元素|get(index: number)|获取指定index位置对应的元素。|
|访问元素|list[index: number]|获取指定索引位置的元素。若索引超出数组范围（index < 0 或 index >= list.length），或者数组是稀疏数组（存在未赋值的索引），则返回undefined。|
|访问元素|getFirst()|获取第一个元素。|
|访问元素|getLast()|获取最后一个元素。|
|访问元素|getIndexOf(element: T)|获取第一个匹配指定元素的位置。|
|访问元素|getLastIndexOf(element: T)|获取最后一个匹配指定元素的位置。|
|访问元素|forEach(callbackfn: (value:T, index?: number, list?: List<T>)=> void,thisArg?: Object)|遍历访问整个List容器中的每个元素，并执行指定的回调函数。|
|访问元素|[Symbol.iterator]():IterableIterator<T>|创建迭代器以进行数据访问。|
|修改元素|set(index:number, element: T)|修改指定index位置的元素值为element。|
|修改元素|list[index] = element|修改指定index位置的元素值为element时，不会对链表中的实际节点进行任何更改，仅会在对象上添加一个属性，这将导致程序状态与链表实际内容不一致，从而产生未定义行为。|
|修改元素|replaceAllElements(callbackFn:(value: T,index?: number,list?: List<T>)=>T,thisArg?: Object)|对List内元素进行逐个替换。|
|删除元素|remove(element: T)|通过 === 运算符逐个比对链表中的元素，删除第一个匹配成功的节点。对于对象类型，只有当传入的对象与链表中某节点的引用完全一致时才会被删除。|
|删除元素|removeByIndex(index:number)|删除index位置对应的元素，如果index超出范围，则会报out of range错误。|

## LinkedList

[LinkedList](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-linkedlist)可用于构造双向链表对象，支持在任意节点向前或向后遍历LinkedList。LinkedList依据泛型定义，其元素在内存中的存储位置可以不连续。

LinkedList和[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-list)相比，LinkedList是双向链表，支持快速的头尾增删操作。List是单向链表，不支持双向操作。

LinkedList和[ArrayList](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arraylist)相比，LinkedList插入数据的效率高于ArrayList，ArrayList查询效率高于LinkedList。

需要频繁插入删除元素且使用双向链表时，推荐使用LinkedList。

可以通过get/set等接口修改存储的元素。LinkedList支持增、删、改、查操作，常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|add(element: T)|在数组尾部增加一个元素。|
|增加元素|insert(element: T, index: number)|在指定位置插入一个元素。|
|访问元素|get(index: number)|获取指定index位置对应的元素。|
|访问元素|list[index: number]|获取指定index位置对应的元素，若索引超出数组范围（index < 0 或 index >= list.length），或者数组是稀疏数组（存在未赋值的索引），则返回undefined。|
|访问元素|getFirst()|获取第一个元素。|
|访问元素|getLast()|获取最后一个元素。|
|访问元素|getIndexOf(element: T)|获取第一个匹配指定元素的位置。|
|访问元素|getLastIndexOf(element: T)|获取最后一个匹配指定元素的位置。|
|访问元素|forEach(callbackFn: (value: T, index?: number, list?: LinkedList<T>) => void, thisArg?: Object)|遍历访问整个LinkedList容器的每个元素，并执行指定的回调函数。|
|访问元素|[Symbol.iterator]():IterableIterator<T>|创建迭代器以进行数据访问。|
|修改元素|set(index:number, element: T)|修改指定index位置的元素值为element。|
|修改元素|list[index] = element|修改指定index位置的元素值为element，若索引超出数组范围（index < 0 或 index >= list.length），或者数组是稀疏数组（存在未赋值的索引），则可能导致未定义行为。|
|删除元素|remove(element: T)|删除第一个匹配到的元素。|
|删除元素|removeByIndex(index:number)|删除index位置对应的元素。|

## Deque

[Deque](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-deque)可用来构造双端队列对象，存储元素遵循先进先出以及先进后出的规则，双端队列可以分别从队头或者队尾进行访问。

Deque依据泛型定义，要求存储位置为连续的内存空间，初始容量为8，支持动态扩容，每次扩容为原容量的2倍。Deque底层采用循环队列实现，入队和出队操作效率高。

Deque和[Queue](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-queue)相比，Deque支持在两端进行元素的增删操作，而Queue仅支持在头部删除元素，尾部增加元素。

Deque和[Vector](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-vector)相比，都支持在两端增删元素，但Deque不支持中间插入。Deque在头部插入和删除元素的效率高于Vector，而Vector访问元素的效率高于Deque。

需要频繁在两端增删元素时，推荐使用Deque。

Deque支持增、删、改、查操作。常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|insertFront(element: T)|在头部增加一个元素。|
|增加元素|insertEnd(element: T)|在尾部增加一个元素。|
|访问元素|getFirst()|获取第一个元素，不进行出队操作。|
|访问元素|getLast()|获取最后一个元素，不进行出队操作。|
|访问元素|forEach(callbackFn:(value: T, index?: number, deque?: Deque<T>) => void, thisArg?: Object)|遍历访问整个Deque容器的每个元素，并执行指定的回调函数。|
|访问元素|[Symbol.iterator]():IterableIterator<T>|创建迭代器以进行数据访问。|
|删除元素|popFirst()|将队首元素作为返回值进行返回，并将其出队，如果队列为空，则返回undefined。|
|删除元素|popLast()|将队尾元素作为返回值进行返回，并将其出队，如果队列为空，则返回undefined。|

## Queue

[Queue](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-queue)可用来构造队列对象，存储元素遵循先进先出的规则。

Queue基于泛型定义，存储位置为连续的内存空间，初始容量为8，支持动态扩容，每次扩容容量翻倍。

Queue底层采用循环队列实现，入队和出队操作效率高。

Queue和[Deque](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-deque)相比，Queue仅支持在头部删除元素，尾部增加元素，而Deque支持在两端进行元素的增删操作。

符合先进先出的场景可以使用Queue。

Queue支持增、删、改、查操作，常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|add(element: T)|在尾部增加一个元素。|
|访问元素|getFirst()|获取队首元素，不进行出队操作。|
|访问元素|forEach(callbackFn: (value: T, index?: number, queue?: Queue<T>) => void,thisArg?: Object)|遍历访问整个Queue容器的每个元素，并执行指定的回调函数。|
|访问元素|[Symbol.iterator]():IterableIterator<T>|创建迭代器以进行数据访问。|
|删除元素|pop()|将队首元素作为返回值进行返回，并将其移除。|

## Stack

[Stack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-stack)可用来构造栈对象，存储元素遵循先进后出的规则。

Stack基于泛型定义，要求使用连续的内存空间存储元素，初始容量为8，并支持动态扩容，每次扩容为原容量的1.5倍。Stack底层使用数组实现，入栈和出栈操作均在数组的一端进行。

Stack和[Queue](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-queue)相比，Queue基于循环队列实现，仅支持在头部删除元素，尾部增加元素，而Stack都在一端进行操作。

符合先进后出的场景可以使用Stack。

Stack支持增、删、改、查操作，常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|push(item: T)|在栈顶增加一个元素。|
|访问元素|peek()|获取栈顶元素，不进行出队操作。|
|访问元素|locate(element: T)|获取元素对应的位置。|
|访问元素|forEach(callbackFn: (value: T, index?: number, stack?: Stack<T>) => void, thisArg?: Object)|遍历访问整个Stack容器的每个元素，并执行指定的回调函数。|
|访问元素|[Symbol.iterator]():IterableIterator<T>|创建迭代器以进行数据访问。|
|删除元素|pop()|将栈顶元素作为返回值进行返回，并将其移除。|

## Vector

说明

API version 9开始，该接口不再维护，推荐使用[ArrayList](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arraylist)。

[Vector](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-vector)是一种连续存储结构，用于创建全局数组对象。它基于泛型定义，要求存储在连续的内存空间中。Vector的初始容量为10，支持动态扩容，每次扩容时容量增加为原来的两倍。

Vector和[ArrayList](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arraylist)相似，都基于数组实现，但Vector提供了更多操作数组的接口，支持操作符访问，增加get/set接口，提供更完善的校验和容错机制，满足不同的场景需求。

Vector支持增、删、改、查操作，常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|add(element: T)|在数组尾部增加一个元素。|
|增加元素|insert(element: T, index: number)|在指定位置插入一个元素。|
|访问元素|get(index: number)|获取指定index位置对应的元素。|
|访问元素|vec[index: number]|获取指定index位置对应的元素，通过指令获取保证访问速度。|
|访问元素|getFirst()|获取第一个元素。|
|访问元素|getLastElement()|获取最后一个元素。|
|访问元素|getIndexOf(element: T)|获取第一个匹配指定元素的位置。|
|访问元素|getLastIndexOf(element: T)|获取最后一个匹配指定元素的位置。|
|访问元素|forEach(callbackFn: (value: T, index?: number, Vector?: Vector<T>) => void, thisArg?: Object)|遍历访问整个Vector容器的每个元素，并执行指定的回调函数。|
|访问元素|[Symbol.iterator]():IterableIterator<T>|创建迭代器以进行数据访问。|
|修改元素|set(index:number, element: T)|修改指定index位置的元素值为element。|
|修改元素|vec[index] = element|修改指定index位置的元素值为element。|
|修改元素|replaceAllElements(callbackFn: (value: T, index?: number, vector?: Vector<T>) => T, thisArg?: Object)|逐个替换Vector内的元素。|
|修改元素|setLength(newSize:number)|设置Vector的长度大小。|
|删除元素|remove(element: T)|删除第一个匹配到的元素。|
|删除元素|removeByIndex(index:number)|删除index位置对应的元素。|
|删除元素|removeByRange(fromIndex:number,toIndex:number)|删除指定范围内的元素。|

## 线性容器的使用

此处列举常用的线性容器ArrayList、Deque、Stack、List的使用示例，包括导入模块、添加元素、访问元素及修改等操作。示例代码如下所示：

1. // ArrayList
2. import { ArrayList } from '@kit.ArkTS'; // 导入ArrayList模块

3. let arrayList1: ArrayList<string> = new ArrayList();
4. arrayList1.add('a'); // 增加一个值为'a'的元素
5. let arrayList2: ArrayList<number> = new ArrayList();
6. arrayList2.add(1); // 增加一个值为1的元素
7. console.info(`result: ${arrayList2[0]}`); // 访问索引为0的元素。输出：result: 1
8. arrayList1[0] = 'one'; // 修改索引为0的元素
9. console.info(`result: ${arrayList1[0]}`); // 输出：result: one

10. // Deque
11. import { Deque } from '@kit.ArkTS'; // 导入Deque模块

12. let deque1: Deque<string> = new Deque();
13. deque1.insertFront('a'); // 头部增加一个值为'a'的元素
14. let deque2: Deque<number> = new Deque();
15. deque2.insertFront(1); // 头部增加一个值为1的元素
16. console.info(`result: ${deque2.getFirst()}`); // 访问队列首部的元素。输出：result: 1
17. deque1.insertEnd('one'); // 尾部增加一个值为'one'的元素
18. console.info(`result: ${deque1.getLast()}`); // 访问队列尾部的元素。输出：result: one

19. // Stack
20. import { Stack } from '@kit.ArkTS'; // 导入Stack模块

21. let stack1: Stack<string> = new Stack();
22. stack1.push('a'); // 向栈里增加一个值为'a'的元素
23. let stack2: Stack<number> = new Stack();
24. stack2.push(1); // 向栈里增加一个值为1的元素
25. console.info(`result: ${stack1.peek()}`); // 访问栈顶元素。输出：result: a
26. console.info(`result: ${stack2.pop()}`); // 删除栈顶元素并返回该删除元素。输出：result: 1
27. console.info(`result: ${stack2.length}`); // 输出：result: 0

28. // List
29. import { List } from '@kit.ArkTS'; // 导入List模块

30. let list1: List<string> = new List();
31. list1.add('a'); // 增加一个值为'a'的元素
32. let list2: List<number> = new List();
33. list2.insert(0, 0); // 在0号位置插入（增加）一个值为0的元素
34. let list3: List<Array<number>> = new List();
35. let b2 = [1, 2, 3];
36. list3.add(b2); // 增加一个Array类型的元素
37. console.info(`result: ${list1[0]}`); // 访问索引为0的元素。输出：result: a
38. console.info(`result: ${list3.get(0)}`); // 访问索引为0的元素。输出：result: 1,2,3

# 非线性容器

更新时间: 2025-12-16 16:39

非线性容器实现能快速查找的数据结构，其底层通过hash或者红黑树实现，包括HashMap、HashSet、TreeMap、TreeSet、LightWeightMap、LightWeightSet、PlainArray七种。非线性容器中的key及value的类型均满足ECMA标准。

## 各非线性容器类型特征对比

|类名|特征及建议使用场景|
|:--|:--|
|HashMap|存储具有关联关系的键值对集合。键唯一，依据键的hash值确定存储位置。访问速度快，但不能自定义排序。推荐用于需要快速存取、插入删除键值对数据时使用。|
|HashSet|存储一系列值的集合。值唯一，依据值的hash确定存储位置。允许放入null值，但不能自定义排序。适用于不重复的集合或去重某个集合。|
|TreeMap|存储具有关联关系的键值对集合。键唯一，允许用户自定义排序方法。适用于按序存储键值对的场景。|
|TreeSet|存储一系列值的集合。值唯一，允许用户自定义排序方法，但不建议放入null值。适用于按序存储集合的场景。|
|LightWeightMap|存储具有关联关系的键值对集合。键唯一，底层采用轻量级结构，空间占用小。推荐用于存取键值对数据且内存不充足时。|
|LightWeightSet|存储一系列值的集合。值唯一，底层采用轻量级结构，空间占用小。适用于不重复的集合或去重某个集合。|
|PlainArray|存储具有关联关系的键值对集合。键唯一，底层与LightWeightMap一样采用轻量级结构，键固定为number类型。适用于存储键为number类型键值对的场景。|

## HashMap

[HashMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-hashmap)可用来存储具有关联关系的key-value键值对集合，存储元素中key是唯一的，每个key会对应一个value值。

HashMap通过泛型定义，利用键的哈希值确定存储位置，实现快速查找。初始容量为16，支持动态扩容，每次扩容为原容量的两倍。底层基于哈希表实现，冲突处理采用链地址法。

HashMap和[TreeMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-treemap)相比，HashMap依据键的hashCode存取数据，访问速度较快。TreeMap则按顺序存取，效率较低。

[HashSet](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-hashset)基于HashMap实现。HashMap的输入参数由key、value两个值组成。在HashSet中，只处理value对象。

需要快速存取、删除以及插入键值对数据时，推荐使用HashMap。

HashMap支持增、删、改、查操作，常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|set(key: K, value: V)|增加一个键值对。|
|访问元素|get(key: K)|获取key对应的value值。|
|访问元素|keys()|返回一个迭代器对象，包含map中的所有key值。|
|访问元素|values()|返回一个迭代器对象，包含map中的所有value值。|
|访问元素|entries()|返回一个迭代器对象，包含map中的所有键值对。|
|访问元素|forEach(callbackFn: (value?: V, key?: K, map?: HashMap<K, V>) => void, thisArg?: Object)|遍历访问整个map的元素。|
|访问元素|[Symbol.iterator]():IterableIterator<[K,V]>|创建迭代器以访问数据。|
|修改元素|replace(key: K, newValue: V)|修改指定key对应的value值。|
|修改元素|forEach(callbackFn: (value?: V, key?: K, map?: HashMap<K, V>) => void, thisArg?: Object)|遍历并修改整个map的元素。|
|删除元素|remove(key: K)|删除map中匹配到的键值对。|
|删除元素|clear()|清空整个map。|

## HashSet

[HashSet](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-hashset)可用来存储一系列值的集合，存储元素中value是唯一的。

HashSet基于泛型定义，集合中通过value的hash值确定存储位置，从而快速找到该值。初始容量为16，支持动态扩容，每次扩容为原始容量的2倍。value的类型需满足ECMA标准。HashSet基于[HashMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-hashmap)实现，只处理value对象，底层数据结构与HashMap一致。

HashSet和[TreeSet](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-treeset)相比，HashSet中的数据无序存放，不支持用户指定排序方式，而TreeSet中的数据有序存放，支持用户通过排序函数对元素进行排序。它们集合中的元素都不允许重复，HashSet允许放入null值，但TreeSet不建议存放null值，可能会对排序结果产生影响。

可以利用HashSet的不重复特性，在需要去重或确保集合元素唯一性时使用。

HashSet支持增、删、改、查操作，常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|add(value: T)|增加一个值。|
|访问元素|values()|返回一个迭代器对象，包含set中的所有value。|
|访问元素|entries()|返回一个迭代器对象，包含类似键值对的数组，键值都是value。|
|访问元素|forEach(callbackFn: (value?: T, key?: T, set?: HashSet<T>) => void, thisArg?: Object)|遍历访问整个set的元素。|
|访问元素|[Symbol.iterator]():IterableIterator<T>|创建迭代器以进行数据访问。|
|修改元素|forEach(callbackFn: (value?: T, key?: T, set?: HashSet<T>) => void, thisArg?: Object)|通过遍历对set中的元素进行操作，可能包括但不限于修改元素。|
|删除元素|remove(value: T)|删除指定的元素。|
|删除元素|clear()|清空整个set。|

## TreeMap

[TreeMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-treemap)用于存储具有关联关系的key-value键值对集合，存储元素中key是唯一的，每个key对应一个value值。

TreeMap的key按照泛型定义有序存储，基于红黑树实现，支持快速插入和删除，key的类型需满足ECMA标准。

TreeMap和[HashMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-hashmap)相比，HashMap依据键的hashCode存取数据，访问速度较快。而TreeMap是有序存取，效率较低。

一般需要存储有序键值对的场景，可以使用TreeMap。

TreeMap支持增、删、改、查操作，常用 API 如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|set(key: K, value: V)|增加一个键值对。|
|访问元素|get(key: K)|获取key对应的value值。|
|访问元素|getFirstKey()|获取map中排在首位的key值。|
|访问元素|getLastKey()|获取map中排在末位的key值。|
|访问元素|keys()|返回一个迭代器对象，包含map中的所有key值。|
|访问元素|values()|返回一个迭代器对象，包含map中的所有value值。|
|访问元素|entries()|返回一个迭代器对象，包含map中的所有键值对。|
|访问元素|forEach(callbackFn: (value?: V, key?: K, map?: TreeMap<K, V>) => void, thisArg?: Object)|遍历访问整个map的元素。|
|访问元素|[Symbol.iterator]():IterableIterator<[K,V]>|创建迭代器以进行数据访问。|
|修改元素|replace(key: K, newValue: V)|修改指定key对应的value值。|
|修改元素|forEach(callbackFn: (value?: V, key?: K, map?: TreeMap<K, V>) => void, thisArg?: Object)|通过遍历对map中的元素进行操作，可能包括但不限于修改元素。|
|删除元素|remove(key: K)|删除map中匹配到的键值对。|
|删除元素|clear()|清空整个map。|

## TreeSet

[TreeSet](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-treeset)可用来存储一系列值的集合，存储元素中value是唯一的。

TreeSet根据泛型定义有序存储值，底层实现基于红黑树，支持快速插入和删除。value的类型符合ECMA标准。

TreeSet基于[TreeMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-treemap)实现，仅处理value对象，用于存储值的集合，元素中value唯一，并支持按用户定义的排序函数排序。

TreeSet和[HashSet](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-hashset)相比，HashSet无序存放数据，TreeSet有序存放数据。两者元素均不允许重复，HashSet允许null值，但TreeSet不建议存放null值，可能影响排序。

在需要存储有序集合的场景中，可以使用TreeSet。

TreeSet支持增、删、改、查操作，常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|add(value: T)|增加一个值。|
|访问元素|values()|返回一个迭代器对象，包含set中的所有value值。|
|访问元素|entries()|返回一个迭代器对象，包含类似键值对的数组，键值都是value。|
|访问元素|getFirstValue()|获取set中排在首位的value值。|
|访问元素|getLastValue()|获取set中排在末位的value值。|
|访问元素|forEach(callbackFn: (value?: T, key?: T, set?: TreeSet<T>) => void, thisArg?: Object)|遍历访问整个set的元素。|
|访问元素|[Symbol.iterator]():IterableIterator<T>|创建迭代器以进行数据访问。|
|修改元素|forEach(callbackFn: (value?: T, key?: T, set?: TreeSet<T>) => void, thisArg?: Object)|通过遍历对set中的元素进行操作，可能包括但不限于修改元素。|
|删除元素|remove(value: T)|删除指定的元素。|
|删除元素|clear()|清空整个set。|

## LightWeightMap

[LightWeightMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-lightweightmap)用于存储具有唯一键的键值对集合，存储元素中key是唯一的，每个key会对应一个value值。LightWeightMap依据泛型定义，采用轻量级结构，底层通过hash实现唯一key，冲突策略为线性探测。集合中的key值的查找依赖于hash值以及二分查找算法，通过一个数组存储hash值，然后映射到其他数组中的key值以及value值，key的类型满足ECMA标准。

初始默认容量为8，每次扩容为原容量的2倍。

LightWeightMap和[HashMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-hashmap)都是用来存储具有关联关系的key-value键值对集合，但LightWeightMap占用内存更小。

当需要存储具有关联关系的key-value键值对集合时，推荐使用占用内存更小的LightWeightMap。

LightWeightMap支持增、删、改、查操作，常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|set(key: K, value: V)|增加一个键值对。|
|访问元素|get(key: K)|获取key对应的value值。|
|访问元素|getIndexOfKey(key: K)|获取map中指定key的index。|
|访问元素|getIndexOfValue(value: V)|获取map中指定value出现的第一个的index。|
|访问元素|keys()|返回一个迭代器对象，包含map中的所有key值。|
|访问元素|values()|返回一个迭代器对象，包含map中的所有value值。|
|访问元素|entries()|返回一个迭代器对象，包含map中的所有键值对。|
|访问元素|getKeyAt(index: number)|获取指定index对应的key值。|
|访问元素|getValueAt(index: number)|获取指定index对应的value值。|
|访问元素|forEach(callbackFn: (value?: V, key?: K, map?: LightWeightMap<K, V>) => void, thisArg?: Object)|遍历访问整个map的元素。|
|访问元素|[Symbol.iterator]():IterableIterator<[K,V]>|创建迭代器以进行数据访问。|
|修改元素|setValueAt(index: number, newValue: V)|修改指定index对应的value值。|
|修改元素|forEach(callbackFn: (value?: V, key?: K, map?: LightWeightMap<K, V>) => void, thisArg?: Object)|通过遍历对map中的元素进行操作，可能包括但不限于修改元素。|
|删除元素|remove(key: K)|删除map中指定key匹配到的键值对。|
|删除元素|removeAt(index: number)|删除map中指定index对应的键值对。|
|删除元素|clear()|清空整个map。|

## LightWeightSet

[LightWeightSet](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-lightweightset)可用来存储一系列值的集合，存储元素中value是唯一的。

LightWeightSet依据泛型定义，采用更加轻量级的结构，初始默认容量为8，每次扩容为原始容量的2倍。集合中的value值的查找依赖于hash值以及二分查找算法，通过一个数组存储hash值，然后映射到其他数组中的value值，value的类型满足ECMA标准。

LightWeightSet底层通过hash表结构实现value的唯一性，冲突策略采用线性探测法，查找策略基于二分查找法。

LightWeightSet和[HashSet](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-hashset)都是用来存储键值的集合，但LightWeightSet的占用内存更小。

当需要存取某个集合或是对某个集合去重时，推荐使用占用内存更小的LightWeightSet。

LightWeightSet支持增、删、改、查操作。常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|add(obj: T)|增加一个值。|
|访问元素|getIndexOf(key: T)|获取对应的index值。|
|访问元素|getValueAt(index: number)|获取指定index对应的value值。|
|访问元素|values()|返回一个迭代器对象，包含set中的所有value值。|
|访问元素|entries()|返回一个迭代器对象，包含类似键值对的数组，键值都是value。|
|访问元素|forEach(callbackFn: (value?: T, key?: T, set?: LightWeightSet<T>) => void, thisArg?: Object)|遍历访问整个set的元素。|
|访问元素|[Symbol.iterator]():IterableIterator<T>|创建迭代器以进行数据访问。|
|修改元素|forEach(callbackFn: (value?: T, key?: T, set?: LightWeightSet<T>) => void, thisArg?: Object)|通过遍历对set中的元素进行操作，可能包括但不限于修改元素。|
|删除元素|remove(key: K)|删除指定的元素。|
|删除元素|removeAt(index: number)|删除set中指定index对应的值。|
|删除元素|clear()|清空整个set。|

## PlainArray

[PlainArray](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-plainarray)可用来存储具有关联关系的键值对集合，存储元素中key是唯一的，并且对于PlainArray来说，其key的类型为number类型。每个key会对应一个value值，类型依据泛型的定义，PlainArray采用轻量级的结构，集合中的key值的查找依赖于二分查找算法，然后映射到其他数组中的value值。

初始默认容量为16，每次扩容为原始容量的2倍。

PlainArray和[LightWeightMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-lightweightmap)都用于存储键值对，且采用轻量级结构。不过，PlainArray的键值类型仅限于number。

当需要存储键为number类型的键值对时，可以使用PlainArray。

PlainArray支持增、删、改、查操作。常用API如下：

|操作|方法|描述|
|:--|:--|:--|
|增加元素|add(key: number,value: T)|增加一个键值对。|
|访问元素|get(key: number)|获取key对应的value值。|
|访问元素|getIndexOfKey(key: number)|获取PlainArray中指定key的index。|
|访问元素|getIndexOfValue(value: T)|获取PlainArray中指定value出现的第一个的index。|
|访问元素|getKeyAt(index: number)|获取指定index对应的key值。|
|访问元素|getValueAt(index: number)|获取指定index对应的value值。|
|访问元素|forEach(callbackFn: (value: T, index?: number, PlainArray?: PlainArray<T>) => void, thisArg?: Object)|遍历访问整个PlainArray的元素。|
|访问元素|[Symbol.iterator]():IterableIterator<[number, T]>|创建迭代器以进行数据访问。|
|修改元素|setValueAt(index:number, value: T)|修改指定index对应的value值。|
|修改元素|forEach(callbackFn: (value: T, index?: number, PlainArray?: PlainArray<T>) => void, thisArg?: Object)|通过遍历对PlainArray中的元素进行操作，可能包括但不限于修改元素。|
|删除元素|remove(key: number)|删除PlainArray中指定key匹配到的键值对。|
|删除元素|removeAt(index: number)|删除PlainArray中指定index对应的键值对。|
|删除元素|removeRangeFrom(index: number, size: number)|删除PlainArray中指定范围内的元素。|
|删除元素|clear()|清空整个PlainArray。|

## 非线性容器的使用

此处列举常用的非线性容器HashMap、TreeMap、LightWeightMap、PlainArray的使用示例，包括导入模块、增加元素、访问元素及修改等操作，示例代码如下所示：

1. // HashMap
2. import { HashMap } from '@kit.ArkTS'; // 导入HashMap模块

3. let hashMap1: HashMap<string, number> = new HashMap();
4. hashMap1.set('a', 123); // 增加一个键为'a'，值为123的元素
5. let hashMap2: HashMap<number, number> = new HashMap();
6. hashMap2.set(4, 123); // 增加一个键为4，值为123的元素
7. console.info(`result: ${hashMap2.hasKey(4)}`); // 判断是否含有键为4的元素。输出：result: true
8. console.info(`result: ${hashMap1.get('a')}`); // 访问键为'a'的元素。输出：result: 123

9. // TreeMap
10. import { TreeMap } from '@kit.ArkTS'; // 导入TreeMap模块

11. let treeMap: TreeMap<string, number> = new TreeMap();
12. treeMap.set('a', 123); // 增加一个键为'a'，值为123的元素
13. treeMap.set('6', 356); // 增加一个键为'6'，值为356的元素
14. console.info(`result: ${treeMap.get('a')}`); // 访问键为'a'的元素。输出：result: 123
15. console.info(`result: ${treeMap.getFirstKey()}`); // 访问首元素。输出：result: 6
16. console.info(`result: ${treeMap.getLastKey()}`); // 访问尾元素。输出：result: a

17. // LightWeightMap
18. import { LightWeightMap } from '@kit.ArkTS'; // 导入LightWeightMap模块

19. let lightWeightMap: LightWeightMap<string, number> = new LightWeightMap();
20. lightWeightMap.set('x', 123); // 增加一个键为'x'，值为123的元素
21. lightWeightMap.set('8', 356); // 增加一个键为'8'，值为356的元素
22. console.info(`result: ${lightWeightMap.get('a')}`); // 访问键为'a'的元素。输出：result: undefined
23. console.info(`result: ${lightWeightMap.get('x')}`); // 访问键为'x'的元素，获取其值。输出：result: 123
24. console.info(`result: ${lightWeightMap.getIndexOfKey('8')}`); // 访问键为'8'的元素，获取其索引。输出：result: 0

25. // PlainArray
26. import { PlainArray } from '@kit.ArkTS'; // 导入PlainArray模块

27. let plainArray: PlainArray<string> = new PlainArray();
28. plainArray.add(1, 'sdd'); // 增加一个键为1，值为'sdd'的元素
29. plainArray.add(2, 'sff'); // 增加一个键为2，值为'sff'的元素
30. console.info(`result: ${plainArray.get(1)}`); // 访问键为1的元素，获取值。输出：result: sdd
31. console.info(`result: ${plainArray.getKeyAt(1)}`); // 访问索引为1的元素，获取键。输出：result: 2
