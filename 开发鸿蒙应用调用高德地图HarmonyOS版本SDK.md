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
# 显示定位蓝点最后更新时间: 2025年11月04日

定位蓝点指的是进入地图后显示当前位置点的功能。

## 实现定位蓝点

1

#### 准备地图

显示地图详细讲解，前往 [显示地图](https://lbs.amap.com/api/harmonyosnext-map3d-sdk/guide/create-map/show-map) 文档。

```
let aMap: AMap = map;
aMap?.moveCamera(CameraUpdateFactory.newLatLngZoom(new LatLng(40.024279, 116.434153), 13)); //设置地图中心点以及缩放级别
```

2

#### 设置定位图层样式

```
let locationStyle: MyLocationStyle = new MyLocationStyle(); //定位样式构造函数

//设置我的位置展示模式
locationStyle.myLocationType(MyLocationStyle.LOCATION_TYPE_FOLLOW); //定位、且将视角移动到地图中心点，定位点跟随设备移动

aMap?.setMyLocationStyle(locationStyle); //设置定位图层的样式
```

3

#### 设置定位源

```
//定义了一个定位源，为地图提供定位数据
let locationSource: LocationSource = {
  activate(listener: OnLocationChangedListener): void {
    let location: geoLocationManager.Location = {
      accuracy: 1000,
      altitude: 0,
      direction: 0,
      //116.438055,40.025108
      latitude: 40.025108,
      longitude: 116.438055,
      speed: 0,
      timeSinceBoot: 123587419434256,
      timeStamp: 0,
      altitudeAccuracy: 0,
      speedAccuracy: 0,
      directionAccuracy: 0,
      uncertaintyOfTimeSinceBoot: 0,
      sourceType: 1
    }
    try {
      listener.onLocationChanged(location);
    } catch (e) {
      console.info((e as BusinessError).message);
    }
  },
  deactivate() {
  }
};

aMap?.setLocationSource(locationSource); //设置定位源
```

4

#### 打开定位图层

```
aMap?.setMyLocationEnabled(true); //打开定位图层
```
# 显示室内地图最后更新时间: 2025年12月10日

开启室内地图后，如果可见区域内包含室内地图覆盖区域（如：西单大悦城等知名商场），且缩放达到一定级别，便可直接在地图上看到精细室内地图效果。

缩放级别放大到一定级别时，地图上可以显示室内地图。

缩放级别继续放大时，不仅可以看到室内地图效果，还允许操作切换楼层，显示精细化室内地图。

左上角为楼层切换组件

如下图示：

![](https://a.amap.com/lbs/static/img/doc/doc_1765347727047_076c2.png)

可以通过以下接口控制是否显示室内地图：

```
/**
 * 设置是否显示室内地图，默认不显示。<br>
 * <p>
 * 注：如果打开了室内地图，会显示3D建筑物，即如果之前有设置不显示3D建筑物，3D建筑物也会被显示出来。
 *
 * @param enabled true：显示室内地图；false：不显示；
 */
public showIndoorMap(enabled: boolean): void {
    this.mapDelegate.setIndoorEnabled(enabled);
}
```

可以通过以下接口控制切换显示室内地图的某一层：

```
/**
 * 室内地图楼层控制接口，通过此接口可以控制某个室内地图显示的楼层。
 *
 * @param indoorBuildingInfo indoorBuildingInfo 对象，它定义了室内地图属性,详情{@link IndoorBuildingInfo}。
 */
public setIndoorBuildingInfo(indoorBuildingInfo: IndoorBuildingInfo): void {
    this.mapDelegate.setIndoorBuildingInfo(indoorBuildingInfo);
}
```

可以通过以下接口设置室内地图楼层状态监听(demo中实现楼层切换的关键)

```
/**
 * 设置室内地图状态监听接口
 *
 * @param listener 室内地图状态监听接口。
 * @since V2.2.4
 */
public setIndoorFloorSwitchAdapter(listener: IndoorFloorSwitchAdapter): void {
    try {
        this.mapDelegate.setIndoorFloorSwitchAdapter(listener);
    } catch (e) {
        LogUtil.e(Constants.MODULE_TAG, "AMap", e);
    }
}
```

调用上述室内地图的接口实现的demo(部分)

```
# 设置状态变量实现楼层切换组件与室内地图楼层之间的实时同步
 @State floorSwitch: IndoorFloorSwitchAdapter = new IndoorFloorSwitchAdapter();

# 楼层切换组件变化后的回调
  OnPicker(valueName: string): void {
    let indoorBuildingInfo: IndoorBuildingInfo = this.floorSwitch.mIndoorBuildingInfo;
    let offset: number = indoorBuildingInfo.floor_names.findIndex((value: string) => value === valueName);
    if (offset >= indoorBuildingInfo.floor_names.length || offset < 0) {
      return
    }
    let index = indoorBuildingInfo.floor_indexs[offset];
    this.floorSwitch.offset = offset;
    indoorBuildingInfo.activeFloorIndex = index;
    indoorBuildingInfo.activeFloorName = valueName;
    this.mAMap?.setIndoorBuildingInfo(indoorBuildingInfo);
  }

# 设置楼层切换组件
TextPicker({range: this.floorSwitch?.mIndoorBuildingInfo.floor_names, selected: this.floorSwitch?.offset})
  .position({left:0, top: 0})
  .visibility(this.floorSwitch.visible)
  .onScrollStop((value: string | string[], index: number | number[]) => {
    this.OnPicker(value as tring);
  })
  .opacity(1)
```
# 显示3D地形图最后更新时间: 2025年12月10日

地形图是在3D地图的基础上，融入地形高程，使3D地图能够显示地形的高低起伏，显示山脉的形状以及走向等。

可以通过以下接口控制是否显示3D地形图：

```
/**
 * 设置是否打开地形图, 默认为关闭
 * 打开地形图之后，底图会变成3D模式，添加的点线面等覆盖物也会自动带有高程
 * <p>
 * 注意：需要在MapView创建之前调用
 *
 * @param isTerrainEnable true为打开，默认false
 * @since 2.2.4
 */
public static setTerrainEnable(isTerrainEnable: boolean)
```

效果如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1765347794339_0d50f.png)

注意：地形图的渲染和普通3D地形图使用的引擎不同不能够同时显示。
# 自定义地图最后更新时间: 2025年09月15日

## 简介

自 Harmony 3D 地图 SDK v2.2.2 起，高德地图支持使用可视化自定义地图模版改变底图颜色和样式，实现可视化的编辑和控制显示地图元素。

## 创建样式文件

### 创建地图样式

高德地图开放平台的开发者在取得开发者账号后，可以进入[开发者控制台](https://lbs.amap.com/dev/key)，在[地图自定义平台](https://lbs.amap.com/dev/mapstyle/index)选择“创建地图样式”，可以选择一个模板进行创建。

![](https://a.amap.com/lbs/static/img/doc/doc_1757930035503_4a47a.png)

#### 编辑地图样式 

在创建的页面的左侧列表选择任一要素编辑样式属性；也可以单击地图，在弹出的列表中选择要素进行编辑。

![](https://a.amap.com/lbs/static/img/doc/doc_1757930043484_fb5c8.png)

#### 发布地图样式并下载 

编辑完成后点击右上角“保存”->“发布”，发布完成后，选择“使用方法”，然后选择“android”平台，点击“下载离线文件”。

![](https://a.amap.com/lbs/static/img/doc/doc_1757930050494_10fb1.png)

![](https://a.amap.com/lbs/static/img/doc/doc_1757930056708_09dd8.png)

## 设定样式文件

注意：自地图SDK v2.2.2 起，自定义地图使用方法进行了较大更新，具体请参见以下具体文档说明。

### 一、设定离线样式文件

1、在官网控制台-我的地图样式中选择与当前使用的地图SDK版本号所对应的版本进行样式文件下载：(注意：harmony 也是使用Android 离线地图样式，版本号选择最新版本)

![](https://a.amap.com/lbs/static/img/doc/doc_1757930065470_8266e.png)

2.下载得到的Zip文件，内部目录结构如下，每个文件都会对应 CustomMapStyleOptions 中一个接口：

|   |   |   |
|---|---|---|
|文件名称|文件内容说明|对应接口|
|style_extra.data|扩展内容，如网格背景色等|CustomMapStyleOptions.setStyleExtraData/setStyleExtraPath|
|style.data|具体样式配置|CustomMapStyleOptions.setStyleData/setStyleDataPath|
|textures.zip|纹理图片(zip文件)|CustomMapStyleOptions.setStyleTextureData/setStyleTexturePath|

注意：可将配置好的样式文件放入任意路径，比如“/mnt/sdcard/amap”

```
//该方法在AMap类中提供
this.aMap?.setCustomMapStyle(new CustomMapStyleOptions()
    .setEnable(true)
    .setStyleDataPath("file://docs/storage/Users/currentUser/style.data")
    .setStyleExtraPath("file://docs/storage/Users/currentUser/style_extra.data")
    .setStyleTexturePath("file://docs/storage/Users/currentUser/textures.zip")
)
```

注意：纹理功能需要[开通相关权限](https://lbs.amap.com/home/package?active=mapstyle)才可使用。

#### 二、设定在线样式文件（需要[开通权限](https://lbs.amap.com/home/package?active=mapstyle)）

1、如果觉得下载样式文件过程比较繁琐，也可以使用在线的方式调用：在自定义平台发布新样式后获得样式ID，并通过SDK的 setCustomMapStyleID 设置使用。如果需要变动样式，只需要在发布之后重新加载一次地图即可看到效果；

2、如果同时设置了在线样式和离线样式，会优先进行在线拉取，如果拉取失败了会再次读取离线样式；

3、示例代码：

```
//该方法在AMap类中提供
  this.aMap.setCustomMapStyle(
    new CustomMapStyleOptions()
    .setEnable(true)
    .setStyleId("您的styleid")//官网控制台-自定义样式 获取
    );
```

注意：纹理暂不支持在线拉取,如果调用了styleid也需要将纹理通过setStyleTexturePath设置了才会生效。
# 显示英文地图最后更新时间: 2025年11月17日

设置地图为英文地图

```
/**
 * 设置地图底图语言，目前支持中文底图和英文底图
 *
 * @param language 中文"zh_cn", 英文"en"
 * @since 2.2.4
 */
public static setMapLanguage(language: string)
```

效果如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1763087490591_b8fad.png)
# 使用离线地图最后更新时间: 2025年11月17日

## 离线地图与基本地图联动

高德3D 地图 SDK支持离线地图功能。（2D 地图 SDK 不支持离线地图功能）

离线地图可满足在无网络环境下查看地图信息的需求，在设备本地有离线地图数据的情况下，SDK 会优先加载离线地图。

## 离线地图UI组件（推荐）

自3D地图SDK V2.2.5起，新增离线地图UI组件，组件涵盖城市下载、暂停、更新、删除以及关键字城市查询等功能，是高德地图客户端离线地图功能的一个子集，UI交互风格上靠拢高德地图app，也考虑到与开发者应用UI的融合问题，尽可能的保持了简约极致。以下方法实现一键完成离线地图开发。

#### 增加权限

```
"requestPermissions": [
  {
    "name": 'ohos.permission.INTERNET',
  },
  {
    "name": 'ohos.permission.GET_NETWORK_INFO'
  }
]
```

#### 导入OfflineMapPage

离线地图使用的是OfflineMapPage组件，本组件在SDK内部实现，仅需要在当前Page中import { OfflineMapPage } from "@amap/amap_lbs_map3d" 即可使用OfflineMapPage组件。

#### 使用离线地图组件

```
import { OfflineMapPage } from "@amap/amap_lbs_map3d"

@Entry
@Component
export struct MapOfflineMapController {
  build() {
      OfflineMapPage()
  }
}
```

#### UI示意

![](https://a.amap.com/lbs/static/img/doc/doc_1763364960039_036ce.png)

## 自定义离线地图UI

#### 开始下载

可以根据城市编码和城市名称两种方式下载当前城市的离线地图。示例代码如下：

```
//构造OfflineMapManager对象 
this.amapManager = new OfflineMapManager(this.context, this)
//按照citycode下载
this.amapManager?.downloadByCityCode(citycode:string)；
//按照cityname下载
this.amapManager?.downloadByCityName(cityname:string)；
```

#### 暂停下载

通过代码暂停地图的下载:

示例代码如下：

```
this.amapManager?.pause();
```

#### 停止下载

停止所有当前正在执行的下载，包括下载队列中等待的部分。

示例代码如下：

```
this.amapManager.stop();
```

#### 更改离线地图存储目录

离线地图默认会下载到手机存储卡的“amap”目录下，也可以自定义路径：

通过 MapInitializer.sdcardDir 设置路径时，需要在 AMap 对象初始化之前进行，否则操作会无效。

```
// 设置应用单独的地图存储目录
MapsInitializer.sdcardDir = "自定义的目录";
```

#### 获取离线地图列表

其属性参数见下表：

|   |   |
|---|---|
|名称|说明|
|获取城市列表|OfflineMapManager.getOfflineMapCityList()|
|获取省列表|OfflineMapManager.getOfflineMapProvinceList()|
|获取已下载城市列表|OfflineMapManager.getDownloadOfflineMapCityList()|
|获取正在或等待下载城市列表|OfflineMapManager.getDownloadingCityList()|

## 检查更新

通过如下代码检查离线地图数据是否存在更新，检查更新操作会同时将本地离线地图配置文件更新成最新的，App 用户可依据最新的配置文件下载新版离线地图数据。

示例代码如下：

```
//通过updateOfflineCityByName方法判断离线地图数据是否存在更新
this.amapManager?.updateOfflineCityByName(city);
```

## 删除离线地图

执行 remove 操作时，需要等待 OfflineLoadedListener 回调之后才可以，否则（即使OfflineMapDownloadListener回调成功）操作将会无效。 

示例代码如下：

```
//删除某一城市的离线地图包
this.amapManager?.remove(city);
```

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
[开发](https://lbs.amap.com/api)  HarmonyOS NEXT 地图SDK  开发指南  在地图上绘制  绘制点标记

# 绘制点标记最后更新时间: 2025年11月17日

点标记用来在地图上标记任何位置，例如用户位置、车辆位置、店铺位置等一切带有位置属性的事物。

## 绘制默认 Marker

绘制 Marker 的代码如下

```
let options: MarkerOptions = new MarkerOptions();
options.setPosition(new LatLng(39.992520, 116.336170));
let marker = aMap.addMarker(options);
```

![](https://a.amap.com/lbs/static/img/doc/doc_1712734659242_e8448.png)

#### Marker 常用属性

|   |   |
|---|---|
|名称|说明|
|setPosition /getPosition|设置/获取标记位置在地图上的经纬度值|
|setTitle /getTitle|设置/获取标记的标题|
|setSnippet/getSnippet|设置/获取标记的文字描述|
|setDraggable/getDraggable|设置/获取标记是否可拖拽|
|setVisible/getVisible|设置/获取点标记是否可见|
|setAnchor|设置标记的锚点比例。锚点标记图标接触地图平面的点。图标的左顶点为（0,0）点，右底点为（1,1）点，默认为（0.5,1.0）|

## 绘制自定义 Marker

可根据实际的业务需求，在地图指定的位置上添加自定义的 Marker。MarkerOptions 是设置 Marker 参数变量的类，自定义 Marker 时会经常用到。

下面以自定义 Marker 图标为例进行代码说明：

```
// add Marker
let options: MarkerOptions = new MarkerOptions();
let bitmapDes = await BitmapDescriptorFactory.fromRawfilePath(globalContext, "location_map_gps_locked.png");
if (bitmapDes) {
  options.setIcon(bitmapDes);
}
options.setTitle('标记'); //设置标记的标题
options.setSnippet('详细信息') //设置标记的文字描述
options.setPosition(new LatLng(39.992520, 116.336170));
let marker1 = this.aMap?.addMarker(options);
```

提示

设置 Marker 的图标时，相同图案 icon 的 Marker 最好使用同一个BitmapDescriptor对象以节省内存空间，

## 绘制多个 Marker

```
let options1: MarkerOptions = new MarkerOptions().setPosition(new LatLng(39.992520, 116.336170)).setIcon(new BitmapDescriptor($rawfile('location_map_gps_locked.png'), 'location_map_gps_locked', 100, 100));
let options2: MarkerOptions = new MarkerOptions().setPosition(new LatLng(40.02380181476392, 116.43124537956452)).setIcon(new BitmapDescriptor($rawfile('location_map_gps_locked.png'), 'location_map_gps_locked', 100, 100));
let markerOptionsList: ArrayList<MarkerOptions> = new ArrayList<MarkerOptions>()
markerOptionsList.add(options1);
markerOptionsList.add(options2);
let markers = aMap.addMarkers(markerOptionsList, false);
```

## 绘制动画效果 Marker

自地图 SDK V2.2.4 版本起，SDK 提供了给 Marker 设置动画的方法，具体实现方法如下：

```
let animation: Animation = new ScaleAnimation(0, 1, 0, 1);
const linearCurve: ICurve = { interpolate: (interpolate: number) => interpolate };
animation.setInterpolator(linearCurve);
//整个移动所需要的时间
animation.setDuration(1000);
//设置动画
this.growMarker.setAnimation(animation);
//开始动画
this.growMarker.startAnimation();
```

## 移除 Marker

```
aMap.removeOverlay(marker.getId());
```

## 可触发的 Marker 事件

#### Marker 点击事件

```
aMap.setOnMarkerClickListener((marker: Marker): boolean => {
  // marker 被点击的 marker 对象
  // 返回true表示已处理点击事件，不再继续传递；返回false则继续传递
  console.log(marker.getId());
  return true
})
```

#### Marker 拖拽事件

```
//当 marker 开始被拖动时回调此方法, 这个 marker 的位置可以通过 getPosition() 方法返回。
// 这个位置可能与拖动的之前的 marker 位置不一样。
// marker 被拖动的 marker 对象。
const onMarkerDragStart = (marker: Marker): void => {
  // 处理拖动开始
  // marker 被拖动的 marker 对象
  // marker 的位置可以通过 getPosition() 方法返回
}
const onMarkerDrag = (marker: Marker): void => {
  // 处理拖动中
  // marker 被拖动的 marker 对象
  // marker 的位置可以通过 getPosition() 方法返回
}
const onMarkerDragEnd = (marker: Marker): void => {
  // 处理拖动结束
  // marker 被拖动的 marker 对象
  // marker 的位置可以通过 getPosition() 方法返回
}

// marker 拖动事件监听接口实例
const dragListener: OnMarkerDragListener = new OnMarkerDragListener(onMarkerDragStart, onMarkerDrag, onMarkerDragEnd);

//给 aMap 设置标记拖动监听器 
aMap.setOnMarkerDragListener(dragListener)
```

## 关于 InfoWindow 的设置

InfoWindow 是点标记的一部分，默认的 Infowindow 只显示 Marker 对象的两个属性，一个是 title 和另一个 snippet。

![](https://a.amap.com/lbs/static/img/doc/doc_1712735251437_174a9.png)

#### 常用属性

|   |   |   |
|---|---|---|
|名称|参数类型|说明|
|setInfoWindowEnable(enabled)|boolean|设置 Marker 覆盖物的 InfoWindow 是否允许显示,默认为 true<br><br>true：允许显示,false：不允许显示|
|setInfoWindowOffset(offsetX, offsetY)|number|设置 Marker 覆盖物的 InfoWindow 相对 Marker 的偏移<br><br>offsetX：InfoWindow 相对原点的横向像素偏移量，单位：像素<br><br>offsetY：InfoWindow 相对原点的纵向像素偏移量，单位：像素|
|autoOverturnInfoWindow(autoOverturn)|boolean|设置Marker覆盖物的InfoWindow是否自动旋转<br><br>true：表示自动翻转,false：表示不自动翻转|
|showInfoWindow()||显示 InfoWindow|
|hideInfoWindow()||隐藏 InfoWindow|
# 绘制线最后更新时间: 2025年11月04日

地图上绘制的线是由 Polyline 类定义实现的，线由一组经纬度（LatLng 对象）点连接而成。

## 绘制一条线

与点标记一样，Polyline 的属性操作集中在 PolylineOptions 类中，添加一条线的示例如下：

```
let options: PolylineOptions = new PolylineOptions();
options.add(new LatLng(39.925539, 116.279037)); //追加一个点到线段的坐标集合
options.add(new LatLng(39.925539, 116.520285));
aMap.addPolyline(options);
```

也可以使用addAll方法追加一批点到线段的坐标集合

```
let options: PolylineOptions = new PolylineOptions();
let polylineOptionsList :ArrayList<LatLng> = new ArrayList<LatLng>()
polylineOptionsList.add(new LatLng(39.925539, 116.279037))
polylineOptionsList.add(new LatLng(39.925539, 116.520285))
options.addAll(polylineOptionsList)
aMap?.addPolyline(options);
```

![](https://a.amap.com/lbs/static/img/doc/doc_1712735500736_12bbe.png)

## 绘制虚线

示例如下

```
let options: PolylineOptions = new PolylineOptions();
options.add(new LatLng(39.925539, 116.279037));
options.add(new LatLng(39.925539, 116.520285));
aMap.addPolyline(options.setDottedLine(true).setColor(1125058090).setWidth(20));
```

![](https://a.amap.com/lbs/static/img/doc/doc_1712735519329_8ec87.png)

## 绘制线常用方法

|   |   |
|---|---|
|名称|说明|
|setColor|设置线段的颜色，需要传入32位的 ARGB 格式。默认：黑色( 0xff000000)|
|setDottedLine|设置是否画虚线，默认：false（画实线）画实线|
|setLineCapType|设置 Polyline 尾部形状|
|setLineJoinType|设置 Polyline 连接处形状|
|setTransparency|设置线段的透明度 0~1，默认：1（表示不透明）表示不透明|
|setVisible|设置线段的可见性。默认：可见|
|setWidth|设置线段的宽度，默认：10|
|setZIndex|设置线段Z轴的值|
|setGeodesic|设置线段是否为大地曲线，默认：false（不画大地曲线）|
# 绘制弧线最后更新时间: 2025年10月10日

地图上绘制的线是由 Arc 类定义实现的，线由一组三个经纬度坐标（LatLng对象）点连接而成圆弧。

## 第一步，绘制弧线

```
let x = 39.904979;
let y = 116.40964;
// 绘制一个经过乌鲁木齐经过北京到哈尔滨弧形
for (let i = 0; i < 10; i++) {
  let x_ = 0;
  let y_ = 0;
  x_ = Math.random() * 0.5 - 0.25;
  y_ = Math.random() * 0.5 - 0.25;
  let x_2 = 0;
  let y_2 = 0;
  x_2 = Math.random() * 0.5 - 0.25;
  y_2 = Math.random() * 0.5 - 0.25;
  let x_3 = 0;
  let y_3 = 0;
  x_3 = Math.random() * 0.5 - 0.25;
  y_3 = Math.random() * 0.5 - 0.25;
  // 数据准备
  let arcOptions: ArcOptions = new ArcOptions().point(
    new LatLng(x+x_, y+y_), new LatLng(x+x_3,y+y_3),
    new LatLng(x+x_2, y+y_2)).setStrokeColor(ColorUtil.colorStringToNumber("#ff0000"))
  // 绘制弧线并保存句柄
  this.arcList.push(this.aMap.addArc(arcOptions));
}
```

## 第二步，修改弧线属性

HeatmapTileProvider 是生成热力图的核心类，一些基础用法可参考如下代码：

```
// 通过句柄修改弧线的属性
this.arcList.forEach((item: Arc | undefined) =>{
  const colorNow = item?.getStrokeColor()
  if(colorNow == ColorUtil.colorStringToNumber('#00ff00')){
    item?.setStrokeColor(ColorUtil.colorStringToNumber('#ff0000'))
  }else{
    item?.setStrokeColor(ColorUtil.colorStringToNumber('#00ff00'))
  }
})
```

效果图如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1758608086230_8266e.png)
# 绘制面最后更新时间: 2025年11月04日

地图上的面分为圆形和多边形两种

## 绘制圆

圆形由 Circle 类定义实现，构造一个圆形需要确定它的圆心和半径，具体的示例代码如下：

```
let circleOptions: CircleOptions = new CircleOptions();
    circleOptions.setRadius(15000); //设置圆的半径，单位:米
    circleOptions.setCenter(new LatLng(39.996441, 116.411146)); //设置圆心经纬度坐标
    circleOptions.setFillColor(0xffff0000); //设置圆的填充颜色
    circleOptions.setStrokeColor(0xff00ff00); //设置圆的边框颜色

    let circleHoleOptions: CircleHoleOptions = new CircleHoleOptions();
    circleHoleOptions.setRadius(5000);
    circleHoleOptions.setCenter(new LatLng(39.996441, 116.411146));
    circleOptions.addHoles(circleHoleOptions); //添加空心洞的配置项
    aMap.addCircle(circleOptions)
```

![](https://a.amap.com/lbs/static/img/doc/doc_1712735656407_edcf9.png)

## 绘制多边形

多边形是由 Polygon 类定义的一组在地图上的封闭线段组成的图形，它由一组 LatLng 点按照传入顺序连接而成的封闭图形。与绘制线类似，面的属性操作集中在 PolygonOptions 中。

```
let polygonOptions: PolygonOptions = new PolygonOptions();
polygonOptions.add(new LatLng(39.781892, 116.293413));
polygonOptions.add(new LatLng(39.787600, 116.391842));
polygonOptions.add(new LatLng(39.733187, 116.417932));
polygonOptions.add(new LatLng(39.704653, 116.338255));
polygonOptions.setFillColor(0xFFFF0000);

let polygonHoleOptions: PolygonHoleOptions = new PolygonHoleOptions;
polygonHoleOptions.add(new LatLng(39.781892 - 0.02, 116.293413 + 0.02));
polygonHoleOptions.add(new LatLng(39.787600 - 0.02, 116.391842 - 0.02));
polygonHoleOptions.add(new LatLng(39.733187 + 0.02, 116.417932 - 0.02));
polygonHoleOptions.add(new LatLng(39.704653 + 0.02, 116.338255 + 0.02));
let list: ArrayList<PolygonHoleOptions> = new ArrayList();
list.add(polygonHoleOptions);
polygonOptions.setHoleOptions(list);
aMap.addPolygon(polygonOptions);
```

![](https://a.amap.com/lbs/static/img/doc/doc_1712735831426_97f74.png)
# 绘制图片图层最后更新时间: 2025年09月29日

## 简介

定义在地图上绘制一个 Ground 覆盖物（一张图片以合适的大小贴在地图上的图片层）

- 位置： 可以通过设置中心点或者图片区域来确定图片层的位置。
    
- 图片： 覆盖物的贴图。
    
- 角度： 图片从正北开始，顺时针方向旋转，中心点为锚点。
    
- Z轴 ： Z轴是控制地图覆盖物（overlay）之间的绘制层次的参数。这个参数能够控制Circles、Polygons、Polyline的绘制层次，但不会影响marker。Z轴数值越大的覆盖物（overlay）将会绘制在更上层。如果两个及两个以上覆盖物（overlay）的Z轴数值相同，则最后的绘制结果是随机的 。覆盖物（overlay）的默认为Z轴为0。
    
- 可见：这个属性表示了覆盖物是否可以显示在地图上。默认为可见。
    

![](https://a.amap.com/lbs/static/img/doc/doc_1758607654947_83b50.jpeg)

## 展示Ground覆盖物

#### 第1步 设置覆盖物属性

```
let options: GroundOverlayOptions = new GroundOverlayOptions();

let texture = await BitmapDescriptorFactory.fromRawfilePath(globalContext, 'groundoverlay.png');

if (texture) {
  options.image(texture); // 设置图片
}
options.position(new LatLng(39.936713,116.386475), 1); // 根据位置和宽设置ground覆盖物
let southwest: LatLng = new LatLng(39.935029, 116.384377)
let northeast: LatLng = new LatLng(39.939577, 116.388331)
let bounds: LatLngBounds = new LatLngBounds(southwest, northeast)
options.positionFromBounds(bounds); // 根据矩形区域设置ground覆盖物的位置
options
  .anchor(0.5, 0.5) // 设置图片的对齐方式
  .setTransparency(0.7) // 设置ground覆盖物的透明度
```

#### 第2步 添加覆盖物

```
// 添加一个groundOverlay
aMap.addGroundOverlay(options);
```

## 绘制Ground覆盖物常用方法

|   |   |
|---|---|
|名称|说明|
|anchor(anchorU: number, anchorV: number)|设置图片的对齐方式|
|position(location: LatLng \| undefined, width: number, height?: number)|根据位置和宽高设置ground覆盖物|
|positionFromBounds(paramLatLngBounds: LatLngBounds)|根据矩形区域设置ground覆盖物的位置|
|setBearing(bearing: number)|设置ground覆盖物从正北顺时针的角度|
|setZIndex(zIndex: number)|设置ground覆盖物的z轴指数|
|visible(visible: boolean)|设置ground覆盖物是否可见|
|setTransparency(transparency: number)|设置ground覆盖物的透明度|
# 绘制海量点图层最后更新时间: 2025年09月29日

在地图上加载显示海量点，支持高达十万级点位的流畅显示。

## 第 1 步：初始化 MapView 并获取 AMap 实例

通过 MapViewComponent 创建地图视图，并在回调中获取底层 AMap 对象，用于后续操作。

```
@Builder
buildMapMultiPointOverlay() {
  Stack() {
    MapViewComponent({ mapViewName: Constants.MAP_MULTIPOINTOVERLAY_FUNC })
  }
  .width('100%')
  .height('100%')
}

private mapViewCreateCallback = (mapview?: MapView, mapViewName?: string) => {
  if (!mapview || mapViewName !== Constants.MAP_MULTIPOINTOVERLAY_FUNC) return;

  this.mapView = mapview;
  this.mapView.onCreate();

  this.mapView.getMapAsync(async (map: AMap) => {
    this.aMap = map;
    await this.setupMultiPointOverlay(); 
  });
};
```

## 第 2 步：准备点位数据源

支持两种方式加载点位数据：

#### 方式一：从本地文件加载（推荐用于真实数据）

将经纬度数据以 CSV 格式保存在 resources/rawfile/point10w.txt 文件中，每行格式为：

经度,纬度 116.397026,39.90976 116.401,39.912 ...

```
private async loadPointItemsFromFile(): Promise<MultiPointItem[]>
```

#### 方式二：动态生成测试数据（用于调试）

可生成指定数量的随机点，中心坐标为中国北京附近。

```
const testPoints = this.generateTestPoints(10000);
```

## 第 3 步：创建 MultiPointOverlay 图层

配置 MultiPointOverlayOptions，设置图标、锚点及初始点集。

```
const overlayOptions = new MultiPointOverlayOptions();
overlayOptions.icon(bitmapDescriptor);        // 设置点图标
overlayOptions.anchor(0.5, 0.5);              // 图标中心对齐
overlayOptions.setMultiPointItems([]);        // 初始为空数组
this.multiPointOverlay = this.aMap.addMultiPointOverlay(overlayOptions);
```

其中：

|   |   |
|---|---|
|参数|说明|
|icon(BitmapDescriptor)|点的显示图标，建议尺寸较小以提升性能|
|anchor(x, y)|图标锚点位置，(0.5, 0.5) 表示居中对齐|
|setMultiPointItems(items)|设置要渲染的点列表|

## 第 4 步：加载并渲染点数据

调用 loadAndRenderPoints() 方法异步加载文件中的点数据，并更新到 MultiPointOverlay。

流程如下：

1. 读取 rawfile/point10w.txt 文件内容；
    
2. 解析每一行为 LatLng 坐标；
    
3. 构造 MultiPointItem 并绑定自定义数据；
    
4. 保存至 this.allPointItems（用于点击检测）；
    
5. 调用 multiPointOverlay.setItems(items) 更新视图；
    
6. 启用图层 .setEnable(true)。
    

## 第 5 步：实现地图点击交互

监听地图点击事件，在所有点中查找距离最近的一个，并用红色 Marker 高亮显示。

```
this.aMap.setOnMapClickListener(async (latLng: LatLng) => {
  let closestItem: MultiPointItem | null = null;
  let minDistSq = 0.1; // 阈值

  for (const item of this.allPointItems) {
    const dLat = item.getLatLng().latitude - latLng.latitude;
    const dLon = item.getLatLng().longitude - latLng.longitude;
    const distSq = dLat * dLat + dLon * dLon;
    if (distSq < minDistSq) {
      minDistSq = distSq;
      closestItem = item;
    }
  }

  if (closestItem) {
    // 显示/移动红色 Marker
    if (!this.marker) {
      const redIcon = await BitmapDescriptorFactory.defaultMarkerASync(globalContext, BitmapDescriptorFactory.HUE_RED);
      const options = new MarkerOptions();
      options.setIcon(redIcon);
      this.marker = this.aMap?.addMarker(options);
    }
    this.marker.setPosition(closestItem.getLatLng());
    this.marker.setZIndex(1000); // 置顶显示
  }
});
```

## 其他：生命周期管理

在页面销毁时释放资源：

```
aboutToDisappear(): void {
  this.isDestroy = true;
  MapViewManager.getInstance().unregisterMapViewCreatedCallback(this.mapViewCreateCallback);
  if (this.mapView) {
    this.mapView.onDestroy();
    this.mapView = undefined;
    this.aMap = undefined;
  }
}
```

![](https://a.amap.com/lbs/static/img/doc/doc_1758607787480_fb5c8.png)
# 点平滑移动最后更新时间: 2025年09月29日

功能说明：根据输入的关键点和时间参数，实现点的平滑移动效果。

使用场景：可应用到展示车辆行驶轨迹、用户移动轨迹等场景。

效果示例：

![](https://a.amap.com/lbs/static/img/doc/doc_1758607919295_18284.jpeg)

#### 如何实现点平滑移动

MovingPointOverlay 代码位置：

src/main/ets/com/amap/api/utils/overlay/MovingPointOverlay.ets

#### 相关接口

- 设置平滑移动的经纬度数组：public setPoints(List points):void
    
- 设置平滑移动的总时间：public setTotalDuration(int duration):void
    
- 设置移动Marker的图标 ：public setDescriptor(BitmapDescriptor descriptor):void
    
- 开始平滑移动 ：public startSmoothMove():void
    
- 停止平滑移动 ：public stopMove():void
    

代码调用示例:

```
// 读取轨迹点
    let points:ArrayList<LatLng> = this.readLatLngs();

    // 实例 MovingPointOverlay 对象
    if(this.smoothMarker == null && this.mAMap) {
      // 设置 平滑移动的 图标
      let descriptor = BitmapDescriptorFactory.fromRawfilePathSync(this.context,"icon_car.png")
      if(descriptor){
        this.marker = this.mAMap.addMarker(new MarkerOptions().setIcon(descriptor).setAnchor(0.5,0.5));
        if(this.marker)
          this.smoothMarker = new MovingPointOverlay(this.mAMap, this.marker);
      }
    }

    // 取轨迹点的第一个点 作为 平滑移动的启动
    let drivePoint:LatLng = points[0];
    let pair = SpatialRelationUtil.calShortestDistanceLatLng(points, drivePoint);
    if(pair && pair[0])
      points[pair[0]]=drivePoint;
    let subList = points.subArrayList(pair?.[0], points.length);

    // 设置轨迹点
    this.smoothMarker?.setPoints(subList);
    // 设置平滑移动的总时间  单位  秒
    this.smoothMarker?.setTotalDuration(40);
    this.smoothMarker?.startSmoothMove();
```
# 绘制热力图最后更新时间: 2025年11月17日

## 绘制热力图

热力图功能提供将业务数据展示在地图上，可以给使用者直观描述一个区域的人员，车辆等事物的热度情况。

#### 第一步，组织热力图数据

以下以本地模拟数据为例，简单说明 SDK 热力图需要的是经纬度点数组/列表数据。

示例代码如下：

```
// 第一步： 生成热力点坐标列表
let latlngs: LatLng[] = [];
let x = 39.904979;
let y = 116.40964;

for (let i = 0; i < 1; i++) {
  let x_ = 0;
  let y_ = 0;
  x_ = Math.random() * 0.5 - 0.25;
  y_ = Math.random() * 0.5 - 0.25;
  latlngs.push(new LatLng(x + x_, y + y_))
}
```

#### 第二步，构建热力图 HeatmapTileProvider

HeatmapTileProvider 是生成热力图的核心类，一些基础用法可参考如下代码：

```
// 第二步： 构建热力图 TileProvider
let builder: HeatMapBuilder = new HeatMapBuilder();
builder.setData(latlngs);
// 设置热力图绘制的数据
builder.setGradient(HeatMapController.ALT_HEATMAP_GRADIENT); // 设置热力图渐变，有默认值 DEFAULT_GRADIENT，可不设置该接口
// Gradient 的设置可见参考手册
// 构造热力图对象
let heatmapTileProvider: HeatmapTileProvider | undefined = builder.build();
```

#### 第三步，绘制热力图图层

通过 TileOverlay 绘制热力图，方法如下：

```
// 第三步： 构建热力图参数对象
let tileOverlayOptions: TileOverlayOptions = new TileOverlayOptions();
if (heatmapTileProvider) {
  tileOverlayOptions.tileProvider(heatmapTileProvider); // 设置瓦片图层的提供者
}
// 第四步： 添加热力图
this.tileOverlay = this.mAMap?.addTileOverlay(tileOverlayOptions);
```

a

效果图如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1758607988774_09dd8.png)

## 绘制蜂窝热力图

蜂窝热力图功能提供将业务数据展示在地图上，以蜂窝的形式给使用者直观展示热度情况。

#### 第一步，组织蜂窝热力图数据

以下以本地模拟数据为例，简单说明 SDK 热力图需要的是经纬度点数组/列表数据。

示例代码如下：

```
// 第一步： 生成热力点坐标列表，数据格式（119.518251,35.683927,1159）
let heatMapStr = Utils.uint8ArrayToString(HoneycombHeatMapController.readFileContentsFromAssets(getContext(), "heatmap/heatmap_honey.data"));
let heatMapStrs = heatMapStr.split("\n");
let weightlatlngs = new ArrayList<WeightedLatLng>();
for (let str of heatMapStrs) {
  let dataItem = str.split(",");
  if (dataItem && dataItem.length == 3) {
    weightlatlngs.add(new WeightedLatLng(new LatLng(Number.parseFloat(dataItem[1]), Number.parseFloat(dataItem[0])), Number.parseFloat(dataItem[2])))
  }
}
let colors = [
  ColorUtil.colorStringToNumber("#ecda9a"),
  ColorUtil.colorStringToNumber("#efc47e"),
  ColorUtil.colorStringToNumber("#f3ad6a"),
  ColorUtil.colorStringToNumber("#f7945d"),
  ColorUtil.colorStringToNumber("#f97b57"),
  ColorUtil.colorStringToNumber("#f66356"),
  ColorUtil.colorStringToNumber("#ee4d5a")
];
let startPoints = new Array<number>(colors.length);
for(let i = 0;i < startPoints.length; i++) {
  startPoints[i] = i * 1.0 / startPoints.length
}
```

#### 第二步，构建热力图 HeatMapLayerOptions

HeatMapLayerOptions 是生成热力图的核心类，一些基础用法可参考如下代码：

```
// 第二步： 构建蜂窝热力图 HeatMapLayerOptions
let heatMapLayerOptions = new HeatMapLayerOptions();

// 带权重的经纬度
heatMapLayerOptions.weightedData(weightlatlngs);

// 指定颜色和颜色变化索引
let gradient = new Gradient(colors, startPoints);
heatMapLayerOptions.gradient(gradient);
// heatMapLayerOptions.gradient(HeatMapLayerOptions.DEFAULT_GRADIENT);

// 大小和间隔
heatMapLayerOptions.size(6000);
heatMapLayerOptions.gap(300);

// 最大最小缩放级别
heatMapLayerOptions.setMinZoom(5);
heatMapLayerOptions.setMaxZoom(19);

// 整个覆盖物的透明度
heatMapLayerOptions.opacity(0.85);

// 热力图类型为蜂窝
heatMapLayerOptions.setType(HeatMapLayerOptions.TYPE_HEXAGON);

// 控制在底图文字的上面，默认底图文字级别是0
heatMapLayerOptions.setZIndex(1);
```

#### 第三步，绘制蜂窝热力图图层

通过 HeatMapLayerOptions 绘制热力图，方法如下：

```
this.layer = this.mAMap?.addHeatMapLayer(heatMapLayerOptions);
```

#### 第四步，注册地图点击事件，回调位置的热力情况

通过 设置点击事件，获取经纬度信息，通过经纬度获取位置的热力情况，方法如下：

```
// 获取指定位置的热力情况
this.mAMap?.setOnMapClickListener((latLng: LatLng) => {
  if (this.layer && this.mAMap && latLng) {
    let item: HeatMapItem | undefined = this.layer.getHeatMapItem(latLng);
    if (item) {
      let stringBuffer = ""
      stringBuffer += "热力中心："
      stringBuffer += (item.getCenter() + "\n");
      stringBuffer += "热力值："
      stringBuffer +=  (item.getIntensity() + "\n");
      let indexes = "";
      for(let integer of item.getIndexes()) {
        indexes += integer + ",";
      }
      stringBuffer += ("热力索引：" + indexes + "\n");
      stringBuffer += ("数据数量：" + item.getIndexes().length);
      this.updateHeatItemTv(stringBuffer.toString());
    } else {
      this.updateHeatItemTv("未找到热力信息");
    }


  }
})
```

a

效果图如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1763089128689_df426.png)
# 绘制3D模型最后更新时间: 2025年11月17日

```
public async addGL3DModel(): Promise<void> {
    // vertexData string
    let options = new GL3DModelOptions();
    let data = globalContext.resourceManager.getRawFileContentSync('obj/logistic_detail_3d_truck.obj');
    let decoder = util.TextDecoder.create('utf-8');
    let content = decoder.decodeWithStream(new Uint8Array(data));

    options.angle(50)
        .position(new LatLng(39.955436, 116.335769))
        .setAltitude(1000)
        .setFixDisplaySize(100, 100)
        .setFixedDisplaySizeEnabled(true)
        .setModelFixedLength(1000)
        .setVisible(true)
        .setZIndex(5)
            // .setSnippet("gl3dmodel")
            // .setTitle("amap3d")
        .vertexData(content)

    let texture = await BitmapDescriptorFactory.fromRawfilePath(globalContext,
        'obj/babel_order_logistic_detail_3d_truck_transport.png');
    if (texture) {
        options.textureDrawable(texture);
    }

    this.gl3DModel = this.aMap?.addGL3DModel(options);
    this.gl3DModel?.showInfoWindow();
}
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763088367918_883dd.png)
# 轨迹纠偏最后更新时间: 2025年11月17日

轨迹记录、纠偏类需求强烈建议您使用高德开放平台提供的猎鹰SDK或者猎鹰服务API，后续版本的地图SDK会逐步停止轨迹纠偏接口的维护。

## 简介

轨迹纠偏可帮助您将您记录的行车轨迹点进行抽稀、纠偏操作，将轨迹匹配到道路上，提供平滑的绘制效果，并计算行驶里程（地图SDK V2.2.5以上支持）；也可以通过结合高德定位帮助您记录真实行车轨迹（地图SDK V2.2.5版本以上支持）。

值得注意的是，目前该功能只支持将驾车轨迹纠正到路上。

![](https://a.amap.com/lbs/static/img/doc/doc_1763088792929_539f7.png)

## 结合定位轨迹纠偏（自2.2.5版本起支持）

### 第 1 步 初始化LBSTraceClient

开始记录轨迹，每2s记录一次轨迹，每隔5个点合并请求一次纠偏并回调。

```
this.traceClient = LBSTraceClient.getInstance(getContext());
```

### 第 2 步 开启轨迹纠偏

```
this.traceClient.startTrace(this.traceStatusListener);//开始采集,需要传入一个状态回调监听。
```

### 第 3 步 解析返回结果

```
  traceStatusListener: TraceStatusListener = {
     onTraceStatus:(locations?:ArrayList<TraceLocation>,rectifications?:ArrayList<LatLng>,errorInfo?:string)=>{
     //locations 定位得到的轨迹点集，rectifications 纠偏后的点集，errorInfo 轨迹纠偏错误信息
    }
  }
```

### 第 4 步 结束轨迹纠偏

```
this.traceClient.stopTrace()//在不需要轨迹纠偏时（如行程结束），可调用此接口结束纠偏
```

## 自有轨迹纠偏

### 第 1 步，初始化LBSTraceClient

```
this.mTraceClient = new LBSTraceClient(getContext())
```

### 第 2 步，构造轨迹点数据 List

需要按照 TraceLocation 定义好的格式构造轨迹点 List。

TraceLocation 的信息通过下表中的方法设置：

需要您注意的是，

1、必填信息的缺失会导致纠偏失败，非必填信息的缺失会在一定程度影响最终纠偏结果，因此尽可能的多提供以下信息是确保绘制一条平滑轨迹的最佳方案。建议使用HarmonyOS定位SDK中高精度，且有速度和角度返回的位置点数据。

2、传入的经纬度点，必须是国内的坐标，轨迹纠偏功能不支持国外的坐标点的纠偏。

|   |   |   |   |
|---|---|---|---|
|方法名|参数说明|返回值说明|方法效果|
|setLongitude(mLongitude:number)|mLongitude：经度，必填。|void|设置经度。|
|setLatitude(mLatitude:number)|mLatitude：纬度，必填。|void|设置纬度。|
|setSpeed(mSpeed:number)|mSpeed：速度，必填。|void|设置速度。|
|setBearing(mBearing:number)|mBearing：方向角，必填。|void|设置方向角。|
|setTime(mTime:number)|mTime：时间，必填。|void|设置时间。|

### 第 3 步，进行轨迹纠偏

轨迹纠偏支持传入多种坐标系（高德、GPS原始坐标以及百度）的轨迹点数据，并且可支持多条数据同时纠偏。进行轨迹纠偏的方法如下：

|   |   |   |   |
|---|---|---|---|
|方法名|参数说明|返回值说明|方法效果|
|queryProcessedTrace|lineID： 用于标示一条轨迹，支持多轨迹纠偏，如果多条轨迹调起纠偏接口，则lineID需不同。<br><br>locations ： 一条轨迹的点集合。建议为一条行车GPS高精度定位轨迹。<br><br>type： 轨迹坐标系，目前支持高德 LBSTraceClient.TYPE_AMAP;<br><br>GPS LBSTraceClient.TYPE_GPS;百度 LBSTraceClient.TYPE_BAID。<br><br>listener ： 轨迹纠偏回调|void|进行轨迹纠偏，返回纠偏后的轨迹数据。|

```
this.mTraceClient.queryProcessedTrace(this.mSequenceLineID,this.mTraceList,this.mCoordinateType,this.traceListener)
```

### 第 4 步，获取纠偏后的数据

#### 1、实现 TraceListener 监听器。

TraceListener 监听器作为轨迹纠偏方法的参数传入后，通过其回调函数，获取纠偏点数据、轨迹的总距离。

#### 2、轨迹纠偏结束回调。

只要当前轨迹点纠偏全部成功就一定会进入 onFinished 回调。该回调方法的说明如下：

|   |   |   |   |
|---|---|---|---|
|方法名|参数说明|返回值说明|方法效果|
|onFinished|lineID：用于标示一条轨迹，支持多轨迹纠偏，如果多条轨迹调起纠偏接口，则lineID需不同。<br><br>linepoints：整条轨迹经过纠偏后点的经纬度集合。<br><br>distance：轨迹经过纠偏后总距离，单位米。<br><br>waitingtime：该轨迹中间停止时间，以GPS速度为参考，单位秒。|void|传入的轨迹点数据全部纠偏完成时回调。|

#### 3、轨迹纠偏失败回调。

当传入的轨迹点数据出现以下几种情况，会因为参数错误导致纠偏失败，进入 onRequestFailed 回调。

- 网络不连通。
    
- 原始轨迹数据只有1个点。
    

该回调方法的说明如下

|   |   |   |   |
|---|---|---|---|
|方法名|参数说明|返回值说明|方法效果|
|onRequestFailed|lineID：用于标示一条轨迹，支持多轨迹纠偏，如果多条轨迹调起纠偏接口，则lineID需不同。<br><br>errorInfo：轨迹纠偏失败原因。|void|轨迹纠偏发生错误时回调。|

#### 4、轨迹纠偏过程回调。

我们采用分段的方式处理轨迹数据，按分段的顺序，每完成一段轨迹数据的纠偏就会进 onTraceProcessing 回调。

采用分段方式有以下两个优势：

- 当轨迹点数据量大的时候，可减少处理整条轨迹数据的等待时间。
    
- 当有部分的轨迹数据不符合要求导致纠偏失败时，通过过程回调可看到已完成部分的结果。
    

该回调方法的说明如下：

|   |   |   |   |
|---|---|---|---|
|方法名|参数说明|返回值说明|方法效果|
|onTraceProcessing|lineID：用于标示一条轨迹，支持多轨迹纠偏，如果多条轨迹调起纠偏接口，则lineID需不同。<br><br>index：一条轨迹分割为多个段,标示当前轨迹段索引。<br><br>segments：一条轨迹分割为多个段，segments标示当前轨迹段经过纠偏后经纬度点集合。|void|一条轨迹分割为多个段，按索引顺序回调其中一段。|

```
  private traceListener:TraceListener = {
    /**
     * 轨迹纠偏失败回调
     */
    onRequestFailed:(lineID: number, errorInfo: string)=>{
      this.getUIContext().getPromptAction().showToast({ message: errorInfo})
      if (this.mOverlayList.hasKey(lineID)) {
        const overlay = this.mOverlayList.get(lineID)
        overlay.setTraceStatus(TraceOverlay.TRACE_STATUS_FAILURE)
        this.setDistanceWaitInfo(overlay)
      }
    },
    /**
     * 轨迹纠偏过程回调
     */
    onTraceProcessing:(lineID: number,index: number,segments: ArrayList<LatLng>)=>{
      if (!segments) {
        return
      }
      if (this.mOverlayList.hasKey(lineID)) {
        const overlay = this.mOverlayList.get(lineID)
        overlay.setTraceStatus(TraceOverlay.TRACE_STATUS_PROCESSING)
        overlay.add(segments)
      }

    },
    /**
     * 轨迹纠偏结束回调
     */
    onFinished:(lineID: number,linepoints:ArrayList<LatLng>, distance:number,waitingtime: number)=>{
      this.getUIContext().getPromptAction().showToast({ message: 'onFinished'})
      if (this.mOverlayList.hasKey(lineID)) {
        const overlay = this.mOverlayList.get(lineID)
        overlay.setTraceStatus(TraceOverlay.TRACE_STATUS_FINISH)
        overlay.setDistance(distance)
        overlay.setWaitTime(waitingtime)
        this.setDistanceWaitInfo(overlay)
      }
    }
  }
```

### 注意事项

1、作为地图SDK的功能，需要设置正确的高德Key才能保证轨迹纠偏功能的正确使用。

2、若您对纠偏结果存疑（例如：距离计算不准确，轨迹不正确等等），可将您的轨迹点转成标准的 JSON 格式文件，通过工单提交给我们（注意：我们只接受转成我们能验证格式的轨迹点数据）。

      a）标准的 JSON 格式文件可通过 http://tool.oschina.net/codeformat/json 转化。

      b）检查参数的字段名称是否与下表吻合，不一样请修改成一样。

|   |   |
|---|---|
|经度|lon|
|纬度|lat|
|时间（单位：毫秒）|loctime|
|速度（单位：Km/h）|speed|
|角度（单位：度）|bearing|

 c）通过工单提交给我们
 # 控件交互最后更新时间: 2025年11月17日

## 地图logo控件

高德地图的 logo 默认在左下角显示，不可以移除，但支持调整到固定位置。设置的方法是：

```
public setLogoPosition(position: number): void //设置“高德地图”Logo的位置
```

|   |   |
|---|---|
|名称|位置说明|
|AMapOptions.LOGO_POSITION_BOTTOM_CENTER|Logo位置（地图底部居中）|
|AMapOptions.LOGO_POSITION_BOTTOM_LEFT|Logo位置（地图左下角）|
|AMapOptions.LOGO_POSITION_BOTTOM_RIGHT|Logo位置（地图右下角）|
|AMapOptions.LOGO_MARGIN_LEFT|LOGO边缘MARGIN（左边）|
|AMapOptions.LOGO_MARGIN_BOTTOM|LOGO边缘MARGIN（底部）|
|AMapOptions.LOGO_MARGIN_RIGHT|LOGO边缘MARGIN（右边）|

## 指南针控件

指南针用于向 App 端用户展示地图方向，默认不显示。通过如下接口控制其显示：

```
public setCompassEnabled(enabled: boolean): void //设置指南针是否可见
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763087640303_d199c.jpeg)

## 比例尺控件

比例尺控件（最大比例是1：10m,最小比例是1：1000Km），位于地图右下角，可控制其显示与隐藏，设置的方法是：

```
public setScaleControlsEnabled(enabled: boolean): void //控制比例尺控件是否显示
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763087668619_6a878.png)
# 手势交互最后更新时间: 2025年11月17日

地图 SDK 提供了多种手势供用户与地图之间进行交互，如缩放、旋转、拖拽、倾斜。这些手势默认开启，如果想要关闭某些手势，可以通过 UiSettings 类提供的接口来控制手势的开关。

## 手势方法说明

#### 以下是控制手势生效与否的方法：

|   |   |
|---|---|
|名称|说明|
|setZoomGesturesEnabled(boolean)|设置缩放手势是否可用|
|setScrollGesturesEnabled(boolean)|设置拖拽手势是否可用|
|setRotateGesturesEnabled(boolean)|设置旋转手势是否可用|
|setTiltGesturesEnabled(boolean)|设置倾斜手势是否可用|
|setGestureScaleByMapCenter(boolean)|设置是否以地图中心点缩放|
|setAllGesturesEnabled(boolean)|设置所有手势是否可用|

#### 以下是检测手势是否生效的方法：

|   |   |
|---|---|
|名称|说明|
|isZoomGesturesEnabled()|缩放手势是否可用|
|isScrollGesturesEnabled()|拖拽手势是否可用|
|isRotateGesturesEnabled()|旋转手势是否可用|
|isTiltGesturesEnabled()|倾斜手势是否可用|
|isGestureScaleByMapCenter()|是否地图中心点缩放|

## 缩放手势

缩放手势可改变地图的缩放级别，地图响应的手势如下：

- 双击地图可以使缩放级别增加1 (放大)
    
- 两个手指捏/拉伸
    

以下是控制缩放手势开启关闭的代码：

```
aMap.getUiSettings()?.setZoomGesturesEnabled(boolean);
```

## 拖拽手势

您可以用手指拖动地图四处滚动（平移）或用手指滑动地图（动画效果），也可以禁用或开启平移（滑动）手势。

以下介绍控制拖拽手势开启关闭的方法，示例代码如下：

```
aMap.getUiSettings()?.setScrollGesturesEnabled(boolean);
```

## 旋转手势

您可以用两个手指在地图上转动，可以旋转地图，也可以禁用旋转手势。

以下介绍控制旋转手势开启关闭的方法，示例代码如下：

```
aMap.getUiSettings()?.setRotateGesturesEnabled(boolean);
```

## 倾斜手势

用户可以在地图上放置两个手指，移动它们一起向下或向上去增加或减小倾斜角，也可以禁用倾斜手势。

以下是控制倾斜手势开启关闭的代码：

```
aMap.getUiSettings()?.setTiltGesturesEnabled(boolean);
```

## 地图中心点缩放

用户可以设置地图缩放位置，可以以中心点缩放或在缩放位置缩放。

以下是控制地图中心点缩放开启关闭的代码：

```
aMap.getUiSettings()?.setGestureScaleByMapCenter(boolean);
```

## 所有手势是否可用

用户可以统一设置地图是否支持手势交互。

以下是控制所有手势是否可用的代码：

```
aMap.getUiSettings()?.setAllGesturesEnabled(boolean);
```

## 指定屏幕中心点的手势操作

在对地图进行手势操作时（滑动手势除外），可以指定屏幕中心点后执行相应手势。

指定屏幕中心点的接口如下，在AMap类中：

```
/**
 * 设置屏幕上的某个像素点为地图中心点。
 * <p>使用该方法设置后，地图将以所设置的屏幕坐标点为中心进行旋转、倾斜。同时， {@link #moveCamera(CameraUpdate) } 方法也将会以此坐标点为中心进行设置。
 *
 * @param x 屏幕像素点x轴坐标。
 * @param y 屏幕像素点y轴坐标。
 * @since v2.2.0
 */
public setPointToCenter(x: number, y: number): void
```

开启以中心点进行手势操作的接口如下，在UiSettings类中：

```
/**
 * 设置是否以地图中心点缩放 <br>
 * 注：优先级低于{@link AMap#setPointToCenter(int, int)}
 *
 * @param isGestureScaleByMapCenter true:以地图中心的进行缩放,false:不以地图中心的进行缩放
 * @since 1.0.0
 */
public setGestureScaleByMapCenter(isGestureScaleByMapCenter: boolean): void
```
# 调用方法交互最后更新时间: 2025年11月04日

方法交互的概念是从程序角度出发提出的。地图 SDK 提供了很多与地图交互的接口方法，例如：改变地图显示的区域（即改变地图中心点）、改变地图的缩放级别、设置地图的显示范围等。

## 改变地图旋转角度

方法交互的核心方法均依赖 AMap 类提供的这两个方法：animateCamera（带有动画效果），moveCamera（直接改变状态，没有动画效果）。

#### 带有动画效果：

```
aMap.animateCamera(CameraUpdateFactory.changeBearing(90)) //逆时针旋转90°
```

#### 不带有动画效果：

```
aMap.moveCamera(CameraUpdateFactory.changeBearing(90)) //逆时针旋转90°
```

## 改变地图的中心点

如果想改变地图中心点，可以通过 changeLatLng 方法，示例代码如下：

```
aMap.moveCamera(CameraUpdateFactory.changeLatLng(new LatLng(39.897743, 116.321349)))
```

## 改变地图的缩放级别

如果想改变地图的缩放级别，可以通过 zoomTo 方法，示例代码如下：

```
aMap.moveCamera(CameraUpdateFactory.zoomTo(12))
```

地图的缩放级别一共分为 18 级，从 3 到 20。数字越大，展示的图面信息越精细。

|   |   |
|---|---|
|名称|说明|
|zoomIn()|放大地图缩放级别，在当前地图显示的级别基础上加1|
|zoomOut()|缩小地图缩放级别，在当前地图显示的级别基础上减1|
|zoomTo(zoom)|设置地图缩放级别|
|newLatLngZoom(latLng, zoom)|设置地图中心点以及缩放级别|
|zoomBy(amount)|根据给定的增量调整地图级别，即在现有地图级别上加上该增量值|

## 设置地图显示范围

如果想将地图的显示范围设置在规定屏幕内，可以通过 newLatLngBounds 方法，示例代码如下：

```
aMap.moveCamera(CameraUpdateFactory.newLatLngBounds(new LatLngBounds(new LatLng(39.889863, 116.354148), new LatLng(39.946781, 116.437982)), 20))
```

除上述介绍的方法外，地图 SDK 支持：给地图设置一个新的状态、修改地图倾斜度等，具体可以查阅 [参考手册](https://a.amap.com/lbs-dev-yuntu/static/reference/harmonyosnext-sdk/map/docs/index.html)。
# 地图截屏功能最后更新时间: 2025年09月29日

地图 SDK 支持对当前屏幕显示区域进行截屏，可以对地图、覆盖物（包含信息窗口）、Logo进行截取屏幕，这其中不包括地图控件、Toast窗口。

详细示例如下：

```
this.aMap?.getMapScreenShot({
  onMapScreenShot: (mapScreenShot: PixelMap | undefined, status: number) => {

    this.image = mapScreenShot;
    let buffer: string = "";
    if (mapScreenShot) {
      buffer += "截屏成功 ";
    } else {
      buffer += "截屏失败 ";
    }
    if (status != 0) {
      buffer += "地图渲染完成，截屏无网格";
    } else {
      buffer += "地图未渲染完成，截屏有网格";
    }

    promptAction.showToast({ message: `${buffer}` });

  }
});
```
# 获取POI数据最后更新时间: 2025年09月15日

## 简介

高德提供了千万级别的 POI（Point of Interest，兴趣点）。在地图表达中，一个 POI 可代表一栋大厦、一家商铺、一处景点等等。通过POI搜索，完成找餐馆、找景点、找厕所等等的功能。地图 SDK 的搜索功能提供多种获取 POI 数据的接口，下文将逐一介绍。

## 关键字检索POI

根据关键字检索适用于在某个城市搜索某个名称相关的POI，例如：查找北京市的“肯德基”。

#### 1，创建回调监听

```
private poiSearchListener: OnPoiSearchListener = {
  onPoiSearched: (pageResult: PoiResult | undefined, errorCode: number) => {
    if (errorCode === AMapException.CODE_AMAP_SUCCESS) { 
    }
  },
  onPoiItemSearched: (poiItem: PoiItem | undefined, errorCode: number) => {}
};
```

#### 2，构建查询对象

```
this.poiQuery = new PoiQuery(this.keyword, "",  this.city);
this.poiSearch.setQuery(this.poiQuery);
```

#### 3，构造 PoiSearch 对象，并设置监听

```
this.poiSearch = new PoiSearch(this.context!, undefined);
this.poiSearch.setOnPoiSearchListener(this.poiSearchListener);
```

#### 4，调用 PoiSearch 的 searchPOIAsyn() 方法发送请求

```
this.poiSearch.searchPOIAsyn();
```

#### 5，通过回调接口 onPoiSearched 解析返回的结果，将查询到的 POI 以绘制点的方式显示在地图上。

#### 6，说明

1）可以在回调中解析result，获取POI信息。

2）result.getPois()可以获取到PoiItem列表，Poi详细信息可参考PoiItem类。

3）若当前城市查询不到所需POI信息，可以通过result.getSearchSuggestionCitys()获取当前Poi搜索的建议城市。

4）如果搜索关键字明显为误输入，则可通过result.getSearchSuggestionKeywords()方法得到搜索关键词建议。

5）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）

效果图：

![](https://a.amap.com/lbs/static/img/doc/doc_1757930156326_83b50.jpeg)

## 周边检索POI
# 获取地址描述数据最后更新时间: 2025年09月15日

## 地理编码（地址转坐标）

#### 地理编码基本介绍

地理编码，又称为地址匹配，是从已知的结构化地址描述到对应的经纬度坐标的转换过程。该功能适用于根据用户输入的地址确认用户具体位置的场景，常用于配送人员根据用户输入的具体地址找地点。

结构化地址的定义： 首先，地址肯定是一串字符，内含国家、省份、城市、城镇、乡村、街道、门牌号码、屋邨、大厦等建筑物名称。按照由大区域名称到小区域名称组合在一起的字符。一个有效的地址应该是独一无二的。注意：针对大陆、港、澳地区的地理编码转换时可以将国家信息选择性的忽略，但省、市、城镇等级别的地址构成是不能忽略的。

注意：该功能可以返回一部分POI数据内容，但核心能力是完成结构化地址到经纬度的转换。

- POI关键字搜索，是根据关键词找到现实中存在的地物点（POI）。
    
- 地理编码是依据当前输入，根据标准化的地址结构（省/市/区或县/乡/村或社区/商圈/街道/门牌号/POI）进行各个地址级别的匹配，以确认输入地址对应的地理坐标，只有返回的地理坐标匹配的级别为POI，才会对应一个具体的地物（POI）。
    

根据给定的地理名称和查询城市，返回地理编码的结果列表。显示效果如图：

![](https://a.amap.com/lbs/static/img/doc/doc_1757930296840_4a47a.png)

实现步骤如下：

1、继承 OnGeocodeSearchListener 监听。

2、构造 GeocodeSearch 对象，并设置监听。

```

this.geocoderSearch = new GeocodeSearch(this.context)
this.geocoderSearch.setOnGeocodeSearchListener(this.onGeocodeSearchListener)
```

3、通过 GeocodeQuery(java.lang.String locationName, java.lang.String city) 设置查询参数，调用 GeocodeSearch 的 getFromLocationNameAsyn(GeocodeQuery geocodeQuery) 方法发起请求。

```
// 第一个参数表示地址，第二个参数表示查询城市，中文或者中文全拼，citycode、adcode，
let query = new GeocodeQuery(name, city) 
// 设置同步地理编码请求
this.geocoderSearch.getFromLocationNameAsyn(query) 
```

4、通过回调接口 onGeocodeSearched 解析返回的结果。

说明：

1）可以在回调中解析result，获取坐标信息。

2）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）

```

public onGeocodeSearched: (geocodeResult: GeocodeResult | undefined, errorCode: number): void => {
//解析geocodeResult获取坐标信息
}

```

## 逆地理编码（坐标转地址）

逆地理编码，又称地址解析服务，是指从已知的经纬度坐标到对应的地址描述（如行政区划、街区、楼层、房间等）的转换。常用于根据定位的坐标来获取该地点的位置详细信息，与定位功能是黄金搭档。

![](https://a.amap.com/lbs/static/img/doc/doc_1757930307013_fb5c8.png)

示例代码如下：

1、继承 OnGeocodeSearchListener 监听。

2、构造 GeocodeSearch 对象，并设置监听。

```
this.geocoderSearch = new GeocodeSearch(this.context)      this.geocoderSearch.setOnGeocodeSearchListener(this.onGeocodeSearchListener)
```

3、通过 RegeocodeQuery(LatLonPoint point, float radius, java.lang.String latLonType) 设置查询参数，调用 GeocodeSearch 的 getFromLocationAsyn(RegeocodeQuery regeocodeQuery) 方法发起请求。

```
// 第一个参数表示一个Latlng，第二参数表示范围多少米，第三个参数表示是火系坐标系还是GPS原生坐标系
let query =new ReGeocodeQuery(latLonPoint, 200, GeocodeSearch.AMAP) 
 // 设置异步逆地理编码请求
this.geocoderSearch.getFromLocationAsyn(query)
```

4、通过回调接口 onRegeocodeSearched 解析返回的结果。

说明：

1）可以在回调中解析result，获取地址、adcode等等信息。

2）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）

```
public onReGeocodeSearched: (reGeocodeResult: ReGeocodeResult | undefined, errorCode: number): void => {
//解析reGeocodeResult获取地址描述信息
}
```

## 注意事项

请注意：使用上述功能需要下载地图SDK，导入搜索功能的har包。
# 获取行政区划数据最后更新时间: 2025年09月29日

根据县（区）级行政区划名称查询其下级区划的详细信息，如：中心点坐标、编码等等。

目前能查询到街道级别的信息，例如：中国>山东省>济南市>历下区>舜华路街道（国>省>市>区>街道）。

## 示例代码：

```
let search = new DistrictSearch(mContext);
let query = new DistrictSearchQuery();
query.setKeywords("朝阳区");//传入关键字
query.setShowBoundary(true);//是否返回边界值
search.setQuery(query);
search.setOnDistrictSearchListener(this);//绑定监听器
search.searchDistrictAnsy();//开始搜索
```

通过回调接口获取数据

```
public onDistrictSearched: (districtResult: DistrictResult | undefined): void => { 

//在回调函数中解析districtResult获取行政区划信息
//在districtResult.getAMapException().getErrorCode()=1000时调用districtResult.getDistrict()方法
//获取查询行政区的结果，详细信息可以参考DistrictItem类。

}
```

显示效果如图所示：

![](https://a.amap.com/lbs/static/img/doc/doc_1758606758258_4a47a.png)

## 注意事项

请注意：使用上述功能需要下载地图SDK，导入搜索功能的har包。
# 获取天气数据最后更新时间: 2025年09月15日

## 简介

通过天气查询，可获取城市的实时天气、今天和未来3天的预报天气，可结合定位和逆地理编码功能使用，查询定位点所在城市的天气情况。注意：仅支持中国部分地区数据（台湾省目前没有数据）返回。

天气查询是一个可用来改善app体验的功能，如：在跑步类app中加入天气的提醒；出行前了解天气情况以便安排行程。

天气查询的请求参数类为 WeatherSearch，city（城市）为必设参数，type（气象类型）为可选，包含有两种类型：WEATHER_TYPE_LIVE为实况天气；WEATHER_TYPE_FORECAST为预报天气，默认为 实况天气。

## 示例代码

实况天气的代码如下：

 第一步：设置查询条件及天气监听接口。

```
//检索参数为城市和天气类型，实况天气为WEATHER_TYPE_LIVE、天气预报为WEATHER_TYPE_FORECAST
et query = new WeatherSearchQuery(this.cityName, WeatherSearchQuery.WEATHER_TYPE_FORECAST)
this.weatherSearch = new WeatherSearch(this.context)
      this.weatherSearch.setOnWeatherSearchListener(this.weatherSearchListener)
this.weatherSearch.setQuery(query)
//异步搜索
this.weatherSearch.searchWeatherAsyn()
```

第二步：获取天气查询结果。

```

/**
  * 实时天气查询回调
  */
public onWeatherLiveSearched: (weatherLiveResult: LocalWeatherLiveResult | undefined, errorCode: number): void => {
      if (errorCode === AMapException.CODE_AMAP_SUCCESS) {
        if (weatherLiveResult && weatherLiveResult.getLiveResult()) {
          this.weatherLive = weatherLiveResult.getLiveResult()
        } else {
          ToastUtil.show(this.uiContext, '对不起，没有搜索到相关数据！')
        }
      } else {
        ToastUtil.showError(this.uiContext, errorCode)
      }
    }
```

截图效果如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1757930372283_4a47a.png)

## 注意事项

请注意：使用上述功能需要下载地图SDK，导入搜索功能的包。
# 获取公交数据最后更新时间: 2025年11月17日

## 公交站点查询

实现公交站点查询的步骤如下:

1、继承 OnBusStationSearchListener 监听。

2、通过 BusStationQuery(query: string, city: string)设置搜索条件。

```
// 第一个参数表示公交线路名，第二个参数表示公交线路查询，第三个参数表示所在城市名或者城市区号
this.busStationQuery = new BusStationQuery(search, this.getCityCode());
```

3、构造 BusStationSearch 对象，并设置监听，并调用 BusStationSearch 的 searchBusStationAsyn() 方法发起查询。

```
this.busStationSearch = new BusStationSearch(this.mContext, this.busStationQuery);
// 设置查询结果的监听
this.busStationSearch?.setOnBusStationSearchListener(this.busStationSearchListener); 
this.busStationSearch?.searchBusStationAsyn();
```

4、通过回调接口 onBusStationSearched 解析返回的结果。

说明：

1）可以在回调中解析result，获取公交站点信息。

2）result.getBusStations()可以获取到 BusStationItem 列表。

3）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）

```
  private busStationSearchListener: OnBusStationSearchListener = {
    onBusStationSearched: (result: BusStationResult, rCode: number) => {
      //ToDo
    }
  }
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763087949254_4b7ff.png)

## 公交路线查询

### 线路名称查询

1、设置查询条件

根据 BusLineQuery(query: string, ctgr: BusSearchType, city: string) 创建一个 BusLineQuery 对象，并设置查询条件，再根据 BusLineSearch(act: Context, query: BusLineQuery) 创建一个 BusLineSearch 对象。查询类型参数 ctgr 此处设置为 BusLineQuery.SearchType.BY_LINE_NAME。

2、发送请求和接收数据

使用 BusLineSearch.searchBusLineAsyn() 搜索公交线路。在 OnBusLineSearchListener 的接口回调方法 onBusLineSearched: (busLinePagedResult: BusLineResult, resultID: number) => void处理返回结果。当根据线路名称搜索无结果时，会自动匹配关键字为途经点名称进行搜索。显示效果如图：

![](https://a.amap.com/lbs/static/img/doc/doc_1763087976935_a7c12.png)

![](https://a.amap.com/lbs/static/img/doc/doc_1763088009425_fcf62.png)

结果返回线路信息有线路 ID、公交类型、线路名称、坐标串、城市编码、首发站、末站。

发送请求

```
this.busLineQuery = new BusLineQuery(search, BusSearchType.BY_LINE_NAME,
  this.getCityCode()); // 第一个参数表示公交线路名，第二个参数表示公交线路查询，第三个参数表示所在城市名或者城市区号
this.busLineQuery.setPageSize(10); // 设置每页返回多少条数据
this.busLineQuery.setPageNumber(this.currentPage); // 设置查询第几页，第一页从0开始算起
this.busLineSearch = new BusLineSearch(this.mContext, this.busLineQuery); // 设置条件
this.busLineSearch?.setOnBusLineSearchListener(this.busLineSearchListener); // 设置查询结果的监听
this.busLineSearch?.searchBusLineAsyn(); // 异步查询公交线路名称
```

回调方法

```
private busLineSearchListener: OnBusLineSearchListener = {
  onBusLineSearched: (result: BusLineResult, rCode: number) => {
    //ToDo
  }
}
```

### 线路 ID 查询

获取公交线路的详细信息，可使用线路 ID 查询。结果返回线路信息有线路 ID、公交类型、线路名称、线路坐标、城市编码、首发站、末站、首班车时间、末班车时间、所属公交公司、全程里程、起步价、全程票价、矩形区域（外包矩形的左下与右上顶点）、线路沿途坐标。

1、参照线路名称查询步骤1设置查询条件。此时，查询类型参数 ctgr 此处设置为 BusLineQuery.SearchType.BY_LINE_ID。

2、发送请求和接收数据。可参考线路名称查询步骤2。可以根据得到的公交线路数据，使用 BusLineOverlay 画出公交线路图层，包括起终点和所有公交站点。另外也可以自定义 Marker 和 InfoWindow 的图标和信息。
# 驾车出行路线规划最后更新时间: 2025年09月15日

## 驾车出行路线规划

驾车路径规划可以根据起终点和驾车路线的数据，使用 DrivingRouteOverlay 画出驾车路线图层，包括起终点和转弯点。另外也可以自定义起终点和驾车转弯点的图标。

注意：地图SDK V1.0.0版本开始，SDK不再提供 com.amap.api.maps.overlay 包下的 overlay，已在官方demo中开源。

#### 第 1 步，初始化 RouteSearch 对象

```
routeSearch = new RouteSearch(this.mContext)
```

#### 第 2 步，设置数据回调监听器

```
this.mRouteSearch.setRouteSearchListener(this.onRouteSearchListener)
```

#### 第 3 步，设置搜索参数

通过 DriveRouteQuery(fromAndTo: FromAndTo, mode: number, passedByPoints: ArrayList<LatLonPoint>, avoidpolygons: ArrayList<ArrayList<LatLonPoint>>, avoidRoad: string) 设置搜索条件，方法对应的参数说明如下：

- fromAndTo，路径的起点终点；
    
- mode，路径规划的策略，可选，默认为0-速度优先；
    
- passedByPoints，途经点，可选；
    
- avoidpolygons，避让区域，可选，支持32个避让区域，每个区域最多可有16个顶点。如果是四边形则有4个坐标点，如果是五边形则有5个坐标点。
    
- avoidRoad，避让道路，只支持一条避让道路，避让区域和避让道路同时设置，只有避让道路生效。
    

```
// fromAndTo包含路径规划的起点和终点，drivingMode表示驾车模式
// 第三个参数表示途经点（最多支持6个），第四个参数表示避让区域（最多支持32个），第五个参数表示避让道路
const query = new DriveRouteQuery(fromAndTo, RouteSearch.DrivingDefault, undefined,
      undefined, ""); // 第一个参数表示路径规划的起点和终点，第二个参数表示驾车模式，第三个参数表示途经点，第四个参数表示避让区域，第五个参数表示避让道路
```

#### 第 4 步，发送请求

使用类 RouteSearch 的 calculateDriveRouteAsyn(query: DriveRouteQuery) 方法进行骑行规划路径计算。

```
this.mRouteSearch.calculateDriveRouteAsyn(query);
```

#### 第 5 步，接收数据

在 OnRouteSearchListener 接口回调方法 onDriveRouteSearched(result: DriveRouteResult | undefined, rCode: number): DriveRouteResult 处理驾车规划路径结果。返回的信息中包括：路线的距离、高速费用（仅针对7座以下轿车）、路况情况等等。

说明：

1）可以在回调中解析 result，获取驾车的路径。

2）result.getPaths()可以获取到 DrivePath 列表，驾车路径的详细信息可参考 DrivePath 类。

3）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）

```
private onRouteSearchListener: OnRouteSearchListener = {
  onDriveRouteSearched: (result: DriveRouteResult | undefined, errorCode: number): void => {
  //todo: 处理result驾车路径信息
  },
  onRideRouteSearched: (result: RideRouteResult, errorCode: number): void => {
  },
  onWalkRouteSearched: (result: WalkRouteResult, errorCode: number) => {
  },
  onBusRouteSearched: (result: BusRouteResult, errorCode: number): void => {
  }
}
```

![](https://a.amap.com/lbs/static/img/doc/doc_1757930498029_4a47a.png)       ![](https://a.amap.com/lbs/static/img/doc/doc_1757930503438_fb5c8.png)

## 驾车出行路线规划V2

驾车路径规划可以根据起终点和驾车路线的数据，使用 DrivingRouteOverlay 画出驾车路线图层，包括起终点和转弯点。另外也可以自定义起终点和驾车转弯点的图标。

注意：地图SDK V1.0.0版本开始，SDK不再提供 com.amap.api.maps.overlay 包下的 overlay，已在官方demo中开源。

#### 第 1 步，初始化 RouteSearchV2 对象

```
routeSearch = new RouteSearchV2(this.mContext)
```

#### 第 2 步，设置数据回调监听器

```
this.mRouteSearch.setRouteSearchListener(this.onRouteSearchListener)
```

#### 第 3 步，设置搜索参数

通过 DriveRouteQueryV2(fromAndTo: FromAndTo, mode: number, passedByPoints: ArrayList<LatLonPoint>, avoidpolygons: ArrayList<ArrayList<LatLonPoint>>, avoidRoad: string) 设置搜索条件，方法对应的参数说明如下：

- fromAndTo，路径的起点终点；
    
- mode，路径规划的策略，可选，默认为0-速度优先；
    
- passedByPoints，途经点，可选；
    
- avoidpolygons，避让区域，可选，支持32个避让区域，每个区域最多可有16个顶点。如果是四边形则有4个坐标点，如果是五边形则有5个坐标点。
    
- avoidRoad，避让道路，只支持一条避让道路，避让区域和避让道路同时设置，只有避让道路生效。
    

```
// fromAndTo包含路径规划的起点和终点，drivingMode表示驾车模式
// 第三个参数表示途经点（最多支持6个），第四个参数表示避让区域（最多支持32个），第五个参数表示避让道路
const fromAndTo = new FromAndTo(this.mStartPoint, this.mEndPoint);
    const query = new DriveRouteQueryV2(fromAndTo, DrivingStrategy.DEFAULT.getValue(), undefined,
      undefined, ""); // 第一个参数表示路径规划的起点和终点，第二个参数表示驾车模式，第三个参数表示途经点，第四个参数表示避让区域，第五个参数表示避让道路
    query.setShowFields(0b0010101)
```

#### 第 4 步，发送请求

使用类 RouteSearch 的 calculateRideRouteAsyn(RideRouteQuery query) 方法进行骑行规划路径计算。

```
this.mRouteSearch.calculateDriveRouteAsyn(query);
```

#### 第 5 步，接收数据

在 RouteSearch.OnRouteSearchListener 接口回调方法 void onDriveRouteSearched(DriveRouteResult result, int rCode) 处理驾车规划路径结果。返回的信息中包括：路线的距离、高速费用（仅针对7座以下轿车）、路况情况等等。

说明：

1）可以在回调中解析 result，获取驾车的路径。

2）result.getPaths()可以获取到 DrivePath 列表，驾车路径的详细信息可参考 DrivePath 类。

3）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）

```
private onRouteSearchListener: OnRouteSearchListenerV2 = {
  onDriveRouteSearched: (result: DriveRouteResultV2 | undefined, errorCode: number): void => {
    //todo: 处理result驾车路径信息，详情参考demo
  },
  onRideRouteSearched: (result: RideRouteResultV2, errorCode: number): void => {
  },
  onWalkRouteSearched: (result: WalkRouteResultV2, errorCode: number) => {
  },
  onBusRouteSearched: (): void => {
  }
}
```
# 步行出行路线规划最后更新时间: 2025年09月15日

## 步行出行路线规划

步行路径规划可以根据起终点和步行路线的数据，使用 WalkRouteOverlay 画出步行路线图层，包括起终点和转弯点。另外也可以自定义起终点和步行转弯点的图标。

#### 第 1 步，初始化 RouteSearch 对象

```
this.mRouteSearch = new RouteSearch(this.mContext)
```

#### 第 2 步，设置数据回调监听器

```
this.mRouteSearch.setRouteSearchListener(this.onRouteSearchListener)
```

#### 第 3 步，设置搜索参数

通过 WalkRouteQuery(fromAndTo: FromAndTo) 设置搜索条件。其中：

- fromAndTo，路径的起终点；
    

```
//fromAndTo，路径的起终点；
const fromAndTo = new FromAndTo(this.mStartPoint, this.mEndPoint)
// 第一个参数表示路径规划的起点和终点
const query = new WalkRouteQuery(fromAndTo); 
//设置扩展字段,可选
query.setExtensions(RouteSearch.EXTENSIONS_ALL);
```

#### 第 4 步，发送请求

使用类 RouteSearch 的 calculateWalkRouteAsyn(WalkRouteQuery query) 方法进行步行规划路径计算。

```
this.mRouteSearch.calculateWalkRouteAsyn(query)
```

#### 第 5 步，接收数据

在 OnRouteSearchListener 接口回调方法中的 onWalkRouteSearched: (walkRouteResult: WalkRouteResult, errorCode: number) => void处理步行规划路径结果。返回的信息中您可以获得路段的距离、步行的预计时间、步行路段的坐标点、步行路段的道路名称、导航主要操作等信息。显示效果如下：

说明：

1）可以在回调中解析result，获取步行的路径。

2）result.getPaths()可以获取到 WalkPath 列表，步行路径的详细信息可参考 WalkPath 类。

3）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站错误码对照表）

```
private onRouteSearchListener: OnRouteSearchListener = {
  onWalkRouteSearched: (result: WalkRouteResult, errorCode: number) => {
    //todo: 处理result步行路径信息
  },
  onDriveRouteSearched: () => {
  },
  onRideRouteSearched: () => {
  },
  onBusRouteSearched: () => {
  }
}
```

![](https://a.amap.com/lbs/static/img/doc/doc_1757930566550_10fb1.png)

## 步行出行路线规划V2

步行路径规划可以根据起终点和步行路线的数据，使用 WalkRouteOverlayV2 画出步行路线图层，包括起终点和转弯点。另外也可以自定义起终点和步行转弯点的图标。

#### 第 1 步，初始化 RouteSearchV2 对象

```
this.mRouteSearch = new RouteSearchV2(this.mContext)
```

#### 第 2 步，设置数据回调监听器

```
this.mRouteSearch.setRouteSearchListener(this.onRouteSearchListener)
```

#### 第 3 步，设置搜索参数

通过 WalkRouteQueryV2(fromAndTo: FromAndTo) 设置搜索条件。其中：

- fromAndTo，路径的起终点；
    

```
//fromAndTo，路径的起终点；
const fromAndTo = new FromAndTo(this.mStartPoint, this.mEndPoint)
// 第一个参数表示路径规划的起点和终点
const query = new WalkRouteQueryV2(fromAndTo); 
//设置请求数据返回的字段
query.setShowFields(0b0010101)//对应'cost,navi,polyline'，可在网站api查询
//设置返回的步行路线数量
query.setAlternativeRoute(3)
```

#### 第 4 步，发送请求

使用类 RouteSearch 的 calculateWalkRouteAsyn(WalkRouteQuery query) 方法进行步行规划路径计算。

```
this.mRouteSearch.calculateWalkRouteAsyn(query)
```

#### 第 5 步，接收数据

在 OnRouteSearchListenerV2 接口回调方法中的 onWalkRouteSearched: (walkRouteResult: WalkRouteResultV2, errorCode: number) => void 处理步行规划路径结果。返回的信息中您可以获得路段的距离、步行的预计时间、步行路段的坐标点、步行路段的道路名称、导航主要操作等信息。显示效果如下：

说明：

1）可以在回调中解析result，获取步行的路径。

2）result.getPaths()可以获取到 WalkPath 列表，步行路径的详细信息可参考 WalkPath 类。

3）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站错误码对照表）

```
private onRouteSearchListener: OnRouteSearchListenerV2 = {
  onWalkRouteSearched: (result: WalkRouteResultV2, errorCode: number) => {
    //todo: 处理result步行路径信息
  },
  onDriveRouteSearched: () => {
  },
  onRideRouteSearched: () => {
  },
  onBusRouteSearched: () => {
  }
}
```

![](https://a.amap.com/lbs/static/img/doc/doc_1757930573813_09dd8.png)
# 公交出行路线规划最后更新时间: 2025年09月29日

公交路径规划可以根据起终点和公交换乘的数据，使用 BusRouteOverlay 画出公交路线图层，包括起终点和换乘点。另外也可以自定义起终点和换乘点的图标。

目前支持跨城公交路线规划，提供不同城市之间的火车换成方案。

## 公交出行路线规划

#### 第 1 步，初始化 RouteSearch 对象

```
this.mRouteSearch = new RouteSearch(this.mContext)
```

#### 第 2 步，设置数据回调监听器

```
this.mRouteSearch.setRouteSearchListener(this.onRouteSearchListener)
```

#### 第 3 步，设置搜索参数

通过 BusRouteQuery(fromAndTo: FromAndTo, mode: numer, city: string,  nightflag: number) 设置搜索条件。方法中的参数说明如下:

- fromAndTo，路径的起终点；
    
- mode，计算路径的模式，可选，默认为最快捷；
    
- city，城市名称/城市区号/电话区号，此项不能为空；当进行跨城查询时，该参数对应起点的城市；
    
- nightflag，是否计算夜班车，默认为不计算，0：不计算，1：计算，可选。
    

如果选择计算夜班车（nightflag=1），返回的夜班车数据将会排列在结果的前边。

如果存在地铁换乘出行，返回结果中还包括地铁的入站口和出站口信息。

如果是跨城公交出行，返回结果中包含火车信息。进行跨城公交查询时，还需调用 BusRouteQuery 的 setCityd(city: string) 方法设置终点城市。

```
// fromAndTo包含路径规划的起点和终点，RouteSearch.BusLeaseWalk表示公交查询模式
// 第三个参数表示公交查询城市区号，第四个参数表示是否计算夜班车，0表示不计算,1表示计算
let query = new BusRouteQuery(fromAndTo, RouteSearch.BusLeaseWalk, "010",0);
//query.setCityd("027");//终点城市区号
```

#### 第 4 步，发送请求

使用类 RouteSearch 的 calculateBusRouteAsyn( query: BusRouteQuery) 方法进行公交规划路径计算。

```
this.mRouteSearch.calculateBusRouteAsyn(query)
```

#### 第 5 步，接收数据

在 OnRouteSearchListener 接口回调方法 onBusRouteSearched( busRouteResult: BusRouteResult, rCode: number) 处理公交路径规划结果。

说明：

1）可以在回调中解析 result，获取驾车的路径。

2）result.getPaths()可以获取到 BusPath 列表，公交路径的详细信息可参考 BusPath 类。公交路径规划的一个路段（类 BusStep），必存在一段公交导航信息，最多包含一段步行信息。返回结果构成如下图所示：

![](https://a.amap.com/lbs/static/img/doc/doc_1758606981193_fb5c8.png)

3）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）

```
private onRouteSearchListener: OnRouteSearchListener = {
  onBusRouteSearched: (result: BusRouteResult, errorCode: number): void => {
    //todo处理返回的公交路线结果
  },
  onRideRouteSearched: () => {
  },
  onWalkRouteSearched: () => {
  },
  onDriveRouteSearched: () => {
  }
}
```

 ![](https://a.amap.com/lbs/static/img/doc/doc_1758606998123_10fb1.png)     ![](https://a.amap.com/lbs/static/img/doc/doc_1758607002240_09dd8.png)

![](https://a.amap.com/lbs/static/img/doc/doc_1758607006813_8266e.png)

## 公交出行路线规划V2

公交路径规划可以根据起终点和公交换乘的数据，使用 BusRouteOverlayV2 画出公交路线图层，包括起终点和换乘点。另外也可以自定义起终点和换乘点的图标。

目前支持跨城公交路线规划，提供不同城市之间的火车换成方案。

#### 第 1 步，初始化 RouteSearchV2 对象

```
this.mRouteSearch = new RouteSearchV2(this.mContext)
```

#### 第 2 步，设置数据回调监听器

```
this.mRouteSearch.setRouteSearchListener(this.onRouteSearchListener)
```

#### 第 3 步，设置搜索参数

通过 BusRouteQueryV2(fromAndTo: FromAndTo, mode: numer, city: string,  nightflag: number) 设置搜索条件。方法中的参数说明如下:

- fromAndTo，路径的起终点；
    
- mode，计算路径的模式，可选，默认为最快捷；
    
- city，城市区号，此项不能为空；当进行跨城查询时，该参数对应起点的城市；
    
- nightflag，是否计算夜班车，默认为不计算，0：不计算，1：计算，可选。
    

如果选择计算夜班车（nightflag=1），返回的夜班车数据将会排列在结果的前边。

如果存在地铁换乘出行，返回结果中还包括地铁的入站口和出站口信息。

如果是跨城公交出行，返回结果中包含火车信息。进行跨城公交查询时，还需调用 BusRouteQueryV2 的 setCityd(city: string) 方法设置终点城市。

```
// fromAndTo包含路径规划的起点和终点，RouteSearch.BusLeaseWalk表示公交查询模式
// 第三个参数表示公交查询城市区号，第四个参数表示是否计算夜班车，0表示不计算,1表示计算
let query = new BusRouteQueryV2(fromAndTo, RouteSearch.BusLeaseWalk, "010",0);
//query.setCityd("027");//终点城市区号
//query.setShowFields(0b0010101);//对应查询结果'cost,navi,polyline'字段展示，可在网站api查询
```

#### 第 4 步，发送请求

使用类 RouteSearchV2 的 calculateBusRouteAsyn( query: BusRouteQueryV2) 方法进行公交规划路径计算。

```
this.mRouteSearch.calculateBusRouteAsyn(query)
```

#### 第 5 步，接收数据

在 OnRouteSearchListenerV2接口回调方法 onBusRouteSearched( busRouteResult: BusRouteResultV2, rCode: number) 处理公交路径规划结果。

说明：

1）可以在回调中解析 result，获取驾车的路径。

2）result.getPaths()可以获取到 BusPathV2 列表，公交路径的详细信息可参考 BusPathV2 类。公交路径规划的一个路段（类 BusStepV2），必存在一段公交导航信息，最多包含一段步行信息。

3）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）

```
private onRouteSearchListener: OnRouteSearchListenerV2 = {
  onBusRouteSearched: (result: BusRouteResultV2, errorCode: number): void => {
    //todo处理返回的公交路线结果
  },
  onRideRouteSearched: () => {
  },
  onWalkRouteSearched: () => {
  },
  onDriveRouteSearched: () => {
  }
}
```

![](https://a.amap.com/lbs/static/img/doc/doc_1758607019334_f19c9.png)     ![](https://a.amap.com/lbs/static/img/doc/doc_1758607022899_9eb9c.png)

![](https://a.amap.com/lbs/static/img/doc/doc_1758607026447_602e8.png)
# 骑行出行路线规划最后更新时间: 2025年09月15日

## 骑行出行路线规划

从搜索功能1.0.0 版本开始支持骑行出行路线规划功能。

骑行路径规划可以根据起终点和骑行路线的数据，使用 RideRouteOverlay 画出骑行路线图层，包括起终点和转弯点。另外也可以自定义起终点和骑行转弯点的图标。

注意：地图SDK V1.0.0版本开始，SDK不再提供 com.amap.api.maps.overlay 包下的 overlay，已在官方demo中开源。

#### 第 1 步，初始化 RouteSearch 对象

```
this.mRouteSearch = new RouteSearch(this.mContext)
```

#### 第 2 步，设置数据回调监听器

```
this.mRouteSearch.setRouteSearchListener(this.onRouteSearchListener)
```

#### 第 3 步，设置搜索参数

通过 RideRouteQuery(fromAndTo:FromAndTo,mode?:number) 设置搜索条件。参数：fromAndTo，路径的起终点；mode，计算路径的模式。可选，默认为“推荐路线及最快路线综合模式”。

```
const fromAndTo = new FromAndTo(this.mStartPoint, this.mEndPoint);
const query = new RideRouteQuery(fromAndTo);
query.setExtensions(RouteSearch.EXTENSIONS_ALL);
```

#### 第 4 步，发送请求

使用类 RouteSearch 的 calculateRideRouteAsyn(query:RideRouteQuery) 方法进行骑行规划路径计算。

```
this.mRouteSearch.calculateRideRouteAsyn(query)
```

#### 第 5 步，接收数据

在 RouteSearch.OnRouteSearchListener 接口回调方法 onRideRouteSearched: (result: RideRouteResult, errorCode: number): void  处理骑行规划路径结果。返回的信息中您可以获得预估的骑行距离、骑行的预计时间、骑行路段的道路名称、坐标点等信息。

说明：

1）可以在回调中解析result，获取骑行的路径。

2）result.getPaths()可以获取到 RidePath 列表，骑行路径的详细信息可参考 RidePath 类。

3）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）

```
  private onRouteSearchListener: OnRouteSearchListener = {
    onRideRouteSearched: (result: RideRouteResult, errorCode: number): void => {
      //解析result获取算路结果，可参考官方demo
    }
  }
```

显示效果如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1757930651341_8266e.png)       ![](https://a.amap.com/lbs/static/img/doc/doc_1757930656718_f19c9.png)

## 骑行出行路线规划V2

从搜索功能1.0.0 版本开始支持骑行出行路线规划功能。

骑行路径规划可以根据起终点和骑行路线的数据，使用 RideRouteOverlay 画出骑行路线图层，包括起终点和转弯点。另外也可以自定义起终点和骑行转弯点的图标。

注意：地图SDK V1.0.0版本开始，SDK不再提供 com.amap.api.maps.overlay 包下的 overlay，已在官方demo中开源。

#### 第 1 步，初始化 RouteSearch 对象

```
this.mRouteSearch = new RouteSearchV2(this.mContext)
```

#### 第 2 步，设置数据回调监听器

```
this.mRouteSearch.setRouteSearchListener(this.onRouteSearchListener)
```

#### 第 3 步，设置搜索参数

通过 RideRouteQueryV2(fromAndTo:FromAndTo) 设置搜索条件。参数：fromAndTo，路径的起终点

```
const fromAndTo = new FromAndTo(this.mStartPoint, this.mEndPoint);
const query = new RideRouteQueryV2(fromAndTo); query.setShowFields(0b0011111)
```

#### 第 4 步，发送请求

使用类 RouteSearchV2 的 calculateRideRouteAsyn(query:RideRouteQuery) 方法进行骑行规划路径计算。

```
this.mRouteSearch.calculateRideRouteAsyn(query);
```

#### 第 5 步，接收数据

在 RouteSearchV2.OnRouteSearchListener 接口回调方法 onRideRouteSearched: (result: RideRouteResult, errorCode: number): void  处理骑行规划路径结果。返回的信息中您可以获得预估的骑行距离、骑行的预计时间、骑行路段的道路名称、坐标点等信息。

说明：

1）可以在回调中解析result，获取骑行的路径。

2）result.getPaths()可以获取到 RidePath 列表，骑行路径的详细信息可参考 RidePath 类。

3）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）

```
private onRouteSearchListener: OnRouteSearchListenerV2 = {
    onRideRouteSearched: (result: RideRouteResultV2, errorCode: number): void => {
      //解析result获取算路结果，可参考官方demo
    }
  }
```

显示效果如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1757930666140_9eb9c.png)       ![](https://a.amap.com/lbs/static/img/doc/doc_1757930670752_602e8.png)
# 货车出行路线规划最后更新时间: 2025年09月29日

从搜索功能1.0.1 版本开始支持货车出行路线规划功能，货车出行路线规划的具体策略可参见服务文档。

#### 第 1 步，初始化 RouteSearch 对象

```
this.mRouteSearch = new RouteSearch(this.mContext)
```

#### 第 2 步，设置数据回调监听器

```
this.mRouteSearch.setOnTruckRouteSearchListener(this.onTruckRouteSearchListener)
```

#### 第 3 步，设置搜索参数

通过 TruckRouteQuery(fromAndTo: FromAndTo, mode: number,passedByPoints:ArrayList<LatLonPoint>|null|undefined,truckSize: number) 设置搜索条件。

|   |   |
|---|---|
|参数|说明|
|fromAndTo|路径的起终点|
|mode|计算路径的模式（可选），默认为“躲避拥堵”|
|passedByPoints|途经点|
|truckSize|货车大小，默认轻型车|

```
const fromAndTo = new FromAndTo(this.mStartPoint, this.mEndPoint);
//设置车牌
fromAndTo.setPlateNumber("A000XXX");
fromAndTo.setPlateProvince("京");
const query = new TruckRouteQuery(fromAndTo,RouteSearch.TRUCK_AVOID_CONGESTION,null,RouteSearch.TRUCK_SIZE_HEAVY); 
//设置车辆信息
query.setTruckAxis(6)
query.setTruckHeight(3.9)
query.setTruckWidth(3)
query.setTruckLoad(45)
query.setTruckWeight(50)
```

#### 第 4 步，发送请求

使用类 RouteSearch 的calculateTruckRouteAsyn(truckQuery: TruckRouteQuery) 方法进行路线规划路径计算。

```
this.mRouteSearch.calculateTruckRouteAsyn(query)
```

#### 第 5 步，接收数据

在 RouteSearch.OnTruckRouteSearchListener 接口回调方法 onTruckRouteSearched:(result: TruckRouteRestult, errorCode: number)处理货车规划路径结果。返回的信息中您可以获得预估的货车路线距离、货车路线的预计时间、货车路线路段的道路名称、坐标点等信息。

说明：

1）可以在回调中解析result，获取货车的路径。

2）result.getPaths()可以获取到 TruckPath 列表，货车路线的具体方案的详细信息可参考 TruckPath 类。

3）返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）

```
private  onTruckRouteSearchListener:OnTruckRouteSearchListener = {

onTruckRouteSearched:(result: TruckRouteRestult, errorCode: number): void => {
      //解析result获取算路结果，可参考官方demo
      //建议通过TruckPath中getRestriction() 判断路线上是否存在限行

  }
```

![](https://a.amap.com/lbs/static/img/doc/doc_1758607160901_7afbb.png)
# 未来行程路线规划最后更新时间: 2025年09月15日

## 简介

自地图 SDK 搜索功能 1.0.0 版本起新增未来行程路线规划，简称ETD。 未来出行规划（ETD）服务已覆盖全国所有城市，可提供未来7天的出行路线规划。 

注意：下面介绍的功能使用的是地图SDK的搜索功能，需要在工程中导入

## 未来行程路线规划

#### 第一步，  初始化 RouteSearch 对象

```
this.mRouteSearch = new RouteSearch(this.mContext);
```

#### 第二步， 设置数据回调监听器

```
this.mRouteSearch?.setOnRoutePlanSearchListener(this.onRoutePlanSearchListener);
```

#### 第三步， 设置搜索参数

通过 DrivePlanQuery(RouteSearch.FromAndTo fromAndTo, int firstTime, int interval, int count) 设置搜索条件，方法对应的参数说明如下：

fromAndTo，路径的起点终点，必设。

firstTime，出发时间，第一个时间戳（unix时间戳，精确到秒)，必设；

interval，规划的时间间隔，单位为秒，必设；

count，规划时间点个数，最大48个，必设。

设置终点的父POIID，无父POI的情况留空即可：

DrivePlanQuery.setDestParentPoiID(destParentPoiID)

设置规划策略模式，可选，默认为速度优先；

DrivePlanQuery.setMode(int mode)

设置车辆类型，默认为普通汽车：

DrivePlanQuery.setCarType(int carType)

```
const fromAndTo = new FromAndTo(
    this.mStartPoint, this.mEndPoint);
    const time = Math.floor(Date.now() / 1000)
    const query = new DrivePlanQuery(fromAndTo, time + utils.queryFirstInterval * 60, utils.queryInterval * 60,
      48); // 第一个参数表示路径规划的起点和终点，第二个参数表示驾车模式，第三个参数表示途经点，第四个参数表示避让区域，第五个参数表示避让道路
```

#### 第四步，发送请求

 使用类 RouteSearch 的 calculateDrivePlanAsyn(DrivePlanQuery driveQuery) 方法进行骑行规划路径计算。

```
this.mRouteSearch?.calculateDrivePlanAsyn(query)
```

#### 第五步，接收数据

 在 RouteSearch.OnRoutePlanSearchListener接口回调方法 void OnRoutePlanSearchListener(DriveRouteResult result, int rCode) 处理驾车规划路径结果。返回的信息中包括：路线的距离、规划时间、路况情况等。

 说明：

- 可以在回调中解析 result，获取驾车的路径；

- result.getPaths()可以获取到 DrivePath 列表，驾车路径的详细信息可参考 DrivePlanPath 类；

- 返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）。

```
private onRoutePlanSearchListener: OnRoutePlanSearchListener = {
  onDriveRoutePlanSearched: (result: DriveRoutePlanResult | undefined, errorCode: number): void => {
    //解析result获取算路结果，可参考官方demo
  }
}
```
# 坐标转换最后更新时间: 2025年11月17日

## 经纬度坐标与屏幕像素坐标互转

屏幕像素坐标转经纬度坐标

```
map.getProjection()?.fromScreenLocation(new Point(10, 10), (coord) => {
console.log('地理坐标', coord)
});
```

经纬度坐标转屏幕像素坐标

```
map.getProjection()?.toScreenLocation(new LatLng(39.957957,116.369404),(coord)=>{
console.log('屏幕坐标', coord)
});
```

## 其他坐标系转到高德坐标系

支持GPS/Mapbar/Baidu等多种类型坐标在高德地图上使用。参见类CoordinateConverter。

```
  const converter = new CoordinateConverter(getContext(this).getApplicationContext())
  // CoordType.GPS 待转换坐标类型
   converter.from(CoordType.GPS)
  // sourceLatLng待转换坐标点
  converter.coord(sourceLatLng)
  // 执行转换操作
  const  desLatLng = converter.convert()
```
# 距离测量最后更新时间: 2025年09月29日

此功能可以在不请求驾车出行路线规划接口的同时完成距离计算。目前支持直线距离和驾车距离的测量。

#### 第1步，初始化DistanceSearch

```
const context: Context | undefined = this.getUIContext().getHostContext()
const distanceSearch = new DistanceSearch(context!);
```

#### 第2步，设置数据回调监听

```
distanceSearch.setDistanceSearchListener({
      onDistanceSearched: (distanceResult: DistanceResult, errorCode: number) => {
        if (errorCode === AMapException.CODE_AMAP_SUCCESS) {

        }
      }
    });
```

#### 第3步，设置搜索参数

```
const start0: LatLonPoint = new LatLonPoint(39.902896,116.42792);
const start1: LatLonPoint = new LatLonPoint(39.865208,116.378596);
const start2: LatLonPoint = new LatLonPoint(39.894914,116.322062);
const start3: LatLonPoint = new LatLonPoint(39.945261,116.352994);
const dest: LatLonPoint = new LatLonPoint(39.902896, 116.42792);

//设置起点和终点，其中起点支持多个
const latLonPoints: ArrayList<LatLonPoint> = new ArrayList<LatLonPoint>();
latLonPoints.add(start0);
latLonPoints.add(start1);
latLonPoints.add(start2);
latLonPoints.add(start3);

const distanceQuery = new DistanceQuery();
distanceQuery.setOrigins(latLonPoints);
distanceQuery.setDestination(dest);
distanceQuery.setType(DistanceSearch.TYPE_DRIVING_DISTANCE);
```

#### 第4步，发送请求

```
 distanceSearch.calculateRouteDistanceAsyn(distanceQuery);
```

#### 第5步，接收数据

在 DistanceSearch对象的setDistanceSearchListener方法中，设置OnDistanceSearchListener回调监听，处理距离测量结果。返回的信息中您可以获得预估的直线或驾车路线距离。

说明：

1. 可以在回调中解析distanceResult，距离测量结果
    
2. distanceResult.getDistanceResults()可以获取到DistanceItem列表，距离测量结果详细信息可参考 DistanceItem 类。
    
3. 返回结果成功或者失败的响应码。1000为成功，其他为失败（详细信息参见网站开发指南-实用工具-错误码对照表）
    

效果事例图：

![](https://a.amap.com/lbs/static/img/doc/doc_1758607241736_549cf.jpeg)
# 距离/面积计算最后更新时间: 2025年11月17日

地图SDK提供了很多计算方法，包括：计算亮点距离、矩形面积、坐标转换、判断点是否在圆或者多边形内等等，下面做简单介绍：

## 两点间的直线距离计算

根据用户指定的两个经纬度坐标点，计算这两个点的直线距离，单位为米。代码如下：

```
/**
 * 根据用户的起点和终点经纬度计算两点间距离，单位米。
 *
 * @param startLatlng 起点的坐标。
 * @param endLatlng   终点的坐标。
 * @return 返回两点间的距离，单位米。
 * @since 1.0.0
 */
public static calculateLineDistance(startLatlng: LatLng, endLatlng: LatLng):  number
```

## 面积计算

高德地图SDK支持计算矩形的面积。代码如下：

```
/**
 * 计算地图上矩形区域的面积，单位平方米。
 *
 * @param leftTopLatlng     矩形区域左上角坐标。
 * @param rightBottomLatlng 矩形区域右下角坐标。
 * @return 返回地图上矩形区域的面积，单位平方米。
 * @since 1.0.0
 */
public static calculateRectangleArea(leftTopLatlng: LatLng, rightBottomLatlng: LatLng):  numbe
```
# 常见问题最后更新时间: 2024年10月29日

### 如何获取AppID

请在当前应用的Ability中使用如下代码获取

```
let flag = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_SIGNATURE_INFO;
let bundleInfo = bundleManager.getBundleInfoForSelfSync(flag)
let appId = bundleInfo.signatureInfo.appId;
```

### 如何确定鸿蒙开发环境是否兼容？

高德地图开放平台当前适配的鸿蒙版本为DevEco Studio: NEXT Beta1-5.0.3.800, SDK: API12 Release(5.0.0.65)，后续鸿蒙系统稳定版本也会持续适配