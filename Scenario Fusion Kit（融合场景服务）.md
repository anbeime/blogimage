# Scenario Fusion Kit简介

更新时间: 2025-12-16 16:35

Scenario Fusion Kit（融合场景服务）基于ArkUI框架组件开发，提供跨多个子系统融合的场景化组件，降低开发者接入复杂度，确保鸿蒙生态体验统一。ArkUI一行核心代码启用，智能推荐输入建议，复杂表单一键填充。融合场景服务通过完善应用/元服务的系统开发能力，进一步丰富鸿蒙生态，满足开发者在HarmonyOS系统下的服务闭环诉求。

## 业务价值

- 提升开发效率
    
    跨子系统构建体验一致的场景化组件，只需开发者一次引入，支持应用/元服务高频通用场景便捷开发，提升应用/元服务开发效率。
    
- 规范组件单击行为，保障用户体验一致性
    
    Button组件与华为账号、系统设置等部件协同，规范组件单击行为，保障用户体验一致性。
    
- 提供场景化的输入建议，实现复杂表单一键填充
    
    智能填充帮助用户轻松地完成表单填写。集成ArkUI输入组件后，一行代码配置快速启用功能。
    

## 约束和限制

### 支持的国家和地区

|场景|国家/地区|
|:--|:--|
|场景化Button|只支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。|
|场景化Input|只支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。|
|场景化API|请参见[支持的国家/地区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-appendix-support-regions)。|
|文件路径转换API|只支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。|
|智能填充服务|只支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。|

### 支持的设备

|场景|支持设备|
|:--|:--|
|快速验证手机号Button|支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持TV设备。|
|选择头像Button|Phone、Tablet、2in1|
|打开APP Button|支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持TV设备。|
|选择收货地址Button|Phone、Tablet、2in1|
|选择发票抬头Button|Phone、Tablet、2in1|
|地图选点Button|支持Phone和Tablet设备，并且从5.0.1（13）版本开始，新增支持2in1设备。|
|权限设置Button|支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持TV设备。|
|服务动态授权码Button|Phone、Tablet|
|元服务分享Button|Phone、Tablet|
|反馈与投诉Button|Phone、Tablet|
|省市区选择器Input|Phone、Tablet、2in1|
|通过API获取系统信息属性|支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持Wearable和TV设备。|
|通过API异步获取系统信息属性|支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持Wearable和TV设备。|
|通过API获取系统设置属性|支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持Wearable和TV设备。|
|通过API展示关注组件|Phone、Tablet|
|文件路径转换API|Phone、Tablet|
|智能填充服务|支持Phone、Tablet设备，并且从5.1.0(18)版本开始，新增支持2in1设备。|

### 模拟器支持范围

- 本kit支持模拟器开发，差异可参考[模拟器与真机的差异](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-specification)。
- 模拟器与真机存在部分支持能力差异，以Phone为例详情如下：

|场景|x86（模拟器）|arm（模拟器）|
|:--|:--|:--|
|快速验证手机号Button|不支持|支持|
|选择头像Button|不支持|支持|
|打开APP Button|支持|支持|
|选择收货地址Button|不支持|支持|
|选择发票抬头Button|不支持|不支持|
|地图选点Button|不支持|支持|
|权限设置Button|支持|支持|
|服务动态授权码Button|不支持|不支持|
|元服务分享Button|不支持|不支持|
|反馈与投诉Button|不支持|不支持|
|通过API获取系统信息属性|支持|支持|
|通过API异步获取系统信息属性|支持|支持|
|通过API获取系统设置属性|支持|支持|
|通过API展示关注组件|不支持|不支持|
|省市区选择器Input|支持|支持|
|智能填充服务|不支持|不支持|
|文件路径转换API|不支持|不支持|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-guide "Scenario Fusion Kit（融合场景服务）")
# 开发准备

更新时间: 2025-12-16 16:36

请先参考“[应用开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview)”完成基本准备工作及指纹配置，再继续进行以下开发活动。

## 申请权限

