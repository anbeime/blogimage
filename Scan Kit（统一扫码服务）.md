# Scan Kit简介

更新时间: 2025-12-16 16:35

Scan Kit（统一扫码服务）作为软硬协同的系统级扫码服务，创新性地推出了更简单的“扫码直达”接入能力。只需少量的接入工作，无需在应用中开发专门的扫码模块，即可通过系统级扫码入口实现扫码到应用的跳转。同时还为开发者提供了面向各种场景的码图识别和生成能力。

Scan Kit应用了多项计算机视觉技术和AI算法技术，不仅实现了远距离自动扫码，同时还针对多种复杂扫码场景（如暗光、污损、模糊、小角度、曲面码等）做了识别优化，提升扫码成功率与用户体验。

为了方便开发者接入，我们提供了详细的样例工程供参考，推荐参考[示例工程](https://gitcode.com/HarmonyOS_Samples/scan-kit_-sample-code_-clientdemo_-arkts)接入。

## 场景介绍

Scan Kit同时提供了系统“扫码直达”和开发者应用内扫码两种能力。优先接入“扫码直达”能力，通过少量的接入工作即可实现开发者应用服务的一步直达。

- 扫码直达（推荐）：用户可通过控制中心等系统级的常驻入口，扫描开发者应用的二维码、条形码并跳转到开发者应用对应服务页，实现一步直达的体验。
- 默认界面扫码：提供系统级体验一致的扫码界面，包含相机预览流，相册扫码入口，暗光环境闪光灯开启提示，具备相机预授权，集成简单，适用于通用扫码场景。
- 自定义界面扫码：提供扫码能力并支持在指定控件上渲染相机预览流，需要开发者实现扫码界面，申请相机权限，适用于对扫码界面有个性化定制的场景。
- 图像识码：对图库中的码图或图像数据进行扫描识别。
- 码图生成：通过文本或字节数组生成码图。

说明

Scan Kit支持十三种全球主流的码制式的识别和生成以及MULTIFUNCTIONAL CODE的识别。目前已支持的码制式包括QR Code、Data Matrix、PDF417、Aztec、EAN-8、EAN-13、UPC-A、UPC-E、Codabar、Code 39、Code 93、Code 128、 ITF-14。

## 功能使用限制

|能力|限制条件|
|:--|:--|
|扫码直达能力|1. 当前只支持开发者配置HTTPS架构的网页链接接入扫码直达。其他方式接入如HTTP配置可以通过[工单](https://developer.huawei.com/consumer/cn/support/feedback/#/)联系我们。<br>2. 当前仅支持中国境内（不包含中国香港、中国澳门、中国台湾）接入使用。|
|默认界面扫码能力|从6.0.0(20)版本开始，支持悬浮屏、分屏场景；相册扫码只支持单码识别；不支持界面UX添加自定义设置。|
|自定义界面扫码能力|需要授权使用相机权限；需要开发者自行实现扫码的人机交互界面。|
|码图生成能力|在设置生成参数时，对参数有限制要求，详细信息请参见[文本生成码图的约束与限制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-barcodegenerate#section9684181513312)和[字节数组生成码图的约束与限制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-generatearray#section9684181513312)。|

### 支持的设备

- 扫码直达能力、默认界面扫码能力、图像识码能力和自定义界面扫码能力支持Phone、Tablet。
- 码图生成能力支持Phone、Tablet、Wearable、2in1、TV（从5.1.0(18)版本开始支持Wearable、从5.1.1(19)版本开始支持2in1、TV）。

### 模拟器支持情况

本Kit支持模拟器开发，但与真机存在部分能力差异，详情请参见“[模拟器与真机的差异](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-specification#section18112195514315)”。

## 示例代码

Scan Kit提供的[示例工程](https://gitcode.com/HarmonyOS_Samples/scan-kit_-sample-code_-clientdemo_-arkts)体现了Scan Kit的默认界面扫码、自定义界面扫码、图像识码、码图生成等特性，可参考该工程进行应用的相关内容开发。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-kit-guide "Scan Kit（统一扫码服务）")
# 开发准备

更新时间: 2025-12-16 16:35

1. 参考“[应用开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview)”完成基本准备工作。
2. （**仅针对“扫码直达”必选**）接入[App Linking](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-linking-kit-guide)，您需要完成以下步骤：
    1. 在AGC控制台开通App Linking服务。
    2. 在开发者网站上关联应用。
    3. 在App Linking中配置二维码、条形码关联的网址域名。
    4. 在应用的“module.json5”文件中关联域名。

说明

- App Linking方式当前仅支持HTTPS网址，具备应用和网页两种呈现方式。当应用安装时则优先直达应用内服务页，当应用未安装时，浏览器也可以为用户提供服务。
- App Linking还广泛应用于社交分享、沉默唤醒、广告引流等场景。
- 接入App Linking不能使用DevEco的自动签名功能，必须使用[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-introduction "Scan Kit简介")
# 接入“扫码直达”服务

更新时间: 2025-12-16 16:35

说明

扫码直达能力仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）接入使用。

在日常生活中，人们会使用各种应用扫各式各样的码，而“扫码直达”服务则为用户带来一种全新的扫码体验。

开发者将域名注册到“扫码直达”服务后，用户可通过控制中心等系统级的常驻入口，扫应用的二维码、条形码并跳转到应用对应服务页，实现一步直达服务的体验。

开发者接入“扫码直达”服务，能为应用带来：

- 更浅层的扫码入口和更便捷的“扫码直达”服务体验。
- HarmonyOS强大的扫码能力。
- 更容易触达用户的全新渠道。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163518.34625033812946401849074383301936:50001231000000:2800:7AA43B50C79EB140BB57E0121184E259F88A5198EAFE618B2BBF16E36D25A2DE.png "点击放大")

1. 开发者参考App Linking指导完成域名注册。
2. 用户通过HarmonyOS扫码入口发起扫码请求。
3. HarmonyOS扫码入口调用系统能力解析码值，查询码值对应的应用信息后拉起应用。
4. 解析码值结果跳转应用服务页。

## 开发步骤

1. 参考[开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-config-agc)完成必要的准备工作。
2. 处理接收到的码值，完成应用内页面跳转逻辑。
    
    1. import { router, window } from '@kit.ArkUI';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    3. import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
    5. export default class EntryAbility extends UIAbility {
    6.   private page: string = 'pages/Index';
    7.   private uiContext?: UIContext;
    
    8.   // 冷启动场景通过onCreate回调获取码值信息
    9.   onCreate(want: Want, _: AbilityConstant.LaunchParam): void {
    10.     hilog.info(0x0001, '[Scan Access]', 'Succeeded in getting want in onCreate');
    11.     // 从want中获取传入的链接信息。
    12.     // 如传入的url为：https://www.example.com/programs?router=Access
    13.     this.getRouterUri(want);
    14.   }
    
    15.   // 热启动场景通过onNewWant回调获取码值信息
    16.   onNewWant(want: Want, _: AbilityConstant.LaunchParam): void {
    17.     hilog.info(0x0001, '[Scan Access]', 'Succeeded in getting want in onNewWant');
    18.     // 从want中获取传入的链接信息
    19.     this.getRouterUri(want);
    20.   }
    
    21.   onWindowStageCreate(windowStage: window.WindowStage): void {
    22.     hilog.info(0x0001, '[Scan Access]', 'Ability onWindowStageCreate');
    23.     try {
    24.       windowStage.getMainWindow().then((windowObj: window.Window) => {
    25.         try {
    26.           windowStage.loadContent(this.page).then(() => {
    27.             hilog.info(0x0001, '[Scan Access]', 'Succeeded in loading the content.');
    28.             try {
    29.               this.uiContext = windowObj.getUIContext();
    30.               hilog.info(0x0001, '[Scan Access]', 'Succeeded in getting UIContext.');
    31.             } catch (error) {
    32.               hilog.error(0x0001, '[Scan Access]', `Failed to get UIContext by windowObj. Code: ${error.code}.`);
    33.             }
    34.           }).catch((error: BusinessError) => {
    35.             hilog.error(0x0001, '[Scan Access]', `Failed to load the content. Code: ${error.code}.`);
    36.           })
    37.         } catch (error) {
    38.           hilog.error(0x0001, '[Scan Access]', `Failed to load the content. Code: ${error.code}.`);
    39.         }
    40.       }).catch((error: BusinessError) => {
    41.         hilog.error(0x0001, '[Scan Access]', `Failed to get MainWindow. Code: ${error.code}.`);
    42.       })
    43.     } catch (error) {
    44.       hilog.error(0x0001, '[Scan Access]', `Failed to get MainWindow. Code: ${error.code}.`);
    45.     }
    46.   }
    
    47.   // 解析扫码结果，跳转相应页面
    48.   private getRouterUri(want: Want) {
    49.     const uri: string | undefined = want?.uri;
    50.     if (uri && this.uiContext) {
    51.       // 开发者根据解析的uri跳转至相应页面，例如需要跳转页面为"pages/Access"
    52.       const status: router.RouterState = this.uiContext.getRouter().getState();
    53.       if (status && status.name !== 'Access' && uri) {
    54.         try {
    55.           // 根据uri参数做业务处理
    56.           this.uiContext.getRouter().pushUrl({
    57.             url: 'pages/Access'
    58.           }).catch((error: BusinessError) => {
    59.             hilog.error(0x0001, '[Scan Access]', `Failed to pushUrl by getRouter. Code: ${error.code}.`);
    60.           });
    61.         } catch (error) {
    62.           hilog.error(0x0001, '[Scan Access]', `Failed to pushUrl by getRouter. Code: ${error.code}.`);
    63.         }
    64.       }
    65.     }
    66.   }
    67. }
    
3. 验证“扫码直达”服务。
    1. 将配置好域名映射关系的测试应用安装到本地。
    2. 打开HarmonyOS扫码入口（控制中心扫码入口），扫描应用发行的二维码。
    3. 确认能否拉起应用并跳转目标服务页。
4. 集成效果，以美团单车场景为例：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163518.38394059662699334780569384937298:50001231000000:2800:37A41EE27F9EF36C7518BDB6F5CD8C4B87084CCFCF9837EF9B4D4FBB7D3D5DC4.gif "点击放大")
    

## 开发后验证

集成扫码直达能力应用用户体验质量建议

应用完成开发后，可参照以下标准检查集成扫码直达后的用户体验是否符合预期：

|标准编号|标准项名称|类型|标准详细描述|
|:--|:--|:--|:--|
|1|应用已安装跳转体验|规则|通过系统扫一扫扫描码图可以跳转到履约页面。履约页面指的是扫码后的目标服务页面，例如，扫支付码跳转到应用的支付页面，而非首页。|
|2|应用未安装跳转体验|建议|通过系统扫一扫扫描码图会拉起浏览器加载码值所对应的网页，请设计网页满足用户诉求、指导用户安装应用等。|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-config-agc "开发准备")
# 默认界面扫码

更新时间: 2025-12-16 16:35

## 基本概念

默认界面扫码能力提供系统级体验一致的扫码界面，包含相机预览流，相册扫码入口，暗光环境闪光灯开启提示。Scan Kit默认界面扫码对系统相机权限进行了预授权且调用期间处于安全访问状态，无需开发者再次申请相机权限。适用于不同扫码场景的应用开发。

说明

通过默认界面扫码可以实现应用内的扫码功能，为了应用更好的体验，推荐同时[接入“扫码直达”服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-directservice)，应用可以同时支持系统扫码入口（控制中心扫一扫）和应用内扫码两种方式跳转到指定服务页面。

## 场景介绍

默认界面扫码能力提供了系统级体验一致的扫码界面以及相册扫码入口，支持单码和多码识别，支持多种识码类型，请参见[ScanType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scancore#section113371139123212)。无需使用三方库就可帮助开发者的应用快速处理各种扫码场景。

默认扫码界面UX：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163519.88143095775275926227646048156790:50001231000000:2800:E6CF96EDD738A0FE8EA737AA4AD547DE07FCD6DA6A79E1905A1975B1771D3B95.png "点击放大")

说明

1. 系统首次使用默认界面扫码功能时，会向用户弹出隐私横幅提醒。
2. 用户可以点击“进一步了解”查看安全访问相机说明，也可以关闭隐私横幅，关闭后重新打开应用的扫码界面将不再显示隐私横幅提醒，显示安全访问提示，3s后消失。

## 约束与限制

- 从6.0.0(20)版本开始，默认界面扫码能力支持悬浮屏、分屏场景。
- 相册扫码只支持单码识别。
- 不支持界面UX添加自定义设置。

## 业务流程

使用默认界面扫码的主要业务流程如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163519.53273011472689306540137329541835:50001231000000:2800:57F80BEBFB25FA61BB5A3EEB9DAA6AA971F0C1CCCA7CA2012F27ACA8F8CB6E30.png "点击放大")

1. 用户向开发者的应用发起扫码请求。
2. 开发者的应用通过调用Scan Kit的startScanForResult接口启动扫码界面。
3. 系统首次使用默认界面扫码功能时，会向用户弹出隐私横幅提醒。
4. 用户可以点击关闭隐私横幅，重新打开应用的扫码界面将不再显示隐私横幅提醒，显示安全访问提示，3s后消失。
5. Scan Kit通过Callback回调函数或Promise方式返回扫码结果。
6. 用户进行多码扫描时，需点击选择其中一个码图获取扫码结果返回。单码扫描则可直接返回扫码结果。
7. 解析码值结果跳转应用服务页。

## 接口说明

接口返回值有两种返回形式：Callback和Promise回调。下表中为默认界面扫码Callback和Promise形式接口，Callback和Promise只是返回值方式不一样，功能相同。startScanForResult接口打开的是应用内呈现的扫码界面样式。具体API说明详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api)。

