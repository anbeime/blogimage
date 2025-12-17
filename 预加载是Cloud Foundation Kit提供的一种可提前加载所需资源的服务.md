# 概述

更新时间: 2025-12-16 16:36

从5.0.3(15)版本开始，新增支持安装预加载和周期性预加载功能。

预加载是Cloud Foundation Kit提供的一种可提前加载所需资源的服务。通过预加载，可以将页面所需的文本、图片、音频、视频等资源数据提前加载到本地进行缓存，以提升应用页面加载速度。预加载仅以原始二进制数据进行缓存，应用使用预加载时不需要修改原有数据格式，获取缓存后可直接进行解析，并且可以对隐私、敏感数据进行加密。

当前支持如下两种预加载类型：

- **安装预加载**：适用于安装后首次打开，应用首页加载提速场景。在应用安装时下载云侧应用数据进行缓存，应用打开时直接获取本地首开页面缓存数据呈现内容。
- **周期性预加载**：适用于任意页面加载提速的场景，可与安装预加载结合使用。系统每隔12小时拉取一次指定页面（不局限首开页面）的云侧数据并将其缓存到本地，并可将静态资源放置到云端，减少包体大小。比较适合节日主题资源、H5离线包等场景。

同时还支持**H5预加载组件FastWeb**，它是基于Open Harmony基础组件开发的高性能Web容器，具有预启动、预渲染、预编译JavaScript生成字节码缓存、离线资源免拦截注入等能力，可为应用中Web页面的加载进行提速。H5预加载组件FastWeb无需使用Cloud Foundation Kit能力，详细使用方法可参考[Web容器FastWeb](https://developer.huawei.com/consumer/cn/market/prod-detail/686766c4728d43cc9741728552a560bf/2adce9bbd4cb42d58a87e6add45594b3)。

## 工作原理

1. 预加载服务根据配置的数据预加载策略从应用后台获取数据。
2. 预加载服务将获取的数据在本地进行缓存。
3. 应用使用获取的缓存数据，进行页面渲染。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163632.12314830358599314824647197935909:50001231000000:2800:F39506412E0EB83A7324766C84E42D4C1B829AE245308E73ED6F18A568760C92.jpg "点击放大")

## 典型应用场景

### 提升应用首开速度

在应用启动前或初始化阶段，为避免出现首页内容加载慢、白屏等情况，开发者可以使用预加载将一些必要的资源，例如图片、音频、视频或数据文件，提前加载到本地进行缓存。用户首次访问应用时，可直接从缓存中获取数据，这样就减少了从服务器重新下载资源的时间，提升了应用首开速度，从而提高用户留存率。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163632.47651895847873447686288485879411:50001231000000:2800:5BFC531EFDA42D06384C4FD073D5564F2D9A8AB2F36518A498D5AE13129969DD.png "点击放大")

### 实现节日主题即发即现

很多应用会在节日更换特定主题内容进行活动营销，用户打开应用时需要从服务器上获取相关资源来呈现内容，可能会造成页面加载速度较慢而导致用户体验不佳。开发者可以使用预加载，在节日活动开始前通过周期性的数据拉取提前将主题资源获取到本地，活动开始用户访问时直接从本地获取即可，减少了网络请求的时间和带宽消耗，从而能够更快地展示节日主题，实现即发即现的效果，提升用户体验。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163632.16663948318507250589677098590597:50001231000000:2800:315673536053B28066C813304D3FCD2A0A6CAC023931D58BC5462361D1703683.png "点击放大")

## 约束与限制

### 设备限制

支持Phone、Tablet设备。

### 数据限制

|限制项|说明|
|:--|:--|
|数据类型|仅支持缓存文本、图片、音频、视频等静态资源数据，不支持代码、脚本等动态资源数据。|

### 配额限制

|配额类型|配额|
|:--|:--|
|安装预加载缓存大小|2MB|
|周期性预加载缓存大小|3MB|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-service "预加载")
# 开发流程

更新时间: 2025-12-16 16:36

开发预加载，总体流程如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163646.93397315707055645053443967058550:50001231000000:2800:6F11D4DA6352FBE558D9B68758D1CF89A6288CB23B4E835FE0638C5220731D29.png "点击放大")

1. [配置预加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-config)：在AGC云端预加载界面选择数据来源类型，并进行相关配置。
2. [开发预加载资源接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-cloud-interdev)：根据选择的数据来源类型，开发对应的云侧接口，以提供预加载所需的资源数据。
3. [调用预加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-call)：在工程代码文件中调用预加载。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-overview "概述")
# 配置预加载

更新时间: 2025-12-16 16:36

安装预加载和周期性预加载需分别进行配置，且两者均可通过云函数和开发者服务器（即HTTPS请求）两种数据来源方式来实现。

对于不同类型的开发者，支持的数据来源方式有所不同：

- 个人开发者：数据来源默认选择云函数，且仅支持通过云函数来实现预加载。需要开通云函数服务并创建函数才可以配置。
- 非个人开发者：数据来源支持云函数和开发者服务器两种。可根据实际需要进行选择。

下文介绍如何配置两种数据来源方式的预加载实现。

说明

当前“开发者服务器”数据来源方式仅对外受限开放，如有需求，请发送邮件申请开通，华为方收到邮件后，将在1~3个工作日内安排对接人员并邮件回复。

邮件格式要求如下：

- 邮箱地址：[agconnect@huawei.com](mailto:agconnect@huawei.com)
- 邮件标题：【预加载】【申请开通开发者服务器权限】

- 邮件内容： 需包含Developer ID、项目ID、应用ID、预加载使用场景。其中，Developer ID等信息查询方法请参见[查看应用信息](https://developer.huawei.com/consumer/cn/doc/app/agc-help-view-app-info-0000002282674569)。

## 数据来源为云函数

### 前提条件

- 已[开通预加载服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-enable-prefetch)。
- 已[创建函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-create-and-config-function)。

### 绑定云函数

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，点击“开发与服务”。
2. 在项目列表中点击您的项目，在项目下的应用列表中选择需要配置预加载的HarmonyOS应用/元服务。
    
3. 在左侧导航栏选择“云开发（Serverless）> 预加载”，进入预加载页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163657.65749202131567523759978307256566:50001231000000:2800:EA52476E9F8A799D485EF4477738984DA3044B95ADB0F099F3851B773AFEB22C.png)
    
