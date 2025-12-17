
**HarmonyOS WebView**

今天分享一下 在鸿蒙中使用webview开发，相信前端开发的同学们都遇到过内嵌webview的情况，微信小程序在这方面不是特别友好，尤其是h5和小程序之间的交互，在鸿蒙中与小程序还是稍有不同的。

  

Web组件提供基础的前端页面加载的能力，包括加载网络页面、本地页面、html格式文本数据。

  

Web组件提供丰富的页面交互的方式，包括：设置前端页面深色模式，新窗口中加载页面，位置权限管理，Cookie管理，应用侧使用前端页面JavaScript等能力。

  

**注意：使用 webview 一定要去开启网络权限，否则页面将无法加载**

  

**1.创建一个简单的 webview 页面**

  

**1.1 app端 创建 webview 页面**

```
// 1. 引入依赖
```

**2.app端 输出 h5 的日志**

  

- 正常情况下我们开发会有很多日志输出，开发过webview的同学都知道，h5的日志不太好看，除非使用Vconsole插件
    
- 鸿蒙对这个情况做的比较好，可以直接在app端的日志输出h5的日志
    
- 使用webvivew属性 OnConsole 监听h5的console.log输出，并在控制台输出日志
    
      
    

```
Web({ src: '自己本地随便启动一个项目地址', controller: this.controller })
```

  

**3.h5 和 app端 方法调用（数据传递）**

  

- 方法1：在鸿蒙中 h5 和 app端的交互是通过 window 来进行的
    
- h5 把方法挂载到 window 对象上，app端 可以通过固定方法调用
    
- app端 也可以通过固定api 把方法挂载到 window 对象上让 h5 调用。
    
- 如果要做数据传递，在方法中加上**返参**或者**回调**即可
    
- 方法2：可以通过双向数据通道进行数据传递
    
- 实际上就是通过 postMessage
    

  

**3.1 app端 调用 h5 的方法**

  

**3.1.1 h5 挂载方法到 window 对象上**

```
// 在 h5 中，监听window.onload事件，挂载方法 testA 到 window 对象上
```

**3.1.2 app端 调用 h5 的方法**

```
// app端 创建一个按钮，通过按钮触发 h5 中的 testA 方法
```

**3.2 h5 调用 app端 的方法**

**3.2.1 app端 挂载方法到 window 对象上**

  

- app端 需要创建一个事件对象
    
- 通过固定api挂载到 window对象上
    
- 根据api可以分为两种方式
    

  

**3.2.1.1 创建事件对象**

```
// 通过 class 创建一个全局公共类，里面包含一个方法 testB
```

**3.2.1.2 使用 web 属性 javaScriptProxy 挂载方法到 window 对象上**

```
// app端
```

**3.2.1.3 使用 webview 控制器的方法 registerJavaScriptProxy 挂载方法到 window 对象上，使用此方法后必须调用 refresh，方法才能生效**

```
// app端
```

**3.2.1.4 使用 webview 控制器的方法 registerJavaScriptProxy 挂载方法到 window 对象上，可以在声明周期 onControllerAttached 上调用该方法，此时 h5 还未加载**

```
Web({ src: '自己本地随便启动一个项目地址', controller: this.controller })
```

**3.2.1.5 h5 调用方法，不管 app端 咋么调用，h5 都通过 window 对象来调用**

  

```
// h5
```

**### 3.3 建立 app端 和 h5 双向数据通道**

  

- 1.创建双向数据通道接口
    

- 使用的 API
    
- webview 控制器方法 createWebMessagePorts()
    
- 返回值:
    
- 是一个数组, 数组内有两个接口 [ 接口1, 接口2 ]
    
- [0] : 提供给 h5端 使用的, 需要传递给 h5端, h5端 使用这个接口去监听 App端 发来的消息, 同时也是使用这个接口向 App 端发送消息
    
- [1] : 提供给 App端 使用的, App端 使用这个接口去监听 h5端 发来的消息, 同时也是使用这个接口向 h5端 发送消息
    

  

- 2.把属于 h5端 的接口传递过去
    

- 注意: 此时不是 App端 和 h5端 建立好通道传递
    
- 而是先把建立通道的 "工具" 传递过去
    
- 所以, 此时是 App端 给 window 发送一个消息( 而不是和 h5端 建立通道连接 )
    

  

- 3.建立通道
    

- 使用 webview 控制器方法 postMessage 把 "接口工具" 发过去
    
- App端 和 h5端 都利用 "接口工具" 去建立双向连接通道
    

  

**3.3.1 创建创建双向数据通道接口，并完成事件监听**

  

- 双向通道数据接口通过 webview 控制器方法 createWebMessagePorts() 创建
    

  

```
// ---------- app端
```

**3.3.2 发送消息**

  

- 发送消息通过 通道 发送
    

  

```
// app端
```
如何在鸿蒙系统增加webview

在鸿蒙系统中增加WebView主要有以下几种方法，以下是具体步骤和示例：

**方法一：使用ArkTS原生开发**

1. **创建项目**  
    使用DevEco Studio创建一个新的鸿蒙项目，选择“Empty Ability”模板。
    
2. **引入依赖**  
    在代码中引入WebView相关模块：
    
    typescript
    
    ```typescript
    import webview from '@ohos.web.webview';
    ```
    
3. **创建WebView控制器**  
    在组件中声明并初始化WebView控制器：
    
    typescript
    
    ```typescript
    @component
    struct WebViewPage {
      controller: webview.webviewcontroller = new webview.webviewcontroller();
    }
    ```
    
4. **添加WebView组件**  
    在页面布局中使用`web`组件，并指定`src`属性加载网页地址，同时关联控制器：
    
    typescript
    
    ```typescript
    build() {
      column() {
        web({
          src: 'https://www.example.com', // 替换为实际网页地址
          controller: this.controller
        })
        .width('100%')
        .height('100%')
      }
    }
    ```
    
5. **配置权限**  
    在`config.json`文件中添加网络权限：
    
    json
    
    ```json
    {
      "module": {
        "reqPermissions": [
          {
            "name": "ohos.permission.INTERNET"
          }
        ]
      }
    }
    ```
    

**方法二：使用Flutter开发**

1. **添加依赖**  
    在`pubspec.yaml`文件中添加`flutter_inappwebview`插件：
    
    yaml
    
    ```yaml
    dependencies:
      flutter_inappwebview: ^5.5.0
    ```
    
2. **配置插件**  
    在`src/main/module.json5`中声明平台视图工厂：
    
    json
    
    ```json
    {
      "abilities": [
        {
          "name": "entryAbility",
          "srcEntry": "./ets/entryAbility/entryAbility.ets",
          "exported": true,
          "skills": []
        }
      ]
    }
    ```
    
3. **实现平台视图**  
    创建`customfactory.ets`和`customview.ets`文件，实现WebView的原生集成：
    
    typescript
    
    ```typescript
    // customfactory.ets
    import { PlatformViewFactory } from '@ohos/flutter_ohos';
    export class CustomFactory extends PlatformViewFactory {
      constructor() {
        super();
      }
      create(context: any, viewId: number, args: any): any {
        return new CustomView(context, viewId, args);
      }
    }
    
    // customview.ets
    import { WebView } from '@kit.arkweb';
    @component
    struct CustomView {
      controller: WebView.WebViewController = new WebView.WebViewController();
      build() {
        WebView({
          src: 'https://www.example.com',
          controller: this.controller
        })
        .width('100%')
        .height('100%');
      }
    }
    ```
    
4. **在Flutter代码中使用**  
    在Dart代码中通过`PlatformView`调用原生WebView：
    
    dart
    
    ```dart
    import 'package:flutter/material.dart';
    import 'package:flutter_inappwebview/flutter_inappwebview.dart';
    
    class WebViewPage extends StatefulWidget {
      @override
      _WebViewPageState createState() => _WebViewPageState();
    }
    
    class _WebViewPageState extends State<WebViewPage> {
      @override
      Widget build(BuildContext context) {
        return Scaffold(
          body: Container(
            child: PlatformViewLink(
              viewType: 'com.example.custom/WebView',
              onCreatePlatformView: (viewId) {
                return PlatformViewsService.initPlatformView(
                  viewId,
                  viewType: 'com.example.custom/WebView',
                  layoutDirection: TextDirection.ltr,
                  creationParams: const <String, dynamic>{},
                  creationParamsCodec: const StandardMessageCodec(),
                );
              },
            ),
          ),
        );
      }
    }
    ```
    

**方法三：加载本地HTML文件**

1. **放置文件**  
    将本地HTML文件放在项目目录的`resources/rawfile/`文件夹中。
    
2. **配置DataAbility**  
    在`config.json`中声明DataAbility：
    
    json
    
    ```json
    {
      "module": {
        "abilities": [
          {
            "name": "com.example.dataability",
            "type": "data",
            "uri": "dataability://com.example.dataability"
          }
        ]
      }
    }
    ```
    
3. **实现DataAbility**  
    创建`dataability.ets`文件，实现文件访问逻辑：
    
    typescript
    
    ```typescript
    import dataability from '@ohos.data.dataability';
    
    @dataability
    export class DataAbility extends dataability.DataAbility {
      openRawFile(uri: string, mode: string): any {
        const path = uri.split('/').pop();
        return this.resourceManager.getRawFileEntry(path).openRawFileDescriptor();
      }
    }
    ```
    
4. **加载本地文件**  
    在WebView中通过DataAbility URI加载本地文件：
    
    typescript
    
    ```typescript
    web({
      src: 'dataability://com.example.dataability/resources/rawfile/index.html',
      controller: this.controller
    })
    ```
    

以上方法可根据项目需求选择，ArkTS原生开发适合纯鸿蒙应用，Flutter开发适合跨平台项目，加载本地文件则适用于需要嵌入静态内容的场景。
# 初识ArkTS语言

更新时间: 2025-12-16 16:33

