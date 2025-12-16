如何在鸿蒙系统使用ARKUI 颜色

在鸿蒙系统中使用ArkUI颜色，主要有以下几种方式：

**1. **使用内置主题颜色****

ArkUI提供了一套内置主题颜色，可通过`theme.colors`对象访问。这些颜色在不同主题模式（如浅色、深色）下会自动适配。

示例：

typescript

```typescript
import { theme } from '@kit.arkui';

@entry
@Component
struct MyComponent {
  build() {
    Column() {
      Text('一级文本').fontColor(theme.colors.fontPrimary);
      Text('二级文本').fontColor(theme.colors.fontSecondary);
      Row() {
        Text('品牌色').fontColor(theme.colors.brand);
        Text('警示色').fontColor(theme.colors.warning);
      }
    }
  }
}
```

**2. **自定义全局主题颜色****

若需自定义颜色，可创建自定义主题并应用到整个应用。

步骤如下：

1. **定义自定义颜色类**：

typescript

```typescript
// apptheme.ets
import { CustomColors, CustomTheme } from '@kit.arkui';

export class AppColors implements CustomColors {
  brand = 0xff75d9;        // 自定义品牌色
  fontPrimary = 0xffd53032; // 自定义一级文本颜色
  backgroundPrimary = 0xfff1f3f5; // 自定义一级背景色
}

export class AppTheme implements CustomTheme {
  public colors: AppColors = new AppColors();
}

export let gAppTheme: CustomTheme = new AppTheme();
```

2. **在Ability中设置全局主题**：

typescript

```typescript
// entryability.ets
import { ThemeControl } from '@kit.arkui';
import { gAppTheme } from './apptheme';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: Window.WindowStage) {
    ThemeControl.setDefaultTheme(gAppTheme);
  }
}
```

**3. **局部应用自定义颜色****

在组件内部通过`withTheme`局部应用自定义主题，无需影响全局。

示例：

typescript

```typescript
@entry
@Component
struct MyPage {
  @State customTheme: CustomTheme = new AppTheme();

  build() {
    withTheme({ theme: this.customTheme }) {
      Column() {
        Text('局部应用主题').fontColor(theme.colors.fontPrimary);
        Button('切换主题').onClick(() => {
          // 切换自定义主题逻辑
        });
      }
    }
  }
}
```

**4. **直接使用颜色值****

可直接使用十六进制颜色值或RGB/RGBA格式定义颜色。

示例：

typescript

```typescript
Text('直接使用颜色').fontColor(0xff00ff00); // 绿色
Text('透明颜色').fontColor(Color.rgba(255, 0, 0, 0.5)); // 半透明红色
```

**5. **颜色渐变****

ArkUI支持线性渐变、角度渐变和径向渐变，适用于背景或特定组件。

示例（线性渐变）：

typescript

```typescript
Row() {
  .width(150)
  .height(150)
  .linearGradient({
    direction: GradientDirection.rightBottom,
    colors: [[0xffe1e1, 0.0], [0xd3e0dc, 0.3], [0xfcd1d1, 1.01]]
  })
}
```

通过以上方法，可在鸿蒙系统中灵活使用ArkUI颜色，实现丰富的视觉效果和主题适配。
根据您提供的文档内容，我将为您详细解答如何在鸿蒙系统（HarmonyOS）中使用 ArkUI。

## 📋 **如何在鸿蒙系统使用 ArkUI**

### ✅ **核心结论**

在鸿蒙系统（HarmonyOS）中使用 ArkUI，**需要遵循其声明式开发范式，使用 Ar****kTS 语言进行应用开发**。ArkUI 是 HarmonyOS 的官方 UI 开发框架，为构建跨设备应用界面提供了完整的解决方案。

---

### 🛠️ **使用 ArkUI 的完整流程**

#### **1. 开发环境准备**

根据《开发准备_c2cc2b11.pdf》：

- **开发工具**：使用 **DevEco Studio**。

- **开发语言**：主要使用 **ArkTS**（HarmonyOS 的官方应用开发语言）。

- **应用模型**：了解 **Stage 模型**（当前主推的应用模型）。

#### **2. 理解 ArkUI 与 ArkT****S 的关系**

根据《ArkTS语言与ArkUI框架、HarmonyOS SDK-API的关系.pdf》：

- **ArkTS** 是**编程语言**，负责业务逻辑和数据处理。

- **ArkUI** 是**基于 ArkTS 构建的 UI 框架**，专注于界面描述和组件化构建。

- 二者关系：**ArkTS 是语言底座，ArkUI** **是上层框架**。开发时，你用 ArkTS 写代码，调用 ArkUI 提供的组件和 API 来构建界面。

#### **3. 创建 UI 界面（核心步骤）**

ArkUI 采用**声明式 UI** 范式。基本结构如下：

1. **定义自定义组件**：使用  @Component  装饰器。

2. **描述 UI 结构**：在  build()  方法中使用内置的**系统组件**（如  Column 、 Row 、 Text 、 Button ）和**属性方法**链式调用。

3. **管理 UI 状态**：使用  @State 、 @Prop  等装饰器实现数据与 UI 的自动同步。

**简单示例（基于《开发准备_c2cc2****b11.pdf》和《基本语法概述.pdf》）：**

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/b3b7e70537954919942a336cc7deabbc?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765880692%3B1765909492&q-key-time=1765880692%3B1765909492&q-header-list=&q-url-param-list=&q-signature=ad97adf3933fb375e9e10ef795577f821388f663)

```
// Entry 装饰的组件为页面入口组件@Entry// Component 装饰的 struct 表示这是一个自定义组件@Componentstruct Index {  // @State 装饰的变量是状态变量，其变化会触发UI更新  @State message: string = 'Hello World'
  build() {    // Column 是内置的垂直布局容器组件    Column() {      // Text 是内置的文本显示组件      Text(this.message)        .fontSize(50) // 属性方法：设置字体大小        .fontWeight(FontWeight.Bold)        .onClick(() => { // 事件方法：设置点击事件          this.message = 'Hello ArkUI!'        })      // Button 是内置的按钮组件      Button('Next')        .onClick(() => {          // 页面跳转逻辑        })    }    .width('100%')    .height('100%')    .justifyContent(FlexAlign.Center) // 属性方法：设置子组件在主轴上的对齐方式  }}
```

TypeScript

#### **4. 利用 ArkUI 的核心能力**

根据文档，ArkUI 提供了丰富的能力，您可以根据需求选择使用：

