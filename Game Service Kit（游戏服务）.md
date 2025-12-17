# Game Service Kit简介

更新时间: 2025-12-16 16:35

## 业务简介

Game Service Kit（游戏服务）主要提供快速、低成本构建游戏基本能力与游戏场景优化服务，有效提升游戏开发效率，帮助游戏运营。

|功能|描述|
|:--|:--|
|[基础游戏服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-dev)（必选）|为游戏快速、低成本地构建基础功能，例如联合登录、华为账号实名认证、未成年人防沉迷等，让开发者聚焦游戏本身的业务能力，从而迅速推广游戏，并基于用户和内容的本地化进行深度的游戏运营。|
|[游戏场景感知](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameperformance-dev)（可选）|通过游戏为系统提供精细化场景信息、配置信息、网络信息等数据，系统向游戏反馈系统状态等信息，使得双方能够利用这些信息进行更紧密和深入的协作，在系统资源有限的情况下优化玩家的游戏体验。|
|[游戏近场快传](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-nearbytransfer-dev)（可选）|游戏近场快传服务支持设备在彼此靠近的情况下进行游戏数据交换。|

## 约束和限制

### 支持的国家和地区

本Kit仅支持华为账号的注册地和服务地均为中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）的用户。

### 支持的设备

|功能|支持的设备|
|:--|:--|
|基础游戏服务|Phone、Tablet、2in1、TV。|
|游戏场景感知|Phone、Tablet、2in1。|
|游戏近场快传|Phone、Tablet、2in1。|

## 模拟器支持情况

本Kit暂不支持模拟器。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/game-service-kit-guide "Game Service Kit（游戏服务）")
# 概述

更新时间: 2025-12-16 16:37

基础游戏服务能为游戏快速、低成本地构建基础功能，例如联合登录、华为账号实名认证、未成年人防沉迷等，让开发者聚焦游戏本身的业务能力，从而迅速推广游戏，并基于用户和内容的本地化进行深度的游戏运营。

## 约束与限制

基础游戏服务支持Phone、Tablet、2in1设备，并且从5.1.1(19)版本开始，新增支持TV设备。

## 场景介绍

### 网络游戏登录

网络游戏是指需要联网的游戏。

接入基础游戏服务后，网络游戏支持用户在联合登录面板选择华为账号登录或游戏官方账号登录。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163749.18763294299795173847095693823756:50001231000000:2800:DB99A5FEF474ADE10A311EE3BC853F4B3A5EE4678B0C9641B60E2D208EB8A8CA.jpg "点击放大")

### 单机游戏登录

单机游戏是指数据本地化存储，不依赖服务器的游戏。

接入基础游戏服务后，单机游戏支持使用华为账号快速进入游戏，且单机游戏的华为账号实名认证、未成年人防沉迷功能由基础游戏服务实现。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-gamelogin "游戏登录")
# 网络游戏登录概述

更新时间: 2025-12-16 16:38

网络游戏是指需要联网的游戏。

接入基础游戏服务后，网络游戏支持用户在联合登录面板选择华为账号登录或游戏官方账号登录。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163810.17786640980713999984679428989369:50001231000000:2800:FBFC2043BBB5AE446936E061C5A82EC6FCA377CE46542AB37938671ED37B3AF0.jpg "点击放大")

## 网络游戏登录场景介绍

### 使用华为账号登录

网络游戏必须接入华为账号登录。

接入后，华为平台会将HarmonyOS 4及以下游戏的玩家标识playerId/openId赋值给HarmonyOS 5.0及以上游戏的玩家标识gamePlayerId，为新老系统游戏的账号资产（角色、区服信息、游戏进度等）实现互通。互通前后，华为账号ID不会发生变化，也不涉及开发者服务器和数据库层面的变动。

使用华为账号登录的网络游戏，华为账号的实名认证、未成年人防沉迷由基础游戏服务实现，华为账号的支付合规控制（例如未成年人支付限额）由IAP Kit（应用内支付服务）实现。

### 使用游戏官方账号登录

若游戏有官包且有官方账号体系，网络游戏还需要接入游戏官方账号登录，且游戏开发者需要正确实现HarmonyOS 5.0及以上系统游戏包与游戏官包之间账号资产的互通。

使用游戏官方账号登录的网络游戏，游戏官方账号的实名认证、未成年人防沉迷、支付合规控制需要游戏开发者自行实现。

说明

用户使用游戏官方账号登录游戏时，设备上基础游戏服务也会基于设备上登录的华为账号实现实名认证、未成年人防沉迷，这属于HarmonyOS 5.0及以上设备的额外要求。游戏官方账号登录游戏时，开发者仍需要基于游戏官方账号实现实名认证、未成年人防沉迷、支付合规控制。

### 账号关系总览

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163810.86549167557537607986927325202845:50001231000000:2800:9BC7045D2F988755A9C8350ED8FF67D00F5218D2F5537D3782258CE19CF30603.png)

## 网络游戏用户体验

玩家侧的游戏登录体验。

### 首次登录

首次启动游戏时，向用户展示联合登录面板。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163810.28347862561822735603244343929240:50001231000000:2800:F1C8BABD5F85289753F8CF44B004C6AD48603D5F0260B84E4A76D9A676D80B51.jpg "点击放大")

- 点击“华为账号登录”，用户使用华为账号进入游戏，顶部展示欢迎横幅。
- 点击“游戏官方账号登录”，弹出游戏官方的登录界面，用户正确输入官方账号后进入游戏。

### 非首次登录

用户非首次启动游戏时，游戏会沿用之前的登录账号。涉及切换账号再登录等特殊场景的接入方式请参见[游戏内切换账号](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-official#section26517112362)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-network "网络游戏登录")
# 使用华为账号登录（必选）

更新时间: 2025-12-16 16:38

接入后，华为平台会将HarmonyOS 4及以下游戏的玩家标识playerId/openId赋值给HarmonyOS 5.0及以上游戏的玩家标识gamePlayerId，为新老系统游戏的账号资产（角色、区服信息、游戏进度等）实现互通。互通前后，华为账号ID不会发生变化，也不涉及开发者服务器和数据库层面的变动。

使用华为账号登录的网络游戏，华为账号的实名认证、未成年人防沉迷由基础游戏服务实现，华为账号的支付合规控制（例如未成年人支付限额）由IAP Kit（应用内支付服务）实现。

## 接入策略

游戏必须接入华为账号登录。

## 开发准备

### 创建游戏

在华为应用市场发布游戏，要求前往AppGallery Connect创建游戏类应用，具体操作请参见[创建HarmonyOS应用](https://developer.huawei.com/consumer/cn/doc/app/agc-help-create-app-0000002247955506)。其中：

- “应用类型”：选择“HarmonyOS应用”。
- “应用分类”：选择“游戏”。

说明

用于正式上架的游戏包名建议不要包含test、dev等信息。

### 申请版署实名认证

按照版署《关于开展网络游戏防沉迷实名认证系统接口对接工作的通知》，各游戏出版运营企业均要求在2021年6月1日前完成接入[网络游戏防沉迷实名认证系统](https://wlc.nppa.gov.cn/fcm_company/index.html#/login?redirect=/)，并获取“bizID（游戏备案识别码）”，再将bizID配置到AppGallery Connect，华为将为游戏自动对接国家新闻出版署的实名认证系统并开启强制实名认证，开发者无需进行额外的开发。具体操作请参见[版署实名认证申请](https://developer.huawei.com/consumer/cn/doc/games-guides/game-center-identification-applyfor-0000002392353221)。

### 申请备案

请参考[APP备案FAQ](https://developer.huawei.com/consumer/cn/doc/App/50130)完成游戏备案。

说明

HarmonyOS 4及以下游戏与HarmonyOS 5.0及以上游戏要求分别申请备案。

### 生成签名证书

数字证书和Profile文件等签名信息可以确保游戏的完整性：

- 调试阶段：[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)、[申请调试证书](https://developer.huawei.com/consumer/cn/doc/app/agc-help-debug-cert-0000002283256797)、[申请调试Profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-debug-profile-0000002248181278)。
- 发布阶段：[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)、[申请发布证书](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-cert-0000002283336729)、[申请发布Profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-profile-0000002248341090)。

### 配置签名证书指纹

AppGallery Connect会自动生成证书对应的公钥信息，并计算出对应的SHA256指纹。开发者前往AppGallery Connect获取并配置SHA256指纹，且每个游戏至多添加4个签名证书指纹，配置签名证书指纹的具体操作请参见[配置公钥指纹](https://developer.huawei.com/consumer/cn/doc/app/agc-help-cert-fingerprint-0000002278002933)。

说明

请在调试阶段添加调试证书对应的指纹，在发布阶段添加发布证书对应的指纹。

### 配置APP ID和Client ID

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，在“开发与服务”下选择项目及项目下的游戏，获取“应用”下的APP ID和Client ID。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.50038260936851987159151380117028:50001231000000:2800:1D9B01B31C54C725D305C44BCF9DE49C9F6A4069F795BBE170CA6EFB45FE9FD7.png)
    
2. 在工程的entry模块module.json5文件中，新增metadata并配置client_id和app_id，同时新增requestPermissions以配置网络权限。如下所示：
    
    1. "module": {
    2.   "name": "entry",
    3.   "type": "xxx",
    4.   "description": "xxxx",
    5.   "mainElement": "xxxx",
    6.   "deviceTypes": [],
    7.   "pages": "xxxx",
    8.   "abilities": [],
    9.   "metadata": [ // 配置如下信息
    10.     {
    11.       "name": "client_id",
    12.       "value": "xxxxxx" // 配置为前面步骤中获取的Client ID
    13.     },
    14.     {
    15.       "name": "app_id",
    16.       "value": "xxxxxx" // 配置为前面步骤中获取的APP ID
    17.     }
    18.   ],
    19.   "requestPermissions": [ // 配置网络权限
    20.     {
    21.       "name": "ohos.permission.INTERNET"
    22.     }
    23.   ]
    24. }
    

### 配置APP ID映射关系

由于要求实现HarmonyOS 5.0及以上系统和HarmonyOS 4及以下系统上游戏内资产互通，用户登录新系统游戏时需要找到对应的老系统游戏，以及用户在该游戏下的账号ID，所以要求开发者在上架游戏时配置游戏在新老系统下的APP ID映射关系，并配置游戏在老系统游戏上接入的账号ID类型（playerId/openId）。

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，在“开发与服务”下选择项目及项目下的游戏，左侧菜单选择“构建 > 游戏服务”，在右侧点击“新增配置”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.33865529565633466916661282552651:50001231000000:2800:8B4D5BF70D9602B7C769EB8B3DDBF846896A4BE3F8D1D42DE5353AB6D347BF37.png)
    
2. 在弹出的“新增配置信息”窗口中选择HAP游戏和APK游戏，完成后点击“下一步”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.33664116493649221296319584170084:50001231000000:2800:CCE5DEC081B5C223C9B141C1C0B57BD4545B3BA642E2FF15D327CF4E50200CE6.png)
    
    |信息项|说明|
    |:--|:--|
    |HarmonyOS 5.0及以上游戏|请选择待上架的HAP游戏。|
    |HarmonyOS 4及以下游戏|请选择已上架或待上架的APK游戏。<br><br>若无待上架的游戏，请新建草稿态游戏。|
    
3. 在弹出的窗口中继续填写信息，完成后点击“下一步”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.62721687593543311145850946446838:50001231000000:2800:83590A5306DED5D793FE624BA30145F5BD2CBB59605A09D0FB1A27687C41AB1D.png)
    
    |信息项|说明|
    |:--|:--|
    |支持数据继承的玩家标识类型|请选择HarmonyOS 4及以下游戏的玩家标识类型：<br><br>- **playerId**：老系统游戏确认使用**playerId**作为玩家标识，请选择“**playerId**”。选择后，新系统游戏的玩家标识gamePlayerId=playerId。<br>- **openId**：如下情况请选择“**openId**”<br>    - 情况一：老系统游戏确认使用**openId**作为玩家标识。<br>    - 情况二：老系统游戏确认使用**unionId**作为玩家标识。此时，请同时勾选“使用了unionId”，并通过[转换ID](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-convertid)用gamePlayerId（openId）换取unionId，若unionId未在游戏侧找到玩家记录，则当前玩家为新系统游戏的新用户。<br>    - 情况三：部分游戏由于处于playerId替换为openId方案的过渡期，导致老系统游戏的玩家标识存在**playerId与openId混用**的情况，例如A玩家使用openId，B玩家使用playerId。此时，若无法通过gamePlayerId在游戏侧找到玩家记录，可通过[转换ID](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-convertid)接口用gamePlayerId（openId）换取playerId，若playerId能在游戏侧找到玩家记录，表明该玩家是使用playerId作为玩家标识的老用户，否则该玩家为新系统游戏的新用户。<br>    - 情况四：HarmonyOS 4及以下游戏未上架时。|
    |接入unionId的HarmonyOS 4及以下游戏实现数据继承需要进行转换处理|若老系统的游戏确认使用**unionId**作为玩家标识，请勾选“使用了unionId”。|
    
4. （可选）填写开发者服务器的回调地址，回调地址要求支持HTTPS协议，且具有合法商用证书，完成后点击“确定”提交APP ID映射关系的审批申请。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.72548708372186131343235297801892:50001231000000:2800:4980A87305832222ED27ACF4A5C6AFF688DCBFEF7E881F035019D0D74562001D.png)
    
5. 若出现异常情况，将在提示框以红字提醒。
    
    建议点击“取消”重新配置映射关系。若忽略异常情况点击“确定”继续提交申请，可能会造成映射关系审批不通过。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.61033344322036192344420782740409:50001231000000:2800:98982F16A0A89EB98E7B689EF3FE929AFFA603230FCC6B71AA0B7113E02FC7EA.png)
    
6. 提交申请后，华为工作人员完成审核需要1~3个工作日，请耐心等待。APP ID映射关系生效后想要重新配置，请先提交映射关系的删除申请。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.87157529638784447038772655824256:50001231000000:2800:F9F53657C65024F595A70FCDB7C837D98A8D61820157A80E31ED2953E2B1006F.png)
    
    配置/删除APP ID映射关系的审核结果将通过互动中心或邮件进行通知。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.87066756617819087033121697290188:50001231000000:2800:5EF8F683DCA9A85069092F25010BD8C44BAACE0BF212DDB53DFCC04142BB83F0.png)
    

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.62473059425114791711805788300501:50001231000000:2800:6A7F9EB3AFC796EAE28E58918098C0B7818C60DBBF08D812DFA485AFE300C695.png)

