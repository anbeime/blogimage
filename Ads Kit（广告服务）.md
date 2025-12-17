# Ads Kit简介

更新时间: 2025-12-16 16:35

Ads Kit（广告服务）依托华为终端平台与数据能力为您提供流量变现服务，帮助您解决流量变现的难题；同时为广告主提供广告服务，配合华为终端平台向用户提供个性化的营销活动或商业广告。

## 流量变现服务

鲸鸿动能流量变现服务（以下简称流量变现服务）是广告服务依托华为终端强大的平台与数据能力为您提供的App流量变现服务，您通过该服务可以在自己的App中获取并向用户展示精美的、高价值的广告内容，并从中获得广告收益。

为满足App不同场景下的内容形式，流量变现服务为您提供了横幅广告、原生广告、激励广告、插屏广告、开屏广告、贴片广告六种广告形式。

## 开放匿名设备标识服务

Ads Kit提供开放匿名设备标识符和转化跟踪能力，方便广告平台和广告主进行个性化广告投放和广告转化渠道跟踪。

开放匿名设备标识符（Open Anonymous Device Identifier, OAID，以下简称OAID）：是一种非永久性设备标识符，基于开放匿名设备标识符，可在保护用户个人数据隐私安全的前提下，向用户提供个性化广告，同时三方监测平台也可以向广告主提供转化归因分析。

## 场景介绍

- 流量变现服务
    
    满足开发者在不同场景下，基于六种广告形式的设计需求。具体详情请参见下方表格。
    
    |广告形式|展示形式|应用场景|
    |:--|:--|:--|
    |横幅广告|图片|以通知栏或矩形固定展示在应用内页面顶部、中部或底部，适合用于用户停留较久或者访问频繁的页面。|
    |原生广告|图片、视频|界面内插入广告，与媒体内容无缝融合。|
    |激励广告|视频|游戏通关、复活、获取道具、积分、继续机会、人物技能升级时等展示。|
    |插屏广告|图片、视频|游戏或流媒体开启、暂停、过关、跳转、加载、退出时弹出。|
    |开屏广告|图片、视频|打开App时，以开屏形式全屏展现，展示时长3s-5s，展示完毕后自动关闭并进入应用主页面。|
    |贴片广告|图片、视频|前贴：视频播放前。<br><br>中贴：视频播放中。<br><br>后贴：视频播放结束后。<br><br>说明：您可以根据自身需求设置广告的播放时长。|
    
- 开放匿名设备标识服务
    
    支持广告平台、开发者、三方监测平台及广告主基于不同场景的使用。
    
    |场景|使用对象|描述|
    |:--|:--|:--|
    |基于OAID的个性化广告|广告平台|广告平台可基于OAID，向用户提供更加个性化的营销活动或商业广告，提升转化效果。|
    |基于OAID进行变现|开发者|您需要按照广告平台的接入流程接入广告平台，即可在华为手机上进行个性化的广告展示和流量变现。|
    |基于OAID的转化归因分析|三方监测平台|三方监测平台可基于OAID，分析广告的曝光、点击事件和App激活、注册等后向转化交互事件，对广告投放效果进行归因分析。|
    

## 约束和限制

### 支持的设备

|能力|支持设备|
|:--|:--|
|流量变现服务|Phone、Tablet。|
|开放匿名设备标识服务|Phone、Tablet、PC/2in1、TV。|

### 支持的国家/地区

|能力|支持的国家/地区|
|:--|:--|
|流量变现服务（横幅广告尺寸设置）|在中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）暂只支持宽360vp* 高57vp和宽360vp*高144vp。|
|流量变现服务（接入媒体限制）|中国境内（香港特别行政区、澳门特别行政区、中国台湾除外），与华为联运的游戏应用禁止接入鲸鸿动能平台以外的其他广告平台、插件、SDK等。其他类型的应用允许接入鲸鸿动能平台且不受此限制。|
|开放匿名设备标识服务（OAID、App转化跟踪参数）|当前仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。|

## 模拟器支持情况

从6.0.0(20) Beta5版本开始，本Kit支持模拟器开发。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-kit-guide "Ads Kit（广告服务）")
# Ads Kit术语

更新时间: 2025-12-16 16:36

## Banner Ad 横幅广告

横幅广告又名Banner广告，是在应用程序顶部、中部或底部占据一个位置的矩形图片，广告内容每隔一段时间会自动刷新。

## Interstital Ad 插屏广告

插屏广告是一种在应用开启、暂停或退出时以全屏或半屏的形式弹出的广告形式，展示时机巧妙避开用户对应用的正常体验，尺寸大，曝光效果好。

## Native Ad 原生广告

原生广告是与应用内容融于一体的广告，通过“和谐”的内容呈现广告信息，在不破坏用户体验的前提下，为用户提供有价值的信息，展示形式包含图片和视频，支持开发者自由定制界面。

## OAID

开放匿名设备标识符（Open Anonymous Device Identifier），是一种非永久性设备标识符，基于开放匿名设备标识符，可在保护用户个人数据隐私安全的前提下，向用户提供个性化广告，同时三方监测平台也可以向广告主提供转化归因分析。

## Reward Ad 激励广告

激励广告是一种全屏幕的视频广告，用户可以选择点击观看，以换取相应奖励。

## Roll Ad 贴片广告

贴片广告是一种在视频播放前、视频播放中或视频播放结束后插入的视频或图片广告。

## Splash Ad 开屏广告

开屏广告是一种在应用启动时且在应用主界面显示之前被展示的广告。开发者需要预先为App设计一张开屏默认的Slogan图片，确保在未获得到开屏广告之前展示默认的Slogan，提供良好的用户体验。

## Petal Ads 鲸鸿动能

鲸鸿动能是鸿蒙生态全场景智慧营销平台，打通华为1+8+N全场景生态布局下的媒介流量，为用户带来高品质的营销体验。

## ECPM

每千次有效收入（effective cost per mille），表示每一千次展示可以获得的广告收入。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-introduction "Ads Kit简介")
# 开发准备

更新时间: 2025-12-16 16:36

## 申请权限

应用在使用Ads Kit能力前，需要检查是否已经获取对应权限。如未获得授权，需要声明对应权限。

Ads Kit所需的权限有：

- ohos.permission.INTERNET：用于请求和展示广告、回传竞价结果。
- ohos.permission.APP_TRACKING_CONSENT：用于获取开放匿名设备标识符。

在模块的module.json5中配置所需申请的权限，其中跨应用关联权限[ohos.permission.APP_TRACKING_CONSENT](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/permissions-for-all-user#ohospermissionapp_tracking_consent)为user_grant权限，reason和abilities标签必填，配置方式参见[requestPermissions标签说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。

示例代码如下所示：

1. {
2.   "module": {
3.     "requestPermissions": [
4.       {
5.         "name": "ohos.permission.APP_TRACKING_CONSENT",
6.         "reason": "$string:reason",
7.         "usedScene": {
8.           "abilities": [
9.             "EntryAbility"
10.           ],
11.           "when": "inuse"
12.         }
13.       },
14.       {
15.         "name": "ohos.permission.INTERNET"
16.       }
17.     ]
18.   }
19. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-kit-glossary "Ads Kit术语")
# 流量变现服务开发概述

更新时间: 2025-12-16 16:36

流量变现服务是依托华为终端强大的平台与数据能力为您提供的App流量变现服务，依托HarmonyOS系统让您无需集成SDK，轻松实现广告的接入，您通过该服务可以在自己的App中获取并向用户展示精美的、高价值的广告内容，并从中获得广告收益，帮助您解决流量变现的难题。

## 产品优势

- 海量高价值用户群体
    
    拥有海量高价值用户，提供更高的变现价值。
    

- 高效的变现效率
    
    依托终端平台能力，用户触达更精准，实现高效变现。
    

- 更佳的用户体验
    
    与设备OS系统一致的广告UI设计，用户体验更佳。
    

## 业务价值

- 高额的变现收益
    
    海量优质广告主，充足的填充率，高竞争力的eCPM；极具优势的分成和激励政策，高额的收入回报。
    

- 丰富的广告形式
    
    主流广告场景，灵活满足展示需求；统一UI设计，适配各类华为终端设备，提供一致性品牌展示。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-dev "流量变现服务开发")
# 横幅广告

更新时间: 2025-12-16 16:36

## 场景介绍

横幅广告又名Banner广告，是在应用程序顶部、中部或底部占据一个位置的矩形图片，广告内容每隔一段时间会自动刷新。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163645.96595301529785902590452936786467:50001231000000:2800:A621DDCDC833EFE6F0BEB3BD0B4BFE59157656D2C70FEEBB7144C85DFD3C21F3.png)

## 接口说明

|接口名|描述|
|:--|:--|
|[AutoAdComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-autoadcomponent)({adParam: advertising.AdRequestParams, adOptions: advertising.AdOptions, displayOptions: advertising.AdDisplayOptions, interactionListener: advertising.AdInteractionListener})|展示广告，通过AdRequestParams、AdOptions进行广告请求参数设置，通过AdDisplayOptions进行广告展示参数设置，通过AdInteractionListener监听广告状态回调。|

## 开发步骤

1. 导入相关模块。
    
    1. import { abilityAccessCtrl, common, PermissionRequestResult } from '@kit.AbilityKit';
    2. import { advertising, AutoAdComponent, identifier } from '@kit.AdsKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 获取OAID。
    
    若需提升广告推送精准度，可以在请求参数[AdRequestParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adrequestparams)中添加oaid属性以提升广告推送精准度和广告填充率。
    
    如何获取OAID参考[获取OAID信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/oaid-service)。
    
    说明
    
    使用以下示例中提供的测试广告位时，必须先获取OAID信息。
    
3. 请求和展示广告。
    
    在您的页面中使用AutoAdComponent组件请求和展示横幅广告。
    
    请求广告关键参数如下所示：
    
    |请求广告参数名|类型|必填|说明|
    |:--|:--|:--|:--|
    |adType|number|是|请求广告类型，横幅广告类型为8。|
    |adId|string|是|广告位ID。<br><br>- 如果仅调测广告，可使用测试广告位ID：testw6vs28auh3。<br>- 如果要接入正式广告，则需要申请正式的广告位ID。可在应用发布前进入[流量变现官网](https://developer.huawei.com/consumer/cn/monetize)，点击“开始变现”，登录[鲸鸿动能媒体服务平台](https://developer.huawei.com/consumer/cn/service/ads/publisher/html/index.html?lang=zh)进行申请，具体操作详情请参见[展示位创建](https://developer.huawei.com/consumer/cn/doc/monetize/zhanshiweichuangjian-0000001132700049)。|
    |adWidth|number|是|广告位宽，单位vp。宽和高支持360*57和360*144两种尺寸。|
    |adHeight|number|是|广告位高，单位vp。宽和高支持360*57和360*144两种尺寸。|
    |oaid|string|否|开放匿名设备标识符，用于精准推送广告。不填无法获取到个性化广告。|
    
    展示广告关键参数如下所示：
    
    |展示广告参数名|类型|必填|说明|
    |:--|:--|:--|:--|
    |refreshTime|number|否|横幅广告轮播时间。单位ms，取值范围[30000, 120000]。<br><br>如果不设置或取值为非数字或小于等于0的数字，则不轮播。设置小于30000的数字取值30000，设置大于120000的数字取值120000。|
    
    展示广告通过[AdInteractionListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adinteractionlistener)监听广告状态回调，涉及的回调状态如下所示：
    
    |回调状态|说明|使用建议|
    |:--|:--|:--|
    |onAdOpen|打开广告。|-|
    |onAdClick|点击广告。|-|
    |onAdClose|关闭广告。|用户关闭广告时触发，需要将广告组件隐藏。|
    |onAdLoad|广告加载成功。|-|
    |onAdFail|广告加载失败。|广告加载失败时触发，需要将广告组件隐藏。|
    
    示例代码如下所示：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   @State visibilityState: Visibility = Visibility.None;
    5.   // 广告请求参数
    6.   private adRequestParams: advertising.AdRequestParams = {
    7.     // 'testw6vs28auh3'为测试专用的广告位ID，App正式发布时需要改为正式的广告位ID
    8.     adId: 'testw6vs28auh3',
    9.     // 横幅广告类型
    10.     adType: 8,
    11.     // 广告位宽
    12.     adWidth: 360,
    13.     // 广告位高
    14.     adHeight: 57
    15.   };
    16.   // 广告配置参数，开发者可根据项目实际情况设置
    17.   private adOptions: advertising.AdOptions = {};
    18.   // 广告展示参数，开发者可根据项目实际情况设置
    19.   private adDisplayOptions: advertising.AdDisplayOptions = {
    20.     // 广告轮播的时间间隔，单位ms，取值范围[30000, 120000]
    21.     refreshTime: 30000
    22.   };
    23.   private ratio: number = 1;
    24.   private context: common.UIAbilityContext = this.getUIContext().getHostContext() as common.UIAbilityContext;
    
    25.   async aboutToAppear(): Promise<void> {
    26.     // 开放匿名设备标识符
    27.     this.adRequestParams.oaid = await requestOAID(this.context);
    28.     this.visibilityState = Visibility.Visible;
    29.     if (this.adRequestParams.adWidth && this.adRequestParams.adHeight) {
    30.       this.ratio = this.adRequestParams.adWidth / this.adRequestParams.adHeight;
    31.     }
    32.   }
    
    33.   build() {
    34.     Stack({ alignContent: Alignment.Bottom }) {
    35.       Row() {
    36.         AutoAdComponent({
    37.           adParam: this.adRequestParams,
    38.           adOptions: this.adOptions,
    39.           displayOptions: this.adDisplayOptions,
    40.           interactionListener: {
    41.             onStatusChanged: (status: string, ad: advertising.Advertisement, data: string) => {
    42.               switch (status) {
    43.                 case 'onAdOpen':
    44.                   hilog.info(0x0000, 'testTag', 'Status is onAdOpen');
    45.                   break;
    46.                 case 'onAdClick':
    47.                   hilog.info(0x0000, 'testTag', 'Status is onAdClick');
    48.                   break;
    49.                 case 'onAdClose':
    50.                   hilog.info(0x0000, 'testTag', 'Status is onAdClose');
    51.                   this.visibilityState = Visibility.None;
    52.                   break;
    53.                 case 'onAdLoad':
    54.                   hilog.info(0x0000, 'testTag', 'Status is onAdLoad');
    55.                   break;
    56.                 case 'onAdFail':
    57.                   hilog.error(0x0000, 'testTag', 'Status is onAdFail');
    58.                   this.visibilityState = Visibility.None;
    59.                   break;
    60.               }
    61.             }
    62.           }
    63.         })
    64.       }
    65.       .width('100%')
    66.       .aspectRatio(this.ratio)
    67.       .visibility(this.visibilityState)
    68.     }
    69.     .width('100%')
    70.     .height('100%')
    71.   }
    72. }
    
    73. async function requestOAID(context: Context): Promise<string | undefined> {
    74.   // 向用户请求授权广告跨应用关联访问权限
    75.   let isPermissionGranted: boolean = false;
    76.   try {
    77.     const atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
    78.     const result: PermissionRequestResult =
    79.       await atManager.requestPermissionsFromUser(context, ['ohos.permission.APP_TRACKING_CONSENT']);
    80.     isPermissionGranted = result.authResults[0] === abilityAccessCtrl.GrantStatus.PERMISSION_GRANTED;
    81.   } catch (err) {
    82.     hilog.error(0x0000, 'testTag', `Failed to request permission. Code is ${err.code}, message is ${err.message}`);
    83.   }
    84.   if (isPermissionGranted) {
    85.     hilog.info(0x0000, 'testTag', 'Succeeded in requesting permission');
    86.     try {
    87.       const oaid = await identifier.getOAID();
    88.       hilog.info(0x0000, 'testTag', 'Succeeded in getting OAID');
    89.       return oaid;
    90.     } catch (err) {
    91.       hilog.error(0x0000, 'testTag', `Failed to get OAID. Code is ${err.code}, message is ${err.message}`);
    92.     }
    93.   } else {
    94.     hilog.error(0x0000, 'testTag', 'Failed to request permission. User rejected');
    95.   }
    96.   return undefined;
    97. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-dev-overview "流量变现服务开发概述")
