# Intents Kit简介

更新时间: 2025-12-16 16:27

Intents Kit（意图框架服务）是HarmonyOS级的意图标准体系 ，意图连接了应用/元服务内的业务功能。

意图框架能帮开发者将应用/元服务内的业务功能，智能分发到各系统入口，这个过程即智慧分发。其中系统入口包括：小艺对话、小艺搜索、小艺建议。

系统入口、意图框架、鸿蒙生态的关系如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162745.33068424796636060849987995712645:50001231000000:2800:E5ECCD7D8D0CEE6544C716CB87C5873EF299E4877844211C1C617583A90FDF15.png "点击放大")

## Intents Kit优势

利用HarmonyOS的大模型、多维设备感知等AI能力，准确且及时地获取到用户显性、潜在意图，从而实现个性化、多模态、精准的智慧分发。

## 智慧分发

为方便开发者接入，智慧分发提供了多种特性类别，当前已开放习惯推荐、事件推荐、技能调用-语音、本地搜索，后续会陆续开放其他特性类别。每种特性类型支持的典型系统入口、分发逻辑见下表：

|**特性类型**|**系统入口**|**分发逻辑**|
|:--|:--|:--|
|习惯推荐|小艺建议|应用或元服务向系统共享意图，系统学习意图规律，在合适的时机推荐服务。比如向系统共享用户浏览资讯意图的数据，经过习惯规律性学习后，小艺建议会在合适的时机给用户推荐合适的浏览资讯服务与内容。|
|事件推荐|小艺建议|应用或元服务向系统共享意图，系统提取意图内容中的事件，结合时间、位置等信息向用户推荐提醒服务。比如向系统共享用户购买的电影票订单数据，由系统提取订单数据中的关键特征如时间、位置等，小艺建议会在合适的时机给用户推荐观影提醒服务。|
|位置推荐|小艺建议|位置感知推荐能力基于华为意图框架与花瓣地图定位识别能力，通过小艺建议等智慧入口，适时、适需地将服务内容以卡片形式推荐给用户。位置感知基于GNSS、WLAN和基站等融合定位技术，设置圆形、多边形等地理围栏，提供室内外高精度定位能力。|
|技能调用-语音|小艺对话|系统基于AI大模型对理解用户显性或隐性的输入，帮用户完成应用或元服务的功能调用。比如用户在小艺对话中询问“从深圳去北京的飞机要多少钱”，可以理解用户搜索机票的意图，调用应用或元服务提供的搜索机票意图获取机票数据并向用户呈现。|
|本地搜索|小艺搜索|应用或元服务向系统共享意图，系统对意图的实体内容构建本地索引，满足用户搜索的需求。比如向系统共享“华为开发者大会”相关报道资讯后，用户在该入口输入相关关键词，即可将应用或元服务内的资讯内容检索出来。|

为了满足更细粒度的分发诉求，每类特性类别下提供多个具体特性，具体特性的分发系统入口、开发依赖见[各垂域的智慧分发特性列表](https://developer.huawei.com/consumer/cn/doc/service/intents-ai-distribution-characteristic-0000001901922213#section2656133582215)。具体特性开发依赖的意图相关字段见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。

## 意图的运行逻辑

HarmonyOS、应用/元服务的交互中，意图运行方式分为意图调用和意图共享：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162746.58323899005931138600038778242973:50001231000000:2800:97707CB300AEA9A8D6952B0C4948727BFDAA14CAA7563C6498A4731EDB616C8D.png "点击放大")

|“**意图”****运行方****式**|**发起者**|**定义**|
|:--|:--|:--|
|**意图共享**|应用/元服务|指应用/元服务主动向HarmonyOS共享意图，可用于HarmonyOS构建本地内容索引、学习用户的行为规律，以支持本地搜索和主动建议。<br><br>意图共享包含动作和实体两个部分，动作支持完成时和将来时两种机制。<br><br>- 完成时：用户意图已执行，共享的数据可用于本地搜索和系统建议。<br>- 将来时：意图是基于用户行为预测的，共享的数据可用于本地搜索。<br><br>意图框架还支持开发者向系统进行辅助实体共享，例如位置信息等，用于场景推荐和其他智慧分发功能的增强。|
|**意图调用**|HarmonyOS|指HarmonyOS主动调用应用/元服务的功能。<br><br>用户在系统入口输入信息或者系统主动推荐后，系统可向应用/元服务发起意图调用，例如播放音乐、查看旅游攻略、搜索视频等。|

## 约束与限制

- 设备限制

本Kit仅适用于Phone、Tablet、PC/2in1，暂不支持模拟器使用。

- 地区限制

本Kit仅支持中国境内（不包含中国香港、中国澳门、中国台湾）提供服务。

- 操作系统限制

HarmonyOS 5.0及以上。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-kit-guide "Intents Kit（意图框架服务）")
# Intents Kit接入流程

更新时间: 2025-12-16 16:27

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162746.51186337737191051377962111800903:50001231000000:2800:8C4E984A91E488197995EA2D58104A191AB70E66088CB2E5D7CC5F2E8F3CB7A9.png "点击放大")

|**阶段**|**任务**|**任务描述**|**示例**|**指导文档**|
|:--|:--|:--|:--|:--|
|**意向**|选择特性确定意图|开发者在已发布的特性列表中根据想达成的用户体验选择特性，根据特性来确定需实现的意图。|开发者想实现“歌曲续听推荐”的特性，则根据智慧分发特性描述，需要实现“播放歌曲”意图。|[歌曲续听推荐](https://developer.huawei.com/consumer/cn/doc/service/intents-ai-distribution-characteristic-0000001901922213)|
|**开发**|调试白名单申请|确定开发意向后，开发者发送邮件到邮箱（hagservice@huawei.com）或者联系华为意图框架接口同事，向华为提供测试应用的信息，用于申请调试白名单。|1. 应用名称：华为音乐。<br>2. 应用包名：com.xxxx。<br>3. 接入意图名称：“播放歌曲”。<br>4. 应用图标：jpg、png……。<br>5. APP ID：1234567。<br>6. Client ID：1234567。<br>7. 华为账号（UID）：1234567、7654321……。|见各特性类型<br><br>习惯推荐：[开发者测试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-habit-rec-dp-self-validation)<br><br>事件推荐：[开发者测试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-event-rec-dp-self-validation)<br><br>技能调用：[开发者测试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-dp-self-validation)|
|意图声明文件中注册意图|在DevEco Studio中开发时，注册对应的意图。|注册“播放歌曲”意图。|[意图注册](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-habit-rec-access-programme#section12621163216260)|
|开发实现意图调用/意图共享|开发应用/元服务的意图共享接口，使其可以通过HarmonyOS接口完成意图数据共享。|开发“播放歌曲”意图中的意图共享接口。|[端侧意图共享](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-habit-rec-access-programme#section14210125472916)|
|开发应用/元服务的意图调用接口，使其可以通过HarmonyOS接口被正确调用。|开发“播放歌曲”意图中的意图调用接口。|[端侧意图调用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-habit-rec-access-programme#section9408948143016)|
|**验证**|端到端验证特性|使用华为侧提供的测试能力完成目标特性的端到端联调测试，联调测试完成后，提交智慧分发配置至审核。|在设备上对应入口进行“华为音乐-歌曲续听推荐”的特性端到端测试，测试完成后点击提交智慧分发配置。|/|
|**上架**|应用市场上架软件包（应用/元服务）|开发完成并打包好软件包后，在应用市场上传软件包。|打包“华为音乐”软件包并通过应用市场上架。|[应用市场上架流程](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-0000002235870050)|
|意图框架注册|在小艺开放平台进行意图注册配置并提交审核。由华为工程师审核，一般情况在3个工作日内完成。|注册“播放歌曲”意图。|[意图标准协议上架指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-kit-listing-standard-protocol)|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-introduction "Intents Kit简介")
# 概述

更新时间: 2025-12-16 16:27

习惯推荐是HarmonyOS学习用户的行为习惯后做出的主动预测推荐。

1. 开发者将用户在应用/元服务内的使用行为向HarmonyOS共享，使得HarmonyOS可以基于共享的数据学习用户的行为习惯。
2. 在HarmonyOS学习到用户的行为习惯后，会给用户推荐相应功能，并且尝试补充详细功能参数，减少用户执行任务的步骤。

以听音乐为例，意图框架设计了统一的意图——播放歌单意图，该意图可以让应用/元服务与HarmonyOS交互。

当用户使用应用/元服务播放歌单时，应用/元服务可以向Intents Kit共享该意图，并提供一些用于学习的特征，例如播放开始/结束时间、播放时长、歌单名等。HarmonyOS会结合底层采集的时间、空间、设备状态等数据共同理解用户行为上下文。最后HarmonyOS结合应用/元服务历史上共享过的数据重建响应意图任务并进行预测推荐，例如在用户每天早上上车后，为其推荐“每日推荐”歌单卡片，用户点击实现一键播放。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-habit-rec "习惯推荐方案")
# 场景体验

更新时间: 2025-12-16 16:27

## 典型场景

当前习惯推荐可在小艺建议入口分发，在不同垂域中，填充功能详细参数或内容的逻辑不同，主要典型场景可分为常用接续、常用复访、常用推新三类。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162754.01202740011193182373052125675305:50001231000000:2800:127E1383C977F95EE202A1CFD840DE51CE93047AAD65AEA97A1086819DAA7735.png "点击放大")

以常看视频续播为例，系统预测当前用户使用华为视频的播放视频功能概率较高，会选择用户最近观看且还没看完的视频内容来补充功能细节，在小艺建议中以模板卡形式推荐展示，用户点击卡片后，实现一步跳转进应用的视频播放页。

## 卡片展示效果

意图框架提供各垂域习惯推荐在小艺建议中展示使用的标准模板卡片，开发者无需开发展示卡片。在展示模板上，会展示应用/元服务名称与logo和内容必要信息，比如音乐名、音乐图片，这类参数需要开发者共享到系统。

以下为播放歌曲-习惯推荐的卡片示例。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162754.44675755519712674664522740103338:50001231000000:2800:3FB261627F6740FDC4D5C4B4F95AB96ED699B93BE30867CC8CD7453D11B25CCC.png "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-habit-rec-introduction "概述")
# 接入方案

更新时间: 2025-12-16 16:27

## 方案概述

当用户在应用/元服务内使用功能时，开发者需要按照标准意图Schema向系统共享行为数据，并支持意图调用（空调用与传参调用），以实现用户点击模板卡后跳转回对应页面。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162757.61254603244746364462212556272396:50001231000000:2800:90E8EC657EC6FA333A11D801041420AB5C1F65895CD3D17ECA5E657DA066E5BB.png "点击放大")

## 意图注册

以歌曲续听推荐特性为例，首先要注册播放歌曲意图（PlayMusic），其他意图见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。

开发者需要编辑对应的意图配置insight_intent.json文件实现意图声明。insight_intent.json文件需要放置在任意一个module下面的指定目录：src/main/resources/base/profile/insight_intent.json，并且整个工程中只能存在一个insight_intent.json文件。

1. {
2.   // 应用支持的意图列表
3.   // 必须声明应用支持插件包含的必选意图，应用上架时会进行校验
4.   "insightIntents": [
5.     {
6.       // 意图名称
7.       // 名称应当遵循意图框架规范，当前仅支持预置垂域意图，不允许自定义
8.       // 应用内意图名称唯一，不允许出现相同的名称定义
9.       "intentName": "PlayMusic",
10.       // 意图所属的垂域
11.       "domain": "MusicDomain",
12.       // 意图版本号
13.       // 插件引用意图时会校验该版本号，只有和插件定义的版本号一致才能正常调用
14.       "intentVersion": "1.0.1",
15.       // 意图调用逻辑入口
16.       // 根据意图调用文件实际路径和实际名称进行填写，此处文件仅做示意
17.       "srcEntry": "./ets/entryability/InsightIntentExecutorImpl.ets",
18.       "uiAbility": {
19.         // 意图所在ability
20.         "ability": "EntryAbility",
21.         // UIAbility支持前后台两种执行模式
22.         "executeMode": [
23.           "background",
24.           "foreground"
25.         ]
26.       }
27.     }
28.   ]
29. }

## 端侧意图共享

构建意图对象，并且调用[shareIntent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/intents-arkts-api-insightintent#section161911659112211)，实现意图共享。可同时构建多个PlayMusic或PlayMusicList的意图对象。

1. import { insightIntent } from '@kit.IntentsKit';
2. import { BusinessError } from '@kit.BasicServicesKit';

3. let playMusicIntent1: insightIntent.InsightIntent;
4. let playMusicIntent2: insightIntent.InsightIntent;
5. // 共享数据接口  意图数组可以是更多的实体
6. // 根据实际代码上下文自行传入合适的context
7. insightIntent.shareIntent(context, [playMusicIntent1, playMusicIntent2]).then(() => {
8.   console.info('shareIntent succeed');
9. }).catch((err: BusinessError) => {
10.   console.error(`error.code: ${err?.code}, failed because ${err?.message}`);
11. });

PlayMusic的意图共享字段定义见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)定义，代码示例如下：

1. import { insightIntent } from '@kit.IntentsKit';

2. let playMusicIntent: insightIntent.InsightIntent = {
3.   intentName: "PlayMusic",
4.   intentVersion: "1.0",
5.   identifier: "52dac3b0-6520-4974-81e5-25f0879449b5",
6.   intentActionInfo: {
7.     actionMode: "EXECUTED",
8.     executedTimeSlots: {
9.       executedStartTime: 1637393112000,
10.       executedEndTime: 1637393212000,
11.     },
12.     currentPercentage: 50,
13.   },
14.   intentEntityInfo: {
15.     entityName: "Music",
16.     entityId: "C10194368",
17.     entityGroupId: "C10194321312",
18.     displayName: "测试歌曲1",
19.     description: "NA",
20.     logoURL: "https://www-file.abc.com/-/media/corporate/images/home/logo/abc_logo.png",
21.     keywords: ["华为音乐", "化妆"],
22.     rankingHint: 99,
23.     expirationTime: 1637393212000,
24.     metadataModificationTime: 1637393212000,
25.     activityType: ["1", "2", "3"],
26.     artist: ["测试歌手1", "测试歌手2"],
27.     lyricist: ["测试词作者1", "测试词作者2"],
28.     composer: ["测试曲作者1", "测试曲作者2"],
29.     albumName: "测试专辑",
30.     duration: 244000,
31.     playCount: 100000,
32.     musicalGenre: ["流行", "华语", "金曲", "00后"],
33.     isPublicData: false,
34.   }
35. }

完整的意图共享示例如下所示，该示例构建了一个PlayMusic意图，并进行了shareIntent调用。

1. import { insightIntent } from '@kit.IntentsKit';
2. import { BusinessError } from '@kit.BasicServicesKit';

3. let playMusicIntent: insightIntent.InsightIntent = {
4.   intentName: "PlayMusic",
5.   intentVersion: "1.0",
6.   identifier: "52dac3b0-6520-4974-81e5-25f0879449b5",
7.   intentActionInfo: {
8.     actionMode: "EXECUTED",
9.     executedTimeSlots: {
10.       executedStartTime: 1637393112000,
11.       executedEndTime: 1637393212000,
12.     },
13.     currentPercentage: 50,
14.   },
15.   intentEntityInfo: {
16.     entityName: "Music",
17.     entityId: "C10194368",
18.     entityGroupId: "C10194321312",
19.     displayName: "测试歌曲1",
20.     description: "NA",
21.     logoURL: "https://www-file.abc.com/-/media/corporate/images/home/logo/abc_logo.png",
22.     keywords: ["华为音乐", "化妆"],
23.     rankingHint: 99,
24.     expirationTime: 1637393212000,
25.     metadataModificationTime: 1637393212000,
26.     activityType: ["1", "2", "3"],
27.     artist: ["测试歌手1", "测试歌手2"],
28.     lyricist: ["测试词作者1", "测试词作者2"],
29.     composer: ["测试曲作者1", "测试曲作者2"],
30.     albumName: "测试专辑",
31.     duration: 244000,
32.     playCount: 100000,
33.     musicalGenre: ["流行", "华语", "金曲", "00后"],
34.     isPublicData: false,
35.   }
36. }
37. // 共享数据接口  意图数组可以是更多的实体
38. // 根据实际代码上下文自行传入合适的context
39. insightIntent.shareIntent(context, [playMusicIntent]).then(() => {
40.   console.info('shareIntent succeed');
41. }).catch((err: BusinessError) => {
42.   console.error(`error.code: ${err?.code}, failed because ${err?.message}`);
43. });

## 端侧意图调用

### 意图执行组件为uiAbility的意图调用

如上文意图注册，当开发者注册的意图承载的运行组件为uiAbility时，开发者需要自己实现InsightIntentExecutor，并在对应回调实现打开落地页（点击推荐卡片跳转的界面）的能力，PlayMusic的意图调用字段定义见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。

步骤如下：

