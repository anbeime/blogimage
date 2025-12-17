# UI Design Kit简介

更新时间: 2025-12-16 16:38

UI Design Kit（UI设计套件）是华为提供的符合华为HarmonyOS Design System定义的UI界面开发套件集合，包含HarmonyOS Design System设计定义的扩展UI组件及其多样化的组件样式、丰富多样的UI界面场景下的光影效果，支撑应用实现跟随HarmonyOS Design System高端精致设计效果UI界面，达成应用界面与华为HarmonyOS多设备UI设计风格完美融合（参见[HarmonyOS设计理念](https://developer.huawei.com/consumer/cn/doc/design-guides/design-concepts-0000001795698445)）。

功能范围：

提供HarmonyOS设计风格控件能力，遵循[HarmonyOS设计规范](https://developer.huawei.com/consumer/cn/doc/design-guides/general_overview-0000001929599380)。

满足HarmonyOS人机交互设计，达成全场景人机交互体验一致，遵循[HarmonyOS设计规范](https://developer.huawei.com/consumer/cn/doc/design-guides/general_overview-0000001929599380)。

提供HarmonyOS视觉风格匹配的开发能力，遵循[HarmonyOS设计规范](https://developer.huawei.com/consumer/cn/doc/design-guides/general_overview-0000001929599380)。

## 场景介绍

UI Design Kit提供了应用图标处理能力，帮助开发者实现[UX体验标准](https://developer.huawei.com/consumer/cn/doc/design-guides/ux-guidelines-general-0000001760708152#section1353515481417)的应用图标，支持在线主题图标默认跟随主题换肤，支持应用列表、应用详情页等图标展示场景，具体如下：

- [（推荐）分层图标处理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-layered-process)：对前后景图标进行合成、剪切、缩放、描边处理，支持批量处理。
- [单层图标处理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-normal-process)：对图标进行剪切、缩放、描边处理，支持批量处理。

UI Design Kit提供了HarmonyOS Design System设计定义的扩展UI组件接口及其多样化的组件样式，具体如下：

- [组件导航](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-navigation)：提供HdsNavigation组件作为路由导航的根视图容器与HdsNavDestination作为HdsNavigation子页面的根容器，实现页面间以及组件内部的页面跳转，支持在不同组件间传递跳转参数，提供灵活的跳转操作，从而更便捷地实现对不同页面的访问和复用，UX风格跟随版本演进。
- [侧边栏样式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-sidebar)：提供可以显示和隐藏的侧边栏容器，支持应用使用侧边栏组件实现自定义侧边栏和内容区，UX风格跟随版本演进。
- [侧边栏菜单样式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-side-menu)：提供一种菜单栏样式组件，支持应用设置侧边栏对应的一级菜单和二级菜单，并显示其新消息数量，UX风格跟随版本演进。
- [底部页签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-hds-tabs)：提供一种通过页签进行内容视图切换的容器组件，支持分割线动态显隐、页签栏模糊效果、页签图标出血、页签半屏居中对齐布局等页签增强样式，UX风格跟随版本演进。
- [即时操作](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-snackbar)：提供即时通知的非模态弹窗，支持文本图标展示和按钮操作区，为应用提供简短通知和操作，UX风格跟随版本演进。
- [核心操作栏](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-actionbar)：提供多按钮操作组件，支持有主按钮展开和收起的多按钮操作动效，支持无主按钮的多按钮操作区，UX风格跟随版本演进。
- [列表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-list-item-card)：提供附带横滑删除动效的列表卡片组件，支持自研和三方应用使用列表卡片组件，实现多设备上的系统列表卡片样式以及横滑删除效果，UX风格跟随版本演进。

UI Design Kit提供了应用加载自定义Symbol的能力，具体如下：

- [资源注册](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-custom-symbol-res-register)：注册应用预置的自定义Symbol的图标资源与动效参数资源，配合ArkUI SymbolGlyph与SymbolSpan组件，展示应用侧预置的Symbol图标，UX风格跟随系统级Symbol规格。

UI Design Kit提供了由HarmonyOS Design System设计定义的丰富多样UI界面场景下的光影效果能力，具体如下：

- [点光源效果](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-visual-effect-point-light)：提供点光源接口，用于设置组件的发光效果以及被照亮的受光效果，提升组件交互沉浸感，UX风格跟随版本演进。
- [按压阴影](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-visual-effect-background-color)： 提供按压阴影接口，用于设置组件按压交互时的背景色变化效果，UX风格跟随版本演进。
- [双边边缘流光](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-visual-effect-double-edge-streamer)：提供双边边缘流光接口，用于设置组件的边缘发光效果，支持配置两条边缘流光的起始、终止位置和边缘颜色效果，UX风格跟随版本演进。
- [背景流光](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-visual-effect-background-streamer)：提供背景流光接口，用于设置组件的背景流动发光效果，支持配置背景色及渐变背景色，UX风格跟随版本演进。
- [自带背景的双边流光](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-visual-effect-background-streamer2)：通过通用视效组件HdsVisualComponent提供的自带背景的双边流光效果场景接口，支持设置两条边缘流光的起始、终止位置、边缘颜色效果以及与流光相叠加的背景板颜色，用于胶囊组件、屏幕边缘发光等，UX风格跟随版本演进。
- [应用内多窗](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-multiwindowentryinapp)：提供单应用多窗口的交互入口组件，用于支持自研和三方应用使用HDS的应用内多窗组件实现多窗并行的体验，并且可以设置图标大小颜色、背板大小颜色、文字大小颜色等，UX风格跟随版本演进。

## 与相关能力的区别

- UI Design Kit提供的[组件导航](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-navigation)与ArkUI [Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation)能力的区别：继承ArkUI [Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation)的页面跳转能力及基础样式，扩展支持标题栏随内容区滚动的动态模糊样式，菜单栏新增信息提醒能力，支持标题栏自定义区域设置及标题栏动态显隐功能，新增半模态样式，支持文字型及图片型图标类型设置。具体支持能力及规格参考UI Design Kit API参考文档的[HdsNavigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation)章节与[HdsNavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavdestination)章节。
- 自定义Symbol能力与系统级Symbol能力的区别：自定义Symbol能力允许应用根据自身业务诉求在应用HAP包中预置Symbol图标与动效参数资源，通过资源注册与SymbolGlyph、SymbolSpan组件使用，快速实现应用Symbol图标自定义，无需同系统级Symbol一样提前预置进手机ROM，不强依赖手机ROM版本发布。
- UI Design Kit提供的[列表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-list-item-card)与ArkUI [ListItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-listitem)能力的区别：增加定制化新样式，统一组件风格样式以提升高端精致视觉体验，同时适配多设备系统列表样式，封装ListItem横滑与删除动效。具体支持能力及规格参考UI Design Kit API参考文档的[HdsListItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdslistitem)章节与[HdsListItemCard](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdslistitemcard)章节。
- UI Design Kit提供的[底部页签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-hds-tabs)与ArkUI [Tabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabs)能力的区别：支持分割线动态显隐、页签栏模糊效果、页签图标出血、页签半屏居中对齐布局等页签增强样式。具体支持能力及规格参考UI Design Kit API参考文档的[HdsTabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdstabs)章节。

## 基础概念

在开发前，需要先了解以下基础概念：

- 分层图标：由前景图片和后景图片组成的格式为JSON的图标资源，应用图标必须为分层图标，具体可参考[应用图标规范](https://developer.huawei.com/consumer/cn/doc/design-guides/application-icon-0000001953444009)。
- 单层图标：HarmonyOS支持的图片资源，且支持解码为[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)的图片。
- Symbol图标：Symbol图标是一种支持多种渲染模式以及多种动效模式的矢量类型图标，响应多种字重以及字号大小变化。

## 约束与限制

|组件|约束与限制|
|:--|:--|
|HdsNavigation|- 横屏，导航栏的显示模式为[Stack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navigationmode9%E6%9E%9A%E4%B8%BE%E8%AF%B4%E6%98%8E)时，不支持合并工具栏到菜单栏。<br>- 标题栏布局方式默认采用层叠布局，标题栏在内容区上层。|
|HdsNavDestination|- 横屏，导航栏的显示模式为[Stack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navigationmode9%E6%9E%9A%E4%B8%BE%E8%AF%B4%E6%98%8E)时，不支持合并工具栏到菜单栏。<br>- 标题栏布局方式默认采用层叠布局，标题栏在内容区上层。|

|接口|约束|
|:--|:--|
|图标批量处理接口|- 最大支持设置10个并发数。<br>- 最大支持一次性处理500个图标。|
|Symbol资源注册接口|- 只支持Phone、Tablet、PC/2in1、TV设备。<br>- 只支持应用注册一组图标资源与动效参数资源。<br>- 最大支持10个自定义Symbol图标资源与动效参数资源注册。|

### 支持的国家和地区

UI Design Kit当前仅支持中国境内（不包含中国香港、中国澳门、中国台湾）。

### 支持的设备

|UI Design Kit提供的能力|支持的设备类型|
|:--|:--|
|[应用展示图标HarmonyOS设计风格化处理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-icon-process)|Phone、Tablet、PC/2in1、TV|
|[组件导航](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-navigation)|Phone、Tablet、PC/2in1、TV|
|[侧边栏样式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-sidebar)|Phone、Tablet、PC/2in1、TV|
|[侧边栏菜单样式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-side-menu)|Phone、Tablet、PC/2in1、TV|
|[底部页签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-hds-tabs)|Phone、Tablet、PC/2in1|
|[即时操作](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-snackbar)|Phone、Tablet、PC/2in1、TV|
|[核心操作栏](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-actionbar)|Phone、Tablet、PC/2in1、TV|
|[列表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-list-item-card)|Phone、Tablet、PC/2in1、Wearable、TV|
|[应用加载自定义Symbol](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-config-custom-symbol)|Phone、Tablet、PC/2in1、TV|
|[HDS视效](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-visual-effect)|Phone、Tablet、PC/2in1|
|[应用内多窗](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-multiwindowentryinapp)|Phone、Tablet|

### 模拟器支持情况

本Kit支持模拟器开发，但与真机存在部分能力差异，详情请参见“[模拟器与真机的差异](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-specification#section69899863016)”。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-kit-guide "UI Design Kit（UI设计套件）")
# （推荐）分层图标处理

更新时间: 2025-12-16 16:38

## 场景介绍

从5.0.0(12)版本开始， Hds支持分层图标处理能力。

适用于图标为分层资源，且图标展示风格要与华为HarmonyOS Design System设计风格一致的应用场景。以下是一些典型的应用场景：

- 展示带图标的应用列表：可调用UI Design Kit批量处理分层图标的接口获取处理后的应用图标。
- 展示应用详情：可调用UI Design Kit处理单个分层图标的接口获取处理后的应用图标。
- 展示跟随在线主题的应用图标：可调用UI Design Kit处理分层图标的接口获取主题换肤后的应用图标。

## 约束条件

分层图标处理支持Phone、Tablet、PC/2in1设备，并且从5.1.1(19)版本开始，新增支持TV设备。

## 开发步骤

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163830.08835753951404964236521425948753:50001231000000:2800:49CADA0F885A7932D4DCFC7A0DA899E713789D0F8194723F112BC9E923B019AE.png "点击放大")

1. 设置分层图标。
    
    将前景资源和背景资源，放到entry/src/main/resources/base/media下，在该目录创建一个json文件（例如：drawable.json），内容为
    
    1. {
    2.   "layered-image":
    3.   {
    4.     "background" : "$media:background",
    5.     "foreground" : "$media:foreground"
    6.   }
    7. }
    
2. 将图标处理的相关类添加至工程。
    
    1. import { LayeredDrawableDescriptor } from '@kit.ArkUI';
    2. import { hdsDrawable } from '@kit.UIDesignKit';
    3. import { image } from '@kit.ImageKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    5. import { resourceManager } from '@kit.LocalizationKit';
    6. import { common } from '@kit.AbilityKit';
    

3. 简单配置页面的布局，调用[分层图标接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsdrawable#section156601033183215)获取处理后的图标信息，也可以调用[异步批量处理接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsdrawable#section712131324710)。
    
    1. @Entry
    2. @Component
    3. struct Index{
    4.   bundleName: string = 'com.example.uidesignkit';
    5.   resManager: resourceManager.ResourceManager | undefined = undefined;
    6.   layeredDrawableDescriptor: LayeredDrawableDescriptor | undefined = undefined;
    7.   @State layeredIconsResult: Array<hdsDrawable.ProcessedIcon> = [];
    
    8.   build() {
    9.     Column() {
    10.       Column() {
    11.         Text('getHdsLayeredIcon')
    12.           .fontWeight(FontWeight.Bold)
    13.           .fontSize(16)
    14.           .margin(5)
    
    15.         Image(this.getHdsLayeredIcon())
    16.           .width(48)
    17.           .height(48)
    18.       }
    19.       .margin(20)
    
    20.       Text('getHdsLayeredIcons')
    21.         .fontWeight(FontWeight.Bold)
    22.         .fontSize(16)
    23.         .margin(5)
    
    24.       List() {
    25.         ForEach(this.layeredIconsResult,
    26.           (item: hdsDrawable.ProcessedIcon, index?: number) => {
    27.             ListItem() {
    28.               Column() {
    29.                 Text(item.bundleName)
    30.                   .fontWeight(FontWeight.Medium)
    31.                   .fontSize(16)
    32.                   .margin(5)
    
    33.                 Image(item.pixelMap)
    34.                   .width(48)
    35.                   .height(48)
    36.               }
    37.               .margin(15)
    38.             }
    39.             .width('100%')
    40.           }, (item: string) => item.toString())
    41.       }
    42.       .scrollBar(BarState.On)
    43.       .height('60%')
    44.     }
    45.     .height('100%')
    46.     .width('100%')
    47.   }
    
    48.   aboutToAppear(): void {
    49.     // 获取资源管理器
    50.     this.resManager = (this.getUIContext().getHostContext() as common.UIAbilityContext)?.resourceManager;
    51.     if (!this.resManager) {
    52.       return;
    53.     }
    54.     // 通过资源管理获取原始分层图标信息
    55.     this.layeredDrawableDescriptor = (this.resManager.getDrawableDescriptor($r('app.media.drawable')
    56.       .id)) as LayeredDrawableDescriptor;
    57.     this.getHdsLayeredIcons();
    58.   }
    
    59.   private getHdsLayeredIcon(): image.PixelMap | null {
    60.     try {
    61.       // 调用HDS分层图标接口处理图标
    62.       return hdsDrawable.getHdsLayeredIcon(this.bundleName, this.layeredDrawableDescriptor, 48, true);
    63.     } catch (err) {
    64.       let message = (err as BusinessError).message;
    65.       let code = (err as BusinessError).code;
    66.       console.error(`getHdsLayeredIcon failed, code: ${code}, message: ${message}`);
    67.       return null;
    68.     }
    69.   }
    
    70.   private getHdsLayeredIcons(): void {
    71.     if (!this.layeredDrawableDescriptor) {
    72.       console.error(`getHdsLayeredIcons layeredDrawableDescriptor is undefined.`);
    73.       return;
    74.     }
    
    75.     // 构造批量接口传参
    76.     let options: hdsDrawable.Options = {
    77.       size: 48,
    78.       hasBorder: true,
    79.       parallelNumber: 4
    80.     };
    
    81.     let layeredIcons: Array<hdsDrawable.LayeredIcon> = [];
    82.     for (let i = 0; i < 10; i++) {
    83.       layeredIcons.push({
    84.         bundleName: `${this.bundleName}-${i}`,
    85.         layeredDrawableDescriptor: this.layeredDrawableDescriptor
    86.       });
    87.     }
    
    88.     try {
    89.       // 调用HDS批量分层接口处理图标
    90.       hdsDrawable.getHdsLayeredIcons(layeredIcons, options)
    91.         .then((data: Array<hdsDrawable.ProcessedIcon>) => {
    92.           console.info(`getHdsLayeredIcons data size: ${data.length}`);
    93.           this.layeredIconsResult = data;
    94.         })
    95.         .catch((err: BusinessError) => {
    96.           console.error(`getHdsLayeredIcons return error, code: ${err.code}, msg: ${err.message}`);
    97.         });
    98.     } catch (err) {
    99.       let message = (err as BusinessError).message;
    100.       let code = (err as BusinessError).code;
    101.       console.error(`getHdsLayeredIcons failed, code: ${code}, message: ${message}`);
    102.     }
    103.   }
    104. }
    

## 开发实例

1. import { LayeredDrawableDescriptor } from '@kit.ArkUI';
2. import { hdsDrawable } from '@kit.UIDesignKit';
3. import { image } from '@kit.ImageKit';
4. import { BusinessError } from '@kit.BasicServicesKit';
5. import { resourceManager } from '@kit.LocalizationKit';
6. import { common } from '@kit.AbilityKit';

7. @Entry
8. @Component
9. struct Index{
10.   bundleName: string = 'com.example.uidesignkit';
11.   resManager: resourceManager.ResourceManager | undefined = undefined;
12.   layeredDrawableDescriptor: LayeredDrawableDescriptor | undefined = undefined;
13.   @State layeredIconsResult: Array<hdsDrawable.ProcessedIcon> = [];

14.   build() {
15.     Column() {
16.       Column() {
17.         Text('getHdsLayeredIcon')
18.           .fontWeight(FontWeight.Bold)
19.           .fontSize(16)
20.           .margin(5)

21.         Image(this.getHdsLayeredIcon())
22.           .width(48)
23.           .height(48)
24.       }
25.       .margin(20)

26.       Text('getHdsLayeredIcons')
27.         .fontWeight(FontWeight.Bold)
28.         .fontSize(16)
29.         .margin(5)

30.       List() {
31.         ForEach(this.layeredIconsResult,
32.           (item: hdsDrawable.ProcessedIcon, index?: number) => {
33.             ListItem() {
34.               Column() {
35.                 Text(item.bundleName)
36.                   .fontWeight(FontWeight.Medium)
37.                   .fontSize(16)
38.                   .margin(5)

39.                 Image(item.pixelMap)
40.                   .width(48)
41.                   .height(48)
42.               }
43.               .margin(15)
44.             }
45.             .width('100%')
46.           }, (item: string) => item.toString())
47.       }
48.       .scrollBar(BarState.On)
49.       .height('60%')
50.     }
51.     .height('100%')
52.     .width('100%')
53.   }

54.   aboutToAppear(): void {
55.     // 获取资源管理器
56.     this.resManager = (this.getUIContext().getHostContext() as common.UIAbilityContext)?.resourceManager;
57.     if (!this.resManager) {
58.       return;
59.     }
60.     // 通过资源管理获取原始分层图标信息
61.     this.layeredDrawableDescriptor = (this.resManager.getDrawableDescriptor($r('app.media.drawable').id)) as LayeredDrawableDescriptor;
62.     this.getHdsLayeredIcons();
63.   }

64.   private getHdsLayeredIcon(): image.PixelMap | null {
65.     try {
66.       // 调用HDS分层图标接口处理图标
67.       return hdsDrawable.getHdsLayeredIcon(this.bundleName, this.layeredDrawableDescriptor, 48, true);
68.     } catch (err) {
69.       let message = (err as BusinessError).message;
70.       let code = (err as BusinessError).code;
71.       console.error(`getHdsLayeredIcon failed, code: ${code}, message: ${message}`);
72.       return null;
73.     }
74.   }

75.   private getHdsLayeredIcons(): void {
76.     if (!this.layeredDrawableDescriptor) {
77.       console.error(`getHdsLayeredIcons layeredDrawableDescriptor is undefined.`);
78.       return;
79.     }

80.     // 构造批量接口传参
81.     let options: hdsDrawable.Options = {
82.       size: 48,
83.       hasBorder: true,
84.       parallelNumber: 4
85.     };

86.     let layeredIcons: Array<hdsDrawable.LayeredIcon> = [];
87.     for (let i = 0; i < 10; i++) {
88.       layeredIcons.push({
89.         bundleName: `${this.bundleName}-${i}`,
90.         layeredDrawableDescriptor: this.layeredDrawableDescriptor
91.       });
92.     }

93.     try {
94.       // 调用HDS批量分层接口处理图标
95.       hdsDrawable.getHdsLayeredIcons(layeredIcons, options)
96.         .then((data: Array<hdsDrawable.ProcessedIcon>) => {
97.           console.info(`getHdsLayeredIcons data size: ${data.length}`);
98.           this.layeredIconsResult = data;
99.         })
100.         .catch((err: BusinessError) => {
101.           console.error(`getHdsLayeredIcons return error, code: ${err.code}, msg: ${err.message}`);
102.         });
103.     } catch (err) {
104.       let message = (err as BusinessError).message;
105.       let code = (err as BusinessError).code;
106.       console.error(`getHdsLayeredIcons failed, code: ${code}, message: ${message}`);
107.     }
108.   }
109. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-icon-process "应用展示图标HarmonyOS设计风格化处理")
# 单层图标处理

更新时间: 2025-12-16 16:38

## 场景介绍

从5.0.0(12)版本开始， Hds支持单层图标处理能力。

适用于图标为单层资源，且图标展示风格要与华为HarmonyOS Design System设计风格一致的应用场景，典型应用场景可参考分层图标[场景介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-layered-process#section154545114557)。

## 约束条件

单层图标处理支持Phone、Tablet、PC/2in1设备，并且从5.1.1(19)版本开始，新增支持TV设备。

## 开发步骤

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163837.27022478347393501634922570172711:50001231000000:2800:6B1C6D387D2C64AA1E0FFB56767A852A0ED6B694189269EF81B12BB97F46F2EC.png "点击放大")

1. 在entry/src/main/resources/base/media下，配置一张图片资源normal_icon.png。
2. 将图标处理的相关类添加至工程。
    
    1. import { LayeredDrawableDescriptor, DrawableDescriptor } from '@kit.ArkUI';
    2. import { hdsDrawable } from '@kit.UIDesignKit';
    3. import { image } from '@kit.ImageKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    5. import { resourceManager } from '@kit.LocalizationKit';
    6. import { common } from '@kit.AbilityKit';
    

3. 简单配置页面的布局，调用[单层图标接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsdrawable#section11716322123212)获取处理后的图标信息，也可以调用[异步批量处理接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsdrawable#section12429174135913)。
    
    1. @Entry
    2. @Component
    3. struct Index{
    4.   bundleName: string = 'com.example.uidesignkit';
    5.   resManager: resourceManager.ResourceManager | undefined = undefined;
    6.   layeredDrawableDescriptor: LayeredDrawableDescriptor | undefined = undefined;
    7.   drawableDescriptor: DrawableDescriptor | undefined = undefined;
    8.   @State iconsResult: Array<hdsDrawable.ProcessedIcon> = [];
    
    9.   build() {
    10.     Column() {
    11.       Column() {
    12.         Text('getHdsIcon')
    13.           .fontWeight(FontWeight.Bold)
    14.           .fontSize(16)
    15.           .margin(5)
    
    16.         Image(this.getHdsIcon())
    17.           .width(48)
    18.           .height(48)
    19.       }
    20.       .margin(20)
    
    21.       Text('getHdsIcons')
    22.         .fontWeight(FontWeight.Bold)
    23.         .fontSize(16)
    24.         .margin(5)
    
    25.       List() {
    26.         ForEach(this.iconsResult,
    27.           (item: hdsDrawable.ProcessedIcon, index?: number) => {
    28.             ListItem() {
    29.               Column() {
    30.                 Text(item.bundleName)
    31.                   .fontWeight(FontWeight.Medium)
    32.                   .fontSize(16)
    33.                   .margin(5)
    
    34.                 Image(item.pixelMap)
    35.                   .width(48)
    36.                   .height(48)
    37.               }
    38.               .margin(15)
    39.             }
    40.             .width('100%')
    41.           }, (item: string) => item.toString())
    42.       }
    43.       .scrollBar(BarState.On)
    44.       .height('60%')
    45.     }
    46.     .height('100%')
    47.     .width('100%')
    48.   }
    
    49.   aboutToAppear(): void {
    50.     // 获取资源管理器
    51.     this.resManager = (this.getUIContext().getHostContext() as common.UIAbilityContext)?.resourceManager;
    52.     if (!this.resManager) {
    53.       return;
    54.     }
    
    55.     // 通过资源管理获取分层图标信息
    56.     this.layeredDrawableDescriptor = (this.resManager.getDrawableDescriptor($r('app.media.drawable').id)) as LayeredDrawableDescriptor;
    
    57.     // 通过资源管理获取单层图标信息
    58.     this.drawableDescriptor =
    59.       (this.resManager?.getDrawableDescriptor($r('app.media.normal_icon').id)) as DrawableDescriptor;
    
    60.     this.getHdsIcons();
    61.   }
    
    62.   private getHdsIcon(): image.PixelMap | null {
    63.     try {
    64.       // 调用HDS单层图标接口
    65.       return hdsDrawable.getHdsIcon(this.bundleName, this.drawableDescriptor?.getPixelMap(), 48,
    66.         this.layeredDrawableDescriptor?.getMask().getPixelMap(), true);
    67.     } catch (err) {
    68.       let message = (err as BusinessError).message;
    69.       let code = (err as BusinessError).code;
    70.       console.error(`getHdsIcon failed, code: ${code}, message: ${message}`);
    71.       return null;
    72.     }
    73.   }
    
    74.   getHdsIcons(): void {
    75.     if (!this.drawableDescriptor) {
    76.       console.error(`getHdsIcons drawableDescriptor is undefined.`);
    77.       return;
    78.     }
    
    79.     if (!this.layeredDrawableDescriptor) {
    80.       console.error(`getHdsIcons layeredDrawableDescriptor is undefined.`);
    81.       return;
    82.     }
    
    83.     // 构造批量接口传参
    84.     let options: hdsDrawable.Options = {
    85.       size: 48,
    86.       hasBorder: true,
    87.       parallelNumber: 4
    88.     };
    
    89.     let icons: Array<hdsDrawable.Icon> = [];
    90.     for (let i = 0; i < 10; i++) {
    91.       icons.push({
    92.         bundleName: `${this.bundleName}-${i}`,
    93.         pixelMap: this.drawableDescriptor.getPixelMap()
    94.       })
    95.     }
    
    96.     try {
    97.       // 调用HDS单层批量接口处理图标
    98.       hdsDrawable.getHdsIcons(icons, this.layeredDrawableDescriptor.getMask().getPixelMap(), options)
    99.         .then((data: Array<hdsDrawable.ProcessedIcon>) => {
    100.           console.info(`getHdsIcons data size: ${data.length}`);
    101.           this.iconsResult = data;
    102.         })
    103.         .catch((err: BusinessError) => {
    104.           console.error(`getHdsIcons error, code: ${err.code}, msg: ${err.message}`);
    105.         });
    106.     } catch (err) {
    107.       let message = (err as BusinessError).message;
    108.       let code = (err as BusinessError).code;
    109.       console.error(`getHdsIcons callback failed: ${message}, code: ${code}`);
    110.     }
    111.   }
    112. }
    

## 开发实例

1. import { LayeredDrawableDescriptor, DrawableDescriptor } from '@kit.ArkUI';
2. import { hdsDrawable } from '@kit.UIDesignKit';
3. import { image } from '@kit.ImageKit';
4. import { BusinessError } from '@kit.BasicServicesKit';
5. import { resourceManager } from '@kit.LocalizationKit';
6. import { common } from '@kit.AbilityKit';

7. @Entry
8. @Component
9. struct Index{
10.   bundleName: string = 'com.example.uidesignkit';
11.   resManager: resourceManager.ResourceManager | undefined = undefined;
12.   layeredDrawableDescriptor: LayeredDrawableDescriptor | undefined = undefined;
13.   drawableDescriptor: DrawableDescriptor | undefined = undefined;
14.   @State iconsResult: Array<hdsDrawable.ProcessedIcon> = [];

15.   build() {
16.     Column() {
17.       Column() {
18.         Text('getHdsIcon')
19.           .fontWeight(FontWeight.Bold)
20.           .fontSize(16)
21.           .margin(5)

22.         Image(this.getHdsIcon())
23.           .width(48)
24.           .height(48)
25.       }
26.       .margin(20)

27.       Text('getHdsIcons')
28.         .fontWeight(FontWeight.Bold)
29.         .fontSize(16)
30.         .margin(5)

31.       List() {
32.         ForEach(this.iconsResult,
33.           (item: hdsDrawable.ProcessedIcon, index?: number) => {
34.             ListItem() {
35.               Column() {
36.                 Text(item.bundleName)
37.                   .fontWeight(FontWeight.Medium)
38.                   .fontSize(16)
39.                   .margin(5)

40.                 Image(item.pixelMap)
41.                   .width(48)
42.                   .height(48)
43.               }
44.               .margin(15)
45.             }
46.             .width('100%')
47.           }, (item: string) => item.toString())
48.       }
49.       .scrollBar(BarState.On)
50.       .height('60%')
51.     }
52.     .height('100%')
53.     .width('100%')
54.   }

55.   aboutToAppear(): void {
56.     // 获取资源管理器
57.     this.resManager = (this.getUIContext().getHostContext() as common.UIAbilityContext)?.resourceManager;
58.     if (!this.resManager) {
59.       return;
60.     }

61.     // 通过资源管理获取分层图标信息
62.     this.layeredDrawableDescriptor = (this.resManager.getDrawableDescriptor($r('app.media.drawable').id)) as LayeredDrawableDescriptor;

63.     // 通过资源管理获取单层图标信息
64.     this.drawableDescriptor =
65.       (this.resManager?.getDrawableDescriptor($r('app.media.normal_icon').id)) as DrawableDescriptor;

66.     this.getHdsIcons();
67.   }

68.   private getHdsIcon(): image.PixelMap | null {
69.     try {
70.       // 调用HDS单层图标接口处理图标
71.       return hdsDrawable.getHdsIcon(this.bundleName, this.drawableDescriptor?.getPixelMap(), 48,
72.         this.layeredDrawableDescriptor?.getMask().getPixelMap(), true);
73.     } catch (err) {
74.       let message = (err as BusinessError).message;
75.       let code = (err as BusinessError).code;
76.       console.error(`getHdsIcon failed, code: ${code}, message: ${message}`);
77.       return null;
78.     }
79.   }

80.   getHdsIcons(): void {
81.     if (!this.drawableDescriptor) {
82.       console.error(`getHdsIcons drawableDescriptor is undefined.`);
83.       return;
84.     }

85.     if (!this.layeredDrawableDescriptor) {
86.       console.error(`getHdsIcons layeredDrawableDescriptor is undefined.`);
87.       return;
88.     }

89.     // 构造批量接口传参
90.     let options: hdsDrawable.Options = {
91.       size: 48,
92.       hasBorder: true,
93.       parallelNumber: 4
94.     };

95.     let icons: Array<hdsDrawable.Icon> = [];
96.     for (let i = 0; i < 10; i++) {
97.       icons.push({
98.         bundleName: `${this.bundleName}-${i}`,
99.         pixelMap: this.drawableDescriptor.getPixelMap()
100.       })
101.     }

102.     try {
103.       // 调用HDS单层批量接口处理图标
104.       hdsDrawable.getHdsIcons(icons, this.layeredDrawableDescriptor.getMask().getPixelMap(), options)
105.         .then((data: Array<hdsDrawable.ProcessedIcon>) => {
106.           console.info(`getHdsIcons data size: ${data.length}`);
107.           this.iconsResult = data;
108.         })
109.         .catch((err: BusinessError) => {
110.           console.error(`getHdsIcons error, code: ${err.code}, msg: ${err.message}`);
111.         });
112.     } catch (err) {
113.       let message = (err as BusinessError).message;
114.       let code = (err as BusinessError).code;
115.       console.error(`getHdsIcons callback failed: ${message}, code: ${code}`);
116.     }
117.   }
118. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-layered-process "（推荐）分层图标处理")
# 设置动态模糊样式

更新时间: 2025-12-16 16:38

## 场景介绍

从5.1.0(18)版本开始， 导航组件新增支持标题栏[通用模糊](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation#section21731754221)样式。

从6.0.0(20) Beta1版本开始，新增支持[过渡模糊](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation#section21731754221)与[渐变模糊](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation#section21731754221)样式。

当应用开发者需要使用标题栏样式随内容区滚动而动态改变样式的导航组件时，可以通过设置titleBar属性中的[style](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation#section1867665412513)配置，自定义滚动前后的标题栏样式。

### 通用模糊样式

对组件背景进行均匀的模糊处理，模糊强度一致，边界清晰，用于强调控件与内容的层级分隔。滑动内容进入/离开标题栏区域过程中，模糊背板和分割线透明渐变出现/消失。此方式适用于非沉浸式场景。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163830.50066546021224089263522782871856:50001231000000:2800:2D33D8FD788CA442B8B22A3B7CBFE6969BADC640BE14193DCCF6C23402C4547E.gif "点击放大")

### 过渡模糊样式

对组件背景进行均匀的模糊处理，模糊强度一致，边界清晰，用于强调控件与内容的层级分隔。滑动前后标题栏内容发生颜色/状态变化，滑动过程中，线性跟手变化。此方式仅适用于沉浸式到非沉浸式相互切换的场景。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163830.47986144434796029188546767507282:50001231000000:2800:B37D3D9EBD0F1E904B45292DA28346887338697B54D5A0918E104B3C377AF810.gif "点击放大")

### 渐变模糊样式

模糊效果在空间维度上呈现渐强/渐弱的变化，模糊边界柔和，用于增强页面沉浸感。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163830.28143546726529060171447244624364:50001231000000:2800:4BF77524DC9CAD778EA34D0AFCEDAED22FBD510558102783D4E350EFDFC2A27C.gif "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsNavigation, HdsNavigationAttribute, ScrollEffectType } from '@kit.UIDesignKit';
    2. import { LengthMetrics } from '@kit.ArkUI';
    
2. 创建一级导航组件，通过配置titleBar中的scrollEffectType属性，可实现通用模糊、过渡模糊、渐变模糊样式。
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   build() {
    5.     HdsNavigation() { // 创建HdsNavigation组件
    6.       // HdsNavigation组件内容区
    7.     }.titleBar({
    8.       style: { // 设置导航组件标题栏样式
    9.         // 标题栏动态模糊样式，包括是否使能滚动动态模糊，动态模糊类型，动态模糊生效的滚动距离等
    10.         scrollEffectOpts: {
    11.           enableScrollEffect: true,
    12.           scrollEffectType: ScrollEffectType.COMMON_BLUR,
    13.           blurEffectiveStartOffset: LengthMetrics.vp(0),
    14.           blurEffectiveEndOffset: LengthMetrics.vp(20)
    15.         },
    16.         originalStyle: { // 内容区滚动前初始样式设置
    17.           backgroundStyle: { // 标题栏背板样式设置
    18.             backgroundColor: $r('sys.color.ohos_id_color_background'),
    19.           },
    20.           contentStyle: { // 标题栏内容区样式设置，包括标题区域，菜单区域，返回按钮区域
    21.             titleStyle: {
    22.               mainTitleColor: $r('sys.color.font_primary'),
    23.               subTitleColor: $r('sys.color.font_secondary')
    24.             },
    25.             menuStyle: {
    26.               backgroundColor: $r('sys.color.comp_background_tertiary'),
    27.               iconColor: $r('sys.color.icon_primary')
    28.             },
    29.             backIconStyle: {
    30.               backgroundColor: $r('sys.color.comp_background_tertiary'),
    31.               iconColor: $r('sys.color.icon_primary')
    32.             }
    33.           }
    34.         },
    35.         scrollEffectStyle: { // 内容区滚动超过blurEffectiveEndOffset后样式设置
    36.           backgroundStyle: {
    37.             backgroundColor: $r('sys.color.ohos_id_color_background_transparent'),
    38.           },
    39.           contentStyle: {
    40.             titleStyle: {
    41.               mainTitleColor: $r('sys.color.font_primary'),
    42.               subTitleColor: $r('sys.color.font_secondary')
    43.             },
    44.             menuStyle: {
    45.               backgroundColor: $r('sys.color.comp_background_tertiary'),
    46.               iconColor: $r('sys.color.icon_primary')
    47.             },
    48.             backIconStyle: {
    49.               backgroundColor: $r('sys.color.comp_background_tertiary'),
    50.               iconColor: $r('sys.color.icon_primary')
    51.             }
    52.           }
    53.         }
    54.       },
    55.       content: { // 标题栏内容设置
    56.         title: { mainTitle: 'Main', subTitle: 'Sub' },
    57.       }
    58.     })
    59.   }
    60. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-navigation "组件导航")
# 设置信息提醒

更新时间: 2025-12-16 16:38

## 场景介绍

从5.1.0(18)版本开始，导航组件新增支持菜单栏设置信息提醒能力。

当应用开发者需要在导航组件菜单项右上角附加消息提醒时，可以通过设置标题栏菜单中的[badge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation#section7349101217489)配置，实现信息提醒能力。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163837.34590632582726425017503081602487:50001231000000:2800:32A6ADD7948A13A9C01D03C6316856C4E080B518C485814A0BFBEFA86F90B84B.jpg "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsNavigation, HdsNavigationAttribute } from '@kit.UIDesignKit';
    
2. 创建一级导航组件，通过配置titleBar中menu的badge属性，设置信息提醒样式。
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   build() {
    5.     HdsNavigation() { // 创建HdsNavigation组件
    6.     }.titleBar({
    7.       content: { // HdsNavigation标题栏内容设置
    8.         menu: { // HdsNavigation标题栏菜单区域内容设置
    9.           value: [{
    10.             content: { // 第一个菜单项内容设置
    11.               label: 'menu1',
    12.               icon: 'resources/base/media/startIcon.png',
    13.               isEnabled: true,
    14.             },
    15.             badge: { // 第一个菜单项信息提醒设置
    16.               count: 1,
    17.             }
    18.           },{
    19.             content: { // 第二个菜单项内容设置
    20.               label: 'menu2',
    21.               icon: 'resources/base/media/startIcon.png',
    22.               isEnabled: true,
    23.             },
    24.             badge: { // 第二个菜单项信息提醒设置
    25.               count: 100,
    26.             }
    27.           }]
    28.         },
    29.         title: { mainTitle: 'MainTitle', subTitle: 'SubTitle' },
    30.       }
    31.     })
    32.   }
    33. }
    # 设置自定义区域

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，导航组件新增支持设置标题栏[stackBuilder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation#section156391311175017)以及[bottomBuilder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation#section156391311175017)。

当应用开发者需要在标题栏区域增加自定义节点时，例如在标题栏上方区域增加分段按钮，标题栏底部区域增加搜索框、页签时，可以使用标题栏自定义区域设置能力。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163841.47922832784972414679093234381992:50001231000000:2800:FB2AB7C3A597636CF1E69637B9F719B25EC88DEDEDDF457F2C57CD15E648D746.png)

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163841.32287203516598070875297709532650:50001231000000:2800:BFA0FD248073D774F9234CF5F44B293E9A908547C8E8A64BC1C867030B0F131A.png "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsNavigation, HdsNavigationAttribute, BottomBuilderShowType } from '@kit.UIDesignKit';
    
2. 创建一级导航组件，通过配置titleBar中content属性的stackBuilder以及bottomBuilder属性，可以使用导航组件的自定义区域设置功能。
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   @Builder
    5.   StackBuilder() { // 自定义StackBuilder组件
    6.     Column() {
    7.       Button("Hello")
    8.     }
    9.     .height(56)
    10.     .justifyContent(FlexAlign.Center)
    11.   }
    
    12.   @Builder
    13.   BottomBuilder() { // 自定义BottomBuilder组件
    14.     Column() {
    15.       Search()
    16.     }
    17.     .width('100%')
    18.     .height(56)
    19.     .backgroundColor(Color.Orange)
    20.   }
    
    21.   build() {
    22.     HdsNavigation() { // 创建HdsNavigation组件
    23.     }.titleBar({
    24.       content: { // 设置HdsNavigation组件内容区
    25.         title: { mainTitle: 'MainTitle', subTitle: 'SubTitle' },
    26.         // 设置HdsNavigation StackBuilder区域
    27.         stackBuilder: (): void => this.StackBuilder(),
    28.         // 设置HdsNavigation BottomBuilder区域，包括设置高度，显示类型
    29.         bottomBuilder: {
    30.           builder: (): void => this.BottomBuilder(),
    31.           height: 56,
    32.           showType: BottomBuilderShowType.DIRECTLY_SHOW
    33.         }
    34.       }
    35.     })
    36.   }
    37. }
    # 标题栏动态显隐

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，导航组件新增支持设置标题栏动态显隐及隐藏类型。

当应用开发者需要动态隐藏标题栏时，可通过使用[dynamicHideTitleBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation#section96017217517)属性实现该功能。设置隐藏标题区域前提下，才可以设置隐藏状态栏。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163845.90013898284924782867143240871453:50001231000000:2800:3167F7849B5D43138965B4E5BD140B7B9B80711747D7F855B69AAE3034763CA3.gif "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsNavigation, HdsNavigationAttribute, BottomBuilderShowType, HideMode } from '@kit.UIDesignKit';
    
2. 创建一级导航组件，通过设置dynamicHideTitleBar属性，可隐藏状态栏、标题区域、bottomBuilder区域。
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   @Builder
    5.   BottomBuilder() { // 自定义BottomBuilder组件
    6.     Column() {
    7.       Search()
    8.     }
    9.     .width('100%')
    10.     .height(56)
    11.     .backgroundColor(Color.Orange)
    12.   }
    
    13.   build() {
    14.     HdsNavigation() { // 创建HdsNavigation组件
    15.     }.titleBar({
    16.       content: {
    17.         title: { mainTitle: 'MainTitle', subTitle: 'SubTitle' },
    18.         // 设置HdsNavigation bottomBuilder区域，包括设置高度，显示类型
    19.         bottomBuilder: { builder: (): void => this.BottomBuilder(), height: 56, showType: BottomBuilderShowType.DIRECTLY_SHOW }
    20.       }
    21.     })
    22.     // 设置HdsNavigation标题栏动态显隐，包括设置标题区域，bottomBuilder区域，状态栏区域是否动态隐藏，隐藏模式以及开始隐藏时内容区的滚动距离。
    23.     .dynamicHideTitleBar({ hideTitleArea:true, hideBottomBuilder: true, hideStatusBar: false, mode: HideMode.SCROLL_UP_TO, hideOffset: 10 })
    24.   }
    25. }
    # 半模态样式

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，导航组件新增支持半模态样式和半模态样式下的标题栏模糊。

用于半模态弹窗中使用导航组件场景。通过设置[HdsNavigationTitleMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation#section26841314155317)为MODAL可以实现标题栏半模态样式及动态模糊。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.75445816044015011710861101854410:50001231000000:2800:D16767AC5FCDA1C4E0DD00737587D44B27A124F313457A7FCD7E48C6A78A37F7.png "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsNavigation, HdsNavigationAttribute, HdsNavigationTitleMode } from '@kit.UIDesignKit';
    
2. 创建一级导航组件，通过设置titleMode属性为HdsNavigationTitleMode.MODAL实现标题栏半模态样式。
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   build() {
    5.     HdsNavigation() { // 创建HdsNavigation组件
    6.     }
    7.     .titleBar({
    8.       content: {
    9.         title: {mainTitle: 'MainTitle', subTitle: 'SubTitle'},
    10.       }
    11.     })
    12.     .titleMode(HdsNavigationTitleMode.MODAL) // 设置HdsNavigation显示模式为半模态样式
    13.   }
    14. }
    # 图标类型设置

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，导航组件新增支持文本型与图片型图标类型设置。

当应用开发者需要配置图片型图标大小，或者使用普通文字型图标（胶囊型按钮）、单字图标（圆形按钮）时，可通过设置titleBar图标内容配置中的[type](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation#section74312125454)属性实现该功能。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163849.62243083857102362399517424836004:50001231000000:2800:F3DB09CB7FCCB00F06B597D242161CD55AE392A07DA0939B40BC386C12CC2013.png)

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsNavigation, HdsNavigationAttribute, HdsNavigationTitleMode, TextStyleMode, IconStyleMode } from '@kit.UIDesignKit';
    
2. 创建一级导航组件，通过配置titleBar中的menu上的type属性，实现文字型图标以及图片型图标大小设置。
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   build() {
    5.     HdsNavigation() { // 创建HdsNavigation组件
    6.     }
    7.     .titleBar({
    8.       content: {
    9.         title: { mainTitle: 'MainTitle', subTitle: 'SubTitle' },
    10.         menu: { // 设置HdsNavigation菜单内容
    11.           value: [{
    12.             content: { // 设置第一个菜单项内容，设置为普通文本按钮
    13.               label: '文字按钮',
    14.               type: TextStyleMode.NORMAL,
    15.             }
    16.           }, {
    17.             content: { // 设置第二个菜单项内容，设置为单字按钮
    18.               label: '单',
    19.               type: TextStyleMode.SINGLE_CHARACTER,
    20.             }
    21.           }, {
    22.             content: { // 设置第三个菜单项内容，设置为大图标按钮
    23.               label: 'largeIcon',
    24.               icon: 'resources/base/media/app_icon.png',
    25.               type: IconStyleMode.LARGE,
    26.             }
    27.           }, {
    28.             content: { // 设置第四个菜单项内容，设置为小图标按钮
    29.               label: 'smallIcon',
    30.               icon: 'resources/base/media/app_icon.png',
    31.               type: IconStyleMode.SMALL,
    32.             }
    33.           }],
    34.           maxCount: 4 // 最大菜单显示个数配置
    35.         },
    36.       }
    37.     })
    38.     .titleMode(HdsNavigationTitleMode.MODAL)
    39.   }
    40. }
    # 设置应用内多窗

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20)Beta3版本开始，新增支持应用内多窗。

当应用开发者需要使用应用内多窗图标（分屏按钮）时，可通过配置titleBar中的menu的[multiWindowEntryInAPPMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation#section158052224917)属性实现该功能。

## 约束条件

依赖全景多窗特性，只有当前设备及屏幕状态支持全景多窗，才支持设置此功能。目前支持全景多窗的设备形态有：

- 双折叠：展开态。
- 三折叠：双屏态，三屏态的横屏态。
- 平板：横屏态。

对于不支持的设备形态，该组件不可交互，不响应点击事件。

## 开发步骤

1. 导入模块。
    
    1. import { HdsNavigation, HdsNavigationAttribute, HdsNavigationMenuContentOptions } from '@kit.UIDesignKit';
    2. import { Want } from '@kit.AbilityKit';
    
2. 创建一级导航组件，通过配置titleBar中的menu上的multiWindowEntryInAPPMenu属性，实现应用内多窗图标设置。
    
    1. @Entry
    2. @Component
    3. struct MultiWindowEntryInAPPTest {
    4.   private want: Want = {
    5.     // 修改为当前应用的bundleName、moduleName、abilityName，启动应用内的UIAbility
    6.     bundleName: "com.example.myapplication",
    7.     moduleName: "entry",
    8.     abilityName: "FuncAbility",
    9.   }
    10.   @State menuContent: HdsNavigationMenuContentOptions = {
    11.     multiWindowEntryInAPPMenu: {
    12.       want: this.want,
    13.     },
    14.     maxCount: 3,
    15.     value: [
    16.       { content: { label: 'menu1', icon: $r('sys.symbol.search_things'), } },
    17.       { content: { label: 'menu2', icon: $r('sys.symbol.plus'), } }
    18.     ]
    19.   }
    
    20.   build() {
    21.     HdsNavigation() {
    22.       Stack() {
    23.         Text("Page1")
    24.       }.alignContent(Alignment.Center)
    25.       .width("100%")
    26.       .height("100%")
    27.     }
    28.     .hideToolBar(false)
    29.     .navBarWidth('100%')
    30.     .titleBar({
    31.       content: {
    32.         title: {
    33.           mainTitle: "Index"
    34.         },
    35.         menu: this.menuContent
    36.       }
    37.     })
    38.   }
    39. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163851.85357872980398722428416349210246:50001231000000:2800:A54C425DFFAB41CE75CDA0316360F60350D13BA5C22074886FB7075D4438BCEC.jpg "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-navigation-icon-type "图标类型设置")
# 开发实例

更新时间: 2025-12-16 16:38

1. 在首页创建一级导航。通过titleBar接口设置HdsNavigation标题栏样式及内容设置。通过pushPath路由方法跳转二级页面。
    
    1. // 模块导入
    2. import { HdsNavigation, HdsNavigationAttribute, ScrollEffectType, HdsNavigationTitleMode } from '@kit.UIDesignKit';
    3. import { LengthMetrics } from '@kit.ArkUI';
    
    4. const  TITLE_BAR_HEIGHT_MINI: number = 64;
    
    5. @Entry
    6. @Component
    7. struct Index {
    8.   private arr: number[] = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
    9.   @Provide('pageInfos') pageInfos: NavPathStack = new NavPathStack();
    10.   scroller: Scroller = new Scroller();
    11.   @State blankHeight: number = TITLE_BAR_HEIGHT_MINI;
    12.   @State isHideBackButton: boolean = false;
    13.   @State titleMode: HdsNavigationTitleMode = HdsNavigationTitleMode.MINI;
    14.   @State subTitle: string = 'Sub';
    
    15.   build() {
    16.     HdsNavigation(this.pageInfos) { // 创建HdsNavigation组件
    17.       Column() {
    18.         Stack() {
    19.           Scroll(this.scroller) { // 内容区设置可滚动容器组件，用于实现内容区滚动联动标题栏动态模糊效果
    20.             Column() {
    21.               // HdsNavigation标题栏与内容区默认设置堆叠布局，可以在内容区叠加标题栏高度的Blank，防止内容区被标题栏遮挡
    22.               Blank().height(this.blankHeight)
    23.               Image($r('app.media.background1')) // background1为自定义资源，开发者需替换本地资源
    24.                 .width('100%')
    25.               Button('pushPath', { stateEffect: true, type: ButtonType.Capsule })
    26.                 .width('80%')
    27.                 .height(40)
    28.                 .margin({ top: '5%', right: '50vp', left: '50vp'})
    29.                 .onClick(() => {
    30.                   console.info('HDS_BASE_COMPONENT', `onClick firstPage`);
    31.                   this.pageInfos.pushPath({ name: 'pageOne' })
    32.                 })
    33.               Button('hide backButton ' + this.isHideBackButton)
    34.                 .onClick(() => {
    35.                   this.isHideBackButton = !this.isHideBackButton
    36.                 })
    37.                 .width('80%')
    38.                 .height(40)
    39.                 .margin({ top: '5%', right: '50vp', left: '50vp' , bottom: '5%'})
    40.               List({ space: 12, initialIndex: 0 }) {
    41.                 ForEach(this.arr, (item: number) => {
    42.                   ListItem() {
    43.                     Text('' + item)
    44.                       .width('100%')
    45.                       .height(72)
    46.                       .fontSize(16)
    47.                       .fontWeight(500)
    48.                       .textAlign(TextAlign.Center)
    49.                   }
    50.                   .height(120)
    51.                   .backgroundColor(Color.Orange)
    52.                   .borderRadius(24)
    53.                 }, (item: number) => item.toString())
    54.               }
    55.               .edgeEffect(EdgeEffect.None)
    56.               .width('100%')
    57.               .height('100%')
    58.               .nestedScroll({scrollForward:NestedScrollMode.PARENT_FIRST, scrollBackward: NestedScrollMode.PARENT_FIRST})
    59.             }
    60.           }.edgeEffect(EdgeEffect.Spring).scrollBar(BarState.Off)
    61.         }
    62.       }
    63.     }
    64.     .titleBar( { // HdsNavigation标题栏设置
    65.       style: { // HdsNavigation标题栏样式设置
    66.         // 标题栏动态模糊样式，包括是否使能滚动动态模糊，动态模糊类型，动态模糊生效的滚动距离等
    67.         scrollEffectOpts: {
    68.           enableScrollEffect: true,
    69.           scrollEffectType: ScrollEffectType.COMMON_BLUR,
    70.           blurEffectiveStartOffset: LengthMetrics.vp(0),
    71.           blurEffectiveEndOffset: LengthMetrics.vp(20)
    72.         },
    73.       },
    74.       content: { // HdsNavigation标题栏内容区设置
    75.         title: { // HdsNavigation标题栏标题设置
    76.           mainTitle: 'Main',
    77.           subTitle: this.subTitle
    78.         },
    79.         menu: { // HdsNavigation标题栏菜单项设置
    80.           value: [{ // 第一个菜单项内容设置
    81.             content: {
    82.               label: 'menu1',
    83.               icon: $r('sys.symbol.ohos_wifi'),
    84.               isEnabled: true,
    85.             },
    86.             badge: {
    87.               count: 1,
    88.             }
    89.           }, { // 第二个菜单项内容设置
    90.             content: {
    91.               label: 'menu2',
    92.               icon: $r('sys.symbol.ohos_lock'),
    93.               isEnabled: true,
    94.               action: () => {
    95.                 console.info("HDS_NAV HELLO 2");
    96.               }
    97.             }
    98.           }, { // 第三个菜单项内容设置
    99.             content: {
    100.               label: 'menu3',
    101.               icon: $r('sys.symbol.speaker_plus'),
    102.             }
    103.           }, {
    104.             content: { // 第三个菜单项内容设置
    105.               label: 'menu4',
    106.               icon: $r('sys.symbol.ohos_star'),
    107.             }
    108.           }]
    109.         },
    110.         backIcon: { // HdsNavigation返回按钮设置
    111.           label: 'backButton',
    112.           icon: $r('sys.symbol.ohos_mic'),
    113.           isEnabled: true,
    114.         }
    115.       }
    116.     })
    117.     .titleMode(this.titleMode)
    118.     .hideBackButton(this.isHideBackButton)
    119.   }
    120. }
    
2. 在PageOne页面创建二级导航组件。通过titleBar接口设置HdsNavDestination标题栏鸿蒙风格化样式及内容设置。展示NavPathStack路由使用示例。
    
    1. // PageOne.ets
    2. // 模块导入
    3. import { HdsNavDestination, HdsNavDestinationAttribute, ScrollEffectType } from '@kit.UIDesignKit';
    4. import { LengthMetrics } from '@kit.ArkUI';
    
    5. @Builder
    6. export function PageOneBuilder() {
    7.   PageOne()
    8. }
    
    9. const  TITLE_BAR_HEIGHT_MINI: number = 56;
    
    10. @Component
    11. export struct PageOne {
    12.   @Consume("pageInfos")pageInfos: NavPathStack;
    13.   private arr: number[] = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
    14.   scroller: Scroller = new Scroller();
    
    15.   build() {
    16.     HdsNavDestination() { // 创建HdsNavDestination组件
    17.       Scroll(this.scroller) { // HdsNavDestination内容区设置可滚动容器组件，用于实现内容区滚动联动标题栏动态模糊样式
    18.         Column() {
    19.           Blank().height(TITLE_BAR_HEIGHT_MINI)
    20.           Button('pushPath', { stateEffect: true, type: ButtonType.Capsule })
    21.             .width('80%')
    22.             .height(40)
    23.             .margin({ top: '5%', right: '50vp', left: '50vp' , bottom: '5%'})
    24.             .onClick(() => {
    25.               console.info('HDS_BASE_COMPONENT', `onClick pageOne`);
    26.               this.pageInfos.pushPath({ name: 'pageTwo' }) // 将name指定的HdsNavDestination页面信息入栈
    27.             })
    28.           Button('popToName', { stateEffect: true, type: ButtonType.Capsule })
    29.             .width('80%')
    30.             .height(40)
    31.             .margin(20)
    32.             .onClick(() => {
    33.               this.pageInfos.popToName('pageTwo') // 回退路由栈到第一个名为name的HdsNavDestination页面
    34.               console.info('popToName' + JSON.stringify(this.pageInfos),
    35.                 '返回值' + JSON.stringify(this.pageInfos.popToName('pageTwo')))
    36.             })
    37.           Button('popToIndex', { stateEffect: true, type: ButtonType.Capsule })
    38.             .width('80%')
    39.             .height(40)
    40.             .margin(20)
    41.             .onClick(() => {
    42.               this.pageInfos.popToIndex(1) // 回退路由栈到index指定的HdsNavDestination页面
    43.               console.info('popToIndex' + JSON.stringify(this.pageInfos))
    44.             })
    45.           Button('moveIndexToTop', { stateEffect: true, type: ButtonType.Capsule })
    46.             .width('80%')
    47.             .height(40)
    48.             .margin(20)
    49.             .onClick(() => {
    50.               this.pageInfos.moveIndexToTop(1) // 将index指定的HdsNavDestination页面移到栈顶
    51.               console.info('moveIndexToTop' + JSON.stringify(this.pageInfos))
    52.             })
    53.           Button('clear', { stateEffect: true, type: ButtonType.Capsule })
    54.             .width('80%')
    55.             .height(40)
    56.             .margin(20)
    57.             .onClick(() => {
    58.               this.pageInfos.clear() // 清除栈中所有页面
    59.             })
    60.           List({ space: 12, initialIndex: 0 }) {
    61.             ForEach(this.arr, (item: number) => {
    62.               ListItem() {
    63.                 Text('' + item)
    64.                   .width('100%')
    65.                   .height(72)
    66.                   .fontSize(16)
    67.                   .fontWeight(500)
    68.                   .textAlign(TextAlign.Center)
    69.               }
    70.               .height(120)
    71.               .backgroundColor(Color.Orange)
    72.               .borderRadius(24)
    73.             }, (item: number) => item.toString())
    74.           }
    75.           .edgeEffect(EdgeEffect.None)
    76.           .width('100%')
    77.           .height('100%')
    78.           .nestedScroll({scrollForward:NestedScrollMode.PARENT_FIRST, scrollBackward: NestedScrollMode.PARENT_FIRST})
    79.         }
    80.       }.edgeEffect(EdgeEffect.Spring).scrollBar(BarState.Off)
    81.     }
    82.     .titleBar({ // HdsNavDestination标题栏配置
    83.         style: { // HdsNavDestination标题栏样式配置
    84.           // 标题栏动态模糊样式，包括是否使能滚动动态模糊，动态模糊类型，动态模糊生效的滚动距离等
    85.           scrollEffectOpts: {
    86.             enableScrollEffect: true,
    87.             scrollEffectType: ScrollEffectType.COMMON_BLUR,
    88.             blurEffectiveStartOffset: LengthMetrics.vp(0),
    89.             blurEffectiveEndOffset: LengthMetrics.vp(20)
    90.           },
    91.         },
    92.         content: { // HdsNavigation标题栏内容区设置
    93.           title: { // HdsNavigation标题栏标题设置
    94.             mainTitle: "PageOne",
    95.           },
    96.           menu: { // HdsNavigation标题栏菜单设置
    97.             value: [{ // 第一个菜单项内容设置
    98.               content: {
    99.                 label: 'menu1',
    100.                 icon: $r('sys.symbol.ohos_star'),
    101.               }
    102.             }, { // 第二个菜单项内容设置
    103.               content: {
    104.                 label: 'menu2',
    105.                 icon: $r('sys.symbol.ohos_circle'),
    106.               },
    107.               badge: {
    108.                   value: '66'
    109.               }
    110.             }]
    111.           },
    112.         }
    113.       })
    114.     .hideBackButton(false)
    115.   }
    116. }
    
3. 在PageTwo页面创建二级导航组件。
    
    1. // PageTwo.ets
    2. // 模块导入
    3. import { HdsNavDestination, HdsNavDestinationAttribute } from '@kit.UIDesignKit';
    
    4. @Builder
    5. export function PageTwoBuilder() {
    6.   PageTwo()
    7. }
    8. const  TITLE_BAR_HEIGHT_MINI: number = 56;
    9. @Component
    10. export struct PageTwo {
    11.   @Consume("pageInfos")pageInfos: NavPathStack;
    
    12.   build() {
    13.     HdsNavDestination() { // 创建HdsNavDestination组件
    14.       Column() { // HdsNavDestination组件内容区设置
    15.         Blank().height(TITLE_BAR_HEIGHT_MINI)
    16.         Button('pushPathByName', { stateEffect: true, type: ButtonType.Capsule })
    17.           .width('80%')
    18.           .height(40)
    19.           .margin(20)
    20.           .onClick(() => {
    21.             this.pageInfos.pushPathByName('pageOne', null) // 将name指定的HdsNavDestination页面信息入栈
    22.           })
    23.       }.width('100%').height('100%')
    24.     }
    25.     .titleBar({ // HdsNavDestination组件标题栏设置
    26.       content: {
    27.         title: {
    28.           mainTitle: 'PageTwo'
    29.         },
    30.         menu: {
    31.           value: [{
    32.             content: {
    33.               label: 'menu1',
    34.               icon: $r('sys.symbol.trunk'),
    35.             }
    36.           }]
    37.         },
    38.       },
    39.     })
    40.     .onReady((context: NavDestinationContext) => {
    41.       this.pageInfos = context.pathStack;
    42.       console.log('current page config info is ' + JSON.stringify(context.getConfigInRouteMap()))
    43.     })
    44.   }
    45. }
    
4. 工程entry/src/main/module.json5文件中的“module”下新增如下配置，用于页面跳转。
    
    1. "routerMap": "$profile:route_map"
    
5. 工程entry/src/main/resources/base/profile目录下增加route_map.json文件。
    
    1. {
    2.   "routerMap": [
    3.     {
    4.       "name": "pageOne",
    5.       "pageSourceFile": "src/main/ets/pages/PageOne.ets",
    6.       "buildFunction": "PageOneBuilder",
    7.       "data": {
    8.         "description": "this is pageOne"
    9.       }
    10.     },
    11.     {
    12.       "name": "pageTwo",
    13.       "pageSourceFile": "src/main/ets/pages/PageTwo.ets",
    14.       "buildFunction": "PageTwoBuilder"
    15.     }
    16.   ]
    17. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163852.41198032205325017501900189420815:50001231000000:2800:07E2B6808A416259DEF3B8D959DE915B811F097F1C38EBF6786693E525B3F7DA.gif "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-navigation-set-multi-window "设置应用内多窗")
# 设置overlay模式的侧边栏

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置overlay模式的侧边栏。

[HdsSideBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdssidebar)提供可以显示和隐藏的侧边栏容器，通过子组件定义侧边栏和内容区，第一个子组件表示侧边栏，第二个子组件表示内容区，通过设置sideBarContainerType的值为[SideBarContainerType.Overlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-sidebarcontainer#sidebarcontainertype%E6%9E%9A%E4%B8%BE%E8%AF%B4%E6%98%8E)，使得当前HdsSideBar为悬浮样式。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163831.48123407928509902817587517462396:50001231000000:2800:A347E6916645437D6DF502953B3740E84B60EA4BA0E635669B6C4609F4EA87DD.png "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsSideBar } from '@kit.UIDesignKit';
    
2. 设置图片。
    
    将图片资源，放到entry/src/main/resources/base/media下。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163831.05177168537518456060305683043795:50001231000000:2800:48E125D59811BEC8A90312532D15AFD0573F5B177C4C38E74DA02019D724C12E.png "点击放大")
    
3. 创建HdsSideBar侧边栏组件，设置展开模式为overlay。
    
    1. @Entry
    2. @ComponentV2
    3. struct Index {
    4.   @Local isSideBarContainerMask: boolean = true;
    5.   @Local blankHeight: number = 48;
    6.   @Local isAutoHide: boolean = false;
    7.   @Local isShowSidebar: boolean = true;
    8.   @Local triggerValueReplace: number = 0;
    9.   //左侧侧边栏区
    10.   @Builder
    11.   SideBarPanelBuilder() {
    12.     Column() {
    13.       Blank().height(this.blankHeight)
    14.       Text('HdsSideBar Menu 1')
    15.         .fontSize(14)
    16.       Text('HdsSideBar Menu 2')
    17.         .fontSize(14)
    18.     }
    19.     .width('100%')
    20.     .height('100%')
    21.   }
    22.   //右侧内容区
    23.   @Builder
    24.   ContentPanelBuilder() {
    25.     Column(){
    26.       Blank().height(this.blankHeight)
    27.       Image($r('app.media.view')) // view为自定义资源，开发者需替换本地资源
    28.         .width('80%')
    29.         .height('50%')
    30.         .margin({ top: 8 })
    31.         .padding({
    32.           right: '16vp',
    33.           left: '16vp',
    34.           bottom: '16vp',
    35.         })
    36.         .borderRadius(8)
    37.       Column() {
    38.         Text('HdsSideBar content text1')
    39.           .fontSize(14)
    40.         Text('HdsSideBar content text2')
    41.           .fontSize(14)
    42.       }
    43.       Button() {
    44.         SymbolGlyph(this.isShowSidebar ? $r('sys.symbol.open_sidebar') : $r('sys.symbol.close_sidebar'))
    45.           .fontWeight(FontWeight.Normal)
    46.           .fontSize($r('sys.float.ohos_id_text_size_headline7'))
    47.           .fontColor([$r('sys.color.ohos_id_color_titlebar_icon')])
    48.           .hitTestBehavior(HitTestMode.None)
    49.       }
    50.       .id('side_bar_button')
    51.       .backgroundColor($r('sys.color.ohos_id_color_button_normal'))
    52.       .height(24)
    53.       .width(24)
    54.       .animation({ curve: Curve.Sharp, duration: 100 })
    55.       .onClick(() => {
    56.         this.isShowSidebar = !this.isShowSidebar;
    57.       })
    58.     }
    59.   }
    60.   @BuilderParam contentBuilder: () => void = this.ContentPanelBuilder
    61.   @BuilderParam sideBarBuilder: () => void = this.SideBarPanelBuilder
    62.   @Builder
    63.   HDSSideBarBuilder() {
    64.     HdsSideBar({
    65.       sideBarPanelBuilder: (): void => {
    66.         this.sideBarBuilder()
    67.       },
    68.       contentPanelBuilder: (): void => {
    69.         this.contentBuilder()
    70.       },
    71.       autoHide: this.isAutoHide,
    72.       contentAreaMask: this.isSideBarContainerMask,
    73.       sideBarContainerType: SideBarContainerType.Overlay,
    74.       isShowSideBar: this.isShowSidebar,
    75.       $isShowSideBar: (isShowSidebar: boolean) => {
    76.         this.isShowSidebar = !isShowSidebar
    77.       },
    78.     })
    79.   }
    80.   @Builder
    81.   build() {
    82.     Stack() {
    83.       this.HDSSideBarBuilder()
    84.     }
    85.   }
    86. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-sidebar "侧边栏样式")
# 设置embed模式的侧边栏

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置embed模式的侧边栏。

[HdsSideBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdssidebar)提供可以显示和隐藏的侧边栏容器，通过子组件定义侧边栏和内容区，第一个子组件表示侧边栏，第二个子组件表示内容区，通过设置sideBarContainerType的值为[SideBarContainerType.Embed](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-sidebarcontainer#sidebarcontainertype%E6%9E%9A%E4%B8%BE%E8%AF%B4%E6%98%8E)，使得当前HdsSideBar为嵌入样式。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163837.41413697747201217083809162039860:50001231000000:2800:5FFF6C3827B1D4A670873DFA8326BC9881B7918C7774316327109B4509CEE721.png "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsSideBar } from '@kit.UIDesignKit';
    
2. 设置图片。
    
    将图片资源，放到entry/src/main/resources/base/media下。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163837.72431315679270670193789851443595:50001231000000:2800:711BC0E3BB4F78F561C13DF46D6BCE0B05A7876190FE3F2A9A7F5EE77474567F.png "点击放大")
    
3. 创建HdsSideBar侧边栏组件，设置展开模式为embed。
    
    1. @Entry
    2. @ComponentV2
    3. struct Index {
    4.   @Local isSideBarContainerMask: boolean = true;
    5.   @Local blankHeight: number = 48;
    6.   @Local isAutoHide: boolean = false;
    7.   @Local isShowSidebar: boolean = true;
    8.   @Local triggerValueReplace: number = 0;
    9.   //左侧侧边栏区
    10.   @Builder
    11.   SideBarPanelBuilder() {
    12.     Column() {
    13.       Blank().height(this.blankHeight)
    14.       Text('HdsSideBar Menu 1')
    15.         .fontSize(14)
    16.       Text('HdsSideBar Menu 2')
    17.         .fontSize(14)
    18.     }
    19.     .width('100%')
    20.     .height('100%')
    21.   }
    22.   //右侧内容区
    23.   @Builder
    24.   ContentPanelBuilder() {
    25.     Column(){
    26.       Blank().height(this.blankHeight)
    27.       Image($r('app.media.view')) // view为自定义资源，开发者需替换本地资源
    28.         .width('80%')
    29.         .height('50%')
    30.         .margin({ top: 8 })
    31.         .padding({
    32.           right: '16vp',
    33.           left: '16vp',
    34.           bottom: '16vp',
    35.         })
    36.         .borderRadius(8)
    37.       Column() {
    38.         Text('HdsSideBar content text1')
    39.           .fontSize(14)
    40.         Text('HdsSideBar content text2')
    41.           .fontSize(14)
    42.       }
    43.       Button() {
    44.         SymbolGlyph(this.isShowSidebar ? $r('sys.symbol.open_sidebar') : $r('sys.symbol.close_sidebar'))
    45.           .fontWeight(FontWeight.Normal)
    46.           .fontSize($r('sys.float.ohos_id_text_size_headline7'))
    47.           .fontColor([$r('sys.color.ohos_id_color_titlebar_icon')])
    48.           .hitTestBehavior(HitTestMode.None)
    49.       }
    50.       .id('side_bar_button')
    51.       .backgroundColor($r('sys.color.ohos_id_color_button_normal'))
    52.       .height(24)
    53.       .width(24)
    54.       .animation({ curve: Curve.Sharp, duration: 100 })
    55.       .onClick(() => {
    56.         this.isShowSidebar = !this.isShowSidebar;
    57.       })
    58.     }
    59.   }
    60.   @BuilderParam contentBuilder: () => void = this.ContentPanelBuilder
    61.   @BuilderParam sideBarBuilder: () => void = this.SideBarPanelBuilder
    62.   @Builder
    63.   HDSSideBarBuilder() {
    64.     HdsSideBar({
    65.       sideBarPanelBuilder: (): void => {
    66.         this.sideBarBuilder()
    67.       },
    68.       contentPanelBuilder: (): void => {
    69.         this.contentBuilder()
    70.       },
    71.       autoHide: this.isAutoHide,
    72.       contentAreaMask: this.isSideBarContainerMask,
    73.       sideBarContainerType: SideBarContainerType.Embed,
    74.       isShowSideBar: this.isShowSidebar,
    75.       $isShowSideBar: (isShowSidebar: boolean) => {
    76.         this.isShowSidebar = !isShowSidebar
    77.       },
    78.     })
    79.   }
    80.   @Builder
    81.   build() {
    82.     Stack() {
    83.       this.HDSSideBarBuilder()
    84.     }
    85.   }
    86. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-sidebar-overlay-mode "设置overlay模式的侧边栏")
# 侧边栏菜单样式

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置侧边栏菜单样式。

[HdsSideMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdssidemenu)提供一种菜单栏样式组件。设置侧边栏对应的一级菜单和二级菜单，并显示其新消息数量。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163821.65787876968171477945037251725857:50001231000000:2800:68FC593E828FC9876C7A1C5E26B6CF4F3F532D3EA134918D91E595D49E447255.png "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsSideMenu, HdsSideMenuMainItem, HdsSideMenuSubItem, HdsSideMenuBadgeParam, HdsSideBar } from '@kit.UIDesignKit';
    2. import { SymbolGlyphModifier } from '@kit.ArkUI';
    
2. 设置对应的一级菜单和二级菜单，并显示其新消息数量。
    
    1. @Entry
    2. @ComponentV2
    3. struct Index {
    4.   @Local showControlButton: boolean = true;
    5.   @Local sideBarMask: boolean = false;
    6.   @Local autoHide: boolean = true;
    7.   @Local barStateTypeText: string = "Select BarState";
    8.   @Local widthIndex: number = 0;
    9.   @Local badgeNumber: HdsSideMenuBadgeParam = { count: 50 };
    10.   @Local useTheme: boolean = false;
    11.   @Local selectedIndex: number = 2;
    12.   @Local selectedTransparency: number = 0.6;
    13.   @Local str: string = "短信";
    14.   @Local isShowSidebar: boolean = true;
    15.   listOptionsDefault?: HdsSideMenuMainItem[] = [
    16.     new HdsSideMenuMainItem(
    17.       {
    18.         symbol: new SymbolGlyphModifier($r('sys.symbol.ohos_folder_badge_plus')).fontSize(14),
    19.         label: $r('sys.string.TextView_engr_phone'),
    20.       }),
    21.     new HdsSideMenuMainItem({
    22.       icon: $r('sys.symbol.person_wave_3'),
    23.       label: 'Tuesday',
    24.       hdsSideMenuSubItem: [
    25.         new HdsSideMenuSubItem({ label: this.str, badge: this.badgeNumber })],
    26.     }),
    27.     new HdsSideMenuMainItem({
    28.       symbol: new SymbolGlyphModifier($r('sys.symbol.person_crop_circle_fill_1')),
    29.       label: 'Wednesday',
    30.     }),
    31.   ]
    32.   @Builder
    33.   SideBarPanelBuilder() {
    34.     Column() {
    35.       HdsSideMenu({
    36.         items: this.listOptionsDefault,
    37.         selectedIndex: this.selectedIndex,
    38.         $selectedIndex: (selectedIndex: number) => {
    39.           this.selectedIndex = selectedIndex;
    40.         },
    41.       })
    42.     }
    43.     .height('100%')
    44.   }
    45.   //右侧内容区
    46.   @Builder
    47.   ContentPanelBuilder() {
    48.     Column() {
    49.       Column() {
    50.         Button() {
    51.           SymbolGlyph(this.isShowSidebar ? $r('sys.symbol.open_sidebar') : $r('sys.symbol.close_sidebar'))
    52.             .fontWeight(FontWeight.Normal)
    53.             .fontSize($r('sys.float.ohos_id_text_size_headline7'))
    54.             .fontColor([$r('sys.color.ohos_id_color_titlebar_icon')])
    55.             .hitTestBehavior(HitTestMode.None)
    56.         }
    57.         .backgroundColor($r('sys.color.ohos_id_color_button_normal'))
    58.         .height(24)
    59.         .width(24)
    60.         .animation({ curve: Curve.Sharp, duration: 100 })
    61.         .onClick(() => {
    62.           this.isShowSidebar = !this.isShowSidebar;
    63.         })
    64.       }
    65.     }
    66.     .height('100%')
    67.     .width('100%')
    68.   }
    69.   @BuilderParam sideBarBuilder: () => void = this.SideBarPanelBuilder
    70.   @BuilderParam contentBuilder: () => void = this.ContentPanelBuilder
    71.   @Builder
    72.   build() {
    73.     Column() {
    74.       HdsSideBar({
    75.         sideBarPanelBuilder: (): void => {
    76.           this.sideBarBuilder()
    77.         },
    78.         contentPanelBuilder: (): void => {
    79.           this.contentBuilder()
    80.         },
    81.         isShowSideBar: this.isShowSidebar,
    82.         $isShowSideBar: (isShowSidebar: boolean) => {
    83.           this.isShowSidebar = !isShowSidebar
    84.         },
    85.       })
    86.     }
    87.   }
    88. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-sidebar-enbed-mode "设置embed模式的侧边栏")
# 设置页签栏的模糊样式

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置页签栏的模糊样式。

[HdsTabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdstabs)容器组件扩展支持页签栏设置直接模糊和渐变模糊效果。

- 直接模糊

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163837.91884881813328780648665636809193:50001231000000:2800:D9CD3E364FDF2C4536109E6E6F9B37244570D1CCE1278D33066A5E69580C64D1.png "点击放大")

- 渐变模糊

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163837.48914251747541471266950515679926:50001231000000:2800:2C28D505481F175E4671BB990C33155AF7CF41BEE97CCEF8F55CBC87E8F4F175.jpg "点击放大")

## 约束条件

1. 依赖页签栏位于容器底部，barPosition设置为BarPosition.End，vertical设置为false。
2. TabBar叠加在TabContent之上，barOverlap设置为true。
3. 去掉TabBar节点，barBackgroundBlurStyle默认设置的模糊的属性值为BlurStyle.NONE。

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsTabs, HdsTabsController, HdsTabsAttribute } from '@kit.UIDesignKit';
    
2. 创建Hds一级容器组件，设置HdsTabs组件的barBackgroundStyle样式，可以自定义模糊的颜色和高度，实现渐变模糊。
    
    说明
    
    1. 当开发者通过Tabs组件属性barBackgroundBlurStyle设置模糊时，HdsTabs的默认模糊效果失效。
    2. 当开发者通过Tabs组件属性barBackgroundEffect设置模糊时，HdsTabs的默认模糊效果失效。
    3. 当开发者通过Tabs组件属性barBackgroundColor设置背景色时，HdsTabs的默认模糊效果只有模糊半径生效，模糊半径为80vp。
    
    4. @Entry
    5. @Component
    6. struct Index {
    7.   private controller: HdsTabsController = new HdsTabsController();
    
    8.   build() {
    9.     Column() {
    10.       HdsTabs({ controller: this.controller }) {
    11.         TabContent() {
    12.           Column().width('100%').height('100%').backgroundColor(Color.Pink)
    13.         }
    14.         .tabBar({ icon: $r('app.media.startIcon'), text: '页签1' })
    
    15.         TabContent() {
    16.           Column().width('100%').height('100%').backgroundColor(Color.Blue)
    17.         }
    18.         .tabBar({ icon: $r('app.media.startIcon'), text: '页签2' })
    19.       }
    20.       .barOverlap(true)
    21.       .barPosition(BarPosition.End)
    22.       .vertical(false)
    23.       .barBackgroundStyle({
    24.         maskColor: Color.Yellow,
    25.         maskHeight: 80
    26.       })
    27.     }
    28.   }
    29. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-hds-tabs-split-line "设置页签栏的分割线")
# 设置页签栏的模糊样式

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置页签栏的模糊样式。

[HdsTabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdstabs)容器组件扩展支持页签栏设置直接模糊和渐变模糊效果。

- 直接模糊

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163837.91884881813328780648665636809193:50001231000000:2800:D9CD3E364FDF2C4536109E6E6F9B37244570D1CCE1278D33066A5E69580C64D1.png "点击放大")

- 渐变模糊

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163837.48914251747541471266950515679926:50001231000000:2800:2C28D505481F175E4671BB990C33155AF7CF41BEE97CCEF8F55CBC87E8F4F175.jpg "点击放大")

## 约束条件

1. 依赖页签栏位于容器底部，barPosition设置为BarPosition.End，vertical设置为false。
2. TabBar叠加在TabContent之上，barOverlap设置为true。
3. 去掉TabBar节点，barBackgroundBlurStyle默认设置的模糊的属性值为BlurStyle.NONE。

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsTabs, HdsTabsController, HdsTabsAttribute } from '@kit.UIDesignKit';
    
2. 创建Hds一级容器组件，设置HdsTabs组件的barBackgroundStyle样式，可以自定义模糊的颜色和高度，实现渐变模糊。
    
    说明
    
    1. 当开发者通过Tabs组件属性barBackgroundBlurStyle设置模糊时，HdsTabs的默认模糊效果失效。
    2. 当开发者通过Tabs组件属性barBackgroundEffect设置模糊时，HdsTabs的默认模糊效果失效。
    3. 当开发者通过Tabs组件属性barBackgroundColor设置背景色时，HdsTabs的默认模糊效果只有模糊半径生效，模糊半径为80vp。
    
    4. @Entry
    5. @Component
    6. struct Index {
    7.   private controller: HdsTabsController = new HdsTabsController();
    
    8.   build() {
    9.     Column() {
    10.       HdsTabs({ controller: this.controller }) {
    11.         TabContent() {
    12.           Column().width('100%').height('100%').backgroundColor(Color.Pink)
    13.         }
    14.         .tabBar({ icon: $r('app.media.startIcon'), text: '页签1' })
    
    15.         TabContent() {
    16.           Column().width('100%').height('100%').backgroundColor(Color.Blue)
    17.         }
    18.         .tabBar({ icon: $r('app.media.startIcon'), text: '页签2' })
    19.       }
    20.       .barOverlap(true)
    21.       .barPosition(BarPosition.End)
    22.       .vertical(false)
    23.       .barBackgroundStyle({
    24.         maskColor: Color.Yellow,
    25.         maskHeight: 80
    26.       })
    27.     }
    28.   }
    29. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-hds-tabs-split-line "设置页签栏的分割线")
# 设置侧边栏半屏居中对齐样式

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置侧边栏半屏居中对齐样式。

[HdsTabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdstabs)容器组件侧边栏支持半屏居中对齐布局。横向Tabs时，若没有主动设置TabBar高度，则TabBar默认高度为48vp，纵向TabBar默认宽度为96vp，barHeight设成固定值后，TabBar无法扩展底部安全区。当safeAreaPadding不设置bottom或者bottom设置为0时，可以实现扩展安全区。

- 半屏居中对齐布局

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163845.38167013487981012849979376582919:50001231000000:2800:04C65E44D2219B9258DEFC6C07207BD177F06A0DDB5D5EDDABF1DD1142D52E6D.png "点击放大")

- 默认横向和纵向宽度

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163846.41489334582998579994233628758485:50001231000000:2800:FBC8A25E52BA0C76E4629B72DB501BE6E70197FA6D45277A52A6AAA9EF710D4C.png "点击放大")

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163846.13033731108689446256783540133307:50001231000000:2800:F027F2ADACE3F0B00AF688495E894CADCD11EA8C77471FD22EF9A46BC59AA61C.png "点击放大")