1. 玩家启动游戏。
2. 游戏调用[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)接口初始化Game Service Kit。初始化后，弹出华为隐私协议，玩家签署协议后，则继续往下执行。
3. 游戏调用[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section1097616266227)接口注册事件监听。若监听到[PlayerChangedEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section57008633419)事件，先清除本地缓存信息，再重新调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)登录逻辑，showLoginDialog设置为true，重新拉起联合登录面板。
4. 游戏调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口。
    
    说明
    
    建议使用session缓存登录状态，玩家下次登录进入游戏无需再调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口，但仍需调用[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)接口。
    
5. 向玩家展示联合登录面板。
6. 玩家选择“华为账号登录”。
7. 游戏顶部弹出欢迎横幅，并向游戏返回accountName（选择华为账号登录返回值为hw_account）、gamePlayerId等信息。
8. 【**异步流程**】玩家信息核验。建议在服务端校验玩家信息，若没有服务器，无需校验一致性。
    1. 游戏调用[createLoginWithHuaweiIDRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/account-api-authentication#section7843123616411)接口，获取用于服务器校验的Authorization Code。
        
        说明
        
        Authorization Code只有5分钟有效期，且仅能使用一次，不可复用。
        
    2. 游戏向开发者服务器上传Authorization Code、gamePlayerId等信息。
    3. 开发者服务器携带Authorization Code，请求[获取用户级凭证](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/account-api-obtain-user-token)接口，获取Access Token。
    4. 开发者服务器携带Access Token，请求[获取玩家标识](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-getplayerinfo)接口，获取gamePlayerId。
    5. 开发者服务器把从华为游戏服务器获取的gamePlayerId与客户端获取的gamePlayerId进行一致性核验。若核验不通过，已通过合规校验进入游戏的玩家也需强制退出游戏。
9. 游戏调用[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)接口，校验当前用户设备登录华为账号的实名认证、未成年人防沉迷信息。校验通过后，玩家进入游戏。若校验未通过请根据返回的[错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code)进行相应处理。
10. 若玩家在游戏内创建角色，建议游戏调用[savePlayerRole](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section201561659105917)上报角色信息。
    
    说明
    
    若游戏无区服角色，或限制为1个区服角色，此时，建议游戏允许玩家直接进入游戏，而无需玩家点击“进入游戏”或者选择区服角色才能进入游戏。
    

## 接口说明

具体API说明请详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer)。

|接口名|描述|
|:--|:--|
|[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)(context: common.UIAbilityContext, callback: AsyncCallback<void>): void|游戏初始化接口，使用默认的上下文信息，使用callback回调。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section1097616266227)(type: 'playerChanged', callback: Callback<PlayerChangedResult>): void|玩家变化事件监听接口，通过Callback回调获取玩家变化结果信息。|
|[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)(context: common.UIAbilityContext, loginParam: UnionLoginParam): Promise<UnionLoginResult>|华为账号和游戏官方账号联合登录接口，通过Promise对象获取返回值。|
|[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)(context: common.UIAbilityContext, thirdUserInfo: ThirdUserInfo): Promise<void>|合规校验接口，校验当前设备登录的华为账号的实名认证、游戏防沉迷信息，通过Promise对象获取返回值。|
|[savePlayerRole](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section201561659105917)(context: common.UIAbilityContext, request: GSKPlayerRole): Promise<void>|保存角色信息到华为游戏服务器，使用默认的上下文信息，通过Promise对象获取返回值。|

## 开发步骤

### 接口调用流程图

接入华为账号登录的接口调用流程如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.41260402486643528358736778482403:50001231000000:2800:20BAA263057C0355CDEA70C2BAA4F99A803363D08E40672C2A746E95ACF0EC3E.png)

### 导入模块

导入Account Kit模块、Game Service Kit模块及相关公共模块。

1. import { authentication } from '@kit.AccountKit';
2. import { gamePlayer } from '@kit.GameServiceKit';
3. import { common } from '@kit.AbilityKit';
4. import { hilog } from '@kit.PerformanceAnalysisKit';
5. import { Callback, BusinessError } from '@kit.BasicServicesKit';
6. import { window } from '@kit.ArkUI';
7. import { util } from '@kit.ArkTS';

### 初始化

调用[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)接口初始化Game Service Kit。

说明

- 调用接口时严格要求继承UIAbility，并且获取上下文的时机是onWindowStageCreate生命周期中页面加载成功后。
- 要求游戏先成功调用初始化[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)接口后再调用其他接口，否则将导致审核被驳回。

1. onWindowStageCreate(windowStage: window.WindowStage) {
2.   windowStage.loadContent("pages/index", (err, data) => {
3.     try {
4.       gamePlayer.init(this.context,()=>{
5.         hilog.info(0x0000, 'testTag', `Succeeded in initing.`);
6.       });
7.     } catch (error) {
8.       let err = error as BusinessError;
9.       hilog.error(0x0000, 'testTag', `Failed to init. Code: ${err.code}, message: ${err.message}`);
10.     }
11.   });
12. }

初始化后，游戏弹出华为隐私协议窗口，用户同意签署协议，则继续往下执行。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.15709983638520893351349742451478:50001231000000:2800:0A0AC5194800BF3AB80D1E92CA0A431CD79A7E354015A05BFFF662426B865563.png "点击放大")

若当前华为账号同意过游戏服务隐私协议，后续使用该华为账号登录的游戏将不会再弹出隐私协议窗口。

### 注册事件监听

调用[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section1097616266227)接口注册[PlayerChangedEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section57008633419)事件监听，及时感知游戏过程中账号的变化。

1. private onPlayerChangedEventCallback(result: gamePlayer.PlayerChangedResult) {
2.   if (result.event === gamePlayer.PlayerChangedEvent.SWITCH_GAME_ACCOUNT) {
3.      // ...
4.     // 游戏号已切换，完成本地缓存清理工作后，再次调用unionLogin接口等
5.   }
6. }
7. // ...
8. // 调用on接口注册playerChanged事件监听
9. try {
10.   gamePlayer.on('playerChanged', this.onPlayerChangedEventCallback);
11.   hilog.info(0x0000, 'testTag', `Succeeded in registering.`);
12. } catch (error) {
13.   let err = error as BusinessError;
14.   hilog.error(0x0000, 'testTag', `Failed to register. Code: ${err.code}, message: ${err.message}`);
15. }

目前有如下两个场景可以监听到账号变化：

|能监听到账号切换的场景|监听到账号切换后的措施|
|:--|:--|
|场景一：<br><br>玩家点击“欢迎横幅->管理->切换”或者点击“欢迎横幅->管理->X”。<br><br>详情请参见[欢迎横幅管理游戏账号](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-huawei#section03151161013)。|若监听到账号变化，游戏应先清除本地缓存信息（session或其他用户缓存），再重新调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口（showLoginDialog设置为true），重新拉起联合登录面板。|
|场景二：<br><br>用户在设备上切换华为账号后，游戏重启但没有调用unionLogin，直接调用verifyLocalPlayer。此时，verifyLocalPlayer接口会返回[1002000015](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code#section1955824812307)错误码，同时触发on回调。|

### 展示联合登录面板

调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口，向玩家展示联合登录面板。

1. let context = this.getUIContext()?.getHostContext() as common.UIAbilityContext;
2. let thirdAccountInfo1: gamePlayer.ThirdAccountInfo = {
3.   'accountName': 'testName1', // 游戏开放给开发者接入的账号类型名字，例如“官方账号”、“xx账号”等，并不是具体某个玩家ID或开发者ID。
4.   'accountIcon': $r('app.media.icon') // 游戏官方账号图标资源信息，图标大小总和不能超过35KB。
5. };
6. let request: gamePlayer.UnionLoginParam = {
7.   showLoginDialog: false, // 是否弹出联合登录面板。true表示强制弹出面板，false表示优先使用玩家上一次的登录选择，不弹出联合登录面板，若玩家首次登录或卸载重装，则正常弹出。
8.   thirdAccountInfos: [ 
9.     thirdAccountInfo1 // 若游戏无官包或无官方账号体系，请传空数组。
10.   ]
11. };
12. try {
13.   gamePlayer.unionLogin(context, request).then((result: gamePlayer.UnionLoginResult) => {
14.     hilog.info(0x0000, 'testTag', `Succeeded in logining: ${result?.accountName}`);
15.   }).catch((error: BusinessError) => {
16.     hilog.error(0x0000, 'testTag', `Failed to login. Code: ${error.code}, message: ${error.message}`);
17.   });
18. } catch (error) {
19.   let err = error as BusinessError;
20.   hilog.error(0x0000, 'testTag', `Failed to login. Code: ${err.code}, message: ${err.message}`);
21. }

联合登录面板为官方统一样式，不支持开发者自定义联合登录面板样式。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163812.61200884786018325659083651801329:50001231000000:2800:D88F33D3C6E8D7C47EA56EC7892D896E0640DA0876521D876F2124852B6E143E.jpg "点击放大")

用户完成登录流程后，游戏顶部弹出欢迎横幅，并向游戏返回accountName（选择华为账号登录返回值为hw_account）、gamePlayerId等信息。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163813.85100975266067603089402687849889:50001231000000:2800:D7D20305C5528818ABDD03DD7FADD5486FE596A4102BD81DF24557E9096751D2.png "点击放大")

游戏获取到的gamePlayerId（HarmonyOS 5.0及以上系统）与openId/playerId（HarmonyOS 4及以下系统）数值相等。开发者可以根据gamePlayerId实现HarmonyOS 5.0及以上游戏和HarmonyOS 4及以下游戏的账号资产互通。

若在开发者服务器找到玩家记录，表明该玩家是老用户。若未找到玩家记录，表明该玩家为新用户，开发者可以为该玩家在HarmonyOS 5.0及以上系统创建新的游戏号。

### 异步步骤：核验玩家信息