1. 继承InsightIntentExecutor。
2. 重写对应方法，例如目标拉起前台页面，则可重写onExecuteInUIAbilityForegroundMode方法。
3. 通过意图名称，识别播放歌曲意图（PlayMusic），在对应的方法中传递意图参数（param），并拉起对应落地页（如歌曲落地页）。
    
    1. import { insightIntent, InsightIntentExecutor } from '@kit.AbilityKit';
    2. import { window } from '@kit.ArkUI';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. /**
    5.  * 意图调用样例
    6.  */
    7. export default class InsightIntentExecutorImpl extends InsightIntentExecutor {
    8.   private static readonly PLAY_MUSIC = 'PlayMusic';
    9.   /**
    10.    * override 执行前台UIAbility意图
    11.    *
    12.    * @param name 意图名称
    13.    * @param param 意图参数
    14.    * @param pageLoader 窗口
    15.    * @returns 意图调用结果
    16.    */
    17.   onExecuteInUIAbilityForegroundMode(name: string, param: Record<string, Object>, pageLoader: window.WindowStage):
    18.     Promise<insightIntent.ExecuteResult> {
    19.     // 根据意图名称分发处理逻辑。接入方可根据实际业务实现页面跳转
    20.     switch (name) {
    21.       case InsightIntentExecutorImpl.PLAY_MUSIC:
    22.         return this.playMusic(param, pageLoader);
    23.       default:
    24.         break;
    25.     }
    26.     return Promise.resolve({
    27.       code: -1,
    28.       result: {
    29.         message: 'unknown intent'
    30.       }
    31.     } as insightIntent.ExecuteResult)
    32.   }
    33.   /**
    34.    * 实现调用播放歌曲功能
    35.    *
    36.    * @param param 意图参数
    37.    * @param pageLoader 窗口
    38.    */
    39.   private playMusic(param: Record<string, Object>, pageLoader: window.WindowStage): Promise<insightIntent.ExecuteResult> {
    40.     return new Promise((resolve, reject) => {
    41.       let para: Record<string, string> = {
    42.         'result': JSON.stringify(param)
    43.       };
    44.       let localStorage: LocalStorage = new LocalStorage(para);
    45.       // TODO 实现意图调用，loadContent的入参为歌曲落地页路径，例如：pages/Index
    46.       pageLoader.loadContent('pages/Index', localStorage)
    47.         .then(() => {
    48.           let entityId: string = (param.items as Array<object>)?.[0]?.['entityId'];
    49.           // TODO 调用成功的情况，此处可以打印日志
    50.           resolve({
    51.             code: 0,
    52.             result: {
    53.               message: 'Intent execute succeed'
    54.             }
    55.           });
    56.         })
    57.         .catch((err: BusinessError) => {
    58.           // TODO 调用失败的情况
    59.           resolve({
    60.             code: -1,
    61.             result: {
    62.               message: 'Intent execute failed'
    63.             }
    64.           })
    65.         });
    66.     })
    67.   }
    68. }
    

### 意图执行组件为form的意图调用

如上文意图注册，当开发者注册的意图承载的运行组件为form（运行组件FormExtensionAbility）时，则需要开发者在实现的FormExtensionAbility中从want中获取并解析意图名和执行参数，用于卡片展示。

步骤如下：

1. 在意图执行绑定FormExtensionAbility的onAddForm(want: Want)中获取运行态意图框架传入的意图名（预定义keyName为ohos.insightIntent.executeParam.name）和意图执行参数（预定义keyName为ohos.insightIntent.executeParam.param）；
2. 通过意图名称，识别播放歌曲意图(PlayMusic)，在对应的方法中传递意图参数（param），并加载对应数据用于卡片展示。

3. **import** { Want } **from** '@kit.AbilityKit';
4. **import** { formBindingData, FormExtensionAbility } **from** '@kit.FormKit';

5. _/**_
6.  _* 卡片意图调用示例_
7.  _*/_
8. **export default class** LoadCardFormAbility **extends** FormExtensionAbility {
9.   onAddForm(want: Want): formBindingData.FormBindingData {
10.     **if** (want?.parameters?.['ohos.insightIntent.executeParam.name'] != **undefined**) {
11.       **const** intentName = want.parameters['ohos.insightIntent.executeParam.name']; _//意图名_
12.       _//__TODO: 根据意图名称分发处理逻辑，若仅一个卡片意图，则可以忽略_
13.     }

14.     **if** (want?.parameters?.['ohos.insightIntent.executeParam.param'] != **undefined**) {
15.       **const** executeParameter = want.parameters['ohos.insightIntent.executeParam.param']; _//意图执行参数_
16.       _//__TODO: 从 executeParameter 中解析具体意图执行参数，用于卡片内容展示_
17.     }

18.     **let** formData = ''; _//__TODO: 仅示例，根据具体逻辑封装_
19.     **return** formBindingData.createFormBindingData(formData);
20.   }
21. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-habit-rec-scene-experience "场景体验")
# 开发者测试

更新时间: 2025-12-16 16:28

Intents Kit向开发者提供真机测试能力，即开发者可连接设备进行调测。开发者完成代码开发之后，功能正式上架应用市场前，可以在HarmonyOS 5及以上的设备上面进行自验证，打磨体验。真机测试分为三个步骤：基础信息提供，环境准备，联调验证。

## 基础信息提供

达成开发意向后，开发者发送邮件到邮箱（hagservice@huawei.com）或者联系华为意图框架接口同事，向华为提供测试应用的信息。

|**序号**|**基础****信息**|**描述**|
|:--|:--|:--|
|1|应用名称|应用市场上架的应用名称。|
|2|应用包名|应用市场上架的应用包名。|
|3|接入意图名称|开发者意向接入的意图名称（中英文）。|
|4|应用图标|应用的图标，具体要求如下：<br><br>图标背景：非透明。<br><br>比例&尺寸：1:1，72px*72px。<br><br>大小：不超过1M。<br><br>格式：png、jpg、jpeg。|
|5|APP ID|登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html#/)，在“开发与服务 > 我的项目 > 项目设置 > 常规 > 应用-APP ID”中获取。|
|6|Client ID|登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html#/)，在“开发与服务 > 我的项目 > 项目设置 > 常规 > 应用 > OAuth 2.0客户端ID(凭据) > Client ID”中获取。|
|7|华为账号（UID）|参考[附录A获取UID](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-appendix-a-get-uid)。|

## 环境准备

准备一台装有HarmonyOS 5及以上版本的手机设备，系统版本最低要求为 Developer Beta 3，并按照以下顺序依次执行，不能更换执行顺序。

1. 保持设备联网，并且设备时间和实际北京时间保持一致。
2. 点击桌面的小艺建议卡片。此时卡片显示的是“欢迎使用小艺建议”，点击卡片打开小艺的隐私页面，并选择“同意”。如果此前已经同意过小艺的隐私协议，此步骤可以跳过。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162757.78760696526409579713067970675008:50001231000000:2800:BCE5244D273801D22C0F823ED0F9C2F8B9AB48E2A302B6A6556B3034BC383D61.png "点击放大")
    
3. 打开开发者调试模式：进入设置 > 机型 > 关于手机，连续点击软件版本7次，弹出开启“开发者模式”，点击“确认开启”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162757.71519605539962538562871981819873:50001231000000:2800:23ADE894F45E34E97B5779110B6C415EC9B5AF8ADB9DE5D922084223716CE826.png "点击放大")
    
4. 长按电源键唤醒小艺，将半屏态小艺向上拉升至全屏态，点击左上角返回上层，返回后点击右上角的头像，进入“设置”，找到并进入应用网络设置，打开“WLAN下自动更新”开关。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162758.51514150521436415661805445635057:50001231000000:2800:A219A2B530785FBC0E35ECF3FFBFA9EA28BACB7E376020F2ECFA7B425C1B837D.png "点击放大")
    
5. 在上一步页面中下滑，点击“个性化推荐”，进入后打开“个性化推荐”的开关。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162800.39762527529047354787519073540137:50001231000000:2800:0B9C237A8BE67FDD41BFB7BC8971E22230BF1F9523B930B60FE64194F5FB84F3.png "点击放大")
    
6. 进入设置 > 系统 > 开发者选项 > 意图框架调试，打开意图框架调试开关，如果下方显示已切换至真机模式并且测试应用包名在“本设备支持测试应用”下，则代表真机模式切换成功。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162800.79237426428501037242068694414689:50001231000000:2800:BAF73FD203E3676A1DCA533131E5FC291B437173C8B586A99D2B9013DABFE58E.png "点击放大")
    
    【提示】如果出现意图框架调试打开后，设备长时间无法出现“已切换至真机模式”或者出现“已切换至真机模式”但没有包名的时候，可以尝试以下操作：
    
    1. 登出华为账号，再登录之后重新开启意图框架调试开关。
    2. 在小艺对话中点击右上角头像，设置 > 服务管理 > 注销服务 > 注销服务，然后返回桌面重新点击小艺建议的卡片，将展示“欢迎使用小艺建议”的卡片刷新成有服务推荐的卡片，最后重新开启意图框架调试开关。
7. 完成以上所有步骤，即可进行联调。

## 联调验证

1. 意图共享：在测试应用当中成功触发意图共享。即通过测试应用内的操作触发[shareIntent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/intents-arkts-api-insightintent#section144826162913)接口的调用，并且意图共享成功。
    
    【举例】某音乐APP接入意图框架音乐续播的特性。通过播放某一首歌曲的用户操作，触发某音乐APP调用系统接口[shareIntent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/intents-arkts-api-insightintent#section144826162913)。某音乐APP的开发者通过日志确认[shareIntent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/intents-arkts-api-insightintent#section144826162913)接口调用成功，则可以认为某音乐APP本次意图共享是成功的。
    
2. 卡片渲染：点击桌面上的小艺建议卡片中任意服务，然后返回桌面，会触发小艺建议卡片强制刷新。刷新之后会展示前一步意图共享的数据所形成的模板卡片。具体卡片样式可参考具体特性的场景说明文档。
    
    【提示】重复意图共享和卡片渲染两步，可以触发卡片上文字元素和图片元素的刷新。
    
3. 意图调用：点击小艺建议卡片中的模板卡片，能够跳转至测试应用的目标页面，则说明意图调用的过程是正确的。
    1. 【提示】意图调用的验证过程中，应当对测试应用的冷启动和热启动场景都进行验证，两个场景最终的跳转页面应当与预期的页面保持一致。
    2. 如果卡片没有正常渲染。可以尝试通过下列方法出卡：
        1. 检查个性化推荐开关是否开启，详见[环境准备章节步骤5](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-habit-rec-dp-self-validation#li11955153025619)；检查意图框架测试开关是否开启，详见[环境准备章节步骤6](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-habit-rec-dp-self-validation#li1467622075715)；检查完后重新执行卡片渲染步骤。
        2. 重新触发意图共享，并且在接口结果返回success之后，重新连接充电线，手机灭屏等待8分钟，再重新执行卡片渲染步骤。

## 端云结合的习惯推荐

涉及习惯推荐叠加上云搜索场景的开发者优先完成习惯推荐在设备上联调，确保测试应用的意图共享和意图调用的业务逻辑正确。后端接口开发完毕，需自行检查接口的出参是否满足意图框架云侧接口规范。以上两步完成之后，可联系华为意图框架接口同事提交后端接口文档，华为同事会配合开发者进行联调。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-habit-rec-access-programme "接入方案")
# 场景体验

更新时间: 2025-12-16 16:27

## 典型场景

**事件****推荐典型场景****包括：**

- 关注提醒事件（购物车降价、加追更新）
- 订单履行提醒事件（门票、机票、打车、外卖、挂号）
- 核销转化事件（会员、优惠券、话费余额）

各垂域也可根据垂域的实际情况定义具体的事件。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162754.22857522940522979061347814361987:50001231000000:2800:EBC1089AE8F2E893B1E7C557A6E7EC5A334C46F3035BC2547DCF5DB604B0A7C3.png "点击放大")

以电影开场提醒为例，用户在应用/元服务中购买了电影票，在电影开场前半小时（具体生效时间将根据具体垂域的情况和用户最佳体验确定），用户可在小艺建议入口看到电影取票提醒的卡片，点击卡片可跳转到应用/元服务的订单详情页，用户可在该页面完成电影取票。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162754.29646220600418792664109798624192:50001231000000:2800:65AD8379B4B430F86881E1D92F97167D7690EE7EE93353ACAB24021E42D01A80.png "点击放大")

## 卡片展示效果

意图框架将提供系统标准的事件模板卡片，无需开发者开发，开发者只需按照具体垂域事件的[意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)将事件推送至智慧分发平台服务器即可。各垂域事件卡片样式的示例如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162754.86687259920734068918164528120930:50001231000000:2800:90AB96015AEDC25836F63316A3B9B9FACFFC0D59B76E668049921CAAA21788E0.png "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-event-rec-introduction "概述")
# 接入方案

更新时间: 2025-12-16 16:27

## 方案概述

当开发者有事件想要通知到用户时，可通过应用/元服务的云侧服务器向智慧分发平台推送事件内容（意图共享）。系统通过智慧决策判断事件发生的条件，在满足条件时，向用户推荐事件提醒卡片，当用户点击卡片后，可跳转到应用/元服务的详情页查看事件详情（意图调用）。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162757.82787700484749801783346405074181:50001231000000:2800:F38B1392D55B774420ED8180C72B4FF959F84D93131BD96D991263C97D491784.png "点击放大")

## 流程图

1. 开发者获取云侧事件捐赠所需的SID（Service OpenID）。

2. 当用户有订单事件后，开发者云将事件内容和SID同步到业务云。
3. 华为内部会根据事件和具体场景制定事件服务推出规则和时机。
4. 在满足制定规则场景下展示对应用户事件，增加服务曝光率。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162757.65095663515521964833501326803320:50001231000000:2800:ABAE20ECFC6DA97D29FAE011EAB4DF85DAC129DFEED211062710EC160C42673B.png "点击放大")

## 意图注册

以还款待办事件提醒特性为例，首先要注册查看还款意图（ViewRepayment），详见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。

开发者需要编辑对应的意图配置insight_intent.json文件实现意图声明。insight_intent.json文件需要放置在任意一个module下面的指定目录：src/main/resources/base/profile/insight_intent.json，并且整个工程中只能存在一个insight_intent.json文件。

1. {
2.   // 应用支持的意图列表
3.   // 必须声明应用支持插件包含的必选意图，应用上架时会进行校验
4.   "insightIntents": [
5.     {
6.       // 意图名称
7.       // 名称应当遵循意图框架规范，当前仅支持预置垂域意图，不允许自定义
8.       // 应用内意图名称唯一，不允许出现相同的名称定义
9.       "intentName": "ViewRepayment",
10.       // 意图所属的垂域
11.       "domain": "BankingDomain",
12.       // 意图版本号
13.       // 插件引用意图时会校验该版本号，只有和插件定义的版本号一致才能正常调用
14.       "intentVersion": "1.0.1",
15.       // 意图调用逻辑入口
16.       "srcEntry": "./ets/entryability/InsightIntentExecutorImpl.ets",
17.       "uiAbility": {
18.         // 意图所在ability
19.         "ability": "EntryAbility",
20.         // UIAbility支持前后台两种执行模式
21.         "executeMode": [
22.           "background",
23.           "foreground"
24.         ]
25.       }
26.     }
27.   ]
28. }

## 获取SID

说明