|接口名|描述|
|:--|:--|
|[startScanForResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section829511911349)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-common#context), options?: [ScanOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section1285191073117)): Promise<[ScanResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section10614317162112)>|启动默认界面扫码，通过ScanOptions进行扫码参数设置，使用Promise异步回调返回扫码结果。|
|[startScanForResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section1738211373353)(context: common.Context, options: ScanOptions, callback: AsyncCallback<ScanResult>): void|启动默认界面扫码，通过ScanOptions进行扫码参数设置，使用Callback异步回调返回扫码结果。|
|[startScanForResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section399311216327)(context: common.Context, callback: AsyncCallback<ScanResult>): void|启动默认界面扫码，使用Callback异步回调返回扫码结果。|

说明

startScanForResult接口需要在页面和组件的生命周期内调用。若需要设置扫码页面为全屏或沉浸式，请参见[开发应用沉浸式效果](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-develop-apply-immersive-effects)。

## 开发步骤

Scan Kit提供了默认界面扫码的能力，由扫码接口直接控制相机实现最优的相机放大控制、自适应的曝光调节、自适应对焦调节等操作，保障流畅的扫码体验，减少开发者的工作量。

为了方便开发者接入，我们提供了详细的样例工程供参考，推荐参考[示例工程](https://gitcode.com/HarmonyOS_Samples/scan-kit_-sample-code_-clientdemo_-arkts)接入。

以下示例为调用Scan Kit的startScanForResult接口跳转扫码页面。

1. 导入默认界面扫码模块，[scanCore](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scancore)提供扫码类型定义，[scanBarcode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api)提供拉起默认界面扫码的方法和参数，导入方法如下。
    
    1. import { scanCore, scanBarcode } from '@kit.ScanKit';
    2. // 导入默认界面扫码需要的日志模块和错误码模块
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 调用startScanForResult方法拉起默认界面扫码。
    - 通过Promise方式得到扫码结果。
        
        1. @Entry
        2. @Component
        3. struct ScanBarCodePage {
        4.   build() {
        5.     Column() {
        6.       Row() {
        7.         Button("Promise with options")
        8.           .backgroundColor('#0D9FFB')
        9.           .fontSize(20)
        10.           .fontColor($r('sys.color.comp_background_list_card'))
        11.           .fontWeight(FontWeight.Normal)
        12.           .align(Alignment.Center)
        13.           .type(ButtonType.Capsule)
        14.           .width('90%')
        15.           .height(40)
        16.           .margin({ top: 5, bottom: 5 })
        17.           .onClick(() => {
        18.             // 定义扫码参数options
        19.             let options: scanBarcode.ScanOptions = {
        20.               scanTypes: [scanCore.ScanType.ALL],
        21.               enableMultiMode: true,
        22.               enableAlbum: true
        23.             };
        24.             try {
        25.               // 可调用getHostContext接口获取当前页面关联的Context
        26.               scanBarcode.startScanForResult(this.getUIContext().getHostContext(), options).then((result: scanBarcode.ScanResult) => {
        27.                 // 解析码值结果跳转应用服务页
        28.                 hilog.info(0x0001, '[Scan CPSample]', `Succeeded in getting ScanResult by promise with options, result is ${JSON.stringify(result)}`);
        29.               }).catch((error: BusinessError) => {
        30.                 hilog.error(0x0001, '[Scan CPSample]',
        31.                   `Failed to get ScanResult by promise with options. Code:${error.code}, message: ${error.message}`);
        32.               });
        33.             } catch (error) {
        34.               hilog.error(0x0001, '[Scan CPSample]',
        35.                 `Failed to start the scanning service. Code:${error.code}, message: ${error.message}`);
        36.             }
        37.           })
        38.       }
        39.       .height('100%')
        40.     }
        41.     .width('100%')
        42.   }
        43. }
        
    - 通过Callback回调函数得到扫码结果。
        
        1. @Entry
        2. @Component
        3. struct ScanBarCodePage {
        4.   build() {
        5.     Column() {
        6.       Row() {
        7.         Button('Callback with options')
        8.           .backgroundColor('#0D9FFB')
        9.           .fontSize(20)
        10.           .fontColor($r('sys.color.comp_background_list_card'))
        11.           .fontWeight(FontWeight.Normal)
        12.           .align(Alignment.Center)
        13.           .type(ButtonType.Capsule)
        14.           .width('90%')
        15.           .height(40)
        16.           .margin({ top: 5, bottom: 5 })
        17.           .onClick(() => {
        18.             // 定义扫码参数options
        19.             let options: scanBarcode.ScanOptions = {
        20.               scanTypes: [scanCore.ScanType.ALL],
        21.               enableMultiMode: true,
        22.               enableAlbum: true
        23.             };
        24.             try {
        25.               // 可调用getHostContext接口获取当前页面关联的Context
        26.               scanBarcode.startScanForResult(this.getUIContext().getHostContext(), options,
        27.                 (error: BusinessError, result: scanBarcode.ScanResult) => {
        28.                   if (error) {
        29.                     hilog.error(0x0001, '[Scan CPSample]',
        30.                       `Failed to get ScanResult by callback with options. Code: ${error.code}, message: ${error.message}`);
        31.                     return;
        32.                   }
        33.                   // 解析码值结果跳转应用服务页
        34.                   hilog.info(0x0001, '[Scan CPSample]', `Succeeded in getting ScanResult by callback with options, result is ${JSON.stringify(result)}`);
        35.                 })
        36.             } catch (error) {
        37.               hilog.error(0x0001, '[Scan CPSample]',
        38.                 `Failed to start the scanning service. Code:${error.code}, message: ${error.message}`);
        39.             }
        40.           })
        41.       }
        42.       .height('100%')
        43.     }
        44.     .width('100%')
        45.   }
        46. }
        

## 模拟器开发

从6.0.0(20)版本开始，支持模拟器开发，使用指导请参见[使用模拟器运行应用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-run-emulator)。

说明

1. 模拟器中，默认界面扫码相机流处于镜像状态，真机中不存在该现象。
2. 模拟器上由于相机流的分辨率仅支持固定比例，默认界面扫码的画面上下存在黑边，真机上不存在该现象。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-directservice "接入“扫码直达”服务")
# 自定义界面扫码

更新时间: 2025-12-16 16:35

## 基本概念

自定义界面扫码能力提供了相机流控制接口，可根据自身需求自定义扫码界面，适用于对扫码界面有定制化需求的应用开发。

说明

通过自定义界面扫码可以实现应用内的扫码功能，为了应用更好的体验，推荐同时[接入“扫码直达”服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-directservice)，应用可以同时支持系统扫码入口（控制中心扫一扫）和应用内扫码两种方式跳转到指定服务页面。

## 场景介绍

自定义界面扫码能力提供扫码相机流控制接口，支持相机流的初始化、开启、暂停、释放、重新扫码功能；支持闪光灯的状态获取、开启、关闭；支持变焦比的获取和设置；支持设置相机焦点和连续自动对焦；支持对条形码、二维码、MULTIFUNCTIONAL CODE进行扫码识别（具体类型参见[ScanType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scancore#section113371139123212)），并获得码类型、码值、码位置信息、相机预览流（YUV）。该能力可用于单码和多码的扫描识别。

开发者集成自定义界面扫码能力可以自行定义扫码的界面样式，请按照业务流程完成扫码接口调用实现实时扫码功能。建议开发者基于[Sample Code](https://gitcode.com/HarmonyOS_Samples/scan-kit_-sample-code_-clientdemo_-arkts)做个性化修改。

扫码页面UX设计规范：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163520.60123715994119481500907363829724:50001231000000:2800:440CFEEFE2BD58BF4822B4743DC3F0210F4F5C5D7B0DFD39B5EAED49BC9F7E7F.png "点击放大")

说明

YUV（相机预览流图像数据）适合于扫码和识物的综合识别场景，开发者需要自己控制相机流，普通扫码场景无需关注。

## 约束与限制

- 需要请求相机的使用权限。
- 需要开发者自行实现扫码的人机交互界面。例如：多码场景需要暂停相机流由用户选择一个码图进行识别。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163520.09128392819082921530992296657550:50001231000000:2800:3CAEDAA083218E20FAAAEED171A65D79291A9376DB4B6276AF75C31C6D3EBE33.png "点击放大")

1. **发起请求：**用户向开发者的应用发起扫码请求，应用拉起已定义好的扫码界面。
2. **申请授权：**应用需要向用户申请相机权限授权。若未同意授权，则无法使用此功能。
3. **启动自定义界面扫码：**在扫码前必须调用init接口初始化自定义扫码界面，加载资源。相机流初始化结束后，调用start接口开始扫码。
4. **自定义界面扫码相机操作：**可以配置自定义界面扫码相机操作参数，调整相应功能，包括闪光灯、变焦、焦距、暂停、重启扫码等。例如：
    - 根据当前码图位置，比如当前码图太远或太近时，调用getZoom获取变焦比，setZoom接口设置变焦比，调整焦距以便于用户扫码。
    - 根据当前扫码的光线条件或根据on('lightingFlash')监听闪光灯开启时机，通过getFlashLightStatus接口先获取闪光灯状态，再调用openFlashLight/closeFlashLight接口控制闪光灯开启或关闭，以便于用户进行扫码。
    - 调用setFocusPoint设置对焦位置，resetFocus恢复默认对焦模式，以便于用户进行扫码。
    - 在应用处于前后台或其他特殊场景需要中断/重新进行扫码时，可调用stop或start接口来控制相机流达到暂停或重新扫码的目的。
5. **自定义界面扫码：**Scan Kit API在扫码完成后会返回扫码结果。同时根据开发者的需要，Scan Kit API会返回每帧相机预览流数据。如需不重启相机并重新触发一次扫码，可以在start接口的Callback异步回调中，调用rescan接口。完成扫码后，需调用release接口进行释放扫码资源的操作。
6. **获取结果：**解析码值结果跳转应用服务页。

