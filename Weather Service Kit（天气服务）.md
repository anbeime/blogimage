# Weather Service Kit简介

更新时间: 2025-12-16 16:35

Weather Service Kit（天气服务）是鸿蒙生态下的一个数据提供服务，Weather Service Kit融合了多家气象行业TOPs供应商，提供专业、精准、稳定的超本地化天气预报服务，帮助开发者为用户提供更贴心的本地生活服务，支撑行业客户防灾减灾、降本增效。开发者可以轻松地在HarmonyOS应用/元服务中获取天气数据。

## 场景介绍

Weather Service Kit可以返回以下天气数据，满足开发者的天气数据使用需求：

- 天气预报：开发者可以通过Weather Service Kit获取城市级和POI级的天气预报，包括实况天气、48小时逐小时天气预报（海外城市24小时逐小时天气预报）、10日天气预报，包含天气状况、温度、风力、风向、湿度等全面的预报数据。
- 分钟级降水预报：为您提供附近方圆5km范围内、未来2小时的分钟级降雨态势预报，包含降水形态、降水强度等。
- 天气预警：为您提供气象局实时发布的天气和环境预警信息。
- 天气指数：为您提供未来3天的晾晒指数、穿衣指数、紫外线指数、路况指数、钓鱼指数等生活指数 。
- 天文数据：为您提供日出时间、日落时间、月出时间、月落时间、以及月相等数据。
- 潮汐：为您提供全国主要港口和城市的潮汐数据。

## 约束与限制

- 使用限制：Weather Service Kit当前仅面向系统应用开放，暂不对外开放。
- 设备限制：本kit仅适用于Phone、Tablet、PC/2in1、Wearable设备。

## 模拟器支持范围

本kit暂不支持模拟器。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/weather-service-kit-guide "Weather Service Kit（天气服务）")
# 开发准备

更新时间: 2025-12-16 16:36

在阅读本章节前，请先参考“[应用开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview)”完成基本准备工作及指纹配置，再继续进行以下开发活动。

## 开通天气服务

说明

Weather Service Kit当前仅面向系统应用开放，暂不对外开放。

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html#/)。
2. 选择“开发与服务”，找到您的项目，选择您创建的HarmonyOS应用。
3. 选择“开放能力管理”标签，勾选“天气服务”能力开关，点击保存按钮。

## 配置Profile文件

在接口调用过程中，天气服务会对您的Profile文件进行鉴权。因此，您需要在开通天气服务后，按照[配置签名信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-overview#section42841246144813)的流程，申请并配置签名信息。

## （可选）申请位置权限

获取用户当前位置的天气数据，需要调用Location Kit（位置服务）获取当前位置经纬度信息，使用前参考[申请权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#%E7%94%B3%E8%AF%B7%E6%9D%83%E9%99%90)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/weather-service-introduction "Weather Service Kit简介")
# 获取天气数据

更新时间: 2025-12-16 16:36

通过开发者提供的经纬度数据，获取天气数据，比如：实况数据、预警数据。

## 约束与限制

本kit支持Phone、Tablet、PC/2in1设备，并且从5.1.0(18)版本开始，新增支持Wearable设备。

## （可选）获取当前位置经纬度

当开发者需要查询当前位置的天气数据时，需要先[申请位置权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#%E7%94%B3%E8%AF%B7%E6%9D%83%E9%99%90)，并且获取当前位置的经纬度信息。获取当前位置的经纬度信息方法如下：

1. 导入模块。
    
    1. import { geoLocationManager } from '@kit.LocationKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 调用[getCurrentLocation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanagergetcurrentlocation-2)，获取经纬度。
    
    1. geoLocationManager.getCurrentLocation().then((result) => {
    2.   console.info('current location latitude: ' + result.latitude);
    3.   console.info('current location longitude: ' + result.longitude);
    4. }).catch((err: BusinessError ) => {
    5.   console.error(`getCurrentLocation failed. Code: ${err.code}, message: ${err.message}`);
    6. });
    

## 查询天气数据

Weather Service Kit依赖开发者提供的经纬度数据（精确到小数点后2位），返回格点天气数据。

1. 导入模块。
    
    1. import { weatherService } from '@kit.WeatherServiceKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 创建请求对象。
    
    - location：使用[当前位置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/weather-service-getweather#section546501255)的数据，或者填入查询目的地的经纬度。
    - limitedDatasets：为可选字段，传入一个数组，表示请求有限的数据集，取值范围参考weatherService.[Dataset](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/weather-service-weatherservice#section83091727192814)。
    
    1. let request: weatherService.WeatherRequest = {
    2.   location: {
    3.     latitude: 22.62,
    4.     longitude: 114.07
    5.   },
    6.   limitedDatasets: [weatherService.Dataset.CURRENT, weatherService.Dataset.ALERTS]
    7. }
    
    说明
    
    如果limitedDatasets参数不传值，或者传入的数组为空，则默认返回Weather Service Kit支持的所有数据。根据实际需要的天气数据设置limitedDatasets，可以大幅降低接口请求时延。
    
3. 请求数据。
    
    1. try {
    2.   let weather = await weatherService.getWeather(request);
    3.   if (weather.current) {
    4.     console.info('getWeather current temperature: ' + weather.current.temperature);
    5.   }
    6.   if (weather.alerts?.length) {
    7.     console.info('getWeather alert: ' + weather.alerts[0].title);
    8.   }
    9. } catch (err) {
    10.   err = err as BusinessError;
    11.   console.error(`getWeather failed. Code: ${err.code}, message: ${err.message}`);
    12. }
    
    说明
    
    getWeather接口的使用依赖当前Ability的Context，如果开发者在无法通过[getHostContext()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-uicontext-uicontext#gethostcontext12)接口获取到Context的环境中请求天气数据，例如使用worker或者taskpool的子线程场景，请使用[weatherService.getWeatherWithContext(context, request)](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/weather-service-weatherservice#section25641843201511)方法并提供Ability的Context信息。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/weather-service-preparations "开发准备")
# 如何获取指定城市的天气数据？

更新时间: 2025-12-16 16:36

先调用[getAddressesFromLocationName](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanagergetaddressesfromlocationname-1)方法获取指定城市的经纬度信息，然后根据返回的经纬度数据调用[getWeather](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/weather-service-weatherservice#section78181857767)方法获取天气数据。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/weather-service-faq "Weather Service Kit 常见问题")
# Weather Service Kit接口有定位功能吗？

更新时间: 2025-12-16 16:36

没有，获取当前位置的经纬度可参考[获取当前位置经纬度](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/weather-service-getweather#section546501255)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/weather-service-faq-1 "如何获取指定城市的天气数据？")
# 请求了分钟级降水预报/天气预警/潮汐，未返回任何数据。

更新时间: 2025-12-16 16:37

如果查询区域当时无短时降水、无天气预警发布或预警已经解除、无潮汐站点时，没有数据返回属于正常现象。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/weather-service-faq-2 "Weather Service Kit接口有定位功能吗？")