# 原生广告

更新时间: 2025-12-16 16:36

## 场景介绍

原生广告是与应用内容融于一体的广告，通过“和谐”的内容呈现广告信息，在不破坏用户体验的前提下，为用户提供有价值的信息，展示形式包含图片和视频，支持您自由定制界面。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163656.44761056259460885269178289133477:50001231000000:2800:37C0903741984F4ED09B7EDD9A26280280A035C63575ACB393E6086E369F94E5.png)

## 接口说明

|接口名|描述|
|:--|:--|
|[loadAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadad)(adParam: AdRequestParams, adOptions: AdOptions, listener: AdLoadListener): void|请求单广告位广告，通过AdRequestParams、AdOptions进行广告请求参数设置，通过AdLoadListener监听广告请求回调。|
|[loadAdWithMultiSlots](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadadwithmultislots)(adParams: AdRequestParams[], adOptions: AdOptions, listener: MultiSlotsAdLoadListener): void|请求多广告位广告，通过AdRequestParams[]、AdOptions进行广告请求参数设置，通过MultiSlotsAdLoadListener监听广告请求回调。|
|[AdComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-adcomponent)({ads: advertising.Advertisement[], displayOptions: advertising.AdDisplayOptions, interactionListener: advertising.AdInteractionListener, @BuilderParam adRenderer?: () => void, @Prop rollPlayState?: number})|展示广告，通过AdDisplayOptions进行广告展示参数设置，通过AdInteractionListener监听广告状态回调。<br><br>**说明：**为了保证广告能正确展示，该接口必须和请求广告接口配套使用。|

## AdComponent组件建议宽高

|样式|建议宽高|
|:--|:--|
|原生信息流|width：与信息流内容保持一致。<br><br>height：无需设置。|
|原生插图|width：312vp。<br><br>height：284vp。|

## 开发步骤

### 请求广告

1. 导入相关模块。
    
    1. import { abilityAccessCtrl, common, PermissionRequestResult } from '@kit.AbilityKit';
    2. import { advertising, identifier } from '@kit.AdsKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 获取OAID。
    
    若需提升广告推送精准度，可以在请求参数[AdRequestParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adrequestparams)中添加oaid属性。
    
    如何获取OAID参见[获取OAID信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/oaid-service)。
    
    说明
    
    使用以下示例中提供的测试广告位时，必须先获取OAID信息。
    
3. 请求广告。
    
    请求广告需要创建一个AdLoader对象。
    
    - 如果要请求单广告位广告，通过AdLoader的[loadAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadad)方法请求广告，通过[AdLoadListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adloadlistener)来监听广告的加载状态。
    - 如果要请求多广告位广告，通过AdLoader的[loadAdWithMultiSlots](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadadwithmultislots)方法请求广告，通过[MultiSlotsAdLoadListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#multislotsadloadlistener)来监听广告的加载状态。
    
    请求广告关键参数如下所示：
    
    |请求广告参数名|类型|必填|说明|
    |:--|:--|:--|:--|
    |adType|number|是|请求广告类型，原生广告类型为3。|
    |adId|string|是|广告位ID。<br><br>- 如果仅调测广告，可使用测试广告位ID：testy63txaom86（原生视频），testu7m3hc4gvm（原生大图），testb65czjivt9（原生小图），testr6w14o0hqz（原生三图）。<br>- 如果要接入正式广告，则需要申请正式的广告位ID。可在应用发布前进入[流量变现官网](https://developer.huawei.com/consumer/cn/monetize)，点击“开始变现”，登录[鲸鸿动能媒体服务平台](https://developer.huawei.com/consumer/cn/service/ads/publisher/html/index.html?lang=zh)进行申请，具体操作详情请参见[展示位创建](https://developer.huawei.com/consumer/cn/doc/monetize/zhanshiweichuangjian-0000001132700049)。|
    |oaid|string|否|开放匿名设备标识符，用于精准推送广告。不填无法获取到个性化广告。|
    
    以请求多广告位广告为例，示例代码如下所示：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   @State ads: advertising.Advertisement[] = [];
    5.   // ...
    6.   private context: common.UIAbilityContext = this.getUIContext().getHostContext() as common.UIAbilityContext;
    
    7.   aboutToAppear(): void {
    8.     // 调用loadAd加载广告
    9.     // ...
    10.   }
    
    11.   private async loadAd(...adIds: string[]): Promise<void> {
    12.     // 广告请求参数
    13.     const adRequestParamsArray: advertising.AdRequestParams[] = [];
    14.     const oaid: string | undefined = await requestOAID(this.context);
    15.     for (const adId of adIds) {
    16.       adRequestParamsArray.push({
    17.         // 广告位ID
    18.         adId: adId,
    19.         // 原生广告类型
    20.         adType: 3,
    21.         // 原生广告扩展参数，是否直接返回广告，不用等待所有广告素材下载完成
    22.         enableDirectReturnVideoAd: true,
    23.         // 开放匿名设备标识符
    24.         oaid: oaid
    25.       });
    26.     }
    27.     // 广告配置参数，开发者可根据项目实际情况设置
    28.     const adOptions: advertising.AdOptions = {};
    29.     // 广告请求回调监听
    30.     const multiSlotsAdLoaderListener: advertising.MultiSlotsAdLoadListener = {
    31.       onAdLoadFailure: (errorCode: number, errorMsg: string) => {
    32.         hilog.error(0x0000, 'testTag', `Failed to load multiSlots ad. Code is ${errorCode}, message is ${errorMsg}`);
    33.       },
    34.       onAdLoadSuccess: (ads: Map<string, Array<advertising.Advertisement>>) => {
    35.         hilog.info(0x0000, 'testTag', 'Succeeded in loading multiSlots ad');
    36.         const returnAds: advertising.Advertisement[] = [];
    37.         ads.forEach((adsArray) => returnAds.push(...adsArray));
    38.         this.ads = returnAds;
    39.       }
    40.     };
    41.     // 创建AdLoader广告对象
    42.     const adLoader: advertising.AdLoader = new advertising.AdLoader(this.context);
    43.     try {
    44.       // 调用广告请求接口
    45.       adLoader.loadAdWithMultiSlots(adRequestParamsArray, adOptions, multiSlotsAdLoaderListener);
    46.     } catch (e) {
    47.       hilog.error(0x0000, 'testTag', `Failed to load multiSlots ad. Code is ${e.code}, message is ${e.message}`);
    48.     }
    49.   }
    
    50.   build() {
    51.     // ...
    52.   }
    
    53.   // ...
    54. }
    
    55. async function requestOAID(context: Context): Promise<string | undefined> {
    56.   // 向用户请求授权广告跨应用关联访问权限
    57.   let isPermissionGranted: boolean = false;
    58.   try {
    59.     const atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
    60.     const result: PermissionRequestResult =
    61.       await atManager.requestPermissionsFromUser(context, ['ohos.permission.APP_TRACKING_CONSENT']);
    62.     isPermissionGranted = result.authResults[0] === abilityAccessCtrl.GrantStatus.PERMISSION_GRANTED;
    63.   } catch (err) {
    64.     hilog.error(0x0000, 'testTag', `Failed to request permission. Code is ${err.code}, message is ${err.message}`);
    65.   }
    66.   if (isPermissionGranted) {
    67.     hilog.info(0x0000, 'testTag', 'Succeeded in requesting permission');
    68.     try {
    69.       const oaid = await identifier.getOAID();
    70.       hilog.info(0x0000, 'testTag', 'Succeeded in getting OAID');
    71.       return oaid;
    72.     } catch (err) {
    73.       hilog.error(0x0000, 'testTag', `Failed to get OAID. Code is ${err.code}, message is ${err.message}`);
    74.     }
    75.   } else {
    76.     hilog.error(0x0000, 'testTag', 'Failed to request permission. User rejected');
    77.   }
    78.   return undefined;
    79. }
    

### 展示广告

1. 导入相关模块。
    
    1. import { AdComponent, advertising } from '@kit.AdsKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 展示广告。
    
    展示广告通过[AdInteractionListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adinteractionlistener)监听广告状态回调，涉及的回调状态如下所示：
    
    |回调状态|说明|使用建议|
    |:--|:--|:--|
    |onAdOpen|打开广告。|-|
    |onAdClick|点击广告。|-|
    |onAdClose|关闭广告。|用户点击负反馈或关闭广告时触发，需要将广告组件隐藏。|
    |onAdFail|广告加载失败。|广告展示失败时触发，需要将广告组件隐藏。|
    
    原生信息流广告通常不需要显式设置广告展示组件[AdComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-adcomponent)的高度，组件会自动调整高度以适应需要展示的内容。
    
    示例代码如下所示：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   @State ads: advertising.Advertisement[] = [];
    5.   @State visibilityState: Visibility = Visibility.Visible;
    6.   // ...
    
    7.   build() {
    8.     Column() {
    9.       if (this.ads.length > 0) {
    10.         this.inFeedNativeAd(this.ads[0])
    11.         // ...
    12.       }
    13.     }
    14.     .width('100%')
    15.     .height('100%')
    16.   }
    
    17.   @Builder
    18.   inFeedNativeAd(ad: advertising.Advertisement): void {
    19.     Row() {
    20.       AdComponent({
    21.         ads: [ad],
    22.         // 广告展示参数，开发者可根据项目实际情况设置
    23.         displayOptions: {
    24.           // 是否静音
    25.           mute: true
    26.         },
    27.         interactionListener: {
    28.           onStatusChanged: (status: string, ad: advertising.Advertisement, data: string) => {
    29.             switch (status) {
    30.               case 'onAdOpen':
    31.                 hilog.info(0x0000, 'testTag', 'Status is onAdOpen');
    32.                 break;
    33.               case 'onAdClick':
    34.                 hilog.info(0x0000, 'testTag', 'Status is onAdClick');
    35.                 break;
    36.               case 'onAdClose':
    37.                 hilog.info(0x0000, 'testTag', 'Status is onAdClose');
    38.                 this.visibilityState = Visibility.None;
    39.                 break;
    40.               case 'onAdFail':
    41.                 hilog.info(0x0000, 'testTag', 'Status is onAdFail');
    42.                 this.visibilityState = Visibility.None;
    43.                 break;
    44.             }
    45.           }
    46.         }
    47.       })
    48.       // 原生信息流样式，不建议设置高度，宽度建议设置为100%，撑满父容器
    49.         .width('100%')
    50.     }
    51.     .width('100%')
    52.     .padding({ left: 16, right: 16 })
    53.     .visibility(this.visibilityState)
    54.   }
    
    55.   // ...
    56. }
    
    原生插图广告宽高为固定值312vp*284vp，开发者可以将广告展示组件[AdComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-adcomponent)居中展示。
    
    示例代码如下所示：
    
    57. @Entry
    58. @Component
    59. struct Index {
    60.   @State ads: advertising.Advertisement[] = [];
    61.   @State visibilityState: Visibility = Visibility.Visible;
    62.   // ...
    
    63.   build() {
    64.     Column() {
    65.       if (this.ads.length > 0) {
    66.         // ...
    67.         this.nativeCardAd(this.ads[0])
    68.       }
    69.     }
    70.     .width('100%')
    71.     .height('100%')
    72.   }
    
    73.   // ...
    
    74.   @Builder
    75.   nativeCardAd(ad: advertising.Advertisement): void {
    76.     Row() {
    77.       AdComponent({
    78.         ads: [ad],
    79.         // 广告展示参数，开发者可根据项目实际情况设置
    80.         displayOptions: {
    81.           // 是否静音
    82.           mute: true
    83.         },
    84.         interactionListener: {
    85.           onStatusChanged: (status: string, ad: advertising.Advertisement, data: string) => {
    86.             switch (status) {
    87.               case 'onAdOpen':
    88.                 hilog.info(0x0000, 'testTag', 'Status is onAdOpen');
    89.                 break;
    90.               case 'onAdClick':
    91.                 hilog.info(0x0000, 'testTag', 'Status is onAdClick');
    92.                 break;
    93.               case 'onAdClose':
    94.                 hilog.info(0x0000, 'testTag', 'Status is onAdClose');
    95.                 this.visibilityState = Visibility.None;
    96.                 break;
    97.               case 'onAdFail':
    98.                 hilog.info(0x0000, 'testTag', 'Status is onAdFail');
    99.                 this.visibilityState = Visibility.None;
    100.                 break;
    101.             }
    102.           }
    103.         }
    104.       })
    105.       // 原生插图样式，宽高为固定值，为312vp*284vp
    106.         .width(312)
    107.         .height(284)
    108.     }
    109.     .width('100%')
    110.     // 宽高固定无法撑满父容器，将广告居中展示
    111.     .justifyContent(FlexAlign.Center)
    112.     .visibility(this.visibilityState)
    113.   }
    114. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-banner "横幅广告")
