# Location Kit简介https://gitcode.com/openharmony/docs/tree/OpenHarmony-6.0-Release/zh-cn/application-dev/reference/apis-location-kit

更新时间: 2025-12-16 16:35

## 场景介绍

移动终端设备已经深入人们日常生活的方方面面，如查看所在城市的天气、新闻轶事、出行打车、旅行导航、运动记录。这些习以为常的活动，都离不开定位用户终端设备的位置。

当用户处于这些丰富的使用场景中时，系统的位置能力可以提供实时准确的位置数据。对于开发者，设计基于位置体验的服务，也可以使应用的使用体验更贴近每个用户。

当应用在实现基于设备位置的功能时，如：驾车导航，记录运动轨迹等，可以调用该模块的API接口，完成位置信息的获取。

## 简介

位置子系统使用多种定位技术提供服务，如GNSS定位、基站定位、WLAN/蓝牙定位（基站定位、WLAN/蓝牙定位后续统称“网络定位技术”）；通过这些定位技术，无论用户设备在室内或是户外，都可以准确地确定设备位置。

- **坐标**
    
    系统以1984年世界大地坐标系统为参考，使用经度、纬度数据描述地球上的一个位置。
    
- **GNSS定位**
    
    基于全球导航卫星系统，包含：GPS、GLONASS、北斗、Galileo等，通过导航卫星、设备芯片提供的定位算法，来确定设备准确位置。定位过程具体使用哪些定位系统，取决于用户设备的硬件能力。
    
- **基站定位**
    
    根据设备当前驻网基站和相邻基站的位置，估算设备当前位置。此定位方式的定位结果精度相对较低，并且需要设备可以访问蜂窝网络。
    
- **WLAN、蓝牙定位**
    
    根据设备可搜索到的周围WLAN、蓝牙设备位置，估算设备当前位置。此定位方式的定位结果精度依赖设备周围可见的固定WLAN、蓝牙设备的分布，密度较高时，精度也相较于基站定位方式更高，同时也需要设备可以访问网络。
    

Location Kit除了提供基础的定位服务之外，还提供了地理围栏、地理编码、逆地理编码等功能和接口。

- 地理围栏（英语：GeoFence）是虚拟地理边界，当设备进入、离开某个特定地理区域时，可以接收自动通知和警告。

- 地理编码（英语：GeoCode）是表示地理实体（位置或要素）的代码。

正地理编码：根据地址获取地点的经纬度。

逆地理编码：获取经纬度对应的地点信息。

## 约束与限制

位置能力作为系统为应用提供的一种基础服务，需要应用在所使用的业务场景，向系统主动发起请求，并在业务场景结束时，主动结束此请求，在此过程中系统会将实时的定位结果上报给应用。

使用设备的位置能力，需要用户进行确认并主动开启位置开关。如果位置开关没有开启，系统不会向任何应用提供定位服务。

设备位置信息属于用户敏感数据，所以即使用户已经开启位置开关，应用在获取设备位置前仍需向用户申请位置访问权限。在用户确认允许后，系统才会向应用提供定位服务。

### 支持的国家/地区

支持的设备中Wearable设备支持以下[支持的国家/地区](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/location-kit-appendix#section161612127114)，其他设备仅支持中国境内（不包含中国香港、中国澳门、中国台湾）。

### 支持的设备

本kit仅适用于Phone、Tablet、PC/2in1和Wearable。

### 相关实例

针对Location Kit，有以下相关实例可供参考：

- Location：[Location Kit（ArkTS）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/DeviceManagement/Location)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/location-kit "Location Kit（位置服务）")
# 申请位置权限开发指导

更新时间: 2025-12-16 16:36

## 场景概述

应用在使用Location Kit系统能力前，需要检查是否已经获取用户授权访问设备位置信息。如未获得授权，可以向用户申请需要的位置权限。

系统提供的定位权限有：

- ohos.permission.LOCATION：用于获取精准位置，精准度在米级别。
- ohos.permission.APPROXIMATELY_LOCATION：用于获取模糊位置，精确度为5公里。
- ohos.permission.LOCATION_IN_BACKGROUND：用于应用切换到后台仍然需要获取定位信息的场景。

Location Kit接口对权限的要求参见：[Location Kit API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/location-api)。

## 开发步骤

1. 开发者可以在应用配置文件中声明所需要的权限并[向用户申请授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/request-user-authorization)。
2. 当APP运行在前台，且访问设备位置信息时，申请位置权限的方式如下：
    
    **表1** 位置权限申请方式介绍
    
    |申请位置权限的方式|是否允许申请|申请成功后获取的位置的精确度|
    |:--|:--|:--|
    |申请ohos.permission.APPROXIMATELY_LOCATION|是|获取到模糊位置，精确度为5公里。|
    |同时申请ohos.permission.APPROXIMATELY_LOCATION和ohos.permission.LOCATION|是|获取到精准位置，精准度在米级别。|
    