## 约束条件

1. 依赖页签位于侧边栏，vertical设置为true。
2. 页签使用BottomTabBarStyle样式。

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsTabs, HdsTabsAttribute, ExtendBarMode } from '@kit.UIDesignKit';
    
2. 创建Hds一级容器组件，设置HdsTabs组件的barMode样式为ExtendBarMode.HALF_SCREEN_FIXED，所有页签总高度之和为HdsTabs组件高度的四分之一，且处在二分之一屏的居中位置。
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   @State isVertical: boolean = false;
    
    5.   build() {
    6.     Column() {
    7.       Column() {
    8.         Row() {
    9.           Button('verticalChange')
    10.             .onClick(() => {
    11.               this.isVertical = !this.isVertical;
    12.             })
    13.         }
    14.       }
    15.       .margin({ top: 20 })
    16.       .width('100%')
    17.       .height('10%')
    18.       HdsTabs({ barPosition: BarPosition.End }) {
    19.         TabContent() {
    20.           Column().width('100%').height('100%').backgroundColor(Color.Yellow)
    21.         }
    22.         .tabBar(new BottomTabBarStyle($r('sys.media.ohos_app_icon'), 'Yellow'))
    23.         TabContent() {
    24.           Column().width('100%').height('100%').backgroundColor(Color.Blue)
    25.         }
    26.         .tabBar(new BottomTabBarStyle($r('sys.media.ohos_app_icon'), 'Blue'))
    27.         TabContent() {
    28.           Column().width('100%').height('100%').backgroundColor(Color.Pink)
    29.         }
    30.         .tabBar(new BottomTabBarStyle($r('sys.media.ohos_app_icon'), 'Pink'))
    31.       }
    32.       .vertical(this.isVertical)
    33.       .barMode(ExtendBarMode.HALF_SCREEN_FIXED)
    34.       .width('100%')
    35.       .height('90%')
    36.     }
    37.   }
    38. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-hds-tabs-icon-bleed-substyle "设置页签的图标出血样式")
