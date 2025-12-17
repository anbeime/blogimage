# Push Kit简介

更新时间: 2025-12-16 16:35

Push Kit（推送服务）是华为提供的消息推送平台，建立了从云端到终端的消息推送通道。所有HarmonyOS应用可通过集成Push Kit，实现向应用实时推送消息，使消息易见，构筑良好的用户关系，提升用户的感知度和活跃度。

## 快速入门

请参考[使用入门](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-gettingstart)章节快速了解接入Push Kit（推送服务）的必要步骤。

## 产品优势

- **稳定的消息发送通道**
    
    Push Kit通过提供系统级长链接，即使应用进程不在也能实时推送消息。
    
- **丰富的消息呈现样式**
    
    支持文本样式、通知大图标样式、多行文本样式、角标样式等多种消息展示方式，满足您多样化、个性化的消息发送需求。
    
- **灵活的场景化消息**
    
    开发者可以根据实际场景灵活接入场景化消息。如通过应用内通话消息实现音视频通话，通过通知扩展消息实现语音播报业务处理，通过后台消息实现配置更新等。
    

## 推送消息提示场景

推送消息指的是应用**通过Push Kit发送的**，在华为终端设备上显示的通知消息。显示场景主要包括通知中心、锁屏、横幅、桌面图标角标与通知图标。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163559.92603487524125937774188805481326:50001231000000:2800:670D49BE4CF09D1D9BD39F08F212B08C5C65EFE5FD9193B9CB760AF91D7C0E95.jpg "点击放大")

有关各场景的详细说明请参见[通知提示场景](https://developer.huawei.com/consumer/cn/doc/design-guides/system-features-notification-0000001793074217#section162699204401)。

## 推送消息类型

Push Kit支持以下消息类型：

|消息类型|说明|
|:--|:--|
|[通知消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-alert)|通知消息由Push Kit直接下发，在终端设备的通知中心、锁屏、横幅等展示，用户点击后拉起应用。<br><br>您可以[设置通知消息样式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section5164103925811)来吸引用户。<br><br>常见场景：行程提醒、账号动态等。|
|[通知扩展消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-extend-noti)|当用户终端收到您发送的通知扩展消息后，Push Kit会拉起应用的子进程，您可以在子进程中自行处理业务。<br><br>常见场景：语音播报。|
|[卡片刷新消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-form-update)|通过卡片刷新服务，在合适场景向用户即时推送卡片内容，提升用户的感知度和活跃度。<br><br>常见场景：打车出行、快递动态等。|
|[后台消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-background)|终端设备接收到后台消息后，如果应用进程在前台则将消息内容传给应用；如果应用进程不在前台则缓存消息，等待应用启动后再传给应用。<br><br>常见场景：用于告知应用更新配置参数。|
|[实况窗消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-update-liveview)|应用服务端向Push Kit服务端发送创建或更新实况窗的请求，创建实况窗，或更新实况窗内容。<br><br>常见场景：赛事比分更新，出行打车状态更新等。|
|[应用内通话消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-voip)|支持应用实现网络音视频通话的能力。<br><br>常见场景：网络音视频通话。|

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163559.49130263933432542984718162336201:50001231000000:2800:8C6CC92CB53D55608C7E2D5FEFAC67234232AA065CDCB69A87B7E05AE7E14362.png "点击放大")

使用Push Kit的主要业务流程如下：

1. 应用调用Push Kit，获取Push Token。
2. 应用成功获取Token后，建议及时上报Token等信息至应用服务端。
3. 应用服务端向华为Push Kit服务端（Push Cloud）发送推送消息请求。应用的通知开关默认关闭，发送请求前，请先请求通知授权，详情请参见[请求通知授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-enable)。
4. Push Kit服务端下发消息到Push Kit。
5. Push Kit进行消息处理。

## 约束和限制

### 影响送达率的因素说明

Push Kit致力于提供安全可靠的系统级消息发送通道，保障消息成功送达。影响消息送达率的因素如下：

- 终端设备是否在线。如果设备离线，Push Kit会缓存消息，待设备上线后，再将消息推送给设备。
- 终端设备上应用是否被卸载。
- 终端设备的网络状况是否稳定。
- 终端设备的安全控制策略。

### 推送消息的及时性

在终端设备网络条件良好且不拥堵情况下，Push Kit将使用智能推送策略以减少推送消息的时延。

说明

为降低对用户的打扰，系统会学习用户的行为习惯，预测用户的睡眠时间，在用户睡眠期间实施消息管控。在此期间推送服务将暂时缓存该时间段内收到的消息（应用内通话或category=VoIP的消息除外）。用户结束睡眠后，推送服务会将消息重新投递到对应设备。

### 推送消息长度与数量限制

- 消息体最大不能超过4096Bytes（不包括Token）。
- 消息发送量，测试消息（参考消息体pushOptions.[testMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)）每个项目限制所有应用共享1000条/天，正式消息区分场景有不同的配额，参考[消息频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control)说明。

### 网络受限说明

如果终端设备连接的网络配置了防火墙或处于受限的网络下，将会影响消息的送达率，请检查以下端口号是否被禁用。

端口号：

- 5223
- 443

说明

终端设备连接的推送服务器的IP是动态分配的，无法通过配置IP白名单方式放行。建议连接不受限的网络或放通以上端口。

### 支持的国家/地区

Push Kit当前[支持的设备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-kit-introduction#section193391236104017)中Wearable设备支持的国家请参见[支持的国家/地区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-country)，其他设备仅支持中国境内（不包含中国香港、中国澳门、中国台湾）。

### 支持的设备

推送服务能力支持Phone、Tablet、PC/2in1、Wearable、TV设备。

### 模拟器版本和云真机说明

Push Kit支持模拟器开发，但与真机存在部分能力差异，详情请参见“[模拟器与真机的差异](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-specification#section38231424133213)”。Push Kit不支持云真机调试。

## 与相关Kit的关系

- Push Kit建立了从云端到终端的消息推送通道，支持开发者从云侧实时推送消息。如果开发者希望从本地推送通知，可通过[Notification Kit（用户通知服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-overview)创建本地通知。
- 开发者[推送卡片刷新消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-form-update)时，需要通过[Form Kit（卡片开发服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/formkit-overview)提前创建应用的服务卡片。
- 开发者[推送实况窗更新消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-update-liveview)时，需要通过[Live View Kit（实况窗服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/liveview-introduction)提前创建本地实况窗。
- 开发者[推送应用内通话消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-voip)时，通过[Call Service Kit（通话服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/call-introduction)管理应用通话能力。

## 示例代码

Push Kit（推送服务）示例代码，请参考[示例代码](https://gitcode.com/harmonyos_samples/push-kit-sample-code-clientdemo-arkts)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-kit-guide "Push Kit（推送服务）")
# 使用入门

更新时间: 2025-12-16 16:36

## 示例代码

开发者可以参考**服务端**[示例代码](https://gitcode.com/harmonyos_samples/push-kit_-sample-code_-server-demo_-java)，了解推送Push场景化消息的过程。参考**客户端**[示例代码](https://gitcode.com/harmonyos_samples/push-kit-sample-code-clientdemo-arkts)，了解生成Push Token和接收Push场景化消息的功能和流程。

## 开发流程

开发者需要按照流程来完成应用的开发工作，**以[推送通知消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert)为例**，完整的开发流程如下：

|序号|步骤|说明|
|:--|:--|:--|
|1|[开通推送服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-config-setting)|在开发应用前，请先参考[操作步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-config-setting#section13206419341)开通推送服务。其中**配置签名信息**时，请使用**手动签名**方式。<br><br>DevEco Studio 6.0.0 Beta5版本开始新增[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)方式。|
|2|[申请通知消息自分类权益](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section16708911111611)|- 请根据[通知消息分类标准](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1924971516101)，申请对应场景化消息权益。不同类型的消息有对应的通知消息分类标准与提醒方式和[通知消息推送数量管理规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1128516504398)。如果您在申请过程中遇到任何问题，请发送邮件至[hwpush@huawei.com](mailto:hwpush@huawei.com)与我们取得联系。<br>- 若未开通权益，或开通的权益类型与[调用REST API推送场景化消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-scenes-send)时，请求体中携带的[category](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)字段值不一致，消息将会默认归为**资讯营销类消息**，则会受到“单个应用每日每设备推送数量为2条或5条”的[频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1128516504398)限制。若超出限制，设备将会收不到该条消息。<br>- 调测阶段建议设置[testMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)为true，以防发送成功的消息被[频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control)，设备将会收不到该条消息。<br>- 若消息被频控，请参考[频控FAQ](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-5)进行问题排查。|
|3|**客户端**获取Push Token|[调用推送服务REST API](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token#section33041381718)时，需要设置token参数，对应的参数值参考[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token#section85173618105)进行获取。注意[Push Token变化的场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token#section123091617105820)，若设备的Push Token发生变化但服务端调用推送服务REST API时未更新token的值，将会导致设备收不到该条消息。|
|4|**客户端**请求通知授权|为确保应用可正常收到消息，应用发送通知前需调用[requestEnableNotification](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-notificationmanager#notificationmanagerrequestenablenotification10-1)()方法弹出提醒，告知用户需要允许接收通知消息。示例代码参见[开发步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section17790171616598)中第2步。|
|5|**客户端**配置skills标签|为确保点击消息可以正常跳转应用页面，在应用项目中完成skills标签配置，详情请参见[点击消息动作](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section697519219136)。|
|6|**服务端**基于服务账号生成鉴权令牌|[调用推送服务REST API](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token#section33041381718)推送场景化消息时，请求头需设置Authorization参数，请参考[基于服务账号生成鉴权令牌](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token)章节进行获取。|
|7|**服务端**[调用REST API推送场景化消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-scenes-send)|应用服务端参考HarmonyOS NEXT版本[请求体结构说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct)、[请求体参数说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param)发送REST API请求。若请求失败请参考[响应参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-response)进行问题排查，若请求成功但设备未收到消息请参考[FAQ](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-2)进行问题排查。|
|8|（可选）开发消息回执|Push服务端会将消息送达状态以回执消息形式发送给您的应用回执服务端，方便您获取消息下达端侧后的状态，定位问题。详情请参考[开发消息回执](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-msg-receipt)。|
|9|（可选）**客户端**收到并处理消息|通过服务端请求传参和客户端的数据获取，可以进行服务端和客户端的[数据传递](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section108252081117)。|

## （可选）其他消息类型

Push Kit支持的所有消息类型及使用场景可以参考[推送消息类型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-kit-introduction#section121512516176)。

如通过应用内通话消息实现音视频通话，通过通知扩展消息实现语音播报（Push Kit会将通知消息内容传递给通知扩展进程，您可在该进程中自行完成语音播报业务处理），通过后台消息实现配置更新等。

- 部分场景化消息类型需要您申请特殊权益才能正常发送，详情请参考[场景化消息权益简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1937015602710)。
- 权益申请通过后，请参考对应消息类型的开发指南章节进行开发。

注意

如果您的项目之前已经基于HarmonyOS 3.x/4.x的系统接入过推送服务，现在需要给HarmonyOS Next/5.x及之后的系统版本推送通知，客户端和服务端仍然需要按照上述开发流程重新进行开发。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-kit-introduction "Push Kit简介")
# 学习Push Kit接入规范

更新时间: 2025-12-16 16:36

为维护华为通知生态秩序，保障用户合法权益和良好的使用体验，根据现行法律法规及[《华为开发者服务协议》](https://developer.huawei.com/consumer/cn/doc/start/agreement-0000001052728169)、[《华为APIs使用协议》](https://developer.huawei.com/consumer/cn/doc/20209)、[《华为推送服务使用协议》](https://developer.huawei.com/consumer/cn/doc/app/20213)、[《应用审核指南》](https://developer.huawei.com/consumer/cn/doc/app/50104)、[《元服务审核指南》](https://developer.huawei.com/consumer/cn/doc/app/50129)，特制定本规范。

所有发布上架到华为应用市场且使用推送通知行为的HarmonyOS应用、联运应用及元服务（以下简称应用）应当遵守本规范，若开发者的行为违反本规范或[《华为应用市场联运服务协议》](https://developer.huawei.com/consumer/cn/doc/app/20204)，华为有权根据本规范和[《华为应用市场联运违规处罚规定》](https://developer.huawei.com/consumer/cn/doc/app/20204#h1-1717147806751-10)对开发者进行处罚。

## Push Kit使用基本原则

- HarmonyOS应用的推送消息，需通过华为官方的消息推送平台下发。
- 遵守[通知样式规范](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-specification#section178791211154912)，禁止采用规范外样式，以保证通知体验的一致性。
- 通知开关需由用户授权允许，应用首次启动时需弹窗询问用户是否允许通知。
- 不可出于商业目的强制改变通知属性（如采用进行中通知强制置顶显示），避免损害用户使用体验。
- 遵守[通知内容管理细则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-detail-rules)。

## 通知内容

为保障推送内容信息的合法性、真实客观性、一致性、可读性，以及用户良好的通知使用体验，请您遵守[通知内容管理细则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-detail-rules)。

## 通知样式

### 通知样式规范概要

|总体原则|例外|
|:--|:--|
|不得伪造其他应用的推送消息，包括伪造应用icon、消息内容等。|-|
|应用通知不得隐藏应用自身的icon。|-|
|禁止使用不符合设计规范的样式。|-|
|不得利用当前系统内仍存在的通知，将特定通知强制置顶显示。|语音、视频通话、媒体播放、进度类通知（下载、更新、上传等）、录音、导航、投屏、运动计时、步数。|
|不得更改一键删除按钮。|-|
|不得伪造横幅通知、锁屏通知。|-|
|不得重复发送相同内容的通知打扰用户。|-|
|通知标题与文本内容不得重复。|-|

### 文本样式

|描述|图片展示|
|:--|:--|
|通知文本内容最多可显示3行，超长后以“...”截断。|请参考[设计-通知-普通通知](https://developer.huawei.com/consumer/cn/doc/design-guides/system-features-notification-0000001793074217#section4182426382)。|

### 通知角标

应用收到消息后以数字的形式展示角标，提醒用户查看消息。

|描述|图片展示|
|:--|:--|
|以数字的形式展示在右上角。|请参考[设计-通知-桌面图标角标](https://developer.huawei.com/consumer/cn/doc/design-guides/system-features-notification-0000001793074217#section20838133494210)。|

说明

Wearable、TV不支持此通知样式。

### 通知大图标

|描述|图片展示|
|:--|:--|
|适用于有图片预览的通知。|请参考[设计-通知-图片预览通知](https://developer.huawei.com/consumer/cn/doc/design-guides/system-features-notification-0000001793074217#section16214134103817)。|

通知大图标需要满足以下要求：

- 图片格式建议使用JPG/JPEG/PNG/BMP，图片长*宽建议小于128*128像素，若超过49152像素，则图片不展示。
- 避免使用饱和度较高的颜色和纯色（如纯黑色、纯红色），颜色纯度和亮度的范围在10%-90%。
- 图片应清晰可读，避免使用影响图片信息阅读体验的元素，包括但不限于二维码、马赛克、明显噪点、密集排布的文字和符号等。
- 图片品质应与通知整体内容品质一致，避免使用内容复杂、排版凌乱、元素混杂、影响整体视觉效果的图片。
- 图片不可影响通知必要文字内容的阅读。

说明

Wearable不支持此通知样式。

### 多行文本样式

应用的通知内容文字较多，且通知消息内容需有序展示。

|描述|图片展示|
|:--|:--|
|适用于文本内容较长的通知，最多可显示3行内容，每行内容超长后以“...”截断。|请参考[设计-通知-多行文本类通知](https://developer.huawei.com/consumer/cn/doc/design-guides/system-features-notification-0000001793074217#section148485300395)。|

说明

Wearable不支持此通知样式。

## 通知跳转

- 不得以推送消息为手段，利用本应用唤醒其他应用。
- 通知点击跳转链接不得为非法网站。
- 不得利用推送消息诱导下载安装第三方应用。

## 通知开关授权

- 应用首次启动时需询问用户通知开关是否需要开启。
- 未获取用户授权，应用的通知开关默认为关闭状态。

## 其他

- 应用不得擅自篡改、损坏、反编译Push Kit提供的服务功能，改变Push Kit的基本功能。
- 避免出现其他可能影响终端用户体验的行为。
- 应用使用推送服务时，推荐接入[应用内通知设置快捷入口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-shortcut-settings)，便于用户找到应用内的通知分类控制开关，提升用户通知管理的体验，减少应用通知关闭率。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-preparations "开发准备")
# 开通推送服务

更新时间: 2025-12-16 16:36

在开通推送服务前，请先参考“[应用开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview)”创建项目和应用工程。

说明

从HarmonyOS NEXT Developer Beta2起，开发者无需配置公钥指纹和Client ID。

## 操作步骤

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163652.33039487343218571128360686649022:50001231000000:2800:D084738E58FEF6DB70E7C01AB5BCF5FEF8DA6DC430543BC734C308E2C09ED099.png "点击放大")
    
2. 在项目列表中找到您的项目，在项目下的应用列表中选择需要配置推送服务参数的应用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163652.07447432826400728160611438694428:50001231000000:2800:455803A34FE680920ACD01D841859AD571D6A3D4D546D0D01B731B7C64904BF6.png "点击放大")
    
3. 在左侧导航栏选择“增长 > 推送服务”，点击“立即开通”，在弹出的提示框中点击“确定”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163652.43841863892245731697141526982217:50001231000000:2800:226FD54EA440265107D28DA13C0887CEFF94C107755D5AAEDBBCA9A8926D5D33.png "点击放大")
    
    说明
    
    推送服务权益为项目级，若您已有开通过推送服务的项目，当您在项目中添加新的应用时，无需再次开通推送服务。
    
4. 若项目当前未配置数据处理位置，请在提示中点击“确定”，会弹出设置数据处理位置的弹窗。完成数据处理位置的设置，点击“确定”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163652.46277148077261807726337776634106:50001231000000:2800:50C6302FC680CF7E2610B510AE0BD24B1A57EC019B97333B76E4EC383C1BC2A3.png "点击放大")
    
    注意
    
    推送服务当前Wearable设备支持的国家请参见[支持的国家/地区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-country)，数据处理地可根据支持的国家/地区设定；其他设备仅支持中国境内（不包含中国香港、中国澳门、中国台湾），数据处理地固定为中国。
    
5. 针对开发调试场景，从DevEco Studio 6.0.0 Beta5版本开始，新增了更高效的自动签名方案，开发者可以选择以下其中一种方式进行调试阶段的应用签名。
    
    - 手动签名：调试阶段**必须**申请调试证书、[注册调试设备](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-device-0000002283189937)、确保“增长 > 推送服务”中已开通“推送服务”后**重新**申请调试Profile文件，并完成[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。
    - 自动签名（新增）：请参考[自动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237)，开通Push Kit开放能力，点击“OK”后，DevEco Studio将自动重新签名。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163652.31838126977679496279555300264978:50001231000000:2800:106E392938341F94E8178EAFA7F429F9D0837FA48D478A3E09F07FE0EC37B12B.png "点击放大")
        
        5-10分钟后访问[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，“项目设置 > 开放能力管理”中推送服务能力将显示已勾选。同时，“增长 > 推送服务”中“推送服务”将自动开通。![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163652.65748553715246048565625692027249:50001231000000:2800:6F222D12BEAD052E37B33E21D7AB54673C8E8A0165421EA85478A78AA394E836.png "点击放大")
        
    
6. 应用发布阶段**必须**申请发布证书、确保“增长 > 推送服务”中已开通“推送服务”后重新申请发布Profile文件，并完成手动签名。详情请参考发布应用[配置签名信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-publish-app#section280162182818)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163653.24510656711037511076670502367998:50001231000000:2800:E42AA0469F4A846D3B6207FFCE3486EB72D7370221A84396456842D14E3BF60D.png "点击放大")
    
7. 您还可以通过“增长 > 推送服务 > 配置”，在“配置”页签下选择需要申请自分类权益的应用，点击**自分类权益**后的“申请”，详见[申请步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section16708911111611)。
    
    注意
    
    强烈建议您申请通知消息的**自分类权益**，并按对应分类发送通知消息。**否则Push Kit默认您推送的是资讯营销类消息**，会导致单个应用每日每设备推送数量为**2条**或**5条**。
    
8. （可选）您还可以通过“增长 > 推送服务 > 配置”，在“配置”页签开通或关闭您的项目级和应用级的[消息回执](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-msg-receipt)。
    
    说明
    
    - 若项目级的消息回执权益开通，应用级的消息回执权益未开通，则该应用消息回执权益取项目级的。
    - 若项目级的消息回执权益开通，应用级的消息回执权益开通，则该应用消息回执权益取应用级的。
    

## （可选）设置数据处理位置

您可以在“项目设置 > 数据处理位置”页面设置或更新数据处理位置，步骤如下：

注意

如果设置的数据处理位置与您的服务器位置不一致，或者设置的数据处理位置与应用所服务的用户所在地不一致，都会导致推送消息无法下发。

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”。
2. 在项目列表中点击您需要设置数据处理位置的项目。
3. 进入“项目设置 > 数据处理位置”页面，点击“管理”。
4. 按需设置数据处理位置。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163653.22285011873374140628059846876538:50001231000000:2800:7FE65CE23AF99320C2A1432F15E257D44BB2697BA6EE4938E6A967E71A25179F.png "点击放大")
    
5. 设置完成后，点击“保存”。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-specification "学习Push Kit接入规范")
# 申请推送场景化消息权益

更新时间: 2025-12-16 16:37

## 场景化消息权益简介

Push Kit支持多种场景化消息类型，其中部分场景化消息类型需要您申请特殊权益才能正常发送。具体见下表：

|场景化消息权益名称|功能描述|开放申请场景|
|:--|:--|:--|
|通知消息自分类权益|允许开发者自行对通知消息进行分类，以改善终端用户推送体验。您无须申请此权益也能推送通知消息，未开通权益时，Push Kit默认您推送的是**[资讯营销类](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1924971516101)**消息。<br><br>注意<br><br>**若您未申请通知消息自分类权益，则推送的通知消息默认为资讯营销类****消息。**资讯营销类消息每天可发送消息数量根据应用类型分为**2条**或**5条。**若您发送通知消息被频控，请尝试发送测试消息或申请自分类权益。|所有应用可申请，部分自分类申请需与应用分类相关。|
|推送通知扩展消息权益|消息到达后，推送通知消息，同时唤醒应用执行语音播报等动作。您必须申请此权益才能推送通知扩展消息。|仅对有商家新订单提醒、商家收款场景的应用开放。|
|推送应用内通话消息权益|应用内通话消息到达用户设备后，唤醒目标应用，弹出呼叫接听界面，实现音视频通话。您必须申请此权益才能推送应用内通话消息。|仅用于具备应用内音视频通话功能场景的沟通类、告警类应用。<br><br>仅服务于自身企业或政府组织单位内部。|

有关场景化消息权益的内容及申请方式，请见下方具体章节。

说明

如果您在申请过程中遇到任何问题，请发送邮件至[hwpush@huawei.com](mailto:hwpush@huawei.com)与我们取得联系。

## 申请通知消息自分类权益

### 通知消息分类方式

为了改善终端用户推送体验、营造良好可持续的通知生态，Push Kit对[通知消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-alert)进行分类管理。根据消息内容，Push Kit将通知消息分类为**服务与通讯**、**资讯营销**两大类别。如您希望通知消息能更精准地符合业务需要，可以根据[通知消息分类标准](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1924971516101)，自行对消息进行分类。

未开通通知消息自分类权益的应用，通知消息类型将会默认归为**资讯营销类消息**。

分类方式示意图：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163702.53523318034200413157221027391867:50001231000000:2800:C1B8D97EA99D258BD42BE5C6800DB7EB3D1578E18640F2C9758347B83B7DAACC.png "点击放大")

说明

- 若应用有通知消息自分类权益，且推送通知消息时携带已开通的[category](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)字段，将信任开发者提供的分类信息（若应用仅发送资讯营销消息，则无需申请自分类权益）。
- 若应用推送通知消息时携带未开通权益的[category](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)字段值（例如，未开通“IM”却在推送通知消息时在category中传入“IM”），应用的通知消息将自动归类为资讯营销消息。

通知消息分类标准适用于[推送通知消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert)、[推送通知扩展消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-extend-noti)，若您的应用使用推送通知消息、推送通知扩展消息，需按照[通知消息分类标准](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1924971516101)进行分类。其他场景化消息可按照相应的指导完成开发适配。

### 通知消息分类标准与提醒方式

结合应用的消息内容和消息发送场景，Push Kit将通知消息分类为**服务与通讯类**和**资讯营销类**，并对不同类别的通知消息的提醒方式、消息展示位置、推送数量进行差异化管理，具体如下：

|**消息类别**|**场景说明**|**提醒方式**与消息展示位置|推送数量限制|
|:--|:--|:--|:--|
|服务与通讯|包括社交通讯与服务提醒类消息，指应用借助通知中心及时向用户传递重要通知提醒，通常用户对接收此类消息有预期。|锁屏、铃声、振动等<br><br>说明<br><br>**服务提醒类消息**在Wearable上静默通知，仅在通知中心展示消息。<br><br>TV不支持铃声和振动。|系统会根据现网使用场景和流量进行管控，不合理的使用场景系统会进行频控|
|资讯营销|包括资讯类消息和营销类消息，指的是运营人员向用户发送的活动信息、内容推荐、资讯等。|静默通知，仅在通知中心展示消息<br><br>说明<br><br>**资讯营销类消息**在Wearable上支持锁屏、铃声、振动等提醒方式。<br><br>TV不支持铃声和振动。|根据应用类别限制每日推送数量，单个应用每日每设备推送数量为2条或5条。|

说明

随着应用的消息发送场景不断变化，Push Kit的分类标准也将不断演进和补充，请及时留意本文档最新的分类说明。

**服务与通讯类****-社交通讯**

|**消息类型**|云端通知category取值|**场景说明**|**消息提醒方式**|
|:--|:--|:--|:--|
|即时聊天|IM|用户间点对点聊天消息（或私信）、群聊天消息。<br><br>**注：需承诺不包括未关注人的私信、官方号或者商家批量推送给用户的私信或广告。**|表示通知消息为**服务与通讯类**中的社交通讯。消息提醒方式默认为锁屏+铃声+振动（实际提醒方式以应用在通知管理中的设置为准）。|
|音频、视频通话|VOIP|语音通话邀请、视频通话邀请、来电提醒等。<br><br>**注：仅为用户通知提醒，不涉及在后台拉起应用进程建立通话过程。**|
|MISS_CALL|未接通话消息提醒。|

**服务与通讯类-服务提醒**

|**消息类型**|云端通知category取值|**场景说明**|**消息提醒方式**|
|:--|:--|:--|:--|
|出行|TRAVEL|用户出行产生的通知提醒，推送对象为消费者。<br><br>- 行程提醒。<br>- 班车/航班变动提醒。<br>- 酒店入住前提醒。<br>- 公交到站提醒。|表示通知消息为**服务与通讯类**中的服务提醒。消息提醒方式默认为锁屏+铃声+振动（实际提醒方式以应用在通知管理中的设置为准）。<br><br>说明<br><br>Wearable上静默通知，仅在通知中心展示消息。|
|健康|HEALTH|用户主动测量的健康数据通知，仅限运动类、健康类应用使用。<br><br>- 运动量（步数、骑行里程、游泳距离等）。<br>- 身体数据（心率、体重、体脂、消耗卡路里等）。|
|工作事项提醒|WORK|用户下一步需要做某件事项的提醒、待处理的业务流程。<br><br>- 工作提醒：会议提醒、待办提醒、日程安排、教学任务/课程提醒等。<br>- 待处理业务流程，推送对象为服务提供方：审核进度提醒、认证状态流程提醒、工单处理、卖家收到订单提醒、卖家收到售后提醒、催促卖家发货提醒、司机接单提醒。<br>- 商家运营：库存不足、售罄提醒、商品下架通知、限制提现、客诉警告、店铺限制、商品黑名单、交易违规、涉假/涉欺诈发货通知。|
|账号动态|ACCOUNT|用户账号和账号下资源资产的动态信息。<br><br>- 账号：账号上下线、账号状态变化、账号信息认证等。<br>- 资产：会员到期/过期、续费提醒、余额变动（余额必须为真实的资产变动，且需排除积分变动、金币变动，排名更新等）。|
|订单&物流|EXPRESS|正在交易或完成交易的订单信息及物流状态信息。<br><br>- 订单，推送对象为消费者：下单成功、订单详情、订单状态、订单投诉处理进度、开票信息。<br>- 物流：已发货、派送中、签收、取件。|
|财务|FINANCE|金额变化的交易提示、用户的理财/投资相关信息提示，仅限金融银行类、支付类应用使用。<br><br>- 收付款、银行到账&扣款、交易提醒、催缴&退款信息、充值、待支付账单、贷款受理进度、还款/逾期提醒、资金冻结提醒、资金限制提醒、缴纳保证金提醒。<br>- 理财购买成功提醒、理财产品到期/开放赎回提醒、分红/收益提醒、风险等级调整提醒。<br>- 条件单触发、委托交易提醒、中签提醒、自动续期或赎回提醒、净值提醒、配股/配债提醒、预约打新提醒、股票买卖交易提醒。|
|设备提醒|DEVICE_REMINDER|IoT设备发出的设备状态/信息/提示/告警等提醒消息。|
|邮件|MAIL|新收到的邮件，仅限邮箱类应用、办公软件应用使用。|
|语音播报|PLAY_VOICE|需要用户特别注意的语音提醒，语音由应用本身进行播报。商家运营：用户支付金额提醒，用户取消支付提醒，来订单通知提醒。|表示通知消息为**服务与通讯类**中的服务提醒。消息提醒方式默认为锁屏+振动（实际提醒方式以应用在通知管理中的设置为准）。为了避免和应用中的语音播报冲突，此种类型消息无铃声提醒。<br><br>说明<br><br>Wearable上静默通知，仅在通知中心展示消息。|
|订阅|SUBSCRIPTION|用户主动订阅的内容并确认会收到推送（订阅仅开放以下场景，其他场景不支持申请）。<br><br>- 主动设置的直播开播提醒、预约活动提醒。<br>- 主动设置的签到打卡提醒。<br>- 主动设置的商品降价提醒。<br>- 特别关注的账号/作者发布动态、书籍更新提醒。<br>- 用户主动设置的行情动态提醒（价格波动和预测）。<br>- 付费订阅内容提醒。<br>- 主动订阅的专题提醒（如新闻、财经动态、天气、垂直行业相关信息）。<br>- 用户之间的社交互动提醒（好友动态、新增粉丝、添加好友、被赞、被@、被收藏、评论、留言、关注、回复、转发等）。|表示通知消息为**服务与通讯类**中的服务提醒。消息提醒方式默认为锁屏+铃声+振动（实际提醒方式以应用在通知管理中的设置为准）。<br><br>说明<br><br>- Wearable上静默通知，仅在通知中心展示消息。<br>- 申请订阅消息类型须遵循下方订阅流程要点。<br>- 推荐应用接入[应用内通知设置快捷入口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-shortcut-settings)，便于用户找到应用内的通知分类控制开关，提升用户通知管理的体验，减少应用通知关闭率。|

**订阅流程要点**

|订阅类型|订阅场景|订阅流程要点（申请时需提供满足下方要求的应用内订阅流程示意图）|
|:--|:--|:--|
|普通订阅类|直播开播提醒<br><br>预约活动提醒<br><br>签到打卡提醒<br><br>商品降价提醒<br><br>特别关注的账号/作者发布动态<br><br>书籍更新提醒<br><br>行情动态提醒<br><br>付费订阅内容提醒<br><br>主动订阅的专题提醒|- 页面应具备“订阅/关注”和对应取消订阅/关注的按钮。<br>- 订阅/关注的消息推送按钮需默认关闭。<br>- 订阅之后需独立弹窗询问用户是否接收该订阅的消息推送。<br>- 推送内容中需要体现该条推送是用户的订阅消息（在消息标题或正文中携带“订阅/预约/关注/好友/粉丝”等字样）。<br>- 订阅消息的范围不宜过于宽泛、不具体（错误示例：订阅资讯、兴趣标签等，则过于宽泛、不具体）。|
|社交动态类|用户之间的社交互动提醒|- 应用设置中有独立的消息开关，如评论、回复、收藏、点赞等。<br>- 推送内容中需要体现该条推送是用户的订阅消息（在消息标题或正文中携带“订阅/预约/关注/好友/粉丝”等字样）。|

**订阅流程示意图**

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163703.94202329168794333254107271832336:50001231000000:2800:C7B77FBDD31E16F7645F4C1B168CA88C2F17C32093601B034D0833B4248CCE39.png "点击放大")

**资讯营销类-内容资讯**

|**消息类型**|云端通知category取值|**场景说明**|**消息提醒方式**|
|:--|:--|:--|:--|
|财经动态|MARKETING|股票、彩票、期货、期权、外汇类通知，包括交易信息、行业公告等。|表示通知消息为**资讯营销类**。消息提醒方式为静默通知，仅在通知中心展示。<br><br>说明<br><br>Wearable上为锁屏+铃声+振动（实际提醒方式以应用在通知管理中的设置为准）。|
|生活资讯|导航：行驶路线、路况规划、路线中的交通状况（拥堵提醒）、位置使用、调用地图类应用进行定位等相关的通知。|
|调研|发送问卷以获得受访者的态度和意见，包括使用习惯、产品满意度、服务满意度等。|
|其他|面向广大用户发布的产品功能推荐、平台公告、应用更新升级提醒等。|
|内容推荐|非用户主动订阅，应用向用户推送的内容。<br><br>包括点评、书籍、广告、视频、音频、节目、课程、直播、社区话题、游戏宣传等。|
|新闻|及时地报道新近发生的、有价值的事实。<br><br>包括政治新闻、经济新闻、法律新闻、军事新闻、科技新闻、文教新闻、体育新闻、社会新闻等。|
|社交动态|用户推荐：附近的人、大V、主播、异性、可能认识的人等。|

**资讯营销类-营销活动**

|**消息类型**|云端通知category取值|**场景说明**|**消息提醒方式**|
|:--|:--|:--|:--|
|功能推荐|MARKETING|推荐用户使用当前产品的某一个功能。|表示通知消息为**资讯营销类**。消息提醒方式为静默通知，仅在通知中心展示。<br><br>说明<br><br>Wearable上为锁屏+铃声+振动（实际提醒方式以应用在通知管理中的设置为准）。|
|运营活动|非用户主动设置，由应用发起需由用户参与的运营活动、提醒消息、游戏提醒、服务等。|
|产品促销|产品信息相关推广、产品优惠，例如满减、低至、促销、买一送一、返利、优惠券、代金券、送红包相关的通知。|

### 通知消息推送数量管理规则

根据[通知消息分类标准](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1924971516101)，Push Kit将通知消息分为服务与通讯、资讯营销两大类别。对这两类通知消息，Push Kit有不同的频控规则。

- 服务与通讯类消息推送数量受设备消息频控限制，系统会根据现网使用场景和流量进行管控，不合理的使用场景系统会进行频控。更多频控说明请参见[消息频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control)。
- 资讯营销类消息会根据应用类型对每日推送数量进行上限管理。详情请见下表。

说明

- 关于应用类别信息，请参见[华为应用市场应用分类示例](https://developer.huawei.com/consumer/cn/doc/50103)。
- 单个应用每日每设备消息发送数量限制中的“每日”指的是自然日。
- 如应用不在下述分类中，或者未申请自分类权益，单个应用每日每设备推送数量默认为2条。
- 为避免在调测阶段消息被频控，建议调测阶段发送测试消息，详情请参见[消息频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control)。

|**二级分类**|**三级分类**|**单个应用每日每设备通知推送数量（单位：条）**|
|:--|:--|:--|
|新闻阅读|新闻（需具备《互联网新闻信息服务许可证》）|5|
|电子书、杂志、有声读物、动漫、幽默、体育、分类信息|2|
|休闲益智|所有|2|
|经营策略|所有|2|
|体育竞技|所有|2|
|棋牌桌游|所有|2|
|动作射击|所有|2|
|角色扮演|所有|2|
|影音娱乐|所有|2|
|实用工具|所有|2|
|社交通讯|所有|2|
|教育|所有|2|
|拍摄美化|所有|2|
|美食|所有|2|
|出行导航|所有|2|
|旅游住宿|所有|2|
|购物比价|所有|2|
|商务|所有|2|
|儿童|所有|2|
|金融理财|所有|2|
|运动健康|所有|2|
|便捷生活|所有|2|
|汽车|所有|2|
|主题个性|所有|2|

### 申请步骤

**申请原则**

当您充分了解了[通知消息分类方式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section12819174063215)，准备申请通知消息自分类权益前，建议您先确认申请是否满足以下原则：

1. 应用的推送消息按照一定维度进行分类，且分类符合[通知消息分类标准](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1924971516101)。
2. 应用遵守[《华为推送服务使用协议》](https://developer.huawei.com/consumer/cn/doc/app/20213)和相关规范，且未产生违规记录。
3. 消息类型需与分类规则要求一致，消息内容示例需与消息类型描述对应。

**申请流程**

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，点击“开发与服务”，在项目列表中找到您的项目，通过“增长 > 推送服务 > 配置”，在“配置”页签下选择需要申请自分类权益的应用，点击**自分类权益**后的“申请”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163703.10043811276655072612386985133376:50001231000000:2800:48213C4E40BBBDEA4FE38E55A44546782D38C35B5F1A24834A5E99E6DD034BFB.png "点击放大")
    
2. 选择消息发送类型，下一步补充消息示例（订阅消息类型需要额外补充场景说明和图片），提交完成后可以通过“查看进展”按钮查看审批进展。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163703.19762797851191904465118440959593:50001231000000:2800:9597433CCE733D38C833D5BF5B3A0E2AFE95C120535D4E1F5025CC3F9066ADE8.png "点击放大")
    
    注意
    
    - 若某消息类型已经申请通过，后续满足此类型的场景范围的消息无需重复申请。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163703.79731354019918309726602997475042:50001231000000:2800:592836BF88ADEA429DC27AE67F38DFAD441652E0716452C716A4C4A4D6A2876E.png "点击放大")
    
    注意
    
    - 消息内容示例需与消息类别的场景相符，且不可包含营销、广告内容。若填写的内容与场景不符，或含营销、广告内容，将按照推送服务《通知违规处罚标准》进行处罚。
    - 为了能够让审核人员理解，并顺利审批通过，请在消息内容示例里尽可能详实的描述消息示例，或者说明消息场景。
    
    说明
    
    以下消息内容仅为示例，需要根据业务实际情况填写。
    
    订单&物流消息类型内容示例：
    
    您购买的商品下单成功，请查看订单详情。
    
    订阅消息类型内容示例：
    
    您订阅/关注的XX主题/XX作者/XX活动有内容更新了，点击查看。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163703.02822164964997670971334942393404:50001231000000:2800:8020C7A0902BD65724F64474F92D7A6413E142AA76DE62F3A3BDBDC3E09A20C1.png "点击放大")
    
3. 非首次申请时可以点击“新增类型”按钮跳转进行消息类型的申请。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163703.35637718056857864114944096226306:50001231000000:2800:B7A26DB99606749EA0D82BEE97980B96C5500D43DAFD5659EB19A3E5CB775281.png "点击放大")
    
4. 消息类型申请审核周期为5个工作日，您可以点击自分类权益后的“**详情**”查看已申请通过的消息类型。也可以通过“申请记录”查看申请过的消息类型。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163703.73974823848355247561164871068879:50001231000000:2800:A78D9B478B57316E17C2C412D69E31A6CC40A86002865DF197079AA0063150D6.png "点击放大")
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163703.28756864978957858098018898223062:50001231000000:2800:1EF8AF184F60FC23ED33B4B36506AEF9B79E36AC2D8AD18910E721BA88043E70.png "点击放大")
    
    点击“申请记录”可以查看申请过的消息类型，对申请记录进行查看、编辑、删除等操作。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163704.75320458176119830979628888499719:50001231000000:2800:1AEC2A11CC0A0108C37C24B5AEE164E051183E552A6AD1612CE8F3BC59EF2641.png "点击放大")
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163704.34824528593044605344674428664200:50001231000000:2800:7722A1CC2ECD2BE6A3E1961C1BB3FB2650EBE4E0EF23539E204C13725A8D9186.png "点击放大")
    
5. 若您的申请已经审核通过（审核通过5分钟后，您申请的自分类权益生效），请根据申请自分类类型适配云端category字段。
    
    自分类权益生效后，应用推送的通知消息类型将根据您发送消息时的云端[category](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)字段进行归类。
    
    category字段取值为大写的英文单词，且仅可填写在分类权益页面中已审批通过的category值，若出现分类错误或违反通知消息分类标准的场景，将被判为违规。
    
    违规行为及相应的处理措施请参见[通知违规处罚标准](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-punishment-standards)。
    
    说明
    
    如果您对上述规则有任何疑问，请发送邮件至[hwpush@huawei.com](mailto:hwpush@huawei.com)与我们取得联系。
    

## 申请推送应用内通话消息权益

应用内通话消息到达用户设备后，唤醒目标应用，弹出呼叫接听界面，实现音视频通话。

该场景仅用于具备应用内音视频通话功能场景的沟通类、告警类应用。

**申请步骤**

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，点击“开发与服务”。
2. 在项目列表中找到您的项目，通过“项目设置 > 选择应用”，在“开放能力管理”页签下找到推送服务的“推送应用内通话消息”权益，点击“申请”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163704.00617707092003667256392659305254:50001231000000:2800:832684E9443AF5F0D6D05AA9B36D03B49E48D6A120A04364099ACD3C0F0FE7A0.png "点击放大")
    
    进入申请页面，按照申请原因现有模板，补充应用信息，上传附件，点击“提交”。
    
    **图1**  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163704.92035477836719556624173669324781:50001231000000:2800:A8967EEA185144403D6591F7D84552A71103977616E4F1511A1404CADD7D82E4.png "点击放大")
    
    **图2**
    
    说明
    
    - 申请权益时，请在附件中上传对应材料：应用为企业内部应用时需提供被服务主体盖章的证明函、为非企业内部应用时需提供《增值电信业务经营许可证》（B22国内多方通信服务业务）。
    - 依照《[中华人民共和国电信条例](https://www.gov.cn/gongbao/content/2016/content_5139478.htm)》《[互联网信息服务管理办法](https://www.cac.gov.cn/2014-08/19/c_1112138363.htm)》，国家对电信业务经营按照电信业务分类，实行许可制度。经营电信业务，必须依照本条例的规定取得国务院信息产业主管部门或者省、自治区、直辖市电信管理机构颁发的电信业务经营许可证。未取得电信业务经营许可证，任何组织或者个人不得从事电信业务经营活动。其中，开展多方通信业务需取得《增值电信业务经营许可证》（B22国内多方通信服务业务），因此申请该权益需提供《增值电信业务经营许可证》（B22国内多方通信服务业务）。具体资质的要求应由电信管理机构审核确定，华为将遵从监管指示对不符合上架资质要求的给以下架处理。
    - Wearable、TV、PC/2in1不支持该权益。
    
    **应用内通话消息权益申请证明函**：
    
    应用名称：***
    
    应用包名&APPID：***&***
    
    承诺事项：
    
    1. （应用名称***）的应用内通话消息仅用于符合规定的场景中（音视频通话场景）。
    
    2. 业务结束后，应用不再阻止系统休眠。
    
    3. 申请的应用内通话消息权益仅用于本应用，且仅服务于本公司/本组织单位内部员工，不会转交或提供给其他范围或非本单位内部员工使用。
    
    4. 如有违反上述1、2、3的其他行为，同意华为Push侧将该权益收回。
    
    XXX公司
    
    XXXX年XX月XX日
    
3. 申请提交之后，进入”互动中心”页面，审批进展会由智能助手通知，审核期限为8个工作日内。如果退出互动中心页面，后续可以点击AGC平台右上角气泡图标再次进入。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163704.61467805555602376182787763627779:50001231000000:2800:D32299C39445A886D1040BF9625D7B30D1DEE102ED9F78357B8D392919678EE4.png "点击放大")
    
