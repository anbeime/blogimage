开发鸿蒙应用调用高德地图HarmonyOS版本SDK不需要通过MCP（Module Control Protocol）。以下是完整的开发步骤示例：

1.搭建开发环境

· 安装DevEco Studio，配置HarmonyOS开发环境，创建新的HarmonyOS项目。

2.获取应用的AppID

· 在应用工程中，通过代码获取应用的AppID：

let flag = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_SIGNATURE_INFO;

let bundleInfo = bundleManager.getBundleInfoForSelfSync(flag);

let appId = bundleInfo.signatureInfo.appId;

· 注意：云真机调试时获取的AppID格式可能不完整，需确保使用正确的AppID格式（包含签名信息）。

3.申请高德API Key

· 访问高德开放平台官网（ [https://lbs.amap.com/），登录后进入控制台。](https://lbs.amap.com/%EF%BC%89%EF%BC%8C%E7%99%BB%E5%BD%95%E5%90%8E%E8%BF%9B%E5%85%A5%E6%8E%A7%E5%88%B6%E5%8F%B0%E3%80%82) · 创建新应用，选择“HarmonyOS平台”，输入获取到的AppID，申请API Key。

4.配置项目依赖

· 在项目模块的

build.gradle文件中，添加高德地图SDK依赖：

dependencies {

implementation filetree(dir: 'libs', include: ['*.har'])

}

· 将高德地图SDK的

.har文件放入项目

libs目录。

5.配置权限

· 在

config.json文件中声明网络权限：

"reqPermissions": [

{

"name": "ohos.permission.internet",

"reason": "地图需要网络连接"

}

]

6.初始化地图

· 在应用的入口文件（如

main.ets或

entry.ets）中，设置API Key并初始化地图：

import { mapsInitializer } from '@amap/amap_lbs_common';

// 设置API Key

mapsInitializer.setApiKey('您的API Key');

// 在页面中创建地图组件

@Entry

@Component

struct MapPage {

build() {

Column() {

MapView()

.width('100%')

.height('100%')

}

}

}

7.使用地图功能

· 在页面逻辑中获取地图对象，进行地图操作：

import { mapViewManager, amap } from '@amap/amap_lbs_map3d';

@Entry

@Component

struct MapPage {

private map: amap;

```
build() {    Column() {        MapView()            .width('100%')            .height('100%')            .onInit((mapView) => {                mapView.onCreate();                mapView.getMapAsync((amap) => {                    this.map = amap;                    // 设置地图中心点和缩放级别                    this.map.moveCamera(CameraUpdateFactory.newCameraPosition(                        new CameraPosition.Builder()                            .target(new LatLng(39.90923, 116.397428)) // 北京天安门坐标                            .zoom(12)                            .build()                    ));                });            })    }}
```

Plain Text

}

以上步骤涵盖了从环境搭建、权限配置到地图功能调用的完整流程。实际开发中，可根据需求进一步扩展地图功能，如添加标记点、路径规划、定位等。 根据您提供的文档内容，我将为您提供一份从零开始创建HarmonyOS项目的详细图文版本指南。
# 显示地图最后更新时间: 2025年12月10日

使用地图SDK之前，需要在 config.json 文件中进行相关权限设置，确保地图功能可以正常使用。

## 第一步，配置module.json5

#### 首先，声明权限

```
...
"requestPermissions": [
  {
    "name": 'ohos.permission.INTERNET',
  }
]
...
```

Json

## 第二步，在工程的oh-package.json5文件中添加依赖

#### 从ohpm仓库获取高德地图包

```
"dependencies": {
    "@amap/amap_lbs_common": ">=1.2.3",
    "@amap/amap_lbs_map3d": ">=2.2.7",
    "@amap/amap_lbs_search": ">=1.0.2",
}
```

Json

## 第三步，初始化地图容器

1

#### 从高德地图包中导入所需模块

```
import { AMap, MapsInitializer, MapView, MapViewComponent, MapViewManager } from '@amap/amap_lbs_map3d';
```

2

#### 设置Key

[获取Key](https://lbs.amap.com/api/harmonyosnext-map3d-sdk/guide/get-key)

```
MapsInitializer.setApiKey("您的key");
```

3

#### 获取MapView

```
MapViewManager.getInstance().registerMapViewCreatedCallback((mapview?: MapView, mapViewName?: string) => {
  if (!mapview) {
    return;
  }
  let mapView = mapview;
  ...
})
```

4

#### 初始化地图并获取AMap对象

```
mapView.onCreate();
mapView.getMapAsync((map) => {
let aMap: AMap = map;
// aMap.setTrafficEnabled(true) //打开交通路况图层
// TODO
})
```

5

#### 地图组件配置

```
MapViewComponent()
.width('100%')
.height('100%')
```

![](https://a.amap.com/lbs/static/img/doc/doc_1712732554708_a2031.png)

至此就可以看到地图展示，并且拿到了AMap对象后，就可以往地图上添加点线面等覆盖物

6

#### 完整代码示例

```
import { AMap, MapsInitializer, MapView, MapViewComponent, MapViewManager, } from '@amap/amap_lbs_map3d';

MapsInitializer.setApiKey("您的key");
MapViewManager.getInstance().registerMapViewCreatedCallback((mapview?: MapView, mapViewName?: string) => {
  if (!mapview) {
    return;
  }
  let mapView = mapview;
  mapView.onCreate();
  mapView.getMapAsync((map) => {
    let aMap: AMap = map;
  })
})

@Entry
@Component
struct Index {
  build() {
    Row() {
      MapViewComponent()
        .width('100%')
        .height('100%')
    }
  }
}
```

# 切换地图图层最后更新时间: 2025年11月17日

在使用地图图层前，请务必确保您已按照 [显示地图](https://lbs.amap.com/api/harmonyosnext-map3d-sdk/guide/create-map/show-map) 完成了所有必要的配置步骤。HarmonyOS 地图 SDK 提供了几种预置的地图图层，包括普通地图、卫星地图、夜景地图、导航地图、公交地图、导航夜景地图。

AMap 类提供图层类型常量，详细如下：

注意：路况图层是通过开关控制，不通过常量控制。

|   |   |
|---|---|
|类型|说明|
|MAP_TYPE_NORMAL：1|普通地图模式（默认模式）|
|MAP_TYPE_SATELLITE：2|卫星图模式|
|MAP_TYPE_NIGHT：3|夜景图模式|
|MAP_TYPE_NAVI：4|导航模式|
|MAP_TYPE_BUS: 5|公交模式|
|MAP_TYPE_NAVI_NIGHT: 6|导航夜间模式|

下文就卫星模式地图、夜景模式地图、导航模式地图为例做简单介绍。

## 卫星地图

在初始化地图时，除了可用选择默认的标准地图，还可以设置地图类型为「卫星图」，代码如下：

```
mapView.getMapAsync((map) => {
  map.setMapType(MapType.MAP_TYPE_SATELLITE)  //设置地图类型为卫星图
  let aMap: AMap = map;
})
```

提示：需要引入地图枚举类型

```
import {MapType} from '@amap/amap_lbs_map3d';
```

显示效果如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1763086826373_1c0b8.jpeg)

## 夜景地图

设置地图类型为「夜景图」，代码如下：

```
mapView.getMapAsync((map) => {
  map.setMapType(MapType.MAP_TYPE_NIGHT)  //设置地图类型为夜景图
  let aMap: AMap = map;
})
```

显示效果如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1763086850510_d9d85.jpeg)

## 导航模式地图

设置地图类型为「导航图」，代码如下：

```
mapView.getMapAsync((map) => {
  map.setMapType(MapType.MAP_TYPE_NAVI)  //设置地图类型为导航图
  let aMap: AMap = map;
})
```

显示效果如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1763086875883_57355.jpeg)

## 📋 **从零开始创建HarmonyOS项目（ArkTS）**

### **第一步：准备工作**

1. **注册华为开发者账号**并完成**实名认证**（注册地需为中国境内）

2. **安装DevEco Studio**（建议最新版本）

3. **确保账号无欠款**（否则云开发服务可能开通失败）

### **第二步：创建新工程**

#### **1. 打开工程创建向导**

- **方式一**：首次打开DevEco Studio，在欢迎页点击 **Create Project**

- **方式二**：已打开工程时，菜单栏选择 **File > New > Create Project**

创建工程入口

#### **2. 选择工程模板**

在 **Choose Your Ability Template** 界面：

- **Application**：普通应用开发

- **Atomic Service**：元服务开发（API 11及以上支持）

**推荐选择**： Application  →  Empty Ability （基础模板）

选择模板

#### **3. 配置工程信息**

进入 **Configure Your Project** 界面，填写以下关键信息：

|配置项|说明|填写示例/选择建议|
|---|---|---|
|**Project name**|工程名称|MyApplication （字母、数字、下划线）|
|**Bundle name**|包名（唯一标识）|com.example.myapplication （必须与AGC创建的应用包名一致）|
|**Save location**|保存路径|不含中文字符的路径|
|**Compatible SDK**|兼容的最低API版本|**关键选择**：根据需求选择（如 5.1.1(19) ）|
|**Module name**|模块名称|entry （默认）|
|**Device type**|支持的设备类型|**关键选择**：勾选目标设备|

**设备类型说明**：

- ✅ **Phone**：手机（最常用）

- ✅ **Tablet**：平板

- ✅ **2in1**：PC/二合一设备（支持多窗口）

- ✅ **Car**：车机

- ✅ **Wearable**：智能手表

- ✅ **TV**：智慧屏

- ✅ **Default**：默认设备（可编译但不上架）

配置工程

**重要提示**：

- **Bundle name**必须与在AGC（AppGallery Connect）创建的应用包名完全一致

- **Compatible SDK**选择后，应用将无法安装在低于此版本的设备上

- 如需**云开发**，必须选择 5.0.0(12) 或以上版本

#### **4. 特殊模板说明**

- **Native C++**：如需C++开发，选择此模板

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/3eedde57c6cc4e57aea3224bc9dbf8fe?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765677827%3B1765706627&q-key-time=1765677827%3B1765706627&q-header-list=&q-url-param-list=&q-signature=51201a8023d1dc0571b92a2692894bf081cb0c26)