ArkTS是HarmonyOS应用的默认开发语言，在[TypeScript](https://www.typescriptlang.org/)（简称TS）生态基础上做了扩展，保持TS的基本风格。通过规范定义，从而强化了开发期的静态检查和分析，提升了程序执行的稳定性和性能。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163346.17954453256828335020446213095736:50001231000000:2800:B0247BBDBC59EE5DDC809A6C4FF54E3FB61DFDECB6C55AE15D6E11BD3040C47D.png)

深入学习请看[ArkTS学习路线](https://developer.huawei.com/consumer/cn/arkts/)和[ArkTS视频课程](https://developer.huawei.com/consumer/cn/training/course/slightMooc/C101717496870909384?pathId=101667550095504391)。

自API version 10起，ArkTS进一步通过规范强化静态检查和分析，其主要特性及标准TS的差异包括[从TypeScript到ArkTS的适配规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/typescript-to-arkts-migration-guide)：

- 强制使用静态类型：静态类型是ArkTS最重要的特性之一。如果使用静态类型，那么程序中变量的类型就是确定的。同时，由于所有类型在程序实际运行前都是已知的，编译器可以验证代码的正确性，从而减少运行时的类型检查，有助于性能提升。
    
- 禁止在运行时改变对象布局：为实现最优性能，ArkTS禁止在程序执行期间更改对象布局。
    
- 限制运算符语义：为获得更好的性能并鼓励编写清晰的代码，ArkTS限制了部分运算符的语义。例如，一元加法运算符仅能作用于数字，不能用于其他类型变量。
    
- 不支持Structural typing：对Structural typing的支持需要在语言、编译器和运行时进行大量的考虑和仔细的实现，当前ArkTS不支持该特性。根据实际场景的需求和反馈，后续会重新考虑是否支持Structural typing。
    

ArkTS兼容TS/JavaScript（简称JS）生态，开发者可以使用TS/JS进行开发或复用已有代码。HarmonyOS系统对TS/JS支持的详细情况见[兼容TS/JS的约束](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-migration-background#%E6%96%B9%E8%88%9F%E8%BF%90%E8%A1%8C%E6%97%B6%E5%85%BC%E5%AE%B9tsjs)。

未来，ArkTS会结合应用开发/运行的需求持续演进，逐步增强并行和并发能力、扩展系统类型，以及引入分布式开发范式等更多特性。

如需深入了解ArkTS语言，可参考[ArkTS具体指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-overview)。
# ArkTS语言介绍

更新时间: 2025-12-16 16:33

ArkTS是一种设计用于构建高性能应用的编程语言。它在继承TypeScript语法的基础上进行了优化，以提供更高的性能和开发效率。

许多编程语言在设计之初未考虑移动设备，导致应用运行缓慢、低效且功耗大。随着移动设备在日常生活中越来越普遍，针对移动环境的编程语言优化需求日益增加。ArkTS专为解决这些问题而设计，聚焦提高运行效率。

TypeScript是在JavaScript基础上通过添加类型定义扩展而来的，ArkTS则是TypeScript的进一步扩展。TypeScript提供了一种更结构化的JavaScript编码方法，深受开发者喜爱。ArkTS保持了TypeScript的大部分语法，旨在为现有的TypeScript开发者提供高度兼容的体验，帮助移动开发者快速上手。

ArkTS的一大特性是它专注于低运行时开销。ArkTS对TypeScript的动态类型特性施加了更严格的限制，以减少运行时开销，提高执行效率。通过取消动态类型特性，ArkTS代码能更有效地被运行前编译和优化，从而实现更快的应用启动和更低的功耗。

ArkTS语言设计中考虑了与TypeScript和JavaScript的互通性。许多移动应用开发者希望重用TypeScript和JavaScript代码及库，因此ArkTS提供与TypeScript和JavaScript的无缝互通，使开发者可以轻松集成TypeScript和JavaScript代码到应用中，充分利用现有代码和库进行ArkTS开发。

本教程将指导开发者了解ArkTS的核心功能、语法和最佳实践，助力开发者使用ArkTS高效构建高性能的移动应用。

如需详细了解ArkTS语言，请参阅[ArkTS具体指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-overview)和[DevEco Studio](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-tools-overview)。

## 基本知识

### 声明

ArkTS通过声明引入变量、常量、类型和函数。

**变量声明**

使用关键字let声明的变量可以在程序执行期间具有不同的值。

1. let hi: string = 'hello';
2. hi = 'hello, world';

**常量声明**

使用关键字const声明的常量为只读类型，只能被赋值一次。

1. const hello: string = 'hello';

对常量重新赋值会造成编译时错误。

**自动类型推断**

如果变量或常量的声明包含初始值，开发者无需显式指定类型，因为ArkTS规范已列举了所有允许自动推断类型的场景。

以下示例中，两条声明语句都是有效的，两个变量都是string类型：

1. let hi1: string = 'hello';
2. let hi2 = 'hello, world';

### 类型

**基本类型和引用类型**

基本数据类型包括number、string等简单类型，它们可以准确地表示单一的数据类型。对基本类型的存储和访问都是直接的，比较时直接比较其值。

引用类型包括对象、数组和函数等复杂数据结构。这些类型通过引用访问数据，对象和数组可以包含多个值或键值对，函数则可以封装可执行的代码逻辑。引用类型在内存中通过指针访问数据，修改引用会影响原始数据。

**number类型**

ArkTS提供number类型，任何整数和浮点数都可以被赋给此类型的变量。

数字字面量包括整数字面量和十进制浮点数字面量。

整数字面量包括以下类别：

- 十进制整数，由数字序列组成。例如：0、117、-345。
- 十六进制整数，以0x（或0X）开头，包含数字（0-9）和字母a-f或A-F。例如：0x1123、0x00111、-0xF1A7。
- 八进制整数，以0o（或0O）开头，只能包含数字（0-7）。例如：0o777。
- 二进制整数，以0b（或0B）开头，只能包含数字0和1。例如：0b11、0b0011、-0b11。

浮点数字面量包括以下部分：

- 十进制整数，可为有符号数（前缀为“+”或“-”）。
- 小数点（“.”）。
- 小数部分（由十进制数字字符串表示）。
- 指数部分，以“e”或“E”开头，后跟有符号（前缀为“+”或“-”）或无符号整数。

示例：

1. let n1 = 3.14;
2. let n2 = 3.141592;
3. let n3 = 0.5;
4. let n4 = 1e2;

5. function factorial(n: number): number {
6.   if (n <= 1) {
7.     return 1;
8.   }
9.   return n * factorial(n - 1);
10. }

11. factorial(n1)  //  7.660344000000002
12. factorial(n2)  //  7.680640444893748
13. factorial(n3)  //  1
14. factorial(n4)  //  9.33262154439441e+157

number类型在表示大整数（即超过-9007199254740991~9007199254740991）时会造成精度丢失。在开发时可以按需使用BigInt类型来确保精度：

1. let bigInt: BigInt = BigInt('999999999999999999999999999999999999999999999999999999999999');
2. console.info('bigInt:' + bigInt.toString());

**boolean类型**

boolean类型由true和false两个逻辑值组成。

通常在条件语句中使用boolean类型的变量：

1. let isDone: boolean = false;

2. // ...

3. if (isDone) {
4.   console.info('Done!');
5. }

**string类型**

string类型代表字符序列，可以使用转义字符来表示字符。

字符串字面量由单引号（'）或双引号（"）之间括起来的零个或多个字符组成。字符串字面量还有一特殊形式，是用反向单引号（`）括起来的模板字面量。

1. let s1 = 'Hello, world!\n';
2. let s2 = 'this is a string';
3. let a = 'Success';
4. let s3 = `The result is ${a}`;

**void类型**

void类型用于指定函数没有返回值。

此类型只有一个值，同样是void。由于void是引用类型，因此它可以用于泛型类型参数。

1. class Class<T> {
2.   //...
3. }
4. let instance: Class<void>;

**Object类型**

Object类型是所有引用类型的基类型。任何值，包括基本类型的值，都可以直接被赋给Object类型的变量（基本类型值会被自动装箱）。

object类型用于表示除基本类型外的类型。

1. let o1: Object = 'Alice';
2. let o2: Object = ['a', 'b'];
3. let o3: Object = 1;
4. let o4: object = [1, 2, 3];

**array类型**

array类型，即数组，是由可赋值给数组声明中指定的元素类型的数据组成的对象。

数组可由数组复合字面量赋值。数组复合字面量是用方括号括起来的零个或多个表达式列表，每个表达式为数组中的一个元素。数组的长度由数组中元素的个数确定。数组中第一个元素的索引为0。

以下示例将创建包含三个元素的数组：

1. let names: string[] = ['Alice', 'Bob', 'Carol'];

**enum类型**

enum类型，即枚举类型，是预先定义的一组命名值的值类型，其中命名值又称为枚举常量。

使用枚举常量时必须以枚举类型名称为前缀。

1. enum ColorSet { Red, Green, Blue }
2. let c: ColorSet = ColorSet.Red;

常量表达式用于显式设置枚举常量的值。

1. enum ColorSet { White = 0xFF, Grey = 0x7F, Black = 0x00 }
2. let c: ColorSet = ColorSet.Black;

**Union类型**

Union类型，即联合类型，是由多个类型组合成的引用类型。联合类型包含了变量可能的所有类型。

1. class Cat {
2.   name: string = 'cat';
3.   // ...
4. }
5. class Dog {
6.   name: string = 'dog';
7.   // ...
8. }
9. class Frog {
10.   name: string = 'frog';
11.   // ...
12. }
13. type Animal = Cat | Dog | Frog | number | string | null | undefined;
14. // Cat、Dog、Frog是一些类型（类或接口）

15. let animal: Animal = new Cat();
16. animal = new Frog();
17. animal = 42;
18. animal = 'dog';
19. animal = undefined;
20. // 可以将类型为联合类型的变量赋值为任何组成类型的有效值

可以使用不同机制获取联合类型中的特定类型值。

示例：

1. class Cat { sleep () {}; meow () {} }
2. class Dog { sleep () {}; bark () {} }
3. class Frog { sleep () {}; leap () {} }

4. type Animal = Cat | Dog | Frog;

5. function foo(animal: Animal) {
6.   if (animal instanceof Frog) {  // 判断animal是否是Frog类型
7.     animal.leap();  // animal在这里是Frog类型
8.   }
9.   animal.sleep(); // Animal具有sleep方法
10. }

**Aliases类型**

Aliases类型为匿名类型（如数组、函数、对象字面量或联合类型）提供名称，或为已定义的类型提供替代名称。

1. // 二维数组类型
2. type Matrix = number[][];
3. const gameBoard: Matrix = [
4.   [1, 0],
5.   [0, 1]
6. ];

7. // 函数类型
8. type Handler = (s: string, no: number) => string;
9. const repeatString: Handler = (str, times) => {
10.   return str.repeat(times);
11. };
12. console.info(repeatString('abc', 3)); // 'abcabcabc'

13. // 泛型函数类型
14. type Predicate<T> = (x: T) => boolean;
15. const isEven: Predicate<number> = (num) => num % 2 === 0;

16. // 可为空的对象类型
17. type NullableObject = Object | null;
18. class Cat {}
19. let animalData: NullableObject = new Cat();
20. let emptyData: NullableObject = null;

### 运算符

**赋值运算符**

赋值运算符=，使用方式如x=y。

复合赋值运算符将赋值与运算符组合在一起，例如：a += b 等价于 a = a + b，

其中的 += 即为复合赋值运算符

复合赋值运算符包括：+=、-=、*=、/=、%=、<<=、>>=、>>>=、&=、|=、^=。

**比较运算符**

|运算符|说明|
|:--|:--|
|===|如果两个操作数严格相等（对于不同类型的操作数认为是不相等的），则返回true。|
|!==|如果两个操作数严格不相等（对于不同类型的操作数认为是不相等的），则返回true。|
|==|如果两个操作数相等，则返回true。|
|!=|如果两个操作数不相等，则返回true。|
|>|如果左操作数大于右操作数，则返回true。|
|>=|如果左操作数大于或等于右操作数，则返回true。|
|<|如果左操作数小于右操作数，则返回true。|
|<=|如果左操作数小于或等于右操作数，则返回true。|

===与==的区别：

1. // ==只比较目标的值相等
2. console.info(String(null == undefined)); // true
3. // ===比较目标的值和类型都相等
4. console.info(String(null === undefined)); // false

**算术运算符**

一元运算符包括：-、+、--、++。

二元运算符列举如下：

|运算符|说明|
|:--|:--|
|+|加法|
|-|减法|
|*|乘法|
|/|除法|
|%|除法后余数|

**位运算符**

|运算符|说明|
|:--|:--|
|a & b|按位与：如果两个操作数的对应位都为1，则将这个位设置为1，否则设置为0。|
|a \| b|按位或：如果两个操作数的相应位中至少有一个为1，则将这个位设置为1，否则设置为0。|
|a ^ b|按位异或：如果两个操作数的对应位不同，则将这个位设置为1，否则设置为0。|
|~ a|按位非：反转操作数的位。|
|a << b|左移：将a的二进制表示向左移b位。|
|a >> b|算术右移：将a的二进制表示向右移b位，带符号扩展。|
|a >>> b|逻辑右移：将a的二进制表示向右移b位，左边补0。|

**逻辑运算符**

|运算符|说明|
|:--|:--|
|a && b|逻辑与|
|a \| b|逻辑或|
|! a|逻辑非|

**instanceof运算符**

instanceof运算符用于在运行时检查一个对象是否是指定类或其子类的实例。

示例如下：

1. obj instanceof className

返回值类型为boolean。

如果obj是className类或其子类的实例，则返回值为true；否则，返回值为false。

示例：

1. class Person {}
2. const person = new Person();
3. if ((person instanceof Person)) {
4.   console.info('true'); // true
5. }

6. class Animal {}
7. class Bird extends Animal {}
8. const bird = new Bird();
9. if (bird instanceof Animal) {
10.   console.info('true'); // true
11. }

### 语句

**if语句**

if语句用于需要根据逻辑条件执行不同语句的场景。当逻辑条件为真时，执行对应的一组语句，否则执行另一组语句（如果有的话）。

else部分也可以包含if语句。

if语句如下所示：

1. if (condition1) {
2.   // 语句1
3. } else if (condition2) {
4.   // 语句2
5. } else {
6.   // else语句
7. }

条件表达式可以是任何类型，非boolean类型会进行隐式类型转换：

1. let s1 = 'Hello';
2. if (s1) {
3.   console.info(s1); // 打印“Hello”
4. }

5. let s2 = 'World';
6. if (s2.length != 0) {
7.   console.info(s2); // 打印“World”
8. }

**switch语句**

使用switch语句执行与switch表达式值匹配的代码块。

switch语句如下所示：

1. switch (expression) {
2.   case label1: // 如果label1匹配，则执行
3.     // ...
4.     // 语句1
5.     // ...
6.     break; // 可省略
7.   case label2:
8.   case label3: // 如果label2或label3匹配，则执行
9.     // ...
10.     // 语句23
11.     // ...
12.     break; // 可省略
13.   default:
14.     // 默认语句
15. }

如果switch表达式的值等于某个label的值，则执行相应的语句。

如果没有任何一个label值与表达式值相匹配，并且switch具有default子句，那么程序会执行default子句对应的代码块。

break语句（可选的）允许跳出switch语句并继续执行switch语句之后的语句。

如果没有break语句，则执行switch中的下一个label对应的代码块。

**条件表达式**

条件表达式根据第一个表达式的布尔值来返回其他两个表达式之一的结果。

示例如下：

1. condition ? expression1 : expression2

如果condition的值为真值（转换后为true的值），则使用expression1作为该表达式的结果；否则，使用expression2作为该表达式的结果。

示例：

1. let message = Math.random() > 0.5 ? 'Valid' : 'Failed';

condition如果是非bool值则会进行隐式转换。

示例：

1.     console.info('a' ? 'true' : 'false'); // true
2.     console.info('' ? 'true' : 'false'); // false
3.     console.info(1 ? 'true' : 'false'); // true
4.     console.info(0 ? 'true' : 'false'); // false
5.     console.info(null ? 'true' : 'false'); // false
6.     console.info(undefined ? 'true' : 'false'); // false

**for语句**

for语句会被重复执行，直到循环退出语句值为false。

for语句如下所示：

1. for ([init]; [condition]; [update]) {
2.   statements
3. }

for语句的执行流程如下：

1、 执行init表达式（如有）。此表达式通常初始化一个或多个循环计数器。

2、 计算condition。如果它为真值（转换后为true的值），则执行循环主体的语句。如果它为假值（转换后为false的值），则for循环终止。

3、 执行循环主体的语句。

4、 如果有update表达式，则执行该表达式。

5、 返回步骤2。

示例：

1. let sum = 0;
2. for (let i = 0; i < 10; i += 2) {
3.   sum += i;
4. }

**for-of语句**

使用for-of语句可遍历数组、Set、Map、字符串等可迭代的类型。示例如下：

1. for (forVar of IterableExpression) {
2.   // process forVar
3. }

示例：

1. for (let ch of 'a string object') {
2.   console.info(ch);
3. }

**while语句**

只要condition为真值（转换后为true的值），while语句就会执行statements语句。示例如下：

1. while (condition) {
2.   statements
3. }

示例：

1. let n = 0;
2. let x = 0;
3. while (n < 3) {
4.   n++;
5.   x += n;
6. }

**do-while语句**

如果condition的值为真值（转换后为true的值），那么statements语句会重复执行。示例如下：

1. do {
2.   statements
3. } while (condition)

示例：

1. let i = 0;
2. do {
3.   i += 1;
4. } while (i < 10)

**break语句**

使用break语句可以终止循环语句或switch。

示例：

1. let x = 0;
2. while (true) {
3.   x++;
4.   if (x > 5) {
5.     break;
6.   }
7. }

如果break语句后带有标识符，则将控制流转移到该标识符所包含的语句块之外。

示例：

1. let x = 1;
2. label: while (true) {
3.   switch (x) {
4.     case 1:
5.       // statements
6.       break label; // 中断while语句
7.   }
8. }

**continue语句**

continue语句会停止当前循环迭代的执行，并将控制传递给下一次迭代。

示例：

1. let sum = 0;
2. for (let x = 0; x < 100; x++) {
3.   if (x % 2 == 0) {
4.     continue;
5.   }
6.   sum += x;
7. }

**throw和try语句**

throw语句用于抛出异常或错误：

1. throw new Error('this error')

try语句用于捕获和处理异常或错误：

1. try {
2.   // 可能发生异常的语句块
3. } catch (e) {
4.   // 异常处理
5. }

下面的示例中throw和try语句用于处理除数为0的错误：

1. class ZeroDivisor extends Error {}

2. function divide (a: number, b: number): number {
3.   if (b == 0) {
4.     throw new ZeroDivisor();
5.   }
6.   return a / b;
7. }

8. function process (a: number, b: number) {
9.   try {
10.     let res = divide(a, b);
11.     console.info('result: ' + res);
12.   } catch (x) {
13.     console.error('some error');
14.   }
15. }

支持finally语句：

1. function processData(s: string) {
2.   let error: Error | null = null;

3.   try {
4.     console.info('Data processed: ' + s);
5.     // ...
6.     // 可能发生异常的语句
7.     // ...
8.   } catch (e) {
9.     error = e as Error;
10.     // ...
11.     // 异常处理
12.     // ...
13.   } finally {
14.     // 无论是否发生异常都会执行的代码
15.     if (error != null) {
16.       console.error(`Error caught: input='${s}', message='${error.message}'`);
17.     }
18.   }
19. }

## 函数

### 函数声明

函数声明引入一个函数，包含其名称、参数列表、返回类型和函数体。

以下示例是一个简单的函数和它的语法语义说明：

1.参数类型标注：x: string, y: string 显式声明参数类型为字符串类型。

2.返回值类型：: string 指定函数返回值为字符串类型。

1. function add(x: string, y: string): string {
2.   let z: string = `${x} ${y}`;
3.   return z;
4. }

在函数声明中，必须为每个参数标记类型。如果参数为可选参数，那么允许在调用函数时省略该参数。函数的最后一个参数可以是rest参数。

### 可选参数

可选参数的格式可为name?: Type。

1. function hello(name?: string) {
2.   if (name == undefined) {
3.     console.info('Hello!');
4.   } else {
5.     console.info(`Hello, ${name}!`);
6.   }
7. }

可选参数的另一种形式为设置的参数默认值。如果在函数调用中这个参数被省略了，则会使用此参数的默认值作为实参。

1. function multiply(n: number, coeff: number = 2): number {
2.   return n * coeff;
3. }
4. multiply(2);  // 返回2*2
5. multiply(2, 3); // 返回2*3

### rest参数

函数的最后一个参数可以是rest参数，格式为...restName: Type[]。rest参数允许函数接收一个不定长数组，用于处理不定数量的参数输入。

1. function sum(...numbers: number[]): number {
2.   let res = 0;
3.   for (let n of numbers) {
4.     res += n;
5.   }
6.   return res;
7. }

8. sum(); // 返回0
9. sum(1, 2, 3); // 返回6

### 返回类型

如果可以从函数体内推断出函数返回类型，则可在函数声明中省略标注返回类型。

1. // 显式指定返回类型
2. function foo(): string { return 'foo'; }

3. // 推断返回类型为string
4. function goo() { return 'goo'; }

不需要返回值的函数的返回类型可以显式指定为void或省略标注。这类函数不需要返回语句。

以下示例中两种函数声明方式都是有效的：

1. function hi1() { console.info('hi'); }
2. function hi2(): void { console.info('hi'); }

### 函数的作用域

函数中定义的变量和其他实例仅可以在函数内部访问，不能从外部访问。

如果函数中定义的变量与外部作用域中已有实例同名，则函数内的局部变量定义将覆盖外部定义。

1. let outerVar = 'I am outer ';

2. function func() {
3.     let outerVar = 'I am inside';
4.     console.info(outerVar); // 输出: I am inside
5. }

6. func();

### 函数调用

调用函数以执行其函数体，实参值会赋值给函数的形参。

如果函数定义如下：

1. function join(x: string, y: string): string {
2.   let z: string = `${x} ${y}`;
3.   return z;
4. }

则此函数的调用需要包含两个string类型的参数：

1. let x = join('hello', 'world');
2. console.info(x); // 输出: hello world

### 函数类型

函数类型通常用于定义回调函数：

1. type trigFunc = (x: number) => number // 这是一个函数类型

2. function do_action(f: trigFunc) {
3.   f(3.141592653589); // 调用函数
4. }

5. do_action(Math.sin); // 将函数作为参数传入

### 箭头函数（又名Lambda函数）

函数可以定义为箭头函数，例如：

1. let sum = (x: number, y: number): number => {
2.   return x + y;
3. }

箭头函数的返回类型可以省略，此时返回类型从函数体推断。

表达式可以指定为箭头函数，使表达更简短，因此以下两种表达方式是等价的：

1. let sum1 = (x: number, y: number) => { return x + y; }
2. let sum2 = (x: number, y: number) => x + y

### 闭包

闭包是由函数及声明该函数的环境组合而成的。该环境包含了这个闭包创建时作用域内的任何局部变量。

在下例中，f函数返回了一个闭包，它捕获了count变量，每次调用z，count的值会被保留并递增。

1. function f(): () => number {
2.   let count = 0;
3.   let g = (): number => { count++; return count; };
4.   return g;
5. }

6. let z = f();
7. z(); // 返回：1
8. z(); // 返回：2

### 函数重载

可以通过编写重载，指定函数的不同调用方式。具体方法是，为同一个函数写入多个同名但签名不同的函数头，函数实现紧随其后。

1. function foo(x: number): void;            /* 第一个函数定义 */
2. function foo(x: string): void;            /* 第二个函数定义 */
3. function foo(x: number | string): void {  /* 函数实现 */
4. }

5. foo(123);     //  OK，使用第一个定义
6. foo('aa'); // OK，使用第二个定义

不允许重载函数有相同的名字和参数列表，否则将导致编译错误。

## 类

类声明引入一个新类型，并定义其字段、方法和构造函数。

在以下示例中，定义了Person类，该类具有字段name和surname、构造函数和方法fullName：

1. class Person {
2.   name: string = '';
3.   surname: string = '';
4.   constructor (n: string, sn: string) {
5.     this.name = n;
6.     this.surname = sn;
7.   }
8.   fullName(): string {
9.     return this.name + ' ' + this.surname;
10.   }
11. }

定义类后，可以使用关键字new创建实例：

1. let p = new Person('John', 'Smith');
2. console.info(p.fullName());

或者，可以使用对象字面量创建实例：

1. class Point {
2.   x: number = 0;
3.   y: number = 0;
4. }
5. let p: Point = {x: 42, y: 42};

### 字段

字段是直接在类中声明的某种类型的变量。

类可以具有实例字段或者静态字段。

**实例字段**

实例字段存在于类的每个实例上。每个实例都有自己的实例字段集合。

要访问实例字段，需要使用类的实例。

1. class Person {
2.   name: string = '';
3.   age: number = 0;
4.   constructor(n: string, a: number) {
5.     this.name = n;
6.     this.age = a;
7.   }

8.   getName(): string {
9.     return this.name;
10.   }
11. }

12. let p1 = new Person('Alice', 25);
13. p1.name; // Alice
14. let p2 = new Person('Bob', 28);
15. p2.getName(); // Bob

**静态字段**

使用关键字static将字段声明为静态。静态字段属于类本身，类的所有实例共享一个静态字段。

要访问静态字段，需要使用类名：

1. class Person {
2.   static numberOfPersons = 0;
3.   constructor() {
4.      // ...
5.      Person.numberOfPersons++;
6.      // ...
7.   }
8. }

9. Person.numberOfPersons;

**字段初始化**

为了减少运行时错误并提升执行性能，

ArkTS要求所有字段在声明时或构造函数中显式初始化，与标准TS的strictPropertyInitialization模式相同。

以下代码在ArkTS中不合法。

1. class Person {
2.   name: string; // undefined

3.   setName(n: string): void {
4.     this.name = n;
5.   }

6.   getName(): string {
7.     // 开发者使用"string"作为返回类型，这隐藏了name可能为"undefined"的事实。
8.     // 更合适的做法是将返回类型标注为"string | undefined"，以告诉开发者这个API所有可能的返回值。
9.     return this.name;
10.   }
11. }

12. let jack = new Person();
13. // 假设代码中没有对name赋值，即没有调用"jack.setName('Jack')"
14. jack.getName().length; // 运行时异常：name is undefined

在ArkTS中，开发者应该这样写代码。

1. class Person {
2.   name: string = '';

3.   setName(n: string): void {
4.     this.name = n;
5.   }

6.   // 类型为'string'，不可能为"null"或者"undefined"
7.   getName(): string {
8.     return this.name;
9.   }
10. }

11. let jack = new Person();
12. // 假设代码中没有对name赋值，即没有调用"jack.setName('Jack')"
13. jack.getName().length; // 0, 没有运行时异常

接下来的代码示例展示了当name的值可能为undefined时，如何正确编写代码。

1. class Person {
2.   name?: string; // 可能为`undefined`

3.   setName(n: string): void {
4.     this.name = n;
5.   }

6.   // 编译时错误：name可以是"undefined"，所以这个API的返回值类型不能仅定义为string类型
7.   getNameWrong(): string {
8.     return this.name;
9.   }

10.   getName(): string | undefined { // 返回类型匹配name的类型
11.     return this.name;
12.   }
13. }

14. let jack = new Person();
15. // 假设代码中没有对name赋值，即没有调用"jack.setName('Jack')"

16. // 编译时错误：编译器认为下一行代码有可能会访问undefined的属性，报错
17. jack.getName().length;  // 编译失败

18. jack.getName()?.length; // 编译成功，没有运行时错误

**getter和setter**

setter和getter可用于提供对类属性的受控访问。

在以下示例中，setter用于禁止将_age属性设置为无效值：

1. class Person {
2.   name: string = '';
3.   private _age: number = 0;
4.   get age(): number { return this._age; }
5.   set age(x: number) {
6.     if (x < 0) {
7.       throw Error('Invalid age argument');
8.     }
9.     this._age = x;
10.   }
11. }

12. let p = new Person();
13. p.age; // 输出0
14. p.age = -42; // 设置无效age值会抛出错误

在类中可以定义getter或者setter。

### 方法

方法属于类。类可以定义实例方法或者静态方法。静态方法属于类本身，只能访问静态字段。而实例方法既可以访问静态字段，也可以访问实例字段，包括类的私有字段。

**实例方法**

以下示例说明了实例方法的工作原理。

calculateArea方法计算矩形面积：

1. class RectangleSize {
2.   private height: number = 0;
3.   private width: number = 0;
4.   constructor(height: number, width: number) {
5.     this.height = height;
6.     this.width = width;
7.   }
8.   calculateArea(): number {
9.     return this.height * this.width;
10.   }
11. }

必须通过类的实例调用实例方法：

1. let square = new RectangleSize(10, 10);
2. square.calculateArea(); // 输出：100

**静态方法**

使用关键字 static 声明静态方法。静态方法属于类，只能访问静态字段。

静态方法定义了类作为一个整体的公共行为。

必须通过类名调用静态方法：

1. class Cl {
2.   static staticMethod(): string {
3.     return 'this is a static method.';
4.   }
5. }
6. console.info(Cl.staticMethod());

**继承**

一个类可以继承另一个类（称为基类），并使用以下语法实现多个接口：

1. class [extends BaseClassName] [implements listOfInterfaces] {
2.   // ...
3. }

继承类继承基类的字段和方法，但不继承构造函数。继承类可以新增定义字段和方法，也可以覆盖其基类定义的方法。

基类也称为“父类”或“超类”。继承类也称为“派生类”或“子类”。

示例：

1. class Person {
2.   name: string = '';
3.   private _age = 0;
4.   get age(): number {
5.     return this._age;
6.   }
7. }
8. class Employee extends Person {
9.   salary: number = 0;
10.   calculateTaxes(): number {
11.     return this.salary * 0.42;
12.   }
13. }

包含implements子句的类必须实现列出的接口中定义的所有方法，但使用默认实现定义的方法除外。

1. interface DateInterface {
2.   now(): string;
3. }
4. class MyDate implements DateInterface {
5.   now(): string {
6.     // 在此实现
7.     return 'now';
8.   }
9. }

**父类访问**

关键字super可用于访问父类的方法和构造函数。在实现子类功能时，可以通过该关键字从父类中获取所需接口：

1. class RectangleSize {
2.   protected height: number = 0;
3.   protected width: number = 0;

4.   constructor (h: number, w: number) {
5.     this.height = h;
6.     this.width = w;
7.   }

8.   draw() {
9.     /* 绘制边界 */
10.   }
11. }
12. class FilledRectangle extends RectangleSize {
13.   color = ''
14.   constructor (h: number, w: number, c: string) {
15.     super(h, w); // 父类构造函数的调用
16.     this.color = c;
17.   }

18.   draw() {
19.     super.draw(); // 父类方法的调用
20.     /* 填充矩形 */
21.   }
22. }

**方法重写**

子类可以重写其父类中定义的方法的实现。重写的方法必须具有与原始方法相同的参数类型和相同或派生的返回类型。

1. class RectangleSize {
2.   // ...
3.   area(): number {
4.     // 实现
5.     return 0;
6.   }
7. }
8. class Square extends RectangleSize {
9.   private side: number = 0;
10.   area(): number {
11.     return this.side * this.side;
12.   }
13. }

**方法重载签名**

通过重载签名，指定方法的不同调用。具体方法为，为同一个方法写入多个同名但签名不同的方法头，方法实现紧随其后。

1. class C {
2.   foo(x: number): void;            /* 第一个签名 */
3.   foo(x: string): void;            /* 第二个签名 */
4.   foo(x: number | string): void {  /* 实现签名 */
5.   }
6. }
7. let c = new C();
8. c.foo(123);     // OK，使用第一个签名
9. c.foo('aa'); // OK，使用第二个签名

如果两个重载签名的名称和参数列表均相同，则为错误。

### 构造函数

类声明可以包含用于初始化对象状态的构造函数。

构造函数定义如下：

1. constructor ([parameters]) {
2.   // ...
3. }

如果未定义构造函数，则会自动创建具有空参数列表的默认构造函数，例如：

1. class Point {
2.   x: number = 0;
3.   y: number = 0;
4. }
5. let p = new Point();

在这种情况下，默认构造函数使用字段类型的默认值初始化实例中的字段。

**派生类的构造函数**

构造函数函数体的第一条语句可以使用关键字super来显式调用直接父类的构造函数。

1. class RectangleSize {
2.   constructor(width: number, height: number) {
3.     // ...
4.   }
5. }
6. class Square extends RectangleSize {
7.   constructor(side: number) {
8.     super(side, side);
9.   }
10. }

**构造函数重载签名**

可以通过编写重载签名，指定构造函数的不同调用方式。具体方法是，为同一个构造函数写入多个同名但签名不同的构造函数头，构造函数实现紧随其后。

1. class C {
2.   constructor(x: number)             /* 第一个签名 */
3.   constructor(x: string)             /* 第二个签名 */
4.   constructor(x: number | string) {  /* 实现签名 */
5.   }
6. }
7. let c1 = new C(123);      // OK，使用第一个签名
8. let c2 = new C('abc');    // OK，使用第二个签名

如果两个重载签名的名称和参数列表均相同，则为错误。

### 可见性修饰符

类的方法和属性都可以使用可见性修饰符。

可见性修饰符包括：private、protected和public。默认可见性为public。

**Public（公有）**

public修饰的类成员（字段、方法、构造函数）在程序的任何可访问该类的地方都是可见的。

**Private（私有）**

private修饰的成员不能在声明该成员的类之外访问，例如：

1. class C {
2.   public x: string = '';
3.   private y: string = '';
4.   set_y (new_y: string) {
5.     this.y = new_y; // OK，因为y在类本身中可以访问
6.   }
7. }
8. let c = new C();
9. c.x = 'a'; // OK，该字段是公有的
10. c.y = 'b'; // 编译时错误：'y'不可见

**Protected（受保护）**

protected修饰符的作用与private修饰符非常相似，不同点是protected修饰的成员允许在派生类中访问，例如：

1. class Base {
2.   protected x: string = '';
3.   private y: string = '';
4. }
5. class Derived extends Base {
6.   foo() {
7.     this.x = 'a'; // OK，访问受保护成员
8.     this.y = 'b'; // 编译时错误，'y'不可见，因为它是私有的
9.   }
10. }

### 对象字面量

对象字面量是一个表达式，可用于创建类实例并提供一些初始值。它在某些情况下更方便，可以用来代替new表达式。

对象字面量的表示方式是：封闭在花括号对({})中的'属性名：值'的列表。

1. class C {
2.   n: number = 0;
3.   s: string = '';
4. }

5. let c: C = {n: 42, s: 'foo'};

ArkTS是静态类型语言，如上述示例所示，对象字面量只能在可以推导出该字面量类型的上下文中使用。其他正确的例子如下所示：

1. class C {
2.   n: number = 0;
3.   s: string = '';
4. }

5. function foo(c: C) {}

6. let c: C

7. c = {n: 42, s: 'foo'};  // 使用变量的类型
8. foo({n: 42, s: 'foo'}); // 使用参数的类型

9. function bar(): C {
10.   return {n: 42, s: 'foo'}; // 使用返回类型
11. }

也可以在数组元素类型或类字段类型中使用：

1. class C {
2.   n: number = 0;
3.   s: string = '';
4. }
5. let cc: C[] = [{n: 1, s: 'a'}, {n: 2, s: 'b'}];

**Record类型的对象字面量**

泛型Record<K, V>用于将类型（键类型）的属性映射到另一个类型（值类型）。常用对象字面量来初始化该类型的值：

1. let map: Record<string, number> = {
2.   'John': 25,
3.   'Mary': 21
4. };

5. map['John']; // 25

类型K可以是字符串类型或数值类型(不包括BigInt)，而V可以是任何类型。

1. interface PersonInfo {
2.   age: number;
3.   salary: number;
4. }
5. let map: Record<string, PersonInfo> = {
6.   'John': { age: 25, salary: 10},
7.   'Mary': { age: 21, salary: 20}
8. }

### 抽象类

带有abstract修饰符的类称为抽象类。抽象类可用于表示一组更具体的概念所共有的概念。

尝试创建抽象类的实例会导致编译错误：

1. abstract class X {
2.   field: number;
3.   constructor(p: number) {
4.     this.field = p;
5.   }
6. }

7. let x = new X(666)  //编译时错误：不能创建抽象类的具体实例

抽象类的子类可以是抽象类也可以是非抽象类。抽象父类的非抽象子类可以实例化。因此，执行抽象类的构造函数和该类非静态字段的字段初始化器：

1. abstract class Base {
2.   field: number;
3.   constructor(p: number) {
4.     this.field = p;
5.   }
6. }

7. class Derived extends Base {
8.   constructor(p: number) {
9.     super(p);
10.   }
11. }

12. let x = new Derived(666);

**抽象方法**

带有abstract修饰符的方法称为抽象方法，抽象方法可以被声明但不能被实现。

只有抽象类内才能有抽象方法，如果非抽象类具有抽象方法，则会发生编译时错误：

1. class Y {
2.   abstract method(p: string)  //编译时错误：抽象方法只能在抽象类内。
3. }

## 接口

接口声明引入新类型。接口是定义代码协定的常见方式。

任何类的实例，只要实现了特定接口，即可通过该接口实现多态。

接口通常包含属性和方法的声明。

示例：

1. interface Style {
2.   color: string; // 属性
3. }
4. interface AreaSize {
5.   calculateAreaSize(): number; // 方法的声明
6.   someMethod(): void;     // 方法的声明
7. }

实现接口的类示例：

1. // 接口：
2. interface AreaSize {
3.   calculateAreaSize(): number; // 方法的声明
4.   someMethod(): void;     // 方法的声明
5. }

6. // 实现：
7. class RectangleSize implements AreaSize {
8.   private width: number = 0;
9.   private height: number = 0;
10.   someMethod(): void {
11.     console.info('someMethod called');
12.   }
13.   calculateAreaSize(): number {
14.     this.someMethod(); // 调用另一个方法并返回结果
15.     return this.width * this.height;
16.   }
17. }

### 接口属性

接口属性可以是字段、getter、setter或getter和setter组合的形式。

属性字段只是getter/setter对的便捷写法。以下表达方式是等价的：

1. interface Style {
2.   color: string;
3. }

4. interface Style {
5.   get color(): string;
6.   set color(x: string);
7. }

实现接口的类也可以使用以下两种方式：

1. interface Style {
2.   color: string;
3. }

4. class StyledRectangle implements Style {
5.   color: string = '';
6. }

7. interface Style {
8.   color: string;
9. }

10. class StyledRectangle implements Style {
11.   private _color: string = '';
12.   get color(): string { return this._color; }
13.   set color(x: string) { this._color = x; }
14. }

### 接口继承

接口可以继承其他接口，示例如下：

1. interface Style {
2.   color: string;
3. }

4. interface ExtendedStyle extends Style {
5.   width: number;
6. }

继承接口包含被继承接口的所有属性和方法，还可以添加自己的属性和方法。

### 抽象类和接口

抽象类与接口都无法实例化。抽象类是类的抽象，抽象类用来捕捉子类的通用特性，接口是行为的抽象。在ArkTS语法中抽象类与接口的区别如下：

- 一个类只能继承一个抽象类，而一个类可以实现一个或多个接口；

1. // Bird类继承Animal抽象类并实现多个接口CanFly、CanSwim
2. class Bird extends Animal implements CanFly, CanSwim {
3.   // ...
4. }

- 接口中不能含有静态代码块以及静态方法，而抽象类可以有静态代码块和静态方法；

1. interface MyInterface {
2.     // 错误：接口中不能包含静态成员
3.     static staticMethod(): void;

4.     // 错误：接口中不能包含静态代码块
5.     static { console.info('static'); };
6. }

7. abstract class MyAbstractClass {
8.     // 正确：抽象类可以有静态方法
9.     static staticMethod(): void { console.info('static'); }

10.     // 正确：抽象类可以有静态代码块
11.     static { console.info('static initialization block'); }
12. }

- 抽象类里面可以有方法的实现，但是接口没有方法的实现，是完全抽象的；

1. abstract class MyAbstractClass {
2.    // 正确：抽象类里面可以有方法的实现
3.    func(): void { console.info('func'); }
4. }
5. interface MyInterface {
6.    // 错误：接口没有方法的实现，是完全抽象的
7.    func(): void { console.info('func'); }
8. }

- 抽象类可以有构造函数，而接口不能有构造函数。

1. abstract class MyAbstractClass {
2.   constructor(){}  // 正确：抽象类可以有构造函数
3. }
4. interface MyInterface {
5.   constructor(); // 错误：接口中不能有构造函数
6. }

## 泛型类型和函数

泛型类型和函数使代码能够以类型安全的方式操作多种数据类型，而无需为每种类型编写重复的逻辑。

### 泛型类和接口

类和接口可以定义为泛型，将参数添加到类型定义中。如以下示例中的类型参数Element：

1. class CustomStack<Element> {
2.   public push(e: Element):void {
3.     // ...
4.   }
5. }

要使用类型CustomStack，必须为每个类型参数指定类型实参：

1. let s = new CustomStack<string>();
2. s.push('hello');

编译器在使用泛型类型和函数时会确保类型安全。参见以下示例：

1. let s = new CustomStack<string>();
2. s.push(55); // 将会产生编译时错误

### 泛型约束

泛型类型的类型参数可以被限制只能取某些特定的值。例如，MyHashMap<Key, Value>这个类中的Key类型参数必须具有hash方法。

1. interface Hashable {
2.   hash(): number;
3. }
4. class MyHashMap<Key extends Hashable, Value> {
5.   public set(k: Key, v: Value) {
6.     let h = k.hash();
7.     // ...其他代码...
8.   }
9. }

在上面的例子中，Key类型扩展了Hashable，Hashable接口的所有方法都可以为key调用。

### 泛型函数

使用泛型函数可编写更通用的代码。比如返回数组最后一个元素的函数：

1. function last(x: number[]): number {
2.   return x[x.length - 1];
3. }
4. last([1, 2, 3]); // 3

如果需要为任何数组定义相同的函数，使用类型参数将该函数定义为泛型：

1. function last<T>(x: T[]): T {
2.   return x[x.length - 1];
3. }

现在，该函数可以与任何数组一起使用。

在函数调用中，类型实参可以显式或隐式设置：

1. // 显式设置的类型实参
2. let res1: string = last<string>(['aa', 'bb']);
3. let res2: number = last<number>([1, 2, 3]);

4. // 隐式设置的类型实参
5. // 编译器根据调用参数的类型来确定类型实参
6. let res3: number = last([1, 2, 3]);

### 泛型默认值

泛型类型的类型参数可以设置默认值，这样无需指定实际类型实参，直接使用泛型类型名称即可。以下示例展示了类和函数的这一特性。

1. class SomeType {}
2. interface Interface <T1 = SomeType> { }
3. class Base <T2 = SomeType> { }
4. class Derived1 extends Base implements Interface { }
5. // Derived1在语义上等价于Derived2
6. class Derived2 extends Base<SomeType> implements Interface<SomeType> { }

7. function foo<T = number>(): void {
8.   // ...
9. }
10. foo();
11. // 此函数在语义上等价于下面的调用
12. foo<number>();

## 空安全

默认情况下，ArkTS中的所有类型都不允许为空，这类似于TypeScript的(strictNullChecks)模式，但规则更严格。

在下面的示例中，所有行都会导致编译时错误：

1. let x: number = null;    // 编译时错误
2. let y: string = null;    // 编译时错误
3. let z: number[] = null;  // 编译时错误

可以为空值的变量定义为联合类型T | null。

1. let x: number | null = null;
2. x = 1;    // ok
3. x = null; // ok
4. if (x != null) { /* do something */ }

### 非空断言运算符

后缀运算符!可用于断言其操作数为非空。

当应用于可空类型的值时，编译时类型会变为非空类型。例如，类型从T | null变为T：

1. class A {
2.   value: number = 0;
3. }

4. function foo(a: A | null) {
5.   a.value;   // 编译时错误：无法访问可空值的属性
6.   a!.value;  // 编译通过，如果运行时a的值非空，可以访问到a的属性；如果运行时a的值为空，则发生运行时异常
7. }

### 空值合并运算符

空值合并二元运算符??用于检查左侧表达式的求值是否等于null或者undefined。如果是，则表达式的结果为右侧表达式；否则，结果为左侧表达式。

换句话说，a ?? b等价于三元运算符(a != null && a != undefined) ? a : b。

在以下示例中，getNick方法返回已设置的昵称。如果未设置，则返回空字符串。

1. class Person {
2.   // ...
3.   nick: string | null = null;
4.   getNick(): string {
5.     return this.nick ?? '';
6.   }
7. }

### 可选链

访问对象属性时，如果属性是undefined或null，可选链运算符返回undefined。

1. class Person {
2.   nick: string | null = null;
3.   spouse?: Person

4.   setSpouse(spouse: Person): void {
5.     this.spouse = spouse;
6.   }

7.   getSpouseNick(): string | null | undefined {
8.     return this.spouse?.nick;
9.   }

10.   constructor(nick: string) {
11.     this.nick = nick;
12.     this.spouse = undefined;
13.   }
14. }

**说明**：getSpouseNick的返回类型必须为string | null | undefined，因为该方法在某些情况下会返回null或undefined。

可选链可以任意长，可以包含任意数量的?.运算符。

在以下示例中，如果Person实例的spouse属性不为空，并且spouse的nick属性也不为空时，输出spouse.nick。否则，输出undefined。

1. class Person {
2.   nick: string | null = null;
3.   spouse?: Person;

4.   constructor(nick: string) {
5.     this.nick = nick;
6.     this.spouse = undefined;
7.   }
8. }

9. let p: Person = new Person('Alice');
10. p.spouse?.nick; // undefined

## 模块

程序可划分为多组编译单元或模块。

每个模块都有其自己的作用域，即在模块中创建的任何声明（变量、函数、类等）在该模块之外都不可见，除非它们被显式导出。

与此相对，必须首先将另一个模块导出的变量、函数、类、接口等导入到当前模块中。

### 导出

可以使用关键字export导出顶层的声明。

未导出的声明名称被视为私有名称，只能在声明该名称的模块中使用。

1. export class Point {
2.   x: number = 0;
3.   y: number = 0;
4.   constructor(x: number, y: number) {
5.     this.x = x;
6.     this.y = y;
7.   }
8. }
9. export let Origin = new Point(0, 0);
10. export function Distance(p1: Point, p2: Point): number {
11.   return Math.sqrt((p2.x - p1.x) * (p2.x - p1.x) + (p2.y - p1.y) * (p2.y - p1.y));
12. }

**导出默认导出的对象**

1. class Demo{
2.   constructor(){
3.   }
4. }
5. export default new Demo();

### 导入

**静态导入**

导入声明用于导入从其他模块导出的实体，并在当前模块中提供其绑定。导入声明由两部分组成：

- 导入路径，用于指定导入的模块；
- 导入绑定，用于定义导入的模块中的可用实体集和使用形式（限定或不限定使用）。

导入绑定可以有几种形式。

假设模块的路径为“./utils”，并且导出了实体“X”和“Y”。

导入绑定* as A表示绑定名称“A”，通过A.name可访问从导入路径指定的模块导出的所有实体：

1. import * as Utils from './utils';
2. Utils.X // 表示来自Utils的X
3. Utils.Y // 表示来自Utils的Y

导入绑定{ ident1, ..., identN }表示将导出的实体与指定名称绑定，该名称可以用作简单名称：

1. import { X, Y } from './utils';
2. X // 表示来自utils的X
3. Y // 表示来自utils的Y

如果标识符列表定义了ident as alias，则实体ident将绑定在名称alias下：

1. import { X as Z, Y } from './utils';
2. Z // 表示来自Utils的X
3. Y // 表示来自Utils的Y
4. X // 编译时错误：'X'不可见

**动态导入**

在应用开发的有些场景中，如果希望根据条件导入模块或者按需导入模块，可以使用动态导入代替静态导入。

import()语法被称为动态导入（dynamic import），是一种类似函数的表达式，用于动态导入模块。调用这种方式，会返回一个promise。

如下例所示，import(modulePath)可以加载模块并返回一个promise，该promise resolve为一个包含其所有导出的模块对象。该表达式可以在代码中的任意位置调用。

1. // Calc.ts
2. export function add(a:number, b:number):number {
3.   let c = a + b;
4.   console.info('Dynamic import, %d + %d = %d', a, b, c);
5.   return c;
6. }

7. // Index.ets
8. import('./Calc').then((obj: ESObject) => {
9.   console.info(obj.add(3, 5));
10. }).catch((err: Error) => {
11.   console.error('Module dynamic import error: ', err);
12. });

如果在异步函数中，可以使用let module = await import(modulePath)。

1. // say.ts
2. export function hi() {
3.   console.info('Hello');
4. }
5. export function bye() {
6.   console.info('Bye');
7. }

那么，可以像下面这样进行动态导入：

1. async function test() {
2.   let ns = await import('./say');
3.   let hi = ns.hi;
4.   let bye = ns.bye;
5.   hi();
6.   bye();
7. }

更多的使用动态import的业务场景和使用实例见[动态import](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-dynamic-import)。

**导入HarmonyOS SDK的开放能力**

HarmonyOS SDK提供的开放能力（接口）也需要在导入声明后使用。可直接导入接口模块来使用该模块内的所有接口能力，例如：

1. import UIAbility from '@ohos.app.ability.UIAbility';

从HarmonyOS NEXT Developer Preview 1版本开始引入Kit概念。SDK对同一个Kit下的接口模块进行了封装，开发者在示例代码中可通过导入Kit的方式来使用Kit所包含的接口能力。其中，Kit封装的接口模块可查看SDK目录下Kit子目录中各Kit的定义。在代码开发中，推荐通过导入Kit方式使用开放能力。

通过导入Kit方式使用开放能力有三种方式：

- 方式一：导入Kit下单个模块的接口能力。例如：
    
    1. import { UIAbility } from '@kit.AbilityKit';
    
- 方式二：导入Kit下多个模块的接口能力。例如：
    
    1. import { UIAbility, Ability, Context } from '@kit.AbilityKit';
    
- 方式三：导入Kit包含的所有模块的接口能力。例如：
    
    1. import * as module from '@kit.AbilityKit';
    
    其中，“module”为别名，可自定义，然后通过该名称调用模块的接口。
    
    说明
    
    方式三可能会导入过多无需使用的模块，导致编译后的HAP包太大，占用过多资源，请谨慎使用。
    

### 顶层语句

顶层语句是指在模块最外层编写的语句，不被任何函数、类或块级作用域包裹。这些语句包括变量声明、函数声明和表达式。

## 关键字

### this

关键字this只能在类的实例方法中使用。

**示例**

1. class A {
2.   count: string = 'a';
3.   m(i: string): void {
4.     this.count = i;
5.   }
6. }

使用限制：

- 不支持this类型
- 不支持在函数和类的静态方法中使用this

**示例**

1. class A {
2.   n: number = 0;
3.   f1(arg1: this) {} // 编译时错误，不支持this类型
4.   static f2(arg1: number) {
5.     this.n = arg1;  // 编译时错误，不支持在类的静态方法中使用this
6.   }
7. }

8. function foo(arg1: number) {
9.   this.n = i;       // 编译时错误，不支持在函数中使用this
10. }

关键字this的指向:

- 调用实例方法的对象
- 正在构造的对象

## 注解

注解（Annotation）是一种语言特性，它通过添加元数据来改变应用声明的语义。

注解的声明和使用如下所示：

**示例：**

1. // 注解的声明：
2. @interface ClassAuthor {
3.   authorName: string
4. }

5. // 注解的使用：
6. @ClassAuthor({authorName: "Bob"})
7. class MyClass {
8.   // ...
9. }

- 使用@interface声明注解。
- 注解ClassAuthor需要将元信息添加到类声明中。
- 注解必须放置在声明之前。
- 注解可以包含上述示例中所示的参数。

对于要使用的注解，其名称必须以符号@（例如：@MyAnno）为前缀。符号@和名称之间不允许有空格和行分隔符。

1. ClassAuthor({authorName: "Bob"}) // 编译错误：注解需要'@'为前缀
2. @ ClassAuthor({authorName: "Bob"}) // 编译错误：符号`@`和名称之间不允许有空格和行分隔符

如果在使用位置无法访问注解名称，则会发生编译错误。

注解声明可以导出并在其他文件中使用。

多个注解可以应用于同一个声明（注解间的先后顺序不影响使用）。

1. @MyAnno()
2. @ClassAuthor({authorName: "John Smith"})
3. class MyClass {
4.   // ...
5. }

注解不是Typescript中的特性，只能在.ets/.d.ets文件中使用。

注意

应用开发中，在[release模式下构建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section19788284410)源码HAR，并同时[开启混淆](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/source-obfuscation)时，由于编译产物为JS文件，而在JS中没有注解的实现机制，因此会在编译过程中被移除，导致无法通过注解实现AOP插桩。

为避免因此引起的功能异常，禁止在JS HAR(编译产物中存在JS的HAR包)中使用注解。

如果需要在release模式并且开启混淆的情况下构建含有注解的HAR包，可以构建[字节码HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-har#section16598338112415)。

### 用户自定义注解

**从API version 20及之后版本，支持用户自定义注解。**

**用户自定义注解的声明**

用户自定义注解的定义与interface的定义类似，其中的interface关键字以符号@为前缀。

注解字段仅限于下面列举的类型：

- number
- boolean
- string
- 枚举
- 以上类型的数组
    
    说明
    
    - 如果使用其他类型用作注解字段的类型，则会发生编译错误。
    - 注解字段类型不支持BigInt。
    

注解字段的默认值必须使用常量表达式来指定。

常量表达式的场景如下所示：

- 数字字面量
- 布尔字面量
- 字符串字面量
- 枚举值（需要在编译时确定值）
- 以上常量组成的数组
    
    说明
    
    如果枚举值不能在编译时确定，会编译报错。
    

1. // a.ts
2. export enum X {
3.   x = foo(); // x不是编译时能确定的常量
4. }

5. // b.ets
6. import {X} from './a';

7. @interface Position {
8.   data: number = X.x; // 编译错误：注解字段的默认值必须使用常量表达式
9. }

注解必须定义在顶层作用域（top-level），否则会出现编译报错。

注解的名称不能与注解定义所在作用域内可见的其他实体名称相同，否则会出现编译报错。

注解不支持类型Typescript中的合并，否则会出现编译报错。

1. namespace ns {
2.   @interface MataInfo { // 编译错误：注解必须定义在顶层作用域
3.     // ...
4.   }
5. }

6. @interface Position {
7.   // ...
8. }

9. class Position { // 编译错误：注解的名称不能与注解定义所在作用域内可见的其他实体名称相同
10.   // ...
11. }

12. @interface ClassAuthor {
13.   name: string;
14. }

15. @interface ClassAuthor { // 编译错误：注解的名称不能与注解定义所在作用域内可见的其他实体名称相同
16.   data: string;
17. }

注解不是类型，把注解当类型使用时会出现编译报错（例如：对注解使用类型别名）。

1. @interface Position {}
2. type Pos = Position; // 编译错误：注解不是类型

注解不支持在类的getter和setter方法中添加，若添加注解会编译报错。

1. @interface ClassAuthor {
2.   authorName: string;
3. }

4. @ClassAuthor({authorName: 'John Smith'})
5. class MyClass {
6.   private _name: string = 'Bob';

7.   @ClassAuthor({authorName: 'John Smith'}) // 编译错误：注解不支持在类的getter和setter方法添加
8.   get name() {
9.     return this._name;
10.   }

11.   @ClassAuthor({authorName: 'John Smith'}) // 编译错误：注解不支持在类的getter和setter方法添加
12.   set name(authorName: string) {
13.     this._name = authorName;
14.   }
15. }

**用户自定义注解的使用**

注解声明示例如下：

1. @interface ClassPreamble {
2.   authorName: string;
3.   revision: number = 1;
4. }
5. @interface MyAnno {}

当前仅允许对class declarations和method declarations使用注解，对类和方法可以同时使用同一个注解。

注解用法示例如下：

1. @ClassPreamble({authorName: "John", revision: 2})
2. class C1 {
3.   // ...
4. }

5. @ClassPreamble({authorName: "Bob"}) // revision的默认值为1
6. class C2 {
7.   // ...
8. }

9. @MyAnno() // 对类和方法可以同时使用同一个注解
10. class C3 {
11.   @MyAnno()
12.   foo() {}
13.   @MyAnno()
14.   static bar() {}
15. }

注解中的字段顺序不影响使用。

1. @ClassPreamble({authorName: "John", revision: 2})
2. // the same as:
3. @ClassPreamble({revision: 2, authorName: "John"})

使用注解时，必须给所有没有默认值的字段赋值，否则会发生编译错误。

说明

赋值应当与注解声明的类型一致，所赋的值与注解字段默认值的要求一样，只能使用常量表达式。

1. @ClassPreamble() // 编译错误：authorName字段未定义
2. class C1 {
3.   // ...
4. }

如果注解中定义了数组类型的字段，则使用数组字面量来设置该字段的值。

1. @interface ClassPreamble {
2.   authorName: string;
3.   revision: number = 1;
4.   reviewers: string[];
5. }

6. @ClassPreamble(
7.   {
8.     authorName: "Alice",
9.     reviewers: ["Bob", "Clara"]
10.   }
11. )
12. class C3 {
13.   // ...
14. }

如果不需要定义注解字段，可以省略注解名称后的括号。

1. @MyAnno
2. class C4 {
3.   // ...
4. }

**导入和导出注解**

注解也可以被导入导出。针对导出，当前仅支持在定义时的导出，即export @interface的形式。

**示例：**

1. export @interface MyAnno {}

针对导入，当前仅支持import {}和import * as两种方式。

**示例：**

1. // a.ets
2. export @interface MyAnno {}
3. export @interface ClassAuthor {}

4. // b.ets
5. import { MyAnno } from './a';
6. import * as ns from './a';

7. @MyAnno
8. @ns.ClassAuthor
9. class C {
10.   // ...
11. }

- 不允许在import中对注解进行重命名。

1. import { MyAnno as Anno } from './a'; // 编译错误：不允许在import中对注解进行重命名

不允许对注解使用任何其他形式的 import/export，这会导致编译报错。

- 由于注解不是类型，因此禁止使用type符号进行导入和导出。

1. import type { MyAnno } from './a'; // 编译错误：注解不允许使用'type'符号进行导入和导出

- 如果仅从模块导入注解，则不会触发模块的副作用。

1. // a.ets
2. export @interface Anno {}

3. export @interface ClassAuthor {}

4. console.info('hello');

5. // b.ets
6. import { Anno } from './a';
7. import * as ns from './a';

8. // 仅引用了Anno注解，不会导致a.ets的console.info执行
9. class X {
10.   // ...
11. }

**.d.ets文件中的注解**

注解可以出现在.d.ets文件中。

可以在.d.ets文件中用环境声明（ambient declaration）来声明注解。

1. ambientAnnotationDeclaration:
2.   'declare' userDefinedAnnotationDeclaration
3.   ;

**示例：**

1. // a.d.ets
2. export declare @interface ClassAuthor {}

上述声明中：

- 不会引入新的注解定义，而是提供注解的类型信息。
- 注解需定义在其他源代码文件中。
- 注解的环境声明和实现需要完全一致，包括字段的类型和默认值。

1. // a.d.ets
2. export declare @interface NameAnno{name: string = ""}

3. // a.ets
4. export @interface NameAnno{name: string = ""} // ok

环境声明的注解和class类似，也可以被import使用。

1. // a.d.ets
2. export declare @interface MyAnno {}

3. // b.ets
4. import { MyAnno } from './a';

5. @MyAnno
6. class C {
7.   // ...
8. }

**编译器自动生成的.d.ets文件**

当编译器根据ets代码自动生成.d.ets文件时，存在以下2种情况。

1. 当注解定义被导出时，源代码中的注解定义会在.d.ets文件中保留。
    
    1. // a.ets
    2. export @interface ClassAuthor {}
    
    3. @interface MethodAnno { // 没导出
    4.   data: number;
    5. }
    
    6. // a.d.ets 编译器生成的声明文件
    7. export declare @interface ClassAuthor {}
    
2. 当下面所有条件成立时，源代码中实体的注解实例会在.d.ets文件中保留。
    
    2.1 注解的定义被导出（import的注解也算作被导出）。
    
    2.2 如果实体是类，则类被导出。
    
    2.3 如果实体是方法，则类被导出，并且方法不是私有方法。
    
    1. // a.ets
    2. import { ClassAuthor } from './author';
    
    3. export @interface MethodAnno {
    4.   data: number = 0;
    5. }
    
    6. @ClassAuthor
    7. class MyClass {
    8.   @MethodAnno({data: 123})
    9.   foo() {}
    
    10.   @MethodAnno({data: 456})
    11.   private bar() {}
    12. }
    
    13. // a.d.ets 编译器生成的声明文件
    14. import {ClassAuthor} from "./author";
    
    15. export declare @interface MethodAnno {
    16.   data: number = 0;
    17. }
    
    18. @ClassAuthor
    19. export declare class MyClass {
    20.   @MethodAnno({data: 123})
    21.   foo(): void;
    
    22.   bar; // 私有方法不保留注解
    23. }
    

**开发者生成的.d.ets文件**

开发者生成的.d.ets文件中的注解信息不会自动应用到实现的源代码中。

**示例：**

1. // b.d.ets 开发者生成的声明文件
2. @interface ClassAuthor {}

3. @ClassAuthor // 声明文件中有注解
4. class C {
5.   // ...
6. }

7. // b.ets 开发者对声明文件实现的源代码
8. @interface ClassAuthor {}

9. // 实现文件中没有注解
10. class C {
11.   // ...
12. }

在最终编译产物中，class C没有注解。

**重复注解和继承**

同一个实体不能重复使用同一注解，否则会导致编译错误。

1. @MyAnno({name: "123", value: 456})
2. @MyAnno({name: "321", value: 654}) // 编译错误：不允许重复注释
3. class C {
4.   // ...
5. }

子类不会继承基类的注解，也不会继承基类方法的注解。

**注解和抽象类、抽象方法**

不支持对抽象类或抽象方法使用注解，否则将导致编译错误。

1. @MyAnno // 编译错误：不允许在抽象类和抽象方法上使用注解
2. abstract class C {
3.   @MyAnno
4.   abstract foo(): void; // 编译错误：不允许在抽象类和抽象方法上使用注解
5. }

## ArkUI支持

本节演示ArkTS为创建图形用户界面（GUI）程序提供的机制。ArkUI基于TypeScript提供了一系列扩展能力，以声明式地描述应用程序的GUI以及GUI组件间的交互。

### ArkUI示例

[MVVM代码示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-mvvm#%E4%BB%A3%E7%A0%81%E7%A4%BA%E4%BE%8B)提供了一个完整的基于ArkUI的应用程序，以展示其GUI编程功能。

有关ArkUI功能的更多详细信息，请参见ArkUI[基本语法概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-basic-syntax-overview)。
# ArkTS编程规范

更新时间: 2025-12-16 16:33

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
# ArkTS语法适配背景

更新时间: 2025-12-16 16:34

ArkTS在保留TypeScript（简称TS）基本语法风格的基础上，进一步通过规范强化了静态检查和分析，使得开发者在程序开发阶段能够检测出更多错误，提升程序的稳定性和运行性能。本文将详细解释为什么建议将TS代码适配为ArkTS代码。

## 程序稳定性

动态类型语言如JavaScript（简称JS）虽能提升开发效率，但也容易在运行时引发非预期错误。例如未检查的undefined值可能导致程序崩溃，这类问题若能在开发阶段发现将显著提升稳定性。TypeScript（TS）通过类型标注机制，使编译器能在编译时检测出多数类型错误，但其非强制类型系统仍存在局限。例如未标注类型的变量会阻碍完整编译检查。ArkTS通过强制静态类型系统克服这一缺陷，实施更严格的类型验证机制，从而最大限度减少运行时错误的发生。

下面这个例子展示了ArkTS通过强制严格的类型检查来提高代码稳定性和正确性。

**显式初始化类的属性**

ArkTS要求类的所有属性在声明时或者在构造函数中显式地初始化，这和TS中的strictPropertyInitialization检查一致。以下的代码片段是非严格模式下的TS代码。

1. class Person {
2.   name: string; // undefined

3.   setName(n: string): void {
4.     this.name = n;
5.   }

6.   getName(): string {
7.   // 开发者使用"string"作为返回类型，这隐藏了name可能为"undefined"的事实。
8.   // 更合适的做法是将返回类型标注为"string | undefined"，以告诉开发者这个API所有可能的返回值的类型。
9.     return this.name;
10.   }
11. }

12. let buddy = new Person()
13. // 假设代码中没有对name的赋值，例如没有调用"buddy.setName('John')"
14. buddy.getName().length; // 运行时异常：name is undefined

ArkTS要求属性显式初始化，代码应如下所示：

1. class Person {
2.   name: string = '';

3.   setName(n: string): void {
4.     this.name = n;
5.   }

6.   // 类型为"string"，不可能为"null"或者"undefined"
7.   getName(): string {
8.     return this.name;
9.   }
10. }

11. let buddy = new Person()
12. // 假设代码中没有对name的赋值，例如没有调用"buddy.setName('John')"
13. buddy.getName().length; // 0, 没有运行时异常

如果name可以是undefined，其类型应在代码中精确标注。

1. class Person {
2.     name?: string; // 可能为undefined

3.     setName(n: string): void {
4.         this.name = n;
5.     }

6.     // 编译时错误：name可能为"undefined"，所以不能将这个API的返回类型标注为"string"
7.     getNameWrong(): string {
8.         return this.name;
9.     }

10.     getName(): string | undefined { // 返回类型匹配name的类型
11.         return this.name;
12.     }
13. }

14. let buddy = new Person()
15. // 假设代码中没有对name的赋值，例如没有调用"buddy.setName('John')"

16. // 编译时错误：编译器认为下一行代码有可能访问"undefined"的属性，报错
17. buddy.getName().length;  // 编译失败

18. buddy.getName()?.length; // 编译成功，没有运行时错误

## 程序性能

为了确保程序的正确性，动态类型语言需要在运行时检查对象的类型。例如JavaScript不允许访问undefined的属性。检查一个值是否为undefined的唯一方法是在运行时进行类型检查。所有JavaScript引擎都会执行以下操作：如果一个值不是undefined，则可以访问其属性；如果尝试访问的值是undefined，则会抛出异常。虽然现代JavaScript引擎可以优化这类操作，但仍然存在一些无法消除的运行时检查，这会导致程序变慢。由于TypeScript代码总是先被编译成JavaScript代码，因此在TypeScript中也会遇到相同的问题。ArkTS解决了这个问题。通过启用静态类型检查，ArkTS代码将被编译成方舟字节码文件，而不是JavaScript代码。因此，ArkTS运行速度更快，更容易被进一步优化。

**Null Safety**

1. function notify(who: string, what: string) {
2.   console.info(`Dear ${who}, a message for you: ${what}`);
3. }

4. notify('Jack', 'You look great today');

在大多数情况下，函数notify会接受两个string类型的变量作为输入，产生一个新的字符串。但是，如果将一些特殊值作为输入，例如notify(null, undefined)，情况会怎么样呢？

程序仍会正常运行，输出预期值：Dear null, a message for you: undefined。虽然系统表现一切正常，但值得注意的是，为了保障该场景下程序的正确性，引擎在运行时会持续进行类型检查，其实现机制类似于以下伪代码所示：

1. function __internal_tostring(s: any): string {
2.   if (typeof s === 'string')
3.     return s;
4.   if (s === undefined)
5.     return 'undefined';
6.   if (s === null)
7.     return 'null';
8.   // ...
9. }

试想一下，如果notify函数并非只是简单的日志打印，而是某些高负载场景下关键逻辑的一部分，那么在运行时频繁执行类似__internal_tostring的类型检查操作，势必会带来显著的性能开销。

如果可以保证在运行时，只有string类型的值（不会是其他类型的值，例如null或者undefined）可以被传入函数notify呢？在这种情况下，因为可以确保没有其他边界情况，像__internal_tostring的检查就是多余的了。在该场景下，这种机制被称为“null-safety”（空安全），其核心目的是确保null不能作为合法的字符串类型值。如果ArkTS支持这一特性，那么任何类型不匹配的代码都将在编译阶段被拦截，无法编译通过。

1. function notify(who: string, what: string) {
2.   console.info(`Dear ${who}, a message for you: ${what}`);
3. }

4. notify('Jack', 'You look great today');
5. notify(null, undefined); // 编译时错误

TS通过启用编译选项strictNullChecks实现此特性。虽然TS被编译成JS，但因为JS没有这个特性，所以严格null检查仅在编译时起效。从程序稳定性和性能的角度考虑，ArkTS将“null-safety”视为一个重要的特性。因此，ArkTS强制进行严格null检查，在ArkTS中上述代码将会编译失败。作为交换，此类代码为ArkTS引擎提供了更多信息和关于值的类型保证，有助于优化性能。

## .ets代码兼容性

在API version 10之前的版本中，ArkTS（以.ets为扩展名的文件）在语法层面完全遵循标准的TypeScript规范。从API version 10 Release起，明确定义ArkTS的语法规则，同时，SDK增加了在编译流程中对.ets文件的ArkTS语法检查，通过编译告警或编译失败提示开发者适配新的ArkTS语法。

根据工程的compatibleSdkVersion，具体策略如下：

- compatibleSdkVersion >= 10 为标准模式。在该模式下，所有.ets文件必须严格遵循ArkTS语法规则，任何语法违规工程都会编译不通过，开发者需要修正所有语法问题后才能获得编译通过。
- compatibleSdkVersion < 10 为兼容模式。在该模式下，对.ets文件以warning形式提示违反ArkTS语法规则的所有代码。尽管违反ArkTS语法规则的工程在兼容模式下仍可编译成功，但需完全适配ArkTS语法后方可在标准模式下编译成功。

## 支持与TS/JS的交互

ArkTS支持与TS/JS的高效互操作。在当前版本中，ArkTS运行时兼容动态类型对象语义。在ArkTS与TypeScript/JavaScript交互操作场景中，直接复用TS/JS的数据和对象作为ArkTS的实体使用时，可能规避ArkTS的静态类型检查机制，进而引发运行时异常或引入额外的性能损耗。

1. // lib.ts
2. export class C {
3.   v: string; // 在TS严格模式下，编译期报错 Property 'v' has no initializer
4. }

5. export let c = new C()

6. // app.ets
7. import { C, c } from './lib';

8. function foo(c: C) {
9.   c.v.length;
10. }

11. foo(c);

## 方舟运行时兼容TS/JS

在API version 11上，HarmonyOS SDK中的TypeScript版本为4.9.5，target字段为es2017。应用中支持使用ECMA2017及更高版本的语法进行TS/JS开发。

**应用环境限制**

1. 强制使用严格模式（use strict）
    
2. 禁止使用eval()
    
3. 禁止使用with() {}
    
4. 禁止以字符串为代码创建函数
    
5. 禁止循环依赖
    
    循环依赖示例:
    
    1. // bar.ets
    2. import {v} from './foo'; // bar.ets依赖foo.ets
    3. export let u = 0;
    
    4. // foo.ets
    5. import {u} from './bar'; // foo.ets同时又依赖bar.ets
    6. export let v = 0;
    
    7. //应用加载失败
    

**与标准TS/JS的差异**

在标准的TS/JS中，JSON的数字格式要求小数点后必须跟随数字，例如 2.e3 这类科学计数法不被允许，会导致 SyntaxError。方舟运行时则支持这类科学计数法。