# 设置常驻通知弹窗

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置常驻通知弹窗。

[HdsSnackBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdssnackbar)支持常驻通知弹窗。当应用开发者需要常驻通知提醒弹窗时，可以通过HdsSnackBar的show方法显示HdsSnackBar弹窗，设置duration是-1表示常驻弹窗。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163831.37585300038647925437690660991221:50001231000000:2800:63E8E33772352A085FBEBAAE00E1C84BD58855DBA2E25F9F4F809690293F9FEA.gif "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import {
    2.   HdsSnackBar,
    3.   SnackBarIconOptions,
    4.   SnackBarMessageOptions,
    5.   SnackBarOperationOptions,
    6.   SnackBarStyleOptions,
    7.   SnackBarOperationType
    8. } from '@kit.UIDesignKit'
    
2. 创建UIContext，创建HdsSnackBar对象hdsSnackBar，调用HdsSnackBar对象的show方法可以显示HdsSnackBar弹窗，入参是左侧图标icon、中间文本message、右侧操作区operation、样式style，其中右侧操作区设置类型是带有关闭按钮的文本按钮，其中style中设置duration是-1表示HdsSnackBar弹窗常驻。
3. 设置textButtonId和nextFocusId两个属性，支持开发者自定义Tab键走焦能力。
    
    1. @Entry
    2. @ComponentV2
    3. struct TestSnackBar {
    4.   uiContext: UIContext = this.getUIContext();
    5.   hdsSnackBar: HdsSnackBar = new HdsSnackBar(this.uiContext);
    6.   icon: SnackBarIconOptions = {
    7.     icon: $r('sys.symbol.checkmark_circle')
    8.   }
    9.   message: SnackBarMessageOptions = {
    10.     title: $r('sys.string.ohos_id_text_location_button_description_current_position'),
    11.     content: $r('sys.string.ohos_id_text_save_button_description_save')
    12.   }
    13.   operation: SnackBarOperationOptions = {
    14.     operationType: SnackBarOperationType.TEXT_WITH_CLOSE,
    15.     content: $r('sys.string.ohos_id_text_save_button_description_save_image'),
    16.     textButtonId: 'snackBarTextButton'
    17.   }
    18.   style: SnackBarStyleOptions = {
    19.     nextFocusId: 'button',
    20.     duration: -1
    21.   }
    
    22.   build() {
    23.     Column() {
    24.       Blank()
    25.         .height(400)
    26.       Button('右侧操作区是文字按钮和关闭按钮的SnackBar弹窗，常驻')
    27.         .onClick(() => {
    28.           this.hdsSnackBar.show(this.icon, this.message, this.operation, this.style);
    29.         })
    30.         .id("button")
    
    31.       Button('关注')
    32.         .nextFocus({
    33.           // 这里forward的id必须和SnackBarOperationOptions接口中传入的textButtonId相同
    34.           forward: 'snackBarTextButton'
    35.         })
    36.     }
    37.     .width('100%')
    38.     .height('100%')
    39.     .backgroundColor(0xF1F3F5)
    40.   }
    41. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-snackbar "即时操作")