API文档参见：[意图框架API参考 > getSid](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/intents-arkts-api-insightintent#section76701233209)。

云侧事件捐赠凭证SID（Service OpenID）优先从缓存获取，当缓存获取失败可以强制从云侧获取新的SID。

1. import { insightIntent } from '@kit.IntentsKit';
2. import { BusinessError } from '@kit.BasicServicesKit';

3. // 根据实际代码上下文自行传入合适的context
4. insightIntent.getSid(context, false) // 优先获取缓存SID，改为true则强制从云侧获取新SID
5.   .then((sid: string) => {
6.     // 获取SID成功
7.     console.info('getSid succeed!');
8.   }).catch((error: BusinessError) => {
9.   // 获取SID失败
10.   console.error(`getSid failed! error=${error.code} reason=${error.message}`);
11. });

## 云侧意图共享

### 意图共享接口调用

应用/元服务通过[云侧意图共享接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/intents-rest-api-intent-share#section105321034437)，把对应意图的相关事件数据共享给Intents Kit，用于事件提醒服务。

### 事件撤销接口调用

当应用/元服务共享的意图相关事件数据超过时效期，Intents Kit需要通过[云侧事件撤销接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/intents-rest-api-revoke-event)把相关事件数据撤销，以避免触发超过时效期的事件提醒。

## 端侧意图调用

开发者需要自己实现InsightIntentExecutor，并在对应回调实现打开落地页（点击推荐卡片跳转的界面）的能力，ViewRepayment的意图调用字段定义见对应[垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)定义表。

步骤如下：

1. 继承InsightIntentExecutor。
2. 重写对应方法，例如目标拉起前台页面，则可重写onExecuteInUIAbilityForegroundMode方法。
3. 通过意图名称，识别查看还款意图（ViewRepayment）。
4. 在对应的方法中传递意图参数（param），并拉起对应落地页（如还款页面）。
    
    1. import { insightIntent, InsightIntentExecutor } from '@kit.AbilityKit';
    2. import { window } from '@kit.ArkUI';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. /**
    5.  * 意图调用样例 */
    6. export default class InsightIntentExecutorImpl extends InsightIntentExecutor {
    7.   private static readonly VIEW_REPAYMENT = 'ViewRepayment';
    8.   /**
    9.    * override 执行前台UIAbility意图
    10.    *
    11.    * @param name 意图名称
    12.    * @param param 意图参数
    13.    * @param pageLoader 窗口
    14.    * @returns 意图调用结果
    15.    */
    16.   onExecuteInUIAbilityForegroundMode(name: string, param: Record<string, Object>, pageLoader: window.WindowStage):
    17.     Promise<insightIntent.ExecuteResult> {
    18.     // 根据意图名称分发处理逻辑。接入方可根据实际业务实现页面跳转
    19.     switch (name) {
    20.       case InsightIntentExecutorImpl.VIEW_REPAYMENT:
    21.         return this.viewRepayment(param, pageLoader);
    22.       default:
    23.         break;
    24.     }
    25.     return Promise.resolve({
    26.       code: -1,
    27.       result: {
    28.         message: 'unknown intent'
    29.       }
    30.     } as insightIntent.ExecuteResult)
    31.   }
    
    32.   /**
    33.    * 实现调用查看还款功能
    34.    *
    35.    * @param param 意图参数
    36.    * @param pageLoader 窗口
    37.    */
    38.   private viewRepayment(param: Record<string, Object>, pageLoader: window.WindowStage): Promise<insightIntent.ExecuteResult> {
    39.     return new Promise((resolve, reject) => {
    40.       let para: Record<string, string> = {
    41.         'result': JSON.stringify(param)
    42.       };
    43.       let localStorage: LocalStorage = new LocalStorage(para);
    44.       // TODO 实现意图调用，loadContent的入参为查看还款落地页路径，例如：'pages/Index'
    45.       pageLoader.loadContent('pages/Index', localStorage)
    46.         .then(() => {
    47.           let entityId: string = (param.items as Array<object>)?.[0]?.['entityId'];
    48.           // TODO 调用成功的情况，此处可以打印日志
    49.           resolve({
    50.             code: 0,
    51.             result: {
    52.               message: 'Intent execute succeed'
    53.             }
    54.           });
    55.         })
    56.         .catch((err: BusinessError) => {
    57.           // TODO 调用失败的情况
    58.           resolve({
    59.             code: -1,
    60.             result: {
    61.               message: 'Intent execute failed'
    62.             }
    63.           })
    64.         });
    65.     })
    66.   }
    67. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-event-rec-scene-experience "场景体验")
# 开发者测试

更新时间: 2025-12-16 16:28

Intents Kit向开发者提供真机测试能力，即开发者可连接设备进行调测。开发者完成代码开发之后，功能正式上架应用市场前，可以在HarmonyOS NEXT设备上面进行自验证，打磨体验。真机测试分为三个步骤：基础信息提供，环境准备，联调验证。

## 基础信息提供

达成开发意向后，开发者发送邮件到邮箱（hagservice@huawei.com）或者联系华为意图框架接口同事，向华为提供测试应用的信息。

|**序号**|**基础****信息**|**描述**|
|:--|:--|:--|
|1|应用名称|应用市场上架的应用名称。|
|2|应用包名|应用市场上架的应用包名。|
|3|接入意图名称|开发者意向接入的意图名称（中英文）。|
|4|应用图标|应用的图标，具体要求如下：<br><br>图标背景：非透明。<br><br>比例&尺寸：1:1，72px*72px。<br><br>大小：不超过1M。<br><br>格式：png、jpg、jpeg。|
|5|APP ID|登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html#/)，在“开发与服务 > 我的项目 > 项目设置 > 常规 > 应用-APP ID”中获取。|
|6|Client ID|登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html#/)，在“开发与服务 > 我的项目 > 项目设置 > 常规 > 应用 > OAuth 2.0客户端ID(凭据) > Client ID”中获取。|
|7|华为账号（UID）|参考[附录A获取UID](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-appendix-a-get-uid)。|

## 环境准备

准备一台装有HarmonyOS Next版本的手机设备，系统版本最低要求为 Developer Beta 3，并按照以下顺序依次执行，不能更换执行顺序。

1. 保持设备联网，并且设备时间和实际北京时间保持一致。
2. 点击桌面的小艺建议卡片。此时卡片显示的是“欢迎使用小艺建议”，点击卡片打开小艺的隐私页面，并选择“同意”。如果此前已经同意过小艺的隐私协议，此步骤可以跳过。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162800.29409559441325233164277501874674:50001231000000:2800:1A926CC0B29A9CCAC9FC84C6D20FC8C25D42A13F5A5963809B33569AA93762EE.png "点击放大")
    
3. 打开开发者调试模式：进入设置 > 机型 > 关于手机，连续点击软件版本7次，弹出开启“开发者模式”，点击“确认开启”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162800.74478604399659633388918669242537:50001231000000:2800:232FEF7B6D5869E7BAB18226DEE13EFEBF360B16BEA188E74652B2CCC2C201CA.png "点击放大")
    
4. 长按电源键唤醒小艺，将半屏态小艺向上拉升至全屏态，点击左上角返回上层，返回后点击右上角的头像，进入“设置”，找到并进入应用网络设置，打开“WLAN下自动更新”开关。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162800.82471725719104278800439297815577:50001231000000:2800:1986F12D337352F21861874E2EFF9246FF3ED49CCC73268EC0D6C61F0817199F.png "点击放大")
    
5. 在上一步页面中下滑，点击“个性化推荐”，进入后打开“个性化推荐”的开关。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162802.28362332938851044075000162958255:50001231000000:2800:0C313152EBFE6DE9CEEC17AC7325FC5CD507ECA8B4F7F7AF10AC29688287D267.png "点击放大")
    
6. 进入设置 > 系统 > 开发者选项 > 意图框架调试，打开意图框架调试开关，如果下方显示已切换至真机模式并且测试应用包名在“本设备支持测试应用”下，则代表真机模式切换成功。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162802.96565669263305875690926742508910:50001231000000:2800:C42947210DBA5A84C32C77A5CAF98ACE3FC0E3A12D00C2C71402ECF4F474DA64.png "点击放大")
    
    【提示】如果出现意图框架调试打开后，设备长时间无法出现“已切换至真机模式”或者出现“已切换至真机模式”但没有包名的时候，可以尝试以下操作：
    
    1. 登出华为账号，再登录之后重新开启意图框架调试开关。
    2. 在小艺对话中点击右上角头像，设置 > 服务管理 > 注销服务 > 注销服务，然后返回桌面重新点击小艺建议的卡片，将展示“欢迎使用小艺建议”的卡片刷新成有服务推荐的卡片，最后重新开启意图框架调试开关。
7. 完成以上所有步骤，即可进行联调。

## 联调验证

1. 事件共享：开发者登录应用即可[获取云侧事件捐赠的SID](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-event-rec-access-programme#section2151759161514)，然后触发事件推送，将事件内容同步到华为云，具体操作可参考[开发者指南-事件推荐方案章节](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-event-rec-access-programme)。
    
    【举例】某出行类APP接入意图框架航班提醒的特性。用户通过APP购买了机票，触发开发者云调用华为事件通知接口（https://insightintent-simenv.cloud.huawei.com/open-ability/v2/service-events/notify），将用户航班事件推送至华为云，接口响应成功。
    
2. 卡片渲染：点击桌面上的小艺建议卡片中任意服务，然后返回桌面，会触发小艺建议卡片强制上云刷新。出卡条件是以事件的生效时间进行偏移，具体出卡条件和卡片的样式可以参考具体特性的场景说明文档（确定开发意向后由华为侧提供）。
    
    【举例】航班提醒是提前24小时提醒用户，如果用户航班起飞时间是8月15日20:00，则8月14号20:00起可查询到该事航班信息，在此之前无法查询到信息。
    
3. 意图调用：点击小艺建议卡片中的模板卡片，在测试应用冷启动或热启动的场景下都能够跳转至测试应用的目标页面，则说明意图调用的过程是正确的。
    
    【举例】点击小艺建议卡片中的模板卡片，会跳转至该用户的购票详情页面。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-event-rec-access-programme "接入方案")
# 场景体验

更新时间: 2025-12-16 16:27

## 典型场景

华为意图框架位置感知推荐能力主要支持室内位置推荐、室外近场位置推荐、跨域位置推荐等高确定性场景，结合华为智慧决策能力，在小艺建议入口推荐更贴心、更及时、更满足用户诉求的场景卡片。场景示例：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162754.32336667753870926686794628792820:50001231000000:2800:6351D3BA2AC70B1E22051A3FA728061F9842F832CD16C46DAF3F65FC46955195.png "点击放大")

|推荐类型|能力概述|适用场景|
|:--|:--|:--|
|室内位置推荐|基于：<br><br>- WLAN指纹识别<br>- 基站Cell信息定位<br>- Beacon定位<br><br>用户进入店内、场馆内触发围栏感知，可实现室内精准定位感知能力。|适用于室内多楼层、小范围高精度定位场景，如美食门店、博物馆、体育馆、医院科室、银行、政务大厅、地铁站等。|
|室外近场位置推荐|基于：<br><br>- POI多边形围栏<br>- POI点+半径<br>- Beacon定位<br><br>用户到达指定位置附近或进入区域范围后触发围栏感知。|适用于室外区域范围定位分发场景，如商圈、景区、医院、机场、火车站、加油站、停车场等。|
|跨域位置推荐|主要基于城市、国家级别围栏触发感知，用户跨城、出境触发围栏感知，可实现跨域定位感知能力。|适用于跨城、出境定位场景，如到新城市推旅游攻略场景。|

## 卡片展示效果

基于POI（Point of interest）和Beacon（蓝牙信标设备）触发的位置推荐场景，由近场服务提供模板卡片的配置入口，开发者开通近场服务权限后自行配置。卡片的尺寸样式可参考：[近场服务-POI接入小艺建议场景-创建全网态服务-创建全网态服务](https://developer.huawei.com/consumer/cn/doc/app/agc-help-xiaoyi-create-formalstate-service-0000002349016144)

基于WLAN指纹和Cell触发的位置推荐场景，意图框架提供标准的卡片模板。卡片由华为侧统一配置。

**卡片模板参考：**

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162754.52594990517443221019999212445340:50001231000000:2800:2C3EF62C37F2FD3FB480D9C824F94BE8B03D25D6275B94607FA25C025FE1E74E.png "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-local-rec-introduction "概述")
# 接入方案

更新时间: 2025-12-16 16:27

## 方案概述

位置感知推荐能力支持开发者云侧共享位置信息与关联推荐的内容，结合实时位置、设备状态与习惯标签完成系统智慧决策，在小艺建议智慧推荐更符合用户诉求的内容信息。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162757.25150118108554168171185749344825:50001231000000:2800:70369E1F2342F4F2A36616588AB1F77F73E39C4611EFE738300C87291A3F304F.png "点击放大")

## 开通近场服务权限