- **[CloudDev]Empty Ability**：端云一体化开发模板

- **元服务工程**：Bundle name自动生成为 com.atomicservice.[appid] 格式

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/4b1bd4b240a74baead397b90b93c4f6a?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765677827%3B1765706627&q-key-time=1765677827%3B1765706627&q-header-list=&q-url-param-list=&q-signature=33be5d166a054fed53defa4330655e1e6f0068ef)

### **第三步：工程创建完成**

点击 **Finish**，DevEco Studio自动生成代码和资源文件。

### **第四步：工程结构解析**

创建完成后，工程目录结构如下：

```
MyApplication/├── .hvigor/                    # 构建配置目录├── .idea/                      # IDE配置目录├── AppScope/                   # 应用全局配置│   └── app.json5              # 应用全局配置文件├── entry/                      # 主模块（HAP包）│   ├── src/│   │   ├── main/│   │   │   ├── ets/           # ArkTS源代码│   │   │   │   ├── entryability/  # 应用入口Ability│   │   │   │   └── pages/     # 页面文件│   │   │   ├── resources/     # 资源文件（图片、字符串等）│   │   │   └── module.json5   # 模块配置文件│   │   └── ohosTest/          # 测试代码│   ├── build-profile.json5    # 模块构建配置│   └── oh-package.json5       # 依赖管理文件└── build-profile.json5        # 工程级构建配置
```