开发者需要根据实际场景申请对应权限，请保证符合[权限使用的基本原则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-permission-mgmt-overview#%E6%9D%83%E9%99%90%E4%BD%BF%E7%94%A8%E7%9A%84%E5%9F%BA%E6%9C%AC%E5%8E%9F%E5%88%99)。然后参考[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)声明对应权限。

|权限|使用场景|
|:--|:--|
|ohos.permission.GET_WIFI_INFO|使用场景化API获取Wi-Fi信息需要申请该权限（使用5.0.1(13)及以上版本时不需要设置该权限）。|
|ohos.permission.ACCESS_BLUETOOTH|使用场景化API获取蓝牙信息需要申请该权限（使用5.0.1(13)及以上版本时不需要设置该权限）。|

说明

获取用户程序访问控制权限可参考[程序访问控制管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-abilityaccessctrl#requestpermissionsfromuser9)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-introduction "Scenario Fusion Kit简介")
# 快速验证手机号Button

更新时间: 2025-12-16 16:36

## 场景介绍

快速验证手机号Button功能用于帮助开发者向用户发起手机号申请，应用在满足《[常见类型移动互联网应用程序必要个人信息范围规定](http://www.cac.gov.cn/2021-03/22/c_1617990997054277.htm)》（对第三方网站的内容，华为公司不承担任何责任）中使用手机号的必要业务场景，经用户同意后，应用可获取手机号，为用户提供相应服务（详见快速验证[场景介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-get-phonenumber#section175151155165314)）。

运行示例代码单击“快速验证手机号”按钮，拉起验证页面（完整场景可参考[快速验证](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-get-phonenumber)）。

## 约束和限制

快速验证手机号Button支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持TV设备。

说明

应用/元服务仅在首次使用时需要用户进行授权，授权成功后，后续只验证授权手机号，不可修改。

## 前提条件

参见[开发前提](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-get-phonenumber#section2011736191112)。

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    1. import { FunctionalButton, functionalButtonComponentManager } from '@kit.ScenarioFusionKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 在容器中声明FunctionalButton，指定Button的openType，并设置对应的回调函数，代码如下：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   build() {
    5.     Row() {
    6.       Column() {
    7.         // 声明FunctionalButton。
    8.         FunctionalButton({
    9.           params: {
    10.             // OpenType.GET_PHONE_NUMBER表示该按钮用于快速验证手机号码。
    11.             openType: functionalButtonComponentManager.OpenType.GET_PHONE_NUMBER,
    12.             label: '快速验证手机号',
    13.             // 调整按钮样式。 
    14.             styleOption: {
    15.               styleConfig: new functionalButtonComponentManager.ButtonConfig()
    16.                 .fontSize(20)
    17.             },
    18.           },
    19.           // 当OpenType为GET_PHONE_NUMBER时，回调必须为onGetPhoneNumber。
    20.           controller: new functionalButtonComponentManager.FunctionalButtonController()
    21.             .onGetPhoneNumber((err, data) => {
    22.               if (err) {
    23.                 // 错误日志处理。
    24.                 hilog.error(0x0000, "testTag", "error: %{public}d %{public}s", err.code, err.message);
    25.                 return;
    26.               }
    27.               // 成功日志处理。
    28.               hilog.info(0x0000, "testTag", "succeeded in authenticating");
    29.               // 授权码处理。 
    30.               let authorizationCode = data.code;
    31.             })
    32.         })
    33.       }
    34.       .width('100%')
    35.     }
    36.     .height('100%')
    37.   }
    38. }
    
    说明
    
    - openType参数填写"functionalButtonComponentManager.OpenType.GET_PHONE_NUMBER"指定Button为快速验证手机号类型。
    - controller参数必须对应填写"new functionalButtonComponentManager.FunctionalButtonController().onGetPhoneNumber"。
    - 若成功调用，可通过回调函数中的临时登录凭证（Authorization Code）获取真实手机号，临时登录凭证时效5分钟，具体操作可参考[服务端开发](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-get-phonenumber#section380015370555)。
    - 可使用自定义Modifier设置按钮样式，参考[示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbuttoncomponentmanager#section1251915241170)。
    
    其他参数请参考：[FunctionalButton（Button组件）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbutton)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-button "场景化Button")
# 选择头像Button

更新时间: 2025-12-16 16:36

## 场景介绍

选择头像Button功能可以帮助开发者调用对应Button组件快速拉起头像选择页面，供用户完成华为账号头像或其他头像的选择与展示。

运行示例代码单击头像按钮，拉起选择头像页面来设置头像（完整场景可参考[获取头像昵称](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-get-avatar-nickname)）。

## 前提条件

参见[开发前提](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-get-avatar-nickname#section41863510349)。

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    1. import { FunctionalButton, functionalButtonComponentManager } from '@kit.ScenarioFusionKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 在容器中声明FunctionalButton，指定Button的openType，并设置对应的回调函数，代码如下：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   // 将account.png文件添加到/resources/base/media/目录中。否则，将显示错误信息，提示找不到该文件。
    5.   @State url: ResourceStr = $r('app.media.account');
    
    6.   build() {
    7.     Column() {
    8.       // 声明FunctionalButton。
    9.       FunctionalButton({
    10.         params: {
    11.           // OpenType.CHOOSE_AVATAR表示该按钮用于选择头像。
    12.           openType: functionalButtonComponentManager.OpenType.CHOOSE_AVATAR,
    13.           label: '',
    14.           // 调整按钮样式。
    15.           styleOption: {
    16.             styleConfig: new functionalButtonComponentManager.ButtonConfig()
    17.               .type(ButtonType.Normal)
    18.               .backgroundImage(this.url)
    19.               .backgroundImageSize(ImageSize.Cover)
    20.               .width(80)
    21.               .height(80)
    22.               .backgroundColor('#E5E5E5')
    23.           },
    24.         },
    25.         // 当OpenType设置为CHOOSE_AVATAR时，回调函数必须是onChooseAvatar。 
    26.         controller: new functionalButtonComponentManager.FunctionalButtonController().onChooseAvatar((err, data) => {
    27.           if (err) {
    28.             // 错误日志处理。
    29.             hilog.error(0x0000, "testTag", "error: %{public}d %{public}s", err.code, err.message);
    30.             return;
    31.           }
    32.           // 成功日志处理。
    33.           hilog.info(0x0000, "testTag", "succeeded in choosing avatar");
    34.           this.url = data.avatarUri!;
    35.         })
    36.       })
    37.     }
    38.     .padding({ top: 200 })
    39.     .height('100%')
    40.     .width('100%')
    41.   }
    42. }
    
    说明
    
    - openType参数填写"functionalButtonComponentManager.OpenType.CHOOSE_AVATAR"指定Button为选择头像类型。
    - controller参数必须对应填写"new functionalButtonComponentManager.FunctionalButtonController().onChooseAvatar"。
    - 若成功调用，可通过回调函数中的"avatarUri"获取头像图片的地址。
    - 可使用自定义Modifier设置按钮样式，参考[示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbuttoncomponentmanager#section1251915241170)。
    
    其他参数请参考：[FunctionalButton（Button组件）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbutton)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-button-getphonenumber "快速验证手机号Button")
# 打开APP Button

更新时间: 2025-12-16 16:37

## 场景介绍

打开APP功能可以帮助调用对应Button组件打开另一个应用。

运行示例代码单击“打开APP”按钮，出现提示弹窗，单击“允许”，跳转至新的应用页面。

说明

弹窗是否弹出以及弹窗效果与跳转目标APP相关。

## 约束和限制

打开APP Button支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持TV设备。

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    1. import { FunctionalButton, functionalButtonComponentManager } from '@kit.ScenarioFusionKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 在容器中声明FunctionalButton，指定Button的openType，并设置对应的回调函数，代码如下：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   build() {
    5.     Row() {
    6.       Column() {
    7.         // 声明FunctionalButton。
    8.         FunctionalButton({
    9.           params: {
    10.             // OpenType.LAUNCH_APP表示该按钮用于启动应用。
    11.             openType: functionalButtonComponentManager.OpenType.LAUNCH_APP,
    12.             label: '打开APP',
    13.             // 当OpenType为functionButtonComponentManager.OpenType.LAUNCH_APP时，appParam为必填项。
    14.             appParam: {
    15.               bundleName: "xxx",
    16.               abilityName: "xxx"
    17.             },
    18.             // 调整按钮样式。
    19.             styleOption: {
    20.               styleConfig: new functionalButtonComponentManager.ButtonConfig()
    21.                 .fontSize(20)
    22.             },
    23.           },
    24.           // 当OpenType设置为LAUNCH_APP时，回调函数必须是onLaunchAPP。 
    25.           controller: new functionalButtonComponentManager.FunctionalButtonController().onLaunchApp((err) => {
    26.             if (err) {
    27.               // 错误日志处理。
    28.               hilog.error(0x0000, "testTag", "error: %{public}d %{public}s", err.code, err.message);
    29.               return;
    30.             }
    31.             // 处理成功。成功时不会返回任何值。 
    32.             hilog.info(0x0000, "testTag", "succeeded in launching app");
    33.           })
    34.         })
    35.       }
    36.       .width('100%')
    37.     }
    38.     .height('100%')
    39.   }
    40. }
    
    说明
    
    - openType参数填写"functionalButtonComponentManager.OpenType.LAUNCH_APP"指定Button为打开APP类型。
    - openType为"functionalButtonComponentManager.OpenType.LAUNCH_APP"时，appParam参数必填。
    - "bundleName"为包名，"abilityName"为Ability名称。
    - controller参数必须对应填写"new functionalButtonComponentManager.FunctionalButtonController().onLaunchApp"。
    - 可使用自定义Modifier设置按钮样式，参考[示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbuttoncomponentmanager#section1251915241170)。
    
    其他参数请参考：[FunctionalButton（Button组件）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbutton)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-button-chooseavatar "选择头像Button")
# 选择收货地址Button

更新时间: 2025-12-16 16:37

## 场景介绍

选择收货地址Button功能可以帮助开发者调用对应Button组件快速拉起地址选择页面，并返回用户选择的收货地址。

运行示例代码单击“选择收货地址”按钮，拉起选择地址页面选择已保存的地址，也可单击“管理/新增收货地址”进入添加收货地址页面（完整场景可参考[获取收货地址](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-choose-address-dev)）。

## 前提条件

参见[开发前提](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-choose-address-dev#section1061219267293)。

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    1. import { FunctionalButton, functionalButtonComponentManager } from '@kit.ScenarioFusionKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 在容器中声明FunctionalButton，指定Button的openType，并设置对应的回调函数，代码如下：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   build() {
    5.     Row() {
    6.       Column() {
    7.         // 声明FunctionalButton。
    8.         FunctionalButton({
    9.           params: {
    10.             // OpenType.CHOOSE_ADDRESS表示该按钮用于选择收货地址。
    11.             openType: functionalButtonComponentManager.OpenType.CHOOSE_ADDRESS,
    12.             label: '选择收货地址',
    13.             // 调整按钮样式。 
    14.             styleOption: {
    15.               bgColor: functionalButtonComponentManager.ColorType.DEFAULT,
    16.               size: functionalButtonComponentManager.SizeType.DEFAULT,
    17.               plain: false,
    18.               disabled: false,
    19.               loading: false,
    20.               hoverClass: functionalButtonComponentManager.HoverClassType.HOVER_CLASS,
    21.               hoverStartTime: 0,
    22.               hoverStayTime: 0,
    23.               styleConfig: new functionalButtonComponentManager.ButtonConfig()
    24.                 .fontSize(20)
    25.             },
    26.           },
    27.           // 当OpenType设置为CHOOSE_ADDRESS时，回调必须为onChooseAddress。
    28.           controller: new functionalButtonComponentManager.FunctionalButtonController()
    29.             .onChooseAddress((err, data) => {
    30.               if (err) {
    31.                 // 错误日志处理。
    32.                 hilog.error(0x0000, "testTag", "error: %{public}d %{public}s", err.code, err.message);
    33.                 return;
    34.               }
    35.               // 成功日志处理。
    36.               hilog.info(0x0000, "testTag", "succeeded in choosing address");
    37.               // 获取地址信息。 
    38.               let userName: string = data.userName;
    39.               let mobileNumber: string = data.mobileNumber as string;
    40.               let countryCode: string = data.countryCode as string;
    41.               let provinceName: string = data.provinceName as string;
    42.               let cityName: string = data.cityName as string;
    43.               let districtName: string = data.districtName as string;
    44.               let streetName: string = data.streetName as string;
    45.               let detailedAddress: string = data.detailedAddress;
    46.             })
    47.         })
    48.       }.width('100%')
    49.     }.height('100%')
    50.   }
    51. }
    
    说明
    
    - openType参数填写"functionalButtonComponentManager.OpenType.CHOOSE_ADDRESS"指定Button为选择收货地址类型。
    - controller参数必须对应填写"new functionalButtonComponentManager.FunctionalButtonController().onChooseAddress"。
    - 可使用自定义Modifier设置按钮样式，参考[示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbuttoncomponentmanager#section1251915241170)。
    
    其他参数请参考：[FunctionalButton（Button组件）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbutton)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-button-launchapp "打开APP Button")