# 激励广告

更新时间: 2025-12-16 16:37

## 场景介绍

激励广告是一种全屏幕的视频广告，用户可以选择点击观看，以换取相应奖励。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163708.22886655456913010975692812154032:50001231000000:2800:B3D1F5CC094FBD09E1982BFED8D3E3A29F3651A554FE303F34F5957F51C9738A.png "点击放大")

## 接口说明

|接口名|描述|
|:--|:--|
|[loadAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadad)(adParam: AdRequestParams, adOptions: AdOptions, listener: AdLoadListener): void|请求单广告位广告，通过AdRequestParams、AdOptions进行广告请求参数设置，通过AdLoadListener监听广告请求回调。|
|[showAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#showad)(ad: Advertisement, options: AdDisplayOptions, context?: common.UIAbilityContext): void|展示广告，通过AdDisplayOptions进行广告展示参数设置。<br><br>**说明：**为了保证广告能正确展示，该接口必须和请求广告接口配套使用。|

## 开发步骤

### 请求广告

1. 导入相关模块。
    
    1. import { abilityAccessCtrl, common, PermissionRequestResult } from '@kit.AbilityKit';
    2. import { advertising, identifier } from '@kit.AdsKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 获取OAID。
    
    若需提升广告推送精准度，可以在请求参数[AdRequestParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adrequestparams)中添加oaid属性。
    
    如何获取OAID参见[获取OAID信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/oaid-service)。
    
    说明
    
    使用以下示例中提供的测试广告位时，必须先获取OAID信息。
    
3. 请求单广告位广告。
    
    需要先创建一个AdLoader对象，通过AdLoader的[loadAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadad)方法请求广告，最后通过[AdLoadListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adloadlistener)，来监听广告的加载状态。
    
    请求广告关键参数如下所示：
    
    |请求广告参数名|类型|必填|说明|
    |:--|:--|:--|:--|
    |adType|number|是|请求广告类型，激励广告类型为7。|
    |adId|string|是|广告位ID。<br><br>- 如果仅调测广告，可使用测试广告位ID：testx9dtjwj8hp。<br>- 如果要接入正式广告，则需要申请正式的广告位ID。可在应用发布前进入[流量变现官网](https://developer.huawei.com/consumer/cn/monetize)，点击“开始变现”，登录[鲸鸿动能媒体服务平台](https://developer.huawei.com/consumer/cn/service/ads/publisher/html/index.html?lang=zh)进行申请，具体操作详情请参见[展示位创建](https://developer.huawei.com/consumer/cn/doc/monetize/zhanshiweichuangjian-0000001132700049)。|
    |oaid|string|否|开放匿名设备标识符，用于精准推送广告。不填无法获取到个性化广告。|
    
    示例代码如下所示：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   private context: common.UIAbilityContext = this.getUIContext().getHostContext() as common.UIAbilityContext;
    
    5.   build() {
    6.     Column() {
    7.       Button('LoadAd')
    8.         .onClick(() => {
    9.           this.loadAd();
    10.         })
    11.     }
    12.     .width('100%')
    13.     .height('100%')
    14.     .justifyContent(FlexAlign.Center)
    15.   }
    
    16.   private async loadAd(): Promise<void> {
    17.     // 广告请求回调监听
    18.     const adLoadListener: advertising.AdLoadListener = {
    19.       // 广告请求失败回调
    20.       onAdLoadFailure: (errorCode: number, errorMsg: string) => {
    21.         hilog.error(0x0000, 'testTag', `Failed to load ad. Code is ${errorCode}, message is ${errorMsg}`);
    22.       },
    23.       // 广告请求成功回调
    24.       onAdLoadSuccess: (ads: Array<advertising.Advertisement>) => {
    25.         hilog.info(0x0000, 'testTag', 'Succeeded in loading ad');
    26.         // ...
    27.       }
    28.     };
    29.     // 广告请求参数
    30.     const adRequestParams: advertising.AdRequestParams = {
    31.       // 'testx9dtjwj8hp'为测试专用的广告位ID，App正式发布时需要改为正式的广告位ID
    32.       adId: 'testx9dtjwj8hp',
    33.       // 激励广告类型
    34.       adType: 7,
    35.       // 开放匿名设备标识符
    36.       oaid: await requestOAID(this.context)
    37.     };
    38.     // 广告配置参数，开发者可根据项目实际情况设置
    39.     const adOptions: advertising.AdOptions = {};
    40.     // 创建AdLoader广告对象
    41.     const adLoader: advertising.AdLoader = new advertising.AdLoader(this.context);
    42.     try {
    43.       // 调用广告请求接口
    44.       adLoader.loadAd(adRequestParams, adOptions, adLoadListener);
    45.     } catch (e) {
    46.       hilog.error(0x0000, 'testTag', `Failed to load ad. Code is ${e.code}, message is ${e.message}`);
    47.     }
    48.   }
    49. }
    
    50. async function requestOAID(context: Context): Promise<string | undefined> {
    51.   // 向用户请求授权广告跨应用关联访问权限
    52.   let isPermissionGranted: boolean = false;
    53.   try {
    54.     const atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
    55.     const result: PermissionRequestResult =
    56.       await atManager.requestPermissionsFromUser(context, ['ohos.permission.APP_TRACKING_CONSENT']);
    57.     isPermissionGranted = result.authResults[0] === abilityAccessCtrl.GrantStatus.PERMISSION_GRANTED;
    58.   } catch (err) {
    59.     hilog.error(0x0000, 'testTag', `Failed to request permission. Code is ${err.code}, message is ${err.message}`);
    60.   }
    61.   if (isPermissionGranted) {
    62.     hilog.info(0x0000, 'testTag', 'Succeeded in requesting permission');
    63.     try {
    64.       const oaid = await identifier.getOAID();
    65.       hilog.info(0x0000, 'testTag', 'Succeeded in getting OAID');
    66.       return oaid;
    67.     } catch (err) {
    68.       hilog.error(0x0000, 'testTag', `Failed to get OAID. Code is ${err.code}, message is ${err.message}`);
    69.     }
    70.   } else {
    71.     hilog.error(0x0000, 'testTag', 'Failed to request permission. User rejected');
    72.   }
    73.   return undefined;
    74. }
    

### 事件订阅

1. 导入相关模块。
    
    1. import { BusinessError, commonEventManager } from '@kit.BasicServicesKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 事件订阅。
    
    开发者需要在应用中订阅com.huawei.hms.pps.action.PPS_REWARD_STATUS_CHANGED事件来监听激励广告页面变化并接收奖励信息。
    
    在订阅到公共事件后，可以从[CommonEventData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-commonevent-commoneventdata)的parameters参数中获取激励广告页面变化状态和奖励信息。
    
    - 使用reward_ad_status作为key值获取激励广告页面变化状态，涉及的页面变化状态如下所示：
        
        |页面变化状态|说明|
        |:--|:--|
        |onAdOpen|打开广告。|
        |onAdClick|点击广告。|
        |onAdClose|关闭广告。|
        |onAdReward|广告获得奖励。|
        |onVideoPlayBegin|广告视频开始播放。|
        |onVideoPlayEnd|广告视频播放结束。|
        
    - 使用reward_ad_data作为key值获取奖励信息，其中：
        - 属性rewardType用来获取奖励物品的名称。
        - 属性rewardAmount用来获取奖励物品的数量。
    
    示例代码如下所示：
    
    1. const KEY_REWARD_DATA = 'reward_ad_data';
    2. const KEY_REWARD_STATUS = 'reward_ad_status';
    
    3. export class RewardAdStatusHandler {
    4.   // 用于保存创建成功的订阅者对象，后续使用其完成订阅及退订的动作
    5.   private subscriber: commonEventManager.CommonEventSubscriber | null = null;
    
    6.   // 订阅方法，需要在每次展示广告前调用
    7.   public registerPPSReceiver(): void {
    8.     if (this.subscriber) {
    9.       this.unRegisterPPSReceiver();
    10.     }
    11.     // 订阅者信息
    12.     const subscribeInfo: commonEventManager.CommonEventSubscribeInfo = {
    13.       events: ['com.huawei.hms.pps.action.PPS_REWARD_STATUS_CHANGED'],
    14.       // publisherBundleName被设置为"com.huawei.hms.adsservice",这意味着只有来自该包名的事件才会被订阅者接受和处理。
    15.       // 如果没有明确声明publisherBundleName，那么订阅者可能会收到来自其它包名的伪造事件，从而导致安全性问题或误导。
    16.       publisherBundleName: 'com.huawei.hms.adsservice'
    17.     };
    18.     // 创建订阅者回调
    19.     commonEventManager.createSubscriber(subscribeInfo, (err: BusinessError, commonEventSubscriber:
    20.       commonEventManager.CommonEventSubscriber) => {
    21.       if (err) {
    22.         hilog.error(0x0000, 'testTag', `Failed to create subscriber. Code is ${err.code}, message is ${err.message}`);
    23.         return;
    24.       }
    25.       hilog.info(0x0000, 'testTag', 'Succeeded in creating subscriber');
    26.       this.subscriber = commonEventSubscriber;
    27.       // 订阅公共事件回调
    28.       commonEventManager.subscribe(this.subscriber, (err: BusinessError, commonEventSubscriber:
    29.         commonEventManager.CommonEventData) => {
    30.         if (err) {
    31.           hilog.error(0x0000, 'testTag', `Failed to subscribe. Code is ${err.code}, message is ${err.message}`);
    32.         } else {
    33.           hilog.info(0x0000, 'testTag', 'Succeeded in subscribing data');
    34.           const status: string = commonEventSubscriber?.parameters?.[KEY_REWARD_STATUS];
    35.           switch (status) {
    36.             case 'onAdOpen':
    37.               hilog.info(0x0000, 'testTag', 'Status is onAdOpen');
    38.               break;
    39.             case 'onAdClick':
    40.               hilog.info(0x0000, 'testTag', 'Status is onAdClick');
    41.               break;
    42.             case 'onAdClose':
    43.               hilog.info(0x0000, 'testTag', 'Status is onAdClose');
    44.               this.unRegisterPPSReceiver();
    45.               break;
    46.             case 'onAdReward':
    47.               const rewardData: Record<string, string | number> = commonEventSubscriber?.parameters?.[KEY_REWARD_DATA];
    48.               const rewardType: string = rewardData?.rewardType as string;
    49.               const rewardAmount: number = rewardData?.rewardAmount as number;
    50.               hilog.info(0x0000, 'testTag', `Status is onAdReward. Type is ${rewardType}, Amount is ${rewardAmount}`);
    51.               break;
    52.             case 'onVideoPlayBegin':
    53.               hilog.info(0x0000, 'testTag', 'Status is onVideoPlayBegin');
    54.               break;
    55.             case 'onVideoPlayEnd':
    56.               hilog.info(0x0000, 'testTag', 'Status is onVideoPlayEnd');
    57.               break;
    58.             default:
    59.               break;
    60.           }
    61.         }
    62.       });
    63.     });
    64.   }
    
    65.   // 取消订阅
    66.   public unRegisterPPSReceiver(): void {
    67.     commonEventManager.unsubscribe(this.subscriber, (err: BusinessError) => {
    68.       if (err) {
    69.         hilog.error(0x0000, 'testTag', `Failed to unsubscribe. Code is ${err.code}, message is ${err.message}`);
    70.       } else {
    71.         hilog.info(0x0000, 'testTag', 'Succeeded in unsubscribing');
    72.         this.subscriber = null;
    73.       }
    74.     });
    75.   }
    76. }
    

### 展示广告

1. 导入相关模块。
    
    1. import { common } from '@kit.AbilityKit';
    2. import { advertising } from '@kit.AdsKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    4. // 事件订阅步骤中创建的文件
    5. import { RewardAdStatusHandler } from './RewardAdStatusHandler';
    
2. 展示广告。
    
    开发者需要调用[showAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#showad)方法来展示广告，ads为[请求广告](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-reward#section1392312617269)返回的广告信息，在每次展示广告前需要注册[事件订阅](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-reward#section395845163219)中定义的监听器。
    
    示例代码如下所示：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   private context: common.UIAbilityContext = this.getUIContext().getHostContext() as common.UIAbilityContext;
    
    5.   build() {
    6.     // ...
    7.   }
    
    8.   private async loadAd(): Promise<void> {
    9.     // 广告请求回调监听
    10.     const adLoadListener: advertising.AdLoadListener = {
    11.       // 广告请求失败回调
    12.       onAdLoadFailure: (errorCode: number, errorMsg: string) => {
    13.         hilog.error(0x0000, 'testTag', `Failed to load ad. Code is ${errorCode}, message is ${errorMsg}`);
    14.       },
    15.       // 广告请求成功回调
    16.       onAdLoadSuccess: (ads: Array<advertising.Advertisement>) => {
    17.         hilog.info(0x0000, 'testTag', 'Succeeded in loading ad');
    18.         try {
    19.           // 注册激励广告状态监听器
    20.           new RewardAdStatusHandler().registerPPSReceiver();
    21.           // 广告展示参数，开发者可根据项目实际情况设置
    22.           const adDisplayOptions: advertising.AdDisplayOptions = {
    23.             // 是否静音
    24.             mute: true,
    25.             // ...
    26.           };
    27.           // 此处ads[0]表示请求到的第一个广告，开发者可根据项目实际情况选择
    28.           advertising.showAd(ads[0], adDisplayOptions, this.context);
    29.         } catch (e) {
    30.           hilog.error(0x0000, 'testTag', `Failed to show ad. Code is ${e.code}, message is ${e.message}`);
    31.         }
    32.       }
    33.     };
    34.     // ...
    35.   }
    36. }
    

## 校验激励广告服务端验证回调

服务端验证回调是指鲸鸿动能平台发送给媒体服务器的网址请求，其中带有特定的查询参数，用来通知媒体服务器某位用户因为与激励视频广告互动而应予以奖励，从而规避欺骗的行为。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163708.62949384161459313569995200772650:50001231000000:2800:DE7677FEE53A00154F65B289A4ACAE5E12CAD3619800C31B5C461D07C6428F4C.png "点击放大")