3. 当APP运行在后台时，申请位置权限的方式如下：
    
    如果应用在后台运行时也需要访问设备位置，除了按照步骤2申请权限外，还需要申请LOCATION类型的长时任务。
    
    长时任务申请可参考：[长时任务介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/continuous-task)。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/location-kit-intro "Location Kit简介")
# 获取设备的位置信息开发指导（ArkTS）

更新时间: 2025-12-16 16:36

## 场景概述

开发者可以调用HarmonyOS位置相关接口，获取设备实时位置，或者最近的历史位置，以及监听设备的位置变化。

对于位置敏感的应用业务，建议获取设备实时位置信息。如果不需要设备实时位置信息，并且希望尽可能的节省耗电，开发者可以考虑获取最近的历史位置。

## 接口说明

获取设备的位置信息所使用的接口如下，详细说明参见：[Location Kit API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/location-api)。

本模块能力仅支持WGS-84坐标系，如需转换成其他坐标系，请参考[坐标转换工具](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-convert-coordinate)。

**表2** 获取设备的位置信息接口介绍

|接口名|功能描述|
|:--|:--|
|[on(type: 'locationChange', request: LocationRequest \| ContinuousLocationRequest, callback: Callback<Location>): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanageronlocationchange)|开启位置变化订阅，并发起定位请求。|
|[off(type: 'locationChange', callback?: Callback<Location>): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanagerofflocationchange)|关闭位置变化订阅，并删除对应的定位请求。|
|[getCurrentLocation(request: CurrentLocationRequest \| SingleLocationRequest, callback: AsyncCallback<Location>): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanagergetcurrentlocation)|获取当前位置，使用callback回调异步返回结果。|
|[getCurrentLocation(request?: CurrentLocationRequest \| SingleLocationRequest): Promise<Location>](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanagergetcurrentlocation-2)|获取当前位置，使用Promise方式异步返回结果。|
|[getLastLocation(): Location](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanagergetlastlocation)|获取最近一次定位结果。|
|[isLocationEnabled(): boolean](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanagerislocationenabled)|判断位置服务是否已经开启。|

## 开发步骤

1. 获取设备的位置信息，需要有位置权限，位置权限申请的方法和步骤见[申请位置权限开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/location-permission-guidelines)。
    
2. 导入geoLocationManager模块，所有与基础定位能力相关的功能API，都是通过该模块提供的。
    
    1. import { geoLocationManager } from '@kit.LocationKit';
    
