# Cloud Foundation Kit简介

更新时间: 2025-12-16 16:35

Cloud Foundation Kit（云开发服务）可以按需为应用提供云函数、云数据库、云存储、预加载等云端服务。应用运行所需的服务器和环境可以皆由云端平台提供，开发者只需关注应用的业务逻辑，而无需关心基础设施（例如：服务器、操作系统、容器等）。

DevEco Studio中还提供了[端云一体化开发](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddevguide)的开发体验，开发者可以基于统一的技术栈，高效、协同地完成端、云代码的编写、调试、编译和部署，极大提高构建HarmonyOS应用和元服务的效率。

## 优势

- 低运维成本
    
    开发者无需构建和管理云端资源，Cloud Foundation Kit提供了包括函数计算、数据库、存储、预加载等一系列能力。
    
- 弹性伸缩、按量计费
    
    面对波峰波谷的业务场景，Cloud Foundation Kit可根据实际请求量弹性伸缩、按量计费，开发者无需为空闲资源买单，有效提升资源利用率，降低资源成本。
    
- 安全可靠
    
    支持数据全密态加密，支持APP、用户和服务三重认证，提供基于角色的权限管理机制，全方位保障开发者和用户的数据安全。
    
- 端云一体化开发
    
    在DevEco Studio中提供了端云一体化开发体验，支持开发者基于统一的技术栈进行端、云代码协同开发，前端开发人员轻松转换为全栈工程师，极大提高构建HarmonyOS应用和元服务的效率、降低开发成本。
    

## 典型场景

### 应用/元服务后端构建

便捷操作云函数、云数据库、云存储、预加载服务，简化应用/元服务开发与运维相关的事务，快速构建应用/元服务的后端服务。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163556.83724663920602251870226472986745:50001231000000:2800:72637946548BB99F3BEFAA20ADA7BE7626462E72D71DEBD5761602CFF04256DA.jpg "点击放大")

### 计算密集型任务

当应用中出现计算密集型任务时，可在任务启动时自动分配足够的算力来支撑任务的执行，并在任务结束时自动释放资源，避免浪费。

开发者可以为云函数配置定时触发器，定时执行任务，也可以通过其他服务主动调用云函数来执行任务。

例如，通过Cloud Foundation Kit实现对数据的渲染、叠加等处理：

- 对原始数据进行封装，例如对报表数据的处理。
- 对数据的同步，例如数据的抽取、转化或者加载。
- 对视频或者图像的处理，例如生成不同分辨率的视频或者图片。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163556.22252686134525558575973863415028:50001231000000:2800:9C9EB256A56C303576B0F1DBEED7973DDCB4007F8D3EAE1282271E1016FAB953.png "点击放大")

### 协议适配和转换场景

可用于协议适配和转换，以及第三方平台场景的对接，轻量灵活、快速部署，让开发者的业务快人一步。

例如：可以将数据存储、身份验证、消息队列、推送通知、定时任务等功能切片通过云服务实现胶水层的链接、转换。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163556.63862579777762975594688797410638:50001231000000:2800:126CD61D3A5E666F38742BD291CE14E74CB5EB4D5A153E54D14285DDEC00FA96.jpg "点击放大")

### 浪涌式访问场景

传统架构服务在某些特殊场景下，可能出现大量的访问。为保证业务高峰时，系统能稳定运行，一般需要购买高性能、昂贵的服务器，组建集群负载均衡。但是，当业务回落时，就导致了大量服务器的资源浪费。

Cloud Foundation Kit能根据业务访问量快速自动扩容，规避业务高峰时系统异常的风险，度过业务流量高峰期，使应用从容应对诸如秒杀、节日活动等业务场景；并发量骤降时，弹性伸缩的特性亦支持自动缩容，释放闲置资源，避免浪费。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163557.69726313071711868282740742326711:50001231000000:2800:3EA3CFD9E1CAA01D0EE33FC7799AA3EC2E01668EAEB3F8F36454F1309093E182.jpg "点击放大")

## 约束与限制

### 支持的设备

|能力|设备|
|:--|:--|
|云函数|Phone、Tablet、Wearable、TV|
|云数据库|
|云存储|
|预加载|Phone、Tablet|

### 支持的国家/地区

|能力|国家/地区|
|:--|:--|
|云函数|请参见[支持的国家/地区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-supported-regions)。|
|云数据库|
|云存储|
|预加载|

### 支持的签名方式

当前仅支持[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。

## 模拟器支持情况

从6.0.0(20) Beta5版本开始，本Kit支持模拟器开发，但与真机存在部分能力差异，详情请参见“[模拟器与真机的差异](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-specification#section38231424133213)”。

关于如何使用模拟器调试，请参见[使用模拟器调试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-emulator)。

## 计费说明

Cloud Foundation Kit包含云函数、云数据库、云存储、预加载服务，预加载服务支持通过云函数来实现资源加载，云函数、云数据库、云存储服务提供了免费额度以供试用，具体的配额明细请参考各服务的配额说明：

- [云函数计费说明](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-cloud-function-price-0000001211271102)
- [云数据库计费说明](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-clouddb-price-0000001256815629)
- [云存储计费说明](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-cloudstorage-price-0000001253665999)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloud-foundation-kit-guide "Cloud Foundation Kit（云开发服务）")
# 开通云函数服务

更新时间: 2025-12-16 16:36

首次使用云函数服务前，需要先开通此服务。如果已经启用，可跳过本步骤。

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，点击“开发与服务”。
2. 在项目列表中点击需要开通云函数的项目。
    
3. 在左侧导航栏选择“云开发（Serverless）> 云函数”，进入云函数页面，点击“立即开通”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163645.90760892683656597728150400771964:50001231000000:2800:810DABE45C3C3DCF3561464231E5C2FEF6605030BAFB530A5900B74FD6405A71.png)
    
    说明
    
    如果开发者此时未设置数据处理位置，系统会自动弹出提示框提示开发者进行设置。目前，云函数支持启用多个数据处理位置，具体请参见[设置数据处理位置](https://developer.huawei.com/consumer/cn/doc/app/agc-help-data-location-0000002277923065#section154810363471)。
    
4. 如果开发者已启用多个数据处理位置，当需要在不同的数据处理位置管理云函数时，可在云函数页面选择“数据处理位置”下拉选项进行切换。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163646.47810137527386396355862135422652:50001231000000:2800:89BD4054EBC4C75754AEF5E2C83CDF8FB9EC898C9D672360DB01DFC3965AA765.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-basic-preparation "基本准备工作")
# 开通云数据库服务

更新时间: 2025-12-16 16:36

首次使用云数据库服务前，需要先开通此服务。如果已经开通，可跳过本步骤。

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，点击“开发与服务”。
2. 在项目列表中点击需要开通云数据库的项目。
3. 在左侧导航栏选择“云开发（Serverless）> 云数据库”，进入云数据库页面，点击“立即开通”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163657.42331740097363342012920124102016:50001231000000:2800:95EE3C6FAED8A0A9F26DEDECB6D70C1B4407D58892C203A6BE4142E8D418F34D.png)
    
    说明
    
    如果开发者此时未设置数据处理位置，系统会自动弹出提示框提示开发者进行设置，具体请参见[设置数据处理位置](https://developer.huawei.com/consumer/cn/doc/app/agc-help-data-location-0000002277923065#section154810363471)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-enable-function "开通云函数服务")
# 开通云存储服务

更新时间: 2025-12-16 16:37

首次使用云存储服务前，需要先开通此服务。如果已经开通，可跳过本步骤。

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，点击“开发与服务”。
2. 在项目列表中点击需要开通云存储的项目。
3. 选择“云开发（Serverless） > 云存储”，进入云存储页面，点击“立即开通”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163708.35224029145494491101054837006308:50001231000000:2800:C3ACE8C8E3B113F8B9C4CCA91C04770AC8EF35DDE8DC3894F6170D9F087F60AD.png)
    
4. 在引导界面输入存储实例名称并设置默认数据处理位置。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163708.20680895400127417758044541569493:50001231000000:2800:AB390B89F88E8AFE8709C2CEBAA628CB7B60E8939F48A23777B1DB26EDBC0B0C.png)
    
    |参数|说明|
    |:--|:--|
    |存储实例|存储实例名称必须符合以下条件：<br><br>- 只能包含英文小写字母、数字、中划线（-）。<br>- 只能以数字或字母开头和结尾。<br>- 要求不少于3个字符，并且不能超过57个字符。<br>- 不能为IP地址。<br>- 不能包含连续两个及以上中划线（-）。<br>- 名称全局唯一，创建后，不能修改。|
    |默认数据处理位置|云存储支持启用多个数据处理位置，具体请参见[设置数据处理位置](https://developer.huawei.com/consumer/cn/doc/app/agc-help-data-location-0000002277923065#section154810363471)。如当前项目已设置数据处理位置，则此处无需再设置。|
    
5. 点击“下一步”，进入默认安全策略展示界面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163708.69101840220406599381472605500241:50001231000000:2800:3EBC4927753BE9210476D068D579F107CE623C1589AA4A2CAB68C11BE21C029A.png)
    
    说明
    
    默认安全策略将允许经过身份验证的用户执行所有读写操作，开通服务时无法修改安全策略。服务开通后，开发者可制定更合适的安全策略来保护其用户数据。关于如何修改安全策略，请参见[安全规则](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-cloudstorage-securityrules-overview-0000001054966859)。
    
6. 点击“完成”，开通云存储成功。
    
    服务开通成功后，AGC将为开发者创建一个默认存储实例，默认存储实例的名称即为步骤[4](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-enable-storage#zh-cn_topic_0000001275330014_li191317012303)中配置的存储实例名称+“-五位随机数字字母”的组合，如“bucket001-2wezr”。
    
7. 如果开发者已启用多个数据处理位置，当需要在不同的数据处理位置管理云存储时，可在云存储页面选择“数据处理位置”下拉选项进行切换。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163709.60538886662300433607153446880390:50001231000000:2800:B35FEC270F05DED06799C5E134D7DC61C50B2CA549D75C744E8EE64C428B26EE.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-enable-database "开通云数据库服务")
# 开通预加载服务