### 奖励用户

- 在给用户发奖励时，要把握好用户体验和奖励验证之间的平衡。由于服务器端回调会存在延迟的情况，因此我们建议客户端立即奖励用户，同时在收到服务器端回调时对所有奖励进行验证。这种做法可确保奖励符合发放条件，同时提供良好的用户体验。
- 对于某些应用而言，奖励是否达到发放条件非常重要，用户可适当接受延迟。这时，推荐做法是等待服务器端回调完成验证，再向用户发放奖励。

### 校验服务端验证回调

说明

App上架至华为应用市场（AppGallery）时间超过12小时才可以收到回调。

1. 设置激励广告的奖励配置。
    
    您在[鲸鸿动能媒体服务平台](https://developer.huawei.com/consumer/cn/service/ads/publisher/html/index.html?lang=zh)上申请激励视频广告位时选择“媒体管理（点击媒体名）> 新增展示位 > 选择激励视频（点击下一步，进入编辑页面）”，设置奖励类型和奖励数量，并点击“高级设置”，设置服务器端验证的URL。如下图：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163708.53861088760416693477746471961943:50001231000000:2800:5E55F9218A1FFF32DD6D02CD521A1D9A05F6209278D5D1E7562D8478EE93B014.png)
    
2. （可选）设置自定义数据customData和userId。
    
    您在[展示广告第2点](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-reward#section16597193515555)之前可以设置自定义数据customData和userId。示例代码如下所示：
    
    1. import { advertising } from '@kit.AdsKit';
    
    2. // 广告展示参数，开发者可根据项目实际情况设置
    3. const adDisplayOptions: advertising.AdDisplayOptions = {
    4.   // 是否静音
    5.   mute: true,
    6.   // 设置自定义数据
    7.   customData: 'CUSTOM_DATA',
    8.   // 设置自定义用户id
    9.   userId: '1234567'
    10. };
    
    说明
    
    如果没有设置customData和userId，不影响发放奖励事件上报但是服务端验证的参数中没有这两个字段。如果设置customData和userId，必须在展示广告之前设置并且URLEncode之后，长度不超过1024个字符，否则影响服务端验证。
    
3. 获取要验证的内容。
    
    用户观看完激励广告时，鲸鸿动能平台服务端会把需要验证的参数以及keyId和sign传给媒体提供的URL：https://www.example.com/feedback（[即第1点中配置的验证URL](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-reward#section77672242539)）。请求体样例：
    
    1. {
    2.     "adId" : "testx9dtjwj8hp",
    3.     "data" : "CUSTOM_DATA",
    4.     "keyId" : "12345678",
    5.     "rewardAmount" : "10",
    6.     "rewardName" : "金币",
    7.     "sign" : "OA33u6mypnhE4hbmF32N/ibYi1uXt72nDDyYMwjDI6JXVVFKePZYo4F7Fuk2MaG......",
    8.     "uniqueId" : "3361626337333932313435313430373438383561376265636130393939313166",
    9.     "userId" : "1234567"
    10. }
    
    服务器端验证回调查询参数说明：
    
    |参数名称|类型|是否必选|描述|
    |:--|:--|:--|:--|
    |adId|String|是|激励视频广告位ID|
    |data|String|否|自定义数据字符串|
    |keyId|String|是|验证回调的密钥|
    |rewardAmount|String|否|奖励数量|
    |rewardName|String|否|奖励奖品|
    |sign|String|是|回调的签名|
    |uniqueId|String|是|获奖事件生成的十六进制的标识符|
    |userId|String|否|用户ID|
    
4. 组装验证参数
    
    验证内容（除sign、keyId）格式顺序如下：
    
    adId={adId}&data={data}&rewardAmount={rewardAmount}&rewardName={rewardName}&uniqueId={uniqueId}&userId={userId}
    
    其中‘{}’里面表示参数的值，且参数顺序不能变。如果参数为null或者空字符串，则URL中不拼接该参数。然后用SHA256计算散列值，得到paramContentData。示例代码如下所示：
    
    1. String adId = request.getParameter("adId");
    2. String data = request.getParameter("data");
    3. // ...
    4. String userId = request.getParameter("userId");
    5. String param = "adId=" + adId + "&data=" + data + "&rewardAmount=" + rewardAmount + "&rewardName=" + rewardName + "&uniqueId=" + uniqueId + "&userId=" + userId;
    6. String sha256Value = Sha256Util.digest(param);
    7. byte[] paramContentData = sha256Value.getBytes(Charset.forName("UTF-8"));
    
5. 获取公钥列表。
    
    a. 在[鲸鸿动能媒体服务平台](https://developer.huawei.com/consumer/cn/service/ads/publisher/html/index.html?lang=zh)上查看对应的账户信息时选择“账户”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163708.23253267306960904258758149921808:50001231000000:2800:CFC957222129D96AB73D11FB8616D942481C430C320E8F266A1D961CBD849061.png)
    
    通过点击上图所示的“获取密钥”按钮弹出如下所示的弹框，获取“开发者ID”和“密钥”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163708.94811095609989241693201688565417:50001231000000:2800:7156DF6D3449396F214E1F237562BC01E5230411FA60D4395CD126DAFBE8BE23.png)
    
    b. 您根据应用分发区域不同，需要使用对应站点的接口URL去获取公钥列表，不同站点对应的接口URL如下所示：
    
    - 中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）：https://ppscrowd-drcn.op.hicloud.com/action-lib-track/publickeys
    
    将body通过密钥进行HMAC-SHA256加密得到签名，替换到Authorization中，并设置“开发者ID”和Authorization到Header中。示例代码如下所示：
    
    1. String data = "";
    2. String url = "https://ppscrowd-dre.op.dbankcloud.com/action-lib-track/publickeys";
    3. String authorization = "Digest validTime=\"{0}\", response=\"{1}\"";
    4. // 开发者ID
    5. String userId = "YOUR_PUBLISHER_ID"; 
    6. // 密钥
    7. String key = "YOUR_KEY"; 
    
    8. HttpClient httpclient = HttpClients.createDefault();
    9. HttpGet request = new HttpGet();
    10. try {
    11.     // 将body通过密钥进行HMAC-SHA256加密得到签名，替换到Authorization中
    12.     String validTime = String.valueOf(System.currentTimeMillis());
    13.     String body = validTime + ":/publickeys";
    14.     byte[] keyBytes = Base64.decodeBase64(key);
    15.     byte[] bodyBytes = body.getBytes(Charsets.UTF_8);
    
    16.     Mac mac = Mac.getInstance("HmacSHA256");
    17.     SecretKey secretKey = new SecretKeySpec(keyBytes, "HmacSHA256");
    18.     mac.init(secretKey);
    19.     byte[] signatureBytes = mac.doFinal(bodyBytes);
    
    20.     String signature = (signatureBytes == null) ? null : Hex.encodeHexString(signatureBytes);
    21.     authorization = MessageFormat.format(authorization, validTime, signature);
    22.     // 设置开发者ID和Authorization到Header中
    23.     request.setURI(new URI(url));
    24.     request.setHeader("userId", userId);
    25.     request.setHeader("Authorization", authorization);
    26.     HttpResponse response = httpclient.execute(request);
    27.     data = EntityUtils.toString(response.getEntity());
    28. } catch (Exception e) {
    29.     System.out.println(e.getMessage());
    30. }
    
    返回data消息体（publicKey已匿名化）：
    
    31. {    
    32.     "keys": [       
    33.         {          
    34.             "keyId":"12345678",          
    35.             "publicKey":"LS0tLS1*******************************************************"       
    36.         },      
    37.         {          
    38.             "keyId": "22345678",                               
    39.             "publicKey":"LS0tLS1*******************************************************"       
    40.         }     
    41.     ]
    42. }
    
    返回消息结构体：
    
    |参数名称|类型|是否必选|描述|
    |:--|:--|:--|:--|
    |keys|List<key>|是|返回公钥列表|
    
    - key结构体：
    
    |参数名称|类型|是否必选|描述|
    |:--|:--|:--|:--|
    |keyId|String|是|密钥ID|
    |publicKey|String|是|公钥|
    
6. 执行验证。
    
    a. 根据keyId从公钥列表中找到对应的base64编码后的publicKey。
    
    b. 将paramContentData、publicKey、sign和SHA256withRSA数字签名算法的入参，执行验证。
    
    示例代码如下所示：
    
    1. public static boolean verify(byte[] data, String publicKey, String sign, String signatureAlgorithm) {
    2.     try {
    3.         byte[] keyBytes = base64Decode(publicKey);
    4.         X509EncodedKeySpec keySpec = new X509EncodedKeySpec(keyBytes);
    5.         KeyFactory keyFactory = KeyFactory.getInstance("RSA");
    6.         PublicKey publicK = keyFactory.generatePublic(keySpec);
    7.         Signature signature = Signature.getInstance(signatureAlgorithm);
    8.         signature.initVerify(publicK);
    9.         signature.update(data);
    10.         return signature.verify(base64Decode(sign));
    11.     } catch (InvalidKeyException | SignatureException | UnsupportedEncodingException | InvalidKeySpecException | NoSuchAlgorithmException e) {
    12.         return false;
    13.     }
    14. }
    
    15. private static byte[] base64Decode(String encoded) throws UnsupportedEncodingException {
    16.     return Base64.decodeBase64(encoded.getBytes("UTF-8"));
    17. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-native "原生广告")
# 插屏广告

更新时间: 2025-12-16 16:37

## 场景介绍

插屏广告是一种在应用开启、暂停或退出时以全屏或半屏的形式弹出的广告形式，展示时机巧妙避开用户对应用的正常体验，尺寸大，曝光效果好。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163730.42309832434424697443468946745584:50001231000000:2800:F17DC752900F6BFF925CC9AAD865F5D1BC3A730750A7B6A198EC910A3E8D19CD.png "点击放大")

## 接口说明

|接口名|描述|
|:--|:--|
|[loadAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadad)(adParam: AdRequestParams, adOptions: AdOptions, listener: AdLoadListener): void|请求单广告位广告，通过AdRequestParams、AdOptions进行广告请求参数设置，通过AdLoadListener监听广告请求回调。|
|[showAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#showad)(ad: Advertisement, options: AdDisplayOptions, context?: common.UIAbilityContext): void|展示广告，通过AdDisplayOptions进行广告展示参数设置。<br><br>**说明：**为了保证广告能正确展示，该接口必须和请求广告接口配套使用。|

## 开发步骤

### 请求广告

1. 导入相关模块。
    
    1. import { abilityAccessCtrl, common, PermissionRequestResult } from '@kit.AbilityKit';
    2. import { advertising, identifier } from '@kit.AdsKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 获取OAID。
    
    若需提升广告推送精准度，可以在请求参数[AdRequestParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adrequestparams)中添加oaid属性。
    
    如何获取OAID参见[获取OAID信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/oaid-service)。
    
    说明
    
    使用以下示例中提供的测试广告位时，必须先获取OAID信息。
    
3. 请求单广告位广告。
    
    需要先创建一个AdLoader对象，通过AdLoader的[loadAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadad)方法请求广告，最后通过[AdLoadListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adloadlistener)来监听广告的加载状态。
    
    请求广告关键参数如下所示：
    
    |请求广告参数名|类型|必填|说明|
    |:--|:--|:--|:--|
    |adType|number|是|请求广告类型，插屏广告类型为12。|
    |adId|string|是|广告位ID。<br><br>- 如果仅调测广告，可使用测试广告位ID：testb4znbuh3n2。<br>- 如果要接入正式广告，则需要申请正式的广告位ID。可在应用发布前进入[流量变现官网](https://developer.huawei.com/consumer/cn/monetize)，点击“开始变现”，登录[鲸鸿动能媒体服务平台](https://developer.huawei.com/consumer/cn/service/ads/publisher/html/index.html?lang=zh)进行申请，具体操作详情请参见[展示位创建](https://developer.huawei.com/consumer/cn/doc/monetize/zhanshiweichuangjian-0000001132700049)。|
    |oaid|string|否|开放匿名设备标识符，用于精准推送广告。不填无法获取到个性化广告。|
    
    示例代码如下所示：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   private context: common.UIAbilityContext = this.getUIContext().getHostContext() as common.UIAbilityContext;
    
    5.   build() {
    6.     Column() {
    7.       Button('LoadAd')
    8.         .onClick(() => {
    9.           this.loadAd();
    10.         })
    11.     }
    12.     .width('100%')
    13.     .height('100%')
    14.     .justifyContent(FlexAlign.Center)
    15.   }
    
    16.   private async loadAd(): Promise<void> {
    17.     // 广告请求回调监听
    18.     const adLoadListener: advertising.AdLoadListener = {
    19.       onAdLoadFailure: (errorCode: number, errorMsg: string) => {
    20.         hilog.error(0x0000, 'testTag', `Failed to load ad. Code is ${errorCode}, message is ${errorMsg}`);
    21.       },
    22.       onAdLoadSuccess: (ads: Array<advertising.Advertisement>) => {
    23.         hilog.info(0x0000, 'testTag', 'Succeeded in loading ad');
    24.         // ...
    25.       }
    26.     };
    27.     // 广告请求参数
    28.     const adRequestParams: advertising.AdRequestParams = {
    29.       // 'testb4znbuh3n2'为测试专用的广告位ID，App正式发布时需要改为正式的广告位ID
    30.       adId: 'testb4znbuh3n2',
    31.       // 插屏广告类型
    32.       adType: 12,
    33.       // 开放匿名设备标识符
    34.       oaid: await requestOAID(this.context)
    35.     };
    36.     // 广告配置参数，开发者可根据项目实际情况设置
    37.     const adOptions: advertising.AdOptions = {};
    38.     // 创建AdLoader广告对象
    39.     const adLoader: advertising.AdLoader = new advertising.AdLoader(this.context);
    40.     try {
    41.       // 调用广告请求接口
    42.       adLoader.loadAd(adRequestParams, adOptions, adLoadListener);
    43.     } catch (e) {
    44.       hilog.error(0x0000, 'testTag', `Failed to load ad. Code is ${e.code}, message is ${e.message}`);
    45.     }
    46.   }
    47. }
    
    48. async function requestOAID(context: Context): Promise<string | undefined> {
    49.   // 向用户请求授权广告跨应用关联访问权限
    50.   let isPermissionGranted: boolean = false;
    51.   try {
    52.     const atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
    53.     const result: PermissionRequestResult =
    54.       await atManager.requestPermissionsFromUser(context, ['ohos.permission.APP_TRACKING_CONSENT']);
    55.     isPermissionGranted = result.authResults[0] === abilityAccessCtrl.GrantStatus.PERMISSION_GRANTED;
    56.   } catch (err) {
    57.     hilog.error(0x0000, 'testTag', `Failed to request permission. Code is ${err.code}, message is ${err.message}`);
    58.   }
    59.   if (isPermissionGranted) {
    60.     hilog.info(0x0000, 'testTag', 'Succeeded in requesting permission');
    61.     try {
    62.       const oaid = await identifier.getOAID();
    63.       hilog.info(0x0000, 'testTag', 'Succeeded in getting OAID');
    64.       return oaid;
    65.     } catch (err) {
    66.       hilog.error(0x0000, 'testTag', `Failed to get OAID. Code is ${err.code}, message is ${err.message}`);
    67.     }
    68.   } else {
    69.     hilog.error(0x0000, 'testTag', 'Failed to request permission. User rejected');
    70.   }
    71.   return undefined;
    72. }
    

### 事件订阅

1. 导入相关模块。
    
    1. import { BusinessError, commonEventManager } from '@kit.BasicServicesKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 事件订阅。
    
    开发者需要在应用中订阅com.huawei.hms.pps.action.PPS_INTERSTITIAL_STATUS_CHANGED事件来监听插屏广告页面变化。
    
    在订阅到公共事件后，可以从[CommonEventData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-commonevent-commoneventdata)的parameters参数中使用interstitial_ad_status作为key值获取插屏广告页面变化状态。
    
    涉及的页面变化状态如下所示：
    
    |页面变化状态|说明|
    |:--|:--|
    |onAdOpen|打开广告。|
    |onAdClick|点击广告。|
    |onAdClose|关闭广告。|
    |onVideoPlayBegin|广告视频开始播放。|
    |onVideoPlayEnd|广告视频播放结束。|
    
    示例代码如下所示：
    
    1. const KEY_INTERSTITIAL_STATUS = 'interstitial_ad_status';
    
    2. export class InterstitialAdStatusHandler {
    3.   // 用于保存创建成功的订阅者对象，后续使用其完成订阅及退订的动作
    4.   private subscriber: commonEventManager.CommonEventSubscriber | null = null;
    
    5.   // 订阅方法，需要在每次展示广告前调用
    6.   public registerPPSReceiver(): void {
    7.     if (this.subscriber) {
    8.       this.unRegisterPPSReceiver();
    9.     }
    10.     // 订阅者信息
    11.     const subscribeInfo: commonEventManager.CommonEventSubscribeInfo = {
    12.       events: ['com.huawei.hms.pps.action.PPS_INTERSTITIAL_STATUS_CHANGED'],
    13.       // publisherBundleName被设置为"com.huawei.hms.adsservice",这意味着只有来自该包名的事件才会被订阅者接受和处理。
    14.       // 如果没有明确声明publisherBundleName，那么订阅者可能会收到来自其它包名的伪造事件，从而导致安全性问题或误导。
    15.       publisherBundleName: 'com.huawei.hms.adsservice'
    16.     };
    17.     // 创建订阅者回调
    18.     commonEventManager.createSubscriber(subscribeInfo,
    19.       (err: BusinessError, commonEventSubscriber: commonEventManager.CommonEventSubscriber) => {
    20.         if (err) {
    21.           hilog.error(0x0000, 'testTag', `Failed to create subscriber. Code is ${err.code}, message is ${err.message}`);
    22.           return;
    23.         }
    24.         hilog.info(0x0000, 'testTag', 'Succeeded in creating subscriber');
    25.         this.subscriber = commonEventSubscriber;
    26.         // 订阅公共事件回调
    27.         commonEventManager.subscribe(this.subscriber,
    28.           (err: BusinessError, commonEventData: commonEventManager.CommonEventData) => {
    29.             if (err) {
    30.               hilog.error(0x0000, 'testTag', `Failed to subscribe. Code is ${err.code}, message is ${err.message}`);
    31.             } else {
    32.               // 订阅者成功接收到公共事件
    33.               hilog.info(0x0000, 'testTag', 'Succeeded in subscribing data');
    34.               // 获取插屏广告页面变化状态
    35.               const status: string = commonEventData?.parameters?.[KEY_INTERSTITIAL_STATUS];
    36.               switch (status) {
    37.                 case 'onAdOpen':
    38.                   hilog.info(0x0000, 'testTag', 'Status is onAdOpen');
    39.                   break;
    40.                 case 'onAdClick':
    41.                   hilog.info(0x0000, 'testTag', 'Status is onAdClick');
    42.                   break;
    43.                 case 'onAdClose':
    44.                   hilog.info(0x0000, 'testTag', 'Status is onAdClose');
    45.                   this.unRegisterPPSReceiver();
    46.                   break;
    47.                 case 'onVideoPlayBegin':
    48.                   hilog.info(0x0000, 'testTag', 'Status is onVideoPlayBegin');
    49.                   break;
    50.                 case 'onVideoPlayEnd':
    51.                   hilog.info(0x0000, 'testTag', 'Status is onVideoPlayEnd');
    52.                   break;
    53.                 default:
    54.                   break;
    55.               }
    56.             }
    57.           });
    58.       });
    59.   }
    
    60.   // 取消订阅
    61.   public unRegisterPPSReceiver(): void {
    62.     commonEventManager.unsubscribe(this.subscriber, (err: BusinessError) => {
    63.       if (err) {
    64.         hilog.error(0x0000, 'testTag', `Failed to unsubscribe. Code is ${err.code}, message is ${err.message}`);
    65.       } else {
    66.         hilog.info(0x0000, 'testTag', 'Succeeded in unsubscribing');
    67.         this.subscriber = null;
    68.       }
    69.     });
    70.   }
    71. }
    

### 展示广告

1. 导入相关模块。
    
    1. import { common } from '@kit.AbilityKit';
    2. import { advertising } from '@kit.AdsKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    4. // 事件订阅步骤中创建的文件
    5. import { InterstitialAdStatusHandler } from './InterstitialAdStatusHandler';
    
2. 展示广告。
    
    开发者需要调用[showAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#showad)方法来展示广告，ads为[请求广告](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-interstitial#section0237145185117)返回的广告信息，在每次展示广告前需要注册[事件订阅](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-interstitial#section14755121210539)中定义的监听器。
    
    示例代码如下所示：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   private context: common.UIAbilityContext = this.getUIContext().getHostContext() as common.UIAbilityContext;
    
    5.   build() {
    6.     // ...
    7.   }
    
    8.   private async loadAd(): Promise<void> {
    9.     // 广告请求回调监听
    10.     const adLoadListener: advertising.AdLoadListener = {
    11.       onAdLoadFailure: (errorCode: number, errorMsg: string) => {
    12.         hilog.error(0x0000, 'testTag', `Failed to load ad. Code is ${errorCode}, message is ${errorMsg}`);
    13.       },
    14.       onAdLoadSuccess: (ads: Array<advertising.Advertisement>) => {
    15.         hilog.info(0x0000, 'testTag', 'Succeeded in loading ad');
    16.         try {
    17.           // 注册插屏广告状态监听器
    18.           new InterstitialAdStatusHandler().registerPPSReceiver();
    19.           // 广告展示参数，开发者可根据项目实际情况设置
    20.           const adDisplayOptions: advertising.AdDisplayOptions = {
    21.             // 是否静音
    22.             mute: true
    23.           };
    24.           // 此处ads[0]表示请求到的第一个广告，开发者可根据项目实际情况选择
    25.           advertising.showAd(ads[0], adDisplayOptions, this.context);
    26.         } catch (e) {
    27.           hilog.error(0x0000, 'testTag', `Failed to show ad. Code is ${e.code}, message is ${e.message}`);
    28.         }
    29.       }
    30.     };
    31.     // ...
    32.   }
    33. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-reward "激励广告")
# 开屏广告

更新时间: 2025-12-16 16:37

## 场景介绍

开屏广告是一种在应用启动时且在应用主界面显示之前需要被展示的广告。您需要预先为App设计一张开屏默认的Slogan图片，确保在未获得到开屏广告之前展示默认的Slogan，提供良好的用户体验。

开屏广告分为全屏开屏广告、半屏开屏广告，其中全屏开屏广告展示形式为广告铺满整个页面；半屏开屏广告展示形式会根据媒体页面自定义布局渲染广告、icon和版权信息，一般情况下建议将icon和版权信息展示在广告下方。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163734.43523459207303452461777687570390:50001231000000:2800:D886C45C69830C775305C2F18C387D7EF22B7D0FCDA7D508861D10E2FB4C9517.png)

## 接口说明

|接口名|描述|
|:--|:--|
|[loadAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadad)(adParam: AdRequestParams, adOptions: AdOptions, listener: AdLoadListener): void|请求单广告位广告，通过AdRequestParams、AdOptions进行广告请求参数设置，通过AdLoadListener监听广告请求回调。|
|[AdComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-adcomponent)({ads: advertising.Advertisement[], displayOptions: advertising.AdDisplayOptions, interactionListener: advertising.AdInteractionListener, @BuilderParam adRenderer?: () => void, @Prop rollPlayState?: number})|展示广告，通过AdDisplayOptions进行广告展示参数设置，通过AdInteractionListener监听广告状态回调。<br><br>**说明：**为了保证广告能正确展示，该接口必须和请求广告接口配套使用。|

## 开发步骤

### 请求广告

1. 导入相关模块。
    
    1. import { abilityAccessCtrl, common, PermissionRequestResult } from '@kit.AbilityKit';
    2. import { advertising, identifier } from '@kit.AdsKit';
    3. import { router, window } from '@kit.ArkUI';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    5. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 获取OAID。
    
    若需提升广告推送精准度，可以在请求参数[AdRequestParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adrequestparams)中添加oaid属性。
    
    如何获取OAID参见[获取OAID信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/oaid-service)。
    
    说明
    
    使用以下示例中提供的测试广告位时，必须先获取OAID信息。
    
3. 请求单广告位广告。
    
    需要创建一个AdLoader对象，通过AdLoader的[loadAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadad)方法请求广告，最后通过[AdLoadListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adloadlistener)来监听广告的加载状态。测试开屏广告时，需要使用专门的测试广告位来获取测试开屏广告，示例代码中提供了两种开屏广告类型对应的广告位：半屏开屏（图片）（testq6zq98hecj）和全屏开屏（视频）（testd7c5cewoj6），测试广告位ID仅作为调试使用，不可用于广告变现。
    
    请求广告关键参数如下所示：
    
    |请求广告参数名|类型|必填|说明|
    |:--|:--|:--|:--|
    |adType|number|是|请求广告类型，开屏广告类型为1。|
    |adId|string|是|广告位ID。<br><br>- 如果仅调测广告，可使用测试广告位ID：testq6zq98hecj半屏开屏（图片）和testd7c5cewoj6全屏开屏（视频）。<br>- 如果要接入正式广告，则需要申请正式的广告位ID。可在应用发布前进入[流量变现官网](https://developer.huawei.com/consumer/cn/monetize)，点击“开始变现”，登录[鲸鸿动能媒体服务平台](https://developer.huawei.com/consumer/cn/service/ads/publisher/html/index.html?lang=zh)进行申请，具体操作详情请参见[展示位创建](https://developer.huawei.com/consumer/cn/doc/monetize/zhanshiweichuangjian-0000001132700049)。|
    |adCount|number|否|广告数量。|
    |orientation|number|否|媒体请求广告的屏幕方向。1表示竖屏，0表示横屏，不设置则默认为1。当前未上架横屏开屏素材，若设置请求屏幕方向为横屏则不展示开屏广告。如果媒体设置应用固定横屏展示，但该参数未设置或者设置为1，则展示效果会受影响。|
    
    |返回广告参数名|类型|说明|
    |:--|:--|:--|
    |isFullScreen|boolean|标识返回的广告是否为全屏，true为全屏广告，false为半屏广告。|
    
    说明
    
    1、如果超时没有请求到广告，应用自行跳转到默认首页。
    
    2、为保证开屏展示效果，建议开发者在请求广告前，设置屏幕方向为竖屏。
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   @State ad: advertising.Advertisement | undefined = undefined;
    5.   // ...
    6.   private context: common.UIAbilityContext = this.getUIContext().getHostContext() as common.UIAbilityContext;
    7.   // 是否超时
    8.   private isTimeOut: boolean = false;
    9.   // 超时时间(单位毫秒)，开发者可根据实际情况修改
    10.   private timeOutDuration: number = 1000;
    11.   // 超时index
    12.   private timeOutIndex: number = -1;
    
    13.   aboutToAppear(): void {
    14.     // 开启全屏模式沉浸页面
    15.     this.setWindowLayoutFullScreen(true);
    16.     // 设置屏幕方向为竖屏
    17.     this.setWindowPreferredOrientation(window.Orientation.PORTRAIT);
    18.     // 调用loadAd加载广告
    19.     // ...
    20.   }
    
    21.   aboutToDisappear(): void {
    22.     // 关闭全屏模式，开发者可根据实际情况修改
    23.     this.setWindowLayoutFullScreen(false);
    24.     // 设置屏幕方向为默认值，开发者可根据实际情况修改
    25.     this.setWindowPreferredOrientation(window.Orientation.UNSPECIFIED);
    26.   }
    
    27.   private async setWindowLayoutFullScreen(isLayoutFullScreen: boolean): Promise<void> {
    28.     try {
    29.       const win: window.Window = await window.getLastWindow(this.context);
    30.       await win.setWindowLayoutFullScreen(isLayoutFullScreen);
    31.     } catch (e) {
    32.       hilog.error(0x0000, 'testTag', `Failed to set window layout. Code is ${e.code}, message is ${e.message}`);
    33.     }
    34.   }
    
    35.   private async setWindowPreferredOrientation(orientation: Orientation): Promise<void> {
    36.     try {
    37.       const win: window.Window = await window.getLastWindow(this.context);
    38.       await win.setPreferredOrientation(orientation);
    39.     } catch (e) {
    40.       hilog.error(0x0000, 'testTag', `Failed to set preferred orientation. Code is ${e.code}, message is ${e.message}`);
    41.     }
    42.   }
    
    43.   build() {
    44.     // ...
    45.   }
    
    46.   // ...
    47.   private async loadAd(adId: string): Promise<void> {
    48.     // 广告请求参数
    49.     const adRequestParams: advertising.AdRequestParams = {
    50.       // 广告位ID
    51.       adId: adId,
    52.       // 开屏广告类型
    53.       adType: 1,
    54.       // 请求的广告数量
    55.       adCount: 1,
    56.       // 开放匿名设备标识符
    57.       oaid: await requestOAID(this.context)
    58.     };
    59.     // 广告请求回调监听
    60.     const adLoadListener: advertising.AdLoadListener = {
    61.       onAdLoadFailure: (errorCode: number, errorMsg: string) => {
    62.         hilog.error(0x0000, 'testTag', `Failed to load ad. Code is ${errorCode}, message is ${errorMsg}`);
    63.       },
    64.       onAdLoadSuccess: (ads: Array<advertising.Advertisement>) => {
    65.         clearTimeout(this.timeOutIndex);
    66.         if (this.isTimeOut) {
    67.           return;
    68.         }
    69.         hilog.info(0x0000, 'testTag', 'Succeeded in loading ad');
    70.         this.ad = ads[0];
    71.       }
    72.     };
    73.     // 广告配置参数，开发者可根据项目实际情况设置
    74.     const adOptions: advertising.AdOptions = {};
    75.     // 创建AdLoader广告对象
    76.     const adLoader: advertising.AdLoader = new advertising.AdLoader(this.context);
    77.     // 启动超时定时器
    78.     this.timeOutHandler();
    79.     try {
    80.       // 调用广告请求接口
    81.       adLoader.loadAd(adRequestParams, adOptions, adLoadListener);
    82.     } catch (e) {
    83.       hilog.error(0x0000, 'testTag', `Failed to load ad. Code is ${e.code}, message is ${e.message}`);
    84.     }
    85.   }
    
    86.   private timeOutHandler(): void {
    87.     this.isTimeOut = false;
    88.     // 超时处理
    89.     this.timeOutIndex = setTimeout(() => {
    90.       this.isTimeOut = true;
    91.       this.routeToHome();
    92.       hilog.error(0x0000, 'testTag', 'Load ad time out');
    93.     }, this.timeOutDuration);
    94.   }
    
    95.   private routeToHome(): void {
    96.     // 开发者可根据项目实际情况修改超时之后要跳转的目标页面
    97.     this.getUIContext().getRouter().replaceUrl({ url: 'pages/Index' }, router.RouterMode.Single)
    98.       .catch((e: BusinessError) => {
    99.         hilog.error(0x0000, 'testTag', `Failed to route to home. Code is ${e.code}, message is ${e.message}`);
    100.       });
    101.   }
    102. }
    
    103. async function requestOAID(context: Context): Promise<string | undefined> {
    104.   // 向用户请求授权广告跨应用关联访问权限
    105.   let isPermissionGranted: boolean = false;
    106.   try {
    107.     const atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
    108.     const result: PermissionRequestResult =
    109.       await atManager.requestPermissionsFromUser(context, ['ohos.permission.APP_TRACKING_CONSENT']);
    110.     isPermissionGranted = result.authResults[0] === abilityAccessCtrl.GrantStatus.PERMISSION_GRANTED;
    111.   } catch (err) {
    112.     hilog.error(0x0000, 'testTag', `Failed to request permission. Code is ${err.code}, message is ${err.message}`);
    113.   }
    114.   if (isPermissionGranted) {
    115.     hilog.info(0x0000, 'testTag', 'Succeeded in requesting permission');
    116.     try {
    117.       const oaid = await identifier.getOAID();
    118.       hilog.info(0x0000, 'testTag', 'Succeeded in getting OAID');
    119.       return oaid;
    120.     } catch (err) {
    121.       hilog.error(0x0000, 'testTag', `Failed to get OAID. Code is ${err.code}, message is ${err.message}`);
    122.     }
    123.   } else {
    124.     hilog.error(0x0000, 'testTag', 'Failed to request permission. User rejected');
    125.   }
    126.   return undefined;
    127. }
    

### 展示广告

1. 导入相关模块。
    
    1. import { AdComponent, advertising } from '@kit.AdsKit';
    2. import { router } from '@kit.ArkUI';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 展示广告。
    
    展示广告通过[AdInteractionListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adinteractionlistener)监听广告状态回调，涉及的回调状态如下所示：
    
    |回调状态|说明|使用建议|
    |:--|:--|:--|
    |onAdOpen|打开广告。|-|
    |onAdClick|点击广告。|-|
    |onAdClose|关闭广告。|广告倒计时结束、用户点击跳过按钮或广告从后台返回时触发，需要跳转到应用首页。|
    |onAdFail|广告加载失败。|广告展示失败时触发，需要跳转到应用首页。|
    
    说明
    
    1、请求到广告之前需要展示默认的Slogan图片。
    
    2、由请求广告中获取的isFullScreen参数判断展示全屏或者半屏广告。
    
    3、目前只支持展示竖屏广告。
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   @State ad: advertising.Advertisement | undefined = undefined;
    5.   // 广告展示参数
    6.   private adDisplayOptions: advertising.AdDisplayOptions = {
    7.     // 是否静音
    8.     mute: true
    9.   };
    10.   // ...
    
    11.   build() {
    12.     RelativeContainer() {
    13.       // 展示开发者自定义Slogan图片
    14.       Image($r('app.media.slogan'))
    15.         .width('100%')
    16.         .height('100%')
    17.         .zIndex(0)
    18.       // 展示开发者自定义icon、应用名称、版权信息
    19.       Column() {
    20.         Row() {
    21.           Image($r('app.media.video'))
    22.             .width(24)
    23.             .height(24)
    24.             .margin(8)
    25.           Text($r('app.string.video'))
    26.             .fontColor('#1A1A1A')
    27.             .fontSize(16)
    28.         }
    29.         .margin({ bottom: 8 })
    
    30.         Column() {
    31.           Text($r('app.string.copyright'))
    32.             .fontColor('#1A1A1A')
    33.             .fontSize(9)
    34.         }
    35.       }
    36.       .zIndex(1)
    37.       .alignRules({ bottom: { anchor: '__container__', align: VerticalAlign.Bottom } })
    38.       .width('100%')
    39.       .height('13%')
    
    40.       if (this.ad) {
    41.         if (this.ad.isFullScreen) {
    42.           // 全屏开屏广告
    43.           this.splashFullScreen()
    44.         } else {
    45.           // 半屏开屏广告
    46.           this.splashHalfScreen()
    47.         }
    48.       }
    49.     }
    50.     .width('100%')
    51.     .height('100%')
    52.   }
    
    53.   /**
    54.    * 半屏开屏广告
    55.    */
    56.   @Builder
    57.   private splashHalfScreen() {
    58.     AdComponent({
    59.       ads: [this.ad!],
    60.       displayOptions: this.adDisplayOptions,
    61.       interactionListener: {
    62.         onStatusChanged: (status: string, ad: advertising.Advertisement, data: string) => {
    63.           switch (status) {
    64.             case 'onAdOpen':
    65.               hilog.info(0x0000, 'testTag', 'Status is onAdOpen');
    66.               break;
    67.             case 'onAdClick':
    68.               hilog.info(0x0000, 'testTag', 'Status is onAdClick');
    69.               break;
    70.             case 'onAdClose':
    71.               hilog.info(0x0000, 'testTag', 'Status is onAdClose');
    72.               this.routeToHome();
    73.               break;
    74.             case 'onAdFail':
    75.               hilog.info(0x0000, 'testTag', 'Status is onAdFail');
    76.               this.routeToHome();
    77.               break;
    78.           }
    79.         }
    80.       }
    81.     })
    82.       .zIndex(1)
    83.       .width('100%')
    84.       .height('87%')
    85.       // 自定义组件动画
    86.       .transition(TransitionEffect.OPACITY.animation({ duration: 1000, curve: Curve.Friction}))
    87.       .alignRules({ top: { anchor: '__container__', align: VerticalAlign.Top } })
    88.   }
    
    89.   /**
    90.    * 全屏开屏广告
    91.    */
    92.   @Builder
    93.   private splashFullScreen() {
    94.     AdComponent({
    95.       ads: [this.ad!],
    96.       displayOptions: this.adDisplayOptions,
    97.       interactionListener: {
    98.         onStatusChanged: (status: string, ad: advertising.Advertisement, data: string) => {
    99.           switch (status) {
    100.             case 'onAdOpen':
    101.               hilog.info(0x0000, 'testTag', 'Status is onAdOpen');
    102.               break;
    103.             case 'onAdClick':
    104.               hilog.info(0x0000, 'testTag', 'Status is onAdClick');
    105.               break;
    106.             case 'onAdClose':
    107.               hilog.info(0x0000, 'testTag', 'Status is onAdClose');
    108.               this.routeToHome();
    109.               break;
    110.             case 'onAdFail':
    111.               hilog.info(0x0000, 'testTag', 'Status is onAdFail');
    112.               this.routeToHome();
    113.               break;
    114.           }
    115.         }
    116.       }
    117.     })
    118.       .zIndex(1)
    119.       .width('100%')
    120.       .height('100%')
    121.   }
    122.   // ...
    
    123.   private routeToHome(): void {
    124.     // 开发者可根据项目实际情况修改超时之后要跳转的目标页面
    125.     this.getUIContext().getRouter().replaceUrl({ url: 'pages/Index' }, router.RouterMode.Single)
    126.       .catch((e: BusinessError) => {
    127.         hilog.error(0x0000, 'testTag', `Failed to route to home. Code is ${e.code}, message is ${e.message}`);
    128.       });
    129.   }
    130. }
    
    131. // ...
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-interstitial "插屏广告")
# 贴片广告