4. 根据实际需要，在“周期性预加载”或者“安装预加载”区域，“数据来源”选择“云函数”，然后点击“函数名称”后的“修改”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163657.89915507251807039581073515304612:50001231000000:2800:54B6BC798F6E467682E8F8B0D5C2686527B5085E0AE5E85F4E9A26865231AC79.png)
    
5. 以“周期性预加载”为例，在“函数名称”下拉框选择实现周期性预加载的函数名称。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163657.51662565549370028993955485509092:50001231000000:2800:D202F8DFE419A1A303470D5FF70F5914F6467BA079BA016966B3C9EF4157DD92.png)
    
6. 点击“保存”完成周期性预加载配置。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163657.70193315525806332911112700299275:50001231000000:2800:773B835551D2E8F12A3929340C4AB3752A364119C4B6CAC94418D3ECC2FE95EC.png)
    
7. 若配置“安装预加载”，重复步骤[4](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-config#zh-cn_topic_0000002166964980_zh-cn_topic_0000002131919472_li2842728132811)-[6](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-config#zh-cn_topic_0000002166964980_zh-cn_topic_0000002131919472_li17782763116)即可。
8. （可选）后续若需要修改绑定的云函数，点击“函数名称”后的“修改”更新即可。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163658.25593365603559138287838000347705:50001231000000:2800:304374E36D6939CD01BFDCF2372EFE499D9BAB7F1FF0C65CF0E90651311E5ACA.png)
    

## 数据来源为开发者服务器

### 前提条件

- 已申请开通开发者服务器权限。
- 已[开通预加载服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-enable-prefetch)。

### 配置服务器地址

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)，点击“开发与服务”。
2. 在项目列表中点击您的项目，在项目下的应用列表中选择需要配置预加载的HarmonyOS应用/元服务。
    
3. 在左侧导航栏选择“云开发（Serverless）> 预加载”，进入预加载页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163658.23636862684209782429641190230693:50001231000000:2800:BF10779565B0E35C62096ACCC662854933E2D2E092D71046D53C7843D1A5DFB5.png)
    
4. 在“周期性预加载”或者“安装预加载”区域，“数据来源”选择“开发者服务器”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163658.56941253774875398619433544869265:50001231000000:2800:43FAF5831F5B1D0AD0A9C562B34E4FC0AFBD517A0E8E5F6E8B9CDC788144634E.png)
    
5. 点击“下载地址”后的“修改”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163658.65580181115431384018201906189462:50001231000000:2800:972166AEB9C42C0AABD8637ED1660D1E738672979D83A08755FFEFF42068CB6C.png)
    
6. 以“周期性预加载”为例，“下载地址”以“https://”开头，输入框中输入服务器地址，配置完成后点击“保存”。
    
    需要注意以下几点：
    
    - 仅支持填写一个服务器地址，需包含预加载资源接口路径，如图中示例：prefetchData。
    - 域名：须填写完整的域名。例如www.example.com，不可写为example.com。
    
    - IP地址：须填写准确的IP地址，确保没有输入错误。
    - 端口号：如果要指定端口号，可在服务器地址后面以冒号分隔，例如https://www.example.com:443。HTTPS协议的默认端口号（443）可以省略。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163658.63794301710952772327038481328981:50001231000000:2800:AD7BEAE33EE5173A7D9A97CAD74BEDD67BB87B2AF21261BFF472502BA394EA33.png)
    
    后续AGC会周期性地向该处配置的开发者服务器（即下载地址）发起一个HTTP GET请求，其中包含的query参数请参考[开发者服务器接口规范](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-cloud-interdev#section83701164150)，获取到数据后会将整个HTTP body缓存在本地。
    
    说明
    
    - 开发者服务器接口返回的数据内容需仅包含文本、图片、视频、音频等供页面展示的静态资源，不支持包含代码、脚本等动态数据。
    - 开发者服务器接口返回的数据类型为其自定义格式的JSON或字符串数据，大小需限定在3MB以内。
    
7. 若配置“安装预加载”，重复步骤[4](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-config#zh-cn_topic_0000002166964980_zh-cn_topic_0000002131919472_li36291744112217)-[6](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-config#zh-cn_topic_0000002166964980_zh-cn_topic_0000002131919472_li41341137143420)即可。
8. （可选）后续若需要修改下载地址，点击“下载地址”后的“修改”更新即可。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163658.35868283346681130927367234704314:50001231000000:2800:96EBC56C3168203255CBE77FD805B44D93112D75ACB8322DFC86C6439A9D5D15.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-devprocess "开发流程")
# 开发预加载资源接口

更新时间: 2025-12-16 16:37

使用预加载服务之前，开发者需要完成云侧接口的开发，以提供预加载所需的资源数据。华为提供两种方式供开发者选择：云函数和开发者服务器，开发者可根据实际业务需要进行选择。

## 云函数

开发者需要先按照云函数接口规范开发函数，然后在AGC云端创建函数，并可测试函数运行是否正常。流程如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163709.55716190059092552623827537735114:50001231000000:2800:18B39512123D98B42AB1916FBD3BAD25ED3F955ED2D2AD3C8CA9AFEE35D8C67A.png "点击放大")

1. [开发函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-develop-function)：按照云函数接口规范开发函数。
2. [创建函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-create-and-config-function)：函数业务代码开发完成后，即可在AGC云端创建函数。
3. [测试函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-test-function)：对函数进行测试，以确保函数代码运行正常。

### 云函数接口规范

