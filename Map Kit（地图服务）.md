# Map Kit简介

更新时间: 2025-12-16 16:35

Map Kit（地图服务）为开发者提供强大而便捷的地图能力，助力全球开发者实现个性化显示地图、位置搜索和路径规划等功能，轻松完成地图构建工作。您可以轻松地在HarmonyOS应用/元服务中集成地图相关的功能，全方位提升用户体验。

Map Kit提供了全球3.2亿的 POI（Point of Interest，兴趣点）。在地图表达中，一个 POI可代表一家商铺、一栋办公楼、一处景点等等。

Map Kit不断优化丰富地图的细节呈现能力，例如在POI和路网信息展示方面，根据POI属性信息及区域路网差异，在不同层级比例尺条件下，为用户展示更合适的POI和路网信息。手势交互方面，提供了包括缩放、旋转、移动、倾斜等流畅的交互体验。

## 场景介绍

中国大陆使用GCJ02坐标系，中国台湾和海外使用WGS84坐标系。详见[坐标纠偏](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-convert-coordinate)。

Map Kit提供以下功能，满足绝大多数地图开发的需求：

- [创建地图](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-creation)：创建地图组件、设置地图属性、自定义地图等。
- [地图交互](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-interaction)：控制地图的交互手势和交互按钮。
- [在地图上绘制](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-drawing)：添加位置标记、覆盖物以及各种形状等。
- [位置搜索](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-location-services)：多种查询POI信息的能力，提供正地理编码、逆地理编码的能力。
- [路径规划](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-navi)：提供驾车、步行、骑行路径规划能力。
- [静态图](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-static-diagram)：获取一张地图图片。
- [地图Picker](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-advanced-controls)：提供地点详情展示控件、地点选取控件、区划选择控件。
- [通过地图应用实现导航等能力](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-petalmaps)：查看位置详情、查看路径规划、发起导航、发起内容搜索。
- [地图计算工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-calculation-tool)：华为地图涉及的2种坐标系及其使用区域和转换。

## 约束和限制

### 支持的国家/地区

请参见[支持的国家/地区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-supported)。

### 支持的设备

本kit仅适用于Phone、Tablet、PC/2in1和Wearable。

### 示例代码

Map Kit（地图服务）示例代码，请参考[示例代码](https://gitcode.com/HarmonyOS_Samples/map-kit_-sample-code_-demo-arkts)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-kit-guide "Map Kit（地图服务）")
# 开发准备

更新时间: 2025-12-16 16:36

请优先[开通地图服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-config-agc#section16133115441516)后，再参考“[应用开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview)”完成基本准备工作，然后再继续进行以下开发活动。

说明

- 从HarmonyOS 5.0.2(14)版本开始，开发者无需配置公钥指纹和Client ID。
- 从DevEco Studio 6.0.0 Beta5版本开始，支持在DevEco Studio中开通地图服务。

## 开通地图服务

Map Kit提供2种方式开通地图服务：

- 通过DevEco Studio开通地图服务。
- 通过AppGallery Connect网站开通地图服务。

方式一：通过DevEco Studio开通地图服务

1. 登录DevEco Studio应用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163608.95546345188853129729687812238046:50001231000000:2800:150CB4AB33800605B13F01142064ECADFAE55E2BB4FA1FB577E114E72CAF34C3.png)
    
2. 选择文件，点击项目结构。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163608.33640228103015397117066187076805:50001231000000:2800:A44A86BBF19910BF6E9954184F32F4FBA11D36F901D0C3B0E4F26AAFAABD0F29.png)
    
3. 进入“Signing Configs”页面，点击“Enable open capabilities”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163608.47277408788487839450596278914425:50001231000000:2800:3A4D0445BB7351B557D90BD2B2002B53C877A890C76E28DF6722AB9B685D0796.png "点击放大")
    
4. 勾选“Map Kit”选项，点击“OK”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163608.26879095707131248872808271959356:50001231000000:2800:B6306DDDEF76A8ED1BA61D75ACB1DF71F99B3F1E0FDCF7797BBB3F8C728016B4.png "点击放大")
    
5. 选择“Apply”应用地图服务配置，点击“OK”完成地图服务配置。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163608.17389334701291495774832097756515:50001231000000:2800:546B8084AD87D3944173AA46287D131B7CC1B94E95E53A644B51217A5CFDC19E.png "点击放大")
    

方式二：通过AppGallery Connect网站开通地图服务。

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163608.12934664532338516439535505825772:50001231000000:2800:525579701164FFC8477FA6AF4B8D00B9348D0796DB53F832E6D6E306C2F97AEC.png "点击放大")
    
2. 在项目列表中找到您的项目，在项目下的应用列表中选择需要打开“地图服务”的应用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163608.47576884967478501932478698395914:50001231000000:2800:8EE2A531A48FF0DF9AE5B2D8743E6B8912A2689567780B0B90327EE6B3FE505D.png "点击放大")
    
3. 选择开放能力管理，找到“地图服务”开关，打开开关。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163608.89463329314473988862193996906617:50001231000000:2800:3FE63FC1B8BFFF3F23AF2F003078B60DE9C5425C2AE20AF9B3129556DDB26FC7.png "点击放大")
    
4. 确认已经开启“地图服务”开放能力，并完成签名。
    - 调试阶段必须[申请调试证书](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-debugcert-0000001914263178)、[注册设备](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-device-0000002283189937)、开启"地图服务"后重新[申请调试Profile文件](https://developer.huawei.com/consumer/cn/doc/app/agc-help-debug-profile-0000002248181278)，并完成[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233)。
    - 发布阶段必须[申请发布证书](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-cert-0000002283336729)、开启“地图服务”后重新[申请发布Profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-profile-0000002248341090)文件，并[配置签名信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-publish-app#section280162182818)。
        
        说明
        
        若使用原有的Profile文件，请确保在申请Profile文件之前已开启“地图服务”。
        

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-introduction "Map Kit简介")
# 显示地图

更新时间: 2025-12-16 16:36

## 场景介绍

从5.0.3(15)开始，支持Logo缩放功能和3D地球功能；从5.1.1(19)开始，支持室内图功能和设置比例尺单位功能；从6.0.0(20)开始，支持设置地图语言功能。

本章节将向您介绍如何使用地图组件[MapComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-mapcomponent#section816451553012)和[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)呈现地图，效果如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163633.05158809618316185994105429999657:50001231000000:2800:936D69749F81407392B8BF4BD188EA65288F88DBC9128F15DAF1F2E36D809965.png "点击放大")

## 接口说明

显示地图功能主要由[MapComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-mapcomponent#section816451553012)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-mapcomponent)。

|接口|接口描述|
|:--|:--|
|[mapCommon.MapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section816451553012)|提供Map组件初始化的属性。|
|[MapComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-mapcomponent#section816451553012)(mapOptions: [mapCommon.MapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section816451553012), mapCallback: AsyncCallback<[map.MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)>)|地图组件。|
|[map.MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)|地图组件的主要功能入口类，用来操作地图，与地图有关的所有方法从此处接入。它所承载的工作包括：地图类型切换（如标准地图、空地图）、改变地图状态（中心点坐标和缩放级别）、添加点标记（Marker）、绘制几何图形(如MapPolyline、MapPolygon、MapCircle)、监听各类事件等。|

## 开发步骤

### 地图显示

1. 导入Map Kit相关模块。
    
    1. import { MapComponent, mapCommon, map } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 新建地图初始化参数mapOptions，设置地图中心点坐标及层级。
    
    通过callback回调的方式获取[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)对象，用来操作地图。
    
    调用[MapComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-mapcomponent#section816451553012)组件，传入mapOptions和mapCallback参数，初始化地图。
    
    1. @Entry
    2. @Component
    3. struct HuaweiMapDemo {
    4.   private TAG = "HuaweiMapDemo";
    5.   private mapOptions?: mapCommon.MapOptions;
    6.   private callback?: AsyncCallback<map.MapComponentController>;
    7.   private mapController?: map.MapComponentController;
    8.   private mapEventManager?: map.MapEventManager;
    
    9.   aboutToAppear(): void {
    10.     // 地图初始化参数，设置地图中心点坐标及层级
    11.     this.mapOptions = {
    12.       position: {
    13.         target: {
    14.           latitude: 39.9,
    15.           longitude: 116.4
    16.         },
    17.         zoom: 10
    18.       }
    19.     };
    
    20.     // 地图初始化的回调
    21.     this.callback = async (err, mapController) => {
    22.       if (!err) {
    23.         // 获取地图的控制器类，用来操作地图
    24.         this.mapController = mapController;
    25.         this.mapEventManager = this.mapController.getEventManager();
    26.         let callback = () => {
    27.           console.info(this.TAG, `on-mapLoad`);
    28.         }
    29.         this.mapEventManager.on("mapLoad", callback);
    30.       } else {
    31.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    32.       }
    33.     };
    34.   }
    
    35.   // 页面每次显示时触发一次，包括路由过程、应用进入前台等场景，仅@Entry装饰的自定义组件生效
    36.   onPageShow(): void {
    37.     // 将地图切换到前台
    38.     if (this.mapController) {
    39.       this.mapController.show();
    40.     }
    41.   }
    
    42.   // 页面每次隐藏时触发一次，包括路由过程、应用进入后台等场景，仅@Entry装饰的自定义组件生效
    43.   onPageHide(): void {
    44.     // 将地图切换到后台
    45.     if (this.mapController) {
    46.       this.mapController.hide();
    47.     }
    48.   }
    
    49.   build() {
    50.     Stack() {
    51.       // 调用MapComponent组件初始化地图
    52.       MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback }).width('100%').height('100%');
    53.     }.height('100%')
    54.   }
    55. }
    
3. 运行您刚完成的工程就可以在您的APP中看到地图了，运行后的效果如下图所示。
    
    如果没有成功加载地图，请参见[地图不显示](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-faq-1)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163634.61306149861334821202333871839481:50001231000000:2800:4F3B440E629A49974C6EFF0DF692B99B8E2D2F96633110DAB2D762C7342163E8.png "点击放大")
    

### 设置地图属性

[MapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section816451553012)包含以下属性。

|属性|描述|
|:--|:--|
|mapType|地图类型，默认值：[MapType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section18522846142615).STANDARD。|
|position|地图相机位置。|
|bounds|地图展示框。|
|minZoom|地图最小图层，有效范围[2, 20]，默认值：2。|
|maxZoom|地图最大图层，有效范围[2, 20]，默认值：20。|
|rotateGesturesEnabled|是否支持旋转手势，默认值：true。|
|scrollGesturesEnabled|是否支持滑动手势，默认值：true。|
|zoomGesturesEnabled|是否支持缩放手势，默认值：true。|
|tiltGesturesEnabled|是否支持倾斜手势，默认值：true。|
|zoomControlsEnabled|是否展示缩放控件，默认值：true。|
|myLocationControlsEnabled|是否展示我的位置按钮，默认值：false。|
|compassControlsEnabled|是否展示指南针控件，默认值：true。|
|scaleControlsEnabled|是否展示比例尺，默认值：false。|
|alwaysShowScaleEnabled|是否始终显示比例尺，默认值：false。|
|padding|设置地图和边界的距离。|
|styleId|自定义样式ID。|
|dayNightMode|日间夜间模式，默认值：[DayNightMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section634916281725).DAY（日间模式）。|
|logoScale|Logo缩放比例，取值范围是[0.8, 1]，默认值：1。|
|sphereEnabled|是否开启3D地球效果，默认值为false。|
|indoorMapEnabled|是否开启室内图，默认值：false。|
|scaleUnit|地图比例尺公英制单位，默认值：[ScaleUnit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section2230143218276).METRIC_UNIT（公制单位）。|

1. 设置mapType，[切换地图类型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-type)章节中有详细讲解。
2. 设置myLocationControlsEnabled，展示我的位置按钮。
    
    在mapOptions中设置myLocationControlsEnabled属性为true，可展示我的位置按钮![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163634.97156233607865439301390514755927:50001231000000:2800:2E0CA42CE48E98B472A3324B650D1CE418CE4B3DCCF3D702D03130CA6C144137.png)，显示效果如下图所示。
    
    也可通过调用[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)对象的方法展示我的位置按钮，详情见[显示我的位置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-location)章节。
    
    1. this.mapOptions = {
    2.   position: {
    3.     target: {
    4.       latitude: 39.9,
    5.       longitude: 116.4
    6.     },
    7.     zoom: 10
    8.   },
    9.   myLocationControlsEnabled: true
    10. };
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163634.45277695723697915809414076945991:50001231000000:2800:B2F0A56B9556486839ED54FAF8DB0283BC1A60B98E849EA257BF48CD6A9A9237.png)
    
3. 展示比例尺。
    
    在mapOptions中设置scaleControlsEnabled属性为true，可展示比例尺，显示效果如下图所示。
    
    1. this.mapOptions = {
    2.   position: {
    3.     target: {
    4.       latitude: 39.9,
    5.       longitude: 116.4
    6.     },
    7.     zoom: 10
    8.   },
    9.   scaleControlsEnabled: true
    10. };
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163634.22839243349614003854432228629527:50001231000000:2800:2048C3695E118FE49A9D369B8FD48C90BA5BD4247F809D37DD9CD9D78B5FC198.png)
    

### 开启3D建筑图层

调用[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)对象的[setBuildingEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section15905291318)方法开启3D建筑图层，将两个手指放在地图上，向上滑动倾斜地图可看到3D建筑图层的效果。

1. this.mapController.setBuildingEnabled(true);

显示效果如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163634.93546466824279237052459349430836:50001231000000:2800:DAD10F05F011FF116A9E2DD3DCD6D75D30AE300C841F20499A7A5AD2FEC43FB1.png "点击放大")

### 地图前后台切换

您可以通过[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)对象来控制地图页面前后台切换的生命周期。应用触发前后台切换时，可以在Page生命周期里调用show/hide，以便申请/释放资源。

**地图切换至前台：**

1. // 页面每次显示时触发一次，包括路由过程、应用进入前台等场景，仅@Entry装饰的自定义组件生效
2. onPageShow(): void {
3.   // 建议页面切换到前台，调用地图组件的show方法 
4.   if (this.mapController) {
5.     this.mapController.show();
6.   }
7. }

**地图切换至后台：**

1. // 页面每次隐藏时触发一次，包括路由过程、应用进入后台等场景，仅@Entry装饰的自定义组件生效
2. onPageHide(): void {
3.   // 建议页面切换到后台，调用地图组件的hide方法
4.   if (this.mapController) {
5.     this.mapController.hide();
6.   }
7. }

### 深色模式

Map Kit提供2种方式设置地图的夜间模式：初始化地图时和创建地图后。

方式一：初始化地图时

在地图初始化参数中设置dayNightMode参数，参数可选值包括DAY（日间模式）、NIGHT（夜间模式）、AUTO（自动模式）。如果将参数值设置为AUTO，地图的深色模式会跟随系统，打开系统深色开关，显示夜间模式，否则显示日间模式。

1. this.mapOptions = {
2.   position: {
3.     target: {
4.       latitude: 39.9,
5.       longitude: 116.4
6.     },
7.     zoom: 10
8.   },
9.   myLocationControlsEnabled: true,
10.   // 设置地图为夜间模式
11.   dayNightMode: mapCommon.DayNightMode.NIGHT
12. };

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163634.22033865253917335945237417773682:50001231000000:2800:C189209CC37A5AA7396DD66D64B01BC500397F5DBAB0A6BD57BDD68FB79FB696.png)

方式二：创建地图后

创建地图后，可调用[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)对象的[setDayNightMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section123945545109)方法设置夜间模式。下面的例子中将参数值设置为AUTO，在设置完之后，打开系统的深色开关，地图会自动变为夜间模式。

1. // 设置地图为自动模式
2. this.mapController.setDayNightMode(mapCommon.DayNightMode.AUTO);

### 室内图

使用室内图可查看楼层平面图，如查看购物中心、博物馆和医院等地点的内部情况。开启3D地图后无法显示室内图。

Map Kit提供2种方式开启地图的室内图功能：初始化地图时和创建地图后。

方式一：初始化地图时

在地图初始化参数中设置将[MapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section816451553012)中的indoorMapEnabled参数设置为true即可开启室内图功能，而且仅17级及以上地图层级可见室内图，仅18级及以上地图层级可见楼层调节控件，通过左下角的楼层调节控件可以切换当前室内图楼层。

1. this.mapOptions = {
2.   position: {
3.     target: {
4.       latitude: 31.979227,
5.       longitude: 118.762245
6.     },
7.     zoom: 18
8.   },
9.   // 开启室内图功能
10.   indoorMapEnabled: true
11. };

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163634.95233783468993534387496882380747:50001231000000:2800:401AB1D19B0F3DF76F89F06A85E3540C77BC05DC6823FCAFDE2E2E0A5358F376.png "点击放大")

方式二：创建地图后

创建地图后，可调用[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)对象的[setIndoorMapEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section12159164214612)方法来开启或关闭室内图功能。下面的例子中将室内图开启后，调用[isIndoorMapEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section820584761611)方法来查询当前室内图功能的开启状态，调用[setFloorControlsPosition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section53651918173410)方法可以设置楼层调节控件的位置。室内图功能还提供了[switchIndoorMapFloor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section15944125342513)方法，可以切换到指定的室内建筑和指定的楼层。

1. // 开启室内图功能
2. this.mapController.setIndoorMapEnabled(true);
3. // 查询当前室内图开启状态
4. let isIndoorMapEnabled: boolean = this.mapController.isIndoorMapEnabled();
5. console.info('indoorMapEnabled is:' + isIndoorMapEnabled);
6. // 设置楼层调节控件的位置
7. this.mapController.setFloorControlsPosition({
8.   positionX: 500,
9.   positionY: 500
10. });
11. // 切换楼层,需要将第一个入参替换成用户需要的建筑物id，第二个参数替换成当前楼层，如'1F'、'B1'等等
12. this.mapController.switchIndoorMapFloor('822588304363886720', '3F');

通过调用[on('indoorMapEnter')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section76731728143918)方法和[on('indoorMapExit')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section15867173119615)可以分别设置进入和退出室内图的监听事件。

1. let callbackEnter = (indoorMapInfo: map.IndoorMapInfo) => {
2.   console.info(this.TAG, `on-indoorMapEnter`);
3. };
4. let callbackExit = () => {
5.   console.info(this.TAG, `on-indoorMapExit`);
6. };
7. // 进入室内图监听回调
8. this.mapEventManager.on("indoorMapEnter", callbackEnter);
9. // 退出室内图监听回调
10. this.mapEventManager.on("indoorMapExit", callbackExit);

### Logo缩放比例

Map Kit提供2种方式设置地图的Logo缩放比例：初始化地图时和创建地图后。

方式一：初始化地图时

在地图初始化参数中设置logoScale参数，取值范围是[0.8, 1]，默认值是1。

1. this.mapOptions = {
2.   position: {
3.     target: {
4.       latitude: 39.9,
5.       longitude: 116.4
6.     },
7.     zoom: 10
8.   },
9.   myLocationControlsEnabled: true,
10.   // 设置logo缩放比例为0.9
11.   logoScale: 0.9
12. };

方式二：创建地图后

1. 创建地图后，调用[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section816451553012)对象的[setLogoScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section205343210177)方法设置Logo缩放比例。
    
    1. this.mapController.setLogoScale(0.9);
    
2. 获取Logo缩放比例。
    
    通过调用[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section816451553012)对象的[getLogoScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section18243711173212)方法获取当前Logo缩放比例。
    
    1. let logoScale: number = this.mapController.getLogoScale();
    

### 开启3D地球

Map Kit提供2种方式开启3D地球：初始化地图时和创建地图后。

开启3D地球后，将地图缩放可看到3D地球的效果。

方式一：初始化地图时

在地图初始化参数中设置3D地球的开启状态，默认值是false。

1. this.mapOptions = {
2.   position: {
3.     target: {
4.       latitude: 39.9,
5.       longitude: 116.4
6.     },
7.     zoom: 2
8.   },
9.   // 开启3D地球
10.   sphereEnabled: true
11. };

方式二：创建地图后

创建地图后，调用[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section816451553012)对象的[setSphereEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section67801022102716)方法开启3D地球，通过调用[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section816451553012)对象的[isSphereEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1825143352110)方法可获取3D地球的开启状态。

1. // 开启3D地球
2. this.mapController.setSphereEnabled(true);
3. // 获取3D地球的开启状态
4. let result: boolean = this.mapController.isSphereEnabled();

显示效果如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163634.11140333585488107724105878713126:50001231000000:2800:8C6817103F08FD85FCC8A6B18A9176D240746257CD8A003E967CEC5C21DE1CDF.png "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-creation "创建地图")
# 切换地图类型

更新时间: 2025-12-16 16:36

## 场景介绍

从6.0.0(20)开始，支持卫星图和混合地图功能。

Map Kit支持以下地图类型：

- STANDARD：标准地图，展示道路、建筑物以及河流等重要的自然特征。
- NONE：空地图，没有加载任何数据的地图。
- TERRAIN：地形图，在保留了行政区划边界、POI、楼块等地图要素的基础上，呈现完整清晰描绘地形走势的标准地图。
- SATELLITE：卫星图，显示卫星照片的地图，只支持中国。
- HYBRID：混合地图，在显示卫星照片的同时也显示路网信息。

|   |   |
|---|---|
|**图1** 标准地图  <br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163648.33207722362037821610759885297849:50001231000000:2800:40CF62A71AFF0A1916B1640A33AE6AF8F7CD3A2C3254C5B081E0DBD32754F66F.jpg "点击放大")|**图2** 空地图  <br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163648.64511750156855257948172645274834:50001231000000:2800:C266464A1DF55B0EFDF9A52AFBBF7B110CD04E472EBF69B66F941759E3B0C7C8.jpg "点击放大")|
|**图3** 地形图  <br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163649.21786718306232372416282000525643:50001231000000:2800:4EF97D044ADF0CCF02D66DD2B7220EACEFA4D4CEF4BD9F75A47CC4A79F0A1E7D.jpg "点击放大")|**图4** 卫星图<br><br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163649.36044762937845427605613590834735:50001231000000:2800:3FF163C379AD3E66B76C34AE02A21AD5A12E83D3550ED323A6E5B4DB36FA4BF9.jpg "点击放大")|
|**图5** 混合地图  <br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163649.19842355175805789389854075504551:50001231000000:2800:C4F4DD5B4AC0F6FD69C7C35A2BB8ADBE3D64CF3BC1070D9B4A81593296AD406A.jpg "点击放大")||

## 接口说明

Map Kit提供2种方式设置地图类型：

方式一：在初始化的时候，通过设置[MapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section816451553012)中的[MapType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section18522846142615)来控制展示不同地图类型。

|属性名|描述|
|:--|:--|
|[mapCommon.MapOptions.MapType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section18522846142615)|地图初始化参数中的MapType地图类型。|

方式二：地图创建后，可通过[setMapType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section388992522618)方法动态设置地图类型。

|方法名|描述|
|:--|:--|
|[setMapType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section388992522618)(mapType: [mapCommon.MapType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section18522846142615)): void|设置地图类型。|

## 开发步骤

1. 导入相关模块。
    
    1. import { mapCommon } from '@kit.MapKit';
    
2. 设置地图类型。
    
    方式一：
    
    在地图初始化的时候，在mapOptions参数中新增mapType属性：[mapCommon.MapType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section18522846142615).STANDARD。
    
    1. this.mapOptions = {
    2.   position: {
    3.     target: {
    4.       latitude: 31.984410259206815,
    5.       longitude: 118.76625379397866
    6.     },
    7.     zoom: 15
    8.   },
    9.   mapType: mapCommon.MapType.STANDARD
    10. };
    
    显示效果如下：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163649.16322878853335138862483382282604:50001231000000:2800:82388D2851AAA9AD5DB4913A568C9A01E4DB285D4642FB5C745F22BA99E95C5F.png "点击放大")
    
    方式二：地图创建后，调用[setMapType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section388992522618)方法设置地图类型为地形图。而且，要将地图缩放层级控制在大于5且小于14的区间内才能看到地形图效果。
    
    1. this.mapController.setMapType(mapCommon.MapType.TERRAIN);
    
    显示效果如下：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163649.65607871375350470519101278322078:50001231000000:2800:9D513C839AE21B4A46DC3D3DBB53305A9D6F37F5D920ACCE5D76D20C8E22B6E6.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-presenting "显示地图")
# 显示我的位置

更新时间: 2025-12-16 16:37

## 场景介绍

从6.0.1(21)开始，支持更改我的位置相对覆盖物的顺序。

本章节将向您介绍如何开启和展示“我的位置”功能，“我的位置”指的是进入地图后点击“我的位置”显示当前位置点的功能。效果如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.09622215530719067781456202721878:50001231000000:2800:DEF9829F1B85F7A05A0D92D2B94AC134E9A0792A7CDF084F46BE4CB37D664844.png)

## 接口说明

“我的位置”功能主要由[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)的方法实现，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section201759451313)。

|方法名|描述|
|:--|:--|
|[setMyLocationEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section201759451313)(myLocationEnabled: boolean): void|“我的位置”图层功能开关，默认使用系统的连续定位能力显示用户位置。开关打开后，“我的位置”按钮默认显示在地图的右下角。点击“我的位置”按钮，将会在屏幕中心显示当前定位，以蓝色圆点的形式呈现。|
|[setMyLocationControlsEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section3464719101814)(enabled: boolean): void|设置是否启用“我的位置”按钮。只显示按钮，在不开启“我的位置”图层功能的情况下，点击按钮没反应。|
|[setMyLocation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1165002535516)(location: [geoLocationManager.Location](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#location)): void|设置“我的位置”坐标。<br><br>如果不使用Map Kit提供的默认定位行为，可以通过[Location Kit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/location-api)获取用户位置后，传给Map Kit。|
|[setMyLocationStyle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section126791641317)(style: [mapCommon.MyLocationStyle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section3713124215275)): Promise<void>|设置“我的位置”样式。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1446539113513)(type: 'myLocationButtonClick', callback: Callback<void>): void|监听“我的位置”按钮点击事件。|
|[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section546609133518)(type: 'myLocationButtonClick', callback?: Callback<void>): void|取消监听“我的位置”按钮点击事件。|

## 开发步骤

### 开启“我的位置”按钮

1. 启用“我的位置”之前，您需要确保您的应用可以获取用户定位。
    
    申请ohos.permission.LOCATION和ohos.permission.APPROXIMATELY_LOCATION权限，您需要在module.json5配置文件中声明所需要的权限，具体可参考[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)。
    
    1. {
    2.   "module" : {
    3.     // ...
    4.     "requestPermissions":[
    5.       {
    6.         // 允许应用在前台运行时获取位置信息
    7.         "name" : "ohos.permission.LOCATION",
    8.         // reason需要在/resources/base/element/string.json中新建
    9.         "reason": "$string:location_permission",
    10.         "usedScene": {
    11.           "abilities": [
    12.             "EntryAbility"
    13.           ],
    14.           "when":"inuse"
    15.         }
    16.       },
    17.       {
    18.         // 允许应用获取设备模糊位置信息
    19.         "name" : "ohos.permission.APPROXIMATELY_LOCATION",
    20.         // reason需要在/resources/base/element/string.json中新建
    21.         "reason": "$string:approximately_location_permission",
    22.         "usedScene": {
    23.           "abilities": [
    24.             "EntryAbility"
    25.           ],
    26.           "when":"inuse"
    27.         }
    28.       }
    29.     ]
    30.   }
    31. }
    
2. 初始化地图并获取[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)地图操作类对象。调用mapController对象的[setMyLocationEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section201759451313)方法启用“我的位置”功能。
    
    建议在获得用户授权后开启“我的位置”功能。
    
    1. import { abilityAccessCtrl, bundleManager, common, PermissionRequestResult, Permissions } from '@kit.AbilityKit';
    2. import { BusinessError, AsyncCallback } from '@kit.BasicServicesKit';
    3. import { MapComponent, mapCommon, map } from '@kit.MapKit';
    
    4. @Entry
    5. @Component
    6. struct LocationDemo {
    7.   private mapOptions?: mapCommon.MapOptions;
    8.   private callback?: AsyncCallback<map.MapComponentController>;
    9.   private mapController?: map.MapComponentController;
    10.   private mapEventManager?: map.MapEventManager;
    
    11.   aboutToAppear(): void {
    12.     // 地图初始化参数，设置地图中心点坐标及层级
    13.     this.mapOptions = {
    14.       position: {
    15.         target: {
    16.           latitude: 39.9,
    17.           longitude: 116.4
    18.         },
    19.         zoom: 10
    20.       }
    21.     };
    
    22.     // 地图初始化的回调
    23.     this.callback = async (err, mapController) => {
    24.       if (!err) {
    25.         // 获取地图的控制器类，用来操作地图
    26.         this.mapController = mapController;
    27.         this.mapEventManager = this.mapController.getEventManager();
    28.         let permission = await this.checkPermissions()
    29.         if (!permission) {
    30.           this.requestPermissions()
    31.           // 启用我的位置按钮
    32.           this.mapController?.setMyLocationControlsEnabled(true);
    33.         }
    34.       } else {
    35.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    36.       }
    37.     };
    38.   }
    
    39.   // 校验应用是否被授予定位权限，可以通过调用checkAccessToken()方法来校验当前是否已经授权。
    40.   async checkPermissions(): Promise<boolean> {
    41.     const permissions: Array<Permissions> = ['ohos.permission.LOCATION', 'ohos.permission.APPROXIMATELY_LOCATION'];
    42.     for (let permission of permissions) {
    43.       let grantStatus: abilityAccessCtrl.GrantStatus = await this.checkAccessToken(permission);
    44.       if (grantStatus === abilityAccessCtrl.GrantStatus.PERMISSION_GRANTED) {
    45.         // 启用我的位置图层，mapController为地图操作类对象
    46.         this.mapController?.setMyLocationEnabled(true);
    47.         // 启用我的位置按钮
    48.         this.mapController?.setMyLocationControlsEnabled(true);
    49.         return true;
    50.       }
    51.     }
    52.     return false;
    53.   }
    
    54.   // 如果没有被授予定位权限，动态向用户申请授权
    55.   requestPermissions(): void {
    56.     let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
    57.     atManager.requestPermissionsFromUser(this.getUIContext().getHostContext() as common.UIAbilityContext,
    58.       ['ohos.permission.LOCATION', 'ohos.permission.APPROXIMATELY_LOCATION'])
    59.       .then((data: PermissionRequestResult) => {
    60.         // 启用我的位置图层
    61.         this.mapController?.setMyLocationEnabled(true);
    62.       })
    63.       .catch((err: BusinessError) => {
    64.         console.error(`Failed to request permissions from user. Code is ${err.code}, message is ${err.message}`);
    65.       })
    66.   }
    
    67.   async checkAccessToken(permission: Permissions): Promise<abilityAccessCtrl.GrantStatus> {
    68.     let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
    69.     let grantStatus: abilityAccessCtrl.GrantStatus = abilityAccessCtrl.GrantStatus.PERMISSION_DENIED;
    
    70.     // 获取应用程序的accessTokenID
    71.     let tokenId: number = 0;
    72.     let bundleInfo: bundleManager.BundleInfo =
    73.       await bundleManager.getBundleInfoForSelf(bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_APPLICATION);
    74.     console.info('Succeeded in getting Bundle.');
    75.     let appInfo: bundleManager.ApplicationInfo = bundleInfo.appInfo;
    76.     tokenId = appInfo.accessTokenId;
    
    77.     // 校验应用是否被授予权限
    78.     grantStatus = await atManager.checkAccessToken(tokenId, permission);
    79.     console.info('Succeeded in checking access token.');
    80.     return grantStatus;
    81.   }
    
    82.   build() {
    83.     Stack() {
    84.       // 调用MapComponent组件初始化地图
    85.       MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback }).width('100%').height('100%');
    86.     }.height('100%')
    87.   }
    88. }
    
3. 检查“我的位置”功能是否成功启用。
    
    “我的位置”按钮![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.49044722398874659647943038304397:50001231000000:2800:4DDD4148F1FDC2E35A52CA248142D87383312277910D100DA6977FD90E42159E.png)默认显示在地图的右下角。点击“我的位置”按钮![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.72283332757603850653280768774030:50001231000000:2800:CA771DF220A053815962EE531D89A444B4D7831076747483EA7A78ACBA476767.png)，将会在屏幕中心显示当前定位，以蓝色圆点的形式呈现，效果如下图所示，效果根据获取到的用户位置会有变化。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.36456249089238195481778949082319:50001231000000:2800:9B347096131FF318FF6891556F6FE5FB42F6829352FDCF00A0D75D3091EDA683.png)
    
4. 获取用户位置坐标并设置用户的位置。
    
    Map Kit默认使用系统的连续定位能力，如果您希望定制显示频率或者精准度，可以调用[geoLocationManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager)相关接口获取用户位置坐标（WGS84坐标系）。注意访问设备的位置信息必须申请权限，并且获得用户授权，详情见[geoLocationManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager)。
    
    下面的示例仅显示一次定位结果，在获取到用户坐标后，调用mapController对象的[setMyLocation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1165002535516)设置用户的位置，[setMyLocation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1165002535516)接口使用的是WGS84坐标系。
    
    1. // 需要引入@kit.LocationKit模块
    2. import { geoLocationManager } from '@kit.LocationKit';
    3. // ...
    
    4. // 获取用户位置坐标
    5. let location = await geoLocationManager.getCurrentLocation();
    
    6. // 设置用户的位置
    7. this.mapController.setMyLocation(location);
    

### 监听“我的位置”按钮点击事件

通过调用[on('myLocationButtonClick')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1446539113513)方法，设置'myLocationButtonClick'事件监听。设置监听后“我的位置按钮”点击事件自定义，反之不设置则由Map Kit执行点击后默认事件，即地图移动到当前用户位置。

1. let callback = () => {
2.   console.info("myLocationButtonClick", `myLocationButtonClick`);
3. };
4. this.mapEventManager.on("myLocationButtonClick", callback);

### 隐藏“我的位置”按钮

控制是否显示“我的位置”按钮。

1. this.mapController.setMyLocationControlsEnabled(false);

### 自定义位置图标样式

通过调用mapController.[setMyLocationStyle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section126791641317)方法，设置用户位置图标样式。效果如下：

