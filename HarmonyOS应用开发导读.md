# 应用开发导读

更新时间: 2025-12-16 16:33

应用开发文档用于指导开发者通过HarmonyOS SDK提供的开放能力完成应用开发。在使用应用开发文档前，推荐您通过[知识地图](https://developer.huawei.com/consumer/cn/app/knowledge-map/)了解应用开发完整旅程。

在应用开发的文档中，您可以获取到如下内容。

## 入门

入门可以帮助开发者了解应用开发的基本方法。

通过这一部分内容的学习和初步实践，开发者可以快速构建出首个HarmonyOS应用，掌握应用程序包结构、资源文件的使用以及ArkTS的核心功能和语法等基础知识，为后续的应用开发奠定基础。

## 开发

从HarmonyOS NEXT Developer Preview1（API 11）版本开始，HarmonyOS SDK以Kit维度提供丰富、完备的开放能力，涵盖应用框架、系统、媒体、图形、应用服务、AI六大领域，例如：

- 应用框架相关Kit开放能力：Ability Kit（程序框架服务）、ArkUI（方舟UI框架）等。
- 系统相关Kit开放能力：Universal Keystore Kit（密钥管理服务）、Network Kit（网络服务）等。
- 媒体相关Kit开放能力：Audio Kit（音频服务）、Media Library Kit（媒体文件管理服务）等。
- 图形相关Kit开放能力：ArkGraphics 2D（方舟2D图形服务）、Graphics Accelerate Kit（图形加速服务）等。
- 应用服务相关Kit开放能力：Game Service Kit（游戏服务）、Location Kit（位置服务）等。
- AI相关Kit开放能力：Intents Kit（意图框架服务）、CANN Kit（CANN 服务）等。

我们针对重点开放能力提供了开发指导，助力开发者高效开发。详情请参见“开发”目录下相关内容。

## 工具

DevEco Studio工具是HarmonyOS应用开发的推荐IDE工具。

在[工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-tools-overview)部分，讲解了DevEco Studio工具的详细用法，包括使用该工具进行工程创建、应用签名、应用调试、应用安装运行的指导。

## API参考

API参考提供了HarmonyOS SDK各Kit开放能力的全量组件和接口的说明文档，可以帮助开发者快速查找到指定接口的详细描述和调用方法。详情请参见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/development-intro-api)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/quick-start "快速入门")
# 开发准备

更新时间: 2025-12-16 16:33

本文档适用于HarmonyOS应用开发的初学者。通过构建一个简单的具有页面跳转/返回功能的应用（如下图所示），快速了解工程目录的主要文件，熟悉HarmonyOS应用开发流程。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163345.03323775836728905272029323089442:50001231000000:2800:384A268773B588FA996B277109499EF18032BA578C51F73F27AF53AE249E2F22.png)

在开始之前，您需要了解有关HarmonyOS应用的一些基本概念：UI框架的简单说明、应用模型的基本概念。

## 基本概念

### UI框架

HarmonyOS提供了一套UI开发框架，即方舟开发框架（ArkUI框架）。方舟开发框架可为开发者提供应用UI开发所必需的能力，比如多种组件、布局计算、动画能力、UI交互、绘制等。

方舟开发框架针对不同目的和技术背景的开发者提供了两种开发范式，分别是基于ArkTS的声明式开发范式（简称“声明式开发范式”）和兼容JS的类Web开发范式（简称“类Web开发范式”）。以下是两种开发范式的简单对比。

|**开发范式名称**|**语言生态**|**UI更新方式**|**适用场景**|**适用人群**|
|:--|:--|:--|:--|:--|
|声明式开发范式|ArkTS语言|数据驱动更新|复杂度较大、团队合作度较高的程序|移动系统应用开发人员、系统应用开发人员|
|类Web开发范式|JS语言|数据驱动更新|界面较为简单的程序应用和卡片|Web前端开发人员|

更多UI框架的开发内容及指导，详见[UI开发](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkui-overview)。

### 应用模型

应用模型是HarmonyOS为开发者提供的应用程序所需能力的抽象提炼，它提供了应用程序必备的组件和运行机制。有了应用模型，开发者可以基于一套统一的模型进行应用开发，使应用开发更简单、高效。

随着系统的演进发展，HarmonyOS先后提供了两种应用模型：

- **FA（Feature Ability）模型：** HarmonyOS API 7开始支持的模型，已经不再主推。FA模型开发可见[FA模型开发概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/fa-model-development-overview)。**快速入门章节不再对此展开提供开发指导。**
- **Stage模型：** HarmonyOS API 9开始新增的模型，是目前主推且会长期演进的模型。在该模型中，由于提供了AbilityStage、WindowStage等类作为应用组件和Window窗口的“舞台”，因此称这种应用模型为Stage模型。Stage模型开发可见[Stage模型开发概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/stage-model-development-overview)。**快速入门以此为例提供开发指导。**
    

FA模型和Stage模型的整体架构和设计思想等更多区别，请见[应用模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-models)。

快速入门提供了一个含有两个页面的开发实例，并基于Stage模型构建第一个ArkTS应用，以便开发者理解以上基本概念及应用开发流程。

## 工具准备

请下载并安装[最新版DevEco Studio](https://developer.huawei.com/consumer/cn/download/)，具体可参照[下载与安装DevEco Studio](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-software-install)，更多工具使用指导可见[工具概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-tools-overview)。

完成上述操作及基本概念的理解后，可参照[构建第一个HarmonyOS应用（ArkTS）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/start-with-ets-stage)进行下一步体验和学习。
# 构建第一个HarmonyOS应用（ArkTS）

更新时间: 2025-12-16 16:33

说明

为确保运行效果，本文以使用**[最新DevEco Studio版本](https://developer.huawei.com/consumer/cn/download/)**为例。

## 创建ArkTS工程

1. 若首次打开**DevEco Studio**，请单击**Create Project**创建工程。如果已经打开了一个工程，请在菜单栏选择**File** > **New** > **Create Project**来创建一个新工程。
2. 选择**Application**应用开发（本文以应用开发为例，[Atomic Service](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/glossary#section10825114113817)对应为元服务开发），选择模板**Empty Ability**，单击**Next**进行下一步配置。
    
    若开发者需要进行Native相关工程的开发，请选择**Native C++**模板，更多模板的使用和说明请见[工程模板介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-template)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163348.89411978189246466657829817582701:50001231000000:2800:BEB6C8CC9E2A8EDF90C3104E5E3297FC7E3379C7096E6B7B6260A0C67C837A7B.png "点击放大")
    
3. 进入配置工程界面，**Compatible SDK**表示兼容的最低API Version，此处以选择**6.0.1(21)**为例，其他参数保持默认设置即可。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163348.41947244973225906774965188691702:50001231000000:2800:4A9BCA17CC6750267DE431B74D67DDD71419E6AED3E285FF7FE7141EB3B8AF8F.png "点击放大")
    
4. 单击**Finish**，工具会自动生成示例代码和相关资源，等待工程创建完成。

## ArkTS工程目录结构（Stage模型）

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163349.21933481987271949884137960021389:50001231000000:2800:4FD71F1B695594EE91FBE6DE5BBE937F786DCD98F09536F711D819D1A0E92939.png "点击放大")

- **AppScope > app.json5**：应用的全局配置信息，详见[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)。
- **entry**：HarmonyOS工程模块，编译构建生成一个[HAP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-package-glossary#hap)包。
    
    - **src > main > ets**：用于存放ArkTS源码。
    - **src > main > ets > entryability**：应用/服务的入口。
    - **src > main > ets > entrybackupability**：应用提供扩展的备份恢复能力。
    - **src > main > ets > pages**：应用/服务包含的页面。
    - **src > main > resources**：用于存放应用/服务所用到的资源文件，如图形、多媒体、字符串、布局文件等。关于资源文件，详见[资源分类与访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access)。
    - **src > main > module.json5**：[模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-package-glossary#module)配置文件。主要包含HAP包的配置信息、应用/服务在具体设备上的配置信息以及应用/服务的全局配置信息。具体的配置文件说明，详见[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)。
    - **build-profile.json5**：当前的模块信息 、编译信息配置项，包括buildOption、targets配置等。
    - **hvigorfile.ts**：模块级编译构建任务脚本。
    - **obfuscation-rules.txt**：混淆规则文件。混淆开启后，在使用Release模式进行编译时，会对代码进行编译、混淆及压缩处理，保护代码资产。详见[开启代码混淆](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-build-obfuscation)。
    - **oh-package.json5**：用来描述包名、版本、入口文件（类型声明文件）和依赖项等信息。
    
- **oh_modules**：用于存放三方库依赖信息。
- **build-profile.json5**：工程级配置信息，包括签名signingConfigs、产品配置products等。其中products中可配置当前运行环境，默认为HarmonyOS。
    
- **hvigorfile.ts**：工程级编译构建任务脚本。
    
- **oh-package.json5**：主要用来描述全局配置，如：依赖覆盖（overrides）、依赖关系重写（overrideDependencyMap）和参数化配置（parameterFile）等。

## 构建第一个页面

1. 使用文本组件。
    
    工程同步完成后，在**Project**窗口，单击**entry > src > main > ets > pages**，打开**Index.ets**文件，将页面从RelativeContainer相对布局修改成Row/Column线性布局。
    
    针对本文中使用文本/按钮来实现页面跳转/返回的应用场景，页面均使用[Row](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-row)和[Column](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-column)组件来组建布局。对于更多复杂元素对齐的场景，可选择使用[RelativeContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-relativecontainer)组件进行布局。更多关于UI布局的选择和使用，可见[如何选择布局](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-layout-development-overview#%E5%A6%82%E4%BD%95%E9%80%89%E6%8B%A9%E5%B8%83%E5%B1%80)。
    
    **Index.ets**文件的示例如下：
    
    1. // Index.ets
    2. @Entry
    3. @Component
    4. struct Index {
    5.   @State message: string = 'Hello World';
    
    6.   build() {
    7.     Row() {
    8.       Column() {
    9.         Text(this.message)
    10.           .fontSize(50)
    11.           .fontWeight(FontWeight.Bold)
    12.       }
    13.       .width('100%')
    14.     }
    15.     .height('100%')
    16.   }
    17. }
    
2. 添加按钮。
    
    在默认页面基础上，我们添加一个Button组件，作为按钮响应用户onClick事件，从而实现跳转到另一个页面。**Index.ets**文件的示例如下：
    
    1. // Index.ets
    2. @Entry
    3. @Component
    4. struct Index {
    5.   @State message: string = 'Hello World';
    
    6.   build() {
    7.     Row() {
    8.       Column() {
    9.         Text(this.message)
    10.           .fontSize(50)
    11.           .fontWeight(FontWeight.Bold)
    12.         // 添加按钮，以响应用户onClick事件
    13.         Button() {
    14.           Text('Next')
    15.             .fontSize(30)
    16.             .fontWeight(FontWeight.Bold)
    17.         }
    18.         .type(ButtonType.Capsule)
    19.         .margin({
    20.           top: 20
    21.         })
    22.         .backgroundColor('#0D9FFB')
    23.         .width('40%')
    24.         .height('5%')
    25.       }
    26.       .width('100%')
    27.     }
    28.     .height('100%')
    29.   }
    30. }
    
3. 在编辑窗口**右上角**的侧边工具栏，单击**Previewer**，打开预览器。第一个页面效果如下图所示：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163349.88395447096248223532528894066077:50001231000000:2800:EF805FC3B1DF9F666B442186E2CA79B43E2746D56795968E64D746B114B12728.png)
    

## 构建第二个页面

1. 创建第二个页面。
    
    - 新建第二个页面文件。在**Project**窗口，打开**entry > src > main > ets**，右键单击**pages**文件夹，选择**New > ArkTS File**，命名为**Second**，单击**回车键**。可以看到文件目录结构如下：
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163349.43653373092515830257163375699101:50001231000000:2800:81C2D14D97912DDA4073414B8F6360BBC55D1857353DF48CA0BF9F11145FFA1C.png)
        
        说明
        
        开发者也可以在右键单击**pages**文件夹时，选择**New > Page** **> Empty Page**，命名为**Second**，单击**Finish**完成第二个页面的创建。使用此种方式则无需再进行下文中第二个页面路由的手动配置。
        
    - 配置第二个页面的路由。在**Project**窗口，打开**entry > src > main > resources > base > profile**，在main_pages.json文件中的"src"下配置第二个页面的路由"pages/Second"。示例如下：
        
        1. {
        2.   "src": [
        3.     "pages/Index",
        4.     "pages/Second"
        5.   ]
        6. }
        
    
2. 添加文本及按钮。
    
    参照第一个页面，在第二个页面添加Text组件、Button组件等，并设置其样式。**Second.ets**文件的示例如下：
    
    1. // Second.ets
    2. @Entry
    3. @Component
    4. struct Second {
    5.   @State message: string = 'Hi there';
    
    6.   build() {
    7.     Row() {
    8.       Column() {
    9.         Text(this.message)
    10.           .fontSize(50)
    11.           .fontWeight(FontWeight.Bold)
    12.         Button() {
    13.           Text('Back')
    14.             .fontSize(30)
    15.             .fontWeight(FontWeight.Bold)
    16.         }
    17.         .type(ButtonType.Capsule)
    18.         .margin({
    19.           top: 20
    20.         })
    21.         .backgroundColor('#0D9FFB')
    22.         .width('40%')
    23.         .height('5%')
    24.       }
    25.       .width('100%')
    26.     }
    27.     .height('100%')
    28.   }
    29. }
    

## 实现页面间的跳转

页面间的导航可以通过[页面路由router](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-router)来实现。页面路由router根据页面url找到目标页面，从而实现跳转。使用页面路由请导入router模块。

如果需要实现更好的转场动效，推荐使用[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation)。

1. 第一个页面跳转到第二个页面。
    
    在第一个页面中，跳转按钮绑定onClick事件，单击按钮时跳转到第二页。**Index.ets**文件的示例如下：
    
    1. // Index.ets
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
    3. @Entry
    4. @Component
    5. struct Index {
    6.   @State message: string = 'Hello World';
    
    7.   build() {
    8.     Row() {
    9.       Column() {
    10.         Text(this.message)
    11.           .fontSize(50)
    12.           .fontWeight(FontWeight.Bold)
    13.         // 添加按钮，以响应用户onClick事件
    14.         Button() {
    15.           Text('Next')
    16.             .fontSize(30)
    17.             .fontWeight(FontWeight.Bold)
    18.         }
    19.         .type(ButtonType.Capsule)
    20.         .margin({
    21.           top: 20
    22.         })
    23.         .backgroundColor('#0D9FFB')
    24.         .width('40%')
    25.         .height('5%')
    26.         // 跳转按钮绑定onClick事件，单击时跳转到第二页
    27.         .onClick(() => {
    28.           console.info(`Succeeded in clicking the 'Next' button.`)
    29.           // 获取UIContext
    30.           let uiContext: UIContext = this.getUIContext();
    31.           let router = uiContext.getRouter();
    32.           // 跳转到第二页
    33.           router.pushUrl({ url: 'pages/Second' }).then(() => {
    34.             console.info('Succeeded in jumping to the second page.')
    
    35.           }).catch((err: BusinessError) => {
    36.             console.error(`Failed to jump to the second page. Code is ${err.code}, message is ${err.message}`)
    37.           })
    38.         })
    39.       }
    40.       .width('100%')
    41.     }
    42.     .height('100%')
    43.   }
    44. }
    
2. 第二个页面返回到第一个页面。
    
    在第二个页面中，返回按钮绑定onClick事件，单击按钮时返回到第一页。**Second.ets**文件的示例如下：
    
    1. // Second.ets
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
    3. @Entry
    4. @Component
    5. struct Second {
    6.   @State message: string = 'Hi there';
    
    7.   build() {
    8.     Row() {
    9.       Column() {
    10.         Text(this.message)
    11.           .fontSize(50)
    12.           .fontWeight(FontWeight.Bold)
    13.         Button() {
    14.           Text('Back')
    15.             .fontSize(30)
    16.             .fontWeight(FontWeight.Bold)
    17.         }
    18.         .type(ButtonType.Capsule)
    19.         .margin({
    20.           top: 20
    21.         })
    22.         .backgroundColor('#0D9FFB')
    23.         .width('40%')
    24.         .height('5%')
    25.         // 返回按钮绑定onClick事件，单击按钮时返回到第一页
    26.         .onClick(() => {
    27.           console.info(`Succeeded in clicking the 'Back' button.`)
    28.           // 获取UIContext
    29.           let uiContext: UIContext = this.getUIContext();
    30.           let router = uiContext.getRouter();
    31.           try {
    32.             // 返回第一页
    33.             router.back()
    34.             console.info('Succeeded in returning to the first page.')
    35.           } catch (err) {
    36.             let code = (err as BusinessError).code; 
    37.             let message = (err as BusinessError).message; 
    38.             console.error(`Failed to return to the first page. Code is ${code}, message is ${message}`)
    39.           }
    40.         })
    41.       }
    42.       .width('100%')
    43.     }
    44.     .height('100%')
    45.   }
    46. }
    
3. 打开**Index.ets**文件，单击预览器中的![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163350.07284834173178165568583324633229:50001231000000:2800:1F2A734785C72D250E5D7E0C13BD7D311C38ACC5BDEE54B49F6A847E2326069D.png)按钮进行刷新。效果如下图所示：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163351.72826992680999953784241523743139:50001231000000:2800:A56B84A2C232DA6F36893BE62F23E302F6674AA1674CF9F8EE8A6BD6A13EC2D7.png)
    

## 使用真机运行应用

1. 将搭载HarmonyOS系统的真机与电脑连接。具体指导及要求，可查看[使用本地真机运行应用/服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-run-device)。
2. 进入**File > Project Structure... > Project > Signing Configs**界面，勾选“**Automatically generate signature**”，即可完成签名。如果未登录，请先单击**Sign In**进行登录，然后自动完成签名。具体请见[配置调试签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section151231211105010)。如下图所示：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163352.51024390051632793442162882556213:50001231000000:2800:DA06305ECE4A97FEEDB91F6B6CCE7D8DB56D8CD4A219032E972C696405741D11.png "点击放大")
    
3. 在编辑窗口右上角的工具栏，单击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163353.46406463707483020988353267194864:50001231000000:2800:84607F7FDAC2FBF7B983B0E1EAC886DB986367427C72D294AA0DE1B2D699F6AC.png)按钮运行。效果如下图所示：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163354.55889307613776296971370051643990:50001231000000:2800:01E4414E4378FC8A8F53CC4D0E6DD4616CAA8E978B73F1DEAD30E63DF212D4E7.png "点击放大")
    

恭喜您已经基于ArkTS语言构建完成第一个HarmonyOS应用，快来探索更多的HarmonyOS功能吧。

## 相关课程