|API名称|说明|参数|   |返回值|
|:--|:--|:--|:--|:--|
|自定义|获取预加载数据接口|- 安装预加载：<br>    <br>    event.body.appId：应用ID，获取方法请参见[查看应用信息](https://developer.huawei.com/consumer/cn/doc/app/agc-help-view-app-info-0000002282674569)。<br>    <br>- 周期性预加载<br>    - event.body.appId：应用ID。<br>    - event.body.token：可选，注册周期性预加载任务时开发者自行传入的用户级认证信息，长度不超过2048个字符。<br>    - event.body.params：可选，注册周期性预加载任务时开发者自行传入的自定义参数，长度不超过1024个字符。|   |自定义JSON字符串|

### 示例

[端云一体化工程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-devprocess)预加载云函数示例如下。其中，axios依赖库为网络请求库，需要在“cloudfunctions/云函数名称/package.json”的“dependencies”中添加axios的1.7.7或以上版本依赖。

- 安装预加载
    
    1. import axios from 'axios';
    
    2. let myHandler = async function (event, context, callback, logger) {
    3.   logger.info("event:" + JSON.stringify(event));
    4.   let env1 = context.env.env1; // 环境变量
    5.   logger.info("env1: " + env1)
    6.   try {
    7.     let body = event.body ? JSON.parse(event.body) : event;
    8.     let appId = body.appId;
    
    9.     logger.info("appId: " + appId);
    
    10.     // http请求示例，请按照实际业务修改
    11.     let url = 'https://example.com/prefetchApi';  // 页面资源数据的请求url
    12.     let headers = { 'k1': 'v1' };  // 请求header
    13.     let res;  // 返回数据
    14.     await axios.post(url, {}, { headers })  // http post请求
    15.       .then(response => {
    16.         res = response.data;
    17.       })
    18.     logger.info("--------Finished-------");
    19.     callback(res);
    20.   } catch (error) {
    21.     logger.error("--------Error-------");
    22.     logger.error("error: " + error);
    23.     callback(error);
    24.   }
    25. };
    
    26. export { myHandler };
    
- 周期性预加载
    
    1. import axios from 'axios';
    
    2. let myHandler = async function (event, context, callback, logger) {
    3.   logger.info("event:" + JSON.stringify(event));
    4.   let env1 = context.env.env1; // 环境变量
    5.   logger.info("env1: " + env1)
    6.   try {
    7.     let body = event.body ? JSON.parse(event.body) : event;
    8.     let appId = body.appId;
    9.     let token = body.token;
    10.     let paramsStr = body.params; // 如果需要解析json结构paramsStr中的参数，需要使用 let params = JSON.parse(paramsStr);
    
    11.     logger.info("appId: " + appId + ",token:" + token + ",params:" + paramsStr);
    
    12.     // http请求示例，请按照实际业务修改
    13.     let url = 'https://example.com/prefetchApi';  // 页面资源数据的请求url
    14.     let headers = { 'k1': 'v1' };  // 请求header
    15.     let res;  // 返回数据
    16.     await axios.post(url, {}, { headers })  // http post请求
    17.       .then(response => {
    18.         res = response.data;
    19.       })
    20.     logger.info("--------Finished-------");
    21.     callback(res);
    22.   } catch (error) {
    23.     logger.error("--------Error-------");
    24.     logger.error("error: " + error);
    25.     callback(error);
    26.   }
    27. };
    
    28. export { myHandler };
    

## 开发者服务器

申请开通开发者服务器权限之后，开发者使用自己的服务器自行开发和实现预加载资源接口，接口需遵循开发者服务器接口规范。

### 开发者服务器接口规范

|API/PATH名称|说明|参数|   |请求方式|返回值|
|:--|:--|:--|:--|:--|:--|
|自定义|获取预加载数据接口|- 安装预加载<br>    <br>    appId：应用ID，获取方法请参见[查看应用信息](https://developer.huawei.com/consumer/cn/doc/app/agc-help-view-app-info-0000002282674569)。<br>    <br>- 周期性预加载<br>    - appId：应用ID。<br>    - token：可选，注册周期性预加载任务时开发者自行传入的用户级认证信息，长度不超过2048个字符。<br>    - params：可选，注册周期性预加载任务时开发者自行传入的自定义参数，长度不超过1024个字符。|   |GET|自定义JSON字符串|

### 示例

定义名称为prefetchData的接口，示例如下：

1. https://www.example.com/prefetchData?appId=1234&token=xxxx&params=yyyy

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-config "配置预加载")
# 预加载工具类

更新时间: 2025-12-16 16:38

在“entry/src/main/ets/common”目录下新增GlobalContext.ets和PreferenceUtil.ets。

## GlobalContext

全局上下文类，提供全局上下文句柄的初始化和获取功能。参考示例如下：

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

## PreferenceUtil

首选项工具类，提供数据读取和存储功能。参考示例如下：

1. import dataPreferences from '@ohos.data.preferences';
2. import { Context } from '@kit.AbilityKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';

4. const DOMAIN = 0x0000;
5. const TAG = 'PreferenceUtil';
6. const DEFAULT_STORE_NAME: string = "prefetchDefaultStore";

7. export class PreferenceUtil {
8.   private static cachedPreferences: Map<string, dataPreferences.Preferences> = new Map();

9.   private constructor() {
10.   }

11.   public static async getValue(context: Context, storeName: string,
12.     key: string): Promise<dataPreferences.ValueType | null> {
13.     try {
14.       let store = await PreferenceUtil.getStore(context, storeName);
15.       PreferenceUtil.updateStoreCache(storeName, store);
16.       const result = await store.get(key, '');    
17.       return result;
18.     } catch (err) {
19.       hilog.error(DOMAIN, TAG,
20.         `getValue from ${storeName} error, key:${key}, err:${err.message}`);
21.       return null;
22.     }
23.   }

24.   public static getValueSync(context: Context, storeName: string, key: string): dataPreferences.ValueType | null {
25.     try {
26.       let store = PreferenceUtil.getStoreSync(context, storeName);
27.       PreferenceUtil.updateStoreCache(storeName, store);
28.       const result = store.getSync(key, '');
29.       return result;
30.     } catch (err) {
31.       hilog.error(DOMAIN, TAG,
32.         `getValueSync from ${storeName} error, key:${key}, err:${err.message}`);
33.       return null;
34.     }
35.   }

36.   public static async setValue(context: Context, storeName: string, key: string,
37.     value: dataPreferences.ValueType): Promise<void> {
38.     try {      
39.       let store = await PreferenceUtil.getStore(context, storeName);
40.       PreferenceUtil.updateStoreCache(storeName, store);
41.       await store.put(key, value);
42.       await store.flush();
43.     } catch (err) {
44.       hilog.error(DOMAIN, TAG, `putValue from ${storeName} error, key:${key}, err:${err.message}`);
45.     }
46.   }

47.   private static async getStore(context: Context, storeName: string): Promise<dataPreferences.Preferences> {
48.     let actualStoreName = !storeName ? DEFAULT_STORE_NAME : storeName;
49.     let store = PreferenceUtil.cachedPreferences.get(actualStoreName);
50.     if (store) {
51.       return store;
52.     }
53.     hilog.info(DOMAIN, TAG, `there is no cached store:${actualStoreName}, begin to get one`);
54.     return dataPreferences.getPreferences(context, actualStoreName);
55.   }

56.   private static getStoreSync(context: Context, storeName: string): dataPreferences.Preferences {
57.     let actualStoreName = !storeName ? DEFAULT_STORE_NAME : storeName;
58.     let store = PreferenceUtil.cachedPreferences.get(actualStoreName);
59.     if (store) {
60.       return store;
61.     }
62.     hilog.info(DOMAIN, TAG, `getStoreSync there is no cached store:${actualStoreName}, begin to get one`);
63.     return dataPreferences.getPreferencesSync(context, { name: actualStoreName });
64.   }

65.   private static updateStoreCache(storeName: string, store: dataPreferences.Preferences): void {
66.     if (!PreferenceUtil.cachedPreferences.has(storeName)) {
67.       PreferenceUtil.cachedPreferences.set(storeName, store);
68.     }
69.   }
70. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-add-dependency-class "添加预加载依赖类")
# 预加载实现类

更新时间: 2025-12-16 16:38

在“entry/src/main/ets/prefetchUtil”目录下新增PrefetchUtil.ets和PrefetchWrapper.ets。

PrefetchUtil和PrefetchWrapper实现类功能如下：

- PrefetchUtil：预加载API的封装类，为PrefetchWrapper提供预加载API封装接口。
    - 提供安装预加载的数据获取接口
    - 提供周期性预加载的任务注册接口和数据获取接口
    - 提供周期性预加载是否已拉取数据的判断接口
- PrefetchWrapper：预加载包装类，为页面提供预加载封装接口。
    - 提供安装预加载数据获取和渲染接口
    - 提供周期性预加载数据获取和渲染接口
    - 提供安装预加载和周期性预加载数据获取和渲染接口

## PrefetchUtil

周期性预加载任务注册间隔需要大于12小时，建议按照如下示例取值为24小时。

1. import { cloudResPrefetch } from '@kit.CloudFoundationKit'
2. import { hilog } from '@kit.PerformanceAnalysisKit';
3. import { PreferenceUtil } from '../common/PreferenceUtil';
4. import { GlobalContext } from '../common/GlobalContext';

5. const PREFERENCES_PREFETCH_STORE_NAME = 'defaultStore';
6. const PREFERENCES_PREFETCH_FIRST_REGISTER_TIME = 'prefetchTaskFirstRegisterTime'; // 首次注册时间
7. const PREFERENCES_PREFETCH_TASK_EXPIRE_TIME = 'prefetchTaskExpireTime'; // 任务过期时间
8. const PREFETCH_TASK_REGISTER_INTERVAL = 24 * 60 * 60 * 1000; // 24h < 72h
9. const PREFETCH_DATA_UPDATE_INTERVAL = 12 * 60 * 60 * 1000; // 12h
10. const HILOG_DOMAIN = 0x0000;
11. const TAG = 'Prefetch';

12. export class PrefetchUtil {
13.   private static timeoutId: number = (0 - Number.MAX_VALUE);
14.   private static hasPrefetchedData: boolean = false;
15.   private static isPrefetchTaskRegistered: boolean = false;
16.   private static now: number = (0 - Number.MAX_VALUE);

17.   private constructor() {
18.   }

19.   /**
20.    * 预加载数据获取
21.    * @param type 安装预加载/周期预加载数据
22.    * @throws 预加载getPrefetchResult API异常
23.    * @returns PrefetchResult
24.    */
25.   public static async getPrefetchResult(type: cloudResPrefetch.PrefetchMode) {
26.     return cloudResPrefetch.getPrefetchResult(type);
27.   }

28.   /**
29.    * 周期性预加载应用注册任务，间隔24h
30.    * @param token 应用/用户级token，可以取空
31.    * @param params 自定义筛选参数，定义为json格式，可以取空
32.    * @param forceRegister 是否强制注册
33.    */
34.   public static async registerPrefetchTask(token: string, params: string | object,
35.     forceRegister: boolean = false) {
36.     await PrefetchUtil.updatePrefetchTaskInfo();
37.     if (!forceRegister) {
38.       await PrefetchUtil.registerPrefetchTaskNotForced(token, params);
39.       return;
40.     }
41.     await PrefetchUtil.registerPrefetchTaskForced(token, params);
42.   }

43.   /**
44.    * 是否有周期性预加载数据：首次注册12h后才有周期性预加载数据
45.    * @returns boolean
46.    */
47.   public static hasPrefetchTaskData() : boolean {
48.     return PrefetchUtil.hasPrefetchedData;
49.   }

50.   private static async updatePrefetchTaskInfo() {
51.     PrefetchUtil.now = Date.now();
52.     if (PrefetchUtil.timeoutId != 0 - Number.MAX_VALUE) {
53.       clearTimeout(PrefetchUtil.timeoutId);
54.     }
55.     let firstRegisterTime = await PreferenceUtil.getValue(GlobalContext.getContext(), PREFERENCES_PREFETCH_STORE_NAME,
56.       PREFERENCES_PREFETCH_FIRST_REGISTER_TIME) as number;
57.     if (firstRegisterTime) {
58.       PrefetchUtil.isPrefetchTaskRegistered = true;
59.       // 判断任务是否已获取数据(首次注册后12h，之后数据每隔12h更新一次)
60.       if (PrefetchUtil.now - firstRegisterTime >= PREFETCH_DATA_UPDATE_INTERVAL) {
61.         PrefetchUtil.hasPrefetchedData = true;
62.       }
63.     }
64.     if (!PrefetchUtil.isPrefetchTaskRegistered) {
65.       hilog.info(HILOG_DOMAIN, TAG, `first register time: ${PrefetchUtil.now}`);
66.       await PreferenceUtil.setValue(GlobalContext.getContext(), PREFERENCES_PREFETCH_STORE_NAME,
67.         PREFERENCES_PREFETCH_FIRST_REGISTER_TIME, PrefetchUtil.now);
68.     }
69.   }

70.   private static async registerPrefetchTaskForced(token: string, params: string | object) {
71.     // 过期或强制更新任务注册
72.     let expireTime = PrefetchUtil.now + PREFETCH_TASK_REGISTER_INTERVAL;
73.     hilog.info(HILOG_DOMAIN, TAG, `new expireTime: ${expireTime}`);
74.     await PreferenceUtil.setValue(GlobalContext.getContext(), PREFERENCES_PREFETCH_STORE_NAME,
75.       PREFERENCES_PREFETCH_TASK_EXPIRE_TIME, expireTime);
76.     // 更新任务注册和定时器
77.     PrefetchUtil.registerPrefetchTaskWithApi(token, params);
78.     PrefetchUtil.updateTaskTimer(PREFETCH_TASK_REGISTER_INTERVAL);
79.   }

80.   private static async registerPrefetchTaskNotForced(token: string, params: string | object) {
81.     // 判断任务到期，重新注册
82.     let expireTime = await PreferenceUtil.getValue(GlobalContext.getContext(), PREFERENCES_PREFETCH_STORE_NAME,
83.       PREFERENCES_PREFETCH_TASK_EXPIRE_TIME) as number;
84.     if (expireTime && (PrefetchUtil.now < expireTime)) {
85.       // 任务没有过期：只更新定时器
86.       let delay = expireTime - PrefetchUtil.now;
87.       hilog.info(HILOG_DOMAIN, TAG, `not expire, delay:${delay}`);
88.       PrefetchUtil.updateTaskTimer(delay);
89.       return;
90.     }
91.     await PrefetchUtil.registerPrefetchTaskForced(token, params);
92.   }

93.   private static registerPrefetchTaskWithApi(token: string, params: string | object) {
94.     try {
95.       cloudResPrefetch.registerPrefetchTask({
96.         token: token,
97.         params: params
98.       });
99.       hilog.info(HILOG_DOMAIN, TAG, `register success`);
100.     } catch (error) {
101.       hilog.error(HILOG_DOMAIN, TAG, `register catch = ${error.message}`);
102.     }
103.   }

104.   private static updateTaskTimer(delay: number) {
105.     PrefetchUtil.timeoutId = setTimeout(() => {
106.       if (PrefetchUtil.timeoutId != (0 - Number.MAX_VALUE)) {
107.         clearInterval(PrefetchUtil.timeoutId)
108.         PrefetchUtil.timeoutId = (0 - Number.MAX_VALUE);
109.       }
110.     }, delay);
111.   }
112. }

## PrefetchWrapper

- 预加载数据获取成功时，需要增加页面的渲染逻辑。
- 预加载数据获取失败时，需要做数据降级处理。如下示例代码以cloudFunctionCall接口触发云函数为例获取数据，请根据实际业务实现进行修改。
    
    说明
    
    - 使用cloudFunctionCall接口之前，请先[设置云函数配置项](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-call-function#section197479161807)。
    - 测试周期性预加载时，需要将下文示例代码periodicPrefetch方法中的如下代码块注释。若不注释，则需等待12h才能获取周期性预加载数据。
        
        1. if (!PrefetchUtil.hasPrefetchTaskData()) { // 是否有周期性预加载数据：首次注册12h后才有周期性预加载数据
        2.   hilog.info(HILOG_DOMAIN, TAG, 'not has prefetch data');
        3.   this.cloudFunctionCall(); // 使用普通方式获取应用数据
        4.   return;
        5. }
        
        测试完成后，取消上述代码块注释即可。
        
    

1. import { hilog } from '@kit.PerformanceAnalysisKit';
2. import { cloudFunction, cloudResPrefetch } from '@kit.CloudFoundationKit';
3. import { PrefetchUtil } from './PrefetchUtil';
4. import { PreferenceUtil } from '../common/PreferenceUtil';
5. import { BusinessError } from '@kit.BasicServicesKit';
6. import { GlobalContext } from '../common/GlobalContext';

7. const HILOG_DOMAIN = 0x0000;
8. const TAG = 'PrefetchWrapper';
9. const PREFETCH_MODE = "prefetchMode";
10. const PREFERENCES_PREFETCH_STORE_NAME = 'defaultStore';

11. export class PrefetchWrapper {
12.   private static instance: PrefetchWrapper;

13.   private constructor() {
14.   }

15.   public static getInstance(): PrefetchWrapper {
16.     if (!PrefetchWrapper.instance) {
17.       PrefetchWrapper.instance = new PrefetchWrapper();
18.     }
19.     return PrefetchWrapper.instance;
20.   }

21.   // 支持安装预加载和周期性预加载（推荐）
22.   public doPrefetch() {
23.     let context = GlobalContext.getContext();
24.     let prefetchMode =
25.       PreferenceUtil.getValueSync(context, PREFERENCES_PREFETCH_STORE_NAME, PREFETCH_MODE) as number;
26.     if (!prefetchMode) {
27.       // 应用安装后首次打开：使用安装预加载
28.       hilog.info(HILOG_DOMAIN, TAG, 'installPrefetch');
29.       this.installPrefetch();
30.       PreferenceUtil.setValue(context, PREFERENCES_PREFETCH_STORE_NAME, PREFETCH_MODE,
31.         cloudResPrefetch.PrefetchMode.PERIODIC_PREFETCH);
32.     } else {
33.       // 应用安装后非首次打开：使用周期性预加载
34.       hilog.info(HILOG_DOMAIN, TAG, 'periodicPrefetch: %{public}d', prefetchMode);
35.       this.periodicPrefetch();
36.     }
37.   }

38.   // 仅支持安装预加载
39.   public doInstallPrefetch() {
40.     let context = GlobalContext.getContext();
41.     let prefetchMode =
42.       PreferenceUtil.getValueSync(context, PREFERENCES_PREFETCH_STORE_NAME, PREFETCH_MODE) as number;
43.     if (!prefetchMode) {
44.       // 应用安装后首次打开：使用安装预加载
45.       hilog.info(HILOG_DOMAIN, TAG, 'installPrefetch');
46.       this.installPrefetch();
47.       PreferenceUtil.setValue(context, PREFERENCES_PREFETCH_STORE_NAME, PREFETCH_MODE,
48.         cloudResPrefetch.PrefetchMode.PERIODIC_PREFETCH);
49.     }
50.   }

51.   // 仅支持周期性预加载
52.   public doPeriodicPrefetch() {
53.     let context = GlobalContext.getContext();
54.     let prefetchMode =
55.       PreferenceUtil.getValueSync(context, PREFERENCES_PREFETCH_STORE_NAME, PREFETCH_MODE) as number;
56.     if (!prefetchMode) {
57.       PreferenceUtil.setValue(context, PREFERENCES_PREFETCH_STORE_NAME, PREFETCH_MODE,
58.         cloudResPrefetch.PrefetchMode.PERIODIC_PREFETCH);
59.     } else {
60.       // 应用安装后非首次打开：使用周期性预加载
61.       hilog.info(HILOG_DOMAIN, TAG, 'periodicPrefetch: %{public}d', prefetchMode);
62.       this.periodicPrefetch();
63.     }
64.   }

65.   private installPrefetch() {
66.     PrefetchUtil.getPrefetchResult(cloudResPrefetch.PrefetchMode.INSTALL_PREFETCH)
67.       .then((data: cloudResPrefetch.PrefetchResult) => { // 接口调用成功处理缓存的应用数据
68.         hilog.info(HILOG_DOMAIN, TAG, 'get install prefetch cache successfully');
69.         let dataResult = data.result; // data.result即是缓存的应用数据
70.         // todo 处理dataResult
71.         hilog.info(HILOG_DOMAIN, TAG, 'get install prefetch dataResult: %{public}s', JSON.stringify(dataResult));
72.       })
73.       .catch((err: BusinessError) => {
74.         hilog.error(HILOG_DOMAIN, TAG, `get install prefetch cache failed: ${err.message}, ${err.code}`);
75.         this.cloudFunctionCall(); // 应用走原有逻辑获取数据，示例使用云函数获取
76.       })
77.   }

78.   private initPeriodPrefetch() {
79.     let token = ''; // 应用自定义token参数，一般是鉴权参数，云侧云函数开发时提取鉴权，不鉴权，可以为空
80.     let params = ''; // 应用自定义params参数，一般是筛选参数，可以定义成json格式，云侧云函数开发是提取进行筛选，不需要，可以为空
81.     PrefetchUtil.registerPrefetchTask(token, params);
82.   }

83.   private periodicPrefetch() {
84.     this.initPeriodPrefetch();
85.     if (!PrefetchUtil.hasPrefetchTaskData()) { // 是否有周期性预加载数据：首次注册12h后才有周期性预加载数据
86.       hilog.info(HILOG_DOMAIN, TAG, 'not has prefetch data');
87.       this.cloudFunctionCall(); // 使用普通方式获取应用数据
88.       return;
89.     }
90.     PrefetchUtil.getPrefetchResult(cloudResPrefetch.PrefetchMode.PERIODIC_PREFETCH)
91.       .then((data: cloudResPrefetch.PrefetchResult) => { // 接口调用成功处理缓存的应用数据
92.         hilog.info(HILOG_DOMAIN, TAG, 'get periodic prefetch cache successfully');
93.         let dataResult = data.result; // data.result即是缓存的应用数据
94.         let timestamp = data.timestamp; // data.timestamp即是缓存拉取时间
95.         let token = data.token; // data.token即是注册任务token
96.         // todo 处理dataResult
97.         hilog.info(HILOG_DOMAIN, TAG, 'get periodic prefetch dataResult: %{public}s', JSON.stringify(dataResult));
98.         hilog.info(HILOG_DOMAIN, TAG, 'get periodic prefetch timestamp: %{public}s', timestamp.toString());
99.         hilog.info(HILOG_DOMAIN, TAG, 'get periodic prefetch token: %{public}s', token)
100.       })
101.       .catch((err: BusinessError) => {
102.         hilog.error(HILOG_DOMAIN, TAG, `get periodic prefetch cache failed: ${err.message}, ${err.code}`);
103.         this.cloudFunctionCall(); // 应用走原有逻辑获取数据，示例使用云函数获取
104.       })
105.   }

106.   private cloudFunctionCall() {
107.     hilog.info(HILOG_DOMAIN, TAG, 'cloudFunctionCall start');
108.     cloudFunction.call({
109.       name: "function_name",  // 需修改为实际的云函数名称
110.       timeout: 5 * 1000
111.     }).then((data: cloudFunction.FunctionResult) => {
112.       hilog.info(HILOG_DOMAIN, TAG, 'call function successfully');
113.       let dataResult = data.result; // data.result即是缓存的应用数据
114.       // todo 处理dataResult
115.       hilog.info(HILOG_DOMAIN, TAG, 'call function get: %{public}s', JSON.stringify(dataResult));
116.     }).catch((err: BusinessError) => {
117.       hilog.error(HILOG_DOMAIN, TAG, 'call function failed: %{public}s', err.message);
118.     })
119.   }
120. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-tool-class "预加载工具类")
# 调用安装预加载

更新时间: 2025-12-16 16:37

在项目的EntryAbility.ets文件中导入预加载实现类[PrefetchWrapper](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-implementation-class#section1192871813236)，并在onCreate中调用PrefetchWrapper的doInstallPrefetch方法。方法内部会调用[getPrefetchResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudresprefetch#section181501852703)获取安装预加载缓存数据。

说明

- 安装预加载缓存数据，仅允许调用一次，被调用后将被销毁。
- 应用安装开始时，系统会拉取安装预加载云侧数据并缓存到本地。

1. import { GlobalContext } from '../common/GlobalContext';
2. import { PrefetchWrapper } from '../prefetchUtil/PrefetchWrapper';

3. onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
4.   GlobalContext.initContext(this.context); // 初始化全局上下文
5.   PrefetchWrapper.getInstance().doInstallPrefetch();
6. }

说明

调用安装预加载过程中，可参考[FAQ](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-faq-prefetch)定位预加载问题。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-implementation-class "预加载实现类")
# 调用周期性预加载

更新时间: 2025-12-16 16:38

在项目的EntryAbility.ets文件中导入预加载实现类[PrefetchWrapper](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-implementation-class#section1192871813236)，并在onCreate中调用PrefetchWrapper的doPeriodicPrefetch方法。方法内部会先调用[registerPrefetchTask](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudresprefetch#section251833512544)方法注册周期性预加载任务，12小时后将调用[getPrefetchResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudresprefetch#section181501852703)获取周期性预加载数据。

说明

- 系统会结合应用活跃情况进行任务清理。应用不活跃后，如果当前时间 – 任务注册时间 > 72小时，则任务将直接从队列移除。移除任务时不立即清理已加载的数据，数据会被定期清理，应用启动时仍然可尝试获取此前已加载的缓存数据，并结合数据时间戳决定是否呈现内容。
- 获取周期性预加载数据的间隔周期是12小时，如果打开应用的时间间隔低于12小时，可能将无法获取到最新的预加载数据。
- 由于系统每隔12小时才会拉取一次周期性预加载数据，不方便调试周期性预加载功能，为此，系统提供了[命令行工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-debugging)，可以实时拉取周期性预加载数据。

1. import { GlobalContext } from '../common/GlobalContext';
2. import { PrefetchWrapper } from '../prefetchUtil/PrefetchWrapper';

3. onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
4.   GlobalContext.initContext(this.context);  // 初始化全局上下文
5.   PrefetchWrapper.getInstance().doPeriodicPrefetch();
6. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-call-installprefetch "调用安装预加载")
# 调用安装预加载和周期性预加载

更新时间: 2025-12-16 16:38

在项目的EntryAbility.ets文件中导入预加载实现类[PrefetchWrapper](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-implementation-class#section1192871813236)，并在onCreate中调用PrefetchWrapper的doPrefetch方法。在应用安装后首次打开时调用安装预加载，非首次打开时调用周期性预加载。

1. import { GlobalContext } from '../common/GlobalContext';
2. import { PrefetchWrapper } from '../prefetchUtil/PrefetchWrapper';

3. onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
4.   GlobalContext.initContext(this.context);  // 初始化全局上下文
5.   PrefetchWrapper.getInstance().doPrefetch();
6. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-call-periodicprefetch "调用周期性预加载")
# 调试周期性预加载

更新时间: 2025-12-16 16:37

prefetch_test_tool是为周期性预加载功能提供的一种命令行工具，开发者集成预加载服务后，使用该工具可以更方便、更高效地进行周期性预加载功能测试和调试，提高开发效率，同时确保预加载服务的平稳运行。

当前命令行工具支持的命令集如下：

|命令名|描述|
|:--|:--|
|[getcache](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-commandtool-debug#section1348600182818)|提供获取周期性预加载数据的能力。|

## 调试准备

使用命令行工具调试周期性预加载之前，需要完成以下准备工作：

- 您已在开发者联盟官网注册账号并通过实名认证，详情请参见[账号注册认证](https://developer.huawei.com/consumer/cn/doc/start/registration-and-verification-0000001053628148)。
- 您已在本地安装DevEco Studio 5.0.3 Release及以上版本。
- 手机/平板终端设备的ROM版本已升级至HarmonyOS 6.0.0 Beta5及以上版本。
- 设置HAP包的“Build Mode”为“debug”，且已[申请调试证书](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-debugcert-0000001914263178)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163748.38553671631929556830450031537869:50001231000000:2800:2CF8925FCC5D69700696A833B13F64D89AA511B86005FC8CA117E742A4F14D80.png)
    

## 切换shell环境

prefetch_test_tool命令行工具基于hdc shell调试，需要切换到hdc shell命令环境。

1. PC连接调试设备。连接方式请根据实际情况选择，详情请参见[设备连接管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hdc#%E8%AE%BE%E5%A4%87%E8%BF%9E%E6%8E%A5%E7%AE%A1%E7%90%86)。
2. 打开DevEco Studio，菜单栏选择“View > Tool Windows > Terminal”进入Terminal窗口。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163748.78731783779492336027391678633666:50001231000000:2800:7A805E7E8CCB9742DB84329FC628648D59A199488EA392EE7E9499803C8FCD01.png)
    
3. 输入hdc shell，切换到hdc shell命令环境。切换过程中如果出现报错，请参见[常见问题](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hdc#%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)排查解决。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163748.59501987872083090879240308983888:50001231000000:2800:BADC9C2E9A97032AA068F238BB81B0AD9501E0A586BB2F15B75C18F2CC2C1CE1.png)
    

## 调试命令

命令名“getcache”，提供获取周期性预加载数据的能力。

### 命令格式

1. cf_prefetch getcache -m <bundlename>

### 命令选项

|命令选项|必填(M)/选填(O)|描述|示例|
|:--|:--|:--|:--|
|-m|M|应用包名。此处的包名需要与您在AppGallery Connect中创建应用时配置的包名保持一致。|cf_prefetch getcache -m com.huawei.hms.xs.test|

## 调用示例

### 正常场景

- 输入cf_prefetch help，获取命令行工具的使用说明。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163748.75256114350666095578553224948381:50001231000000:2800:E9365CFBD7D283E73ABB57E94B7848D91C53BABBE746E6F5FB042413EEEDD175.png)
    
- 输入cf_prefetch getcache -h，获取getcache命令支持的参数信息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163749.43842707877150011146315058293722:50001231000000:2800:FEFA70995A770B6B3CED47996AAE437503812CB988B6EF72CF86F2992AB970CF.png)
    
- 输入cf_prefetch getcache -m <bundlename>，立即向云侧请求获取一次周期性预加载数据。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163749.94885995985230341937064578354238:50001231000000:2800:917912E119E81162ED17DC018C5E75D332B93AE4152508B490FD41E73AAB783B.png)
    
    说明
    
    如果返回结果中的“fetch data timestamp”不是当前时间，则表示仍为上一次成功拉取数据的时间戳，此次数据拉取失败，请参见[异常场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-commandtool-debug#section990573323613)排查。
    

### 异常场景

- 链路不通，例如无网络情况；或周期性预加载配置不正确。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163749.55978826771808853100810778975627:50001231000000:2800:CD53CEDBCF8DC04AF8B2A90974A195894898C731D932EB542DB84F35D816ABA6.png)
    