更新时间: 2025-12-16 16:37

## 场景介绍

贴片广告是一种在视频播放前、视频播放中或视频播放结束后插入的视频或图片广告。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163739.14086114086639384126142061359948:50001231000000:2800:3FF1DF0DA025AD559BB1928673AB37375A1F7F806885EC6E498A6FA83007345D.png)

## 接口说明

|接口名|描述|
|:--|:--|
|[loadAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadad)(adParam: AdRequestParams, adOptions: AdOptions, listener: AdLoadListener): void|请求单广告位广告，通过AdRequestParams、AdOptions进行广告请求参数设置，通过AdLoadListener监听广告请求回调。|
|[AdComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-adcomponent)({ads: advertising.Advertisement[], displayOptions: advertising.AdDisplayOptions, interactionListener: advertising.AdInteractionListener, @BuilderParam adRenderer?: () => void, @Prop rollPlayState?: number})|展示广告，通过AdDisplayOptions进行广告展示参数设置，通过AdInteractionListener监听广告状态回调。<br><br>**说明：**为了保证广告能正确展示，该接口必须和请求广告接口配套使用。|

## 开发步骤

### 请求广告

1. 导入相关模块。
    
    1. import { abilityAccessCtrl, common, PermissionRequestResult } from '@kit.AbilityKit';
    2. import { advertising, identifier } from '@kit.AdsKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 获取OAID。
    
    若需提升广告推送精准度，可以在请求参数[AdRequestParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adrequestparams)中添加oaid属性。
    
    如何获取OAID参见[获取OAID信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/oaid-service)。
    
    说明
    
    使用以下示例中提供的测试广告位时，必须先获取OAID信息。
    