# 设置定时通知弹窗

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置定时通知弹窗。

[HdsSnackBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdssnackbar)支持定时通知弹窗。当应用开发者需要定时通知提醒弹窗时，可以通过HdsSnackBar的show方法显示HdsSnackBar弹窗，设置duration是大于0的时间表示弹窗是定时消失的，默认定时时间是5000ms。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163838.13176296106524815305323963269961:50001231000000:2800:A02AABBDCB26CCFD33129BFB754E5D2A3B57F95EE641D4E8B532C99C3783DF62.gif "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import {
    2.   HdsSnackBar,
    3.   SnackBarIconOptions,
    4.   SnackBarMessageOptions,
    5.   SnackBarOperationOptions,
    6.   SnackBarStyleOptions,
    7.   SnackBarOperationType
    8. } from '@kit.UIDesignKit'
    
2. 创建UIContext，创建HdsSnackBar对象hdsSnackBar，调用HdsSnackBar对象的show方法可以显示HdsSnackBar弹窗，入参是左侧图标icon、中间文本message、右侧操作区operation、样式style，其中右侧操作区设置类型是带有右箭头的文本按钮，其中style中设置duration是2000ms表示HdsSnackBar弹窗2秒后定时消失。
3. 设置arrowButtonId和nextFocusId两个属性，支持开发者自定义Tab键走焦能力。
    
    1. @Entry
    2. @ComponentV2
    3. struct TestSnackBar02 {
    4.   uiContext: UIContext = this.getUIContext();
    5.   hdsSnackBar: HdsSnackBar = new HdsSnackBar(this.uiContext);
    6.   icon: SnackBarIconOptions = {
    7.     icon: $r('sys.symbol.checkmark_circle')
    8.   }
    9.   message: SnackBarMessageOptions = {
    10.     title: $r('sys.string.ohos_id_text_location_button_description_current_position'),
    11.     content: $r('sys.string.ohos_id_text_save_button_description_save')
    12.   }
    13.   operation: SnackBarOperationOptions = {
    14.     operationType: SnackBarOperationType.TEXT_WITH_ARROW,
    15.     content: $r('sys.string.ohos_id_text_save_button_description_save_image'),
    16.     arrowButtonId: 'snackBarArrowButton'
    17.   }
    18.   style: SnackBarStyleOptions = {
    19.     nextFocusId: 'button',
    20.     duration: 2000
    21.   }
    
    22.   build() {
    23.     Column() {
    24.       Blank()
    25.         .height(400)
    26.       Button('文字按钮和右箭头的SnackBar弹窗，2秒后定时消失')
    27.         .onClick(() => {
    28.           this.hdsSnackBar.show(this.icon, this.message, this.operation, this.style);
    29.         })
    30.         .id("button")
    
    31.       Button('关注')
    32.         .nextFocus({
    33.           // 这里forward的id必须和SnackBarOperationOptions接口中传入的arrowButtonId相同
    34.           forward: 'snackBarArrowButton'
    35.         })
    36.     }
    37.     .width('100%')
    38.     .height('100%')
    39.     .backgroundColor(0xF1F3F5)
    40.   }
    41. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-snackbar-resident-notification "设置常驻通知弹窗")