|能力类别|关键文档参考|核心用途|
|---|---|---|
|**布局与组件**|《组件布局场景.pdf》、《自定义组件的自定义布局.pdf》|使用  Flex 、 Grid 、 List 、 WaterFlow  等组件进行界面布局，或通过  onMeasureSize  和  onPlaceChildren  实现自定义布局。|
|**样式与主题**|《添加标题行和文本区域.pdf》、《ArkUI_NativeModule.pdf》|通过  .css  文件或链式调用设置组件样式（颜色、字体、边距等）。|
|**手势与事件**|《绑定手势事件.pdf》、《单一手势.pdf》、《监听组件事件.pdf》|为组件绑定点击、长按、拖拽、捏合等手势，并处理相关事件。|
|**动画**|《使用动画.pdf》|使用属性动画或显式动画（ animateTo ）为组件添加转场和动态效果。|
|**状态管理**|《@ohos.arkui.StateManagement.pdf》|使用  AppStorage 、 PersistenceV2  等进行应用级状态管理和数据持久化。|
|**多设备适配**|《一次开发，多端部署概览.pdf》、《多设备社区评论界面.pdf》|利用**断点机制**和响应式组件（如  GridRow 、 GridCol ），为不同屏幕尺寸的设备定义差异化布局。|
|**高级 UI 功能**|《自定义渲染 (XComponent).pdf》、《通过XComponent接入无障碍.pdf》|嵌入原生渲染视图（如游戏、地图），或为自定义视图添加无障碍支持。|
|**弹窗与交互**|《menu开发指导.pdf》、《页面级弹出框.pdf》、《ArkUI_NativeDialogAPI_1.pdf》|创建菜单、对话框、全屏模态页等交互组件。|

#### **5. 调试与预览**

- **实时预览**：DevEco Studio 提供 ArkUI 预览器，可实时查看 UI 效果（《查看ArkUI预览效果.pdf》）。

- **布局调试**：使用 **ArkUI Inspector** 工具分析组件树、属性和布局边界，定位 UI 问题（《布局分析.pdf》）。

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/760e494c39fd476c80d9c6c98c4d1042?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765880693%3B1765909493&q-key-time=1765880693%3B1765909493&q-header-list=&q-url-param-list=&q-signature=9e52241d0afecf83e511ab96fee4cb20703e2f6a)

#### **6. 深入学习**

- **官方指南**：参考《UI开发》文档（在《开发准备》中提及）。

- **最佳实践**：学习《最佳实践概览.pdf》中关于界面开发、功能开发、多设备开发等主题的案例。

- **示例代码**：研究提供的各类示例，如《足球比赛十六强晋级图》、《酒店入住评价》、《购物比价类行业实践》等，了解复杂 UI 的实现。

### 📝 **总结与快速入门步骤**

1. **安装 DevEco Studio**，配置 HarmonyOS SDK。

2. 创建一个新的 **HarmonyOS 应用工程**，选择 **ArkTS** 语言和 **Stage** 模型。

3. 在  entry/src/main/ets  /pages  目录下的  .ets  文件中，使用 **ArkTS 语法**和 **ArkUI 组件**编写 UI。

4. 利用  @State  等装饰器管理数据状态，实现 UI 的动态更新。

5. 使用 **预览器** 查看效果，在 **真机或模拟器** 上运行测试。

6. 根据应用需求，参考对应文档，集成布局、手势、动画、多设备适配等高级功能。

**简单来说，在鸿蒙系统使用 ArkUI****，就是：用 ArkTS 语言，在 DevEco Studio 中，通过声明式语法调用 ArkUI 框架提供的丰富组件和 API，来构建你的应用界面。** 根据您提供的文档内容，我将以**具体实例**的形式，讲解几个核心 ArkUI 组件的使用方法。

### 📋 **核心原则**

所有实例都基于文档中提到的 **ArkTS 声明式开发范式**，遵循  @Component 、 @State 、 build()  等基本语法。

---

## 📚 **实例一：使用**  **@LocalBuilder**  **装饰器实现参数引用传递**

**文档依据**：《@LocalBuilder装饰器： 维持组件关系.pdf》

**场景**：父组件  Parent  中有一个  @LocalBuilder  装饰的函数，该函数内部调用了子组件  HelloComponent ，并按**引用**传递参数。当父组件的状态变量变化时，子组件的显示内容也同步更新。

**代码实例**：

```
// 定义一个引用类型class ReferenceType {  paramString: string = '';}
// 子组件，通过 @Prop 接收引用参数@Componentstruct HelloComponent {  @Prop message: string; // @Prop 装饰器接收父组件的引用
  build() {    Row() {      Text(`HelloComponent===${this.message}`)    }  }}
// 父组件@Entry@Componentstruct Parent {  @State variableValue: string = 'Hello World'; // 父组件的状态变量
  // 使用 @LocalBuilder 装饰一个函数，按引用传递参数  @LocalBuilder  citeLocalBuilder($$: ReferenceType) {    Row() {      Column() {        Text(`citeLocalBuilder===${$$.paramString}`)        // 调用子组件，并将引用参数传递给它        HelloComponent({ message: $$.paramString })      }    }  }
  build() {    Column() {      // 调用 LocalBuilder 函数，传入当前状态变量的引用      this.citeLocalBuilder({ paramString: this.variableValue })            Button('Click me')        .onClick(() => {          // 点击按钮改变状态变量          this.variableValue = 'Hi World';        })    }  }}
```

TypeScript

**运行效果**：

1. 初始界面显示  citeLocalBuilder==  =Hello World  和  HelloComponent===H  ello World 。

2. 点击按钮后，两处文本都变为  citeLocalBuilder==  =Hi World  和  HelloComponent===H  i World 。

**关键点**：

-  @LocalBuilder  装饰的函数可以**维持组件间的响应式关系**。

- 通过**引用类型（如**  **ReferenceType** **）** 传递参数，子组件使用  @Prop  接收，当父组件状态变化时，子组件会自动更新。

- 使用  $$  作为引用传递的范式参数名。

---

## 📚 **实例二：使用**  **List**  **和**  **LazyForEach**  **实现高性能长列表**

**文档依据**：《使用列表.pdf》、《监听组件事件.pdf》

**场景**：创建一个可滚动的长列表，使用  NodeAdapter （NDK 侧的  LazyForEach ）实现**懒加载**，以提升性能。同时监听列表的滚动事件。

**代码实例（ArkTS 侧简化示意，原****理同 NDK 的 NodeAdapter）**：