Plain Text

### **第五步：关键配置文件详解**

#### **1. app.json5（应用全局配置）**

```
{  "app": {    "bundleName": "com.example.myapplication",  // 必须与AGC包名一致    "vendor": "example",    "versionCode": 1000000,    "versionName": "1.0.0",    "icon": "$media:app_icon",    "label": "$string:app_name"  }}
```

JSON

#### **2. module.json5（模块配置）**

```
{  "module": {    "name": "entry",    "type": "entry",    "description": "$string:module_desc",    "mainElement": "EntryAbility",    "deviceTypes": ["phone", "tablet"],  // 支持的设备类型    "pages": "$profile:main_pages",    "abilities": [...],    "requestPermissions": [...]  // 权限声明  }}
```

JSON

#### **3. build-profile.json5（构建配置）**

```
{  "app": {    "signingConfigs": [],    "products": [      {        "name": "default",        "signingConfig": "default",        "compileSdkVersion": "5.1.1(19)",      // 编译SDK版本        "compatibleSdkVersion": "5.1.1(19)",   // 兼容的最低版本        "targetSdkVersion": "5.1.1(19)",       // 目标版本（可选）        "runtimeOS": "HarmonyOS",              // 运行环境        "buildOption": {          "externalNativeOptions": {            "abiFilters": ["armeabi-v7a"]      // Native C++需要（如RK开发板）          }        }      }    ]  }}
```

JSON

### **第六步：特殊场景配置**

#### **1. 创建OpenHarmony工程**

如需开发OpenHarmony应用，创建HarmonyOS工程后，修改 build-profile.json5 ：

```
{  "products": [    {      "name": "default",      "signingConfig": "default",      "compileSdkVersion": "20",        // 改为字符串      "compatibleSdkVersion": "20",    // 改为字符串      "runtimeOS": "OpenHarmony"        // 关键修改    }  ]}
```

JSON

#### **2. 配置AGC云开发**

如需使用云开发功能：

1. 创建工程时选择 **[CloudDev]Empty Ability** 模板

2. 确保 **Enable CloudDev** 已勾选

3. 工程创建后自动关联AGC项目

4. 在 module.json5 中添加AGC配置：

```
"metadata": [  {    "name": "client_id",    "value": "从AGC获取的Client ID"  }]
```

JSON

#### **3. 元服务工程特殊要求**

- Bundle name格式： com.atomicservice.[appid] 

- Compatible SDK必须≥ 5.0.0(12) 

- 自动生成包名，不可手动修改

### **第七步：同步与运行**

1. 配置完成后点击 **Sync Now** 同步工程

2. 如提示设备类型变更，点击 **Yes** 确认

3. 连接真机或启动模拟器

4. 点击 **Run** 运行应用

### **第八步：常见问题解决**

#### **问题1：工程检查报错**

```
Incorrect settings found in the build-profile.json5 file
```

Plain Text

**解决方案**：

- 检查 compileSdkVersion 、 compatibleSdkVersion 格式是否为字符串（如 "5.1.1(19)" ）

- 确认 runtimeOS 位置正确（在products数组内）

- 删除模块级 build-profile.json5 中的 runtimeOS 字段

#### **问题2：设备类型不匹配**

```
The type of target device does not match the device type configured by module
```

