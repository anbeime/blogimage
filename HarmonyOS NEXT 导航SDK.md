# 基础功能最后更新时间: 2025年12月10日

使用导航SDK之前，需要在 config.json 文件中进行相关权限设置，确保导航功能可以正常使用。

## 预置条件

#### 第一步，配置module.json5

首先，声明权限

```
...
"requestPermissions": [
      {
        "name": "ohos.permission.APPROXIMATELY_LOCATION",
        "reason": "$string:Harmony_navi_permission_reason",
        "usedScene": {
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.LOCATION",
        "reason": "$string:Harmony_navi_permission_reason",
        "usedScene": {
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.LOCATION_IN_BACKGROUND",
        "reason": "$string:Harmony_navi_permission_reason",
        "usedScene": {
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.INTERNET",
        "reason": "$string:Harmony_navi_permission_reason",
        "usedScene": {
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.KEEP_BACKGROUND_RUNNING",
        "reason": "$string:Harmony_navi_permission_reason",
        "usedScene": {
          "when": "always"
        }
      }
    ]
...
```

Json

#### 第二步，向工程中添加导航开发包

从ohpm仓库获取导航包，依次添加依赖。

```
"dependencies": {
    "@amap/amap_lbs_common": ">=1.2.3",
    "@amap/amap_lbs_location": ">=1.2.3",
    "@amap/amap_lbs_navi": ">=2.2.6"
}
```

Json

#### 第三步，使用示例

1

首先，创建导航单例，并设置Key