1. let style: mapCommon.MyLocationStyle = {
2.   anchorU: 0.5,
3.   anchorV: 0.5,
4.   radiusFillColor: 0xffff0000,
5.   // icon为自定义图标资源，使用时需要替换
6.   // 图标存放在resources/rawfile，icon参数传入rawfile文件夹下的相对路径
7.   icon: 'test.png'
8. };
9. await this.mapController.setMyLocationStyle(style);

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.42337143849277912834617865730769:50001231000000:2800:73DD4B723F875F72023AAEDEB284D218D8601C01CBEBFA642AFCE3C449D4AF0B.png)

### 更改我的位置图层相对于覆盖物的压盖顺序

通过调用mapController.[changeMyLocationLayerOrder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section16251915293)方法，更改我的位置图层相对于覆盖物的压盖顺序。效果如下：

1. // true：我的位置图层位于覆盖物之下
2. this.mapController?.changeMyLocationLayerOrder(true);

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.26262749304900695982404433687592:50001231000000:2800:C451B3141153244DAC7AC83FB157F3C982CE580F32E9ADD6818C55E30306C8BE.jpg "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-type "切换地图类型")
# 显示自定义地图

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将向您介绍如何在应用中添加自定义样式的地图。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163710.33618966210663667741718280922930:50001231000000:2800:54A7E5449260DC6BE0FEF73D35A213623D4E981F0CE138A1621A86CCCDB15E4D.png "点击放大")

## 接口说明

自定义样式功能主要由[CustomMapStyleOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section13899143818719)、[setCustomMapStyle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section70103143520)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section70103143520)。

|接口名|描述|
|:--|:--|
|[CustomMapStyleOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section13899143818719)|自定义样式参数。|
|[setCustomMapStyle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section70103143520)(customMapStyleOptions: [mapCommon.CustomMapStyleOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section13899143818719)): Promise<void>|将地图样式修改为自定义样式。|

## 开发步骤

Map Kit提供两种方法设置自定义地图样式：

- 设置样式ID：使用[Petal Maps Studio](https://developer.petalmaps.com/console/studio/)管理地图样式，并使用样式ID将它们链接到您的地图上。您可以在[Petal Maps Studio](https://developer.petalmaps.com/console/studio/)上创建新样式，或导入现有样式定义。样式一旦发布，使用此样式的应用都会自动应用新样式。
- 设置样式内容：通过传入自定义JSON更改地图样式，JSON的定义参见[样式参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-style#section156991344101012)。

### 设置样式ID

1. 导入相关模块。
    
    1. import { MapComponent, mapCommon, map } from '@kit.MapKit';
    2. import { AsyncCallback, BusinessError } from '@kit.BasicServicesKit';
    
2. 创建样式ID。
    
    1. 登录[Petal Maps Studio](https://developer.petalmaps.com/console/studio/)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163710.02883839715733124892212121009426:50001231000000:2800:796B2F9BDFC0A978DBDDD6155FB2BBC0BC5D07EF1563C853BB7847C4EB8DCA18.png "点击放大")
    
    2. 点击“Create map”创建自定义样式。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163711.21099529420431804655207021049947:50001231000000:2800:EF215530C6BE2CE36191AA4F7DC22AEA80AEBFF38935B050CD9B58745BE1ABA0.png "点击放大")
    
    3. 导入JSON样式文件，点击“Import”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163711.14141627966720706000674299178543:50001231000000:2800:3566B217BDD4A7EE8801EDCF397D9A0F4C2BD58E87322550464C1032BF82187D.png "点击放大")
    
    4. 在编辑器里修改样式。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163711.01484753453601789233390887674006:50001231000000:2800:75F643AD72C3F0A94EDF276D1BF0A14233C9AC8342B9C83DDFF11F9EBB4BF520.png "点击放大")
    
    5. 点击“SAVE”生成预览ID，预览ID在编辑样式时会重新生成，您可以通过预览ID测试样式效果。点击“PUBLISH”发布生成样式ID，样式ID是唯一ID，一旦发布生效不会变化。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163711.70709135444670866938112119348413:50001231000000:2800:4F3F4D59513F33EEEDCABDF9289C7821382A4D656598345068155B0A0D50D0F1.png "点击放大")
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163711.95498728023657709753548619637986:50001231000000:2800:934A9D50D1DE782C526DB269CCD2738A68E330D746924D6A5AA231351CE00066.png "点击放大")
        
3. Map Kit提供两种方法设置样式ID：
    - 在创建地图后设置样式ID
        
        1. @Entry
        2. @Component
        3. struct CustomMapStyleDemo {
        4.   private TAG = "CustomMapStyleDemo";
        5.   private mapOptions?: mapCommon.MapOptions;
        6.   private mapController?: map.MapComponentController;
        7.   private callback?: AsyncCallback<map.MapComponentController>;
        
        8.   aboutToAppear(): void {
        9.     // 地图初始化参数
        10.     this.mapOptions = {
        11.       position: {
        12.         target: {
        13.           latitude: 31.984410259206815,
        14.           longitude: 118.76625379397866
        15.         },
        16.         zoom: 15
        17.       }
        18.     };
        19.     this.callback = async (err, mapController) => {
        20.       if (!err) {
        21.         this.mapController = mapController;
        22.         // 自定义样式参数，styleId需要替换为您自己的样式ID或者预览ID，样式ID或者预览ID可在[Petal Maps Studio](https://developer.petalmaps.com/console/studio/)平台上创建
        23.         let param: mapCommon.CustomMapStyleOptions = {
        24.            styleId: "XXX"
        25.         };
        26.         // 设置自定义样式
        27.         await this.mapController.setCustomMapStyle(param).then(() => {
        28.           console.info(this.TAG + `setCustomMapStyle OK`);
        29.         }).catch((error: BusinessError) => {
        30.           console.error(this.TAG + `Failed in getting CustomMapStyle, code is：${error.code},message is ${error.message}`);
        31.         })
        32.       } else {
        33.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
        34.       }
        35.     };
        36.   }
        
        37.   build() {
        38.     Stack() {
        39.       Column() {
        40.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback });
        41.       }.width('100%')
        42.     }.height('100%')
        43.   }
        44. }
        
    - 在初始化地图时设置样式ID
        
        1. @Entry
        2. @Component
        3. struct CustomMapStyleDemo {
        4.   private mapOptions?: mapCommon.MapOptions;
        5.   private mapController?: map.MapComponentController;
        6.   private callback?: AsyncCallback<map.MapComponentController>;
        
        7.   aboutToAppear(): void {
        8.     // 地图初始化参数
        9.     this.mapOptions = {
        10.       position: {
        11.         target: {
        12.           latitude: 31.984410259206815,
        13.           longitude: 118.76625379397866
        14.         },
        15.         zoom: 15
        16.       },
        17.       // 自定义样式参数，styleId需要替换为您自己的样式ID或者预览ID，样式ID或者预览ID可在[Petal Maps Studio](https://developer.petalmaps.com/console/studio/)平台上创建
        18.       styleId: "XXX"
        19.     };
        20.     this.callback = async (err, mapController) => {
        21.       if (!err) {
        22.         this.mapController = mapController;
        23.       } else {
        24.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
        25.       }
        26.     };
        27.   }
        
        28.   build() {
        29.     Stack() {
        30.       Column() {
        31.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback });
        32.       }.width('100%')
        33.     }.height('100%')
        34.   }
        35. }
        
        设置样式ID之后效果如下：
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163711.85540242597378017250168148004718:50001231000000:2800:15AEF5DB4A815C728FCFB94E368BDA728EDD8C3804EAEC94C7555F60E25FA9A2.png "点击放大")
        

### 设置样式内容

1. 导入相关模块。
    
    1. import { MapComponent, mapCommon, map } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 设置样式内容。
    
    1. @Entry
    2. @Component
    3. struct CustomMapStyleDemo {
    4.   private mapOptions?: mapCommon.MapOptions;
    5.   private mapController?: map.MapComponentController;
    6.   private callback?: AsyncCallback<map.MapComponentController>;
    
    7.   aboutToAppear(): void {
    8.     // 地图初始化参数
    9.     this.mapOptions = {
    10.       position: {
    11.         target: {
    12.           latitude: 31.984410259206815,
    13.           longitude: 118.76625379397866
    14.         },
    15.         zoom: 15
    16.       }
    17.     };
    18.     this.callback = async (err, mapController) => {
    19.       if (!err) {
    20.         this.mapController = mapController;
    21.         // 自定义样式参数
    22.         let param: mapCommon.CustomMapStyleOptions = {
    23.                styleContent: `[{
    24.                    "mapFeature": "landcover.natural",
    25.                    "options": "geometry.fill",
    26.                    "paint": {
    27.                        "color": "#8FBC8F"
    28.                    }},
    29.                    {
    30.                   "mapFeature": "water",
    31.                   "options": "geometry.fill",
    32.                   "paint": {
    33.                       "color": "#4682B4"
    34.                   }}]`
    35.         };
    36.         // 设置自定义样式
    37.         await this.mapController.setCustomMapStyle(param);
    38.       } else {
    39.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    40.       }
    41.     };
    42.   }
    
    43.   build() {
    44.     Stack() {
    45.       Column() {
    46.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback });
    47.       }.width('100%')
    48.     }.height('100%')
    49.   }
    50. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163711.17664320498945310723297704316036:50001231000000:2800:5E9C31B673ADB76EBCF5939F46B63222E81852662A29E41D3E402AA688801301.png)
    

### 样式参考

自定义地图样式JSON内容通过下列4个元素来定义地图样式：

- mapFeature：地图要素
- options：元素选项
    - geometry.fill：几何填充
    - geometry.stroke：几何描边
    - geometry.icon：几何图标
    - labels.text.fill：文本填充
    - labels.text.stroke：文本描边
- paint：绘制属性
    - color：颜色，16进制颜色，例如“#FFFF00”
    - weight：线条宽度。整型值，[0, 8]，默认为0，大于0表示加宽
    - saturation：饱和度。整型值，[-100, 100]，默认为0
    - lightness：亮度。整型值，[-100, 100]，默认为0
    - icon-type：图标类型，目前支持night、simple、standard
- visibility：可见属性，默认为可见
    - true：可见
    - false：不可见

下列各表将向您展示支持修改的地图元素。

说明

- 图标类型icon-type支持范围为：standard/night/simple。
- 饱和度saturation和亮度lightness可在元素颜色color中进行配置。

1. All
    
    All代表全部，即所有类别的集合，支持能力范围同其他所有列表。
    
2. Administrative
    
    |元素类型<br><br>Feature type|Geometry|   |   |   |Labels|   |   |   |Icon|
    |:--|:--|:--|:--|:--|:--|:--|:--|:--|:--|
    |填充颜色<br><br>fill.<br><br>color|填充宽度<br><br>fill.<br><br>weight|描边颜色<br><br>stroke.<br><br>color|描边宽度<br><br>stroke.<br><br>weight|填充颜色<br><br>fill.<br><br>color|文本大小<br><br>fill.<br><br>weight|描边颜色<br><br>stroke.<br><br>color|描边大小<br><br>stroke.<br><br>weight|图标类型<br><br>icon-type|
    |:--|:--|:--|:--|:--|:--|:--|:--|:--|
    |Capital<br><br>首都|-|-|-|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163711.97169393703666587612087534813822:50001231000000:2800:826BEAD4E80B191EAF917DF57ED17E603939D6B43D76B69ABD6F93C5E1914B06.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163711.52803577749257058846524102068699:50001231000000:2800:6425333C62D86348180340F8E5F2EDB761ECDA87EC55CD846F8C866ADEECF42B.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163711.44614902130916634209624707129679:50001231000000:2800:72BFFB98C20E4A3B82B1D8BE961B93E1898C5FE1F8C2F11E3A3AF3DADE13878A.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163711.30409833064059108837013818490798:50001231000000:2800:3FE078889F4B9879CB892CA3F4D9C8256C225C7E709F738A12F01284D6E9BE06.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.39171897559816005527103651479200:50001231000000:2800:604C0A6E21FEBB3080F2FB464F6A1688077525983705A8AA1F65355B8DF8DF50.png)|
    |Country<br><br>国家|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.05097923481674001198771765120613:50001231000000:2800:F4322A95C203909C5B479BA6296560688C1F639F9649B0F83CA18B7AF9D5A303.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.47494391311773311785112822473414:50001231000000:2800:4F5976B91CF60EF25E2551BB3B4DDDC239C9D25261CA2FEC839ADB613F38E7D1.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.58999867208103956363006190447905:50001231000000:2800:E00D8BF875BDF04081B93CBC84065F5675E48F37F4C933BFEB3E2754638538CE.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.23416330257623006188477999028222:50001231000000:2800:1793F0E4607A0EF655A379DEE5FD3EA32F9D63983D3E117AF21D354DA60312CE.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.00602502264804502570415428901795:50001231000000:2800:7757CD44E406AA9CF91B87C8385F70519B9DCADBB791C8CB7430687D3D3AA3EC.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.18789772991897718649453838663823:50001231000000:2800:8FF2EA5E0DDE53E24FCA349ABAA9051E80C2709C26E3DB5E914186C1E19D5B9B.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.29750507626624195454262474813010:50001231000000:2800:3C7CB6E89A40059351B8122B1FD0EB16A5D190A8F194767DBAA5FB9DC912308C.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.74869045521142975505948921382353:50001231000000:2800:475EBD0338FF515C97555CC945726A86F76E3AD8C8065C1DB63067523A5BFF92.png)|-|
    |District<br><br>区/县|-|-|-|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.24502686701527575317513058467875:50001231000000:2800:387C8579366B0FEA7810DDDC60B64A2524297EDFE25D7D343CCF38BF0EAB34C3.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.29832930025475889254574220017732:50001231000000:2800:EBE4EE3A71485342CC2B6297CA33D6A481430736DDE0F85F8C933538355FA71E.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.08743882887587708150788128767669:50001231000000:2800:09D97819E45A01FD7D5681016C31B24B846A41F56C487265BDD9EEE3CCBA8FB7.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.39995849782049698676003379706721:50001231000000:2800:1207F63E40BBC79F6CB135FC4140C7F89CB0421C0B570F523CA66D3B0F20817C.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.15279602242945869455079539913786:50001231000000:2800:D20F8543110C06DA8557BF4211251F631A5069FF263299FE7F7C7561B9BCEA61.png)|
    |Locality<br><br>乡村、城镇|-|-|-|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.94417924322725327551361760833269:50001231000000:2800:ED8DAB6EB72EFB1708A620AF8F45946EB7ADEE6F042A7F4D562AC4658453274C.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.41615129645118418664020592483581:50001231000000:2800:F912BE4DDC5349958668ABA1577B6A552722E644ABBBD943CA9CB353E2162678.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.21943115223608286020888608318005:50001231000000:2800:21AA592D3D97CCC4220C5BDF272A6FCB58106E754D9E6F8AE22F8DBB6627016D.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163712.69104966287072522651300073260681:50001231000000:2800:7260A9B5F391A4058AF77A422B92D90A7979F5C8C937528DA584D93C18D685CB.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.21537507366827431912825467386695:50001231000000:2800:6582286D48EE93B4EB517D96AF9CCFD7208D81E638FF19198CD2D8B9003E25FE.png)|
    |Major-city<br><br>1-4级城市|-|-|-|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.09858659862375023727749617545369:50001231000000:2800:DFB860E12A7E1546922274E87D3D43D3ED1590FA28AC705BF4206152CE605605.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.43923343958377076078629333686721:50001231000000:2800:00C63E733B18A3D40C187F88E29A68E80061871A262A864BAD9E47AF3AAC7283.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.34586020160264358687283132002550:50001231000000:2800:DF4F2AF445A3539620F4ED95102EC887241FDF8A8E1E476E21C133792280657A.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.19661362233844886693079009315588:50001231000000:2800:379AE12AA7069C1B56E0134E256CD9D5CBB7C75C2DDA66F698FF28113BD93DC7.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.41322373413080945257474970765182:50001231000000:2800:BC9AF752760B28A3A76FC857159CAAB53661D579D3FD3C5EEACFE8A7F1825769.png)|
    |Province<br><br>省|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.13406957234572571716942444564892:50001231000000:2800:84B59249FDCA985AFDA0C640B8FDAD1299B452FEA58710321453F588686A63BD.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.74432634071158592730310687463106:50001231000000:2800:A7F383A965AD14C2090BC8ADE10FE034FFA9E12C863003E9A6F64C0A54F93054.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.81246705962481482708683374751968:50001231000000:2800:7155867BD720E84A629E3B7F4F2833EA024601F57838899D1A62720DEF0DAFB7.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.30297154325671398365999839626957:50001231000000:2800:2454109DF7F78546EB3F5C20CC8B21DD9728957B1513B6FB81E2A76C87AC0BE5.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.15269626104199200926697865412816:50001231000000:2800:2C9B941BF87128484740A037897583932948ADF349B0D9900042F3EFDB390777.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.43699539605502654172885342114335:50001231000000:2800:E7D98C65FD0077535D852B157F18EC01B540C3E1C529D6E00506FAB7CEB8AA38.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.76949599239623122053475389658893:50001231000000:2800:252D1A3B5041C286939C9E0D677E26091A859122A5006ACFE5727B630F6C1B1D.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.33877054513592911337246545451521:50001231000000:2800:0C4D7EC70A11DA4800D8229FB6D8A85E70A463FEEDDCAF92C1B57E23F9654CCA.png)|-|
    
3. Landcover
    
    |元素类型<br><br>Feature type|Geometry|   |Labels|   |   |   |
    |:--|:--|:--|:--|:--|:--|:--|
    |填充颜色<br><br>fill.color|描边颜色<br><br>stroke.color|填充颜色<br><br>fill.color|文本大小<br><br>fill.weight|描边颜色<br><br>stroke.color|描边大小<br><br>stroke.weight|
    |:--|:--|:--|:--|:--|:--|
    |Attraction<br><br>游乐场、动植物园等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.13056478961610571906683302398063:50001231000000:2800:AC04FD990BD1F6F995E04121E99AB26CAAC3E5BC7DB2CCB188DC364C92B39CAD.png)|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.84805212603044106675841253385750:50001231000000:2800:230DBC078768F256AC9BFF98334F0675E93CDBF9C60CE8B0CEC961EC51DB5FA5.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.27202654768542076729403435694216:50001231000000:2800:4821602C6E169EB7DA516EFADD7BE38F3F325B5496093CA1C165B069D8CE83BF.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.40722976397639480189967619832592:50001231000000:2800:31E0D8EBD0A29191F1E54853BAAF794D55AD537A8CC9F2B3CE69D5D44CEABA67.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.80212938779248803293755879660488:50001231000000:2800:A7289E864326EA7CEA7607891255573CDC086146578911CDD1F3F9E2804DC487.png)|
    |Business<br><br>购物中心、商业区等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163713.56764400797864009973803104842182:50001231000000:2800:CB8843ED29ED24D5D7602794D1563D90F98C7EE761882432A27A29442AEBB8A8.png)|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.49799393289993715935281501661800:50001231000000:2800:8C7FBE80532B57F35B84DB466F5B60E9C9CF42E500AA2FCBCAAA3D5E205F2220.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.88423502897878680372333555675691:50001231000000:2800:81E3D4C0597C27645126EFE0BBEA02077DD1FB92A28E440F95B9309FD9308A4D.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.66484718512822952605229642676522:50001231000000:2800:21BC538142B453912E72F4B3C4D6DB2F11D732FE9468D19A786DB5D011189D05.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.30569965113657532780856692611177:50001231000000:2800:E09D65217651C61AE606886E727863F0FF984DFDE83229DB782AA3B999CA7A4B.png)|
    |College<br><br>学校|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.40861413631464942085292612587853:50001231000000:2800:A3217E01CA1C264BF3491CA31E0A7ED86E3E84133244D424AA1AD5C38DAF83D0.png)|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.90705713595332378886732903720053:50001231000000:2800:846837C805211457FC48101592F84F650CDEED98BEF53AD9B567A5E50765997C.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.76915355433748446370866690081617:50001231000000:2800:52C410D9BA8EA4BB913B704ACA0C1D8CFE471FCBDC14E6654B1700B79EDD3103.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.73817594765639907963809559401682:50001231000000:2800:226B1C064A99276D6FC4B36CCE72921C2FB90C7101FA9457B1CBE8447EE27ADC.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.62537289225488243737250698124361:50001231000000:2800:C6BB2F44238935430C1395BB4E0DF48F6C3E4BF55082A6AB71787D64695135CA.png)|
    |Hospital<br><br>医院|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.74753372330152208360220352720092:50001231000000:2800:BF0F2AD9400CC514CC7A14C78589D54E187CBEC0B8373167E1A973F18252FE76.png)|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.89580919449311967974785755485746:50001231000000:2800:3CA413ECC29791094441D7EF6A68FA3A2085BB9CA1C8A10BABAF49F05E9226ED.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.04082752202350564789790598780951:50001231000000:2800:06B66BADDA6005D9E60364223ACE6402C9AA0CBBCC1785EFECCA0AFE0658E932.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.88748696020944897153375633329079:50001231000000:2800:F3A1AEBEDD5454AA591811FCE6DD6C4888281BF8EF7CE300C56670B7A8939B70.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.17736484949456201761701239767727:50001231000000:2800:F3B9C8EAE61566BA0FF7E6A42329E45D3911523144F2EEE11414904B5268F79D.png)|
    |Human-made<br><br>聚集区、小区、工业区、监狱地面等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.65673163010757795755356301041262:50001231000000:2800:16ADCCCAA5CC87D59235C1BAD7BAB0D64B5DF111626FCB2EE4A30577FB4C4EE9.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.33689288936768684135652683849965:50001231000000:2800:88D63B2FA1CB022ED7FBC570BC5D7B65BD1E1F7EF9FDB73A891091F121206469.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.14143388540495127579830444486177:50001231000000:2800:045F2A781CC00444DE1569EB327EBD271B4800ECFB8156024DC1397BC64D5B6E.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.83771244952835026063728991585071:50001231000000:2800:06330D445C78FDEB12AE3E6FBB009F09A8DE8815004264A11C798886C9EA0451.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.60312629072745737926888888166232:50001231000000:2800:F8DB939F0219D9D11653B53BE476D049976338D6882E7CF64C5592A4BA958782.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163714.37479414848362813742088944432911:50001231000000:2800:F3C60115850757BAF6E7041044659A5503AE16D7B586C728F29E7B7B1BBFA8F4.png)|
    |Human-made<br><br>建筑物|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.74490489192136423430032080060140:50001231000000:2800:4F2ED091FA842DF588924506B35E378DF95FB5548E979FD5BB85661FA8FDBF90.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.39638443322610045101972305504266:50001231000000:2800:D82DFE14AB2BF305EE46ABAAB7E1D9991FF78FD3087C7841D023C1181F79C56D.png)|-|-|-|-|
    |Natural<br><br>陆地、岛屿、海滩、冰川等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.66286085104584818933996911522875:50001231000000:2800:3ED0A3618320638C14C359290BC274C57458ED119F700719620E18C820683E51.png)|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.55129089563363407465280230790222:50001231000000:2800:10B2021F6A701A938AB5E8B7B25A1DFC4EBB95937859ABFFE92950F990940472.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.45220434002998513227103540958093:50001231000000:2800:DCE22438C431754389F0926738FBBA46C3A28119B8F58F788C85A453A16D51F9.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.20939843495135295093941964683436:50001231000000:2800:D5301F1831AB33F6BF2B3E0687232957621E56CC26A3F482EA57BB77F664BA6D.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.92506885826169040203594080516847:50001231000000:2800:0C4F262A67289E4B9E72DED829BE2C818A8818ED1E0E33D98513FF19A4E5E311.png)|
    |Parkland<br><br>森林、公园、荒地、高尔夫球场等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.88685557284556885408840340381458:50001231000000:2800:718E68BF6353AF64F31A8DB40C53D6E8493AC59BAAC5201FFB39A78A1F9CB751.png)|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.59634750734001874713613438121300:50001231000000:2800:BEE5928EDFFFDEB9D915715DA4E45A23D4FD042E6025BF86C03199719324FFB0.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.05999532881348695771767951861805:50001231000000:2800:CC99D08D6FA2E62D5044468B11F2D383044F3CB9A67E615A85144170FE6EA8B0.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.95568333749125207146592328587902:50001231000000:2800:5821A88E06366B96617BEB8C751F4097EFC671DEFAB1E3E415B224648DE8FCBB.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.20209232990721507402627839764569:50001231000000:2800:11D7F6CC44A08D51B5E1C4314AA57AD3FDE36D2A08C9A2641EBBD72398AA3388.png)|
    
4. Poi
    
    |元素类型<br><br>Feature type|Labels|   |   |   |Icon|
    |:--|:--|:--|:--|:--|:--|
    |填充颜色<br><br>fill.color|文本大小<br><br>fill.weight|描边颜色<br><br>stroke.color|描边大小<br><br>stroke.weight|图标类型<br><br>icon-type|
    |:--|:--|:--|:--|:--|
    |Airport<br><br>飞机场|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.85282501174160642584108795669816:50001231000000:2800:517233EBF99E8B6C4CEF03CE8660B08E9CE5B2B2D19635BD1F22D087C811B581.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.56954059328766545007989523038755:50001231000000:2800:21D09462BA840897E79AF9F9D199508E9AA7AA52C198CE2874519225DDAA6F56.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.27901537085358730777612003810922:50001231000000:2800:B9B4128F1635036C2A2595BB996EFF1F71A179CDE2612FE13711520203FA83DF.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.30452729015252794820051741711979:50001231000000:2800:BFED0C463CF822374F6F7F00A2E69462D44C89FFCDEAA27C508616964C78CEE6.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.77851261168214236835894673328262:50001231000000:2800:3E5C84BEA813608F2AC7E0854D2FDC85C166566FCE6C4FAAB4E303F09ABBBF24.png)|
    |Automotive<br><br>汽修、充电桩、洗车等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.35382087938446638815211679408635:50001231000000:2800:143739A465676C7A301D89AE0CE0616E73722FB977F890ED29FC7280690DEF17.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.30471587830370528805874847032038:50001231000000:2800:113589355E137F94457A35A370A427885FA356D66EB8E7CA5D2617ED53E6BE8E.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163715.85846076575286143758289367261643:50001231000000:2800:6F6B3936FBB691A2B6690EF767491E0DD87832F0ADADFDE5C71EF7FAFC1CF8BB.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.06212099784381979685492513672568:50001231000000:2800:D3B1B6F2851A8D75EF683471C85AFE225167EB65DAEF6969D281F44DB82048D5.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.78691243192320685286798164388393:50001231000000:2800:EB0BFE8A1E0DBC5D9F00E9745EA268011BEA196414F24A4A17412A683B91C314.png)|
    |Beauty<br><br>美容中心|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.71065596081079187377674512273755:50001231000000:2800:34D176E3219214AE5522BE3FAE08E11565D3DF2D9E32CF44165159E21C4F3310.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.95268652048396590330873256460617:50001231000000:2800:A5BC1BFA4D17A7C2A31DE8BD5E629E2CA645BC8F726F65E1960CE6AC14778A74.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.82145770941329789728563090009718:50001231000000:2800:42DBAC88E54FFC24F2301A4AFA45DAEA5132A9639B435074BD7880FDC055365C.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.48111873955253676829489944140571:50001231000000:2800:ADC067CB30462DA0FC5A5D9D89FA7C48E46569CC933265B90939C86B4192D4F4.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.54241103324847258289696790415012:50001231000000:2800:E0533E41678383888E91096A0DA386C91E29ED5E78BB1EA3D712B5D32293CA2E.png)|
    |Business<br><br>公司、商业楼等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.88134717322533691308894538385319:50001231000000:2800:633E707A3F5573CED6C96F1C9AB37535B4A6700E09104952AEC011443F6BB8DD.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.00135844772010571126308508703559:50001231000000:2800:8F57FE2B3DBE67A0BA9A2E24292F693D0DC7F065FF6DDB0615D9E205BF0FB1B1.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.10664302622149568795471866007131:50001231000000:2800:35AE0BD844DA934E3984E3BE2A1DAE986B86D8BE17F28BF1FDB50EAA0DB815AA.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.65369420041406665809714221711693:50001231000000:2800:3935C01AA6D8E62EBC49C5AC9EFDDC600205333C0FD408CCCCDF49A2E24C779B.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.43259924043492179817121300425507:50001231000000:2800:0058FFFF34E4476E4EE1FC7D1FA7C24886CE0A9A18BC8543B53A9C7A32019648.png)|
    |Eating&drinking<br><br>饮食快餐|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.79511444616407269988105925183609:50001231000000:2800:E3DEB9D168460BE3FD1DC3ACFF77E8BFCC804D0111048ACA9A1D16D2A86EE850.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.55255219996803095701352852424484:50001231000000:2800:081A7BF664E3688D206493068235FDA7010DC732A3F54550CA01304EE1DFD343.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.63977357848842811214185295071552:50001231000000:2800:85F7E62EEA08FB044248F6EB7605545FEDABABCE98D8C03D47118603B9161219.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.24324120028310457206490803034204:50001231000000:2800:637BB42A53E44CFCBE8472C666D8DDB52E9A01B8CDB62E7FB2DC5CA49128BCDC.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.97212710166542190927468600481799:50001231000000:2800:9C205CC13EB4DA02707EE331FBC7C28C7FC88BD680F2D8925BA6C6A73359FA01.png)|
    |Health-care<br><br>医院、诊所、药店等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163716.10742238456126393035998408384343:50001231000000:2800:7EDBFA3E96C94488AA0C73F5D41AC8C5ADE1057F619154D895808ED069842258.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.75731144018653315719766471197801:50001231000000:2800:2A393A2599D2D9F6ECF864931EF54E142005440C14C6D0B2C26B0AB6D4391A53.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.74940245369588842899565597533865:50001231000000:2800:1A7F3670D8456CABD85562A6F932118BC8F2434D293E3365D7862A2F5C6A7DCF.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.83303684117208627018796255024629:50001231000000:2800:6CCD7AF035A7C2F9EB5EC7EB41626B1DD5588BC9744FE7E14F7BBB773617A1BF.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.27636435825124441900933534637063:50001231000000:2800:454EB4DCAF0D1168876BCAFF04F2DC99897FFF4A0A7404E3B201A420F8E90374.png)|
    |Leisure<br><br>休闲娱乐|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.59513129539345214931121895142404:50001231000000:2800:A252345E0144CC070742100142D5126EAAD72060C9FBE8A5D559DE3202363262.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.90237564498943073420052438466962:50001231000000:2800:BD4A0EED121EEBAA9F77AD63B30324F3A67E82061632737481D5190E14A71D93.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.87207360553589764764823575650748:50001231000000:2800:28E287821C96901780E5C92EA76EF1DD25EA4DFB884B8FD049356C4D6CBF85A6.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.31950748459664830526044026632824:50001231000000:2800:6F51C53982D39A8D515E9A4154A3B716646F4A7506D15F107A772B366CD17421.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.97256237473780024868744105329348:50001231000000:2800:694E6FC68962E557008872EFEDFC362F840DFFEE841F70C3EC372AAB13DA46C2.png)|
    |Lodging<br><br>酒店、住宿点|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.46108267865990444024275719357390:50001231000000:2800:BC25AAF2BA01D6A913F4D48B4AB0F4E1FAE5CC76C547F113BF61D8BBD9EF6D68.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.93633708808095533551896369248096:50001231000000:2800:731C4C6BB3AAEE137419D3D036BB5E7E510ADEC183538248A3325055BCB9D203.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.47918488560409229263815154475222:50001231000000:2800:E75244BDCB84C9680EF8704343B04D9693DD58B35B5580E2F4D04ECA391E4FFC.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.10254210956566066757694416340457:50001231000000:2800:61E0E1AEFA2BC8D7390F6517F65860CFE7B99B632C17B6A5AF14513C93E19C57.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.13046208611805128379661331379205:50001231000000:2800:269FDD03AD64461EA14A5F2F02F9B4297DC768017A9DC55A5B4CCFF709F320A7.png)|
    |Miscellaneous<br><br>自然地物|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.94960193381746698472462804309755:50001231000000:2800:AEA3CF83C53CDCF1BB08CDE4ABCCD0A79AF84500D7F4DD7AF3F7B25A0C1C492E.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.20977756393910307445230130201071:50001231000000:2800:E80824DA3F17D3C1D2DEC523A39CF6FFD56A2ECDE6789BE332B1D284A3085E43.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.08299578575882003835119515238041:50001231000000:2800:7CCA738900EC116C096AD615976AA38D7305831A8D9C67BBDF5E2AA47983A92C.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163717.35694466166406919537148646358452:50001231000000:2800:BA74AC8274F4E5A7EAF190EB838C91D2FC711DE3B5518CA3869FEA428F95B8BD.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.57668552453077794037211214154288:50001231000000:2800:E0BAE8F5D3053349113207F8DD86FAB8C5106032A6556B232E54C2AA7C559568.png)|
    |Natural<br><br>山峰、森林等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.49123175015454557561379300644599:50001231000000:2800:0D1F8BD04728DFE17AB1C74778A0E62435F8EB617DB25CCC174F42FC81F28B99.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.87958892688770293573826081545652:50001231000000:2800:3A1565B498DD0598AA839099081CB94AECF161F973043C75298D9BE12C3243A3.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.42701037863962754708247112915879:50001231000000:2800:21C45E3E8FA9A51DA2FCB9D59B4A5081939893EBB1D933A4BC749793C9FF4C75.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.36297409558178174199494621115902:50001231000000:2800:D196F7ACAED60E2234FF1DA51818FDED033331D00D16C9B15D4498E632483519.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.21763845082113702263963728013604:50001231000000:2800:6623C602CA24145299E9E2EC8C3312A8C38035FF3F956523F8BE06218BBE3E82.png)|
    |Public-service<br><br>医院、诊所、药店等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.48148844304393385920483273847104:50001231000000:2800:A72219D3952F157DAC0D98A676F5D5EE5F7C0CE71AA8E8A5E9BDFEF35EA467C8.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.97652325304212680511929464276631:50001231000000:2800:2F590BAD4462DDB1262A07942858721067D17F737AAB808580EA6595C57FBCD7.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.22680351702608112814286900505255:50001231000000:2800:EE25CEE01B6C0ECF60815F9B069CF7E9A1C790929763F7D172A14138116F6D5B.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.72950495766827631279630313544450:50001231000000:2800:99DCE15E57154198CE59CFF116A7113694244EC1F4C2648499B17CF907FCB399.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.98391307802350424876350206409428:50001231000000:2800:C6E24EAA684BD7BED1D565C81452C3982F1C1E1A1566B08CF0919443D4E95362.png)|
    |Railway<br><br>铁路|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.02508231721616184826921500513985:50001231000000:2800:0055A918752C62462AB50449A55EEB41707D1268021521CD6991D529ECF0B834.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.03085217681074921754983775871179:50001231000000:2800:066FA1CD593157E2F768860397BB89EF47174B7C594209399CE1BD5AA2F90640.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.98053379096963611187474100980025:50001231000000:2800:E8292DFD2535ACA34922643EEE544061216C863B1D1E33E2DB63DB7A42DFA9D2.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.27228708119196681418356151523945:50001231000000:2800:01E276AD44E6771986043BD9E819C1EEA1941F7B90014A6B8A9543CF5B8F90E4.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.83463305191200950038516425898024:50001231000000:2800:4BBB7380B3F68EA80D1D1E8E918EE8E109439BC5522B9EAF9A0CA6A2298EDE0B.png)|
    |Shopping<br><br>购物中心、市场等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.88408482655632951326053430868652:50001231000000:2800:0D4BD53A1473CF6CA8211349705D7F6D446F3A7D434BC11C787C3BD80950C97E.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.00748518546786646849027128436607:50001231000000:2800:4825A941E9C1AAC3D53A4E20529532B2DCC2795C87743305005FFAB4EB0EE2DF.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163718.42774410873523134024537740491158:50001231000000:2800:22EC292E886EC49220A2CEE4AE7C591EEB796E09B89699B2A7CC86181DE2A118.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.20020097531988661508954727744725:50001231000000:2800:DAA8CD76BDDDC06EBBA021293B11CF83725DB8BAB8F9B12008E3D992D0112D59.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.16985466277398676641266452768162:50001231000000:2800:4E1198BB93243A7E8DA37A22A5D92D78AC513A9AAA5EE614BB95F2E28964E8CA.png)|
    |Sports-outdoor<br><br>户外运动、爬山、骑车等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.27952568518085367520436353948076:50001231000000:2800:B9EEA8A37A89CDD19C0EAFE3E056E5EF08EBBBF4FFB9D4CBDD3363BBE558CEF1.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.76512777503895529416511623707138:50001231000000:2800:4F424903D8C9967A8E155F2B789922C0F4E9ED5152A91BBCB324ACFF01E3B552.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.40732089663145161417267936019306:50001231000000:2800:71B7C1FCBC8084A04B248CDF32394E6E58C2D1A9126151733F1D4DB0525C2750.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.17304848785017921619208282902539:50001231000000:2800:87CF2AD1D570B40069326F77BAC9EDF88A810DADD219B0317C267734EBE2DF07.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.88516034591351620324824660923461:50001231000000:2800:98E1E715901B54BB1266913914413F9FDB241D191DC64AAD4E0917A622245CC4.png)|
    |Tourism<br><br>旅游景点、历史遗迹、教堂等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.17462134136474670054023240674820:50001231000000:2800:1154D6E325E41F9D1D6FDA6695B0B14326156452DA33B3E22BE9137AB465F80F.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.49947480983385004856826379816204:50001231000000:2800:2BFF6B4CBD5AC4E933449969B6C71C7C1B9DF040B9B738AE2408D1283802C717.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.88383110177483400817466348207010:50001231000000:2800:F2738040CA3776BBDBFDCCEE9AC8DDE0E484D10C8FD1072378575FD0C2B83454.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.61760738444509923390434170581262:50001231000000:2800:B11416FBE2AA9BE9B1CFA4FB6F8CAF98CAB336CF4E0C99BCE21E1264D4B1E763.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.34837396935793399975081543065324:50001231000000:2800:D1D8B596679BA2F8FC00FBF2AB5F3CCD18FE4F5528E60746AFA3F57240D1EA03.png)|
    