# 设置有主按钮的组件

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置有主按钮的组件。

[HdsActionBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsactionbar)组件支持多个按钮的样式。当应用开发者需要多个按钮并且有主按钮，支持展开和收缩的动效时，可以通过设置主按钮配置样式。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163831.91627262502748734569881372246375:50001231000000:2800:EF07990F350B1156779F067ED39E512EB54EBE9C2D4BB11FC524F80C23347618.gif)

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsActionBar, ActionBarButton, ActionBarStyle } from '@kit.UIDesignKit'
    
2. 创建左边的按钮数组startButtons，创建右边的按钮数组endButtons，创建主按钮primaryButton，设置isExpand初始值是true表示HdsActionBar的初始状态是展开状态，点击主按钮会收起，再次点击可以展开。
    
    1. @Entry
    2. @ComponentV2
    3. struct TestActionBar {
    4.   @Local isExpand: boolean = true;
    
    5.   @Local isPrimaryIconChanged: boolean = false;
    
    6.   @Local primaryHoverTips: ResourceStr = '开始';
    
    7.   build() {
    8.     Column() {
    9.       HdsActionBar({
    10.         startButtons: [new ActionBarButton({
    11.           baseIcon: $r('sys.symbol.stopwatch_fill')
    12.         })],
    13.         endButtons: [new ActionBarButton({
    14.           baseIcon: $r('sys.symbol.mic_fill')
    15.         })],
    16.         primaryButton: new ActionBarButton({
    17.           baseIcon: $r('sys.symbol.plus'),
    18.           altIcon: $r('sys.symbol.play_fill'),
    19.           onClick: () => {
    20.             this.isExpand = !this.isExpand;
    21.             this.isPrimaryIconChanged = !this.isPrimaryIconChanged;
    22.             if (this.isPrimaryIconChanged) {
    23.               this.primaryHoverTips = '暂停';
    24.             } else {
    25.               this.primaryHoverTips = '开始';
    26.             }
    27.           },
    28.           hoverTips: this.primaryHoverTips
    29.         }),
    30.         actionBarStyle: new ActionBarStyle({
    31.           isPrimaryIconChanged: this.isPrimaryIconChanged
    32.         }),
    33.         isExpand: this.isExpand!!
    34.       })
    35.     }
    36.     .width('100%')
    37.     .height('100%')
    38.     .backgroundColor(0xF1F3F5)
    39.     .justifyContent(FlexAlign.Center)
    40.     .alignItems(HorizontalAlign.Center)
    41.   }
    42. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-actionbar "核心操作栏")