# 选择发票抬头Button

更新时间: 2025-12-16 16:37

## 场景介绍

选择发票抬头Button功能可以帮助开发者调用对应Button组件跳转发票抬头选择页面，供用户完成已保存发票抬头的选择。

运行示例代码单击“选择发票抬头”按钮，拉起选择发票抬头页面可选择已保存发票，也可单击“管理发票抬头”进入新增企业/个人发票抬头页面（完整场景请参考[获取发票抬头](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-select-invoice-title)）。

## 前提条件

参见[开发前提](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-select-invoice-title#section74611018114315)。

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    1. import { FunctionalButton, functionalButtonComponentManager } from '@kit.ScenarioFusionKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 在容器中声明FunctionalButton，指定Button的openType，并设置对应的回调函数，代码如下：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   build() {
    5.     Row() {
    6.       Column() {
    7.         // 声明FunctionalButton。
    8.         FunctionalButton({
    9.           params: {
    10.             // OpenType.CHOOSE_INVOICE_TITLE表示该按钮用于选择发票抬头。
    11.             openType: functionalButtonComponentManager.OpenType.CHOOSE_INVOICE_TITLE,
    12.             label: '选择发票抬头',
    13.             // 调整按钮样式。
    14.             styleOption: {
    15.               bgColor: functionalButtonComponentManager.ColorType.DEFAULT,
    16.               size: functionalButtonComponentManager.SizeType.DEFAULT,
    17.               plain: false,
    18.               disabled: false,
    19.               loading: false,
    20.               hoverClass: functionalButtonComponentManager.HoverClassType.HOVER_CLASS,
    21.               hoverStartTime: 0,
    22.               hoverStayTime: 0,
    23.               styleConfig: new functionalButtonComponentManager.ButtonConfig()
    24.                 .fontSize(20)                
    25.             },
    26.           },
    27.           // 当OpenType为CHOOSE_INVOICE_TITLE时，回调必须为onChooseInvoiceTitle。
    28.           controller: new functionalButtonComponentManager.FunctionalButtonController()
    29.             .onChooseInvoiceTitle((err, data) => {
    30.               if (err) {
    31.                 // 错误日志处理。
    32.                 hilog.error(0x0000, "testTag", "error: %{public}d %{public}s", err.code, err.message);
    33.                 return;
    34.               }
    35.               // 成功日志处理。
    36.               hilog.info(0x0000, "testTag", "succeeded in obtaining invoice title");
    37.               // 获取发票信息。 
    38.               let type: string = data.type;
    39.               let title: string = data.title;
    40.               let taxNumber: string = data.taxNumber;
    41.               let companyAddress: string | undefined = data.companyAddress;
    42.               let telephone: string | undefined = data.telephone;
    43.               let bankName: string | undefined = data.bankName;
    44.               let bankAccount: string | undefined = data.bankAccount;
    45.             })
    46.         })
    47.       }
    48.       .width('100%')
    49.     }
    50.     .height('100%')
    51.   }
    52. }
    
    说明
    
    - openType参数填写"functionalButtonComponentManager.OpenType.CHOOSE_INVOICE_TITLE"指定Button为选择发票抬头类型。
    - controller参数必须对应填写"new functionalButtonComponentManager.FunctionalButtonController().onChooseInvoiceTitle"。
    - 可使用自定义Modifier设置按钮样式，参考[示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbuttoncomponentmanager#section1251915241170)。
    
    其他参数请参考：[FunctionalButton（Button组件）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbutton)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-button-ship-to "选择收货地址Button")
