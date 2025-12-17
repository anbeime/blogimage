# 能力介绍

更新时间: 2025-12-16 16:34

AR Engine（AR引擎服务）是一个用于在HarmonyOS上构建增强现实应用的引擎，提供了运动跟踪、环境跟踪和命中检测等空间计算能力。

通过这些能力，应用可以实现虚拟世界与现实世界的融合，给用户提供全新的视觉体验和交互方式。

AR Engine包含三大能力，分别是运动跟踪能力、环境跟踪能力和命中检测能力。

## 运动跟踪能力

AR Engine通过获取终端设备摄像头数据，结合图像特征和惯性传感器（IMU），计算设备位置（沿x、y、z轴方向位移）和姿态（绕x、y、z轴旋转），实现6自由度（6DoF）运动跟踪能力。

**图1** 6DoF运动跟踪能力示意图（红色线代表设备运动方向）  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163440.50146546245852980299834956510296:50001231000000:2800:9B329E50EE3C0B30D7C6B681FF0DAF2228CCF5FE4768466250674733360E4A13.png "点击放大")

## 环境跟踪能力

AR Engine通过检测和跟踪设备周围的平面及语义，实现环境跟踪能力。环境跟踪能力包括：平面检测、平面语义、目标语义、深度估计、环境网格扫描、图像跟踪和高精几何重建。

- 平面检测
    
    检测水平和竖直平面（如地面、墙面等），并识别平面边界。应用可使用这些平面来放置虚拟物体。
    
    **图2** 平面检测示意图（左图为水平平面，右图为竖直平面）  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163440.39293037214862564347621518959084:50001231000000:2800:BCAE130EE78889C41A162085470A67493AD2B13799E5047C405D38E5F627D738.jpg "点击放大")
    
- 平面语义
    
    检测不同的平面类型。当前支持的平面类型共11种，分别为：墙面、地面、座椅面、桌面、天花板、门面、窗面、床面、平面空间、立方体体积、立方体空间容积（平面空间、立方体体积和立方体空间容积仅在高精几何重建模式下支持）。
    
    **图3** 平面语义示意图（蓝色表示地面，绿色表示桌面）  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163440.29192573247859993966089780662566:50001231000000:2800:558EDB5DAD684ADCCC630B9D3777DE4602CC32CB05125F2060A458B29C41DBEB.jpg "点击放大")
    
- 目标语义
    
    当目标物体位于平面上时，检测目标物体的形状，当前包括矩形和圆形。
    
    **图4** 目标语义示意图 (左图为矩形检测，右图为圆形检测）  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163440.75567056288448224165358492685841:50001231000000:2800:6F8C5C22980B1F1DDF7E7C167AADFEFA8A0BCFF8D499B52D431ECE09BCD7F116.jpg "点击放大")
    
- 深度估计
    
    支持持续输出周围环境相对终端设备的深度信息，利用这些深度信息，可以实现更加自然、无缝的虚实体验。本功能提供的深度信息是指从终端设备摄像头到显示场景中各点的深度值，每个像素点都有该深度值。同时输出置信度信息，开发者可自行根据应用需求根据置信度选择更稠密或者更精确的深度信息。
    
    **图5** 深度渲染示意图  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163440.41866937653576990515767018811132:50001231000000:2800:780B1A7873C5D9A4EC756B038AF0A8B3D597B78978D8EA71B9A4F92684688CA4.png)
    
- 环境网格扫描
    
    实时计算并输出当前画面中的环境网格数据，可用于处理虚实遮挡等应用场景。
    
    通过环境网格能力，可将虚拟物体放置在任意可重建的曲面上，而不再受限于水平面和垂直面。同时可利用重建的环境网格实现虚实遮挡和碰撞检测，使得虚拟角色能够准确的知道当前所在的周围三维空间情况，实现更好的沉浸式AR体验。
    
    **图6** 环境网格扫描示意图  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163441.96488469270155677445057146204711:50001231000000:2800:F76A895A9C180725B4B6894E45DA03AE70656737E93636DF7A54962D7151ACF7.png)
    
- 图像跟踪
    
    AR Engine提供图像识别与跟踪的能力，检测场景中是否存在用户提供的图像，识别之后输出图像的位姿。
    
    通过图像识别与跟踪功能，可实现基于现实世界场景中图像（海报或封面等）的增强现实。可提供一组参考图像，当这些图像出现在终端设备的相机视野范围内时，AR Engine可为AR应用实时跟踪图像，丰富场景理解及交互体验。
    
    **图7** 图像跟踪示意图
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163441.48890022469245081275578269886497:50001231000000:2800:9D5CED2D5A89E9A02993A63AAD78EF1DC44F0E4A54D64E27FFAF2C632C196C39.png)
    
- 高精几何重建
    
    AR Engine高精几何重建用于识别空间中的立方体物体或者嵌入式立方体空间，计算出被识别物体或空间的长、宽、高以及体积。体积测量可以用于测量立方体体积以及嵌入式空间的大小。
    
    高精几何重建主要包含稠密点云绘制、体积测量、空间识别三大能力。
    
    **图8** 稠密点云绘制示意图  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163441.49664309575422773934332689411964:50001231000000:2800:B139FBD7E637FF84FC4F38B51474F86CAB89F714B0A19D68DAD740BFB5C205D5.png)
    
    **图9** 体积测量示意图  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163441.99631870932570475698936776826210:50001231000000:2800:73E0CF9D1C608C40B7224F75C1C3BB4E5AAC35D74997760EEC3E4FA91CACD107.png)
    
    **图10** 空间识别示意图  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163442.37455640253135441258604505372604:50001231000000:2800:EC85651BDE74FE68AFE776B614B0F4C72C7F8F200B302242D2D2E69A6CB60E47.png)
    

## 命中检测能力

AR Engine通过命中检测（Hit Testing）技术，将终端设备屏幕上的兴趣点映射为现实环境中的兴趣点。命中检测以现实环境中的兴趣点为源，发出一条射线连接到摄像头所在位置，返回射线与平面（或特征点）的交点。通过命中检测能力，用户可以通过点击终端设备屏幕，选中现实环境中的兴趣点，与虚拟物体进行交互。

**图11** 命中检测示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163442.80135347240859308872605219886210:50001231000000:2800:00F69222AEA2F501A9E6B44A6E2257093AC89BBE050494AB1001773955B5808E.jpg "点击放大")

## 场景介绍

通过以上能力，可以实现AR场景的应用开发，如AR物体摆放等，为用户提供虚实融合的全新交互体验。

- AR物体摆放：通过摄像头构建AR虚拟世界，支持用户在虚拟世界中放置虚拟物体。AR物体摆放可用于虚拟家具试用等，实现虚拟与现实世界融合。
- 平面语义识别：对于检测到的平面，开发者可以对平面进行平面的语义识别，包括墙面、地面、座椅面、桌面、天花板、门面、窗面、床面等。
- 目标形状识别：对于检测到的目标物体，开发者可以对目标物体进行形状识别，可识别的形状包括矩形和圆形。
- 网格扫描：通过摄像头构建AR虚拟世界，通过重建周围环境网格实现虚实遮挡和碰撞检测，支持用户在虚拟世界中放置虚拟物体。通过感知当前所在的周围三维空间情况，实现更好的沉浸式AR体验。
- 深度估计：通过摄像头获取周围环境信息，持续输出周围环境的深度信息，为用户提供环境三维感知能力。该技术可应用于测量、体积估算、场景重建等获取空间物体深度信息，基于此信息完成一些空间计算任务，比如计算物体体积等。
- 图像跟踪：通过摄像头获取周围环境信息，持续检测场景中是否存在输入的图像，识别之后输出图像的位姿。
    
    AR Engine提供图像识别与跟踪的能力，检测场景中是否存在用户提供的图像，识别之后输出图像的位姿。
    
    通过图像识别与跟踪功能，可实现基于现实世界场景中图像（海报或封面等）的增强现实。可提供一组参考图像，当这些图像出现在终端设备的相机视野范围内时，AR Engine可为AR应用实时跟踪图像，丰富场景理解及交互体验。
    
- 高精几何重建：通过摄像头获取周围环境信息，识别空间中的立方体物体或者嵌入式立方体空间，计算出被识别物体或空间的长、宽、高以及体积。体积测量可以用于测量立方体体积以及嵌入式空间的大小。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-introduction "AR Engine简介")
# 坐标系说明

更新时间: 2025-12-16 16:34

## AR Engine重力对齐世界坐标系

- 以相机启动时相机中心为坐标原点；
- 重力方向为Y轴，向上+Y，向下-Y；
- 设备水平前后移动为X轴，由近及远+X，由远及近-X；
- 设备水平左右移动为Z轴，向右+Z，向左-Z。

**图1** 重力对齐世界坐标系示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163445.99408857311922582325275399864109:50001231000000:2800:522B563F8A5F9568B42AD85594BD231F1C24CAE2B072D882A0AB46ACC90000F6.png)

## AR Engine重力对齐北向坐标系

- 以相机启动时相机中心为坐标原点；
- 重力方向为Y轴，向上+Y，向下-Y；
- 指南针北向为+X轴，南向为-X轴；
- 指南针东向为+Z轴，西向为-Z轴；
- 重力对齐北向坐标系为固定坐标系，不受设备位姿变化影响。

**图2** 重力对齐北向坐标系示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163446.99858955136078796890782777529952:50001231000000:2800:C9A59AA9184D11F8EBB5F42AC621CBB45DCE970D30B74466AB85B05C3356D65C.png)

## AGP世界坐标系

- 以相机启动时相机中心为坐标原点；
- 设备垂直方向为Y轴，向上+Y，向下-Y；
- 设备水平前后移动为Z轴，向前+Z，向后-Z；
- 设备水平左右移动为X轴，向左+X，向右-X。

**图3** AGP世界坐标系示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163446.64459401920892827582460221480129:50001231000000:2800:98FA051A68408FE6AFECF96C6F43F4DF82549EF5ED0BFEC769FC0BD06F25A395.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-ability "能力介绍")
# 开发准备

更新时间: 2025-12-16 16:34

## 软件要求

- 推荐使用Windows 10及以上版本、MacOS 11及以上版本安装应用开发环境DevEco Studio。
- 推荐DevEco Studio版本：DevEco Studio 6.0.0 Release及以上。
- 推荐HarmonyOS SDK版本：HarmonyOS 6.0.0 Release SDK及以上。

## 硬件要求

开发者可根据实际的开发语言，选择对应接口判断当前设备是否支持AR Engine。接口的调用参考如下方式：

ArkTS（[ARViewContext.init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section07524457283)）：

1. import { arViewController, ARView } from '@kit.AREngine';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. @Component
4. struct ARTest {
5.   @State arContext?: arViewController.ARViewContext = undefined;
6.   build() {
7.     NavDestination() {
8.       RelativeContainer() {
9.         if (this.arContext) {
10.           ARView({ context: this.arContext })
11.         }
12.       }
13.     }
14.     .onAppear(() => {
15.       this.initARView()
16.     })
17.     .onWillDisappear(() => {
18.       this.arContext?.destroy();
19.     })
20.   }

21.   private initARView(): void {
22.     let context = new arViewController.ARViewContext()
23.     context.init().then(() => {
24.       this.arContext = context;
25.       console.info(`Succeeded in initializing ARView.`);
26.     }).catch((err: BusinessError) => {
27.       console.error(`Failed to init context. Code is ${err.code}, message is ${err.message}`);
28.     });
29.   }
30. }