## 接口说明

自定义界面扫码提供init、start、stop、release、getFlashLightStatus、openFlashLight、closeFlashLight、setZoom、getZoom、setFocusPoint、resetFocus、rescan、on('lightingFlash')、off('lightingFlash')接口，其中部分接口返回值有两种返回形式：Callback和Promise回调。Callback和Promise回调函数只是返回值方式不一样，功能相同。具体API说明详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api)。

|接口名|描述|
|:--|:--|
|[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section447114223245)(options?: scanBarcode.[ScanOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section1285191073117)): void|初始化自定义界面扫码，加载资源。无返回结果。|
|[start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section38711535114711)(viewControl: [ViewControl](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section8604949165313)): Promise<Array<scanBarcode.[ScanResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section10614317162112)>>|启动扫码相机流。使用Promise异步回调获取扫码结果。|
|[stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section6949611114915)(): Promise<void>|暂停扫码相机流。使用Promise异步回调返回执行结果。|
|[release](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section1109456134917)(): Promise<void>|释放扫码相机流。使用Promise异步回调返回执行结果。|
|[start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section747366165913)(viewControl: ViewControl, callback: AsyncCallback<Array<scanBarcode.ScanResult>>, frameCallback?: AsyncCallback<[ScanFrame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section1670633211200)>): void|启动扫码相机流。使用Callback异步回调返回扫码结果以及YUV图像数据。|
|[getFlashLightStatus](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section1693117333508)(): boolean|获取闪光灯状态。返回结果为布尔值，true为打开状态，false为关闭状态。|
|[openFlashLight](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section75901948175116)(): void|开启闪光灯。无返回结果。|
|[closeFlashLight](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section17980725135120)(): void|关闭闪光灯。无返回结果。|
|[setZoom](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section070810389567)(zoomValue : number): void|设置变焦比。无返回结果。|
|[getZoom](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section1699185032017)(): number|获取当前的变焦比。|
|[setFocusPoint](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section288962116197)(point: scanBarcode.[Point](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section9634457911)): void|设置相机焦点。|
|[resetFocus](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section12891152115196)(): void|设置连续自动对焦模式。|
|[rescan](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section19244173211169)(): void|触发一次重新扫码。仅对start接口Callback异步回调有效，Promise异步回调无效。|
|[stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section031674815483)(callback: AsyncCallback<void>): void|暂停扫码相机流。使用Callback异步回调返回执行结果。|
|[release](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section169321832184912)(callback: AsyncCallback<void>): void|释放扫码相机流。使用Callback异步回调返回执行结果。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section1788353253914)(type: 'lightingFlash', callback: AsyncCallback<boolean>): void|订阅闪光灯状态监听事件，当环境昏、亮状态变化时，使用Callback异步回调返回打开时机。|
|[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section128574416409)(type: 'lightingFlash', callback?: AsyncCallback<boolean>): void|注销闪光灯状态监听事件。|

## 开发步骤

自定义界面扫码接口支持自定义UI界面，识别相机流中的条形码，二维码以及MULTIFUNCTIONAL CODE，并返回码图的值、类型、码的位置信息（码图最小外接矩形左上角和右下角的坐标）以及相机预览流（YUV）。