更新时间: 2025-12-16 16:37

首次使用预加载服务前，需要先开通此服务。如果已经开通，可跳过本步骤。

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，点击“开发与服务”。
2. 在项目列表中点击您的项目，在项目下的应用列表中选择需要开通预加载的HarmonyOS应用/元服务。
    
3. 在左侧导航栏选择“云开发（Serverless）> 预加载”，进入预加载页面，点击“立即开通”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163730.94379866849107051789564614731138:50001231000000:2800:701E400C78B03D09DC973DE15FF1E8FA161BA9C59421342B8CE0228B9C5E71BA.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-enable-storage "开通云存储服务")
# Node.js

更新时间: 2025-12-16 16:38

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 入口方法

入口方法定义如下：

1. module.exports.myHandler = function(event, context, callback, logger)

- myHandler：入口方法名称。
- event：调用方传递的事件对象，JSON格式。具体内容请参见[event对象](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-cloudfunction-trigger-event-0000001620581529)。
- context：函数运行时上下文对象，封装了日志接口、回调接口、环境变量env对象等。
- callback：事件处理结果。
- logger：记录日志。

函数必须通过显式调用callback(object)将事件处理结果返回给AppGallery Connect（简称AGC），结果可以是任意对象，但必须与JSON.stringify兼容，AGC会将结果转换成JSON字符串后，返回给调用方。callback执行完成，函数即执行结束。

完整的Node.js 20.x云函数示例代码请参考[函数示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-develop-function-nodejs#section817193312817)。

## 日志记录

开发者可在代码中使用logger接口记录日志，后端已通过global.logger全局定义，目前支持四种级别：

- logger.debug()
- logger.error()
- logger.warn()
- logger.info()

## 获取环境变量

开发者可在代码中使用context.env.key访问环境变量，获取环境变量env1示例如下：

1. let env1 = context.env.env1;

若环境变量未配置，则会返回环境变量为undefined。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163810.81676637822220145803447656891921:50001231000000:2800:68E430F8E885E16E73D2BD0F0E276E279B18B93FE9B302F50F22EA4F4EA2651F.png)

## 异常处理

开发者可以在函数代码中捕获异常，封装成error对象返回给调用方。对于函数执行期间被平台捕获的异常，平台同样以error对象形式返回给调用方。error对象定义如下。

1. let error = {
2.     code: xxxxxx,
3.     message: "xxxxxxxx"
4. };

其中code为错误码，message为错误码的描述信息。

示例代码如下：

1. try {
2.     logger.info(JSON.stringify(event));
3.     let result = { message: "success" };
4.     callback(result);
5. } catch (err) {
6.     let error = {
7.         code: 400,
8.         message: err.message
9.     };
10.     callback(error);
11. }

## 函数示例

示例函数如下：

说明

示例代码中入口方法**myHandler()**的返回值类型仅供参考，开发者可以根据实际需要定义。

1. /**
2.  * Describe the basic method of Cloud Functions
3.  */

4. let myHandler = function (event, context, callback, logger) {
5.   // example of display environment variables
6.   let env1 = context.env.env1;

7.   // example of display logs
8.   logger.info("Test info log");
9.   logger.warn("Test warn log");
10.   logger.debug("Test debug log");
11.   logger.error("Test error log");

12.   logger.info("--------Start-------");
13.   try {
14.     let startTime = new Date().getTime();
15.     let endTime = startTime;
16.     let interval = 0;
17.     startTime = process.uptime() * 1000;

18.     // print input parameters and environment variables
19.     logger.info("request: " + JSON.stringify(event.request));
20.     logger.info("env1: " + env1);

21.     endTime = process.uptime() * 1000;
22.     interval = endTime - startTime;
23.     logger.info("intervalTime: " + interval);
24.     logger.info("--------Finished-------");

25.     let res = new context.HTTPResponse(context.env, {
26.       "res-type": "context.env",
27.       "faas-content-type": "json"
28.     }, "application/json", "200");
29.     res.body = { "intervalTime": interval };
30.     callback(res);
31.   } catch (error) {
32.     logger.error("--------Error-------");
33.     logger.error("error: " + error);
34.     callback(error);
35.   }
36. };

37. module.exports.myHandler = myHandler;

## 准备函数部署包

上传的nodejs函数部署包须使用如下结构，处理程序所在代码文件，例如示例中的handler.js，必须在zip包根目录下，依赖项放到node_modules目录下。

1. my-function.zip
2.   |---- handler.js
3.   |---- node_modules
4.     |----async
5.     |----async-listener

可通过npm工具的相关命令，安装与管理依赖。例如npm install xxx命令（执行路径无限制）可将依赖xxx自动安装到根目录的node_modules文件夹下。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163810.06087162547432657009063707340587:50001231000000:2800:68B8C78CA237A00978EEB876132CE5ACD306F2201648A41814EE016F3B24B97E.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-develop-function "开发函数")
# 创建函数

更新时间: 2025-12-16 16:37

## 创建函数

开通云函数服务后，首先需要在AGC中创建函数，并添加函数执行的代码。

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，点击“开发与服务”。
2. 在项目列表中点击需要创建云函数的项目。
3. 在左侧导航栏选择“云开发（Serverless） > 云函数”，进入云函数主界面。
4. 选择“函数”页签，点击“创建函数”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.77775925616284883127780255427519:50001231000000:2800:EB9B830B19FBC4F38858D74852821D0BB6CBAB605E012EF8397195A9FA330632.png)
    
5. 页面右侧抽屉式滑出“创建函数”窗口，按照“函数配置 -> 触发器 -> 函数代码 -> 层配置”引导顺序配置函数。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.68551072418499940367857895044024:50001231000000:2800:946272D4C673AB01F283466C163372FA4EC538C4F9168DB9B0D3FCEE46FF41BB.png)
    

## 函数配置

1. 在“函数配置”页面，配置“函数名称”、“触发方式”、“超时时长”等函数信息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.89773623877474115247209726723324:50001231000000:2800:663C0963AC09BA67C7DA22D0195494013AB96AFE1AB506026748DC9BC72D44AC.png)
    
    |配置项|**说明**|
    |:--|:--|
    |函数名称|函数的名称。|
    |描述|函数的描述信息。|
    |触发方式|**请配置为“事件调用”。**<br><br>“事件调用”表示通过触发器方式调用函数。|
    |超时时长|函数最大运行时长，超过该时长，则默认函数执行失败，单位为秒，取值范围为1~1800。不同调用方式下，函数最大运行时长不同：<br><br>- “同步”调用方式时，函数最大运行时长为55秒。<br><br>- “异步”调用方式时，函数最大运行时长为1800秒。|
    |实例并发|函数请求并发量上限，单位为个，取值范围为1~10000。|
    |环境变量|key-value形式，可以将需要的变量配置信息传入函数执行环境中，用于函数在运行时读取和使用。|
    
2. （可选）可根据需要添加环境变量，支持**表单格式**和**JSON格式**两种编辑方式。添加完成后，还可以点击“JSON格式导出”，导出以“函数名称.json”格式命名的环境变量文件，以备后续使用。
    
    说明
    
    - 环境变量的key值具有唯一性，且“PROJECT_CREDENTIAL”和“AGC_”为系统级环境变量标识，不允许添加以其命名或以其为前缀的环境变量。
    - 环境变量总数不超过1000个。
    
    - 表单格式编辑
        
        点击“新增变量”，输入key和value值，如下图中所示，env1为环境变量的key值，test为value值。点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.57162155166574900386636546127442:50001231000000:2800:A7426455147CA7E26B49B6F5FB61EA4AE97C46F07CB3D37261A0B08BEB95E5FA.png)可将变量删除。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.56667271142750128540832031672447:50001231000000:2800:BB6CBACB2BCEF745947A3152C484F99014370470A218316B1563D486635CF612.png)
        
    - JSON格式编辑
        
        选中“JSON格式编辑”，在文本框中以key-value键值对JSON格式添加环境变量。当添加的环境变量比较多时，为了方便核对，可点击“format”对变量进行格式化排列。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.54405867801030691930183630113521:50001231000000:2800:1A66B6668EB52873570B13F5A234B54A2C98D67E21A8D692EEDA494D2F34DD9F.png)
        
3. “函数配置”页面配置完成后点击“下一步”。

## 触发器

进入“触发器”页面，可基于函数触发场景配置需要的触发器，本场景下添加HTTP触发器。“触发器类型”和“请求方式”保持默认选择，并配置“认证类型”，配置完成后点击“下一步”。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.90161317130195468306581728625157:50001231000000:2800:C709D4494D6430A1B2276A08C2994F5E6D572B1DA0110DA132B1E13004C280EE.png)

|参数|说明|
|:--|:--|
|触发器类型|HTTP触发器。|
|请求方式|HTTP触发器目前仅支持POST请求方式。|
|认证类型|HTTP触发器的认证类型。<br><br>- API客户端鉴权（Client适用）：端侧网关认证，适用于来自APP客户端侧（即本地应用或者项目）的函数调用。<br>- API客户端鉴权（Server适用）：云侧网关认证，适用于来自APP服务器侧（即云函数）的函数调用。|
|启用decode|通过HTTP触发器触发函数时，对于contentType为“application/x-www-form-urlencoded”的触发请求，是否使用URLDecoder对请求body进行解码再传入到函数中。|

## 函数代码

进入“函数代码”页面，配置“运行环境”、“内存配置”、“代码输入类型”等信息，配置完成后点击“下一步”。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.19497443035968666722348889099253:50001231000000:2800:0873858829951E612834BAC314268B5AD9D14AB3D4E5F0C146346A3A2CC08B40.png)