Plain Text

**解决方案**：

1. 检查 module.json5 中 deviceTypes 是否包含目标设备

2. 检查 build-profile.json5 中 targets 配置

3. 检查 hvigorfile.ts 是否修改了设备类型设置

#### **问题3：SDK版本兼容性**

- 确保真机/模拟器系统版本≥ compatibleSdkVersion 

- 如需使用新API， compileSdkVersion 需≥API版本

### **第九步：后续开发建议**

1. **添加新Module**：

- 菜单栏选择 **File > New > Module**

- 选择Module类型： Entry 、 Feature 、 Library 

2. **配置签名**：

- 调试阶段：使用自动签名

- 发布前：申请发布证书和Profile文件

3. **多设备适配**：

- 使用响应式布局

- 针对不同设备类型提供差异化资源

4. **版本管理**：

- 定期更新SDK版本

- 关注API变更和废弃通知

### **总结**

创建HarmonyOS项目的关键步骤：

1. **选择正确模板**（Application/Atomic Service）

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/a2ec83c6db984d2d8a8374b84b9ec05b?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765677827%3B1765706627&q-key-time=1765677827%3B1765706627&q-header-list=&q-url-param-list=&q-signature=60d9c6c093300fcbcadc3fcbf9f6b06a6ab2240c)

2. **配置唯一Bundle name**（与AGC一致）

3. **选择合适的SDK版本**（考虑兼容性和功能需求）

4. **勾选目标设备类型**（Phone、Tablet等）

5. **完成AGC关联**（如需云开发）

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/e294d4efed1f4b5b90568fbb9f36771e?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765677827%3B1765706627&q-key-time=1765677827%3B1765706627&q-header-list=&q-url-param-list=&q-signature=09927efec4915f8062de7146f480a5b6873a621c)

通过以上步骤，您就可以成功创建并配置一个HarmonyOS应用工程，开始您的应用开发之旅。 根据文档内容，我将为您详细解答如何从零开始创建一个HarmonyOS项目，包括SDK、Module Name、Device Type等关键配置的选择。

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/98b79b6fda734971a67dccee3eb4779f?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765677843%3B1765706643&q-key-time=1765677843%3B1765706643&q-header-list=&q-url-param-list=&q-signature=6022aa9684e628e2d0679ae6c5ee1b33ad22b4fa)

## 📋 从零开始创建HarmonyOS项目的完整指南

### 1. **创建新工程的基本流程**

#### **第一步：打开工程创建向导**

- **方式一**：如果当前未打开任何工程，在DevEco Studio欢迎页选择 **Create Project**

- **方式二**：如果已打开工程，在菜单栏选择 **File > New > Create Project**

#### **第二步：选择工程类型**

```
Choose Your Ability Template├── Application（应用开发）│   ├── Empty Ability（空模板）│   ├── Native C++（C++开发）│   └── [CloudDev]Empty Ability（云开发模板）└── Atomic Service（元服务开发）    └── Empty Ability（空模板）
```

Plain Text

**选择建议**：

- **普通应用**：选择 **Application > Empty Ability**

- **需要云开发功能**：选择 **Application > [CloudDev]Empty Ability**

- **元服务**：选择 **Atomic Service > Empty Ability**

- **C++开发**：选择 **Native C++**

### 2. **配置工程基本信息**

#### **关键配置参数详解**

|参数|说明|选择建议|
|---|---|---|
|**Project name**|工程名称|由大小写字母、数字和下划线组成|
|**Bundle name**|包名|需保证唯一，需与AGC创建的HarmonyOS应用“应用包名”一致|
|**Save location**|保存路径|不能包含中文字符|
|**Compatible SDK**|兼容的最低API Version|**关键选择**：根据目标设备选择|
|**Module name**|模块名称|默认entry，可自定义|
|**Device type**|支持的设备类型|**关键选择**：根据应用目标设备选择|

#### **SDK版本选择（Compatible SDK）**

文档中提到的SDK版本示例：

-  5.0.0(12)  - 支持云开发的最低版本

-  5.0.4(16)  - Native版本示例

-  5.1.0(18)  - 常规开发版本

-  6.0.0(20)  - 较新版本

**选择原则**：

1. **功能需求**：如果需要云开发，选择 5.0.0(12) 或以上

2. **设备兼容**：考虑要支持的最低系统版本

3. **API特性**：新版SDK提供更多API能力

#### **设备类型选择（Device type）**

文档中列出的设备类型及枚举值：

|设备类型|枚举值|说明|
|---|---|---|
|手机|phone|最常用设备类型|
|平板|tablet|平板设备|
|PC/2in1|2in1|PC设备，支持多窗口、键盘鼠标操作|
|智慧屏|tv|电视设备|
|智能手表|wearable|系统能力较丰富的手表|
|车机|car|车载设备|
|默认设备|default|可编译但不支持上架，建议用phone替代|

**选择建议**：

- **单设备应用**：只选择目标设备类型

- **多设备应用**：勾选所有支持的设备类型