4. 审核通过，权益立即生效，推送服务的“推送应用内通话消息”权益被勾选。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163704.96702947791045165089947175336937:50001231000000:2800:BC147C21546E2A5CA9D0B95DC09688B995AC7E2DE13776C96A8B522E0E3F1A86.png "点击放大")
    

## 申请推送通知扩展消息权益

当用户终端收到您发送的通知扩展消息后，Push Kit会拉起应用的子进程，您可以在子进程中自行处理业务，执行语音播报等动作，每次拉起通知扩展子进程的时长默认为10秒，每次拉起通知扩展子进程后，请在10秒内完成事务处理，超出10秒子进程生命周期结束。

申请推送通知扩展消息存在以下限制：

- 该场景化消息仅为有商家新订单提醒、商家收款场景的应用开放。
- 应用不得以推送消息为手段，利用通知扩展消息能力拉起应用主进程。

**申请步骤**

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，点击“开发与服务”。
2. 在项目列表中找到您的项目，通过“项目设置 > 选择应用”，在“开放能力管理”页签下找到推送服务的“推送通知扩展消息”权益，点击“申请”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163704.40594205024086718556848590528344:50001231000000:2800:FDE0D339056F262376A445870159D6879B5B938C5FC902BCC2B247BEA0BB60C3.png "点击放大")
    
    进入申请页面，按照申请原因现有模板，补充应用信息，上传附件，点击“提交”。
    
    **图3**  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163704.38220020355788321437481881188387:50001231000000:2800:4E19F0323C0ED98DD055CA3AF69EE3A923FD32789DA625C40646C4434E332CA6.png "点击放大")
    
    **图4**
    
    说明
    
    - 申请权益时，请在附件中上传语音消息通知界面截图或示意图或语音播报录像。
    - TV不支持该权益。
    
3. 申请提交之后，进入”互动中心”页面，审批进展会由智能助手通知，审核期限为8个工作日内。如果退出互动中心页面，后续可以点击AGC平台右上角气泡图标再次进入。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163704.65086159903926552456623079483966:50001231000000:2800:F6032FB1E4EC36AAFCD299FBC02EA73A0BF4C38470A017C3CFD63158C933B9BE.png "点击放大")
    
4. 审核通过，权益立即生效，推送服务的“推送通知扩展消息”权益被勾选。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163704.49618463785020395462309693882186:50001231000000:2800:FEC845A6AFA6448DDCE31C9646753ACD189C19E018655BFC0C89D74E60421BC4.png "点击放大")
    

## 申请自定义铃声权益

当用户终端收到您发送的[通知消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-alert)/[推送通知扩展消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-extend-noti)时，如果消息携带**[sound](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)**字段，通知提示会播放该自定义铃声， 否则播放系统默认铃声；如果消息同时携带**[soundDuration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)**字段，则自定义铃声的时长受此字段控制。

说明

为进一步优化推送服务自定义铃声功能使用体验，从2025年11月开始，自定义铃声功能不再作为权益管控项，权益不需要申请即可使用。

原本申请过自定义铃声权益的业务仍可正常使用，无需对代码或业务流程进行调整。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-config-setting "开通推送服务")
# 获取Push Token

更新时间: 2025-12-16 16:37

## 场景介绍

注意

Push Kit对Push Token进行了推送服务权益校验，请在进行开发前先阅读[开通推送服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-config-setting)章节，完成相关配置。

Push Token标识了每台设备上每个应用，开发者调用[getToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section562973524818)()接口向Push Kit服务端请求Push Token，获取到之后使用Push Token来推送消息。

Push Token一般情况不会变化，仅下列场景会导致之前的Push Token发生变化而失效：