# 地图选点Button

更新时间: 2025-12-16 16:37

## 场景介绍

地图选点Button功能可以帮助开发者调用Button组件拉起Map Kit的地图选点页面，用户在地图中选择位置后，位置相关信息返回Button页面。

运行示例代码单击“地图选点”按钮拉起地图选点页面。

## 约束和限制

地图选点Button支持Phone和Tablet设备，并且从5.0.1（13）版本开始，新增支持2in1设备。

## 前提条件

参见[开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-config-agc)。

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    1. import { FunctionalButton, functionalButtonComponentManager } from '@kit.ScenarioFusionKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 在容器中声明FunctionalButton，指定Button的openType，并设置对应的回调函数，代码如下：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   build() {
    5.     Row() {
    6.       Column() {
    7.         // 声明FunctionalButton。
    8.         FunctionalButton({
    9.           params: {
    10.             // OpenType.CHOOSE_LOCATION表示该按钮用于在地图上选择位置。
    11.             openType: functionalButtonComponentManager.OpenType.CHOOSE_LOCATION,
    12.             label: '地图选点',
    13.             // 调整按钮样式。
    14.             styleOption: {
    15.               bgColor: functionalButtonComponentManager.ColorType.DEFAULT,
    16.               size: functionalButtonComponentManager.SizeType.DEFAULT,
    17.               plain: false,
    18.               disabled: false,
    19.               loading: false,
    20.               hoverClass: functionalButtonComponentManager.HoverClassType.HOVER_CLASS,
    21.               hoverStartTime: 0,
    22.               hoverStayTime: 0,
    23.               styleConfig: new functionalButtonComponentManager.ButtonConfig()
    24.                 .fontSize(20)                
    25.             },
    26.           },
    27.           // 当OpenType设置为CHOOSE_LOCATION时，回调必须为onChooseLocation。
    28.           controller: new functionalButtonComponentManager.FunctionalButtonController()
    29.             .onChooseLocation((err, data) => {
    30.               if (err) {
    31.                 // 错误日志处理。
    32.                 hilog.error(0x0000, "testTag", "error: %{public}d %{public}s", err.code, err.message);
    33.                 return;
    34.               }
    35.               // 成功日志处理。
    36.               hilog.info(0x0000, "testTag", "succeeded in choosing location");
    37.               let name: string = data.name;
    38.               let address: string = data.address;
    39.               let longitude: number = data.longitude;
    40.               let latitude: number = data.latitude;
    41.             })
    42.         })
    43.       }
    44.       .width('100%')
    45.     }
    46.     .height('100%')
    47.   }
    48. }
    
    说明
    
    - openType参数填写"functionalButtonComponentManager.OpenType.CHOOSE_LOCATION"指定Button为打开地图选点类型。
    - controller参数必须对应填写"new functionalButtonComponentManager.FunctionalButtonController().onChooseLocation"。
    - 可使用自定义Modifier设置按钮样式，参考[示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbuttoncomponentmanager#section1251915241170)。
    
    其他参数请参考：[FunctionalButton（Button组件）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbutton)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-button-invoice-title "选择发票抬头Button")