C/C++（[HMS_AREngine_ARSession_Create](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-capi-arengine#ga47713cb18234569e03b5216b6c8442d3)）：

1. #include "ar/ar_engine_core.h" 

2. bool isSupportAREngine() {
3.     AREngine_ARSession *arSession = nullptr;
4.     if(HMS_AREngine_ARSession_Create(nullptr, nullptr, &arSession) == ARENGINE_ERROR_DEVICE_NOT_SUPPORTED){
5.         return false;
6.     }
7.     return true;
8. }

若对应接口返回错误码为801或ARENGINE_ERROR_DEVICE_NOT_SUPPORTED，则表示AR Engine不支持当前设备。

## 环境搭建

请参考[应用开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview)完成基本准备工作。

## 申请权限

在开发AR应用时，需要先申请相机相关权限，确保应用拥有访问相机硬件及其他功能的权限，需要的权限如下表。在申请权限前，请保证符合[权限使用的基本原则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-permission-mgmt-overview#%E6%9D%83%E9%99%90%E4%BD%BF%E7%94%A8%E7%9A%84%E5%9F%BA%E6%9C%AC%E5%8E%9F%E5%88%99)。

- 使用相机拍摄前，需要申请**ohos.permission.CAMERA**相机权限。
- 当需要使用加速计感知设备运动状态时，需要申请**ohos.permission.ACCELEROMETER**加速计权限。
- 当需要陀螺仪感知设备位姿信息时，需要申请**ohos.permission.GYROSCOPE**陀螺仪权限。

## 前置准备

推荐使用[组件导航(Navigation) (推荐)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation)作为页面路由，使用[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)的[页面生命周期](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E9%A1%B5%E9%9D%A2%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)所示方法。

开发者需先创建首页，通过首页选择进入AR Engine场景。

1. 导入所需模块。
    
    1. import { abilityAccessCtrl, PermissionRequestResult } from '@kit.AbilityKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 创建一个基础的页面，具体可参考[组件导航(Navigation) (推荐)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation)。
    
    1. @Entry
    2. @Component
    3. struct Selector {
    4.   pageInfo: NavPathStack = new NavPathStack();
    
    5.   build(): void {
    6.     Navigation(this.pageInfo) {
    
    7.     }
    8.     .mode(NavigationMode.Stack)
    9.     .hideTitleBar(true)
    10.     .hideBackButton(true)
    11.     .hideToolBar(true)
    12.   }
    13. }
    
3. 创建sampleButton，封装Button及权限校验功能，使用@Builder装饰，并配置routerMap进行页面跳转。
    
    1. @Entry
    2. @Component
    3. struct Selector {
    4.   pageInfo: NavPathStack = new NavPathStack();
    5.   private hasPermission: boolean = false;
    6.   @State context: Context = this.getUIContext().getHostContext() as Context;
    
    7.   build(): void {
    8.     // ...
    9.   }
    
    10.   @Builder
    11.   sampleButton(sampleName: string): void {
    12.     Button(sampleName, { type: ButtonType.Normal, stateEffect: true })
    13.       .borderRadius(8)
    14.       .width('50%')
    15.       .height('5%')
    16.       .onClick(async () => {
    17.         if (!this.hasPermission) {
    18.           this.hasPermission = await requestPermissionOnSetting(this.context);
    19.           if (!this.hasPermission) {
    20.             return;
    21.           }
    22.         }
    23.         this.pageInfo.clear();
    24.         this.pageInfo.pushDestinationByName(sampleName, null);
    25.       })
    26.   }
    27. }
    
4. 创建requestPermissionOnSetting方法用于校验在进入AR场景时是否已经获取相机权限。
    
    1. struct Selector {
    2.   // ...
    3. }
    
    4. async function requestPermissionOnSetting(context: Context): Promise<boolean> {
    5.   let requestResult: boolean = false;
    6.   let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
    7.   await atManager.requestPermissionOnSetting(context, ['ohos.permission.CAMERA'])
    8.     .then((data: abilityAccessCtrl.GrantStatus[]) => {
    9.       console.info('data:' + JSON.stringify(data));
    10.       if (data[0] === abilityAccessCtrl.GrantStatus.PERMISSION_GRANTED) {
    11.         requestResult = true;
    12.       }
    13.     })
    14.     .catch((err: BusinessError) => {
    15.       console.error('data:' + JSON.stringify(err));
    16.     })
    17.   return requestResult;
    18. }
    
5. 在页面上创建按钮，用于进入AR场景。
    
    1. build(): void {
    2.   Navigation(this.pageInfo) {
    3.     Column() {
    4.       this.sampleButton('ARWorld'); // 进入ARWorld场景
    5.     }
    6.     .justifyContent(FlexAlign.SpaceEvenly)
    7.     .width('100%')
    8.     .height('100%')
    9.   }
    10.   .mode(NavigationMode.Stack)
    11.   .hideTitleBar(true)
    12.   .hideBackButton(true)
    13.   .hideToolBar(true)
    14. }
    
6. 在onAppear中配置应用首次启动时的权限校验方法requestPermissionOnFirstStartup。
    
    1. struct Selector {
    2.   // ...
    3.   build(): void {
    4.     Navigation(this.pageInfo) {
    5.       Column() {
    6.         this.sampleButton('ARWorld');
    7.       }
    8.       .justifyContent(FlexAlign.SpaceEvenly)
    9.       .width('100%')
    10.       .height('100%')
    11.     }
    12.     .onAppear(() => {
    13.       this.requestPermissionOnFirstStartup();
    14.     })
    15.     .mode(NavigationMode.Stack)
    16.     .hideTitleBar(true)
    17.     .hideBackButton(true)
    18.     .hideToolBar(true)
    19.   }
    
    20.   @Builder
    21.   sampleButton(sampleName: string): void { 
    22.     // ...
    23.   }
    
    24.   private requestPermissionOnFirstStartup(): void {
    25.     abilityAccessCtrl.createAtManager()
    26.       .requestPermissionsFromUser(this.context, ['ohos.permission.CAMERA'])
    27.       .then((data: PermissionRequestResult) => {
    28.         let grantStatus: number[] = data.authResults;
    29.         if (grantStatus[0] === 0) {
    30.           this.hasPermission = true;
    31.           console.info('Succeeded in getting requestPermission.');
    32.         } else {
    33.           this.hasPermission = false;
    34.           console.error('Failed to get requestPermission, user rejected.');
    35.         }
    36.       })
    37.       .catch((err: BusinessError) => {
    38.         console.error(`Failed to request permissions from user. Code is ${err.code}, message is ${err.message}.`);
    39.       })
    40.   }
    41. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-coordinate "坐标系说明")
# 管理AR会话

更新时间: 2025-12-16 16:34

## 概要

在开发AR应用之前，需调用AR会话接口创建一个唯一的AR会话，供后续操作与管理使用。在整个AR应用生命周期中，AR会话扮演着至关重要的角色。

开发者可以使用[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)来进行AR会话session的创建与销毁等操作。

[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)和[ARSession](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section19193165314510)的不同之处在于，[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)不仅封装了AR会话session，还集成了AR场景的创建与管理，从而使得开发更为便捷。

在进行后续功能开发前，请确保已创建一个可用且唯一的AR会话。

## 接口说明

AR会话主要依赖[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，以下接口为AR会话相关接口。详细接口和说明，请参考[arViewController（AR场景管理能力）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller)。

|接口名|描述|
|:--|:--|
|[ARViewContext.init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section07524457283)|初始化[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，初始化AR会话和设置AR渲染场景等。|
|[ARViewContext.pause](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9795165613212)|暂停相机跟踪与AR场景渲染。|
|[ARViewContext.destroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section169251835133414)|销毁[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，释放ARView使用资源，包括AR会话与呈现场景销毁，在退出ARView场景时使用。|
|[ARViewContext.resume](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section639015333356)|用于恢复暂停的相机跟踪与AR场景渲染。|
|[ARViewContext.scene](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section885612613616)|设置ARView的AR场景。|
|[ARViewContext.scene](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section1371542426)|获得的AR呈现场景，用于管理空间节点。|
|[ARViewContext.session](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section18461161774312)|获取AR会话，用于获取相关AR环境跟踪、相机跟踪、命中检测等能力，如相机位姿、平面信息、创建锚点等。|
|[ARViewContext.config](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section4323184815436)|设置AR会话的配置文件，如北向坐标、性能模式等。|
|[ARViewContext.callback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section20507194174418)|设置回调函数，以根据回调功能实现对应业务逻辑。|

## 开发步骤

对于使用ArkTS的任何AR应用，首先需要创建一个AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，用于管理AR Engine的系统状态。

### 导入模块

导入AR Engine相关模块，导入方法如下。

1. import { arEngine, ARView, arViewController } from '@kit.AREngine';
2. import { Node, Scene } from '@kit.ArkGraphics3D';
3. import { BusinessError } from '@kit.BasicServicesKit';

### 初始化AR会话和AR场景

通过[ARViewContext.init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section07524457283)方法初始化一个AR会话及场景。

在此之前请确保已获取相机权限，否则将不会加载AR场景，具体指导请参考[前置准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-preparations#section148162301428)或者[申请权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-preparations#section12219144310509)。

AR会话及场景创建好后使用[组件导航(Navigation) (推荐)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation)组件及[ARView](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-component-arview#section46518288429)组件在设备上显示AR场景，关于[组件导航(Navigation) (推荐)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation)具体指导可参考[前置准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-preparations#section148162301428)。

1. @Builder
2. export function ARWorldBuilder(): void {
3.   ARWorld();
4. }

5. @Component
6. struct ARWorld {
7.   @State arContext?: arViewController.ARViewContext = undefined;

8.   // 创建UI窗口，显示AR场景
9.   build(): void {
10.     NavDestination() {
11.       RelativeContainer() {
12.         if (this.arContext) {
13.           ARView({ context: this.arContext })
14.             .height('100%')
15.             .width('100%')
16.             .alignRules({
17.               center: { anchor: '__container__', align: VerticalAlign.Center },
18.               middle: { anchor: '__container__', align: HorizontalAlign.Center }
19.             })
20.         }
21.       }
22.     }
23.     .onAppear(() => {
24.       this.initARView();
25.     })
26.     .onWillDisappear(() => {
27.       this.stopARView();
28.     })
29.     .onShown(() => {
30.       this.resumeARView();
31.     })
32.     .onHidden(() => {
33.       this.pauseARView();
34.     })
35.     .hideTitleBar(true)
36.     .hideBackButton(true)
37.     .hideToolBar(true)
38.   }

39.   private initARView(): void {
40.     Scene.load().then(async (scene: Scene) => {
41.       let viewContext: arViewController.ARViewContext = new arViewController.ARViewContext();
42.       viewContext.scene = scene;
43.       viewContext.callback = new ARViewCallbackImpl();  // 通过回调实现业务场景
44.       viewContext.config = {
45.         type: arEngine.ARType.WORLD,
46.         planeFindingMode: arEngine.ARPlaneFindingMode.HORIZONTAL_AND_VERTICAL,
47.         powerMode: arEngine.ARPowerMode.NORMAL,
48.         semanticMode: arEngine.ARSemanticMode.NONE,
49.         poseMode: arEngine.ARPoseMode.GRAVITY,
50.         depthMode: arEngine.ARDepthMode.AUTOMATIC,
51.         meshMode: arEngine.ARMeshMode.DISABLED,
52.         focusMode: arEngine.ARFocusMode.AUTO
53.       }
54.       viewContext.init().then(() => {
55.         this.arContext = viewContext;
56.         console.info('Succeeded in initializing ARView.');
57.       }).catch((err: BusinessError) => {
58.         console.error(`Failed to init ARView. Code is ${err.code}, message is ${err.message}.`);
59.       })
60.     })
61.   }
62. }

### 使用AR会话对象处理业务

调用[ARViewCallback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9396615174614)，使用其中的[onFrameUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section52341758194715)方法获取AR会话对象，之后可根据开发者所需的具体业务编写处理逻辑。

1. class ARViewCallbackImpl extends arViewController.ARViewCallback {
2.   onAnchorAdd(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
3.   }

4.   onAnchorUpdate(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
5.   }

6.   async onFrameUpdate(ctx: arViewController.ARViewContext, sysBootTs: number): Promise<void> {
7.     if (!ctx.session) {
8.       return;
9.     }

10.     let arSession: arEngine.ARSession = ctx.session; // 获取AR会话

11.     try {
12.       // 示例为一个帧对象的获取与销毁
13.       let frame: arEngine.ARFrame = arSession.getFrame();
14.       await frame.release();

15.     } catch (error) {
16.       const err: BusinessError = error as BusinessError;
17.       console.error(`Failed to update data. Code is ${err.code}, message is ${err.message}.`);
18.     }
19.   }
20. }

### 暂停AR会话

要暂停AR会话，开发者可以使用[ARViewContext.pause](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9795165613212)方法，在应用置为后台时可以暂停AR会话和暂停AR场景。

1. private pauseARView(): void {
2.   if (!this.arContext) {
3.     return;
4.   }
5.   try {
6.     this.arContext.pause();
7.   } catch (error) {
8.     const err: BusinessError = error as BusinessError;
9.     console.error(`Failed to pause context. Code is ${err.code}, message is ${err.message}.`);
10.   }
11. }

### 恢复AR会话

要恢复暂停的AR会话和AR场景，开发者可以使用[ARViewContext.resume](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section639015333356)方法。

1. private resumeARView(): void {
2.   if (!this.arContext) {
3.     return;
4.   }
5.   try {
6.     this.arContext.resume();
7.   } catch (error) {
8.     const err: BusinessError = error as BusinessError;
9.     console.error(`Failed to resume context. Code is ${err.code}, message is ${err.message}.`);
10.   }
11. }

### 销毁AR会话

退出AR会话和AR场景时，开发者可以使用[ARViewContext.destroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section169251835133414)方法同时销毁AR会话及AR场景。

1. private stopARView(): void {
2.   if (!this.arContext) {
3.     return;
4.   }
5.   try {
6.     this.arContext.destroy();
7.   } catch (error) {
8.     const err: BusinessError = error as BusinessError;
9.     console.error(`Failed to stop context. Code is ${err.code}, message is ${err.message}`);
10.   }
11. }

说明

组件生命周期的方法，除[aboutToAppear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttoappear)、[aboutToDisappear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#abouttodisappear)、[onPageShow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#onpageshow)、[onPageHide](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-custom-component-lifecycle#onpagehide)外，还可以使用[Navigation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-navigation)的[页面生命周期](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation#%E9%A1%B5%E9%9D%A2%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)所示方法，开发者可根据需要进行选择。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-guide "AR Engine开发指导（ArkTS）")
# 获取设备位姿

更新时间: 2025-12-16 16:34

## 概要

从5.1.0(18)开始，AR Engine支持获取设备位姿能力。

设备位姿描述了物体在真实世界中的位置和朝向。AR Engine提供了世界坐标下6自由度（6DoF）的位姿计算，包括物体的位置（沿x、y、z轴方向位移）和朝向（绕x、y、z轴旋转）。通过AR Engine，开发者可以实时获取设备在空间中任意时刻的位姿。

## 世界坐标系与位姿示意

设备位姿一般在世界坐标系下进行表示。世界坐标系描述了真实物理空间中物体的绝对位置，其正方向如图所示。

**图1** 世界坐标系示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163446.27949601274382115352690756910159:50001231000000:2800:865BECCA2416D280BD3B08A4202253954E09F04FF2416A7030B3BF373A4F327A.png)

AR Engine会自动完成世界坐标系初始化。

在AR Engine中，设备位姿由一个7维向量描述，包括旋转量![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163447.13956746960188903814577745804669:50001231000000:2800:2144DA35B1215A846E215F18ACD3F75445CD3A8B4FE2E44FDD0C2D1FC5495036.png)和位移量![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163447.68767566407486297265295013578369:50001231000000:2800:0B31F81C500E015BAE81794657CB4FDE840BFFA832289A4A38F44679FEBC21BE.png)。其中旋转量![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163447.45897212598316578672654921359889:50001231000000:2800:6B7B065EEBAADD791D12CAC9585C60858AEEB0381B9A847D79E136BE902016AB.png)是一组四元数，描述了设备相对于坐标原点的旋转状态；位移量![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163447.58179202435710519550659759540930:50001231000000:2800:9DDECBD21BB38AE6F448C7296CDC77070C27ED5BEE365D38B5F730CD56EFF36F.png)是一组三维向量，描述了设备相对于坐标原点的平移状态，如下图所示。

**图2** 设备位姿的旋转和平移变化示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163447.94108546535767328311474448945036:50001231000000:2800:82FE83A6F6CFF61C80C886C008BB2C89F6D27444DCDA2BCB4CF79E553B6BEF78.png)

通过旋转分量和平移分量，可以描述设备在空间中任意时刻的位姿状态。

## 接口说明

获取设备位姿可以通过[ARCamera](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section176984261612)相机对象获取，以下接口为获取设备位姿接口。详细接口和说明，请参考[AR Engine API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-arkts-api)。

|接口名|描述|
|:--|:--|
|[ARCamera.getPose](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section0507108132710)|获取摄像机在世界空间中的位姿信息。|

## 开发步骤

对于使用ArkTS的任何AR应用，首先需要创建一个AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，用于管理AR Engine的系统状态。AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)的创建可以参考[管理AR会话](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession)章节。

### 导入模块

获取设备位姿能力需要依赖以下模块。

1. import { arEngine, ARView, arViewController } from '@kit.AREngine';
2. import { Node, Scene, Vec3 } from '@kit.ArkGraphics3D';
3. import { BusinessError } from '@kit.BasicServicesKit';

Vec3是一个三维向量，用于存储设备的位姿信息。

### 定义变量

定义两个变量pose和stateReason，用于接收pose位姿信息和追踪失败原因。

1. let pose: arEngine.ARPose;
2. let stateReason: arEngine.ARTrackingStateReason;

### 显示预览流及设备位姿信息

首先初始化AR会话和AR场景，可以参考[初始化AR会话和AR场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession#section3391814131611)章节。

在设备界面上显示设备位姿信息及追踪失败原因，使用重复调用函数方法在设备界面上实时更新位姿和追踪失败原因的信息。

1. @Builder
2. export function ARPoseBuilder(): void {
3.   ARPose();
4. }

5. @Component
6. struct ARPose {
7.   @State arContext?: arViewController.ARViewContext = undefined;
8.   private intervalId: number = -1;
9.   // 重复调用函数时间间隔为33ms，即设定为30fps
10.   private delayInterval: number = 33;
11.   // 位姿的信息参数
12.   @State translation: Vec3 = {
13.     x: 0,
14.     y: 0,
15.     z: 0
16.   }
17.   // 追踪失败的原因
18.   @State reason: arEngine.ARTrackingStateReason = stateReason;

19.   build(): void {
20.     NavDestination() {
21.       RelativeContainer() {
22.         if (this.arContext) {
23.           ARView({ context: this.arContext })
24.             .height('100%')
25.             .width('100%')
26.             .alignRules({
27.               center: { anchor: "__container__", align: VerticalAlign.Center },
28.               middle: { anchor: "__container__", align: HorizontalAlign.Center }
29.             })

30.           // 在屏幕上显示设备位姿信息
31.           Column() {
32.             Text(`x: ${this.translation.x.toFixed(4)}`)
33.               .infoStyles()
34.             Text(`y: ${this.translation.y.toFixed(4)}`)
35.               .infoStyles()
36.             Text(`z: ${this.translation.z.toFixed(4)}`)
37.               .infoStyles()
38.             Text(`reason: ${this.reason}`)
39.               .infoStyles()
40.           }
41.           .alignItems(HorizontalAlign.Start)
42.           .margin({ left: 28, top: 28 })
43.           .alignRules({
44.             top: { anchor: "__container__", align: VerticalAlign.Top },
45.             left: { anchor: "__container__", align: HorizontalAlign.Start }
46.           })
47.         }
48.       }
49.     }
50.     .onAppear(() => {
51.       this.initARView();
52.       // 设定在30fps下更新位姿和追踪失败原因的信息
53.       this.intervalId = setInterval(() => {
54.         if (pose !== undefined) {
55.           this.translation = pose.translation;
56.           this.reason = stateReason;
57.         }
58.       }, this.delayInterval);
59.     })
60.     .onWillDisappear(() => {
61.       // 退出setInterval函数
62.       clearInterval(this.intervalId);
63.       this.stopARView();
64.     })
65.     .onShown(() => {
66.       this.resumeARView();
67.     })
68.     .onHidden(() => {
69.       this.pauseARView();
70.     })
71.     .hideTitleBar(true)
72.     .hideBackButton(true)
73.     .hideToolBar(true)
74.   }

75.   private initARView(): void {
76.     // ...
77.   }
78.   private stopARView(): void {
79.     // ...
80.   }
81.   private resumeARView(): void {
82.     // ...
83.   }
84.   private pauseARView(): void {
85.     // ...
86.   }
87. }

88. // 界面显示文本样式
89. @Extend(Text)
90. function infoStyles() {
91.   .fontColor(Color.Yellow)
92.   .fontSize(24)
93.   .textShadow({
94.     radius: 10,
95.     color: Color.Black,
96.     offsetX: 0,
97.     offsetY: 0
98.   })
99.   .textAlign(TextAlign.Start)
100. }

### 获取设备位姿信息

调用[ARViewCallback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9396615174614)，使用其中的[onFrameUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section52341758194715)方法获取AR会话对象arSession，之后通过AR会话对象arSession获取每一帧对应的设备位姿信息。

1. class ARViewCallbackImpl extends arViewController.ARViewCallback {
2.   onAnchorAdd(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
3.   }

4.   onAnchorUpdate(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
5.   }

6.   async onFrameUpdate(ctx: arViewController.ARViewContext, sysBootTs: number): Promise<void> {
7.     if (!ctx.session) {
8.       return;
9.     }

10.     let arSession: arEngine.ARSession = ctx.session; // 获取AR会话

11.     try {
12.       // 获取每一帧的设备位姿信息及追踪失败的原因
13.       let frame: arEngine.ARFrame = arSession.getFrame();
14.       pose = frame.getCamera().getPose();
15.       stateReason = frame.getCamera().stateReason;
16.     } catch (error) {
17.       const err: BusinessError = error as BusinessError;
18.       console.error(`Failed to update data. Code is ${err.code}, message is ${err.message}`);
19.     }
20.   }
21. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession "管理AR会话")
# 检测环境中的平面

更新时间: 2025-12-16 16:34

## 概要

从5.1.0(18)开始，AR Engine支持检测环境中的平面能力。

本章节介绍如何通过AR Engine进行平面检测。通过学习本章节，可以检测当前环境中的平面，并在应用中处理这些平面。

本章节涉及的AR Engine能力如下：

- 运动跟踪能力
- 环境跟踪能力（平面检测）

注意

初始化之后需要缓慢移动相机来寻找平面。

## 接口说明

检测平面通过[ARPlane](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section3392194311417)平面对象进行，以下接口为平面相关接口。详细接口和说明，请参考[AR Engine API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-arkts-api)。

|接口名|描述|
|:--|:--|
|[ARTrackable.getPose](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section14241133116264)|获取追踪目标的位姿信息。|
|[ARTrackable.getAnchors](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section10878141483010)|获取绑定到输入可跟踪对象的锚点对象。|
|[ARPose.getMatrix](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section5278038164917)|将位姿数据转换为一个4x4的矩阵。|
|[ARPlane.getPolygonXZ](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section12949442354)|获取检测到的平面2D顶点数组。|
|[ARPlane.getSubsumedBy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1127511467514)|获取平面的父平面（当平面与另一个平面合并时会生成父平面）。|
|[ARPlane.isPoseInExtents](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section102761471453)|检查给定位姿是否在平面的边界矩形内。|
|[ARPlane.isPoseInPolygon](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1471811920162)|检查给定位姿是否在平面的边界多边形内。|

## 开发步骤

AR Engine仅输出识别到的平面数据。为便于用户观察，开发者可使用AGP（Ark Graphics Platform）渲染引擎或者[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent)绘制识别的平面。关于AGP的介绍可以查看[ArkGraphics 3D简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkgraphics3d-overview)和[AGP引擎](https://gitcode.com/openharmony/graphic_graphic_3d)。

对于使用ArkTS的任何AR应用，首先需要创建一个AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，用于管理AR Engine的系统状态。AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)的创建可以参考[管理AR会话](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession)章节。

### 导入模块

平面检测能力所需的模块导入如下：

1. import { arEngine, ARView, arViewController } from '@kit.AREngine';
2. import { Node, Scene, Vec3 } from '@kit.ArkGraphics3D';
3. import { BusinessError } from '@kit.BasicServicesKit';
4. import { Matrix4 } from '@kit.ArkUI';

### 显示预览流

首先初始化AR会话和AR场景，可以参考[初始化AR会话和AR场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession#section3391814131611)章节。

1. @Builder
2. export function ARPlaneBuilder(): void {
3.   ARPlane();
4. }

5. @Component
6. struct ARPlane {
7.   @State arContext?: arViewController.ARViewContext = undefined;

8.   build(): void {
9.     // ...
10.   }

11.   private initARView(): void {
12.     // ...
13.   }
14.   private stopARView(): void {
15.     // ...
16.   }
17.   private resumeARView(): void {
18.     // ...
19.   }
20.   private pauseARView(): void {
21.     // ...
22.   }
23. }

### 检测环境平面

调用[ARViewCallback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9396615174614)，使用其中的[onFrameUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section52341758194715)方法进行帧数据更新，通过[ARSession.getAllTrackables](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section559349112710)方法获取所有识别到的平面。

1. class ARViewCallbackImpl extends arViewController.ARViewCallback {
2.   onAnchorAdd(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
3.   }

4.   onAnchorUpdate(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
5.   }

6.   async onFrameUpdate(ctx: arViewController.ARViewContext, sysBootTs: number): Promise<void> {
7.     if (!ctx.session) {
8.       return;
9.     }

10.     let arSession: arEngine.ARSession = ctx.session;

11.     try {
12.       let frame: arEngine.ARFrame = arSession.getFrame();
13.       let camera: arEngine.ARCamera = frame.getCamera();
14.       let trackable: arEngine.ARTrackable[] = [];

15.       if (camera.state === arEngine.ARTrackingState.TRACKING) {
16.         trackable = arSession.getAllTrackables(arEngine.ARTrackableType.PLANE);
17.         console.info(`Succeeded in getting tracking plane, length is: ${trackable.length}`);  // 打印当前识别到的平面数量
18.       }

19.     } catch (error) {
20.       const err: BusinessError = error as BusinessError;
21.       console.error(`Failed to update data. Code is ${err.code}, message is ${err.message}.`);
22.     }
23.   }
24. }

### 检测平面的自定义方法

自定义方法获取顶点数据getVertices、创建索引generateMeshIndex、创建mesh数据generateMeshInput。

1. // 获取三维空间顶点坐标，第一个入参的位姿矩阵按垂直列排列，第二个坐标点为(x, 0, z, 1)，对应x-z平面。
2. export function getVertices(mat: Matrix4, point: number[]): Vec3[] {
3.   let result: Vec3[] = [];
4.   for (let i = 0; i < point.length; i += 2) {
5.     let single: Vec3 = {
6.       x: (mat[2] * point[i] + mat[6] * 0
7.         + mat[10] * point[i + 1] + mat[14] * 1.0),
8.       y: mat[1] * point[i] + mat[5] * 0
9.         + mat[9] * point[i + 1] + mat[13] * 1.0,
10.       z: -(mat[0] * point[i] + mat[4] * 0
11.         + mat[8] * point[i + 1] + mat[12] * 1.0),
12.     }
13.     result.push(single);
14.   }
15.   return result;
16. }
17. // 创建 ARWorld 的 mesh索引。由于平面是由三角形拼接而成的，因此每个平面上的每个三角形的首个顶点索引都是相同的。
18. export function generateMeshIndex(input: Vec3[][]): number[] {
19.   let result: number[] = [];
20.   let start: number = 0;

21.   for (let i = 0; i < input.length; i++) {
22.     let length: number = input[i].length;

23.     for (let j = start + 1; j < start + length - 1; j++) {
24.       result.push(start);
25.       result.push(j);
26.       result.push(j + 1);
27.     }
28.     start += length;
29.   }
30.   return result;
31. }

32. export function generateMeshInput(vex: Vec3[][]): Vec3[] {
33.   let result: Vec3[] = [];
34.   for (let i = 0; i < vex.length; i++) {
35.     let tmp: Vec3[] = vex[i];
36.     for (let j = 0; j < tmp.length; j++) {
37.       result.push(tmp[j]);
38.     }
39.   }
40.   return result;
41. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-get-pose "获取设备位姿")
# 识别平面语义

更新时间: 2025-12-16 16:34

## 概要

从5.1.0(18)开始，AR Engine支持识别平面语义能力。

对于检测到的平面，开发者可以通过AR Engine识别该平面的语义，语义类型包括墙面、地面、座椅、桌面、天花板、门、窗户、床、平面空间、立方体体积、立方体空间容积和未知类型（平面空间、立方体体积和立方体空间容积仅在高精几何重建模式下支持）。

## 接口说明

获取平面语义信息可以通过[ARPlane](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section3392194311417)平面对象获取，以下接口为平面相关接口。详细接口和说明，请参考[AR Engine API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-arkts-api)。

|接口名|描述|
|:--|:--|
|[ARTrackable.getPose](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section14241133116264)|获取追踪目标的位姿信息。|
|[ARTrackable.getAnchors](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section10878141483010)|获取绑定到输入可跟踪对象的锚点对象。|
|[ARPose.getMatrix](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section5278038164917)|将位姿数据转换为一个4x4的矩阵。|
|[ARPlane.getPolygonXZ](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section12949442354)|获取检测到的平面2D顶点数组。|
|[ARPlane.getSubsumedBy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1127511467514)|获取平面的父平面（当平面与另一个平面合并时会生成父平面）。|
|[ARPlane.isPoseInExtents](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section102761471453)|检查给定位姿是否在平面的边界矩形内。|
|[ARPlane.isPoseInPolygon](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1471811920162)|检查给定位姿是否在平面的边界多边形内。|

## 开发步骤

AR Engine仅输出识别到的平面数据。为便于用户观察，开发者可使用AGP（Ark Graphics Platform）渲染引擎或者[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent)绘制识别的平面。关于AGP的介绍可以查看[ArkGraphics 3D简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkgraphics3d-overview)和[AGP引擎](https://gitcode.com/openharmony/graphic_graphic_3d)。

对于使用ArkTS的任何AR应用，首先需要创建一个AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，用于管理AR Engine的系统状态。AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)的创建可以参考[管理AR会话](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession)章节。

识别平面语义之前需要先检测识别环境中的平面，如何检测识别环境中的平面请参考[检测环境中的平面](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-get-plane)。

### 导入模块

识别平面语义能力所需要导入的模块如下：

1. import { arEngine, ARView, arViewController } from '@kit.AREngine';
2. import { Node, Scene } from '@kit.ArkGraphics3D';
3. import { BusinessError } from '@kit.BasicServicesKit';

### 定义变量

定义变量planeLabel接收平面类型标签信息。

1. let planeLabel: arEngine.ARSemanticPlaneLabel;

### 显示平面语义信息

首先初始化AR会话和AR场景，可以参考[初始化AR会话和AR场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession#section3391814131611)章节。

更改semanticMode为[ARSemanticMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section19325205718138).PLANE，启用平面语义识别能力。

在设备界面上显示识别到平面的信息，使用重复调用函数方法在设备界面上实时更新识别到的平面语义信息。

1. @Builder
2. export function ARTargetBuilder(): void {
3.   ARTarget();
4. }

5. @Component
6. struct ARTarget {
7.   @State arContext?: arViewController.ARViewContext = undefined;
8.   // 平面类型
9.   @State targetPlaneLabel: arEngine.ARSemanticPlaneLabel = planeLabel;
10.   private intervalId: number = -1;
11.   // 重复调用函数时间间隔为33ms，即设定为30fps
12.   private delayInterval: number = 33;

13.   build(): void {
14.     NavDestination() {
15.       RelativeContainer() {
16.         if (this.arContext) {
17.           ARView({ context: this.arContext })
18.             .height('100%')
19.             .width('100%')
20.             .alignRules({
21.               center: { anchor: '__container__', align: VerticalAlign.Center },
22.               middle: { anchor: '__container__', align: HorizontalAlign.Center }
23.             })

24.           // 在屏幕底部显示识别的平面信息
25.           Column() {
26.             Text(`Label: ${convertSemanticLabel(this.targetPlaneLabel)}`)
27.               .infoStyles()
28.           }
29.           .alignItems(HorizontalAlign.Center)
30.           .margin({ bottom: 10 })
31.           .alignRules({
32.             bottom: { anchor: "__container__", align: VerticalAlign.Bottom },
33.             middle: { anchor: "__container__", align: HorizontalAlign.Center }
34.           })
35.         }
36.       }
37.     }
38.     .onAppear(() => {
39.       this.initARView();
40.       // 设定在30fps下更新识别平面语义信息
41.       this.intervalId = setInterval(async () => {
42.         this.targetPlaneLabel = planeLabel;
43.       }, this.delayInterval);
44.     })
45.     .onWillDisappear(() => {
46.       // 退出setInterval函数
47.       clearInterval(this.intervalId);
48.       this.stopARView();
49.     })
50.     .onShown(() => {
51.       this.resumeARView();
52.     })
53.     .onHidden(() => {
54.       this.pauseARView();
55.     })
56.     .hideTitleBar(true)
57.     .hideBackButton(true)
58.     .hideToolBar(true)
59.   }

60.   private initARView(): void {
61.     Scene.load().then(async (scene: Scene) => {
62.       let viewContext: arViewController.ARViewContext = new arViewController.ARViewContext();
63.       viewContext.scene = scene;
64.       viewContext.callback = new ARViewCallbackImpl();
65.       viewContext.config = {
66.         type: arEngine.ARType.WORLD,
67.         planeFindingMode: arEngine.ARPlaneFindingMode.HORIZONTAL_AND_VERTICAL,
68.         powerMode: arEngine.ARPowerMode.NORMAL,
69.         semanticMode: arEngine.ARSemanticMode.PLANE, // 识别平面语义
70.         poseMode: arEngine.ARPoseMode.GRAVITY,
71.         depthMode: arEngine.ARDepthMode.AUTOMATIC,
72.         meshMode: arEngine.ARMeshMode.DISABLED,
73.         focusMode: arEngine.ARFocusMode.AUTO
74.       }
75.       viewContext.init().then(() => {
76.         this.arContext = viewContext;
77.         console.info('Succeeded in initializing ARView.');
78.       }).catch((err: BusinessError) => {
79.         console.error(`Failed to init ARView. Code is ${err.code}, message is ${err.message}.`);
80.       })
81.     })
82.   }

83.   private stopARView(): void {
84.     // ...
85.   }
86.   private resumeARView(): void {
87.     // ...
88.   }
89.   private pauseARView(): void {
90.     // ...
91.   }
92. }

93. // 界面显示文本样式
94. @Extend(Text)
95. function infoStyles() {
96.   .fontColor(Color.Yellow)
97.   .fontSize(24)
98.   .textShadow({
99.     radius: 10,
100.     color: Color.Black,
101.     offsetX: 0,
102.     offsetY: 0
103.   })
104.   .textAlign(TextAlign.Start)
105. }

### 获取语义信息

调用[ARViewCallback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9396615174614)，使用其中的[onFrameUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section52341758194715)方法进行帧数据更新，在设备界面上显示识别到的平面类型。

增加获取语义信息的方法plane.label，获取每一帧识别到的平面语义信息。

1. class ARViewCallbackImpl extends arViewController.ARViewCallback {
2.   onAnchorAdd(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
3.   }

4.   onAnchorUpdate(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
5.   }

6.   async onFrameUpdate(ctx: arViewController.ARViewContext, sysBootTs: number): Promise<void> {
7.     if (!ctx.session) {
8.       return;
9.     }

10.     let arSession: arEngine.ARSession = ctx.session;

11.     try {
12.       let frame: arEngine.ARFrame = arSession.getFrame();
13.       let camera: arEngine.ARCamera = frame.getCamera();
14.       let trackable: arEngine.ARTrackable[] = [];

15.       if (camera.state === arEngine.ARTrackingState.TRACKING) {
16.         trackable = arSession.getAllTrackables(arEngine.ARTrackableType.PLANE);
17.         console.info(`Succeeded in getting tracking plane, length is: ${trackable.length}`);
18.       }

19.       for (let i = 0; i < trackable.length; ++i) {
20.         let plane: arEngine.ARPlane = trackable[i] as arEngine.ARPlane;

21.         // 更新识别的平面语义信息
22.         planeLabel = plane.label;
23.         console.info(`Succeeded in updating frame data for loop: ${plane.label}`);
24.       }

25.     } catch (error) {
26.       const err: BusinessError = error as BusinessError;
27.       console.error(`Failed to update data. Code is ${err.code}, message is ${err.message}.`);
28.     }
29.   }
30. }

### 识别平面语义的自定义方法

自定义方法获取顶点数据getVertices、创建索引generateMeshIndex、创建mesh数据generateMeshInput，可参考[检测平面的自定义方法](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-get-plane#section142331216260)。

arrayBufferFloat32ToNumber可以参考[数据类型转换说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arraybuffer-info)。

平面语义标签转换convertSemanticLabel可参考如下。

1. function convertSemanticLabel(obj: number): string {
2.   let res: string = '';
3.   if (obj === 0) {
4.     res = 'UNKNOWN';
5.   } else if (obj === 1) {
6.     res = 'WALL';
7.   } else if (obj === 2) {
8.     res = 'FLOOR';
9.   } else if (obj === 3) {
10.     res = 'SEAT';
11.   } else if (obj === 4) {
12.     res = 'TABLE';
13.   } else if (obj === 5) {
14.     res = 'CEILING';
15.   } else if (obj === 6) {
16.     res = 'DOOR';
17.   } else if (obj === 7) {
18.     res = 'WINDOW';
19.   } else if (obj === 8) {
20.     res = 'BED';
21.   } else if (obj === 9) {
22.     res = 'PLANE SPACE';
23.   } else if (obj === 10) {
24.     res = 'CUBE VOLUME';
25.   } else if (obj === 11) {
26.     res = 'CUBE SPACE';
27.   }
28.   return res;
29. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-get-plane "检测环境中的平面")
# 获取深度估计信息

更新时间: 2025-12-16 16:34

## 概要

从5.1.0(18)开始，AR Engine支持获取深度估计信息能力。

AR Engine提供的深度估计功能通过算法输出深度估计数据（物体表面离相机的距离）和深度置信度信息，为开发者提供环境三维感知能力。该技术可应用于测量、体积估算、场景重建等场景。基于空间物体的深度信息，开发者可完成一些空间计算任务，比如计算物体体积等。

开发者如果需要使用获取深度图功能请使用NAPI进行开发，参见[获取深度图](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-c-get-depth)。ArkTS API将于后期版本上线深度图能力。

**图1** 深度估计信息示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163452.32515488953511282635803047815927:50001231000000:2800:95EDE9422C3C15572D23EB737929E2A7C00C97A8933D07BF23F0898891809296.png)

注意

本功能仅提供能力，接入该功能不构成对产品的质量保证或任何承诺，详见[AR Engine深度估计功能技术局限性及免责声明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-appendix#section1854314717219)。

本章节涉及的AR Engine能力如下：

- 运动跟踪能力
- 环境跟踪能力（平面检测）

## 接口说明

获取深度估计信息可以通过[ARFrame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section83421523123819)帧对象获取，以下接口为深度估计相关接口。详细接口和说明，请参考[AR Engine API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-arkts-api)。

|接口名|描述|
|:--|:--|
|[ARSession.getFrame](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section114051108916)|获取AR Engine处理后的一帧数据。|
|[ARFrame.acquireDepthImage16Bits](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section8978424152512)|获取当前帧对应的深度图像对象。|
|[ARFrame.acquireDepthConfidenceImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section58412318287)|获取当前帧的深度置信度图像。|

## 开发步骤

对于使用ArkTS的任何AR应用，首先需要创建一个AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，用于管理AR Engine的系统状态。AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)的创建可以参考[管理AR会话](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession)章节。

### 导入模块

获取深度估计信息能力所需的模块导入方法如下：

1. import { arEngine, ARView, arViewController } from '@kit.AREngine';
2. import { Node, Scene } from '@kit.ArkGraphics3D';
3. import { BusinessError } from '@kit.BasicServicesKit';

### 定义变量

定义变量centerDistance深度估计距离和centerConfidence深度置信度。

1. let centerDistance: number;
2. let centerConfidence: number;

### 显示深度估计信息

首先初始化AR会话和AR场景，可以参考[初始化AR会话和AR场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession#section3391814131611)章节。

在设备界面上显示深度估计信息及深度置信度信息，使用重复调用函数方法在设备界面上实时更新深度估计信息及置信度信息。

1. @Builder
2. export function ARDepthBuilder(): void {
3.   ARDepth();
4. }

5. @Component
6. struct ARDepth {
7.   private delayInterval: number = 33;
8.   private intervalId: number = -1;
9.   @State arContext?: arViewController.ARViewContext = undefined;
10.   @State depthConfidence: number = 0;
11.   @State depthDistance: string = '0';

12.   build(): void {
13.     NavDestination() {
14.       RelativeContainer() {
15.         if (this.arContext) {
16.           ARView({ context: this.arContext })
17.             .height('100%')
18.             .width('100%')
19.             .alignRules({
20.               center: { anchor: "__container__", align: VerticalAlign.Center },
21.               middle: { anchor: "__container__", align: HorizontalAlign.Center }
22.             })

23.           // 在屏幕上显示中心点、深度估计值及置信度
24.           Text('●')
25.             .fontSize(8)
26.             .fontColor(Color.Red)
27.             .alignRules({
28.               center: { anchor: '__container__', align: VerticalAlign.Center },
29.               middle: { anchor: '__container__', align: HorizontalAlign.Center }
30.             })

31.           Column() {
32.             Text(`${this.depthDistance} | ${this.depthConfidence}`)
33.               .fontColor(Color.Yellow)
34.               .fontSize(24)
35.               .textShadow({
36.                 radius: 10,
37.                 color: Color.Black,
38.                 offsetX: 0,
39.                 offsetY: 0
40.               })
41.           }
42.           .alignItems(HorizontalAlign.Center)
43.           .margin({ bottom: 10 })
44.           .alignRules({
45.             bottom: { anchor: "__container__", align: VerticalAlign.Bottom },
46.             middle: { anchor: "__container__", align: HorizontalAlign.Center }
47.           })
48.         }
49.       }
50.     }
51.     .onAppear(() => {
52.       this.initARView();
53.       this.renderDepthMsg();
54.     })
55.     .onWillAppear(() => {
56.       this.stopARView();
57.     })
58.     .onShown(() => {
59.       this.resumeARView();
60.     })
61.     .onHidden(() => {
62.       this.pauseARView();
63.     })
64.     .hideTitleBar(true)
65.     .hideBackButton(true)
66.     .hideToolBar(true)
67.   }

68.   private initARView(): void {
69.     Scene.load().then(async (scene: Scene) => {
70.       let viewContext: arViewController.ARViewContext = new arViewController.ARViewContext();
71.       viewContext.scene = scene;
72.       viewContext.callback = new ARViewCallbackImpl();
73.       viewContext.config = {
74.         type: arEngine.ARType.WORLD,
75.         planeFindingMode: arEngine.ARPlaneFindingMode.HORIZONTAL_AND_VERTICAL,
76.         powerMode: arEngine.ARPowerMode.NORMAL,
77.         semanticMode: arEngine.ARSemanticMode.NONE,
78.         poseMode: arEngine.ARPoseMode.GRAVITY,
79.         depthMode: arEngine.ARDepthMode.AUTOMATIC,
80.         meshMode: arEngine.ARMeshMode.DISABLED,
81.         focusMode: arEngine.ARFocusMode.AUTO
82.       }
83.       viewContext.init().then(() => {
84.         this.arContext = viewContext;
85.         console.info('Succeeded in initializing ARView.');
86.       }).catch((err: BusinessError) => {
87.         console.error(`Failed to init ARView. Code is ${err.code}, message is ${err.message}`);
88.       })
89.     })
90.   }

91.   private renderDepthMsg(): void {
92.     this.intervalId = setInterval(() => {
93.       if (centerDistance === undefined || centerConfidence === undefined) {
94.         return;
95.       }
96.       this.depthDistance = centerDistance.toFixed(4);
97.       this.depthConfidence = centerConfidence;
98.     }, this.delayInterval)
99.   }

100.   private stopARView(): void {
101.     if (!this.arContext) {
102.       return;
103.     }
104.     try {
105.       clearInterval(this.intervalId);
106.       this.arContext.destroy();
107.       centerDistance = 0;
108.       centerConfidence = 0;
109.     } catch (error) {
110.       const err: BusinessError = error as BusinessError;
111.       console.error(`Failed to stop context. Code is ${err.code}, message is ${err.message}`);
112.     }
113.   }

114.   private resumeARView(): void {
115.     // ...
116.   }
117.   private pauseARView(): void {
118.     // ...
119.   }
120. }

### 获取深度估计信息

调用[ARViewCallback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9396615174614)，使用其中的[onFrameUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section52341758194715)方法获取到AR会话对象后进行深度估计，获取深度信息、置信度信息。

1. class ARViewCallbackImpl extends arViewController.ARViewCallback {
2.   onAnchorAdd(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
3.   }

4.   onAnchorUpdate(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
5.   }

6.   async onFrameUpdate(ctx: arViewController.ARViewContext, sysBootTs: number): Promise<void> {
7.     if (!ctx.session) {
8.       return;
9.     }

10.     let session: arEngine.ARSession | undefined = ctx.session;

11.     try {
12.       let frame: arEngine.ARFrame = session.getFrame();
13.       let depthImage: arEngine.ARImage = frame.acquireDepthImage16Bits();
14.       let confidenceImage: arEngine.ARImage = frame.acquireDepthConfidenceImage();
15.       let depthPlane: number[] = arrayBufferInt32ToNumber(depthImage.planes[0].buffer);
16.       let confidencePlane: number[] = arrayBufferInt32ToNumber(confidenceImage.planes[0].buffer);
17.       const index: number = depthImage.height * depthImage.width / 2 + depthImage.width / 2;

18.       centerDistance = depthPlane[index] / 1000;
19.       centerConfidence = confidencePlane[index];
20.     } catch (error) {
21.       const err: BusinessError = error as BusinessError;
22.       console.error(`Failed to acquire depth information. Code is ${err.code}, message is ${err.message}`);
23.     }
24.   }
25. }

### 获取深度估计信息的自定义方法

自定义数据转换方法arrayBufferInt32ToNumber可参考[数据类型转换说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arraybuffer-info)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-get-semantics "识别平面语义")
# 获取网格扫描信息

更新时间: 2025-12-16 16:34

## 概要

从5.1.0(18)开始，AR Engine支持获取网格扫描信息能力。

本章节介绍如何获取目标物体的网格（mesh）扫描数据信息，通过学习本章节，可以检测当前环境中的自由曲面，并在应用中处理这些曲面信息。

**图1** 环境网格扫描示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163452.77480662564778514706610146876558:50001231000000:2800:F42FD087AEAA1FABA5D236E192AA3F9ABC195B7EFC3E5859C192235A08B0CA87.png)

本章节涉及的AR Engine能力如下：

- 运动跟踪能力
- 环境跟踪能力（平面检测）
- 命中检测能力

## 接口说明

网格扫描主要依赖[ARSceneMesh](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section81184417712)，以下接口为AR网格扫描相关接口。详细接口和说明，请参考[AR Engine API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-arkts-api)。

|接口名|描述|
|:--|:--|
|[ARSceneMesh.getVertices](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section15211205153115)|获取场景网格中的顶点坐标数据。|
|[ARSceneMesh.getVertexNormals](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section4793111183211)|获取场景网格中的顶点法线坐标数据。|
|[ARSceneMesh.getTriangleIndices](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section19221187183218)|获取场景网格中的三角形索引数据。|
|[ARSceneMesh.release](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section625851110329)|释放环境网格数据对象。|
|[ARFrame.hitTest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section20353182861218)|根据相机投射光线，获取预览区域中的像素坐标（pixelX和pixelY）来确定射线方向，然后检测这个射线在平面或点云中是否有交点。|
|[ARHitResult.getHitPose](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1864219177109)|获取交点位姿。|
|[ARHitResult.getTrackable](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section727122311104)|获取被命中的可追踪对象。|
|[ARHitResult.createAnchor](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section12541329171017)|在交点（intersection）创建一个锚点。|
|[ARHitResult.release](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1690193413100)|释放命中检测结果对象占用的内存。|
|[ARPose.getMatrix](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section5278038164917)|将位姿数据转换为一个4x4的矩阵。|
|[ARPose.release](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section22831038104913)|释放位姿对象占用的内存。|

## 开发步骤

AR Engine仅输出识别到的平面数据。为便于用户观察，开发者可使用AGP（Ark Graphics Platform）渲染引擎或者[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent)绘制识别的平面。关于AGP的介绍可以查看[ArkGraphics 3D简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkgraphics3d-overview)和[AGP引擎](https://gitcode.com/openharmony/graphic_graphic_3d)。

对于使用ArkTS的任何AR应用，首先需要创建一个AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，用于管理AR Engine的系统状态。AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)的创建可以参考[管理AR会话](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession)章节。

### 导入模块

网格扫描能力所需要导入的模块如下：

1. import { arEngine, ARView, arViewController } from '@kit.AREngine';
2. import { Node, Scene, Vec3 } from '@kit.ArkGraphics3D';
3. import { window } from '@kit.ArkUI';
4. import { BusinessError } from '@kit.BasicServicesKit';

### 定义变量

定义变量hitAnchorList存储放置物体处的锚点信息、hitPoseList存储放置物体处的位姿信息和statusBarHeight设备状态栏高度。

用户点击设备的坐标和显示预览流的坐标不一致，预览流的窗口略小于设备屏幕，因此需要减去设备状态栏高度以获取准确的点击坐标。

1. let frame: arEngine.ARFrame;
2. let hitAnchorList: arEngine.ARAnchor[] = [];
3. let hitPoseList: Vec3[] = [];
4. let statusBarHeight: number = 0;

### 显示预览流

首先初始化AR会话和AR场景，可以参考[初始化AR会话和AR场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession#section3391814131611)章节。

1. @Builder
2. export function ARMeshBuilder(): void {
3.   ARMesh();
4. }

5. @Component
6. struct ARMesh {
7.   @State arContext?: arViewController.ARViewContext = undefined;
8.   @State context: Context = this.getUIContext().getHostContext() as Context;

9.   build(): void {
10.     NavDestination() {
11.       RelativeContainer() {
12.         if (this.arContext) {
13.           ARView({ context: this.arContext })
14.             .height('100%')
15.             .width('100%')
16.             .alignRules({
17.               center: { anchor: '__container__', align: VerticalAlign.Center },
18.               middle: { anchor: '__container__', align: HorizontalAlign.Center }
19.             })
20.             .onClick((event) => {
21.               this.objectCollisionDetection(event);
22.             })
23.         }
24.       }
25.     }
26.     .onAppear(() => {
27.       this.initARView();
28.       this.getAvoidArea();
29.     })
30.     .onWillDisappear(() => {
31.       this.stopARView();
32.     })
33.     .onShown(() => {
34.       this.resumeARView();
35.     })
36.     .onHidden(() => {
37.       this.pauseARView();
38.     })
39.     .hideTitleBar(true)
40.     .hideBackButton(true)
41.     .hideToolBar(true)
42.   }

43.   // 获取用户点击坐标，获取碰撞检测结果
44.   private objectCollisionDetection(event: ClickEvent): void {
45.     let x: number = this.getUIContext().vp2px(event.windowX);
46.     let y: number = this.getUIContext().vp2px(event.windowY) - statusBarHeight;
47.     console.info(`Get onclick position, x: ${x} y: ${y}.`);

48.     try {
49.       let result: arEngine.ARHitResult[] = frame.hitTest(x, y);
50.       console.info(`The hitResult size is: ${result.length}.`);
51.       if (!result) {
52.         return;
53.       }

54.       for (let i = 0; i < result.length; i++) {
55.         let hitResult: arEngine.ARHitResult = result[i];
56.         let distance: number = hitResult.distance;

57.         if (distance <= 0) {
58.           continue;
59.         }

60.         let hitAnchor: arEngine.ARAnchor = hitResult.createAnchor();
61.         let pos: Vec3 = hitAnchor.getPose().translation;

62.         hitPoseList.push(pos);
63.         hitAnchorList.push(hitAnchor);

64.       }
65.       console.info('Succeeded in getting hit result.');  // 成功获取碰撞目标
66.     } catch (error) {
67.       const err: BusinessError = error as BusinessError;
68.       console.error(`Failed to get hitResults. Code is ${err.code}, message is ${err.message}`);
69.     }
70.   }

71.   private initARView(): void {
72.     Scene.load().then(async (scene: Scene) => {
73.       let viewContext: arViewController.ARViewContext = new arViewController.ARViewContext();
74.       viewContext.scene = scene;
75.       viewContext.callback = new ARViewCallbackImpl();
76.       viewContext.config = {
77.         type: arEngine.ARType.WORLD,
78.         planeFindingMode: arEngine.ARPlaneFindingMode.HORIZONTAL_AND_VERTICAL,
79.         powerMode: arEngine.ARPowerMode.NORMAL,
80.         semanticMode: arEngine.ARSemanticMode.NONE,
81.         poseMode: arEngine.ARPoseMode.GRAVITY,
82.         depthMode: arEngine.ARDepthMode.AUTOMATIC,
83.         meshMode: arEngine.ARMeshMode.ENABLE,  // 开启mesh
84.         focusMode: arEngine.ARFocusMode.AUTO
85.       }
86.       viewContext.init().then(() => {
87.         this.arContext = viewContext;
88.         console.info('Succeeded in initializing ARView.');
89.       }).catch((err: BusinessError) => {
90.         console.error(`Failed to init ARView. Code is ${err.code}, message is ${err.message}.`);
91.       })
92.     })
93.   }

94.   // 获取屏幕上减去状态栏的真实高度（预览流高度）
95.   private getAvoidArea(): void {
96.     let avoidAreaType: window.AvoidAreaType = window.AvoidAreaType.TYPE_SYSTEM;
97.     window.getLastWindow(this.context).then((data) => {
98.       // 获取顶部状态栏高度
99.       let avoidArea1: window.AvoidArea = data.getWindowAvoidArea(avoidAreaType);
100.       statusBarHeight = avoidArea1.topRect.height;
101.       console.info(`The statusBarHeight is ${statusBarHeight}.`);
102.     }).catch((err: BusinessError) => {
103.       console.error(`Failed to obtain the window. Code is ${err.code}, message is ${err.message}.`);
104.     })
105.   }

106.   private stopARView(): void {
107.     // ...
108.   }
109.   private resumeARView(): void {
110.     // ...
111.   }
112.   private pauseARView(): void {
113.     // ...
114.   }
115. }

### 获取mesh网格数据

调用[ARViewCallback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9396615174614)，使用其中的[onFrameUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section52341758194715)方法进行帧数据更新，获取mesh网格数据。

1. class ARViewCallbackImpl extends arViewController.ARViewCallback {
2.   onAnchorAdd(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
3.   }

4.   onAnchorUpdate(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
5.   }

6.   async onFrameUpdate(ctx: arViewController.ARViewContext, sysBootTs: number): Promise<void> {
7.     let planeVertices: number[] = [];
8.     let vertexNormals: number[] = [];
9.     let triangleIndices: number[] = [];

10.     if (!ctx.session) {
11.       return;
12.     }

13.     let session: arEngine.ARSession | undefined = ctx.session;

14.     try {
15.       frame = session.getFrame();
16.       let camera: arEngine.ARCamera = frame.getCamera();
17.       let sceneMesh: arEngine.ARSceneMesh = frame.acquireSceneMesh();

18.       if (camera.state === arEngine.ARTrackingState.TRACKING) {
19.         planeVertices = arrayBufferFloat32ToNumber(sceneMesh.getVertices());
20.         triangleIndices = arrayBufferInt32ToNumber(sceneMesh.getTriangleIndices());
21.         vertexNormals = arrayBufferFloat32ToNumber(sceneMesh.getVertexNormals());

22.         // 输出mesh数据
23.         console.info(`The mesh data planeVertices is: ${planeVertices}, triangleIndices is: ${triangleIndices},
24.           vertexNormals is: ${vertexNormals}.`);
25.       }

26.     } catch (error) {
27.       const err: BusinessError = error as BusinessError;
28.       console.error(`Failed to acquire depth information. Code is ${err.code}, message is ${err.message}.`);
29.     }
30.   }
31. }

### 获取网格扫描信息的自定义方法

自定义数据转换方法arrayBufferFloat32ToNumber及arrayBufferInt32ToNumber可以参考[数据类型转换说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arraybuffer-info)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-get-depth "获取深度估计信息")
# 图像跟踪

更新时间: 2025-12-16 16:34

## 概要

从5.1.0(18)开始，AR Engine支持获取图像跟踪能力。

本章节介绍如何识别2D图像（二维图像）并跟踪其位姿信息，通过学习本章节，可以检测场景中是否存在输入的图像，识别之后输出图像的位姿。

**图1** 图像跟踪示意图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163452.72194650817536511837604239001792:50001231000000:2800:3D1C3CD6D2626216AE29AC361D1A2CB9CB74F9E1BD1FCB17E48D23A12DA38D37.png)

本章节涉及的AR Engine能力如下：

- 运动跟踪能力
- 环境跟踪能力（平面检测）

## 接口说明

图像识别主要依赖[ARAugmentedImageDatabase](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1410345414514)、[ARImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section3211104815419)，以下接口为图像识别相关接口。详细接口和说明，请参考[AR Engine API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-arkts-api)。

|接口名|描述|
|:--|:--|
|[arEngine.createARAugmentedImageDatabase](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section204881041154517)|创建一个增强型图像数据库。|
|[ARAugmentedImageDatabase.deserialize](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section11965134812716)|将增强图像数据库缓冲区反序列化为一个新的增强图像数据库对象。|
|[ARAugmentedImageDatabase.serialize](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section18164121486)|将增强图像数据库序列化为一个缓冲区。|
|[ARAugmentedImageDatabase.addImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section9315052814)|将图像添加到图像数据库，并输出对应图像的索引。|
|[ARAugmentedImageDatabase.getImageCount](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section106577102812)|获取图像数据库中图像的数量。|
|[ARAugmentedImageDatabase.getCapacity](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section87071617088)|可以添加的最大图像数量。|
|[ARAugmentedImageDatabase.getImageAddMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section121563216515)|获取图片添加模式。|
|[ARAugmentedImageDatabase.setImageAddMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section15149542135910)|设置图片添加模式。|
|[ARAugmentedImageDatabase.release](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section72331823587)|释放增强图像数据库对象[ARAugmentedImageDatabase](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1410345414514)占用的内存。|
|[ARImage.release](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1060545815466)|释放相机视频流帧对象[ARImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section3211104815419)占用的内存。|
|[ARAugmentedImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1570811755212)|表示可被追踪的增强图像对象。|

## 开发步骤

AR Engine仅输出识别到的平面数据。为便于用户观察，开发者可使用AGP（Ark Graphics Platform）渲染引擎或者[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent)绘制识别的平面。关于AGP的介绍可以查看[ArkGraphics 3D简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkgraphics3d-overview)和[AGP引擎](https://gitcode.com/openharmony/graphic_graphic_3d)。

对于使用ArkTS的任何AR应用，首先需要创建一个AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，用于管理AR Engine的系统状态。AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)的创建可以参考[管理AR会话](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession)章节。

### 创建UI页面

首先创建一个初始UI页面“ARImage.ets”，设置两个按钮，用于实现“添加本地图片”和“读取本地数据库”两个功能，分别命名“ARImageByAdd.ets”和“ARImageByDatabase.ets”。并配置路由进行页面间跳转，页面路由配置详细可查看[组件导航(Navigation) (推荐)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-navigation-navigation)。

### ARImage页面

1. // ARImage.ets
2. // 导入图片模块
3. import { photoAccessHelper } from '@kit.MediaLibraryKit';

4. @Builder
5. export function ARImageBuilder(): void {
6.   ARImage();
7. }

8. @Component
9. struct ARImage {
10.   pageInfo: NavPathStack = new NavPathStack();

11.   // UI配置
12.   build(): void {
13.     NavDestination() {
14.       Column() {
15.         Button('选择本地图片', { type: ButtonType.Normal, stateEffect: true })
16.           .borderRadius(8)
17.           .width('50%')
18.           .height('5%')
19.           .onClick(() => {
20.             this.chooseImageToTrack();
21.           })

22.         Button('加载本地数据库', { type: ButtonType.Normal, stateEffect: true })
23.           .borderRadius(8)
24.           .width('50%')
25.           .height('5%')
26.           .onClick(() => {
27.             this.loadDatabaseToTrack();
28.           })
29.       }
30.       .justifyContent(FlexAlign.SpaceEvenly)
31.       .width('100%')
32.       .height('100%')
33.     }
34.     .onReady((context: NavDestinationContext) => {
35.       this.pageInfo = context.pathStack;
36.     })
37.     .hideTitleBar(true)
38.     .hideBackButton(true)
39.     .hideToolBar(true)
40.   }

41.   // 选择本地图片模式
42.   private chooseImageToTrack(): void {
43.     try {
44.       let photoOption: photoAccessHelper.PhotoSelectOptions = new photoAccessHelper.PhotoSelectOptions();
45.       photoOption.MIMEType = photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE;
46.       photoOption.maxSelectNumber = 50; // Default
47.       photoOption.isEditSupported = false;
48.       let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();

49.       photoPicker.select(photoOption).then((photoResult) => {
50.         if (photoResult.photoUris.length > 0 && photoResult.photoUris[0].length > 0) {
51.           this.pageInfo.pushDestinationByName('ARImageByAdd', photoResult.photoUris);
52.         }
53.       })
54.     } catch (error) {
55.       console.error(`Failed to select by photoPicker. Code: ${error.code}.`);
56.     }
57.   }

58.   // 加载本地数据库模式
59.   private loadDatabaseToTrack(): void {
60.     this.pageInfo.pushDestinationByName('ARImageByDatabase', null);
61.   }
62. }

### ARImageByAdd页面

加载本地图片模式。

1. 选择本地图片进行图像识别能力所需要导入的模块如下：
    
    1. // ARImageByAdd.ets
    
    2. import { arEngine, ARView, arViewController } from '@kit.AREngine';
    3. import { Node, Scene } from '@kit.ArkGraphics3D';
    4. import { collections } from '@kit.ArkTS';
    5. import { BusinessError } from '@kit.BasicServicesKit';
    6. import { fileIo } from '@kit.CoreFileKit';
    7. import { image } from '@kit.ImageKit';
    
2. 配置页面路由信息，定义数据库dataBase。
    
    1. // ARImageByAdd.ets
    
    2. // 页面路由
    3. @Builder
    4. export function ARImageByAddBuilder(): void {
    5.   ARImageByAdd();
    6. }
    
    7. let dataBase: arEngine.ARAugmentedImageDatabase;
    
3. 在设备界面上显示图片添加情况，无可用图片则弹窗提示，加载AR场景。
    
    1. // ARImageByAdd.ets
    
    2. @Component
    3. struct ARImageByAdd {
    4.   pageInfo: NavPathStack = new NavPathStack();
    5.   private imagePathArray: string[] = [];
    6.   private isProgramExits: boolean = false;
    7.   private isSaveDatabase: boolean = false;
    8.   @State arContext?: arViewController.ARViewContext = undefined;
    9.   @State context: Context = this.getUIContext().getHostContext() as Context;
    10.   @State totalImageCounts: number = this.imagePathArray.length;
    11.   @State addFailedImageCounts: number = 0;
    12.   @State succeedImageCounts: number = 0;
    13.   @State addFailedMessage: string[] = [];
    
    14.   build(): void {
    15.     NavDestination() {
    16.       RelativeContainer() {
    17.         Column() {
    18.           Text(`添加图片进度: ${this.succeedImageCounts + this.addFailedImageCounts} / ${this.totalImageCounts}`)
    19.           Text(`添加成功数量：${this.succeedImageCounts}`)
    20.           Text(`添加失败数量：${this.addFailedImageCounts}`)
    
    21.           if (this.addFailedMessage) {
    22.             ForEach(this.addFailedMessage, (item: string) => {
    23.               Text(`${item}`)
    24.                 .fontColor(Color.Red)
    25.             })
    26.           }
    27.         }
    28.         .visibility(this.addFailedImageCounts + this.succeedImageCounts < this.totalImageCounts ? Visibility.Visible :
    29.         Visibility.None)
    30.         .foregroundColor(Color.Red)
    31.         .zIndex(1)
    32.         .alignRules({
    33.           center: { anchor: '__container__', align: VerticalAlign.Center },
    34.           middle: { anchor: '__container__', align: HorizontalAlign.Center }
    35.         })
    
    36.         if (this.arContext) {
    37.           ARView({ context: this.arContext })
    38.             .height('100%')
    39.             .width('100%')
    40.             .alignRules({
    41.               center: { anchor: '__container__', align: VerticalAlign.Center },
    42.               middle: { anchor: '__container__', align: HorizontalAlign.Center }
    43.             })
    44.         }
    45.       }
    46.     }
    47.     // 创建数据库，加载本地缓存，初始化AR场景，创建AR会话
    48.     .onAppear(() => {
    49.       arEngine.createARAugmentedImageDatabase()
    50.         .then((arDataBase) => {
    51.           dataBase = arDataBase;
    
    52.           this.addImage(dataBase).then(() => {
    53.             if (this.addFailedImageCounts === this.totalImageCounts) {
    54.               this.ShowDialog('请添加有效图片。');
    55.             }
    56.             this.initARView();
    57.           })
    58.         })
    59.     })
    60.     .onWillDisappear(async () => {
    61.       this.stopARView();
    62.     })
    63.     .onShown(() => {
    64.       this.resumeARView();
    65.     })
    66.     .onHidden(() => {
    67.       this.pauseARView();
    68.     })
    69.     .onReady((context: NavDestinationContext) => {
    70.       this.pageInfo = context.pathStack;
    71.       this.imagePathArray = context.pathInfo.param as string[];
    72.       this.totalImageCounts = this.imagePathArray.length;
    73.     })
    74.     .hideTitleBar(true)
    75.     .hideBackButton(true)
    76.     .hideToolBar(true)
    77.   }
    
    78.   // 初始化AR场景，创建AR会话
    79.   private initARView(): void {
    80.     Scene.load().then(async (scene: Scene) => {
    81.       let viewContext: arViewController.ARViewContext = new arViewController.ARViewContext();
    82.       viewContext.scene = scene;
    83.       viewContext.callback = new ARViewCallbackImpl();
    84.       viewContext.config = {
    85.         type: arEngine.ARType.IMAGE,  // 使用图像跟踪模式
    86.         planeFindingMode: arEngine.ARPlaneFindingMode.HORIZONTAL_AND_VERTICAL,
    87.         powerMode: arEngine.ARPowerMode.NORMAL,
    88.         semanticMode: arEngine.ARSemanticMode.NONE,
    89.         poseMode: arEngine.ARPoseMode.GRAVITY,
    90.         depthMode: arEngine.ARDepthMode.AUTOMATIC,
    91.         meshMode: arEngine.ARMeshMode.DISABLED,
    92.         focusMode: arEngine.ARFocusMode.AUTO
    93.       }
    94.       viewContext.init().then(() => {
    95.         this.arContext = viewContext;
    96.         console.info('Succeeded in initializing ARView.');
    97.       }).catch((err: BusinessError) => {
    98.         console.error(`Failed to init ARView. Code is ${err.code}, message is ${err.message}.`);
    99.       })
    100.     })
    101.   }
    
    102.   private async stopARView(): Promise<void> {
    103.     if (!this.arContext) {
    104.       return;
    105.     }
    106.     try {
    107.       this.isProgramExits = true;
    108.       if (this.isSaveDatabase) {
    109.         SaveBufferToLocal(dataBase, this.context);
    110.       }
    
    111.       await dataBase.release();
    112.       await this.arContext?.destroy();
    113.     } catch (error) {
    114.       const err: BusinessError = error as BusinessError;
    115.       console.error(`Failed to stop context. Code is ${err.code}, message is ${err.message}`);
    116.     }
    117.   }
    
    118.   private resumeARView(): void {
    119.     // ...
    120.   }
    121.   private pauseARView(): void {
    122.     // ...
    123.   }
    
    124.   // 异步执行添加图片的任务
    125.   async addImage(dataBase: arEngine.ARAugmentedImageDatabase): Promise<void> {
    126.     for (let index = 0; index < this.totalImageCounts; index++) {
    127.       const imagePath: string = this.imagePathArray[index];
    128.       let file: fileIo.File = fileIo.openSync(imagePath, fileIo.OpenMode.READ_ONLY);
    129.       let imageName: string = file.name;
    130.       const imageSourceApi: image.ImageSource = image.createImageSource(file.fd);
    131.       try {
    132.         fileIo.closeSync(file);
    133.       } catch (error) {
    134.         const err: BusinessError = error as BusinessError;
    135.         console.error(`Failed to closeSync. Code: ${err.code}.`);
    136.         this.addFailedImageCounts += 1;
    137.         continue;
    138.       }
    139.       const imageInfo: image.ImageInfo = imageSourceApi.getImageInfoSync(0);
    140.       if (!imageInfo) {
    141.         console.error('Failed to obtain the image pixel map information.');
    142.         this.addFailedImageCounts += 1;
    143.         continue;
    144.       }
    145.       const opts: image.DecodingOptions = {
    146.         editable: true,
    147.         desiredPixelFormat: image.PixelMapFormat.RGBA_8888,
    148.         desiredSize: { width: imageInfo.size.width, height: imageInfo.size.height }
    149.       }
    150.       let pixelMap: image.PixelMap = imageSourceApi.createPixelMapSync(opts);
    151.       const info: image.ImageInfo = pixelMap.getImageInfoSync();
    152.       let size: number = pixelMap.getPixelBytesNumber();
    153.       console.info(`The ets create pixelMap width: ${info.size.width}, height: ${info.size.height}, size: ${size}.`);
    
    154.       if (this.isProgramExits) {
    155.         break;
    156.       }
    
    157.       await dataBase.addImage(imageName, pixelMap, 10).then((result: arEngine.ARAddAugmentedImageResult) => {
    158.         console.info(`The imageResult: ${result.index} ${result.stateReason}.`);
    159.         if (result.stateReason !== arEngine.ARAddAugmentedImageReason.NONE) {
    160.           this.addFailedImageCounts += 1;
    161.           this.addFailedMessage.push('失败图片名:' + imageName + '失败原因:' + errcode.get(result.stateReason) + ' ');
    162.         } else {
    163.           this.succeedImageCounts += 1;
    164.         }
    165.       }).catch(() => {
    166.         this.addFailedImageCounts += 1;
    167.       })
    
    168.       imageSourceApi.release();
    169.       pixelMap.release();
    170.     }
    171.   }
    
    172.   // 自定义的弹窗提示
    173.   ShowDialog(msg: string): void {
    174.     this.getUIContext().showAlertDialog(
    175.       {
    176.         title: '警告',
    177.         message: msg,
    178.         autoCancel: true,
    179.         alignment: DialogAlignment.Center,
    180.         offset: { dx: 0, dy: -20 },
    181.         gridCount: 3,
    182.         transition: TransitionEffect
    183.           .asymmetric(TransitionEffect.OPACITY
    184.             .animation({ duration: 1000, curve: Curve.Sharp })
    185.             .combine(TransitionEffect
    186.               .scale({ x: 1.5, y: 1.5 })
    187.               .animation({ duration: 1000, curve: Curve.Sharp })
    188.             ),
    189.           TransitionEffect.OPACITY
    190.             .animation({ duration: 100, curve: Curve.Smooth })
    191.             .combine(TransitionEffect.scale({ x: 0.5, y: 0.5 })
    192.               .animation({ duration: 100, curve: Curve.Smooth })
    193.             )
    194.           ),
    195.         buttons: [{
    196.           enabled: true,
    197.           defaultFocus: true,
    198.           style: DialogButtonStyle.HIGHLIGHT,
    199.           value: '退出',
    200.           action: () => {
    201.             console.info('Callback when the second button is clicked.');
    202.             this.pageInfo.pop();
    203.             return;
    204.           }
    205.         }]
    206.       })
    207.     }
    208.   }
    
4. 退出应用时，缓存图片特征到本地。
    
    1. // ARImageByAdd.ets
    
    2. async function SaveBufferToLocal(dataBase: arEngine.ARAugmentedImageDatabase, context: Context): Promise<void> {
    3.   let filesDir: string = context.filesDir;
    4.   let file: fileIo.File =
    5.     fileIo.openSync(filesDir + '/test.bin',
    6.       fileIo.OpenMode.READ_WRITE | fileIo.OpenMode.CREATE | fileIo.OpenMode.TRUNC);
    7.   let buf: ArrayBuffer = await dataBase.serialize();
    8.   let writeLen: number = fileIo.writeSync(file.fd, buf);
    9.   console.info(`The length of buffer is: ${writeLen}`);
    10.   fileIo.closeSync(file);
    11. }
    
5. 调用[ARViewCallback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9396615174614)，使用其中的[onFrameUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section52341758194715)方法进行帧数据更新，识别到目标图像则打印日志。
    
    1. // ARImageByAdd.ets
    
    2. class ARViewCallbackImpl extends arViewController.ARViewCallback {
    3.   onAnchorAdd(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
    4.   }
    
    5.   onAnchorUpdate(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
    6.   }
    
    7.   async onFrameUpdate(ctx: arViewController.ARViewContext, sysBootTs: number): Promise<void> {
    8.     if (!ctx.session || !dataBase) {
    9.       return;
    10.     }
    
    11.     let session: arEngine.ARSession = ctx.session; // 获取AR会话
    
    12.     try {
    13.       let imageNumber: number = dataBase.getImageCount();
    14.       console.info(`The number of images in the database is ${imageNumber}.`);
    
    15.       let imageCapacity: number = dataBase.getCapacity();
    16.       console.info(`The dataBase image capacity is: ${imageCapacity}.`);
    
    17.       let trackable: arEngine.ARTrackable[] = session.getAllTrackables(arEngine.ARTrackableType.AUGMENTED_IMAGE);
    
    18.       console.info(`The image trackable size: ${trackable.length}.`);
    19.       for (let i = 0; i < trackable.length; ++i) {
    20.         if (trackable[i].type === arEngine.ARTrackableType.AUGMENTED_IMAGE) {
    21.           let arimage: arEngine.ARAugmentedImage = trackable[i] as arEngine.ARAugmentedImage;
    22.           if (arEngine.ARTrackingState.TRACKING !== arimage.state) {
    23.             continue;
    24.           }
    25.           let centerPose: arEngine.ARPose = arimage.getPose();
    26.           console.info(`The image width: ${arimage.extendX}, height: ${arimage.extendZ}, pose: ${centerPose.getMatrix()}.`);  // 打印目标图像的信息
    27.         }
    28.       }
    
    29.     } catch (error) {
    30.       const err: BusinessError = error as BusinessError;
    31.       console.error(`Failed to got image count. Code is ${err.code}, message is ${err.message}`);
    32.     }
    33.   }
    34. }
    
    35. // 图像添加失败原因
    36. const errcode: collections.Map<number, string> = new collections.Map<number, string>([
    37.   [0, 'success'],
    38.   [1, 'size not match'],
    39.   [2, 'too bright or too dark'],
    40.   [3, 'image color is relatively single'],
    41.   [4, 'other error']
    42. ])
    

### ARImageByDatabase页面

加载本地数据库模式。

1. 选择本地数据库进行图像识别能力所需要导入的模块如下：
    
    1. // ARImageByDatabase.ets
    
    2. import { arEngine, ARView, arViewController } from '@kit.AREngine';
    3. import { Node, Scene } from '@kit.ArkGraphics3D';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    5. import { fileIo, ReadOptions } from '@kit.CoreFileKit';
    
2. 配置页面路由信息，定义数据库dataBase。
    
    1. // ARImageByDatabase.ets
    
    2. // 页面路由
    3. @Builder
    4. export function ARImageByDatabaseBuilder(): void {
    5.   ARImageByDatabase();
    6. }
    
    7. let dataBase: arEngine.ARAugmentedImageDatabase;
    
3. 加载AR场景，加载图像数据库，无可用数据库则弹窗提示。
    
    1. // ARImageByDatabase.ets
    
    2. @Component
    3. struct ARImageByDatabase {
    4.   pageInfo: NavPathStack = new NavPathStack();
    5.   @State arContext?: arViewController.ARViewContext = undefined;
    6.   @State context: Context = this.getUIContext().getHostContext() as Context;
    
    7.   build() {
    8.     NavDestination() {
    9.       RelativeContainer() {
    10.         if (this.arContext) {
    11.           ARView({ context: this.arContext })
    12.             .height('100%')
    13.             .width('100%')
    14.             .alignRules({
    15.               center: { anchor: '__container__', align: VerticalAlign.Center },
    16.               middle: { anchor: '__container__', align: HorizontalAlign.Center }
    17.             })
    18.         }
    19.       }
    20.     }
    21.     // 创建数据库，加载本地缓存，初始化AR场景，创建AR会话
    22.     .onAppear(() => {
    23.       arEngine.createARAugmentedImageDatabase()
    24.         .then((arDataBase) => {
    25.           dataBase = arDataBase;
    
    26.           try {
    27.             let databaseBuffer: ArrayBuffer = ReadBuffer(this.context);
    28.             dataBase.deserialize(databaseBuffer).then(() => {
    29.               this.initARView();
    30.             })
    31.           } catch (error) {
    32.             const err: BusinessError = error as BusinessError;
    33.             console.error(`Failed to init context. Code is ${err.code}, message is ${err.message}.`);
    34.             this.ShowDialog('请添加有效图片。');
    35.           }
    36.         })
    37.     })
    38.     .onWillDisappear(async () => {
    39.       this.stopARView();
    40.     })
    41.     .onShown(() => {
    42.       this.resumeARView();
    43.     })
    44.     .onHidden(() => {
    45.       this.pauseARView();
    46.     })
    47.     .onReady((context: NavDestinationContext) => {
    48.       this.pageInfo = context.pathStack;
    49.     })
    50.     .hideTitleBar(true)
    51.     .hideBackButton(true)
    52.     .hideToolBar(true)
    53.   }
    
    54.   // 初始化AR场景，创建AR会话
    55.   private initARView(): void {
    56.     Scene.load().then(async (scene: Scene) => {
    57.       let context: arViewController.ARViewContext = new arViewController.ARViewContext();
    58.       context.scene = scene;
    59.       context.callback = new ARViewCallbackImpl();
    60.       context.config = {
    61.         type: arEngine.ARType.IMAGE,  // 使用图像跟踪模式
    62.         planeFindingMode: arEngine.ARPlaneFindingMode.HORIZONTAL_AND_VERTICAL,
    63.         powerMode: arEngine.ARPowerMode.NORMAL,
    64.         semanticMode: arEngine.ARSemanticMode.NONE,
    65.         poseMode: arEngine.ARPoseMode.GRAVITY,
    66.         depthMode: arEngine.ARDepthMode.AUTOMATIC,
    67.         meshMode: arEngine.ARMeshMode.ENABLE
    68.       }
    69.       context.init().then(() => {
    70.         this.arContext = context;
    71.         console.info('Succeeded in initializing ARView.');
    72.       }).catch((err: BusinessError) => {
    73.         console.error(`Failed to init context. Code is ${err.code}, message is ${err.message}.`);
    74.       })
    75.     })
    76.   }
    
    77.   private async stopARView(): Promise<void> {
    78.     if (!this.arContext) {
    79.       return;
    80.     }
    81.     try {
    82.       await dataBase.release();
    83.       await this.arContext?.destroy();
    84.     } catch (error) {
    85.       const err: BusinessError = error as BusinessError;
    86.       console.error(`Failed to stop context. Code is ${err.code}, message is ${err.message}`);
    87.     }
    88.   }
    
    89.   private resumeARView(): void {
    90.     // ...
    91.   }
    92.   private pauseARView(): void {
    93.     // ...
    94.   }
    
    95.   // 自定义的弹窗提示
    96.   ShowDialog(msg: string): void {
    97.     this.getUIContext().showAlertDialog(
    98.       {
    99.         title: '警告',
    100.         message: msg,
    101.         autoCancel: true,
    102.         alignment: DialogAlignment.Center,
    103.         offset: { dx: 0, dy: -20 },
    104.         gridCount: 3,
    105.         transition: TransitionEffect
    106.           .asymmetric(TransitionEffect.OPACITY
    107.             .animation({ duration: 1000, curve: Curve.Sharp })
    108.             .combine(TransitionEffect
    109.               .scale({ x: 1.5, y: 1.5 })
    110.               .animation({ duration: 1000, curve: Curve.Sharp })
    111.             ),
    112.           TransitionEffect.OPACITY
    113.             .animation({ duration: 100, curve: Curve.Smooth })
    114.             .combine(TransitionEffect.scale({ x: 0.5, y: 0.5 })
    115.               .animation({ duration: 100, curve: Curve.Smooth })
    116.             )
    117.           ),
    118.         buttons: [{
    119.           enabled: true,
    120.           defaultFocus: true,
    121.           style: DialogButtonStyle.HIGHLIGHT,
    122.           value: '退出',
    123.           action: () => {
    124.             console.info('Callback when the second button is clicked.');
    125.             this.pageInfo.pop();
    126.             return;
    127.           }
    128.         }]
    129.       })
    130.     }
    131.   }
    
4. 读取本地数据库缓存文件的方法。
    
    1. // ARImageByDatabase.ets
    
    2. function ReadBuffer(context: Context): ArrayBuffer {
    3.   let filesDir: string = context.filesDir;
    4.   let srcFile: fileIo.File =
    5.     fileIo.openSync(filesDir + '/test.bin', fileIo.OpenMode.READ_WRITE | fileIo.OpenMode.CREATE);
    6.   const fileStat: fileIo.Stat = fileIo.statSync(srcFile.fd);
    7.   // 读取源文件的内容并写入目标文件
    8.   let readSize: number = 0;
    9.   let buf: ArrayBuffer = new ArrayBuffer(fileStat.size);
    10.   let readOptions: ReadOptions = {
    11.     offset: readSize,
    12.     length: fileStat.size
    13.   }
    14.   let readLen: number = fileIo.readSync(srcFile.fd, buf, readOptions);
    15.   console.info(`The length of buffer is: ${readLen}.`);
    16.   fileIo.closeSync(srcFile);
    17.   return buf;
    18. }
    
5. 调用[ARViewCallback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9396615174614)，使用其中的[onFrameUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section52341758194715)方法进行帧数据更新，识别到目标图像则打印日志。
    
    1. // ARImageByDatabase.ets
    
    2. class ARViewCallbackImpl extends arViewController.ARViewCallback {
    3.   onAnchorAdd(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
    4.   }
    
    5.   onAnchorUpdate(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
    6.   }
    
    7.   async onFrameUpdate(ctx: arViewController.ARViewContext, sysBootTs: number): Promise<void> {
    8.     if (!ctx.session || !dataBase) {
    9.       return;
    10.     }
    
    11.     let session: arEngine.ARSession = ctx.session;
    
    12.     try {
    13.       let imageNumber: number = dataBase.getImageCount();
    14.       console.info(`The number of images in the database is ${imageNumber}.`);
    
    15.       let imageCapacity: number = dataBase.getCapacity();
    16.       console.info(`The dataBase image capacity = ${imageCapacity}.`);
    
    17.       let trackable: arEngine.ARTrackable[] = session.getAllTrackables(arEngine.ARTrackableType.AUGMENTED_IMAGE);
    
    18.       console.info(`The image trackable size: ${trackable.length}.`);
    19.       for (let i = 0; i < trackable.length; ++i) {
    20.         if (trackable[i].type === arEngine.ARTrackableType.AUGMENTED_IMAGE) {
    21.           let arimage: arEngine.ARAugmentedImage = trackable[i] as arEngine.ARAugmentedImage;
    22.           if (arEngine.ARTrackingState.TRACKING !== arimage.state) {
    23.             continue;
    24.           }
    25.           let centerPose: arEngine.ARPose = arimage.getPose();
    26.           console.info(`The image width: ${arimage.extendX}, height: ${arimage.extendZ}, pose: ${centerPose.getMatrix()}.`);  // 打印目标图像的信息
    27.         }
    28.       }
    
    29.     } catch (error) {
    30.       const err: BusinessError = error as BusinessError;
    31.       console.error(`Failed to got image count. Code is ${err.code}, message is ${err.message}.`);
    32.     }
    33.   }
    34. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-get-mesh "获取网格扫描信息")
# AR物体摆放

更新时间: 2025-12-16 16:34

## 概要

从5.1.0(18)开始，AR Engine支持物体摆放能力。

本章节通过AR Engine识别设备周围的平面，并允许用户在平面上放置虚拟物体，实现虚拟和现实的融合。AR物体摆放可用于虚拟家具、数字展厅等应用，给用户提供虚实结合的新体验。

**图1** AR物体摆放示意图  
![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163453.83456101093754706678152385613260:50001231000000:2800:B5B6E49F288B70C08DFDACA388FF9FD57006104AE10D6A02F7F89C4F6703E216.jpg "点击放大")

本章节涉及的AR Engine能力如下：

- 运动跟踪能力
- 环境跟踪能力（平面检测）
- 命中检测能力

## 接口说明

AR物体摆放主要依赖[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，以下接口为AR物体摆放相关接口。详细接口和说明，请参考[AR Engine API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-arkts-api)。

|接口名|描述|
|:--|:--|
|[ARViewContext.init](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section07524457283)|初始化[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，初始化AR会话和设置AR渲染场景等。|
|[ARViewContext.pause](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9795165613212)|暂停相机跟踪与AR场景渲染。|
|[ARViewContext.destroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section169251835133414)|销毁[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，释放ARView使用资源，包括AR会话与呈现场景销毁，在退出ARView场景时使用。|
|[ARViewContext.resume](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section639015333356)|用于恢复暂停的相机跟踪与AR场景渲染。|
|[ARViewContext.scene](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section885612613616)|设置ARView的AR场景。|
|[ARViewContext.scene](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section1371542426)|获得的AR呈现场景，用于管理空间节点。|
|[ARViewContext.session](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section18461161774312)|获取AR会话，用于获取相关AR环境跟踪、相机跟踪、命中检测等能力，如相机位姿、平面信息、创建锚点等。|
|[ARViewContext.config](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section4323184815436)|设置AR会话的配置文件，如北向坐标、性能模式等。|
|[ARViewContext.callback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section20507194174418)|设置回调函数，以根据回调功能实现对应业务逻辑。|
|[ARFrame.getCamera](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1293654414328)|获取当前帧的摄像机参数对象。|
|[ARFrame.getUpdatedTrackables](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section43145512417)|获取更新后的指定类型的可追踪对象。|
|[ARFrame.hitTest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section20353182861218)|根据相机投射光线，获取预览区域中的像素坐标（pixelX和pixelY）来确定射线方向，然后检测这个射线在平面或点云中是否有交点。|
|[ARAnchor.getPose](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1448415478356)|获取锚点在世界坐标系中的位姿信息。|
|[ARHitResult.getHitPose](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1864219177109)|获取交点位姿。|
|[ARHitResult.getTrackable](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section727122311104)|获取被命中的可追踪对象。|
|[ARPose.getMatrix](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section5278038164917)|将位姿数据转换为一个4x4的矩阵。|

## 开发步骤

AR Engine仅输出识别到的平面数据。为便于用户观察，开发者可使用AGP（Ark Graphics Platform）渲染引擎或者[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent)绘制识别的平面。关于AGP的介绍可以查看[ArkGraphics 3D简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkgraphics3d-overview)和[AGP引擎](https://gitcode.com/openharmony/graphic_graphic_3d)。

对于使用ArkTS的任何AR应用，首先需要创建一个AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)，用于管理AR Engine的系统状态。AR会话[ARViewContext](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section12681656121519)的创建可以参考[管理AR会话](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-arsession)章节。

### 导入模块

AR物体摆放所需要导入的模块如下。

1. import { arEngine, ARView, arViewController } from '@kit.AREngine';
2. import { Node, Scene, Vec3 } from '@kit.ArkGraphics3D';
3. import { window } from '@kit.ArkUI';
4. import { BusinessError } from '@kit.BasicServicesKit';

### 定义变量

定义变量hitAnchorList存储放置物体处的锚点信息、hitPoseList存储放置物体处的位姿信息和statusBarHeight设备状态栏高度。

用户点击设备的坐标和显示预览流的坐标不一致，预览流的窗口略小于设备屏幕，因此需要减去设备状态栏高度以获取准确的点击坐标。

1. let frame: arEngine.ARFrame;
2. let hitAnchorList: arEngine.ARAnchor[] = [];
3. let hitPoseList: Vec3[] = [];
4. let statusBarHeight: number = 0;

### 显示预览流

在ARView中加入点击事件，进行碰撞检测，获取锚点位姿数据加入列表。

1. @Builder
2. export function ARWorldBuilder(): void {
3.   ARWorld();
4. }

5. @Component
6. struct ARWorld {
7.   @State arContext?: arViewController.ARViewContext = undefined;
8.   @State context: Context = this.getUIContext().getHostContext() as Context;

9.   build(): void {
10.     NavDestination() {
11.       RelativeContainer() {
12.         if (this.arContext) {
13.           ARView({ context: this.arContext })
14.             .height('100%')
15.             .width('100%')
16.             .alignRules({
17.               center: { anchor: '__container__', align: VerticalAlign.Center },
18.               middle: { anchor: '__container__', align: HorizontalAlign.Center }
19.             })
20.             .onClick((event: ClickEvent) => {
21.               this.objectCollisionDetection(event);
22.             })
23.         }
24.       }
25.     }
26.     .onAppear(() => {
27.       this.initARView();
28.       this.getAvoidArea();
29.     })
30.     .onWillDisappear(() => {
31.       this.stopARView();
32.     })
33.     .onShown(() => {
34.       this.resumeARView();
35.     })
36.     .onHidden(() => {
37.       this.pauseARView();
38.     })
39.     .hideTitleBar(true)
40.     .hideBackButton(true)
41.     .hideToolBar(true)
42.   }

43.   // 获取用户点击坐标，获取碰撞检测结果
44.   private objectCollisionDetection(event: ClickEvent): void {
45.     let x: number = this.getUIContext().vp2px(event.windowX);
46.     let y: number = this.getUIContext().vp2px(event.windowY) - statusBarHeight;
47.     console.info(`Get onclick position, x: ${x} y: ${y}.`);

48.     try {
49.       let result: arEngine.ARHitResult[] = frame.hitTest(x, y);
50.       console.info(`The hitResult size is: ${result.length}.`);
51.       if (!result) {
52.         return;
53.       }

54.       for (let i = 0; i < result.length; i++) {
55.         let hitResult: arEngine.ARHitResult = result[i];
56.         let trackable: arEngine.ARTrackable = hitResult.getTrackable();

57.         if (trackable.type !== arEngine.ARTrackableType.PLANE) {
58.           continue;
59.         }

60.         let hitPlane: arEngine.ARPlane = trackable as arEngine.ARPlane;
61.         let hitPose: arEngine.ARPose = hitResult.getHitPose();
62.         let inPolygon: boolean = hitPlane.isPoseInPolygon(hitPose);
63.         let distance: number = hitResult.distance;
64.         console.info(`The hitResult inPolygon is: ${inPolygon}, distance is: ${distance}.`);

65.         if (!inPolygon || distance <= 0) {
66.           continue;
67.         }

68.         let hitAnchor: arEngine.ARAnchor = hitResult.createAnchor();
69.         let pos: Vec3 = hitAnchor.getPose().translation;

70.         hitPoseList.push(pos);
71.         hitAnchorList.push(hitAnchor);

72.       }
73.       console.info('Succeeded in getting hit result.');
74.     } catch (error) {
75.       const err: BusinessError = error as BusinessError;
76.       console.error(`Failed to get hitResults. Code is ${err.code}, message is ${err.message}.`);
77.     }
78.   }

79.   private initARView(): void {
80.     Scene.load().then(async (scene: Scene) => {
81.       let viewContext: arViewController.ARViewContext = new arViewController.ARViewContext();
82.       viewContext.scene = scene;
83.       viewContext.callback = new ARViewCallbackImpl();
84.       viewContext.config = {
85.         type: arEngine.ARType.WORLD,
86.         planeFindingMode: arEngine.ARPlaneFindingMode.HORIZONTAL_AND_VERTICAL,
87.         powerMode: arEngine.ARPowerMode.NORMAL,
88.         semanticMode: arEngine.ARSemanticMode.NONE,
89.         poseMode: arEngine.ARPoseMode.GRAVITY,
90.         depthMode: arEngine.ARDepthMode.AUTOMATIC,
91.         meshMode: arEngine.ARMeshMode.DISABLED,
92.         focusMode: arEngine.ARFocusMode.AUTO
93.       }
94.       viewContext.init().then(() => {
95.         this.arContext = viewContext;
96.         console.info('Succeeded in initializing ARView.');
97.       }).catch((err: BusinessError) => {
98.         console.error(`Failed to init ARView. Code is ${err.code}, message is ${err.message}.`);
99.       })
100.     })
101.   }

102.  // 获取屏幕上减去状态栏的真实高度（预览流高度）
103.   private getAvoidArea(): void {
104.     let avoidAreaType: window.AvoidAreaType = window.AvoidAreaType.TYPE_SYSTEM;
105.     window.getLastWindow(this.context).then((data) => {
106.       // 获取顶部状态栏高度
107.       let avoidArea: window.AvoidArea = data.getWindowAvoidArea(avoidAreaType);
108.       statusBarHeight = avoidArea.topRect.height;
109.       console.info(`The statusBarHeight is ${statusBarHeight}.`);
110.     }).catch((err: BusinessError) => {
111.       console.error(`Failed to obtain the window. Code is ${err.code}, message is ${err.message}.`);
112.     })
113.   }

114.   private stopARView(): void {
115.     // ...
116.   }
117.   private resumeARView(): void {
118.     // ...
119.   }
120.   private pauseARView(): void {
121.     // ...
122.   }
123. }

### 渲染识别的平面和放置的物体

调用[ARViewCallback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section9396615174614)，使用其中的[onFrameUpdate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arviewcontroller#section52341758194715)方法进行帧数据更新，获取平面信息。

1. class ARViewCallbackImpl extends arViewController.ARViewCallback {
2.   onAnchorAdd(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
3.   }

4.   onAnchorUpdate(ctx: arViewController.ARViewContext, node: Node, anchor: arEngine.ARAnchor): void {
5.   }

6.   async onFrameUpdate(ctx: arViewController.ARViewContext, sysBootTs: number): Promise<void> {
7.     if (!ctx.session) {
8.       return;
9.     }

10.     let arSession: arEngine.ARSession = ctx.session;

11.     try {
12.       frame = arSession.getFrame();
13.       let camera: arEngine.ARCamera = frame.getCamera();
14.       let trackable: arEngine.ARTrackable[] = [];

15.       if (camera.state === arEngine.ARTrackingState.TRACKING) {
16.         trackable = arSession.getAllTrackables(arEngine.ARTrackableType.PLANE);
17.         console.info(`Succeeded in getting tracking plane，length is: ${trackable.length}.`);  // 输出识别到的平面数量
18.       }

19.     } catch (error) {
20.       const err: BusinessError = error as BusinessError;
21.       console.error(`Failed to update data. Code is ${err.code}, message is ${err.message}.`);
22.     }
23.   }
24. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-image-track "图像跟踪")
# 数据类型转换说明

更新时间: 2025-12-16 16:34

在开发AR应用时，部分数据类型需要转换才能使用，以下进行汇总及示例。

## ArrayBuffer

在一些不支持接收ArrayBuffer数据类型的方法中，需要将其反序列化为int32或者float32类型，涉及转换的接口列表如下：

|接口名|描述|
|:--|:--|
|[ImageComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section175993235012)|参数buffer为ArrayBuffer类型，可转换为int32。|
|[ARPlane.getPolygonXZ](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section12949442354)|返回值为ArrayBuffer类型，可转换为float32。|
|[ARSceneMesh.getVertices](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section15211205153115)|返回值为ArrayBuffer类型，可转换为float32。|
|[ARSceneMesh.getVertexNormals](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section4793111183211)|返回值为ArrayBuffer类型，可转换为float32。|
|[ARSceneMesh.getTriangleIndices](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section19221187183218)|返回值为ArrayBuffer类型，可转换为int32。|
|[ARSemanticDensePointData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1031071863714)|参数id为ArrayBuffer类型，可转换为int32。|
|[ARSemanticDensePointData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1031071863714)|参数position为ArrayBuffer类型，可转换为float32。|
|[ARSemanticDensePointData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1031071863714)|参数color为ArrayBuffer类型，可转换为int32。|

转换的示例如下：

1. // ArrayBuffer转float32
2. function arrayBufferFloat32ToNumber(buffer: ArrayBuffer): number[] {
3.   let view: Float32Array = new Float32Array(buffer);
4.   let numberArray: number[] = Array.from(view);
5.   return numberArray;
6. }

7. // ArrayBuffer转int32
8. function arrayBufferInt32ToNumber(buffer: ArrayBuffer): number[] {
9.   let view: Int32Array = new Int32Array(buffer);
10.   let numberArray: number[] = Array.from(view);
11.   return numberArray;
12. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-volume-measurement "高精几何重建")
# 数据类型转换说明

更新时间: 2025-12-16 16:34

在开发AR应用时，部分数据类型需要转换才能使用，以下进行汇总及示例。

## ArrayBuffer

在一些不支持接收ArrayBuffer数据类型的方法中，需要将其反序列化为int32或者float32类型，涉及转换的接口列表如下：

|接口名|描述|
|:--|:--|
|[ImageComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section175993235012)|参数buffer为ArrayBuffer类型，可转换为int32。|
|[ARPlane.getPolygonXZ](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section12949442354)|返回值为ArrayBuffer类型，可转换为float32。|
|[ARSceneMesh.getVertices](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section15211205153115)|返回值为ArrayBuffer类型，可转换为float32。|
|[ARSceneMesh.getVertexNormals](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section4793111183211)|返回值为ArrayBuffer类型，可转换为float32。|
|[ARSceneMesh.getTriangleIndices](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section19221187183218)|返回值为ArrayBuffer类型，可转换为int32。|
|[ARSemanticDensePointData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1031071863714)|参数id为ArrayBuffer类型，可转换为int32。|
|[ARSemanticDensePointData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1031071863714)|参数position为ArrayBuffer类型，可转换为float32。|
|[ARSemanticDensePointData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine#section1031071863714)|参数color为ArrayBuffer类型，可转换为int32。|

转换的示例如下：

1. // ArrayBuffer转float32
2. function arrayBufferFloat32ToNumber(buffer: ArrayBuffer): number[] {
3.   let view: Float32Array = new Float32Array(buffer);
4.   let numberArray: number[] = Array.from(view);
5.   return numberArray;
6. }

7. // ArrayBuffer转int32
8. function arrayBufferInt32ToNumber(buffer: ArrayBuffer): number[] {
9.   let view: Int32Array = new Int32Array(buffer);
10.   let numberArray: number[] = Array.from(view);
11.   return numberArray;
12. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-volume-measurement "高精几何重建")
# 获取检测平面的二维顶点数组时报错：“plane is nullptr!”，返回错误码：401

更新时间: 2025-12-16 16:34

## 现象描述

调用[HMS_AREngine_ARPlane_GetPolygonSize](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-capi-arengine#ga98760556eee2a4a69c33699b7ce3edc6)获取检测到平面的二维顶点数组大小时报错：“plane is nullptr!”，返回错误码：401。

## 可能原因

初次打开应用还未识别到平面，调用[HMS_AREngine_ARSession_GetAllTrackables](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-capi-arengine#gac5b39338f95317671d8de6d4f409cf9c)获取的可跟踪对象列表为空，导致后续[HMS_AREngine_ARTrackableList_AcquireItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-capi-arengine#gab1782eeeeddc01b77a140af915cb351c)获取对应索引的对象也为空，使用前未做有效性判断，使用时出现无效参数错误。

## 处理步骤

开发者从AR Engine获取平面之后需判断其有效性后使用，例如，进行非空判断。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-faq "AR Engine常见问题")
# 反光、光线暗或者弱纹理场景（输入图像颜色变化小）下无法识别平面

更新时间: 2025-12-16 16:34

## 现象描述

使用环境跟踪能力时，如果输入图像中有反光、光线暗、有弱纹理（输入图像颜色变化小），识别到的点云数量会变少甚至没有，出平面时间也会变长或无法生成平面。

1. 反光：镜面，光滑的大理石地板等
    
    **图1** 镜面  
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163449.93039554891296411889714938644405:50001231000000:2800:F5B58115819C3D0B9F3FBB2BA7B338064C2C1E2128E3BA3F08075FE1C7CA7173.jpg "点击放大")
    
2. 光线暗：夜晚的路面或摄像头遮挡等。
    
    **图2** 夜晚的路面
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163449.28451016626675150974706364344459:50001231000000:2800:D65A4A5493F2ED806AFC5A5501C3142B0130BC26F9FD3BBFAD4385BD9DB817DB.jpg "点击放大")
    
3. 弱纹理：如单色柜子、单色桌面和墙面等。
    
    **图3** 墙面
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163449.91894221396570323151174206029775:50001231000000:2800:961B51F9992E99821FF1E018AB13F2BF4744C1BB02938DB1AB2BEF756C9A8E57.jpg "点击放大")
    
    **图4** 纯色的桌面
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163450.97599737998736748837017869156757:50001231000000:2800:D7398FCB87AFDBB2B48DB06C55E84FF4557D51FAB8F3050FCC0E7833995A0B8B.jpg "点击放大")
    

## 可能原因

AR Engine通过输入的图像数据进行平面上特征点的计算，如果输入图像数据中存在反光、光线暗和弱纹理，AR Engine计算后只能得到很少的点，而平面根据识别到的点云生成，因此会导致平面出现缓慢或无法出现的现象。

## 处理步骤

建议应用在持续无法获取点云或平面数据时，提示用户移动相机，避免画面中持续出现反光、光线暗或弱纹理。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-faq-2 "摄像头被遮挡一段时间后再放开，输出的位姿有跳变")
# 某些特殊场景下（如附近存在磁场干扰、手机发烫或扫描到重复纹理等），出现平面漂移或者位姿数据跳变现象

更新时间: 2025-12-16 16:34

## 现象描述

某些特殊场景下，如使用环境附近存在强磁场，手机处于高负载场景下（后台开启很多应用或长时间使用导致手机发烫），或者扫描到重复纹理（见下图）时，可能出现识别到的平面无法锚定到现实世界中，或者通过[HMS_AREngine_ARCamera_GetPose](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-capi-arengine#ga00df108c4ba187967a10e9c4d2e27d3a)接口获取的位姿信息出现大幅度跳变等现象。

**图1** 重复纹理的地板

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163451.55542792290827054715503255643034:50001231000000:2800:B9D9D2FD478A8EA4E1108E5AB0D92FAD7B5DEF94A86D97E6880D8955D8C6AD98.jpg "点击放大")

## 可能原因

AR Engine通过获取到的加速度计传感器和磁力计传感器的信息进行平面计算和相机位姿计算，上述特殊场景下，系统传感器数据可能会存在异常，从而导致平面漂移或者位姿跳变的现象发生。

## 处理步骤

建议应用对通过[HMS_AREngine_ARCamera_GetPose](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-capi-arengine#ga00df108c4ba187967a10e9c4d2e27d3a)接口获取到的位姿数据，按照实际应用使用场景进行滤波，如步行导航场景，应用可以缓存多帧数据，通过多帧数据可以计算得到运动速度，如果检测到此速度明显高于步行速度，证明此时AR数据已经不可信，可以丢弃此数据或者重启AR算法。

说明

**计算运动速度**：x,y,z为在t时刻的位姿数据的位移量。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163451.68188005743940400298726363638189:50001231000000:2800:28C5DA0F8CE73F736F6479CE150D0FF096C28DA2ECB5CCB5892972EDD87D8AB4.png "点击放大")

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-faq-3 "反光、光线暗或者弱纹理场景（输入图像颜色变化小）下无法识别平面")
# 个人数据处理说明

更新时间: 2025-12-16 16:34

此文档针对华为作为最终用户数据处理者，开发者作为最终用户数据控制者的数据处理进行说明，包括：

- 华为处理的个人数据清单
- 指导开发者如何帮助最终用户实现对数据的控制

## 华为处理的个人数据清单

最后修改时间：2025/8/28

|个人数据清单|使用目的|存留期|
|:--|:--|:--|
|传感器信息(包含加速度传感器、陀螺仪传感器、磁场传感器、重力传感器)|该信息用于计算设备运动变化时位姿的状态|传感器捕获到的信息只在端侧处理，处理完成后即丢弃，不会留存|
|相机捕获的图像|AR Engine通过分析相机捕获到的图像信息来实现运动跟踪、环境跟踪和命中检测等AR能力|相机捕获到的图像只在端侧处理，处理完成后即丢弃，不会留存|

## 指导开发者如何帮助最终用户实现对数据的控制

AR Engine不存储用户数据，由数据控制者面向最终用户提供相应的数据主体权利及其相关解释。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-faq-4 "某些特殊场景下（如附近存在磁场干扰、手机发烫或扫描到重复纹理等），出现平面漂移或者位姿数据跳变现象")
# 个人数据处理说明

更新时间: 2025-12-16 16:34

此文档针对华为作为最终用户数据处理者，开发者作为最终用户数据控制者的数据处理进行说明，包括：

- 华为处理的个人数据清单
- 指导开发者如何帮助最终用户实现对数据的控制

## 华为处理的个人数据清单

最后修改时间：2025/8/28

|个人数据清单|使用目的|存留期|
|:--|:--|:--|
|传感器信息(包含加速度传感器、陀螺仪传感器、磁场传感器、重力传感器)|该信息用于计算设备运动变化时位姿的状态|传感器捕获到的信息只在端侧处理，处理完成后即丢弃，不会留存|
|相机捕获的图像|AR Engine通过分析相机捕获到的图像信息来实现运动跟踪、环境跟踪和命中检测等AR能力|相机捕获到的图像只在端侧处理，处理完成后即丢弃，不会留存|

## 指导开发者如何帮助最终用户实现对数据的控制

AR Engine不存储用户数据，由数据控制者面向最终用户提供相应的数据主体权利及其相关解释。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-faq-4 "某些特殊场景下（如附近存在磁场干扰、手机发烫或扫描到重复纹理等），出现平面漂移或者位姿数据跳变现象")