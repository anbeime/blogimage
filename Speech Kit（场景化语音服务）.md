# Speech Kit简介

更新时间: 2025-12-16 16:27

Speech Kit（场景化语音服务）集成了语音类AI能力，包括朗读控件（TextReader）和AI字幕控件（AICaptionComponent）能力，便于用户与设备进行互动，为用户实现朗读文章。

## 场景介绍

- 朗读控件应用广泛，例如在用户不方便或者无法查看屏幕文字时，为用户朗读新闻，提供资讯。
- AI字幕控件应用广泛，例如在用户不熟悉音频源语言或者静音时，为用户提供字幕服务。

## 约束与限制

- 设备限制
    
    本Kit仅适用于Phone、Tablet、和2in1设备，暂不支持模拟器。
    
- 地区限制
    
    本Kit仅支持中国境内（不包含中国香港、中国澳门、中国台湾）提供服务。
    
- 能力限制

|AI能力|约束|
|:--|:--|
|朗读控件|支持的语种类型：中文。|
|AI字幕控件|支持的语种类型：中英文。<br><br>支持的音频流：<br><br>- 音频类型：当前仅支持 "pcm"编码。<br>- 音频采样率：当前仅支持16000采样率。<br>- 音频声道：当前仅支持1个通道。<br>- 音频采样位深：当前仅支持16位。<br><br>部分机型暂不支持，调用失败返回对应错误码[初始化失败](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-errorcode#section1989336165612)。|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/speech-kit-guide "Speech Kit（场景化语音服务）")
# 朗读控件

更新时间: 2025-12-16 16:27

## 适用场景

朗读控件应用广泛，例如在用户不方便或者无法查看屏幕文字的时候，为用户朗读新闻，提供资讯。

本章节将向您介绍如何使用朗读组件，效果如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162747.95345178436513255428745818609401:50001231000000:2800:B4991AD0819FEF11249E9E8A8F447F7CCB618DBC6ED0DC919BD14822584AF184.png)

## 接口说明

以下仅列出demo中调用的部分主要接口，具体API说明详见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-textreader-api)。