3. 请求单广告位广告。
    
    需要创建一个AdLoader对象，通过AdLoader的[loadAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadad)方法请求广告，最后通过[AdLoadListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adloadlistener)来监听广告的加载状态。
    
    在请求贴片广告时，需要在[AdOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adoptions)中设置参数：totalDuration。
    
    请求广告关键参数如下所示：
    
    |请求广告参数名|类型|必填|说明|
    |:--|:--|:--|:--|
    |adType|number|是|请求广告类型，贴片广告类型为60。|
    |adId|string|是|广告位ID。<br><br>- 如果仅调测广告，可使用测试广告位ID：testy3cglm3pj0。<br>- 如果要接入正式广告，则需要申请正式的广告位ID。可在应用发布前进入[流量变现官网](https://developer.huawei.com/consumer/cn/monetize)，点击“开始变现”，登录[鲸鸿动能媒体服务平台](https://developer.huawei.com/consumer/cn/service/ads/publisher/html/index.html?lang=zh)进行申请，具体操作详情请参见[展示位创建](https://developer.huawei.com/consumer/cn/doc/monetize/zhanshiweichuangjian-0000001132700049)。|
    |oaid|string|否|开放匿名设备标识符，用于精准推送广告。不填无法获取到个性化广告。|
    
    示例代码如下所示：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   // 请求到的广告内容
    5.   @State ads: advertising.Advertisement[] = [];
    6.   // ...
    7.   private context: common.UIAbilityContext = this.getUIContext().getHostContext() as common.UIAbilityContext;
    
    8.   aboutToAppear(): void {
    9.     // 调用loadAd加载广告
    10.     this.loadAd();
    11.   }
    
    12.   // ...
    
    13.   build() {
    14.     // ...
    15.   }
    
    16.   // ...
    
    17.   private async loadAd(): Promise<void> {
    18.     // 广告请求回调监听
    19.     const adLoadListener: advertising.AdLoadListener = {
    20.       onAdLoadFailure: (errorCode: number, errorMsg: string) => {
    21.         hilog.error(0x0000, 'testTag', `Failed to load ad. Code is ${errorCode}, message is ${errorMsg}`);
    22.       },
    23.       onAdLoadSuccess: (ads: Array<advertising.Advertisement>) => {
    24.         hilog.info(0x0000, 'testTag', 'Succeeded in loading ad');
    25.         this.ads = ads;
    26.       }
    27.     };
    28.     // 广告请求参数
    29.     const adRequestParams: advertising.AdRequestParams = {
    30.       // 'testy3cglm3pj0'为测试专用的广告位ID，App正式发布时需要改为正式的广告位ID
    31.       adId: 'testy3cglm3pj0',
    32.       // 贴片广告类型
    33.       adType: 60,
    34.       // 用于区分普通在线请求和素材预加载请求 true: 素材预加载请求 false: 普通在线请求
    35.       isPreload: false,
    36.       // 开放匿名设备标识符
    37.       oaid: await requestOAID(this.context)
    38.     };
    39.     // 广告配置参数，开发者可根据项目实际情况设置
    40.     const adOptions: advertising.AdOptions = {
    41.       // 设置贴片广告展示时长（贴片广告必填）
    42.       totalDuration: 30
    43.     };
    44.     // 创建AdLoader广告对象
    45.     const adLoader: advertising.AdLoader = new advertising.AdLoader(this.context);
    46.     try {
    47.       // 调用广告请求接口
    48.       adLoader.loadAd(adRequestParams, adOptions, adLoadListener);
    49.     } catch (e) {
    50.       hilog.error(0x0000, 'testTag', `Failed to load ad. Code is ${e.code}, message is ${e.message}`);
    51.     }
    52.   }
    53. }
    
    54. async function requestOAID(context: Context): Promise<string | undefined> {
    55.   // 向用户请求授权广告跨应用关联访问权限
    56.   let isPermissionGranted: boolean = false;
    57.   try {
    58.     const atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
    59.     const result: PermissionRequestResult =
    60.       await atManager.requestPermissionsFromUser(context, ['ohos.permission.APP_TRACKING_CONSENT']);
    61.     isPermissionGranted = result.authResults[0] === abilityAccessCtrl.GrantStatus.PERMISSION_GRANTED;
    62.   } catch (err) {
    63.     hilog.error(0x0000, 'testTag', `Failed to request permission. Code is ${err.code}, message is ${err.message}`);
    64.   }
    65.   if (isPermissionGranted) {
    66.     hilog.info(0x0000, 'testTag', 'Succeeded in requesting permission');
    67.     try {
    68.       const oaid = await identifier.getOAID();
    69.       hilog.info(0x0000, 'testTag', 'Succeeded in getting OAID');
    70.       return oaid;
    71.     } catch (err) {
    72.       hilog.error(0x0000, 'testTag', `Failed to get OAID. Code is ${err.code}, message is ${err.message}`);
    73.     }
    74.   } else {
    75.     hilog.error(0x0000, 'testTag', 'Failed to request permission. User rejected');
    76.   }
    77.   return undefined;
    78. }
    