5. Road
    
    |元素类型<br><br>Feature type|Geometry|   |   |   |Labels|   |   |   |Icon|
    |:--|:--|:--|:--|:--|:--|:--|:--|:--|:--|
    |填充颜色<br><br>fill.<br><br>color|填充宽度<br><br>fill.<br><br>weight|描边颜色<br><br>stroke.<br><br>color|描边宽度<br><br>stroke.<br><br>weight|填充颜色<br><br>fill.<br><br>color|文本大小<br><br>fill.<br><br>weight|描边颜色<br><br>stroke.<br><br>color|描边大小<br><br>stroke.<br><br>weight|图标类型<br><br>icon-type|
    |:--|:--|:--|:--|:--|:--|:--|:--|:--|
    |City-arterial<br><br>城市主干道|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.28850090170761331420741010866211:50001231000000:2800:DBB9907C0A0EC5057AA33FAEB932FA0DB5503B94468B5F92378E813DEB8D8844.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.19776945274202628918532315671502:50001231000000:2800:0EF7277A4ED53324CBD299289628CBE4A4B5DB11E158486F290BC3C0D9D8270F.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.09048043703058740373805542742238:50001231000000:2800:32C10AAA6CE103CF7E4C4B645D1FCBAA766484C00B27E4481F61E0B26DFA6D69.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.53632817615576564689268518283742:50001231000000:2800:6807D0BBCF5AED32543787C27F44C64C303F3C2C473DF39DB6F1728450601E98.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.11302416972231774654129772605250:50001231000000:2800:01C2F10DB518810332FADAEF49790731469C24A7EE3A0C1C59F4ABB77424236F.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.61162716770536103917068735000491:50001231000000:2800:B8BFEBDF914912E1E91F96BF24F7D2BF56675702CD8B73E97ACE1ED198CB22D6.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.99776931000985356850901486714499:50001231000000:2800:ABC6EFEF3AE576DE006AB079961D492D4DD0C393DAF33BBDF52424C66A92F5B7.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163719.46895995183305486042418482505033:50001231000000:2800:58E4A8FA556B6C09158FB93C303659DC5661786061F7E0D8E2B9F4AF9A3EC97C.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.31229146125260227506117709513204:50001231000000:2800:24D5A4DE338E04F7787FBC8B6A2B4434F984FB3B1718C48EEF39037CB0571197.png)|
    |Highway<br><br>城市高速|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.31801478399040473850053317845180:50001231000000:2800:A99D5A76F09D72896903631C0B74CCE8954EB7C256807E603044DBD268F2D544.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.81509517872741589785867362094789:50001231000000:2800:5161CD6907EC0D9265DC18B873D770024654380288309742A290CB3E6F769F97.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.68964102974383297417504413430571:50001231000000:2800:DC1DAD1776C4E4EDDDE4109BD0CCF20A2B834C13EA909D6BA25123FBAB295472.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.39056797849671359176849010242779:50001231000000:2800:059ABF63D6D5BF5D3179DFCD6DC99D72DCC891275F1232A62D19A06A824D117D.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.75701866599890014869643381656792:50001231000000:2800:F1873DA358341DECE16737B5CADD49A545D634077CEAD7F3285CE2EC6F73026E.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.75561635937334492820757254290926:50001231000000:2800:19A4BCE12B1D1091A51E4D3676E7F5DC4336453A0DA69544BA987A41AAAB065C.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.31837326777067164354824744880728:50001231000000:2800:98296391C05689C45356EE0F46DCC99D2A5C57DB400B2081F9A8DD91E979AC5F.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.70488612767119897957075765057396:50001231000000:2800:81B7293E4DA4D6B53162BB2707062633BE02A08AEF4B629DA3B2BBDA35B7758D.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.19204833279630732342299097505056:50001231000000:2800:617ACFD5029148492F05F88B39F789203C3CC64C7F3D425C589646D6C5382344.png)|
    |Minor-road<br><br>市区内支线等|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.02746844252875906239983533560956:50001231000000:2800:AAC10CCC1AB835916850FE94E29C1F77E1F4A73E449DE2F8EA122CB797613379.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.32268879865836416917321353282083:50001231000000:2800:308D35FA4E221C21829F74CF35876F8B01282FFA3CA236DE9AB93469BF4C48BC.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.29211417120860826248078400875171:50001231000000:2800:06C3115CF1D1EC709B368B21CD9C3FC99333667E6158C6D2545B96783509069D.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.80802245170659839085752186633325:50001231000000:2800:35AC197F4D81AA72A910AF2E18BECC11BFC2729757D42B9565E11FC1DF80A918.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.59995209621670202272434185210121:50001231000000:2800:7AF0EBF514FB09B795FCC401314AAF1C4B8B419327336CE085528CBA2B03C864.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163720.49128671651254892650877981122805:50001231000000:2800:9B976B76C9B160F6CD665F5B3870AA34C9A80CAD1833C61EF25BA10085DDBBB6.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.29563297885798208796223425515201:50001231000000:2800:5C9921101274163610F97A0A4E53C1CED30A628282F624189BEB8495B0A9AC88.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.35213065646421408164621893551926:50001231000000:2800:1FD0313DE933339A5DCE5D7E4148806F330A45443D9D66F88AF1BCCDA5B68D5F.png)|-|
    |National<br><br>国道|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.62509749691655635460440016056744:50001231000000:2800:7A57B27B37628EDB00F342C7D051D7E2756A1DBF07463C09D305ABE43DCB74D4.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.87070393650776442211125080377523:50001231000000:2800:200360C1031594368C0890BCB31DD019E1DA095C0A7F92A161E68A4664567716.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.04614686369256237869897422142181:50001231000000:2800:54D87F6AF036FD358D5A53E73F77A7D0858C296D001F66C40EEDF118EB4CFDAA.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.46981754367912665005311186619414:50001231000000:2800:EE8031E51709B8547C1A23C7A2863BD4F6EF172AB61BFC62334C065BE04F16B3.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.44967047191775805977712947235481:50001231000000:2800:DEC649638291D566B2CC0AB633B5F398F697DBE2FF0ACBCC53F5EBCD22361286.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.93653713779342627401928024405049:50001231000000:2800:BE65F749AED4A02E0D9F5B0CEACB8DBCB3742CA5B6991F96C0E364230DA0B585.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.88525161680171710822207634217797:50001231000000:2800:4F3CE51E90081AA8CEAA07966D729DC5F02DEF0EE310150C250E8A5C4AE87310.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.34395120847565630199432330096858:50001231000000:2800:281C5740CCDC3886EDD8CEDD88DD5C0910DF07129D922B60E86BB528B72A98C0.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.18413162934325180140716521566045:50001231000000:2800:981CB8432809C8B29F7912F395577A10523655F410C2D66B6866B9267694B5FE.png)|
    |Province<br><br>省道|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.00709426142639821006586005438245:50001231000000:2800:F41B94AFCF36AB1397F0FB4EAF5B85443ED8025DB5FCFD8604838BC683968B4D.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.79855791861217623445025439590971:50001231000000:2800:2FEE6FB17256B5A47CB1B0D0CB07288FFDFD8E7F023D2BC8994E293EEEDDF493.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.14634306219957091773271974292223:50001231000000:2800:AB5DC50AFCB303ECE828AE878D188752C8E67EBEB91783B24538D5BC7845FD87.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.68878670701184572550678021873533:50001231000000:2800:20FC1076D92DE9C8DEFBA0A761CE3A1AA4AEEA6629713D6E4922AD53920E27CC.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.96313105753241389006895026332625:50001231000000:2800:5665D6F96781ED7A8530E44F669D84C108F69BDB8358BB929DA1FAC6C691A2F2.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163721.27188928475976102872069156695902:50001231000000:2800:BA9093329F05E62B77F9013E2A18501C3A3408918A916705243A21FF72B8CBCB.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.23927816974138329200832277907906:50001231000000:2800:46CFC0754DEFD22A31A93F741A0993B5762B8A2F7418CFCF1B719CD60A181797.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.48366248722115922553379320143008:50001231000000:2800:72DC29027E071A1449D5E5DD28A70F72B7A07A4B3FEC669CA2D1D7086D08C75C.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.91816871967033682593158974666680:50001231000000:2800:33310B481F6D483862DFF87AC24769EBF78E3C40FA0D8C5A55068D8C5F663DAC.png)|
    |Sidewalk<br><br>人行道|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.29952368936246609027504583395180:50001231000000:2800:31282368A3D9B8E3BE4F2374B5F310F02F8D450FBBF0026AEFB19BC911168250.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.80398742642889324780288239418603:50001231000000:2800:F4B712DD5B568489FD512873F2B73F1C4160A3C26FC3C7A371710FEDA4228FE6.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.40562552609187160133557224342685:50001231000000:2800:95ED104E88051306B09822238C148598ECA895B35F2B6532D5E07595D90DC3F2.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.54751671663624207794087314625723:50001231000000:2800:D45A8C76931A68055D0204059E63F9C97B20EB47D5591AAC74D94D33984087CD.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.90356638041156541372034822554821:50001231000000:2800:9E9C77E4650A16DD62D1EB3498A07CC0F4169B21102748B35AC3B6AF76DB9A2B.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.35814474792048734078030743328132:50001231000000:2800:8CB2B483714EFC6A1BFEC8BC55DA7D46D9DC2243226EE94BA8D088B9CE74763A.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.84199267179236403237828398382994:50001231000000:2800:9203BDFBBAF0B340A65B0B623C0946F748910F1EF71D6C56798F7B09E70FAFE0.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.56260076659672195353756144186207:50001231000000:2800:B26A114438DF46FF2BBA0E6FC6513275022F52F02FF4027E2023506FD1AC02D0.png)|-|
    
6. Trafficinfo
    
    |元素类型<br><br>Feature type|Geometry|Labels|   |
    |:--|:--|:--|:--|
    |填充颜色<br><br>fill.color|填充颜色<br><br>fill.color|文本大小<br><br>fill.weight|
    |:--|:--|:--|
    |Closed<br><br>封路|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.79445911542890531458734576870247:50001231000000:2800:6510C97457D2022043DAAD424B46A1E6503819581CDC129FA64422663CDB96DD.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.96377177075200581369196349069068:50001231000000:2800:079841AF53AF9F7B9EC2C7427F12B20F0D10A134052D43B068398ED039059A3B.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.49896284962127456043188501808969:50001231000000:2800:C2059DBED037D2CE4516E9C1A88699934BB87D1C49F7F02DDC9A390A4CD58241.png)|
    
7. Transit
    
    |元素类型<br><br>Feature type|Geometry|   |   |   |Labels|   |   |   |Icon|
    |:--|:--|:--|:--|:--|:--|:--|:--|:--|:--|
    |填充颜色<br><br>fill.<br><br>color|填充宽度<br><br>fill.<br><br>weight|描边颜色<br><br>stroke.<br><br>color|描边宽度<br><br>stroke.weight|填充颜色<br><br>fill.<br><br>color|文本大小<br><br>fill.<br><br>weight|描边颜色<br><br>stroke.<br><br>color|描边大小<br><br>stroke.weight|图标类型<br><br>icon-type|
    |:--|:--|:--|:--|:--|:--|:--|:--|:--|
    |Airport<br><br>机场|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.56882968393189044210422885161717:50001231000000:2800:88771FA8F1EAB44D2F9DB3BB522F63F45D5537F2884AA6420EFF1DB3F066D382.png)|-|-|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.15314365326134280737632103837925:50001231000000:2800:E5E1CCE6288732B96D071B4C1D2BCFA1C5FD329F11537B6DA80DED2A7F0154AA.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.59546681833204068251810770566491:50001231000000:2800:6EB2D0A02897C07133C068310AAACA40D8DDF8B735DDC8B034E399FAAB64A0D8.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.97972358338346068269451885550643:50001231000000:2800:0E49D912733E16B980187B1BBF95849F8E27EC2A3445D25CF0470DD19A8CCF99.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163722.88214840564936167387775235844048:50001231000000:2800:6FFC218ADE6A0F9914F1D567B099B4F422FDCEF8FD89B1EED5B8C969A08CE02E.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.80489862923162331874215685873415:50001231000000:2800:4289CD62C00BF6BFBD360E808D17A8847BB29A22743160E854036C42BD165C80.png)|
    |Airport Runway<br><br>机场跑道|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.79870847311413117641234567687239:50001231000000:2800:7740CE5B3A035F6722BD02A53B7AA65931C23BCEC090E65CA9A85C81981BA3AA.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.55890660357731855479778510484811:50001231000000:2800:1725C623F5FDE65F294B2A0125D1DE854EB05A77D05F78194113CB74A7B6E379.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.82386802877046330457491243161715:50001231000000:2800:5551926500D2BE14ED252463F842F5D38BC7526C014A819322AA41CED980F774.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.34529573943677058524924308217819:50001231000000:2800:111593A15875BBC17115FE0B982FFE8661C3CBC8009D22A86FC0E8F043C8A115.png)||||||
    |Airport Runway Taxiway<br><br>机场跑道滑行道|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.34884282646090113619188006367455:50001231000000:2800:8177A8BF0F69443E30C4C3187B79D02430C082190ABD4442B6BCDA1D63467231.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.15982545494965141866847409212163:50001231000000:2800:ECA58259B748196F38244D9CAD99F5BFDA3CA0C75EC7891E626CBCFA792AAB59.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.33130776537059764513409028335114:50001231000000:2800:117FC58DB59C28BE83F1FCA9D3B04958CFF466FAE23A96FD135781BE89775627.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.40155218945423502420123557614551:50001231000000:2800:902485663B674E47DC01486E1EBF486FB5EB967D8F4F0E271A687D7C21EEAF1B.png)||||||
    |Bus<br><br>公交|-|-|-|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.80341714316418126853547793534373:50001231000000:2800:0D1222C260EF583453ED922F2E2BF8EE689AC8E50598C031D1236D5BAE034A1A.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.67090502329430878679808820832850:50001231000000:2800:26BB464DE170F0B243413AB30A0CFD5CA71FE0A9D1F0FEE6C7AD74DA52DDE7DD.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.11109979602257273170011476677014:50001231000000:2800:50718E8294CDCA0124AAF4875A334433805081726CBFCBAC6D995AF37B1E6781.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.51857066094085317269782230298233:50001231000000:2800:F9B4DA6CA9B7FA8054BD9DD0B020081D08D3FF062A1ACFCAEF61E4F2D67254B1.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.42364802518487665189995432609496:50001231000000:2800:B6E634C209D657DBC0F11B6755DB5290D9E3849F2BDAF14E3A81732DB4F99761.png)|
    |Ferry-line<br><br>航线|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.10527777374802596690627054228664:50001231000000:2800:794FB95B9D4BBB9A1BE9A39614FCE4C047AF56AE588D520D5D82042EE99577AE.png)|-|-|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163723.58551852915515556050667512278195:50001231000000:2800:2F86A39E1AA38936F8DC68DB835EB09383CF8A93DBE042A66C4666E65F67DAEF.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.54324121690674865889254256550626:50001231000000:2800:9FCC3A862CD374170A2978732C9DE365D44F00871543F8FC85A763490AAC901B.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.89601445439725880492992501617064:50001231000000:2800:349A87990E93D96D8018E287FEDABB73B9C63BE215401549EF1B099B46D46081.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.89492258083032413017667108520958:50001231000000:2800:54A37C57C9DB0CD010B27DF8B2EFFBB3CE8BB2176DE3F41C0AEF3D994430B029.png)|-|
    |Ferry-terminal<br><br>港口|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.47736602327751977960155978459084:50001231000000:2800:E6AA89119D39E8037F47E657F4B710FB5D056051B83C65A6BC5DAA25313BD476.png)|-|-|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.37806153850313398534945272494299:50001231000000:2800:C4F417C31D8DF9CA890126F9D0823E1C3AFEC0D28FF8800270B96B14C85878DD.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.34907531006582265194682639111667:50001231000000:2800:931349E2EA62FA16D799BFEC10B3A8B701A4C96C0FF4AB2479DAD0AFDCF9FCA6.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.22748147551474932234189706617617:50001231000000:2800:356CF80DF11B5B40CD0B90CDF259FB21EBC80CA02E932C4205808D3CDBBF68B3.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.73516544744148644528128304340501:50001231000000:2800:E713A6BF6379D304AE932EBA77730B6B6FE370C59AC24FCA33FDFA1278333A01.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.01726098758627218435877451321887:50001231000000:2800:47278C426DCBEC8DA962D49B1612ED1486807847F0CF48287C6BD3564E606F52.png)|
    |Other<br><br>出租车、<br><br>出入口等|-|-|-|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.41029938342631181267824163749860:50001231000000:2800:899E4560AD205A16D66FC435D6883AD3BDAA2D7CD25164E2E37417A7B1FB459E.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.61455985099554504445548505030258:50001231000000:2800:0A0E38E5B517B53FEEABE8F1A2C8D803981182DAEA7C8E99EBB48C492494B194.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163724.26178230064323634065942422769448:50001231000000:2800:93A3B797E0F6F791E4835FE5871A821B99539479B6AF7EABEB5932B03A246B90.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.98243274668997826024736999520600:50001231000000:2800:9FF2719C56786BF259D1D622FD18340EE227293EDBDCE46E8E1FE6DAADC684D3.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.37566064373786835851281115749098:50001231000000:2800:DB898FD89F0AEE9F91409207ACD653F8C2177ACEBF61BC28034C2E7939418F87.png)|
    |Rail-station<br><br>火车站、<br><br>高铁站|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.65231994798917209945723965694332:50001231000000:2800:E04356E01EC2FE629776950DE003749F3D9D17826E59EA2E06CBC86449E11508.png)|-|-|-|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.86174282622652475655280734600095:50001231000000:2800:367E8C8DDFB911F3F2C78D695F2AE9A985CC586C35B71B2C151CDCA5F2F7E76B.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.17750177197196729608441389564527:50001231000000:2800:F980D5AD3AF1F099E52A68F7F6F389EB9018418E0B81B6AC457A38C1B5D33A55.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.73425501660436181391251573313254:50001231000000:2800:3ABE121D87A0F58A7E03F15749FC90820F410C7FD0EE675367D408DC8A67A318.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.16874288946926820505387420495790:50001231000000:2800:197CCB0B96795E2337EE2D1BCB2E22F2B2E5F3798938F92C739CAB813A7CB338.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.57757746427507535879421013535233:50001231000000:2800:C35B38367C1867D8849E9146E2BCA92FCC9FEAE671FA17F9C0CA2896B150A829.png)|
    |Railway<br><br>铁路线、<br><br>高铁线|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.66428882249365013519321410745373:50001231000000:2800:7C6C06F40AFDFC56ADBF565D7FF54F6637A731BA8D1768F856D83EDCD3F3BFF9.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.33057834320510052135864152442645:50001231000000:2800:CBA04E166178E162DDBE552A45ABDFC41D92E6DFC61EE84CB70EDA62BA7134FC.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.10763237874932519446992152601212:50001231000000:2800:A15979E9D42850246EE0EE16C5E38BB4C9587F0F8F958B58DF7F3EBB852F0CD7.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.60466413299815857594431759999880:50001231000000:2800:2596D7CACC7FF78783056F08731FEC4844A84979C590E8F1D68B841A413D5FF8.png)|-|-|-|-|-|
    |Subway<br><br>地铁|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.43069737462771675561741348757781:50001231000000:2800:B3B4B44AD145D169598E93A2CD6338DE4CB982DAFE8EAF2A934EC7C7D59FC427.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.45936638098830876411804718737259:50001231000000:2800:921CD36C22795730AD568A71E8B0E0F26FAFE70033166CD8609505C7791A326E.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.39426733568336153513092477994286:50001231000000:2800:C758999637015AD19BD5515E65BB0A186F2BA06BA42208E241BD9ADAD5DF2CC7.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.48292567873231559338919495516421:50001231000000:2800:97A5AA588DDFF81B9BD86F99E3A075573F4D7E1B2E89B5383B7905985EBEDDC6.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.24345842067327337989126190112280:50001231000000:2800:06CB88517A189F8599406EDA2937E016A10E389BC965E00D303284BBC2927BFF.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.07868562086771424619148910005638:50001231000000:2800:16A2B657DEC1B00A032A5A0F879A9410564813E871D30B91719B36DDFE4602AF.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163725.44477426399586599082790569440132:50001231000000:2800:47955B82BA401A47FF2DED1A231D55533585731CE48F387141E4069D93F6B0E1.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.25443701970185998416797164511982:50001231000000:2800:6A3B0D9125C6008A264B5DA09FB7AEFDCB6B521FE27E14753CAB8FD21AB04879.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.73381553236569952938502998238803:50001231000000:2800:52337C97B3C6CAC04D84418A2111199B309B3A1C1DD9B95E154E1FB81FA32A54.png)|
    |Traffic_light<br><br>交通灯|||||||||![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.46124118726363684305655030081287:50001231000000:2800:0A611FF5547AD3FDAFDECAE279006FA1673092FCBDBD8E84DDCAB461F064FD0F.png)|
    
8. Water
    
    |元素类型<br><br>Feature type|Geometry|Labels|   |
    |:--|:--|:--|:--|
    |填充颜色<br><br>fill.color|填充颜色<br><br>fill.color|文本大小<br><br>fill.weight|
    |:--|:--|:--|
    |Ocean<br><br>水系、海洋、湖泊、河流|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.96159574210927461357984485659247:50001231000000:2800:A4A0DCD12BEEDF18BB43F0AB490A94D18F1FC5E9A1B9D51F2B6BA5E5B7FAE4A1.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.06494236956928041988575519014966:50001231000000:2800:DC996E584896C24A80045D32E74E869DA6625380E1BA639B8C7CA2C4E896967A.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.19653474818617231806332110385889:50001231000000:2800:9D57DA1DF1367F41CDF32A3C6251DB58CCFEC678015ABE698B42A2673C90709A.png)|
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-location "显示我的位置")


# 手势交互

更新时间: 2025-12-16 16:36

## 场景介绍

本章节将向您介绍如何使用地图的手势。

Map Kit提供了多种手势供用户与地图之间进行交互，如缩放、滚动、旋转和倾斜。这些手势默认开启，如果想要关闭某些手势，可以通过[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)类提供的接口来控制手势的开关。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163649.42367527239413132826206001659071:50001231000000:2800:E13B2F04F23C26347AB89ACF1CB742DF7D5B8701F65B6E054E42C4829531A3B1.png "点击放大")

## 接口说明

以下是地图手势相关接口，该功能有2种实现方式：

- 地图初始化时，可在初始化参数[MapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section816451553012)中设置是否启用手势功能，详细讲解见[显示地图](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-presenting)章节。
- 通过调用[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)提供的set方法实现相关手势的开启或关闭。

|接口名|描述|
|:--|:--|
|[setZoomGesturesEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1151381081514)(enabled: boolean): void|设置是否启用缩放手势。<br><br>默认值为true。|
|[setScrollGesturesEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section31711513156)(enabled: boolean): void|设置是否启用滚动手势。<br><br>默认值为true。|
|[setRotateGesturesEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section299655171811)(enabled: boolean): void|设置是否启用旋转手势。<br><br>默认值为true。|
|[setTiltGesturesEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section183712595910)(enabled: boolean): void|设置是否启用倾斜手势。<br><br>默认值为true。|
|[setAllGesturesEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1965712771211)(enabled: boolean): void|设置手势是否可用。<br><br>默认值为true。|

## 开发步骤

mapController对象在初始化地图时获取，初始化地图功能在[显示地图](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-presenting)章节中有详细讲解。

### 地图手势控制

您可以通过mapController对象来启用或禁止相关的地图手势。

**缩放手势：**

用户可以通过用双指张合，实现放大缩小地图。

1. this.mapController.setZoomGesturesEnabled(true);

**滚动平移手势：**

用户可以通过用手指拖动地图来进行移动。

1. this.mapController.setScrollGesturesEnabled(true);

**旋转手势：**

用户可以通过将两个手指放在地图上旋转来旋转地图。

1. this.mapController.setRotateGesturesEnabled(true);

**倾斜手势：**

用户可以通过将两个手指放在地图上下滑动来倾斜地图。

1. this.mapController.setTiltGesturesEnabled(true);

**启用或禁止所有手势：**

通过调用[setAllGesturesEnabled](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1965712771211)方法，可启用或禁止所有手势。

1. // 禁止所有手势
2. this.mapController.setAllGesturesEnabled(false);

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-controls-and-interaction "控件交互")
# 事件交互

更新时间: 2025-12-16 16:37

本章节包含地图的点击和长按、相机移动（华为地图的移动是通过模拟相机移动的方式实现的）、以及“我的位置”按钮点击等事件监听。

## 接口说明

以下是地图监听事件相关接口，以下功能主要由[MapEventManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager)提供，可通过[getEventManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section154601059144812)方法获得[MapEventManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager)，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager)。

|接口名|描述|
|:--|:--|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section824544714394)(type: 'mapClick', callback: Callback<[mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810)>): void|设置地图点击事件监听器。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section0257247133915)(type: 'mapLongClick', callback: Callback<[mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810)>): void|设置地图长按事件监听器。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section6240147113918)(type: 'cameraMoveStart', callback: Callback<number>): void|设置相机开始移动事件监听器。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section142347477396)(type: 'cameraMove', callback: Callback<void>): void|设置相机移动事件监听器。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section1963201310319)(type: 'cameraIdle', callback: Callback<void>): void|设置相机移动结束事件监听器。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section19286104716392)(type: 'markerClick' , callback: Callback<[Marker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker)>): void|设置标记点击事件监听器。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section9264124723916)(type: 'myLocationButtonClick', callback: Callback<void>): void|设置我的位置按钮点击事件监听器。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section636111479397)(type: 'pointAnnotationClick', callback: Callback<[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)>): void|设置点注释点击事件监听器。|

## 开发步骤

### 初始化地图组件的事件管理接口

1. this.mapEventManager = this.mapController.getEventManager();

### 地图点击事件监听

1. let callback = (position: mapCommon.LatLng) => {
2.   console.info("mapClick", `on-mapClick position = ${position.longitude}`);
3. };
4. this.mapEventManager.on("mapClick", callback);

### 地图长按事件监听

1. let callback = (position: mapCommon.LatLng) => {
2.   console.info("mapLongClick", `on-mapLongClick position = ${position.longitude}`);
3. };
4. this.mapEventManager.on("mapLongClick", callback);

### 相机移动监听

相机移动时（华为地图的移动是通过模拟相机移动的方式实现的），通过设置监听器，能够对相机移动状态进行监听。

- 当相机开始移动时，会回调cameraMoveStart。

1. let callback = (reason: number) => {
2.   console.info("cameraMoveStart", `on-cameraMoveStart reason = ${reason}`);
3. };
4. this.mapEventManager.on("cameraMoveStart", callback);

- 当相机移动或用户与触摸屏交互时，会多次调用cameraMove。

1. let callback = () => {
2.   console.info("cameraMove", `on-cameraMove`);
3. };
4. this.mapEventManager.on("cameraMove", callback);

- 当相机停止移动时，会回调cameraIdle。

1. let callback = () => {
2.   console.info("cameraIdle", `on-cameraIdle`);
3. };
4. this.mapEventManager.on("cameraIdle", callback);

### 标记点击事件监听

标记是指在地图的指定位置添加标记以标识位置、商家、建筑等。详情请参见[标记](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-marker)。

1. let callback = (marker: map.Marker) => {
2.   console.info("markerClick", `markerClick: ${marker.getId()}`);
3. };
4. this.mapEventManager.on("markerClick", callback);

### 我的位置监听

详情请参见[显示我的位置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-location)。

1. let callback = () => {
2.   console.info("myLocationButtonClick", `myLocationButtonClick`);
3. };
4. this.mapEventManager.on("myLocationButtonClick", callback);

### 点注释事件监听

点注释是指在地图的指定位置添加点注释以标识位置、商家、建筑等，并可以通过信息窗口展示详细信息。详情请参见[点注释](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-annotation)。

1. let callback = (pointAnnotation: map.PointAnnotation) => {
2.   console.info("pointAnnotationClick", `pointAnnotationClick: ${pointAnnotation.getId()}`);
3. };
4. this.mapEventManager.on("pointAnnotationClick", callback);

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-controls-and-gestures "手势交互")
# 更改地图位置

更新时间: 2025-12-16 16:37

## 场景介绍

华为地图的移动是通过模拟相机移动的方式实现的，该相机可称为地图相机，您可以通过改变地图相机位置，来控制地图的可见区域，效果如图所示。

本章节将向您介绍地图相机的各个属性与含义，并移动相机。

|   |   |
|---|---|
|**图1** 相机移动前  <br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.28738240256011213275641444552697:50001231000000:2800:006668146D5F9D1E5C6CF752657BEF2CBBF98F78F462261D881091D75855C6BA.png "点击放大")|**图2** 相机移动后  <br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.29289510214371409958672700758720:50001231000000:2800:41B03C81450EB56639A449BA85E22D6FC005F164ADA77C84342BCC86F65D6703.png "点击放大")|

## 接口说明

您可以通过[map](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map)命名空间下的[moveCamera](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section141021341974)方法、[animateCamera](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section6163175355113)方法和[animateCameraStatus](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section972910185717)实现移动地图相机。方法入参[CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)可通过以下方法创建。

|接口名|描述|
|:--|:--|
|[zoomTo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-zoomto)(zoom: number): [CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)|设置地图缩放级别。|
|[zoomOut](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-zoomout)(): [CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)|缩小地图缩放级别，在当前地图显示的级别基础上减1。|
|[zoomIn](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-zoomin)(): [CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)|放大地图缩放级别，在当前地图显示的级别基础上加1。|
|[zoomBy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-zoomby)(amount: number, focus?: [mapCommon.MapPoint](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section123881566186)): [CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)|根据给定增量并以给定的屏幕像素点为中心点缩放地图级别。|
|[scrollBy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-scrollby)(x: number, y: number): [CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)|按像素移动地图中心点。|
|[newLatLngBounds](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-newlatlngbounds-1)(bounds: [mapCommon.LatLngBounds](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section96341159111320), padding?: number): [CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)|设置地图经纬度范围、设置地图区域和边界之间的距离。|
|[newLatLngBounds](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-newlatlngbounds-2)(bounds: [mapCommon.LatLngBounds](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section96341159111320), width: number, height: number, padding: number): [CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)|设置地图经纬度范围、设置经纬度矩形范围的高和宽、设置地图区域和边界之间的距离。|
|[newLatLngBounds](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-newlatlngbounds-3)(bounds: [mapCommon.LatLngBounds](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section96341159111320), padding: [mapCommon.Padding](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section144591344648)): [CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)|支持设置地图经纬度范围和4个方向与边界之间的距离。|
|[newLatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-newlatlng)(latLng: [mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810), zoom?: number): [CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)|设置地图的中心点和缩放层级。|
|[newCameraPosition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-newcameraposition)(cameraPosition: [mapCommon.CameraPosition](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section105031244194712)): [CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)|更新地图状态。|

## 开发步骤

### 相机移动