# 设置无主按钮的组件

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置无主按钮的组件。

[HdsActionBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsactionbar)组件支持多个按钮的样式。当应用开发者需要多个按钮并且没有主按钮，没有展开和收缩的动效时，可以通过设置左按钮和右按钮配置样式。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163838.38837401383002691842426628135940:50001231000000:2800:2BCA9CB6C4065510A4A30AD0D1DABBA29878BBBFF618187FA067C87F28C31C74.png)

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsActionBar, ActionBarButton } from '@kit.UIDesignKit'
    
2. 创建左边的按钮数组startButtons，创建右边的按钮数组endButtons，无主按钮，不支持切换展开和收缩状态。
    
    1. @Entry
    2. @ComponentV2
    3. struct TestNoPrimaryButton {
    
    4.   build() {
    5.     Column() {
    6.       HdsActionBar({
    7.         startButtons: [new ActionBarButton({
    8.           baseIcon: $r('sys.symbol.stopwatch_fill')
    9.         }), new ActionBarButton({
    10.           baseIcon: $r('sys.symbol.stopwatch_fill')
    11.         })],
    12.         endButtons: [new ActionBarButton({
    13.           baseIcon: $r('sys.symbol.mic_fill')
    14.         })]
    15.       })
    16.     }
    17.     .width('100%')
    18.     .height('100%')
    19.     .backgroundColor(0xF1F3F5)
    20.     .justifyContent(FlexAlign.Center)
    21.     .alignItems(HorizontalAlign.Center)
    22.   }
    23. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-actionbar-main-buttons "设置有主按钮的组件")
