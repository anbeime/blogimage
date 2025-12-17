# IME Kit简介

更新时间: 2025-12-16 16:38

IME Kit 负责建立编辑框所在应用与输入法应用之间的通信通道，确保两者可以共同协作提供文本输入功能，也为系统应用提供管理输入法应用的能力。

## Kit使用场景

IME Kit提供输入法框架和输入法服务两类API。用于实现输入法应用，也可以用于实现自绘编辑框以及实现对输入法应用的控制。

## 框架原理

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163818.07955323548606164620983400530470:50001231000000:2800:B2B72EA42480851A812CAC56B8797645CEC997F87FAA504E0C3283B519F2CEB4.png)

## 功能特点

- 输入法应用：
    
    支持创建固定态、悬浮态、状态栏三种类型的Panel，可支持开发一个输入法应用同时部署在手机、平板等多设备中。
    
- 自定义编辑框：
    
    支持开发者自定义编辑框，实现绑定输入法应用，并实现输入法应用的文字输入、删除、选中、光标移动等操作。
    

## 能力范围

- 提供输入法服务相关API，用于输入法应用，包括：创建软键盘窗口、插入/删除字符、选中文本、监听物理键盘按键事件等。
    
- 提供输入法框架相关API，可用于自绘编辑框，包括绑定输入法，实现输入、删除、选中、光标移动等。
    
- 提供系统应用管理输入法应用能力，实现对输入法应用的控制，包括显示/隐藏输入法软键盘、切换输入法、获取所有输入法列表。
    

## 与相关Kit的关系

ArkUI: IME Kit在输入法软键盘和自绘编辑框时使用ArkUI提供的部分组件、事件、动效、状态管理等能力，例如Text、Button组件，onClick点击事件。

## 约束限制

针对切换输入法应用的系统API，需要申请系统权限，部分API仅支持当前输入法应用调用。

## IME Kit API参考

- [inputMethodEngine](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethodengine)
    
- [inputMethod](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod)
    
- [InputMethodExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod-extension-ability)
    
- [InputMethodExtensionContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod-extension-context)
    
- [inputMethodList](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethodlist)
    
- [InputMethodSubtype](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod-subtype)
    
- [inputMethod.Panel](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod-panel)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ime-kit "IME Kit（输入法开发服务）")
# 实现一个输入法应用

更新时间: 2025-12-16 16:38

[InputMethodExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod-extension-ability)提供了onCreate()和onDestroy()生命周期回调，根据需要重写对应的回调方法。InputMethodExtensionAbility的生命周期如下：

- **onCreate()**
    
    服务被首次创建时触发该回调，开发者可以在此进行一些初始化的操作，例如注册公共事件监听等。
    
    说明
    
    如果服务已创建，再次启动该InputMethodExtensionAbility不会触发onCreate()回调。
    
- **onDestroy()**
    
    当不再使用服务且准备将该实例销毁时，触发该回调。开发者可以在该回调中清理资源，如注销监听等。
    

## 开发步骤

开发者在实现一个输入法应用时，需要在DevEco Studio工程中新建一个InputMethodExtensionAbility，具体步骤如下：

1. 在工程Module对应的ets目录下，右键选择“New > Directory”，新建一个目录，并命名为InputMethodExtensionAbility。
    
2. 在InputMethodExtensionAbility目录下，右键选择“New > File”，新建四个文件，分别为KeyboardController.ts、InputMethodService.ts、Index.ets以及KeyboardKeyData.ts。目录如下：
    
    1. /src/main/
    2. ├── ets/InputMethodExtensionAbility
    3. │       └──model/KeyboardController.ts            # 显示键盘
    4. │       └──InputMethodService.ts                # 自定义类继承InputMethodExtensionAbility并加上需要的生命周期回调
    5. │       └──pages
    6. │         └── Index.ets                        # 绘制键盘，添加输入删除功能
    7. │         └── KeyboardKeyData.ts                # 键盘属性定义
    8. ├── resources/base/profile/main_pages.json
    

## 文件介绍

1. InputMethodService.ts文件。
    
    在InputMethodService.ts文件中，增加导入InputMethodExtensionAbility的依赖包，自定义类继承InputMethodExtensionAbility并加上需要的生命周期回调。
    
    1. import { Want } from '@kit.AbilityKit';
    2. import keyboardController from './model/KeyboardController';
    3. import { InputMethodExtensionAbility } from '@kit.IMEKit';
    
    4. export default class InputDemoService extends InputMethodExtensionAbility {
    
    5.   onCreate(want: Want): void {
    6.     keyboardController.onCreate(this.context); // 初始化窗口并注册对输入法框架的事件监听
    7.   }
    
    8.   onDestroy(): void {
    9.     console.info("onDestroy.");
    10.     keyboardController.onDestroy(); // 销毁窗口并去注册事件监听
    11.   }
    12. }
    