近场服务是华为软硬协同解决方案中的关键能力环节，旨在帮助商家触达更多HarmonyOS用户，并为这些用户提供更精准、更优质的服务。开通近场服务的步骤详情参考：[近场服务-申请开通权限](https://developer.huawei.com/consumer/cn/doc/app/agc-help-xiaoyi-create-formalstate-service-0000002349016144)。

## 意图声明

以“搜索旅游攻略”特性为例，开发者首先要注册“查看旅游攻略”（viewTravelGuides），其他意图见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。

开发者需要编辑对应的意图配置insight_intent.json文件实现意图声明。insight_intent.json文件需要放置在任意一个module下面的指定目录：src/main/resources/base/profile/insight_intent.json，并且整个工程中只能存在一个insight_intent.json文件。

1. {
2.   // 应用支持的意图列表
3.   // 必须声明应用支持插件包含的必选意图，应用上架时会进行校验
4.   "insightIntents": [
5.     {
6.       // 意图名称
7.       // 名称应当遵循意图框架规范，当前仅支持预置垂域意图，不允许自定义
8.       // 应用内意图名称唯一，不允许出现相同的名称定义
9.       "intentName": "ViewTravelGuides",
10.       // 意图所属的垂域
11.       "domain": "TravelDomain",
12.       // 意图版本号
13.       // 插件引用意图时会校验该版本号，只有和插件定义的版本号一致才能正常调用
14.       "intentVersion": "1.0.1",
15.       // 意图调用逻辑入口
16.       "srcEntry": "./ets/entryability/InsightIntentExecutorImpl.ets",
17.       "uiAbility": {
18.         // 意图所在ability
19.         "ability": "EntryAbility",
20.         // UIAbility支持前后台两种执行模式
21.         "executeMode": [
22.           "background",
23.           "foreground"
24.         ]
25.       }
26.     }
27.   ]
28. }

## 端侧前台意图调用

开发者需自己实现InsightIntentExecutor，并在对应回调实现打开落地页（点击推荐卡片跳转的界面，如旅游攻略落地页）的能力，ViewTravelGuides的意图调用字段定义见查看旅游攻略（ViewTravelGuides）。

步骤如下：

1. 继承InsightIntentExecutor；
2. 重写对应方法，例如目标拉起前台页面，则可重写onExecuteInUIAbilityForegroundMode方法；
3. 通过意图名称，识别查看旅游攻略意图(ViewTravelGuides)，在对应的方法中传递意图参数（param），并拉起对应落地页（点击推荐卡片跳转的界面，如旅游攻略落地页）。

4. import { insightIntent, InsightIntentExecutor } from '@kit.AbilityKit';
5. import { window } from '@kit.ArkUI';
6. import { BusinessError } from '@kit.BasicServicesKit';
7. /**
8.  * 意图调用样例 */
9. export default class InsightIntentExecutorImpl extends InsightIntentExecutor {
10.   private static readonly VIEW_TRAVEL_GUIDES = 'ViewTravelGuides';
11.   /**
12.    * override 执行前台UIAbility意图
13.    *
14.    * @param name 意图名称
15.    * @param param 意图参数
16.    * @param pageLoader 窗口
17.    * @returns 意图调用结果
18.    */
19.   onExecuteInUIAbilityForegroundMode(name: string, param: Record<string, Object>, pageLoader: window.WindowStage):
20.     Promise<insightIntent.ExecuteResult> {
21.     // 根据意图名称分发处理逻辑，接入方可根据实际业务实现页面跳转
22.     switch (name) {
23.       case InsightIntentExecutorImpl.VIEW_TRAVEL_GUIDES:
24.         return this.viewTravelGuides(param, pageLoader);
25.       default:
26.         break;
27.     }
28.     return Promise.resolve({
29.       code: -1,
30.       result: {
31.         message: 'unknown intent'
32.       }
33.     } as insightIntent.ExecuteResult)
34.   }
35.   /**
36.    * 实现调用查看旅游攻略功能
37.    *
38.    * @param param 意图参数
39.    * @param pageLoader 窗口
40.    */
41.   private viewTravelGuides(param: Record<string, Object>, pageLoader: window.WindowStage): Promise<insightIntent.ExecuteResult> {
42.     return new Promise((resolve, reject) => {
43.       // TODO 实现意图调用，loadContent的入参为旅游攻略落地页路径，例如：pages/TravelGuidePage
44.       pageLoader.loadContent('pages/TravelGuidePage')
45.         .then(() => {
46.           let entityId: string = (param.items as Array<object>)?.[0]?.['entityId'];
47.           // TODO 调用成功的情况，此处可以打印日志
48.           resolve({
49.             code: 0,
50.             result: {
51.               message: 'Intent execute succeed'
52.             }
53.           });
54.         })
55.         .catch((err: BusinessError) => {
56.           // TODO 调用失败的情况
57.           resolve({
58.             code: -1,
59.             result: {
60.               message: 'Intent execute failed'
61.             }
62.           })
63.         });
64.     })
65.   }
66. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-local-rec-scene-experience "场景体验")
# POI方案

更新时间: 2025-12-16 16:28

根据与华为方锁定的场景选择的POI方案对应步骤详情参考：

[近场服务-POI接入小艺建议场景](https://developer.huawei.com/consumer/cn/doc/app/agc-help-location-sense-by-poi-xiaoyi-0000002349175920)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-local-rec-dp-self-validation "开发者测试")
# 场景体验

更新时间: 2025-12-16 16:27

用户通过小艺对话进行自然语言输入实现服务闭环和内容查询。主要场景分为两大类：任务执行和功能一步达。其中任务执行体验又分为两种：功能服务类和信息交互类。

1. 任务执行：
    - 功能服务类：端侧意图调用直接进入应用或元服务对应意图功能服务页面，可携带业务参数。
    - 信息交互类：端侧或云侧意图调用进行内容查询后展示，用户点击进行端侧意图调用闭环（此场景请发送邮件至“hagservice@huawei.com”邮箱申请接入）。
2. 功能一步达：端侧意图调用直接进入应用功能页面，无需其他业务参数，开发者可自定义批量声明接入。

## 典型场景

### 功能服务类

- 跳转页面不带参数场景。例如查询交易明细：语音对话输入“查询XX银行卡交易明细”，即跳转至对应App落地页。
- 跳转页面带参数场景。例如用XX应用打车：语音对话输入“用xx应用打车去xx商场”，即可跳转对应打车页面并填入提取的地址信息。
- 功能执行并展示窗口化界面。例如操控蓝牙开关：语音对话输入“打开蓝牙”，即可弹窗蓝牙设置窗口，并执行打开蓝牙开关操作。

### 信息交互类

- 内容展示场景。例如查找菜谱：语音对话输入“鱼香肉丝怎么做”，即可搜索到对应的菜谱。
- 功能履约场景。例如订电影票：语音对话输入“买两张今天的电影票，xxx电影”，即可进行电影票购买选座。

### 功能一步达

开发者将应用内的功能声明接入意图框架后，用户可以通过小艺直接打开相应功能页面，比如“打开华为视频的会员中心“，可直接拉起对应页面，实现一步直达。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162755.85257937616985392389393074662949:50001231000000:2800:A29B6F191E88CACCAA554AC2F44895F69C4EF78F8BE07F43A580FD7A56D874B0.png "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-introduction "概述")
# 任务执行类场景方案（配置文件接入方式）

更新时间: 2025-12-16 16:28

## 方案概述

开发者需要按照意图定义，进行意图注册并实现意图调用；用户通过对小艺对话进行自然语言输入，小艺理解语义转换成意图调用（含意图参数），执行意图调用实现对应交互体验。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162808.43485410818098204785387588933921:50001231000000:2800:525285A422AFF560F065F6DACF147BC92743E028FF986F7DC696B4E92F31DC84.png "点击放大")

#### 意图声明

以“搜索旅游攻略”特性为例，开发者首先要注册“查看旅游攻略”（viewTravelGuides），其他意图见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。

开发者需要编辑对应的意图配置insight_intent.json文件实现意图注册。insight_intent.json文件需要放置在module下面的指定目录：src/main/resources/base/profile/insight_intent.json，并且整个工程中只能存在一个insight_intent.json文件。

1. {
2.   // 应用支持的意图列表
3.   // 必须声明应用支持插件包含的必选意图，应用上架时会进行校验
4.   "insightIntents": [
5.     {
6.       // 意图名称
7.       // 名称应当遵循意图框架规范，当前仅支持预置垂域意图，不允许自定义
8.       // 应用内意图名称唯一，不允许出现相同的名称定义
9.       "intentName": "ViewTravelGuides",
10.       // 意图所属的垂域
11.       "domain": "TravelDomain",
12.       // 意图版本号
13.       // 插件引用意图时会校验该版本号，只有和插件定义的版本号一致才能正常调用
14.       "intentVersion": "1.0.1",
15.       // 意图调用逻辑入口
16.       "srcEntry": "./ets/entryability/InsightIntentExecutorImpl.ets",
17.       "uiAbility": {
18.         // 意图所在ability
19.         "ability": "EntryAbility",
20.         // UIAbility支持前后台两种执行模式
21.         "executeMode": [
22.           "background",
23.           "foreground"
24.         ]
25.       },
26.       "uiExtension": {//提供意图执行的窗口化界面时需要进行的声明配置
27.         "ability": "insightIntentUIExtensionAbility"，//意图调用API所在ability名称
28.       }
29.     }
30.   ]
31. }

## 端侧前台意图调用

开发者需自己实现InsightIntentExecutor，并在对应回调实现打开落地页（点击推荐卡片跳转的界面，如旅游攻略详情页）的能力，ViewTravelGuides的意图调用字段定义见查看旅游攻略（ViewTravelGuides）。

步骤如下：

1. 继承InsightIntentExecutor。
2. 重写对应方法，例如目标拉起前台页面，则可重写onExecuteInUIAbilityForegroundMode方法。
3. 通过意图名称，识别查看旅游攻略意图（ViewTravelGuides），在对应的方法中传递意图参数（param），并拉起对应落地页（点击推荐卡片跳转的界面，如旅游攻略页面）。

4. import { insightIntent, InsightIntentExecutor } from '@kit.AbilityKit';
5. import { window } from '@kit.ArkUI';
6. import { BusinessError } from '@kit.BasicServicesKit';
7. /**
8.  * 意图调用样例 */
9. export default class InsightIntentExecutorImpl extends InsightIntentExecutor {
10.   private static readonly VIEW_TRAVEL_GUIDES = 'ViewTravelGuides';
11.   /**
12.    * override 执行前台UIAbility意图
13.    *
14.    * @param name 意图名称
15.    * @param param 意图参数
16.    * @param pageLoader 窗口
17.    * @returns 意图调用结果
18.    */
19.   onExecuteInUIAbilityForegroundMode(name: string, param: Record<string, Object>, pageLoader: window.WindowStage):
20.     Promise<insightIntent.ExecuteResult> {
21.     // 根据意图名称分发处理逻辑。接入方可根据实际业务实现页面跳转
22.     switch (name) {
23.       case InsightIntentExecutorImpl.VIEW_TRAVEL_GUIDES:
24.         return this.viewTravelGuides(param, pageLoader);
25.       default:
26.         break;
27.     }
28.     return Promise.resolve({
29.       code: -1,
30.       result: {
31.         message: 'unknown intent'
32.       }
33.     } as insightIntent.ExecuteResult)
34.   }
35.   /**
36.    * 实现调用查看旅游攻略功能
37.    *
38.    * @param param 意图参数
39.    * @param pageLoader 窗口
40.    */
41.   private viewTravelGuides(param: Record<string, Object>, pageLoader: window.WindowStage): Promise<insightIntent.ExecuteResult> {
42.     return new Promise((resolve, reject) => {
43.       // TODO 实现意图调用，loadContent的入参为旅游攻略落地页路径，例如：pages/TravelGuidePage
44.       pageLoader.loadContent('pages/TravelGuidePage')
45.         .then(() => {
46.           let entityId: string = (param.items as Array<object>)?.[0]?.['entityId'];
47.           // TODO 调用成功的情况，此处可以打印日志
48.           resolve({
49.             code: 0,
50.             result: {
51.               message: 'Intent execute success'
52.             }
53.           });
54.         })
55.         .catch((err: BusinessError) => {
56.           // TODO 调用失败的情况
57.           resolve({
58.             code: -1,
59.             result: {
60.               message: 'Intent execute failed'
61.             }
62.           })
63.         });
64.     })
65.   }
66. }

## 端侧前台窗口意图调用

开发者需自己实现InsightIntentExecutor，并在对应回调实现窗口页面内容加载的能力。

步骤如下：

1. 继承InsightIntentExecutor。
2. 重写对应方法，例如目标拉起前台窗口化页面，则可重写onExecuteInUIExtensionAbility方法。
3. 通过意图名称，识别打开蓝牙意图（LoadBluetoothCard）调用扩展意图，在对应的方法中传递意图参数（param），并拉起对应窗口化页面（如打开蓝牙窗口化页面）。

4. import { insightIntent, InsightIntentExecutor, UIExtensionContentSession } from '@kit.AbilityKit';
5. import { window } from '@kit.ArkUI';
6. /**
7.  * 意图调用样例 */
8. export default class IntentExecutorImpl extends InsightIntentExecutor {
9.   private static readonly TAG: string = 'IntentExecutorImpl';
10.   private static readonly LOAD_BLUETOOTH_CARD: string = 'LoadBluetoothCard';
11.   /**
12.    * override 执行前台UI扩展意图
13.    *
14.    * @param name 意图名称
15.    * @param param 意图参数
16.    * @param pageLoader 窗口
17.    * @returns 意图调用结果
18.    */
19.   async onExecuteInUIExtensionAbility(name: string, param: Record<string, Object>,
20.     pageLoader: UIExtensionContentSession):
21.     Promise<insightIntent.ExecuteResult> {
22.     console.info(IntentExecutorImpl.TAG, `onExecuteInUIExtensionAbility`);
23.     switch (name) {
24.       case IntentExecutorImpl.LOAD_BLUETOOTH_CARD:
25.         console.info(IntentExecutorImpl.TAG, `onExecuteInUIAbilityForegroundMode::ForegroundUiAbility intent`);
26.         return this.openLoadBluetoothCard(pageLoader);
27.       default:
28.         console.info(IntentExecutorImpl.TAG, `onExecuteInUIAbilityForegroundMode::invalid intent`);
29.         break;
30.     }
31.     let result: insightIntent.ExecuteResult = {
32.       code: -1,
33.       result: {
34.         message: 'onExecuteInUIExtensionAbility failed'
35.       }
36.     };
37.     return result;
38.   }
39.   /**
40.    * 打开加载蓝牙卡片意图
41.    *
42.    * @param pageLoader 意图内容Session对象
43.    * @returns 执行结果
44.    */
45.   private async openLoadBluetoothCard(pageLoader: UIExtensionContentSession): Promise<insightIntent.ExecuteResult> {
46.     pageLoader.loadContent('pages/UiExtensionPage');
47.     let result: insightIntent.ExecuteResult = {
48.       code: 0,
49.       result: {
50.         message: 'intent execute success'
51.       }
52.     }
53.     return result;
54.   }
55. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-access-introduction "概述")
# 方案概述

更新时间: 2025-12-16 16:28

从6.0.0(20)开始，支持通过装饰器开发意图，支持将现有功能通过装饰器快速集成至系统入口。开发者可自定义意图，通过添加装饰器方式实现意图快速接入，支持Link跳转、Page和函数等意图装饰器，方便开发者快速开放应用内功能。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162813.43318732530216321492866571895811:50001231000000:2800:38574B9063966E340E828EFAF429F9A768582C12D6B99B32BB0E2575CEAB50B8.png "点击放大")

开发者可根据想要暴露的应用功能，选择不同类型的装饰器进行意图声明：

- [基于Link的装饰器：@InsightIntentLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-decorator-link)
    
    在开发者已实现的DeepLink，AppLink上添加装饰器，实现功能页面的拉起。
    
    约束：仅支持前台执行。
    

- [基于Page的装饰器：@InsightIntentPage](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-decorator-page)
    
    在开发者已实现的Page上添加装饰器，实现功能页面的拉起。
    
    约束：仅支持前台执行，仅支持Navigation架构。
    

- [基于函数的装饰器：@InsightIntentFunction和@InsightIntentFunctionMethod](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-decorator-function)
    
    在目标执行函数上添加@InsightIntentFunctionMethod装饰器，以及在目标执行函数所属Class上添加@InsightIntentFunction进行意图声明，实现目标函数的执行。
    
    约束：仅支持后台执行。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-decorator "任务执行类场景方案（装饰器接入方式）")
# 基于Link的装饰器方案

更新时间: 2025-12-16 16:28

开发者使用@InsightIntentLink装饰器进行基于Link的意图声明，可快速将已实现的Link跳转功能接入意图框架，以购买电影票意图为例，详细说明如下：

1. 装饰器的添加位置：装饰器建议添加到处理该Link的Class上，如下所示。
    
    1. import { InsightIntentLink, LinkParamCategory } from "@ohos.app.ability.InsightIntentDecorator";
    2. import { url } from "@kit.ArkTS";
    
    3. @InsightIntentLink({
    4.   intentName: 'PurchaseMovieTickets',
    5.   domain: 'PurchaseTickets',
    6.   intentVersion: '1.0.1',
    7.   displayName: '购买电影票',
    8.   llmDescription: '用于在线购买电影票，允许用户选择指定影院、电影和场次时间进行购票。在用户明确表达购票需求，且已提供所有必要信息（cinema, film, time）时使用。如果信息不全或者用户只是查询电影信息、放映时间或票价，不应调用此工具。',
    9.   uri: 'decorator://ability.entry/main',
    10.   parameters: {
    11.     "type": "object",
    12.     "properties": {
    13.       "cinema": {
    14.         "type": "string",
    15.         "description": "目标影院名称，仅支持平台合作的影院"
    16.       },
    17.       "film": {
    18.         "type": "string",
    19.         "description": "目标电影名称，需为当前上映或即将上映且在影院排片列表中的电影"
    20.       },
    21.       "time": {
    22.         "type": "string",
    23.         "description": "放映时间，必须为未来的场次，且需为影院当天有效排片时间；时间格式应为'YYYY-MM-DD HH:MM'（例如'2025-07-01 19:30'）"
    24.       }
    25.     },
    26.     "required": ["cinema", "film", "time"]
    27.   },
    28.   paramMappings:[
    29.     {
    30.       paramName: 'cinema',
    31.       paramMappingName: 'location',
    32.       paramCategory: LinkParamCategory.LINK
    33.     },
    34.     {
    35.       paramName: 'film',
    36.       paramMappingName: 'title',
    37.       paramCategory: LinkParamCategory.LINK
    38.     },
    39.     {
    40.       paramName: 'time',
    41.       paramMappingName: 'time',
    42.       paramCategory: LinkParamCategory.LINK
    43.     }
    44.   ]
    45. })
    46. **export class** PurchaseMovieTicketsLinkIntent {
    47.    **private** purchaseMovieTickets(uri: string): void {
    48.      _// 从want中获取传入的链接信息。_
    49.      _// 如传入的url为：decorator://ability.entry/main?location=XXX影城&title=XXX&time=2025.06.01_
    50.      **let** urlObject = url.URL.parseURL(uri);
    51.      **let** location = urlObject.params.get('location');
    52.      **if** (location === "XXX影城") {
    53.        _// ..._
    54.      }
    55.    }
    56.  }
    
2. 装饰器的字段说明以及示例：@InsightIntentLink字段以及具体说明如下。
    
    |**字段名称**|**类型**|**必选**|**说明**|
    |:--|:--|:--|:--|
    |intentName|string|是|意图名称，最大长度：64。|
    |domain|string|是|意图所属的功能垂域。|
    |intentVersion|string|是|意图的版本号，用于兼容性管理。|
    |displayName|string|是|意图的展示名称，用于界面显示，最大长度：64。|
    |llmDescription|string|否|意图的描述，详细描述该意图可实现的能力，便于大模型理解并调用，接入自定义意图时，该字段必选。|
    |uri|string|是|Link跳转uri。|
    |parameters|Record<string, object >|否|意图参数定义，描述参数类型以及含义。|
    |paramMappings|[LinkIntentParamMapping[]](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-decorator-link#table1558332918513)|否|Link的参数映射，定义了意图入参与uri拼接参数的映射关系，如果需要参数映射或者需要添加wantParams，需要使用该字段。|
    |result|Record<string, object >|否|意图执行返回结果定义。|
    
    LinkIntentParamMapping结构如下表：
    
    |**字段名称**|**类型**|**必选**|**说明**|
    |:--|:--|:--|:--|
    |paramName|string|是|映射后的意图参数名称。|
    |paramMappingName|string|否|映射前的Link参数名称，意图调用时可将意图参数映射为Link参数，用于适配已有的Link调用。|
    |paramCategory|LinkParamCategory|否|Link参数类型枚举，默认作为域名参数，设置为“link”类型；如需要wantParams，则需要设置为“want”类型。|
    
    为便于大模型理解和调用，相关参数定义需要遵照[自定义意图相关信息定义规范](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-specification)。
    
3. 添加装饰器的方式：装饰器可以直接手动添加，同时也支持一键生成装饰器，建议使用后者，此方式需要安装相应插件，详细步骤如下：
    
    1. 打开CodeGenie插件：在DevEco Studio右侧边栏点击CodeGenie或输入快捷键Alt/Option+U，可以进入DevEco CodeGenie。若使用非最新版本的DevEco Studio，可通过[下载中心](https://developer.huawei.com/consumer/cn/download/deveco-codegenie)获取并使用相关功能，具体请参考[插件获取及安装](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie#section18337533718)。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162813.28470262338000088087774604538262:50001231000000:2800:828E0BFC020C3957FD19D2FB18D6E26B7F342EF2635D43C6883D7CD059E43580.png "点击放大")
        
    2. 框选想要接入意图框架功能的代码。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162814.76828759941558529576367243518646:50001231000000:2800:73A533628C3323EDBF4490C4AC70018E13D8F911C60C43F13C89EE02D489841A.png "点击放大")
        
    3. 在选中的代码块上右键CodeGenie > Insight Intent > 选择适合的装饰器。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162814.46477546695012667774492260496011:50001231000000:2800:43C150D0015BE6F5ED23FB6F800071D7D863268633D0DB18E03B240663E3151B.png "点击放大")
        
    4. 在DevEco CodeGenie对话框中对意图定义、功能和参数等进行描述。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162814.94381605153158297057370222701814:50001231000000:2800:288584660AE6703C0646D752EA44FE68E8C834458F0A73096D15493983DD9D45.png "点击放大")
        
    5. 回车或者点击发送按钮，即可生成对应的装饰器内容。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162814.35011903348070534305311085370517:50001231000000:2800:02CF725E19C4E10861CAC4AB675002B7EA687E239A12E996163F7E0B03D3454A.png "点击放大")
        
    6. 将光标放置于要插入装饰器的位置，点击插入图标，即可在对应位置插入装饰器。
    
    插入前：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162814.81868352528902359634719471294749:50001231000000:2800:977DA8AEA66D58BCF6D7D2C0CCA21CB37918CEABA4B93ECB569939ECE0ABABC8.png "点击放大")
    
    插入后：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162814.01473333728358564034267884456927:50001231000000:2800:C7162005095999BDD064D37B5FF3CA32595B9633205647F4EA64DE99D2B4EF93.png "点击放大")
    
4. 装饰器的使用约束和说明：
    - Link装饰器包含通过Link接入意图的所有配置，因此对装饰器所在Class、变量、成员没有要求，但是必须要在被依赖的ets文件中添加装饰器才可以被编译。
    - 支持开发者设置wantParameter，执行Link时，会将该参数附带到want的parameter中。
    - 装饰器方式仅支持参数名映射，不做参数加工，包括取值转换、合并等情况。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-decorator-overview "方案概述")
# 基于Page的装饰器方案

更新时间: 2025-12-16 16:28

开发者使用@InsightIntentPage装饰器进行基于Page的意图声明，可快速将已有的Page页面接入意图框架，以购买电影票的意图为例，详细说明如下：