|配置项|**说明**|
|:--|:--|
|运行环境|函数容器的运行环境。请选择nodejs 20.x/latest，其中latest表示使用最新版本。|
|内存配置|函数容器所占有的内存大小，单位为MB，取值范围：500，1000，2000，4000。|
|代码输入类型|包括“在线编辑”与“*.zip文件”两种方式，默认值为“在线编辑”。<br><br>选择“*.zip文件”方式部署云函数时，入口方法文件的编写方法请参见[入口方法](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-develop-function-nodejs#section69815160394)。|
|函数入口|包括入口文件名称和入口方法名称，通过“.”连接。例如handler.myHandler，其中handler为入口文件名称，myHandler为入口方法名称。<br><br>nodejs运行环境下入口文件必须放置在函数部署包的根目录下，具体请参见[准备函数部署包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-develop-function-nodejs#section527564201715)。|
|代码文件|用于在线编辑函数代码或上传函数部署包。<br><br>- “代码输入类型”配置项选择“在线编辑”时，可在创建函数界面集成的WebIDE区域在线编辑函数代码。WebIDE的详细使用方法见下文。<br>- “代码输入类型”配置项选择“*.zip文件”时，点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.05267492152801664091826482538818:50001231000000:2800:1EE516344A69CDDF59F9292C8E7A8B18708E0D400E235F1FC3AC90D2B6D8460B.png)即可上传函数部署包，也可直接拖曳zip文件至虚线框内。|

**WebIDE**

当“代码输入类型”配置项选择“在线编辑”时，创建函数界面中集成了WebIDE功能，支持在线编辑函数代码。

注意

如果在函数实例已经运行的情况下进行函数代码或配置更新，AGC后台会滚动更新函数实例，请耐心等待10-20秒。

WebIDE从左至右分两个部分：目录树、代码编辑器和最大化，如下图所示。编辑完成后平台会生成部署包并上传。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.89495048115263932734578353848997:50001231000000:2800:852A3C25E7D7200D2E8CED86C0AC06C1062BF2DC189CBF4D5E91619B91582350.png)

|组成|说明|
|:--|:--|
|目录树|目录树支持如下能力：<br><br>- 新增文件夹：选中一个文件或文件夹，点击右上角新增文件夹按钮“![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.43391454597827420227919972245561:50001231000000:2800:08C4513B123FA436DF6034196B46DD6DCE96F59D210E0110A9FE27FAC2648926.png)”。若选中的是文件夹，则新增一个子文件夹。若选中的是文件，则新增一个同级文件夹。<br>- 新增文件：选中一个文件或文件夹，点击右上角新增文件按钮“![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.07415459252905278752428219012353:50001231000000:2800:E9A01363E60072FDDFF5C52773F3A1F6769C68B91F326452DE19B6B20ADF2405.png)”。若选中的是文件夹，则新增一个子文件。若选中的是文件，则新增一个同级文件。<br>- 删除文件：选中一个文件或文件夹，点击右侧删除按钮“![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.85612518804548022417277475991846:50001231000000:2800:FC69E21731A0824E1C60E3A191DCC10CCC0B2309D4B5753E7098C36508F795C8.png)”，删除文件或文件夹。不允许删除根目录。<br>- 重命名：双击文件或文件夹，输入新命名（仅支持字母、数字、下划线和中划线），完毕后按Enter键完成重命名。|
|编辑器|编辑器具有如下能力：<br><br>- 语法高亮：按照node.js语法高亮显示代码。<br>- 语法校验：语法有错误时会给出错误提示。<br>- 代码提示：输出代码自动给出相关代码提示。<br>- 代码填充：选择后系统代码可自动填充。<br>- 格式化：快捷键Ctrl+Shift+B。<br>- 支持快捷键操作：Ctrl+v, Ctrl+c, Ctrl+z, Ctrl+x, Ctrl+f, Ctrl+/等。|
|最大化|点击最大化按钮![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.12512930995705702991580910696490:50001231000000:2800:5E4CA4B363E9A11A147FDEE7782E1DB47B89A41CC9A1AA7E947C19AFFEC12FAF.png)，可以最大化在线编辑区，再次点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.48770863112301042931828811697411:50001231000000:2800:10B1AEC832D4F1253A42F057ABC5B66355934056D4424ADE50414424E8BE26C9.png)按钮或按ESC键退出最大化。|

## 层配置

层可以提供公共依赖库的发布与部署能力。开发者可以将函数依赖的公共库和相关依赖项提炼到层，通过为函数绑定层，便可以在函数中使用库，而不必将库包含在函数的代码包中，从而达到缩小函数代码包体积与缩短函数部署时间的效果，也避免了使用函数代码安装和打包依赖项时可能出现的错误。详细的层管理功能，请参见[层管理](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-cloud-function-layer-0000001517762624)。

如果尚未创建层，可跳过下述步骤，直接点击页面底部的“创建”完成函数定义，后续创建层之后可在函数详情页再进行层配置，为函数绑定层。如果在创建函数之前已创建层，可按照下述步骤进行操作。

1. 进入“层配置”页面，点击“绑定层”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163758.80943816115312057350736304395534:50001231000000:2800:1272C12020FDB6DC12654734D24C385445195A846F3177044631DDCD49BA83A7.png)
    
2. 在右侧弹出的“绑定层”界面中，下拉框选择“层名称”和“版本”，“层范围”等信息根据层的配置将被自动填充，完成层绑定后点击“确定”。一个函数最多可以绑定5个层。
    
    说明
    
    选择层时，层的兼容运行时需与函数运行环境相符，系统会自动完成过滤。如果无匹配的层，请参考[创建层](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-cloud-function-layer-0000001517762624#section11358162018572)创建相同运行环境的层后再进行绑定。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163759.65460288873529812589592437051905:50001231000000:2800:828E5094B6FA028B7CE61446EB2B8261EC72D541367D33331A44995BC5DBEC7A.png)
    
    |参数|说明|
    |:--|:--|
    |层名称|层的名称。重复时自动在同名的层中创建一个新版本。|
    |版本|存在多个层版本时，选择函数绑定的层版本。|
    |层范围|层的共享范围。<br><br>- 项目内共享<br>- 团队内共享|
    |兼容运行时|层使用的语言环境。请选择“nodejs”。|
    |层描述|层的附加说明，长度不超过1024位。|
    
3. 返回到“层配置”界面，绑定成功的层将展示在层列表中。如果需要解除层与函数的绑定关系，点击“解绑”即可。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163759.93798611682349404650486027043501:50001231000000:2800:82E0DD74E7F7ABF2DD14C5580C271C114FEDD61FF4E010437F800B7513DF0989.png)
    
4. 按照“函数配置 -> 触发器 -> 函数代码 -> 层配置”顺序配置过程中，如果需要修改前面步骤中的配置，可点击“上一步”进行回退，配置完成后点击“创建”提交函数定义。

## 更多信息

函数配置完成后，可以[修改函数高级配置](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/modify-function-advanced-config-0000001734287937)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-develop-function-nodejs "Node.js")
# 测试函数

更新时间: 2025-12-16 16:38

说明

下文以函数latest版本为例介绍测试方法。如果需要测试函数的已发布版本，可在已发布版本详情页面选择“函数代码”页签，参考方式二进行测试。

函数创建后可以在AGC控制台测试函数的代码运行是否正常。进入测试界面有两种方式：

- 方式一：函数列表中点击函数名称右侧“操作”列的“测试”，在右侧弹出的“测试函数”界面进行测试。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163803.38082894185931533358802075538364:50001231000000:2800:D13A27E2035FE48A50B722348720A6A978D7DEC31594C6C48126DAF388A7EC91.png)
    
- 方式二：
    1. 在函数列表中点击已创建的函数名称，进入函数详情页面。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163803.60048132464220287776776767389249:50001231000000:2800:C738B891DC492B8B2A92E7314D2E9F5775603E65ADBBCC4C26F9F9C062094AAB.png)
        
    2. 选择“函数代码”页签，点击“测试函数”。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163803.89207899876370429598226371164562:50001231000000:2800:011A82A14693B4E63BD573DE638FE8053E28A40B569AD4163C54EFB020D6F6D0.png)
        
    3. 在右侧弹出的“测试函数”界面，使用默认测试事件、创建新测试事件或者使用已保存测试事件进行测试。
        - 使用默认测试事件
            
            直接点击“测试”对函数进行测试。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163803.79293264815675780028134082685559:50001231000000:2800:11E4C332376290B7B8F53F8A782E3D299DC36FF7CBCFD3CAB402F1BE589BCCDC.png)
            
        - 创建新测试事件
            
            如果需要设置调用函数的请求消息体，可按照如下步骤配置测试参数，并可保存为测试事件方便后续继续使用。
            
            1. 在“事件”文本框中输入JSON格式的事件参数，点击“保存”。然后在“提示”弹出框中输入事件名称，配置完成后点击弹出框右下角的“确认”。
                
                说明
                
                “事件”文本框内输入的JSON对象，对应的是触发器的event事件格式，会透传给函数。
                
                ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163803.04625948031927408195135036383423:50001231000000:2800:53A74A7363C65704BA6BAA198BB63ECB1E23194B48798D5FD7DE6C044990DFD6.png)
                
            2. 点击“测试”，函数处理事件并返回测试结果。
        - 使用已保存测试事件
            1. 在“测试函数”界面，点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163803.83169537638253814217545079511656:50001231000000:2800:CBA20701ABDF2AA4601C6FAA210FB67072BCF19DD07920682380D7D3E7A93B31.png)展开已保存的测试事件列表，选择已配置的事件名称右侧的“加载”，然后点击“测试”，函数处理事件并返回测试结果。
                
                ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163803.88910897103816327504136900411825:50001231000000:2800:6C12E260B9BE4ECF1051805A90B96A6C56ACCCE1BB716F16A4B2B12DB0045F2B.png)
                
            2. （可选）如果需要删除已添加的测试事件，可在测试事件列表中点击事件名称右侧的“删除”即可删除测试事件。
                
                ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163803.15329227537409297028601031375324:50001231000000:2800:DA24FD468A37AF437EF87F895098EAAA0D78D42AE3D8940CB7E4ED87289D47FB.png)
                
    4. 查看测试结果。
        - 执行结果：展示测试后获得的响应结果。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163804.32154581797944403429642555333140:50001231000000:2800:DD3E4FC1D61C0D3BA88977AA41E990EC64F4C41E76C19DE7C801AFDDAAEDAB90.png)
            
        - 运行日志：展示函数运行过程中，通过logger API打印的日志，支持输出debug级别及以上日志（以下仅为日志级别测试结果）。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163804.01254753607320642459727387566753:50001231000000:2800:4CFE39601CA594BE3B2A1FE13758155A3042E5B6C12ECA933400B9A27032C15A.png)
            
        - 执行摘要：展示该次测试请求相关信息。
            
            - 请求ID：该条测试请求的RequestID，在后台日志中体现为X-Trace-ID。
            - 持续时间：函数执行的端到端时间。
            - 执行版本：该次调用测试的具体函数版本。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163804.23845752744497459309166427700759:50001231000000:2800:71B1EC51B644A61331485E9C7D7871E39B031D797A80D3BD09BA24DE687DD21A.png)
            
    5. “代码输入类型”为“在线编辑”的函数，测试过程中，如果需要修改函数入口文件代码，可直接在“函数代码”页签的代码编辑器中修改，然后点击页面底部的“提交”。当界面提示更新函数成功时，则可以点击“测试函数”对更改后的代码进行测试。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163804.78687716583344040760838952773864:50001231000000:2800:2CD069C42F9FAB6F48D3C8695555E242CE4243E521DC470E3698B35774A17D7B.png)
        
        “代码输入类型”为“.zip文件”的函数，测试过程中，如果需要修改函数代码文件，可在本地修改且打包完成后，点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163804.36201977631809224135943061639616:50001231000000:2800:8890A417760A01377613A810634AA99B49BADF0F1C621C647E685BB977363DA2.png)重新上传函数部署包，然后点击页面底部的“提交”。当界面提示更新函数成功时，则可以点击“测试函数”对更改后的代码进行测试。
        
        说明
        
        如果代码更新量比较大，需要调整函数内存配置，可点击“内存配置”下拉框进行调整，然后再上传函数部署包。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163804.86300081878708369689960999601688:50001231000000:2800:6D538B0502EA69972C37DC1EA4020D326B96A4726F0389DB268538706C58C01F.png)
        
    6. 函数测试无误后，可在“函数代码”页签点击“导出函数”导出函数部署包。导出包以“函数名称+函数版本.zip”格式命名，可查看函数结构和文件内容。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-create-and-config-function "创建函数")