- [HarmonyOS第一课](https://developer.huawei.com/consumer/cn/training/study-path/101667550095504391)
- [开发入门：Hello World](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_Next-HelloWorld)
- # 应用程序包概述

更新时间: 2025-12-16 16:34

在基于[Stage模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-configuration-file-overview-stage)开发应用之前，开发者需要了解应用的设计机制、应用程序包结构等基础知识。

## 应用与应用程序包

用户应用程序是指运行在设备操作系统之上，为用户提供特定服务的程序，简称“应用”。一个应用所对应的软件包文件，称为“应用程序包”。

系统提供了应用程序包开发、安装、查询、更新、卸载的管理机制，便于开发者开发和管理应用。此外，系统还屏蔽了不同的芯片平台的差异（包括x86/ARM，32位/64位等），保证应用程序包在不同的芯片平台都能够安装运行，使得开发者可以聚焦于应用的功能实现。

## 应用的多Module设计机制

- **支持模块化开发：** 一个应用通常包含多种功能，将不同的功能特性按模块来划分和管理是一种良好的设计方式。在开发过程中，开发者可以将每个功能模块作为一个独立的Module进行开发，Module中可以包含源代码、资源文件、第三方库、配置文件等，每一个Module可以独立编译，实现特定的功能。这种模块化、松耦合的应用管理方式有利于应用的开发、维护与扩展。
    
- **支持多设备适配：** 一个应用往往需要适配多种设备类型，在采用多Module设计的应用中，每个Module都会标注所支持的设备类型。Module支持的设备类型不同，有的支持全部类型，有的仅支持特定类型（例如平板）。在应用市场分发应用包时，可以根据设备类型进行精准筛选和匹配，从而合理组合和部署不同的包到对应的设备上。
    

## Module类型

Module按照使用场景可以分为两种类型：

- **Ability类型的Module：** 用于实现应用的功能和特性。每一个Ability类型的Module编译后，会生成一个以.hap为后缀的文件，称为HAP（Harmony Ability Package）包。HAP包可以独立安装和运行，是应用安装的基本单位，一个应用可以包含一个或多个HAP包，包含的HAP包分为以下两种类型。
    
    - entry类型的Module：应用的主模块，包含应用的入口界面、入口图标和主功能特性，编译后生成entry类型的HAP。每一个应用分发到同一类型的设备上的应用程序包，只能包含唯一一个entry类型的HAP，也可以不包含。
    - feature类型的Module：应用的动态特性模块，编译后生成feature类型的HAP。一个应用中可以包含一个或多个feature类型的HAP，也可以不包含。
- **Library类型的Module：** 用于实现代码和资源的共享。同一个Library类型的Module可以被其他的Module多次引用，合理地使用该类型的Module，能够降低开发和维护成本。Library类型的Module分为Static和Shared两种类型，编译后生成共享包。
    
    - Static Library：静态共享库。编译后生成一个以.har为后缀的文件，即静态共享包HAR（Harmony Archive）。
    - Shared Library：动态共享库。编译后生成一个以.hsp为后缀的文件，即动态共享包HSP（Harmony Shared Package）。
    
    说明
    
    实际上，Shared Library编译后除了会生成一个.hsp文件，还会生成一个.har文件。这个.har文件中包含了HSP对外导出的接口，应用中的其他模块需要通过.har文件来引用HSP的功能。为了表述方便，通常认为编译Shared Library后会生成HSP。
    
    HAR与HSP两种共享包的主要区别体现在：
    
    |共享包类型|编译和运行方式|发布和引用方式|
    |:--|:--|:--|
    |HAR|HAR中的代码和资源跟随使用方编译，如果有多个使用方，它们的编译产物中会存在多份相同拷贝。<br><br>注意：[编译HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/har-package#%E7%BC%96%E8%AF%91)时，建议开启混淆能力，保护代码资产。|HAR除了支持应用内引用，还可以独立打包发布到[OHPM中心仓](https://ohpm.openharmony.cn/#/cn/home)或者[OHPM私仓](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo)，供其他应用引用。|
    |HSP|HSP中的代码和资源可以独立编译，运行时在一个进程中代码也只会存在一份。|HSP一般随应用进行打包，当前支持应用内和[集成态HSP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/integrated-hsp)。应用内HSP只支持应用内引用，集成态HSP支持发布到OHPM私仓和跨应用引用。<br><br>**说明：**<br><br>集成态HSP只是应用内HSP的中间形态，只能参与编译构建过程，无法单独安装。在构建和发布OHPM私仓的过程中，集成态HSP不与特定的应用包名耦合。使用时，工具链支持自动将集成态HSP的包名替换成宿主应用包名，并且会重新签名生成一个新的HSP包，作为宿主应用的安装包，这个新的HSP也属于宿主应用HAP的应用内HSP。|
    
    **图1** HAR和HSP在APP包中的形态示意图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163402.72894675038488182380229254868462:50001231000000:2800:176830D4AEA225F16D5C1FE36C361CF0969F5B294C67EEFBDCD60526EC0482BA.png)
    

## 选择合适的包类型

HAP、HAR、HSP三者的功能和使用场景总结对比如下：

|Module类型|包类型|说明|
|:--|:--|:--|
|Ability|[HAP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hap-package)|应用的功能模块，可以独立安装和运行。|
|Static Library|[HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/har-package)|静态共享包，编译态复用。<br><br>- 支持应用内共享，也可以作为二方库（SDK）、三方库（SDK）发布后供其他应用使用。<br><br>- 作为二方库（SDK），发布到[OHPM私仓](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo)，供公司内部其他应用使用。<br><br>- 作为三方库（SDK），发布到[OHPM中心仓](https://ohpm.openharmony.cn/#/cn/home)，供其他应用使用。<br><br>- 多包（HAP/HSP）同时引用相同的HAR时，会造成多包间代码和资源的重复拷贝，从而导致应用包增大。<br><br>- 注意：[编译HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/har-package#%E7%BC%96%E8%AF%91)时，建议开启混淆能力，保护代码资产。|
|Shared Library|[HSP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/in-app-hsp)|动态共享包，运行时复用。<br><br>- 当多包（HAP/HSP）同时依赖同一个共享包时，使用HSP替代HAR，可以避免HAR造成的多包间代码和资源的重复拷贝，从而减小应用包大小。|

HAP、HSP、HAR支持的规格对比如下，其中“√”表示是，“×”表示否。

开发者可以根据具体的应用需求，选择相应类型的包进行开发。在后续的章节中还会针对如何使用[HAP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hap-package)、[HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/har-package)、[HSP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/in-app-hsp)分别展开详细介绍。

|规格|HAP|HAR|HSP|
|:--|:--|:--|:--|
|支持在配置文件中声明[UIAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uiability-overview)组件|√|√|√|
|支持在配置文件中声明[ExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/extensionability-overview)组件|√|√|√|
|支持在配置文件中声明[pages](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#pages%E6%A0%87%E7%AD%BE)页面|√|×|√|
|支持包含资源文件与.so文件|√|√|√|
|支持依赖其他HAR文件|√|√|√|
|支持依赖其他HSP文件|√|√|√|
|支持在设备上独立安装运行|√|×|×|

说明

- 如果HAR支持声明pages页面，那么当HAR被打包到HAP或HSP中时，其内部声明的pages页面可能会与HAP/HSP中的pages页面存在相对路径上的重复，这将导致无法根据相对路径识别特定的路由页面。因此，HAR不支持在配置文件中声明pages页面，但可以包含pages页面，并通过[Navigation跳转](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E8%B7%AF%E7%94%B1%E6%93%8D%E4%BD%9C)的方式进行跳转。
- 由于HSP仅支持应用内共享，如果HAR依赖了HSP，则该HAR文件仅支持应用内共享，不支持发布到二方仓或三方仓供其他应用使用，否则会导致编译失败。
- HAR和HSP均不支持循环依赖，也不支持依赖传递，详情说明可以参考[HAR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/har-package#%E7%BA%A6%E6%9D%9F%E9%99%90%E5%88%B6)或者[HSP](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/in-app-hsp#%E7%BA%A6%E6%9D%9F%E9%99%90%E5%88%B6)中约束限制说明。
- # Stage模型应用程序包结构

更新时间: 2025-12-16 16:34

为了让开发者能对应用程序包在不同阶段的形态有更加清晰的认知，分别对开发态、编译态、发布态的应用程序结构展开介绍。

## 开发态包结构

在DevEco Studio上创建项目工程，并尝试创建多个不同类型的Module。根据实际工程中的目录对照本章节进行学习，可以有助于理解开发态的应用程序结构。

**图1** 项目工程结构示意图（以实际为准）

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163420.23670159295271570493213133031335:50001231000000:2800:EDFB3528EA767F305612CA89B87A169C31A9466D7441D6566A391632D67DEC71.png)

说明

- AppScope目录由DevEco Studio自动生成，该目录名称更改会导致当前目录下配置文件和资源加载不到，导致编译报错问题，因此该目录名称请勿修改。
- Module目录名称可以由DevEco Studio自动生成（比如entry、library等），也可以自定义。为了便于说明，下表中统一采用ModuleName表示。

工程结构主要包含的文件类型及用途如下：

|文件类型|说明|
|:--|:--|
|配置文件|包括应用级配置信息、以及Module级配置信息：<br><br>- **AppScope > app.json5**：[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)，用于声明应用的全局配置信息，比如应用Bundle名称、应用名称、应用图标、应用版本号等。<br><br>- **ModuleName > src > main > module.json5**：[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)，用于声明Module基本信息、支持的设备类型、所含的组件信息、运行所需申请的权限等。|
|ArkTS源码文件|**ModuleName > src > main > ets**：用于存放Module的ArkTS源码文件（.ets文件）。|
|资源文件|包括应用级资源文件、以及Module级资源文件，支持图形、多媒体、字符串、布局文件等，详见[资源分类与访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access)。<br><br>- **AppScope > resources** ：用于存放应用需要用到的资源文件。<br><br>- **ModuleName > src > main > resources** ：用于存放该Module需要用到的资源文件。|
|其他配置文件|用于编译构建，包括构建配置文件、编译构建任务脚本、混淆规则文件、依赖的共享包信息等。<br><br>- **build-profile.json5**：[工程级](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app)或[Module级](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile)的构建配置文件，包括[应用签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing)、产品配置等。<br><br>- **hvigorfile.ts**：工程级或Module级的编译构建任务脚本，开发者可以自定义编译构建工具版本、控制构建行为的配置参数。<br><br>- **[obfuscation-rules.txt](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-build-obfuscation#section760533133313)**：混淆规则文件。混淆开启后，在使用Release模式进行编译时，会对代码进行编译、混淆及压缩处理，保护代码资产。<br><br>- **[oh-package.json5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-oh-package-json5)**：用于存放依赖库的信息，包括所依赖的三方库和共享包。|

## 编译态包结构

不同类型的Module编译后会生成对应的HAP、HAR、HSP等文件，编译后可通过DevEco Studio或打包工具打包成APP包，用于上架应用市场。编译HAP和HSP时，会把它们所依赖的HAR直接编译到HAP和HSP中，因此打包成APP包后，编译打包视图中只有.hap和.hsp文件，没有.har文件。开发态视图与编译态视图的对照关系如下：

**图2** 开发态与编译态的工程结构视图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163421.05289072395347782668695512531854:50001231000000:2800:44432256D403429DCE202303EF8FBC963D44424E562A148D63238C67C903F6E1.png)

从开发态到编译态，Module文件变更如下：

- **ets目录**：ArkTS源码编译生成.abc文件。
- **resources目录**：AppScope目录下的资源文件会合入到Module下面资源目录中，如果两个目录下存在重名文件，编译打包后只会保留AppScope目录下的资源文件。
- **module配置文件**：AppScope目录下的app.json5文件字段会合入到Module下面的module.json5文件之中，编译后生成HAP或HSP最终的module.json文件。

## 发布态包结构

每个应用中至少包含一个.hap文件，可能包含若干个.hsp文件、也可能不含，一个应用中的所有.hap与.hsp文件合在一起称为**Bundle**，其对应的bundleName是应用的唯一标识（详见[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中的bundleName标签）。

当应用发布上架到应用市场时，需要将Bundle打包为一个.app后缀的文件用于上架，这个.app文件称为**App Pack**（Application Package），与此同时，DevEco Studio工具会自动生成一个**pack.info**文件。**pack.info**文件描述了App Pack中每个HAP和HSP的属性，包含APP中的bundleName和versionCode信息、以及Module中的name、type和abilities等信息。

说明

- App Pack是发布上架到应用市场的基本单元，但是不能在设备上直接安装和运行。
- 在[应用签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing)、云端分发、端侧安装时，都是以HAP/HSP为单位进行签名、分发和安装的。

**图3** 编译发布与上架部署流程图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163423.33962965173820106515942551015910:50001231000000:2800:94EDDC3D5CCE5772871163D8EF2719F287169141C5EEF14CFBDE836EC7914506.png)
# FA模型应用程序包结构

更新时间: 2025-12-16 16:34

基于[FA模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-configuration-file-overview-fa)开发的应用，其应用程序包结构如下图应用程序包结构（FA模型）所示。开发者需要熟悉应用程序包结构相关的基本概念。

说明

API version 8及更早的版本支持的应用模型，FA模型已经不再主推。建议使用新的Stage模型进行开发。

FA模型与Stage模型的主要区别在于HAP内部文件的存放位置不同。FA模型中，所有资源文件、库文件和代码文件都存放在assets文件夹中，并在文件夹内部进一步区分。

- config.json是应用配置文件，DevEco Studio会自动生成部分模块代码，开发者按需修改其中的配置。详细字段请参见[应用配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-configuration-file-overview-fa#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E7%9A%84%E5%86%85%E9%83%A8%E7%BB%93%E6%9E%84)。
    
- assets是HAP所有的资源文件、库文件和代码文件的集合，内部可以分为entry和js文件夹。entry文件夹中存放的是resources目录和resources.index文件。
    
- resources目录用于存放应用的资源文件（字符串、图片等），便于开发者使用和维护，详见[资源文件的使用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access)。
    
- resources.index是资源索引表，由DevEco Studio调用SDK工具生成。
    
- js文件夹中存放的是编译后的代码文件。
    
- pack.info 是 Bundle 中用于描述每个 HAP 属性的文件，包含应用的 bundleName 和 versionCode 信息、模块的 name、type 和 abilities 等信息。该文件由 DevEco Studio 工具在构建 Bundle 包时自动生成。
    

**图1** 应用程序包结构（FA模型）

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163425.31223305750495401512006278686627:50001231000000:2800:BB74C88D3CB6DE92D842415E7312A7CC4978B02E9723AB4DAD2442290E18B903.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-package-structure-stage "Stage模型应用程序包结构")
# HAP

更新时间: 2025-12-16 16:34

HAP（Harmony Ability Package）是应用安装和运行的基本单元。HAP包是由代码、资源、第三方库、配置文件等打包生成的模块包，其主要分为两种类型：entry和feature。

- entry：应用的主模块，作为应用的入口，提供了应用的基础功能。
- feature：应用的动态特性模块，作为应用能力的扩展，可以根据用户的需求和设备类型进行选择性安装。

应用程序包可以只包含一个基础的entry包，也可以包含一个基础的entry包和多个功能性的feature包。

## 使用场景

- 单HAP场景：如果只包含UIAbility组件，无需使用ExtensionAbility组件，优先采用单HAP（即一个entry包）来实现应用开发。虽然一个HAP中可以包含一个或多个UIAbility组件，为了避免不必要的资源加载，推荐采用“一个UIAbility+多个页面”的方式。
    
- 多HAP场景：如果应用的功能比较复杂，需要使用ExtensionAbility组件，可以采用多HAP（即一个entry包+多个feature包）来实现应用开发，每个HAP中包含一个UIAbility组件或者一个ExtensionAbility组件。在这种场景下，多个HAP引用相同的库文件，可能导致重复打包的问题。
    

## 约束限制

- 不支持导出接口和ArkUI组件，给其他模块使用。
    
- 多HAP场景下，App Pack包中同一设备类型的所有HAP中最多只能包含一个Entry类型的HAP，也可以不包含；可以包含一个或者多个Feature类型的HAP，也可以不包含。
    
- 多HAP场景下，在安装或更新时，存在一致性校验，详情参考[应用安装与更新一致性校验](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/odule_installation_update_consistency_verification)。使用打包工具进行打包成APP时，也会进行合法性校验，详情请参考[打包工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/packing-tool#app%E6%89%93%E5%8C%85%E6%8C%87%E4%BB%A4)。
    
- 多HAP场景下，同一应用的所有HAP、HSP的签名证书要保持一致。上架应用市场是以App Pack形式上架，应用市场分发时会将所有HAP从App Pack中拆分出来，同时对所有HAP进行重签名，以保证签名证书的一致性。在调试阶段，开发者通过命令行或DevEco Studio将HAP安装到设备上时，要保证所有HAP签名证书一致，否则会出现安装失败的问题，签名操作请参考[应用/元服务签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing)。
    

## 创建

下面简要介绍如何通过DevEco Studio新建一个HAP模块。

1. 创建工程，构建第一个ArkTS应用。
    
2. 在工程目录上单击右键，选择**New > Module**。
    
3. 在弹出的对话框中选择**Empty Ability**模板，单击**Next**。
    
4. 在Module配置界面，配置**Module name**，选择**Module Type**和**Device Type**，然后单击**Next**。
    
5. 在Ability配置界面，配置**Ability name**，然后单击**Finish**完成创建。
    

## 开发

- HAP中支持添加UIAbility组件或ExtensionAbility组件，以及pages页面。具体操作可参考[在模块中添加Ability](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-add-new-ability)和[添加Page](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-add-page)。
    
- HAP中支持引用HAR或HSP共享包，详见[HAR的使用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/har-package#%E4%BD%BF%E7%94%A8)、[HSP的使用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/in-app-hsp#%E4%BD%BF%E7%94%A8)。
    

## 调试

通过DevEco Studio编译打包，生成单个或者多个HAP，即可基于HAP进行调试。如需根据不同的部署环境、目标人群、运行环境等，将同一个HAP定制编译为不同版本，请参见[定制编译指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-customized-multi-targets-and-products-guides#section1011341611469)。

开发者可以使用DevEco Studio或者hdc工具进行调试：

- **方法一：** 使用DevEco Studio进行调试，详见[应用程序包调试方法](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-run-debug-configurations)。
    
- **方法二：** 使用[hdc工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hdc)进行调试。
    
    在调试前，需要先安装或更新HAP，此处有两种方式：
    
    - 直接使用hdc安装、更新HAP。
        
        HAP的路径为开发平台上的文件路径，以Windows开发平台为例，命令参考如下：
        
        1. # 安装、更新，多HAP可以指定多个文件路径
        2. hdc install entry.hap feature.hap
        3. # 执行结果
        4. install bundle successfully.
        5. # 卸载
        6. hdc uninstall com.example.myapplication
        7. # 执行结果
        8. uninstall bundle successfully.
        
    - 先执行hdc shell，再使用bm工具安装、更新HAP。
        
        HAP的文件路径为真机上的文件路径，命令参考如下：
        
        1. # 先执行hdc shell才能使用bm工具
        2. hdc shell
        3. # 安装、更新，多HAP可以指定多个文件路径
        4. bm install -p /data/app/entry.hap /data/app/feature.hap
        5. # 执行结果
        6. install bundle successfully.
        7. # 卸载
        8. bm uninstall -n com.example.myapplication
        9. # 执行结果
        10. uninstall bundle successfully.
        
    
    完成HAP安装或更新后，即可参考相关调试命令进行[调试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/aa-tool#%E8%BF%9B%E5%85%A5%E8%B0%83%E8%AF%95%E6%A8%A1%E5%BC%8F%E5%91%BD%E4%BB%A4attach)。
    

## 示例代码

- [多HAP](https://gitcode.com/HarmonyOS_Samples/multi-hap)
- # 应用安装卸载与更新开发指导

更新时间: 2025-12-16 16:34

本章节介绍应用程序包的安装卸载流程和两种更新方式。

## 应用程序包的安装卸载

开发者可以通过调试命令安装和卸载应用，安装应用命令参考bm工具中的[install](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/bm-tool#%E5%AE%89%E8%A3%85%E5%91%BD%E4%BB%A4install)，卸载应用命令参考bm工具中的[uninstall](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/bm-tool#%E5%8D%B8%E8%BD%BD%E5%91%BD%E4%BB%A4uninstall)，详情参考[编译发布与上架部署流程图](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-package-structure-stage#%E5%8F%91%E5%B8%83%E6%80%81%E5%8C%85%E7%BB%93%E6%9E%84)。

**图1** 应用程序包安装和卸载流程（开发者）

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163423.00188063485510315871058221593107:50001231000000:2800:7D592DD8B4C1D2D204A78F634AA123D1ED1D7DD87AD8A9B48DEDA659896C7017.png)

应用上架应用市场后，终端设备用户可在设备上通过应用市场安装应用。

**图2** 应用程序包安装和卸载流程（终端设备用户）

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163424.23959145523593898829294147499958:50001231000000:2800:7222CA13382A118EFE9360DE098F833158D8BD1F9763B9E3B0460525C7296D15.png)

## 应用程序包的更新

对于开发者，应用程序包的更新，首先需要更新[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中的versionCode版本号字段，通过DevEco Studio打包后在应用市场发布，发布流程与首次发布一致。对于终端设备用户，新版本发布后，可以通过以下两种方式更新应用程序包。

- 应用市场内更新：应用市场通知用户该应用有新版本，用户根据通知到应用市场（客户端）进行升级。
- 应用内检测升级：开发者根据[更新指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/store-update#section316371715233)实现版本更新提醒功能，应用启动完成或用户在应用中主动检查新版本时，会弹出升级对话框，用户根据对话框提示升级。
- # 应用安装与更新一致性校验

更新时间: 2025-12-16 16:34

随着应用发展越来越复杂，应用也被拆成多个模块进行开发维护，不同的团队负责单个或者多个模块，应用在安装更新过程中会针对不同的字段进行一致性校验和验证，保证应用的安全合法性。本文介绍多模块安装或更新时，签名证书、配置文件的一致性校验规则。

说明

[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中versionCode字段一致，表示安装或更新包同版本，否则为不同版本。

使用打包工具进行打包时，会进行合法性校验。详情请参考[打包工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/packing-tool)。

## 签名证书一致性校验

|字段名称|说明|安装一致性校验规则|更新一致性校验规则|
|:--|:--|:--|:--|
|appId|应用的appId，表示应用的唯一标识，详情信息可参考[什么是appId](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/common_problem_of_application#%E4%BB%80%E4%B9%88%E6%98%AFappid)。|是|appId和appIdentifier任一相同即可。|
|appIdentifier|应用的唯一标识。详情信息可参考[什么是appIdentifier](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/common_problem_of_application#%E4%BB%80%E4%B9%88%E6%98%AFappidentifier)。|是|appId和appIdentifier任一相同即可。|
|appDistributionType|应用[Profile文件](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-profile-0000002248341090)中的类型，标识应用的发布上架类型，如类型为[企业MDM应用发布](https://developer.huawei.com/consumer/cn/doc/app/agc-help-enterprise-mdm-profile-0000002248341094)。|是|更新不同版本时无校验，同版本有校验。|
|appProvisionType|应用签名证书类型。[Profile签名文件](https://developer.huawei.com/consumer/cn/doc/app/agc-help-profile-overview-0000002283260125)的类型，分为debug和release。debug为本地调试使用，release为上架应用市场使用。|是|更新不同版本时无校验，同版本有校验。|
|apl|表示应用程序的[APL等级](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-permission-mgmt-overview#%E6%9D%83%E9%99%90%E6%9C%BA%E5%88%B6%E4%B8%AD%E7%9A%84%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5)，系统定义的apl包括：normal、system_basic和system_core。|是|更新不同版本时无校验，同版本有校验。|

## 配置文件一致性校验

|字段名称|说明|安装一致性校验规则|更新一致性校验规则|
|:--|:--|:--|:--|
|bundleName|标识应用名称。该字段来源于[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中的bundleName字段。|是|是|
|versionCode|标识应用版本号。该字段来源于[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中的versionCode字段。|是|是|
|apiReleaseType|标识应用运行需要的API目标版本的类型。设备中未安装该应用，该应用包含多个模块包，模块一个一个安装时，不检验一致性。该字段来源于[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中的apiReleaseType字段。|否|是|
|targetBundleName|标识当前包所指定的目标应用，配置该字段的应用为具有overlay特征的应用。该字段来源[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中targetBundleName字段。|是|是|
|targetPriority|标识当前应用的优先级。该字段来源于[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中的targetPriority字段。|是|是|
|bundleType|标识应用的类型。该字段来源于[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中的bundleType字段。|是|是|
|installationFree|标识是否支持免安装。该字段来源于[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中的installationFree字段。|是|是|
|debug|标识应用是否可调试。该字段来源于[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中的debug字段。|是|否|
|moduleType|标识模块的类型。该字段来源于[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中的type字段。|是，同版本entry类型的moduleName不能修改|是|
# 应用配置文件概述（Stage模型）

更新时间: 2025-12-16 16:34

每个应用项目的代码目录下必须包含应用配置文件，这些配置文件会向编译工具、操作系统和应用市场提供应用的基本信息。

在基于Stage模型开发的应用项目代码下，都存在一个app.json5配置文件、以及一个或多个module.json5配置文件。

说明

编译后，单个模块的编译产物中，app.json5和module.json5的内容会合并到一个module.json文件中，详情参考[编译态包结构](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-package-structure-stage#%E7%BC%96%E8%AF%91%E6%80%81%E5%8C%85%E7%BB%93%E6%9E%84)的编译打包后的视图。

[app.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)包含以下内容：

- 应用的全局配置信息，包含应用的Bundle名称、开发厂商、版本号等基本信息。
    
- 特定设备类型的配置信息。
    

[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)包含以下内容：

- [Module](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-package-overview#module%E7%B1%BB%E5%9E%8B)的基本配置信息，包含Module名称、类型、描述、支持的设备类型等基本信息。
    
- 应用组件信息，包含[UIAbility组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#abilities%E6%A0%87%E7%AD%BE)和[ExtensionAbility组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#extensionabilities%E6%A0%87%E7%AD%BE)的描述信息。
    
- 应用运行过程中需要的权限信息。
- # app.json5配置文件

更新时间: 2025-12-16 16:34

应用级配置文件，包含应用的全局配置信息和特定设备类型的配置信息，用于向编译工具、操作系统和应用市场提供应用的基本信息。每个工程下必须包含一个app.json5配置文件，文件所在目录为工程名称/AppScope/app.json5。

说明

配置文件中的示例代码直接拷贝到工程中可能编译不通过，请开发者根据需求进行配置。例如：通过$符号引用的资源文件如果工程中不存在，需要开发者手动添加或替换为实际的资源文件。

配置文件中，字段可以重复，以最后一个配置为准。

## 配置文件示例

先通过一个示例，了解app.json5配置文件的结构和内容。

1. {
2.   "app": {
3.     "bundleName": "com.application.myapplication",
4.     "vendor": "example",
5.     "versionCode": 1000000,
6.     "versionName": "1.0.0",
7.     "icon": "$media:layered_image",
8.     "label": "$string:app_name",
9.     "description": "$string:description_application",
10.     "minAPIVersion": 9,
11.     "targetAPIVersion": 9,
12.     "debug": false,
13.     "car": {
14.       "minAPIVersion": 8
15.     },
16.     "targetBundleName": "com.application.test",
17.     "targetPriority": 50,
18.     "appEnvironments": [
19.       {
20.         "name":"name1",
21.         "value": "value1"
22.       }
23.     ],
24.     "maxChildProcess": 5,
25.     "multiAppMode": {
26.       "multiAppModeType": "multiInstance",
27.       "maxCount": 5
28.     },
29.     "hwasanEnabled": false,
30.     "ubsanEnabled": false,
31.     "cloudFileSyncEnabled": false,
32.     "cloudStructuredDataSyncEnabled": false,
33.     "configuration": "$profile:configuration",
34.     "assetAccessGroups": [
35.       "com.ohos.photos",
36.       "com.ohos.screenshot",
37.       "com.ohos.note"
38.     ],
39.     "startMode": "mainTask"
40.   }
41. }

## 配置文件标签

app.json5配置文件包含以下标签。

**表1** app.json5配置文件标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|bundleName|标识应用的Bundle名称，用于标识应用的唯一性。命名规则如下 ：<br><br>- 必须为以点号（.）分隔的字符串，且至少包含三段，每段中仅允许使用英文字母、数字、下划线（_）。<br><br>- 首段以英文字母开头，非首段以数字或英文字母开头，每一段以数字或者英文字母结尾。<br><br>- 不允许多个点号（.）连续出现。<br><br>- 字符串最小长度为7字节，最大长度128字节。<br><br>- 推荐采用反域名形式命名（如“com.example.demo”，建议第一级为域名后缀com，第二级为厂商/个人名，第三级为应用名，也可以多级）。|字符串|该标签不可缺省。|
|bundleType|标识应用的Bundle类型。支持的取值如下：<br><br>- app：当前Bundle为应用。<br><br>- atomicService：当前Bundle为元服务。<br><br>- shared：当前Bundle为共享库应用，仅支持系统应用配置，三方应用配置后应用无法安装。<br><br>- appService：当前Bundle为系统级共享库应用，仅系统应用生效。<br><br>- appPlugin：当前Bundle为应用的插件包。从API version 19开始，支持该标签。|字符串|该标签可缺省，缺省值为app。|
|debug|标识应用是否可调试。<br><br>- true：可调试，一般用于开发阶段。<br><br>- false：不可调试，一般用于发布阶段。|布尔值|由DevEco Studio编译构建时生成。该标签可缺省，缺省值为false。|
|icon|标识应用的图标，取值为图标资源文件的索引。支持配置单层图标和分层图标，配置规则和示例请参考[配置应用图标和名称](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/layered-image)。|字符串|该标签不可缺省。|
|label|标识应用的名称，取值为字符串资源的索引，以支持多语言，字符串长度不超过63字节，具体请参考[配置应用图标和名称](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/layered-image) 。|字符串|该标签不可缺省。|
|description|标识应用的描述信息，取值为长度不超过255字节的字符串，内容为描述信息的字符串或者字符串资源索引。该标签可用于应用信息展示，如在应用的关于页面，取该标签展示应用描述信息。|字符串|该标签可缺省，缺省值为空。|
|vendor|标识对应用开发厂商的描述，取值为长度不超过255字节的字符串。该标签可用于展示开发厂商信息，如在应用的关于页面，取该标签展示开发厂商信息。|字符串|该标签可缺省，缺省值为空。|
|versionCode|标识应用的版本号，取值范围为0~2147483647。此数字仅用于确定某个版本是否比另一个版本新，数值越大表示版本越新。<br><br>开发者可以将该值设置为任何正整数，但是必须确保应用的新版本都使用比旧版本更大的值。|数值|该标签不可缺省。|
|versionName|标识向用户展示的应用版本号。<br><br>取值为长度不超过127字节的字符串，仅由数字和点构成，推荐采用“A.B.C.D”四段式的形式。四段式推荐的含义如下所示。<br><br>第一段：主版本号/Major，重大修改的版本，如实现新的大功能或重大变化。<br><br>第二段：次版本号/Minor，表示实现较突出的特点，如新功能添加或大问题修复。<br><br>第三段：特性版本号/Feature，标识规划的新版本特性。<br><br>第四段：修订版本号/Patch，表示维护版本，如修复bug。|字符串|该标签不可缺省。|
|minCompatibleVersionCode|标识应用能够兼容的最低历史版本号，用于应用多设备之间协同、数据迁移、跨设备兼容性判断，该标签为预留字段，暂未使用。取值范围为0~2147483647。|数值|该标签可缺省，缺省值等于versionCode标签值。|
|minAPIVersion|标识应用运行所需的最小SDK API版本。取值范围为0~2147483647。|数值|该标签在应用编译构建时自动生成，手动配置无效，对应[工程级build-profile.json5文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section45865492619)中的compatibleSdkVersion标签。相关标签与应用兼容性关系参见[应用兼容性说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/app-compatibility)。|
|targetAPIVersion|标识应用运行需要的API目标版本。取值范围为0~2147483647。|数值|该标签在应用编译构建时自动生成，手动配置无效，对应[工程级build-profile.json5文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section45865492619)中的targetSdkVersion标签，如果未配置targetSdkVersion标签，则由工程级build-profile.json5文件中的compileSdkVersion自动生成。相关标签与应用兼容性关系参见[应用兼容性说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/app-compatibility)。|
|apiReleaseType|标识应用运行需要的API目标版本的类型，采用字符串类型表示。取值为“CanaryN”、“BetaN”或者“ReleaseN”，其中，N代表大于零的整数。<br><br>- Canary：受限发布的版本。<br><br>- Beta：公开发布的Beta版本。<br><br>- Release：公开发布的正式版本。|字符串|应用编译构建时根据当前使用的SDK的版本类型自动生成。手动配置无效。|
|accessible|标识应用是否能访问应用的安装目录，仅预置的系统应用配置生效，三方应用配置不生效。<br><br>- true：当前应用可以访问应用的安装目录。<br><br>- false：当前应用不可以访问应用的安装目录。|布尔值|该标签可缺省，缺省值为false。|
|multiProjects|标识当前工程是否支持多个工程的联合开发。<br><br>- true：当前工程支持多个工程的联合开发。多工程开发可参考[多工程构建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-multi-projects)。<br><br>- false：当前工程不支持多个工程的联合开发。|布尔值|该标签在应用编译构建时自动生成，手动配置无效，对应[工程级build-profile.json5文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app)中的multiProjects标签。|
|asanEnabled|标识应用程序是否开启[asan检测](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-asan)，用于辅助定位buffer越界造成的crash问题。<br><br>- true：当前工程开启asan检测。<br><br>- false：当前工程不开启asan检测。|布尔值|该标签可缺省，缺省值为false。|
|tablet|标识对tablet设备做的特殊配置，可以配置的属性标签有上文提到的：minAPIVersion。<br><br>如果使用该属性对tablet设备做了特殊配置，则应用在tablet设备中会采用此处配置的属性值，并忽略在app.json5公共区域配置的属性值。|对象|该标签可缺省，缺省时tablet设备使用app.json5公共区域配置的属性值。|
|tv|标识对tv设备做的特殊配置，可以配置的属性标签有上文提到的：minAPIVersion。<br><br>如果使用该属性对tv设备做了特殊配置，则应用在tv设备中会采用此处配置的属性值，并忽略在app.json5公共区域配置的属性值。|对象|该标签可缺省，缺省时tv设备使用app.json5公共区域配置的属性值。|
|wearable|标识对wearable设备做的特殊配置，可以配置的属性标签有上文提到的：minAPIVersion。<br><br>如果使用该属性对wearable设备做了特殊配置，则应用在wearable设备中会采用此处配置的属性值，并忽略在app.json5公共区域配置的属性值。|对象|该标签可缺省，缺省时wearable设备使用app.json5公共区域配置的属性值。|
|car|标识对car设备做的特殊配置，可以配置的属性标签有上文提到的：minAPIVersion。<br><br>如果使用该属性对car设备做了特殊配置，则应用在car设备中会采用此处配置的属性值，并忽略在app.json5公共区域配置的属性值。|对象|该标签可缺省，缺省时car设备使用app.json5公共区域配置的属性值。|
|default|标识对default设备做的特殊配置，可以配置的属性标签有上文提到的：minAPIVersion。<br><br>如果使用该属性对default设备做了特殊配置，则应用在default设备中会采用此处配置的属性值，并忽略在app.json5公共区域配置的属性值。|对象|该标签可缺省，缺省时default设备使用app.json5公共区域配置的属性值。|
|targetBundleName|标识当前包所指定的目标应用, 标签值的取值规则和范围与bundleName标签一致。配置该标签的应用为具有overlay特征的应用。|字符串|该标签可缺省，缺省值为空。|
|targetPriority|标识当前应用的优先级，取值范围为1~100。配置targetBundleName标签之后，才支持配置该标签。|数值|该标签可缺省，缺省值为1。|
|generateBuildHash|标识当前应用的所有HAP和HSP是否由打包工具生成哈希值。<br><br>该标签配置为true时，该应用下的所有HAP和HSP都会由打包工具生成对应的哈希值。系统OTA升级时，若应用的versionCode保持不变，可根据哈希值判断应用是否需要升级。<br><br>- true：当前应用下所有HAP和HSP都会由打包工具生成对应的哈希值。<br><br>- false：当前应用下所有HAP和HSP都不会由打包工具生成对应的哈希值。<br><br>**说明：**<br><br>该标签仅对预置应用生效。|布尔值|该标签可缺省，缺省值为false。|
|GWPAsanEnabled|标识应用程序是否开启[GWP-asan](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-stability-gwpasan-detection#section2735718353)堆内存检测工具，用于对内存越界、内存释放后使用等内存破坏问题进行分析。<br><br>- true：应用程序开启GWP-asan检测。<br><br>- false：应用程序不开启GWP-asan检测。|布尔值|该标签可缺省，缺省值为false。|
|[appEnvironments](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file#appenvironments%E6%A0%87%E7%AD%BE)|标识当前应用配置的应用环境变量。|对象数组|该标签可缺省，缺省值为空。|
|maxChildProcess|标识当前应用自身可创建的子进程的最大个数，取值范围为0到512，0表示不限制，当应用有多个模块时，以entry模块的配置为准。|数值|该标签可缺省，缺省时使用系统配置的默认值512。|
|[multiAppMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file#multiappmode%E6%A0%87%E7%AD%BE)|标识当前应用配置的多开模式。仅bundleType为app的应用的entry或feature模块配置有效，存在多个模块时，以entry模块的配置为准。|对象|该标签可缺省，缺省值为空。|
|hwasanEnabled|标识应用程序是否开启[HWAsan检测](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hwasan)。HWAsan(HardWare-assisted AddressSanitizer)是利用Top-Byte-Ignore特性实现的增强版Asan，与Asan相比HWAsan的内存开销更低，检测到的内存错误范围更大。<br><br>- true：当前工程开启HWAsan检测。<br><br>- false：当前工程不开启HWAsan检测。<br><br>**说明：**<br><br>从API version 14开始，支持该标签。|布尔值|该标签可缺省，缺省值为false。|
|ubsanEnabled|标识应用程序是否开启UBsan检测。<br><br>UBsan(Undefined Behavior Sanitizer)是一个用于运行时检测程序中未定义行为的工具，旨在帮助开发人员发现代码中潜在的错误和漏洞。<br><br>- true：当前工程开启UBsan检测。<br><br>- false：当前工程不开启UBsan检测。<br><br>**说明：**<br><br>从API version 14开始，支持该标签。|布尔值|该标签可缺省，缺省值为false。|
|cloudFileSyncEnabled|标识当前应用是否启用端云文件同步能力。<br><br>- true：当前应用启用端云文件同步能力。<br><br>- false：当前应用不启用端云文件同步能力。|布尔值|该标签可缺省，缺省值为false。|
|cloudStructuredDataSyncEnabled|标识当前应用是否启用端云结构化数据同步能力。<br><br>- true：当前应用启用端云结构化数据同步能力。<br><br>- false：当前应用不启用端云结构化数据同步能力。<br><br>**说明：**<br><br>从API version 20开始，支持该标签。|布尔值|该标签可缺省，缺省值为false。|
|[configuration](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file#configuration%E6%A0%87%E7%AD%BE)|标识当前应用字体大小跟随系统配置的能力。<br><br>该标签是一个profile文件资源，用于指定描述应用字体大小跟随系统变更的配置文件。|字符串|该标签可缺省，缺省时configuration使用不跟随系统默认设定。|
|assetAccessGroups|配置应用的Group ID，它和Developer ID一起组成群组信息。<br><br>打包HAP时，DevEco使用开发者证书对群组信息签名，其中群组信息由Developer ID（由应用市场分配）+ Group ID（开发者配置）组成。<br><br>**说明：**<br><br>从API version 18开始，支持该标签。|字符串数组|该标签可缺省，缺省值为空。|
|appPreloadPhase|配置[应用预加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preload-application)到不同阶段。支持的取值如下：<br><br>-processCreated：预加载到进程创建完成阶段。<br><br>-abilityStageCreated：预加载到[AbilityStage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-abilitystage)创建完成阶段。<br><br>-windowStageCreated：预加载到[WindowStage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-windowstage)创建完成阶段。<br><br>**说明：**<br><br>从API version 20开始，支持该标签。<br><br>仅在PC/2in1设备上生效。<br><br>仅在应用的entry模块配置有效。<br><br>该标签仅表示应用自身是否为预加载到所配置阶段做好了准备，最终能否预加载还需要由系统根据用户习惯等信息来决策。|字符串|该标签可缺省，缺省时不进行预加载。|
|[startMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-component-configuration-stage#%E5%BA%94%E7%94%A8%E5%90%AF%E5%8A%A8%E6%A8%A1%E5%BC%8F%E9%85%8D%E7%BD%AE)|配置应用的启动模式，支持的取值如下：<br><br>- mainTask：主任务模式，表示图标启动后打开主UIAbility。<br><br>- recentTask：最近任务模式，表示图标启动后打开最近使用的UIAbility。<br><br>**说明：**<br><br>从API version 20开始，支持该标签。<br><br>仅在launchType为[单实例模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uiability-launch-type#singleton%E5%90%AF%E5%8A%A8%E6%A8%A1%E5%BC%8F)时生效。<br><br>该标签仅支持phone和tablet设备(不包含自由多窗)。|字符串|该标签可缺省，缺省值为mainTask。|

## appEnvironments标签

此标签标识应用配置的环境变量。应用运行时有时会依赖一些三方库，这些三方库会使用到一些自定义的环境变量，为了不修改三方库的实现逻辑，可以在工程的配置文件中设置自定义的环境变量，以供运行时使用。

**表2** appEnvironments标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识环境变量的变量名称。取值为长度不超过4096字节的字符串。|字符串|该标签可缺省，缺省值为空。|
|value|标识环境变量的值。取值为长度不超过4096字节的字符串。|字符串|该标签可缺省，缺省值为空。|

appEnvironments标签示例：

1. {
2.   "app": {
3.     "appEnvironments": [
4.       {
5.         "name":"name1",
6.         "value": "value1"
7.       }
8.     ]
9.   }
10. }

## multiAppMode标签

应用多开模式。

**表3** multiAppMode标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|multiAppModeType|标识应用多开模式类型，支持的取值如下：<br><br>- multiInstance：多实例模式。该标签仅支持2in1设备，常驻进程不支持该标签。<br><br>- appClone：应用分身模式。|字符串|该标签不可缺省。|
|maxCount|标识最大允许的应用多开个数，支持的取值如下：<br><br>- multiInstance模式：取值范围1~10。<br><br>- appClone模式：取值范围1~5。|数值|该标签不可缺省。|

multiAppMode标签示例：

1. {
2.   "app": {
3.     "multiAppMode": {
4.       "multiAppModeType": "appClone",
5.       "maxCount": 5
6.     }
7.   }
8. }

## configuration标签

该标签对应一个profile文件资源，对应文件用于配置应用字体大小是否跟随系统变更。

configuration标签示例：

1. {
2.   "app": {
3.     "configuration": "$profile:configuration"
4.   }
5. }

在开发视图的AppScope/resources/base/profile下面定义配置文件configuration.json，其中文件名"configuration"可自定义，需要和configuration标签指定的文件资源对应。配置文件中列举了设置当前应用字体大小跟随系统变化所需要的属性。

**表4** configuration标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|fontSizeScale|应用字体大小是否跟随系统，支持的取值如下：<br><br>- followSystem：跟随系统。<br><br>- nonFollowSystem：不跟随系统。|字符串|该标签可缺省，缺省值为nonFollowSystem。|
|fontSizeMaxScale|应用字体大小选择跟随系统后，配置的应用字体最大放大倍数，支持的取值为：1、1.15、1.3、1.45、1.75、2、3.2。<br><br>例如配置应用字体最大放大倍数为1.75，系统字体标准大小为10fp。<br><br>（1）如果设置中调整系统字体放大倍数为1.5倍，应用会跟随系统一起调整为15fp。<br><br>（2）如果设置中调整系统字体放大倍数为2倍，此时系统的字体大小为20fp，但由于应用配置的最大放大倍数为1.75，所以此时应用的字体大小为17.5fp。<br><br>**说明**<br><br>fontSizeScale为nonFollowSystem时，该项不生效。|字符串|该标签可缺省，缺省值为3.2。|

configuration标签示例：

1. {
2.   "configuration": {
3.     "fontSizeScale": "followSystem",
4.     "fontSizeMaxScale": "3.2"
5.   }
6. }
# module.json5配置文件

更新时间: 2025-12-16 16:34

模块级配置文件，包含模块的基本配置信息、UIAbility组件ExtensionAbility组件信息，和应用运行过程中需要的权限信息，用于向编译工具、操作系统和应用市场提供应用的基本信息。每个模块下必须包括一个module.json5配置文件，文件所在目录为工程名称/模块名称（例如entry）/src/main/module.json5。

说明

配置文件中的示例代码直接拷贝到工程中可能编译不通过，请开发者根据需求进行配置。例如：通过$符号引用的资源文件如果工程中不存在，需要开发者手动添加或替换为实际的资源文件。

配置文件中，字段可以重复，以最后一个配置为准。

## 配置文件示例

通过一个示例，整体了解module.json5配置文件。

1. {
2.   "module": {
3.     "name": "entry",
4.     "type": "entry",
5.     "description": "$string:module_desc",
6.     "mainElement": "EntryAbility",
7.     "deviceTypes": [
8.       "tv",
9.       "tablet"
10.     ],
11.     "deliveryWithInstall": true,
12.     "pages": "$profile:main_pages",
13.     "appStartup": "$profile:app_startup_config",
14.     "metadata": [
15.       {
16.         "name": "string",
17.         "value": "string",
18.         "resource": "$profile:distributionFilter_config"
19.       }
20.     ],
21.     "abilities": [
22.       {
23.         "name": "EntryAbility",
24.         "srcEntry": "./ets/entryability/EntryAbility.ets",
25.         "description": "$string:EntryAbility_desc",
26.         "icon": "$media:layered_image",
27.         "label": "$string:EntryAbility_label",
28.         "startWindow": "$profile:start_window",
29.         "startWindowIcon": "$media:icon",
30.         "startWindowBackground": "$color:start_window_background",
31.         "exported": true,
32.         "skills": [
33.           {
34.             "entities": [
35.               "entity.system.home"
36.             ],
37.             "actions": [
38.               "ohos.want.action.home"
39.             ]
40.           }
41.         ],
42.         "continueType": [
43.           "continueType1"
44.         ],
45.         "continueBundleName": [
46.           "com.example.myapplication1",
47.           "com.example.myapplication2"
48.         ]
49.       }
50.     ],
51.     "requestPermissions": [
52.       {
53.         "name": "ohos.permission.ACCESS_BLUETOOTH",
54.         "reason": "$string:reason",
55.         "usedScene": {
56.           "abilities": [
57.             "EntryAbility"
58.           ],
59.           "when": "inuse"
60.         }
61.       }
62.     ],
63.     "querySchemes": [
64.       "app1Scheme",
65.       "app2Scheme"
66.     ],
67.     "routerMap": "$profile:router_map",
68.     "appEnvironments": [
69.       {
70.         "name": "name1",
71.         "value": "value1"
72.       }
73.     ],
74.     "hnpPackages": [
75.       {
76.         "package": "hnpsample.hnp",
77.         "type": "public"
78.       }
79.     ],
80.     "fileContextMenu": "$profile:menu",
81.     "crossAppSharedConfig": "$profile:shared_config"
82.   }
83. }

## 配置文件标签

module.json5配置文件包含以下标签。

**表1** module.json5配置文件标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识当前Module的名称，确保该名称在整个应用中唯一。命名规则如下 ：<br><br>- 由字母、数字和下划线组成，且必须以字母开头。<br><br>- 最大长度128字节。<br><br>应用升级时允许修改该名称，但需要应用适配Module相关数据目录的迁移，详见[文件管理接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs)。|字符串|该标签不可缺省。|
|type|标识当前Module的类型。支持的取值如下：<br><br>- entry：应用的主模块。<br><br>- feature：应用的动态特性模块。<br><br>- har：静态共享包模块。<br><br>- shared：动态共享包模块。|字符串|该标签不可缺省。|
|srcEntry|标识AbilityStage组件的代码路径，详情参考[AbilityStage组件容器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/abilitystage)，取值为长度不超过127字节的字符串。|字符串|该标签可缺省，缺省值为空。|
|description|标识当前Module的描述信息，开发者可以通过该标签描述当前模块的功能与作用，取值为长度不超过255字节的字符串，可以采用字符串资源索引格式。|字符串|该标签可缺省，缺省值为空。|
|mainElement|标识当前Module的入口UIAbility名称，取值为长度不超过255字节的字符串。<br><br>**说明：**<br><br>如果在[abilities](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#abilities%E6%A0%87%E7%AD%BE)中配置了多个入口[UIAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uiability-overview)，则桌面图标、名称和启动入口以该标签配置为准。如果该标签缺省或未匹配到，则按照ASCII字典序对UIAbility的name标签正序排序，返回第一个作为桌面图标、名称和启动入口。|字符串|该标签可缺省，缺省值为空。|
|[deviceTypes](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#devicetypes%E6%A0%87%E7%AD%BE)|标识当前Module可以运行在哪类设备上。<br><br>**说明：**<br><br>当存在多个模块时，各模块的配置可以不同，但都必须包含将要安装的设备类型，以确保正常运行。|字符串数组|该标签不可缺省。|
|deliveryWithInstall|标识当前Module是否在用户主动安装的时候安装，即该Module对应的HAP/HSP是否跟随应用一起安装。<br><br>- true：跟随应用一起安装。<br><br>- false：不跟随应用一起安装。通过[按需分发](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/store-moduleinstall_arkts)的方式安装。|布尔值|当前Module类型为HAP或HSP时，该标签不可缺省。|
|installationFree|标识当前Module是否支持免安装特性。<br><br>- true：表示支持免安装特性，且符合免安装约束。<br><br>- false：表示不支持免安装特性。|布尔值|该标签可缺省。该标签在编译构建时自动生成，手动配置不生效。<br><br>**说明：**<br><br>当[bundleType](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E6%A0%87%E7%AD%BE)为元服务时，该标签自动配置为true。反之，该标签自动配置为false。|
|virtualMachine|标识当前Module运行的目标虚拟机类型，供云端分发使用，如应用市场和分发中心。如果目标虚拟机类型为ArkTS引擎，则其值为“ark+版本号”。|字符串|该标签可缺省，手动配置不生效，由编译构建时自动生成。|
|[pages](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#pages%E6%A0%87%E7%AD%BE)|标识当前Module的profile资源，用于列举每个页面信息，取值为长度不超过255字节的字符串。|字符串|该标签可缺省，缺省值为空。|
|[metadata](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#metadata%E6%A0%87%E7%AD%BE)|标识当前Module的自定义元信息，可通过资源引用的方式配置[distributionFilter](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#distributionfilter%E6%A0%87%E7%AD%BE)、[shortcuts](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#shortcuts%E6%A0%87%E7%AD%BE)等信息。只对当前Module、UIAbility、ExtensionAbility生效。|对象数组|该标签可缺省，缺省值为空。|
|[abilities](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#abilities%E6%A0%87%E7%AD%BE)|标识当前Module中UIAbility的配置信息，只对当前UIAbility生效。|对象数组|该标签可缺省，缺省值为空。|
|[extensionAbilities](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#extensionabilities%E6%A0%87%E7%AD%BE)|标识当前Module中ExtensionAbility的配置信息，只对当前ExtensionAbility生效。|对象数组|该标签可缺省，缺省值为空。|
|[requestPermissions](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)|标识当前应用运行时需向系统申请的权限集合。|对象数组|该标签可缺省，缺省值为空。|
|[testRunner](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#testrunner%E6%A0%87%E7%AD%BE)|标识用于测试当前Module的测试框架的配置。详情请参考[启动测试框架命令](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/aa-tool#%E5%90%AF%E5%8A%A8%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6%E5%91%BD%E4%BB%A4test)。|对象|该标签可缺省，缺省值为空。|
|[atomicService](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#atomicservice%E6%A0%87%E7%AD%BE)|标识当前应用是元服务时，有关元服务的相关配置。|对象|该标签可缺省，缺省值为空。|
|[dependencies](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#dependencies%E6%A0%87%E7%AD%BE)|标识当前模块运行时依赖的共享库列表。|对象数组|该标签可缺省，缺省值为空。手动配置不生效，由编译构建时自动生成。|
|targetModuleName|标识当前包所指定的目标Module。取值为长度不超过128字节的字符串，不支持中文。配置该标签的Module具有overlay特性。仅在动态共享包（HSP）中适用。|字符串|该标签可缺省，缺省值为空。|
|targetPriority|标识当前Module的优先级，取值范围为1~100。配置targetModuleName标签之后，才需要配置该标签。仅在动态共享包（HSP）中适用。|整型数值|该标签可缺省，缺省值为1。|
|[proxyData](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#proxydata%E6%A0%87%E7%AD%BE)|标识当前Module提供的数据代理列表。|对象数组|该标签可缺省，缺省值为空。|
|isolationMode|标识当前Module的多进程配置项。支持的取值如下：<br><br>- nonisolationFirst：优先在非独立进程中运行。<br><br>- isolationFirst：优先在独立进程中运行。<br><br>- isolationOnly：只在独立进程中运行。<br><br>- nonisolationOnly：只在非独立进程中运行。<br><br>**说明：**<br><br>1.仅2in1和tablet设备支持将当前Module设置为独立进程。<br><br>2.该标签仅对HAP生效。|字符串|该标签可缺省，缺省值为nonisolationFirst。|
|generateBuildHash|标识当前HAP/HSP是否由打包工具生成哈希值。当配置为true时，如果系统OTA升级时应用versionCode保持不变，可根据哈希值判断应用是否需要升级。<br><br>该标签仅在[app.json5文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file)中的generateBuildHash标签为false时使能。<br><br>**说明：**<br><br>该标签仅对预置应用生效。|布尔值|该标签可缺省，缺省值为false。|
|compressNativeLibs|在打包hap时，该标签标识libs库是否以压缩存储的方式打包到HAP。<br><br>- true：libs库以压缩方式存储。<br><br>- false：libs库以不压缩方式存储。|布尔值|该标签可缺省，在打包hap时缺省值为false。|
|extractNativeLibs|标识应用安装时，libs库是否解压到应用安装目录。当compressNativeLibs和extractNativeLibs都配置为false时，应用以不解压libs库的方式进行安装；其他场景，应用以解压libs库的方式进行安装。<br><br>**说明：**<br><br>从API version 20开始，支持该标签。|布尔值|该标签可缺省，缺省值为true。|
|libIsolation|在libs目录下是否生成模块名称目录存储so，用于区分同一应用中不同HAP的.so文件，以防止.so文件冲突。<br><br>- true：当前HAP的.so文件会储存在libs目录中以Module名命名的路径下。<br><br>- false：当前HAP的.so文件会直接储存在libs目录中。|布尔值|该标签可缺省，缺省值为false。|
|[fileContextMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#filecontextmenu%E6%A0%87%E7%AD%BE)|标识当前HAP的右键菜单配置项，是一个profile文件资源。取值为长度不超过255字节的字符串。<br><br>**说明：**<br><br>仅在PC/2in1设备上生效。<br><br>仅允许在entry类型模块中配置。|字符串|该标签可缺省，缺省值为空。|
|querySchemes|标识允许当前应用进行跳转查询的URL schemes，只允许entry类型模块配置，每个字符串取值不超过128字节。<br><br>**说明：**<br><br>从API version 21开始，最多允许配置200个URL scheme。API version 20及之前的版本，最多允许配置50个URL scheme。|字符串数组|该标签可缺省，缺省值为空。|
|[routerMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#routermap%E6%A0%87%E7%AD%BE)|标识当前模块配置的路由表路径。取值为长度不超过255字节的字符串。|字符串|该标签可缺省，缺省值为空。|
|[appEnvironments](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#appenvironments%E6%A0%87%E7%AD%BE)|标识当前模块配置的应用环境变量，只允许entry和feature模块配置。|对象数组|该标签可缺省，缺省值为空。|
|appStartup|标识当前Module[启动框架](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-startup)配置路径，只允许entry类型模块配置。<br><br>从API version 18开始，新增支持在HSP、HAR中配置。<br><br>从API version 20开始，新增支持在feature类型的Module中配置。|字符串|该标签可缺省，缺省值为空。|
|[hnpPackages](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#hnppackages%E6%A0%87%E7%AD%BE)|标识当前应用包含的Native软件包信息。只允许entry类型模块配置。|对象数组|该标签可缺省，缺省值为空。|
|[systemTheme](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#systemtheme%E6%A0%87%E7%AD%BE)|标识当前使用的系统主题配置项。只允许entry类型模块配置。取值为不超过255字节的字符串。<br><br>**说明：**<br><br>从API version 20开始，支持该标签。|字符串|该标签可缺省，缺省值为空。|
|abilitySrcEntryDelegator|标识当前Module需要重定向到的UIAbility的名称，与abilityStageSrcEntryDelegator标签组合使用，共同指定重定向的目标对象。<br><br>**说明：**<br><br>1.从API version 17开始，支持该标签。<br><br>2.当UIAbility是通过[startAbilityByCall](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-uiabilitycontext#startabilitybycall)接口启动时，该标签不生效。<br><br>3.不支持在HAR的配置文件中配置该标签，也不支持重定向到HAR的UIAbility。|字符串|该标签可缺省，缺省值为空。|
|abilityStageSrcEntryDelegator|标识当前Module需要重定向到的UIAbility对应的Module名称（不可为当前Module名称），与abilitySrcEntryDelegator标签组合使用，共同指定重定向的目标对象。<br><br>**说明：**<br><br>1.从API version 17开始，支持该标签。<br><br>2.当UIAbility是通过[startAbilityByCall](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-uiabilitycontext#startabilitybycall)接口启动时，该标签不生效。<br><br>3.不支持在HAR的配置文件中配置该标签，也不支持重定向到HAR的UIAbility。|字符串|该标签可缺省，缺省值为空。|
|crossAppSharedConfig|标识应用间共享配置的配置文件名。取值为不超过255字节的字符串。用于发布配置给其他应用读取，在应用安装时生效，应用卸载时失效。详细使用方式见[共享配置使用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/share-config#%E9%85%8D%E7%BD%AE%E5%8F%91%E5%B8%83%E6%96%B9)。<br><br>**说明：**<br><br>从API version 20开始，支持该标签。|字符串|该标签可缺省，缺省值为空。|
|formWidgetModule|在[独立卡片包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-ui-widget-creation#%E6%96%B9%E5%BC%8F%E4%BA%8C%E7%8B%AC%E7%AB%8B%E5%8C%85%E6%96%B9%E5%BC%8F%E5%88%9B%E5%BB%BA%E5%8D%A1%E7%89%87)中，应用包需要配置该标签，用来关联卡片包。取值为卡片包的模块名称，对应卡片包module.json5中的name标签。具体使用方式请参考[FormExtensionAbility配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-ui-widget-configuration#formextensionability%E9%85%8D%E7%BD%AE)。<br><br>**说明：**<br><br>1. 从API version 20开始，支持该标签。<br><br>2. 仅在独立卡片包的应用包中，该标签配置生效，且要求对应的卡片包模块必须配置formExtensionModule标签。|字符串|该标签可缺省，缺省值为空。|
|formExtensionModule|在[独立卡片包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-ui-widget-creation#%E6%96%B9%E5%BC%8F%E4%BA%8C%E7%8B%AC%E7%AB%8B%E5%8C%85%E6%96%B9%E5%BC%8F%E5%88%9B%E5%BB%BA%E5%8D%A1%E7%89%87)中，卡片包需要配置该标签，用来关联应用包。取值为应用包的模块名称，对应应用包module.json5中的name标签。具体使用方式请参考[独立卡片包配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-ui-widget-configuration#%E7%8B%AC%E7%AB%8B%E5%8D%A1%E7%89%87%E5%8C%85%E9%85%8D%E7%BD%AE)。<br><br>**说明：**<br><br>1. 从API version 20开始，支持该标签。<br><br>2. 仅在独立卡片包的卡片包中，该标签配置生效，且要求对应的应用包模块必须配置formWidgetModule标签。|字符串|该标签可缺省，缺省值为空。|
|[requiredDeviceFeatures](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#requireddevicefeatures%E6%A0%87%E7%AD%BE)|标识当前Module运行所需要的特定的设备特性，应用市场可以根据此配置，将应用分发给支持该特性的设备。**说明：**<br><br>1.从API version 19开始，支持该字段。<br><br>2.不支持插件应用配置。|对象|该标签可缺省，缺省值为空。|

## deviceTypes标签

**表2** deviceTypes标签说明

|设备类型|枚举值|说明|
|:--|:--|:--|
|手机|phone|-|
|平板|tablet|-|
|PC/2in1|2in1|即PC设备，主要交互方式以多窗口、多任务及键盘鼠标操作为主，充分发挥设备的生产力属性。在HarmonyOS文档中，所有“2in1”均代表“PC/2in1”。|
|智慧屏|tv|-|
|智能手表|wearable|系统能力较丰富的手表，具备电话功能。|
|车机|car|-|
|默认设备|default|配置为default类型的应用，虽然可以正常编译构建，但是不支持发布上架。建议使用phone替代。|

deviceTypes示例：

1. {
2.   "module": {
3.     "name": "myHapName",
4.     "type": "feature",
5.     "deviceTypes" : [
6.        "tablet"
7.     ]
8.   }
9. }

## pages标签

该标签是一个profile文件资源，用于指定描述页面信息的配置文件。

1. {
2.   "module": {
3.     // ...
4.     "pages": "$profile:main_pages", // 通过profile下的资源文件配置
5.   }
6. }

在开发视图的resources/base/profile下面定义配置文件main_pages.json，其中文件名"main_pages"可自定义，需要和pages标签指定的信息对应。配置文件中列举了当前应用组件中的页面信息，包含页面的路由信息和显示窗口相关的配置。

**表3** pages标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|src|标识当前Module中所有页面的路由信息，包括页面路径和页面名称。其中，页面路径是以当前Module的src/main/ets为基准。该标签取值为一个字符串数组，其中每个元素表示一个页面。|字符串数组|该标签不可缺省。|
|window|标识用于定义与显示窗口相关的配置。|对象|该标签可缺省，缺省值为空。|

**表4** window标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|designWidth|标识页面设计基准宽度。以此为基准，根据实际设备宽度来缩放元素大小。|数值|可缺省，缺省值为720px。|
|autoDesignWidth|标识页面设计基准宽度是否自动计算。当配置为true时，designWidth将会被忽略，设计基准宽度由设备宽度与屏幕密度计算得出。当配置为false时，设计基准宽度为designWidth。|布尔值|可缺省，缺省值为false。|

1. {
2.   "src": [
3.     "pages/index/mainPage",
4.     "pages/second/payment",
5.     "pages/third/shopping_cart",
6.     "pages/four/owner"
7.   ],
8.   "window": {
9.     "designWidth": 720,
10.     "autoDesignWidth": false
11.   }
12. }

## metadata标签

该标签标识HAP的自定义元信息，标签值为数组类型，包含name、value、resource三个子标签。

**表5** metadata标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识数据项的名称，取值为长度不超过255字节的字符串。|字符串|该标签可缺省，缺省值为空。|
|value|标识数据项的值，取值为长度不超过255字节的字符串。|字符串|该标签可缺省，缺省值为空。|
|resource|标识了用户自定义数据，取值为长度不超过255字节的字符串，内容为该数据的资源索引，例如配置成$profile:shortcuts_config，表示指向了/resources/base/profile/shortcuts_config.json配置文件。|字符串|该标签可缺省，缺省值为空。|

1. {
2.   "module": {
3.     "metadata": [{
4.       "name": "module_metadata",
5.       "value": "a test demo for module metadata",
6.       "resource": "$profile:shortcuts_config"
7.     }]
8.   }
9. }

## abilities标签

abilities标签描述UIAbility组件的配置信息，标签值为数组类型，该标签下的配置只对当前UIAbility生效。

**表6** abilities标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识当前UIAbility组件的名称，确保该名称在整个应用中唯一。取值为长度不超过127字节的字符串，以字母开头，可包含字母、数字、下划线（_）或点号（.）。|字符串|该标签不可缺省。|
|srcEntry|标识当前UIAbility的代码路径，取值为长度不超过127字节的字符串。|字符串|该标签不可缺省。|
|[launchType](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uiability-launch-type)|标识当前UIAbility组件的启动模式，支持的取值如下：<br><br>- multiton：多实例模式，每次启动创建一个新实例。<br><br>- singleton：单实例模式，仅第一次启动创建新实例。<br><br>- specified：指定实例模式，运行时由开发者决定是否创建新实例。<br><br>- standard：multiton的曾用名，效果与多实例模式一致。<br><br>**说明：**<br><br>元服务启动模式需要设置为单例模式，详情请参考[元服务规格](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/atomic-specifications)要求。|字符串|该标签可缺省，该标签缺省为“singleton”。|
|description|标识当前UIAbility组件的描述信息，开发者可以通过该标签描述当前组件的功能与作用，取值为长度不超过255字节的字符串。建议采用描述信息的资源索引，以支持多语言。|字符串|该标签可缺省，缺省值为空。|
|icon|标识当前UIAbility组件的[图标](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/layered-image)，取值为图标资源文件的索引。|字符串|该标签可缺省，缺省值为空。|
|label|标识当前UIAbility组件对用户显示的[名称](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/layered-image)，取值为字符串资源的索引，以支持多语言，长度不超过255字节的字符串。|字符串|该标签可缺省，缺省值为空。|
|permissions|标识当前UIAbility组件的权限信息。其他应用访问该UIAbility时，需要申请相应的权限。<br><br>一个数组元素为一个权限名称，不超过255字节，取值请参考[应用权限列表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-permissions)。|字符串数组|该标签可缺省，缺省值为空。|
|[metadata](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#metadata%E6%A0%87%E7%AD%BE)|标识当前UIAbility组件的元信息，典型使用场景详见[窗口元数据配置中的metadata标签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/window-config-m#metadata%E6%A0%87%E7%AD%BE)。|对象数组|该标签可缺省，缺省值为空。|
|exported|标识当前UIAbility组件是否可以被其他应用拉起。<br><br>- true：表示可以被其他应用拉起（入口UIAbility建议配置为true）。<br><br>- false：只能由同应用或者具有ohos.permission.START_INVISIBLE_ABILITY权限（该权限仅系统应用支持申请）的应用拉起。<br><br>例如，配置为false时，桌面具备该权限，桌面图标、快捷方式或push通知消息可以拉起当前UIAbility组件，但aa命令行工具没有权限无法拉起。|布尔值|该标签可缺省，缺省值为false。|
|continuable|标识当前UIAbility组件是否支持跨端迁移。<br><br>- true：表示支持迁移。<br><br>- false：表示不支持迁移。|布尔值|该标签可缺省，缺省值为false。|
|[skills](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#skills%E6%A0%87%E7%AD%BE)|标识当前UIAbility组件能够接收的[Want](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/want-overview)特征集，为数组格式。<br><br>配置规则：<br><br>- 对于Entry类型的HAP，应用可以配置多个具有入口能力的skills标签（即配置了ohos.want.action.home和entity.system.home）。<br><br>- 对于Feature类型的HAP，只有应用可以配置具有入口能力的skills标签，服务不允许配置。|对象数组|该标签可缺省，缺省值为空。|
|backgroundModes|标识当前UIAbility组件的[长时任务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/continuous-task)集合，指定用于满足特定类型的长时任务。<br><br>长时任务类型有如下：<br><br>- dataTransfer：数据传输。<br><br>- audioPlayback：音视频播放。<br><br>- audioRecording：录制。<br><br>- location：定位导航。<br><br>- bluetoothInteraction：蓝牙相关业务。<br><br>- multiDeviceConnection：多设备互联。<br><br>- wifiInteraction：WLAN相关业务（仅对系统应用开放）。<br><br>- voip：音视频通话。<br><br>- taskKeeping：计算任务（仅对PC/2in1设备开放）。|字符串数组|该标签可缺省，缺省值为空。|
|[startWindow](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#startwindow%E6%A0%87%E7%AD%BE)|标识当前UIAbility组件启动页面profile资源，取值为长度不超过255字节的字符串，如果配置了该标签，startWindowIcon和startWindowBackground标签均不生效。<br><br>**说明：**<br><br>从API version 19开始，支持使用该字段配置增强启动页。|字符串|该标签可缺省，缺省值为空。|
|startWindowIcon|标识当前UIAbility组件启动页面图标资源文件的索引，取值为长度不超过255字节的字符串。|字符串|该标签不可缺省。|
|startWindowBackground|标识当前UIAbility组件启动页面背景颜色资源文件的索引，取值为长度不超过255字节的字符串。<br><br>取值示例：$color:red。|字符串|该标签不可缺省。|
|removeMissionAfterTerminate|标识当前UIAbility组件销毁后，是否从任务列表中移除任务。<br><br>- true表示销毁后移除任务。<br><br>- false表示销毁后不移除任务。<br><br>**说明：**<br><br>2in1设备和平板设备的自由多窗模式下配置不生效，默认移除任务。|布尔值|该标签可缺省，缺省值为false。|
|orientation|标识当前UIAbility组件启动时的方向，支持配置枚举，或启动方向资源索引。<br><br>**启动方向枚举支持的取值如下：**<br><br>- unspecified：未指定方向，由系统自动判断显示方向。<br><br>- landscape：横屏。<br><br>- portrait：竖屏。<br><br>- follow_recent：跟随背景窗口的旋转模式。<br><br>- landscape_inverted：反向横屏。<br><br>- portrait_inverted：反向竖屏。<br><br>- auto_rotation：随传感器旋转。<br><br>- auto_rotation_landscape：传感器横屏旋转，包括横屏和反向横屏。<br><br>- auto_rotation_portrait：传感器竖屏旋转，包括竖屏和反向竖屏。<br><br>- auto_rotation_restricted：传感器开关打开，方向可随传感器旋转。<br><br>- auto_rotation_landscape_restricted：传感器开关打开，方向可随传感器旋转为横屏， 包括横屏和反向横屏。<br><br>- auto_rotation_portrait_restricted：传感器开关打开，方向随可传感器旋转为竖屏， 包括竖屏和反向竖屏。<br><br>- locked：传感器开关关闭，方向锁定。<br><br>- auto_rotation_unspecified：受开关控制和由系统判定的自动旋转模式。<br><br>- follow_desktop：跟随桌面的旋转模式。<br><br>**配置启动方向的资源索引时**，取值为长度不超过255字节的字符串，配置示例：$string:orientation。<br><br>**说明：**<br><br>- 从API version 14开始，支持配置启动方向资源索引。|字符串|该标签可缺省，缺省值为unspecified。|
|supportWindowMode|标识当前UIAbility组件所支持的窗口模式。支持的取值如下：<br><br>- fullscreen：全屏模式。<br><br>- split：分屏模式。<br><br>- floating：悬浮窗模式。<br><br>在[自由窗口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/window-terminology#%E8%87%AA%E7%94%B1%E7%AA%97%E5%8F%A3)状态下同时配置fullscreen和split时，如果应用的[targetAPIVersion](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E6%A0%87%E7%AD%BE)小于15，窗口将以悬浮窗模式启动；如果应用的[targetAPIVersion](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-configuration-file#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E6%A0%87%E7%AD%BE)大于等于15，窗口将以全屏模式启动。<br><br>此外，还可以通过metadata配置窗口模式，具体的配置规则和优先级请参考[metadata](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#metadata%E6%A0%87%E7%AD%BE)。|字符串数组|该标签可缺省，缺省值为<br><br>["fullscreen", "split", "floating"]。|
|maxWindowRatio|标识当前UIAbility组件支持的最大的宽高比。该标签最小取值为0。|数值|该标签可缺省，缺省值为平台支持的最大的宽高比。|
|minWindowRatio|标识当前UIAbility组件支持的最小的宽高比。该标签最小取值为0。|数值|该标签可缺省，缺省值为平台支持的最小的宽高比。|
|maxWindowWidth|标识当前UIAbility组件支持的最大的窗口宽度，宽度单位为vp。<br><br>最小取值为minWindowWidth，最大取值为平台支持的最大窗口宽度。窗口尺寸可以参考[窗口大小限制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/window-overview#%E7%BA%A6%E6%9D%9F%E4%B8%8E%E9%99%90%E5%88%B6)。|数值|该标签可缺省，缺省值为平台支持的最大的窗口宽度。|
|minWindowWidth|标识当前UIAbility组件支持的最小的窗口宽度， 宽度单位为vp。<br><br>最小取值为平台支持的最小窗口宽度，最大取值为maxWindowWidth。窗口尺寸可以参考[窗口大小限制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/window-overview#%E7%BA%A6%E6%9D%9F%E4%B8%8E%E9%99%90%E5%88%B6)。|数值|该标签可缺省，缺省值为平台支持的最小的窗口宽度。|
|maxWindowHeight|标识当前UIAbility组件支持的最大的窗口高度， 高度单位为vp。<br><br>最小取值为minWindowHeight，最大取值为平台支持的最大窗口高度。 窗口尺寸可以参考[窗口大小限制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/window-overview#%E7%BA%A6%E6%9D%9F%E4%B8%8E%E9%99%90%E5%88%B6)。|数值|该标签可缺省，缺省值为平台支持的最大的窗口高度。|
|minWindowHeight|标识当前UIAbility组件支持的最小的窗口高度， 高度单位为vp。<br><br>最小取值为平台支持的最小窗口高度，最大取值为maxWindowHeight。窗口尺寸可以参考[窗口大小限制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/window-overview#%E7%BA%A6%E6%9D%9F%E4%B8%8E%E9%99%90%E5%88%B6)。|数值|该标签可缺省，缺省值为平台支持的最小的窗口高度。|
|recoverable|标识当前UIAbility组件是否支持在检测到应用故障后，恢复到应用原界面。<br><br>- true：支持检测到出现故障后，恢复到原界面。<br><br>- false：不支持检测到出现故障后，恢复到原界面。|布尔值|该标签可缺省，缺省值为false。|
|isolationProcess|标识组件能否运行在独立的进程中。<br><br>- true：表示能运行在独立的进程中。<br><br>- false：表示不能运行在独立的进程中。<br><br>**说明：**<br><br>仅2in1和tablet设备支持将UIAbility设置为独立进程。|布尔值|该标签可缺省，缺省值为false。|
|excludeFromDock|标识当前UIAbility组件是否支持从dock区域隐藏图标。<br><br>- true：表示在dock区域隐藏。<br><br>- false：表示不能在dock区域隐藏。<br><br>**说明：**<br><br>该标签配置不生效。|布尔值|该标签可缺省，缺省值为false。|
|preferMultiWindowOrientation|标识当前UIAbility组件多窗布局方向：<br><br>- default：缺省值，参数不配置默认值，建议其他应用类配置。<br><br>- portrait：多窗布局方向为竖向，建议竖向游戏类应用配置。<br><br>- landscape：多窗布局方向为横向，配置后支持横屏悬浮窗和上下分屏，建议横向游戏类应用配置。<br><br>- landscape_auto：多窗布局动态可变为横向，需要配合API enableLandScapeMultiWindow/disableLandScapeMultiWindow使用，建议视频类应用配置。|字符串|该标签可缺省，缺省值为default。|
|continueType|标识当前UIAbility组件的跨端迁移类型。|字符串数组|该标签可缺省，缺省值为当前组件的名称。|
|continueBundleName|标识当前应用支持跨端迁移的其它应用名称列表。<br><br>**说明：**<br><br>不能配置为本应用包名，仅为了做异包名迁移使用。<br><br>从API version 13开始，支持该标签。|字符串数组|该标签可缺省，缺省值为空。|
|process|标识组件的进程名称。具体使用方式参考[进程模型定义](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/process-model-stage#%E5%85%B6%E4%BB%96%E8%BF%9B%E7%A8%8B%E7%B1%BB%E5%9E%8B)中的"静态指定进程"。<br><br>**说明：**<br><br>1. 仅在[PC/2in1](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#devicetypes%E6%A0%87%E7%AD%BE)和[Tablet](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#devicetypes%E6%A0%87%E7%AD%BE)设备上生效。<br><br>2. UIAbility组件和type为embeddedUI的ExtensionAbility组件标签一致时运行在同一个进程中。<br><br>3. 从API version 14开始，支持该标签。|字符串|该标签可缺省，缺省值为空。|

abilities示例：

1. {
2.   "abilities": [{
3.     "name": "EntryAbility",
4.     "srcEntry": "./ets/entryability/EntryAbility.ets",
5.     "launchType":"singleton",
6.     "description": "$string:description_main_ability",
7.     "icon": "$media:layered_image",
8.     "label": "$string:EntryAbility_label",
9.     "permissions": [],
10.     "metadata": [],
11.     "exported": true,
12.     "continuable": true,
13.     "skills": [{
14.       "actions": ["ohos.want.action.home"],
15.       "entities": ["entity.system.home"],
16.       "uris": []
17.     }],
18.     "backgroundModes": [
19.       "dataTransfer"
20.     ],
21.     "startWindowIcon": "$media:icon",
22.     "startWindowBackground": "$color:red",
23.     "removeMissionAfterTerminate": true,
24.     "orientation": "$string:orientation",
25.     "supportWindowMode": ["fullscreen", "split", "floating"],
26.     "maxWindowRatio": 3.5,
27.     "minWindowRatio": 0.5,
28.     "maxWindowWidth": 2560,
29.     "minWindowWidth": 1400,
30.     "maxWindowHeight": 300,
31.     "minWindowHeight": 200,
32.     "excludeFromMissions": false,
33.     "preferMultiWindowOrientation": "default",
34.     "isolationProcess": false,
35.     "continueType": [
36.       "continueType1",
37.       "continueType2"
38.     ],
39.     "continueBundleName": [
40.       "com.example.myapplication1",
41.       "com.example.myapplication2"
42.     ],
43.     "process": ":processTag"
44.   }]
45. }

## skills标签

该标签标识UIAbility组件或者ExtensionAbility组件能够接收的[Want](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/want-overview)的特征。

**表7** skills标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|actions|标识能够接收的Action值集合，取值通常为系统预定义的action值，也允许自定义。<br><br>一个skill中不建议配置多个action，否则可能导致无法匹配预期场景。详情请参考[常见action与entities](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/actions-entities)。|字符串数组|该标签可缺省，缺省值为空。|
|entities|标识能够接收的Entity值的集合。<br><br>一个skill中不建议配置多个entity，否则可能导致无法匹配预期场景。详情请参考[常见action与entities](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/actions-entities)。|字符串数组|该标签可缺省，缺省值为空。|
|uris|标识与Want中URI（Uniform Resource Identifier）相匹配的集合。|对象数组|该标签可缺省，缺省值为空。|
|permissions|标识当前UIAbility或ExtensionAbility组件的权限信息。其他应用访问该组件时，需要申请相应的权限。<br><br>一个数组元素为一个权限名称，不超过255字节，取值请参考[应用权限列表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-permissions)。|字符串数组|该标签可缺省，缺省值为空。|
|domainVerify|标识是否开启[域名校验](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-linking-startup#section4452103365213)。<br><br>- true：表示开启域名校验。<br><br>- false：表示不开启域名校验。|布尔值|该标签可缺省，缺省值为false。|

**表8** uris标签说明

说明

以下字符串类型的标签不支持使用资源索引的方式（$string）配置。

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|scheme|标识URI的协议名部分，常见的有http、https、file、ftp等。<br><br>**说明：**<br><br>从API 18开始，该标签在参与隐式Want匹配时不区分大小写。|字符串|uris中仅配置type时可以缺省，缺省值为空，否则不可缺省。|
|host|标识URI的主机地址部分，该标签只有当scheme配置时才生效。常见的方式：<br><br>- 域名方式，如example.com。<br><br>- IP地址方式，如10.10.10.1。<br><br>**说明：**<br><br>从API 18开始，该标签在参与隐式Want匹配时不区分大小写。|字符串|该标签可缺省，缺省值为空。|
|port|标识URI的端口部分。如http默认端口为80，https默认端口是443，ftp默认端口是21。该标签只有当scheme和host都配置时才生效。|字符串|该标签可缺省，缺省值为空。|
|path \| pathStartWith \| pathRegex|标识URI的路径部分，path、pathStartWith和pathRegex配置时三选一。path标识URI与want中的路径部分全匹配，pathStartWith标识URI与want中的路径部分允许前缀匹配，pathRegex标识URI与want中的路径部分允许正则匹配。该标签只有当scheme和host都配置时才生效。|字符串|该标签可缺省，缺省值为空。|
|type|标识与Want相匹配的数据类型，使用MIME（Multipurpose Internet Mail Extensions）类型规范和[UniformDataType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-data-uniformtypedescriptor)类型规范。可以与scheme同时配置，也可以单独配置。|字符串|该标签可缺省，缺省值为空。|
|utd|标识与Want相匹配的[标准化数据类型](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-data-uniformtypedescriptor)，适用于分享等场景。|字符串|该标签可缺省，缺省值为空。|
|maxFileSupported|对于指定类型的文件，标识一次能接收或打开的最大数量，适用于分享等场景，需要与utd配合使用。|整数|该标签可缺省，缺省值为0。|
|linkFeature|标识URI提供的功能类型（如文件打开、分享、导航等），用于实现应用间跳转。取值为长度不超过127字节的字符串，不支持中文。同一Bundle中声明的linkFeature数量不能超过150个。详情见[linkFeature标签说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-uri-config#linkfeature%E6%A0%87%E7%AD%BE%E8%AF%B4%E6%98%8E)。|字符串|该标签可缺省，缺省值为空。|

skills示例：

说明

如下示例为通用配置，部分组件和模块在实际配置时存在差异，例如[点击消息进入应用首页](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section697519219136)的限制，具体请参考对应文档说明。

1. {
2.   "abilities": [
3.     {
4.       "skills": [
5.         {
6.           "actions": [
7.             "ohos.want.action.home"
8.           ],
9.           "entities": [
10.             "entity.system.home"
11.           ],
12.           "uris": [
13.             {
14.               "scheme":"http",
15.               "host":"example.com",
16.               "port":"80",
17.               "path":"path",
18.               "type": "text/*",
19.               "linkFeature": "Login"
20.             }
21.           ],
22.           "permissions": [],
23.           "domainVerify": false
24.         }
25.       ]
26.     }
27.   ]
28. }

## extensionAbilities标签

描述extensionAbilities的配置信息，标签值为数组类型，该标签下的配置只对当前extensionAbilities生效。

**表9** extensionAbilities标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识当前ExtensionAbility组件的名称，确保该名称在整个应用中唯一，取值为长度不超过127字节的字符串。|字符串|该标签不可缺省。|
|srcEntry|标识当前ExtensionAbility组件所对应的代码路径，取值为长度不超过127字节的字符串。|字符串|该标签不可缺省。|
|description|标识当前ExtensionAbility组件的描述，开发者可以通过该标签描述当前组件的功能与作用，取值为长度不超过255字节的字符串，可以是对描述内容的资源索引，用于支持多语言。|字符串|该标签可缺省，缺省值为空。|
|icon|标识当前ExtensionAbility组件的图标，取值为资源文件的索引。|字符串|该标签可缺省，缺省值为空。|
|label|标识当前ExtensionAbility组件对用户显示的名称，取值为该名称的资源索引，以支持多语言，字符串长度不超过255字节。|字符串|该标签可缺省，缺省值为空。|
|type|标识当前ExtensionAbility组件的类型，支持的取值如下：<br><br>- form：卡片的ExtensionAbility。<br><br>- workScheduler：延时任务的ExtensionAbility。<br><br>- inputMethod：输入法的ExtensionAbility。<br><br>- share：提供内容分享处理功能的[ShareExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-shareextensionability)。<br><br>- accessibility：辅助能力的ExtensionAbility。<br><br>- fileShare：文件共享的ExtensionAbility。<br><br>- sysPicker/camera：拉起相机picker的ExtensionAbility。<br><br>- vpn：为开发者[提供VPN能力](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-vpnextensionability)的ExtensionAbility<br><br>- wallpaper：壁纸的ExtensionAbility。<br><br>- backup：数据备份的ExtensionAbility。<br><br>- enterpriseAdmin：[企业设备管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/mdm-kit-admin)的ExtensionAbility。企业设备管理应用必须拥有此类型的ExtensionAbility。<br><br>- thumbnail：获取文件缩略图的ExtensionAbility，开发者可以对自定义文件类型的文件提供缩略。<br><br>- preview：该ExtensionAbility会将文件解析后在一个窗口中显示，开发者可以通过将此窗口组合到其他应用窗口中。<br><br>- print：打印框架的ExtensionAbility。<br><br>- push：推送的ExtensionAbility。<br><br>- driver：驱动框架的ExtensionAbility。应用配置了driver类型的ExtensionAbility后会被视为驱动应用，驱动应用在安装、卸载和恢复时不会区分用户，且创建新用户时也会安装设备上已有的驱动应用。例如，创建子用户时会默认安装主用户已有的驱动应用，在子用户上卸载驱动应用时，主用户上对应的驱动应用也会同时被卸载。<br><br>- remoteNotification：远程通知的ExtensionAbility。<br><br>- remoteLocation：远程定位的ExtensionAbility。<br><br>- voip：网络音视频通话的ExtensionAbility。<br><br>- action：自定义操作业务模板的ExtensionAbility，为开发者提供基于UIExtension的自定义操作业务模板。<br><br>- embeddedUI：嵌入式UI扩展能力，提供跨进程界面嵌入的能力。<br><br>- insightIntentUI：为开发者提供能被小艺意图调用，以窗口形态呈现内容的扩展能力。<br><br>- ads：广告业务的ExtensionAbility，与AdComponent控件组合使用，将广告页面展示到其他应用中。仅支持设备厂商使用。<br><br>- photoEditor：图片编辑业务的ExtensionAbility，为开发者提供基于UIExtension的图片编辑业务模版。<br><br>- appAccountAuthorization：应用账号授权扩展能力的ExtensionAbility，用于处理账号授权请求，比如账号登录授权。<br><br>- autoFill/password：用于账号和密码自动填充业务的ExtensionAbility，支持数据的保存、填充能力。<br><br>- hms/account：应用账号管理能力的ExtensionAbility。<br><br>- autoFill/smart：用于情景化场景自动填充业务的ExtensionAbility，支持数据的保存、填充能力。<br><br>- statusBarView：[状态栏开放服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/statusbar-extension-introduction)的ExtensionAbility。<br><br>- liveViewLockScreen：实况窗锁屏沉浸态的ExtensionAbility。<br><br>- recentPhoto：最近照片推荐的ExtensionAbility。<br><br>- fence：地理围栏的ExtensionAbility。<br><br>- callerInfoQuery：企业联系人查询的ExtensionAbility。<br><br>- assetAcceleration：资源预下载的ExtensionAbility。<br><br>- formEdit：卡片编辑的ExtensionAbility。<br><br>- distributed：分布式扩展的ExtensionAbility。<br><br>- liveForm：互动卡片的[ExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-form-liveformextensionability)。从API version 20开始，支持该标签。<br><br>- appService：为应用提供后台服务相关扩展能力[AppServiceExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-appserviceextensionability)，包括后台服务的创建、销毁、连接、断开等生命周期回调。从API version 20开始，支持该标签。<br><br>- webNativeMessaging：为开发者提供Web原生消息通信能力的[ExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability)。从API version 21开始，支持该标签。<br><br>- faultLog：故障延迟通知的[ExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-hiviewdfx-faultlogextensionability)。从API version 21开始，支持该标签。|字符串|该标签不可缺省。|
|permissions|标识当前ExtensionAbility组件的权限信息。当其他应用访问该ExtensionAbility时，需要申请相应的权限。<br><br>一个数组元素为一个权限名称。不超过255字节，取值请参考[应用权限列表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-permissions)。|字符串数组|该标签可缺省，缺省值为空。|
|appIdentifierAllowList|标识允许启动此ExtensionAbility的应用程序列表。<br><br>一个数组元素为一个应用程序的appIdentifier，appIdentifier信息可参考[什么是appIdentifier](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/common_problem_of_application#%E4%BB%80%E4%B9%88%E6%98%AFappidentifier)。<br><br>**说明：**<br><br>仅当ExtensionAbility组件的type为appService时支持配置该标签。<br><br>从API version 20开始，支持该标签。|字符串数组|该标签可缺省，缺省值为空。|
|readPermission|标识读取当前ExtensionAbility组件数据所需的权限，取值为长度不超过255字节的字符串。仅当预置的系统应用ExtensionAbility的type配置为dataShare时，该标签生效。dataShare类型仅支持系统应用支持配置，三方应用配置不生效。|字符串|该标签可缺省，缺省值为空。|
|writePermission|标识向当前ExtensionAbility组件写数据所需的权限，取值为长度不超过255字节的字符串。仅当预置的系统应用ExtensionAbility的type配置为dataShare时，该标签生效。dataShare类型仅支持系统应用支持配置，三方应用配置不生效。|字符串|该标签可缺省，缺省值为空。|
|uri|标识当前ExtensionAbility组件提供的数据URI，取值为长度不超过255字节的字符数组，用反向域名的格式表示。<br><br>**说明：**<br><br>该标签在type为dataShare类型的ExtensionAbility时，不可缺省。|字符串|该标签可缺省，缺省值为空。|
|skills|标识当前ExtensionAbility组件能够接收的[Want](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/want-overview)的特征集。<br><br>配置规则：entry包可以配置多个具有入口能力的skills标签（配置了ohos.want.action.home和entity.system.home）的ExtensionAbility，其中第一个配置了skills标签的ExtensionAbility中的label和icon作为服务或应用的label和icon。<br><br>**说明：**<br><br>服务的Feature包不支持配置具有入口能力的skills标签。<br><br>应用的Feature包支持配置具有入口能力的skills标签。|数组|该标签可缺省，缺省值为空。|
|[metadata](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#metadata%E6%A0%87%E7%AD%BE)|标识当前ExtensionAbility组件的元信息。<br><br>**说明：**<br><br>该标签在type为form时，不可缺省，且必须存在一个name为ohos.extension.form的对象值，其对应的resource值不能缺省，为服务卡片的二级资源引用。|对象数组|该标签可缺省，缺省值为空。|
|exported|标识当前ExtensionAbility组件是否可以被其他应用调用。<br><br>- true：表示可以被其他应用调用。<br><br>- false：表示不可以被其他应用调用，包括无法被aa工具命令拉起应用。|布尔值|该标签可缺省，缺省值为false。|
|extensionProcessMode|标识当前ExtensionAbility组件的多进程实例模型,当前只对UIExtensionAbility以及从UIExtensionAbility扩展的ExtensionAbility生效。<br><br>- instance：表示该ExtensionAbility每个实例一个进程。<br><br>- type：表示该ExtensionAbility实例都运行在同一个进程里，与其他ExtensionAbility分离进程。<br><br>- bundle：表示该ExtensionAbility实例都运行在应用统一进程里，与其他配置了bundle模型的ExtensionAbility共进程。<br><br>- runWithMainProcess：表示该ExtensionAbility和应用主进程共进程，只有[状态栏开放服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/statusbar-extension-introduction)的ExtensionAbility可以配置runWithMainProcess。|字符串|该标签可缺省，缺省值为空。|
|dataGroupIds|标识当前ExtensionAbility组件的dataGroupId集合。如果当前ExtensionAbility组件所在的应用在应用市场申请的证书里groupIds也申请了某个dataGroupId，那么当前ExtensionAbility组件可以和应用共享这一个dataGroupId生成的目录，所以ExtensionAbility组件的dataGroupId需要是应用的签名证书中groupIds标签里配置的才能生效。 且该标签仅在当前ExtensionAbility组件存在独立的沙箱目录时生效。详见[dataGroupId申请流程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ime-kit-security#section4219152220459)。|字符串数组|该标签可缺省，缺省值为空。|
|process|标识组件的进程名称，只有type为embeddedUI时可以配置该标签。具体使用方式参考[进程模型定义](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/process-model-stage#%E5%85%B6%E4%BB%96%E8%BF%9B%E7%A8%8B%E7%B1%BB%E5%9E%8B)中的"静态指定进程"。<br><br>**说明：**<br><br>1. 仅在[PC/2in1](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#devicetypes%E6%A0%87%E7%AD%BE)和[Tablet](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#devicetypes%E6%A0%87%E7%AD%BE)设备上生效。<br><br>2. UIAbility组件和ExtensionAbility组件标签一致时运行在同一个进程中。<br><br>3. 从API version 14开始，支持该标签。|字符串|该标签可缺省，缺省值为空。|
|isolationProcess|标识ExtensionAbility组件能否运行在独立的进程中。<br><br>- true：表示能运行在独立的进程中。<br><br>- false：表示不能运行在独立的进程中。<br><br>**说明：**<br><br>仅当ExtensionAbility组件的type为"sys/commonUI"时该标签配置生效，且仅支持由系统应用配置type为"sys/commonUI"。<br><br>从API version 20开始，支持该标签。|布尔值|该标签可缺省，缺省值为false。|

extensionAbilities示例：

1. {
2.   "extensionAbilities": [
3.     {
4.       "name": "FormName",
5.       "srcEntry": "./form/MyForm.ts",
6.       "icon": "$media:icon",
7.       "label" : "$string:extension_name",
8.       "description": "$string:form_description",
9.       "type": "form",
10.       "permissions": ["ohos.permission.ACCESS_BLUETOOTH"],
11.       "exported": true,
12.       "uri":"scheme://authority/path/query",
13.       "skills": [{
14.         "actions": [],
15.         "entities": [],
16.         "uris": [],
17.         "permissions": []
18.       }],
19.       "metadata": [
20.         {
21.           "name": "ohos.extension.form",
22.           "resource": "$profile:form_config",
23.         }
24.       ],
25.       "extensionProcessMode": "instance",
26.       "dataGroupIds": [
27.         "testGroupId1"
28.       ]
29.     }
30.   ]
31. }

## shortcuts标签

shortcuts标识应用的快捷方式信息。标签值为数组，包含四个子标签shortcutId、label、icon、wants。

[metadata](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#metadata%E6%A0%87%E7%AD%BE)中指定shortcut信息，其中：

- name：指定shortcuts的名称，使用ohos.ability.shortcuts作为shortcuts信息的标识。
    
- resource：指定shortcuts信息的资源位置。
    

**表10** shortcuts标签说明

|属性名称|含义|类型|是否可缺省|
|:--|:--|:--|:--|
|shortcutId|标识快捷方式的ID，取值为长度不超过63字节的字符串。**不支持通过资源索引的方式（$string）配置该标签。**|字符串|该标签不可缺省。|
|label|标识快捷方式的标签信息，即快捷方式对外显示的文字描述信息。取值为长度不超过255字节的字符串，可以是描述性内容，也可以是标识label的资源索引。|字符串|该标签可缺省，缺省值为空。|
|icon|标识快捷方式的图标，取值为资源文件的索引。<br><br>**说明：**<br><br>图标分为单层图标和分层图标，单层图标包含一个图片，分层图标包含前景图和背景图，推荐使用如下配置的分层图标：<br><br>1.前景图：图标显示大小为450*450px，资源大小为1024*1024px的透明图层。<br><br>2.背景图：大小为1024*1024px。|字符串|该标签可缺省，缺省值为空。|
|visible|标识快捷方式是否显示，取值为true时显示快捷方式，取值为false时不显示快捷方式。<br><br>**说明：**<br><br>1.从API version 20开始，支持该标签。|布尔值|该标签可缺省，缺省为true。|
|[wants](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#wants%E6%A0%87%E7%AD%BE)|标识快捷方式内定义的目标wants信息集合，在调用launcherBundleManager的startShortcut接口时，会拉起wants标签里的第一个目标组件，推荐只配置一个wants元素。|对象|该标签可缺省，缺省为空。|

1. 在/resources/base/profile/目录下配置shortcuts_config.json配置文件。
    
    1. {
    2.   "shortcuts": [
    3.     {
    4.       "shortcutId": "id_test1",
    5.       "label": "$string:shortcut",
    6.       "icon": "$media:aa_icon",
    7.       "visible": true,
    8.       "wants": [
    9.         {
    10.           "bundleName": "com.ohos.hello",
    11.           "moduleName": "entry",
    12.           "abilityName": "EntryAbility",
    13.           "parameters": {
    14.             "testKey": "testValue"
    15.           }
    16.         }
    17.       ]
    18.     }
    19.   ]
    20. }
    
2. 在module.json5配置文件的abilities标签中，针对需要添加快捷方式的UIAbility进行配置metadata标签，使shortcut配置文件对该UIAbility生效。
    
    1. {
    2.   "module": {
    3.     // ...
    4.     "abilities": [
    5.       {
    6.         "name": "EntryAbility",
    7.         "srcEntry": "./ets/entryability/EntryAbility.ets",
    8.         // ...
    9.         "skills": [
    10.           {
    11.             "entities": [
    12.               "entity.system.home"
    13.             ],
    14.             "actions": [
    15.               "ohos.want.action.home"
    16.             ]
    17.           }
    18.         ],
    19.         "metadata": [
    20.           {
    21.             "name": "ohos.ability.shortcuts",
    22.             "resource": "$profile:shortcuts_config"
    23.           }
    24.         ]
    25.       }
    26.     ]
    27.   }
    28. }
    

### wants标签

此标签用于标识快捷方式内定义的目标wants信息集合。

**表11** wants标签说明

|属性名称|含义|类型|是否可缺省|
|:--|:--|:--|:--|
|bundleName|表示快捷方式的目标包名。|字符串|该标签可缺省。|
|moduleName|表示快捷方式的目标模块名。|字符串|该标签可缺省。|
|abilityName|表示快捷方式的目标组件名。|字符串|该标签可缺省。|
|parameters|表示拉起快捷方式时的自定义数据，仅支持配置字符串类型的数据。其中键值均最大支持1024长度的字符串。|对象|该标签可缺省。|

data标签示例：

1. {
2.   "wants": [
3.     {
4.       "bundleName": "com.ohos.hello",
5.       "moduleName": "entry",
6.       "abilityName": "EntryAbility",
7.       "parameters": {
8.         "testKey": "testValue"
9.       }
10.     }
11.   ]
12. }

## distributionFilter标签

该标签用于定义HAP对应的细分设备规格的分发策略，以便在应用市场进行云端分发应用包时做精准匹配。

说明

该标签从API10及以后版本开始生效，API9及以前版本使用distroFilter标签。

- **适用场景：** 当一个工程中存在多个Entry，且多个Entry配置的deviceTypes存在交集时，则需要通过该标签进行区分。比如下面的两个Entry都支持tablet类型，就需要通过该标签进行区分。
    
    1. // entry1支持的设备类型
    2. {
    3.   "module": {
    4.     "name": "entry1",
    5.     "type": "entry",
    6.     "deviceTypes" : [
    7.       "tv",
    8.       "tablet"
    9.     ]
    10.   }
    11. }
    
    12. // entry2支持的设备类型
    13. {
    14.   "module": {
    15.     "name": "entry2",
    16.     "type": "entry",
    17.     "deviceTypes" : [
    18.       "car",
    19.       "tablet"
    20.     ]
    21.   }
    22. }
    
- **配置规则：** 该标签支持配置四个属性，包括屏幕形状([screenShape](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#screenshape%E6%A0%87%E7%AD%BE))、窗口分辨率([screenWindow](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#screenwindow%E6%A0%87%E7%AD%BE))、屏幕像素密度([screenDensity](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#screendensity%E6%A0%87%E7%AD%BE) )、设备所在国家与地区([countryCode](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#countrycode%E6%A0%87%E7%AD%BE))。详见下表。
    
    在分发应用包时，通过deviceTypes与这四个属性的匹配关系，唯一确定一个用于分发到设备的HAP。
    
    - 如果需要配置该标签，则至少包含一个属性。
    - 如果一个Entry中配置了任意一个或多个属性，则其他Entry也必须包含相同的属性。
    - screenShape和screenWindow属性仅适用于轻量级智能穿戴设备。
- **配置方式：** 该标签需要配置在/resources/base/profile资源目录下，并在metadata的resource标签中引用。
    

**表12** distributionFilter标签配置说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|[screenShape](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#screenshape%E6%A0%87%E7%AD%BE)|标识屏幕形状的支持策略。|对象数组|该标签可缺省，缺省值为空。|
|[screenWindow](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#screenwindow%E6%A0%87%E7%AD%BE)|标识应用运行时的窗口分辨率的支持策略。|对象数组|该标签可缺省，缺省值为空。|
|[screenDensity](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#screendensity%E6%A0%87%E7%AD%BE)|标识屏幕的像素密度（dpi：Dot Per Inch）的支持策略。|对象数组|该标签可缺省，缺省值为空。|
|[countryCode](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#countrycode%E6%A0%87%E7%AD%BE)|标识国家与地区的支持策略，取值参考ISO-3166-1标准。支持多个国家和地区枚举定义。|对象数组|该标签可缺省，缺省值为空。|

### screenShape标签

**表13** screenShape标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|policy|标识条件属性的过滤规则。<br><br>- exclude：表示需要排除的value属性。<br><br>- include：表示需要包含的value属性。|字符串|该标签不可缺省。|
|value|支持的取值为circle（圆形）、rect（矩形）。例如，针对智能穿戴设备，可为圆形表盘和矩形表盘分别提供不同的HAP。|字符串数组|该标签不可缺省。|

### screenWindow标签

**表14** screenWindow标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|policy|标识条件属性的过滤规则。当前取值仅支持“include”。<br><br>- include：表示需要包含的value属性。|字符串|该标签不可缺省。|
|value|单个字符串的取值格式为“宽 * 高”，取值为整数像素值，例如“454 * 454”。|字符串数组|该标签不可缺省。|

### screenDensity标签

**表15** screenDensity标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|policy|标识条件属性的过滤规则。<br><br>- exclude：表示需要排除的value属性。<br><br>- include：表示需要包含的value属性。|字符串|该标签不可缺省。|
|value|标识屏幕的像素密度（dpi :Dot Per Inch）。支持的取值如下：<br><br>- sdpi：表示小规模的屏幕密度（Small-scale Dots per Inch），适用于dpi取值为(0,120]的设备。<br><br>- mdpi：表示中规模的屏幕密度（Medium-scale Dots Per Inch），适用于dpi取值为(120,160]的设备。<br><br>- ldpi：表示大规模的屏幕密度（Large-scale Dots Per Inch），适用于dpi取值为(160,240]的设备。<br><br>- xldpi：表示大规模的屏幕密度（Extra Large-scale Dots Per Inch），适用于dpi取值为(240,320]的设备。<br><br>- xxldpi：表示大规模的屏幕密度（Extra Extra Large-scale Dots Per Inch），适用于dpi取值为(320，480]的设备。<br><br>- xxxldpi：表示大规模的屏幕密度（Extra Extra Extra Large-scale Dots Per Inch），适用于dpi取值为(480, 640]的设备。|字符串数组|该标签不可缺省。|

### countryCode标签

**表16** countryCode标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|policy|标识条件属性的过滤规则。<br><br>- exclude：表示需要排除的value属性。<br><br>- include：表示需要包含的value属性。|字符串|该标签不可缺省。|
|value|标识应用需要分发的国家地区码。|字符串数组|该标签不可缺省。|

示例如下：

1. 在开发视图的resources/base/profile下定义配置文件，文件名为distributionFilter_config.json，文件名可以自定义。
    
    1. {
    2.   "distributionFilter": {
    3.     "screenShape": {
    4.       "policy": "include",
    5.       "value": [
    6.         "circle",
    7.         "rect"
    8.       ]
    9.     },
    10.     "screenWindow": {
    11.       "policy": "include",
    12.       "value": [
    13.         "454*454",
    14.         "466*466"
    15.       ]
    16.     },
    17.     "screenDensity": {
    18.       "policy": "exclude",
    19.       "value": [
    20.         "ldpi",
    21.         "xldpi"
    22.       ]
    23.     },
    24.     "countryCode": { // 支持在中国分发
    25.       "policy": "include",
    26.       "value": [
    27.         "CN"
    28.       ]
    29.     }
    30.   }
    31. }
    
2. 在module.json5配置文件的module标签中定义metadata信息。
    
    1. {
    2.   "module": {
    3.     // ...
    4.     "metadata": [
    5.       {
    6.         "name": "ohos.module.distribution",
    7.         "resource": "$profile:distributionFilter_config",
    8.       }
    9.     ]
    10.   }
    11. }
    

## testRunner标签

此标签用于支持对测试框架的配置。

**表17** testRunner标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识测试框架对象名称，取值为长度不超过255字节的字符串。|字符串|不可缺省。|
|srcPath|标识测试框架代码路径，取值为长度不超过255字节的字符串。|字符串|不可缺省。|

testRunner标签示例：

1. {
2.   "module": {
3.     // ...
4.     "testRunner": {
5.       "name": "myTestRunnerName",
6.       "srcPath": "etc/test/TestRunner.ts"
7.     }
8.   }
9. }

## atomicService标签

此标签用于支持对元服务的配置。此标签仅在app.json中将bundleType设置为atomicService时生效。

**表18** atomicService标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|preloads|标识元服务中预加载列表。|对象数组|该标签可缺省，缺省值为空。|
|resizeable|标识元服务是否支持自适应窗口大小显示。当标签配置成true时，平板横屏模式切换或者折叠屏展开关闭，会自适应屏幕窗口的宽高，使得屏幕显示正常。<br><br>**说明：**<br><br>1.从API version 20开始，支持该标签。<br><br>2.如果已经适配了平板横屏及折叠屏展开态显示，建议将该标签设置为true。<br><br>- true：表示元服务可以自适应窗口大小。<br><br>- false：表示元服务不可以自适应窗口大小。|布尔值|可缺省，缺省值为false。|

**表19** preloads标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|moduleName|标识元服务中当前模块被加载时，需预加载的模块名。不能配置自身modulename，且必须有对应的模块，取值为长度不超过31字节的字符串。|字符串|该标签不可缺省。|

atomicService标签示例：

1. {
2.   "module": {
3.     "atomicService": {
4.       "preloads":[
5.         {
6.           "moduleName":"feature"
7.         }
8.       ],
9.       "resizeable": true
10.     }
11.   }
12. }

## dependencies标签

此标签标识模块运行时依赖的共享库列表。

**表20** dependencies标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|bundleName|标识当前模块依赖的共享包包名。取值为长度7~128字节的字符串。|字符串|该标签可缺省，缺省值为空。|
|moduleName|标识当前模块依赖的共享包模块名。取值为长度不超过31字节的字符串。|字符串|该标签不可缺省。|
|versionCode|标识当前模块依赖的共享包的版本号。取值范围为0~2147483647。|数值|该标签可缺省，缺省值为空。|

dependencies标签示例：

1. {
2.   "module": {
3.     "dependencies": [
4.       {
5.         "bundleName":"com.share.library",
6.         "moduleName": "library",
7.         "versionCode": 10001
8.       }
9.     ]
10.   }
11. }

## proxyData标签

此标签标识模块提供的数据代理列表，仅限entry和feature配置。

**表21** proxyData标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|uri|标识用于访问该数据代理的URI，不同的数据代理配置的URI不可重复，且需要满足datashareproxy://当前应用包名/xxx的格式。取值为长度不超过255字节的字符串。|字符串|该标签不可缺省。|
|requiredReadPermission|标识从该数据代理中读取数据所需要的权限。若不配置，则其他应用无法使用该代理。非系统应用配置的权限的等级需为system_basic或system_core，系统应用配置的权限的等级没有限制。权限等级可以参考[权限列表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-permissions)。取值为长度不超过255字节的字符串。|字符串|该标签可缺省，缺省值为空。|
|requiredWritePermission|标识向该数据代理中写入数据所需要的权限。若不配置，则其他应用无法使用该代理。非系统应用配置的权限的等级需为system_basic或system_core，系统应用配置的权限的等级没有限制。权限等级可以参考[权限列表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-permissions)。取值为长度不超过255字节的字符串。|字符串|该标签可缺省，缺省值为空。|
|[metadata](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#metadata%E6%A0%87%E7%AD%BE)|标识该数据代理的元信息，只支持配置name和resource标签。|对象|该标签可缺省，缺省值为空。|

proxyData标签示例：

1. {
2.   "module": {
3.     "proxyData": [
4.       {
5.         "uri":"datashareproxy://com.ohos.datashare/event/Meeting",
6.         "requiredReadPermission": "ohos.permission.ACCESS_BLUETOOTH",
7.         "requiredWritePermission": "ohos.permission.ACCESS_BLUETOOTH",
8.         "metadata": {
9.           "name": "datashare_metadata",
10.           "resource": "$profile:datashare"
11.         }
12.       }
13.     ]
14.   }
15. }

## routerMap标签

此标签标识模块配置的路由表的路径。

routerMap配置文件描述模块的路由表信息，routerMap标签的值为数组类型。

**表22** routerMap标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识跳转页面的名称。取值为长度不超过1023字节的字符串。|字符串|该标签不可缺省。|
|pageSourceFile|标识页面在模块内的路径。取值为长度不超过255字节的字符串。|字符串|该标签不可缺省。|
|buildFunction|标识被@Builder修饰的函数，该函数描述页面的UI。取值为长度不超过1023字节的字符串。|字符串|该标签不可缺省。|
|[data](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#data%E6%A0%87%E7%AD%BE)|标识字符串类型的自定义数据，开发者自行扩展能力，可以通过[HapModuleInfo对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-bundlemanager-hapmoduleinfo)中routerMap集合对象下的data获取标签内容，该标签已由系统解析，无需开发者自行解析。 每个自定义数据字符串取值不超过128字节。|对象|该标签可缺省，缺省值为空。|
|[customData](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#customdata%E6%A0%87%E7%AD%BE)|标识任意类型的自定义数据，开发者自行扩展能力，可以通过[HapModuleInfo对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-bundlemanager-hapmoduleinfo)中routerMap集合对象下的customData获取标签内容，开发者需要调用JSON.parse函数解析出具体内容。总长度不超过4096字节。|对象|该标签可缺省，缺省值为空。|

示例如下：

1. 在开发视图的resources/base/profile下面定义配置文件，文件名可以自定义，例如：router_map.json。
    
    1. {
    2.   "routerMap": [
    3.     {
    4.       "name": "DynamicPage1",
    5.       "pageSourceFile": "src/main/ets/pages/pageOne.ets",
    6.       "buildFunction": "myFunction",
    7.       "customData": {
    8.         "stringKey": "data1",
    9.         "numberKey": 123,
    10.         "booleanKey": true,
    11.         "objectKey": {
    12.           "name": "test"
    13.         },
    14.         "arrayKey": [
    15.           {
    16.             "id": 123
    17.           }
    18.         ]
    19.       }
    20.     },
    21.     {
    22.       "name": "DynamicPage2",
    23.       "pageSourceFile": "src/main/ets/pages/pageTwo.ets",
    24.       "buildFunction": "myBuilder",
    25.       "data": {
    26.         "key1": "data1",
    27.         "key2": "data2"
    28.       }
    29.     }
    30.   ]
    31. }
    
2. 在module.json5配置文件的module标签中定义routerMap标签，指向定义的路由表配置文件，例如："routerMap": "$profile:router_map"。
    

### data标签

此标签用于支持在路由表中配置自定义的字符串数据。

data标签示例：

1. {
2.   "routerMap": [
3.     {
4.       "name": "DynamicPage",
5.       "pageSourceFile": "src/main/ets/pages/pageOne.ets",
6.       "buildFunction": "myBuilder",
7.       "data": {
8.         "key1": "data1",
9.         "key2": "data2"
10.       }
11.     }
12.   ]
13. }

### customData标签

此标签用于支持在路由表中配置自定义数据。

customData对象内部，可以配置任意类型的自定义数据。

customData标签示例：

1. {
2.   "routerMap": [
3.     {
4.       "name": "DynamicPage",
5.       "pageSourceFile": "src/main/ets/pages/pageOne.ets",
6.       "buildFunction": "myBuilder",
7.       "customData": {
8.         "stringKey": "data1",
9.         "numberKey": 123,
10.         "booleanKey": true,
11.         "objectKey": {
12.           "name": "test"
13.         },
14.         "arrayKey": [
15.           {
16.             "id": 123
17.           }
18.         ]
19.       }
20.     }
21.   ]
22. }

## appEnvironments标签

此标签标识模块配置的应用环境变量。

**表23** appEnvironments标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识环境变量的变量名称。取值为长度不超过4096字节的字符串。|字符串|该标签可缺省，缺省值为空。|
|value|标识环境变量的值。取值为长度不超过4096字节的字符串。|字符串|该标签可缺省，缺省值为空。|

appEnvironments标签示例：

1. {
2.   "module": {
3.     "appEnvironments": [
4.       {
5.         "name":"name1",
6.         "value": "value1"
7.       }
8.     ]
9.   }
10. }

## hnpPackages标签

该标签标识应用包含的Native软件包信息。

**表24** hnpPackages标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|package|标识Native软件包名称。|字符串|该标签不可缺省。|
|type|标识Native软件包类型。支持的取值如下：<br><br>- public：公有类型。<br><br>- private：私有类型。|字符串|该标签不可缺省。|

hnpPackages示例：

1. {
2.   "module" : {
3.     "hnpPackages": [
4.       {
5.         "package": "hnpsample.hnp",
6.         "type": "public"
7.       }
8.     ]
9.   }
10. }

## fileContextMenu标签

该标签标识当前HAP的右键菜单配置项，是一个profile文件资源，用于指定描述应用注册右键菜单配置文件。仅在PC/2in1设备上生效。仅允许在entry类型模块中配置。

fileContextMenu标签示例

1. {
2.   "module": {
3.     // ...
4.     "fileContextMenu": "$profile:menu" // 通过profile下的资源文件配置
5.   }
6. }

在开发视图的resources/base/profile下面定义配置文件menu.json，其中文件名“menu.json”可自定义，需要和fileContextMenu标签指定的信息对应。配置文件中描述了当前应用注册的右键菜单的项目和响应行为。

配置文件根节点名称为fileContextMenu，为对象数组，标识当前module注册右键菜单的数量。（单模块和单应用注册数量不能超过5个，配置超过数量当前只解析随机5个）

**表25** fileContextMenu标签配置说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|abilityName|表示当前右键菜单对应的需要拉起的ability名称。|字符串|不可缺省。|
|menuItem|右键菜单显示的信息。命名建议：<br><br>原则一：[动作]+[应用名]，中文示例：用{App}打开、用{App} ({Plugin}插件) 打开；英文示例：Open with {App}、Open with {App} ({Plugin})。<br><br>原则二：[动作]+[目的]，示例：压缩为{文件名}、压缩至{路径}、用{App}转换为{格式}。|资源id|不可缺省。|
|menuHandler|一个ability可以创建多个右键菜单， 该标签与右键菜单显示项一一对应，用于区分用户拉起的不同右键菜单项。开发者可自定义该标签取值，确保该标签在整个ability中唯一。在用户点击右键菜单拉起应用时，会作为参数传递给应用。|字符串|不可缺省。|
|menuContext|定义展示该菜单项需要的上下文，可以支持多种情况，类型为数组。|对象数组|不可缺省。|

**表26** menuContext标签配置说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|menuKind|表示单击如下类型时会触发右键菜单。取值范围如下：<br><br>- 0：空白处<br><br>- 1：文件<br><br>- 2：文件夹<br><br>- 3：文件和文件夹|数值|不可缺省。|
|menuRule|表示采用什么方式选择文件或文件夹时，会触发右键菜单。取值范围如下：<br><br>- single：单选<br><br>- multi：多选<br><br>- both：单选或多选|字符串|仅当menuKind为1或2时，才会读取该标签，此时不可缺省。|
|fileSupportType|表示当选中的文件列表里包含指定的文件类型时，显示右键菜单。<br><br>当该标签取值为["*"]时，将会读取fileNotSupportType标签。<br><br>当该标签取值为[]时，将不做任何处理。|字符串数组|仅当menuKind为1时，才会读取该标签，此时不可缺省。|
|fileNotSupportType|表示当选中的文件列表里包含这些文件类型时，不显示该右键菜单。<br><br>仅当menuKind为1、且fileSupportType为["*"]时，才会读取该标签。|字符串数组|可缺省，缺省值为空。|

resources/base/profile路径下的menu.json资源文件示例如下：

1. {
2.   "fileContextMenu": [
3.     {
4.       "abilityName": "EntryAbility",
5.       "menuItem": "$string:module_desc",
6.       "menuHandler": "openCompress",
7.       "menuContext": [
8.         {
9.           "menuKind": 0
10.         },
11.         {
12.           "menuKind": 1,
13.           "menuRule": "both",
14.           "fileSupportType": [
15.             ".rar",
16.             ".zip"
17.           ],
18.           "fileNotSupportType": [
19.             ""
20.           ]
21.         },
22.         {
23.           "menuKind": 2,
24.           "menuRule": "single"
25.         },
26.         {
27.           "menuKind": 3
28.         }
29.       ]
30.     }
31.   ]
32. }

**响应行为**

应用进行右键扩展菜单注册后，在文件管理器通过右键操作拉起菜单，该菜单中会有“更多”选项。单击“更多”选项后，会出现注册后的menuItem列表，单击任意一个选项后，文件管理器默认通过startAbility的方式拉起三方应用，除了指定三方应用的包名和ability名之外，want中的parameter中，也会传入如下标签：

**表27** want中parameter标签说明

|参数名|值|类型|
|:--|:--|:--|
|menuHandler|对应注册配置文件中menuHandler的值。|字符串|
|uriList|用户在具体文件上触发右键的uri值，如果空白处响应，此值为空，单个文件响应，数组长度1，多个文件响应则传入对应所有文件的uri值。|字符串数组|

## startWindow标签

该标签指向一个profile文件资源，用于指定UIAbility组件启动页面的配置文件，在开发视图的resources/base/profile下面定义配置文件start_window.json，如果配置了该标签，startWindowIcon和startWindowBackground标签将不生效。

**说明：**

从API version 19开始，支持使用该字段配置增强启动页。

**表28** startWindow标签配置说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|startWindowType|标识当前UIAbility组件是否隐藏启动页。<br><br>当前仅支持在2in1设备或平板设备的自由多窗模式下使用。<br><br>不同取值含义如下：<br><br>- "REQUIRED_SHOW"：强制显示启动页。不受[Ability管理服务（即StartOptions中hideStartWindow标签）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-startoptions#startoptions)的影响。<br><br>- "REQUIRED_HIDE"：强制隐藏启动页。不受[Ability管理服务（即StartOptions中hideStartWindow标签）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-startoptions#startoptions)的影响。<br><br>- "OPTIONAL_SHOW"：可选显示，默认行为为显示启动页，如果[Ability管理服务（即StartOptions中hideStartWindow标签）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-startoptions#startoptions)设置隐藏启动页，则隐藏启动页。<br><br>- 如未配置该标签，默认取值为"REQUIRED_SHOW"，即强制显示启动页。<br><br>从API version 20开始支持该标签。|字符串|可缺省，缺省值为REQUIRED_SHOW。|
|startWindowAppIcon|标识当前UIAbility组件启动页面图标资源文件的索引，取值为长度不超过255字节的字符串。<br><br>从API version 19开始支持该字段。|字符串|可缺省，缺省值为空。|
|startWindowIllustration|标识当前UIAbility组件启动页面插画资源文件的索引，取值为长度不超过255字节的字符串。<br><br>从API version 19开始支持该字段。|字符串|可缺省，缺省值为空。|
|startWindowBrandingImage|标识当前UIAbility组件启动页面品牌标识资源文件的索引，取值为长度不超过255字节的字符串。<br><br>从API version 19开始支持该字段。|字符串|可缺省，缺省值为空。|
|startWindowBackgroundColor|标识当前UIAbility组件启动页面背景颜色资源文件的索引，取值为长度不超过255字节的字符串。<br><br>从API version 19开始支持该字段。|字符串|不可缺省。|
|startWindowBackgroundImage|标识当前UIAbility组件启动页面背景图片资源文件的索引，取值为长度不超过255字节的字符串。<br><br>从API version 19开始支持该字段。|字符串|可缺省，缺省值为空。|
|startWindowBackgroundImageFit|标识当前UIAbility组件启动页面背景图像适应方式，支持的取值如下：<br><br>- Contain：按照宽高比进行缩小或放大，图片完全显示在显示边界内。<br><br>- Cover：按照宽高比进行缩小或放大，图片两边都大于或等于显示边界。<br><br>- Auto：自适应显示。<br><br>- Fill：不按照宽高比进行放大或缩小，图片充满显示边界。<br><br>- ScaleDown：按照宽高比显示，图片缩小或保持不变。<br><br>- None：保持原有尺寸显示。<br><br>从API version 19开始支持该字段。|字符串|可缺省，缺省值为Cover。|
|startWindowColorModeType|标识当前UIAbility组件启动页深浅色模式，仅作用于同进程间拉起场景。<br><br>不同取值含义如下：<br><br>- "FOLLOW_SYSTEM"：启动页颜色模式跟随系统深浅色。<br><br>- "FOLLOW_APPLICATION"：启动页颜色模式跟随应用深浅色。<br><br>- 如未配置该字段，默认取值为"FOLLOW_SYSTEM"，即启动页颜色模式跟随系统深浅色。<br><br>从API version 20开始支持该字段。|字符串|可缺省，缺省值为FOLLOW_SYSTEM。|

resources/base/profile路径下的start_window.json资源文件示例如下：

1. {
2.   "startWindowType": "REQUIRED_SHOW",
3.   "startWindowColorModeType": "FOLLOW_SYSTEM",
4.   "startWindowAppIcon": "$media:start_window_app_icon",
5.   "startWindowIllustration": "$media:start_window_illustration",
6.   "startWindowBrandingImage": "$media:start_window_branding_image",
7.   "startWindowBackgroundColor": "$color:start_window_back_ground_color",
8.   "startWindowBackgroundImage": "$media:start_window_back_ground_image",
9.   "startWindowBackgroundImageFit": "Cover"
10. }

## systemTheme标签

该标签指向一个profile文件资源，用于指定当前应用使用的系统主题配置文件。从API version 20开始，支持该标签。

systemTheme标签示例：

1. {
2.   "module": {
3.     // ...
4.     "systemTheme": "$profile:theme_config", // 通过profile下的资源文件配置
5.   }
6. }

在开发视图的resources/base/profile下面定义配置文件theme_config.json，其中文件名“theme_config.json”可自定义为“theme_config”开头文件名，例如"theme_config"、"theme_config_1"。需要和systemTheme标签指定的信息对应。配置文件中标识当前应用使用的系统主题。

**表29** theme_config.json配置说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|systemTheme|标识当前应用使用的系统主题，取值为引用系统主题名称的枚举。枚举支持的取值如下：<br><br>- $ohos:theme:ohos_theme 系统默认的主题|字符串|该标签不可缺省。|

resources/base/profile路径下的theme_config.json资源文件示例如下：

1. {
2.   "systemTheme": "$ohos:theme:ohos_theme"
3. }

## requiredDeviceFeatures标签

**表30** requiredDeviceFeatures标签说明

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|phone|手机设备需要支持的设备特性，当前支持取值如下：<br><br>- large_screen：表示设备需要支持[大屏横屏](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-multi-device-screen-layout#section6493354468)。|字符串数组|可缺省，缺省值为空。|

requiredDeviceFeatures示例：

1. {
2.   "module": {
3.     "requiredDeviceFeatures": {
4.       "phone": [
5.         "large_screen"
6.       ]
7.     },
8.   }
9. }
# 应用配置文件概述（FA模型）

更新时间: 2025-12-16 16:34

每个应用项目必须在项目的代码目录下加入配置文件，这些配置文件会向编译工具、操作系统和应用市场提供描述应用的基本信息。

应用配置文件需要声明以下内容：

- 应用的软件Bundle名称，应用的开发厂商，版本号等应用的基本配置信息，这些信息被要求设置在app这个字段下。
    
- 应用的组件的基本信息，包括所有的Ability，设备类型，组件的类型以及当前组件所使用的语法类型。
    
- 应用在具体设备上的配置信息，这些信息会影响应用在设备上的具体功能。
    

在FA模型的应用开发过程中，需要在config.json配置文件中对应用的包结构进行声明。

## 配置文件的内部结构

config.json由app、deviceConfig和module三个部分组成，缺一不可。

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|[app](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-structure)|标识应用的全局配置信息。同一个应用的不同HAP的app配置必须保持一致。|对象|不可缺省。|
|[deviceConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/deviceconfig-structure)|标识应用在具体设备上的配置信息。|对象|不可缺省。|
|[module](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-structure)|标识HAP的配置信息。该标签下的配置只对当前HAP生效。|对象|不可缺省。|

config.json示例：

1. {
2.   "app": {
3.     "vendor": "example",
4.     "bundleName": "com.example.demo",
5.     "version": {
6.       "code": 1000000,
7.       "name": "1.0.0"
8.     }
9.   },
10.   "deviceConfig": {
11.   },
12.   "module": {
13.     "mainAbility": ".MainAbility_entry",
14.     "deviceType": [
15.       "tablet"
16.     ],
17.     "commonEvents": [
18.       {
19.         "name": ".EntryAbility",
20.         "permission": "ohos.permission.GET_BUNDLE_INFO",
21.         "data": [
22.           "com.example.demo",
23.           "100"
24.         ],
25.         "events": [
26.           "install",
27.           "update"
28.         ]
29.       }
30.     ],
31.     "abilities": [
32.       {
33.         "skills": [
34.           {
35.             "entities": [
36.               "entity.system.home"
37.             ],
38.             "actions": [
39.               "action.system.home"
40.             ]
41.           }
42.         ],
43.         "orientation": "unspecified",
44.         "visible": true,
45.         "srcPath": "MainAbility_entry",
46.         "name": ".MainAbility_entry",
47.         "srcLanguage": "ets",
48.         "icon": "$media:icon",
49.         // $string:MainAbility_entry_desc为资源索引
50.         "description": "$string:MainAbility_entry_desc",
51.         "formsEnabled": false,
52.         // $string:MainAbility_entry_label为资源索引
53.         "label": "$string:MainAbility_entry_label",
54.         "type": "page",
55.         "launchType": "multiton"
56.       }
57.     ],
58.     "distro": {
59.       "moduleType": "entry",
60.       "installationFree": false,
61.       "deliveryWithInstall": true,
62.       "moduleName": "myapplication"
63.     },
64.     "package": "com.example.myapplication",
65.     "srcPath": "",
66.     "name": ".myapplication",
67.     "js": [
68.       {
69.         "mode": {
70.           "syntax": "ets",
71.           "type": "pageAbility"
72.         },
73.         "pages": [
74.           "pages/index"
75.         ],
76.         "name": ".MainAbility_entry",
77.         "window": {
78.           "designWidth": 720,
79.           "autoDesignWidth": false
80.         }
81.       }
82.     ]
83.   }
84. }
# app对象内部结构

更新时间: 2025-12-16 16:34

app对象包含应用全局配置信息，内部结构如下：

**表1** **app对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|bundleName|标识应用的Bundle名称，用于标识应用的唯一性。Bundle名称是由字母、数字、下划线（_）和点号（.）组成的字符串，必须以字母开头。支持的字符串长度为7~128字节。Bundle名称通常采用反向域名形式表示（例如，"com.example.myapplication"）。建议第一级为域名后缀"com"，第二级为厂商/个人名，也可以采用多级。|字符串|不可缺省。|
|vendor|标识对应用开发厂商的描述。字符串长度不超过255字节。|字符串|可缺省，缺省值为空。|
|version|标识应用的版本信息。|对象|不可缺省。|
|apiVersion|标识应用程序所依赖的操作系统 API版本。|对象|可缺省，缺省值为空。|
|smartWindowSize|标识应用在模拟器中运行时使用的屏幕尺寸。|字符串|可缺省，缺省值为空。|
|smartWindowDeviceType|标识应用在模拟器中运行时可以模拟的设备。|字符串数组|可缺省，缺省值为空。|
|asanEnabled|标识应用程序是否开启asan检测，用于辅助定位buffer越界造成的crash问题。<br><br>- true：当前工程开启asan检测。<br><br>- false：当前工程不开启asan检测。|布尔值|可缺省，缺省值false。|

## version对象内部结构

**表2** **version对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识应用的版本号，用于向应用的终端用户呈现。取值可以自定义，长度不超过127字节。自定义规则如下：API5及更早的版本：推荐使用三段数字版本号（也兼容两段式版本号），如A.B.C（也兼容A.B），其中A、B、C取值为0-999范围内的整数。除此之外不支持其他格式。<br><br>A段，一般表示主版本号（Major）。<br><br>B段，一般表示次版本号（Minor）。<br><br>C段，一般表示修订版本号（Patch）。API6版本起：推荐采用四段式数字版本号，如A.B.C.D，其中A、B、C取值为0-99范围内的整数，D的取值为0-999范围内的整数。<br><br>A段，一般表示主版本号（Major）。<br><br>B段，一般表示次版本号（Minor）。<br><br>C段，一般表示特性版本号（Feature）。<br><br>D段，一般表示修订版本号（Patch）。|数值|不可缺省。|
|code|标识应用的版本号，仅用于操作系统管理该应用，不对应用的终端用户呈现。取值规则如下：API5及更早版本：二进制32位以内的非负整数，需要从version.name的值转换得到。转换规则为：code值=A * 1,000,000 + B * 1,000 + C例如，version.name字段取值为2.2.1，则code值为2002001。API6版本起：code的取值不与version.name字段的取值关联，开发者可自定义code取值，取值范围为2^31以内的非负整数，但是每次应用版本的更新，均需要更新code字段的值，新版本code取值必须大于旧版本code的值。|数值|不可缺省。|
|minCompatibleVersionCode|标识应用可兼容的最低版本号，用于跨设备场景下，判断其他设备上该应用的版本是否兼容。格式与version.code字段的格式要求相同。|数值|可缺省，缺省值为code标签值。|

## apiVersion内部结构

**表3** **apiVersion内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|compatible|运行应用所需要的最低API版本，取值范围为0~2147483647。|数值|配置在build.profile中，打包时由DevEco Studio填充到config.json中。|
|target|用于标识应用运行时使用的API版本，取值范围为0~2147483647。|数值|配置在build.profile中，打包时由DevEco Studio填充到config.json中。|
|releaseType|用于标识应用运行时SDK的状态。<br><br>canary：面向特定开发者早期预览版本，不承诺质量，不承诺API稳定。<br><br>beta：公开发布的Beta版本，早期Beta版本不承诺API稳定，经历若干次发布后，通过Release Notes对开发者声明该Beta版本为API稳定里程碑，后续版本的API冻结。<br><br>release：正式发布版本，承诺质量，API不可变更。当版本处于此状态时版本号中不呈现Stage字段。|字符串|配置在build.profile中，打包时由DevEco Studio填充到config.json中。|

app对象示例

1. "app": {
2.     "bundleName": "com.example.myapplication",
3.     "vendor": "example",
4.     "version": {
5.       "code": 8,
6.       "name": "8.0.1"
7.     },
8.     "apiVersion": {
9.       "compatible": 8,
10.       "target": 9,
11.       "releaseType": "Beta1"
12.     }
13.   }
# deviceConfig内部结构

更新时间: 2025-12-16 16:34

deviceConfig 包含设备上的应用配置信息，支持 default、tv、car、wearable 等属性。

## deviceConfig对象内部结构

**表1** **deviceConfig对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|default|配置为default类型的应用，虽然可以正常编译构建，但是不支持发布上架。建议使用phone替代。|对象|可缺省，缺省值为空。|
|tablet|标识平板特有的应用配置信息。|对象|可缺省，缺省值为空。|
|tv|标识智慧屏特有的应用配置信息。|对象|可缺省，缺省值为空。|
|car|标识车机特有的应用配置信息。|对象|可缺省，缺省值为空。|
|wearable|标识智能穿戴特有的应用配置信息。|对象|可缺省，缺省值为空。|
|2in1|标识PC设备，主要交互方式以多窗口、多任务及键盘鼠标操作为主，充分发挥设备的生产力属性。|对象|可缺省，缺省值为空。|
|phone|标识手机特有的应用配置信息。|对象|可缺省，缺省值为空。|
|liteWearable|标识运动手表特有的应用配置信息。|对象|可缺省，缺省值为空。|

上表中各设备对象的内部结构说明参见[deviceConfig设备对象内部结构](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/deviceconfig-structure#deviceconfig%E8%AE%BE%E5%A4%87%E5%AF%B9%E8%B1%A1%E5%86%85%E9%83%A8%E7%BB%93%E6%9E%84)。

## deviceConfig设备对象内部结构

**表2** **deviceConfig设备对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|process|标识应用或Ability的进程名。如果在deviceConfig标签下配置了process标签，则应用的所有Ability运行在此进程中。如果在abilities标签下为某个Ability配置了process标签，则该Ability运行在此进程中。该标签最大长度为31。|字符串|可缺省，缺省值为空。|
|keepAlive|标识应用是否始终保持运行状态，仅支持系统应用配置，三方应用配置不生效。<br><br>- true：应用始终保持为运行状态。系统启动时，该应用会被系统驱动起来。应用进程退出后，系统也会重新启动应用进程。<br><br>- false：应用不会始终保持为运行状态。系统启动时，该应用不会被系统驱动起来。应用进程退出后，系统不会重新启动应用进程。|布尔类型|可缺省，缺省值为false。|
|supportBackup|标识应用是否支持备份和恢复。<br><br>- true：该应用支持执行备份或恢复操作。<br><br>- false：该应用不支持执行备份或恢复操作。|布尔类型|可缺省，缺省值为false。|
|compressNativeLibs|该字段在打包HAP时标识libs库是否以压缩方式存储。<br><br>- true：libs库以压缩方式存储。<br><br>- false：libs库以不压缩方式存储。<br><br>在应用安装时，该字段用于标识libs库是否需要解压出来（API16及之后版本支持，之前的版本均默认解压libs库）。<br><br>- true：解压。<br><br>- false：不解压。|布尔类型|该标签可缺省。打包HAP时缺省值为false，安装应用时未配置则默认为true。|
|network|标识网络安全性配置。该标签允许应用通过配置文件的安全声明自定义其网络安全，无需修改应用代码。|对象|可缺省，缺省值为空。|

## network对象内部结构

**表3** **network对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|cleartextTraffic|标识是否允许应用使用明文网络流量（例如，明文HTTP）。<br><br>- true：允许应用使用明文流量的请求。<br><br>- false：拒绝应用使用明文流量的请求。|布尔类型|可缺省，缺省值为false。|
|securityConfig|标识应用的网络安全配置信息。|对象|可缺省，缺省为空。|

## securityConfig对象内部结构

**表4** **securityConfig对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|domainSettings|标识自定义网域范围的安全配置，支持多层嵌套。一个domainSettings对象中可嵌套更小网域范围的domainSettings对象。|对象类型|可缺省，缺省为空。|

## domainSettings对象内部结构

**表5** **domainSettings对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|cleartextPermitted|标识自定义网域范围内是否允许明文流量传输。cleartextTraffic和securityConfig同时存在时，以cleartextPermitted的值为准。<br><br>- true：允许明文流量传输。<br><br>- false：拒绝明文流量传输。|布尔类型|可缺省，缺省值为false。|
|domains|标识域名配置信息，包含两个参数：subdomains和name。<br><br>- subdomains：表示是否包含子域名。取值为"true"时，表示该规则将与相应网域及所有子网域（包括子网域的子网域）匹配；取值为"false"时，规则仅适用于精确匹配项。<br><br>- name：表示域名名称，为字符串类型。|对象数组|可缺省，缺省值为空。|

以下是deviceConfig的示例：

1. "deviceConfig": {
2.   "default": {
3.     "process": "com.example.test.example",
4.     "supportBackup": false,
5.     "network": {
6.       "cleartextTraffic": true,
7.       "securityConfig": {
8.         "domainSettings": {
9.           "cleartextPermitted": true,
10.           "domains": [
11.             {
12.               "subdomains": true,
13.               "name": "example.ohos.com"
14.             }
15.           ]
16.         }
17.       }
18.     }
19.   }
20. }
# module对象内部结构

更新时间: 2025-12-16 16:34

module对象包含HAP的配置信息。

**表1** **module对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|mainAbility|服务中心图标露出的Ability，常驻进程拉起时会启动mainAbility。|字符串|可缺省，缺省值为空。|
|package|标识HAP的包结构名称，在应用内保证唯一性。采用反向域名格式（建议与HAP的工程目录保持一致）。字符串长度为1-127个字节。|字符串|不可缺省。|
|name|标识HAP的类名。采用反向域名方式标识，前缀要与同级的package标签指定的包名一致，也可采用"."开头的命名方式。字符串长度不超过255字节。|字符串|可缺省，缺省值为空。|
|description|标识HAP的描述信息。字符串长度不超过255字节。如果字符串超出长度或者需要支持多语言，可以采用资源索引的方式添加描述内容。|字符串|可缺省，缺省值为空。|
|supportedModes|标识应用支持的运行模式，当前只定义了驾驶模式（drive）。该标签只适用于车机。|字符串数组|可缺省，缺省值为空。|
|deviceType|标识允许Ability运行的设备类型。系统预定义的设备类型包括：tablet(平板)、tv（智慧屏）、car(车机)、wearable(智能穿戴)、litewearable(运动表)等。|字符串数组|不可缺省。|
|distro|标识HAP发布的具体描述。|对象|不可缺省。|
|metaData|标识HAP的元信息。|对象|可缺省，缺省值为空。|
|abilities|标识当前模块内的所有Ability。采用对象数据格式。|对象数组|可缺省，缺省值为空。|
|js|标识基于ArkUI框架开发的JS模块集合，其中的每个元素代表一个JS模块的信息。|对象数组|可缺省，缺省值为空。|
|shortcuts|标识应用的快捷方式信息。采用对象数组格式，其中的每个元素表示一个快捷方式对象。|对象数组|可缺省，缺省值为空。|
|reqPermissions|标识应用运行时向系统申请的权限。|对象数组|可缺省，缺省值为空。|
|colorMode|标识应用自身的颜色模式，目前支持如下三种模式：<br><br>- dark：表示按照深色模式选取资源。<br><br>- light：表示按照浅色模式选取资源。<br><br>- auto：表示跟随系统的颜色模式值选取资源。|字符串|可缺省，缺省值为"auto"。|
|distroFilter|该标签下的子标签均为可选字段，用于定义HAP对应的细分设备规格的分发策略，以便应用市场在云端分发HAP时做精准匹配。该标签需要配置在/resource/profile资源目录下；在进行分发时，通过deviceType与下表属性的匹配关系，唯一确定一个用于分发到设备的HAP。|对象|可缺省，缺省值为空。但当应用中包含多个entry模块时，必须配置该标签。|
|commonEvents|定义了公共事件静态订阅者的信息，该字段中需要声明静态订阅者的名称、权限要求及订阅事件列表信息，当订阅的公共事件发送时，该公共事件静态订阅者将被拉起。这里的静态订阅者区分于常用的动态订阅者，前者无需在业务代码中主动调用订阅事件的接口，在公共事件发布时可能未被拉起，而动态订阅者则在业务代码中主动调用公共事件订阅的相关API，因此需要应用处于活动状态。|对象数组|可缺省，缺省为空。|
|entryTheme|此标签标识系统内部主题的关键字。将标记值设置为名称的资源索引。|字符串|可缺省，缺省值为空。|
|testRunner|此标签用于支持对测试框架的配置。|对象|可缺省，缺省值为空。|
|generateBuildHash|标识当前HAP/HSP是否由打包工具生成哈希值。<br><br>该字段配置为true时，当前HAP/HSP会由打包工具生成对应的哈希值。系统OTA升级时，若应用的[version下的code](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-structure#version%E5%AF%B9%E8%B1%A1%E5%86%85%E9%83%A8%E7%BB%93%E6%9E%84)保持不变时，可根据哈希值判断应用是否需要升级。<br><br>- true：表示当前HAP/HSP是由打包工具生成对应的哈希值。<br><br>- false：表示当前HAP/HSP不会由打包工具生成对应的哈希值。<br><br>**说明：**<br><br>该字段仅对预置应用生效。|布尔值|该标签可缺省，缺省值为false。|
|libIsolation|用于区分同应用不同hap下的so文件，以防止so冲突。<br><br>- true：当前hap的so会储存在libs目录中以Module名命名的路径下。<br><br>- false：当前hap的so会直接储存在libs目录中。|布尔值|该标签可缺省, 缺省值为false。|

module示例：

1. {
2.   "module": {
3.     "mainAbility": ".EntryAbility",
4.     "deviceType": [
5.       "default",
6.       "tablet"
7.     ],
8.     "abilities": [
9.       {
10.         "skills": [
11.           {
12.             "entities": [
13.               "entity.system.home"
14.             ],
15.             "actions": [
16.               "action.system.home"
17.             ]
18.           }
19.         ],
20.         "orientation": "unspecified",
21.         "visible": true,
22.         "srcPath": "EntryAbility",
23.         "name": ".EntryAbility",
24.         "srcLanguage": "ets",
25.         "icon": "$media:icon",
26.         "description": "$string:MainAbility_desc",
27.         "formsEnabled": false,
28.         "label": "$string:MainAbility_label",
29.         "type": "page",
30.         "launchType": "multiton"
31.       }
32.     ],
33.     "distro": {
34.       "moduleType": "entry",
35.       "installationFree": false,
36.       "deliveryWithInstall": true,
37.       "moduleName": "entry"
38.     },
39.     "package": "com.example.entry",
40.     "srcPath": "",
41.     "name": ".entry",
42.     "js": [
43.       {
44.         "mode": {
45.           "syntax": "ets",
46.           "type": "pageAbility"
47.         },
48.         "pages": [
49.           "pages/Index"
50.         ],
51.         "name": ".EntryAbility",
52.         "window": {
53.           "designWidth": 720,
54.           "autoDesignWidth": false
55.         }
56.       }
57.     ]
58.   }
59. }

## distro对象内部结构

**表2** **distro对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|moduleName|标识当前HAP的名称，最大长度为31个字节。 在应用升级时，该名称允许修改，但需要应用适配Module相关数据目录的迁移，可使用[文件操作接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs)。|字符串|不可缺省。|
|moduleType|标识当前HAP的类型，包括三种类型：entry、feature和har。|字符串|不可缺省。|
|installationFree|标识当前HAP是否支持免安装特性。true：表示支持免安装特性，且符合免安装约束。false：表示不支持免安装特性。另外还需注意：当entry.hap该字段配置为true时，与该entry.hap相关的所有feature.hap该字段也需要配置为true。当entry.hap该字段配置为false时，与该entry.hap相关的各feature.hap该字段可按业务需求配置true或false。|布尔值|不可缺省。|
|deliveryWithInstall|标识当前HAP是否在用户主动安装HAP所在应用的时候一起安装。true： 安装应用时当前HAP随应用一起下载安装。false：安装应用时当前HAP并不下载安装，后续使用是按需下载。|布尔值|不可缺省。|

distro示例：

1. "distro": {
2.   "moduleName": "ohos_entry",
3.   "moduleType": "entry",
4.   "installationFree": true,
5.   "deliveryWithInstall": true
6. }

## metadata对象内部结构

**表3** **metadata对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|parameters|标识调用Ability时所有调用参数的元信息。每个调用参数的元信息由以下三个标签组成：description、name、type。|对象数组|可缺省，缺省值为空。|
|results|标识Ability返回值的元信息。每个返回值的元信息由以下三个标签组成：description、name、type。|对象数组|可缺省，缺省值为空。|
|customizeData|该标签标识父级组件的自定义元信息，Parameters和results在application不可配。|对象数组|可缺省，缺省值为空。|

## parameters对象内部结构

**表4** **parameters对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|description|标识对调用参数的描述，可以是表示描述内容的字符串，也可以是对描述内容的资源索引以支持多语言。该标签最大长度为255个字节。|字符串|可缺省，缺省值为空。|
|name|标识调用参数的名称。该标签最大长度为255个字节。|字符串|不可缺省。|
|type|标识调用参数的类型，如Integer。|字符串|不可缺省。|

## results对象内部结构

**表5** **results对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|description|标识对返回值的描述，可以是表示描述内容的字符串，也可以是对描述内容的资源索引以支持多语言。该标签最大长度为255个字节。|字符串|可缺省，缺省值为空。|
|name|标识返回值的名字。该标签最大长度为255个字节。|字符串|可缺省，缺省值为空。|
|type|标识返回值的类型，如Integer。|字符串|不可缺省。|

## customizeData对象的内部结构

**表6** **customizeData对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识数据项的键名称，字符串类型（最大长度255字节）。|字符串|可缺省，缺省值为空。|
|value|标识数据项的值名称，字符串类型（最大长度255字节）。|字符串|可缺省，缺省值为空。|
|extra|标识用户自定义数据格式，标签值为标识该数据的资源的索引值。|字符串|可缺省，缺省值为空。|

metadata对象示例：

1. "metaData": {
2.   "parameters" : [{
3.     "name" : "a test for metadata parameter",
4.     "type" : "Float",
5.     // "$string:parameters_description"为文件资源索引值
6.     "description" : "$string:parameters_description"
7.   }],
8.   "results" : [{
9.     "name" : "a test for metadata result",
10.     "type" : "Float",
11.     "description" : "$string:results_description"
12.   }],
13.   "customizeData" : [{
14.     "name" : "a customizeData",
15.     "value" : "string",
16.     "extra" : "$string:customizeData_description"
17.   }]
18. }

## deviceType标签

**表7** **deviceType标签配置说明**

|设备类型|枚举值|说明|
|:--|:--|:--|
|手机|phone|-|
|平板|tablet|-|
|智慧屏|tv|-|
|智能手表|wearable|系统能力较丰富的手表，具备电话功能。|
|车机|car|-|
|运动表|litewearable|-|
|默认设备|default|配置为default类型的应用，虽然可以正常编译构建，但是不支持发布上架。建议使用phone替代。|
|路由器|router|路由器设备。|
|智慧视觉设备|smartVision|带摄像头的设备。|
|2in1|2in1|即PC设备，主要交互方式以多窗口、多任务及键盘鼠标操作为主，充分发挥设备的生产力属性。|

## abilities对象的内部结构

**表8** **abilities对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|process|运行应用程序或Ability的进程名称。如果在deviceConfig标记中配置了进程，则应用程序的所有能力都在此进程中运行。您还可以为特定能力设置流程属性，以便该能力可以在此流程中运行。如果此属性设置为与其他应用程序相同的进程名称，则所有这些应用程序可以在同一进程中运行，前提是他们具有相同的联合用户ID和相同的签名。该标签最大字节数为31个字节。|字符串|可缺省，缺省值为空。|
|name|标识Ability名称。取值可采用反向域名方式表示，由包名和类名组成，如"com.example.myapplication.EntryAbility"；也可采用"."开头的类名方式表示，如".EntryAbility"。<br><br>Ability的名称，需在一个应用的范围内保证唯一。说明：在使用DevEco Studio新建项目时，默认生成首个Ability的配置，即"config.json"中"EntryAbility"的配置。如使用其他DevEco Studio工具，可自定义名称。该标签最大长度为127个字节。|字符串|不可缺省。|
|description|标识对Ability的描述。取值可以是描述性内容，也可以是对描述性内容的资源索引，以支持多语言。该标签最大长度为255个字节。|字符串|可缺省，缺省值为空。|
|icon|标识Ability图标资源文件的索引。取值示例：$media:ability_icon。如果在该Ability的skills属性中，actions的取值包含 "action.system.home"，entities取值中包含"entity.system.home"，则该Ability的icon将同时作为应用的icon。如果存在多个符合条件的Ability，则取位置靠前的Ability的icon作为应用的icon。<br><br>说明：应用的"icon"和"label"是用户可感知配置项，需要区别于当前所有已有的应用"icon"或"label"（至少有一个不同）。|字符串|可缺省，缺省值为空。|
|label|标识Ability对用户显示的名称。取值是对该名称的资源索引，支持多语言，例：$string:ability_label。如果在该Ability的skills属性中，actions的取值包含 "action.system.home"，entities取值中包含"entity.system.home"，则该Ability的label将同时作为应用的label。如果存在多个符合条件的Ability，则取位置靠前的Ability的label作为应用的label。<br><br>说明： 应用的"icon"和"label"是用户可感知配置项，需要区别于当前所有已有的应用"icon"或"label"（至少有一个不同）。该标签为资源文件中定义的字符串的引用，或以"{}"包括的字符串。该标签最大长度为255个字节。|字符串|可缺省，缺省值为空。|
|uri|标识Ability的统一资源标识符。该标签最大长度为255个字节。|字符串|可缺省，对于data类型的Ability不可缺省。|
|launchType|标识Ability的启动模式，支持"multiton"和"singleton"两种模式：<br><br>multiton：表示该Ability可以有多实例。该模式适用于大多数应用场景。<br><br>singleton：表示该Ability在所有任务栈中仅可以有一个实例。例如，具有全局唯一性的呼叫来电界面即采用"singleton"模式。该标签仅适用于默认设备、平板、智慧屏、车机、智能穿戴。|字符串|可缺省，缺省值为"singleton"。|
|visible|标识Ability是否可以被其他应用调用。<br><br>true：可以被其他应用调用。<br><br>false：不能被其他应用调用，包括无法被aa工具命令拉起应用。|布尔类型|可缺省，缺省值为"false"。|
|permissions|标识其他应用的Ability调用此Ability时需要申请的权限集合，一个数组元素为一个权限名称。通常采用反向域名格式（最大255字节），取值为系统预定义的权限。|字符串数组|可缺省，缺省值为空。|
|skills|标识Ability能够接收的want的特征。|对象数组|可缺省，缺省值为空。|
|deviceCapability|标识Ability运行时要求设备具有的能力，采用字符串数组的格式表示。该标签为数组，支持最多配置512个元素，单个元素最大字节长度为64。|字符串数组|可缺省，缺省值为空。|
|metaData|元数据。|对象|可缺省，缺省值为空。|
|type|标识Ability的类型。取值范围如下：<br><br>page：表示基于Page模板开发的FA，用于提供与用户交互的能力。<br><br>service：表示基于Service模板开发的PA，用于提供后台运行任务的能力。<br><br>data：表示基于Data模板开发的PA，用于对外部提供统一的数据访问对象。<br><br>CA：表示支持其他应用以窗口方式调起该Ability。|字符串|不可缺省。|
|orientation|标识该Ability的显示模式。该标签仅适用于page类型的Ability。取值范围如下：<br><br>unspecified：由系统自动判断显示方向。<br><br>landscape：横屏模式。<br><br>portrait：竖屏模式。<br><br>followRecent：跟随栈中最近的应用。|字符串|可缺省，缺省值为"unspecified"。|
|backgroundModes|标识后台服务的类型，可以为一个服务配置多个后台服务类型。该标签仅适用于service类型的Ability。取值范围如下：<br><br>dataTransfer：通过网络/对端设备进行数据下载、备份、分享、传输等。<br><br>audioPlayback：音频播放。<br><br>audioRecording：录音。<br><br>pictureInPicture：画中画、小窗口播放视频。<br><br>voip：音视频电话、VOIP。<br><br>location：定位、导航。<br><br>bluetoothInteraction：蓝牙扫描、连接、传输。<br><br>wifiInteraction：Wi-Fi扫描、连接、传输。<br><br>screenFetch：录屏、截屏。<br><br>multiDeviceConnection：多设备互联。|字符串数组|可缺省，缺省值为空。|
|grantPermission|指定是否可以向Ability内任何数据授予权限。<br><br>- true：表示可以向Ability内任何数据授予权限。<br><br>- false：表示不可以向Ability内任何数据授予权限。|布尔值|可缺省，缺省值为空。|
|readPermission|标识读取Ability的数据所需的权限。该标签仅适用于data类型的Ability。取值为长度不超过255字节的字符串。该标签仅适用于默认设备、平板、智慧屏、车机、智能穿戴。|字符串|可缺省，缺省为空。|
|writePermission|标识向Ability写数据所需的权限。该标签仅适用于data类型的Ability。取值为长度不超过255字节的字符串。|字符串|可缺省，缺省为空。|
|configChanges|标识Ability关注的环境变量集合。当已关注的环境变量更新后，Ability会收到onConfigurationUpdated回调。取值范围：<br><br>mcc：表示IMSI移动设备国家/地区代码（MCC）发生变更。典型场景：检测到SIM并更新MCC。<br><br>mnc：IMSI移动设备网络代码（MNC）发生变更。典型场景：检测到SIM并更新MNC。<br><br>locale：表示语言区域发生变更。典型场景：用户已为设备文本的文本显示选择新的语言类型。<br><br>layout：表示屏幕布局发生变更。典型场景：当前有不同的显示形态都处于活跃状态。<br><br>fontSize：表示字号发生变更。典型场景：用户已设置新的全局字号。<br><br>orientation：表示屏幕方向发生变更。典型场景：用户旋转设备。<br><br>density：表示显示密度发生变更。典型场景：用户可能指定不同的显示比例，或当前有不同的显示形态同时处于活跃状态。<br><br>size：显示窗口大小发生变更。<br><br>smallestSize：显示窗口较短边的边长发生变更。<br><br>colorMode：颜色模式发生变更。|字符串数组|可缺省，缺省为空。|
|mission|标识Ability指定的任务栈。该标签仅适用于page类型的Ability。默认情况下应用中所有Ability同属一个任务栈。|字符串|可缺省，缺省为应用的包名。|
|targetAbility|标识当前Ability重用的目标Ability。该标签仅适用于page类型的Ability。如果配置了targetAbility属性，则当前Ability（即别名Ability）的属性中仅name、icon、label、visible、permissions、skills生效，其他属性均沿用targetAbility中的属性值。目标Ability必须与别名Ability在同一应用中，且在配置文件中目标Ability必须在别名之前进行声明。|字符串|可缺省，缺省值为空。表示当前Ability不是一个别名Ability。|
|formsEnabled|标识Ability是否支持卡片（forms）功能。该标签仅适用于page类型的Ability。<br><br>true：支持卡片能力。<br><br>false：不支持卡片能力。|布尔值|可缺省，缺省值为false。|
|forms|标识服务卡片的属性。该标签仅当formsEnabled为"true"时，才能生效。|对象数组|可缺省，缺省值为空。|
|srcLanguage|Ability开发语言的类型，开发者创建工程时由开发者手动选择开发语言。取值如下："js"、"ets"、"java"。|字符串|可缺省，缺省值为"js"。|
|srcPath|该标签标识Ability对应的JS组件代码路径，该标签最大长度为127字节。|字符串|不可缺省。|
|uriPermission|标识该Ability有权访问的应用程序数据。此属性由模式和路径子属性组成。此属性仅对类型提供者的能力有效。|对象|可缺省，缺省值为空。|
|startWindowIcon|标识该Ability启动页面图标资源文件的索引。该标签仅适用于page类型的Ability。取值示例：$media:icon。|字符串|可缺省，缺省值为空。|
|startWindowBackground|标识该Ability启动页面背景颜色资源文件的索引。该标签仅适用于page类型的Ability。取值示例：$color:red。|字符串|可缺省，缺省值为空。|
|removeMissionAfterTerminate|该标签标识Ability销毁后是否从任务列表中移除任务。该标签仅适用于page类型的Ability。true表示销毁后移除任务， false表示销毁后不移除任务。|布尔值|可缺省，缺省值为false。|

**不允许应用隐藏入口图标**

系统对无图标应用实施严格管控，防止一些恶意应用故意配置无入口图标，导致用户找不到软件所在的位置，无法操作卸载应用，在一定程度上保证用户终端设备的安全。

**入口图标的设置:** 需要在配置文件（config.json）中abilities配置下设置icon，label以及skills，而且skills的配置下必须同时包含“action.system.home” 和 “entity.system.home”。

1. {
2.   "module":{

3.     // ...

4.     "abilities": [{
5.       "icon": "$media:icon",
6.       "label": "Login",
7.       "skills": [{
8.         "actions": ["action.system.home"],
9.         "entities": ["entity.system.home"],
10.         "uris": []
11.       }]
12.     }],

13.     // ...

14.   }
15. }

如果应用确需隐藏入口图标，需要配置AllowAppDesktopIconHide应用特权。详细的入口图标及入口标签的显示规则如下。

- HAP中包含Page类型的PageAbility
    - 配置文件（config.json）中abilities配置中设置了入口图标
        - 该应用没有隐藏图标的特权
            - 系统将使用该PageAbility配置的icon作为入口图标，并显示在桌面上。用户点击该图标，页面跳转到该PageAbility首页。
            - 系统将使用该PageAbility配置的label作为入口标签，并显示在桌面上（如果没有配置label，返回包名）。
        - 该应用具有隐藏图标的特权
            - 桌面查询时不返回应用信息，不会在桌面上显示对应的入口图标和标签。
    - 配置文件（config.json）中abilities配置中未设置入口图标
        - 该应用没有隐藏图标的特权
            - 系统将使用系统默认图标作为入口图标，并显示在桌面上。用户点击该图标，页面跳转到应用管理中对应的应用详情页面（参考下图）。
            - 系统将使用应用的包名作为入口标签，并显示在桌面上。
        - 该应用具有隐藏图标的特权
            - 桌面查询时不返回应用信息，不会在桌面上显示对应的入口图标和标签。
- HAP中不包含Page类型的PageAbility
    - 该应用没有隐藏图标的特权
        - 系统将使用系统默认图标作为入口图标，并显示在桌面上。用户点击该图标，页面跳转到应用管理中对应的应用详情页面（参考下图）。
        - 系统将使用应用的包名作为入口标签，并显示在桌面上。
    - 该应用具有隐藏图标的特权
        - 桌面查询时不返回应用信息，不会在桌面上显示对应的入口图标和标签。

**图1** 应用的详情页示意图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163414.79537993160776306807288149518203:50001231000000:2800:EE8C4974185FA8BD3F1349F8C1DE679E9EFAF6D7E5776147B3F153F423AD3A59.jpg)

注：应用详情页面中显示的label可能与桌面上显示的不同。如果非Page类型的PageAbility配置了入口图标和label，那么详情页中显示的即为配置的。

## uriPermission对象的内部结构

**表9** **uriPermission对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|path|uriPermission标识的路径，该标签最大字节长度为255个字节。|字符串|不可缺省。|
|mode|uriPermission的匹配模式。|字符串|可缺省，缺省值为default。|

abilities示例：

1. "abilities": [
2.   {
3.     "name": ".EntryAbility",
4.     "description": "test main ability",
5.     // $media:ic_launcher 为媒体类资源
6.     "icon": "$media:ic_launcher",
7.     // $string:example 为字符串类资源
8.     "label": "$string:example",
9.     "launchType": "multiton",
10.     "orientation": "unspecified",
11.     "permissions": [],
12.     "visible": true,
13.     "skills": [
14.       {
15.         "actions": [
16.           "action.system.home"
17.         ],
18.         "entities": [
19.           "entity.system.home"
20.         ]
21.       }
22.     ],
23.     "configChanges": [
24.       "locale",
25.       "layout",
26.       "fontSize",
27.       "orientation"
28.     ],
29.     "type": "page",
30.     "startWindowIcon": "$media:icon",
31.     "startWindowBackground": "$color:red",
32.     "removeMissionAfterTerminate": true
33.   },
34.   {
35.     "name": ".PlayService",
36.     "description": "example play ability",
37.     "icon": "$media:ic_launcher",
38.     "label": "$string:example",
39.     "launchType": "multiton",
40.     "orientation": "unspecified",
41.     "visible": false,
42.     "skills": [
43.       {
44.         "actions": [
45.           "action.play.music",
46.           "action.stop.music"
47.         ],
48.         "entities": [
49.           "entity.audio"
50.         ]
51.       }
52.     ],
53.     "type": "service",
54.     "backgroundModes": [
55.       "audioPlayback"
56.     ]
57.   },
58.   {
59.     "name": ".UserADataAbility",
60.     "type": "data",
61.     "uri": "dataability://com.example.world.test.UserADataAbility",
62.     "visible": true
63.   }
64. ]

## skills对象的内部结构

**表10** **skills对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|actions|标识能够接收的want的action值，可以包含一个或多个action。取值通常为系统预定义的action值。|字符串数组|可缺省，缺省值为空。|
|entities|标识能够接收的want的Ability的类别（如视频、桌面应用等），可以包含一个或多个entity。|字符串数组|可缺省，缺省值为空。|
|uris|该标签标识向want过滤器添加数据规范集合。该规范可以是只有数据类型（mimeType属性），可以是只有URI，也可以是既有数据类型又有URI。<br><br>URI由其各个部分的单独属性指定：<scheme>://<host>:<port>[<path>\|<pathStartWith>\|<pathRegex>]。该标签可缺省，缺省值为空。<br><br>其中，scheme字段配置为uri时必配；当只设置数据类型（mimeType）时，则scheme字段为非必配项。|对象数组|可缺省，缺省值为空。|

## uris对象的内部结构

**表11** **uris对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|scheme|标识uri的scheme值。|字符串|不可缺省。|
|host|标识uri的host值。|字符串|可缺省，缺省值为空。|
|port|标识uri的port值。|字符串|可缺省，缺省值为空。|
|pathStartWith|标识uri的pathStartWith值。|字符串|可缺省，缺省值为空。|
|path|标识uri的path值。|字符串|可缺省，缺省值为空。|
|pathRegx|标识uri的pathRegx值。|字符串|可缺省，缺省值为空。|
|type|标识uri的type值。type为MIME-TYPE属性，为资源的媒体类型，常见的类型有"audio/aac"，"text/css"等。<br><br>注意：只支持*/*、mainType/*的通配符格式，不支持mainType/subType.*的通配符格式，mainType为标准媒体类型。|字符串|可缺省，缺省值为空。|

skills示例：

1. "skills": [
2.   {
3.     "actions": [
4.       "action.system.home"
5.     ],
6.     "entities": [
7.       "entity.system.home"
8.     ],
9.     "uris": [
10.       {
11.         "scheme": "http",
12.         "host": "www.example.com",
13.         "port": "8080",
14.         "path": "query/student/name",
15.         "type": "text/*"
16.       }
17.     ]
18.   }
19. ]

## reqPermissions权限申请

**表12** **reqPermissions权限申请字段说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|需要使用的权限名称。|字符串|否|
|reason|描述申请权限的原因。需要做多语种适配。|字符串|分情况：当申请的权限为user_grant时，必须填写此字段，否则不允许在应用市场上架；其他权限可缺省，缺省为空。|
|usedScene|描述权限使用的场景和时机。场景类型如下两种：<br><br>- ability：ability的名称，可配置多个。<br><br>- when：调用时机，可填的值有inuse（使用时）、always（始终）。|对象|可缺省，缺省值为空。<br><br>when可缺省，缺省值为"inuse"。|

## usedScene对象内部结构

**表13** **usedScene对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|ability|标识哪些Ability需要此权限，里面配置Ability的名称。|字符串数组|可以缺省，缺省表示所有Ability都需要此权限。|
|when|标识此权限的使用时间：<br><br>inuse: 使用时需要此权限。<br><br>always: 所有时间都需要此权限。|枚举值|可缺省，缺省值为空。|

## js对象的内部结构

**表14** **js对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识JS Component的名字。|字符串|不可缺省。|
|pages|标识JS Component的页面用于列举JS Component中每个页面的路由信息，格式为“页面路径+页面名称”。其中，页面路径是以当前Ability的srcPath字段取值为基准，例如srcPath取值为EntryAbility，则JS Component页面路径需要从EntryAbility的下一层开始描述。该标签取值为数组，数组第一个元素代表JS FA首页。|字符串数组|不可缺省。|
|window|用于定义与显示窗口相关的配置。|对象|可缺省，缺省值见表15。|
|type|标识JS应用的类型。取值范围如下：<br><br>normal：标识该JS Component为应用实例。<br><br>form：标识该JS Component为卡片实例。|字符串|可缺省，缺省值为"normal"。|
|mode|定义JS组件的开发模式。|对象|可缺省，缺省值为空。|

## window对象的内部结构

**表15** **window对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|designWidth|标识页面设计基准宽度。以此为基准，根据实际设备宽度来缩放元素大小。|数值|可缺省，缺省值为720px。|
|autoDesignWidth|标识页面设计基准宽度是否自动计算。当配置为true时，designWidth将会被忽略，设计基准宽度由设备宽度与屏幕密度计算得出。当配置为false时，设计基准宽度为designWidth。|布尔值|可缺省，缺省值为false。|

## mode对象的内部结构

**表16** **mode对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|type|定义JS组件的功能类型。|字符串，取值为"pageAbility"、"form"|可缺省，缺省值为pageAbility。|
|syntax|定义JS组件的语法类型。|字符串，取值为"hml"，"ets"|可缺省，默认值为"hml"。|

js示例：

1. "js": [
2.   {
3.     "name": ".EntryAbility",
4.     "pages": [
5.       "pages/index",
6.       "pages/detail/detail"
7.     ],
8.     "window": {
9.       "designWidth": 720,
10.       "autoDesignWidth": false
11.     },
12.     "type": "form",
13.     "mode": {
14.       "syntax": "ets",
15.       "type": "pageAbility"
16.     }
17.   }
18. ]

## shortcuts对象的内部结构

**表17** **shortcuts对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|shortcutId|标识快捷方式的ID。字符串的最大长度为63字节。|字符串|不可缺省。|
|label|标识快捷方式的标签信息，即快捷方式对外显示的文字描述信息。取值可以是描述性内容，也可以是标识label的资源索引。字符串最大长度为63字节。|字符串|可缺省，缺省为空。|
|icon|标识快捷方式的图标信息。取值为表示icon的资源索引。|字符串|可缺省，缺省为空。|
|intents|标识快捷方式内定义的目标intent信息集合，每个intent可配置两个子标签，targetClass, targetBundle。|对象数组|可缺省，缺省为空。|

## intents对象的内部结构

**表18** **intents对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|targetClass|标识快捷方式目标类名。|字符串|可缺省，缺省值为空。|
|targetBundle|标识快捷方式目标Ability所在应用的包名。|字符串|可缺省，缺省值为空。|

shortcuts示例：

1. "shortcuts": [
2.   {
3.     "shortcutId": "id",
4.     // $string:shortcut 为配置的字符串资源值
5.     "label": "$string:shortcut",
6.     "intents": [
7.       {
8.         "targetBundle": "com.example.world.test",
9.         "targetClass": "com.example.world.test.entry.EntryAbility"
10.       }
11.     ]
12.   }
13. ]

## forms对象的内部结构

**表19** **forms对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识卡片的类名。字符串最大长度为127字节。|字符串|不可缺省。|
|description|标识卡片的描述。取值可以是描述性内容，也可以是对描述性内容的资源索引，以支持多语言。字符串最大长度为255字节。|字符串|可缺省，缺省为空。|
|isDefault|标识该卡片是否为默认卡片，每个Ability有且只有一个默认卡片。<br><br>true：默认卡片。<br><br>false：非默认卡片。|布尔值|不可缺省。|
|type|标识卡片的类型。取值范围如下：<br><br>JS：JS卡片。<br><br>Java：Java卡片。|字符串|不可缺省。|
|colorMode|标识卡片的主题样式，取值范围如下：<br><br>auto：自适应。<br><br>dark：深色主题。<br><br>light：浅色主题。|字符串|可缺省，缺省值为"auto"。|
|supportDimensions|标识卡片支持的外观规格，取值范围：<br><br>1 * 2：表示1行2列的二宫格。<br><br>2 * 1：表示2行1列的二宫格。<br><br>2 * 2：表示2行2列的四宫格。<br><br>2 * 4：表示2行4列的八宫格。<br><br>4 * 4：表示4行4列的十六宫格。|字符串数组|不可缺省。|
|defaultDimension|标识卡片的默认外观规格，取值必须在该卡片supportDimensions配置的列表中。|字符串|不可缺省。|
|updateEnabled|标识卡片是否支持周期性刷新，取值范围：<br><br>true：表示支持周期性刷新，可以在定时刷新（updateDuration）和定点刷新（scheduledUpdateTime）两种方式任选其一，优先选择定时刷新。<br><br>false：表示不支持周期性刷新。|布尔类型|不可缺省。|
|scheduledUpdateTime|标识卡片的定点刷新的时刻，采用24小时制，精确到分钟。|字符串|可缺省，缺省值为"0:0"。|
|updateDuration|标识卡片定时刷新的更新周期，单位为30分钟，取值为自然数。<br><br>当取值为0时，表示该参数不生效。<br><br>当取值为正整数N时，表示刷新周期为30*N分钟。|数值|可缺省，缺省值为"0"。|
|formConfigAbility|标识用于调整卡片的设施或活动的名称。|字符串|可缺省，缺省值为空。|
|jsComponentName|标识JS卡片的Component名称。字符串最大长度为127字节。仅当卡片类型为JS卡片时，需要配置该标签。|字符串|可缺省，缺省值为空。|
|metaData|标识卡片的自定义信息，包含customizeData数组标签。|对象|可缺省，缺省值为空。|
|formVisibleNotify|标识是否允许卡片使用卡片可见性通知。<br><br>true：允许。<br><br>false：不允许。|布尔值|可缺省，缺省值为false。|

## customizeData对象内部结构

**表20** **customizeData对象内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识数据项的键名称。字符串最大长度为255字节。|字符串|可缺省，缺省值为空。|
|value|标识数据项的值。字符串最大长度为255字节。|字符串|可缺省，缺省值为空。|
|extra|标识当前custom数据的格式，取值为表示extra的资源值。|字符串|可缺省，缺省值为空。|

forms示例：

1. "forms": [
2.   {
3.     "name": "Form_Js1",
4.     "description": "It's Js Form",
5.     "type": "JS",
6.     "jsComponentName": "card",
7.     "colorMode": "auto",
8.     "isDefault": true,
9.     "updateEnabled": true,
10.     "scheduledUpdateTime": "11:00",
11.     "updateDuration": 1,
12.     "defaultDimension": "2*2",
13.     "supportDimensions": [
14.       "2*2",
15.       "2*4",
16.       "4*4"
17.     ]
18.   },
19.   {
20.     "name": "Form_Js2",
21.     "description": "It's JS Form",
22.     "type": "JS",
23.     "colorMode": "auto",
24.     "isDefault": false,
25.     "updateEnabled": true,
26.     "scheduledUpdateTime": "21:05",
27.     "updateDuration": 1,
28.     "defaultDimension": "1*2",
29.     "supportDimensions": [
30.       "1*2"
31.     ],
32.     "landscapeLayouts": [
33.       "$layout:ability_form"
34.     ],
35.     "portraitLayouts": [
36.       "$layout:ability_form"
37.     ],
38.     "formConfigAbility": "ability://com.example.myapplication.fa/.EntryAbility",
39.     "metaData": {
40.       "customizeData": [
41.         {
42.           "name": "originWidgetName",
43.           "value": "com.example.weather.testWidget"
44.         }
45.       ]
46.     }
47.   }
48. ]

## distroFilter对象的内部结构

**表21** **distroFilter对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|apiVersion|标识支持的apiVersion范围。|对象数组|可缺省，缺省值为空。|
|screenShape|标识屏幕形状的支持策略。|对象数组|可缺省，缺省值为空。|
|screenWindow|标识应用运行时窗口的分辨率支持策略。该字段仅支持对轻量级智能穿戴设备进行配置。|对象数组|可缺省，缺省值为空。|
|screenDensity|标识屏幕的像素密度（dpi：Dots Per Inch）。|对象数组|可缺省，缺省值为空。|
|countryCode|标识分发应用时的国家码。具体值参考ISO-3166-1的标准，支持多个国家和地区的枚举定义。|对象数组|可缺省，缺省值为空。|

## apiVersion对象的内部结构

**表22** **apiVersion对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|policy|标识该子属性取值规则。配置为“exclude”或“include”。<br><br>- exclude：表示需要排除的value属性。<br><br>- include：表示需要包含的value属性。|字符串|不可缺省。|
|value|支持的取值为API Version存在的整数值，例如4、5、6。场景示例：某应用，针对相同设备型号，同时在网的为使用API 5和API 6开发的两个软件版本，则允许上架2个entry类型的安装包，分别支持到对应设备侧软件版本的分发。|数组|不可缺省。|

## screenShape对象的内部结构

**表23** **screenShape对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|policy|标识该子属性取值规则。配置为“exclude”或“include”。<br><br>- exclude：表示需要排除的value属性。<br><br>- include：表示需要包含的value属性。|字符串|不可缺省。|
|value|支持的取值为API Version存在的整数值，例如4、5、6。场景示例：某应用，针对相同设备型号，同时在网的为使用API 5和API 6开发的两个软件版本，则允许上架2个entry类型的安装包，分别支持到对应设备侧软件版本的分发。|数组|不可缺省。|

## screenWindow对象的内部结构

**表24** **screenWindow对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|policy|标识该子属性取值规则。配置为“exclude”或“include”。<br><br>- exclude：表示需要排除的value属性。<br><br>- include：表示需要包含的value属性。|字符串|不可缺省。|
|value|支持的取值为API Version存在的整数值，例如4、5、6。场景示例：某应用，针对相同设备型号，同时在网的为使用API 5和API 6开发的两个软件版本，则允许上架2个entry类型的安装包，分别支持到对应设备侧软件版本的分发。|数组|不可缺省。|

## screenDensity对象的内部结构

**表25** **screenDensity对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|policy|标识该子属性取值规则。配置为“exclude”或“include”。<br><br>- exclude：表示需要排除的value属性。<br><br>- include：表示需要包含的value属性。|字符串|不可缺省。|
|value|取值范围如下：<br><br>sdpi：表示小规模的屏幕密度（Small-scale Dots Per Inch），适用于dpi取值为（0,120]的设备。<br><br>mdpi：表示中规模的屏幕密度(Medium-scale Dots Per Inch)，适用于dpi取值为（120,160]的设备。<br><br>ldpi：表示大规模的屏幕密度(Large-scale Dots Per Inch)，适用于dpi取值为（160,240]的设备。<br><br>xldpi：表示特大规模的屏幕密度(Extra Large-scale Dots Per Inch)，适用于dpi取值为（240,320]的设备。<br><br>xxldpi：表示超大规模的屏幕密度(Extra Extra Large-scale Dots Per Inch)，适用于dpi取值为（320,480]的设备。<br><br>xxxldpi：表示超特大规模的屏幕密度(Extra Extra Extra Large-scale Dots Per Inch)，适用于dpi取值为（480,640]的设备。|数组|不可缺省。|

## countryCode对象的内部结构

**表26** **countryCode对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|policy|标识该子属性取值规则。配置为“exclude”或“include”。<br><br>- exclude：表示需要排除的value属性。<br><br>- include：表示需要包含的value属性。|字符串|不可缺省。|
|value|该标签标识应用需要分发的国家码，标签为字符串数组，子串表示支持的国家或地区，由两个大写字母表示。|字符串数组|不可缺省。|

distroFilter示例：

1. "distroFilter":  {
2.   "apiVersion": {
3.     "policy": "include",
4.     "value": [4,5]
5.   },
6.   "screenShape": {
7.     "policy": "include",
8.     "value": ["circle","rect"]
9.   },
10.   "screenWindow": {
11.     "policy": "include",
12.     "value": ["454*454","466*466"]
13.   },
14.   "screenDensity":{
15.     "policy": "exclude",
16.     "value": ["ldpi","xldpi"]
17.   },
18.   "countryCode": {
19.     "policy":"include",
20.     "value":["CN","HK"]
21.   }
22. }

## commonEvents对象的内部结构

**表27** **commonEvents对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识静态公共事件名称，该标签最大长度为127字节。|字符串|不可缺省。|
|permission|此标签标识实现静态公共事件所需要申请的权限，该标签最大长度为255字节。|字符串|可缺省，缺省值为空。|
|data|标识配置当前静态公共事件要携带的附加数据数组。|字符串数组|可缺省，缺省值为空。|
|type|该标签用于配置当前静态公共事件的分类数组。|字符串数组|可缺省，缺省值为空。|
|events|此标签标识可接收的意图的一组事件值。一般由系统预定义，也可以自定义。|字符串数组|不可缺省。|

commonEvents示例：

1. "commonEvents": [
2.   {
3.     "name": ".EntryAbility",
4.     "permission": "ohos.permission.GET_BUNDLE_INFO",
5.     "data": [
6.       "com.example.demo",
7.       "100"
8.     ],
9.     "events": [
10.       "install",
11.       "update"
12.     ]
13.   }
14. ]

## testRunner对象的内部结构

**表28** **testRunner对象的内部结构说明**

|属性名称|含义|数据类型|是否可缺省|
|:--|:--|:--|:--|
|name|标识测试框架对象名称，该标签最大长度为255字节。|字符串|不可缺省。|
|srcPath|标识测试框架代码路径，该标签最大长度为255字节。|字符串|不可缺省。|

1. "testRunner": {
2.   "name": "myTestRunnerName",
3.   "srcPath": "etc/test/TestRunner.ts"
4. }
5. 