3. 调用获取位置接口之前需要先判断位置开关是否打开。
    
    查询当前位置开关状态，返回结果为布尔值，true代表位置开关开启，false代表位置开关关闭，示例代码如下：
    
    1. import { geoLocationManager } from '@kit.LocationKit';
    2. try {
    3.     let locationEnabled = geoLocationManager.isLocationEnabled();
    4. } catch (err) {
    5.     console.error("errCode:" + err.code + ", message:"  + err.message);
    6. }
    
    如果位置开关未开启，可以拉起全局开关设置弹框，引导用户打开位置开关，具体可参考[拉起全局开关设置弹框](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-abilityaccessctrl#requestglobalswitch12)。
    
4. 单次获取当前设备位置。多用于查看当前位置、签到打卡、服务推荐等场景。
    
    - 方式一：获取系统缓存的最新位置。
        
        如果系统当前没有缓存位置会返回错误码。
        
        推荐优先使用该接口获取位置，可以减少系统功耗。
        
        如果对位置的新鲜度比较敏感，可以先获取缓存位置，将位置中的时间戳与当前时间对比，若新鲜度不满足预期可以使用方式二获取位置。
        
        1. import { geoLocationManager } from '@kit.LocationKit';
        2. import { BusinessError } from '@kit.BasicServicesKit'
        3. try {
        4.     let location = geoLocationManager.getLastLocation();
        5. } catch (err) {
        6.     console.error("errCode:" + JSON.stringify(err));
        7. }
        
    - 方式二：获取当前位置。
        
        首先要实例化[SingleLocationRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#singlelocationrequest12)对象，用于告知系统该向应用提供何种类型的位置服务，以及单次定位超时时间。
        
        - 设置LocatingPriority：
            
            如果对位置的返回精度要求较高，建议LocatingPriority参数优先选择PRIORITY_ACCURACY，会将一段时间内精度较好的结果返回给应用。
            
            如果对定位速度要求较高，建议LocatingPriority参数选择PRIORITY_LOCATING_SPEED，会将最先拿到的定位结果返回给应用。
            
            两种定位策略均会同时使用GNSS定位和网络定位技术，以便在室内和户外场景下均可以获取到位置结果，对设备的硬件资源消耗较大，功耗也较大。
            
        - 设置locatingTimeoutMs：
            
            因为设备环境、设备所处状态、系统功耗管控策略等的影响，定位返回的时延会有较大波动，建议把单次定位超时时间设置为10秒。
            
        
        以快速定位策略(PRIORITY_LOCATING_SPEED)为例，调用方式如下：
        
        1. import { geoLocationManager } from '@kit.LocationKit';
        2. import { BusinessError } from '@kit.BasicServicesKit'
        3. let request: geoLocationManager.SingleLocationRequest = {
        4.    'locatingPriority': geoLocationManager.LocatingPriority.PRIORITY_LOCATING_SPEED,
        5.    'locatingTimeoutMs': 10000
        6. }
        7. try {
        8.    geoLocationManager.getCurrentLocation(request).then((result) => { // 调用getCurrentLocation获取当前设备位置，通过promise接收上报的位置
        9.       console.log('current location: ' + JSON.stringify(result));
        10.    })
        11.    .catch((error:BusinessError) => { // 接收上报的错误码
        12.       console.error('promise, getCurrentLocation: error=' + JSON.stringify(error));
        13.    });
        14.  } catch (err) {
        15.    console.error("errCode:" + JSON.stringify(err));
        16.  }
        
    
    通过本模块获取到的坐标均为WGS-84坐标系坐标点，如需使用其它坐标系类型的坐标点，请进行坐标系转换后再使用。
    
    可使用三方地图提供的SDK能力进行坐标系转换。
    
5. 持续定位。多用于导航、运动轨迹、出行等场景。
    
    首先要实例化[ContinuousLocationRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#continuouslocationrequest12)对象，用于告知系统该向应用提供何种类型的位置服务，以及位置结果上报的频率。
    
    - 设置locationScenario：
        
        建议locationScenario参数优先根据应用的使用场景进行设置，该参数枚举值定义参见[UserActivityScenario](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#useractivityscenario12)，例如地图在导航时使用NAVIGATION参数，可以持续在室内和室外场景获取位置用于导航。
        
    - 设置interval：
        
        表示上报位置信息的时间间隔，单位是秒，默认值为1秒。如果对位置上报时间间隔无特殊要求，可以不填写该字段。
        
    
    以地图导航场景为例，调用方式如下：
    
    1. import { geoLocationManager } from '@kit.LocationKit';
    2. let request: geoLocationManager.ContinuousLocationRequest= {
    3.    'interval': 1,
    4.    'locationScenario': geoLocationManager.UserActivityScenario.NAVIGATION
    5. }
    6. let locationCallback = (location:geoLocationManager.Location):void => {
    7.    console.log('locationCallback: data: ' + JSON.stringify(location));
    8. };
    9. try {
    10.    geoLocationManager.on('locationChange', request, locationCallback);
    11. } catch (err) {
    12.    console.error("errCode:" + JSON.stringify(err));
    13. }
    
    如果不主动结束定位可能导致设备功耗高，耗电快；建议在不需要获取定位信息时及时结束定位。
    
    14. geoLocationManager.off('locationChange', locationCallback);
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/location-guidelines-index "获取设备的位置信息开发指导")
# 获取设备的位置信息开发指导（C/C++）

更新时间: 2025-12-16 16:36

## 场景介绍

开发者可以调用OpenHarmony位置相关接口，监听设备的位置变化。

## 函数说明

|名称|描述|
|:--|:--|
|OH_Location_IsLocatingEnabled(bool* enabled)|查询位置开关是否开启。|
|OH_Location_StartLocating(const Location_RequestConfig* requestConfig)|启动定位并订阅位置变化。|
|Location_ResultCode OH_Location_StopLocating(const Location_RequestConfig* requestConfig)|停止定位并取消订阅位置变化。|
|OH_LocationInfo_GetBasicInfo(Location_Info* location)|从定位结果中获取基本信息，如经纬度、海拔、速度等信息。|
|OH_LocationInfo_GetAdditionalInfo(Location_Info* location, char* additionalInfo, uint32_t length)|从定位结果中获取附加信息。附加信息是一个JSON格式的字符串。|
|OH_Location_CreateRequestConfig(void)|创建一个位置请求参数结构体实例。|
|OH_Location_DestroyRequestConfig(Location_RequestConfig* requestConfig)|销毁位置请求参数实例并回收内存。|
|OH_LocationRequestConfig_SetUseScene(Location_RequestConfig* requestConfig, Location_UseScene useScene)|设置发起定位时的用户活动场景。<br><br>如果设置了useScene，则powerConsumptionScene无效。<br><br>如果未设置useScene，且设置了powerConsumptionScene，则该参数生效。<br><br>如果两个参数都不设置，则默认useScene为LOCATION_USE_SCENE_DAILY_LIFE_SERVICE,powerConsumptionScene参数无效。|
|OH_LocationRequestConfig_SetPowerConsumptionScene(Location_RequestConfig* requestConfig, Location_PowerConsumptionScene powerConsumptionScene)|设置发起定位时的功耗场景。|
|OH_LocationRequestConfig_SetInterval(Location_RequestConfig* requestConfig, int interval)|设置定位结果上报时间间隔。|
|OH_LocationRequestConfig_SetCallback(Location_RequestConfig* requestConfig, Location_InfoCallback callback, void* userData)|设置用于接收位置上报的回调函数。|

## 开发步骤

1. 新建一个Native C++工程。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163648.62728801426803698704994853198009:50001231000000:2800:31946C39BA9DB259F43D8F74E6CBE6E61336A2BD78156E13D6F38F1284D96410.png)
    
2. 获取设备的位置信息，需要有位置权限，位置权限申请的方法和步骤见[申请位置权限开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/location-permission-guidelines)。
    
3. CMakeLists.txt文件中引入动态依赖库。
    
    1. target_link_libraries(entry PUBLIC libace_napi.z.so)
    2. target_link_libraries(entry PUBLIC libhilog_ndk.z.so)
    3. target_link_libraries(entry PUBLIC liblocation_ndk.so)
    
4. 在napi_init.cpp文件中编码，首先导入模块。
    
    1. #include "napi/native_api.h"
    2. #include "LocationKit/oh_location.h"
    3. #include "LocationKit/oh_location_type.h"
    4. #include "hilog/log.h"
    5. #include <stdlib.h>
    
5. 调用获取位置接口之前需要先判断位置开关是否打开。
    
    查询当前位置开关状态，返回结果为布尔值，true代表位置开关开启，false代表位置开关关闭，示例代码如下：
    
    1.  static napi_value OhLocationIsEnabled(napi_env env, napi_callback_info info)
    2.  {
    3.      bool isEnabled = false;
    4.      int resultCode = OH_Location_IsLocatingEnabled(&isEnabled);
    5.      napi_value result = NULL;
    6.      napi_get_boolean(env, isEnabled, &result);
    7.      return result;
    8.  }
    9.  // 在Init函数中补充接口。
    10.  EXTERN_C_START
    11.  static napi_value Init(napi_env env, napi_value exports)
    12.  {
    13.      napi_property_descriptor desc[] = {
    14.          {"ohLocationIsEnabled", NULL, OhLocationIsEnabled, NULL, NULL, NULL, napi_default, NULL},
    15.      };
    16.      napi_define_properties(env, exports, sizeof(desc) / sizeof(desc[0]), desc);
    17.      return exports;
    18.  }
    19.  EXTERN_C_END
    
6. 定位位置变化。
    
    1. // 定义一个请求参数
    2. struct Location_RequestConfig *g_requestConfig = NULL;
    3. void *mydata = NULL;
    
    4. // 定义一个回调函数用来接收位置信息
    5. void reportLocation(Location_Info* location, void* userData)
    6. {
    7.     Location_BasicInfo baseInfo = OH_LocationInfo_GetBasicInfo(location);
    8.     char additionalInfo[1024] = "";
    9.     Location_ResultCode result = OH_LocationInfo_GetAdditionalInfo(location, additionalInfo, sizeof(additionalInfo));
    10.     if (mydata == userdata) {
    11.         OH_LOG_INFO(LOG_APP, "userData is mydata");
    12.     }
    13.     return;
    14. }
    
    15. // 订阅位置信息
    16. static napi_value OhLocationStartLocating(napi_env env, napi_callback_info info)
    17. {
    18.     if (g_requestConfig == NULL) {
    19.         g_requestConfig = OH_Location_CreateRequestConfig();
    20.     }
    21.     OH_LocationRequestConfig_SetUseScene(g_requestConfig, LOCATION_USE_SCENE_NAVIGATION);
    22.     OH_LocationRequestConfig_SetInterval(g_requestConfig, 1);
    23.     mydata = (void *)malloc(sizeof("mydata")); // 用户自定义任意类型，callback 透传返回
    24.     OH_LocationRequestConfig_SetCallback(g_requestConfig, reportLocation, mydata);
    25.     OH_Location_StartLocating(g_requestConfig);
    26.     int32_t ret = 0;
    27.     napi_value result = NULL;
    28.     napi_create_int32(env, ret, &result);
    29.     return result;
    30. }
    
    31. //取消订阅位置信息， g_requestConfig要和订阅时传入的对象保持一致
    32. static napi_value OhLocationStopLocating(napi_env env, napi_callback_info info)
    33. {
    34.     OH_Location_StopLocating(g_requestConfig);
    35.     if (g_requestConfig != NULL) {
    36.         OH_Location_DestroyRequestConfig(g_requestConfig);
    37.         g_requestConfig = NULL;
    38.     }
    39.     free(mydata);
    40.     mydata = NULL;
    41.     int32_t ret = 0;
    42.     napi_value result = NULL;
    43.     napi_create_int32(env, ret, &result);
    44.     return result;
    45. }
    
    46. // 在Init函数中补充接口。
    47. EXTERN_C_START
    48. static napi_value Init(napi_env env, napi_value exports)
    49. {
    50.     napi_property_descriptor desc[] = {
    51.         {"ohLocationStartLocating", NULL, OhLocationStartLocating, NULL, NULL, NULL, napi_default, NULL},
    52.         {"ohLocationStopLocating", NULL, OhLocationStopLocating, NULL, NULL, NULL, napi_default, NULL},
    53.     };
    54.     napi_define_properties(env, exports, sizeof(desc) / sizeof(desc[0]), desc);
    55.     return exports;
    56. }
    57. EXTERN_C_END
    
7. 在types/libentry路径下index.d.ts文件中引入Napi接口。
    
    1.  export const ohLocationIsEnabled: () => boolean;
    2.  export const ohLocationStartLocating: () => number;
    3.  export const ohLocationStopLocating: () => number;
    
8. 删除Index.ets中的已废弃函数。
    
    1. .onClick(() => {
    2.     hilog.info(0x0000, 'testTag', 'Test NAPI 2 + 3 = %{public}d', testNapi.add(2, 3));
    3. })
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/location-guidelines "获取设备的位置信息开发指导（ArkTS）")
# 正地理编码与逆地理编码开发指导

更新时间: 2025-12-16 16:36

## 场景概述

使用经纬度坐标描述一个位置，非常准确，但是并不直观，面向用户表达并不友好。系统向开发者提供了以下两种转化能力。

- 正地理编码：将地理位置信息转化为具体经纬度坐标。
    
- 逆地理编码：将具体的经纬度坐标转化为地理位置信息。
    

其中地理编码包含多个属性来描述位置，包括国家、行政区划、街道、门牌号、地址描述等等，这样的信息更便于用户理解。

## 接口说明

进行经纬度坐标和地理位置信息的相互转化，所使用的接口说明如下，详细信息参见：[Location Kit API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/location-api)。

## 接口介绍

|接口名|功能描述|
|:--|:--|
|[isGeocoderAvailable(): boolean;](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanagerisgeocoderavailable)|判断正地理编码与逆地理编码服务是否可用。|
|[getAddressesFromLocation(request: ReverseGeoCodeRequest, callback: AsyncCallback<Array<GeoAddress>>): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanagergetaddressesfromlocation)|调用逆地理编码服务，将经纬度坐标转换为地理位置信息，使用callback回调异步返回结果。|
|[getAddressesFromLocationName(request: GeoCodeRequest, callback: AsyncCallback<Array<GeoAddress>>): void](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanagergetaddressesfromlocationname)|调用正地理编码服务，将地理位置信息转换为具体经纬度坐标，使用callback回调异步返回结果。|

## 开发步骤

说明

正地理编码与逆地理编码功能需要访问后端服务，请确保设备联网，以进行信息获取。

1. 导入geoLocationManager模块，所有与正地理编码&逆地理编码能力相关的功能API，都是通过该模块提供的。
    
    1. import { geoLocationManager } from '@kit.LocationKit';
    
2. 查询正地理编码与逆地理编码服务是否可用。
    
    - 调用isGeoServiceAvailable查询正地理编码与逆地理编码服务是否可用，如果服务可用再继续进行步骤3。如果服务不可用，说明该设备不具备正地理编码与逆地理编码能力，请勿使用相关接口。
        
        1. import { geoLocationManager } from '@kit.LocationKit';
        2. try {
        3.     let isAvailable = geoLocationManager.isGeocoderAvailable();
        4. } catch (err) {
        5.     console.error("errCode:" + JSON.stringify(err));
        6. }
        
3. 获取转化结果。
    
    - 调用getAddressesFromLocation，把经纬度坐标转化为地理位置信息。应用可以获得与此坐标匹配的[GeoAddress](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geoaddress)（地理编码地址信息）列表，应用可以根据实际使用需求，读取相应的参数数据。
        
        1. let reverseGeocodeRequest:geoLocationManager.ReverseGeoCodeRequest = {"latitude": 31.12, "longitude": 121.11, "maxItems": 1};
        2. try {
        3.     geoLocationManager.getAddressesFromLocation(reverseGeocodeRequest, (err, data) => {
        4.         if (err) {
        5.             console.log('getAddressesFromLocation err: ' + JSON.stringify(err));
        6.         } else {
        7.             console.log('getAddressesFromLocation data: ' + JSON.stringify(data));
        8.         }
        9.     });
        10. } catch (err) {
        11.     console.error("errCode:" + JSON.stringify(err));
        12. }
        
    - 调用getAddressesFromLocationName把位置信息转化为经纬度坐标。
        
        1. let geocodeRequest:geoLocationManager.GeoCodeRequest = {"description": "上海市浦东新区xx路xx号", "maxItems": 1};
        2. try {
        3.     geoLocationManager.getAddressesFromLocationName(geocodeRequest, (err, data) => {
        4.         if (err) {
        5.             console.log('getAddressesFromLocationName err: ' + JSON.stringify(err));
        6.         } else {
        7.             console.log('getAddressesFromLocationName data: ' + JSON.stringify(data));
        8.         }
        9.     });
        10. } catch (err) {
        11.     console.error("errCode:" + JSON.stringify(err));
        12. }
        
        应用可以获得与位置描述相匹配的[GeoAddress](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geoaddress)（地理编码地址信息）列表，其中包含对应的坐标数据。
        
        如果需要查询的位置描述可能出现多地重名的请求，可以设置[GeoCodeRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geocoderequest)，通过设置一个经纬度范围，以高效地获取期望的准确结果。
        

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/location-guidelines-capi "获取设备的位置信息开发指导（C/C++）")
# 地理围栏简介