1. 初始化地图并获取[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)地图操作类对象。[显示地图](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-presenting)章节中有详细讲解。
2. 导入模块。
    
    1. import { MapComponent, mapCommon, map } from '@kit.MapKit';
    
3. 通过调用[MapComponentController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller)的[moveCamera](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section141021341974)方法、[animateCamera](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section6163175355113)方法和[animateCameraStatus](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section972910185717)方法，可实现移动地图相机。
    
    您可以选择以动画方式或非动画方式移动相机。
    
    - 动画方式移动相机时，您可以设置动画持续的时间。
    - 非动画方式移动相机是瞬时完成的。
    
    1. // 创建CameraUpdate对象
    2. let cameraPosition: mapCommon.CameraPosition = {
    3.   target: {
    4.     latitude: 32.0,
    5.     longitude: 118.0
    6.   },
    7.   zoom: 10,
    8.   tilt: 0,
    9.   bearing: 0
    10. };
    11. let cameraUpdate = map.newCameraPosition(cameraPosition);
    12. // 以非动画方式移动地图相机
    13. this.mapController.moveCamera(cameraUpdate);
    
    14. // 以动画方式移动地图相机
    15. this.mapController.animateCamera(cameraUpdate, 1000);
    
    16. // 以动画方式移动地图相机，并返回动画结果
    17. let animateResult = await this.mapController.animateCameraStatus(cameraUpdate, 1000);
    
    |   |   |
    |---|---|
    |**图3** 相机移动前<br><br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.53880620373376553173367091603198:50001231000000:2800:E15D78AAEF67BFB8B5CF4F4D8C47AD173CA3769E73159C1026C24C2557359F06.jpg "点击放大")|**图4** 相机移动后<br><br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.26316560775962278443885320848347:50001231000000:2800:C6D048D22BA487588BE824D25C4ED8294C4D9DF76ED2800F063A2AE8BB9E175B.jpg "点击放大")|
    
4. 您还可以通过以下方式创建[CameraUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-cameraupdate)对象。
    
    1. // 方式1：相机放大级数加1，保持其他属性不变
    2. let cameraUpdate = map.zoomIn();
    
    3. // 方式2：相机放大级数减1，保持其他属性不变
    4. let cameraUpdate1 = map.zoomOut();
    
    5. // 方式3：指定相机缩放级数zoom值，其他属性不变
    6. let zoom1 = 8.0;
    7. let cameraUpdate2 = map.zoomTo(zoom1);
    
    8. // 方式4：
    9. // a、指定相机缩放级别增量amount，您调用此方法可以在原来相机的缩放级别之上，进行适当的缩放
    10. // b、指定缩放级别增量和一个中心点，您调用此API可以移动相机至中心点位置，并进行缩放
    11. // 以屏幕左顶点为（0, 0）点，positionX正值代表可视区域向右移动，负值代表可视区域向左移动
    12. // positionY正值代表可视区域向下移动，负值代表可视区域向上移动
    13. let point: mapCommon.MapPoint = {
    14.   positionX: 31,
    15.   positionY: 118
    16. };
    17. let amount = 2.0;
    18. let cameraUpdate3 = map.zoomBy(amount, point);
    
    19. // 方式5：设置相机的经纬度和地图层级
    20. // a、仅指定相机的经纬度，实现中心点的移动
    21. // b、指定相机的经纬度和地图层级，您调用此API可以移动相机至中心点位置，并进行缩放
    22. let latLng: mapCommon.LatLng = {
    23.   latitude: 31.5,
    24.   longitude: 118.9
    25. };
    26. let zoom2 = 10;
    27. let cameraUpdate4 = map.newLatLng(latLng, zoom2);
    
    28. // 方式6：设置相机的可见区域
    29. let latLngBounds: mapCommon.LatLngBounds = {
    30.   northeast: {
    31.     latitude: 32.5,
    32.     longitude: 119.9
    33.   },
    34.   southwest: {
    35.     latitude: 31.5,
    36.     longitude: 118.9
    37.   }
    38. };
    39. // 设置地图显示经纬度范围，设置地图区域和边界之间的距离为5像素
    40. let cameraUpdate5 = map.newLatLngBounds(latLngBounds, 5);
    41. // 方式7：设置相机的可见区域
    42. // 设置地图显示经纬度范围，设置经纬度矩形范围的宽为1000像素，设置经纬度矩形范围的高为1000像素，设置地图区域和边界之间的距离为100像素
    43. let cameraUpdate6 = map.newLatLngBounds(latLngBounds, 1000, 1000, 100);
    44. // 方式8：设置地图显示经纬度范围，设置地图区域和4个方向的边界之间的距离分别为5、6、7、8像素
    45. let paddings: mapCommon.Padding = {
    46.   left:5,
    47.   top: 6,
    48.   right: 7,
    49.   bottom: 8
    50. };
    51. let cameraUpdate7 = map.newLatLngBounds(latLngBounds, paddings);
    
    52. // 方式9：滚动相机，将相机按照指定的像素点移动
    53. let x = 100.0;
    54. let y = 100.0;
    55. let cameraUpdate8 = map.scrollBy(x, y);
    

### 设置相机最大/最小偏好缩放级别

1. // 设置最小偏好缩放级别，范围为[2, 20] 
2. this.mapController.setMinZoom(6); 
3. // 设置最大偏好缩放级别，范围为[2, 20] 
4. this.mapController.setMaxZoom(14);

### 设置地图相机的边界

Map Kit支持设置地图相机的边界。通过[setLatLngBounds](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section14990184514712)接口指定一个[LatLngBounds](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section96341159111320)来约束相机目标，使用户移动地图时，相机目标不会移出此边界。当设置参数为空时，地图相机的边界清除。

1. let bounds: mapCommon.LatLngBounds = {
2.   northeast: {
3.     latitude: 31,
4.     longitude: 118
5.   },
6.   southwest: {
7.     latitude: 30,
8.     longitude: 113
9.   }
10. };
11. this.mapController.setLatLngBounds(bounds);

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-listening "事件交互")
# 地图截图

更新时间: 2025-12-16 16:37

本章节将向您介绍如何实现地图截图功能。

地图截图指对当前屏幕显示区域进行截屏，支持对地图、覆盖物、Logo进行屏幕截图。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163731.80992960431072925500584359966006:50001231000000:2800:C749C9350C3746E7C5360E2F3CF7F479CEDDD8374C73A3D185410CC0E8964F7B.png)

## 接口说明

以下是地图截图相关接口，以下功能主要由[snapshot](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section4803202315197)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section4803202315197)。

|接口名|描述|
|:--|:--|
|[snapshot](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section4803202315197)(): Promise<[image.PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)>|地图截图。|

## 开发步骤

1. 导入相关模块。
    
    1. import { MapComponent, mapCommon, map } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    3. import { image } from '@kit.ImageKit';
    
2. 调用[snapshot](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section4803202315197)方法对当前屏幕进行截图。
    
    1. @Entry
    2. @Component
    3. struct HuaweiMapDemo {
    4.   private mapOptions?: mapCommon.MapOptions;
    5.   private callback?: AsyncCallback<map.MapComponentController>;
    6.   private mapController?: map.MapComponentController;
    7.   @State image?: image.PixelMap = undefined;
    
    8.   aboutToAppear(): void {
    9.     // 地图初始化参数，设置地图中心点坐标及层级
    10.     this.mapOptions = {
    11.       position: {
    12.         target: {
    13.           latitude: 39.9,
    14.           longitude: 116.4
    15.         },
    16.         zoom: 10
    17.       }
    18.     };
    
    19.     // 地图初始化的回调
    20.     this.callback = async (err, mapController) => {
    21.       if (!err) {
    22.         // 获取地图的控制器类，用来操作地图
    23.         this.mapController = mapController;
    24.       } else {
    25.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    26.       }
    27.     };
    28.   }
    
    29.   build() {
    30.     Stack() {
    31.       Column() {
    32.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback })
    33.           .width('100%')
    34.           .height('50%');
    
    35.         Scroll(new Scroller()) {
    36.           Column() {
    37.             Image(this.image)
    38.               .objectFit(ImageFit.Auto)
    39.               .border({ width: 1, color: Color.Red }).width("100%")
    40.             Button("获取截图")
    41.               .margin({ left: 10 })
    42.               .fontSize(12)
    43.               .onClick(async () => {
    44.                 if (this.mapController) {
    45.                   let pixelMap = await this.mapController.snapshot();
    46.                   this.image = pixelMap;
    47.                 }
    48.               });
    49.           }
    50.         }.width('70%').height("50%")
    51.       }.width('100%')
    52.     }.height('100%')
    53.   }
    54. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-camera "更改地图位置")
# 标记

更新时间: 2025-12-16 16:36

## 场景介绍

从5.1.1(19)开始，支持控制Marker文字显隐功能；从6.0.0(20)开始，支持自定义组件实现marker图标功能。

本章节将向您介绍如何在地图的指定位置添加标记以标识位置、商家、建筑等。

点标记用来在地图上标记任何位置，例如用户位置、车辆位置、店铺位置等一切带有位置属性的事物。Map Kit提供的点标记功能（又称 Marker）封装了大量的触发事件，例如点击事件、长按事件、拖拽事件。

Marker有默认风格，同时也支持自定义。由于内容丰富，以下只能展示一些基础功能的使用。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163635.27026253038140647821741690719977:50001231000000:2800:D907065A12DD6F92DA05878673ABA3829BC5817ECBCEA8473D2AC6A81A395151.png "点击放大")

## 接口说明

添加标记功能主要由[MarkerOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section559041743210)、[addMarker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section0810361284)和[Marker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker)。

|接口名|描述|
|:--|:--|
|[MarkerOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section559041743210)|标记参数。|
|[addMarker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section0810361284)(options: [mapCommon.MarkerOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section559041743210)): Promise<[Marker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker)>|在地图上添加标记。|
|[Marker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker)|标记，支持更新和查询相关属性。|

## 开发步骤

### 添加标记

1. 导入相关模块。
    
    1. import { MapComponent, mapCommon, map } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 添加标记，在callback方法中创建初始化参数并新建[Marker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker)。
    
    1. @Entry
    2. @Component
    3. struct MarkerDemo {
    4.   private mapOptions?: mapCommon.MapOptions;
    5.   private mapController?: map.MapComponentController;
    6.   private callback?: AsyncCallback<map.MapComponentController>;
    7.   private mapEventManager?: map.MapEventManager;
    8.   private marker?: map.Marker;
    
    9.   aboutToAppear(): void {
    10.     // 地图初始化参数
    11.     this.mapOptions = {
    12.       position: {
    13.         target: {
    14.           latitude: 31.984410259206815,
    15.           longitude: 118.76625379397866
    16.         },
    17.         zoom: 15
    18.       }
    19.     };
    20.     this.callback = async (err, mapController) => {
    21.       if (!err) {
    22.         this.mapController = mapController;
    23.         this.mapEventManager = this.mapController.getEventManager();
    24.         // Marker初始化参数
    25.         let markerOptions: mapCommon.MarkerOptions = {
    26.           position: {
    27.             latitude: 31.984410259206815,
    28.             longitude: 118.76625379397866
    29.           },
    30.           rotation: 0,
    31.           visible: true,
    32.           zIndex: 0,
    33.           alpha: 1,
    34.           anchorU: 0.5,
    35.           anchorV: 1,
    36.           clickable: true,
    37.           draggable: true,
    38.           flat: false
    39.         };
    40.         // 创建Marker
    41.         try {
    42.           this.marker = await this.mapController.addMarker(markerOptions);
    43.         } catch (e) {
    44.           console.error(`Failed to create the marker, code is：${e.code}, message is ${e.message}`);
    45.         }
    46.       } else {
    47.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    48.       }
    49.     };
    50.   }
    
    51.   build() {
    52.     Stack() {
    53.       Column() {
    54.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback });
    55.       }.width('100%')
    56.     }.height('100%')
    57.   }
    58. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163635.37856330096752789591946418423990:50001231000000:2800:02618C8DE668325B7B86FC9B7D203C2409374820B237777C53F773DADCF76882.png "点击放大")
    
3. 在添加标记之后，修改已经设置的标记属性。
    
    1. // 设置标记可拖拽
    2. this.marker.setDraggable(true);
    3. // 设置标记锚点
    4. this.marker.setMarkerAnchor(1.0, 1.0);
    

### 自定义标记

通过在[MarkerOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section559041743210)中将icon属性设置为自定义图标的资源，可将默认标记图标修改成自定义图标。

1. let markerOptions: mapCommon.MarkerOptions = {
2.   position: {
3.     latitude: 31.984410259206815,
4.     longitude: 118.76625379397866
5.   },
6.   rotation: 0,
7.   visible: true,
8.   zIndex: 0,
9.   alpha: 1,
10.   anchorU: 0.5,
11.   anchorV: 1,
12.   clickable: true,
13.   draggable: true,
14.   flat: false,
15.   // 图标存放在resources/rawfile，icon参数传入rawfile文件夹下的相对路径
16.   icon: 'test.png'
17. };
18. this.marker = await this.mapController.addMarker(markerOptions);

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163635.78310337407126483315041274688656:50001231000000:2800:6DD17A2AFDACC8E9934D8DA5068C30C4EF94EC9E18B7F21F6D2D674F312358E1.png "点击放大")

### 控制Marker文字显隐

通过[setAnnotationVisible](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker#section6403556152318)方法可以控制Marker文字显隐，还可以通过[isAnnotationVisible](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker#section7880311173111)方法来获取Marker文字显隐的状态。

1. // Marker初始化参数
2. let markerOptions: mapCommon.MarkerOptions = {
3.   position: {
4.     latitude: 31.984410259206815,
5.     longitude: 118.76625379397866
6.   },
7.   rotation: 0,
8.   visible: true,
9.   zIndex: 0,
10.   alpha: 1,
11.   anchorU: 0.5,
12.   anchorV: 1,
13.   clickable: true,
14.   draggable: true,
15.   flat: false,
16.   annotations: [{
17.     // 定义标题内容
18.     content: "text",
19.     fontStyle: 1,
20.     strokeWidth: 3,
21.     fontSize: 15
22.   }]
23. };
24. // 创建Marker
25. this.marker = await this.mapController.addMarker(markerOptions);
26. // 设置文字隐藏
27. this.marker.setAnnotationVisible(false);
28. // 查询当前显隐状态
29. let isAnnotationVisible: boolean = this.marker.isAnnotationVisible();
30. console.info(`isAnnotationVisible is: ` + isAnnotationVisible);

|   |   |
|---|---|
|**图1** 隐藏Marker文字之前|**图2** 隐藏Marker文字之后|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163635.44379892995861225395755740548342:50001231000000:2800:9B0B08B3B58290587EDB88E2E4072C47A450B7B675EF94B1EBBD375F1CC995D0.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163635.36407988393153363679958712019797:50001231000000:2800:290EA196CB640F52677E84CF8931CE142A73967DBEFCA03D2C8C7037C3E6B2AD.png)|

### 碰撞检测

通过在[MarkerOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section559041743210)中设置collisionRule属性，可以设置标记的冲突处理规则。

1. let markerOptions: mapCommon.MarkerOptions = {
2.   position: {
3.     latitude: 31.984410259206815,
4.     longitude: 118.76625379397866
5.   },
6.   rotation: 0,
7.   visible: true,
8.   zIndex: 0,
9.   alpha: 1,
10.   anchorU: 0.5,
11.   anchorV: 1,
12.   clickable: true,
13.   draggable: true,
14.   flat: false,
15.   // 图标存放在resources/rawfile，icon参数传入rawfile文件夹下的相对路径
16.   icon: 'icon.png',
17.   annotations:  [{
18.     // 定义标题内容
19.     content: "Test",
20.     fontStyle: 1,
21.     strokeWidth: 3,
22.     fontSize: 15
23.   }],
24.   // 设置碰撞规则为图标和名称都参与碰撞
25.   collisionRule: mapCommon.CollisionRule.ALL,
26.   annotationPosition: mapCommon.TextPosition.TOP
27. };
28. this.marker = await this.mapController.addMarker(markerOptions);

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163635.95868333666649513286437375120619:50001231000000:2800:54FA25B10797520BFDF97B37110C4AE8E80951BE70E4508D95B0A7A7F8D26EA6.gif "点击放大")

### 设置监听标记点击事件

1. let callback = (marker: map.Marker) => {
2.   console.info(`on-markerClick marker = ${marker.getId()}`);
3. };
4. this.mapEventManager.on("markerClick", callback);

### 设置监听标记拖动事件

通过如下步骤设置监听标记拖动事件：

1. 将[Marker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker)的拖拽属性设置为true。
2. 调用[on(type: 'markerDragStart' , callback: Callback<Marker>)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section88711444165714)方法监听标记是否开始拖拽。
3. 调用[on(type: 'markerDrag' , callback: Callback<Marker>)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section486516467570)，监听标记拖动过程。
4. 调用[on(type: 'markerDragEnd' , callback: Callback<Marker>)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section288194865719)，监听标记拖动结束事件。

5. // 设置标记可拖拽
6. this.marker.setDraggable(true);

7. // 监听标记开始拖拽
8. let markerCallback = (marker: map.Marker) => {
9.   console.info(`on-markerDragStart marker = ${marker.getId()}`);
10. };
11. this.mapEventManager.on("markerDragStart", markerCallback);

12. // 监听标记拖拽事件
13. let markerDragCallback = (marker: map.Marker) => {
14.   console.info(`on-markerDrag marker = ${marker.getId()}`);
15. };
16. this.mapEventManager.on("markerDrag", markerDragCallback);

17. // 监听标记拖拽结束
18. let markerDragEndCallback = (marker: map.Marker) => {
19.   console.info(`on-markerDragEnd marker = ${marker.getId()}`);
20. };
21. this.mapEventManager.on("markerDragEnd", markerDragEndCallback);

### 信息窗

1. // 添加信息窗
2. let markerOptions: mapCommon.MarkerOptions = {
3.   position: {
4.     latitude: 31.984410259206815,
5.     longitude: 118.76625379397866
6.   }
7. };
8. this.marker = await this.mapController?.addMarker(markerOptions);
9. // 设置信息窗的标题
10. this.marker.setTitle('南京');
11. // 设置信息窗的子标题
12. this.marker.setSnippet('华东地区');
13. // 设置标记可点击
14. this.marker.setClickable(true);
15. // 设置信息窗的锚点位置
16. this.marker.setInfoWindowAnchor(1, 1);
17. // 设置信息窗可见，点击标记后可展示信息窗
18. this.marker.setInfoWindowVisible(true);

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163635.79617107507189861340723755325732:50001231000000:2800:DA604A55A43AACE0F46BF09AEFE59163325B6D9B70817688A1CCE87EAF9CC584.png "点击放大")

### 自定义信息窗

1. @Entry
2. @Component
3. struct MarkerDemo {
4.   private mapOptions?: mapCommon.MapOptions;
5.   private mapController?: map.MapComponentController;
6.   private callback?: AsyncCallback<map.MapComponentController>;

7.   aboutToAppear(): void {
8.     this.mapOptions = {
9.       position: {
10.         target: {
11.           latitude: 32.120750,
12.           longitude: 118.788765
13.         },
14.         zoom: 15
15.       }
16.     }

17.     this.callback = async (err, mapController) => {
18.       if (!err) {
19.         this.mapController = mapController;
20.         let markerOptions: mapCommon.MarkerOptions = {
21.           position: {
22.             latitude: 32.120750,
23.             longitude: 118.788765
24.           },
25.           clickable: true,
26.           // 设置信息窗标题，点击标记后可展示信息窗
27.           title: "自定义信息窗"
28.         };
29.         await this.mapController?.addMarker(markerOptions);
30.       } else {
31.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
32.       }
33.     }
34.   }

35.   build() {
36.     Stack() {
37.       Column() {
38.         MapComponent({
39.           mapOptions: this.mapOptions,
40.           mapCallback: this.callback,
41.           // 自定义信息窗
42.           customInfoWindow: this.customInfoWindow
43.         })
44.           .width('100%')
45.           .height('100%');
46.       }.width('100%')
47.     }.height('100%')
48.   }
49.   // 自定义信息窗BuilderParam
50.   @BuilderParam customInfoWindow: ($$: map.MarkerDelegate) => void = this.customInfoWindowBuilder;
51.   // 自定义信息窗Builder
52.   @Builder
53.   customInfoWindowBuilder($$: map.MarkerDelegate) {
54.     if ($$.marker) {
55.       Text($$.marker.getTitle())
56.         .width("50%")
57.         .height(50)
58.         .backgroundColor(Color.Green)
59.         .textAlign(TextAlign.Center)
60.         .fontColor(Color.Black)
61.         .font({ size: 25, weight: 10, style: FontStyle.Italic })
62.         .border({ width: 3, color: Color.Black, radius: 25, style: BorderStyle.Dashed })
63.     }
64.   }
65. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163635.46843059131844181428584457901735:50001231000000:2800:5BF813BF446DC8343FDA48BA3315237040A8EE830772DF43C7B213CC9AF83716.png "点击放大")

### 标记动画

Marker支持设置旋转、缩放、平移、透明、图片动画播放和组合动画效果。

|接口名|描述|
|:--|:--|
|[AlphaAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-alphaanimation)|控制透明度的动画类。|
|[RotateAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-rotateanimation)|控制旋转的动画类。|
|[ScaleAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-scaleanimation)|控制缩放的动画类。|
|[TranslateAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-translateanimation)|控制平移的动画类。|
|[PlayImageAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-playimageanimation)|控制多张图片的动画类。|
|[AnimationSet](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-animationset)|动画集合。|

旋转动画效果的示例代码如下：

1. import { map, mapCommon, MapComponent } from '@kit.MapKit';
2. import { AsyncCallback } from '@kit.BasicServicesKit';

3. @Entry
4. @Component
5. struct MarkerDemo {
6.   private mapOptions?: mapCommon.MapOptions;
7.   private callback?: AsyncCallback<map.MapComponentController>;

8.   aboutToAppear(): void {
9.     this.mapOptions = {
10.       position: {
11.         target: {
12.           latitude: 32.020750,
13.           longitude: 118.788765
14.         },
15.         zoom: 11
16.       }
17.     }

18.     this.callback = async (err, mapController) => {
19.       if (!err) {
20.         // 构造MarkerOptions对象
21.         let markerOptions: mapCommon.MarkerOptions = {
22.           position: {
23.             latitude: 32.020750,
24.             longitude: 118.788765
25.           }
26.         };
27.         // 新建marker
28.         let marker: map.Marker = await mapController.addMarker(markerOptions);
29.         // 构造RotateAnimation对象
30.         let animation = new map.RotateAnimation(0, 270);
31.         // 动画执行时间
32.         animation.setDuration(2000);

33.         // 动画结束状态
34.         animation.setFillMode(map.AnimationFillMode.BACKWARDS);

35.         // 动画重复模式
36.         animation.setRepeatMode(map.AnimationRepeatMode.REVERSE);

37.         // 动画重复次数
38.         animation.setRepeatCount(100);

39.         // 设置动画开始监听
40.         let callbackStart = () => {
41.           console.info("animationStart", `callback`);
42.         };
43.         animation.on("animationStart", callbackStart);

44.         // 设置动画结束监听
45.         let callbackEnd = () => {
46.           console.info("animationEnd", `callback`);
47.         };
48.         animation.on("animationEnd", callbackEnd);

49.         // 设置动画
50.         marker.setAnimation(animation);
51.         // 开启动画
52.         marker.startAnimation();
53.       } else {
54.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
55.       }
56.     }
57.   }

58.   build() {
59.     Stack() {
60.       Column() {
61.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback })
62.       }.width('100%')
63.     }.height('100%')
64.   }
65. }

展示效果如图：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163636.31210913176158243646939112895546:50001231000000:2800:2CA43EF39A8C63A10AF0C18EDA046A4E6C3DC2A0393DAFF2697F06B180D5DB4C.gif "点击放大")

### 图片动画播放

1. import { map, mapCommon, MapComponent } from '@kit.MapKit';
2. import { AsyncCallback } from '@kit.BasicServicesKit';
3. import { image } from '@kit.ImageKit';

4. @Entry
5. @Component
6. struct MarkerDemo {
7.   private mapOptions?: mapCommon.MapOptions;
8.   private callback?: AsyncCallback<map.MapComponentController>;

9.   aboutToAppear(): void {
10.     this.mapOptions = {
11.       position: {
12.         target: {
13.           latitude: 32.020750,
14.           longitude: 118.788765
15.         },
16.         zoom: 11
17.       }
18.     }

19.     this.callback = async (err, mapController) => {
20.       if (!err) {
21.         // 构造MarkerOptions对象
22.         let markerOptions: mapCommon.MarkerOptions = {
23.           position: {
24.             latitude: 32.020750,
25.             longitude: 118.788765
26.           },
27.         };
28.         let images: Array<ResourceStr | image.PixelMap> = [
29.           // 图标需存放在resources/rawfile目录下
30.           'icon/avocado.png',
31.           'icon/20231027.png',
32.           // 图标需存放在resources/base/media目录下
33.           $r('app.media.maps_blue_dot')
34.         ]
35.         let mContext = this.getUIContext().getHostContext();
36.         if (mContext) {
37.           const fileData: Uint8Array = await mContext?.resourceManager?.getRawFileContent('icon/icon.png');
38.           let imageSource: image.ImageSource =
39.             image.createImageSource(fileData.buffer.slice(0, fileData.buffer.byteLength));
40.           let pixelMap: PixelMap = await imageSource.createPixelMap();
41.           images.push(pixelMap);
42.         }
43.         // 新建marker
44.         let marker: map.Marker = await mapController.addMarker(markerOptions);
45.         // 构造PlayImageAnimation对象
46.         let animation: map.PlayImageAnimation = new map.PlayImageAnimation();
47.         // 添加图片
48.         await animation.addImages(images)
49.         // 动画执行时间
50.         animation.setDuration(3000);

51.         // 动画结束状态
52.         animation.setFillMode(map.AnimationFillMode.BACKWARDS);

53.         // 动画重复模式
54.         animation.setRepeatMode(map.AnimationRepeatMode.REVERSE);

55.         // 动画重复次数
56.         animation.setRepeatCount(100);

57.         // 设置动画开始监听
58.         let callbackStart = () => {
59.           console.info("animationStart", `callback`);
60.         };
61.         animation.on("animationStart", callbackStart);
62.         // 设置动画结束监听
63.         let callbackEnd = () => {
64.           console.info("animationEnd", `callback`);
65.         };
66.         animation.on("animationEnd", callbackEnd);
67.         // 设置动画
68.         marker.setAnimation(animation);
69.         // 开启动画
70.         marker.startAnimation();
71.       } else {
72.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
73.       }
74.     }
75.   }

76.   build() {
77.     Stack() {
78.       Column() {
79.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback })
80.       }.width('100%')
81.     }.height('100%')
82.   }
83. }

展示效果如图：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163636.13562826131966303795365777049409:50001231000000:2800:AC65CE5D57786FEBB6146E6D6C52E7BE4B613E439D6F50DE9C4F9159B87C9DE4.gif "点击放大")

### 自定义组件实现marker图标

通过自定义组件生成marker图标。

1. import { map, mapCommon, MapComponent } from '@kit.MapKit';
2. import { AsyncCallback } from '@kit.BasicServicesKit';

3. @Entry
4. @Component
5. struct MarkerDemo {
6.   private mapOption?: mapCommon.MapOptions;
7.   private mapController?: map.MapComponentController;
8.   private callback?: AsyncCallback<map.MapComponentController>;
9.   private marker?: map.Marker;
10.   aboutToAppear(): void {
11.     this.mapOption = {
12.       position: {
13.         target: {
14.           latitude: 32.120750,
15.           longitude: 118.788765
16.         },
17.         zoom: 14
18.       },
19.       scaleControlsEnabled: true
20.     }
21.     this.callback = async (err, mapController) => {
22.       if (!err) {
23.         this.mapController = mapController;
24.         // 构造MarkerOptions对象
25.         let markerOptions: mapCommon.MarkerOptions = {
26.           position: {
27.             latitude: 32.120750,
28.             longitude: 118.788765
29.           },
30.           // 自定义组件
31.           iconBuilder: () => {
32.             this.renderBuilder();
33.           }
34.         };
35.         this.marker = await this.mapController?.addMarker(markerOptions);
36.       }
37.     }
38.   }
39.   @Builder
40.   renderBuilder() {
41.     Stack({ alignContent: Alignment.Center }) {
42.       // 需要替换您自己的资源图片，存放在resources/base/media目录下
43.       Image($r('app.media.iconbuilder'))
44.         .syncLoad(true)
45.     }
46.     .height(50)
47.     .width(50)
48.   }

49.   build() {
50.     Stack() {
51.       Column() {
52.         MapComponent({ mapOptions: this.mapOption, mapCallback: this.callback })
53.           .width('100%')
54.           .height('100%');
55.       }.width('100%')
56.     }.height('100%')
57.   }
58. }

展示效果如图：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163636.05691893087815391216074136308185:50001231000000:2800:F105772AEAEF4979E3F32CEDE13DE9635B9B49678A57F96265FD8B39B0EC4F06.jpg "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-drawing "在地图上绘制")
# 弧线

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将向您介绍如何在地图上绘制弧线，通过[MapArcParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section943619551002)类设置弧线的位置、宽度、颜色等参数。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.82953408125200674400841715913517:50001231000000:2800:348EEF3D6916E8105B5F9319B6D31FAD965FF3BCA1D09944760AA598F44C23C6.png "点击放大")

## 接口说明

添加弧线功能主要由[MapArcParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section943619551002)、[addArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section123390488448)和[MapArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-maparc)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-maparc)。

|接口名|描述|
|:--|:--|
|[MapArcParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section943619551002)|弧线参数。|
|[addArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section123390488448)(params: [mapCommon.MapArcParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section943619551002)): [MapArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-maparc)|添加一条弧线。|
|[MapArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-maparc)|弧线，支持更新和查询相关属性。|

## 开发步骤

### 添加弧线

1. 导入相关模块。
    
    1. import { map, mapCommon, MapComponent } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 添加弧线，在callback方法中创建初始化参数并新建MapArc。
    
    1. @Entry
    2. @Component
    3. struct MapArcDemo {
    4.   private TAG = "OHMapSDK_MapArcDemo";
    5.   private mapOptions?: mapCommon.MapOptions;
    6.   private mapController?: map.MapComponentController;
    7.   private callback?: AsyncCallback<map.MapComponentController>;
    8.   private mapArc?: map.MapArc;
    
    9.   aboutToAppear(): void {
    10.     this.mapOptions = {
    11.       position: {
    12.         target: {
    13.           latitude: 34.757975,
    14.           longitude: 113.665412
    15.         },
    16.         zoom: 6
    17.       }
    18.     }
    
    19.     this.callback = async (err, mapController) => {
    20.       if (!err) {
    21.         this.mapController = mapController;
    22.         if (!this.mapController) {
    23.           console.error(this.TAG, "mapController is null");
    24.           return;
    25.         }
    26.         // 设置弧线参数
    27.         let mapArcParams: mapCommon.MapArcParams = {
    28.           // 弧线起点坐标
    29.           startPoint: {
    30.             latitude: 39.913138,
    31.             longitude: 116.415112
    32.           },
    33.           // 弧线终点坐标
    34.           endPoint: {
    35.             latitude: 28.239473,
    36.             longitude: 112.954094
    37.           },
    38.           // 弧线中心点坐标
    39.           centerPoint: {
    40.             latitude: 33.86970399048567,
    41.             longitude: 112.08633528544145
    42.           },
    43.           width: 10,
    44.           color: 0xffff0000,
    45.           visible: true,
    46.           zIndex: 100
    47.         };
    48.         // 添加弧线
    49.         try {
    50.           this.mapArc = await this.mapController.addArc(mapArcParams);
    51.         } catch (e) {
    52.           console.error(`Failed to create the mapArc, code is：${e.code}, message is ${e.message}`);
    53.         }
    54.       } else {
    55.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    56.       }
    57.     }
    58.   }
    
    59.   build() {
    60.     Stack() {
    61.       Column() {
    62.         MapComponent({
    63.           mapOptions: this.mapOptions,
    64.           mapCallback: this.callback
    65.         })
    66.           .width('100%')
    67.           .height('100%');
    68.       }.width('100%')
    69.     }.height('100%')
    70.   }
    71. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.57878551733187142412358201578568:50001231000000:2800:139BB1FD1AE105FAE6B395A68FAB3114599C56491F4E4061364D27AD6A3A6E61.png "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-polyline "折线")
# 弧线

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将向您介绍如何在地图上绘制弧线，通过[MapArcParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section943619551002)类设置弧线的位置、宽度、颜色等参数。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.82953408125200674400841715913517:50001231000000:2800:348EEF3D6916E8105B5F9319B6D31FAD965FF3BCA1D09944760AA598F44C23C6.png "点击放大")

## 接口说明

添加弧线功能主要由[MapArcParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section943619551002)、[addArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section123390488448)和[MapArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-maparc)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-maparc)。

|接口名|描述|
|:--|:--|
|[MapArcParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section943619551002)|弧线参数。|
|[addArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section123390488448)(params: [mapCommon.MapArcParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section943619551002)): [MapArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-maparc)|添加一条弧线。|
|[MapArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-maparc)|弧线，支持更新和查询相关属性。|

## 开发步骤

### 添加弧线