```
// 定义列表项数据类class ItemData {  id: string;  name: string;
  constructor(id: string, name: string) {    this.id = id;    this.name = name;  }}
// 数据源管理类，用于 LazyForEachclass ItemDataSource implements IDataSource {  private dataArray: ItemData[] = [];
  // ... 数据增删改查方法
  totalCount(): number {    return this.dataArray.length;  }
  getData(index: number): ItemData {    return this.dataArray[index];  }
  registerDataChangeListener(listener: DataChangeListener): void {}  unregisterDataChangeListener(listener: DataChangeListener): void {}}
@Entry@Componentstruct LongListExample {  private dataSource: ItemDataSource = new ItemDataSource();  private scroller: Scroller = new Scroller();
  aboutToAppear() {    // 初始化数据    for (let i = 0; i < 1000; i++) {      this.dataSource.pushData(new ItemData(i.toString(), `Item ${i}`));    }  }
  build() {    Column() {      // 创建 List 组件      List({ space: 10, scroller: this.scroller }) {        // 使用 LazyForEach 进行懒加载渲染        LazyForEach(this.dataSource, (item: ItemData) => {          ListItem() {            Text(item.name)              .fontSize(18)              .padding(10)              .backgroundColor(Color.White)              .borderRadius(8)          }          .onClick(() => {            console.info(`Clicked item: ${item.name}`);          })        }, (item: ItemData) => item.id)      }      .width('100%')      .height('100%')      .onScroll((scrollOffset, scrollState) => {        // 监听滚动事件        console.info(`Scrolled to offset: ${scrollOffset}`);        if (scrollState === ScrollState.ScrollEnd) {          // 滚动到底部时，可以加载更多数据          console.info('Reached end, load more data...');        }      })      .onReachEnd(() => {        // 另一种监听到底部的方式        console.info('List reach end event triggered.');      })    }  }}
```

TypeScript

**关键点**：

-  **LazyForEach** ：用于大数据量列表，只创建可视区域内的列表项，大幅提升性能。

-  **NodeAdapter** **（NDK）**：在 C++ 侧实现类似功能，通过  NODE_ADAPTER_EVENT  _ON_ADD_NODE_TO_ADAPTER  等事件按需创建和销毁节点。

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/90e018d190ee423f9c4ee742761d275b?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765880769%3B1765909569&q-key-time=1765880769%3B1765909569&q-header-list=&q-url-param-list=&q-signature=664a7d55828c619c06ce9c594afa6e5bb4b7fdb0)

- **滚动监听**：通过  onScroll  或  onReachEnd  事件可以实现**无限滚动**、**曝光埋点**等功能。

---

## 📚 **实例三：使用**  **@Builder**  **和**  **@BuilderParam**  **实现类似“插槽”的功能**

**文档依据**：《如何实现类似插槽的功能.pdf》、《如何实现类似插槽的功能_23f96e45.pdf》

**场景**：创建一个可复用的卡片组件  Card ，其内容区域（类似“插槽”）可以由父组件动态传入。

**代码实例**：

```
// 子组件：定义卡片容器，预留一个“插槽”@Componentstruct Card {  @BuilderParam content: () => void; // 使用 @BuilderParam 声明一个占位符
  build() {    Column() {      // 卡片的固定头部      Text('Card Title')        .fontSize(20)        .fontWeight(FontWeight.Bold)        .margin({ top: 10 })
      Divider().margin(10)
      // “插槽”位置：显示父组件传入的内容      this.content() // 调用 @BuilderParam
      // 卡片的固定底部      Button('Action')        .margin(10)    }    .width('90%')    .padding(10)    .backgroundColor(Color.White)    .border({ width: 1, color: Color.Grey })    .borderRadius(15)    .shadow({ radius: 6, color: Color.Grey })  }}
// 父组件@Entry@Componentstruct ParentPage {  @State cardData: string = 'Dynamic Content from Parent';
  // 定义一个 @Builder 函数，作为要传入卡片的内容  @Builder  CustomCardContent() {    Column() {      Text(this.cardData)        .fontSize(16)        .fontColor(Color.Blue)      Image($r('app.media.icon'))        .width(50)        .height(50)        .margin({ top: 10 })    }    .alignItems(HorizontalAlign.Center)  }
  build() {    Column({ space: 20 }) {      // 使用 Card 组件，并通过属性初始化传入自定义内容      Card({ content: this.CustomCardContent })
      Button('Change Content')        .onClick(() => {          this.cardData = 'Updated Content!';        })    }    .width('100%')    .height('100%')    .padding(20)    .backgroundColor(Color.LightGray)  }}
```

TypeScript

**运行效果**：

1. 卡片内部显示父组件定义的  CustomCardContent ，包括文本和图片。

2. 点击按钮后，卡片内的文本内容更新。

**关键点**：

-  **@Builder** ：用于封装可复用的 UI 描述块。

-  **@BuilderParam** ：在自定义组件中声明一个属性，作为 UI 描述的“占位符”，允许父组件在初始化时传入一个  @Builder  函数。

- 实现了**组件内容动态化**，提高了组件的复用性和灵活性。

---

## 📚 **实例四：使用**  **Navigation**  **和**  **NavPathStack**  **实现页面路由与参数传递**

**文档依据**：《酒店入住评价_0fd549c5.pdf》、《router页面和自定义组件生命周期.pdf》

**场景**：构建一个简单的酒店订单列表，点击订单项跳转到评价页面，并传递订单信息。

**代码实例**：

```
// 定义订单数据类型class Order {  id: string;  hotelName: string;  date: string;
  constructor(id: string, name: string, date: string) {    this.id = id;    this.hotelName = name;    this.date = date;  }}
// 订单列表页@Entry@Componentstruct OrderListPage {  @State orders: Order[] = [    new Order('1', 'Grand Hotel', '2023-10-26'),    new Order('2', 'Seaside Resort', '2023-10-27'),  ];  private navStack: NavPathStack = new NavPathStack();
  build() {    Navigation(this.navStack) {      Column() {        Text('My Orders')          .fontSize(24)          .margin({ top: 20, bottom: 20 })
        List({ space: 10 }) {          ForEach(this.orders, (item: Order) => {            ListItem() {              Row({ space: 10 }) {                Column() {                  Text(item.hotelName).fontSize(18)                  Text(`Date: ${item.date}`).fontSize(14).fontColor(Color.Gray)                }                .layoutWeight(1)                Image($r('app.media.arrow_right'))                  .width(20)                  .height(20)              }              .padding(15)              .backgroundColor(Color.White)              .borderRadius(10)            }            .onClick(() => {              // 点击跳转到评价页，并通过 NavPathStack 传递参数              this.navStack.pushPath({                name: 'RatingPage',                param: { orderId: item.id, hotelName: item.hotelName } // 传递参数              });            })          })        }        .width('100%')        .layoutWeight(1)      }      .width('100%')      .height('100%')      .padding(20)    }    .title('Order List')    .hideTitleBar(false)  }}
// 评价页面@Componentstruct RatingPage {  private orderId: string = '';  private hotelName: string = '';
  onPageShow() {    // 从路由参数中获取数据    const params = this.getUIContext().getRouter().getParams();    if (params) {      this.orderId = params['orderId'] as string;      this.hotelName = params['hotelName'] as string;    }    console.info(`Rating page for order: ${this.orderId}, hotel: ${this.hotelName}`);  }
  build() {    Column({ space: 20 }) {      Text(`Rate your stay at:`)        .fontSize(16)      Text(this.hotelName)        .fontSize(24)        .fontWeight(FontWeight.Bold)
      // 这里可以添加评分组件、输入框等      Text('Rating UI here...')
      Button('Submit Rating')        .width('80%')        .onClick(() => {          // 提交评价，然后返回          promptAction.showToast({ message: 'Rating submitted!' });          router.back();        })    }    .width('100%')    .height('100%')    .padding(20)    .alignItems(HorizontalAlign.Center)  }}
```