由于[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口返回的gamePlayerId存在被篡改的风险，建议在开发者服务端核验玩家信息，即从开发者服务器获取gamePlayerId与[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口返回的gamePlayerId做比对，确保玩家信息一致性。若无服务器，无需校验一致性。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163813.66039508598456208902491438742826:50001231000000:2800:D70CDB4B8E8B05FA8C2B6961B498BF5EBFFDD51B7FFD551AF8EDF05E761339ED.png "点击放大")

1. 调用[createLoginWithHuaweiIDRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/account-api-authentication#section7843123616411)创建认证请求并设置参数。
    
    1. // 创建认证请求，并设置参数
    2. let loginRequest = new authentication.HuaweiIDProvider().createLoginWithHuaweiIDRequest();
    3. loginRequest.state = util.generateRandomUUID();
    
    调用[AuthenticationController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/account-api-authentication#section620452019185)对象的[executeRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/account-api-authentication#section164113311433)方法执行认证请求，并在Callback中处理认证结果，获取到Authorization Code。
    
    说明
    
    Authorization Code有效时间为5分钟，且仅能使用一次，不可复用。
    
    4. // 执行认证请求
    5. try {
    6.   let controller = new authentication.AuthenticationController(this.getUIContext()?.getHostContext());
    7.   controller.executeRequest(loginRequest, (err, data) => {
    8.     if (err) {
    9.       hilog.error(0x0000, 'testTag', `Failed to login. Code: ${err.code}, message: ${err.message}`);
    10.       return;
    11.     }
    12.     let loginWithHuaweiIDResponse = data as authentication.LoginWithHuaweiIDResponse;
    13.     let state = loginWithHuaweiIDResponse.state;
    14.     if (state != undefined && loginRequest.state != state) {
    15.       hilog.error(0x0000, 'testTag', `Failed to login. State is different.`);
    16.       return;
    17.     }
    18.     hilog.info(0x0000, 'testTag', `Succeeded in logining.`);
    19.     let loginWithHuaweiIDCredential = loginWithHuaweiIDResponse.data!;
    20.     let authorizationCode = loginWithHuaweiIDCredential.authorizationCode;
    21.     // 开发者处理authorizationCode
    22.   });
    23. } catch (error) {
    24.   let err = error as BusinessError;
    25.   hilog.error(0x0000, 'testTag', `Failed to login. Code: ${err.code}, message: ${err.message}`);
    26. }
    
2. 游戏向开发者服务器上传[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口返回的gamePlayerId。
3. 携带Authorization Code，请求[获取用户级凭证](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/account-api-obtain-user-token)接口，获取Access Token。
    
    说明
    
    由于Access Token的有效期仅为60分钟，当Access Token失效或者即将失效时（可通过[NSP_STATUS错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/account-api-get-token-info#section1737691991515)判断），可以使用Refresh Token（有效期180天）通过[获取用户级凭证](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/account-api-obtain-user-token)向华为账号服务器请求获取新的Access Token。
    
4. 携带Access Token，请求[获取玩家标识](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-getplayerinfo)接口，获取华为服务器侧的玩家标识gamePlayerId。
5. 将华为服务器返回的玩家标识gamePlayerId与步骤**2**传入的玩家标识gamePlayerId进行玩家信息核验。
    
    若gamePlayerId一致，表示玩家标识gamePlayerId核验通过，允许玩家进入游戏。若核验不通过，已通过合规校验进入游戏的玩家也需强制退出游戏。
    

### 合规校验

调用[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)接口对用户设备登录华为账号的实名认证和未成年人防沉迷进行合规校验，校验通过后，玩家进入游戏。

1. let context = this.getUIContext()?.getHostContext() as common.UIAbilityContext;
2. // ThirdUserInfo是使用游戏官方账号登录游戏的玩家合规信息，接入华为账号登录时无需传入该信息，但在接入游戏官方账号登录时要求传入相关信息。
3. let request: gamePlayer.ThirdUserInfo = {
4.   thirdOpenId: '123xxxx', // 游戏官方账号ID，接入华为账号登录时传空。
5.   isRealName: true // 玩家是否实名,该值为true时表示已实名,为false时表示未实名，接入华为账号登录时不传该字段。
6. };
7. try {
8.   gamePlayer.verifyLocalPlayer(context, request).then(() => {
9.     hilog.info(0x0000, 'testTag', `Succeeded in verifying.`);
10.   }).catch((error: BusinessError) => {
11.     hilog.error(0x0000, 'testTag', `Failed to verify. Code: ${error.code}, message: ${error.message}`);
12.   });
13. } catch (error) {
14.   let err = error as BusinessError;
15.   hilog.error(0x0000, 'testTag', `Failed to verify. Code: ${err.code}, message: ${err.message}`);
16. }

使用华为账号登录的网络游戏，华为账号的实名认证、未成年人防沉迷由基础游戏服务实现，华为账号的支付合规控制（例如未成年人支付限额）由IAP Kit（应用内支付服务）实现。

|合规校验|校验项|国家政策|解决方案|
|:--|:--|:--|:--|
|华为账号实名认证|校验用户设备登录的华为账号是否已实名认证。|根据相关法律法规要求，所有网络游戏玩家必须使用真实有效身份信息注册并登录网络游戏。|若玩家使用未实名认证的华为账号登录游戏时，基础游戏服务向玩家弹出实名认证窗口，要求玩家进行实名认证。若玩家取消实名认证，则返回[1002000004](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code#section206921217496)错误码。|
|未成年人防沉迷|校验已实名认证为未成年人的华为账号是否在规定时间内登录游戏。|根据国家新闻出版署的最新规定，所有网络游戏企业仅可在周五、周六、周日和法定节假日每日20时至21时向未成年人提供1小时网络游戏服务，其他时间均不得以任何形式向未成年人提供网络游戏服务。|- 已实名认证为未成年人的华为账号在规定时间内登录游戏，当游戏进行到晚上21时，基础游戏服务会弹窗提示玩家已到游戏时间，强制玩家退出游戏并返回[1002000006](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code#section4418848101513)错误码。<br>- 已实名认证为未成年人的华为账号在非规定游戏时间内登录游戏，基础游戏服务会弹框提示玩家不允许游戏，强制玩家退出游戏并返回[1002000006](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code#section4418848101513)错误码。|
|未成年人支付限额|校验已实名认证为未成年人的华为账号是否限额付费。|根据国家新闻出版署的最新规定，网络游戏企业不得为未满8周岁的用户提供游戏付费服务。同一网络游戏企业所提供的游戏付费服务，8周岁以上未满16周岁的用户，单次充值金额不得超过50元人民币，每月充值金额累计不得超过200元人民币；16周岁以上未满18周岁的用户，单次充值金额不得超过100元人民币，每月充值金额累计不得超过400元人民币。|已实名认证为未成年人的华为账号在游戏内超额付费，IAP Kit会弹窗提示消费金额超出限制。<br><br>用户在使用华为应用内支付时，华为会自动根据国家新闻出版署的要求进行支付限额控制，您无需处理。|

|   |   |   |
|---|---|---|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163813.67651115104210443769051750729356:50001231000000:2800:BCA2E0A2225F199F9403C20FCBB4192565B926C3E22B0FBFD27EAE3BF5FA19BC.png "点击放大")<br><br>华为账号实名认证|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163813.06467265794723102405225206403761:50001231000000:2800:4D0D637ED6DBB74B6E36751BDF896E52B4B185D69252DDD5BEB53D6C385C6C74.png "点击放大")<br><br>未成年人防沉迷|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163813.85262079665314641893085561455852:50001231000000:2800:EB6F00330452DAEE957C55FAEB14632F61E86DAA1F9D43765FE550D138BC43C6.png "点击放大")<br><br>未成年人支付限额|

### 提交玩家角色信息

推荐接入。

玩家成功登录游戏并选择角色、区服后，游戏将角色信息提交到华为游戏服务器，可用于后续基于角色维度的联运活动规划，为玩家提供更好的体验和更丰富的能力。

调用[savePlayerRole](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section201561659105917)接口，将角色信息上报至华为游戏服务器。

注意

若游戏没有角色系统，“roleId”请传入“0”，“roleName”请传入“default”，请勿传""和null。

1. let context = this.getUIContext()?.getHostContext() as common.UIAbilityContext;
2. let request: gamePlayer.GSKPlayerRole = {
3.   roleId: '123', // 玩家角色ID，如游戏没有角色系统，请传入“0”，务必不要传""和null。
4.   roleName: 'Jason', // 玩家角色名，如游戏没有角色系统，请传入“default”，务必不要传""和null。
5.   serverId: '456',
6.   serverName: 'Zhangshan',
7.   gamePlayerId: '789', // 请根据实际获取到的gamePlayerId传值。
8.   thirdOpenId: '123' // 接入华为账号登录时不传该字段。接入游戏官方账号登录时，请根据实际获取到的thirdOpenId传值。
9. };
10. try {
11.   gamePlayer.savePlayerRole(context, request).then(() => {
12.     hilog.info(0x0000, 'testTag', `Succeeded in saving.`);
13.   });
14. } catch (error) {
15.   let err = error as BusinessError;
16.   hilog.error(0x0000, 'testTag', `Failed to save. Code: ${err.code}, message: ${err.message}`);
17. }

### 欢迎横幅管理游戏账号

不涉及角色交易、或不存在多个游戏号的游戏可忽略。

接入角色交易、或存在多个游戏号的游戏，玩家成功登录后会在顶部欢迎横幅出现“管理”按钮。

若玩家在“顶部欢迎横幅 > 管理 > 管理游戏号”中切换/删除游戏号时，开发者的实现逻辑如下：

1. 在[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section1097616266227)接口回调中清理游戏的登录缓存。
2. 在[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section1097616266227)接口回调中重新调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口，将**showLoginDialog**参数设置为**true**，即可强制拉起联合登录面板，允许玩家重新选择华为账号登录或游戏官方账号登录。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163813.49116853587237062073015097699848:50001231000000:2800:E72C81D0EDDAFDEE95A8FA37AA85FBDCBBDBB85EBAD5662A0FFA136BCD51A1FB.png "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-network-introduction "网络游戏登录概述")
# 使用游戏官方账号登录

更新时间: 2025-12-16 16:38

|   |   |
|---|---|
|为了支持用户在HarmonyOS 5.0及以上系统上继承其他系统（例如HarmonyOS 4及以下）的官包进度继续游玩，基础游戏服务支持用户使用游戏官方账号登录HarmonyOS 5.0及以上游戏。||

## 接入策略

若游戏有官包且有官方账号体系，游戏要求接入游戏官方账号登录。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163813.67946042596730935735482122557280:50001231000000:2800:293C97B2CF7C1EEDC8C5C5024A45C7934D09B01307A7C8E07F2D2DE11801FDC8.png)

1. 玩家启动游戏。
2. 游戏调用[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)接口初始化Game Service Kit。初始化后，弹出华为隐私协议，玩家签署协议后，则继续往下执行。
3. 游戏调用[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section1097616266227)接口注册事件监听。若监听到playerChanged事件，先清除本地缓存信息，再重新执行unionLogin登录逻辑。
4. 游戏调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口。
    
    说明
    
    建议使用session缓存登录状态，玩家下次登录进入游戏无需再调用unionLogin接口，但仍需调用[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)接口。
    
5. 向玩家展示联合登录面板。
6. 玩家选择“游戏官方账号登录”。
7. 游戏获取到accountName等信息。
8. 游戏开发者要求自行实现官方账号的实名认证、未成年人防沉迷、支付合规控制。
9. 游戏调用[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)接口，实现华为账号的实名认证、未成年人防沉迷功能。游戏官方账号和华为账号均通过合规校验，玩家才能进入游戏。若有一方未通过校验，不允许玩家进入游戏。若校验未通过请根据返回的[错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code)进行相应处理。
10. 若玩家在游戏内创建角色，建议游戏调用[savePlayerRole](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section201561659105917)上报角色信息。
    
    说明
    
    若游戏无区服角色，或限制为1个区服角色，此时，建议游戏允许玩家直接进入游戏，而无需玩家点击“进入游戏”或者选择区服角色才能进入游戏。
    

## 接口说明

具体API说明请详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer)。

|接口名|描述|
|:--|:--|
|[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)(context: common.UIAbilityContext, callback: AsyncCallback<void>): void|游戏初始化接口，使用默认的上下文信息，使用callback回调。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section1097616266227)(type: 'playerChanged', callback: Callback<PlayerChangedResult>): void|玩家变化事件监听接口，通过Callback回调获取玩家变化结果信息。|
|[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)(context: common.UIAbilityContext, loginParam: UnionLoginParam): Promise<UnionLoginResult>|华为账号和游戏官方账号联合登录接口，通过Promise对象获取返回值。|
|[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)(context: common.UIAbilityContext, thirdUserInfo: ThirdUserInfo): Promise<void>|合规校验接口，校验当前设备登录的华为账号的实名认证、游戏防沉迷信息，通过Promise对象获取返回值。|
|[savePlayerRole](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section201561659105917)(context: common.UIAbilityContext, request: GSKPlayerRole): Promise<void>|保存角色信息到华为游戏服务器，使用默认的上下文信息，通过Promise对象获取返回值。|

## 开发步骤

请先参考华为账号登录的[开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-huawei#section818512085410)和[开发步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-huawei#section11559185483318)完成华为账号登录的接入，再继续接入游戏官方账号登录。

### 接口调用流程图

接入游戏官方账号登录的接口调用流程如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163814.14545934793690152759083710401537:50001231000000:2800:C3A4216012F371E475635CE96ACE76A53F4C4C1F4E87BEBAD5CA4E46B7443996.png)

### 合规校验

接入游戏官方账号登录时，要求游戏开发者自行实现游戏官方账号的实名认证、未成年人防沉迷、支付合规控制。

说明

- 用户使用游戏官方账号登录游戏时，设备上基础游戏服务也会基于设备上登录的华为账号实现实名认证、未成年人防沉迷，这属于HarmonyOS 5.0及以上设备的额外要求。游戏官方账号登录游戏时，开发者仍需要基于游戏官方账号实现实名认证、未成年人防沉迷、支付合规控制。
- 华为账号与游戏官方账号均通过合规校验，玩家才能进入游戏。若有一方未通过校验，不允许玩家进入游戏或成功完成支付。

### 游戏内切换账号

由于showLoginDialog设置为false，且玩家是非首次登录游戏时，默认沿用上次的登录账号，因此要求开发者在游戏页面上自行增加“切换账号”按钮，玩家点击按钮后强制弹出联合登录面板，允许玩家重新选择华为账号登录或游戏官方账号登录。

1. 建议在游戏内为玩家提供一个“切换账号”按钮。按钮常见的位置如下：
    
    |   |   |
    |---|---|
    |![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163814.20374083106030600252387742866856:50001231000000:2800:B8822A1518F563B494823B2BF7325F27F70925098D03428268D980CDB866EC11.png "点击放大")<br><br>选择区服界面|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163814.80396803687385250913628097887642:50001231000000:2800:17A7A9DC53F4A3950EC456FE7B0A43219F86AEE0A39709E504DC58328B5CC3E9.png "点击放大")<br><br>游戏内的设置界面|
    
2. 玩家点击切换账号按钮时，开发者重新调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口，将showLoginDialog参数设置为true，即可强制拉起联合登录面板，允许玩家重新选择华为账号登录或游戏官方账号登录。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-huawei "使用华为账号登录（必选）")
# 单机游戏登录

更新时间: 2025-12-16 16:38

单机游戏是指数据本地化存储，不依赖服务器的游戏。

单机游戏接入基础游戏服务后，支持玩家使用华为账号快速进入游戏，且单机游戏的华为账号实名认证、未成年人防沉迷功能由基础游戏服务实现。

## 开发准备

### 创建游戏

在华为应用市场发布游戏，要求前往AppGallery Connect创建游戏类应用，具体操作请参见[创建HarmonyOS应用](https://developer.huawei.com/consumer/cn/doc/app/agc-help-create-app-0000002247955506)。其中：

- “应用类型”：选择“HarmonyOS应用”。
- “应用分类”：选择“游戏”。

说明

用于正式上架的游戏包名建议不要包含test、dev等信息。

### 申请版署实名认证

按照版署《关于开展网络游戏防沉迷实名认证系统接口对接工作的通知》，各游戏出版运营企业均要求在2021年6月1日前完成接入[网络游戏防沉迷实名认证系统](https://wlc.nppa.gov.cn/fcm_company/index.html#/login?redirect=/)，并获取“bizID（游戏备案识别码）”，再将bizID配置到AppGallery Connect，华为将为游戏自动对接国家新闻出版署的实名认证系统并开启强制实名认证，开发者无需进行额外的开发。具体操作请参见[版署实名认证申请](https://developer.huawei.com/consumer/cn/doc/games-guides/game-center-identification-applyfor-0000002392353221)。

### 生成签名证书

数字证书和Profile文件等签名信息可以确保游戏的完整性：

- 调试阶段：[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)、[申请调试证书](https://developer.huawei.com/consumer/cn/doc/app/agc-help-debug-cert-0000002283256797)、[申请调试Profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-debug-profile-0000002248181278)。
- 发布阶段：[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)、[申请发布证书](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-cert-0000002283336729)、[申请发布Profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-profile-0000002248341090)。

### 配置签名证书指纹

AppGallery Connect会自动生成证书对应的公钥信息，并计算出对应的SHA256指纹。开发者前往AppGallery Connect获取并配置SHA256指纹，且每个游戏至多添加4个签名证书指纹，配置签名证书指纹的具体操作请参见[配置公钥指纹](https://developer.huawei.com/consumer/cn/doc/app/agc-help-cert-fingerprint-0000002278002933)。

说明

请在调试阶段添加调试证书对应的指纹，在发布阶段添加发布证书对应的指纹。

### 配置APP ID和Client ID

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，在“开发与服务”下选择项目及项目下的游戏，获取“应用”下的APP ID和Client ID。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163804.99079118466934724360190463350124:50001231000000:2800:71148DDC8F4669BFAF338992A3792FD5B9888C54C9F64ABB1232EC15F2D8CC80.png)
    
2. 在工程的entry模块module.json5文件中，新增metadata并配置client_id和app_id，同时新增requestPermissions以配置网络权限。如下所示：
    
    1. "module": {
    2.   "name": "entry",
    3.   "type": "xxx",
    4.   "description": "xxxx",
    5.   "mainElement": "xxxx",
    6.   "deviceTypes": [],
    7.   "pages": "xxxx",
    8.   "abilities": [],
    9.   "metadata": [ // 配置如下信息
    10.     {
    11.       "name": "client_id",
    12.       "value": "xxxxxx" // 配置为前面步骤中获取的Client ID
    13.     },
    14.     {
    15.       "name": "app_id",
    16.       "value": "xxxxxx" // 配置为前面步骤中获取的APP ID
    17.     }
    18.   ],
    19.   "requestPermissions": [ // 配置网络权限
    20.     {
    21.       "name": "ohos.permission.INTERNET"
    22.     }
    23.   ]
    24. }
    

### 配置APP ID映射关系

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，在“开发与服务”下选择项目及项目下的游戏，左侧菜单选择“构建 > 游戏服务”，在右侧点击“新增配置”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163804.48486301117984024854609420834684:50001231000000:2800:CF1D2045D2E67F95AA4F25F3D33F8194278189155D2F35256FF24039744E07B8.png)
    
2. 在弹出的“新增配置信息”窗口中选择HAP游戏和APK游戏，完成后点击“下一步”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.03611618419018530702859733515383:50001231000000:2800:B32C4289FBCE7863974553B1C60660B8A6624F2920EDFEBC9749D58B3F439FAA.png)
    
    |信息项|说明|
    |:--|:--|
    |HarmonyOS 5.0及以上游戏|请选择待上架的HAP游戏。|
    |HarmonyOS 4及以下游戏|请选择已上架或待上架的APK游戏。|
    
3. 在弹出的窗口中继续填写信息，完成后点击“下一步”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.25983928363542947809596419466605:50001231000000:2800:3F953799DA834AEF6ACB31DBA53D6BECCF5BA9A01A03FD1664000DCF304EDD1D.png)
    