- **PC端适配**：必须包含 2in1 才能在PC上全屏展示

### 3. **Module Name配置**

#### **Module命名规则**

- Module name不可与工程名称相同

- 由字母、数字和下划线组成，且必须以字母开头

- 最大长度31字节

#### **Module类型选择**

在**添加Module**时需选择Module type：

- **Entry**：应用的主模块，一个工程只能有一个Entry模块

- **Feature**：动态特性模块

- **Library**：共享包模块（HAR/HSP）

### 4. **工程结构说明**

创建完成后生成的典型工程结构：

```
MyApplication/├── .hvigor/           # 构建配置├── .idea/             # IDE配置├── AppScope/          # 全局配置│   └── app.json5      # 应用全局配置├── entry/             # 主模块（默认Module name）│   ├── src/│   │   ├── main/│   │   │   ├── ets/           # ArkTS源码│   │   │   │   ├── entryability/  # 应用入口│   │   │   │   └── pages/      # 页面文件│   │   │   ├── resources/      # 资源文件│   │   │   └── module.json5    # 模块配置文件│   │   └── ohosTest/          # 测试代码│   ├── build-profile.json5    # 模块构建配置│   └── oh-package.json5       # 依赖管理└── build-profile.json5        # 工程级构建配置
```

Plain Text

### 5. **重要配置文件说明**

#### **module.json5 - 模块配置**

```
{  "module": {    "name": "entry",                    // Module名称    "type": "entry",                    // 模块类型：entry/feature/har/shared    "description": "$string:module_desc",    "mainElement": "EntryAbility",      // 主Ability    "deviceTypes": ["phone", "tablet"], // 支持的设备类型    "deliveryWithInstall": true,    "installationFree": false,    "pages": "$profile:main_pages",    "abilities": [...],    "metadata": [      {        "name": "client_id",           // AGC Client ID配置        "value": "***"      }    ]  }}
```

JSON

#### **app.json5 - 应用全局配置**

```
{  "app": {    "bundleName": "com.example.myapplication",  // 必须与AGC包名一致    "vendor": "example",    "versionCode": 1000000,    "versionName": "1.0.0",    "icon": "$media:app_icon",    "label": "$string:app_name"  }}
```

JSON

### 6. **特殊场景配置**

#### **创建OpenHarmony工程**

如需创建OpenHarmony工程，需修改 build-profile.json5 ：

```
{  "app": {    "products": [{      "name": "default",      "signingConfig": "default",      "compileSdkVersion": "20",        // 改为字符串类型      "compatibleSdkVersion": "20",     // 改为字符串类型      "runtimeOS": "OpenHarmony"        // 关键修改    }]  }}
```

JSON

#### **Native C++工程特殊配置**

如果选择Native C++模板且需要在RK开发板上运行：

```
{  "buildOption": {    "externalNativeOptions": {      "abiFilters": ["armeabi-v7a"]    // RK板需要    }  }}
```

JSON

#### **元服务工程特殊要求**

- Bundle name采用固定格式： com.atomicservice.[appid] 

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/6cb688a941564fce8a77c7955d456c93?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765677843%3B1765706643&q-key-time=1765677843%3B1765706643&q-header-list=&q-url-param-list=&q-signature=123faa43127e4d2da0d83100a5dd156ebb726b88)

- 自动生成，开发者无法手动修改

- Compatible SDK必须选择 5.0.0(12) 或以上版本

### 7. **常见问题与解决方案**

#### **编译报错：设备类型不匹配**

```
错误：The type of target device does not match the device type configured by module: xxx
```

Plain Text

**解决措施**：

1. 确保 module.json5 中 deviceTypes 包含所需设备类型

2. 确保 build-profile.json5 中 targets 下指定的设备类型包含所需类型

3. 检查 hvigorfile.ts 或 hvigorconfig.ts 是否修改了设备类型设置

#### **配置AGC身份信息**

在 module.json5 中添加：

```
"metadata": [  {    "name": "client_id",    "value": "从AGC获取的Client ID"  }]
```

JSON

### 8. **最佳实践建议**

1. **SDK版本选择**：

- 新项目建议选择较新版本（如 6.0.0(20) ）

- 考虑目标用户设备系统版本

- 如需云开发，必须≥ 5.0.0(12) 

2. **设备类型选择**：

- 初始开发可只选 phone 

- 如需多端适配，逐步添加 tablet 、 2in1 等

- PC端适配必须包含 2in1 

3. **Module规划**：

- 简单应用：一个Entry模块即可

- 复杂应用：Entry + 多个Feature模块

- 代码复用：创建Library模块（HAR/HSP）

4. **工程同步**：

- 配置修改后点击 **Sync Now**

- 如提示设备类型变更，点击 **Yes** 确认

通过以上步骤，您可以顺利完成HarmonyOS项目的创建和基础配置。根据您的具体应用场景选择合适的SDK版本和设备类型，是项目成功的关键第一步。

# 创建模拟器

更新时间: 2025-12-12 10:48