|接口名|描述|
|:--|:--|
|[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-textreader-api#section173751154134515)(context: [common.BaseContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-basecontext), readParams: [ReaderParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-textreader-api#section6129163245310)): Promise<void>|初始化TextReader。|
|[start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-textreader-api#section143611912403)(readInfoList: [ReadInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-textreader-api#section129918404172)[], articleId?: string): Promise<void>|启动TextReader。|
|on(type: string, callback: function): void|注册所有事件回调，具体事件类型详见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-textreader-api)。|
|[ReaderParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-textreader-api#section6129163245310)(isVoiceBrandVisible: boolean, businessBrandInfo?: [BusinessBrandInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-textreader-api#section472059101210), isFastForward?: boolean, keepBackgroundRunning?: boolean, online?: number)|朗读参数。|

## 开发步骤

1. 首先从项目根目录进入/src/main/ets/entryability/EntryAbility.ets文件，将WindowManager添加至工程。
    
    1. import { WindowManager } from '@kit.SpeechKit';
    2. import { ConfigurationConstant } from '@kit.AbilityKit';
    
2. （可选）在onWindowStageCreate(windowStage: window.WindowStage)生命周期方法中，添加setWindowStage方法设置窗口管理器。
    
    1. onWindowStageCreate(windowStage: window.WindowStage): void {
    2.   console.info('Ability onWindowStageCreate');
    3.   WindowManager.setWindowStage(windowStage);
    
    4.   windowStage.loadContent('pages/Index', (err, data) => {
    5.     if (err) {
    6.       console.error(`Failed to load the content. Code: ${err.code}, message: ${err.message}`);
    7.       return;
    8.     }
    9.     console.info(`Succeeded in loading the content. Data: ${JSON.stringify(data)}.` );
    10.   });
    11. }
    
3. 在onCreate()生命周期方法中，设置应用的颜色模式，使控件颜色模式跟应用的颜色模式保持一致。
    
    - 如果应用想要跟随系统切换深浅色模式，请将颜色模式设置为COLOR_MODE_NOT_SET。
    - 如果应用想要主动配置颜色模式，请将颜色模式设置为COLOR_MODE_LIGHT（浅色）或者COLOR_MODE_DARK（深色）。
    
    下面以自动跟随系统切换为例。
    
    1. onCreate(): void {
    2.   this.context.getApplicationContext().setColorMode(ConfigurationConstant.ColorMode.COLOR_MODE_NOT_SET);
    3. }
    
4. 从项目根目录进入/src/main/ets/pages/Index.ets文件，在使用朗读控件前，将实现朗读控件和其他相关的类添加至工程。
    
    1. import { TextReader, TextReaderIcon, ReadStateCode } from '@kit.SpeechKit';
    
5. 简单配置页面的布局，加入听筒图标，并且设置onClick点击事件。
    
    1. /**
    2.  * 播放状态
    3.  */
    4. @State readState: ReadStateCode = ReadStateCode.WAITING;
    
    5. build() {
    6.     Column() {
    7.       TextReaderIcon({ readState: this.readState })
    8.         .margin({ right: 20 })
    9.         .width(32)
    10.         .height(32)
    11.         .onClick(async () => {
    12.             // 设置点击事件
    13.             // ...
    14.         })
    15.     }
    16. }
    
6. 初始化朗读控件。
    
    1. // 用于显示当前页的按钮状态
    2. @State isInit: boolean = false;
    3. /**
    4. * 待加载的文章
    5. */
    6. @State readInfoList: TextReader.ReadInfo[] = [];
    7. @State selectedReadInfo: TextReader.ReadInfo = this.readInfoList[0];
    
    8. async aboutToAppear() {
    9.   // ...
    10.   this.init();
    11.   /**
    12.    * 加载数据
    13.    */
    14.   let readInfoList: TextReader.ReadInfo[] = [{
    15.     id: '001',
    16.     title: {
    17.       text:'水调歌头.明月几时有',
    18.       isClickable:true
    19.     },
    20.     author:{
    21.       text:'宋.苏轼',
    22.       isClickable:true
    23.     },
    24.     date: {
    25.       text:'2024/01/01',
    26.       isClickable:false
    27.     },
    28.     bodyInfo: '明月几时有？把酒问青天。'
    29.   }];
    30.   this.readInfoList = readInfoList;
    31.   this.selectedReadInfo = this.readInfoList[0];
    32.   // ...
    33. }
    
    34. /**
    35.  * 初始化
    36.  */
    37. async init() {
    38.   const readerParam: TextReader.ReaderParam = {
    39.     isVoiceBrandVisible: true,
    40.     businessBrandInfo: {
    41.       panelName: '小艺朗读',
    42.       panelIcon: $r('app.media.startIcon')
    43.     }
    44.   }
    45.   try {
    46.     let context: Context | undefined = this.getUIContext().getHostContext()
    47.     if (context) {
    48.       await TextReader.init(context, readerParam);
    49.       this.isInit = true;
    50.       this.setActionListener();
    51.     }
    52.   } catch (err) {
    53.     console.error(`TextReader failed to init. Code: ${err.code}, message: ${err.message}`);
    54.   }
    55. }
    
    56. onStateChanged = (state: TextReader.ReadState) => {
    57.   if (this.selectedReadInfo?.id === state.id) {
    58.     this.readState = state.state;
    59.   } else {
    60.     this.readState = ReadStateCode.WAITING;
    61.   }
    62. }
    
    63. // 设置操作监听
    64. setActionListener() {
    65.   TextReader.on('stateChange', (state: TextReader.ReadState) => {
    66.     this.onStateChanged(state);
    67.   });
    68.   // 在列表页无更多内容时，会显示加载失败，需要设置requestMore监听，调用loadMore函数以获得正确的显示信息。
    69.   TextReader.on('requestMore', () => {
    70.     TextReader.loadMore([], true);
    71.   })
    72. }
    
    73. // 注销监听，根据业务情况在合适的时机调用
    74. releaseActionListener() {
    75.   TextReader.off('stateChange');
    76.   TextReader.off('requestMore');
    77. }
    
7. （可选）在setActionListener方法中设置更多监听，在用户与控件进行交互时触发回调通知开发者。注销监听，监听结束后进行释放。
    
    1. // 设置监听
    2. setActionListener() {
    3.   TextReader.on('setArticle', async (id: string) => { console.info(`setArticle ${id}`) });
    4.   TextReader.on('clickArticle', (id: string) => {console.info(`onClickArticle ${id}`) });
    5.   TextReader.on('clickAuthor', (id: string) => { console.info(`onClickAuthor ${id}`) });
    6.   TextReader.on('clickNotification',  (id: string) => { console.info(`onClickNotification ${id}`) });
    7.   TextReader.on('showPanel', () => { console.info(`onShowPanel`) });
    8.   TextReader.on('hidePanel', () => { console.info(`onHidePanel`) });
    9.   // ...
    10. }
    11. // 注销监听
    12. releaseActionListener() {
    13.   TextReader.off('setArticle');
    14.   TextReader.off('clickArticle');
    15.   TextReader.off('clickAuthor');
    16.   TextReader.off('clickNotification');
    17.   TextReader.off('showPanel');
    18.   TextReader.off('hidePanel');
    19.   // ...
    20. }
    
8. 启动朗读控件。
    
    1. build() {
    2.   Column() {
    3.     TextReaderIcon({ readState: this.readState })
    4.       // ...
    5.       .onClick(async () => {
    6.         try {
    7.           await TextReader.start(this.readInfoList, this.selectedReadInfo?.id);
    8.         } catch (err) {
    9.           console.error(`TextReader failed to start. Code: ${err.code}, message: ${err.message}`);
    10.         }
    11.       })
    12.   }
    13. }
    
9. （可选）若要配置长时任务，需要在[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中添加ohos.permission.KEEP_BACKGROUND_RUNNING权限，并且加入backgroundModes选项，然后在readerParam中将keepBackgroundRunning配置为true，确保朗读控件后台播报正常。
    
    1. // module.json5
    2. {
    3.   "module": {
    4.     // ...
    5.     "requestPermissions": [
    6.       {
    7.         "name": "ohos.permission.KEEP_BACKGROUND_RUNNING",
    8.         "usedScene": {
    9.           "abilities": [
    10.             "FormAbility"
    11.           ],
    12.           "when": "inuse"
    13.         }
    14.       },
    15.     ],
    16.     "abilities": [
    17.       {
    18.         // ...
    19.         "backgroundModes": [
    20.           "audioPlayback"
    21.         ],
    22.         // ...
    23.       }
    24.     ]
    25.   }
    26. }
    
    27. // Index.ets
    28. async init() {
    29.   const readerParam: TextReader.ReaderParam = {
    30.     // ...
    31.     keepBackgroundRunning: true
    32.   }
    33. }
    
10. （可选）若要在控件使用功能时切换音色，需要在[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中添加ohos.permission.INTERNET和ohos.permission.GET_NETWORK_INFO权限，确保朗读控件可以正常切换音色。
    
    1. // module.json5
    2. {
    3.   "module": {
    4.     // ...
    5.     "requestPermissions": [
    6.       {
    7.         "name": "ohos.permission.INTERNET",
    8.         "reason": "$string:reason",
    9.         "usedScene": {"abilities": []}
    10.       },
    11.       {
    12.         "name": "ohos.permission.GET_NETWORK_INFO",
    13.         "reason": "$string:reason",
    14.         "usedScene": {"abilities": []}
    15.       },
    16.     ],
    17.   }
    18. }
    

## 开发实例

EntryAbility.ets

1. import { AbilityConstant, ConfigurationConstant, UIAbility, Want } from '@kit.AbilityKit';
2. import { window } from '@kit.ArkUI';
3. import { WindowManager } from '@kit.SpeechKit';

4. export default class EntryAbility extends UIAbility {
5.   onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
6.     this.context.getApplicationContext().setColorMode(ConfigurationConstant.ColorMode.COLOR_MODE_NOT_SET);
7.     console.info('Ability onCreate');
8.   }

9.   onDestroy(): void {
10.     console.info('Ability onDestroy');
11.   }

12.   onWindowStageCreate(windowStage: window.WindowStage): void {
13.     console.info('Ability onWindowStageCreate');
14.     WindowManager.setWindowStage(windowStage);

15.     windowStage.loadContent('pages/Index', (err, data) => {
16.       if (err.code) {
17.         console.error(`Failed to load the content. Code: ${err.code}, message: ${err.message}`);
18.         return;
19.       }
20.       console.info(`Succeeded in loading the content. Data: ${JSON.stringify(data)}.` );
21.     });
22.   }

23.   onWindowStageDestroy(): void {
24.     console.info('Ability onWindowStageDestroy');
25.   }

26.   onForeground(): void {
27.     console.info('Ability onForeground');
28.   }

29.   onBackground(): void {
30.     console.info('Ability onBackground');
31.   }
32. }

Index.ets

1. import { TextReader, TextReaderIcon, ReadStateCode } from '@kit.SpeechKit';

2. @Entry
3. @Component
4. struct Index {

5.   /**
6.    * 待加载的文章
7.    */
8.   @State readInfoList: TextReader.ReadInfo[] = [];
9.   @State selectedReadInfo: TextReader.ReadInfo = this.readInfoList[0];

10.   /**
11.    * 播放状态
12.    */
13.   @State readState: ReadStateCode = ReadStateCode.WAITING;

14.   /**
15.    * 用于显示当前页的按钮状态
16.    */
17.   @State isInit: boolean = false;

18.   async aboutToAppear(){
19.     /**
20.      * 加载数据
21.      */
22.     let readInfoList: TextReader.ReadInfo[] = [{
23.       id: '001',
24.       title: {
25.         text:'水调歌头.明月几时有',
26.         isClickable:true
27.       },
28.       author:{
29.         text:'宋.苏轼',
30.         isClickable:true
31.       },
32.       date: {
33.         text:'2024/01/01',
34.         isClickable:false
35.       },
36.       bodyInfo: '明月几时有？把酒问青天。'
37.     }];
38.     this.readInfoList = readInfoList;
39.     this.selectedReadInfo = this.readInfoList[0];
40.     this.init();
41.   }

42.   /**
43.    * 初始化
44.    */
45.   async init() {
46.     const readerParam: TextReader.ReaderParam = {
47.       isVoiceBrandVisible: true,
48.       businessBrandInfo: {
49.         panelName: '小艺朗读',
50.         panelIcon: $r('app.media.startIcon')
51.       }
52.     }
53.     try {
54.       let context: Context | undefined = this.getUIContext().getHostContext()
55.       if (context) {
56.         await TextReader.init(context, readerParam);
57.         this.isInit = true;
58.         this.setActionListener();
59.       }
60.     } catch (err) {
61.       console.error(`TextReader failed to init. Code: ${err.code}, message: ${err.message}`);
62.     }
63.   }

64.   // 设置操作监听
65.   setActionListener() {
66.     TextReader.on('stateChange', (state: TextReader.ReadState) => {
67.       this.onStateChanged(state);
68.     });

69.     TextReader.on('requestMore', () => {
70.       TextReader.loadMore([], true);
71.     })
72.   }

73.   onStateChanged = (state: TextReader.ReadState) => {
74.     if (this.selectedReadInfo?.id === state.id) {
75.       this.readState = state.state;
76.     } else {
77.       this.readState = ReadStateCode.WAITING;
78.     }
79.   }

80.   build() {
81.     Column() {
82.       TextReaderIcon({ readState: this.readState })
83.         .margin({ right: 20 })
84.         .width(32)
85.         .height(32)
86.         .onClick(async () => {
87.           try {
88.             await TextReader.start(this.readInfoList, this.selectedReadInfo?.id);
89.           } catch (err) {
90.             console.error(`TextReader failed to start. Code: ${err.code}, message: ${err.message}`);
91.           }
92.         })
93.     }
94.     .height('100%')
95.   }
96. }

## 2in1适配步骤

2in1设备除了适配[开发步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/speech-textreader-guide#section1418318341804)，还需执行以下步骤。如果开发者按照上述开发步骤来适配2in1，将会出现无法拉起播放面板的情况。

1. 在/src/main/ets/entryability下新建一个ability，用来承载2in1主窗，导入相关依赖。
    
    1. import { TextReader, WindowManager } from '@kit.SpeechKit';
    2. import { commonEventManager } from '@kit.BasicServicesKit';
    
2. 在新ability中声明一个应用全局的状态变量isReadyToStart，并且通过AppStorage管理此状态变量。
    
    1. private link: SubscribedAbstractProperty<boolean>= AppStorage.link('isReadyToStart');
    
3. 在Index.ets的aboutToAppear生命周期方法中，创建全局的状态变量isReadyToStart。
    
    1. aboutToAppear() {
    2.   AppStorage.setOrCreate('isReadyToStart', false);
    3.   // ...其他配置
    4. }
    
4. 配置WindowStage。说明：从6.0.0(20)开始使用以下逻辑实现。对于5.1.1(19)及之前版本，使用getContext(this)接口实现。
    
    - 在新ability的onWindowStageCreate生命周期方法中，发送onLoadSubAbility事件。
    - 通过WindowManager.setWindowStage(windowStage)来设置新ability的windowStage。
    - 在onWindowStageCreate中将isReadyToStart设为true。
    
    1. onWindowStageCreate(windowStage: window.WindowStage): void {
    2.   // Main window is created, set main page for this ability
    3.   WindowManager.setWindowStage(windowStage)
    4.   let eventData: emitter.EventData = {
    5.     data: {
    6.       'state': 'publish'
    7.     }
    8.   }
    9.   emitter.emit("onLoadSubAbility", eventData);
    10.   this.link.set(true);
    11. }
    
5. 在新ability的onWindowStageDestroy生命周期方法中，将isReadyToStart设为false，同时隐藏面板并停止播放。
    
    1. async onWindowStageDestroy(): Promise<void> {
    2.   try {
    3.     TextReader.hidePanel();
    4.     await TextReader.stop();
    5.     this.link.set(false);
    6.   }catch (e) {
    7.     console.error(`onWindowStageDestroy fail , msg: ${e}`)
    8.   }
    9. }
    
6. 在entryability中，onCreate方法需要用eventHub设置'onShowPanel'回调，用来创造新的ability；onShowPanel回调中，首先构造want，然后通过context.startAbility接口创建新的ability。
    
    1. import { AbilityConstant, Want } from '@kit.AbilityKit';
    2. import { common } from "@kit.AbilityKit";
    3. import { BusinessError } from "@kit.BasicServicesKit";
    
    4. onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    5.   // ...其他配置
    6.   let eventHub = this.context.eventHub;
    7.   eventHub.on('onShowPanel', this.onShowPanel);
    8. }
    
    9. onShowPanel = () => {
    10.   let context: common.UIAbilityContext = this.context;
    11.   let want: Want = {
    12.     deviceId: '',
    13.     bundleName: 'com.example.speechkit', // 需替换成实际应用包名
    14.     abilityName: 'SubAbility',
    15.     parameters: {
    16.       info: 'From EntryAbility onShowPanel'
    17.     }
    18.   }
    19.   context?.startAbility(want).then(() => {
    20.     console.info('Succeeded in starting ability');
    21.   }).catch((e: BusinessError) => {
    22.     console.error(`Failed to start ability. Code is ${e.code}, message is ${e.message}`);
    23.   })
    24. }
    
7. 在调用start之前根据设备类型进行判断，如果是2in1需要首先发送'onShowPanel'事件构造ability。
    
    1. import { deviceInfo } from '@kit.BasicServicesKit';
    
    2. if (deviceInfo.deviceType === '2in1') {
    3.   let context = this.getUIContext().getHostContext();
    4.   context?.eventHub.emit('onShowPanel');
    5. }
    6. TextReader.showPanel();
    
8. 在module.json5中添加ability配置项，max和min的值需要保持一致，固定窗口的大小。
    
    1. {
    2.   "name": "SubAbility", // UIAbility组件的名称
    3.   "srcEntry": "./ets/entryability/SubAbility.ets", // UIAbility组件的代码路径
    4.   "description": "$string:SubAbility_desc", // UIAbility组件的描述信息
    5.   "icon": "$media:icon", // UIAbility组件的图标
    6.   "label": "$string:EntryAbility_label", // UIAbility组件的标签
    7.   "startWindowIcon": "$media:icon", // UIAbility组件启动页面图标资源文件的索引
    8.   "startWindowBackground": "$color:start_window_background", // UIAbility组件启动页面背景颜色资源文件的索引
    9.   "supportWindowMode": ['floating'], // 窗口支持悬浮窗显示
    10.   "maxWindowWidth": 1158,  // 最大窗口宽度
    11.   "minWindowWidth": 1158,  // 最小窗口宽度
    12.   "maxWindowHeight": 772,  // 最大窗口高度
    13.   "minWindowHeight": 772,  // 最小窗口高度
    14.  }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/speech-production "Speech Kit简介")
# AI字幕控件

更新时间: 2025-12-16 16:27

## 适用场景

AI字幕控件应用广泛，例如在用户不熟悉音频源语言或者静音的时候，为用户提供字幕服务。

本章节将向您介绍如何使用AI字幕组件[AICaptionComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-aicaptioncomponent)和[AICaptionController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-aicaptioncomponent#section816451553012)展示AI字幕，效果如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162748.13034644834190899635309030256756:50001231000000:2800:A330E23D0F5D004766412C02D1727C2606A29F245F5E20977F4AA305041BA07C.jpg "点击放大")

## 接口说明

AI字幕功能主要由[AICaptionComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-aicaptioncomponent)提供，更多接口及使用方法请参见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-aicaptioncomponent)。

|接口|描述|
|:--|:--|
|[AICaptionComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-aicaptioncomponent)|AI字幕组件。|
|[AICaptionOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-aicaptioncomponent#section15787428226)|AI字幕初始化参数。|
|[AICaptionController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/speech-aicaptioncomponent#section816451553012)|AI字幕组件的控制器，是AI字幕组件的主要功能入口类，用来操作AI字幕。它所承载的工作包括：写音频数据、获取音频流信息等。|

## 开发步骤

1. 从项目根目录进入/src/main/ets/pages/Index.ets文件，在使用AI字幕控件前，将实现AI字幕控件和其他相关的类添加至工程。
    
    1. import { AICaptionComponent, AICaptionController, AICaptionOptions } from '@kit.SpeechKit';
    
2. 简单配置页面的布局，加入AI字幕组件，并在aboutToAppear中设置AI字幕组件的传入参数。
    
    1. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    2. const TAG = 'AI_CAPTION_DEMO'
    
    3. class Logger {
    4.   static info(...msg: string[]) {
    5.     hilog.info(0x0000, TAG, msg.join())
    6.   }
    
    7.   static error(...msg: string[]) {
    8.     hilog.error(0x0000, TAG, msg.join())
    9.   }
    10. }
    
    11. @Entry
    12. @Component
    13. struct Index {
    14.   private captionOption ?: AICaptionOptions;
    15.   private controller = new AICaptionController();
    16.   @State isShown: boolean = false;
    
    17.   aboutToAppear(): void {
    18.     // AI字幕初始化参数，设置字幕的不透明度和回调函数
    19.     this.captionOption = {
    20.       initialOpacity: 1,
    21.       onPrepared: () => {
    22.         Logger.info('onPrepared')
    23.       },
    24.       onError: (error) => {
    25.         Logger.error(`onError, code: ${error.code}, msg: ${error.message}`)
    26.       }
    27.     }
    28.   }
    
    29.   build() {
    30.     Column({ space: 20 }) {
    31.       // 调用AICaptionComponent组件初始化字幕
    32.       AICaptionComponent({
    33.         isShown: this.isShown,
    34.         controller: this.controller,
    35.         options: this.captionOption
    36.       })
    37.         .width('100%')
    38.         .height(100)
    39.       Divider()
    40.       if (this.isShown) {
    41.         Text('上面是字幕区域')
    42.           .fontColor(Color.White)
    43.       }
    44.     }
    45.     .width('100%')
    46.     .height('100%')
    47.     .padding(10)
    48.     .backgroundColor('#7A7D6A')
    49.   }
    50. }
    
3. 在布局中加入两个按钮以及点击事件的回调函数。
    
    - 第一个按钮的回调函数负责控制AI字幕组件的显示状态。
    - 第二个按钮的回调函数负责读取资源目录中的音频文件，将音频数据传给AI字幕组件。
    
    1. import { AudioData } from '@kit.SpeechKit';
    
    2. @Entry
    3. @Component
    4. struct Index {
    
    5.   isReading: boolean = false;
    
    6.   async readPcmAudio() {
    7.     this.isReading = true;
    8.     let fileData: Uint8Array | undefined;
    9.     try {
    10.       fileData =
    11.         await this.getUIContext()?.getHostContext()?.resourceManager.getMediaContent($r('app.media.chineseAudio').id);
    12.     } catch (e) {
    13.       Logger.info(`get fileData fail , msg ${e} `)
    14.     }
    15.     if (fileData === undefined) {
    16.       return;
    17.     }
    18.     const bufferSize = 640;
    19.     const byteLength = fileData.byteLength;
    20.     let offset = 0;
    21.     Logger.info('byteLength', byteLength.toString())
    22.     let startTime = new Date().getTime();
    23.     while (offset < byteLength) {
    24.       // 模拟实际情况，读文件比录音机返回流快，所以要等待一段时间
    25.       let nextOffset = offset + bufferSize
    26.       if (offset > byteLength) {
    27.         this.isReading = false;
    28.         return
    29.       }
    30.       const arrayBuffer = fileData.buffer.slice(offset, nextOffset);
    31.       let data = new Uint8Array(arrayBuffer);
    32.       Logger.info('data byteLength', data.byteLength.toString())
    33.       const audioData: AudioData = {
    34.         data: data
    35.       }
    36.       Logger.info(`offset: ${offset} | byteLength: ${byteLength} | bufferSize: ${bufferSize}`)
    
    37.       if (this.controller) {
    38.         Logger.info(`writeAudio： ${audioData.data.byteLength}`)
    39.        try {
    40.           this.controller.writeAudio(audioData)
    41.         } catch (e) {
    42.           Logger.error(`writeAudio exception`)
    43.         }
    44.       }
    45.       offset = offset + bufferSize;
    46.       const waitTime = bufferSize / 32
    47.       await this.sleep(waitTime)
    48.     }
    49.     let endTime = new Date().getTime()
    50.     this.isReading = false;
    51.     Logger.info('playtime', JSON.stringify(endTime - startTime))
    52.   }
    
    53.   sleep(time: number): Promise<void> {
    54.     return new Promise(resolve => setTimeout(resolve, time))
    55.   }
    
    56.   build() {
    57.     Column({ space: 20 }) {
    58.      // ...
    59.       Button('切换字幕显示状态:' + (this.isShown ? '显示' : '隐藏'))
    60.         .backgroundColor('#B8BDA0')
    61.         .width(200)
    62.         .onClick(() => {
    63.           this.isShown = !this.isShown;
    64.         })
    65.       Button('读取PCM音频')
    66.         .backgroundColor('#B8BDA0')
    67.         .width(200)
    68.         .onClick(() => {
    69.           if (!this.isReading) {
    70.             this.readPcmAudio()
    71.           }
    72.         })
    73.      // ...
    74.     }
    75.   }
    76. }
    

## 开发实例

Index.ets

1. import { AICaptionComponent, AICaptionOptions, AICaptionController, AudioData } from '@kit.SpeechKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';

4. const TAG = 'AI_CAPTION_DEMO'

5. class Logger {
6.   static info(...msg: string[]) {
7.     hilog.info(0x0000, TAG, msg.join())
8.   }

9.   static error(...msg: string[]) {
10.     hilog.error(0x0000, TAG, msg.join())
11.   }
12. }

13. @Entry
14. @Component
15. struct Index {
16.   private captionOption?: AICaptionOptions;
17.   private controller: AICaptionController = new AICaptionController();
18.   @State isShown: boolean = false;
19.   isReading: boolean = false;

20.   aboutToAppear(): void {
21.     // AI字幕初始化参数，设置字幕的不透明度和回调函数
22.     this.captionOption = {
23.       initialOpacity: 1,
24.       onPrepared: () => {
25.         Logger.info('onPrepared')
26.       },
27.       onError: (error: BusinessError) => {
28.         Logger.error(`AICaption component error. Error code: ${error.code}, message: ${error.message}`)
29.       }
30.     }
31.   }

32.   async readPcmAudio() {
33.     this.isReading = true;
34.     // chineseAudio.pcm文件放在entry\src\main\resources\base\media路径下
35.     let fileData: Uint8Array | undefined;
36.     try {
37.       fileData =
38.         await this.getUIContext()?.getHostContext()?.resourceManager.getMediaContent($r('app.media.chineseAudio').id);
39.     } catch (e) {
40.       Logger.info(`get fileData fail , msg ${e} `)
41.     }
42.     if (fileData === undefined) {
43.       return;
44.     }
45.     const bufferSize = 640;
46.     const byteLength = fileData.byteLength;
47.     let offset = 0;
48.     Logger.info(`Pcm data total bytes: ${byteLength.toString()}`)
49.     let startTime = new Date().getTime();
50.     while (offset < byteLength) {
51.       // 模拟实际情况，读文件比录音机返回流快，所以要等待一段时间
52.       let nextOffset = offset + bufferSize
53.       if (offset > byteLength) {
54.         this.isReading = false;
55.         return
56.       }
57.       const arrayBuffer = fileData.buffer.slice(offset, nextOffset);
58.       let data = new Uint8Array(arrayBuffer);
59.       const audioData: AudioData = {
60.         data: data
61.       }

62.       if (this.controller) {
63.         try {
64.           this.controller.writeAudio(audioData)
65.         } catch (e) {
66.           Logger.error(`writeAudio exception`)
67.         }
68.       }
69.       offset = offset + bufferSize;
70.       const waitTime = bufferSize / 32
71.       await this.sleep(waitTime)
72.     }
73.     let endTime = new Date().getTime()
74.     this.isReading = false;
75.     Logger.info(`Audio play time: ${JSON.stringify(endTime - startTime)}`)
76.   }

77.   sleep(time: number): Promise<void> {
78.     return new Promise(resolve => setTimeout(resolve, time))
79.   }

80.   build() {
81.     Column({ space: 20 }) {
82.       Button('切换字幕显示状态:' + (this.isShown ? '显示' : '隐藏'))
83.         .backgroundColor('#B8BDA0')
84.         .width(200)
85.         .onClick(() => {
86.           this.isShown = !this.isShown;
87.         })
88.       Button('读取PCM音频')
89.         .backgroundColor('#B8BDA0')
90.         .width(200)
91.         .onClick(() => {
92.           if (!this.isReading) {
93.             this.readPcmAudio()
94.           }
95.         })
96.       Divider()
97.       // 调用AICaptionComponent组件初始化字幕
98.       AICaptionComponent({
99.         isShown: this.isShown,
100.         controller: this.controller,
101.         options: this.captionOption
102.       })
103.         .width('100%')
104.         .height(100)
105.       Divider()
106.       if (this.isShown) {
107.         Text('上面是字幕区域')
108.           .fontColor(Color.White)
109.       }
110.     }
111.     .width('100%')
112.     .height('100%')
113.     .padding(10)
114.     .backgroundColor('#7A7D6A')
115.   }
116. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/speech-textreader-guide "朗读控件")
# Vision Kit简介

更新时间: 2025-12-16 16:27

Vision Kit（场景化视觉服务）集成了视觉类AI能力，包括人脸活体检测（interactiveLiveness）能力、卡证识别（CardRecognition）能力、文档扫描（DocumentScanner）能力、AI识图控件（visionImageAnalyzer）能力。人脸活体检测能力便于用户与设备进行互动，验证用户是否为真实活体；卡证识别能力可提供身份证、行驶证、驾驶证、护照、银行卡等证件的结构化识别服务；文档扫描控件可提供拍摄文档并转换为高清扫描件的服务；AI识图控件可提供场景化的文本识别、主体分割、识图搜索功能。其中动作活体检测能力、卡证识别能力实施试用期免费的计费政策，试用期至2026年12月31日。开始正式收费前，华为将会提前通过正式途径发布计费调整通告。

## 场景介绍

Vision Kit提供了人脸活体检测能力、卡证识别能力、文档扫描能力和AI识图能力，具体如下：

- [人脸活体检测](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-interactiveliveness)：通过动作活体检测，验证用户是否为真实活体。
- [卡证识别](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-cardrecognition)：多证件的结构化识别服务。
- [文档扫描](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-documentscanner)：提供拍摄文档并转换为高清扫描件的服务。
- [AI识图](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-imageanalyzer)：提供场景化的文本识别、主体分割、识图搜索功能。

## 约束与限制

### 支持的设备

|能力|支持的设备|
|:--|:--|
|人脸活体检测|Phone、Tablet。|
|卡证识别|Phone、Tablet。|
|文档扫描|Phone、Tablet。|
|AI识图|Phone、Tablet、PC/2in1。|

### 支持的国家/地区

仅适用于中国境内（不包含中国香港、中国澳门、中国台湾）。

### 能力限制

|AI能力|约束|
|:--|:--|
|人脸活体检测|- 支持的文本语种类型：简体中文、繁体中文、英文、维吾尔文、藏文。<br>- 支持的播报语种类型：简体中文、英文。<br>- 人脸活体检测服务暂不支持横屏、分屏进行检测。|
|卡证识别|- 支持的语种类型：简体中文、英文。<br>- 卡证识别暂时只支持身份证、行驶证、驾驶证、护照、银行卡5种卡证。<br>- 不允许被其他组件或窗口遮挡。|
|文档扫描|- 支持的语种类型：简体中文、英文。<br>- 文档扫描暂时只支持phone、tablet设备。<br>- 不允许被其他组件或窗口遮挡。|
|AI识图|- 支持的文本语种类型：简体中文、繁体中文、英文、维吾尔文、藏文。<br>- 支持图片最小规格100*100分辨率。<br>- 分析图像要求是静态非矢量图，即svg、gif等图像类型不支持分析，支持传入[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)进行分析，目前仅支持[RGBA_8888](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-e#pixelmapformat7)类型。<br>- 支持翻译的图片宽高最小比例为1:3（高度小于宽度的3倍），支持文本识别的图片宽高最小比例为1:7（高度小于宽度的7倍）。<br>- 支持的设备情况请参见[约束与限制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-imageanalyzer#section2020122517405)。|

## 模拟器支持情况

本kit暂不支持模拟器。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-kit-guide "Vision Kit（场景化视觉服务）")
# 人脸活体检测

更新时间: 2025-12-16 16:27

## 场景介绍

人脸活体检测支持动作活体检测模式。

动作活体检测支持实时捕捉人脸，需要用户配合做指定动作就可以判断是真实活体，还是非活体攻击（比如：打印图片、人脸翻拍视频以及人脸面具等）。

注意

活体检测是一项纯端侧算法、试用期免费的系统基础服务，推荐开发者使用在考勤打卡、辅助登录和实名认证等低危业务场景中。

端侧算法在HarmonyOS NEXT/5.0.x已完成权威机构（CFCA）检测认证。鉴于支付和金融应用的高风险性，建议开发者基于现有的安全性，针对不同的功能场景进行风险评估和风控策略评估，并采取必要的安全措施。

**图1** 权威认证**增强级**检测报告  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162747.08153058506732242218850520175855:50001231000000:2800:4E42E5ECCAA3AEC4FA161944071FF8F3DA52609180923AB9A024D86A593E9E1B.png "点击放大")

**图2** 活体检测示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162747.06731897092860592271151877672823:50001231000000:2800:F34D314644EC33725648231171168D9A77D756F653731E3626660425352AC79B.png "点击放大")

## 约束与限制

- 平板仅支持竖屏检测，大折叠屏仅支持折叠时使用，小折叠屏仅支持展开时使用。
- 支持的文本语种类型：简体中文、繁体中文、英文、维吾尔文、藏文。
- 支持的播报语种类型：简体中文、英文。
- 人脸活体检测服务暂不支持横屏、分屏进行检测。

## 接口说明

以下仅列出demo中调用的部分主要接口，具体API说明详见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-interactive-liveness)。

|接口名|描述|
|:--|:--|
|[startLivenessDetection](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-interactive-liveness#section68501963545)(config: InteractiveLivenessConfig): Promise<boolean>;|跳转到人脸活体检测页面的入口|
|[getInteractiveLivenessResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-interactive-liveness#section19136935154313)(): Promise<InteractiveLivenessResult>|获取人脸活体检测的结果。使用Promise异步回调|

## 开发步骤

1. 将实现人脸活体检测相关的类添加至工程。
    
    1. import { common, abilityAccessCtrl, Permissions } from '@kit.AbilityKit';
    2. import { interactiveLiveness } from '@kit.VisionKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 在module.json5文件中添加CAMERA权限，其中reason，abilities标签必填，配置方式参见[requestPermissions标签说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。
    
    1. "requestPermissions":[
    2.   {
    3.     "name": "ohos.permission.CAMERA",
    4.     "reason": "$string:camera_desc",
    5.     "usedScene": {"abilities": []}
    6.   }
    7. ]
    
3. 简单配置页面的布局，选择人脸活体检测验证完后的跳转模式。如果使用back跳转模式，表示人脸活体检测完成后返回到上一页。如果使用replace跳转模式，表示人脸活体检测完跳转到成功或失败页面。默认选择的是replace跳转模式。
    
    1. Flex({ direction: FlexDirection.Row, justifyContent: FlexAlign.Start, alignItems: ItemAlign.Center }) {
    2.   Text("验证完的跳转模式：")
    3.     .fontSize(18)
    4.     .width("25%")
    5.   Flex({ direction: FlexDirection.Row, justifyContent: FlexAlign.Start, alignItems: ItemAlign.Center }) {
    6.     Row() {
    7.       Radio({ value: "replace", group: "routeMode" }).checked(true)
    8.         .height(24)
    9.         .width(24)
    10.         .onChange((isChecked: boolean) => {
    11.           this.routeMode = "replace"
    12.         })
    13.       Text("replace")
    14.         .fontSize(16)
    15.     }
    16.     .margin({ right: 15 })
    
    17.     Row() {
    18.       Radio({ value: "back", group: "routeMode" }).checked(false)
    19.         .height(24)
    20.         .width(24)
    21.         .onChange((isChecked: boolean) => {
    22.           this.routeMode = "back";
    23.         })
    24.       Text("back")
    25.         .fontSize(16)
    26.     }
    27.   }
    28.   .width("75%")
    29. }
    
4. 如果选择动作活体模式，可填写验证的动作个数。
    
    1. Flex({ direction: FlexDirection.Row, justifyContent: FlexAlign.Start, alignItems: ItemAlign.Center }) {
    2.   Text("动作数量：")
    3.     .fontSize(18)
    4.     .width("25%")
    5.   TextInput({
    6.     placeholder: this.actionsNum != 0 ? this.actionsNum.toString() : "动作数量为3或4个"
    7.   })
    8.     .type(InputType.Number)
    9.     .placeholderFont({
    10.       size: 18,
    11.       weight: FontWeight.Normal,
    12.       family: "HarmonyHeiTi",
    13.       style: FontStyle.Normal
    14.     })
    15.     .fontSize(18)
    16.     .fontWeight(FontWeight.Bold)
    17.     .fontFamily("HarmonyHeiTi")
    18.     .fontStyle(FontStyle.Normal)
    19.     .width("65%")
    20.     .onChange((value: string) => {
    21.       this.actionsNum = Number(value) as interactiveLiveness.ActionsNumber;
    22.     })
    23. }
    
5. 点击“开始检测“按钮，触发点击事件。
    
    1. Button("开始检测", { type: ButtonType.Normal, stateEffect: true })
    2.   .width(192)
    3.   .height(40)
    4.   .fontSize(16)
    5.   .backgroundColor(0x317aff)
    6.   .borderRadius(20)
    7.   .margin({
    8.     bottom: 56
    9.   })
    10.   .onClick(() => {
    11.     this.startDetection();
    12.   })
    
6. 触发CAMERA权限校验。
    
    1. private context: common.UIAbilityContext = this.getUIContext()?.getHostContext() as common.UIAbilityContext;
    2. private array: Array<Permissions> = ["ohos.permission.CAMERA"];
    3. // 校验CAMERA权限
    4. private startDetection() {
    5.   abilityAccessCtrl.createAtManager().requestPermissionsFromUser(this.context, this.array).then((res) => {
    6.     for (let i = 0; i < res.permissions.length; i++) {
    7.       if (res.permissions[i] === "ohos.permission.CAMERA" && res.authResults[i] === 0) {
    8.         this.routerLibrary();
    9.       }
    10.     }
    11.   }).catch((err: BusinessError) => {
    12.     hilog.error(0x0001, "LivenessCollectionIndex", `Failed to request permissions from user. Code is ${err.code}, message is ${err.message}`);
    13.   })
    14. }
    
7. 配置人脸活体检测控件的配置项[InteractiveLivenessConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-interactive-liveness#section16532153115517)，用于跳转到人脸活体检测控件。
    
    配置中具体的参数可参考[API文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-interactive-liveness)。
    
    1. let routerOptions: interactiveLiveness.InteractiveLivenessConfig = {
    2.   isSilentMode: this.isSilentMode as interactiveLiveness.DetectionMode,
    3.   routeMode: this.routeMode as interactiveLiveness.RouteRedirectionMode,
    4.   actionsNum: this.actionsNum
    5. };
    
8. 调用interactiveLiveness的[startLivenessDetection](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-interactive-liveness#section68501963545)接口，判断跳转到人脸活体检测控件是否成功。
    
    1. // 跳转到人脸活体检测控件
    2. private routerLibrary() {
    3.   if (canIUse("SystemCapability.AI.Component.LivenessDetect")) {
    4.     interactiveLiveness.startLivenessDetection(routerOptions).then((DetectState: boolean) => {
    5.       hilog.info(0x0001, "LivenessCollectionIndex", `Succeeded in jumping.`);
    6.     }).catch((err: BusinessError) => {
    7.       hilog.error(0x0001, "LivenessCollectionIndex", `Failed to jump. Code：${err.code}，message：${err.message}`);
    8.     })
    9.   } else {
    10.     hilog.error(0x0001, "LivenessCollectionIndex", 'this api is not supported on this device');
    11.   }
    12. }
    
9. 检测结束后回到当前界面，可调用interactiveLiveness的[getInteractiveLivenessResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-interactive-liveness#section19136935154313)接口，验证人脸活体检测的结果。
    
    1. // 获取验证结果
    2. private getDetectionResultInfo() {
    3.   // getInteractiveLivenessResult接口调用完会释放资源
    4.   if (canIUse("SystemCapability.AI.Component.LivenessDetect")) {
    5.     let resultInfo = interactiveLiveness.getInteractiveLivenessResult();
    6.     resultInfo.then(data => {
    7.       this.resultInfo = data;
    8.     }).catch((err: BusinessError) => {
    9.       this.failResult = {
    10.         "code": err.code,
    11.         "message": err.message
    12.       }
    13.     })
    14.   } else {
    15.     hilog.error(0x0001, "LivenessCollectionIndex", 'this api is not supported on this device');
    16.   }
    17. }
    

## 开发实例

### Index.ets

1. import { common, abilityAccessCtrl, Permissions } from '@kit.AbilityKit';
2. import { interactiveLiveness } from '@kit.VisionKit';
3. import { BusinessError } from '@kit.BasicServicesKit';
4. import { hilog } from '@kit.PerformanceAnalysisKit';

5. @Entry
6. @Component
7. struct LivenessCollectionIndex{
8.   private context: common.UIAbilityContext = this.getUIContext().getHostContext() as common.UIAbilityContext;
9.   private array: Array<Permissions> = ["ohos.permission.CAMERA"];
10.   @State actionsNum: number = 0;
11.   @State isSilentMode: string = "INTERACTIVE_MODE";
12.   @State routeMode: string = "replace";
13.   @State resultInfo: interactiveLiveness.InteractiveLivenessResult = {
14.     livenessType: 0
15.   };
16.   @State failResult: Record<string, number | string> = {
17.     "code": 1008302000,
18.     "message": ""
19.   };

20.   build() {
21.     Stack({
22.       alignContent: Alignment.Top
23.     }) {
24.       Column() {
25.         Row() {
26.           Flex({ direction: FlexDirection.Row, justifyContent: FlexAlign.Start, alignItems: ItemAlign.Center }) {
27.             Text("验证完的跳转模式：")
28.               .fontSize(18)
29.               .width("25%")
30.             Flex({ direction: FlexDirection.Row, justifyContent: FlexAlign.Start, alignItems: ItemAlign.Center }) {
31.               Row() {
32.                 Radio({ value: "replace", group: "routeMode" }).checked(true)
33.                   .height(24)
34.                   .width(24)
35.                   .onChange(() => {
36.                     this.routeMode = "replace"
37.                   })
38.                 Text("replace")
39.                   .fontSize(16)
40.               }
41.               .margin({ right: 15 })

42.               Row() {
43.                 Radio({ value: "back", group: "routeMode" }).checked(false)
44.                   .height(24)
45.                   .width(24)
46.                   .onChange(() => {
47.                     this.routeMode = "back";
48.                   })
49.                 Text("back")
50.                   .fontSize(16)
51.               }
52.             }
53.             .width("75%")
54.           }
55.         }
56.         .margin({ bottom: 30 })

57.           Row() {
58.             Flex({ direction: FlexDirection.Row, justifyContent: FlexAlign.Start, alignItems: ItemAlign.Center }) {
59.               Text("动作数量：")
60.                 .fontSize(18)
61.                 .width("25%")
62.               TextInput({
63.                 placeholder: this.actionsNum != 0 ? this.actionsNum.toString() : "动作数量为3或4个"
64.               })
65.                 .type(InputType.Number)
66.                 .placeholderFont({
67.                   size: 18,
68.                   weight: FontWeight.Normal,
69.                   family: "HarmonyHeiTi",
70.                   style: FontStyle.Normal
71.                 })
72.                 .fontSize(18)
73.                 .fontWeight(FontWeight.Bold)
74.                 .fontFamily("HarmonyHeiTi")
75.                 .fontStyle(FontStyle.Normal)
76.                 .width("65%")
77.                 .onChange((value: string) => {
78.                   this.actionsNum = Number(value) as interactiveLiveness.ActionsNumber;
79.                 })
80.             }
81.           }
82.       }
83.       .margin({ left: 24, top: 80 })
84.       .zIndex(1)

85.       Stack({
86.         alignContent: Alignment.Bottom
87.       }) {
88.         if (this.resultInfo?.mPixelMap) {
89.           Image(this.resultInfo?.mPixelMap)
90.             .width(260)
91.             .height(260)
92.             .align(Alignment.Center)
93.             .margin({ bottom: 260 })
94.           Circle()
95.             .width(300)
96.             .height(300)
97.             .fillOpacity(0)
98.             .strokeWidth(60)
99.             .stroke(Color.White)
100.             .margin({ bottom: 250, left: 0 })
101.         }

102.         Text(this.resultInfo.mPixelMap ?
103.           "检测成功" :
104.           this.failResult.code != 1008302000 ?
105.             "检测失败" :
106.             "")
107.           .width("100%")
108.           .height(26)
109.           .fontSize(20)
110.           .fontColor("#000000")
111.           .fontFamily("HarmonyHeiTi")
112.           .margin({ top: 50 })
113.           .textAlign(TextAlign.Center)
114.           .fontWeight("Medium")
115.           .margin({ bottom: 240 })

116.         if(this.failResult.code != 1008302000) {
117.           Text(this.failResult.message as string)
118.             .width("100%")
119.             .height(26)
120.             .fontSize(16)
121.             .fontColor(Color.Gray)
122.             .textAlign(TextAlign.Center)
123.             .fontFamily("HarmonyHeiTi")
124.             .fontWeight("Medium")
125.             .margin({ bottom: 200 })
126.         }

127.         Button("开始检测", { type: ButtonType.Normal, stateEffect: true })
128.           .width(192)
129.           .height(40)
130.           .fontSize(16)
131.           .backgroundColor(0x317aff)
132.           .borderRadius(20)
133.           .margin({
134.             bottom: 56
135.           })
136.           .onClick(() => {
137.             this.startDetection();
138.           })
139.       }
140.       .height("100%")
141.     }
142.   }

143.   onPageShow() {
144.     this.resultRelease();
145.     this.getDetectionResultInfo();
146.   }

147.   // 跳转到人脸活体检测控件
148.   private routerLibrary() {
149.     let routerOptions: interactiveLiveness.InteractiveLivenessConfig = {
150.       isSilentMode: this.isSilentMode as interactiveLiveness.DetectionMode,
151.       routeMode: this.routeMode as interactiveLiveness.RouteRedirectionMode,
152.       actionsNum: this.actionsNum
153.     }

154.     if (canIUse("SystemCapability.AI.Component.LivenessDetect")) {
155.       interactiveLiveness.startLivenessDetection(routerOptions).then((DetectState: boolean) => {
156.         hilog.info(0x0001, "LivenessCollectionIndex", `Succeeded in jumping.`);
157.       }).catch((err: BusinessError) => {
158.         hilog.error(0x0001, "LivenessCollectionIndex", `Failed to jump. Code：${err.code}，message：${err.message}`);
159.       })
160.     } else {
161.       hilog.error(0x0001, "LivenessCollectionIndex", 'this api is not supported on this device');
162.     }
163.   }

164.   // 校验CAMERA权限
165.   private startDetection() {
166.     abilityAccessCtrl.createAtManager().requestPermissionsFromUser(this.context, this.array).then((res) => {
167.       for (let i = 0; i < res.permissions.length; i++) {
168.         if (res.permissions[i] === "ohos.permission.CAMERA" && res.authResults[i] === 0) {
169.         this.routerLibrary();
170.       }
171.      }
172.     }).catch((err: BusinessError) => {
173.       hilog.error(0x0001, "LivenessCollectionIndex", `Failed to request permissions from user. Code is ${err.code}, message is ${err.message}`);
174.     })
175.   }

176.   // 获取验证结果
177.   private getDetectionResultInfo() {
178.     // getInteractiveLivenessResult接口调用完会释放资源
179.     if (canIUse("SystemCapability.AI.Component.LivenessDetect")) {
180.       interactiveLiveness.getInteractiveLivenessResult().then(data => {
181.         this.resultInfo = data;
182.       }).catch((err: BusinessError) => {
183.         this.failResult = {
184.           "code": err.code,
185.           "message": err.message
186.         }
187.       })
188.     } else {
189.       hilog.error(0x0001, "LivenessCollectionIndex", 'this api is not supported on this device');
190.     }
191.   }

192.   // result release
193.   private resultRelease() {
194.     this.resultInfo = {
195.       livenessType: 0
196.     }
197.     this.failResult = {
198.       "code": 1008302000,
199.       "message": ""
200.     }
201.   }
202. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-introduction "Vision Kit简介")
# 卡证识别

更新时间: 2025-12-16 16:27

从5.1.1(19)开始，[CardRecognition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-card-recognition#section143611912403)接口中的callback参数废弃，请使用onResult代替。

## 场景介绍

卡证识别控件提供身份证（目前仅支持中国大陆二代身份证，且不包含民汉双文身份证）、行驶证、驾驶证、护照、银行卡的结构化识别服务，满足卡证的自动分类功能，系统可自动判断所属卡证类型并返回结构化信息和卡证图片信息。

对于需要填充卡证信息的场景，如身份证、银行卡信息等，可使用卡证识别控件读取OCR（Optical Character Recognition）信息，将结果信息返回后进行填充。支持单独识别正面、反面，或同时进行双面识别。

**图1** 银行卡识别示意图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162748.13469380655189781268947624313441:50001231000000:2800:D364AC7DAC3266480EEFAC0FBE7DFFF7785BA5DFCEA8ABBF7EECB8A353E4A289.png "点击放大")

## 约束与限制

- 支持的语种类型：简体中文、英文。
- 卡证识别暂时只支持身份证、行驶证、驾驶证、护照、银行卡5种卡证。
- 不允许被其他组件或窗口遮挡。

## 接口说明

以下仅列出demo中调用的部分主要接口，具体API说明详见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-card-recognition)。

|接口名|描述|
|:--|:--|
|[CardRecognition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-card-recognition#section143611912403)|卡证识别控件|
|[CardRecognitionResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-card-recognition#section161551745133610)|卡证识别结果|

## 开发步骤

1. 将卡证识别控件相关的类添加至工程。
    
    1. import { CardRecognition, CardRecognitionResult, CardType, CardSide, CardRecognitionConfig, ShootingMode, CardContentConfig, BankCardConfig } from "@kit.VisionKit";
    
2. 配置页面的布局，选择需要识别的卡证类型和需要识别的卡证页面，配置对应设置项，在回调中获取结果返回值。
    
    以下分别为身份证、银行卡、护照、驾驶证和行驶证的示例代码。
    
    1. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    2. const TAG = 'CardRecognition'
    
    3. @Entry
    4. @Component
    5. struct Index {
    6.   build() {
    7.     Column() {
    8.       // 身份证
    9.       CardRecognition({
    10.         supportType: CardType.CARD_ID,
    11.         // 身份证可双面识别
    12.         cardSide: CardSide.DEFAULT,
    13.         cardRecognitionConfig: {
    14.           defaultShootingMode: ShootingMode.MANUAL,
    15.           isPhotoSelectionSupported: true
    16.         },
    17.         onResult: ((params: CardRecognitionResult) => {
    18.           hilog.info(0x0001, TAG, `params code: ${params.code}`)
    19.           hilog.info(0x0001, TAG, `params cardType: ${params.cardType}`)
    20.           hilog.info(0x0001, TAG, `params cardInfo front: ${JSON.stringify(params.cardInfo?.front)}`)
    21.           hilog.info(0x0001, TAG, `params cardInfo back: ${JSON.stringify(params.cardInfo?.back)}`)
    22.         })
    23.       })
    24.     }
    25.     .height('100%')
    26.     .width('100%')
    27.   }
    28. }
    
    29. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    30. const TAG = 'CardRecognition'
    
    31. @Entry
    32. @Component
    33. struct Index {
    34.   build() {
    35.     Column() {
    36.       // 银行卡
    37.       CardRecognition({
    38.         supportType: CardType.CARD_BANK,
    39.         // 银行卡为单面识别
    40.         cardSide: CardSide.FRONT,
    41.         cardRecognitionConfig: {
    42.           defaultShootingMode: ShootingMode.MANUAL,
    43.           isPhotoSelectionSupported: true,
    44.           cardContentConfig: { bankCard: { isBankNumberDialogShown: true} }
    45.         },
    46.         onResult: ((params: CardRecognitionResult) => {
    47.           hilog.info(0x0001, TAG, `params code: ${params.code}`)
    48.           hilog.info(0x0001, TAG, `params cardType: ${params.cardType}`)
    49.           hilog.info(0x0001, TAG, `params cardInfo: ${JSON.stringify(params.cardInfo?.main)}`)
    50.         })})
    51.     }
    52.     .height('100%')
    53.     .width('100%')
    54.   }
    55. }
    
    56. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    57. const TAG = 'CardRecognition'
    
    58. @Entry
    59. @Component
    60. struct Index {
    61.   build() {
    62.     Column() {
    63.       // 护照
    64.       CardRecognition({
    65.         supportType: CardType.CARD_PASSPORT,
    66.         // 护照为单面识别
    67.         cardSide: CardSide.FRONT,
    68.         cardRecognitionConfig: {
    69.           defaultShootingMode: ShootingMode.MANUAL,
    70.           isPhotoSelectionSupported: true
    71.         },
    72.         onResult: ((params: CardRecognitionResult) => {
    73.           hilog.info(0x0001, TAG, `params code: ${params.code}`)
    74.           hilog.info(0x0001, TAG, `params cardType: ${params.cardType}`)
    75.           hilog.info(0x0001, TAG, `params cardInfo: ${JSON.stringify(params.cardInfo?.main)}`)
    76.         })})
    77.     }
    78.     .height('100%')
    79.     .width('100%')
    80.   }
    81. }
    
    82. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    83. const TAG = 'CardRecognition'
    
    84. @Entry
    85. @Component
    86. struct Index {
    87.   build() {
    88.     Column() {
    89.       // 驾驶证
    90.       CardRecognition({
    91.         supportType: CardType.CARD_DRIVER_LICENSE,
    92.         // 驾驶证可双面识别
    93.         cardSide: CardSide.DEFAULT,
    94.         cardRecognitionConfig: {
    95.           defaultShootingMode: ShootingMode.MANUAL,
    96.           isPhotoSelectionSupported: true
    97.         },
    98.         onResult: ((params: CardRecognitionResult) => {
    99.           hilog.info(0x0001, TAG, `params code: ${params.code}`)
    100.           hilog.info(0x0001, TAG, `params cardType: ${params.cardType}`)
    101.           hilog.info(0x0001, TAG, `params cardInfo front: ${JSON.stringify(params.cardInfo?.front)}`)
    102.           hilog.info(0x0001, TAG, `params cardInfo back: ${JSON.stringify(params.cardInfo?.back)}`)
    103.         })
    104.       })
    105.     }
    106.     .height('100%')
    107.     .width('100%')
    108.   }
    109. }
    
    110. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    111. const TAG = 'CardRecognition'
    
    112. @Entry
    113. @Component
    114. struct Index {
    115.   build() {
    116.     Column() {
    117.       // 行驶证
    118.       CardRecognition({
    119.         supportType: CardType.CARD_VEHICLE_LICENSE,
    120.         // 行驶证可双面识别
    121.         cardSide: CardSide.DEFAULT,
    122.         cardRecognitionConfig: {
    123.           defaultShootingMode: ShootingMode.MANUAL,
    124.           isPhotoSelectionSupported: true
    125.         },
    126.         onResult: ((params: CardRecognitionResult) => {
    127.           hilog.info(0x0001, TAG, `params code: ${params.code}`)
    128.           hilog.info(0x0001, TAG, `params cardType: ${params.cardType}`)
    129.           hilog.info(0x0001, TAG, `params cardInfo front: ${JSON.stringify(params.cardInfo?.front)}`)
    130.           hilog.info(0x0001, TAG, `params cardInfo back: ${JSON.stringify(params.cardInfo?.back)}`)
    131.         })
    132.       })
    133.     }
    134.     .height('100%')
    135.     .width('100%')
    136.   }
    137. }
    

## 开发实例

### Index.ets

1. // 卡证识别开发实例分两页实现，一页为卡证识别入口页，一页为卡证识别实现页
2. // 卡证识别入口页，需引入卡证识别实现页，以下文实例为例，实现页文件名为CardDemoPage
3. import { CardDemoPage } from './CardDemoPage'

4. @Entry
5. @Component
6. struct MainPage {
7.   @Provide('pathStack') pathStack: NavPathStack = new NavPathStack()

8.   @Builder
9.   PageMap(name: string) {
10.     if (name === 'cardRecognition') {
11.       CardDemoPage()
12.     }
13.   }

14.   // 卡证识别入口按钮
15.   build() {
16.     Navigation(this.pathStack) {
17.       Button('CardRecognition', { stateEffect: true, type: ButtonType.Capsule })
18.         .width('50%')
19.         .height(40)
20.         .onClick(() => {
21.           this.pathStack.pushPath({ name: 'cardRecognition' })
22.         })
23.     }.title('卡证识别控件demo').navDestination(this.PageMap)
24.     .mode(NavigationMode.Stack)
25.   }
26. }

### CardDemoPage.ets

1. // 卡证识别实现页，文件名为CardDemoPage，需被引入至入口页
2. import { CardRecognition, CardRecognitionResult, CardType, CardSide, ShootingMode } from "@kit.VisionKit"
3. import { hilog } from '@kit.PerformanceAnalysisKit';

4. const TAG: string = 'CardRecognitionPage'

5. // 卡证识别页，用于加载uiExtensionAbility
6. @Component
7. export struct CardDemoPage {
8.   @State cardDataSource: Record<string, string>[] = []
9.   @Consume('pathStack') pathStack: NavPathStack

10.   build() {
11.     NavDestination() {
12.       Stack({ alignContent: Alignment.Top }) {
13.         Stack() {
14.           this.cardDataShowBuilder()
15.         }
16.         .width('80%')
17.         .height('80%')

18.         CardRecognition({
19.           // 此处选择身份证类型作为示例
20.           supportType: CardType.CARD_ID,
21.           cardSide: CardSide.DEFAULT,
22.           cardRecognitionConfig: {
23.             defaultShootingMode: ShootingMode.MANUAL,
24.             isPhotoSelectionSupported: true
25.           },
26.           onResult: ((params: CardRecognitionResult) => {
27.             hilog.info(0x0001, TAG, `params code: ${params.code}`)
28.             if (params.code !== 200) {
29.               this.pathStack.pop()
30.             }
31.             hilog.info(0x0001, TAG, `params cardType: ${params.cardType}`)
32.             if (params.cardInfo?.front !== undefined) {
33.               this.cardDataSource.push(params.cardInfo?.front)
34.             }

35.             if (params.cardInfo?.back !== undefined) {
36.               this.cardDataSource.push(params.cardInfo?.back)
37.             }

38.             if (params.cardInfo?.main !== undefined) {
39.               this.cardDataSource.push(params.cardInfo?.main)
40.             }
41.             hilog.info(0x0001, TAG, `params cardInfo front: ${JSON.stringify(params.cardInfo?.front)}`)
42.             hilog.info(0x0001, TAG, `params cardInfo back: ${JSON.stringify(params.cardInfo?.back)}`)
43.           })
44.         })
45.       }
46.       .width('100%')
47.       .height('100%')
48.     }
49.     .width('100%')
50.     .height('100%')
51.     .hideTitleBar(true)
52.   }

53.   @Builder
54.   cardDataShowBuilder() {
55.     List() {
56.       ForEach(this.cardDataSource, (cardData: Record<string, string>) => {
57.         ListItem() {
58.           Column() {
59.             Image(cardData.cardImageUri)
60.               .objectFit(ImageFit.Contain)
61.               .width(100)
62.               .height(100)

63.             Text(JSON.stringify(cardData))
64.               .width('100%')
65.               .fontSize(12)
66.           }
67.         }
68.       })
69.     }
70.     .listDirection(Axis.Vertical)
71.     .alignListItem(ListItemAlign.Center)
72.     .margin({
73.       top: 50
74.     })
75.     .width('100%')
76.     .height('100%')
77.   }
78. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-interactiveliveness "人脸活体检测")
# AI识图

更新时间: 2025-12-16 16:27

## 场景介绍

AI识图是通过聚合OCR（Optical Character Recognition）、主体分割、实体识别、多目标识别等AI能力，提供场景化的文本识别、主体分割、识图搜索功能。AI识图功能主开关入口在基础控件API列表中，如果您接受AI识图默认的交互和功能，仅需使用基础控件提供的相关使能接口打开功能开关即可。该文档配套的API配合基础控件使用，主要满足您的定制诉求，帮助您完成AI识图功能交互上的细粒度控制，获取文本识别、图像分割等分析结果以便您进行扩展业务的开发，目前支持的基础控件范围包括[Image](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-image#enableanalyzer11)、[Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video#enableanalyzer12)、[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent#enableanalyzer12)。其中，配合Image控件可完成静态图片上的识图功能，配合Video控件可完成视频播放暂停帧的识图功能，配合XComponent可完成自定义渲染等场景下的图像的识图功能。

识图功能提供如下能力：

- 识别文字。
    
    用户长按文本选取文字或持续长按文本中的电话号码、邮箱、网址、地址、时间等实体，可触发对应实体的快捷操作，如持续长按文本中的时间，可触发"新建日程"快捷操作入口。
    
- 识图搜索。
    
    用户抠图后可基于抠出的主体进行识图搜索，开发者也可以主动触发目标标识，触发后会识别图中的动物、植物、建筑物等目标并用相应的ICON标识，用户点击ICON也可以进行识图搜索，搜索结果会以模态窗的方式为用户呈现。
    
- 主体分割。
    
    用户长按主体分割，分割后用户可以完成复制，分享，全选，识图搜索等功能。
    
- AIButton。
    
    AIButton承载了电话号码、邮箱、网址、地址、时间等实体的显性下划线标识（点击后出现快捷操作菜单），原图翻译（系统设置语种与图片上文本语种不一致且能将图中文本翻译为系统当前设置的语种时出现），表格提取（图片中存在表格时出现）等功能特性。配置AIButton属性可见后，会对图片进行预分析，当图片中存在文本且文本区域大于图片区域的5%时AIButton才会显示。
    

识图功能提供如下建议：

- AI识图特性可帮助消费者从图片上获取更多的信息（长按抠图，长按选取文本，长按实体识别等）。建议在大图预览场景都打开此能力，大图预览场景下用户对图片中的内容会更感兴趣，此时适时的提供识图服务契合用户体验场景，同时为用户提供最佳的识图交互体验。
- AI识图特性中的AIButton与图片中是否有文本存在关联，显性的提醒用户操作文本。开启AIButton会触发图片的预分析从而导致一定的功耗开销，建议开发者充分理解自身业务场景，预估目标用户图片内容分布，兼顾用户图片浏览体验和提供更高阶AI识图功能体验的情况下按需提供AIButton露出。例如，业务本身是辅助用户高效提取图片中的文本内容，开启AIButton将会提升用户文本提取的体验。业务本身更偏向于图片编辑，也可隐藏AIButton。

**图1** AI识图示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162749.19315385489373374942173618742941:50001231000000:2800:C5D70BDBB1D22658357FD591617E8222ABEA45FACE91B751B78710287C783D1F.png "点击放大")

## 约束与限制

- 支持的文本语种类型：简体中文、繁体中文、英文、维吾尔文、藏文。
- 支持图片最小规格100*100分辨率。
- 分析图像要求是静态非矢量图，即svg、gif等图像类型不支持分析，支持传入[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)进行分析，目前仅支持[RGBA_8888](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-e#pixelmapformat7)类型。
- 支持翻译的图片宽高最小比例为1:3（高度小于宽度的3倍），支持文本识别的图片宽高最小比例为1:7（高度小于宽度的7倍）。
- 当前设备支持本能力可以通过[getImageAnalyzerSupportTypes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-image-common#getimageanalyzersupporttypes12)进行判断。
    
    日志返回格式为“SupportTypes: [_主体识别功能枚举值_,_文字识别功能枚举值_,_对象查找功能枚举值_]”，具体枚举值可参见[ImageAnalyzerType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-image-common#imageanalyzertype12)。
    
    若返回“SupportTypes: []”，则说明当前设备不支持AI识图能力；若返回其他值，则说明当前设备支持AI识图能力。
    
    1. import { visionImageAnalyzer } from '@kit.VisionKit';
    
    2. @Entry
    3. @Component
    4. struct Index {
    5.   private aiController: visionImageAnalyzer.VisionImageAnalyzerController = new visionImageAnalyzer.VisionImageAnalyzerController()
    
    6.   build() {
    7.     Row() {
    8.       Button('getTypes')
    9.         .onClick(() => {
    10.           let SupportTypes = this.aiController.getImageAnalyzerSupportTypes()
    11.           console.info(`SupportTypes: ${JSON.stringify(SupportTypes)}`)
    12.         })
    13.     }
    14.   }
    15. }
    

## 开发步骤

1. 将AI识图控件相关的类添加。
    
    1. import { visionImageAnalyzer } from '@kit.VisionKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 初始化[VisionImageAnalyzerController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-image-analyzer#section37192953318)对象。
    
    1. private visionImageAnalyzerController: visionImageAnalyzer.VisionImageAnalyzerController = new visionImageAnalyzer.VisionImageAnalyzerController();
    
3. 添加订阅事件。
    
    1. aboutToAppear(): void {
    2.   this.visionImageAnalyzerController.on('imageAnalyzerVisibilityChange', (visibility: visionImageAnalyzer.ImageAnalyzerVisibility) => {
    3.     console.info("DEMO_TAG", `imageAnalyzerVisibilityChange result: ${JSON.stringify(visibility)}`)
    4.   })
    5.   this.visionImageAnalyzerController.on('textAnalysis', (text: string) => {
    6.     console.info("DEMO_TAG", `textAnalysis result: ${JSON.stringify(text)}`)
    7.   })
    8.   this.visionImageAnalyzerController.on('selectedTextChange', (selectedText: string) => {
    9.     console.info("DEMO_TAG", `selectedTextChange result: ${JSON.stringify(selectedText)}`)
    10.   })
    11.   this.visionImageAnalyzerController.on('subjectAnalysis', (subjects: visionImageAnalyzer.Subject[]) => {
    12.     console.info("DEMO_TAG", `subjectAnalysis result: ${JSON.stringify(subjects)}`)
    13.   })
    14.   this.visionImageAnalyzerController.on('selectedSubjectsChange', (subjects: visionImageAnalyzer.Subject[]) => {
    15.     console.info("DEMO_TAG", `selectedSubjectsChange result: ${JSON.stringify(subjects)}`)
    16.   })
    17.   this.visionImageAnalyzerController.on('analyzerFailed', (error: BusinessError) => {
    18.     console.error("DEMO_TAG", `analyzerFailed result: ${JSON.stringify(error)}`)
    19.   })
    20. }
    
4. 绑定[VisionImageAnalyzerController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-image-analyzer#section37192953318)对象，可以控制识图相关的交互。
    
    1. build() {
    2.   Stack() {
    3.     // 需要替换您自己的资源图片，存放在resources/base/media目录下
    4.     Image($r('app.media.img'), {
    5.       types: [ImageAnalyzerType.TEXT, ImageAnalyzerType.SUBJECT, ImageAnalyzerType.OBJECT_LOOKUP],
    6.       aiController: this.visionImageAnalyzerController
    7.     })
    8.       .width('100%')
    9.       .height('100%')
    10.       .enableAnalyzer(true)
    11.       .objectFit(ImageFit.Contain)
    12.   }.width('100%').height('100%')
    13. }
    
5. 取消订阅事件。
    
    1. aboutToDisappear(): void {
    2.   this.visionImageAnalyzerController.off('imageAnalyzerVisibilityChange')
    3.   this.visionImageAnalyzerController.off('textAnalysis')
    4.   this.visionImageAnalyzerController.off('selectedTextChange')
    5.   this.visionImageAnalyzerController.off('subjectAnalysis')
    6.   this.visionImageAnalyzerController.off('selectedSubjectsChange')
    7.   this.visionImageAnalyzerController.off('analyzerFailed')
    8. }
    

## 开发实例

### Index.ets

1. import { visionImageAnalyzer } from '@kit.VisionKit';
2. import { BusinessError } from '@kit.BasicServicesKit'
3. @Entry
4. @Component
5. struct ImageDemo {
6.   private visionImageAnalyzerController: visionImageAnalyzer.VisionImageAnalyzerController = new visionImageAnalyzer.VisionImageAnalyzerController()
7.   aboutToAppear(): void {
8.     this.visionImageAnalyzerController.on('imageAnalyzerVisibilityChange', (visibility: visionImageAnalyzer.ImageAnalyzerVisibility) => {
9.       console.info("DEMO_TAG", `imageAnalyzerVisibilityChange result: ${JSON.stringify(visibility)}`)
10.     })
11.     this.visionImageAnalyzerController.on('textAnalysis', (text: string) => {
12.       console.info("DEMO_TAG", `textAnalysis result: ${JSON.stringify(text)}`)
13.     })
14.     this.visionImageAnalyzerController.on('selectedTextChange', (selectedText: string) => {
15.       console.info("DEMO_TAG", `selectedTextChange result: ${JSON.stringify(selectedText)}`)
16.     })
17.     this.visionImageAnalyzerController.on('subjectAnalysis', (subjects: visionImageAnalyzer.Subject[]) => {
18.       console.info("DEMO_TAG", `subjectAnalysis result: ${JSON.stringify(subjects)}`)
19.     })
20.     this.visionImageAnalyzerController.on('selectedSubjectsChange', (subjects: visionImageAnalyzer.Subject[]) => {
21.       console.info("DEMO_TAG", `selectedSubjectsChange result: ${JSON.stringify(subjects)}`)
22.     })
23.     this.visionImageAnalyzerController.on('analyzerFailed', (error: BusinessError) => {
24.       console.error("DEMO_TAG", `analyzerFailed result: ${JSON.stringify(error)}`)
25.     })
26.   }
27.   build() {
28.     Stack() {
29.       Image($r('app.media.img'), {
30.         types: [ImageAnalyzerType.TEXT, ImageAnalyzerType.SUBJECT, ImageAnalyzerType.OBJECT_LOOKUP],
31.         aiController: this.visionImageAnalyzerController
32.       })
33.         .width('100%')
34.         .height('100%')
35.         .enableAnalyzer(true)
36.         .objectFit(ImageFit.Contain)
37.     }.width('100%').height('100%')
38.   }
39.     aboutToDisappear(): void {
40.       this.visionImageAnalyzerController.off('imageAnalyzerVisibilityChange')
41.       this.visionImageAnalyzerController.off('textAnalysis')
42.       this.visionImageAnalyzerController.off('selectedTextChange')
43.       this.visionImageAnalyzerController.off('subjectAnalysis')
44.       this.visionImageAnalyzerController.off('selectedSubjectsChange')
45.       this.visionImageAnalyzerController.off('analyzerFailed')
46.     }
47. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-documentscanner "文档扫描")
# AI识图

更新时间: 2025-12-16 16:27

## 场景介绍

AI识图是通过聚合OCR（Optical Character Recognition）、主体分割、实体识别、多目标识别等AI能力，提供场景化的文本识别、主体分割、识图搜索功能。AI识图功能主开关入口在基础控件API列表中，如果您接受AI识图默认的交互和功能，仅需使用基础控件提供的相关使能接口打开功能开关即可。该文档配套的API配合基础控件使用，主要满足您的定制诉求，帮助您完成AI识图功能交互上的细粒度控制，获取文本识别、图像分割等分析结果以便您进行扩展业务的开发，目前支持的基础控件范围包括[Image](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-image#enableanalyzer11)、[Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video#enableanalyzer12)、[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent#enableanalyzer12)。其中，配合Image控件可完成静态图片上的识图功能，配合Video控件可完成视频播放暂停帧的识图功能，配合XComponent可完成自定义渲染等场景下的图像的识图功能。

识图功能提供如下能力：

- 识别文字。
    
    用户长按文本选取文字或持续长按文本中的电话号码、邮箱、网址、地址、时间等实体，可触发对应实体的快捷操作，如持续长按文本中的时间，可触发"新建日程"快捷操作入口。
    
- 识图搜索。
    
    用户抠图后可基于抠出的主体进行识图搜索，开发者也可以主动触发目标标识，触发后会识别图中的动物、植物、建筑物等目标并用相应的ICON标识，用户点击ICON也可以进行识图搜索，搜索结果会以模态窗的方式为用户呈现。
    
- 主体分割。
    
    用户长按主体分割，分割后用户可以完成复制，分享，全选，识图搜索等功能。
    
- AIButton。
    
    AIButton承载了电话号码、邮箱、网址、地址、时间等实体的显性下划线标识（点击后出现快捷操作菜单），原图翻译（系统设置语种与图片上文本语种不一致且能将图中文本翻译为系统当前设置的语种时出现），表格提取（图片中存在表格时出现）等功能特性。配置AIButton属性可见后，会对图片进行预分析，当图片中存在文本且文本区域大于图片区域的5%时AIButton才会显示。
    

识图功能提供如下建议：

- AI识图特性可帮助消费者从图片上获取更多的信息（长按抠图，长按选取文本，长按实体识别等）。建议在大图预览场景都打开此能力，大图预览场景下用户对图片中的内容会更感兴趣，此时适时的提供识图服务契合用户体验场景，同时为用户提供最佳的识图交互体验。
- AI识图特性中的AIButton与图片中是否有文本存在关联，显性的提醒用户操作文本。开启AIButton会触发图片的预分析从而导致一定的功耗开销，建议开发者充分理解自身业务场景，预估目标用户图片内容分布，兼顾用户图片浏览体验和提供更高阶AI识图功能体验的情况下按需提供AIButton露出。例如，业务本身是辅助用户高效提取图片中的文本内容，开启AIButton将会提升用户文本提取的体验。业务本身更偏向于图片编辑，也可隐藏AIButton。

**图1** AI识图示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162749.19315385489373374942173618742941:50001231000000:2800:C5D70BDBB1D22658357FD591617E8222ABEA45FACE91B751B78710287C783D1F.png "点击放大")

## 约束与限制

- 支持的文本语种类型：简体中文、繁体中文、英文、维吾尔文、藏文。
- 支持图片最小规格100*100分辨率。
- 分析图像要求是静态非矢量图，即svg、gif等图像类型不支持分析，支持传入[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)进行分析，目前仅支持[RGBA_8888](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-e#pixelmapformat7)类型。
- 支持翻译的图片宽高最小比例为1:3（高度小于宽度的3倍），支持文本识别的图片宽高最小比例为1:7（高度小于宽度的7倍）。
- 当前设备支持本能力可以通过[getImageAnalyzerSupportTypes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-image-common#getimageanalyzersupporttypes12)进行判断。
    
    日志返回格式为“SupportTypes: [_主体识别功能枚举值_,_文字识别功能枚举值_,_对象查找功能枚举值_]”，具体枚举值可参见[ImageAnalyzerType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-image-common#imageanalyzertype12)。
    
    若返回“SupportTypes: []”，则说明当前设备不支持AI识图能力；若返回其他值，则说明当前设备支持AI识图能力。
    
    1. import { visionImageAnalyzer } from '@kit.VisionKit';
    
    2. @Entry
    3. @Component
    4. struct Index {
    5.   private aiController: visionImageAnalyzer.VisionImageAnalyzerController = new visionImageAnalyzer.VisionImageAnalyzerController()
    
    6.   build() {
    7.     Row() {
    8.       Button('getTypes')
    9.         .onClick(() => {
    10.           let SupportTypes = this.aiController.getImageAnalyzerSupportTypes()
    11.           console.info(`SupportTypes: ${JSON.stringify(SupportTypes)}`)
    12.         })
    13.     }
    14.   }
    15. }
    

## 开发步骤

1. 将AI识图控件相关的类添加。
    
    1. import { visionImageAnalyzer } from '@kit.VisionKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 初始化[VisionImageAnalyzerController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-image-analyzer#section37192953318)对象。
    
    1. private visionImageAnalyzerController: visionImageAnalyzer.VisionImageAnalyzerController = new visionImageAnalyzer.VisionImageAnalyzerController();
    
3. 添加订阅事件。
    
    1. aboutToAppear(): void {
    2.   this.visionImageAnalyzerController.on('imageAnalyzerVisibilityChange', (visibility: visionImageAnalyzer.ImageAnalyzerVisibility) => {
    3.     console.info("DEMO_TAG", `imageAnalyzerVisibilityChange result: ${JSON.stringify(visibility)}`)
    4.   })
    5.   this.visionImageAnalyzerController.on('textAnalysis', (text: string) => {
    6.     console.info("DEMO_TAG", `textAnalysis result: ${JSON.stringify(text)}`)
    7.   })
    8.   this.visionImageAnalyzerController.on('selectedTextChange', (selectedText: string) => {
    9.     console.info("DEMO_TAG", `selectedTextChange result: ${JSON.stringify(selectedText)}`)
    10.   })
    11.   this.visionImageAnalyzerController.on('subjectAnalysis', (subjects: visionImageAnalyzer.Subject[]) => {
    12.     console.info("DEMO_TAG", `subjectAnalysis result: ${JSON.stringify(subjects)}`)
    13.   })
    14.   this.visionImageAnalyzerController.on('selectedSubjectsChange', (subjects: visionImageAnalyzer.Subject[]) => {
    15.     console.info("DEMO_TAG", `selectedSubjectsChange result: ${JSON.stringify(subjects)}`)
    16.   })
    17.   this.visionImageAnalyzerController.on('analyzerFailed', (error: BusinessError) => {
    18.     console.error("DEMO_TAG", `analyzerFailed result: ${JSON.stringify(error)}`)
    19.   })
    20. }
    
4. 绑定[VisionImageAnalyzerController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/vision-image-analyzer#section37192953318)对象，可以控制识图相关的交互。
    
    1. build() {
    2.   Stack() {
    3.     // 需要替换您自己的资源图片，存放在resources/base/media目录下
    4.     Image($r('app.media.img'), {
    5.       types: [ImageAnalyzerType.TEXT, ImageAnalyzerType.SUBJECT, ImageAnalyzerType.OBJECT_LOOKUP],
    6.       aiController: this.visionImageAnalyzerController
    7.     })
    8.       .width('100%')
    9.       .height('100%')
    10.       .enableAnalyzer(true)
    11.       .objectFit(ImageFit.Contain)
    12.   }.width('100%').height('100%')
    13. }
    
5. 取消订阅事件。
    
    1. aboutToDisappear(): void {
    2.   this.visionImageAnalyzerController.off('imageAnalyzerVisibilityChange')
    3.   this.visionImageAnalyzerController.off('textAnalysis')
    4.   this.visionImageAnalyzerController.off('selectedTextChange')
    5.   this.visionImageAnalyzerController.off('subjectAnalysis')
    6.   this.visionImageAnalyzerController.off('selectedSubjectsChange')
    7.   this.visionImageAnalyzerController.off('analyzerFailed')
    8. }
    

## 开发实例

### Index.ets

1. import { visionImageAnalyzer } from '@kit.VisionKit';
2. import { BusinessError } from '@kit.BasicServicesKit'
3. @Entry
4. @Component
5. struct ImageDemo {
6.   private visionImageAnalyzerController: visionImageAnalyzer.VisionImageAnalyzerController = new visionImageAnalyzer.VisionImageAnalyzerController()
7.   aboutToAppear(): void {
8.     this.visionImageAnalyzerController.on('imageAnalyzerVisibilityChange', (visibility: visionImageAnalyzer.ImageAnalyzerVisibility) => {
9.       console.info("DEMO_TAG", `imageAnalyzerVisibilityChange result: ${JSON.stringify(visibility)}`)
10.     })
11.     this.visionImageAnalyzerController.on('textAnalysis', (text: string) => {
12.       console.info("DEMO_TAG", `textAnalysis result: ${JSON.stringify(text)}`)
13.     })
14.     this.visionImageAnalyzerController.on('selectedTextChange', (selectedText: string) => {
15.       console.info("DEMO_TAG", `selectedTextChange result: ${JSON.stringify(selectedText)}`)
16.     })
17.     this.visionImageAnalyzerController.on('subjectAnalysis', (subjects: visionImageAnalyzer.Subject[]) => {
18.       console.info("DEMO_TAG", `subjectAnalysis result: ${JSON.stringify(subjects)}`)
19.     })
20.     this.visionImageAnalyzerController.on('selectedSubjectsChange', (subjects: visionImageAnalyzer.Subject[]) => {
21.       console.info("DEMO_TAG", `selectedSubjectsChange result: ${JSON.stringify(subjects)}`)
22.     })
23.     this.visionImageAnalyzerController.on('analyzerFailed', (error: BusinessError) => {
24.       console.error("DEMO_TAG", `analyzerFailed result: ${JSON.stringify(error)}`)
25.     })
26.   }
27.   build() {
28.     Stack() {
29.       Image($r('app.media.img'), {
30.         types: [ImageAnalyzerType.TEXT, ImageAnalyzerType.SUBJECT, ImageAnalyzerType.OBJECT_LOOKUP],
31.         aiController: this.visionImageAnalyzerController
32.       })
33.         .width('100%')
34.         .height('100%')
35.         .enableAnalyzer(true)
36.         .objectFit(ImageFit.Contain)
37.     }.width('100%').height('100%')
38.   }
39.     aboutToDisappear(): void {
40.       this.visionImageAnalyzerController.off('imageAnalyzerVisibilityChange')
41.       this.visionImageAnalyzerController.off('textAnalysis')
42.       this.visionImageAnalyzerController.off('selectedTextChange')
43.       this.visionImageAnalyzerController.off('subjectAnalysis')
44.       this.visionImageAnalyzerController.off('selectedSubjectsChange')
45.       this.visionImageAnalyzerController.off('analyzerFailed')
46.     }
47. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-documentscanner "文档扫描")
