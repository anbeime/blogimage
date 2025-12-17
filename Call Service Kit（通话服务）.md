# Call Service Kit简介

更新时间: 2025-12-16 16:35

Call Service Kit（通话服务）是HarmonyOS为开发者提供的应用内通话管理服务。

开发者通过集成Call Service Kit，可以实现便捷的来电一键接听、横幅通知、静音与取消静音等功能，提升用户体验。

## 场景分类

应用内通话，主要分为来电场景、去电场景两类。

- 来电场景
    
    应用接收到来自网络的音/视频通话，称为来电场景。
    
    在来电场景中，应用需要将来电信息上报给Call Service Kit，系统会为用户展示来电横幅通知。用户可以在横幅上执行接听或拒接来电、静音与解除静音、挂断通话等操作。
    
    此外，Call Service Kit还支持锁屏来电通知、多路来电通知等。
    
- 去电场景
    
    应用主动发起音/视频通话，称为去电场景。去电场景与来电场景大部分功能相似，但有以下几点区别：
    
    - 去电时，由于应用在前台，不需要展示横幅通知，只在屏幕左上角展示通话胶囊。
    - 去电不支持多路共存，即同一时间，只能有1路去电存在。

## 与相关Kit的关系

当应用在后台时，如果有来电，需要[Push Kit（推送服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-kit-guide)先拉起应用主进程，应用才能给Call Service Kit上报来电。

业务流程如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163556.03190566050000807460685091125155:50001231000000:2800:12B2AAD0C64CE59939CCD1831BE354A3AF23B60FCED4D87D097C3B4CCDF3D98E.jpg "点击放大")

## 约束和限制

### 设备限制

本示例仅支持标准系统上运行，不支持模拟器。

|能力|支持设备|
|:--|:--|
|来电场景|Phone、Tablet，Wearable。|
|去电场景|Phone、Tablet，Wearable。|
|企业联系人信息来去电页面显示|Phone、Tablet、PC/2in1、Wearable。|

### 通话数量

- 同一时间，最多支持3路应用内来电。
- 同一时间，最多支持1路应用内去电。

### 支持的国家/地区

Call Service Kit提供的能力当前只支持中国大陆。

### 相关Kit的约束和限制