### 展示广告

1. 导入相关模块。
    
    1. import { common } from '@kit.AbilityKit';
    2. import { AdComponent, advertising } from '@kit.AdsKit';
    3. import { window } from '@kit.ArkUI';
    4. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 展示广告。
    
    展示广告通过[AdInteractionListener](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adinteractionlistener)监听广告状态回调，涉及的回调状态如下所示：
    
    |回调状态|说明|扩展信息|使用建议|
    |:--|:--|:--|:--|
    |onAdFail|广告加载失败。|-|广告展示失败时触发，需要将广告组件隐藏，播放正片。|
    |onPortrait|全屏状态下点击返回按钮。|-|用户在全屏状态下点击返回按钮时触发，需要设置屏幕方向为竖屏，按需显示导航栏、状态栏、底部导航条和设置广告组件宽高。|
    |onLandscape|竖屏状态下点击全屏按钮。|-|用户在竖屏状态下点击全屏按钮时触发，需要设置屏幕方向为横屏，按需隐藏导航栏、状态栏、底部导航条和设置广告组件宽高。|
    |onMediaProgress|广告播放进度。|- playTime：类型number，单位ms，广告播放时长。<br>- percentage：类型number，单位百分比，广告播放进度。|-|
    |onMediaStart|广告开始播放。|- playTime：类型number，单位ms，广告播放时长。|-|
    |onMediaPause|广告暂停播放。|- playTime：类型number，单位ms，广告播放时长。|-|
    |onMediaStop|广告停止播放。|- playTime：类型number，单位ms，广告播放时长。|-|
    |onMediaComplete|广告播放完成。|- playTime：类型number，单位ms，广告播放时长。|单个广告播放完成时触发，当所有广告播放完成后，需要将广告组件隐藏，播放正片。|
    |onMediaError|广告播放失败。|- playTime：类型number，单位ms，广告播放时长，-1为异常值。<br>- errorCode：类型number，错误码ID。<br>- errorMsg：类型string，错误信息。<br><br>错误码的详细介绍请参见AVPlayer.[on('error')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media-avplayer#onerror9)错误码。|-|
    |onMediaCountdown|广告倒计时。|- countdownTime：类型number，单位s，倒计时时长。|广告倒计时时触发，需要根据扩展信息的倒计时时长绘制倒计时控件。|
    |onBackClicked|点击返回按钮。|-|用户在非全屏状态下或系统锁定全屏状态下点击返回按钮时触发，需要返回上一页面。|
    
    在您的页面中使用AdComponent组件展示贴片广告。以前贴广告为例，前贴广告播放完成后进入正片播放。
    
    示例代码如下所示：
    
    1. @Entry
    2. @Component
    3. struct Index {
    4.   // 请求到的广告内容
    5.   @State ads: advertising.Advertisement[] = [];
    6.   // 倒计时文案
    7.   @State countDownText: string = '';
    8.   // 贴片广告播放状态
    9.   @State rollPlayState: number = 1;
    10.   // 是否播放正片
    11.   @State isPlayVideo: boolean = false;
    12.   // 视频宽高比
    13.   @State ratio: number = 16 / 9;
    14.   // 广告展示参数，开发者可根据项目实际情况设置
    15.   private adDisplayOptions: advertising.AdDisplayOptions = {
    16.     // 是否静音
    17.     mute: true
    18.   };
    19.   // 已经播放的贴片广告数量
    20.   private playedAdSize: number = 0;
    21.   // 用于渲染右上角倒计时
    22.   private countDownTxtPlaceholder: string = '%d | VIP免广告';
    23.   private context: common.UIAbilityContext = this.getUIContext().getHostContext() as common.UIAbilityContext;
    
    24.   // ...
    
    25.   aboutToDisappear(): void {
    26.     // 设置屏幕方向为默认值，开发者可根据项目实际情况修改
    27.     this.setWindowPreferredOrientation(window.Orientation.UNSPECIFIED);
    28.     // 显示导航栏、状态栏、底部导航条，开发者可根据项目实际情况修改
    29.     this.setWindowSystemBar(['status', 'navigation']);
    30.   }
    
    31.   build() {
    32.     Stack({ alignContent: Alignment.TopEnd }) {
    33.       if (!this.isPlayVideo && this.ads.length > 0) {
    34.         AdComponent({
    35.           ads: [...this.ads],
    36.           rollPlayState: this.rollPlayState,
    37.           displayOptions: this.adDisplayOptions,
    38.           interactionListener: {
    39.             // 广告状态变化回调
    40.             onStatusChanged: (status: string, ad: advertising.Advertisement, data: string) => {
    41.               switch (status) {
    42.                 case 'onAdFail':
    43.                   hilog.info(0x0000, 'testTag', 'Status is onAdFail');
    44.                   this.isPlayVideo = true;
    45.                   break;
    46.                 case 'onPortrait':
    47.                   hilog.info(0x0000, 'testTag', 'Status is onPortrait');
    48.                   // 设置屏幕方向为竖屏
    49.                   this.setWindowPreferredOrientation(window.Orientation.PORTRAIT);
    50.                   // 显示导航栏、状态栏、底部导航条
    51.                   this.setWindowSystemBar(['status', 'navigation']);
    52.                   // 竖屏时还原宽高比
    53.                   this.ratio = 16 / 9;
    54.                   break;
    55.                 case 'onLandscape':
    56.                   hilog.info(0x0000, 'testTag', 'Status is onLandscape');
    57.                   // 设置屏幕方向为横屏
    58.                   this.setWindowPreferredOrientation(window.Orientation.LANDSCAPE);
    59.                   // 隐藏导航栏、状态栏、底部导航条
    60.                   this.setWindowSystemBar([]);
    61.                   // 横屏时忽略宽高比
    62.                   this.ratio = -1;
    63.                   break;
    64.                 case 'onMediaProgress':
    65.                   hilog.info(0x0000, 'testTag', 'Status is onMediaProgress');
    66.                   break;
    67.                 case 'onMediaStart':
    68.                   hilog.info(0x0000, 'testTag', 'Status is onMediaStart');
    69.                   break;
    70.                 case 'onMediaPause':
    71.                   hilog.info(0x0000, 'testTag', 'Status is onMediaPause');
    72.                   break;
    73.                 case 'onMediaStop':
    74.                   hilog.info(0x0000, 'testTag', 'Status is onMediaStop');
    75.                   break;
    76.                 case 'onMediaComplete':
    77.                   hilog.info(0x0000, 'testTag', 'Status is onMediaComplete');
    78.                   // 所有广告都播放完毕后，开始播放正片
    79.                   this.playedAdSize++;
    80.                   if (this.playedAdSize === this.ads.length) {
    81.                     this.isPlayVideo = true;
    82.                   }
    83.                   break;
    84.                 case 'onMediaError':
    85.                   hilog.error(0x0000, 'testTag', 'Status is onMediaError');
    86.                   break;
    87.                 case 'onMediaCountdown':
    88.                   hilog.info(0x0000, 'testTag', 'Status is onMediaCountdown');
    89.                   const parseData: Record<string, Object> = this.safeParseData(data);
    90.                   this.countDownText = this.countDownTxtPlaceholder.replace('%d', String(parseData.countdownTime));
    91.                   break;
    92.                 case 'onBackClicked':
    93.                   hilog.info(0x0000, 'testTag', 'Status is onBackClicked');
    94.                   this.getUIContext().getRouter().back();
    95.                   break;
    96.               }
    97.             }
    98.           }
    99.         })
    100.           .visibility(!this.isPlayVideo ? Visibility.Visible : Visibility.None)
    101.           .width('100%')
    102.           .height('100%')
    
    103.         Text(this.countDownText)
    104.           .fontSize(12)
    105.           .lineHeight(12)
    106.           .maxLines(1)
    107.           .textAlign(TextAlign.Center)
    108.           .fontColor(Color.White)
    109.           .textOverflow({ overflow: TextOverflow.Ellipsis })
    110.           .backgroundColor('#66000000')
    111.           .border({ radius: 25 })
    112.           .padding(8)
    113.           .margin(16)
    114.           .height(24)
    115.           .onClick(() => {
    116.             hilog.info(0x0000, 'testTag', 'OnVipClicked, do something...');
    117.             this.isPlayVideo = true;
    118.           })
    119.           .visibility(this.countDownText ? Visibility.Visible : Visibility.None)
    120.       }
    
    121.       Video({
    122.         // 广告后播放的视频，开发者需根据项目实际情况设置
    123.         src: $rawfile('videoTest.mp4'),
    124.         // 播放视频的预览图，开发者需根据项目实际情况设置
    125.         previewUri: $r('app.media.video_preview'),
    126.         controller: new VideoController()
    127.       })
    128.         .visibility(this.isPlayVideo ? Visibility.Visible : Visibility.None)
    129.         .autoPlay(this.isPlayVideo)
    130.         .controls(false)
    131.         .width('100%')
    132.         .height('100%')
    133.     }
    134.     .width('100%')
    135.     .height('100%')
    136.     .aspectRatio(this.ratio)
    137.   }
    
    138.   private async setWindowPreferredOrientation(orientation: Orientation): Promise<void> {
    139.     try {
    140.       const win: window.Window = await window.getLastWindow(this.context);
    141.       await win.setPreferredOrientation(orientation);
    142.     } catch (e) {
    143.       hilog.error(0x0000, 'testTag', `Failed to set preferred orientation. Code is ${e.code}, message is ${e.message}`);
    144.     }
    145.   }
    
    146.   private async setWindowSystemBar(names: Array<'status' | 'navigation'>): Promise<void> {
    147.     try {
    148.       const win: window.Window = await window.getLastWindow(this.context);
    149.       await win.setWindowSystemBarEnable(names);
    150.     } catch (e) {
    151.       hilog.error(0x0000, 'testTag', `Failed to set window system bar. Code is ${e.code}, message is ${e.message}`);
    152.     }
    153.   }
    
    154.   private safeParseData(data: string): Record<string, Object> {
    155.     try {
    156.       if (typeof data === 'string') {
    157.         return JSON.parse(data);
    158.       }
    159.       return JSON.parse(JSON.stringify(data));
    160.     } catch (e) {
    161.       hilog.error(0x0000, 'testTag', `Failed to parse data. Code is ${e.code}, message is ${e.message}`);
    162.     }
    163.     return {};
    164.   }
    
    165.   // ...
    166. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-splash "开屏广告")
# 实时竞价

更新时间: 2025-12-16 16:37

## 场景介绍

实时竞价是指用户在访问媒体产生曝光机会时，众多家DSP（Demand Side Platform，需求方平台）根据曝光的上下文以及用户属性实时地评估曝光价值并给出报价，出价最高的DSP胜出，赢得此次曝光机会。

## 支持场景

- 原生广告
- 激励广告
- 插屏广告
- 开屏广告
- 贴片广告

## 接口说明

|接口名|描述|
|:--|:--|
|[loadAd](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadad)(adParam: AdRequestParams, adOptions: AdOptions, listener: AdLoadListener): void|请求单广告位广告，通过AdRequestParams、AdOptions进行广告请求参数设置，通过AdLoadListener监听广告请求回调。|
|[loadAdWithMultiSlots](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#loadadwithmultislots)(adParams: AdRequestParams[], adOptions: AdOptions, listener: MultiSlotsAdLoadListener): void|请求多广告位广告，通过AdRequestParams[]、AdOptions进行广告请求参数设置，通过MultiSlotsAdLoadListener监听广告请求回调。|

## 开发步骤

### 添加竞价参数

开发者需要在广告请求参数[AdRequestParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#adrequestparams)中添加实时竞价相关参数。

实时竞价关键参数如下所示：

|名称|类型|必填|说明|
|:--|:--|:--|:--|
|tMax|number|否|交易的最大超时时间（包含网络延迟），单位ms。|
|cur|string|否|竞价请求支持的币种，支持传多个，用英文逗号分隔。当前支持五种货币：<br><br>1. CNY。<br>2. USD。<br>3. EUR。<br>4. GBP。<br>5. JPY。<br><br>不填默认是CNY。|
|bidFloor|number|否|竞价广告位的底价。|
|bidFloorCur|string|否|竞价广告位底价使用的币种。如果bidFloor非空，则bidFloorCur也非空。当前只支持五种货币中的一种：<br><br>1. CNY。<br>2. USD。<br>3. EUR。<br>4. GBP。<br>5. JPY。<br><br>不填则默认是CNY。|
|bpkgName|string|否|广告位竞投的APP包名，支持传多个，用英文逗号分隔。|

示例代码如下所示：

1. import { advertising } from '@kit.AdsKit';

2. const adRequestParams: advertising.AdRequestParams = {
3.   // 'testu7m3hc4gvm'为测试专用的广告位ID，暂无竞价信息，App正式发布时需要改为正式的广告位ID
4.   adId: 'testu7m3hc4gvm',
5.   // 广告类型
6.   adType: 3,
7.   // 交易的最大超时时间
8.   tMax: 100,
9.   // 竞价请求支持的币种，多个用英文逗号分隔
10.   cur: 'CNY',
11.   // 竞价广告位的底价
12.   bidFloor: 6.66,
13.   // 竞价广告位底价使用的币种
14.   bidFloorCur: 'CNY',
15.   // 广告位竞投的APP包名，多个用英文逗号分隔
16.   bpkgName: 'com.huawei.baidu,com.huawei.music'
17. };

### 处理竞价结果

开发者需要在广告请求成功后的回调AdLoadListener.[onAdLoadSuccess](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#onadloadsuccess)或MultiSlotsAdLoadListener.[onAdLoadSuccess](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#onadloadsuccess)中，处理广告返回的实时竞价结果[Advertisement](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-advertising#advertisement).biddingInfo。

实时竞价结果信息如下所示：

说明

回传竞价结果，需要申请使用Internet网络权限[ohos.permission.INTERNET](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/permissions-for-all#ohospermissioninternet)。详细申请权限流程请参考[开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/development-preparation)。

|名称|类型|必填|说明|
|:--|:--|:--|:--|
|price|number|是|本条广告的eCPM（Effective Cost Per Mille，每一千次展示可以获得的广告收入）。|
|cur|string|是|本条广告的价格币种。支持币种：CNY、USD、EUR、GBP、JPY。|
|nurl|string|是|媒体回传竞价成功结果的URL。|
|lurl|string|是|媒体回传竞价失败结果的URL。|

- 若广告竞胜，开发者需要替换nurl中的宏，并回传竞胜结果。
    
    宏说明如下：
    
    |宏|说明|
    |:--|:--|
    |SECOND_PRICE|竞胜时，其他DSP最高出价。样例：3.6。|
    |AUCTION_CURRENCY|价格币种。支持币种：CNY、USD、EUR、GBP、JPY。|
    

- 若广告竞败，开发者需要替换lurl中的宏，并回传竞败结果。
    
    宏说明如下：
    
    |宏|说明|
    |:--|:--|
    |AUCTION_PRICE|竞败时，其他DSP最高出价。样例：3.6。|
    |AUCTION_LOSS|竞价结果，如果没有走到参竞环节也需要回调，并替换具体过滤结果码。<br><br>枚举：<br><br>102：竞价失败。<br><br>103：底价过滤。<br><br>104：包名过滤。<br><br>105：其他原因过滤。<br><br>4005：超时未返回。|
    |AUCTION_CURRENCY|价格币种。支持币种：CNY、USD、EUR、GBP、JPY。|
    |AUCTION_APP_PKG|竞败时，竞胜DSP推广的App包名。|
    |AUCTION_APP_NAME|竞败时，竞胜DSP推广的App名称。|
    |AUCTION_CP_ID|竞败时，竞胜DSP的编号：<br><br>1：广点通<br><br>2：穿山甲<br><br>3：百青藤<br><br>4：快手联盟<br><br>5：爱奇艺<br><br>6：阿里<br><br>7：VIVO<br><br>8：OPPO<br><br>9：小米<br><br>10：京东<br><br>11：拼多多<br><br>100：其他|
    

示例代码如下所示：

1. import { advertising } from '@kit.AdsKit';
2. import { hilog } from '@kit.PerformanceAnalysisKit';
3. import { rcp } from '@kit.RemoteCommunicationKit';

4. interface BiddingInfo {
5.   // 本条广告的eCPM（每一千次展示可以获得的广告收入）
6.   price: number;

7.   // 本条广告的价格币种
8.   cur: string;

9.   // 媒体回传竞价成功结果的URL
10.   nurl: string;

11.   // 媒体回传竞价失败结果的URL
12.   lurl: string;
13. }

14. const adLoaderListener: advertising.AdLoadListener = {
15.   // 广告请求失败回调
16.   onAdLoadFailure: (errorCode: number, errorMsg: string) => {
17.     hilog.error(0x0000, 'testTag', `Failed to load ad. Code is ${errorCode}, message is ${errorMsg}`);
18.   },
19.   // 广告请求成功回调
20.   onAdLoadSuccess: (ads: Array<advertising.Advertisement>) => {
21.     hilog.info(0x0000, 'testTag', 'Succeeded in loading ad');
22.     // 期望的底价
23.     const bidFloor: number = 6;
24.     const biddingSuccessAds: Array<advertising.Advertisement> = [];
25.     for (const ad of ads) {
26.       const biddingInfo: BiddingInfo = ad.biddingInfo as BiddingInfo;
27.       if (!biddingInfo) {
28.         continue;
29.       }
30.       if (biddingInfo.cur === 'CNY' && biddingInfo.price >= bidFloor) {
31.         hilog.info(0x0000, 'testTag', 'Petal Ads wins.');
32.         if (biddingInfo.nurl) {
33.           const url: string = biddingInfo.nurl
34.             // 竞胜时，其他DSP最高出价
35.             .replace('SECOND_PRICE', '3.6')
36.             // 价格币种
37.             .replace('AUCTION_CURRENCY', 'CNY');
38.           sendBiddingResult(url);
39.         }
40.         biddingSuccessAds.push(ad);
41.       } else {
42.         hilog.info(0x0000, 'testTag', 'Petal Ads loses.');
43.         if (biddingInfo.lurl) {
44.           const url: string = biddingInfo.lurl
45.             // 竞败时，其他DSP最高出价
46.             .replace('AUCTION_PRICE', '3.6')
47.             // 竞价结果
48.             .replace('AUCTION_LOSS', '102')
49.             // 价格币种
50.             .replace('AUCTION_CURRENCY', 'CNY')
51.             // 竞败时，竞胜DSP推广的App包名
52.             .replace('AUCTION_APP_PKG', 'com.huawei.music')
53.             // 竞败时，竞胜DSP推广的App名称
54.             .replace('AUCTION_APP_NAME', 'music')
55.             // 竞败时，竞胜DSP的编号
56.             .replace('AUCTION_CP_ID', '100')
57.           sendBiddingResult(url);
58.         }
59.       }
60.     }
61.     // ...此处省略展示广告的逻辑
62.   }
63. };

64. async function sendBiddingResult(url: string): Promise<void> {
65.   let session: rcp.Session | undefined = undefined;
66.   try {
67.     session = rcp.createSession();
68.     await session.get(url);
69.   } catch (e) {
70.     hilog.error(0x0000, 'testTag', `Failed to send bidding result. Code is ${e.code}, message is ${e.message}`);
71.   } finally {
72.     session?.close();
73.   }
74. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-roll "贴片广告")
# 鲸鸿动能媒体服务平台打开受限

更新时间: 2025-12-16 16:37

受制于您所在国家/地区的外汇管制、税务处理等因素，您所在的国家/地区尚未对个人开发者开放鲸鸿动能流量变现服务，您需要实名认证成为华为开发者联盟的企业开发者，包括获得应用开发者合法授权的企业，详细步骤请参见[受限说明](https://developer.huawei.com/consumer/cn/doc/monetize/restriction-0000001061730052)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-faq-4 "展示广告时显示白屏")
# 鲸鸿动能媒体服务平台打开受限

更新时间: 2025-12-16 16:37

受制于您所在国家/地区的外汇管制、税务处理等因素，您所在的国家/地区尚未对个人开发者开放鲸鸿动能流量变现服务，您需要实名认证成为华为开发者联盟的企业开发者，包括获得应用开发者合法授权的企业，详细步骤请参见[受限说明](https://developer.huawei.com/consumer/cn/doc/monetize/restriction-0000001061730052)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-publisher-service-faq-4 "展示广告时显示白屏")