## 操作步骤

1. 点击菜单栏的**Tools > Device Manager**，点击右下角的**Edit**设置模拟器实例的存储路径**Local Emulator Location**，Mac默认存储在~/.Huawei/Emulator/deployed下，Windows默认存储在C:\Users\xxx\AppData\Local\Huawei\Emulator\deployed下。

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/35ee78dc177d4b7996514109f99bac24?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=cc360ee6f6effef855400288825df9735d01eaa4)

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/8fc1f144c95d4c9981a8a02936b572af?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=de67e15fd1bc36678a28cb2dd819facfd2ef06fd)

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/28f31f77e64c40bca7c87f446dd59344?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=c4ba08bd2091b641dc922e61e7d39fdc16fe139d)

2. 在**Local Emulator**页签中，单击右下角的**New Emulator**按钮，创建一个模拟器。在模拟器配置界面，可以选择一个默认的设备模板，首次使用时请点击设备右侧的下载模拟器镜像，您也可以在该界面更新或删除不同设备的模拟器镜像。单击**Edit**可以设置镜像文件的存储路径。macOS默认存储在~/Library/Huawei/Sdk下，Windows默认存储在C:\Users\xxx\AppData\Local\Huawei\Sdk下。**说明**如果配置界面显示异常，例如设备列表为空等，可先关闭DevEco Studio，并清理~/Library/Huawei（Windows路径为C:\Users\xxx\AppData\Local\Huawei）路径下对应DevEco Studio版本的缓存。

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/544ef58256714a93a3f32b36ba37aba5?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=99b9f1ad9864fff54b91b999a221bad19f2a477b)

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/be5dbf8287a34c4ba6aa9aa5055b7a88?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=be4bb8efe14b8f1ae147ed896cee3c335c8e338b)

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/f8b96c65f72a4b51b6c142e7f39ea46f?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=ec4fbb9f458c3c70f1be6b5cbed98be0e1a96e14)

3. 单击**Next**，设置设备相关的参数。该功能从DevEco Studio 6.0.0 Beta1版本开始支持。

- **Name**：设置模拟器的名称。

- **Screen Profile**：模拟器屏幕配置参数，可点击下拉框选择预置的机型配置，也可点击**Customize**自定义配置，在自定义配置的情况下可以对屏幕尺寸、分辨率和DPI进行修改，取值范围参考界面提示。

- **Screen size：**屏幕的对角线长度，单位为英寸。

- **Resolution**：分辨率，包括横向像素数量和纵向像素数量。

- **DPI**：像素密度，DPI 越高，UI组件占用的像素点越多，从而提供更精细的显示效果。

- **Memory**：设置模拟器的内存。

- **Storage**：设置模拟器的存储空间。

确认所有参数后，点击**Finish**创建模拟器。

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/8a2115e6a0df41fead60b35fdb84db55?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=a9c46c05e8af5f30e5976dadc43ca183fbb4a4bb)

1. 在设备管理器页面，单击

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/66ecd72645af4f54980dad68ae819784?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=2f6e81fbab1ba095b85981abfaa00db6e2426006)

启动模拟器。

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/35e8f081f423483b8a794076ca71c74e?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=cf147d77bcf84c2b5552582103c5c0784144095e)

2. 单击DevEco Studio的**Run > Run'模块名称'**或

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/5d190f8190e14afa95adc1e52f2fb631?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=a1f447d357303da294631977a8355d807497b745)

。

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/d16c0c773df146ab8eae21160dd84b14?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=e3bc55c72fd2dda8af71d7afa6292b31b0da4595)

3. DevEco Studio会启动应用/元服务的编译构建与推包，完成后应用/元服务即可运行在模拟器上。

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/c372ebf6130d469b94bf0121a0799a4a?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765678094%3B1765706894&q-key-time=1765678094%3B1765706894&q-header-list=&q-url-param-list=&q-signature=5df423ef20541b98288acc5f716077645bbe3739)

 [**管理模拟器**](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-management)  好的，根据您提供的文档内容，我将为您详细解释端云一体化开发工程与传统工程的不同之处，并提供一份详细的图文版开发过程指南。

# 📦 端云一体化开发工程详解与图文开发指南

## 一、 端云一体化开发工程与传统工程的核心区别

端云一体化开发工程是DevEco Studio中一种**集成云端服务**的特殊工程类型，它与传统的纯端侧HarmonyOS应用工程有本质区别。