更新时间: 2025-12-16 16:36

地理围栏（GeoFence）是一种基于地理位置的技术，它允许开发者设定特定的地理区域，在用户进入、离开或驻留在这个特定区域的时候，可以把该地理围栏事件（进入/离开/驻留）通知应用，应用在接收到这些事件时完成后面的业务逻辑，以达到提醒用户的目的。

HarmonyOS支持2种类型的地理围栏：端侧围栏和云侧围栏。端侧围栏是指由开发者来管理围栏的生命周期，比如创建围栏，删除围栏；云侧围栏是指开发者直接使用华为云侧的公共围栏。端侧围栏比较适合于开发者要使用自己的个性化围栏场景，云侧围栏比较适合于开发者要使用公共围栏的场景。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/geofence-guidelines-index "地理围栏开发指导")
# 端侧GNSS围栏开发指导

更新时间: 2025-12-16 16:36

目前端侧仅支持构建圆形围栏，并且依赖GNSS芯片的地理围栏功能，仅在室外开阔区域才能准确识别用户进出围栏事件。

应用场景举例：开发者可以使用地理围栏技术，在企业周围创建一个区域围栏，当用户进入这个区域，在移动设备上进行有针对性的提醒。

## 接口说明

地理围栏所使用的接口如下，详细说明参见：[Location Kit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager)。