# 权限设置Button

更新时间: 2025-12-16 16:37

## 场景介绍

权限设置Button可以帮助开发者调用对应Button组件，二次拉起权限设置弹框。

运行示例代码单击“请求用户授权”按钮触发首次权限设置弹框，选择“不允许”后，单击“权限设置”按钮拉起二次授权页面。

## 约束和限制

权限设置Button支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持TV设备。

说明

仅支持UIAbility/UIExtensionAbility。

在调用此接口前，应用需要先调用[requestPermissionsFromUser](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-abilityaccessctrl#requestpermissionsfromuser9)，如果用户在首次权限设置弹框时已授权，调用当前接口将无法拉起二次授权页面。

## 前提条件

- 调用[requestPermissionsFromUser](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-abilityaccessctrl#requestpermissionsfromuser9)接口，用户在首次权限设置弹框时拒绝授权。
- 参见[开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-preparations)。

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    1. import { FunctionalButton, functionalButtonComponentManager } from '@kit.ScenarioFusionKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    3. import { abilityAccessCtrl, common, PermissionRequestResult } from '@kit.AbilityKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 在容器中声明FunctionalButton，指定Button的openType，并设置对应的回调函数，代码如下：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   build() {
    5.     Row() {
    6.       Column({ space: 3 }) {
    7.         // 调用requestPermissionsFromUser接口Button。
    8.         Button('请求用户授权')
    9.           .fontSize(20)          
    10.           .onClick(() => {
    11.             let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
    12.             let context: Context = this.getUIContext().getHostContext() as common.UIAbilityContext;
    13.             try {
    14.               // 在module.json5文件中添加ohos.permission.READ_CALENDAR、ohos.permission.WRITE_CALENDAR权限。
    15.               atManager.requestPermissionsFromUser(context,
    16.                 ['ohos.permission.READ_CALENDAR', 'ohos.permission.WRITE_CALENDAR'],
    17.                 (err: BusinessError, data: PermissionRequestResult) => {
    18.                   if (err) {
    19.                     hilog.error(0x0000, "testTag", "failed in requesting Permissions from user : %{public}d %{public}s",
    20.                       err.code, err.message);
    21.                   } else {
    22.                     hilog.info(0x0000, "testTag", 'data permissions: %{public}s', data.permissions?.join(','));
    23.                     hilog.info(0x0000, "testTag", 'data authResults: %{public}s', data.authResults?.join(','));
    24.                     hilog.info(0x0000, "testTag", 'data dialogShownResults: %{public}s', data.dialogShownResults?.join(','));
    25.                   }
    26.                 })
    27.             } catch (err) {
    28.               hilog.error(0x0000, "testTag", "error: %{public}d %{public}s", err.code, err.message);
    29.             }
    30.           })
    
    31.         // 声明FunctionalButton。
    32.         FunctionalButton({
    33.           params: {
    34.             // OpenType.PERMISSION_SETTING表示该按钮用于设置权限。
    35.             openType: functionalButtonComponentManager.OpenType.PERMISSION_SETTING,
    36.             label: '权限设置',
    37.             permissionListParam: ['ohos.permission.READ_CALENDAR', 'ohos.permission.WRITE_CALENDAR'],
    38.             // 调整按钮样式。
    39.             styleOption: {
    40.               styleConfig: new functionalButtonComponentManager.ButtonConfig()
    41.                 .fontSize(20)                
    42.             },
    43.           },
    44.           // 当OpenType设置为PERMISSION_SETTING时，回调必须为onPermissionSetting。
    45.           controller: new functionalButtonComponentManager.FunctionalButtonController().onPermissionSetting((err,
    46.             data) => {
    47.             if (err) {
    48.               // 错误日志处理。
    49.               hilog.error(0x0000, "testTag", "error: %{public}d %{public}s", err.code, err.message);
    50.               return;
    51.             }
    52.             // 成功日志处理。
    53.             hilog.info(0x0000, "testTag", "succeeded in setting permission ");
    54.             let result = data.permissionResult;
    55.             result.forEach(res => {
    56.               hilog.info(0x0000, "testTag", "data: %{public}s", String(res));
    57.             })
    58.           })
    59.         })
    60.       }
    61.       .width('100%')
    62.     }
    63.     .height('100%')
    64.   }
    65. }
    
    说明
    
    - openType参数填写"functionalButtonComponentManager.OpenType.PERMISSION_SETTING"指定Button为权限设置类型。
    - controller参数必须对应填写"new functionalButtonComponentManager.FunctionalButtonController().onPermissionSetting"。
    - 可使用自定义Modifier设置按钮样式，参考[示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbuttoncomponentmanager#section1251915241170)。
        
        其他参数请参考：[FunctionalButton（Button组件）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalbutton)。
        
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-button-selecting-point "地图选点Button")
# 省市区选择器Input

更新时间: 2025-12-16 16:36

## 场景介绍

从5.1.0(18)开始，支持省市区选择器Input功能。

省市区选择器Input功能可以帮助开发者调用对应FunctionalInput组件快速拉起选择地区页面，供用户选择地区信息。

运行示例代码后单击“所在地区”文本框，拉起选择地区页面，按照需求选择地址信息，选择完成后将所选地址回填至文本框中。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163639.62607399102049939492842744279097:50001231000000:2800:5E75DCFE40D7A1BB00C76B6620999B3D6D327E06B561419090EC1960911EA9C2.png "点击放大")