|对比维度|**传统HarmonyOS应用工程**|**端云一体化开发工程**|
|---|---|---|
|**工程结构**|仅包含端侧工程 ( Application )。|包含**端侧工程 (** **Application** **)** 和**云侧工程 (** **CloudProgram** **)** 两个并列目录。|
|**开发工具**|仅需DevEco Studio进行端侧开发。|**一套DevEco Studio** 即可完成**端侧和云侧**的协同开发、调试与部署。|
|**技术栈与技能**|端侧开发人员需掌握ArkTS/ArkUI等端侧技术。|端侧开发人员依托**Cloud Foundation Kit**，使用**统一的ArkTS技术栈**即可开发云函数、云对象等云侧服务，降低了全栈开发门槛。|
|**服务器与运维**|需要开发者自行搭建、配置和维护后端服务器、数据库等基础设施。|**无需管理服务器**。云侧服务（云函数、云数据库、云存储）由华为AGC平台提供，具备**开箱即用、一键部署、自动弹性伸缩、免运维**的特点。|
|**开发流程**|端侧与云侧分离开发，沟通成本高，部署流程复杂。|**端云协同开发**：在DevEco Studio内即可完成云侧代码开发、调试，并**一键部署至AGC云端**，端侧代码可直接调用。|
|**工程模板**|选择  Empty Ability  等标准模板。|选择带有  [CloudDev]  前缀的模板，如  [CloudDev]Empty Ability 。|
|**签名方式**|支持自动签名和手动签名。|**当前仅支持手动签名**。|
|**运行调试**|支持模拟器和真机。|**仅支持真机**，不支持模拟器运行调试。|
|**服务地域**|无限制。|当前云服务**仅在中国境内**（不含港澳台）提供。|

**总结**：端云一体化开发工程的最大不同在于**将云服务的开发、部署和调用深度集成到了DevEco Studio IDE和开发流程中**，实现了前端开发者向全栈开发者的平滑过渡，极大提升了开发效率并降低了运维成本。

---

## 二、 端云一体化开发详细图文过程

以下流程基于文档《文档导览.pdf》、《创建HarmonyOS应用工程_acfec549.pdf》等综合整理。

### **第一阶段：准备阶段**

#### **步骤1：注册与认证**

1. 注册**华为开发者账号**。

2. 完成**实名认证**（企业或个人）。

3. 确保账号**无欠费**，否则可能影响云服务开通。

#### **步骤2：搭建开发环境**

1. **安装DevEco Studio**：必须使用 **NEXT Developer Beta1 或更高版本**。

2. **配置网络**：如果网络需要代理才能访问外网，请提前在DevEco Studio中**配置NPM代理**，否则工程初始化时下载依赖会失败。

### **第二阶段：创建端云一体化工程**

#### **步骤1：启动工程创建向导**

- **首次打开**：在欢迎页点击  **Create Project** 。

- **已有工程**：菜单栏选择  **File > New > Create Project** 。

创建工程入口

#### **步骤2：选择云开发模板**

在  Choose Your Ability Template  界面：

1. 选择  Application （应用）或  Atomic Service （元服务）。

2. 在模板列表中，**必须选择带有**  **[CloudDev]**  **标识的模板**，例如  [CloudDev]Empty Ability 。

> **说明**： [CloudDev]Empty Ability  是通用云开发模板，预置了云函数、云数据库、云存储的演示代码。

选择云开发模板

#### **步骤3：配置工程信息**

在  Configure Your Project  界面，填写关键信息：

|配置项|说明与要求|
|---|---|
|**Project name**|工程名称，字母、数字、下划线组成。|
|**Bundle name**|**应用包名，必须与在AGC（AppGallery Connect）创建的应用包名完全一致**。|
|**Save location**|工程保存路径，**不能包含中文字符**。|
|**Compatible SDK**|**必须选择 5.0.0(12) 或更高版本**，否则无法使用端云一体化功能。|
|**Module name**|模块名，默认  entry 。|
|**Device type**|目前**仅支持手机 (Phone)**。|
|**Enable CloudDev**|**必须勾选**（云开发模板默认已勾选且不可更改）。|

配置工程信息

#### **步骤4：关联云开发资源**

点击  Next  后，进入  Associate Your CloudDev Resources  界面。

1. 选择您的华为开发者账号和团队。

2. 选择或创建AGC项目。

3. **仔细阅读并勾选同意相关服务协议**（只有账号持有者或法务角色有权限签署）。

4. 点击  Finish 。

关联云资源

#### **步骤5：工程初始化**

1. DevEco Studio会自动执行工程同步。

2. **端侧工程**会自动执行  ohpm install  下载ArkTS依赖。

3. **云侧工程**会自动执行  npm install  下载Node.js依赖。

> **注意**：如果云侧  npm install  失败，请检查网络或NPM代理配置。

4. DevEco Studio会**自动为您在AGC关联的项目中开通云函数、云数据库、云存储服务**。开通状态可在  Notifications  窗口查看。

> **注意**：如果云存储服务开通失败，可能是账户欠费，需在AGC控制台手动开通。

### **第三阶段：工程结构与开发**

#### **工程目录结构**

创建完成后，工程包含两个核心部分：

```
MyCloudApp/                      # 工程根目录├── Application/                 # 【端侧工程】开发HarmonyOS应用/元服务界面和业务逻辑│   ├── entry/                   # 主模块│   │   └── src/main/ets/│   │       ├── pages/           # 页面文件，模板预置了云函数、数据库、存储的示例页面│   │       └── entryability/    # 应用入口│   └── cloud_objects/          # （可选）存放从云对象生成的端侧调用接口类└── CloudProgram/                # 【云侧工程】开发云端服务    ├── cloudfunctions/          # 云函数和云对象目录    │   └── id-generator/        # 示例云函数/对象    └── clouddb/                 # 云数据库目录        ├── objecttype/          # 对象类型定义        └── dataentry/           # 数据条目
```