# 调用函数

更新时间: 2025-12-16 16:38

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 设置云函数配置项

在“entry/src/main/module.json5”文件中添加网络权限。

1. "requestPermissions": [
2.   {
3.     "name": "ohos.permission.INTERNET"
4.   }
5. ]

## 查询函数名和版本

在函数的触发器页面点击“HTTP触发器”，查看“触发URL”的后缀，获取触发器的标识，格式为“函数名-版本号”。如下图所示，“myhandlerxxxx-$latest”即为HTTP触发器标识，其中“myhandlerxxxx”为函数名，“$latest”为版本号。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163808.29225463733054356941991051734579:50001231000000:2800:76917A7B0DB31A71172E69EA967E8E8A2A153AC02DCFDD2C5E827178281DF115.png)

## 在应用中调用函数

1. 在项目中导入cloudFunction组件。
    
    1. import { cloudFunction } from '@kit.CloudFoundationKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    

2. 调用[call()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudfunction#section251833512544)方法设置函数，在方法中传入函数名称，返回调用结果。
    
    - （可选）通过设置timeout属性对云函数设置超时时长，单位为毫秒。
    - （可选）通过设置version属性对云函数设置函数版本号，默认为最新版本'$latest'。
    - （可选）如果函数有入参，可以将data参数转化为JSON对象或JSON字符串传入，如果没有参数则不传。
    
    使用Promise异步回调：
    
    1. import { hilog } from '@kit.PerformanceAnalysisKit';
    2. import { cloudFunction } from '@kit.CloudFoundationKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. function callFunction() {
    5.   cloudFunction.call({
    6.     name: 'functionName', // functionName需替换为实际的函数名
    7.     version: '$latest',   // 如果不传入版本号，默认为“$latest”。
    8.     timeout: 10 * 1000,   // 单位为毫秒，默认为70*1000毫秒。
    9.     data: {               // data为函数请求体
    10.       param1: 'val1', 
    11.       param2: 'val2'
    12.     }
    13.   }).then((value: cloudFunction.FunctionResult) => {
    14.     hilog.info(0x0000, 'testTag', `Succeeded in calling the function, result: ${JSON.stringify(value.result)}`);
    15.   }).catch((err: BusinessError) => {
    16.     hilog.error(0x0000, 'testTag', `Failed to call the function, code: ${err.code}, message: ${err.message}`);
    17.   })
    18. }
    
    或者，使用callback异步回调：
    
    19. import { hilog } from '@kit.PerformanceAnalysisKit';
    20. import { cloudFunction } from '@kit.CloudFoundationKit';
    21. import { BusinessError } from '@kit.BasicServicesKit';
    
    22. function callFunction() {
    23.   cloudFunction.call({
    24.     name: 'functionName', // functionName需替换成实际的函数名
    25.     version: '$latest',  // 如果不传入版本号，默认为“$latest”。
    26.     timeout: 10 * 1000,  // 单位为毫秒，默认为70*1000毫秒。
    27.     data: {              // data为函数请求体
    28.       param1: 'val1',
    29.       param2: 'val2'
    30.     }
    31.   }, (err: BusinessError, value: cloudFunction.FunctionResult) => {
    32.     if (err) {
    33.       hilog.error(0x0000, 'testTag', `Failed to call the function, code: ${err.code}, message: ${err.message}`);
    34.       return;
    35.     }
    36.     hilog.info(0x0000, 'testTag', `Succeeded in calling the function, result: ${JSON.stringify(value.result)}`);
    37.   })
    38. }
    

3. 如果需要关注函数的返回值，可调用result属性获取。
    
    1. let returnValue = value.result;
    
    value为步骤2中调用call()方法返回的cloudFunction.FunctionResult对象，返回值为云函数body返回的值，以[测试函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-test-function)时返回的结果为例，value.result = {"simple":"example"}。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-test-function "测试函数")
# 启动本地云函数

更新时间: 2025-12-16 16:37

请按照如下步骤启动本地云函数：

1. [创建端云一体化开发工程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-devproject)：选择合适的云开发模板，根据工程向导创建端云一体化开发工程。
2. [开发云函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-cloudfunctions)：使用DevEco Studio在端云一体化云侧工程下创建函数、开发函数、调试函数（通过本地调用方式调试函数）。
    
    调试函数过程中，如果下方通知栏的“cloudfunctions”窗口显示“Cloud Functions loaded successfully”，则表示本地云函数启动成功，将生成本地函数的Function URI。**请记录下该Function URI的域名和端口信息，例如下图中的“http://localhost:18090”，后续[调用本地云函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-call-local-function)时需要使用这些信息。**
    
    注意
    
    由于本地云函数和部署至云端的函数获取请求体的方式不同，开发函数时必须按照如下示例获取请求体：
    
    let body = event.body ? JSON.parse(event.body) : event;
    
    完整示例代码请参见[函数示例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-develop-function-nodejs#section817193312817)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163748.36578710508095627996172939553139:50001231000000:2800:F2365C5A83FAF756EBACCAEEF33B66DE2DF5FEA605C7DA80FAD05DC023309A5C.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-debug-local-function "（可选）通过端云一体化开发工程调试本地云函数")
# 调用本地云函数

更新时间: 2025-12-16 16:37

## 设置“设备端口”到“主机端口”的映射

调用本地云函数之前，请按照以下示例设置“设备端口”到“主机端口”的映射。详情请参见[创建反向端口转发任务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hdc#%E5%88%9B%E5%BB%BA%E5%8F%8D%E5%90%91%E7%AB%AF%E5%8F%A3%E8%BD%AC%E5%8F%91%E4%BB%BB%E5%8A%A1)。

1. hdc rport tcp:18090 tcp:18090

其中，设备端口和主机端口即为Function URI中的端口。

## 在应用中调用本地云函数

从6.0.1(21)版本开始，新增支持调用本地云函数功能。

1. 在项目中导入cloudFunction组件。
    
    1. import { cloudFunction } from '@kit.CloudFoundationKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    

2. 调用[call()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudfunction#section251833512544)方法设置函数，在方法中传入函数名称和本地启动的云函数地址，返回调用结果。
    
    - （可选）通过设置timeout属性对云函数设置超时时长，单位为毫秒。
    - （可选）通过设置version属性对云函数设置函数版本号，默认为最新版本'$latest'。
    - （可选）如果函数有入参，可以将data参数转化为JSON对象或JSON字符串传入，如果没有参数则不传。
    
    使用Promise异步回调：
    
    1. function callFunctionLocal() {
    2.   cloudFunction.call({
    3.     name: 'my-cloud-function', // my-cloud-function需替换为实际的函数名
    4.     version: '$latest',   // 如果不传入版本号，默认为“$latest”。
    5.     timeout: 10 * 1000,   // 单位为毫秒，默认为70*1000毫秒。
    6.     data: {               // data为函数请求体
    7.       param1: 'val1',
    8.       param2: 'val2'
    9.     },
    10.     localUrl: 'http://localhost:18090' // 本地启动的云函数地址
    11.   }).then((value: cloudFunction.FunctionResult) => {
    12.     hilog.info(0x0000, 'testTag', `Succeeded in calling the function, result: ${JSON.stringify(value.result)}`);
    13.   }).catch((err: BusinessError) => {
    14.     hilog.error(0x0000, 'testTag', `Failed to call the function, code: ${err.code}, message: ${err.message}`);
    15.   })
    16. }
    
    或者，使用callback异步回调：
    
    1. function callFunctionLocal() {
    2.   cloudFunction.call({
    3.     name: 'my-cloud-function', // my-cloud-function需替换为实际的函数名
    4.     version: '$latest',   // 如果不传入版本号，默认为“$latest”。
    5.     timeout: 10 * 1000,   // 单位为毫秒，默认为70*1000毫秒。
    6.     data: {               // data为函数请求体
    7.       param1: 'val1',
    8.       param2: 'val2'
    9.     },
    10.     localUrl: 'http://localhost:18090' // 本地启动的云函数地址
    11.   }, (err: BusinessError, value: cloudFunction.FunctionResult) => {
    12.     if (err) {
    13.       hilog.error(0x0000, 'testTag', `Failed to call the function, code: ${err.code}, message: ${err.message}`);
    14.       return;
    15.     }
    16.     hilog.info(0x0000, 'testTag', `Succeeded in calling the function, result: ${JSON.stringify(value.result)}`);
    17.   })
    18. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-start-local-function "启动本地云函数")
# 新增对象类型

更新时间: 2025-12-16 16:36

开发者需要基于AGC控制台创建对象类型。

## 前提条件

已[开通云数据库服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-enable-database)。

## 操作步骤

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，点击“开发与服务”。
2. 在项目列表中点击需要创建对象类型的项目。
3. 在左侧导航栏选择“云开发（Serverless）> 云数据库”，进入云数据库页面。
4. 点击“新增”，创建新的对象类型。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163631.77134990551352960292779729157081:50001231000000:2800:BECA5BABDF79C0E29836A97424F75E8F10114E8B542D9AA205C3D4B1483F98FB.png)
    
5. 输入“对象类型名”为“BookInfo”后，点击“下一步”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163631.67176426171110155928288448878239:50001231000000:2800:C0935867CD2A2D321E4F356496BECC74E10835CDF5A8FAA3E43BBFAF68D351A3.png)
    
6. 点击“+新增字段”，新增如下表字段后，点击“下一步”。
    
    |字段名称|类型|主键|非空|加密|默认值|
    |:--|:--|:--|:--|:--|:--|
    |id|Integer|✓|✓|–|–|
    |bookName|String|–|✓|–|–|
    |author|String|–|–|–|–|
    |price|Double|–|–|–|–|
    |borrowerId|Integer|–|–|–|–|
    |borrowerName|String|–|–|–|–|
    |borrowerTime|Date|–|–|–|–|
    
7. 点击“+”新增索引，设置“索引名”为“bookName”，点击“下一步”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163631.51603128083006337261231586239210:50001231000000:2800:903757D3F7FAF1B22EB221D077C4F02844E6A5BEE5FE5C1BFE3F197826B01D11.png)
    