- 卸载应用后重新安装。
- 设备恢复出厂设置。
- 应用显式调用[deleteToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section1298316346493)()接口后重新调用[getToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section562973524818)()接口。
- 应用显式调用[deleteAAID](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-aaid-api#section18269336164311)()接口后重新调用[getToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section562973524818)()接口。
- 将设备（仅涉及Wearable设备）拿到海外其他国家或者地区后，系统会更新设备的token。更新后的token通过[pushService.on('tokenUpdate')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section1730794845210)接口的回调返回。

因此，建议您在应用启动时调用getToken()接口，若设备的Push Token发生变化，及时上报到您的应用服务器更新Push Token，以防由于Push Token失效导致收不到消息。

## 约束与限制

获取Push Token能力支持Phone、Tablet、PC/2in1设备。并且从5.1.0(18)版本开始新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 注意事项

- 请勿使用Push Token跟踪标记用户。
- 应用不要固定判断Push Token长度，因为Push Token长度可能会变化。
- 禁止应用频繁申请Push Token。建议应用每次启动时获取Push Token。
- 只有在[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)平台[开通推送服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-config-setting)后，[getToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section562973524818)方法才会返回Push Token。

## 接口说明

接口返回值有两种返回形式：Callback和Promise回调。下表中仅展示Promise回调形式的接口，Promise和Callback只是返回值方式不一样，功能相同。

|接口名|描述|
|:--|:--|
|[getToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section562973524818)(): Promise<string>|以Promise形式获取Push Token。|
|[deleteToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section1298316346493)(): Promise<void>|以Promise形式删除Push Token。|

## 获取Push Token

1. Push Kit对Push Token进行了推送服务权益校验，请在进行开发前先阅读[开通推送服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-config-setting)章节，完成相关配置。
2. 导入pushService模块及相关公共模块。
    
    1. import { pushService } from '@kit.PushKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { UIAbility, AbilityConstant, Want } from '@kit.AbilityKit';
    
3. 建议在您的UIAbility（例如EntryAbility）的[onCreate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#oncreate)()方法中调用[getToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section562973524818)()接口获取Push Token并上报到您的服务端，方便您的服务端向终端推送消息。代码示例：
    
    1. // 文件路径: src/main/ets/entryability/EntryAbility.ets
    2. export default class EntryAbility extends UIAbility {
    3.   // 入参 want 与 launchParam 并未使用，为初始化项目时自带参数
    4.   onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    5.     // 获取Push Token
    6.     pushService.getToken().then(token => {
    7.       hilog.info(0x0000, 'testTag', 'Succeeded in getting push token');
    8.     }).catch((err: BusinessError) => {
    9.       hilog.error(0x0000, 'testTag', 'Failed to get push token: %{public}d %{public}s', err.code, err.message);
    10.     })
    11.     // 上报Push Token并上报到您的服务端
    12.   }
    13. }
    

注意

若您获取Push Token时发生APP身份验证失败错误（1000900010），请参考[ArkTS API错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-error-code#section3835124673016)排查。

## 删除Push Token

注意

删除Push Token后，本应用下的所有Push Kit历史数据会一并删除。非必要情况，请您不要主动调用[deleteToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section1298316346493)()接口。

1. 导入pushService模块
    
    1. import { pushService } from '@kit.PushKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { UIAbility } from '@kit.AbilityKit';
    
2. 调用PushService.[deleteToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section1298316346493)()接口删除Push Token。代码示例：
    
    1. // 文件路径: src/main/ets/entryability/EntryAbility.ets
    2. export default class EntryAbility extends UIAbility {
    3.   async myDeletePushToken() {
    4.     try {
    5.       await pushService.deleteToken();
    6.       hilog.info(0x0000, 'testTag', 'Succeeded in deleting push token');
    7.     } catch (err) {
    8.       let e: BusinessError = err as BusinessError;
    9.       hilog.error(0x0000, 'testTag', 'Failed to delete push token: %{public}d %{public}s', e.code, e.message);
    10.     }
    11.   }
    12. }
    

#### Push Token更新回调

注意

该接口目前仅支持Wearable设备。

当设备离开当前国家或地区时，可能会触发Push Token自动更新，如果应用期望感知到Push Token更新事件，需要调用on接口进行回调注册；对应的，可以调用off接口解除回调注册，解除后当Push Token更新时，应用将不会收到回调。

1. 导入pushService模块
    
    1. import { pushService } from '@kit.PushKit';
    
2. 在您项目的ability（下以PushMessageAbility为例）内导入push模块，调用on()方法接收token更新的消息。注意，您仅能使用UIAbility接收token更新消息。代码示例：
    
    1. // 文件路径: src/main/ets/abilities/PushMessageAbility.ets
    2. import { UIAbility } from '@kit.AbilityKit';
    3. import { pushService } from '@kit.PushKit';
    4. import { hilog } from '@kit.PerformanceAnalysisKit';
    5. import { BusinessError } from '@kit.BasicServicesKit';
    
    6. // 无需新增UIAbility，在原有UIAbility的onCreate方法中调用即可。以PushMessageAbility为例 
    7. export default class PushMessageAbility extends UIAbility {
    8.   onCreate(): void {
    9.     const callBack = (data: string) => {
    10.       try {
    11.         hilog.info(0x0000, 'testTag', 'update token: %{public}s', data);
    12.       } catch (e) {
    13.         let err: BusinessError = e as BusinessError;
    14.         hilog.error(0x0000, 'testTag', 'Failed to update data: %{public}d %{public}s', err.code, err.message);
    15.       }
    16.     }
    
    17.     try {
    18.       // 注册token更新回调场景
    19.       pushService.on('tokenUpdate', this, callBack);
    20.       hilog.info(0x0000, 'testTag', 'Register on success');
    21.     } catch (e) {
    22.       let err: BusinessError = e as BusinessError;
    23.       hilog.error(0x0000, 'testTag', 'Register on error: %{public}d %{public}s', err.code, err.message);
    24.     }
    25.   }
    
    26.   onDestroy(): void {
    27.     try {
    28.       // 解除注册token更新回调场景
    29.       pushService.off('tokenUpdate');
    30.       hilog.info(0x0000, 'testTag', 'Register off success');
    31.     } catch (e) {
    32.       let err: BusinessError = e as BusinessError;
    33.       hilog.error(0x0000, 'testTag', 'Register off error: %{public}d %{public}s', err.code, err.message);
    34.     }
    35.   }
    36. }
    
3. 在项目工程的 src/main/module.json5文件的abilities模块的**skills**标签中配置**actions**内容为**action.ohos.push.listener**（有且只能有一个ability定义该action，**若同时添加****uris****参数，则uris****内容需为空**）。
    
    1. "abilities": [
    2.   {
    3.     "name": "PushMessageAbility",
    4.     "srcEntry": "./ets/abilities/PushMessageAbility.ets",
    5.     "launchType": "singleton",
    6.     "startWindowIcon": "$media:startIcon",
    7.     "startWindowBackground": "$color:start_window_background",
    8.     "exported": false,
    9.     "skills": [
    10.       {
    11.         "actions": [
    12.           "action.ohos.push.listener"
    13.         ]
    14.       }
    15.     ]
    16.   }
    17. ]
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right "申请推送场景化消息权益")
# 发送通知消息

更新时间: 2025-12-16 16:37

## 场景介绍

通知消息通过Push Kit通道直接下发，可在终端设备的通知中心、锁屏、横幅等展示，用户点击后拉起应用。您可以通过[设置通知消息样式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section5164103925811)来吸引用户。

## 约束与限制

发送通知消息能力支持Phone、Tablet、PC/2in1设备。并且从5.1.0(18)版本开始新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 开通权益

Push Kit根据消息内容，将通知消息分类为**服务与通讯**、**资讯营销**两大类别，开放通知消息自分类权益。

两种类型的通知消息在**提醒方式、消息展示位置、推送数量**上皆存在差异。更多说明与权益申请详情参见[申请通知消息自分类权益](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section16708911111611)。

注意

- **若您未申请通知消息自分类权益，则推送的通知消息默认为资讯营销类（[category](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)取值为MARKETING）消息**；若您仅需发送资讯营销类消息，则无需申请通知消息自分类权益。
- 资讯营销类消息每天可发送消息数量根据应用类型分为**2条**或**5条**，详情请参见[通知消息推送数量管理规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1128516504398)。若您发送通知消息被频控，请尝试发送测试消息或申请自分类权益，详情请参见[消息频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control)。

## 频控规则

**调测阶段**，每个项目每日全网最多可推送1000条测试消息。发送测试消息需设置[testMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)为true。

**正式发布阶段**，单设备单应用下每日推送消息总条数受[设备消息频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control#section993063213715)限制，系统会根据现网使用场景和流量进行管控，不合理的使用场景系统会进行频控。

服务通讯类消息与资讯营销类消息存在不同的频控策略，详情请参见[通知消息推送数量管理规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1128516504398)。

## 开发步骤

1. 参见指导[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)。
2. 为确保应用可正常收到消息，应用发送通知前需调用[requestEnableNotification](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-notificationmanager#notificationmanagerrequestenablenotification10-1)()方法弹出提醒，告知用户需要允许接收通知消息。示例代码如下：
    
    1. // 文件路径: src/main/ets/entryability/EntryAbility.ets
    2. import { BusinessError } from '@kit.BasicServicesKit';
    3. import { UIAbility } from '@kit.AbilityKit';
    4. import { window } from '@kit.ArkUI';
    5. import { hilog } from '@kit.PerformanceAnalysisKit';
    6. import { notificationManager } from '@kit.NotificationKit';
    
    7. export default class EntryAbility extends UIAbility {
    8.   onWindowStageCreate(windowStage: window.WindowStage) {
    9.     hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageCreate');
    10.     windowStage.loadContent('pages/Index', (err, data) => {
    11.       if (err.code) {
    12.         hilog.error(0x0000, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
    13.         return;
    14.       }
    15.       hilog.info(0x0000, 'testTag', 'Succeeded in loading the content. Data: %{public}s', JSON.stringify(data) ?? '');
    16.       notificationManager.requestEnableNotification(this.context).then(() => {
    17.         hilog.info(0x0000, 'testTag', `[ANS] requestEnableNotification success`);
    18.       }).catch((err: BusinessError) => {
    19.         hilog.error(0x0000, 'testTag', `[ANS] requestEnableNotification failed, code is ${err.code}, message is ${err.message}`);
    20.       });
    21.     });
    22.   }
    23. }
    
3. 为确保点击消息可以正常跳转应用页面，在应用项目中完成skills标签配置，详情请参见[点击消息动作](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section697519219136)。
4. 应用服务端调用Push Kit服务端的REST API推送通知消息。若未[开通权益](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section15809122792917)，或开通的权益类型与[调用REST API推送场景化消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-scenes-send)时，请求体中携带的[category](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)字段值不一致，消息将会默认归为**资讯营销类消息**，则会受到“单个应用每日每设备推送数量为2条或5条”的[频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1128516504398)限制。
    
    说明
    
    - 本示例仅包含REST API中部分消息字段，关于服务端开发的更多详情请参见[端云调试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-server)。
    
    - 请使用V3版本的请求URL（https://push-api.cloud.huawei.com/v3/[projectId]/messages:send）进行消息推送。
        
        请求URL版本为V3（https://push-api.cloud.huawei.com/v3/[projectId]/messages:send）时，仅支持给HarmonyOS Next/5.x及之后的系统版本推送通知；版本为V2（https://push-api.cloud.huawei.com/v2/[projectId]/messages:send）时，仅支持给HarmonyOS 3.x/4.x的系统版本推送通知。
        
    
    请求示例如下（注意category参数设置为实际消息类型）：
    
    1. // Request URL
    2. POST "https://push-api.cloud.huawei.com/v3/**[projectId]**/messages:send"
    
    3. // Request Header
    4. Content-Type: application/json
    5. Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
    6. push-type: 0
    
    7. // Request Body
    8. {
    9.   "payload": {
    10.     **"notification": {**
    11.       "category": "xxxxxx",// 替换为实际消息类型
    12.       "title": "普通通知标题",
    13.       "body": "普通通知内容",
    14.       "clickAction": {
    15.         "actionType": 0
    16.       },
    17.       // 通知是否在应用在前台情况下展示，仅对push-type为0的通知消息生效
    18.       "foregroundShow": true,
    19.       "notifyId": 12345
    20.     **}**
    21.   },
    22.   "target": {
    23.     "token": ["MAMzLg**********lPW"]
    24.   },
    25.   "pushOptions": {
    26.    "testMessage": true,
    27.     "ttl": 86400
    28.   }
    29. }
    
    - [projectId]：项目ID，登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”，在该页面获取。
    - Authorization：JWT格式字符串，可参见[Authorization](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct#section20573634202313)获取。
    - push-type：0表示Alert消息，此处为通知消息场景。
    - category：表示通知消息自分类的类别，MARKETING为资讯营销类消息，更多类别可参见[category](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)获取。
    - actionType：0表示[点击消息进入应用首页](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section1792616175914)，1表示[点击消息后进入应用内页](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section8794131614597)。
    - token：Push Token，可参见[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)获取。
    - testMessage：（选填）测试消息标识，true表示测试消息。每个项目每天限制发送1000条测试消息，单次推送可发送Token数不超过10个。详情请参见[testMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)。
    - ttl：（选填）消息缓存时间，详见[ttl](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)。
    - notifyId：（选填）自定义消息标识字段。不携带或者设置-1时，推送服务自动为每条消息生成一个唯一标识；不同的通知消息可以拥有相同的notifyId，实现新消息覆盖旧消息功能。仅支持数字，范围 [0, 2147483647]，若要**用于消息撤回则必填**。详情请参见[notifyId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)。
    - foregroundShow：（选填）通知消息是否在应用在前台时候展示。true表示应用在前后台都展示。false表示应用只在后台展示，应用在前台时，通知栏消息将不会展示。默认为true。foregroundShow为true时，[receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)不会被触发，无法获取消息数据。
    
5. 发送消息推送请求，请求响应请参见[响应参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-response)。请求发送成功后，可检查设备是否收到通知消息，如果设备未收到通知消息，请参见[常见问题](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-2)进行排查。

## 点击消息动作

### 点击消息进入应用首页

1. 检查项目模块级别下的**src/main/module.json5**中的[skills标签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#skills%E6%A0%87%E7%AD%BE)配置，其中用于标识**应用首页**的skill（即配置了"entity.system.home"和"ohos.want.action.home"的skill）中**不要配置uris，否则消息会接收不到**。
    
    注意
    
    module.json5文件中的skills标签下可以同时存在多个skill对象，每个对象对应一种能力。
    
    若您需要同时设置推送消息跳转能力和其他跳转能力（如NFC跳转、浏览器跳转等），需要在skills数组中创建不同的skill对象，分别映射对应的能力。
    
    点击消息进入应用首页skills标签配置示例：
    
    1. {
    2.   "module": {
    3.     // ...
    4.     "abilities": [
    5.       {
    6.         "name": "TestAbility",
    7.         "srcEntry": "./ets/abilities/TestAbility.ets",
    8.         "exported": false,
    9.         "startWindowIcon": "$media:startIcon",
    10.         "startWindowBackground": "$color:start_window_background",
    11.         "skills": [
    12.           // 该skill标识应用首页，不要配置uris
    13.           {
    14.             "entities": [
    15.               "entity.system.home"
    16.             ],
    17.             "actions": [
    18.               // "action.system.home"为API19以下版本配置，已废弃
    19.               "ohos.want.action.home"
    20.             ]
    21.           },
    22.           // 其他skill配置
    23.           {}
    24.         ]
    25.       }
    26.     ]
    27.   }
    28. }
    
2. 发送消息时设置**actionType**字段为0。
    
    1. // Request URL
    2. POST "https://push-api.cloud.huawei.com/v3/**[projectId]**/messages:send"
    
    3. // Request Header
    4. Content-Type: application/json
    5. Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
    6. **push-type: 0**
    
    7. // Request Body
    8. {
    9.   "payload": {
    10.     **"notification": {**
    11.       "category": "MARKETING",
    12.       "title": "普通通知标题",
    13.       "body": "普通通知内容",
    14.       **"clickAction": {**
    15.         **"actionType": 0,**
    16.         **"data": {"testKey": "testValue"}**
    17.       **}**
    18.     **}**
    19.   },
    20.   "target": {
    21.     "token": ["MAMzLg**********lPW"]
    22.   },
    23.   "pushOptions": {
    24.     "testMessage": true
    25.   }
    26. }
    
    - actionType：点击消息的动作，0表示点击消息后进入首页（即入口Ability当前所在页面，入口Ability通常为EntryAbility）。
        
        说明
        
        场景化消息[请求体](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct)中，接口URL版本为V3（https://push-api.cloud.huawei.com/v3/[projectId]/messages:send）时，仅支持给HarmonyOS Next/5.x及之后的系统版本推送通知；接口URL版本为V2（https://push-api.cloud.huawei.com/v2/[projectId]/messages:send）时，仅支持给HarmonyOS 3.x/4.x的系统版本推送通知。
        
    

### 点击消息进入应用内页

1. 在您的项目模块级别下的**src/main/module.json5** 中设置目标Ability中[skills标签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#skills%E6%A0%87%E7%AD%BE)的actions或uris值，两种方式如下：
    
    方式一：在[skills标签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#skills%E6%A0%87%E7%AD%BE)中新增一个**独立的skill****对象**，配置**actions参数**用于点击消息进入应用内页，示例如下：
    
    1. {
    2.   "name": "TestAbility",
    3.   "srcEntry": "./ets/abilities/TestAbility.ets",
    4.   "exported": false,
    5.   "startWindowIcon": "$media:startIcon",
    6.   "startWindowBackground": "$color:start_window_background",
    7.   "skills": [
    8.     // 保持现有skill对象不变
    9.     {
    10.       "actions": [
    11.         "com.app.action"
    12.       ]
    13.     },
    14.     // 新增一个独立的skill对象，配置actions参数
    15.     {
    16.       "actions": [
    17.         "com.test.action"
    18.       ]
    19.     }
    20.   ]
    21. }
    
    方式二：在[skills标签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#skills%E6%A0%87%E7%AD%BE)中新增一个**独立的skill****对象**，配置**uris参数**用于点击消息进入应用内页（**必须同时配置actions参数和uris参数，actions参数为空**），示例如下：
    
    22. {
    23.   "name": "TestAbility",
    24.   "srcEntry": "./ets/abilities/TestAbility.ets",
    25.   "exported": false,
    26.   "startWindowIcon": "$media:startIcon",
    27.   "startWindowBackground": "$color:start_window_background",
    28.   "skills": [
    29.     // 保持现有skill对象不变
    30.     {
    31.       "actions": [
    32.         "com.app.action"
    33.       ]
    34.     },
    35.     // 新增一个独立的skill对象，配置uris参数，且必须同时配置actions参数，actions参数为空字符串
    36.     {
    37.       "actions": [""],
    38.       "uris": [
    39.         {
    40.           "scheme": "https",
    41.           "host": "www.xxx.com",
    42.           "port": "8080",
    43.           "path": "push/test"
    44.         }
    45.       ]
    46.     }
    47.   ]
    48. }
    
    注意
    
    module.json5文件中的skills标签下可以同时存在多个skill对象，每个对象对应一种能力。
    
    若您需要同时设置推送消息跳转能力和其他跳转能力（如NFC跳转、浏览器跳转等），需要在skills数组中创建不同的skill对象，分别映射对应的能力。
    
2. 发送消息时[clickAction](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section152462191216)中设置**actionType**字段为1。
    
    1. // Request URL
    2. POST "https://push-api.cloud.huawei.com/v3/**[projectId]**/messages:send"
    
    3. // Request Header
    4. Content-Type: application/json
    5. Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
    6. **push-type: 0**
    
    7. // Request Body
    8. {
    9.   "payload": {
    10.     **"notification": {**
    11.       "category": "MARKETING",
    12.       "title": "普通通知标题",
    13.       "body": "普通通知内容",
    14.       **"clickAction": {**
    15.         **"actionType": 1,**
    16.         **"action": "com.test.action",**
    17.         **"uri": "https://www.xxx.com:8080/push/test",**
    18.         **"data": {"testKey": "testValue"}**
    19.       **}**
    20.     **}**
    21.   },
    22.   "target": {
    23.     "token": ["MAMzLg**********lPW"]
    24.   },
    25.   "pushOptions": {
    26.     "testMessage": true
    27.   }
    28. }
    
    - actionType：点击消息动作，1表示点击消息后进入应用内页。当本字段设置为1时，uri和action至少填写一个，若都填写优先寻找与action匹配的应用页面。若action和uri都未匹配到应用页面，则点击消息后会进入应用首页。
    - action：表示能够接收[Want](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-ability-want)的action值的集合，取值可以自定义。
    - uri：表示与[Want](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-ability-want)中uris相匹配的集合，uris规则请参见[skills标签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#skills%E6%A0%87%E7%AD%BE)。
    
    说明
    
    - 场景化消息[请求体](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct)中，接口URL版本为V3（https://push-api.cloud.huawei.com/v3/[projectId]/messages:send）时，仅支持给HarmonyOS Next/5.x及之后的系统版本推送通知；接口URL版本为V2（https://push-api.cloud.huawei.com/v2/[projectId]/messages:send）时，仅支持给HarmonyOS 3.x/4.x的系统版本推送通知。
    
    - 若action和uri都未匹配成功，则点击消息后会进入应用首页。
    

### 数据传递

应用服务端调用Push Kit服务端的REST API推送通知消息时，可携带**data**字段，当用户点击消息时将传递数据至客户端应用。

1. 调用REST API推送通知消息，消息体中[clickAction](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section152462191216)携带**data**字段。
    
    1. {
    2.   "payload": {
    3.     **"notification": {**
    4.       "category": "MARKETING",
    5.       "title": "普通通知标题",
    6.       "body": "普通通知内容",
    7.       **"clickAction": {**
    8.         **"actionType": 0,**
    9.         **"data": {"testKey": "testValue"}** // 携带**data**字段
    10.       **}**
    11.     **}**
    12.   },
    13.   "target": {
    14.     "token": ["MAMzLg**********lPW"]
    15.   },
    16.   "pushOptions": {
    17.     "testMessage": true
    18.   }
    19. }
    
    - data：点击消息时携带的JSON格式的数据。
    
2. 在待跳转页面（以TestAbility为例）中的[onCreate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#oncreate)()方法中覆写如下代码（[冷启动](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uiability-intra-device-interaction#%E7%9B%AE%E6%A0%87uiability%E5%86%B7%E5%90%AF%E5%8A%A8)时进入该生命周期回调）：
    
    1. // 文件路径: src/main/ets/abilities/TestAbility.ets
    2. import { UIAbility, Want } from '@kit.AbilityKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    4. export default class TestAbility extends UIAbility {
    5.   onCreate(want: Want): void {
    6.     // 获取消息中传递的data数据
    7.     const data = want.parameters;
    8.     const value = want.parameters?.["testKey"]; // value: "testValue"
    9.     hilog.info(0x0000, 'testTag', 'Succeeded in getting message data, value is %{public}s', value);
    10.     // 根据实际业务场景对data进行处理
    11.   }
    12. }
    
    [onNewWant](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#onnewwant)()方法中覆写如下代码（[热启动](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uiability-intra-device-interaction#%E7%9B%AE%E6%A0%87uiability%E7%83%AD%E5%90%AF%E5%8A%A8)时进入该生命周期回调）：
    
    13. // 文件路径: src/main/ets/abilities/TestAbility.ets
    14. import { UIAbility, Want } from '@kit.AbilityKit';
    15. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    16. export default class TestAbility extends UIAbility {
    17.   onNewWant(want: Want): void {
    18.     // 获取消息中传递的data数据
    19.     const data = want.parameters;
    20.     const value = want.parameters?.["testKey"]; // value: "testValue"
    21.     hilog.info(0x0000, 'testTag', 'Succeeded in getting message data, value is %{public}s', value);
    22.     // 根据实际业务场景对data进行处理
    23.   }
    24. }
    
    注意
    
    onNewWant()方法仅在单例（singleton）模式下可用。
    

## 设置通知消息样式

Push Kit提供了多种通知消息样式，您可以自定义其中内容来吸引用户，从而提高应用的日活跃用户数量。

### 普通通知

您在发送通知消息时[notification](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)参数中必须携带**title**与**body**字段，来设置应用收到通知消息后展示在通知中心的标题与内容。文本内容最多显示3行，超出3行以“...”截断。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163753.97488861369474747645851365491071:50001231000000:2800:6E7A83306C6DF6B98D5859AEC37FC72C1F47306D26D21954F2F27B9B35E2529A.png)

消息体示例：

1. {
2.   "payload": {
3.     "notification": {
4.       "category": "MARKETING",
5.       **"title": "推送服务",**
6.       **"body": "推送服务（Push Kit）是华为提供的消息推送平台，建立了从云端到终端的消息推送通道。您通过集成推送服务，可以向客户端应用实时推送消息，构筑良好的用户关系，提升用户的感知度和活跃度。",**
7.       "clickAction": {
8.         "actionType": 0
9.       }
10.     }
11.   },
12.   "target": {
13.     "token": ["MAMzLg**********lPW"]
14.   },
15.   "pushOptions": {
16.     "testMessage": true
17.   }
18. }

### 通知角标

说明

Wearable、TV不支持此通知样式。

您可以发送通知消息时携带[badge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section266310382145)字段来设置应用收到通知消息后以数字的形式展示角标，提醒用户查看消息。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163753.08787642609181446330735564638024:50001231000000:2800:3FAB3DFAFB5285C6EB10A210EA7DF2C0140DA455832F34BE4B2F83595AC36A43.png "点击放大")

消息体示例：

1. {
2.   "payload": {
3.     "notification": {
4.       "category": "MARKETING",
5.       "title": "通知标题",
6.       "body": "通知内容",
7.       **"badge":{**
8.         **"addNum": 1**,
9.         **"setNum": 99**
10.       **},**
11.       "clickAction": {
12.         "actionType": 0
13.       }
14.     }
15.   },
16.   "target": {
17.     "token": ["MAMzLg**********lPW"]
18.   },
19.   "pushOptions": {
20.     "testMessage": true
21.   }
22. }

说明

- addNum设置后为应用角标累加数字，非应用角标实际显示数字。
- setNum设置后为应用角标实际显示数字。setNum优先级高于addNum。
- 打开应用或者点击、清理通知消息并不会清理角标数字，开发者可通过[setBadgeNumber](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-notificationmanager#notificationmanagersetbadgenumber10)()方法清理角标，使用前需先[导入模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-notificationmanager#%E5%AF%BC%E5%85%A5%E6%A8%A1%E5%9D%97)。
- 当setBadgeNumber()方法中的badgeNumber设置为0时，可以实现清理效果。

### 通知大图标

说明

Wearable不支持此通知样式。

**推送服务禁止推送包含敏感信息的图片。**

您可以发送通知消息时携带[image](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)字段设置消息大图标内容，提醒用户查看消息。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163754.51388639842882614125526626579707:50001231000000:2800:FB4DB60B818DD5952C362D2D6C92C72586E5C305AD77AD09772D55CF581816CF.png)

消息体示例：

1. {
2.   "payload": {
3.     "notification": {
4.       "category": "MARKETING",
5.       "title": "推送服务",
6.       "body": "推送服务是华为提供的消息推送平台",
7.       **"image": "https://***.png"**, // 支持的图片格式为PNG、JPG、JPEG、BMP，图片长*宽建议小于128*128像素，若超过49152像素，则图片不展示。
8.       "clickAction": {
9.         "actionType": 0
10.       }
11.     }
12.   },
13.   "target": {
14.     "token": ["MAMzLg**********lPW"]
15.   },
16.   "pushOptions": {
17.     "testMessage": true
18.   }
19. }

### 多行文本样式

说明

Wearable不支持此通知样式。

您可以发送通知消息时在[notification](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)中携带**inboxContent**和**style**字段设置通知消息为多行文本样式。最多可展示3行内容，每行内容无法完全展示时以“...”截断。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163754.79329642283842091034116725017135:50001231000000:2800:F4C8EB0404653C34F6747BEB53E6830C3E10182F9BF411753C6BBAF940176634.png)

消息体示例：

1. {
2.   "payload": {
3.     "notification": {
4.       "category": "MARKETING",
5.       "title": "推送个性化显示",
6.       "body": "通知内容",
7.       **"style": 3,**
8.       **"inboxContent"****: [**
9.           **"1. 通知栏消息样式",** 
10.           **"2. 通知栏消息提醒方式和展示方式",** 
11.           **"3. 通知栏消息语言本地化"**
12.           **],**
13.       "clickAction": {
14.         "actionType": 0
15.       }
16.     }
17.   },
18.   "target": {
19.     "token": ["MAMzLg**********lPW"]
20.   },
21.   "pushOptions": {
22.     "testMessage": true
23.   }
24. }

说明

- 多行文本样式需要设置style字段为3。
- 当您发送多条通知消息导致用户通知消息折叠时，多行文本样式在展开前显示的标题与内容取自title与body字段。
- 当用户展开多行文本消息，或仅存在一条多行文本消息时，通知中显示的标题与内容取自title与inboxContent字段。

## 开发通知消息账号校验

Push Kit提供了账号校验功能，该功能支持您根据终端设备上不同账户属性来推送消息，将通知发送给对应设备上的对应账号。

举例：华为手机上某个应用存在账号A和账号B，若当前登录的账号A切换至账号B后，发送给账号A的通知消息在到达设备后不会进行展示，以避免账号B看到账号A的消息。

注意

- 当Push Token变更后，账号与应用的绑定关系自动解除。
- 绑定的应用内账号数量最大为10。

Push Kit支持华为账号和应用账号两种账号类型：

- **华为账号**
    
    该profileId为应用通过华为账号映射的唯一匿名标识。
    
    调用[bindAppProfileId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section20575105524912)()绑定接口时机：
    
    - 在应用内通过华为账号授权登录后。
    - 在应用内从其他账号切换到当前华为账号后。
    
    调用[unbindAppProfileId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section915174525214)()解绑接口时机：
    
    - 在应用内登出华为账号后。
    
    举例： 用户选择华为账号作为应用登录账号并登录账号A成功后，调用Push Kit绑定接口[bindAppProfileId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section20575105524912)()将账号A的profileId绑定到当前设备的应用token上。应用服务器发送通知消息时若携带该账号A的profileId，则只有当前登录的华为账号为账号A时，才会展示通知消息；若不携带profileId，则无论当前登录的华为账号是否为账号A，都正常展示通知消息。
    
- **应用账号**
    
    该profileId为应用通过自己的账号映射的唯一匿名标识。
    
    调用[bindAppProfileId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section20575105524912)()绑定接口时机：
    
    - 在应用内登录应用账号后。
    - 在应用内从其他应用账号切换到当前应用账号后。
    
    调用[unbindAppProfileId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section915174525214)()解绑接口时机：
    
    - 在应用内登出应用账号后。
    
    举例： 用户成功登录应用的账号A后，调用Push Kit绑定接口[bindAppProfileId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section20575105524912)()将账号A的profileId绑定到当前设备的应用token上。应用服务器发送通知消息时若携带账号A的profileId，则只有当前登录的应用账号为账号A时，才会展示通知消息；若不携带profileId，则无论当前登录的应用账号是否为账号A，都正常展示通知消息。
    

注意

若在账号登出时未做[unbindAppProfileId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section915174525214)()解绑，或者在账号切换时未做[bindAppProfileId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section20575105524912)()重新绑定，则会导致应用依然能接收到原账号的通知消息。

1. 参见指导[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)。
2. 为确保应用可正常收到通知消息，建议应用发送通知前调用[requestEnableNotification](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-notificationmanager#notificationmanagerrequestenablenotification10-1)()方法弹出提醒，告知用户需要允许接收通知消息。详情请参见Notification Kit-[请求通知授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-enable)。
3. 为待绑定的账号生成一个非空唯一的profileId（不建议使用真实的账号id，推荐使用账号id自行生成对应的匿名标识，能与该账号id建立唯一映射关系即可，生成算法无限制），调用[bindAppProfileId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section20575105524912)()方法，添加当前设备上该用户与应用的关系，代码示例：
    
    1. import { hilog } from '@kit.PerformanceAnalysisKit';
    2. import { pushCommon, pushService } from '@kit.PushKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. // 定义需要绑定的profileId，建议使用账号id对应的匿名标识
    5. const profileId = '111***222';
    6. // 绑定应用账号
    7. pushService.bindAppProfileId(pushCommon.AppProfileType.PROFILE_TYPE_APPLICATION_ACCOUNT, profileId).then(() => {
    8.   hilog.info(0x0000, 'testTag', 'Succeeded in binding app profile id');
    9. }).catch((err: BusinessError) => {
    10.   hilog.error(0x0000, 'testTag', 'Failed to bind app profile id: %{public}d %{public}s', err.code, err.message);
    11. });
    
4. 建议您将Push Token和生成的profileId上报到应用服务端，便于应用服务端向终端推送消息。
5. 应用服务端调用REST API推送通知消息，通知消息示例如下：
    
    1. // Request URL
    2. POST "https://push-api.cloud.huawei.com/v3/**[projectId]**/messages:send"
    
    3. // Request Header
    4. Content-Type: application/json
    5. Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
    6. push-type: 0
    
    7. // Request Body
    8. {
    9.   "payload": {
    10.     **"notification": {**
    11.       "category": "MARKETING",
    12.       "title": "普通通知标题",
    13.       "body": "普通通知内容",
    14.       **"profileId": "111***222"**,
    15.       "clickAction": {
    16.         "actionType": 0
    17.       }
    18.     **}**
    19.   },
    20.   "target": {
    21.     "token": ["MAMzLg**********lPW"]
    22.   },
    23.   "pushOptions": {
    24.     "testMessage": true
    25.   }
    26. }
    
    - [projectId]：项目ID，登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”，在该页面获取。
    - Authorization：JWT格式字符串，可参见[Authorization](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct#section20573634202313)获取。
    - push-type：0表示通知消息场景。
    - actionType：0表示点击消息打开应用首页。
    - token：Push Token，可参见[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)获取。
    - profileId：应用内账号id匿名标识。详情请参见[profileId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)。
    
    消息发送成功后，Push Kit会先校验绑定账号时的[AppProfileType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushcommon#section411410371767)（华为账号或应用账号）：
    
    - 若绑定华为账号则先校验下发消息中携带的profileId和之前应用绑定的profileId是否一致，再校验当前登录的华为账号和绑定时登录的分布式账号是否一致，若全部满足则展示消息，否则不展示消息。
    - 若绑定应用账号则校验下发消息中携带的profileId和之前应用绑定的profileId是否一致，若满足则展示消息，否则不展示消息。
        
        说明
        
        场景化消息[请求体](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct)中，接口URL版本为V3（https://push-api.cloud.huawei.com/v3/[projectId]/messages:send）时，仅支持给HarmonyOS Next/5.x及之后的系统版本推送通知；接口URL版本为V2（https://push-api.cloud.huawei.com/v2/[projectId]/messages:send）时，仅支持给HarmonyOS 3.x/4.x的系统版本推送通知。
        
    

## 应用在前台时处理通知消息

为实现应用在后台时展示通知消息，在前台时只接收通知消息并自行完成业务处理，需要服务端和客户端协同配置，具体步骤可以参考以下：

1. 服务端调用REST API推送通知消息，消息体中携带[foregroundShow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)字段，并且**设置为false（默认为true，表示前后台都展示）**，则应用在前台时不会展示通知消息。
    
    1. {
    2.   "payload": {
    3.     **"notification": {**
    4.       "category": "MARKETING",
    5.       "title": "普通通知标题",
    6.       "body": "普通通知内容",
    7.       "clickAction": {
    8.         "actionType": 0
    9.       },
    10.       "foregroundShow": false  // 设置为false则应用在前台时不会展示通知消息
    11.     **}**
    12.   },
    13.   "target": {
    14.     "token": ["MAMzLg**********lPW"]
    15.   },
    16.   "pushOptions": {
    17.     "testMessage": true
    18.   }
    19. }
    
2. 在客户端项目模块的**src/main/module.json5**文件的对应Ability配置中（以PushMessageAbility为例），skills标签的actions属性内容配置为 **action.ohos.push.listener**（**项目中有且只能有一个ability定义该action**）。
    
    1. {
    2.   "name": "PushMessageAbility",
    3.   "srcEntry": "./ets/abilities/PushMessageAbility.ets",
    4.   "launchType": "singleton",
    5.   "startWindowIcon": "$media:startIcon",
    6.   "startWindowBackground": "$color:start_window_background",
    7.   "exported": false,
    8.   "skills": [
    9.     // 保持现有skill对象不变
    10.     {
    11.       "actions": [
    12.         "com.app.action"
    13.       ]
    14.     },
    15.     // 新增一个独立的skill对象，配置actions参数
    16.     {
    17.       "actions": [
    18.         **"action.ohos.push.listener"**
    19.       ]
    20.     }
    21.   ]
    22. }
    
3. 在客户端项目中，已经通过步骤2配置了actions属性内容的UIAbility类的onCreate()中（以PushMessageAbility为例），通过[receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)()方法传入[PushType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section5507492425)为"DEFAULT"获取通知消息，用于应用在前台时接收通知消息，示例代码如下：
    
    1. // 文件路径: src/main/ets/abilities/PushMessageAbility.ets
    2. import { UIAbility } from '@kit.AbilityKit';
    3. import { pushService } from '@kit.PushKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    5. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    6. /**
    7.  * 此处以PushMessageAbility为例，用于应用在前台时接收通知消息
    8.  */
    9. export default class PushMessageAbility extends UIAbility {
    10.   onCreate(): void {
    11.     try {
    12.       // receiveMessage中的参数固定为DEFAULT
    13.       pushService.receiveMessage('DEFAULT', this, (payload) => {
    14.         try {
    15.           // 获取服务端传递的数据
    16.           const data: string = payload.data;
    17.           // TODO：业务自行处理
    18.           hilog.info(0x0000, 'testTag', 'Succeeded in getting notification,data=%{public}s',
    19.             JSON.stringify(JSON.parse(data)?.notification));
    20.         } catch (e) {
    21.           let errRes: BusinessError = e as BusinessError;
    22.           hilog.error(0x0000, 'testTag', 'Failed to process data: %{public}d %{public}s',
    23.             errRes.code, errRes.message);
    24.         }
    25.       });
    26.     } catch (err) {
    27.       let e: BusinessError = err as BusinessError;
    28.       hilog.error(0x0000, 'testTag', 'Failed to get message: %{public}d %{public}s', e.code,
    29.         e.message);
    30.     }
    31.   }
    32. }
    

## 通知消息自定义铃声实现

当用户终端收到通知消息时，通知提示会播放系统默认通知铃声。如需实现自定义铃声功能（category取值为MARKETING不支持该功能）， 消息需要携带**[sound](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)**字段。此功能需要服务端和客户端协同配置，具体步骤可以参考以下：

1. 将自定义铃声文件放在**客户端**工程中/resources/rawfile路径下（例如设置为**alert.mp3**，对应本地的**/resources/rawfile/alert.mp3**文件），重新编译安装应用程序包。
2. **服务端**调用REST API推送通知消息，消息体中携带**sound**字段。
    
    1. // Request URL
    2. POST "https://push-api.cloud.huawei.com/v3/**[projectId]**/messages:send"
    
    3. // Request Header
    4. Content-Type: application/json
    5. Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
    6. push-type: 0
    
    7. // Request Body
    8. {
    9.   "payload": {
    10.     "notification": {
    11.       "category": "TRAVEL", // 替换为实际消息类型
    12.       "title": "普通通知标题",
    13.       "body": "普通通知内容",
    14.       "clickAction": {
    15.         "actionType": 0
    16.       },
    17.       "notifyId": 12345,
    18.       "sound": "alert.mp3",  // category取值为MARKETING时，不支持该功能
    19.       "soundDuration": 10  // 请求同时携带sound字段时才会生效
    20.     }
    21.   },
    22.   "target": {
    23.     "token": ["MAMzLg**********lPW"]
    24.   },
    25.   "pushOptions": {
    26.    "testMessage": true,
    27.     "ttl": 86400
    28.   }
    29. }
    
    - sound：（选填）自定义消息通知铃声。此处设置的铃声文件必须放在应用的/resources/rawfile路径下。例如设置为**alert.mp3**，对应应用本地的**/resources/rawfile/alert.mp3**文件。详情请见[sound](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)。category取值为MARKETING时，不支持该功能。
    - soundDuration：（选填）自定义消息通知铃声时长，仅支持数字，单位为秒，取值范围 [1, 60]，在请求同时携带**sound字段**时才会生效。sound字段传入的自定义消息通知铃声会播放至soundDuration字段值后停止，若自定义消息通知铃声对应的时长不足soundDuration字段值则会循环播放，在达到soundDuration字段值后停止。详情请参见[soundDuration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-alert "推送通知消息")
# 撤回通知消息

更新时间: 2025-12-16 16:38

当推送的通知消息内容有误或者存在违规情况时，可能会引起用户投诉或监管部门处罚等不良后果。Push Kit为您提供消息撤回功能，降低此类推送可能造成的影响。

说明

- 消息撤回仅支持使用token和notifyId撤回。
- 若要使用消息撤回功能，请确保您在推送消息时设置了notifyId字段。
- 消息撤回仅支持以下类型：还未下发到端侧的消息，已在终端展示但用户还未点击的消息。
- 消息撤回不会影响应用的通知角标。

## 约束与限制

撤回通知消息能力支持Phone、Tablet、PC/2in1设备。并且从5.1.0(18)版本开始新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 开发步骤

1. 参考[开发步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section17790171616598)章节进行消息推送，确保应用可正常收到通知消息。
2. 应用服务端调用REST API撤回通知消息，消息详情可参见[消息撤回](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-revoke)，请求示例如下：
    
    1. // Request URL 
    2. POST "https://push-api.cloud.huawei.com/v1/**[clientId]**/messages:revoke"
    
    3. // Request Header 
    4. Content-Type:application/json
    5. Authorization:Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
    6. **push-type: 0** 
    
    7. // Request Body 
    8. {
    9.   "notifyId": 1234567,
    10.   "token": [
    11.     "pushToken1",
    12.     "pushToken2",
    13.     "pushToken3"
    14.   ]
    15. }
    
    - [clientId]：请替换为您应用的Client ID，可参见[指导](https://developer.huawei.com/consumer/cn/doc/app/agc-help-view-app-info-0000002282674569)获取。
    - Authorization：JWT格式字符串，可参见[Authorization](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-revoke#section7551144075816)获取。
    - push-type：0表示通知消息场景。
    - notifyId：消息ID，消息的唯一标识，详情请参见[notifyId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-revoke#section166472121113)。
    - token：Push Token，可参见[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)获取。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert "发送通知消息")
# 推送卡片刷新消息

更新时间: 2025-12-16 16:36

## 场景介绍

如今衣食住行娱乐影音应用占据了大多数人的手机，一部手机可以满足日常大多需求，但对需要经常查看或进行简单操作的应用来说，总需要用户点开应用体验较繁琐。针对此种场景，HarmonyOS提供了[Form Kit（卡片开发服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/form-kit)，您可以将应用的重要信息或操作前置到卡片，以达到服务直达、减少体验层级的目的。

面对需要实时更新信息的应用卡片，Push Kit向开发者提供了卡片刷新服务。应用通过集成Push Kit后获取Push Token，基于Push Kit的系统级通道，便可以在合适场景向用户即时推送卡片内容，从而提升用户的感知度和活跃度。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163653.80451263964415676623533569834011:50001231000000:2800:24A989061168D003960295CCCBD42CB1A881ED7B2474C0B2B33C484074CE9C33.png "点击放大")

说明

推送卡片刷新消息仅支持Phone、Tablet、PC/2in1设备。

## 频控规则

**调测阶段**，每个项目每日全网最多可推送1000条测试消息。发送测试消息需设置[testMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)为true。

**正式发布阶段**，单设备单应用下每日推送消息总条数受[设备消息频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control#section993063213715)限制，系统会根据现网使用场景和流量进行管控，不合理的使用场景系统会进行频控。

单张服务卡片刷新消息受应用是否上架影响：

- 已上架：单设备单应用下单张卡片每日限制发送2条消息。
- 未上架：单设备单应用下单张卡片每日限制发送5条消息。

说明

不论是测试消息还是正式消息，卡片刷新消息单次发送仅能携带一个Token。

## 开发步骤

### 开发卡片

推送卡片刷新消息前，您需先完成本地卡片的开发。

1. 参见[创建一个ArkTS卡片](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-ui-widget-creation)，完成本地服务卡片的创建。
2. 在项目模块级别下的**src/main/resources/base/profile/form_config.json**中配置dataProxyEnabled字段为**true**，开启卡片代理刷新功能。
    
    1. {
    2.   "forms": [
    3.     {
    4.       "name": "widget",
    5.       "src": "./ets/widget/pages/WidgetCard.ets",
    6.       "uiSyntax": "arkts",
    7.       "window": {
    8.         "designWidth": 720,
    9.         "autoDesignWidth": true
    10.       },
    11.       "colorMode": "auto",
    12.       "isDefault": true,
    13.       "updateEnabled": true,
    14.       "updateDuration": 1,
    15.       "scheduledUpdateTime": "10:30",
    16.       "defaultDimension": "2*2",
    17.       "supportDimensions": ["2*2"],
    18.       **"dataProxyEnabled": true**
    19.     }
    20.   ]
    21. }
    
3. 在卡片生命周期管理文件（下以EntryFormAbility为例）的[onAddForm](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-form-formextensionability#formextensionabilityonaddform)()回调中获取**formId**，定义需要在卡片页面文件（下以WidgetCard为例）中和通过Push Kit要刷新的字段，如下以**text_key**和**image_key**为例。
    
    1. // 文件路径: src/main/ets/entryformability/EntryFormAbility.ets
    2. import { formBindingData, formInfo, FormExtensionAbility } from '@kit.FormKit';
    3. import { Want } from '@kit.AbilityKit';
    
    4. export default class EntryFormAbility extends FormExtensionAbility {
    5.   onAddForm(want: Want): formBindingData.FormBindingData {
    6.     // 获取formId
    7.     const formId = want.parameters![formInfo.FormParam.IDENTITY_KEY] as string;
    
    8.     // 定义需要在WidgetCard中刷新的字段
    9.     class CreateFormData {
    10.       formId: string = '';
    11.       text_key: string = '';
    12.       image_key: string = '';
    13.     }
    
    14.     const obj: CreateFormData = {
    15.       formId: formId,
    16.       text_key: '默认文本',
    17.       image_key: ''
    18.     }
    19.     const bindingData: formBindingData.FormBindingData = formBindingData.createFormBindingData(obj);
    
    20.     // 定义需要通过Push Kit代理刷新的字段，每个key均需要在上面bindingData中定义
    21.     const text_key: formBindingData.ProxyData = {
    22.       key: 'text_key',
    23.       subscriberId: formId
    24.     };
    25.     const image_key: formBindingData.ProxyData = {
    26.       key: 'image_key',
    27.       subscriberId: formId
    28.     };
    29.     bindingData.proxies = [text_key, image_key];
    30.     return bindingData;
    31.   }
    32. }
    
4. 卡片页面文件（ **下以src/main/ets/widget/pages/WidgetCard.ets为例**）中，创建**[LocalStorage](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-localstorage)**变量并与**[@Entry](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-create-custom-components#entry)**装饰器绑定，使用**[@LocalStorageProp](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-localstorage#localstorageprop)**装饰器创建key-value的变量。
    
    本文创建了formId、text和image三个变量，对应的key为**formId**、**text_key**和**image_key**，需要注意的是卡片页面布局中image对应的组件是Image图片组件，图片组件传递的变量必须以 **memory://** 开头。
    
    1. // 文件路径: src/main/ets/widget/pages/WidgetCard.ets
    2. // 定义页面级的UI状态存储LocalStorage
    3. const storage = new LocalStorage();
    
    4. // 绑定
    5. @Entry(storage)
    6. @Component
    7. struct WidgetCard {
    8.   @LocalStorageProp('formId') formId: string = '';
    9.   @LocalStorageProp('text_key') text: string = '';
    10.   @LocalStorageProp('image_key') image: string = '';
    
    11.   build() {
    12.     Flex({ direction: FlexDirection.Column }) {
    13.       Row() {
    14.         Text() {
    15.           // Span是Text组件的子组件，用于显示行内文本
    16.           Span('formID:')
    17.           Span(this.formId)
    18.         }
    19.         .fontSize(10)
    20.       }
    
    21.       Row() {
    22.         Text() {
    23.           Span('文本:')
    24.           Span(this.text)
    25.         }
    26.         .fontSize(10)
    27.       }
    
    28.       Row() {
    29.         if (this.image) {
    30.           Image('memory://' + this.image).height(80)
    31.         }
    32.       }
    33.     }
    34.     .padding(10)
    35.     .onClick(() => {
    36.       postCardAction(this, {
    37.         action: 'router',
    38.         abilityName: 'MainAbility', // 请配置为应用实际的abilityName
    39.       });
    40.     })
    41.   }
    42. }
    

### 推送卡片刷新消息

1. 参见指导[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)。
2. （可选）建议您将**formId**、**pushToken**等信息上报到应用服务端，用于向应用发送卡片刷新消息。
    
    1. // 以下为伪代码
    2. import { Want } from '@kit.AbilityKit';
    3. import { pushService } from '@kit.PushKit';
    4. import { hilog } from '@kit.PerformanceAnalysisKit';
    5. import { BusinessError } from '@kit.BasicServicesKit';
    6. import { formInfo } from '@kit.FormKit';
    
    7. async function saveFormInfo(want: Want): Promise<void> {
    8.   try {
    9.     const formId = want.parameters![formInfo.FormParam.IDENTITY_KEY] as string;
    10.     const moduleName = want.moduleName;
    11.     const abilityName = want.abilityName;
    12.     const formName = want.parameters![formInfo.FormParam.NAME_KEY] as string;
    13.     const pushToken: string = await pushService.getToken();
    
    14.     // 将formId, moduleName, abilityName, formName, pushToken 上报到应用服务端
    15.   } catch (err) {
    16.     let e: BusinessError = err as BusinessError;
    17.     hilog.error(0x0000, 'testTag', 'Failed to save form info: %{public}d %{public}s', e.code, e.message);
    18.   }
    19. }
    
3. 应用服务端调用REST API推送卡片刷新消息，消息详情可参见[场景化消息API接口功能介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-intro)，请求示例如下：
    
    1. // Request URL
    2. POST "https://push-api.cloud.huawei.com/v3/**[projectId]**/messages:send"
    
    3. // Request Header
    4. Content-Type: application/json
    5. Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---**** 
    6. **push-type: 1**
    
    7. // Request Body
    8. {
    9.     "payload": {
    10.     "moduleName": "entry",
    11.     "abilityName": "EntryFormAbility",
    12.     "formName": "widget",
    13.     "formId": 423434262,
    14.     "version": 123456,
    15.     "formData": {
    16.       "text_key": "刷新文本内容"
    17.     },
    18.     "images": [
    19.       {
    20.         "keyName": "image_key",
    21.         "url": "https://***.png"**,**
    22.         "require": 1
    23.       }
    24.     ]
    25.   },
    26.   "target": {
    27.     "token": [
    28.       "MAMzLg**********lPW"
    29.     ]
    30.   },
    31.   "pushOptions": {
    32.      "testMessage": true
    33.   }
    34. }
    
    - [projectId]：项目ID，登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”，在该页面获取。
    - Authorization：JWT格式字符串，可参见[Authorization](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct#section20573634202313)获取。
    - push-type：1表示服务卡片刷新场景。
    - moduleName：项目模块级别下的 **src/main/module.json5** 中的 **module** 标签下的**name**值。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163653.84601733084632199151503124957942:50001231000000:2800:E1F3F1EA0C4CABAB1EDB56FF065B37C2C47A795C718CFCAE47D02CDC8FDE3BC0.png "点击放大")
        
    - abilityName：项目模块级别下的**src/main/module.json5**中的**extensionAbilities**标签下的服务卡片的ability名称。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163653.04312550908680333566095843367638:50001231000000:2800:DA8609065846578303839EAACE5121A69099F0F5AC07A01DF87526EF16E902D4.png "点击放大")
        
    - formName：项目模块级别下的**src/main/resources/base/profile/form_config.json**中的**forms**标签下的服务卡片的名称。下图以卡片配置文件form_config为例：
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163653.18075421240348421439515919931501:50001231000000:2800:300C2C39720C4F0061BE196DF1956EBDA448494B1DD930568AF2E1A32897BC83.png "点击放大")
        
    - version：当前卡片刷新消息的版本号，新的卡片刷新消息的版本号需**大于**当前卡片刷新消息版本号，否则会刷新失败。详情参见[version](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section6471174713249)。
    - formId：服务卡片的实例ID，当卡片的[onAddForm](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-form-formextensionability#formextensionabilityonaddform)()方法被调用时（卡片使用方添加卡片至桌面）进行获取。最大值为**2^31-1**。
    - formData：填写待刷新服务卡片的业务数据，该数据来源于项目模块级别下的**src/main/ets/widget/pages/WidgetCard.ets**文件下的声明式范式组件名称。下图以卡片页面文件WidgetCard为例：
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163653.21204215293764292665739312265203:50001231000000:2800:ACAB6FBB6A6DAC065523255E4234ACA1242712F0DAFC2409845AAC3136CC5E7E.png "点击放大")
        
    - images：待刷新服务卡片业务数据中的图片数据，其中keyName为您服务卡片中图片控件的key值，url为图片的地址，下图以卡片页面文件**WidgetCard**为例：
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163653.61535768842231098401891125355104:50001231000000:2800:84EB2DD162B1D2128D4CCD6F6D5FE521FF355E0DB165342A25C961112729F07A.png "点击放大")
        
        注意
        
        推送服务禁止推送包含敏感信息的图片。
        
        支持图片的格式为PNG、JPG、JPEG，图片文件最大为512KB，图片长*宽<12800像素。
        
    - require：图片刷新策略控制，“0”表示如果图片下载失败，仅刷新文字；“1”表示如果图片下载失败，则不进行刷新操作。
    - token：Push Token，可参见[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)获取。
    - testMessage：（选填）测试消息标识，true表示测试消息。每个项目每天限制发送1000条测试消息，单次推送仅能发送一个Token。详情请参见[testMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-revoke-alert "撤回通知消息")
# 撤回通知扩展消息

更新时间: 2025-12-16 16:38

## 场景介绍

当推送的通知扩展消息内容有误或者存在违规情况时，可能会引起用户投诉或监管部门处罚等不良后果。Push Kit为您提供消息撤回功能，降低此类推送可能造成的影响。

说明

- 消息撤回当前仅支持使用Token和notifyId撤回。
- 若要使用消息撤回功能，请确保您在推送通知扩展消息时设置了notifyId字段。
- 消息撤回仅支持以下类型：还未下发到端侧的消息，已在终端展示但用户还未点击的消息。

## 约束与限制

撤回通知扩展消息能力支持Phone、Tablet、PC/2in1。并且从5.1.0(18)版本开始新增支持Wearable设备。

## 开发步骤

1. 参考[发送通知扩展消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-extend-noti)章节进行消息推送，确保应用可正常收到通知扩展消息。
2. 应用服务端调用REST API撤回通知消息，消息详情可参见[消息撤回](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-revoke)，请求示例如下：
    
    1. // Request URL 
    2. POST "https://push-api.cloud.huawei.com/v1/**[clientId]**/messages:revoke"
    
    3. // Request Header 
    4. Content-Type:application/json
    5. Authorization:Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
    6. **push-type: 2** 
    
    7. // Request Body 
    8. {
    9.   "notifyId": 1234567,
    10.   "token": [
    11.     "pushToken1",
    12.     "pushToken2",
    13.     "pushToken3"
    14.   ]
    15. }
    
    - [clientId]：请替换为您应用的Client ID，可参见[指导](https://developer.huawei.com/consumer/cn/doc/app/agc-help-view-app-info-0000002282674569)获取。
    - Authorization：JWT格式字符串，可参见[Authorization](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-revoke#section7551144075816)获取。
    - push-type：2表示通知扩展消息场景。
    - notifyId：消息ID，消息的唯一标识，详情请参见[notifyId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-revoke#section166472121113)。
    - token：Push Token，可参见[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)获取。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-extend-noti "发送通知扩展消息")
# 推送后台消息

更新时间: 2025-12-16 16:37

## 场景介绍

后台消息用于内容不频繁更新的场景，不会显示通知、播放铃声或改变应用角标。终端设备接收到后台消息后，如果应用进程在前台则将消息内容传给应用；如果应用进程不在前台则缓存消息，等待应用启动后再传给应用。

说明

终端缓存消息默认仅缓存最新的一条消息，最多缓存7天。

## 约束与限制

推送后台消息能力支持Phone、Tablet、PC/2in1。并且从5.1.0(18)版本开始新增支持Wearable设备。从5.1.1(19)版本开始，新增支持TV设备。

## 频控规则

**调测阶段**，每个项目每日全网最多可推送1000条测试消息。发送测试消息需设置[testMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)为true。

**正式发布阶段**，单设备单应用下每日推送消息总条数受[设备消息频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control#section993063213715)限制，系统会根据现网使用场景和流量进行管控，不合理的使用场景系统会进行频控。

注意

- 后台消息优先级较低，建议每小时不超过2条，否则消息可能会被丢弃。
- 后台消息推送会受设备电量状态、系统休眠、用户使用行为等影响，消息可能不会及时下发。

## 开发步骤

说明

开发者希望在应用进程不在前台时，可根据实际情况选择消息缓存的策略。

- 开发者仅需缓存终端侧的最新一条消息，可不执行步骤2~步骤4。
- 若开发者需缓存终端侧更多消息，可参考开发步骤2~步骤4开发适配端侧数据库并开启数据代理写入，Push Kit将后台消息写入数据库中，当您的应用进程在前台时，需要自行读取数据库中的消息。

1. 参见指导[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)。
2. （可选）应用客户端参见[指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/data-persistence-by-rdb-store)新建一个数据库（如**pushmessage.db**），并严格按照如下格式创建一张数据表（如**t_push_message**）。
    
    |字段名称|字段类型|说明|
    |:--|:--|:--|
    |id|INTEGER|自增主键。|
    |message_id|TEXT|消息id。|
    |push_type|TEXT|场景类型。|
    |message_action|INTEGER|消息动作。|
    |message|TEXT|消息内容，结构体如下：<br><br>1. {<br>2.   "data": "消息体中的extraData"<br>3. }|
    |field1|TEXT|扩展字段1|
    |field2|TEXT|扩展字段2|
    |field3|TEXT|扩展字段3|
    |field4|TEXT|扩展字段4|
    |field5|TEXT|扩展字段5|
    |create_time|INTEGER|消息写入数据库的时间戳，单位毫秒（ms）。|
    
3. （可选）在项目模块级目录的 src/main/resources/base/profile/ 下创建 **PushMessage.json** 文件，文件内容如下：
    
    1. {
    2.   "path": "pushmessage/t_push_message",
    3.   "type": "rdb",
    4.   "scope": "application"
    5. }
    
    - path：值为步骤2中创建的数据表路径，格式为**[数据库名称]/[数据表名称]**（如pushmessage/t_push_message）。
    - type：固定值为 **rdb**，表示关系型数据库。
    - scope：表示数据库的范围，可填 **application**（应用级）或**module**（hap模块级）。
    
4. （可选）在项目模块级目录的 src/main/module.json5 文件添加 **proxyData** 如下配置：
    
    1. {
    2.   "module": {
    3.     "proxyData":[{
    4.       "uri": "datashareproxy://{bundleName}/PushMessage",
    5.       "requiredWritePermission": "ohos.permission.WRITE_PRIVACY_PUSH_DATA",
    6.       "metadata":{
    7.         "name": "dataProperties",
    8.         "resource": "$profile:PushMessage"
    9.       }
    10.     }]
    11.   }
    12. }
    
    - uri：固定格式为 datashareproxy://{bundleName}/PushMessage，请将**{bundleName}**替换为您应用的bundleName，PushMessage为固定名称，请勿随意更改。
    - requiredWritePermission：固定值为 **ohos.permission.WRITE_PRIVACY_PUSH_DATA**，推送服务需要使用该权限往数据库里写入后台消息数据。
    - metadata：扩展配置，name固定值为**dataProperties**，resource固定格式为**$profile:文件名称**，文件名称固定为**PushMessage**。
    
5. 在项目中现有的UIAbility类（以PushMessageAbility为例）的onCreate()中，调用[receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)()方法接收后台消息。注意，您仅能使用UIAbility接收后台消息。
    
    1. // 文件路径: src/main/ets/abilities/PushMessageAbility.ets
    2. import { UIAbility } from '@kit.AbilityKit';
    3. import { pushService, pushCommon } from '@kit.PushKit';
    4. import { hilog } from '@kit.PerformanceAnalysisKit';
    5. import { BusinessError } from '@kit.BasicServicesKit';
    
    6. /**
    7.  * 此处以PushMessageAbility为例，接收后台消息内容
    8.  */
    9. export default class PushMessageAbility extends UIAbility {
    10.   onCreate(): void {
    11.     try {
    12.       pushService.receiveMessage('BACKGROUND', this, (data: pushCommon.PushPayload) => {
    13.         // process message，并建议对Callback进行try-catch
    14.         try {
    15.           hilog.info(0x0000, 'testTag', 'Receive background message');
    16.         } catch (e) {
    17.           let errRes: BusinessError = e as BusinessError;
    18.           hilog.error(0x0000, 'testTag', 'Failed to process data: %{public}d %{public}s', errRes.code, errRes.message);
    19.         }
    20.       });
    21.     } catch (err) {
    22.       let e: BusinessError = err as BusinessError;
    23.       hilog.error(0x0000, 'testTag', 'Failed to get background message: %{public}d %{public}s', e.code, e.message);
    24.     }
    25.   }
    26. }
    
6. 在项目工程的 src/main/module.json5文件的abilities模块的**skills**标签中配置**actions**内容为**action.ohos.push.listener**（有且只能有一个ability定义该action，**若同时添加uris参数，则uris内容需为空**）。
    
    1. "abilities": [
    2.   {
    3.     "name": "PushMessageAbility",
    4.     "srcEntry": "./ets/abilities/PushMessageAbility.ets",
    5.     "launchType": "singleton",
    6.     "startWindowIcon": "$media:startIcon",
    7.     "startWindowBackground": "$color:start_window_background",
    8.     "exported": false,
    9.     "skills": [
    10.       // 保持现有skill对象不变
    11.       {
    12.         "actions": [
    13.           "com.app.action"
    14.         ]
    15.       },
    16.       // 新增一个独立的skill对象，配置actions参数
    17.       {
    18.         "actions": [
    19.           "action.ohos.push.listener"
    20.         ]
    21.       }
    22.     ]
    23.   }
    24. ]
    
7. 应用服务端调用REST API推送后台消息，消息详情可参见[场景化消息API接口功能介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-intro)，请求示例如下：
    
    1. // Request URL
    2. POST "https://push-api.cloud.huawei.com/v3/**[projectId]**/messages:send"
    
    3. // Request Header
    4. Content-Type: application/json
    5. Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
    6. **push-type: 6**
    
    7. // Request Body
    8. {
    9.   "payload": {
    10.     "extraData": "携带的额外数据",
    11.     "proxyData": "ENABLE"
    12.   },
    13.   "target": {
    14.     "token": ["MAMzLg**********lPW"]
    15.   }
    16. }
    
    - [projectId]：项目ID，登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”，在该页面获取。
    - Authorization：JWT格式字符串，可参见[Authorization](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct#section20573634202313)获取。
    - push-type：6表示后台消息场景。
    - token：Push Token，可参见[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)获取。
    - extraData：携带的额外数据，字符串类型。详情请参见[extraData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section056120245274)。
    - proxyData（选填）：进程不存在时是否开启数据代理静默写入到应用自身缓存，当前只能传全大写"ENABLE"开启代理。若您不希望开启代理写入，请不要在消息体中填写此字段。详情请参见[proxyData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section056120245274)。
    
    当设备中的应用进程在前台时会直接拉起应用并将数据传递，您可以在[receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)()方法中获取消息数据。
    
    当应用进程不在前台且[proxyData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section056120245274)为“ENABLE”时，推送服务将后台消息写入到数据库中，建议您在应用进程在前台时将数据库中数据迁移到您业务数据库中（**避免数据库大小无限制增长**）。当应用进程不在前台且无[proxyData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section056120245274)时则为缓存消息（**发送多条消息时仅缓存最新的一条**），等下次应用进程在前台时调用[getToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section562973524818)()接口，Push Kit将重新发送缓存消息，您可以在[receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)()方法获取消息数据。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-revoke-extend-noti "撤回通知扩展消息")
# 推送后台消息

更新时间: 2025-12-16 16:37

## 场景介绍

后台消息用于内容不频繁更新的场景，不会显示通知、播放铃声或改变应用角标。终端设备接收到后台消息后，如果应用进程在前台则将消息内容传给应用；如果应用进程不在前台则缓存消息，等待应用启动后再传给应用。

说明

终端缓存消息默认仅缓存最新的一条消息，最多缓存7天。

## 约束与限制

推送后台消息能力支持Phone、Tablet、PC/2in1。并且从5.1.0(18)版本开始新增支持Wearable设备。从5.1.1(19)版本开始，新增支持TV设备。

## 频控规则

**调测阶段**，每个项目每日全网最多可推送1000条测试消息。发送测试消息需设置[testMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)为true。

**正式发布阶段**，单设备单应用下每日推送消息总条数受[设备消息频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control#section993063213715)限制，系统会根据现网使用场景和流量进行管控，不合理的使用场景系统会进行频控。

注意

- 后台消息优先级较低，建议每小时不超过2条，否则消息可能会被丢弃。
- 后台消息推送会受设备电量状态、系统休眠、用户使用行为等影响，消息可能不会及时下发。

## 开发步骤

说明

开发者希望在应用进程不在前台时，可根据实际情况选择消息缓存的策略。

- 开发者仅需缓存终端侧的最新一条消息，可不执行步骤2~步骤4。
- 若开发者需缓存终端侧更多消息，可参考开发步骤2~步骤4开发适配端侧数据库并开启数据代理写入，Push Kit将后台消息写入数据库中，当您的应用进程在前台时，需要自行读取数据库中的消息。

1. 参见指导[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)。
2. （可选）应用客户端参见[指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/data-persistence-by-rdb-store)新建一个数据库（如**pushmessage.db**），并严格按照如下格式创建一张数据表（如**t_push_message**）。
    
    |字段名称|字段类型|说明|
    |:--|:--|:--|
    |id|INTEGER|自增主键。|
    |message_id|TEXT|消息id。|
    |push_type|TEXT|场景类型。|
    |message_action|INTEGER|消息动作。|
    |message|TEXT|消息内容，结构体如下：<br><br>1. {<br>2.   "data": "消息体中的extraData"<br>3. }|
    |field1|TEXT|扩展字段1|
    |field2|TEXT|扩展字段2|
    |field3|TEXT|扩展字段3|
    |field4|TEXT|扩展字段4|
    |field5|TEXT|扩展字段5|
    |create_time|INTEGER|消息写入数据库的时间戳，单位毫秒（ms）。|
    
3. （可选）在项目模块级目录的 src/main/resources/base/profile/ 下创建 **PushMessage.json** 文件，文件内容如下：
    
    1. {
    2.   "path": "pushmessage/t_push_message",
    3.   "type": "rdb",
    4.   "scope": "application"
    5. }
    
    - path：值为步骤2中创建的数据表路径，格式为**[数据库名称]/[数据表名称]**（如pushmessage/t_push_message）。
    - type：固定值为 **rdb**，表示关系型数据库。
    - scope：表示数据库的范围，可填 **application**（应用级）或**module**（hap模块级）。
    
4. （可选）在项目模块级目录的 src/main/module.json5 文件添加 **proxyData** 如下配置：
    
    1. {
    2.   "module": {
    3.     "proxyData":[{
    4.       "uri": "datashareproxy://{bundleName}/PushMessage",
    5.       "requiredWritePermission": "ohos.permission.WRITE_PRIVACY_PUSH_DATA",
    6.       "metadata":{
    7.         "name": "dataProperties",
    8.         "resource": "$profile:PushMessage"
    9.       }
    10.     }]
    11.   }
    12. }
    
    - uri：固定格式为 datashareproxy://{bundleName}/PushMessage，请将**{bundleName}**替换为您应用的bundleName，PushMessage为固定名称，请勿随意更改。
    - requiredWritePermission：固定值为 **ohos.permission.WRITE_PRIVACY_PUSH_DATA**，推送服务需要使用该权限往数据库里写入后台消息数据。
    - metadata：扩展配置，name固定值为**dataProperties**，resource固定格式为**$profile:文件名称**，文件名称固定为**PushMessage**。
    
5. 在项目中现有的UIAbility类（以PushMessageAbility为例）的onCreate()中，调用[receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)()方法接收后台消息。注意，您仅能使用UIAbility接收后台消息。
    
    1. // 文件路径: src/main/ets/abilities/PushMessageAbility.ets
    2. import { UIAbility } from '@kit.AbilityKit';
    3. import { pushService, pushCommon } from '@kit.PushKit';
    4. import { hilog } from '@kit.PerformanceAnalysisKit';
    5. import { BusinessError } from '@kit.BasicServicesKit';
    
    6. /**
    7.  * 此处以PushMessageAbility为例，接收后台消息内容
    8.  */
    9. export default class PushMessageAbility extends UIAbility {
    10.   onCreate(): void {
    11.     try {
    12.       pushService.receiveMessage('BACKGROUND', this, (data: pushCommon.PushPayload) => {
    13.         // process message，并建议对Callback进行try-catch
    14.         try {
    15.           hilog.info(0x0000, 'testTag', 'Receive background message');
    16.         } catch (e) {
    17.           let errRes: BusinessError = e as BusinessError;
    18.           hilog.error(0x0000, 'testTag', 'Failed to process data: %{public}d %{public}s', errRes.code, errRes.message);
    19.         }
    20.       });
    21.     } catch (err) {
    22.       let e: BusinessError = err as BusinessError;
    23.       hilog.error(0x0000, 'testTag', 'Failed to get background message: %{public}d %{public}s', e.code, e.message);
    24.     }
    25.   }
    26. }
    
6. 在项目工程的 src/main/module.json5文件的abilities模块的**skills**标签中配置**actions**内容为**action.ohos.push.listener**（有且只能有一个ability定义该action，**若同时添加uris参数，则uris内容需为空**）。
    
    1. "abilities": [
    2.   {
    3.     "name": "PushMessageAbility",
    4.     "srcEntry": "./ets/abilities/PushMessageAbility.ets",
    5.     "launchType": "singleton",
    6.     "startWindowIcon": "$media:startIcon",
    7.     "startWindowBackground": "$color:start_window_background",
    8.     "exported": false,
    9.     "skills": [
    10.       // 保持现有skill对象不变
    11.       {
    12.         "actions": [
    13.           "com.app.action"
    14.         ]
    15.       },
    16.       // 新增一个独立的skill对象，配置actions参数
    17.       {
    18.         "actions": [
    19.           "action.ohos.push.listener"
    20.         ]
    21.       }
    22.     ]
    23.   }
    24. ]
    
7. 应用服务端调用REST API推送后台消息，消息详情可参见[场景化消息API接口功能介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-intro)，请求示例如下：
    
    1. // Request URL
    2. POST "https://push-api.cloud.huawei.com/v3/**[projectId]**/messages:send"
    
    3. // Request Header
    4. Content-Type: application/json
    5. Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
    6. **push-type: 6**
    
    7. // Request Body
    8. {
    9.   "payload": {
    10.     "extraData": "携带的额外数据",
    11.     "proxyData": "ENABLE"
    12.   },
    13.   "target": {
    14.     "token": ["MAMzLg**********lPW"]
    15.   }
    16. }
    
    - [projectId]：项目ID，登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”，在该页面获取。
    - Authorization：JWT格式字符串，可参见[Authorization](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct#section20573634202313)获取。
    - push-type：6表示后台消息场景。
    - token：Push Token，可参见[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)获取。
    - extraData：携带的额外数据，字符串类型。详情请参见[extraData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section056120245274)。
    - proxyData（选填）：进程不存在时是否开启数据代理静默写入到应用自身缓存，当前只能传全大写"ENABLE"开启代理。若您不希望开启代理写入，请不要在消息体中填写此字段。详情请参见[proxyData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section056120245274)。
    
    当设备中的应用进程在前台时会直接拉起应用并将数据传递，您可以在[receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)()方法中获取消息数据。
    
    当应用进程不在前台且[proxyData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section056120245274)为“ENABLE”时，推送服务将后台消息写入到数据库中，建议您在应用进程在前台时将数据库中数据迁移到您业务数据库中（**避免数据库大小无限制增长**）。当应用进程不在前台且无[proxyData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section056120245274)时则为缓存消息（**发送多条消息时仅缓存最新的一条**），等下次应用进程在前台时调用[getToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section562973524818)()接口，Push Kit将重新发送缓存消息，您可以在[receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)()方法获取消息数据。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-revoke-extend-noti "撤回通知扩展消息")
# 推送应用内通话消息

更新时间: 2025-12-16 16:37

## 场景介绍

应用内通话消息，支持应用实现网络音视频通话的能力。当终端处于锁屏或解锁两种不同状态时，Push Kit将分别进行以下处理：

- 终端处于锁屏状态时，可在锁屏上点击接听或拒绝按钮。锁屏状态下**只支持接听语音**。
- 终端处于解锁状态时，网络音视频通话呼叫消息显性展示于横幅，支持用户接听视频或语音。

接听视频时会拉起应用内的接听界面。接通后，可以正常挂断（主动挂断/被动挂断）应用内通话消息。

应用内通话消息样式可参考如下示例，真实样式请以实际效果为准：

|锁屏|来电横幅|
|:--|:--|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163738.95789268380557169745132586561808:50001231000000:2800:6359DF4338FFA9F86B5319771639375662903ED1A539E7203FB88E4A4941A635.png "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163738.84733605057743539692059526829988:50001231000000:2800:61C68595F43E0E34A273F7DAFB96F2CCFD486725B979D031105320B159121753.png "点击放大")|

说明

- 应用内通话消息的问题场景请参见[指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-7)。
- 应用内通话消息的pushOptions.[ttl](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)建议设置为**30~60秒**。

## 约束与限制

应用内通话消息当前仅支持Phone、Tablet机型。

## 开通权益

推送应用内通话消息需要申请场景化消息权益，请参见[申请推送应用内通话消息权益](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section7291115452410)。

## 频控规则

**调测阶段**，每个项目每日全网最多可推送1000条测试消息。发送测试消息需设置[testMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)为true。

**正式发布阶段**，单设备单应用下每日推送消息总条数受[设备消息频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control#section993063213715)限制，系统会根据现网使用场景和流量进行管控，不合理的使用场景系统会进行频控。

## 开发步骤

1. 参见指导[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)。
2. 在您的工程内创建一个UIAbility类型的组件，如VoIPUIAbility.ets（在项目工程的**src/main/ets/entryability**目录下），负责处理应用内通话消息的主流程，并完成[onCreate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#oncreate)()、[onWindowStageCreate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#onwindowstagecreate)()、[onDestroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#ondestroy)()方法的覆写，代码示例如下：
    
    // 文件路径: src/main/ets/entryability/VoIPUIAbility.ets
    import { UIAbility } from '@kit.AbilityKit';
    import { pushService } from '@kit.PushKit';
    import { window } from '@kit.ArkUI';
    import { hilog } from '@kit.PerformanceAnalysisKit';
    import { VoipCallService } from '../service/VoipCallService';
    import { BusinessError } from '@kit.BasicServicesKit';
    
    export default class VoIPUIAbility extends UIAbility {
      onCreate(): void {
        hilog.info(0x0000, 'testTag', `VoIPUIAbility onCreate`);
    
        try {
          pushService.receiveMessage('VoIP', this, async (data) => {
            // process message，并建议对Callback进行try-catch
            try {
              await VoipCallService.processVoIPMainMsg(data.data, this.context);
            } catch (error) {
              hilog.error(0x0000, 'testTag', 'Failed to process VoIP message: %{public}d %{public}s',
                error.code,
                error.message);
            }
          });
        } catch (e) {
          hilog.error(0x0000, 'testTag', `Failed to register VOIP, error: ${e.code}, ${e.message}.`);
        }
      }
    
      onWindowStageCreate(windowStage: window.WindowStage): void {
        hilog.info(0x0000, 'testTag', `VoIPUIAbility onWindowStageCreate`);
    
        windowStage.loadContent('pages/CalleePage').catch((err: BusinessError) => {
          hilog.error(0x0000, 'testTag', `Failed to load content, error: ${err.code}, ${err.message}.`);
        });
      }
    
      onDestroy(): void {
        hilog.info(0x0000, 'testTag', 'VoIPUIAbility onDestroy');
      }
    }
    
    VoipCallService.ets（在项目工程的**src/main/ets/service**目录下），处理应用内通话消息，代码示例如下：
    
    // 文件路径: src/main/ets/service/VoipCallService.ets
    import { voipCall } from '@kit.CallServiceKit';
    import { hilog } from '@kit.PerformanceAnalysisKit';
    import { common } from '@kit.AbilityKit';
    import { image } from '@kit.ImageKit';
    import { resourceManager } from '@kit.LocalizationKit';
    import { BusinessError } from '@kit.BasicServicesKit';
    
    export interface VoipScene {
      scene: string;
    }
    
    export interface Content {
      data: string;
      header: string;
      callId: string;
    }
    
    export class VoipCallService {
      private static callId: string | undefined;
    
      public static async processVoIPMainMsg(data: string,
        context: common.UIAbilityContext): Promise<void> {
        hilog.info(0x0000, 'testTag', `Process VoIP message: ${data}`);
    
        let content: Content = JSON.parse(data);
        let scene: VoipScene = JSON.parse(content.data);
        let callId: string = content.callId;
        if (!callId) {
          hilog.error(0x0000, 'testTag', `CallId is null`);
        }
        VoipCallService.callId = callId;
    
        try {
          // 注册voipCallUiEvent事件
          voipCall.on('voipCallUiEvent', async (event) => {
            hilog.info(0x0000, 'testTag', `Process voip call ui event: ${JSON.stringify(event)}.`);
    
            await VoipCallService.processVoipCallEvent(event.voipCallUiEvent);
          });
        } catch (err) {
          let e: BusinessError = err as BusinessError;
          hilog.error(0x0000, 'testTag', 'Failed to register event: %{public}d %{public}s', e.code, e.message);
        }
    
        const resourceMgr: resourceManager.ResourceManager = context.resourceManager;
        // example.png表示用户头像，取值为“/resources/rawfile”路径下的文件名
        let fileData: Uint8Array = new Uint8Array(0);
        try {
          fileData = await resourceMgr.getRawFileContent('example.png');
        } catch (e) {
          hilog.error(0x0000, 'testTag', 'Failed to get raw file: %{public}d %{public}s', e.code, e.message);
        }
        const buffer = fileData.buffer;
        const imageSource: image.ImageSource = image.createImageSource(buffer);
        const pixelMap: image.PixelMap = await imageSource.createPixelMap();
        if (pixelMap) {
          pixelMap.getImageInfo((err, imageInfo) => {
            if (imageInfo) {
              hilog.info(0x0000, 'testTag',
                `User profile imageInfo: ${imageInfo.size.width} * ${imageInfo.size.height}.`);
            }
          });
        }
    
        // 构造上报来电的参数。注意，voipCallType.scene为您自定义的场景类型字段，从云侧推送消息时，请注意与端侧取值保持一致
        let call: voipCall.VoipCallAttribute = {
          callId: callId,
          voipCallType: scene?.scene === 'video' ? voipCall.VoipCallType.VOIP_CALL_VIDEO :
          voipCall.VoipCallType.VOIP_CALL_VOICE,
          userName: 'push',
          userProfile: pixelMap,
          abilityName: 'VoIPUIAbility',
          voipCallState: voipCall.VoipCallState.VOIP_CALL_STATE_RINGING
        };
    
        try {
          // 上报来电
          let error = await voipCall.reportIncomingCall(call);
          hilog.info(0x0000, 'testTag', `ReportIncomingCall result: ${error}.`);
        } catch (err) {
          let e: BusinessError = err as BusinessError;
          hilog.error(0x0000, 'testTag', 'Failed to report incoming call: %{public}d %{public}s', e.code, e.message);
        }
    
        // ...应用播放振动和铃声
      }
    
      public static async processVoipCallEvent(event: voipCall.VoipCallUiEvent) {
        try {
          switch (event) {
            case voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_VOICE_ANSWER:
            case voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_VIDEO_ANSWER:
              // 立即向Call Service Kit上报answered状态
              await voipCall.reportCallStateChange(VoipCallService.callId,
                voipCall.VoipCallState.VOIP_CALL_STATE_ANSWERED);
    
              // ...在应用内完成接听
    
              // 应用内接听后，向Call Service Kit上报active状态
              await voipCall.reportCallStateChange(VoipCallService.callId,
                voipCall.VoipCallState.VOIP_CALL_STATE_ACTIVE);
              break;
            case voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_REJECT:
            case voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_HANGUP:
              // ...应用内完成挂断
    
              // 向Call Service Kit上报通话状态
              await voipCall.reportCallStateChange(VoipCallService.callId,
                voipCall.VoipCallState.VOIP_CALL_STATE_DISCONNECTED);
              break;
            default: {
              break;
            }
          }
        } catch (err) {
          let e: BusinessError = err as BusinessError;
          hilog.error(0x0000, 'testTag', 'Failed to report call state change: %{public}d %{public}s', e.code, e.message);
        }
      }
    
      public static close(): void {
        hilog.info(0x0000, 'testTag', `Close VoIP`);
    
        VoipCallService.processVoipCallEvent(voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_HANGUP);
        try {
          voipCall.off('voipCallUiEvent');
        } catch (err) {
          let e: BusinessError = err as BusinessError;
          hilog.error(0x0000, 'testTag', 'Failed to unregister event: %{public}d %{public}s', e.code, e.message);
        }
      }
    }
    
    注意
    
    需要在项目工程的src/main/resources/rawfile目录下添加example.png，表示来电时的用户头像。
    
    - UIAbility.onCreate是同步接口，不支持异步回调，需要在onCreate生命周期的入口，完成[pushService.receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)()注册，并且保证在注册前没有等待异步方法执行的调用。
    - 在[receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)()回调中接收应用内通话消息，建议应用提前和服务器建连，用户点击接听后可以立即进行通话，并调用[voipCall.on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section7587131203319)()接口注册监听通话状态回调。用户点击接听或者拒绝接听之后，系统会通过应用注册的事件监听通话状态回调结果。
    - 应用需要在10秒内调用[voipCall.reportIncomingCall](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section13177019143216)()接口上报通话来电状态，调用完成之后，系统会弹出应用内通话横幅通知。[voipCall.reportIncomingCall](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section13177019143216)()**接口入参中的callId需要使用receiveMessage()回调中的callId**。
    - 如果应用来电消息建立失败，需要调用[voipCall.reportIncomingCallError](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section155796451716)()通知来电消息建立失败。如果应用在前台，通过自己的网络连接接收到来电消息，调用[voipCall.reportIncomingCall](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section13177019143216)()接口上报了通话来电状态，后面才收到Push推送的应用内通话消息，在该消息处理中需要调用[voipCall.reportIncomingCallError](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section155796451716)()上报[应用线路忙](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section157617591167)。
    - 应用内通话主要有三种回调状态，分别为：接听状态、拒绝状态和挂断状态。
        - 在接听状态回调中，应用在建立连接成功之后，需要调用[voipCall.reportCallStateChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section491515915329)()接口上报通话激活状态。
        - 在拒绝接听状态回调中，应用断开和服务器的连接之后，需要调用[voipCall.reportCallStateChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section491515915329)()接口上报通话断开状态。
        - 在应用进行应用内通话的同时，若运营商来电，会弹出运营商来电接听界面，用户点击接听运营商来电之后，会回调应用内通话挂断状态，在回调方法中应用需要自行断开和服务器的连接，并调用[voipCall.reportCallStateChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section491515915329)()接口上报通话断开状态。
    - 有关应用内通话回调状态的更多信息，详情请参见[Call Service Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/call-introduction)。
    - 应用上报通话来电状态之后，可以调用[vibrator.startVibration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-vibrator#vibratorstartvibration9-1)触发振动，有关振动的更多详情，请参见[Sensor Service Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/sensorservice-kit-intro)。可以使用AVPlayer播放应用铃声，音频流建议设置为铃声，usage设置为STREAM_USAGE_RINGTONE，效果为开始响铃，播放的音乐会暂停播放。同时推荐使用AudioSession管理音频焦点，可以保证接听过程中、通话过程中都保持音频焦点，详情请参见[Audio Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/audio-kit-intro)。
    - 进行音视频通话时，若您的应用处于Overhead场景（设备发热严重或负载较重，Level=4），请降低码率和帧率，或关闭视频流降级为音频。相关说明请参见Basic Services Kit（基础服务）提供的接口[getLevel](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-systemload#systemloadgetlevel)()。
    
3. 在项目工程的 **src/main/ets/pages**目录添加：视频接听页面CalleePage.ets，代码示例如下：
    
    // 文件路径: src/main/ets/pages/CalleePage.ets
    import CallComponent from '../component/CallComponent';
    import { hilog } from '@kit.PerformanceAnalysisKit';
    
    @Entry
    @Component
    struct CalleePage {
      @StorageLink('close') @Watch('close') end: boolean | undefined = undefined;
    
      aboutToAppear() {
        hilog.info(0x0000, 'testTag', `CalleePage aboutToAppear`);
    
        this.end = false;
      }
    
      private close() {
        if (this.end) {
          hilog.info(0x0000, 'testTag', `CalleePage close`);
    
          this.getUIContext().getRouter().back(); // 此处仅为示例（跳转返回），请根据实际情况设定路由
        }
      }
    
      aboutToDisappear() {
        hilog.info(0x0000, 'testTag', `CalleePage aboutToDisappear`);
      }
    
      build() {
        Column() {
          CallComponent({})
        }
      }
    }
    
    CallComponent.ets（在项目工程的**src/main/ets/component**目录下），代码示例如下：
    
    // 文件路径: src/main/ets/component/CallComponent.ets
    import { VoipCallService } from '../service/VoipCallService';
    import { voipCall } from '@kit.CallServiceKit';
    
    @Component
    export default struct CallComponent {
      @StorageLink('close') end: boolean | undefined = undefined;
    
      build() {
        Flex({ direction: FlexDirection.Column, justifyContent: FlexAlign.SpaceBetween }) {
          Row() {
          }
          .width('100%')
          .justifyContent(FlexAlign.Center)
    
          Row({ space: 30 }) {
    
            Column() {
              Button()
                .width(80)
                .height(80)
                .backgroundColor(Color.Green)
                .onClick(() => {
                  VoipCallService.processVoipCallEvent(voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_VIDEO_ANSWER);
                })
    
              Text('Answer').fontColor(Color.White).padding({ top: 5 })
            }
    
            Column() {
              Button()
                .width(80)
                .height(80)
                .backgroundColor(Color.Red)
                .onClick(() => {
                  this.end = true;
                  VoipCallService.close();
                })
    
              Text('Hang Up').fontColor(Color.White).padding({ top: 5 })
            }
    
          }
          .width('100%')
          .justifyContent(FlexAlign.Center)
        }
        .padding('30 10')
        .backgroundColor(Color.Black)
      }
    }
    
    在项目工程的 src/main/resources/base/profile/main_pages.json添加page目录，示例如下：
    
    {
      "src": [
        "pages/Index",
        "pages/CalleePage"
      ]
    }
    
    注意
    
    示例代码提供的页面效果仅供开发参考，不代表最终效果。
    
4. 在项目工程的 **src/main/module.json5** 文件的 **abilities** 模块中配置VoIPUIAbility的**actions**信息。
    
    "abilities": [ 
      { 
        "name": "VoIPUIAbility", 
        "srcEntry": "./ets/entryability/VoIPUIAbility.ets", 
        "launchType": "singleton",
        "description": "VoIPUIAbility test", 
        "startWindowIcon": "$media:startIcon",
        "startWindowBackground": "$color:start_window_background",
        "exported": false, 
        "skills": [ 
          // 保持现有skill对象不变
          // 新增一个独立的skill对象，配置actions参数
          { 
            **"actions": ["action.ohos.push.listener"]**
          }
        ]
      } 
    ]
    
    - actions：内容为**action.ohos.push.listener**，有且只能有一个ability定义该action，**若同时添加uris参数，则uris内容需为空**。
    
5. 应用服务端调用REST API推送消息，消息详情可参见[场景化消息API接口功能介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-intro)。

### 应用内通话消息

1. 如果您需要呼叫，应用服务器可以调用REST API推送应用内通话消息，请求示例如下：
    
    // Request URL    
    POST "https://push-api.cloud.huawei.com/v3/[projectId]/messages:send"
    
    // Request Header   
    Content-Type: application/json   
    Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****   
    push-type: 10 
    
    // Request Body
    {   
      "pushOptions": { 
        "ttl": 30 
      }, 
      "payload": {   
        "extraData": "{\"scene\": \"voice\"}" 
      },   
      "target": {   
        "token": ["MAMzLg**********aZW"]   
      } 
    }
    
    - [projectId]：项目ID，登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”，在该页面获取。
    - Authorization：JWT格式字符串，可参见[基于服务账号生成鉴权令牌](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token)进行获取。
    - push-type：10表示应用内通话消息场景。
    - token：Push Token，可参见[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)章节获取。
    - extraData：携带的额外数据，字符串类型。详情参见[VoIPCallPayload 应用内通话消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section146341550144011)中extraData参数用法。extraData数据获取请参考[示例代码](https://gitcode.com/harmonyos_samples/push-kit-sample-code-clientdemo-arkts/blob/master/entry/src/main/ets/service/VoipCallService.ets)。
    - ttl：消息缓存时间，建议设置为30~60秒，详见pushOptions.[ttl](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)。
    

说明

- 应用内通话消息只能用于音视频通话场景唤醒应用，完成呼叫，不要通过此种类型消息来挂断来电或者和应用通信，应用应该使用自己建立的网络连接和应用通信。相比应用服务器推送Push消息，使用现有的网络连接和应用通信通常会更快，在网络不佳的情况下，推送的Push消息可能无法到达应用。
- 应用无论是否在前台，自己的网络连接存在时，建议您通过Push推送应用内通话消息，再通过自己的网络连接发送通话消息，保证该呼叫能够到达应用。

### 未接来电通知

1. 如果您需要给被叫方发送未接来电通知，应用服务器可以调用REST API推送[通知消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert)。以通知消息为例，请求示例如下：
    
    // Request URL    
    POST "https://push-api.cloud.huawei.com/v3/**[projectId]**/messages:send"
       
    // Request Header   
    Content-Type: application/json   
    Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****   
    **push-type: 0** 
       
    // Request Body
    {   
      "pushOptions": { 
        **"ttl":**86400
      }, 
      "payload": {   
        "notification": { 
          "category": "MISS_CALL",  
          "title": "通知标题", 
          "body": "通知内容", 
          "clickAction": { 
            "actionType": 0 
          },
          "appMessageId": "12345"
        }
       },   
       "target": {   
         "token": ["MAMzLg**********aZW"]   
       } 
     }
    
    - push-type：0表示通知消息场景。
    - category：消息自分类类别，设置为MISS_CALL，请参见[参数说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)，发送消息前请确保您已[申请通知消息自分类权益](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section16708911111611)。
    - appMessageId：应用消息的唯一标识。被叫挂断，被叫方VoIP应用在前台时应用可以通过调用[Notification Kit（用户通知服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-overview)发送未接来电通知。被叫方VoIP应用在后台时，可以通过Push推送未接来电通知。应用可能存在前后台状态判断不准确，同一电话会产生两条未接来电，建议您通过Notification Kit和Push Kit推送的未接来电通知使用相同的appMessageId，系统会进行通知去重。
    - 其他参数说明可参见[通知消息请求体参数说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section1152516418157)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-update-liveview "推送实况窗消息")
# 推送应用内通话消息

更新时间: 2025-12-16 16:37

## 场景介绍

应用内通话消息，支持应用实现网络音视频通话的能力。当终端处于锁屏或解锁两种不同状态时，Push Kit将分别进行以下处理：

- 终端处于锁屏状态时，可在锁屏上点击接听或拒绝按钮。锁屏状态下**只支持接听语音**。
- 终端处于解锁状态时，网络音视频通话呼叫消息显性展示于横幅，支持用户接听视频或语音。

接听视频时会拉起应用内的接听界面。接通后，可以正常挂断（主动挂断/被动挂断）应用内通话消息。

应用内通话消息样式可参考如下示例，真实样式请以实际效果为准：

|锁屏|来电横幅|
|:--|:--|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163738.95789268380557169745132586561808:50001231000000:2800:6359DF4338FFA9F86B5319771639375662903ED1A539E7203FB88E4A4941A635.png "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163738.84733605057743539692059526829988:50001231000000:2800:61C68595F43E0E34A273F7DAFB96F2CCFD486725B979D031105320B159121753.png "点击放大")|

说明

- 应用内通话消息的问题场景请参见[指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-7)。
- 应用内通话消息的pushOptions.[ttl](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)建议设置为**30~60秒**。

## 约束与限制

应用内通话消息当前仅支持Phone、Tablet机型。

## 开通权益

推送应用内通话消息需要申请场景化消息权益，请参见[申请推送应用内通话消息权益](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section7291115452410)。

## 频控规则

**调测阶段**，每个项目每日全网最多可推送1000条测试消息。发送测试消息需设置[testMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)为true。

**正式发布阶段**，单设备单应用下每日推送消息总条数受[设备消息频控](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control#section993063213715)限制，系统会根据现网使用场景和流量进行管控，不合理的使用场景系统会进行频控。

## 开发步骤

1. 参见指导[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)。
2. 在您的工程内创建一个UIAbility类型的组件，如VoIPUIAbility.ets（在项目工程的**src/main/ets/entryability**目录下），负责处理应用内通话消息的主流程，并完成[onCreate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#oncreate)()、[onWindowStageCreate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#onwindowstagecreate)()、[onDestroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#ondestroy)()方法的覆写，代码示例如下：
    
    // 文件路径: src/main/ets/entryability/VoIPUIAbility.ets
    import { UIAbility } from '@kit.AbilityKit';
    import { pushService } from '@kit.PushKit';
    import { window } from '@kit.ArkUI';
    import { hilog } from '@kit.PerformanceAnalysisKit';
    import { VoipCallService } from '../service/VoipCallService';
    import { BusinessError } from '@kit.BasicServicesKit';
    
    export default class VoIPUIAbility extends UIAbility {
      onCreate(): void {
        hilog.info(0x0000, 'testTag', `VoIPUIAbility onCreate`);
    
        try {
          pushService.receiveMessage('VoIP', this, async (data) => {
            // process message，并建议对Callback进行try-catch
            try {
              await VoipCallService.processVoIPMainMsg(data.data, this.context);
            } catch (error) {
              hilog.error(0x0000, 'testTag', 'Failed to process VoIP message: %{public}d %{public}s',
                error.code,
                error.message);
            }
          });
        } catch (e) {
          hilog.error(0x0000, 'testTag', `Failed to register VOIP, error: ${e.code}, ${e.message}.`);
        }
      }
    
      onWindowStageCreate(windowStage: window.WindowStage): void {
        hilog.info(0x0000, 'testTag', `VoIPUIAbility onWindowStageCreate`);
    
        windowStage.loadContent('pages/CalleePage').catch((err: BusinessError) => {
          hilog.error(0x0000, 'testTag', `Failed to load content, error: ${err.code}, ${err.message}.`);
        });
      }
    
      onDestroy(): void {
        hilog.info(0x0000, 'testTag', 'VoIPUIAbility onDestroy');
      }
    }
    
    VoipCallService.ets（在项目工程的**src/main/ets/service**目录下），处理应用内通话消息，代码示例如下：
    
    // 文件路径: src/main/ets/service/VoipCallService.ets
    import { voipCall } from '@kit.CallServiceKit';
    import { hilog } from '@kit.PerformanceAnalysisKit';
    import { common } from '@kit.AbilityKit';
    import { image } from '@kit.ImageKit';
    import { resourceManager } from '@kit.LocalizationKit';
    import { BusinessError } from '@kit.BasicServicesKit';
    
    export interface VoipScene {
      scene: string;
    }
    
    export interface Content {
      data: string;
      header: string;
      callId: string;
    }
    
    export class VoipCallService {
      private static callId: string | undefined;
    
      public static async processVoIPMainMsg(data: string,
        context: common.UIAbilityContext): Promise<void> {
        hilog.info(0x0000, 'testTag', `Process VoIP message: ${data}`);
    
        let content: Content = JSON.parse(data);
        let scene: VoipScene = JSON.parse(content.data);
        let callId: string = content.callId;
        if (!callId) {
          hilog.error(0x0000, 'testTag', `CallId is null`);
        }
        VoipCallService.callId = callId;
    
        try {
          // 注册voipCallUiEvent事件
          voipCall.on('voipCallUiEvent', async (event) => {
            hilog.info(0x0000, 'testTag', `Process voip call ui event: ${JSON.stringify(event)}.`);
    
            await VoipCallService.processVoipCallEvent(event.voipCallUiEvent);
          });
        } catch (err) {
          let e: BusinessError = err as BusinessError;
          hilog.error(0x0000, 'testTag', 'Failed to register event: %{public}d %{public}s', e.code, e.message);
        }
    
        const resourceMgr: resourceManager.ResourceManager = context.resourceManager;
        // example.png表示用户头像，取值为“/resources/rawfile”路径下的文件名
        let fileData: Uint8Array = new Uint8Array(0);
        try {
          fileData = await resourceMgr.getRawFileContent('example.png');
        } catch (e) {
          hilog.error(0x0000, 'testTag', 'Failed to get raw file: %{public}d %{public}s', e.code, e.message);
        }
        const buffer = fileData.buffer;
        const imageSource: image.ImageSource = image.createImageSource(buffer);
        const pixelMap: image.PixelMap = await imageSource.createPixelMap();
        if (pixelMap) {
          pixelMap.getImageInfo((err, imageInfo) => {
            if (imageInfo) {
              hilog.info(0x0000, 'testTag',
                `User profile imageInfo: ${imageInfo.size.width} * ${imageInfo.size.height}.`);
            }
          });
        }
    
        // 构造上报来电的参数。注意，voipCallType.scene为您自定义的场景类型字段，从云侧推送消息时，请注意与端侧取值保持一致
        let call: voipCall.VoipCallAttribute = {
          callId: callId,
          voipCallType: scene?.scene === 'video' ? voipCall.VoipCallType.VOIP_CALL_VIDEO :
          voipCall.VoipCallType.VOIP_CALL_VOICE,
          userName: 'push',
          userProfile: pixelMap,
          abilityName: 'VoIPUIAbility',
          voipCallState: voipCall.VoipCallState.VOIP_CALL_STATE_RINGING
        };
    
        try {
          // 上报来电
          let error = await voipCall.reportIncomingCall(call);
          hilog.info(0x0000, 'testTag', `ReportIncomingCall result: ${error}.`);
        } catch (err) {
          let e: BusinessError = err as BusinessError;
          hilog.error(0x0000, 'testTag', 'Failed to report incoming call: %{public}d %{public}s', e.code, e.message);
        }
    
        // ...应用播放振动和铃声
      }
    
      public static async processVoipCallEvent(event: voipCall.VoipCallUiEvent) {
        try {
          switch (event) {
            case voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_VOICE_ANSWER:
            case voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_VIDEO_ANSWER:
              // 立即向Call Service Kit上报answered状态
              await voipCall.reportCallStateChange(VoipCallService.callId,
                voipCall.VoipCallState.VOIP_CALL_STATE_ANSWERED);
    
              // ...在应用内完成接听
    
              // 应用内接听后，向Call Service Kit上报active状态
              await voipCall.reportCallStateChange(VoipCallService.callId,
                voipCall.VoipCallState.VOIP_CALL_STATE_ACTIVE);
              break;
            case voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_REJECT:
            case voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_HANGUP:
              // ...应用内完成挂断
    
              // 向Call Service Kit上报通话状态
              await voipCall.reportCallStateChange(VoipCallService.callId,
                voipCall.VoipCallState.VOIP_CALL_STATE_DISCONNECTED);
              break;
            default: {
              break;
            }
          }
        } catch (err) {
          let e: BusinessError = err as BusinessError;
          hilog.error(0x0000, 'testTag', 'Failed to report call state change: %{public}d %{public}s', e.code, e.message);
        }
      }
    
      public static close(): void {
        hilog.info(0x0000, 'testTag', `Close VoIP`);
    
        VoipCallService.processVoipCallEvent(voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_HANGUP);
        try {
          voipCall.off('voipCallUiEvent');
        } catch (err) {
          let e: BusinessError = err as BusinessError;
          hilog.error(0x0000, 'testTag', 'Failed to unregister event: %{public}d %{public}s', e.code, e.message);
        }
      }
    }
    
    注意
    
    需要在项目工程的src/main/resources/rawfile目录下添加example.png，表示来电时的用户头像。
    
    - UIAbility.onCreate是同步接口，不支持异步回调，需要在onCreate生命周期的入口，完成[pushService.receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)()注册，并且保证在注册前没有等待异步方法执行的调用。
    - 在[receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)()回调中接收应用内通话消息，建议应用提前和服务器建连，用户点击接听后可以立即进行通话，并调用[voipCall.on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section7587131203319)()接口注册监听通话状态回调。用户点击接听或者拒绝接听之后，系统会通过应用注册的事件监听通话状态回调结果。
    - 应用需要在10秒内调用[voipCall.reportIncomingCall](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section13177019143216)()接口上报通话来电状态，调用完成之后，系统会弹出应用内通话横幅通知。[voipCall.reportIncomingCall](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section13177019143216)()**接口入参中的callId需要使用receiveMessage()回调中的callId**。
    - 如果应用来电消息建立失败，需要调用[voipCall.reportIncomingCallError](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section155796451716)()通知来电消息建立失败。如果应用在前台，通过自己的网络连接接收到来电消息，调用[voipCall.reportIncomingCall](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section13177019143216)()接口上报了通话来电状态，后面才收到Push推送的应用内通话消息，在该消息处理中需要调用[voipCall.reportIncomingCallError](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section155796451716)()上报[应用线路忙](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section157617591167)。
    - 应用内通话主要有三种回调状态，分别为：接听状态、拒绝状态和挂断状态。
        - 在接听状态回调中，应用在建立连接成功之后，需要调用[voipCall.reportCallStateChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section491515915329)()接口上报通话激活状态。
        - 在拒绝接听状态回调中，应用断开和服务器的连接之后，需要调用[voipCall.reportCallStateChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section491515915329)()接口上报通话断开状态。
        - 在应用进行应用内通话的同时，若运营商来电，会弹出运营商来电接听界面，用户点击接听运营商来电之后，会回调应用内通话挂断状态，在回调方法中应用需要自行断开和服务器的连接，并调用[voipCall.reportCallStateChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section491515915329)()接口上报通话断开状态。
    - 有关应用内通话回调状态的更多信息，详情请参见[Call Service Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/call-introduction)。
    - 应用上报通话来电状态之后，可以调用[vibrator.startVibration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-vibrator#vibratorstartvibration9-1)触发振动，有关振动的更多详情，请参见[Sensor Service Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/sensorservice-kit-intro)。可以使用AVPlayer播放应用铃声，音频流建议设置为铃声，usage设置为STREAM_USAGE_RINGTONE，效果为开始响铃，播放的音乐会暂停播放。同时推荐使用AudioSession管理音频焦点，可以保证接听过程中、通话过程中都保持音频焦点，详情请参见[Audio Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/audio-kit-intro)。
    - 进行音视频通话时，若您的应用处于Overhead场景（设备发热严重或负载较重，Level=4），请降低码率和帧率，或关闭视频流降级为音频。相关说明请参见Basic Services Kit（基础服务）提供的接口[getLevel](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resourceschedule-systemload#systemloadgetlevel)()。
    
3. 在项目工程的 **src/main/ets/pages**目录添加：视频接听页面CalleePage.ets，代码示例如下：
    
    // 文件路径: src/main/ets/pages/CalleePage.ets
    import CallComponent from '../component/CallComponent';
    import { hilog } from '@kit.PerformanceAnalysisKit';
    
    @Entry
    @Component
    struct CalleePage {
      @StorageLink('close') @Watch('close') end: boolean | undefined = undefined;
    
      aboutToAppear() {
        hilog.info(0x0000, 'testTag', `CalleePage aboutToAppear`);
    
        this.end = false;
      }
    
      private close() {
        if (this.end) {
          hilog.info(0x0000, 'testTag', `CalleePage close`);
    
          this.getUIContext().getRouter().back(); // 此处仅为示例（跳转返回），请根据实际情况设定路由
        }
      }
    
      aboutToDisappear() {
        hilog.info(0x0000, 'testTag', `CalleePage aboutToDisappear`);
      }
    
      build() {
        Column() {
          CallComponent({})
        }
      }
    }
    
    CallComponent.ets（在项目工程的**src/main/ets/component**目录下），代码示例如下：
    
    // 文件路径: src/main/ets/component/CallComponent.ets
    import { VoipCallService } from '../service/VoipCallService';
    import { voipCall } from '@kit.CallServiceKit';
    
    @Component
    export default struct CallComponent {
      @StorageLink('close') end: boolean | undefined = undefined;
    
      build() {
        Flex({ direction: FlexDirection.Column, justifyContent: FlexAlign.SpaceBetween }) {
          Row() {
          }
          .width('100%')
          .justifyContent(FlexAlign.Center)
    
          Row({ space: 30 }) {
    
            Column() {
              Button()
                .width(80)
                .height(80)
                .backgroundColor(Color.Green)
                .onClick(() => {
                  VoipCallService.processVoipCallEvent(voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_VIDEO_ANSWER);
                })
    
              Text('Answer').fontColor(Color.White).padding({ top: 5 })
            }
    
            Column() {
              Button()
                .width(80)
                .height(80)
                .backgroundColor(Color.Red)
                .onClick(() => {
                  this.end = true;
                  VoipCallService.close();
                })
    
              Text('Hang Up').fontColor(Color.White).padding({ top: 5 })
            }
    
          }
          .width('100%')
          .justifyContent(FlexAlign.Center)
        }
        .padding('30 10')
        .backgroundColor(Color.Black)
      }
    }
    
    在项目工程的 src/main/resources/base/profile/main_pages.json添加page目录，示例如下：
    
    {
      "src": [
        "pages/Index",
        "pages/CalleePage"
      ]
    }
    
    注意
    
    示例代码提供的页面效果仅供开发参考，不代表最终效果。
    
4. 在项目工程的 **src/main/module.json5** 文件的 **abilities** 模块中配置VoIPUIAbility的**actions**信息。
    
    "abilities": [ 
      { 
        "name": "VoIPUIAbility", 
        "srcEntry": "./ets/entryability/VoIPUIAbility.ets", 
        "launchType": "singleton",
        "description": "VoIPUIAbility test", 
        "startWindowIcon": "$media:startIcon",
        "startWindowBackground": "$color:start_window_background",
        "exported": false, 
        "skills": [ 
          // 保持现有skill对象不变
          // 新增一个独立的skill对象，配置actions参数
          { 
            **"actions": ["action.ohos.push.listener"]**
          }
        ]
      } 
    ]
    
    - actions：内容为**action.ohos.push.listener**，有且只能有一个ability定义该action，**若同时添加uris参数，则uris内容需为空**。
    
5. 应用服务端调用REST API推送消息，消息详情可参见[场景化消息API接口功能介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-intro)。

### 应用内通话消息

1. 如果您需要呼叫，应用服务器可以调用REST API推送应用内通话消息，请求示例如下：
    
    // Request URL    
    POST "https://push-api.cloud.huawei.com/v3/[projectId]/messages:send"
    
    // Request Header   
    Content-Type: application/json   
    Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****   
    push-type: 10 
    
    // Request Body
    {   
      "pushOptions": { 
        "ttl": 30 
      }, 
      "payload": {   
        "extraData": "{\"scene\": \"voice\"}" 
      },   
      "target": {   
        "token": ["MAMzLg**********aZW"]   
      } 
    }
    
    - [projectId]：项目ID，登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”，在该页面获取。
    - Authorization：JWT格式字符串，可参见[基于服务账号生成鉴权令牌](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token)进行获取。
    - push-type：10表示应用内通话消息场景。
    - token：Push Token，可参见[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)章节获取。
    - extraData：携带的额外数据，字符串类型。详情参见[VoIPCallPayload 应用内通话消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section146341550144011)中extraData参数用法。extraData数据获取请参考[示例代码](https://gitcode.com/harmonyos_samples/push-kit-sample-code-clientdemo-arkts/blob/master/entry/src/main/ets/service/VoipCallService.ets)。
    - ttl：消息缓存时间，建议设置为30~60秒，详见pushOptions.[ttl](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section418321011212)。
    

说明

- 应用内通话消息只能用于音视频通话场景唤醒应用，完成呼叫，不要通过此种类型消息来挂断来电或者和应用通信，应用应该使用自己建立的网络连接和应用通信。相比应用服务器推送Push消息，使用现有的网络连接和应用通信通常会更快，在网络不佳的情况下，推送的Push消息可能无法到达应用。
- 应用无论是否在前台，自己的网络连接存在时，建议您通过Push推送应用内通话消息，再通过自己的网络连接发送通话消息，保证该呼叫能够到达应用。

### 未接来电通知

1. 如果您需要给被叫方发送未接来电通知，应用服务器可以调用REST API推送[通知消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert)。以通知消息为例，请求示例如下：
    
    // Request URL    
    POST "https://push-api.cloud.huawei.com/v3/**[projectId]**/messages:send"
       
    // Request Header   
    Content-Type: application/json   
    Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****   
    **push-type: 0** 
       
    // Request Body
    {   
      "pushOptions": { 
        **"ttl":**86400
      }, 
      "payload": {   
        "notification": { 
          "category": "MISS_CALL",  
          "title": "通知标题", 
          "body": "通知内容", 
          "clickAction": { 
            "actionType": 0 
          },
          "appMessageId": "12345"
        }
       },   
       "target": {   
         "token": ["MAMzLg**********aZW"]   
       } 
     }
    
    - push-type：0表示通知消息场景。
    - category：消息自分类类别，设置为MISS_CALL，请参见[参数说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)，发送消息前请确保您已[申请通知消息自分类权益](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section16708911111611)。
    - appMessageId：应用消息的唯一标识。被叫挂断，被叫方VoIP应用在前台时应用可以通过调用[Notification Kit（用户通知服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-overview)发送未接来电通知。被叫方VoIP应用在后台时，可以通过Push推送未接来电通知。应用可能存在前后台状态判断不准确，同一电话会产生两条未接来电，建议您通过Notification Kit和Push Kit推送的未接来电通知使用相同的appMessageId，系统会进行通知去重。
    - 其他参数说明可参见[通知消息请求体参数说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section1152516418157)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-update-liveview "推送实况窗消息")
# 基于服务账号生成鉴权令牌

更新时间: 2025-12-16 16:36

## 概述

服务账号（Service Account）是一种可实现服务器与服务器之间接口鉴权的账号，在华为开发者联盟的[API Console](https://developer.huawei.com/consumer/cn/console/api/myApi)上创建服务账号，您可根据返回的公私钥在业务应用中生成鉴权令牌，调用支持此类鉴权的华为公开API。

服务账号令牌为JWT（JSON Web Token）格式字符串，JWT数据格式包括三个部分：

- Header（头部）
- Payload（负载）
- Signature（签名）

这三个部分通过“.”进行连接，其中Signature为通过SHA256withRSA/PSS算法对Header与Payload拼接的字符串签名生成的字符串。

**示例**

1. eyJra*****JjNjBjMXXX.
2. eyJhd*****JodHRXXX.
3. BRNss*****7az5oU7-Zp5g9X2WJVXXX

更多JWT的相关知识请参见[Introduction to JSON Web Tokens](https://jwt.io/introduction/)。

## 开发步骤

1. 创建服务账号密钥文件。
    
    您需要在华为开发者联盟的[API Console](https://developer.huawei.com/consumer/cn/console/api/myApi)上创建并下载推送服务API的服务账号密钥文件，凭证创建入口如下图所示，选择所在项目，创建“服务账号密钥“凭证。相关创建步骤请参见[API服务操作指南-服务账号密钥](https://developer.huawei.com/consumer/cn/doc/start/api-0000001062522591#section3554194116341)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163653.03619726759598780798133696727698:50001231000000:2800:F23308EB217C49D562A833923FDFF0DF339B8C2F7EC58D74488C56EAD9669B4D.png "点击放大")
    
    您申请后的服务账号密钥样例文件形式可参考（文件内容已经经过脱敏处理）：
    
    1. {
    2.     "project_id": "*****",
    3.     "key_id": "*****",
    4.     "private_key": "-----BEGIN PRIVATE KEY-----\nMIIJQgIBADANBgkqhkiG9w0BAQEFAASCCSwwggkoAgEAAoICAQCKw6kJKtCh7qmMvp1u1dI27z2TKZrPOzHbQaXO/Eez0AWZ2EN+ouF496R3pfo7fQXC1XOT/YTbVC4DNZwWSMA54fu3/AOCY9Zzyi46OK*****==\n-----END PRIVATE KEY-----\n",
    5.     "sub_account": "*****",
    6.     "auth_uri": "https://oauth-login.cloud.huawei.com/oauth2/v3/authorize",
    7.     "token_uri": "https://oauth-login.cloud.huawei.com/oauth2/v3/token",
    8.     "auth_provider_cert_uri": "https://oauth-login.cloud.huawei.com/oauth2/v3/certs",
    9.     "client_cert_uri": "https://oauth-login.cloud.huawei.com/oauth2/v3/x509?client_id="
    10. }
    
2. 请确认以上密钥文件中的project_id是否与您的应用所属项目一致。
    
    您的应用所属项目ID查看方法：登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”，在该页面获取。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163654.04006347368954682241947506528527:50001231000000:2800:8BA53E3046BA12EFB1C10ACF6095DD4C90DF3F45B6D0BBCF5F184A00090714F1.png "点击放大")
    
3. 生成JWT Header数据。
    
    根据服务账号密钥文件中的key_id（对应示例中的kid）字段拼接以下JSON体，对JSON体进行BASE64编码。
    
    示例
    
    1. {
    2.   "kid": "*****",
    3.   "typ": "JWT",
    4.   "alg": "PS256"
    5. }
    
    |字段名|描述|
    |:--|:--|
    |kid|服务账号密钥文件中key_id字段。|
    |typ|数据类型，固定为：JWT。|
    |alg|算法类型，固定为：PS256。|
    
4. 生成JWT Payload数据。
    
    根据服务账号密钥文件中的sub_account（对应示例中的iss）字段拼接以下JSON体，对JSON体进行BASE64编码。
    
    **示例**
    
    1. {
    2.   "aud": "https://oauth-login.cloud.huawei.com/oauth2/v3/token",
    3.   "iss": "*****",
    4.   "exp": 1581410664,
    5.   "iat": 1581407064
    6. }
    
    |字段名|描述|
    |:--|:--|
    |iss|服务账号密钥文件中sub_account字段，标识数据生成者。|
    |aud|固定为：https://oauth-login.cloud.huawei.com/oauth2/v3/token。|
    |iat|JWT签发UTC时间戳，为自UTC时间1970年1月1日00:00:00起的秒数（您的服务器时间需要校准为标准时间）。|
    |exp|JWT到期UTC时间戳，比iat晚3600秒。|
    
5. 生成JWT Token。
    
    将完成BASE64编码后的Header字符串与Payload字符串，通过“.”进行连接，您可在业务应用中，通过服务账号密钥文件中的private_key（华为不进行存储，请您妥善保管），使用SHA256withRSA/PSS算法对拼接的字符串签名。
    
    至此，您已经完成服务账号鉴权令牌JWT Token的生成。
    

## 调用推送服务REST API

您的应用调用推送服务REST API时，需要把已获得的服务账号鉴权令牌放在Authorization头部来进行鉴权。请使用v3版本调用推送服务REST API。

**示例**

1. POST "https://push-api.cloud.huawei.com/v3/3158882***52863/messages:send"
2. Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
3. push-type:0

说明

Authorization格式：Bearer后面拼接空格，再拼接获取的鉴权信息。

接口版本：请使用V3版本调用推送服务REST API。

场景化消息[请求体](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct)中，接口URL版本为V3（https://push-api.cloud.huawei.com/v3/[projectId]/messages:send）时，仅支持给HarmonyOS Next/5.x及之后的系统版本推送通知；接口URL版本为V2（https://push-api.cloud.huawei.com/v2/[projectId]/messages:send）时，仅支持给HarmonyOS 3.x/4.x的系统版本推送通知。

## 示例代码

为了方便您生成服务账号鉴权令牌，我们提供了Java语言的示例代码，请按照说明替换参数运行。

如果您使用其他开发语言，请选择对应的[JWT开源组件](https://jwt.io/libraries)进行开发。

其中鉴权令牌生成步骤如下：

1. 完成上述[开发步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token#section16173145352)中的步骤1创建服务账号密钥文件后，从华为开发者联盟的[API Console](https://developer.huawei.com/consumer/cn/console/api/myApi)上创建并下载推送服务API的服务账号密钥文件（.json文件），格式如下：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163654.97398906352097504323242389129760:50001231000000:2800:3C40B032CE4B41B5E6AEFC3C79E755EF684A636465DD8AE4AD68696E7D5D03BB.png)
    
2. 以上json文件复制至工程中，参考如下代码进行解析（以private.json为例）。

Java

Node.js

Go

Python

PHP

1. /* 推荐的java版本为java8，maven依赖如下：
2.   <dependency>
3.    <groupId>com.fasterxml.jackson.core</groupId>
4.    <artifactId>jackson-databind</artifactId>
5.    <version>2.16.2</version>
6.   </dependency>
7.   <dependency>
8.    <groupId>io.jsonwebtoken</groupId>
9.    <artifactId>jjwt-api</artifactId>
10.    <version>0.11.5</version>
11.   </dependency>
12.   <dependency>
13.    <groupId>io.jsonwebtoken</groupId>
14.    <artifactId>jjwt-impl</artifactId>
15.    <version>0.11.5</version>
16.    <scope>runtime</scope>
17.   </dependency>
18.   <dependency>
19.    <groupId>io.jsonwebtoken</groupId>
20.    <artifactId>jjwt-jackson</artifactId>
21.    <version>0.11.5</version>
22.    <scope>runtime</scope>
23.   </dependency>
24.   <dependency>
25.    <groupId>org.bouncycastle</groupId>
26.    <artifactId>bcprov-jdk18on</artifactId>
27.    <version>1.78.1</version>
28.    <scope>runtime</scope>
29.   </dependency>
30. */

31. import com.fasterxml.jackson.databind.JsonNode;
32. import com.fasterxml.jackson.databind.ObjectMapper;

33. import io.jsonwebtoken.*;
34. import io.jsonwebtoken.lang.Maps;

35. import java.io.File;
36. import java.io.IOException;
37. import java.net.URL;
38. import java.nio.charset.StandardCharsets;
39. import java.security.KeyFactory;
40. import java.security.NoSuchAlgorithmException;
41. import java.security.PrivateKey;
42. import java.security.interfaces.RSAPrivateKey;
43. import java.security.spec.InvalidKeySpecException;
44. import java.security.spec.PKCS8EncodedKeySpec;
45. import java.util.Base64;
46. import java.util.Map;

47. public class JsonWebTokenFactory {

48.     // 实际开发时请将公网地址存储在配置文件或数据库
49.     private static final String AUD = "https://oauth-login.cloud.huawei.com/oauth2/v3/token";

50.     public static String createJwt() throws NoSuchAlgorithmException, InvalidKeySpecException, IOException, NullPointerException {
51.         // 读取配置文件
52.         ObjectMapper mapper = new ObjectMapper();
53.         // 上述private.json文件放置于工程的src/main/resources路径下
54.         URL url = JsonWebTokenFactory.class.getClassLoader().getResource("private.json");
55.         if (url == null) {
56.             throw new NullPointerException("File not exist");
57.         }
58.         JsonNode rootNode = mapper.readTree(new File(url.getPath()));

59.         RSAPrivateKey privateKey = (RSAPrivateKey) generatePrivateKey(rootNode.get("private_key").asText()
60.                 .replace("-----BEGIN PRIVATE KEY-----", "")
61.                 .replace("-----END PRIVATE KEY-----", "")
62.                 .replaceAll("\\s", ""));
63.         long iat = System.currentTimeMillis() / 1000;
64.         long exp = iat + 3600;

65.         Map<String, Object> header = Maps.<String, Object>of(JwsHeader.KEY_ID, rootNode.get("key_id").asText())
66.                 .and(JwsHeader.TYPE, JwsHeader.JWT_TYPE)
67.                 .and(JwsHeader.ALGORITHM, SignatureAlgorithm.PS256.getValue())
68.                 .build();

69.         Map<String, Object> payload = Maps.<String, Object>of(Claims.ISSUER, rootNode.get("sub_account").asText())
70.                 .and(Claims.ISSUED_AT, iat)
71.                 .and(Claims.EXPIRATION, exp)
72.                 .and(Claims.AUDIENCE, AUD)
73.                 .build();

74.         return Jwts.builder()
75.                 .setHeader(header)
76.                 .setPayload(new ObjectMapper().writeValueAsString(payload))
77.                 .signWith(privateKey, SignatureAlgorithm.PS256)
78.                 .compact();
79.     }

80.     private static PrivateKey generatePrivateKey(String base64Key) throws NoSuchAlgorithmException, InvalidKeySpecException {
81.         PKCS8EncodedKeySpec keySpec = new PKCS8EncodedKeySpec(Base64.getDecoder().decode(base64Key.getBytes(StandardCharsets.UTF_8)));
82.         KeyFactory keyFactory = KeyFactory.getInstance("RSA");
83.         return keyFactory.generatePrivate(keySpec);
84.     }

85.     public static void main(String[] args) {
86.         try {
87.             // 获取鉴权令牌
88.             String jwt = createJwt();
89.         } catch (NoSuchAlgorithmException e) {
90.             // 异常处理流程1
91.         } catch (InvalidKeySpecException e) {
92.             // 异常处理流程2
93.         } catch (IOException e) {
94.             // 异常处理流程3
95.         } catch (NullPointerException e) {
96.             // 异常处理流程4
97.         }
98.     }
99. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-server-intro "端云调试概述")
# 基于服务账号生成鉴权令牌

更新时间: 2025-12-16 16:36

## 概述

服务账号（Service Account）是一种可实现服务器与服务器之间接口鉴权的账号，在华为开发者联盟的[API Console](https://developer.huawei.com/consumer/cn/console/api/myApi)上创建服务账号，您可根据返回的公私钥在业务应用中生成鉴权令牌，调用支持此类鉴权的华为公开API。

服务账号令牌为JWT（JSON Web Token）格式字符串，JWT数据格式包括三个部分：

- Header（头部）
- Payload（负载）
- Signature（签名）

这三个部分通过“.”进行连接，其中Signature为通过SHA256withRSA/PSS算法对Header与Payload拼接的字符串签名生成的字符串。

**示例**

1. eyJra*****JjNjBjMXXX.
2. eyJhd*****JodHRXXX.
3. BRNss*****7az5oU7-Zp5g9X2WJVXXX

更多JWT的相关知识请参见[Introduction to JSON Web Tokens](https://jwt.io/introduction/)。

## 开发步骤

1. 创建服务账号密钥文件。
    
    您需要在华为开发者联盟的[API Console](https://developer.huawei.com/consumer/cn/console/api/myApi)上创建并下载推送服务API的服务账号密钥文件，凭证创建入口如下图所示，选择所在项目，创建“服务账号密钥“凭证。相关创建步骤请参见[API服务操作指南-服务账号密钥](https://developer.huawei.com/consumer/cn/doc/start/api-0000001062522591#section3554194116341)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163653.03619726759598780798133696727698:50001231000000:2800:F23308EB217C49D562A833923FDFF0DF339B8C2F7EC58D74488C56EAD9669B4D.png "点击放大")
    
    您申请后的服务账号密钥样例文件形式可参考（文件内容已经经过脱敏处理）：
    
    1. {
    2.     "project_id": "*****",
    3.     "key_id": "*****",
    4.     "private_key": "-----BEGIN PRIVATE KEY-----\nMIIJQgIBADANBgkqhkiG9w0BAQEFAASCCSwwggkoAgEAAoICAQCKw6kJKtCh7qmMvp1u1dI27z2TKZrPOzHbQaXO/Eez0AWZ2EN+ouF496R3pfo7fQXC1XOT/YTbVC4DNZwWSMA54fu3/AOCY9Zzyi46OK*****==\n-----END PRIVATE KEY-----\n",
    5.     "sub_account": "*****",
    6.     "auth_uri": "https://oauth-login.cloud.huawei.com/oauth2/v3/authorize",
    7.     "token_uri": "https://oauth-login.cloud.huawei.com/oauth2/v3/token",
    8.     "auth_provider_cert_uri": "https://oauth-login.cloud.huawei.com/oauth2/v3/certs",
    9.     "client_cert_uri": "https://oauth-login.cloud.huawei.com/oauth2/v3/x509?client_id="
    10. }
    
2. 请确认以上密钥文件中的project_id是否与您的应用所属项目一致。
    
    您的应用所属项目ID查看方法：登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”，在该页面获取。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163654.04006347368954682241947506528527:50001231000000:2800:8BA53E3046BA12EFB1C10ACF6095DD4C90DF3F45B6D0BBCF5F184A00090714F1.png "点击放大")
    
3. 生成JWT Header数据。
    
    根据服务账号密钥文件中的key_id（对应示例中的kid）字段拼接以下JSON体，对JSON体进行BASE64编码。
    
    示例
    
    1. {
    2.   "kid": "*****",
    3.   "typ": "JWT",
    4.   "alg": "PS256"
    5. }
    
    |字段名|描述|
    |:--|:--|
    |kid|服务账号密钥文件中key_id字段。|
    |typ|数据类型，固定为：JWT。|
    |alg|算法类型，固定为：PS256。|
    
4. 生成JWT Payload数据。
    
    根据服务账号密钥文件中的sub_account（对应示例中的iss）字段拼接以下JSON体，对JSON体进行BASE64编码。
    
    **示例**
    
    1. {
    2.   "aud": "https://oauth-login.cloud.huawei.com/oauth2/v3/token",
    3.   "iss": "*****",
    4.   "exp": 1581410664,
    5.   "iat": 1581407064
    6. }
    
    |字段名|描述|
    |:--|:--|
    |iss|服务账号密钥文件中sub_account字段，标识数据生成者。|
    |aud|固定为：https://oauth-login.cloud.huawei.com/oauth2/v3/token。|
    |iat|JWT签发UTC时间戳，为自UTC时间1970年1月1日00:00:00起的秒数（您的服务器时间需要校准为标准时间）。|
    |exp|JWT到期UTC时间戳，比iat晚3600秒。|
    
5. 生成JWT Token。
    
    将完成BASE64编码后的Header字符串与Payload字符串，通过“.”进行连接，您可在业务应用中，通过服务账号密钥文件中的private_key（华为不进行存储，请您妥善保管），使用SHA256withRSA/PSS算法对拼接的字符串签名。
    
    至此，您已经完成服务账号鉴权令牌JWT Token的生成。
    

## 调用推送服务REST API

您的应用调用推送服务REST API时，需要把已获得的服务账号鉴权令牌放在Authorization头部来进行鉴权。请使用v3版本调用推送服务REST API。

**示例**

1. POST "https://push-api.cloud.huawei.com/v3/3158882***52863/messages:send"
2. Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
3. push-type:0

说明

Authorization格式：Bearer后面拼接空格，再拼接获取的鉴权信息。

接口版本：请使用V3版本调用推送服务REST API。

场景化消息[请求体](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct)中，接口URL版本为V3（https://push-api.cloud.huawei.com/v3/[projectId]/messages:send）时，仅支持给HarmonyOS Next/5.x及之后的系统版本推送通知；接口URL版本为V2（https://push-api.cloud.huawei.com/v2/[projectId]/messages:send）时，仅支持给HarmonyOS 3.x/4.x的系统版本推送通知。

## 示例代码

为了方便您生成服务账号鉴权令牌，我们提供了Java语言的示例代码，请按照说明替换参数运行。

如果您使用其他开发语言，请选择对应的[JWT开源组件](https://jwt.io/libraries)进行开发。

其中鉴权令牌生成步骤如下：

1. 完成上述[开发步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token#section16173145352)中的步骤1创建服务账号密钥文件后，从华为开发者联盟的[API Console](https://developer.huawei.com/consumer/cn/console/api/myApi)上创建并下载推送服务API的服务账号密钥文件（.json文件），格式如下：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163654.97398906352097504323242389129760:50001231000000:2800:3C40B032CE4B41B5E6AEFC3C79E755EF684A636465DD8AE4AD68696E7D5D03BB.png)
    
2. 以上json文件复制至工程中，参考如下代码进行解析（以private.json为例）。

Java

Node.js

Go

Python

PHP

1. /* 推荐的java版本为java8，maven依赖如下：
2.   <dependency>
3.    <groupId>com.fasterxml.jackson.core</groupId>
4.    <artifactId>jackson-databind</artifactId>
5.    <version>2.16.2</version>
6.   </dependency>
7.   <dependency>
8.    <groupId>io.jsonwebtoken</groupId>
9.    <artifactId>jjwt-api</artifactId>
10.    <version>0.11.5</version>
11.   </dependency>
12.   <dependency>
13.    <groupId>io.jsonwebtoken</groupId>
14.    <artifactId>jjwt-impl</artifactId>
15.    <version>0.11.5</version>
16.    <scope>runtime</scope>
17.   </dependency>
18.   <dependency>
19.    <groupId>io.jsonwebtoken</groupId>
20.    <artifactId>jjwt-jackson</artifactId>
21.    <version>0.11.5</version>
22.    <scope>runtime</scope>
23.   </dependency>
24.   <dependency>
25.    <groupId>org.bouncycastle</groupId>
26.    <artifactId>bcprov-jdk18on</artifactId>
27.    <version>1.78.1</version>
28.    <scope>runtime</scope>
29.   </dependency>
30. */

31. import com.fasterxml.jackson.databind.JsonNode;
32. import com.fasterxml.jackson.databind.ObjectMapper;

33. import io.jsonwebtoken.*;
34. import io.jsonwebtoken.lang.Maps;

35. import java.io.File;
36. import java.io.IOException;
37. import java.net.URL;
38. import java.nio.charset.StandardCharsets;
39. import java.security.KeyFactory;
40. import java.security.NoSuchAlgorithmException;
41. import java.security.PrivateKey;
42. import java.security.interfaces.RSAPrivateKey;
43. import java.security.spec.InvalidKeySpecException;
44. import java.security.spec.PKCS8EncodedKeySpec;
45. import java.util.Base64;
46. import java.util.Map;

47. public class JsonWebTokenFactory {

48.     // 实际开发时请将公网地址存储在配置文件或数据库
49.     private static final String AUD = "https://oauth-login.cloud.huawei.com/oauth2/v3/token";

50.     public static String createJwt() throws NoSuchAlgorithmException, InvalidKeySpecException, IOException, NullPointerException {
51.         // 读取配置文件
52.         ObjectMapper mapper = new ObjectMapper();
53.         // 上述private.json文件放置于工程的src/main/resources路径下
54.         URL url = JsonWebTokenFactory.class.getClassLoader().getResource("private.json");
55.         if (url == null) {
56.             throw new NullPointerException("File not exist");
57.         }
58.         JsonNode rootNode = mapper.readTree(new File(url.getPath()));

59.         RSAPrivateKey privateKey = (RSAPrivateKey) generatePrivateKey(rootNode.get("private_key").asText()
60.                 .replace("-----BEGIN PRIVATE KEY-----", "")
61.                 .replace("-----END PRIVATE KEY-----", "")
62.                 .replaceAll("\\s", ""));
63.         long iat = System.currentTimeMillis() / 1000;
64.         long exp = iat + 3600;

65.         Map<String, Object> header = Maps.<String, Object>of(JwsHeader.KEY_ID, rootNode.get("key_id").asText())
66.                 .and(JwsHeader.TYPE, JwsHeader.JWT_TYPE)
67.                 .and(JwsHeader.ALGORITHM, SignatureAlgorithm.PS256.getValue())
68.                 .build();

69.         Map<String, Object> payload = Maps.<String, Object>of(Claims.ISSUER, rootNode.get("sub_account").asText())
70.                 .and(Claims.ISSUED_AT, iat)
71.                 .and(Claims.EXPIRATION, exp)
72.                 .and(Claims.AUDIENCE, AUD)
73.                 .build();

74.         return Jwts.builder()
75.                 .setHeader(header)
76.                 .setPayload(new ObjectMapper().writeValueAsString(payload))
77.                 .signWith(privateKey, SignatureAlgorithm.PS256)
78.                 .compact();
79.     }

80.     private static PrivateKey generatePrivateKey(String base64Key) throws NoSuchAlgorithmException, InvalidKeySpecException {
81.         PKCS8EncodedKeySpec keySpec = new PKCS8EncodedKeySpec(Base64.getDecoder().decode(base64Key.getBytes(StandardCharsets.UTF_8)));
82.         KeyFactory keyFactory = KeyFactory.getInstance("RSA");
83.         return keyFactory.generatePrivate(keySpec);
84.     }

85.     public static void main(String[] args) {
86.         try {
87.             // 获取鉴权令牌
88.             String jwt = createJwt();
89.         } catch (NoSuchAlgorithmException e) {
90.             // 异常处理流程1
91.         } catch (InvalidKeySpecException e) {
92.             // 异常处理流程2
93.         } catch (IOException e) {
94.             // 异常处理流程3
95.         } catch (NullPointerException e) {
96.             // 异常处理流程4
97.         }
98.     }
99. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-server-intro "端云调试概述")
# 推送场景化消息

更新时间: 2025-12-16 16:37

## 场景介绍

Push Kit支持您使用HTTPS协议接入云侧，使用场景化V3接口发送场景化消息，并将不同场景定义为不同push-type。

您可发送的场景化消息类型如下表：

|push-type|名称|
|:--|:--|
|0|Alert消息（通知消息）|
|1|卡片刷新（Wearable、TV不支持）|
|2|通知扩展消息（TV不支持）|
|6|后台消息|
|7|实况窗消息（Wearable、TV、PC/2in1不支持）|
|9|定位消息（Wearable、TV不支持）|
|10|应用内通话消息（Wearable、TV、PC/2in1不支持）|

有关场景化消息的更详细说明，请参见REST API-[场景化消息API接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-rest-api-scenes)。

## 开发步骤

1. 您的服务端获取鉴权令牌，详情请参见[基于服务账号生成鉴权令牌](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token)。
2. 您的服务端调用API发送Push场景化消息，更多消息内容请参见REST API-[场景化消息API接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-rest-api-scenes)。
    
    **HTTPS POST URL：**
    
    1. POST https://push-api.cloud.huawei.com/v3/**[projectId]**/messages:send
    
    “[projectId]”请替换为您应用的项目ID。登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”，在该页面获取“项目ID”。
    
    **请求消息头示例：**
    
    2. Content-Type: application/json
    3. Authorization: Bearer eyJr*****OiIx---****.eyJh*****iJodHR--***.QRod*****4Gp---****
    4. **push-type: 0**
    
    - 请求消息头中的Authorization参数为"Bearer "拼接上您在上一步[在线生成服务账号鉴权令牌](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token)中获取的鉴权令牌。
    - 请求消息头中的push-type参数为场景化消息类型，0代表Alert消息（通知消息）。
    
    **通知消息体示例：**
    
    1. {
    2.   "payload": {
    3.     **"notification": {**
    4.       "category": "MARKETING",
    5.       "title": "普通通知标题",
    6.       "body": "普通通知内容",
    7.       "clickAction": {
    8.         "actionType": 0
    9.       },
    10.       "notifyId": 12345
    11.     **}**
    12.   },
    13.   "target": {
    14.     "token": ["MAMzLg**********lPW"]
    15.   },
    16.   "pushOptions": {
    17.     "testMessage": true
    18.   }
    19. }
    
    - 更多场景化消息示例可参见[请求示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-example)。
    - 建议您在开发代码前先使用Postman等调试工具发送消息，测试功能。
    
3. （可选）您的应用服务器接收Push Kit的消息回执，详情请参见[消息回执](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-msg-receipt)。

说明

Push Kit提供了基于Java语言的服务端示例代码（包括申请鉴权令牌、发送通知消息、卡片刷新消息等功能），方便您参考使用，详情请参见[示例代码](https://gitee.com/harmonyos_samples/push-kit_-sample-code_-server-demo_-java)。

## AppGallery Connect在线推送通知消息

注意

**当前仅支持配置Alert消息**。

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，点击“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163705.98350207444325472483105857266762:50001231000000:2800:D129A77C882DDC5C439F1B1DF06EE415F183A659BD49104867C67E4D86388994.png)
    
2. 在项目列表中找到您的项目，通过“增长 > 推送服务 > 推送通知（V3 Beta）”导航到“推送通知（V3 Beta）”页签。在该页签下点击“添加推送通知”新建推送任务。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163705.07267367370083241294284782574404:50001231000000:2800:9BDD429A6FC47C4A1A4C03D7241F12182EF8608F49C13F5BBD818F61F7C2A27D.png "点击放大")
    
3. 这里以Alert消息举例，配置参数如下。
    
    - **配置推送任务**
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163705.63029130468285580938016986203057:50001231000000:2800:67B1B59610FE6CB57777DFEAC3CD7A2300DB14BE947E06BA28664C4BE9930358.png "点击放大")
        
        |字段值|说明|
        |:--|:--|
        |选择应用|必填字段，消息发送的目标应用。|
        |名称|必填字段，用于在管理台中标识通知，此名称不会给用户显示。|
        |场景化类型|场景化消息类型，**当前仅支持Alert消息**。|
        
    
    - **配置推送内容-****通用参数**
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163705.06676988339306898624312316440919:50001231000000:2800:C82716B1A78FA7E449259CF785398CE30BB784E57FB8E8858AB9069652AE7F86.png "点击放大")
        
        |字段值|说明|
        |:--|:--|
        |是否测试消息 (testMessage)|必选字段，对应场景化接口中的testMessage参数；<br><br>测试消息标识：<br><br>- false：正式消息<br>- true：测试消息**（默认值）**|
        |离线消息缓存机制 (collapseKey)|可选字段，对应场景化接口中的collapseKey参数；<br><br>离线消息缓存控制方式，取值范围-1~100：<br><br>- -1：对所有离线消息都缓存（**默认值）**；<br>- 0~100：离线消息缓存分组标识，对离线消息进行分组缓存，每个应用每一组只缓存一条最新的离线消息。|
        |消息缓存时间 (ttl)|可选字段，对应场景化接口中的ttl参数；<br><br>消息缓存时间，单位是秒。在用户设备离线时，消息在Push服务器进行缓存，在消息缓存时间内用户设备上线，消息会下发，超过缓存时间后消息会丢弃，**默认值为86400秒（1天）**，最大值为15天。|
        |批量任务消息标识 (biTag)|可选字段，对应场景化接口中的biTag参数；<br><br>批量任务消息标识，[消息回执](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-msg-receipt)时会返回给应用服务器，长度最大64字节。|
        |回执ID (receiptId)|可选字段，对应场景化接口中的receiptId参数；<br><br>回执ID指定本次下行消息的回执地址及配置。该回执ID可以在[配置回执参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-msg-receipt#section462935643010)中查看。|
        
    
    - **配置推送内容-发送目标设备**
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163705.85170121253670495467917529783599:50001231000000:2800:08D2F7B6201ECC481130788A71F2952EA39A64992CF3633311AB4046C36A789C.png)
        
        |字段值|说明|
        |:--|:--|
        |设备Token (token)|必填字段，对应场景化接口中的token参数；<br><br>按照Token向目标用户推送消息**。**<br><br>**样例：MAMzL*********|
        
    
    - **配置推送内容-消息内容**
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163705.89187365648732105068237264950159:50001231000000:2800:8A4E753CEBC6206C3B0E8086213F8167C82CFCDB06A82BBCE202DA6E9B1F4783.png "点击放大")
        
        |字段值|说明|
        |:--|:--|
        |消息类别 (category)|必填字段，对应场景化接口中的category参数；<br><br>通知消息类别。完成[申请通知消息自分类权益](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section16708911111611)后，用于标识消息类型，不同的通知消息类型影响消息展示和提醒方式。取值如下：<br><br>- 即时聊天：IM<br>- 音视频通话：VOIP<br>- 订阅：SUBSCRIPTION<br>- 出行：TRAVEL<br>- 健康：HEALTH<br>- 工作事项提醒：WORK<br>- 账号动态：ACCOUNT<br>- 订单&物流：EXPRESS<br>- 财务：FINANCE<br>- 设备提醒：DEVICE_REMINDER<br>- 邮件：MAIL<br>- 新闻、内容推荐、社交动态、产品促销、财经动态、生活资讯、调研、功能推荐、运营活动（仅对内容进行标识，不会加快消息发送），统称为资讯营销类消息：MARKETING<br>- PLAY_VOICE：语音播报|
        |消息标题 (title)|必填字段，对应场景化接口中的title参数；<br><br>通知消息标题。|
        |消息内容 (body)|必填字段，对应场景化接口中的body参数；<br><br>通知消息内容。|
        |点击通知动作 (actionType)|必填字段，对应场景化接口中的clickAction中actionType参数；<br><br>点击消息后触发的动作，可选择打开应用首页、自定义action页面或自定义intentUri页面。|
        
4. 当您完成上述步骤后，点击右上方“提交”按钮即可推送消息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163705.63022227175854242642173563366511:50001231000000:2800:AC44BF002F740CC3B423E988EB75BB85F5F01B40DCFD771E0B417DCC3C1868C9.png)
    
    注意
    
    预览效果仅供参考，请以客户端实际效果为准。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token "基于服务账号生成鉴权令牌")
# （可选）开发消息回执

更新时间: 2025-12-16 16:37

## 场景介绍

消息回执是指Push Kit服务端将消息推送到用户终端之后，端侧会给Push服务端反馈送达结果，与此同时，Push服务端会将消息送达状态以回执消息形式发送给您的应用回执服务端，方便您获取消息下达端侧后的状态，定位问题等。

受网络环境以及消息量的影响，消息回执在Push服务端收到端侧响应后发送，会存在一些延迟现象，如果较长时间无法收到回执，可能是设备处于离线状态。

## 回执服务开发

请参见[消息回执API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-api-msg-receipt)开发您的回执服务器代码，服务接口地址将作为[配置回执参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-msg-receipt#section462935643010)中的回调地址。

## 开通回执权益

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”，在项目列表中选择对应的项目，左侧导航栏选择“项目设置”。
    
2. 在项目列表中找到您的项目，通过“增长 > 推送服务 > 配置”导航到“配置”页签。在该页面可以选择配置项目级回执或者应用级回执，需要注意的是项目级回执消息接收URL地址，对该项目下所有应用生效。如果您同时配置了项目级回执和应用级回执地址，则优先获取应用级回执地址信息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163728.52018951846250779885878554393517:50001231000000:2800:3A7C963EAB6125515BE7783307A07189B171D500F39417BD43F1CA5B5C977894.png "点击放大")
    
3. 这里以应用级回执举例，选择需要配置回执的应用，点击“开通”应用回执状态。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163728.15533150174486651507067840892648:50001231000000:2800:B6B9CF33F075D1ED46E1E86841847AC13FB2E959C2A307D398FF1D58D3655FF5.png "点击放大")
    
4. 进入回执参数配置，可以选择已有回执或者新建回执。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163728.46809325721444035577478413639876:50001231000000:2800:D5E6A857736B58F328BCC8F54C4B50CD2DAEF01DA3746DB13F6522B30D2A4D88.png "点击放大")
    

## 配置回执参数

点击“新建回执”后，需要配置如下参数：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163728.01388206383230515836625629050313:50001231000000:2800:DB74D4ADC90E9178F4723D7D4ADA6FD7E8E64B7CAB58694740D0D1C2ADF8F21F.png "点击放大")

1. 配置消息回执的名称和回调地址。
    
    回调地址配置完成后，Push Kit服务器会校验回执服务器（接收回执消息的应用服务器）提供的证书是否为商用CA签发证书。
    
    - 商用CA提示：
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163728.20710317383981547955639555293967:50001231000000:2800:03E89D2A4AD26BC40D50C6F79CB8C69E99BB0BE630FC1C463C68602E37ABA2A3.png "点击放大")
        
    - 自签CA提示：
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163728.79604334784140216319770472510299:50001231000000:2800:EAC339C0C27EB6E2B5346B44BEC42142E25D42799D52F3D47A18702AF272233F.png "点击放大")
        
        注意
        
        证书过期将导致您无法接收消息回执，请及时更换回执服务器证书。
        
2. 配置回调用户名（可选，下文描述为userName）和回调密钥（可选，下文描述为secret）进行身份验证。回调密钥支持自动生成。
    1. 从回执消息的请求Header中获取X-HUAWEI-CALLBACK-ID，举例如下：
        
        1. X-HUAWEI-CALLBACK-ID: 
        2. timestamp=1563*****1261;nonce=a07bfa17-6d82-4b53-a9a2-07c*****eef1;value=E4YeO*********************QXF+c=
        
        其中timestamp为回执消息的时间戳（毫秒级时间戳），nonce为UUID随机数，value为签名信息，签名方法为：Base64(HMAC-SHA256(secret, timestamp+nonce+userName))。
        
    2. 开发者可以根据timestamp、nonce、userName、secret参考示例生成签名，与value的值比较进行签名验证。开发者也可点击网页提供的“生成密钥”自动生成回调密钥。
        
        生成签名示例（以下为java代码）：
        
        1. StringBuilder buf = new StringBuilder(); 
        2. buf.append(timestamp); 
        3. buf.append(nonce); 
        4. // 在回执配置中的回调用户名
        5. buf.append(userName); 
        6. // 在回执配置中的回调密钥
        7. String secret = "your secret"; 
        8. String signature = ""; 
        9. try { 
        10.   Mac mac = Mac._getInstance_("HmacSHA256");
        11.   // 老旧版本的回执配置密钥使用secret.getBytes(UTF_8)，新的回执配置密钥使用base64编码
        12.   SecretKeySpec key = new SecretKeySpec(Base64.getDecoder().decode(secret), "HmacSHA256"); 
        13.   mac.init(key); 
        14.   byte[] encodeV = mac.doFinal(buf.toString().getBytes(UTF_8));  
        15.   signature = Base64._getEncoder_().encodeToString(encodeV); 
        16. } catch (NoSuchAlgorithmException | InvalidKeyException e) {  
        17.   // 打印错误日志 
        18.   // ...
        19. }
        
3. 配置回执支持版本
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163728.24695269733579236006882336953404:50001231000000:2800:76DAAD7E6D5945436AB698DF53BB5BA83A5F2953A8093A33A12141369A4AEC60.png "点击放大")
    
    V1回执不支持场景化消息发送，请使用V2回执。
    
4. “测试回执”可以对回执地址进行功能测试，点击“提交”完成回执的创建。
    
    说明
    
    - 华为Push服务器和接收回执消息的应用服务器之间使用HTTPS协议，华为Push服务器会校验应用服务器提供证书的合法性，请使用商用CA签发的HTTPS证书。
    - 如果您的回执配置正确，点击“测试回执”后，您的回执服务器将收到由华为Push服务器发送的测试消息，同一回执版本该消息内容固定，仅供测试使用。
    
    **示例报文：**
    
    消息到达回执：
    
    说明
    
    除卡片刷新场景外的其他场景化消息均支持消息到达回执。
    
    1.  {
    2.   "statuses": [
    3.     {
    4.       "biTag": "bi**62",
    5.       "pushType": 0,
    6.       "token": "MsDZmCSyuS+Gd***********ZLs8Es",
    7.       "requestId": "169802**1701",
    8.       "appPackageName": "com.**.**",
    9.       "deliveryStatus": {
    10.         "result": 0,
    11.         "timestamp": 1697741455082
    12.       }
    13.     }
    14.   ]
    15. }
    
    卡片刷新回执：
    
    16. {
    17.   "statuses": [
    18.     {
    19.       "biTag": "bi**62",
    20.       "pushType": 1,
    21.       "token": "MsDZmCSyuS+Gd***********ZLs8Es",
    22.       "requestId": "169802**1701",
    23.       "appPackageName": "com.**.**",
    24.       "formStatus": {
    25.         "formId": 10086,
    26.         "result": 0,
    27.         "timestamp": 1698027152082
    28.       }
    29.     }
    30.   ]
    31. }
    
    您的回执服务器必须返回成功的响应，才能测试通过，再点击“提交”完成回执的创建。
    
    成功响应：
    
    32. { 
    33.      "code": "0", 
    34.      "message": "success" 
    35.  }
    

## 回执状态码

注意

通过回执状态码定位问题之前，请优先检查[消息推送接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct)URL（https://push-api.cloud.huawei.com/**v3**/**[projectId]**/messages:send）是否正确：

- 请使用v3版本的推送接口URL，不要使用v1或v2版本的推送接口URL，详情请参见[场景化消息中的请求URL版本问题](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-8)。
- 请检查推送接口地址中的projectId，确保与您当前应用所属的项目保持一致，若不一致请更新推送接口URL中的projectId，并重新[生成鉴权令牌](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token)，应用重新[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)，再进行消息推送。

您可以基于接收到的消息回执码进行数据统计和分析，回执状态码如下表所示：

|回执状态码|状态码描述|原因及处理|
|:--|:--|:--|
|0|成功送达|不涉及。|
|2|Token无效，应用卸载|成功发送到设备后发现应用不存在，通常表示应用已卸载。|
|5|Token无效，Token不匹配|终端收到应用的Push消息，但Push消息带的Token与本地应用的Token不一致。请排查以下几种原因：<br><br>- 终端用户清除了本地应用数据。<br>- 终端用户通过卸载再安装的方式更新了本地应用。<br>- 您在应用中调用pushService.[deleteToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section108761115154914)()方法删除了本地应用的Token。<br>- 您在应用中调用了[deleteAAID](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-aaid-api#section4466259194220)()，该方法删除AAID的同时也会删除本地应用的Token。<br>- 终端设备恢复出厂设置后终端用户重新进入预安装应用或者重新安装并进入应用。<br><br>终端收到应用的Push消息，但检查本地数据存储中并没有应用的Token。请排查以下原因：<br><br>- 应用未激活。<br><br>若您的问题仍无法解决，请通过[在线提单](https://developer.huawei.com/consumer/cn/support/feedback/#/)提交问题。|
|6|通知消息不展示|请排查以下三种原因：<br><br>- 用户关闭了设备上的系统通知总开关。<br>- 用户关闭了本应用的通知渠道开关。<br>- 用户开启了未成年模式。|
|10|非活跃设备|设备为非活跃设备（终端设备未接入网络达30天），消息不进行下发。|
|14|其它错误|系统内部网络异常。|
|15|离线用户消息管控|1. 设置了离线用户消息覆盖（服务端API中的collapseKey）功能，消息被覆盖掉了，未下发到设备。<br>2. 离线消息最多缓存120条，超过后旧消息被新消息覆盖。|
|22|目标用户不匹配|下发消息时Push Token归属的用户与当前终端设备上的本地用户不匹配。请排查Push Token是否是当前本地用户下申请的。<br><br>注意<br><br>如您在进入隐私空间前的本地用户为用户A，点击进入隐私空间后，系统会将本地用户切换为用户B，如果此刻您使用归属用户A下的Push Token推送消息，则会返回该回执状态码。|
|27|应用进程不在，后台消息被缓存|在终端设备上目标应用进程不存在导致后台消息被缓存。|
|31|目标应用中不存在指向的页面|请参见[点击消息动作](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section697519219136)检查应用skills标签配置和消息请求体中的clickAction字段。|
|51|终端设备处于开机未解锁状态|用户重启终端设备后，点亮屏幕未解锁。|
|102|消息频控丢弃|系统会根据现网使用场景和流量进行管控，不合理的使用场景系统会进行频控。|
|144|profileId不存在|发送下行消息时请检查场景化消息payload中的[profileId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section17371529101117)字段。|
|151|推送消息未展示或卡片formId不存在|1. 请检查卡片是否已经添加到终端设备桌面。<br>2. 请检查卡片刷新消息中指定的[formId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section6471174713249)是否存在。|
|155|实况窗通知更新失败|请检查您的通知是否未创建或已经过期。|
|156|实况窗通知消息乱序更新|实况窗通知消息携带[version](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section66881469306)小于当前版本，更新失败。|
|158|创建的实况窗已存在|在设备中已存在通过Live View Kit创建的[activityId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section66881469306)相同的实况窗。|
|188|拉起应用失败|请稍后重试。|
|191|角标更新失败|系统内部设置角标异常。|
|256|消息频次限制|频次限制请参考消息发送[频次限制](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-msg-freq-control#section551882820368)。|
|259|消息被拒绝|1. 发送消息中存在违规内容。<br>2. 存在不安全的url。<br><br>请更换消息体内容或url。|
|261|卡片不存在|卡片刷新消息被Push服务端管控不下发（管控周期30天），建议做过滤处理减少无效推送。原因：不存在卡片刷新消息中指定[formId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section6471174713249)的卡片。<br><br>建议填写已分配过的formId，避免后续formId分配后，对应的卡片刷新消息被管控导致管控周期内无法下发。|
|262|卡片刷新次数达上限|卡片刷新消息被Push服务端管控不下发（管控周期1天），建议做过滤处理减少无效推送。原因：终端设备上对应的卡片刷新次数达到上限(未被Push服务端频次限制)。|
|264|消息未订阅|发送的订阅消息，但实际未订阅。|
|265|实况窗通知更新被管控|发送的[activityId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section66881469306)对应的实况窗通知不存在，限制发送该activityId的实况窗通知消息24小时。|
|268|未携带status字段|通过Push Kit创建的实况窗，在对该实况窗更新时未携带[status](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section66881469306)字段。|
|269|重复创建实况窗|通过Push Kit创建的实况窗重复（[activityId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-param#section66881469306)相同）。|

说明

您需要对上述状态中的2、5、6、10做过滤处理，减少对这些用户的无效推送。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-scenes-send "推送场景化消息")
# （可选）推送报告

更新时间: 2025-12-16 16:37

登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，点击“开发与服务”，在项目列表中找到您的项目，通过“增长 > 推送服务 > 推送报告”，您可以在“推送报告”中查看推送消息详情和推送用户详情。

说明

推送报告数据不是实时数据，当天生成的数据在控制台次日才能查看到。

## 推送消息详情

您可以查看推送消息的详情，场景化消息的统计图和对应表格，同时可以按照通道维度进行查看，有“通过AGC控制台”、“通过API方式”和“全部通道”**；**也可以按照消息类型维度进行查看。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163733.72443036447681086866710788994642:50001231000000:2800:1113E680EFB285528D924A403137F082F37C0F707D70939BA69D17165C9D116D.png "点击放大")

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163733.70062817264164458042379473445375:50001231000000:2800:E18217FE688B6159366D2673BBBBE2880228C5DF0684798ED3C7BABFFBA81D8B.png "点击放大")

点击自定义后的![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163733.36989922615489339651787612989773:50001231000000:2800:A7B99F3B23EFDE219D4289CC59A943C1721AD231AB27AC18F41E39D16117FB47.png)，可自定义推送消息报表展示的表格列，默认展示的表格列有：日期、消息类型、请求量、发送量、到达量、显示量、点击量、到达率（%）、点击率（%）、沉默设备丢弃、应用被卸载、无效TOKEN、通知关闭。全选可展示全部表格列，重置则恢复默认表格列。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163733.67871492046569469373140178884140:50001231000000:2800:2151349486525EF0D3F1F6DC0F68CD269A13C345E8B53FA89A4523346A6C558F.png "点击放大")

报表数据条目说明：

- 请求量：该推送任务预计覆盖的设备数量。
- 发送量：在请求量的基础上剔除不符合下发条件的消息数量，实际下发的消息数量。
- 到达量：扣除未触达量后实际到达的数量。
- 显示量：消息展示在通知栏的数量。
- 点击量：用户点击推送消息的数量。
- 到达率（%）：到达量/发送量。
- 点击率（%）：点击量/显示量。
- 沉默设备丢弃：终端设备超过30天没有联网的数量。
- 频控丢弃量：向单个设备发送消息超出上限，超出部分被丢弃的数量。
- 应用被卸载：用户已经卸载该应用并且没有重新安装的数量。
- 无效TOKEN：消息从云端发送到终端设备过程中，由于Token无效不展示的数量。
- 通知关闭：用户关闭了应用的消息通知权限的数量。
- 消息覆盖：待发送消息被覆盖的数量。针对待发送消息，只保留最新一条，其余待发送消息会被覆盖不下发。
- 其他原因：其他不满足触达条件的情况，如推送链接无法正常访问等。
- 过期量：目标设备离线，在消息有效期内设备未上线导致消息过期的数量。
- 缓存量：目标设备离线，消息仍在有效期内的数量。
- 未触达量：消息未到达终端设备的数量。

说明

不符合下发条件的消息数量包括：沉默设备丢弃、频控丢弃量、应用被卸载、无效TOKEN、通知关闭、消息覆盖、其他原因、过期量、缓存量。

## 推送用户详情

您可以查看推送用户的详情，根据时间维度查看活跃用户、新增用户和总用户的统计数据。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163734.54908754620730174297840518550873:50001231000000:2800:3B1DE0E9925F3ED49CB2B6BECBDD9AD9E6CD4605880E33513C4A74D4DB75657B.png "点击放大")

报表数据条目说明：

- 当天活跃用户数：当天设备与Push服务端建立连接的用户数量。
- 当天新增用户数：当天新安装的用户数量。不统计重复卸载安装应用场景。
- 30日活跃用户数：查询日往前30日内设备与Push服务端建立连接的用户数量。
- 总用户数：已安装的总用户数量。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-msg-receipt "（可选）开发消息回执")
# 如何处理推送消息时遇到的问题

更新时间: 2025-12-16 16:36

当使用REST API接口进行消息推送时，您可能遇到一些问题，请按照如下思路进行处理：

1. 优先检查[消息推送接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct)URL（https://push-api.cloud.huawei.com/**v3**/**[projectId]**/messages:send）是否正确。
    - 请使用v3版本的推送接口URL，不要使用v1或v2版本的推送接口URL，详情请参见[场景化消息中的请求URL版本问题](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-8)。
    - 请检查推送接口地址中的projectId，确保与您当前应用所属的项目保持一致，若不一致请更新推送接口URL中的projectId，并重新[生成鉴权令牌](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token)，应用重新[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)，再进行消息推送。
2. 若调用消息推送接口返回了错误码，请参见[业务响应码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-response#section204526160327)进行排查。
3. 若调用消息推送接口返回成功，但设备未展示消息，请参见[“如何处理云侧推送消息成功端侧消息未展示的问题”](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-2)进行排查。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq "Push Kit常见问题")
# 如何处理推送消息时遇到的问题

更新时间: 2025-12-16 16:36

当使用REST API接口进行消息推送时，您可能遇到一些问题，请按照如下思路进行处理：

1. 优先检查[消息推送接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct)URL（https://push-api.cloud.huawei.com/**v3**/**[projectId]**/messages:send）是否正确。
    - 请使用v3版本的推送接口URL，不要使用v1或v2版本的推送接口URL，详情请参见[场景化消息中的请求URL版本问题](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-8)。
    - 请检查推送接口地址中的projectId，确保与您当前应用所属的项目保持一致，若不一致请更新推送接口URL中的projectId，并重新[生成鉴权令牌](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-jwt-token)，应用重新[获取Push Token](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token)，再进行消息推送。
2. 若调用消息推送接口返回了错误码，请参见[业务响应码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-response#section204526160327)进行排查。
3. 若调用消息推送接口返回成功，但设备未展示消息，请参见[“如何处理云侧推送消息成功端侧消息未展示的问题”](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-2)进行排查。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq "Push Kit常见问题")
# 关于云侧接口推送成功但设备收不到推送消息的问题

更新时间: 2025-12-16 16:36

云侧消息下发成功后，可能会因为消息频控、通知开关未打开等原因，导致端侧消息未展示。

## 收不到推送消息的可能原因

- 消息被频控，请检查是否[开通消息自分类权益](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section15809122792917)。调测阶段建议发送测试消息，详情请参见[关于通知消息被频控的问题](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-5)。
- 终端设备的网络连接异常。如终端设备切到测试环境，且未连接外部网络。
- 终端的通知开关关闭。
- 使用的Push Token已经失效，如应用已卸载，未安装等（Push Token失效原因请参见[场景介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-get-token#section123091617105820)），请重新生成Push Token发送消息。
- 应用在前台，推送的是通知扩展消息（[push-type](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-scenariozed-api-request-struct#section20573634202313)为2）。请将应用切至后台重新推送通知扩展消息，或重新推送普通通知消息（push-type字段设置为0）。
- skills标签配置问题，正确的配置方法请参见[点击消息动作](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert#section697519219136)。
- 检查消息是否是静默通知。发送了资讯营销类的消息，或是未申请自分类权益，都会静默通知。当收到消息时，由于静默通知仅在通知中心展示，并不会锁屏和横幅通知、响铃和振动，需要去通知中心查看。

## 如何定位此类问题

1. Push Kit建议您[开发消息回执](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-msg-receipt)，Push服务端会将消息送达状态以回执消息形式发送给您的应用回执服务端，您可通过[回执状态码](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-msg-receipt#section19100519195717)定位问题。
2. 您还可以登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)进行消息追踪和token信息查询，查询路径：“开发与服务 > 增长 > 推送服务 > 自助分析（Beta）”。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-1 "如何处理推送消息时遇到的问题")
# 如何处理误分类问题

更新时间: 2025-12-16 16:37

## 如何处理应用类别误分类

未发布应用，可以登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，点击“应用上架”，在应用列表中找到您的应用，修改应用分类。关于应用分类信息，请参见[华为应用市场应用分类示例](https://developer.huawei.com/consumer/cn/doc/50103)。

## 如何处理通知消息类别误分类

应用在不违反[通知违规处罚标准](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-punishment-standards)的前提下推送消息，可按要求[申请通知消息自分类权益](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section16708911111611)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-2 "关于云侧接口推送成功但设备收不到推送消息的问题")
# 要实现即时聊天功能应该使用什么类型的场景化消息？

更新时间: 2025-12-16 16:37

可以使用通知消息和通知扩展消息，详情请参见[发送通知消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert)、[发送通知扩展消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-extend-noti)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-9 "应用处于后台时应用内如何接收消息")
# 要实现即时聊天功能应该使用什么类型的场景化消息？

更新时间: 2025-12-16 16:37

可以使用通知消息和通知扩展消息，详情请参见[发送通知消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-alert)、[发送通知扩展消息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-send-extend-noti)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-faq-9 "应用处于后台时应用内如何接收消息")
# 通知违规处罚标准

更新时间: 2025-12-16 16:36

## 违规分类、违规行为及违规处罚标准

说明

当您的应用存在违规行为时，Push Kit会向应用的开发者账号发送违规通知邮件或短信，请您按照邮件或短信中提供的步骤查看违规处罚详情。

|**违规分类及违规行为**|**违规处罚标准**|
|:--|:--|
|**类型一：违反通知样式、通知跳转、通知内容、通知分类、通知开关授权等，影响用户体验。**<br><br>**[通知样式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-specification#section66741239491)****违规**<br><br>- 伪造成其他应用推送消息，包括伪造应用名称、icon和消息内容等。<br>- 应用通知隐藏应用自身的名称和icon。<br>- 发送不符合设计规范的通知样式。<br>- 滥用通知样式，如设置通知背景图或更改推送文案颜色等。<br>- 更改一键删除按钮。<br>- 重复发送相同内容的通知打扰用户。<br>- 通知标题与文本内容重复。<br>- 利用当前系统内仍存在的通知，将特定通知强制置顶显示。<br>- 未经授权，强行将通知置顶。<br>- 通知无法直接删除。<br>- 伪造横幅通知、锁屏通知。<br><br>**[通知跳转](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-specification#section1792717184810)****违规**<br><br>- 以推送消息为手段，故意在后台拉起应用进程。<br>- 以推送消息为手段，利用本应用唤醒其他应用。<br>- 利用推送消息诱导下载安装第三方应用。<br>- 通知点击跳转链接为非法网站。<br><br>**[通知内容原则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-detail-rules#section146985016916)****违规**<br><br>- 违反通知内容一致性原则、真实客观原则、可读性原则及合规性原则。<br><br>**通知分类违规**<br><br>- 通知分类错误，违反[通知消息分类标准与提醒方式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1924971516101)。<br><br>**[通知开关授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-specification#section02319296486)****违规**<br><br>- 首次启动时未弹窗询问用户是否允许通知。<br>- 通知未经用户授权而默认开启。<br>- 将多个事件通知放在一个授权开关内诱导用户一键开启。<br><br>**其他**<br><br>- 应用间互相恶意“保活”。<br>- 其他影响华为终端用户体验的行为。<br><br>说明<br><br>恶意“保活”：指的是未经过用户允许和非正常业务需要的场景下，将应用进程拉起。|近12个月内：<br><br>- **首次违规**：邮件警告。7个自然日内未完成整改，按二次违规处罚。<br>- **二次违规**：暂停应用发送资讯营销消息7个自然日。7个自然日内未完成整改，按三次违规处罚。<br>- **三次及以上违规**：90个自然日内所有消息归为静默提醒，所有消息统一限频2条/天。<br><br>注意<br><br>- 违规应用需在违规警告发出的7个自然日内完成整改，并反馈整改结果，否则平台将加重处罚。<br>- 应用提交整改反馈时，请参考[整改承诺声明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-punishment-standards#section19877944201013)。|
|**类型二：违反法律法规**|禁用华为推送；按行政监管机构要求，禁用至处罚指令解除。|
|**类型三：****违反实况窗样式、场景使用规范，影响用户体验**<br><br>**样式违规**<br><br>- 使用不符合规范的实况窗样式。<br><br>**[场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/liveview-introduction)使用违规**<br><br>- 非用户主动行为触发的实况窗通知，用户对通知内容无明确的预期。<br>- 实况窗用于营销、广告场景或其他未经评审的场景。<br>- 实况窗具体使用场景与应用实际申请通过的场景不一致。|应用需在收到违规处罚通知的3个自然日内完成整改，并反馈整改结果，否则将回收违规场景的实况窗通知权益。<br><br>注意<br><br>应用提交整改反馈时，请参考[整改承诺声明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-punishment-standards#section19877944201013)。|

## 整改承诺声明

应用提交整改反馈时，需提供**带有该违规应用上架主体公司盖章**的《整改承诺声明》，具体内容如下：

致：华为软件技术有限公司

本公司的应用：应用名称：***（以下简称“该应用”）、APP ID/应用包名：***，***版本，在使用Push Kit（推送服务）期间，于__年__月__日，因_______原因（“违规情况”）被处罚。

本公司在此确认，针对违规情况，整改措施如下：

问题一：***

整改措施：

问题二：***

整改措施：

整改完成时间：__年__月__日

本公司承诺将遵守适用的法律法规，在使用Push Kit期间，已仔细阅读并同意遵守《华为推送服务协议》《Push Kit接入规范》等相关的协议条款。若本公司再次出现任何违反适用法律法规或前述协议条款的情形，本公司同意接受华为对该应用和/或本公司的处理，并独立承担关于该应用的全部问题和责任；如给华为及其关联公司、合作伙伴或其他第三方造成损失的，本公司将承担全部责任并赔偿由此造成的一切损失。

特此声明和保证。

## 违规处罚申诉

根据违规处理规定，应用出现违规行为，其对应的推送权益可能受到影响。

若您对应用违规处罚判定有异议，您可以通过下述路径查看违规处罚详情，并在收到违规处罚通知后三个工作日内进行申诉（同一违规事件仅允许三次申诉）。

违规处罚详情查看路径：登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，点击“开发与服务”，在项目列表中找到您的项目，点击“项目设置 > 增长 > 推送服务”，找到“配置 > 项目状态”，进入违规处罚页面，即可查看和处理违规处罚。

我们将根据您申诉的合理性、申诉材料真实性、违规影响范围进行评议，并反馈结果。若申诉评议通过，可酌情减轻处罚。

如有疑问，请发送邮件至[hwpush@huawei.com](mailto:hwpush@huawei.com)咨询。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-detail-rules "通知内容管理细则")
# 通知违规处罚标准

更新时间: 2025-12-16 16:36

## 违规分类、违规行为及违规处罚标准

说明

当您的应用存在违规行为时，Push Kit会向应用的开发者账号发送违规通知邮件或短信，请您按照邮件或短信中提供的步骤查看违规处罚详情。

|**违规分类及违规行为**|**违规处罚标准**|
|:--|:--|
|**类型一：违反通知样式、通知跳转、通知内容、通知分类、通知开关授权等，影响用户体验。**<br><br>**[通知样式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-specification#section66741239491)****违规**<br><br>- 伪造成其他应用推送消息，包括伪造应用名称、icon和消息内容等。<br>- 应用通知隐藏应用自身的名称和icon。<br>- 发送不符合设计规范的通知样式。<br>- 滥用通知样式，如设置通知背景图或更改推送文案颜色等。<br>- 更改一键删除按钮。<br>- 重复发送相同内容的通知打扰用户。<br>- 通知标题与文本内容重复。<br>- 利用当前系统内仍存在的通知，将特定通知强制置顶显示。<br>- 未经授权，强行将通知置顶。<br>- 通知无法直接删除。<br>- 伪造横幅通知、锁屏通知。<br><br>**[通知跳转](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-specification#section1792717184810)****违规**<br><br>- 以推送消息为手段，故意在后台拉起应用进程。<br>- 以推送消息为手段，利用本应用唤醒其他应用。<br>- 利用推送消息诱导下载安装第三方应用。<br>- 通知点击跳转链接为非法网站。<br><br>**[通知内容原则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-detail-rules#section146985016916)****违规**<br><br>- 违反通知内容一致性原则、真实客观原则、可读性原则及合规性原则。<br><br>**通知分类违规**<br><br>- 通知分类错误，违反[通知消息分类标准与提醒方式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-apply-right#section1924971516101)。<br><br>**[通知开关授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-specification#section02319296486)****违规**<br><br>- 首次启动时未弹窗询问用户是否允许通知。<br>- 通知未经用户授权而默认开启。<br>- 将多个事件通知放在一个授权开关内诱导用户一键开启。<br><br>**其他**<br><br>- 应用间互相恶意“保活”。<br>- 其他影响华为终端用户体验的行为。<br><br>说明<br><br>恶意“保活”：指的是未经过用户允许和非正常业务需要的场景下，将应用进程拉起。|近12个月内：<br><br>- **首次违规**：邮件警告。7个自然日内未完成整改，按二次违规处罚。<br>- **二次违规**：暂停应用发送资讯营销消息7个自然日。7个自然日内未完成整改，按三次违规处罚。<br>- **三次及以上违规**：90个自然日内所有消息归为静默提醒，所有消息统一限频2条/天。<br><br>注意<br><br>- 违规应用需在违规警告发出的7个自然日内完成整改，并反馈整改结果，否则平台将加重处罚。<br>- 应用提交整改反馈时，请参考[整改承诺声明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-punishment-standards#section19877944201013)。|
|**类型二：违反法律法规**|禁用华为推送；按行政监管机构要求，禁用至处罚指令解除。|
|**类型三：****违反实况窗样式、场景使用规范，影响用户体验**<br><br>**样式违规**<br><br>- 使用不符合规范的实况窗样式。<br><br>**[场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/liveview-introduction)使用违规**<br><br>- 非用户主动行为触发的实况窗通知，用户对通知内容无明确的预期。<br>- 实况窗用于营销、广告场景或其他未经评审的场景。<br>- 实况窗具体使用场景与应用实际申请通过的场景不一致。|应用需在收到违规处罚通知的3个自然日内完成整改，并反馈整改结果，否则将回收违规场景的实况窗通知权益。<br><br>注意<br><br>应用提交整改反馈时，请参考[整改承诺声明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-punishment-standards#section19877944201013)。|

## 整改承诺声明

应用提交整改反馈时，需提供**带有该违规应用上架主体公司盖章**的《整改承诺声明》，具体内容如下：

致：华为软件技术有限公司

本公司的应用：应用名称：***（以下简称“该应用”）、APP ID/应用包名：***，***版本，在使用Push Kit（推送服务）期间，于__年__月__日，因_______原因（“违规情况”）被处罚。

本公司在此确认，针对违规情况，整改措施如下：

问题一：***

整改措施：

问题二：***

整改措施：

整改完成时间：__年__月__日

本公司承诺将遵守适用的法律法规，在使用Push Kit期间，已仔细阅读并同意遵守《华为推送服务协议》《Push Kit接入规范》等相关的协议条款。若本公司再次出现任何违反适用法律法规或前述协议条款的情形，本公司同意接受华为对该应用和/或本公司的处理，并独立承担关于该应用的全部问题和责任；如给华为及其关联公司、合作伙伴或其他第三方造成损失的，本公司将承担全部责任并赔偿由此造成的一切损失。

特此声明和保证。

## 违规处罚申诉

根据违规处理规定，应用出现违规行为，其对应的推送权益可能受到影响。

若您对应用违规处罚判定有异议，您可以通过下述路径查看违规处罚详情，并在收到违规处罚通知后三个工作日内进行申诉（同一违规事件仅允许三次申诉）。

违规处罚详情查看路径：登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，点击“开发与服务”，在项目列表中找到您的项目，点击“项目设置 > 增长 > 推送服务”，找到“配置 > 项目状态”，进入违规处罚页面，即可查看和处理违规处罚。

我们将根据您申诉的合理性、申诉材料真实性、违规影响范围进行评议，并反馈结果。若申诉评议通过，可酌情减轻处罚。

如有疑问，请发送邮件至[hwpush@huawei.com](mailto:hwpush@huawei.com)咨询。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-detail-rules "通知内容管理细则")