4. （可选）填写开发者服务器的回调地址，回调地址要求支持HTTPS协议，且具有合法商用证书，完成后点击“确定”提交APP ID映射关系的审批申请。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.48703812463280441067609043287324:50001231000000:2800:C3B3D38F27E5B0127D9B06B0966E6153156BEA4AD89C889EDB587ADD0B689E21.png)
    
5. 若出现异常情况，将在提示框以红字提醒。
    
    建议点击“取消”重新配置映射关系。若忽略异常情况点击“确定”继续提交申请，可能会造成映射关系审批不通过。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.14923032416293882380514421564951:50001231000000:2800:88A835A0BDC84D253DE2502FE0D3F7834AEEAB6BA45A5D0F5E6CEB7E7CB2FFFB.png)
    
6. 提交申请后，华为工作人员完成审核需要1~3个工作日，请耐心等待。
    
    APP ID映射关系生效后想要重新配置，请先提交映射关系的删除申请。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.78242543419030434936176926600379:50001231000000:2800:46DBC6E25291BE1925D09F84A468918ACB91176E2D396839414102F76559E523.png)
    
    配置/删除APP ID映射关系的审核结果将通过互动中心或邮件进行通知。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.55286235142833398762925353231608:50001231000000:2800:E9E8671BDF3A3211117B67A7AF4BD51D22CB4B9C232858BD18E8D7E41835E035.png)
    

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.62981514501243540686820868615030:50001231000000:2800:37EB4D815EE83CBCFAEA5C90DF5F95A0E200778BFABB2DF95D85FB73429EE77D.png)

1. 玩家启动游戏。
2. 游戏调用[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)接口初始化Game Service Kit。初始化后，弹出华为隐私协议，玩家签署协议后，则继续往下执行。
3. 游戏调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口，要求showLoginDialog参数为false，thirdAccountInfos参数传空数组。
4. 游戏顶部弹出欢迎横幅，并向游戏返回accountName（使用华为账号登录返回值为hw_account），gamePlayerId等信息。
5. 调用[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)接口，对用户设备登录的华为账号进行如下合规校验。合规校验通过后，玩家进入游戏。
    1. 若玩家未完成实名认证，[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)接口自动弹出实名认证窗口要求玩家进行实名认证。
    2. 若玩家账号实名认证为未成年人，[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)接口将自动检测未成年人的游戏时间。若玩家不在指定时间内登录游戏，将强制玩家退出游戏并返回[1002000006](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code#section4418848101513)错误码。

## 接口说明

具体API说明请详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer)。

|接口名|描述|
|:--|:--|
|[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)(context: common.UIAbilityContext, callback: AsyncCallback<void>): void|游戏初始化接口，使用默认的上下文信息，使用callback回调。|
|[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)(context: common.UIAbilityContext, loginParam: UnionLoginParam): Promise<UnionLoginResult>|登录接口，通过Promise对象获取返回值。|
|[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)(context: common.UIAbilityContext, thirdUserInfo: ThirdUserInfo): Promise<void>|合规校验接口，校验当前设备登录的华为账号的实名认证、游戏防沉迷信息，通过Promise对象获取返回值。|

## 开发步骤

### 导入模块

导入Game Service Kit模块及相关公共模块。

1. import { gamePlayer } from '@kit.GameServiceKit';
2. import { common } from '@kit.AbilityKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';
4. import { BusinessError } from '@kit.BasicServicesKit';
5. import { window } from '@kit.ArkUI';

### 初始化

调用[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)接口初始化Game Service Kit。

说明

- 调用接口时严格要求继承UIAbility，并且获取上下文的时机是onWindowStageCreate生命周期中页面加载成功后。
- 要求游戏先成功调用初始化[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)接口后再调用其他接口，否则将导致审核被驳回。

1. onWindowStageCreate(windowStage: window.WindowStage) {
2.   windowStage.loadContent("pages/index", (err, data) => {
3.     try {
4.       gamePlayer.init(this.context,()=>{
5.         hilog.info(0x0000, 'testTag', `Succeeded in initing.`);
6.       });
7.     } catch (error) {
8.       let err = error as BusinessError;
9.       hilog.error(0x0000, 'testTag', `Failed to init. Code: ${err.code}, message: ${err.message}`);
10.     }
11.   });
12. }

初始化后，游戏弹出华为隐私协议窗口，用户同意签署协议，则继续往下执行。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.26079837663144878114256409384918:50001231000000:2800:C54C41FD286CC0C62AEFCE85EDB51B59A8B488E1CD2A57D9D0D1498D70E0B7F7.png "点击放大")

若当前华为账号同意过游戏服务隐私协议，后续使用该华为账号登录的游戏将不会再弹出隐私协议窗口。

### 登录游戏

调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口登录游戏。

1. let context = this.getUIContext()?.getHostContext() as common.UIAbilityContext;
2. let request: gamePlayer.UnionLoginParam = {
3.   showLoginDialog: false, // 是否弹出联合登录面板。true表示强制弹出面板，false表示优先使用玩家上一次的登录选择，不弹出联合登录面板，若玩家首次登录或卸载重装，则正常弹出。
4.   thirdAccountInfos: [] // 单机游戏请传空数组。
5. };
6. try {
7.   gamePlayer.unionLogin(context, request).then((result: gamePlayer.UnionLoginResult) => {
8.     hilog.info(0x0000, 'testTag', `Succeeded in logining: ${result?.accountName}`);
9.   }).catch((error: BusinessError) => {
10.     hilog.error(0x0000, 'testTag', `Failed to login. Code: ${error.code}, message: ${error.message}`);
11.   });
12. } catch (error) {
13.   let err = error as BusinessError;
14.   hilog.error(0x0000, 'testTag', `Failed to login. Code: ${err.code}, message: ${err.message}`);
15. }

用户完成登录流程后，游戏顶部弹出欢迎横幅，并向游戏返回accountName（华为账号登录返回值为hw_account）、gamePlayerId等信息。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.44973294956303260048098705010701:50001231000000:2800:E6CD9BA8BC12CF51D013EB97CABB3C4B88FFBE1A34CC4930E473F04F0D455C59.png "点击放大")

### 合规校验

调用[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)接口对用户设备登录华为账号的实名认证和未成年人防沉迷进行合规校验，校验通过后，玩家进入游戏。

1. let context = this.getUIContext()?.getHostContext() as common.UIAbilityContext;
2. let request: gamePlayer.ThirdUserInfo = {
3.   thirdOpenId: '' // 单机游戏传空
4. };
5. try {
6.   gamePlayer.verifyLocalPlayer(context, request).then(() => {
7.     hilog.info(0x0000, 'testTag', `Succeeded in verifying.`);
8.   }).catch((error: BusinessError) => {
9.     hilog.error(0x0000, 'testTag', `Failed to verify. Code: ${error.code}, message: ${error.message}`);
10.   });
11. } catch (error) {
12.   let err = error as BusinessError;
13.   hilog.error(0x0000, 'testTag', `Failed to verify. Code: ${err.code}, message: ${err.message}`);
14. }

华为账号的实名认证、未成年人防沉迷由基础游戏服务实现，华为账号的支付合规控制（例如未成年人支付限额）由IAP Kit（应用内支付服务）实现。

|合规校验|校验项|国家政策|解决方案|
|:--|:--|:--|:--|
|华为账号实名认证|校验用户设备登录的华为账号是否已实名认证。|根据相关法律法规要求，所有网络游戏玩家必须使用真实有效身份信息注册并登录网络游戏。|若玩家使用未实名认证的华为账号登录游戏时，基础游戏服务向玩家弹出实名认证窗口，要求玩家进行实名认证。若玩家取消实名认证，则返回[1002000004](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code#section206921217496)错误码。|
|未成年人防沉迷|校验已实名认证为未成年人的华为账号是否在规定时间内登录游戏。|根据国家新闻出版署的最新规定，所有网络游戏企业仅可在周五、周六、周日和法定节假日每日20时至21时向未成年人提供1小时网络游戏服务，其他时间均不得以任何形式向未成年人提供网络游戏服务。|- 已实名认证为未成年人的华为账号在规定时间内登录游戏，当游戏进行到晚上21时，基础游戏服务会弹窗提示玩家已到游戏时间，强制玩家退出游戏并返回[1002000006](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code#section4418848101513)错误码。<br>- 已实名认证为未成年人的华为账号在非规定游戏时间内登录游戏，基础游戏服务会弹框提示玩家不允许游戏，强制玩家退出游戏并返回[1002000006](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code#section4418848101513)错误码。|
|未成年人支付限额|校验已实名认证为未成年人的华为账号是否限额付费。|根据国家新闻出版署的最新规定，网络游戏企业不得为未满8周岁的用户提供游戏付费服务。同一网络游戏企业所提供的游戏付费服务，8周岁以上未满16周岁的用户，单次充值金额不得超过50元人民币，每月充值金额累计不得超过200元人民币；16周岁以上未满18周岁的用户，单次充值金额不得超过100元人民币，每月充值金额累计不得超过400元人民币。|已实名认证为未成年人的华为账号在游戏内超额付费，IAP Kit会弹窗提示消费金额超出限制。<br><br>用户在使用华为应用内支付时，华为会自动根据国家新闻出版署的要求进行支付限额控制，您无需处理。|

|   |   |   |
|---|---|---|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.56197619912340813512749302535400:50001231000000:2800:165A5B1EDA45EFE922752982638FABA94B8F50454BF77F682B75277E4979823C.png "点击放大")<br><br>华为账号实名认证|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.56100537932784869221097877076765:50001231000000:2800:1A29094A6DB8881A319599C0578274319224AB738324AB0EB51D9F617380DF1F.png "点击放大")<br><br>未成年人防沉迷|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.99830369480498379078718458666122:50001231000000:2800:88305F9DB3507DBD92AD660FD513645676932225959C83B3314FED0DFCC104D5.png "点击放大")<br><br>未成年人支付限额|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-official "使用游戏官方账号登录")
# 开发后自检

更新时间: 2025-12-16 16:38

为减少提交审核后被驳回的概率，请参考如下自检CheckList进行自检。

自检通过后，再前往AppGallery Connect提交游戏上架审核，具体操作请参见[发布HarmonyOS游戏](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-game-0000002364930906)。