8. 按照如下要求设置各角色权限后，点击“确定”。
    
    |角色|query|upsert|delete|说明|
    |:--|:--|:--|:--|:--|
    |所有人|✓|✓|✓|代表所有用户，包含认证和非认证用户。<br><br>该角色默认拥有query权限，可自定义配置upsert和delete权限。如：角色勾选了upsert权限，该角色可在本对象类型中写入数据。<br><br>但是，不建议将upsert和delete权限配置给所有人角色。<br><br>当对象类型中设置了加密字段之后，表示开启全程加密功能，此时**所有人**角色将不会拥有query、upsert和delete权限，且不允许修改。|
    |认证用户|✓|✓|✓|经过AGC登录认证的用户。<br><br>该角色默认拥有query权限，可自定义配置upsert和delete权限。如：角色勾选了upsert权限，该角色可在本对象类型中写入数据。<br><br>当对象类型中设置了加密字段之后，表示开启全程加密功能，此时**认证用户**角色将不会拥有query、upsert和delete权限，且不允许修改。|
    |数据创建者|✓|✓|✓|经过认证的数据创建用户。<br><br>该角色默认拥有所有权限，且可自定义配置所有权限。如：角色勾选了upsert权限，该角色可在本对象类型中写入数据。<br><br>每条数据都有其对应的数据创建人（即应用用户），每个数据创建者仅可以upsert或者delete自己创建的数据，不能upsert或者delete他人创建的数据。<br><br>数据创建者的信息保存在数据记录的系统表中。|
    |管理员|✓|✓|✓|应用开发者，主要是指通过AGC控制台或FaaS（Function as a Service，函数即服务）侧访问云数据库的角色。<br><br>该角色默认拥有所有权限，且可自定义配置所有权限。如：角色勾选了upsert权限，该角色可在本对象类型中写入数据。<br><br>管理员可以管理并配置其他角色的权限。|
    
9. 创建完成后返回对象类型列表，可以查看已创建的对象类型。
10. 勾选创建的BookInfo对象类型，点击“导出”。若不勾选对象类型，默认导出所有对象类型。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163631.53104475643677768211605168637291:50001231000000:2800:A5B036063346A40E9BC583748F412C7217A8B377412882F7952F5B4041196E1B.png)
    
11. 导出“json格式”文件，点击“确定”。后续[引入对象类型文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-add-file)时，需要使用此文件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163631.35180822683374677942368944093889:50001231000000:2800:1C82487B5E0761AD9EB42703CA83BA981DA20869DBDFE996D5FF718411C7AACF.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-service "云数据库")
# 新增存储区

更新时间: 2025-12-16 16:36

此章节以建一个“存储区名称”为“QuickStartDemo”的存储区举例说明。

## 前提条件

已[开通云数据库服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-enable-database)。

## 操作步骤

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，点击“开发与服务”。
2. 在项目列表中点击需要创建存储区的项目。
3. 在左侧导航栏选择“云开发（Serverless）> 云数据库”，进入云数据库页面。
4. 点击“存储区”页签，点击“新增”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163646.00715492021748704286321347954593:50001231000000:2800:E6E5F275E8A5B0921CB42544FA17028B39E19C9095AFB656C1CAADBFCF50E7C9.png)
    
5. 在“新增存储区”弹框中填写“存储区名称”为“QuickStartDemo”，点击“确定”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163646.64357762685734209562457198826469:50001231000000:2800:AEF3B71B7581DF2C9EC547CB800D3F194C2613F1CF0DDF2081A5A11D2D634691.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-add-object "新增对象类型")
# 引入对象类型文件

更新时间: 2025-12-16 16:36

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

- 已[新增对象类型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-add-object)。
- 已[新增存储区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-add-zone)。

## 操作步骤

1. 将导出的[json格式文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-add-object#zh-cn_topic_0000001518866308_li0821548919)命名为schema.json，拷贝到DevEco Studio项目的“AppScope/resources/rawfile”或者“entry/src/main/resources/rawfile”目录下。在编译构建过程中，AppScope目录下的资源文件会合入到模块的资源文件中，详细信息请参见[资源分类](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access#%E8%B5%84%E6%BA%90%E5%88%86%E7%B1%BB)。
2. 按照AGC控制台上创建的对象类型“BookInfo”在代码工程中创建BookInfo.ets文件，文件内容参考以下代码。
    
    说明
    
    在AGC控制台创建的字段类型与ArkTS数据类型的匹配关系如下：
    
    - String、Text对应string。
    - Boolean对应boolean。
    - Byte、ByteArray对应Uint8Array。
    - Short、Integer、Long、Float、Double、IntAutoIncrement、LongAutoIncrement对应number。
    - Date对应Date。
    
    1. import { cloudDatabase } from '@kit.CloudFoundationKit';
    
    2. class BookInfo extends cloudDatabase.DatabaseObject{
    3.   public naturalbase_ClassName(): string {
    4.     return "BookInfo";
    5.   }
    6.   public id: number | undefined;
    7.   public bookName: string | undefined;
    8.   public author: string | undefined;
    9.   public price: number | undefined;
    10.   public borrowerId: number | undefined;
    11.   public borrowerName: string | undefined;
    12.   public borrowerTime: Date | undefined;
    13. }
    
    14. export { BookInfo };
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-add-zone "新增存储区")
# 初始化数据库访问

更新时间: 2025-12-16 16:37

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

已[引入对象类型文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-add-file)。

## 操作步骤

1. 设置云数据库配置项。
    
    在“entry/src/main/module.json5”文件中添加网络权限。
    
    1. "requestPermissions": [
    2.   {
    3.     "name": "ohos.permission.INTERNET"
    4.   }
    5. ]
    