2. KeyboardController.ts文件。KeyboardController中除创建输入法窗口，设置输入法事件监听，实现文本插入、删除之外，还可以获取[输入法键盘与系统面板的偏移区域](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethodengine#getsystempanelcurrentinsets21)，输入法系统面板在不同设备上存在差异，当设备有系统面板时，输入法软键盘相对系统面板的偏移区域如图所示：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163819.72260112188146875709379858845876:50001231000000:2800:64C69CDF01D22A529F33700717A4CA93F59C254C58D5C9A2374732CF315B951D.png)
    
    1. import { display } from '@kit.ArkUI';
    2. import { inputMethodEngine, InputMethodExtensionContext } from '@kit.IMEKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. // 调用输入法框架的getInputMethodAbility方法获取实例，并由此实例调用输入法框架功能接口
    5. const inputMethodAbility: inputMethodEngine.InputMethodAbility = inputMethodEngine.getInputMethodAbility();
    
    6. export class KeyboardController {
    7.   private mContext: InputMethodExtensionContext | undefined = undefined; // 保存InputMethodExtensionAbility中的context属性
    8.   private panel: inputMethodEngine.Panel | undefined = undefined;
    9.   private textInputClient: inputMethodEngine.InputClient | undefined = undefined;
    10.   private keyboardController: inputMethodEngine.KeyboardController | undefined = undefined;
    
    11.   constructor() {
    12.   }
    
    13.   public onCreate(context: InputMethodExtensionContext): void
    14.   {
    15.     this.mContext = context;
    16.     this.initWindow(); // 初始化窗口
    17.     this.registerListener(); // 注册对输入法框架的事件监听
    18.   }
    
    19.   public onDestroy(): void // 应用生命周期销毁
    20.   {
    21.     this.unRegisterListener(); // 去注册事件监听
    22.     if(this.panel) { // 销毁窗口
    23.       inputMethodAbility.destroyPanel(this.panel);
    24.     }
    25.     if(this.mContext) {
    26.       this.mContext.destroy();
    27.     }
    28.   }
    
    29.   public insertText(text: string): void {
    30.     if(this.textInputClient) {
    31.       this.textInputClient.insertText(text);
    32.     }
    33.   }
    
    34.   public deleteForward(length: number): void {
    35.     if(this.textInputClient) {
    36.       this.textInputClient.deleteForward(length);
    37.     }
    38.   }
    
    39.   private initWindow(): void // 初始化窗口
    40.   {
    41.     if(this.mContext === undefined) {
    42.       return;
    43.     }
    44.     let dis = display.getDefaultDisplaySync();
    45.     let dWidth = dis.width;
    46.     let dHeight = dis.height;
    47.     let keyHeightRate = 0.47;
    48.     let keyHeight = dHeight * keyHeightRate;
    49.     let nonBarPosition = dHeight - keyHeight;
    50.     let panelInfo: inputMethodEngine.PanelInfo = {
    51.       type: inputMethodEngine.PanelType.SOFT_KEYBOARD,
    52.       flag: inputMethodEngine.PanelFlag.FLG_FIXED
    53.     };
    54.     inputMethodAbility.createPanel(this.mContext, panelInfo).then(async (inputPanel: inputMethodEngine.Panel) => {
    55.       this.panel = inputPanel;
    56.       if (this.panel) {
    57.         await this.panel.resize(dWidth, keyHeight);
    58.         await this.panel.moveTo(0, nonBarPosition);
    59.         await this.panel.setUiContent('InputMethodExtensionAbility/pages/Index');
    60.         // 获取输入法键盘与系统面板偏移区域大小，实际开发中可以根据实际情况判断是否需要实现
    61.         let defaultDisplay = display.getDefaultDisplaySync();
    62.         if (defaultDisplay !== undefined) {
    63.           this.panel.getSystemPanelCurrentInsets(defaultDisplay.id)
    64.             .then((insets: inputMethodEngine.SystemPanelInsets) => {
    65.               console.info(`getSystemPanelCurrentInsets success, insets is { left: ${insets.left}, right: ${insets.right}, bottom: ${insets.bottom} }`);
    66.             })
    67.             .catch((error: BusinessError) => {
    68.               console.error(`getSystemPanelCurrentInsets failed, code: ${error.code}, message: ${error.message}`);
    69.             })
    70.         }
    71.       }
    72.     }).catch((err: BusinessError) => {
    73.       console.error(`Failed to createPanel, code: ${err.code}, message: ${err.message}`);
    74.     });
    75.   }
    
    76.   private registerListener(): void
    77.   {
    78.     this.registerInputListener(); // 注册对输入法框架服务的监听
    79.     // 注册隐藏键盘事件监听等
    80.   }
    
    81.   private registerInputListener(): void {
    82.     // 注册开始输入的事件监听
    83.     inputMethodAbility.on('inputStart', (kbController, textInputClient) => {
    84.       this.textInputClient = textInputClient; // 此为输入法客户端实例，由此调用输入法框架提供给输入法应用的功能接口
    85.       this.keyboardController = kbController;
    86.     })
    87.     inputMethodAbility.on('inputStop', this.inputStopCallback);
    88.   }
    
    89.   private inputStopCallback(): void {
    90.     this.onDestroy(); // 销毁KeyboardController
    91.   }
    
    92.   private unRegisterListener(): void {
    93.     inputMethodAbility.off('inputStart');
    94.     inputMethodAbility.off('inputStop', this.inputStopCallback);
    95.   }
    96. }
    
    97. const keyboardController = new KeyboardController();
    
    98. export default keyboardController;
    
3. KeyboardKeyData.ts文件。
    
    定义软键盘的按键显示内容。
    
    1. export interface sourceListType {
    2.   content: string,
    3. }
    
    4. export const numberSourceListData: sourceListType[] = [
    5.   {
    6.     content: '1'
    7.   },
    8.   {
    9.     content: '2'
    10.   },
    11.   {
    12.     content: '3'
    13.   },
    14.   {
    15.     content: '4'
    16.   },
    17.   {
    18.     content: '5'
    19.   },
    20.   {
    21.     content: '6'
    22.   },
    23.   {
    24.     content: '7'
    25.   },
    26.   {
    27.     content: '8'
    28.   },
    29.   {
    30.     content: '9'
    31.   },
    32.   {
    33.     content: '0'
    34.   }
    35. ]
    
4. Index.ets文件。
    
    主要描绘了具体按键功能。如按下数字键，就会将数字内容在输入框中打印出来，按下删除键，就会将内容删除。
    
    1. import { numberSourceListData, sourceListType } from './KeyboardKeyData';
    2. import keyboardController from '../model/KeyboardController';
    
    3. @Component
    4. struct keyItem {
    5.   private keyValue: sourceListType = numberSourceListData[0];
    6.   @State keyBgc: string = "#fff"
    7.   @State keyFontColor: string = "#000"
    
    8.   build() {
    9.     Column() {
    10.       Flex({ direction: FlexDirection.Column,
    11.         alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
    12.         Text(this.keyValue.content).fontSize(20).fontColor(this.keyFontColor)
    13.       }
    14.     }
    15.     .backgroundColor(this.keyBgc)
    16.     .borderRadius(6)
    17.     .width("8%")
    18.     .height("65%")
    19.     .onClick(() => {
    20.       keyboardController.insertText(this.keyValue.content);
    21.     })
    22.   }
    23. }
    
    24. // 删除组件
    25. @Component
    26. export struct deleteItem {
    27.   @State keyBgc: string = "#fff"
    28.   @State keyFontColor: string = "#000"
    
    29.   build() {
    30.     Column() {
    31.       Flex({ direction: FlexDirection.Column,
    32.         alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
    33.         Text("删除").fontSize(20).fontColor(this.keyFontColor)
    34.       }
    35.     }
    36.     .backgroundColor(this.keyBgc)
    37.     .width("13%")
    38.     .borderRadius(6)
    39.     .onClick(() => {
    40.       keyboardController.deleteForward(1);
    41.     })
    42.   }
    43. }
    
    44. // 数字键盘
    45. @Component
    46. struct numberMenu {
    47.   private numberList: sourceListType[] = numberSourceListData;
    
    48.   build() {
    49.     Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.SpaceEvenly }) {
    50.       Flex({ justifyContent: FlexAlign.SpaceBetween }) {
    51.         ForEach(this.numberList, (item: sourceListType) => { // 数字键盘第一行
    52.           keyItem({ keyValue: item })
    53.         }, (item: sourceListType) => item.content);
    54.       }
    55.       .padding({ top: "2%" })
    56.       .width("96%")
    57.       .height("25%")
    
    58.       Flex({ justifyContent: FlexAlign.SpaceBetween }) {
    59.         deleteItem()
    60.       }
    61.       .width("96%")
    62.       .height("25%")
    63.     }
    64.   }
    65. }
    
    66. @Entry
    67. @Component
    68. struct Index {
    69.   private numberList: sourceListType[] = numberSourceListData
    
    70.   build() {
    71.     Stack() {
    72.       Flex({
    73.         direction: FlexDirection.Column,
    74.         alignItems: ItemAlign.Center,
    75.         justifyContent: FlexAlign.End
    76.       }) {
    77.             Flex({
    78.               direction: FlexDirection.Column,
    79.               alignItems: ItemAlign.Center,
    80.               justifyContent: FlexAlign.SpaceBetween
    81.             }) {
    82.               numberMenu({
    83.                 numberList: this.numberList
    84.               })
    85.             }
    86.             .align(Alignment.End)
    87.             .width("100%")
    88.             .height("75%")
    89.           }
    90.       .height("100%").align(Alignment.End).backgroundColor("#cdd0d7")
    91.     }
    92.     .position({ x: 0, y: 0 }).zIndex(99999)
    93.   }
    94. }
    
5. main_pages.json文件。对应ets/InputMethodExtensionAbility/pages/路径下键盘的绘制页面。
    
    1. {
    2.   "src": [
    3.     "InputMethodExtensionAbility/pages/Index"
    4.   ]
    5. }
    
6. 在工程Module对应的[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中注册InputMethodExtensionAbility，type标签需要设置为“inputMethod”，srcEntry标签表示当前InputMethodExtensionAbility组件所对应的代码路径。
    
    1. {
    2.   "module": {
    3.     ...
    4.     "extensionAbilities": [
    5.       {
    6.         "description": "inputMethod",
    7.         "name": "InputMethodExtensionAbility",
    8.         "icon": "$media:app_icon",
    9.         "srcEntry": "./ets/InputMethodExtensionAbility/InputMethodService.ts",
    10.         "type": "inputMethod",
    11.         "exported": true
    12.       }
    13.     ]
    14.   }
    15. }
    

## 约束与限制

为了降低InputMethodExtensionAbility能力被三方应用滥用的风险，现通过基础访问模式的功能约束对输入法应用进行安全管控。

说明

严格遵从基础访问模式的功能约束。在此模式下，开发者应仅提供基础打字功能，不应提供任何形式与网络交互相关的功能。系统会逐步增加基础访问模式的安全管控能力，包括但不限于：以独立进程和沙箱的方式运行Extension进程；禁止Extension进程创建子进程；进程间通信与网络访问等。因此未遵从此约定可能会导致功能异常。

## 示例效果图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163819.33856660498978436801378837719405:50001231000000:2800:FCAB959072880DBE3ED0B3E205D1C829907A5D4BC2B093512F9C513A9A7A8580.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ime-kit-intro "IME Kit简介")
# 在自绘编辑框中使用输入法

更新时间: 2025-12-16 16:38

在输入法框架中，可以通过[getController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#inputmethodgetcontroller9)方法获取到[InputMethodController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#inputmethodcontroller)实例来绑定输入法并监听输入法应用的各种操作，比如插入、删除、选择、光标移动等。这样就可以在自绘编辑框中使用输入法，并实现更加灵活和自由的编辑操作。

## 开发步骤

1. 开发者在自绘编辑框中使用输入法时，首先需要在DevEco Studio工程中新建一个ets文件，命名为自定义控件的名称，本示例中命名为CustomInput，在文件中定义一个自定义控件，并从@kit.IMEKit中导入inputMethod。
    
    1. import { inputMethod } from '@kit.IMEKit';
    
    2. @Component
    3. export struct CustomInput {
    4.   build() {
    5.   }
    6. }
    
2. 在控件中，使用Text组件作为自绘编辑框的文本显示组件，使用状态变量inputText作为Text组件要显示的内容。
    
    1. import { inputMethod } from '@kit.IMEKit';
    
    2. @Component
    3. export struct CustomInput {
    4.   @State inputText: string = ''; // inputText作为Text组件要显示的内容。
    
    5.   build() {
    6.     Text(this.inputText) // Text组件作为自绘编辑框的文本显示组件。
    7.       .fontSize(16)
    8.       .width('100%')
    9.       .lineHeight(40)
    10.       .id('customInput')
    11.       .height(45)
    12.       .border({ color: '#554455', radius: 30, width: 1 })
    13.       .maxLines(1)
    14.   }
    15. }
    
3. 在控件中获取inputMethodController实例，先在文本点击时调用controller实例的attach方法绑定和拉起软键盘，再注册监听输入法插入文本、删除等方法。本示例仅展示插入、删除。
    
    1. import { inputMethod } from '@kit.IMEKit';
    
    2. @Component
    3. export struct CustomInput {
    4.   @State inputText: string = ''; // inputText作为Text组件要显示的内容。
    5.   private isAttach: boolean = false;
    6.   private inputController: inputMethod.InputMethodController = inputMethod.getController();
    
    7.   build() {
    8.     Text(this.inputText) // Text组件作为自绘编辑框的文本显示组件。
    9.       .fontSize(16)
    10.       .width('100%')
    11.       .lineHeight(40)
    12.       .id('customInput')
    13.       .onBlur(() => {
    14.         this.off();
    15.       })
    16.       .height(45)
    17.       .border({ color: '#554455', radius: 30, width: 1 })
    18.       .maxLines(1)
    19.       .onClick(() => {
    20.         this.attachAndListener(); // 点击控件
    21.       })
    22.   }
    
    23.   async attachAndListener() { // 绑定和设置监听
    24.     focusControl.requestFocus('CustomInput');
    25.     try {
    26.      await this.inputController.attach(true, {
    27.       inputAttribute: {
    28.         textInputType: inputMethod.TextInputType.TEXT,
    29.         enterKeyType: inputMethod.EnterKeyType.SEARCH
    30.       }
    31.     });
    32.     } catch(err) {
    33.       console.error(`Failed to attach: code:${err.code}, message:${err.message}`);
    34.     }
    35.     if (!this.isAttach) {
    36.       this.inputController.on('insertText', (text) => {
    37.         this.inputText += text;
    38.       })
    39.       this.inputController.on('deleteLeft', (length) => {
    40.         this.inputText = this.inputText.substring(0, this.inputText.length - length);
    41.       })
    42.       this.isAttach = true;
    43.     }
    44.   }
    
    45.   off() {
    46.     this.isAttach = false;
    47.     this.inputController.off('insertText');
    48.     this.inputController.off('deleteLeft');
    49.   }
    50. }
    
4. 在应用界面布局中引入该控件即可，此处假设使用界面为Index.ets和控件CustomInput.ets在同一目录下。
    
    1. import { CustomInput } from './CustomInput'; // 导入控件
    
    2. @Entry
    3. @Component
    4. struct Index {
    
    5.   build() {
    6.     Column() {
    7.       CustomInput() // 使用控件
    8.     }
    9.   }
    10. }
    
    **示例效果图**

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163820.82862336769506656449812958791500:50001231000000:2800:2D2B160AD284634FDBD38CD38C99F25D52996C1E65DE53FD45C3396356990B27.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/inputmethod-application-guide "实现一个输入法应用")
# 切换输入法应用

更新时间: 2025-12-16 16:38

输入法框架服务提供了切换输入法应用的API，支持切换输入法、切换输入法和子类型、切换当前输入法的子类型。

说明

1. 以下接口的使用仅允许在当前输入法应用中调用。
    
2. 本示例假设已经在输入法应用中执行，如何实现一个输入法应用，请参考[实现一个输入法应用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/inputmethod-application-guide)开发指导。
    

## 切换当前输入法子类型

1. 在已完成一个输入法应用的基础上，当输入法应用是当前输入法时，在输入法应用中使用[switchCurrentInputMethodSubtype](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#inputmethodswitchcurrentinputmethodsubtype9)接口，传入当前输入法的子类型[InputMethodSubtype](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod-subtype#inputmethodsubtype)作为参数即可切换当前输入法子类型。
    
    1. import { InputMethodSubtype, inputMethod } from '@kit.IMEKit';
    
    2. export class KeyboardController {
    3.   async switchCurrentInputMethodSubtype() {
    4.     try {
    5.       let subTypes: Array<InputMethodSubtype> =
    6.         await inputMethod.getSetting().listCurrentInputMethodSubtype(); // 获取当前输入法的所有子类型
    7.       let currentSubType: InputMethodSubtype = inputMethod.getCurrentInputMethodSubtype(); // 获取当前输入法当前的子类型
    8.       if (subTypes.length === 0) {
    9.         return;
    10.       }
    11.       for (let i = 0; i < subTypes.length; i++) {
    12.         if (subTypes[i].id != currentSubType.id) { // 判断不是当前的子类型时切换，实际开发中可以根据需要填固定子类型
    13.           await inputMethod.switchCurrentInputMethodSubtype(subTypes[i]);
    14.           return;
    15.         }
    16.       }
    17.     } catch (err) {
    18.       let error: BusinessError = err as BusinessError;
    19.       console.error(`Failed to switchCurrentInputMethodSubtype, code: ${err.code}, message: ${err.message}`);
    20.     }
    21.   }
    22. }
    
2. 输入法应用中注册子类型变化事件，根据不同子类型加载不同的输入界面。
    
    1. import { InputMethodSubtype, inputMethodEngine, inputMethod } from '@kit.IMEKit';
    
    2. export class KeyboardController {
    3.   async switchCurrentInputMethodSubtype() {
    4.     let panel: inputMethodEngine.Panel; // 此处panel需要在createPanel接口创建panel实例后使用
    5.     let inputMethodAbility: inputMethodEngine.InputMethodAbility = inputMethodEngine.getInputMethodAbility();
    6.     // 设置监听子类型事件，改变输入法应用界面
    7.     inputMethodAbility.on('setSubtype', (inputMethodSubtype: InputMethodSubtype) => {
    8.       if(inputMethodSubtype.id == 'InputMethodExtAbility') {
    9.         panel.setUiContent('pages/Index'); // 假设在输入法应用中此时Panel已经在onCreate流程中创建
    10.       }
    11.       if(inputMethodSubtype.id == 'InputMethodExtAbility1') {
    12.         panel.setUiContent('pages/Index1'); // 假设在输入法应用中此时Panel已经在onCreate流程中创建
    13.       }
    14.     });
    15.   }
    16. }
    

## 切换输入法应用

在已完成一个输入法应用的基础上，当输入法应用是当前输入法时，在输入法应用中使用[switchInputMethod](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#inputmethodswitchinputmethod9)接口，传入目标输入法的[InputMethodProperty](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#inputmethodproperty8)信息，即可切换输入法到目标输入法。

1. import { inputMethod } from '@kit.IMEKit';

2. export class KeyboardController {
3.   async switchInputMethod(){
4.     try {
5.       let inputMethods: Array<inputMethod.InputMethodProperty> =
6.         await inputMethod.getSetting().getInputMethods(true); // 获取已使能的输入法列表
7.       let currentInputMethod: inputMethod.InputMethodProperty = inputMethod.getCurrentInputMethod(); // 获取当前输入法
8.       for (let i = 0; i < inputMethods.length; i++) {
9.         if (inputMethods[i].name != currentInputMethod.name) { // 判断不是当前输入法时，切换到该输入法，实际开发中可以切换到固定输入法
10.           await inputMethod.switchInputMethod(inputMethods[i]);
11.           return;
12.         }
13.       }
14.     } catch (err) {
15.       let error: BusinessError = err as BusinessError;
16.       console.error(`Failed to switchInputMethod, code: ${err.code}, message: ${err.message}`);
17.     }
18.   }
19. }

## 切换输入法应用和子类型

在已完成一个输入法应用的基础上，当输入法应用是当前输入法时，在输入法应用中使用[switchCurrentInputMethodAndSubtype](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#inputmethodswitchcurrentinputmethodandsubtype9)接口，传入目标输入法的[InputMethodProperty](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#inputmethodproperty8)，目标输入法的子类型[InputMethodSubtype](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod-subtype#inputmethodsubtype)信息，即可切换输入法到目标输入法的指定子类型。

1. import { inputMethod } from '@kit.IMEKit';

2. export class KeyboardController {
3.   async switchInputMethodAndSubtype() {
4.     try {
5.       let inputMethods: Array<inputMethod.InputMethodProperty> =
6.         await inputMethod.getSetting().getInputMethods(true); // 获取已使能的输入法列表
7.       let currentInputMethod: inputMethod.InputMethodProperty = inputMethod.getCurrentInputMethod(); // 获取当前输入法
8.       for (let i = 0; i < inputMethods.length; i++) {
9.         if (inputMethods[i].name != currentInputMethod.name) { // 判断不是当前输入法时，切换到该输入法，实际开发中可以切换到固定输入法
10.           let subTypes = await inputMethod.getSetting().listInputMethodSubtype(inputMethods[i]); // 获取目标输入法的子类型
11.           if (subTypes.length > 0) {
12.             await inputMethod.switchCurrentInputMethodAndSubtype(inputMethods[i], subTypes[0]); // 本示例默认切换到获取的第一个子类型
13.           }
14.           return;
15.         }
16.       }
17.     } catch (err) {
18.       let error: BusinessError = err as BusinessError;
19.       console.error(`Failed to switchCurrentInputMethodAndSubtype, code: ${err.code}, message: ${err.message}`);
20.     }
21.   }
22. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/use-inputmethod-in-custom-edit-box "在自绘编辑框中使用输入法")
# 输入法子类型开发指南

更新时间: 2025-12-16 16:38

输入法子类型允许输入法展现不同的输入模式或语言，用户可以根据需要在不同模式和语言中切换。如输入法的中文键盘、英文键盘等，都属于输入法的子类型。

## 输入法子类型的配置与实现

1. 输入法应用开发者只需要注册实现一个InputMethodExtensionAbility，所有的输入法子类型共用该InputMethodExtensionAbility，在[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中添加metadata，name为ohos_extension.input_method，用于配置所有子类型的资源信息。
    
    1. {
    2.   "module": {
    3.     // ...
    4.     "extensionAbilities": [
    5.       {
    6.         "description": "InputMethodExtDemo",
    7.         "icon": "$media:icon",
    8.         "name": "InputMethodExtAbility",
    9.         "srcEntry": "./ets/InputMethodExtensionAbility/InputMethodService.ts",
    10.         "type": "inputMethod",
    11.         "exported": true,
    12.         "metadata": [
    13.           {
    14.             "name": "ohos.extension.input_method",
    15.             "resource": "$profile:input_method_config"
    16.           }
    17.         ]
    18.       }
    19.     ]
    20.   }
    21. }
    
2. 子类型配置文件input_method_config.json需要放在应用资源目录的profile文件夹中，格式如下，字段释义参照[InputMethodSubtype](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod-subtype#inputmethodsubtype)；开发者需要严格按照配置文件格式及字段进行子类型信息配置，locale字段的配置参照[i18n-locale-culture](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/i18n-locale-culture#%E5%AE%9E%E7%8E%B0%E5%8E%9F%E7%90%86)。
    
    1. {
    2.   "subtypes": [
    3.     {
    4.       "icon": "$media:icon",
    5.       "id": "InputMethodExtAbility",
    6.       "label": "$string:english",
    7.       "locale": "en-US",
    8.       "mode": "lower"
    9.     },
    10.     {
    11.       "icon": "$media:icon",
    12.       "id": "InputMethodExtAbility1",
    13.       "label": "$string:chinese",
    14.       "locale": "zh-CN",
    15.       "mode": "lower"
    16.     }
    17.   ]
    18. }
    
3. 输入法应用中监听子类型事件，根据不同的子类型，可以加载不同的软键盘界面，或者通过状态变量控制软键盘显示效果。
    
    1. import { InputMethodSubtype, inputMethodEngine } from '@kit.IMEKit';
    
    2. let panelInfo: inputMethodEngine.PanelInfo = {
    3.   type: inputMethodEngine.PanelType.SOFT_KEYBOARD,
    4.   flag: inputMethodEngine.PanelFlag.FLG_FIXED
    5. };
    6. let inputMethodAbility: inputMethodEngine.InputMethodAbility = inputMethodEngine.getInputMethodAbility();
    7. // createPanel需要在InputMethodExtensionAbility的Create声明周期中完成，this.context是InputMethodExtensionAbility中的InputMethodExtensionContext
    8. inputMethodAbility.createPanel(this.context, panelInfo).then(async (panel: inputMethodEngine.Panel) => {
    9.   let inputPanel: inputMethodEngine.Panel = panel;
    10.   inputMethodAbility.on('setSubtype', (inputMethodSubtype: InputMethodSubtype) => {
    11.     // 保存当前输入法子类型, 此处也可以改变状态变量的值，布局中判断状态变量，不同的子类型显示不同的布局控件
    12.     let subType: InputMethodSubtype = inputMethodSubtype;
    13.     if (inputMethodSubtype.id == 'InputMethodExtAbility') { // 根据不同的子类型，可以加载不同的软键盘界面
    14.       inputPanel.setUiContent('pages/Index');
    15.     }
    16.     if (inputMethodSubtype.id == 'InputMethodExtAbility1') { // 根据不同的子类型，可以加载不同的软键盘界面
    17.       inputPanel.setUiContent('pages/Index1');
    18.     }
    19.   });
    20. }).catch((err: BusinessError) => {
    21.   console.error(`Failed to createPanel, code: ${err.code}, message: ${err.message}`);
    22. });
    

## 输入法子类型相关信息的获取

1. 开发者可以通过调用[getCurrentInputMethodSubtype](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#inputmethodgetcurrentinputmethodsubtype9)获取当前输入法应用的当前子类型。
    
2. 开发者可以通过调用[listCurrentInputMethodSubtype](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#listcurrentinputmethodsubtype9)获取当前输入法应用的所有子类型。
    
3. 开发者可以通过调用[listInputMethodSubtype](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#listinputmethodsubtype9)获取指定输入法应用的所有子类型。
    

## 输入法子类型的切换

1. 开发者可以通过调用[switchCurrentInputMethodSubtype](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#inputmethodswitchcurrentinputmethodsubtype9)切换当前输入法应用的子类型。
    
2. 开发者可以通过调用[switchCurrentInputMethodAndSubtype](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod#inputmethodswitchcurrentinputmethodandsubtype9)切换至指定输入法应用的指定子类型。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/switch-inputmethod-guide "切换输入法应用")
# 输入法安全模式介绍

更新时间: 2025-12-16 16:38

为了保护用户数据安全，系统增加了输入法安全模式功能，包括基础模式和完整体验模式。在基础模式下，输入法扩展无法调用任何可能涉及访问或泄漏用户隐私数据的系统能力；而在完整体验模式下，则没有该限制。

用户可以在设置应用中切换基础模式和完整体验模式。

## 基础模式介绍

1. 基础模式下，输入法扩展（InputMethodExtensionAbility）进程无法拉起其他UIAbility或ExtensionAbility。
2. 基础模式下，输入法扩展会受到系统管控，不能使用涉及访问或泄漏用户个人数据的各种接口，同时无法将数据传递出进程。管控功能包括但不限于：网络、短信、电话、麦克风、定位、相机、蓝牙、壁纸、支付、日历、游戏、扬声器、Wi-Fi、剪切板、多媒体、联系人、公共事件、系统账号、健康数据、地图服务、推送服务、融合搜索、共享内存、分布式特性、广告设备标识、振动等。
3. 基础模式下，输入法扩展可以使用基础输入功能必要的系统能力，例如，IME Kit、ArkUI、窗口、图形、屏幕管理等。
4. 基础模式下，输入法扩展对[共享沙箱](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ime-kit-security#section4219152220459)只读，对输入法扩展独立沙箱可读写；应用主入口可以对[共享沙箱](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ime-kit-security#section4219152220459)及其独立沙箱读写。

## 完整体验模式介绍

1. 完整体验模式下，输入法扩展不受基础模式相关限制，例如可以拉起其他UIAbility或ExtensionAbility、以调用访问用户数据的接口等。
2. 完整体验模式下，输入法扩展可以对[共享沙箱](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ime-kit-security#section4219152220459)读写。

## 开发指导

[onCreate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod-extension-ability#oncreate)在输入法扩展的 [onCreate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod-extension-ability#oncreate)生命周期回调函数中通过[getSecurityMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethodengine#getsecuritymode11)接口查询当前输入法应用的安全模式。

- 如果当前处于基础模式，开发者需要调整内部功能的呈现情况，以避免出现功能不可用的情况。
- 当处于完整体验模式时，开发者可以使用访问用户数据的接口，但这些接口的使用仅限于提升输入法的用户体验。

为了确保输入法功能的稳定性，开发者应当在基础模式下仅使用与基础输入功能相关的能力，并且不得试图绕过系统机制将数据传递到输入法扩展之外。

## 共享沙箱介绍

1. 输入法扩展使用独立沙箱，与应用主入口不可互相访问对方的独立沙箱。
2. 为方便输入法扩展和应用主入口之间数据传递和共享，提供了共享沙箱机制。输入法扩展和应用主入口都能够访问共享沙箱。
    
    **图1** 共享沙箱  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163822.14349901892980793407351425676225:50001231000000:2800:0D656594C1E2222A45E35B85A523D4FCA38CD74D0E0C8633DF76FC7FED7C7349.png "点击放大")
    
3. 共享沙箱的配置流程。
    
    当应用主入口的[profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-releaseprofile-0000001914714796)和输入法扩展的[dataGroupIds](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#extensionabilities%E6%A0%87%E7%AD%BE)包含相同的data-group-id时，他们就可以使用这个data-group-id对应的共享沙箱。
    
    为了使用共享沙箱，需要先申请一个data-group-id，分别配置到应用主入口的[profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-releaseprofile-0000001914714796)和输入法扩展的[dataGroupIds](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#extensionabilities%E6%A0%87%E7%AD%BE)。具体流程如下：
    
    1. 申请data-group-id，申请流程如下。
        1. 按照如下格式发送邮件到agconnect@huawei.com。
            1. 邮件标题格式：【输入法应用申请应用内数据共享】xxx应用
            2. 邮件内容：
                
                应用appid：xxx
                
                应用名称：xxx
                
                开发者id：xxx
                
                邮件附件中提供：
                
                ①输入法应用安装系统，在设置的输入法列表中该应用的截图。
                
                ②输入法应用中module.json5的InputMethodExtensionAbility相关配置截图。
                
        2. 审批完成后，您将收到邮件回复。
    2. 待您收到data-group-id申请成功的邮件回复后，重新生成[应用的profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-releaseprofile-0000001914714796)，新生成的profile里面包含本次申请到的data-group-id；并使用DevEco Studio[配置工程的签名信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-publish-app#section280162182818)，将新的profile配置到工程中。
    3. 按照data-group-id申请成功的回复邮件指导，获取到您本次申请到的data-group-id，并在InputMethodExtensionAbility所在的module.json5中配置[dataGroupIds](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#extensionabilities%E6%A0%87%E7%AD%BE)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163822.26774003681116737377411254502551:50001231000000:2800:FDB2F5FB1FC5763B7C2E8FA87841A37A980D689BBAA450CD2F765227B5CB1DC7.png)
    
4. 共享沙箱使用流程。
    1. 分别在输入法扩展和应用主入口通过[getGroupDir](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context#getgroupdir10)获取共享沙箱路径。
        
        说明
        
        注意：接口入参dataGroupID应该填写您本次申请到的data-group-id。
        
    2. 如果接口调用成功，且能够返回共享沙箱路径，说明您申请并配置的data-group-id已生效，此时您可通过共享沙箱在应用主入口和输入法扩展之间进行数据共享。
        
        说明
        
        注意：基础模式下输入法扩展对共享沙箱是只读权限，不可写入数据；完整体验模式下可读写。
        

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/input-method-subtype-guide "输入法子类型开发指南")
# 输入法应用沉浸模式

更新时间: 2025-12-16 16:38

## 场景介绍

为了让应用能够提供一致的沉浸式体验，我们提供了前台应用和输入法应用之间的通信机制。通过该机制，输入法应用根据前台应用设置的沉浸模式来决定最终沉浸模式。

## 框架原理

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163822.40537081826016969131979443759692:50001231000000:2800:92DE953C71B0E24EB44DEDA54D0EB60DDF582674460437AB0801290718FA57EF.png)

- 前台应用根据应用场景，设置应用期望的沉浸模式。
- 输入法框架在拉起输入法应用时会将前台应用期望的沉浸模式传递给输入法应用。
- 输入法应用根据前台应用的沉浸模式决定最终的沉浸模式，并设置最终沉浸模式给输入法框架。

## 接入指导

1. 前台应用[设置编辑框沉浸模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textarea#keyboardappearance15)。示例代码如下。
    
    1. TextArea({text: "hello world"})
    2.    .keyboardAppearance(KeyboardAppearance.IMMERSIVE)
    
2. 输入法应用[订阅编辑框属性变化事件](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethodengine#oneditorattributechanged10)，通过回调参数EditorAttribute中的immersiveMode字段感知前台应用期望的沉浸模式。示例代码如下。
    
    1. import { inputMethodEngine } from '@kit.IMEKit';
    
    2. inputMethodEngine.getKeyboardDelegate().on("editorAttributeChanged", (attr : inputMethodEngine.EditorAttribute) => {
    3.    console.info("received editorAttributeChanged, immersiveMode: " + attr.immersiveMode);
    4. })
    
3. 输入法应用[设置沉浸模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethodengine#setimmersivemode15)。
    
    - IMMERSIVE表示沉浸模式由输入法应用决定。
    - 输入法应用不能设置IMMERSIVE模式给输入法框架。
    - 如果输入法应用收到前台应用期望的沉浸模式为IMMERSIVE，建议输入法应用根据当前系统所处颜色模式，将最终沉浸模式设置为浅色沉浸模式（LIGHT_IMMERSIVE）或深色沉浸模式（DARK_IMMERSIVE）。
    
    设置沉浸模式，示例代码如下。setImmersiveMode接口需使用[createPanel](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethodengine#createpanel10)获取到Panel实例后，通过实例调用。
    
    1. import { inputMethodEngine } from '@kit.IMEKit';
    
    2. let panelInfo: inputMethodEngine.PanelInfo = {
    3.   type: inputMethodEngine.PanelType.SOFT_KEYBOARD,
    4.   flag: inputMethodEngine.PanelFlag.FLG_FIXED
    5. };
    6. let inputMethodAbility: inputMethodEngine.InputMethodAbility = inputMethodEngine.getInputMethodAbility();
    7. // createPanel需要在InputMethodExtensionAbility的Create声明周期中完成，this.context是InputMethodExtensionAbility中的InputMethodExtensionContext
    8. inputMethodAbility.createPanel(this.context, panelInfo).then(async (panel: inputMethodEngine.Panel) => {
    9.   let inputPanel: inputMethodEngine.Panel = panel;
    10.   try {
    11.     inputPanel?.setImmersiveMode(inputMethodEngine.ImmersiveMode.LIGHT_IMMERSIVE);
    12.   } catch (err) {
    13.     let error: BusinessError = err as BusinessError;
    14.     console.error(`Failed to setImmersiveMode, code: ${error.code}, message: ${error.message}`);
    15.   }
    16. }).catch((err: BusinessError) => {
    17.   console.error(`Failed to createPanel, code: ${err.code}, message: ${err.message}`);
    18. });
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/use-inputmethod-in-custom-edit-box-ndk "在自绘编辑框中使用输入法开发指导 (C/C++)")# Ime工具

更新时间: 2025-12-16 16:38

说明

Ime工具从API version 20开始支持。

**工具用法**

hdc shell ime [选项] [参数]

**命令列表**

|选项|参数|描述|
|:--|:--|:--|
|-e|bundle [-b /-f]|启用指定输入法到指定模式。未设置-b/-f选项时，默认-b为基础模式，-f为完整体验模式。<br><br>**注意：** 预置默认输入法不支持调用此命令改变使能状态。|
|-d|bundle|禁用指定输入法。<br><br>**注意：** 不允许禁用预置默认输入法。|
|-s|bundle|切换到指定输入法。<br><br>**注意：** 在锁屏或密码输入场景下，不允许切换到其他输入法。|
|-g|NA|获取当前输入法。|
|-l|NA|列出所有输入法。|
|-h|NA|显示本帮助信息。|

## 通过Ime工具管理输入法示例代码

1. 启用输入法，支持启用三方输入法到基础模式或者完整体验模式。
    
    1.  # 输入：hdc命令启用输入法。
    2.  # 处理：检查为shell调用后，将接到启用输入法的接口。
    3.  # 输出：效果等同于启用API调用。
    4.  # 基础模式
    5.  hdc shell ime -e com.xxx.yyy
    6.  # 完整体验模式
    7.  hdc shell ime -e com.xxx.yyy -f
    
2. 禁用输入法，支持停用三方输入法应用。
    
    1.  # 输入：hdc命令禁用输入法。
    2.  # 处理：检查为shell调用后，将接到禁用输入法的接口。
    3.  # 输出：效果等同于禁用API调用。
    4.  hdc shell ime -d com.xxx.yyy
    
3. 切换到指定输入法。
    
    1.  # 输入：hdc命令切换输入法。
    2.  # 处理：检查为shell调用后，将接到切换输入法接口。
    3.  # 输出：效果等同于切换输入法API调用。
    4.  hdc shell ime -s com.xxx.yyy
    
4. 获取当前输入法。
    
    1.  # 输入：hdc命令获取当前输入法。
    2.  # 处理：检查为shell调用后，将接到获取当前输入法接口。
    3.  # 输出：效果等同于获取当前输入法API调用。
    4.  hdc shell ime -g
    
5. 列出所有输入法，预置默认输入法不显示使能状态。
    
    1.  # 输入：hdc命令列出所有输入法。
    2.  # 处理：检查为shell调用后，将接到列出所有输入法接口。
    3.  # 输出：效果等同于列出所有输入法API调用。
    4.  hdc shell ime -l
    
6. 显示本帮助信息。
    
    1.  # 输入：hdc命令显示ime帮助信息。
    2.  # 输出：显示ime帮助信息。
    3.  hdc shell ime -h
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/inputmethod-immersive-mode-guide "输入法应用沉浸模式")
# 不可获焦窗口中输入框与输入法交互指南

更新时间: 2025-12-16 16:38

## 场景介绍

应用获得焦点是使用输入法的必要条件，开发者需要正确处理焦点以确保输入法的正常工作。

例如，在应用开发中，开发者可以通过[setWindowFocusable](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowfocusable9)，将创建的窗口的可获焦属性设置为false（如悬浮窗、辅助交互窗口等），并希望在该窗口中绘制输入框（如[TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput)、[TextArea](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textarea)或[自绘输入框](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/use-inputmethod-in-custom-edit-box)）以支持用户输入，即拉起系统键盘进行输入操作。

## 系统限制

当通过[setWindowFocusable](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowfocusable9)将窗口设置为不可获焦时，系统侧会对该窗口施加限制。由于窗口无焦点，输入事件（如按键信息）无法被窗口正确接收和处理，输入内容无法同步到该窗口中的输入框，导致输入框与键盘交互异常。

## 推荐方案

若需要在不可获焦窗口中绘制输入框，并希望能够与键盘正常交互，建议按照以下方式开发（以[TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput)为例）：

1. 在主窗中创建一个子窗，设置其初始为不可获焦窗口。
    
    可达到效果：点击主窗输入组件，弹出子窗，焦点仍然在主窗的输入框上。
    
    1. // Index.ets实现主窗的布局内容
    2. import { window } from '@kit.ArkUI';
    
    3. @Entry
    4. @Component
    5. struct Index {
    6.   async createSubWindow() {
    7.     try {
    8.       // 1.创建子窗并设置子窗id
    9.       let windowStage: window.WindowStage | undefined = AppStorage.get('windowStage');
    10.       if (windowStage == null) {
    11.         console.error('Failed to get windowStage');
    12.         return;
    13.       }
    14.       let options: window.SubWindowOptions = { title: 'title', decorEnabled: true };
    15.       let subWindow = await windowStage?.createSubWindowWithOptions('mySubWindow', options);
    16.       const subWindowId: number | undefined = subWindow?.getWindowProperties().id;
    17.       AppStorage.setOrCreate('subWindowId', subWindowId);
    18.       // 2.设置子窗为不可获焦
    19.       subWindow?.resize(500, 500);
    20.       subWindow?.setUIContent("pages/SubWindowIndex");
    21.       subWindow?.setWindowFocusable(false);
    22.       // 3.显示子窗
    23.       subWindow?.showWindow();
    24.     } catch (exception) {
    25.       console.error(`Failed to create the subWindow. Cause code: ${exception.code}, message: ${exception.message}`);
    26.     }
    27.   }
    
    28.   build() {
    29.     Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
    30.       TextInput({ placeholder: '点击创建并显示子窗' })
    31.         .onClick(() => {
    32.           this.createSubWindow();
    33.         })
    34.     }
    35.   }
    36. }
    
2. 当用户点击子窗中的输入框组件时，可以先通过[setWindowFocusable](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowfocusable9)将子窗设置为可获焦，然后通过[shiftAppWindowFocus](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-f#windowshiftappwindowfocus11)将焦点窗口从主窗切换为子窗，即可在子窗的输入框中正常使用输入法。
    
    1. // SubWindowIndex.ets实现子窗的布局内容
    2. import { window } from '@kit.ArkUI';
    
    3. @Entry
    4. @Component
    5. struct SubWindowIndex {
    6.   async shiftFocusToSubWindow() {
    7.     try {
    8.       let windowStage: window.WindowStage | undefined = AppStorage.get('windowStage');
    9.       if (windowStage == null) {
    10.         console.error('Failed to get the subwindow. Cause: windowStage is undefined');
    11.         return;
    12.       }
    13.       let subWindowList: window.Window[] = await windowStage?.getSubWindow();
    14.       let subWindow: window.Window = subWindowList[0];
    15.       // 1.将子窗口设置为可获焦
    16.       subWindow?.setWindowFocusable(true);
    17.       // 2.将焦点切换到子窗口
    18.       const mainWindowId: number = AppStorage.get('mainWindowId') || 0;
    19.       const subWindowId: number = AppStorage.get('subWindowId') || 0;
    20.       await window.shiftAppWindowFocus(mainWindowId, subWindowId);
    21.     } catch (exception) {
    22.       console.error(`Failed to shift focus to subWindow. Cause code: ${exception.code}, message: ${exception.message}`);
    23.     }
    24.   }
    
    25.   build() {
    26.     Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
    27.       TextInput({ placeholder: '这是一个输入组件' })
    28.         .onClick(() => {
    29.           // 用户点击子窗的输入组件，切换焦点至子窗
    30.           this.shiftFocusToSubWindow();
    31.         })
    32.     }
    33.   }
    34. }
    
3. 当用户重新点击子窗中的非输入框组件时，可以通过[setWindowFocusable](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window-window#setwindowfocusable9)将子窗重新设置为不可获焦，焦点窗口即可恢复至主窗。
    
    1. // SubWindowIndex.ets实现子窗的布局内容
    2. import { window } from '@kit.ArkUI';
    
    3. @Entry
    4. @Component
    5. struct SubWindowIndex {
    6.   async shiftFocusToSubWindow() {
    7.     try {
    8.       let windowStage: window.WindowStage | undefined = AppStorage.get('windowStage');
    9.       if (windowStage == null) {
    10.         console.error('Failed to get the subwindow. Cause: windowStage is undefined');
    11.         return;
    12.       }
    13.       let subWindowList: window.Window[] = await windowStage?.getSubWindow();
    14.       let subWindow: window.Window = subWindowList[0];
    15.       // 1.将子窗口设置为可获焦
    16.       subWindow?.setWindowFocusable(true);
    17.       // 2.将焦点切换到子窗口
    18.       const mainWindowId: number = AppStorage.get('mainWindowId') || 0;
    19.       const subWindowId: number = AppStorage.get('subWindowId') || 0;
    20.       await window.shiftAppWindowFocus(mainWindowId, subWindowId);
    21.     } catch (exception) {
    22.       console.error(`Failed to shift focus to subWindow. Cause code: ${exception.code}, message: ${exception.message}`);
    23.     }
    24.   }
    
    25.   async shiftFocusToMainWindow() {
    26.     try {
    27.       let windowStage: window.WindowStage | undefined = AppStorage.get('windowStage');
    28.       if (windowStage == null) {
    29.         console.error('Failed to get the subwindow. Cause: windowStage is undefined');
    30.         return;
    31.       }
    32.       let subWindowList: window.Window[] = await windowStage?.getSubWindow();
    33.       let subWindow: window.Window = subWindowList[0];
    34.       // 将子窗口设置为不可获焦
    35.       subWindow?.setWindowFocusable(false);
    36.     } catch (exception) {
    37.       console.error(`Failed to shift focus to main window. Cause code: ${exception.code}, message: ${exception.message}`);
    38.     }
    39.   }
    
    40.   build() {
    41.     Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
    42.       TextInput({ placeholder: '这是一个输入组件' })
    43.         .onClick(() => {
    44.           // 点击子窗输入组件时，切换焦点至子窗口
    45.           this.shiftFocusToSubWindow();
    46.         })
    47.       Button('这是一个普通组件')
    48.         .onClick(() => {
    49.           // 点击子窗非输入组件时，可切换焦点回主窗口
    50.           this.shiftFocusToMainWindow();
    51.         })
    52.     }
    53.   }
    54. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/inputmethod-hdc-commands-guide "Ime工具")