1. 导入相关模块。
    
    1. import { map, mapCommon, MapComponent } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 添加弧线，在callback方法中创建初始化参数并新建MapArc。
    
    1. @Entry
    2. @Component
    3. struct MapArcDemo {
    4.   private TAG = "OHMapSDK_MapArcDemo";
    5.   private mapOptions?: mapCommon.MapOptions;
    6.   private mapController?: map.MapComponentController;
    7.   private callback?: AsyncCallback<map.MapComponentController>;
    8.   private mapArc?: map.MapArc;
    
    9.   aboutToAppear(): void {
    10.     this.mapOptions = {
    11.       position: {
    12.         target: {
    13.           latitude: 34.757975,
    14.           longitude: 113.665412
    15.         },
    16.         zoom: 6
    17.       }
    18.     }
    
    19.     this.callback = async (err, mapController) => {
    20.       if (!err) {
    21.         this.mapController = mapController;
    22.         if (!this.mapController) {
    23.           console.error(this.TAG, "mapController is null");
    24.           return;
    25.         }
    26.         // 设置弧线参数
    27.         let mapArcParams: mapCommon.MapArcParams = {
    28.           // 弧线起点坐标
    29.           startPoint: {
    30.             latitude: 39.913138,
    31.             longitude: 116.415112
    32.           },
    33.           // 弧线终点坐标
    34.           endPoint: {
    35.             latitude: 28.239473,
    36.             longitude: 112.954094
    37.           },
    38.           // 弧线中心点坐标
    39.           centerPoint: {
    40.             latitude: 33.86970399048567,
    41.             longitude: 112.08633528544145
    42.           },
    43.           width: 10,
    44.           color: 0xffff0000,
    45.           visible: true,
    46.           zIndex: 100
    47.         };
    48.         // 添加弧线
    49.         try {
    50.           this.mapArc = await this.mapController.addArc(mapArcParams);
    51.         } catch (e) {
    52.           console.error(`Failed to create the mapArc, code is：${e.code}, message is ${e.message}`);
    53.         }
    54.       } else {
    55.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    56.       }
    57.     }
    58.   }
    
    59.   build() {
    60.     Stack() {
    61.       Column() {
    62.         MapComponent({
    63.           mapOptions: this.mapOptions,
    64.           mapCallback: this.callback
    65.         })
    66.           .width('100%')
    67.           .height('100%');
    68.       }.width('100%')
    69.     }.height('100%')
    70.   }
    71. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.57878551733187142412358201578568:50001231000000:2800:139BB1FD1AE105FAE6B395A68FAB3114599C56491F4E4061364D27AD6A3A6E61.png "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-polyline "折线")
# 多边形

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将向您介绍如何在地图上绘制多边形。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.11671146316817067911833559437125:50001231000000:2800:41C5439BC0DCD88236B8F611026E6DC06D83F3B8DDDFE45F5D52F7D1DB726012.jpg "点击放大")

## 接口说明

添加多边形功能主要由[MapPolygonOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1615694815308)、[addPolygon](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1825517119280)和[MapPolygon](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mappolygon)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mappolygon)。

|接口名|描述|
|:--|:--|
|[MapPolygonOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1615694815308)|多边形参数。|
|[addPolygon](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1825517119280)(options: [mapCommon.MapPolygonOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1615694815308)): Promise<[MapPolygon](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mappolygon)>|在地图上添加一个多边形。|
|[MapPolygon](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mappolygon)|多边形，支持更新和查询相关属性。|

## 开发步骤

1. 导入相关模块。
    
    1. import { MapComponent, mapCommon, map } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 添加多边形，在callback方法中创建初始化参数并新建polygon。
    
    1. @Entry
    2. @Component
    3. struct MapPolygonDemo {
    4.   private mapOptions?: mapCommon.MapOptions;
    5.   private mapController?: map.MapComponentController;
    6.   private callback?: AsyncCallback<map.MapComponentController>;
    7.   private mapPolygon?: map.MapPolygon;
    
    8.   aboutToAppear(): void {
    9.     // 地图初始化参数
    10.     this.mapOptions = {
    11.       position: {
    12.         target: {
    13.           latitude: 31.98,
    14.           longitude: 118.78
    15.         },
    16.         zoom: 14
    17.       }
    18.     };
    19.     this.callback = async (err, mapController) => {
    20.       if (!err) {
    21.         this.mapController = mapController;
    22.         // 多边形初始化参数
    23.         let polygonOptions: mapCommon.MapPolygonOptions = {
    24.           points: [
    25.             { longitude: 118.78, latitude: 31.975 },
    26.             { longitude: 118.78, latitude: 31.985 },
    27.             { longitude: 118.79, latitude: 31.985 },
    28.             { longitude: 118.79, latitude: 31.975 }
    29.           ],
    30.           clickable: true,
    31.           fillColor: 0xff00DE00,
    32.           geodesic: false,
    33.           strokeColor: 0xff000000,
    34.           jointType: mapCommon.JointType.DEFAULT,
    35.           strokeWidth: 10,
    36.           visible: true,
    37.           zIndex: 10
    38.         }
    39.         // 创建多边形
    40.         try {
    41.           this.mapPolygon = await this.mapController.addPolygon(polygonOptions);
    42.         } catch (e) {
    43.           console.error(`Failed to create the mapPolygon, code is：${e.code}, message is ${e.message}`);
    44.         }
    45.       } else {
    46.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    47.       }
    48.     };
    49.   }
    
    50.   build() {
    51.     Stack() {
    52.       Column() {
    53.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback });
    54.       }.width('100%')
    55.     }.height('100%')
    56.   }
    57. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163726.22714731653159277514093990656870:50001231000000:2800:EC9573360DF239E385811EEED2714E557B779D70FE34FE4C40E0D9ABBF016259.jpg "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-arc "弧线")
# 点注释

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将向您介绍如何在地图的指定位置添加点注释以标识位置、商家、建筑等，并可以通过信息窗口展示详细信息。

点注释支持功能：

- 支持设置图标、文字、碰撞规则等。
- 支持添加点击事件。

[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)有默认风格，同时也支持自定义。由于内容丰富，以下只展示一些基础功能的使用，详细内容可参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163737.28891704460603994950413881942453:50001231000000:2800:DD7AC8AE0F71EFFF2802FD6FBAFD38C3D7B030E1EC83627EEEE14463B6C782CF.jpg "点击放大")

## 接口说明

添加点注释功能主要由[PointAnnotationParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section161194598375)、[addPointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1899064804520)、[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)、[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section636111479397)、[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section5365154710393)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)。

|接口名|描述|
|:--|:--|
|[PointAnnotationParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section161194598375)|点注释参数。|
|[addPointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1899064804520)(params: [mapCommon.PointAnnotationParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section161194598375)): Promise<[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)>|在地图上添加点注释。|
|[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)|点注释，支持更新和查询相关属性。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section636111479397)(type: 'pointAnnotationClick', callback: Callback<[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)>): void|设置点注释点击事件监听器。|
|[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section5365154710393)(type: 'pointAnnotationClick', callback?: Callback<[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)>): void|取消监听点注释点击事件。|

## 开发步骤

### 添加点注释

1. 导入相关模块。
    
    1. import { MapComponent, mapCommon, map } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 添加点注释，在callback方法中创建初始化参数并新建点注释。
    
    1. @Entry
    2. @Component
    3. struct PointAnnotationDemo {
    4.   private mapOptions?: mapCommon.MapOptions;
    5.   private mapController?: map.MapComponentController;
    6.   private callback?: AsyncCallback<map.MapComponentController>;
    7.   private mapEventManager?: map.MapEventManager;
    8.   private pointAnnotation?: map.PointAnnotation;
    9.   aboutToAppear(): void {
    10.     this.mapOptions = {
    11.       position: {
    12.         target: {
    13.           latitude: 32.020750,
    14.           longitude: 118.788765
    15.         },
    16.         zoom: 14
    17.       }
    18.     };
    19.     this.callback = async (err, mapController) => {
    20.       if (!err) {
    21.         this.mapController = mapController;
    22.         this.mapEventManager = this.mapController.getEventManager();
    23.         let pointAnnotationOptions: mapCommon.PointAnnotationParams = {
    24.           // 定义点注释图标锚点
    25.           position: {
    26.             latitude: 32.020750,
    27.             longitude: 118.788765
    28.           },
    29.           // 定义点注释名称与地图POI名称相同时，是否支持去重
    30.           repeatable: true,
    31.           // 定义点注释的碰撞规则
    32.           collisionRule: mapCommon.CollisionRule.NAME,
    33.           // 定义点注释的标题，数组长度最小为1，最大为3
    34.           titles: [{
    35.             // 定义标题内容
    36.             content: "南京夫子庙",
    37.             // 定义标题字体颜色
    38.             color: 0xFF000000,
    39.             // 定义标题字体大小
    40.             fontSize: 15,
    41.             // 定义标题描边颜色
    42.             strokeColor: 0xFFFFFFFF,
    43.             // 定义标题描边宽度
    44.             strokeWidth: 2,
    45.             // 定义标题字体样式
    46.             fontStyle: mapCommon.FontStyle.ITALIC
    47.           }],
    48.           // 定义点注释的图标，图标存放在resources/rawfile
    49.           icon: "",
    50.           // 定义点注释是否展示图标
    51.           showIcon: true,
    52.           // 定义点注释的锚点在水平方向上的位置
    53.           anchorU: 0.5,
    54.           // 定义点注释的锚点在垂直方向上的位置
    55.           anchorV: 1,
    56.           // 定义点注释的显示属性，为true时，在被碰撞后仍能显示
    57.           forceVisible: false,
    58.           // 定义碰撞优先级，数值越大，优先级越低
    59.           priority: 3,
    60.           // 定义点注释展示的最小层级
    61.           minZoom: 2,
    62.           // 定义点注释展示的最大层级
    63.           maxZoom: 20,
    64.           // 定义点注释是否可见
    65.           visible: true,
    66.           // 定义点注释叠加层级属性
    67.           zIndex: 10
    68.         }
    
    69.         // 创建pointAnnotation
    70.         try {
    71.           this.pointAnnotation = await this.mapController.addPointAnnotation(pointAnnotationOptions);
    72.         } catch (e) {
    73.           console.error(`Failed to create the pointAnnotation, code is：${e.code}, message is ${e.message}`);
    74.         }
    75.       } else {
    76.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    77.       }
    78.     };
    79.   }
    80.   build() {
    81.     Stack() {
    82.       Column() {
    83.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback });
    84.       }.width('100%')
    85.     }.height('100%')
    86.   }
    87. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163738.28299898701297285456222652471511:50001231000000:2800:290C863459CEDD1E16F409249AA1C7DF7543A1B2BE76C46ED15DB5DEB706CBDC.png "点击放大")
    
3. 在添加点注释之后，修改已经设置的点注释属性。
    
    1. // 设置点注释的显示层级为3~14级
    2. this.pointAnnotation.setZoom(3,14);
    3. // 设置点注释的碰撞优先级为10
    4. this.pointAnnotation.setPriority(10);
    

### 设置监听点注释点击事件

1. let callback = (pointAnnotation: map.PointAnnotation) => {
2.   console.info("pointAnnotationClick", `pointAnnotationClick: ${pointAnnotation.getId()}`);
3. };
4. this.mapEventManager.on("pointAnnotationClick", callback);

### 点注释动画

使用[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)的[setAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-basepriorityoverlay#section688810310374)方法设置动画。

调用[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)的[startAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-basepriorityoverlay#section15532754163419)方法启动动画。

1. let animation: map.ScaleAnimation = new map.ScaleAnimation(1, 3, 1, 3);
2. // 设置动画单次的时长
3. animation.setDuration(3000);
4. // 设置动画开始监听
5. let callbackStart = () => {
6.   console.info("animationStart", `callback`);
7. };
8. animation.on("animationStart", callbackStart);
9. // 设置动画结束监听
10. let callbackEnd = () => {
11.   console.info("animationEnd", `callback`);
12. };
13. animation.on("animationEnd", callbackEnd);
14. // 设置动画执行完成的状态
15. animation.setFillMode(map.AnimationFillMode.BACKWARDS);
16. // 设置动画重复的方式
17. animation.setRepeatMode(map.AnimationRepeatMode.REVERSE);
18. // 设置动画插值器
19. animation.setInterpolator(Curve.Linear);
20. // 设置动画的重复次数
21. animation.setRepeatCount(100);
22. this.pointAnnotation.setAnimation(animation);
23. this.pointAnnotation.startAnimation();

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163738.39738273380400265398250346751751:50001231000000:2800:77A2A1D463DB05899299260032993901D53BA240F0B18287F0EBAACFF0761558.gif "点击放大")

### 点注释标题动画

使用[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)的[setTitleAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation#section884818504399)方法设置标题动画。

调用[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)的[startTitleAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation#section108531150183916)方法启动标题动画。

1. let animation: map.FontSizeAnimation = new map.FontSizeAnimation(15, 45);
2. // 设置动画单次的时长
3. animation.setDuration(3000);
4. // 设置动画开始监听
5. let callbackStart = () => {
6.   console.info("animationStart", `callback`);
7. };
8. animation.on("animationStart", callbackStart);
9. // 设置动画结束监听
10. let callbackEnd = () => {
11.   console.info("animationEnd", `callback`);
12. };
13. animation.on("animationEnd", callbackEnd);
14. // 设置动画执行完成的状态
15. animation.setFillMode(map.AnimationFillMode.FORWARDS);
16. // 设置动画重复的方式
17. animation.setRepeatMode(map.AnimationRepeatMode.REVERSE);
18. // 设置动画插值器
19. animation.setInterpolator(Curve.Linear);
20. // 设置动画的重复次数
21. animation.setRepeatCount(100);
22. this.pointAnnotation.setTitleAnimation(animation);
23. this.pointAnnotation.startTitleAnimation();

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-circle "圆形")
# 点注释

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将向您介绍如何在地图的指定位置添加点注释以标识位置、商家、建筑等，并可以通过信息窗口展示详细信息。

点注释支持功能：

- 支持设置图标、文字、碰撞规则等。
- 支持添加点击事件。

[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)有默认风格，同时也支持自定义。由于内容丰富，以下只展示一些基础功能的使用，详细内容可参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163737.28891704460603994950413881942453:50001231000000:2800:DD7AC8AE0F71EFFF2802FD6FBAFD38C3D7B030E1EC83627EEEE14463B6C782CF.jpg "点击放大")

## 接口说明

添加点注释功能主要由[PointAnnotationParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section161194598375)、[addPointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1899064804520)、[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)、[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section636111479397)、[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section5365154710393)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)。

|接口名|描述|
|:--|:--|
|[PointAnnotationParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section161194598375)|点注释参数。|
|[addPointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1899064804520)(params: [mapCommon.PointAnnotationParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section161194598375)): Promise<[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)>|在地图上添加点注释。|
|[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)|点注释，支持更新和查询相关属性。|
|[on](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section636111479397)(type: 'pointAnnotationClick', callback: Callback<[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)>): void|设置点注释点击事件监听器。|
|[off](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapeventmanager#section5365154710393)(type: 'pointAnnotationClick', callback?: Callback<[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)>): void|取消监听点注释点击事件。|

## 开发步骤

### 添加点注释

1. 导入相关模块。
    
    1. import { MapComponent, mapCommon, map } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 添加点注释，在callback方法中创建初始化参数并新建点注释。
    
    1. @Entry
    2. @Component
    3. struct PointAnnotationDemo {
    4.   private mapOptions?: mapCommon.MapOptions;
    5.   private mapController?: map.MapComponentController;
    6.   private callback?: AsyncCallback<map.MapComponentController>;
    7.   private mapEventManager?: map.MapEventManager;
    8.   private pointAnnotation?: map.PointAnnotation;
    9.   aboutToAppear(): void {
    10.     this.mapOptions = {
    11.       position: {
    12.         target: {
    13.           latitude: 32.020750,
    14.           longitude: 118.788765
    15.         },
    16.         zoom: 14
    17.       }
    18.     };
    19.     this.callback = async (err, mapController) => {
    20.       if (!err) {
    21.         this.mapController = mapController;
    22.         this.mapEventManager = this.mapController.getEventManager();
    23.         let pointAnnotationOptions: mapCommon.PointAnnotationParams = {
    24.           // 定义点注释图标锚点
    25.           position: {
    26.             latitude: 32.020750,
    27.             longitude: 118.788765
    28.           },
    29.           // 定义点注释名称与地图POI名称相同时，是否支持去重
    30.           repeatable: true,
    31.           // 定义点注释的碰撞规则
    32.           collisionRule: mapCommon.CollisionRule.NAME,
    33.           // 定义点注释的标题，数组长度最小为1，最大为3
    34.           titles: [{
    35.             // 定义标题内容
    36.             content: "南京夫子庙",
    37.             // 定义标题字体颜色
    38.             color: 0xFF000000,
    39.             // 定义标题字体大小
    40.             fontSize: 15,
    41.             // 定义标题描边颜色
    42.             strokeColor: 0xFFFFFFFF,
    43.             // 定义标题描边宽度
    44.             strokeWidth: 2,
    45.             // 定义标题字体样式
    46.             fontStyle: mapCommon.FontStyle.ITALIC
    47.           }],
    48.           // 定义点注释的图标，图标存放在resources/rawfile
    49.           icon: "",
    50.           // 定义点注释是否展示图标
    51.           showIcon: true,
    52.           // 定义点注释的锚点在水平方向上的位置
    53.           anchorU: 0.5,
    54.           // 定义点注释的锚点在垂直方向上的位置
    55.           anchorV: 1,
    56.           // 定义点注释的显示属性，为true时，在被碰撞后仍能显示
    57.           forceVisible: false,
    58.           // 定义碰撞优先级，数值越大，优先级越低
    59.           priority: 3,
    60.           // 定义点注释展示的最小层级
    61.           minZoom: 2,
    62.           // 定义点注释展示的最大层级
    63.           maxZoom: 20,
    64.           // 定义点注释是否可见
    65.           visible: true,
    66.           // 定义点注释叠加层级属性
    67.           zIndex: 10
    68.         }
    
    69.         // 创建pointAnnotation
    70.         try {
    71.           this.pointAnnotation = await this.mapController.addPointAnnotation(pointAnnotationOptions);
    72.         } catch (e) {
    73.           console.error(`Failed to create the pointAnnotation, code is：${e.code}, message is ${e.message}`);
    74.         }
    75.       } else {
    76.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    77.       }
    78.     };
    79.   }
    80.   build() {
    81.     Stack() {
    82.       Column() {
    83.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback });
    84.       }.width('100%')
    85.     }.height('100%')
    86.   }
    87. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163738.28299898701297285456222652471511:50001231000000:2800:290C863459CEDD1E16F409249AA1C7DF7543A1B2BE76C46ED15DB5DEB706CBDC.png "点击放大")
    
3. 在添加点注释之后，修改已经设置的点注释属性。
    
    1. // 设置点注释的显示层级为3~14级
    2. this.pointAnnotation.setZoom(3,14);
    3. // 设置点注释的碰撞优先级为10
    4. this.pointAnnotation.setPriority(10);
    

### 设置监听点注释点击事件

1. let callback = (pointAnnotation: map.PointAnnotation) => {
2.   console.info("pointAnnotationClick", `pointAnnotationClick: ${pointAnnotation.getId()}`);
3. };
4. this.mapEventManager.on("pointAnnotationClick", callback);

### 点注释动画

使用[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)的[setAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-basepriorityoverlay#section688810310374)方法设置动画。

调用[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)的[startAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-basepriorityoverlay#section15532754163419)方法启动动画。

1. let animation: map.ScaleAnimation = new map.ScaleAnimation(1, 3, 1, 3);
2. // 设置动画单次的时长
3. animation.setDuration(3000);
4. // 设置动画开始监听
5. let callbackStart = () => {
6.   console.info("animationStart", `callback`);
7. };
8. animation.on("animationStart", callbackStart);
9. // 设置动画结束监听
10. let callbackEnd = () => {
11.   console.info("animationEnd", `callback`);
12. };
13. animation.on("animationEnd", callbackEnd);
14. // 设置动画执行完成的状态
15. animation.setFillMode(map.AnimationFillMode.BACKWARDS);
16. // 设置动画重复的方式
17. animation.setRepeatMode(map.AnimationRepeatMode.REVERSE);
18. // 设置动画插值器
19. animation.setInterpolator(Curve.Linear);
20. // 设置动画的重复次数
21. animation.setRepeatCount(100);
22. this.pointAnnotation.setAnimation(animation);
23. this.pointAnnotation.startAnimation();

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163738.39738273380400265398250346751751:50001231000000:2800:77A2A1D463DB05899299260032993901D53BA240F0B18287F0EBAACFF0761558.gif "点击放大")

### 点注释标题动画

使用[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)的[setTitleAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation#section884818504399)方法设置标题动画。

调用[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)的[startTitleAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation#section108531150183916)方法启动标题动画。

1. let animation: map.FontSizeAnimation = new map.FontSizeAnimation(15, 45);
2. // 设置动画单次的时长
3. animation.setDuration(3000);
4. // 设置动画开始监听
5. let callbackStart = () => {
6.   console.info("animationStart", `callback`);
7. };
8. animation.on("animationStart", callbackStart);
9. // 设置动画结束监听
10. let callbackEnd = () => {
11.   console.info("animationEnd", `callback`);
12. };
13. animation.on("animationEnd", callbackEnd);
14. // 设置动画执行完成的状态
15. animation.setFillMode(map.AnimationFillMode.FORWARDS);
16. // 设置动画重复的方式
17. animation.setRepeatMode(map.AnimationRepeatMode.REVERSE);
18. // 设置动画插值器
19. animation.setInterpolator(Curve.Linear);
20. // 设置动画的重复次数
21. animation.setRepeatCount(100);
22. this.pointAnnotation.setTitleAnimation(animation);
23. this.pointAnnotation.startTitleAnimation();

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-circle "圆形")
# 气泡

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将向您介绍如何在地图的指定位置添加气泡。

您可以通过气泡在道路上指定位置显示测速、拥堵情况。气泡支持功能：

- 支持设置四个方向的图标（传入的图标宽高需要相同）。
- 支持设置图标碰撞规则。
- 支持设置当前气泡的候选坐标段，通过计算使气泡在最佳的线段位置上。
- 支持设置图标动画。
- 支持添加点击事件。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163740.31667381632505295764456295474346:50001231000000:2800:046B0003D3845E422360CAB77C1EEB3AD4B36C05FAA5C92BBB12695229AB63D0.png "点击放大")

## 接口说明

添加气泡功能主要由[BubbleParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section10348735114315)、[addBubble](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1732020231338)和[Bubble](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-bubble)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-bubble)。

|接口名|描述|
|:--|:--|
|[BubbleParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section10348735114315)|气泡参数。|
|[addBubble](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1732020231338)(params: [mapCommon.BubbleParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section10348735114315)): Promise<[Bubble](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-bubble)>|在地图上添加气泡。|
|[Bubble](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-bubble)|气泡，支持更新和查询相关属性。|

## 开发步骤

### 添加气泡

1. 导入相关模块。
    
    1. import { MapComponent, mapCommon, map } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 添加气泡，在callback方法中创建初始化参数并新建气泡。
    
    1. @Entry
    2. @Component
    3. struct BubbleDemo {
    4.   private mapOptions?: mapCommon.MapOptions;
    5.   private mapController?: map.MapComponentController;
    6.   private callback?: AsyncCallback<map.MapComponentController>;
    7.   private bubble?: map.Bubble;
    
    8.   aboutToAppear(): void {
    9.     this.mapOptions = {
    10.       position: {
    11.         target: {
    12.           latitude: 39.918,
    13.           longitude: 116.397
    14.         },
    15.         zoom: 14
    16.       }
    17.     };
    
    18.     this.callback = async (err, mapController) => {
    19.       if (!err) {
    20.         this.mapController = mapController;
    21.         let bubbleOptions: mapCommon.BubbleParams = {
    22.           // 气泡位置
    23.           positions: [[{ 
    24.             latitude: 39.918,
    25.             longitude: 116.397
    26.           }]],
    27.           // 设置图标，必须提供4个方向的图标，图标存放在resources/rawfile
    28.           icons: [
    29.             'speed_limit_10.png',
    30.             'speed_limit_20.png',
    31.             'speed_limit_30.png',
    32.             'speed_limit_40.png'
    33.           ],
    34.           // 定义气泡的显示属性，为true时，在被碰撞后仍能显示
    35.           forceVisible: true,
    36.           // 定义气泡碰撞优先级，数值越大，优先级越低
    37.           priority: 3,
    38.           // 定义气泡展示的最小层级
    39.           minZoom: 2,
    40.           // 定义气泡展示的最大层级
    41.           maxZoom: 20,
    42.           // 定义气泡是否可见
    43.           visible: true,
    44.           // 定义气泡叠加层级属性
    45.           zIndex: 1
    46.         }
    
    47.         // 添加气泡
    48.         try {
    49.           this.bubble = await this.mapController.addBubble(bubbleOptions);
    50.         } catch (e) {
    51.           console.error(`Failed to create the bubble, code is：${e.code}, message is ${e.message}`);
    52.         }
    53.       } else {
    54.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    55.       }
    56.     };
    57.   }
    
    58.   build() {
    59.     Stack() {
    60.       Column() {
    61.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback });
    62.       }.width('100%')
    63.     }.height('100%')
    64.   }
    65. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163740.00854629280719425999522248475484:50001231000000:2800:B43B32ADAF0C06D1C7651ED52F96ACE47CB7378E8E224B54596A25607266FF93.jpg "点击放大")
    

### 设置监听气泡点击事件

1. let callback = (bubble: map.Bubble) => {
2.   console.info("bubbleClick", `callback bubble = ${bubble.getId()}`);
3. };
4. this.mapController?.on("bubbleClick", callback);

### 气泡动画

[Bubble](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-bubble)调用[setAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-basepriorityoverlay#section688810310374)设置动画。

[Bubble](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-bubble)调用[startAnimation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-basepriorityoverlay#section15532754163419)启动动画。

1. let animation: map.ScaleAnimation = new map.ScaleAnimation(1, 3, 1, 3);
2. // 设置动画单次的时长
3. animation.setDuration(3000);
4. // 设置动画开始监听
5. let callbackStart = () => {
6.   console.info("animationStart", `callback`);
7. };
8. animation.on("animationStart", callbackStart);
9. // 设置动画结束监听
10. let callbackEnd = () => {
11.   console.info("animationEnd", `callback`);
12. };
13. animation.on("animationEnd", callbackEnd);
14. // 设置动画执行完成的状态
15. animation.setFillMode(map.AnimationFillMode.BACKWARDS);
16. // 设置动画重复的方式
17. animation.setRepeatMode(map.AnimationRepeatMode.REVERSE);
18. // 设置动画插值器
19. animation.setInterpolator(Curve.Linear);
20. // 设置动画的重复次数
21. animation.setRepeatCount(100);
22. this.bubble.setAnimation(animation);
23. this.bubble.startAnimation();

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-annotation "点注释")
# 覆盖物

更新时间: 2025-12-16 16:37

## 场景介绍

地图覆盖物是固定在地图上的图片，本章节将向您介绍如何为地图增加覆盖物。

覆盖物，是一种位于底图和底图标注层之间的特殊Overlay，该图层不会遮挡地图标注信息。通过[ImageOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section12537418218)类来设置，开发者可以通过[ImageOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section12537418218)类设置一张图片，该图片可随地图的平移、缩放、旋转等操作做相应的变换。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163742.01698082155714487850815302676025:50001231000000:2800:1A6C597B63D96E2A98A93ACF54F3C245E02BBB50293CF4812FC61C93D337490F.png)

## 接口说明

增加覆盖物功能主要由[ImageOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section12537418218)、[addImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1177619539267)、[ImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-imageoverlay)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-imageoverlay)。

|接口名|描述|
|:--|:--|
|[ImageOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section12537418218)|覆盖物参数。|
|[addImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1177619539267)(params: [mapCommon.ImageOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section12537418218)): Promise<[ImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-imageoverlay)>|为地图增加覆盖物。|
|[ImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-imageoverlay)|覆盖物，支持更新和查询相关属性。|

## 开发步骤

1. 导入相关模块。
    
    import { map, mapCommon, MapComponent } from '@kit.MapKit';
    import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 增加覆盖物。
    
    @Entry
    @Component
    struct ImageOverlayDemo {
      private mapOptions?: mapCommon.MapOptions;
      private mapController?: map.MapComponentController;
      private callback?: AsyncCallback<map.MapComponentController>;
      private mapEventManager?: map.MapEventManager;
    
      aboutToAppear(): void {
        this.mapOptions = {
          position: {
            target: {
              latitude: 32.2,
              longitude: 118.2
            },
            zoom: 10
          }
        }
    
        this.callback = async (err, mapController) => {
          if (!err) {
            this.mapController = mapController;
            this.mapEventManager = this.mapController.getEventManager();
            let imageOverlayParams: mapCommon.ImageOverlayParams = {
              // 覆盖物范围
              bounds: {
                southwest: {
                  latitude: 32,
                  longitude: 118
                },
                northeast: {
                  latitude: 32.4,
                  longitude: 118.4
                }
              },
              // 覆盖物图片，图标需存放在resources/rawfile目录下
              image: 'icon/icon.png',
              transparency: 0.3,
              zIndex: 101,
              anchorU: 0.5,
              anchorV: 0.5,
              clickable: true,
              visible: true,
              bearing: 0
            };
            // 添加覆盖物
            try {
              let imageOverlay = await this.mapController?.addImageOverlay(imageOverlayParams);
            } catch (e) {
              console.error(`Failed to create the imageOverlay, code is：${e.code}, message is ${e.message}`);
            }
          } else {
            console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
          }
        }
      }
      build() {
        Stack() {
          Column() {
            MapComponent({
              mapOptions: this.mapOptions,
              mapCallback: this.callback,
            })
              .width('100%')
              .height('100%');
          }.width('100%')
        }.height('100%')
      }
    }
    
3. 设置覆盖物点击监听事件。
    
    let imageOverlayCallback: Callback<map.ImageOverlay> = (imageOverlay: map.ImageOverlay) => {
      console.info("imageOverlay callback");
    }
    // 打开覆盖物的点击监听
    this.mapEventManager.on("imageOverlayClick", imageOverlayCallback);
    // 关闭覆盖物的点击监听
    this.mapEventManager.off("imageOverlayClick", imageOverlayCallback);
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-aggregate "点聚合")
# 覆盖物

更新时间: 2025-12-16 16:37

## 场景介绍

地图覆盖物是固定在地图上的图片，本章节将向您介绍如何为地图增加覆盖物。

覆盖物，是一种位于底图和底图标注层之间的特殊Overlay，该图层不会遮挡地图标注信息。通过[ImageOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section12537418218)类来设置，开发者可以通过[ImageOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section12537418218)类设置一张图片，该图片可随地图的平移、缩放、旋转等操作做相应的变换。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163742.01698082155714487850815302676025:50001231000000:2800:1A6C597B63D96E2A98A93ACF54F3C245E02BBB50293CF4812FC61C93D337490F.png)

## 接口说明

增加覆盖物功能主要由[ImageOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section12537418218)、[addImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1177619539267)、[ImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-imageoverlay)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-imageoverlay)。

|接口名|描述|
|:--|:--|
|[ImageOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section12537418218)|覆盖物参数。|
|[addImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section1177619539267)(params: [mapCommon.ImageOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section12537418218)): Promise<[ImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-imageoverlay)>|为地图增加覆盖物。|
|[ImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-imageoverlay)|覆盖物，支持更新和查询相关属性。|

## 开发步骤

1. 导入相关模块。
    
    import { map, mapCommon, MapComponent } from '@kit.MapKit';
    import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 增加覆盖物。
    
    @Entry
    @Component
    struct ImageOverlayDemo {
      private mapOptions?: mapCommon.MapOptions;
      private mapController?: map.MapComponentController;
      private callback?: AsyncCallback<map.MapComponentController>;
      private mapEventManager?: map.MapEventManager;
    
      aboutToAppear(): void {
        this.mapOptions = {
          position: {
            target: {
              latitude: 32.2,
              longitude: 118.2
            },
            zoom: 10
          }
        }
    
        this.callback = async (err, mapController) => {
          if (!err) {
            this.mapController = mapController;
            this.mapEventManager = this.mapController.getEventManager();
            let imageOverlayParams: mapCommon.ImageOverlayParams = {
              // 覆盖物范围
              bounds: {
                southwest: {
                  latitude: 32,
                  longitude: 118
                },
                northeast: {
                  latitude: 32.4,
                  longitude: 118.4
                }
              },
              // 覆盖物图片，图标需存放在resources/rawfile目录下
              image: 'icon/icon.png',
              transparency: 0.3,
              zIndex: 101,
              anchorU: 0.5,
              anchorV: 0.5,
              clickable: true,
              visible: true,
              bearing: 0
            };
            // 添加覆盖物
            try {
              let imageOverlay = await this.mapController?.addImageOverlay(imageOverlayParams);
            } catch (e) {
              console.error(`Failed to create the imageOverlay, code is：${e.code}, message is ${e.message}`);
            }
          } else {
            console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
          }
        }
      }
      build() {
        Stack() {
          Column() {
            MapComponent({
              mapOptions: this.mapOptions,
              mapCallback: this.callback,
            })
              .width('100%')
              .height('100%');
          }.width('100%')
        }.height('100%')
      }
    }
    
3. 设置覆盖物点击监听事件。
    
    let imageOverlayCallback: Callback<map.ImageOverlay> = (imageOverlay: map.ImageOverlay) => {
      console.info("imageOverlay callback");
    }
    // 打开覆盖物的点击监听
    this.mapEventManager.on("imageOverlayClick", imageOverlayCallback);
    // 关闭覆盖物的点击监听
    this.mapEventManager.off("imageOverlayClick", imageOverlayCallback);
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-aggregate "点聚合")
# 设置地图元素压盖顺序

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将向您介绍如何设置地图元素的层级压盖关系。

设置地图元素的显示顺序，按照从低到高排列，即后面的地图元素会压盖前面的地图元素。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163743.30722807287018354758333431573877:50001231000000:2800:E93F022432B3A0FBBD1A3F10E0184035EB028D6A6E8637491E9EABBCAE903864.jpg "点击放大")

**表1** 地图元素类型压盖顺序
|枚举|枚举值|枚举含义|
|:--|:--|:--|
|OVERLAY|1|覆盖物，包括[MapCircle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcircle#section46461317478)、[MapPolygon](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mappolygon)、[MapPolyline](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mappolyline)、[MapArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-maparc)、[ImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-imageoverlay)、[TraceOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-traceoverlay)。|
|POI|2|底图[Poi](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1155919456273)。|
|CUSTOM_POI|3|支持碰撞的覆盖物，包括[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)、[Bubble](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-bubble)。|
|MARKER|4|包括[Marker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker)、[ClusterOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-clusteroverlay)。|

## 接口说明

设置层级压盖关系功能主要由[MapElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section17215821103111)、[setDisplayOrder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section10934934202319)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section10934934202319)。

|接口名|描述|
|:--|:--|
|[mapCommon.MapElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section17215821103111)|地图元素类型。|
|[setDisplayOrder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section10934934202319)(types: Array<[mapCommon.MapElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section17215821103111)>): void|设置地图元素的显示顺序。|

## 开发步骤