- 命令行工具内部错误。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163749.08781390820907388883198076113046:50001231000000:2800:568F800AE8E86FF7644A234713F51CFC42454547221F507FCEAF59C309D7529A.png)
    
- HAP包非debug调试模式。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163749.11715322781555622656314125625037:50001231000000:2800:DC7C8F90E29BE7A80938A219A93B5386D1245A122B6ABDDCD091A1C946A5815B.png)
    
- 应用包名输入错误。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163749.57869832800727538376121359226908:50001231000000:2800:51A154BBCABAB9052AF22967CA6C3094934A2BEB7DBFE851E12EC419D1083C0B.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-debugging "（可选）使用命令行工具调试周期性预加载")
# 错误码

更新时间: 2025-12-16 16:37

|错误码|描述|解决方法|
|:--|:--|:--|
|1008200005|周期性预加载执行失败。|请从以下方面进行排查：<br><br>- 检查设备网络连接情况。<br>- 确保周期性预加载配置正确。若配置不正确，请参考[配置预加载](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-config)重新配置。<br>- 确保云函数数据存储到中国境内（不包含中国香港、中国澳门、中国台湾）。|
|1008200009|命令行工具内部错误。|请通过[在线工单系统](https://developer.huawei.com/consumer/cn/support/feedback/#/add/101704353566310877?level2=101704353626565886&level3=101723605535783370&keyWord=Cloud%20Foundation%20Kit&channel=ICS0000)联系技术支持人员定位问题。|
|1008240000|HAP包不在debug模式下。|请确保HAP包的“Build Mode”设置为“debug”，且已申请调试证书。|
|1008240007|无法获取当前HAP包信息，例如APP ID等。|请检查应用包名合法性，输入正确的应用包名。|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-commandtool-debug "调试周期性预加载")
# 使用模拟器调试

