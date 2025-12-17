# UI国际化

更新时间: 2025-12-16 16:38

本文介绍如何实现应用程序UI界面的国际化，包含资源配置和镜像布局，关于应用适配国际化的详细参考，请参考[Localization Kit（本地化开发服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/i18n-l10n)。

## 利用资源限定词配置国际化资源

在开发阶段，通过DevEco Studio，可以为应用在对应语言和地区的资源限定词目录下配置不同的资源，来实现UI国际化。详细介绍请参考[资源分类与访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access)。

## 使用镜像能力

不同国家对文本对齐方式和读取顺序有所不同，例如英语采用从左到右的顺序，阿拉伯语和希腊语则采用从右到左（RTL）的顺序。为满足不同用户的阅读习惯，ArkUI提供了镜像能力。在特定情况下将显示内容在X轴上进行镜像反转。

|镜像前|镜像后|
|:--|:--|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163854.00666330128547974406605013115319:50001231000000:2800:888ED075890A7D828F3FF63A2266D0BAC7A4768E9E7AC757EC61010625CB7B52.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163855.93061723300259622196769921879239:50001231000000:2800:B0CBCA1CAB681E05AAD48FA79739180997B676AD040AAB334646D321FAADC237.png)|

当组件满足以下任意条件时，镜像能力生效：

1. 组件的direction属性设置为Direction.Rtl。
    
2. 组件的direction属性设置为Direction.Auto，且当前的系统语言（如维吾尔语）的阅读习惯是从右向左。
    

### 基本概念

- LTR：顺序为从左向右。
- RTL：顺序为从右向左。

### 使用约束

ArkUI 如下能力已默认适配镜像：