## 前提条件

参见[开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-config-agc)。

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    1. import { FunctionalInput, functionalInputComponentManager } from '@kit.ScenarioFusionKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    3. import { SymbolGlyphModifier, TextInputModifier } from '@kit.ArkUI';
    
2. 在容器中声明FunctionalInput，指定FunctionalInput的inputType，并设置对应的回调函数，代码如下：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   @State inputContent: string = '';
    
    5.   build() {
    6.     Column() {
    7.       Row() {
    8.         Text('所在地区').width(64)
    9.         // 声明FunctionalInput。
    10.         FunctionalInput({
    11.           params: {
    12.             // InputType.SELECT_DISTRICT表示输入类型为省/市/区选择器类型。
    13.             inputType: functionalInputComponentManager.InputType.SELECT_DISTRICT,
    14.             textInputValue: {
    15.               text: this.inputContent,
    16.               placeholder: '省、市、区、街道地址',
    17.             },
    18.             // 调整TextInput样式。
    19.             inputAttributeModifier: new TextInputModifier()
    20.               .fontColor($r('sys.color.ohos_id_color_badge_red'))
    21.               .onChange((value) => {
    22.                 if (value !== this.inputContent) {
    23.                   this.inputContent = value;
    24.                 }
    25.               }),
    26.             // 将图标设置在末尾。
    27.             icon: $r('sys.symbol.xmark'),
    28.             // 设置符号图标的事件和样式。
    29.             iconSymbolModifier: new SymbolGlyphModifier()
    30.               .onClick(() => {
    31.                 this.inputContent = '';
    32.               })
    33.               .fontSize(32),
    34.           },
    35.           // 当InputType为SELECT_DISTRICT时，回调必须为onSelectDistrict。
    36.           controller: new functionalInputComponentManager.FunctionalInputController().onSelectDistrict((err,
    37.             data: functionalInputComponentManager.DistrictSelectResult) => {
    38.             if (err) {
    39.               // 错误日志处理。
    40.               hilog.error(0x0000, "testTag", "error: %{public}d %{public}s", err.code, err.message);
    41.               return;
    42.             }
    43.             // 成功日志处理。
    44.             hilog.info(0x0000, "testTag", "succeeded in selecting district");
    45.             // 在输入组件中显示所选区域信息。
    46.             this.inputContent = data.inputContent;
    47.           })
    48.         })
    49.           .layoutWeight(1)
    50.       }.height('100%')
    51.     }.width('100%')
    52.   }
    53. }
    
    说明
    
    - inputType参数填写"functionalInputComponentManager.InputType.SELECT_DISTRICT"指定Input为省市区选择器类型。
    - controller参数必须对应填写"new functionalInputComponentManager.FunctionalInputController().onSelectDistrict"。
    - 可从返回结果中自行处理结果回填至组件中。
    - 组件支持显示两种类型的图标：symbol和image，"icon"设置为symbol资源时，请使用"[iconSymbolModifier](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalinputcomponentmanager#section19784874147)"进行图标事件、样式的设置；设置为image资源时，请使用"[iconImgModifier](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalinputcomponentmanager#section19784874147)"进行图标事件、样式的设置。
    - functionalInput支持[智能填充](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-intelligent-filling)，对应支持的[ContentType](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-intelligentfilling-appendix)为"ADDRESS_CITY_AND_STATE"。
    
    其他参数请参考：[FunctionalInput（Input组件）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-functionalinput)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-input "场景化Input")
# 通过API获取系统信息属性

更新时间: 2025-12-16 16:36

## 场景介绍

Scenario Fusion Kit提供获取系统信息属性API，调用该接口可以获取设备、网络状态、屏幕、语言、主题等系统信息属性。

## 约束和限制

场景化API支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持Wearable和TV设备。

## 接口说明

以下是获取系统信息属性的接口说明，更多接口及使用方法请参见[atomicService（融合场景化API）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice)。

|接口名|描述|
|:--|:--|
|[getSystemInfoSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section1465318121834)(properties?: Array<[SystemInfoType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section994220537517)>): [SystemInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section6926144111527)|获取系统信息属性的方法，支持获取设备、网络状态、屏幕、语言、主题等系统信息的请求对象，包含请求参数。<br><br>说明<br><br>getSystemInfoSync接口不支持获取windowWidth、windowHeight、statusBarHeight和screenSafeArea属性，如需获取可使用[getSystemInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section17779133174510)接口。|

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    1. import { atomicService } from '@kit.ScenarioFusionKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 传入属性参数，调用接口获取对应属性值，代码如下：
    
    1. let stateArray: Array<atomicService.SystemInfoType> =
    2.   ['brand', 'deviceModel', 'screenWidth', 'screenHeight', 'language', 'osFullName', 'fontSizeSetting',
    3.     'sdkApiVersion', 'bluetoothEnabled', 'wifiEnabled', 'locationEnabled', 'deviceOrientation', 'theme'];
    4. try {
    5.   let data = atomicService.getSystemInfoSync(stateArray);
    6.   hilog.info(0x0000, 'testTag', 'succeeded in getting system info');
    7.   let brand: string | undefined = data.brand;
    8.   let deviceModel: string | undefined = data.deviceModel;
    9.   let screenWidth: number | undefined = data.screenWidth;
    10.   let screenHeight: number | undefined = data.screenHeight;
    11.   let language: string | undefined = data.language;
    12.   let osFullName: string | undefined = data.osFullName;
    13.   let fontSizeSetting: number | undefined = data.fontSizeSetting;
    14.   let sdkApiVersion: number | undefined = data.sdkApiVersion;
    15.   let bluetoothEnabled: boolean | undefined = data.bluetoothEnabled;
    16.   let wifiEnabled: boolean | undefined = data.wifiEnabled;
    17.   let locationEnabled: boolean | undefined = data.locationEnabled;
    18.   let deviceOrientation: string | undefined = data.deviceOrientation;
    19.   let theme: ColorMode | undefined = data.theme;
    20. } catch (error) {
    21.   hilog.error(0x0000, 'testTag', 'failReason: %{public}d %{public}s', error.code, error.message);
    22. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-api-information-attribute "场景化API")