更新时间: 2025-12-16 16:36

使用模拟器调试时，需在AGC云侧注册调试凭据，以保护应用/元服务对Cloud Foundation Kit的访问。在模拟器中启动应用/元服务时，开发者触发一次云函数、云数据库或云存储业务接口，该模拟器下会生成调试凭据并输出到日志；将生成的调试凭据注册到AGC云侧，即可在模拟器中调试应用/元服务。

具体可按如下步骤操作：

1. 获取调试凭据。
    1. 创建并启动模拟器，具体请参见[管理模拟器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-management)。
    2. 在模拟器中启动应用，并触发任意一次云函数、云数据库或云存储业务接口（建议使用云函数接口）。此时，由于未注册调试凭据，接口调用会失败，请忽略，继续执行下一步。
    3. 通过设置“No filters”模式、过滤“clouddevelopproxy.debugToken”关键字，查找日志中打印的调试凭据，并复制该调试凭据。
        
        格式示例：[clouddevelopproxy.debugToken=_xxx_]，其中“_xxx_”为调试凭据。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163624.36572482575018022776260352139793:50001231000000:2800:428505C0BA4403FEDFC68117411403A5F872E25232A4C099117CF02BB020474C.png)
        
2. 将获取的调试凭据注册到AGC云侧，具体可参见[注册模拟器调试凭据](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-credential-0000002415343501)。
3. 调试凭据注册成功后，您即可使用模拟器调试应用/元服务。关于模拟器使用指导，请参见[使用模拟器运行应用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-run-emulator)。
    
    如调用接口时返回的错误信息提示401签名校验失败或者403鉴权失败，可能原因如下：
    
    - 调试凭据未注册。请先[注册模拟器调试凭据](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-credential-0000002415343501)。
    - 注册调试凭据时绑定了错误的应用/元服务。请先删除该调试凭据，重新绑定正确的应用/元服务，等待30分钟后再进行调试。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-commandtool-errorcode "错误码")