## 开发步骤

1. 使用地理围栏功能，需要有ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION权限，位置权限申请的方法和步骤见[申请位置权限开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/location-permission-guidelines)。
2. 导入geoLocationManager模块、wantAgent模块和BusinessError模块。
    
    1. import { geoLocationManager } from '@kit.LocationKit';
    2. import { wantAgent } from '@kit.AbilityKit';
    3. import { BusinessError } from '@kit.BasicServicesKit'
    
3. 创建WantAgentInfo信息。
    
    场景一：创建拉起Ability的WantAgentInfo信息。
    
    1. // 通过WantAgentInfo的operationType设置动作类型
    2. let wantAgentInfo:wantAgent.WantAgentInfo = {
    3.     wants: [
    4.         {
    5.             deviceId: '',
    6.             bundleName: 'com.example.myapplication',
    7.             abilityName: 'EntryAbility',
    8.             action: '',
    9.             entities: [],
    10.             uri: '',
    11.             parameters: {}
    12.         }
    13.     ],
    14.     operationType: wantAgent.OperationType.START_ABILITY,
    15.     requestCode: 0,
    16.     wantAgentFlags:[wantAgent.WantAgentFlags.CONSTANT_FLAG]
    17. };
    
    场景二：创建发布公共事件的WantAgentInfo信息。
    
    18. // 通过WantAgentInfo的operationType设置动作类型
    19. let wantAgentInfo:wantAgent.WantAgentInfo = {
    20.     wants: [
    21.         {
    22.             action: 'event_name', // 设置事件名
    23.             parameters: {},
    24.         }
    25.     ],
    26.     operationType: wantAgent.OperationType.SEND_COMMON_EVENT,
    27.     requestCode: 0,
    28.     wantAgentFlags: [wantAgent.WantAgentFlags.CONSTANT_FLAG],
    29. }
    