1. 导入相关模块。
    
    1. import { mapCommon, map, MapComponent } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 设置地图元素层级压盖关系。
    
    1. @Entry
    2. @Component
    3. struct MarkerDemo {
    4.   private mapOptions?: mapCommon.MapOptions;
    5.   private mapController?: map.MapComponentController;
    6.   private callback?: AsyncCallback<map.MapComponentController>;
    7.   private mapEventManager?: map.MapEventManager;
    8.   private marker?: map.Marker;
    9.   private bubble?: map.Bubble;
    
    10.   aboutToAppear(): void {
    11.     // 地图初始化参数
    12.     this.mapOptions = {
    13.       position: {
    14.         target: {
    15.           latitude: 31.984410259206815,
    16.           longitude: 118.26625379397866
    17.         },
    18.         zoom: 10
    19.       }
    20.     };
    21.     this.callback = async (err, mapController) => {
    22.       if (!err) {
    23.         this.mapController = mapController;
    24.         this.mapEventManager = this.mapController.getEventManager();
    25.         // Marker初始化参数
    26.         let markerOptions: mapCommon.MarkerOptions = {
    27.           position: {
    28.             latitude: 31.984410259206815,
    29.             longitude: 118.26625379397866
    30.           },
    31.           rotation: 0,
    32.           visible: true,
    33.           zIndex: 0,
    34.           alpha: 1,
    35.           anchorU: 0.5,
    36.           anchorV: 1,
    37.           clickable: true,
    38.           draggable: true,
    39.           flat: false
    40.         };
    41.         // 创建Marker
    42.         try {
    43.           this.marker = await this.mapController.addMarker(markerOptions);
    44.         } catch (e) {
    45.           console.error(`Failed to create the marker, code is：${e.code}, message is ${e.message}`);
    46.         }
    47.         let bubbleOptions: mapCommon.BubbleParams = {
    48.           // 气泡位置
    49.           positions: [[{
    50.             latitude: 32.384410259206815,
    51.             longitude: 118.26625379397866
    52.           }]],
    53.           // 设置图标，必须提供4个方向的图标，图标存放在resources/rawfile
    54.           icons: [
    55.             'speed_limit_10.png',
    56.             'speed_limit_20.png',
    57.             'speed_limit_30.png',
    58.             'speed_limit_40.png'
    59.           ],
    60.           // 定义气泡的显示属性，为true时，在被碰撞后仍能显示
    61.           forceVisible: true,
    62.           // 定义气泡碰撞优先级，数值越大，优先级越低
    63.           priority: 3,
    64.           // 定义气泡展示的最小层级
    65.           minZoom: 2,
    66.           // 定义气泡展示的最大层级
    67.           maxZoom: 20,
    68.           // 定义气泡是否可见
    69.           visible: true,
    70.           // 定义气泡叠加层级属性
    71.           zIndex: 1
    72.         }
    73.         // 添加气泡
    74.         try {
    75.           this.bubble = await this.mapController.addBubble(bubbleOptions);
    76.         } catch (e) {
    77.           console.error(`Failed to create the bubble, code is：${e.code}, message is ${e.message}`);
    78.         }
    79.         let imageOverlayParams: mapCommon.ImageOverlayParams = {
    80.           // 覆盖物范围
    81.           bounds: {
    82.             southwest: {
    83.               latitude: 32,
    84.               longitude: 118
    85.             },
    86.             northeast: {
    87.               latitude: 32.4,
    88.               longitude: 118.4
    89.             }
    90.           },
    91.           // 覆盖物图片
    92.           image: 'icon/icon.png',
    93.           transparency: 0.3,
    94.           zIndex: 101,
    95.           anchorU: 0.5,
    96.           anchorV: 0.5,
    97.           clickable: true,
    98.           visible: true,
    99.           bearing: 0
    100.         };
    101.         // 添加覆盖物
    102.         try {
    103.           await this.mapController?.addImageOverlay(imageOverlayParams);
    104.         } catch (e) {
    105.           console.error(`Failed to create the imageOverlay, code is：${e.code}, message is ${e.message}`);
    106.         }
    
    107.         // 设置压盖顺序，最底层的是覆盖物，后面依次是POI、支持碰撞的覆盖物和Marker，Marker在最表面一层
    108.         let mapElementTypeArr: Array<mapCommon.MapElementType> = [
    109.           mapCommon.MapElementType.OVERLAY,
    110.           mapCommon.MapElementType.POI,
    111.           mapCommon.MapElementType.CUSTOM_POI,
    112.           mapCommon.MapElementType.MARKER];
    113.         this.mapController.setDisplayOrder(mapElementTypeArr);
    114.       } else {
    115.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    116.       }
    117.     }
    118.   }
    
    119.   build() {
    120.     Stack() {
    121.       Column() {
    122.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback });
    123.       }.width('100%')
    124.     }.height('100%')
    125.   }
    126. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-dyntrajectories "动态轨迹")
# 设置地图元素压盖顺序

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将向您介绍如何设置地图元素的层级压盖关系。

设置地图元素的显示顺序，按照从低到高排列，即后面的地图元素会压盖前面的地图元素。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163743.30722807287018354758333431573877:50001231000000:2800:E93F022432B3A0FBBD1A3F10E0184035EB028D6A6E8637491E9EABBCAE903864.jpg "点击放大")

**表1** 地图元素类型压盖顺序
|枚举|枚举值|枚举含义|
|:--|:--|:--|
|OVERLAY|1|覆盖物，包括[MapCircle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcircle#section46461317478)、[MapPolygon](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mappolygon)、[MapPolyline](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mappolyline)、[MapArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-maparc)、[ImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-imageoverlay)、[TraceOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-traceoverlay)。|
|POI|2|底图[Poi](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1155919456273)。|
|CUSTOM_POI|3|支持碰撞的覆盖物，包括[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)、[Bubble](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-bubble)。|
|MARKER|4|包括[Marker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker)、[ClusterOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-clusteroverlay)。|

## 接口说明

设置层级压盖关系功能主要由[MapElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section17215821103111)、[setDisplayOrder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section10934934202319)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section10934934202319)。

|接口名|描述|
|:--|:--|
|[mapCommon.MapElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section17215821103111)|地图元素类型。|
|[setDisplayOrder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section10934934202319)(types: Array<[mapCommon.MapElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section17215821103111)>): void|设置地图元素的显示顺序。|

## 开发步骤

1. 导入相关模块。
    
    1. import { mapCommon, map, MapComponent } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 设置地图元素层级压盖关系。
    
    1. @Entry
    2. @Component
    3. struct MarkerDemo {
    4.   private mapOptions?: mapCommon.MapOptions;
    5.   private mapController?: map.MapComponentController;
    6.   private callback?: AsyncCallback<map.MapComponentController>;
    7.   private mapEventManager?: map.MapEventManager;
    8.   private marker?: map.Marker;
    9.   private bubble?: map.Bubble;
    
    10.   aboutToAppear(): void {
    11.     // 地图初始化参数
    12.     this.mapOptions = {
    13.       position: {
    14.         target: {
    15.           latitude: 31.984410259206815,
    16.           longitude: 118.26625379397866
    17.         },
    18.         zoom: 10
    19.       }
    20.     };
    21.     this.callback = async (err, mapController) => {
    22.       if (!err) {
    23.         this.mapController = mapController;
    24.         this.mapEventManager = this.mapController.getEventManager();
    25.         // Marker初始化参数
    26.         let markerOptions: mapCommon.MarkerOptions = {
    27.           position: {
    28.             latitude: 31.984410259206815,
    29.             longitude: 118.26625379397866
    30.           },
    31.           rotation: 0,
    32.           visible: true,
    33.           zIndex: 0,
    34.           alpha: 1,
    35.           anchorU: 0.5,
    36.           anchorV: 1,
    37.           clickable: true,
    38.           draggable: true,
    39.           flat: false
    40.         };
    41.         // 创建Marker
    42.         try {
    43.           this.marker = await this.mapController.addMarker(markerOptions);
    44.         } catch (e) {
    45.           console.error(`Failed to create the marker, code is：${e.code}, message is ${e.message}`);
    46.         }
    47.         let bubbleOptions: mapCommon.BubbleParams = {
    48.           // 气泡位置
    49.           positions: [[{
    50.             latitude: 32.384410259206815,
    51.             longitude: 118.26625379397866
    52.           }]],
    53.           // 设置图标，必须提供4个方向的图标，图标存放在resources/rawfile
    54.           icons: [
    55.             'speed_limit_10.png',
    56.             'speed_limit_20.png',
    57.             'speed_limit_30.png',
    58.             'speed_limit_40.png'
    59.           ],
    60.           // 定义气泡的显示属性，为true时，在被碰撞后仍能显示
    61.           forceVisible: true,
    62.           // 定义气泡碰撞优先级，数值越大，优先级越低
    63.           priority: 3,
    64.           // 定义气泡展示的最小层级
    65.           minZoom: 2,
    66.           // 定义气泡展示的最大层级
    67.           maxZoom: 20,
    68.           // 定义气泡是否可见
    69.           visible: true,
    70.           // 定义气泡叠加层级属性
    71.           zIndex: 1
    72.         }
    73.         // 添加气泡
    74.         try {
    75.           this.bubble = await this.mapController.addBubble(bubbleOptions);
    76.         } catch (e) {
    77.           console.error(`Failed to create the bubble, code is：${e.code}, message is ${e.message}`);
    78.         }
    79.         let imageOverlayParams: mapCommon.ImageOverlayParams = {
    80.           // 覆盖物范围
    81.           bounds: {
    82.             southwest: {
    83.               latitude: 32,
    84.               longitude: 118
    85.             },
    86.             northeast: {
    87.               latitude: 32.4,
    88.               longitude: 118.4
    89.             }
    90.           },
    91.           // 覆盖物图片
    92.           image: 'icon/icon.png',
    93.           transparency: 0.3,
    94.           zIndex: 101,
    95.           anchorU: 0.5,
    96.           anchorV: 0.5,
    97.           clickable: true,
    98.           visible: true,
    99.           bearing: 0
    100.         };
    101.         // 添加覆盖物
    102.         try {
    103.           await this.mapController?.addImageOverlay(imageOverlayParams);
    104.         } catch (e) {
    105.           console.error(`Failed to create the imageOverlay, code is：${e.code}, message is ${e.message}`);
    106.         }
    
    107.         // 设置压盖顺序，最底层的是覆盖物，后面依次是POI、支持碰撞的覆盖物和Marker，Marker在最表面一层
    108.         let mapElementTypeArr: Array<mapCommon.MapElementType> = [
    109.           mapCommon.MapElementType.OVERLAY,
    110.           mapCommon.MapElementType.POI,
    111.           mapCommon.MapElementType.CUSTOM_POI,
    112.           mapCommon.MapElementType.MARKER];
    113.         this.mapController.setDisplayOrder(mapElementTypeArr);
    114.       } else {
    115.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    116.       }
    117.     }
    118.   }
    
    119.   build() {
    120.     Stack() {
    121.       Column() {
    122.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback });
    123.       }.width('100%')
    124.     }.height('100%')
    125.   }
    126. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-dyntrajectories "动态轨迹")
# 设置地图元素压盖顺序

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将向您介绍如何设置地图元素的层级压盖关系。

设置地图元素的显示顺序，按照从低到高排列，即后面的地图元素会压盖前面的地图元素。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163743.30722807287018354758333431573877:50001231000000:2800:E93F022432B3A0FBBD1A3F10E0184035EB028D6A6E8637491E9EABBCAE903864.jpg "点击放大")

**表1** 地图元素类型压盖顺序
|枚举|枚举值|枚举含义|
|:--|:--|:--|
|OVERLAY|1|覆盖物，包括[MapCircle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcircle#section46461317478)、[MapPolygon](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mappolygon)、[MapPolyline](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mappolyline)、[MapArc](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-maparc)、[ImageOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-imageoverlay)、[TraceOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-traceoverlay)。|
|POI|2|底图[Poi](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1155919456273)。|
|CUSTOM_POI|3|支持碰撞的覆盖物，包括[PointAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-pointannotation)、[Bubble](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-bubble)。|
|MARKER|4|包括[Marker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-marker)、[ClusterOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-clusteroverlay)。|

## 接口说明

设置层级压盖关系功能主要由[MapElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section17215821103111)、[setDisplayOrder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section10934934202319)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section10934934202319)。

|接口名|描述|
|:--|:--|
|[mapCommon.MapElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section17215821103111)|地图元素类型。|
|[setDisplayOrder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section10934934202319)(types: Array<[mapCommon.MapElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section17215821103111)>): void|设置地图元素的显示顺序。|

## 开发步骤

1. 导入相关模块。
    
    1. import { mapCommon, map, MapComponent } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 设置地图元素层级压盖关系。
    
    1. @Entry
    2. @Component
    3. struct MarkerDemo {
    4.   private mapOptions?: mapCommon.MapOptions;
    5.   private mapController?: map.MapComponentController;
    6.   private callback?: AsyncCallback<map.MapComponentController>;
    7.   private mapEventManager?: map.MapEventManager;
    8.   private marker?: map.Marker;
    9.   private bubble?: map.Bubble;
    
    10.   aboutToAppear(): void {
    11.     // 地图初始化参数
    12.     this.mapOptions = {
    13.       position: {
    14.         target: {
    15.           latitude: 31.984410259206815,
    16.           longitude: 118.26625379397866
    17.         },
    18.         zoom: 10
    19.       }
    20.     };
    21.     this.callback = async (err, mapController) => {
    22.       if (!err) {
    23.         this.mapController = mapController;
    24.         this.mapEventManager = this.mapController.getEventManager();
    25.         // Marker初始化参数
    26.         let markerOptions: mapCommon.MarkerOptions = {
    27.           position: {
    28.             latitude: 31.984410259206815,
    29.             longitude: 118.26625379397866
    30.           },
    31.           rotation: 0,
    32.           visible: true,
    33.           zIndex: 0,
    34.           alpha: 1,
    35.           anchorU: 0.5,
    36.           anchorV: 1,
    37.           clickable: true,
    38.           draggable: true,
    39.           flat: false
    40.         };
    41.         // 创建Marker
    42.         try {
    43.           this.marker = await this.mapController.addMarker(markerOptions);
    44.         } catch (e) {
    45.           console.error(`Failed to create the marker, code is：${e.code}, message is ${e.message}`);
    46.         }
    47.         let bubbleOptions: mapCommon.BubbleParams = {
    48.           // 气泡位置
    49.           positions: [[{
    50.             latitude: 32.384410259206815,
    51.             longitude: 118.26625379397866
    52.           }]],
    53.           // 设置图标，必须提供4个方向的图标，图标存放在resources/rawfile
    54.           icons: [
    55.             'speed_limit_10.png',
    56.             'speed_limit_20.png',
    57.             'speed_limit_30.png',
    58.             'speed_limit_40.png'
    59.           ],
    60.           // 定义气泡的显示属性，为true时，在被碰撞后仍能显示
    61.           forceVisible: true,
    62.           // 定义气泡碰撞优先级，数值越大，优先级越低
    63.           priority: 3,
    64.           // 定义气泡展示的最小层级
    65.           minZoom: 2,
    66.           // 定义气泡展示的最大层级
    67.           maxZoom: 20,
    68.           // 定义气泡是否可见
    69.           visible: true,
    70.           // 定义气泡叠加层级属性
    71.           zIndex: 1
    72.         }
    73.         // 添加气泡
    74.         try {
    75.           this.bubble = await this.mapController.addBubble(bubbleOptions);
    76.         } catch (e) {
    77.           console.error(`Failed to create the bubble, code is：${e.code}, message is ${e.message}`);
    78.         }
    79.         let imageOverlayParams: mapCommon.ImageOverlayParams = {
    80.           // 覆盖物范围
    81.           bounds: {
    82.             southwest: {
    83.               latitude: 32,
    84.               longitude: 118
    85.             },
    86.             northeast: {
    87.               latitude: 32.4,
    88.               longitude: 118.4
    89.             }
    90.           },
    91.           // 覆盖物图片
    92.           image: 'icon/icon.png',
    93.           transparency: 0.3,
    94.           zIndex: 101,
    95.           anchorU: 0.5,
    96.           anchorV: 0.5,
    97.           clickable: true,
    98.           visible: true,
    99.           bearing: 0
    100.         };
    101.         // 添加覆盖物
    102.         try {
    103.           await this.mapController?.addImageOverlay(imageOverlayParams);
    104.         } catch (e) {
    105.           console.error(`Failed to create the imageOverlay, code is：${e.code}, message is ${e.message}`);
    106.         }
    
    107.         // 设置压盖顺序，最底层的是覆盖物，后面依次是POI、支持碰撞的覆盖物和Marker，Marker在最表面一层
    108.         let mapElementTypeArr: Array<mapCommon.MapElementType> = [
    109.           mapCommon.MapElementType.OVERLAY,
    110.           mapCommon.MapElementType.POI,
    111.           mapCommon.MapElementType.CUSTOM_POI,
    112.           mapCommon.MapElementType.MARKER];
    113.         this.mapController.setDisplayOrder(mapElementTypeArr);
    114.       } else {
    115.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    116.       }
    117.     }
    118.   }
    
    119.   build() {
    120.     Stack() {
    121.       Column() {
    122.         MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback });
    123.       }.width('100%')
    124.     }.height('100%')
    125.   }
    126. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-dyntrajectories "动态轨迹")
# 热力图

更新时间: 2025-12-16 16:37

## 场景介绍

从6.0.0(20)开始，支持热力图功能。

新增热力图层，用于展示数据的分布情况。通过热力图功能，将数据用不同颜色的区块在地图上展示，可以直观地描述在地图上某个区域内人群或车辆的密度和分布情况。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163744.07938495166908534953321192215270:50001231000000:2800:89D2DF6A47F5A4AE2FC6E305A8A46277F4B7286C44C2C874D63CDF3DBB04060A.png "点击放大")

## 接口说明

热力图功能主要由[HeatmapParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section273113662417)、[addHeatmap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section849314585910)和[Heatmap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-heatmap#section792365317339)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-heatmap#section792365317339)。

|接口名|描述|
|:--|:--|
|[HeatmapParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section273113662417)|热力图参数。|
|[addHeatmap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section849314585910)(params: [mapCommon.HeatmapParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section273113662417)): Promise<[Heatmap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-heatmap#section792365317339)>|新增热力图。|
|[Heatmap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-heatmap#section792365317339)|热力图，支持修改和删除热力图，例如：支持设置颜色、设置透明度等。|

## 开发步骤

1. 导入相关模块。
    
    1. import { map, mapCommon, MapComponent } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 增加热力图。
    
    1. @Entry
    2. @Component
    3. struct HeatMapDemo {
    4.   private TAG = "OHMapSDK_HeatMapDemo";
    5.   private mapOption?: mapCommon.MapOptions;
    6.   private mapController?: map.MapComponentController;
    7.   private callback?: AsyncCallback<map.MapComponentController>;
    
    8.   aboutToAppear(): void {
    9.     this.mapOption = {
    10.       position: {
    11.         target: {
    12.           latitude: 31.000000,
    13.           longitude: 118.000000
    14.         },
    15.         zoom: 11
    16.       }
    17.     }
    18.     this.callback = async (err, mapController) => {
    19.       console.info(this.TAG, "mapCallback err=" + JSON.stringify(err) +
    20.         "; mapController=" + JSON.stringify(mapController));
    21.       if (!err) {
    22.         this.mapController = mapController;
    23.         let data: mapCommon.WeightedLatLng[] = [];
    24.         for (let i = 0; i < 500; i++) {
    25.           data.push({
    26.             point: {
    27.               longitude: 118.000000 + Math.random() * 1 - 0.25,
    28.               latitude: 31.000000 + Math.random() * 1 - 0.25
    29.             },
    30.             intensity: 1
    31.           });
    32.         }
    33.         let heatMapOptions: mapCommon.HeatmapParams = {
    34.           id: 'heatmap0001',
    35.           data:data,
    36.           radius:20,
    37.           intensity: {
    38.             2: 1,
    39.             5: 5,
    40.             8: 10
    41.           }
    42.         }
    43.         try {
    44.           await this.mapController?.addHeatmap(heatMapOptions);
    45.         } catch (e) {
    46.           console.error(this.TAG, `code:${e.code}, message:${e.message}`);
    47.         }
    48.       } else {
    49.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    50.       }
    51.     }
    52.   }
    53.   build() {
    54.     Stack() {
    55.       Column() {
    56.         MapComponent({ mapOptions: this.mapOption, mapCallback: this.callback })
    57.           .width('100%')
    58.           .height('100%');
    59.       }.width('100%')
    60.     }.height('100%')
    61.   }
    62. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-tile "瓦片图层")
# 热力图

更新时间: 2025-12-16 16:37

## 场景介绍

从6.0.0(20)开始，支持热力图功能。

新增热力图层，用于展示数据的分布情况。通过热力图功能，将数据用不同颜色的区块在地图上展示，可以直观地描述在地图上某个区域内人群或车辆的密度和分布情况。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163744.07938495166908534953321192215270:50001231000000:2800:89D2DF6A47F5A4AE2FC6E305A8A46277F4B7286C44C2C874D63CDF3DBB04060A.png "点击放大")

## 接口说明

热力图功能主要由[HeatmapParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section273113662417)、[addHeatmap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section849314585910)和[Heatmap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-heatmap#section792365317339)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-heatmap#section792365317339)。

|接口名|描述|
|:--|:--|
|[HeatmapParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section273113662417)|热力图参数。|
|[addHeatmap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section849314585910)(params: [mapCommon.HeatmapParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section273113662417)): Promise<[Heatmap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-heatmap#section792365317339)>|新增热力图。|
|[Heatmap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-heatmap#section792365317339)|热力图，支持修改和删除热力图，例如：支持设置颜色、设置透明度等。|

## 开发步骤

1. 导入相关模块。
    
    1. import { map, mapCommon, MapComponent } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 增加热力图。
    
    1. @Entry
    2. @Component
    3. struct HeatMapDemo {
    4.   private TAG = "OHMapSDK_HeatMapDemo";
    5.   private mapOption?: mapCommon.MapOptions;
    6.   private mapController?: map.MapComponentController;
    7.   private callback?: AsyncCallback<map.MapComponentController>;
    
    8.   aboutToAppear(): void {
    9.     this.mapOption = {
    10.       position: {
    11.         target: {
    12.           latitude: 31.000000,
    13.           longitude: 118.000000
    14.         },
    15.         zoom: 11
    16.       }
    17.     }
    18.     this.callback = async (err, mapController) => {
    19.       console.info(this.TAG, "mapCallback err=" + JSON.stringify(err) +
    20.         "; mapController=" + JSON.stringify(mapController));
    21.       if (!err) {
    22.         this.mapController = mapController;
    23.         let data: mapCommon.WeightedLatLng[] = [];
    24.         for (let i = 0; i < 500; i++) {
    25.           data.push({
    26.             point: {
    27.               longitude: 118.000000 + Math.random() * 1 - 0.25,
    28.               latitude: 31.000000 + Math.random() * 1 - 0.25
    29.             },
    30.             intensity: 1
    31.           });
    32.         }
    33.         let heatMapOptions: mapCommon.HeatmapParams = {
    34.           id: 'heatmap0001',
    35.           data:data,
    36.           radius:20,
    37.           intensity: {
    38.             2: 1,
    39.             5: 5,
    40.             8: 10
    41.           }
    42.         }
    43.         try {
    44.           await this.mapController?.addHeatmap(heatMapOptions);
    45.         } catch (e) {
    46.           console.error(this.TAG, `code:${e.code}, message:${e.message}`);
    47.         }
    48.       } else {
    49.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    50.       }
    51.     }
    52.   }
    53.   build() {
    54.     Stack() {
    55.       Column() {
    56.         MapComponent({ mapOptions: this.mapOption, mapCallback: this.callback })
    57.           .width('100%')
    58.           .height('100%');
    59.       }.width('100%')
    60.     }.height('100%')
    61.   }
    62. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-tile "瓦片图层")
# 流场图层

更新时间: 2025-12-16 16:37

## 场景介绍

从6.0.0(20)开始，支持流场图层功能。

新增流场图层，用于在基础地图之上叠加数据。通常用于实时展示天气风场、洋流等场景。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163745.34062036025672050284630166327802:50001231000000:2800:6B82A49EC4D6AB60A2F26CBCAE1FD0E108A0E675BA2A2E0800BA6DAA339C092A.gif "点击放大")

## 接口说明

流场图层功能主要由[FlowFieldOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1920897172416)、[addFlowFieldOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section7516202017439)和[FlowFieldOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-flowfieldoverlay)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-flowfieldoverlay)。

|接口名|描述|
|:--|:--|
|[FlowFieldOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1920897172416)|流场覆盖物参数。|
|[addFlowFieldOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section7516202017439)(params: mapCommon.[FlowFieldOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1920897172416)): Promise<[FlowFieldOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-flowfieldoverlay)>|新增流场覆盖物。|
|[FlowFieldOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-flowfieldoverlay)|流场覆盖物管理对象。|

## 开发步骤

### 添加流场图层

1. 导入相关模块。
    
    1. import { mapCommon, map, MapComponent } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 绘制流场图层。
    
    1. @Entry
    2. @Component
    3. struct MapFlowFieldOverlayDemo {
    4.   private TAG = "OHMapSDK_MapFlowFieldOverlayDemo";
    5.   private mapOption?: mapCommon.MapOptions;
    6.   private mapController?: map.MapComponentController;
    7.   private callback?: AsyncCallback<map.MapComponentController>;
    8.   private fieldOverlay?: map.FlowFieldOverlay;
    
    9.   aboutToAppear(): void {
    10.     this.mapOption = {
    11.       position: {
    12.         target: {
    13.           latitude: 48.87278,
    14.           longitude: 2.33016
    15.         },
    16.         zoom: 4
    17.       },
    18.       scaleControlsEnabled: true
    19.     }
    
    20.     this.callback = async (err, mapController) => {
    21.       if (!err) {
    22.         this.mapController = mapController;
    23.         let params: mapCommon.FlowFieldOverlayParams = {
    24.           // data为GRIB2规范的json数据，需开发者自行传输，可参考流场数据格式
    25.           data: `xxxxx`,
    26.           style: {
    27.             count: 10000,
    28.             color: 0xff0000ff,
    29.             maxSpeed: 70,
    30.             speedFactor: 0.2
    31.           }
    32.         };
    
    33.         try {
    34.           this.fieldOverlay = await this.mapController?.addFlowFieldOverlay(params);
    35.         } catch (e) {
    36.           console.error(this.TAG, `code:${e.code}, message:${e.message}`);
    37.         }
    38.       } else {
    39.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    40.       }
    41.     }
    42.   }
    
    43.   build() {
    44.     Stack() {
    45.       Column() {
    46.         MapComponent({ mapOptions: this.mapOption, mapCallback: this.callback })
    47.           .width('100%')
    48.           .height('65%');
    49.       }.width('100%')
    50.     }.height('100%')
    51.   }
    52. }
    

### 流场数据格式参考

[FlowFieldOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1920897172416)类的data参数格式为GRIB2规范的json数据。GRIB2是一种由世界气象组织（WMO）定义的二进制数据格式，主要用于存储和传输气象和气候数据。

1. [
2.   // header表示数据的整体信息，data表示横向速度
3.   {"header":{},"data":[]},
4.   // header表示数据的整体信息，data表示纵向速度
5.   {"header":{},"data":[]}
6. ]

下面是风场数据的示例：

1. [{
2.   "header": {
3.     "parameterUnit": "m.s-1",   // 风速单位
4.     "parameterNumber": 2,       // 风速方向，2为U方向（横向），3为V方向（纵向）
5.     "dx": 10,                   // 横向步长，即每个格子占用的经度值
6.     "dy": 20,                   // 纵向步长，即每个格子占用的纬度值
7.     "parameterNumberName": "U-component-wind",   // 风速方向名称，U方向
8.     "la2": -90,                 // 纬度范围
9.     "la1": 90,                  // 纬度范围
10.     "parameterCategory": 2,     // 数据类别
11.     "lo1": 0,                   // 经度范围
12.     "lo2": 359.75,              // 经度范围
13.     "ny": 4,                    // 纵向格子数量
14.     "nx": 4,                    // 横向格子数量
15.     "numberPoints": 16          // 表示风速的点数量，即单个data中的数据量
16.   },
17.   // 横向速度，数据量需等于numberPoints
18.   "data": [2, 2, 2, 2, 2, 2, 2, 2, -10, -10, -1, -1, -1, -1, -3, 2]
19. }, {
20.   "header": {
21.     "parameterUnit": "m.s-1",   // 风速单位
22.     "parameterNumber": 3,       // 风速方向，2为U方向（横向），3为V方向（纵向）
23.     "dx": 4,                    // 横向步长，即每个格子占用的经度值
24.     "dy": 4,                    // 纵向步长，即每个格子占用的纬度值
25.     "parameterNumberName": "U-component-wind",   // 风速方向名称，U方向
26.     "la2": -90,                 // 纬度范围
27.     "la1": 90,                  // 纬度范围
28.     "parameterCategory": 2,     // 数据类别
29.     "lo1": 0,                   // 经度范围
30.     "lo2": 359.75,              // 经度范围
31.     "ny": 4,                    // 纵向格子数量
32.     "nx": 4,                    // 横向格子数量
33.     "numberPoints": 16          // 表示风速的点数量，即单个data中的数据量
34.   },
35.   // 横向速度，数据量需等于numberPoints
36.   "data": [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, -1, -1, -2, -3, -1]
37. }]

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-mvt-overlay "矢量图层")
# 流场图层

更新时间: 2025-12-16 16:37

## 场景介绍

从6.0.0(20)开始，支持流场图层功能。

新增流场图层，用于在基础地图之上叠加数据。通常用于实时展示天气风场、洋流等场景。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163745.34062036025672050284630166327802:50001231000000:2800:6B82A49EC4D6AB60A2F26CBCAE1FD0E108A0E675BA2A2E0800BA6DAA339C092A.gif "点击放大")

## 接口说明

流场图层功能主要由[FlowFieldOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1920897172416)、[addFlowFieldOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section7516202017439)和[FlowFieldOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-flowfieldoverlay)提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-flowfieldoverlay)。

|接口名|描述|
|:--|:--|
|[FlowFieldOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1920897172416)|流场覆盖物参数。|
|[addFlowFieldOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-mapcomponentcontroller#section7516202017439)(params: mapCommon.[FlowFieldOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1920897172416)): Promise<[FlowFieldOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-flowfieldoverlay)>|新增流场覆盖物。|
|[FlowFieldOverlay](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-flowfieldoverlay)|流场覆盖物管理对象。|

## 开发步骤

### 添加流场图层

1. 导入相关模块。
    
    1. import { mapCommon, map, MapComponent } from '@kit.MapKit';
    2. import { AsyncCallback } from '@kit.BasicServicesKit';
    
2. 绘制流场图层。
    
    1. @Entry
    2. @Component
    3. struct MapFlowFieldOverlayDemo {
    4.   private TAG = "OHMapSDK_MapFlowFieldOverlayDemo";
    5.   private mapOption?: mapCommon.MapOptions;
    6.   private mapController?: map.MapComponentController;
    7.   private callback?: AsyncCallback<map.MapComponentController>;
    8.   private fieldOverlay?: map.FlowFieldOverlay;
    
    9.   aboutToAppear(): void {
    10.     this.mapOption = {
    11.       position: {
    12.         target: {
    13.           latitude: 48.87278,
    14.           longitude: 2.33016
    15.         },
    16.         zoom: 4
    17.       },
    18.       scaleControlsEnabled: true
    19.     }
    
    20.     this.callback = async (err, mapController) => {
    21.       if (!err) {
    22.         this.mapController = mapController;
    23.         let params: mapCommon.FlowFieldOverlayParams = {
    24.           // data为GRIB2规范的json数据，需开发者自行传输，可参考流场数据格式
    25.           data: `xxxxx`,
    26.           style: {
    27.             count: 10000,
    28.             color: 0xff0000ff,
    29.             maxSpeed: 70,
    30.             speedFactor: 0.2
    31.           }
    32.         };
    
    33.         try {
    34.           this.fieldOverlay = await this.mapController?.addFlowFieldOverlay(params);
    35.         } catch (e) {
    36.           console.error(this.TAG, `code:${e.code}, message:${e.message}`);
    37.         }
    38.       } else {
    39.         console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
    40.       }
    41.     }
    42.   }
    
    43.   build() {
    44.     Stack() {
    45.       Column() {
    46.         MapComponent({ mapOptions: this.mapOption, mapCallback: this.callback })
    47.           .width('100%')
    48.           .height('65%');
    49.       }.width('100%')
    50.     }.height('100%')
    51.   }
    52. }
    

### 流场数据格式参考

[FlowFieldOverlayParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section1920897172416)类的data参数格式为GRIB2规范的json数据。GRIB2是一种由世界气象组织（WMO）定义的二进制数据格式，主要用于存储和传输气象和气候数据。

1. [
2.   // header表示数据的整体信息，data表示横向速度
3.   {"header":{},"data":[]},
4.   // header表示数据的整体信息，data表示纵向速度
5.   {"header":{},"data":[]}
6. ]

下面是风场数据的示例：

1. [{
2.   "header": {
3.     "parameterUnit": "m.s-1",   // 风速单位
4.     "parameterNumber": 2,       // 风速方向，2为U方向（横向），3为V方向（纵向）
5.     "dx": 10,                   // 横向步长，即每个格子占用的经度值
6.     "dy": 20,                   // 纵向步长，即每个格子占用的纬度值
7.     "parameterNumberName": "U-component-wind",   // 风速方向名称，U方向
8.     "la2": -90,                 // 纬度范围
9.     "la1": 90,                  // 纬度范围
10.     "parameterCategory": 2,     // 数据类别
11.     "lo1": 0,                   // 经度范围
12.     "lo2": 359.75,              // 经度范围
13.     "ny": 4,                    // 纵向格子数量
14.     "nx": 4,                    // 横向格子数量
15.     "numberPoints": 16          // 表示风速的点数量，即单个data中的数据量
16.   },
17.   // 横向速度，数据量需等于numberPoints
18.   "data": [2, 2, 2, 2, 2, 2, 2, 2, -10, -10, -1, -1, -1, -1, -3, 2]
19. }, {
20.   "header": {
21.     "parameterUnit": "m.s-1",   // 风速单位
22.     "parameterNumber": 3,       // 风速方向，2为U方向（横向），3为V方向（纵向）
23.     "dx": 4,                    // 横向步长，即每个格子占用的经度值
24.     "dy": 4,                    // 纵向步长，即每个格子占用的纬度值
25.     "parameterNumberName": "U-component-wind",   // 风速方向名称，U方向
26.     "la2": -90,                 // 纬度范围
27.     "la1": 90,                  // 纬度范围
28.     "parameterCategory": 2,     // 数据类别
29.     "lo1": 0,                   // 经度范围
30.     "lo2": 359.75,              // 经度范围
31.     "ny": 4,                    // 纵向格子数量
32.     "nx": 4,                    // 横向格子数量
33.     "numberPoints": 16          // 表示风速的点数量，即单个data中的数据量
34.   },
35.   // 横向速度，数据量需等于numberPoints
36.   "data": [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, -1, -1, -2, -3, -1]
37. }]

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-mvt-overlay "矢量图层")
# POI搜索