1. 装饰器添加位置：基于Page的装饰器需要添加在Entry页面组件上，建议在目标页面中进行声明。
    
    1. import { InsightIntentPage } from "@ohos.app.ability.InsightIntentDecorator";
    
    2. @Builder
    3. export function PurchaseMovieTicketsIntentPageBuilder(pageName: string, param: object) {
    4.   PurchaseMovieTicketsIntentPage({ param: param });
    5. }
    
    6. @InsightIntentPage({
    7.   intentName: 'PurchaseMovieTickets',
    8.   domain: 'PurchaseTickets',
    9.   intentVersion: '1.0.1',
    10.   displayName: '购买电影票',
    11.   llmDescription: '用于在线购买电影票，允许用户选择指定影院、电影和场次时间进行购票。在用户明确表达购票需求，且已提供所有必要信息（cinema, film, time）时使用。如果信息不全或者用户只是查询电影信息、放映时间或票价，不应调用此工具。',
    12.   uiAbility: 'EntryAbility',
    13.   pagePath: './ets/pages/MainPage',
    14.   navDestinationName: 'PurchaseMovieTicketsIntentPage',
    15.   parameters: {
    16.     "type": "object",
    17.     "properties": {
    18.       "cinema": {
    19.         "type": "string",
    20.         "description": "目标影院名称，仅支持平台合作的影院"
    21.       },
    22.       "film": {
    23.         "type": "string",
    24.         "description": "目标电影名称，需为当前上映或即将上映且在影院排片列表中的电影"
    25.       },
    26.       "time": {
    27.         "type": "string",
    28.         "description": "放映时间，必须为未来的场次，且需为影院当天有效排片时间；时间格式应为'YYYY-MM-DD HH:MM'（例如'2025-07-01 19:30'）"
    29.       }
    30.     },
    31.     "required": ["cinema", "film", "time"]
    32.   }
    33. })
    34. @Entry
    35. @Component
    36. struct PurchaseMovieTicketsIntentPage {
    37.   param: object = new Object();
    38.   cinema: string = '';
    39.   film: string = '';
    40.   time: string = '';
    41.   aboutToAppear(): void {
    42.     this.cinema= this.param?.['cinema'];
    43.     this.film = this.param?.['film'];
    44.     this.time = this.param?.['time'];
    45.   }
    46.   build() {
    47.     NavDestination(){
    48.       Text(`${this.cinema} ${this.film} ${this.time}`)
    49.         .fontSize(30)
    50.         .fontWeight(FontWeight.Bolder)
    51.     }
    52.     .title('IntentPage')
    53.     .width('100%')
    54.   }
    55. }
    
2. 装饰器的字段说明以及示例：@InsightIntentPage字段以及具体说明如下。
    
    |字段名称|类型|必选|说明|
    |:--|:--|:--|:--|
    |intentName|string|是|意图名称，最大长度：64。|
    |domain|string|是|意图所属的功能垂域。|
    |intentVersion|string|是|意图的版本号，用于兼容性管理。|
    |displayName|string|是|意图的展示名称，用于界面显示，最大长度：64。|
    |llmDescription|string|否|意图的描述，详细描述该意图可实现的能力，便于大模型理解并调用。|
    |parameters|Record<string, object>|否|意图参数定义，描述参数类型以及含义。|
    |uiAbility|string|否|页面依赖的UiAbility名，如果不传递默认使用EntryAbility。|
    |pagePath|string|是|Navigation组件所在页面的路径，路径基于Module的根目录的相对路径。|
    |navDestinationName|string|否|Navigation子页面名称，如果不填写，则跳转到pagePath指定的页面。|
    
    为便于大模型理解和调用，相关参数定义需要遵照[自定义意图相关信息定义规范](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-specification)。
    
3. 装饰器的添加方式：装饰器可以直接手动添加，同时也支持一键生成装饰器，建议使用后者，此方式需要安装相应插件，详细步骤如下。
    1. 打开CodeGenie插件：在DevEco Studio右侧边栏点击CodeGenie或输入快捷键Alt/Option+U，可以进入DevEco CodeGenie。若使用非最新版本的DevEco Studio，可通过[下载中心](https://developer.huawei.com/consumer/cn/download/deveco-codegenie)获取并使用相关功能，具体请参考[插件获取及安装](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-codegenie#section18337533718)。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162815.57439369698613657293264250662072:50001231000000:2800:A11752101727785BE18B7D20C0D183D915780D0C82302D1EF4AF89B12313F41F.png "点击放大")
        
    2. 框选想要接入意图框架功能的代码。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162815.00189102068821844890011914145916:50001231000000:2800:E22AEF2D0E739E280F633401F8B6A9DB2EBD6703EFD715C927886E230580B9B8.png "点击放大")
        
    3. 在选中的代码块上右键CodeGenie > Insight Intent > 选择适合的装饰器。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162815.81289549283940054812995754972653:50001231000000:2800:BB3B0CBED0DD2C4166EDC5E28BED4A000199F7223EB1F8B068AAC6BA710033D7.png "点击放大")
        
    4. 在DevEco CodeGenie对话框中对意图定义，功能，参数等进行描述。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162815.84772461142040004822645360626891:50001231000000:2800:5D63EABAD1192ABA3A2501BBABF5C1AAC08EF70E8FB406588D6E248972D51AD6.png "点击放大")
        
    5. 回车或者点击发送按钮，即可生成对应的装饰器内容。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162815.25747524691529661721427465865096:50001231000000:2800:096D32EC0E3BA394242C3B9FDE48D95176361FE2116B5067AD1C4E7CEAE900FA.png "点击放大")
        
    6. 将光标放置于要插入装饰器的位置，点击插入图标，即可在对应位置插入装饰器。
        
        插入前：
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162816.94578875810946401116115388775975:50001231000000:2800:FD062E502F3B185A85F6D727A28E8744186FFA5F04F045DD8517DA613E3B688A.png "点击放大")
        
        插入后：
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162816.98197264356823328319469897521916:50001231000000:2800:DBEB04A11F5A0BF78B16719B44AA5E9A54496B47179F6C16A6550D5BA0F5B6B9.png "点击放大")
        
4. 装饰器的使用约束和说明：
    - 仅支持Navigation页面架构跳转。
    - 该跳转不能有自定义上下文依赖，比如必须打开前置页面才能跳转，开发者需要进行验证，确认兜底策略。
    - 跳转页面时，默认使用Navigation页面栈进行push，如果开发者需要实现其他跳转逻辑，则需要自行适配。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-decorator-link "基于Link的装饰器方案")
# 自定义意图相关信息定义规范

更新时间: 2025-12-16 16:28

Intents Kit支持开发者自定义意图，开发者可通过在其代码上添加自然语言装饰器接入，装饰器中相关信息建议参考以下规范，以便于大模型更好的理解和分发调用。

1. **意图名称**
    
    意图名称应当遵循动词+名词的结构，命名风格通常使用大写字母开头的驼峰式命名法。命名应精准反映意图的核心功能，不宜过长（最大长度：64）或模糊。
    
    - 形式：动词+名词，采用驼峰命名，如CancelAlarm、CheckWeather、CreateReminder等。
    - 逻辑：意图名应直接描述该意图的操作行为，看到意图名称即可推测出意图功能，且避免使用模棱两可的词汇。例如，SwitchRoute本意是切换导航路线，但SwitchRoute也有切换路由的意思，可以改为SwitchNavigationRoute。
2. **意图描述**
    
    - 准确全面性：确保描述涵盖意图的全部功能，避免遗漏可能的功能点。例如，SendEmail意图的描述应明确指出其能发送邮件的能力，包括发送文本和附件功能。
    - 边界性（功能解耦）：意图必须有清晰的功能边界，避免与其他意图功能重叠或模糊，比如 ShareFile不能通过邮件分享。
    - 独立性：一个意图应只做一件事，如果功能可以拆解，应拆分为多个意图，每个意图各司其职。这样有助于保持结构简洁，功能独立，便于大语言模型的正确理解与使用。
    
    备注：意图描述中可以增加使用示例，举例说明使用者可以如何使用，更有利于大模型理解和分发调用。
    
3. **参数命名**
    
    参数命名应简洁且语义明确，采用小驼峰命名法，确保参数名能够直观反映其功能。
    
    - 语义明确：可简洁明了的看出参数用途。
4. **参数定义**
    
    参数定义包含参数的功能描述、参数类型（type）、必须参数（required）。
    
    - 功能描述：需详细描述每个参数的含义及其对意图功能的影响，每个参数应仅负责一个功能，避免单一参数混合多种用途。例如，modifyAttribute参数，不能同时具有修改属性和属性值的含义。
    - 参数类型（type）：定义参数的类型，如string、int、array等。
    - 必须参数（required）：定位意图的必须参数，使用某一意图时必须指定的参数。

以购买电影票为例，使用基于Link的装饰器来进行意图声明，实现的功能为通过deepLink的方式来拉起电影票购买页面，包含影院，影片名，时间三个自定义参数。

1. import { InsightIntentLink, LinkParamCategory } from "@ohos.app.ability.InsightIntentDecorator";
2. import { url } from "@kit.ArkTS";

3. @InsightIntentLink({
4.   intentName: 'PurchaseMovieTickets',
5.   domain: 'PurchaseTickets',
6.   intentVersion: '1.0.1',
7.   displayName: '购买电影票',
8.   llmDescription: '用于在线购买电影票，允许用户选择指定影院、电影和场次时间进行购票。在用户明确表达购票需求，且已提供所有必要信息（cinema, film, time）时使用。如果信息不全或者用户只是查询电影信息、放映时间或票价，不应调用此工具。',
9.   uri: 'decorator://ability.entry/main',
10.   parameters: {
11.     "type": "object",
12.     "properties": {
13.       "cinema": {
14.         "type": "string",
15.         "description": "目标影院名称，仅支持平台合作的影院"
16.       },
17.       "film": {
18.         "type": "string",
19.         "description": "目标电影名称，需为当前上映或即将上映且在影院排片列表中的电影"
20.       },
21.       "time": {
22.         "type": "string",
23.         "description": "放映时间，必须为未来的场次，且需为影院当天有效排片时间；时间格式应为'YYYY-MM-DD HH:MM'（例如'2025-07-01 19:30'）"
24.       }
25.     },
26.     "required": ["cinema", "film", "time"]
27.   },
28.   paramMappings:[
29.     {
30.       paramName: 'cinema',
31.       paramMappingName: 'location',
32.       paramCategory: LinkParamCategory.LINK
33.     },
34.     {
35.       paramName: 'film',
36.       paramMappingName: 'title',
37.       paramCategory: LinkParamCategory.LINK
38.     },
39.     {
40.       paramName: 'time',
41.       paramMappingName: 'time',
42.       paramCategory: LinkParamCategory.LINK
43.     }
44.   ]
45. })
46. **export class** PurchaseMovieTicketsLinkIntent {
47.    **private** purchaseMovieTickets(uri: string): void {
48.      _// 从want中获取传入的链接信息。_
49.      _// 如传入的url为：decorator://ability.entry/main?location=XXX影城&title=XXX&time=2025.06.01_
50.      **let** urlObject = url.URL.parseURL(uri);
51.      **let** location = urlObject.params.get('location');
52.      **if** (location === "XXX影城") {
53.        _// ..._
54.      }
55.    }
56.  }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-decorator-function "基于函数的装饰器方案")
# 自定义意图相关信息定义规范

更新时间: 2025-12-16 16:28

Intents Kit支持开发者自定义意图，开发者可通过在其代码上添加自然语言装饰器接入，装饰器中相关信息建议参考以下规范，以便于大模型更好的理解和分发调用。

1. **意图名称**
    
    意图名称应当遵循动词+名词的结构，命名风格通常使用大写字母开头的驼峰式命名法。命名应精准反映意图的核心功能，不宜过长（最大长度：64）或模糊。
    
    - 形式：动词+名词，采用驼峰命名，如CancelAlarm、CheckWeather、CreateReminder等。
    - 逻辑：意图名应直接描述该意图的操作行为，看到意图名称即可推测出意图功能，且避免使用模棱两可的词汇。例如，SwitchRoute本意是切换导航路线，但SwitchRoute也有切换路由的意思，可以改为SwitchNavigationRoute。
2. **意图描述**
    
    - 准确全面性：确保描述涵盖意图的全部功能，避免遗漏可能的功能点。例如，SendEmail意图的描述应明确指出其能发送邮件的能力，包括发送文本和附件功能。
    - 边界性（功能解耦）：意图必须有清晰的功能边界，避免与其他意图功能重叠或模糊，比如 ShareFile不能通过邮件分享。
    - 独立性：一个意图应只做一件事，如果功能可以拆解，应拆分为多个意图，每个意图各司其职。这样有助于保持结构简洁，功能独立，便于大语言模型的正确理解与使用。
    
    备注：意图描述中可以增加使用示例，举例说明使用者可以如何使用，更有利于大模型理解和分发调用。
    
3. **参数命名**
    
    参数命名应简洁且语义明确，采用小驼峰命名法，确保参数名能够直观反映其功能。
    
    - 语义明确：可简洁明了的看出参数用途。
4. **参数定义**
    
    参数定义包含参数的功能描述、参数类型（type）、必须参数（required）。
    
    - 功能描述：需详细描述每个参数的含义及其对意图功能的影响，每个参数应仅负责一个功能，避免单一参数混合多种用途。例如，modifyAttribute参数，不能同时具有修改属性和属性值的含义。
    - 参数类型（type）：定义参数的类型，如string、int、array等。
    - 必须参数（required）：定位意图的必须参数，使用某一意图时必须指定的参数。

以购买电影票为例，使用基于Link的装饰器来进行意图声明，实现的功能为通过deepLink的方式来拉起电影票购买页面，包含影院，影片名，时间三个自定义参数。

1. import { InsightIntentLink, LinkParamCategory } from "@ohos.app.ability.InsightIntentDecorator";
2. import { url } from "@kit.ArkTS";

3. @InsightIntentLink({
4.   intentName: 'PurchaseMovieTickets',
5.   domain: 'PurchaseTickets',
6.   intentVersion: '1.0.1',
7.   displayName: '购买电影票',
8.   llmDescription: '用于在线购买电影票，允许用户选择指定影院、电影和场次时间进行购票。在用户明确表达购票需求，且已提供所有必要信息（cinema, film, time）时使用。如果信息不全或者用户只是查询电影信息、放映时间或票价，不应调用此工具。',
9.   uri: 'decorator://ability.entry/main',
10.   parameters: {
11.     "type": "object",
12.     "properties": {
13.       "cinema": {
14.         "type": "string",
15.         "description": "目标影院名称，仅支持平台合作的影院"
16.       },
17.       "film": {
18.         "type": "string",
19.         "description": "目标电影名称，需为当前上映或即将上映且在影院排片列表中的电影"
20.       },
21.       "time": {
22.         "type": "string",
23.         "description": "放映时间，必须为未来的场次，且需为影院当天有效排片时间；时间格式应为'YYYY-MM-DD HH:MM'（例如'2025-07-01 19:30'）"
24.       }
25.     },
26.     "required": ["cinema", "film", "time"]
27.   },
28.   paramMappings:[
29.     {
30.       paramName: 'cinema',
31.       paramMappingName: 'location',
32.       paramCategory: LinkParamCategory.LINK
33.     },
34.     {
35.       paramName: 'film',
36.       paramMappingName: 'title',
37.       paramCategory: LinkParamCategory.LINK
38.     },
39.     {
40.       paramName: 'time',
41.       paramMappingName: 'time',
42.       paramCategory: LinkParamCategory.LINK
43.     }
44.   ]
45. })
46. **export class** PurchaseMovieTicketsLinkIntent {
47.    **private** purchaseMovieTickets(uri: string): void {
48.      _// 从want中获取传入的链接信息。_
49.      _// 如传入的url为：decorator://ability.entry/main?location=XXX影城&title=XXX&time=2025.06.01_
50.      **let** urlObject = url.URL.parseURL(uri);
51.      **let** location = urlObject.params.get('location');
52.      **if** (location === "XXX影城") {
53.        _// ..._
54.      }
55.    }
56.  }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-decorator-function "基于函数的装饰器方案")
# 功能一步达场景方案

更新时间: 2025-12-16 16:28

## 方案概述

从5.1.0(18)开始，新增功能一步达接入方案，可通过该方案实现快速打开应用内功能页面。若应用中有“查找路线”和“扫一扫”两个功能需要注册到意图框架中，让用户通过小艺快速打开对应功能页面，比如“帮我打开XXX的查找路线”、“帮我打开XXX的扫一扫”或“帮我打开XXX的扫码”，则需要在意图声明文件中声明JumpFunctionPage意图，以及上述两个功能，并实现对应意图调用。

**意图名称：跳转App功能页 JumpFunctionPage（端侧前台意图调用）**

|**参数类别**|**参数（中文）**|**参数（英文）**|是否必选|**描述**|类型|**数据样例**|
|:--|:--|:--|:--|:--|:--|:--|
|**Input**|功能页面标识|pageId|是|具体功能的标识，开发者自定义|string|1、2、3…|
|**Output**|结果码|code|是|意图调用的结果码。|number|0：成功<br><br>其他：失败（需提前与华为侧协商，不支持自定义）|
|结果体|result|是|意图调用返回的数据，如果无数据则返回空。|Record<string, Object>|1. {<br>2.   message: 'Intent execute success'<br>3. }|

## 意图声明

开发者需要编辑对应的意图配置insight_intent.json文件实现意图注册。insight_intent.json文件需要放置在module下面的指定目录：src/main/resources/base/profile/insight_intent.json，并且整个工程中只能出现一个insight_intent.json文件。