4. 调用getWantAgent()方法进行创建WantAgent。
    
    并且在获取到WantAgent对象之后调用地理围栏接口添加围栏，当设备进入或者退出该围栏时，系统会自动触发WantAgent的动作。
    
    1. let wantAgentObj : object | undefined = undefined;
    2. // 创建WantAgent
    3. wantAgent.getWantAgent(wantAgentInfo, (err, data) => {
    4.     if (err) {
    5.       console.error('getWantAgent err=' + JSON.stringify(err));
    6.       return;
    7.     }
    8.     console.info('getWantAgent success');
    9.     wantAgentObj = data;
    10.     let requestInfo:geoLocationManager.GeofenceRequest = {'scenario': 0x301, "geofence": {"latitude": 31.12, "longitude": 121.11, "radius": 100, "expiration": 10000}};
    11.     try {
    12.         geoLocationManager.on('gnssFenceStatusChange', requestInfo, wantAgentObj);
    13.     } catch (err) {
    14.         console.error("errCode:" + JSON.stringify(err));
    15.     }
    16. });
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/geofence-intro "地理围栏简介")
# 云侧围栏开发指导

更新时间: 2025-12-16 16:37

## 概述

云侧围栏是指开发者直接使用云侧公共围栏，当用户进入这个区域，在移动设备上进行有针对性的提醒。

## 开通云侧围栏服务

在开通定位服务前，请先参考“[应用开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview)”创建项目和应用工程。

说明

从HarmonyOS NEXT Developer Beta2起，开发者无需配置公钥指纹和Client ID。

**操作步骤**

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“开发与服务”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163659.99172216173534930437950006022162:50001231000000:2800:3C284851033ED847F31D281845123E2AF45E548AA8BBAD0DB16B8F2C75106E1D.png "点击放大")
    