更新时间: 2025-12-16 16:36

## 场景介绍

提供多种查询POI信息的能力：

- 关键字搜索：通过用户输入的关键字，返回地点列表。
- 周边搜索：基于用户设备位置进行地点查找。
- 自动补全：根据输入的关键字返回预测的输入关键字和地点查询建议。
- 地点详情：查询某个地点更详细的信息。

## 接口说明

以下是POI搜索相关接口，主要由[site](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site)命名空间下的方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site)。

|接口名|描述|
|:--|:--|
|[searchByText](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section1117619561413)(searchByTextParams: [SearchByTextParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section186305710274)): Promise<[SearchByTextResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section55651334123013)>|关键字搜索。|
|[searchByText](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section142981754612)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), searchByTextParams: [SearchByTextParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section186305710274)): Promise<[SearchByTextResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section55651334123013)>|关键字搜索。支持上传Context上下文。|
|[nearbySearch](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section6315894393)(nearbySearchParams: [NearbySearchParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section1963813341280)): Promise<[NearbySearchResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section15617144513016)>|周边搜索。|
|[nearbySearch](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section4478173620711)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), nearbySearchParams: [NearbySearchParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section1963813341280)): Promise<[NearbySearchResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section15617144513016)>|周边搜索。支持上传Context上下文。|
|[queryAutoComplete](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section20324320183912)(queryAutoCompleteParams: [QueryAutoCompleteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section18371146292)): Promise<[QueryAutoCompleteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section81901456163020)>|自动补全。|
|[queryAutoComplete](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section1095410462267)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), queryAutoCompleteParams: [QueryAutoCompleteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section18371146292)): Promise<[QueryAutoCompleteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section81901456163020)>|自动补全。支持上传Context上下文。|
|[searchById](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section17490031173910)(searchByIdParams: [SearchByIdParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section756019297292)): Promise<[SearchByIdResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section9671461314)>|地点详情。|
|[searchById](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section192881428123313)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), searchByIdParams: [SearchByIdParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section756019297292)): Promise<[SearchByIdResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section9671461314)>|地点详情。支持上传Context上下文。|

## 开发步骤

导入相关模块。

1. import { site } from '@kit.MapKit';
2. import { BusinessError } from '@kit.BasicServicesKit';

### 关键字搜索

通过指定的关键字和可选的地理范围，查询诸如旅游景点、企业和学校之类的地点。

1. let params: site.SearchByTextParams = {
2.   // 根据自定义关键字进行搜索，例如：“故宫”、“夫子庙”
3.   query: "Piazzale Dante, 41, 55049 Viareggio, Tuscany, Italy",
4.   // 经纬度坐标
5.   location: {
6.     latitude: 31.984,
7.     longitude: 118.76625
8.   },
9.   // 指定地理位置的范围半径
10.   radius: 10000,
11.   // 搜索结果的语言类型
12.   language: "en"
13. };
14. // 返回关键字搜索结果
15. try {
16.   const result = await site.searchByText(params);
17.   console.info(`Succeeded in searching by text. result is ${JSON.stringify(result)}`);
18. } catch (error) {
19.   const err: BusinessError = error as BusinessError;
20.   console.error(`Failed in searching by text. Code is ${err.code}, message is ${err.message}`);
21. }

### 周边搜索

通过用户传入自己的位置，可以返回周边地点列表。您可以通过提供关键字或指定要搜索的地点的类型来优化搜索结果。

1. let params: site.NearbySearchParams = {
2.   location: {
3.     latitude:51.50811219132287,
4.     longitude:-0.07594896472392065
5.   },
6.   poiTypes: [
7.     "Watch_Store",
8.     "SUBWAY",
9.     "PRIMARY_SCHOOL",
10.     "GENERAL_AUTO_REPAIR_SERVICE_CENTER"
11.   ]
12. }
13. // 返回周边搜索结果
14. try {
15.   const result = await site.nearbySearch(params);
16.   console.info(`Succeeded in searching nearby. result is ${JSON.stringify(result)}`);
17. } catch (error) {
18.   const err: BusinessError = error as BusinessError;
19.   console.error(`Failed in searching nearby. Code is ${err.code}, message is ${err.message}`);
20. }

### 自动补全

根据输入的关键字，将最有可能的搜索词呈现给用户，以减少用户输入信息，提升用户体验。如：输入“北京”，提示“北京市”、“北京站”、“北京西站”等。

1. let params: site.QueryAutoCompleteParams = {
2.   // 自定义关键字
3.   query: "hotel",
4.   // 经纬度坐标
5.   location: {
6.     latitude: 31.984410259206815,
7.     longitude: 118.76625379397866
8.   },
9.   language: "en",
10.   // 返回子节点
11.   isChildren: true
12. };
13. // 返回自动补全结果
14. try {
15.   const result = await site.queryAutoComplete(params);
16.   console.info(`Succeeded in querying. result is ${JSON.stringify(result)}`);
17. } catch (error) {
18.   const err: BusinessError = error as BusinessError;
19.   console.error(`Failed in querying. Code is ${err.code}, message is ${err.message}`);
20. }

### 地点详情

根据地点的唯一主键地点ID（siteId）获取地点详情。地点详细信息请求返回有关指定地点的更全面的信息，如地点名称、地址详细信息、经纬度等。siteId可通过其他接口（关键字搜索、周边搜索、地点详情、自动补全、正地理编码）的返回结果中获取。

1. let params: site.SearchByIdParams = {
2.   // 指定主键地点ID
3.   siteId: "144129739873977856",
4.   language: "en",
5.   // 返回子节点
6.   isChildren: true
7. };
8. // 返回地点详情结果
9. try {
10.   const result = await site.searchById(params);
11.   console.info(`Succeeded in searching. result is ${JSON.stringify(result)}`);
12. } catch (error) {
13.   const err: BusinessError = error as BusinessError;
14.   console.error(`Failed in searching. Code is ${err.code}, message is ${err.message}`);
15. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-location-services "位置搜索")
# POI搜索

更新时间: 2025-12-16 16:36

## 场景介绍

提供多种查询POI信息的能力：

- 关键字搜索：通过用户输入的关键字，返回地点列表。
- 周边搜索：基于用户设备位置进行地点查找。
- 自动补全：根据输入的关键字返回预测的输入关键字和地点查询建议。
- 地点详情：查询某个地点更详细的信息。

## 接口说明

以下是POI搜索相关接口，主要由[site](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site)命名空间下的方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site)。

|接口名|描述|
|:--|:--|
|[searchByText](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section1117619561413)(searchByTextParams: [SearchByTextParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section186305710274)): Promise<[SearchByTextResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section55651334123013)>|关键字搜索。|
|[searchByText](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section142981754612)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), searchByTextParams: [SearchByTextParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section186305710274)): Promise<[SearchByTextResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section55651334123013)>|关键字搜索。支持上传Context上下文。|
|[nearbySearch](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section6315894393)(nearbySearchParams: [NearbySearchParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section1963813341280)): Promise<[NearbySearchResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section15617144513016)>|周边搜索。|
|[nearbySearch](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section4478173620711)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), nearbySearchParams: [NearbySearchParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section1963813341280)): Promise<[NearbySearchResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section15617144513016)>|周边搜索。支持上传Context上下文。|
|[queryAutoComplete](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section20324320183912)(queryAutoCompleteParams: [QueryAutoCompleteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section18371146292)): Promise<[QueryAutoCompleteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section81901456163020)>|自动补全。|
|[queryAutoComplete](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section1095410462267)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), queryAutoCompleteParams: [QueryAutoCompleteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section18371146292)): Promise<[QueryAutoCompleteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section81901456163020)>|自动补全。支持上传Context上下文。|
|[searchById](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section17490031173910)(searchByIdParams: [SearchByIdParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section756019297292)): Promise<[SearchByIdResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section9671461314)>|地点详情。|
|[searchById](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section192881428123313)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), searchByIdParams: [SearchByIdParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section756019297292)): Promise<[SearchByIdResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-site#section9671461314)>|地点详情。支持上传Context上下文。|

## 开发步骤

导入相关模块。

1. import { site } from '@kit.MapKit';
2. import { BusinessError } from '@kit.BasicServicesKit';

### 关键字搜索

通过指定的关键字和可选的地理范围，查询诸如旅游景点、企业和学校之类的地点。

1. let params: site.SearchByTextParams = {
2.   // 根据自定义关键字进行搜索，例如：“故宫”、“夫子庙”
3.   query: "Piazzale Dante, 41, 55049 Viareggio, Tuscany, Italy",
4.   // 经纬度坐标
5.   location: {
6.     latitude: 31.984,
7.     longitude: 118.76625
8.   },
9.   // 指定地理位置的范围半径
10.   radius: 10000,
11.   // 搜索结果的语言类型
12.   language: "en"
13. };
14. // 返回关键字搜索结果
15. try {
16.   const result = await site.searchByText(params);
17.   console.info(`Succeeded in searching by text. result is ${JSON.stringify(result)}`);
18. } catch (error) {
19.   const err: BusinessError = error as BusinessError;
20.   console.error(`Failed in searching by text. Code is ${err.code}, message is ${err.message}`);
21. }

### 周边搜索

通过用户传入自己的位置，可以返回周边地点列表。您可以通过提供关键字或指定要搜索的地点的类型来优化搜索结果。

1. let params: site.NearbySearchParams = {
2.   location: {
3.     latitude:51.50811219132287,
4.     longitude:-0.07594896472392065
5.   },
6.   poiTypes: [
7.     "Watch_Store",
8.     "SUBWAY",
9.     "PRIMARY_SCHOOL",
10.     "GENERAL_AUTO_REPAIR_SERVICE_CENTER"
11.   ]
12. }
13. // 返回周边搜索结果
14. try {
15.   const result = await site.nearbySearch(params);
16.   console.info(`Succeeded in searching nearby. result is ${JSON.stringify(result)}`);
17. } catch (error) {
18.   const err: BusinessError = error as BusinessError;
19.   console.error(`Failed in searching nearby. Code is ${err.code}, message is ${err.message}`);
20. }

### 自动补全

根据输入的关键字，将最有可能的搜索词呈现给用户，以减少用户输入信息，提升用户体验。如：输入“北京”，提示“北京市”、“北京站”、“北京西站”等。

1. let params: site.QueryAutoCompleteParams = {
2.   // 自定义关键字
3.   query: "hotel",
4.   // 经纬度坐标
5.   location: {
6.     latitude: 31.984410259206815,
7.     longitude: 118.76625379397866
8.   },
9.   language: "en",
10.   // 返回子节点
11.   isChildren: true
12. };
13. // 返回自动补全结果
14. try {
15.   const result = await site.queryAutoComplete(params);
16.   console.info(`Succeeded in querying. result is ${JSON.stringify(result)}`);
17. } catch (error) {
18.   const err: BusinessError = error as BusinessError;
19.   console.error(`Failed in querying. Code is ${err.code}, message is ${err.message}`);
20. }

### 地点详情

根据地点的唯一主键地点ID（siteId）获取地点详情。地点详细信息请求返回有关指定地点的更全面的信息，如地点名称、地址详细信息、经纬度等。siteId可通过其他接口（关键字搜索、周边搜索、地点详情、自动补全、正地理编码）的返回结果中获取。

1. let params: site.SearchByIdParams = {
2.   // 指定主键地点ID
3.   siteId: "144129739873977856",
4.   language: "en",
5.   // 返回子节点
6.   isChildren: true
7. };
8. // 返回地点详情结果
9. try {
10.   const result = await site.searchById(params);
11.   console.info(`Succeeded in searching. result is ${JSON.stringify(result)}`);
12. } catch (error) {
13.   const err: BusinessError = error as BusinessError;
14.   console.error(`Failed in searching. Code is ${err.code}, message is ${err.message}`);
15. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-location-services "位置搜索")
# 出行路线规划

更新时间: 2025-12-16 16:36

## 场景介绍

从5.1.1(19)开始，支持公共交通规划功能。

提供两点之间驾车、步行、骑行和公共交通的路径规划能力。其中驾车路径规划支持添加途经点。

## 接口说明

以下是路径规划功能相关接口，主要由[navi](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api)命名空间下的方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api)。

|接口名|描述|
|:--|:--|
|[getDrivingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section15371229153110)(params: [DrivingRouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section1345541155712)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|驾车路径规划。|
|[getDrivingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section89883616310)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), params: [DrivingRouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section1345541155712)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|驾车路径规划。支持传入Context上下文。|
|[getWalkingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section18808624125913)(params: [RouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section17987175793914)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|步行路径规划。|
|[getWalkingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section20859185187)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), params: [RouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section17987175793914)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|步行路径规划。支持传入Context上下文。|
|[getCyclingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section151981115506)(params: [RouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section17987175793914)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|骑行路径规划。|
|[getCyclingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section6187385125)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), params: [RouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section17987175793914)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|骑行路径规划。支持传入Context上下文。|
|[getTransitRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section5970105744912)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), params: [TransitRouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section54957561312)): Promise<[TransitRouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section7752185614207)>|公共交通规划。支持传入Context上下文。|
|[DrivingRouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section1345541155712)|驾车路径规划的参数。|
|[RouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section17987175793914)|步行、骑行路径规划的参数。|
|[TransitRouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section54957561312)|公共交通规划的参数。|
|[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)|路径规划的结果。|
|[TransitRouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section7752185614207)|公共交通规划的结果。|

## 开发步骤

导入相关模块。

1. import { navi } from '@kit.MapKit';
2. import { BusinessError } from '@kit.BasicServicesKit';

### 驾车路径规划

根据起终点坐标检索符合条件的驾车路径规划方案。支持以下功能：

- 支持一次请求返回多条路线，最多支持3条路线。
- 最多支持5个途经点。
- 支持未来出行规划。
- 支持根据实时路况进行合理路线规划。
- 支持多种路线偏好选择，如时间最短、避免经过收费的公路、避开高速公路、距离优先等。

1. async testDrivingRoutes() {
2.   let params: navi.DrivingRouteParams = {
3.     // 起点的经纬度
4.     origins: [{
5.       latitude: 31.982129213545843,
6.       longitude: 120.27745557768591
7.     }],
8.     // 终点的经纬度
9.     destination: {
10.       latitude: 31.986129213545843,
11.       longitude: 120.32745557768591
12.     },
13.     // 路径的途经点
14.     waypoints: [{
15.       latitude: 31.967236140819114,
16.       longitude: 120.27142088866847
17.     }, {
18.       latitude: 31.972868002238872,
19.       longitude: 120.2943211817165
20.     }, {
21.       latitude: 31.98469327973332,
22.       longitude: 120.29101107384068
23.     }],
24.     language: 'zh_CN'
25.   };
26.   try {
27.     const result = await navi.getDrivingRoutes(params);
28.     console.info(`Succeeded in getting driving routes. result is ${JSON.stringify(result)}`);
29.   } catch (error) {
30.     const err: BusinessError = error as BusinessError;
31.     console.error(`Failed in getting driving routes. Code is ${err.code}, message is ${err.message}`);
32.   }
33. }

### 步行路径规划

根据起终点坐标检索符合条件的步行路径规划方案。支持以下功能：

- 支持直线距离150km以内的步行路径规划能力。
- 融入出行策略（时间最短、避免轮渡）。

1. async testWalkingRoutes() {
2.   let params: navi.RouteParams = {
3.     // 起点的经纬度
4.     origins: [{
5.       latitude: 39.992281,
6.       longitude: 116.31088
7.     }, { 
8.       latitude: 39.996,
9.       longitude: 116.311 
10.     }],
11.     // 终点的经纬度
12.     destination: { 
13.       latitude: 39.94,
14.       longitude: 116.311 
15.     },
16.     language: 'zh_CN'
17.   };
18.   try {
19.     const result = await navi.getWalkingRoutes(params);
20.     console.info(`Succeeded in getting walking routes. result is ${JSON.stringify(result)}`);
21.   } catch (error) {
22.     const err: BusinessError = error as BusinessError;
23.     console.error(`Failed in getting walking routes. Code is ${err.code}, message is ${err.message}`);
24.   }
25. }

### 骑行路径规划

根据起终点坐标检索符合条件的骑行路径规划方案。支持以下功能：

- 支持直线距离500km以内的骑行路径规划能力。
- 融入出行策略（时间最短、避免轮渡）。

1. async testCyclingRoutes() {
2.   let params: navi.RouteParams = {
3.     // 起点的经纬度
4.     origins: [{ 
5.       latitude: 31.9844102,
6.       longitude: 118.7662537
7.     }],
8.     // 终点的经纬度
9.     destination: { 
10.       latitude: 31.9874102,
11.       longitude: 118.7362537
12.     },
13.     language: 'zh_CN'
14.   };
15.   try {
16.     const result = await navi.getCyclingRoutes(params);
17.     console.info(`Succeeded in getting cycling routes. result is ${JSON.stringify(result)}`);
18.   } catch (error) {
19.     const err: BusinessError = error as BusinessError;
20.     console.error(`Failed in getting cycling routes. Code is ${err.code}, message is ${err.message}`);
21.   }
22. }

### 公共交通规划

根据起点终点坐标规划道路，从而返回两地之间的多种公共交通中转路线，仅支持中国大陆。

1. async testGetTransitRoutes() {
2.   let params: navi.TransitRouteParams = {
3.     // 起点经纬度
4.     origin: { 
5.       latitude: 39.921619,
6.       longitude: 116.356587 
7.     },
8.     // 终点经纬度
9.     destination: {
10.       latitude: 39.94161,
11.       longitude: 116.353621 
12.     },
13.     // 预计出发时间
14.     departureTime: new Date().getTime() / 1000
15.   };
16.   try {
17.     const result = await navi.getTransitRoutes(this.getUIContext().getHostContext(), params);
18.     console.info(`Succeeded in getting transit routes. result is ${JSON.stringify(result)}`);
19.   } catch (error) {
20.     const err: BusinessError = error as BusinessError;
21.     console.error(`Failed in getting transit routes. Code is ${err.code}, message is ${err.message}`);
22.   }
23. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-navi "路径规划")
# 出行路线规划

更新时间: 2025-12-16 16:36

## 场景介绍

从5.1.1(19)开始，支持公共交通规划功能。

提供两点之间驾车、步行、骑行和公共交通的路径规划能力。其中驾车路径规划支持添加途经点。

## 接口说明

以下是路径规划功能相关接口，主要由[navi](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api)命名空间下的方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api)。

|接口名|描述|
|:--|:--|
|[getDrivingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section15371229153110)(params: [DrivingRouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section1345541155712)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|驾车路径规划。|
|[getDrivingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section89883616310)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), params: [DrivingRouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section1345541155712)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|驾车路径规划。支持传入Context上下文。|
|[getWalkingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section18808624125913)(params: [RouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section17987175793914)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|步行路径规划。|
|[getWalkingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section20859185187)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), params: [RouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section17987175793914)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|步行路径规划。支持传入Context上下文。|
|[getCyclingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section151981115506)(params: [RouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section17987175793914)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|骑行路径规划。|
|[getCyclingRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section6187385125)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), params: [RouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section17987175793914)): Promise<[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)>|骑行路径规划。支持传入Context上下文。|
|[getTransitRoutes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section5970105744912)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), params: [TransitRouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section54957561312)): Promise<[TransitRouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section7752185614207)>|公共交通规划。支持传入Context上下文。|
|[DrivingRouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section1345541155712)|驾车路径规划的参数。|
|[RouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section17987175793914)|步行、骑行路径规划的参数。|
|[TransitRouteParams](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section54957561312)|公共交通规划的参数。|
|[RouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section14125152320374)|路径规划的结果。|
|[TransitRouteResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-navi-api#section7752185614207)|公共交通规划的结果。|

## 开发步骤

导入相关模块。

1. import { navi } from '@kit.MapKit';
2. import { BusinessError } from '@kit.BasicServicesKit';

### 驾车路径规划

根据起终点坐标检索符合条件的驾车路径规划方案。支持以下功能：

- 支持一次请求返回多条路线，最多支持3条路线。
- 最多支持5个途经点。
- 支持未来出行规划。
- 支持根据实时路况进行合理路线规划。
- 支持多种路线偏好选择，如时间最短、避免经过收费的公路、避开高速公路、距离优先等。

1. async testDrivingRoutes() {
2.   let params: navi.DrivingRouteParams = {
3.     // 起点的经纬度
4.     origins: [{
5.       latitude: 31.982129213545843,
6.       longitude: 120.27745557768591
7.     }],
8.     // 终点的经纬度
9.     destination: {
10.       latitude: 31.986129213545843,
11.       longitude: 120.32745557768591
12.     },
13.     // 路径的途经点
14.     waypoints: [{
15.       latitude: 31.967236140819114,
16.       longitude: 120.27142088866847
17.     }, {
18.       latitude: 31.972868002238872,
19.       longitude: 120.2943211817165
20.     }, {
21.       latitude: 31.98469327973332,
22.       longitude: 120.29101107384068
23.     }],
24.     language: 'zh_CN'
25.   };
26.   try {
27.     const result = await navi.getDrivingRoutes(params);
28.     console.info(`Succeeded in getting driving routes. result is ${JSON.stringify(result)}`);
29.   } catch (error) {
30.     const err: BusinessError = error as BusinessError;
31.     console.error(`Failed in getting driving routes. Code is ${err.code}, message is ${err.message}`);
32.   }
33. }

### 步行路径规划

根据起终点坐标检索符合条件的步行路径规划方案。支持以下功能：

- 支持直线距离150km以内的步行路径规划能力。
- 融入出行策略（时间最短、避免轮渡）。

1. async testWalkingRoutes() {
2.   let params: navi.RouteParams = {
3.     // 起点的经纬度
4.     origins: [{
5.       latitude: 39.992281,
6.       longitude: 116.31088
7.     }, { 
8.       latitude: 39.996,
9.       longitude: 116.311 
10.     }],
11.     // 终点的经纬度
12.     destination: { 
13.       latitude: 39.94,
14.       longitude: 116.311 
15.     },
16.     language: 'zh_CN'
17.   };
18.   try {
19.     const result = await navi.getWalkingRoutes(params);
20.     console.info(`Succeeded in getting walking routes. result is ${JSON.stringify(result)}`);
21.   } catch (error) {
22.     const err: BusinessError = error as BusinessError;
23.     console.error(`Failed in getting walking routes. Code is ${err.code}, message is ${err.message}`);
24.   }
25. }

### 骑行路径规划

根据起终点坐标检索符合条件的骑行路径规划方案。支持以下功能：

- 支持直线距离500km以内的骑行路径规划能力。
- 融入出行策略（时间最短、避免轮渡）。

1. async testCyclingRoutes() {
2.   let params: navi.RouteParams = {
3.     // 起点的经纬度
4.     origins: [{ 
5.       latitude: 31.9844102,
6.       longitude: 118.7662537
7.     }],
8.     // 终点的经纬度
9.     destination: { 
10.       latitude: 31.9874102,
11.       longitude: 118.7362537
12.     },
13.     language: 'zh_CN'
14.   };
15.   try {
16.     const result = await navi.getCyclingRoutes(params);
17.     console.info(`Succeeded in getting cycling routes. result is ${JSON.stringify(result)}`);
18.   } catch (error) {
19.     const err: BusinessError = error as BusinessError;
20.     console.error(`Failed in getting cycling routes. Code is ${err.code}, message is ${err.message}`);
21.   }
22. }

### 公共交通规划

根据起点终点坐标规划道路，从而返回两地之间的多种公共交通中转路线，仅支持中国大陆。

1. async testGetTransitRoutes() {
2.   let params: navi.TransitRouteParams = {
3.     // 起点经纬度
4.     origin: { 
5.       latitude: 39.921619,
6.       longitude: 116.356587 
7.     },
8.     // 终点经纬度
9.     destination: {
10.       latitude: 39.94161,
11.       longitude: 116.353621 
12.     },
13.     // 预计出发时间
14.     departureTime: new Date().getTime() / 1000
15.   };
16.   try {
17.     const result = await navi.getTransitRoutes(this.getUIContext().getHostContext(), params);
18.     console.info(`Succeeded in getting transit routes. result is ${JSON.stringify(result)}`);
19.   } catch (error) {
20.     const err: BusinessError = error as BusinessError;
21.     console.error(`Failed in getting transit routes. Code is ${err.code}, message is ${err.message}`);
22.   }
23. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-navi "路径规划")
# 静态图

更新时间: 2025-12-16 16:36

## 场景介绍

本章节将向您介绍如何使用静态图功能。静态图功能会返回一张地图图片，您可以将地图以图片形式嵌入自己的应用/元服务中。在使用时，您可以指定请求的地图位置、图片大小。

**图1** 静态图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163626.69872037083296610074711748168427:50001231000000:2800:E366A139DC9323523EC1653B94B583C5B66B9ABE349E127EF2744B900A1D35CA.png "点击放大")

## 接口说明

以下是地图静态图相关接口，获取静态图功能主要由[staticMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap)命名空间下的方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap)。

|接口名|描述|
|:--|:--|
|[StaticMapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1555293218278)|用于描述静态图属性。|
|[getMapImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1117619561413)(options: [StaticMapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1555293218278)): Promise<[image.PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)>|根据提供的参数创建静态图。|
|[getMapImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1068516421577)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), options: [StaticMapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1555293218278)): Promise<[image.PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)>|根据提供的参数创建静态图。支持上传Context上下文。|

## 开发步骤

1. 导入相关模块。
    
    1. import { staticMap } from '@kit.MapKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 创建静态图初始化参数，调用[getMapImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1117619561413)方法获取静态图，效果如下图。
    
    1. @Entry
    2. @Component
    3. struct StaticMapDemo {
    4.   @State image?: PixelMap = undefined;
    
    5.   build() {
    6.     Column() {
    7.       this.buildDemoUI();
    8.     }.width('100%')
    9.     .margin({ bottom: 48 })
    10.     .backgroundColor(0xf2f2f2)
    11.     .height('100%')
    12.   }
    
    13.   @Builder
    14.   buildDemoUI() {
    15.     // 展示获取的静态图
    16.     Image(this.image)
    17.       .width('100%')
    18.       .fitOriginalSize(false)
    19.       .border({ width: 1 })
    20.       .borderStyle(BorderStyle.Dashed)
    21.       .objectFit(ImageFit.Contain)
    22.       .height("90%")
    
    23.     Row() {
    24.       Button("getStaticMap")
    25.         .fontSize(12)
    26.         .onClick(async () => {
    27.           // 设置静态图标记参数
    28.           let markers: Array<staticMap.StaticMapMarker> = [{
    29.             location: {
    30.               latitude: 50,
    31.               longitude: 126.3
    32.             },
    33.             font: 'statics',
    34.             defaultIconSize: staticMap.IconSize.TINY
    35.           }];
    
    36.           // 设置静态图绘制路径参数
    37.           let path: staticMap.StaticMapPath = {
    38.             locations: [
    39.               {
    40.                 latitude: 50,
    41.                 longitude: 126
    42.               },
    43.               {
    44.                 latitude: 50.3,
    45.                 longitude: 126
    46.               },
    47.               {
    48.                 latitude: 50.3,
    49.                 longitude: 126.3
    50.               },
    51.               {
    52.                 latitude: 49.7,
    53.                 longitude: 126
    54.               },
    55.               {
    56.                 latitude: 50,
    57.                 longitude: 126
    58.               }
    59.             ],
    60.             width: 3
    61.           };
    
    62.           // 拼装静态图参数
    63.           let option: staticMap.StaticMapOptions = {
    64.             location: {
    65.               latitude: 50,
    66.               longitude: 126
    67.             },
    68.             zoom: 10,
    69.             imageWidth: 1024,
    70.             imageHeight: 1024,
    71.             scale: 1,
    72.             markers: markers,
    73.             path: path
    74.           };
    
    75.           try {
    76.             // 获取静态图
    77.             this.image = await staticMap.getMapImage(option);
    78.             console.info("Succeeded in getting image.");
    79.           } catch (error) {
    80.             const err: BusinessError = error as BusinessError;
    81.             console.error(`Failed in getting image, code: ${err.code}, message: ${err.message}`);
    82.           }
    83.         })
    84.     }.margin({ top: 12 })
    85.   }
    86. }
    
    **图2** 调用getMapImage方法获取静态图  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163626.20379873704880173875496221736813:50001231000000:2800:9C832D1B3C0139D1377E692C1180C203A61CBB0A4DAF87DBA9FF592B755F470D.png "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-navi-snap "轨迹绑路")
# 静态图

更新时间: 2025-12-16 16:36

## 场景介绍

本章节将向您介绍如何使用静态图功能。静态图功能会返回一张地图图片，您可以将地图以图片形式嵌入自己的应用/元服务中。在使用时，您可以指定请求的地图位置、图片大小。

**图1** 静态图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163626.69872037083296610074711748168427:50001231000000:2800:E366A139DC9323523EC1653B94B583C5B66B9ABE349E127EF2744B900A1D35CA.png "点击放大")

## 接口说明

以下是地图静态图相关接口，获取静态图功能主要由[staticMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap)命名空间下的方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap)。

|接口名|描述|
|:--|:--|
|[StaticMapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1555293218278)|用于描述静态图属性。|
|[getMapImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1117619561413)(options: [StaticMapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1555293218278)): Promise<[image.PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)>|根据提供的参数创建静态图。|
|[getMapImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1068516421577)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), options: [StaticMapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1555293218278)): Promise<[image.PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)>|根据提供的参数创建静态图。支持上传Context上下文。|

## 开发步骤

1. 导入相关模块。
    
    1. import { staticMap } from '@kit.MapKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 创建静态图初始化参数，调用[getMapImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1117619561413)方法获取静态图，效果如下图。
    
    1. @Entry
    2. @Component
    3. struct StaticMapDemo {
    4.   @State image?: PixelMap = undefined;
    
    5.   build() {
    6.     Column() {
    7.       this.buildDemoUI();
    8.     }.width('100%')
    9.     .margin({ bottom: 48 })
    10.     .backgroundColor(0xf2f2f2)
    11.     .height('100%')
    12.   }
    
    13.   @Builder
    14.   buildDemoUI() {
    15.     // 展示获取的静态图
    16.     Image(this.image)
    17.       .width('100%')
    18.       .fitOriginalSize(false)
    19.       .border({ width: 1 })
    20.       .borderStyle(BorderStyle.Dashed)
    21.       .objectFit(ImageFit.Contain)
    22.       .height("90%")
    
    23.     Row() {
    24.       Button("getStaticMap")
    25.         .fontSize(12)
    26.         .onClick(async () => {
    27.           // 设置静态图标记参数
    28.           let markers: Array<staticMap.StaticMapMarker> = [{
    29.             location: {
    30.               latitude: 50,
    31.               longitude: 126.3
    32.             },
    33.             font: 'statics',
    34.             defaultIconSize: staticMap.IconSize.TINY
    35.           }];
    
    36.           // 设置静态图绘制路径参数
    37.           let path: staticMap.StaticMapPath = {
    38.             locations: [
    39.               {
    40.                 latitude: 50,
    41.                 longitude: 126
    42.               },
    43.               {
    44.                 latitude: 50.3,
    45.                 longitude: 126
    46.               },
    47.               {
    48.                 latitude: 50.3,
    49.                 longitude: 126.3
    50.               },
    51.               {
    52.                 latitude: 49.7,
    53.                 longitude: 126
    54.               },
    55.               {
    56.                 latitude: 50,
    57.                 longitude: 126
    58.               }
    59.             ],
    60.             width: 3
    61.           };
    
    62.           // 拼装静态图参数
    63.           let option: staticMap.StaticMapOptions = {
    64.             location: {
    65.               latitude: 50,
    66.               longitude: 126
    67.             },
    68.             zoom: 10,
    69.             imageWidth: 1024,
    70.             imageHeight: 1024,
    71.             scale: 1,
    72.             markers: markers,
    73.             path: path
    74.           };
    
    75.           try {
    76.             // 获取静态图
    77.             this.image = await staticMap.getMapImage(option);
    78.             console.info("Succeeded in getting image.");
    79.           } catch (error) {
    80.             const err: BusinessError = error as BusinessError;
    81.             console.error(`Failed in getting image, code: ${err.code}, message: ${err.message}`);
    82.           }
    83.         })
    84.     }.margin({ top: 12 })
    85.   }
    86. }
    
    **图2** 调用getMapImage方法获取静态图  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163626.20379873704880173875496221736813:50001231000000:2800:9C832D1B3C0139D1377E692C1180C203A61CBB0A4DAF87DBA9FF592B755F470D.png "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-navi-snap "轨迹绑路")
# 静态图

更新时间: 2025-12-16 16:36

## 场景介绍

本章节将向您介绍如何使用静态图功能。静态图功能会返回一张地图图片，您可以将地图以图片形式嵌入自己的应用/元服务中。在使用时，您可以指定请求的地图位置、图片大小。

**图1** 静态图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163626.69872037083296610074711748168427:50001231000000:2800:E366A139DC9323523EC1653B94B583C5B66B9ABE349E127EF2744B900A1D35CA.png "点击放大")

## 接口说明

以下是地图静态图相关接口，获取静态图功能主要由[staticMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap)命名空间下的方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap)。

|接口名|描述|
|:--|:--|
|[StaticMapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1555293218278)|用于描述静态图属性。|
|[getMapImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1117619561413)(options: [StaticMapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1555293218278)): Promise<[image.PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)>|根据提供的参数创建静态图。|
|[getMapImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1068516421577)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), options: [StaticMapOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1555293218278)): Promise<[image.PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)>|根据提供的参数创建静态图。支持上传Context上下文。|

## 开发步骤