1. {
2.     "insightIntents": [
3.        {
4.             "intentName": "JumpFunctionPage",    // 意图名称
5.             "domain": "ToolsDomain",
6.             "intentVersion": "1.0.1", // 意图本身的版本号
7.             // 意图调用逻辑入口
8.             "srcEntry": "./ets/entryability/InsightIntentExecutorImpl.ets",
9.             "uiAbility": {
10.             // 意图所在ability
11.             "ability": "EntryAbility",
12.             // UIAbility支持前后台两种执行模式
13.             "executeMode": [
14.                 "foreground"
15.             ]
16.             },
17.             "inputParams": [{ // 部分意图开放意图参数定义，格式整体参考JSON-Schema。 
18.                 "properties": { // 描述参数列表，后续可以同级别增加其他描述节点
19.                     "pageId": { // 具体功能的标识的key值
20.                         "type": "string", // 参数类型
21.                         "enum": [ 
22.                             {
23.                                 "value": "1", // 具体功能的标识的value值
24.                                 "displayName": "查找路线", // 功能名，用于匹配用户query
25.                                 "keywords": [
26.                                     "查路线"，"查询路线"，"路线查询"，"找路线"
27.                                 ], // 参数枚举值别名，可以用于索引、过滤，最多不超过5个
28.                                 "displayDescription": "查找到达目的地的路线", // 功能描述
29.                                 "icon": "https://abc.xx" // 功能图标
30.                             },
31.                             {
32.                                 "value": "2", // 具体功能的标识的value值
33.                                 "displayName": "扫一扫", // 功能名，用于匹配用户query
34.                                 "keywords": [
35.                                     "扫码"
36.                                 ], // 参数枚举值别名，可以用于索引、过滤
37.                                 "displayDescription": "用于扫码", // 功能描述
38.                                 "icon": "https://abc.xx" // 功能图标
39.                             }
40.                         ]
41.                     }
42.                 }
43.             }]
44.         }
45.     ]
46. }

若intentName报错Intent 'xxxxxx' is not included in domain 'xxxxxx'. Select an intent from the list of suggestions.该报错不影响正常编译及运行，请忽略。

## 端侧前台意图调用

开发者需自己实现InsightIntentExecutor，并在对应回调实现打开落地页的能力。

步骤如下：

1. 继承InsightIntentExecutor。
2. 重写对应方法，例如目标拉起前台页面，则可重写onExecuteInUIAbilityForegroundMode方法。
3. 通过意图名称，识别跳转功能页面意图(JumpFunctionPage)，在对应的方法中传递意图参数（param），并拉起对应落地页。

4. import { insightIntent, InsightIntentExecutor } from '@kit.AbilityKit';
5. import { window } from '@kit.ArkUI';
6. import { BusinessError } from '@kit.BasicServicesKit';
7. /**
8.  * 意图调用样例 */
9. export default class InsightIntentExecutorImpl extends InsightIntentExecutor {
10.   private static readonly JUMP_FUNCTION_PAGE = 'JumpFunctionPage';
11.   /**
12.    * override 执行前台UIAbility意图
13.    *
14.    * @param name 意图名称
15.    * @param param 意图参数
16.    * @param pageLoader 窗口
17.    * @returns 意图调用结果
18.    */
19.   onExecuteInUIAbilityForegroundMode(name: string, param: Record<string, Object>, pageLoader: window.WindowStage):
20.     Promise<insightIntent.ExecuteResult> {
21.     // 根据意图名称分发处理逻辑。接入方可根据实际业务实现页面跳转
22.     switch (name) {
23.       case InsightIntentExecutorImpl.JUMP_FUNCTION_PAGE:
24.         return this.jumpFunctionPage(param, pageLoader);
25.       default:
26.         break;
27.     }
28.     return Promise.resolve({
29.       code: -1,
30.       result: {
31.         message: 'unknown intent'
32.       }
33.     } as insightIntent.ExecuteResult)
34.   }
35.   /**
36.    * 实现跳转目标页面的功能
37.    *
38.    * @param param 意图参数
39.    * @param pageLoader 窗口
40.    */
41.   private jumpFunctionPage(param: Record<string, Object>, pageLoader: window.WindowStage): Promise<insightIntent.ExecuteResult> {
42.     return new Promise((resolve, reject) => {
43.       let pageId: string = param?.pageId as string;
44.       pageLoader.loadContent('pages/'+ pageId)
45.         .then(() => {
46.         resolve({
47.             code: 0,
48.             result: {
49.               message: 'Intent execute success'
50.             }
51.           });
52.         })
53.         .catch((err: BusinessError) => {
54.           // TODO 调用失败的情况
55.           resolve({
56.             code: -1,
57.             result: {
58.               message: 'Intent execute failed'
59.             }
60.           })
61.         });
62.     })
63.   }
64. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-specification "自定义意图相关信息定义规范")
# 配置文件接入方式自测试方案

更新时间: 2025-12-16 16:28

Intents Kit向开发者提供意图调用调试能力。开发者完成代码开发之后，功能正式上架应用市场前，可以在HarmonyOS 5及以上的设备上面进行自验证，调试分为三个步骤：基础信息提供，环境准备，联调验证。

## 基础信息提供

达成开发意向后，开发者发送邮件到邮箱（hagservice@huawei.com）或者联系华为意图框架接口同事，向华为提供测试应用的信息。

|**序号**|**基础****信息**|**描述**|
|:--|:--|:--|
|1|应用名称|应用市场上架的应用名称。|
|2|应用包名|应用市场上架的应用包名。|
|3|华为账号（UID）|参考[附录A获取UID](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-appendix-a-get-uid)。|
|4|应用图标|应用的图标，具体要求如下：<br><br>图标背景：非透明。<br><br>比例&尺寸：1:1，72px*72px。<br><br>大小：不超过1M。<br><br>格式：png、jpg、jpeg。|
|5|接入意图名称|开发者意向接入的意图名称（中英文）。|

## 环境准备

准备一台装有HarmonyOS Next版本的手机设备，通过应用市场将小艺版本升级至最新，并按照以下顺序依次执行，不能更换执行顺序。

1. 保持设备联网，并且设备时间和实际北京时间保持一致。
2. 安装开发完成并携有意图声明文件的应用。
3. 打开开发者调试模式：进入设置 > 机型 > 关于手机，连续点击软件版本7次，弹出“开启“开发者模式””，点击“确认开启”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162803.33973307054115962331221697131653:50001231000000:2800:209D01A412200E87EE59676B2EACC8B601C1C2BC549E252B183B4F6DA53BFD86.png "点击放大")
    
4. 长按电源键唤醒小艺，将半屏态小艺向上拉升至全屏态，点击左上角返回上层，返回后点击右上角的头像，进入“设置”，找到并进入应用网络设置，打开“WLAN下自动更新”开关。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162803.11816285091552385633818245972865:50001231000000:2800:5CEE5A70804ADAB3C3C551647D456130AF76E91E24E808649128855AC5D81C6E.png "点击放大")
    
5. 进入设置 > 系统 > 开发者选项 > 意图框架调试，打开意图框架调试开关，如果下方显示“已切换至真机模式”，则代表真机模式切换成功。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162806.42504102960671901016249896527313:50001231000000:2800:EFA616E431AEBF6F4D4747A808BEB777A410F60B6AC9CAD3A1990BEB0B443D1A.png "点击放大")
    
    【提示】如果出现意图框架调试开关打开后，设备长时间无法出现“已切换至真机模式”时，可以尝试以下操作：
    
    登出华为账号，再登录之后重新开启意图框架调试开关。
    
    在小艺对话中点击右上角头像，设置 > 服务管理 > 注销服务 > 注销服务，然后返回桌面重新点击小艺建议的卡片，将展示“欢迎使用小艺建议”的卡片刷新成有服务推荐的卡片，最后重新开启意图框架调试开关。
    
6. 打开意图调试助手：进入“小艺 > 返回主页面 > 发现”，搜索“意图调试助手”，点击进入意图调试助手。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162806.12173007415252141339705574840818:50001231000000:2800:E9AD9232C123EAA4888EA7E6D8A7153BFF7F8235EC2537C1DDD697887AD787A7.png "点击放大")

完成以上所有步骤，即可进行联调。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-dp-self-validation "开发者测试")
# 装饰器接入方式自测试方案

更新时间: 2025-12-16 16:28

从6.0.0(20)开始，Intents Kit向开发者提供意图调用调试能力。开发者完成代码开发之后，功能正式上架应用市场前，可以在HarmonyOS 5及以上的设备上面进行自验证，调试分为两个步骤：环境准备和联调验证。

## 环境准备

1. 登录[华为开发者联盟](https://developer.huawei.com/consumer/cn/) ，通过“管理中心 > 生态服务 > 智慧服务 > 小艺开放平台（原HarmonyOS服务开放平台） > 意图框架”，点击“立即体验”进入意图注册入口，需使用与应用上架相同的账号登录。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162808.49938453401585300366731791904109:50001231000000:2800:3B8EE768745A353A998B9282D38331DFAAD21CE01333F4E8209C86DF73DDA0BE.png "点击放大")
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162808.50068563801382069615932030588721:50001231000000:2800:50704C8A5D0167D6176E9CDD643FBD727C5828E899D41C83CCF9C48773874C79.png "点击放大")
    
2. 点击注册意图新增意图集。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162808.64229899765828133225297941447694:50001231000000:2800:82283A4C3ADFFA960060296C9B40249332F39F80D73224914C8F1A0769DAA8B6.png "点击放大")
    
    1. 点击新增注册意图，填写注册信息进行创建。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162808.43792641024701375810966221687574:50001231000000:2800:4E62C7C0ED6E1452D2AD52BE3349E404F7904C09A23A981447CACBCAD229EF0D.png "点击放大")
        
        |名称|描述|
        |:--|:--|
        |意图注册协议类型|选择意图标准协议。|
        |意图集（插件）名称|需唯一标识。|
        |分类|开发者根据自定义意图选择对应垂域。|
        
    2. 编辑意图集基本信息。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162808.92527520327343226433652085655422:50001231000000:2800:D54809194AD38B9D07740D452E679C513D03FEFC3153DA8B003C96ACEB97A1A4.png "点击放大")
        
        |名称|描述|
        |:--|:--|
        |意图注册名称|填写应用名称。|
        |APP名称|填写应用名称。|
        |关联APP|选择需要进行测试的应用。|
        |支持的设备类型|选择手机、平板、PC。|
        |版本号|开发者自定义，仅支持正整数。|
        |版本描述|开发者自定义，该内容不对外展示。|
        |图标|尺寸：72*72（1:1）、格式：png、jpg、jpeg、样式要求：方角、不透明背景|
        
3. 添加意图。
    1. 切换至意图页签并添加意图。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162808.23131233920019822688513480664669:50001231000000:2800:5E62F86B42C2D3349B7CCB8CBEC792BA9A2F1AA4DA4315B120587F9187DA5E61.png "点击放大")
        
    2. 选择自定义意图并填入意图信息（根据接入方案进行填入）并确定。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162808.39484070712960140110202031410436:50001231000000:2800:4F7D04B43B6B9BBD89317A6ACB7C5776A599006B91E896BBA6F15A05F7E2D8C8.png "点击放大")
        
    3. 展开已创建的意图，并填入自定义输入、输出参数，点击保存。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162808.69107207778864264344204454398367:50001231000000:2800:5D770133738C465E8DF9E96266B30FA83DE1C710051D6DB28B0A967E163FDFE9.png "点击放大")
        
4. 添加意图使用样本（意图样本用于提升模型对意图识别的准确率）。
    1. 意图使用样本可通过新增/批量导入进行上传。
    2. 若无需添加意图使用样本，打开是否已提供线下样本开关即可。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162809.98392009985645747718856044449781:50001231000000:2800:F5EA0927C1664266E7FCE1297B210775C56BA9C02D1357B3F3BE60756BA1EBD8.png "点击放大")
        
5. 添加账号至真机测试用户组。
    1. 切换至测试页签，点击编辑用户组。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162809.89919961001756536114382773001378:50001231000000:2800:3316C48CB5F5DAF3FDB32D95A6F4C819B01AAF20817348A3A63D80940E042F74.png "点击放大")
        
    2. 点击新增组，输入新用户组名称（名称自定义）。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162809.49502315296157519547976349248515:50001231000000:2800:9A640F6ED2C87A169521DA0552911F23E1214CFB99744F6444DE2FDEE6D01A13.png "点击放大")
        
    3. 选择已新增用户组，点击查看进入。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162809.06200662981095161867438721970802:50001231000000:2800:D8B82DB56D383B85A8977C3E37E53AADBC0B2496A2781362B4495563A6CF6BE9.png "点击放大")
        
    4. 点击添加用户，选择账号类型为邮箱/手机号码，填入后点击确定（测试用户须为该项目团队下的成员）。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162809.74667745858555983392214059560303:50001231000000:2800:CDA024C766CA0FED9153009CC532211CB0B95C26E6D7BF87E31762CB53B36EBA.png "点击放大")
        
    5. 返回测试页签，选择所创建的真机测试用户组进行保存，点击开始测试准备，开发者即可通过HarmonyOS 6.0.0(20)版本及以上的设备在小艺进行端到端测试。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162809.48892459749726063873437596376660:50001231000000:2800:32760ACE67C5408887DEAAC0FCB06FEDEA5E5F15488E7CAB2D6009C181D874AD.png "点击放大")
        

## 联调验证

1. 开发者需确认调试设备系统版本为HarmonyOS 6.0.0(20)及以上。
2. 在调试设备上登录已添加真机测试用户组的华为账号。
3. 检查小艺App是否为应用市场最新版本（需升级至最新版）。
4. 长按电源键/语音唤起小艺，通过小艺进行自验证。
    1. 开发者预期：用户可通过小艺打开应用内页面并传递参数。
    2. 开发者验证：正常跳转目标落地页并收到对应参数。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-dp-self-validation-con "配置文件接入方式自测试方案")
# 功能搜索方案

更新时间: 2025-12-16 16:28

## 方案概述

从5.1.0(18)开始，新增功能搜索接入方案，可通过该方案实现快速打开应用内功能页面。开发者将应用内的功能在意图声明文件中声明，并实现对应的意图调用，即可实现用户在小艺搜索入口直接搜索到应用内功能，点击后可直接拉起应用，直达功能页面。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162806.27657820417026479270016821825388:50001231000000:2800:B182A2A13DBF6A90D8EDED816E5D9D47D73B9519395DE2D954599015E8E35FE2.png "点击放大")

**意图名称：跳转App功能页 JumpFunctionPage（端侧前台意图调用）**

|**参数类别**|**参数（中文）**|**参数（英文）**|是否必选|**描述**|类型|**数据样例**|
|:--|:--|:--|:--|:--|:--|:--|
|**Input**|功能页面标识|pageId|是|具体功能的标识，开发者自定义。|string|1、2、3…。|
|**Output**|结果码|code|是|意图调用的结果码。|number|0：成功。<br><br>其他：失败（需提前与华为侧协商，不支持自定义）。|
|结果体|result|是|意图调用返回的数据，如果无数据则返回空。|Record<string, Object>|1. {<br>2.   message: 'Intent execute success'<br>3. }|

## 意图声明

开发者需要编辑对应的意图配置insight_intent.json文件实现意图注册。insight_intent.json文件需要放置在module下面的指定目录：src/main/resources/base/profile/insight_intent.json，并且整个工程中只能存在一个insight_intent.json文件。

1. {
2.     "insightIntents": [
3.        {
4.             "intentName": "JumpFunctionPage",   // 功能搜意图
5.             "domain": "ToolsDomain",
6.             "intentVersion": "1.0.1", // 意图版本号
7.              // 意图调用逻辑入口
8.             "srcEntry": "./ets/entryability/InsightIntentExecutorImpl.ets",
9.             "uiAbility": {
10.             // 意图所在ability        
11.             "ability": "EntryAbility",
12.             // UIAbility仅支持前台执行模式
13.             "executeMode": [
14.                 "foreground"
15.             ]
16.             },
17.             "inputParams": [{ // 部分意图开放意图参数定义，格式整体参考JSON-Schema。 
18.                 "properties": { // 描述参数列表，后续可以同级别增加其他描述节点
19.                     "pageId": { // 具体功能的标识的key值
20.                         "type": "string", // 参数类型
21.                         "enum": [ 
22.                             {
23.                                 "value": "1", // 具体功能的标识的value值
24.                                 "displayName": "查找路线", // 功能名，小艺搜索展示
25.                                 "keywords": [
26.                                     "查路线"
27.                                 ], // 参数枚举值别名，可以用于索引、过滤，最多不超过5个
28.                                 "displayDescription": "查找到达目的地的路线", // 功能描述，小艺搜索展示
29.                                 "icon": "https://abc.xx" // 功能图标，小艺搜索展示
30.                             },
31.                             {
32.                                 "value": "2", // 具体功能的标识的value值
33.                                 "displayName": "扫一扫", // 功能名，小艺搜索展示
34.                                 "keywords": [
35.                                     "扫码"
36.                                 ], // 参数枚举值别名，可以用于索引、过滤
37.                                 "displayDescription": "用于扫码", // 功能描述，小艺搜索展示
38.                                 "icon": "https://abc.xx" // 功能图标，小艺搜索展示
39.                             }
40.                         ]
41.                     }
42.                 }
43.             }]
44.         }
45.     ]
46. }

## 端侧前台意图调用

开发者自行实现InsightIntentExecutor，并在对应回调实现打开落地页的能力。

步骤如下：

1. 继承InsightIntentExecutor。
2. 重写对应方法，例如目标拉起前台页面，则可重写onExecuteInUIAbilityForegroundMode方法。
3. 通过意图名称，识别跳转功能页面意图（JumpFunctionPage），在对应的方法中传递意图参数（param），并拉起对应落地页。