# 如何通过应用侧日志定位预加载问题

更新时间: 2025-12-16 16:37

预加载的日志进程为“clouddevelopproxy”，日志过滤选择“No filters”。

下文列举几种场景下的日志提示信息：

- 场景一：系统服务在应用安装期间预加载数据成功
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163749.61194474420455796743831187517426:50001231000000:2800:3F8194DB0F2743BCBF0A1F87870DAB737B01E4804F3086D610FEFA3C6DCA3DCB.png)
    
    预加载数据成功时日志会提示：http onSuccess code: 200，并且提示预加载的数据大小：get rsp data, len 47（单位为字节）。
    
- 场景二：应用调用getPrefetchResult接口获取预加载数据成功
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163749.41435898554857094782300736771919:50001231000000:2800:F2DBF76365C4BE384720B92F3ED60A56C6C89CD2B42EBF4EDF372C5BF0B6B91D.png)
    
    数据获取成功时，无Error级别日志，会提示OnGetPreloadCache: end status:0。
    
- 场景三：应用调用getPrefetchResult接口获取预加载数据失败
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163749.98387042697885984731238816155559:50001231000000:2800:549CB3CCBFDCD78C1466BBBBAB55B4E98AAE6D318F2C1D02A3B3AC315FCFBDDB.png)
    
    **问题现象**
    
    数据获取失败时，存在Error级别日志，会提示GetPreloadData get cache fail。
    
    **解决措施**
    
    出现此问题，可按照如下步骤排查和解决：
    
    1. 检查系统服务在应用安装期间预加载数据的日志。如果打印日志与上文场景一提示的日志信息不一致，则继续执行后续步骤。
    2. 确认是否存在多次调用安装预加载接口问题。安装预加载接口不支持多次调用。
    3. 排除以上原因后，检查日志中是否出现“appid **** is not in white list, to skip”或者“XXX Read timed out”。如果出现，请参考[运行应用时提示“appid **** is not in white list, to skip”](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-faq-3)或者[运行应用时报“XXX Read timed out”异常](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-faq-4)解决。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-faq-prefetch "预加载")