[获取Key](https://lbs.amap.com/api/harmonyosnext-navi-sdk/guide/get-key)

```
AMapNaviFactory.getAMapNaviInstance(getContext().getApplicationContext(), appkey)
```

2

然后，添加导航组件

```
build() {
    NavDestination() {
      AMapNaviComponent({
        appCustomerConfig: {
          mType: AmapNaviType.Driver, //引擎类型（驾车、骑行、步行）。当前支持驾车、货车、摩托车
          //默认模拟导航
          // mNaviType: NaviType.EMULATOR,
          //实时导航
          mNaviType: NaviType.GPS,
          start: {
            coordinate: this.startLatLng
          }, //起点
          end: {
            coordinate: this.endLatLng
          }, //终点
          // wayPoints: this.wayPoints, //途经点
          mRouteStrategy: 10, //设置默认规划路线策略
          serviceAreaDetailsEnable: true, //服务区信息
          goBack: () => {
            this.goback()
          },
        }
      })
    }.title('导航组件')
    .hideTitleBar(true)
    .onBackPressed(() => {
      this.goback()
      return true
    })
  }
```

3

最后，添加导航监听，监听回调中开始算路、导航

```
let listener: IAMapNaviListener = {
      onInitNaviFailure: this.onInitNaviFailure,
      onInitNaviSuccess: this.onInitNaviSuccess,
      onStartNavi: this.onStartNavi,
      onTrafficStatusUpdate: this.onTrafficStatusUpdate,
      onLocationChange: this.onLocationChange,
      onGetNavigationTextAndType: this.onGetNavigationTextAndType,
      onEndEmulatorNavi: this.onEndEmulatorNavi,
      onArriveDestination: this.onArriveDestination,
      onReCalculateRouteForYaw: this.onReCalculateRouteForYaw,
      onReCalculateRouteForTrafficJam: this.onReCalculateRouteForTrafficJam,
      onArrivedWayPoint: this.onArrivedWayPoint,
      onGpsOpenStatus: this.onGpsOpenStatus,
      onNaviInfoUpdate: this.onNaviInfoUpdate,
      updateCameraInfo: this.updateCameraInfo,
      updateIntervalCameraInfo: this.updateIntervalCameraInfo,
      onServiceAreaUpdate: this.onServiceAreaUpdate,
      showCross: this.showCross,
      hideCross: this.hideCross,
      showModeCross: this.showModeCross,
      hideModeCross: this.hideModeCross,
      showLaneInfo: this.showLaneInfo,
      hideLaneInfo: this.hideLaneInfo,
      notifyParallelRoad: this.notifyParallelRoad,
      // OnUpdateTrafficFacility: this.OnUpdateTrafficFacility,
      onPlayRing: this.onPlayRing,
      onTTSIsPlaying: this.onTTSIsPlaying,
      onCalculateRouteSuccess: this.onCalculateRouteSuccess,
      onCalculateRouteFailureForResult: this.onCalculateRouteFailureForResult,
      onNaviRouteNotify: this.onNaviRouteNotify,
      onUpdateGPSSignalStrength: this.onUpdateGPSSignalStrength,
    }
    this.listener = listener
    //添加导航事件回调监听。
    this.naviInstance.addAMapNaviListener(this.listener)
```

## 无起终点启动导航组件

```
//构建导航组件配置类，没有传入起点，所以起点默认为 “我的位置”
const params = new AmapNaviParams();
//启动导航组件
AmapNaviPage.getInstance().showRoutePage(params, null);
```

示例图：

![](https://a.amap.com/lbs/static/img/doc/doc_1763098805813_bbfc9.jpeg)

## 传入起终点启动导航组件

通过设置起点、途径点（最多支持三个）、终点启动导航组件；每个点数据可以通过经纬度、名称、高德 POIId 来描述，其参数规则如下：

1. 经纬度数据为必填参数；
    
2. 名称是可选参数仅用于显示地点名称，如果设置了名称参数，会优先显示所设置的名称，如果不传名称将使用默认值，如“终点”、“途径点1”；
    
3. 高德 POIId 是可选参数，但强烈建议传入，因为其可以有效的减少绕路情况的出现。设置高德 POIId 来启动导航组件时，将会执行 POI 的精确检索，获得 POI 详情后不仅会辅助算路，也会覆盖传入的经纬度和名称两个参数。
    
4. 当不设置起点信息时，会采用用户当前位置作为起点，并显示地点名称为“我的位置”。
    

```
const start = new NaviPoi("北京首都机场", new NaviLatLng(40.080525,116.603039), "B000A28DAE");
            //途经点
            const poiList = new ArrayList<NaviPoi>();
            poiList.add(new NaviPoi("善各庄地铁", new NaviLatLng(40.027021,116.478391), null));
            poiList.add(new NaviPoi("故宫", new NaviLatLng(39.918058,116.397026), "B000A8UIN8"));
            //终点
            const end = new NaviPoi("北京大学", new NaviLatLng(39.992873,116.310918), "B000A816R6");

            const params = AmapNaviParams.buildForPoi(start, poiList, end, AmapNaviType.Driver);

            AmapNaviPage.getInstance().showRoutePage(params, this.naviInfoCallback);
```

示例图：

![](https://alidocs.dingtalk.com/core/api/resources/img/5eecdaf48460cde5b7098e3da115e8b3a48d29c7ecccf50775b8339e1c4c2483d73fcbd75708105f8d68742cd653602afa4cc552274ccc037a2f6d5013ce2f7893de9e0a69a98faacd5ed93ee5fa131b0242bd66ccaafc97eb35c1922cdf0bdb?tmpCode=1dca33ab-6128-4c1d-8da7-aeaeee85a5c8)

## 退出导航组件

导航组件调起之后，用户可以点击“路径规划页面”左上角的回退按钮来退出导航组件，开发者也可以根据需要调用如下函数退出导航组件。 

```
AmapNaviPage.getInstance().exitRoutePage();
```

## 导航组件回调方法说明

INaviInfoCallback接口中提供了一系列回调方法，可以实现该接口后, 将回调实例通过启动组件方法的最后一个参数传入，关键回调如下（注意：使用导航组件以后，任然可以使用IAMapNavi注册导航回调，监听更多导航信息） 

```
/**
 * 导航初始化失败时的回调函数。
 */
onInitNaviFailure?: () => void;

/**
 * 导航播报信息回调函数。
 * @param s 播报文字。
 */
onGetNavigationText?: (s: string) => void;

/**
 * 当GPS位置有更新时的回调函数。
 * @param location 当前位置的定位信息。
 */
onLocationChange?: (location: AMapNaviLocation | null) => void;

/**
 * 到达目的地后回调函数。
 * @param isEmulaterNavi true代表是模拟导航到达目的地，false代表实时导航到达目的地
 */
onArriveDestination?: (isEmulaterNavi: boolean) => void;

/**
 * 启动导航后的回调函数
 * @param type 导航类型
 */
onStartNavi?: (type: NaviType) => void;

/**
 * 算路成功回调
 * @param ids 路线索引id数组，第一条为12，第二条为13，第三条为14。
 */
onCalculateRouteSuccess?: (ids: Int32Array) => void;

/**
 * 驾车路径规划失败后的回调函数。
 */
onCalculateRouteFailure?: (errorInfo: number) => void;

/**
 * 停止播报回调
 * 当退出组件导航页，或切换组件的播报模式为静音的时候，会触发该回调。建议在收到该回调时，停止外部一切导航相关的播报。
 */
onStopSpeaking?: () => void;

/**
 * 重新规划的回调
 * @param type 参见ReCalculateRouteType类
 */
onReCalculateRoute?: (type: number) => void;

/**
 * 退出组件或退出组件导航的回调函数
 */
onExitPage?: (pageType: AMapPageType) => void;

/**
 * 切换算路偏好回调
 */
onStrategyChanged?: (strategy: number) => void;

/**
 * 驾车路径导航到达某个途经点的回调函数。
 * @param wayID 到达途径点的编号，标号从0开始，依次累加。
 */
onArrivedWayPoint?: (wayID: number) => void;

/**
 * 组件地图白天黑夜模式切换回调
 * @param mapType 枚举值参考AMap类, 3-黑夜，4-白天
 */
onMapTypeChanged?: (mapType: number) => void;

/**
 * 导航视角变化回调
 * @param naviMode 导航视角, 1-正北朝上模式 2-车头朝上状态
 */
onNaviDirectionChanged?: (naviMode: AMapNaviViewTrackingMode) => void;

/**
 * 昼夜模式设置变化回调
 * @param mode 0-自动切换 1-白天 2-夜间
 */
onDayAndNightModeChanged?: (mode: number) => void;

/**
 * 播报模式变化回调
 * @param mode 1-简洁播报 2-详细播报 3-静音
 */
onBroadcastModeChanged?: (mode: number) => void;

/**
 * 比例尺智能缩放设置变化回调
 * @param enable 是否开启
 */
onScaleAutoChanged?: (enable: boolean) => void;
```
# 高级功能最后更新时间: 2025年11月17日

## 导航组件的配置类

AmapNaviParams中提供了很多配置方法，支持在启动同时传入，满足自定义需求。

## 启动相关配置

如果已经在外部通过AMapNavi计算过一条路线，可以选择启动组件不进行重新算路，使用现有路线进行导航。 

```
/**
 * 启动组件进行直接导航时，设置是否进行算路 (只有在直接跳转导航页的情况下才生效)
 *
 * @param needCalculateRouteWhenPresent true : 算路，false : 启动组件以后不会算路直接开启导航。默认为true。
 * @since 5.6.0
 */
public setNeedCalculateRouteWhenPresent(needCalculateRouteWhenPresent: boolean) 
```

可以选择启动组件的导航界面，还是路线规划界面。

```
// 组件参数配置
const params = AmapNaviParams.buildForPageType(start, null, end, AmapNaviType.Driver, AMapPageType.NAVI);
```

设置退出导航组件的时候是否停止并且销毁导航。

```
/**
 * 设置退出导航组件是否销毁导航实例
 *
 * @param destroy true-退出导航页时停止导航，退出组件时销毁导航
 *                false-退出组件不会销毁导航；当使用组件直接导航时，退出导航页也不会停止导航
 * @since 5.6.0
 */
public setNeedDestroyDriveManagerInstanceWhenNaviExit(destroy: boolean): AmapNaviParams 
```

其他重要配置参数。

```
/**
 * 设置车辆信息，进行尾号限行与货车导航
 *
 * @param carInfo {@link AMapCarInfo}<br>
 * @since 6.0.0
 */
public setCarInfo(carInfo: AMapCarInfo): AmapNaviParams 

/**
 * 设置是否使用内部语音播报
 *
 * @param isUseInnerVoice 是否使用内部语音播报
 *                        注意：6.1.0版本开始，默认值改为true
 * @since 6.0.0
 */
public setUseInnerVoice(isUseInnerVoice: boolean): AmapNaviParams

/**
 * 设置组件规划路线的策略，默认为{@link com.amap.api.navi.enums.PathPlanningStrategy#DRIVING_MULTIPLE_ROUTES_DEFAULT}，速度优先+躲避拥堵+距离较短
 *
 * @param routeStrategy {@link com.amap.api.navi.enums.PathPlanningStrategy}
 */
public setRouteStrategy(routeStrategy: PathPlanningStrategy): AmapNaviParams

/**
 * 设置播报模式
 *
 * @param context
 * @param mode  1-简洁播报 2-详细播报 3-静音模式
 * @since 7.1.0
 */
public setBroadcastMode(mode: AMapNaviBroadcastMode): AmapNaviParams

/**
 * 设置导航视角
 *
 * @param context
 * @param mode 0-车头朝上 1-正北朝上
 * @since 7.1.0
 */
public setCarDirectionMode(mode: AMapNaviViewTrackingMode): AmapNaviParams

/**
 * 设置比例尺智能缩放是否开启
 *
 * @param context
 * @param enable
 * @since 7.1.0
 */
public setScaleAutoChangeEnable(enable: boolean): AmapNaviParams
```
# 实时导航与模拟导航最后更新时间: 2025年11月17日

实时导航会自动打开手机卫星定位功能，通过手机的定位信息来驱动的导航，应用于实际的导航过程。模拟导航则不需要使用定位功能，仅用于室内模拟使用，目的是让您对导航功能有一些更直观的了解，比如预先了解既定路线的一些情况，如路况信息、电子眼信息等。注意：不要将模拟导航作为实际导航展示。

实时导航的显示效果如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1763098980809_e5bc6.jpeg)

模拟导航的显示效果如下：

![](https://a.amap.com/lbs/static/img/doc/doc_1763098997200_d96f5.jpeg)

实现导航的步骤如下：

## 第一步：创建导航单例，并设置Key

[获取Key](https://lbs.amap.com/api/harmonyosnext-navi-sdk/guide/get-key)

```
AMapNaviFactory.getAMapNaviInstance(getContext().getApplicationContext(), appkey)
```

## 第二步：创建导航组件

设置引擎类型、导航类型、起点、终点等信息。

```
build() {
    NavDestination() {
      AMapNaviComponent({
        appCustomerConfig: {
          mType: AmapNaviType.Driver, //引擎类型（驾车、骑行、步行）。当前支持驾车、货车、摩托车
          //默认模拟导航
          // mNaviType: NaviType.EMULATOR,
          //实时导航
          mNaviType: NaviType.GPS,
          start: {
            coordinate: this.startLatLng
          }, //起点
          end: {
            coordinate: this.endLatLng
          }, //终点
          // wayPoints: this.wayPoints, //途经点
          mRouteStrategy: 10, //设置默认规划路线策略
          serviceAreaDetailsEnable: true, //服务区信息
          goBack: () => {
            this.goback()
          },
        }
      })
    }.title('导航组件')
    .hideTitleBar(true)
    .onBackPressed(() => {
      this.goback()
      return true
    })
  }
```

## 第三步：规划路线

如选择驾车，会调用如下接口进行算路

```
  /**
   * 算路
   *
   * @param startPoiInfo 起点poi信息
   * @param endPoiInfo 终点poi信息
   * @param wayPoiInfos 途经点poi信息
   * @param drivingStrategy 导航策略
   * @return 发起算路是否成功
   */
  public calculateDriveRoute(startPoiInfo: CorePoiInfo| null, endPoiInfo: CorePoiInfo| null, wayPoiInfos: ArrayList<CorePoiInfo> | null, drivingStrategy: number):  boolean {}
```

## 第四步：接收算路回调

```
/**
 * 路线规划成功回调，包括算路、导航中偏航、用户改变算路策略、行程点等触发的重算，具体算路结果可以通过{@link com.amap.api.navi.model.AMapCalcRouteResult}获取
 * 可以通过CalcRouteResult获取算路错误码、算路类型以及路线id
 * @param routeResult {@link IAMapCalcRouteResult}
 * @since 1.0.0
 */
onCalculateRouteSuccess?:(routeResult: IAMapCalcRouteResult | null) => void

/**
 * 路线规划失败回调，包括算路、导航中偏航、用户改变算路策略、行程点等触发的重算，具体算路结果可以通过{@link com.amap.api.navi.model.AMapCalcRouteResult}获取
 * 可以通过CalcRouteResult获取算路错误码、算路类型以及路线id
 * @param routeResult {@link com.amap.api.navi.model.AMapCalcRouteResult}
 * @since 1.0.0
 */
onCalculateRouteFailureForResult?:(routeResult: IAMapCalcRouteResult| null) => void
```

在路线规划成功后，才可以开始导航。

## 第五步：算路成功后开始导航

```
/**
 * 开始导航。实时导航会自动打开手机卫星定位功能。模拟导航则不需要使用定位功能。
 *
 * @param naviType 导航类型，0:实时导航 1:模拟导航。
 * @return 启动成功或者失败。true是成功，false是失败。
 * @since 1.0.0
 */
startNavi(naviType: number): boolean;
```

设置参数0即实时导航，1即模拟导航。

## 多路线功能介绍

导航SDK从v2.2.4开始，支持多路线导航模式，即实时导航中拥有1到2条备选路线供用户选择，用户可以根据提供的时间差、距离差、费用差等信息，自行点击路线进行引导路线的变更，效果如图所示。 

![](https://a.amap.com/lbs/static/img/doc/doc_1763099083108_df426.png)

通过设置AMapNavi.setMultipleRouteNaviMode: 来开关多路线导航模式，然后开始算路，关键代码如下：

```
//开启多路线模式
mAMapNavi.setMultipleRouteNaviMode(true);
//起点
const start:NaviPoi = new NaviPoi("立水桥(北5环)", new LatLng(40.066957,116.320518), "");
//终点
const end:NaviPoi = new NaviPoi("新三余公园(南5环)", new LatLng(40.070882 ,116.319429), "");
//开启多路线模式
let isSuccess:boolean = mAMapNavi.calculateDriveRoute(start ,end, null, PathPlanningStrategy.DRIVING_MULTIPLE_ROUTES_DEFAULT);
```

## 注意点：

- 设置的导航模式会在下一次主动路径规划时生效, 建议在AMapNavi单例初始化时就进行设置。
    
- 多路线导航除了模式设置为true，还需同时满足以下4个条件才能够生效：
    
    - 路径规划时 AMapNaviDrivingStrategy 需选用多路径策略; 
        
    - 起终点的直线距离需<=80KM; 
        
    - 不能有途经点;
        
    - 支持货车类型，但多路线模式会消耗货车算路服务配额。
# 平行路检测最后更新时间: 2025年11月17日

平行路检测支持“主辅路状态检测”和“高架桥上下状态检测”。当用户所在的位置，具有两条相邻的平行路，如城市快速路的主干道和辅路，绕城高架的桥上和桥下，会收到ParallelRoadListener的回调，表明目前是支持用户自行切换平行路来触发重算的。 

比如AMapNaviParallelRoadStatus.mParallelRoadStatusFlag为1，表明SDK认为目前自车位置是在主路，如果用户当前确实是在主路，用户就无需做任何动作，如果用户当前是在辅路，那么表明SDK的推测是错的，用户可以点击在主路按钮来切换到辅路。

```
/**
 * 道路切换回调类
 */
export  class AMapNaviParallelRoadStatus implements IAMapNaviParallelRoadStatus {
  STATUS_NONE: number = 0;
  STATUS_MAIN_ROAD: number = 1;
  STATUS_SIDE_ROAD: number = 2;
  mParallelRoadStatusFlag: number = 0;
  mElevatedRoadStatusFlag: number = 0;
  status: number = 0;

  /**
   * 主辅路标识（默认0）
   * 0：无主辅路（车标所在道路旁无主辅路）
   * 1：车标在主路（车标所在道路旁有辅路）
   * 2：车标在辅路（车标所在道路旁有主路）
   *
   */
  public getmParallelRoadStatusFlag():  number {
    return this.mParallelRoadStatusFlag;
  }

  /**
   * 高架上下标识（默认0）
   * 0：无高架
   * 1：车标在高架上（车标所在道路有对应高架下）
   * 2：车标在高架下（车标所在道路有对应高架上）
   *
   */
  public getmElevatedRoadStatusFlag():  number {
    return this.mElevatedRoadStatusFlag;
  }

  /**
   * 道路切换切换状态
   * 0：非路线切换期间
   * 1：道路切换期间
   *
   */
  public getStatus():  number {
    return this.status;
  }
}
```

开发者可以根据回调返回的值提供对应的操作界面，调用AMapNaviCoreManager 的如下函数来让用户切换平行路：

```
/**
 * 切换平行路
 *
 * @param type 类型
 *             <li>1:主辅路切换</li>
 *             <li>2:高架桥上下切换</li>
 */
public switchParallelRoad(type: number):  void {
  AMapNaviNative.nativeSwitchParallelRoad(type);
}
```

操作界面可以参考下图：

![](https://a.amap.com/lbs/static/img/doc/doc_1763100077877_72699.png)

![](https://a.amap.com/lbs/static/img/doc/doc_1763100082351_b3245.png)

![](https://a.amap.com/lbs/static/img/doc/doc_1763100087014_539f7.png)

![](https://a.amap.com/lbs/static/img/doc/doc_1763100091509_8fccd.png)

![](https://a.amap.com/lbs/static/img/doc/doc_1763100096164_c81a0.png)# 导航实时数据获取最后更新时间: 2025年11月17日

在实际驾车导航中，导航SDK会通过AMapNaviListener监听器实时的透出导航信息与数据，可帮助您进行UI的定制化开发，是HUD和智能硬件的解决方案。骑行、步行与驾车一致，同样可以通过AMapNaviListener来获取导航事件与数据。

## 注册一般导航事件与数据监听（驾车、骑行、步行通用）：

```
naviInstance = AMapNaviFactory.getAMapNaviInstance(getContext().getApplicationContext(), appkey)
naviInstance.addAMapNaviListener({
  // 导航数据数据更新回调
  onNaviInfoUpdate: (naviInfo: INaviInfo) => {
   LogUtil.i('Navi_Demo','naviListener', 'onNaviInfoUpdate: ' + naviInfo.mRouteRemainDis + ' onUpdateNaviInfo curRouteName: ' + naviInfo.mCurRoadName)
  },
  
  // 算路成功回调
  onCalculateRouteSuccess: (routeResult: IAMapCalcRouteResult | null) => {
   console.info('demo 算路成功')
  },
  
  // 开始导航回调
  onStartNavi: (type: number) => {
   console.info('onStartNavi: ' + type)
  }
})
```

## 主要导航信息NaviInfo

NaviInfo主要指的是导航信息，比如当前道路名称、距离终点的时间和距离、没有避开的设施信息等。可通过AMapNaviListener中的onNaviInfoUpdate 回调接口更新导航信息。自定义导航视图AMapNaviView，以及导航组件中导航页顶部诱导面板、底部面板的信息，就是主要从该回调获取的。 

```
/**
 * 导航引导信息回调。
 *
 * @param naviInfo 导航信息类对象。
 * @since 1.0.0
 */
onNaviInfoUpdate?: (naviInfo: INaviInfo) => void
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763100189162_b62bc.png)

## 路口放大图

路口放大图包含了显示和隐藏两个回调，又根据放大图类别为实景图还是模型图分为两套，一共4个回调，均位于MessageDispatcher中，仅对驾车有效，如下： 

```
/**
 * 显示路口放大图（模型图）
 */
public showModeCross(modelCross: AMapModelCross): void {
  this.doShowModeCross(modelCross);
}
/**
 * 显示路口放大图（实景图）
 */
public showCross(cross: AMapNaviCross): void {
  this.doShowCross(cross);
}
/**
 * 隐藏路口放大图（模型图）
 */
public hideModeCross(): void {
  this.doHideModeCross();
}
/**
 * 隐藏路口放大图（实景图）
 */
public hideCross(): void {
  this.doHideCross();
}
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763100212396_b8fad.png)

![](https://a.amap.com/lbs/static/img/doc/doc_1763100226506_6a878.png)

## 车道线

```
//显示车道线信息
showLaneInfo = (laneInfo: IAMapLaneInfo | null) => {
  this.naviListenerArray.forEach(listener => {
   if (listener.showLaneInfo) {
    listener.showLaneInfo(laneInfo)
   }
  })
}

//隐藏车道线信息
hideLaneInfo = () => {
  this.naviListenerArray.forEach(listener => {
   if (listener.hideLaneInfo) {
    listener.hideLaneInfo()
   }
  })
}
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763100252708_4b7ff.png)

## 转向图标

导航过程中路口的转向图标信息，可从NaviInfo中获取，NaviInfo的获取上面已经介绍不再赘述，NaviInfo中转向图标相关的接口有2个，一个是直接获取转向图标的bitmap，另一个是获取转向图标类型的枚举值，可用于自定义转向图标的绘制。图标bitmap带有路网信息，更加直观。

转向图标对应NaviInfo中的接口： 

```
/**
 * 获取转向图标bitmap
 * <p>
 * 此接口可能返回为空，返回空的情况下，请使用 {@link NaviInfo#getIconType()} 来判别转向类型。请优先使用此接口来绘制转向图标。
 * </p>
 * 注意：<font color='red'>该接口仅驾车模式有效</font>
 *
 * @return  转向图标bitmap
 * @since 6.4.0
 */
public getIconBitmap():  image.PixelMap | null {
  return this.iconBitmap;
}

/**
 * 获取导航转向图标类型
 * <p>
 * 注意，当 {@link NaviInfo#getIconBitmap()} 有返回值的时候，请优先使用其返回的Bitmap来绘制转向图标，这样结果更加准确。
 * <p/>
 *
 * @return 导航转向图标类型值。参见{@link com.amap.api.navi.enums.IconType}
 */
public getIconType():  number {
    return this.mIcon;
}
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763100285141_076c2.png)

## 路况信息

路况信息涉及的接口一共有2个，一个主动接口，位于路线类AMapNaviPath中的getTrafficStatuses ，返回的是当前路线的即时路况信息，可用来绘制光柱图。另一个为被动回调，为AMapNaviListener中的onTrafficStatusUpdate，当路线上的路况发生变化时会触发回调。

AMapNaviPath中的主动接口： 

```
/**
 * 获取当前路线的交通状态
 * <br>
 * 注意：<font color='red'>该接口仅驾车模式有效</font>
 * @return 交通状态对象集合
 * @since 1.0.0
 */
public getTrafficStatuses():  ArrayList<AMapTrafficStatus> | null {
  return this.trafficStatuses;
}
```

 AMapNaviListener中的被动接口：

```
/**
 * 当前方路况光柱信息有更新时回调函数。
 * 注意：<font color='red'>该接口仅驾车模式有效</font>
 * @since 1.0.0
 */
onTrafficStatusUpdate?:() => void
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763100317162_b3245.png)

注意：为了获取更加实时准确的路况信息，建议设置AMapNaviListener监听，在收到onTrafficStatusUpdate回调后，通过AMapNavi的getNaviPath或getNaviPaths接口拿到最新的路线对象，然后通过路线对象的getTrafficStatuses接口获取实时的路况。  

## 电子眼信息

电子眼信息包含电子眼的类型、是否限速、经纬度坐标、当前自车位置到电子眼的距离等信息。位于AMapNaviListener中。 

```
/**
 * 导航过程中的摄像头信息回调函数
 * 注意：<font color='red'>该接口仅驾车模式有效</font>
 * @param infoArray 摄像头对象数组
 * @since 1.0.0
 */

updateCameraInfo?:(infoArray: IAMapNaviCameraInfo[ ] | null) => void
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763100336222_539f7.png)

## 区间测速电子眼信息

区间测速电子眼信息包含了自车位置和区间测速路段的位置关系、一些实时更新的动态信息等。 

```
/**
 * 导航过程中的区间测速信息回调函数
 * 注意：<font color='red'>该接口仅驾车模式有效</font>
 * @param startCameraInfo  区间测速起点信息
 * @param endCameraInfo    区间测速终点信息
 * @param status           具体类型可参考{@link CarEnterCameraStatus}
 * @since 1.0.0
 */
updateIntervalCameraInfo?:(startCameraInfo: IAMapNaviCameraInfo| null, endCameraInfo: IAMapNaviCameraInfo | null, status: number) => void
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763100358379_8fccd.png)

## 服务区和收费站信息

服务区和收费站信息包含了服务区的类型、名称、经纬度坐标、自车位置到服务区的距离，可用于一些自定义的信息展示。 

```
/**
 * 服务区信息回调函数
 * 注意：<font color='red'>该接口仅驾车模式有效</font>
 * @param infoArray 服务区对象数组
 * @since 1.0.0
 */

onServiceAreaUpdate?:(infoArray: IAMapServiceAreaInfo[ ] | null) => void
```

![](https://a.amap.com/lbs/static/img/doc/doc_1763100379597_c81a0.png)# 智能巡航最后更新时间: 2025年12月10日

## 功能简介

智能巡航模式 是一种无需设置起点与终点、无需路径规划的轻量级导航引导模式。在驾车过程中，系统会自动播报前方交通设施、电子眼、拥堵路段等实时信息，提升驾驶安全性与体验感。

- 无需算路
    
- 无需起终点
    
- 支持语音/视觉提示
    
- 实时获取交通事件信息
    

- 巡航模式需联网使用。
    
- 巡航效果建议在真实车辆行驶或模拟定位环境中体验。
    
- 巡航模式与导航模式互斥，不可同时运行。
    

---

## 核心 API 使用说明

### 1. 获取导航实例

```
import { AMapNaviFactory } from "@amap/amap_lbs_navi";

const context = getContext().getApplicationContext();
this.mAMapNavi = AMapNaviFactory.getAMapNaviInstance(context, 'YOUR_API_KEY');
```

---

### 2. 设置巡航监听器（IAimlessModeListener）

实现 IAimlessModeListener 接口以接收各类巡航事件回调：

#### 回调方法说明：

|   |   |   |
|---|---|---|
|方法|触发时机|说明|
|onUpdateTrafficFacility(infos)|道路设施更新|如服务区、收费站、摄像头等|
|onUpdateAimlessModeElecCameraInfo(cameraInfo)|电子眼信息更新|包含距离、限速等|
|updateAimlessModeStatistics(stat)|统计信息更新|当前巡航里程、拥堵耗时等|
|updateAimlessModeCongestionInfo(info)|拥堵信息更新|当前道路拥堵状态及预计通过时间|

---

### 3. 启动/停止智能巡航

#### 启动巡航模式

```
this.mAMapNavi.startAimlessMode(mode: number);
```

|   |   |
|---|---|
|mode 值|播报内容|
|1|仅播报电子眼|
|2|仅播报特殊路段（如隧道、桥梁）|
|3|播报电子眼 + 特殊路段（推荐）|

```
tsthis.mAMapNavi.startAimlessMode(3); // 开启智能播报
```

#### 停止巡航模式

```
tsthis.mAMapNavi.stopAimlessMode();
```

---

## 模式切换规则

由于 导航模式 与 巡航模式 互斥，请遵循以下流程进行切换：

|   |   |   |
|---|---|---|
|当前状态|目标状态|操作步骤|
|正在导航|启动巡航|先调用 stopNavi() → 再调用 startAimlessMode()|
|正在巡航|启动导航|先调用 stopAimlessMode() → 再调用正常导航接口|

---

## 支持模拟测试（可选）

可通过 MockLocationManager 模拟路径行驶，验证巡航逻辑是否正常。

### 启用模拟定位步骤：

1. 设置模拟管理器：
    

```
this.mAMapNavi.setMockLocationManager(MockLocationManager.getInstance());
```

2. 添加路径计算成功监听：
    

```
this.mAMapNavi.addAMapNaviListener({
  onCalculateRouteSuccess: () => {
    const path = this.mAMapNavi?.getNaviPath();
    if (path) {
      this.mAMapNavi?.setEmulatorNaviSpeed(10); // 设置模拟速度：10km/h
      this.mAMapNavi?.startAimlessMode(3);
      this.mAMapNavi?.startMockLocation(path);
    }
  },
  onCalculateRouteFailure: (errorCode) => {
    console.error('路径规划失败:', errorCode);
  }
});
```

3. 发起路径规划请求：
    

```
const startList = new ArrayList<INaviLatLng>();
startList.add({ latitude: 40.037530, longitude: 116.417580 });

const endList = new ArrayList<INaviLatLng>();
endList.add({ latitude: 40.035570, longitude: 116.417020 });

const wayPoints = new ArrayList<INaviLatLng>();

this.mAMapNavi.calculateDriveRoute(startList, endList, wayPoints, 0);
```
# 语音合成最后更新时间: 2025年11月17日

## 内置语音控制

导航SDK在AMapNavi提供了内置语音功能，开启内置语音以后，导航SDK会使用SDK内部语音合成方案进行播报，外部无需关心语音播报相关内容。

内置语音开关接口:

```
/**
 * 设置使用内部语音播报
 *
 * @param isUseInnerVoice 是否使用内部语音播报， 默认为false
 * @param isCallBackText  isUseInnerVoice设置为true以后，{@link AMapNaviListener#onGetNavigationText}接口会继续返回文字，默认为false
 * @since 2.2.4
 */
setUseInnerVoice(isUseInnerVoice: boolean, isCallBackText?: boolean): void
```

如果您使用内置语音，可以通过如下接口来控制内置语音的播报行为：

```
/**
 * 开始内置语音播报，只有在使用内置语音的情况下才有效
 *
 * @since 2.2.4
 */
startSpeak(): void;

/**
 * 停止内置语音播报，只有在使用内置语音的情况下有效
 * 注意：调用该接口，会停止播放导航语音，但是仍然可以播放自定义语音
 *
 * @since 2.2.4
 */
stopSpeak(): void;
```

SDK 会通过AMapNaviListener类回调将播报的文字内容透传出来，如果您不想使用SDK的内置语音进行播报，也可以选择第三方的语音合成SDK（如：[阿里云语音](https://help.aliyun.com/product/54853.html)合成）将内容转化成声音信息，完成导航播报。以下是涉及到相关接口和回调：

```
/**
 * 导航播报信息回调函数。
 *
 * @param type 播报类型枚举，详情见 {NaviTTSType}
 * @param text 播报文案
 * @since 1.0.0
 */
onGetNavigationTextAndType?:(text: string | null, type: number) => void
```

如果您使用自己合成的方式来进行播报，需要在每句播报前和播报完成后设置一下AMapNavi中如下接口，保证不出现语音打断和延迟问题。

```
/**
 * 设置外部播放器是否正在播报
 *
 * @since 1.0.0
 */
setTtsPlaying(playing: boolean): void
```

## 自定义语音播报

如果您使用了导航sdk的内置语音，我们还提供了自定义语音的播报功能，可以根据您的需要，传入自定义的播报文案进行语音合成与播报。

```
/**
 * 播放自定义文字，注意如果当前正在播放导航语音，可能导致播放失败，只在内置语音下生效
 *
 * @param tts       要播放的文字
 * @param forcePlay 是否强制进行播报
 *                  true  如果当前有其他导航语音，会等导航语音播放完毕后播放该文字，但是可能导致导航丢失掉关键引导信息
 *                  false 如果当前有其他导航语音，则不播报
 * @return 播放是否成功 true 成功，false 失败
 * @since 2.2.4
 */
playTTS(tts: string, forcePlay: boolean): boolean
```
# 定位相关设置与回调最后更新时间: 2025年11月17日

导航SDK是强依赖定位的，当您初始化AMapNavi时，SDK内部会自行启动定位，默认周期为一秒定位一次，如果您有控制定位频率的需求，可以使用如下接口，为保证导航效果，建议定位频率一秒一次。 

```
/**
* 启动GPS定位, 带距离和时间参数。
* <p>
* 用户可以手动启动GPS，如果没有启动GPS， 在驾车或者步行导航启动时（startNavi）会自动启动。默认定位时间间隔为1秒，变化距离为0。
* </p>
*
* @param time 位置更新的时间间隔, 单位：秒。
* @param dis  位置更新的距离间隔,单位：米。
* @return 返回GPS启动是否成功。true代表成功，false代表失败。
* @since 2.2.4
*/
startGPS(time?: number , dis?: number): boolean

/**
* 停止手机卫星定位。
*
* @return 返回是否停止手机卫星定位成功。true，成功；false，失败。
* @since 2.2.4
*/
stopGPS(): boolean
```

定位相关回调接口在AMapNaviListener类中，接入如下，定位详细信息在AMapNaviLocation中。

```
/**
* 当位置信息有更新时的回调函数。
*
* @param location 当前位置的定位信息。
* @since 1.0.0
*/
onLocationChange?:(location: IAMapNaviLocation | null) => void

/**
* 用户手机位置信息设置是否开启的回调函数。
*
* @param enabled true,开启;false,未开启。
* @since 1.0.0
*/
onGpsOpenStatus?:(enabled: boolean) => void

/**
* 手机卫星定位信号强弱变化的回调
*
* @param isWeak true: 信号弱;false：信号强
* @since 2.2.4
*/
onGpsSignalWeak?:(isWeak: boolean) => void
```

手机定位信号可以分为卫星定位、网络定位，精度依次递减，导航是强依赖精确定位的，但有一些地方可能无法收到高精度的卫星定位信号，如城市里的高楼旁边，高架桥下等。所以在这种时候，我们需要网络定位信号来辅助导航，网络点导航是一个补偿逻辑，它能够让用户在定位信号弱的区域也享受到较为精准的导航效果。

是否为网络点导航可以使用IAMapNaviLocation中locationType方法来判断。

```
onLocationChange: (location: IAMapNaviLocation | null) => {
 console.info('onLocationChange', location?.locationType)
}
```
# 传入外部定位点数据最后更新时间: 2025年11月17日

传入外部定位点数据，等价于不再使用系统的定位点进行驱动了，导航SDK内部将会以您传入的定位点数据为标准进行无起点算路和实时导航，建议传入频率为一秒一次，否则可能影响导航效果。

## 第1步，开启使用外部定位点数据

调用IAMapNavi的setIsUseExtraGPSData方法开启使用外部定位点数据。

```
  /**
   * 设置是否使用外部定位数据.
   * 只有将此开关打开后，{@link AMapNavi#setExtraGPSData(int, Location)}方法才会生效。
   *
   * @param isUseExtraData 是否使用外部定位数据
   * @since 2.2.5
   */
  setIsUseExtraGPSData(isUseExtraData: boolean): void
```

## 第2步，传入外部定位点数据

调用IAMapNavi的setExtraGPSData方法传入外部定位点数据。注意：传入的定位点数据必须是WGS84坐标系（type传入1）或者高德坐标系（type传入2），并且经度、纬度、速度、精度、角度、时间参数缺一不可。

```
  /**
   * 此方法用于设置外部定位数据，并使用外部定位数据进行导航
   * 使用此方法前需要先调用{@link AMapNavi#setIsUseExtraGPSData(boolean)}将开关打开.
   *
   * @param type     坐标类型。如果使用系统默认返回的定位坐标，type值为1。使用高德坐标，type值传2
   * @param location 外部定位数据。Longitude、Latitude、Accuracy、Speed、Bearing、Time 缺一不可
   * @since 2.2.5
   */
  setExtraGPSData(type: number,location: AMapLocation): void
```
# 卫星定位信号强弱最后更新时间: 2025年11月17日

提供获取了当前卫星定位信号强弱的方法和回调。当卫星定位信号为弱时，可能会出现小车位置刷新不及时的问题

```
/**
* 手机卫星定位信号强弱变化的回调
*
* @param strength 0-未知 1-信号强 2-信号弱 3-智能定位
* @since 1.0.0
*/
onUpdateGPSSignalStrength?: (strength: number) => void
```

用于导航组件黑卡信号强弱显示

![](https://a.amap.com/lbs/static/img/doc/doc_1763100620690_57355.jpeg)![](https://a.amap.com/lbs/static/img/doc/doc_1763100623599_50e59.jpeg)![](https://a.amap.com/lbs/static/img/doc/doc_1763100626606_083fd.jpeg)
# 网络点导航最后更新时间: 2025年11月17日

在复杂城市环境中，例如高楼密集区、高架桥下方、隧道内部等场景，GPS 卫星信号容易受到遮挡或干扰，导致定位精度下降甚至完全丢失。为保障导航服务的连续性，高德导航 SDK 提供了“网络点导航”作为补偿机制。

当系统检测到卫星信号弱或不可用时，会自动切换至基于 Wi-Fi、基站等信息的网络定位方式，确保用户仍能获得基本的路径引导服务。这种模式虽然精度低于 GNSS 定位，但可有效避免导航中断。

本功能旨在实现对“是否进入网络点导航状态”的实时感知

通过监听导航过程中的定位变化事件，判断当前是否处于网络定位状态（即 locationType === 1），并在满足条件时触发提示。

该功能主要用于开发和调试阶段的状态可视化，正式上线版本中不会保留 UI 提示。

### 监听定位变化事件

导航 SDK 通过 AMapNaviListener 提供定位回调接口，其中 onLocationChange 是获取实时位置信息的核心方法。

```
tsonLocationChange: (location: IAMapNaviLocation | null) => {
  console.log('GPS定位状态：locationType', location?.locationType);
}
```

### 判断并提示网络定位状态

在 onLocationChange 回调中增加判断逻辑，一旦识别为网络定位，则弹出临时提示用于调试。

```
tsonLocationChange: (location: IAMapNaviLocation | null) => {
  console.info('onLocationChange - 当前定位类型:', location?.locationType);

  if (location?.locationType === 1) {
    // 【仅测试使用】显示当前为网络定位
    promptAction.showToast({
      message: '当前为网络定位',
      duration: 100000000  // 长时间显示，便于观察
    });
  }
}
```

图中所示弹窗仅为测试使用

![](https://a.amap.com/lbs/static/img/doc/doc_1763100696736_4b7ff.png)# 驾车/货车路线规划最后更新时间: 2025年09月29日

## 基本介绍

根据出发地、目的地、途经地以及路径策略设置，为用户量身设计出行方案。同时可结合实时交通，帮助用户绕开拥堵路段，提供更贴心、更人性化的驾车出行体验。要实现驾车、货车路径规划功能，以下两个类您需要了解：

- AMapNavi ：此类是导航功能管理类，提供路线规划、行前选路、导航中重算等方法。它是一个单例，通过getInstance方法获取该单例，通过destroy方法来销毁该单例。
    
- AMapNaviListener：此类是导航事件信息与数据协议类，提供算路导航过程中的事件（如：路径规划成功/失败、TTS字符串、GPS信号弱、到达目的地等）以及实时数据（如：诱导信息NaviInfo、定位信息、电子眼信息等）回调接口。
    

## 说明

- 路径规划功能需要联网使用
    
- 起终点信息可通过多种方式获取，如：使用坐标拾取器查询您需要的点的坐标；还可以通过搜索 SDK 中的 POI  搜索查询兴趣点，作为起终点。
    
- 最多支持设置 16 个途经点，注意：导航组件最多支持设置3个途径点。
    
- 路径的计算策略包含单一策略和多策略，通过多策略，可计算出多条规划路径，需要通过 AMapNavi 的 getNaviPaths 方法获取这些路径。
    

#### 1、算路策略

导航SDK提供21种驾车策略，分成两种类型：返回单一路径的策略和返回多条路径的策略，对应             PathPlanningStrategy 枚举。 

|   |   |   |
|---|---|---|
|策略ID|常量字段|策略描述|
|0|DRIVING_DEFAULT|速度优先，不考虑当时路况，返回耗时最短的路线，但是此路线不一定距离最短|
|1|DRIVING_SAVE_MONEY|费用优先，不走收费路段，且耗时最少的路线|
|2|DRIVING_SHORTEST_DISTANCE|距离优先，不考虑路况，仅走距离最短的路线，但是可能存在穿越小路/小区的情况|
|3|DRIVING_NO_EXPRESS_WAYS|速度优先，不走快速路，例如京通快速路（因为策略迭代，建议使用13）|
|4|DRIVING_AVOID_CONGESTION|躲避拥堵，但是可能会存在绕路的情况，耗时可能较长|
|5|DRIVING_MULTIPLE_PRIORITY_SPEED_COST_DISTANCE|多策略（同时使用速度优先、费用优先、距离优先三个策略计算路径）。其中必须说明，就算使用三个策略算路，会根据路况不固定的返回一到三条路径规划信息|
|6|DRIVING_SINGLE_ROUTE_AVOID_HIGHSPEED|速度优先，不走高速，但是不排除走其余收费路段|
|7|DRIVING_SINGLE_ROUTE_AVOID_HIGHSPEED_COST|费用优先，不走高速且避免所有收费路段|
|8|DRIVING_SINGLE_ROUTE_AVOID_CONGESTION_COST|躲避拥堵和收费，可能存在走高速的情况，并且考虑路况不走拥堵路线，但有可能存在绕路和时间较长|
|9|DRIVING_SINGLE_ROUTE_AVOID_HIGHSPEED_COST_CONGESTION|躲避拥堵和收费，不走高速|
|10|DRIVING_MULTIPLE_ROUTES_DEFAULT|返回结果会躲避拥堵，路程较短，尽量缩短时间，与高德地图的默认策略（也就是不进行任何勾选）一致|
|11|DRIVING_MULTIPLE_SHORTEST_TIME_DISTANCE|返回三个结果包含：时间最短；距离最短；躲避拥堵（由于有更优秀的算法，建议用10代替）|
|12|DRIVING_MULTIPLE_ROUTES_AVOID_CONGESTION|返回的结果考虑路况，尽量躲避拥堵而规划路径，与高德地图的“躲避拥堵”策略一致|
|13|DRIVING_MULTIPLE_ROUTES_AVOID_HIGHSPEED|返回的结果不走高速，与高德地图“不走高速”策略一致|
|14|DRIVING_MULTIPLE_ROUTES_AVOID_COST|返回的结果尽可能规划收费较低甚至免费的路径，与高德地图“避免收费”策略一致|
|15|DRIVING_MULTIPLE_ROUTES_AVOID_HIGHSPEED_CONGESTION|返回的结果考虑路况，尽量躲避拥堵而规划路径，并且不走高速，与高德地图的“躲避拥堵&不走高速”策略一致|
|16|DRIVING_MULTIPLE_ROUTES_AVOID_HIGHTSPEED_COST|返回的结果尽量不走高速，并且尽量规划收费较低甚至免费的路径结果，与高德地图的“避免收费&不走高速”策略一致|
|17|DRIVING_MULTIPLE_ROUTES_AVOID_COST_CONGESTION|返回路径规划结果会尽量的躲避拥堵，并且规划收费较低甚至免费的路径结果，与高德地图的“躲避拥堵&避免收费”策略一致|
|18|DRIVING_MULTIPLE_ROUTES_AVOID_HIGHSPEED_COST_CONGESTION|返回的结果尽量躲避拥堵，规划收费较低甚至免费的路径结果，并且尽量不走高速路，与高德地图的“避免拥堵&避免收费&不走高速”策略一致|
|19|DRIVING_MULTIPLE_ROUTES_PRIORITY_HIGHSPEED|返回的结果会优先选择高速路，与高德地图的“高速优先”策略一致|
|20|DRIVING_MULTIPLE_ROUTES_PRIORITY_HIGHSPEED_AVOID_CONGESTION|返回的结果会优先考虑高速路，并且会考虑路况躲避拥堵，与高德地图的“躲避拥堵&高速优先”策略一致|

您可以使用以上表格中的策略值进行直接算路，若您想实现和高德地图一样的 checkbox 选项，那么建议您直接使用我们封装的AMapNavi中的strategyConvert 方法来获取策略值。  

|   |   |   |   |   |
|---|---|---|---|---|
|方法名|参数说明|返回值说明|方法效果|备注|
|strategyConvert|avoidCongestion：是否躲避拥堵<br><br>avoidHighway：是否不走高速<br><br>avoidCost：是否避免收费<br><br>prioritiseHighway：是否高速优先<br><br>multipleRoute： 统一使用多路线算路。|int|进行算路策略转换，将传入的特定规则转换成 PathPlanningStrategy 的枚举值。|不走高速与高速优先不能同时为true。<br><br>高速优先与避免收费不能同时为true。|

#### 2、经纬度算路

传入起、终点的经纬度信息，来进行路线规划。

示例代码：  

```
const appKey = "您的appKey";
const naviInstance: IAMapNavi = AMapNaviFactory.getAMapNaviInstance(getContext().getApplicationContext(), appKey);

// 起点信息
const startList = new ArrayList<NaviLatLng>();
startList.add(new NaviLatLng(39.993308,116.473199));

// 终点信息
const endList = new ArrayList<NaviLatLng>();
endList.add(new NaviLatLng(39.917834, 116.397036));

// 经纬度算路
naviInstance.calculateDriveRoute(startList, endList, null, PathPlanningStrategy.DRIVING_MULTIPLE_ROUTES_DEFAULT);
```

![](https://a.amap.com/lbs/static/img/doc/doc_1758611519272_4f84f.jpeg)

#### 3、POI算路

传入起、终点的经纬度信息，来进行路线规划。

示例代码： 

```
const appKey = "您的appKey";
const naviInstance: IAMapNavi = AMapNaviFactory.getAMapNaviInstance(getContext().getApplicationContext(), appKey);

// 起点信息
let start: NaviPoi | string | null = null;
// 终点信息
let end: NaviPoi | string | null = null;

//注：以下三种类型任选一种即可

//1， 第一种类型： NaviPoi类型(POI ID)
start = new NaviPoi("龙城花园", null, "B000A8UF3J");
end = new NaviPoi("北京大学", null, "B000A816R6");

// //2， 第二种类型：NaviPoi类型(经纬度)
// start = new NaviPoi(null, new NaviLatLng(40.100204,116.376890), null);
// end = new NaviPoi(null, new NaviLatLng(39.941597,116.352869), null);

// //3， 第三种类型：string类型(POI ID)
// start = "B000A8UF3J";
// end = "B000A816R6"

naviInstance.calculateDriveRouteForPoi(start, end, null, PathPlanningStrategy.DRIVING_MULTIPLE_ROUTES_DEFAULT);
```

说明：POI算路中，NaviPoi对象内也可以传入经纬度信息，优先使用POIID，如果POIID无效，则使用经纬度算路。

![](https://a.amap.com/lbs/static/img/doc/doc_1758611541068_02519.jpeg)

#### 4、起点角度算路

在POI算路中，支持通过NaviPoi对象传入自定义的起点角度，根据不同的出发角度规划出对应合理的路线。需要注意的是，想要使用自定义的起点角度来算路时，则不能使用poiId，且需要传入经纬度信息与合法的角度值。

示例代码： 

```
const appKey = "您的appKey";
const naviInstance: IAMapNavi = AMapNaviFactory.getAMapNaviInstance(getContext().getApplicationContext(), appKey);

// 起点信息
let start: NaviPoi | string | null = null;
// 终点信息
let end: NaviPoi | string | null = null;

start = new NaviPoi(null, new NaviLatLng(40.100204,116.376890), null);
//设置起点角度
start.setDirection(35);
end = new NaviPoi(null, new NaviLatLng(39.941597,116.352869), null);

naviInstance.calculateDriveRouteForPoi(start, end, null, PathPlanningStrategy.DRIVING_MULTIPLE_ROUTES_DEFAULT);
```

#### 5、设置车辆信息

支持在算路前，通过相关接口设置车辆信息，包括车牌号、车型、货车宽高载重，以及算路时是否躲避限行等，充分考虑车牌限号、ETA限行、限高限重等车辆因素给路线规划带来的影响，计算出最合理的行驶路线，为出行带来便捷。

示例代码： 

```
const appKey = "您的appKey";
const naviInstance: IAMapNavi = AMapNaviFactory.getAMapNaviInstance(getContext().getApplicationContext(), appKey);

// 起点信息
let start: NaviPoi | string | null = null;
// 终点信息
let end: NaviPoi | string | null = null;

start = new NaviPoi("龙城花园", null, "B000A8UF3J");
end = new NaviPoi("北京大学", null, "B000A816R6");

const carInfo: AMapCarInfo = new AMapCarInfo();
//设置车牌
carInfo.mCarNumber = "京C123456";
//设置车辆类型， 0-燃油客车，1-燃油货车，2-纯电动客车，3-纯电动货车，4-插电式混动汽车，5-插电式混动货车，11-摩托车
carInfo.mCarType = 1;
//设置货车的轴数，mCarType = 1时候生效，取值[0-255]，默认为2
carInfo.mVehicleAxis = 2;
//设置货车的高度，单位：米，mCarType = 1时候生效，取值[0-25.5] 如:1.8，1.5等等。
carInfo.mVehicleHeight = 2;
//设置货车的最大宽度，单位：米，mCarType = 1时候生效，取值[0-25.5] 如:1.8，1.5等等。
carInfo.mVehicleWidth = 2;
//设置货车的核定载重，单位：吨，mCarType = 1时候生效，取值[0-6553.5]
carInfo.mVehicleWeight = 2;
//设置货车的最大长度，单位：米，mCarType = 1时候生效，取值[0-25] 如:1.8，1.5等等，默认6米
carInfo.mVehicleLength = 6;
//设置货车大小， 1-微型货车 2-轻型/小型货车 3-中型货车 4-重型货车
carInfo.mVehicleSize = 2;
//设置货车的总重，即车重+核定载重，单位：吨，mCarType = 1时候生效，取值[0-6553.5]
carInfo.mVehicleLoad = 4.5;
//设置是否躲避车辆限行， true代表躲避车辆限行，false代表不躲避车辆限行。默认为true
carInfo.isRestriction = true;
//设置货车重量是否参与算路， true-重量会参与算路；false-重量不会参与算路。默认为false
carInfo.mVehicleLoadSwitch = true;
naviInstance.setCarInfo(carInfo);

naviInstance.calculateDriveRouteForPoi(start, end, null, PathPlanningStrategy.DRIVING_MULTIPLE_ROUTES_DEFAULT);
```

#### 6、途经点算路

最多支持设置 16 个途经点的路线规划。

```
const appKey = "您的appKey";
const naviInstance: IAMapNavi = AMapNaviFactory.getAMapNaviInstance(getContext().getApplicationContext(), appKey);

// 起点信息
let start: NaviPoi | string | null = null;
// 终点信息
let end: NaviPoi | string | null = null;

//NaviPoi类型
start = new NaviPoi("龙城花园", null, "B000A8UF3J");
end = new NaviPoi("北京大学", null, "B000A816R6");

// 途经点信息
const wayPoints: ArrayList<NaviPoi> = new ArrayList<NaviPoi>();
wayPoints.add(new NaviPoi("途经点1", null, "B000A805M7"));
wayPoints.add(new NaviPoi("途经点2", null, "B0FFFAADBU"));
wayPoints.add(new NaviPoi("途经点3", null, "B0FFF5BER7"));

// 经纬度算路
naviInstance.calculateDriveRouteForPoi(start, end, wayPoints, PathPlanningStrategy.DRIVING_MULTIPLE_ROUTES_DEFAULT);
```

![](https://a.amap.com/lbs/static/img/doc/doc_1758611573860_549cf.jpeg)

## 货车路线规划

货车的路径规划策略中，会将货车特有的限高、限重、车型等信息加入到路径规划策略中进行计算。

特别注意：货车路径规划是收费接口，您如果申请试用或者正式应用都请通过工单系统[提交商务合作类工单](https://lbs.amap.com/dev/ticket/create/others)进行沟通，否则默认是无法算路成功的。

货车的算路接口和驾车都是一样的，SDK是通车辆信息来区别是否为货车的。AMapCarInfo的 CarType 为1\3\5时都为货车。 

```
const carInfo: AMapCarInfo = new AMapCarInfo();
//设置车牌
carInfo.mCarNumber = "京C123456";
//设置车辆类型， 0-燃油客车，1-燃油货车，2-纯电动客车，3-纯电动货车，4-插电式混动汽车，5-插电式混动货车，11-摩托车
carInfo.mCarType = 1;
//设置货车的轴数，mCarType = 1时候生效，取值[0-255]，默认为2
carInfo.mVehicleAxis = 2;
//设置货车的高度，单位：米，mCarType = 1时候生效，取值[0-25.5] 如:1.8，1.5等等。
carInfo.mVehicleHeight = 2;
//设置货车的最大宽度，单位：米，mCarType = 1时候生效，取值[0-25.5] 如:1.8，1.5等等。
carInfo.mVehicleWidth = 2;
//设置货车的核定载重，单位：吨，mCarType = 1时候生效，取值[0-6553.5]
carInfo.mVehicleWeight = 2;
//设置货车的最大长度，单位：米，mCarType = 1时候生效，取值[0-25] 如:1.8，1.5等等，默认6米
carInfo.mVehicleLength = 6;
//设置货车大小， 1-微型货车 2-轻型/小型货车 3-中型货车 4-重型货车
carInfo.mVehicleSize = 2;
//设置货车的总重，即车重+核定载重，单位：吨，mCarType = 1时候生效，取值[0-6553.5]
carInfo.mVehicleLoad = 4.5;
//设置是否躲避车辆限行， true代表躲避车辆限行，false代表不躲避车辆限行。默认为true
carInfo.isRestriction = true;
//设置货车重量是否参与算路， true-重量会参与算路；false-重量不会参与算路。默认为false
carInfo.mVehicleLoadSwitch = true;
naviInstance.setCarInfo(carInfo);
```

注意，务必在算路前进行车辆信息的设置，否则需要等到下次算路才生效。 

## 处理结果：

 当路线规划成功时，会触发 AMapNaviListener 的 onCalculateRouteSuccess 回调，在该回调函数中，可以获取路线对象，进行规划路线的显示： 

```
 this.naviInstance?.addAMapNaviListener({
      onCalculateRouteSuccess: (routeResult: IAMapCalcRouteResult | null) => {
        // 获取路线数据对象
        const paths: HashMap<number, AMapNaviPath> | null = this.naviInstance!.getNaviPaths();
        // 绘制显示路径
        ...
        
      }
    })
```

也可以直接开启导航：

```
 this.naviInstance?.addAMapNaviListener({
      onCalculateRouteSuccess: (routeResult: IAMapCalcRouteResult | null) => {
        // 开启导航
        this.naviInstance!.startNavi(NaviType.GPS)
      }
    })
```

如果路线规划失败，则会触发 AMapNaviListener 的 onCalculateRouteFailure 回调，可以在此回调中来执行相应处理逻辑
# 独立路径规划最后更新时间: 2025年09月29日

### 基本介绍

独立路径规划是指路径规划的结果不会自动应用于当前导航，也不会干扰当前的导航，需要手动调用API传入路径规划结果来开始导航。可用于不干扰本次导航的单独路径规划场景，比如路线预览等。适用于驾车/货车路径规划,支持以下几种功能的路径规划功能：

- 无起点路径规划：路径规划时，起点坐标传空
    
- 经纬度路径规划：路径规划时，起终点NaviPoi只传经纬度
    
- POI路径规划：路径规划时，可传入POIID，提高规划的准确性。
    

### 独立路径规划功能

要实现独立路径规划功能，需要了解以下几个接口：

### 驾车/货车独立路径规划的接口

调用接口如下，位于IAMapNavi中：

```
/**
* POI独立算路
*
* @param fromPoi       起点信息
* @param toPoi         终点信息
* @param wayPoints     途经点信息，最多支持16个途经点，超过16个会取前16个。如果POIID合法，优先使用ID参与算路，否则使用坐标点。注意:POIID和坐标点不能同时为空
* @param strategy      算路策略: 驾车参考 {@link com.amap.api.navi.enums.PathPlanningStrategy}， 骑步行参考 {@link TravelStrategy}
* @param transportType 交通类型 1-驾车 
* @param observer      算路结果监听器
* @return 规划路径所需条件和参数校验是否成功，不代表算路成功与否
* @since 2.2.3
*/
independentCalculateRoute(fromPoi: NaviPoi | null, toPoi: NaviPoi, wayPoints: ArrayList<NaviPoi> | null, strategy: number, transportType: number, observer: AMapNaviIndependentRouteListener | null): boolean
```

### 独立路径规划结果回调

独立算路与普通算路一样，需要监听算路回调结果。独立算路结果监听器AMapNaviIndependentRouteListener，在调用独立算路接口时，通过最后一个参数传入，内部通知算路结果。

AMapNaviIndependentRouteListener中一共有两个回调，如下：

```
/**
* 独立算路成功回调
*
* @param group 算路结果（路线组）
* @since 2.2.3
*/
onIndependentCalculateSuccess:(group: AMapNaviPathGroup)=> void;

/**
* 独立算路失败回调
*
* @param routeResult 失败信息
* @since 2.2.3
*/
onIndependentCalculateFail:(routeResult: AMapCalcRouteResult)=> void;
```

### 独立路径规划结果

算路成功时，会回调独立算路结果类 AMapNaviPathGroup 的一个对象。此类对象为一个路线集合，集合中会存储这当前的路线，并且可以操作路线的顺序，达到行前选路的效果。

AMapNaviPathGroup中核心方法如下：

```
/**
* 获取主路线
*
* @return
* @since 2.2.3
*/
public getMainPath():  AMapNaviPath | null 

/**
* 获取主路线的索引
*
* @return
* @since 2.2.3
*/
public getMainPathIndex():  number

/**
* 获取指定索引的路线
*
* @param index 路线索引
* @return
* @since 2.2.3
*/
public getPath(index: number):  AMapNaviPath | null

/**
* 获取路线组的路线数量
*
* @return
* @since 2.2.3
*/
public getPathCount():  number

/**
* 导航前选择主路线
*
* @param routeId 主路线的routeId，第一条路为12，第二条为13，第三条为14
* @since 2.2.3
*/
public selectRouteWithIndex(routeId: number):  boolean
```

### 独立路径导航

独立路径规划的路线结果可以为用户提供路线预览，也可以让用户用于导航，接口位于IAMapNavi中，调用方式如下：

```
/**
* 使用指定路线开始导航
*
* @param naviType  导航类型 {@link com.amap.api.navi.enums.NaviType}
* @param pathGroup 路线组
* @return true-成功 false-失败
* @since 2.2.3
*/
startNaviWithPath(naviType: number, pathGroup: AMapNaviPathGroup): boolean
```
# 摩托车路线规划最后更新时间: 2025年12月10日

从导航SDK v8.0.0版本开始，全面支持摩托车路径规划和导航功能。其中主要区别于驾车的部分，就是在摩托车的路径规划策略中，会将摩托车的车牌号、排量等信息加入到路径规划策略中进行计算。

特别注意：摩托车路径规划是收费接口，您如果申请试用或者正式应用都请通过工单系统提交商务合作类工单进行沟通，否则默认是无法算路成功的。

摩托车的算路接口和驾车都是一样的，SDK是通车辆信息来区别是否为摩托车的。AMapCarInfo的 CarType 为11时为摩托车。

```
let carInfo: AMapCarInfo = new AMapCarInfo()
carInfo.setCarType("11"); //设置车辆类型,11代表摩托车
carInfo.setCarNumber('京B66666');
```

注意，务必在算路前进行车辆信息的设置，否则需要等到下次算路才生效。

## 处理结果

当路线规划成功时，会触发 IAMapNaviListener 的 onCalculateRouteSuccess 回调，在该回调函数中，可以获取路线对象，进行规划路线的显示：

```
//算路成功回调
onCalculateRouteSuccess: (routeResult: IAMapCalcRouteResult | null) => {
  if (routeResult !== null && routeResult.routeId) {
    const paths: HashMap<number, AMapNaviPath> | null = this.naviInstance!.getNaviPaths();
  }
}
```

也可以直接开启导航：

```
//算路成功回调
onCalculateRouteSuccess: (routeResult: IAMapCalcRouteResult | null) => {
  if (routeResult !== null && routeResult.routeId) {
    this.naviInstance?.startNavi(NaviType.GPS);
  }
}
```

如果路线规划失败，则会触发 IAMapNaviListener 的 onCalculateRouteFailure 回调，可以在此回调中来执行相应处理逻辑。
# 显示模式与跟随模式最后更新时间: 2025年09月29日

## 显示模式

导航界面的显示模式分为：

- 锁车态：地图图面一直跟着定位位置的改变而移动，又由于自车图标也在移动，两者相互抵消，视觉上会感觉自车图标被锁在屏幕的一个固定的点上；
    
- 全览态：地图的中心点和缩放层级都调整到合适的值来让整条路线都显示在可见区域内；
    
- 普通态：地图图面一直不动，只有自车图标在移动。
    

![](https://a.amap.com/lbs/static/img/doc/doc_1758610351221_83b50.jpeg)          ![](https://a.amap.com/lbs/static/img/doc/doc_1758610354146_ea571.jpeg)

![](https://a.amap.com/lbs/static/img/doc/doc_1758610357157_18284.jpeg)

通过 AMapNaviViewOptions 中接口设置锁车相关配置。

```
/**
* 设置自动锁车逻辑开关
*
* @param autoLockCar true代表自动锁车，false代表不自动锁车
* @since 2.2.3
*/
public setAutoLockCar(autoLockCar: boolean):  void

/**
* 设置是否自动全览模式，即在算路成功后自动进入全览模式
* @param isAutoDisplay
* @since 2.2.3
*/
public setAutoDisplayOverview(isAutoDisplay: boolean):  void

/**
* 设置锁定地图延迟毫秒数。
*
* @param lockMapDelayed 延迟毫秒。
* @since 2.2.3
*/
public setLockMapDelayed(lockMapDelayed: number):  void 
```

## 注意：AMapNaviViewOptions.setAutoDisplayOverview()方法在新版本中不建议使用，可通过IAMapNavi.setShowMode()来动态设置模式。

```
/**
* 设置导航页面显示模式
*
* @param showMode 1-锁车态 2-全览态 3-普通态
* @since 2.2.3
*/
setShowMode(showMode: number): void
```

通过 IAMapNaviListener 类监听显示模式变化。

```
/**
*导航视图展示模式变化回调
*
* @param showMode 展示模式
* @since 2.2.3
*/
onNaviViewShowMode?: (showMode:number) => void
```

## 车头朝向

导航界面的车头朝上、正北朝上 

![](https://a.amap.com/lbs/static/img/doc/doc_1758610417786_9679c.jpeg)          ![](https://a.amap.com/lbs/static/img/doc/doc_1758610420459_ddf9c.jpeg)

通过IAMapNavi类调整车头朝向。

```
/**
* 设置车头朝向
* @param mode 车头朝向
*  0-CAR_UP_MODE 车头朝上模式
*  1-NORTH_UP_MODE 正北朝上模式
* @since 2.2.3
*/
setNaviMode(mode: number): void
```

通过IAMapNaviListener监听车头朝向变化。

```
/**
* 导航视角变化回调
*
* @param naviMode 导航视角，0:车头朝上状态；1:正北朝上模式。
* @since 2.2.3
*/
onNaviMapMode?: (naviMode:number) => void
```
# 自定义标注最后更新时间: 2025年09月29日

AMapNaviView可以分为两层，底层是以地图为容器的图面元素层，SDK会根据路线信息在地图上绘制自车标、起终点、交通路线、转向箭头、牵引线、红绿灯等元素。上层是以UI控件元素为主的View层，如路口大图、光柱图、全览按钮、设置按钮等。这里主要介绍一些常用标注的自定义，其他还有：交通路线的自定义，其他图面元素的自定义，UI控件的自定义。

## 车标样式

![](https://a.amap.com/lbs/static/img/doc/doc_1758610571861_83b50.jpeg)

驾车导航界面的车标是由蓝色箭头样式图标和方向罗盘图标两部分组成的，可以通过AMapNaviViewOptions类进行自定义，对应接口如下：

```
/**
* 设置自车的图片对象
* @param carPixelMap 车标对象
* @since 2.2.3
*/
public setCarPixelMap(carPixelMap: PixelMap | null):  void

/**
* 设置罗盘位图对象
* @param fourCornersPixelMap
* @since 2.2.3
*/
public setFourCornersPixelMap(fourCornersPixelMap: PixelMap | null):  void 
```

## 起点\终点

![](https://a.amap.com/lbs/static/img/doc/doc_1758610595520_ea571.jpeg)         ![](https://a.amap.com/lbs/static/img/doc/doc_1758610598687_18284.jpeg)

通过AMapNaviViewOptions类进行起终点图标自定义，对应接口如下：

```
/**
* 设置起点位图，须在画路前设置
* @param icon 起点位图
* @since 2.2.3
*/
public setStartPointPixelMap(icon: PixelMap | null):  void

/**
* 设置终点位图，须在画路前设置
* @param icon 终点位图
* @since 2.2.3
*/
public setEndPointPixelMap(icon: PixelMap | null):  void
```
# 自定义交通路线最后更新时间: 2025年09月29日

通过AMapNaviViewOptions可以进行路线相关元素的显示隐藏控制，包括自车、罗盘、交通信号灯、路线显隐、路线Marker图标的显隐控制；结合其中的RouteOverlayOption，可以控制路线相关属性的自定义，包括路线宽度、不同路况路线颜色、虚线颜色、置灰效果和颜色 。

## 路线显隐

![](https://a.amap.com/lbs/static/img/doc/doc_1758610687210_4a47a.png)

可以通过以下接口控制路线显隐，默认显示，隐藏路线时，摄像头、红绿灯、转向箭头、牵引线、起终点等也会一起隐藏。

```
/**
 * 设置是否自动显示交通路线，默认显示
 *
 * @param autoDrawRoute true, 自动显示；false，隐藏
 * @since 2.2.3
 */
public setAutoDrawRoute(autoDrawRoute: boolean):  void
```

## 自车、罗盘显隐

![](https://a.amap.com/lbs/static/img/doc/doc_1758610702220_fb5c8.png)

可以通过以下接口控制自车、罗盘显隐，默认显示，设置为隐藏时，牵引线也会被隐藏。

```
/**
 * 设置是否隐藏AMapNaviView上的CarOverlay，包括自车、罗盘
 * @param isVisible true 显示 false 不显示 默认为显示，设置为false时，牵引线也会隐藏
 * @since 2.2.3
 */
public setCarOverlayVisible(isVisible: boolean)
```

## 起终途点\步行轮渡扎点\禁行限行封路icon显隐

路线上的点位标记，包括起点、终点途经点、步行轮渡扎点、禁行限行封路图标。

![](https://a.amap.com/lbs/static/img/doc/doc_1758610720212_10fb1.png)

可以通过以下接口控制其显示和隐藏。

```
/**
 * 是否显示 起终途点\步行轮渡扎点\禁行限行封路icon
 * @param showStartEndVia 是否显示起终途点
 * @param showFootFerry   是否显示步行轮渡扎点
 * @param showForbidden   是否显示禁行限行图标
 * @since 2.2.3
 */
public setRouteMarkerVisible(showStartEndVia: boolean, showFootFerry: boolean, showForbidden: boolean)
```

## 路线宽度

交通路线的宽度包含实线的宽度和虚线的宽度，虚线一般出现在需要步行和轮渡的地方，如下图所示：

![](https://a.amap.com/lbs/static/img/doc/doc_1758610736003_09dd8.png)

修改路线宽度可以调用如下接口，设置为0时，可恢复默认宽度：

```
/**
 * 设置导航线路的宽度
 *
 * @param lineWidth 单位：像素
 */
public setLineWidth(lineWidth: number):  void
```

## 路线颜色

路线的颜色包括不同路况（未知／畅通／缓慢／拥堵／严重拥堵）的路线颜色、虚线颜色、路过置灰的颜色

![](https://a.amap.com/lbs/static/img/doc/doc_1758610752790_8266e.png)

可以通过以下接口自定义不同路况下的路线颜色，虚线颜色以及路过置灰的颜色（走过的路颜色）：

```
/**
 * 设置自定义的虚线颜色
 * @param color
 * @since 2.2.3
 */
public setDashedLineColor(color: CoreRouteDashedLineColor | undefined):  void
/**
 * 设置不同路况下的路线颜色
 *
 * @param routeStatusColor
 * @since 2.2.3
 */
public setRouteStatusColor(routeStatusColor: ArrayList<CoreRouteTrafficStatusColor>| null):  void
/**
 * 设置自定义的走过路线的颜色
 *
 * @param routeGreyColor
 * @since 2.2.3
 */
public setRouteGreyColor(routeGreyColor: CoreRoutePassLineColor | undefined):  void
```

## 路过置灰

![](https://a.amap.com/lbs/static/img/doc/doc_1758610769218_f19c9.png)

路过置灰即将走过路线置成灰色效果，您只需调用如下接口进行效果的开关：

```
/**
 * 通过路线是否自动置灰
 * 可以使用{@link RouteOverlayOptions#setRouteGreyColor}改变颜色
 *
 * @param afterRouteAutoGray
 * @since 2.2.3
 */
public setAfterRouteAutoGray(afterRouteAutoGray: boolean):  void
```

在开启路过置灰功能时，还可以自定义其颜色

```
/**
 * 设置自定义的走过路线的颜色
 * @param routeGreyColor
 * @since 2.2.3
 * @exclude
 */
public setRouteGreyColor(routeGreyColor: CoreRoutePassLineColor | undefined):  void
```
# 自定义其他图面元素最后更新时间: 2025年09月29日

通过AMapNaviViewOptions和其中的RouteOverlayOption，可以进行一些图面元素的自定义，包括转向箭头、电子眼、牵引线、红绿灯

## 转向箭头

![](https://a.amap.com/lbs/static/img/doc/doc_1758610968900_4a47a.png)

转向箭头可以控制其显隐、颜色、宽度、是否为3D效果以及3D效果下的侧面颜色，

具体配置接口如下

```
/**
 * 设置路线转向箭头隐藏和显示
 *
 * @param isArrow true: 显示，false: 隐藏，默认为true
 * @since  2.2.3
 */
public setNaviArrowVisible(isArrow: boolean):  void
```

```
/**
 * 设置路线上转弯处箭头的颜色
 *
 * @param arrowColor 颜色值
 */
public setArrowColor(arrowColor: number):  void
/**
 * 设置路线上转弯处箭头的宽度,单位px 0代表默认宽度
 *
 * @param arrowColor 颜色值
 */
public setArrowWidth(arrowWidth: number):  void
/**
 * 设置是否显示3D箭头，默认显示
 * @param turnArrowIs3  true 显示,false 不显示
 * @since 2.2.3
 */
public setTurnArrowIs3D(turnArrowIs3: boolean):  void
/**
 * 设置3D箭头侧面颜色，只有显示 3D箭头情况加才有效
 * @param arrowSideColor
 * @since 2.2.3
 */
public setArrowSideColor(arrowSideColor: number):  void
```

## 电子眼

![](https://a.amap.com/lbs/static/img/doc/doc_1758610984338_fb5c8.png)

可以控制电子眼的显示和隐藏、电子眼距离的显示和隐藏

```
/**
 * 设置路线上的摄像头气泡是否显示。
 *
 * @param routeCameShow true代表显示，false代表不显示，默认显示
 * @since 2.2.3
 */
public setOnRouteCameShow(routeCameShow: boolean): void
```

```
/**
 * 设置电子眼的距离是否显示
 * @param show true, 显示；false，隐藏。默认隐藏
 * @since 2.2.3
 */
public setShowCameraDistance(show: boolean):  void
/**
 * 设置路线上的摄像头气泡是否显示
 *
 * @param cameraBubbleShow true代表显示，false代表不显示，默认显示
 * @deprecated 请配合 {@link RouteOverlayOptions#setOnRouteCameShow(boolean)} 与 {@link AMapNaviViewOptions#setRouteOverlayOptions(RouteOverlayOptions)} 使用
 */
public setCameraBubbleShow(cameraBubbleShow: boolean):  void
```

## 牵引线

牵引线指的是当前位置到终点的飞线，默认不显示。

![](https://a.amap.com/lbs/static/img/doc/doc_1758611001124_10fb1.png)

牵引线指的是当前位置到终点的飞线，可以控制其显示和隐藏、颜色

```
/**
 * 设置是否绘制牵引线（当前位置到目的地的指引线）。默认不绘制牵引线。
 *
 * @param color 设置牵引线颜色，为ARGB格式。不显示牵引线时，颜色设置为-1即可。
 */
public setLeaderLineEnabled(color: number):  void
```

## 红绿灯

![](https://a.amap.com/lbs/static/img/doc/doc_1758611014586_09dd8.png)

可以通过以下接口控制红绿灯的显示和隐藏

```
/**
 * 设置是否隐藏路线上的交通信号灯
 * @param isVisible true 显示 false 不显示 默认为显示
 * @since 2.2.3
 */
public setTrafficLightsVisible(isVisible: boolean)
```
# 自定义UI控件最后更新时间: 2025年09月29日

## 单元素自定义

可以通过AMapNaviViewOptions中如下接口进行单UI元素显示隐藏，只列出部分接口，更多功能请参考AMapNaviViewOptions类。 

```
、	/**
   * 设置菜单按钮是否在导航界面显示。
   *
   * @param enabled 菜单按钮是否在导航界面显示。true代表显示，false代表不显示。
   */
  public setSettingMenuEnabled(enabled: boolean):  void {
    this.isSettingMenuEnabled = enabled;
  }
    	/**
   * 设置导航界面是否显示路线全览按钮。
   *
   * @param isShow 设置全览按钮是否在导航界面显示，默认显示。true，显示；false，隐藏。
   */
  public setRouteListButtonShow(isShow: boolean):  void {
    this.isRouteListButtonShow = isShow;
  }
```

## 整体UI自定义

![](https://a.amap.com/lbs/static/img/doc/doc_1758611280726_8266e.png)

如上图所示，我们可以通过AMapNaviViewOptions中如下接口，来一键控制所有 UI 控件的显示和隐藏。 

```
  /**
   * 设置导航界面UI是否显示。
   * 注意：<font color='red'>该接口会同时隐藏模型放大图和实景放大图，隐藏后可以通过{@link AMapModeCrossOverlay}绘制放大图</font>
   * @param isLayoutVisible true导航界面显示，false导航界面不显示。
   */
  public setLayoutVisible(isLayoutVisible: boolean):  void {
    this.isLayoutVisible = isLayoutVisible;
  }
```

当不显示UI时，地图锚点也可以通过AMapNaviViewOptions进行自定义，可以根据自己的UI布局来调整比例尺的位置和锁车态时自车图标的默认显示位置，接口如下：

```
  /**
   * 设置自车位置锁定在屏幕中的位置
   *
   * @param x 取值范围：0-1 在x轴的位置，百分比
   * @param y 取值范围：0-1 在y轴的位置，百分比
   * @since 2.2.3
   */
  public setPointToCenter(x: number, y: number):  void {
    this.mapCenterX = x;
    this.mapCenterY = y;
  }
```

借助导航提供的View（DriveWay、CrossImage、CustomTrafficProgressBar、TrafficButtonView、PreviewRouteButton等），组装自己的导航界面。

创建AMapNaviComponent以后设置appCustomerConfig中调用一下方法。

```
 /**
   * 设置用户自定义的车道线
   * @param lazyDriveWayView
   * @since 2.2.3
   */
  setLazyDriveWayView?: ()=> void
    /**
   * 设置自定义的路口放大图
   *
   * @param zoomInIntersectionView
   * @since 2.2.3
   */
  setLazyZoomInIntersectionView?: ()=>void
    /**
   * 设置自定义的路况按钮视图
   *
   * @param lazyTrafficButtonView
   * @since 2.2.3
   */
  setLazyTrafficButtonView?:() => void
    /**
   * 设置用户自定义的全览按钮
   *
   * @param lazyOverviewButtonView
   */
  setLazyOverviewButtonView?:() => void
```
# 其他自定义能力最后更新时间: 2025年09月29日

UI界面定制指的是AMapNaviComponent中的图面元素和UI控件都是支持定制化修改的，以便您做出独一无二，符合您业务需求和App风格的导航界面。 

## 智能比例尺

![](https://a.amap.com/lbs/static/img/doc/doc_1758611391204_f19c9.png)

如上图，所谓的智能比例尺，就是锁车模式下为了在图面上提前看见下一个导航动作，根据您的自车位置自动缩放地图的一种效果。开启了智能比例尺，我们就能够以一个合适的缩放级别在图面上看见白色的转向箭头，比如当看见了左拐箭头，我们就有了预判，需要提前变道。您可以调用AMapNaviViewOptions中如下接口进行设置，支持导航中动态切换。 

```
  /**
   * 设置是否开启动态比例尺 (锁车态下自动进行地图缩放变化)
   *
   * @param isAutoChangeZoom true,自动改变；false，不自动改变
   * @since 2.2.3
   */
  public setAutoChangeZoom(isAutoChangeZoom: boolean):  void
```

## 日夜模式

![](https://a.amap.com/lbs/static/img/doc/doc_1758611413384_9eb9c.png)

上图为黑夜模式，AMapNaviComponent的日夜模式分为4种，白天模式、黑夜模式、根据日出日落时间自动切换白天黑夜、自定义地图样式(优先级最高)。您可以调用AMapNaviViewOptions中如下接口进行设置，支持导航中动态切换。 

```
  /**
   * 设置导航界面是否显示黑夜模式。
   * 此方法与{@link AMapNaviViewOptions#setCustomMapStylePath(String path)}方法相斥，不可同时调用.
   *
   * @param isNight 导航界面是否显示黑夜模式。true代表显示；false代表不显示。
   * @deprecated 请使用 {@link #setMapStyle(MapStyle mapStyle, String customStylePath)}
   */
  public setNaviNight(isNight: boolean):  void

    /**
   * 设置地图自定义样式文件的路径
   * 此方法与{@link AMapNaviViewOptions#setNaviNight(boolean isNight)}方法相斥，不可同时调用.
   *
   * @since 2.2.3
   * @deprecated 请使用 {@link #setMapStyle(MapStyle mapStyle, String customStylePath)}
   */
  public setCustomMapStylePath(path: string| null):  void 
    	/**
   * 设置是否开启自动黑夜模式切换，默认为false，不自动切换
   * @param isAutoNaviViewNightMode
   * @since 2.2.3
   * @deprecated 请使用 {@link #setMapStyle(MapStyle mapStyle, String customStylePath)}
   */
  public setAutoNaviViewNightMode(isAutoNaviViewNightMode: boolean):  void
```

这里需要注意的是，自定义地图样式与白天黑夜模式是互斥的，设置自定义样式以后，设置白天黑夜模式就不会生效了。 

## 自动锁车

所谓的自动锁车，就是当用户触碰了图面，让显示模式变成普通态，或者点击了全览按钮，让显示模式变成全览态，过一段时间后，显示模式是否需要再自动变成锁车态。您可以调用如下接口进行设置，支持导航中动态切换

```
  /**
   * 设置6秒后是否自动锁车
   *
   * @param autoLockCar true代表自动锁车，false代表不自动锁车
   */
  public setAutoLockCar(autoLockCar: boolean):  void
```
# 算路错误码最后更新时间: 2025年11月17日

进行路径规划时，如果算路失败了，会回调下面的接口，我们可以从IAMapCalcRouteResult中errorCode字段获取错误信息，下面的表格为errorCod的详细解释，此外errorDetail 和errorDescription也会包含一些额外的信息，需要排查问题的时候请务必提供这两个信息。 

```
  /**
   * 路线规划失败回调，包括算路、导航中偏航、用户改变算路策略、行程点等触发的重算，具体算路结果可以通过{@link com.amap.api.navi.model.AMapCalcRouteResult}获取
   * 可以通过CalcRouteResult获取算路错误码、算路类型以及路线id
   * @param routeResult {@link com.amap.api.navi.model.AMapCalcRouteResult}
   * @since 1.0.0
   */
  onCalculateRouteFailureForResult?:(routeResult: IAMapCalcRouteResult| null) => void
```

|   |   |   |
|---|---|---|
|响应码|问题说明|问题排查策略|
|2|网络失败|请检查网络是否通畅，稍候再试。|
|3|起点错误|请选择国内坐标点，确保经纬度格式正常。|
|4|协议解析错误|请将算路的起点、终点、途经点以及算路策略，通过[工单系统](https://lbs.amap.com/dev/ticket/create/19)反馈给我们。|
|6|终点错误|请选择国内坐标点，确保经纬度格式正常。|
|7|服务端编码异常|请将算路的起点、终点、途经点以及算路策略，通过[工单系统](https://lbs.amap.com/dev/ticket/create/19)反馈给我们。|
|8|数据缺乏预览数据|请将算路的起点、终点、途经点以及算路策略，通过[工单系统](https://lbs.amap.com/dev/ticket/create/19)反馈给我们。|
|9|数据格式错误|请将算路的起点、终点、途经点以及算路策略，通过[工单系统](https://lbs.amap.com/dev/ticket/create/19)反馈给我们。|
|10|没有找到通向起点的道路|请对起点进行调整。|
|11|没有找到通向终点的道路|请对终点进行调整。|
|12|没有找到通向途经点的道路|请对途径点进行调整。|
|13|用户key非法或过期|请检查key配置|
|17|请求超出配额|请将key、errorDetail 和errorDescription 通过[工单系统](https://lbs.amap.com/dev/ticket/create/19)反馈给我们。|
|18|请求参数非法|请检查是否有异常信息输出，请将key、errorDetail 和errorDescription 通过[工单系统](https://lbs.amap.com/dev/ticket/create/19)反馈给我们。|
|19|未知错误(可能是由于连接的网络无法访问外网)|请检查是否有异常信息输出，请将key、errorDetail 和errorDescription 通过[工单系统](https://lbs.amap.com/dev/ticket/create/19)反馈给我们。|
|20|起点/终点/途经点的距离太长|起点到途经点再到终点，两两相加的直线距离太长，导致的失败。一般发生在货车算路、骑步行算路。请将算路的起点、终点、途经点以及 NSError 信息，通过[工单系统](https://lbs.amap.com/dev/ticket/create/19)反馈给我们。|
|21|途经点错误|请选择国内坐标点，确保经纬度格式正常。|
|22|MD5安全码未通过验证,需要开发者判定key绑定的SHA1,package是否与sdk包里的一致.|请检查签名包名与KEY绑定关系是否正确|
|23|单位时间内访问过于频繁|请检查是否有异常信息输出，请将key、errorDetail 和errorDescription 通过[工单系统](https://lbs.amap.com/dev/ticket/create/19)反馈给我们。|
|24|请求中使用的key与绑定平台不符，例如：开发者申请的是js api的key，却用来调web服务接口|请检查key配置是否正确|
|25|使用路径规划服务接口时可能出现该问题，规划点（包括起点、终点、途经点）不在中国陆地范围内|请检查起终点是否正确，经纬度是否填反|
|26|使用路径规划服务接口时可能出现该问题，路线计算失败，通常是由于道路起点和终点距离过长导致|请检查起终点是否正确，经纬度是否填反|
|28|调用直接导航 没有算路 参数错误，缺失有效的导航路径，无法开始导航|请检查调起组件的时候是否算路成功|
|29|路径规划与当前导航状态不匹配。如果正在导航中，无法进行与导航不匹配的普通算路|请检查当前算路类型（驾车/骑行/步行）与当前正在导航的交通类型是否一致|
|2999|有新的独立算路任务在进行中导致本次独立算路失败|当有连续两次算路的时候，第一次算路会被取消返回算路失败错误码2999，请确保前一次算路结果返回后，再触发调用下一次算路|
## 导航 SDK

导航 SDK 从 ohpm 安装

```
"dependencies": {
  "@amap/amap_lbs_navi": ">=2.2.6"
}
```