|一级分类|二级分类|检查项|影响|
|:--|:--|:--|:--|
|合规检查|隐私、游戏资质等|游戏内容、游戏安全性、用户隐私等符合华为应用市场审核规定，具体参考[应用审核指南](https://developer.huawei.com/consumer/cn/doc/50104)。|如不符合华为应用市场审核要求，游戏将会被驳回。|
|用户实名认证信息|游戏提交上架前在AppGallery Connect完成[版署实名认证申请](https://developer.huawei.com/consumer/cn/doc/games-guides/game-center-identification-applyfor-0000002392353221)并通过审核。|上架申请可能会被驳回。|
|配置检查|应用类型|登录AppGallery Connect，检查应用类型是否为游戏。|如果不是游戏类型，会导致游戏防沉迷异常，提交审核会被驳回。|
|发布包版本|上架游戏要求使用release版本的发布包。在SDK目录下检查oh-uni-package.json文件，非release要求替换，或者出包后解压并查看HAP资源文件夹，检查pack.info文件的releaseType字段。|使用非release版本的发布包申请上架会被驳回。|
|签名证书指纹信息|在发布阶段要求添加发布证书对应的指纹。|未添加发布证书对应的指纹会影响上架。|
|APP ID映射关系|前往AppGallery Connect[配置APP ID映射关系](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-huawei#section3907114313255)。|未配置APP ID映射关系会影响游戏上架。|
|module.json5文件|在工程的entry模块module.json5文件中，查看metadata中client_id和app_id是否配置准确。|如果配置错误，Game Service Kit的接口将调用失败。|
|代码检查|初始化|游戏启动后，要求先调用[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)接口，调用结束后再调用其他接口。|游戏如未调用init接口，将导致审核被驳回。|
|登录|华为账号登录图标要求遵守[开发者使用Account Kit的登录能力的管理细则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-detailedrules)。|如不符合规范，可能会影响游戏上架。|
|- 使用华为账号登录HarmonyOS 4及以下游戏与HarmonyOS 5.0及以上游戏时，账号资产要保持互通。<br>- 使用游戏官方账号登录官包与HarmonyOS 5.0及以上游戏时，账号资产要保持互通。|账号资产不互通会影响上架。|
|游戏登录必须调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口拉起联合登录面板进行登录。|游戏如未调用unionLogin接口将导致审核被驳回。|
|用户设备未登录华为账号时，[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口会拉起设备登录华为账号的弹窗。在窗口上点击返回后，该窗口无需反复自动弹出，且玩家可以手动再次拉起该窗口。|若设备登录华为账号的弹窗无法手动拉起，或反复自动弹出，将导致上架审核被驳回。|
|已接入官方账号登录的游戏，用户登录游戏默认沿用上次选择的登录账号，建议在游戏内为玩家提供[游戏内切换账号](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-official#section26517112362)功能，支持玩家重新选择游戏的登录账号。游戏重新拉起联合登录面板时，要求调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口将loginParam中的showLoginDialog参数设置为true。若调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口，整个游戏登录流程无需再调用[getLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section17453143012584)接口。|建议游戏支持玩家重新选择游戏的登录账号，否则游戏的登录体验不佳。|
|游戏登录后，要求调用[verifyLocalPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section15119154416715)接口进行合规校验，华为侧将校验当前设备的华为账号实名认证和游戏防沉迷管控情况，如校验未通过将返回对应的错误码。|游戏如未调用verifyLocalPlayer接口将导致审核被驳回。|
|支付|若游戏内提供商品购买，则要求接入[IAP Kit（应用内支付服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/iap-kit-guide)。|游戏如未调用createPurchase接口将导致审核被驳回。|
|purchase接口传入的商品ID和商品类型与AppGallery Connect创建的商品ID和商品类型一致。|如果支付时传入的商品ID或商品类型与AppGallery Connect不一致，将无法拉起支付页面。|
|支付接口调用返回时、应用启动时均进行了补单处理和错误码[1001860001](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/iap-error-code#section194868144472)、[1001860051](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/iap-error-code#section5254205612317)。请参考[权益发放](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/iap-delivering-products)。|如未在适当时机进行补单处理，会导致异常场景下（如关闭进程、崩溃）商品未正常发放。|
|游戏退出|发布中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）的游戏要求具备玩家退出功能。|如不具备退出功能，审核将会被驳回。|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-single-access "单机游戏登录")
# 概述

更新时间: 2025-12-16 16:37

从6.0.1(21)版本开始，新增小游戏相关能力。

小游戏是一种基于行业标准开发的新型免安装应用，无需安装，即点即玩，并且可以添加到设备桌面。开发者一次开发即可将小游戏分发到所有支持行业标准的设备运行。

## 约束与限制

小游戏相关能力支持Phone、Tablet、2in1和TV设备。

## 使用场景

提供给小游戏运行时应用间共享库调用，以实现小游戏的登录及支付功能。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-minigame "小游戏")
# 开发准备

更新时间: 2025-12-16 16:38

## 创建小游戏

在华为应用市场发布小游戏，要求前往AppGallery Connect创建小游戏类元服务，具体操作请参见[创建小游戏](https://developer.huawei.com/consumer/cn/doc/app/agc-help-create-minigame-0000002434138360)。其中：

- “应用类型”：选择“元服务”。
- “应用分类”：选择“小游戏”。

说明

用于正式上架的游戏包名建议不要包含test、dev等信息。

## 申请版署实名认证

按照版署《关于开展网络游戏防沉迷实名认证系统接口对接工作的通知》，各游戏出版运营企业均要求在2021年6月1日前完成接入[网络游戏防沉迷实名认证系统](https://wlc.nppa.gov.cn/fcm_company/index.html#/login?redirect=/)，并获取“bizID（游戏备案识别码）”，再将bizID配置到AppGallery Connect，华为将为游戏自动对接国家新闻出版署的实名认证系统并开启强制实名认证，开发者无需进行额外的开发。具体操作请参见[版署实名认证申请](https://developer.huawei.com/consumer/cn/doc/games-guides/game-center-identification-applyfor-0000002392353221)。

## 申请备案

请参考[APP备案FAQ](https://developer.huawei.com/consumer/cn/doc/App/50130#h2-1710150107897-0)、[快游戏备案指南](https://developer.huawei.com/consumer/cn/doc/quickApp-Guides/quickgame-filing-guide-0000001806139508)和[国产游戏小程序备案准备](https://developer.huawei.com/consumer/cn/doc/games-guides/quickgame-filing-chinese-preparation-0000001979934858)，完成小游戏备案，并保存好备案信息。

## 申请JSVM权限和存储空间管理开放能力

小游戏上架必须申请JSVM权限和存储空间管理开放能力，具体操作请参见[申请ACL权限和开放能力](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-minigame-acl-and-ability-0000002425276004)。

## 生成签名证书

数字证书和Profile文件等签名信息可以确保小游戏的完整性：

- 调试阶段：[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)、[申请调试证书](https://developer.huawei.com/consumer/cn/doc/app/agc-help-debug-cert-0000002283256797)、[申请调试Profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-debug-profile-0000002248181278)。
- 发布阶段：[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)、[申请发布证书](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-cert-0000002283336729)、[申请发布Profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-profile-0000002248341090)。

## 配置签名证书指纹

AppGallery Connect会自动生成证书对应的公钥信息，并计算出对应的SHA256指纹。开发者前往AppGallery Connect获取并配置SHA256指纹，且每个游戏至多添加4个签名证书指纹，配置签名证书指纹的具体操作请参见[配置公钥指纹](https://developer.huawei.com/consumer/cn/doc/app/agc-help-cert-fingerprint-0000002278002933)。

说明

请在调试阶段添加调试证书对应的指纹，在发布阶段添加发布证书对应的指纹。

## 配置APP ID、Client ID和权限信息

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，在“开发与服务”下选择项目及项目下的小游戏，获取“应用”下的APP ID和Client ID。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163759.20321376140887004497273818062891:50001231000000:2800:DC6B7F4D3E284D183E2428A33F3141561C5708755E3FC780787F3667FF19C241.png)
    
2. 在工程的entry模块module.json5文件中，新增metadata并配置client_id和app_id，同时新增requestPermissions以配置ACL权限和开放能力。如下所示：
    
    1. "module": {
    2.   "name": "entry",
    3.   "type": "xxx",
    4.   "description": "xxxx",
    5.   "mainElement": "xxxx",
    6.   "deviceTypes": [],
    7.   "pages": "xxxx",
    8.   "abilities": [],
    9.   "metadata": [ // 配置如下信息
    10.     {
    11.       "name": "client_id",
    12.       "value": "xxxxxx" // 配置为前面步骤中获取的Client ID
    13.     },
    14.     {
    15.       "name": "app_id",
    16.       "value": "xxxxxx" // 配置为前面步骤中获取的APP ID
    17.     }
    18.   ],
    19.   "requestPermissions": [ // 配置JSVM权限和存储空间管理开放能力
    20.     {
    21.       "name": "ohos.permission.kernel.ALLOW_EXECUTABLE_FORT_MEMORY"
    22.     },
    23.     {
    24.       "name": "ohos.permission.atomicService.MANAGE_STORAGE"
    25.     }
    26.   ]
    27. }
    

## 配置APP ID映射关系

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，在“开发与服务”下选择项目及项目下的小游戏，左侧菜单选择“构建 > 游戏服务”，在右侧点击“新增配置”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163759.22928895094416386653314128302627:50001231000000:2800:31F75E7E89BD7CA51393FCE53D178E2A0691550EEF9191D0F15567848CAD79D6.png)
    
2. 在弹出的“新增配置信息”窗口中填写信息，完成后点击“下一步”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163759.98902705521677815462579238213346:50001231000000:2800:E1F5BEB98F396CC1EFA758E40D418A1A844A1A3DA1796FAD1829FED09C433D32.png)
    
    |信息项|说明|
    |:--|:--|
    |HarmonyOS 5.0及以上游戏|请选择待上架的HAP小游戏。|
    |HarmonyOS 4及以下游戏|请选择已上架或草稿态的RPK快游戏。|
    
3. （可选）填写开发者服务器的回调地址，完成后点击“确定”提交APP ID映射关系的审批申请。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163759.52219278631649074703629983186659:50001231000000:2800:16AB312CDB0A977198FC0D56E7E556659667789D0C873EBE7FB7472543527ED0.png)
    
4. 若出现异常情况（例如在架状态不符合要求），将在提示框以红字提醒，建议点击“取消”并重新配置映射关系。若忽略异常情况点击“确定”继续提交申请，可能会造成映射关系审批不通过。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163759.07960421577440419058302561442380:50001231000000:2800:D38F39AF7583B4C483CC57107FCC249DD56B524E4A202D5306AC70DB408D5460.png)
    
5. 提交申请后，华为工作人员完成审核需要1~3个工作日，请耐心等待。APP ID映射关系生效后想要重新配置，请先提交映射关系的删除申请。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163800.27297869218135087433119691877410:50001231000000:2800:FE051080CAD596CCC57F3F32849732CC220DA466E5401805D6A1FEFDF0787C53.png)
    
    配置/删除APP ID映射关系的审核结果将通过互动中心或邮件进行通知。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163800.08240956656615309351456728642523:50001231000000:2800:000CA3DD63B34921CC7CF7C63F5A4F168EA1E8E0EE9CABC9B80AEEC5E6BAD5BA.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-minigame-introduction "概述")
# 小游戏登录

更新时间: 2025-12-16 16:38

小游戏接入基础游戏服务的小游戏登录API后，支持玩家使用华为账号快速进入游戏，且小游戏的华为账号实名认证、未成年人防沉迷功能由基础游戏服务实现。

## 前提条件

已完成[开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-minigame-preparation)。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163805.90790841871315891459637153825039:50001231000000:2800:B02D58B3390851761800785853794C0FE534139F722148188A41DAB427EF3B7A.png)

1. 玩家启动小游戏。
2. 小游戏调用[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)接口初始化Game Service Kit。初始化后，弹出华为隐私声明，玩家确认后可继续往下执行。
3. 小游戏调用[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section145017424483)接口注册小游戏防沉迷事件监听。
4. 小游戏调用[miniGameLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section44488469397)接口，实现玩家登录小游戏。
5. 小游戏顶部弹出欢迎横幅，并向小游戏返回playerId、playerSign等信息。同时对玩家是否完成实名认证及是否成年进行校验。
    - 若玩家未完成实名认证，[miniGameLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section44488469397)接口自动弹出实名认证窗口要求玩家进行实名认证。
    - 若玩家账号实名认证为未成年人，[miniGameLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section44488469397)接口将自动检测未成年人的游戏时间。若玩家不在指定时间内登录小游戏，将强制玩家退出小游戏并返回[1002000006](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code#section4418848101513)错误码。

## 接口说明

具体API说明详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer)。

|接口名|描述|
|:--|:--|
|[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)(context: common.UIAbilityContext, callback: AsyncCallback<void>): void|游戏初始化接口，使用默认的上下文信息，通过callback回调获取返回值。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section145017424483)(type: 'miniGameAddictionPrevented', callback: Callback<string>): void|小游戏防沉迷事件监听接口，通过callback回调获取小游戏防沉迷事件结果。|
|[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section171668301498)(type: 'miniGameAddictionPrevented', callback?: Callback<string>): void|取消小游戏防沉迷事件监听接口。|
|[miniGameLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section44488469397)(context: common.Context, loginParam: MiniGameLoginParam): Promise<MiniGamePlayer>|小游戏登录接口，通过Promise对象获取返回值。|

## 开发步骤

### 导入模块

导入Game Service Kit及公共模块。

1. import { gamePlayer } from '@kit.GameServiceKit';
2. import { common } from '@kit.AbilityKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';
4. import { BusinessError } from '@kit.BasicServicesKit';
5. import { window } from '@kit.ArkUI';

### 初始化

调用[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)接口初始化Game Service Kit。

1. onWindowStageCreate(windowStage: window.WindowStage) {
2.   windowStage.loadContent("pages/index", (err, data) => {
3.     try {
4.       gamePlayer.init(this.context,()=>{
5.         hilog.info(0x0000, 'testTag', `Succeeded in initing.`);
6.       });
7.     } catch (error) {
8.       let err = error as BusinessError;
9.       hilog.error(0x0000, 'testTag', `Failed to init. Code: ${err.code}, message: ${err.message}`);
10.     }
11.   });
12. }

### 监听小游戏防沉迷事件

调用[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section145017424483)接口注册小游戏防沉迷事件监听。

1. private miniGameAddictionPreventedCallback(result: string) {
2.   // 退出小游戏
3. }
4. // ...
5. // 调用on接口注册小游戏防沉迷事件监听
6. try {
7.   gamePlayer.on('miniGameAddictionPrevented', this.miniGameAddictionPreventedCallback);
8. } catch (error) {
9.   let err = error as BusinessError;
10.   hilog.error(0x0000, 'testTag', `Failed to register. Code: ${err.code}, message: ${err.message}`);
11. }

### 小游戏登录

调用[miniGameLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section44488469397)接口登录小游戏。

1. let context = this.getUIContext()?.getHostContext() as common.UIAbilityContext;
2. let request: gamePlayer.MiniGameLoginParam = {
3.   'gameAppId': '123xxx', // 小游戏appId
4.   'extraData': 'xxx' // 附加信息，要求JSON String格式
5. };
6. try {
7.   gamePlayer.miniGameLogin(context, request).then((result: gamePlayer.MiniGamePlayer) => {
8.     hilog.info(0x0000, 'testTag', `Succeeded in logining`);
9.   }).catch((error: BusinessError) => {
10.     hilog.error(0x0000, 'testTag', `Failed to login. Code: ${error.code}, message: ${error.message}`);
11.   });
12. } catch (error) {
13.   let err = error as BusinessError;
14.   hilog.error(0x0000, 'testTag', `Failed to login. Code: ${err.code}, message: ${err.message}`);
15. }

### 取消监听小游戏防沉迷事件

游戏退出时通过调用[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section171668301498)接口取消监听状态。

1. // 取消miniGameAddictionPrevented事件的全部监听
2. try {
3.   gamePlayer.off('miniGameAddictionPrevented');
4. } catch (error) {
5.   let err = error as BusinessError;
6.   hilog.error(0x0000, 'testTag', `Failed to unregister. Code: ${err.code}, message: ${err.message}`);
7. }

8. // 取消miniGameAddictionPrevented事件监听
9. try {
10.   // 参数this.miniGameAddictionPreventedCallback为gamePlayer.on('miniGameAddictionPrevented', this.miniGameAddictionPreventedCallback)中第二个参数
11.   gamePlayer.off('miniGameAddictionPrevented', this.miniGameAddictionPreventedCallback);
12. } catch (error) {
13.   let err = error as BusinessError;
14.   hilog.error(0x0000, 'testTag', `Failed to unregister. Code: ${err.code}, message: ${err.message}`);
15. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-minigame-preparation "开发准备")
# 小游戏支付

更新时间: 2025-12-16 16:38

小游戏接入基础游戏服务的小游戏支付API后，支持在小游戏内提供付费商品，玩家可以在小游戏内进行购买。

## 前提条件

- 已完成[开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-minigame-preparation)。
- 已开通[商户服务](https://developer.huawei.com/consumer/cn/doc/start/merchant-service-0000001053025967)。
- 已前往AGC控制台为小游戏[添加数字商品](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-minigame-goods-0000002424923350)。

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163808.52004686124861302014277743303002:50001231000000:2800:602B864D09BD4F6578706FC4A530379CE4F9AADBE119BB67F3E39CEAD9DC8FE5.png)