由于Call Service Kit依赖Push Kit，还需要参考[Push Kit的约束和限制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-kit-introduction#section15315537123318)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/call-kit-guide "Call Service Kit（通话服务）")
# 开发准备

更新时间: 2025-12-16 16:36

在开通应用内通话服务之前，请先参考“[应用开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview)”完成基本准备工作，再继续进行以下开发活动。

## 开通Push Kit（推送服务）

如[与其他Kit的关系](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/call-introduction#section194981821202916)所述，开发者在开通Call Service Kit之前，需要开通Push Kit（推送服务），开通方法详见[开通推送服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-config-setting)。

## 申请权限

开发者需要根据实际场景申请对应权限，具体申请方式请参见[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)。

|权限|使用场景|备注|
|:--|:--|:--|
|[ohos.permission.MICROPHONE](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/permissions-for-all-user#ohospermissionmicrophone)|用于在语音通话中，使用麦克风。|必须申请。|
|[ohos.permission.CAMERA](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/permissions-for-all-user#ohospermissioncamera)|用于在视频通话中，使用相机。|如果应用支持视频通话业务，则需要申请。|

## 示例代码

该指南涉及到的示例代码均为片段，全量示例代码请参考：[Samplecode](https://gitcode.com/harmonyos_samples/callkit-samplecode-voipdemo-arkts)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/call-introduction "Call Service Kit简介")
# 来电场景

更新时间: 2025-12-16 16:36

## 场景介绍

应用接收到来自网络的音/视频通话，称为来电场景。

来电场景的效果图展示如下：

|   |   |   |
|---|---|---|
|**语音来电**|**视频来电**|**视频来电（不支持语音接听**）|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163612.24408948198320770951031277556993:50001231000000:2800:6CCC7D2F26CE3B8A7048C3622F5185CABCF5F16E8864E771B98065EB8EA2BC99.jpg "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163612.05107432867698046283173894667140:50001231000000:2800:79ED9BE5B85185A911E18B8F22B255E9AC0C51B64E56C9187073772F2AED1A73.jpg "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163612.94671777756240777185972813529687:50001231000000:2800:4B71A9F934EF87C17C91A0458B8990E968D01BF6781BEBA97EB16F1022D8A1CF.jpg "点击放大")|
|**通话中**|**锁屏语音来电**|**锁屏视频来电**|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163612.29068783223579340130023180730999:50001231000000:2800:2B032023633C352B3C32777CB2F086EFFAD3DC3BB460681BCC3EE7103611B609.jpg "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163612.27388820897467986443007059402169:50001231000000:2800:5FE36FBEDD5C9E8E956FEABF19C10E296A2B7C990E6D13CA56374490E0EAE1CB.jpg "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163612.18003658573065187474388120340208:50001231000000:2800:D134C650CE9E9EF907B95418B30923E11B25D4FB24FB2EF340FD148D6050E34B.jpg "点击放大")|

## 约束与限制

来电场景支持Phone、Tablet设备，并从6.0(20)版本开始支持Wearable设备。

## 业务流程

### 来电场景：接听流程图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163612.71273917420645823530856211408837:50001231000000:2800:31F34A8F0D20131277EB84CFA5CBF8C438FC0C985851AA82970DBB2BB4DD052D.jpg "点击放大")

### 来电场景：拒接流程图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163613.07750843291616302475625023057143:50001231000000:2800:F7E064DB4FD29DEC98BA14347D325E88B49F26B4F1BB761877EDECAFFAFA6B41.jpg "点击放大")

## 接口说明

来电场景的接口，由[voipCall](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall)提供。更多接口信息详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall)。

|接口名|描述|
|:--|:--|
|on(type: 'voipCallUiEvent', callback: Callback<VoipCallUiEventInfo>): void|订阅voipCallUiEvent事件。|
|off(type: 'voipCallUiEvent', callback?: Callback<VoipCallUiEventInfo>): void|取消订阅voipCallUiEvent事件。|
|reportIncomingCall(voipCallAttribute: VoipCallAttribute): Promise<ErrorReason>|上报来电。|
|reportCallAudioEventChange(callId: string, callAudioEvent: CallAudioEvent): Promise<void>|上报音频事件。|
|reportCallStateChange(callId: string, callState: VoipCallState): Promise<void>|上报通话状态改变。|
|reportCallStateChange(callId: string, callState: VoipCallState, callType: VoipCallType): Promise<void>|上报通话状态改变，并指定通话类型。|

#### 开发步骤

1. 导入相关依赖。
    
    1. import { voipCall } from '@kit.CallServiceKit';
    2. import { image } from '@kit.ImageKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 为了感知到用户在横幅通知上做的接听、挂断、静音与解除静音等操作，应用需要注册voipCallUiEvent事件。建议在上报来电之前注册。
    
    示例代码如下：
    
    1. // 注册voipCallUiEvent事件
    2. voipCall.on('voipCallUiEvent', callback => {
    3.   hilog.info(0x0000, 'CallDemo', 'Succeeded in registering voipCallUiEvent');
    4. });
    
3. 应用内部建立通话连接之后，需要向Call Service Kit上报来电，并携带通话信息，详见[VoipCallAttribute](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section4221135015444)。
    
    如果当时应用在后台，系统会展示来电横幅。
    
    示例代码如下：
    
    1. // 构造上报来电的参数
    2. let voipCallAttribute: voipCall.VoipCallAttribute = {
    3.   callId: '1234567890',
    4.   voipCallType: voipCall.VoipCallType.VOIP_CALL_VOICE,
    5.   userName: 'Callman',
    6.   userProfile: image.createPixelMapSync(new ArrayBuffer(100), { size: { width: 90, height: 90 } }),
    7.   abilityName: 'VoipCallAbility',
    8.   voipCallState: voipCall.VoipCallState.VOIP_CALL_STATE_RINGING,
    9.   showBannerForIncomingCall: true
    10. };
    
    11. // 上报来电
    12. voipCall.reportIncomingCall(voipCallAttribute).then(errorReason => {
    13.   if (errorReason == voipCall.ErrorReason.ERROR_NONE) {
    14.     hilog.info(0x0000, 'CallDemo', 'Succeeded in reporting the incoming call');
    15.   } else {
    16.     hilog.error(0x0000, 'CallDemo', 'Failed to report the incoming call: %{public}d', errorReason);
    17.   }
    18. });
    
    对于视频通话，可以通过参数[isVoiceAnswerSupported](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section4221135015444)指定是否允许语音接听，示例代码如下：
    
    19. // 构造上报来电的参数
    20. let voipCallAttribute: voipCall.VoipCallAttribute = {
    21.   callId: '1234567890',
    22.   voipCallType: voipCall.VoipCallType.VOIP_CALL_VIDEO,
    23.   userName: 'Jack',
    24.   userProfile: image.createPixelMapSync(new ArrayBuffer(100), { size: { width: 90, height: 90 } }),
    25.   abilityName: 'VoipCallAbility',
    26.   voipCallState: voipCall.VoipCallState.VOIP_CALL_STATE_RINGING,
    27.   showBannerForIncomingCall: true,
    28.   isVoiceAnswerSupported: false  // 视频通话不支持语音接听
    29. };
    
4. 接收到来电之后，用户可以选择接听或拒接。
    
    接听有两种开发方式：上报两次状态、只上报一次状态。
    
    - 上报两次状态（推荐）。
        
        以语音通话为例，应用在接收到[VOIP_CALL_EVENT_VOICE_ANSWER](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section26961727970)事件回调之后，立即向Call Service Kit上报[VOIP_CALL_STATE_ANSWERED](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section24523814719)状态，并同时执行应用内接听。
        
        在完成应用内接听之后，再向Call Service Kit上报[VOIP_CALL_STATE_ACTIVE](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section24523814719)状态，系统会更新通话横幅。
        
        示例代码如下：
        
        1. voipCall.on('voipCallUiEvent', callback => {
        2.   if (callback?.voipCallUiEvent == voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_VOICE_ANSWER) {
        3.     // 立即向Call Service Kit上报answered状态
        4.     voipCall.reportCallStateChange(callback.callId, voipCall.VoipCallState.VOIP_CALL_STATE_ANSWERED);
        
        5.     //...在应用内完成接听
        
        6.     // 应用内接听后，向Call Service Kit上报active状态
        7.     voipCall.reportCallStateChange(callback.callId, voipCall.VoipCallState.VOIP_CALL_STATE_ACTIVE);
        8.   }
        9. });
        
        接听过程的效果图展示如下：
        
        |   |   |
        |---|---|
        |**正在接通**|**接通后**|
        |![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163613.45629470647512557706546215828184:50001231000000:2800:D0CA6E3ACC526C3CF39566952F9C557F6DDF87027C3CFB165329A4B2B2DF51C4.jpg "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163613.35408075296723299244900872953596:50001231000000:2800:8D6629191532DDB03842D4301F421B8CDBFFBD1B8916A420C6D82A69C8CCAEEF.jpg "点击放大")|
        
        说明
        
        通话接听时，上报两次状态的好处是：
        
        因为网络等原因，从用户点击接听，到通话真正被接通的时间间隔可能比较长（比如，1s左右）。这段时间，如果横幅通知的样式不变，一直停留在来电状态，用户可能认为点击接听无响应，体验不好。
        
        上报两次状态，可以在接听的过程中，在界面上给用户以反馈。
        
    - 只上报一次状态。
    
    以语音通话为例，应用在接收到[VOIP_CALL_EVENT_VOICE_ANSWER](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section26961727970)事件回调之后，执行应用内接听。
    
    一直到完成应用内接听后，再向Call Service Kit上报[VOIP_CALL_STATE_ACTIVE](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section24523814719)状态。
    
    示例代码如下：
    
    1. voipCall.on('voipCallUiEvent', callback => {
    2.   if (callback?.voipCallUiEvent == voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_VOICE_ANSWER) {
    3.     //...在应用内完成接听
    
    4.     // 应用内接听后，向Call Service Kit上报通话状态
    5.     voipCall.reportCallStateChange(callback.callId, voipCall.VoipCallState.VOIP_CALL_STATE_ACTIVE);
    6.   }
    7. });
    
    如果用户在横幅通知上点击拒接，则应用在接收到[VOIP_CALL_EVENT_REJECT](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section26961727970)事件回调之后，在应用内完成拒接，然后向Call Service Kit 上报[VOIP_CALL_STATE_DISCONNECTED](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section24523814719)状态，系统会取消横幅通知。
    
    拒接之后，应用可跳过5、6步，直接看第7步。
    
    拒接的示例代码如下：
    
    8. voipCall.on('voipCallUiEvent', callback => {
    9.   if (callback?.voipCallUiEvent == voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_REJECT) {
    10.     // ...应用内完成拒接
    
    11.     // 向Call Service Kit上报通话状态
    12.     voipCall.reportCallStateChange(callback.callId, voipCall.VoipCallState.VOIP_CALL_STATE_DISCONNECTED);
    13.   }
    14. });
    
5. 在通话过程中，用户可以根据需要，可以静音或解除静音。
    
    以静音为例，用户在横幅上点击静音，Call Service Kit会给应用回调[VOIP_CALL_EVENT_MUTED](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section26961727970)事件。
    
    应用在完成静音后，应向Call Service Kit上报[AUDIO_EVENT_MUTED](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section312217120409)音频状态。
    
    示例代码如下：
    
    1. voipCall.on('voipCallUiEvent', callback => {
    2.   if (callback?.voipCallUiEvent == voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_MUTED) {
    3.     // 向Call Service Kit上报静音
    4.     voipCall.reportCallAudioEventChange(callback.callId, voipCall.CallAudioEvent.AUDIO_EVENT_MUTED);
    5.   } else if (callback?.voipCallUiEvent == voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_UNMUTED) {
    6.     // 向Call Service Kit上报解除静音
    7.     voipCall.reportCallAudioEventChange(callback.callId, voipCall.CallAudioEvent.AUDIO_EVENT_UNMUTED);
    8.   }
    9. });
    
    静音、解除静音的横幅通知效果图展示如下：
    
    |   |   |
    |---|---|
    |**静音**|**解除静音**|
    |![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163613.09184017403645352139622611410588:50001231000000:2800:89BCBB80B4D761D1734EA1D51E12EC8ACF081EA9FB2B5733113FE028DEF1D6F2.jpg "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163613.47492276596854569085090413262202:50001231000000:2800:7AEBE9F18C06937DEF124C88B66EB0413F81C9E6623AEAF82E0BD898263A2C86.jpg "点击放大")|
    
6. 用户在横幅点击挂断，Call Service Kit会给应用回调[VOIP_CALL_EVENT_HANGUP](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section26961727970)事件。
    
    应用收到该事件后，应在应用内完成挂断，然后，向Call Service Kit上报[VOIP_CALL_STATE_DISCONNECTED](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section24523814719)状态，系统会取消横幅通知。
    
    示例代码如下：
    
    1. voipCall.on('voipCallUiEvent', callback => {
    2.   if (callback?.voipCallUiEvent == voipCall.VoipCallUiEvent.VOIP_CALL_EVENT_HANGUP) {
    3.     // ...应用内完成挂断
    
    4.     // 向Call Service Kit上报通话状态
    5.     voipCall.reportCallStateChange(callback.callId, voipCall.VoipCallState.VOIP_CALL_STATE_DISCONNECTED);
    6.   }
    7. });
    
7. 通话结束后，应用不再需要感知到用户在通话横幅上的操作，可以解除voipCallUiEvent事件。
    
    示例代码如下：
    
    1. // 解除voipCallUiEvent事件
    2. voipCall.off('voipCallUiEvent', callback => {
    3.   hilog.info(0x0000, 'CallDemo', `Succeeded in unRegistering voipCallUiEvent, callId: ${callback.callId}`);
    4. });
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/call-preparations "开发准备")
# 去电场景

更新时间: 2025-12-16 16:36

## 场景介绍

应用主动发起音/视频通话，称为去电场景。

去电场景，由于应用在前台，不需要横幅通知，只在屏幕左上角，展示通话胶囊。去电场景的效果图展示如下：

|   |   |   |   |
|---|---|---|---|
|**语音去电(正在呼叫)**|**语音去电（通话中）**|**视频去电****（正在呼叫）**|**视频去电（通话中）**|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163614.39623149962362629187827005273913:50001231000000:2800:8D3D55FF8E31C1E52DF6F0B7C6151436D9C53F7E181E649DB0315B616DE445AA.jpg "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163614.65766252244096584275253711557126:50001231000000:2800:D9182D0E5F20BFCC09CBA9FC13B68BFA416DD0BCF0DF13FC4C328ED6B3037879.jpg "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163614.31562966105367660282725380802232:50001231000000:2800:4A942E1A8242E0D9F59B1146312561672B533826D30704E6F71E609577939E4D.jpg "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163614.97745542627338681748716618926296:50001231000000:2800:0147EBC5839C05FB042F8BD3D836CBCE62F293A4CD4A31A376BA1C47E694667F.jpg "点击放大")|

去电场景，用户也可以拉起通知中心面板，在实况窗横幅上做静音与解除静音、挂断通话等操作。

|   |   |
|---|---|
|**去电实况窗通知（正在呼叫）**|**去电实况窗通知（通话中）**|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163614.55111408823747828751315214598442:50001231000000:2800:319D2F1B6F28EEC71943BABE68DAF69F72B49BE74735EAF052F339317D7CE717.jpg "点击放大")|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.48213860232623641019887307369160:50001231000000:2800:95654A2142C9B5424549A2E2E67D9259B1995355EF16AAAA9580D944F6B41518.jpg "点击放大")|

## 约束与限制

去电场景支持Phone、Tablet设备，并从6.0(20)版本开始支持Wearable设备。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.91425137374329683688378135790250:50001231000000:2800:B6685F1829988C7BF418EEB2561F3067B9C8A1DA935DA691AD36D253C9B63067.jpg "点击放大")