4. import { insightIntent, InsightIntentExecutor } from '@kit.AbilityKit';
5. import { window } from '@kit.ArkUI';
6. import { BusinessError } from '@kit.BasicServicesKit';
7. /**
8.  * 意图调用样例 */
9. export default class InsightIntentExecutorImpl extends InsightIntentExecutor {
10.   private static readonly JUMP_FUNCTION_PAGE = 'JumpFunctionPage';
11.   /**
12.    * override 执行前台UIAbility意图
13.    *
14.    * @param name 意图名称
15.    * @param param 意图参数
16.    * @param pageLoader 窗口
17.    * @returns 意图调用结果
18.    */
19.   onExecuteInUIAbilityForegroundMode(name: string, param: Record<string, Object>, pageLoader: window.WindowStage):
20.     Promise<insightIntent.ExecuteResult> {
21.     // 根据意图名称分发处理逻辑。接入方可根据实际业务实现页面跳转
22.     switch (name) {
23.       case InsightIntentExecutorImpl.JUMP_FUNCTION_PAGE:
24.         return this.jumpFunctionPage(param, pageLoader);
25.       default:
26.         break;
27.     }
28.     return Promise.resolve({
29.       code: -1,
30.       result: {
31.         message: 'unknown intent'
32.       }
33.     } as insightIntent.ExecuteResult)
34.   }
35.   /**
36.    * 实现跳转目标页面的功能
37.    *
38.    * @param param 意图参数
39.    * @param pageLoader 窗口
40.    */
41.   private jumpFunctionPage(param: Record<string, Object>, pageLoader: window.WindowStage): Promise<insightIntent.ExecuteResult> {
42.     return new Promise((resolve, reject) => {
43.       let pageId: string = param?.pageId as string;
44.       pageLoader.loadContent('pages/'+ pageId)
45.         .then(() => {
46.         resolve({
47.             code: 0,
48.             result: {
49.               message: 'Intent execute success'
50.             }
51.           });
52.         })
53.         .catch((err: BusinessError) => {
54.           // TODO 调用失败的情况
55.           resolve({
56.             code: -1,
57.             result: {
58.               message: 'Intent execute failed'
59.             }
60.           })
61.         });
62.     })
63.   }
64. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-search-rec-access-programme "接入方案")
# 内容搜索方案

更新时间: 2025-12-16 16:28

## 方案概述

当用户使用应用/元服务时，开发者可以按照标准意图Schema（具体意图详见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)）向系统共享数据（数据包含用户行为和内容实体），并实现意图调用（空调用与传参调用）。已实现用户点击卡片后，可后台执行功能（例如播放指定歌曲）或跳转至指定内容页面（例如指定的歌曲播放页面）。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162809.20110941362461148417525428937996:50001231000000:2800:FCF1E0C5841AD2C221DCC5DDD5D5DA8AAC807A3E3003A82AB81F1D1F48C82A64.png "点击放大")

## 意图声明

以歌曲本地搜索特性为例，首先要注册播放歌曲意图（PlayMusic），其他意图见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。

开发者需要编辑对应的意图配置insight_intent.json文件实现意图注册。insight_intent.json文件需要放置在module下面的指定目录：src/main/resources/base/profile/insight_intent.json，并且整个工程中只能存在一个insight_intent.json文件。

1. {
2.   // 应用支持的意图列表
3.   // 必须声明应用支持插件包含的必选意图，应用上架时会进行校验
4.   "insightIntents": [
5.     {
6.       // 意图名称
7.       // 名称应当遵循意图框架规范，当前仅支持预置垂域意图，不允许自定义
8.       // 应用内意图名称唯一，不允许出现相同的名称定义
9.       "intentName": "PlayMusic",
10.       // 意图所属的垂域
11.       "domain": "MusicDomain",
12.       // 意图版本号
13.       // 插件引用意图时会校验该版本号，只有和插件定义的版本号一致才能正常调用
14.       "intentVersion": "1.0.1",
15.       // 意图调用逻辑入口
16.       "srcEntry": "./ets/entryability/InsightIntentExecutorImpl.ets",
17.       "uiAbility": {
18.         // 意图所在ability        
19.       "ability": "EntryAbility",
20.         // UIAbility支持前后台两种执行模式
21.         "executeMode": [
22.           "background",
23.           "foreground"
24.         ]
25.       }
26.     }
27.   ]
28. }

## 意图共享

构建意图对象，并且调用[shareIntent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/intents-arkts-api-insightintent#section161911659112211)，实现意图共享。可同时构建多个PlayMusic或PlayMusicList的意图对象。

以歌曲本地搜索特性为例，首先要注册播放歌曲意图（PlayMusic），其他意图见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。开发者需要编辑对应的意图配置insight_intent.json文件实现意图注册。insight_intent.json文件需要放置在module下面的指定目录：src/main/resources/base/profile/insight_intent.json，并且整个工程中只能存在一个insight_intent.json文件。

1. import { insightIntent } from '@kit.IntentsKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. let playMusicIntent1: insightIntent.InsightIntent;
4. let playMusicIntent2: insightIntent.InsightIntent;
5. // 共享数据接口  意图数组可以是更多的实体
6. insightIntent.shareIntent(this.context, [playMusicIntent1, playMusicIntent2]).then(() => {
7.   console.info('shareIntent succeed');
8. }).catch((err: BusinessError) => {
9.   console.error(`error.code: ${err?.code}, failed because ${err?.message}`);
10. });

PlayMusic的意图共享字段定义见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)定义，代码示例如下：

1. import { insightIntent } from '@kit.IntentsKit';
2. let playMusicIntent: insightIntent.InsightIntent = {
3.   intentName: "PlayMusic",
4.   intentVersion: "1.0.1",
5.   identifier: "52dac3b0-6520-4974-81e5-25f0879449b5",
6.   intentActionInfo: {
7.     actionMode: "EXECUTED",
8.     executedTimeSlots: {
9.       executedStartTime: 1637393212000,
10.       executedEndTime: 1637393112000,
11.     },
12.     currentPercentage: 50,
13.   },
14.   intentEntityInfo: {
15.     entityName: "Music",
16.     entityId: "C10194368",
17.     entityGroupId: "C10194321312",
18.     displayName: "测试歌曲1",
19.     description: "NA",
20.     logoURL: "https://www-file.abc.com/-/media/corporate/images/home/logo/abc_logo.png",
21.     keywords: ["华为音乐", "化妆"],
22.     rankingHint: 99,
23.     expirationTime: 1637393212000,
24.     metadataModificationTime: 1637393212000,
25.     activityType: ["1", "2", "3"],
26.     artist: ["测试歌手1", "测试歌手2"],
27.     lyricist: ["测试词作者1", "测试词作者2"],
28.     composer: ["测试曲作者1", "测试曲作者2"],
29.     albumName: "测试专辑",
30.     duration: 244000,
31.     playCount: 100000,
32.     musicalGenre: ["流行", "华语", "金曲", "00后"],
33.     isPublicData: false,
34.   }
35. }

完整的意图共享示例如下所示，该示例构建了一个PlayMusic意图、一个PlayMusicList意图，并进行了shareIntent调用。

1. import { insightIntent } from '@kit.IntentsKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. let playMusicIntent: insightIntent.InsightIntent = {
4.   intentName: "PlayMusic",
5.   intentVersion: "1.0.1",
6.   identifier: "52dac3b0-6520-4974-81e5-25f0879449b5",
7.   intentActionInfo: {
8.     actionMode: "EXECUTED",
9.     executedTimeSlots: {
10.       executedStartTime: 1637393212000,
11.       executedEndTime: 1637393112000,
12.     },
13.     currentPercentage: 50,
14.   },
15.   intentEntityInfo: {
16.     entityName: "Music",
17.     entityId: "C10194368",
18.     entityGroupId: "C10194321312",
19.     displayName: "测试歌曲1",
20.     description: "NA",
21.     logoURL: "https://www-file.abc.com/-/media/corporate/images/home/logo/abc_logo.png",
22.     keywords: ["华为音乐", "化妆"],
23.     rankingHint: 99,
24.     expirationTime: 1637393212000,
25.     metadataModificationTime: 1637393212000,
26.     activityType: ["1", "2", "3"],
27.     artist: ["测试歌手1", "测试歌手2"],
28.     lyricist: ["测试词作者1", "测试词作者2"],
29.     composer: ["测试曲作者1", "测试曲作者2"],
30.     albumName: "测试专辑",
31.     duration: 244000,
32.     playCount: 100000,
33.     musicalGenre: ["流行", "华语", "金曲", "00后"],
34.     isPublicData: false,
35.   }
36. }
37. // 共享数据接口  意图数组可以是更多的实体
38. insightIntent.shareIntent(this.context, [playMusicIntent]).then(() => {
39.   console.info('shareIntent succeed');
40. }).catch((err: BusinessError) => {
41.   console.error(`error.code: ${err?.code}, failed because ${err?.message}`);
42. });

## 端侧意图调用

开发者需要自己实现InsightIntentExecutor，并在对应回调实现打开落地页（点击推荐卡片跳转的界面）或后台执行的能力，PlayMusic的意图调用字段定义见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。

步骤如下：

1. 继承InsightIntentExecutor。
2. 重写对应方法，例如目标拉起前台页面，则可重写onExecuteInUIAbilityForegroundMode方法。
3. 通过意图名称，识别播放歌曲意图（PlayMusic），在对应的方法中传递意图参数（param），并拉起对应落地页（如播放歌曲落地页）或后台执行（播放歌曲）。

4. import { insightIntent, InsightIntentExecutor } from '@kit.AbilityKit';
5. import { window } from '@kit.ArkUI';
6. import { BusinessError } from '@kit.BasicServicesKit';
7. /**
8.  * 意图调用样例
9. */
10. export default class InsightIntentExecutorImpl extends InsightIntentExecutor {
11.   private static readonly PLAY_MUSIC = 'PlayMusic';
12.   /**
13.    * override 执行前台UIAbility意图
14.    *
15.    * @param name 意图名称
16.    * @param param 意图参数
17.    * @param pageLoader 窗口
18.    * @returns 意图调用结果
19.    */
20.   onExecuteInUIAbilityForegroundMode(name: string, param: Record<string, Object>, pageLoader: window.WindowStage):
21.     Promise<insightIntent.ExecuteResult> {
22.     // 根据意图名称分发处理逻辑。接入方可根据实际业务实现页面跳转
23.     switch (name) {
24.       case InsightIntentExecutorImpl.PLAY_MUSIC:
25.         return this.playMusic(param, pageLoader);
26.       default:
27.         break;
28.     }
29.     return Promise.resolve({
30.       code: -1,
31.       result: {
32.         message: 'unknown intent'
33.       }
34.     } as insightIntent.ExecuteResult)
35.   }
36.   /**
37.    * 实现调用播放歌曲功能
38.    *
39.    * @param param 意图参数
40.    * @param pageLoader 窗口
41.    */
42.   private playMusic(param: Record<string, Object>, pageLoader: window.WindowStage): Promise<insightIntent.ExecuteResult> {
43.     return new Promise((resolve, reject) => {
44.       // TODO 实现意图调用，loadContent的入参为歌曲落地页路径，例如：pages/SongPage
45.       pageLoader.loadContent('pages/SongPage')
46.         .then(() => {
47.           let entityId: string = (param.items as Array<object>)?.[0]?.['entityId'];
48.           // TODO 调用成功的情况，此处可以打印日志
49.           resolve({
50.             code: 0,
51.             result: {
52.               message: 'Intent execute succeed'
53.             }
54.           });
55.         })
56.         .catch((err: BusinessError) => {
57.           // TODO 调用失败的情况
58.           resolve({
59.             code: -1,
60.             result: {
61.               message: 'Intent execute failed'
62.             }
63.           })
64.         });
65.     })
66.   }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-function-search "功能搜索方案")
# 内容搜索方案

更新时间: 2025-12-16 16:28

## 方案概述

当用户使用应用/元服务时，开发者可以按照标准意图Schema（具体意图详见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)）向系统共享数据（数据包含用户行为和内容实体），并实现意图调用（空调用与传参调用）。已实现用户点击卡片后，可后台执行功能（例如播放指定歌曲）或跳转至指定内容页面（例如指定的歌曲播放页面）。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162809.20110941362461148417525428937996:50001231000000:2800:FCF1E0C5841AD2C221DCC5DDD5D5DA8AAC807A3E3003A82AB81F1D1F48C82A64.png "点击放大")

## 意图声明

以歌曲本地搜索特性为例，首先要注册播放歌曲意图（PlayMusic），其他意图见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。

开发者需要编辑对应的意图配置insight_intent.json文件实现意图注册。insight_intent.json文件需要放置在module下面的指定目录：src/main/resources/base/profile/insight_intent.json，并且整个工程中只能存在一个insight_intent.json文件。

1. {
2.   // 应用支持的意图列表
3.   // 必须声明应用支持插件包含的必选意图，应用上架时会进行校验
4.   "insightIntents": [
5.     {
6.       // 意图名称
7.       // 名称应当遵循意图框架规范，当前仅支持预置垂域意图，不允许自定义
8.       // 应用内意图名称唯一，不允许出现相同的名称定义
9.       "intentName": "PlayMusic",
10.       // 意图所属的垂域
11.       "domain": "MusicDomain",
12.       // 意图版本号
13.       // 插件引用意图时会校验该版本号，只有和插件定义的版本号一致才能正常调用
14.       "intentVersion": "1.0.1",
15.       // 意图调用逻辑入口
16.       "srcEntry": "./ets/entryability/InsightIntentExecutorImpl.ets",
17.       "uiAbility": {
18.         // 意图所在ability        
19.       "ability": "EntryAbility",
20.         // UIAbility支持前后台两种执行模式
21.         "executeMode": [
22.           "background",
23.           "foreground"
24.         ]
25.       }
26.     }
27.   ]
28. }

## 意图共享

构建意图对象，并且调用[shareIntent()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/intents-arkts-api-insightintent#section161911659112211)，实现意图共享。可同时构建多个PlayMusic或PlayMusicList的意图对象。

以歌曲本地搜索特性为例，首先要注册播放歌曲意图（PlayMusic），其他意图见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。开发者需要编辑对应的意图配置insight_intent.json文件实现意图注册。insight_intent.json文件需要放置在module下面的指定目录：src/main/resources/base/profile/insight_intent.json，并且整个工程中只能存在一个insight_intent.json文件。

1. import { insightIntent } from '@kit.IntentsKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. let playMusicIntent1: insightIntent.InsightIntent;
4. let playMusicIntent2: insightIntent.InsightIntent;
5. // 共享数据接口  意图数组可以是更多的实体
6. insightIntent.shareIntent(this.context, [playMusicIntent1, playMusicIntent2]).then(() => {
7.   console.info('shareIntent succeed');
8. }).catch((err: BusinessError) => {
9.   console.error(`error.code: ${err?.code}, failed because ${err?.message}`);
10. });

PlayMusic的意图共享字段定义见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)定义，代码示例如下：

1. import { insightIntent } from '@kit.IntentsKit';
2. let playMusicIntent: insightIntent.InsightIntent = {
3.   intentName: "PlayMusic",
4.   intentVersion: "1.0.1",
5.   identifier: "52dac3b0-6520-4974-81e5-25f0879449b5",
6.   intentActionInfo: {
7.     actionMode: "EXECUTED",
8.     executedTimeSlots: {
9.       executedStartTime: 1637393212000,
10.       executedEndTime: 1637393112000,
11.     },
12.     currentPercentage: 50,
13.   },
14.   intentEntityInfo: {
15.     entityName: "Music",
16.     entityId: "C10194368",
17.     entityGroupId: "C10194321312",
18.     displayName: "测试歌曲1",
19.     description: "NA",
20.     logoURL: "https://www-file.abc.com/-/media/corporate/images/home/logo/abc_logo.png",
21.     keywords: ["华为音乐", "化妆"],
22.     rankingHint: 99,
23.     expirationTime: 1637393212000,
24.     metadataModificationTime: 1637393212000,
25.     activityType: ["1", "2", "3"],
26.     artist: ["测试歌手1", "测试歌手2"],
27.     lyricist: ["测试词作者1", "测试词作者2"],
28.     composer: ["测试曲作者1", "测试曲作者2"],
29.     albumName: "测试专辑",
30.     duration: 244000,
31.     playCount: 100000,
32.     musicalGenre: ["流行", "华语", "金曲", "00后"],
33.     isPublicData: false,
34.   }
35. }

完整的意图共享示例如下所示，该示例构建了一个PlayMusic意图、一个PlayMusicList意图，并进行了shareIntent调用。

