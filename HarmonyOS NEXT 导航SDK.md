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