TypeScript

**关键点**：

-  **Navigation**  **和**  **NavPathStack** ：管理页面栈，实现页面跳转和返回。

- **参数传递**：通过  pushPath  的  param  字段将数据传递给目标页面。

- **生命周期**：目标页面在  onPageShow  生命周期中通过  router.getParams()  获取参数。

-  **ForEach** ：用于循环渲染列表数据。

---

## 📚 **实例五：使用**  **@State** **、** **@Prop** **、** **@Link**  **进行组件间状态管理**

**文档依据**：《MVVM模式_108201dc.pdf》、《基本语法概述.pdf》

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/1a56ca320a6640ec94f76b2ad946f387?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765880769%3B1765909569&q-key-time=1765880769%3B1765909569&q-header-list=&q-url-param-list=&q-signature=796696f0c72644de37e294e68926007cf01a84b2)

**场景**：构建一个简单的待办事项（Todo）应用，展示父子组件间不同的状态传递方式。

**代码实例**：

```
// 子组件：单个待办项@Componentstruct TodoItem {  @Prop isFinished: boolean; // @Prop：单向从父到子，子组件修改不影响父组件  @Link @Watch('onTaskChange') taskName: string; // @Link：双向同步，父子组件数据联动
  @State private tempName: string = ''; // @State：组件内部私有状态
  onTaskChange() {    console.info(`Task name changed to: ${this.taskName}`);  }
  build() {    Row({ space: 10 }) {      // 复选框      Checkbox({ name: '', group: '' })        .select(this.isFinished)        .onChange((value: boolean) => {          this.isFinished = value;        })
      // 可编辑的文本      if (this.isFinished) {        Text(this.taskName)          .fontSize(16)          .decoration({ type: TextDecorationType.LineThrough })          .fontColor(Color.Gray)      } else {        TextInput({ text: this.taskName })          .fontSize(16)          .onChange((value: string) => {            this.taskName = value; // 修改 @Link 变量，会同步回父组件          })      }
      Button('Delete')        .fontSize(12)        .onClick(() => {          // 触发自定义事件（需父组件传递事件函数，此处简化）        })    }    .width('100%')    .padding(10)    .backgroundColor(Color.White)    .borderRadius(8)  }}
// 父组件：待办列表@Entry@Componentstruct TodoList {  @State tasks: { name: string, finished: boolean }[] = [    { name: 'Learn ArkUI', finished: false },    { name: 'Build a sample app', finished: true },  ];
  build() {    Column({ space: 15 }) {      Text('Todo List')        .fontSize(28)        .fontWeight(FontWeight.Bold)
      ForEach(this.tasks, (item: { name: string, finished: boolean }, index: number) => {        TodoItem({          isFinished: item.finished, // 传递 @Prop          taskName: $rawApp(this.tasks[index].name) // 传递 @Link，使用 $rawApp 或新建对象        })      })
      Button('Add New Task')        .width('80%')        .margin({ top: 20 })        .onClick(() => {          this.tasks.push({ name: 'New Task', finished: false });        })    }    .width('100%')    .height('100%')    .padding(20)    .backgroundColor(Color.LightGray)  }}
```

TypeScript

**关键点**：

-  **@State** ：组件内部私有状态，变化驱动 UI 刷新。

-  **@Prop** ：子组件接收父组件的**单向**数据流。子组件可以修改它，但不会同步回父组件。

-  **@Link** ：子组件接收父组件的**双向**数据流。子组件的修改会同步回父组件的源数据。

-  **@Watch** ：监听装饰变量的变化并执行回调。

-  **$rawApp** （或新建对象）：在  ForEach  中传递  @Link  时，需要确保每个项是独立的响应式对象。

---

### 🎯 **总结**

这些实例涵盖了 ArkUI 的核心概念：

1. **状态管理**（ @State ,  @Prop ,  @Link ）

2. **UI 复用与组合**（ @Builder ,  @BuilderParam ,  @LocalBuilder ）

3. **列表与性能**（ List ,  LazyForEach , 懒加载）

4. **路由与导航**（ Navigation ,  NavPathStack ）

5. **组件生命周期**（ aboutToAppear ,  onPageShow ）

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/a76eeccc3ffb4467a843649e7cd8ec26?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765880769%3B1765909569&q-key-time=1765880769%3B1765909569&q-header-list=&q-url-param-list=&q-signature=b8747cf503ebe61bc9d377a767cbb120da49cfee)

每个实例都基于您提供的文档，并展示了从**组件定义**、**状态绑定**到**交互逻辑**的完整流程。您可以将这些代码片段复制到 DevEco Studio 的 ArkTS 文件中运行和体验。 根据您提供的文档内容，我将为您梳理和总结与**日历提醒、出行、旅游、本地生活、充电**相关的“一次开发，多端部署”（“一多”）最佳实践案例。

### 📋 **筛选原则**

以下所有案例均严格基于您提供的文档内容，确保“回答准确，完整，清晰”。若文档未明确提及，则不予列出。

---

## 📅 **1. 日历提醒相关案例**

文档中直接提及“日历”功能的案例主要出现在商务办公类应用中。

- **文档来源**：《多设备商务办公界面.pdf》、《多设备商务办公界面_a007ece5.pdf》

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/c5fce91501b94a178b26c93f0b243d14?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765881520%3B1765910320&q-key-time=1765881520%3B1765910320&q-header-list=&q-url-param-list=&q-signature=2fd01b339763d34060b6ee741209812f4b7d0fd4)