Plain Text

#### **步骤6：开发云侧工程**

云侧工程支持开发三种核心服务：

1. **开发云函数/云对象**

- 在  CloudProgram/cloudfunctions/  下创建新的云函数或云对象。

- 编写业务逻辑代码（使用JavaScript/TypeScript）。

- 在DevEco Studio内进行**本地调试**。

- **部署到AGC**：右击云函数/对象，选择  Deploy 。

2. **开发云数据库**

- 在  CloudProgram/clouddb/objecttype/  下定义对象类型（数据表结构）。

- 在  CloudProgram/clouddb/dataentry/  下添加示例数据。

- 将数据库结构**部署到AGC**。

> **最佳实践建议**：虽然端云代码可并行开发，但若端侧需要调用云侧代码，**建议先完成云侧代码的开发、调试与部署**，再开发端侧。

#### **步骤7：开发端侧工程**

端侧工程在  Application  目录下开发，主要工作是调用已部署的云服务。

1. **调用云函数**：

```
import { cloudFunction } from '@kit.CloudFoundationKit';cloudFunction.call({ name: '你的云函数名' })  .then((res) => { /* 处理结果 */ })  .catch((err) => { /* 处理错误 */ });
```

TypeScript

2. **调用云对象**：

- 首先，在云侧工程右击云对象，选择  Generate Invoke Interface ，生成端侧调用接口类（位于  Application/cloud_objects/ ）。

- 在端侧代码中导入并调用该对象的方法。

3. **访问云数据库**：

- 首先，为云数据库对象类型**生成Client Model**（端侧数据模型）。

- 在端侧代码中引入Client Model，使用Cloud Foundation Kit API进行增删改查。

4. **调用云存储**：

- 初始化云存储实例。

- 使用  uploadFile ,  downloadFile  等接口进行文件操作。

通用模板 ( [CloudDev]Empty Ability ) 已在  entry/src/main/ets/pages/  下提供了上述四种调用的示例代码 ( CloudFunction.ets ,  CloudDb.ets ,  CloudStorage.ets )，可供参考。

#### **步骤8：配置云存储安全策略（重要！）**

由于模板初始化代码未配置AccessToken，**必须手动配置云存储安全策略为“始终可读写”**，否则文件上传会失败。

1. 登录 **AppGallery Connect**。

2. 进入您的项目，选择  **云开发(Serverless) > 云存储** 。

3. 进入  **安全**  页签。

4. 在“配置策略”中，将默认规则修改为：

```
allow read, write: if true;
```

Plain Text

5. 点击  **发布** 。

配置云存储策略

### **第四阶段：调试与发布**

#### **步骤9：本地调试**

1. 使用 **USB连接真机**（端云一体化开发不支持模拟器）。

2. 在DevEco Studio中点击运行按钮，将应用安装到手机。

3. 在手机上体验端云交互功能，查看运行效果和日志。

#### **步骤10：打包与发布**

1. 完成所有开发后，对工程进行**手动签名**（配置发布证书和Profile文件）。

2. 将签名的HAP/HAPP包**提交至AGC**，申请上架到华为应用市场。

---

## 三、 关键注意事项与常见问题

1. **设备与地域限制**：目前仅支持**手机设备**，且云服务仅在中国大陆可用。

2. **签名方式**：**仅支持手动签名**，不支持自动签名。

3. **目录结构**：工程根目录下**只能有**  **Application**  **和**  **CloudProgram**  **两个文件夹**，否则DevEco Studio可能无法识别为端云一体化工程。

4. **云数据库限制**：

- AGC云端**存储区(Zone)数量不得超过4个**。

- 已部署的数据库字段**不能修改**，如需修改需删除后重新创建。

![](https://ima-notebook-prod.image.myqcloud.com/2/bHkNGeYDapykL9V0ON6P2D/c4f55c59c9ca4104b6fc1322b3c56bf3?q-sign-algorithm=sha1&q-ak=AKID9IDtLZZKqGRO7hVFnMn0zjXTXovoTtAN&q-sign-time=1765679148%3B1765707948&q-key-time=1765679148%3B1765707948&q-header-list=&q-url-param-list=&q-signature=ab823b7a75a41d63099c2f2498e17586e5645852)

5. **历史工程转换**：可以将已有的非端云工程转换为端云一体化工程，方法是创建一个同Bundle name的端云工程，然后用历史工程的  Application  目录替换新工程的  Application  目录。

通过以上步骤，您就可以完成一个完整的端云一体化HarmonyOS应用的开发、调试和发布准备。这种模式极大地简化了云端开发的复杂性，让开发者可以更专注于业务逻辑创新。