# UI开发（ArkTS声明式开发范式）概述

更新时间: 2025-12-16 16:38

基于ArkTS的声明式开发范式的方舟开发框架是一套开发极简、高性能、支持跨设备的UI开发框架，提供了构建应用UI所必需的能力，主要包括：

- **ArkTS**
    
    ArkTS是优选的主力应用开发语言，围绕应用开发在[TypeScript](https://www.typescriptlang.org/)（简称TS）生态基础上做了进一步扩展。扩展能力包含声明式UI描述、自定义组件、动态扩展UI元素、状态管理和渲染控制。状态管理作为基于ArkTS的声明式开发范式的特色，通过功能不同的装饰器给开发者提供了清晰的页面更新渲染流程和管道。状态管理包括UI组件状态和应用程序状态，两者协作可以使开发者完整地构建整个应用的数据更新和UI渲染。ArkTS语言的基础知识请参考[初识ArkTS语言](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-get-started)。
    
- **布局**
    
    布局是UI的必要元素，它定义了组件在界面中的位置。ArkUI框架提供了多种布局方式，除了基础的线性布局、层叠布局、弹性布局、相对布局、栅格布局外，也提供了相对复杂的列表、宫格、轮播。
    
- **组件**
    
    组件是UI的必要元素，形成了在界面中的样子，由框架直接提供的称为**系统组件**，由开发者定义的称为**自定义组件**。系统组件包括按钮、单选框、进度条、文本等。开发者可以通过链式调用的方式设置系统组件的渲染效果。开发者可以将系统组件组合为自定义组件，通过这种方式将页面组件化为一个个独立的UI单元，实现页面不同单元的独立创建、开发和复用，具有更强的工程性。
    
- **页面路由和组件导航**
    
    开发者可以将应用的用户界面设计为多个功能页面[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)，页面通过栈结构管理，并通过导航容器[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)完成页面间的调度管理如跳转、回退等操作，以实现应用内的功能解耦。
    
- **图形**
    
    方舟开发框架提供了多种类型图片的显示能力和多种自定义绘制的能力，以满足开发者的自定义绘图需求，支持绘制形状、填充颜色、绘制文本、变形与裁剪、嵌入图片等。
    
- **动画**
    
    动画是UI的重要元素之一。优秀的动画设计能够极大地提升用户体验，框架提供了丰富的动画能力，除了组件内置动画效果外，还包括属性动画、显式动画、自定义转场动画以及动画API等，开发者可以通过封装的物理模型或者调用动画能力API来实现自定义动画轨迹。
    
- **交互事件**
    
    交互事件是UI和用户交互的必要元素。方舟开发框架提供了多种交互事件，除了触摸事件、鼠标事件、键盘按键事件、焦点事件等通用事件外，还包括基于通用事件进行进一步识别的手势事件。手势事件有单一手势如点击手势、长按手势、拖动手势、捏合手势、旋转手势、滑动手势，以及通过单一手势事件进行组合的组合手势事件。
    
- **自定义能力**
    
    自定义能力是UI开发框架提供给开发者对UI界面进行开发和定制化的能力。包括：自定义组合、自定义扩展、自定义节点和自定义渲染。
    

## 特点

- 开发效率高，开发体验好
    
    - 代码简洁：通过接近自然语义的方式描述UI，不必关心框架如何实现UI绘制和渲染。
    - 数据驱动UI变化：让开发者更专注自身业务逻辑的处理。当UI发生变化时，开发者无需编写在不同的UI之间进行切换的UI代码， 开发人员仅需要编写引起界面变化的数据，具体UI如何变化交给框架。
    - 开发体验好：界面也是代码，让开发者的编程体验得到提升。
- 性能优越
    
    - 声明式UI前端和UI后端分层：UI后端采用C++语言构建，提供对应前端的基础组件、布局、动效、交互事件、组件状态管理和渲染管线。
    - 语言编译器和运行时的优化：统一字节码、高效FFI（Foreign Function Interface）、AOT（Ahead Of Time）、引擎极小化、类型优化等。
- 生态容易快速推进
    
    能够借力主流语言生态快速推进，语言相对中立友好，有相应的标准组织可以逐步演进。
    

## 整体架构

**图1** 整体架构图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163826.99677842590292424283240459096482:50001231000000:2800:4B27C8DC572BE038CC901FB8D19BE43E00A905408EBFBB38191BE99BF16166B7.png)

- **声明式UI前端**
    
    提供了UI开发范式的基础语言规范，并提供内置的UI组件、布局和动画，提供了多种状态管理机制，为应用开发者提供一系列接口支持。
    
- **语言运行时**
    
    选用方舟语言运行时，提供了针对UI范式语法的解析能力、跨语言调用支持的能力和TS语言高性能运行环境。
    
- **声明式UI后端引擎**
    
    后端引擎提供了兼容不同开发范式的UI渲染管线，提供多种基础组件、布局计算、动效、交互事件，提供了状态管理和绘制能力。
    
- **渲染引擎**
    
    提供了高效的绘制能力，将渲染管线收集的渲染指令，绘制到屏幕的能力。
    
- **平台适配层**
    
    提供了对系统平台的抽象接口，具备接入不同系统的能力，如系统渲染管线、生命周期调度等。
    

## 开发流程

使用UI开发框架开发应用时，主要涉及如下开发过程。

|任务|简介|相关指导|
|:--|:--|:--|
|学习ArkTS|介绍了ArkTS的基本语法、状态管理和渲染控制的场景。|- [基本语法](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-basic-syntax-overview)<br><br>- [状态管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-state-management-overview)<br><br>- [渲染控制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-overview)|
|设置组件导航和页面路由|介绍了如何设置组件间的导航以及页面路由。|- [组件导航（推荐）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation)<br><br>- [页面路由](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-routing)|
|组件布局|介绍了几种常用的布局方式。|- [常用布局](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-layout-development-overview)|
|列表与网格|介绍了几种列表与网格组件的使用方法。|- [列表与网格](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-list-grid-development-overview)|
|使用文本|介绍了输入框、富文本和属性字符串等文本组件的使用方法。|- [文本显示](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-text-display)<br><br>- [文本输入](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-text-input)<br><br>- [富文本](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-richeditor)<br><br>- [图标小符号](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-symbol)<br><br>- [属性字符串](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-styled-string)|
|媒体展示|介绍了几种媒体展示组件的使用方法。|- [显示图片 (Image)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-graphics-display)<br><br>- [视频播放 (Video)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-video-player)<br><br>- [创建轮播 (Swiper)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-layout-development-create-looping)<br><br>- [创建弧形轮播 (ArcSwiper)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-layout-development-arcswiper)|
|表单选择|介绍了几种常用表单选择组件的使用方法。|- [表单与选择组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-forms-overview)|
|添加组件|介绍了XComponent和Progress组件的使用方法。|- [自定义渲染 (XComponent)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/napi-xcomponent-guidelines)<br><br>- [进度条 (Progress)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-progress-indicator)|
|使用弹窗|介绍了弹窗的应用场景与使用方法。|- [使用弹出框](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-base-dialog-overview)<br><br>- [菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-menu-overview)<br><br>- [气泡提示](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-popup-overview)<br><br>- [绑定模态页面](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-modal-overview)<br><br>- [即时反馈](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-toast)<br><br>- [设置浮层](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-overlaymanager)|
|显示图形|介绍了如何显示图片、绘制自定义几何图形以及使用画布绘制自定义图形。|- [几何图形](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-geometric-shape-drawing)<br><br>- [画布](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-drawing-customization-on-canvas)|
|几何图形|介绍了如何绘制几何图形。|- [几何图形绘制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-shape-overview)|
|添加交互响应|介绍了交互基础机制、输入设备与事件和手势响应的能力。|- [交互基础机制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-interaction-basic-principles)<br><br>- [输入设备与事件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/rkts-interaction-development-guide-raw-input-event)<br><br>- [手势响应](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/rkts-interaction-development-guide-support-gesture)|
|使用动画|介绍了组件和页面使用动画的典型场景。|- [属性动画](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-attribute-animation-overview)<br><br>- [转场动画](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-transition-overview)<br><br>- [粒子动画](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-particle-animation)<br><br>- [组件动画](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-component-animation)<br><br>- [动画曲线](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-traditional-curve)<br><br>- [动画衔接](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-animation-smoothing)<br><br>- [动画效果](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-blur-effect)<br><br>- [帧动画](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-animator)|
|使用自定义能力|介绍了自定义能力的基本概念和如何使用自定义能力。|- [自定义组合](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-user-defined-composition)<br><br>- [自定义节点](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-user-defined-node)<br><br>- [自定义扩展](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-user-defined-modifier)|
|UI国际化|介绍如何实现应用程序UI界面的国际化，包含资源配置和镜像布局。|- [UI国际化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-internationalization)|
|无障碍与适老化|介绍了无障碍和适老化的使用场景和使用方法。|- [支持无障碍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-universal-attributes-accessibility)<br><br>- [支持适老化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkui-support-for-aging-adaptation)|
|主题设置|介绍了应用级和页面级的主题设置能力。|- [应用深浅色适配](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-dark-light-color-adaptation)<br><br>- [设置应用内主题换肤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/theme_skinning)|
|UI系统场景化能力|介绍了如何使用UIContext中对应的接口获取与实例绑定的对象，以及全屏方式拉起元服务的方法。|- [使用UI上下文接口操作界面](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-global-interface)<br><br>- [全屏启动元服务组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-fullscreencomponent)|

## 通用规则

- **默认单位**
    
    表示长度的入参单位默认为vp，即入参为number类型、以及[Length](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-types#length)和[Dimension](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-types#dimension10)类型中的number单位为vp。
    
- **异常值处理**
    
    输入的参数为异常（undefined，null或无效值）时，处理规则如下：
    
    （1）对应参数有默认值，按默认值处理；
    
    （2）对应参数无默认值，该参数对应的属性或接口不生效。
    # 基本语法概述

更新时间: 2025-12-16 16:38

在初步了解ArkTS语言后，本指南将以具体的示例来说明ArkTS的基本组成。

如下图所示，点击“按钮”时，文本内容从“Hello World”变为“Hello ArkUI”。

**图1** 示例效果图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163856.11141780793269377806891242130528:50001231000000:2800:6226B257CF346C1B332B42EC0F899472A2D46C63779E3EDD1090F9DB54B3F449.gif)

本示例中，ArkTS的基本组成如下所示。

**图2** ArkTS的基本组成

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163856.30126230128707271975624442001967:50001231000000:2800:D5AB7D011DDD13C0E053C270695DA698EFEDE62D0FEC25C8F85D6AD98A8752B3.png)

说明

自定义变量不能与基础通用属性/事件名重复。

- 装饰器： 用于装饰类、结构、方法以及变量，并赋予其特殊的含义。如上述示例中@Entry、@Component和@State都是装饰器，[@Component](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components#component)表示自定义组件，[@Entry](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components#entry)表示该自定义组件为入口组件，[@State](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-state)表示组件中的状态变量，状态变量变化会触发UI刷新。
    
- [UI描述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-declarative-ui-description)：以声明式的方式来描述UI的结构，例如build()方法中的代码块。
    
- [自定义组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components)：可复用的UI单元，可组合其他组件，如上述被@Component装饰的struct Hello。
    
- 系统组件：ArkUI框架中默认内置的基础和容器组件，可以直接调用，例如示例中的Column、Text、Divider、Button。
    
- [属性方法](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-component-general-attributes)：组件可以通过链式调用配置多项属性，如fontSize()、width()、height()、backgroundColor()等。
    
- [事件方法](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-component-general-events)：组件可以通过链式调用设置多个事件的响应逻辑，如跟随在Button后面的onClick()。
    

除此之外，ArkTS扩展了多种语法范式来使开发更加便捷：

- [@Builder](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-builder)/[@BuilderParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-builderparam)：特殊的封装UI描述的方法，细粒度的封装和复用UI描述。
    
- [@Extend](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-extend)/[@Styles](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-style)：扩展系统组件和封装属性样式，更灵活地组合系统组件。
    
- [stateStyles](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-statestyles)：多态样式，可以依据组件的内部状态的不同，设置不同样式。
- # 声明式UI描述

更新时间: 2025-12-16 16:39

ArkTS以声明方式组合和扩展组件来描述应用程序的UI，同时还提供了基本的属性、事件和子组件配置方法，帮助开发者实现应用交互逻辑。

## 创建组件

根据组件构造方法的不同，创建组件包含有参数和无参数两种方式。

说明

创建组件不需要使用new关键字。

### 无参数

如果组件接口定义中不包含必选构造参数，则组件后面的“()”不需要配置任何内容。例如：Divider组件不包含构造参数。

1. Column() {
2.   Text('item 1')
3.   Divider()
4.   Text('item 2')
5. }

### 有参数

如果组件接口定义包含构造参数，则在组件后的“()”中配置相应参数。

- Image组件的必选参数src。
    
    1. Image('https://xyz/test.jpg')
    
- Text组件的非必选参数content。
    
    1. // string类型的参数
    2. Text('test')
    3. // $r形式引入应用资源，可应用于多语言场景
    4. Text($r('app.string.title_value'))
    5. // 无参数形式
    6. Text()
    
- 变量或表达式可以用于参数赋值，表达式结果类型必须符合参数要求。
    
    例如，设置变量或表达式来构造Image和Text组件的参数。
    
    1. Image(this.imagePath)
    2. Image('https://' + this.imageUrl)
    3. Text(`count: ${this.count}`)
    

## 配置属性

属性方法以“.”链式调用配置组件样式和其他属性，建议每个属性方法单独一行。

- 配置Text组件的字体大小。
    
    1. Text('test')
    2.   .fontSize(12)
    
- 配置组件的多个属性。
    
    1. Image('test.jpg')
    2.   .alt('error.jpg')
    3.   .width(100)
    4.   .height(100)
    
- 除了直接传递常量参数，还可以传递变量或表达式。
    
    1. Text('hello')
    2.   .fontSize(this.size)
    3. Image('test.jpg')
    4.   .width(this.count % 2 === 0 ? 100 : 200)
    5.   .height(this.offset + 100)
    
- 对于系统组件，ArkUI还为其属性预定义了一些枚举类型供开发者调用，枚举类型可以作为参数传递，但必须满足参数类型要求。
    
    例如，可以按以下方式配置Text组件的颜色和字体样式。
    
    1. Text('hello')
    2.   .fontSize(20)
    3.   .fontColor(Color.Red)
    4.   .fontWeight(FontWeight.Bold)
    

## 配置事件

事件方法以“.”链式调用的方式配置系统组件支持的事件，建议每个事件方法单独写一行。

- 使用箭头函数配置组件的事件方法。
    
    1. Button('Click me')
    2.   .onClick(() => {
    3.     this.myText = 'ArkUI';
    4.   })
    
- 使用箭头函数表达式配置组件的事件方法，要求使用“() => {...}”，以确保函数与组件绑定，同时符合ArkTS语法规范。
    
    1. Button('add counter')
    2.   .onClick(() => {
    3.     this.counter += 2;
    4.   })
    
- 使用组件的成员函数配置组件的事件方法，需要bind this。ArkTS语法不建议使用成员函数配合bind this来配置组件的事件方法。
    
    1. myClickHandler(): void {
    2.   this.counter += 2;
    3. }
    4. // ...
    5. Button('add counter')
    6.   .onClick(this.myClickHandler.bind(this))
    
- 使用声明的箭头函数时可以直接调用，不需要bind this。
    
    1. fn = () => {
    2.   console.info(`counter: ${this.counter}`)
    3.   this.counter++
    4. }
    5. // ...
    6. Button('add counter')
    7.   .onClick(this.fn)
    

说明

箭头函数内部的this是词法作用域，由上下文确定。匿名函数可能会出现this指向不明确的问题，因此在ArkTS中不允许使用。

## 配置子组件

如果组件支持子组件配置，则需在尾随闭包"{...}"中为组件添加子组件的UI描述。Column、Row、Stack、Grid、List等组件都是容器组件。

- 以下是简单的Column组件配置子组件的示例。
    
    1. Column() {
    2.   Text('Hello')
    3.     .fontSize(100)
    4.   Divider()
    5.   Text(this.myText)
    6.     .fontSize(100)
    7.     .fontColor(Color.Red)
    8. }
    
- 容器组件均支持子组件配置，可以实现相对复杂的多级嵌套。
    
    1. Column() {
    2.   Row() {
    3.     Image('test1.jpg')
    4.       .width(100)
    5.       .height(100)
    6.     Button('click +1')
    7.       .onClick(() => {
    8.         console.info('+1 clicked!');
    9.       })
    10.   }
    11. }
    # 创建自定义组件

更新时间: 2025-12-16 16:40

在ArkUI中，UI显示的内容均为组件，由框架直接提供的称为系统组件，由开发者定义的称为自定义组件。进行UI界面开发时，不仅要组合使用系统组件，还需考虑代码的可复用性、业务逻辑与UI的分离，以及后续版本的演进等因素。因此，将UI和部分业务逻辑封装成自定义组件是不可或缺的能力。

自定义组件具有以下特点：

- 可组合：允许开发者组合使用系统组件及其属性和方法。
    
- 可重用：自定义组件可以被其他组件重用，并作为不同的实例在不同的父组件或容器中使用。
    
- 数据驱动UI更新：通过状态变量的改变，来驱动UI的刷新。
    

## 自定义组件的基本用法

以下示例展示了自定义组件的基本用法。

1. @Component
2. struct HelloComponent {
3.   @State message: string = 'Hello, World!';

4.   build() {
5.     // HelloComponent自定义组件组合系统组件Row和Text
6.     Row() {
7.       Text(this.message)
8.         .onClick(() => {
9.           // 状态变量message的改变驱动UI刷新，UI从'Hello, World!'刷新为'Hello, ArkUI!'
10.           this.message = 'Hello, ArkUI!';
11.         })
12.     }
13.   }
14. }

注意

如果在其他文件中引用自定义组件，需要使用export关键字导出组件，并在使用的页面import该自定义组件。

可以在其他自定义组件的build()函数中多次创建HelloComponent，以实现自定义组件的重用。

1. @Entry
2. @Component
3. struct ParentComponent {
4.   build() {
5.     Column() {
6.       Text('ArkUI message')
7.       HelloComponent({ message: 'Hello World!' });
8.       Divider()
9.       HelloComponent({ message: '你好，世界!' });
10.     }
11.   }
12. }

要完全理解上面的示例，需要了解自定义组件的以下概念定义，本文将在后面的小节中介绍：

- [自定义组件的基本结构](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components#%E8%87%AA%E5%AE%9A%E4%B9%89%E7%BB%84%E4%BB%B6%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%BB%93%E6%9E%84)
    
- [成员函数/变量](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components#%E6%88%90%E5%91%98%E5%87%BD%E6%95%B0%E5%8F%98%E9%87%8F)
    
- [自定义组件的参数规定](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components#%E8%87%AA%E5%AE%9A%E4%B9%89%E7%BB%84%E4%BB%B6%E7%9A%84%E5%8F%82%E6%95%B0%E8%A7%84%E5%AE%9A)
    
- [build()函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components#build%E5%87%BD%E6%95%B0)
    
- [自定义组件通用样式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components#%E8%87%AA%E5%AE%9A%E4%B9%89%E7%BB%84%E4%BB%B6%E9%80%9A%E7%94%A8%E6%A0%B7%E5%BC%8F)
    

## 自定义组件的基本结构

### struct

自定义组件基于struct实现，struct + 自定义组件名 + {...}的组合构成自定义组件，不能有继承关系。对于struct的实例化，可以省略new。

说明

自定义组件名、类名、函数名不得与系统组件名重复。

### @Component

@Component装饰器仅装饰struct关键字声明的数据结构。被装饰的struct具备组件化的能力，需要实现build方法描述UI，一个struct只能被一个@Component装饰。@Component可以接受一个可选的boolean类型参数。

说明

从API version 9开始，该装饰器支持在ArkTS卡片中使用。

从API version 11开始，@Component可以接受一个可选的boolean类型参数。

从API version 11开始，该装饰器支持在元服务中使用。

1. @Component
2. struct MyComponent {
3. }

**freezeWhenInactive11+**

[组件冻结](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-custom-components-freeze)选项。

|名称|类型|只读|可选|说明|
|:--|:--|:--|:--|:--|
|freezeWhenInactive|boolean|否|否|是否开启组件冻结。默认值false。true表示开启组件冻结，false表示不开启组件冻结。|

1. @Component({ freezeWhenInactive: true })
2. struct MyComponent {
3. }

### build()函数

build()函数用于定义自定义组件的声明式UI描述，自定义组件必须定义build()函数。

1. @Component
2. struct MyComponent {
3.   build() {
4.   }
5. }

### @Entry

@Entry装饰的自定义组件将作为UI页面的入口。在单个UI页面中，仅允许存在一个由@Entry装饰的自定义组件作为页面的入口。@Entry可以接受一个可选的[LocalStorage](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-localstorage)参数。

说明

从API version 9开始，该装饰器支持在ArkTS卡片中使用。

从API version 10开始，@Entry可以接受一个可选的[LocalStorage](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-localstorage)参数或者一个可选的EntryOptions10+参数。

从API version 11开始，该装饰器支持在元服务中使用。

1. @Entry
2. @Component
3. struct MyComponent {
4. }

**EntryOptions10+**

命名路由跳转选项。

|名称|类型|只读|可选|说明|
|:--|:--|:--|:--|:--|
|routeName|string|否|是|表示作为命名路由页面的名字。|
|storage|[LocalStorage](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-localstorage)|否|是|页面级的UI状态存储。当未传入时，框架会创建一个新的LocalStorage实例作为默认值。|
|useSharedStorage12+|boolean|否|是|是否使用[loadContent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-windowstage#loadcontent9)传入的LocalStorage实例对象。默认值false。true：使用共享的[LocalStorage](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-localstorage)实例对象。false：不使用共享的[LocalStorage](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-localstorage)实例对象。|

说明

当useSharedStorage设置为true且storage已赋值时，useSharedStorage的值优先级更高。

1. @Entry({ routeName : 'myPage' })
2. @Component
3. struct MyComponent {
4. }

### @Reusable

@Reusable装饰的自定义组件具备可复用能力。详细请参考：[@Reusable装饰器：组件复用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-reusable#%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF)。

说明

从API version 10开始，该装饰器支持在ArkTS卡片中使用。

1. @Reusable
2. @Component
3. struct MyComponent {
4. }

## 成员函数/变量

自定义组件除了必须要实现build()函数外，还可以实现其他成员函数，成员函数具有以下约束：

- 自定义组件的成员函数仅能从组件内部访问，且不建议声明为静态函数。

自定义组件可以包含成员变量，成员变量具有以下约束：

- 自定义组件的成员变量仅能从组件内部访问，且不建议声明为静态变量。
    
- 自定义组件的成员变量本地初始化有些是可选的，有些是必选的。具体是否需要本地初始化，是否需要从父组件通过参数传递初始化子组件的成员变量，请参考[状态管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-state-management-overview)。
    

## 自定义组件的参数规定

以下示例展示了如何在build方法里创建自定义组件，并在创建自定义组件的过程中，根据装饰器的规则来初始化自定义组件的参数。

1. @Component
2. struct MyComponent {
3.   private countDownFrom: number = 0;
4.   private color: Color = Color.Blue;

5.   build() {
6.     Column() {
7.       Text(`${this.countDownFrom}`)
8.         .backgroundColor(this.color)
9.     }
10.   }
11. }

12. @Entry
13. @Component
14. struct ParentComponent {
15.   private someColor: Color = Color.Pink;

16.   build() {
17.     Column() {
18.       // 创建MyComponent实例，并将创建MyComponent成员变量countDownFrom初始化为10，将成员变量color初始化为this.someColor
19.       MyComponent({ countDownFrom: 10, color: this.someColor })
20.     }
21.   }
22. }

以下示例代码将父组件中的函数传递给子组件，并在子组件中调用。

1. @Entry
2. @Component
3. struct Parent {
4.   @State cnt: number = 0
5.   submit: () => void = () => {
6.     this.cnt++;
7.   }

8.   build() {
9.     Column() {
10.       Text(`${this.cnt}`)
11.       Son({ submitArrow: this.submit })
12.     }
13.   }
14. }

15. @Component
16. struct Son {
17.   submitArrow?: () => void

18.   build() {
19.     Row() {
20.       Button('add')
21.         .width(80)
22.         .onClick(() => {
23.           if (this.submitArrow) {
24.             this.submitArrow()
25.           }
26.         })
27.     }
28.     .height(56)
29.   }
30. }

## build()函数

所有在build()函数中声明的语句统称为UI描述，UI描述需要遵循以下规则：

- @Entry装饰的自定义组件，其build()函数下的根节点唯一且必要，且必须为容器组件，其中ForEach禁止作为根节点。
    
    @Component装饰的自定义组件，其build()函数下的根节点唯一且必要，可以为非容器组件，其中ForEach禁止作为根节点。
    
    1. @Entry
    2. @Component
    3. struct MyComponent {
    4.   build() {
    5.     // 根节点唯一且必要，必须为容器组件
    6.     Row() {
    7.       ChildComponent()
    8.     }
    9.   }
    10. }
    
    11. @Component
    12. struct ChildComponent {
    13.   build() {
    14.     // 根节点唯一且必要，可为非容器组件
    15.     Image('test.jpg')
    16.   }
    17. }
    
- 不允许声明本地变量，反例如下。
    
    1. build() {
    2.   // 反例：不允许声明本地变量
    3.   let num: number = 1;
    4. }
    
- 不允许在UI描述里直接使用console.info，但允许在方法或者函数里使用，反例如下。
    
    1. build() {
    2.   // 反例：不允许console.info
    3.   console.info('print debug log');
    4. }
    
- 不允许创建本地的作用域，反例如下。
    
    1. build() {
    2.   // 反例：不允许本地作用域
    3.   {
    4.     // ...
    5.   }
    6. }
    
- 不允许调用没有用@Builder装饰的方法，允许系统组件的参数是TS方法的返回值。
    
    1. @Component
    2. struct ParentComponent {
    3.   doSomeCalculations() {
    4.   }
    
    5.   calcTextValue(): string {
    6.     return 'Hello World';
    7.   }
    
    8.   @Builder doSomeRender() {
    9.     Text(`Hello World`)
    10.   }
    
    11.   build() {
    12.     Column() {
    13.       // 反例：不能调用没有用@Builder装饰的方法
    14.       this.doSomeCalculations();
    15.       // 正例：可以调用
    16.       this.doSomeRender();
    17.       // 正例：参数可以为调用TS方法的返回值
    18.       Text(this.calcTextValue())
    19.     }
    20.   }
    21. }
    
- 不允许使用switch语法，当需要使用条件判断时，请使用[if](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-ifelse)。示例如下。
    
    1. build() {
    2.   Column() {
    3.     // 反例：不允许使用switch语法
    4.     switch (expression) {
    5.       case 1:
    6.         Text('...')
    7.         break;
    8.       case 2:
    9.         Image('...')
    10.         break;
    11.       default:
    12.         Text('...')
    13.         break;
    14.     }
    15.     // 正例：使用if
    16.     if(expression == 1) {
    17.       Text('...')
    18.     } else if(expression == 2) {
    19.       Image('...')
    20.     } else {
    21.       Text('...')
    22.     }
    23.   }
    24. }
    
- 不允许使用表达式，请使用if组件，示例如下。
    
    1. build() {
    2.   Column() {
    3.     // 反例：不允许使用表达式
    4.     (this.aVar > 10) ? Text('...') : Image('...')
    
    5.     // 正例：使用if判断
    6.     if(this.aVar > 10) {
    7.       Text('...')
    8.     } else {
    9.       Image('...')
    10.     }
    11.   }
    12. }
    
- 不允许直接改变状态变量，反例如下。详细分析见[@State常见问题：不允许在build里改状态变量](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-state#%E4%B8%8D%E5%85%81%E8%AE%B8%E5%9C%A8build%E9%87%8C%E6%94%B9%E7%8A%B6%E6%80%81%E5%8F%98%E9%87%8F)。
    
    1. @Component
    2. struct MyComponent {
    3.   @State textColor: Color = Color.Yellow;
    4.   @State columnColor: Color = Color.Green;
    5.   @State count: number = 1;
    6.   build() {
    7.     Column() {
    8.       // 应避免直接在Text组件内改变count的值
    9.       Text(`${this.count++}`)
    10.         .width(50)
    11.         .height(50)
    12.         .fontColor(this.textColor)
    13.         .onClick(() => {
    14.           this.columnColor = Color.Red;
    15.         })
    16.       Button("change textColor").onClick(() =>{
    17.         this.textColor = Color.Pink;
    18.       })
    19.     }
    20.     .backgroundColor(this.columnColor)
    21.   }
    22. }
    
    在ArkUI状态管理中，状态驱动UI更新。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164009.92080870358361048152722759391511:50001231000000:2800:3B8012A18813A95600E1F3C5492A33989D554986C70F6D2357D1A896F2917CBE.png)
    
    所以，不能在自定义组件的build()或@Builder方法里直接改变状态变量，这可能会造成循环渲染的风险。Text('${this.count++}')在全量更新或最小化更新会产生不同的影响：
    
    - 全量更新（API8及以前版本）： ArkUI可能会陷入一个无限的重渲染的循环里，因为Text组件的每一次渲染都会改变应用的状态，就会再引起下一轮渲染的开启。 当 this.columnColor 更改时，都会执行整个build构建函数，因此，Text(${this.count++})绑定的文本也会更改，每次重新渲染Text(${this.count++})，又会使this.count状态变量更新，导致新一轮的build执行，从而陷入无限循环。
    - 最小化更新（API9及以上版本）：当this.columnColor更新时，仅Column组件更新，Text组件不会更新。只有当this.textColor更改时，会去更新整个Text组件，其所有属性函数都会执行，所以会看到Text(${this.count++})自增。因为目前UI以组件为单位进行更新，如果组件上某一个属性发生改变，会更新整个的组件。所以整体的更新链路是：this.textColor = Color.Pink ->Text组件整个更新->this.count++ ->Text组件整个更新。值得注意的是，这种写法在初次渲染时会导致Text组件渲染两次，影响性能。
    
    build函数中更改应用状态的行为可能比上面的示例更加隐蔽，例如：
    
    - 在@Builder，@Extend或@Styles方法内改变状态变量 。
        
    - 在计算参数时调用函数中改变应用状态变量，例如 Text('${this.calcLabel()}')。
        
    - 对当前数组做出修改，sort()改变了数组this.arr，随后的filter方法会返回一个新的数组。
        
        1. // 反例
        2. @State arr : Array<...> = [ ... ];
        3. ForEach(this.arr.sort().filter(...),
        4.   item => {
        5.   // ...
        6. })
        7. // 正确的执行方式为：filter返回一个新数组，后面的sort方法才不会改变原数组this.arr
        8. ForEach(this.arr.filter(...).sort(),
        9.   item => {
        10.   // ...
        11. })
        

## 自定义组件通用样式

自定义组件通过“.”链式调用设置通用样式。

1. @Component
2. struct ChildComponent {
3.   build() {
4.     Button(`Hello World`)
5.   }
6. }

7. @Entry
8. @Component
9. struct MyComponent {
10.   build() {
11.     Row() {
12.       ChildComponent()
13.         .width(200)
14.         .height(300)
15.         .backgroundColor(Color.Red)
16.     }
17.   }
18. }

说明

ArkUI给自定义组件设置样式时，相当于给ChildComponent套了一个不可见的容器组件，这些样式是设置在容器组件上，而非直接设置给ChildComponent的Button组件。渲染结果显示，背景颜色红色并没有直接设置到Button上，而是设置在Button所在的不可见容器组件上。
# 自定义组件生命周期

更新时间: 2025-12-16 16:40

自定义组件生命周期，即用[@Component](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components#component)或[@ComponentV2](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-componentv2)装饰的自定义组件的生命周期，提供以下生命周期接口：

- [aboutToAppear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttoappear)：组件即将出现时回调该接口，具体时机为在创建自定义组件的新实例后，在执行其build函数之前执行。
    
- [onDidBuild](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#ondidbuild12)：在组件首次渲染触发的build函数执行完成之后回调该接口，后续组件重新渲染将不回调该接口。开发者可以在这个阶段实现埋点数据上报等不影响实际UI的功能。
    
- [aboutToDisappear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttodisappear)：aboutToDisappear函数在自定义组件析构销毁之前执行。不允许在aboutToDisappear函数中改变状态变量，特别是@Link变量的修改可能会导致应用程序行为不稳定。
    

说明

页面生命周期及其相关内容参考[页面路由](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-routing#%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)。

自定义组件生命周期流程如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164022.95956784393937385641182391724380:50001231000000:2800:A1149043F523608139001259434577377D6B872A88E2BF3CDD36AE9B93BF7511.png)

根据上面的流程图，接下来从自定义组件的初始创建、重新渲染和删除来详细说明。

## 自定义组件的创建和渲染流程

1. 自定义组件的创建：自定义组件的实例由ArkUI框架创建。
    
2. 初始化自定义组件的成员变量：通过本地默认值或者构造方法传递参数来初始化自定义组件的成员变量，初始化顺序为成员变量的定义顺序。
    
3. 如果开发者定义了aboutToAppear，则执行build方法之前执行该方法。
    
4. 在首次渲染的时候，执行build方法渲染系统组件，如果子组件为自定义组件，则创建自定义组件的实例。在首次渲染的过程中，框架会记录状态变量和组件的映射关系，当状态变量改变时，驱动其相关的组件刷新。
    
5. 如果开发者定义了onDidBuild，则执行build方法之后执行该方法。
    

## 自定义组件重新渲染

当触发事件（比如点击）改变状态变量时，或者[LocalStorage](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-localstorage) / [AppStorage](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-appstorage)中的属性更改，并导致绑定的状态变量更改其值时：

1. 框架观察到变化，启动重新渲染。
    
2. 根据框架记录的状态变量和组件的映射关系，仅刷新发生变化的状态变量所关联的组件，实现最小化更新。
    

## 自定义组件的删除

例如if组件的分支改变或ForEach循环渲染中数组的个数改变，组件将被移除：

1. 在删除组件之前，将调用其aboutToDisappear生命周期函数，标记着该节点将要被销毁。ArkUI的节点删除机制是：后端节点直接从组件树上摘下，后端节点被销毁，对前端节点解引用，前端节点已经没有引用时，将被Ark虚拟机垃圾回收。
    
2. 自定义组件和它的变量将被删除，如果组件有同步的变量（如[@Link](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-link)、[@Prop](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-prop)、[@StorageLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-appstorage#storagelink)），将从[同步源](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-state-management-overview#%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5)上取消注册。
    

不建议在生命周期aboutToDisappear中使用async await。如果在此生命周期中使用异步操作（如 Promise 或回调方法），自定义组件将被保留在Promise的闭包中，直到回调方法执行完毕，这会阻止自定义组件的垃圾回收。

## 自定义组件嵌套使用与示例

通过以下示例，来详细说明自定义组件在嵌套使用时，自定义组件生命周期的调用时序：

1. // Index.ets
2. @Entry
3. @Component
4. struct Parent {
5.   @State showChild: boolean = true;
6.   @State btnColor: string = '#FF007DFF';

7.   // 组件生命周期
8.   aboutToAppear() {
9.     console.info('Parent aboutToAppear');
10.   }

11.   // 组件生命周期
12.   onDidBuild() {
13.     console.info('Parent onDidBuild');
14.   }

15.   // 组件生命周期
16.   aboutToDisappear() {
17.     console.info('Parent aboutToDisappear');
18.   }

19.   build() {
20.     Column() {
21.       // this.showChild为true，创建Child子组件，执行Child aboutToAppear
22.       if (this.showChild) {
23.         Child()
24.       }
25.       Button('delete Child')
26.         .margin(20)
27.         .backgroundColor(this.btnColor)
28.         .onClick(() => {
29.           // 更改this.showChild为false，删除Child子组件，执行Child aboutToDisappear
30.           // 更改this.showChild为true，添加Child子组件，执行Child aboutToAppear
31.           this.showChild = !this.showChild;
32.         })
33.     }
34.   }
35. }

36. @Component
37. struct Child {
38.   @State title: string = 'Hello World';

39.   // 组件生命周期
40.   aboutToDisappear() {
41.     console.info('Child aboutToDisappear');
42.   }

43.   // 组件生命周期
44.   onDidBuild() {
45.     console.info('Child onDidBuild');
46.   }

47.   // 组件生命周期
48.   aboutToAppear() {
49.     console.info('Child aboutToAppear');
50.   }

51.   build() {
52.     Text(this.title)
53.       .fontSize(50)
54.       .margin(20)
55.       .onClick(() => {
56.         this.title = 'Hello ArkUI';
57.       })
58.   }
59. }

以上示例中，Index页面包含两个自定义组件，一个是Parent，一个是Child，Parent及其子组件Child分别声明了各自的自定义组件生命周期函数（aboutToAppear / onDidBuild / aboutToDisappear）。

- 应用冷启动的初始化流程为：Parent aboutToAppear --> Parent build --> Parent onDidBuild --> Child aboutToAppear --> Child build --> Child onDidBuild。此处体现了自定义组件懒展开特性，即Parent执行完onDidBuild之后才会执行Child组件的aboutToAppear。日志输出信息如下：

1. Parent aboutToAppear
2. Parent onDidBuild
3. Child aboutToAppear
4. Child onDidBuild

- 点击Button按钮，更改showChild为false，删除Child组件，执行Child aboutToDisappear方法。
    
- 如果直接退出应用，则会触发以下生命周期：Parent aboutToDisappear --> Child aboutToDisappear，此处体现了自定义组件删除顺序也是从父到子。日志输出信息如下：
    

1. Parent aboutToDisappear
2. Child aboutToDisappear

- 最小化应用或者应用进入后台，当前Index页面未被销毁，所以并不会执行组件的aboutToDisappear。
    
- 如果showChild的默认值为false，则应用冷启动的初始化流程为：Parent aboutToAppear --> Parent build --> Parent onDidBuild。日志输出信息如下：
    

1. Parent aboutToAppear
2. Parent onDidBuild

- 如果showChild的默认值为false，直接退出应用，则只执行Parent aboutToDisappear方法。
    
- 如果showChild的默认值为false，此时点击Button按钮，更改showChild为true，添加Child组件，添加流程为：Child aboutToAppear --> Child build --> Child onDidBuild。日志输出信息如下：
    

1. Child aboutToAppear
2. Child onDidBuild

当showChild为默认值true时，该示例的生命周期流程图如下所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164022.52182549701542031189746922275793:50001231000000:2800:549F50279DB027DEEA7878FF368753F2D7742986C5419A3D59AA558A39D804C7.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components "创建自定义组件")
# 自定义组件的自定义布局

更新时间: 2025-12-16 16:40

如果系统提供的布局组件（如[Flex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-flex)，[Column](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-column)，[Row](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-row)等）无法满足复杂布局需求，或开发者希望自定义计算组件内子组件的大小和位置，建议在自定义组件中使用以下接口：

- [onMeasureSize](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-layout#onmeasuresize10)：组件每次布局时触发，开发者可以在这个回调中增加自定义组件内子组件的大小的计算逻辑，返回自定义组件的尺寸信息，其执行时间先于onPlaceChildren。
    
- [onPlaceChildren](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-layout#onplacechildren10)：组件每次布局时触发，开发者可以在这个回调中增加放置自定义组件内子组件位置的逻辑。
    

以下示例中，Index页面包含一个实现了自定义布局的自定义组件，且对应自定义组件的子组件通过index页面内的builder方式传入。

而在自定义组件中，调用了onMeasureSize和onPlaceChildren设置子组件大小和放置位置。例如，在本示例中，在onMeasureSize中初始化组件大小size=100，后续的每一个子组件size会加上上一个子组件大小的一半，实现组件大小递增的效果。而在onPlaceChildren中，定义startPos=300，设置每一个子组件的位置为startPos减去子组件自身的高度，所有子组件右下角一致在顶点位置(300, 300)，实现一个从右下角开始展示组件的类Stack组件。

**示例：**

1. // xxx.ets
2. @Entry
3. @Component
4. struct Index {
5.   build() {
6.     Column() {
7.       CustomLayout({ builder: ColumnChildren })
8.     }
9.   }
10. }

11. // 通过builder的方式传递多个组件，作为自定义组件的一级子组件（即不包含容器组件，如Column）
12. @Builder
13. function ColumnChildren() {
14.   ForEach([1, 2, 3], (index: number) => { // 暂不支持lazyForEach的写法
15.     Text('S' + index)
16.       .fontSize(30)
17.       .width(100)
18.       .height(100)
19.       .borderWidth(2)
20.       .offset({ x: 10, y: 20 })
21.   })
22. }

23. @Component
24. struct CustomLayout {
25.   @Builder
26.   doNothingBuilder() {
27.   };

28.   @BuilderParam builder: () => void = this.doNothingBuilder;
29.   @State startSize: number = 100;
30.   result: SizeResult = {
31.     width: 0,
32.     height: 0
33.   };

34.   // 第一步：计算各子组件的大小
35.   onMeasureSize(selfLayoutInfo: GeometryInfo, children: Array<Measurable>, constraint: ConstraintSizeOptions) {
36.     let size = 100;
37.     children.forEach((child) => {
38.       let result: MeasureResult = child.measure({ minHeight: size, minWidth: size, maxWidth: size, maxHeight: size })
39.       size += result.width / 2;
40.     })
41.     // this.result在该用例中代表自定义组件本身的大小，onMeasureSize方法返回的是组件自身的尺寸。
42.     this.result.width = 100;
43.     this.result.height = 400;
44.     return this.result;
45.   }
46.   // 第二步：放置各子组件的位置
47.   onPlaceChildren(selfLayoutInfo: GeometryInfo, children: Array<Layoutable>, constraint: ConstraintSizeOptions) {
48.     let startPos = 300;
49.     children.forEach((child) => {
50.       let pos = startPos - child.measureResult.height;
51.       child.layout({ x: pos, y: pos })
52.     })
53.   }

54.   build() {
55.     this.builder()
56.   }
57. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164034.25687620088850054917823160123744:50001231000000:2800:B3B2C81B965B253C665D6C0941DC243FB711649290E7F7FC1CF39FD93C9594A6.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-page-custom-components-lifecycle "自定义组件生命周期")
# 自定义组件成员属性访问限定符使用限制

更新时间: 2025-12-16 16:40

在状态管理V1版本中，完成自定义组件封装后，调用方难以明确知晓应传入哪些变量作为组件的输入参数。当组件开发者不希望状态变量被外部初始化时，可以使用private限定符来限制当前变量不允许被外部初始化。外部初始化也需要遵循装饰器自身的规则，具体规则见[使用限制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-custom-components-access-restrictions#%E4%BD%BF%E7%94%A8%E9%99%90%E5%88%B6)。

ArkTS会对自定义组件的成员变量使用的访问限定符private/public/protected进行校验，当不按规范使用访问限定符private/public/protected时，会产生对应的日志信息。

在阅读本文档前，建议提前阅读：[状态管理概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-state-management-overview)。

说明

从API version 12开始，支持自定义组件成员属性访问限定符使用限制的规则。

## 使用限制

- [@State](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-state)/[@Prop](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-prop)/[@Provide](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-provide-and-consume)/[@BuilderParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-builderparam)/常规成员变量(不涉及更新的普通变量)的初始化规则为可以被外部初始化，也可以使用本地值进行初始化。当组件开发者不希望当前变量被外部初始化时，可以使用private进行修饰，在这种情况下，错误进行外部初始化会有编译告警日志提示。
    
- [@StorageLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-appstorage#storagelink)/[@StorageProp](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-appstorage#storageprop)/[@LocalStorageLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-localstorage#localstoragelink)/[@LocalStorageProp](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-localstorage#localstorageprop)/[@Consume](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-provide-and-consume)变量的初始化规则为不可以被外部初始化，当组件开发者希望当前变量被外部初始化而使用public修饰时，与装饰器本身的初始化规则不符，会有编译告警日志提示。
    
- [@Link](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-link)/[@ObjectLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-observed-and-objectlink)变量的初始化规则为必须被外部初始化，禁止本地初始化。当组件开发者使用private对变量进行修饰时，与装饰器本身的初始化规则不符，会有编译告警日志提示。
    
- 由于struct没有继承能力，上述所有的这些变量使用protected修饰时，会有编译告警日志提示。
    
- [@Require](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-require)含义是当前被@Require装饰的变量必须被外部初始化，当@Require和private同时装饰[@State](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-state)/[@Prop](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-prop)/[@Provide](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-provide-and-consume)/[@BuilderParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-builderparam)/常规成员变量(不涉及更新的普通变量)时，他们的含义是自相矛盾的，会有编译告警日志提示。
    

## 使用场景

1. 当成员变量被private访问限定符和@State/@Prop/@Provide/@BuilderParam装饰器同时修饰，并且通过父组件进行初始化赋值，ArkTS会进行校验并产生告警日志。
    
    【反例】
    
    1. @Entry
    2. @Component
    3. struct AccessRestrictions {
    4.   @Builder
    5.   buildTest() {
    6.     Text('Parent builder')
    7.   }
    
    8.   build() {
    9.     Column() {
    10.       ComponentsChild({
    11.         state_value: 'Hello',
    12.         prop_value: 'Hello',
    13.         provide_value: 'Hello',
    14.         builder_value: this.buildTest,
    15.         regular_value: 'Hello'
    16.       })
    17.     }
    18.     .width('100%')
    19.   }
    20. }
    
    21. @Component
    22. struct ComponentsChild {
    23.   // 此处使用private修饰符时会出现告警日志
    24.   @State private state_value: string = 'Hello';
    25.   // 此处使用private修饰符时会出现告警日志
    26.   @Prop private prop_value: string = 'Hello';
    27.   // 此处使用private修饰符时会出现告警日志
    28.   @Provide private provide_value: string = 'Hello';
    29.   // 此处使用private修饰符时会出现告警日志
    30.   @BuilderParam private builder_value: () => void = this.buildTest;
    31.   // 此处使用private修饰符时会出现告警日志
    32.   private regular_value: string = 'Hello';
    
    33.   @Builder
    34.   buildTest() {
    35.     Text('Child builder')
    36.   }
    
    37.   build() {
    38.     Column() {
    39.       Text('Hello')
    40.         .fontSize(50)
    41.         .fontWeight(FontWeight.Bold)
    42.     }
    43.   }
    44. }
    
    编译告警日志如下：
    
    45. Property 'state_value' is private and can not be initialized through the component constructor.
    46. Property 'prop_value' is private and can not be initialized through the component constructor.
    47. Property 'provide_value' is private and can not be initialized through the component constructor.
    48. Property 'builder_value' is private and can not be initialized through the component constructor.
    49. Property 'regular_value' is private and can not be initialized through the component constructor.
    
    【正例】
    
    50. @Entry
    51. @Component
    52. struct AccessRestrictions {
    53.   @Builder
    54.   buildTest() {
    55.     Text('Parent builder')
    56.   }
    
    57.   build() {
    58.     Column() {
    59.       ComponentsChild({
    60.         state_value: 'Hello',
    61.         prop_value: 'Hello',
    62.         provide_value: 'Hello',
    63.         builder_value: this.buildTest,
    64.         regular_value: 'Hello'
    65.       })
    66.     }
    67.     .width('100%')
    68.   }
    69. }
    
    70. @Component
    71. struct ComponentsChild {
    72.   @State state_value: string = 'Hello';
    73.   @Prop prop_value: string = 'Hello';
    74.   @Provide provide_value: string = 'Hello';
    75.   @BuilderParam builder_value: () => void = this.buildTest;
    76.   regular_value: string = 'Hello';
    
    77.   @Builder
    78.   buildTest() {
    79.     Text('Child builder')
    80.   }
    
    81.   build() {
    82.     Column() {
    83.       Text('Hello')
    84.         .fontSize(50)
    85.         .fontWeight(FontWeight.Bold)
    86.     }
    87.   }
    88. }
    
2. 当成员变量被public访问限定符和@StorageLink/@StorageProp/@LocalStorageLink/@LocalStorageProp/@Consume装饰器同时修饰，并且通过父组件进行初始化赋值，ArkTS会进行校验并产生告警日志。
    
    【反例】
    
    1. @Entry
    2. @Component
    3. struct AccessRestrictions {
    4.   @Provide consume_value: string = 'Hello';
    5.   build() {
    6.     Column() {
    7.       ComponentChild()
    8.     }
    9.     .width('100%')
    10.   }
    11. }
    
    12. @Component
    13. struct ComponentChild {
    14.   // 此处使用public修饰符时会出现告警日志
    15.   @LocalStorageProp('sessionLocalProp') public local_prop_value: string = 'Hello';
    16.   // 此处使用public修饰符时会出现告警日志
    17.   @LocalStorageLink('sessionLocalLink') public local_link_value: string = 'Hello';
    18.   // 此处使用public修饰符时会出现告警日志
    19.   @StorageProp('sessionProp') public storage_prop_value: string = 'Hello';
    20.   // 此处使用public修饰符时会出现告警日志
    21.   @StorageLink('sessionLink') public storage_link_value: string = 'Hello';
    22.   // 此处使用public修饰符时会出现告警日志
    23.   @Consume public consume_value: string;
    
    24.   build() {
    25.     Column() {
    26.       Text('Hello')
    27.         .fontSize(50)
    28.         .fontWeight(FontWeight.Bold)
    29.     }
    30.   }
    31. }
    
    编译告警日志如下：
    
    32. Property 'local_prop_value' can not be decorated with both '@LocalStorageProp' and public.
    33. Property 'local_link_value' can not be decorated with both '@LocalStorageLink' and public.
    34. Property 'storage_prop_value' can not be decorated with both '@StorageProp' and public.
    35. Property 'storage_link_value' can not be decorated with both '@StorageLink' and public.
    36. Property 'consume_value' can not be decorated with both '@Consume' and public.
    
    【正例】
    
    37. @Entry
    38. @Component
    39. struct AccessRestrictions {
    40.   @Provide consume_value: string = 'Hello';
    41.   build() {
    42.     Column() {
    43.       ComponentChild()
    44.     }
    45.     .width('100%')
    46.   }
    47. }
    
    48. @Component
    49. struct ComponentChild {
    50.   @LocalStorageProp('sessionLocalProp') local_prop_value: string = 'Hello';
    51.   @LocalStorageLink('sessionLocalLink') local_link_value: string = 'Hello';
    52.   @StorageProp('sessionProp') storage_prop_value: string = 'Hello';
    53.   @StorageLink('sessionLink') storage_link_value: string = 'Hello';
    54.   @Consume consume_value: string;
    55.   build() {
    56.     Column() {
    57.       Text('Hello')
    58.         .fontSize(50)
    59.         .fontWeight(FontWeight.Bold)
    60.     }
    61.   }
    62. }
    
3. 当成员变量被private访问限定符和@Link/@ObjectLink装饰器同时修饰，并且通过父组件进行初始化赋值，ArkTS会进行校验并产生告警日志。
    
    【反例】
    
    1. @Entry
    2. @Component
    3. struct AccessRestrictions {
    4.   @State link_value: string = 'Hello';
    5.   @State objectLink_value: ComponentObj = new ComponentObj();
    6.   build() {
    7.     Column() {
    8.       ComponentChild({link_value: this.link_value, objectLink_value: this.objectLink_value})
    9.     }
    10.     .width('100%')
    11.   }
    12. }
    
    13. @Observed
    14. class ComponentObj {
    15.   count: number = 0;
    16. }
    17. @Component
    18. struct ComponentChild {
    19.   // 此处使用private修饰符时会出现告警日志
    20.   @Link private link_value: string;
    21.   // 此处使用private修饰符时会出现告警日志
    22.   @ObjectLink private objectLink_value: ComponentObj;
    23.   build() {
    24.     Column() {
    25.       Text('Hello')
    26.         .fontSize(50)
    27.         .fontWeight(FontWeight.Bold)
    28.     }
    29.   }
    30. }
    
    编译告警日志如下：
    
    31. Property 'link_value' can not be decorated with both '@Link' and private.
    32. Property 'objectLink_value' can not be decorated with both '@ObjectLink' and private.
    
    【正例】
    
    33. @Entry
    34. @Component
    35. struct AccessRestrictions {
    36.   @State link_value: string = 'Hello';
    37.   @State objectLink_value: ComponentObj = new ComponentObj();
    38.   build() {
    39.     Column() {
    40.       ComponentChild({link_value: this.link_value, objectLink_value: this.objectLink_value})
    41.     }
    42.     .width('100%')
    43.   }
    44. }
    
    45. @Observed
    46. class ComponentObj {
    47.   count: number = 0;
    48. }
    49. @Component
    50. struct ComponentChild {
    51.   @Link link_value: string;
    52.   @ObjectLink objectLink_value: ComponentObj;
    53.   build() {
    54.     Column() {
    55.       Text('Hello')
    56.         .fontSize(50)
    57.         .fontWeight(FontWeight.Bold)
    58.     }
    59.   }
    60. }
    
4. 当成员变量被protected访问限定符修饰，并且通过父组件进行初始化赋值，ArkTS会进行校验并产生告警日志。
    
    【反例】
    
    1. @Entry
    2. @Component
    3. struct AccessRestrictions {
    4.   build() {
    5.     Column() {
    6.       ComponentChild({regular_value: 'Hello'})
    7.     }
    8.     .width('100%')
    9.   }
    10. }
    
    11. @Component
    12. struct ComponentChild {
    13.   // 此处使用protected修饰符时会出现告警日志
    14.   protected regular_value: string = 'Hello';
    15.   build() {
    16.     Column() {
    17.       Text('Hello')
    18.         .fontSize(50)
    19.         .fontWeight(FontWeight.Bold)
    20.     }
    21.   }
    22. }
    
    编译告警日志如下：
    
    23. The member attributes of a struct can not be protected.
    
    【正例】
    
    24. @Entry
    25. @Component
    26. struct AccessRestrictions {
    27.   build() {
    28.     Column() {
    29.       ComponentChild({regular_value: 'Hello'})
    30.     }
    31.     .width('100%')
    32.   }
    33. }
    
    34. @Component
    35. struct ComponentChild {
    36.   regular_value: string = 'Hello';
    37.   build() {
    38.     Column() {
    39.       Text('Hello')
    40.         .fontSize(50)
    41.         .fontWeight(FontWeight.Bold)
    42.     }
    43.   }
    44. }
    
5. 当成员变量被private访问限定符、@Require和@State/@Prop/@Provide/@BuilderParam装饰器同时修饰，并且通过父组件初始化赋值时，ArkTS会进行校验并产生告警日志。
    
    【反例】
    
    1. @Entry
    2. @Component
    3. struct AccessRestrictions {
    4.   build() {
    5.     Column() {
    6.       ComponentChild({prop_value: 'Hello'})
    7.     }
    8.     .width('100%')
    9.   }
    10. }
    11. @Component
    12. struct ComponentChild {
    13.   // 此处使用private修饰符时会出现告警日志
    14.   @Require @Prop private prop_value: string = 'Hello';
    15.   build() {
    16.     Column() {
    17.       Text('Hello')
    18.         .fontSize(50)
    19.         .fontWeight(FontWeight.Bold)
    20.     }
    21.   }
    22. }
    
    编译告警日志如下：
    
    1. Property 'prop_value' can not be decorated with both '@Require' and private.
    2. Property 'prop_value' is private and can not be initialized through the component constructor.
    
    【正例】
    
    1. @Entry
    2. @Component
    3. struct AccessRestrictions {
    4.   build() {
    5.     Column() {
    6.       ComponentChild({prop_value: 'Hello'})
    7.     }
    8.     .width('100%')
    9.   }
    10. }
    11. @Component
    12. struct ComponentChild {
    13.   @Require @Prop prop_value: string = 'Hello';
    14.   build() {
    15.     Column() {
    16.       Text('Hello')
    17.         .fontSize(50)
    18.         .fontWeight(FontWeight.Bold)
    19.     }
    20.   }
    21. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-page-custom-components-layout "自定义组件的自定义布局")
# @Styles装饰器：定义组件重用样式

更新时间: 2025-12-16 16:39

如果每个组件的样式都需要单独设置，在开发过程中会出现大量代码在进行重复样式设置，虽然可以复制粘贴，但为了代码简洁性和后续方便维护，我们推出了可以提炼公共样式进行复用的装饰器@Styles。

@Styles装饰器可以将多条样式设置提炼成一个方法，直接在组件声明的位置调用。通过@Styles装饰器可以快速定义并复用自定义样式。

说明

从API version 9开始，该装饰器支持在ArkTS卡片中使用。

从API version 11开始，该装饰器支持在元服务中使用。

## 装饰器使用说明

- 当前@Styles仅支持[通用属性](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-component-general-attributes)和[通用事件](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-component-general-events)。
    
- @Styles可以定义在组件内或全局，在全局定义时需在方法名前面添加function关键字，组件内定义时则不需要添加function关键字。请参考用例[组件内styles和全局styles的用法](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-style#%E7%BB%84%E4%BB%B6%E5%86%85styles%E5%92%8C%E5%85%A8%E5%B1%80styles%E7%9A%84%E7%94%A8%E6%B3%95)。
    
- 组件内@Styles的优先级高于全局@Styles。框架优先找当前组件内的@Styles，如果找不到，则会全局查找。
    

说明

只能在当前文件内使用@Styles，不支持export。

若需要实现样式导出，推荐使用[AttributeModifier](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-user-defined-extension-attributemodifier)。

定义在组件内的@Styles可以通过this访问组件的常量和状态变量，并可以在@Styles里通过事件来改变状态变量的值，示例如下：

1. @Entry
2. @Component
3. struct FancyUse {
4.   @State heightValue: number = 50;

5.   @Styles
6.   fancy() {
7.     .height(this.heightValue)
8.     .backgroundColor(Color.Blue)
9.     .onClick(() => {
10.       this.heightValue = 100;
11.     })
12.   }

13.   build() {
14.     Column() {
15.       Button('change height')
16.         .fancy()
17.     }
18.     .height('100%')
19.     .width('100%')
20.   }
21. }

## 限制条件

- @Styles方法不能有参数，编译期会报错，表明@Styles方法不支持参数。

1. // 错误写法： @Styles不支持参数，编译期报错
2. @Styles
3. function globalFancy (value: number) {
4.   .width(value)
5. }

6. // 正确写法
7. @Styles
8. function globalFancy () {
9.   .width(100)
10. }

- 不支持在@Styles方法内使用逻辑组件，逻辑组件内的属性不生效。

1. // 错误写法
2. @Styles
3. function backgroundColorStyle() {
4.   if (true) {
5.     .backgroundColor(Color.Red)
6.   }
7. }

8. // 正确写法
9. @Styles
10. function backgroundColorStyle() {
11.   .backgroundColor(Color.Red)
12. }

## 使用场景

### 组件内@Styles和全局@Styles的用法

1. // 定义在全局的@Styles封装的样式
2. @Styles
3. function globalFancy () {
4.   .width(150)
5.   .height(100)
6.   .backgroundColor(Color.Pink)
7. }

8. @Entry
9. @Component
10. struct FancyUse {
11.   @State heightValue: number = 100;
12.   // 定义在组件内的@Styles封装的样式
13.   @Styles fancy() {
14.     .width(200)
15.     .height(this.heightValue)
16.     .backgroundColor(Color.Yellow)
17.     .onClick(() => {
18.       this.heightValue = 200;
19.     })
20.   }

21.   build() {
22.     Column({ space: 10 }) {
23.       // 使用全局的@Styles封装的样式
24.       Text('FancyA')
25.         .globalFancy()
26.         .fontSize(30)
27.       // 使用组件内的@Styles封装的样式
28.       Text('FancyB')
29.         .fancy()
30.         .fontSize(30)
31.     }
32.   }
33. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-wrapbuilder "wrapBuilder：封装全局@Builder")
# @Extend装饰器：定义扩展组件样式

更新时间: 2025-12-16 16:39

在前文的示例中，可以使用[@Styles](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-style)用于样式的重用，在@Styles的基础上，我们提供了@Extend，用于扩展组件样式。

说明

从API version 9开始，该装饰器支持在ArkTS卡片中使用。

从API version 11开始，该装饰器支持在元服务中使用。

## 装饰器使用说明

### 语法

1. @Extend(UIComponentName) function functionName { ... }

### 使用规则

- 和@Styles不同，@Extend支持封装指定组件的私有属性、私有事件和自身定义的全局方法。
    
    1. // @Extend(Text)可以支持Text的私有属性fontColor
    2. @Extend(Text)
    3. function fancy() {
    4.   .fontColor(Color.Red)
    5. }
    
    6. // superFancyText可以调用预定义的fancy
    7. @Extend(Text)
    8. function superFancyText(size: number) {
    9.   .fontSize(size)
    10.   .fancy()
    11. }
    
- 和@Styles不同，@Extend装饰的方法支持参数，开发者可以在调用时传递参数，调用遵循TS方法传值调用。
    
    1. // xxx.ets
    2. @Extend(Text)
    3. function fancy(fontSize: number) {
    4.   .fontColor(Color.Red)
    5.   .fontSize(fontSize)
    6. }
    
    7. @Entry
    8. @Component
    9. struct FancyUse {
    10.   build() {
    11.     Row({ space: 10 }) {
    12.       Text('Fancy')
    13.         .fancy(16)
    14.       Text('Fancy')
    15.         .fancy(24)
    16.     }
    17.   }
    18. }
    
- @Extend装饰的方法的参数可以为function，作为Event事件的句柄。
    
    1. @Extend(Text)
    2. function makeMeClick(onClick: () => void) {
    3.   .backgroundColor(Color.Blue)
    4.   .onClick(onClick)
    5. }
    
    6. @Entry
    7. @Component
    8. struct FancyUse {
    9.   @State label: string = 'Hello World';
    
    10.   onClickHandler() {
    11.     this.label = 'Hello ArkUI';
    12.   }
    
    13.   build() {
    14.     Row({ space: 10 }) {
    15.       Text(`${this.label}`)
    16.         .makeMeClick(() => {
    17.           this.onClickHandler();
    18.         })
    19.     }
    20.   }
    21. }
    
- @Extend的参数可以为[状态变量](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-state-management-overview)，当状态变量改变时，UI可以正常的被刷新渲染。
    
    1. @Extend(Text)
    2. function fancy(fontSize: number) {
    3.   .fontColor(Color.Red)
    4.   .fontSize(fontSize)
    5. }
    
    6. @Entry
    7. @Component
    8. struct FancyUse {
    9.   @State fontSizeValue: number = 20;
    
    10.   build() {
    11.     Row({ space: 10 }) {
    12.       Text('Fancy')
    13.         .fancy(this.fontSizeValue)
    14.         .onClick(() => {
    15.           this.fontSizeValue = 30;
    16.         })
    17.     }
    18.   }
    19. }
    

## 限制条件

- 和@Styles不同，@Extend仅支持在全局定义，不支持在组件内部定义。

说明

仅限在当前文件内使用，不支持导出。

如果要实现export功能，推荐使用[AttributeModifier](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-user-defined-extension-attributemodifier)。

【反例】

1. @Entry
2. @Component
3. struct FancyUse {
4.   // 错误写法，@Extend仅支持在全局定义，不支持在组件内部定义
5.   @Extend(Text) function fancy (fontSize: number) {
6.     .fontSize(fontSize)
7.   }

8.   build() {
9.     Row({ space: 10 }) {
10.       Text('Fancy')
11.         .fancy(16)
12.     }
13.   }
14. }

【正例】

1. // 正确写法
2. @Extend(Text)
3. function fancy(fontSize: number) {
4.   .fontSize(fontSize)
5. }

6. @Entry
7. @Component
8. struct FancyUse {
9.   build() {
10.     Row({ space: 10 }) {
11.       Text('Fancy')
12.         .fancy(16)
13.     }
14.   }
15. }

## 使用场景

以下示例声明了3个Text组件，每个Text组件均设置了fontStyle、fontWeight和backgroundColor样式。

1. @Entry
2. @Component
3. struct FancyUse {
4.   @State label: string = 'Hello World';

5.   build() {
6.     Row({ space: 10 }) {
7.       Text(`${this.label}`)
8.         .fontStyle(FontStyle.Italic)
9.         .fontWeight(100)
10.         .backgroundColor(Color.Blue)
11.       Text(`${this.label}`)
12.         .fontStyle(FontStyle.Italic)
13.         .fontWeight(200)
14.         .backgroundColor(Color.Pink)
15.       Text(`${this.label}`)
16.         .fontStyle(FontStyle.Italic)
17.         .fontWeight(300)
18.         .backgroundColor(Color.Orange)
19.     }.margin('20%')
20.   }
21. }

使用@Extend将样式组合复用，示例如下。

1. @Extend(Text)
2. function fancyText(weightValue: number, color: Color) {
3.   .fontStyle(FontStyle.Italic)
4.   .fontWeight(weightValue)
5.   .backgroundColor(color)
6. }

通过@Extend组合样式后，使得代码更加简洁，增强可读性。

1. @Entry
2. @Component
3. struct FancyUse {
4.   @State label: string = 'Hello World';

5.   build() {
6.     Row({ space: 10 }) {
7.       Text(`${this.label}`)
8.         .fancyText(100, Color.Blue)
9.       Text(`${this.label}`)
10.         .fancyText(200, Color.Pink)
11.       Text(`${this.label}`)
12.         .fancyText(300, Color.Orange)
13.     }.margin('20%')
14.   }
15. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-style "@Styles装饰器：定义组件重用样式")
# stateStyles：多态样式

更新时间: 2025-12-16 16:40

@Styles仅应用于静态页面的样式复用，stateStyles可以依据组件的内部状态的不同，快速设置不同样式。这就是我们本章要介绍的内容stateStyles（又称为：多态样式）。

说明

多态样式仅支持通用属性。如果多态样式不生效，则该属性可能为组件的私有属性，例如：[fontColor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-text-style)、[TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput)组件的[backgroundColor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-background)等。此时，可以通过[attributeModifier](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-attribute-modifier#attributemodifier)动态设置组件属性来解决此问题。

## 概述

stateStyles是属性方法，可以根据UI内部状态来设置样式，类似于css伪类，但语法不同。ArkUI提供以下六种状态：

- focused：获焦态。
    
- normal：正常态。
    
- pressed：按压态。
    
- disabled：不可用态。
    
- clicked：点击态。
    
- selected10+：选中态。
    

说明

获焦态目前仅支持通过外接键盘的Tab键或方向键触发，不支持在嵌套滚动组件场景下通过按键触发。

## 使用场景

### 基础场景

下面的示例展示了stateStyles最基本的使用场景。Button1处于第一个组件，Button2处于第二个组件。按压时显示为pressed态指定的黑色。使用Tab键走焦，Button1获焦并显示为focused态指定的粉色。当Button2获焦的时候，Button2显示为focused态指定的粉色，Button1失焦显示normal态指定的蓝色。

1. @Entry
2. @Component
3. struct StateStylesSample {
4.   build() {
5.     Column() {
6.       Button('Button1')
7.         .stateStyles({
8.           focused: {
9.             .backgroundColor('#ffffeef0')
10.           },
11.           pressed: {
12.             .backgroundColor('#ff707070')
13.           },
14.           normal: {
15.             .backgroundColor('#ff2787d9')
16.           }
17.         })
18.         .margin(20)
19.       Button('Button2')
20.         .stateStyles({
21.           focused: {
22.             .backgroundColor('#ffffeef0')
23.           },
24.           pressed: {
25.             .backgroundColor('#ff707070')
26.           },
27.           normal: {
28.             .backgroundColor('#ff2787d9')
29.           }
30.         })
31.     }.margin('30%')
32.   }
33. }

**图1** 获焦态和按压态

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164004.58609718392067532302358987903723:50001231000000:2800:42CAA085A078C41FC3E01C641A762E7A5DDD14AB00F4D20CA987707854752D32.gif)

### @Styles和stateStyles联合使用

以下示例通过@Styles指定stateStyles的不同状态。

1. @Entry
2. @Component
3. struct MyComponent {
4.   @Styles normalStyle() {
5.     .backgroundColor(Color.Gray)
6.   }

7.   @Styles pressedStyle() {
8.     .backgroundColor(Color.Red)
9.   }

10.   build() {
11.     Column() {
12.       Text('Text1')
13.         .fontSize(50)
14.         .fontColor(Color.White)
15.         .stateStyles({
16.           normal: this.normalStyle,
17.           pressed: this.pressedStyle,
18.         })
19.     }
20.   }
21. }

**图2** 正常态和按压态

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164004.53013930624240574944207561807220:50001231000000:2800:79D6E2E99246DD5C61F547A8A86D544AAF84B18F1F33ABEE92A67E4ECA87970D.gif)

### 在stateStyles里使用常规变量和状态变量

stateStyles可以通过this绑定组件内的常规变量和状态变量。

1. @Entry
2. @Component
3. struct CompWithInlineStateStyles {
4.   @State focusedColor: Color = 0xD5D5D5;
5.   normalColor: Color = 0x004AAF;

6.   build() {
7.     Column() {
8.       Button('clickMe')
9.         .height(100)
10.         .width(100)
11.         .stateStyles({
12.           normal: {
13.             .backgroundColor(this.normalColor)
14.           },
15.           focused: {
16.             .backgroundColor(this.focusedColor)
17.           }
18.         })
19.         .onClick(() => {
20.           this.focusedColor = 0x707070;
21.         })
22.         .margin('30%')
23.     }
24.   }
25. }

Button默认normal态显示蓝色，第一次按下Tab键让Button获焦显示为focus态的浅灰色，点击事件触发后，再次按下Tab键让Button获焦，focus态变为深灰色。

**图3** 点击改变获焦态样式

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164004.51151388705586636318193697166878:50001231000000:2800:2E061E2F10CCA856D4C9D3E0C5C8B260D04E26FDBC775FD02B685D66F868BA43.gif)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-extend "@Extend装饰器：定义扩展组件样式")
# @AnimatableExtend装饰器：定义可动画属性

更新时间: 2025-12-16 16:40

@AnimatableExtend装饰器用于自定义可动画的属性方法，在这个属性方法中修改组件不可动画的属性。在动画执行过程中，通过逐帧回调函数修改不可动画属性值，让不可动画属性也能实现动画效果。也可通过逐帧回调函数修改可动画属性的值，实现逐帧布局的效果。

- 可动画属性：如果一个属性方法在animation属性前调用，改变这个属性的值可以使animation属性的动画效果生效，这个属性称为可动画属性。比如height、width、backgroundColor、translate属性，和Text组件的fontSize属性等。
    
- 不可动画属性：如果一个属性方法在animation属性前调用，改变这个属性的值不能使animation属性的动画效果生效，这个属性称为不可动画属性。比如Polyline组件的points属性等。
    

说明

该装饰器从API version 10开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。

从API version 11开始，该装饰器支持在元服务中使用。

## 装饰器使用说明

### 语法

1. @AnimatableExtend(UIComponentName) function functionName(value: typeName) {
2.   .propertyName(value)
3. }

- @AnimatableExtend仅支持定义在全局，不支持在组件内部定义。
- @AnimatableExtend定义的函数参数类型必须为number类型或者实现 AnimatableArithmetic<T>接口的自定义类型。
- @AnimatableExtend定义的函数体内只能调用@AnimatableExtend括号内组件的属性方法。

### AnimatableArithmetic<T>接口说明

该接口定义非number数据类型的动画运算规则。对非number类型的数据（如数组、结构体、颜色等）做动画，需要实现AnimatableArithmetic<T>接口中加法、减法、乘法和判断相等函数，

使得该数据能参与动画的插值运算和识别该数据是否发生改变。即定义它们为实现了AnimatableArithmetic<T>接口的类型。

|名称|入参类型|返回值类型|说明|
|:--|:--|:--|:--|
|plus|AnimatableArithmetic<T>|AnimatableArithmetic<T>|定义该数据类型的加法运算规则|
|subtract|AnimatableArithmetic<T>|AnimatableArithmetic<T>|定义该数据类型的减法运算规则|
|multiply|number|AnimatableArithmetic<T>|定义该数据类型的乘法运算规则|
|equals|AnimatableArithmetic<T>|boolean|定义该数据类型的相等判断规则|

## 使用场景

以下示例通过改变Text组件宽度实现逐帧布局的效果。

1. @AnimatableExtend(Text)
2. function animatableWidth(width: number) {
3.   .width(width)
4. }

5. @Entry
6. @Component
7. struct AnimatablePropertyExample {
8.   @State textWidth: number = 80;

9.   build() {
10.     Column() {
11.       Text("AnimatableProperty")
12.         .animatableWidth(this.textWidth)
13.         .animation({ duration: 2000, curve: Curve.Ease })
14.       Button("Play")
15.         .onClick(() => {
16.           this.textWidth = this.textWidth == 80 ? 160 : 80;
17.         })
18.     }.width("100%")
19.     .padding(10)
20.   }
21. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164005.47421154328893857725333044561371:50001231000000:2800:E667200FF95095D6E538ECC5165B5DAF8434C918F094318E0148151B90B34202.gif)

以下示例实现折线的动画效果。

1. class Point {
2.   x: number
3.   y: number

4.   constructor(x: number, y: number) {
5.     this.x = x
6.     this.y = y
7.   }

8.   plus(rhs: Point): Point {
9.     return new Point(this.x + rhs.x, this.y + rhs.y);
10.   }

11.   subtract(rhs: Point): Point {
12.     return new Point(this.x - rhs.x, this.y - rhs.y);
13.   }

14.   multiply(scale: number): Point {
15.     return new Point(this.x * scale, this.y * scale);
16.   }

17.   equals(rhs: Point): boolean {
18.     return this.x === rhs.x && this.y === rhs.y;
19.   }
20. }

21. // PointVector实现了AnimatableArithmetic<T>接口
22. class PointVector extends Array<Point> implements AnimatableArithmetic<PointVector> {
23.   constructor(value: Array<Point>) {
24.     super();
25.     value.forEach(p => this.push(p));
26.   }

27.   plus(rhs: PointVector): PointVector {
28.     let result = new PointVector([]);
29.     const len = Math.min(this.length, rhs.length);
30.     for (let i = 0; i < len; i++) {
31.       result.push((this as Array<Point>)[i].plus((rhs as Array<Point>)[i]));
32.     }
33.     return result;
34.   }

35.   subtract(rhs: PointVector): PointVector {
36.     let result = new PointVector([]);
37.     const len = Math.min(this.length, rhs.length);
38.     for (let i = 0; i < len; i++) {
39.       result.push((this as Array<Point>)[i].subtract((rhs as Array<Point>)[i]));
40.     }
41.     return result;
42.   }

43.   multiply(scale: number): PointVector {
44.     let result = new PointVector([]);
45.     for (let i = 0; i < this.length; i++) {
46.       result.push((this as Array<Point>)[i].multiply(scale));
47.     }
48.     return result;
49.   }

50.   equals(rhs: PointVector): boolean {
51.     if (this.length != rhs.length) {
52.       return false;
53.     }
54.     for (let i = 0; i < this.length; i++) {
55.       if (!(this as Array<Point>)[i].equals((rhs as Array<Point>)[i])) {
56.         return false;
57.       }
58.     }
59.     return true;
60.   }

61.   get(): Array<Object[]> {
62.     let result: Array<Object[]> = [];
63.     this.forEach(p => result.push([p.x, p.y]));
64.     return result;
65.   }
66. }

67. @AnimatableExtend(Polyline)
68. function animatablePoints(points: PointVector) {
69.   .points(points.get())
70. }

71. @Entry
72. @Component
73. struct AnimatablePropertyExample {
74.   @State points: PointVector = new PointVector([
75.     new Point(50, Math.random() * 200),
76.     new Point(100, Math.random() * 200),
77.     new Point(150, Math.random() * 200),
78.     new Point(200, Math.random() * 200),
79.     new Point(250, Math.random() * 200),
80.   ])

81.   build() {
82.     Column() {
83.       Polyline()
84.         .animatablePoints(this.points)
85.         .animation({ duration: 1000, curve: Curve.Ease })// 设置动画参数
86.         .size({ height: 220, width: 300 })
87.         .fill(Color.Green)
88.         .stroke(Color.Red)
89.         .backgroundColor('#eeaacc')
90.       Button("Play")
91.         .onClick(() => {
92.           // points是实现了可动画协议的数据类型，points在动画过程中可按照定义的运算规则、动画参数从之前的PointVector变为新的PointVector数据，产生每一帧的PointVector数据，进而产生动画
93.           this.points = new PointVector([
94.             new Point(50, Math.random() * 200),
95.             new Point(100, Math.random() * 200),
96.             new Point(150, Math.random() * 200),
97.             new Point(200, Math.random() * 200),
98.             new Point(250, Math.random() * 200),
99.           ]);
100.         })
101.     }.width("100%")
102.     .padding(10)
103.   }
104. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164005.10663038976468191984243252585365:50001231000000:2800:00D6AA57D812BC18097AD5B83E12A8DE9D530DA1506DFB46F0E8B998DB629AC8.gif)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-statestyles "stateStyles：多态样式")
# @Require装饰器：校验构造传参

更新时间: 2025-12-16 16:40

@Require是校验@Prop、@State、@Provide、@BuilderParam、@Param和普通变量(无状态装饰器修饰的变量)是否需要构造传参的一个装饰器。

说明

从API version 11开始对@Prop/@BuilderParam进行校验。

从API version 11开始，该装饰器支持在ArkTS卡片中使用。

从API version 11开始，该装饰器支持在元服务中使用。

从API version 12开始对@State/@Provide/@Param/普通变量(无状态装饰器修饰的变量)进行校验。

## 概述

当@Require装饰器和[@Prop](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-prop)、[@State](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-state)、[@Provide](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-provide-and-consume)、[@Param](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-param)、[@BuilderParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-builderparam)、普通变量(无状态装饰器修饰的变量)结合使用时，在构造该自定义组件时，@Prop、@State、@Provide、@Param、@BuilderParam和普通变量(无状态装饰器修饰的变量)必须在构造时传参。

## 限制条件

@Require装饰器仅用于装饰struct内的@Prop、@State、@Provide、@BuilderParam、@Param和普通变量(无状态装饰器修饰的变量)。

预览器的限制场景请参考[PreviewChecker检测规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-previewer-previewchecker-V5)。

## 使用场景

当Child组件内使用@Require装饰器和@Prop、@State、@Provide、@BuilderParam、@Param和普通变量(无状态装饰器修饰的变量)结合使用时，父组件Index在构造Child时必须传参，否则编译不通过。

1. @Entry
2. @Component
3. struct Index {
4.   @State message: string = 'Hello World';

5.   @Builder
6.   buildTest() {
7.     Row() {
8.       Text('Hello, world')
9.         .fontSize(30)
10.     }
11.   }

12.   build() {
13.     Row() {
14.       // 构造Child时需传入所有@Require对应参数，否则编译失败。
15.       Child({
16.         regular_value: this.message,
17.         state_value: this.message,
18.         provide_value: this.message,
19.         initMessage: this.message,
20.         message: this.message,
21.         buildTest: this.buildTest,
22.         initBuildTest: this.buildTest
23.       })
24.     }
25.   }
26. }

27. @Component
28. struct Child {
29.   @Builder
30.   buildFunction() {
31.     Column() {
32.       Text('initBuilderParam')
33.         .fontSize(30)
34.     }
35.   }

36.   @Require regular_value: string = 'Hello';
37.   @Require @State state_value: string = 'Hello';
38.   @Require @Provide provide_value: string = 'Hello';
39.   @Require @BuilderParam buildTest: () => void;
40.   @Require @BuilderParam initBuildTest: () => void = this.buildFunction;
41.   @Require @Prop initMessage: string = 'Hello';
42.   @Require @Prop message: string;

43.   build() {
44.     Column() {
45.       Text(this.initMessage)
46.         .fontSize(30)
47.       Text(this.message)
48.         .fontSize(30)
49.       this.initBuildTest();
50.       this.buildTest();
51.     }
52.     .width('100%')
53.     .height('100%')
54.   }
55. }

使用[@ComponentV2](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-componentv2)修饰的自定义组件ChildPage通过父组件ParentPage进行初始化，因为有@Require装饰@Param，所以父组件必须进行构造赋值。

1. @ObservedV2
2. class Info {
3.   @Trace name: string = '';
4.   @Trace age: number = 0;
5. }

6. @ComponentV2
7. struct ChildPage {
8.   @Require @Param childInfo: Info = new Info();
9.   @Require @Param state_value: string = 'Hello';

10.   build() {
11.     Column() {
12.       Text(`ChildPage childInfo name :${this.childInfo.name}`)
13.         .fontSize(20)
14.         .fontWeight(FontWeight.Bold)
15.       Text(`ChildPage childInfo age :${this.childInfo.age}`)
16.         .fontSize(20)
17.         .fontWeight(FontWeight.Bold)
18.       Text(`ChildPage state_value age :${this.state_value}`)
19.         .fontSize(20)
20.         .fontWeight(FontWeight.Bold)
21.     }
22.   }
23. }

24. @Entry
25. @ComponentV2
26. struct ParentPage {
27.   info1: Info = { name: 'Tom', age: 25 };
28.   label1: string = 'Hello World';
29.   @Local info2: Info = { name: 'Tom', age: 25 };
30.   @Local label2: string = 'Hello World';

31.   build() {
32.     Column() {
33.       Text(`info1: ${this.info1.name}  ${this.info1.age}`) // Text1
34.         .fontSize(30)
35.         .fontWeight(FontWeight.Bold)
36.       // 父组件ParentPage构造子组件ChildPage时进行了构造赋值。
37.       // 为ChildPage中被@Require @Param装饰的childInfo和state_value属性传入了值。
38.       ChildPage({ childInfo: this.info1, state_value: this.label1 }) // 创建自定义组件。
39.       Line()
40.         .width('100%')
41.         .height(5)
42.         .backgroundColor('#000000').margin(10)
43.       Text(`info2: ${this.info2.name}  ${this.info2.age}`) // Text2。
44.         .fontSize(30)
45.         .fontWeight(FontWeight.Bold)
46.       // 同上，在父组件创建子组件的过程中进行构造赋值。
47.       ChildPage({ childInfo: this.info2, state_value: this.label2 }) // 创建自定义组件。
48.       Line()
49.         .width('100%')
50.         .height(5)
51.         .backgroundColor('#000000').margin(10)
52.       Button('change info1&info2')
53.         .onClick(() => {
54.           this.info1 = { name: 'Cat', age: 18 }; // Text1不会刷新，原因是info1没有装饰器装饰，监听不到值的改变。
55.           this.info2 = { name: 'Cat', age: 18 }; // Text2会刷新，原因是info2有装饰器装饰，能够监听到值的改变。
56.           this.label1 = 'Luck'; // 不会刷新，原因是label1没有装饰器装饰，监听不到值的改变。
57.           this.label2 = 'Luck'; // 会刷新，原因是label2有装饰器装饰，可以监听到值的改变。
58.         })
59.     }
60.   }
61. }

从API version 18开始，使用@Require装饰@State、@Prop、@Provide装饰的状态变量，可以在无本地初始值的情况下直接在组件内使用，不会编译报错。

1. @Entry
2. @Component
3. struct Index {
4.   message: string = 'Hello World';

5.   build() {
6.     Column() {
7.       Child({ message: this.message })
8.     }
9.   }
10. }

11. @Component
12. struct Child {
13.   @Require @State message: string;

14.   build() {
15.     Column() {
16.       Text(this.message) // 从API version 18开始，可以编译通过。
17.     }
18.   }
19. }

## 常见问题

当Child组件内将@Require装饰器与@Prop、@State、@Provide、@BuilderParam、普通变量（无状态装饰器修饰的变量）结合使用时，若父组件Index在构造Child时未传递相应参数，则会导致编译失败。当ChildV2组件内将@Require装饰器与@Param结合使用时，若父组件Index在构造ChildV2时未传递相应参数，则同样会导致编译失败。

【反例】

1. @Entry
2. @Component
3. struct Index {
4.   @State message: string = 'Hello World!';

5.   @Builder
6.   buildTest() {
7.     Row() {
8.       Text('Hello, world!!')
9.         .fontSize(30)
10.     }
11.   }

12.   build() {
13.     Row() {
14.       // 构造Child、ChildV2组件时没有传参，会导致编译不通过。
15.       Child()
16.       ChildV2()
17.     }
18.   }
19. }

20. @Component
21. struct Child {
22.   @Builder
23.   buildFunction() {
24.     Column() {
25.       Text('initBuilderParam')
26.         .fontSize(30)
27.     }
28.   }

29.   // 使用@Require必须构造时传参。
30.   @Require regular_value: string = 'Hello';
31.   @Require @State state_value: string = 'Hello';
32.   @Require @Provide provide_value: string = 'Hello';
33.   @Require @BuilderParam initBuildTest: () => void = this.buildFunction;
34.   @Require @Prop initMessage: string = 'Hello';

35.   build() {
36.     Column() {
37.       Text(this.initMessage)
38.         .fontSize(30)
39.       this.initBuildTest();
40.     }
41.   }
42. }

43. @ComponentV2
44. struct ChildV2 {
45.   // 使用@Require必须构造时传参。
46.   @Require @Param message: string;

47.   build() {
48.     Column() {
49.       Text(this.message)
50.     }
51.   }
52. }

当父组件Index在构造Child与ChildV2时传递了相应的参数，则编译通过。

【正例】

1. @Entry
2. @Component
3. struct Index {
4.   @State message: string = 'Hello World!';

5.   @Builder
6.   buildTest() {
7.     Row() {
8.       Text('Hello, world!!')
9.         .fontSize(30)
10.     }
11.   }

12.   build() {
13.     Row() {
14.       // 构造Child、ChildV2组件时传递相应参数，编译通过。
15.       Child({
16.         regular_value: 'Hello',
17.         state_value: 'Hello',
18.         provide_value: 'Hello',
19.         initBuildTest: this.buildTest,
20.         initMessage: 'Hello'
21.       })
22.       ChildV2({ message: this.message })
23.     }
24.   }
25. }

26. @Component
27. struct Child {
28.   @Builder
29.   buildFunction() {
30.     Column() {
31.       Text('initBuilderParam')
32.         .fontSize(30)
33.     }
34.   }

35.   // 使用@Require必须构造时传参。
36.   @Require regular_value: string = 'Hello';
37.   @Require @State state_value: string = 'Hello';
38.   @Require @Provide provide_value: string = 'Hello';
39.   @Require @BuilderParam initBuildTest: () => void = this.buildFunction;
40.   @Require @Prop initMessage: string = 'Hello';

41.   build() {
42.     Column() {
43.       Text(this.initMessage)
44.         .fontSize(30)
45.       this.initBuildTest();
46.     }
47.   }
48. }

49. @ComponentV2
50. struct ChildV2 {
51.   // 使用@Require必须构造时传参。
52.   @Require @Param message: string;

53.   build() {
54.     Column() {
55.       Text(this.message)
56.     }
57.   }
58. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-animatable-extend "@AnimatableExtend装饰器：定义可动画属性")
# @Reusable装饰器：组件复用

更新时间: 2025-12-16 16:40

@Reusable装饰器标记的自定义组件支持视图节点、组件实例和状态上下文的复用，避免重复创建和销毁，提升性能。

## 概述

使用@Reusable装饰器时，表示该自定义组件可以复用。与[@Component装饰器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components#component)结合使用，标记为@Reusable的自定义组件在从组件树中移除时，组件及其对应的JS对象将被放入复用缓存中。后续创建新自定义组件节点时，将复用缓存中的节点，从而节约组件重新创建的时间。

说明

API version 10开始支持@Reusable，支持在ArkTS中使用。

关于组件复用的原理与使用、优化方法、适用场景，请参考最佳实践[组件复用最佳实践](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-component-reuse)。

@Reusable标识之后，在组件上下树时ArkUI框架会调用该组件的[aboutToReuse](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttoreuse10)方法和[aboutToRecycle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttorecycle10)方法，因此，开发者在实现复用时，大部分代码都集中在这两个生命周期方法中。

如果一个组件里可复用的组件不止一个，可以使用[reuseId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-reuse-id)来区分不同结构的复用组件。

## 限制条件

- @Reusable装饰器仅用于自定义组件。
    
- @Reusable不支持跟[@ComponentV2](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-componentv2)搭配使用，@ComponentV2组件复用推荐[@ReusableV2装饰器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-reusablev2)。
    

1. import { ComponentContent } from "@kit.ArkUI";

2. // @Builder加上@Reusable编译报错,不适用于builder。
3. // @Reusable
4. @Builder
5. function buildCreativeLoadingDialog(closedClick: () => void) {
6.   Crash()
7. }

8. @Component
9. export struct Crash {
10.   build() {
11.     Column() {
12.       Text("Crash")
13.         .fontSize(12)
14.         .lineHeight(18)
15.         .fontColor(Color.Blue)
16.         .margin({
17.           left: 6
18.         })
19.     }.width('100%')
20.     .height('100%')
21.     .justifyContent(FlexAlign.Center)
22.   }
23. }

24. @Entry
25. @Component
26. struct Index {
27.   @State message: string = 'Hello World';
28.   private uiContext = this.getUIContext();

29.   build() {
30.     RelativeContainer() {
31.       Text(this.message)
32.         .id('Index')
33.         .fontSize(50)
34.         .fontWeight(FontWeight.Bold)
35.         .alignRules({
36.           center: { anchor: '__container__', align: VerticalAlign.Center },
37.           middle: { anchor: '__container__', align: HorizontalAlign.Center }
38.         })
39.         .onClick(() => {
40.           let contentNode = new ComponentContent(this.uiContext, wrapBuilder(buildCreativeLoadingDialog), () => {
41.           });
42.           this.uiContext.getPromptAction().openCustomDialog(contentNode);
43.         })
44.     }
45.     .height('100%')
46.     .width('100%')
47.   }
48. }

- 被@Reusable装饰的自定义组件在复用时，会递归调用该自定义组件及其所有子组件的aboutToReuse回调函数。若在子组件的aboutToReuse函数中修改了父组件的状态变量，此次修改将不会生效，请避免此类用法。若需设置父组件的状态变量，可使用setTimeout设置延迟执行，将任务抛出组件复用的作用范围，使修改生效。
    
    【反例】
    
    在子组件的aboutToReuse中，直接修改父组件的状态变量。
    
    1. class BasicDataSource implements IDataSource {
    2.   private listener: DataChangeListener | undefined = undefined;
    3.   public dataArray: number[] = [];
    
    4.   totalCount(): number {
    5.     return this.dataArray.length;
    6.   }
    
    7.   getData(index: number): number {
    8.     return this.dataArray[index];
    9.   }
    
    10.   registerDataChangeListener(listener: DataChangeListener): void {
    11.     this.listener = listener;
    12.   }
    
    13.   unregisterDataChangeListener(listener: DataChangeListener): void {
    14.     this.listener = undefined;
    15.   }
    16. }
    
    17. @Entry
    18. @Component
    19. struct Index {
    20.   private data: BasicDataSource = new BasicDataSource();
    
    21.   aboutToAppear(): void {
    22.     for (let index = 1; index < 20; index++) {
    23.       this.data.dataArray.push(index);
    24.     }
    25.   }
    
    26.   build() {
    27.     List() {
    28.       LazyForEach(this.data, (item: number, index: number) => {
    29.         ListItem() {
    30.           ReuseComponent({ num: item })
    31.         }
    32.       }, (item: number, index: number) => index.toString())
    33.     }.cachedCount(0)
    34.   }
    35. }
    
    36. @Reusable
    37. @Component
    38. struct ReuseComponent {
    39.   @State num: number = 0;
    
    40.   aboutToReuse(params: ESObject): void {
    41.     this.num = params.num;
    42.   }
    
    43.   build() {
    44.     Column() {
    45.       Text('ReuseComponent num:' + this.num.toString())
    46.       ReuseComponentChild({ num: this.num })
    47.       Button('plus')
    48.         .onClick(() => {
    49.           this.num += 10;
    50.         })
    51.     }
    52.     .height(200)
    53.   }
    54. }
    
    55. @Component
    56. struct ReuseComponentChild {
    57.   @Link num: number;
    
    58.   aboutToReuse(params: ESObject): void {
    59.     this.num = -1 * params.num;
    60.   }
    
    61.   build() {
    62.     Text('ReuseComponentChild num:' + this.num.toString())
    63.   }
    64. }
    
    【正例】
    
    在子组件的aboutToReuse中，使用setTimeout，将修改抛出组件复用的作用范围。
    
    65. class BasicDataSource implements IDataSource {
    66.   private listener: DataChangeListener | undefined = undefined;
    67.   public dataArray: number[] = [];
    
    68.   totalCount(): number {
    69.     return this.dataArray.length;
    70.   }
    
    71.   getData(index: number): number {
    72.     return this.dataArray[index];
    73.   }
    
    74.   registerDataChangeListener(listener: DataChangeListener): void {
    75.     this.listener = listener;
    76.   }
    
    77.   unregisterDataChangeListener(listener: DataChangeListener): void {
    78.     this.listener = undefined;
    79.   }
    80. }
    
    81. @Entry
    82. @Component
    83. struct Index {
    84.   private data: BasicDataSource = new BasicDataSource();
    
    85.   aboutToAppear(): void {
    86.     for (let index = 1; index < 20; index++) {
    87.       this.data.dataArray.push(index);
    88.     }
    89.   }
    
    90.   build() {
    91.     List() {
    92.       LazyForEach(this.data, (item: number, index: number) => {
    93.         ListItem() {
    94.           ReuseComponent({ num: item })
    95.         }
    96.       }, (item: number, index: number) => index.toString())
    97.     }.cachedCount(0)
    98.   }
    99. }
    
    100. @Reusable
    101. @Component
    102. struct ReuseComponent {
    103.   @State num: number = 0;
    
    104.   aboutToReuse(params: ESObject): void {
    105.     this.num = params.num;
    106.   }
    
    107.   build() {
    108.     Column() {
    109.       Text('ReuseComponent num:' + this.num.toString())
    110.       ReuseComponentChild({ num: this.num })
    111.       Button('plus')
    112.         .onClick(() => {
    113.           this.num += 10;
    114.         })
    115.     }
    116.     .height(200)
    117.   }
    118. }
    
    119. @Component
    120. struct ReuseComponentChild {
    121.   @Link num: number;
    
    122.   aboutToReuse(params: ESObject): void {
    123.     setTimeout(() => {
    124.       this.num = -1 * params.num;
    125.     }, 1)
    126.   }
    
    127.   build() {
    128.     Text('ReuseComponentChild num:' + this.num.toString())
    129.   }
    130. }
    
- 被@Reusable装饰的自定义组件在复用前后，应保持组件的结构不变。否则，会在复用过程中创建或销毁子组件，降低复用效率和性能，甚至造成应用行为异常。
    
    对于复用过程中创建的子组件，框架会在其创建后依次调用aboutToReuse方法和aboutToAppear方法。在调用aboutToReuse方法时，由于其aboutToAppear方法还未执行，且内部子组件还未创建，因此可能引起预期外的行为。在调用aboutToReuse方法后，框架会再调用aboutToAppear方法并初始化组件。
    
    针对组件结构存在差异的场景，开发者需要通过设定不同的reuseId来进行区分，具体方式请参考[多种条目类型使用场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-reusable#%E5%A4%9A%E7%A7%8D%E6%9D%A1%E7%9B%AE%E7%B1%BB%E5%9E%8B%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF)。
    
    【反例】
    
    组件结构存在差异，但未通过reuseId进行区分。
    
    以下示例中，先点击“show/hide branch A”按钮，组件被回收，再点击“show/hide branch B”按钮，组件被复用。子组件ReusableChildB在复用过程中被创建，aboutToReuse方法和aboutToAppear方法被同时依次调用。
    
    1. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    2. const TAG = '[Sample_ReusableComponent]';
    3. const DOMAIN = 0xF811;
    4. const BUNDLE = 'ReusableComponent_';
    
    5. @Entry
    6. @Component
    7. struct Index {
    8.   @State showBranchA: boolean = true;
    9.   @State showBranchB: boolean = false;
    
    10.   build() {
    11.     Column({ space: 5 }) {
    12.       Button('show/hide branch A')
    13.         .onClick(() => {
    14.           this.showBranchA = !this.showBranchA;
    15.         })
    16.       if (this.showBranchA) {
    17.         ReusableComponent({ flag: true })
    18.       }
    19.       Button('show/hide branch B')
    20.         .onClick(() => {
    21.           this.showBranchB = !this.showBranchB;
    22.         })
    23.       if (this.showBranchB) {
    24.         ReusableComponent({ flag: false })
    25.       }
    26.     }
    27.   }
    28. }
    
    29. @Reusable
    30. @Component
    31. struct ReusableComponent {
    32.   @Require @Prop flag: boolean = true;
    
    33.   aboutToAppear() {
    34.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableComponent aboutToAppear');
    35.   }
    
    36.   aboutToReuse(params: ESObject) {
    37.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableComponent aboutToReuse');
    38.     this.flag = params.flag;
    39.   }
    
    40.   build() {
    41.     Column({ space: 5 }) {
    42.       Text('ReusableComponent')
    43.       if (this.flag) {
    44.         ReusableChildA()
    45.       } else {
    46.         ReusableChildB()
    47.       }
    48.     }.border({ width: 1 })
    49.   }
    50. }
    
    51. @Component
    52. struct ReusableChildA {
    53.   aboutToAppear() {
    54.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableChildA aboutToAppear');
    55.   }
    
    56.   aboutToReuse() {
    57.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableChildA aboutToReuse');
    58.   }
    
    59.   build() {
    60.     Text('ReusableChildA')
    61.       .border({ width: 1 })
    62.   }
    63. }
    
    64. @Component
    65. struct ReusableChildB {
    66.   aboutToAppear() {
    67.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableChildB aboutToAppear');
    68.   }
    
    69.   aboutToReuse() {
    70.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableChildB aboutToReuse');
    71.   }
    
    72.   build() {
    73.     Text('ReusableChildB')
    74.       .border({ width: 1 })
    75.   }
    76. }
    
    【正例】
    
    组件结构存在差异，通过reuseId进行区分。
    
    77. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    78. const TAG = '[Sample_ReusableComponent]';
    79. const DOMAIN = 0xF811;
    80. const BUNDLE = 'ReusableComponent_';
    
    81. @Entry
    82. @Component
    83. struct Index {
    84.   @State showBranchA: boolean = true;
    85.   @State showBranchB: boolean = false;
    
    86.   build() {
    87.     Column({ space: 5 }) {
    88.       Button('show/hide branch A')
    89.         .onClick(() => {
    90.           this.showBranchA = !this.showBranchA;
    91.         })
    92.       if (this.showBranchA) {
    93.         ReusableComponent({ flag: true })
    94.           .reuseId('ReuseA') // 通过reuseId区分不同结构的复用组件
    95.       }
    96.       Button('show/hide branch B')
    97.         .onClick(() => {
    98.           this.showBranchB = !this.showBranchB;
    99.         })
    100.       if (this.showBranchB) {
    101.         ReusableComponent({ flag: false })
    102.           .reuseId('ReuseB') // 通过reuseId区分不同结构的复用组件
    103.       }
    104.     }
    105.   }
    106. }
    
    107. @Reusable
    108. @Component
    109. struct ReusableComponent {
    110.   @Require @Prop flag: boolean = true;
    
    111.   aboutToAppear() {
    112.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableComponent aboutToAppear');
    113.   }
    
    114.   aboutToReuse(params: ESObject) {
    115.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableComponent aboutToReuse');
    116.     this.flag = params.flag;
    117.   }
    
    118.   build() {
    119.     Column({ space: 5 }) {
    120.       Text('ReusableComponent')
    121.       if (this.flag) {
    122.         ReusableChildA()
    123.       } else {
    124.         ReusableChildB()
    125.       }
    126.     }.border({ width: 1 })
    127.   }
    128. }
    
    129. @Component
    130. struct ReusableChildA {
    131.   aboutToAppear() {
    132.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableChildA aboutToAppear');
    133.   }
    
    134.   aboutToReuse() {
    135.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableChildA aboutToReuse');
    136.   }
    
    137.   build() {
    138.     Text('ReusableChildA')
    139.       .border({ width: 1 })
    140.   }
    141. }
    
    142. @Component
    143. struct ReusableChildB {
    144.   aboutToAppear() {
    145.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableChildB aboutToAppear');
    146.   }
    
    147.   aboutToReuse() {
    148.     hilog.info(DOMAIN, TAG, BUNDLE + 'ReusableChildB aboutToReuse');
    149.   }
    
    150.   build() {
    151.     Text('ReusableChildB')
    152.       .border({ width: 1 })
    153.   }
    154. }
    
- ComponentContent不支持传入@Reusable装饰器装饰的自定义组件。
    

1. import { ComponentContent } from "@kit.ArkUI";

2. @Builder
3. function buildCreativeLoadingDialog(closedClick: () => void) {
4.   Crash()
5. }

6. // 如果注释掉就可以正常弹出弹窗，如果加上@Reusable就直接crash。
7. @Reusable
8. @Component
9. export struct Crash {
10.   build() {
11.     Column() {
12.       Text("Crash")
13.         .fontSize(12)
14.         .lineHeight(18)
15.         .fontColor(Color.Blue)
16.         .margin({
17.           left: 6
18.         })
19.     }.width('100%')
20.     .height('100%')
21.     .justifyContent(FlexAlign.Center)
22.   }
23. }

24. @Entry
25. @Component
26. struct Index {
27.   @State message: string = 'Hello World';
28.   private uiContext = this.getUIContext();

29.   build() {
30.     RelativeContainer() {
31.       Text(this.message)
32.         .id('Index')
33.         .fontSize(50)
34.         .fontWeight(FontWeight.Bold)
35.         .alignRules({
36.           center: { anchor: '__container__', align: VerticalAlign.Center },
37.           middle: { anchor: '__container__', align: HorizontalAlign.Center }
38.         })
39.         .onClick(() => {
40.           // ComponentContent底层是BuilderNode，BuilderNode不支持传入@Reusable注解的自定义组件。
41.           let contentNode = new ComponentContent(this.uiContext, wrapBuilder(buildCreativeLoadingDialog), () => {
42.           });
43.           this.uiContext.getPromptAction().openCustomDialog(contentNode);
44.         })
45.     }
46.     .height('100%')
47.     .width('100%')
48.   }
49. }

- @Reusable装饰器不建议嵌套使用，会增加内存，降低复用效率，加大维护难度。嵌套使用会导致额外缓存池的生成，各缓存池拥有相同树状结构，复用效率低下。此外，嵌套使用会使生命周期管理复杂，资源和变量共享困难。

## 使用场景

### 动态布局更新

重复创建与移除视图可能引起频繁的布局计算，从而影响帧率。采用组件复用可以避免不必要的视图创建与布局计算，提升性能。

以下示例中，将Child自定义组件标记为复用组件，通过Button点击更新Child，触发复用。

1. // xxx.ets
2. export class Message {
3.   value: string | undefined;

4.   constructor(value: string) {
5.     this.value = value;
6.   }
7. }

8. @Entry
9. @Component
10. struct Index {
11.   @State switch: boolean = true;

12.   build() {
13.     Column() {
14.       Button('Hello')
15.         .fontSize(30)
16.         .fontWeight(FontWeight.Bold)
17.         .onClick(() => {
18.           this.switch = !this.switch;
19.         })
20.       if (this.switch) {
21.         // 如果只有一个复用的组件，可以不用设置reuseId。
22.         Child({ message: new Message('Child') })
23.           .reuseId('Child')
24.       }
25.     }
26.     .height("100%")
27.     .width('100%')
28.   }
29. }

30. @Reusable
31. @Component
32. struct Child {
33.   @State message: Message = new Message('AboutToReuse');

34.   aboutToReuse(params: Record<string, ESObject>) {
35.     this.message = params.message as Message;
36.   }

37.   build() {
38.     Column() {
39.       Text(this.message.value)
40.         .fontSize(30)
41.     }
42.     .borderWidth(1)
43.     .height(100)
44.   }
45. }

### 列表滚动配合LazyForEach使用

- 当应用展示大量数据的列表并进行滚动操作时，频繁创建和销毁列表项视图可能导致卡顿和性能问题。使用列表组件的组件复用机制可以重用已创建的列表项视图，提高滚动流畅度。
    
- 以下示例代码将CardView自定义组件标记为复用组件，List上下滑动，触发CardView复用。
    

1. class MyDataSource implements IDataSource {
2.   private dataArray: string[] = [];
3.   private listener: DataChangeListener | undefined;

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.   }

13.   public reloadListener(): void {
14.     this.listener?.onDataReloaded();
15.   }

16.   public registerDataChangeListener(listener: DataChangeListener): void {
17.     this.listener = listener;
18.   }

19.   public unregisterDataChangeListener(listener: DataChangeListener): void {
20.     this.listener = undefined;
21.   }
22. }

23. @Entry
24. @Component
25. struct ReuseDemo {
26.   private data: MyDataSource = new MyDataSource();

27.   aboutToAppear() {
28.     for (let i = 1; i < 1000; i++) {
29.       this.data.pushData(i + "");
30.     }
31.   }

32.   // ...
33.   build() {
34.     Column() {
35.       List() {
36.         LazyForEach(this.data, (item: string) => {
37.           ListItem() {
38.             CardView({ item: item })
39.           }
40.         }, (item: string) => item)
41.       }
42.     }
43.   }
44. }

45. // 复用组件
46. @Reusable
47. @Component
48. export struct CardView {
49.   // 被@State修饰的变量item才能更新，未被@State修饰的变量不会更新。
50.   @State item: string = '';

51.   aboutToReuse(params: Record<string, Object>): void {
52.     this.item = params.item as string;
53.   }

54.   build() {
55.     Column() {
56.       Text(this.item)
57.         .fontSize(30)
58.     }
59.     .borderWidth(1)
60.     .height(100)
61.   }
62. }

### 列表滚动-if使用场景

以下示例代码将OneMoment自定义组件标记为复用组件。当List上下滑动时，会触发OneMoment的复用。设置reuseId可为复用组件分配复用组，相同reuseId的组件将在同一复用组中复用。单个复用组件无需设置reuseId。使用reuseId标识复用组件，可避免重复执行if语句的删除和重新创建逻辑，提高复用效率和性能。

1. @Entry
2. @Component
3. struct Index {
4.   private dataSource = new MyDataSource<FriendMoment>();

5.   aboutToAppear(): void {
6.     for (let i = 0; i < 20; i++) {
7.       let title = i + 1 + "test_if";
8.       this.dataSource.pushData(new FriendMoment(i.toString(), title, 'app.media.app_icon'));
9.     }

10.     for (let i = 0; i < 50; i++) {
11.       let title = i + 1 + "test_if";
12.       this.dataSource.pushData(new FriendMoment(i.toString(), title, ''));
13.     }
14.   }

15.   build() {
16.     Column() {
17.       // TopBar()
18.       List({ space: 3 }) {
19.         LazyForEach(this.dataSource, (moment: FriendMoment) => {
20.           ListItem() {
21.             // 使用reuseId进行组件复用的控制。
22.             OneMoment({ moment: moment })
23.               .reuseId((moment.image !== '') ? 'withImage' : 'noImage')
24.           }
25.         }, (moment: FriendMoment) => moment.id)
26.       }
27.       .cachedCount(0)
28.     }
29.   }
30. }

31. class FriendMoment {
32.   id: string = '';
33.   text: string = '';
34.   title: string = '';
35.   image: string = '';
36.   answers: Array<ResourceStr> = [];

37.   constructor(id: string, title: string, image: string) {
38.     this.text = id;
39.     this.title = title;
40.     this.image = image;
41.   }
42. }

43. @Reusable
44. @Component
45. export struct OneMoment {
46.   @Prop moment: FriendMoment;

47.   // 复用id相同的组件才能触发复用。
48.   aboutToReuse(params: ESObject): void {
49.     console.log("=====aboutToReuse====OneMoment==复用了==" + this.moment.text);
50.   }

51.   build() {
52.     Column() {
53.       Text(this.moment.text)
54.       // if分支判断。
55.       if (this.moment.image !== '') {
56.         Flex({ wrap: FlexWrap.Wrap }) {
57.           Image($r(this.moment.image)).height(50).width(50)
58.           Image($r(this.moment.image)).height(50).width(50)
59.           Image($r(this.moment.image)).height(50).width(50)
60.           Image($r(this.moment.image)).height(50).width(50)
61.         }
62.       }
63.     }
64.   }
65. }

66. class BasicDataSource<T> implements IDataSource {
67.   private listeners: DataChangeListener[] = [];
68.   private originDataArray: T[] = [];

69.   public totalCount(): number {
70.     return 0;
71.   }

72.   public getData(index: number): T {
73.     return this.originDataArray[index];
74.   }

75.   registerDataChangeListener(listener: DataChangeListener): void {
76.     if (this.listeners.indexOf(listener) < 0) {
77.       this.listeners.push(listener);
78.     }
79.   }

80.   unregisterDataChangeListener(listener: DataChangeListener): void {
81.     const pos = this.listeners.indexOf(listener);
82.     if (pos >= 0) {
83.       this.listeners.splice(pos, 1);
84.     }
85.   }

86.   notifyDataAdd(index: number): void {
87.     this.listeners.forEach(listener => {
88.       listener.onDataAdd(index);
89.     });
90.   }
91. }

92. export class MyDataSource<T> extends BasicDataSource<T> {
93.   private dataArray: T[] = [];

94.   public totalCount(): number {
95.     return this.dataArray.length;
96.   }

97.   public getData(index: number): T {
98.     return this.dataArray[index];
99.   }

100.   public pushData(data: T): void {
101.     this.dataArray.push(data);
102.     this.notifyDataAdd(this.dataArray.length - 1);
103.   }
104. }

### 列表滚动-Foreach使用场景

使用Foreach创建可复用的自定义组件，由于Foreach渲染控制语法的全展开属性，导致复用组件无法复用。示例中点击update，数据刷新成功，但滑动列表时，ListItemView无法复用。点击clear，再次点击update，ListItemView复用成功，因为一帧内重复创建多个已被销毁的自定义组件。

1. // xxx.ets
2. class MyDataSource implements IDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.   }

13.   public registerDataChangeListener(listener: DataChangeListener): void {
14.   }

15.   public unregisterDataChangeListener(listener: DataChangeListener): void {
16.   }
17. }

18. @Entry
19. @Component
20. struct Index {
21.   private data: MyDataSource = new MyDataSource();
22.   private data02: MyDataSource = new MyDataSource();
23.   @State isShow: boolean = true;
24.   @State dataSource: ListItemObject[] = [];

25.   aboutToAppear() {
26.     for (let i = 0; i < 100; i++) {
27.       this.data.pushData(i.toString());
28.     }

29.     for (let i = 30; i < 80; i++) {
30.       this.data02.pushData(i.toString());
31.     }
32.   }

33.   build() {
34.     Column() {
35.       Row() {
36.         Button('clear').onClick(() => {
37.           for (let i = 1; i < 50; i++) {
38.             this.dataSource.pop();
39.           }
40.         }).height(40)

41.         Button('update').onClick(() => {
42.           for (let i = 1; i < 50; i++) {
43.             let obj = new ListItemObject();
44.             obj.id = i;
45.             obj.uuid = Math.random().toString();
46.             obj.isExpand = false;
47.             this.dataSource.push(obj);
48.           }
49.         }).height(40)
50.       }

51.       List({ space: 10 }) {
52.         ForEach(this.dataSource, (item: ListItemObject) => {
53.           ListItem() {
54.             ListItemView({
55.               obj: item
56.             })
57.           }
58.         }, (item: ListItemObject) => {
59.           return item.uuid.toString();
60.         })

61.       }.cachedCount(0)
62.       .width('100%')
63.       .height('100%')
64.     }
65.   }
66. }

67. @Reusable
68. @Component
69. struct ListItemView {
70.   @ObjectLink obj: ListItemObject;
71.   @State item: string = '';

72.   aboutToAppear(): void {
73.     // 点击 update，首次进入，上下滑动，由于Foreach折叠展开属性，无法复用。
74.     console.log("=====aboutToAppear=====ListItemView==创建了==" + this.item);
75.   }

76.   aboutToReuse(params: ESObject) {
77.     this.item = params.item;
78.     // 点击clear，再次update，复用成功。
79.     // 符合一帧内重复创建多个已被销毁的自定义组件。
80.     console.log("=====aboutToReuse====ListItemView==复用了==" + this.item);
81.   }

82.   build() {
83.     Column({ space: 10 }) {
84.       Text(`${this.obj.id}.标题`)
85.         .fontSize(16)
86.         .fontColor('#000000')
87.         .padding({
88.           top: 20,
89.           bottom: 20,
90.         })

91.       if (this.obj.isExpand) {
92.         Text('')
93.           .fontSize(14)
94.           .fontColor('#999999')
95.       }
96.     }
97.     .width('100%')
98.     .borderRadius(10)
99.     .backgroundColor(Color.White)
100.     .padding(15)
101.     .onClick(() => {
102.       this.obj.isExpand = !this.obj.isExpand;
103.     })
104.   }
105. }

106. @Observed
107. class ListItemObject {
108.   uuid: string = "";
109.   id: number = 0;
110.   isExpand: boolean = false;
111. }

### Grid使用场景

示例中使用@Reusable装饰器修饰GridItem中的自定义组件ReusableChildComponent，即表示其具备组件复用的能力。

使用aboutToReuse可以在 Grid 滑动时，从复用缓存中加入到组件树之前触发，从而更新组件状态变量，展示正确内容。

需要注意的是无需在aboutToReuse中对[@Link](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-link)、[@StorageLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-appstorage#storagelink)、[@ObjectLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-observed-and-objectlink)、[@Consume](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-provide-and-consume)等自动更新值的状态变量进行更新，可能触发不必要的组件刷新。

1. // MyDataSource类实现IDataSource接口。
2. class MyDataSource implements IDataSource {
3.   private dataArray: number[] = [];

4.   public pushData(data: number): void {
5.     this.dataArray.push(data);
6.   }

7.   // 数据源的数据总量。
8.   public totalCount(): number {
9.     return this.dataArray.length;
10.   }

11.   // 返回指定索引位置的数据。
12.   public getData(index: number): number {
13.     return this.dataArray[index];
14.   }

15.   registerDataChangeListener(listener: DataChangeListener): void {
16.   }

17.   unregisterDataChangeListener(listener: DataChangeListener): void {
18.   }
19. }

20. @Entry
21. @Component
22. struct MyComponent {
23.   // 数据源。
24.   private data: MyDataSource = new MyDataSource();

25.   aboutToAppear() {
26.     for (let i = 1; i < 1000; i++) {
27.       this.data.pushData(i);
28.     }
29.   }

30.   build() {
31.     Column({ space: 5 }) {
32.       Grid() {
33.         LazyForEach(this.data, (item: number) => {
34.           GridItem() {
35.             // 使用可复用自定义组件。
36.             ReusableChildComponent({ item: item })
37.           }
38.         }, (item: string) => item)
39.       }
40.       .cachedCount(2) // 设置GridItem的缓存数量。
41.       .columnsTemplate('1fr 1fr 1fr')
42.       .columnsGap(10)
43.       .rowsGap(10)
44.       .margin(10)
45.       .height(500)
46.       .backgroundColor(0xFAEEE0)
47.     }
48.   }
49. }

50. @Reusable
51. @Component
52. struct ReusableChildComponent {
53.   @State item: number = 0;

54.   // aboutToReuse从复用缓存中加入到组件树之前调用，可在此处更新组件的状态变量以展示正确的内容。
55.   // aboutToReuse参数类型已不支持any，这里使用Record指定明确的数据类型。Record用于构造一个对象类型，其属性键为Keys，属性值为Type。
56.   aboutToReuse(params: Record<string, number>) {
57.     this.item = params.item;
58.   }

59.   build() {
60.     Column() {
61.       // 请开发者自行在src/main/resources/base/media路径下添加app.media.app_icon图片，否则运行时会因资源缺失而报错。
62.       Image($r('app.media.app_icon'))
63.         .objectFit(ImageFit.Fill)
64.         .layoutWeight(1)
65.       Text(`图片${this.item}`)
66.         .fontSize(16)
67.         .textAlign(TextAlign.Center)
68.     }
69.     .width('100%')
70.     .height(120)
71.     .backgroundColor(0xF9CF93)
72.   }
73. }

### WaterFlow使用场景

- 在WaterFlow滑动场景中，FlowItem及其子组件频繁创建和销毁。可以将FlowItem中的组件封装成自定义组件，并使用@Reusable装饰器修饰，实现组件复用。

1. class WaterFlowDataSource implements IDataSource {
2.   private dataArray: number[] = [];
3.   private listeners: DataChangeListener[] = [];

4.   constructor() {
5.     for (let i = 0; i <= 60; i++) {
6.       this.dataArray.push(i);
7.     }
8.   }

9.   // 获取索引对应的数据。
10.   public getData(index: number): number {
11.     return this.dataArray[index];
12.   }

13.   // 通知控制器增加数据。
14.   notifyDataAdd(index: number): void {
15.     this.listeners.forEach(listener => {
16.       listener.onDataAdd(index);
17.     });
18.   }

19.   // 获取数据总数。
20.   public totalCount(): number {
21.     return this.dataArray.length;
22.   }

23.   // 注册改变数据的控制器。
24.   registerDataChangeListener(listener: DataChangeListener): void {
25.     if (this.listeners.indexOf(listener) < 0) {
26.       this.listeners.push(listener);
27.     }
28.   }

29.   // 注销改变数据的控制器。
30.   unregisterDataChangeListener(listener: DataChangeListener): void {
31.     const pos = this.listeners.indexOf(listener);
32.     if (pos >= 0) {
33.       this.listeners.splice(pos, 1);
34.     }
35.   }

36.   // 在数据尾部增加一个元素。
37.   public addLastItem(): void {
38.     this.dataArray.splice(this.dataArray.length, 0, this.dataArray.length);
39.     this.notifyDataAdd(this.dataArray.length - 1);
40.   }
41. }

42. @Reusable
43. @Component
44. struct ReusableFlowItem {
45.   @State item: number = 0;

46.   // 从复用缓存中加入到组件树之前调用，可在此处更新组件的状态变量以展示正确的内容。
47.   aboutToReuse(params: ESObject) {
48.     this.item = params.item;
49.     console.log("=====aboutToReuse====FlowItem==复用了==" + this.item);
50.   }

51.   aboutToRecycle(): void {
52.     console.log("=====aboutToRecycle====FlowItem==回收了==" + this.item);
53.   }

54.   build() {
55.     // 请开发者自行在src/main/resources/base/media路径下添加app.media.app_icon图片，否则运行时会因资源缺失而报错。
56.     Column() {
57.       Text("N" + this.item).fontSize(24).height('26').margin(10)
58.       Image($r('app.media.app_icon'))
59.         .objectFit(ImageFit.Cover)
60.         .width(50)
61.         .height(50)
62.     }
63.   }
64. }

65. @Entry
66. @Component
67. struct Index {
68.   @State minSize: number = 50;
69.   @State maxSize: number = 80;
70.   @State fontSize: number = 24;
71.   @State colors: number[] = [0xFFC0CB, 0xDA70D6, 0x6B8E23, 0x6A5ACD, 0x00FFFF, 0x00FF7F];
72.   scroller: Scroller = new Scroller();
73.   dataSource: WaterFlowDataSource = new WaterFlowDataSource();
74.   private itemWidthArray: number[] = [];
75.   private itemHeightArray: number[] = [];

76.   // 计算flow item宽/高。
77.   getSize() {
78.     let ret = Math.floor(Math.random() * this.maxSize);
79.     return (ret > this.minSize ? ret : this.minSize);
80.   }

81.   // 保存flow item宽/高。
82.   getItemSizeArray() {
83.     for (let i = 0; i < 100; i++) {
84.       this.itemWidthArray.push(this.getSize());
85.       this.itemHeightArray.push(this.getSize());
86.     }
87.   }

88.   aboutToAppear() {
89.     this.getItemSizeArray();
90.   }

91.   build() {
92.     Stack({ alignContent: Alignment.TopStart }) {
93.       Column({ space: 2 }) {
94.         Button('back top')
95.           .height('5%')
96.           .onClick(() => {

97.             // 点击后回到顶部。
98.             this.scroller.scrollEdge(Edge.Top);
99.           })
100.         WaterFlow({ scroller: this.scroller }) {
101.           LazyForEach(this.dataSource, (item: number) => {
102.             FlowItem() {
103.               ReusableFlowItem({ item: item })
104.             }.onAppear(() => {
105.               if (item + 20 == this.dataSource.totalCount()) {
106.                 for (let i = 0; i < 50; i++) {
107.                   this.dataSource.addLastItem();
108.                 }
109.               }
110.             })

111.           })
112.         }
113.       }
114.     }
115.   }
116. }

### Swiper使用场景

- 在Swiper滑动场景中，条目中的子组件频繁创建和销毁。可以将这些子组件封装成自定义组件，并使用@Reusable装饰器修饰，以实现组件复用。

1. @Entry
2. @Component
3. struct Index {
4.   private dataSource = new MyDataSource<Question>();

5.   aboutToAppear(): void {
6.     for (let i = 0; i < 1000; i++) {
7.       let title = i + 1 + "test_swiper";
8.       let answers = ["test1", "test2", "test3",
9.         "test4"];
10.       // 请开发者自行在src/main/resources/base/media路径下添加app.media.app_icon图片，否则运行时会因资源缺失而报错。
11.       this.dataSource.pushData(new Question(i.toString(), title, $r('app.media.app_icon'), answers));
12.     }
13.   }

14.   build() {
15.     Column({ space: 5 }) {
16.       Swiper() {
17.         LazyForEach(this.dataSource, (item: Question) => {
18.           QuestionSwiperItem({ itemData: item })
19.         }, (item: Question) => item.id)
20.       }
21.     }
22.     .width('100%')
23.     .margin({ top: 5 })
24.   }
25. }

26. class Question {
27.   id: string = '';
28.   title: ResourceStr = '';
29.   image: ResourceStr = '';
30.   answers: Array<ResourceStr> = [];

31.   constructor(id: string, title: ResourceStr, image: ResourceStr, answers: Array<ResourceStr>) {
32.     this.id = id;
33.     this.title = title;
34.     this.image = image;
35.     this.answers = answers;
36.   }
37. }

38. @Reusable
39. @Component
40. struct QuestionSwiperItem {
41.   @State itemData: Question | null = null;

42.   aboutToReuse(params: Record<string, Object>): void {
43.     this.itemData = params.itemData as Question;
44.     console.info("===aboutToReuse====QuestionSwiperItem==");
45.   }

46.   build() {
47.     Column() {
48.       Text(this.itemData?.title)
49.         .fontSize(18)
50.         .fontColor($r('sys.color.ohos_id_color_primary'))
51.         .alignSelf(ItemAlign.Start)
52.         .margin({
53.           top: 10,
54.           bottom: 16
55.         })
56.       Image(this.itemData?.image)
57.         .width('100%')
58.         .borderRadius(12)
59.         .objectFit(ImageFit.Contain)
60.         .margin({
61.           bottom: 16
62.         })
63.         .height(80)
64.         .width(80)

65.       Column({ space: 16 }) {
66.         ForEach(this.itemData?.answers, (item: Resource) => {
67.           Text(item)
68.             .fontSize(16)
69.             .fontColor($r('sys.color.ohos_id_color_primary'))
70.         }, (item: ResourceStr) => JSON.stringify(item))
71.       }
72.       .width('100%')
73.       .alignItems(HorizontalAlign.Start)
74.     }
75.     .width('100%')
76.     .padding({
77.       left: 16,
78.       right: 16
79.     })
80.   }
81. }

82. class BasicDataSource<T> implements IDataSource {
83.   private listeners: DataChangeListener[] = [];
84.   private originDataArray: T[] = [];

85.   public totalCount(): number {
86.     return 0;
87.   }

88.   public getData(index: number): T {
89.     return this.originDataArray[index];
90.   }

91.   registerDataChangeListener(listener: DataChangeListener): void {
92.     if (this.listeners.indexOf(listener) < 0) {
93.       this.listeners.push(listener);
94.     }
95.   }

96.   unregisterDataChangeListener(listener: DataChangeListener): void {
97.     const pos = this.listeners.indexOf(listener);
98.     if (pos >= 0) {
99.       this.listeners.splice(pos, 1);
100.     }
101.   }

102.   notifyDataAdd(index: number): void {
103.     this.listeners.forEach(listener => {
104.       listener.onDataAdd(index);
105.     });
106.   }
107. }

108. export class MyDataSource<T> extends BasicDataSource<T> {
109.   private dataArray: T[] = [];

110.   public totalCount(): number {
111.     return this.dataArray.length;
112.   }

113.   public getData(index: number): T {
114.     return this.dataArray[index];
115.   }

116.   public pushData(data: T): void {
117.     this.dataArray.push(data);
118.     this.notifyDataAdd(this.dataArray.length - 1);
119.   }
120. }

### 列表滚动-ListItemGroup使用场景

- 可以视作特殊List滑动场景，将ListItem需要移除重建的子组件封装成自定义组件，并使用@Reusable装饰器修饰，使其具备组件复用能力。

1. @Entry
2. @Component
3. struct ListItemGroupAndReusable {
4.   data: DataSrc2 = new DataSrc2();

5.   @Builder
6.   itemHead(text: string) {
7.     Text(text)
8.       .fontSize(20)
9.       .backgroundColor(0xAABBCC)
10.       .width('100%')
11.       .padding(10)
12.   }

13.   aboutToAppear() {
14.     for (let i = 0; i < 10000; i++) {
15.       let data_1 = new DataSrc1();
16.       for (let j = 0; j < 12; j++) {
17.         data_1.Data.push(`测试条目数据: ${i} - ${j}`);
18.       }
19.       this.data.Data.push(data_1);
20.     }
21.   }

22.   build() {
23.     Stack() {
24.       List() {
25.         LazyForEach(this.data, (item: DataSrc1, index: number) => {
26.           ListItemGroup({ header: this.itemHead(index.toString()) }) {
27.             LazyForEach(item, (ii: string, index: number) => {
28.               ListItem() {
29.                 Inner({ str: ii })
30.               }
31.             })
32.           }
33.           .width('100%')
34.           .height('60vp')
35.         })
36.       }
37.     }
38.     .width('100%')
39.     .height('100%')
40.   }
41. }

42. @Reusable
43. @Component
44. struct Inner {
45.   @State str: string = '';

46.   aboutToReuse(param: ESObject) {
47.     this.str = param.str;
48.   }

49.   build() {
50.     Text(this.str)
51.   }
52. }

53. class DataSrc1 implements IDataSource {
54.   listeners: DataChangeListener[] = [];
55.   Data: string[] = [];

56.   public totalCount(): number {
57.     return this.Data.length;
58.   }

59.   public getData(index: number): string {
60.     return this.Data[index];
61.   }

62.   // 该方法为框架侧调用，为LazyForEach组件向其数据源处添加listener监听。
63.   registerDataChangeListener(listener: DataChangeListener): void {
64.     if (this.listeners.indexOf(listener) < 0) {
65.       this.listeners.push(listener);
66.     }
67.   }

68.   // 该方法为框架侧调用，为对应的LazyForEach组件在数据源处去除listener监听。
69.   unregisterDataChangeListener(listener: DataChangeListener): void {
70.     const pos = this.listeners.indexOf(listener);
71.     if (pos >= 0) {
72.       this.listeners.splice(pos, 1);
73.     }
74.   }

75.   // 通知LazyForEach组件需要重载所有子组件。
76.   notifyDataReload(): void {
77.     this.listeners.forEach(listener => {
78.       listener.onDataReloaded();
79.     });
80.   }

81.   // 通知LazyForEach组件需要在index对应索引处添加子组件。
82.   notifyDataAdd(index: number): void {
83.     this.listeners.forEach(listener => {
84.       listener.onDataAdd(index);
85.     });
86.   }

87.   // 通知LazyForEach组件在index对应索引处数据有变化，需要重建该子组件。
88.   notifyDataChange(index: number): void {
89.     this.listeners.forEach(listener => {
90.       listener.onDataChange(index);
91.     });
92.   }

93.   // 通知LazyForEach组件需要在index对应索引处删除该子组件。
94.   notifyDataDelete(index: number): void {
95.     this.listeners.forEach(listener => {
96.       listener.onDataDelete(index);
97.     });
98.   }

99.   // 通知LazyForEach组件将from索引和to索引处的子组件进行交换。
100.   notifyDataMove(from: number, to: number): void {
101.     this.listeners.forEach(listener => {
102.       listener.onDataMove(from, to);
103.     });
104.   }
105. }

106. class DataSrc2 implements IDataSource {
107.   listeners: DataChangeListener[] = [];
108.   Data: DataSrc1[] = [];

109.   public totalCount(): number {
110.     return this.Data.length;
111.   }

112.   public getData(index: number): DataSrc1 {
113.     return this.Data[index];
114.   }

115.   // 该方法为框架侧调用，为LazyForEach组件向其数据源处添加listener监听。
116.   registerDataChangeListener(listener: DataChangeListener): void {
117.     if (this.listeners.indexOf(listener) < 0) {
118.       this.listeners.push(listener);
119.     }
120.   }

121.   // 该方法为框架侧调用，为对应的LazyForEach组件在数据源处去除listener监听。
122.   unregisterDataChangeListener(listener: DataChangeListener): void {
123.     const pos = this.listeners.indexOf(listener);
124.     if (pos >= 0) {
125.       this.listeners.splice(pos, 1);
126.     }
127.   }

128.   // 通知LazyForEach组件需要重载所有子组件。
129.   notifyDataReload(): void {
130.     this.listeners.forEach(listener => {
131.       listener.onDataReloaded();
132.     });
133.   }

134.   // 通知LazyForEach组件需要在index对应索引处添加子组件。
135.   notifyDataAdd(index: number): void {
136.     this.listeners.forEach(listener => {
137.       listener.onDataAdd(index);
138.     });
139.   }

140.   // 通知LazyForEach组件在index对应索引处数据有变化，需要重建该子组件。
141.   notifyDataChange(index: number): void {
142.     this.listeners.forEach(listener => {
143.       listener.onDataChange(index);
144.     });
145.   }

146.   // 通知LazyForEach组件需要在index对应索引处删除该子组件。
147.   notifyDataDelete(index: number): void {
148.     this.listeners.forEach(listener => {
149.       listener.onDataDelete(index);
150.     });
151.   }

152.   // 通知LazyForEach组件将from索引和to索引处的子组件进行交换。
153.   notifyDataMove(from: number, to: number): void {
154.     this.listeners.forEach(listener => {
155.       listener.onDataMove(from, to);
156.     });
157.   }
158. }

### 多种条目类型使用场景

**标准型**

复用组件的布局相同，示例参见本文列表滚动部分的描述。

**有限变化型**

复用组件间存在差异，但类型有限。例如，可以通过显式设置两个reuseId或使用两个自定义组件来实现复用。

1. class MyDataSource implements IDataSource {
2.   private dataArray: string[] = [];
3.   private listener: DataChangeListener | undefined;

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.   }

13.   public reloadListener(): void {
14.     this.listener?.onDataReloaded();
15.   }

16.   public registerDataChangeListener(listener: DataChangeListener): void {
17.     this.listener = listener;
18.   }

19.   public unregisterDataChangeListener(listener: DataChangeListener): void {
20.     this.listener = undefined;
21.   }
22. }

23. @Entry
24. @Component
25. struct Index {
26.   private data: MyDataSource = new MyDataSource();

27.   aboutToAppear() {
28.     for (let i = 0; i < 1000; i++) {
29.       this.data.pushData(i + "");
30.     }
31.   }

32.   build() {
33.     Column() {
34.       List({ space: 10 }) {
35.         LazyForEach(this.data, (item: number) => {
36.           ListItem() {
37.             ReusableComponent({ item: item })
38.               // 设置两种有限变化的reuseId
39.               .reuseId(item % 2 === 0 ? 'ReusableComponentOne' : 'ReusableComponentTwo')
40.           }
41.           .backgroundColor(Color.Orange)
42.           .width('100%')
43.         }, (item: number) => item.toString())
44.       }
45.       .cachedCount(2)
46.     }
47.   }
48. }

49. @Reusable
50. @Component
51. struct ReusableComponent {
52.   @State item: number = 0;

53.   aboutToReuse(params: ESObject) {
54.     this.item = params.item;
55.   }

56.   build() {
57.     Column() {
58.       // 组件内部根据类型差异渲染
59.       if (this.item % 2 === 0) {
60.         Text(`Item ${this.item} ReusableComponentOne`)
61.           .fontSize(20)
62.           .margin({ left: 10 })
63.       } else {
64.         Text(`Item ${this.item} ReusableComponentTwo`)
65.           .fontSize(20)
66.           .margin({ left: 10 })
67.       }
68.     }.margin({ left: 10, right: 10 })
69.   }
70. }

**组合型**

复用组件间存在多种差异，但通常具备共同的子组件。将三种复用组件以组合型方式转换为Builder函数后，内部的共享子组件将统一置于父组件MyComponent之下。复用这些子组件时，缓存池在父组件层面实现共享，减少组件创建过程中的资源消耗。

1. class MyDataSource implements IDataSource {
2.   private dataArray: string[] = [];
3.   private listener: DataChangeListener | undefined;

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.   }

13.   public reloadListener(): void {
14.     this.listener?.onDataReloaded();
15.   }

16.   public registerDataChangeListener(listener: DataChangeListener): void {
17.     this.listener = listener;
18.   }

19.   public unregisterDataChangeListener(listener: DataChangeListener): void {
20.     this.listener = undefined;
21.   }
22. }

23. @Entry
24. @Component
25. struct MyComponent {
26.   private data: MyDataSource = new MyDataSource();

27.   aboutToAppear() {
28.     for (let i = 0; i < 1000; i++) {
29.       this.data.pushData(i.toString());
30.     }
31.   }

32.   // itemBuilderOne作为复用组件的写法未展示，以下为转为Builder之后的写法。
33.   @Builder
34.   itemBuilderOne(item: string) {
35.     Column() {
36.       ChildComponentA({ item: item })
37.       ChildComponentB({ item: item })
38.       ChildComponentC({ item: item })
39.     }
40.   }

41.   // itemBuilderTwo转为Builder之后的写法。
42.   @Builder
43.   itemBuilderTwo(item: string) {
44.     Column() {
45.       ChildComponentA({ item: item })
46.       ChildComponentC({ item: item })
47.       ChildComponentD({ item: item })
48.     }
49.   }

50.   // itemBuilderThree转为Builder之后的写法。
51.   @Builder
52.   itemBuilderThree(item: string) {
53.     Column() {
54.       ChildComponentA({ item: item })
55.       ChildComponentB({ item: item })
56.       ChildComponentD({ item: item })
57.     }
58.   }

59.   build() {
60.     List({ space: 40 }) {
61.       LazyForEach(this.data, (item: string, index: number) => {
62.         ListItem() {
63.           if (index % 3 === 0) {
64.             this.itemBuilderOne(item)
65.           } else if (index % 5 === 0) {
66.             this.itemBuilderTwo(item)
67.           } else {
68.             this.itemBuilderThree(item)
69.           }
70.         }
71.         .backgroundColor('#cccccc')
72.         .width('100%')
73.         .onAppear(() => {
74.           console.log(`ListItem ${index} onAppear`);
75.         })
76.       }, (item: number) => item.toString())
77.     }
78.     .width('100%')
79.     .height('100%')
80.     .cachedCount(0)
81.   }
82. }

83. @Reusable
84. @Component
85. struct ChildComponentA {
86.   @State item: string = '';

87.   aboutToReuse(params: ESObject) {
88.     console.log(`ChildComponentA ${params.item} Reuse ${this.item}`);
89.     this.item = params.item;
90.   }

91.   aboutToRecycle(): void {
92.     console.log(`ChildComponentA ${this.item} Recycle`);
93.   }

94.   build() {
95.     Column() {
96.       Text(`Item ${this.item} Child Component A`)
97.         .fontSize(20)
98.         .margin({ left: 10 })
99.         .fontColor(Color.Blue)
100.       Grid() {
101.         ForEach((new Array(20)).fill(''), (item: string, index: number) => {
102.           GridItem() {
103.             // 请开发者自行在src/main/resources/base/media路径下添加app.media.startIcon图片，否则运行时会因资源缺失而报错。
104.             Image($r('app.media.startIcon'))
105.               .height(20)
106.           }
107.         })
108.       }
109.       .columnsTemplate('1fr 1fr 1fr 1fr 1fr')
110.       .rowsTemplate('1fr 1fr 1fr 1fr')
111.       .columnsGap(10)
112.       .width('90%')
113.       .height(160)
114.     }
115.     .margin({ left: 10, right: 10 })
116.     .backgroundColor(0xFAEEE0)
117.   }
118. }

119. @Reusable
120. @Component
121. struct ChildComponentB {
122.   @State item: string = '';

123.   aboutToReuse(params: ESObject) {
124.     this.item = params.item;
125.   }

126.   build() {
127.     Row() {
128.       Text(`Item ${this.item} Child Component B`)
129.         .fontSize(20)
130.         .margin({ left: 10 })
131.         .fontColor(Color.Red)
132.     }.margin({ left: 10, right: 10 })
133.   }
134. }

135. @Reusable
136. @Component
137. struct ChildComponentC {
138.   @State item: string = '';

139.   aboutToReuse(params: ESObject) {
140.     this.item = params.item;
141.   }

142.   build() {
143.     Row() {
144.       Text(`Item ${this.item} Child Component C`)
145.         .fontSize(20)
146.         .margin({ left: 10 })
147.         .fontColor(Color.Green)
148.     }.margin({ left: 10, right: 10 })
149.   }
150. }

151. @Reusable
152. @Component
153. struct ChildComponentD {
154.   @State item: string = '';

155.   aboutToReuse(params: ESObject) {
156.     this.item = params.item;
157.   }

158.   build() {
159.     Row() {
160.       Text(`Item ${this.item} Child Component D`)
161.         .fontSize(20)
162.         .margin({ left: 10 })
163.         .fontColor(Color.Orange)
164.     }.margin({ left: 10, right: 10 })
165.   }
166. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-require "@Require装饰器：校验构造传参")
# if/else：条件渲染

更新时间: 2025-12-16 16:39

ArkTS提供了渲染控制能力。条件渲染可根据应用状态，使用if、else和else if渲染相应的UI内容。

说明

从API version 9开始，该接口支持在ArkTS卡片中使用。

## 使用规则

- 支持if、else和else if语句。
    
- if和else if后的条件语句可以使用状态变量或常规变量（状态变量的值改变时会实时渲染UI，而常规变量的值改变则不会）。
    
- 允许在容器组件内使用，通过条件渲染语句构建不同的子组件。
    
- 条件渲染语句在涉及到组件的父子关系时是“透明”的，父组件和子组件之间的条件渲染语句不影响父组件关于子组件使用的限制。例如，某些容器组件限制子组件的类型或数量。将条件渲染语句用于这些组件内时，这些限制同样适用于条件渲染语句内创建的组件。具体而言，[Grid](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-grid)容器组件的子组件仅支持[GridItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-griditem)组件。在Grid内使用条件渲染语句时，条件渲染语句内仅允许使用GridItem组件。
    
- 每个分支内部的构建函数必须遵循构建函数的规则，并创建一个或多个组件。无法创建组件的空构建函数会产生语法错误。关于构建函数的规则，请参考：[基本语法概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-basic-syntax-overview)、[声明式UI描述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-declarative-ui-description)。
    

## 更新机制

当if、else if后跟随的状态判断中使用的状态变量值变化时，条件渲染语句会进行更新，更新步骤如下：

1. 评估if和else if的状态判断条件，如果分支没有变化，无需执行以下步骤。如果分支有变化，则执行2、3步骤。
    
2. 移除此前构建的所有子组件。
    
3. 执行新分支的构造函数，将生成的子组件添加到if父容器中。如果缺少适用的else分支，则不创建任何内容。
    

条件可以包含Typescript表达式。构造函数中的表达式不得更改应用程序状态。

## 使用场景

### 使用if进行条件渲染

1. @Entry
2. @Component
3. struct MyComponent {
4.   @State count: number = 0;

5.   build() {
6.     Column() {
7.       Text(`count=${this.count}`)

8.       if (this.count > 0) {
9.         Text(`count is positive`)
10.           .fontColor(Color.Green)
11.       }

12.       Button('increase count')
13.         .onClick(() => {
14.           this.count++;
15.         })

16.       Button('decrease count')
17.         .onClick(() => {
18.           this.count--;
19.         })
20.     }
21.   }
22. }

if语句的每个分支都包含一个构建函数。此类构建函数必须创建一个或多个子组件。在初始渲染时，if语句会执行构建函数，并将生成的子组件添加到其父组件中。

每当if或else if条件语句中使用的状态变量发生变化时，条件语句都会更新并重新评估新的条件值。如果条件值评估发生了变化，这意味着需要构建另一个条件分支。此时ArkUI框架将：

1. 移除所有以前渲染的（早期分支的）组件。
    
2. 执行新分支的构造函数，将生成的子组件添加到其父组件中。
    

在以上示例中，当count从0增至1时，if (this.count > 0)更新为true，执行该分支的构造函数，创建一个Text组件并添加到父组件Column中。如果后续count更改为0，则Text组件将从Column组件中删除。由于没有else分支，因此不会执行新的构造函数。

### if ... else ...语句和子组件状态

以下示例包含if ... else ...语句与拥有[@State](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-state)装饰变量的子组件。

1. @Component
2. struct CounterView {
3.   @State counter: number = 0;
4.   label: string = 'unknown';

5.   build() {
6.     Column({ space: 20 }) {
7.       Text(`${this.label}`)
8.       Button(`counter ${this.counter} +1`)
9.         .onClick(() => {
10.           this.counter += 1;
11.         })
12.     }
13.     .margin(10)
14.     .padding(10)
15.     .border({ width: 1 })
16.   }
17. }

18. @Entry
19. @Component
20. struct MainView {
21.   @State toggle: boolean = true;

22.   build() {
23.     Column() {
24.       if (this.toggle) {
25.         CounterView({ label: 'CounterView #positive' })
26.       } else {
27.         CounterView({ label: 'CounterView #negative' })
28.       }
29.       Button(`toggle ${this.toggle}`)
30.         .onClick(() => {
31.           this.toggle = !this.toggle;
32.         })
33.     }
34.     .width('100%')
35.     .justifyContent(FlexAlign.Center)
36.   }
37. }

**初次渲染**：创建CounterView子组件（label为 'CounterView #positive'），其状态变量counter初始值为0。

**修改CounterView的counter状态变量**：CounterView子组件（label为 'CounterView #positive'）重新渲染并保留状态变量值。

**修改MainView.toggle状态变量为false**：MainView父组件内的if语句将更新，并进行以下处理：

1. 删除旧的CounterView子组件（label为 'CounterView #positive'）。
2. 创建新的CounterView子组件（label为 'CounterView #negative'），其状态变量counter初始值为0。

说明

CounterView（label为 'CounterView #positive'）和CounterView（label为 'CounterView #negative'）是同一自定义组件的两个不同实例。if分支的更改，不会更新现有子组件，也不会保留状态。

以下示例展示了条件更改时，若需要保留counter值所做的修改。

1. @Component
2. struct CounterView {
3.   @Link counter: number;
4.   label: string = 'unknown';

5.   build() {
6.     Column({ space: 20 }) {
7.       Text(`${this.label}`)
8.         .fontSize(20)
9.       Button(`counter ${this.counter} +1`)
10.         .onClick(() => {
11.           this.counter += 1;
12.         })
13.     }
14.     .margin(10)
15.     .padding(10)
16.     .border({ width: 1 })
17.   }
18. }

19. @Entry
20. @Component
21. struct MainView {
22.   @State toggle: boolean = true;
23.   @State counter: number = 0;

24.   build() {
25.     Column() {
26.       if (this.toggle) {
27.         CounterView({ counter: $counter, label: 'CounterView #positive' })
28.       } else {
29.         CounterView({ counter: $counter, label: 'CounterView #negative' })
30.       }
31.       Button(`toggle ${this.toggle}`)
32.         .onClick(() => {
33.           this.toggle = !this.toggle;
34.         })
35.     }
36.     .width('100%')
37.     .justifyContent(FlexAlign.Center)
38.   }
39. }

此处，@State counter变量归父组件所有。因此，当CounterView组件实例被删除时，该变量不会被销毁。CounterView组件通过[@Link](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-link)装饰器引用状态。状态必须从子级移动到其父级（或父级的父级），以避免在条件内容或重复内容被销毁时丢失状态。

### 嵌套if语句

嵌套条件语句不会影响父组件的相关规则。

1. @Entry
2. @Component
3. struct MyComponent {
4.   @State toggle: boolean = false;
5.   @State toggleColor: boolean = false;

6.   build() {
7.     Column({ space: 20 }) {
8.       Text('Before')
9.         .fontSize(15)
10.       if (this.toggle) {
11.         Text('Top True, positive 1 top')
12.           .backgroundColor('#aaffaa').fontSize(20)
13.         // 内部if语句
14.         if (this.toggleColor) {
15.           Text('Top True, Nested True, positive COLOR  Nested ')
16.             .backgroundColor('#00aaaa').fontSize(15)
17.         } else {
18.           Text('Top True, Nested False, Negative COLOR  Nested ')
19.             .backgroundColor('#aaaaff').fontSize(15)
20.         }
21.       } else {
22.         Text('Top false, negative top level').fontSize(20)
23.           .backgroundColor('#ffaaaa')
24.         if (this.toggleColor) {
25.           Text('positive COLOR  Nested ')
26.             .backgroundColor('#00aaaa').fontSize(15)
27.         } else {
28.           Text('Negative COLOR  Nested ')
29.             .backgroundColor('#aaaaff').fontSize(15)
30.         }
31.       }
32.       Text('After')
33.         .fontSize(15)
34.       Button('Toggle Outer')
35.         .onClick(() => {
36.           this.toggle = !this.toggle;
37.         })
38.       Button('Toggle Inner')
39.         .onClick(() => {
40.           this.toggleColor = !this.toggleColor;
41.         })
42.     }
43.     .width('100%')
44.     .justifyContent(FlexAlign.Center)
45.   }
46. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-overview "渲染控制概述")
# LazyForEach：数据懒加载

更新时间: 2025-12-16 16:39

API参数说明见：[LazyForEach API参数说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach)。

## 概述

LazyForEach为开发者提供了基于数据源渲染出一系列子组件的能力。具体而言，LazyForEach从数据源中按需迭代数据，并在每次迭代时创建相应组件。当在滚动容器中使用了LazyForEach，框架会根据滚动容器可视区域按需创建组件，当组件滑出可视区域外时，框架会销毁并回收组件以降低内存占用。

本文档依次介绍了LazyForEach的[基本用法](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95)、[高级用法](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach#%E9%AB%98%E7%BA%A7%E7%94%A8%E6%B3%95)和[常见问题](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach#%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)，开发者可以按需阅读。在[首次渲染](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach#%E9%A6%96%E6%AC%A1%E6%B8%B2%E6%9F%93)小节中，给出了简单的示例，可以帮助开发者快速上手LazyForEach的使用。

说明

在大量子组件的的场景下，LazyForEach与缓存列表项、动态预加载、组件复用等方法配合使用，可以进一步提升滑动帧率并降低应用内存占用。最佳实践请参考[长列表加载丢帧优化](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-best-practices-long-list)。

## 使用限制

- LazyForEach必须在容器组件内使用，仅有[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-list)、[ListItemGroup](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-listitemgroup)、[Grid](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-grid)、[Swiper](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-swiper)以及[WaterFlow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-waterflow)组件支持数据懒加载（可配置cachedCount属性，即只加载可视部分以及其前后少量数据用于缓冲），其他组件仍然是一次性加载所有的数据。支持数据懒加载的父组件根据自身及子组件的高度或宽度计算可视区域内需布局的子节点数量，高度或宽度的缺失会导致部分场景[懒加载失效](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach#%E6%87%92%E5%8A%A0%E8%BD%BD%E5%A4%B1%E6%95%88)。
- LazyForEach依赖生成的键值判断是否刷新子组件，键值不变则不触发刷新。
- 容器组件内只能包含一个LazyForEach。以List为例，不建议同时包含ListItem、ForEach、LazyForEach，不建议同时包含多个LazyForEach。
- LazyForEach在每次迭代中，必须创建且只允许创建一个子组件；即LazyForEach的子组件生成函数有且只有一个根组件。
- 生成的子组件必须是允许包含在LazyForEach父容器组件中的子组件。
- 允许LazyForEach包含在if/else条件渲染语句中，也允许LazyForEach中出现if/else条件渲染语句。
- 键值生成器必须针对每个数据生成唯一的值，如果键值相同，将导致键值相同的UI组件渲染出现问题。
- LazyForEach必须使用一个数据变化监听器DataChangeListener对象进行更新（具体参数使用参考[LazyForEach](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach)），重新赋值第一个参数dataSource会导致异常；dataSource使用状态变量时，状态变量改变不会触发LazyForEach的UI刷新。
- 为了高性能渲染，使用DataChangeListener对象的onDataChange方法更新UI时，需要生成不同于原来的键值来触发组件刷新。
- LazyForEach和[@Reusable装饰器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-reusable)一起使用能触发节点复用。使用方法：将@Reusable装饰在LazyForEach列表的组件上，见[列表滚动配合LazyForEach使用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-reusable#%E5%88%97%E8%A1%A8%E6%BB%9A%E5%8A%A8%E9%85%8D%E5%90%88lazyforeach%E4%BD%BF%E7%94%A8)。
- LazyForEach和[@ReusableV2装饰器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-reusablev2)一起使用能触发节点复用。详见@ReusableV2装饰器指南文档中的[在LazyForEach组件中使用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-reusablev2#%E5%9C%A8lazyforeach%E7%BB%84%E4%BB%B6%E4%B8%AD%E4%BD%BF%E7%94%A8)。
- LazyForEach的子节点在离开可视区域和预加载区域时，不会立即被析构或回收，LazyForEach会在空闲时析构或回收这些节点。

## 基本用法

### 设置数据源

为了管理[DataChangeListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#datachangelistener)监听器和通知LazyForEach更新数据，开发者需要使用如下方法：首先实现LazyForEach提供的[IDataSource](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#idatasource)接口，将其作为LazyForEach的数据源，然后管理监听器和更新数据。

为实现基本的数据管理和监听能力，开发者需要实现IDataSource的[totalCount](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#totalcount)、[getData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#getdata)、[registerDataChangeListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#registerdatachangelistener)和[unregisterDataChangeListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#unregisterdatachangelistener)方法，具体请参考[BasicDataSource示例代码](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach#basicdatasource%E7%A4%BA%E4%BE%8B%E4%BB%A3%E7%A0%81)。当数据源变化时，通过调用监听器的接口通知LazyForEach更新，具体请参考[数据更新](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach#%E6%95%B0%E6%8D%AE%E6%9B%B4%E6%96%B0)。

### 键值生成规则

在LazyForEach循环渲染过程中，系统为每个item生成一个唯一且持久的键值，用于标识对应的组件。键值变化时，ArkUI框架将视为该数组元素已被替换或修改，并基于新的键值创建新的组件。

LazyForEach提供了参数keyGenerator，开发者可以使用该函数生成自定义键值。如果未定义keyGenerator函数，ArkUI框架将使用默认的键值生成函数：(item: Object, index: number) => { return viewId + '-' + index.toString(); }。viewId在编译器转换过程中生成，同一个LazyForEach组件内的viewId一致。

键值应满足以下条件。

1. 键值具有唯一性，每个数据项对应的键值互不相同。
2. 键值具有一致性，数据项不变时对应的键值也不变。

上述条件保证LazyForEach正确、高效地更新子组件，否则可能存在渲染结果异常、渲染效率降低等问题。

### 组件创建规则

在确定键值生成规则后，LazyForEach的第二个参数itemGenerator函数会根据组件创建规则为数据源的每个数组项创建组件。组件的创建包括两种情况：LazyForEach[首次渲染](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach#%E9%A6%96%E6%AC%A1%E6%B8%B2%E6%9F%93)和LazyForEach非首次渲染的[数据更新](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach#%E6%95%B0%E6%8D%AE%E6%9B%B4%E6%96%B0)。

### 首次渲染

使用LazyForEach时，开发者需要提供数据源、键值生成函数和组件创建函数。**开发者需保证键值生成函数为每项数据生成不同的键值。**

在LazyForEach首次渲染时，会根据上述键值生成规则为数据源的每个数组项生成唯一键值并创建相应的组件。

对于预加载区域内的节点，若创建耗时较长，框架会分帧执行创建任务。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Entry
16. @Component
17. struct MyComponent {
18.   private data: MyDataSource = new MyDataSource();

19.   aboutToAppear() {
20.     for (let i = 0; i <= 20; i++) {
21.       this.data.pushData(`Hello ${i}`);
22.     }
23.   }

24.   build() {
25.     List({ space: 3 }) {
26.       LazyForEach(this.data, (item: string) => {
27.         ListItem() {
28.           Row() {
29.             Text(item).fontSize(50)
30.               .onAppear(() => {
31.                 console.info(`appear: ${item}`);
32.               })
33.           }.margin({ left: 10, right: 10 })
34.         }
35.       }, (item: string) => item)
36.     }.cachedCount(5)
37.   }
38. }

在上述代码中，keyGenerator函数的返回值是item。LazyForEach循环渲染时，为数据源数组项依次生成键值Hello 0、Hello 1 ... Hello 20，并创建对应的ListItem子组件渲染到界面上。

运行效果如下图所示。

**图1** LazyForEach正常首次渲染

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163945.41140068263652180764056903748987:50001231000000:2800:EB7A0106C4BC638E497D99ADD3BD609F502DF3FA691A8784F41BE717159C4C29.gif)

**错误案例：键值相同导致渲染异常**

当不同数据项生成的键值相同时，框架的行为是不可预测的。例如，在以下代码中，LazyForEach渲染的数据项键值均相同，在滑动过程中，LazyForEach会预加载划入划出当前页面的子组件，而新建的子组件和销毁的旧子组件具有相同的键值，框架可能取用错误的缓存，导致子组件渲染出现问题。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Entry
16. @Component
17. struct MyComponent {
18.   private data: MyDataSource = new MyDataSource();

19.   aboutToAppear() {
20.     for (let i = 0; i <= 20; i++) {
21.       this.data.pushData(`Hello ${i}`);
22.     }
23.   }

24.   build() {
25.     List({ space: 3 }) {
26.       LazyForEach(this.data, (item: string) => {
27.         ListItem() {
28.           Row() {
29.             Text(item).fontSize(50)
30.               .onAppear(() => {
31.                 console.info(`appear: ${item}`);
32.               })
33.           }.margin({ left: 10, right: 10 })
34.         }
35.       }, (item: string) => `same key`) // 自定义键值生成函数，返回相同键值
36.     }.cachedCount(5)
37.   }
38. }

运行效果如下图所示。

**图2** LazyForEach存在相同键值

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163945.16317690581967053878672170495546:50001231000000:2800:34C7EC6C3C65668DDA85D9DC1EA8D638934499DAA410A70E9159E9D8B2A95FA3.gif)

修改上述示例中LazyForEach的键值生成函数，使每个数据项生成唯一的键值，保证渲染效果符合预期。

1. LazyForEach(this.data, (item: string) => {
2.   ListItem() {
3.    Row() {
4.     Text(item).fontSize(50)
5.       .onAppear(() => {
6.         console.info(`appear: ${item}`);
7.       })
8.     }.margin({ left: 10, right: 10 })
9.   }
10. }, (item: string, index: number) => `${item}-${index}`) // 自定义键值生成函数，返回唯一键值

修改后运行效果如下图所示。

**图3** LazyForEach生成唯一键值

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163945.21578851806088103605759699816179:50001231000000:2800:03A17C18B9AB740D67C27B08C1B31BF458B6ABB62A9230CEADB0F32F107F349A.gif)

### 数据更新

当LazyForEach数据源发生变化，需要再次渲染时，开发者应根据数据源的变化情况调用listener对应的接口，通知LazyForEach做相应的更新。LazyForEach的更新操作包括：添加数据、删除数据、交换数据、改变单个数据、改变多个数据以及精准批量修改数据，各使用场景示例如下。

**添加数据**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Entry
16. @Component
17. struct MyComponent {
18.   private data: MyDataSource = new MyDataSource();

19.   aboutToAppear() {
20.     for (let i = 0; i <= 20; i++) {
21.       this.data.pushData(`Hello ${i}`);
22.     }
23.   }

24.   build() {
25.     List({ space: 3 }) {
26.       LazyForEach(this.data, (item: string) => {
27.         ListItem() {
28.           Row() {
29.             Text(item).fontSize(50)
30.               .onAppear(() => {
31.                 console.info(`appear: ${item}`);
32.               })
33.           }.margin({ left: 10, right: 10 })
34.         }
35.         .onClick(() => {
36.           // 点击追加子组件
37.           this.data.pushData(`Hello ${this.data.totalCount()}`);
38.         })
39.       }, (item: string) => item)
40.     }.cachedCount(5)
41.   }
42. }

点击LazyForEach的子组件时，首先调用数据源data的pushData方法。此方法会在数据源末尾添加数据，并调用notifyDataAdd方法。notifyDataAdd方法内部会调用listener.onDataAdd方法，通知LazyForEach有数据添加。LazyForEach接收到通知后，在该索引处新建子组件。

运行效果如下图所示。

**图4** LazyForEach添加数据

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.62602198990997454456435861984947:50001231000000:2800:BD6D6EBA93850953AFDA543EA8D0BC31714F78DB8B813CB3CB11BF08BCF42B31.gif)

**删除数据**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public getAllData(): string[] {
11.     return this.dataArray;
12.   }

13.   public pushData(data: string): void {
14.     this.dataArray.push(data);
15.   }

16.   public deleteData(index: number): void {
17.     this.dataArray.splice(index, 1);
18.     this.notifyDataDelete(index);
19.   }
20. }

21. @Entry
22. @Component
23. struct MyComponent {
24.   private data: MyDataSource = new MyDataSource();

25.   aboutToAppear() {
26.     for (let i = 0; i <= 20; i++) {
27.       this.data.pushData(`Hello ${i}`);
28.     }
29.   }

30.   build() {
31.     List({ space: 3 }) {
32.       LazyForEach(this.data, (item: string, index: number) => {
33.         ListItem() {
34.           Row() {
35.             Text(item).fontSize(50)
36.               .onAppear(() => {
37.                 console.info(`appear: ${item}`);
38.               })
39.           }.margin({ left: 10, right: 10 })
40.         }
41.         .onClick(() => {
42.           // 点击删除子组件
43.           this.data.deleteData(this.data.getAllData().indexOf(item));
44.         })
45.       }, (item: string) => item)
46.     }.cachedCount(5)
47.   }
48. }

点击LazyForEach的子组件时，调用数据源data的deleteData方法。此方法删除数据源中对应索引的数据，并调用notifyDataDelete方法。notifyDataDelete方法内调用listener.onDataDelete方法，通知 LazyForEach删除该索引处的子组件。

运行效果如下图所示。

**图5** LazyForEach删除数据

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.17291737946690652466906958079562:50001231000000:2800:0185AD7BCCF7CF3B4B1AFF887C0D94057E4359F283EA9FA993D8C92442B2A0E9.gif)

**交换数据**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public getAllData(): string[] {
11.     return this.dataArray;
12.   }

13.   public pushData(data: string): void {
14.     this.dataArray.push(data);
15.   }

16.   public moveData(from: number, to: number): void {
17.     let temp: string = this.dataArray[from];
18.     this.dataArray[from] = this.dataArray[to];
19.     this.dataArray[to] = temp;
20.     this.notifyDataMove(from, to);
21.   }
22. }

23. @Entry
24. @Component
25. struct MyComponent {
26.   private moved: number[] = [];
27.   private data: MyDataSource = new MyDataSource();

28.   aboutToAppear() {
29.     for (let i = 0; i <= 20; i++) {
30.       this.data.pushData(`Hello ${i}`);
31.     }
32.   }

33.   build() {
34.     List({ space: 3 }) {
35.       LazyForEach(this.data, (item: string, index: number) => {
36.         ListItem() {
37.           Row() {
38.             Text(item).fontSize(50)
39.               .onAppear(() => {
40.                 console.info(`appear: ${item}`);
41.               })
42.           }.margin({ left: 10, right: 10 })
43.         }
44.         .onClick(() => {
45.           this.moved.push(this.data.getAllData().indexOf(item));
46.           if (this.moved.length === 2) {
47.             // 点击交换子组件
48.             this.data.moveData(this.moved[0], this.moved[1]);
49.             this.moved = [];
50.           }
51.         })
52.       }, (item: string) => item)
53.     }.cachedCount(5)
54.   }
55. }

首次点击LazyForEach的子组件时，将要移动的数据索引存储在moved成员变量中。再次点击LazyForEach的另一个子组件时，将首次点击的子组件移到此处。调用数据源data的moveData方法，该方法将数据源中的数据移动到预期位置，并调用notifyDataMove方法。notifyDataMove方法会调用listener.onDataMove方法，通知LazyForEach在该处有数据需要移动。LazyForEach将from和to索引处的子组件进行位置调换。

运行效果如下图所示。

**图6** LazyForEach交换数据

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.06958948193021443493944577970577:50001231000000:2800:B069B3FBDAD59FD747FE9558F79148135BDFBF8B50BD3CA88F2518583E845261.gif)

**改变单个数据**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.   }

13.   public changeData(index: number, data: string): void {
14.     this.dataArray.splice(index, 1, data);
15.     this.notifyDataChange(index);
16.   }
17. }

18. @Entry
19. @Component
20. struct MyComponent {
21.   private data: MyDataSource = new MyDataSource();

22.   aboutToAppear() {
23.     for (let i = 0; i <= 20; i++) {
24.       this.data.pushData(`Hello ${i}`);
25.     }
26.   }

27.   build() {
28.     List({ space: 3 }) {
29.       LazyForEach(this.data, (item: string, index: number) => {
30.         ListItem() {
31.           Row() {
32.             Text(item).fontSize(50)
33.               .onAppear(() => {
34.                 console.info(`appear: ${item}`);
35.               })
36.           }.margin({ left: 10, right: 10 })
37.         }
38.         .onClick(() => {
39.           this.data.changeData(index, item + '00');
40.         })
41.       }, (item: string) => item)
42.     }.cachedCount(5)
43.   }
44. }

点击LazyForEach的子组件时，首先改变当前数据，然后调用数据源data的changeData方法。changeData 方法会调用notifyDataChange方法，该方法又会调用listener.onDataChange方法，通知LazyForEach组件数据发生变化。LazyForEach会在对应索引处重建子组件。

运行效果如下图所示。

**图7** LazyForEach改变单个数据

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.62099682252848888306333469503206:50001231000000:2800:637AA3D270D377EE902FE7D57182ED1E0B008BB01D7DE58126D948A69203D225.gif)

**改变多个数据**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.   }

13.   public reloadData(): void {
14.     this.notifyDataReload();
15.   }

16.   public modifyAllData(): void {
17.     this.dataArray = this.dataArray.map((item: string) => {
18.       return item + '0';
19.     });
20.   }
21. }

22. @Entry
23. @Component
24. struct MyComponent {
25.   private data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(`Hello ${i}`);
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: string, index: number) => {
34.         ListItem() {
35.           Row() {
36.             Text(item).fontSize(50)
37.               .onAppear(() => {
38.                 console.info(`appear: ${item}`);
39.               })
40.           }.margin({ left: 10, right: 10 })
41.         }
42.         .onClick(() => {
43.           this.data.modifyAllData();
44.           this.data.reloadData();
45.         })
46.       }, (item: string) => item)
47.     }.cachedCount(5)
48.   }
49. }

点击LazyForEach的子组件时，首先调用data的modifyAllData方法修改数据源中的所有数据，然后调用数据源的reloadData方法。该方法内会调用notifyDataReload方法，notifyDataReload方法内会调用listener.onDataReloaded方法，通知LazyForEach重建所有子节点。LazyForEach会将原数据项和新数据项进行键值比对，若键值相同则使用缓存，若键值不同则重新构建。

运行效果如下图所示。

**图8** LazyForEach改变多个数据

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.28700881958198316762323198860955:50001231000000:2800:F116E78D90BD264BA00C4A42AF614C09147F717F86B7B23825AAEFACAC64EBC2.gif)

**精准批量修改数据**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public operateData(): void {
11.     console.info(`[${this.dataArray.join(', ')}]`);
12.     this.dataArray.splice(4, 0, this.dataArray[1]);
13.     this.dataArray.splice(1, 1);
14.     let temp = this.dataArray[4];
15.     this.dataArray[4] = this.dataArray[6];
16.     this.dataArray[6] = temp;
17.     this.dataArray.splice(8, 0, 'Hello 1', 'Hello 2');
18.     this.dataArray.splice(12, 2);
19.     console.info(`[${this.dataArray.join(', ')}]`);
20.     this.notifyDatasetChange([
21.       { type: DataOperationType.MOVE, index: { from: 1, to: 3 } },
22.       { type: DataOperationType.EXCHANGE, index: { start: 4, end: 6 } },
23.       { type: DataOperationType.ADD, index: 8, count: 2 },
24.       { type: DataOperationType.DELETE, index: 10, count: 2 }]);
25.   }

26.   public init(): void {
27.     this.dataArray.splice(0, 0, 'Hello a', 'Hello b', 'Hello c', 'Hello d', 'Hello e', 'Hello f', 'Hello g', 'Hello h',
28.       'Hello i', 'Hello j', 'Hello k', 'Hello l', 'Hello m', 'Hello n', 'Hello o', 'Hello p', 'Hello q', 'Hello r');
29.   }
30. }

31. @Entry
32. @Component
33. struct MyComponent {
34.   private data: MyDataSource = new MyDataSource();

35.   aboutToAppear() {
36.     this.data.init();
37.   }

38.   build() {
39.     Column() {
40.       Text('change data')
41.         .fontSize(10)
42.         .backgroundColor(Color.Blue)
43.         .fontColor(Color.White)
44.         .borderRadius(50)
45.         .padding(5)
46.         .onClick(() => {
47.           this.data.operateData();
48.         })
49.       List({ space: 3 }) {
50.         LazyForEach(this.data, (item: string, index: number) => {
51.           ListItem() {
52.             Row() {
53.               Text(item).fontSize(35)
54.                 .onAppear(() => {
55.                   console.info(`appear: ${item}`);
56.                 })
57.             }.margin({ left: 10, right: 10 })
58.           }

59.         }, (item: string) => item + new Date().getTime())
60.       }.cachedCount(5)
61.     }
62.   }
63. }

onDatasetChange接口允许开发者一次性通知LazyForEach进行数据添加、删除、移动和交换等操作。在上述例子中，点击“change data”文本后，第二项数据被移动到第四项位置，第五项与第七项数据交换位置，并且从第九项开始添加了数据"Hello 1"和"Hello 2"，同时从第十一项开始删除了两项数据。

**图9** LazyForEach改变多个数据

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.07428604698035507193124668580513:50001231000000:2800:98B1CE66AAF17CEE438678D5CD60AE049E9060CCB1E391F8DFB81271C12A115F.gif)

第二个例子，直接给数组赋值，不涉及 splice 操作。operations直接从比较原数组和新数组得到。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public operateData(): void {
11.     this.dataArray =
12.       ['Hello x', 'Hello 1', 'Hello 2', 'Hello b', 'Hello c', 'Hello e', 'Hello d', 'Hello f', 'Hello g', 'Hello h'];
13.     this.notifyDatasetChange([
14.       { type: DataOperationType.CHANGE, index: 0 },
15.       { type: DataOperationType.ADD, index: 1, count: 2 },
16.       { type: DataOperationType.EXCHANGE, index: { start: 3, end: 4 } },
17.     ]);
18.   }

19.   public init(): void {
20.     this.dataArray = ['Hello a', 'Hello b', 'Hello c', 'Hello d', 'Hello e', 'Hello f', 'Hello g', 'Hello h'];
21.   }
22. }

23. @Entry
24. @Component
25. struct MyComponent {
26.   private data: MyDataSource = new MyDataSource();

27.   aboutToAppear() {
28.     this.data.init();
29.   }

30.   build() {
31.     Column() {
32.       Text('Multi-Data Change')
33.         .fontSize(10)
34.         .backgroundColor(Color.Blue)
35.         .fontColor(Color.White)
36.         .borderRadius(50)
37.         .padding(5)
38.         .onClick(() => {
39.           this.data.operateData();
40.         })
41.       List({ space: 3 }) {
42.         LazyForEach(this.data, (item: string, index: number) => {
43.           ListItem() {
44.             Row() {
45.               Text(item).fontSize(35)
46.                 .onAppear(() => {
47.                   console.info(`appear: ${item}`);
48.                 })
49.             }.margin({ left: 10, right: 10 })
50.           }

51.         }, (item: string) => item + new Date().getTime())
52.       }.cachedCount(5)
53.     }
54.   }
55. }

**图10** LazyForEach改变多个数据

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.50988095528600364935076937749452:50001231000000:2800:AEA828D6567ADE3D49349EF4045D179CD861CCA2C1DF505CF6F230E764481ECC.gif)

使用该接口时请注意以下事项。

1. 不要将onDatasetChange与其他操作数据的接口混用。
    
2. 传入onDatasetChange的operations中，每一项operation的index均从修改前的原数组中查找。因此，operations中的index不总是与Datasource中的index一一对应，并且不能为负数。
    
    第一个例子清楚地显示了这一点:
    
    1. // 修改之前的数组
    2. ['Hello a','Hello b','Hello c','Hello d','Hello e','Hello f','Hello g','Hello h','Hello i','Hello j','Hello k','Hello l','Hello m','Hello n','Hello o','Hello p','Hello q','Hello r']
    3. // 修改之后的数组
    4. ['Hello a','Hello c','Hello d','Hello b','Hello g','Hello f','Hello e','Hello h','Hello 1','Hello 2','Hello i','Hello j','Hello m','Hello n','Hello o','Hello p','Hello q','Hello r']
    
    "Hello b" 从第2项变成第4项，因此第一个 operation 为 { type: DataOperationType.MOVE, index: { from: 1, to: 3 } }。
    
    "Hello e" 跟 "Hello g" 对调了，而 "Hello e" 在修改前的原数组中的 index=4，"Hello g" 在修改前的原数组中的 index=6, 因此第二个 operation 为 { type: DataOperationType.EXCHANGE, index: { start: 4, end: 6 } }。
    
    "Hello 1","Hello 2" 在 "Hello h" 之后插入，而 "Hello h" 在修改前的原数组中的 index=7，因此第三个 operation 为 { type: DataOperationType.ADD, index: 8, count: 2 }。
    
    "Hello k","Hello l" 被删除了，而 "Hello k" 在原数组中的 index=10，因此第四个 operation 为 { type: DataOperationType.DELETE, index: 10, count: 2 }。
    
3. 在同一个onDatasetChange批量处理数据时，如果多个DataOperation操作同一个index，只有第一个DataOperation生效。
    
4. 部分操作由开发者传入键值，LazyForEach不再重复调用keygenerator获取键值，开发者需保证传入键值的正确性。
    
5. 若操作集合中包含RELOAD操作，则其他操作均不生效。
    

## 高级用法

### 改变数据子属性

若仅靠LazyForEach的刷新机制，当item变化时若想更新子组件，需要将原来的子组件全部销毁再重新构建，在子组件结构较为复杂的情况下，靠改变键值去刷新渲染性能较低。因此框架提供了[@Observed装饰器和@ObjectLink装饰器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-observed-and-objectlink)机制进行深度观测，可以做到仅刷新使用了该属性的组件，提高渲染性能。开发者可根据其自身业务特点选择使用哪种刷新方式。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Observed
16. class StringData {
17.   message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @Component
24. struct MyComponent {
25.   private data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           ChildComponent({ data: item })
36.         }
37.         .onClick(() => {
38.           item.message += '0';
39.         })
40.       }, (item: StringData, index: number) => index.toString())
41.     }.cachedCount(5)
42.   }
43. }

44. @Component
45. struct ChildComponent {
46.   @ObjectLink data: StringData;

47.   build() {
48.     Row() {
49.       Text(this.data.message).fontSize(50)
50.         .onAppear(() => {
51.           console.info(`appear: ${this.data.message}`);
52.         })
53.     }.margin({ left: 10, right: 10 })
54.   }
55. }

点击LazyForEach子组件改变item.message时，重渲染依赖ChildComponent的@ObjectLink成员变量对子属性的监听。框架仅刷新Text(this.data.message)，不会重建整个ListItem子组件。

**图11** LazyForEach改变数据子属性

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.86573944337673717607837165555306:50001231000000:2800:70AF9D1190DECEB7D69A19AF66E2268801F6B65CDDE23F79169F66ED5B8014D0.gif)

### 使用状态管理V2

状态管理V2提供[@ObservedV2装饰器和@Trace装饰器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-observedv2-and-trace)，用于实现属性的深度观测。使用[@Local装饰器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-local)和[@Param装饰器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-param)，可以管理子组件的刷新，仅刷新使用了对应属性的组件。

**嵌套类属性变化观测**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. class StringData {
16.   firstLayer: FirstLayer;

17.   constructor(firstLayer: FirstLayer) {
18.     this.firstLayer = firstLayer;
19.   }
20. }

21. class FirstLayer {
22.   secondLayer: SecondLayer;

23.   constructor(secondLayer: SecondLayer) {
24.     this.secondLayer = secondLayer;
25.   }
26. }

27. class SecondLayer {
28.   thirdLayer: ThirdLayer;

29.   constructor(thirdLayer: ThirdLayer) {
30.     this.thirdLayer = thirdLayer;
31.   }
32. }

33. @ObservedV2
34. class ThirdLayer {
35.   @Trace fourthLayer: string;

36.   constructor(fourthLayer: string) {
37.     this.fourthLayer = fourthLayer;
38.   }
39. }

40. @Entry
41. @ComponentV2
42. struct MyComponent {
43.   private data: MyDataSource = new MyDataSource();

44.   aboutToAppear() {
45.     for (let i = 0; i <= 20; i++) {
46.       this.data.pushData(new StringData(new FirstLayer(new SecondLayer(new ThirdLayer(`Hello ${i}`)))));
47.     }
48.   }

49.   build() {
50.     List({ space: 3 }) {
51.       LazyForEach(this.data, (item: StringData, index: number) => {
52.         ListItem() {
53.           Text(item.firstLayer.secondLayer.thirdLayer.fourthLayer).fontSize(50)
54.             .onClick(() => {
55.               item.firstLayer.secondLayer.thirdLayer.fourthLayer += '!';
56.             })
57.         }
58.       }, (item: StringData, index: number) => index.toString())
59.     }.cachedCount(5)
60.   }
61. }

@ObservedV2与@Trace用于装饰类以及类中的属性，配合使用能深度观测被装饰的类和属性。示例中，展示了深度嵌套类结构下，通过@ObservedV2和@Trace实现对多层嵌套属性变化的观测和子组件刷新。当点击子组件Text修改被@Trace修饰的嵌套类最内层的类成员属性时，仅重新渲染依赖了该属性的组件。

**组件内部状态**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @ObservedV2
16. class StringData {
17.   @Trace message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @ComponentV2
24. struct MyComponent {
25.   data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           Row() {

36.             Text(item.message).fontSize(50)
37.               .onClick(() => {
38.                 // 修改@ObservedV2装饰类中@Trace装饰的变量，触发刷新此处Text组件
39.                 item.message += '!';
40.               })
41.             ChildComponent()
42.           }
43.         }
44.       }, (item: StringData, index: number) => index.toString())
45.     }.cachedCount(5)
46.   }
47. }

48. @ComponentV2
49. struct ChildComponent {
50.   @Local message: string = '?';

51.   build() {
52.     Row() {
53.       Text(this.message).fontSize(50)
54.         .onClick(() => {
55.           // 修改@Local装饰的变量，触发刷新此处Text组件
56.           this.message += '?';
57.         })
58.     }
59.   }
60. }

@Local使得自定义组件内被修饰的变量具有观测其变化的能力，该变量必须在组件内部进行初始化。示例中，点击Text组件修改item.message触发变量更新并刷新使用该变量的组件，ChildComponent中@Local装饰的变量message变化时也能刷新子组件。

**组件外部输入**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @ObservedV2
16. class StringData {
17.   @Trace message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @ComponentV2
24. struct MyComponent {
25.   data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           ChildComponent({ data: item.message })
36.             .onClick(() => {
37.               item.message += '!';
38.             })
39.         }
40.       }, (item: StringData, index: number) => index.toString())
41.     }.cachedCount(5)
42.   }
43. }

44. @ComponentV2
45. struct ChildComponent {
46.   @Param @Require data: string = '';

47.   build() {
48.     Row() {
49.       Text(this.data).fontSize(50)
50.     }
51.   }
52. }

使用@Param装饰器，子组件可以接受外部输入参数，实现父子组件间的数据同步。在MyComponent中创建子组件时，传递item.message，并用@Param修饰的变量data与其关联。点击ListItem中的组件修改item.message，数据变化会从父组件传递到子组件，触发子组件刷新。

### 拖拽排序

当LazyForEach在List组件下使用，并且设置了[onMove](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-drag-sorting#onmove)事件，可以使能拖拽排序。拖拽排序释放后，如果数据位置发生变化，将触发onMove事件，上报原始索引号和目标索引号。在onMove事件中，根据上报的索引号修改数据源。修改数据源时，无需调用DataChangeListener接口通知数据源变化。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public moveDataWithoutNotify(from: number, to: number): void {
11.     let tmp = this.dataArray.splice(from, 1);
12.     this.dataArray.splice(to, 0, tmp[0]);
13.   }

14.   public pushData(data: string): void {
15.     this.dataArray.push(data);
16.     this.notifyDataAdd(this.dataArray.length - 1);
17.   }
18. }

19. @Entry
20. @Component
21. struct Parent {
22.   private data: MyDataSource = new MyDataSource();

23.   aboutToAppear(): void {
24.     for (let i = 0; i < 100; i++) {
25.       this.data.pushData(i.toString());
26.     }
27.   }

28.   build() {
29.     Row() {
30.       List() {
31.         LazyForEach(this.data, (item: string) => {
32.           ListItem() {
33.             Text(item.toString())
34.               .fontSize(16)
35.               .textAlign(TextAlign.Center)
36.               .size({ height: 100, width: '100%' })
37.           }.margin(10)
38.           .borderRadius(10)
39.           .backgroundColor('#FFFFFFFF')
40.         }, (item: string) => item)
41.           .onMove((from: number, to: number) => {
42.             this.data.moveDataWithoutNotify(from, to);
43.           })
44.       }
45.       .width('100%')
46.       .height('100%')
47.       .backgroundColor('#FFDCDCDC')
48.     }
49.   }
50. }

**图12** LazyForEach拖拽排序效果图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.79872815745800611896550687727063:50001231000000:2800:3CBB47BD9F68E7E5759AB5EB2A0458783C6C097AD7A72E9D8DEFFD71F389AA60.gif)

## 常见问题

### 渲染结果非预期

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }

14.   public deleteData(index: number): void {
15.     this.dataArray.splice(index, 1);
16.     this.notifyDataDelete(index);
17.   }
18. }

19. @Entry
20. @Component
21. struct MyComponent {
22.   private data: MyDataSource = new MyDataSource();

23.   aboutToAppear() {
24.     for (let i = 0; i <= 20; i++) {
25.       this.data.pushData(`Hello ${i}`);
26.     }
27.   }

28.   build() {
29.     List({ space: 3 }) {
30.       LazyForEach(this.data, (item: string, index: number) => {
31.         ListItem() {
32.           Row() {
33.             Text(item).fontSize(50)
34.               .onAppear(() => {
35.                 console.info(`appear: ${item}`);
36.               })
37.           }.margin({ left: 10, right: 10 })
38.         }
39.         .onClick(() => {
40.           // 点击删除子组件
41.           this.data.deleteData(index);
42.         })
43.       }, (item: string) => item)
44.     }.cachedCount(5)
45.   }
46. }

**图13** LazyForEach删除数据非预期

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.33030181564705804490569896874694:50001231000000:2800:0B8A6F6E6E78CAFF93114041CEB16D0AF6C4FD463E13661C3F01BDA4F15F11F4.gif)

多次点击子组件时，发现删除的不一定是点击的那个子组件。原因在于删除某个子组件后，该子组件之后的数据项的index应减1，但实际后续数据项对应的子组件仍使用最初分配的index，itemGenerator中的index未更新，导致删除结果与预期不符。

修复代码如下。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }

14.   public deleteData(index: number): void {
15.     this.dataArray.splice(index, 1);
16.     this.notifyDataDelete(index);
17.   }

18.   public reloadData(): void {
19.     this.notifyDataReload();
20.   }
21. }

22. @Entry
23. @Component
24. struct MyComponent {
25.   private data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(`Hello ${i}`);
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: string, index: number) => {
34.         ListItem() {
35.           Row() {
36.             Text(item).fontSize(50)
37.               .onAppear(() => {
38.                 console.info(`appear: ${item}`);
39.               })
40.           }.margin({ left: 10, right: 10 })
41.         }
42.         .onClick(() => {
43.           // 点击删除子组件
44.           this.data.deleteData(index);
45.           // 重置所有子组件的index索引
46.           this.data.reloadData();
47.         })
48.       }, (item: string, index: number) => item + index.toString())
49.     }.cachedCount(5)
50.   }
51. }

在删除一个数据项后调用reloadData方法，重建后面的数据项，以达到更新index索引的目的。要保证reloadData方法重建数据项，必须保证数据项能生成新的key。这里用了item + index.toString()保证被删除数据项后面的数据项都被重建。如果用item + Date.now().toString()替代，那么所有数据项都生成新的key，导致所有数据项都被重建。这种方法，效果是一样的，只是性能略差。

**图14** 修复LazyForEach删除数据非预期

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.79849597709093500147638956133738:50001231000000:2800:A54992B562DCACF96248560CC752C5FFA9FF7EF677DBE51080624BBFED70B7D3.gif)

### 重渲染时图片闪烁

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }

14.   public reloadData(): void {
15.     this.notifyDataReload();
16.   }
17. }

18. class StringData {
19.   message: string;
20.   imgSrc: Resource;

21.   constructor(message: string, imgSrc: Resource) {
22.     this.message = message;
23.     this.imgSrc = imgSrc;
24.   }
25. }

26. @Entry
27. @Component
28. struct MyComponent {
29.   private moved: number[] = [];
30.   private data: MyDataSource = new MyDataSource();

31.   aboutToAppear() {
32.     for (let i = 0; i <= 20; i++) {
33.       // 此处'app.media.img'仅作示例，请开发者自行替换，否则imageSource创建失败会导致后续无法正常执行。
34.       this.data.pushData(new StringData(`Hello ${i}`, $r('app.media.img')));
35.     }
36.   }

37.   build() {
38.     List({ space: 3 }) {
39.       LazyForEach(this.data, (item: StringData, index: number) => {
40.         ListItem() {
41.           Column() {
42.             Text(item.message).fontSize(50)
43.               .onAppear(() => {
44.                 console.info(`appear: ${item.message}`);
45.               })
46.             Image(item.imgSrc)
47.               .width(500)
48.               .height(200)
49.           }.margin({ left: 10, right: 10 })
50.         }
51.         .onClick(() => {
52.           item.message += '00';
53.           this.data.reloadData();
54.         })
55.       }, (item: StringData, index: number) => item.message) // 修改message属性会导致键值变化
56.     }.cachedCount(5)
57.   }
58. }

**图15** LazyForEach仅改变文字但是图片闪烁问题

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.48621283665703744066328107905709:50001231000000:2800:2D31E1D751C3C7466095D037121AFB372A71FD28639CED9EC76CAE982DF85599.gif)

单击ListItem子组件时，只改变了数据项的message属性，但因为键值发生变化，导致整个ListItem被重建。由于Image组件异步刷新，视觉上图片会闪烁。解决方法是保持键值不变，并使用@ObjectLink和@Observed单独刷新子组件Text。

修复代码如下。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. // @Observed类装饰器 和 @ObjectLink 用于在涉及嵌套对象或数组的场景中进行双向数据同步
16. @Observed
17. class StringData {
18.   message: string;
19.   imgSrc: Resource;

20.   constructor(message: string, imgSrc: Resource) {
21.     this.message = message;
22.     this.imgSrc = imgSrc;
23.   }
24. }

25. @Entry
26. @Component
27. struct MyComponent {
28.   private data: MyDataSource = new MyDataSource();

29.   aboutToAppear() {
30.     for (let i = 0; i <= 20; i++) {
31.       // 此处'app.media.img'仅作示例，请开发者自行替换，否则imageSource创建失败会导致后续无法正常执行。
32.       this.data.pushData(new StringData(`Hello ${i}`, $r('app.media.img')));
33.     }
34.   }

35.   build() {
36.     List({ space: 3 }) {
37.       LazyForEach(this.data, (item: StringData, index: number) => {
38.         ListItem() {
39.           ChildComponent({ data: item })
40.         }
41.         .onClick(() => {
42.           item.message += '0';
43.         })
44.       }, (item: StringData, index: number) => index.toString()) // 键值不受message属性影响
45.     }.cachedCount(5)
46.   }
47. }

48. @Component
49. struct ChildComponent {
50.   // 用状态变量来驱动UI刷新，而不是通过Lazyforeach的api来驱动UI刷新
51.   @ObjectLink data: StringData;

52.   build() {
53.     Column() {
54.       Text(this.data.message).fontSize(50)
55.         .onAppear(() => {
56.           console.info(`appear: ${this.data.message}`);
57.         })
58.       Image(this.data.imgSrc)
59.         .width(500)
60.         .height(200)
61.     }.margin({ left: 10, right: 10 })
62.   }
63. }

**图16** 修复LazyForEach仅改变文字但是图片闪烁问题

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.01120955685363301686263583087538:50001231000000:2800:7B4CBEEF4377C8CFCD7C1D2653EEE663B602B647B197CA5CBBCE438E8F1A004E.gif)

### @ObjectLink属性变化UI未更新

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Observed
16. class StringData {
17.   message: NestedString;

18.   constructor(message: NestedString) {
19.     this.message = message;
20.   }
21. }

22. @Observed
23. class NestedString {
24.   message: string;

25.   constructor(message: string) {
26.     this.message = message;
27.   }
28. }

29. @Entry
30. @Component
31. struct MyComponent {
32.   private moved: number[] = [];
33.   private data: MyDataSource = new MyDataSource();

34.   aboutToAppear() {
35.     for (let i = 0; i <= 20; i++) {
36.       this.data.pushData(new StringData(new NestedString(`Hello ${i}`)));
37.     }
38.   }

39.   build() {
40.     List({ space: 3 }) {
41.       LazyForEach(this.data, (item: StringData, index: number) => {
42.         ListItem() {
43.           ChildComponent({ data: item })
44.         }
45.         .onClick(() => {
46.           item.message.message += '0';
47.         })
48.       }, (item: StringData, index: number) => item.message.message + index.toString())
49.     }.cachedCount(5)
50.   }
51. }

52. @Component
53. struct ChildComponent {
54.   @ObjectLink data: StringData;

55.   build() {
56.     Row() {
57.       Text(this.data.message.message).fontSize(50)
58.         .onAppear(() => {
59.           console.info(`appear: ${this.data.message.message}`);
60.         })
61.     }.margin({ left: 10, right: 10 })
62.   }
63. }

**图17** ObjectLink属性变化后UI未更新

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.79945457127792213556459215072088:50001231000000:2800:649B4C86EEF3CC6810590552342EC634894312FC6EEC775CD5EC160421539CD7.gif)

@ObjectLink装饰的成员变量仅能监听到其子属性的变化，无法监听深层嵌套属性，因此，只能通过修改子属性来通知组件重新渲染。具体请查看[@ObjectLink装饰器与@Observed装饰器的详细使用方法和限制条件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-observed-and-objectlink)。

修复代码如下。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Observed
16. class StringData {
17.   message: NestedString;

18.   constructor(message: NestedString) {
19.     this.message = message;
20.   }
21. }

22. @Observed
23. class NestedString {
24.   message: string;

25.   constructor(message: string) {
26.     this.message = message;
27.   }
28. }

29. @Entry
30. @Component
31. struct MyComponent {
32.   private moved: number[] = [];
33.   private data: MyDataSource = new MyDataSource();

34.   aboutToAppear() {
35.     for (let i = 0; i <= 20; i++) {
36.       this.data.pushData(new StringData(new NestedString(`Hello ${i}`)));
37.     }
38.   }

39.   build() {
40.     List({ space: 3 }) {
41.       LazyForEach(this.data, (item: StringData, index: number) => {
42.         ListItem() {
43.           ChildComponent({ data: item })
44.         }
45.         .onClick(() => {
46.           // @ObjectLink装饰的成员变量仅能监听到其子属性的变化，再深入嵌套的属性便无法观测到
47.           item.message = new NestedString(item.message.message + '0');
48.         })
49.       }, (item: StringData, index: number) => item.message.message + index.toString())
50.     }.cachedCount(5)
51.   }
52. }

53. @Component
54. struct ChildComponent {
55.   @ObjectLink data: StringData;

56.   build() {
57.     Row() {
58.       Text(this.data.message.message).fontSize(50)
59.         .onAppear(() => {
60.           console.info(`appear: ${this.data.message.message}`);
61.         })
62.     }.margin({ left: 10, right: 10 })
63.   }
64. }

**图18** 修复ObjectLink属性变化后UI更新

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.58173914423403132155059269662543:50001231000000:2800:B9B3C60C3A46C0BA4750FE94134F1A7964AC03C23FDF725C6FB6364F5BD8AA0E.gif)

### 在List内使用屏幕闪烁

在List的onScrollIndex方法中调用onDataReloaded可能会导致屏幕闪烁。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }

14.   operateData(): void {
15.     const totalCount = this.dataArray.length;
16.     const batch = 5;
17.     for (let i = totalCount; i < totalCount + batch; i++) {
18.       this.dataArray.push(`Hello ${i}`);
19.     }
20.     this.notifyDataReload();
21.   }
22. }

23. @Entry
24. @Component
25. struct MyComponent {
26.   private moved: number[] = [];
27.   private data: MyDataSource = new MyDataSource();

28.   aboutToAppear() {
29.     for (let i = 0; i <= 10; i++) {
30.       this.data.pushData(`Hello ${i}`);
31.     }
32.   }

33.   build() {
34.     List({ space: 3 }) {
35.       LazyForEach(this.data, (item: string, index: number) => {
36.         ListItem() {
37.           Row() {
38.             Text(item)
39.               .width('100%')
40.               .height(80)
41.               .backgroundColor(Color.Gray)
42.               .onAppear(() => {
43.                 console.info(`appear: ${item}`);
44.               })
45.           }.margin({ left: 10, right: 10 })
46.         }
47.       }, (item: string) => item)
48.     }.cachedCount(10)
49.     .onScrollIndex((start, end, center) => {
50.       if (end === this.data.totalCount() - 1) {
51.         console.info('scroll to end');
52.         this.data.operateData();
53.       }
54.     })
55.   }
56. }

**图19** 当List下拉到底时，屏幕闪烁

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.85350843901989014204475387751140:50001231000000:2800:892588CB6EDD57E85A3EF927658D47E07265353D14C3043A6706849DB6334926.gif)

使用onDatasetChange代替onDataReloaded，不仅可以修复闪屏问题，还能提升加载性能。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }

14.   operateData(): void {
15.     const totalCount = this.dataArray.length;
16.     const batch = 5;
17.     for (let i = totalCount; i < totalCount + batch; i++) {
18.       this.dataArray.push(`Hello ${i}`);
19.     }
20.     // 替换 notifyDataReload
21.     this.notifyDatasetChange([{ type: DataOperationType.ADD, index: totalCount - 1, count: batch }]);
22.   }
23. }

24. @Entry
25. @Component
26. struct MyComponent {
27.   private moved: number[] = [];
28.   private data: MyDataSource = new MyDataSource();

29.   aboutToAppear() {
30.     for (let i = 0; i <= 10; i++) {
31.       this.data.pushData(`Hello ${i}`);
32.     }
33.   }

34.   build() {
35.     List({ space: 3 }) {
36.       LazyForEach(this.data, (item: string, index: number) => {
37.         ListItem() {
38.           Row() {
39.             Text(item)
40.               .width('100%')
41.               .height(80)
42.               .backgroundColor(Color.Gray)
43.               .onAppear(() => {
44.                 console.info(`appear: ${item}`);
45.               })
46.           }.margin({ left: 10, right: 10 })
47.         }
48.       }, (item: string) => item)
49.     }.cachedCount(10)
50.     .onScrollIndex((start, end, center) => {
51.       if (end === this.data.totalCount() - 1) {
52.         console.info('scroll to end');
53.         this.data.operateData();
54.       }
55.     })
56.   }
57. }

**图20** 修复后，当List下拉到底时，屏幕不闪烁

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163946.89014012020159826788367943584961:50001231000000:2800:E7615FF069B82F7D77529D6C462ADC4FE501AA987AFE87026A959211CF573A2C.gif)

### 组件复用渲染异常

@Reusable装饰器与[@ComponentV2装饰器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-componentv2)混用会导致组件渲染异常。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. class StringData {
16.   message: string;

17.   constructor(message: string) {
18.     this.message = message;
19.   }
20. }

21. @Entry
22. @ComponentV2
23. struct MyComponent {
24.   data: MyDataSource = new MyDataSource();

25.   aboutToAppear() {
26.     for (let i = 0; i <= 30; i++) {
27.       this.data.pushData(new StringData(`Hello${i}`));
28.     }
29.   }

30.   build() {
31.     List({ space: 3 }) {
32.       LazyForEach(this.data, (item: StringData, index: number) => {
33.         ListItem() {
34.           ChildComponent({ data: item })
35.             .onAppear(() => {
36.               console.info(`onAppear: ${item.message}`);
37.             })
38.         }
39.       }, (item: StringData, index: number) => index.toString())
40.     }.cachedCount(5)
41.   }
42. }

43. @Reusable
44. @Component
45. struct ChildComponent {
46.   @State data: StringData = new StringData('');

47.   aboutToAppear(): void {
48.     console.info(`aboutToAppear: ${this.data.message}`);
49.   }

50.   aboutToRecycle(): void {
51.     console.info(`aboutToRecycle: ${this.data.message}`);
52.   }

53.   // 对复用的组件进行数据更新
54.   aboutToReuse(params: Record<string, ESObject>): void {
55.     this.data = params.data as StringData;
56.     console.info(`aboutToReuse: ${this.data.message}`);
57.   }

58.   build() {
59.     Row() {
60.       Text(this.data.message).fontSize(50)
61.     }
62.   }
63. }

反例中，在@ComponentV2装饰的组件MyComponent中，LazyForEach列表使用了@Reusable装饰的组件ChildComponent，导致组件渲染失败。从日志中可以看到，组件触发了onAppear，但没有触发aboutToAppear。

将@ComponentV2修改为[@Component](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components#component)可以修复渲染异常。修复后，当滑动事件触发组件节点下树时，对应的可复用组件ChildComponent会被加入复用缓存，而非被销毁，并触发aboutToRecycle事件，打印日志信息。当列表滑动，出现新节点时，会将可复用的组件从复用缓存中重新加入到节点树，触发aboutToReuse刷新组件数据，并打印日志信息。

### 组件不刷新

开发者需要定义合适的键值生成函数，返回与目标数据相关联的键值。目标数据发生改变时，LazyForEach识别到键值改变才会刷新对应组件。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }

14.   public updateAllData(): void {
15.     this.dataArray = this.dataArray.map((item: string) => item + `!`);
16.     this.notifyDataReload();
17.   }
18. }

19. @Entry
20. @Component
21. struct MyComponent {
22.   private data: MyDataSource = new MyDataSource();

23.   aboutToAppear() {
24.     for (let i = 0; i <= 20; i++) {
25.       this.data.pushData(`Hello ${i}`);
26.     }
27.   }

28.   build() {
29.     Column() {
30.       Button(`update all`)
31.         .onClick(() => {
32.           this.data.updateAllData();
33.         })
34.       List({ space: 3 }) {
35.         LazyForEach(this.data, (item: string) => {
36.           ListItem() {
37.             Text(item).fontSize(50)
38.           }
39.         })
40.       }.cachedCount(5)
41.     }
42.   }
43. }

**图21** 点击按钮更新数据，组件不会刷新

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163947.29975353379451077941688498548567:50001231000000:2800:65B08417A8AE9D713213A7F999A7EC7CF443E23F528D9A61BF3FAFABC98D5F99.gif)

LazyForEach依赖生成的键值判断是否刷新子组件，如果更新的数据没有改变键值（如示例中开发者没有定义键值生成函数，此时键值仅与组件索引index有关，更新数据时键值不变），则LazyForEach不会刷新对应组件。

1. LazyForEach(this.data, (item: string) => {
2.   ListItem() {
3.     Text(item).fontSize(50)
4.   }
5. }, (item: string) => item) // 定义键值生成函数

**图22** 定义键值生成函数后，点击按钮更新数据，组件刷新

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163947.51812777395659702003813931248026:50001231000000:2800:A4335038F336190CD9CEC2C8DE8EBED1224B3B53A3F9CCFFDB0E9A23146A851B.gif)

### 懒加载失效

支持数据懒加载的父组件基于自身和子组件的高度或宽度计算可视范围内应布局的子节点数量，高度或宽度的缺失会导致部分场景懒加载失效。如下示例，在纵向布局中，首次渲染时子组件的高度缺失，所有数据项对应组件都会被创建。

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   public dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Entry
16. @Component
17. struct MyComponent {
18.   private data: MyDataSource = new MyDataSource();

19.   aboutToAppear() {
20.     for (let i = 0; i <= 100; i++) {
21.       this.data.pushData(``);
22.     }
23.   }

24.   build() {
25.     List() {
26.       LazyForEach(this.data, (item: string, index: number) => {
27.         ChildComponent({ message: item, index: index })
28.         // 子组件未设置默认高度，首次渲染时所有数据项对应组件都被创建
29.         // .height(60)
30.       }, (item: string, index: number) => item + index)
31.     }
32.     .cachedCount(2)
33.   }
34. }

35. @Component
36. struct ChildComponent {
37.   message: string = ``;
38.   index: number = -1;

39.   aboutToAppear(): void {
40.     console.info(`about to appear ${this.index}`);
41.   }

42.   build() {
43.     Text(this.message).fontSize(50)
44.   }
45. }

上述示例由于子组件ChildComponent的变量message初始值为空字符串，导致其内部的Text组件高度为 0，同时子组件未显式设置默认高度（如.height(60)），因此在首次渲染时所有子组件的高度均被计算为0。父组件List在基于高度计算可视范围时，判断所有子组件均位于可视区域内，导致懒加载机制失效，最终触发了全部数据项对应组件的创建（可通过日志观察到所有about to appear打印）。

为子组件设置默认高度，确保父组件能正确计算可视范围，从而恢复此场景下懒加载功能。

1. List() {
2.   LazyForEach(this.data, (item: string, index: number) => {
3.     ChildComponent({ message: item, index: index })
4.       // 设置子组件默认高度，首次渲染懒加载生效
5.       .height(60)
6.   }, (item: string, index: number) => item + index)
7. }
8. .cachedCount(2)

## BasicDataSource示例代码

### string类型数组的BasicDataSource代码

1. // BasicDataSource实现了IDataSource接口，用于管理listener监听，以及通知LazyForEach数据更新
2. class BasicDataSource implements IDataSource {
3.   private listeners: DataChangeListener[] = [];
4.   private originDataArray: string[] = [];

5.   public totalCount(): number {
6.     return this.originDataArray.length;
7.   }

8.   public getData(index: number): string {
9.     return this.originDataArray[index];
10.   }

11.   // 该方法为框架侧调用，为LazyForEach组件向其数据源处添加listener监听
12.   registerDataChangeListener(listener: DataChangeListener): void {
13.     if (this.listeners.indexOf(listener) < 0) {
14.       console.info('add listener');
15.       this.listeners.push(listener);
16.     }
17.   }

18.   // 该方法为框架侧调用，为对应的LazyForEach组件在数据源处去除listener监听
19.   unregisterDataChangeListener(listener: DataChangeListener): void {
20.     const pos = this.listeners.indexOf(listener);
21.     if (pos >= 0) {
22.       console.info('remove listener');
23.       this.listeners.splice(pos, 1);
24.     }
25.   }

26.   // 通知LazyForEach组件需要重载所有子组件
27.   notifyDataReload(): void {
28.     this.listeners.forEach(listener => {
29.       listener.onDataReloaded();
30.     });
31.   }

32.   // 通知LazyForEach组件需要在index对应索引处添加子组件
33.   notifyDataAdd(index: number): void {
34.     this.listeners.forEach(listener => {
35.       listener.onDataAdd(index);
36.       // 写法2：listener.onDatasetChange([{type: DataOperationType.ADD, index: index}]);
37.     });
38.   }

39.   // 通知LazyForEach组件在index对应索引处数据有变化，需要重建该子组件
40.   notifyDataChange(index: number): void {
41.     this.listeners.forEach(listener => {
42.       listener.onDataChange(index);
43.       // 写法2：listener.onDatasetChange([{type: DataOperationType.CHANGE, index: index}]);
44.     });
45.   }

46.   // 通知LazyForEach组件需要在index对应索引处删除该子组件
47.   notifyDataDelete(index: number): void {
48.     this.listeners.forEach(listener => {
49.       listener.onDataDelete(index);
50.       // 写法2：listener.onDatasetChange([{type: DataOperationType.DELETE, index: index}]);
51.     });
52.   }

53.   // 通知LazyForEach组件将from索引和to索引处的子组件进行交换
54.   notifyDataMove(from: number, to: number): void {
55.     this.listeners.forEach(listener => {
56.       listener.onDataMove(from, to);
57.       // 写法2：listener.onDatasetChange(
58.       //         [{type: DataOperationType.EXCHANGE, index: {start: from, end: to}}]);
59.     });
60.   }

61.   notifyDatasetChange(operations: DataOperation[]): void {
62.     this.listeners.forEach(listener => {
63.       listener.onDatasetChange(operations);
64.     });
65.   }
66. }

### StringData类型数组的BasicDataSource代码

1. class BasicDataSource implements IDataSource {
2.   private listeners: DataChangeListener[] = [];
3.   private originDataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.originDataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.originDataArray[index];
9.   }

10.   registerDataChangeListener(listener: DataChangeListener): void {
11.     if (this.listeners.indexOf(listener) < 0) {
12.       console.info('add listener');
13.       this.listeners.push(listener);
14.     }
15.   }

16.   unregisterDataChangeListener(listener: DataChangeListener): void {
17.     const pos = this.listeners.indexOf(listener);
18.     if (pos >= 0) {
19.       console.info('remove listener');
20.       this.listeners.splice(pos, 1);
21.     }
22.   }

23.   notifyDataReload(): void {
24.     this.listeners.forEach(listener => {
25.       listener.onDataReloaded();
26.     });
27.   }

28.   notifyDataAdd(index: number): void {
29.     this.listeners.forEach(listener => {
30.       listener.onDataAdd(index);
31.     });
32.   }

33.   notifyDataChange(index: number): void {
34.     this.listeners.forEach(listener => {
35.       listener.onDataChange(index);
36.     });
37.   }

38.   notifyDataDelete(index: number): void {
39.     this.listeners.forEach(listener => {
40.       listener.onDataDelete(index);
41.     });
42.   }

43.   notifyDataMove(from: number, to: number): void {
44.     this.listeners.forEach(listener => {
45.       listener.onDataMove(from, to);
46.     });
47.   }

48.   notifyDatasetChange(operations: DataOperation[]): void {
49.     this.listeners.forEach(listener => {
50.       listener.onDatasetChange(operations);
51.     });
52.   }
53. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-foreach "ForEach：循环渲染")
# LazyForEach迁移Repeat指南

更新时间: 2025-12-16 16:39

[Repeat](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat)是ArkUI在API version 12中新引入的循环渲染组件，相比[LazyForEach](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach)具有更简洁的API、更丰富的功能以及更强的性能优化能力。本指南帮助开发者将LazyForEach平滑地迁移到Repeat。

## 基础用法迁移

### 数据首次渲染

**LazyForEach示例**

LazyForEach根据数据源循环渲染子组件。

示例1中，在容器组件[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-layout-development-create-list)中使用LazyForEach，并基于数据源循环渲染出了一系列[Text](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-text-display)子组件。

**示例1 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Entry
16. @Component
17. struct MyComponent {
18.   private data: MyDataSource = new MyDataSource();

19.   aboutToAppear() {
20.     for (let i = 0; i <= 20; i++) {
21.       this.data.pushData(`Hello ${i}`);
22.     }
23.   }

24.   build() {
25.     List({ space: 3 }) {
26.       LazyForEach(this.data, (item: string) => {
27.         ListItem() {
28.           Row() {
29.             Text(item).fontSize(50)
30.               .onAppear(() => {
31.                 console.info(`appear: ${item}`);
32.               })
33.           }.margin({ left: 10, right: 10 })
34.         }
35.       }, (item: string) => item)
36.     }.cachedCount(5)
37.   }
38. }

以上是一个典型的使用LazyForEach循环渲染子组件的场景，下面将介绍如何将此示例迁移至Repeat。

**迁移步骤**

1. 使用状态管理V2装饰器。
    
    Repeat推荐和状态管理V2装饰器配合使用（[懒加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat#%E5%BE%AA%E7%8E%AF%E6%B8%B2%E6%9F%93%E8%83%BD%E5%8A%9B%E8%AF%B4%E6%98%8E)模式下只支持和状态管理V2装饰器配合使用）。如果之前使用的是状态管理V1装饰器，需要修改为状态管理V2装饰器。
    
    1. // 迁移前 - LazyForEach
    2. @Component // 状态管理V1
    3. struct MyComponent {
    4.   build() {
    5.     // ...
    6.     LazyForEach(...)
    7.     // ...
    8.   }
    9.   // ...其他属性、方法
    10. }
    
    11. // 迁移后 - Repeat
    12. @ComponentV2 // 状态管理V2
    13. struct MyComponent {
    14.   build() {
    15.     // ...
    16.     Repeat(...)
    17.     // ...
    18.   }
    19.   // ...其他属性、方法
    20. }
    
2. 迁移数据源。
    
    LazyForEach使用专用的数据结构[IDataSource](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#idatasource)作为数据源。迁移至Repeat后，不再使用IDataSource作为数据源，而是使用状态管理V2装饰的数组作为数据源。
    
    1. // 迁移前 - LazyForEach
    2. class MyDataSource implements IDataSource {
    3.   private dataArray: string[] = [];
    
    4.   public totalCount(): number {
    5.     return this.dataArray.length;
    6.   }
    
    7.   public getData(index: number): string {
    8.     return this.dataArray[index];
    9.   }
    
    10.   // ...其他方法
    11. }
    
    12. // 迁移后 - Repeat
    13. @Local data: Array<string> = [];
    
3. 迁移组件生成函数和键值生成函数。
    
    LazyForEach与Repeat均通过组件生成函数，为每一项数据创建一个子组件；通过键值生成函数，为每一项数据生成一个唯一的键值。
    
    从LazyForEach迁移至Repeat时，两者的语法存在差异。Repeat需要在[.each()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#each)或[.template()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#template)中设置组件生成函数，在[.key()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#key)中设置键值生成函数。
    
    1. // 迁移前 - LazyForEach
    2. List() {
    3.   LazyForEach(
    4.     this.data, // 数据源
    5.     (item: string, index: number) => { // 组件生成函数
    6.       ListItem() {
    7.         Text(item)
    8.       }
    9.     },
    10.     (item: string, index: number) => item // 键值生成函数
    11.   )
    12. }
    
    13. // 迁移后 - Repeat
    14. List() {
    15.   Repeat<string>(this.data) // 数据源
    16.     .each((repeatItem: RepeatItem<string>) => { // 组件生成函数
    17.       ListItem() {
    18.         Text(repeatItem.item)
    19.       }
    20.     })
    21.     .key((item: string, index: number) => item) // 键值生成函数
    22. }
    
4. 配置懒加载功能。
    
    Repeat具有[懒加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat#%E5%BE%AA%E7%8E%AF%E6%B8%B2%E6%9F%93%E8%83%BD%E5%8A%9B%E8%AF%B4%E6%98%8E)和[全量加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat#%E5%85%B3%E9%97%AD%E6%87%92%E5%8A%A0%E8%BD%BD)两种模式。
    
    - 全量加载模式渲染所有子节点（对标[ForEach](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-foreach)）。
    - 懒加载模式动态渲染屏幕区域和预加载区域内的子节点（需要与容器组件配合使用，对标LazyForEach）。
    
    从LazyForEach迁移至Repeat时，需要调用[virtualScroll](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#virtualscroll))属性，使能懒加载。
    
    1. // 迁移前 - LazyForEach
    2. LazyForEach(data, (item) => {...}, (item) => item)
    
    3. // 迁移后 - Repeat
    4. Repeat(data)
    5.   .virtualScroll() // 使能懒加载
    

**迁移后代码**

通过以上步骤，可以将示例1从LazyForEach迁移至Repeat，迁移后的完整示例如下所示。

**示例1 - 迁移后**

1. @Entry
2. @ComponentV2 // 使用状态管理V2
3. struct MyComponent {
4.   @Local data: Array<string> = []; // 数据源为状态管理V2装饰的数组

5.   aboutToAppear() {
6.     for (let i = 0; i <= 20; i++) {
7.       this.data.push(`Hello ${i}`);
8.     }
9.   }

10.   build() {
11.     List({ space: 3 }) {
12.       Repeat(this.data) // 使用Repeat
13.         .each((repeatItem: RepeatItem<string>) => { // 组件生成函数
14.           ListItem() {
15.             Row() {
16.               Text(repeatItem.item).fontSize(50)
17.                 .onAppear(() => {
18.                   console.info(`appear: ${repeatItem.item}`);
19.                 })
20.             }.margin({ left: 10, right: 10 })
21.           }
22.         })
23.         .key((item: string) => item) // 键值生成函数
24.         .virtualScroll() // 使能懒加载
25.     }.cachedCount(5)
26.   }
27. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.62687963044335291653345093467222:50001231000000:2800:E646A9E8F759C173C6DA35673112979325C60EE00AD6B6D6653A61C483F5895B.gif)

### 数据更新操作

**LazyForEach示例**

当LazyForEach的数据源发生变化时，开发者需要根据数据源的变化情况调用[DataChangeListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#datachangelistener)对应的接口，通知LazyForEach做相应的更新。主要的数据操作包括：添加数据、删除数据、交换数据、修改单个数据、修改多个数据、精准批量修改数据。

示例2演示了主要的数据操作。

**示例2 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   // 添加数据
11.   public pushData(data: string): void {
12.     this.dataArray.push(data);
13.     this.notifyDataAdd(this.dataArray.length - 1);
14.   }

15.   // 删除数据
16.   public deleteData(index: number): void {
17.     this.dataArray.splice(index, 1);
18.     this.notifyDataDelete(index);
19.   }

20.   // 交换数据
21.   public moveData(from: number, to: number): void {
22.     let temp: string = this.dataArray[from];
23.     this.dataArray[from] = this.dataArray[to];
24.     this.dataArray[to] = temp;
25.     this.notifyDataMove(from, to);
26.   }

27.   // 修改单个数据
28.   public changeData(index: number, data: string): void {
29.     this.dataArray.splice(index, 1, data);
30.     this.notifyDataChange(index);
31.   }

32.   // 修改多个数据
33.   public modifyAllData(): void {
34.     this.dataArray = this.dataArray.map((item: string) => {
35.         return 'Changed ' + item;
36.     });
37.     this.notifyDataReload();
38.   }
39. }

40. @Entry
41. @Component
42. struct MyComponent {
43.   private data: MyDataSource = new MyDataSource();
44.   private count: number = 0;

45.   aboutToAppear() {
46.     for (let i = 0; i <= 10; i++) {
47.       this.data.pushData(`Hello ${i}`);
48.     }
49.   }

50.   build() {
51.     Column({ space: 3 }) {
52.       // 点击追加子组件
53.       Button('Add new item')
54.         .onClick(() => {
55.           this.data.pushData(`New item ${this.count++}`);
56.         })
57.       // 点击删除子组件
58.       Button('Delete item 0')
59.         .onClick(() => {
60.           this.data.deleteData(0);
61.         })
62.       // 点击交换子组件
63.       Button('Swap item 0 and item 1')
64.         .onClick(() => {
65.           this.data.moveData(0, 1);
66.         })
67.       // 点击修改单个子组件
68.       Button('Change item 0')
69.         .onClick(() => {
70.           this.data.changeData(0, `Changed item ${this.count++}`);
71.         })
72.       // 点击修改多个子组件
73.       Button('Change all items')
74.         .onClick(() => {
75.           this.data.modifyAllData();
76.         })
77.       List({ space: 3 }) {
78.         LazyForEach(this.data, (item: string) => {
79.           ListItem() {
80.             Row() {
81.               Text(item).fontSize(25)
82.             }
83.           }
84.         }, (item: string) => item)
85.       }.cachedCount(5)
86.     }
87.   }
88. }

以上是一个典型的更新数据后LazyForEach重新渲染子组件的场景，下面将介绍如何将此示例迁移至Repeat。

**迁移步骤**

1. 迁移准备。
    
    根据数据首次渲染小节中的步骤，将LazyForEach替换为Repeat。
    
    1. 使用状态管理V2装饰器。
    2. 迁移数据源。
    3. 迁移组件生成函数与键值生成函数。
    4. 使能懒加载。
2. 迁移数据源修改方式。
    
    - 对于LazyForEach，在修改数据源后需要调用对应的接口通知其更新。
    - 对于Repeat，由状态管理V2监听其数据源变化，并触发更新。因此，开发者直接修改数据源即可，无需其他额外操作。
    
    1. // 以修改单个数据为例
    2. // 迁移前 - LazyForEach
    3. class MyDataSource implements IDataSource {
    4.   private dataArray: string[] = [];
    
    5.   public changeData(index: number, newData: string): void {
    6.     this.dataArray.splice(index, 1, data);
    7.     this.notifyDataChange(index);
    8.   }
    
    9.   // ...其他方法
    10. }
    
    11. // 迁移后 - Repeat
    12. this.data.splice(index, 1, data);
    
    其他数据更新操作，如添加数据、删除数据、交换数据等，与以上方法类似，可通过直接修改数据源数组实现。
    

**迁移后代码**

迁移后的完整示例如下。

**示例2 - 迁移后**

1. @Entry
2. @ComponentV2
3. struct MyComponent {
4.   @Local data: Array<string> = [];
5.   private count: number = 0;

6.   aboutToAppear() {
7.     for (let i = 0; i <= 10; i++) {
8.       this.data.push(`Hello ${i}`);
9.     }
10.   }

11.   build() {
12.     Column({ space: 3 }) {
13.       // 点击追加子组件
14.       Button('Add new item')
15.         .onClick(() => { this.data.push(`New item ${this.count++}`); })
16.       // 点击删除子组件
17.       Button('Delete item 0')
18.         .onClick(() => { this.data.splice(0, 1); })
19.       // 点击交换子组件
20.       Button('Swap item 0 and item 1')
21.         .onClick(() => { let temp: string = this.data[0];
22.                          this.data[0] = this.data[1];
23.                          this.data[1] = temp; })
24.       // 点击修改单个子组件
25.       Button('Change item 0')
26.         .onClick(() => { this.data.splice(0, 1, `Changed item ${this.count++}`); })
27.       // 点击修改多个子组件
28.       Button('Change all items')
29.         .onClick(() => { this.data = this.data.map((item: string) => { return 'Changed ' + item; }); })
30.       List({ space: 3 }) {
31.         Repeat(this.data)
32.           .each((repeatItem: RepeatItem<string>) => {
33.             ListItem() {
34.               Row() {
35.                 Text(repeatItem.item).fontSize(25)
36.               }
37.             }
38.           })
39.           .key((item: string) => item)
40.           .virtualScroll()
41.       }.cachedCount(5)
42.     }
43.   }
44. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.11265996241335720350651991932968:50001231000000:2800:F4FD69EEBCCC06E46710835E4A45D5C513032A0460CCAE3FB242E4CBA0728C6A.gif)

## 典型场景迁移

### 修改数据子属性

**LazyForEach示例**

LazyForEach可以使用[@Observed与@ObjectLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-observed-and-objectlink)装饰器实现对数据子属性的观测。当有数据子属性发生变化时，仅更新使用了该子属性的组件，从而提高性能。

示例3演示了对子属性的观测。

**示例3 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Observed
16. class StringData {
17.   message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @Component
24. struct MyComponent {
25.   private data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           ChildComponent({ data: item })
36.         }
37.         .onClick(() => {
38.           item.message += '0';
39.         })
40.       }, (item: StringData, index: number) => index.toString())
41.     }.cachedCount(5)
42.   }
43. }

44. @Component
45. struct ChildComponent {
46.   @ObjectLink data: StringData;

47.   build() {
48.     Row() {
49.       Text(this.data.message).fontSize(50)
50.         .onAppear(() => {
51.           console.info(`appear: ${this.data.message}`);
52.         })
53.     }.margin({ left: 10, right: 10 })
54.   }
55. }

**迁移Repeat**

Repeat需要和状态管理V2一起使用，状态管理V2提供了[@ObserveV2和@Trace](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-observedv2-and-trace)装饰器对子属性进行深度观测。迁移时，需要将@Observe和@ObjectLink装饰器迁移至@ObserveV2和@Trace装饰器。

迁移后的示例如下所示。

**示例3 - 迁移后**

1. @ObservedV2
2. class StringData {
3.   @Trace message: string; // 观测子属性

4.   constructor(message: string) {
5.     this.message = message;
6.   }
7. }

8. @Entry
9. @ComponentV2
10. struct MyComponent {
11.   @Local data: StringData[] = [];

12.   aboutToAppear() {
13.     for (let i = 0; i <= 20; i++) {
14.       this.data.push(new StringData(`Hello ${i}`));
15.     }
16.   }

17.   build() {
18.     List({ space: 3 }) {
19.       Repeat(this.data)
20.         .each((repeatItem) => {
21.           ListItem() {
22.             Text(repeatItem.item.message).fontSize(50)
23.               .onAppear(() => {
24.                 console.info(`appear: ${repeatItem.item.message}`);
25.               })
26.           }
27.           .onClick(() => {
28.             repeatItem.item.message += '0';
29.           })
30.         })
31.         .key((item: StringData, index: number) => index.toString())
32.         .virtualScroll()
33.     }.cachedCount(5)
34.   }
35. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.32541381118823681067088850163641:50001231000000:2800:6DC836D57AD8076BADB0DA63972483D68B833E42BD062B584B80D32363B0530D.gif)

### 状态管理V2观测组件内部状态

**LazyForEach示例**

状态管理V2的[@Local](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-local)装饰器提供了观测自定义组件内部变量的能力。被@Local装饰的变量发生变化时，会通知LazyForEach更新对应的组件。

示例4演示了在LazyForEach中使用@Local装饰器观测数据变化，触发组件更新。

**示例4 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @ObservedV2
16. class StringData {
17.   @Trace message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @ComponentV2
24. struct MyComponent {
25.   data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           Row() {
36.             Text(item.message).fontSize(50)
37.               .onClick(() => {
38.                 // 修改@ObservedV2装饰类中@Trace装饰的变量，触发刷新此处Text组件
39.                 item.message += '!';
40.               })
41.             ChildComponent()
42.           }
43.         }
44.       }, (item: StringData, index: number) => index.toString())
45.     }.cachedCount(5)
46.   }
47. }

48. @ComponentV2
49. struct ChildComponent {
50.   @Local message: string = '?';

51.   build() {
52.     Row() {
53.       Text(this.message).fontSize(50)
54.         .onClick(() => {
55.           // 修改@Local装饰的变量，触发刷新此处Text组件
56.           this.message += '?';
57.         })
58.     }
59.   }
60. }

**迁移Repeat**

Repeat本身支持与状态管理V2联合使用，将LazyForEach相关代码修改为Repeat后，即可实现对组件内部状态变量的观测。

迁移后的示例如下所示。

**示例4 - 迁移后**

1. @ObservedV2
2. class StringData {
3.   @Trace message: string;

4.   constructor(message: string) {
5.     this.message = message;
6.   }
7. }

8. @Entry
9. @ComponentV2
10. struct MyComponent {
11.   @Local data: StringData[] = [];

12.   aboutToAppear() {
13.     for (let i = 0; i <= 20; i++) {
14.       this.data.push(new StringData(`Hello ${i}`));
15.     }
16.   }

17.   build() {
18.     List({ space: 3 }) {
19.       Repeat(this.data)
20.         .each((repeatItem) => {
21.           ListItem() {
22.             Row() {
23.               Text(repeatItem.item.message).fontSize(50)
24.                 .onClick(() => {
25.                   // 修改@ObservedV2装饰类中@Trace装饰的变量，触发刷新此处Text组件
26.                   repeatItem.item.message += '!';
27.                 })
28.               ChildComponent()
29.             }
30.           }
31.         })
32.         .key((item: StringData, index: number) => index.toString())
33.         .virtualScroll()
34.     }.cachedCount(5)
35.   }
36. }

37. @ComponentV2
38. struct ChildComponent {
39.   @Local message: string = '?';

40.   build() {
41.     Row() {
42.       Text(this.message).fontSize(50)
43.         .onClick(() => {
44.           // 修改@Local装饰的变量，触发刷新此处Text组件
45.           this.message += '?';
46.         })
47.     }
48.   }
49. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.07940817595587609092357466015835:50001231000000:2800:55F4286074152FE31295E59C0F225F1BD4F9819FEADF363E992B70AC51CA12C5.gif)

### 状态管理V2观测组件外部输入

**LazyForEach示例**

状态管理V2的[@Param](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-param)装饰器提供了观测自定义组件外部输入变量的能力，可以实现父子组件间的数据同步。将父组件的变量传递给子组件，并用@Param装饰，当父组件变量发生变化时，会通知对应的组件更新。

示例5演示了在LazyForEach中使用@Param装饰器观测数据变化，触发组件更新。

**示例5 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @ObservedV2
16. class StringData {
17.   @Trace message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @ComponentV2
24. struct MyComponent {
25.   data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           ChildComponent({ data: item.message }) // 向自定义组件内传入变量
36.             .onClick(() => {
37.               item.message += '!';
38.             })
39.         }
40.       }, (item: StringData, index: number) => index.toString())
41.     }.cachedCount(5)
42.   }
43. }

44. @ComponentV2
45. struct ChildComponent {
46.   @Param @Require data: string = ''; // 接收来自外部的变量

47.   build() {
48.     Row() {
49.       Text(this.data).fontSize(50)
50.     }
51.   }
52. }

**迁移Repeat**

Repeat本身支持与状态管理V2联合使用，将LazyForEach相关代码修改为Repeat后，即可实现对组件外部输入状态变量的观测。

迁移后的示例如下所示。

**示例5 - 迁移后**

1. @ObservedV2
2. class StringData {
3.   @Trace message: string;

4.   constructor(message: string) {
5.     this.message = message;
6.   }
7. }

8. @Entry
9. @ComponentV2
10. struct MyComponent {
11.   @Local data: StringData[] = [];

12.   aboutToAppear() {
13.     for (let i = 0; i <= 20; i++) {
14.       this.data.push(new StringData(`Hello ${i}`));
15.     }
16.   }

17.   build() {
18.     List({ space: 3 }) {
19.       Repeat(this.data)
20.         .each((repeatItem) => {
21.           ListItem() {
22.             ChildComponent({ data: repeatItem.item.message }) // 向自定义组件内传入变量
23.               .onClick(() => {
24.                 repeatItem.item.message += '!';
25.               })
26.           }
27.         })
28.         .key((item: StringData, index: number) => index.toString())
29.         .virtualScroll()
30.     }.cachedCount(5)
31.   }
32. }

33. @ComponentV2
34. struct ChildComponent {
35.   @Param @Require data: string = ''; // 接收来自外部的变量

36.   build() {
37.     Row() {
38.       Text(this.data).fontSize(50)
39.     }
40.   }
41. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.90430579311480355869393459661229:50001231000000:2800:D4D2486C4784B911F9EE9A49363DC9C8BDDA17CD0B1BC1A8E5741ECB7881C668.gif)

### 拖拽排序

**LazyForEach示例**

LazyForEach的[onMove](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-drag-sorting#onmove)属性提供了拖拽排序能力。

示例6为典型用例。

**示例6 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public moveDataWithoutNotify(from: number, to: number): void {
11.     let tmp = this.dataArray.splice(from, 1);
12.     this.dataArray.splice(to, 0, tmp[0]);
13.   }

14.   public pushData(data: string): void {
15.     this.dataArray.push(data);
16.     this.notifyDataAdd(this.dataArray.length - 1);
17.   }
18. }

19. @Entry
20. @Component
21. struct Parent {
22.   private data: MyDataSource = new MyDataSource();

23.   aboutToAppear(): void {
24.     for (let i = 0; i < 100; i++) {
25.       this.data.pushData(i.toString());
26.     }
27.   }

28.   build() {
29.     Row() {
30.       List() {
31.         LazyForEach(this.data, (item: string) => {
32.           ListItem() {
33.             Text(item.toString())
34.               .fontSize(16)
35.               .textAlign(TextAlign.Center)
36.               .size({ height: 100, width: '100%' })
37.           }.margin(10)
38.           .borderRadius(10)
39.           .backgroundColor('#FFFFFFFF')
40.         }, (item: string) => item)
41.           .onMove((from: number, to: number) => { // 实现拖拽排序
42.             this.data.moveDataWithoutNotify(from, to);
43.           })
44.       }
45.       .width('100%')
46.       .height('100%')
47.       .backgroundColor('#FFDCDCDC')
48.     }
49.   }
50. }

**迁移Repeat**

Repeat具有与LazyForEach相同的onMove属性。将LazyForEach相关代码修改为Repeat后，即可实现拖拽排序。

迁移后的示例如下所示。

**示例6 - 迁移后**

1. @Entry
2. @ComponentV2
3. struct Parent {
4.   @Local data: string[] = [];

5.   aboutToAppear(): void {
6.     for (let i = 0; i < 100; i++) {
7.       this.data.push(i.toString());
8.     }
9.   }

10.   moveData(from: number, to: number) {
11.     let tmp = this.data.splice(from, 1);
12.     this.data.splice(to, 0, tmp[0]);
13.   }

14.   build() {
15.     Row() {
16.       List() {
17.         Repeat(this.data)
18.           .each((repeatItem) => {
19.             ListItem() {
20.               Text(repeatItem.item.toString())
21.                 .fontSize(16)
22.                 .textAlign(TextAlign.Center)
23.                 .size({ height: 100, width: '100%' })
24.             }.margin(10)
25.             .borderRadius(10)
26.             .backgroundColor('#FFFFFFFF')
27.           })
28.           .key((item: string) => item)
29.           .virtualScroll()
30.           .onMove((from: number, to: number) => { // 实现拖拽排序
31.             this.moveData(from, to);
32.           })
33.       }
34.       .width('100%')
35.       .height('100%')
36.       .backgroundColor('#FFDCDCDC')
37.     }
38.   }
39. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.50484491938529264108091518082071:50001231000000:2800:7CAE3B2495540FB53C8B4D3E84D871A4940E6E483AA646ACA1E03F8F75D22A5D.gif)

### 组件复用

**LazyForEach示例**

LazyForEach自身并不具备组件复用能力，为实现组件复用，需要与[@Reusable](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-reusable)装饰器配合使用（被@Reusable装饰的自定义组件具有复用能力）。

示例7演示了组件复用的典型场景。

**示例7 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. class StringData {
16.   message: string;

17.   constructor(message: string) {
18.     this.message = message;
19.   }
20. }

21. @Entry
22. @Component
23. struct MyComponent {
24.   data: MyDataSource = new MyDataSource();

25.   aboutToAppear() {
26.     for (let i = 0; i <= 30; i++) {
27.       this.data.pushData(new StringData(`Hello${i}`));
28.     }
29.   }

30.   build() {
31.     List({ space: 3 }) {
32.       LazyForEach(this.data, (item: StringData, index: number) => {
33.         ListItem() {
34.           ChildComponent({ data: item })
35.             .onAppear(() => {
36.               console.info(`onAppear: ${item.message}`);
37.             })
38.         }
39.       }, (item: StringData, index: number) => index.toString())
40.     }.cachedCount(5)
41.   }
42. }

43. @Reusable
44. @Component
45. struct ChildComponent {
46.   @State data: StringData = new StringData('');

47.   aboutToAppear(): void {
48.     console.info(`aboutToAppear: ${this.data.message}`);
49.   }

50.   aboutToRecycle(): void {
51.     console.info(`aboutToRecycle: ${this.data.message}`);
52.   }

53.   // 对复用的组件进行数据更新
54.   aboutToReuse(params: Record<string, ESObject>): void {
55.     this.data = params.data as StringData;
56.     console.info(`aboutToReuse: ${this.data.message}`);
57.   }

58.   build() {
59.     Row() {
60.       Text(this.data.message).fontSize(50)
61.     }
62.   }
63. }

**迁移Repeat**

Repeat本身具备组件复用能力，同时也支持与状态管理V2的[@ReusableV2](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-reusablev2)装饰器联合使用。因此，迁移至Repeat后，其组件复用具有两种实现方案。

1. 直接使用Repeat自身的复用能力。
2. 使用@ReusableV2装饰器提供的复用能力。

需要注意的是，Repeat默认使能自身的复用能力，且优先级高于@ReusableV2装饰器。若要使用@ReusableV2装饰器，需要先手动关闭Repeat自身的复用能力（@ReusableV2装饰器从API version 18开始支持，Repeat从API version 19开始支持关闭自身复用能力）。

**示例7 - 迁移方案1：使用Repeat自身的复用能力**

Repeat本身具备复用能力，且默认开启。将LazyForEach相关代码迁移至Repeat后，便已经具备了复用能力。

修改后的示例如下。

1. class StringData {
2.   message: string;

3.   constructor(message: string) {
4.     this.message = message;
5.   }
6. }

7. @Entry
8. @ComponentV2
9. struct MyComponent {
10.   @Local data: StringData[] = [];

11.   aboutToAppear() {
12.     for (let i = 0; i <= 30; i++) {
13.       this.data.push(new StringData(`Hello${i}`));
14.     }
15.   }

16.   build() {
17.     List({ space: 3 }) {
18.       Repeat(this.data) // Repeat自身具备复用功能
19.         .each((repeatItem) => {
20.           ListItem() {
21.             Text(repeatItem.item.message).fontSize(50)
22.           }
23.         })
24.         .key((item: StringData, index: number) => index.toString())
25.         .virtualScroll()
26.     }.cachedCount(5)
27.   }
28. }

**示例7 - 迁移方案2：使用@ReusableV2装饰器**

若要使用@ReusableV2装饰器，首先需要通过.virtualScroll({ reusable: false })关闭Repeat自身的复用功能，再用@ReusableV2装饰需要复用的自定义组件。

相较于Repeat自身的复用，@ReusableV2装饰的自定义组件在回收和复用时，会触发aboutToRecycle和aboutToReuse两个生命周期。

使用@ReusableV2装饰器的迁移示例如下所示。

1. class StringData {
2.   message: string;

3.   constructor(message: string) {
4.     this.message = message;
5.   }
6. }

7. @Entry
8. @ComponentV2
9. struct MyComponent {
10.   @Local data: StringData[] = [];

11.   aboutToAppear() {
12.     for (let i = 0; i <= 30; i++) {
13.       this.data.push(new StringData(`Hello${i}`));
14.     }
15.   }

16.   build() {
17.     List({ space: 3 }) {
18.       Repeat(this.data)
19.         .each((repeatItem) => {
20.           ListItem() {
21.             ChildComponent({ data: repeatItem.item })
22.               .onAppear(() => {
23.                 console.info(`onAppear: ${repeatItem.item.message}`);
24.               })
25.           }
26.         })
27.         .key((item: StringData, index: number) => index.toString())
28.         .virtualScroll({ reusable: false }) // 关闭Repeat自身的复用功能（API 19）
29.     }.cachedCount(5)
30.   }
31. }

32. // 使用@ReusableV2实现组件复用（API 18）
33. @ReusableV2
34. @ComponentV2
35. struct ChildComponent {
36.   @Param data: StringData = new StringData('');

37.   aboutToAppear(): void {
38.     console.info(`aboutToAppear: ${this.data.message}`);
39.   }

40.   aboutToRecycle(): void {
41.     console.info(`aboutToRecycle: ${this.data.message}`);
42.   }

43.   aboutToReuse(): void {
44.     console.info(`aboutToReuse: ${this.data.message}`);
45.   }

46.   build() {
47.     Row() {
48.       Text(this.data.message).fontSize(50)
49.     }
50.   }
51. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.24263212202420592585590536450661:50001231000000:2800:16BFB5890C31649EC35FF4CE09025AA08349FC37026607631E2C028628AD3731.gif)

### 模板渲染

**LazyForEach示例**

LazyForEach自身并不具备模板渲染能力。为实现模板渲染能力，需要开发者自己实现逻辑判断，为不同的数据项选择不同的渲染模板。

示例8演示了模板渲染的典型场景。

**示例8 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. class StringData {
16.   message: string;
17.   type: number;

18.   constructor(message: string, type: number) {
19.     this.message = message;
20.     this.type = type;
21.   }

22.   getType(): number {
23.     if (this.type >= 1) {
24.       return 1;
25.     } else {
26.       return 0;
27.     }
28.   }
29. }

30. @Entry
31. @Component
32. struct MyComponent {
33.   data: MyDataSource = new MyDataSource();

34.   aboutToAppear() {
35.     for (let i = 0; i <= 200; i++) {
36.       this.data.pushData(new StringData(`Hello${i}`, i % 2));
37.     }
38.   }

39.   build() {
40.     List({ space: 3 }) {
41.       LazyForEach(this.data, (item: StringData, index: number) => {
42.         ListItem() {
43.           // 开发者自己实现逻辑判断，为不同的数据项选择不同的渲染模板
44.           if (item.getType() == 0) {
45.             // 模板A
46.             ChildComponentA({ data: item })
47.               .onAppear(() => {
48.                 console.info(`type A onAppear: ${item.message}`);
49.               })
50.           } else {
51.             // 模板B
52.             ChildComponentB({ data: item })
53.               .onAppear(() => {
54.                 console.info(`type B onAppear: ${item.message}`);
55.               })
56.           }
57.         }
58.       }, (item: StringData, index: number) => index.toString())
59.     }.cachedCount(5)
60.   }
61. }

62. // 使用@Reusable实现组件复用
63. @Reusable
64. @Component
65. struct ChildComponentA {
66.   @State data: StringData = new StringData('', 0);

67.   aboutToAppear(): void {
68.     console.info(`type A aboutToAppear: ${this.data.message}`);
69.   }

70.   aboutToRecycle(): void {
71.     console.info(`type A aboutToRecycle: ${this.data.message}`);
72.   }

73.   aboutToReuse(params: Record<string, ESObject>): void {
74.     this.data = params.data as StringData;
75.     console.info(`type A aboutToReuse: ${this.data.message}`);
76.   }

77.   build() {
78.     Row() {
79.       Text(this.data.message).fontSize(50)
80.       Button('Type A')
81.     }
82.   }
83. }

84. @Reusable
85. @Component
86. struct ChildComponentB {
87.   @State data: StringData = new StringData('', 0);

88.   aboutToAppear(): void {
89.     console.info(`type B aboutToAppear: ${this.data.message}`);
90.   }

91.   aboutToRecycle(): void {
92.     console.info(`type B aboutToRecycle: ${this.data.message}`);
93.   }

94.   aboutToReuse(params: Record<string, ESObject>): void {
95.     this.data = params.data as StringData;
96.     console.info(`type B aboutToReuse: ${this.data.message}`);
97.   }

98.   build() {
99.     Row() {
100.       Text(this.data.message).fontSize(50).fontColor(Color.Gray)
101.       Text('Type B')
102.     }
103.   }
104. }

**迁移Repeat**

Repeat本身具备模板渲染能力，开发者可以通过[templateId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#templateid)方法为不同的数据项选择不同的模板，再通过[template](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#template)方法为不同的模板配置不同的组件生成函数。同时，开发者仍然可以选择自己实现逻辑判断，为不同的数据项分配不同的模板。

需要注意的是，如果开发者选择自己实现模板渲染，则需要关闭Repeat自身的复用功能。否则，Repeat在复用子组件时无法选择正确的模板，会导致渲染异常。

**示例8 - 迁移方案1：使用Repeat自身的模板渲染能力**

1. class StringData {
2.   message: string;
3.   type: number;

4.   constructor(message: string, type: number) {
5.     this.message = message;
6.     this.type = type;
7.   }

8.   getType(): number {
9.     if (this.type >= 1) {
10.       return 1;
11.     } else {
12.       return 0;
13.     }
14.   }
15. }

16. @Entry
17. @ComponentV2
18. struct MyComponent {
19.   data: StringData[] = [];

20.   aboutToAppear() {
21.     for (let i = 0; i <= 200; i++) {
22.       this.data.push(new StringData(`Hello${i}`, i % 2));
23.     }
24.   }

25.   build() {
26.     List({ space: 3 }) {
27.       Repeat(this.data)
28.         .each((repeatItem) => {
29.           ListItem() {
30.             Text('Default item')
31.           }
32.         })
33.         .template('A', (repeatItem) => { // 模板A
34.           ListItem() {
35.             Row() {
36.               Text(repeatItem.item.message).fontSize(50)
37.               Button('Type A')
38.             }
39.           }
40.         })
41.         .template('B', (repeatItem) => { // 模板B
42.           ListItem() {
43.             Row() {
44.               Text(repeatItem.item.message).fontSize(50).fontColor(Color.Gray)
45.               Text('Type B')
46.             }
47.           }
48.         })
49.         .templateId((item: StringData) => { // 为不同的数据项选择不同的模板
50.           if (item.getType() == 0) {
51.             return 'A';
52.           } else {
53.             return 'B';
54.           }
55.         })
56.         .key((item: StringData, index: number) => index.toString())
57.         .virtualScroll()
58.     }.cachedCount(5)
59.   }
60. }

**示例8 - 迁移方案2：由开发者实现模板渲染能力**

1. class StringData {
2.   message: string;
3.   type: number;

4.   constructor(message: string, type: number) {
5.     this.message = message;
6.     this.type = type;
7.   }

8.   getType(): number {
9.     if (this.type >= 1) {
10.       return 1;
11.     } else {
12.       return 0;
13.     }
14.   }
15. }

16. @Entry
17. @ComponentV2
18. struct MyComponent {
19.   data: StringData[] = [];

20.   aboutToAppear() {
21.     for (let i = 0; i <= 200; i++) {
22.       this.data.push(new StringData(`Hello${i}`, i % 2));
23.     }
24.   }

25.   build() {
26.     List({ space: 3 }) {
27.       Repeat(this.data)
28.         .each((repeatItem) => {
29.           ListItem() {
30.             // 开发者自己实现逻辑判断，为不同的数据项选择不同的渲染模板
31.             if (repeatItem.item.getType() == 0) {
32.               ChildComponentA({ data: repeatItem.item }) // 模板A
33.                 .onAppear(() => {
34.                   console.info(`type A onAppear: ${repeatItem.item.message}`);
35.                 })
36.             } else {
37.               ChildComponentB({ data: repeatItem.item }) // 模板B
38.                 .onAppear(() => {
39.                   console.info(`type B onAppear: ${repeatItem.item.message}`);
40.                 })
41.             }
42.           }
43.         })
44.         .key((item: StringData, index: number) => index.toString())
45.         .virtualScroll({ reusable: false }) // 关闭Repeat自身的复用功能（API 19），避免渲染异常
46.     }.cachedCount(5)
47.   }
48. }

49. // 使用@ReusableV2实现组件复用（API 18）
50. @ReusableV2
51. @ComponentV2
52. struct ChildComponentA {
53.   @Param data: StringData = new StringData('', 0);

54.   aboutToAppear(): void {
55.     console.info(`type A aboutToAppear: ${this.data.message}`);
56.   }

57.   aboutToRecycle(): void {
58.     console.info(`type A aboutToRecycle: ${this.data.message}`);
59.   }

60.   aboutToReuse(): void {
61.     console.info(`type A aboutToReuse: ${this.data.message}`);
62.   }

63.   build() {
64.     Row() {
65.       Text(this.data.message).fontSize(50)
66.       Button('Type A')
67.     }
68.   }
69. }

70. @ReusableV2
71. @ComponentV2
72. struct ChildComponentB {
73.   @Param data: StringData = new StringData('', 0);

74.   aboutToAppear(): void {
75.     console.info(`type B aboutToAppear: ${this.data.message}`);
76.   }

77.   aboutToRecycle(): void {
78.     console.info(`type B aboutToRecycle: ${this.data.message}`);
79.   }

80.   aboutToReuse(): void {
81.     console.info(`type B aboutToReuse: ${this.data.message}`);
82.   }

83.   build() {
84.     Row() {
85.       Text(this.data.message).fontSize(50).fontColor(Color.Gray)
86.       Text('Type B')
87.     }
88.   }
89. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.16951959361312922505157389391226:50001231000000:2800:13C72E252FDC6CE53545D7A59467B7BD1037B80FD52FCFA7AE75684E3288912F.gif)

## BasicDataSource示例代码

### string类型数组的BasicDataSource代码

1. // BasicDataSource实现了IDataSource接口，用于管理listener监听，以及通知LazyForEach数据更新
2. class BasicDataSource implements IDataSource {
3.   private listeners: DataChangeListener[] = [];
4.   private originDataArray: string[] = [];

5.   public totalCount(): number {
6.     return this.originDataArray.length;
7.   }

8.   public getData(index: number): string {
9.     return this.originDataArray[index];
10.   }

11.   // 该方法为框架侧调用，为LazyForEach组件向其数据源处添加listener监听
12.   registerDataChangeListener(listener: DataChangeListener): void {
13.     if (this.listeners.indexOf(listener) < 0) {
14.       console.info('add listener');
15.       this.listeners.push(listener);
16.     }
17.   }

18.   // 该方法为框架侧调用，为对应的LazyForEach组件在数据源处去除listener监听
19.   unregisterDataChangeListener(listener: DataChangeListener): void {
20.     const pos = this.listeners.indexOf(listener);
21.     if (pos >= 0) {
22.       console.info('remove listener');
23.       this.listeners.splice(pos, 1);
24.     }
25.   }

26.   // 通知LazyForEach组件需要重载所有子组件
27.   notifyDataReload(): void {
28.     this.listeners.forEach(listener => {
29.       listener.onDataReloaded();
30.     });
31.   }

32.   // 通知LazyForEach组件需要在index对应索引处添加子组件
33.   notifyDataAdd(index: number): void {
34.     this.listeners.forEach(listener => {
35.       listener.onDataAdd(index);
36.       // 写法2：listener.onDatasetChange([{type: DataOperationType.ADD, index: index}]);
37.     });
38.   }

39.   // 通知LazyForEach组件在index对应索引处数据有变化，需要重建该子组件
40.   notifyDataChange(index: number): void {
41.     this.listeners.forEach(listener => {
42.       listener.onDataChange(index);
43.       // 写法2：listener.onDatasetChange([{type: DataOperationType.CHANGE, index: index}]);
44.     });
45.   }

46.   // 通知LazyForEach组件需要在index对应索引处删除该子组件
47.   notifyDataDelete(index: number): void {
48.     this.listeners.forEach(listener => {
49.       listener.onDataDelete(index);
50.       // 写法2：listener.onDatasetChange([{type: DataOperationType.DELETE, index: index}]);
51.     });
52.   }

53.   // 通知LazyForEach组件将from索引和to索引处的子组件进行交换
54.   notifyDataMove(from: number, to: number): void {
55.     this.listeners.forEach(listener => {
56.       listener.onDataMove(from, to);
57.       // 写法2：listener.onDatasetChange(
58.       //         [{type: DataOperationType.EXCHANGE, index: {start: from, end: to}}]);
59.     });
60.   }

61.   notifyDatasetChange(operations: DataOperation[]): void {
62.     this.listeners.forEach(listener => {
63.       listener.onDatasetChange(operations);
64.     });
65.   }
66. }

### StringData类型数组的BasicDataSource代码

1. class BasicDataSource implements IDataSource {
2.   private listeners: DataChangeListener[] = [];
3.   private originDataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.originDataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.originDataArray[index];
9.   }

10.   registerDataChangeListener(listener: DataChangeListener): void {
11.     if (this.listeners.indexOf(listener) < 0) {
12.       console.info('add listener');
13.       this.listeners.push(listener);
14.     }
15.   }

16.   unregisterDataChangeListener(listener: DataChangeListener): void {
17.     const pos = this.listeners.indexOf(listener);
18.     if (pos >= 0) {
19.       console.info('remove listener');
20.       this.listeners.splice(pos, 1);
21.     }
22.   }

23.   notifyDataReload(): void {
24.     this.listeners.forEach(listener => {
25.       listener.onDataReloaded();
26.     });
27.   }

28.   notifyDataAdd(index: number): void {
29.     this.listeners.forEach(listener => {
30.       listener.onDataAdd(index);
31.     });
32.   }

33.   notifyDataChange(index: number): void {
34.     this.listeners.forEach(listener => {
35.       listener.onDataChange(index);
36.     });
37.   }

38.   notifyDataDelete(index: number): void {
39.     this.listeners.forEach(listener => {
40.       listener.onDataDelete(index);
41.     });
42.   }

43.   notifyDataMove(from: number, to: number): void {
44.     this.listeners.forEach(listener => {
45.       listener.onDataMove(from, to);
46.     });
47.   }

48.   notifyDatasetChange(operations: DataOperation[]): void {
49.     this.listeners.forEach(listener => {
50.       listener.onDatasetChange(operations);
51.     });
52.   }
53. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat "Repeat：可复用的循环渲染")
# LazyForEach迁移Repeat指南

更新时间: 2025-12-16 16:39

[Repeat](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat)是ArkUI在API version 12中新引入的循环渲染组件，相比[LazyForEach](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach)具有更简洁的API、更丰富的功能以及更强的性能优化能力。本指南帮助开发者将LazyForEach平滑地迁移到Repeat。

## 基础用法迁移

### 数据首次渲染

**LazyForEach示例**

LazyForEach根据数据源循环渲染子组件。

示例1中，在容器组件[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-layout-development-create-list)中使用LazyForEach，并基于数据源循环渲染出了一系列[Text](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-text-display)子组件。

**示例1 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Entry
16. @Component
17. struct MyComponent {
18.   private data: MyDataSource = new MyDataSource();

19.   aboutToAppear() {
20.     for (let i = 0; i <= 20; i++) {
21.       this.data.pushData(`Hello ${i}`);
22.     }
23.   }

24.   build() {
25.     List({ space: 3 }) {
26.       LazyForEach(this.data, (item: string) => {
27.         ListItem() {
28.           Row() {
29.             Text(item).fontSize(50)
30.               .onAppear(() => {
31.                 console.info(`appear: ${item}`);
32.               })
33.           }.margin({ left: 10, right: 10 })
34.         }
35.       }, (item: string) => item)
36.     }.cachedCount(5)
37.   }
38. }

以上是一个典型的使用LazyForEach循环渲染子组件的场景，下面将介绍如何将此示例迁移至Repeat。

**迁移步骤**

1. 使用状态管理V2装饰器。
    
    Repeat推荐和状态管理V2装饰器配合使用（[懒加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat#%E5%BE%AA%E7%8E%AF%E6%B8%B2%E6%9F%93%E8%83%BD%E5%8A%9B%E8%AF%B4%E6%98%8E)模式下只支持和状态管理V2装饰器配合使用）。如果之前使用的是状态管理V1装饰器，需要修改为状态管理V2装饰器。
    
    1. // 迁移前 - LazyForEach
    2. @Component // 状态管理V1
    3. struct MyComponent {
    4.   build() {
    5.     // ...
    6.     LazyForEach(...)
    7.     // ...
    8.   }
    9.   // ...其他属性、方法
    10. }
    
    11. // 迁移后 - Repeat
    12. @ComponentV2 // 状态管理V2
    13. struct MyComponent {
    14.   build() {
    15.     // ...
    16.     Repeat(...)
    17.     // ...
    18.   }
    19.   // ...其他属性、方法
    20. }
    
2. 迁移数据源。
    
    LazyForEach使用专用的数据结构[IDataSource](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#idatasource)作为数据源。迁移至Repeat后，不再使用IDataSource作为数据源，而是使用状态管理V2装饰的数组作为数据源。
    
    1. // 迁移前 - LazyForEach
    2. class MyDataSource implements IDataSource {
    3.   private dataArray: string[] = [];
    
    4.   public totalCount(): number {
    5.     return this.dataArray.length;
    6.   }
    
    7.   public getData(index: number): string {
    8.     return this.dataArray[index];
    9.   }
    
    10.   // ...其他方法
    11. }
    
    12. // 迁移后 - Repeat
    13. @Local data: Array<string> = [];
    
3. 迁移组件生成函数和键值生成函数。
    
    LazyForEach与Repeat均通过组件生成函数，为每一项数据创建一个子组件；通过键值生成函数，为每一项数据生成一个唯一的键值。
    
    从LazyForEach迁移至Repeat时，两者的语法存在差异。Repeat需要在[.each()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#each)或[.template()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#template)中设置组件生成函数，在[.key()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#key)中设置键值生成函数。
    
    1. // 迁移前 - LazyForEach
    2. List() {
    3.   LazyForEach(
    4.     this.data, // 数据源
    5.     (item: string, index: number) => { // 组件生成函数
    6.       ListItem() {
    7.         Text(item)
    8.       }
    9.     },
    10.     (item: string, index: number) => item // 键值生成函数
    11.   )
    12. }
    
    13. // 迁移后 - Repeat
    14. List() {
    15.   Repeat<string>(this.data) // 数据源
    16.     .each((repeatItem: RepeatItem<string>) => { // 组件生成函数
    17.       ListItem() {
    18.         Text(repeatItem.item)
    19.       }
    20.     })
    21.     .key((item: string, index: number) => item) // 键值生成函数
    22. }
    
4. 配置懒加载功能。
    
    Repeat具有[懒加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat#%E5%BE%AA%E7%8E%AF%E6%B8%B2%E6%9F%93%E8%83%BD%E5%8A%9B%E8%AF%B4%E6%98%8E)和[全量加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat#%E5%85%B3%E9%97%AD%E6%87%92%E5%8A%A0%E8%BD%BD)两种模式。
    
    - 全量加载模式渲染所有子节点（对标[ForEach](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-foreach)）。
    - 懒加载模式动态渲染屏幕区域和预加载区域内的子节点（需要与容器组件配合使用，对标LazyForEach）。
    
    从LazyForEach迁移至Repeat时，需要调用[virtualScroll](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#virtualscroll))属性，使能懒加载。
    
    1. // 迁移前 - LazyForEach
    2. LazyForEach(data, (item) => {...}, (item) => item)
    
    3. // 迁移后 - Repeat
    4. Repeat(data)
    5.   .virtualScroll() // 使能懒加载
    

**迁移后代码**

通过以上步骤，可以将示例1从LazyForEach迁移至Repeat，迁移后的完整示例如下所示。

**示例1 - 迁移后**

1. @Entry
2. @ComponentV2 // 使用状态管理V2
3. struct MyComponent {
4.   @Local data: Array<string> = []; // 数据源为状态管理V2装饰的数组

5.   aboutToAppear() {
6.     for (let i = 0; i <= 20; i++) {
7.       this.data.push(`Hello ${i}`);
8.     }
9.   }

10.   build() {
11.     List({ space: 3 }) {
12.       Repeat(this.data) // 使用Repeat
13.         .each((repeatItem: RepeatItem<string>) => { // 组件生成函数
14.           ListItem() {
15.             Row() {
16.               Text(repeatItem.item).fontSize(50)
17.                 .onAppear(() => {
18.                   console.info(`appear: ${repeatItem.item}`);
19.                 })
20.             }.margin({ left: 10, right: 10 })
21.           }
22.         })
23.         .key((item: string) => item) // 键值生成函数
24.         .virtualScroll() // 使能懒加载
25.     }.cachedCount(5)
26.   }
27. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.62687963044335291653345093467222:50001231000000:2800:E646A9E8F759C173C6DA35673112979325C60EE00AD6B6D6653A61C483F5895B.gif)

### 数据更新操作

**LazyForEach示例**

当LazyForEach的数据源发生变化时，开发者需要根据数据源的变化情况调用[DataChangeListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#datachangelistener)对应的接口，通知LazyForEach做相应的更新。主要的数据操作包括：添加数据、删除数据、交换数据、修改单个数据、修改多个数据、精准批量修改数据。

示例2演示了主要的数据操作。

**示例2 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   // 添加数据
11.   public pushData(data: string): void {
12.     this.dataArray.push(data);
13.     this.notifyDataAdd(this.dataArray.length - 1);
14.   }

15.   // 删除数据
16.   public deleteData(index: number): void {
17.     this.dataArray.splice(index, 1);
18.     this.notifyDataDelete(index);
19.   }

20.   // 交换数据
21.   public moveData(from: number, to: number): void {
22.     let temp: string = this.dataArray[from];
23.     this.dataArray[from] = this.dataArray[to];
24.     this.dataArray[to] = temp;
25.     this.notifyDataMove(from, to);
26.   }

27.   // 修改单个数据
28.   public changeData(index: number, data: string): void {
29.     this.dataArray.splice(index, 1, data);
30.     this.notifyDataChange(index);
31.   }

32.   // 修改多个数据
33.   public modifyAllData(): void {
34.     this.dataArray = this.dataArray.map((item: string) => {
35.         return 'Changed ' + item;
36.     });
37.     this.notifyDataReload();
38.   }
39. }

40. @Entry
41. @Component
42. struct MyComponent {
43.   private data: MyDataSource = new MyDataSource();
44.   private count: number = 0;

45.   aboutToAppear() {
46.     for (let i = 0; i <= 10; i++) {
47.       this.data.pushData(`Hello ${i}`);
48.     }
49.   }

50.   build() {
51.     Column({ space: 3 }) {
52.       // 点击追加子组件
53.       Button('Add new item')
54.         .onClick(() => {
55.           this.data.pushData(`New item ${this.count++}`);
56.         })
57.       // 点击删除子组件
58.       Button('Delete item 0')
59.         .onClick(() => {
60.           this.data.deleteData(0);
61.         })
62.       // 点击交换子组件
63.       Button('Swap item 0 and item 1')
64.         .onClick(() => {
65.           this.data.moveData(0, 1);
66.         })
67.       // 点击修改单个子组件
68.       Button('Change item 0')
69.         .onClick(() => {
70.           this.data.changeData(0, `Changed item ${this.count++}`);
71.         })
72.       // 点击修改多个子组件
73.       Button('Change all items')
74.         .onClick(() => {
75.           this.data.modifyAllData();
76.         })
77.       List({ space: 3 }) {
78.         LazyForEach(this.data, (item: string) => {
79.           ListItem() {
80.             Row() {
81.               Text(item).fontSize(25)
82.             }
83.           }
84.         }, (item: string) => item)
85.       }.cachedCount(5)
86.     }
87.   }
88. }

以上是一个典型的更新数据后LazyForEach重新渲染子组件的场景，下面将介绍如何将此示例迁移至Repeat。

**迁移步骤**

1. 迁移准备。
    
    根据数据首次渲染小节中的步骤，将LazyForEach替换为Repeat。
    
    1. 使用状态管理V2装饰器。
    2. 迁移数据源。
    3. 迁移组件生成函数与键值生成函数。
    4. 使能懒加载。
2. 迁移数据源修改方式。
    
    - 对于LazyForEach，在修改数据源后需要调用对应的接口通知其更新。
    - 对于Repeat，由状态管理V2监听其数据源变化，并触发更新。因此，开发者直接修改数据源即可，无需其他额外操作。
    
    1. // 以修改单个数据为例
    2. // 迁移前 - LazyForEach
    3. class MyDataSource implements IDataSource {
    4.   private dataArray: string[] = [];
    
    5.   public changeData(index: number, newData: string): void {
    6.     this.dataArray.splice(index, 1, data);
    7.     this.notifyDataChange(index);
    8.   }
    
    9.   // ...其他方法
    10. }
    
    11. // 迁移后 - Repeat
    12. this.data.splice(index, 1, data);
    
    其他数据更新操作，如添加数据、删除数据、交换数据等，与以上方法类似，可通过直接修改数据源数组实现。
    

**迁移后代码**

迁移后的完整示例如下。

**示例2 - 迁移后**

1. @Entry
2. @ComponentV2
3. struct MyComponent {
4.   @Local data: Array<string> = [];
5.   private count: number = 0;

6.   aboutToAppear() {
7.     for (let i = 0; i <= 10; i++) {
8.       this.data.push(`Hello ${i}`);
9.     }
10.   }

11.   build() {
12.     Column({ space: 3 }) {
13.       // 点击追加子组件
14.       Button('Add new item')
15.         .onClick(() => { this.data.push(`New item ${this.count++}`); })
16.       // 点击删除子组件
17.       Button('Delete item 0')
18.         .onClick(() => { this.data.splice(0, 1); })
19.       // 点击交换子组件
20.       Button('Swap item 0 and item 1')
21.         .onClick(() => { let temp: string = this.data[0];
22.                          this.data[0] = this.data[1];
23.                          this.data[1] = temp; })
24.       // 点击修改单个子组件
25.       Button('Change item 0')
26.         .onClick(() => { this.data.splice(0, 1, `Changed item ${this.count++}`); })
27.       // 点击修改多个子组件
28.       Button('Change all items')
29.         .onClick(() => { this.data = this.data.map((item: string) => { return 'Changed ' + item; }); })
30.       List({ space: 3 }) {
31.         Repeat(this.data)
32.           .each((repeatItem: RepeatItem<string>) => {
33.             ListItem() {
34.               Row() {
35.                 Text(repeatItem.item).fontSize(25)
36.               }
37.             }
38.           })
39.           .key((item: string) => item)
40.           .virtualScroll()
41.       }.cachedCount(5)
42.     }
43.   }
44. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.11265996241335720350651991932968:50001231000000:2800:F4FD69EEBCCC06E46710835E4A45D5C513032A0460CCAE3FB242E4CBA0728C6A.gif)

## 典型场景迁移

### 修改数据子属性

**LazyForEach示例**

LazyForEach可以使用[@Observed与@ObjectLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-observed-and-objectlink)装饰器实现对数据子属性的观测。当有数据子属性发生变化时，仅更新使用了该子属性的组件，从而提高性能。

示例3演示了对子属性的观测。

**示例3 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Observed
16. class StringData {
17.   message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @Component
24. struct MyComponent {
25.   private data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           ChildComponent({ data: item })
36.         }
37.         .onClick(() => {
38.           item.message += '0';
39.         })
40.       }, (item: StringData, index: number) => index.toString())
41.     }.cachedCount(5)
42.   }
43. }

44. @Component
45. struct ChildComponent {
46.   @ObjectLink data: StringData;

47.   build() {
48.     Row() {
49.       Text(this.data.message).fontSize(50)
50.         .onAppear(() => {
51.           console.info(`appear: ${this.data.message}`);
52.         })
53.     }.margin({ left: 10, right: 10 })
54.   }
55. }

**迁移Repeat**

Repeat需要和状态管理V2一起使用，状态管理V2提供了[@ObserveV2和@Trace](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-observedv2-and-trace)装饰器对子属性进行深度观测。迁移时，需要将@Observe和@ObjectLink装饰器迁移至@ObserveV2和@Trace装饰器。

迁移后的示例如下所示。

**示例3 - 迁移后**

1. @ObservedV2
2. class StringData {
3.   @Trace message: string; // 观测子属性

4.   constructor(message: string) {
5.     this.message = message;
6.   }
7. }

8. @Entry
9. @ComponentV2
10. struct MyComponent {
11.   @Local data: StringData[] = [];

12.   aboutToAppear() {
13.     for (let i = 0; i <= 20; i++) {
14.       this.data.push(new StringData(`Hello ${i}`));
15.     }
16.   }

17.   build() {
18.     List({ space: 3 }) {
19.       Repeat(this.data)
20.         .each((repeatItem) => {
21.           ListItem() {
22.             Text(repeatItem.item.message).fontSize(50)
23.               .onAppear(() => {
24.                 console.info(`appear: ${repeatItem.item.message}`);
25.               })
26.           }
27.           .onClick(() => {
28.             repeatItem.item.message += '0';
29.           })
30.         })
31.         .key((item: StringData, index: number) => index.toString())
32.         .virtualScroll()
33.     }.cachedCount(5)
34.   }
35. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.32541381118823681067088850163641:50001231000000:2800:6DC836D57AD8076BADB0DA63972483D68B833E42BD062B584B80D32363B0530D.gif)

### 状态管理V2观测组件内部状态

**LazyForEach示例**

状态管理V2的[@Local](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-local)装饰器提供了观测自定义组件内部变量的能力。被@Local装饰的变量发生变化时，会通知LazyForEach更新对应的组件。

示例4演示了在LazyForEach中使用@Local装饰器观测数据变化，触发组件更新。

**示例4 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @ObservedV2
16. class StringData {
17.   @Trace message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @ComponentV2
24. struct MyComponent {
25.   data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           Row() {
36.             Text(item.message).fontSize(50)
37.               .onClick(() => {
38.                 // 修改@ObservedV2装饰类中@Trace装饰的变量，触发刷新此处Text组件
39.                 item.message += '!';
40.               })
41.             ChildComponent()
42.           }
43.         }
44.       }, (item: StringData, index: number) => index.toString())
45.     }.cachedCount(5)
46.   }
47. }

48. @ComponentV2
49. struct ChildComponent {
50.   @Local message: string = '?';

51.   build() {
52.     Row() {
53.       Text(this.message).fontSize(50)
54.         .onClick(() => {
55.           // 修改@Local装饰的变量，触发刷新此处Text组件
56.           this.message += '?';
57.         })
58.     }
59.   }
60. }

**迁移Repeat**

Repeat本身支持与状态管理V2联合使用，将LazyForEach相关代码修改为Repeat后，即可实现对组件内部状态变量的观测。

迁移后的示例如下所示。

**示例4 - 迁移后**

1. @ObservedV2
2. class StringData {
3.   @Trace message: string;

4.   constructor(message: string) {
5.     this.message = message;
6.   }
7. }

8. @Entry
9. @ComponentV2
10. struct MyComponent {
11.   @Local data: StringData[] = [];

12.   aboutToAppear() {
13.     for (let i = 0; i <= 20; i++) {
14.       this.data.push(new StringData(`Hello ${i}`));
15.     }
16.   }

17.   build() {
18.     List({ space: 3 }) {
19.       Repeat(this.data)
20.         .each((repeatItem) => {
21.           ListItem() {
22.             Row() {
23.               Text(repeatItem.item.message).fontSize(50)
24.                 .onClick(() => {
25.                   // 修改@ObservedV2装饰类中@Trace装饰的变量，触发刷新此处Text组件
26.                   repeatItem.item.message += '!';
27.                 })
28.               ChildComponent()
29.             }
30.           }
31.         })
32.         .key((item: StringData, index: number) => index.toString())
33.         .virtualScroll()
34.     }.cachedCount(5)
35.   }
36. }

37. @ComponentV2
38. struct ChildComponent {
39.   @Local message: string = '?';

40.   build() {
41.     Row() {
42.       Text(this.message).fontSize(50)
43.         .onClick(() => {
44.           // 修改@Local装饰的变量，触发刷新此处Text组件
45.           this.message += '?';
46.         })
47.     }
48.   }
49. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.07940817595587609092357466015835:50001231000000:2800:55F4286074152FE31295E59C0F225F1BD4F9819FEADF363E992B70AC51CA12C5.gif)

### 状态管理V2观测组件外部输入

**LazyForEach示例**

状态管理V2的[@Param](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-param)装饰器提供了观测自定义组件外部输入变量的能力，可以实现父子组件间的数据同步。将父组件的变量传递给子组件，并用@Param装饰，当父组件变量发生变化时，会通知对应的组件更新。

示例5演示了在LazyForEach中使用@Param装饰器观测数据变化，触发组件更新。

**示例5 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @ObservedV2
16. class StringData {
17.   @Trace message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @ComponentV2
24. struct MyComponent {
25.   data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           ChildComponent({ data: item.message }) // 向自定义组件内传入变量
36.             .onClick(() => {
37.               item.message += '!';
38.             })
39.         }
40.       }, (item: StringData, index: number) => index.toString())
41.     }.cachedCount(5)
42.   }
43. }

44. @ComponentV2
45. struct ChildComponent {
46.   @Param @Require data: string = ''; // 接收来自外部的变量

47.   build() {
48.     Row() {
49.       Text(this.data).fontSize(50)
50.     }
51.   }
52. }

**迁移Repeat**

Repeat本身支持与状态管理V2联合使用，将LazyForEach相关代码修改为Repeat后，即可实现对组件外部输入状态变量的观测。

迁移后的示例如下所示。

**示例5 - 迁移后**

1. @ObservedV2
2. class StringData {
3.   @Trace message: string;

4.   constructor(message: string) {
5.     this.message = message;
6.   }
7. }

8. @Entry
9. @ComponentV2
10. struct MyComponent {
11.   @Local data: StringData[] = [];

12.   aboutToAppear() {
13.     for (let i = 0; i <= 20; i++) {
14.       this.data.push(new StringData(`Hello ${i}`));
15.     }
16.   }

17.   build() {
18.     List({ space: 3 }) {
19.       Repeat(this.data)
20.         .each((repeatItem) => {
21.           ListItem() {
22.             ChildComponent({ data: repeatItem.item.message }) // 向自定义组件内传入变量
23.               .onClick(() => {
24.                 repeatItem.item.message += '!';
25.               })
26.           }
27.         })
28.         .key((item: StringData, index: number) => index.toString())
29.         .virtualScroll()
30.     }.cachedCount(5)
31.   }
32. }

33. @ComponentV2
34. struct ChildComponent {
35.   @Param @Require data: string = ''; // 接收来自外部的变量

36.   build() {
37.     Row() {
38.       Text(this.data).fontSize(50)
39.     }
40.   }
41. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.90430579311480355869393459661229:50001231000000:2800:D4D2486C4784B911F9EE9A49363DC9C8BDDA17CD0B1BC1A8E5741ECB7881C668.gif)

### 拖拽排序

**LazyForEach示例**

LazyForEach的[onMove](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-drag-sorting#onmove)属性提供了拖拽排序能力。

示例6为典型用例。

**示例6 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public moveDataWithoutNotify(from: number, to: number): void {
11.     let tmp = this.dataArray.splice(from, 1);
12.     this.dataArray.splice(to, 0, tmp[0]);
13.   }

14.   public pushData(data: string): void {
15.     this.dataArray.push(data);
16.     this.notifyDataAdd(this.dataArray.length - 1);
17.   }
18. }

19. @Entry
20. @Component
21. struct Parent {
22.   private data: MyDataSource = new MyDataSource();

23.   aboutToAppear(): void {
24.     for (let i = 0; i < 100; i++) {
25.       this.data.pushData(i.toString());
26.     }
27.   }

28.   build() {
29.     Row() {
30.       List() {
31.         LazyForEach(this.data, (item: string) => {
32.           ListItem() {
33.             Text(item.toString())
34.               .fontSize(16)
35.               .textAlign(TextAlign.Center)
36.               .size({ height: 100, width: '100%' })
37.           }.margin(10)
38.           .borderRadius(10)
39.           .backgroundColor('#FFFFFFFF')
40.         }, (item: string) => item)
41.           .onMove((from: number, to: number) => { // 实现拖拽排序
42.             this.data.moveDataWithoutNotify(from, to);
43.           })
44.       }
45.       .width('100%')
46.       .height('100%')
47.       .backgroundColor('#FFDCDCDC')
48.     }
49.   }
50. }

**迁移Repeat**

Repeat具有与LazyForEach相同的onMove属性。将LazyForEach相关代码修改为Repeat后，即可实现拖拽排序。

迁移后的示例如下所示。

**示例6 - 迁移后**

1. @Entry
2. @ComponentV2
3. struct Parent {
4.   @Local data: string[] = [];

5.   aboutToAppear(): void {
6.     for (let i = 0; i < 100; i++) {
7.       this.data.push(i.toString());
8.     }
9.   }

10.   moveData(from: number, to: number) {
11.     let tmp = this.data.splice(from, 1);
12.     this.data.splice(to, 0, tmp[0]);
13.   }

14.   build() {
15.     Row() {
16.       List() {
17.         Repeat(this.data)
18.           .each((repeatItem) => {
19.             ListItem() {
20.               Text(repeatItem.item.toString())
21.                 .fontSize(16)
22.                 .textAlign(TextAlign.Center)
23.                 .size({ height: 100, width: '100%' })
24.             }.margin(10)
25.             .borderRadius(10)
26.             .backgroundColor('#FFFFFFFF')
27.           })
28.           .key((item: string) => item)
29.           .virtualScroll()
30.           .onMove((from: number, to: number) => { // 实现拖拽排序
31.             this.moveData(from, to);
32.           })
33.       }
34.       .width('100%')
35.       .height('100%')
36.       .backgroundColor('#FFDCDCDC')
37.     }
38.   }
39. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.50484491938529264108091518082071:50001231000000:2800:7CAE3B2495540FB53C8B4D3E84D871A4940E6E483AA646ACA1E03F8F75D22A5D.gif)

### 组件复用

**LazyForEach示例**

LazyForEach自身并不具备组件复用能力，为实现组件复用，需要与[@Reusable](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-reusable)装饰器配合使用（被@Reusable装饰的自定义组件具有复用能力）。

示例7演示了组件复用的典型场景。

**示例7 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. class StringData {
16.   message: string;

17.   constructor(message: string) {
18.     this.message = message;
19.   }
20. }

21. @Entry
22. @Component
23. struct MyComponent {
24.   data: MyDataSource = new MyDataSource();

25.   aboutToAppear() {
26.     for (let i = 0; i <= 30; i++) {
27.       this.data.pushData(new StringData(`Hello${i}`));
28.     }
29.   }

30.   build() {
31.     List({ space: 3 }) {
32.       LazyForEach(this.data, (item: StringData, index: number) => {
33.         ListItem() {
34.           ChildComponent({ data: item })
35.             .onAppear(() => {
36.               console.info(`onAppear: ${item.message}`);
37.             })
38.         }
39.       }, (item: StringData, index: number) => index.toString())
40.     }.cachedCount(5)
41.   }
42. }

43. @Reusable
44. @Component
45. struct ChildComponent {
46.   @State data: StringData = new StringData('');

47.   aboutToAppear(): void {
48.     console.info(`aboutToAppear: ${this.data.message}`);
49.   }

50.   aboutToRecycle(): void {
51.     console.info(`aboutToRecycle: ${this.data.message}`);
52.   }

53.   // 对复用的组件进行数据更新
54.   aboutToReuse(params: Record<string, ESObject>): void {
55.     this.data = params.data as StringData;
56.     console.info(`aboutToReuse: ${this.data.message}`);
57.   }

58.   build() {
59.     Row() {
60.       Text(this.data.message).fontSize(50)
61.     }
62.   }
63. }

**迁移Repeat**

Repeat本身具备组件复用能力，同时也支持与状态管理V2的[@ReusableV2](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-reusablev2)装饰器联合使用。因此，迁移至Repeat后，其组件复用具有两种实现方案。

1. 直接使用Repeat自身的复用能力。
2. 使用@ReusableV2装饰器提供的复用能力。

需要注意的是，Repeat默认使能自身的复用能力，且优先级高于@ReusableV2装饰器。若要使用@ReusableV2装饰器，需要先手动关闭Repeat自身的复用能力（@ReusableV2装饰器从API version 18开始支持，Repeat从API version 19开始支持关闭自身复用能力）。

**示例7 - 迁移方案1：使用Repeat自身的复用能力**

Repeat本身具备复用能力，且默认开启。将LazyForEach相关代码迁移至Repeat后，便已经具备了复用能力。

修改后的示例如下。

1. class StringData {
2.   message: string;

3.   constructor(message: string) {
4.     this.message = message;
5.   }
6. }

7. @Entry
8. @ComponentV2
9. struct MyComponent {
10.   @Local data: StringData[] = [];

11.   aboutToAppear() {
12.     for (let i = 0; i <= 30; i++) {
13.       this.data.push(new StringData(`Hello${i}`));
14.     }
15.   }

16.   build() {
17.     List({ space: 3 }) {
18.       Repeat(this.data) // Repeat自身具备复用功能
19.         .each((repeatItem) => {
20.           ListItem() {
21.             Text(repeatItem.item.message).fontSize(50)
22.           }
23.         })
24.         .key((item: StringData, index: number) => index.toString())
25.         .virtualScroll()
26.     }.cachedCount(5)
27.   }
28. }

**示例7 - 迁移方案2：使用@ReusableV2装饰器**

若要使用@ReusableV2装饰器，首先需要通过.virtualScroll({ reusable: false })关闭Repeat自身的复用功能，再用@ReusableV2装饰需要复用的自定义组件。

相较于Repeat自身的复用，@ReusableV2装饰的自定义组件在回收和复用时，会触发aboutToRecycle和aboutToReuse两个生命周期。

使用@ReusableV2装饰器的迁移示例如下所示。

1. class StringData {
2.   message: string;

3.   constructor(message: string) {
4.     this.message = message;
5.   }
6. }

7. @Entry
8. @ComponentV2
9. struct MyComponent {
10.   @Local data: StringData[] = [];

11.   aboutToAppear() {
12.     for (let i = 0; i <= 30; i++) {
13.       this.data.push(new StringData(`Hello${i}`));
14.     }
15.   }

16.   build() {
17.     List({ space: 3 }) {
18.       Repeat(this.data)
19.         .each((repeatItem) => {
20.           ListItem() {
21.             ChildComponent({ data: repeatItem.item })
22.               .onAppear(() => {
23.                 console.info(`onAppear: ${repeatItem.item.message}`);
24.               })
25.           }
26.         })
27.         .key((item: StringData, index: number) => index.toString())
28.         .virtualScroll({ reusable: false }) // 关闭Repeat自身的复用功能（API 19）
29.     }.cachedCount(5)
30.   }
31. }

32. // 使用@ReusableV2实现组件复用（API 18）
33. @ReusableV2
34. @ComponentV2
35. struct ChildComponent {
36.   @Param data: StringData = new StringData('');

37.   aboutToAppear(): void {
38.     console.info(`aboutToAppear: ${this.data.message}`);
39.   }

40.   aboutToRecycle(): void {
41.     console.info(`aboutToRecycle: ${this.data.message}`);
42.   }

43.   aboutToReuse(): void {
44.     console.info(`aboutToReuse: ${this.data.message}`);
45.   }

46.   build() {
47.     Row() {
48.       Text(this.data.message).fontSize(50)
49.     }
50.   }
51. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.24263212202420592585590536450661:50001231000000:2800:16BFB5890C31649EC35FF4CE09025AA08349FC37026607631E2C028628AD3731.gif)

### 模板渲染

**LazyForEach示例**

LazyForEach自身并不具备模板渲染能力。为实现模板渲染能力，需要开发者自己实现逻辑判断，为不同的数据项选择不同的渲染模板。

示例8演示了模板渲染的典型场景。

**示例8 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. class StringData {
16.   message: string;
17.   type: number;

18.   constructor(message: string, type: number) {
19.     this.message = message;
20.     this.type = type;
21.   }

22.   getType(): number {
23.     if (this.type >= 1) {
24.       return 1;
25.     } else {
26.       return 0;
27.     }
28.   }
29. }

30. @Entry
31. @Component
32. struct MyComponent {
33.   data: MyDataSource = new MyDataSource();

34.   aboutToAppear() {
35.     for (let i = 0; i <= 200; i++) {
36.       this.data.pushData(new StringData(`Hello${i}`, i % 2));
37.     }
38.   }

39.   build() {
40.     List({ space: 3 }) {
41.       LazyForEach(this.data, (item: StringData, index: number) => {
42.         ListItem() {
43.           // 开发者自己实现逻辑判断，为不同的数据项选择不同的渲染模板
44.           if (item.getType() == 0) {
45.             // 模板A
46.             ChildComponentA({ data: item })
47.               .onAppear(() => {
48.                 console.info(`type A onAppear: ${item.message}`);
49.               })
50.           } else {
51.             // 模板B
52.             ChildComponentB({ data: item })
53.               .onAppear(() => {
54.                 console.info(`type B onAppear: ${item.message}`);
55.               })
56.           }
57.         }
58.       }, (item: StringData, index: number) => index.toString())
59.     }.cachedCount(5)
60.   }
61. }

62. // 使用@Reusable实现组件复用
63. @Reusable
64. @Component
65. struct ChildComponentA {
66.   @State data: StringData = new StringData('', 0);

67.   aboutToAppear(): void {
68.     console.info(`type A aboutToAppear: ${this.data.message}`);
69.   }

70.   aboutToRecycle(): void {
71.     console.info(`type A aboutToRecycle: ${this.data.message}`);
72.   }

73.   aboutToReuse(params: Record<string, ESObject>): void {
74.     this.data = params.data as StringData;
75.     console.info(`type A aboutToReuse: ${this.data.message}`);
76.   }

77.   build() {
78.     Row() {
79.       Text(this.data.message).fontSize(50)
80.       Button('Type A')
81.     }
82.   }
83. }

84. @Reusable
85. @Component
86. struct ChildComponentB {
87.   @State data: StringData = new StringData('', 0);

88.   aboutToAppear(): void {
89.     console.info(`type B aboutToAppear: ${this.data.message}`);
90.   }

91.   aboutToRecycle(): void {
92.     console.info(`type B aboutToRecycle: ${this.data.message}`);
93.   }

94.   aboutToReuse(params: Record<string, ESObject>): void {
95.     this.data = params.data as StringData;
96.     console.info(`type B aboutToReuse: ${this.data.message}`);
97.   }

98.   build() {
99.     Row() {
100.       Text(this.data.message).fontSize(50).fontColor(Color.Gray)
101.       Text('Type B')
102.     }
103.   }
104. }

**迁移Repeat**

Repeat本身具备模板渲染能力，开发者可以通过[templateId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#templateid)方法为不同的数据项选择不同的模板，再通过[template](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#template)方法为不同的模板配置不同的组件生成函数。同时，开发者仍然可以选择自己实现逻辑判断，为不同的数据项分配不同的模板。

需要注意的是，如果开发者选择自己实现模板渲染，则需要关闭Repeat自身的复用功能。否则，Repeat在复用子组件时无法选择正确的模板，会导致渲染异常。

**示例8 - 迁移方案1：使用Repeat自身的模板渲染能力**

1. class StringData {
2.   message: string;
3.   type: number;

4.   constructor(message: string, type: number) {
5.     this.message = message;
6.     this.type = type;
7.   }

8.   getType(): number {
9.     if (this.type >= 1) {
10.       return 1;
11.     } else {
12.       return 0;
13.     }
14.   }
15. }

16. @Entry
17. @ComponentV2
18. struct MyComponent {
19.   data: StringData[] = [];

20.   aboutToAppear() {
21.     for (let i = 0; i <= 200; i++) {
22.       this.data.push(new StringData(`Hello${i}`, i % 2));
23.     }
24.   }

25.   build() {
26.     List({ space: 3 }) {
27.       Repeat(this.data)
28.         .each((repeatItem) => {
29.           ListItem() {
30.             Text('Default item')
31.           }
32.         })
33.         .template('A', (repeatItem) => { // 模板A
34.           ListItem() {
35.             Row() {
36.               Text(repeatItem.item.message).fontSize(50)
37.               Button('Type A')
38.             }
39.           }
40.         })
41.         .template('B', (repeatItem) => { // 模板B
42.           ListItem() {
43.             Row() {
44.               Text(repeatItem.item.message).fontSize(50).fontColor(Color.Gray)
45.               Text('Type B')
46.             }
47.           }
48.         })
49.         .templateId((item: StringData) => { // 为不同的数据项选择不同的模板
50.           if (item.getType() == 0) {
51.             return 'A';
52.           } else {
53.             return 'B';
54.           }
55.         })
56.         .key((item: StringData, index: number) => index.toString())
57.         .virtualScroll()
58.     }.cachedCount(5)
59.   }
60. }

**示例8 - 迁移方案2：由开发者实现模板渲染能力**

1. class StringData {
2.   message: string;
3.   type: number;

4.   constructor(message: string, type: number) {
5.     this.message = message;
6.     this.type = type;
7.   }

8.   getType(): number {
9.     if (this.type >= 1) {
10.       return 1;
11.     } else {
12.       return 0;
13.     }
14.   }
15. }

16. @Entry
17. @ComponentV2
18. struct MyComponent {
19.   data: StringData[] = [];

20.   aboutToAppear() {
21.     for (let i = 0; i <= 200; i++) {
22.       this.data.push(new StringData(`Hello${i}`, i % 2));
23.     }
24.   }

25.   build() {
26.     List({ space: 3 }) {
27.       Repeat(this.data)
28.         .each((repeatItem) => {
29.           ListItem() {
30.             // 开发者自己实现逻辑判断，为不同的数据项选择不同的渲染模板
31.             if (repeatItem.item.getType() == 0) {
32.               ChildComponentA({ data: repeatItem.item }) // 模板A
33.                 .onAppear(() => {
34.                   console.info(`type A onAppear: ${repeatItem.item.message}`);
35.                 })
36.             } else {
37.               ChildComponentB({ data: repeatItem.item }) // 模板B
38.                 .onAppear(() => {
39.                   console.info(`type B onAppear: ${repeatItem.item.message}`);
40.                 })
41.             }
42.           }
43.         })
44.         .key((item: StringData, index: number) => index.toString())
45.         .virtualScroll({ reusable: false }) // 关闭Repeat自身的复用功能（API 19），避免渲染异常
46.     }.cachedCount(5)
47.   }
48. }

49. // 使用@ReusableV2实现组件复用（API 18）
50. @ReusableV2
51. @ComponentV2
52. struct ChildComponentA {
53.   @Param data: StringData = new StringData('', 0);

54.   aboutToAppear(): void {
55.     console.info(`type A aboutToAppear: ${this.data.message}`);
56.   }

57.   aboutToRecycle(): void {
58.     console.info(`type A aboutToRecycle: ${this.data.message}`);
59.   }

60.   aboutToReuse(): void {
61.     console.info(`type A aboutToReuse: ${this.data.message}`);
62.   }

63.   build() {
64.     Row() {
65.       Text(this.data.message).fontSize(50)
66.       Button('Type A')
67.     }
68.   }
69. }

70. @ReusableV2
71. @ComponentV2
72. struct ChildComponentB {
73.   @Param data: StringData = new StringData('', 0);

74.   aboutToAppear(): void {
75.     console.info(`type B aboutToAppear: ${this.data.message}`);
76.   }

77.   aboutToRecycle(): void {
78.     console.info(`type B aboutToRecycle: ${this.data.message}`);
79.   }

80.   aboutToReuse(): void {
81.     console.info(`type B aboutToReuse: ${this.data.message}`);
82.   }

83.   build() {
84.     Row() {
85.       Text(this.data.message).fontSize(50).fontColor(Color.Gray)
86.       Text('Type B')
87.     }
88.   }
89. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.16951959361312922505157389391226:50001231000000:2800:13C72E252FDC6CE53545D7A59467B7BD1037B80FD52FCFA7AE75684E3288912F.gif)

## BasicDataSource示例代码

### string类型数组的BasicDataSource代码

1. // BasicDataSource实现了IDataSource接口，用于管理listener监听，以及通知LazyForEach数据更新
2. class BasicDataSource implements IDataSource {
3.   private listeners: DataChangeListener[] = [];
4.   private originDataArray: string[] = [];

5.   public totalCount(): number {
6.     return this.originDataArray.length;
7.   }

8.   public getData(index: number): string {
9.     return this.originDataArray[index];
10.   }

11.   // 该方法为框架侧调用，为LazyForEach组件向其数据源处添加listener监听
12.   registerDataChangeListener(listener: DataChangeListener): void {
13.     if (this.listeners.indexOf(listener) < 0) {
14.       console.info('add listener');
15.       this.listeners.push(listener);
16.     }
17.   }

18.   // 该方法为框架侧调用，为对应的LazyForEach组件在数据源处去除listener监听
19.   unregisterDataChangeListener(listener: DataChangeListener): void {
20.     const pos = this.listeners.indexOf(listener);
21.     if (pos >= 0) {
22.       console.info('remove listener');
23.       this.listeners.splice(pos, 1);
24.     }
25.   }

26.   // 通知LazyForEach组件需要重载所有子组件
27.   notifyDataReload(): void {
28.     this.listeners.forEach(listener => {
29.       listener.onDataReloaded();
30.     });
31.   }

32.   // 通知LazyForEach组件需要在index对应索引处添加子组件
33.   notifyDataAdd(index: number): void {
34.     this.listeners.forEach(listener => {
35.       listener.onDataAdd(index);
36.       // 写法2：listener.onDatasetChange([{type: DataOperationType.ADD, index: index}]);
37.     });
38.   }

39.   // 通知LazyForEach组件在index对应索引处数据有变化，需要重建该子组件
40.   notifyDataChange(index: number): void {
41.     this.listeners.forEach(listener => {
42.       listener.onDataChange(index);
43.       // 写法2：listener.onDatasetChange([{type: DataOperationType.CHANGE, index: index}]);
44.     });
45.   }

46.   // 通知LazyForEach组件需要在index对应索引处删除该子组件
47.   notifyDataDelete(index: number): void {
48.     this.listeners.forEach(listener => {
49.       listener.onDataDelete(index);
50.       // 写法2：listener.onDatasetChange([{type: DataOperationType.DELETE, index: index}]);
51.     });
52.   }

53.   // 通知LazyForEach组件将from索引和to索引处的子组件进行交换
54.   notifyDataMove(from: number, to: number): void {
55.     this.listeners.forEach(listener => {
56.       listener.onDataMove(from, to);
57.       // 写法2：listener.onDatasetChange(
58.       //         [{type: DataOperationType.EXCHANGE, index: {start: from, end: to}}]);
59.     });
60.   }

61.   notifyDatasetChange(operations: DataOperation[]): void {
62.     this.listeners.forEach(listener => {
63.       listener.onDatasetChange(operations);
64.     });
65.   }
66. }

### StringData类型数组的BasicDataSource代码

1. class BasicDataSource implements IDataSource {
2.   private listeners: DataChangeListener[] = [];
3.   private originDataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.originDataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.originDataArray[index];
9.   }

10.   registerDataChangeListener(listener: DataChangeListener): void {
11.     if (this.listeners.indexOf(listener) < 0) {
12.       console.info('add listener');
13.       this.listeners.push(listener);
14.     }
15.   }

16.   unregisterDataChangeListener(listener: DataChangeListener): void {
17.     const pos = this.listeners.indexOf(listener);
18.     if (pos >= 0) {
19.       console.info('remove listener');
20.       this.listeners.splice(pos, 1);
21.     }
22.   }

23.   notifyDataReload(): void {
24.     this.listeners.forEach(listener => {
25.       listener.onDataReloaded();
26.     });
27.   }

28.   notifyDataAdd(index: number): void {
29.     this.listeners.forEach(listener => {
30.       listener.onDataAdd(index);
31.     });
32.   }

33.   notifyDataChange(index: number): void {
34.     this.listeners.forEach(listener => {
35.       listener.onDataChange(index);
36.     });
37.   }

38.   notifyDataDelete(index: number): void {
39.     this.listeners.forEach(listener => {
40.       listener.onDataDelete(index);
41.     });
42.   }

43.   notifyDataMove(from: number, to: number): void {
44.     this.listeners.forEach(listener => {
45.       listener.onDataMove(from, to);
46.     });
47.   }

48.   notifyDatasetChange(operations: DataOperation[]): void {
49.     this.listeners.forEach(listener => {
50.       listener.onDatasetChange(operations);
51.     });
52.   }
53. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat "Repeat：可复用的循环渲染")
# LazyForEach迁移Repeat指南

更新时间: 2025-12-16 16:39

[Repeat](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat)是ArkUI在API version 12中新引入的循环渲染组件，相比[LazyForEach](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-lazyforeach)具有更简洁的API、更丰富的功能以及更强的性能优化能力。本指南帮助开发者将LazyForEach平滑地迁移到Repeat。

## 基础用法迁移

### 数据首次渲染

**LazyForEach示例**

LazyForEach根据数据源循环渲染子组件。

示例1中，在容器组件[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-layout-development-create-list)中使用LazyForEach，并基于数据源循环渲染出了一系列[Text](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-text-display)子组件。

**示例1 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: string): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Entry
16. @Component
17. struct MyComponent {
18.   private data: MyDataSource = new MyDataSource();

19.   aboutToAppear() {
20.     for (let i = 0; i <= 20; i++) {
21.       this.data.pushData(`Hello ${i}`);
22.     }
23.   }

24.   build() {
25.     List({ space: 3 }) {
26.       LazyForEach(this.data, (item: string) => {
27.         ListItem() {
28.           Row() {
29.             Text(item).fontSize(50)
30.               .onAppear(() => {
31.                 console.info(`appear: ${item}`);
32.               })
33.           }.margin({ left: 10, right: 10 })
34.         }
35.       }, (item: string) => item)
36.     }.cachedCount(5)
37.   }
38. }

以上是一个典型的使用LazyForEach循环渲染子组件的场景，下面将介绍如何将此示例迁移至Repeat。

**迁移步骤**

1. 使用状态管理V2装饰器。
    
    Repeat推荐和状态管理V2装饰器配合使用（[懒加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat#%E5%BE%AA%E7%8E%AF%E6%B8%B2%E6%9F%93%E8%83%BD%E5%8A%9B%E8%AF%B4%E6%98%8E)模式下只支持和状态管理V2装饰器配合使用）。如果之前使用的是状态管理V1装饰器，需要修改为状态管理V2装饰器。
    
    1. // 迁移前 - LazyForEach
    2. @Component // 状态管理V1
    3. struct MyComponent {
    4.   build() {
    5.     // ...
    6.     LazyForEach(...)
    7.     // ...
    8.   }
    9.   // ...其他属性、方法
    10. }
    
    11. // 迁移后 - Repeat
    12. @ComponentV2 // 状态管理V2
    13. struct MyComponent {
    14.   build() {
    15.     // ...
    16.     Repeat(...)
    17.     // ...
    18.   }
    19.   // ...其他属性、方法
    20. }
    
2. 迁移数据源。
    
    LazyForEach使用专用的数据结构[IDataSource](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#idatasource)作为数据源。迁移至Repeat后，不再使用IDataSource作为数据源，而是使用状态管理V2装饰的数组作为数据源。
    
    1. // 迁移前 - LazyForEach
    2. class MyDataSource implements IDataSource {
    3.   private dataArray: string[] = [];
    
    4.   public totalCount(): number {
    5.     return this.dataArray.length;
    6.   }
    
    7.   public getData(index: number): string {
    8.     return this.dataArray[index];
    9.   }
    
    10.   // ...其他方法
    11. }
    
    12. // 迁移后 - Repeat
    13. @Local data: Array<string> = [];
    
3. 迁移组件生成函数和键值生成函数。
    
    LazyForEach与Repeat均通过组件生成函数，为每一项数据创建一个子组件；通过键值生成函数，为每一项数据生成一个唯一的键值。
    
    从LazyForEach迁移至Repeat时，两者的语法存在差异。Repeat需要在[.each()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#each)或[.template()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#template)中设置组件生成函数，在[.key()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#key)中设置键值生成函数。
    
    1. // 迁移前 - LazyForEach
    2. List() {
    3.   LazyForEach(
    4.     this.data, // 数据源
    5.     (item: string, index: number) => { // 组件生成函数
    6.       ListItem() {
    7.         Text(item)
    8.       }
    9.     },
    10.     (item: string, index: number) => item // 键值生成函数
    11.   )
    12. }
    
    13. // 迁移后 - Repeat
    14. List() {
    15.   Repeat<string>(this.data) // 数据源
    16.     .each((repeatItem: RepeatItem<string>) => { // 组件生成函数
    17.       ListItem() {
    18.         Text(repeatItem.item)
    19.       }
    20.     })
    21.     .key((item: string, index: number) => item) // 键值生成函数
    22. }
    
4. 配置懒加载功能。
    
    Repeat具有[懒加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat#%E5%BE%AA%E7%8E%AF%E6%B8%B2%E6%9F%93%E8%83%BD%E5%8A%9B%E8%AF%B4%E6%98%8E)和[全量加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat#%E5%85%B3%E9%97%AD%E6%87%92%E5%8A%A0%E8%BD%BD)两种模式。
    
    - 全量加载模式渲染所有子节点（对标[ForEach](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-rendering-control-foreach)）。
    - 懒加载模式动态渲染屏幕区域和预加载区域内的子节点（需要与容器组件配合使用，对标LazyForEach）。
    
    从LazyForEach迁移至Repeat时，需要调用[virtualScroll](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#virtualscroll))属性，使能懒加载。
    
    1. // 迁移前 - LazyForEach
    2. LazyForEach(data, (item) => {...}, (item) => item)
    
    3. // 迁移后 - Repeat
    4. Repeat(data)
    5.   .virtualScroll() // 使能懒加载
    

**迁移后代码**

通过以上步骤，可以将示例1从LazyForEach迁移至Repeat，迁移后的完整示例如下所示。

**示例1 - 迁移后**

1. @Entry
2. @ComponentV2 // 使用状态管理V2
3. struct MyComponent {
4.   @Local data: Array<string> = []; // 数据源为状态管理V2装饰的数组

5.   aboutToAppear() {
6.     for (let i = 0; i <= 20; i++) {
7.       this.data.push(`Hello ${i}`);
8.     }
9.   }

10.   build() {
11.     List({ space: 3 }) {
12.       Repeat(this.data) // 使用Repeat
13.         .each((repeatItem: RepeatItem<string>) => { // 组件生成函数
14.           ListItem() {
15.             Row() {
16.               Text(repeatItem.item).fontSize(50)
17.                 .onAppear(() => {
18.                   console.info(`appear: ${repeatItem.item}`);
19.                 })
20.             }.margin({ left: 10, right: 10 })
21.           }
22.         })
23.         .key((item: string) => item) // 键值生成函数
24.         .virtualScroll() // 使能懒加载
25.     }.cachedCount(5)
26.   }
27. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.62687963044335291653345093467222:50001231000000:2800:E646A9E8F759C173C6DA35673112979325C60EE00AD6B6D6653A61C483F5895B.gif)

### 数据更新操作

**LazyForEach示例**

当LazyForEach的数据源发生变化时，开发者需要根据数据源的变化情况调用[DataChangeListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-lazyforeach#datachangelistener)对应的接口，通知LazyForEach做相应的更新。主要的数据操作包括：添加数据、删除数据、交换数据、修改单个数据、修改多个数据、精准批量修改数据。

示例2演示了主要的数据操作。

**示例2 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   // 添加数据
11.   public pushData(data: string): void {
12.     this.dataArray.push(data);
13.     this.notifyDataAdd(this.dataArray.length - 1);
14.   }

15.   // 删除数据
16.   public deleteData(index: number): void {
17.     this.dataArray.splice(index, 1);
18.     this.notifyDataDelete(index);
19.   }

20.   // 交换数据
21.   public moveData(from: number, to: number): void {
22.     let temp: string = this.dataArray[from];
23.     this.dataArray[from] = this.dataArray[to];
24.     this.dataArray[to] = temp;
25.     this.notifyDataMove(from, to);
26.   }

27.   // 修改单个数据
28.   public changeData(index: number, data: string): void {
29.     this.dataArray.splice(index, 1, data);
30.     this.notifyDataChange(index);
31.   }

32.   // 修改多个数据
33.   public modifyAllData(): void {
34.     this.dataArray = this.dataArray.map((item: string) => {
35.         return 'Changed ' + item;
36.     });
37.     this.notifyDataReload();
38.   }
39. }

40. @Entry
41. @Component
42. struct MyComponent {
43.   private data: MyDataSource = new MyDataSource();
44.   private count: number = 0;

45.   aboutToAppear() {
46.     for (let i = 0; i <= 10; i++) {
47.       this.data.pushData(`Hello ${i}`);
48.     }
49.   }

50.   build() {
51.     Column({ space: 3 }) {
52.       // 点击追加子组件
53.       Button('Add new item')
54.         .onClick(() => {
55.           this.data.pushData(`New item ${this.count++}`);
56.         })
57.       // 点击删除子组件
58.       Button('Delete item 0')
59.         .onClick(() => {
60.           this.data.deleteData(0);
61.         })
62.       // 点击交换子组件
63.       Button('Swap item 0 and item 1')
64.         .onClick(() => {
65.           this.data.moveData(0, 1);
66.         })
67.       // 点击修改单个子组件
68.       Button('Change item 0')
69.         .onClick(() => {
70.           this.data.changeData(0, `Changed item ${this.count++}`);
71.         })
72.       // 点击修改多个子组件
73.       Button('Change all items')
74.         .onClick(() => {
75.           this.data.modifyAllData();
76.         })
77.       List({ space: 3 }) {
78.         LazyForEach(this.data, (item: string) => {
79.           ListItem() {
80.             Row() {
81.               Text(item).fontSize(25)
82.             }
83.           }
84.         }, (item: string) => item)
85.       }.cachedCount(5)
86.     }
87.   }
88. }

以上是一个典型的更新数据后LazyForEach重新渲染子组件的场景，下面将介绍如何将此示例迁移至Repeat。

**迁移步骤**

1. 迁移准备。
    
    根据数据首次渲染小节中的步骤，将LazyForEach替换为Repeat。
    
    1. 使用状态管理V2装饰器。
    2. 迁移数据源。
    3. 迁移组件生成函数与键值生成函数。
    4. 使能懒加载。
2. 迁移数据源修改方式。
    
    - 对于LazyForEach，在修改数据源后需要调用对应的接口通知其更新。
    - 对于Repeat，由状态管理V2监听其数据源变化，并触发更新。因此，开发者直接修改数据源即可，无需其他额外操作。
    
    1. // 以修改单个数据为例
    2. // 迁移前 - LazyForEach
    3. class MyDataSource implements IDataSource {
    4.   private dataArray: string[] = [];
    
    5.   public changeData(index: number, newData: string): void {
    6.     this.dataArray.splice(index, 1, data);
    7.     this.notifyDataChange(index);
    8.   }
    
    9.   // ...其他方法
    10. }
    
    11. // 迁移后 - Repeat
    12. this.data.splice(index, 1, data);
    
    其他数据更新操作，如添加数据、删除数据、交换数据等，与以上方法类似，可通过直接修改数据源数组实现。
    

**迁移后代码**

迁移后的完整示例如下。

**示例2 - 迁移后**

1. @Entry
2. @ComponentV2
3. struct MyComponent {
4.   @Local data: Array<string> = [];
5.   private count: number = 0;

6.   aboutToAppear() {
7.     for (let i = 0; i <= 10; i++) {
8.       this.data.push(`Hello ${i}`);
9.     }
10.   }

11.   build() {
12.     Column({ space: 3 }) {
13.       // 点击追加子组件
14.       Button('Add new item')
15.         .onClick(() => { this.data.push(`New item ${this.count++}`); })
16.       // 点击删除子组件
17.       Button('Delete item 0')
18.         .onClick(() => { this.data.splice(0, 1); })
19.       // 点击交换子组件
20.       Button('Swap item 0 and item 1')
21.         .onClick(() => { let temp: string = this.data[0];
22.                          this.data[0] = this.data[1];
23.                          this.data[1] = temp; })
24.       // 点击修改单个子组件
25.       Button('Change item 0')
26.         .onClick(() => { this.data.splice(0, 1, `Changed item ${this.count++}`); })
27.       // 点击修改多个子组件
28.       Button('Change all items')
29.         .onClick(() => { this.data = this.data.map((item: string) => { return 'Changed ' + item; }); })
30.       List({ space: 3 }) {
31.         Repeat(this.data)
32.           .each((repeatItem: RepeatItem<string>) => {
33.             ListItem() {
34.               Row() {
35.                 Text(repeatItem.item).fontSize(25)
36.               }
37.             }
38.           })
39.           .key((item: string) => item)
40.           .virtualScroll()
41.       }.cachedCount(5)
42.     }
43.   }
44. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.11265996241335720350651991932968:50001231000000:2800:F4FD69EEBCCC06E46710835E4A45D5C513032A0460CCAE3FB242E4CBA0728C6A.gif)

## 典型场景迁移

### 修改数据子属性

**LazyForEach示例**

LazyForEach可以使用[@Observed与@ObjectLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-observed-and-objectlink)装饰器实现对数据子属性的观测。当有数据子属性发生变化时，仅更新使用了该子属性的组件，从而提高性能。

示例3演示了对子属性的观测。

**示例3 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @Observed
16. class StringData {
17.   message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @Component
24. struct MyComponent {
25.   private data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           ChildComponent({ data: item })
36.         }
37.         .onClick(() => {
38.           item.message += '0';
39.         })
40.       }, (item: StringData, index: number) => index.toString())
41.     }.cachedCount(5)
42.   }
43. }

44. @Component
45. struct ChildComponent {
46.   @ObjectLink data: StringData;

47.   build() {
48.     Row() {
49.       Text(this.data.message).fontSize(50)
50.         .onAppear(() => {
51.           console.info(`appear: ${this.data.message}`);
52.         })
53.     }.margin({ left: 10, right: 10 })
54.   }
55. }

**迁移Repeat**

Repeat需要和状态管理V2一起使用，状态管理V2提供了[@ObserveV2和@Trace](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-observedv2-and-trace)装饰器对子属性进行深度观测。迁移时，需要将@Observe和@ObjectLink装饰器迁移至@ObserveV2和@Trace装饰器。

迁移后的示例如下所示。

**示例3 - 迁移后**

1. @ObservedV2
2. class StringData {
3.   @Trace message: string; // 观测子属性

4.   constructor(message: string) {
5.     this.message = message;
6.   }
7. }

8. @Entry
9. @ComponentV2
10. struct MyComponent {
11.   @Local data: StringData[] = [];

12.   aboutToAppear() {
13.     for (let i = 0; i <= 20; i++) {
14.       this.data.push(new StringData(`Hello ${i}`));
15.     }
16.   }

17.   build() {
18.     List({ space: 3 }) {
19.       Repeat(this.data)
20.         .each((repeatItem) => {
21.           ListItem() {
22.             Text(repeatItem.item.message).fontSize(50)
23.               .onAppear(() => {
24.                 console.info(`appear: ${repeatItem.item.message}`);
25.               })
26.           }
27.           .onClick(() => {
28.             repeatItem.item.message += '0';
29.           })
30.         })
31.         .key((item: StringData, index: number) => index.toString())
32.         .virtualScroll()
33.     }.cachedCount(5)
34.   }
35. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.32541381118823681067088850163641:50001231000000:2800:6DC836D57AD8076BADB0DA63972483D68B833E42BD062B584B80D32363B0530D.gif)

### 状态管理V2观测组件内部状态

**LazyForEach示例**

状态管理V2的[@Local](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-local)装饰器提供了观测自定义组件内部变量的能力。被@Local装饰的变量发生变化时，会通知LazyForEach更新对应的组件。

示例4演示了在LazyForEach中使用@Local装饰器观测数据变化，触发组件更新。

**示例4 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @ObservedV2
16. class StringData {
17.   @Trace message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @ComponentV2
24. struct MyComponent {
25.   data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           Row() {
36.             Text(item.message).fontSize(50)
37.               .onClick(() => {
38.                 // 修改@ObservedV2装饰类中@Trace装饰的变量，触发刷新此处Text组件
39.                 item.message += '!';
40.               })
41.             ChildComponent()
42.           }
43.         }
44.       }, (item: StringData, index: number) => index.toString())
45.     }.cachedCount(5)
46.   }
47. }

48. @ComponentV2
49. struct ChildComponent {
50.   @Local message: string = '?';

51.   build() {
52.     Row() {
53.       Text(this.message).fontSize(50)
54.         .onClick(() => {
55.           // 修改@Local装饰的变量，触发刷新此处Text组件
56.           this.message += '?';
57.         })
58.     }
59.   }
60. }

**迁移Repeat**

Repeat本身支持与状态管理V2联合使用，将LazyForEach相关代码修改为Repeat后，即可实现对组件内部状态变量的观测。

迁移后的示例如下所示。

**示例4 - 迁移后**

1. @ObservedV2
2. class StringData {
3.   @Trace message: string;

4.   constructor(message: string) {
5.     this.message = message;
6.   }
7. }

8. @Entry
9. @ComponentV2
10. struct MyComponent {
11.   @Local data: StringData[] = [];

12.   aboutToAppear() {
13.     for (let i = 0; i <= 20; i++) {
14.       this.data.push(new StringData(`Hello ${i}`));
15.     }
16.   }

17.   build() {
18.     List({ space: 3 }) {
19.       Repeat(this.data)
20.         .each((repeatItem) => {
21.           ListItem() {
22.             Row() {
23.               Text(repeatItem.item.message).fontSize(50)
24.                 .onClick(() => {
25.                   // 修改@ObservedV2装饰类中@Trace装饰的变量，触发刷新此处Text组件
26.                   repeatItem.item.message += '!';
27.                 })
28.               ChildComponent()
29.             }
30.           }
31.         })
32.         .key((item: StringData, index: number) => index.toString())
33.         .virtualScroll()
34.     }.cachedCount(5)
35.   }
36. }

37. @ComponentV2
38. struct ChildComponent {
39.   @Local message: string = '?';

40.   build() {
41.     Row() {
42.       Text(this.message).fontSize(50)
43.         .onClick(() => {
44.           // 修改@Local装饰的变量，触发刷新此处Text组件
45.           this.message += '?';
46.         })
47.     }
48.   }
49. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.07940817595587609092357466015835:50001231000000:2800:55F4286074152FE31295E59C0F225F1BD4F9819FEADF363E992B70AC51CA12C5.gif)

### 状态管理V2观测组件外部输入

**LazyForEach示例**

状态管理V2的[@Param](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-param)装饰器提供了观测自定义组件外部输入变量的能力，可以实现父子组件间的数据同步。将父组件的变量传递给子组件，并用@Param装饰，当父组件变量发生变化时，会通知对应的组件更新。

示例5演示了在LazyForEach中使用@Param装饰器观测数据变化，触发组件更新。

**示例5 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. @ObservedV2
16. class StringData {
17.   @Trace message: string;

18.   constructor(message: string) {
19.     this.message = message;
20.   }
21. }

22. @Entry
23. @ComponentV2
24. struct MyComponent {
25.   data: MyDataSource = new MyDataSource();

26.   aboutToAppear() {
27.     for (let i = 0; i <= 20; i++) {
28.       this.data.pushData(new StringData(`Hello ${i}`));
29.     }
30.   }

31.   build() {
32.     List({ space: 3 }) {
33.       LazyForEach(this.data, (item: StringData, index: number) => {
34.         ListItem() {
35.           ChildComponent({ data: item.message }) // 向自定义组件内传入变量
36.             .onClick(() => {
37.               item.message += '!';
38.             })
39.         }
40.       }, (item: StringData, index: number) => index.toString())
41.     }.cachedCount(5)
42.   }
43. }

44. @ComponentV2
45. struct ChildComponent {
46.   @Param @Require data: string = ''; // 接收来自外部的变量

47.   build() {
48.     Row() {
49.       Text(this.data).fontSize(50)
50.     }
51.   }
52. }

**迁移Repeat**

Repeat本身支持与状态管理V2联合使用，将LazyForEach相关代码修改为Repeat后，即可实现对组件外部输入状态变量的观测。

迁移后的示例如下所示。

**示例5 - 迁移后**

1. @ObservedV2
2. class StringData {
3.   @Trace message: string;

4.   constructor(message: string) {
5.     this.message = message;
6.   }
7. }

8. @Entry
9. @ComponentV2
10. struct MyComponent {
11.   @Local data: StringData[] = [];

12.   aboutToAppear() {
13.     for (let i = 0; i <= 20; i++) {
14.       this.data.push(new StringData(`Hello ${i}`));
15.     }
16.   }

17.   build() {
18.     List({ space: 3 }) {
19.       Repeat(this.data)
20.         .each((repeatItem) => {
21.           ListItem() {
22.             ChildComponent({ data: repeatItem.item.message }) // 向自定义组件内传入变量
23.               .onClick(() => {
24.                 repeatItem.item.message += '!';
25.               })
26.           }
27.         })
28.         .key((item: StringData, index: number) => index.toString())
29.         .virtualScroll()
30.     }.cachedCount(5)
31.   }
32. }

33. @ComponentV2
34. struct ChildComponent {
35.   @Param @Require data: string = ''; // 接收来自外部的变量

36.   build() {
37.     Row() {
38.       Text(this.data).fontSize(50)
39.     }
40.   }
41. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.90430579311480355869393459661229:50001231000000:2800:D4D2486C4784B911F9EE9A49363DC9C8BDDA17CD0B1BC1A8E5741ECB7881C668.gif)

### 拖拽排序

**LazyForEach示例**

LazyForEach的[onMove](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-drag-sorting#onmove)属性提供了拖拽排序能力。

示例6为典型用例。

**示例6 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: string类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: string[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): string {
8.     return this.dataArray[index];
9.   }

10.   public moveDataWithoutNotify(from: number, to: number): void {
11.     let tmp = this.dataArray.splice(from, 1);
12.     this.dataArray.splice(to, 0, tmp[0]);
13.   }

14.   public pushData(data: string): void {
15.     this.dataArray.push(data);
16.     this.notifyDataAdd(this.dataArray.length - 1);
17.   }
18. }

19. @Entry
20. @Component
21. struct Parent {
22.   private data: MyDataSource = new MyDataSource();

23.   aboutToAppear(): void {
24.     for (let i = 0; i < 100; i++) {
25.       this.data.pushData(i.toString());
26.     }
27.   }

28.   build() {
29.     Row() {
30.       List() {
31.         LazyForEach(this.data, (item: string) => {
32.           ListItem() {
33.             Text(item.toString())
34.               .fontSize(16)
35.               .textAlign(TextAlign.Center)
36.               .size({ height: 100, width: '100%' })
37.           }.margin(10)
38.           .borderRadius(10)
39.           .backgroundColor('#FFFFFFFF')
40.         }, (item: string) => item)
41.           .onMove((from: number, to: number) => { // 实现拖拽排序
42.             this.data.moveDataWithoutNotify(from, to);
43.           })
44.       }
45.       .width('100%')
46.       .height('100%')
47.       .backgroundColor('#FFDCDCDC')
48.     }
49.   }
50. }

**迁移Repeat**

Repeat具有与LazyForEach相同的onMove属性。将LazyForEach相关代码修改为Repeat后，即可实现拖拽排序。

迁移后的示例如下所示。

**示例6 - 迁移后**

1. @Entry
2. @ComponentV2
3. struct Parent {
4.   @Local data: string[] = [];

5.   aboutToAppear(): void {
6.     for (let i = 0; i < 100; i++) {
7.       this.data.push(i.toString());
8.     }
9.   }

10.   moveData(from: number, to: number) {
11.     let tmp = this.data.splice(from, 1);
12.     this.data.splice(to, 0, tmp[0]);
13.   }

14.   build() {
15.     Row() {
16.       List() {
17.         Repeat(this.data)
18.           .each((repeatItem) => {
19.             ListItem() {
20.               Text(repeatItem.item.toString())
21.                 .fontSize(16)
22.                 .textAlign(TextAlign.Center)
23.                 .size({ height: 100, width: '100%' })
24.             }.margin(10)
25.             .borderRadius(10)
26.             .backgroundColor('#FFFFFFFF')
27.           })
28.           .key((item: string) => item)
29.           .virtualScroll()
30.           .onMove((from: number, to: number) => { // 实现拖拽排序
31.             this.moveData(from, to);
32.           })
33.       }
34.       .width('100%')
35.       .height('100%')
36.       .backgroundColor('#FFDCDCDC')
37.     }
38.   }
39. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.50484491938529264108091518082071:50001231000000:2800:7CAE3B2495540FB53C8B4D3E84D871A4940E6E483AA646ACA1E03F8F75D22A5D.gif)

### 组件复用

**LazyForEach示例**

LazyForEach自身并不具备组件复用能力，为实现组件复用，需要与[@Reusable](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-reusable)装饰器配合使用（被@Reusable装饰的自定义组件具有复用能力）。

示例7演示了组件复用的典型场景。

**示例7 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. class StringData {
16.   message: string;

17.   constructor(message: string) {
18.     this.message = message;
19.   }
20. }

21. @Entry
22. @Component
23. struct MyComponent {
24.   data: MyDataSource = new MyDataSource();

25.   aboutToAppear() {
26.     for (let i = 0; i <= 30; i++) {
27.       this.data.pushData(new StringData(`Hello${i}`));
28.     }
29.   }

30.   build() {
31.     List({ space: 3 }) {
32.       LazyForEach(this.data, (item: StringData, index: number) => {
33.         ListItem() {
34.           ChildComponent({ data: item })
35.             .onAppear(() => {
36.               console.info(`onAppear: ${item.message}`);
37.             })
38.         }
39.       }, (item: StringData, index: number) => index.toString())
40.     }.cachedCount(5)
41.   }
42. }

43. @Reusable
44. @Component
45. struct ChildComponent {
46.   @State data: StringData = new StringData('');

47.   aboutToAppear(): void {
48.     console.info(`aboutToAppear: ${this.data.message}`);
49.   }

50.   aboutToRecycle(): void {
51.     console.info(`aboutToRecycle: ${this.data.message}`);
52.   }

53.   // 对复用的组件进行数据更新
54.   aboutToReuse(params: Record<string, ESObject>): void {
55.     this.data = params.data as StringData;
56.     console.info(`aboutToReuse: ${this.data.message}`);
57.   }

58.   build() {
59.     Row() {
60.       Text(this.data.message).fontSize(50)
61.     }
62.   }
63. }

**迁移Repeat**

Repeat本身具备组件复用能力，同时也支持与状态管理V2的[@ReusableV2](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-reusablev2)装饰器联合使用。因此，迁移至Repeat后，其组件复用具有两种实现方案。

1. 直接使用Repeat自身的复用能力。
2. 使用@ReusableV2装饰器提供的复用能力。

需要注意的是，Repeat默认使能自身的复用能力，且优先级高于@ReusableV2装饰器。若要使用@ReusableV2装饰器，需要先手动关闭Repeat自身的复用能力（@ReusableV2装饰器从API version 18开始支持，Repeat从API version 19开始支持关闭自身复用能力）。

**示例7 - 迁移方案1：使用Repeat自身的复用能力**

Repeat本身具备复用能力，且默认开启。将LazyForEach相关代码迁移至Repeat后，便已经具备了复用能力。

修改后的示例如下。

1. class StringData {
2.   message: string;

3.   constructor(message: string) {
4.     this.message = message;
5.   }
6. }

7. @Entry
8. @ComponentV2
9. struct MyComponent {
10.   @Local data: StringData[] = [];

11.   aboutToAppear() {
12.     for (let i = 0; i <= 30; i++) {
13.       this.data.push(new StringData(`Hello${i}`));
14.     }
15.   }

16.   build() {
17.     List({ space: 3 }) {
18.       Repeat(this.data) // Repeat自身具备复用功能
19.         .each((repeatItem) => {
20.           ListItem() {
21.             Text(repeatItem.item.message).fontSize(50)
22.           }
23.         })
24.         .key((item: StringData, index: number) => index.toString())
25.         .virtualScroll()
26.     }.cachedCount(5)
27.   }
28. }

**示例7 - 迁移方案2：使用@ReusableV2装饰器**

若要使用@ReusableV2装饰器，首先需要通过.virtualScroll({ reusable: false })关闭Repeat自身的复用功能，再用@ReusableV2装饰需要复用的自定义组件。

相较于Repeat自身的复用，@ReusableV2装饰的自定义组件在回收和复用时，会触发aboutToRecycle和aboutToReuse两个生命周期。

使用@ReusableV2装饰器的迁移示例如下所示。

1. class StringData {
2.   message: string;

3.   constructor(message: string) {
4.     this.message = message;
5.   }
6. }

7. @Entry
8. @ComponentV2
9. struct MyComponent {
10.   @Local data: StringData[] = [];

11.   aboutToAppear() {
12.     for (let i = 0; i <= 30; i++) {
13.       this.data.push(new StringData(`Hello${i}`));
14.     }
15.   }

16.   build() {
17.     List({ space: 3 }) {
18.       Repeat(this.data)
19.         .each((repeatItem) => {
20.           ListItem() {
21.             ChildComponent({ data: repeatItem.item })
22.               .onAppear(() => {
23.                 console.info(`onAppear: ${repeatItem.item.message}`);
24.               })
25.           }
26.         })
27.         .key((item: StringData, index: number) => index.toString())
28.         .virtualScroll({ reusable: false }) // 关闭Repeat自身的复用功能（API 19）
29.     }.cachedCount(5)
30.   }
31. }

32. // 使用@ReusableV2实现组件复用（API 18）
33. @ReusableV2
34. @ComponentV2
35. struct ChildComponent {
36.   @Param data: StringData = new StringData('');

37.   aboutToAppear(): void {
38.     console.info(`aboutToAppear: ${this.data.message}`);
39.   }

40.   aboutToRecycle(): void {
41.     console.info(`aboutToRecycle: ${this.data.message}`);
42.   }

43.   aboutToReuse(): void {
44.     console.info(`aboutToReuse: ${this.data.message}`);
45.   }

46.   build() {
47.     Row() {
48.       Text(this.data.message).fontSize(50)
49.     }
50.   }
51. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.24263212202420592585590536450661:50001231000000:2800:16BFB5890C31649EC35FF4CE09025AA08349FC37026607631E2C028628AD3731.gif)

### 模板渲染

**LazyForEach示例**

LazyForEach自身并不具备模板渲染能力。为实现模板渲染能力，需要开发者自己实现逻辑判断，为不同的数据项选择不同的渲染模板。

示例8演示了模板渲染的典型场景。

**示例8 - 迁移前**

1. /** BasicDataSource代码见文档末尾BasicDataSource示例代码: StringData类型数组的BasicDataSource代码 **/

2. class MyDataSource extends BasicDataSource {
3.   private dataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.dataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.dataArray[index];
9.   }

10.   public pushData(data: StringData): void {
11.     this.dataArray.push(data);
12.     this.notifyDataAdd(this.dataArray.length - 1);
13.   }
14. }

15. class StringData {
16.   message: string;
17.   type: number;

18.   constructor(message: string, type: number) {
19.     this.message = message;
20.     this.type = type;
21.   }

22.   getType(): number {
23.     if (this.type >= 1) {
24.       return 1;
25.     } else {
26.       return 0;
27.     }
28.   }
29. }

30. @Entry
31. @Component
32. struct MyComponent {
33.   data: MyDataSource = new MyDataSource();

34.   aboutToAppear() {
35.     for (let i = 0; i <= 200; i++) {
36.       this.data.pushData(new StringData(`Hello${i}`, i % 2));
37.     }
38.   }

39.   build() {
40.     List({ space: 3 }) {
41.       LazyForEach(this.data, (item: StringData, index: number) => {
42.         ListItem() {
43.           // 开发者自己实现逻辑判断，为不同的数据项选择不同的渲染模板
44.           if (item.getType() == 0) {
45.             // 模板A
46.             ChildComponentA({ data: item })
47.               .onAppear(() => {
48.                 console.info(`type A onAppear: ${item.message}`);
49.               })
50.           } else {
51.             // 模板B
52.             ChildComponentB({ data: item })
53.               .onAppear(() => {
54.                 console.info(`type B onAppear: ${item.message}`);
55.               })
56.           }
57.         }
58.       }, (item: StringData, index: number) => index.toString())
59.     }.cachedCount(5)
60.   }
61. }

62. // 使用@Reusable实现组件复用
63. @Reusable
64. @Component
65. struct ChildComponentA {
66.   @State data: StringData = new StringData('', 0);

67.   aboutToAppear(): void {
68.     console.info(`type A aboutToAppear: ${this.data.message}`);
69.   }

70.   aboutToRecycle(): void {
71.     console.info(`type A aboutToRecycle: ${this.data.message}`);
72.   }

73.   aboutToReuse(params: Record<string, ESObject>): void {
74.     this.data = params.data as StringData;
75.     console.info(`type A aboutToReuse: ${this.data.message}`);
76.   }

77.   build() {
78.     Row() {
79.       Text(this.data.message).fontSize(50)
80.       Button('Type A')
81.     }
82.   }
83. }

84. @Reusable
85. @Component
86. struct ChildComponentB {
87.   @State data: StringData = new StringData('', 0);

88.   aboutToAppear(): void {
89.     console.info(`type B aboutToAppear: ${this.data.message}`);
90.   }

91.   aboutToRecycle(): void {
92.     console.info(`type B aboutToRecycle: ${this.data.message}`);
93.   }

94.   aboutToReuse(params: Record<string, ESObject>): void {
95.     this.data = params.data as StringData;
96.     console.info(`type B aboutToReuse: ${this.data.message}`);
97.   }

98.   build() {
99.     Row() {
100.       Text(this.data.message).fontSize(50).fontColor(Color.Gray)
101.       Text('Type B')
102.     }
103.   }
104. }

**迁移Repeat**

Repeat本身具备模板渲染能力，开发者可以通过[templateId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#templateid)方法为不同的数据项选择不同的模板，再通过[template](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-rendering-control-repeat#template)方法为不同的模板配置不同的组件生成函数。同时，开发者仍然可以选择自己实现逻辑判断，为不同的数据项分配不同的模板。

需要注意的是，如果开发者选择自己实现模板渲染，则需要关闭Repeat自身的复用功能。否则，Repeat在复用子组件时无法选择正确的模板，会导致渲染异常。

**示例8 - 迁移方案1：使用Repeat自身的模板渲染能力**

1. class StringData {
2.   message: string;
3.   type: number;

4.   constructor(message: string, type: number) {
5.     this.message = message;
6.     this.type = type;
7.   }

8.   getType(): number {
9.     if (this.type >= 1) {
10.       return 1;
11.     } else {
12.       return 0;
13.     }
14.   }
15. }

16. @Entry
17. @ComponentV2
18. struct MyComponent {
19.   data: StringData[] = [];

20.   aboutToAppear() {
21.     for (let i = 0; i <= 200; i++) {
22.       this.data.push(new StringData(`Hello${i}`, i % 2));
23.     }
24.   }

25.   build() {
26.     List({ space: 3 }) {
27.       Repeat(this.data)
28.         .each((repeatItem) => {
29.           ListItem() {
30.             Text('Default item')
31.           }
32.         })
33.         .template('A', (repeatItem) => { // 模板A
34.           ListItem() {
35.             Row() {
36.               Text(repeatItem.item.message).fontSize(50)
37.               Button('Type A')
38.             }
39.           }
40.         })
41.         .template('B', (repeatItem) => { // 模板B
42.           ListItem() {
43.             Row() {
44.               Text(repeatItem.item.message).fontSize(50).fontColor(Color.Gray)
45.               Text('Type B')
46.             }
47.           }
48.         })
49.         .templateId((item: StringData) => { // 为不同的数据项选择不同的模板
50.           if (item.getType() == 0) {
51.             return 'A';
52.           } else {
53.             return 'B';
54.           }
55.         })
56.         .key((item: StringData, index: number) => index.toString())
57.         .virtualScroll()
58.     }.cachedCount(5)
59.   }
60. }

**示例8 - 迁移方案2：由开发者实现模板渲染能力**

1. class StringData {
2.   message: string;
3.   type: number;

4.   constructor(message: string, type: number) {
5.     this.message = message;
6.     this.type = type;
7.   }

8.   getType(): number {
9.     if (this.type >= 1) {
10.       return 1;
11.     } else {
12.       return 0;
13.     }
14.   }
15. }

16. @Entry
17. @ComponentV2
18. struct MyComponent {
19.   data: StringData[] = [];

20.   aboutToAppear() {
21.     for (let i = 0; i <= 200; i++) {
22.       this.data.push(new StringData(`Hello${i}`, i % 2));
23.     }
24.   }

25.   build() {
26.     List({ space: 3 }) {
27.       Repeat(this.data)
28.         .each((repeatItem) => {
29.           ListItem() {
30.             // 开发者自己实现逻辑判断，为不同的数据项选择不同的渲染模板
31.             if (repeatItem.item.getType() == 0) {
32.               ChildComponentA({ data: repeatItem.item }) // 模板A
33.                 .onAppear(() => {
34.                   console.info(`type A onAppear: ${repeatItem.item.message}`);
35.                 })
36.             } else {
37.               ChildComponentB({ data: repeatItem.item }) // 模板B
38.                 .onAppear(() => {
39.                   console.info(`type B onAppear: ${repeatItem.item.message}`);
40.                 })
41.             }
42.           }
43.         })
44.         .key((item: StringData, index: number) => index.toString())
45.         .virtualScroll({ reusable: false }) // 关闭Repeat自身的复用功能（API 19），避免渲染异常
46.     }.cachedCount(5)
47.   }
48. }

49. // 使用@ReusableV2实现组件复用（API 18）
50. @ReusableV2
51. @ComponentV2
52. struct ChildComponentA {
53.   @Param data: StringData = new StringData('', 0);

54.   aboutToAppear(): void {
55.     console.info(`type A aboutToAppear: ${this.data.message}`);
56.   }

57.   aboutToRecycle(): void {
58.     console.info(`type A aboutToRecycle: ${this.data.message}`);
59.   }

60.   aboutToReuse(): void {
61.     console.info(`type A aboutToReuse: ${this.data.message}`);
62.   }

63.   build() {
64.     Row() {
65.       Text(this.data.message).fontSize(50)
66.       Button('Type A')
67.     }
68.   }
69. }

70. @ReusableV2
71. @ComponentV2
72. struct ChildComponentB {
73.   @Param data: StringData = new StringData('', 0);

74.   aboutToAppear(): void {
75.     console.info(`type B aboutToAppear: ${this.data.message}`);
76.   }

77.   aboutToRecycle(): void {
78.     console.info(`type B aboutToRecycle: ${this.data.message}`);
79.   }

80.   aboutToReuse(): void {
81.     console.info(`type B aboutToReuse: ${this.data.message}`);
82.   }

83.   build() {
84.     Row() {
85.       Text(this.data.message).fontSize(50).fontColor(Color.Gray)
86.       Text('Type B')
87.     }
88.   }
89. }

运行后界面如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163959.16951959361312922505157389391226:50001231000000:2800:13C72E252FDC6CE53545D7A59467B7BD1037B80FD52FCFA7AE75684E3288912F.gif)

## BasicDataSource示例代码

### string类型数组的BasicDataSource代码

1. // BasicDataSource实现了IDataSource接口，用于管理listener监听，以及通知LazyForEach数据更新
2. class BasicDataSource implements IDataSource {
3.   private listeners: DataChangeListener[] = [];
4.   private originDataArray: string[] = [];

5.   public totalCount(): number {
6.     return this.originDataArray.length;
7.   }

8.   public getData(index: number): string {
9.     return this.originDataArray[index];
10.   }

11.   // 该方法为框架侧调用，为LazyForEach组件向其数据源处添加listener监听
12.   registerDataChangeListener(listener: DataChangeListener): void {
13.     if (this.listeners.indexOf(listener) < 0) {
14.       console.info('add listener');
15.       this.listeners.push(listener);
16.     }
17.   }

18.   // 该方法为框架侧调用，为对应的LazyForEach组件在数据源处去除listener监听
19.   unregisterDataChangeListener(listener: DataChangeListener): void {
20.     const pos = this.listeners.indexOf(listener);
21.     if (pos >= 0) {
22.       console.info('remove listener');
23.       this.listeners.splice(pos, 1);
24.     }
25.   }

26.   // 通知LazyForEach组件需要重载所有子组件
27.   notifyDataReload(): void {
28.     this.listeners.forEach(listener => {
29.       listener.onDataReloaded();
30.     });
31.   }

32.   // 通知LazyForEach组件需要在index对应索引处添加子组件
33.   notifyDataAdd(index: number): void {
34.     this.listeners.forEach(listener => {
35.       listener.onDataAdd(index);
36.       // 写法2：listener.onDatasetChange([{type: DataOperationType.ADD, index: index}]);
37.     });
38.   }

39.   // 通知LazyForEach组件在index对应索引处数据有变化，需要重建该子组件
40.   notifyDataChange(index: number): void {
41.     this.listeners.forEach(listener => {
42.       listener.onDataChange(index);
43.       // 写法2：listener.onDatasetChange([{type: DataOperationType.CHANGE, index: index}]);
44.     });
45.   }

46.   // 通知LazyForEach组件需要在index对应索引处删除该子组件
47.   notifyDataDelete(index: number): void {
48.     this.listeners.forEach(listener => {
49.       listener.onDataDelete(index);
50.       // 写法2：listener.onDatasetChange([{type: DataOperationType.DELETE, index: index}]);
51.     });
52.   }

53.   // 通知LazyForEach组件将from索引和to索引处的子组件进行交换
54.   notifyDataMove(from: number, to: number): void {
55.     this.listeners.forEach(listener => {
56.       listener.onDataMove(from, to);
57.       // 写法2：listener.onDatasetChange(
58.       //         [{type: DataOperationType.EXCHANGE, index: {start: from, end: to}}]);
59.     });
60.   }

61.   notifyDatasetChange(operations: DataOperation[]): void {
62.     this.listeners.forEach(listener => {
63.       listener.onDatasetChange(operations);
64.     });
65.   }
66. }

### StringData类型数组的BasicDataSource代码

1. class BasicDataSource implements IDataSource {
2.   private listeners: DataChangeListener[] = [];
3.   private originDataArray: StringData[] = [];

4.   public totalCount(): number {
5.     return this.originDataArray.length;
6.   }

7.   public getData(index: number): StringData {
8.     return this.originDataArray[index];
9.   }

10.   registerDataChangeListener(listener: DataChangeListener): void {
11.     if (this.listeners.indexOf(listener) < 0) {
12.       console.info('add listener');
13.       this.listeners.push(listener);
14.     }
15.   }

16.   unregisterDataChangeListener(listener: DataChangeListener): void {
17.     const pos = this.listeners.indexOf(listener);
18.     if (pos >= 0) {
19.       console.info('remove listener');
20.       this.listeners.splice(pos, 1);
21.     }
22.   }

23.   notifyDataReload(): void {
24.     this.listeners.forEach(listener => {
25.       listener.onDataReloaded();
26.     });
27.   }

28.   notifyDataAdd(index: number): void {
29.     this.listeners.forEach(listener => {
30.       listener.onDataAdd(index);
31.     });
32.   }

33.   notifyDataChange(index: number): void {
34.     this.listeners.forEach(listener => {
35.       listener.onDataChange(index);
36.     });
37.   }

38.   notifyDataDelete(index: number): void {
39.     this.listeners.forEach(listener => {
40.       listener.onDataDelete(index);
41.     });
42.   }

43.   notifyDataMove(from: number, to: number): void {
44.     this.listeners.forEach(listener => {
45.       listener.onDataMove(from, to);
46.     });
47.   }

48.   notifyDatasetChange(operations: DataOperation[]): void {
49.     this.listeners.forEach(listener => {
50.       listener.onDatasetChange(operations);
51.     });
52.   }
53. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-new-rendering-control-repeat "Repeat：可复用的循环渲染")
# 组件导航(Navigation) (推荐)

更新时间: 2025-12-16 16:39

组件导航（[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)）主要用于实现Navigation页面（[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)）间的跳转，支持在不同Navigation页面间传递参数，提供灵活的跳转栈操作，从而更便捷地实现对不同页面的访问和复用。本文将从组件导航（Navigation）的显示模式、路由操作、子页面管理、跨包跳转以及跳转动效等几个方面进行详细介绍。

[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)是路由导航的根视图容器，一般作为页面（@Entry）的根容器，包括单栏（Stack）、分栏（Split）和自适应（Auto）三种显示模式。Navigation组件适用于模块内和跨模块的路由切换，通过组件级路由能力实现更加自然流畅的转场体验，并提供多种标题栏样式来呈现更好的标题和内容联动效果。一次开发，多端部署场景下，Navigation组件能够自动适配窗口显示大小，在窗口较大的场景下自动切换分栏展示效果。

Navigation组件主要包含​导航页和子页。导航页由标题栏（包含菜单栏）、内容区和工具栏组成，可以通过[hideNavBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#hidenavbar9)属性进行隐藏，导航页不存在[路由栈](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)中，与子页，以及子页之间可以通过路由操作进行切换。

在API version 9上，Navigation需要配合[NavRouter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navrouter)组件实现页面路由。从API version 10开始，更推荐使用[NavPathStack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)实现页面路由。

## 设置页面显示模式

[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)组件通过[mode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#mode9)属性设置页面的显示模式。

- 自适应模式
    
    Navigation组件默认为自适应模式，此时mode属性为NavigationMode.Auto。自适应模式下，当页面宽度大于等于一定阈值( API version 9及以前：520vp，API version 10及以后：600vp )时，Navigation组件采用分栏模式，反之采用单栏模式。
    
    收起
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .mode(NavigationMode.Auto)
    
- 单栏模式
    
    单栏模式适用于窄屏设备，发生路由跳转时，整个页面都会被替换。
    
    **图1** 单栏布局示意图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163913.39247956913604846372315161784606:50001231000000:2800:925B5823D0F65790083C974E6538E7DE423A4CD226690DE88CA88D854F7E3F88.png)
    
    将mode属性设置为NavigationMode.Stack，Navigation组件即可设置为单栏显示模式。
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .mode(NavigationMode.Stack)
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163913.94781536402667387449603288907682:50001231000000:2800:5E623CF9E47772521FAF0D79441B418D1FBF0ED5B16BADE1E1FC081CCAEFACA4.jpg)
    
- 分栏模式
    
    分栏模式适用于宽屏设备，分为左右两部分，发生路由跳转时，只有右边子页会被替换。
    
    **图2** 分栏布局示意图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163913.44635127908442444956882181138608:50001231000000:2800:29D142503D371ED20B0604DA5CCCBD05F9767952FCC5D5CE19B49743361AF01D.png)
    
    将mode属性设置为NavigationMode.Split，Navigation组件即可设置为分栏显示模式。
    
    1. import { hilog } from '@kit.PerformanceAnalysisKit';
    2. const DOMAIN = 0x0000;
    3. @Entry
    4. @Component
    5. struct NavigationExample {
    6.   @State toolTmp: ToolbarItem = {
    7.     'value': "func",
    8.     'icon': "./image/ic_public_highlights.svg",  // 当前目录image文件夹下的图标资源
    9.     'action': () => {}
    10.   };
    11.   @Provide('navPathStack') navPathStack: NavPathStack = new NavPathStack();
    12.   private arr: number[] = [1, 2, 3];
    
    13.   @Builder
    14.   pageMap(name: string) {
    15.     if (name === "NavDestinationTitle1") {
    16.       pageOneTmp();
    17.     } else if (name === "NavDestinationTitle2") {
    18.       pageTwoTmp();
    19.     } else if (name === "NavDestinationTitle3") {
    20.       pageThreeTmp();
    21.     }
    22.   }
    
    23.   build() {
    24.     Column() {
    25.       Navigation(this.navPathStack) {
    26.         TextInput({ placeholder: 'search...' })
    27.           .width("90%")
    28.           .height(40)
    29.           .backgroundColor('#FFFFFF')
    
    30.         List({ space: 12 }) {
    31.           ForEach(this.arr, (item: number) => {
    32.             ListItem() {
    33.               Text("Page" + item)
    34.                 .width("100%")
    35.                 .height(72)
    36.                 .backgroundColor('#FFFFFF')
    37.                 .borderRadius(24)
    38.                 .fontSize(16)
    39.                 .fontWeight(500)
    40.                 .textAlign(TextAlign.Center)
    41.                 .onClick(() => {
    42.                   this.navPathStack.pushPath({ name: 'NavDestinationTitle' + item });
    43.                 })
    44.             }
    45.           }, (item: number) => item.toString())
    46.         }
    47.         .width("90%")
    48.         .margin({ top: 12 })
    49.       }
    50.       .title("主标题")
    51.       .mode(NavigationMode.Split)
    52.       .navDestination(this.pageMap)
    53.       .menus([
    54.         {
    55.           value: "", icon: "./image/ic_public_search.svg", action: () => {
    56.           }
    57.         },
    58.         {
    59.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    60.           }
    61.         },
    62.         {
    63.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    64.           }
    65.         },
    66.         {
    67.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    68.           }
    69.         },
    70.         {
    71.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    72.           }
    73.         }
    74.       ])
    75.       .toolbarConfiguration([this.toolTmp, this.toolTmp, this.toolTmp])
    76.     }
    77.     .height('100%')
    78.     .width('100%')
    79.     .backgroundColor('#F1F3F5')
    80.   }
    81. }
    
    82. // PageOne.ets
    83. @Component
    84. export struct pageOneTmp {
    85.   @Consume('navPathStack') navPathStack: NavPathStack;
    86.   context = this.getUIContext().getHostContext();
    87.   build() {
    88.     NavDestination() {
    89.       Column() {
    90.         Text("NavDestinationContent1")
    91.       }.width('100%').height('100%')
    92.     }.title("NavDestinationTitle1")
    93.     .onBackPressed(() => {
    94.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈栈顶元素
    95.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
    96.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
    97.         JSON.stringify(popDestinationInfo));
    98.       return true;
    99.     })
    100.   }
    101. }
    
    102. // PageTwo.ets
    103. @Component
    104. export struct pageTwoTmp {
    105.   @Consume('navPathStack') navPathStack: NavPathStack;
    106.   context = this.getUIContext().getHostContext();
    107.   build() {
    108.     NavDestination() {
    109.       Column() {
    110.         Text("NavDestinationContent2")
    111.       }.width('100%').height('100%')
    112.     }.title("NavDestinationTitle2")
    113.     .onBackPressed(() => {
    114.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈栈顶元素
    115.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
    116.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
    117.         JSON.stringify(popDestinationInfo));
    118.       return true;
    119.     })
    120.   }
    121. }
    
    122. // PageThree.ets
    123. @Component
    124. export struct pageThreeTmp {
    125.   @Consume('navPathStack') navPathStack: NavPathStack;
    126.   context = this.getUIContext().getHostContext();
    127.   build() {
    128.     NavDestination() {
    129.       Column() {
    130.         Text("NavDestinationContent3")
    131.       }.width('100%').height('100%')
    132.     }.title("NavDestinationTitle3")
    133.     .onBackPressed(() => {
    134.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈栈顶元素
    135.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
    136.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
    137.         JSON.stringify(popDestinationInfo));
    138.       return true;
    139.     })
    140.   }
    141. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.38522712307407973042152555339603:50001231000000:2800:210862FB40488CA357496A333F8C814C3375FF85E9C6EC2074FEB76A3517DB98.jpg)
    

## 设置标题栏模式

标题栏在界面顶部，用于呈现界面名称和操作入口，Navigation组件通过[titleMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#titlemode)属性设置标题栏模式。

说明

Navigation或NavDestination未设置主副标题并且没有返回键时，不显示标题栏。

- Mini模式
    
    普通型标题栏，用于一级页面不需要突出标题的场景。
    
    **图3** Mini模式标题栏
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.88917640640829362862283509704068:50001231000000:2800:A6899C99862B2B677DC35E58E135729F02D8AFC91611D3785F415702713E36CA.jpg)
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .titleMode(NavigationTitleMode.Mini)
    
- Full模式
    
    强调型标题栏，用于一级页面需要突出标题的场景。
    
    **图4** Full模式标题栏
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.76716253096362819389528325214830:50001231000000:2800:4F8C50DC6DC180EEDFCCD3B4029968E2FF19618370ED06D5B688BD572BCFB1EA.jpg)
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .titleMode(NavigationTitleMode.Full)
    

## 设置菜单栏

菜单栏位于Navigation组件的右上角，开发者可以通过[menus](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#menus)属性进行设置。menus支持Array<[NavigationMenuItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navigationmenuitem)>和[CustomBuilder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-types#custombuilder8)两种参数类型。使用Array<NavigationMenuItem>类型时，竖屏最多支持显示3个图标，横屏最多支持显示5个图标，多余的图标会被放入自动生成的更多图标。

**图5** 设置了3个图标的菜单栏

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.73673441631946749215245150548418:50001231000000:2800:807E87EF7E5ADFFA9A9A846ED20101AC4AB9A0643F48CF41A0150795BC65B0DD.jpg)

1. let toolTmp: NavigationMenuItem  = {
2.   'value': 'func',
3.   'icon': 'ets/pages/navigation/template1/image/ic_public_add.svg',
4.   'action': () => {}
5. };
6. // ...
7.       Navigation(this.navPathStack) {
8.         // ...
9.       }
10.       .menus([toolTmp, toolTmp, toolTmp])

图片也可以引用resources中的资源。

1. let toolTmp: NavigationMenuItem  = {
2.   'value': 'func',
3.   'icon': 'resources/base/media/ic_public_add.svg',
4.   'action': () => {}
5. };
6. // ...
7.       Navigation(this.navPathStack) {
8.         // ...
9.       }
10.       .menus([toolTmp, toolTmp, toolTmp])

**图6** 设置了4个图标的菜单栏

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.50787801697064920089908207920699:50001231000000:2800:E62E892050408B63ACDFEA78F71C670DAD4153B291E146916FEB0AD290D16B77.jpg)

1. let toolTmp: NavigationMenuItem  = {
2.   'value': 'func',
3.   'icon': 'ets/pages/navigation/template1/image/ic_public_add.svg',
4.   'action': () => {}
5. };
6. // ...
7.       Navigation(this.navPathStack) {
8.         // ...
9.       }
10.       // 竖屏最多支持显示3个图标，多余的图标会被放入自动生成的更多图标
11.       .menus([toolTmp, toolTmp, toolTmp, toolTmp])

## 设置工具栏

工具栏位于Navigation组件的底部，开发者可以通过[toolbarConfiguration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#toolbarconfiguration10)属性进行设置。

**图7** 工具栏

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.17051218093016793180970087149026:50001231000000:2800:99FD7107F1BDE63C8614828B7CB573E786230469AEF4242386295E47BECFC7B5.jpg)

1. let toolTmp: ToolbarItem = {
2.   'value': 'func',
3.   'icon': 'ets/pages/navigation/template1/image/ic_public_highlights.svg',
4.   'action': () => {}
5. };
6. let tooBar: ToolbarItem[] = [toolTmp,toolTmp,toolTmp];
7. // ...
8.       Navigation(this.navPathStack) {
9.         // ...
10.       }
11.       .toolbarConfiguration(tooBar)

## 路由操作

Navigation路由相关的操作都是基于导航控制器[NavPathStack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)提供的方法进行，每个Navigation都需要创建并传入一个NavPathStack对象，用于管理页面。主要涉及页面跳转、页面返回、页面替换、页面删除、参数获取、路由拦截等功能。

从API version 12开始，导航控制器允许被继承。开发者可以在派生类中自定义属性和方法，也可以重写父类的方法。派生类对象可以替代基类NavPathStack对象使用。Navigation中的[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)页面存在于NavPathStack中，以栈的结构管理，我们称为路由栈。具体示例代码参见：[导航控制器继承示例代码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#%E7%A4%BA%E4%BE%8B10%E5%AE%9A%E4%B9%89%E5%AF%BC%E8%88%AA%E6%8E%A7%E5%88%B6%E5%99%A8%E6%B4%BE%E7%94%9F%E7%B1%BB)。

说明

1.不建议开发者通过监听生命周期的方式管理自己的路由栈。

2.在应用处于后台状态下，调用NavPathStack的栈操作方法，会在应用再次回到前台状态时触发刷新。

1. @Entry
2. @Component
3. struct Index {
4.   // 创建一个导航控制器对象并传入Navigation
5.   pageStack: NavPathStack = new NavPathStack();

6.   build() {
7.     Navigation(this.pageStack) {
8.     }
9.     .title('Main')
10.   }
11. }

### 页面跳转

NavPathStack通过Push相关的接口（如[pushPath](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpath10)、[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)、[pushDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushdestination11)、[pushDestinationByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushdestinationbyname11)）去实现页面跳转的功能，主要分为以下三类：

1. 普通跳转，通过页面的name去跳转，并可以携带param。
    
    1. this.pageStack.pushPath({ name: "PageOne", param: "PageOne Param" });
    2. this.pageStack.pushPathByName("PageOne", "PageOne Param");
    
2. 带返回回调的跳转，跳转时添加onPop回调，能在页面出栈时获取返回信息，并进行处理。
    
    1. this.pageStack.pushPathByName('PageOne', "PageOne Param", (popInfo) => {
    2.   console.info('Pop page name is: ' + popInfo.info.name + ', result: ' + JSON.stringify(popInfo.result));
    3. });
    
3. 带错误码的跳转，跳转结束会触发异步回调，返回错误码信息。
    
    1. this.pageStack.pushDestination({name: "PageOne", param: "PageOne Param"})
    2.   .catch((error: BusinessError) => {
    3.     console.error(`Push destination failed, error code = ${error.code}, error.message = ${error.message}.`);
    4.   }).then(() => {
    5.     console.info('Push destination succeed.');
    6.   });
    7. this.pageStack.pushDestinationByName("PageOne", "PageOne Param")
    8.   .catch((error: BusinessError) => {
    9.     console.error(`Push destination failed, error code = ${error.code}, error.message = ${error.message}.`);
    10.   }).then(() => {
    11.     console.info('Push destination succeed.');
    12.   });
    

### 页面返回

NavPathStack通过pop相关接口（如[pop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pop10)、[popToName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#poptoname10)、[popToIndex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#poptoindex10)、[clear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#clear10)）去实现页面返回功能。

1. // 返回到上一页
2. this.pageStack.pop();
3. // 返回到上一个PageOne页面
4. this.pageStack.popToName("PageOne");
5. // 返回到索引为1的页面
6. this.pageStack.popToIndex(1);
7. // 返回到根首页（清除栈中所有页面）
8. this.pageStack.clear();

### 页面替换

NavPathStack通过Replace相关接口（如[replacePath](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#replacepath11)、[replacePathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#replacepathbyname11)、[replaceDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#replacedestination18)）去实现页面替换功能。

1. // 将栈顶页面替换为PageOne
2. this.pageStack.replacePath({ name: "PageOne", param: "PageOne Param" });
3. this.pageStack.replacePathByName("PageOne", "PageOne Param");
4. // 带错误码的替换，跳转结束会触发异步回调，返回错误码信息
5. this.pageStack.replaceDestination({name: "PageOne", param: "PageOne Param"})
6.   .catch((error: BusinessError) => {
7.     console.error(`Replace destination failed, error code = ${error.code}, error.message = ${error.message}.`);
8.   }).then(() => {
9.     console.info('Replace destination succeed.');
10.   })

### 页面删除

NavPathStack通过Remove相关接口（如[removeByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#removebyname11)、[removeByIndexes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#removebyindexes11)、[removeByNavDestinationId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#removebynavdestinationid12)）去实现删除路由栈中特定页面的功能。

1. // 删除栈中name为PageOne的所有页面
2. this.pageStack.removeByName("PageOne");
3. // 删除指定索引的页面
4. this.pageStack.removeByIndexes([1, 3, 5]);
5. // 删除指定id的页面
6. this.pageStack.removeByNavDestinationId("1");

### 移动页面

NavPathStack通过Move相关接口（如[moveToTop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#movetotop10)、[moveIndexToTop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#moveindextotop10)）去实现移动路由栈中特定页面到栈顶的功能。

1. // 移动栈中name为PageOne的页面到栈顶
2. this.pageStack.moveToTop("PageOne");
3. // 移动栈中索引为1的页面到栈顶
4. this.pageStack.moveIndexToTop(1);

### 参数获取

[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)子页第一次创建时会触发[onReady](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onready11)回调，可以获取此页面对应的参数。

1. @Component
2. struct Page01 {
3.   pathStack: NavPathStack | undefined = undefined;
4.   pageParam: string = '';

5.   build() {
6.     NavDestination() {
7.       // ...
8.     }.title('Page01')
9.     .onReady((context: NavDestinationContext) => {
10.       this.pathStack = context.pathStack;
11.       this.pageParam = context.pathInfo.param as string;
12.     })
13.   }
14. }

NavDestination组件中可以通过设置[onResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onresult15)接口，接收返回时传递的路由参数。

1. class NavParam {
2.   desc: string = 'navigation-param'
3. }

4. @Component
5. struct DemoNavDestination {
6.   // ...
7.   build() {
8.     NavDestination() {
9.       // ...
10.     }
11.     .onResult((param: Object) => {
12.       if (param instanceof NavParam) {
13.         console.info('TestTag', 'get NavParam, its desc: ' + (param as NavParam).desc);
14.         return;
15.       }
16.       console.info('TestTag', 'param not instance of NavParam');
17.     })
18.   }
19. }

其他业务场景，可以通过主动调用NavPathStack的Get相关接口（如[getAllPathName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getallpathname10)、[getParamByIndex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getparambyindex10)、[getParamByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getparambyname10)、[getIndexByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getindexbyname10)）去获取指定页面的参数。

1. // 获取栈中所有页面name集合
2. this.pageStack.getAllPathName();
3. // 获取索引为1的页面参数
4. this.pageStack.getParamByIndex(1);
5. // 获取PageOne页面的参数
6. this.pageStack.getParamByName("PageOne");
7. // 获取PageOne页面的索引集合
8. this.pageStack.getIndexByName("PageOne");

### 路由拦截

NavPathStack提供了[setInterception](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#setinterception12)方法，用于设置Navigation页面跳转拦截回调。该方法需要传入一个[NavigationInterception](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navigationinterception12)对象，该对象包含三个回调函数：

|名称|描述|
|:--|:--|
|willShow|页面跳转前回调，允许操作栈，在当前跳转生效。|
|didShow|页面跳转后回调，在该回调中操作栈会在下一次跳转生效。|
|modeChange|Navigation单双栏显示状态发生变更时触发该回调。|

说明

无论是哪个回调，在进入回调时路由栈都已经发生了变化。

开发者可以在willShow回调中通过修改路由栈来实现路由拦截重定向的能力。

1. this.pageStack.setInterception({
2.   willShow: (from: NavDestinationContext | "navBar", to: NavDestinationContext | "navBar",
3.     operation: NavigationOperation, animated: boolean) => {
4.     if (typeof to === "string") {
5.       console.info("target page is navigation home page.");
6.       return;
7.     }
8.     // 将跳转到PageTwo的路由重定向到PageOne
9.     let target: NavDestinationContext = to as NavDestinationContext;
10.     if (target.pathInfo.name === 'PageTwo') {
11.       target.pathStack.pop();
12.       target.pathStack.pushPathByName('PageOne', null);
13.     }
14.   }
15. })

### 单例跳转

通过设置[LaunchMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#launchmode12%E6%9E%9A%E4%B8%BE%E8%AF%B4%E6%98%8E)为LaunchMode.MOVE_TO_TOP_SINGLETON或LaunchMode.POP_TO_SINGLETON，可以实现Navigation路由栈的单实例跳转。单实例跳转的规则如下：

1. 当指定为LaunchMode.MOVE_TO_TOP_SINGLETON时，系统会从栈底到栈顶查找具有指定名称的NavDestination。找到后，该页面将被移动到栈顶（replace操作会用指定的NavDestination替换当前栈顶）。
2. 若指定为LaunchMode.POP_TO_SINGLETON，系统同样会从栈底到栈顶查找具有指定名称的NavDestination。找到后，便会移除该NavDestination上方的所有页面（replace操作会用指定的NavDestination替换当前栈顶）。

当栈中存在的NavDestination页面通过单实例方式移动到栈顶时，将触发[onNewParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onnewparam19)回调。

有关单实例跳转的示例代码，可以参考[Navigation单例跳转示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#%E7%A4%BA%E4%BE%8B2%E4%BD%BF%E7%94%A8%E5%AF%BC%E8%88%AA%E6%8E%A7%E5%88%B6%E5%99%A8%E6%96%B9%E6%B3%95)。

## 子页面

[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)是[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)子页面的根容器，用于承载子页面的一些特殊属性以及生命周期等。NavDestination可以设置独立的标题栏和菜单栏等属性，使用方法与Navigation相同。NavDestination也可以通过[mode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#mode11)属性设置不同的显示类型，用于满足不同页面的诉求。

### 页面显示类型

- 标准类型
    
    NavDestination组件默认为标准类型，此时mode属性为NavDestinationMode.STANDARD。标准类型的NavDestination的生命周期跟随其在NavPathStack路由栈中的位置变化而改变。
    
- 弹窗类型
    
    NavDestination设置mode为NavDestinationMode.DIALOG弹窗类型，此时整个NavDestination默认透明显示。弹窗类型的NavDestination显示和消失时不会影响下层标准类型的NavDestination的显示和生命周期，两者可以同时显示。
    
    1. // Dialog NavDestination
    2. @Entry
    3. @Component
    4.  struct Index {
    5.    @Provide('NavPathStack') pageStack: NavPathStack = new NavPathStack();
    
    6.    @Builder
    7.    PagesMap(name: string) {
    8.      if (name == 'DialogPage') {
    9.        DialogPage();
    10.      }
    11.    }
    
    12.    build() {
    13.      Navigation(this.pageStack) {
    14.        Button('Push DialogPage')
    15.          .margin(20)
    16.          .width('80%')
    17.          .onClick(() => {
    18.            this.pageStack.pushPathByName('DialogPage', '');
    19.          })
    20.      }
    21.      .mode(NavigationMode.Stack)
    22.      .title('Main')
    23.      .navDestination(this.PagesMap)
    24.    }
    25.  }
    
    26.  @Component
    27.  export struct DialogPage {
    28.    @Consume('NavPathStack') pageStack: NavPathStack;
    
    29.    build() {
    30.      NavDestination() {
    31.        Stack({ alignContent: Alignment.Center }) {
    32.          Column() {
    33.            Text("Dialog NavDestination")
    34.              .fontSize(20)
    35.              .margin({ bottom: 100 })
    36.            Button("Close").onClick(() => {
    37.              this.pageStack.pop();
    38.            }).width('30%')
    39.          }
    40.          .justifyContent(FlexAlign.Center)
    41.          .backgroundColor(Color.White)
    42.          .borderRadius(10)
    43.          .height('30%')
    44.          .width('80%')
    45.        }.height("100%").width('100%')
    46.      }
    47.      .backgroundColor('rgba(0,0,0,0.5)')
    48.      .hideTitleBar(true)
    49.      .mode(NavDestinationMode.DIALOG)
    50.    }
    51.  }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.54044996889160545821333494615153:50001231000000:2800:1C6F64946E20589F1ADDBC055027E949D521EFD4BDC226343350F6401D3A6E86.png)
    

### 页面生命周期

Navigation作为路由容器，其生命周期承载在NavDestination组件上，以组件事件的形式开放。

其生命周期大致可分为三类，自定义组件生命周期、通用组件生命周期和自有生命周期。其中，[aboutToAppear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttoappear)和[aboutToDisappear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttodisappear)是自定义组件的生命周期(NavDestination外层包含的自定义组件)，[OnAppear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-events-show-hide#onappear)和[OnDisappear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-events-show-hide#ondisappear)是组件的通用生命周期。剩下的生命周期为NavDestination独有。

生命周期时序如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.71014053475673058396905454101583:50001231000000:2800:2E7A765B6F0E13E37F64EA39C86F41B0C6FD73A0946A0B1D7B98F3744C840BB3.png)

- **aboutToAppear**：在创建自定义组件后，执行其build()函数之前执行（NavDestination创建之前），允许在该方法中改变状态变量，更改将在后续执行build()函数中生效。
- **onWillAppear**：NavDestination创建后，挂载到组件树之前执行，在该方法中更改状态变量会在当前帧显示生效。
- **onAppear**：通用生命周期事件，NavDestination组件挂载到组件树时执行。
- **onWillShow**：NavDestination组件布局显示之前执行，此时页面不可见（应用切换到前台不会触发）。
- **onShown**：NavDestination组件布局显示之后执行，此时页面已完成布局。
- **onActive**：NavDestination处于激活态（处于栈顶可操作，且上层无特殊组件遮挡）触发。
- **onWillHide**：NavDestination组件触发隐藏之前执行（应用切换到后台不会触发）。
- **onInactive**：NavDestination组件处于非激活态（处于非栈顶不可操作，或处于栈顶时上层有特殊组件遮挡）触发。
- **onHidden**：NavDestination组件触发隐藏后执行（非栈顶页面push进栈，栈顶页面pop出栈或应用切换到后台）。
- **onWillDisappear**：NavDestination组件即将销毁之前执行，如果有转场动画，会在动画前触发（栈顶页面pop出栈）。
- **onDisappear**：通用生命周期事件，NavDestination组件从组件树上卸载销毁时执行。
- **aboutToDisappear**：自定义组件析构销毁之前执行，不允许在该方法中改变状态变量。

### 页面监听和查询

为了方便组件跟页面解耦，在NavDestination子页面内部的自定义组件可以通过全局方法监听或查询到页面的一些状态信息。

- 页面信息查询
    
    自定义组件提供[queryNavDestinationInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-api#querynavdestinationinfo)方法，可以在NavDestination内部查询到当前所属页面的信息，返回值为[NavDestinationInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-observer#navdestinationinfo)，若查询不到则返回undefined。
    
    1.  import { uiObserver } from '@kit.ArkUI';
    
    2.  // NavDestination内的自定义组件
    3.  @Component
    4.  struct MyComponent {
    5.    navDesInfo: uiObserver.NavDestinationInfo | undefined;
    
    6.    aboutToAppear(): void {
    7.      this.navDesInfo = this.queryNavDestinationInfo();
    8.    }
    
    9.    build() {
    10.        Column() {
    11.          Text("所属页面Name: " + this.navDesInfo?.name)
    12.        }.width('100%').height('100%')
    13.    }
    14.  }
    
- 页面状态监听
    
    通过[observer.on('navDestinationUpdate')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-observer#uiobserveronnavdestinationupdate)提供的注册接口可以注册NavDestination生命周期变化的监听，使用方式如下：
    
    1. uiObserver.on('navDestinationUpdate', (info) => {
    2.      console.info('NavDestination state update', JSON.stringify(info));
    3.  });
    
    也可以注册页面切换的状态回调，能在页面发生路由切换的时候拿到对应的页面信息[NavDestinationSwitchInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-observer#navdestinationswitchinfo12)，并且提供了UIAbilityContext和UIContext不同范围的监听：
    
    4.  // 在UIAbility中使用
    5.  import { UIContext, uiObserver } from '@kit.ArkUI';
    
    6.  // callbackFunc是开发者定义的监听回调函数
    7.  function callbackFunc(info: uiObserver.NavDestinationSwitchInfo) {}
    8.  uiObserver.on('navDestinationSwitch', this.context, callbackFunc);
    
    9.  // 可以通过窗口的getUIContext()方法获取对应的UIContent
    10.  uiContext: UIContext | null = null;
    11.  uiObserver.on('navDestinationSwitch', this.uiContext, callbackFunc);
    

## 页面转场

[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)默认提供了页面切换的转场动画，通过导航控制器操作时，会触发不同的转场效果（API version 13之前，[Dialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-base-dialog-overview)类型的页面默认无转场动画。从API version13开始，Dialog类型的页面支持系统转场动画。），Navigation也提供了关闭系统转场、自定义转场以及共享元素转场的能力。系统默认动画时长由物理曲线参数决定，不同设备上动画时长存在差异。

### 关闭转场

- 全局关闭
    
    Navigation通过NavPathStack中提供的[disableAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#disableanimation11)方法可以在当前Navigation中关闭或打开所有转场动画。
    
    1. pageStack: NavPathStack = new NavPathStack();
    
    2. aboutToAppear(): void {
    3.   this.pageStack.disableAnimation(true);
    4. }
    
- 单次关闭
    
    NavPathStack中提供的Push、Pop、Replace等接口中可以设置animated参数，默认为true表示有转场动画，需要单次关闭转场动画可以置为false，不影响下次转场动画。
    
    1. pageStack: NavPathStack = new NavPathStack();
    
    2. this.pageStack.pushPath({ name: "PageOne" }, false);
    3. this.pageStack.pop(false);
    

### 自定义转场

- Navigation自定义转场
    
    Navigation自定义转场动画能力通过[customNavContentTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#customnavcontenttransition11)事件提供，可以通过以下三步定义自定义转场动画：
    
    1. 构建一个自定义转场动画工具类CustomNavigationUtils，通过一个Map管理各页面的自定义动画对象CustomTransition。页面在创建时注册其自定义转场动画对象，在销毁时取消注册。
    2. 实现一个转场协议对象[NavigationAnimatedTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navigationanimatedtransition11)。其中，timeout属性表示转场结束的超时时间，默认为1000ms，transition属性为自定义的转场动画方法。开发者需在此实现自己的转场动画逻辑，系统在转场开始时会调用此方法，onTransitionEnd为转场结束时的回调。
    3. 调用customNavContentTransition方法并返回实现的转场协议对象，若返回undefined，则使用系统默认转场。
    
    具体示例代码可参考[Navigation自定义转场示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#%E7%A4%BA%E4%BE%8B3%E8%AE%BE%E7%BD%AE%E5%8F%AF%E4%BA%A4%E4%BA%92%E8%BD%AC%E5%9C%BA%E5%8A%A8%E7%94%BB)。
    
- NavDestination自定义转场
    
    [NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)支持自定义转场动画，通过设置[customTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#customtransition15)属性即可实现单个页面的自定义转场效果。要实现这一功能，需完成以下步骤：
    
    1. 实现[NavDestination的转场代理](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#navdestinationtransitiondelegate15)，针对不同的堆栈操作类型返回自定义的转场协议对象[NavDestinationTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#navdestinationtransition15)。其中，event是必填参数，需在此处编写自定义转场动画的逻辑；而onTransitionEnd、duration、curve与delay为可选参数，分别对应动画结束后的回调、动画持续时间、动画曲线类型与开始前的延时。若在转场代理中返回多个转场协议对象，这些动画效果将逐层叠加。
    2. 通过调用NavDestination组件的customTransition属性，并传入上述实现的转场代理，完成自定义转场的设置。
    
    具体示例代码可以参考[NavDestination自定义转场示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#%E7%A4%BA%E4%BE%8B2%E8%AE%BE%E7%BD%AEnavdestination%E8%87%AA%E5%AE%9A%E4%B9%89%E8%BD%AC%E5%9C%BA)。
    
- 使用建议
    
    1. Navigation自定义转场[customNavContentTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#customnavcontenttransition11)适用于控制Navigation内所有页面，统一转场动画效果。
    2. NavDestination自定义转场[customTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#customtransition15)适用于控制单个页面的转场效果。
    3. 在同时使用[customNavContentTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#customnavcontenttransition11)和[customTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#customtransition15)时，customNavContentTransition优先级更高。

### 共享元素转场

NavDestination之间切换时可以通过[geometryTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-transition-animation-geometrytransition#geometrytransition)实现共享元素转场。配置了共享元素转场的页面同时需要关闭系统默认的转场动画。

1. 为需要实现共享元素转场的组件添加geometryTransition属性，id参数必须在两个NavDestination之间保持一致。
    
    1. // 起始页配置共享元素id
    2. NavDestination() {
    3.   Column() {
    4.     // ...
    5.     // $r('app.media.startIcon')需要替换为开发者所需的资源文件
    6.     Image($r('app.media.startIcon'))
    7.     .geometryTransition('sharedId')
    8.     .width(100)
    9.     .height(100)
    10.   }
    11. }
    12. .title('FromPage')
    
    13. // 目的页配置共享元素id
    14. NavDestination() {
    15.   Column() {
    16.     // ...
    17.     // $r('app.media.startIcon')需要替换为开发者所需的资源文件
    18.     Image($r('app.media.startIcon'))
    19.     .geometryTransition('sharedId')
    20.     .width(200)
    21.     .height(200)
    22.   }
    23. }
    24. .title('ToPage')
    
2. 将页面路由的操作，放到animateTo动画闭包中，配置对应的动画参数以及关闭系统默认的转场。
    
    1. NavDestination() {
    2.   Column() {
    3.     Button('跳转目的页')
    4.     .width('80%')
    5.     .height(40)
    6.     .margin(20)
    7.     .onClick(() => {
    8.         this.getUIContext()?.animateTo({ duration: 1000 }, () => {
    9.           this.pageStack.pushPath({ name: 'ToPage' }, false)
    10.         });
    11.     })
    12.   }
    13. }
    14. .title('FromPage')
    

## 跨包路由

系统提供[系统路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E7%B3%BB%E7%BB%9F%E8%B7%AF%E7%94%B1%E8%A1%A8)和[自定义路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E7%94%B1%E8%A1%A8)两种实现方式。

- 系统路由表相对自定义路由表，使用更简单，只需要添加对应页面跳转配置项，即可实现页面跳转。
    
- 自定义路由表使用起来更复杂，但是可以根据应用业务进行定制处理。
    

支持自定义路由表和系统路由表混用。

### 路由表能力对比

不同路由方式适用于不同需求，易用性或可扩展性需根据项目特点权衡选择。

|路由方式|跨包跳转能力|可扩展性|易用性|
|:--|:--|:--|:--|
|[系统路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E7%B3%BB%E7%BB%9F%E8%B7%AF%E7%94%B1%E8%A1%A8)|跳转前无需import页面文件，页面按需动态加载。|可扩展性一般。|易用性更强，系统自动维护路由表。|
|[自定义路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E7%94%B1%E8%A1%A8)|跳转前需要import页面文件。|可扩展性更强。|易用性一般，需要开发者自行维护路由表。|

### 系统路由表

系统路由表是动态路由的一种实现方式。从API version 12开始，[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)支持使用系统路由表的方式进行动态路由。各业务模块（[HSP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/in-app-hsp)/[HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/har-package)）中需要独立配置route_map.json文件，在触发路由跳转时，应用只需要通过NavPathStack提供的路由方法，传入需要路由的页面配置名称，此时系统会自动完成路由模块的动态加载、页面组件构建，并完成路由跳转，从而实现了开发层面的模块解耦。系统路由表支持模拟器但不支持预览器。其主要步骤如下：

1. 在跳转目标模块的配置文件[module.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)添加路由表配置：
    
    1.   {
    2.     "module" : {
    3.       "routerMap": "$profile:route_map"
    4.     }
    5.   }
    
2. 添加完路由配置文件地址后，需要在工程resources/base/profile中创建route_map.json文件。添加如下配置信息：
    
    1.   {
    2.     "routerMap": [
    3.       {
    4.         "name": "PageOne",
    5.         "pageSourceFile": "src/main/ets/pages/PageOne.ets",
    6.         "buildFunction": "PageOneBuilder",
    7.         "data": {
    8.           "description" : "this is PageOne"
    9.         }
    10.       }
    11.     ]
    12.   }
    
    配置说明如下：
    
    |配置项|说明|
    |:--|:--|
    |name|可自定义的跳转页面名称。|
    |pageSourceFile|跳转目标页在包内的路径，相对src目录的相对路径。|
    |buildFunction|跳转目标页的入口函数名称，必须以@Builder修饰。|
    |data|应用自定义字段。可以通过配置项读取接口getConfigInRouteMap获取。|
    
3. 在跳转目标页面中，需要配置入口Builder函数，函数名称需要和route_map.json配置文件中的buildFunction保持一致，否则在编译时会报错。
    
    1.   // 跳转页面入口函数
    2.   @Builder
    3.   export function PageOneBuilder() {
    4.     PageOne();
    5.   }
    
    6.   @Component
    7.   struct PageOne {
    8.     pathStack: NavPathStack = new NavPathStack();
    
    9.     build() {
    10.       NavDestination() {
    11.       }
    12.       .title('PageOne')
    13.       .onReady((context: NavDestinationContext) => {
    14.          this.pathStack = context.pathStack;
    15.       })
    16.     }
    17.   }
    
4. 通过[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)等路由接口进行页面跳转。(注意：此时Navigation中可以不用配置[navDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)属性。)
    
    1.   @Entry
    2.   @Component
    3.   struct Index {
    4.     pageStack : NavPathStack = new NavPathStack();
    
    5.     build() {
    6.       Navigation(this.pageStack){
    7.       }.onAppear(() => {
    8.         this.pageStack.pushPathByName("PageOne", null, false);
    9.       })
    10.       .hideNavBar(true)
    11.     }
    12.   }
    

### 自定义路由表

自定义路由表通过给Navigation的[navDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)属性设置Builder函数实现，其特点是需要import页面。有两种import页面的方式，静态import和动态import，二者的区别在于：

|import方式|模块间耦合度|实现复杂度|性能|
|:--|:--|:--|:--|
|动态import|模块间解耦。|复杂度高。|性能好，按需加载，跳转前再加载对应页面。|
|静态import|模块间耦合。|复杂度低。|性能一般，初始化时一次性加载所有依赖的页面。|

**动态import（推荐）**

动态import旨在解决多个模块（HAR/HSP）能够复用相同的业务逻辑，实现各业务模块间的解耦，同时支持路由功能的扩展与整合，可以按需import，具体实现方法请参考[Navigation自定义动态路由](https://gitcode.com/harmonyos-cases/cases/blob/master/CommonAppDevelopment/common/routermodule/README_AUTO_GENERATE.md)示例。

动态import的优势：

- 路由定义除了跳转的URL以外，可以配置丰富的扩展信息，如横竖屏默认模式、是否需要鉴权等等，做路由跳转时统一处理。
- 给每个路由页面设置一个名字，按照名称进行跳转而不是文件路径。
- 页面的加载可以使用动态import（按需加载），防止首个页面加载大量代码导致卡顿。

实现方案：

1. 定义页面跳转配置项。
    - 使用资源文件进行定义，通过资源管理[@ohos.resourceManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resource-manager)在运行时对资源文件解析。
    - 在ets文件中配置路由加载配置项，一般包括路由页面名称（即pushPath等接口中页面的别名），文件所在模块名称（hsp/har的模块名），加载页面在模块内的路径（相对src目录的路径）。
2. 加载目标跳转页面，通过[动态import](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-dynamic-import)将跳转目标页面所在的模块在运行时加载，在模块加载完成后，调用模块中的方法，通过import在模块的方法中加载模块中显示的目标页面，并返回页面加载完成后定义的Builder函数。
3. 触发页面跳转，在Navigation的[navDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)属性执行步骤2中加载的Builder函数，即可跳转到目标页面。

**静态import**

静态import实现方式简单，但通过静态import页面进行路由跳转会导致不同模块之间的依赖耦合，并增加首页加载时间长等问题。建议使用[自定义路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E7%94%B1%E8%A1%A8)的动态import或[系统路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E7%B3%BB%E7%BB%9F%E8%B7%AF%E7%94%B1%E8%A1%A8)。

实现方案：

1. import { hilog } from '@kit.PerformanceAnalysisKit';
2. const DOMAIN = 0x0000;
3. @Entry
4. @Component
5. struct NavigationExample {
6.   @Provide('navPathStack') navPathStack: NavPathStack = new NavPathStack();
7.   private arr: number[] = [1, 2];

8.   @Builder
9.   pageMap(name: string) {
10.     if (name === "NavDestinationTitle1") {
11.       pageOneTmp();
12.     } else if (name === "NavDestinationTitle2") {
13.       pageTwoTmp();
14.     }
15.   }

16.   build() {
17.     Column() {
18.       Navigation(this.navPathStack) {
19.         TextInput({ placeholder: 'search...' })
20.           .width("90%")
21.           .height(40)

22.         List({ space: 12 }) {
23.           ForEach(this.arr, (item: number) => {
24.             ListItem() {
25.               Text("Page" + item)
26.                 .width("100%")
27.                 .height(72)
28.                 .borderRadius(24)
29.                 .fontSize(16)
30.                 .fontWeight(500)
31.                 .textAlign(TextAlign.Center)
32.                 .onClick(() => {
33.                   this.navPathStack.pushPath({ name: 'NavDestinationTitle' + item });
34.                 })
35.             }
36.           }, (item: number) => item.toString())
37.         }
38.         .width("90%")
39.         .margin({ top: 12 })
40.       }
41.       // $r('app.string.mainTitle')需要替换为开发者所需的字符串资源文件
42.       .title($r('app.string.mainTitle'))
43.       .navDestination(this.pageMap)
44.       .mode(NavigationMode.Split)
45.     }
46.     .height('100%')
47.     .width('100%')
48.   }
49. }

50. @Component
51. export struct pageTwoTmp {
52.   @Consume('navPathStack') navPathStack: NavPathStack;
53.   context = this.getUIContext().getHostContext();
54.   build() {
55.     NavDestination() {
56.       Column() {
57.         Text("NavDestinationContent2")
58.       }.width('100%').height('100%')
59.     }.title("NavDestinationTitle2")
60.     .onBackPressed(() => {
61.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈的栈顶元素
62.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
63.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
64.         JSON.stringify(popDestinationInfo));
65.       return true;
66.     })
67.   }
68. }

69. // pageOne.ets
70. @Component
71. export struct pageOneTmp {
72.   @Consume('navPathStack') navPathStack: NavPathStack;
73.   context = this.getUIContext().getHostContext();
74.   build() {
75.     NavDestination() {
76.       Column() {
77.         Text("NavDestinationContent1")
78.       }.width('100%').height('100%')
79.     }.title("NavDestinationTitle1")
80.     .onBackPressed(() => {
81.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈的栈顶元素
82.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
83.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
84.         JSON.stringify(popDestinationInfo));
85.       return true;
86.     })
87.   }
88. }

## 导航示例

### 创建导航首页

实现步骤为：

1.使用[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)创建导航主页，并创建导航控制器NavPathStack以此来实现不同页面之间的跳转。

2.在Navigation中增加[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-list)组件，来定义导航主页中不同的一级界面。

3.在List内的组件添加onClick方法，并在其中使用导航控制器NavPathStack的[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)方法，使组件可以在点击之后从当前页面跳转到输入参数name在路由表内对应的页面。

1. @Entry
2. @Component
3. struct NavigationDemo {
4.   @Provide('navPathStack') navPathStack: NavPathStack = new NavPathStack();
5.   private listArray: Array<string> = ['WLAN', 'Bluetooth', 'Personal Hotspot', 'Connect & Share'];

6.   build() {
7.     Column() {
8.       Navigation(this.navPathStack) {
9.         TextInput({ placeholder: '输入关键字搜索' })
10.           .width('90%')
11.           .height(40)
12.           .margin({ bottom: 10 })

13.         // 通过List定义导航的一级界面
14.         List({ space: 12, initialIndex: 0 }) {
15.           ForEach(this.listArray, (item: string) => {
16.             ListItem() {
17.               Row() {
18.                 Row() {
19.                   Text(`${item.slice(0, 1)}`)
20.                     .fontColor(Color.White)
21.                     .fontSize(14)
22.                     .fontWeight(FontWeight.Bold)
23.                 }
24.                 .width(30)
25.                 .height(30)
26.                 .backgroundColor('#a8a8a8')
27.                 .margin({ right: 20 })
28.                 .borderRadius(20)
29.                 .justifyContent(FlexAlign.Center)

30.                 Column() {
31.                   Text(item)
32.                     .fontSize(16)
33.                     .margin({ bottom: 5 })
34.                 }
35.                 .alignItems(HorizontalAlign.Start)

36.                 Blank()

37.                 Row()
38.                   .width(12)
39.                   .height(12)
40.                   .margin({ right: 15 })
41.                   .border({
42.                     width: { top: 2, right: 2 },
43.                     color: 0xcccccc
44.                   })
45.                   .rotate({ angle: 45 })
46.               }
47.               .borderRadius(15)
48.               .shadow({ radius: 100, color: '#ededed' })
49.               .width('90%')
50.               .alignItems(VerticalAlign.Center)
51.               .padding({ left: 15, top: 15, bottom: 15 })
52.               .backgroundColor(Color.White)
53.             }
54.             .width('100%')
55.             .onClick(() => {
56.               this.navPathStack.pushPathByName(`${item}`, '详情页面参数'); // 将name指定的NaviDestination页面信息入栈,传递的参数为param
57.             })
58.           }, (item: string): string => item)
59.         }
60.         .listDirection(Axis.Vertical)
61.         .edgeEffect(EdgeEffect.Spring)
62.         .sticky(StickyStyle.Header)
63.         .chainAnimation(false)
64.         .width('100%')
65.       }
66.       .width('100%')
67.       .mode(NavigationMode.Auto)
68.       .title('设置') // 设置标题文字
69.     }
70.     .size({ width: '100%', height: '100%' })
71.     .backgroundColor(0xf4f4f5)
72.   }
73. }

### 创建导航子页

导航子页1实现步骤为：

1.使用[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)，来创建导航子页PageOne。

2.创建导航控制器[NavPathStack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)并在[onReady](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onready11)时进行初始化，获取当前所在的导航控制器，以此来实现不同页面之间的跳转。

3.在子页面内的组件添加onClick，并在其中使用导航控制器NavPathStack的[pop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pop10)方法，使组件可以在点击之后弹出路由栈栈顶元素实现页面的返回。

1. //PageOne.ets
2. @Builder
3. export function PageOneBuilder(name: string, param: string) {
4.   PageOne({ name: name, value: param });
5. }

6. @Component
7. export struct PageOne {
8.   navPathStack: NavPathStack = new NavPathStack();
9.   name: string = '';
10.   @State value: string = '';

11.   build() {
12.     NavDestination() {
13.       Column() {
14.         Text(`${this.name}设置页面`)
15.           .width('100%')
16.           .fontSize(20)
17.           .fontColor(0x333333)
18.           .textAlign(TextAlign.Center)
19.           .textShadow({
20.             radius: 2,
21.             offsetX: 4,
22.             offsetY: 4,
23.             color: 0x909399
24.           })
25.           .padding({ top: 30 })
26.         Text(`${JSON.stringify(this.value)}`)
27.           .width('100%')
28.           .fontSize(18)
29.           .fontColor(0x666666)
30.           .textAlign(TextAlign.Center)
31.           .padding({ top: 45 })
32.         Button('返回')
33.           .width('50%')
34.           .height(40)
35.           .margin({ top: 50 })
36.           .onClick(() => {
37.             //弹出路由栈栈顶元素，返回上个页面
38.             this.navPathStack.pop();
39.           })
40.       }
41.       .size({ width: '100%', height: '100%' })
42.     }.title(`${this.name}`)
43.     .onReady((ctx: NavDestinationContext) => {
44.       // NavDestinationContext获取当前所在的导航控制器
45.       this.navPathStack = ctx.pathStack;
46.     })
47.   }
48. }

导航子页2实现步骤为：

1.使用NavDestination，来创建导航子页PageTwo。

2.创建导航控制器NavPathStack并在onReady时进行初始化，获取当前所在的导航控制器，以此来实现不同页面之间的跳转。

3.在子页面内的组件添加onClick，并在其中使用导航控制器NavPathStack的[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)方法，使组件可以在点击之后从当前页面跳转到输入参数name在路由表内对应的页面。

1. //PageTwo.ets
2. @Builder
3. export function PageTwoBuilder(name: string) {
4.   PageTwo({ name: name });
5. }

6. @Component
7. export struct PageTwo {
8.   navPathStack: NavPathStack = new NavPathStack();
9.   name: string = '';
10.   private listArray: Array<string> = ['Projection', 'Print', 'VPN', 'Private DNS', 'NFC'];

11.   build() {
12.     NavDestination() {
13.       Column() {
14.         List({ space: 12, initialIndex: 0 }) {
15.           ForEach(this.listArray, (item: string) => {
16.             ListItem() {
17.               Row() {
18.                 Row() {
19.                   Text(`${item.slice(0, 1)}`)
20.                     .fontColor(Color.White)
21.                     .fontSize(14)
22.                     .fontWeight(FontWeight.Bold)
23.                 }
24.                 .width(30)
25.                 .height(30)
26.                 .backgroundColor('#a8a8a8')
27.                 .margin({ right: 20 })
28.                 .borderRadius(20)
29.                 .justifyContent(FlexAlign.Center)

30.                 Column() {
31.                   Text(item)
32.                     .fontSize(16)
33.                     .margin({ bottom: 5 })
34.                 }
35.                 .alignItems(HorizontalAlign.Start)

36.                 Blank()

37.                 Row()
38.                   .width(12)
39.                   .height(12)
40.                   .margin({ right: 15 })
41.                   .border({
42.                     width: { top: 2, right: 2 },
43.                     color: 0xcccccc
44.                   })
45.                   .rotate({ angle: 45 })
46.               }
47.               .borderRadius(15)
48.               .shadow({ radius: 100, color: '#ededed' })
49.               .width('90%')
50.               .alignItems(VerticalAlign.Center)
51.               .padding({ left: 15, top: 15, bottom: 15 })
52.               .backgroundColor(Color.White)
53.             }
54.             .width('100%')
55.             .onClick(() => {
56.               this.navPathStack.pushPathByName(`${item}`, '页面设置参数');
57.             })
58.           }, (item: string): string => item)
59.         }
60.         .listDirection(Axis.Vertical)
61.         .edgeEffect(EdgeEffect.Spring)
62.         .sticky(StickyStyle.Header)
63.         .width('100%')
64.       }
65.       .size({ width: '100%', height: '100%' })
66.     }.title(`${this.name}`)
67.     .onReady((ctx: NavDestinationContext) => {
68.       // NavDestinationContext获取当前所在的导航控制器
69.       this.navPathStack = ctx.pathStack;
70.     })
71.   }
72. }

### 创建路由跳转

实现步骤为：

1.工程配置文件[module.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中配置 {"routerMap": "$profile:router_map"}。

2.router_map.json中配置全局路由表，导航控制器NavPathStack可根据路由表中的name将对应页面信息入栈。

1. {
2.   "routerMap" : [
3.     {
4.       "name" : "WLAN",
5.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
6.       "buildFunction" : "PageOneBuilder"
7.     },
8.     {
9.       "name" : "Bluetooth",
10.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
11.       "buildFunction" : "PageOneBuilder"
12.     },
13.     {
14.       "name" : "Personal Hotspot",
15.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
16.       "buildFunction" : "PageOneBuilder"
17.     },
18.     {
19.       "name" : "Connect & Share",
20.       "pageSourceFile"  : "src/main/ets/pages/PageTwo.ets",
21.       "buildFunction" : "PageTwoBuilder"
22.     },
23.     {
24.       "name" : "Projection",
25.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
26.       "buildFunction" : "PageOneBuilder"
27.     },
28.     {
29.       "name" : "Print",
30.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
31.       "buildFunction" : "PageOneBuilder"
32.     },
33.     {
34.       "name" : "VPN",
35.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
36.       "buildFunction" : "PageOneBuilder"
37.     },
38.     {
39.       "name" : "Private DNS",
40.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
41.       "buildFunction" : "PageOneBuilder"
42.     },
43.     {
44.       "name" : "NFC",
45.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
46.       "buildFunction" : "PageOneBuilder"
47.     }
48.   ]
49. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.30221763759141194730167703387201:50001231000000:2800:EB5B03A9F555626B4E13396CEDB9352183B61BA8917A1A339930A3837013D609.gif)

## 示例代码

- [Navigation系统路由](https://gitcode.com/harmonyos_samples/system-router-map)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-introduction "组件导航和页面路由概述")
# 组件导航(Navigation) (推荐)

更新时间: 2025-12-16 16:39

组件导航（[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)）主要用于实现Navigation页面（[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)）间的跳转，支持在不同Navigation页面间传递参数，提供灵活的跳转栈操作，从而更便捷地实现对不同页面的访问和复用。本文将从组件导航（Navigation）的显示模式、路由操作、子页面管理、跨包跳转以及跳转动效等几个方面进行详细介绍。

[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)是路由导航的根视图容器，一般作为页面（@Entry）的根容器，包括单栏（Stack）、分栏（Split）和自适应（Auto）三种显示模式。Navigation组件适用于模块内和跨模块的路由切换，通过组件级路由能力实现更加自然流畅的转场体验，并提供多种标题栏样式来呈现更好的标题和内容联动效果。一次开发，多端部署场景下，Navigation组件能够自动适配窗口显示大小，在窗口较大的场景下自动切换分栏展示效果。

Navigation组件主要包含​导航页和子页。导航页由标题栏（包含菜单栏）、内容区和工具栏组成，可以通过[hideNavBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#hidenavbar9)属性进行隐藏，导航页不存在[路由栈](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)中，与子页，以及子页之间可以通过路由操作进行切换。

在API version 9上，Navigation需要配合[NavRouter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navrouter)组件实现页面路由。从API version 10开始，更推荐使用[NavPathStack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)实现页面路由。

## 设置页面显示模式

[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)组件通过[mode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#mode9)属性设置页面的显示模式。

- 自适应模式
    
    Navigation组件默认为自适应模式，此时mode属性为NavigationMode.Auto。自适应模式下，当页面宽度大于等于一定阈值( API version 9及以前：520vp，API version 10及以后：600vp )时，Navigation组件采用分栏模式，反之采用单栏模式。
    
    收起
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .mode(NavigationMode.Auto)
    
- 单栏模式
    
    单栏模式适用于窄屏设备，发生路由跳转时，整个页面都会被替换。
    
    **图1** 单栏布局示意图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163913.39247956913604846372315161784606:50001231000000:2800:925B5823D0F65790083C974E6538E7DE423A4CD226690DE88CA88D854F7E3F88.png)
    
    将mode属性设置为NavigationMode.Stack，Navigation组件即可设置为单栏显示模式。
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .mode(NavigationMode.Stack)
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163913.94781536402667387449603288907682:50001231000000:2800:5E623CF9E47772521FAF0D79441B418D1FBF0ED5B16BADE1E1FC081CCAEFACA4.jpg)
    
- 分栏模式
    
    分栏模式适用于宽屏设备，分为左右两部分，发生路由跳转时，只有右边子页会被替换。
    
    **图2** 分栏布局示意图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163913.44635127908442444956882181138608:50001231000000:2800:29D142503D371ED20B0604DA5CCCBD05F9767952FCC5D5CE19B49743361AF01D.png)
    
    将mode属性设置为NavigationMode.Split，Navigation组件即可设置为分栏显示模式。
    
    1. import { hilog } from '@kit.PerformanceAnalysisKit';
    2. const DOMAIN = 0x0000;
    3. @Entry
    4. @Component
    5. struct NavigationExample {
    6.   @State toolTmp: ToolbarItem = {
    7.     'value': "func",
    8.     'icon': "./image/ic_public_highlights.svg",  // 当前目录image文件夹下的图标资源
    9.     'action': () => {}
    10.   };
    11.   @Provide('navPathStack') navPathStack: NavPathStack = new NavPathStack();
    12.   private arr: number[] = [1, 2, 3];
    
    13.   @Builder
    14.   pageMap(name: string) {
    15.     if (name === "NavDestinationTitle1") {
    16.       pageOneTmp();
    17.     } else if (name === "NavDestinationTitle2") {
    18.       pageTwoTmp();
    19.     } else if (name === "NavDestinationTitle3") {
    20.       pageThreeTmp();
    21.     }
    22.   }
    
    23.   build() {
    24.     Column() {
    25.       Navigation(this.navPathStack) {
    26.         TextInput({ placeholder: 'search...' })
    27.           .width("90%")
    28.           .height(40)
    29.           .backgroundColor('#FFFFFF')
    
    30.         List({ space: 12 }) {
    31.           ForEach(this.arr, (item: number) => {
    32.             ListItem() {
    33.               Text("Page" + item)
    34.                 .width("100%")
    35.                 .height(72)
    36.                 .backgroundColor('#FFFFFF')
    37.                 .borderRadius(24)
    38.                 .fontSize(16)
    39.                 .fontWeight(500)
    40.                 .textAlign(TextAlign.Center)
    41.                 .onClick(() => {
    42.                   this.navPathStack.pushPath({ name: 'NavDestinationTitle' + item });
    43.                 })
    44.             }
    45.           }, (item: number) => item.toString())
    46.         }
    47.         .width("90%")
    48.         .margin({ top: 12 })
    49.       }
    50.       .title("主标题")
    51.       .mode(NavigationMode.Split)
    52.       .navDestination(this.pageMap)
    53.       .menus([
    54.         {
    55.           value: "", icon: "./image/ic_public_search.svg", action: () => {
    56.           }
    57.         },
    58.         {
    59.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    60.           }
    61.         },
    62.         {
    63.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    64.           }
    65.         },
    66.         {
    67.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    68.           }
    69.         },
    70.         {
    71.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    72.           }
    73.         }
    74.       ])
    75.       .toolbarConfiguration([this.toolTmp, this.toolTmp, this.toolTmp])
    76.     }
    77.     .height('100%')
    78.     .width('100%')
    79.     .backgroundColor('#F1F3F5')
    80.   }
    81. }
    
    82. // PageOne.ets
    83. @Component
    84. export struct pageOneTmp {
    85.   @Consume('navPathStack') navPathStack: NavPathStack;
    86.   context = this.getUIContext().getHostContext();
    87.   build() {
    88.     NavDestination() {
    89.       Column() {
    90.         Text("NavDestinationContent1")
    91.       }.width('100%').height('100%')
    92.     }.title("NavDestinationTitle1")
    93.     .onBackPressed(() => {
    94.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈栈顶元素
    95.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
    96.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
    97.         JSON.stringify(popDestinationInfo));
    98.       return true;
    99.     })
    100.   }
    101. }
    
    102. // PageTwo.ets
    103. @Component
    104. export struct pageTwoTmp {
    105.   @Consume('navPathStack') navPathStack: NavPathStack;
    106.   context = this.getUIContext().getHostContext();
    107.   build() {
    108.     NavDestination() {
    109.       Column() {
    110.         Text("NavDestinationContent2")
    111.       }.width('100%').height('100%')
    112.     }.title("NavDestinationTitle2")
    113.     .onBackPressed(() => {
    114.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈栈顶元素
    115.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
    116.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
    117.         JSON.stringify(popDestinationInfo));
    118.       return true;
    119.     })
    120.   }
    121. }
    
    122. // PageThree.ets
    123. @Component
    124. export struct pageThreeTmp {
    125.   @Consume('navPathStack') navPathStack: NavPathStack;
    126.   context = this.getUIContext().getHostContext();
    127.   build() {
    128.     NavDestination() {
    129.       Column() {
    130.         Text("NavDestinationContent3")
    131.       }.width('100%').height('100%')
    132.     }.title("NavDestinationTitle3")
    133.     .onBackPressed(() => {
    134.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈栈顶元素
    135.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
    136.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
    137.         JSON.stringify(popDestinationInfo));
    138.       return true;
    139.     })
    140.   }
    141. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.38522712307407973042152555339603:50001231000000:2800:210862FB40488CA357496A333F8C814C3375FF85E9C6EC2074FEB76A3517DB98.jpg)
    

## 设置标题栏模式

标题栏在界面顶部，用于呈现界面名称和操作入口，Navigation组件通过[titleMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#titlemode)属性设置标题栏模式。

说明

Navigation或NavDestination未设置主副标题并且没有返回键时，不显示标题栏。

- Mini模式
    
    普通型标题栏，用于一级页面不需要突出标题的场景。
    
    **图3** Mini模式标题栏
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.88917640640829362862283509704068:50001231000000:2800:A6899C99862B2B677DC35E58E135729F02D8AFC91611D3785F415702713E36CA.jpg)
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .titleMode(NavigationTitleMode.Mini)
    
- Full模式
    
    强调型标题栏，用于一级页面需要突出标题的场景。
    
    **图4** Full模式标题栏
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.76716253096362819389528325214830:50001231000000:2800:4F8C50DC6DC180EEDFCCD3B4029968E2FF19618370ED06D5B688BD572BCFB1EA.jpg)
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .titleMode(NavigationTitleMode.Full)
    

## 设置菜单栏

菜单栏位于Navigation组件的右上角，开发者可以通过[menus](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#menus)属性进行设置。menus支持Array<[NavigationMenuItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navigationmenuitem)>和[CustomBuilder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-types#custombuilder8)两种参数类型。使用Array<NavigationMenuItem>类型时，竖屏最多支持显示3个图标，横屏最多支持显示5个图标，多余的图标会被放入自动生成的更多图标。

**图5** 设置了3个图标的菜单栏

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.73673441631946749215245150548418:50001231000000:2800:807E87EF7E5ADFFA9A9A846ED20101AC4AB9A0643F48CF41A0150795BC65B0DD.jpg)

1. let toolTmp: NavigationMenuItem  = {
2.   'value': 'func',
3.   'icon': 'ets/pages/navigation/template1/image/ic_public_add.svg',
4.   'action': () => {}
5. };
6. // ...
7.       Navigation(this.navPathStack) {
8.         // ...
9.       }
10.       .menus([toolTmp, toolTmp, toolTmp])

图片也可以引用resources中的资源。

1. let toolTmp: NavigationMenuItem  = {
2.   'value': 'func',
3.   'icon': 'resources/base/media/ic_public_add.svg',
4.   'action': () => {}
5. };
6. // ...
7.       Navigation(this.navPathStack) {
8.         // ...
9.       }
10.       .menus([toolTmp, toolTmp, toolTmp])

**图6** 设置了4个图标的菜单栏

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.50787801697064920089908207920699:50001231000000:2800:E62E892050408B63ACDFEA78F71C670DAD4153B291E146916FEB0AD290D16B77.jpg)

1. let toolTmp: NavigationMenuItem  = {
2.   'value': 'func',
3.   'icon': 'ets/pages/navigation/template1/image/ic_public_add.svg',
4.   'action': () => {}
5. };
6. // ...
7.       Navigation(this.navPathStack) {
8.         // ...
9.       }
10.       // 竖屏最多支持显示3个图标，多余的图标会被放入自动生成的更多图标
11.       .menus([toolTmp, toolTmp, toolTmp, toolTmp])

## 设置工具栏

工具栏位于Navigation组件的底部，开发者可以通过[toolbarConfiguration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#toolbarconfiguration10)属性进行设置。

**图7** 工具栏

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.17051218093016793180970087149026:50001231000000:2800:99FD7107F1BDE63C8614828B7CB573E786230469AEF4242386295E47BECFC7B5.jpg)

1. let toolTmp: ToolbarItem = {
2.   'value': 'func',
3.   'icon': 'ets/pages/navigation/template1/image/ic_public_highlights.svg',
4.   'action': () => {}
5. };
6. let tooBar: ToolbarItem[] = [toolTmp,toolTmp,toolTmp];
7. // ...
8.       Navigation(this.navPathStack) {
9.         // ...
10.       }
11.       .toolbarConfiguration(tooBar)

## 路由操作

Navigation路由相关的操作都是基于导航控制器[NavPathStack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)提供的方法进行，每个Navigation都需要创建并传入一个NavPathStack对象，用于管理页面。主要涉及页面跳转、页面返回、页面替换、页面删除、参数获取、路由拦截等功能。

从API version 12开始，导航控制器允许被继承。开发者可以在派生类中自定义属性和方法，也可以重写父类的方法。派生类对象可以替代基类NavPathStack对象使用。Navigation中的[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)页面存在于NavPathStack中，以栈的结构管理，我们称为路由栈。具体示例代码参见：[导航控制器继承示例代码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#%E7%A4%BA%E4%BE%8B10%E5%AE%9A%E4%B9%89%E5%AF%BC%E8%88%AA%E6%8E%A7%E5%88%B6%E5%99%A8%E6%B4%BE%E7%94%9F%E7%B1%BB)。

说明

1.不建议开发者通过监听生命周期的方式管理自己的路由栈。

2.在应用处于后台状态下，调用NavPathStack的栈操作方法，会在应用再次回到前台状态时触发刷新。

1. @Entry
2. @Component
3. struct Index {
4.   // 创建一个导航控制器对象并传入Navigation
5.   pageStack: NavPathStack = new NavPathStack();

6.   build() {
7.     Navigation(this.pageStack) {
8.     }
9.     .title('Main')
10.   }
11. }

### 页面跳转

NavPathStack通过Push相关的接口（如[pushPath](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpath10)、[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)、[pushDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushdestination11)、[pushDestinationByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushdestinationbyname11)）去实现页面跳转的功能，主要分为以下三类：

1. 普通跳转，通过页面的name去跳转，并可以携带param。
    
    1. this.pageStack.pushPath({ name: "PageOne", param: "PageOne Param" });
    2. this.pageStack.pushPathByName("PageOne", "PageOne Param");
    
2. 带返回回调的跳转，跳转时添加onPop回调，能在页面出栈时获取返回信息，并进行处理。
    
    1. this.pageStack.pushPathByName('PageOne', "PageOne Param", (popInfo) => {
    2.   console.info('Pop page name is: ' + popInfo.info.name + ', result: ' + JSON.stringify(popInfo.result));
    3. });
    
3. 带错误码的跳转，跳转结束会触发异步回调，返回错误码信息。
    
    1. this.pageStack.pushDestination({name: "PageOne", param: "PageOne Param"})
    2.   .catch((error: BusinessError) => {
    3.     console.error(`Push destination failed, error code = ${error.code}, error.message = ${error.message}.`);
    4.   }).then(() => {
    5.     console.info('Push destination succeed.');
    6.   });
    7. this.pageStack.pushDestinationByName("PageOne", "PageOne Param")
    8.   .catch((error: BusinessError) => {
    9.     console.error(`Push destination failed, error code = ${error.code}, error.message = ${error.message}.`);
    10.   }).then(() => {
    11.     console.info('Push destination succeed.');
    12.   });
    

### 页面返回

NavPathStack通过pop相关接口（如[pop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pop10)、[popToName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#poptoname10)、[popToIndex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#poptoindex10)、[clear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#clear10)）去实现页面返回功能。

1. // 返回到上一页
2. this.pageStack.pop();
3. // 返回到上一个PageOne页面
4. this.pageStack.popToName("PageOne");
5. // 返回到索引为1的页面
6. this.pageStack.popToIndex(1);
7. // 返回到根首页（清除栈中所有页面）
8. this.pageStack.clear();

### 页面替换

NavPathStack通过Replace相关接口（如[replacePath](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#replacepath11)、[replacePathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#replacepathbyname11)、[replaceDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#replacedestination18)）去实现页面替换功能。

1. // 将栈顶页面替换为PageOne
2. this.pageStack.replacePath({ name: "PageOne", param: "PageOne Param" });
3. this.pageStack.replacePathByName("PageOne", "PageOne Param");
4. // 带错误码的替换，跳转结束会触发异步回调，返回错误码信息
5. this.pageStack.replaceDestination({name: "PageOne", param: "PageOne Param"})
6.   .catch((error: BusinessError) => {
7.     console.error(`Replace destination failed, error code = ${error.code}, error.message = ${error.message}.`);
8.   }).then(() => {
9.     console.info('Replace destination succeed.');
10.   })

### 页面删除

NavPathStack通过Remove相关接口（如[removeByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#removebyname11)、[removeByIndexes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#removebyindexes11)、[removeByNavDestinationId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#removebynavdestinationid12)）去实现删除路由栈中特定页面的功能。

1. // 删除栈中name为PageOne的所有页面
2. this.pageStack.removeByName("PageOne");
3. // 删除指定索引的页面
4. this.pageStack.removeByIndexes([1, 3, 5]);
5. // 删除指定id的页面
6. this.pageStack.removeByNavDestinationId("1");

### 移动页面

NavPathStack通过Move相关接口（如[moveToTop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#movetotop10)、[moveIndexToTop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#moveindextotop10)）去实现移动路由栈中特定页面到栈顶的功能。

1. // 移动栈中name为PageOne的页面到栈顶
2. this.pageStack.moveToTop("PageOne");
3. // 移动栈中索引为1的页面到栈顶
4. this.pageStack.moveIndexToTop(1);

### 参数获取

[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)子页第一次创建时会触发[onReady](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onready11)回调，可以获取此页面对应的参数。

1. @Component
2. struct Page01 {
3.   pathStack: NavPathStack | undefined = undefined;
4.   pageParam: string = '';

5.   build() {
6.     NavDestination() {
7.       // ...
8.     }.title('Page01')
9.     .onReady((context: NavDestinationContext) => {
10.       this.pathStack = context.pathStack;
11.       this.pageParam = context.pathInfo.param as string;
12.     })
13.   }
14. }

NavDestination组件中可以通过设置[onResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onresult15)接口，接收返回时传递的路由参数。

1. class NavParam {
2.   desc: string = 'navigation-param'
3. }

4. @Component
5. struct DemoNavDestination {
6.   // ...
7.   build() {
8.     NavDestination() {
9.       // ...
10.     }
11.     .onResult((param: Object) => {
12.       if (param instanceof NavParam) {
13.         console.info('TestTag', 'get NavParam, its desc: ' + (param as NavParam).desc);
14.         return;
15.       }
16.       console.info('TestTag', 'param not instance of NavParam');
17.     })
18.   }
19. }

其他业务场景，可以通过主动调用NavPathStack的Get相关接口（如[getAllPathName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getallpathname10)、[getParamByIndex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getparambyindex10)、[getParamByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getparambyname10)、[getIndexByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getindexbyname10)）去获取指定页面的参数。

1. // 获取栈中所有页面name集合
2. this.pageStack.getAllPathName();
3. // 获取索引为1的页面参数
4. this.pageStack.getParamByIndex(1);
5. // 获取PageOne页面的参数
6. this.pageStack.getParamByName("PageOne");
7. // 获取PageOne页面的索引集合
8. this.pageStack.getIndexByName("PageOne");

### 路由拦截

NavPathStack提供了[setInterception](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#setinterception12)方法，用于设置Navigation页面跳转拦截回调。该方法需要传入一个[NavigationInterception](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navigationinterception12)对象，该对象包含三个回调函数：

|名称|描述|
|:--|:--|
|willShow|页面跳转前回调，允许操作栈，在当前跳转生效。|
|didShow|页面跳转后回调，在该回调中操作栈会在下一次跳转生效。|
|modeChange|Navigation单双栏显示状态发生变更时触发该回调。|

说明

无论是哪个回调，在进入回调时路由栈都已经发生了变化。

开发者可以在willShow回调中通过修改路由栈来实现路由拦截重定向的能力。

1. this.pageStack.setInterception({
2.   willShow: (from: NavDestinationContext | "navBar", to: NavDestinationContext | "navBar",
3.     operation: NavigationOperation, animated: boolean) => {
4.     if (typeof to === "string") {
5.       console.info("target page is navigation home page.");
6.       return;
7.     }
8.     // 将跳转到PageTwo的路由重定向到PageOne
9.     let target: NavDestinationContext = to as NavDestinationContext;
10.     if (target.pathInfo.name === 'PageTwo') {
11.       target.pathStack.pop();
12.       target.pathStack.pushPathByName('PageOne', null);
13.     }
14.   }
15. })

### 单例跳转

通过设置[LaunchMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#launchmode12%E6%9E%9A%E4%B8%BE%E8%AF%B4%E6%98%8E)为LaunchMode.MOVE_TO_TOP_SINGLETON或LaunchMode.POP_TO_SINGLETON，可以实现Navigation路由栈的单实例跳转。单实例跳转的规则如下：

1. 当指定为LaunchMode.MOVE_TO_TOP_SINGLETON时，系统会从栈底到栈顶查找具有指定名称的NavDestination。找到后，该页面将被移动到栈顶（replace操作会用指定的NavDestination替换当前栈顶）。
2. 若指定为LaunchMode.POP_TO_SINGLETON，系统同样会从栈底到栈顶查找具有指定名称的NavDestination。找到后，便会移除该NavDestination上方的所有页面（replace操作会用指定的NavDestination替换当前栈顶）。

当栈中存在的NavDestination页面通过单实例方式移动到栈顶时，将触发[onNewParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onnewparam19)回调。

有关单实例跳转的示例代码，可以参考[Navigation单例跳转示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#%E7%A4%BA%E4%BE%8B2%E4%BD%BF%E7%94%A8%E5%AF%BC%E8%88%AA%E6%8E%A7%E5%88%B6%E5%99%A8%E6%96%B9%E6%B3%95)。

## 子页面

[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)是[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)子页面的根容器，用于承载子页面的一些特殊属性以及生命周期等。NavDestination可以设置独立的标题栏和菜单栏等属性，使用方法与Navigation相同。NavDestination也可以通过[mode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#mode11)属性设置不同的显示类型，用于满足不同页面的诉求。

### 页面显示类型

- 标准类型
    
    NavDestination组件默认为标准类型，此时mode属性为NavDestinationMode.STANDARD。标准类型的NavDestination的生命周期跟随其在NavPathStack路由栈中的位置变化而改变。
    
- 弹窗类型
    
    NavDestination设置mode为NavDestinationMode.DIALOG弹窗类型，此时整个NavDestination默认透明显示。弹窗类型的NavDestination显示和消失时不会影响下层标准类型的NavDestination的显示和生命周期，两者可以同时显示。
    
    1. // Dialog NavDestination
    2. @Entry
    3. @Component
    4.  struct Index {
    5.    @Provide('NavPathStack') pageStack: NavPathStack = new NavPathStack();
    
    6.    @Builder
    7.    PagesMap(name: string) {
    8.      if (name == 'DialogPage') {
    9.        DialogPage();
    10.      }
    11.    }
    
    12.    build() {
    13.      Navigation(this.pageStack) {
    14.        Button('Push DialogPage')
    15.          .margin(20)
    16.          .width('80%')
    17.          .onClick(() => {
    18.            this.pageStack.pushPathByName('DialogPage', '');
    19.          })
    20.      }
    21.      .mode(NavigationMode.Stack)
    22.      .title('Main')
    23.      .navDestination(this.PagesMap)
    24.    }
    25.  }
    
    26.  @Component
    27.  export struct DialogPage {
    28.    @Consume('NavPathStack') pageStack: NavPathStack;
    
    29.    build() {
    30.      NavDestination() {
    31.        Stack({ alignContent: Alignment.Center }) {
    32.          Column() {
    33.            Text("Dialog NavDestination")
    34.              .fontSize(20)
    35.              .margin({ bottom: 100 })
    36.            Button("Close").onClick(() => {
    37.              this.pageStack.pop();
    38.            }).width('30%')
    39.          }
    40.          .justifyContent(FlexAlign.Center)
    41.          .backgroundColor(Color.White)
    42.          .borderRadius(10)
    43.          .height('30%')
    44.          .width('80%')
    45.        }.height("100%").width('100%')
    46.      }
    47.      .backgroundColor('rgba(0,0,0,0.5)')
    48.      .hideTitleBar(true)
    49.      .mode(NavDestinationMode.DIALOG)
    50.    }
    51.  }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.54044996889160545821333494615153:50001231000000:2800:1C6F64946E20589F1ADDBC055027E949D521EFD4BDC226343350F6401D3A6E86.png)
    

### 页面生命周期

Navigation作为路由容器，其生命周期承载在NavDestination组件上，以组件事件的形式开放。

其生命周期大致可分为三类，自定义组件生命周期、通用组件生命周期和自有生命周期。其中，[aboutToAppear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttoappear)和[aboutToDisappear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttodisappear)是自定义组件的生命周期(NavDestination外层包含的自定义组件)，[OnAppear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-events-show-hide#onappear)和[OnDisappear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-events-show-hide#ondisappear)是组件的通用生命周期。剩下的生命周期为NavDestination独有。

生命周期时序如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.71014053475673058396905454101583:50001231000000:2800:2E7A765B6F0E13E37F64EA39C86F41B0C6FD73A0946A0B1D7B98F3744C840BB3.png)

- **aboutToAppear**：在创建自定义组件后，执行其build()函数之前执行（NavDestination创建之前），允许在该方法中改变状态变量，更改将在后续执行build()函数中生效。
- **onWillAppear**：NavDestination创建后，挂载到组件树之前执行，在该方法中更改状态变量会在当前帧显示生效。
- **onAppear**：通用生命周期事件，NavDestination组件挂载到组件树时执行。
- **onWillShow**：NavDestination组件布局显示之前执行，此时页面不可见（应用切换到前台不会触发）。
- **onShown**：NavDestination组件布局显示之后执行，此时页面已完成布局。
- **onActive**：NavDestination处于激活态（处于栈顶可操作，且上层无特殊组件遮挡）触发。
- **onWillHide**：NavDestination组件触发隐藏之前执行（应用切换到后台不会触发）。
- **onInactive**：NavDestination组件处于非激活态（处于非栈顶不可操作，或处于栈顶时上层有特殊组件遮挡）触发。
- **onHidden**：NavDestination组件触发隐藏后执行（非栈顶页面push进栈，栈顶页面pop出栈或应用切换到后台）。
- **onWillDisappear**：NavDestination组件即将销毁之前执行，如果有转场动画，会在动画前触发（栈顶页面pop出栈）。
- **onDisappear**：通用生命周期事件，NavDestination组件从组件树上卸载销毁时执行。
- **aboutToDisappear**：自定义组件析构销毁之前执行，不允许在该方法中改变状态变量。

### 页面监听和查询

为了方便组件跟页面解耦，在NavDestination子页面内部的自定义组件可以通过全局方法监听或查询到页面的一些状态信息。

- 页面信息查询
    
    自定义组件提供[queryNavDestinationInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-api#querynavdestinationinfo)方法，可以在NavDestination内部查询到当前所属页面的信息，返回值为[NavDestinationInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-observer#navdestinationinfo)，若查询不到则返回undefined。
    
    1.  import { uiObserver } from '@kit.ArkUI';
    
    2.  // NavDestination内的自定义组件
    3.  @Component
    4.  struct MyComponent {
    5.    navDesInfo: uiObserver.NavDestinationInfo | undefined;
    
    6.    aboutToAppear(): void {
    7.      this.navDesInfo = this.queryNavDestinationInfo();
    8.    }
    
    9.    build() {
    10.        Column() {
    11.          Text("所属页面Name: " + this.navDesInfo?.name)
    12.        }.width('100%').height('100%')
    13.    }
    14.  }
    
- 页面状态监听
    
    通过[observer.on('navDestinationUpdate')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-observer#uiobserveronnavdestinationupdate)提供的注册接口可以注册NavDestination生命周期变化的监听，使用方式如下：
    
    1. uiObserver.on('navDestinationUpdate', (info) => {
    2.      console.info('NavDestination state update', JSON.stringify(info));
    3.  });
    
    也可以注册页面切换的状态回调，能在页面发生路由切换的时候拿到对应的页面信息[NavDestinationSwitchInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-observer#navdestinationswitchinfo12)，并且提供了UIAbilityContext和UIContext不同范围的监听：
    
    4.  // 在UIAbility中使用
    5.  import { UIContext, uiObserver } from '@kit.ArkUI';
    
    6.  // callbackFunc是开发者定义的监听回调函数
    7.  function callbackFunc(info: uiObserver.NavDestinationSwitchInfo) {}
    8.  uiObserver.on('navDestinationSwitch', this.context, callbackFunc);
    
    9.  // 可以通过窗口的getUIContext()方法获取对应的UIContent
    10.  uiContext: UIContext | null = null;
    11.  uiObserver.on('navDestinationSwitch', this.uiContext, callbackFunc);
    

## 页面转场

[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)默认提供了页面切换的转场动画，通过导航控制器操作时，会触发不同的转场效果（API version 13之前，[Dialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-base-dialog-overview)类型的页面默认无转场动画。从API version13开始，Dialog类型的页面支持系统转场动画。），Navigation也提供了关闭系统转场、自定义转场以及共享元素转场的能力。系统默认动画时长由物理曲线参数决定，不同设备上动画时长存在差异。

### 关闭转场

- 全局关闭
    
    Navigation通过NavPathStack中提供的[disableAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#disableanimation11)方法可以在当前Navigation中关闭或打开所有转场动画。
    
    1. pageStack: NavPathStack = new NavPathStack();
    
    2. aboutToAppear(): void {
    3.   this.pageStack.disableAnimation(true);
    4. }
    
- 单次关闭
    
    NavPathStack中提供的Push、Pop、Replace等接口中可以设置animated参数，默认为true表示有转场动画，需要单次关闭转场动画可以置为false，不影响下次转场动画。
    
    1. pageStack: NavPathStack = new NavPathStack();
    
    2. this.pageStack.pushPath({ name: "PageOne" }, false);
    3. this.pageStack.pop(false);
    

### 自定义转场

- Navigation自定义转场
    
    Navigation自定义转场动画能力通过[customNavContentTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#customnavcontenttransition11)事件提供，可以通过以下三步定义自定义转场动画：
    
    1. 构建一个自定义转场动画工具类CustomNavigationUtils，通过一个Map管理各页面的自定义动画对象CustomTransition。页面在创建时注册其自定义转场动画对象，在销毁时取消注册。
    2. 实现一个转场协议对象[NavigationAnimatedTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navigationanimatedtransition11)。其中，timeout属性表示转场结束的超时时间，默认为1000ms，transition属性为自定义的转场动画方法。开发者需在此实现自己的转场动画逻辑，系统在转场开始时会调用此方法，onTransitionEnd为转场结束时的回调。
    3. 调用customNavContentTransition方法并返回实现的转场协议对象，若返回undefined，则使用系统默认转场。
    
    具体示例代码可参考[Navigation自定义转场示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#%E7%A4%BA%E4%BE%8B3%E8%AE%BE%E7%BD%AE%E5%8F%AF%E4%BA%A4%E4%BA%92%E8%BD%AC%E5%9C%BA%E5%8A%A8%E7%94%BB)。
    
- NavDestination自定义转场
    
    [NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)支持自定义转场动画，通过设置[customTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#customtransition15)属性即可实现单个页面的自定义转场效果。要实现这一功能，需完成以下步骤：
    
    1. 实现[NavDestination的转场代理](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#navdestinationtransitiondelegate15)，针对不同的堆栈操作类型返回自定义的转场协议对象[NavDestinationTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#navdestinationtransition15)。其中，event是必填参数，需在此处编写自定义转场动画的逻辑；而onTransitionEnd、duration、curve与delay为可选参数，分别对应动画结束后的回调、动画持续时间、动画曲线类型与开始前的延时。若在转场代理中返回多个转场协议对象，这些动画效果将逐层叠加。
    2. 通过调用NavDestination组件的customTransition属性，并传入上述实现的转场代理，完成自定义转场的设置。
    
    具体示例代码可以参考[NavDestination自定义转场示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#%E7%A4%BA%E4%BE%8B2%E8%AE%BE%E7%BD%AEnavdestination%E8%87%AA%E5%AE%9A%E4%B9%89%E8%BD%AC%E5%9C%BA)。
    
- 使用建议
    
    1. Navigation自定义转场[customNavContentTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#customnavcontenttransition11)适用于控制Navigation内所有页面，统一转场动画效果。
    2. NavDestination自定义转场[customTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#customtransition15)适用于控制单个页面的转场效果。
    3. 在同时使用[customNavContentTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#customnavcontenttransition11)和[customTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#customtransition15)时，customNavContentTransition优先级更高。

### 共享元素转场

NavDestination之间切换时可以通过[geometryTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-transition-animation-geometrytransition#geometrytransition)实现共享元素转场。配置了共享元素转场的页面同时需要关闭系统默认的转场动画。

1. 为需要实现共享元素转场的组件添加geometryTransition属性，id参数必须在两个NavDestination之间保持一致。
    
    1. // 起始页配置共享元素id
    2. NavDestination() {
    3.   Column() {
    4.     // ...
    5.     // $r('app.media.startIcon')需要替换为开发者所需的资源文件
    6.     Image($r('app.media.startIcon'))
    7.     .geometryTransition('sharedId')
    8.     .width(100)
    9.     .height(100)
    10.   }
    11. }
    12. .title('FromPage')
    
    13. // 目的页配置共享元素id
    14. NavDestination() {
    15.   Column() {
    16.     // ...
    17.     // $r('app.media.startIcon')需要替换为开发者所需的资源文件
    18.     Image($r('app.media.startIcon'))
    19.     .geometryTransition('sharedId')
    20.     .width(200)
    21.     .height(200)
    22.   }
    23. }
    24. .title('ToPage')
    
2. 将页面路由的操作，放到animateTo动画闭包中，配置对应的动画参数以及关闭系统默认的转场。
    
    1. NavDestination() {
    2.   Column() {
    3.     Button('跳转目的页')
    4.     .width('80%')
    5.     .height(40)
    6.     .margin(20)
    7.     .onClick(() => {
    8.         this.getUIContext()?.animateTo({ duration: 1000 }, () => {
    9.           this.pageStack.pushPath({ name: 'ToPage' }, false)
    10.         });
    11.     })
    12.   }
    13. }
    14. .title('FromPage')
    

## 跨包路由

系统提供[系统路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E7%B3%BB%E7%BB%9F%E8%B7%AF%E7%94%B1%E8%A1%A8)和[自定义路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E7%94%B1%E8%A1%A8)两种实现方式。

- 系统路由表相对自定义路由表，使用更简单，只需要添加对应页面跳转配置项，即可实现页面跳转。
    
- 自定义路由表使用起来更复杂，但是可以根据应用业务进行定制处理。
    

支持自定义路由表和系统路由表混用。

### 路由表能力对比

不同路由方式适用于不同需求，易用性或可扩展性需根据项目特点权衡选择。

|路由方式|跨包跳转能力|可扩展性|易用性|
|:--|:--|:--|:--|
|[系统路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E7%B3%BB%E7%BB%9F%E8%B7%AF%E7%94%B1%E8%A1%A8)|跳转前无需import页面文件，页面按需动态加载。|可扩展性一般。|易用性更强，系统自动维护路由表。|
|[自定义路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E7%94%B1%E8%A1%A8)|跳转前需要import页面文件。|可扩展性更强。|易用性一般，需要开发者自行维护路由表。|

### 系统路由表

系统路由表是动态路由的一种实现方式。从API version 12开始，[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)支持使用系统路由表的方式进行动态路由。各业务模块（[HSP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/in-app-hsp)/[HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/har-package)）中需要独立配置route_map.json文件，在触发路由跳转时，应用只需要通过NavPathStack提供的路由方法，传入需要路由的页面配置名称，此时系统会自动完成路由模块的动态加载、页面组件构建，并完成路由跳转，从而实现了开发层面的模块解耦。系统路由表支持模拟器但不支持预览器。其主要步骤如下：

1. 在跳转目标模块的配置文件[module.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)添加路由表配置：
    
    1.   {
    2.     "module" : {
    3.       "routerMap": "$profile:route_map"
    4.     }
    5.   }
    
2. 添加完路由配置文件地址后，需要在工程resources/base/profile中创建route_map.json文件。添加如下配置信息：
    
    1.   {
    2.     "routerMap": [
    3.       {
    4.         "name": "PageOne",
    5.         "pageSourceFile": "src/main/ets/pages/PageOne.ets",
    6.         "buildFunction": "PageOneBuilder",
    7.         "data": {
    8.           "description" : "this is PageOne"
    9.         }
    10.       }
    11.     ]
    12.   }
    
    配置说明如下：
    
    |配置项|说明|
    |:--|:--|
    |name|可自定义的跳转页面名称。|
    |pageSourceFile|跳转目标页在包内的路径，相对src目录的相对路径。|
    |buildFunction|跳转目标页的入口函数名称，必须以@Builder修饰。|
    |data|应用自定义字段。可以通过配置项读取接口getConfigInRouteMap获取。|
    
3. 在跳转目标页面中，需要配置入口Builder函数，函数名称需要和route_map.json配置文件中的buildFunction保持一致，否则在编译时会报错。
    
    1.   // 跳转页面入口函数
    2.   @Builder
    3.   export function PageOneBuilder() {
    4.     PageOne();
    5.   }
    
    6.   @Component
    7.   struct PageOne {
    8.     pathStack: NavPathStack = new NavPathStack();
    
    9.     build() {
    10.       NavDestination() {
    11.       }
    12.       .title('PageOne')
    13.       .onReady((context: NavDestinationContext) => {
    14.          this.pathStack = context.pathStack;
    15.       })
    16.     }
    17.   }
    
4. 通过[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)等路由接口进行页面跳转。(注意：此时Navigation中可以不用配置[navDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)属性。)
    
    1.   @Entry
    2.   @Component
    3.   struct Index {
    4.     pageStack : NavPathStack = new NavPathStack();
    
    5.     build() {
    6.       Navigation(this.pageStack){
    7.       }.onAppear(() => {
    8.         this.pageStack.pushPathByName("PageOne", null, false);
    9.       })
    10.       .hideNavBar(true)
    11.     }
    12.   }
    

### 自定义路由表

自定义路由表通过给Navigation的[navDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)属性设置Builder函数实现，其特点是需要import页面。有两种import页面的方式，静态import和动态import，二者的区别在于：

|import方式|模块间耦合度|实现复杂度|性能|
|:--|:--|:--|:--|
|动态import|模块间解耦。|复杂度高。|性能好，按需加载，跳转前再加载对应页面。|
|静态import|模块间耦合。|复杂度低。|性能一般，初始化时一次性加载所有依赖的页面。|

**动态import（推荐）**

动态import旨在解决多个模块（HAR/HSP）能够复用相同的业务逻辑，实现各业务模块间的解耦，同时支持路由功能的扩展与整合，可以按需import，具体实现方法请参考[Navigation自定义动态路由](https://gitcode.com/harmonyos-cases/cases/blob/master/CommonAppDevelopment/common/routermodule/README_AUTO_GENERATE.md)示例。

动态import的优势：

- 路由定义除了跳转的URL以外，可以配置丰富的扩展信息，如横竖屏默认模式、是否需要鉴权等等，做路由跳转时统一处理。
- 给每个路由页面设置一个名字，按照名称进行跳转而不是文件路径。
- 页面的加载可以使用动态import（按需加载），防止首个页面加载大量代码导致卡顿。

实现方案：

1. 定义页面跳转配置项。
    - 使用资源文件进行定义，通过资源管理[@ohos.resourceManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resource-manager)在运行时对资源文件解析。
    - 在ets文件中配置路由加载配置项，一般包括路由页面名称（即pushPath等接口中页面的别名），文件所在模块名称（hsp/har的模块名），加载页面在模块内的路径（相对src目录的路径）。
2. 加载目标跳转页面，通过[动态import](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-dynamic-import)将跳转目标页面所在的模块在运行时加载，在模块加载完成后，调用模块中的方法，通过import在模块的方法中加载模块中显示的目标页面，并返回页面加载完成后定义的Builder函数。
3. 触发页面跳转，在Navigation的[navDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)属性执行步骤2中加载的Builder函数，即可跳转到目标页面。

**静态import**

静态import实现方式简单，但通过静态import页面进行路由跳转会导致不同模块之间的依赖耦合，并增加首页加载时间长等问题。建议使用[自定义路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E7%94%B1%E8%A1%A8)的动态import或[系统路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E7%B3%BB%E7%BB%9F%E8%B7%AF%E7%94%B1%E8%A1%A8)。

实现方案：

1. import { hilog } from '@kit.PerformanceAnalysisKit';
2. const DOMAIN = 0x0000;
3. @Entry
4. @Component
5. struct NavigationExample {
6.   @Provide('navPathStack') navPathStack: NavPathStack = new NavPathStack();
7.   private arr: number[] = [1, 2];

8.   @Builder
9.   pageMap(name: string) {
10.     if (name === "NavDestinationTitle1") {
11.       pageOneTmp();
12.     } else if (name === "NavDestinationTitle2") {
13.       pageTwoTmp();
14.     }
15.   }

16.   build() {
17.     Column() {
18.       Navigation(this.navPathStack) {
19.         TextInput({ placeholder: 'search...' })
20.           .width("90%")
21.           .height(40)

22.         List({ space: 12 }) {
23.           ForEach(this.arr, (item: number) => {
24.             ListItem() {
25.               Text("Page" + item)
26.                 .width("100%")
27.                 .height(72)
28.                 .borderRadius(24)
29.                 .fontSize(16)
30.                 .fontWeight(500)
31.                 .textAlign(TextAlign.Center)
32.                 .onClick(() => {
33.                   this.navPathStack.pushPath({ name: 'NavDestinationTitle' + item });
34.                 })
35.             }
36.           }, (item: number) => item.toString())
37.         }
38.         .width("90%")
39.         .margin({ top: 12 })
40.       }
41.       // $r('app.string.mainTitle')需要替换为开发者所需的字符串资源文件
42.       .title($r('app.string.mainTitle'))
43.       .navDestination(this.pageMap)
44.       .mode(NavigationMode.Split)
45.     }
46.     .height('100%')
47.     .width('100%')
48.   }
49. }

50. @Component
51. export struct pageTwoTmp {
52.   @Consume('navPathStack') navPathStack: NavPathStack;
53.   context = this.getUIContext().getHostContext();
54.   build() {
55.     NavDestination() {
56.       Column() {
57.         Text("NavDestinationContent2")
58.       }.width('100%').height('100%')
59.     }.title("NavDestinationTitle2")
60.     .onBackPressed(() => {
61.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈的栈顶元素
62.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
63.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
64.         JSON.stringify(popDestinationInfo));
65.       return true;
66.     })
67.   }
68. }

69. // pageOne.ets
70. @Component
71. export struct pageOneTmp {
72.   @Consume('navPathStack') navPathStack: NavPathStack;
73.   context = this.getUIContext().getHostContext();
74.   build() {
75.     NavDestination() {
76.       Column() {
77.         Text("NavDestinationContent1")
78.       }.width('100%').height('100%')
79.     }.title("NavDestinationTitle1")
80.     .onBackPressed(() => {
81.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈的栈顶元素
82.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
83.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
84.         JSON.stringify(popDestinationInfo));
85.       return true;
86.     })
87.   }
88. }

## 导航示例

### 创建导航首页

实现步骤为：

1.使用[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)创建导航主页，并创建导航控制器NavPathStack以此来实现不同页面之间的跳转。

2.在Navigation中增加[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-list)组件，来定义导航主页中不同的一级界面。

3.在List内的组件添加onClick方法，并在其中使用导航控制器NavPathStack的[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)方法，使组件可以在点击之后从当前页面跳转到输入参数name在路由表内对应的页面。

1. @Entry
2. @Component
3. struct NavigationDemo {
4.   @Provide('navPathStack') navPathStack: NavPathStack = new NavPathStack();
5.   private listArray: Array<string> = ['WLAN', 'Bluetooth', 'Personal Hotspot', 'Connect & Share'];

6.   build() {
7.     Column() {
8.       Navigation(this.navPathStack) {
9.         TextInput({ placeholder: '输入关键字搜索' })
10.           .width('90%')
11.           .height(40)
12.           .margin({ bottom: 10 })

13.         // 通过List定义导航的一级界面
14.         List({ space: 12, initialIndex: 0 }) {
15.           ForEach(this.listArray, (item: string) => {
16.             ListItem() {
17.               Row() {
18.                 Row() {
19.                   Text(`${item.slice(0, 1)}`)
20.                     .fontColor(Color.White)
21.                     .fontSize(14)
22.                     .fontWeight(FontWeight.Bold)
23.                 }
24.                 .width(30)
25.                 .height(30)
26.                 .backgroundColor('#a8a8a8')
27.                 .margin({ right: 20 })
28.                 .borderRadius(20)
29.                 .justifyContent(FlexAlign.Center)

30.                 Column() {
31.                   Text(item)
32.                     .fontSize(16)
33.                     .margin({ bottom: 5 })
34.                 }
35.                 .alignItems(HorizontalAlign.Start)

36.                 Blank()

37.                 Row()
38.                   .width(12)
39.                   .height(12)
40.                   .margin({ right: 15 })
41.                   .border({
42.                     width: { top: 2, right: 2 },
43.                     color: 0xcccccc
44.                   })
45.                   .rotate({ angle: 45 })
46.               }
47.               .borderRadius(15)
48.               .shadow({ radius: 100, color: '#ededed' })
49.               .width('90%')
50.               .alignItems(VerticalAlign.Center)
51.               .padding({ left: 15, top: 15, bottom: 15 })
52.               .backgroundColor(Color.White)
53.             }
54.             .width('100%')
55.             .onClick(() => {
56.               this.navPathStack.pushPathByName(`${item}`, '详情页面参数'); // 将name指定的NaviDestination页面信息入栈,传递的参数为param
57.             })
58.           }, (item: string): string => item)
59.         }
60.         .listDirection(Axis.Vertical)
61.         .edgeEffect(EdgeEffect.Spring)
62.         .sticky(StickyStyle.Header)
63.         .chainAnimation(false)
64.         .width('100%')
65.       }
66.       .width('100%')
67.       .mode(NavigationMode.Auto)
68.       .title('设置') // 设置标题文字
69.     }
70.     .size({ width: '100%', height: '100%' })
71.     .backgroundColor(0xf4f4f5)
72.   }
73. }

### 创建导航子页

导航子页1实现步骤为：

1.使用[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)，来创建导航子页PageOne。

2.创建导航控制器[NavPathStack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)并在[onReady](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onready11)时进行初始化，获取当前所在的导航控制器，以此来实现不同页面之间的跳转。

3.在子页面内的组件添加onClick，并在其中使用导航控制器NavPathStack的[pop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pop10)方法，使组件可以在点击之后弹出路由栈栈顶元素实现页面的返回。

1. //PageOne.ets
2. @Builder
3. export function PageOneBuilder(name: string, param: string) {
4.   PageOne({ name: name, value: param });
5. }

6. @Component
7. export struct PageOne {
8.   navPathStack: NavPathStack = new NavPathStack();
9.   name: string = '';
10.   @State value: string = '';

11.   build() {
12.     NavDestination() {
13.       Column() {
14.         Text(`${this.name}设置页面`)
15.           .width('100%')
16.           .fontSize(20)
17.           .fontColor(0x333333)
18.           .textAlign(TextAlign.Center)
19.           .textShadow({
20.             radius: 2,
21.             offsetX: 4,
22.             offsetY: 4,
23.             color: 0x909399
24.           })
25.           .padding({ top: 30 })
26.         Text(`${JSON.stringify(this.value)}`)
27.           .width('100%')
28.           .fontSize(18)
29.           .fontColor(0x666666)
30.           .textAlign(TextAlign.Center)
31.           .padding({ top: 45 })
32.         Button('返回')
33.           .width('50%')
34.           .height(40)
35.           .margin({ top: 50 })
36.           .onClick(() => {
37.             //弹出路由栈栈顶元素，返回上个页面
38.             this.navPathStack.pop();
39.           })
40.       }
41.       .size({ width: '100%', height: '100%' })
42.     }.title(`${this.name}`)
43.     .onReady((ctx: NavDestinationContext) => {
44.       // NavDestinationContext获取当前所在的导航控制器
45.       this.navPathStack = ctx.pathStack;
46.     })
47.   }
48. }

导航子页2实现步骤为：

1.使用NavDestination，来创建导航子页PageTwo。

2.创建导航控制器NavPathStack并在onReady时进行初始化，获取当前所在的导航控制器，以此来实现不同页面之间的跳转。

3.在子页面内的组件添加onClick，并在其中使用导航控制器NavPathStack的[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)方法，使组件可以在点击之后从当前页面跳转到输入参数name在路由表内对应的页面。

1. //PageTwo.ets
2. @Builder
3. export function PageTwoBuilder(name: string) {
4.   PageTwo({ name: name });
5. }

6. @Component
7. export struct PageTwo {
8.   navPathStack: NavPathStack = new NavPathStack();
9.   name: string = '';
10.   private listArray: Array<string> = ['Projection', 'Print', 'VPN', 'Private DNS', 'NFC'];

11.   build() {
12.     NavDestination() {
13.       Column() {
14.         List({ space: 12, initialIndex: 0 }) {
15.           ForEach(this.listArray, (item: string) => {
16.             ListItem() {
17.               Row() {
18.                 Row() {
19.                   Text(`${item.slice(0, 1)}`)
20.                     .fontColor(Color.White)
21.                     .fontSize(14)
22.                     .fontWeight(FontWeight.Bold)
23.                 }
24.                 .width(30)
25.                 .height(30)
26.                 .backgroundColor('#a8a8a8')
27.                 .margin({ right: 20 })
28.                 .borderRadius(20)
29.                 .justifyContent(FlexAlign.Center)

30.                 Column() {
31.                   Text(item)
32.                     .fontSize(16)
33.                     .margin({ bottom: 5 })
34.                 }
35.                 .alignItems(HorizontalAlign.Start)

36.                 Blank()

37.                 Row()
38.                   .width(12)
39.                   .height(12)
40.                   .margin({ right: 15 })
41.                   .border({
42.                     width: { top: 2, right: 2 },
43.                     color: 0xcccccc
44.                   })
45.                   .rotate({ angle: 45 })
46.               }
47.               .borderRadius(15)
48.               .shadow({ radius: 100, color: '#ededed' })
49.               .width('90%')
50.               .alignItems(VerticalAlign.Center)
51.               .padding({ left: 15, top: 15, bottom: 15 })
52.               .backgroundColor(Color.White)
53.             }
54.             .width('100%')
55.             .onClick(() => {
56.               this.navPathStack.pushPathByName(`${item}`, '页面设置参数');
57.             })
58.           }, (item: string): string => item)
59.         }
60.         .listDirection(Axis.Vertical)
61.         .edgeEffect(EdgeEffect.Spring)
62.         .sticky(StickyStyle.Header)
63.         .width('100%')
64.       }
65.       .size({ width: '100%', height: '100%' })
66.     }.title(`${this.name}`)
67.     .onReady((ctx: NavDestinationContext) => {
68.       // NavDestinationContext获取当前所在的导航控制器
69.       this.navPathStack = ctx.pathStack;
70.     })
71.   }
72. }

### 创建路由跳转

实现步骤为：

1.工程配置文件[module.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中配置 {"routerMap": "$profile:router_map"}。

2.router_map.json中配置全局路由表，导航控制器NavPathStack可根据路由表中的name将对应页面信息入栈。

1. {
2.   "routerMap" : [
3.     {
4.       "name" : "WLAN",
5.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
6.       "buildFunction" : "PageOneBuilder"
7.     },
8.     {
9.       "name" : "Bluetooth",
10.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
11.       "buildFunction" : "PageOneBuilder"
12.     },
13.     {
14.       "name" : "Personal Hotspot",
15.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
16.       "buildFunction" : "PageOneBuilder"
17.     },
18.     {
19.       "name" : "Connect & Share",
20.       "pageSourceFile"  : "src/main/ets/pages/PageTwo.ets",
21.       "buildFunction" : "PageTwoBuilder"
22.     },
23.     {
24.       "name" : "Projection",
25.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
26.       "buildFunction" : "PageOneBuilder"
27.     },
28.     {
29.       "name" : "Print",
30.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
31.       "buildFunction" : "PageOneBuilder"
32.     },
33.     {
34.       "name" : "VPN",
35.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
36.       "buildFunction" : "PageOneBuilder"
37.     },
38.     {
39.       "name" : "Private DNS",
40.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
41.       "buildFunction" : "PageOneBuilder"
42.     },
43.     {
44.       "name" : "NFC",
45.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
46.       "buildFunction" : "PageOneBuilder"
47.     }
48.   ]
49. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.30221763759141194730167703387201:50001231000000:2800:EB5B03A9F555626B4E13396CEDB9352183B61BA8917A1A339930A3837013D609.gif)

## 示例代码

- [Navigation系统路由](https://gitcode.com/harmonyos_samples/system-router-map)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-introduction "组件导航和页面路由概述")
# 组件导航(Navigation) (推荐)

更新时间: 2025-12-16 16:39

组件导航（[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)）主要用于实现Navigation页面（[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)）间的跳转，支持在不同Navigation页面间传递参数，提供灵活的跳转栈操作，从而更便捷地实现对不同页面的访问和复用。本文将从组件导航（Navigation）的显示模式、路由操作、子页面管理、跨包跳转以及跳转动效等几个方面进行详细介绍。

[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)是路由导航的根视图容器，一般作为页面（@Entry）的根容器，包括单栏（Stack）、分栏（Split）和自适应（Auto）三种显示模式。Navigation组件适用于模块内和跨模块的路由切换，通过组件级路由能力实现更加自然流畅的转场体验，并提供多种标题栏样式来呈现更好的标题和内容联动效果。一次开发，多端部署场景下，Navigation组件能够自动适配窗口显示大小，在窗口较大的场景下自动切换分栏展示效果。

Navigation组件主要包含​导航页和子页。导航页由标题栏（包含菜单栏）、内容区和工具栏组成，可以通过[hideNavBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#hidenavbar9)属性进行隐藏，导航页不存在[路由栈](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)中，与子页，以及子页之间可以通过路由操作进行切换。

在API version 9上，Navigation需要配合[NavRouter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navrouter)组件实现页面路由。从API version 10开始，更推荐使用[NavPathStack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)实现页面路由。

## 设置页面显示模式

[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)组件通过[mode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#mode9)属性设置页面的显示模式。

- 自适应模式
    
    Navigation组件默认为自适应模式，此时mode属性为NavigationMode.Auto。自适应模式下，当页面宽度大于等于一定阈值( API version 9及以前：520vp，API version 10及以后：600vp )时，Navigation组件采用分栏模式，反之采用单栏模式。
    
    收起
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .mode(NavigationMode.Auto)
    
- 单栏模式
    
    单栏模式适用于窄屏设备，发生路由跳转时，整个页面都会被替换。
    
    **图1** 单栏布局示意图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163913.39247956913604846372315161784606:50001231000000:2800:925B5823D0F65790083C974E6538E7DE423A4CD226690DE88CA88D854F7E3F88.png)
    
    将mode属性设置为NavigationMode.Stack，Navigation组件即可设置为单栏显示模式。
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .mode(NavigationMode.Stack)
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163913.94781536402667387449603288907682:50001231000000:2800:5E623CF9E47772521FAF0D79441B418D1FBF0ED5B16BADE1E1FC081CCAEFACA4.jpg)
    
- 分栏模式
    
    分栏模式适用于宽屏设备，分为左右两部分，发生路由跳转时，只有右边子页会被替换。
    
    **图2** 分栏布局示意图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163913.44635127908442444956882181138608:50001231000000:2800:29D142503D371ED20B0604DA5CCCBD05F9767952FCC5D5CE19B49743361AF01D.png)
    
    将mode属性设置为NavigationMode.Split，Navigation组件即可设置为分栏显示模式。
    
    1. import { hilog } from '@kit.PerformanceAnalysisKit';
    2. const DOMAIN = 0x0000;
    3. @Entry
    4. @Component
    5. struct NavigationExample {
    6.   @State toolTmp: ToolbarItem = {
    7.     'value': "func",
    8.     'icon': "./image/ic_public_highlights.svg",  // 当前目录image文件夹下的图标资源
    9.     'action': () => {}
    10.   };
    11.   @Provide('navPathStack') navPathStack: NavPathStack = new NavPathStack();
    12.   private arr: number[] = [1, 2, 3];
    
    13.   @Builder
    14.   pageMap(name: string) {
    15.     if (name === "NavDestinationTitle1") {
    16.       pageOneTmp();
    17.     } else if (name === "NavDestinationTitle2") {
    18.       pageTwoTmp();
    19.     } else if (name === "NavDestinationTitle3") {
    20.       pageThreeTmp();
    21.     }
    22.   }
    
    23.   build() {
    24.     Column() {
    25.       Navigation(this.navPathStack) {
    26.         TextInput({ placeholder: 'search...' })
    27.           .width("90%")
    28.           .height(40)
    29.           .backgroundColor('#FFFFFF')
    
    30.         List({ space: 12 }) {
    31.           ForEach(this.arr, (item: number) => {
    32.             ListItem() {
    33.               Text("Page" + item)
    34.                 .width("100%")
    35.                 .height(72)
    36.                 .backgroundColor('#FFFFFF')
    37.                 .borderRadius(24)
    38.                 .fontSize(16)
    39.                 .fontWeight(500)
    40.                 .textAlign(TextAlign.Center)
    41.                 .onClick(() => {
    42.                   this.navPathStack.pushPath({ name: 'NavDestinationTitle' + item });
    43.                 })
    44.             }
    45.           }, (item: number) => item.toString())
    46.         }
    47.         .width("90%")
    48.         .margin({ top: 12 })
    49.       }
    50.       .title("主标题")
    51.       .mode(NavigationMode.Split)
    52.       .navDestination(this.pageMap)
    53.       .menus([
    54.         {
    55.           value: "", icon: "./image/ic_public_search.svg", action: () => {
    56.           }
    57.         },
    58.         {
    59.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    60.           }
    61.         },
    62.         {
    63.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    64.           }
    65.         },
    66.         {
    67.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    68.           }
    69.         },
    70.         {
    71.           value: "", icon: "./image/ic_public_add.svg", action: () => {
    72.           }
    73.         }
    74.       ])
    75.       .toolbarConfiguration([this.toolTmp, this.toolTmp, this.toolTmp])
    76.     }
    77.     .height('100%')
    78.     .width('100%')
    79.     .backgroundColor('#F1F3F5')
    80.   }
    81. }
    
    82. // PageOne.ets
    83. @Component
    84. export struct pageOneTmp {
    85.   @Consume('navPathStack') navPathStack: NavPathStack;
    86.   context = this.getUIContext().getHostContext();
    87.   build() {
    88.     NavDestination() {
    89.       Column() {
    90.         Text("NavDestinationContent1")
    91.       }.width('100%').height('100%')
    92.     }.title("NavDestinationTitle1")
    93.     .onBackPressed(() => {
    94.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈栈顶元素
    95.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
    96.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
    97.         JSON.stringify(popDestinationInfo));
    98.       return true;
    99.     })
    100.   }
    101. }
    
    102. // PageTwo.ets
    103. @Component
    104. export struct pageTwoTmp {
    105.   @Consume('navPathStack') navPathStack: NavPathStack;
    106.   context = this.getUIContext().getHostContext();
    107.   build() {
    108.     NavDestination() {
    109.       Column() {
    110.         Text("NavDestinationContent2")
    111.       }.width('100%').height('100%')
    112.     }.title("NavDestinationTitle2")
    113.     .onBackPressed(() => {
    114.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈栈顶元素
    115.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
    116.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
    117.         JSON.stringify(popDestinationInfo));
    118.       return true;
    119.     })
    120.   }
    121. }
    
    122. // PageThree.ets
    123. @Component
    124. export struct pageThreeTmp {
    125.   @Consume('navPathStack') navPathStack: NavPathStack;
    126.   context = this.getUIContext().getHostContext();
    127.   build() {
    128.     NavDestination() {
    129.       Column() {
    130.         Text("NavDestinationContent3")
    131.       }.width('100%').height('100%')
    132.     }.title("NavDestinationTitle3")
    133.     .onBackPressed(() => {
    134.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈栈顶元素
    135.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
    136.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
    137.         JSON.stringify(popDestinationInfo));
    138.       return true;
    139.     })
    140.   }
    141. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.38522712307407973042152555339603:50001231000000:2800:210862FB40488CA357496A333F8C814C3375FF85E9C6EC2074FEB76A3517DB98.jpg)
    

## 设置标题栏模式

标题栏在界面顶部，用于呈现界面名称和操作入口，Navigation组件通过[titleMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#titlemode)属性设置标题栏模式。

说明

Navigation或NavDestination未设置主副标题并且没有返回键时，不显示标题栏。

- Mini模式
    
    普通型标题栏，用于一级页面不需要突出标题的场景。
    
    **图3** Mini模式标题栏
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.88917640640829362862283509704068:50001231000000:2800:A6899C99862B2B677DC35E58E135729F02D8AFC91611D3785F415702713E36CA.jpg)
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .titleMode(NavigationTitleMode.Mini)
    
- Full模式
    
    强调型标题栏，用于一级页面需要突出标题的场景。
    
    **图4** Full模式标题栏
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.76716253096362819389528325214830:50001231000000:2800:4F8C50DC6DC180EEDFCCD3B4029968E2FF19618370ED06D5B688BD572BCFB1EA.jpg)
    
    1. Navigation() {
    2.   // ...
    3. }
    4. .titleMode(NavigationTitleMode.Full)
    

## 设置菜单栏

菜单栏位于Navigation组件的右上角，开发者可以通过[menus](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#menus)属性进行设置。menus支持Array<[NavigationMenuItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navigationmenuitem)>和[CustomBuilder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-types#custombuilder8)两种参数类型。使用Array<NavigationMenuItem>类型时，竖屏最多支持显示3个图标，横屏最多支持显示5个图标，多余的图标会被放入自动生成的更多图标。

**图5** 设置了3个图标的菜单栏

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.73673441631946749215245150548418:50001231000000:2800:807E87EF7E5ADFFA9A9A846ED20101AC4AB9A0643F48CF41A0150795BC65B0DD.jpg)

1. let toolTmp: NavigationMenuItem  = {
2.   'value': 'func',
3.   'icon': 'ets/pages/navigation/template1/image/ic_public_add.svg',
4.   'action': () => {}
5. };
6. // ...
7.       Navigation(this.navPathStack) {
8.         // ...
9.       }
10.       .menus([toolTmp, toolTmp, toolTmp])

图片也可以引用resources中的资源。

1. let toolTmp: NavigationMenuItem  = {
2.   'value': 'func',
3.   'icon': 'resources/base/media/ic_public_add.svg',
4.   'action': () => {}
5. };
6. // ...
7.       Navigation(this.navPathStack) {
8.         // ...
9.       }
10.       .menus([toolTmp, toolTmp, toolTmp])

**图6** 设置了4个图标的菜单栏

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.50787801697064920089908207920699:50001231000000:2800:E62E892050408B63ACDFEA78F71C670DAD4153B291E146916FEB0AD290D16B77.jpg)

1. let toolTmp: NavigationMenuItem  = {
2.   'value': 'func',
3.   'icon': 'ets/pages/navigation/template1/image/ic_public_add.svg',
4.   'action': () => {}
5. };
6. // ...
7.       Navigation(this.navPathStack) {
8.         // ...
9.       }
10.       // 竖屏最多支持显示3个图标，多余的图标会被放入自动生成的更多图标
11.       .menus([toolTmp, toolTmp, toolTmp, toolTmp])

## 设置工具栏

工具栏位于Navigation组件的底部，开发者可以通过[toolbarConfiguration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#toolbarconfiguration10)属性进行设置。

**图7** 工具栏

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.17051218093016793180970087149026:50001231000000:2800:99FD7107F1BDE63C8614828B7CB573E786230469AEF4242386295E47BECFC7B5.jpg)

1. let toolTmp: ToolbarItem = {
2.   'value': 'func',
3.   'icon': 'ets/pages/navigation/template1/image/ic_public_highlights.svg',
4.   'action': () => {}
5. };
6. let tooBar: ToolbarItem[] = [toolTmp,toolTmp,toolTmp];
7. // ...
8.       Navigation(this.navPathStack) {
9.         // ...
10.       }
11.       .toolbarConfiguration(tooBar)

## 路由操作

Navigation路由相关的操作都是基于导航控制器[NavPathStack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)提供的方法进行，每个Navigation都需要创建并传入一个NavPathStack对象，用于管理页面。主要涉及页面跳转、页面返回、页面替换、页面删除、参数获取、路由拦截等功能。

从API version 12开始，导航控制器允许被继承。开发者可以在派生类中自定义属性和方法，也可以重写父类的方法。派生类对象可以替代基类NavPathStack对象使用。Navigation中的[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)页面存在于NavPathStack中，以栈的结构管理，我们称为路由栈。具体示例代码参见：[导航控制器继承示例代码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#%E7%A4%BA%E4%BE%8B10%E5%AE%9A%E4%B9%89%E5%AF%BC%E8%88%AA%E6%8E%A7%E5%88%B6%E5%99%A8%E6%B4%BE%E7%94%9F%E7%B1%BB)。

说明

1.不建议开发者通过监听生命周期的方式管理自己的路由栈。

2.在应用处于后台状态下，调用NavPathStack的栈操作方法，会在应用再次回到前台状态时触发刷新。

1. @Entry
2. @Component
3. struct Index {
4.   // 创建一个导航控制器对象并传入Navigation
5.   pageStack: NavPathStack = new NavPathStack();

6.   build() {
7.     Navigation(this.pageStack) {
8.     }
9.     .title('Main')
10.   }
11. }

### 页面跳转

NavPathStack通过Push相关的接口（如[pushPath](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpath10)、[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)、[pushDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushdestination11)、[pushDestinationByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushdestinationbyname11)）去实现页面跳转的功能，主要分为以下三类：

1. 普通跳转，通过页面的name去跳转，并可以携带param。
    
    1. this.pageStack.pushPath({ name: "PageOne", param: "PageOne Param" });
    2. this.pageStack.pushPathByName("PageOne", "PageOne Param");
    
2. 带返回回调的跳转，跳转时添加onPop回调，能在页面出栈时获取返回信息，并进行处理。
    
    1. this.pageStack.pushPathByName('PageOne', "PageOne Param", (popInfo) => {
    2.   console.info('Pop page name is: ' + popInfo.info.name + ', result: ' + JSON.stringify(popInfo.result));
    3. });
    
3. 带错误码的跳转，跳转结束会触发异步回调，返回错误码信息。
    
    1. this.pageStack.pushDestination({name: "PageOne", param: "PageOne Param"})
    2.   .catch((error: BusinessError) => {
    3.     console.error(`Push destination failed, error code = ${error.code}, error.message = ${error.message}.`);
    4.   }).then(() => {
    5.     console.info('Push destination succeed.');
    6.   });
    7. this.pageStack.pushDestinationByName("PageOne", "PageOne Param")
    8.   .catch((error: BusinessError) => {
    9.     console.error(`Push destination failed, error code = ${error.code}, error.message = ${error.message}.`);
    10.   }).then(() => {
    11.     console.info('Push destination succeed.');
    12.   });
    

### 页面返回

NavPathStack通过pop相关接口（如[pop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pop10)、[popToName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#poptoname10)、[popToIndex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#poptoindex10)、[clear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#clear10)）去实现页面返回功能。

1. // 返回到上一页
2. this.pageStack.pop();
3. // 返回到上一个PageOne页面
4. this.pageStack.popToName("PageOne");
5. // 返回到索引为1的页面
6. this.pageStack.popToIndex(1);
7. // 返回到根首页（清除栈中所有页面）
8. this.pageStack.clear();

### 页面替换

NavPathStack通过Replace相关接口（如[replacePath](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#replacepath11)、[replacePathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#replacepathbyname11)、[replaceDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#replacedestination18)）去实现页面替换功能。

1. // 将栈顶页面替换为PageOne
2. this.pageStack.replacePath({ name: "PageOne", param: "PageOne Param" });
3. this.pageStack.replacePathByName("PageOne", "PageOne Param");
4. // 带错误码的替换，跳转结束会触发异步回调，返回错误码信息
5. this.pageStack.replaceDestination({name: "PageOne", param: "PageOne Param"})
6.   .catch((error: BusinessError) => {
7.     console.error(`Replace destination failed, error code = ${error.code}, error.message = ${error.message}.`);
8.   }).then(() => {
9.     console.info('Replace destination succeed.');
10.   })

### 页面删除

NavPathStack通过Remove相关接口（如[removeByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#removebyname11)、[removeByIndexes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#removebyindexes11)、[removeByNavDestinationId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#removebynavdestinationid12)）去实现删除路由栈中特定页面的功能。

1. // 删除栈中name为PageOne的所有页面
2. this.pageStack.removeByName("PageOne");
3. // 删除指定索引的页面
4. this.pageStack.removeByIndexes([1, 3, 5]);
5. // 删除指定id的页面
6. this.pageStack.removeByNavDestinationId("1");

### 移动页面

NavPathStack通过Move相关接口（如[moveToTop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#movetotop10)、[moveIndexToTop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#moveindextotop10)）去实现移动路由栈中特定页面到栈顶的功能。

1. // 移动栈中name为PageOne的页面到栈顶
2. this.pageStack.moveToTop("PageOne");
3. // 移动栈中索引为1的页面到栈顶
4. this.pageStack.moveIndexToTop(1);

### 参数获取

[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)子页第一次创建时会触发[onReady](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onready11)回调，可以获取此页面对应的参数。

1. @Component
2. struct Page01 {
3.   pathStack: NavPathStack | undefined = undefined;
4.   pageParam: string = '';

5.   build() {
6.     NavDestination() {
7.       // ...
8.     }.title('Page01')
9.     .onReady((context: NavDestinationContext) => {
10.       this.pathStack = context.pathStack;
11.       this.pageParam = context.pathInfo.param as string;
12.     })
13.   }
14. }

NavDestination组件中可以通过设置[onResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onresult15)接口，接收返回时传递的路由参数。

1. class NavParam {
2.   desc: string = 'navigation-param'
3. }

4. @Component
5. struct DemoNavDestination {
6.   // ...
7.   build() {
8.     NavDestination() {
9.       // ...
10.     }
11.     .onResult((param: Object) => {
12.       if (param instanceof NavParam) {
13.         console.info('TestTag', 'get NavParam, its desc: ' + (param as NavParam).desc);
14.         return;
15.       }
16.       console.info('TestTag', 'param not instance of NavParam');
17.     })
18.   }
19. }

其他业务场景，可以通过主动调用NavPathStack的Get相关接口（如[getAllPathName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getallpathname10)、[getParamByIndex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getparambyindex10)、[getParamByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getparambyname10)、[getIndexByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#getindexbyname10)）去获取指定页面的参数。

1. // 获取栈中所有页面name集合
2. this.pageStack.getAllPathName();
3. // 获取索引为1的页面参数
4. this.pageStack.getParamByIndex(1);
5. // 获取PageOne页面的参数
6. this.pageStack.getParamByName("PageOne");
7. // 获取PageOne页面的索引集合
8. this.pageStack.getIndexByName("PageOne");

### 路由拦截

NavPathStack提供了[setInterception](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#setinterception12)方法，用于设置Navigation页面跳转拦截回调。该方法需要传入一个[NavigationInterception](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navigationinterception12)对象，该对象包含三个回调函数：

|名称|描述|
|:--|:--|
|willShow|页面跳转前回调，允许操作栈，在当前跳转生效。|
|didShow|页面跳转后回调，在该回调中操作栈会在下一次跳转生效。|
|modeChange|Navigation单双栏显示状态发生变更时触发该回调。|

说明

无论是哪个回调，在进入回调时路由栈都已经发生了变化。

开发者可以在willShow回调中通过修改路由栈来实现路由拦截重定向的能力。

1. this.pageStack.setInterception({
2.   willShow: (from: NavDestinationContext | "navBar", to: NavDestinationContext | "navBar",
3.     operation: NavigationOperation, animated: boolean) => {
4.     if (typeof to === "string") {
5.       console.info("target page is navigation home page.");
6.       return;
7.     }
8.     // 将跳转到PageTwo的路由重定向到PageOne
9.     let target: NavDestinationContext = to as NavDestinationContext;
10.     if (target.pathInfo.name === 'PageTwo') {
11.       target.pathStack.pop();
12.       target.pathStack.pushPathByName('PageOne', null);
13.     }
14.   }
15. })

### 单例跳转

通过设置[LaunchMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#launchmode12%E6%9E%9A%E4%B8%BE%E8%AF%B4%E6%98%8E)为LaunchMode.MOVE_TO_TOP_SINGLETON或LaunchMode.POP_TO_SINGLETON，可以实现Navigation路由栈的单实例跳转。单实例跳转的规则如下：

1. 当指定为LaunchMode.MOVE_TO_TOP_SINGLETON时，系统会从栈底到栈顶查找具有指定名称的NavDestination。找到后，该页面将被移动到栈顶（replace操作会用指定的NavDestination替换当前栈顶）。
2. 若指定为LaunchMode.POP_TO_SINGLETON，系统同样会从栈底到栈顶查找具有指定名称的NavDestination。找到后，便会移除该NavDestination上方的所有页面（replace操作会用指定的NavDestination替换当前栈顶）。

当栈中存在的NavDestination页面通过单实例方式移动到栈顶时，将触发[onNewParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onnewparam19)回调。

有关单实例跳转的示例代码，可以参考[Navigation单例跳转示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#%E7%A4%BA%E4%BE%8B2%E4%BD%BF%E7%94%A8%E5%AF%BC%E8%88%AA%E6%8E%A7%E5%88%B6%E5%99%A8%E6%96%B9%E6%B3%95)。

## 子页面

[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)是[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)子页面的根容器，用于承载子页面的一些特殊属性以及生命周期等。NavDestination可以设置独立的标题栏和菜单栏等属性，使用方法与Navigation相同。NavDestination也可以通过[mode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#mode11)属性设置不同的显示类型，用于满足不同页面的诉求。

### 页面显示类型

- 标准类型
    
    NavDestination组件默认为标准类型，此时mode属性为NavDestinationMode.STANDARD。标准类型的NavDestination的生命周期跟随其在NavPathStack路由栈中的位置变化而改变。
    
- 弹窗类型
    
    NavDestination设置mode为NavDestinationMode.DIALOG弹窗类型，此时整个NavDestination默认透明显示。弹窗类型的NavDestination显示和消失时不会影响下层标准类型的NavDestination的显示和生命周期，两者可以同时显示。
    
    1. // Dialog NavDestination
    2. @Entry
    3. @Component
    4.  struct Index {
    5.    @Provide('NavPathStack') pageStack: NavPathStack = new NavPathStack();
    
    6.    @Builder
    7.    PagesMap(name: string) {
    8.      if (name == 'DialogPage') {
    9.        DialogPage();
    10.      }
    11.    }
    
    12.    build() {
    13.      Navigation(this.pageStack) {
    14.        Button('Push DialogPage')
    15.          .margin(20)
    16.          .width('80%')
    17.          .onClick(() => {
    18.            this.pageStack.pushPathByName('DialogPage', '');
    19.          })
    20.      }
    21.      .mode(NavigationMode.Stack)
    22.      .title('Main')
    23.      .navDestination(this.PagesMap)
    24.    }
    25.  }
    
    26.  @Component
    27.  export struct DialogPage {
    28.    @Consume('NavPathStack') pageStack: NavPathStack;
    
    29.    build() {
    30.      NavDestination() {
    31.        Stack({ alignContent: Alignment.Center }) {
    32.          Column() {
    33.            Text("Dialog NavDestination")
    34.              .fontSize(20)
    35.              .margin({ bottom: 100 })
    36.            Button("Close").onClick(() => {
    37.              this.pageStack.pop();
    38.            }).width('30%')
    39.          }
    40.          .justifyContent(FlexAlign.Center)
    41.          .backgroundColor(Color.White)
    42.          .borderRadius(10)
    43.          .height('30%')
    44.          .width('80%')
    45.        }.height("100%").width('100%')
    46.      }
    47.      .backgroundColor('rgba(0,0,0,0.5)')
    48.      .hideTitleBar(true)
    49.      .mode(NavDestinationMode.DIALOG)
    50.    }
    51.  }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.54044996889160545821333494615153:50001231000000:2800:1C6F64946E20589F1ADDBC055027E949D521EFD4BDC226343350F6401D3A6E86.png)
    

### 页面生命周期

Navigation作为路由容器，其生命周期承载在NavDestination组件上，以组件事件的形式开放。

其生命周期大致可分为三类，自定义组件生命周期、通用组件生命周期和自有生命周期。其中，[aboutToAppear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttoappear)和[aboutToDisappear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttodisappear)是自定义组件的生命周期(NavDestination外层包含的自定义组件)，[OnAppear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-events-show-hide#onappear)和[OnDisappear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-events-show-hide#ondisappear)是组件的通用生命周期。剩下的生命周期为NavDestination独有。

生命周期时序如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.71014053475673058396905454101583:50001231000000:2800:2E7A765B6F0E13E37F64EA39C86F41B0C6FD73A0946A0B1D7B98F3744C840BB3.png)

- **aboutToAppear**：在创建自定义组件后，执行其build()函数之前执行（NavDestination创建之前），允许在该方法中改变状态变量，更改将在后续执行build()函数中生效。
- **onWillAppear**：NavDestination创建后，挂载到组件树之前执行，在该方法中更改状态变量会在当前帧显示生效。
- **onAppear**：通用生命周期事件，NavDestination组件挂载到组件树时执行。
- **onWillShow**：NavDestination组件布局显示之前执行，此时页面不可见（应用切换到前台不会触发）。
- **onShown**：NavDestination组件布局显示之后执行，此时页面已完成布局。
- **onActive**：NavDestination处于激活态（处于栈顶可操作，且上层无特殊组件遮挡）触发。
- **onWillHide**：NavDestination组件触发隐藏之前执行（应用切换到后台不会触发）。
- **onInactive**：NavDestination组件处于非激活态（处于非栈顶不可操作，或处于栈顶时上层有特殊组件遮挡）触发。
- **onHidden**：NavDestination组件触发隐藏后执行（非栈顶页面push进栈，栈顶页面pop出栈或应用切换到后台）。
- **onWillDisappear**：NavDestination组件即将销毁之前执行，如果有转场动画，会在动画前触发（栈顶页面pop出栈）。
- **onDisappear**：通用生命周期事件，NavDestination组件从组件树上卸载销毁时执行。
- **aboutToDisappear**：自定义组件析构销毁之前执行，不允许在该方法中改变状态变量。

### 页面监听和查询

为了方便组件跟页面解耦，在NavDestination子页面内部的自定义组件可以通过全局方法监听或查询到页面的一些状态信息。

- 页面信息查询
    
    自定义组件提供[queryNavDestinationInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-api#querynavdestinationinfo)方法，可以在NavDestination内部查询到当前所属页面的信息，返回值为[NavDestinationInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-observer#navdestinationinfo)，若查询不到则返回undefined。
    
    1.  import { uiObserver } from '@kit.ArkUI';
    
    2.  // NavDestination内的自定义组件
    3.  @Component
    4.  struct MyComponent {
    5.    navDesInfo: uiObserver.NavDestinationInfo | undefined;
    
    6.    aboutToAppear(): void {
    7.      this.navDesInfo = this.queryNavDestinationInfo();
    8.    }
    
    9.    build() {
    10.        Column() {
    11.          Text("所属页面Name: " + this.navDesInfo?.name)
    12.        }.width('100%').height('100%')
    13.    }
    14.  }
    
- 页面状态监听
    
    通过[observer.on('navDestinationUpdate')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-observer#uiobserveronnavdestinationupdate)提供的注册接口可以注册NavDestination生命周期变化的监听，使用方式如下：
    
    1. uiObserver.on('navDestinationUpdate', (info) => {
    2.      console.info('NavDestination state update', JSON.stringify(info));
    3.  });
    
    也可以注册页面切换的状态回调，能在页面发生路由切换的时候拿到对应的页面信息[NavDestinationSwitchInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-observer#navdestinationswitchinfo12)，并且提供了UIAbilityContext和UIContext不同范围的监听：
    
    4.  // 在UIAbility中使用
    5.  import { UIContext, uiObserver } from '@kit.ArkUI';
    
    6.  // callbackFunc是开发者定义的监听回调函数
    7.  function callbackFunc(info: uiObserver.NavDestinationSwitchInfo) {}
    8.  uiObserver.on('navDestinationSwitch', this.context, callbackFunc);
    
    9.  // 可以通过窗口的getUIContext()方法获取对应的UIContent
    10.  uiContext: UIContext | null = null;
    11.  uiObserver.on('navDestinationSwitch', this.uiContext, callbackFunc);
    

## 页面转场

[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)默认提供了页面切换的转场动画，通过导航控制器操作时，会触发不同的转场效果（API version 13之前，[Dialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-base-dialog-overview)类型的页面默认无转场动画。从API version13开始，Dialog类型的页面支持系统转场动画。），Navigation也提供了关闭系统转场、自定义转场以及共享元素转场的能力。系统默认动画时长由物理曲线参数决定，不同设备上动画时长存在差异。

### 关闭转场

- 全局关闭
    
    Navigation通过NavPathStack中提供的[disableAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#disableanimation11)方法可以在当前Navigation中关闭或打开所有转场动画。
    
    1. pageStack: NavPathStack = new NavPathStack();
    
    2. aboutToAppear(): void {
    3.   this.pageStack.disableAnimation(true);
    4. }
    
- 单次关闭
    
    NavPathStack中提供的Push、Pop、Replace等接口中可以设置animated参数，默认为true表示有转场动画，需要单次关闭转场动画可以置为false，不影响下次转场动画。
    
    1. pageStack: NavPathStack = new NavPathStack();
    
    2. this.pageStack.pushPath({ name: "PageOne" }, false);
    3. this.pageStack.pop(false);
    

### 自定义转场

- Navigation自定义转场
    
    Navigation自定义转场动画能力通过[customNavContentTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#customnavcontenttransition11)事件提供，可以通过以下三步定义自定义转场动画：
    
    1. 构建一个自定义转场动画工具类CustomNavigationUtils，通过一个Map管理各页面的自定义动画对象CustomTransition。页面在创建时注册其自定义转场动画对象，在销毁时取消注册。
    2. 实现一个转场协议对象[NavigationAnimatedTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navigationanimatedtransition11)。其中，timeout属性表示转场结束的超时时间，默认为1000ms，transition属性为自定义的转场动画方法。开发者需在此实现自己的转场动画逻辑，系统在转场开始时会调用此方法，onTransitionEnd为转场结束时的回调。
    3. 调用customNavContentTransition方法并返回实现的转场协议对象，若返回undefined，则使用系统默认转场。
    
    具体示例代码可参考[Navigation自定义转场示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#%E7%A4%BA%E4%BE%8B3%E8%AE%BE%E7%BD%AE%E5%8F%AF%E4%BA%A4%E4%BA%92%E8%BD%AC%E5%9C%BA%E5%8A%A8%E7%94%BB)。
    
- NavDestination自定义转场
    
    [NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)支持自定义转场动画，通过设置[customTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#customtransition15)属性即可实现单个页面的自定义转场效果。要实现这一功能，需完成以下步骤：
    
    1. 实现[NavDestination的转场代理](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#navdestinationtransitiondelegate15)，针对不同的堆栈操作类型返回自定义的转场协议对象[NavDestinationTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#navdestinationtransition15)。其中，event是必填参数，需在此处编写自定义转场动画的逻辑；而onTransitionEnd、duration、curve与delay为可选参数，分别对应动画结束后的回调、动画持续时间、动画曲线类型与开始前的延时。若在转场代理中返回多个转场协议对象，这些动画效果将逐层叠加。
    2. 通过调用NavDestination组件的customTransition属性，并传入上述实现的转场代理，完成自定义转场的设置。
    
    具体示例代码可以参考[NavDestination自定义转场示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#%E7%A4%BA%E4%BE%8B2%E8%AE%BE%E7%BD%AEnavdestination%E8%87%AA%E5%AE%9A%E4%B9%89%E8%BD%AC%E5%9C%BA)。
    
- 使用建议
    
    1. Navigation自定义转场[customNavContentTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#customnavcontenttransition11)适用于控制Navigation内所有页面，统一转场动画效果。
    2. NavDestination自定义转场[customTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#customtransition15)适用于控制单个页面的转场效果。
    3. 在同时使用[customNavContentTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#customnavcontenttransition11)和[customTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#customtransition15)时，customNavContentTransition优先级更高。

### 共享元素转场

NavDestination之间切换时可以通过[geometryTransition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-transition-animation-geometrytransition#geometrytransition)实现共享元素转场。配置了共享元素转场的页面同时需要关闭系统默认的转场动画。

1. 为需要实现共享元素转场的组件添加geometryTransition属性，id参数必须在两个NavDestination之间保持一致。
    
    1. // 起始页配置共享元素id
    2. NavDestination() {
    3.   Column() {
    4.     // ...
    5.     // $r('app.media.startIcon')需要替换为开发者所需的资源文件
    6.     Image($r('app.media.startIcon'))
    7.     .geometryTransition('sharedId')
    8.     .width(100)
    9.     .height(100)
    10.   }
    11. }
    12. .title('FromPage')
    
    13. // 目的页配置共享元素id
    14. NavDestination() {
    15.   Column() {
    16.     // ...
    17.     // $r('app.media.startIcon')需要替换为开发者所需的资源文件
    18.     Image($r('app.media.startIcon'))
    19.     .geometryTransition('sharedId')
    20.     .width(200)
    21.     .height(200)
    22.   }
    23. }
    24. .title('ToPage')
    
2. 将页面路由的操作，放到animateTo动画闭包中，配置对应的动画参数以及关闭系统默认的转场。
    
    1. NavDestination() {
    2.   Column() {
    3.     Button('跳转目的页')
    4.     .width('80%')
    5.     .height(40)
    6.     .margin(20)
    7.     .onClick(() => {
    8.         this.getUIContext()?.animateTo({ duration: 1000 }, () => {
    9.           this.pageStack.pushPath({ name: 'ToPage' }, false)
    10.         });
    11.     })
    12.   }
    13. }
    14. .title('FromPage')
    

## 跨包路由

系统提供[系统路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E7%B3%BB%E7%BB%9F%E8%B7%AF%E7%94%B1%E8%A1%A8)和[自定义路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E7%94%B1%E8%A1%A8)两种实现方式。

- 系统路由表相对自定义路由表，使用更简单，只需要添加对应页面跳转配置项，即可实现页面跳转。
    
- 自定义路由表使用起来更复杂，但是可以根据应用业务进行定制处理。
    

支持自定义路由表和系统路由表混用。

### 路由表能力对比

不同路由方式适用于不同需求，易用性或可扩展性需根据项目特点权衡选择。

|路由方式|跨包跳转能力|可扩展性|易用性|
|:--|:--|:--|:--|
|[系统路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E7%B3%BB%E7%BB%9F%E8%B7%AF%E7%94%B1%E8%A1%A8)|跳转前无需import页面文件，页面按需动态加载。|可扩展性一般。|易用性更强，系统自动维护路由表。|
|[自定义路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E7%94%B1%E8%A1%A8)|跳转前需要import页面文件。|可扩展性更强。|易用性一般，需要开发者自行维护路由表。|

### 系统路由表

系统路由表是动态路由的一种实现方式。从API version 12开始，[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)支持使用系统路由表的方式进行动态路由。各业务模块（[HSP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/in-app-hsp)/[HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/har-package)）中需要独立配置route_map.json文件，在触发路由跳转时，应用只需要通过NavPathStack提供的路由方法，传入需要路由的页面配置名称，此时系统会自动完成路由模块的动态加载、页面组件构建，并完成路由跳转，从而实现了开发层面的模块解耦。系统路由表支持模拟器但不支持预览器。其主要步骤如下：

1. 在跳转目标模块的配置文件[module.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)添加路由表配置：
    
    1.   {
    2.     "module" : {
    3.       "routerMap": "$profile:route_map"
    4.     }
    5.   }
    
2. 添加完路由配置文件地址后，需要在工程resources/base/profile中创建route_map.json文件。添加如下配置信息：
    
    1.   {
    2.     "routerMap": [
    3.       {
    4.         "name": "PageOne",
    5.         "pageSourceFile": "src/main/ets/pages/PageOne.ets",
    6.         "buildFunction": "PageOneBuilder",
    7.         "data": {
    8.           "description" : "this is PageOne"
    9.         }
    10.       }
    11.     ]
    12.   }
    
    配置说明如下：
    
    |配置项|说明|
    |:--|:--|
    |name|可自定义的跳转页面名称。|
    |pageSourceFile|跳转目标页在包内的路径，相对src目录的相对路径。|
    |buildFunction|跳转目标页的入口函数名称，必须以@Builder修饰。|
    |data|应用自定义字段。可以通过配置项读取接口getConfigInRouteMap获取。|
    
3. 在跳转目标页面中，需要配置入口Builder函数，函数名称需要和route_map.json配置文件中的buildFunction保持一致，否则在编译时会报错。
    
    1.   // 跳转页面入口函数
    2.   @Builder
    3.   export function PageOneBuilder() {
    4.     PageOne();
    5.   }
    
    6.   @Component
    7.   struct PageOne {
    8.     pathStack: NavPathStack = new NavPathStack();
    
    9.     build() {
    10.       NavDestination() {
    11.       }
    12.       .title('PageOne')
    13.       .onReady((context: NavDestinationContext) => {
    14.          this.pathStack = context.pathStack;
    15.       })
    16.     }
    17.   }
    
4. 通过[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)等路由接口进行页面跳转。(注意：此时Navigation中可以不用配置[navDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)属性。)
    
    1.   @Entry
    2.   @Component
    3.   struct Index {
    4.     pageStack : NavPathStack = new NavPathStack();
    
    5.     build() {
    6.       Navigation(this.pageStack){
    7.       }.onAppear(() => {
    8.         this.pageStack.pushPathByName("PageOne", null, false);
    9.       })
    10.       .hideNavBar(true)
    11.     }
    12.   }
    

### 自定义路由表

自定义路由表通过给Navigation的[navDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)属性设置Builder函数实现，其特点是需要import页面。有两种import页面的方式，静态import和动态import，二者的区别在于：

|import方式|模块间耦合度|实现复杂度|性能|
|:--|:--|:--|:--|
|动态import|模块间解耦。|复杂度高。|性能好，按需加载，跳转前再加载对应页面。|
|静态import|模块间耦合。|复杂度低。|性能一般，初始化时一次性加载所有依赖的页面。|

**动态import（推荐）**

动态import旨在解决多个模块（HAR/HSP）能够复用相同的业务逻辑，实现各业务模块间的解耦，同时支持路由功能的扩展与整合，可以按需import，具体实现方法请参考[Navigation自定义动态路由](https://gitcode.com/harmonyos-cases/cases/blob/master/CommonAppDevelopment/common/routermodule/README_AUTO_GENERATE.md)示例。

动态import的优势：

- 路由定义除了跳转的URL以外，可以配置丰富的扩展信息，如横竖屏默认模式、是否需要鉴权等等，做路由跳转时统一处理。
- 给每个路由页面设置一个名字，按照名称进行跳转而不是文件路径。
- 页面的加载可以使用动态import（按需加载），防止首个页面加载大量代码导致卡顿。

实现方案：

1. 定义页面跳转配置项。
    - 使用资源文件进行定义，通过资源管理[@ohos.resourceManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resource-manager)在运行时对资源文件解析。
    - 在ets文件中配置路由加载配置项，一般包括路由页面名称（即pushPath等接口中页面的别名），文件所在模块名称（hsp/har的模块名），加载页面在模块内的路径（相对src目录的路径）。
2. 加载目标跳转页面，通过[动态import](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-dynamic-import)将跳转目标页面所在的模块在运行时加载，在模块加载完成后，调用模块中的方法，通过import在模块的方法中加载模块中显示的目标页面，并返回页面加载完成后定义的Builder函数。
3. 触发页面跳转，在Navigation的[navDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)属性执行步骤2中加载的Builder函数，即可跳转到目标页面。

**静态import**

静态import实现方式简单，但通过静态import页面进行路由跳转会导致不同模块之间的依赖耦合，并增加首页加载时间长等问题。建议使用[自定义路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%B7%AF%E7%94%B1%E8%A1%A8)的动态import或[系统路由表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E7%B3%BB%E7%BB%9F%E8%B7%AF%E7%94%B1%E8%A1%A8)。

实现方案：

1. import { hilog } from '@kit.PerformanceAnalysisKit';
2. const DOMAIN = 0x0000;
3. @Entry
4. @Component
5. struct NavigationExample {
6.   @Provide('navPathStack') navPathStack: NavPathStack = new NavPathStack();
7.   private arr: number[] = [1, 2];

8.   @Builder
9.   pageMap(name: string) {
10.     if (name === "NavDestinationTitle1") {
11.       pageOneTmp();
12.     } else if (name === "NavDestinationTitle2") {
13.       pageTwoTmp();
14.     }
15.   }

16.   build() {
17.     Column() {
18.       Navigation(this.navPathStack) {
19.         TextInput({ placeholder: 'search...' })
20.           .width("90%")
21.           .height(40)

22.         List({ space: 12 }) {
23.           ForEach(this.arr, (item: number) => {
24.             ListItem() {
25.               Text("Page" + item)
26.                 .width("100%")
27.                 .height(72)
28.                 .borderRadius(24)
29.                 .fontSize(16)
30.                 .fontWeight(500)
31.                 .textAlign(TextAlign.Center)
32.                 .onClick(() => {
33.                   this.navPathStack.pushPath({ name: 'NavDestinationTitle' + item });
34.                 })
35.             }
36.           }, (item: number) => item.toString())
37.         }
38.         .width("90%")
39.         .margin({ top: 12 })
40.       }
41.       // $r('app.string.mainTitle')需要替换为开发者所需的字符串资源文件
42.       .title($r('app.string.mainTitle'))
43.       .navDestination(this.pageMap)
44.       .mode(NavigationMode.Split)
45.     }
46.     .height('100%')
47.     .width('100%')
48.   }
49. }

50. @Component
51. export struct pageTwoTmp {
52.   @Consume('navPathStack') navPathStack: NavPathStack;
53.   context = this.getUIContext().getHostContext();
54.   build() {
55.     NavDestination() {
56.       Column() {
57.         Text("NavDestinationContent2")
58.       }.width('100%').height('100%')
59.     }.title("NavDestinationTitle2")
60.     .onBackPressed(() => {
61.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈的栈顶元素
62.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
63.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
64.         JSON.stringify(popDestinationInfo));
65.       return true;
66.     })
67.   }
68. }

69. // pageOne.ets
70. @Component
71. export struct pageOneTmp {
72.   @Consume('navPathStack') navPathStack: NavPathStack;
73.   context = this.getUIContext().getHostContext();
74.   build() {
75.     NavDestination() {
76.       Column() {
77.         Text("NavDestinationContent1")
78.       }.width('100%').height('100%')
79.     }.title("NavDestinationTitle1")
80.     .onBackPressed(() => {
81.       const popDestinationInfo = this.navPathStack.pop(); // 弹出路由栈的栈顶元素
82.       // $r('app.string.returnValue')需要替换为开发者所需的字符串资源文件
83.       hilog.info(DOMAIN, 'testTag', 'pop', this.context!.resourceManager.getStringSync($r('app.string.returnValue').id),
84.         JSON.stringify(popDestinationInfo));
85.       return true;
86.     })
87.   }
88. }

## 导航示例

### 创建导航首页

实现步骤为：

1.使用[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)创建导航主页，并创建导航控制器NavPathStack以此来实现不同页面之间的跳转。

2.在Navigation中增加[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-list)组件，来定义导航主页中不同的一级界面。

3.在List内的组件添加onClick方法，并在其中使用导航控制器NavPathStack的[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)方法，使组件可以在点击之后从当前页面跳转到输入参数name在路由表内对应的页面。

1. @Entry
2. @Component
3. struct NavigationDemo {
4.   @Provide('navPathStack') navPathStack: NavPathStack = new NavPathStack();
5.   private listArray: Array<string> = ['WLAN', 'Bluetooth', 'Personal Hotspot', 'Connect & Share'];

6.   build() {
7.     Column() {
8.       Navigation(this.navPathStack) {
9.         TextInput({ placeholder: '输入关键字搜索' })
10.           .width('90%')
11.           .height(40)
12.           .margin({ bottom: 10 })

13.         // 通过List定义导航的一级界面
14.         List({ space: 12, initialIndex: 0 }) {
15.           ForEach(this.listArray, (item: string) => {
16.             ListItem() {
17.               Row() {
18.                 Row() {
19.                   Text(`${item.slice(0, 1)}`)
20.                     .fontColor(Color.White)
21.                     .fontSize(14)
22.                     .fontWeight(FontWeight.Bold)
23.                 }
24.                 .width(30)
25.                 .height(30)
26.                 .backgroundColor('#a8a8a8')
27.                 .margin({ right: 20 })
28.                 .borderRadius(20)
29.                 .justifyContent(FlexAlign.Center)

30.                 Column() {
31.                   Text(item)
32.                     .fontSize(16)
33.                     .margin({ bottom: 5 })
34.                 }
35.                 .alignItems(HorizontalAlign.Start)

36.                 Blank()

37.                 Row()
38.                   .width(12)
39.                   .height(12)
40.                   .margin({ right: 15 })
41.                   .border({
42.                     width: { top: 2, right: 2 },
43.                     color: 0xcccccc
44.                   })
45.                   .rotate({ angle: 45 })
46.               }
47.               .borderRadius(15)
48.               .shadow({ radius: 100, color: '#ededed' })
49.               .width('90%')
50.               .alignItems(VerticalAlign.Center)
51.               .padding({ left: 15, top: 15, bottom: 15 })
52.               .backgroundColor(Color.White)
53.             }
54.             .width('100%')
55.             .onClick(() => {
56.               this.navPathStack.pushPathByName(`${item}`, '详情页面参数'); // 将name指定的NaviDestination页面信息入栈,传递的参数为param
57.             })
58.           }, (item: string): string => item)
59.         }
60.         .listDirection(Axis.Vertical)
61.         .edgeEffect(EdgeEffect.Spring)
62.         .sticky(StickyStyle.Header)
63.         .chainAnimation(false)
64.         .width('100%')
65.       }
66.       .width('100%')
67.       .mode(NavigationMode.Auto)
68.       .title('设置') // 设置标题文字
69.     }
70.     .size({ width: '100%', height: '100%' })
71.     .backgroundColor(0xf4f4f5)
72.   }
73. }

### 创建导航子页

导航子页1实现步骤为：

1.使用[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)，来创建导航子页PageOne。

2.创建导航控制器[NavPathStack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navpathstack10)并在[onReady](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination#onready11)时进行初始化，获取当前所在的导航控制器，以此来实现不同页面之间的跳转。

3.在子页面内的组件添加onClick，并在其中使用导航控制器NavPathStack的[pop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pop10)方法，使组件可以在点击之后弹出路由栈栈顶元素实现页面的返回。

1. //PageOne.ets
2. @Builder
3. export function PageOneBuilder(name: string, param: string) {
4.   PageOne({ name: name, value: param });
5. }

6. @Component
7. export struct PageOne {
8.   navPathStack: NavPathStack = new NavPathStack();
9.   name: string = '';
10.   @State value: string = '';

11.   build() {
12.     NavDestination() {
13.       Column() {
14.         Text(`${this.name}设置页面`)
15.           .width('100%')
16.           .fontSize(20)
17.           .fontColor(0x333333)
18.           .textAlign(TextAlign.Center)
19.           .textShadow({
20.             radius: 2,
21.             offsetX: 4,
22.             offsetY: 4,
23.             color: 0x909399
24.           })
25.           .padding({ top: 30 })
26.         Text(`${JSON.stringify(this.value)}`)
27.           .width('100%')
28.           .fontSize(18)
29.           .fontColor(0x666666)
30.           .textAlign(TextAlign.Center)
31.           .padding({ top: 45 })
32.         Button('返回')
33.           .width('50%')
34.           .height(40)
35.           .margin({ top: 50 })
36.           .onClick(() => {
37.             //弹出路由栈栈顶元素，返回上个页面
38.             this.navPathStack.pop();
39.           })
40.       }
41.       .size({ width: '100%', height: '100%' })
42.     }.title(`${this.name}`)
43.     .onReady((ctx: NavDestinationContext) => {
44.       // NavDestinationContext获取当前所在的导航控制器
45.       this.navPathStack = ctx.pathStack;
46.     })
47.   }
48. }

导航子页2实现步骤为：

1.使用NavDestination，来创建导航子页PageTwo。

2.创建导航控制器NavPathStack并在onReady时进行初始化，获取当前所在的导航控制器，以此来实现不同页面之间的跳转。

3.在子页面内的组件添加onClick，并在其中使用导航控制器NavPathStack的[pushPathByName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#pushpathbyname10)方法，使组件可以在点击之后从当前页面跳转到输入参数name在路由表内对应的页面。

1. //PageTwo.ets
2. @Builder
3. export function PageTwoBuilder(name: string) {
4.   PageTwo({ name: name });
5. }

6. @Component
7. export struct PageTwo {
8.   navPathStack: NavPathStack = new NavPathStack();
9.   name: string = '';
10.   private listArray: Array<string> = ['Projection', 'Print', 'VPN', 'Private DNS', 'NFC'];

11.   build() {
12.     NavDestination() {
13.       Column() {
14.         List({ space: 12, initialIndex: 0 }) {
15.           ForEach(this.listArray, (item: string) => {
16.             ListItem() {
17.               Row() {
18.                 Row() {
19.                   Text(`${item.slice(0, 1)}`)
20.                     .fontColor(Color.White)
21.                     .fontSize(14)
22.                     .fontWeight(FontWeight.Bold)
23.                 }
24.                 .width(30)
25.                 .height(30)
26.                 .backgroundColor('#a8a8a8')
27.                 .margin({ right: 20 })
28.                 .borderRadius(20)
29.                 .justifyContent(FlexAlign.Center)

30.                 Column() {
31.                   Text(item)
32.                     .fontSize(16)
33.                     .margin({ bottom: 5 })
34.                 }
35.                 .alignItems(HorizontalAlign.Start)

36.                 Blank()

37.                 Row()
38.                   .width(12)
39.                   .height(12)
40.                   .margin({ right: 15 })
41.                   .border({
42.                     width: { top: 2, right: 2 },
43.                     color: 0xcccccc
44.                   })
45.                   .rotate({ angle: 45 })
46.               }
47.               .borderRadius(15)
48.               .shadow({ radius: 100, color: '#ededed' })
49.               .width('90%')
50.               .alignItems(VerticalAlign.Center)
51.               .padding({ left: 15, top: 15, bottom: 15 })
52.               .backgroundColor(Color.White)
53.             }
54.             .width('100%')
55.             .onClick(() => {
56.               this.navPathStack.pushPathByName(`${item}`, '页面设置参数');
57.             })
58.           }, (item: string): string => item)
59.         }
60.         .listDirection(Axis.Vertical)
61.         .edgeEffect(EdgeEffect.Spring)
62.         .sticky(StickyStyle.Header)
63.         .width('100%')
64.       }
65.       .size({ width: '100%', height: '100%' })
66.     }.title(`${this.name}`)
67.     .onReady((ctx: NavDestinationContext) => {
68.       // NavDestinationContext获取当前所在的导航控制器
69.       this.navPathStack = ctx.pathStack;
70.     })
71.   }
72. }

### 创建路由跳转

实现步骤为：

1.工程配置文件[module.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中配置 {"routerMap": "$profile:router_map"}。

2.router_map.json中配置全局路由表，导航控制器NavPathStack可根据路由表中的name将对应页面信息入栈。

1. {
2.   "routerMap" : [
3.     {
4.       "name" : "WLAN",
5.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
6.       "buildFunction" : "PageOneBuilder"
7.     },
8.     {
9.       "name" : "Bluetooth",
10.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
11.       "buildFunction" : "PageOneBuilder"
12.     },
13.     {
14.       "name" : "Personal Hotspot",
15.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
16.       "buildFunction" : "PageOneBuilder"
17.     },
18.     {
19.       "name" : "Connect & Share",
20.       "pageSourceFile"  : "src/main/ets/pages/PageTwo.ets",
21.       "buildFunction" : "PageTwoBuilder"
22.     },
23.     {
24.       "name" : "Projection",
25.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
26.       "buildFunction" : "PageOneBuilder"
27.     },
28.     {
29.       "name" : "Print",
30.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
31.       "buildFunction" : "PageOneBuilder"
32.     },
33.     {
34.       "name" : "VPN",
35.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
36.       "buildFunction" : "PageOneBuilder"
37.     },
38.     {
39.       "name" : "Private DNS",
40.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
41.       "buildFunction" : "PageOneBuilder"
42.     },
43.     {
44.       "name" : "NFC",
45.       "pageSourceFile"  : "src/main/ets/pages/PageOne.ets",
46.       "buildFunction" : "PageOneBuilder"
47.     }
48.   ]
49. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163914.30221763759141194730167703387201:50001231000000:2800:EB5B03A9F555626B4E13396CEDB9352183B61BA8917A1A339930A3837013D609.gif)

## 示例代码

- [Navigation系统路由](https://gitcode.com/harmonyos_samples/system-router-map)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-introduction "组件导航和页面路由概述")
# 开发应用沉浸式效果

更新时间: 2025-12-16 16:39

## 概述

典型应用全屏窗口UI元素包括顶部[状态栏](https://developer.huawei.com/consumer/cn/doc/design-guides/status-bar-0000001776775568)、应用界面和底部导航区域（根据用户设置可表现为[导航条](https://developer.huawei.com/consumer/cn/doc/design-guides/navigation-0000001957075737)或三键导航），其中状态栏和导航区域，通常在沉浸式布局下称为避让区；避让区之外的区域称为安全区。开发应用沉浸式效果主要指通过调整状态栏、应用界面和底部导航区域的显示效果来减少状态栏、导航条或三键导航等系统界面的突兀感，从而使用户获得最佳的UI体验。

**图1** 界面元素示意图（此处以导航区域表现为导航条为例给出示意）  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.66183599372440285502873852231614:50001231000000:2800:7913E74432ECA76CC08C129FF68240BE3F1A235F53DBAC59530E070D48BD1C50.png "点击放大")

开发应用沉浸式效果主要要考虑如下几个设计要素：

- UI元素避让处理：底部导航区域可以响应点击事件，除此之外的可交互UI元素和应用关键信息不建议放到导航区域。状态栏显示系统信息，如果与界面元素有冲突，需要考虑避让状态栏。
- 沉浸式效果处理：设置状态栏的颜色和导航区域的显隐与界面元素颜色相匹配，不出现明显的突兀感。

针对上面的设计要求，可以通过如下两种方式实现应用沉浸式效果：

- [窗口全屏布局方案](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section15671730447)：调整布局系统为全屏布局，界面元素延伸到状态栏和导航区域实现沉浸式效果。当不隐藏避让区时，可通过接口查询状态栏和导航区域进行可交互元素避让处理，并设置状态栏或导航区域的颜色或显隐等属性与界面元素匹配。当隐藏避让区时，通过对应接口设置全屏布局即可。
- [组件安全区方案](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section202081847174413)：布局系统保持安全区内布局，然后通过接口延伸绘制内容（如背景色，背景图）到状态栏和导航区域实现沉浸式效果。
    
    该方案下，界面元素仅做绘制延伸，无法单独布局到状态栏和导航区域，针对需要单独布局UI元素到状态栏和导航区域的场景建议使用窗口全屏布局方案处理。
    

## 窗口全屏布局方案

窗口全屏布局方案主要涉及以下[应用扩展布局，全屏显示，不隐藏避让区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section171801550301)和[应用扩展布局，隐藏避让区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section202484117114)两个应用场景。

### 应用扩展布局，全屏显示，不隐藏避让区

可以通过调用窗口强制全屏布局接口[setWindowLayoutFullScreen()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowlayoutfullscreen9)实现界面元素延伸到状态栏和导航区域；然后通过接口[getWindowAvoidArea()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#getwindowavoidarea9)和[on('avoidAreaChange')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowlayoutfullscreen9)获取并动态监听避让区域的变更信息，页面布局根据避让区域信息进行动态调整；设置状态栏或导航区域的颜色或显隐等属性与界面元素进行匹配。

1. 调用setWindowLayoutFullScreen()接口设置窗口全屏。
    
    1. // EntryAbility.ets
    2. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    3. import { window } from '@kit.ArkUI';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
    5. export default class EntryAbility extends UIAbility {
    6.   // ...
    
    7.   onWindowStageCreate(windowStage: window.WindowStage): void {
    8.     windowStage.loadContent('pages/Index', (err, data) => {
    9.       if (err.code) {
    10.         return;
    11.       }
    
    12.       let windowClass: window.Window = windowStage.getMainWindowSync(); // 获取应用主窗口
    13.       // 1. 设置窗口全屏
    14.       let isLayoutFullScreen = true;
    15.       windowClass.setWindowLayoutFullScreen(isLayoutFullScreen).then(() => {
    16.         console.info('Succeeded in setting the window layout to full-screen mode.');
    17.       }).catch((err: BusinessError) => {
    18.         console.error(`Failed to set the window layout to full-screen mode. Code is ${err.code}, message is ${err.message}`);
    19.       });
    20.       // 进行后续步骤2-3中的操作
    21.     });
    22.   }
    23. }
    
2. 使用[getWindowAvoidArea()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#getwindowavoidarea9)接口获取当前布局遮挡区域（此处以状态栏、导航区域为例）。
    
    1. // EntryAbility.ets
    2. // 2. 获取布局避让遮挡的区域
    3. let type = window.AvoidAreaType.TYPE_NAVIGATION_INDICATOR; // 此处以导航条避让为例
    4. let avoidArea = windowClass.getWindowAvoidArea(type);
    5. let bottomRectHeight = avoidArea.bottomRect.height; // 获取到导航区域的高度
    6. AppStorage.setOrCreate('bottomRectHeight', bottomRectHeight);
    
    7. type = window.AvoidAreaType.TYPE_SYSTEM; // 以状态栏避让为例
    8. avoidArea = windowClass.getWindowAvoidArea(type);
    9. let topRectHeight = avoidArea.topRect.height; // 获取状态栏区域高度     
    10. AppStorage.setOrCreate('topRectHeight', topRectHeight);
    
3. 注册监听函数，动态获取避让区域的实时数据。常见的触发避让区回调的场景如下：应用窗口在全屏模式、悬浮模式、分屏模式之间的切换；应用窗口旋转；多折叠设备在屏幕折叠态和展开态之间的切换；应用窗口在多设备之间的流转。
    
    1. // EntryAbility.ets
    2. // 3. 注册监听函数，动态获取避让区域数据
    3. windowClass.on('avoidAreaChange', (data) => {
    4.   if (data.type === window.AvoidAreaType.TYPE_SYSTEM) {
    5.     let topRectHeight = data.area.topRect.height;
    6.     AppStorage.setOrCreate('topRectHeight', topRectHeight);
    7.   } else if (data.type == window.AvoidAreaType.TYPE_NAVIGATION_INDICATOR) {
    8.     let bottomRectHeight = data.area.bottomRect.height;
    9.     AppStorage.setOrCreate('bottomRectHeight', bottomRectHeight);
    10.   }
    11. });
    
4. 布局中的UI元素需要避让状态栏和导航区域，否则可能产生UI元素重叠等情况。
    
    说明
    
    避让区域存在大小为0的情况，当获取到的避让区域为0时，开发者需注意针对性处理适配此时的页面区域和布局，避免贴边、内容裁剪等问题，影响应用界面正常显示或美观性。
    
    如下例子中，对控件顶部设置padding（具体数值与状态栏高度一致），实现对状态栏的避让；对底部设置padding（具体数值与底部导航区域高度一致），实现对导航条的避让。如果去掉顶部和底部的padding设置，即不避让状态栏和导航条，UI元素就会发生重叠。具体可见下文步骤中图2和图3的效果对比。
    
    1. // Index.ets
    2. @Entry
    3. @Component
    4. struct Index {
    5.   @StorageProp('bottomRectHeight')
    6.   bottomRectHeight: number = 0;
    7.   @StorageProp('topRectHeight')
    8.   topRectHeight: number = 0;
    
    9.   build() {
    10.     Column() {
    11.       Row() {
    12.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    13.       }.backgroundColor('#2786d9')
    
    14.       Row() {
    15.         Text('Display Content 2').fontSize(30)
    16.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    17.       Row() {
    18.         Text('Display Content 3').fontSize(30)
    19.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    20.       Row() {
    21.         Text('Display Content 4').fontSize(30)
    22.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    23.       Row() {
    24.         Text('Display Content 5').fontSize(30)
    25.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    26.       Row() {
    27.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    28.       }.backgroundColor('#96dffa')
    29.     }
    30.     .width('100%')
    31.     .height('100%')
    32.     .alignItems(HorizontalAlign.Center)
    33.     .backgroundColor('#d5d5d5')
    34.     .justifyContent(FlexAlign.SpaceBetween)
    35.     // top数值与状态栏区域高度保持一致；bottom数值与导航区域高度保持一致
    36.     .padding({
    37.       top: this.getUIContext().px2vp(this.topRectHeight),
    38.       bottom: this.getUIContext().px2vp(this.bottomRectHeight)
    39.     })
    40.   }
    41. }
    
5. 根据实际的UI界面显示或相关UI元素背景颜色等，还可以按需设置状态栏的文字颜色、背景色或设置导航区域的显示或隐藏，以使UI界面效果呈现和谐。状态栏和导航区域默认是透明的，透传的是应用界面的背景色。
    
    此例中UI颜色主要有两种，比较简单，故未对状态栏文字颜色、背景色进行设置，未对导航区域进行隐藏。
    
    **图2** 布局避让状态栏和导航区域（此处以导航区域表现为导航条为例给出示意）  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.87006013163778539261709498662392:50001231000000:2800:A746E4D652D3D20AA672A5BF165B3699C55DC9456E44001D102D538ACD77E72B.jpg "点击放大")
    
    **图3** 布局未避让状态栏和导航区域，UI元素重叠（此处以导航区域表现为导航条为例给出示意）  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.57353412750221239108308721929172:50001231000000:2800:648A1F02A8BC0F5532422C2B618955F93999C9C2477489BA8D5714D235BF32FC.jpg "点击放大")
    

### 应用扩展布局，隐藏避让区

此场景下状态栏和导航区域需要隐藏，适用于游戏、电影等应用场景。用户可以通过从底部上滑唤出导航条或三键导航。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.99837954210435397706545783363927:50001231000000:2800:E0DDA552D6BF528E237CF861592011D02174A684C85AF203C34ACA45490F2C88.png "点击放大")

1. 调用setWindowLayoutFullScreen()接口设置窗口全屏。
    
    1. // EntryAbility.ets
    2. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    3. import { window } from '@kit.ArkUI';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
    5. export default class EntryAbility extends UIAbility {
    6.   // ...
    
    7.   onWindowStageCreate(windowStage: window.WindowStage): void {
    8.     windowStage.loadContent('pages/Index', (err, data) => {
    9.       if (err.code) {
    10.         return;
    11.       }
    
    12.       let windowClass: window.Window = windowStage.getMainWindowSync(); // 获取应用主窗口
    13.       // 1. 设置窗口全屏
    14.       let isLayoutFullScreen = true;
    15.       windowClass.setWindowLayoutFullScreen(isLayoutFullScreen).then(() => {
    16.         console.info('Succeeded in setting the window layout to full-screen mode.');
    17.       }).catch((err: BusinessError) => {
    18.         console.error(`Failed to set the window layout to full-screen mode. Code is ${err.code}, message is ${err.message}`);
    19.       });
    20.       // 进行后续步骤2中的状态栏和导航区域的隐藏操作
    21.     });
    22.   }
    23. }
    
2. 调用[setSpecificSystemBarEnabled()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setspecificsystembarenabled11)接口设置状态栏和导航区域的具体显隐状态，此场景下将其设置为隐藏。
    
    1. // EntryAbility.ets
    2. // 2. 设置状态栏隐藏
    3. windowClass.setSpecificSystemBarEnabled('status', false).then(() => {
    4.   console.info('Succeeded in setting the status bar to be invisible.');
    5. }).catch((err: BusinessError) => {
    6.   console.error(`Failed to set the status bar to be invisible. Code is ${err.code}, message is ${err.message}`);
    7. });
    8. // 2. 设置导航区域隐藏
    9. windowClass.setSpecificSystemBarEnabled('navigationIndicator', false).then(() => {
    10.   console.info('Succeeded in setting the navigation indicator to be invisible.');
    11. }).catch((err: BusinessError) => {
    12.   console.error(`Failed to set the navigation indicator to be invisible. Code is ${err.code}, message is ${err.message}`);
    13. });
    
3. 在界面中无需进行导航区域避让操作。
    
    1. // Index.ets
    2. @Entry()
    3. @Component
    4. struct Index {
    5.   build() {
    6.     Row() {
    7.       Column() {
    8.         Row() {
    9.           Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    10.         }.backgroundColor('#2786d9')
    
    11.         Row() {
    12.           Text('Display Content 2').fontSize(30)
    13.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    14.         Row() {
    15.           Text('Display Content 3').fontSize(30)
    16.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    17.         Row() {
    18.           Text('Display Content 4').fontSize(30)
    19.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    20.         Row() {
    21.           Text('Display Content 5').fontSize(30)
    22.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    23.         Row() {
    24.           Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    25.         }.backgroundColor('#96dffa')
    26.       }
    27.       .width('100%')
    28.       .height('100%')
    29.       .alignItems(HorizontalAlign.Center)
    30.       .justifyContent(FlexAlign.SpaceBetween)
    31.       .backgroundColor('#d5d5d5')
    32.     }
    33.   }
    34. }
    

## 组件安全区方案

应用未使用setWindowLayoutFullScreen()接口设置窗口全屏布局时，默认采取组件安全区布局方案。

应用在默认情况下窗口背景绘制范围是全屏，但UI元素被限制在安全区内（自动排除状态栏和导航区域）进行布局，来避免界面元素被状态栏和导航区域遮盖。

**图4** 界面元素自动避让状态栏和导航区域示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.49785881633116705159423116990391:50001231000000:2800:B33C69BC76D51355EC3CAE2413AEFC2778B11EF1DE34BF763C3215C43D52EEA0.png "点击放大")

针对状态栏和导航区域颜色与界面元素颜色不匹配问题，可以通过如下两种方式实现沉浸式效果：

- 状态栏和导航区域颜色相同场景，可以通过设置窗口的背景色来实现沉浸式效果。窗口背景色可通过[setWindowBackgroundColor()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowbackgroundcolor9)进行设置。
    
    1. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    2. import { window } from '@kit.ArkUI';
    
    3. export default class EntryAbility extends UIAbility {
    4.   //...
    
    5.   onWindowStageCreate(windowStage: window.WindowStage): void {
    6.     windowStage.loadContent('pages/Index', (err) => {
    7.       if (err.code) {
    8.         return;
    9.       }
    
    10.       // 设置全窗颜色和应用元素颜色一致
    11.       windowStage.getMainWindowSync().setWindowBackgroundColor('#d5d5d5');
    12.     });
    13.   }
    14. }
    
    界面状态栏和导航区域颜色相同场景。
    
    15. // xxx.ets
    16. @Entry
    17. @Component
    18. struct Example {
    19.   build() {
    20.     Column() {
    21.       Row() {
    22.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    23.       }.backgroundColor('#2786d9')
    
    24.       Row() {
    25.         Text('Display Content 2').fontSize(30)
    26.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    27.       Row() {
    28.         Text('Display Content 3').fontSize(30)
    29.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    30.       Row() {
    31.         Text('Display Content 4').fontSize(30)
    32.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    33.       Row() {
    34.         Text('Display Content 5').fontSize(30)
    35.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    36.       Row() {
    37.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    38.       }.backgroundColor('#96dffa')
    39.     }
    40.     .width('100%').height('100%')
    41.     .alignItems(HorizontalAlign.Center)
    42.     .backgroundColor('#d5d5d5')
    43.     .justifyContent(FlexAlign.SpaceBetween)
    44.   }
    45. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.48684961595489300477977200533131:50001231000000:2800:4DB5CDA0E0D7958CB4FB8E8AEC3D5128DD0539822614E9C3C8FD853148872890.png)
    
- 状态栏和导航区域颜色不同时，可以使用[expandSafeArea](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-expand-safe-area#expandsafearea)属性扩展安全区域属性进行调整。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct Example {
    5.   build() {
    6.     Column() {
    7.       Row() {
    8.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    9.       }.backgroundColor('#2786d9')
    10.       // 设置顶部绘制延伸到状态栏
    11.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])
    
    12.       Row() {
    13.         Text('Display Content 2').fontSize(30)
    14.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    15.       Row() {
    16.         Text('Display Content 3').fontSize(30)
    17.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    18.       Row() {
    19.         Text('Display Content 4').fontSize(30)
    20.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    21.       Row() {
    22.         Text('Display Content 5').fontSize(30)
    23.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    24.       Row() {
    25.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    26.       }.backgroundColor('#96dffa')
    27.       // 设置底部绘制延伸到导航区域
    28.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
    29.     }
    30.     .width('100%').height('100%')
    31.     .alignItems(HorizontalAlign.Center)
    32.     .backgroundColor('#d5d5d5')
    33.     .justifyContent(FlexAlign.SpaceBetween)
    34.   }
    35. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.75061394560447074198529736772042:50001231000000:2800:902E75D5CF9C4DD79174E234EDE65E52140DEE800228E4183BD6AB6FD0CFA27E.png)
    

### 扩展安全区域属性原理

- 布局阶段按照安全区范围大小进行UI元素布局。
- 布局完成后查看设置了expandSafeArea的组件边界（不包括margin）是否和安全区边界相交。
- 如果设置了expandSafeArea的组件和安全区边界相交，根据expandSafeArea传递的属性则进一步扩大组件绘制区域大小覆盖状态栏、导航区域这些非安全区域。
- 上述过程仅改变组件自身绘制大小，不进行二次布局，不影响子节点和兄弟节点的大小和位置。
- 子节点可以单独设置该属性，只需要自身边界和安全区域重合就可以延伸自身大小至非安全区域内，需要确保父组件未设置clip等裁切属性。
- 配置expandSafeArea属性组件进行绘制扩展时，需要关注组件不能配置固定宽高尺寸，百分比除外。
- 组件可以设置通用属性safeAreaPadding，给自身添加组件级安全区域。该属性作为一种特殊边距，在提供布局约束的同时作为安全区可以被一些系统组件利用。
    - safeAreaPadding位于原有的padding内侧。容器自外向内各层分别为border、padding、safeAreaPadding、内容区。当border和padding确定后，若容器可用空间不足以满足safeAreaPadding的设置，则优先分配给左侧和上侧safeAreaPadding、其次分配给右侧和下侧safeAreaPadding。safeAreaPadding实际尺寸确定后，余下空间为内容区。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.40814739523074922976450985656583:50001231000000:2800:3069DA8848E75088A5E18CA4DEFE8D5B560459053EC369BEE936096F37485126.png "点击放大")
        
    - 系统组件如Navigation、List、Scroll、Tabs等可以利用外层或容器自身safeAreaPadding实现扩大裁剪范围等能力。

### 背景图和视频场景

设置背景图、视频组件大小为安全区域大小并配置expandSafeArea属性。

说明

Video组件在使用expandSafeArea扩展到安全区域时，组件视频显示内容区域不支持扩展。

1. // xxx.ets
2. @Entry
3. @Component
4. struct SafeAreaExample1 {
5.   build() {
6.     Stack() {
7.       Image($r('app.media.bg'))
8.         .height('100%').width('100%')
9.         .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM]) // 图片组件的绘制区域扩展至状态栏和导航区域。
10.     }.height('100%').width('100%')
11.   }
12. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.43327826020269771674865794312820:50001231000000:2800:1022E21DA063B1509DB723CB9C69FDA61F3F93D6E7581D7C47F6EA7DAE310B6F.png)

### 滚动类场景

滚动容器设置expandSafeArea属性生效，但当父组件是滚动容器时，子组件设置expandSafeArea属性不生效。对于滚动容器的子组件，有两种方法实现沉浸式效果：

1. 设置父组件滚动容器和子组件相同的背景色，给父组件设置expandSafeArea属性扩展安全区。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct ScrollExample {
    5.   scroller: Scroller = new Scroller()
    6.   private arr: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    7.   build() {
    8.     Stack({ alignContent: Alignment.TopStart }) {
    9.       Scroll(this.scroller) {
    10.         Column() {
    11.           ForEach(this.arr, (item: number) => {
    12.             Stack() {
    13.               Text('Display Content ' + item.toString()).fontSize(30)
    14.             }
    15.             .width('80%').padding(20).borderRadius(15).backgroundColor(Color.White).margin({ top:30, bottom:30 })
    16.           }, (item: string) => item)
    17.         }.width('100%').backgroundColor('rgb(213,213,213)')
    18.       }.backgroundColor('rgb(213,213,213)')
    19.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    20.     }.width('100%').height('100%')
    21.     .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    22.   }
    23. }
    
    **图5** 滚动类容器设置expandSafeArea属性实现沉浸式效果  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.36343620665340982594714223798161:50001231000000:2800:AD6E0F7C59190801230E58A4FFAF23D4F65F1FDE15A3D82DCDAE08D5214E16FC.png)
    
2. 设置父组件滚动容器和子组件相同的背景色，设置滚动容器的内容裁剪属性clipContent(ContentClipMode.SAFE_AREA)，将内容层裁剪区域扩展至避让区。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct ScrollExample {
    5.   scroller: Scroller = new Scroller()
    6.   private arr: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    7.   build() {
    8.     Stack({ alignContent: Alignment.TopStart }) {
    9.       Scroll(this.scroller) {
    10.         Column() {
    11.           ForEach(this.arr, (item: number) => {
    12.             Stack() {
    13.               Text('Display Content ' + item.toString()).fontSize(30)
    14.             }
    15.             .width('80%').padding(20).borderRadius(15).backgroundColor(Color.White).margin({ top:30, bottom:30 })
    16.           }, (item: string) => item)
    17.         }.width('100%').backgroundColor('rgb(213,213,213)')
    18.       }.backgroundColor('rgb(213,213,213)')
    19.       .clipContent(ContentClipMode.SAFE_AREA)
    20.     }.width('100%').height('100%')
    21.   }
    22. }
    

**图6** 滚动类容器设置clipContent属性实现沉浸式效果  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.72942034796131303316500546979165:50001231000000:2800:F0FEA17F4AD3FF502D702340C369F02EFCC501694E07893050822DC1F2ADAEA3.png "点击放大")

### 底部页签场景

要求页签背景色能够延伸到导航区域（此处以导航区域表现为导航条为例给出示意），但页签内部可操作元素需要在导航区域之上。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.37246522656942551464504700503566:50001231000000:2800:F55E4980F4B7D0B0006E3960732E793DA44500BA6386C295E62801FCCCC9C579.png "点击放大")

针对底部的页签部分，Navigation组件和Tabs组件默认实现了页签的延伸处理，开发者只需要保证Navigation和Tabs组件的底部边界和底部导航区域重合即可。若开发者显式调用expandSafeArea接口，则安全区效果由expandSafeArea参数指定。

如果未使用上述组件而是采用自定义方式实现页签的场景，可以针对底部元素设置expandSafeArea属性实现底部元素的背景扩展。

**图7** 顶部和底部UI元素未设置和设置expandSafeArea属性效果对比

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.41747390740743659941506414504724:50001231000000:2800:E50527CF67161602DF8FD0C190F67F7D0B4B3B04CF45C3A0446CC37FE90CC51F.png)

1. // xxx.ets
2. @Entry
3. @Component
4. struct Example {
5.   build() {
6.     Column() {
7.       Row() {
8.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
9.       }.backgroundColor('#2786d9')
10.       // 设置顶部绘制延伸到状态栏
11.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])

12.       Row() {
13.         Text('Display Content 2').fontSize(30)
14.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

15.       Row() {
16.         Text('Display Content 3').fontSize(30)
17.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

18.       Row() {
19.         Text('Display Content 4').fontSize(30)
20.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

21.       Row() {
22.         Text('Display Content 5').fontSize(30)
23.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

24.       Row() {
25.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
26.       }.backgroundColor('#96dffa')
27.       // 设置底部绘制延伸到导航区域
28.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
29.     }
30.     .width('100%').height('100%')
31.     .alignItems(HorizontalAlign.Center)
32.     .backgroundColor('#d5d5d5')
33.     .justifyContent(FlexAlign.SpaceBetween)
34.   }
35. }

### 图文场景

当状态栏元素和底部导航区域元素不同时，无法单纯通过窗口背景色或者背景图组件延伸实现，此时需要对顶部元素和底部元素分别配置expandSafeArea属性，顶部元素配置expandSafeArea([SafeAreaType.SYSTEM],[SafeAreaEdge.TOP])，底部元素配置expandSafeArea([SafeAreaType.SYSTEM],[SafeAreaEdge.BOTTOM])。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.28582942626334677493417993476880:50001231000000:2800:70849062F759622A69E9F0C2E65D297CE52324158491314B545F1CF41A4F9041.png "点击放大")

1. @Entry
2. @Component
3. struct Index {
4.   build() {
5.     Swiper() {
6.       Column() {
7.         Image($r('app.media.start'))
8.           .height('50%').width('100%')
9.           // 设置图片延伸到状态栏
10.           .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])
11.         Column() {
12.           Text('HarmonyOS 第一课')
13.             .fontSize(32)
14.             .margin(30)
15.           Text('通过循序渐进的学习路径，无经验和有经验的开发者都可以掌握ArkTS语言声明式开发范式，体验更简洁、更友好的HarmonyOS应用开发旅程。')
16.             .fontSize(20).margin(20)
17.         }.height('50%').width('100%')
18.         .backgroundColor(Color.White)
19.         // 设置文本内容区背景延伸到导航栏
20.         .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
21.       }
22.     }
23.     .width('100%')
24.     .height('100%')
25.     // 关闭Swiper组件默认的裁切效果以便子节点可以绘制在Swiper外。
26.     .clip(false)
27.   }
28. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-tabs "选项卡 (Tabs)")
# 开发应用沉浸式效果

更新时间: 2025-12-16 16:39

## 概述

典型应用全屏窗口UI元素包括顶部[状态栏](https://developer.huawei.com/consumer/cn/doc/design-guides/status-bar-0000001776775568)、应用界面和底部导航区域（根据用户设置可表现为[导航条](https://developer.huawei.com/consumer/cn/doc/design-guides/navigation-0000001957075737)或三键导航），其中状态栏和导航区域，通常在沉浸式布局下称为避让区；避让区之外的区域称为安全区。开发应用沉浸式效果主要指通过调整状态栏、应用界面和底部导航区域的显示效果来减少状态栏、导航条或三键导航等系统界面的突兀感，从而使用户获得最佳的UI体验。

**图1** 界面元素示意图（此处以导航区域表现为导航条为例给出示意）  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.66183599372440285502873852231614:50001231000000:2800:7913E74432ECA76CC08C129FF68240BE3F1A235F53DBAC59530E070D48BD1C50.png "点击放大")

开发应用沉浸式效果主要要考虑如下几个设计要素：

- UI元素避让处理：底部导航区域可以响应点击事件，除此之外的可交互UI元素和应用关键信息不建议放到导航区域。状态栏显示系统信息，如果与界面元素有冲突，需要考虑避让状态栏。
- 沉浸式效果处理：设置状态栏的颜色和导航区域的显隐与界面元素颜色相匹配，不出现明显的突兀感。

针对上面的设计要求，可以通过如下两种方式实现应用沉浸式效果：

- [窗口全屏布局方案](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section15671730447)：调整布局系统为全屏布局，界面元素延伸到状态栏和导航区域实现沉浸式效果。当不隐藏避让区时，可通过接口查询状态栏和导航区域进行可交互元素避让处理，并设置状态栏或导航区域的颜色或显隐等属性与界面元素匹配。当隐藏避让区时，通过对应接口设置全屏布局即可。
- [组件安全区方案](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section202081847174413)：布局系统保持安全区内布局，然后通过接口延伸绘制内容（如背景色，背景图）到状态栏和导航区域实现沉浸式效果。
    
    该方案下，界面元素仅做绘制延伸，无法单独布局到状态栏和导航区域，针对需要单独布局UI元素到状态栏和导航区域的场景建议使用窗口全屏布局方案处理。
    

## 窗口全屏布局方案

窗口全屏布局方案主要涉及以下[应用扩展布局，全屏显示，不隐藏避让区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section171801550301)和[应用扩展布局，隐藏避让区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section202484117114)两个应用场景。

### 应用扩展布局，全屏显示，不隐藏避让区

可以通过调用窗口强制全屏布局接口[setWindowLayoutFullScreen()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowlayoutfullscreen9)实现界面元素延伸到状态栏和导航区域；然后通过接口[getWindowAvoidArea()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#getwindowavoidarea9)和[on('avoidAreaChange')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowlayoutfullscreen9)获取并动态监听避让区域的变更信息，页面布局根据避让区域信息进行动态调整；设置状态栏或导航区域的颜色或显隐等属性与界面元素进行匹配。

1. 调用setWindowLayoutFullScreen()接口设置窗口全屏。
    
    1. // EntryAbility.ets
    2. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    3. import { window } from '@kit.ArkUI';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
    5. export default class EntryAbility extends UIAbility {
    6.   // ...
    
    7.   onWindowStageCreate(windowStage: window.WindowStage): void {
    8.     windowStage.loadContent('pages/Index', (err, data) => {
    9.       if (err.code) {
    10.         return;
    11.       }
    
    12.       let windowClass: window.Window = windowStage.getMainWindowSync(); // 获取应用主窗口
    13.       // 1. 设置窗口全屏
    14.       let isLayoutFullScreen = true;
    15.       windowClass.setWindowLayoutFullScreen(isLayoutFullScreen).then(() => {
    16.         console.info('Succeeded in setting the window layout to full-screen mode.');
    17.       }).catch((err: BusinessError) => {
    18.         console.error(`Failed to set the window layout to full-screen mode. Code is ${err.code}, message is ${err.message}`);
    19.       });
    20.       // 进行后续步骤2-3中的操作
    21.     });
    22.   }
    23. }
    
2. 使用[getWindowAvoidArea()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#getwindowavoidarea9)接口获取当前布局遮挡区域（此处以状态栏、导航区域为例）。
    
    1. // EntryAbility.ets
    2. // 2. 获取布局避让遮挡的区域
    3. let type = window.AvoidAreaType.TYPE_NAVIGATION_INDICATOR; // 此处以导航条避让为例
    4. let avoidArea = windowClass.getWindowAvoidArea(type);
    5. let bottomRectHeight = avoidArea.bottomRect.height; // 获取到导航区域的高度
    6. AppStorage.setOrCreate('bottomRectHeight', bottomRectHeight);
    
    7. type = window.AvoidAreaType.TYPE_SYSTEM; // 以状态栏避让为例
    8. avoidArea = windowClass.getWindowAvoidArea(type);
    9. let topRectHeight = avoidArea.topRect.height; // 获取状态栏区域高度     
    10. AppStorage.setOrCreate('topRectHeight', topRectHeight);
    
3. 注册监听函数，动态获取避让区域的实时数据。常见的触发避让区回调的场景如下：应用窗口在全屏模式、悬浮模式、分屏模式之间的切换；应用窗口旋转；多折叠设备在屏幕折叠态和展开态之间的切换；应用窗口在多设备之间的流转。
    
    1. // EntryAbility.ets
    2. // 3. 注册监听函数，动态获取避让区域数据
    3. windowClass.on('avoidAreaChange', (data) => {
    4.   if (data.type === window.AvoidAreaType.TYPE_SYSTEM) {
    5.     let topRectHeight = data.area.topRect.height;
    6.     AppStorage.setOrCreate('topRectHeight', topRectHeight);
    7.   } else if (data.type == window.AvoidAreaType.TYPE_NAVIGATION_INDICATOR) {
    8.     let bottomRectHeight = data.area.bottomRect.height;
    9.     AppStorage.setOrCreate('bottomRectHeight', bottomRectHeight);
    10.   }
    11. });
    
4. 布局中的UI元素需要避让状态栏和导航区域，否则可能产生UI元素重叠等情况。
    
    说明
    
    避让区域存在大小为0的情况，当获取到的避让区域为0时，开发者需注意针对性处理适配此时的页面区域和布局，避免贴边、内容裁剪等问题，影响应用界面正常显示或美观性。
    
    如下例子中，对控件顶部设置padding（具体数值与状态栏高度一致），实现对状态栏的避让；对底部设置padding（具体数值与底部导航区域高度一致），实现对导航条的避让。如果去掉顶部和底部的padding设置，即不避让状态栏和导航条，UI元素就会发生重叠。具体可见下文步骤中图2和图3的效果对比。
    
    1. // Index.ets
    2. @Entry
    3. @Component
    4. struct Index {
    5.   @StorageProp('bottomRectHeight')
    6.   bottomRectHeight: number = 0;
    7.   @StorageProp('topRectHeight')
    8.   topRectHeight: number = 0;
    
    9.   build() {
    10.     Column() {
    11.       Row() {
    12.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    13.       }.backgroundColor('#2786d9')
    
    14.       Row() {
    15.         Text('Display Content 2').fontSize(30)
    16.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    17.       Row() {
    18.         Text('Display Content 3').fontSize(30)
    19.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    20.       Row() {
    21.         Text('Display Content 4').fontSize(30)
    22.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    23.       Row() {
    24.         Text('Display Content 5').fontSize(30)
    25.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    26.       Row() {
    27.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    28.       }.backgroundColor('#96dffa')
    29.     }
    30.     .width('100%')
    31.     .height('100%')
    32.     .alignItems(HorizontalAlign.Center)
    33.     .backgroundColor('#d5d5d5')
    34.     .justifyContent(FlexAlign.SpaceBetween)
    35.     // top数值与状态栏区域高度保持一致；bottom数值与导航区域高度保持一致
    36.     .padding({
    37.       top: this.getUIContext().px2vp(this.topRectHeight),
    38.       bottom: this.getUIContext().px2vp(this.bottomRectHeight)
    39.     })
    40.   }
    41. }
    
5. 根据实际的UI界面显示或相关UI元素背景颜色等，还可以按需设置状态栏的文字颜色、背景色或设置导航区域的显示或隐藏，以使UI界面效果呈现和谐。状态栏和导航区域默认是透明的，透传的是应用界面的背景色。
    
    此例中UI颜色主要有两种，比较简单，故未对状态栏文字颜色、背景色进行设置，未对导航区域进行隐藏。
    
    **图2** 布局避让状态栏和导航区域（此处以导航区域表现为导航条为例给出示意）  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.87006013163778539261709498662392:50001231000000:2800:A746E4D652D3D20AA672A5BF165B3699C55DC9456E44001D102D538ACD77E72B.jpg "点击放大")
    
    **图3** 布局未避让状态栏和导航区域，UI元素重叠（此处以导航区域表现为导航条为例给出示意）  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.57353412750221239108308721929172:50001231000000:2800:648A1F02A8BC0F5532422C2B618955F93999C9C2477489BA8D5714D235BF32FC.jpg "点击放大")
    

### 应用扩展布局，隐藏避让区

此场景下状态栏和导航区域需要隐藏，适用于游戏、电影等应用场景。用户可以通过从底部上滑唤出导航条或三键导航。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.99837954210435397706545783363927:50001231000000:2800:E0DDA552D6BF528E237CF861592011D02174A684C85AF203C34ACA45490F2C88.png "点击放大")

1. 调用setWindowLayoutFullScreen()接口设置窗口全屏。
    
    1. // EntryAbility.ets
    2. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    3. import { window } from '@kit.ArkUI';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
    5. export default class EntryAbility extends UIAbility {
    6.   // ...
    
    7.   onWindowStageCreate(windowStage: window.WindowStage): void {
    8.     windowStage.loadContent('pages/Index', (err, data) => {
    9.       if (err.code) {
    10.         return;
    11.       }
    
    12.       let windowClass: window.Window = windowStage.getMainWindowSync(); // 获取应用主窗口
    13.       // 1. 设置窗口全屏
    14.       let isLayoutFullScreen = true;
    15.       windowClass.setWindowLayoutFullScreen(isLayoutFullScreen).then(() => {
    16.         console.info('Succeeded in setting the window layout to full-screen mode.');
    17.       }).catch((err: BusinessError) => {
    18.         console.error(`Failed to set the window layout to full-screen mode. Code is ${err.code}, message is ${err.message}`);
    19.       });
    20.       // 进行后续步骤2中的状态栏和导航区域的隐藏操作
    21.     });
    22.   }
    23. }
    
2. 调用[setSpecificSystemBarEnabled()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setspecificsystembarenabled11)接口设置状态栏和导航区域的具体显隐状态，此场景下将其设置为隐藏。
    
    1. // EntryAbility.ets
    2. // 2. 设置状态栏隐藏
    3. windowClass.setSpecificSystemBarEnabled('status', false).then(() => {
    4.   console.info('Succeeded in setting the status bar to be invisible.');
    5. }).catch((err: BusinessError) => {
    6.   console.error(`Failed to set the status bar to be invisible. Code is ${err.code}, message is ${err.message}`);
    7. });
    8. // 2. 设置导航区域隐藏
    9. windowClass.setSpecificSystemBarEnabled('navigationIndicator', false).then(() => {
    10.   console.info('Succeeded in setting the navigation indicator to be invisible.');
    11. }).catch((err: BusinessError) => {
    12.   console.error(`Failed to set the navigation indicator to be invisible. Code is ${err.code}, message is ${err.message}`);
    13. });
    
3. 在界面中无需进行导航区域避让操作。
    
    1. // Index.ets
    2. @Entry()
    3. @Component
    4. struct Index {
    5.   build() {
    6.     Row() {
    7.       Column() {
    8.         Row() {
    9.           Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    10.         }.backgroundColor('#2786d9')
    
    11.         Row() {
    12.           Text('Display Content 2').fontSize(30)
    13.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    14.         Row() {
    15.           Text('Display Content 3').fontSize(30)
    16.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    17.         Row() {
    18.           Text('Display Content 4').fontSize(30)
    19.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    20.         Row() {
    21.           Text('Display Content 5').fontSize(30)
    22.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    23.         Row() {
    24.           Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    25.         }.backgroundColor('#96dffa')
    26.       }
    27.       .width('100%')
    28.       .height('100%')
    29.       .alignItems(HorizontalAlign.Center)
    30.       .justifyContent(FlexAlign.SpaceBetween)
    31.       .backgroundColor('#d5d5d5')
    32.     }
    33.   }
    34. }
    

## 组件安全区方案

应用未使用setWindowLayoutFullScreen()接口设置窗口全屏布局时，默认采取组件安全区布局方案。

应用在默认情况下窗口背景绘制范围是全屏，但UI元素被限制在安全区内（自动排除状态栏和导航区域）进行布局，来避免界面元素被状态栏和导航区域遮盖。

**图4** 界面元素自动避让状态栏和导航区域示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.49785881633116705159423116990391:50001231000000:2800:B33C69BC76D51355EC3CAE2413AEFC2778B11EF1DE34BF763C3215C43D52EEA0.png "点击放大")

针对状态栏和导航区域颜色与界面元素颜色不匹配问题，可以通过如下两种方式实现沉浸式效果：

- 状态栏和导航区域颜色相同场景，可以通过设置窗口的背景色来实现沉浸式效果。窗口背景色可通过[setWindowBackgroundColor()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowbackgroundcolor9)进行设置。
    
    1. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    2. import { window } from '@kit.ArkUI';
    
    3. export default class EntryAbility extends UIAbility {
    4.   //...
    
    5.   onWindowStageCreate(windowStage: window.WindowStage): void {
    6.     windowStage.loadContent('pages/Index', (err) => {
    7.       if (err.code) {
    8.         return;
    9.       }
    
    10.       // 设置全窗颜色和应用元素颜色一致
    11.       windowStage.getMainWindowSync().setWindowBackgroundColor('#d5d5d5');
    12.     });
    13.   }
    14. }
    
    界面状态栏和导航区域颜色相同场景。
    
    15. // xxx.ets
    16. @Entry
    17. @Component
    18. struct Example {
    19.   build() {
    20.     Column() {
    21.       Row() {
    22.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    23.       }.backgroundColor('#2786d9')
    
    24.       Row() {
    25.         Text('Display Content 2').fontSize(30)
    26.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    27.       Row() {
    28.         Text('Display Content 3').fontSize(30)
    29.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    30.       Row() {
    31.         Text('Display Content 4').fontSize(30)
    32.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    33.       Row() {
    34.         Text('Display Content 5').fontSize(30)
    35.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    36.       Row() {
    37.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    38.       }.backgroundColor('#96dffa')
    39.     }
    40.     .width('100%').height('100%')
    41.     .alignItems(HorizontalAlign.Center)
    42.     .backgroundColor('#d5d5d5')
    43.     .justifyContent(FlexAlign.SpaceBetween)
    44.   }
    45. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.48684961595489300477977200533131:50001231000000:2800:4DB5CDA0E0D7958CB4FB8E8AEC3D5128DD0539822614E9C3C8FD853148872890.png)
    
- 状态栏和导航区域颜色不同时，可以使用[expandSafeArea](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-expand-safe-area#expandsafearea)属性扩展安全区域属性进行调整。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct Example {
    5.   build() {
    6.     Column() {
    7.       Row() {
    8.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    9.       }.backgroundColor('#2786d9')
    10.       // 设置顶部绘制延伸到状态栏
    11.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])
    
    12.       Row() {
    13.         Text('Display Content 2').fontSize(30)
    14.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    15.       Row() {
    16.         Text('Display Content 3').fontSize(30)
    17.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    18.       Row() {
    19.         Text('Display Content 4').fontSize(30)
    20.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    21.       Row() {
    22.         Text('Display Content 5').fontSize(30)
    23.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    24.       Row() {
    25.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    26.       }.backgroundColor('#96dffa')
    27.       // 设置底部绘制延伸到导航区域
    28.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
    29.     }
    30.     .width('100%').height('100%')
    31.     .alignItems(HorizontalAlign.Center)
    32.     .backgroundColor('#d5d5d5')
    33.     .justifyContent(FlexAlign.SpaceBetween)
    34.   }
    35. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.75061394560447074198529736772042:50001231000000:2800:902E75D5CF9C4DD79174E234EDE65E52140DEE800228E4183BD6AB6FD0CFA27E.png)
    

### 扩展安全区域属性原理

- 布局阶段按照安全区范围大小进行UI元素布局。
- 布局完成后查看设置了expandSafeArea的组件边界（不包括margin）是否和安全区边界相交。
- 如果设置了expandSafeArea的组件和安全区边界相交，根据expandSafeArea传递的属性则进一步扩大组件绘制区域大小覆盖状态栏、导航区域这些非安全区域。
- 上述过程仅改变组件自身绘制大小，不进行二次布局，不影响子节点和兄弟节点的大小和位置。
- 子节点可以单独设置该属性，只需要自身边界和安全区域重合就可以延伸自身大小至非安全区域内，需要确保父组件未设置clip等裁切属性。
- 配置expandSafeArea属性组件进行绘制扩展时，需要关注组件不能配置固定宽高尺寸，百分比除外。
- 组件可以设置通用属性safeAreaPadding，给自身添加组件级安全区域。该属性作为一种特殊边距，在提供布局约束的同时作为安全区可以被一些系统组件利用。
    - safeAreaPadding位于原有的padding内侧。容器自外向内各层分别为border、padding、safeAreaPadding、内容区。当border和padding确定后，若容器可用空间不足以满足safeAreaPadding的设置，则优先分配给左侧和上侧safeAreaPadding、其次分配给右侧和下侧safeAreaPadding。safeAreaPadding实际尺寸确定后，余下空间为内容区。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.40814739523074922976450985656583:50001231000000:2800:3069DA8848E75088A5E18CA4DEFE8D5B560459053EC369BEE936096F37485126.png "点击放大")
        
    - 系统组件如Navigation、List、Scroll、Tabs等可以利用外层或容器自身safeAreaPadding实现扩大裁剪范围等能力。

### 背景图和视频场景

设置背景图、视频组件大小为安全区域大小并配置expandSafeArea属性。

说明

Video组件在使用expandSafeArea扩展到安全区域时，组件视频显示内容区域不支持扩展。

1. // xxx.ets
2. @Entry
3. @Component
4. struct SafeAreaExample1 {
5.   build() {
6.     Stack() {
7.       Image($r('app.media.bg'))
8.         .height('100%').width('100%')
9.         .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM]) // 图片组件的绘制区域扩展至状态栏和导航区域。
10.     }.height('100%').width('100%')
11.   }
12. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.43327826020269771674865794312820:50001231000000:2800:1022E21DA063B1509DB723CB9C69FDA61F3F93D6E7581D7C47F6EA7DAE310B6F.png)

### 滚动类场景

滚动容器设置expandSafeArea属性生效，但当父组件是滚动容器时，子组件设置expandSafeArea属性不生效。对于滚动容器的子组件，有两种方法实现沉浸式效果：

1. 设置父组件滚动容器和子组件相同的背景色，给父组件设置expandSafeArea属性扩展安全区。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct ScrollExample {
    5.   scroller: Scroller = new Scroller()
    6.   private arr: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    7.   build() {
    8.     Stack({ alignContent: Alignment.TopStart }) {
    9.       Scroll(this.scroller) {
    10.         Column() {
    11.           ForEach(this.arr, (item: number) => {
    12.             Stack() {
    13.               Text('Display Content ' + item.toString()).fontSize(30)
    14.             }
    15.             .width('80%').padding(20).borderRadius(15).backgroundColor(Color.White).margin({ top:30, bottom:30 })
    16.           }, (item: string) => item)
    17.         }.width('100%').backgroundColor('rgb(213,213,213)')
    18.       }.backgroundColor('rgb(213,213,213)')
    19.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    20.     }.width('100%').height('100%')
    21.     .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    22.   }
    23. }
    
    **图5** 滚动类容器设置expandSafeArea属性实现沉浸式效果  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.36343620665340982594714223798161:50001231000000:2800:AD6E0F7C59190801230E58A4FFAF23D4F65F1FDE15A3D82DCDAE08D5214E16FC.png)
    
2. 设置父组件滚动容器和子组件相同的背景色，设置滚动容器的内容裁剪属性clipContent(ContentClipMode.SAFE_AREA)，将内容层裁剪区域扩展至避让区。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct ScrollExample {
    5.   scroller: Scroller = new Scroller()
    6.   private arr: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    7.   build() {
    8.     Stack({ alignContent: Alignment.TopStart }) {
    9.       Scroll(this.scroller) {
    10.         Column() {
    11.           ForEach(this.arr, (item: number) => {
    12.             Stack() {
    13.               Text('Display Content ' + item.toString()).fontSize(30)
    14.             }
    15.             .width('80%').padding(20).borderRadius(15).backgroundColor(Color.White).margin({ top:30, bottom:30 })
    16.           }, (item: string) => item)
    17.         }.width('100%').backgroundColor('rgb(213,213,213)')
    18.       }.backgroundColor('rgb(213,213,213)')
    19.       .clipContent(ContentClipMode.SAFE_AREA)
    20.     }.width('100%').height('100%')
    21.   }
    22. }
    

**图6** 滚动类容器设置clipContent属性实现沉浸式效果  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.72942034796131303316500546979165:50001231000000:2800:F0FEA17F4AD3FF502D702340C369F02EFCC501694E07893050822DC1F2ADAEA3.png "点击放大")

### 底部页签场景

要求页签背景色能够延伸到导航区域（此处以导航区域表现为导航条为例给出示意），但页签内部可操作元素需要在导航区域之上。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.37246522656942551464504700503566:50001231000000:2800:F55E4980F4B7D0B0006E3960732E793DA44500BA6386C295E62801FCCCC9C579.png "点击放大")

针对底部的页签部分，Navigation组件和Tabs组件默认实现了页签的延伸处理，开发者只需要保证Navigation和Tabs组件的底部边界和底部导航区域重合即可。若开发者显式调用expandSafeArea接口，则安全区效果由expandSafeArea参数指定。

如果未使用上述组件而是采用自定义方式实现页签的场景，可以针对底部元素设置expandSafeArea属性实现底部元素的背景扩展。

**图7** 顶部和底部UI元素未设置和设置expandSafeArea属性效果对比

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.41747390740743659941506414504724:50001231000000:2800:E50527CF67161602DF8FD0C190F67F7D0B4B3B04CF45C3A0446CC37FE90CC51F.png)

1. // xxx.ets
2. @Entry
3. @Component
4. struct Example {
5.   build() {
6.     Column() {
7.       Row() {
8.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
9.       }.backgroundColor('#2786d9')
10.       // 设置顶部绘制延伸到状态栏
11.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])

12.       Row() {
13.         Text('Display Content 2').fontSize(30)
14.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

15.       Row() {
16.         Text('Display Content 3').fontSize(30)
17.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

18.       Row() {
19.         Text('Display Content 4').fontSize(30)
20.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

21.       Row() {
22.         Text('Display Content 5').fontSize(30)
23.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

24.       Row() {
25.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
26.       }.backgroundColor('#96dffa')
27.       // 设置底部绘制延伸到导航区域
28.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
29.     }
30.     .width('100%').height('100%')
31.     .alignItems(HorizontalAlign.Center)
32.     .backgroundColor('#d5d5d5')
33.     .justifyContent(FlexAlign.SpaceBetween)
34.   }
35. }

### 图文场景

当状态栏元素和底部导航区域元素不同时，无法单纯通过窗口背景色或者背景图组件延伸实现，此时需要对顶部元素和底部元素分别配置expandSafeArea属性，顶部元素配置expandSafeArea([SafeAreaType.SYSTEM],[SafeAreaEdge.TOP])，底部元素配置expandSafeArea([SafeAreaType.SYSTEM],[SafeAreaEdge.BOTTOM])。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.28582942626334677493417993476880:50001231000000:2800:70849062F759622A69E9F0C2E65D297CE52324158491314B545F1CF41A4F9041.png "点击放大")

1. @Entry
2. @Component
3. struct Index {
4.   build() {
5.     Swiper() {
6.       Column() {
7.         Image($r('app.media.start'))
8.           .height('50%').width('100%')
9.           // 设置图片延伸到状态栏
10.           .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])
11.         Column() {
12.           Text('HarmonyOS 第一课')
13.             .fontSize(32)
14.             .margin(30)
15.           Text('通过循序渐进的学习路径，无经验和有经验的开发者都可以掌握ArkTS语言声明式开发范式，体验更简洁、更友好的HarmonyOS应用开发旅程。')
16.             .fontSize(20).margin(20)
17.         }.height('50%').width('100%')
18.         .backgroundColor(Color.White)
19.         // 设置文本内容区背景延伸到导航栏
20.         .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
21.       }
22.     }
23.     .width('100%')
24.     .height('100%')
25.     // 关闭Swiper组件默认的裁切效果以便子节点可以绘制在Swiper外。
26.     .clip(false)
27.   }
28. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-tabs "选项卡 (Tabs)")
# 开发应用沉浸式效果

更新时间: 2025-12-16 16:39

## 概述

典型应用全屏窗口UI元素包括顶部[状态栏](https://developer.huawei.com/consumer/cn/doc/design-guides/status-bar-0000001776775568)、应用界面和底部导航区域（根据用户设置可表现为[导航条](https://developer.huawei.com/consumer/cn/doc/design-guides/navigation-0000001957075737)或三键导航），其中状态栏和导航区域，通常在沉浸式布局下称为避让区；避让区之外的区域称为安全区。开发应用沉浸式效果主要指通过调整状态栏、应用界面和底部导航区域的显示效果来减少状态栏、导航条或三键导航等系统界面的突兀感，从而使用户获得最佳的UI体验。

**图1** 界面元素示意图（此处以导航区域表现为导航条为例给出示意）  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.66183599372440285502873852231614:50001231000000:2800:7913E74432ECA76CC08C129FF68240BE3F1A235F53DBAC59530E070D48BD1C50.png "点击放大")

开发应用沉浸式效果主要要考虑如下几个设计要素：

- UI元素避让处理：底部导航区域可以响应点击事件，除此之外的可交互UI元素和应用关键信息不建议放到导航区域。状态栏显示系统信息，如果与界面元素有冲突，需要考虑避让状态栏。
- 沉浸式效果处理：设置状态栏的颜色和导航区域的显隐与界面元素颜色相匹配，不出现明显的突兀感。

针对上面的设计要求，可以通过如下两种方式实现应用沉浸式效果：

- [窗口全屏布局方案](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section15671730447)：调整布局系统为全屏布局，界面元素延伸到状态栏和导航区域实现沉浸式效果。当不隐藏避让区时，可通过接口查询状态栏和导航区域进行可交互元素避让处理，并设置状态栏或导航区域的颜色或显隐等属性与界面元素匹配。当隐藏避让区时，通过对应接口设置全屏布局即可。
- [组件安全区方案](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section202081847174413)：布局系统保持安全区内布局，然后通过接口延伸绘制内容（如背景色，背景图）到状态栏和导航区域实现沉浸式效果。
    
    该方案下，界面元素仅做绘制延伸，无法单独布局到状态栏和导航区域，针对需要单独布局UI元素到状态栏和导航区域的场景建议使用窗口全屏布局方案处理。
    

## 窗口全屏布局方案

窗口全屏布局方案主要涉及以下[应用扩展布局，全屏显示，不隐藏避让区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section171801550301)和[应用扩展布局，隐藏避让区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section202484117114)两个应用场景。

### 应用扩展布局，全屏显示，不隐藏避让区

可以通过调用窗口强制全屏布局接口[setWindowLayoutFullScreen()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowlayoutfullscreen9)实现界面元素延伸到状态栏和导航区域；然后通过接口[getWindowAvoidArea()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#getwindowavoidarea9)和[on('avoidAreaChange')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowlayoutfullscreen9)获取并动态监听避让区域的变更信息，页面布局根据避让区域信息进行动态调整；设置状态栏或导航区域的颜色或显隐等属性与界面元素进行匹配。

1. 调用setWindowLayoutFullScreen()接口设置窗口全屏。
    
    1. // EntryAbility.ets
    2. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    3. import { window } from '@kit.ArkUI';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
    5. export default class EntryAbility extends UIAbility {
    6.   // ...
    
    7.   onWindowStageCreate(windowStage: window.WindowStage): void {
    8.     windowStage.loadContent('pages/Index', (err, data) => {
    9.       if (err.code) {
    10.         return;
    11.       }
    
    12.       let windowClass: window.Window = windowStage.getMainWindowSync(); // 获取应用主窗口
    13.       // 1. 设置窗口全屏
    14.       let isLayoutFullScreen = true;
    15.       windowClass.setWindowLayoutFullScreen(isLayoutFullScreen).then(() => {
    16.         console.info('Succeeded in setting the window layout to full-screen mode.');
    17.       }).catch((err: BusinessError) => {
    18.         console.error(`Failed to set the window layout to full-screen mode. Code is ${err.code}, message is ${err.message}`);
    19.       });
    20.       // 进行后续步骤2-3中的操作
    21.     });
    22.   }
    23. }
    
2. 使用[getWindowAvoidArea()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#getwindowavoidarea9)接口获取当前布局遮挡区域（此处以状态栏、导航区域为例）。
    
    1. // EntryAbility.ets
    2. // 2. 获取布局避让遮挡的区域
    3. let type = window.AvoidAreaType.TYPE_NAVIGATION_INDICATOR; // 此处以导航条避让为例
    4. let avoidArea = windowClass.getWindowAvoidArea(type);
    5. let bottomRectHeight = avoidArea.bottomRect.height; // 获取到导航区域的高度
    6. AppStorage.setOrCreate('bottomRectHeight', bottomRectHeight);
    
    7. type = window.AvoidAreaType.TYPE_SYSTEM; // 以状态栏避让为例
    8. avoidArea = windowClass.getWindowAvoidArea(type);
    9. let topRectHeight = avoidArea.topRect.height; // 获取状态栏区域高度     
    10. AppStorage.setOrCreate('topRectHeight', topRectHeight);
    
3. 注册监听函数，动态获取避让区域的实时数据。常见的触发避让区回调的场景如下：应用窗口在全屏模式、悬浮模式、分屏模式之间的切换；应用窗口旋转；多折叠设备在屏幕折叠态和展开态之间的切换；应用窗口在多设备之间的流转。
    
    1. // EntryAbility.ets
    2. // 3. 注册监听函数，动态获取避让区域数据
    3. windowClass.on('avoidAreaChange', (data) => {
    4.   if (data.type === window.AvoidAreaType.TYPE_SYSTEM) {
    5.     let topRectHeight = data.area.topRect.height;
    6.     AppStorage.setOrCreate('topRectHeight', topRectHeight);
    7.   } else if (data.type == window.AvoidAreaType.TYPE_NAVIGATION_INDICATOR) {
    8.     let bottomRectHeight = data.area.bottomRect.height;
    9.     AppStorage.setOrCreate('bottomRectHeight', bottomRectHeight);
    10.   }
    11. });
    
4. 布局中的UI元素需要避让状态栏和导航区域，否则可能产生UI元素重叠等情况。
    
    说明
    
    避让区域存在大小为0的情况，当获取到的避让区域为0时，开发者需注意针对性处理适配此时的页面区域和布局，避免贴边、内容裁剪等问题，影响应用界面正常显示或美观性。
    
    如下例子中，对控件顶部设置padding（具体数值与状态栏高度一致），实现对状态栏的避让；对底部设置padding（具体数值与底部导航区域高度一致），实现对导航条的避让。如果去掉顶部和底部的padding设置，即不避让状态栏和导航条，UI元素就会发生重叠。具体可见下文步骤中图2和图3的效果对比。
    
    1. // Index.ets
    2. @Entry
    3. @Component
    4. struct Index {
    5.   @StorageProp('bottomRectHeight')
    6.   bottomRectHeight: number = 0;
    7.   @StorageProp('topRectHeight')
    8.   topRectHeight: number = 0;
    
    9.   build() {
    10.     Column() {
    11.       Row() {
    12.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    13.       }.backgroundColor('#2786d9')
    
    14.       Row() {
    15.         Text('Display Content 2').fontSize(30)
    16.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    17.       Row() {
    18.         Text('Display Content 3').fontSize(30)
    19.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    20.       Row() {
    21.         Text('Display Content 4').fontSize(30)
    22.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    23.       Row() {
    24.         Text('Display Content 5').fontSize(30)
    25.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    26.       Row() {
    27.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    28.       }.backgroundColor('#96dffa')
    29.     }
    30.     .width('100%')
    31.     .height('100%')
    32.     .alignItems(HorizontalAlign.Center)
    33.     .backgroundColor('#d5d5d5')
    34.     .justifyContent(FlexAlign.SpaceBetween)
    35.     // top数值与状态栏区域高度保持一致；bottom数值与导航区域高度保持一致
    36.     .padding({
    37.       top: this.getUIContext().px2vp(this.topRectHeight),
    38.       bottom: this.getUIContext().px2vp(this.bottomRectHeight)
    39.     })
    40.   }
    41. }
    
5. 根据实际的UI界面显示或相关UI元素背景颜色等，还可以按需设置状态栏的文字颜色、背景色或设置导航区域的显示或隐藏，以使UI界面效果呈现和谐。状态栏和导航区域默认是透明的，透传的是应用界面的背景色。
    
    此例中UI颜色主要有两种，比较简单，故未对状态栏文字颜色、背景色进行设置，未对导航区域进行隐藏。
    
    **图2** 布局避让状态栏和导航区域（此处以导航区域表现为导航条为例给出示意）  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.87006013163778539261709498662392:50001231000000:2800:A746E4D652D3D20AA672A5BF165B3699C55DC9456E44001D102D538ACD77E72B.jpg "点击放大")
    
    **图3** 布局未避让状态栏和导航区域，UI元素重叠（此处以导航区域表现为导航条为例给出示意）  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.57353412750221239108308721929172:50001231000000:2800:648A1F02A8BC0F5532422C2B618955F93999C9C2477489BA8D5714D235BF32FC.jpg "点击放大")
    

### 应用扩展布局，隐藏避让区

此场景下状态栏和导航区域需要隐藏，适用于游戏、电影等应用场景。用户可以通过从底部上滑唤出导航条或三键导航。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.99837954210435397706545783363927:50001231000000:2800:E0DDA552D6BF528E237CF861592011D02174A684C85AF203C34ACA45490F2C88.png "点击放大")

1. 调用setWindowLayoutFullScreen()接口设置窗口全屏。
    
    1. // EntryAbility.ets
    2. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    3. import { window } from '@kit.ArkUI';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
    5. export default class EntryAbility extends UIAbility {
    6.   // ...
    
    7.   onWindowStageCreate(windowStage: window.WindowStage): void {
    8.     windowStage.loadContent('pages/Index', (err, data) => {
    9.       if (err.code) {
    10.         return;
    11.       }
    
    12.       let windowClass: window.Window = windowStage.getMainWindowSync(); // 获取应用主窗口
    13.       // 1. 设置窗口全屏
    14.       let isLayoutFullScreen = true;
    15.       windowClass.setWindowLayoutFullScreen(isLayoutFullScreen).then(() => {
    16.         console.info('Succeeded in setting the window layout to full-screen mode.');
    17.       }).catch((err: BusinessError) => {
    18.         console.error(`Failed to set the window layout to full-screen mode. Code is ${err.code}, message is ${err.message}`);
    19.       });
    20.       // 进行后续步骤2中的状态栏和导航区域的隐藏操作
    21.     });
    22.   }
    23. }
    
2. 调用[setSpecificSystemBarEnabled()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setspecificsystembarenabled11)接口设置状态栏和导航区域的具体显隐状态，此场景下将其设置为隐藏。
    
    1. // EntryAbility.ets
    2. // 2. 设置状态栏隐藏
    3. windowClass.setSpecificSystemBarEnabled('status', false).then(() => {
    4.   console.info('Succeeded in setting the status bar to be invisible.');
    5. }).catch((err: BusinessError) => {
    6.   console.error(`Failed to set the status bar to be invisible. Code is ${err.code}, message is ${err.message}`);
    7. });
    8. // 2. 设置导航区域隐藏
    9. windowClass.setSpecificSystemBarEnabled('navigationIndicator', false).then(() => {
    10.   console.info('Succeeded in setting the navigation indicator to be invisible.');
    11. }).catch((err: BusinessError) => {
    12.   console.error(`Failed to set the navigation indicator to be invisible. Code is ${err.code}, message is ${err.message}`);
    13. });
    
3. 在界面中无需进行导航区域避让操作。
    
    1. // Index.ets
    2. @Entry()
    3. @Component
    4. struct Index {
    5.   build() {
    6.     Row() {
    7.       Column() {
    8.         Row() {
    9.           Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    10.         }.backgroundColor('#2786d9')
    
    11.         Row() {
    12.           Text('Display Content 2').fontSize(30)
    13.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    14.         Row() {
    15.           Text('Display Content 3').fontSize(30)
    16.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    17.         Row() {
    18.           Text('Display Content 4').fontSize(30)
    19.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    20.         Row() {
    21.           Text('Display Content 5').fontSize(30)
    22.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    23.         Row() {
    24.           Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    25.         }.backgroundColor('#96dffa')
    26.       }
    27.       .width('100%')
    28.       .height('100%')
    29.       .alignItems(HorizontalAlign.Center)
    30.       .justifyContent(FlexAlign.SpaceBetween)
    31.       .backgroundColor('#d5d5d5')
    32.     }
    33.   }
    34. }
    

## 组件安全区方案

应用未使用setWindowLayoutFullScreen()接口设置窗口全屏布局时，默认采取组件安全区布局方案。

应用在默认情况下窗口背景绘制范围是全屏，但UI元素被限制在安全区内（自动排除状态栏和导航区域）进行布局，来避免界面元素被状态栏和导航区域遮盖。

**图4** 界面元素自动避让状态栏和导航区域示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.49785881633116705159423116990391:50001231000000:2800:B33C69BC76D51355EC3CAE2413AEFC2778B11EF1DE34BF763C3215C43D52EEA0.png "点击放大")

针对状态栏和导航区域颜色与界面元素颜色不匹配问题，可以通过如下两种方式实现沉浸式效果：

- 状态栏和导航区域颜色相同场景，可以通过设置窗口的背景色来实现沉浸式效果。窗口背景色可通过[setWindowBackgroundColor()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowbackgroundcolor9)进行设置。
    
    1. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    2. import { window } from '@kit.ArkUI';
    
    3. export default class EntryAbility extends UIAbility {
    4.   //...
    
    5.   onWindowStageCreate(windowStage: window.WindowStage): void {
    6.     windowStage.loadContent('pages/Index', (err) => {
    7.       if (err.code) {
    8.         return;
    9.       }
    
    10.       // 设置全窗颜色和应用元素颜色一致
    11.       windowStage.getMainWindowSync().setWindowBackgroundColor('#d5d5d5');
    12.     });
    13.   }
    14. }
    
    界面状态栏和导航区域颜色相同场景。
    
    15. // xxx.ets
    16. @Entry
    17. @Component
    18. struct Example {
    19.   build() {
    20.     Column() {
    21.       Row() {
    22.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    23.       }.backgroundColor('#2786d9')
    
    24.       Row() {
    25.         Text('Display Content 2').fontSize(30)
    26.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    27.       Row() {
    28.         Text('Display Content 3').fontSize(30)
    29.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    30.       Row() {
    31.         Text('Display Content 4').fontSize(30)
    32.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    33.       Row() {
    34.         Text('Display Content 5').fontSize(30)
    35.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    36.       Row() {
    37.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    38.       }.backgroundColor('#96dffa')
    39.     }
    40.     .width('100%').height('100%')
    41.     .alignItems(HorizontalAlign.Center)
    42.     .backgroundColor('#d5d5d5')
    43.     .justifyContent(FlexAlign.SpaceBetween)
    44.   }
    45. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.48684961595489300477977200533131:50001231000000:2800:4DB5CDA0E0D7958CB4FB8E8AEC3D5128DD0539822614E9C3C8FD853148872890.png)
    
- 状态栏和导航区域颜色不同时，可以使用[expandSafeArea](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-expand-safe-area#expandsafearea)属性扩展安全区域属性进行调整。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct Example {
    5.   build() {
    6.     Column() {
    7.       Row() {
    8.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    9.       }.backgroundColor('#2786d9')
    10.       // 设置顶部绘制延伸到状态栏
    11.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])
    
    12.       Row() {
    13.         Text('Display Content 2').fontSize(30)
    14.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    15.       Row() {
    16.         Text('Display Content 3').fontSize(30)
    17.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    18.       Row() {
    19.         Text('Display Content 4').fontSize(30)
    20.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    21.       Row() {
    22.         Text('Display Content 5').fontSize(30)
    23.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    24.       Row() {
    25.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    26.       }.backgroundColor('#96dffa')
    27.       // 设置底部绘制延伸到导航区域
    28.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
    29.     }
    30.     .width('100%').height('100%')
    31.     .alignItems(HorizontalAlign.Center)
    32.     .backgroundColor('#d5d5d5')
    33.     .justifyContent(FlexAlign.SpaceBetween)
    34.   }
    35. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.75061394560447074198529736772042:50001231000000:2800:902E75D5CF9C4DD79174E234EDE65E52140DEE800228E4183BD6AB6FD0CFA27E.png)
    

### 扩展安全区域属性原理

- 布局阶段按照安全区范围大小进行UI元素布局。
- 布局完成后查看设置了expandSafeArea的组件边界（不包括margin）是否和安全区边界相交。
- 如果设置了expandSafeArea的组件和安全区边界相交，根据expandSafeArea传递的属性则进一步扩大组件绘制区域大小覆盖状态栏、导航区域这些非安全区域。
- 上述过程仅改变组件自身绘制大小，不进行二次布局，不影响子节点和兄弟节点的大小和位置。
- 子节点可以单独设置该属性，只需要自身边界和安全区域重合就可以延伸自身大小至非安全区域内，需要确保父组件未设置clip等裁切属性。
- 配置expandSafeArea属性组件进行绘制扩展时，需要关注组件不能配置固定宽高尺寸，百分比除外。
- 组件可以设置通用属性safeAreaPadding，给自身添加组件级安全区域。该属性作为一种特殊边距，在提供布局约束的同时作为安全区可以被一些系统组件利用。
    - safeAreaPadding位于原有的padding内侧。容器自外向内各层分别为border、padding、safeAreaPadding、内容区。当border和padding确定后，若容器可用空间不足以满足safeAreaPadding的设置，则优先分配给左侧和上侧safeAreaPadding、其次分配给右侧和下侧safeAreaPadding。safeAreaPadding实际尺寸确定后，余下空间为内容区。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.40814739523074922976450985656583:50001231000000:2800:3069DA8848E75088A5E18CA4DEFE8D5B560459053EC369BEE936096F37485126.png "点击放大")
        
    - 系统组件如Navigation、List、Scroll、Tabs等可以利用外层或容器自身safeAreaPadding实现扩大裁剪范围等能力。

### 背景图和视频场景

设置背景图、视频组件大小为安全区域大小并配置expandSafeArea属性。

说明

Video组件在使用expandSafeArea扩展到安全区域时，组件视频显示内容区域不支持扩展。

1. // xxx.ets
2. @Entry
3. @Component
4. struct SafeAreaExample1 {
5.   build() {
6.     Stack() {
7.       Image($r('app.media.bg'))
8.         .height('100%').width('100%')
9.         .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM]) // 图片组件的绘制区域扩展至状态栏和导航区域。
10.     }.height('100%').width('100%')
11.   }
12. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.43327826020269771674865794312820:50001231000000:2800:1022E21DA063B1509DB723CB9C69FDA61F3F93D6E7581D7C47F6EA7DAE310B6F.png)

### 滚动类场景

滚动容器设置expandSafeArea属性生效，但当父组件是滚动容器时，子组件设置expandSafeArea属性不生效。对于滚动容器的子组件，有两种方法实现沉浸式效果：

1. 设置父组件滚动容器和子组件相同的背景色，给父组件设置expandSafeArea属性扩展安全区。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct ScrollExample {
    5.   scroller: Scroller = new Scroller()
    6.   private arr: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    7.   build() {
    8.     Stack({ alignContent: Alignment.TopStart }) {
    9.       Scroll(this.scroller) {
    10.         Column() {
    11.           ForEach(this.arr, (item: number) => {
    12.             Stack() {
    13.               Text('Display Content ' + item.toString()).fontSize(30)
    14.             }
    15.             .width('80%').padding(20).borderRadius(15).backgroundColor(Color.White).margin({ top:30, bottom:30 })
    16.           }, (item: string) => item)
    17.         }.width('100%').backgroundColor('rgb(213,213,213)')
    18.       }.backgroundColor('rgb(213,213,213)')
    19.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    20.     }.width('100%').height('100%')
    21.     .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    22.   }
    23. }
    
    **图5** 滚动类容器设置expandSafeArea属性实现沉浸式效果  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.36343620665340982594714223798161:50001231000000:2800:AD6E0F7C59190801230E58A4FFAF23D4F65F1FDE15A3D82DCDAE08D5214E16FC.png)
    
2. 设置父组件滚动容器和子组件相同的背景色，设置滚动容器的内容裁剪属性clipContent(ContentClipMode.SAFE_AREA)，将内容层裁剪区域扩展至避让区。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct ScrollExample {
    5.   scroller: Scroller = new Scroller()
    6.   private arr: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    7.   build() {
    8.     Stack({ alignContent: Alignment.TopStart }) {
    9.       Scroll(this.scroller) {
    10.         Column() {
    11.           ForEach(this.arr, (item: number) => {
    12.             Stack() {
    13.               Text('Display Content ' + item.toString()).fontSize(30)
    14.             }
    15.             .width('80%').padding(20).borderRadius(15).backgroundColor(Color.White).margin({ top:30, bottom:30 })
    16.           }, (item: string) => item)
    17.         }.width('100%').backgroundColor('rgb(213,213,213)')
    18.       }.backgroundColor('rgb(213,213,213)')
    19.       .clipContent(ContentClipMode.SAFE_AREA)
    20.     }.width('100%').height('100%')
    21.   }
    22. }
    

**图6** 滚动类容器设置clipContent属性实现沉浸式效果  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.72942034796131303316500546979165:50001231000000:2800:F0FEA17F4AD3FF502D702340C369F02EFCC501694E07893050822DC1F2ADAEA3.png "点击放大")

### 底部页签场景

要求页签背景色能够延伸到导航区域（此处以导航区域表现为导航条为例给出示意），但页签内部可操作元素需要在导航区域之上。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.37246522656942551464504700503566:50001231000000:2800:F55E4980F4B7D0B0006E3960732E793DA44500BA6386C295E62801FCCCC9C579.png "点击放大")

针对底部的页签部分，Navigation组件和Tabs组件默认实现了页签的延伸处理，开发者只需要保证Navigation和Tabs组件的底部边界和底部导航区域重合即可。若开发者显式调用expandSafeArea接口，则安全区效果由expandSafeArea参数指定。

如果未使用上述组件而是采用自定义方式实现页签的场景，可以针对底部元素设置expandSafeArea属性实现底部元素的背景扩展。

**图7** 顶部和底部UI元素未设置和设置expandSafeArea属性效果对比

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.41747390740743659941506414504724:50001231000000:2800:E50527CF67161602DF8FD0C190F67F7D0B4B3B04CF45C3A0446CC37FE90CC51F.png)

1. // xxx.ets
2. @Entry
3. @Component
4. struct Example {
5.   build() {
6.     Column() {
7.       Row() {
8.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
9.       }.backgroundColor('#2786d9')
10.       // 设置顶部绘制延伸到状态栏
11.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])

12.       Row() {
13.         Text('Display Content 2').fontSize(30)
14.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

15.       Row() {
16.         Text('Display Content 3').fontSize(30)
17.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

18.       Row() {
19.         Text('Display Content 4').fontSize(30)
20.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

21.       Row() {
22.         Text('Display Content 5').fontSize(30)
23.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

24.       Row() {
25.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
26.       }.backgroundColor('#96dffa')
27.       // 设置底部绘制延伸到导航区域
28.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
29.     }
30.     .width('100%').height('100%')
31.     .alignItems(HorizontalAlign.Center)
32.     .backgroundColor('#d5d5d5')
33.     .justifyContent(FlexAlign.SpaceBetween)
34.   }
35. }

### 图文场景

当状态栏元素和底部导航区域元素不同时，无法单纯通过窗口背景色或者背景图组件延伸实现，此时需要对顶部元素和底部元素分别配置expandSafeArea属性，顶部元素配置expandSafeArea([SafeAreaType.SYSTEM],[SafeAreaEdge.TOP])，底部元素配置expandSafeArea([SafeAreaType.SYSTEM],[SafeAreaEdge.BOTTOM])。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.28582942626334677493417993476880:50001231000000:2800:70849062F759622A69E9F0C2E65D297CE52324158491314B545F1CF41A4F9041.png "点击放大")

1. @Entry
2. @Component
3. struct Index {
4.   build() {
5.     Swiper() {
6.       Column() {
7.         Image($r('app.media.start'))
8.           .height('50%').width('100%')
9.           // 设置图片延伸到状态栏
10.           .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])
11.         Column() {
12.           Text('HarmonyOS 第一课')
13.             .fontSize(32)
14.             .margin(30)
15.           Text('通过循序渐进的学习路径，无经验和有经验的开发者都可以掌握ArkTS语言声明式开发范式，体验更简洁、更友好的HarmonyOS应用开发旅程。')
16.             .fontSize(20).margin(20)
17.         }.height('50%').width('100%')
18.         .backgroundColor(Color.White)
19.         // 设置文本内容区背景延伸到导航栏
20.         .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
21.       }
22.     }
23.     .width('100%')
24.     .height('100%')
25.     // 关闭Swiper组件默认的裁切效果以便子节点可以绘制在Swiper外。
26.     .clip(false)
27.   }
28. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-tabs "选项卡 (Tabs)")
# 开发应用沉浸式效果

更新时间: 2025-12-16 16:39

## 概述

典型应用全屏窗口UI元素包括顶部[状态栏](https://developer.huawei.com/consumer/cn/doc/design-guides/status-bar-0000001776775568)、应用界面和底部导航区域（根据用户设置可表现为[导航条](https://developer.huawei.com/consumer/cn/doc/design-guides/navigation-0000001957075737)或三键导航），其中状态栏和导航区域，通常在沉浸式布局下称为避让区；避让区之外的区域称为安全区。开发应用沉浸式效果主要指通过调整状态栏、应用界面和底部导航区域的显示效果来减少状态栏、导航条或三键导航等系统界面的突兀感，从而使用户获得最佳的UI体验。

**图1** 界面元素示意图（此处以导航区域表现为导航条为例给出示意）  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.66183599372440285502873852231614:50001231000000:2800:7913E74432ECA76CC08C129FF68240BE3F1A235F53DBAC59530E070D48BD1C50.png "点击放大")

开发应用沉浸式效果主要要考虑如下几个设计要素：

- UI元素避让处理：底部导航区域可以响应点击事件，除此之外的可交互UI元素和应用关键信息不建议放到导航区域。状态栏显示系统信息，如果与界面元素有冲突，需要考虑避让状态栏。
- 沉浸式效果处理：设置状态栏的颜色和导航区域的显隐与界面元素颜色相匹配，不出现明显的突兀感。

针对上面的设计要求，可以通过如下两种方式实现应用沉浸式效果：

- [窗口全屏布局方案](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section15671730447)：调整布局系统为全屏布局，界面元素延伸到状态栏和导航区域实现沉浸式效果。当不隐藏避让区时，可通过接口查询状态栏和导航区域进行可交互元素避让处理，并设置状态栏或导航区域的颜色或显隐等属性与界面元素匹配。当隐藏避让区时，通过对应接口设置全屏布局即可。
- [组件安全区方案](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section202081847174413)：布局系统保持安全区内布局，然后通过接口延伸绘制内容（如背景色，背景图）到状态栏和导航区域实现沉浸式效果。
    
    该方案下，界面元素仅做绘制延伸，无法单独布局到状态栏和导航区域，针对需要单独布局UI元素到状态栏和导航区域的场景建议使用窗口全屏布局方案处理。
    

## 窗口全屏布局方案

窗口全屏布局方案主要涉及以下[应用扩展布局，全屏显示，不隐藏避让区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section171801550301)和[应用扩展布局，隐藏避让区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects#section202484117114)两个应用场景。

### 应用扩展布局，全屏显示，不隐藏避让区

可以通过调用窗口强制全屏布局接口[setWindowLayoutFullScreen()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowlayoutfullscreen9)实现界面元素延伸到状态栏和导航区域；然后通过接口[getWindowAvoidArea()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#getwindowavoidarea9)和[on('avoidAreaChange')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowlayoutfullscreen9)获取并动态监听避让区域的变更信息，页面布局根据避让区域信息进行动态调整；设置状态栏或导航区域的颜色或显隐等属性与界面元素进行匹配。

1. 调用setWindowLayoutFullScreen()接口设置窗口全屏。
    
    1. // EntryAbility.ets
    2. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    3. import { window } from '@kit.ArkUI';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
    5. export default class EntryAbility extends UIAbility {
    6.   // ...
    
    7.   onWindowStageCreate(windowStage: window.WindowStage): void {
    8.     windowStage.loadContent('pages/Index', (err, data) => {
    9.       if (err.code) {
    10.         return;
    11.       }
    
    12.       let windowClass: window.Window = windowStage.getMainWindowSync(); // 获取应用主窗口
    13.       // 1. 设置窗口全屏
    14.       let isLayoutFullScreen = true;
    15.       windowClass.setWindowLayoutFullScreen(isLayoutFullScreen).then(() => {
    16.         console.info('Succeeded in setting the window layout to full-screen mode.');
    17.       }).catch((err: BusinessError) => {
    18.         console.error(`Failed to set the window layout to full-screen mode. Code is ${err.code}, message is ${err.message}`);
    19.       });
    20.       // 进行后续步骤2-3中的操作
    21.     });
    22.   }
    23. }
    
2. 使用[getWindowAvoidArea()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#getwindowavoidarea9)接口获取当前布局遮挡区域（此处以状态栏、导航区域为例）。
    
    1. // EntryAbility.ets
    2. // 2. 获取布局避让遮挡的区域
    3. let type = window.AvoidAreaType.TYPE_NAVIGATION_INDICATOR; // 此处以导航条避让为例
    4. let avoidArea = windowClass.getWindowAvoidArea(type);
    5. let bottomRectHeight = avoidArea.bottomRect.height; // 获取到导航区域的高度
    6. AppStorage.setOrCreate('bottomRectHeight', bottomRectHeight);
    
    7. type = window.AvoidAreaType.TYPE_SYSTEM; // 以状态栏避让为例
    8. avoidArea = windowClass.getWindowAvoidArea(type);
    9. let topRectHeight = avoidArea.topRect.height; // 获取状态栏区域高度     
    10. AppStorage.setOrCreate('topRectHeight', topRectHeight);
    
3. 注册监听函数，动态获取避让区域的实时数据。常见的触发避让区回调的场景如下：应用窗口在全屏模式、悬浮模式、分屏模式之间的切换；应用窗口旋转；多折叠设备在屏幕折叠态和展开态之间的切换；应用窗口在多设备之间的流转。
    
    1. // EntryAbility.ets
    2. // 3. 注册监听函数，动态获取避让区域数据
    3. windowClass.on('avoidAreaChange', (data) => {
    4.   if (data.type === window.AvoidAreaType.TYPE_SYSTEM) {
    5.     let topRectHeight = data.area.topRect.height;
    6.     AppStorage.setOrCreate('topRectHeight', topRectHeight);
    7.   } else if (data.type == window.AvoidAreaType.TYPE_NAVIGATION_INDICATOR) {
    8.     let bottomRectHeight = data.area.bottomRect.height;
    9.     AppStorage.setOrCreate('bottomRectHeight', bottomRectHeight);
    10.   }
    11. });
    
4. 布局中的UI元素需要避让状态栏和导航区域，否则可能产生UI元素重叠等情况。
    
    说明
    
    避让区域存在大小为0的情况，当获取到的避让区域为0时，开发者需注意针对性处理适配此时的页面区域和布局，避免贴边、内容裁剪等问题，影响应用界面正常显示或美观性。
    
    如下例子中，对控件顶部设置padding（具体数值与状态栏高度一致），实现对状态栏的避让；对底部设置padding（具体数值与底部导航区域高度一致），实现对导航条的避让。如果去掉顶部和底部的padding设置，即不避让状态栏和导航条，UI元素就会发生重叠。具体可见下文步骤中图2和图3的效果对比。
    
    1. // Index.ets
    2. @Entry
    3. @Component
    4. struct Index {
    5.   @StorageProp('bottomRectHeight')
    6.   bottomRectHeight: number = 0;
    7.   @StorageProp('topRectHeight')
    8.   topRectHeight: number = 0;
    
    9.   build() {
    10.     Column() {
    11.       Row() {
    12.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    13.       }.backgroundColor('#2786d9')
    
    14.       Row() {
    15.         Text('Display Content 2').fontSize(30)
    16.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    17.       Row() {
    18.         Text('Display Content 3').fontSize(30)
    19.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    20.       Row() {
    21.         Text('Display Content 4').fontSize(30)
    22.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    23.       Row() {
    24.         Text('Display Content 5').fontSize(30)
    25.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    26.       Row() {
    27.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    28.       }.backgroundColor('#96dffa')
    29.     }
    30.     .width('100%')
    31.     .height('100%')
    32.     .alignItems(HorizontalAlign.Center)
    33.     .backgroundColor('#d5d5d5')
    34.     .justifyContent(FlexAlign.SpaceBetween)
    35.     // top数值与状态栏区域高度保持一致；bottom数值与导航区域高度保持一致
    36.     .padding({
    37.       top: this.getUIContext().px2vp(this.topRectHeight),
    38.       bottom: this.getUIContext().px2vp(this.bottomRectHeight)
    39.     })
    40.   }
    41. }
    
5. 根据实际的UI界面显示或相关UI元素背景颜色等，还可以按需设置状态栏的文字颜色、背景色或设置导航区域的显示或隐藏，以使UI界面效果呈现和谐。状态栏和导航区域默认是透明的，透传的是应用界面的背景色。
    
    此例中UI颜色主要有两种，比较简单，故未对状态栏文字颜色、背景色进行设置，未对导航区域进行隐藏。
    
    **图2** 布局避让状态栏和导航区域（此处以导航区域表现为导航条为例给出示意）  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.87006013163778539261709498662392:50001231000000:2800:A746E4D652D3D20AA672A5BF165B3699C55DC9456E44001D102D538ACD77E72B.jpg "点击放大")
    
    **图3** 布局未避让状态栏和导航区域，UI元素重叠（此处以导航区域表现为导航条为例给出示意）  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.57353412750221239108308721929172:50001231000000:2800:648A1F02A8BC0F5532422C2B618955F93999C9C2477489BA8D5714D235BF32FC.jpg "点击放大")
    

### 应用扩展布局，隐藏避让区

此场景下状态栏和导航区域需要隐藏，适用于游戏、电影等应用场景。用户可以通过从底部上滑唤出导航条或三键导航。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.99837954210435397706545783363927:50001231000000:2800:E0DDA552D6BF528E237CF861592011D02174A684C85AF203C34ACA45490F2C88.png "点击放大")

1. 调用setWindowLayoutFullScreen()接口设置窗口全屏。
    
    1. // EntryAbility.ets
    2. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    3. import { window } from '@kit.ArkUI';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
    5. export default class EntryAbility extends UIAbility {
    6.   // ...
    
    7.   onWindowStageCreate(windowStage: window.WindowStage): void {
    8.     windowStage.loadContent('pages/Index', (err, data) => {
    9.       if (err.code) {
    10.         return;
    11.       }
    
    12.       let windowClass: window.Window = windowStage.getMainWindowSync(); // 获取应用主窗口
    13.       // 1. 设置窗口全屏
    14.       let isLayoutFullScreen = true;
    15.       windowClass.setWindowLayoutFullScreen(isLayoutFullScreen).then(() => {
    16.         console.info('Succeeded in setting the window layout to full-screen mode.');
    17.       }).catch((err: BusinessError) => {
    18.         console.error(`Failed to set the window layout to full-screen mode. Code is ${err.code}, message is ${err.message}`);
    19.       });
    20.       // 进行后续步骤2中的状态栏和导航区域的隐藏操作
    21.     });
    22.   }
    23. }
    
2. 调用[setSpecificSystemBarEnabled()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setspecificsystembarenabled11)接口设置状态栏和导航区域的具体显隐状态，此场景下将其设置为隐藏。
    
    1. // EntryAbility.ets
    2. // 2. 设置状态栏隐藏
    3. windowClass.setSpecificSystemBarEnabled('status', false).then(() => {
    4.   console.info('Succeeded in setting the status bar to be invisible.');
    5. }).catch((err: BusinessError) => {
    6.   console.error(`Failed to set the status bar to be invisible. Code is ${err.code}, message is ${err.message}`);
    7. });
    8. // 2. 设置导航区域隐藏
    9. windowClass.setSpecificSystemBarEnabled('navigationIndicator', false).then(() => {
    10.   console.info('Succeeded in setting the navigation indicator to be invisible.');
    11. }).catch((err: BusinessError) => {
    12.   console.error(`Failed to set the navigation indicator to be invisible. Code is ${err.code}, message is ${err.message}`);
    13. });
    
3. 在界面中无需进行导航区域避让操作。
    
    1. // Index.ets
    2. @Entry()
    3. @Component
    4. struct Index {
    5.   build() {
    6.     Row() {
    7.       Column() {
    8.         Row() {
    9.           Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    10.         }.backgroundColor('#2786d9')
    
    11.         Row() {
    12.           Text('Display Content 2').fontSize(30)
    13.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    14.         Row() {
    15.           Text('Display Content 3').fontSize(30)
    16.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    17.         Row() {
    18.           Text('Display Content 4').fontSize(30)
    19.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    20.         Row() {
    21.           Text('Display Content 5').fontSize(30)
    22.         }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    23.         Row() {
    24.           Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    25.         }.backgroundColor('#96dffa')
    26.       }
    27.       .width('100%')
    28.       .height('100%')
    29.       .alignItems(HorizontalAlign.Center)
    30.       .justifyContent(FlexAlign.SpaceBetween)
    31.       .backgroundColor('#d5d5d5')
    32.     }
    33.   }
    34. }
    

## 组件安全区方案

应用未使用setWindowLayoutFullScreen()接口设置窗口全屏布局时，默认采取组件安全区布局方案。

应用在默认情况下窗口背景绘制范围是全屏，但UI元素被限制在安全区内（自动排除状态栏和导航区域）进行布局，来避免界面元素被状态栏和导航区域遮盖。

**图4** 界面元素自动避让状态栏和导航区域示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.49785881633116705159423116990391:50001231000000:2800:B33C69BC76D51355EC3CAE2413AEFC2778B11EF1DE34BF763C3215C43D52EEA0.png "点击放大")

针对状态栏和导航区域颜色与界面元素颜色不匹配问题，可以通过如下两种方式实现沉浸式效果：

- 状态栏和导航区域颜色相同场景，可以通过设置窗口的背景色来实现沉浸式效果。窗口背景色可通过[setWindowBackgroundColor()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowbackgroundcolor9)进行设置。
    
    1. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    2. import { window } from '@kit.ArkUI';
    
    3. export default class EntryAbility extends UIAbility {
    4.   //...
    
    5.   onWindowStageCreate(windowStage: window.WindowStage): void {
    6.     windowStage.loadContent('pages/Index', (err) => {
    7.       if (err.code) {
    8.         return;
    9.       }
    
    10.       // 设置全窗颜色和应用元素颜色一致
    11.       windowStage.getMainWindowSync().setWindowBackgroundColor('#d5d5d5');
    12.     });
    13.   }
    14. }
    
    界面状态栏和导航区域颜色相同场景。
    
    15. // xxx.ets
    16. @Entry
    17. @Component
    18. struct Example {
    19.   build() {
    20.     Column() {
    21.       Row() {
    22.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    23.       }.backgroundColor('#2786d9')
    
    24.       Row() {
    25.         Text('Display Content 2').fontSize(30)
    26.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    27.       Row() {
    28.         Text('Display Content 3').fontSize(30)
    29.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    30.       Row() {
    31.         Text('Display Content 4').fontSize(30)
    32.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    33.       Row() {
    34.         Text('Display Content 5').fontSize(30)
    35.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    36.       Row() {
    37.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    38.       }.backgroundColor('#96dffa')
    39.     }
    40.     .width('100%').height('100%')
    41.     .alignItems(HorizontalAlign.Center)
    42.     .backgroundColor('#d5d5d5')
    43.     .justifyContent(FlexAlign.SpaceBetween)
    44.   }
    45. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163937.48684961595489300477977200533131:50001231000000:2800:4DB5CDA0E0D7958CB4FB8E8AEC3D5128DD0539822614E9C3C8FD853148872890.png)
    
- 状态栏和导航区域颜色不同时，可以使用[expandSafeArea](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-expand-safe-area#expandsafearea)属性扩展安全区域属性进行调整。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct Example {
    5.   build() {
    6.     Column() {
    7.       Row() {
    8.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    9.       }.backgroundColor('#2786d9')
    10.       // 设置顶部绘制延伸到状态栏
    11.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])
    
    12.       Row() {
    13.         Text('Display Content 2').fontSize(30)
    14.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    15.       Row() {
    16.         Text('Display Content 3').fontSize(30)
    17.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    18.       Row() {
    19.         Text('Display Content 4').fontSize(30)
    20.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    21.       Row() {
    22.         Text('Display Content 5').fontSize(30)
    23.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')
    
    24.       Row() {
    25.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
    26.       }.backgroundColor('#96dffa')
    27.       // 设置底部绘制延伸到导航区域
    28.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
    29.     }
    30.     .width('100%').height('100%')
    31.     .alignItems(HorizontalAlign.Center)
    32.     .backgroundColor('#d5d5d5')
    33.     .justifyContent(FlexAlign.SpaceBetween)
    34.   }
    35. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.75061394560447074198529736772042:50001231000000:2800:902E75D5CF9C4DD79174E234EDE65E52140DEE800228E4183BD6AB6FD0CFA27E.png)
    

### 扩展安全区域属性原理

- 布局阶段按照安全区范围大小进行UI元素布局。
- 布局完成后查看设置了expandSafeArea的组件边界（不包括margin）是否和安全区边界相交。
- 如果设置了expandSafeArea的组件和安全区边界相交，根据expandSafeArea传递的属性则进一步扩大组件绘制区域大小覆盖状态栏、导航区域这些非安全区域。
- 上述过程仅改变组件自身绘制大小，不进行二次布局，不影响子节点和兄弟节点的大小和位置。
- 子节点可以单独设置该属性，只需要自身边界和安全区域重合就可以延伸自身大小至非安全区域内，需要确保父组件未设置clip等裁切属性。
- 配置expandSafeArea属性组件进行绘制扩展时，需要关注组件不能配置固定宽高尺寸，百分比除外。
- 组件可以设置通用属性safeAreaPadding，给自身添加组件级安全区域。该属性作为一种特殊边距，在提供布局约束的同时作为安全区可以被一些系统组件利用。
    - safeAreaPadding位于原有的padding内侧。容器自外向内各层分别为border、padding、safeAreaPadding、内容区。当border和padding确定后，若容器可用空间不足以满足safeAreaPadding的设置，则优先分配给左侧和上侧safeAreaPadding、其次分配给右侧和下侧safeAreaPadding。safeAreaPadding实际尺寸确定后，余下空间为内容区。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.40814739523074922976450985656583:50001231000000:2800:3069DA8848E75088A5E18CA4DEFE8D5B560459053EC369BEE936096F37485126.png "点击放大")
        
    - 系统组件如Navigation、List、Scroll、Tabs等可以利用外层或容器自身safeAreaPadding实现扩大裁剪范围等能力。

### 背景图和视频场景

设置背景图、视频组件大小为安全区域大小并配置expandSafeArea属性。

说明

Video组件在使用expandSafeArea扩展到安全区域时，组件视频显示内容区域不支持扩展。

1. // xxx.ets
2. @Entry
3. @Component
4. struct SafeAreaExample1 {
5.   build() {
6.     Stack() {
7.       Image($r('app.media.bg'))
8.         .height('100%').width('100%')
9.         .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM]) // 图片组件的绘制区域扩展至状态栏和导航区域。
10.     }.height('100%').width('100%')
11.   }
12. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.43327826020269771674865794312820:50001231000000:2800:1022E21DA063B1509DB723CB9C69FDA61F3F93D6E7581D7C47F6EA7DAE310B6F.png)

### 滚动类场景

滚动容器设置expandSafeArea属性生效，但当父组件是滚动容器时，子组件设置expandSafeArea属性不生效。对于滚动容器的子组件，有两种方法实现沉浸式效果：

1. 设置父组件滚动容器和子组件相同的背景色，给父组件设置expandSafeArea属性扩展安全区。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct ScrollExample {
    5.   scroller: Scroller = new Scroller()
    6.   private arr: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    7.   build() {
    8.     Stack({ alignContent: Alignment.TopStart }) {
    9.       Scroll(this.scroller) {
    10.         Column() {
    11.           ForEach(this.arr, (item: number) => {
    12.             Stack() {
    13.               Text('Display Content ' + item.toString()).fontSize(30)
    14.             }
    15.             .width('80%').padding(20).borderRadius(15).backgroundColor(Color.White).margin({ top:30, bottom:30 })
    16.           }, (item: string) => item)
    17.         }.width('100%').backgroundColor('rgb(213,213,213)')
    18.       }.backgroundColor('rgb(213,213,213)')
    19.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    20.     }.width('100%').height('100%')
    21.     .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    22.   }
    23. }
    
    **图5** 滚动类容器设置expandSafeArea属性实现沉浸式效果  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.36343620665340982594714223798161:50001231000000:2800:AD6E0F7C59190801230E58A4FFAF23D4F65F1FDE15A3D82DCDAE08D5214E16FC.png)
    
2. 设置父组件滚动容器和子组件相同的背景色，设置滚动容器的内容裁剪属性clipContent(ContentClipMode.SAFE_AREA)，将内容层裁剪区域扩展至避让区。
    
    1. // xxx.ets
    2. @Entry
    3. @Component
    4. struct ScrollExample {
    5.   scroller: Scroller = new Scroller()
    6.   private arr: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    7.   build() {
    8.     Stack({ alignContent: Alignment.TopStart }) {
    9.       Scroll(this.scroller) {
    10.         Column() {
    11.           ForEach(this.arr, (item: number) => {
    12.             Stack() {
    13.               Text('Display Content ' + item.toString()).fontSize(30)
    14.             }
    15.             .width('80%').padding(20).borderRadius(15).backgroundColor(Color.White).margin({ top:30, bottom:30 })
    16.           }, (item: string) => item)
    17.         }.width('100%').backgroundColor('rgb(213,213,213)')
    18.       }.backgroundColor('rgb(213,213,213)')
    19.       .clipContent(ContentClipMode.SAFE_AREA)
    20.     }.width('100%').height('100%')
    21.   }
    22. }
    

**图6** 滚动类容器设置clipContent属性实现沉浸式效果  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.72942034796131303316500546979165:50001231000000:2800:F0FEA17F4AD3FF502D702340C369F02EFCC501694E07893050822DC1F2ADAEA3.png "点击放大")

### 底部页签场景

要求页签背景色能够延伸到导航区域（此处以导航区域表现为导航条为例给出示意），但页签内部可操作元素需要在导航区域之上。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.37246522656942551464504700503566:50001231000000:2800:F55E4980F4B7D0B0006E3960732E793DA44500BA6386C295E62801FCCCC9C579.png "点击放大")

针对底部的页签部分，Navigation组件和Tabs组件默认实现了页签的延伸处理，开发者只需要保证Navigation和Tabs组件的底部边界和底部导航区域重合即可。若开发者显式调用expandSafeArea接口，则安全区效果由expandSafeArea参数指定。

如果未使用上述组件而是采用自定义方式实现页签的场景，可以针对底部元素设置expandSafeArea属性实现底部元素的背景扩展。

**图7** 顶部和底部UI元素未设置和设置expandSafeArea属性效果对比

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.41747390740743659941506414504724:50001231000000:2800:E50527CF67161602DF8FD0C190F67F7D0B4B3B04CF45C3A0446CC37FE90CC51F.png)

1. // xxx.ets
2. @Entry
3. @Component
4. struct Example {
5.   build() {
6.     Column() {
7.       Row() {
8.         Text('Top Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
9.       }.backgroundColor('#2786d9')
10.       // 设置顶部绘制延伸到状态栏
11.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])

12.       Row() {
13.         Text('Display Content 2').fontSize(30)
14.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

15.       Row() {
16.         Text('Display Content 3').fontSize(30)
17.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

18.       Row() {
19.         Text('Display Content 4').fontSize(30)
20.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

21.       Row() {
22.         Text('Display Content 5').fontSize(30)
23.       }.backgroundColor(Color.White).padding(20).borderRadius(15).width('80%')

24.       Row() {
25.         Text('Bottom Content').fontSize(40).textAlign(TextAlign.Center).width('100%')
26.       }.backgroundColor('#96dffa')
27.       // 设置底部绘制延伸到导航区域
28.       .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
29.     }
30.     .width('100%').height('100%')
31.     .alignItems(HorizontalAlign.Center)
32.     .backgroundColor('#d5d5d5')
33.     .justifyContent(FlexAlign.SpaceBetween)
34.   }
35. }

### 图文场景

当状态栏元素和底部导航区域元素不同时，无法单纯通过窗口背景色或者背景图组件延伸实现，此时需要对顶部元素和底部元素分别配置expandSafeArea属性，顶部元素配置expandSafeArea([SafeAreaType.SYSTEM],[SafeAreaEdge.TOP])，底部元素配置expandSafeArea([SafeAreaType.SYSTEM],[SafeAreaEdge.BOTTOM])。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163938.28582942626334677493417993476880:50001231000000:2800:70849062F759622A69E9F0C2E65D297CE52324158491314B545F1CF41A4F9041.png "点击放大")

1. @Entry
2. @Component
3. struct Index {
4.   build() {
5.     Swiper() {
6.       Column() {
7.         Image($r('app.media.start'))
8.           .height('50%').width('100%')
9.           // 设置图片延伸到状态栏
10.           .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP])
11.         Column() {
12.           Text('HarmonyOS 第一课')
13.             .fontSize(32)
14.             .margin(30)
15.           Text('通过循序渐进的学习路径，无经验和有经验的开发者都可以掌握ArkTS语言声明式开发范式，体验更简洁、更友好的HarmonyOS应用开发旅程。')
16.             .fontSize(20).margin(20)
17.         }.height('50%').width('100%')
18.         .backgroundColor(Color.White)
19.         // 设置文本内容区背景延伸到导航栏
20.         .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM])
21.       }
22.     }
23.     .width('100%')
24.     .height('100%')
25.     // 关闭Swiper组件默认的裁切效果以便子节点可以绘制在Swiper外。
26.     .clip(false)
27.   }
28. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-tabs "选项卡 (Tabs)")