2. 在项目列表中找到您的项目，在项目下的应用列表中选择需要配置定位服务参数的应用。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163659.34907471036168015221775313982470:50001231000000:2800:64D8EED751322FD90D6281D6D1E3CE8739E396558BED05E68A4F17E67D602B3F.png "点击放大")

3. 在左侧导航栏选择“定位服务”，并点击收藏。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163659.25671156111084783561694919411565:50001231000000:2800:8E3C51FF3799DA41C458A7F273CD5499A07132A68AA10E8A1A63A7B24AB717C3.png "点击放大")

4. 在左侧导航栏选择“构建 > 定位服务”。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163659.61618189045565859733350675834641:50001231000000:2800:C837236024CE672955A947A0EDA72246D5EF5B57F45324467FEC487CDAA84C63.png "点击放大")

说明

如果需要使用地理围栏，请确保已联系华为地图定位运营团队（locationkit@huawei.com）开通服务。

## 使用场景

1.开发者可以通过该围栏扩展能力来使用云侧公共围栏；

2.开发者首先需要在AGC（AppGallery Connect）平台定位服务选择右侧“添加围栏组触发”开始创建地理围栏。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163659.37030773765480200636869450013116:50001231000000:2800:B70219ADDA47CC36F3EBE32516E9B10810353C05A16B460E25A7D08434B8EFEE.png "点击放大")

3.可以根据商圈、景点等类别，配置围栏组下发围栏策略；

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163700.66362813417677762914913421935763:50001231000000:2800:61E365702DE8F76F07E5D4033E1D84E3FEDE8E1FDF61A1D6D1220BD24ADEB28A.png "点击放大")

4. 定位服务在满足围栏触发条件后，通过FenceExtensionAbility把围栏事件通知给APP，APP接收到围栏事件后完成相关的业务处理。

## 接口介绍

接口详情参见[FenceExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-fenceextensionability)。

|接口|描述|
|:--|:--|
|onFenceStatusChange(transition: geoLocationManager.GeofenceTransition, additions: Record<string, string>): void|接收系统通知的地理围栏事件，根据围栏事件类型和数据进行相应处理。|
|onDestroy(): void|接收FenceExtensionAbility的销毁事件并处理，会在FenceExtensionAbility销毁前回调。|

## 开发步骤

要实现一个地理围栏扩展服务，开发者需要实现[FenceExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-fenceextensionability)的能力，具体步骤如下：

1. 在工程Module对应的ets目录下，右键选择“New > Directory”，新建一个目录并命名为fenceextensionability;
2. 在fenceextensionability目录，右键选择“New > File”，新建一个.ets文件并命名为MyFenceExtensionAbility.ets;
3. 打开MyFenceExtensionAbility.ets，导入FenceExtensionAbility的依赖包，自定义类继承FenceExtensionAbility并实现onFenceStatusChange和onDestroy接口;
    
    示例代码如下：
    
    1. import { FenceExtensionAbility, geoLocationManager } from '@kit.LocationKit';
    2. import { wantAgent } from '@kit.AbilityKit';
    3. import { notificationManager } from '@kit.NotificationKit';
    
    4. export default class MyFenceExtensionAbility extends FenceExtensionAbility {
    5.   async onFenceStatusChange(transition: geoLocationManager.GeofenceTransition, additions: Record<string, string>): Promise<void> {
    6.     super.onFenceStatusChange(transition, additions);
    
    7.     // 接收围栏触发信息
    8.     console.info('MyFenceExtensionAbility onFenceStatusChange');
    
    9.     let poiId: string = additions['poiId'];// 围栏id，唯一标识，示例：'999287512272780934'
    10.     let policyType: string = additions['policyType'];// 策略类型：'0'-普通策略;'1'-标签策略
    11.     let policyResult: string = additions['policyResult'];// 策略结果：标签等策略的额外信息
    
    12.     console.info(`poiId:${poiId},policyType:${policyType},policyResult:${policyResult}`);
    
    13.     // 可以发送围栏业务通知
    14.     let wantAgentInfo: wantAgent.WantAgentInfo = {
    15.       wants: [
    16.         {
    17.           bundleName: 'com.huawei.hmos.locationtest.smartfence',
    18.           abilityName: 'EntryAbility'
    19.         } as Want
    20.       ],
    21.       actionType: wantAgent.OperationType.START_ABILITY,
    22.       requestCode: 100
    23.     };
    24.     let wantAgentMy = await wantAgent.getWantAgent(wantAgentInfo);
    25.     let notificationRequest: notificationManager.NotificationRequest = {
    26.       id: 1,
    27.       content: {
    28.         notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
    29.         normal: {
    30.           title: `围栏通知`,
    31.           text: `poiId:${poiId},policyType:${policyType},policyResult:${policyResult}`,
    32.         }
    33.       },
    34.       notificationSlotType: notificationManager.SlotType.SOCIAL_COMMUNICATION,
    35.       wantAgent: wantAgentMy
    36.     };
    37.     notificationManager.publish(notificationRequest);
    38.   }
    
    39.   onDestroy(): void {
    40.     super.onDestroy();
    41.     console.info('MyFenceExtensionAbility onDestroy');
    42.   }
    43. }
    