|类别|名称|
|:--|:--|
|基础组件|[Swiper](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-swiper)、[Tabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabs)、[TabContent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabcontent)、[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-list)、[Progress](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-progress)、[CalendarPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-calendarpicker)、[CalendarPickerDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-methods-calendarpicker-dialog)、[TextPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textpicker)、[TextPickerDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-methods-textpicker-dialog)、[DatePicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-datepicker)、[DatePickerDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-methods-datepicker-dialog)、[Grid](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-grid)、[WaterFlow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-waterflow)、[Scroll](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-scroll)、[ScrollBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-scrollbar)、[AlphabetIndexer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-alphabet-indexer)、[Stepper](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-stepper)、[SideBarContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-sidebarcontainer)、[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)、[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navdestination)、[Rating](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-rating)、[Slider](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-slider)、[Toggle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-toggle)、[Badge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-badge)、[Counter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-counter)、[Chip](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-chip)、[SegmentButton](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-segmentbutton)、[bindMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-menu#bindmenu)、[bindContextMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-menu#bindcontextmenu8)、[TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput)、[TextArea](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textarea)、[Search](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-search)、[Stack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-stack)、[GridRow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-gridrow)、[Text](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-text)、[Select](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-select)、[Marquee](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-marquee)、[Row](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-row)、[Column](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-column)、[Flex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-flex)、[RelativeContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-relativecontainer)、[ListItemGroup](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-listitemgroup)|
|高级组件|[SelectionMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-selectionmenu) 、[TreeView](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-treeview) 、[Filter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-filter)、[SplitLayout](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-splitlayout)、[ToolBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-toolbar)、[ComposeListItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-composelistitem)、[EditableTitleBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-editabletitlebar)、[ProgressButton](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-progressbutton)、[SubHeader](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-subheader) 、[Popup](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-popup)、[Dialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-dialog)、[SwipeRefresher](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-swiperefresher)|
|通用属性|[position](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-location#position)、[markAnchor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-location#markanchor)、[offset](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-location#offset)、[alignRules](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-location#alignrules12)、[borderWidth](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-border#borderwidth)、[borderColor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-border#bordercolor)、[borderRadius](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-border#borderradius)、[padding](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-size#padding)、[margin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-size#margin)|
|接口|[AlertDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-methods-alert-dialog-box)、[ActionSheet](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-methods-action-sheet)、[promptAction.showDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-promptaction#promptactionshowdialogdeprecated)、[promptAction.showToast](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-promptaction#promptactionshowtoastdeprecated)|

但如下三种场景还需要进行适配：

1. 界面布局、边框设置：关于方向类的通用属性，如果需要支持镜像能力，使用泛化的方向指示词 start/end入参类型替换 left/right、x/y等绝对方向指示词的入参类型，来表示自适应镜像能力。
    
2. Canvas组件只有限支持文本绘制的镜像能力。
    
3. XComponent组件不支持组件镜像能力。
    

### 界面布局和边框设置

目前，以下三类通用属性需要使用新入参类型适配：

位置设置：[position](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-location#position)、[markAnchor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-location#markanchor)、[offset](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-location#offset)、[alignRules](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-location#alignrules12)

边框设置：[borderWidth](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-border#borderwidth)、[borderColor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-border#bordercolor)、[borderRadius](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-border#borderradius)

尺寸设置：[padding](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-size#padding)、[margin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-size#margin)

以position为例，需要把绝对方向x、y描述改为新入参类型start、end的描述，其他属性类似。

1. import { LengthMetrics } from '@kit.ArkUI';

2. @Entry
3. @Component
4. struct Index1 {
5.   build() {
6.     Stack({ alignContent: Alignment.TopStart }) {
7.       Stack({ alignContent: Alignment.TopStart }) {
8.         Column()
9.           .width(100)
10.           .height(100)
11.           .backgroundColor(Color.Red)
12.           .position({ start: LengthMetrics.px(200), top: LengthMetrics.px(200) })  //需要同时支持LTR和RTL时使用API12新增的LocalizedEdges入参类型,
13.                                                                                    //仅支持LTR时等同于.position({ x: '200px', y: '200px' })

14.       }.backgroundColor(Color.Blue)
15.     }.width("100%").height("100%").border({ color: '#880606' })
16.   }
17. }

### 自定义绘制Canvas组件

Canvas组件的绘制内容和坐标均不支持镜像能力。已绘制到Canvas组件上的内容并不会跟随系统语言的切换自动做镜像效果。

[CanvasRenderingContext2D](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-canvasrenderingcontext2d)的文本绘制支持镜像能力，在使用时需要与Canvas组件的通用属性direction（组件显示方向）和CanvasRenderingContext2D的属性direction（文本绘制方向）协同使用。具体规格如下：

1. 优先级：CanvasRenderingContext2D的direction属性 > Canvas组件通用属性direction > 系统语言决定的水平显示方向。
2. Canvas组件本身不会自动跟随系统语言切换镜像效果，需要应用监听到系统语言切换后自行重新绘制。
3. CanvasRenderingContext2D绘制文本时，只有符号等文本会对绘制方向生效，英文字母和数字不响应绘制方向的变化。

4. import { BusinessError, commonEventManager } from '@kit.BasicServicesKit';

5. @Entry
6. @Component
7. struct Index {
8.   @State message: string = 'Hello world';
9.   private settings: RenderingContextSettings = new RenderingContextSettings(true)
10.   private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)

11.   aboutToAppear(): void {
12.     // 监听系统语言切换
13.     let subscriber: commonEventManager.CommonEventSubscriber | null = null;
14.     let subscribeInfo2: commonEventManager.CommonEventSubscribeInfo = {
15.       events: ["usual.event.LOCALE_CHANGED"],
16.     }
17.     commonEventManager.createSubscriber(subscribeInfo2, (err: BusinessError, data: commonEventManager.CommonEventSubscriber) => {
18.       if (err) {
19.         console.error(`Failed to create subscriber. Code is ${err.code}, message is ${err.message}`);
20.         return;
21.       }

22.       subscriber = data;
23.       if (subscriber !== null) {
24.         commonEventManager.subscribe(subscriber, (err: BusinessError, data: commonEventManager.CommonEventData) => {
25.           if (err) {
26.             console.error(`订阅语言地区状态变化公共事件失败. Code is ${err.code}, message is ${err.message}`);
27.             return;
28.           }
29.           console.info('成功订阅语言地区状态变化公共事件: data: ' + JSON.stringify(data))
30.           // 监听到语言切换后，需要重新绘制Canvas内容
31.           this.drawText();
32.         })
33.       } else {
34.         console.error(`MayTest Need create subscriber`);
35.       }
36.     })
37.   }

38.   drawText(): void {
39.     console.error("MayTest drawText")
40.     this.context.reset()
41.     this.context.direction = "inherit"
42.     this.context.font = '30px sans-serif'
43.     this.context.fillText("ab%123&*@", 50, 50)
44.   }

45.   build() {
46.     Row() {
47.       Canvas(this.context)
48.         .direction(Direction.Auto)
49.         .width("100%")
50.         .height("100%")
51.         .onReady(() =>{
52.           this.drawText()
53.         })
54.         .backgroundColor(Color.Pink)
55.     }
56.     .height('100%')
57.   }

58. }

|镜像前|镜像后|
|:--|:--|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163855.97187894346782860413070045185900:50001231000000:2800:38B0782147A220E16A3881C5D06EDFD6F30BBAC604E4852F15982E1BD085E29F.jpg)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163855.82051447289845639648508258014582:50001231000000:2800:3794A6A5F1A7E2F85CB62C0F725BE5603931906D9A3C26EC86FA887154570823.jpg)|

### 镜像状态字符对齐

[Direction](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-appendix-enums#direction)是指文字的方向，即文本在屏幕上呈现时字符的顺序。在从左到右（LTR）文本中，显示顺序是从左向右；在从右到左（RTL）文本中，显示顺序是从右向左。

[TextAlign](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-appendix-enums#textalign)是将文本作为一个整体，在布局上的影响，具体位置会受Direction影响，以TextAlign为start为例，当Direction为LTR时，布局位置靠左；当Direction为RTL时，布局位置靠右。

在LTR与RTL文本混排时，如一个英文句子中包含阿拉伯语的单词或短语，显示顺序将变得复杂。下图为数字和维吾尔语混合时对应的字符逻辑顺序。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163855.34717957587343075279125249814916:50001231000000:2800:913695A30B0AB89ECC7D70EC0F48A9E47A1EB9E1A54C7FB3AE9FC89C96EA3820.png)

此时，文本渲染引擎会采用名为“双向算法”或“Unicode双向算法”（Unicode Bidirectional Algorithm）的方法来确定字符的显示顺序。下图展示了LTR与RTL文本混合时对应的字符显示顺序，确定字符方向的基本原则如下：

1. 强字符的方向性：强字符具有明确的方向性，例如，中文为LTR，阿拉伯语为RTL，这类字符的方向性会影响其周围的中性字符。
    
2. 弱字符的方向性：弱字符不具备明确的方向性，这些字符不会影响其周围中性字符的方向。
    
3. 中性字符的方向性：中性字符无固定方向性，它们会继承其最近的强字符的方向；若附近无强字符，则采用全局方向。
    

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163855.01845232581623425965771640965600:50001231000000:2800:5666B9E5C4800DD0FCB10F843EE123BFA9F65130B8CBD5130EB1EC7962831FBA.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-user-defined-extension-attributeupdater "属性更新器 (AttributeUpdater)")
# 支持无障碍

更新时间: 2025-12-16 16:39

## 概述

ArkUI提供了丰富的无障碍能力，使开发者能够创建可访问的应用界面，满足视觉、听觉、运动和认知障碍等用户的需求。

组件的[无障碍属性](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-accessibility)变化时，会触发辅助工具重新读取组件信息、无障碍服务重新扫描组件树、状态播报、虚拟节点动态更新等响应，这些机制确保辅助工具（如屏幕朗读）能及时感知并适配变化，为障碍用户提供连贯的体验。

## 设置无障碍分组

accessibilityGroup属性，用于设置是否启用无障碍分组。若启用，则该组件及其所有子组件将作为一个整体处理，无障碍服务不再单独处理各子组件。accessibilityGroup属性支持以下值：

- false（默认）：不启用无障碍分组。
    
- true：启用无障碍分组。
    

这里以Column组件为例，启用无障碍分组：

1. Column() {
2.   Text("HelloWorld").fontSize(50).fontWeight(FontWeight.Bold)
3. }
4. .accessibilityGroup(true)

## 设置无障碍重要性

accessibilityLevel属性表示组件的无障碍重要性，用于控制组件是否能被无障碍服务识别，支持以下值：

- "auto"（默认）：当前组件由无障碍分组服务和ArkUI进行综合判断组件是否可被无障碍辅助服务所识别。
    
- "yes"：当前组件可被无障碍辅助服务所识别。
    
- "no"：当前组件不可被无障碍辅助服务所识别。
    
- "no-hide-descendants"：当前组件及其所有子组件均不可被无障碍辅助服务所识别。
    

这里以Column组件为例，设置其无障碍重要性为可被无障碍辅助服务所识别：

1. Column() {
2.   Text("HelloWorld").fontSize(50).fontWeight(FontWeight.Bold)
3. }
4. .accessibilityGroup(true)
5. .accessibilityLevel("yes")

## 设置无障碍文本

accessibilityText属性用于为无文本内容的组件提供朗读文本。若组件已有文本，则优先播报无障碍文本。

支持字符串或资源引用。

这里以Column组件为例，设置其无障碍文本为“分组”：

1. Column() {
2.   Text("HelloWorld").fontSize(50).fontWeight(FontWeight.Bold)
3. }
4. .accessibilityGroup(true)
5. .accessibilityLevel("yes")
6. .accessibilityText("分组")

## 设置无障碍说明

accessibilityDescription属性用于提供更详细的组件说明，播报时紧随文本内容之后。

这里以Column组件为例，设置其无障碍说明为“分组”：

1. Column() {
2.   Text("HelloWorld")
3. }
4. .accessibilityGroup(true)
5. .accessibilityLevel("yes")
6. .accessibilityText("分组")
7. .accessibilityDescription("Column组件可以被选中，播报的内容是“分组”")

## 设置无障碍虚拟子节点

accessibilityVirtualNode属性，用于为自绘制组件添加虚拟无障碍节点，辅助工具会读取这些节点的信息而非实际显示内容。

1. @Entry
2. @Component
3. struct VirtualNodeExample {
4.   @Builder customAccessibilityNode() {
5.     Text("文本2")
6.       .fontSize(50)
7.       .fontWeight(FontWeight.Bold)
8.   }

9.   build() {
10.     Column() {
11.       Text("文本1")
12.         .fontSize(50)
13.         .fontWeight(FontWeight.Bold)
14.     }
15.     .accessibilityGroup(true)
16.     .accessibilityLevel("yes")
17.     .accessibilityVirtualNode(this.customAccessibilityNode)
18.   }
19. }

## 设置无障碍节点是否被选中

accessibilityChecked和accessibilitySelected是两个用于增强无障碍体验的属性，主要用于向屏幕朗读等辅助工具传达组件的选中状态。

### 在支持多选的情况下，设置无障碍节点是否被选中

accessibilityChecked属性，用于表示组件在支持多选的情况下是否被勾选（如复选框、开关按钮等二态或三态组件），适用于需要明确“选中/未选中”语义的场景，支持以下值：

- undefined（默认）：由系统自动判断（依赖组件自身的状态，如Toggle组件的isOn属性）。
    
- false：未选中。
    
- true：选中（如复选框打勾）。
    

这里以Column组件为例，设置其在支持多选的情况下被选中：

1. Column() {
2.   Text("HelloWorld").fontSize(50).fontWeight(FontWeight.Bold)
3. }
4. .accessibilityGroup(true)
5. .accessibilityLevel("yes")
6. .accessibilityText("分组")
7. .accessibilityDescription("Column组件可以被选中，播报的内容是“分组”")
8. .accessibilityChecked(true)

### 在支持单选的情况下，设置无障碍节点是否被选中

accessibilitySelected属性，用于表示组件在支持单选的情况下是否被选择（如单选列表项、标签页等），适用于需要区分“当前选中项”的场景（如单选组、导航菜单），支持以下值：

- undefined（默认）：由系统自动判断。
    
- false：未选中。
    
- true：当前选中。
    

这里以Column组件为例，设置在支持单选的情况下由系统自行确定其选中状态：

1. Column() {
2.   Text("HelloWorld").fontSize(50).fontWeight(FontWeight.Bold)
3. }
4. .accessibilityGroup(true)
5. .accessibilityLevel("yes")
6. .accessibilityText("分组")
7. .accessibilityDescription("Column组件可以被选中，播报的内容是“分组”")
8. .accessibilitySelected(undefined)

### accessibilityChecked属性与accessibilitySelected属性的关键区别

在ArkUI无障碍属性中，accessibilityChecked和accessibilitySelected均用于表示组件的状态，但二者应用场景与语义含义存在本质差异。以下是二者的对比：

|属性|accessibilityChecked|accessibilitySelected|
|:--|:--|:--|
|常见场景|复选框、开关等二态/三态组件。|单选列表、标签页等互斥选择场景。|
|语义目标|控件物理状态（如开关是否打开）。|导航焦点项（如列表当前选中项）。|
|状态持久性|通常需显式保存（如表单提交）。|临时性（随焦点移动变化）。|
|典型组件|Checkbox，Toggle。|List，Tabs。|

## 使用建议

- 优先级控制
    
    通过accessibilityLevel确保关键操作可被识别。
    
- 语义化描述
    
    为图标、图片等非文本元素添加accessibilityText和accessibilityDescription。
    
- 分组优化
    
    对复杂布局使用accessibilityGroup减少冗余播报。
    

## 场景示例

该示例主要演示accessibilityText无障碍文本和accessibilityDescription无障碍说明的播报内容。

其中，对于该组件的无障碍文本的内容，在既拥有文本属性又拥有无障碍文本属性的情况下，当组件被选中时，仅播报无障碍文本内容。

1. @Entry
2. @Component
3. struct Index {

4.   @Builder customAccessibilityNode() {
5.     Column() {
6.       Text(`virtual node`)
7.     }
8.     .width(10)
9.     .height(10)
10.   }

11.   build() {
12.     Row() {
13.       Column() {
14.         Text("文本1")
15.           .fontSize(50)
16.           .fontWeight(FontWeight.Bold)
17.         Text("文本2")
18.           .fontSize(50)
19.           .fontWeight(FontWeight.Bold)
20.       }
21.       .width('100%')
22.       .accessibilityGroup(true)
23.       .accessibilityLevel("yes")
24.       .accessibilityText("分组")
25.       .accessibilityDescription("Column组件可以被选中，播报的内容是“分组”")
26.       .accessibilityVirtualNode(this.customAccessibilityNode)
27.       .accessibilityChecked(true)
28.       .accessibilitySelected(undefined)
29.     }
30.     .height('100%')
31.   }
32. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163900.86195489852322311378724683175703:50001231000000:2800:D032E9AC3C0D4C2B266459FBC80120C50F32E874BF48210651959612C737A6D8.jpg)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-support-accessibility-friendliness "无障碍与适老化")
# 支持适老化

更新时间: 2025-12-16 16:39

系统字体被放大后，应用应确保整体布局不出现错乱，组件不出现重叠。可以根据业务需要限制跟随的字体最大档位、改变布局来更好的适配更大字体等。本文旨在指导应用如何跟随系统字体大小和跟随到的最大倍数。

## 应用适配规则

- 在系统使用1.75倍及以上的大字体时，页面布局不得错乱，组件不得叠加，文字不得截断。
    
- 图标及图片不会随着字体的变大而变化。
    
- 页面中不重要的内容字体，可采用不跟随系统字体变化或限制字体最大尺寸的方法进行布局。
    
- 若应用跟随系统字体增大后导致页面内容位置挤压或截断等问题，可采取将X轴扩展至Y轴的措施，例如将左右布局调整为上下布局。
    
- [系统组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkui-support-for-aging-adaptation#%E9%80%82%E9%85%8D%E9%80%82%E8%80%81%E5%8C%96%E7%9A%84%E7%B3%BB%E7%BB%9F%E7%BB%84%E4%BB%B6%E5%8F%8A%E8%A7%A6%E5%8F%91%E6%96%B9%E5%BC%8F)已针对适老化大字体进行了单独适配，尽可能在开发过程中使用系统组件。
    

## 应用适配适老化大字体

1. 开启路径
    
    在“设置-辅助功能-关怀模式-放大显示”中开启。
    
    各档位对应参数：
    
    |档位|字体大小|字体粗细|
    |:--|:--|:--|
    |标准|1倍|1倍|
    |大1档|1.15倍|1倍|
    |大2档|1.3倍|1.1倍|
    |大3档|1.45倍|1.1倍|
    |大4档|1.75倍|1.25倍|
    |大5档|2.0倍|1.25倍|
    |大6档|3.2倍|1.25倍|
    
2. 适配方法
    
    当前默认应用不跟随系统字体的变化。如需跟随系统字体变化，并设置最大跟随变化的倍数，请按以下步骤操作：
    
    - [app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)适配。
        
        通过配置"configuration": "$profile:configuration"，指向base/profile/configuration.json文件；
        
        1. {
        2.   "app": {
        3.     "bundleName": "com.example.myapplication",
        4.     "vendor": "example",
        5.     "versionCode": 1000000,
        6.     "versionName": "1.0.0",
        7.     "icon": "$media:app_icon",
        8.     "label": "$string:app_name",
        9.     "configuration": "$profile:configuration"
        10.   }
        11. }
        
    - 在base文件目录下新增profile文件夹，并在此目录下新增 configuration.json 文件。
        
        配置"fontSizeScale": "followSystem"表示该应用的字体大小将根据系统设置进行缩放，"fontSizeMaxScale": "1.3"表示应用字体大小随系统变化的最大缩放比例为1.3倍。
        
        1. {
        2.   "configuration": {
        3.     "fontSizeScale": "followSystem",
        4.     "fontSizeMaxScale": "1.3"
        5.   }
        6. }
        
    - 若应用需适应系统字体大小的变化，最大应调整至1.75倍，但部分组件可调整至2倍。
        
        首先需要按照上述步骤配置"fontSizeMaxScale"为1.75。
        
        1. {
        2.   "configuration": {
        3.     "fontSizeScale": "followSystem",
        4.     "fontSizeMaxScale": "1.75"
        5.   }
        6. }
        
        然后，为Text添加maxFontScale属性，传递参数为2，表示该Text组件跟随系统字体大小变化的最大倍数为2倍。
        
        1. Text('hello world!')
        2.   .fontSize($r('sys.float.Body_M'))
        3.   .maxFontScale(2)
        4.   .fontColor($r('sys.color.font_secondary'))
        
        当Text组件配置了maxFontScale属性时，将采用组件设置的最大放大倍数，而非系统默认的最大放大倍数。
        
    - 若应用不需要跟随系统字体大小变化，无需配置。
        
3. 获取字体大小和粗细。
    
    - 生命周期回调方法[onConfigurationUpdated](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-environmentcallback#onconfigurationupdated)的config参数可接收字体大小（[fontSizeScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-configuration#configuration)）与字体粗细（[fontWeightScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-configuration#configuration)）。
        
        注册系统环境变化的监听后，在系统环境变化时可触发回调。
        
    - 应用冷启动查询系统字体大小档位。
        
        1. let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
        2. let fontSizeScale: number = context.config?.fontSizeScale ?? 1;
        

## 适配适老化的系统组件及触发方式

适老化提供了一种通过鼠标或手指长按的方法来放大所选区域或组件，即如果系统字体大小大于1倍，当用户使用鼠标或手指长按装配了适老化方法的组件，需要从所选区域的组件中提取数据，并放入另一个弹窗组件中展示。该方法的目的在于使组件和组件内部数据（子组件）放大，同时将整体组件在屏幕中央显示，让用户能够更好的观察该组件。

- 适老化规则
    
    由于在系统字体大于1倍时，组件并没有默认放大，需要通过配置[configuration标签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file#configuration%E6%A0%87%E7%AD%BE)，实现组件放大的适老化功能。
    
- 如何开启适老化
    
    进入手机设置，点击辅助功能，开启关怀模式。
    
- 适老化操作
    
    在已经支持适老化能力的组件上长按组件，能够触发弹窗，当用户释放时，适老化操作结束。当设置系统字体大于1倍时，组件自动放大，当系统字体恢复至1倍时组件恢复正常状态。
    
- 适老化对象
    
    触发适老化操作并提供数据的组件。
    
- 适老化弹窗目标
    
    可接收并处理适老化数据的组件。
    
- 弹窗限制
    
    当用户将系统字体设置为2倍以上时，弹窗内容包括icon和文字的放大倍数固定为2倍。
    
- 联合其他能力
    
    适老化能力可以适配其他能力（如：滑动拖拽）。底部页签（tabBar）组件在触发适老化时，如果用户滑动手指或鼠标可以触发底部页签其他子组件的适老化功能。
    

|触发方式|组件名称|
|:--|:--|
|长按系统组件触发|[SideBarContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-sidebarcontainer)， [底部页签（tabBar）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabcontent#tabbar9)，[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)，[NavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation#navdestination10)， [Tabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabs)|
|设置系统字体默认放大|[PickerDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-methods-calendarpicker-dialog)， [Button](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-button)， [Menu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-menu)， [Stepper](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-stepper)， [BindSheet](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-sheet-transition#bindsheet)，[TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput)，[TextArea](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textarea)，[Search](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-search)，[SelectionMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-selectionmenu)，[Chip](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-chip)，[Dialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ohos-arkui-advanced-dialog)，[Slider](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-slider)， [Progress](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-progress)， [Badge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-badge)|

SideBarContainer组件通过长按控制按钮触发适老化弹窗。在系统字体为1倍的情况下，长按控制按钮不能弹窗。在系统字体大于1倍的情况下，长按控制按钮可以弹窗。

1. @Entry
2. @Component
3. struct SideBarContainerExample {
4.   @State currentFontSizeScale: number = 1
5.   normalIcon: Resource = $r("app.media.icon")
6.   selectedIcon: Resource = $r("app.media.icon")
7.   @State arr: number[] = [1, 2, 3]
8.   @State current: number = 1
9.   @State title: string = 'Index01';

10.   build() {
11.     SideBarContainer(SideBarContainerType.Embed) {
12.       Column() {
13.         ForEach(this.arr, (item: number) => {
14.           Column({ space: 5 }) {
15.             Image(this.current === item ? this.selectedIcon : this.normalIcon).width(64).height(64)
16.             Text("0" + item)
17.               .fontSize(25)
18.               .fontColor(this.current === item ? '#0A59F7' : '#999')
19.               .fontFamily('source-sans-pro,cursive,sans-serif')
20.           }
21.           .onClick(() => {
22.             this.current = item;
23.             this.title = "Index0" + item;
24.           })
25.         }, (item: string) => item)
26.       }.width('100%')
27.       .justifyContent(FlexAlign.SpaceEvenly)
28.       .backgroundColor($r('sys.color.mask_fifth'))
29.     }
30.     .controlButton({
31.       icons: {
32.         hidden: $r('sys.media.ohos_ic_public_drawer_open_filled'),
33.         shown: $r('sys.media.ohos_ic_public_drawer_close')
34.       }
35.     })
36.     .sideBarWidth(150)
37.     .minSideBarWidth(50)
38.     .maxSideBarWidth(300)
39.     .minContentWidth(0)
40.     .onChange((value: boolean) => {
41.       console.info('status:' + value)
42.     })
43.     .divider({ strokeWidth: '1vp', color: Color.Gray, startMargin: '4vp', endMargin: '4vp' })
44.   }
45. }

切换系统字体前后长按已经支持适老化能力的组件，有如下效果：

|系统字体为一倍（适老化能力开启前）|系统字体为1.75倍（适老化能力开启后）|
|:--|:--|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163923.86712360537302917589317246679864:50001231000000:2800:6FB54AE1AD7B97D5C367C388C7C5518A792031CA3F04E8EFD62E3AA22A13D6B0.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163923.20515375300425839694870559379957:50001231000000:2800:0139D704105ECABB6763C345A5EEB3556169886063B17BA9A059D51B54856BD8.png)|

[TextPickerDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-methods-textpicker-dialog)组件通过设置系统字体大小触发适老化弹窗。在系统字体为1倍的情况下，适老化不触发；在系统字体大于1倍的情况下，适老化触发。

1. @Entry
2. @Component
3. struct TextPickerExample {
4.   private select: number | number[] = 0;
5.   private cascade: TextCascadePickerRangeContent[] = [
6.     {
7.       text: '辽宁省',
8.       children: [{ text: '沈阳市', children: [{ text: '沈河区' }, { text: '和平区' }, { text: '浑南区' }] },
9.         { text: '大连市', children: [{ text: '中山区' }, { text: '金州区' }, { text: '长海县' }] }]
10.     },
11.     {
12.       text: '吉林省',
13.       children: [{ text: '长春市', children: [{ text: '南关区' }, { text: '宽城区' }, { text: '朝阳区' }] },
14.         { text: '四平市', children: [{ text: '铁西区' }, { text: '铁东区' }, { text: '梨树县' }] }]
15.     },
16.     {
17.       text: '黑龙江省',
18.       children: [{ text: '哈尔滨市', children: [{ text: '道里区' }, { text: '道外区' }, { text: '南岗区' }] },
19.         { text: '牡丹江市', children: [{ text: '东安区' }, { text: '西安区' }, { text: '爱民区' }] }]
20.     }
21.   ]
22.   @State v: string = '';
23.   @State showTriggered: string = '';
24.   private triggered: string = '';
25.   private maxLines: number = 3;

26.   linesNum(max: number): void {
27.     let items: string[] = this.triggered.split('').filter(item => item != '');
28.     if (items.length > max) {
29.       this.showTriggered = items.slice(-this.maxLines).join('');
30.     } else {
31.       this.showTriggered = this.triggered;
32.     }
33.   }

34.   build() {
35.     Column() {
36.       Button("TextPickerDialog.show:" + this.v)
37.         .onClick(() => {
38.           TextPickerDialog.show({
39.             range: this.cascade,
40.             selected: this.select,
41.             onAccept: (value: TextPickerResult) => {
42.               this.select = value.index
43.               console.log(this.select + '')
44.               this.v = value.value as string
45.               console.info("TextPickerDialog:onAccept()" + JSON.stringify(value))
46.               if (this.triggered != '') {
47.                 this.triggered += `onAccept(${JSON.stringify(value)})`;
48.               } else {
49.                 this.triggered = `onAccept(${JSON.stringify(value)})`;
50.               }
51.               this.linesNum(this.maxLines);
52.             },
53.             onCancel: () => {
54.               console.info("TextPickerDialog:onCancel()")
55.               if (this.triggered != '') {
56.                 this.triggered += `onCancel()`;
57.               } else {
58.                 this.triggered = `onCancel()`;
59.               }
60.               this.linesNum(this.maxLines);
61.             },
62.             onChange: (value: TextPickerResult) => {
63.               console.info("TextPickerDialog:onChange()" + JSON.stringify(value))
64.               if (this.triggered != '') {
65.                 this.triggered += `onChange(${JSON.stringify(value)})`;
66.               } else {
67.                 this.triggered = `onChange(${JSON.stringify(value)})`;
68.               }
69.               this.linesNum(this.maxLines);
70.             },
71.           })
72.         })
73.         .margin({ top: 60 })
74.     }
75.   }
76. }

|系统字体为一倍（适老化能力开启前）|系统字体为1.75倍（适老化能力开启后）|
|:--|:--|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163923.03177954377401691604463283717287:50001231000000:2800:9F1E00DA0A89646B4395DDCA60FE6F5318A18995682B5CDE169150C4AD647932.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163923.30844582682613954572146897870173:50001231000000:2800:2C1DA7803F89A42ED0BCA54102DE462ACFFCD2CAC3ED16F94F574E2A3C31F7B2.png)|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-universal-attributes-accessibility "支持无障碍")
# 应用深浅色适配

更新时间: 2025-12-16 16:39

## 概述

当前系统存在深浅色两种显示模式，为了给用户更好的使用体验，应用应适配深浅色模式。从应用与系统配置关联的角度来看，适配深浅色模式可以分为下面两种情况：

[应用跟随系统的深浅色模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-dark-light-color-adaptation#%E5%BA%94%E7%94%A8%E8%B7%9F%E9%9A%8F%E7%B3%BB%E7%BB%9F%E7%9A%84%E6%B7%B1%E6%B5%85%E8%89%B2%E6%A8%A1%E5%BC%8F)

[应用主动设置深浅色模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-dark-light-color-adaptation#%E5%BA%94%E7%94%A8%E4%B8%BB%E5%8A%A8%E8%AE%BE%E7%BD%AE%E6%B7%B1%E6%B5%85%E8%89%B2%E6%A8%A1%E5%BC%8F)

## 应用跟随系统的深浅色模式

1. 颜色适配
    
    - 自定义资源实现
        
        resources目录下增加深色模式限定词目录（命名为dark）并新建color.json文件，可显示深色模式颜色资源的配置。详细请参考[资源分类与访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access)。
        
        图1 resources目录结构示意
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163900.27826512888013815143979434576814:50001231000000:2800:B75A85162A17A27FD075207B5F5D65DC35AE355F603F25CEC4167539AE56BF67.png)
        
        例如，开发者可在这两个color.json中定义同名配色定义并赋予不同的色值。
        
        base/element/color.json文件：
        
        1. {
        2.   "color": [
        3.     {
        4.       "name": "app_title_color",
        5.       "value": "#000000"
        6.     }
        7.   ]
        8. }
        
        dark/element/color.json文件：
        
        1. {
        2.   "color": [
        3.     {
        4.       "name": "app_title_color",
        5.       "value": "#FFFFFF"
        6.     }
        7.   ]
        8. }
        
    - 通过系统资源实现
        
        开发者可直接使用的[系统预置资源](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access#%E7%B3%BB%E7%BB%9F%E8%B5%84%E6%BA%90)，即分层参数，同一资源ID在设备类型、深浅色等不同配置下有不同的取值。通过使用系统资源，不同的开发者可以开发出具有相同视觉风格的应用，不需要自定义两份颜色资源，在深浅色模式下也会自动切换成不同的颜色值。例如，开发者可调用系统资源中的文本主要配色来定义应用内文本颜色。
        
        1. Text('使用系统定义配色')
        2.   .fontColor($r('sys.color.ohos_id_color_text_primary'))
        
2. 图片资源适配
    
    采用资源限定词目录的方式。参照颜色适配的方法，需要将深色模式下对应的同名图片放到 dark/media 目录下，再通过$r的方式加载图片资源的key值，系统做深浅色模式切换时，会自动加载对应资源文件中的value值。
    
    对于 SVG 格式的一些简单图标，可以使用[fillColor](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-graphics-display#%E6%98%BE%E7%A4%BA%E7%9F%A2%E9%87%8F%E5%9B%BE)属性配合系统资源改变图片的绘制颜色。不通过两套图片资源的方式，也可以实现深浅色模式适配。
    
    1. Image($r('app.media.pic_svg'))
    2.   .width(50)
    3.   .fillColor($r('sys.color.ohos_id_color_text_primary'))
    
3. Web组件适配
    
    Web组件支持对前端页面进行深色模式配置，可参考[Web组件深色模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-set-dark-mode)进行相关配置。
    
4. "自定义节点"适配
    
    自定义节点BuilderNode和ComponentContent需手动传递系统环境变化事件，触发节点的全量更新，详细请参考[BuilderNode系统环境变化更新](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-buildernode#updateconfiguration12)。
    
    1. // 记录创建的自定义节点对象
    2. const builderNodeMap: Array<BuilderNode<[Params]>> = new Array();
    
    3. class MyFrameCallback extends FrameCallback {
    4.   onFrame() {
    5.     updateColorMode();
    6.   }
    7. }
    
    8. function updateColorMode() {
    9.   builderNodeMap.forEach((value, index) => {
    10.     // 通知BuilderNode环境变量改变，触发深浅色切换
    11.     value.updateConfiguration();
    12.   })
    13. }
    14. // ... other code ...
    15. aboutToAppear() {
    16. // ... other code ...
    17.   this.getUIContext()?.postFrameCallback(new MyFrameCallback());
    18. // ... other code ...
    19. }
    
5. 应用监听深浅色模式切换事件
    
    应用可以主动监听系统深浅色模式变化，进行其他类型的资源初始化等自定义逻辑。应用使用[setColorMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-uiabilitycontext#setcolormode18)手动设置深浅色的情况下，将不会收到onConfigurationUpdate回调。除此之外，无论应用是否跟随系统深浅色模式变化，该监听方式均可生效。
    
    a. 在 AbilityStage 的 onCreate() 生命周期中获取APP当前的颜色模式并保存到 AppStorage。
    
    1. onCreate(): void {
    2.   hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
    3.   AppStorage.setOrCreate('currentColorMode', this.context.config.colorMode);
    4. }
    
    b. 在AbilityStage的onConfigurationUpdate()生命周期中获取最新更新的颜色模式并刷新到AppStorage。
    
    1. onConfigurationUpdate(newConfig: Configuration): void {
    2.   AppStorage.setOrCreate('currentColorMode', newConfig.colorMode);
    3.   hilog.info(0x0000, 'testTag', 'the newConfig.colorMode is %{public}s', JSON.stringify(AppStorage.get('currentColorMode')) ?? '');
    4. }
    
    c. 在Page中通过 @StorageProp + @Watch 方式获取当前最新颜色并监听设备深色模式变化。
    
    1. @StorageProp('currentColorMode') @Watch('onColorModeChange') currentMode: number = ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT;
    
    d. 在 aboutToAppear 初始化函数中根据当前最新颜色模式刷新状态变量。
    
    2. aboutToAppear(): void {
    3.   if (this.currentMode == ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT) {
    4.     //当前为浅色模式，资源初始化逻辑
    5.   }else {
    6.     //当前为深色模式，资源初始化逻辑
    7.   }
    8. }
    
    e. 在 @Watch 回调函数中执行同样的适配逻辑。
    
    9. onColorModeChange(): void {
    10.   if (this.currentMode == ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT) {
    11.     //当前为浅色模式，资源初始化逻辑
    12.   } else {
    13.     //当前为深色模式，资源初始化逻辑
    14.   }
    15. }
    
6. 局部深浅色适配
    
    通过[WithTheme](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-with-theme)可以设置三种[颜色模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-foreground-blur-style#themecolormode%E6%9E%9A%E4%B8%BE%E8%AF%B4%E6%98%8E)，分别为：跟随系统深浅色模式、固定使用浅色模式和固定使用深色模式。
    
    在WithTheme作用范围内，组件的样式资源值将依据指定模式，读取对应的深浅色模式系统和应用资源值。这表明，在WithTheme作用范围内，组件的配色将根据指定的深浅模式进行调整。详情请参阅[设置应用页面局部深浅色](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/theme_skinning#%E8%AE%BE%E7%BD%AE%E5%BA%94%E7%94%A8%E9%A1%B5%E9%9D%A2%E5%B1%80%E9%83%A8%E6%B7%B1%E6%B5%85%E8%89%B2)。
    

## 应用主动设置深浅色模式

应用默认配置为跟随系统切换深浅色模式，如不希望应用跟随系统深浅色模式变化，可主动设置应用的深浅色风格。设置后，应用的深浅色模式固定，不会随系统改变。

说明

应用未专门适配深色模式，直接跟随系统切换可能遇到深色模式下的显示异常，也可考虑使用该方法将本应用固定为浅色模式。

1. onCreate(): void {
2.   hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
3.   this.context.getApplicationContext().setColorMode(ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT);
4. }

## 系统判定应用深浅色模式的规则

1. 如果应用调用上述setColorMode接口主动设置了深浅色，则以接口效果优先。
    
2. 应用没有调用setColorMode接口时：
    
    - 如果应用工程dark目录下有深色资源，则系统组件在深色模式下会自动切换成为深色。
        
    - 如果应用工程dark目录下没有任何深色资源，则系统组件在深色模式下仍会保持浅色体验。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163900.52800042319637217304208500903577:50001231000000:2800:A9256E79D1C211E8EFCCA3180F50623C161A0DD16CDDB6E57B1049038E451F5D.png)
        

如果应用全部都是由系统组件/系统颜色开发，且想要跟随系统切换深浅色模式时，请参考以下示例修改代码来保证应用体验。

1. onCreate(): void {
2.   this.context.getApplicationContext().setColorMode(ConfigurationConstant.ColorMode.COLOR_MODE_NOT_SET);
3. }

## 深浅色模式的使用建议与注意事项

- 建议方法
    
    当应用跟随系统深色或浅色模式时，建议采用[AbilityStage的监听回调](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-abilitystage#onconfigurationupdate)或[Ability的监听回调](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-ability#abilityonconfigurationupdate)方式，主动监听系统深浅色模式变化。一旦颜色模式发生变化，应通过绑定状态变量等方法，执行特定的业务逻辑。
    
- 不推荐方法
    
    开发者在使用资源时，未采用监听系统深浅色模式变化的方式，而是在属性设置中，通过函数返回值实现深浅色切换。例如以下写法：
    
    1. getResource() : string {
    2.   // 获取系统颜色模式
    3.   if (colorMode == "dark") {
    4.     return "#FF000000"
    5.   } else {
    6.     return "#FFFFFFFF"
    7.   }
    8. }
    9. // ... other code ...
    10. build() {
    11.   // ... other code ...
    12.   Button.backgroundColor(this.getResource())
    13.   // ... other code ...
    14. }
    
    这种方式依赖于切换流程中重新执行属性设置代码，随着系统的发展和性能优化，并不能确保所有属性代码均被重新执行。因为在大部分热更新场景中，重新执行全部页面构建和属性设置代码显然是冗余的。
    

## 优化深浅色模式切换开销

默认情况下，深浅色模式的切换需要执行全量重绘，包括重新设置所有组件的属性，性能开销会随着应用UI的复杂度线性增加。

从API version 20开始，系统提供了一种高性能的深浅色切换流程，开发者可通过新增[metadata](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#metadata%E6%A0%87%E7%AD%BE)配置项开启该能力，从而实现深浅色切换时的开销更小。

说明

配置此metadata时，必须确保在属性设置中，没有通过函数返回值实现深浅色切换。

[HdsNavigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavigation)、[HdsNavDestination](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdsnavdestination)、[HdsTabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdstabs)、[HdsListItemCard](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ui-design-hdslistitemcard)四个高级组件暂未适配，这些高级组件的颜色相关属性均需使用[AbilityStage的监听回调](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-abilitystage#onconfigurationupdate)或[Ability的监听回调](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-ability#abilityonconfigurationupdate)方式来处理。

1. 通过metadata开启深浅色切换优化选项。
    
    优化深浅色模式切换开销，需在module.json5文件中新增metadata字段，同时需对部分组件的属性进行适配。
    
    1. "metadata": [
    2.   {
    3.     "name": "configColorModeChangePerformanceInArkUI",
    4.     "value": "true"
    5.   }
    6. ]
    
2. 应用的自定义行为需要正确适配。
    
    开启深浅色切换优化选项后，深浅色切换不会全量重新执行前端代码和属性设置，仅会更新、重绘必要的属性，如果开发者之前在属性设置中通过函数适配深浅色更新将不会生效，这种情况需要开启优化流程前进行正确适配，可参考[深浅色模式的使用建议与注意事项](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-dark-light-color-adaptation#%E6%B7%B1%E6%B5%85%E8%89%B2%E6%A8%A1%E5%BC%8F%E7%9A%84%E4%BD%BF%E7%94%A8%E5%BB%BA%E8%AE%AE%E4%B8%8E%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)进行适配。以下是三个典型的适配场景：
    

- 根据实时读取的深浅色模式返回不同资源值。
    
    开启深浅色切换优化选项后，可以采用[AbilityStage的监听回调](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-abilitystage#onconfigurationupdate)或[Ability的监听回调](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-ability#abilityonconfigurationupdate)方式，主动监听系统深浅色模式变化，更新对应文本的文字颜色，示例代码如下：
    
    1. // EntryAbility.ets
    2. import { Configuration, UIAbility } from '@kit.AbilityKit';
    
    3. export default class EntryAbility extends UIAbility {
    
    4.   onConfigurationUpdate(newConfig: Configuration): void {
    5.     AppStorage.setOrCreate('colorMode', newConfig.colorMode);
    6.   }
    7. }
    
    8. // Index.ets
    9. import { ConfigurationConstant } from '@kit.AbilityKit';
    
    10. @Entry
    11. @Component
    12. struct MainPage {
    13.   @StorageLink('colorMode') @Watch('colorModeChange') colorMode: ConfigurationConstant.ColorMode = ConfigurationConstant.ColorMode.COLOR_MODE_NOT_SET;
    14.   @State textColor: Resource = $r("app.color.color_light");
    
    15.   colorModeChange() {
    16.     if (this.colorMode === ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT) {
    17.       this.textColor = $r("app.color.color_light")
    18.     } else {
    19.       this.textColor = $r("app.color.color_night")
    20.     }
    21.   }
    
    22.   build() {
    23.     Column() {
    24.       Text('fontColor')
    25.         .fontColor(this.textColor)
    26.     }
    27.   }
    28. }
    
- 根据判断自定义主题模式返回不同资源值。
    
    开启深浅色切换优化选项后，需要将Text中文本内容和文本颜色与状态变量进行绑定，在接收到深浅色切换事件后通过状态变量更新实现组件属性的更新，示例代码如下：
    
    1. // ResourceTheme.ets
    2. export enum ThemeMode {
    3.   mode1 = 0,
    4.   mode2
    5. }
    
    6. export class ResourceTheme {
    7.   fontColor: ResourceColor = this.getColor();
    8.   themeMode: ThemeMode = ThemeMode.mode1;
    
    9.   setThemeMode(mode: ThemeMode) {
    10.     this.themeMode = mode
    11.   }
    12.   getThemeMode(): ThemeMode {
    13.     return this.themeMode
    14.   }
    15.   getColor(): ResourceColor {
    16.     if (this.themeMode === ThemeMode.mode1) {
    17.       return $r("app.color.color_light")
    18.     } else {
    19.       return $r("app.color.color_night")
    20.     }
    21.   }
    22. }
    
    23. // Index.ets
    24. import { ConfigurationConstant } from '@kit.AbilityKit';
    25. import { ResourceTheme, ThemeMode } from './ResourceTheme';
    
    26. @Entry
    27. @Component
    28. struct MainPage {
    29.   @StorageLink('colorMode') @Watch('colorModeChange') colorMode: ConfigurationConstant.ColorMode = ConfigurationConstant.ColorMode.COLOR_MODE_NOT_SET;
    30.   resourceTheme = new ResourceTheme();
    31.   @State textColor: ResourceColor = this.resourceTheme.getColor();
    32.   @State textContent: string = this.resourceTheme.getThemeMode().toString();
    
    33.   colorModeChange() {
    34.     if (this.colorMode === ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT) {
    35.       this.resourceTheme.setThemeMode(ThemeMode.mode1)
    36.     } else {
    37.       this.resourceTheme.setThemeMode(ThemeMode.mode2)
    38.     }
    39.     this.textContent = this.resourceTheme.getThemeMode().toString()
    40.     this.textColor = this.resourceTheme.getColor()
    41.   }
    
    42.   build() {
    43.     Column() {
    44.       Text('ThemeMode is ' + this.textContent)
    45.         .fontColor(this.textColor)
    46.     }
    47.   }
    48. }
    
- 根据读取的成员变量值返回不同资源值。
    
    开启深浅色切换优化选项后，需要将文本文字颜色属性与状态变量绑定。在深浅色切换时通过回调函数更新状态变量，从而实现仅在下一次深浅色切换时发生属性更新的效果，示例代码如下：
    
    1. // Index.ets
    2. import { ConfigurationConstant } from '@kit.AbilityKit';
    
    3. @Entry
    4. @Component
    5. struct MainPage {
    6.   mode: number = 0;
    7.   @StorageLink('colorMode') @Watch('colorModeChange') colorMode: ConfigurationConstant.ColorMode = ConfigurationConstant.ColorMode.COLOR_MODE_NOT_SET;
    8.   @State textColor: Resource = $r("app.color.color_light");
    
    9.   colorModeChange() {
    10.     if (this.mode % 2 === 0) {
    11.       return $r("app.color.color_light")
    12.     } else {
    13.       return $r("app.color.color_night")
    14.     }
    15.   }
    
    16.   build() {
    17.     Column() {
    18.       Button('change mode')
    19.         .onClick((event: ClickEvent) => {
    20.           this.mode++
    21.         })
    22.       Text('fontColor')
    23.         .fontColor(this.textColor)
    24.     }
    25.   }
    26. }
    

## 利用反色能力快速适配深色模式

从API version 20开始，对于有大量存量代码，之前已经通过[资源配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-dark-light-color-adaptation#%E5%BA%94%E7%94%A8%E8%B7%9F%E9%9A%8F%E7%B3%BB%E7%BB%9F%E7%9A%84%E6%B7%B1%E6%B5%85%E8%89%B2%E6%A8%A1%E5%BC%8F)模式或[主题](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-with-theme)方式，实现部分深色模式适配。可使用系统提供的反色能力，快速实现全量深色模式适配。

这种方式虽然管理上不如资源配置和主题方式精细可控，但适配工作量更低，应用包也不会因为大量的资源配置而膨胀，同时也能够带来一定程度上可以接受的视觉效果。

说明

反色能力需在[优化深浅色模式切换开销](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-dark-light-color-adaptation#%E4%BC%98%E5%8C%96%E6%B7%B1%E6%B5%85%E8%89%B2%E6%A8%A1%E5%BC%8F%E5%88%87%E6%8D%A2%E5%BC%80%E9%94%80)使用的前提下使用。

1. 使用反色能力。
    
    从API version 20开始，ArkUI开发框架新增了[OH_ArkUI_SetForceDarkConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-node-h#oh_arkui_setforcedarkconfig)接口，提供反色能力。该功能可根据开发者自定义的反色算法，在深浅色切换时自动对颜色属性进行反色。反色能力只有在颜色属性设置为非资源值时生效，若通过$r设置颜色属性，则优先生效资源文件中配置的颜色值。
    
    在应用开发时，可能会涉及到多个颜色属性的设置，当该属性不存在深色模式颜色资源的配置时，使用该能力可以快速实现深色模式的适配。
    
    说明
    
    - 调用OH_ArkUI_SetForceDarkConfig前，需确保已加载过[OH_ArkUI_QueryModuleInterfaceByName(ARKUI_NATIVE_NODE, "ArkUI_NativeNodeAPI_1")](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-interface-h#oh_arkui_querymoduleinterfacebyname)。
        
    - OH_ArkUI_SetForceDarkConfig接口一定要在节点创建前的UI线程中调用。**页面创建完成后，不支持通过该接口动态修改应用的反色能力生效状态。**
        
    - OH_ArkUI_SetForceDarkConfig接口仅支持进程级生效，暂不支持不同实例使用不同的反色算法。
        
    - OH_ArkUI_SetForceDarkConfig接口仅支持CAPI接口，考虑到反色算法在深浅色切换时会被频繁调用，采用C-API接口可以避免存在大量的跨语言调用开销。
        
    - [DatePickerDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-methods-datepicker-dialog)、[TimePickerDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-methods-timepicker-dialog)、[CalendarPickerDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-methods-calendarpicker-dialog)、[TextPickerDialog](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-methods-textpicker-dialog)由于不存在实体节点，无法使能反色算法。
        
    - TextArea中NODE_BORDER_COLOR、NODE_TEXT_RADIAL_GRADIENT及NODE_TEXT_LINEAR_GRADIENT等属性无法使能反色算法。
        
    - 如果组件设置了异常值颜色或者undefined，反色能力不生效。
        
    
    本示例展示OH_ArkUI_SetForceDarkConfig接口的基础使用方式，自定义反色算法根据开发者实际场景进行设置，便于深浅色切换时展示不同的颜色值。
    
    1. OH_ArkUI_SetForceDarkConfig(nullptr, true, ArkUI_NodeType::ARKUI_NODE_UNDEFINED, nullptr); // 对所有组件使用x系统默认反色算法，即三原色取反。
    
    2. // page1 ArkTs侧创建组件使用反色能力。
    3. // 前置已默认对所有组件使用默认反色算法，深浅色切换时会对文本的文字颜色进行反色，浅色模式下展示为黑色字体，深色模式下展示为白色字体。
    4. build() {
    5.   // ... other code ...
    6.   Text("测试反色算法")
    7.     .fontColor(Color.Black)
    8.   // ... other code ...
    9. }
    
    OH_ArkUI_SetForceDarkConfig接口不同入参效果如下：
    
    10. // 开发者自定义的反色算法函数。
    11. uint32_t colorInvertFunc(uint32_t color) {
    12.   return ~color;
    13. }
    14. OH_ArkUI_SetForceDarkConfig(nullptr, true, ArkUI_NodeType::ARKUI_NODE_UNDEFINED, colorInvertFunc); // 对所有组件使用自定义反色算法。
    
    15. OH_ArkUI_SetForceDarkConfig(nullptr, false, ArkUI_NodeType::ARKUI_NODE_UNDEFINED, nullptr); // 对所有组件停用反色能力，深浅色切换使用系统原始逻辑。
    
    16. OH_ArkUI_SetForceDarkConfig(nullptr, true, ArkUI_NodeType::ARKUI_NODE_TEXT, nullptr); // 仅对文本组件使用默认反色算法。
    
    17. // 开发者自定义的反色算法函数。
    18. uint32_t colorInvertFunc(uint32_t color) {
    19.   return ~color;
    20. }
    21. OH_ArkUI_SetForceDarkConfig(nullptr, true, ArkUI_NodeType::ARKUI_NODE_TEXT, colorInvertFunc); // 仅对文本组件使用自定义反色算法。
    
    说明
    
    - 不支持全局禁用反色能力的同时仅对某类组件使用反色算法。
        
    - 不支持全局使用反色能力的同时仅对某类组件禁用反色算法。
        
    
2. 反色算法生效优先级说明。
    
    a. 使用开发者深色模式颜色资源的配置。
    
    b. 使用开发者为本进程中指定组件配置的反色算法。
    
    c. 使用开发者为本进程中所有组件配置的反色算法。
    
3. 反色能力逃生通道。
    
    从API version 21开始，基于开发者当前实现，开发者可以通过主动设置[allowForceDark](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-allow-force-dark#allowforcedark)属性，禁用指定组件的自动反色能力，维持深浅色切换时的原有逻辑，即使用主题或资源值切换。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-theme "主题设置")
# 设置应用内主题换肤

更新时间: 2025-12-16 16:39

## 概述

对于采用ArkTS开发的应用，提供了应用内组件的主题换肤功能，支持局部的深浅色切换及动态换肤。目前，该功能只支持设置应用内主题换肤，暂不支持在UIAbility或窗口层面进行主题设置，同时也不支持C-API和Node-API。

## 自定义主题色

当应用需要使用换肤功能时，应自定义主题颜色。[CustomTheme](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-theme#customtheme)用于自定义主题色的内容，其属性可选，仅需要复写需修改的部分，未修改内容将继承系统默认设置，可参考[系统默认的token颜色值](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/theme_skinning#%E7%B3%BB%E7%BB%9F%E7%BC%BA%E7%9C%81token%E8%89%B2%E5%80%BC)。请参照以下示例自定义主题色：

1.   // AppTheme.ets
2.   import { CustomColors, CustomTheme } from '@kit.ArkUI';

3.   export class AppColors implements CustomColors {
4.     // 自定义主题色
5.     brand: ResourceColor = '#FF75D9';
6.     // 使用$r，让一级警示色在深色和浅色模式下，设置为不同的颜色
7.     warning: ResourceColor = $r('sys.color.ohos_id_color_warning');
8.   }

9.   export class AppTheme implements CustomTheme {
10.     public colors: AppColors = new AppColors();
11.   }

12.   export let gAppTheme: CustomTheme = new AppTheme();

## 设置应用内组件自定义主题色

- 若在页面入口处设置应用内组件自定义主题色，需确保在页面build前执行[ThemeControl](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-theme#themecontrol).[setDefaultTheme](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-theme#setdefaulttheme)。
    
    示例代码中，[onWillApplyTheme](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#onwillapplytheme12)回调函数用于使自定义组件获取当前生效的Theme对象。
    
    1.   // Index.ets
    2.   import { Theme, ThemeControl } from '@kit.ArkUI';
    3.   import { gAppTheme } from './AppTheme';
    
    4.   //在页面build前执行ThemeControl
    5.   ThemeControl.setDefaultTheme(gAppTheme);
    
    6.   @Entry
    7.   @Component
    8.   struct DisplayPage {
    9.     @State menuItemColor: ResourceColor = $r('sys.color.background_primary');
    
    10.     onWillApplyTheme(theme: Theme) {
    11.       this.menuItemColor = theme.colors.backgroundPrimary;
    12.     }
    
    13.     build() {
    14.       Column() {
    15.         List({ space: 10 }) {
    16.           ListItem() {
    17.             Column({ space: '5vp' }) {
    18.               Text('Color mode')
    19.                 .margin({ top: '5vp', left: '14fp' })
    20.                 .width('100%')
    21.               Row() {
    22.                 Column() {
    23.                   Text('Light')
    24.                     .fontSize('16fp')
    25.                     .textAlign(TextAlign.Start)
    26.                     .alignSelf(ItemAlign.Center)
    27.                   Radio({ group: 'light or dark', value: 'light' })
    28.                     .checked(true)
    29.                 }
    30.                 .width('50%')
    
    31.                 Column() {
    32.                   Text('Dark')
    33.                     .fontSize('16fp')
    34.                     .textAlign(TextAlign.Start)
    35.                     .alignSelf(ItemAlign.Center)
    36.                   Radio({ group: 'light or dark', value: 'dark' })
    37.                 }
    38.                 .width('50%')
    39.               }
    40.             }
    41.             .width('100%')
    42.             .height('90vp')
    43.             .borderRadius('10vp')
    44.             .backgroundColor(this.menuItemColor)
    45.           }
    
    46.           ListItem() {
    47.             Column() {
    48.               Text('Brightness')
    49.                 .width('100%')
    50.                 .margin({ top: '5vp', left: '14fp' })
    51.               Slider({ value: 40, max: 100 })
    52.             }
    53.             .width('100%')
    54.             .height('70vp')
    55.             .borderRadius('10vp')
    56.             .backgroundColor(this.menuItemColor)
    57.           }
    
    58.           ListItem() {
    59.             Column() {
    60.               Row() {
    61.                 Column({ space: '5vp' }) {
    62.                   Text('Touch sensitivity')
    63.                     .fontSize('16fp')
    64.                     .textAlign(TextAlign.Start)
    65.                     .width('100%')
    66.                   Text('Increase the touch sensitivity of your screen' +
    67.                     ' for use with screen protectors')
    68.                     .fontSize('12fp')
    69.                     .fontColor(Color.Blue)
    70.                     .textAlign(TextAlign.Start)
    71.                     .width('100%')
    72.                 }
    73.                 .alignSelf(ItemAlign.Center)
    74.                 .margin({ left: '14fp' })
    75.                 .width('75%')
    
    76.                 Toggle({ type: ToggleType.Switch, isOn: true })
    77.                   .margin({ right: '14fp' })
    78.                   .alignSelf(ItemAlign.Center)
    79.               }
    80.               .width('100%')
    81.               .height('80vp')
    82.             }
    83.             .width('100%')
    84.             .borderRadius('10vp')
    85.             .backgroundColor(this.menuItemColor)
    86.           }
    87.           ListItem() {
    88.             Column() {
    89.               Text('Warning')
    90.                 .width('100%')
    91.                 .margin({ top: '5vp', left: '14fp' })
    92.               Button('Text')
    93.                 .type(ButtonType.Capsule)
    94.                 .role(ButtonRole.ERROR)
    95.                 .width('40%')
    96.             }
    97.             .width('100%')
    98.             .height('70vp')
    99.             .borderRadius('10vp')
    100.             .backgroundColor(this.menuItemColor)
    101.           }
    102.         }
    103.       }
    104.       .padding('10vp')
    105.       .backgroundColor('#dcdcdc')
    106.       .width('100%')
    107.       .height('100%')
    108.     }
    109.   }
    
- 若在UIAbility中设置应用内组件自定义主题色，需在onWindowStageCreate()方法的windowStage.[loadContent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#loadcontent9)的完成时回调中调用[ThemeControl](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-theme#themecontrol).[setDefaultTheme](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-theme#setdefaulttheme)，设置应用内组件的自定义主题色。
    
    1.   // EntryAbility.ets
    2.   import {AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    3.   import { hilog } from '@kit.PerformanceAnalysisKit';
    4.   import { window, CustomColors, ThemeControl } from '@kit.ArkUI';
    
    5.   class AppColors implements CustomColors {
    6.     fontPrimary = 0xFFD53032;
    7.     iconOnPrimary = 0xFFD53032;
    8.     iconFourth = 0xFFD53032;
    9.   }
    
    10.   const abilityThemeColors = new AppColors();
    
    11.   export default class EntryAbility extends UIAbility {
    12.     onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
    13.       hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
    14.     }
    
    15.     onDestroy() {
    16.       hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onDestroy');
    17.     }
    
    18.     onWindowStageCreate(windowStage: window.WindowStage) {
    19.       // Main window is created, set main page for this ability
    20.       hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageCreate');
    
    21.       windowStage.loadContent('pages/Index', (err, data) => {
    22.         if (err.code) {
    23.           hilog.error(0x0000, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
    24.           return;
    25.         }
    26.         hilog.info(0x0000, 'testTag', 'Succeeded in loading the content. Data: %{public}s', JSON.stringify(data) ?? '');
    27.         // 在onWindowStageCreate()方法中setDefaultTheme
    28.         ThemeControl.setDefaultTheme({ colors: abilityThemeColors });
    29.         hilog.info(0x0000, 'testTag', '%{public}s', 'ThemeControl.setDefaultTheme done');
    30.       });
    31.     }
    
    32.   }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163923.98224536496830314561772801639897:50001231000000:2800:02EA3C0A464DB5CEE653F5B53EC3C5D1D8832BE1A52CDC10D6705AD30D980D14.png)
    
    说明
    
    - 当setDefaultTheme的参数为undefined时，会清除先前设置的自定义主题，默认token值对应的色值参考[系统缺省token色值](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/theme_skinning#%E7%B3%BB%E7%BB%9F%E7%BC%BA%E7%9C%81token%E8%89%B2%E5%80%BC)。
        
    - setDefaultTheme需要在ArkUI初始化后即windowStage.loadContent的完成时回调中使用。
        
    

## 设置应用局部页面自定义主题风格

通过设置[WithTheme](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-with-theme)，将自定义主题Theme的配色应用于内部组件的默认样式。在WithTheme的作用范围内，组件的配色会根据Theme的配色进行调整。

如示例所示，使用WithTheme({ theme: this.CustomTheme })可将作用域内组件的配色设置为自定义主题风格。后续可以通过更新this.CustomTheme来更换主题风格。[onWillApplyTheme](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#onwillapplytheme12)回调函数用于使自定义组件能够获取当前生效的Theme对象。

1.   import { CustomColors, CustomTheme, Theme } from '@kit.ArkUI';

2.   class AppColors implements CustomColors {
3.     fontPrimary: ResourceColor = $r('app.color.brand_purple');
4.     backgroundEmphasize: ResourceColor = $r('app.color.brand_purple');
5.   }

6.   class AppColorsSec implements CustomColors {
7.     fontPrimary: ResourceColor = $r('app.color.brand');
8.     backgroundEmphasize: ResourceColor = $r('app.color.brand');
9.   }

10.   class AppTheme implements CustomTheme {
11.     public colors: AppColors = new AppColors();
12.   }

13.   class AppThemeSec implements CustomTheme {
14.     public colors: AppColors = new AppColorsSec();
15.   }

16.   @Entry
17.   @Component
18.   struct DisplayPage {
19.     @State customTheme: CustomTheme = new AppTheme();
20.     @State message: string = '设置应用局部页面自定义主题风格';
21.     count = 0;

22.     build() {
23.       WithTheme({ theme: this.customTheme }) {
24.         Row(){
25.           Column() {
26.             Text('WithTheme')
27.               .fontSize(30)
28.               .margin({bottom: 10})
29.             Text(this.message)
30.               .margin({bottom: 10})
31.             Button('change theme').onClick(() => {
32.               this.count++;
33.               if (this.count > 1) {
34.                 this.count = 0;
35.               }
36.               switch (this.count) {
37.                 case 0:
38.                   this.customTheme = new AppTheme();
39.                   break;
40.                 case 1:
41.                   this.customTheme = new AppThemeSec();
42.                   break;
43.               }
44.             })
45.           }
46.           .width('100%')
47.         }
48.         .height('100%')
49.         .width('100%')
50.       }
51.     }
52.   }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163923.81205166109118133056745366905822:50001231000000:2800:0C4C500D12C2A7A7D5A3BDA29679AA21D9B5FCD0B5CB31887E39842B3CB5A08A.gif)

## 设置应用页面局部深浅色

通过[WithTheme](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-with-theme)可以设置三种颜色模式，跟随系统模式，浅色模式和深色模式。

在WithTheme的作用范围内，组件的样式资源值会根据指定的模式，读取对应的深浅色模式系统和应用资源值。这意味着，在WithTheme作用范围内，组件的配色会根据所指定的深浅模式进行调整。

如下面的示例所示，通过WithTheme({ colorMode: ThemeColorMode.DARK })，可以将作用范围内的组件设置为深色模式。

设置局部深浅色时，需要添加dark.json资源文件，深浅色模式才会生效。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163923.03311128858046138432432237380717:50001231000000:2800:82771EDB9B6B8CC95E26EDE198EDD3723D15909BF013F7C5EFB1BECE6EFD451C.png)

dark.json数据示例：

1.   {
2.     "color": [
3.       {
4.         "name": "start_window_background",
5.         "value": "#000000"
6.       }
7.     ]
8.   }

9.   @Entry
10.   @Component
11.   struct DisplayPage {
12.     @State message: string = 'Hello World';
13.     @State colorMode: ThemeColorMode = ThemeColorMode.DARK;

14.     build() {
15.       WithTheme({ colorMode: this.colorMode }) {
16.         Row() {
17.           Column() {
18.             Text(this.message)
19.               .fontSize(50)
20.               .fontWeight(FontWeight.Bold)
21.             Button('Switch ColorMode').onClick(() => {
22.               if (this.colorMode === ThemeColorMode.LIGHT) {
23.                 this.colorMode = ThemeColorMode.DARK;
24.               } else if (this.colorMode === ThemeColorMode.DARK) {
25.                 this.colorMode = ThemeColorMode.LIGHT;
26.               }
27.             })
28.           }
29.           .width('100%')
30.         }
31.         .backgroundColor($r('app.color.start_window_background'))
32.         .height('100%')
33.         .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.END, SafeAreaEdge.BOTTOM, SafeAreaEdge.START])
34.       }
35.     }
36.   }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163923.97209813896207852416230702217996:50001231000000:2800:542E6DF8DE219CCC42AD24C07B22D8A4CE808460A071BDD5F057E14E68980A71.png)

## 系统缺省token色值

|Token|场景类别|Light|说明|Dark|说明|
|:--|:--|:--|:--|:--|:--|
|theme.colors.brand|品牌色|#ff0a59f7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163923.93233210688136543433991494425419:50001231000000:2800:BD81A86328BA8CBE8A991CAF740D739231CB72E0115A05393D720BFD501BF737.png)|#ff317af7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163923.09598927691456226714470583178030:50001231000000:2800:E83C46EA7AE00147ECE291693588B929CAD29342689881E0535F4AB070A660D3.png)|
|theme.colors.warning|一级警示色|#ffe84026|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.06276649311570231294625861733081:50001231000000:2800:9031D0CF26807CEB04CBF09ECC68BB9B7DB96AFD15BD3D947ED9F7CA0F68FBC2.png)|#ffd94838|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.01250406263429529186302576136800:50001231000000:2800:62B45E1B457A88E15AF79D28AD44A758E8FD393148E97A06BAF9BCA55EB66A85.png)|
|theme.colors.alert|二级警示色|#ffed6f21|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.61294821864800777923423425851862:50001231000000:2800:CE292C76136E986C49FE6E18513705841F14FCF9FAA45494F46D162552262E35.png)|#ffdb6b42|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.11942839774288813253707558078750:50001231000000:2800:40967B184CAA979A3FAF0C31C22335E2AD21CD173C83D7D44A92E6970298CFC5.png)|
|theme.colors.confirm|确认色|#ff64bb5c|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.72112757273824508267297875594275:50001231000000:2800:F9B857B37C707A9CCD48873374BC8BCD34DCD182730DD0C9BC0B92E2A30F28DA.png)|#ff5ba854|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.92276821072805977035134494343574:50001231000000:2800:D35442327E83DFD054F3E540A41904196E4EA8095AA7F0E40898C823058BAFFF.png)|
|theme.colors.fontPrimary|一级文本|#e5000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.34893493429456726563755525436972:50001231000000:2800:257CDAFE05B3CC7AE37DE26E244A12986C2D9DBCBDC947B56C2B1756B1F2EA51.png)|#e5ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.35944335596529602617518833371574:50001231000000:2800:5B11F72E09EA1A3C55B4FC535F6B850B9C276CA1C95E49665A045246DC8E79FE.png)|
|theme.colors.fontSecondary|二级文本|#99000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.83105099563762590263527495238374:50001231000000:2800:BEA486508B37D432DBC2B823251F4A372ACA6B045BCA0E5B242EBA0B9C9ABA2B.png)|#99ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.36806938875442947512259809545746:50001231000000:2800:858072F413880749C699659C3DE6A008C9664EB4F6CEB436CE7C44C8C070FF99.png)|
|theme.colors.fontTertiary|三级文本|#66000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.41556591117756717276260074286502:50001231000000:2800:2273644D2EAD5B496423CCF4C780D43FC73E0FD28C6B3CD7454E91B3D4E77260.png)|#66ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.70464506588050983739724689074516:50001231000000:2800:5C31E01045C37C4A853543AC6CADB2AC1F81A85259DF3267D614CE8EE92FA763.png)|
|theme.colors.fontFourth|四级文本|#33000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.68708479294525057346213475850966:50001231000000:2800:A14343D7A7F523B20A90BAFAD69734454D487D1A1F1C8C014BD7434CFBAF9555.png)|#33ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.20691430644158126599963731582966:50001231000000:2800:5D0293BD4642C0530DDD948DE05AD46C4B7DF7B88545758E243C541BA9EA7164.png)|
|theme.colors.fontEmphasize|高亮文本|#ff0a59f7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.57163739798236105069158890474658:50001231000000:2800:2519AB50C0F39D7941E52CE7E7C8D606CAC00B3672BC69F6EE1725ABE89A2BD7.png)|#ff317af7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.55519003843972444083268366946369:50001231000000:2800:64244ACF76D36D3EC34D9969A12CCA0E330F7CCB54AC677091BAC14CAB6CDCDE.png)|
|theme.colors.fontOnPrimary|一级文本反色|#ffffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163924.77794510541720461106634748932103:50001231000000:2800:7029F1A888DDB0BD5F1DE8BCE5F0AE6DA35F1D1A9AFE3321F5C64FCFEDCFF5B8.png)|#ff000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.41003923568267853665513596613441:50001231000000:2800:88283DC54DB1F88194E761C0154B3BF063E6782DACA9F8F6AE5EB02DCB1EAD60.png)|
|theme.colors.fontOnSecondary|二级文本反色|#99ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.21377058401174125039299041522182:50001231000000:2800:C3867CF5CD075B0419316303EA94BC0F99D0D0363D9BBAD380A381B95D375BA1.png)|#99000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.11905225010696509098356082494644:50001231000000:2800:9F030C104E2C3DDB34B0153DF9FEF960570856755ECD16ACA0FB8E63CA1F1B0F.png)|
|theme.colors.fontOnTertiary|三级文本反色|#66ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.55575113559872916854989135504354:50001231000000:2800:7CF91325BB4B9DCC1C632AF8DED85AD0D432F77380A81A15BE0020588BB35A82.png)|#66000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.64478543832109655494468003838290:50001231000000:2800:724067959F6D7559007E1A66F633242E1129C6220C4E2D93433161DC4E64EEF4.png)|
|theme.colors.fontOnFourth|四级文本反色|#33ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.91322022012524370820998539886794:50001231000000:2800:24454579CD948749B044138A021FA9D846ECBE43F74EC56E7965A86BC6FC100A.png)|#33000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.21972539980532463795985086669000:50001231000000:2800:87F0E17C9D7EAAA013829ADD5FEAB4D0D2BEB1D1BA1820BEFE959525040BA9D8.png)|
|theme.colors.iconPrimary|一级图标|#e5000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.81914850111042091243474378437998:50001231000000:2800:8685050A6D2DD49744868EB418B2D4CD1EE543E76A384B91137B54BD292AF307.png)|#e5ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.88052341025626008628554380523985:50001231000000:2800:7771C11D64E895C8A68239E07F2D4B6D4FB3473AD3247C7832810AA4A59528E3.png)|
|theme.colors.iconSecondary|二级图标|#99000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.59486838196516909284363231161503:50001231000000:2800:896D6D6723C1D46185F0C47823C5C5150BD0E18BEFBD2D8484CBE1F30D286BF6.png)|#99ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.13582147319476876327276081299542:50001231000000:2800:BBDDCC437E7537FBAFAB0873EF7BA8B0A905E9FFD3BCB6C4FE52EA96DE1E85DC.png)|
|theme.colors.iconTertiary|三级图标|#66000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.38408596317367716086190698578800:50001231000000:2800:4153A613AED32BE8C5CD861755B82C879BFACF3D55559DE27DB6AF0C64FDF221.png)|#66ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.45206633614720296413191029641684:50001231000000:2800:DD3F6B1AFCCBB5CA5FC92973C56DFB41B492163BD42B9E402B648B665DAE9B9A.png)|
|theme.colors.iconFourth|四级图标|#33000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.93026245459930595156638494550043:50001231000000:2800:F73785211AD7C8F8CA827953BC717DDE8D076921190A6D2D19F61B530E46AED0.png)|#33ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.16512584652874608888950783463351:50001231000000:2800:16039FCC3046A0B1F0C48A76815FAEAE837CF29F79BFED082200CA342163B4E4.png)|
|theme.colors.iconEmphasize|高亮图标|#ff0a59f7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.97978961429593084684436863386728:50001231000000:2800:883E1A6A4A2A32AEC8AC23AAF245096909E60EA441C64C3F561118AFD3C3302B.png)|#ff317af7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.87336210531561927531775423960120:50001231000000:2800:558538707886992BC51DC25C359A6F2B9D6DF66340F23899BF1C064EB098120D.png)|
|theme.colors.iconSubEmphasize|高亮辅助图标|#660a59f7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163925.27040515825524394863219036434872:50001231000000:2800:AC3B0BA3F6A53960F68CDCF61BEFE88D56F15B0646565593B816121AA46CDBB2.png)|#66317af7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.16743617704795349534887450963792:50001231000000:2800:57F93A8E1DB8D7A0AB7E178AB0B4846D5C949419711EB7A61E78EBB6A94E5488.png)|
|theme.colors.iconOnPrimary|一级图标反色|#ffffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.69916674245970946977905379083420:50001231000000:2800:BD811F475208E0E12ECA48A8BC3E49C54538861DB225441AB30D458316456501.png)|#ff000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.13554496313687973087108229340127:50001231000000:2800:D134452EF565805FDBA4977A22373ED0F1C0670D7F41CB99DB58F462FA9E187D.png)|
|theme.colors.iconOnSecondary|二级图标反色|#99ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.37550362457025142204001213951206:50001231000000:2800:600FCECF58070CA79112C58407931CE801329E092B643DBCDE5F1BCFC63652AF.png)|#99000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.65857086628433015496369640110540:50001231000000:2800:A213A5416EC7022BFF863BB257F1119A5468B7A90D34A9ACA5CD4FF096A6FC80.png)|
|theme.colors.iconOnTertiary|三级图标反色|#66ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.96609526000825669042518662337931:50001231000000:2800:C92B09B1C6B0D7ACEF2DBC71585A8427E48F38F0AEA8CBDC8679FDC575F52750.png)|#66000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.25028926271719406405253359661535:50001231000000:2800:E1443D435C0D0521BA1B5528E0E9E2768B3CB214E746268E3792354E2DE6C555.png)|
|theme.colors.iconOnFourth|四级图标反色|#33ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.04987057813411778312438399615661:50001231000000:2800:0CF1B75C8D3F35469F1CEA25E62F3443C3CB5F5F010D4373B4BCC4EC49141A9C.png)|#33000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.20870981158417776456582797544950:50001231000000:2800:6B9AE879482A6270F2A52BFF7421FB66A6D3CF7E1985D870107C8484D267B0C7.png)|
|theme.colors.backgroundPrimary|一级背景（实色/不透明色）|#ffffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.92457202488750549391496200694100:50001231000000:2800:4497B17C82DE0648E38BFBD1AC7B208884E9BB12F038867FA68EF4E878A39984.png)|#ffe5e5e5|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.29222167415791408403056850373295:50001231000000:2800:5181ACB8EE4F1A8178E48CE4AA43E4B8286A5D156876CEDC459C375D66DDE6AE.png)|
|theme.colors.backgroundSecondary|二级背景（实色/不透明色）|#fff1f3f5|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.40315307155181697376941804965540:50001231000000:2800:A5133A473D834C16731E84F92EF81DFDC6E1BB6B952540C243972413ACF56548.png)|#ff191a1c|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.41984656912567949564090049205289:50001231000000:2800:CFE6622D788A5059DEA6988F480F37E325EB8CC2A6EC8E9109876481137C05CB.png)|
|theme.colors.backgroundTertiary|三级背景（实色/不透明色）|#ffe5e5ea|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.10775492035417231522524725227871:50001231000000:2800:459ED835E7045DB707D7D034F106EF3CF1E127BF5098D5DFC94B4A97D11A9043.png)|#ff202224|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.23679517815513215643216175308298:50001231000000:2800:6D994C02869968B4F10438571A97C4F30E12138CC9E1421282F9F2C969E9C063.png)|
|theme.colors.backgroundFourth|四级背景（实色/不透明色）|#ffd1d1d6|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.19795240993015141435963647739022:50001231000000:2800:2E09B6D8977FAB454BFBFF5CB6D3436EB4762C010B46607F4BBE29D10DA6FC50.png)|#ff2e3033|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.36427782390981980940627831333739:50001231000000:2800:D503883863B61B1B8358E93FCE41C3D1D8203C0FF3CB614D76FE6615E5A6A071.png)|
|theme.colors.backgroundEmphasize|高亮背景（实色/不透明色）|#ff0a59f7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.63880087046190605707063993721781:50001231000000:2800:C80371D5D724CC4DCA84CC5A91EC50949050CCC67602F6D10FDB0E92890D3A23.png)|#ff317af7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.27210723067555295570631182241673:50001231000000:2800:5A641AE145FA5C84E6054FE8879FFCC475997AB17D364115602A3E38F1D812C9.png)|
|theme.colors.compForegroundPrimary|前背景|#ff000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163926.16546827767373822089935293711678:50001231000000:2800:523F6998DAD168B3B119FDAB3B2D83A2ED1AFD726A424EA0CF3ACA9CEC481320.png)|#ffe5e5e5|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.27778686800062364716380518864181:50001231000000:2800:2DB7FF9FD0701809195CC48A879D823AF6043DDAA3983008397B2DAC7B4C88CA.png)|
|theme.colors.compBackgroundPrimary|白色背景|#ffffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.26942864723921763674836962761490:50001231000000:2800:3EA08E5D1784A29E173E33FD06BF208FF1606BE67A1AB6F553A42884AE987296.png)|#ffffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.56692330826750320765236054117252:50001231000000:2800:A5A49E9D568A57388CD2F35AE5B0B6891C05D690DE84BB6B468E172708F7CFF4.png)|
|theme.colors.compBackgroundPrimaryTran|白色透明背景|#ffffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.29867364657998665399234982754841:50001231000000:2800:4B33B8A821E9E01A2F7053029FE2ABF2E342B66969AB45D83C4D765DAFE16A92.png)|#33ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.14339468187883462547833262177687:50001231000000:2800:7123804ADA865481F3B47BE4DA527D0D2D0949E52C997D8A47B5268853BD7CD1.png)|
|theme.colors.compBackgroundPrimaryContrary|常亮背景|#ffffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.35549401023304584957952117669676:50001231000000:2800:5316A6A3452B45DF15F185EAC802A8112B815B60AB3CE1D64124B77FD007AE4A.png)|#ffe5e5e5|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.25918220676942745135221066718384:50001231000000:2800:C9E0B71D9C752770162D00E7F9DA64BD3C91E3111EB188A09B5F5E1157FFFE11.png)|
|theme.colors.compBackgroundGray|灰色背景|#fff1f3f5|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.57325232720639447924063728100360:50001231000000:2800:F6F7BBC99F3A7D6C20759B5CCE5A247222BA78F77723905F10EDF073C4B71D04.png)|#ffe5e5ea|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.42484836715340202887821794094749:50001231000000:2800:9A725891ECF3AC707933EFCBC6E0F64A5792277D7401DA8DC3138B001B90FB9C.png)|
|theme.colors.compBackgroundSecondary|二级背景|#19000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.17724014439132191788407086921731:50001231000000:2800:192343780C2151F1FE73BECFC4D9EA95F2603CEC572EB983005809E89908FAEC.png)|#19ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.94231040549219511268802492548788:50001231000000:2800:8ED870325B2E4CDB1027DE087B628AAC603BA23D7FA98C3F102CA578F064AC4C.png)|
|theme.colors.compBackgroundTertiary|三级背景|#0c000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.68074312221938954192304130588833:50001231000000:2800:B38ED1876A5AE5E9E73D028DB1FE058695520D9036B3F3DB8349E61489D5EE6C.png)|#0cffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.47267136253413863735574760734268:50001231000000:2800:25ACA7E9953B8C3D33C21F30CFF19E21C1932AE2A7C30BEB83FD96ABB271FD70.png)|
|theme.colors.compBackgroundEmphasize|高亮背景|#ff0a59f7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.08959515066368672103257796584249:50001231000000:2800:EECC30D3EF24CF36698EB03434DF3686C4B1045447F2A52A620CDF7A227D840E.png)|#ff317af7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.93770610566298047738266560375221:50001231000000:2800:177FF21CFC0D98A38D2D5975BB4D1F50A0D069494C9E5EB474ED542BD4C81130.png)|
|theme.colors.compBackgroundNeutral|黑色中性高亮背景|#ff000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.10636660642202581300717600270456:50001231000000:2800:6AB8D15DFF26B50DF7ADB84BC3D9A2C4430184866F431F864545C4D53E46530C.png)|#ffffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.08300596343561615963457149662051:50001231000000:2800:583ABE310F550B41C65BF76596C80B18461658E20F2D66B629B1EB53C9EF726E.png)|
|theme.colors.compEmphasizeSecondary|20%高亮背景|#330a59f7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.20968371984545588865966646267528:50001231000000:2800:94DCB5B29A0C3D8CC0A1DE604621C3A909E4E759FC25D18B26148DD0543C08AE.png)|#33317af7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163927.21629999732880023396237603673658:50001231000000:2800:716B30F50EAF5539E17B5DFA6326060EAEDEF2403CF2B2A2898872D97D8B891B.png)|
|theme.colors.compEmphasizeTertiary|10%高亮背景|#190a59f7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.27353321507975658135385290898469:50001231000000:2800:ACC0EF8289BC7BC53325A061E9E3F49FEFBAE957997C4CE8C4520C594DC2E235.png)|#19317af7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.90939336618275230349726072448316:50001231000000:2800:0419F84AA4C3F09D1E2FD65EFFF44445737589A2EE8BA4F79A4DF50016A59DF1.png)|
|theme.colors.compDivider|分割线颜色|#33000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.63721510053182716188825528903391:50001231000000:2800:11222CF08926D548F8A61C4A9BEDDA51CF95F0FF0F81316733B3C5411BB742B2.png)|#33ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.22284297071152138471783692907240:50001231000000:2800:AB26DEE7BF265EE394339F11DA215417554BAA3C1CF4058CEC4FF760830410E4.png)|
|theme.colors.compCommonContrary|通用反色|#ffffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.52150626310899878820096236623234:50001231000000:2800:2CCDD2FB20CDE32F6F9365761FF2E23D549C75B0AE5ED395A4EA2F983ABDA08B.png)|#ff000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.81067736066056502077801402283824:50001231000000:2800:0A1B8F3BCD057335FA9D7D0F1D87750FAE8A9879614F0B1F6C0B69E319D20FF9.png)|
|theme.colors.compBackgroundFocus|获焦态背景色|#fff1f3f5|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.56259489599630245959143460593336:50001231000000:2800:F3B4708991E4B8803305C4B11FD8B20BD02545B40CC14CC60BDC95B498FA44DC.png)|#ff000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.51962980433950404922474422105482:50001231000000:2800:10A8765E10AC809F1074295492021D6A4BF1E95A56175F733833025D74C0FD27.png)|
|theme.colors.compFocusedPrimary|获焦态一级反色|#e5000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.46995042908056647827732057937530:50001231000000:2800:BA4BE4FF564341F63161FC57AC0C51C62EA996A4337366B62156BDB81394C04C.png)|#e5ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.84712927199110949736647588122272:50001231000000:2800:4267E9E8E4A145BA8BF875927B3051D6EA591C936854239811F9DFECBFD61198.png)|
|theme.colors.compFocusedSecondary|获焦态二级反色|#99000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.92644120303067813067512659549933:50001231000000:2800:CF71102FB8CD72DD027B855B4A42AC06458F92F835761407211AF1FD82E65D71.png)|#99ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.63169635052471731562191968274401:50001231000000:2800:423F6671BB57740F2EB8AE940E288E76152117B4673C55E902D03D02FB503E26.png)|
|theme.colors.compFocusedTertiary|获焦态三级反色|#66000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.17146495293153968917353698046372:50001231000000:2800:BCA3A9CD1601EDCD34A50A58D61A3693409DBF52AD509055745E65518DE98268.png)|#66ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.80579384956078495595688911102464:50001231000000:2800:DC69CF0B48D446B8EFD36185FE2B7C1FCEF765DEBDCDC3C2A09C3DBC3DF82D3C.png)|
|theme.colors.interactiveHover|通用悬停交互式颜色|#0c000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.46531194107682566533177703921422:50001231000000:2800:2DD8335A4CAA8606279B75B2D8E22DF28BDFF19F184412164221045E852BE597.png)|#0cffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163928.27331655802519641880606181661483:50001231000000:2800:726D6C7DCB4B0409171FFAFF9843F0F8A2A0526421BDEC550D0E6AFAA8B81FD7.png)|
|theme.colors.interactivePressed|通用按压交互式颜色|#19000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163929.58511770410322026595769974922782:50001231000000:2800:A5EDD8A26B0AC9FB9E248B49656793DFDB5A84FBEB7F41D45278133A426BB20F.png)|#19ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163929.26550115332181715713710897776958:50001231000000:2800:D8CD9D091031267D8B8156A7890AE8CB8CCC549D2D2F3F7B93A0E45CEC26EC1F.png)|
|theme.colors.interactiveFocus|通用获焦交互式颜色|#ff0a59f7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163929.00698460457109217980713394479224:50001231000000:2800:F3CFA6B10CCBF5EB2ABD7EFDA09884797F5C6B3013831EDE08AF7D3F0CEF3F1B.png)|#ff317af7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163929.72119982093006187759877467353371:50001231000000:2800:52455B728F546FE10DB6BACB8AE0B7DF4F18E21FF99DB1337A48486F947B6DC0.png)|
|theme.colors.interactiveActive|通用激活交互式颜色|#ff0a59f7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163929.49048947680564088685627530208011:50001231000000:2800:A74378E43B7813650F4039966F7D1F03EA61401A5B20E76E13F5123D4C4BEA25.png)|#ff317af7|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163929.62885399959658551291120352016043:50001231000000:2800:874839AD5BCC387A7FF03F235554ACBC55FF894703643EA0664F86E8E13FBD09.png)|
|theme.colors.interactiveSelect|通用选择交互式颜色|#33000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163929.40142185206856221551583494385901:50001231000000:2800:0CF12E93BB2A81AA262EB7E8E83D997599259E4A3C5679DA82748CA1D3813E99.png)|#33ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163929.73745404527753051382050617205356:50001231000000:2800:C1EDA2E9CFB491C5C5B9DA01FEA29D8B68AAE7B4456ADBB694AE059A0846A3A3.png)|
|theme.colors.interactiveClick|通用点击交互式颜色|#19000000|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163929.97686333532634336630291694224819:50001231000000:2800:58A06810CFDF6FFB750356595E33542405A0EA9C36B858B7AD4D9B2722461FA5.png)|#19ffffff|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163929.52570323210719635769722202429641:50001231000000:2800:76E974DEE3FEE37B5A1775F1F28EBE9C904A0B4DF1C0CB2F17A6C1A3A37DA965.png)|

各个token色值可影响的组件可参考[Colors](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-theme#colors)接口说明。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-dark-light-color-adaptation "应用深浅色适配")
# 使用UI上下文接口操作界面（UIContext）

更新时间: 2025-12-16 16:39

本文主要介绍了多UI实例涉及的概念，以及使用[UIContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext)的方法替换全局接口的原因，并提供了相应的替换方案。

## 基本概念

**UI实例：** UI实例是用于管理用户界面的对象，主要负责组件、布局、动画以及交互事件等UI功能的管理。每个窗口对象都会创建并管理一个UI实例。

**UI上下文：** UI上下文是指UI实例运行环境的抽象概念，UI功能在UI上下文中运行，其效果最终反映在相应的UI实例中。

**全局接口：** ArkUI提供的一系列全局接口，这些接口在调用时无需显式指定UI实例或组件。它们会根据调用发生时所在的UI上下文，自动作用于相应的UI实例。

## UI上下文不明确

UI上下文不明确是指调用ArkUI全局接口时，调用点无法明确指认UI实例的问题。

当前的系统支持两种[应用模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-models)——FA模型和Stage模型。在FA模型中，每个UI实例拥有独立的ArkTS引擎，全局接口可以通过ArkTS引擎跟踪到对应的UI实例上，因此不存在UI上下文不明确的问题。

在Stage模型中，一个ArkTS引擎中可运行多个ArkUI实例。全局接口通过分析调用链中的上下文信息来确定当前UI上下文，异步接口和非UI接口可能导致UI上下文跟踪失败。

为了保证全局接口的相关功能正常，开发者应当使用UIContext的接口替换全局接口。

下图展示了Stage模型下ArkTS引擎和UI上下文的对应关系，一个ArkTS引擎中存在两个[Ability](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/abilitykit-overview)，这些Ability对应了三个窗口，三个窗口各自对应一个ArkUI实例。

**图1** 多实例关系图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163900.83009349879482187090346532705117:50001231000000:2800:F7C661E5E07F0F2DD8FEB6DA2D63257816245377A88166D2D1B18A935FF8D5F8.png)

## UIContext接口替换全局接口的关系

部分多实例替代接口如下表所示，UIContext实例支持的全量接口以[UIContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext)中描述为准。

示例代码使用的接口中，[isAvailable](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext#isavailable20)从API version 20开始生效，其余接口从API version 18开始生效。

|全局接口|替代接口|说明|
|:--|:--|:--|
|@ohos.animator|createAnimator|自定义动画控制器|
|@ohos.arkui.componentSnapshot|getComponentSnapshot|组件截图|
|@ohos.arkui.componentUtils|getComponentUtils|组件工具类|
|@ohos.arkui.dragController|getDragController|拖拽控制器|
|@ohos.arkui.inspector|getUIInspector|组件布局回调|
|@ohos.arkui.observer|getUIObserver|无感监听|
|@ohos.font|getFont|自定义字体|
|@ohos.measure|getMeasureUtil|文本计算|
|@ohos.mediaquery|getMediaQuery|媒体查询|
|@ohos.promptAction|getPromptAction|弹窗|
|@ohos.router|getRouter|页面路由|
|AlertDialog|showAlertDialog|警告弹窗|
|ActionSheet|showActionSheet|列表选择弹窗|
|CalendarPickerDialog|不支持|日历选择器弹窗|
|DatePickerDialog|showDatePickerDialog|日期滑动选择弹窗|
|TimePickerDialog|showTimePickerDialog|时间滑动选择器弹窗|
|TextPickerDialog|showTextPickerDialog|文本滑动选择器弹窗|
|ContextMenu|getContextMenuController|菜单控制|
|vp2px/px2vp/fp2px/px2fp/lpx2px/px2lpx|vp2px/px2vp/fp2px/px2fp/lpx2px/px2lpx|像素单位转换|
|focusControl|getFocusControl|焦点控制|
|cursorControl|getCursorControl|光标控制|
|getContext|getHostContext|获取当前的Ability的Context|
|LocalStorage.getShared|getSharedLocalStorage|获取Ability传递的Storage|
|animateTo|animateTo|显式动画|
|animateToImmediately|不支持|显式立即动画|

## 常见UIContext接口替换全局接口的场景

以下UIContext接口替换全局接口示例以[像素单位](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-pixel-units)接口为例。

### 通过自定义组件获取UIContext

当全局接口在[自定义组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-js-custom-components)的成员方法或组件生命周期方法等其他作用域中，且this指向自定义组件时，可以通过调用自定义组件的成员方法[getUIContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-api#getuicontext)来获取UIContext对象。

说明

1. 在异步调用的回调方法中使用getUIContext，或者该接口的起始调用不在当前页面时，可能会在自定义组件销毁后调用接口，从而导致返回undefined。
2. 该方法只能通过this调用，不能通过new关键字创建的自定义组件对象调用。
3. 通过在[自定义声明式节点 (BuilderNode)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-user-defined-arktsnode-buildernode)中创建的自定义节点获取的UIContext与创建BuilderNode的UIContext指向同一个UI实例。

使用全局接口：

1. // pages/NewGlobal.ets
2. import { hilog } from '@kit.PerformanceAnalysisKit';

3. const DOMAIN = 0x0000;

4. @Entry
5. @Component
6. struct Index {
7.   build() {
8.     RelativeContainer() {
9.       Text('Calculate 20vp to px')
10.         .fontWeight(FontWeight.Bold)
11.         .alignRules({
12.           center: { anchor: '__container__', align: VerticalAlign.Center },
13.           middle: { anchor: '__container__', align: HorizontalAlign.Center }
14.         })
15.         .onClick(() => {
16.           let pxValue = vp2px(20);
17.         })
18.     }
19.     .height('100%')
20.     .width('100%')
21.   }
22. }

使用UIContext接口替换：

1. import { hilog } from '@kit.PerformanceAnalysisKit';

2. const DOMAIN = 0x0000;

3. @Entry
4. @Component
5. struct Index {
6.   build() {
7.     RelativeContainer() {
8.       Text('Calculate 20vp to px')
9.         .fontWeight(FontWeight.Bold)
10.         .alignRules({
11.           center: { anchor: '__container__', align: VerticalAlign.Center },
12.           middle: { anchor: '__container__', align: HorizontalAlign.Center }
13.         })
14.         .onClick(() => {
15.           let uiContext = this.getUIContext();
16.           let pxValue = uiContext.vp2px(20);
17.           hilog.info(DOMAIN, 'testTag', `20vp equals to ${pxValue}px`);
18.         })
19.     }
20.     .height('100%')
21.     .width('100%')
22.   }
23. }

### 通过窗口对象获取UIContext对象

开发者可以通过窗口对象的[getUIContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#getuicontext10)方法获取UIContext对象。

说明

1. 必须在UI实例创建完成后，才可以通过窗口对象的getUIContext方法获取UIContext。建议在loadContent的成功回调中调用，以确保UI实例准备就绪。
2. vp2px/px2vp在UI实例未创建时会获取默认值进行计算，替换时可考虑获取当前默认的[Display](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-display#display)对象的逻辑像素密度进行计算结果，可参考[像素单位转换接口替换为UIContext接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-global-interface#%E5%83%8F%E7%B4%A0%E5%8D%95%E4%BD%8D%E8%BD%AC%E6%8D%A2%E6%8E%A5%E5%8F%A3%E6%9B%BF%E6%8D%A2%E4%B8%BAuicontext%E6%8E%A5%E5%8F%A3)。

使用全局接口：

1. // entryability/EntryAbility.ets
2. import { AbilityConstant, ConfigurationConstant, UIAbility, Want } from '@kit.AbilityKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';
4. import { window } from '@kit.ArkUI';

5. const DOMAIN = 0x0000;

6. export default class EntryAbility extends UIAbility {
7.   // ...

8.   onWindowStageCreate(windowStage: window.WindowStage): void {
9.     hilog.info(DOMAIN, 'testTag', '%{public}s', 'Ability onWindowStageCreate');
10.     // 在loadContent前调用时，vp2px会根据屏幕默认像素密度返回计算结果。
11.     let pxValue = vp2px(20);
12.     hilog.info(DOMAIN, 'testTag', `20vp equals to ${pxValue}px`);
13.     windowStage.loadContent('pages/Index', (err) => {
14.       if (err.code) {
15.         hilog.error(DOMAIN, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err));
16.         return;
17.       }
18.       // 需要在回调中调用。
19.       let pxValue = vp2px(20);
20.       hilog.info(DOMAIN, 'testTag', `20vp equals to ${pxValue}px`);
21.     });
22.     // loadContent是异步接口，在此处调用不能保证UI实例已经创建成功。
23.     pxValue = vp2px(20);
24.     hilog.info(DOMAIN, 'testTag', `20vp equals to ${pxValue}px`);
25.   }

26.   // ...
27. }

使用UIContext接口替换：

1. import { AbilityConstant, ConfigurationConstant, UIAbility, Want } from '@kit.AbilityKit';
2. import { hilog } from '@kit.PerformanceAnalysisKit';
3. import { window } from '@kit.ArkUI';

4. const DOMAIN = 0x0000;

5. export default class EntryAbility extends UIAbility {
6.   // ...

7.   onWindowStageCreate(windowStage: window.WindowStage): void {
8.     hilog.info(DOMAIN, 'testTag', '%{public}s', 'Ability onWindowStageCreate');
9.     let window = windowStage.getMainWindowSync();
10.     // 在loadContent前调用getUIContext时，UI实例未创建，存在异常。
11.     windowStage.loadContent('pages/Index', (err) => {
12.       if (err.code) {
13.         hilog.error(DOMAIN, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err));
14.         return;
15.       }
16.       // 需要在回调中调用。
17.       try {
18.         let uiContext = window.getUIContext();
19.         if (!uiContext) {
20.           hilog.error(DOMAIN, 'testTag', `Can't get UIContext`);
21.           return;
22.         }
23.         let pxValue = uiContext.vp2px(20);
24.         hilog.info(DOMAIN, 'testTag', `20vp equals to ${pxValue}px`);
25.       } catch(e) {
26.         hilog.error(DOMAIN, 'testTag', `Can't get UIContext, ${e}`);
27.       }
28.     });
29.     // loadContent是异步接口，在此处调用不能保证UI实例已经创建成功。
30.   }

31.   onWindowStageDestroy(): void {
32.     hilog.info(DOMAIN, 'testTag', '%{public}s', 'Ability onWindowStageDestroy');
33.     // 在窗口销毁时需要移除失效的UIContext
34.     PixelUtils.removeUIContext();
35.   }

36.   // ...
37. }

### 在封装的接口中获取UI上下文

开发者通常在封装的接口中使用全局接口。对于这类场景，应优先考虑增加UIContext类型的入参。如果应用只有一个窗口，可以使用全局存储对象来保存UIContext。

说明

1. 创建UI实例是异步过程，需要在回调中调用窗口对象的getUIContext来获取UIContext对象。
2. 建议增加可选的UIContext入参，方便调用者传入UIContext。
3. vp2px/px2vp在UI实例未创建时会获取默认值进行计算，替换时可考虑获取当前默认的Display对象的逻辑像素密度进行计算，可参考[像素单位转换接口替换为UIContext接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-global-interface#%E5%83%8F%E7%B4%A0%E5%8D%95%E4%BD%8D%E8%BD%AC%E6%8D%A2%E6%8E%A5%E5%8F%A3%E6%9B%BF%E6%8D%A2%E4%B8%BAuicontext%E6%8E%A5%E5%8F%A3)。

使用全局接口：

1. // common/Utils.ets
2. class PixelUtils {
3.   static vp2px(vpValue: number) : number {
4.     return vp2px(vpValue);
5.   }

6.   static fp2px(fpValue: number) : number | undefined {
7.     return fp2px(fpValue);
8.   }

9.   static lpx2px(lpxValue: number) : number | undefined {
10.     return lpx2px(lpxValue);
11.   }
12. }

使用UIContext接口替换：

1. // common/Utils.ets
2. import { hilog } from '@kit.PerformanceAnalysisKit';

3. const DOMAIN = 0x0000;

4. export class PixelUtils {
5.   static uiContext : UIContext | undefined;
6.   static setUIContext(uiContext : UIContext): void {
7.     PixelUtils.uiContext = uiContext;
8.   }

9.   static removeUIContext(): void {
10.     PixelUtils.uiContext = undefined;
11.   }

12.   static vp2px(vpValue: number, uiContext?: UIContext): number | undefined {
13.     let _uiContext = uiContext??PixelUtils.uiContext;
14.     if (!_uiContext || !_uiContext.isAvailable()) {
15.       hilog.error(DOMAIN, 'testTag', `Can't get UIContext`);
16.       return undefined;
17.     }
18.     return _uiContext.vp2px(vpValue)
19.   }

20.   static fp2px(fpValue: number, uiContext?: UIContext): number | undefined {
21.     let _uiContext = uiContext??PixelUtils.uiContext;
22.     if (!_uiContext || !_uiContext.isAvailable()) {
23.       hilog.error(DOMAIN, 'testTag', `Can't get UIContext`);
24.       return undefined;
25.     }
26.     return _uiContext.fp2px(fpValue)
27.   }

28.   lpx2px(lpxValue: number, uiContext?: UIContext): number | undefined {
29.     let _uiContext = uiContext??PixelUtils.uiContext;
30.     if (!_uiContext || !_uiContext.isAvailable()) {
31.       hilog.error(DOMAIN, 'testTag', `Can't get UIContext`);
32.       return undefined;
33.     }
34.     return _uiContext.lpx2px(lpxValue)
35.   }
36. }

37. // entryability/EntryAbility.ets
38. import { UIAbility } from '@kit.AbilityKit';
39. import { hilog } from '@kit.PerformanceAnalysisKit';
40. import { window } from '@kit.ArkUI';
41. import { PixelUtils } from '../common/Utils';

42. const DOMAIN = 0x0000;

43. export default class EntryAbility extends UIAbility {
44.   // ...

45.   onWindowStageCreate(windowStage: window.WindowStage): void {
46.     hilog.info(DOMAIN, 'testTag', '%{public}s', 'Ability onWindowStageCreate');
47.     let window = windowStage.getMainWindowSync();
48.     windowStage.loadContent('pages/Index', (err) => {
49.       if (err.code) {
50.         hilog.error(DOMAIN, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err));
51.         return;
52.       }
53.       // 需要在回调中调用。
54.       try {
55.         let uiContext = window.getUIContext();
56.         PixelUtils.setUIContext(uiContext);
57.       } catch(e) {
58.         hilog.error(DOMAIN, 'testTag', `Can't get UIContext, ${e}`);
59.       }
60.     });
61.   }

62.   onWindowStageDestroy(): void {
63.     hilog.info(DOMAIN, 'testTag', '%{public}s', 'Ability onWindowStageDestroy');
64.     // 在窗口销毁时需要移除失效的UIContext。
65.     PixelUtils.removeUIContext();
66.   }
67.   // ...
68. }

使用替换的封装接口时，建议在能够获取UIContext的场景下传入UIContext参数。

1. import { hilog } from '@kit.PerformanceAnalysisKit';
2. import { PixelUtils } from '../common/Utils';

3. const DOMAIN = 0x0000;

4. @Entry
5. @Component
6. struct Index {
7.   build() {
8.     RelativeContainer() {
9.       Text('Calculate 20vp to px')
10.         .fontWeight(FontWeight.Bold)
11.         .alignRules({
12.           center: { anchor: '__container__', align: VerticalAlign.Center },
13.           middle: { anchor: '__container__', align: HorizontalAlign.Center }
14.         })
15.         .onClick(() => {
16.           let pxValue = PixelUtils.vp2px(20, this.getUIContext());
17.           hilog.info(DOMAIN, 'testTag', `20vp equals to ${pxValue}px`);
18.         })
19.     }
20.     .height('100%')
21.     .width('100%')
22.   }
23. }

无法获取UIContext时，可考虑直接调用。

1. let pxValue = PixelUtils.vp2px(20);
2. hilog.info(DOMAIN, 'testTag', `20vp equals to ${pxValue}px`);

### 应用存在多窗时，通过最近获焦窗口获取UIContext

当应用有多个窗口且无法直接获取UIContext时，可通过最近获得焦点的窗口获取其UIContext。

说明

1. 该方案将跟踪最近一个获得焦点的窗口，在调用具体功能时，该窗口可能处于失焦状态。
2. 创建窗口时需要调用registerWindowCallback注册回调。

使用UIContext接口替换：

1. // common/WindowUtils.ets
2. import { display, window } from '@kit.ArkUI';
3. import { hilog } from '@kit.PerformanceAnalysisKit';

4. const DOMAIN = 0x0000;

5. export class WindowUIContextUtils {
6.   static activeUIContext : UIContext | undefined;

7.   static registerWindowCallback(windowClass: window.Window) : void {
8.     try {
9.       windowClass.on('windowEvent', (event: window.WindowEventType) => {
10.         if (event === window.WindowEventType.WINDOW_ACTIVE) {
11.           try {
12.             let uiContext = windowClass.getUIContext();
13.             WindowUIContextUtils.activeUIContext = uiContext;
14.           } catch(exception) {
15.             hilog.error(DOMAIN, 'testTag', `Can't get UIContext, ${exception}`);
16.           }
17.         }
18.       });
19.     } catch (exception) {
20.       console.error(`Failed to unregister callback. Cause: ${exception}`);
21.     }
22.   }

23.   static unregisterWindowCallback(windowClass: window.Window): void {
24.     windowClass.off('windowEvent');
25.   }

26.   static setActiveUIContext(uiContext: UIContext) : void {
27.     WindowUIContextUtils.activeUIContext = uiContext;
28.   }

29.   static vp2px(vpValue: number, uiContext?: UIContext): number {
30.     let _uiContext = uiContext??WindowUIContextUtils.activeUIContext;
31.     if (!_uiContext || !_uiContext.isAvailable()) {
32.       let displayClass = display.getDefaultDisplaySync();
33.       let density = displayClass.densityPixels;
34.       return vpValue * density;
35.     }

36.     return _uiContext.vp2px(vpValue);
37.   }
38. }

39. // entryability/EntryAbility.ets
40. import { UIAbility } from '@kit.AbilityKit';
41. import { hilog } from '@kit.PerformanceAnalysisKit';
42. import { window } from '@kit.ArkUI';
43. import { WindowUIContextUtils } from '../common/WindowUtils';

44. const DOMAIN = 0x0000;

45. export default class EntryAbility extends UIAbility {
46.   // ...

47.   onWindowStageCreate(windowStage: window.WindowStage): void {
48.     hilog.info(DOMAIN, 'testTag', '%{public}s', 'Ability onWindowStageCreate');
49.     let window = windowStage.getMainWindowSync();
50.     // 注册主窗的回调。
51.     WindowUIContextUtils.registerWindowCallback(window);
52.     windowStage.loadContent('pages/WindowTestPage', (err) => {
53.       // 需要在loadContent完成后获取UIContext。
54.       if (err.code) {
55.         hilog.error(DOMAIN, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err));
56.         return;
57.       }
58.       try {
59.         let uiContext = window.getUIContext();
60.         // 主窗获焦可能早于loadContent完成，需要在成功后设置保证有效。
61.         WindowUIContextUtils.setActiveUIContext(uiContext)
62.       } catch(exception) {
63.         hilog.error(DOMAIN, 'testTag', 'Failed to getUIContext in loadContent. Cause: %{public}s', JSON.stringify(exception));
64.       }
65.     });
66.   }

67.   onWindowStageWillDestroy(windowStage: window.WindowStage) {
68.     let window = windowStage.getMainWindowSync();
69.     hilog.info(DOMAIN, 'testTag', '%{public}s', `The main window: ${window}`);
70.     // 注销主窗的回调。
71.     WindowUIContextUtils.unregisterWindowCallback(window);
72.   }

73.   // ...
74. }

75. // pages/WindowTestPage.ets
76. import { hilog } from '@kit.PerformanceAnalysisKit';
77. import { window } from '@kit.ArkUI';
78. import { BusinessError } from '@kit.BasicServicesKit';
79. import { WindowUIContextUtils } from '../common/WindowUtils';

80. const DOMAIN = 0x0000;

81. @Entry
82. @Component
83. struct Index {
84.   private subWindow : window.Window | undefined;

85.   build() {
86.     Column() {
87.       Text('Create SubWindow')
88.         .onClick(() => {
89.           let config: window.Configuration = {
90.             name: "test",
91.             windowType: window.WindowType.TYPE_DIALOG,
92.             ctx: this.getUIContext().getHostContext()
93.           };
94.           try {
95.             window.createWindow(config, (err: BusinessError, windowClass: window.Window) => {
96.               const errCode: number = err.code;
97.               if (errCode) {
98.                 hilog.error(DOMAIN, 'testTag', `Failed to create the window. Cause: ${errCode}`);
99.                 return;
100.               }
101.               // 在窗口创建后注册回调。
102.               this.subWindow = windowClass;
103.               try {
104.                 windowClass.setUIContent('pages/Index', () => {
105.                   WindowUIContextUtils.registerWindowCallback(windowClass);
106.                   windowClass.resize(500, 1000);
107.                   windowClass.showWindow();
108.                 });
109.               } catch(exception) {
110.                 hilog.error(DOMAIN, 'testTag', `Failed to setUIContent. Cause : ${exception}`);
111.               }
112.             });
113.           } catch (exception) {
114.             hilog.error(DOMAIN, 'testTag', `Failed to create the window. Cause : ${exception}`);
115.           }
116.         })
117.       Text('Destroy SubWindow')
118.         .onClick(() => {
119.           if (this.subWindow) {
120.             // 在窗口销毁前注销回调。
121.             WindowUIContextUtils.unregisterWindowCallback(this.subWindow);
122.             this.subWindow.destroyWindow();
123.           }
124.         })
125.     }
126.     .height('100%')
127.     .width('100%')
128.   }
129. }

### 执行绑定UI实例的闭包

对于UIContext中没有提供替代的接口（例如CalendarPickerDialog），或者开发者自定义实现的业务行为与多实例相关，需要和实例绑定时（例如，一个代码段），可以使用UIContext对象[runScopedTask](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext#runscopedtask)方法执行闭包。

使用UIContext接口替换：

1. @Entry
2. @Component
3. struct CalendarPickerDialogPage {
4.   private selectedDate: Date = new Date('2025-10-01');

5.   build() {
6.     RelativeContainer() {
7.       Button('Show CalendarPicker Dialog')
8.         .alignRules({
9.           center: { anchor: '__container__', align: VerticalAlign.Center },
10.           middle: { anchor: '__container__', align: HorizontalAlign.Center }
11.         })
12.         .onClick(() => {
13.           let uiContext = this.getUIContext();
14.           uiContext.runScopedTask(() => {
15.             CalendarPickerDialog.show({
16.               selected: this.selectedDate,
17.               backgroundColor: Color.White,
18.               backgroundBlurStyle: BlurStyle.NONE,
19.               shadow: ShadowStyle.OUTER_FLOATING_SM
20.             });
21.           });
22.         })
23.     }
24.     .height('100%')
25.     .width('100%')
26.   }
27. }

## 特殊全局接口替换示例

部分全局接口在替换为UIContext接口时，需要考虑一些特殊的调用场景。

### 像素单位转换接口替换为UIContext接口

因为不同的UI实例可以有不同的转换系数，[像素单位](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-pixel-units)接口计算结果依赖UI实例。其中fp2px/px2fp/lpx2px/px2lpx接口在无有效UI上下文时会返回undefined，而vp2px/px2vp接口在无有效UI上下文时，会获取默认屏幕像素密度进行计算。

|像素单位转换接口调用时机|接口行为|可能与预期不一致的场景|
|:--|:--|:--|
|主窗口创建并调用loadContent或setUIContent前。|没有合适的UI实例。<br><br>px2vp/vp2px使用默认屏幕的density进行换算，返回结果。<br><br>fp2px/px2fp/lpx2px/px2lpx返回undefined。|px2vp/vp2px在多屏场景下可能与预期不一致。如预期以主屏的逻辑像素密度计算结果，实际以扩展屏的像素密度计算结果。|
|在loadContent或setUIContent后，且在UI的回调函数中。|根据UI跟踪的调用域（Scope）找到具体的UI实例，使用该UI实例关联的信息进行计算。|无|
|应用单Ability单窗口的场景，并在loadContent或setUIContent之后，但在非UI的其他异步回调中调用。|无法根据UI跟踪的调用域（Scope）找到具体的UI实例，但根据当前单例场景可以确定唯一UI实例，使用该UI实例关联的信息进行计算。|无|
|多Ability或多窗口的多UI实例场景，在loadContent或setUIContent调用之后，但在其他异步回调中调用。|无法根据UI跟踪的调用域（Scope）找到具体的UI实例，也无法确定唯一实例。接口按照最近获焦、最近前台、最近创建的优先级依次查找匹配的UI实例，并根据UI实例关联的信息进行计算。|多实例场景可能存在作用实例和预期不一致。如预期以主窗所处屏幕的逻辑像素密度计算结果，实际以子窗所处屏幕的像素密度计算结果。|
|所有的窗口销毁，无UI实例后。|没有合适的UI实例。<br><br>px2vp/vp2px使用默认屏幕的density进行换算，返回结果。<br><br>fp2px/px2fp/lpx2px/px2lpx返回undefined。|px2vp/vp2px在多屏场景下可能与预期不一致。如预期以扩展屏的逻辑像素密度计算结果，实际以主屏的像素密度计算结果。|

在实际的开发场景中，全局接口可能在UI实例创建前被调用。此时，在替换vp2px/px2vp时，开发者可以通过[display.getDefaultDisplaySync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-display#displaygetdefaultdisplaysync9)获取当前默认屏幕的逻辑像素密度计算结果；替换fp2px/px2fp/lpx2px/px2lpx接口时，可以直接返回undefined，以保证行为的一致性。

使用全局接口：

1. // Common/UIContext.ets
2. export class PixelUtils {
3.   static vp2px(vpValue: number) : number {
4.     return vp2px(vpValue);
5.   }

6.   static fp2px(fpValue: number) : number | undefined {
7.     return fp2px(fpValue);
8.   }

9.   static lpx2px(lpxValue: number) : number | undefined {
10.     return lpx2px(lpxValue);
11.   }
12. }

使用UIContext接口替换：

1. import { hilog } from '@kit.PerformanceAnalysisKit';
2. import { display } from '@kit.ArkUI';

3. const DOMAIN = 0x0000;

4. export class PixelUtils {
5.   static uiContext : UIContext | undefined;
6.   static setUIContext(uiContext : UIContext) : void {
7.     PixelUtils.uiContext = uiContext;
8.   }

9.   static removeUIContext(): void {
10.     PixelUtils.uiContext = undefined;
11.   }

12.  static vp2px(vpValue: number, uiContext?: UIContext): number | undefined {
13.    let _uiContext = uiContext??PixelUtils.uiContext;
14.     if (!_uiContext || !_uiContext.isAvailable()) {
15.       let displayClass = display.getDefaultDisplaySync();
16.       let density = displayClass.densityPixels;
17.       return vpValue * density;
18.     }
19.     return _uiContext.vp2px(vpValue)
20.   }

21.   static fp2px(fpValue: number, uiContext?: UIContext): number | undefined {
22.     let _uiContext = uiContext??PixelUtils.uiContext;
23.     if (!_uiContext || !_uiContext.isAvailable()) {
24.       hilog.error(DOMAIN, 'testTag', `Can't get UIContext`);
25.       return undefined;
26.     }
27.     return _uiContext.fp2px(fpValue)
28.   }

29.   lpx2px(lpxValue: number, uiContext?: UIContext): number | undefined {
30.     let _uiContext = uiContext??PixelUtils.uiContext;
31.     if (!_uiContext || !_uiContext.isAvailable()) {
32.       hilog.error(DOMAIN, 'testTag', `Can't get UIContext`);
33.       return undefined;
34.     }
35.     return _uiContext.lpx2px(lpxValue)
36.   }
37. }

### 获取Ability的Context

[getContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-getcontext)接口用于在UI页面中获取对应UI实例所属Ability的Context，因此依赖于UI实例。

|getContext接口的调用时机|接口行为|可能与预期不一致的场景|
|:--|:--|:--|
|主窗口创建并调用loadContent或setUIContent前。|没有合适的UI实例，返回undefined。|无|
|主窗口创建并调用loadContent或setUIContent后，且传入自定义组件对象。|跟踪自定义组件所属的UI实例，返回该UI实例所属Ability的Context。|无|
|在loadContent或setUIContent后，且在UI的回调函数中。|根据UI跟踪的调用域（Scope）找到具体的UI实例，返回该UI实例所属Ability的Context。|无|
|应用单Ability单窗口的场景，并在loadContent或setUIContent之后，但在非UI的其他异步回调中调用且未传入自定义组件对象。|无法根据UI跟踪的调用域（Scope）找到具体的UI实例，但根据当前单例场景可以确定唯一UI实例，返回该UI实例所属Ability的Context。|无|
|多Ability或多窗口的多UI实例场景，在loadContent或setUIContent调用之后，但在其他异步回调中调用且未传入自定义组件对象。|无法根据UI跟踪的调用域(Scope)找到具体的UI实例，也无法确定唯一实例。接口按照最近获焦、最近前台、最近创建的优先级依次查找匹配的UI实例，返回该UI实例所属Ability的Context。|多实例场景可能与预期不一致。如存在两个Ability时，预期返回第一个创建的Ability的Context，实际返回第二个创建的Ability的Context。|
|所有的窗口销毁，无UI实例后。|没有合适的UI实例，返回undefined。|无|

在单Ability场景中，建议直接获取Ability的context属性。

使用全局接口：

1. // Common/ContextUtils.ets
2. import { hilog } from '@kit.PerformanceAnalysisKit';

3. const DOMAIN = 0x0000;

4. @Entry
5. @Component
6. struct GetContextPage {
7.   @State message: string = 'Hello World';

8.   build() {
9.     RelativeContainer() {
10.       Text(this.message)
11.         .fontWeight(FontWeight.Bold)
12.         .alignRules({
13.           center: { anchor: '__container__', align: VerticalAlign.Center },
14.           middle: { anchor: '__container__', align: HorizontalAlign.Center }
15.         })
16.         .onClick(() => {
17.           // 需要确保传入的是自定义组件对象。
18.           let context = getContext(this);
19.           hilog.info(DOMAIN, 'testTag', `The context is ${context}`);
20.         })
21.     }
22.     .height('100%')
23.     .width('100%')
24.   }
25. }

使用UIContext接口替换：

1. // common/ContextUtils.ets
2. export class ContextUtils {
3.   static context: Context | undefined;

4.   static setContext(context: Context): void {
5.     ContextUtils.context = context;
6.   }

7.   static removeContext(): void {
8.     ContextUtils.context = undefined;
9.   }

10.   static getContext(uiContext?: UIContext): Context | undefined {
11.     if (uiContext) {
12.       return uiContext.getHostContext();
13.     }

14.     return ContextUtils.context;
15.   }
16. }

接口的默认返回值设置为Ability的成员属性context。

1. // entryAbility/EntryAbility.ets
2. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';
4. import { ContextUtils } from '../common/ContextUtils';

5. const DOMAIN = 0x0000;

6. export default class EntryAbility extends UIAbility {
7.   onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
8.     hilog.info(DOMAIN, 'testTag', '%{public}s', 'Ability onCreate');
9.     ContextUtils.setContext(this.context);
10.   }

11.   onDestroy(): void {
12.     hilog.info(DOMAIN, 'testTag', '%{public}s', 'Ability onDestroy');
13.     ContextUtils.removeContext();
14.   }

15.   // ...
16. }

在UI界面中，建议传入UIContext，以保证符合预期或直接调用getHostContext。

1. import { ContextUtils } from '../common/ContextUtils';
2. import { hilog } from '@kit.PerformanceAnalysisKit';

3. const DOMAIN = 0x0000;

4. @Entry
5. @Component
6. struct ContextPage {
7.   build() {
8.     Column() {
9.       Text('getContext')
10.         .onClick(() => {
11.           let context = ContextUtils.getContext(this.getUIContext());
12.           hilog.info(DOMAIN, 'testTag', `The context is ${context}`);
13.         })
14.     }
15.     .height('100%')
16.     .width('100%')
17.   }
18. }

无UI场景直接返回窗口创建时设置的默认返回值。

1. let context = ContextUtils.getContext();
2. hilog.info(DOMAIN, 'testTag', `The context is ${context}`);

### LocalStorage替换为UIContext的接口

LocalStorage是页面级的UI状态存储，通过@Entry装饰器接收的参数可以在页面内共享同一个LocalStorage实例。使用全局接口时，开发者使用[getShared](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-state-management#getshareddeprecated)向@Entry装饰器传递LocalStorage对象。使用UIContext接口后，无法直接获取UIContext对象，可以将[EntryOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-entry#entryoptions10)的useSharedStorage参数设置为true，以使用共享的LocalStorage实例对象。

使用全局接口：

1. // pages/LocalStoragePage
2. @Entry({storage: LocalStorage.getShared()})
3. @Component
4. struct LocalStoragePage {
5.   @LocalStorageLink('message') message: string = 'Hello World';

6.   build() {
7.     RelativeContainer() {
8.       Text(this.message)
9.         .id('LocalStoragePageHelloWorld')
10.         .fontWeight(FontWeight.Bold)
11.         .alignRules({
12.           center: { anchor: '__container__', align: VerticalAlign.Center },
13.           middle: { anchor: '__container__', align: HorizontalAlign.Center }
14.         })
15.         .onClick(() => {
16.           let storage = LocalStorage.getShared();
17.           if (storage) {
18.             storage.setOrCreate('message', 'onClick is called.')
19.           }
20.         })
21.     }
22.     .height('100%')
23.     .width('100%')
24.   }
25. }

使用UIContext接口替换：

1. // pages/LocalStoragePage
2. @Entry({useSharedStorage: true})
3. @Component
4. struct LocalStoragePage {
5.   @LocalStorageLink('message') message: string = 'Hello World';

6.   build() {
7.     RelativeContainer() {
8.       Text(this.message)
9.         .id('LocalStoragePageHelloWorld')
10.         .fontWeight(FontWeight.Bold)
11.         .alignRules({
12.           center: { anchor: '__container__', align: VerticalAlign.Center },
13.           middle: { anchor: '__container__', align: HorizontalAlign.Center }
14.         })
15.         .onClick(() => {
16.           let uiContext = this.getUIContext();
17.           let storage = uiContext.getSharedLocalStorage();
18.           if (storage) {
19.             storage.setOrCreate('message', 'onClick is called.')
20.           }
21.         })
22.     }
23.     .height('100%')
24.     .width('100%')
25.   }
26. }

使用共享的LocalStorage对象需要在loadContent时传入LocalStorage，详细可参考[LocalStorage：页面级UI状态存储](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-localstorage)。

1. import { AbilityConstant, UIAbility } from '@kit.AbilityKit';
2. import { hilog } from '@kit.PerformanceAnalysisKit';
3. import { window } from '@kit.ArkUI';

4. const DOMAIN = 0x0000;

5. export default class EntryAbility extends UIAbility {
6.   // ...

7.   onWindowStageCreate(windowStage: window.WindowStage): void {
8.     hilog.info(DOMAIN, 'testTag', '%{public}s', 'Ability onWindowStageCreate');
9.     let localStorage = new LocalStorage();
10.     localStorage.setOrCreate('message', 'Message from Storage')
11.     windowStage.loadContent('pages/LocalStoragePage', localStorage, (err) => {
12.       if (err.code) {
13.         hilog.error(DOMAIN, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err));
14.         return;
15.       }
16.       hilog.info(DOMAIN, 'testTag', `loadContent success.`);
17.     });
18.   }

19.   // ...
20. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-ui-system-scenarization-capability "UI系统场景化能力")
# 使用组件截图（ComponentSnapshot）

更新时间: 2025-12-16 16:39

## 能力介绍

组件截图是将应用内一个组件节点树的渲染结果生成位图（[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)）的能力，支持两种方式：一种是对已挂树显示的组件进行截图，另一种是对通过Builder或ComponentContent实现的离线组件进行截图。

说明

组件截图依赖UI上下文，需要在具备明确上下文的环境中调用，因此请优先使用UIContext的getComponentSnapshot接口返回的[ComponentSnapshot](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-componentsnapshot)对象的接口，不建议直接使用从@kit.ArkUI导入的componentSnapshot接口。

### 对挂树组件截图

对已明确挂树的组件进行截图，可通过[get](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-componentsnapshot#get12-1)或[getSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-componentsnapshot#getsync12)实现，传入组件标识（需提前通过.id通用属性配置）以指定组件根节点。系统在通过指定的ID查找待截图组件时，仅遍历已挂树的组件，不对cache或离屏组件进行查找。系统以首个查找到的结果为准，故应用需**确保组件标识ID的唯一性**。

从API version 15开始，在已知组件的[getUniqueId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-framenode#getuniqueid12)的情况下，也可以使用[getWithUniqueId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-componentsnapshot#getwithuniqueid15)或[getSyncWithUniqueId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-componentsnapshot#getsyncwithuniqueid15)接口来实现截图，这可以省去查找组件的过程。

截图仅能获取最近一帧的绘制内容。若在组件触发更新的同时调用截图，更新的渲染内容不会被截取，截图将返回前一帧的绘制内容。

说明

尽量避免在使用截图时触发待截图组件的刷新，防止对截图内容的干扰。

### 对离线组件截图

离线组件是指通过Builder或ComponentContent封装的、尚未挂载到树上的组件，可以使用[createFromBuilder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-componentsnapshot#createfrombuilder12-1)来实现。从API version 18开始，也可以使用[createFromComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-componentsnapshot#createfromcomponent18)实现离线组件截图。

这些组件不参与真实渲染，因此对其截图需要更长的时间，因为系统必须先进行离线构建、布局及资源加载等操作，在这些操作完成前执行的截图所获位图不符合预期。因此，通常需要通过设置delay参数指定足够的时间，确保系统能够完成这些操作。对于图片资源的加载，建议将图片组件的[syncLoad](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-image#syncload8)属性设为 true，以强制同步加载，确保离线组件构建时图片已加载、下载及解码完成，从而确保截图过程中能够正确呈现图片像素。

## 典型使用场景

以下通过几个典型场景来说明组件截图能力的常见使用方式。

### 截取长内容（滚动截图）

较长内容通常使用滚动类容器组件实现。截图时，仅能捕获容器内可见内容，超出边界部分无法截取。若使用LazyForEach或Repeat，超出显示范围内容亦不会被系统构建及截取。

可利用滚动类容器接口，模拟用户滑动逐页截图，之后按偏移量拼接各页PixelMap位图，以生成完整长图。关键点在于模拟滑动、维护位移与位图关系及实现PixelMap位图读写。

**步骤1：添加滚动控制器及事件监听**

为了能够模拟滚动，以及监听组件滚动的具体offset，需要为List（此处以列表为例）组件添加滚动控制器以及滚动监听。

1. // src/main/ets/view/ScrollSnapshot.ets
2. @Component
3. export struct ScrollSnapshot {
4.   private scroller: Scroller = new Scroller();
5.   private listComponentWidth: number = 0;
6.   private listComponentHeight: number = 0;
7.   // list组件的当前偏移量
8.   private curYOffset: number = 0;
9.   // 每次滚动距离
10.   private scrollHeight: number = 0;

11.   // ...
12.   build() {
13.     // ...
14.     Stack() {
15.       // ...
16.       // 1.1 绑定滚动控制器，并通过`.id`配置组件唯一标识。
17.       List({
18.         scroller: this.scroller
19.       })// ...
20.         .id(LIST_ID)
21.           // 1.2 通过回调获取滚动偏移量。
22.         .onDidScroll(() => {
23.           this.curYOffset = this.scroller.currentOffset().yOffset;
24.         })
25.         .onAreaChange((oldValue, newValue) => {
26.           // 1.3 获取组件的宽高。
27.           this.listComponentWidth = newValue.width as number;
28.           this.listComponentHeight = newValue.height as number;
29.         })
30.     }
31.   }
32. }

**步骤2：循环滚动截图并缓存**

通过实现一个递归方法滚动循环截图，并在滚动过程配合一些动效实现。

1.   /**
2.    * 递归滚动截图，直到滚动到底，最后合并所有截图
3.    */
4.   async scrollSnapAndMerge() {
5.     // 记录滚动偏移
6.     this.scrollYOffsets.push(this.curYOffset - this.yOffsetBefore);
7.     // 调用组件截图接口，获取list组件的截图
8.     const pixelMap = await this.getUIContext().getComponentSnapshot().get(LIST_ID);
9.     // 获取位图像素字节，并保存在数组中
10.     let area: image.PositionArea =
11.       await this.getSnapshotArea(pixelMap, this.scrollYOffsets, this.listComponentWidth, this.listComponentHeight)
12.     this.areaArray.push(area);

13.     // 判断是否滚动到底以及用户是否已经强制停止
14.     if (!this.scroller.isAtEnd() && !this.isClickStop) {
15.       // 如果没有到底或被停止，则播放一个滚动动效，延迟一段时间后，继续递归截图
16.       CommonUtils.scrollAnimation(this.scroller, 1000, this.scrollHeight);
17.       await CommonUtils.sleep(1500);
18.       await this.scrollSnapAndMerge();
19.     } else {
20.       // 当滚动到底时，调用`mergeImage`将所有保存的位图数据进行拼接，返回长截图位图对象
21.       this.mergedImage =
22.         await this.mergeImage(this.areaArray, this.scrollYOffsets[this.scrollYOffsets.length - 1],
23.           this.listComponentWidth, this.listComponentHeight);
24.     }
25.   }

26. // src/main/ets/common/CommonUtils.ets
27. static scrollAnimation(scroller: Scroller, duration: number, scrollHeight: number): void {
28.   scroller.scrollTo({
29.     xOffset: 0,
30.     yOffset: (scroller.currentOffset().yOffset + scrollHeight),
31.     animation: {
32.       duration: duration,
33.       curve: Curve.Smooth,
34.       canOverScroll: false
35.     }
36.   });
37. }

**步骤3：拼接长截图**

使用image.createPixelMapSync()方法创建长截图longPixelMap，并遍历之前保存的图像片段数据（this.areaArray），构建image.PositionArea对象area，然后调用longPixelMap.writePixelsSync(area)方法将这些片段逐个写入到正确的位置，从而拼接成一个完整的长截图。

1. async mergeImage(areaArray: image.PositionArea[], lastOffsetY: number, listWidth: number,
2.   listHeight: number): Promise<PixelMap> {
3.   // 创建一个长截图位图对象
4.   let opts: image.InitializationOptions = {
5.     editable: true,
6.     pixelFormat: 4,
7.     size: {
8.       width: this.getUIContext().vp2px(listWidth),
9.       height: this.getUIContext().vp2px(lastOffsetY + listHeight)
10.     }
11.   };
12.   let longPixelMap = image.createPixelMapSync(opts);
13.   let imgPosition: number = 0;

14.   for (let i = 0; i < areaArray.length; i++) {
15.     let readArea = areaArray[i];
16.     let area: image.PositionArea = {
17.       pixels: readArea.pixels,
18.       offset: 0,
19.       stride: readArea.stride,
20.       region: {
21.         size: {
22.           width: readArea.region.size.width,
23.           height: readArea.region.size.height
24.         },
25.         x: 0,
26.         y: imgPosition
27.       }
28.     }
29.     imgPosition += readArea.region.size.height;
30.     longPixelMap.writePixelsSync(area);
31.   }
32.   return longPixelMap;
33. }

**步骤4：保存截图**

使用安全控件SaveButton实现截图保存到相册。

1. // src/main/ets/view/SnapshotPreview.ets
2. SaveButton({
3.   icon: SaveIconStyle.FULL_FILLED,
4.   text: SaveDescription.SAVE_IMAGE,
5.   buttonType: ButtonType.Capsule
6. })
7.   .onClick((event, result) => {
8.     this.saveSnapshot(result);
9.   })

10. async saveSnapshot(result: SaveButtonOnClickResult): Promise<void> {
11.   if (result === SaveButtonOnClickResult.SUCCESS) {
12.     const helper = photoAccessHelper.getPhotoAccessHelper(this.context);
13.     const uri = await helper.createAsset(photoAccessHelper.PhotoType.IMAGE, 'png');
14.     const file = await fileIo.open(uri, fileIo.OpenMode.READ_WRITE | fileIo.OpenMode.CREATE);
15.     const imagePackerApi: image.ImagePacker = image.createImagePacker();
16.     const packOpts: image.PackingOption = {
17.       format: 'image/png',
18.       quality: 100,
19.     };
20.     imagePackerApi.packing(this.mergedImage, packOpts).then((data) => {
21.       fileIo.writeSync(file.fd, data);
22.       fileIo.closeSync(file.fd);
23.       Logger.info(TAG, `Succeeded in packToFile`);
24.       promptAction.showToast({
25.         message: $r('app.string.save_album_success'),
26.         duration: 1800
27.       })
28.     }).catch((error: BusinessError) => {
29.       Logger.error(TAG, `Failed to packToFile. Error code is ${error.code}, message is ${error.message}`);
30.     });
31.   }
32.   // ...
33. }

**步骤5：保存完成后释放位图**

当位图对象不再使用时，应及时将其赋值为空，例如：this.mergedImage = undefined;。

1.   closeSnapPopup(): void {
2.     // 关闭弹窗
3.     this.isShowPreview = false;
4.     // 释放位图对象
5.     this.mergedImage = undefined;
6.     // 重置相关参数
7.     this.snapPopupWidth = 100;
8.     this.snapPopupHeight = 200;
9.     this.snapPopupPosition =
10.       PopupUtils.calcPopupCenter(this.screenWidth, this.screenHeight, this.snapPopupWidth, this.snapPopupHeight);
11.     this.isLargePreview = false;
12.   }

### 封装全局截图接口

如前文所述，截图接口必须在UI上下文明确的位置使用。然而，应用有时希望对不同模块封装统一的全局截图方法。例如，在下述示例中，awardBuilder构建的组件是固定结构的。GlobalStaticSnapshot提供了一个getAwardSnapshot全局方法，能够满足不同模块的需求，对同一固定模式的组件进行截图，从而实现全局截图接口的封装。本示例从API version 18开始支持。

1. import { image } from '@kit.ImageKit';
2. import { ComponentContent } from '@kit.ArkUI';

3. export class Params {
4.   text: string | undefined | null = "";

5.   constructor(text: string | undefined | null) {
6.     this.text = text;
7.   }
8. }

9. @Builder
10. function awardBuilder(params: Params) {
11.   Column() {
12.     Text(params.text)
13.       .fontSize(90)
14.       .fontWeight(FontWeight.Bold)
15.       .margin({ bottom: 36 })
16.       .width('100%')
17.       .height('100%')
18.   }.backgroundColor('#FFF0F0F0')
19. }

20. export class GlobalStaticSnapshot {
21.   /**
22.    * 一个可以获取固定对象截图的静态方法
23.    */
24.   static getAwardSnapshot(uiContext: UIContext, textParam: Params): image.PixelMap | undefined {
25.     let resultPixmap: image.PixelMap | undefined = undefined
26.     let contentNode = new ComponentContent(uiContext, wrapBuilder(awardBuilder), textParam);
27.     uiContext.getComponentSnapshot()
28.       .createFromComponent(contentNode, 320, true, { scale: 1, waitUntilRenderFinished: true })
29.       .then((pixmap: image.PixelMap) => {
30.         resultPixmap = pixmap
31.       })
32.       .catch((err: Error) => {
33.         console.error("error: " + err)
34.       })
35.     return resultPixmap;
36.   }
37. }

**完整示例：**

完整示例请参考[长截图](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-long-snapshot-practice#section1566681910427)。

## 组件截图最佳实践

### 合理控制截图时机

在实现截图功能时，需注意组件的渲染过程非一次性完成。系统在构建与显示组件时，将经过测量、布局、提交指令等多个复杂步骤，最终在一次硬件刷新时呈现于屏幕上。因此，在特定情况下，若在组件刷新后立即调用截图，可能无法获取预期内容或出现截图失败报错。

为了确保截图结果准确，建议在组件完全渲染后再执行截图操作。

**了解组件的绘制状态**

为了确保截图内容符合预期，应该了解代码对界面状态的修改时机，并注意给系统预留处理时间，这通常可以通过增加一定延时来实现。

尽管可以通过inspector上的[ComponentObserver](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-inspector#componentobserver)感知应用组件绘制（draw）送显通知，但需要注意的是，ComponentObserver的组件绘制通知并不意味着系统已经真正将绘制指令执行，这取决于图形系统服务的负载情况。

**明确等待绘制完成**

影响截图预期的主要因素是截图时机与系统服务执行绘制指令的时间差。在发起截图调用时，应用侧之前提交的所有绘制指令可能尚未被图形服务真正执行。为此，可以通过指定[SnapshotOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-componentsnapshot#snapshotoptions12)参数中的waitUntilRenderFinished为true，来确保系统在执行截图请求时等待所有之前的绘制指令均执行完毕，从而截取到更完整的内容。

说明

建议始终开启waitUntilRenderFinished参数。

**了解资源加载对截图的影响**

影响截图预期的另一个常见原因，是图片资源的加载。图片组件支持在线资源链接，也可指定本地资源，且绝大多数图片资源为PNG、JPEG等压缩格式。这些资源需要系统解码为可提交绘制的位图格式，此过程默认在异步IO线程上进行，因此可能由于该过程耗时的不确定性而导致截图不符合预期。

应用可通过以下几种方式进行优化：

1. 自行提前解析图片为PixelMap格式，将PixelMap配置给图片组件；建议优先以此方法进行优化。
2. 配置所使用的图片组件的syncload属性为true来强制同步加载，这样组件被构建时，即可确保资源可以直接被提交；
3. 通过指定延迟时长以及checkImageStatus设置为true，尝试截图，当返回160001错误后，重新加大时长进行截图；

### 及时保存和释放位图对象

为了及时释放资源，当截图接口返回的PixelMap对象不再使用时，应将其赋值为空。

### 合理控制采样精度

请不要截取过大尺寸的图片，截图不建议超过屏幕尺寸大小。当要截取的图片目标长宽超过底层限制时，截图会返回失败，不同设备的底层限制并不相同。可以通过控制SnapshotOptions中的scale参数，减小采样精度，这可以在很大程度上节省内存，并大幅度提高截图的效率。

### 使用其他能力对自渲染场景实现截图

尽管截图只需传入一个组件根节点即可实现对其下所有组件进行截图，但当子组件中存在[Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video)、[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent)或[Web](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)组件时，这并不是推荐的截图方式。建议直接使用[image.createPixelMapFromSurface](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-f#imagecreatepixelmapfromsurface11)接口来实现。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-global-interface "使用UI上下文接口操作界面（UIContext）")
# 检查页面布局

更新时间: 2025-12-16 16:39

inspector用于检查页面布局，通过双向定位功能帮助开发者在DevEco Studio中快速定位组件、修改属性和调试组件，以提高开发效率。

ArkUI获取当前显示页面中所有组件的信息，包括组件树的父子结构、尺寸、位置、样式、属性和状态。获取组件树信息后，生成并展示为Inspector组件树。DevEco Studio的使用具体可以参考[Inspector调试能力](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-inspector-profiler#inspector%E8%B0%83%E8%AF%95%E8%83%BD%E5%8A%9B)。

inspector针对UI组件的布局或绘制送显完成，还提供了注册与取消监听函数的C API接口，具体使用可以参考[监听组件布局和绘制送显事件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ndk-inspector-component-observer)。

## 使用约束

1. 不支持动效类组件的控件树实时刷新功能。
    
2. 支持获取组件的属性和样式，但不支持获取controller和Builder对象。
    
3. 不支持获取组件的方法、事件。
    

## UIContext查询组件树和组件信息能力

ArkUI提供@ohos.arkui.UIContext(UIContext)扩展能力，通过[getFilteredInspectorTree](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext#getfilteredinspectortree12)获取组件树及组件属性，通过[getFilteredInspectorTreeById](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext#getfilteredinspectortreebyid12)获取指定的组件及其子组件的属性。支持设置过滤条件进行查询。

下述示例，展示了getFilteredInspectorTree和getFilteredInspectorTreeById的基本用法。

1. import { UIContext } from '@kit.ArkUI';

2. @Entry
3. @Component
4. struct ComponentPage {
5.   loopConsole(inspectorStr: string, i: string) {
6.     console.info(`InsTree ${i}| type: ${JSON.parse(inspectorStr).$type}, ID: ${JSON.parse(inspectorStr).$ID}`);
7.     if (JSON.parse(inspectorStr).$children) {
8.       i += '-';
9.       for (let index = 0; index < JSON.parse(inspectorStr).$children.length; index++) {
10.         this.loopConsole(JSON.stringify(JSON.parse(inspectorStr).$children[index]), i);
11.       }
12.     }
13.   }

14.   build() {
15.     Column() {
16.       Text("Hello World")
17.         .fontSize(20)
18.         .id("TEXT")
19.       Button('content').onClick(() => {
20.         const uiContext: UIContext = this.getUIContext();
21.         let inspectorStr = uiContext.getFilteredInspectorTree(['content']);
22.         console.info(`InsTree : ${inspectorStr}`);
23.         inspectorStr = JSON.stringify(JSON.parse(inspectorStr));
24.         this.loopConsole(inspectorStr, '-');
25.       })
26.       Button('isLayoutInspector').onClick(() => {
27.         const uiContext: UIContext = this.getUIContext();
28.         let inspectorStr = uiContext.getFilteredInspectorTree(['isLayoutInspector']);
29.         console.info(`InsTree : ${inspectorStr}`);
30.         inspectorStr = JSON.stringify(JSON.parse(inspectorStr).content);
31.         this.loopConsole(inspectorStr, '-');
32.       })
33.       Button('getFilteredInspectorTreeById').onClick(() => {
34.         const uiContext: UIContext = this.getUIContext();
35.         try {
36.           let inspectorStr = uiContext.getFilteredInspectorTreeById('TEXT', 1, ["id", "src"]);
37.           console.info(`result1: ${inspectorStr}`);
38.           inspectorStr = JSON.stringify(JSON.parse(inspectorStr)['$children'][0]);
39.           console.info(`result2: ${inspectorStr}`);
40.           inspectorStr = uiContext.getFilteredInspectorTreeById('TEXT', 1, ["src"]);
41.           inspectorStr = JSON.stringify(JSON.parse(inspectorStr)['$children'][0]);
42.           console.info(`result3: ${inspectorStr}`);
43.         } catch(e) {
44.           console.error(`getFilteredInspectorTreeById error: ${e}`);
45.         }
46.       })

47.     }
48.     .width('100%')
49.     .height('100%')
50.   }
51. }

## 布局回调

通过[@ohos.arkui.arkui.inspector(布局回调)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-inspector)提供注册组件布局和组件绘制完成的回调通知能力。

下述示例，展示了布局回调的基本用法。

1. import { inspector } from '@kit.ArkUI'

2. @Entry
3. @Component
4. struct ImageExample {
5.   build() {
6.     Column() {
7.       Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Start }) {
8.         Row({ space: 5 }) {
9.           // 可以替换成本地存在的图片
10.           Image($r('app.media.startIcon'))
11.             .width(110)
12.             .height(110)
13.             .border({ width: 1 })
14.             .id('IMAGE_ID')
15.         }
16.       }
17.     }.height(320).width(360).padding({ right: 10, top: 10 })
18.   }

19.   listener:inspector.ComponentObserver = this.getUIContext().getUIInspector().createComponentObserver('IMAGE_ID')

20.   aboutToAppear() {
21.     let onLayoutComplete:()=>void=():void=>{
22.       // 补充待实现的功能
23.     }
24.     let onDrawComplete:()=>void=():void=>{
25.       // 补充待实现的功能
26.     }
27.     let onDrawChildrenComplete:()=>void=():void=>{
28.       // 补充待实现的功能
29.     }
30.     let FuncLayout = onLayoutComplete // 绑定当前js对象
31.     let FuncDraw = onDrawComplete // 绑定当前js对象
32.     let FuncDrawChildren = onDrawChildrenComplete // 绑定当前js对象
33.     let OffFuncLayout = onLayoutComplete // 绑定当前js对象
34.     let OffFuncDraw = onDrawComplete // 绑定当前js对象
35.     let OffFuncDrawChildren = onDrawChildrenComplete // 绑定当前js对象

36.     this.listener.on('layout', FuncLayout)
37.     this.listener.on('draw', FuncDraw)
38.     this.listener.on('drawChildren', FuncDrawChildren)

39.     // 通过句柄向对应的查询条件取消注册回调，由开发者自行决定在何时调用。
40.     // this.listener.off('layout', OffFuncLayout)
41.     // this.listener.off('draw', OffFuncDraw)
42.     // this.listener.off('drawChildren', OffFuncDrawChildren)
43.   }
44. }

## 组件标识属性的扩展能力

通过getInspectorByKey、getInspectorTree、sendEventByKey提供组件标识属性扩展能力，具体如下：

- [getInspectorByKey](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-component-id#getinspectorbykey9)，获取指定id的组件的所有属性。
- [getInspectorTree](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-component-id#getinspectortree9)，获取组件树及组件属性。
- [sendEventByKey](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-component-id#sendeventbykey9)，给指定id的组件发送事件。

下述示例，展示了getInspectorByKey、getInspectorTree和sendEventByKey的基本用法。

1. @Entry
2. @Component
3. struct ComponentPage {
4.   build() {
5.     Column() {
6.       Text("Hello World")
7.         .fontSize(20)
8.         .id("TEXT")
9.         .onClick(() => {
10.           console.info(`Text is clicked`);
11.         })
12.       Button('getInspectorByKey').onClick(() => {
13.         let result = getInspectorByKey("TEXT");
14.         console.info(`result is ${result}`);
15.       })
16.       Button('getInspectorTree').onClick(() => {
17.         let result = getInspectorTree();
18.         console.info(`result is ${JSON.stringify(result)}`);
19.       })
20.       Button('sendEventByKey').onClick(() => {
21.         sendEventByKey("TEXT", 10, "");
22.       })
23.     }
24.     .width('100%')
25.     .height('100%')
26.   }
27. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-manage-components-visibility "感知组件可见性")
# 检查页面布局

更新时间: 2025-12-16 16:39

inspector用于检查页面布局，通过双向定位功能帮助开发者在DevEco Studio中快速定位组件、修改属性和调试组件，以提高开发效率。

ArkUI获取当前显示页面中所有组件的信息，包括组件树的父子结构、尺寸、位置、样式、属性和状态。获取组件树信息后，生成并展示为Inspector组件树。DevEco Studio的使用具体可以参考[Inspector调试能力](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-inspector-profiler#inspector%E8%B0%83%E8%AF%95%E8%83%BD%E5%8A%9B)。

inspector针对UI组件的布局或绘制送显完成，还提供了注册与取消监听函数的C API接口，具体使用可以参考[监听组件布局和绘制送显事件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ndk-inspector-component-observer)。

## 使用约束

1. 不支持动效类组件的控件树实时刷新功能。
    
2. 支持获取组件的属性和样式，但不支持获取controller和Builder对象。
    
3. 不支持获取组件的方法、事件。
    

## UIContext查询组件树和组件信息能力

ArkUI提供@ohos.arkui.UIContext(UIContext)扩展能力，通过[getFilteredInspectorTree](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext#getfilteredinspectortree12)获取组件树及组件属性，通过[getFilteredInspectorTreeById](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext#getfilteredinspectortreebyid12)获取指定的组件及其子组件的属性。支持设置过滤条件进行查询。

下述示例，展示了getFilteredInspectorTree和getFilteredInspectorTreeById的基本用法。

1. import { UIContext } from '@kit.ArkUI';

2. @Entry
3. @Component
4. struct ComponentPage {
5.   loopConsole(inspectorStr: string, i: string) {
6.     console.info(`InsTree ${i}| type: ${JSON.parse(inspectorStr).$type}, ID: ${JSON.parse(inspectorStr).$ID}`);
7.     if (JSON.parse(inspectorStr).$children) {
8.       i += '-';
9.       for (let index = 0; index < JSON.parse(inspectorStr).$children.length; index++) {
10.         this.loopConsole(JSON.stringify(JSON.parse(inspectorStr).$children[index]), i);
11.       }
12.     }
13.   }

14.   build() {
15.     Column() {
16.       Text("Hello World")
17.         .fontSize(20)
18.         .id("TEXT")
19.       Button('content').onClick(() => {
20.         const uiContext: UIContext = this.getUIContext();
21.         let inspectorStr = uiContext.getFilteredInspectorTree(['content']);
22.         console.info(`InsTree : ${inspectorStr}`);
23.         inspectorStr = JSON.stringify(JSON.parse(inspectorStr));
24.         this.loopConsole(inspectorStr, '-');
25.       })
26.       Button('isLayoutInspector').onClick(() => {
27.         const uiContext: UIContext = this.getUIContext();
28.         let inspectorStr = uiContext.getFilteredInspectorTree(['isLayoutInspector']);
29.         console.info(`InsTree : ${inspectorStr}`);
30.         inspectorStr = JSON.stringify(JSON.parse(inspectorStr).content);
31.         this.loopConsole(inspectorStr, '-');
32.       })
33.       Button('getFilteredInspectorTreeById').onClick(() => {
34.         const uiContext: UIContext = this.getUIContext();
35.         try {
36.           let inspectorStr = uiContext.getFilteredInspectorTreeById('TEXT', 1, ["id", "src"]);
37.           console.info(`result1: ${inspectorStr}`);
38.           inspectorStr = JSON.stringify(JSON.parse(inspectorStr)['$children'][0]);
39.           console.info(`result2: ${inspectorStr}`);
40.           inspectorStr = uiContext.getFilteredInspectorTreeById('TEXT', 1, ["src"]);
41.           inspectorStr = JSON.stringify(JSON.parse(inspectorStr)['$children'][0]);
42.           console.info(`result3: ${inspectorStr}`);
43.         } catch(e) {
44.           console.error(`getFilteredInspectorTreeById error: ${e}`);
45.         }
46.       })

47.     }
48.     .width('100%')
49.     .height('100%')
50.   }
51. }

## 布局回调

通过[@ohos.arkui.arkui.inspector(布局回调)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-inspector)提供注册组件布局和组件绘制完成的回调通知能力。

下述示例，展示了布局回调的基本用法。

1. import { inspector } from '@kit.ArkUI'

2. @Entry
3. @Component
4. struct ImageExample {
5.   build() {
6.     Column() {
7.       Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Start }) {
8.         Row({ space: 5 }) {
9.           // 可以替换成本地存在的图片
10.           Image($r('app.media.startIcon'))
11.             .width(110)
12.             .height(110)
13.             .border({ width: 1 })
14.             .id('IMAGE_ID')
15.         }
16.       }
17.     }.height(320).width(360).padding({ right: 10, top: 10 })
18.   }

19.   listener:inspector.ComponentObserver = this.getUIContext().getUIInspector().createComponentObserver('IMAGE_ID')

20.   aboutToAppear() {
21.     let onLayoutComplete:()=>void=():void=>{
22.       // 补充待实现的功能
23.     }
24.     let onDrawComplete:()=>void=():void=>{
25.       // 补充待实现的功能
26.     }
27.     let onDrawChildrenComplete:()=>void=():void=>{
28.       // 补充待实现的功能
29.     }
30.     let FuncLayout = onLayoutComplete // 绑定当前js对象
31.     let FuncDraw = onDrawComplete // 绑定当前js对象
32.     let FuncDrawChildren = onDrawChildrenComplete // 绑定当前js对象
33.     let OffFuncLayout = onLayoutComplete // 绑定当前js对象
34.     let OffFuncDraw = onDrawComplete // 绑定当前js对象
35.     let OffFuncDrawChildren = onDrawChildrenComplete // 绑定当前js对象

36.     this.listener.on('layout', FuncLayout)
37.     this.listener.on('draw', FuncDraw)
38.     this.listener.on('drawChildren', FuncDrawChildren)

39.     // 通过句柄向对应的查询条件取消注册回调，由开发者自行决定在何时调用。
40.     // this.listener.off('layout', OffFuncLayout)
41.     // this.listener.off('draw', OffFuncDraw)
42.     // this.listener.off('drawChildren', OffFuncDrawChildren)
43.   }
44. }

## 组件标识属性的扩展能力

通过getInspectorByKey、getInspectorTree、sendEventByKey提供组件标识属性扩展能力，具体如下：

- [getInspectorByKey](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-component-id#getinspectorbykey9)，获取指定id的组件的所有属性。
- [getInspectorTree](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-component-id#getinspectortree9)，获取组件树及组件属性。
- [sendEventByKey](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-component-id#sendeventbykey9)，给指定id的组件发送事件。

下述示例，展示了getInspectorByKey、getInspectorTree和sendEventByKey的基本用法。

1. @Entry
2. @Component
3. struct ComponentPage {
4.   build() {
5.     Column() {
6.       Text("Hello World")
7.         .fontSize(20)
8.         .id("TEXT")
9.         .onClick(() => {
10.           console.info(`Text is clicked`);
11.         })
12.       Button('getInspectorByKey').onClick(() => {
13.         let result = getInspectorByKey("TEXT");
14.         console.info(`result is ${result}`);
15.       })
16.       Button('getInspectorTree').onClick(() => {
17.         let result = getInspectorTree();
18.         console.info(`result is ${JSON.stringify(result)}`);
19.       })
20.       Button('sendEventByKey').onClick(() => {
21.         sendEventByKey("TEXT", 10, "");
22.       })
23.     }
24.     .width('100%')
25.     .height('100%')
26.   }
27. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-manage-components-visibility "感知组件可见性")
# 同应用进程嵌入式组件 (EmbeddedComponent)

更新时间: 2025-12-16 16:40

EmbeddedComponent组件允许当前页面嵌入同一应用内其他EmbeddedUIExtensionAbility供给的UI内容，这些UI运行在独立进程中，提供更高的安全性和稳定性。

EmbeddedComponent组件主要用于实现跨模块、跨进程的嵌入式界面集成，其核心目标是通过模块化设计提升应用的灵活性和用户体验。

开发者在使用时需注意其使用限制和生命周期管理，合理设计应用架构以最大限度地发挥其优势。

## 基本概念

- [EmbeddedComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component)组件
    
    EmbeddedComponent组件用于在当前页面嵌入本应用内其他EmbeddedUIExtensionAbility提供的UI。它允许开发者将应用的某些功能或界面嵌入另一个界面中，实现更灵活的用户界面设计，适用于需要进程隔离的模块化开发场景。
    
- [EmbeddedUIExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-embeddeduiextensionability)组件
    
    提供方应用中定义使用，用于实现跨进程界面嵌入功能，仅能被同应用的UIAbility拉起，并需在多进程权限的场景下使用。
    

## 使用约束

- 设备要求
    
    EmbeddedComponent组件仅可在支持[EmbeddedUIExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-embeddeduiextensionability)的设备上正常运行。
    
- 应用范围
    
    EmbeddedComponent组件只能在UIAbility中使用，且被拉起的EmbeddedUIExtensionAbility需与UIAbility属于同一应用。
    
- 属性限制
    
    EmbeddedComponent组件支持[通用属性](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-component-general-attributes)，且宽高默认值和最小值均为10vp；
    
    不支持如下与宽高相关的属性：
    
    "constraintSize"、"aspectRatio"、"layoutWeight"、"flexBasis"、"flexGrow"和"flexShrink"。
    
- 事件调用
    
    与屏幕坐标相关的事件信息会基于EmbeddedComponent的位置宽高进行坐标转换后传递给被拉起的EmbeddedUIExtensionAbility处理。
    
    EmbeddedComponent组件不支持[点击](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-events-click)等通用事件，仅支持[onTerminated](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component#onterminated)事件和[onError](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component#onerror)事件。
    

## 场景示例

该示例简单展示了EmbeddedComponent组件和EmbeddedUIExtensionAbility的基础使用方式。

**加载项首页**

加载项首页是EmbeddedComponent组件的宿主页面，负责加载和展示嵌入式UI扩展能力的内容。以下是一个完整的加载项首页实现示例：

1. import { Want } from '@kit.AbilityKit';

2. @Entry
3. @Component
4. struct Index {
5.   @State message: string = 'Message: '
6.   private want: Want = {
7.     bundleName: "com.example.embeddeddemo",
8.     abilityName: "ExampleEmbeddedAbility",
9.   }

10.   build() {
11.     Row() {
12.       Column() {
13.         Text(this.message).fontSize(30)
14.         EmbeddedComponent(this.want, EmbeddedType.EMBEDDED_UI_EXTENSION)
15.           .width('100%')
16.           .height('90%')
17.           .onTerminated((info) => {
18.             // 点击extension页面内的terminateSelfWithResult按钮后触发onTerminated回调，文本框显示如下信息
19.             this.message = 'Termination: code = ' + info.code + ', want = ' + JSON.stringify(info.want);
20.           })
21.           .onError((error) => {
22.             // 失败或异常触发onError回调，文本框显示如下报错内容
23.             this.message = 'Error: code = ' + error.code;
24.           })
25.       }
26.       .width('100%')
27.     }
28.     .height('100%')
29.   }
30. }

在ArkTS项目中，EmbeddedUIExtensionAbility的实现代码通常位于项目的ets/extensionAbility目录下。例如，ExampleEmbeddedAbility.ets文件位于./ets/extensionAbility/目录中。

在实现加载项首页时，开发者需要注意以下几点：

- 多进程模型检测
    
    在应用启动时，建议检测设备是否已开启多进程模型。如果未开启，应提供明确的错误提示或引导用户开启。
    
- 异常处理
    
    通过[onError](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component#onerror)事件处理加载或运行嵌入式能力时可能出现的错误，提升用户体验。
    
- 生命周期管理
    
    了解并管理好嵌入式组件的生命周期，确保资源的正确释放和回收。
    
- 样式配置
    
    合理配置EmbeddedComponent组件的大小和位置，确保嵌入式界面能够以期望的尺寸和位置显示。
    

**提供方应用生命周期实现**

提供方应用是指提供嵌入式UI扩展能力的应用。以下是提供方应用生命周期实现的代码示例：

1. import { EmbeddedUIExtensionAbility, UIExtensionContentSession, Want } from '@kit.AbilityKit';

2. const TAG: string = '[ExampleEmbeddedAbility]'

3. export default class ExampleEmbeddedAbility extends EmbeddedUIExtensionAbility {
4.   onCreate() {
5.     console.info(TAG, `onCreate`);
6.   }

7.   onForeground() {
8.     console.info(TAG, `onForeground`);
9.   }

10.   onBackground() {
11.     console.info(TAG, `onBackground`);
12.   }

13.   onDestroy() {
14.     console.info(TAG, `onDestroy`);
15.   }

16.   onSessionCreate(want: Want, session: UIExtensionContentSession) {
17.     console.info(TAG, `onSessionCreate, want: ${JSON.stringify(want)}`);
18.     let param: Record<string, UIExtensionContentSession> = {
19.       'session': session
20.     };
21.     let storage: LocalStorage = new LocalStorage(param);
22.     // 加载pages/extension.ets页面内容
23.     session.loadContent('pages/extension', storage);
24.   }

25.   onSessionDestroy(session: UIExtensionContentSession) {
26.     console.info(TAG, `onSessionDestroy`);
27.   }
28. }

关键实现说明：

- 生命周期阶段
    
    onCreate → onForeground：组件初始化到可见的完整流程；
    
    onBackground → onForeground：前后台切换时的状态迁移；
    
    onDestroy：组件被宿主主动销毁时的资源回收点。
    
- 会话管理
    
    onSessionCreate：创建独立存储上下文并加载UI界面；
    
    onSessionDestroy：处理会话结束时（如用户主动关闭）的清理操作。
    
- 上下文传递
    
    通过LocalStorage实现UIExtensionContentSession的跨组件传递；
    
    使用loadContent方法绑定ArkTS页面与扩展能力上下文。
    

**入口页面**

以下提供方应用的入口组件实现，展示了如何使用UIExtensionContentSession会话以及如何通过按钮点击事件退出嵌入式页面并返回结果，该代码文件需要在main_pages.json配置文件中声明使用。

1. import { UIExtensionContentSession } from '@kit.AbilityKit';

2. @Entry
3. @Component
4. struct Extension {
5.   @State message: string = 'EmbeddedUIExtensionAbility Index';
6.   private localStorage: LocalStorage|undefined = this.getUIContext().getSharedLocalStorage();
7.   private session: UIExtensionContentSession | undefined = this.localStorage?.get<UIExtensionContentSession>('session');

8.   build() {
9.     Column() {
10.       Text(this.message)
11.         .fontSize(20)
12.         .fontWeight(FontWeight.Bold)
13.       Button("terminateSelfWithResult").fontSize(20).onClick(() => {
14.         // 点击按钮后调用terminateSelfWithResult退出
15.         this.session?.terminateSelfWithResult({
16.           resultCode: 1,
17.           want: {
18.             bundleName: "com.example.embeddeddemo",
19.             abilityName: "ExampleEmbeddedAbility",
20.           }
21.         });
22.       })
23.     }.width('100%').height('100%')
24.   }
25. }

在实现入口页面时，开发者需要注意以下几点：

1. 会话管理
    
    正确获取并使用UIExtensionContentSession会话对象，确保与宿主应用的通信正常。
    
2. 结果返回
    
    通过terminateSelfWithResult方法向宿主应用返回结果时，需要指定：
    
    - resultCode：结果代码；
        
    - want：目标意图，指定结果的接收方。
        
3. 页面生命周期
    
    了解并管理好入口页面的生命周期，确保资源的正确释放和回收。
    
4. 样式配置
    
    合理配置页面元素的样式，确保界面显示效果符合预期。
    

**添加配置项**

为了使嵌入式UI扩展能力正常工作，需要在应用的配置文件中进行相应的设置。

在module.json5配置文件的"extensionAbilities"标签下增加ExampleEmbeddedAbility配置，以注册ExampleEmbeddedAbility嵌入式UI扩展能力。

1. {
2.   "name": "ExampleEmbeddedAbility",
3.   "srcEntry": "./ets/extensionAbility/ExampleEmbeddedAbility.ets",
4.   "type": "embeddedUI"
5. }

**预期效果**

1. 在支持EmbeddedUIExtensionAbility的设备上启动应用；
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164028.95389895307243646852896155797513:50001231000000:2800:6C2798BB426D46AD3D1697D607D00976CECE5CEA0B31AD98A5CF00D2B3547366.jpg)
    
2. 点击terminateSelfWithResult按钮，提供方内容消失，页面显示onTerminated信息。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-fullscreencomponent "全屏启动元服务组件（FullScreenLaunchComponent）")
# 同应用进程嵌入式组件 (EmbeddedComponent)

更新时间: 2025-12-16 16:40

EmbeddedComponent组件允许当前页面嵌入同一应用内其他EmbeddedUIExtensionAbility供给的UI内容，这些UI运行在独立进程中，提供更高的安全性和稳定性。

EmbeddedComponent组件主要用于实现跨模块、跨进程的嵌入式界面集成，其核心目标是通过模块化设计提升应用的灵活性和用户体验。

开发者在使用时需注意其使用限制和生命周期管理，合理设计应用架构以最大限度地发挥其优势。

## 基本概念

- [EmbeddedComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component)组件
    
    EmbeddedComponent组件用于在当前页面嵌入本应用内其他EmbeddedUIExtensionAbility提供的UI。它允许开发者将应用的某些功能或界面嵌入另一个界面中，实现更灵活的用户界面设计，适用于需要进程隔离的模块化开发场景。
    
- [EmbeddedUIExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-embeddeduiextensionability)组件
    
    提供方应用中定义使用，用于实现跨进程界面嵌入功能，仅能被同应用的UIAbility拉起，并需在多进程权限的场景下使用。
    

## 使用约束

- 设备要求
    
    EmbeddedComponent组件仅可在支持[EmbeddedUIExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-embeddeduiextensionability)的设备上正常运行。
    
- 应用范围
    
    EmbeddedComponent组件只能在UIAbility中使用，且被拉起的EmbeddedUIExtensionAbility需与UIAbility属于同一应用。
    
- 属性限制
    
    EmbeddedComponent组件支持[通用属性](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-component-general-attributes)，且宽高默认值和最小值均为10vp；
    
    不支持如下与宽高相关的属性：
    
    "constraintSize"、"aspectRatio"、"layoutWeight"、"flexBasis"、"flexGrow"和"flexShrink"。
    
- 事件调用
    
    与屏幕坐标相关的事件信息会基于EmbeddedComponent的位置宽高进行坐标转换后传递给被拉起的EmbeddedUIExtensionAbility处理。
    
    EmbeddedComponent组件不支持[点击](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-events-click)等通用事件，仅支持[onTerminated](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component#onterminated)事件和[onError](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component#onerror)事件。
    

## 场景示例

该示例简单展示了EmbeddedComponent组件和EmbeddedUIExtensionAbility的基础使用方式。

**加载项首页**

加载项首页是EmbeddedComponent组件的宿主页面，负责加载和展示嵌入式UI扩展能力的内容。以下是一个完整的加载项首页实现示例：

1. import { Want } from '@kit.AbilityKit';

2. @Entry
3. @Component
4. struct Index {
5.   @State message: string = 'Message: '
6.   private want: Want = {
7.     bundleName: "com.example.embeddeddemo",
8.     abilityName: "ExampleEmbeddedAbility",
9.   }

10.   build() {
11.     Row() {
12.       Column() {
13.         Text(this.message).fontSize(30)
14.         EmbeddedComponent(this.want, EmbeddedType.EMBEDDED_UI_EXTENSION)
15.           .width('100%')
16.           .height('90%')
17.           .onTerminated((info) => {
18.             // 点击extension页面内的terminateSelfWithResult按钮后触发onTerminated回调，文本框显示如下信息
19.             this.message = 'Termination: code = ' + info.code + ', want = ' + JSON.stringify(info.want);
20.           })
21.           .onError((error) => {
22.             // 失败或异常触发onError回调，文本框显示如下报错内容
23.             this.message = 'Error: code = ' + error.code;
24.           })
25.       }
26.       .width('100%')
27.     }
28.     .height('100%')
29.   }
30. }

在ArkTS项目中，EmbeddedUIExtensionAbility的实现代码通常位于项目的ets/extensionAbility目录下。例如，ExampleEmbeddedAbility.ets文件位于./ets/extensionAbility/目录中。

在实现加载项首页时，开发者需要注意以下几点：

- 多进程模型检测
    
    在应用启动时，建议检测设备是否已开启多进程模型。如果未开启，应提供明确的错误提示或引导用户开启。
    
- 异常处理
    
    通过[onError](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component#onerror)事件处理加载或运行嵌入式能力时可能出现的错误，提升用户体验。
    
- 生命周期管理
    
    了解并管理好嵌入式组件的生命周期，确保资源的正确释放和回收。
    
- 样式配置
    
    合理配置EmbeddedComponent组件的大小和位置，确保嵌入式界面能够以期望的尺寸和位置显示。
    

**提供方应用生命周期实现**

提供方应用是指提供嵌入式UI扩展能力的应用。以下是提供方应用生命周期实现的代码示例：

1. import { EmbeddedUIExtensionAbility, UIExtensionContentSession, Want } from '@kit.AbilityKit';

2. const TAG: string = '[ExampleEmbeddedAbility]'

3. export default class ExampleEmbeddedAbility extends EmbeddedUIExtensionAbility {
4.   onCreate() {
5.     console.info(TAG, `onCreate`);
6.   }

7.   onForeground() {
8.     console.info(TAG, `onForeground`);
9.   }

10.   onBackground() {
11.     console.info(TAG, `onBackground`);
12.   }

13.   onDestroy() {
14.     console.info(TAG, `onDestroy`);
15.   }

16.   onSessionCreate(want: Want, session: UIExtensionContentSession) {
17.     console.info(TAG, `onSessionCreate, want: ${JSON.stringify(want)}`);
18.     let param: Record<string, UIExtensionContentSession> = {
19.       'session': session
20.     };
21.     let storage: LocalStorage = new LocalStorage(param);
22.     // 加载pages/extension.ets页面内容
23.     session.loadContent('pages/extension', storage);
24.   }

25.   onSessionDestroy(session: UIExtensionContentSession) {
26.     console.info(TAG, `onSessionDestroy`);
27.   }
28. }

关键实现说明：

- 生命周期阶段
    
    onCreate → onForeground：组件初始化到可见的完整流程；
    
    onBackground → onForeground：前后台切换时的状态迁移；
    
    onDestroy：组件被宿主主动销毁时的资源回收点。
    
- 会话管理
    
    onSessionCreate：创建独立存储上下文并加载UI界面；
    
    onSessionDestroy：处理会话结束时（如用户主动关闭）的清理操作。
    
- 上下文传递
    
    通过LocalStorage实现UIExtensionContentSession的跨组件传递；
    
    使用loadContent方法绑定ArkTS页面与扩展能力上下文。
    

**入口页面**

以下提供方应用的入口组件实现，展示了如何使用UIExtensionContentSession会话以及如何通过按钮点击事件退出嵌入式页面并返回结果，该代码文件需要在main_pages.json配置文件中声明使用。

1. import { UIExtensionContentSession } from '@kit.AbilityKit';

2. @Entry
3. @Component
4. struct Extension {
5.   @State message: string = 'EmbeddedUIExtensionAbility Index';
6.   private localStorage: LocalStorage|undefined = this.getUIContext().getSharedLocalStorage();
7.   private session: UIExtensionContentSession | undefined = this.localStorage?.get<UIExtensionContentSession>('session');

8.   build() {
9.     Column() {
10.       Text(this.message)
11.         .fontSize(20)
12.         .fontWeight(FontWeight.Bold)
13.       Button("terminateSelfWithResult").fontSize(20).onClick(() => {
14.         // 点击按钮后调用terminateSelfWithResult退出
15.         this.session?.terminateSelfWithResult({
16.           resultCode: 1,
17.           want: {
18.             bundleName: "com.example.embeddeddemo",
19.             abilityName: "ExampleEmbeddedAbility",
20.           }
21.         });
22.       })
23.     }.width('100%').height('100%')
24.   }
25. }

在实现入口页面时，开发者需要注意以下几点：

1. 会话管理
    
    正确获取并使用UIExtensionContentSession会话对象，确保与宿主应用的通信正常。
    
2. 结果返回
    
    通过terminateSelfWithResult方法向宿主应用返回结果时，需要指定：
    
    - resultCode：结果代码；
        
    - want：目标意图，指定结果的接收方。
        
3. 页面生命周期
    
    了解并管理好入口页面的生命周期，确保资源的正确释放和回收。
    
4. 样式配置
    
    合理配置页面元素的样式，确保界面显示效果符合预期。
    

**添加配置项**

为了使嵌入式UI扩展能力正常工作，需要在应用的配置文件中进行相应的设置。

在module.json5配置文件的"extensionAbilities"标签下增加ExampleEmbeddedAbility配置，以注册ExampleEmbeddedAbility嵌入式UI扩展能力。

1. {
2.   "name": "ExampleEmbeddedAbility",
3.   "srcEntry": "./ets/extensionAbility/ExampleEmbeddedAbility.ets",
4.   "type": "embeddedUI"
5. }

**预期效果**

1. 在支持EmbeddedUIExtensionAbility的设备上启动应用；
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164028.95389895307243646852896155797513:50001231000000:2800:6C2798BB426D46AD3D1697D607D00976CECE5CEA0B31AD98A5CF00D2B3547366.jpg)
    
2. 点击terminateSelfWithResult按钮，提供方内容消失，页面显示onTerminated信息。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-fullscreencomponent "全屏启动元服务组件（FullScreenLaunchComponent）")
# 同应用进程嵌入式组件 (EmbeddedComponent)

更新时间: 2025-12-16 16:40

EmbeddedComponent组件允许当前页面嵌入同一应用内其他EmbeddedUIExtensionAbility供给的UI内容，这些UI运行在独立进程中，提供更高的安全性和稳定性。

EmbeddedComponent组件主要用于实现跨模块、跨进程的嵌入式界面集成，其核心目标是通过模块化设计提升应用的灵活性和用户体验。

开发者在使用时需注意其使用限制和生命周期管理，合理设计应用架构以最大限度地发挥其优势。

## 基本概念

- [EmbeddedComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component)组件
    
    EmbeddedComponent组件用于在当前页面嵌入本应用内其他EmbeddedUIExtensionAbility提供的UI。它允许开发者将应用的某些功能或界面嵌入另一个界面中，实现更灵活的用户界面设计，适用于需要进程隔离的模块化开发场景。
    
- [EmbeddedUIExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-embeddeduiextensionability)组件
    
    提供方应用中定义使用，用于实现跨进程界面嵌入功能，仅能被同应用的UIAbility拉起，并需在多进程权限的场景下使用。
    

## 使用约束

- 设备要求
    
    EmbeddedComponent组件仅可在支持[EmbeddedUIExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-embeddeduiextensionability)的设备上正常运行。
    
- 应用范围
    
    EmbeddedComponent组件只能在UIAbility中使用，且被拉起的EmbeddedUIExtensionAbility需与UIAbility属于同一应用。
    
- 属性限制
    
    EmbeddedComponent组件支持[通用属性](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-component-general-attributes)，且宽高默认值和最小值均为10vp；
    
    不支持如下与宽高相关的属性：
    
    "constraintSize"、"aspectRatio"、"layoutWeight"、"flexBasis"、"flexGrow"和"flexShrink"。
    
- 事件调用
    
    与屏幕坐标相关的事件信息会基于EmbeddedComponent的位置宽高进行坐标转换后传递给被拉起的EmbeddedUIExtensionAbility处理。
    
    EmbeddedComponent组件不支持[点击](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-events-click)等通用事件，仅支持[onTerminated](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component#onterminated)事件和[onError](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component#onerror)事件。
    

## 场景示例

该示例简单展示了EmbeddedComponent组件和EmbeddedUIExtensionAbility的基础使用方式。

**加载项首页**

加载项首页是EmbeddedComponent组件的宿主页面，负责加载和展示嵌入式UI扩展能力的内容。以下是一个完整的加载项首页实现示例：

1. import { Want } from '@kit.AbilityKit';

2. @Entry
3. @Component
4. struct Index {
5.   @State message: string = 'Message: '
6.   private want: Want = {
7.     bundleName: "com.example.embeddeddemo",
8.     abilityName: "ExampleEmbeddedAbility",
9.   }

10.   build() {
11.     Row() {
12.       Column() {
13.         Text(this.message).fontSize(30)
14.         EmbeddedComponent(this.want, EmbeddedType.EMBEDDED_UI_EXTENSION)
15.           .width('100%')
16.           .height('90%')
17.           .onTerminated((info) => {
18.             // 点击extension页面内的terminateSelfWithResult按钮后触发onTerminated回调，文本框显示如下信息
19.             this.message = 'Termination: code = ' + info.code + ', want = ' + JSON.stringify(info.want);
20.           })
21.           .onError((error) => {
22.             // 失败或异常触发onError回调，文本框显示如下报错内容
23.             this.message = 'Error: code = ' + error.code;
24.           })
25.       }
26.       .width('100%')
27.     }
28.     .height('100%')
29.   }
30. }

在ArkTS项目中，EmbeddedUIExtensionAbility的实现代码通常位于项目的ets/extensionAbility目录下。例如，ExampleEmbeddedAbility.ets文件位于./ets/extensionAbility/目录中。

在实现加载项首页时，开发者需要注意以下几点：

- 多进程模型检测
    
    在应用启动时，建议检测设备是否已开启多进程模型。如果未开启，应提供明确的错误提示或引导用户开启。
    
- 异常处理
    
    通过[onError](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-embedded-component#onerror)事件处理加载或运行嵌入式能力时可能出现的错误，提升用户体验。
    
- 生命周期管理
    
    了解并管理好嵌入式组件的生命周期，确保资源的正确释放和回收。
    
- 样式配置
    
    合理配置EmbeddedComponent组件的大小和位置，确保嵌入式界面能够以期望的尺寸和位置显示。
    

**提供方应用生命周期实现**

提供方应用是指提供嵌入式UI扩展能力的应用。以下是提供方应用生命周期实现的代码示例：

1. import { EmbeddedUIExtensionAbility, UIExtensionContentSession, Want } from '@kit.AbilityKit';

2. const TAG: string = '[ExampleEmbeddedAbility]'

3. export default class ExampleEmbeddedAbility extends EmbeddedUIExtensionAbility {
4.   onCreate() {
5.     console.info(TAG, `onCreate`);
6.   }

7.   onForeground() {
8.     console.info(TAG, `onForeground`);
9.   }

10.   onBackground() {
11.     console.info(TAG, `onBackground`);
12.   }

13.   onDestroy() {
14.     console.info(TAG, `onDestroy`);
15.   }

16.   onSessionCreate(want: Want, session: UIExtensionContentSession) {
17.     console.info(TAG, `onSessionCreate, want: ${JSON.stringify(want)}`);
18.     let param: Record<string, UIExtensionContentSession> = {
19.       'session': session
20.     };
21.     let storage: LocalStorage = new LocalStorage(param);
22.     // 加载pages/extension.ets页面内容
23.     session.loadContent('pages/extension', storage);
24.   }

25.   onSessionDestroy(session: UIExtensionContentSession) {
26.     console.info(TAG, `onSessionDestroy`);
27.   }
28. }

关键实现说明：

- 生命周期阶段
    
    onCreate → onForeground：组件初始化到可见的完整流程；
    
    onBackground → onForeground：前后台切换时的状态迁移；
    
    onDestroy：组件被宿主主动销毁时的资源回收点。
    
- 会话管理
    
    onSessionCreate：创建独立存储上下文并加载UI界面；
    
    onSessionDestroy：处理会话结束时（如用户主动关闭）的清理操作。
    
- 上下文传递
    
    通过LocalStorage实现UIExtensionContentSession的跨组件传递；
    
    使用loadContent方法绑定ArkTS页面与扩展能力上下文。
    

**入口页面**

以下提供方应用的入口组件实现，展示了如何使用UIExtensionContentSession会话以及如何通过按钮点击事件退出嵌入式页面并返回结果，该代码文件需要在main_pages.json配置文件中声明使用。

1. import { UIExtensionContentSession } from '@kit.AbilityKit';

2. @Entry
3. @Component
4. struct Extension {
5.   @State message: string = 'EmbeddedUIExtensionAbility Index';
6.   private localStorage: LocalStorage|undefined = this.getUIContext().getSharedLocalStorage();
7.   private session: UIExtensionContentSession | undefined = this.localStorage?.get<UIExtensionContentSession>('session');

8.   build() {
9.     Column() {
10.       Text(this.message)
11.         .fontSize(20)
12.         .fontWeight(FontWeight.Bold)
13.       Button("terminateSelfWithResult").fontSize(20).onClick(() => {
14.         // 点击按钮后调用terminateSelfWithResult退出
15.         this.session?.terminateSelfWithResult({
16.           resultCode: 1,
17.           want: {
18.             bundleName: "com.example.embeddeddemo",
19.             abilityName: "ExampleEmbeddedAbility",
20.           }
21.         });
22.       })
23.     }.width('100%').height('100%')
24.   }
25. }

在实现入口页面时，开发者需要注意以下几点：

1. 会话管理
    
    正确获取并使用UIExtensionContentSession会话对象，确保与宿主应用的通信正常。
    
2. 结果返回
    
    通过terminateSelfWithResult方法向宿主应用返回结果时，需要指定：
    
    - resultCode：结果代码；
        
    - want：目标意图，指定结果的接收方。
        
3. 页面生命周期
    
    了解并管理好入口页面的生命周期，确保资源的正确释放和回收。
    
4. 样式配置
    
    合理配置页面元素的样式，确保界面显示效果符合预期。
    

**添加配置项**

为了使嵌入式UI扩展能力正常工作，需要在应用的配置文件中进行相应的设置。

在module.json5配置文件的"extensionAbilities"标签下增加ExampleEmbeddedAbility配置，以注册ExampleEmbeddedAbility嵌入式UI扩展能力。

1. {
2.   "name": "ExampleEmbeddedAbility",
3.   "srcEntry": "./ets/extensionAbility/ExampleEmbeddedAbility.ets",
4.   "type": "embeddedUI"
5. }

**预期效果**

1. 在支持EmbeddedUIExtensionAbility的设备上启动应用；
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216164028.95389895307243646852896155797513:50001231000000:2800:6C2798BB426D46AD3D1697D607D00976CECE5CEA0B31AD98A5CF00D2B3547366.jpg)
    
2. 点击terminateSelfWithResult按钮，提供方内容消失，页面显示onTerminated信息。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-fullscreencomponent "全屏启动元服务组件（FullScreenLaunchComponent）")