1. 玩家在小游戏内购买商品。
2. 小游戏调用[miniGamePay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section91831924175010)向Game Service Kit发起支付请求。
3. Game Service Kit向IAP Kit发送请求拉起收银台，IAP Kit处理支付请求，详情请参考[商品购买](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/iap-purchases)。
4. IAP Kit处理完成后向Game Service Kit返回此次商品购买的结果等信息。
5. Game Service Kit返回此次商品购买的结果等信息，开发者将接收到一个[CreatePurchaseResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section193852021105111)对象，对象内的purchaseData字段包括了此次购买的结果信息。

## 接口说明

具体API说明详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer)。

|接口名|描述|
|:--|:--|
|[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)(context: common.UIAbilityContext, callback: AsyncCallback<void>): void|游戏初始化接口，使用默认的上下文信息，通过callback回调获取返回值。|
|[miniGamePay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section91831924175010)(context: common.Context, parameter: PurchaseParameter): Promise<CreatePurchaseResult>|小游戏支付接口，通过Promise对象获取返回值。|

## 开发步骤

### 导入模块

导入Game Service Kit及公共模块。

1. import { gamePlayer } from '@kit.GameServiceKit';
2. import { common } from '@kit.AbilityKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';
4. import { BusinessError } from '@kit.BasicServicesKit';
5. import { window } from '@kit.ArkUI';

### 初始化

调用[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section225333655719)接口初始化Game Service Kit。

1. onWindowStageCreate(windowStage: window.WindowStage) {
2.   windowStage.loadContent("pages/index", (err, data) => {
3.     try {
4.       gamePlayer.init(this.context,()=>{
5.         hilog.info(0x0000, 'testTag', `Succeeded in initing.`);
6.       });
7.     } catch (error) {
8.       let err = error as BusinessError;
9.       hilog.error(0x0000, 'testTag', `Failed to init. Code: ${err.code}, message: ${err.message}`);
10.     }
11.   });
12. }

### 发起支付请求

调用[miniGamePay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section91831924175010)向Game Service Kit发起支付请求，Game Service Kit将向IAP Kit发送请求拉起收银台，IAP Kit处理支付请求。IAP Kit处理完成后向Game Service Kit返回此次商品购买的结果等信息，Game Service Kit将此次商品购买的结果等信息通过[CreatePurchaseResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section193852021105111)对象返回给开发者。

1. let context = this.getUIContext()?.getHostContext() as common.UIAbilityContext;
2. let request: gamePlayer.PurchaseParameter = {
3.   productId: 'xxx', // 待支付的商品ID
4.   productType: 0, // 待查询的商品类型
5.   developerPayload: 'xxx', // 商户侧保留信息，该参数长度限制为[0, 256]。若该字段有值，在支付成功后的回调结果中会原样返回给应用。
6.   reservedInfo: 'xxx' // 要求JSON String格式，商户可以将额外需要传入的字段以key-value的形式设置在JSON String中，并通过该参数传入。
7. };
8. try {
9.   gamePlayer.miniGamePay(context, request).then((result: gamePlayer.CreatePurchaseResult) => {
10.     hilog.info(0x0000, 'testTag', `Succeeded in paying`);
11.   }).catch((error: BusinessError) => {
12.     hilog.error(0x0000, 'testTag', `Failed to pay. Code: ${error.code}, message: ${error.message}`);
13.   });
14. } catch (error) {
15.   let err = error as BusinessError;
16.   hilog.error(0x0000, 'testTag', `Failed to pay. Code: ${err.code}, message: ${err.message}`);
17. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-minigame-login "小游戏登录")
# 基础游戏服务术语

更新时间: 2025-12-16 16:36

## H

### HarmonyOS 4及以下

包含HarmonyOS 3.1/4.0及以下、EMUI在内的老系统。

### HarmonyOS 5.0及以上

HarmonyOS 5.0及以上商用版本的新系统。

## I

### Interoperability

互通是HarmonyOS 4及以下系统与HarmonyOS 5.0及以上系统的玩家标识进行统一化，支持玩家使用华为账号登录新老系统的游戏。并且新老系统下的账号资产保持一致。

## S

### Standalone Games

单机游戏，是指游戏数据本地化存储，不依赖服务器。

## U

### User ID

HarmonyOS 4及以下系统或HarmonyOS 5.0及以上系统的玩家标识。

|系统|名称|组成|说明|
|:--|:--|:--|:--|
|HarmonyOS 5.0及以上系统|gamePlayerId|根据[配置APP ID映射关系](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-huawei#section3907114313255)时的选择openId或playerId。|用于华为账号登录的玩家标识。<br><br>不同游戏下，同一玩家的gamePlayerId不同。|
|teamPlayerId|teamPlayerId≈uid+developerid|同一个开发者账号developerid下的不同游戏，玩家使用同一个华为账号登录后获取的teamPlayerId相同。<br><br>新接入基础游戏服务的游戏无需关注该玩家标识。|
|HarmonyOS 4及以下系统|openId|由华为账号（用户账号）和应用唯一标识组合加密起来的用户标识。<br><br>简单理解：openid≈uid+clientid|openId是应用内唯一账号标识。若应用主体转移后，该openId标识不会发生改变。<br><br>使用相同华为账号登录不同的游戏（包括同一个开发者的不同游戏），获取到的openId唯一且不相同。|
|playerId|华为游戏服务给华为账号（用户账号）封装处理后的对外开放的游戏玩家标识。<br><br>简单理解：playerId≈uid|playerId仅跟华为账号（用户账号）有关，不会随着应用或开发者账号信息变化而变化，用于游戏类应用。|
|unionId|由华为账号（用户账号）和开发者账号组合加密后的用户标识。<br><br>简单理解：unionid≈uid+developerid|unionId是同一个开发者主体下的唯一账号标识。若应用主体转移后，unionId会发生改变。<br><br>同一个开发者主体下的不同游戏，使用华为账号登录后获取的unionId相同。|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-minigame-pay "小游戏支付")
# 概述

更新时间: 2025-12-16 16:36

## 功能说明

游戏场景感知提供API接口，帮助开发者快速实现游戏与系统的交互，开发者通过游戏场景感知，可以完成向系统发送游戏信息以及从系统获取设备状态信息两大动作。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163632.49875437760164376704833703191052:50001231000000:2800:026D333B16838EBB0F9BAB3949A148DB47BB1277EAF27E66A8F6DAE557A7B001.jpg)

## 场景介绍

游戏场景感知主要服务于游戏场景优化，其特点是可以通过感知游戏场景和运行状态的不同，使用不同策略调度系统资源以达到更精细化的优化效果。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameperformance-dev "游戏场景感知（可选）")
# 开发准备

更新时间: 2025-12-16 16:36

## 创建游戏

若在华为应用市场发布游戏，或使用AGC控制台提供的服务，需要前往AGC控制台创建游戏类应用，具体操作请参见[创建项目](https://developer.huawei.com/consumer/cn/doc/app/agc-help-create-project-0000002242804048)和[创建HarmonyOS应用](https://developer.huawei.com/consumer/cn/doc/app/agc-help-create-app-0000002247955506)。其中：

- “应用类型”：选择“HarmonyOS应用”。
- “应用分类”：选择“游戏”。

## 生成签名证书

数字证书和Profile文件等签名信息可以确保游戏的完整性，请参见[配置签名信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview#section42841246144813)完成配置。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameperformance-introduction "概述")
# 开发指导(ArkTS)

更新时间: 2025-12-16 16:36

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163658.78351701403145598413075205801631:50001231000000:2800:3323EECFCDA202AB4B6250444DF1757E15116D505B28E8A7142783F3BFED8B12.png)

1. 游戏启动后调用[gamePerformance.init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section131971556806)接口对游戏场景感知进行初始化。
2. 初始化成功后，游戏调用[gamePerformance.on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section17453143012584)接口注册设备状态变化事件监听，订阅设备状态变化通知。
3. 游戏调用[gamePerformance.updateGameInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section225333655719)接口向游戏场景感知上报游戏信息（包信息、配置信息、场景信息和网络信息等）。
4. 游戏场景感知广播游戏信息给终端系统。
5. 终端系统根据游戏信息进行系统资源调度。
6. 终端系统会将设备状态变化通知游戏场景感知。
7. 游戏场景感知向游戏客户端反馈设备状态变化。
8. 如不再需要订阅，游戏可调用[gamePerformance.off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section3614173614593)接口取消设备状态变化事件监听。
9. 游戏调用[gamePerformance.getDeviceInfoByScope](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section106164517195)接口向游戏场景感知主动查询设备状态信息。

说明

Mali系列GPU不支持采集GPU信息，调用订阅和查询设备状态信息接口时无法获取设备GPU信息。

## 接口说明

具体API说明详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance)。

|接口名|描述|
|:--|:--|
|[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section131971556806)(gamePackageInfo: GamePackageInfo): Promise<void>|游戏初始化接口，对游戏场景感知进行初始化，通过Promise对象获取返回值。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section17453143012584)(type: 'deviceStateChanged', callback: Callback<DeviceInfo>): void|订阅设备状态变化接口，主要用于监听deviceStateChanged（设备状态变化）事件。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section060864914495)(type: 'deviceStateChanged', callback: Callback<DeviceInfo>, scope: Array<DeviceInfoType>): void|按需订阅设备状态变化接口。主要用于监听deviceStateChanged（设备状态变化）事件，支持传入参数指定订阅的设备状态信息类型。|
|[updateGameInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section225333655719)<T extends BaseGameInfo>(gameInfo: T): Promise<void>|更新游戏信息接口，主要用于上报游戏信息（包信息、配置信息、场景信息和网络信息等），通过Promise对象获取返回值。|
|[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section3614173614593)(type: 'deviceStateChanged', callback?: Callback<DeviceInfo>): void|取消订阅设备状态变化接口，主要用于取消监听deviceStateChanged（设备状态变化）事件。|
|[getDeviceInfoByScope](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section106164517195)(scope: Array<DeviceInfoParameter>): Promise<DeviceInfo>|查询设备状态信息接口。|

## 接入步骤

### 导入模块

导入Game Service Kit及公共模块。

1. import { gamePerformance } from '@kit.GameServiceKit';
2. import { hilog } from '@kit.PerformanceAnalysisKit';
3. import { BusinessError } from '@kit.BasicServicesKit';

### 初始化

导入相关模块后，需先调用[init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section131971556806)接口对游戏场景感知进行初始化。

说明

init接口是调用其他接口的前提，如果未初始化或初始化失败，将无法调用其他接口。

1. let gamePackageInfo: gamePerformance.GamePackageInfo = {
2.   messageType: 0,
3.   bundleName: "com.example.demo", // 仅示例，请替换为实际的游戏包名
4.   appVersion: "1.0"
5. }
6. try {
7.   gamePerformance.init(gamePackageInfo).then(() => {
8.     // 初始化成功
9.     hilog.info(0x0001, 'demo', `Succeeded in initializing.`);
10.   })
11. } catch (error) {
12.   // 初始化失败
13.   let err = error as BusinessError;
14.   hilog.error(0x0001, 'demo', `Failed to initialize. Code: ${err.code}, message: ${err.message}`);
15. }

### 订阅设备状态变化

调用[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section17453143012584)接口可以订阅设备状态变化事件，获取设备状态变化的通知（如设备温控档位）。

1. function onDeviceStateChange(data:gamePerformance.DeviceInfo) {
2.   // 设备信息详情
3.   hilog.info(0x0001, 'demo', `device state changed. tempLevel is ${data.tempLevel}`);
4. }

5. // 订阅deviceStateChanged事件
6. try {
7.   gamePerformance.on('deviceStateChanged', onDeviceStateChange);
8. } catch (error) {
9.   // 订阅失败
10.   let err = error as BusinessError;
11.   hilog.error(0x0001, 'demo', `Failed to subscribe. Code: ${err.code}, message: ${err.message}`);
12. }

目前支持订阅GPU和温度变化趋势两种类型的设备状态数据，也可以调用[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section060864914495)接口按需订阅，如只订阅GPU数据：

1. function onDeviceStateChange(data:gamePerformance.DeviceInfo) {
2.   // data中仅含有gpuInfo
3.   hilog.info(0x0001, 'demo', `device state changed. tempLevel is ${data.tempLevel}`);
4. }

5. // 订阅deviceStateChanged事件
6. try {
7.   let types:Array<gamePerformance.DeviceInfoType> = [gamePerformance.DeviceInfoType.GPU];
8.   gamePerformance.on('deviceStateChanged', onDeviceStateChange, types);
9. } catch (error) {
10.   // 订阅失败
11.   let err = error as BusinessError;
12.   hilog.error(0x0001, 'demo', `Failed to subscribe. Code: ${err.code}, message: ${err.message}`);
13. }

### 上报游戏信息

初始化成功后，可以通过调用[updateGameInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section225333655719)接口上报游戏信息（包信息、配置信息、场景信息和网络信息等）。若需上报自定义数据，可调用[addGameCustomData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section72524718166)接口。

1. // 以更新游戏场景信息为例
2. let gameSceneInfo: gamePerformance.GameSceneInfo = {
3.   messageType: 2,
4.   sceneID: 7,
5.   importanceLevel: 4
6. }
7. try {
8.   gamePerformance.updateGameInfo(gameSceneInfo).then(() => {
9.     // 更新游戏场景信息成功
10.     hilog.info(0x0001, 'demo', `Succeeded in updating.`);
11.   });
12. } catch (error) {
13.   // 更新游戏场景信息失败
14.   let err = error as BusinessError;
15.   hilog.error(0x0001, 'demo', `Failed to update. Code: ${err.code}, message: ${err.message}`);
16. }

### 取消订阅设备状态

如不再需要订阅，则可以通过调用[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section3614173614593)接口取消订阅设备状态。

1. function onDeviceStateChange(data:gamePerformance.DeviceInfo) {
2.   // 设备信息详情
3.   hilog.info(0x0001, 'demo', `device state changed. tempLevel is ${data.tempLevel}`);
4. }

5. // 取消订阅deviceStateChanged事件
6. try {
7.   gamePerformance.off('deviceStateChanged', onDeviceStateChange);
8. } catch (error) {
9.   // 取消订阅失败
10.   let err = error as BusinessError;
11.   hilog.error(0x0001, 'demo', `Failed to unsubscribe. Code: ${err.code}, message: ${err.message}`);
12. }

13. // 取消deviceStateChanged事件的全部订阅
14. try {
15.   gamePerformance.off("deviceStateChanged");
16. } catch (error) {
17.   // 取消订阅失败
18.   let err = error as BusinessError;
19.   hilog.error(0x0001, 'demo', `Failed to unsubscribe. Code: ${err.code}, message: ${err.message}`);
20. }