1. 导入相关模块。
    
    1. import { staticMap } from '@kit.MapKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 创建静态图初始化参数，调用[getMapImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-staticmap#section1117619561413)方法获取静态图，效果如下图。
    
    1. @Entry
    2. @Component
    3. struct StaticMapDemo {
    4.   @State image?: PixelMap = undefined;
    
    5.   build() {
    6.     Column() {
    7.       this.buildDemoUI();
    8.     }.width('100%')
    9.     .margin({ bottom: 48 })
    10.     .backgroundColor(0xf2f2f2)
    11.     .height('100%')
    12.   }
    
    13.   @Builder
    14.   buildDemoUI() {
    15.     // 展示获取的静态图
    16.     Image(this.image)
    17.       .width('100%')
    18.       .fitOriginalSize(false)
    19.       .border({ width: 1 })
    20.       .borderStyle(BorderStyle.Dashed)
    21.       .objectFit(ImageFit.Contain)
    22.       .height("90%")
    
    23.     Row() {
    24.       Button("getStaticMap")
    25.         .fontSize(12)
    26.         .onClick(async () => {
    27.           // 设置静态图标记参数
    28.           let markers: Array<staticMap.StaticMapMarker> = [{
    29.             location: {
    30.               latitude: 50,
    31.               longitude: 126.3
    32.             },
    33.             font: 'statics',
    34.             defaultIconSize: staticMap.IconSize.TINY
    35.           }];
    
    36.           // 设置静态图绘制路径参数
    37.           let path: staticMap.StaticMapPath = {
    38.             locations: [
    39.               {
    40.                 latitude: 50,
    41.                 longitude: 126
    42.               },
    43.               {
    44.                 latitude: 50.3,
    45.                 longitude: 126
    46.               },
    47.               {
    48.                 latitude: 50.3,
    49.                 longitude: 126.3
    50.               },
    51.               {
    52.                 latitude: 49.7,
    53.                 longitude: 126
    54.               },
    55.               {
    56.                 latitude: 50,
    57.                 longitude: 126
    58.               }
    59.             ],
    60.             width: 3
    61.           };
    
    62.           // 拼装静态图参数
    63.           let option: staticMap.StaticMapOptions = {
    64.             location: {
    65.               latitude: 50,
    66.               longitude: 126
    67.             },
    68.             zoom: 10,
    69.             imageWidth: 1024,
    70.             imageHeight: 1024,
    71.             scale: 1,
    72.             markers: markers,
    73.             path: path
    74.           };
    
    75.           try {
    76.             // 获取静态图
    77.             this.image = await staticMap.getMapImage(option);
    78.             console.info("Succeeded in getting image.");
    79.           } catch (error) {
    80.             const err: BusinessError = error as BusinessError;
    81.             console.error(`Failed in getting image, code: ${err.code}, message: ${err.message}`);
    82.           }
    83.         })
    84.     }.margin({ top: 12 })
    85.   }
    86. }
    
    **图2** 调用getMapImage方法获取静态图  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163626.20379873704880173875496221736813:50001231000000:2800:9C832D1B3C0139D1377E692C1180C203A61CBB0A4DAF87DBA9FF592B755F470D.png "点击放大")
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-navi-snap "轨迹绑路")
# 区划选择

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将介绍如何集成区划选择控件。该控件不支持在智能表设备中调用。

区划选择控件可加载全球或指定国家的区划信息，支持以树状结构化选择，支持功能：

- 支持查看选中区划的下级区划。
- 支持推荐热门区划。
- 支持子窗拉起区划控件，适合宽屏设备使用。

|   |   |
|---|---|
|**图1** 选择国家  <br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.76530906541531190549335412037436:50001231000000:2800:BED684F2D1A36E8B05E9C10A44590B8E09FEA0B1269B6B99D589528DF41EB4D1.png "点击放大")|**图2** 选择省市<br><br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.04995116294825329983954356690406:50001231000000:2800:87000C481D601B3255A34330731C3D2BAA810B2B46325D4CA88425BA9DE8BDDF.png "点击放大")|
|**图3** 子窗拉起区划控件<br><br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.01158823156850416948869453147510:50001231000000:2800:532C3B915CE45F418275F183AB2CCAB5E5ABB73ED853C2546B1AEB8FF5831903.png "点击放大")||

## 约束与限制

使用该功能需满足以下条件：

- 仅支持手机、平板和2in1设备。

## 接口说明

区划选择控件功能主要由[sceneMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap)命名空间下的[selectDistrict](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section1567213912302)方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap)。

|接口名|描述|
|:--|:--|
|[DistrictSelectOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section17211958161110)|区划选择页面初始选项。|
|[selectDistrict](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section1567213912302)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), options: [DistrictSelectOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section17211958161110)): Promise<[DistrictSelectResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section3745121172118)>|调出区划选择页面。|
|[DistrictSelectResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section3745121172118)|区划选择结果。|

## 开发步骤

1. 导入相关模块。
    
    1. import { sceneMap } from '@kit.MapKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 创建区划选择请求参数，调用[selectDistrict](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section1567213912302)方法拉起区划选择页。
    
    1. let districtSelectOptions: sceneMap.DistrictSelectOptions = {
    2.   countryCode: "CN",
    3.   // 使用子窗拉起方式
    4.   subWindowEnabled: true
    5. };
    6. // 拉起区划选择页
    7. sceneMap.selectDistrict(this.getUIContext().getHostContext(), districtSelectOptions).then((data) => {
    8.   console.info("SelectDistrict", "Succeeded in selecting district.");
    9. }).catch((err: BusinessError) => {
    10.   console.error("SelectDistrict", `Failed to select district, code: ${err.code}, message: ${err.message}`);
    11. });
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-location-selecting "地点选取")
# 区划选择

更新时间: 2025-12-16 16:37

## 场景介绍

本章节将介绍如何集成区划选择控件。该控件不支持在智能表设备中调用。

区划选择控件可加载全球或指定国家的区划信息，支持以树状结构化选择，支持功能：

- 支持查看选中区划的下级区划。
- 支持推荐热门区划。
- 支持子窗拉起区划控件，适合宽屏设备使用。

|   |   |
|---|---|
|**图1** 选择国家  <br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.76530906541531190549335412037436:50001231000000:2800:BED684F2D1A36E8B05E9C10A44590B8E09FEA0B1269B6B99D589528DF41EB4D1.png "点击放大")|**图2** 选择省市<br><br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.04995116294825329983954356690406:50001231000000:2800:87000C481D601B3255A34330731C3D2BAA810B2B46325D4CA88425BA9DE8BDDF.png "点击放大")|
|**图3** 子窗拉起区划控件<br><br>![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.01158823156850416948869453147510:50001231000000:2800:532C3B915CE45F418275F183AB2CCAB5E5ABB73ED853C2546B1AEB8FF5831903.png "点击放大")||

## 约束与限制

使用该功能需满足以下条件：

- 仅支持手机、平板和2in1设备。

## 接口说明

区划选择控件功能主要由[sceneMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap)命名空间下的[selectDistrict](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section1567213912302)方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap)。

|接口名|描述|
|:--|:--|
|[DistrictSelectOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section17211958161110)|区划选择页面初始选项。|
|[selectDistrict](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section1567213912302)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), options: [DistrictSelectOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section17211958161110)): Promise<[DistrictSelectResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section3745121172118)>|调出区划选择页面。|
|[DistrictSelectResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section3745121172118)|区划选择结果。|

## 开发步骤

1. 导入相关模块。
    
    1. import { sceneMap } from '@kit.MapKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 创建区划选择请求参数，调用[selectDistrict](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-scenemap#section1567213912302)方法拉起区划选择页。
    
    1. let districtSelectOptions: sceneMap.DistrictSelectOptions = {
    2.   countryCode: "CN",
    3.   // 使用子窗拉起方式
    4.   subWindowEnabled: true
    5. };
    6. // 拉起区划选择页
    7. sceneMap.selectDistrict(this.getUIContext().getHostContext(), districtSelectOptions).then((data) => {
    8.   console.info("SelectDistrict", "Succeeded in selecting district.");
    9. }).catch((err: BusinessError) => {
    10.   console.error("SelectDistrict", `Failed to select district, code: ${err.code}, message: ${err.message}`);
    11. });
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-location-selecting "地点选取")
# 坐标纠偏

更新时间: 2025-12-16 16:36

## 坐标系知识介绍

华为地图涉及2种坐标系：

- WGS84：一种大地坐标系，也是目前广泛使用的GPS全球卫星定位系统使用的坐标系。
- GCJ02：由中国国家测绘局制订的地理信息系统的坐标系统，是由WGS84坐标系经过加密后的坐标系。

## 华为地图使用的坐标类型

中国大陆使用GCJ02坐标系，中国台湾和海外使用WGS84坐标系。

## 场景介绍

华为地图在中国大陆使用GCJ02坐标系，若使用WGS84坐标系直接叠加在华为地图上，因坐标值不同，展示位置会有偏移。所以，在中国大陆如果使用WGS84坐标调用Map Kit服务，需要先将其转换为GCJ02坐标系再访问。

## 接口说明

以下是坐标纠偏功能相关接口，主要由[map](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map)命名空间下的[convertCoordinateSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-convertcoordinatesync)、[rectifyCoordinate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-rectifycoordinate)方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-convertcoordinatesync)。

|接口名|描述|
|:--|:--|
|[mapCommon.CoordinateType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section78948324526)|坐标系类型。|
|[convertCoordinateSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-convertcoordinatesync)(fromType: [mapCommon.CoordinateType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section78948324526), toType: [mapCommon.CoordinateType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section78948324526), location: [mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810)): [mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810)|坐标转换，将WGS84坐标系转换为GCJ02坐标系。|
|[rectifyCoordinate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-rectifycoordinate)(context: [common.Context](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-application-context), locations: Array<[mapCommon.CoordinateLatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section196281647173615)>): Promise<Array<[mapCommon.CoordinateLatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section196281647173615)>>|坐标纠偏。|
|[mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810)|经纬度对象。|

## 开发步骤

导入相关模块。

1. import { map, mapCommon } from '@kit.MapKit';

### 坐标纠偏

[rectifyCoordinate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-rectifycoordinate)接口根据用户输入的坐标系和坐标以及获取当前的路由地，判断是否需要修正坐标。如果需要修正，则返回修正后的坐标系和坐标。

说明

- [rectifyCoordinate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-rectifycoordinate)接口仅为解决原始坐标与华为地图展示偏转的问题。
- [rectifyCoordinate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-rectifycoordinate)接口仅支持WGS84坐标系转为GCJ02坐标系。

1. let locations: Array<mapCommon.CoordinateLatLng> = [
2.   {
3.     // 输入香港坐标和WGS84坐标系，若当前地图站点使用GCJ02坐标系，返回GCJ02坐标系和转换后的香港坐标（输入的坐标转换为GCJ02坐标系）
4.     coordinateType: mapCommon.CoordinateType.WGS84,
5.     location: {
6.       latitude: 22.280556,
7.       longitude: 114.984000
8.     }
9.   }
10. ];
11. // 包含await的外层方法需要添加async关键字
12. let arr: Array<mapCommon.CoordinateLatLng> = await map.rectifyCoordinate(this.getUIContext().getHostContext(), locations);

### 坐标转换

初始化需要转换的坐标，调用[convertCoordinateSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-convertcoordinatesync)方法转换坐标。

1. let wgs84Position: mapCommon.LatLng = {
2.   latitude: 30,
3.   longitude: 118
4. };
5. // 转换经纬度坐标
6. let gcj02Position: mapCommon.LatLng =
7.   map.convertCoordinateSync(mapCommon.CoordinateType.WGS84, mapCommon.CoordinateType.GCJ02, wgs84Position);

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-calculation-tool "地图计算工具")
# 距离计算

更新时间: 2025-12-16 16:36

## 场景介绍

根据用户指定的两个经纬度坐标点，计算这两个点间的直线距离，单位为米。

## 接口说明

以下是距离计算功能相关接口，主要由[map](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map)命名空间下的[calculateDistance](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)。

|接口名|描述|
|:--|:--|
|[mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810)|经纬度对象。|
|[calculateDistance](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)(from: [mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810), to: [mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810)): number|计算坐标点之间的距离。|

## 开发步骤

1. 导入相关模块。
    
    1. import { map, mapCommon } from '@kit.MapKit';
    
2. 初始化需要计算的坐标，调用[calculateDistance](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)方法计算距离。
    
    1. let fromLatLng: mapCommon.LatLng = {
    2.   latitude: 38,
    3.   longitude: 118
    4. };
    5. let toLatLng: mapCommon.LatLng = {
    6.   latitude: 39,
    7.   longitude: 119
    8. };
    
    9. let distance = map.calculateDistance(fromLatLng, toLatLng);
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-convert-coordinate "坐标纠偏")
# 距离计算

更新时间: 2025-12-16 16:36

## 场景介绍

根据用户指定的两个经纬度坐标点，计算这两个点间的直线距离，单位为米。

## 接口说明

以下是距离计算功能相关接口，主要由[map](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map)命名空间下的[calculateDistance](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)。

|接口名|描述|
|:--|:--|
|[mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810)|经纬度对象。|
|[calculateDistance](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)(from: [mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810), to: [mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810)): number|计算坐标点之间的距离。|

## 开发步骤

1. 导入相关模块。
    
    1. import { map, mapCommon } from '@kit.MapKit';
    
2. 初始化需要计算的坐标，调用[calculateDistance](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)方法计算距离。
    
    1. let fromLatLng: mapCommon.LatLng = {
    2.   latitude: 38,
    3.   longitude: 118
    4. };
    5. let toLatLng: mapCommon.LatLng = {
    6.   latitude: 39,
    7.   longitude: 119
    8. };
    
    9. let distance = map.calculateDistance(fromLatLng, toLatLng);
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-convert-coordinate "坐标纠偏")
# 距离计算

更新时间: 2025-12-16 16:36

## 场景介绍

根据用户指定的两个经纬度坐标点，计算这两个点间的直线距离，单位为米。

## 接口说明

以下是距离计算功能相关接口，主要由[map](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map)命名空间下的[calculateDistance](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)方法提供，更多接口及使用方法请参见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)。

|接口名|描述|
|:--|:--|
|[mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810)|经纬度对象。|
|[calculateDistance](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)(from: [mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810), to: [mapCommon.LatLng](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-common#section20691173773810)): number|计算坐标点之间的距离。|

## 开发步骤

1. 导入相关模块。
    
    1. import { map, mapCommon } from '@kit.MapKit';
    
2. 初始化需要计算的坐标，调用[calculateDistance](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-map-calculatedistance)方法计算距离。
    
    1. let fromLatLng: mapCommon.LatLng = {
    2.   latitude: 38,
    3.   longitude: 118
    4. };
    5. let toLatLng: mapCommon.LatLng = {
    6.   latitude: 39,
    7.   longitude: 119
    8. };
    
    9. let distance = map.calculateDistance(fromLatLng, toLatLng);
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-convert-coordinate "坐标纠偏")
# 手势卡顿或者不生效

更新时间: 2025-12-16 16:37

**现象描述**

地图页面操作手势卡顿或者不生效。

**可能原因**

1. 手势遮盖或者手势冲突。
    - 手势遮盖：地图组件的上层存在没有做手势穿透的组件。
    - 手势冲突：以Swiper容器组件中使用地图组件为例，Swiper容器组件和地图组件手势会存在冲突。
2. 主线程阻塞。
    
    应用主线程处理大批量逻辑时，存在主线程阻塞，此时进行地图手势操作，手势应答会变慢甚至手势响应失败。
    

**处理步骤**

1. 手势遮盖或者手势冲突。
    - 手势遮盖：参考[触摸测试控制](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-hit-test-behavior)做手势穿透。
    - 手势冲突：以Swiper容器组件和地图组件手势存在冲突为例，解决方案参考如下代码：
        
        import { AsyncCallback, BusinessError } from '@kit.BasicServicesKit';
        import { map, mapCommon, MapComponent } from '@kit.MapKit';
        
        class MyDataSource implements IDataSource {
          private list: number[] = [];
        
          constructor(list: number[]) {
            this.list = list;
          }
        
          totalCount(): number {
            return this.list.length;
          }
        
          getData(index: number): number {
            return this.list[index];
          }
        
          registerDataChangeListener(listener: DataChangeListener): void {
          }
        
          unregisterDataChangeListener(listener: DataChangeListener): void {
          }
        }
        
        @Entry
        @Component
        struct SwiperExample {
          private swiperController: SwiperController = new SwiperController();
          private data: MyDataSource = new MyDataSource([]);
          private mapOptions?: mapCommon.MapOptions;
          private callback?: AsyncCallback<map.MapComponentController>;
          private mapController?: map.MapComponentController;
          private mapEventManager?: map.MapEventManager;
          @State mapPositionX: number = 0;
          @State mapPositionY: number = 0;
          @State mapHeight: number = 0;
          @State mapWidth: number = 0;
          @State index: number = 0;
        
          // 判断坐标是否在地图矩形内
          isMap(event: TouchEvent) {
            if (event.changedTouches[0].displayX > this.mapPositionX
              && event.changedTouches[0].displayX < this.mapPositionX + this.mapWidth
              && event.changedTouches[0].displayY > this.mapPositionY
              && event.changedTouches[0].displayY < this.mapPositionY + this.mapHeight) {
              return true;
            }
            return false;
          }
        
          aboutToAppear(): void {
            let list: number[] = [];
            for (let i = 1; i <= 10; i++) {
              list.push(i);
            }
            this.data = new MyDataSource(list);
        
            this.mapOptions = {
              position: {
                target: {
                  latitude: 31.98441025,
                  longitude: 118.766253
                },
                zoom: 10,
                tilt: 10,
                bearing: 90
              },
              scaleControlsEnabled: true
            }
        
            this.callback = async (err, mapController) => {
              if (!err) {
                this.mapController = mapController;
                this.mapEventManager = this.mapController.getEventManager();
                let callback = () => {
                  console.info(`on-mapLoad`);
                };
                this.mapEventManager.on("mapLoad", callback);
              } else {
                console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
              }
            }
          }
        
          build() {
            Column({ space: 5 }) {
              Swiper(this.swiperController) {
                LazyForEach(this.data, (item: string) => {
                  if (item == "3") {
                    Column() {
                      Text(item.toString())
                        .width('90%')
                        .height(160)
                        .backgroundColor(0xAFEEEE)
                        .textAlign(TextAlign.Center)
                        .fontSize(30)
                      MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback })
                        // 获取MapComponent的位置和长宽
                        .width('100%')
                        .height('65%')
                        .onAreaChange((_oldValue: Area, newValue: Area) => {
                          try {
                            if (newValue.globalPosition.x !== undefined && newValue.globalPosition.y !== undefined) {
                              this.mapPositionX = Number(newValue.globalPosition.x);
                              this.mapPositionY = Number(newValue.globalPosition.y);
                              this.mapHeight = Number(newValue.height);
                              this.mapWidth = Number(newValue.width);
                            }
                          } catch (error) {
                            let e: BusinessError = error as BusinessError;
                            console.error("onAreaChange error code:" + e.code + "message:" + e.message);
                          }
                        })
                    }.height("100%")
                  } else {
                    Text(item.toString())
                      .width('90%')
                      .height(160)
                      .backgroundColor(0xAFEEEE)
                      .textAlign(TextAlign.Center)
                      .fontSize(30)
                  }
                }, (item: string) => item)
              }
              // 手势判断 当index为存在地图页面且点击在地图矩形内时为HitTestMode.None（不响应Swiper手势，响应子组件手势）
              .onTouchIntercept((event: TouchEvent) => {
                if (this.index === 2 && this.isMap(event)) {
                  return HitTestMode.None;
                }
                return HitTestMode.Transparent;
              })
              .cachedCount(2)
              .index(1)
              .loop(true)
              .itemSpace(0)
              // 设置圆点导航点样式
              .indicator(
                new DotIndicator()
                  .itemWidth(15)
                  .itemHeight(15)
                  .selectedItemWidth(15)
                  .selectedItemHeight(15)
                  .color(Color.Gray)
                  .selectedColor(Color.Blue))
              .displayArrow({
                // 设置导航点箭头样式
                showBackground: true,
                isSidebarMiddle: true,
                backgroundSize: 24,
                backgroundColor: Color.White,
                arrowSize: 18,
                arrowColor: Color.Blue
              }, false)
              .curve(Curve.Linear)
              .onChange((index: number) => {
                this.index = index;
              })
              .onGestureSwipe((index: number, extraInfo: SwiperAnimationEvent) => {
                console.info("index: " + index);
                console.info("current offset: " + extraInfo.currentOffset);
              })
        
              Row({ space: 12 }) {
                Button('showNext')
                  .onClick(() => {
                    this.swiperController.showNext();
                  })
                Button('showPrevious')
                  .onClick(() => {
                    this.swiperController.showPrevious();
                  })
              }.margin(5)
            }.width('100%')
            .margin({ top: 5 })
          }
        }
        
2. 主线程阻塞。
    
    请分析应用的业务逻辑，将复杂逻辑放到子线程中处理。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-faq-2 "siteId参数如何获取")
# 手势卡顿或者不生效

更新时间: 2025-12-16 16:37

**现象描述**

地图页面操作手势卡顿或者不生效。

**可能原因**

1. 手势遮盖或者手势冲突。
    - 手势遮盖：地图组件的上层存在没有做手势穿透的组件。
    - 手势冲突：以Swiper容器组件中使用地图组件为例，Swiper容器组件和地图组件手势会存在冲突。
2. 主线程阻塞。
    
    应用主线程处理大批量逻辑时，存在主线程阻塞，此时进行地图手势操作，手势应答会变慢甚至手势响应失败。
    

**处理步骤**

1. 手势遮盖或者手势冲突。
    - 手势遮盖：参考[触摸测试控制](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-hit-test-behavior)做手势穿透。
    - 手势冲突：以Swiper容器组件和地图组件手势存在冲突为例，解决方案参考如下代码：
        
        import { AsyncCallback, BusinessError } from '@kit.BasicServicesKit';
        import { map, mapCommon, MapComponent } from '@kit.MapKit';
        
        class MyDataSource implements IDataSource {
          private list: number[] = [];
        
          constructor(list: number[]) {
            this.list = list;
          }
        
          totalCount(): number {
            return this.list.length;
          }
        
          getData(index: number): number {
            return this.list[index];
          }
        
          registerDataChangeListener(listener: DataChangeListener): void {
          }
        
          unregisterDataChangeListener(listener: DataChangeListener): void {
          }
        }
        
        @Entry
        @Component
        struct SwiperExample {
          private swiperController: SwiperController = new SwiperController();
          private data: MyDataSource = new MyDataSource([]);
          private mapOptions?: mapCommon.MapOptions;
          private callback?: AsyncCallback<map.MapComponentController>;
          private mapController?: map.MapComponentController;
          private mapEventManager?: map.MapEventManager;
          @State mapPositionX: number = 0;
          @State mapPositionY: number = 0;
          @State mapHeight: number = 0;
          @State mapWidth: number = 0;
          @State index: number = 0;
        
          // 判断坐标是否在地图矩形内
          isMap(event: TouchEvent) {
            if (event.changedTouches[0].displayX > this.mapPositionX
              && event.changedTouches[0].displayX < this.mapPositionX + this.mapWidth
              && event.changedTouches[0].displayY > this.mapPositionY
              && event.changedTouches[0].displayY < this.mapPositionY + this.mapHeight) {
              return true;
            }
            return false;
          }
        
          aboutToAppear(): void {
            let list: number[] = [];
            for (let i = 1; i <= 10; i++) {
              list.push(i);
            }
            this.data = new MyDataSource(list);
        
            this.mapOptions = {
              position: {
                target: {
                  latitude: 31.98441025,
                  longitude: 118.766253
                },
                zoom: 10,
                tilt: 10,
                bearing: 90
              },
              scaleControlsEnabled: true
            }
        
            this.callback = async (err, mapController) => {
              if (!err) {
                this.mapController = mapController;
                this.mapEventManager = this.mapController.getEventManager();
                let callback = () => {
                  console.info(`on-mapLoad`);
                };
                this.mapEventManager.on("mapLoad", callback);
              } else {
                console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
              }
            }
          }
        
          build() {
            Column({ space: 5 }) {
              Swiper(this.swiperController) {
                LazyForEach(this.data, (item: string) => {
                  if (item == "3") {
                    Column() {
                      Text(item.toString())
                        .width('90%')
                        .height(160)
                        .backgroundColor(0xAFEEEE)
                        .textAlign(TextAlign.Center)
                        .fontSize(30)
                      MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback })
                        // 获取MapComponent的位置和长宽
                        .width('100%')
                        .height('65%')
                        .onAreaChange((_oldValue: Area, newValue: Area) => {
                          try {
                            if (newValue.globalPosition.x !== undefined && newValue.globalPosition.y !== undefined) {
                              this.mapPositionX = Number(newValue.globalPosition.x);
                              this.mapPositionY = Number(newValue.globalPosition.y);
                              this.mapHeight = Number(newValue.height);
                              this.mapWidth = Number(newValue.width);
                            }
                          } catch (error) {
                            let e: BusinessError = error as BusinessError;
                            console.error("onAreaChange error code:" + e.code + "message:" + e.message);
                          }
                        })
                    }.height("100%")
                  } else {
                    Text(item.toString())
                      .width('90%')
                      .height(160)
                      .backgroundColor(0xAFEEEE)
                      .textAlign(TextAlign.Center)
                      .fontSize(30)
                  }
                }, (item: string) => item)
              }
              // 手势判断 当index为存在地图页面且点击在地图矩形内时为HitTestMode.None（不响应Swiper手势，响应子组件手势）
              .onTouchIntercept((event: TouchEvent) => {
                if (this.index === 2 && this.isMap(event)) {
                  return HitTestMode.None;
                }
                return HitTestMode.Transparent;
              })
              .cachedCount(2)
              .index(1)
              .loop(true)
              .itemSpace(0)
              // 设置圆点导航点样式
              .indicator(
                new DotIndicator()
                  .itemWidth(15)
                  .itemHeight(15)
                  .selectedItemWidth(15)
                  .selectedItemHeight(15)
                  .color(Color.Gray)
                  .selectedColor(Color.Blue))
              .displayArrow({
                // 设置导航点箭头样式
                showBackground: true,
                isSidebarMiddle: true,
                backgroundSize: 24,
                backgroundColor: Color.White,
                arrowSize: 18,
                arrowColor: Color.Blue
              }, false)
              .curve(Curve.Linear)
              .onChange((index: number) => {
                this.index = index;
              })
              .onGestureSwipe((index: number, extraInfo: SwiperAnimationEvent) => {
                console.info("index: " + index);
                console.info("current offset: " + extraInfo.currentOffset);
              })
        
              Row({ space: 12 }) {
                Button('showNext')
                  .onClick(() => {
                    this.swiperController.showNext();
                  })
                Button('showPrevious')
                  .onClick(() => {
                    this.swiperController.showPrevious();
                  })
              }.margin(5)
            }.width('100%')
            .margin({ top: 5 })
          }
        }
        
2. 主线程阻塞。
    
    请分析应用的业务逻辑，将复杂逻辑放到子线程中处理。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-faq-2 "siteId参数如何获取")
# 手势卡顿或者不生效

更新时间: 2025-12-16 16:37

**现象描述**

地图页面操作手势卡顿或者不生效。

**可能原因**

1. 手势遮盖或者手势冲突。
    - 手势遮盖：地图组件的上层存在没有做手势穿透的组件。
    - 手势冲突：以Swiper容器组件中使用地图组件为例，Swiper容器组件和地图组件手势会存在冲突。
2. 主线程阻塞。
    
    应用主线程处理大批量逻辑时，存在主线程阻塞，此时进行地图手势操作，手势应答会变慢甚至手势响应失败。
    

**处理步骤**

1. 手势遮盖或者手势冲突。
    - 手势遮盖：参考[触摸测试控制](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-hit-test-behavior)做手势穿透。
    - 手势冲突：以Swiper容器组件和地图组件手势存在冲突为例，解决方案参考如下代码：
        
        import { AsyncCallback, BusinessError } from '@kit.BasicServicesKit';
        import { map, mapCommon, MapComponent } from '@kit.MapKit';
        
        class MyDataSource implements IDataSource {
          private list: number[] = [];
        
          constructor(list: number[]) {
            this.list = list;
          }
        
          totalCount(): number {
            return this.list.length;
          }
        
          getData(index: number): number {
            return this.list[index];
          }
        
          registerDataChangeListener(listener: DataChangeListener): void {
          }
        
          unregisterDataChangeListener(listener: DataChangeListener): void {
          }
        }
        
        @Entry
        @Component
        struct SwiperExample {
          private swiperController: SwiperController = new SwiperController();
          private data: MyDataSource = new MyDataSource([]);
          private mapOptions?: mapCommon.MapOptions;
          private callback?: AsyncCallback<map.MapComponentController>;
          private mapController?: map.MapComponentController;
          private mapEventManager?: map.MapEventManager;
          @State mapPositionX: number = 0;
          @State mapPositionY: number = 0;
          @State mapHeight: number = 0;
          @State mapWidth: number = 0;
          @State index: number = 0;
        
          // 判断坐标是否在地图矩形内
          isMap(event: TouchEvent) {
            if (event.changedTouches[0].displayX > this.mapPositionX
              && event.changedTouches[0].displayX < this.mapPositionX + this.mapWidth
              && event.changedTouches[0].displayY > this.mapPositionY
              && event.changedTouches[0].displayY < this.mapPositionY + this.mapHeight) {
              return true;
            }
            return false;
          }
        
          aboutToAppear(): void {
            let list: number[] = [];
            for (let i = 1; i <= 10; i++) {
              list.push(i);
            }
            this.data = new MyDataSource(list);
        
            this.mapOptions = {
              position: {
                target: {
                  latitude: 31.98441025,
                  longitude: 118.766253
                },
                zoom: 10,
                tilt: 10,
                bearing: 90
              },
              scaleControlsEnabled: true
            }
        
            this.callback = async (err, mapController) => {
              if (!err) {
                this.mapController = mapController;
                this.mapEventManager = this.mapController.getEventManager();
                let callback = () => {
                  console.info(`on-mapLoad`);
                };
                this.mapEventManager.on("mapLoad", callback);
              } else {
                console.error(`Failed to initialize the map, code is：${err.code}, message is ${err.message}`);
              }
            }
          }
        
          build() {
            Column({ space: 5 }) {
              Swiper(this.swiperController) {
                LazyForEach(this.data, (item: string) => {
                  if (item == "3") {
                    Column() {
                      Text(item.toString())
                        .width('90%')
                        .height(160)
                        .backgroundColor(0xAFEEEE)
                        .textAlign(TextAlign.Center)
                        .fontSize(30)
                      MapComponent({ mapOptions: this.mapOptions, mapCallback: this.callback })
                        // 获取MapComponent的位置和长宽
                        .width('100%')
                        .height('65%')
                        .onAreaChange((_oldValue: Area, newValue: Area) => {
                          try {
                            if (newValue.globalPosition.x !== undefined && newValue.globalPosition.y !== undefined) {
                              this.mapPositionX = Number(newValue.globalPosition.x);
                              this.mapPositionY = Number(newValue.globalPosition.y);
                              this.mapHeight = Number(newValue.height);
                              this.mapWidth = Number(newValue.width);
                            }
                          } catch (error) {
                            let e: BusinessError = error as BusinessError;
                            console.error("onAreaChange error code:" + e.code + "message:" + e.message);
                          }
                        })
                    }.height("100%")
                  } else {
                    Text(item.toString())
                      .width('90%')
                      .height(160)
                      .backgroundColor(0xAFEEEE)
                      .textAlign(TextAlign.Center)
                      .fontSize(30)
                  }
                }, (item: string) => item)
              }
              // 手势判断 当index为存在地图页面且点击在地图矩形内时为HitTestMode.None（不响应Swiper手势，响应子组件手势）
              .onTouchIntercept((event: TouchEvent) => {
                if (this.index === 2 && this.isMap(event)) {
                  return HitTestMode.None;
                }
                return HitTestMode.Transparent;
              })
              .cachedCount(2)
              .index(1)
              .loop(true)
              .itemSpace(0)
              // 设置圆点导航点样式
              .indicator(
                new DotIndicator()
                  .itemWidth(15)
                  .itemHeight(15)
                  .selectedItemWidth(15)
                  .selectedItemHeight(15)
                  .color(Color.Gray)
                  .selectedColor(Color.Blue))
              .displayArrow({
                // 设置导航点箭头样式
                showBackground: true,
                isSidebarMiddle: true,
                backgroundSize: 24,
                backgroundColor: Color.White,
                arrowSize: 18,
                arrowColor: Color.Blue
              }, false)
              .curve(Curve.Linear)
              .onChange((index: number) => {
                this.index = index;
              })
              .onGestureSwipe((index: number, extraInfo: SwiperAnimationEvent) => {
                console.info("index: " + index);
                console.info("current offset: " + extraInfo.currentOffset);
              })
        
              Row({ space: 12 }) {
                Button('showNext')
                  .onClick(() => {
                    this.swiperController.showNext();
                  })
                Button('showPrevious')
                  .onClick(() => {
                    this.swiperController.showPrevious();
                  })
              }.margin(5)
            }.width('100%')
            .margin({ top: 5 })
          }
        }
        
2. 主线程阻塞。
    
    请分析应用的业务逻辑，将复杂逻辑放到子线程中处理。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-faq-2 "siteId参数如何获取")
# 上架前准备-获取地图服务协议及资质证明

更新时间: 2025-12-16 16:36

## 华为地图服务使用协议

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“协议签署记录”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163628.28162664039774783890126493239070:50001231000000:2800:B1DC23CE6791B31253E54A2C7546559B634A05A34471D2999486943BAFFCDCAF.png)
    
2. 在查看下载协议中选择可查看“华为地图服务使用协议”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163628.63219648811905166666962585337979:50001231000000:2800:37649350D0AD714DE4B4DA29327CE1D9A089B2F59B2D8A6E5A001BAEBD362122.png "点击放大")
    

## 地图审图号

标准地图审图号：GS（2024）1955号

卫星地图审图号：GS（2025）2036号

送审单位：华为软件技术有限公司

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-personal-privacy "个人数据处理说明")
# 上架前准备-获取地图服务协议及资质证明

更新时间: 2025-12-16 16:36

## 华为地图服务使用协议

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“协议签署记录”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163628.28162664039774783890126493239070:50001231000000:2800:B1DC23CE6791B31253E54A2C7546559B634A05A34471D2999486943BAFFCDCAF.png)
    
2. 在查看下载协议中选择可查看“华为地图服务使用协议”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163628.63219648811905166666962585337979:50001231000000:2800:37649350D0AD714DE4B4DA29327CE1D9A089B2F59B2D8A6E5A001BAEBD362122.png "点击放大")
    

## 地图审图号

标准地图审图号：GS（2024）1955号

卫星地图审图号：GS（2025）2036号

送审单位：华为软件技术有限公司

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-personal-privacy "个人数据处理说明")