## 接口说明

去电场景的接口，由[voipCall](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall)提供。更多接口信息详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall)。

|接口名|描述|
|:--|:--|
|on(type: 'voipCallUiEvent', callback: Callback<VoipCallUiEventInfo>): void|订阅voipCallUiEvent事件。|
|off(type: 'voipCallUiEvent', callback?: Callback<VoipCallUiEventInfo>): void|取消订阅voipCallUiEvent事件。|
|reportOutgoingCall(voipCallAttribute: VoipCallAttribute): Promise<ErrorReason>|上报去电。|
|reportCallAudioEventChange(callId: string, callAudioEvent: CallAudioEvent): Promise<void>|上报音频事件。|
|reportCallStateChange(callId: string, callState: VoipCallState): Promise<void>|上报通话状态改变。|
|reportCallStateChange(callId: string, callState: VoipCallState, callType: VoipCallType): Promise<void>|上报通话状态改变，并指定通话类型。|

## 开发步骤

去电场景的开发步骤与来电场景相似。

1. 导入相关依赖。
    
    1. import { voipCall } from '@kit.CallServiceKit';
    2. import { image } from '@kit.ImageKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 为了感知到用户在实况窗上做的静音与解除静音、挂断通话等操作，应用需要注册voipCallUiEvent事件。建议在上报去电之前注册。
    
    示例代码如下：
    
    1. // 注册voipCallUiEvent事件
    2. voipCall.on('voipCallUiEvent', callback => {
    3.   hilog.info(0x0000, 'CallDemo', 'Succeeded in registering voipCallUiEvent');
    4. });
    