### 查询设备状态信息

除订阅设备状态变化的方式外，也可以通过调用[getDeviceInfoByScope](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameperformance#section106164517195)接口主动查询设备状态：

1. // 查询设备状态
2. try {
3.   let gpuParam: gamePerformance.DeviceInfoParameter = {
4.     deviceInfoType: gamePerformance.DeviceInfoType.GPU
5.   }
6.   let thermalParam: gamePerformance.DeviceInfoParameter = {
7.     deviceInfoType: gamePerformance.DeviceInfoType.THERMAL     
8.   }
9.   let gameInfos: Array<gamePerformance.DeviceInfoParameter> = [gpuParam, thermalParam];
10.   gamePerformance.getDeviceInfoByScope(gameInfos).then((deviceInfo:gamePerformance.DeviceInfo) => {
11.     hilog.info(0x0001, 'demo', `Succeeded in querying device info. tempLevel is ${deviceInfo.tempLevel}`);
12.   });
13. } catch (error) {
14.   // 查询失败
15.   let err = error as BusinessError;
16.   hilog.error(0x0001, 'demo', `Failed to query. Code: ${err.code}, message: ${err.message}`);
17. }

主动查询接口同样支持按需查询，如只查询温度变化趋势数据：

1. // 只查询设备温度数据
2. try {
3.   let thermalParam: gamePerformance.DeviceInfoParameter = {
4.     deviceInfoType: gamePerformance.DeviceInfoType.THERMAL     
5.   }
6.   let gameInfos: Array<gamePerformance.DeviceInfoParameter> = [thermalParam];
7.   gamePerformance.getDeviceInfoByScope(gameInfos).then((deviceInfo:gamePerformance.DeviceInfo) => {
8.     // 此处的查询结果中将不含有gpuInfo
9.     hilog.info(0x0001, 'demo', `Succeeded in querying device info. tempLevel is ${deviceInfo.tempLevel}`);
10.   });
11. } catch (error) {
12.   // 查询失败
13.   let err = error as BusinessError;
14.   hilog.error(0x0001, 'demo', `Failed to query. Code: ${err.code}, message: ${err.message}`);
15. }

说明

查询温度变化趋势需要历史数据作为计算依据，调用该接口时请保证设备已启动至少一分钟，否则会返回1010300003错误。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameperformance-config-agc "开发准备")
# 开发准备

更新时间: 2025-12-16 16:36

说明

游戏近场快传功能当前受限开放。如需使用，请通过[在线提单](https://developer.huawei.com/consumer/cn/support/feedback/#/)的方式提供APP ID申请开通。

## 创建游戏

若在华为应用市场发布游戏，或使用AGC控制台提供的服务，需要前往AGC控制台创建游戏类应用，具体操作请参见[创建项目](https://developer.huawei.com/consumer/cn/doc/app/agc-help-create-project-0000002242804048)和[创建HarmonyOS应用](https://developer.huawei.com/consumer/cn/doc/app/agc-help-create-app-0000002247955506)。其中：

- “应用类型”：选择“HarmonyOS应用”。
- “应用分类”：选择“游戏”。

## 生成签名证书

数字证书和Profile文件等签名信息可以确保游戏的完整性，请参见[配置签名信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview#section42841246144813)完成配置。

## 配置APP ID和相关权限

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)平台，在“开发与服务”中选择目标应用，获取“项目设置 > 常规 > 应用”的**APP ID**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163646.46212774659316222983215122342811:50001231000000:2800:E9457F6A50710537C1B01AFB51466F2B78218F2C8B5ACF00BA795BBF52A64E66.png)
    
2. 在工程的entry模块module.json5文件中，新增metadata并配置app_id，同时新增requestPermissions并配置如下权限。
    
    1. "module": {
    2.   "name": "entry",
    3.   "type": "entry",
    4.   "description": "xxxx",
    5.   "mainElement": "xxxx",
    6.   "deviceTypes": [
    7.     "phone"
    8.   ],
    9.   "deliveryWithInstall": true,
    10.   "pages": "$profile:main_pages",
    11.   "abilities": [],
    12.   "metadata": [ // 配置如下信息
    13.     {
    14.       "name": "app_id",
    15.       "value": "xxxxxx" // 配置为前面步骤中获取的APP ID
    16.     }
    17.   ],
    18.    "requestPermissions": [ // 配置权限
    19.      {
    20.        "name": "ohos.permission.INTERNET" // 允许使用Internet网络权限
    21.      },
    22.      {
    23.        "name": "ohos.permission.GET_NETWORK_INFO"  // 允许应用获取数据网络信息权限
    24.      },
    25.      {
    26.        "name": "ohos.permission.SET_NETWORK_INFO" // 允许应用配置数据网络权限
    27.      },
    28.      {
    29.        "name": "ohos.permission.DISTRIBUTED_DATASYNC", // 允许不同设备间的数据交换权限
    30.        "reason": "$string:distributed_permission",
    31.        "usedScene": {
    32.          "abilities": [
    33.            "EntryAbility"
    34.          ],
    35.          "when": "inuse"
    36.        }
    37.      }
    38.    ]
    39. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-nearbytransfer-introduction "概述")
# 开发指导(ArkTS)

更新时间: 2025-12-16 16:36

## 业务流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163658.20567914177414033590646584546632:50001231000000:2800:626EA16F8309EC9C391D4F902698B012C9BBF5B157D3E3B92539852CCF6DF645.png)

1. 发送端和接收端调用[create](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section131971556806)创建游戏近场快传服务。
2. 创建成功后，游戏客户端调用以下接口注册监听。
    - 注册连接通知监听接口：[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section17453143012584)('connectNotify')
    - （发送端选择绑定接收端情况下需调用）注册发现结果事件监听接口：[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section766518402463)('discovery')
    - 注册收到包信息监听接口：[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section1959517425315)('receivePackageInfo')
    - 注册传输通知监听接口：[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section05583466314)('transferNotify')
    - 注册错误事件监听接口：[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section122432503314)('error')
3. 接收端调用[publishNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section225333655719)发布自身近场快传服务。
4. 绑定接收端，支持如下两种方式。
    - 自动绑定：
        
        发送端调用[autoBindNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section52391745713)自动绑定附近设备（搜索并绑定附近10米内第一个发现的近场快传服务）。
        
        说明
        
        自动绑定操作2分钟内有效，超时需重新调用接口。
        
    - 选择绑定：
        
        发送端调用[discoveryNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section16687197125918)发现附近设备，发现操作完成后将收到discovery事件回调，获得可绑定的设备列表供玩家选择，调用[bindNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section13279659901)接口绑定玩家选定的接收端设备。
        
        说明
        
        发现操作2分钟内有效，超时需重新调用接口。
        
5. 接收端收到UIAbility的[onCollaborate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#oncollaborate18)回调后调用[acceptCollaboration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section106164517195)接受协同。
6. 接收端收到建链成功connectNotify事件回调。
7. 接收端调用[sendPackageInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section12490112992612)发送自身文件信息，如版本信息、包信息。
8. 发送端收到receivePackageInfo事件回调。
9. 发送端比较版本并调用[replyPackageInfoResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section78288285293)上报对比结果。
10. 如发送端对比结果为需要发送，则调用[transferPackageData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section1227711101118)向接收端发送需要传输的资源包。
11. 接收端可在transferNotify回调中获取当前已传输的包体大小、包体总大小、传输速率、传输剩余时间等信息，传输完成可获取已接收资源包的存储目录，对传输完成的资源文件做处理。
12. 处理传输完成的资源文件后，可调用[destroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section13373155416)销毁服务。
    
    说明
    
    - destroy接口会清除已接收数据，请确保对已接收数据做好处理或转移后再调用该接口。
    - 每次调用[create](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section131971556806)接口会自动清理自身历史数据。
    

## 接口说明

具体API说明详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer)。

|接口名|描述|
|:--|:--|
|[create](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section131971556806)(createParameters: CreateParameters): Promise<CreateResult>|创建游戏近场快传服务。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section17453143012584)(type: 'connectNotify', callback: Callback<ConnectNotification>): void|订阅连接通知事件。|
|[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section3614173614593)(type: 'connectNotify', callback?: Callback<ConnectNotification>): void|取消订阅连接通知事件。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section766518402463)(type: 'discovery', callback: Callback<DiscoveryResult>): void|订阅发现结果事件。|
|[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section10671640104614)(type: 'discovery', callback?: Callback<DiscoveryResult>): void|取消订阅发现结果事件。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section1959517425315)(type: 'receivePackageInfo', callback: Callback<PackageInfo>): void|订阅收到包信息事件。|
|[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section1359944210319)(type: 'receivePackageInfo', callback?: Callback<PackageInfo>): void|取消订阅收到包信息事件。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section05583466314)(type: 'transferNotify', callback: Callback<TransferNotification>): void|订阅传输通知事件。|
|[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section65611146153113)(type: 'transferNotify', callback?: Callback<TransferNotification>): void|取消订阅传输通知事件。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section122432503314)(type: 'error', callback: Callback<ReturnResult>): void|订阅错误事件。|
|[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section20246850163115)(type: 'error', callback?: Callback<ReturnResult>): void|取消订阅错误事件。|
|[publishNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section225333655719)(): Promise<void>|发布近场快传服务。|
|[autoBindNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section52391745713)(): Promise<void>|自动绑定近场快传服务。|
|[discoveryNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section16687197125918)(): Promise<void>|发现近场快传服务。|
|[bindNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section13279659901)(bindParameters: BindParameters): Promise<void>|绑定指定近场快传服务。|
|[acceptCollaboration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section106164517195)(acceptParameters: Record<string, object>): Promise<void>|接受协同。|
|[sendPackageInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section12490112992612)(packageInfo: PackageInfo): Promise<void>|接收端发送自身文件信息。|
|[replyPackageInfoResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section78288285293)(packageInfoResult: PackageInfoResult): Promise<void>|上报包信息对比结果。|
|[transferPackageData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section1227711101118)(packageData: PackageData): Promise<void>|传输包数据。|
|[destroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section13373155416)(): Promise<void>|销毁游戏近场快传服务。|

## 接入步骤

### 导入模块

导入Game Service Kit及公共模块。

1. import { abilityAccessCtrl, AbilityConstant, UIAbility, common } from "@kit.AbilityKit";
2. import { hilog } from '@kit.PerformanceAnalysisKit';
3. import { gameNearbyTransfer } from '@kit.GameServiceKit';
4. import { BusinessError } from '@kit.BasicServicesKit';

### 申请权限

申请ohos.permission.DISTRIBUTED_DATASYNC权限用于设备发现，详情可参考[向用户申请授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/request-user-authorization)。

1. let atManager = abilityAccessCtrl.createAtManager();
2. let uiAbilityContext = this.getUIContext()?.getHostContext() as common.UIAbilityContext;
3. try {
4.   atManager.requestPermissionsFromUser(uiAbilityContext, ['ohos.permission.DISTRIBUTED_DATASYNC']).then((data) => {
5.     hilog.info(0x0000, 'nearby', '%{public}s', 'data: ' + JSON.stringify(data));
6.   }).catch((err: object) => {
7.     hilog.error(0x0000, 'nearby', '%{public}s', 'err: ' + JSON.stringify(err));
8.   })
9. } catch (err) {
10.   hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
11. }

### 创建游戏近场快传服务并注册相关回调

导入相关模块后，需先调用[create](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section131971556806)接口创建游戏近场快传服务，然后注册各回调事件。

说明

[create](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section131971556806)接口是调用其他接口的前提，如果未创建游戏近场快传服务或创建失败，将无法调用其他接口。

1. public create() {
2.   let uiAbilityContext = this.getUIContext()?.getHostContext() as common.UIAbilityContext;
3.   let initParam: gameNearbyTransfer.CreateParameters = {
4.     abilityName: uiAbilityContext.abilityInfo.name,
5.     context: uiAbilityContext,
6.     moduleName: uiAbilityContext.abilityInfo.moduleName,
7.     needShowSystemUI: false // 是否展示系统UI，true为展示，false为不展示，默认为false
8.   };
9.   try {
10.     gameNearbyTransfer.create(initParam).then((createResult) => {
11.       hilog.info(0x0000, '[nearby]', '%{public}s', 'create success' + createResult.localDeviceName);
12.       this.registerCallback();
13.     }).catch((err: BusinessError) => {
14.       hilog.error(0x0000, '[nearby]', '%{public}s', 'create error' + (err as Error).message);
15.     })
16.   } catch (err) {
17.     hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
18.   }
19. }

20. // 注册监听
21. public registerCallback() {
22.   try {
23.     gameNearbyTransfer.on('connectNotify', connectNotifyCallBack);
24.     gameNearbyTransfer.on('receivePackageInfo', receivePackageInfoCallBack);
25.     gameNearbyTransfer.on('transferNotify', transferNotifyCallBack);
26.     gameNearbyTransfer.on('error', errorCallBack);
27.   } catch (err) {
28.     hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
29.   }
30. }

31. function connectNotifyCallBack(callback: gameNearbyTransfer.ConnectNotification) {
32.   // 连接状态回调，接收端收到建链成功回调后，在此处调用sendPackageInfo接口发送自身文件信息，如版本信息、包信息
33. }

34. function receivePackageInfoCallBack(callback: gameNearbyTransfer.PackageInfo) {
35.   // 接收包信息回调，发送端收到接收端发送的版本信息后进行对比，根据对比结果决定是否需要传输资源包数据。
36. }

37. function transferNotifyCallBack(callback: gameNearbyTransfer.TransferNotification) {
38.   // 传输回调，处理传输进度信息
39. }

40. function errorCallBack(callback: gameNearbyTransfer.ReturnResult) {
41.   // 异常信息回调，处理相关异常信息
42. }

### 接收端接受协同