- **核心场景**：在商务办公应用中，日历是一个典型页面。

- **关键技术与实践**：

- **Navigation组件的单双栏切换**：通过监听断点变化，动态改变  Navigation  组件的  mode  属性，实现在小屏设备（如手机）上使用单栏模式，在大屏设备（如平板、PC）上使用双栏模式，以充分利用屏幕空间展示更多日程信息。

- **实现目标**：提升大屏设备上的信息浏览和操作效率。

---

## 🚗 **2. 出行相关案例**

出行是一个大类，文档中包含了**地图导航**和**打车**两个核心垂类的详细案例。

- **文档来源**：《多设备地图导航界面.pdf》、《多设备地图导航界面_e9e6b279.pdf》

- **核心场景**：首页、路线规划页、导航页、打车页。

- **关键技术与实践**：

- **面板自适应布局**：

- **手机**：使用**底部面板**展示功能入口和搜索结果，减少对地图的遮挡。

- **折叠屏/平板/PC**：使用**侧边面板**，并可支持用户拖拽至左侧或右侧。

- **面板多档位调节**：面板高度支持多个档位滑动调节，适应不同交互需求。

- **响应式搜索结果**：搜索结果列表在面板中档位和高档位时，分别采用  Swiper  和  List  组件实现延伸能力，以适配不同信息密度。

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/d5e5d5fa2d0c41bd869a6e188ed06cd6?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765881520%3B1765910320&q-key-time=1765881520%3B1765910320&q-header-list=&q-url-param-list=&q-signature=38d67266205c5b1a5f22822e82e9909886010e53)

- **导航信息挪移布局**：导航页的当前路径信息和剩余路线信息，利用栅格布局监听断点变化，实现信息块的智能位置调整（挪移布局）。

- **打车页布局**：使用  Row  组件并设置  justifyContent  属性为  SpaceBetween ，让车辆类型和价格信息自适应占满可用空间。

---

## ✈️ **3. 旅游相关案例**

旅游垂类以**旅行订票**应用为典型案例，文档提供了非常详尽的实现方案。

- **文档来源**：《多设备旅行订票界面.pdf》、《多设备旅行订票界面_1f03a5be.pdf》

- **核心场景**：涵盖了**首页、时间选择页、查询车票页、填写购****票信息页、提交订单页、订单信息页、酒店详情页、低价日历页**等11个典型页面。

- **关键技术与实践（部分列举）**：

- **首页**：

- **底部/侧边栏挪移**：使用栅格布局监听断点，在手机等小屏设备上底部显示，在大屏设备上侧边显示。

- **功能入口延伸**：使用  Swiper  组件，并通过在不同断点下设置  displayCount  属性，控制一屏显示的功能入口数量。

- **查询车票页（上滑沉浸）**：通过  Scroll  组件的  onReachStart  和  onWillScroll  属性实现上滑隐藏筛选信息、下滑展示的沉浸式浏览效果。

- **酒店详情页顶部Banner**：

- **手机**：支持上滑展开、下滑收起的动画效果。

- **折叠屏**：使用  Scroll  组件展示小图，点击切换大图。

- **平板**：使用  Swiper  组件实现滑动切换。

- **布局能力广泛应用**：在整个应用中大量使用了**栅格断点能力**、**拉伸能力**（ Blank 组件、 layoutWeight ）、**延伸能力**（ List 组件）、**均分能力**（ Grid 组件）等，实现了一套代码对不同屏幕尺寸的自适应。

---

## 🛒 **4. 本地生活相关案例**

本地生活涵盖了购物、便捷生活等多个场景。

**1. 购物比价**

- **文档来源**：《多设备购物比价界面.pdf》、《多设备购物比价界面_db3cedd6.pdf》

- **核心场景**：首页、商品分类页、商品详情页、商品支付页、咨询客服页、直播间页。

- **关键技术与实践**：

- **商品分类页分栏布局**：提升商品查找效率。

- **商品支付页浅层窗口**：采用半模态窗口进行支付，避免全页面跳转遮挡商品信息。

- **直播间商品信息响应式适配**：根据设备屏幕尺寸，避让直播关键信息进行布局。

- **画中画**：退出直播间时，支持以小窗口形式继续观看直播。

**2. 便捷生活**

- **文档来源**：《最佳实践文档变更说明_2e4bedfb.pdf》（提及新增《多设备便捷生活界面》文档）

- **核心场景**：文档概述中指出，便捷生活类场景主要包括**点餐、观影、看攻略**等。此类场景在宽屏设备上可以让用户拥有更高效和流畅的使用体验。

- **关键实践**：文档指出该主题有独立的“场景案例最佳实践:多设备便捷生活界面”可供参考。

---

## 🔋 **5. 充电相关案例**

文档中有一个非常具体的与“充电”相关的行业实践案例。

- **文档来源**：《汽车类行业实践_c1d8f3ed.pdf》

- **核心场景**：**最优充电站点查找与路径规划**。

- **功能描述**：该案例提供了“最优站点”的技术方案，功能页面路径为： 首页 → 服务 → 最优站点 。页面功能包括：

1. 提供**最优充电站点列表**。

2. 提供从当前位置到选定站点的**路径规划**。

3. 支持按**关键词**（如“坂田街道天安云谷附近”）筛选位置。

4. 支持按**网点类型**筛选（可租借 Rentable 、可归还 Returnable 、全部 All ）。

- **技术关联**：该功能背后调用了名为  SearchPowerBankSta  tionLocal  的标准意图（Intent），这属于 **AI使能** 中的 **意图框架** 应用，系统可以根据用户查询精准分发到该功能。此意图的定义可在《附录：标准意图接入规范_99b87c4a.pdf》中找到。

---

### 🎯 **总结与关联**

您所关注的几个领域，在HarmonyOS应用开发最佳实践中均有覆盖，其核心思想都是利用 **“一次开发，多端部署”** 能力：

1. **工程级一多**：采用清晰的三层架构（数据层、逻辑层、展示层）组织代码。

2. **界面级一多**：综合运用 **响应式布局**（监听栅格断点）和 **自适应布局能力**（拉伸、延伸、均分、挪移、隐藏、折行、缩放），使界面能自动适配手机、折叠屏、平板、PC等不同设备。

3. **功能级一多**：通过 **系统能力（SysCap）** 机制管理功能兼容性，确保应用在支持所需能力的设备上运行。

4. **全场景协同**：基于分布式能力，实现跨设备接续、迁移等体验。