# 设置无主按钮的组件

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置无主按钮的组件。

[HdsActionBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsactionbar)组件支持多个按钮的样式。当应用开发者需要多个按钮并且没有主按钮，没有展开和收缩的动效时，可以通过设置左按钮和右按钮配置样式。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163838.38837401383002691842426628135940:50001231000000:2800:2BCA9CB6C4065510A4A30AD0D1DABBA29878BBBFF618187FA067C87F28C31C74.png)

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsActionBar, ActionBarButton } from '@kit.UIDesignKit'
    
2. 创建左边的按钮数组startButtons，创建右边的按钮数组endButtons，无主按钮，不支持切换展开和收缩状态。
    
    1. @Entry
    2. @ComponentV2
    3. struct TestNoPrimaryButton {
    
    4.   build() {
    5.     Column() {
    6.       HdsActionBar({
    7.         startButtons: [new ActionBarButton({
    8.           baseIcon: $r('sys.symbol.stopwatch_fill')
    9.         }), new ActionBarButton({
    10.           baseIcon: $r('sys.symbol.stopwatch_fill')
    11.         })],
    12.         endButtons: [new ActionBarButton({
    13.           baseIcon: $r('sys.symbol.mic_fill')
    14.         })]
    15.       })
    16.     }
    17.     .width('100%')
    18.     .height('100%')
    19.     .backgroundColor(0xF1F3F5)
    20.     .justifyContent(FlexAlign.Center)
    21.     .alignItems(HorizontalAlign.Center)
    22.   }
    23. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-actionbar-main-buttons "设置有主按钮的组件")
# 设置附带横滑的列表样式

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置附带横滑的列表样式。

应用使用[HdsListItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdslistitem)组件实现多设备上的系统列表的横滑动效按钮的内容和样式。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163831.11981623124704216604411609100323:50001231000000:2800:560219EED3E1CBE82FC810BB7F30E860650326EC3B4E9FFF23C0E34A15BB0603.gif "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import { promptAction, SymbolGlyphModifier, TextModifier } from '@kit.ArkUI';
    2. import { HdsListItem } from '@kit.UIDesignKit';
    
2. 简单配置页面的布局，调用HdsListItem的接口绘制列表的横滑动效按钮的内容和样式。
    
    1. @Entry
    2. @Component
    3. struct HdsListItemExample {
    4.   @State dataSource: LazyDataSource<Item> = new LazyDataSource();
    5.   @State dataArr: Array<Item> = [];
    6.   @State EndOffset: number = 0;
    7.   private scroller: Scroller = new Scroller();
    
    8.   build() {
    9.     Column() {
    10.       List({ space: 10, scroller: this.scroller }) {
    11.         LazyForEach(this.dataSource, (item: Item) => {
    12.           HdsListItem({
    13.             hdsListItemCard: {
    14.               textItem: {
    15.                 primaryText: {
    16.                   text: 'Primary Text',
    17.                   modifier: new TextModifier().fontColor(Color.Orange).fontSize(16),
    18.                 }
    19.               }
    20.             },
    21.             swipeActionOptions: {
    22.               icons: [
    23.                 {
    24.                   icon: new SymbolGlyphModifier($r('sys.symbol.share')).fontColor([Color.Red]).fontSize(16),
    25.                   backgroundColor: Color.Green,
    26.                   onAction: () => {
    27.                     promptAction.openToast({ message: '点击share按钮', duration: 100 });
    28.                   },
    29.                 },
    30.                 {
    31.                   icon: new SymbolGlyphModifier($r('sys.symbol.plus_square_on_square')),
    32.                   backgroundColor: Color.Orange,
    33.                   onAction: () => {
    34.                     promptAction.openToast({ message: '点击copy按钮', duration: 100 });
    35.                   },
    36.                 },
    37.                 {
    38.                   icon: new SymbolGlyphModifier($r('sys.symbol.plus_square_dashed_on_square'))
    39.                           .symbolEffect(new BounceSymbolEffect(), true),
    40.                   onAction: () => {
    41.                     promptAction.openToast({ message: '点击paste按钮', duration: 100 });
    42.                   },
    43.                 },
    44.               ],
    45.               deleteIconOptions: {
    46.                 backgroundColor: Color.Red, //  ---修改背景色
    47.                 iconColor: Color.Gray, //  ---- 修改垃圾桶的颜色
    48.                 onAction: () => {
    49.                   promptAction.openToast({ message: '点击删除按钮', duration: 100 });
    50.                 }, //   --点击回调
    51.               },
    52.               fullDeleteOptions: {
    53.                 isFullDelete: true, // --- 划动距离超过划出组件大小后自动触发删除，默认是false
    54.                 onFullDeleteAction: () => {
    55.                   promptAction.openToast({ message: '触发自动删除', duration: 100 });
    56.                   this.getUIContext()?.animateTo({
    57.                     duration: 350,
    58.                   }, () => {
    59.                     this.dataSource.deleteItem(item)
    60.                   });
    61.                 }, //   -- 触发删除时的回调
    62.               },
    63.             }
    64.           })
    65.         }, (item: Item) => item.data)
    66.       }
    67.       .scrollBar(BarState.Off)
    68.       .onDidScroll((scrollOffset: number) => {
    69.         this.EndOffset = scrollOffset
    70.       })
    71.       .margin(10)
    72.       .width('100%')
    73.       .height('100%')
    74.     }
    75.     .backgroundColor('#0D182431')
    76.     .width('100%')
    77.     .height('100%')
    78.   }
    
    79.   aboutToAppear() {
    80.     for (let i = 0; i < 2; i++) {
    81.       this.dataSource.pushItem(new Item(i + ''));
    82.       this.dataArr.push(new Item(i + ''));
    83.     }
    84.   }
    85. }
    
    86. class Item {
    87.   constructor(data: string) {
    88.     this.data = data;
    89.   }
    
    90.   public data: string = '';
    91. }
    
    92. export class LazyDataSource<T> implements IDataSource {
    93.   private elements: T[];
    94.   private listeners: Set<DataChangeListener>;
    
    95.   constructor(elements: T[] = []) {
    96.     this.elements = elements;
    97.     this.listeners = new Set();
    98.   }
    
    99.   public totalCount(): number {
    100.     return this.elements.length;
    101.   }
    
    102.   public getData(index: number): T {
    103.     return this.elements[index];
    104.   }
    
    105.   public indexOf(item: T): number {
    106.     return this.elements.indexOf(item);
    107.   }
    
    108.   public pinItem(item: T, index: number): void {
    109.     this.elements.splice(index, 1);
    110.     this.elements.unshift(item);
    111.     this.listeners.forEach(listener => listener.onDataReloaded());
    112.   }
    
    113.   public pushItem(item: T) {
    114.     this.elements.push(item);
    115.     this.listeners.forEach(listener => listener.onDataAdd(this.elements.length - 1));
    116.   }
    
    117.   public deleteItem(item: T): void {
    118.     const index = this.elements.indexOf(item);
    119.     if (index < 0) {
    120.       return;
    121.     }
    122.     this.elements.splice(index, 1);
    123.     this.listeners.forEach(listener => listener.onDataDelete(index));
    124.   }
    
    125.   public deleteItemByIndex(index: number): void {
    126.     this.elements.splice(index, 1);
    127.     this.listeners.forEach(listener => listener.onDataDelete(index));
    128.   }
    
    129.   public registerDataChangeListener(listener: DataChangeListener): void {
    130.     this.listeners.add(listener);
    131.   }
    
    132.   public unregisterDataChangeListener(listener: DataChangeListener): void {
    133.     this.listeners.delete(listener);
    134.   }
    135. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-list-item-card "列表")
# 设置列表卡片样式

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持设置列表卡片样式。

应用使用[HdsListItemCard](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdslistitemcard)组件实现多设备上的系统列表样式。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163838.18405688528397624436695207856184:50001231000000:2800:43AD94ACB759527889A8F5B3E6BA09F445E9F42109D2281C5A20D9BBD3961E2D.jpg "点击放大")

## 开发步骤

1. 导入相关模块。
    
    1. import { HdsListItemCard, PrefixImage, SuffixSwitch} from '@kit.UIDesignKit';
    2. import { promptAction } from '@kit.ArkUI';
    
2. 创建HdsListItemCard组件，设置左边为Image，中间为Text，右边为Switch的场景。
    
    1. @Entry
    2. @Component
    3. struct Test {
    4.   private scroller: ListScroller = new ListScroller();
    
    5.   build() {
    6.     Column() {
    7.       List({ space: 10, scroller: this.scroller }) {
    8.         ListItem() {
    9.           HdsListItemCard({
    10.             // A区图片
    11.             prefixItem: new PrefixImage({
    12.               image: $r('app.media.background'),
    13.               onClick: () => {
    14.                 promptAction.openToast({ message: 'left image' });
    15.               }
    16.             }),
    17.             // B区文本
    18.             textItem: {
    19.               primaryText: {
    20.                 text: 'Primary Text'
    21.               },
    22.               secondaryText: {
    23.                 text: 'Secondary Text'
    24.               },
    25.               description: {
    26.                 text: 'Description Text'
    27.               }
    28.             },
    29.             // C区Switch
    30.             suffixItem: new SuffixSwitch({
    31.               isCheck: false,
    32.               onChange: (num: boolean) => {
    33.                 if (num) {
    34.                   promptAction.openToast({ message: 'switch is true' });
    35.                 } else {
    36.                   promptAction.openToast({ message: 'switch is false' });
    37.                 }
    38.               }
    39.             }),
    40.             onClick: () => {
    41.               promptAction.openToast({ message: 'hdslistitem' });
    42.             }
    43.           })
    44.         }
    45.       }
    46.       .width('100%')
    47.       .height('100%')
    48.       .margin(10)
    49.     }.backgroundColor(0x1a0a59f7).height('100%')
    50.   }
    51. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-set-hds-slide-horizon-listitem "设置附带横滑的列表样式")
# 资源注册

更新时间: 2025-12-16 16:38

## 场景介绍

从5.1.1 (19)版本开始，新增支持资源注册。

适用于需要快速定制应用内[Symbol图标](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-symbolregister)，不想强依赖于系统版本中预制的系统Symbol图标资源。

## 约束条件

资源注册支持Phone、Tablet、PC/2in1设备，并且从5.1.1(19)版本开始，新增支持TV设备。

## 开发步骤

1. 将UX设计师提供的Symbol图标资源（TTF文件）与动效参数资源（JSON文件）放入entry/src/main/resources/rawfile下，可新建目录。
    
    说明：[Symbol资源设计规范](https://developer.huawei.com/consumer/cn/doc/design-guides/system-icons-0000001929854962)
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163831.27786259012748336933439011955244:50001231000000:2800:161DCFBAECE4295FE3DC72573E8A56C01B0243CF9CEAA3C2D1696362EBE2B03E.png "点击放大")
    