接收端实现[onCollaborate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-uiability#oncollaborate18)回调，回调中调用[acceptCollaboration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section106164517195)接口接受协同。

1. export default class EntryAbility extends UIAbility { 
2.   // 协同回调
3.   onCollaborate(wantParam: Record<string, Object>): AbilityConstant.CollaborateResult {
4.     try {
5.       gameNearbyTransfer.acceptCollaboration(wantParam);
6.     } catch (err) {
7.       hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
8.     }
9.     hilog.info(0x0000, '[nearby]', '%{public}s', 'onCollaborate: accept collaborate');
10.     return AbilityConstant.CollaborateResult.ACCEPT;
11.   }
12. }

### 接收端发布自身游戏近场快传服务

接收端调用[publishNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section225333655719)接口发布自身游戏近场快传服务。

1. try {
2.   gameNearbyTransfer.publishNearbyGame().then(() => {
3.     hilog.info(0x0000, '[nearby]', '%{public}s', 'publishNearbyGame success');
4.   }).catch((err: BusinessError) => {
5.     hilog.error(0x0000, '[nearby]', '%{public}s', 'publishNearbyGame error' + (err as Error).message);
6.   })
7. } catch (err) {
8.   hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
9. }

### 发送端绑定接收端游戏近场快传服务

发送端绑定接收端游戏近场快传服务支持如下两种方式：

- 方式一：自动绑定
    
    发送端调用[autoBindNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section52391745713)接口自动绑定接收端近场快传服务。
    
    1. try {
    2.   gameNearbyTransfer.autoBindNearbyGame().then(() => {
    3.     hilog.info(0x0000, '[nearby]', '%{public}s', 'autoBindNearbyGame success');
    4.   }).catch((err: BusinessError) => {
    5.     hilog.error(0x0000, '[nearby]', '%{public}s', 'autoBindNearbyGame error' + (err as Error).message);
    6.   })
    7. } catch (err) {
    8.   hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
    9. }
    

- 方式二：选择绑定
    1. 发送端调用[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section766518402463)('discovery')接口注册“发现设备”结果事件监听。
        
        1. try {
        2.   gameNearbyTransfer.on('discovery', discoveryCallBack);
        3. } catch (err) {
        4.   hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message)
        5. }
        
        6. function discoveryCallBack(callback: gameNearbyTransfer.DiscoveryResult) {
        7.   // 获取到发现的设备 展示设备列表
        8.   callback.nearbyGameDevices.forEach((device: gameNearbyTransfer.NearbyGameDevice, index: number) => {    
        9.   });
        10. }
        
    2. 发送端调用[discoveryNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section16687197125918)发现附近设备。
        
        1. try {
        2.   gameNearbyTransfer.discoveryNearbyGame().then(() => {
        3.     hilog.info(0x0000, '[nearby]', '%{public}s', 'discoveryNearbyGame success');
        4.   }).catch((err: BusinessError) => {
        5.     hilog.error(0x0000, '[nearby]', '%{public}s', 'discoveryNearbyGame error' + (err as Error).message);
        6.   })
        7. } catch (err) {
        8.   hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
        9. }
        
    3. “发现设备”操作完成后将收到discovery事件回调，获得发现的设备列表供玩家选择，调用[bindNearbyGame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section13279659901)接口绑定玩家选定的接收端设备。
        
        1. public bindNearbyGame(deviceInfo: gameNearbyTransfer.NearbyGameDevice) {
        2.   try {
        3.     let bindInfo: gameNearbyTransfer.BindParameters = {
        4.       deviceId: deviceInfo.deviceId,
        5.       networkId: deviceInfo.networkId
        6.     };
        7.     gameNearbyTransfer.bindNearbyGame(bindInfo).then(() => {
        8.       hilog.info(0x0000, '[nearby]', '%{public}s', 'bindNearbyGame success');
        9.     }).catch((err: BusinessError) => {
        10.       hilog.error(0x0000, '[nearby]', '%{public}s', 'bindNearbyGame error' + (err as Error).message);
        11.     })
        12.   } catch (err) {
        13.     hilog.error(0x0000, '[nearby]', '%{public}s', 'bindNearbyGame error' + (err as Error).message);
        14.   }
        15. }
        

### 接收端发送自身文件信息

收到建链成功回调后，接收端调用[sendPackageInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section12490112992612)接口发送自身文件，如版本信息、包信息。

1. function connectNotifyCallBack(callback: gameNearbyTransfer.ConnectNotification) {
2.   if (callback.connectState == gameNearbyTransfer.ConnectState.CONNECTED) {
3.     // 连接成功回调，判断当前是否为接收端。若当前设备为接收端，请设置为true，否则请设置为false。
4.     let isReceive = true;
5.     if (!isReceive) {
6.       return;
7.     }
8.     // 接收端收到连接回调后需要处理,发送资源包信息给发送端
9.     let packageInfo: gameNearbyTransfer.PackageInfo = {
10.       name: 'com.huawei.xxxx',
11.       files: [],
12.       version: '1.1.0',
13.       extraData: 'extraData'
14.     };
15.     let fileInfo: gameNearbyTransfer.FileInfo = {
16.       path: "/xxx/xxxx/files/data.zip",  // 使用沙箱路径，详情请参见[应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)。
17.       hash: 'fileHash' // 可选
18.     };
19.     packageInfo.files?.push(fileInfo);
20.     try {
21.       gameNearbyTransfer.sendPackageInfo(packageInfo).then(() => {
22.         hilog.info(0x0000, '[nearby]', '%{public}s', 'sendPackageInfo success');
23.       }).catch((err: BusinessError) => {
24.         hilog.error(0x0000, '[nearby]', '%{public}s', 'sendPackageInfo error' + (err as Error).message);
25.       });
26.     } catch (err) {
27.       hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
28.     }
29.   }
30. }

### 发送端对比后传输资源包

发送端收到接收端发送的版本信息后进行对比，调用[replyPackageInfoResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section78288285293)上报对比结果，根据对比结果决定是否需要调用[transferPackageData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section1227711101118)接口发送资源包数据。

1. function receivePackageInfoCallBack(callback: gameNearbyTransfer.PackageInfo) {
2.   // 比较版本,决定是否需要发送资源包,也可以比较文件hash
3.   let packageInfoResult: gameNearbyTransfer.PackageInfoResult = {
4.     packageInfoResultCode: gameNearbyTransfer.PackageInfoResultCode.PACKAGE_AVAILABLE_COMPARED
5.   };
6.   try {
7.     // 上报对比结果
8.     gameNearbyTransfer.replyPackageInfoResult(packageInfoResult).then(() => {
9.       let packageData: gameNearbyTransfer.PackageData = {
10.         name: 'com.huawei.gamenearbydemo',
11.         version: '1.0.0',
12.         files: [{
13.           srcPath: '/data/xxxx/a.zip', // srcPath是需要发送文件的沙箱路径，详情请参见[应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)。
14.           destPath: 'xxxx/a.zip'       // destPath是接收文件的自定义路径，完整的沙箱路径是[fileStoragePath](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section116223815415)+destPath，详情请参见[应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)。
15.         }] 
16.       }
17.       try {
18.         // 发送资源包
19.         gameNearbyTransfer.transferPackageData(packageData).then(() => {
20.           // 发送成功
21.         }).catch((err: BusinessError) => {
22.           // 发送异常
23.           hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);          
24.         });
25.       } catch (err) {
26.         hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
27.       }
28.     }).catch((err: BusinessError) => {
29.       // 上报异常
30.       hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
31.     });
32.   } catch (err) {
33.     hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
34.   }
35. }

### 处理资源包传输进度信息

发送端和接收端在传输回调中处理传输进度信息。

1. function transferNotifyCallBack(callback: gameNearbyTransfer.TransferNotification) {
2.   if (callback.transferState == gameNearbyTransfer.TransferState.SEND_PROCESS) {
3.     // 处理发送进度,如显示进度条和速率
4.   }
5.   if (callback.transferState == gameNearbyTransfer.TransferState.SEND_FINISH) {
6.     // 发送完成
7.   }
8.   if (callback.transferState == gameNearbyTransfer.TransferState.RECEIVE_PROCESS) {
9.     // 处理接收进度,如显示进度条和速率
10.   }
11.   if (callback.transferState == gameNearbyTransfer.TransferState.RECEIVE_FINISH) {
12.     // 接收完成,获取到资源包存储的沙箱路径
13.     let fileStoragePath = callback.fileStoragePath;
14.     // 对fileStoragePath下的文件做处理
15.   }
16. }

### 处理已接收资源包后销毁服务

对已接收数据做好处理或转移后，调用[destroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-nearbytransfer#section13373155416)接口销毁服务。若服务销毁后再次使用近场快传服务，需重新[创建游戏近场快传服务并注册相关回调](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-nearbytransfer-access-procedure#section8810153223912)。

1. public destroy() {
2.   // 取消回调注册
3.   this.unregisterCallback();
4.   // 销毁服务
5.   try {
6.     gameNearbyTransfer.destroy().then(() => {
7.       hilog.info(0x0000, '[nearby]', '%{public}s', 'destroy success');
8.     }).catch((err: Error) => {
9.       hilog.error(0x0000, '[nearby]', '%{public}s', 'destroy error' + (err as Error).message);
10.     });
11.   } catch (err) {
12.     hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
13.   }
14. }

15. public unregisterCallback() {
16.   try {
17.     gameNearbyTransfer.off('connectNotify', connectNotifyCallBack);
18.     gameNearbyTransfer.off('receivePackageInfo', receivePackageInfoCallBack);
19.     gameNearbyTransfer.off('transferNotify', transferNotifyCallBack);
20.     gameNearbyTransfer.off('error', errorCallBack);
21.     // 发送端选择手动绑定接收端且已订阅discovery事件
22.     gameNearbyTransfer.off('discovery', discoveryCallBack);
23.   } catch (err) {
24.     hilog.error(0x0000, '[nearby]', '%{public}s', 'error' + (err as Error).message);
25.   }
26. }

27. function connectNotifyCallBack(callback: gameNearbyTransfer.ConnectNotification) {
28.   // 连接状态回调，接收端收到建链成功回调后，在此处调用sendPackageInfo接口发送自身文件信息，如版本信息、包信息
29. }

30. function receivePackageInfoCallBack(callback: gameNearbyTransfer.PackageInfo) {
31.   // 接收包信息回调，发送端收到接收端发送的版本信息后进行对比，根据对比结果决定是否需要传输资源包数据。
32. }

33. function transferNotifyCallBack(callback: gameNearbyTransfer.TransferNotification) {
34.   // 传输回调，处理传输进度信息
35. }

36. function errorCallBack(callback: gameNearbyTransfer.ReturnResult) {
37.   // 异常信息回调，处理相关异常信息
38. }

39. function discoveryCallBack(callback: gameNearbyTransfer.DiscoveryResult) {
40.   // 获取到发现的设备 展示设备列表
41.   callback.nearbyGameDevices.forEach((device: gameNearbyTransfer.NearbyGameDevice, index: number) => {
42.   });
43. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-nearbytransfer-config-agc "开发准备")
# 若游戏无HarmonyOS 4及以下系统包时，是否可以不配置APP ID映射关系？

更新时间: 2025-12-16 16:37

不可以。

在[配置APP ID映射关系](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-huawei#section3907114313255)时，请先创建草稿态的HarmonyOS 4及以下游戏，再与HarmonyOS 5.0及以上游戏进行关联。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-faq-unlogin "基础游戏服务")
# 游戏官方账号图标大小是多少？

更新时间: 2025-12-16 16:38

游戏官方账号ICON大小总和不超过35KB。若超过35KB，调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口时，会出现[1002000001](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-error-code#section132125911468)错误码。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-faq-1 "若游戏无HarmonyOS 4及以下系统包时，是否可以不配置APP ID映射关系？")
# 游戏如何实现不展示官方账号登录？

更新时间: 2025-12-16 16:38

在游戏调用[unionLogin](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-gameplayer#section157848375136)接口时，将thirdAccountInfos参数传空数组，即可实现玩家登录游戏时不展示“游戏官方账号登录”选项，默认使用华为账号登录。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-faq-2 "游戏官方账号图标大小是多少？")
# 玩家选错登录账号后如何处理？

更新时间: 2025-12-16 16:38

玩家点击游戏内的“切换账号”按钮拉起联合登录面板，支持玩家重新选择华为账号登录或游戏官方账号登录。开发者在游戏内提供切换账号功能的开发步骤请参见[游戏内切换账号](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-gameplayer-official#section26517112362)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-faq-3 "游戏如何实现不展示官方账号登录？")
# 使用C#语言开发的游戏是否可以接入游戏场景感知功能？

更新时间: 2025-12-16 16:37

当前提供游戏场景感知C# SDK，可以实现使用C#语言开发的游戏接入游戏场景感知功能，具体请参见[游戏场景感知C# SDK开发指导](https://gitee.com/petal-gaming-services/HarmonyAdaptivePerformanceForUnity/blob/main/%E6%B8%B8%E6%88%8F%E5%9C%BA%E6%99%AF%E6%84%9F%E7%9F%A5C-SDK%E5%BC%80%E5%8F%91%E6%8C%87%E5%AF%BC.md)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-faq-performance "游戏场景感知")# 配置回调地址

更新时间: 2025-12-16 16:36

若在关键事件发生时，华为游戏服务器向开发者服务器发送事件通知，请前往AppGallery Connect配置开发者服务器的回调地址。发送通知的接口原型等信息请参见[解绑账号通知](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/gameservice-unbindplayer-notification)接口。涉及的关键事件及对应的处理逻辑如下：

|关键事件|游戏自行实现的处理逻辑|
|:--|:--|
|玩家注销华为账号。|清理账号数据。|

在AppGallery Connect配置服务器的回调地址步骤如下：

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，在“开发与服务”下选择项目及项目下的游戏。
2. 左侧菜单选择“构建 > 游戏服务”，在“账号方案接入回调地址配置”配置开发者服务器地址，用于华为游戏服务器在发生关键事件时向该地址发送事件通知。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163632.55762365070307887433286737231508:50001231000000:2800:70B49700C077D69F6735560DA7C5062606A4F9BD6DA0EE766F4AAC9AB29B3A6A.png)
    
    说明
    
    回调地址要求支持HTTPS协议，且具有合法商用证书。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-appendix "附录")
# 获取游戏密钥

更新时间: 2025-12-16 16:36

在开发者服务器加签或验签时，请开发者前往AppGallery Connect获取游戏私钥或游戏公钥。

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，在“开发与服务”下选择项目及项目下的游戏。
2. 选择“构建 > 游戏服务”，记录下游戏密钥信息。若需要刷新密钥信息，请通过[在线提单](https://developer.huawei.com/consumer/cn/support/feedback/#/add/101704353566310877?level2=101704353626565886&level3=101704354579010004&keyWord=Game%20Service%20Kit)方式联系华为工作人员。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163646.17885499430210140611313995526457:50001231000000:2800:97A77D9CBA5DEF3B1C94C3FF260D7126B030ECAFCE96D8932656EF20864E6380.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/gameservice-address "配置回调地址")