这些案例表明，无论是日历、出行导航、旅行订票、本地生活购物，还是充电找桩，都可以通过上述统一的“一多”开发范式，用一套代码高效地构建出能适配多种设备、提供一致且优质体验的应用。 根据《多设备地图导航界面.pdf》文档内容，该文章详细介绍了地图导航应用在多设备适配和响应式设计中的实现方案。以下是文档中明确提及的**具体代码示例**，我将按照文档中出现的顺序和区域进行整理和说明。

---

### 📍 **1. 首页（地图与面板）**

文档中提供了首页的核心布局和交互代码，展示了如何结合地图、面板和手势。

#### **1.1 地图与面板基础结构**

```
build() {  Stack({ alignContent: Alignment.BottomStart }) {    // 1. 地图区域    MapComponent({      mapOptions: this.mapOption,      mapCallback: this.callback    })    .width('100%')    .height('100%')
    // 2. 面板区域（Column嵌套在Stack中）    Column() {      Row() {        // ... 面板内容      }      .height('26vp')      .width('100%')      .justifyContent(FlexAlign.Center)      .gesture(        PanGesture(this.panOptionHeight)          .onActionUpdate((event?: GestureEvent) => {            if (event) {              let height = this.columnHeight - event.offsetY;              this.tempColumnHeight = height;              if (this.tempColumnHeight < 150) {                this.tempColumnHeight = 150;              }              if (this.tempColumnHeight > this.columnMaxHeight) {                this.tempColumnHeight = this.columnMaxHeight;              }            }          })          .onActionEnd(() => {            if (this.tempColumnHeight > (this.columnMaxHeight - 269) / 2 + 269) {              this.columnHeight = this.columnMaxHeight;              this.isShowBack = false;            } else if (this.tempColumnHeight < (269 - 150) / 2 + 150) {              this.columnHeight = 150;              this.isShowBack = true;            } else {              this.columnHeight = 269;              this.isShowBack = true;            }            this.tempColumnHeight = this.columnHeight;          })      )      // ... 其他面板内容    }    .height('100%')    .width('100%')    .gesture(      PanGesture(this.panOptionPosition)        .onActionUpdate((event?: GestureEvent) => {          if (event) {            let position = this.left + event.offsetX;            this.tempLeft = position;            if (this.tempLeft < 24) {              this.tempLeft = 24;            }            if (this.tempLeft > 350) {              this.tempLeft = 350;            }          }        })        .onActionEnd(() => {          if (this.tempLeft < 200) {            this.left = 24;          } else {            this.left = 350;          }          this.tempLeft = this.left;        })    )  }}
```

TypeScript

**说明**：

- 使用  Stack  组件将  MapComponent （地图）和  Column （面板）叠加。

-  PanGesture  手势用于实现面板的**高度调节**（三个档位）和**左右位置调整**（在宽屏设备上）。

- 通过  this.columnHeight  和  this.left  等状态变量控制面板的响应式行为。

---

### 📍 **2. 路线规划页**

文档中提到了路线规划页的实现思路，但未提供完整的代码块，仅以表格形式描述了各区域的实现方案：

- **输入区域**：通过判断当前面板高度更换按钮及输入区域布局， Row  组件配合  layoutWeight  实现拉伸能力。

- **方案页签**： Tabs  组件实现延伸能力。

- **常去地点信息**： Column  组件实现延伸能力。

- **路线规划结果**： List  组件实现延伸能力，并在不同面板高度时设置  List  的不同方向。

---

### 📍 **3. 导航页**

文档中同样以表格形式描述了导航页的实现方案：

- **当前路径信息**：栅格布局监听断点变化实现挪移布局。

- **剩余路线信息**： Row  组件设置  justifyContent  属性为  SpaceBetween  实现自适应占满。

---

### 📍 **4. 打车页**

文档中描述了打车页的实现方案：

- **车辆信息**： List  组件实现延伸能力。

- **打车操作区域**： Row  组件实现拉伸效果。

---

### 📍 **5. 服务卡片页**

文档中提供了服务卡片页的静态卡片实现代码片段：

```
Column() {  FormLink({    action: 'router',    abilityName: 'EntryAbility',    params: {      message: 'add detail'    }  }) {    Column() {      Row() {        Image($r('app.media.ic_public_input_search'))          .width('15vp')          .margin({ left: '10vp', right: '10vp' })        Text($r('app.string.textInput_holder'))          .fontColor('#99000000')          .width('80%')          .maxLines(1)          .textOverflow({ overflow: TextOverflow.Ellipsis })      }      .borderRadius('22vp')      .width('100%')      .height('44vp')      .backgroundColor('#0d000000')      .margin({ top: '20vp' })
      Row() {        ForEach(FormViewData.FUNCTIONS, (item: FunctionType) => {          Column() {            Image(item.icon)              .width('40vp')              .height('40vp')            Text(item.desc)              .fontSize('12vp')              .padding({ top: '4vp' })          }        }, (item: FunctionType) => item.id.toString())      }      .justifyContent(FlexAlign.SpaceBetween)      .height('60%')      .width('100%')    }    .width('90%')  }}.width('100%')
```

TypeScript

**说明**：

- 使用  FormLink  实现卡片与应用的交互。

- 使用  ForEach  渲染功能入口列表。

- 通过样式设置实现搜索框和功能入口的布局。

---

### 📍 **6. 实况窗页**

文档中提供了实况窗（LiveView）的构建代码示例：

```
private static async buildDefaultView(): Promise<liveViewManager.LiveView> {  return {    id: 0,    event: 'PICK_UP',    liveViewData: {      primary: {        title: 'The driver has taken the order',        content: [          { text: 'distance from you' },          { text: '1 km', textColor: '#FF0A59F7' }        ],        keepTime: 15,        clickAction: await LiveViewController.buildWantAgent(),        layoutData: {          layoutType: 4,          underlineColor: '#00ffffff',          title: 'Deep Space Gray · Question M7',          content: 'Pard 123456',          descPic: 'taxi.png'        }      },      capsule: {        type: 1,        status: 1,        icon: 'navigate.png',        backgroundColor: '#FF0A59F7',        title: '1 km'      }    }  };}
```

TypeScript

**说明**：

- 定义了实况窗的数据结构，包括主视图（ primary ）和胶囊视图（ capsule ）的内容。

- 用于在后台运行时向用户展示打车订单状态等信息。

---

### 📋 **总结**

《多设备地图导航界面.pdf》文档中提供的代码主要集中在：

1. **首页的响应式面板实现**：使用  Stack 、 Column 、 PanGesture  等组件和手势实现面板的多形态交互。