# 通过API异步获取系统信息属性

更新时间: 2025-12-16 16:36

## 场景介绍

Scenario Fusion Kit提供获取系统信息属性API，调用该接口可以获取设备、网络状态、屏幕、语言、主题等系统信息属性。

## 约束和限制

场景化API支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持Wearable和TV设备。

## 接口说明

以下是使用Promise异步回调获取系统信息属性的接口说明，更多接口及使用方法请参见[atomicService（融合场景化API）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice)。

|接口名|描述|
|:--|:--|
|[getSystemInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section17779133174510)(properties?: Array<[SystemInfoType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section994220537517)>): Promise<[SystemInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section6926144111527)>|获取系统信息属性的方法，支持获取设备、网络状态、屏幕、语言、主题等系统信息的请求对象，包含请求参数。|

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    1. import { atomicService } from '@kit.ScenarioFusionKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { window } from '@kit.ArkUI';
    
2. 传入属性参数，调用接口获取对应属性值，代码如下：
    
    1. let stateArray: Array<atomicService.SystemInfoType> =
    2.   ['brand', 'deviceModel', 'screenWidth', 'screenHeight', 'statusBarHeight', 'screenSafeArea', 'language', 'osFullName',
    3.     'fontSizeSetting', 'sdkApiVersion', 'bluetoothEnabled', 'wifiEnabled', 'locationEnabled', 'deviceOrientation',
    4.     'theme', 'windowWidth', 'windowHeight'];
    5. try {
    6.   atomicService.getSystemInfo(stateArray).then((data: atomicService.SystemInfo) => {
    7.     hilog.info(0x0000, 'testTag', 'succeeded in getting system info asynchronously');
    8.     let brand: string | undefined = data.brand;
    9.     let deviceModel: string | undefined = data.deviceModel;
    10.     let screenWidth: number | undefined = data.screenWidth;
    11.     let screenHeight: number | undefined = data.screenHeight;
    12.     let statusBarHeight: number | undefined = data.statusBarHeight;
    13.     let screenSafeArea: window.AvoidArea | undefined = data.screenSafeArea;
    14.     let language: string | undefined = data.language;
    15.     let osFullName: string | undefined = data.osFullName;
    16.     let fontSizeSetting: number | undefined = data.fontSizeSetting;
    17.     let sdkApiVersion: number | undefined = data.sdkApiVersion;
    18.     let bluetoothEnabled: boolean | undefined = data.bluetoothEnabled;
    19.     let wifiEnabled: boolean | undefined = data.wifiEnabled;
    20.     let locationEnabled: boolean | undefined = data.locationEnabled;
    21.     let deviceOrientation: string | undefined = data.deviceOrientation;
    22.     let theme: ColorMode | undefined = data.theme;
    23.     let windowWidth: number | undefined = data.windowWidth;
    24.     let windowHeight: number | undefined = data.windowHeight;
    25.   }).catch((error: BusinessError) => {
    26.     hilog.error(0x0000, 'testTag', 'Promise error: %{public}d %{public}s', error.code, error.message);
    27.   })
    28. } catch (error) {
    29.   hilog.error(0x0000, 'testTag', 'failReason: %{public}d %{public}s', error.code, error.message);
    30. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-api-system-info "通过API获取系统信息属性")
# 通过API获取系统设置属性

更新时间: 2025-12-16 16:37

## 场景介绍

Scenario Fusion Kit提供获取系统设置属性API，调用该接口可以获取蓝牙、定位、Wi-Fi开关信息，以及设备方向信息等系统信息属性。

## 约束和限制

场景化API支持Phone、Tablet和2in1设备，并且从5.1.0(18)版本开始，新增支持Wearable和TV设备。

## 接口说明

以下是获取系统设置属性的接口说明，更多接口及使用方法请参见[atomicService（融合场景化API）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice)。

|接口名|描述|
|:--|:--|
|[getSystemSetting](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section171285335615)(properties?: Array<[SystemSettingType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section11423195912475)>): [SystemSettingInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section53111326141919)|获取系统设置属性的方法，支持获取蓝牙、定位、Wi-Fi开关信息，以及设备方向信息的请求对象。|

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    import { atomicService } from '@kit.ScenarioFusionKit';
    import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 传入属性参数，调用接口获取对应属性值，代码如下：
    
    let stateArray: Array<atomicService.SystemSettingType> =
      ['bluetoothEnabled', 'locationEnabled', 'deviceOrientation', 'wifiEnabled'];
    try {
      let data = atomicService.getSystemSetting(stateArray);
      hilog.info(0x0000, 'testTag', 'succeeded in getting system setting info');
      let bluetoothEnabled: boolean | undefined = data.bluetoothEnabled;
      let locationEnabled: boolean | undefined = data.locationEnabled;
      let deviceOrientation: string | undefined = data.deviceOrientation;
      let wifiEnabled: boolean | undefined = data.wifiEnabled;
    } catch (error) {
      hilog.error(0x0001, 'testTag', 'failReason: %{public}d %{public}s', error.code, error.message);
    }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-api-system-info "通过API获取系统信息属性")
# 通过API展示关注组件

更新时间: 2025-12-16 16:37

## 场景介绍

从6.0.1(21)版本开始，支持关注组件API功能。

Scenario Fusion Kit提供服务号关注组件功能，调用该接口可以在业务应用/元服务页面展示服务号关注组件，用户点击关注按钮可关注上对应服务号。