为了方便开发者接入，我们提供了详细的样例工程供参考，推荐参考[示例工程](https://gitcode.com/HarmonyOS_Samples/scan-kit_-sample-code_-clientdemo_-arkts)接入。

以下示例为调用自定义界面扫码接口拉起相机流并返回扫码结果和相机预览流（YUV）。

1. 在开发应用前，需要先申请相机相关权限，确保应用拥有访问相机的权限。在“module.json5”文件中配置相机权限，具体配置方式，请参见[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)。
    
    |权限名|说明|授权方式|
    |:--|:--|:--|
    |ohos.permission.CAMERA|允许应用使用相机扫码。|user_grant|
    
2. 使用接口[requestPermissionsFromUser](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-abilityaccessctrl#requestpermissionsfromuser9-1)请求用户授权。具体申请方式及校验方式，请参见[向用户申请授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/request-user-authorization)。
3. 导入自定义界面扫码接口以及相关接口模块，导入方法如下。
    
    1. import { scanCore, scanBarcode, customScan } from '@kit.ScanKit';
    2. // 导入功能涉及的权限申请、回调接口
    3. import { display } from '@kit.ArkUI';
    4. import { AsyncCallback, BusinessError } from '@kit.BasicServicesKit';
    5. import { hilog } from '@kit.PerformanceAnalysisKit';
    6. import { common, abilityAccessCtrl, PermissionRequestResult } from '@kit.AbilityKit';
    
4. 遵循[业务流程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-customscan#section52491649171418)完成自定义界面扫码功能。
    
    说明
    
    1. 在设置start接口的viewControl参数时，width和height与[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent)的宽高值相同，start接口会根据XComponent的宽高比例从相机的分辨率选择最优分辨率，如果比例与相机的分辨率比例相差过大会返回内部错误。当前支持的分辨率比例为16:9、4:3、1:1。竖屏场景下，XComponent的高度需要大于宽度，且高宽比在支持的分辨率比例中。横屏场景下，XComponent的宽度需要大于高度，且宽高比在支持的分辨率比例中。
    2. XComponent的宽高需根据使用场景计算适配。例如：在开发设备为折叠屏时，需按照折叠屏的展开态和折叠态分别计算XComponent的宽高，start接口会根据XComponent的宽高适配对应的相机分辨率。设备屏幕宽高可通过[display.getDefaultDisplaySync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-display#displaygetdefaultdisplaysync9)方法获取（获取的为px单位，需要通过[px2vp](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext#px2vp12)方法转为vp）。
    
    - 通过Promise方式回调，调用自定义界面扫码接口拉起相机流并返回扫码结果。
        
        1. const TAG: string = '[customScanPage]';
        
        2. @Entry
        3. @Component
        4. struct CustomScanPage {
        5.   @State userGrant: boolean = false // 是否已申请相机权限
        6.   @State surfaceId: string = '' // XComponent组件生成id
        7.   @State isShowBack: boolean = false // 是否已经返回扫码结果
        8.   @State isFlashLightEnable: boolean = false // 是否开启了闪光灯
        9.   @State isSensorLight: boolean = false // 记录当前环境亮暗状态
        10.   @State cameraHeight: number = 640 // 设置预览流高度，默认单位：vp
        11.   @State cameraWidth: number = 360 // 设置预览流宽度，默认单位：vp
        12.   @State offsetX: number = 0 // 设置预览流x轴方向偏移量，默认单位：vp
        13.   @State offsetY: number = 0 // 设置预览流y轴方向偏移量，默认单位：vp
        14.   @State zoomValue: number = 1 // 预览流缩放比例
        15.   @State setZoomValue: number = 1 // 已设置的预览流缩放比例
        16.   @State scaleValue: number = 1 // 屏幕缩放比
        17.   @State pinchValue: number = 1 // 双指缩放比例
        18.   @State displayHeight: number = 0 // 屏幕高度，单位vp
        19.   @State displayWidth: number = 0 // 屏幕宽度，单位vp
        20.   @State scanResult: Array<scanBarcode.ScanResult> = [] // 扫码结果
        21.   private mXComponentController: XComponentController = new XComponentController()
        
        22.   async onPageShow() {
        23.     // 自定义启动第一步，用户申请权限
        24.     await this.requestCameraPermission();
        25.     // 多码扫码识别，enableMultiMode: true 单码扫码识别enableMultiMode: false
        26.     let options: scanBarcode.ScanOptions = {
        27.       scanTypes: [scanCore.ScanType.ALL],
        28.       enableMultiMode: true,
        29.       enableAlbum: true
        30.     }
        31.     // 自定义启动第二步：设置预览流布局尺寸
        32.     this.setDisplay();
        33.     try {
        34.       // 自定义启动第三步，初始化接口
        35.       customScan.init(options);
        36.     } catch (error) {
        37.       hilog.error(0x0001, TAG, `Failed to init customScan. Code: ${error.code}, message: ${error.message}`);
        38.     }
        39.   }
        
        40.   async onPageHide() {
        41.     // 页面消失或隐藏时，停止并释放相机流
        42.     this.userGrant = false;
        43.     this.isFlashLightEnable = false;
        44.     this.isSensorLight = false;
        45.     try {
        46.       customScan.off('lightingFlash');
        47.     } catch (error) {
        48.       hilog.error(0x0001, TAG, `Failed to off lightingFlash. Code: ${error.code}, message: ${error.message}`);
        49.     }
        50.     this.customScanStop();
        51.     try {
        52.       // 自定义相机流释放接口
        53.       customScan.release().catch((error: BusinessError) => {
        54.         hilog.error(0x0001, TAG,
        55.           `Failed to release customScan by promise. Code: ${error.code}, message: ${error.message}`);
        56.       })
        57.     } catch (error) {
        58.       hilog.error(0x0001, TAG, `Failed to release customScan. Code: ${error.code}, message: ${error.message}`);
        59.     }
        60.   }
        
        61.   // 用户申请权限
        62.   async reqPermissionsFromUser(): Promise<number[]> {
        63.     hilog.info(0x0001, TAG, 'reqPermissionsFromUser start');
        64.     let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
        65.     let atManager = abilityAccessCtrl.createAtManager();    
        66.     try {
        67.       const grantStatus: PermissionRequestResult =
        68.         await atManager.requestPermissionsFromUser(context, ['ohos.permission.CAMERA']);
        69.       return grantStatus.authResults;
        70.     } catch (error) {
        71.       hilog.error(0x0001, TAG, `Failed to requestPermissionsFromUser. Code: ${error.code}, message: ${error.message}`);
        72.       return [];
        73.     }
        74.   }
        
        75.   // 用户申请相机权限
        76.   async requestCameraPermission() {
        77.     let grantStatus = await this.reqPermissionsFromUser();
        78.     for (let i = 0; i < grantStatus.length; i++) {
        79.       if (grantStatus[i] === 0) {
        80.         // 用户授权，可以继续访问目标操作
        81.         hilog.info(0x0001, TAG, 'Succeeded in getting permissions.');
        82.         this.userGrant = true;
        83.         break;
        84.       }
        85.     }
        86.   }
        
        87.   // 竖屏时获取屏幕尺寸，设置预览流全屏示例
        88.   setDisplay() {
        89.     try {
        90.       // 默认竖屏
        91.       let displayClass = display.getDefaultDisplaySync();
        92.       this.displayHeight = this.getUIContext().px2vp(displayClass.height);
        93.       this.displayWidth = this.getUIContext().px2vp(displayClass.width);
        94.       let maxLen: number = Math.max(this.displayWidth, this.displayHeight);
        95.       let minLen: number = Math.min(this.displayWidth, this.displayHeight);
        96.       const RATIO: number = 16 / 9;
        97.       this.cameraHeight = maxLen;
        98.       this.cameraWidth = maxLen / RATIO;
        99.       this.offsetX = (minLen - this.cameraWidth) / 2;
        100.     } catch (error) {
        101.       hilog.error(0x0001, TAG, `Failed to getDefaultDisplaySync. Code: ${error.code}, message: ${error.message}`);
        102.     }
        103.   }
        
        104.   // toast显示扫码结果
        105.   async showScanResult(result: scanBarcode.ScanResult) {
        106.     try {
        107.       // 使用toast显示出扫码结果
        108.       this.getUIContext().getPromptAction().showToast({
        109.         message: JSON.stringify(result),
        110.         duration: 5000
        111.       });
        112.     } catch (error) {
        113.       hilog.error(0x0001, TAG, `Failed to showToast. Code: ${error.code}, message: ${error.message}`);
        114.     }
        115.   }
        
        116.   initCamera() {
        117.     this.isShowBack = false;
        118.     this.scanResult = [];
        119.     let viewControl: customScan.ViewControl = {
        120.       width: this.cameraWidth,
        121.       height: this.cameraHeight,
        122.       surfaceId: this.surfaceId
        123.     };
        124.     try {
        125.       // 自定义启动第四步，请求扫码接口，通过Promise方式回调
        126.       customScan.start(viewControl)
        127.         .then((result: Array<scanBarcode.ScanResult>) => {
        128.           hilog.info(0x0001, TAG, `result: ${JSON.stringify(result)}`);
        129.           if (result.length) {
        130.             // 解析码值结果跳转应用服务页
        131.             this.scanResult = result;
        132.             this.isShowBack = true;
        133.             // 获取到扫描结果后暂停相机流
        134.             this.customScanStop();
        135.           }
        136.         }).catch((error: BusinessError) => {
        137.         hilog.error(0x0001, TAG, `Failed to start customScan. Code: ${error.code}, message: ${error.message}`);
        138.       });
        139.     } catch (error) {
        140.       hilog.error(0x0001, TAG, `Failed to start customScan. Code: ${error.code}, message: ${error.message}`);
        141.     }
        142.   }
        
        143.   customScanStop() {
        144.     try {
        145.       customScan.stop().catch((error: BusinessError) => {
        146.         hilog.error(0x0001, TAG, `Failed to stop customScan. Code: ${error.code}, message: ${error.message}`);
        147.       })
        148.     } catch (error) {
        149.       hilog.error(0x0001, TAG, `Failed to stop customScan. Code: ${error.code}, message: ${error.message}`);
        150.     }
        151.   }
        
        152.   // 自定义扫码界面的顶部返回按钮和扫码提示
        153.   @Builder
        154.   TopTool() {
        155.     Column() {
        156.       Flex({ direction: FlexDirection.Row, justifyContent: FlexAlign.SpaceBetween, alignItems: ItemAlign.Center }) {
        157.         Text('返回')
        158.           .onClick(async () => {
        159.             this.getUIContext().getRouter().back();
        160.           })
        161.       }.padding({ left: 24, right: 24, top: 40 })
        
        162.       Column() {
        163.         Text('扫描二维码/条形码')
        164.         Text('对准二维码/条形码，即可自动扫描')
        165.       }.margin({ left: 24, right: 24, top: 24 })
        166.     }
        167.     .height(146)
        168.     .width('100%')
        169.   }
        
        170.   build() {
        171.     Stack() {
        172.       if (this.userGrant) {
        173.         Column() {
        174.           XComponent({
        175.             id: 'componentId',
        176.             type: XComponentType.SURFACE,
        177.             controller: this.mXComponentController
        178.           })
        179.             .onLoad(async () => {
        180.               hilog.info(0x0001, TAG, 'Succeeded in loading, onLoad is called.');
        181.               // 获取XComponent组件的surfaceId
        182.               this.surfaceId = this.mXComponentController.getXComponentSurfaceId();
        183.               hilog.info(0x0001, TAG, `Succeeded in getting surfaceId: ${this.surfaceId}`);
        184.               this.initCamera();
        185.               // 闪光灯监听接口
        186.               customScan.on('lightingFlash', (error, isLightingFlash) => {
        187.                 if (error) {
        188.                   hilog.error(0x0001, TAG,
        189.                     `Failed to on lightingFlash. Code: ${error.code}, message: ${error.message}`);
        190.                   return;
        191.                 }
        192.                 if (isLightingFlash) {
        193.                   this.isFlashLightEnable = true;
        194.                 } else {
        195.                   try {
        196.                     if (!customScan.getFlashLightStatus()) {
        197.                       this.isFlashLightEnable = false;
        198.                     }
        199.                   } catch (error) {
        200.                     hilog.error(0x0001, TAG,
        201.                       `Failed to get flashLightStatus. Code: ${error.code}, message: ${error.message}`);
        202.                   }
        203.                 }
        204.                 this.isSensorLight = isLightingFlash;
        205.               });
        206.             })
        207.             .width(this.cameraWidth)
        208.             .height(this.cameraHeight)
        209.             .position({ x: this.offsetX, y: this.offsetY })
        210.         }
        211.         .height('100%')
        212.         .width('100%')
        213.       }
        
        214.       Column() {
        215.         this.TopTool()
        216.         Column() {
        217.         }
        218.         .layoutWeight(1)
        219.         .width('100%')
        
        220.         Column() {
        221.           Row() {
        222.             // 闪光灯按钮，启动相机流后才能使用
        223.             Button('FlashLight')
        224.               .onClick(() => {
        225.                 let lightStatus: boolean = false;
        226.                 try {
        227.                   lightStatus = customScan.getFlashLightStatus();
        228.                 } catch (error) {
        229.                   hilog.error(0x0001, TAG,
        230.                     `Failed to get flashLightStatus. Code: ${error.code}, message: ${error.message}`);
        231.                 }
        
        232.                 // 根据当前闪光灯状态，选择打开或关闭闪光灯
        233.                 if (lightStatus) {
        234.                   try {
        235.                     customScan.closeFlashLight();
        236.                     setTimeout(() => {
        237.                       this.isFlashLightEnable = this.isSensorLight;
        238.                     }, 200);
        239.                   } catch (error) {
        240.                     hilog.error(0x0001, TAG,
        241.                       `Failed to close flashLight. Code: ${error.code}, message: ${error.message}`);
        242.                   }
        243.                 } else {
        244.                   try {
        245.                     customScan.openFlashLight();
        246.                   } catch (error) {
        247.                     hilog.error(0x0001, TAG,
        248.                       `Failed to open flashLight. Code: ${error.code}, message: ${error.message}`);
        249.                   }
        250.                 }
        251.               })
        252.               .visibility((this.userGrant && this.isFlashLightEnable) ? Visibility.Visible : Visibility.None)
        
        253.             // 扫码成功后，点击按钮后重新扫码
        254.             Button('Scan')
        255.               .onClick(() => {
        256.                 // 点击按钮重启相机流，重新扫码
        257.                 this.initCamera();
        258.               })
        259.               .visibility(this.isShowBack ? Visibility.Visible : Visibility.None)
        260.           }
        
        261.           Row() {
        262.             // 预览流设置缩放比例
        263.             Button('缩放比例,当前比例:' + this.setZoomValue)
        264.               .onClick(() => {
        265.                 // 设置相机缩放比例
        266.                 if (!this.isShowBack) {
        267.                   if (!this.zoomValue || this.zoomValue === this.setZoomValue) {
        268.                     this.setZoomValue = this.customGetZoom();
        269.                   } else {
        270.                     this.zoomValue = this.zoomValue;
        271.                     this.customSetZoom(this.zoomValue);
        272.                     setTimeout(() => {
        273.                       if (!this.isShowBack) {
        274.                         this.setZoomValue = this.customGetZoom();
        275.                       }
        276.                     }, 1000);
        277.                   }
        278.                 }
        279.               })
        280.           }
        281.           .margin({ top: 10, bottom: 10 })
        
        282.           Row() {
        283.             // 输入要设置的预览流缩放比例
        284.             TextInput({ placeholder: '输入缩放倍数' })
        285.               .type(InputType.Number)
        286.               .borderWidth(1)
        287.               .backgroundColor(Color.White)
        288.               .onChange(value => {
        289.                 this.zoomValue = Number(value);
        290.               })
        291.           }
        292.         }
        293.         .width('50%')
        294.         .height(180)
        295.       }
        
        296.       // 单码、多码扫描后，显示码图蓝点位置。点击toast码图信息
        297.       ForEach(this.scanResult, (item: scanBarcode.ScanResult) => {
        298.         if (item.scanCodeRect) {
        299.           Image($rawfile('scan_selected2.svg')) // src/main/resources/rawfile/scan_selected2.svg
        300.             .width(40)
        301.             .height(40)
        302.             .markAnchor({ x: 20, y: 20 })
        303.             .position({
        304.               x: (item.scanCodeRect.left + item?.scanCodeRect?.right) / 2 + this.offsetX,
        305.               y: (item.scanCodeRect.top + item?.scanCodeRect?.bottom) / 2 + this.offsetY
        306.             })
        307.             .onClick(() => {
        308.               this.showScanResult(item);
        309.             })
        310.         }
        311.       }, (item: scanBarcode.ScanResult) => '' + item?.scanCodeRect?.left + item?.scanCodeRect?.right + 'px')
        312.     }
        313.     // 建议相机流设置为全屏
        314.     .width('100%')
        315.     .height('100%')
        316.     .onClick((event: ClickEvent) => {
        317.       // 是否已扫描到结果
        318.       if (this.isShowBack) {
        319.         return;
        320.       }
        321.       // 点击屏幕位置，获取点击位置(x,y)，设置相机焦点
        322.       let x1 = this.getUIContext().vp2px(event.displayY) / (this.displayHeight + 0.0);
        323.       let y1 = 1.0 - (this.getUIContext().vp2px(event.displayX) / (this.displayWidth + 0.0));
        324.       try {
        325.         customScan.setFocusPoint({ x: x1, y: y1 });
        326.         hilog.info(0x0001, TAG, `Succeeded in setting focusPoint x1: ${x1}, y1: ${y1}`);
        327.       } catch (error) {
        328.         hilog.error(0x0001, TAG, `Failed to set focusPoint. Code: ${error.code}, message: ${error.message}`);
        329.       }
        330.       hilog.info(0x0001, TAG, `Succeeded in setting focusPoint x1: ${x1}, y1: ${y1}`);
        331.       // 设置连续自动对焦模式
        332.       setTimeout(() => {
        333.         try {
        334.           customScan.resetFocus();
        335.         } catch (error) {
        336.           hilog.error(0x0001, TAG, `Failed to reset focus. Code: ${error.code}, message: ${error.message}`);
        337.         }
        338.       }, 200);
        339.     }).gesture(PinchGesture({ fingers: 2 })
        340.       .onActionStart((_: GestureEvent) => {
        341.         hilog.info(0x0001, TAG, 'Pinch start');
        342.       })
        343.       .onActionUpdate((event: GestureEvent) => {
        344.         if (event) {
        345.           this.scaleValue = event.scale;
        346.         }
        347.       })
        348.       .onActionEnd((_: GestureEvent) => {
        349.         // 是否已扫描到结果
        350.         if (this.isShowBack) {
        351.           return;
        352.         }
        353.         // 获取双指缩放比例，设置变焦比
        354.         try {
        355.           let zoom = this.customGetZoom();
        356.           this.pinchValue = this.scaleValue * zoom;
        357.           this.customSetZoom(this.pinchValue);
        358.           hilog.info(0x0001, TAG, 'Pinch end');
        359.         } catch (error) {
        360.           hilog.error(0x0001, TAG, `Failed to set zoom. Code: ${error.code}, message: ${error.message}`);
        361.         }
        362.       }))
        363.   }
        
        364.   public customGetZoom(): number {
        365.     let zoom = 1;
        366.     try {
        367.       zoom = customScan.getZoom();
        368.       hilog.info(0x0001, TAG, `Succeeded in getting zoom, zoom: ${zoom}`);
        369.     } catch (error) {
        370.       hilog.error(0x0001, TAG, `Failed to get zoom. Code: ${error.code}, message: ${error?.message}`);
        371.     }
        372.     return zoom;
        373.   }
        
        374.   public customSetZoom(pinchValue: number): void {
        375.     try {
        376.       customScan.setZoom(pinchValue);
        377.       hilog.info(0x0001, TAG, `Succeeded in setting zoom.`);
        378.     } catch (error) {
        379.       hilog.error(0x0001, TAG, `Failed to set zoom. Code: ${error.code}, message: ${error?.message}`);
        380.     }
        381.   }
        382. }
        
    - 通过Callback方式回调，调用自定义界面扫码接口拉起相机流并返回扫码结果和相机预览流（YUV）。
        
        1. import { bundleManager, Permissions } from '@kit.AbilityKit';
        
        2. const TAG = '[YUV CPSample]';
        
        3. // 用户申请权限
        4. export class PermissionsUtil {
        5.   public static async checkAccessToken(permission: Permissions): Promise<abilityAccessCtrl.GrantStatus> {
        6.     let atManager = abilityAccessCtrl.createAtManager();
        7.     let grantStatus: abilityAccessCtrl.GrantStatus = -1;
        8.     // 获取应用程序的accessTokenID
        9.     let tokenId: number = 0;    
        10.     try {
        11.       let bundleInfo: bundleManager.BundleInfo =
        12.         await bundleManager.getBundleInfoForSelf(bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_APPLICATION);
        13.       let appInfo: bundleManager.ApplicationInfo = bundleInfo.appInfo;
        14.       tokenId = appInfo.accessTokenId;
        15.       // 校验应用是否被授予权限
        16.       grantStatus = await atManager.checkAccessToken(tokenId, permission);
        17.     } catch (error) {
        18.       hilog.error(0x0001, TAG,
        19.        `Failed to getBundleInfoForSelf or checkAccessToken. Code: ${error.code}, message: ${error.message}`);
        20.     }
        21.     return grantStatus;
        22.   }
        
        23.   // 申请相机权限
        24.   public static async reqPermissionsFromUser(context: Context): Promise<number[]> {
        25.     hilog.info(0x0001, TAG, 'Succeeded in getting permissions by promise.')
        26.     let atManager = abilityAccessCtrl.createAtManager();    
        27.     try {
        28.       const grantStatus: PermissionRequestResult =
        29.         await atManager.requestPermissionsFromUser(context, ['ohos.permission.CAMERA']);
        30.       return grantStatus.authResults;
        31.     } catch (error) {
        32.       hilog.error(0x0001, TAG, `Failed to requestPermissionsFromUser. Code: ${error.code}, message: ${error.message}`);
        33.       return [];
        34.     }
        35.   }
        36. }
        
        37. @Extend(Column)
        38. function mainStyle() {
        39.   .width('100%')
        40.   .height('100%')
        41.   .padding({
        42.     top: 40
        43.   })
        44.   .justifyContent(FlexAlign.Center)
        45. }
        
        46. @Entry
        47. @Component
        48. struct YUVScan {
        49.   @State userGrant: boolean = false // 是否已申请相机权限
        50.   @State surfaceId: string = '' // XComponent组件生成id
        51.   @State cameraHeight: number = 640 // 设置预览流高度，默认单位：vp
        52.   @State cameraWidth: number = 360 // 设置预览流宽度，默认单位：vp
        53.   @State zoomValue: number = 1 // 预览流缩放比例
        54.   @State setZoomValue: number = 1 // 已设置的预览流缩放比例
        55.   @State isReleaseCamera: boolean = false // 是否已释放相机流
        56.   @State scanWidth: number = 384 // XComponent宽度，默认设置384，单位vp
        57.   @State scanHeight: number = 682 // XComponent高度，默认设置682，单位vp
        58.   @State scanBottom: number = 220
        59.   @State offsetX: number = 0 // XComponent位置x轴偏移量，单位vp
        60.   @State offsetY: number = 0 // XComponent位置y轴偏移量，单位vp
        61.   @State scanCodeRect: Array<scanBarcode.ScanCodeRect> = [] // 扫码结果码图位置
        62.   @State scanFlag: boolean = false // 是否已经扫码到结果
        63.   @State scanFrameResult: string = ''
        64.   @State scaleValue: number = 1 // 屏幕缩放比
        65.   @State pinchValue: number = 1 // 双指缩放比例
        66.   @State displayHeight: number = 0 // 屏幕高度，单位vp
        67.   @State displayWidth: number = 0 // 屏幕宽度，单位vp
        68.   private mXComponentController: XComponentController = new XComponentController()
        69.   private viewControl: customScan.ViewControl = { width: 1920, height: 1080, surfaceId: this.surfaceId }
        70.   options: scanBarcode.ScanOptions = {
        71.     // 扫码类型，可选参数
        72.     scanTypes: [scanCore.ScanType.ALL],
        73.     // 是否开启多码识别，可选参数
        74.     enableMultiMode: true,
        75.     // 是否开启相册扫码，可选参数
        76.     enableAlbum: true,
        77.   }
        78.   // 返回自定义扫描结果的回调
        79.   private callback: AsyncCallback<scanBarcode.ScanResult[]> =
        80.     async (error: BusinessError, result: scanBarcode.ScanResult[]) => {
        81.       if (error && error.code) {
        82.         hilog.error(0x0001, TAG,
        83.           `Failed to get ScanResult by callback. Code: ${error.code}, message: ${error.message}`);
        84.         return;
        85.       }
        86.       // 解析码值结果跳转应用服务页
        87.       hilog.info(0x0001, TAG, `Succeeded in getting ScanResult by callback, result: ${JSON.stringify(result)}`);
        88.     }
        89.   // 返回相机帧的回调
        90.   private frameCallback: AsyncCallback<customScan.ScanFrame> =
        91.     async (error: BusinessError, frameResult: customScan.ScanFrame) => {
        92.       if (error) {
        93.         hilog.error(0x0001, TAG, `Failed to get ScanFrame by callback. Code: ${error.code}, message: ${error.message}`);
        94.         return;
        95.       }
        96.       // byteBuffer相机YUV图像数组
        97.       hilog.info(0x0001, TAG,
        98.         `Succeeded in getting ScanFrame.byteBuffer.byteLength: ${frameResult.byteBuffer.byteLength}`)
        99.       hilog.info(0x0001, TAG, `Succeeded in getting ScanFrame.width: ${frameResult.width}`)
        100.       hilog.info(0x0001, TAG, `Succeeded in getting ScanFrame.height: ${frameResult.height}`)
        101.       this.scanFrameResult = JSON.stringify(frameResult.scanCodeRects);
        102.       if (frameResult && frameResult.scanCodeRects && frameResult.scanCodeRects.length > 0 && !this.scanFlag) {
        103.         if (frameResult.scanCodeRects[0]) {
        104.           this.stopCamera();
        105.           this.scanCodeRect = [];
        106.           this.scanFlag = true;
        107.           // 码图位置信息转换
        108.           this.changeToXComponent(frameResult);
        109.         } else {
        110.           this.scanFlag = false;
        111.         }
        112.       }
        113.     }
        
        114.   // frameCallback横向码图位置信息转换为预览流XComponent对应码图位置信息
        115.   changeToXComponent(frameResult: customScan.ScanFrame) {
        116.     if (frameResult && frameResult.scanCodeRects) {
        117.       let frameHeight = frameResult.height;
        118.       let ratio = this.scanWidth / frameHeight;
        119.       frameResult.scanCodeRects.forEach((item) => {
        120.         this.scanCodeRect.push({
        121.           left: this.toFixedNumber((frameHeight - item.bottom) * ratio),
        122.           top: this.toFixedNumber(item.left * ratio),
        123.           right: this.toFixedNumber((frameHeight - item.top) * ratio),
        124.           bottom: this.toFixedNumber(item.right * ratio)
        125.         });
        126.       });
        127.       this.scanFrameResult = JSON.stringify(this.scanCodeRect);
        128.     }
        129.   }
        
        130.   toFixedNumber(no: number): number {
        131.     return Number((no).toFixed(1));
        132.   }
        
        133.   async onPageShow() {
        134.     // 自定义启动第一步，用户申请权限
        135.     const permissions: Array<Permissions> = ['ohos.permission.CAMERA'];
        136.     // 自定义启动第二步：设置预览流布局尺寸
        137.     this.setDisplay();
        138.     let grantStatus = await PermissionsUtil.checkAccessToken(permissions[0]);
        139.     if (grantStatus === abilityAccessCtrl.GrantStatus.PERMISSION_GRANTED) {
        140.       // 已经授权，可以继续访问目标操作
        141.       this.userGrant = true;
        142.       if (this.surfaceId) {
        143.         // 自定义启动第三步，初始化接口
        144.         this.initCamera();
        145.       }
        146.     } else {
        147.       // 申请相机权限
        148.       this.requestCameraPermission();
        149.     }
        150.   }
        
        151.   async onPageHide() {
        152.     this.releaseCamera();
        153.   }
        
        154.   // 用户申请权限
        155.   async requestCameraPermission() {
        156.     let grantStatus =
        157.       await PermissionsUtil.reqPermissionsFromUser(this.getUIContext().getHostContext() as common.UIAbilityContext)
        158.     let length: number = grantStatus.length;
        159.     let userGrant: boolean = false; // 用户拒绝授权，提示用户必须授权才能访问当前页面的功能，并引导用户到系统设置中打开相应的权限
        160.     for (let i = 0; i < length; i++) {
        161.       if (grantStatus[i] === 0) {
        162.         // 用户授权，可以继续访问目标操作
        163.         userGrant = true;
        164.       }
        165.     }
        166.     this.userGrant = userGrant;
        167.   }
        
        168.   // 竖屏时获取屏幕尺寸，设置预览流全屏示例
        169.   setDisplay() {
        170.     try {
        171.       // 以手机为例计算宽高
        172.       let displayClass = display.getDefaultDisplaySync();
        173.       this.displayHeight = this.getUIContext().px2vp(displayClass.height);
        174.       this.displayWidth = this.getUIContext().px2vp(displayClass.width);
        175.       if (displayClass !== null) {
        176.         this.scanWidth = this.getUIContext().px2vp(displayClass.width);
        177.         this.scanHeight = Math.round(this.scanWidth * this.viewControl.width / this.viewControl.height);
        178.         this.scanBottom = Math.max(220, this.getUIContext().px2vp(displayClass.height) - this.scanHeight);
        179.         this.offsetX = 0;
        180.         this.offsetY = 0;
        181.       }
        182.     } catch (error) {
        183.       hilog.error(0x0001, TAG, `Failed to getDefaultDisplaySync. Code: ${error.code}, message: ${error.message}`);
        184.     }
        185.   }
        
        186.   // 初始化相机流
        187.   async initCamera() {
        188.     this.isReleaseCamera = false;
        189.     try {
        190.       // 自定义启动第三步，初始化接口
        191.       customScan.init(this.options);
        192.       hilog.info(0x0001, TAG, 'Succeeded in initializing customScan with options.');
        193.     } catch (error) {
        194.       hilog.error(0x0001, TAG, `Failed to init customScan. Code: ${error.code}, message: ${error.message}`);
        195.     }
        196.     this.scanCodeRect = [];
        197.     this.scanFlag = false;
        198.     try {
        199.       // 自定义启动第四步，请求扫码接口
        200.       customScan.start(this.viewControl, this.callback, this.frameCallback);
        201.     } catch (error) {
        202.       hilog.error(0x0001, TAG, `Failed to start customScan. Code: ${error.code}, message: ${error.message}`);
        203.     }
        204.   }
        
        205.   // 暂停相机流
        206.   async stopCamera() {
        207.     if (!this.isReleaseCamera) {
        208.       try {
        209.         customScan.stop().catch((error: BusinessError) => {
        210.           hilog.error(0x0000, TAG, `Failed to stop customScan. Code: ${error.code}, message: ${error.message}`);
        211.         });
        212.       } catch (error) {
        213.         hilog.error(0x0001, TAG, `Failed to stop customScan. Code: ${error.code}, message: ${error.message}`);
        214.       }
        215.     }
        216.   }
        
        217.   // 释放相机流
        218.   async releaseCamera() {
        219.     if (!this.isReleaseCamera) {
        220.       await this.stopCamera();
        221.       try {
        222.         await customScan.release();
        223.       } catch (error) {
        224.         hilog.error(0x0001, TAG, `Failed to release customScan. Code: ${error.code}, message: ${error.message}`);
        225.       }
        226.       this.isReleaseCamera = true;
        227.     }
        228.   }
        
        229.   build() {
        230.     Stack() {
        231.       // 相机预览流XComponent
        232.       if (this.userGrant) {
        233.         Column() {
        234.           XComponent({
        235.             id: 'componentId',
        236.             type: XComponentType.SURFACE,
        237.             controller: this.mXComponentController
        238.           })
        239.             .onLoad(() => {
        240.               hilog.info(0x0001, TAG, 'Succeeded in loading, onLoad is called.');
        241.               this.surfaceId = this.mXComponentController.getXComponentSurfaceId();
        242.               hilog.info(0x0001, TAG, `Succeeded in getting surfaceId is ${this.surfaceId}`);
        243.               this.viewControl = { width: this.scanWidth, height: this.scanHeight, surfaceId: this.surfaceId };
        244.               // 启动相机进行扫码
        245.               this.initCamera();
        246.             })
        247.             .height(this.scanHeight)
        248.             .width(this.scanWidth)
        249.             .position({ x: 0, y: 0 })
        250.         }
        251.         .height('100%')
        252.         .width('100%')
        253.         .position({ x: this.offsetX, y: this.offsetY })
        254.       }
        
        255.       Column() {
        256.         Column() {
        257.         }
        258.         .layoutWeight(1)
        259.         .width('100%')
        
        260.         Column() {
        
        261.           Row() {
        262.             // 闪光灯按钮，启动相机流后才能使用
        263.             Button('FlashLight')
        264.               .onClick(() => {
        265.                 let lightStatus: boolean = false;
        266.                 try {
        267.                   lightStatus = customScan.getFlashLightStatus();
        268.                 } catch (error) {
        269.                   hilog.error(0x0001, TAG,
        270.                     `Failed to get flashLightStatus. Code: ${error.code}, message: ${error.message}`);
        271.                 }
        272.                 // 根据当前闪光灯状态，选择打开或关闭闪光灯
        273.                 if (lightStatus) {
        274.                   try {
        275.                     customScan.closeFlashLight();
        276.                   } catch (error) {
        277.                     hilog.error(0x0001, TAG,
        278.                       `Failed to close flashLight. Code: ${error.code}, message: ${error.message}`);
        279.                   }
        280.                 } else {
        281.                   try {
        282.                     customScan.openFlashLight();
        283.                   } catch (error) {
        284.                     hilog.error(0x0001, TAG,
        285.                       `Failed to open flashLight. Code: ${error.code}, message: ${error.message}`);
        286.                   }
        287.                 }
        288.               })
        289.               .visibility(this.scanFlag ? Visibility.None : Visibility.Visible)
        290.           }
        
        291.           Row() {
        292.             // 预览流设置缩放比例
        293.             Button('缩放比例,当前比例:' + this.setZoomValue)
        294.               .width(200)
        295.               .alignSelf(ItemAlign.Center)
        296.               .onClick(() => {
        297.                 // 设置相机缩放比例
        298.                 if (!this.scanFlag) {
        299.                   if (!this.zoomValue || this.zoomValue === this.setZoomValue) {
        300.                     this.setZoomValue = this.customGetZoom();
        301.                   } else {
        302.                     this.zoomValue = this.zoomValue;
        303.                     this.customSetZoom(this.zoomValue);
        304.                     setTimeout(() => {
        305.                       if (!this.scanFlag) {
        306.                         this.setZoomValue = this.customGetZoom();
        307.                       }
        308.                     }, 1000);
        309.                   }
        310.                 }
        311.               })
        312.           }
        313.           .margin({ top: 10, bottom: 10 })
        314.           .visibility(this.scanFlag ? Visibility.None : Visibility.Visible)
        
        315.           Row() {
        316.             // 输入要设置的预览流缩放比例
        317.             TextInput({ placeholder: '输入缩放倍数' })
        318.               .width(200)
        319.               .type(InputType.Number)
        320.               .borderWidth(1)
        321.               .backgroundColor(Color.White)
        322.               .onChange(value => {
        323.                 this.zoomValue = Number(value);
        324.               })
        325.           }
        326.           .visibility(this.scanFlag ? Visibility.None : Visibility.Visible)
        
        327.           Text(this.scanFlag ? '继续扫码' : '扫码中')
        328.             .height(30)
        329.             .fontSize(16)
        330.             .fontColor(Color.White)
        331.             .onClick(() => {
        332.               if (this.scanFlag) {
        333.                 this.scanFrameResult = '';
        334.                 this.initCamera();
        335.               }
        336.             })
        337.           Text('扫码结果：' + this.scanFrameResult).fontColor(Color.White).fontSize(12)
        338.         }
        339.         .width('100%')
        340.         .height(this.scanBottom)
        341.         .backgroundColor(Color.Black)
        342.       }
        343.       .mainStyle()
        
        344.       Image($rawfile('scan_back.svg')) // src/main/resources/rawfile/scan_back.svg
        345.         .width(20)
        346.         .height(20)
        347.         .position({
        348.           x: 40,
        349.           y: 40
        350.         })
        351.         .onClick(() => {
        352.           this.getUIContext().getRouter().back();
        353.         })
        
        354.       // 实时扫码码图中心点位置
        355.       if (this.scanFlag && this.scanCodeRect.length > 0) {
        356.         ForEach(this.scanCodeRect, (item: scanBarcode.ScanCodeRect) => {
        357.           Image($rawfile('scan_selected2.svg')) // src/main/resources/rawfile/scan_selected2.svg
        358.             .width(40)
        359.             .height(40)
        360.             .markAnchor({ x: 20, y: 20 })
        361.             .position({
        362.               x: (item.left + item.right) / 2 + this.offsetX,
        363.               y: (item.top + item.bottom) / 2 + this.offsetY
        364.             })
        365.         }, (item: scanBarcode.ScanCodeRect) => '' + item.left + item.right)
        366.       }
        367.     }
        368.     .width('100%')
        369.     .height('100%')
        370.     .backgroundColor(this.userGrant ? Color.Transparent : Color.Black)
        371.     .onClick((event: ClickEvent) => {
        372.       // 是否已扫描到结果
        373.       if (this.scanFlag) {
        374.         return;
        375.       }
        376.       // 点击屏幕位置，获取点击位置(x,y)，设置相机焦点
        377.       let x1 = this.getUIContext().vp2px(event.displayY) / (this.displayHeight + 0.0);
        378.       let y1 = 1.0 - (this.getUIContext().vp2px(event.displayX) / (this.displayWidth + 0.0));
        379.       try {
        380.         customScan.setFocusPoint({ x: x1, y: y1 });
        381.         hilog.info(0x0001, TAG, `Succeeded in setting focusPoint x1: ${x1}, y1: ${y1}`);
        382.       } catch (error) {
        383.         hilog.error(0x0001, TAG, `Failed to set focusPoint. Code: ${error.code}, message: ${error.message}`);
        384.       }
        385.       setTimeout(() => {
        386.         try {
        387.           customScan.resetFocus();
        388.         } catch (error) {
        389.           hilog.error(0x0001, TAG, `Failed to reset focus. Code: ${error.code}, message: ${error.message}`);
        390.         }
        391.       }, 200);
        392.     })
        393.     .gesture(PinchGesture({ fingers: 2 })
        394.       .onActionStart((_: GestureEvent) => {
        395.         hilog.info(0x0001, TAG, 'Pinch start');
        396.       })
        397.       .onActionUpdate((event: GestureEvent) => {
        398.         if (event) {
        399.           this.scaleValue = event.scale;
        400.         }
        401.       })
        402.       .onActionEnd((_: GestureEvent) => {
        403.         // 是否已扫描到结果
        404.         if (this.scanFlag) {
        405.           return;
        406.         }
        407.         // 获取双指缩放比例，设置变焦比
        408.         try {
        409.           let zoom = this.customGetZoom();
        410.           this.pinchValue = this.scaleValue * zoom;
        411.           this.customSetZoom(this.pinchValue);
        412.           hilog.info(0x0001, TAG, 'Pinch end');
        413.         } catch (error) {
        414.           hilog.error(0x0001, TAG, `Failed to set zoom. Code: ${error.code}, message: ${error.message}`);
        415.         }
        416.       }))
        417.   }
        
        418.   public customGetZoom(): number {
        419.     let zoom = 1;
        420.     try {
        421.       zoom = customScan.getZoom();
        422.       hilog.info(0x0001, TAG, `Succeeded in getting zoom, zoom: ${zoom}`);
        423.     } catch (error) {
        424.       hilog.error(0x0001, TAG, `Failed to get zoom. Code: ${error.code}, message: ${error?.message}`);
        425.     }
        426.     return zoom;
        427.   }
        
        428.   public customSetZoom(pinchValue: number): void {
        429.     try {
        430.       customScan.setZoom(pinchValue);
        431.       hilog.info(0x0001, TAG, `Succeeded in setting zoom.`);
        432.     } catch (error) {
        433.       hilog.error(0x0001, TAG, `Failed to set zoom. Code: ${error.code}, message: ${error?.message}`);
        434.     }
        435.   }
        436. }
        
5. 通过scanCodeRect数据可确定码图中心点的位置。
    
    - 以设备竖屏、充电口向下为例，使用说明如下。
        - scanCodeRect的四个点坐标如下，可根据坐标点绘制码图外围矩形框
            
            - 左上角(x, y)：(left, top)
            
            - 右上角(x, y)：(right, top)
            
            - 左下角(x, y)：(left, bottom)
            
            - 右下角(x, y)：(right, bottom)
        - 由于码图中心点坐标需和XComponent的坐标保持一致，如果XComponent的x轴和y轴存在偏移，则码图位置需做相应的偏移。例如：x轴偏移量为：offsetX；y轴偏移量为：offsetY，中心点坐标最终转换为：
            
            - x = (left + right) / 2 + offsetX
            
            - y = (top + bottom) / 2 + offsetY
    - 如果设备涉及旋转，码图中心点位置需要根据屏幕旋转角度([Display.rotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-display#%E5%B1%9E%E6%80%A7))进行变换，以保证在各旋转角度下码图中心位置正确。推荐参考[示例工程](https://gitcode.com/HarmonyOS_Samples/scan-kit_-sample-code_-clientdemo_-arkts)。
        
        例如：XComponent宽度为width，高度为height，x轴偏移量为offsetX，y轴偏移量为offsetY：
        
        - 当[Display.rotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-display#%E5%B1%9E%E6%80%A7) = 0时，中心点坐标为：
            - x = (left + right) / 2 + offsetX
            - y = (top + bottom) / 2 + offsetY
        - 当[Display.rotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-display#%E5%B1%9E%E6%80%A7) = 1时，中心点坐标为：
            - x = width - (top + bottom) / 2 + offsetX
            - y = (left + right) / 2 + offsetY
        - 当[Display.rotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-display#%E5%B1%9E%E6%80%A7) = 2时，中心点坐标为：
            - x = width - (left + right) / 2 + offsetX
            - y = height - (top + bottom) / 2 + offsetY
        - 当[Display.rotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-display#%E5%B1%9E%E6%80%A7) = 3时，中心点坐标为：
            - x = (top + bottom) / 2 + offsetX
            - y = height - (left + right) / 2+ offsetY
    
    说明
    
    从5.0.2(14)开始，由于屏幕Display对象rotation和orientation属性变更，设备旋转不同角度后码图的位置需要重新适配。
    
    - 对于5.0.2(14)之前版本，可以使用Display对象中的rotation或者orientation属性处理设备旋转不同角度后的码图位置，且需要针对设备类型做特殊适配。
    - 对于5.0.2(14)及之后版本，需要统一使用Display对象的rotation属性处理设备旋转不同角度后的码图位置，无需针对设备类型做特殊适配。
    

## 模拟器开发

从6.0.0(20)版本开始，自定义界面扫码部分接口支持模拟器开发，支持情况参考说明，使用指导请参见[使用模拟器运行应用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-run-emulator)。

说明

1. 自定义界面扫码[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section447114223245)、[start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section38711535114711)、[stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section6949611114915)、[release](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section1109456134917)、[rescan](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-customscan-api#section19244173211169)基础扫码能力接口支持在模拟器上使用，可基于上述接口完成自定义界面扫码基本功能验证。
2. 模拟器场景下，自定义界面扫码仅支持1280*720分辨率，传入其他分辨率会统一转换成1280*720。
3. 其他自定义界面扫码接口由于模拟器硬件原因暂不支持模拟器使用，调用会返回模拟器不支持。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-scanbarcode "默认界面扫码")
# 识别本地图片

更新时间: 2025-12-16 16:35

## 基本概念

图片识码能力支持对图库中的码图进行扫描识别，并获取信息。

## 场景介绍

图片识码能力支持对图库中的条形码、二维码、MULTIFUNCTIONAL CODE进行识别，并获得码类型、码值、码位置信息。该能力可用于一图单码和一图多码的识别，比如条形码、付款码等。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163523.01126896551230130761506051955431:50001231000000:2800:8935288642CCC33EAC36C08DFE8E14EA007AA94A91243527544DD011FBDD1868.png "点击放大")

1. 用户向开发者的应用发起图片识码请求。
2. 应用通过调用Scan Kit的decode接口启动图片识码。
3. Scan Kit通过回调返回图片识码结果。
4. 应用向用户返回扫码结果。

## 接口说明

接口返回值有两种返回形式：Callback和Promise回调。下表中为启动图片识码Callback和Promise形式接口，Callback和Promise只是返回值方式不一样，功能相同。具体API说明详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-imagedecode)。

|接口名|描述|
|:--|:--|
|[decode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-imagedecode#section9221156204617)(inputImage: [InputImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-imagedecode#section2194164873812), options?: scanBarcode.[ScanOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section1285191073117)): Promise<Array<scanBarcode.[ScanResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section10614317162112)>>|启动图片识码，通过InputImage传入图片信息，通过ScanOptions进行识码参数设置（options为可选参数），使用Promise异步回调返回识码结果。|
|[decode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-imagedecode#section12482559194718)(inputImage: InputImage, options: scanBarcode.ScanOptions, callback: AsyncCallback<Array<scanBarcode.ScanResult>>): void|启动图片识码，通过InputImage传入图片信息，通过ScanOptions进行识码参数设置，使用Callback异步回调返回识码结果。|
|[decode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-imagedecode#section17256144317492)(inputImage: InputImage, callback: AsyncCallback<Array<scanBarcode.ScanResult>>): void|启动图片识码，通过InputImage传入图片信息，使用Callback异步回调返回识码结果。|

## 开发步骤

图片识码接口支持识别图库中的条形码，二维码以及MULTIFUNCTIONAL CODE，并返回图片中码图的值，类型以及码的位置信息（码图最小外接矩形左上角和右下角的坐标）。

为了方便开发者接入，我们提供了详细的样例工程供参考，推荐参考[示例工程](https://gitcode.com/HarmonyOS_Samples/scan-kit_-sample-code_-clientdemo_-arkts)接入。

以下示例为调用图片识码的detectBarcode.decode接口获取码图信息。

1. 导入图片识码接口和相关接口模块，该接口提供了图片识码参数和方法，导入方法如下。
    
    1. // 导入图片识码需要的日志和picker模块
    2. import { scanCore, scanBarcode, detectBarcode } from '@kit.ScanKit';
    3. import { photoAccessHelper } from '@kit.MediaLibraryKit';
    4. import { hilog } from '@kit.PerformanceAnalysisKit';
    5. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 调用detectBarcode.decode接口解析码图。
    - 通过Promise回调函数得到扫码结果，InputImage对象中uri参数推荐通过[picker](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/photoaccesshelper-photoviewpicker)方式获取。
        
        1. @Entry
        2. @Component
        3. struct DetectPage {
        4.   build() {
        5.     Column() {
        6.       Button('Promise with options')
        7.         .backgroundColor('#0D9FFB')
        8.         .fontSize(20)
        9.         .fontColor($r('sys.color.comp_background_list_card'))
        10.         .fontWeight(FontWeight.Normal)
        11.         .align(Alignment.Center)
        12.         .type(ButtonType.Capsule)
        13.         .width('90%')
        14.         .height(40)
        15.         .margin({ top: 5, bottom: 5 })
        16.         .onClick(() => {
        17.           // 定义识码参数options
        18.           let options: scanBarcode.ScanOptions = {
        19.             scanTypes: [scanCore.ScanType.ALL],
        20.             enableMultiMode: true,
        21.           }
        22.           // 通过picker拉起图库的图片
        23.           let photoOption = new photoAccessHelper.PhotoSelectOptions();
        24.           photoOption.MIMEType = photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE;
        25.           photoOption.maxSelectNumber = 1;
        26.           let photoPicker = new photoAccessHelper.PhotoViewPicker();
        27.           photoPicker.select(photoOption).then((result) => {
        28.             // 定义识码参数inputImage，其中uri为picker选择图片
        29.             let inputImage: detectBarcode.InputImage = { uri: result.photoUris[0] };
        30.             try {
        31.               // 调用图片识码接口
        32.               detectBarcode.decode(inputImage, options).then((result: Array<scanBarcode.ScanResult>) => {
        33.                 hilog.info(0x0001, '[Scan Sample]',
        34.                   `Succeeded in getting ScanResult by promise with options, result is ${JSON.stringify(result)}`);
        35.               }).catch((error: BusinessError) => {
        36.                 hilog.error(0x0001, '[Scan Sample]',
        37.                   `Failed to get ScanResult by promise with options. Code: ${error.code}, message: ${error.message}`);
        38.               });
        39.             } catch (error) {
        40.               hilog.error(0x0001, '[Scan Sample]',
        41.                 `Failed to detectBarcode. Code: ${error.code}, message: ${error.message}`);
        42.             }
        43.           }).catch((error: BusinessError) => {
        44.             hilog.error(0x0001, '[Scan Sample]',
        45.               `Failed to select a photo. Code: ${error.code}, message: ${error.message}`);
        46.           })
        47.         });
        48.     }
        49.     .width('100%')
        50.     .height('100%')
        51.     .alignItems(HorizontalAlign.Center)
        52.     .justifyContent(FlexAlign.Center)
        53.   }
        54. }
        
    - 通过Callback回调函数得到扫码结果，InputImage对象中uri参数推荐通过[picker](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/photoaccesshelper-photoviewpicker)方式获取。
        
        1. @Entry
        
        2. @Component
        3. struct DetectPage {
        4.   build() {
        5.     Column() {
        6.       Button('Callback with options')
        7.         .backgroundColor('#0D9FFB')
        8.         .fontSize(20)
        9.         .fontColor($r('sys.color.comp_background_list_card'))
        10.         .fontWeight(FontWeight.Normal)
        11.         .align(Alignment.Center)
        12.         .type(ButtonType.Capsule)
        13.         .width('90%')
        14.         .height(40)
        15.         .margin({ top: 5, bottom: 5 })
        16.         .onClick(() => {
        17.           // 定义识码参数options
        18.           let options: scanBarcode.ScanOptions = {
        19.             scanTypes: [scanCore.ScanType.ALL],
        20.             enableMultiMode: true,
        21.             enableAlbum: true
        22.           }
        23.           // 通过选择模式拉起photoPicker界面，用户可以选择一个图片
        24.           let photoOption = new photoAccessHelper.PhotoSelectOptions();
        25.           photoOption.MIMEType = photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE;
        26.           photoOption.maxSelectNumber = 1;
        27.           let photoPicker = new photoAccessHelper.PhotoViewPicker();
        28.           photoPicker.select(photoOption).then((result) => {
        29.             // 定义识码参数inputImage，其中uri为picker选择图片
        30.             let inputImage: detectBarcode.InputImage = { uri: result.photoUris[0] };
        31.             try {
        32.               // 调用图片识码接口
        33.               detectBarcode.decode(inputImage, options,
        34.                 (error: BusinessError, result: Array<scanBarcode.ScanResult>) => {
        35.                   if (error && error.code) {
        36.                     hilog.error(0x0001, '[Scan Sample]',
        37.                       `Failed to get ScanResult by callback with options. Code: ${error.code}, message: ${error.message}`);
        38.                     return;
        39.                   }
        40.                   hilog.info(0x0001, '[Scan Sample]',
        41.                     `Succeeded in getting ScanResult by callback with options, result is ${JSON.stringify(result)}`);
        42.                 });
        43.             } catch (error) {
        44.               hilog.error(0x0001, '[Scan Sample]',
        45.                 `Failed to detectBarcode. Code: ${error.code}, message: ${error.message}`);
        46.             }
        47.           }).catch((error: BusinessError) => {
        48.             hilog.error(0x0001, '[Scan Sample]',
        49.               `Failed to select a photo. Code: ${error.code}, message: ${error.message}`);
        50.           })
        51.         });
        52.     }
        53.     .width('100%')
        54.     .height('100%')
        55.     .alignItems(HorizontalAlign.Center)
        56.     .justifyContent(FlexAlign.Center)
        57.   }
        58. }
        

## 模拟器开发

支持模拟器开发，使用指导请参见[使用模拟器运行应用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-run-emulator)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-imagerecognition "图像识码")
# 识别图像数据

更新时间: 2025-12-16 16:35

## 基本概念

图像数据识码能力支持对相机预览流数据中的码图进行扫描识别，并获取信息。

## 场景介绍

图像数据识码能力支持对相机预览流数据中的条形码、二维码、MULTIFUNCTIONAL CODE进行识别，并获得码类型、码值、码位置信息和相机变焦比。该能力可用于一图单码和一图多码的识别，比如条形码、付款码等。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163526.83183189602354605532063453217981:50001231000000:2800:5031205A9858798F06F4790220216FC6AFAF71009B5590B99EBAC5635D94E185.png "点击放大")

1. 用户向应用发起识码请求。
2. 应用通过调用[Camera Kit](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-overview)启动相机，获取预览流数据。
3. 应用通过调用Scan Kit的decodeImage接口识别码图。
4. Scan Kit通过回调返回识别结果。
5. 应用向用户返回扫码结果。

## 接口说明

识别图像数据中的码图，以Promise形式返回识别结果。具体API说明详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-imagedecode)。

|接口名|描述|
|:--|:--|
|[decodeImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-imagedecode#section387381185013)(image: [ByteImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-imagedecode#section596225419382), options?: scanBarcode.[ScanOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section1285191073117)): Promise<[DetectResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-imagedecode#section655375703713)>|启动图像识码，通过ByteImage传入图像数据信息，使用Promise异步回调返回识码结果。|

## 开发步骤

图像数据识码能力支持对相机预览流数据中的条形码、二维码、MULTIFUNCTIONAL CODE进行识别，并返回码图的值、类型、码的位置信息（码图最小外接矩形左上角和右下角的坐标，QR码支持返回四个点坐标）和相机变焦比。

为了方便开发者接入，我们提供了详细的样例工程供参考，推荐参考[示例工程](https://gitcode.com/HarmonyOS_Samples/scan-kit_-sample-code_-clientdemo_-arkts)接入。

以下示例为调用detectBarcode.decodeImage接口获取码图信息。

1. 导入图像识码接口和相关接口模块，该模块提供了图像识码参数和方法，导入方法如下。
    
    1. import { detectBarcode, scanBarcode, scanCore } from '@kit.ScanKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    3. import { camera } from '@kit.CameraKit';
    4. import { image } from '@kit.ImageKit';
    5. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 使用Camera Kit启动相机能力，实现双路预览功能，具体实现详见[双路预览](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-dual-channel-preview)。
3. 通过ImageReceiver实时获取预览图像数据，详见[双路预览](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-dual-channel-preview)，调用detectBarcode.decodeImage接口解析图像数据。请在识别完成后再释放图像数据。
    
    1. // 从ImageReceiver获取imgComponent: image.Component，预览流设置的宽高: width, height
    2. function decodeImageBuffer(imgComponent: image.Component, width: number, height: number) {
    3.   let byteImg: detectBarcode.ByteImage = {
    4.     byteBuffer: imgComponent.byteBuffer,
    5.     // 相机预览流数据旋转90°
    6.     width: height,
    7.     height: width,
    8.     format: detectBarcode.ImageFormat.NV21
    9.   };
    10.   let options: scanBarcode.ScanOptions = {
    11.     scanTypes: [scanCore.ScanType.ALL],
    12.     enableMultiMode: true,
    13.     enableAlbum: false
    14.   };
    15.   try {
    16.     detectBarcode.decodeImage(byteImg, options).then((result: detectBarcode.DetectResult) => {
    17.       hilog.info(0x0001, '[Scan Sample]',
    18.         `Succeeded in getting DetectResult by promise with options, result is ${JSON.stringify(result)}`);
    19.     }).catch((error: BusinessError) => {
    20.       hilog.error(0x0001, '[Scan Sample]',
    21.         `Failed to get DetectResult by promise with options. Code: ${error.code}, message: ${error.message}`);
    22.     })
    23.   } catch (error) {
    24.     hilog.error(0x0001, '[Scan Sample]', `Failed to detectBarcode. Code: ${error.code}, message: ${error.message}`);
    25.   }
    26. }
    
4. detectBarcode.[DetectResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-imagedecode#section655375703713)中返回的cornerPoints可参考以下说明使用。
    
    - 因为屏幕自然方向和摄像头传感器方向不同，所以cornerPoints四个点的坐标需按屏幕自然方向对应的坐标系转换。四个点的对应转换逻辑如下（假设创建的相机预览流宽高为1080 * 1920）。
        - 右下角(x, y)：(1080 - cornerPoints[0].y, cornerPoints[0].x）
        - 左下角(x, y)：(1080 - cornerPoints[1].y, cornerPoints[1].x）
        - 左上角(x, y)：(1080 - cornerPoints[2].y, cornerPoints[2].x）
        - 右上角(x, y)：(1080 - cornerPoints[3].y, cornerPoints[3].x）
    
    - 当创建的相机预览流宽高和实际预览组件XComponent的宽高不一致时，cornerPoints四个点的坐标需按缩放比例转换。例如相机预览流宽高为1080 * 1920，XComponent的宽高为width * height，则坐标缩放比例ratio为：width / 1080, 最终转换后的坐标为(x * ratio, y * ratio)。

## 模拟器开发

暂不支持模拟器使用，调用会返回错误信息“Emulator is not supported.”

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-detectbarcode "识别本地图片")
# 通过字节数组生成码图

更新时间: 2025-12-16 16:35

## 基本概念

码图生成能力支持将字节数组转换为自定义格式的码图。

## 场景介绍

码图生成能力支持将字节数组转换为自定义格式的码图。

例如：调用码图生成能力, 将字节数组转换成交通一卡通二维码使用。

## 约束与限制

- 码图生成能力支持Phone、Tablet。从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持2in1、TV设备。
- 只支持QR Code生成，根据纠错水平不同对生成参数有不同的要求，参数限制可见下表，具体接口参数限制信息请参见[CreateOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-generatebarcode#section87678254617)。
    
    说明
    
    Scan Kit识别该码图内容显示内容为乱码，这种字节数组需要专门的解码器解析，例如地铁闸机。
    
    |纠错水平|参数内容限制|
    |:--|:--|
    |LEVEL_L|字节数组长度限制建议不超过2048。|
    |LEVEL_M|字节数组长度限制建议不超过2048。|
    |LEVEL_Q|字节数组长度限制建议不超过1536。|
    |LEVEL_H|字节数组长度限制建议不超过1024。|
    
    说明
    
    - 生成码参数建议：
    - 码图颜色和背景
        
        建议使用默认颜色和背景：黑色码图、白色背景。如果码图颜色和背景对比度较小会影响识别率。
        
    - 码图边距
        
        建议使用默认边距1，单位：px，取值范围：[1, 10]。
        
    - 码图大小
        
        输入的width和height值相同且均大于等于200小于等于4096，单位：px，否则生成的码图过小会影响识别。
        
    

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163526.21644878665640886525804909667317:50001231000000:2800:24616A0CCF3E32187FD5FC0504541519D9960A6BEB8618228ADD591B0A5CDD26.png "点击放大")

1. 用户向应用发起生成码请求后，传入需要生成的码的信息，包括码的类型、宽高等。
2. 应用通过调用Scan Kit的createBarcode接口启动码图生成能力。
3. Scan Kit通过将字节数组转换为码图并返回给应用。
4. 应用向用户返回生成码结果。

## 接口说明

通过字节数组生成码图，以Promise形式生成码图。具体API说明详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-generatebarcode)。

|接口名|接口描述|
|:--|:--|
|[createBarcode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-generatebarcode#section77911759145019)(content: ArrayBuffer, options: [CreateOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-generatebarcode#section87678254617)): Promise<image.[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)>|码图生成接口，返回image.PixelMap类型的参数，可以使用Image组件渲染成图片。使用Promise异步回调返回生成的码图。|

## 开发步骤

码图生成根据传参内容直接生成所需码图，需要传入固定参数和可选参数。

为了方便开发者接入，我们提供了详细的样例工程供参考，推荐参考[示例工程](https://gitcode.com/HarmonyOS_Samples/scan-kit_-sample-code_-clientdemo_-arkts)接入。

以下示例为调用码图生成能力的createBarcode接口实现码图生成。

1. 导入码图生成接口模块，该模块提供了码图生成的参数和方法，导入方法如下。
    
    1. // 导入码图生成需要的图片模块、错误码模块
    2. import { scanCore, generateBarcode } from '@kit.ScanKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { image } from '@kit.ImageKit';
    5. import { hilog } from '@kit.PerformanceAnalysisKit';
    6. import { buffer } from '@kit.ArkTS';
    
2. 调用码图生成能力的createBarcode接口实现码图生成。
    - 通过Promise方式回调，获取生成的码图。
        
        1. const TAG: string = 'Create barcode';
        
        2. @Entry
        3. @Component
        4. struct Index {
        5.   @State pixelMap: image.PixelMap | undefined = undefined
        6.   build() {
        7.     Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        8.       Button('generateBarcode Promise').onClick(() => {
        9.         this.pixelMap = undefined;
        10.         let content: string =
        11. '0177C10DD10F7768600202312110000063458FD14112345678FFFFD381012610b746365409210201b66636540ad0200020000000000110e617003201000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000006645fbec664358ECF657CB40693c92da';
        12.         let contentBuffer: ArrayBuffer = buffer.from(content, 'hex').buffer; // 通过包含十六进制字符的字符串创建Buffer
        13.         let options: generateBarcode.CreateOptions = {
        14.           scanType: scanCore.ScanType.QR_CODE,
        15.           height: 400,
        16.           width: 400
        17.         }
        18.         try {
        19.           // 码图生成接口，成功返回PixelMap格式图片
        20.           generateBarcode.createBarcode(contentBuffer, options).then((pixelMap: image.PixelMap) => {
        21.             this.pixelMap = pixelMap;
        22.             hilog.info(0x0001, TAG, 'Succeeded in creating barCode.');
        23.           }).catch((error: BusinessError) => {
        24.             hilog.error(0x0001, TAG, `Failed to createBarCode. Code: ${error.code}, message: ${error.message}`);
        25.           })
        26.         } catch (error) {
        27.           hilog.error(0x0001, TAG,
        28.             `Failed to createBarcode by Promise with options. Code: ${error.code}, message: ${error.message}`);
        29.         }
        30.       })
        31.       // 获取生成码后显示
        32.       if (this.pixelMap) {
        33.         Image(this.pixelMap).width(300).height(300).objectFit(ImageFit.Contain)
        34.       }
        35.     }
        36.     .width('100%')
        37.     .height('100%')
        38.   }
        39. }
        

## 模拟器开发

暂不支持模拟器使用，调用会返回错误信息“Emulator is not supported.”

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-barcodegenerate "通过文本生成码图")
# 如何添加“扫码直达”服务的快速入口

更新时间: 2025-12-16 16:35

**问题现象**

有些用户编辑过控制中心，删除了默认存在的“扫一扫”入口，后续如何添加。

**解决措施**

控制中心编辑添加“扫一扫”入口：手机下滑菜单栏，打开控制中心，点击编辑按钮，在编辑区域中添加选择“扫一扫”后保存，即可在下拉控制列表中找到。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-faq "Scan Kit常见问题")
# 如何添加“扫码直达”服务的快速入口

更新时间: 2025-12-16 16:35

**问题现象**

有些用户编辑过控制中心，删除了默认存在的“扫一扫”入口，后续如何添加。

**解决措施**

控制中心编辑添加“扫一扫”入口：手机下滑菜单栏，打开控制中心，点击编辑按钮，在编辑区域中添加选择“扫一扫”后保存，即可在下拉控制列表中找到。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-faq "Scan Kit常见问题")
# 扫码直达跳转失败

更新时间: 2025-12-16 16:35

**问题现象**

扫码直达跳转失败。

**解决措施**

请检查App Linking配置是否正确：

1. 检查开发者网站服务器配置是否正确。
2. 检查App Linking中网址域名关联是否正确。
3. 检查应用的“module.json5”文件中域名关联是否正确。
4. 检查应用的签名是否正确，参考[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

详情参考：App Linking的[FAQ](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-linking-startupapp#section145763212066)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-faq-1 "如何添加“扫码直达”服务的快速入口")
# Scan Kit无法识别多个码图

更新时间: 2025-12-16 16:35

**问题现象**

实时扫描多个码图时，只返回一个码图结果。

**解决措施**

1. 检查[ScanOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-scanbarcode-api#section1285191073117)的enableMultiMode参数是否设置为true，开启多码扫描。
2. 检查ScanOptions的scanTypes参数是否已设置相应的码类型。
3. 检查码图类型是否在Scan Kit所定义支持的码图类型内。
4. 目前实时扫描多个码图时，最多仅支持返回4个码图。
5. 如还未解决，请通过[在线提单](https://developer.huawei.com/consumer/cn/support/feedback/#/)提交问题，华为支持人员会及时处理。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-faq-2 "扫码直达跳转失败")
# 上传软件包时提示“上传的软件包与声明支持设备不一致”

更新时间: 2025-12-16 16:35

**问题现象**

在进行应用上架操作中，上传软件包时，AGC平台提示“上传的软件包与声明支持设备不一致，请重新上传或修改可支持设备”。

**解决措施**

1. 检查工程“entry”路径下，“module.json5”文件中的“deviceTypes”是否和AGC平台上应用支持的设备勾选的应用基本信息中支持的设备保持一致。如支持设备勾选手机，那么“module.json5”中“deviceTypes”需配置为“phone”。
2. 如还未解决，请通过[在线提单](https://developer.huawei.com/consumer/cn/support/feedback/#/)提交问题，华为支持人员会及时处理。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-faq-3 "Scan Kit无法识别多个码图")