2. 多语言场景，在entry/src/main/resources目录中对应语言目录下的string.json文件中配置对应的Symbol图标Unicode值。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163831.94292368103071999432850900645519:50001231000000:2800:5FAD4CCB6292667B4CDE7DDBC1E8605EDA5855CF1600545CF9AAE3AFBADB2486.png)
    
    1. {
    2.   "string": [
    3.     {
    4.       "name": "symbol_custom_phone_fill_1",
    5.       "value": "0x100016"
    6.     }
    7.   ]
    8. }
    
3. 导入相关模块。
    
    1. import { symbolRegister } from '@kit.UIDesignKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
4. 在通过SymbolGlyph/SymbolSpan组件展示自定义Symbol图标前，需要注册加载图标资源与动效参数资源。
    
    1. try {
    2.   let result = symbolRegister.registerSymbol($rawfile("symbol/symbol_register.ttf"), $rawfile("symbol/symbol_register.json"));
    3. } catch (error) {
    4.   let err = error as BusinessError;
    5.   console.error("errCode: " + err.code)
    6.   console.error("error: " + err.message);
    7. }
    
5. 在需要展示自定义Symbol图标的页面通过SymbolGlyph/SymbolSpan组件展示该图标。
    
    1. struct test {
    2.   build() {
    3.     Column(){
    4.       SymbolGlyph($r('app.string.symbol_custom_phone_fill_1'))
    5.     }
    6.   }
    7. }
    

## 开发实例

1. import { symbolRegister } from '@kit.UIDesignKit';
2. import { BusinessError } from '@ohos.base';

3. @Entry
4. @Component
5. struct test {
6.   aboutToAppear(): void {
7.     try {
8.       let result = symbolRegister.registerSymbol($rawfile("symbol/symbol_register.ttf"), $rawfile("symbol/symbol_register.json"));
9.     } catch (error) {
10.       let err = error as BusinessError;
11.       console.error("errCode: " + err.code)
12.       console.error("error: " + err.message);
13.     }
14.   }
15.   build() {
16.     Column(){
17.       SymbolGlyph($r('app.string.symbol_custom_phone_fill_1'))
18.     }
19.   }
20. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163831.39014887776557122940678314319086:50001231000000:2800:28DD14FEC144585C17119593B5A3D63184646C6C78531C428F527A2D8E5AEC5D.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-config-custom-symbol "应用加载自定义Symbol")
# 点光源效果

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持[点光源效果](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdseffect#section285511175574)。

通过点光源接口可以设置组件的发光效果以及被照亮的受光效果，使得组件交互体验更显沉浸。

## 约束与限制

单个组件最多同时受12个光源照亮。

## 开发步骤

1. 导入模块。
    
    1. import { hdsEffect } from '@kit.UIDesignKit';
    
2. 创建点光源发光效果。如果需要发光，配置sourceType属性；如果需要被照亮，配置illuminatedType属性。
    
    以下代码表示：当中间的Button点击时，产生点光源效果，重复点击触发不同点光源效果。
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   @State bloomValue: number = 0;
    5.   @State index: number = 0;
    6.   @State illuminatedType: hdsEffect.PointLightIlluminatedType = hdsEffect.PointLightIlluminatedType.NONE;
    7.   @State button_gradient_state: hdsEffect.PressShadowType = hdsEffect.PressShadowType.NONE;
    8.   @State lightIntensity: number = 10;
    9.   @State types: hdsEffect.PointLightIlluminatedType[] =
    10.     [hdsEffect.PointLightIlluminatedType.NONE, hdsEffect.PointLightIlluminatedType.BORDER,
    11.       hdsEffect.PointLightIlluminatedType.CONTENT, hdsEffect.PointLightIlluminatedType.BORDER_CONTENT,
    12.       hdsEffect.PointLightIlluminatedType.DEFAULT_FEATHERING_BORDER];
    
    13.   build() {
    14.     Flex({
    15.       direction: FlexDirection.Column,
    16.       justifyContent: FlexAlign.Center,
    17.       alignItems: ItemAlign.Center,
    18.     }) {
    19.       // 纵向循环
    20.       ForEach(Array<number>(4).fill(0), (row: number) => {
    21.         Flex({
    22.           direction: FlexDirection.Row,
    23.           justifyContent: FlexAlign.Center,
    24.           alignItems: ItemAlign.Center,
    25.         }) {
    26.           // 横向循环
    27.           ForEach(Array<number>(4).fill(0), (col: number) => {
    28.             Flex()
    29.               .visualEffect(new hdsEffect.HdsEffectBuilder().pointLight({
    30.                 illuminatedType: this.illuminatedType,
    31.               }).buildEffect())
    32.               .backgroundColor(0x808080)
    33.               .size({ width: 60, height: 60 })
    34.               .borderRadius(50)
    35.               .margin({ top: 20, right: 10, left: 10 }) // 添加间距
    36.           })
    37.         }
    38.         .width('100%') // 设置 Row 组件的宽度为 100%
    39.       })
    
    40.       Flex({
    41.         direction: FlexDirection.Row,
    42.         justifyContent: FlexAlign.Center, // 使用 SpaceBetween 来均匀分布间距
    43.         alignItems: ItemAlign.Center,
    44.       }) {
    45.         Flex()
    46.           .visualEffect(new hdsEffect.HdsEffectBuilder().pointLight({
    47.             illuminatedType: this.illuminatedType,
    48.           }).buildEffect())
    49.           .backgroundColor(0x808080)
    50.           .size({ width: 60, height: 60 })
    51.           .borderRadius(50)
    52.           .margin({ top: 20, right: 10, left: 10 })
    
    53.         Button('点击发光')
    54.           .size({ width: 140, height: 60 })
    55.           .backgroundColor(0x808080)
    56.           .fontColor(0xADD8E6)
    57.           .visualEffect(new hdsEffect.HdsEffectBuilder()
    58.             .pressShadow(this.button_gradient_state)
    59.             .pointLight({
    60.               options: {
    61.                 color: Color.White,
    62.                 intensity: this.lightIntensity,
    63.                 height: 150
    64.               }
    65.             })
    66.             .pressShadow(this.button_gradient_state)
    67.             .buildEffect())
    68.           .onClick(() => {
    69.             if (this.index <= 3) {
    70.               this.index++;
    71.               this.illuminatedType = this.types[this.index];
    72.               this.button_gradient_state = hdsEffect.PressShadowType.BLEND_GRADIENT;
    73.             }
    74.             let message = 'NONE';
    75.             if (this.illuminatedType == 1) {
    76.               message = 'BORDER';
    77.             } else if (this.illuminatedType == 2) {
    78.               message = 'CONTENT';
    79.             } else if (this.illuminatedType == 3) {
    80.               message = 'BORDER_CONTENT';
    81.             } else {
    82.               message = 'DEFAULT_FEATHERING_BORDER';
    83.             }
    84.             this.getUIContext().getPromptAction().showToast({
    85.               message: message,
    86.               duration: 2000,
    87.               bottom: '80%'
    88.             });
    89.           })
    90.           .margin({ top: 20, right: 10, left: 10 })
    
    91.         Flex()
    92.           .visualEffect(new hdsEffect.HdsEffectBuilder().pointLight({
    93.             illuminatedType: this.illuminatedType,
    94.           }).buildEffect())
    95.           .backgroundColor(0x808080)
    96.           .size({ width: 60, height: 60 })
    97.           .borderRadius(50)
    98.           .margin({ top: 20, right: 10, left: 10 })
    99.       }
    100.       .width('100%') // 设置 Row 组件的宽度为 100%
    
    101.       ForEach(Array<number>(4).fill(0), (row: number) => {
    102.         Flex({
    103.           direction: FlexDirection.Row,
    104.           justifyContent: FlexAlign.Center,
    105.           alignItems: ItemAlign.Center,
    106.         }) {
    107.           // 横向循环
    108.           ForEach(Array<number>(4).fill(0), (col: number) => {
    109.             Flex()
    110.               .visualEffect(new hdsEffect.HdsEffectBuilder().pointLight({
    111.                 illuminatedType: this.illuminatedType,
    112.               }).buildEffect())
    113.               .backgroundColor(0x808080)
    114.               .size({ width: 60, height: 60 })
    115.               .borderRadius(50)
    116.               .margin({ top: 20, right: 10, left: 10 })
    117.           })
    118.         }
    119.         .width('100%') // 设置 Row 组件的宽度为 100%
    120.       })
    121.     }
    122.     .backgroundColor(Color.Black)
    123.   }
    124. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163831.40145396779540735044245462233238:50001231000000:2800:ED53A0CC0F2FEA2CF15714AE7F0BEF8FE3E83B885BCA8F4605050424D97F9787.png "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-visual-effect "视效")
# 按压阴影

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持[按压阴影](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdseffect#section132615713716)。

通过按压阴影接口可以设置组件的背景色变化效果，一般常用于组件按压交互时的背景色变化场景。

## 开发步骤

1. 导入模块。
    
    1. import { hdsEffect } from '@kit.UIDesignKit';
    
2. 创建按压阴影效果
    
    1. @Entry
    2. @Component
    3. struct PressShadowExample {
    4.   @State button_blend_state: hdsEffect.PressShadowType = hdsEffect.PressShadowType.NONE;
    5.   @State button_gradient_state: hdsEffect.PressShadowType = hdsEffect.PressShadowType.NONE;
    
    6.   build() {
    7.     NavDestination() {
    8.       Column({ space: 50 }) {
    9.         Button("BLEND_WHITE", { buttonStyle: ButtonStyleMode.EMPHASIZED, role: ButtonRole.ERROR, stateEffect: false })
    10.           .visualEffect(new hdsEffect.HdsEffectBuilder()
    11.             .pressShadow(this.button_blend_state)
    12.             .buildEffect())
    13.           .onTouch((event: TouchEvent) => {
    14.             if (event.type === TouchType.Down) {
    15.               this.button_blend_state =  hdsEffect.PressShadowType.BLEND_WHITE;
    16.             } else if (event.type === TouchType.Up || event.type === TouchType.Cancel) {
    17.               this.button_blend_state =  hdsEffect.PressShadowType.NONE;
    18.             }
    19.           })
    
    20.         Button("GRADIENT", { buttonStyle: ButtonStyleMode.NORMAL, stateEffect: false })
    21.           .visualEffect(new hdsEffect.HdsEffectBuilder()
    22.             .pressShadow(this.button_gradient_state)
    23.             .buildEffect())
    24.           .onTouch((event: TouchEvent) => {
    25.             if (event.type === TouchType.Down) {
    26.               this.button_gradient_state =  hdsEffect.PressShadowType.BLEND_GRADIENT;
    27.             } else if (event.type === TouchType.Up || event.type === TouchType.Cancel) {
    28.               this.button_gradient_state =  hdsEffect.PressShadowType.NONE;
    29.             }
    30.           })
    31.       }
    32.       .height('70%')
    33.       .justifyContent(FlexAlign.Center)
    34.     }
    35.     .width('100%')
    36.     .height('100%')
    37.     .title('Button example')
    38.     .backgroundColor('#040404')
    39.   }
    40. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163838.49964906801119010631160101095423:50001231000000:2800:BA15A0A46FD1D90E499FDC2D34FCC299F9CC0ED5E2ED089B77E5636E41D03441.gif)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-visual-effect-point-light "点光源效果")
# 背景流光

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持[背景流光](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdseffect#section139655943218)。

通过背景流光接口可以设置组件的背景流动发光效果，并且可以设置背景色及渐变背景色，常用于全屏幕背景流光等。

## 开发步骤

1. 导入模块。
    
    1. import { hdsEffect } from '@kit.UIDesignKit';
    
2. 设置背景流光效果。
    
    1. @Entry
    2. @Component
    3. struct UVFlowLight {
    4.   @State controller: hdsEffect.ShaderEffectController = new hdsEffect.ShaderEffectController();
    
    5.   build() {
    6.     Stack() {
    7.     }
    8.     .visualEffect(new hdsEffect.HdsEffectBuilder()
    9.       .shaderEffect({
    10.         effectType: hdsEffect.EffectType.UV_BACKGROUND_FLOW_LIGHT,
    11.         animation: {
    12.           duration: 10000,
    13.           iterations: -1,
    14.           autoPlay: true,
    15.           onFinish: ()=> {
    16.             console.info('Succeeded in finishing');
    17.           }
    18.         },
    19.         controller: this.controller,
    20.       })
    21.       .buildEffect())
    22.     .width('100%')
    23.     .height('100%')
    24.   }
    25. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163846.88828913340383578731955837093853:50001231000000:2800:EA749448E96A24EB74947BDAE31CA739520CB8A390AB180A123A474F9A09D9FF.jpg "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-visual-effect-double-edge-streamer "双边边缘流光")
# 背景流光

更新时间: 2025-12-16 16:38

## 场景介绍

从6.0.0(20) Beta1版本开始，新增支持[背景流光](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdseffect#section139655943218)。

通过背景流光接口可以设置组件的背景流动发光效果，并且可以设置背景色及渐变背景色，常用于全屏幕背景流光等。

## 开发步骤

1. 导入模块。
    
    1. import { hdsEffect } from '@kit.UIDesignKit';
    
2. 设置背景流光效果。
    
    1. @Entry
    2. @Component
    3. struct UVFlowLight {
    4.   @State controller: hdsEffect.ShaderEffectController = new hdsEffect.ShaderEffectController();
    
    5.   build() {
    6.     Stack() {
    7.     }
    8.     .visualEffect(new hdsEffect.HdsEffectBuilder()
    9.       .shaderEffect({
    10.         effectType: hdsEffect.EffectType.UV_BACKGROUND_FLOW_LIGHT,
    11.         animation: {
    12.           duration: 10000,
    13.           iterations: -1,
    14.           autoPlay: true,
    15.           onFinish: ()=> {
    16.             console.info('Succeeded in finishing');
    17.           }
    18.         },
    19.         controller: this.controller,
    20.       })
    21.       .buildEffect())
    22.     .width('100%')
    23.     .height('100%')
    24.   }
    25. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163846.88828913340383578731955837093853:50001231000000:2800:EA749448E96A24EB74947BDAE31CA739520CB8A390AB180A123A474F9A09D9FF.jpg "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-visual-effect-double-edge-streamer "双边边缘流光")
# 怎么获取layeredDrawableDescriptor对象信息？

更新时间: 2025-12-16 16:38

应用配置的图标和名称信息，可以通过[resourceManager.getDrawableDescriptor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resource-manager#getdrawabledescriptor10)获取。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-faq "UI Design Kit常见问题")
# 怎么获取layeredDrawableDescriptor对象信息？

更新时间: 2025-12-16 16:38

应用配置的图标和名称信息，可以通过[resourceManager.getDrawableDescriptor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resource-manager#getdrawabledescriptor10)获取。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-faq "UI Design Kit常见问题")
# 怎么获取layeredDrawableDescriptor对象信息？

更新时间: 2025-12-16 16:38

应用配置的图标和名称信息，可以通过[resourceManager.getDrawableDescriptor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resource-manager#getdrawabledescriptor10)获取。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-faq "UI Design Kit常见问题")