- 用户关注服务号成功，按钮会变为已关注并置灰，在1.5秒后关注组件会自动消失。
- 用户关注服务号失败，则会出现错误提示。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163729.74524733381844294261098867646953:50001231000000:2800:294BCC2BF991735D3C55289B03633EB8916ED245C7B4B71D0C78BC5D16976B2A.png)![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163729.68954391946856981943233833107181:50001231000000:2800:DA77B438E43D4B46AC3C56C34959B979F6637638B395D4C1DF17868AA53F3072.png)
    

## 前提条件

在[华为开发者联盟服务号管理首页](https://developer.huawei.com/consumer/cn/console/service/FastService/service/1063)，申请华为服务号，并获取服务号id。

1. 使用企业开发者账号登录，并完成企业认证。
2. 申请服务号并完成认证。
3. 元服务/应用须与服务号处于同一个开发者账号下。

## 接口说明

以下是关注组件的接口说明，更多接口及使用方法请参见[atomicService（融合场景化API）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice)。

|接口名|描述|
|:--|:--|
|[showFollowComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section13456131695414)(ctx: [UIContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-api#uicontext), params: [FollowComponentParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section1881114501476), callback: [FollowComponentCallback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-atomicservice#section137361343174413)): Promise<void>|调用该方法展示关注组件。|

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    **import { atomicService } from '@kit.ScenarioFusionKit';**
    **import { hilog } from '@kit.PerformanceAnalysisKit';**
    **import { BusinessError } from '@kit.BasicServicesKit';**
    
2. 在需要添加关注组件的页面，调用接口展示关注组件，示例代码如下：
    
    @Entry
    @Component
    struct Index {
      aboutToAppear(): void {
        // 一键关注组件。
        // pubId: 服务号id，此处以官方小助手服务号id为例。
        const pubId: string = '0cca1c645526449fb89d4a83e3bc25df';
        // channelId：渠道id，长度限制32，只能是数字或字母组成; offset：设置关注组件的位置坐标。
        const params: atomicService.FollowComponentParams =
          { pubId: pubId, channelId: '', offset: { x: 0, y: 300 } };
        // 点击关注按钮的关注结果回调。
        const callbacks: atomicService.FollowComponentCallback = {
          onFollowComplete: (err, result) => {
            if (err) {
              // 错误日志处理。
              hilog.error(0x0000, "testTag", "error: %{public}d %{public}s", err.code, err.message);
              return;
            }
            hilog.info(0x0000, "testTag", "follow result: %{public}d", result.code);
            if (result.code === atomicService.FollowResult.SUCCESS) {
              hilog.info(0x0000, "testTag", "follow succeeded handle");
            } else {
              hilog.info(0x0000, "testTag", "follow failed handle");
            }
          }
        }
        // 展示关注组件。
        atomicService.showFollowComponent(this.getUIContext(), params, callbacks).catch((error: BusinessError<void>) => {
          hilog.error(0x0000, 'testTag', 'showFollowComponent failReason: %{public}d %{public}s', error.code,
            error.message);
        })
      }
    
      build() {
      }
    }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-api-asyn-system-info "通过API异步获取系统信息属性")
# 文件路径转换API

更新时间: 2025-12-16 16:36

## 场景介绍

Scenario Fusion Kit提供文件路径转换的API，在HarmonyOS 4及以下到HarmonyOS 5及以上的升级场景和克隆场景，调用该接口可以将源文件路径转换为目标文件路径。

## 接口说明

以下是获取转换文件uri信息的接口说明，更多接口及使用方法请参见[fileUriService（文件路径转换API）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-fileuriresult)。

|接口名|描述|
|:--|:--|
|[convertFileUris](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-fileuriresult#section1272664195920)(sourceFileUris: Array<string>): Promise<Array<[FileUriResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scenario-fusion-fileuriresult#section443872764410)>>|获取转换文件uri信息的请求对象。|

## 开发步骤

1. 导入Scenario Fusion Kit模块以及相关公共模块。
    
    1. import { fileUriService } from '@kit.ScenarioFusionKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 传入待转换的文件路径参数列表，调用接口获取转换后的文件路径列表，代码如下：
    
    1. try {
    2.   // '/storage/emulated/0/Pictures/test.gif'表示test.gif的文件路径。
    3.   let sourceFileUris: Array<string> =
    4.     ['100','content://media/external/files/10', '/storage/emulated/0/Pictures/test.gif',
    5.       '/storage/emulated/0/media/com.test/test.mp4'];
    6.   fileUriService.convertFileUris(sourceFileUris).then(result => {
    7.     hilog.info(0x0000, 'testTag', 'succeeded in converting file uris');
    8.     result.forEach(data => {
    9.       switch (data.targetType) {
    10.         case fileUriService.TargetType.UNKNOWN:
    11.           hilog.info(0x0000, 'testTag', 'input uri or path is not exist');
    12.           break;
    13.         case fileUriService.TargetType.MEDIA:
    14.           hilog.info(0x0000, 'testTag', 'converted media uri: %{public}s', data.targetUri);
    15.           break;
    16.         case fileUriService.TargetType.FILE:
    17.           // 如果输入路径存在，结果中的targetUri将是转换后的URI。
    18.           // 否则，targetUri 将与输入路径相同，targetType 将为 UNKNOWN。
    19.           hilog.info(0x0000, 'testTag', 'converted file path: %{public}s', data.targetUri);
    20.           break;
    21.       }
    22.     })
    23.   }).catch((error: BusinessError) => {
    24.     hilog.error(0x0000, 'testTag', 'Promise error: %{public}d %{public}s', error.code, error.message);
    25.   });
    26. } catch (error) {
    27.   hilog.error(0x0000, 'testTag', 'failReason: %{public}d %{public}s', error.code, error.message);
    28. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-api-followcomponent "通过API展示关注组件")