1. import { insightIntent } from '@kit.IntentsKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. let playMusicIntent: insightIntent.InsightIntent = {
4.   intentName: "PlayMusic",
5.   intentVersion: "1.0.1",
6.   identifier: "52dac3b0-6520-4974-81e5-25f0879449b5",
7.   intentActionInfo: {
8.     actionMode: "EXECUTED",
9.     executedTimeSlots: {
10.       executedStartTime: 1637393212000,
11.       executedEndTime: 1637393112000,
12.     },
13.     currentPercentage: 50,
14.   },
15.   intentEntityInfo: {
16.     entityName: "Music",
17.     entityId: "C10194368",
18.     entityGroupId: "C10194321312",
19.     displayName: "测试歌曲1",
20.     description: "NA",
21.     logoURL: "https://www-file.abc.com/-/media/corporate/images/home/logo/abc_logo.png",
22.     keywords: ["华为音乐", "化妆"],
23.     rankingHint: 99,
24.     expirationTime: 1637393212000,
25.     metadataModificationTime: 1637393212000,
26.     activityType: ["1", "2", "3"],
27.     artist: ["测试歌手1", "测试歌手2"],
28.     lyricist: ["测试词作者1", "测试词作者2"],
29.     composer: ["测试曲作者1", "测试曲作者2"],
30.     albumName: "测试专辑",
31.     duration: 244000,
32.     playCount: 100000,
33.     musicalGenre: ["流行", "华语", "金曲", "00后"],
34.     isPublicData: false,
35.   }
36. }
37. // 共享数据接口  意图数组可以是更多的实体
38. insightIntent.shareIntent(this.context, [playMusicIntent]).then(() => {
39.   console.info('shareIntent succeed');
40. }).catch((err: BusinessError) => {
41.   console.error(`error.code: ${err?.code}, failed because ${err?.message}`);
42. });

## 端侧意图调用

开发者需要自己实现InsightIntentExecutor，并在对应回调实现打开落地页（点击推荐卡片跳转的界面）或后台执行的能力，PlayMusic的意图调用字段定义见[各垂域意图Schema](https://developer.huawei.com/consumer/cn/doc/service/intents-schema-0000001901962713)。

步骤如下：

1. 继承InsightIntentExecutor。
2. 重写对应方法，例如目标拉起前台页面，则可重写onExecuteInUIAbilityForegroundMode方法。
3. 通过意图名称，识别播放歌曲意图（PlayMusic），在对应的方法中传递意图参数（param），并拉起对应落地页（如播放歌曲落地页）或后台执行（播放歌曲）。

4. import { insightIntent, InsightIntentExecutor } from '@kit.AbilityKit';
5. import { window } from '@kit.ArkUI';
6. import { BusinessError } from '@kit.BasicServicesKit';
7. /**
8.  * 意图调用样例
9. */
10. export default class InsightIntentExecutorImpl extends InsightIntentExecutor {
11.   private static readonly PLAY_MUSIC = 'PlayMusic';
12.   /**
13.    * override 执行前台UIAbility意图
14.    *
15.    * @param name 意图名称
16.    * @param param 意图参数
17.    * @param pageLoader 窗口
18.    * @returns 意图调用结果
19.    */
20.   onExecuteInUIAbilityForegroundMode(name: string, param: Record<string, Object>, pageLoader: window.WindowStage):
21.     Promise<insightIntent.ExecuteResult> {
22.     // 根据意图名称分发处理逻辑。接入方可根据实际业务实现页面跳转
23.     switch (name) {
24.       case InsightIntentExecutorImpl.PLAY_MUSIC:
25.         return this.playMusic(param, pageLoader);
26.       default:
27.         break;
28.     }
29.     return Promise.resolve({
30.       code: -1,
31.       result: {
32.         message: 'unknown intent'
33.       }
34.     } as insightIntent.ExecuteResult)
35.   }
36.   /**
37.    * 实现调用播放歌曲功能
38.    *
39.    * @param param 意图参数
40.    * @param pageLoader 窗口
41.    */
42.   private playMusic(param: Record<string, Object>, pageLoader: window.WindowStage): Promise<insightIntent.ExecuteResult> {
43.     return new Promise((resolve, reject) => {
44.       // TODO 实现意图调用，loadContent的入参为歌曲落地页路径，例如：pages/SongPage
45.       pageLoader.loadContent('pages/SongPage')
46.         .then(() => {
47.           let entityId: string = (param.items as Array<object>)?.[0]?.['entityId'];
48.           // TODO 调用成功的情况，此处可以打印日志
49.           resolve({
50.             code: 0,
51.             result: {
52.               message: 'Intent execute succeed'
53.             }
54.           });
55.         })
56.         .catch((err: BusinessError) => {
57.           // TODO 调用失败的情况
58.           resolve({
59.             code: -1,
60.             result: {
61.               message: 'Intent execute failed'
62.             }
63.           })
64.         });
65.     })
66.   }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-function-search "功能搜索方案")
# 意图标准协议上架指导

更新时间: 2025-12-16 16:27

该配置需开发者完成自测后，先将携有对应意图信息的App在AppGallery Connect（以下简称AGC）完成应用上架，具体操作步骤参见[应用开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview)。

## **意图注册配置操作步骤**

1. 账号登录：
    
    1. 通过“[华为开发者联盟](https://developer.huawei.com/consumer/cn/) > 管理中心 > 生态服务 > 智慧服务 > 小艺开放平台（原HarmonyOS服务开放平台） > 意图框架”，进入意图注册入口，需使用与应用上架相同的账号登录。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162751.26920677935032918781775443076106:50001231000000:2800:AA0D020F78706DDEF75965EFDE256A7F47FD0A2FFE4E8E8F6016AB98A13F311D.png "点击放大")
        
    2. 点击“立即体验”即可进入意图注册入口。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162751.66716203991307236427195735152594:50001231000000:2800:AF9B81DA852AA5940F09504B7FDFF16EAE921FD4C13D5BE8C611D89372441944.png "点击放大")
    
2. 选择意图集：在“小艺开放平台”首页“意图集（插件）”中，携有意图声明文件的应用在AGC**正式上架**后可**自动****生成**一条草稿态的记录，记录中包含开发者在意图配置文件中声明的所有**端侧意图**（云侧意图需手动新增，见下图）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162751.59314470715960903058310592491828:50001231000000:2800:E9357525277BBFD137F7BF559E4EB899A863956B6ECDCF87CEFA8076653C18B5.png "点击放大")
    
3. 基本信息编辑：点击对应的意图集记录的“编辑”按钮，进入基本信息编辑页面，开发者补充完基本信息后点击“保存”即可。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162751.26969132674836423890312944752345:50001231000000:2800:1377BF6A3C6A6E53D35A3C671FBC5A048EAFAB9E57A6AD4B6DF4F96996CB2ED7.png "点击放大")
    
    此处的版本号和版本描述为智慧分发配置的版本信息，用于开发者记录和识别智慧分发配置版本变更，与APP软件包版本无关，意图注册名称与APP名称保持一致。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162751.06084687700500607076234213560036:50001231000000:2800:FDC13932EC838DC28B455E16EAD1F44D344828ABD948ABA7ED252D583FDBEC47.png "点击放大")
    
4. 意图检查：切换至“意图”页签，点击“保存”会触发刷新，需检查接入特性所依赖的全量意图是否在此页面都已列出，同时打开意图使用样本中“是否已提供线下样本“开关。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162751.35805887998111932665990713864932:50001231000000:2800:38705139A2CDFF1C7122C4BE4DF225D814F27B0F942D658393C8B1AA777E7F8B.png "点击放大")
    
    1. 其中，“端云类型”涉及端的意图需在APP软件包中定义，此处会自动呈现。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162751.26954727186082036754998289986193:50001231000000:2800:6AF3AA0C85D3BF8A25D145AFDE980AA0B2579E2D886F7798DC01F2B40C4DDF53.png "点击放大")
        
    2. “端云类型”仅涉及云的意图需要需手动添加该意图。可参照如下步骤配置：
        1. 点击添加进行意图新增。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162751.12015735884673059464585022216078:50001231000000:2800:7B36BBDD1EE0D1A51A93DB06F937D35BFEDF683B29F0C403B2E62DFAFB1B87CA.png "点击放大")
            
        2. 选择云侧意图分类，搜索意图名称，勾选所需意图进行添加（若没有找到对应意图可联系华为工程师，检查是否未配置该意图）。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162751.76726063379042154281810805868519:50001231000000:2800:A40248D46AB93F6A323A1B3ACE250B2E4C5527F86724E279EA7A706EF796D286.png "点击放大")
            
        3. 添加完成后，需录入接口信息配置，具体信息如下：
            
            1. API：即开发者的URL地址信息，供华为侧服务器进行云侧意图调用。
            2. 认证方式：如果涉及接口鉴权，则选择认证方式（例如AK/SK认证）并配置密钥信息；如果不涉及则选择不认证。
            3. 个人数据授权：该信息是指华为侧服务器携带对应信息访问开发者服务器，当有个性化推荐诉求时需要填写，默认不填写；比如选中“用户授权的用户唯一标识”（即SID），则华为侧服务器访问开发者服务器时会携带SID，开发者服务器则可以识别用户返回个性化的数据用户推荐展示。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162751.89851417054310641447070581289312:50001231000000:2800:46809A8179663D10B49CB654F7A4BA8D443A6AE45823BDD404D12907C395E9D8.png "点击放大")
            
    3. 如仍未全部列出，检查软件包中意图注册配置文件是否漏配，若漏配则在意图配置文件中补充配置，并重新在AGC进行应用上架/升级，完成后在小艺开放平台进行意图注册。
    4. 如果提示声明意图不存在，则说明华为意图框架后台未配置该意图。开发者可以继续点击保存走完本次流程，但相应意图和关联特性不会生效；可联系华为工程师，检查是否未配置该意图。
    
5. 检查完成：如果特性依赖的所有意图都已列出，检查意图名称、意图调用配置和意图共享配置等是否正确，正确则点击“保存”，进入下一步。
6. 发布选择“发布”页签，进入配置检查页面。
    
    1. 点击“开始检查”，检查接入特性和其关联的意图是否正确，如下图所示。生成特性时会同时生成abilityId，若开发者接入特性的方案涉及此参数，则事件推荐请求字段abilityId参数需要填写当前界面的abilityId值。若提示特性undefined，则联系华为工程师，检查是否未配置该特性。
    2. 配置检查完成后点击“提交审核”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162752.32953648102302872517297065962787:50001231000000:2800:75016C44BFAB07B87088A4CA74619C2DA83A6A620DB7E045FAF4BFB23466FE8F.png "点击放大")
    
7. 审核：提交审核后，在“小艺开放平台> 意图集中”，该条记录状态变为“上架审核中”，一般审核周期为3-5个工作日，审核通过后状态变为“已上架”，至此意图注册及特性选择已完成。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162752.51223771571302259578903043488972:50001231000000:2800:E69FCDDABAAECB1253DB2C120BC559D3AC50D30821D14CD98BC12B727C587377.png "点击放大")
    
8. 新增意图：若开发者有新意图上架，可在同一条记录上进行编辑后提交，操作流程同上述步骤，未提交审核不影响已经注册的意图。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-kit-listing-configuration "意图框架上架配置指导")
# MCP协议上架指导

更新时间: 2025-12-16 16:27

## **意图注册配置操作步骤**

1. 账号登录：
    
    1. 通过“[华为开发者联盟](https://developer.huawei.com/consumer/cn/) > 管理中心 > 生态服务 > 智慧服务 > 小艺开放平台（原HarmonyOS服务开放平台） > 意图框架”，进入意图注册入口。
        
        如发布渠道为“智能体/小艺对话”只能使用与应用上架相同的账号登录。反之发布渠道为“插件市场”无特殊账号要求。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162755.40493639949244799620709132070627:50001231000000:2800:97FF81CD3B0F29A39F61E0C861A783BE6FC8D6F992042E22CE629ABC63F8E5FE.png "点击放大")
        
    2. 点击“立即体验”即可进入意图注册入口。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162755.23276352208373265720177646197961:50001231000000:2800:D6671AB4CC56309CEB0D06FF329C9252FEB7AC95A04D4A6A53F1D3F0C7F1DECB.png "点击放大")
    
2. 注册意图集
    1. 如图，点击“注册意图”。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162755.29430614268873135298900168543117:50001231000000:2800:557E213D6D368E4E31B1C93D2592A9F613C64EE648C6C8FCEB50A263E3EA0BF6.png "点击放大")
        
    2. 选择“MCP协议”并填写基本信息创建意图集。
        
        1. 意图集（插件）名称：需唯一标识。
        2. 意图集（插件）描述：开发者自定义插件描述信息。
        3. 分类：按业务场景选择。
        4. MCP服务配置：填写MCP URL（服务器地址信息，不含鉴权信息）。
        5. 认证信息配置：对应鉴权信息（注意放在Header/Query）。
        6. 协议类型：根据情况选择，提供SSE/Streamable两种。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162756.44734700150548481557040991485166:50001231000000:2800:1528EFF873BA692306B380C57110CCE65E60F6B8F349C870E71E02A2E104521B.png "点击放大")
        
3. 编辑：创建后自动进入”插件编辑“页面。
    1. 编辑基本信息：
        
        1. 开发者品牌：该信息是对外露出的品牌传播名（注意和企业账号，公司名称区别开）。
        2. 图标：192*192。
        3. 使用描述：需使用Markdown格式。（需对server的功能概述、apikey申请方式表达准确清晰）。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162756.27844223421742434643681122648715:50001231000000:2800:0792A8961EF9D41CF7874789A532632A8BE59CDF8322CB199C283FDE7E851426.png "点击放大")
        
4. 工具检查：保存后切换至"工具"页签。若基本信息配置无误，工具列表中会根据基本信息内容自动生成1条/多条信息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162756.82781946031915867336832643842833:50001231000000:2800:9AF6994507F578BE7F34DBA006DB5917FB1D433FF37D5EBE5B54553D24436F3A.png "点击放大")
    
    1. 出现工具列表：请检查工具入参，参数是否重复或者缺失，参数类型是否正确。若一切无误，则配置成功。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162756.21748498210274096443589036638516:50001231000000:2800:EAE39B3485ECFE5509EA551CEA2A399BDC135D2DDF8B58608F300124D5D8024E.png "点击放大")
        
    2. 未出现工具列表：请等候几分钟重新进入，后台加载存在延时；如若重新进入后，仍未加载出工具信息，可能是插件的链接和鉴权信息配置错误。多次尝试后仍未解决，请通过邮箱联系华为意图框架同学（hagservice@huawei.com） 。
    
5. 审核：切换至“发布”页签，点击“提交审核”。
    1. 选择发布渠道，点击确定，提交审核。
        
        1. 智能体：开发者上架MCP Server，仅供开发者自己开发的智能体来调用。
        2. 小艺对话：开发者上架MCP Server，可供开发者自己开发的智能体调用，也可供小艺APP主对话调用（当前暂不支持开发者独立在小艺主对话上线该能力，需联系华为意图框架同学）。
        3. 插件市场：开发者上架MCP server，可供开发者自己开发的智能体调用，也可供平台上其他开发者开发智能体时调用（回到开发者源头平台去开服）。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162756.69921729342352869293527960020356:50001231000000:2800:425A6F37BE100666F53E799BCFD195BD5614E4CA68A127C8E5358FDDA0898A04.png "点击放大")
        
    2. 提交审核后，请耐心等待平台相关审核流程完成；完成后即可在“[华为开发者联盟](https://developer.huawei.com/consumer/cn/) > 管理中心 > 生态服务 > 智慧服务 > 小艺开放平台（原HarmonyOS服务开放平台） > 意图框架 > 小艺插件市场”中找到您的工具。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-kit-listing-standard-protocol "意图标准协议上架指导")# 使用意图框架调试助手Agent进行联调时，小艺拉起应用后，出现闪退情况，应该如何处理？

更新时间: 2025-12-16 16:27

出现此现象时，优先排查接入意图框架的代码是否被混淆。接入意图框架的代码文件不可被混淆。关于混淆的详细内容请参考[应用代码混淆](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-app-code-ob#section13780943192313)。若排查后问题依然存在，请检查应用的业务代码是否有其他异常引发应用闪退。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-frequently-asked-questions-two "inputParams报错Value should be one of: \"intentName\", \"domain\", \"intentVersion\", \"srcEntry\", \"uiAbility\", \"serviceExtension\", \"uiExtension\", \"form\"如何解决？")
# 附录A：获取华为账号对应UID的方式

更新时间: 2025-12-16 16:27

1. 使用需要添加白名单的华为账号登录“[华为开发者联盟](https://developer.huawei.com/consumer/cn/)”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162750.97084445062115118559009225192643:50001231000000:2800:66B1E64646383F1C5CA9A58D500CD963BC2F9D0116CE0E9D69701F4674A6BCC9.png "点击放大")
    
2. 点击右上角我的-头像进入详情页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162750.94744225527123492941945992781192:50001231000000:2800:55535A700F24DE4158F2E3553D9F16458A6CA248048226ABE2C4787DEC4EFC43.png "点击放大")
    
3. 如图开发者ID即为对应账号UID。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162750.37299986036254103099223108268319:50001231000000:2800:53CC9A848C104886D60318EACDD98149EC5D9071749A45191C3F285416A843B9.png "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/four "功能一步达场景是否有云侧动态声明词条的方案？")
# 附录A：获取华为账号对应UID的方式

更新时间: 2025-12-16 16:27

1. 使用需要添加白名单的华为账号登录“[华为开发者联盟](https://developer.huawei.com/consumer/cn/)”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162750.97084445062115118559009225192643:50001231000000:2800:66B1E64646383F1C5CA9A58D500CD963BC2F9D0116CE0E9D69701F4674A6BCC9.png "点击放大")
    
2. 点击右上角我的-头像进入详情页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162750.94744225527123492941945992781192:50001231000000:2800:55535A700F24DE4158F2E3553D9F16458A6CA248048226ABE2C4787DEC4EFC43.png "点击放大")
    
3. 如图开发者ID即为对应账号UID。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162750.37299986036254103099223108268319:50001231000000:2800:53CC9A848C104886D60318EACDD98149EC5D9071749A45191C3F285416A843B9.png "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/four "功能一步达场景是否有云侧动态声明词条的方案？")