2. （可选）如果存在需要登录应用才能操作数据库的场景（如新增或删除数据），您需要执行如下操作：
    1. [通过AuthProvider获取用户凭据](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudcommon#section136610231214)。
    2. 调用[cloudCommon.init()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudcommon#section15555111210233)方法进行初始化时，传入获取的凭据。
3. 在业务代码中，使用AGC开发平台上创建的存储区“QuickStartDemo”类初始化DatabaseZone。
    
    1. import { cloudDatabase } from '@kit.CloudFoundationKit';
    
    2. let databaseZone = cloudDatabase.zone('QuickStartDemo');
    
    注意
    
    - cloudDatabase.zone方法接收的入参为“存储区名称”，即cloudDBZoneName，请参见[新增存储区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-add-zone)章节。
    - 存储区最多创建4个，超过4个会导致云数据库访问失败。
    
4. 如果需要使用数据库查询方法，可以使用类（此处以BookInfo为例）初始化DatabaseQuery。
    
    1. import { BookInfo } from 'xx/BookInfo'; // xx是BookInfo文件的相对路径
    
    2. let condition = new cloudDatabase.DatabaseQuery(BookInfo);
    
    说明
    
    后续“databaseZone”、“condition”都需要在每个查询中独立使用，可以参考此章节创建，下文代码中不再重复创建的操作。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-add-file "引入对象类型文件")
# 查询数据

更新时间: 2025-12-16 16:37

云数据库通过[query()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section390417613213)方法查询对象，并提供了丰富的谓词查询，比如[equalTo()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section9706571488)、[notEqualTo()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section16955165444812)、[in()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section6276103955110)等。通过单个或者多个链式过滤条件，开发者可以从存储区查询到满足特定条件的对象，也可以通过排序谓词对查询结果排序，或者通过限定查询返回数量谓词限定查询结果返回的数量。详细的查询条件请参见[DatabaseQuery](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section76501736191415)。

应用会直接从云侧存储区服务器查询数据，本地不会缓存数据。

说明

- 每次的查询操作仅支持查询一个对象类型下的数据。

- 调用查询数据方法，有两种返回方式，返回一个Promise对象或者在参数中传入一个callback对象返回，下面以Promise为例详细说明。

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

已[初始化数据库访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-initialize)。

## 简单查询

开发者可以在无查询条件时，获取一个对象类型中所有的对象；也可以指定单个查询条件，来获取满足该条件的对象。

- 查询对象类型BookInfo的所有数据。
    
    1. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    2. async queryAll() {
    3.   try {
    4.     let resultArray = await databaseZone.query(condition);
    5.     hilog.info(0x0000, 'testTag', `Succeeded in querying data, result: ${JSON.stringify(resultArray)}`);
    6.   } catch (err) {
    7.     hilog.error(0x0000, 'testTag', `Failed to query data, code: ${err.code}, message: ${err.message}`);
    8.   }
    9. }
    
    说明
    
    后续hilog都需要从@kit.PerformanceAnalysisKit中引入，将不在示例代码中呈现。
    
- 通过异步侦听的方式查询“bookName”参数对应的书籍。
    
    1. async queryBook(bookName: string): Promise<BookInfo> {
    2.   try {
    3.     condition.equalTo('bookName', bookName);
    4.     let resultArray = await databaseZone.query(condition);
    5.     let bookInfo = resultArray[0];
    6.     hilog.info(0x0000, 'testTag', `Succeeded in querying data, result: ${JSON.stringify(resultArray)}`);
    7.     return Promise.resolve(bookInfo);
    8.   } catch (err) {
    9.     hilog.error(0x0000, 'testTag', `Failed to query data, code: ${err.code}, message: ${err.message}`);
    10.     return Promise.reject(err);
    11.   }
    12. }
    

## 复合查询

开发者可以通过多个链式过滤条件，来获取满足条件的对象。多个链式条件之间默认用“与”运算。

- 构造查询条件，并调用[query()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section390417613213)方法，查询“bookName”包含“数据库”，“price”大于20.0并且小于50.0的书籍。
    
    1. condition.contains('bookName', '数据库')
    2.   .greaterThan('price', 20.0)
    3.   .and()
    4.   .lessThan('price', 50.0);
    5. let resultArray = await databaseZone.query(condition);
    
- 构造查询条件，并调用[query()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section390417613213)方法，查询“bookName”包含“数据库”，“price”在小于20.0或者大于50.0区间的书籍。
    
    1. condition.contains('bookName', '数据库')
    2.   .lessThan('price', 20.0)
    3.   .or()
    4.   .greaterThan('price', 50.0);
    5. let resultArray = await databaseZone.query(condition);
    
- 构造查询条件，并调用[query()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section390417613213)方法，查询“bookName”包含“史记”，“author”是“司马迁”，“price”大于60.0的书籍。
    
    1. condition.contains('bookName', '史记')
    2.   .equalTo('author', '司马迁')
    3.   .greaterThan('price', 60.0);
    4. let resultArray = await databaseZone.query(condition);
    
- 构造查询条件，并调用[query()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section390417613213)方法，查询“bookName”包含“自传”，并且“author”是“齐白石”，或者“author”是“司马迁”，并且“price”大于60.0的书籍。
    
    1. condition.contains('bookName', '自传')
    2.   .beginGroup()
    3.   .equalTo('author', '齐白石')
    4.   .or()
    5.   .equalTo('author', '司马迁')
    6.   .endGroup()
    7.   .greaterThan('price', 60.0);
    8. let resultArray = await databaseZone.query(condition);
    

## 数据排序

开发者可以通过[orderByAsc()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section0344144315513)或者[orderByDesc()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section1754544435111)实现对查询结果集中的对象按某个字段进行升序或者降序排列，排序谓词需要在其它查询谓词之后且在限定数据查询数量谓词之前。

1. condition.lessThan('price', 50.0)
2.   .orderByDesc('price');
3. let resultArray = await databaseZone.query(condition);

## 随机查询

从6.0.1(21)版本开始，新增支持随机查询功能。

开发者可以通过[orderByRandom()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section19149641220)按随机顺序展示查询结果集中的对象。

该方法适用于推荐随机内容、播放随机音视频等场景。

1. condition.orderByRandom()
2.   .limit(10);
3. let resultArray = await databaseZone.query(condition);

## 限定数据查询返回数量

在查询数据时，开发者可以通过[limit()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section9232724175819)限定查询返回数据的起始位置和数量，实现数据的分页。例如与排序查询谓词组合使用，可以实现获取top-N条数据。

对查询结果中的对象限定查询返回数量时，限定数据查询返回数量谓词在所有其他谓词查询之后。

- 构造查询条件，并调用[query()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section390417613213)方法，查询所有价格小于50.0的书籍，并且只显示最开始10条记录。
    
    1. condition.lessThan('price', 50.0)
    2.   .limit(10);
    3. let resultArray = await databaseZone.query(condition);
    
- 构造查询条件，并调用[query()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section390417613213)方法，查询所有价格小于50.0的书籍，并将查询结果按照降序排序，只显示价格排序从第6条开始的10条记录。
    
    1. condition.lessThan('price', 50.0)
    2.   .orderByDesc('price')
    3.   .limit(10, 6);
    4. let resultArray = await databaseZone.query(condition);
    

## 对查询结果进行算术计算

在查询数据时，可以通过[calculateQuery()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section1248132432017)对查询结果对象中的某个字段进行算术计算并返回计算的结果。

构造查询条件，并调用[calculateQuery()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section1248132432017)方法，查询所有价格小于50.0的书籍，并且计算所有书籍价格的平均值。

1. async calculateQuery() {
2.   try {
3.     condition.lessThan('price', 50.0);
4.     let resultNum = await databaseZone.calculateQuery(condition, 'price', cloudDatabase.QueryCalculate.AVERAGE);
5.     hilog.info(0x0000, 'testTag', `Succeeded in calculating queried data, result: ${JSON.stringify(resultNum)}`);
6.   } catch (err) {
7.     hilog.error(0x0000, 'testTag', `Failed to calculate queried data, code: ${err.code}, message: ${err.message}`);
8.   }
9. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-initialize "初始化数据库访问")
# 写入数据

更新时间: 2025-12-16 16:37

开发者可以通过[upsert()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section686153211276)将一个或者一组对象写入到当前存储区中。在写入对象时，如果在存储区已经存在主键相同的对象，则更新已有的对象；如果不存在，则写入一个新的对象。写入的数据可以来自于新建对象，或者从存储区查询出来的对象。

写入一组对象时，数据的写入操作是原子性的，即对象列表中的对象要么全部成功写入，要么全部失败。

说明

- 写入一组对象时，该组中的对象必须属于同一个对象类型，否则会导致写入失败。
- 写入一组对象时，数据总大小不能超过2MB，否则会导致写入失败。
- 写入一组对象时，数据总条数不能超过1000条，否则会导致写入失败。
- 调用写入数据方法，有两种返回方式，返回一个Promise对象或者在参数中传入一个callback对象返回，下面以Promise为例详细说明。

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

已[初始化数据库访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-initialize)。

## 写入数据

Promise对象中封装了写入操作执行的结果，通过该Promise对象可以异步侦听执行结果：如果执行成功，可以获取写入的对象数量；如果执行失败，可以获取错误信息。

**代码示例：**

将BookInfo对象写入至存储区中，写入成功后，返回写入的数量；写入失败，抛出异常。

1. // 更新”西游记”的借阅者信息
2. async upsert() {
3.   try {
4.     let book = await this.queryBook('西游记'); // 查询出”西游记”的书籍信息
5.     book.borrowerId = 1;
6.     book.borrowerName = '小明';
7.     book.borrowerTime = new Date();
8.     let record = await databaseZone.upsert(book);
9.     hilog.info(0x0000, 'testTag', `Succeeded in upserting a book, result: ${JSON.stringify(record)}`);
10.   } catch (err) {
11.     hilog.error(0x0000, 'testTag', `Failed to upsert a book, code: ${err.code}, message: ${err.message}`);
12.   }
13. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-query "查询数据")
# 删除数据

更新时间: 2025-12-16 16:37

开发者可以通过[delete()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase#section1630522892714)删除单个对象或者一组对象。删除数据时，云数据库会根据传入对象主键删除相应的数据，不会比对该对象其它属性与存储的数据是否一致。删除一组对象时，删除操作是原子性的，即对象列表中的对象要么全部删除成功，要么全部删除失败。

说明

- 删除一组对象时，该组中的对象必须属于同一个对象类型，否则会导致删除失败。
- 调用删除数据方法，有两种返回方式，返回一个Promise对象或者在参数中传入一个callback对象返回，本文以Promise为例详细说明。

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

已[初始化数据库访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-initialize)。

## 删除数据

**代码示例：**

将对象删除，如果删除成功，返回删除对象的个数；执行失败，抛出异常。

1. // 假设图书遗失，图书管理员需要将遗失的书籍从BookInfo表里删除
2. async delete() {
3.   try {
4.     let book = new BookInfo(); 
5.     book.id = 3;
6.     let deleteNum = await databaseZone.delete(book);
7.     hilog.info(0x0000, 'testTag', `Succeeded in deleting data, result: ${JSON.stringify(deleteNum)}`);
8.   } catch (err) {
9.     hilog.error(0x0000, 'testTag', `Failed to delete data, code: ${err.code}, message: ${err.message}`);
10.   }
11. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-upsert "写入数据")
# 设置云存储配置项

更新时间: 2025-12-16 16:36

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 操作步骤

1. 在“entry/src/main/module.json5”文件中添加网络权限。
    
    1. "requestPermissions": [
    2.   {
    3.     "name": "ohos.permission.INTERNET"
    4.   }
    5. ]
    
2. （可选）如果存在需要登录应用才能使用云存储的场景（如上传下载文件），您需要执行如下操作：
    1. [通过AuthProvider获取用户凭据](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudcommon#section136610231214)。
    2. 调用[cloudCommon.init()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudcommon#section15555111210233)方法进行初始化时，传入获取的凭据。
3. （可选）自定义初始化参数。
    
    如开发者需要自定义云存储接口使用的网络类型或任务模式等初始化参数，可参考如下配置。
    
    - 通过[StorageOptions.network](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudcommon#section1772621115138)配置云存储接口使用的网络类型，不配置则使用默认值request.agent.Network.ANY。
        
        1. import { cloudCommon } from '@kit.CloudFoundationKit';
        2. import { request } from '@kit.BasicServicesKit';
        
        3. // 设置云存储只使用wifi网络
        4. cloudCommon.init({
        5.   storageOptions: {
        6.     network: request.agent.Network.WIFI
        7.   }  
        8. })
        
    - 通过[StorageOptions.mode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudcommon#section1772621115138)配置云存储上传下载任务的工作模式，不配置则使用默认值request.agent.Mode.BACKGROUND。
        
        1. import { cloudCommon } from '@kit.CloudFoundationKit';
        2. import { request } from '@kit.BasicServicesKit';
        
        3. // 设置云存储上传下载任务为前台模式
        4. cloudCommon.init({
        5.   storageOptions: {
        6.     mode: request.agent.Mode.FOREGROUND
        7.   }
        8. })
        

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-service "云存储")
# 初始化全局应用上下文

更新时间: 2025-12-16 16:36

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 操作步骤

在使用云存储服务进行上传下载时，需要使用应用上下文context。可参考如下代码初始化全局应用上下文。

1. 在“entry/src/main/ets/common”目录下添加GlobalContext.ets文件，开发初始化和获取应用上下文的接口。
    
    1. import { common } from '@kit.AbilityKit';
    
    2. export class GlobalContext {
    3.   private static context: common.UIAbilityContext;
    
    4.   public static initContext(context: common.UIAbilityContext): void {
    5.     GlobalContext.context = context;
    6.   }
    
    7.   public static getContext(): common.UIAbilityContext {
    8.     return GlobalContext.context;
    9.   }
    10. }
    
2. 在“entry/src/main/ets/entryability/EntryAbility.ets”文件中导入GlobalContext，在onCreate方法中使用GlobalContext.initContext(this.context)初始化全局应用上下文。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-config "设置云存储配置项")
# 初始化存储实例

更新时间: 2025-12-16 16:36

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

已[开通云存储服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-enable-storage)。

## 操作步骤

调用[cloudStorage.bucket](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudstorage#section1286815320203)初始化一个存储实例。支持使用两种方式初始化实例：

- 使用默认实例
    
    1. import { cloudStorage } from '@kit.CloudFoundationKit';
    
    2. let bucket: cloudStorage.StorageBucket = cloudStorage.bucket(); // 将启动异步任务查询云侧默认实例
    
    以“使用默认实例”方式初始化云存储实例，将启动异步任务去云侧查询默认实例。因此，当涉及多次云存储操作时，建议只初始化一次，后续的操作基于初始化一次的云存储实例进行，而非每次操作都初始化云存储实例。
    
    3. // 只初始化一次云存储实例
    4. let bucket: cloudStorage.StorageBucket = cloudStorage.bucket(); 
    5. bucket.list(...); 
    6. bucket.uploadFile(...);
    
    不建议：
    
    7. // 多次初始化云存储实例
    8. cloudStorage.bucket().list(...);
    9. cloudStorage.bucket().uploadFile(...);
    
- 使用指定的实例
    
    1. import { cloudStorage } from '@kit.CloudFoundationKit';
    
    2. let bucket: cloudStorage.StorageBucket = cloudStorage.bucket('bucket001-ki6tc'); // 指定 bucket001-ki6tc 实例
    
    注意
    
    以“使用指定的实例”方式初始化云存储实例，请确保当前云侧存在该存储实例，否则后续操作将出现找不到存储实例错误。在云侧创建新的存储实例，可参考[存储实例管理](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-storage-manage-bucket-0000001281294006)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-initialize-context "初始化全局应用上下文")
# 上传指定文件至云侧

更新时间: 2025-12-16 16:37

开发者可以快速将本地设备上的文件上传至云侧，上传完后，可以前往AppGallery Connect的“云存储”页面，查看上传的文档内容。

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

已[初始化存储实例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-initialize-bucket)。

## 操作步骤

1. 选择待上传的文件，下方示例代码中使用[photoAccessHelper.PhotoViewPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-photoaccesshelper-photoviewpicker)指定需要上传的文件。
2. 将待上传的文件复制到[context.cacheDir](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context#%E5%B1%9E%E6%80%A7)目录下。
    
    说明
    
    由于StorageBucket.uploadFile接口传入参数localPath只能设置为context.cacheDir目录下的文件路径，所以上传前需要先将文件复制到context.cacheDir目录下。
    
3. 调用[StorageBucket.uploadFile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudstorage#section2105131521913)接口创建上传任务，监听上传任务的progress、completed、failed等事件。
4. 启动上传任务。

完整的示例代码如下：

1. import { cloudStorage } from '@kit.CloudFoundationKit';
2. import { BusinessError, request } from '@kit.BasicServicesKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';
4. import { photoAccessHelper } from '@kit.MediaLibraryKit';
5. import { fileIo as fs } from '@kit.CoreFileKit';
6. import { GlobalContext } from '../common/GlobalContext';

7. let storageBucket: cloudStorage.StorageBucket = cloudStorage.bucket();

8. @Component
9. export struct testPage {
10.   build() {
11.   }

12.   // 上传指定文件至云侧
13.   upload() {
14.     this.selectPhoto().then((photoSelectResult: photoAccessHelper.PhotoSelectResult) => {
15.       let fileUri = photoSelectResult.photoUris[0];
16.       hilog.info(0x0000, 'testTag', `pick file ${fileUri}`);
17.       let fileName = fileUri.split('/').pop() as string;
18.       hilog.info(0x0000, 'testTag', `file name ${fileName}`);
19.       let cacheFile = GlobalContext.getContext().cacheDir + '/' + fileName;
20.       hilog.info(0x0000, 'testTag', `cacheFile ${cacheFile}`);
21.       // 将选中文件copy至cache目录下
22.       this.copyFile(fileUri, cacheFile);
23.       // 上传至云存储默认实例
24.       this.uploadFile(cacheFile, `screenshot/${fileName}`);
25.     }).catch((err: BusinessError) => {
26.       hilog.error(0x0000, 'testTag', `Failed to upload file, code: ${err.code}, message: ${err.message}`);
27.     })
28.   }

29.   /**
30.    * @throws photoViewPicker select throws
31.    */
32.   selectPhoto(): Promise<photoAccessHelper.PhotoSelectResult> {
33.     // 使用photoAccessHelper选择指定的文件
34.     let photoSelectOptions = new photoAccessHelper.PhotoSelectOptions();
35.     photoSelectOptions.MIMEType = photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE; // 过滤选择媒体文件类型为IMAGE
36.     photoSelectOptions.maxSelectNumber = 1; // 选择媒体文件的最大数目
37.     let photoViewPicker = new photoAccessHelper.PhotoViewPicker();
38.     return photoViewPicker.select(photoSelectOptions);
39.   }

40.   copyFile(srcPath: string, dstPath: string) {
41.     try {
42.       let srcFile = fs.openSync(srcPath);
43.       let dstFile = fs.openSync(dstPath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
44.       fs.copyFileSync(srcFile.fd, dstFile.fd);
45.       fs.closeSync(srcFile);
46.       fs.closeSync(dstFile);
47.     } catch (e) {
48.       hilog.error(0x0000, 'testTag', `copy file failed ${e.message}`);
49.       return;
50.     }
51.   }

52.   uploadFile(localPath: string, cloudPath: string) {
53.     storageBucket.uploadFile(GlobalContext.getContext(), {
54.       localPath: localPath, // 本地文件路径（context.cacheDir目录下的文件路径）
55.       cloudPath: cloudPath   // 云侧路径，支持传入“文件目录/文件名”（如“screenshot/demo.jpg”），或仅传入文件名。
56.     }).then((task: request.agent.Task) => {
57.       task.on('progress', (progress) => {
58.         hilog.info(0x0000, 'testTag', `on progress ${JSON.stringify(progress)}`);
59.       });
60.       task.on('completed', (progress) => {
61.         hilog.info(0x0000, 'testTag', `on completed ${JSON.stringify(progress)}`);
62.         // 删除cache目录临时文件
63.         fs.unlink(localPath).catch((err: BusinessError) => {
64.           hilog.error(0x0000, 'testTag', `Failed to unlink, code: ${err.code}, message: ${err.message}.`);
65.         });
66.       });
67.       task.on('failed', (progress) => {
68.         hilog.info(0x0000, 'testTag', `on failed ${JSON.stringify(progress)}`);
69.         // 删除cache目录临时文件
70.         fs.unlink(localPath).catch((err: BusinessError) => {
71.           hilog.error(0x0000, 'testTag', `Failed to unlink, code: ${err.code}, message: ${err.message}.`);
72.         });
73.       });
74.       task.on('response', (response) => {
75.         hilog.info(0x0000, 'testTag', `on response ${JSON.stringify(response)}`);
76.       });

77.       // start task
78.       task.start((err: BusinessError) => {
79.         if (err) {
80.           hilog.error(0x0000, 'testTag',
81.             `Failed to start a file upload task, code: ${err.code}, message: ${err.message}`);
82.         } else {
83.           hilog.info(0x0000, 'testTag', `Succeeded in starting a file upload task.`);
84.         }
85.       });
86.     }).catch((err: BusinessError) => {
87.       hilog.error(0x0000, 'testTag', `Failed to upload file, code: ${err.code}, message: ${err.message}`);
88.     })
89.   }
90. }

说明

上传完成，可以登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，选择项目，进入“云存储”界面查看文件列表。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-initialize-bucket "初始化存储实例")
# 下载云侧文件至本地

更新时间: 2025-12-16 16:37

文件上传至云侧后，开发者可以将云侧文件下载到本地设备中。

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

- 已[初始化存储实例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-initialize-bucket)。
- 已[上传指定文件至云侧](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-upload-file)。

## 操作步骤

1. 调用[StorageBucket.downloadFile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudstorage#section02263293319)接口创建下载任务，监听下载任务的progress、completed、failed等事件。
2. 启动下载任务。
    
    说明
    
    下载成功后，文件将保存在[context.cacheDir](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context#%E5%B1%9E%E6%80%A7)目录下。
    

完整示例代码如下：

1. import { cloudStorage } from '@kit.CloudFoundationKit';
2. import { BusinessError, request } from '@kit.BasicServicesKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';
4. import { GlobalContext } from '../common/GlobalContext';

5. let storageBucket: cloudStorage.StorageBucket = cloudStorage.bucket();

6. @Component
7. export struct testPage {
8.   build() {
9.   }

10.   // 下载云侧文件至本地
11.   download() {
12.     // 获取云存储默认实例中fileName文件，保存至本地
13.     storageBucket.downloadFile(GlobalContext.getContext(), {
14.       localPath: `screenshot.jpg`, // 文件将会保存在context.cacheDir目录下
15.       cloudPath: `screenshot/screenshot_20250115_155321.jpg`  // 云侧文件路径，支持传入“文件目录/文件名”，或仅传入文件名
16.     }).then((task: request.agent.Task) => {
17.       task.on('progress', (progress) => {
18.         hilog.info(0x0000, 'testTag', `on progress ${JSON.stringify(progress)} `);
19.       });
20.       task.on('completed', (progress) => {
21.         hilog.info(0x0000, 'testTag', `on completed ${JSON.stringify(progress)} `);
22.       });
23.       task.on('failed', (progress) => {
24.         hilog.info(0x0000, 'testTag', `on failed ${JSON.stringify(progress)} `);
25.       });
26.       task.on('response', (response) => {
27.         hilog.info(0x0000, 'testTag', `on response ${JSON.stringify(response)} `);
28.       });
29.       task.start((err: BusinessError) => {
30.         if (err) {
31.           hilog.error(0x0000, 'testTag',
32.             `Failed to start a file download task, code: ${err.code}, message: ${err.message}`);
33.         } else {
34.           hilog.info(0x0000, 'testTag', `Succeeded in starting a file download task. result: ${task.tid}`);
35.         }
36.       });
37.     }).catch((err: BusinessError) => {
38.       hilog.error(0x0000, 'testTag', `Failed to download file, code: ${err.code}, message: ${err.message}`);
39.     })
40.   }
41. }

说明

如果本地已存在同名文件，将出现错误，可以通过设置[DownloadParams.overwrite](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudstorage#section14137913019)来决定是否覆盖本地文件。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-upload-file "上传指定文件至云侧")
# 获取云侧文件下载地址

更新时间: 2025-12-16 16:37

文件上传至云侧后，开发者可以获取云侧文件的下载地址，将下载地址放到网站中提供文件下载的体验。

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

- 已[初始化存储实例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-initialize-bucket)。
- 已[上传指定文件至云侧](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-upload-file)。

## 操作步骤

调用[StorageBucket.getDownloadURL](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudstorage#section9969145143317)接口获取云侧文件的下载地址。

完整示例代码如下：

1. import { cloudStorage } from '@kit.CloudFoundationKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';

4. let storageBucket: cloudStorage.StorageBucket = cloudStorage.bucket();

5. @Component
6. export struct testPage {
7.   build() {
8.   }

9.   // 获取云侧文件下载地址
10.   getUrl() {
11.     // 获取云存储默认实例中screenshot/screenshot_20250115_155321.jpg文件的下载地址
12.     storageBucket.getDownloadURL('screenshot/screenshot_20250115_155321.jpg').then((downloadURL: string) => {
13.       hilog.info(0x0000, 'testTag', `Succeeded in getting download URL: ${downloadURL}`);
14.     }).catch((err: BusinessError) => {
15.       hilog.error(0x0000, 'testTag', `Failed to get download URL, code: ${err.code}, message: ${err.message}`);
16.     })
17.   }
18. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-download-file "下载云侧文件至本地")
# 删除云侧文件

更新时间: 2025-12-16 16:37

当云侧文件不需要时，开发者可以在应用客户端删除云侧的文件。

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

- 已[初始化存储实例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-initialize-bucket)。
- 已[上传指定文件至云侧](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-upload-file)。

## 操作步骤

调用[StorageBucket.deleteFile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudstorage#section1290422653419)删除云侧的文件。

注意

删除操作不可逆，一旦执行，文件会被物理删除，不可找回。

完整示例代码如下：

1. import { cloudStorage } from '@kit.CloudFoundationKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';

4. let storageBucket: cloudStorage.StorageBucket = cloudStorage.bucket();

5. @Component
6. export struct testPage {
7.   build() {
8.   }

9.   // 删除云侧文件
10.   deleteFile() {
11.     // 删除云存储默认实例中screenshot/screenshot_20250115_155321.jpg文件
12.     storageBucket.deleteFile('screenshot/screenshot_20250115_155321.jpg').then(() => {
13.       hilog.info(0x0000, 'testTag', `Succeeded in deleting file.`);
14.     }).catch((err: BusinessError) => {
15.       hilog.error(0x0000, 'testTag', `Failed to delete file, code: ${err.code}, message: ${err.message}`);
16.     })
17.   }
18. }

说明

删除文件后，可以登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，选择项目，进入“云存储”界面查看文件列表。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-getdownloadurl "获取云侧文件下载地址")
# 获取云侧文件列表

更新时间: 2025-12-16 16:37

开发者可以获取指定云侧目录下所有的文件信息，包括文件存储目录、文件名称等。

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

- 已[初始化存储实例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-initialize-bucket)。
- 已[上传指定文件至云侧](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-upload-file)。

## 操作步骤

调用[StorageBucket.list](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudstorage#section420475053513)可以获取云侧指定目录的文件列表。

完整示例代码如下：

1. import { cloudStorage } from '@kit.CloudFoundationKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';

4. let storageBucket: cloudStorage.StorageBucket = cloudStorage.bucket();

5. @Component
6. export struct testPage {
7.   build() {
8.   }

9.   // 获取文件列表
10.   getList() {
11.     // 获取云存储默认实例中根路径下的文件列表
12.     storageBucket.list('').then((result: cloudStorage.ListResults) => {
13.       hilog.info(0x0000, 'testTag', `Succeeded in listing files, result: ${JSON.stringify(result)}`);
14.     }).catch((err: BusinessError) => {
15.       hilog.error(0x0000, 'testTag', `Failed to list files, code: ${err.code}, message: ${err.message}`);
16.     })
17.   }
18. }

获取文件列表信息结构如下：

1. {
2.   directories: ["empty-dir1\/", "screenshot\/"],
3.   files: ["IMG_20240229_103118.jpg", "IMG_20240318_093732.jpg"]
4. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-delete-file "删除云侧文件")
# 获取云侧文件的元数据

更新时间: 2025-12-16 16:37

文件元数据包含云侧文件名、文件大小、文件类型等常用属性，也包括用户自定义的文件属性。

文件上传至云侧后，开发者可以在下载文件前获取指定云侧文件的元数据，来决定是否下载此文件。

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

- 已[初始化存储实例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-initialize-bucket)。
- 已[上传指定文件至云侧](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-upload-file)。

## 操作步骤

调用[StorageBucket.getMetadata](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudstorage#section2031534817364)获取指定云侧文件的元数据信息。

完整示例代码如下：

1. import { cloudStorage } from '@kit.CloudFoundationKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';

4. let storageBucket: cloudStorage.StorageBucket = cloudStorage.bucket();

5. @Component
6. export struct testPage {
7.   build() {
8.   }

9.   // 获取元数据
10.   getMetaData() {
11.     // 获取云存储默认实例中screenshot/screenshot_20250115_155321.jpg文件的元数据信息
12.     storageBucket.getMetadata('screenshot/screenshot_20250115_155321.jpg').then((metadata: cloudStorage.Metadata) => {
13.       hilog.info(0x0000, 'testTag', `Succeeded in getting metadata: ${JSON.stringify(metadata)}`);
14.     }).catch((err: BusinessError) => {
15.       hilog.error(0x0000, 'testTag', `Failed to get metadata, code: ${err.code}, message: ${err.message}`);
16.     })
17.   }
18. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-list-files "获取云侧文件列表")
# 设置云侧文件的元数据

更新时间: 2025-12-16 16:37

文件元数据包含云侧文件名、文件大小、文件类型等常用属性，也包括用户自定义的文件属性。

文件保存至云侧后，开发者可以设置文件的自定义属性。

## 约束与限制

支持Phone、Tablet设备。并且从5.1.0(18)版本开始，新增支持Wearable设备；从5.1.1(19)版本开始，新增支持TV设备。

## 前提条件

- 已[初始化存储实例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-initialize-bucket)。
- 已[上传指定文件至云侧](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-upload-file)。

## 操作步骤

调用[StorageBucket.setMetadata](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudstorage#section1924314716387)可以设置云侧文档的元数据信息。

1. import { cloudStorage } from '@kit.CloudFoundationKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';

4. let storageBucket: cloudStorage.StorageBucket = cloudStorage.bucket();

5. @Component
6. export struct testPage {
7.   build() {
8.   }

9.   // 设置元数据
10.   setMetaData() {
11.     // 设置云存储默认实例中screenshot/screenshot_20250115_155321.jpg文件的元数据信息
12.     storageBucket.setMetadata('screenshot/screenshot_20250115_155321.jpg', {
13.       customMetadata: {
14.         key1: "value1",
15.         key2: "value2"
16.       }
17.     }).then((metadata: cloudStorage.Metadata) => {
18.       hilog.info(0x0000, 'testTag', `Succeeded in setting metadata: ${JSON.stringify(metadata)}`);
19.     }).catch((err: BusinessError) => {
20.       hilog.error(0x0000, 'testTag', `Failed to set metadata, code: ${err.code}, message: ${err.message}`);
21.     })
22.   }
23. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-storage-getmetadata "获取云侧文件的元数据")
# 云存储

更新时间: 2025-12-16 16:36

- **[使用云存储上传文件失败，提示“404:Product does not exist”](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-faq-1)**  
    
- **[使用云存储上传文件失败，app日志提示“"state":65”，upload进程日志提示“403 Forbidden”](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-faq-2)**  
    
- **[调用云存储业务接口失败，app日志提示“"state":65”，upload进程日志提示“404 Not Found”](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-faq-6)**  
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-faq "Cloud Foundation Kit常见问题")