4. 在工程Module对应的[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中注册FenceExtensionAbility，type标签需要设置为fence，srcEntry标签表示当前FenceExtensionAbility组件所对应的代码路径。
    
    1. {
    2.   "module": {
    3.     "extensionAbilities": [
    4.       {
    5.         "name": "MyFenceExtensionAbility",
    6.         "srcEntry": "./ets/fenceextensionability/MyFenceExtensionAbility.ets",
    7.         "description": "MyFenceExtensionAbility",
    8.         "type": "fence",
    9.         "exported": false
    10.       },
    11.     ]
    12.   }
    13. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/geofence-guidelines "端侧GNSS围栏开发指导")
# 位置信息

### [](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/DeviceManagement/Location#%E4%BB%8B%E7%BB%8D)介绍

本示例使用 [geolocation](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/reference/apis-location-kit/js-apis-geolocation.md) 实现获取当前位置的经纬度，然后通过 [http](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/reference/apis-network-kit/js-apis-http.md) 将经纬度作为请求参数，获取到该经纬度所在的城市。通过 [AlphabetIndexer](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/reference/apis-arkui/arkui-ts/ts-container-alphabet-indexer.md) 容器组件实现按逻辑结构快速定位容器显示区域。

### [](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/DeviceManagement/Location#%E6%95%88%E6%9E%9C%E9%A2%84%E8%A7%88)效果预览

|首页|
|---|
|![](https://gitee.com/openharmony/applications_app_samples/raw/master/code/BasicFeature/DeviceManagement/Location/screenshots/devices/zh/position.png)|

使用说明

1. 进入主页，点击国内热门城市，配送地址会更新为选择的城市。点击右边字母索引条，可快速定位到想要选择的城市区域，点击该城市后若该城市还细化到区，继续点击该城市的区，配送地址会更新为城市/区，若未细化到区，则只选择城市。
2. 若测试机支持GPS，点击国内热门城市上面的定位图标，应用会获取本机所在经纬度，然后根据经纬度获取所在城市，定位图标后的城市会进行刷新，当前城市数据为模拟数据。

### [](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/DeviceManagement/Location#%E5%B7%A5%E7%A8%8B%E7%9B%AE%E5%BD%95)工程目录

```
position/src/main/ets/
|---components
|   |---mock
|   |   |---LocationMock.ts                         // 城市信息mock数据
|   |---model
|   |   |---data.ts                                 // AlphabetIndexer索引
|   |---net
|   |   |---HttpRequestResponse.ts                  // 网络请求
|   |---pages
|   |   |---Location.ts                             // 页面
|   |---utils
|   |   |---DataSource.ts                           // 懒加载数据格式
|   |   |---Logger.ts                               // 日志工具
```

### [](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/DeviceManagement/Location#%E5%85%B7%E4%BD%93%E5%AE%9E%E7%8E%B0)具体实现

- 本示例展示获取定位的功能在页面中直接调用，使用geolocation.on方法获取当前位置的经纬度，然后监听经纬度变化发送request请求获取对应城市信息，源码参考[Location.ets](https://gitee.com/openharmony/applications_app_samples/blob/master/code/BasicFeature/DeviceManagement/Location/position/src/main/ets/components/pages/Location.ets)。

### [](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/DeviceManagement/Location#%E7%9B%B8%E5%85%B3%E6%9D%83%E9%99%90)相关权限

[ohos.permission.INTERNET](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/permissions-for-all.md#ohospermissioninternet)

[ohos.permission.LOCATION](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/permissions-for-all.md#ohospermissionlocation)

[ohos.permission.LOCATION_IN_BACKGROUND](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/permissions-for-all.md#ohospermissionlocation_in_background)

[ohos.permission.APPROXIMATELY_LOCATION](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/permissions-for-all.md#ohospermissionapproximately_location)

### [](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/DeviceManagement/Location#%E4%BE%9D%E8%B5%96)依赖

不涉及。

### [](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/DeviceManagement/Location#%E7%BA%A6%E6%9D%9F%E4%B8%8E%E9%99%90%E5%88%B6)约束与限制

1. 本示例仅支持标准系统上运行，支持设备：GPS定位功能仅支持部分机型。
2. 本示例为Stage模型，已适配API version 9版本SDK，版本号：3.2.11.9。
3. 本示例需要使用DevEco Studio 3.1 Beta2 (Build Version: 3.1.0.400 构建 2023年4月7日)及以上版本才可编译运行。

### [](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/DeviceManagement/Location#%E4%B8%8B%E8%BD%BD)下载

如需单独下载本工程，执行如下命令：

```
git init
git config core.sparsecheckout true
echo code/BasicFeature/DeviceManagement/Location/ > .git/info/sparse-checkout
git remote add origin https://gitee.com/openharmony/applications_app_samples.git
git pull origin master
```