2. **服务卡片的静态布局**：使用  FormLink 、 ForEach  等组件构建八宫格卡片。

3. **实况窗的数据结构定义**：展示了如何构建后台通知的视图数据。

对于**路线规划页、导航页、打车页**等，文档主要描述了各区域的**实现方案和使用的组件能力**（如  Tabs 、 List 、 Row  等），但未提供完整的、可运行的代码块。开发者需要根据文档描述的设计方案和组件用法，自行组合实现具体页面。

> **注意**：以上代码均严格来自文档内容。若文档未提供某页面的完整代码，则无法给出。 根据《汽车类行业实践_c1d8f3ed.pdf》文档内容，关于“最优充电站点查找与路径规划”核心场景，其具体使用的代码主要集中在  **OptimalStation.ets**  页面中，该页面负责地图展示、站点列表和路径规划。以下是文档中提供的核心代码实现：
> 
> ### 📍 **1. 权限配置 (** **module.json5** **)**
> 
> 在  entry/src/main/mod  ule.json5  文件中声明定位权限，这是使用地图服务（Map Kit）和路径规划（navi）的前提。
> 
> ```
> "requestPermissions": [  {    "name": "ohos.permission.LOCATION",    "reason": "$string:EntryAbility_desc",    "usedScene": {      "abilities": ["EntryAbility"],      "when": "always"    }  },  {    "name": "ohos.permission.APPROXIMATELY_LOCATION",    "reason": "$string:EntryAbility_desc",    "usedScene": {      "abilities": ["EntryAbility"],      "when": "always"    }  }]
> ```
> 
> JSON
> 
> ### 📍 **2. 最优站点页面核心代码 (** **OptimalStation.ets** **)**
> 
> 该页面是“首页 -> 服务 -> 最优站点”功能的核心实现，集成了地图展示和路径规划。
> 
> ```
> // features/service/src/main/ets/pages/OptimalStation.etsimport { navi } from '@kit.MapKit';import { BusinessError } from '@kit.BasicServicesKit';
> @Entry@Componentexport struct OptimalStation {  // 地图控制器和配置  private mapController?: map.MapComponentController;  private mapOption?: mapCommon.MapOptions;  private callback?: AsyncCallback<map.MapComponentController>;
>   // 地图初始中心点坐标（示例坐标，可自定义）  private latLng: mapCommon.LatLng = {    latitude: 31.97413747571286,    longitude: 118.77314161376894  };
>   // 页面状态  @State addressString: string = '';  @Consume('pageInfos') pageInfos: NavPathStack;
>   build() {    NavDestination() {      Stack({ alignContent: Alignment.Bottom }) {        // 1. 地图组件        MapComponent({ mapOptions: this.mapOption, mapCallback: this.callback })          .width('100%')          .height('100%')
>         // 2. 底部半模态面板（显示站点列表）        Row() {          SheetTransition({            StationList: Station.getStationList(), // 从本地模型获取站点数据            addressName: this.addressName          })        }        .margin({ bottom: 220 })      }    }    .hideTitleBar(true)    .onReady(() => {      // 地图初始化参数      this.mapOption = {        position: {          target: this.latLng,          zoom: 14        },        zoomControlsEnabled: false,        myLocationControlsEnabled: true      };
>       // 地图初始化回调      this.callback = async (err, mapController) => {        if (!err) {          this.mapController = mapController;          // 启用“我的位置”图层          this.mapController?.setMyLocationEnabled(true);
>           // 监听地图加载完成事件          this.mapController.on("mapLoad", () => {            // 地图加载完成后可执行的操作          });
>           // 监听“我的位置”按钮点击事件          this.mapController.on("myLocationButtonClick", () => {            this.getMyLocation();          });
>           // 初始化获取用户当前位置          this.getMyLocation();        }      };    })  }
>   // 获取用户当前位置的方法  private getMyLocation(): void {    // 此处应调用 Location Kit 获取经纬度，文档中未提供具体实现代码    // 获取到位置后，可调用路径规划接口  }
>   // 路径规划核心方法（调用 navi.getDrivingRoutes）  private async calculateRoute(startPoint: mapCommon.LatLng, endPoint: mapCommon.LatLng): Promise<void> {    let params: navi.DrivingRouteParams = {      origins: [{        latitude: startPoint.latitude,        longitude: startPoint.longitude      }],      destination: {        latitude: endPoint.latitude,        longitude: endPoint.longitude      },      // 可选的途经点（最多5个）      waypoints: [        // { latitude: 31.967236140819114, longitude: 120.27142088866847 },        // ...      ],      language: "zh_CN",      // 其他可选参数，如 avoids（避开策略）、departAt（出发时间）等    };
>     try {      const result: navi.RouteResult = await navi.getDrivingRoutes(params);      console.info('Succeeded in getting driving routes. result is', JSON.stringify(result));      // 处理规划结果：例如在地图上绘制路线（polyline）      this.drawRouteOnMap(result.routes[0](@ref);    } catch (error) {      const err: BusinessError = error as BusinessError;      console.error(`Failed in getting driving routes. Code is ${err.code}, message is ${err.message}`);    }  }
>   // 在地图上绘制路线（示例方法，文档中未提供完整实现）  private drawRouteOnMap(route: navi.Route): void {    // 使用 mapController.addPolyline() 绘制路线    // this.mapController?.addPolyline({    //   points: route.overviewPolyline, // 路线坐标点数组    //   color: '#007AFF',    //   width: 5    // });  }}
> ```
> 
> TypeScript
> 
> ### 📍 **3. 本地站点数据模型 (** **StationModel.ets** **)**
> 
> 文档指出，由于框架示例代码访问API受限，**最优站点列表数据目前来源于本地静态数****据**。开发者可以替换为真实的网络API响应。
> 
> ```
> // features/service/src/main/ets/model/StationModel.etsexport class Station {  static getStationList(): Array<StationInfo> {    // 返回本地模拟的充电站列表数据    return [      {        id: '1',        name: '软件谷万博科技园地库一层充电站',        address: '软件大道附近',        distance: '1.28km',        price: '¥1.15/度起',        type: '直流',        available: '18/20',        latitude: 31.974137,        longitude: 118.773141      },      // ... 更多站点数据    ];  }}
> ```
> 
> TypeScript
> 
> ### 📍 **4. 路径规划接口调用示例（来自其他****相关文档）**
> 
> 虽然《汽车类行业实践_c1d8f3ed.pdf》未提供完整的  getDrivingRoutes  调用示例，但根据同系列的《navi（路径规划）_a1fa7dc6.pdf》和《出行路线规划_2827ac53.pdf》，其标准调用方式如下，可直接应用于最优站点的路径规划：
> 
> ```
> // 驾车路径规划调用示例（可直接集成到 calculateRoute 方法中）let params: navi.DrivingRouteParams = {  origins: [{    latitude: 31.982129213545843,    longitude: 120.27745557768591  }],  destination: {    latitude: 31.983545843,    longitude: 120.27745557768591  },  waypoints: [ // 可选，最多5个途经点    { latitude: 31.967236140819114, longitude: 120.27142088866847 },    { latitude: 31.972868002238872, longitude: 120.2943211817165 }  ],  language: "zh_CN",  avoids: [1, 2], // 可选：避开收费和高速  alternatives: true // 可选：是否返回多条路线（最多3条）};
> const result = await navi.getDrivingRoutes(params);// result.routes 包含规划出的路线数组
> ```
> 
> TypeScript
> 
> ### 📋 **总结：关键实现步骤**
> 
> 1. **配置权限**：在  module.json5  中声明  LOCATION  和  APPROXIMATELY_LOCA  TION  权限。
> 
> 2. **初始化地图**：在页面中使用  MapComponent ，并通过  MapComponentContro  ller  控制地图（如设置中心点、缩放级别、启用定位图层）。
> 
> 3. **获取站点数据**：从本地模型  StationModel.ets  获取充电站列表，并展示在底部面板。
> 
> 4. **路径规划**：当用户选择某个充电站作为目的地时，调用  navi.getDrivingRou  tes()  接口，传入用户当前位置（起点）和站点坐标（终点），获取驾车路线。
> 
> 5. **绘制路线**：使用  mapController.addP  olyline()  将规划出的路线绘制在地图上。
> 
> 6. **（可选）导航体验提升**：文档中提到的“元服务内嵌”创新设计，可在用户未安装导航App时，内嵌导航元服务提供无缝导航体验。
>     
>     ![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/0c306b9b8bbb497884b4d17542f37456?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765881678%3B1765910478&q-key-time=1765881678%3B1765910478&q-header-list=&q-url-param-list=&q-signature=aba9537652762a1a3727d3a46ccb85e321caf027)
>     
> 
> > **注意**：文档中提供的代码是**框架示例代码**，并非完整可运行的应用。开发者需要：
> > 
> > 1. 自行实现  getMyLocation()  方法（使用  @kit.LocationKit ）。
> > 
> > 2. 将本地站点数据  StationModel.ets  替换为真实的网络API请求。
> > 
> > 3. 根据  navi.getDrivingRou  tes()  返回的  RouteResult  数据结构，实现具体的路线绘制逻辑。 根据您提供的《多设备旅行订票界面.pdf》文档内容，其中**明确提及并提供了具体代码示例**的页面和功能如下。对于文档中仅描述实现方案但未提供代码的部分，将不予回答。
> > 
> > ### 📍 **1. 酒店详情页 - 顶部Banne****r实现**
> > 
> > 文档在“酒店详情页”章节的“顶部banner的具体实现”部分，针对不同设备形态，提供了具体的实现代码。
> > 
> > #### **1.1 手机设备（上滑展开/下滑收起****）**
> > 
> > 使用  Scroll  组件的  onReachStart  和  onWillScroll  属性控制图片展开动画。
> > 
> > ```
> > Scroll(this.scroller) {  HotelDetailsPictureView({ topLength: this.topLength })}.scrollBar(BarState.Off).width('100%').height('100%').onReachStart(() => {  if (!this.isInitialization) {    this.topLength = 225;    this.isInitialization = true;  } else {    this.topLength = 460;  }}).onWillScroll((xOffset: number, yOffset: number) => {  if (yOffset > 0) {    this.topLength = 225;  }})
> > ```
> > 
> > TypeScript
> > 
> > #### **1.2 折叠屏设备（小图点击切换大图****）**
> > 
> > 使用  Scroll  和  ForEach  组件，点击小图后通过索引值参数修改大图。
> > 
> > ```
> > Scroll() {  Row() {    ForEach(CommonConstants.HOTEL_PICTURE_MESSAGE, (item: Resource, index: number) => {      Column() {        Image(item)          .width(CommonConstants.THIRTY_PERCENT)          .borderRadius($r('app.float.hotel_grade_border'))          .margin(index === CommonConstants.NUMBER_FOUR ? {} : { right: CommonConstants.FIVE_PERCENT })          .onClick(() => {            this.getMainPicture(index);          })      }    }, (item: Resource) => JSON.stringify(item))  }}
> > ```
> > 
> > TypeScript
> > 
> > #### **1.3 平板设备（Swiper滑动切****换）**
> > 
> > 使用  Swiper  组件实现图片的滑动切换。
> > 
> > ```
> > Swiper() {  ForEach(CommonConstants.HOTEL_PICTURE_MESSAGE, (item: Resource) => {    Image(item)      .width('100%')  }, (item: Resource) => JSON.stringify(item))}.width('40%').height('100%')
> > ```
> > 
> > TypeScript
> > 
> > ### 📍 **2. 低价日历页 - 断点响应逻辑**
> > 
> > 文档在“低价日历”章节提供了一个关键交互逻辑的代码片段，用于根据断点（ breakPoint ）决定是跳转新页面还是显示弹窗。
> > 
> > ```
> > .onClick(() => {  if (this.breakPoint === 'sm') {    this.pageInfos.pushPath(new NavPathInfo('LowPriceCalendarPage', []));  } else {    this.isShowingCalendar = true;  }})
> > ```
> > 
> > TypeScript
> > 
> > **说明**：
> > 
> > - 在  sm （小屏，如手机）断点下，通过路由（ pushPath ）跳转到新的“低价日历页”。
> > 
> > - 在其他大屏（如平板、折叠屏）断点下，通过设置状态变量（ isShowingCalendar   = true ）在当前页面显示日历弹窗。
> > 
> > ### 📋 **总结**
> > 
> > 文档《多设备旅行订票界面.pdf》中**明确提供的具体代码**仅包含以上两部分：
> > 
> > 1. **酒店详情页顶部Banner**在不同设备（手机、折叠屏、平板）上的三种实现方式。
> > 
> > 2. **低价日历页**的交互逻辑，根据屏幕断点决定是页面跳转还是弹窗显示。
> > 
> > 对于文档中其他页面（如首页、查询车票页、提交订单页等）的“实现方案”表格，文档**仅描述了使用的组件和能力**（例如：“使用栅格断点能力”、“使用Tabs组件实现延伸能力”），**并未提供任何具体的ArkTS/Ark****UI代码实现**。因此，无法提供这些页面的具体代码。