# 运行应用时提示“appid **** is not in white list, to skip”

更新时间: 2025-12-16 16:37

**问题现象**

运行应用时提示“appid **** is not in white list, to skip”。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163759.82457527952897697714543783306804:50001231000000:2800:EF68F405F4F7E0FBFA5D0E6E6B1A0F21B70E5F8412E1977973E105BEA2C4B670.png)

**解决措施**

出现此错误，是因为手机白名单中未包含当前应用。可按照如下步骤排查和解决：

1. 确认云侧是否已开通云函数和预加载服务。须确保已成功开通。
2. 确认日志中提示的APP ID前缀与云侧创建应用的实际APP ID是否一致。若两者不一致，可能配置了自动签名，请更改为手动配置签名信息。
3. 手机端进入“设置->系统->日期和时间”，关闭“自动设置”开关，将“日期”往后加1天，然后卸载应用重新安装，应用会自动更新白名单。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-faq-5 "如何通过应用侧日志定位预加载问题")
# 运行应用时报“XXX Read timed out”异常

更新时间: 2025-12-16 16:38

**问题现象**

运行应用时报“XXX Read timed out”异常。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163804.44452686510920933956020974473319:50001231000000:2800:E6C72E4F6D3F20C5C2DF86255851FC422084C132F0F54B78BB958A0E88C23D31.png)

**解决措施**

出现此错误，是因为云侧没有启动云函数实例，卸载应用重新安装即可。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-faq-3 "运行应用时提示“appid **** is not in white list, to skip”")