3. 应用内部建立通话连接之后，需要向Call Service Kit上报去电，并携带通话信息，详见[VoipCallAttribute](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section4221135015444)。
    
    系统会在屏幕左上角，展示通话胶囊。
    
    以语音去电为例，示例代码如下：
    
    1. // 构建上报去电的参数
    2. let voipCallAttribute: voipCall.VoipCallAttribute = {
    3.   callId: '1234567890',
    4.   voipCallType: voipCall.VoipCallType.VOIP_CALL_VOICE,
    5.   userName: 'Jack',
    6.   userProfile: image.createPixelMapSync(new ArrayBuffer(100), { size: { width: 90, height: 90 } }),
    7.   abilityName: 'VoipCallAbility',
    8.   voipCallState: voipCall.VoipCallState.VOIP_CALL_STATE_DIALING,  // 去电的状态必须是DIALING
    9.   showBannerForIncomingCall: true
    10. };
    
    11. // 向Call Service Kit上报去电
    12. voipCall.reportOutgoingCall(voipCallAttribute).then(errorReason => {
    13.   if (errorReason == voipCall.ErrorReason.ERROR_NONE) {
    14.     hilog.info(0x0000, 'CallDemo', 'Succeeded in reporting the outgoing call');
    15.   } else {
    16.     hilog.error(0x0000, 'CallDemo', 'Failed to report the outgoing call: %{public}d', errorReason);
    17.   }
    18. });
    
    注意
    
    上报去电时，通话状态必须是VOIP_CALL_STATE_DIALING，否则Call Service Kit会认为参数不合法而返回[1007200001错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-error-code#section13010304159)。
    
4. 如果对端接听，应用需要向Call Service Kit上报通话状态[VOIP_CALL_STATE_ACTIVE](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section24523814719)。系统会更新通话胶囊，开始展示通话计时。
    
    示例代码如下：
    
    1. // ...应用服务器收到对端接听的消息
    2. let answeredCallId = '123456';
    
    3. // 向Call Service Kit上报通话状态
    4. voipCall.reportCallStateChange(answeredCallId, voipCall.VoipCallState.VOIP_CALL_STATE_ACTIVE);
    
5. 去电场景，用户也可以拉起通知中心面板，在实况窗通知上执行静音或解除静音。
    
    开发方法与来电场景相同，详见[来电场景：静音与解除静音](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/incoming-calls#li161271020155311)。
    
6. 去电场景，用户也可以拉起通知中心面板，在实况窗通知上点击挂断。
    
    开发方式与来电场景相同，详见[来电场景：用户点击挂断](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/incoming-calls#li12946111323712)。
    
7. 通话结束后，可以解除voipCallUiEvent事件。
    
    示例代码如下：
    
    1. // 解除voipCallUiEvent事件
    2. voipCall.off('voipCallUiEvent', callback => {
    3.   hilog.info(0x0000, 'CallDemo', `Succeeded in unRegistering voipCallUiEvent, callId: ${callback.callId}`);
    4. });
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/incoming-calls "来电场景")
# 企业联系人信息来去电页面显示

更新时间: 2025-12-16 16:36

本功能仅供企业应用开发者接入。

## 场景介绍

来去电时，页面显示已安装企业应用的联系人信息，方便用户识别来去电人信息，快速回应，增强企业内部沟通效率。

说明

来去电页面或横幅仅展示一个联系人信息，对于多个应用里存在相同联系人的情况，按照应用包名的字典序排序，展示首个查询结果。

## 接口说明

具体API说明详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/callservicekit-callerinfoquery-extension-ability#section1220554318191)。

|接口名|描述|
|:--|:--|
|onQueryCallerInfo(phoneNumber: string)：Promise<CallerInfo>|查询联系人信息接口|

## 申请接入

该API使用受限，如需接入需要申请，方式如下：

企业应用开发者将申请信息发送至公共邮箱agconnect@huawei.com。

邮件标题：【申请公司名】—企业来电显示能力—Developer ID

邮件内容需包括：开发者接入企业来电显示能力的应用使用主体、应用名称、应用ID、应用包名、场景说明（具体描述该应用对应通讯录量级等使用的必要信息）。

## 替换调试Profile

当企业联系人信息来去电页面显示能力申请成功后，需要重新[申请调试Profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-debugprofile-0000001914423102)。并且在DevEco Studio中替换新申请的调试Profile。

## 开发步骤

1. 在工程内创建一个ExtensionAbility类型的自定义组件并继承[CallerInfoQueryExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/callservicekit-callerinfoquery-extension-ability)，完成onQueryCallerInfo方法的复写。
    
    说明：
    
    由于调用onQueryCallerInfo方法时，系统先创建应用的AbilityStage实例，请勿在AbilityStage中添加过于复杂耗时的逻辑，避免调用超时。
    
    代码示例：
    
    1. import { CallerInfoQueryExtensionAbility, CallerInfo } from '@kit.CallServiceKit';
    
    2. export default class EntryCallerInfoQueryExtAbility extends CallerInfoQueryExtensionAbility {
    3.  // 来去电时由系统通话应用主动调用该接口查询企业联系人信息
    4.   onQueryCallerInfo(phoneNumber: string): Promise<CallerInfo> {
    5.     return new Promise<CallerInfo>((resolve, reject) => {
    6.       let isSuccess = true;
    7.       // 在此处实现根据号码查询企业联系人的业务逻辑
    8.       if (isSuccess) {
    9.         // 查询成功，返回结果
    10.         resolve({
    11.           contactName:"xxxx",
    12.           employeeId:"xxxx",
    13.           department:"xxxx",
    14.           position:"xxxx"
    15.         });
    16.       } else {
    17.         // 查询失败，返回错误原因
    18.         reject("error reason");
    19.       }
    20.     });
    21.   }
    22. }
    
2. 在应用配置文件module.json5中注册extensionAbilities，具体详见[module.json5配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)。
    
    配置文件示例：
    
    1. {
    2.     "extensionAbilities": [
    3.       {
    4.         "name": "EntryCallerInfoQueryExtAbility",
    5.         "srcEntry": "./ets/callerinfoquery/EntryCallerInfoQueryExtAbility.ets",
    6.         "type": "callerInfoQuery"
    7.       }
    8.     ]
    9. }
    
    - type标签需设为"callerInfoQuery"，表示该拓展类型为CallerInfoQueryExtensionAbility。
    - srcEntry标签表示上述ExtensionAbility组件所对应的代码路径。
3. 在调试设备上，前往“电话”，点击右上角的“更多”图标，前往“设置”>“陌生号码和信息识别”，打开对应企业应用的号码识别功能开关，进行调试。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/outgoing-calls "去电场景")
# 来电横幅无法拉起

更新时间: 2025-12-16 16:36

**问题现象**

调用[voipCall.reportIncomingCall](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-voipcall#section13177019143216)上报来电信息，但来电横幅无法显示。

**解决措施**

1. 检查应用是否已开启[通知权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-enable)。
2. 检查是否继承UIAbility，调用[pushService.receiveMessage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/push-pushservice#section125883044911)并在接收后调用上报接口。
3. 来电信息中获取的callId，上报给通话服务接口的callId，二者应该保持一致。
4. 检查构造的callInfo信息是否有参数错误，如voipCallState需要是VOIP_CALL_STATE_RINGING。
5. 如还未解决，请通过[在线提单](https://developer.huawei.com/consumer/cn/support/feedback/#/)提交问题，华为支持人员会及时处理。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/call-faq "Call Service Kit常见问题")
# 来电横幅通知头像无法显示

更新时间: 2025-12-16 16:36

**问题现象**

来电过程中，横幅通知展示，但头像无法正常显示。

**解决措施**

1. 保证头像图片大小在196608以内。
2. 支持传入的最大图片大小为 221 x 221 像素，推荐传入的图片大小为 112 x 112 像素。
3. 如还未解决，请通过[在线提单](https://developer.huawei.com/consumer/cn/support/feedback/#/)提交问题，华为支持人员会及时处理。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/call-faq-1 "来电横幅无法拉起")
