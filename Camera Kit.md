# Camera Kit简介

更新时间: 2025-12-16 16:35

开发者通过调用Camera Kit(相机服务)提供的接口可以开发相机应用，应用通过访问和操作相机硬件，实现基础操作，如预览、拍照和录像；还可以通过接口组合完成更多操作，如控制闪光灯和曝光时间、对焦或调焦等。

## 开发场景

当开发者需要开发一个相机应用（或是在应用内开发相机模块）时，可参考以下开发模型了解相机的工作流程，进而开发相机应用。

如果开发者仅是需要拉起系统相机拍摄一张照片、录制一段视频，可直接使用CameraPicker，无需申请相机权限，直接拉起系统相机完成拍摄，具体可参考[CameraPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-camerapicker)。

## 开发模型

相机调用相机采集、加工图像视频数据，精确控制对应的硬件，灵活输出图像、视频内容，满足多镜头硬件适配（如广角、长焦、TOF）、多业务场景适配（如不同分辨率、不同格式、不同效果）的要求。

相机的工作流程如图所示，可概括为相机输入设备管理、会话管理和相机输出管理三部分。

- 相机设备调用相机采集数据，作为相机输入流。
    
- 会话管理可配置输入流，即选择哪些镜头进行拍摄。另外还可以配置闪光灯、曝光时间、对焦和调焦等参数，实现不同效果的拍摄，从而适配不同的业务场景。应用可以通过切换会话满足不同场景的拍摄需求。
    
- 配置相机的输出流，即将内容以预览流、拍照流或视频流输出。
    

**图1** 相机工作流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163515.35424618023153077197730854027476:50001231000000:2800:F6F25AD5F12DFFBEA6BA4D3F6AB5096361AE30C6FE40D9522E4AC42DD552F283.png)

了解相机工作流程后，建议开发者了解相机的开发模型，便于更好地开发相机应用。

**图2** 相机开发模型

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163515.58110490124308284230445531775990:50001231000000:2800:41E7F915D1856CA4720336CCB0ECAC1A293DC2FCCB1F050A2983AB003E54BBF1.png)

相机应用通过控制相机，实现图像显示（预览）、照片保存（拍照）、视频录制（录像）等基础操作。在实现基本操作过程中，相机服务会控制相机设备采集和输出数据，采集的图像数据在相机底层的设备硬件接口（HDI，Hardware Device Interfaces），直接通过BufferQueue传递到具体的功能模块进行处理。BufferQueue在应用开发中无需关注，用于将底层处理的数据及时送到上层进行图像显示。

以视频录制为例进行说明，相机应用在录制视频过程中，媒体录制服务先创建一个视频Surface用于传递数据，并提供给相机服务，相机服务可控制相机设备采集视频数据，生成视频流。采集的数据通过底层相机HDI处理后，通过Surface将视频流传递给媒体录制服务，媒体录制服务对视频数据进行处理后，保存为视频文件，完成视频录制。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-kit "Camera Kit（相机服务）")
# 申请相机开发的权限

更新时间: 2025-12-16 16:35

相机应用开发的主要流程包含开发准备、设备输入、会话管理、预览、拍照和录像等。

在开发相机应用时，需要先申请相机相关权限，确保应用拥有访问相机硬件及其他功能的权限，需要的权限如下表。在申请权限前，请保证符合[权限使用的基本原则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-permission-mgmt-overview#%E6%9D%83%E9%99%90%E4%BD%BF%E7%94%A8%E7%9A%84%E5%9F%BA%E6%9C%AC%E5%8E%9F%E5%88%99)。

- 使用相机拍摄前，需要申请**ohos.permission.CAMERA**相机权限。
- 当需要使用麦克风同时录制音频时，需要申请**ohos.permission.MICROPHONE**麦克风权限。
- 当需要拍摄的图片/视频显示地理位置信息时，需要申请**ohos.permission.MEDIA_LOCATION**，来访问用户媒体文件中的地理位置信息。

以上权限均需要配置文件权限声明和通过弹窗向用户申请授权，具体申请方式及校验方式，请参考[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)和[向用户申请授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/request-user-authorization)。

- 当需要读取图片或视频文件时，请优先使用媒体库[Picker选择媒体资源](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/photoaccesshelper-photoviewpicker)。
- 当需要保存图片或视频文件时，请优先使用[安全控件保存媒体资源](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/photoaccesshelper-savebutton)。

说明

仅应用需要克隆、备份或同步用户公共目录的图片、视频类文件时，可申请ohos.permission.READ_IMAGEVIDEO、ohos.permission.WRITE_IMAGEVIDEO权限来读写音频文件，申请方式请参考[申请受控权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions-in-acl)，通过AGC审核后才能使用。为避免应用的上架申请被驳回，开发者应优先使用Picker/控件等替代方案，仅少量符合[特殊场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/restricted-permissions#ohospermissionread_imagevideo)的应用被允许申请受限权限。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-overview "Camera Kit简介")
# 相机管理(ArkTS)

更新时间: 2025-12-16 16:35

在开发一个相机应用前，需要先通过调用相机接口来创建一个独立的相机设备。

## 开发步骤

详细的API说明请参考[Camera API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera)。

1. 导入camera接口，接口中提供了相机相关的属性和方法，导入方法如下。
    
    1. import { camera } from '@kit.CameraKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    3. import { common } from '@kit.AbilityKit';
    
2. 通过[getCameraManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-f#cameragetcameramanager)方法，获取cameraManager对象。
    
    Context获取方式请参考：[获取UIAbility的上下文信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uiability-usage#%E8%8E%B7%E5%8F%96uiability%E7%9A%84%E4%B8%8A%E4%B8%8B%E6%96%87%E4%BF%A1%E6%81%AF)。
    
    1. function getCameraManager(context: common.BaseContext): camera.CameraManager | undefined {
    2.   let cameraManager: camera.CameraManager;
    3.   try {
    4.     cameraManager = camera.getCameraManager(context);
    5.   } catch (error) {
    6.     let err = error as BusinessError;
    7.     console.error(`getCameraManager error, errCode: ${err.code}`);
    8.     return undefined;
    9.   }
    10.   return cameraManager;
    11. }
    
    说明
    
    如果获取对象失败，说明相机可能被占用或无法使用。如果被占用，须等到相机被释放后才能重新获取。
    
3. 通过[CameraManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager)中的[getSupportedCameras](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#getsupportedcameras)方法，获取当前设备支持的相机列表，列表中存储了设备支持的所有相机ID。若列表不为空，则说明列表中的每个ID都支持独立创建相机对象；否则，说明当前设备无可用相机，不可继续后续操作。
    
    1. function getCameraDevices(cameraManager: camera.CameraManager): Array<camera.CameraDevice> {
    2.   let cameraArray: Array<camera.CameraDevice> = cameraManager.getSupportedCameras();
    3.   if (cameraArray != undefined && cameraArray.length > 0) {
    4.     for (let index = 0; index < cameraArray.length; index++) {
    5.       console.info('cameraId : ' + cameraArray[index].cameraId);  // 获取相机ID。
    6.       console.info('cameraPosition : ' + cameraArray[index].cameraPosition);  // 获取相机位置。
    7.       console.info('cameraType : ' + cameraArray[index].cameraType);  // 获取相机类型。
    8.       console.info('connectionType : ' + cameraArray[index].connectionType);  // 获取相机连接类型。
    9.     }
    10.     return cameraArray;
    11.   } else {
    12.     console.error("cameraManager.getSupportedCameras error");
    13.     return [];
    14.   }
    15. }
    

## 状态监听

在相机应用开发过程中，可以随时监听相机状态，包括新相机的出现、相机的移除、相机的可用状态。在回调函数中，通过相机ID、相机状态这两个参数进行监听，如当有新相机出现时，可以将新相机加入到应用的备用相机中。

通过注册cameraStatus事件，通过回调返回监听结果，callback返回CameraStatusInfo参数，参数的具体内容可参考相机管理器回调接口实例[CameraStatusInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#camerastatusinfo)。

1. function onCameraStatusChange(cameraManager: camera.CameraManager): void {
2.   cameraManager.on('cameraStatus', (err: BusinessError, cameraStatusInfo: camera.CameraStatusInfo) => {
3.     if (err !== undefined && err.code !== 0) {
4.       console.error(`Callback Error, errorCode: ${err.code}`);
5.       return;
6.     }
7.     // 如果当通过USB连接相机设备时，回调函数会返回新的相机出现状态。
8.     if (cameraStatusInfo.status == camera.CameraStatus.CAMERA_STATUS_APPEAR) {
9.       console.info(`New Camera device appear.`);
10.     }
11.     // 如果当断开相机设备USB连接时，回调函数会返回相机被移除状态。
12.     if (cameraStatusInfo.status == camera.CameraStatus.CAMERA_STATUS_DISAPPEAR) {
13.       console.info(`Camera device has been removed.`);
14.     }
15.     // 相机被关闭时，回调函数会返回相机可用状态。
16.     if (cameraStatusInfo.status == camera.CameraStatus.CAMERA_STATUS_AVAILABLE) {
17.       console.info(`Current Camera is available.`);
18.     }
19.     // 相机被打开/占用时，回调函数会返回相机不可用状态。
20.     if (cameraStatusInfo.status == camera.CameraStatus.CAMERA_STATUS_UNAVAILABLE) {
21.       console.info(`Current Camera has been occupied.`);
22.     }
23.     console.info(`camera: ${cameraStatusInfo.camera.cameraId}`);
24.     console.info(`status: ${cameraStatusInfo.status}`);
25.   });
26. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-dev-arkts-mandatory "开发相机应用必选能力(ArkTS)")
# 设备输入(ArkTS)

更新时间: 2025-12-16 16:35

在开发相机应用时，需要先[申请相关权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-preparation)。

相机应用可通过调用和控制相机设备，完成预览、拍照和录像等基础操作。

## 开发步骤

详细的API说明请参考[Camera API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera)。

1. 导入camera接口，接口中提供了相机相关的属性和方法，导入方法如下。
    
    1. import { camera } from '@kit.CameraKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
    说明
    
    在相机设备输入之前需要先完成相机管理，详细开发步骤请参考[相机管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-device-management)。
    
2. 通过[cameraManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager)中的[createCameraInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#createcamerainput)方法创建相机输入流。
    
    1. async function createInput(cameraDevice: camera.CameraDevice, cameraManager: camera.CameraManager): Promise<camera.CameraInput | undefined> {
    2.   // 创建相机输入流。
    3.   let cameraInput: camera.CameraInput | undefined = undefined;
    4.   try {
    5.     cameraInput = cameraManager.createCameraInput(cameraDevice);
    6.   } catch (error) {
    7.     let err = error as BusinessError;
    8.     console.error('Failed to createCameraInput errorCode = ' + err.code);
    9.   }
    10.   if (cameraInput === undefined) {
    11.     return undefined;
    12.   }
    13.   // 监听cameraInput错误信息。
    14.   cameraInput.on('error', cameraDevice, (error: BusinessError) => {
    15.     console.error(`Camera input error code: ${error.code}`);
    16.   });
    17.   // 打开相机。
    18.   await cameraInput.open();
    19.   return cameraInput;
    20. }
    
3. 通过[getSupportedSceneModes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#getsupportedscenemodes11)方法，获取当前相机设备支持的模式列表，列表中存储了相机设备支持的所有模式[SceneMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#scenemode11)。
    
    1. function getSupportedSceneMode(cameraDevice: camera.CameraDevice, cameraManager: camera.CameraManager): Array<camera.SceneMode> {
    2.   // 获取相机设备支持的模式列表。
    3.   let sceneModeArray: Array<camera.SceneMode> = cameraManager.getSupportedSceneModes(cameraDevice);
    4.   if (sceneModeArray != undefined && sceneModeArray.length > 0) {
    5.     for (let index = 0; index < sceneModeArray.length; index++) {
    6.       console.info('Camera SceneMode : ' + sceneModeArray[index]);
    7.   }
    8.     return sceneModeArray;
    9.   } else {
    10.       console.error("cameraManager.getSupportedSceneModes error");
    11.       return [];
    12.   }
    13. }
    
4. 通过[getSupportedOutputCapability](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#getsupportedoutputcapability11)方法，获取当前相机设备支持的所有输出流，如预览流、拍照流、录像流等。输出流在[CameraOutputCapability](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#cameraoutputcapability)中的各个profile字段中，根据相机设备指定模式[SceneMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#scenemode11)的不同，需要添加不同类型的输出流。
    
    1. async function getSupportedOutputCapability(cameraDevice: camera.CameraDevice, cameraManager: camera.CameraManager, sceneMode: camera.SceneMode): Promise<camera.CameraOutputCapability | undefined> {
    2.    // 获取相机设备支持的输出流能力。
    3.    let cameraOutputCapability: camera.CameraOutputCapability = cameraManager.getSupportedOutputCapability(cameraDevice, sceneMode);
    4.    if (!cameraOutputCapability) {
    5.      console.error("cameraManager.getSupportedOutputCapability error");
    6.      return undefined;
    7.    }
    8.    console.info("outputCapability: " + JSON.stringify(cameraOutputCapability));
    9.    // 以NORMAL_PHOTO模式为例，需要添加预览流、拍照流。
    10.    // previewProfiles属性为获取当前设备支持的预览输出流。
    11.    let previewProfilesArray: Array<camera.Profile> = cameraOutputCapability.previewProfiles;
    12.    if (!previewProfilesArray) {
    13.      console.error("createOutput previewProfilesArray == null || undefined");
    14.    }
    15.    //photoProfiles属性为获取当前设备支持的拍照输出流。
    16.    let photoProfilesArray: Array<camera.Profile> = cameraOutputCapability.photoProfiles;
    17.    if (!photoProfilesArray) {
    18.      console.error("createOutput photoProfilesArray == null || undefined");
    19.    }
    20.    return cameraOutputCapability;
    21. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-device-management "相机管理(ArkTS)")
# 会话管理(ArkTS)

更新时间: 2025-12-16 16:35

相机使用预览、拍照、录像、元数据功能前，均需要创建相机会话。

在会话中，可以完成以下功能：

- 配置相机的输入流和输出流。相机在拍摄前，必须完成输入输出流的配置。
    
    配置输入流即添加设备输入，对用户而言，相当于选择设备的某一相机拍摄；配置输出流，即选择数据将以什么形式输出。当应用需要实现拍照时，输出流应配置为预览流和拍照流，预览流的数据将显示在XComponent组件上，拍照流的数据将通过ImageReceiver接口的能力保存到相册中。
    
- 添加闪光灯、调整焦距等配置。具体支持的配置及接口说明请参考[Camera API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera)。
    
- 会话切换控制。应用可以通过移除和添加输出流的方式，切换相机模式。如当前会话的输出流为拍照流，应用可以将拍照流移除，然后添加视频流作为输出流，即完成了拍照到录像的切换。
    

完成会话配置后，应用提交和开启会话，可以开始调用相机相关功能。

## 开发步骤

1. 导入相关接口，导入方法如下。
    
    1. import { camera } from '@kit.CameraKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 调用cameraManager中的[createSession](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#createsession11)方法创建一个会话。
    
    1. // 此处以videoSession为例。
    2. function getSession(cameraManager: camera.CameraManager): camera.VideoSession | undefined {
    3.   let videoSession: camera.VideoSession | undefined = undefined;
    4.   try {
    5.     videoSession = cameraManager.createSession(camera.SceneMode.NORMAL_VIDEO) as camera.VideoSession;
    6.   } catch (error) {
    7.     let err = error as BusinessError;
    8.     console.error(`Failed to create the session instance. error: ${err.code}`);
    9.   }
    10.   return videoSession;
    11. }
    
3. 调用VideoSession中的[beginConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#beginconfig11)方法配置会话。
    
    1. function beginConfig(videoSession: camera.VideoSession): void {
    2.   try {
    3.     videoSession.beginConfig();
    4.   } catch (error) {
    5.     let err = error as BusinessError;
    6.     console.error(`Failed to beginConfig. error: ${err.code}`);
    7.   }
    8. }
    
4. 使能。向会话中添加相机的输入流和输出流，调用[addInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#addinput11)添加相机的输入流；调用[addOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#addoutput11)添加相机的输出流。以下示例代码以添加预览流previewOutput和拍照流photoOutput为例，即当前模式支持拍照和预览。
    
    调用VideoSession中的[commitConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#commitconfig11)和[start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#start11)方法提交相关配置，并启动会话。
    
    说明
    
    在调用[addOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#addoutput11)添加相机的输出流前，可通过[canAddOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#canaddoutput11)判断当前相机输出流是否可以添加到session中。
    
    相机输入流cameraInput创建流程请参考[设备输入](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-device-input)，相机预览输出流previewOutput和拍照输出流photoOutput创建流程请分别参考[预览](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-preview)和[拍照](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-shooting)。
    
    1. async function startSession(videoSession: camera.VideoSession, cameraInput: camera.CameraInput, previewOutput: camera.PreviewOutput, photoOutput: camera.PhotoOutput): Promise<void> {
    2.   try {
    3.     videoSession.addInput(cameraInput);
    4.   } catch (error) {
    5.     let err = error as BusinessError;
    6.     console.error(`Failed to addInput. error: ${err.code}`);
    7.   }
    8.   let canAddPreviewOutput : boolean = false;
    9.   try {
    10.     canAddPreviewOutput = videoSession.canAddOutput(previewOutput);
    11.   } catch (error) {
    12.     let err = error as BusinessError;
    13.     console.error(`Failed to add previewOutput. error: ${err.code}`);
    14.   }
    15.   if (!canAddPreviewOutput) {
    16.     console.error(`Failed to add preview output.`);
    17.     return;
    18.   }
    19.   try {
    20.     videoSession.addOutput(previewOutput);
    21.   } catch (error) {
    22.     let err = error as BusinessError;
    23.     console.error(`Failed to add previewOutput. error: ${err.code}`);
    24.   }
    25.   let canAddPhotoOutput : boolean = false
    26.   try {
    27.     canAddPhotoOutput = videoSession.canAddOutput(photoOutput);
    28.   } catch (error) {
    29.     let err = error as BusinessError;
    30.     console.error(`Failed to add photoOutput error: ${err.code}`);
    31.   }
    32.   if (!canAddPhotoOutput) {
    33.     console.error(`Failed to add photo output.`);
    34.     return;
    35.   }
    36.   try {
    37.     videoSession.addOutput(photoOutput);
    38.   } catch (error) {
    39.     let err = error as BusinessError;
    40.     console.error(`Failed to add photoOutput. error: ${err.code}`);
    41.   }
    42.   try {
    43.     await videoSession.commitConfig();
    44.   } catch (error) {
    45.     let err = error as BusinessError;
    46.     console.error(`Failed to commitConfig. error: ${err.code}`);
    47.    return;
    48.   }
    
    49.   try {
    50.     await videoSession.start();
    51.   } catch (error) {
    52.     let err = error as BusinessError;
    53.     console.error(`Failed to start. error: ${err.code}`);
    54.   }
    55. }
    
5. 会话控制。调用VideoSession中的[stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#stop11)方法可以停止当前会话。调用[removeOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#removeoutput11)和[addOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#addoutput11)方法可以完成会话切换控制。以下示例代码以移除拍照流photoOutput，添加视频流videoOutput为例，完成了拍照到录像的切换。
    
    1. async function switchOutput(videoSession: camera.VideoSession, videoOutput: camera.VideoOutput, photoOutput: camera.PhotoOutput): Promise<void> {
    2.   try {
    3.     await videoSession.stop();
    4.   } catch (error) {
    5.     let err = error as BusinessError;
    6.     console.error(`Failed to stop. error: ${err.code}`);
    7.   }
    
    8.   try {
    9.     videoSession.beginConfig();
    10.   } catch (error) {
    11.     let err = error as BusinessError;
    12.     console.error(`Failed to beginConfig. error: ${err.code}`);
    13.   }
    14.   // 从会话中移除拍照输出流。
    15.   try {
    16.     videoSession.removeOutput(photoOutput);
    17.   } catch (error) {
    18.     let err = error as BusinessError;
    19.     console.error(`Failed to remove photoOutput. error: ${err.code}`);
    20.   }
    21.   try {
    22.     videoSession.canAddOutput(videoOutput);
    23.   } catch (error) {
    24.     let err = error as BusinessError;
    25.     console.error(`Failed to add videoOutput error: ${err.code}`);
    26.   }
    27.   // 向会话中添加视频输出流。
    28.   try {
    29.     videoSession.addOutput(videoOutput);
    30.   } catch (error) {
    31.     let err = error as BusinessError;
    32.     console.error(`Failed to add videoOutput. error: ${err.code}`);
    33.   }
    34.   try {
    35.     await videoSession.commitConfig();
    36.   } catch (error) {
    37.     let err = error as BusinessError;
    38.     console.error(`Failed to commitConfig. error: ${err.code}`);
    39.   }
    
    40.   try {
    41.     await videoSession.start();
    42.   } catch (error) {
    43.     let err = error as BusinessError;
    44.     console.error(`Failed to start. error: ${err.code}`);
    45.   }
    46. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-device-input "设备输入(ArkTS)")
# 通过系统相机拍照和录像(CameraPicker)

更新时间: 2025-12-16 16:35

应用可调用CameraPicker拍摄照片或录制视频，无需申请相机权限。

CameraPicker的相机交互界面由系统提供，在用户点击拍摄和确认按钮后，调用CameraPicker的应用获取对应的照片或者视频。

应用开发者如果只是需要获取即时拍摄的照片或者视频，则可以使用CameraPicker能力来轻松实现。

由于照片的拍摄和确认都是由用户进行主动确认，因此应用开发者可以不用申请操作相机的相关权限。

## 开发步骤

详细的API说明请参考[CameraPicker API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-camerapicker)。

1. 导入相关接口，导入方法如下。
    
    1. import { camera, cameraPicker as picker } from '@kit.CameraKit';
    2. import { fileIo, fileUri } from '@kit.CoreFileKit';
    
2. 配置[PickerProfile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-camerapicker#pickerprofile)。
    
    说明
    
    PickerProfile的saveUri为可选参数，如果未配置该项，拍摄的照片和视频默认存入媒体库中。
    
    如果不想将照片和视频存入媒体库，请自行配置应用沙箱内的文件路径。
    
    应用沙箱内的这个文件必须是一个存在的、可写的文件。这个文件的uri传入picker接口之后，相当于应用给系统相机授权该文件的读写权限。系统相机在拍摄结束之后，会对此文件进行覆盖写入。
    
    1. import { BusinessError } from '@kit.BasicServicesKit';
    
    2. function createPickerProfile(context: Context): picker.PickerProfile {
    3.   let pathDir = context.filesDir;
    4.   let fileName = `${new Date().getTime()}`;
    5.   let filePath = pathDir + `/${fileName}.tmp`;
    6.   try {
    7.     fileIo.createRandomAccessFileSync(filePath, fileIo.OpenMode.CREATE);
    8.   } catch (error) {
    9.     let err = error as BusinessError;
    10.     console.error(`create picker profile failed. error code: ${err.code}`);
    11.   }
    
    12.   let uri = fileUri.getUriFromPath(filePath);
    13.   let pickerProfile: picker.PickerProfile = {
    14.     cameraPosition: camera.CameraPosition.CAMERA_POSITION_BACK,
    15.     saveUri: uri
    16.   };
    17.   return pickerProfile;
    18. }
    
    fileIo接口调用方法请参考：[createRandomAccessFileSync](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs#fscreaterandomaccessfilesync10)和[getUriFromPath](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fileuri#fileurigeturifrompath)。
    
3. 调用picker拍摄接口获取拍摄的结果。
    
    1. async function getPickerResult(context: Context, pickerProfile: picker.PickerProfile): Promise<picker.PickerResult> {
    2.   let result: picker.PickerResult =
    3.     // 调用picker方法拉起系统相机，获取拍摄的图片或视频。
    4.     await picker.pick(context, [picker.PickerMediaType.PHOTO, picker.PickerMediaType.VIDEO],
    5.       pickerProfile);
    6.   console.info(`picker resultCode: ${result.resultCode},resultUri: ${result.resultUri},mediaType: ${result.mediaType}`);
    7.   return result;
    8. }
    

## 完整示例

1. import { camera, cameraPicker as picker } from '@kit.CameraKit';
2. import { fileIo, fileUri } from '@kit.CoreFileKit';

3. @Entry
4. @Component
5. struct Index {
6.   @State imgSrc: string = '';
7.   @State videoSrc: string = '';
8.   createPickerProfile(context: Context): picker.PickerProfile {
9.     let pathDir = context.filesDir;
10.     let fileName = `${new Date().getTime()}`;
11.     let filePath = pathDir + `/${fileName}.tmp`;
12.     fileIo.createRandomAccessFileSync(filePath, fileIo.OpenMode.CREATE);

13.     let uri = fileUri.getUriFromPath(filePath);
14.     let pickerProfile: picker.PickerProfile = {
15.       cameraPosition: camera.CameraPosition.CAMERA_POSITION_BACK,
16.       saveUri: uri
17.     };
18.     return pickerProfile;
19.   }

20.   async getPickerResult(context: Context, pickerProfile: picker.PickerProfile): Promise<picker.PickerResult> {
21.     let result: picker.PickerResult =
22.       await picker.pick(context, [picker.PickerMediaType.PHOTO, picker.PickerMediaType.VIDEO],
23.         pickerProfile);
24.     console.info(`picker resultCode: ${result.resultCode},resultUri: ${result.resultUri},mediaType: ${result.mediaType}`);
25.     return result;
26.   }

27.   getContext(): Context | undefined {
28.     let uiContext: UIContext = this.getUIContext();
29.     let context: Context | undefined = uiContext.getHostContext();
30.     return context;
31.   }

32.   build() {
33.     RelativeContainer() {
34.       Column() {
35.         Image(this.imgSrc).width(200).height(200).backgroundColor(Color.Black).margin(5);
36.         Video({ src: this.videoSrc}).width(200).height(200).autoPlay(true);
37.         Button("Test Picker Photo&Video").fontSize(20)
38.           .fontWeight(FontWeight.Bold)
39.           .onClick(async () => {
40.             let context = this.getContext();
41.             if (context === undefined) {
42.               return;
43.             }
44.             let pickerProfile = this.createPickerProfile(context);
45.             let result = await this.getPickerResult(context, pickerProfile);
46.             if (result.resultCode == 0) {
47.               if (result.mediaType === picker.PickerMediaType.PHOTO) {
48.                 this.imgSrc = result.resultUri;
49.               } else {
50.                 this.videoSrc = result.resultUri;
51.               }
52.             }
53.           }).margin(5);

54.       }.alignRules({
55.         center: { anchor: '__container__', align: VerticalAlign.Center },
56.         middle: { anchor: '__container__', align: HorizontalAlign.Center }
57.       });
58.     }
59.     .height('100%')
60.     .width('100%')
61.   }
62. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-dev-arkts "开发相机应用基础能力(ArkTS)")
# 预览(ArkTS)

更新时间: 2025-12-16 16:35

在开发相机应用时，需要先[申请相关权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-preparation)。

预览是启动相机后看见的画面，通常在拍照和录像前执行。

## 开发步骤

详细的API说明请参考[Camera API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera)。

1. 导入camera接口，接口中提供了相机相关的属性和方法，导入方法如下。
    
    1. import { camera } from '@kit.CameraKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 创建Surface。
    
    相机开发模型为Surface模型，该模型主要通过Surface实现数据交互。在开发相机应用界面时，首先需要通过创建XComponent组件为预览流提供Surface，再通过获取XComponent组件对应Surface的ID创建预览流，预览流画面即可直接在XComponent组件内渲染，详细获取surfaceId请参考[getXComponentSurfaceId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent#getxcomponentsurfaceid9)方法。而XComponent的能力由UI提供，相关介绍可参考[XComponent组件参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent)。
    
    说明
    
    预览流与录像输出流的分辨率的宽高比要保持一致，如果设置XComponent组件中的Surface显示区域宽高比为1920:1080 = 16:9，则需要预览流中的分辨率的宽高比也为16:9，如分辨率选择640:360，或960:540，或1920:1080，以此类推。
    
    1. @Entry
    2. @Component
    3. struct example {
    4.   xComponentCtl: XComponentController = new XComponentController();
    5.   surfaceId:string = '';
    6.   imageWidth: number = 1920;
    7.   imageHeight: number = 1080;
    8.   private uiContext: UIContext = this.getUIContext();
    
    9.   build() {
    10.     XComponent({
    11.       id: 'componentId',
    12.       type: XComponentType.SURFACE,
    13.       controller: this.xComponentCtl
    14.     })
    15.       .onLoad(async () => {
    16.         console.info('onLoad is called');
    17.         this.surfaceId = this.xComponentCtl.getXComponentSurfaceId(); // 获取组件surfaceId。
    18.         // 使用surfaceId创建预览流，开启相机，组件实时渲染每帧预览流数据。
    19.       })
    20.       // surface的宽、高设置与XComponent组件的宽、高设置相反，或使用.renderFit(RenderFit.RESIZE_CONTAIN)自动填充显示无需设置宽、高。
    21.       .width(this.uiContext.px2vp(this.imageHeight))
    22.       .height(this.uiContext.px2vp(this.imageWidth))
    23.   }
    24. }
    
3. 通过[CameraOutputCapability](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#cameraoutputcapability)中的previewProfiles属性获取当前设备支持的预览能力，返回previewProfilesArray数组 。通过[createPreviewOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#createpreviewoutput)方法创建预览输出流，其中，[createPreviewOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#createpreviewoutput)方法中的两个参数分别是当前设备支持的预览配置信息previewProfile和步骤二中获取的surfaceId。
    
    1. function getPreviewOutput(cameraManager: camera.CameraManager, cameraOutputCapability: camera.CameraOutputCapability, surfaceId: string): camera.PreviewOutput | undefined {
    2.   if (!cameraOutputCapability || !cameraOutputCapability.previewProfiles) {
    3.     return;
    4.   }
    5.   let previewProfilesArray: Array<camera.Profile> = cameraOutputCapability.previewProfiles;
    6.   if (!previewProfilesArray || previewProfilesArray.length === 0) {
    7.     console.error("previewProfilesArray is null or []");
    8.     return;
    9.   }
    10.   let previewOutput: camera.PreviewOutput | undefined = undefined;
    11.   try {
    12.     //previewProfilesArray要选择与步骤二设置宽高比一致的previewProfile配置信息，此处选择数组第一项仅供接口使用示例参考。
    13.     previewOutput = cameraManager.createPreviewOutput(previewProfilesArray[0], surfaceId);
    14.   } catch (error) {
    15.     let err = error as BusinessError;
    16.     console.error("Failed to create the PreviewOutput instance. error code: " + err.code);
    17.   }
    18.   return previewOutput;
    19. }
    
4. 使能。通过[Session.start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#start11)方法输出预览流，接口调用失败会返回相应错误码，错误码类型参见[Camera错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraerrorcode)。
    
    1. async function startPreviewOutput(cameraManager: camera.CameraManager, previewOutput: camera.PreviewOutput): Promise<void> {
    2.   try {
    3.     let cameraArray: Array<camera.CameraDevice> = [];
    4.     cameraArray = cameraManager.getSupportedCameras();
    5.     if (cameraArray.length == 0) {
    6.       console.error('no camera.');
    7.       return;
    8.     }
    9.     // 获取支持的模式类型。
    10.     let sceneModes: Array<camera.SceneMode> = cameraManager.getSupportedSceneModes(cameraArray[0]);
    11.     let isSupportPhotoMode: boolean = sceneModes.indexOf(camera.SceneMode.NORMAL_PHOTO) >= 0;
    12.     if (!isSupportPhotoMode) {
    13.       console.error('photo mode not support');
    14.       return;
    15.     }
    16.     let cameraInput: camera.CameraInput | undefined;
    17.     cameraInput = cameraManager.createCameraInput(cameraArray[0]);
    18.     if (cameraInput === undefined) {
    19.       console.error('cameraInput is undefined');
    20.       return;
    21.     }
    22.     // 打开相机。
    23.     await cameraInput.open();
    24.     let session = cameraManager.createSession(camera.SceneMode.NORMAL_PHOTO);
    25.     if (!session) {
    26.       console.error('session is null');
    27.       return;
    28.     }
    29.     let photoSession: camera.PhotoSession = session as camera.PhotoSession;
    30.     photoSession.beginConfig();
    31.     photoSession.addInput(cameraInput);
    32.     photoSession.addOutput(previewOutput);
    33.     await photoSession.commitConfig();
    34.     await photoSession.start();
    35.   } catch (error) {
    36.     console.error(`startPreviewOutput call failed, error: ${error}`);
    37.   }
    38. }
    

## 状态监听

在相机应用开发过程中，可以随时监听预览输出流状态，包括预览流启动、预览流结束、预览流输出错误。

- 通过注册固定的frameStart回调函数获取监听预览启动结果，previewOutput创建成功时即可监听，预览第一次曝光时触发，有该事件返回结果则认为预览流已启动。
    
    1. function onPreviewOutputFrameStart(previewOutput: camera.PreviewOutput): void {
    2.   previewOutput.on('frameStart', (err: BusinessError) => {
    3.     if (err !== undefined && err.code !== 0) {
    4.       return;
    5.     }
    6.     console.info('Preview frame started');
    7.   });
    8. }
    
- 通过注册固定的frameEnd回调函数获取监听预览结束结果，previewOutput创建成功时即可监听，预览完成最后一帧时触发，有该事件返回结果则认为预览流已结束。
    
    1. function onPreviewOutputFrameEnd(previewOutput: camera.PreviewOutput): void {
    2.   previewOutput.on('frameEnd', (err: BusinessError) => {
    3.     if (err !== undefined && err.code !== 0) {
    4.       return;
    5.     }
    6.     console.info('Preview frame ended');
    7.   });
    8. }
    
- 通过注册固定的error回调函数获取监听预览输出错误结果，回调返回预览输出接口使用错误时对应的错误码，错误码类型参见[Camera错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraerrorcode)。
    
    1. function onPreviewOutputError(previewOutput: camera.PreviewOutput): void {
    2.   previewOutput.on('error', (previewOutputError: BusinessError) => {
    3.     console.error(`Preview output error code: ${previewOutputError.code}`);
    4.   });
    5. }
    

## 完整示例

1. import { camera } from '@kit.CameraKit';
2. import { BusinessError } from '@kit.BasicServicesKit';
3. import { abilityAccessCtrl, Permissions } from '@kit.AbilityKit';

4. @Entry
5. @Component
6. struct Index {
7.   private xComponentCtl: XComponentController = new XComponentController();
8.   private xComponentSurfaceId: string = '';
9.   @State imageWidth: number = 1920;
10.   @State imageHeight: number = 1080;
11.   private cameraManager: camera.CameraManager | undefined = undefined;
12.   private cameras: Array<camera.CameraDevice> | Array<camera.CameraDevice> = [];
13.   private cameraInput: camera.CameraInput | undefined = undefined;
14.   private previewOutput: camera.PreviewOutput | undefined = undefined;
15.   private session: camera.VideoSession | undefined = undefined;
16.   private uiContext: UIContext = this.getUIContext();
17.   private context: Context | undefined = this.uiContext.getHostContext();
18.   private cameraPermission: Permissions = 'ohos.permission.CAMERA'; // 申请权限相关问题可参考本篇开头的申请相关权限文档
19.   @State isShow: boolean = false;

20.   async requestPermissionsFn(): Promise<void> {
21.     let atManager = abilityAccessCtrl.createAtManager();
22.     if (this.context) {
23.       let res = await atManager.requestPermissionsFromUser(this.context, [this.cameraPermission]);
24.       for (let i = 0; i < res.permissions.length; i++) {
25.         if (this.cameraPermission.toString() === res.permissions[i] && res.authResults[i] === 0) {
26.           this.isShow = true;
27.         }
28.       }
29.     }
30.   }

31.   aboutToAppear(): void {
32.     this.requestPermissionsFn();
33.   }

34.   onPageShow(): void {
35.     console.info('onPageShow');
36.     if (this.xComponentSurfaceId !== '') {
37.       this.initCamera();
38.     }
39.   }

40.   onPageHide(): void {
41.     console.info('onPageHide');
42.     this.releaseCamera();
43.   }

44.   build() {
45.     Column() {
46.       if (this.isShow) {
47.         XComponent({
48.           id: 'componentId',
49.           type: XComponentType.SURFACE,
50.           controller: this.xComponentCtl
51.         })
52.           .onLoad(async () => {
53.             console.info('onLoad is called');
54.             this.xComponentSurfaceId = this.xComponentCtl.getXComponentSurfaceId(); // 获取组件surfaceId。
55.             // 初始化相机，组件实时渲染每帧预览流数据。
56.             this.initCamera()
57.           })
58.           .width(this.uiContext.px2vp(this.imageHeight))
59.           .height(this.uiContext.px2vp(this.imageWidth))
60.       }
61.     }
62.     .justifyContent(FlexAlign.Center)
63.     .height('100%')
64.     .width('100%')
65.   }

66.   // 初始化相机。
67.   async initCamera(): Promise<void> {
68.     console.info(`initCamera previewOutput xComponentSurfaceId:${this.xComponentSurfaceId}`);
69.     try {
70.       // 获取相机管理器实例。
71.       this.cameraManager = camera.getCameraManager(this.context);
72.       if (!this.cameraManager) {
73.         console.error('initCamera getCameraManager');
74.         return;
75.       }
76.       // 获取当前设备支持的相机device列表。
77.       this.cameras = this.cameraManager.getSupportedCameras();
78.       if (!this.cameras) {
79.         console.error('initCamera getSupportedCameras');
80.       }
81.       // 选择一个相机device，创建cameraInput输出对象。
82.       this.cameraInput = this.cameraManager.createCameraInput(this.cameras[0]);
83.       if (!this.cameraInput) {
84.         console.error('initCamera createCameraInput');
85.         return;
86.       }
87.       // 打开相机。
88.       await this.cameraInput.open();
89.       // 获取相机device支持的profile。
90.       let capability: camera.CameraOutputCapability =
91.         this.cameraManager.getSupportedOutputCapability(this.cameras[0], camera.SceneMode.NORMAL_VIDEO);
92.       if (!capability || capability.previewProfiles.length === 0) {
93.         console.error('capability is null || []');
94.         this.releaseCamera();
95.         return;
96.       }
97.       let minRatioDiff : number = 0.1;
98.       let surfaceRatio : number = this.imageWidth / this.imageHeight; // 最接近16:9宽高比。
99.       let previewProfile: camera.Profile = capability.previewProfiles[0];
100.       // 应用开发者根据实际业务需求选择一个支持的预览流previewProfile。
101.       // 此处以选择CAMERA_FORMAT_YUV_420_SP（NV21）格式、满足限定条件分辨率的预览流previewProfile为例。
102.       for (let index = 0; index < capability.previewProfiles.length; index++) {
103.         const tempProfile = capability.previewProfiles[index];
104.         let tempRatio = tempProfile.size.width >= tempProfile.size.height ?
105.           tempProfile.size.width / tempProfile.size.height : tempProfile.size.height / tempProfile.size.width;
106.         let currentRatio = Math.abs(tempRatio - surfaceRatio);
107.         if (currentRatio <= minRatioDiff && tempProfile.format == camera.CameraFormat.CAMERA_FORMAT_YUV_420_SP) {
108.           previewProfile = tempProfile;
109.           break;
110.         }
111.       }
112.       this.imageWidth = previewProfile.size.width; // 更新xComponent组件的宽。
113.       this.imageHeight = previewProfile.size.height; // 更新xComponent组件的高。
114.       console.info(`initCamera imageWidth:${this.imageWidth} imageHeight:${this.imageHeight}`);

115.       // 使用xComponentSurfaceId创建预览。
116.       this.previewOutput = this.cameraManager.createPreviewOutput(previewProfile, this.xComponentSurfaceId);
117.       if (!this.previewOutput) {
118.         console.error('initCamera createPreviewOutput');
119.         this.releaseCamera();
120.         return;
121.       }
122.       // 创建录像模式相机会话。
123.       let session = this.cameraManager.createSession(camera.SceneMode.NORMAL_VIDEO);
124.       if (!session) {
125.         console.error('session is null');
126.         this.releaseCamera();
127.         return;
128.       }
129.       this.session = session as camera.VideoSession;
130.       // 开始配置会话。
131.       this.session.beginConfig();
132.       // 添加相机设备输入。
133.       this.session.addInput(this.cameraInput);
134.       // 添加预览流输出。
135.       this.session.addOutput(this.previewOutput);
136.       // 提交会话配置。
137.       await this.session.commitConfig();
138.       // 开始启动已配置的输入输出流。
139.       await this.session.start();
140.     } catch (error) {
141.       console.error(`initCamera fail: ${JSON.stringify(error)}`);
142.       this.releaseCamera();
143.     }
144.   }

145.   // 释放相机。
146.   async releaseCamera(): Promise<void> {
147.     console.info('releaseCamera');
148.     // 停止当前会话。
149.     await this.session?.stop().catch((e: BusinessError) => {console.error('Failed to stop session: ', e)});
150.     // 释放相机输入流。
151.     await this.cameraInput?.close().catch((e: BusinessError) => {console.error('Failed to close the camera: ', e)});
152.     // 释放预览输出流。
153.     await this.previewOutput?.release().catch((e: BusinessError) => {console.error('Failed to stop the preview stream: ', e)});
154.     // 释放会话。
155.     await this.session?.release().catch((e: BusinessError) => {console.error('Failed to release session: ', e)});
156.   }
157. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-picker "通过系统相机拍照和录像(CameraPicker)")
# 双路预览(ArkTS)

更新时间: 2025-12-16 16:35

在开发相机应用时，需要先[申请相关权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-preparation)。

双路预览，即应用可同时使用两路预览流，一路用于在屏幕上显示，一路用于图像处理等其他操作，提升处理效率。

相机应用通过控制相机，实现图像显示（预览）、照片保存（拍照）、视频录制（录像）等基础操作。相机开发模型为Surface模型，即应用通过Surface进行数据传递，通过ImageReceiver的surface获取拍照流的数据、通过XComponent的surface获取预览流的数据。

如果要实现双路预览，即将拍照流改为预览流，将拍照流中的surface改为预览流的surface，通过ImageReceiver的surface创建previewOutput，其余流程与拍照流和预览流一致。

详细的API说明请参考[Camera API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera)。

## 约束与限制

- 暂不支持动态添加流，即不能在没有调用[session.stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#stop11)的情况下，调用[addOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#addoutput11)添加流。
- 对ImageReceiver组件获取到的图像数据处理后，需要将对应的图像Buffer释放，确保Surface的BufferQueue正常轮转。

## 调用流程

双路方案调用流程图建议如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163527.74658574462699001737860768233763:50001231000000:2800:A8BB014BCAFB745D9A38AF42650DF96ADCFE361EBBE68E1D483C2C132B6C7320.png)

## 开发步骤

- 用于处理图像的第一路预览流：创建ImageReceiver对象，获取SurfaceId创建第一路预览流，注册图像监听，按需处理预览流每帧图像。
- 用于显示画面的第二路预览流：创建XComponent组件，获取SurfaceId创建第二路预览流，预览流画面直接在组件内渲染。
- 创建预览流获取数据：创建上述两路预览流，配置进相机会话，启动会话后，两路预览流同时获取数据。

### 用于处理图像的第一路预览流

1. 导入依赖，本篇文档需要用到图片和相机框架等相关依赖包。
    
    1. import { image } from '@kit.ImageKit';
    2. import { camera } from '@kit.CameraKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 获取第一路预览流SurfaceId：创建ImageReceiver对象，通过ImageReceiver对象可获取其SurfaceId。
    
    1. let imageWidth: number = 1920; // 请使用设备支持profile的size的宽。
    2. let imageHeight: number = 1080; // 请使用设备支持profile的size的高。
    
    3. async function initImageReceiver():Promise<void>{
    4.   // 创建ImageReceiver对象。
    5.   let size: image.Size = { width: imageWidth, height: imageHeight };
    6.   let imageReceiver: image.ImageReceiver | undefined;
    7.   try {
    8.     imageReceiver = image.createImageReceiver(size, image.ImageFormat.JPEG, 8);
    9.   }  catch (error) {
    10.     let err = error as BusinessError;
    11.     console.error(`Init image receiver failed. error code: ${err.code}`);
    12.     return;
    13.   }
    14.   // 获取第一路流SurfaceId。
    15.   let imageReceiverSurfaceId = await imageReceiver.getReceivingSurfaceId();
    16.   console.info(`initImageReceiver imageReceiverSurfaceId:${imageReceiverSurfaceId}`);
    17. }
    
3. ImageReceiver接收预览流图像数据获取图像格式请参考[Image](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-image)中的format参数，[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)格式请参考[PixelMapFormat](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-e#pixelmapformat7)。
    
    1. // Image格式与PixelMap格式映射关系。
    2. let formatToPixelMapFormatMap = new Map<number, image.PixelMapFormat>([
    3.   [12, image.PixelMapFormat.RGBA_8888],
    4.   [25, image.PixelMapFormat.NV21],
    5.   [35, image.PixelMapFormat.YCBCR_P010],
    6.   [36, image.PixelMapFormat.YCRCB_P010]
    7. ]);
    8. // PixelMapFormat格式的单个像素点大小映射关系。
    9. let pixelMapFormatToSizeMap = new Map<image.PixelMapFormat, number>([
    10.   [image.PixelMapFormat.RGBA_8888, 4],
    11.   [image.PixelMapFormat.NV21, 1.5],
    12.   [image.PixelMapFormat.YCBCR_P010, 3],
    13.   [image.PixelMapFormat.YCRCB_P010, 3]
    14. ]);
    
4. 注册监听处理预览流每帧图像数据：通过ImageReceiver组件中imageArrival事件监听获取底层返回的图像数据，详细的API说明请参考[Image API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagereceiver)。
    
    说明
    
    - 在通过[createPixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-f#imagecreatepixelmap8)接口创建[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)实例时，设置的Size、srcPixelFormat等属性必须和相机预览输出流previewProfile中配置的Size、Format属性保持一致，ImageReceiver图片像素格式请参考[PixelMapFormat](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-e#pixelmapformat7)，相机预览输出流previewProfile输出格式请参考[CameraFormat](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraformat)。
    - 由于一多设备产品差异性，应用开发者在创建相机预览输出流前，必须先通过[getSupportedOutputCapability](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#getsupportedoutputcapability11)方法获取当前设备支持的预览输出流previewProfile，再根据实际业务需求选择[CameraFormat](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraformat)和[Size](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#size)适合的预览输出流previewProfile。
    - ImageReceiver接收预览流图像数据实际format格式由应用开发者在创建预览输出流相机预览输出流时，根据实际业务需求选择的previewProfile中format格式参数影响，详细步骤请参考[创建预览流获取数据](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-dual-channel-preview#%E5%88%9B%E5%BB%BA%E9%A2%84%E8%A7%88%E6%B5%81%E8%8E%B7%E5%8F%96%E6%95%B0%E6%8D%AE)。
    
    1. function onImageArrival(receiver: image.ImageReceiver): void {
    2.   // 注册imageArrival监听。
    3.   receiver.on('imageArrival', () => {
    4.     // 获取图像。
    5.     receiver.readNextImage((err: BusinessError, nextImage: image.Image) => {
    6.       if (err || nextImage === undefined) {
    7.         console.error('readNextImage failed');
    8.         return;
    9.       }
    10.       // 解析图像内容。
    11.       nextImage.getComponent(image.ComponentType.JPEG, async (err: BusinessError, imgComponent: image.Component) => {
    12.         if (err || imgComponent === undefined) {
    13.           console.error('getComponent failed');
    14.         }
    15.         if (imgComponent.byteBuffer) {
    16.           // 详情见下方解析图片buffer数据参考，本示例以方式一为例。
    17.           let width = nextImage.size.width; // 获取图片的宽。
    18.           let height = nextImage.size.height; // 获取图片的高。
    19.           let stride = imgComponent.rowStride; // 获取图片的stride。
    20.           let imageFormat = nextImage.format; // 获取图片的format。
    21.           let pixelMapFormat = formatToPixelMapFormatMap.get(imageFormat) ?? image.PixelMapFormat.NV21;
    22.           let mSize = pixelMapFormatToSizeMap.get(pixelMapFormat) ?? 1.5;
    23.           console.info(`getComponent with width:${width} height:${height} stride:${stride}`);
    24.           // 如需使用pixelMap，参考以下逻辑。
    25.           // pixelMap创建时使用的size、srcPixelFormat需要与相机预览输出流previewProfile中的size、format保持一致。
    26.           // stride与width一致。
    27.           let pixelMap : image.PixelMap;
    28.           if (stride == width) {
    29.             pixelMap = await image.createPixelMap(imgComponent.byteBuffer, {
    30.               size: { height: height, width: width },
    31.               srcPixelFormat: pixelMapFormat,
    32.             })
    33.           } else {
    34.             // stride与width不一致。
    35.             const dstBufferSize = width * height * mSize
    36.             const dstArr = new Uint8Array(dstBufferSize)
    37.             for (let j = 0; j < height * mSize; j++) {
    38.               const srcBuf = new Uint8Array(imgComponent.byteBuffer, j * stride, width)
    39.               dstArr.set(srcBuf, j * width)
    40.             }
    41.             pixelMap = await image.createPixelMap(dstArr.buffer, {
    42.               size: { height: height, width: width },
    43.               srcPixelFormat: pixelMapFormat,
    44.             })
    45.           }
    46.           // 确保当前pixelMap没有在使用的情况下，可进行资源释放。
    47.           if (pixelMap != undefined) {
    48.             await pixelMap.release().then(() => {
    49.               console.info('Succeeded in releasing pixelMap object.');
    50.             }).catch((error: BusinessError) => {
    51.               console.error(`Failed to release pixelMap object. code is ${error.code}, message is ${error.message}`);
    52.             })
    53.           }
    54.         } else {
    55.           console.error('byteBuffer is null');
    56.         }
    57.         // 确保当前buffer没有在使用的情况下，可进行资源释放。
    58.         // 如果对buffer进行异步操作，需要在异步操作结束后再释放该资源（nextImage.release()）。
    59.         nextImage.release();
    60.       })
    61.     })
    62.   })
    63. }
    
    通过 [image.Component](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-i#component9) 解析图片buffer数据参考：
    
    注意
    
    需要确认图像的宽width是否与行距rowStride一致，如果不一致可参考以下方式处理：
    
    方式一：去除imgComponent.byteBuffer中stride数据，拷贝得到新的buffer，调用不支持stride的接口处理buffer。
    
    64. // pixelMap创建时使用的size、srcPixelFormat需要与相机预览输出流previewProfile中的size、format保持一致.
    65. const dstBufferSize = width * height * mSize;
    66. const dstArr = new Uint8Array(dstBufferSize);
    67. // 逐行读取buffer数据。
    68. for (let j = 0; j < height * mSize; j++) {
    69.   // imgComponent.byteBuffer的每行数据拷贝前width个字节到dstArr中。
    70.   const srcBuf = new Uint8Array(imgComponent.byteBuffer, j * stride, width);
    71.   dstArr.set(srcBuf, j * width);
    72. }
    73. let pixelMap = await image.createPixelMap(dstArr.buffer, {
    74.   size: { height: height, width: width }, srcPixelFormat: pixelMapFormat
    
    75. });
    
    方式二：根据stride*height创建pixelMap，然后调用pixelMap的cropSync方法裁剪掉多余的像素。
    
    76. // 创建pixelMap，width宽传行距stride的值。
    77. let pixelMap = await image.createPixelMap(imgComponent.byteBuffer, {
    78.   size:{height: height, width: stride}, srcPixelFormat: pixelMapFormat});
    79. // 裁剪多余的像素。
    80. pixelMap.cropSync({size:{width:width, height:height}, x:0, y:0});
    
    方式三：将原始imgComponent.byteBuffer和stride信息一起传给支持stride的接口处理。
    

### 用于显示画面的第二路预览流

获取第二路预览流SurfaceId：创建XComponent组件用于预览流显示，获取surfaceId请参考XComponent组件提供的[getXComponentSurfaceId](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent#getxcomponentsurfaceid9)方法，而XComponent的能力由UI提供，相关介绍可参考[XComponent组件参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent)。

1. @Component
2. struct example {
3.   xComponentCtl: XComponentController = new XComponentController();
4.   surfaceId:string = '';
5.   imageWidth: number = 1920;
6.   imageHeight: number = 1080;
7.   private uiContext: UIContext = this.getUIContext();

8.   build() {
9.     XComponent({
10.       id: 'componentId',
11.       type: XComponentType.SURFACE,
12.       controller: this.xComponentCtl
13.     })
14.       .onLoad(async () => {
15.         console.info('onLoad is called');
16.         this.surfaceId = this.xComponentCtl.getXComponentSurfaceId(); // 获取组件surfaceId。
17.         // 使用surfaceId创建预览流，开启相机，组件实时渲染每帧预览流数据。
18.       })
19.       // surface的宽、高设置与XComponent组件的宽、高设置相反，或使用.renderFit(RenderFit.RESIZE_CONTAIN)自动填充显示无需设置宽、高。
20.       .width(this.uiContext.px2vp(this.imageHeight))
21.       .height(this.uiContext.px2vp(this.imageWidth))
22.   }
23. }

### 创建预览流获取数据

通过两个SurfaceId分别创建两路预览流输出，加入相机会话，启动相机会话，获取预览流数据。

1. function createDualPreviewOutput(cameraManager: camera.CameraManager, previewProfile: camera.Profile,
2.   session: camera.Session, imageReceiverSurfaceId: string, xComponentSurfaceId: string): void {
3.   try {
4.     // 使用imageReceiverSurfaceId创建第一路预览。
5.     let previewOutput1 = cameraManager.createPreviewOutput(previewProfile, imageReceiverSurfaceId);
6.     if (!previewOutput1) {
7.       console.error('createPreviewOutput1 error');
8.       return;
9.     }
10.     // 使用xComponentSurfaceId创建第二路预览。
11.     let previewOutput2 = cameraManager.createPreviewOutput(previewProfile, xComponentSurfaceId);
12.     if (!previewOutput2) {
13.       console.error('createPreviewOutput2 error');
14.       return;
15.     }
16.     // 添加第一路预览流输出。
17.     session.addOutput(previewOutput1);
18.     // 添加第二路预览流输出。
19.     session.addOutput(previewOutput2);
20.   } catch (error) {
21.     console.error('createDualPreviewOutput  call failed');
22.   }
23. }

## 完整示例

1. import { camera } from '@kit.CameraKit';
2. import { image } from '@kit.ImageKit';
3. import { BusinessError } from '@kit.BasicServicesKit';
4. import { abilityAccessCtrl, Permissions } from '@kit.AbilityKit';

5. interface CameraResources {
6.   videoOutput?: camera.VideoOutput;
7.   cameraInput?: camera.CameraInput;
8.   previewOutput1?: camera.PreviewOutput;
9.   previewOutput2?: camera.PreviewOutput;
10.   session?: camera.VideoSession;
11. }

12. @Entry
13. @Component
14. struct Index {
15.   private imageReceiver: image.ImageReceiver | undefined = undefined;
16.   private imageReceiverSurfaceId: string = '';
17.   private xComponentCtl: XComponentController = new XComponentController();
18.   private xComponentSurfaceId: string = '';
19.   @State imageWidth: number = 1920;
20.   @State imageHeight: number = 1080;
21.   private cameraManager: camera.CameraManager | undefined = undefined;
22.   private cameras: Array<camera.CameraDevice> | undefined = [];
23.   private uiContext: UIContext = this.getUIContext();
24.   private context: Context | undefined = this.uiContext.getHostContext();
25.   private cameraPermission: Permissions = 'ohos.permission.CAMERA'; // 申请权限相关问题可参考本篇开头的申请相关权限文档。
26.   @State isShow: boolean = false;
27.   private cameraResources: CameraResources = {};

28.   async requestPermissionsFn(): Promise<void> {
29.     let atManager = abilityAccessCtrl.createAtManager();
30.     if (this.context) {
31.       let res = await atManager.requestPermissionsFromUser(this.context, [this.cameraPermission]);
32.       if (!res || !res.permissions || res.permissions.length === 0) {
33.         console.error('requestPermissionsFromUser interface call fails');
34.         return;
35.       }
36.       if (res.permissions.length !== res.authResults.length) {
37.         console.error('Authentication result mismatch');
38.         return;
39.       }
40.       res.permissions.forEach((value: string, index: number, permissions: string[]) => {
41.         if (this.cameraPermission.toString() === value && res.authResults[index] === 0) {
42.           this.isShow = true;
43.         }
44.       })
45.     }
46.   }

47.   aboutToAppear(): void {
48.     this.requestPermissionsFn();
49.   }

50.   onPageShow(): void {
51.     console.info('onPageShow');
52.     this.initImageReceiver();
53.     if (this.xComponentSurfaceId !== '') {
54.       this.initCamera();
55.     }
56.   }

57.   onPageHide(): void {
58.     console.info('onPageHide');
59.     this.releaseCamera();
60.   }

61.   /**
62.    * 获取ImageReceiver的SurfaceId
63.    * @param receiver
64.    * @returns
65.    */
66.   async initImageReceiver(): Promise<void> {
67.     if (!this.imageReceiver) {
68.       // 创建ImageReceiver。
69.       let size: image.Size = { width: this.imageWidth, height: this.imageHeight };
70.       try {
71.         this.imageReceiver = image.createImageReceiver(size, image.ImageFormat.JPEG, 8);
72.       } catch (error) {
73.         let err = error as BusinessError;
74.         console.error(`Init image receiver failed. error code: ${err.code}`);
75.         return;
76.       }
77.       // 获取第一路流SurfaceId。
78.       this.imageReceiverSurfaceId = await this.imageReceiver.getReceivingSurfaceId();
79.       console.info(`initImageReceiver imageReceiverSurfaceId:${this.imageReceiverSurfaceId}`);
80.       // 注册监听处理预览流每帧图像数据。
81.       this.onImageArrival(this.imageReceiver);
82.     }
83.   }

84.   // Image格式与PixelMap格式映射关系。
85.   private formatToPixelMapFormatMap = new Map<number, image.PixelMapFormat>([
86.     [12, image.PixelMapFormat.RGBA_8888],
87.     [25, image.PixelMapFormat.NV21],
88.     [35, image.PixelMapFormat.YCBCR_P010],
89.     [36, image.PixelMapFormat.YCRCB_P010]
90.   ]);
91.   // PixelMapFormat格式的单个像素点大小映射关系。
92.   private pixelMapFormatToSizeMap = new Map<image.PixelMapFormat, number>([
93.     [image.PixelMapFormat.RGBA_8888, 4],
94.     [image.PixelMapFormat.NV21, 1.5],
95.     [image.PixelMapFormat.YCBCR_P010, 3],
96.     [image.PixelMapFormat.YCRCB_P010, 3]
97.   ]);

98.   /**
99.    * 注册ImageReceiver图像监听
100.    * @param receiver
101.    */
102.   onImageArrival(receiver: image.ImageReceiver): void {
103.     // 注册imageArrival监听。
104.     receiver.on('imageArrival', () => {
105.       console.info('image arrival');
106.       // 获取图像。
107.       receiver.readNextImage((err: BusinessError, nextImage: image.Image) => {
108.         if (err || nextImage === undefined) {
109.           console.error('readNextImage failed');
110.           return;
111.         }
112.         // 解析图像内容。
113.         nextImage.getComponent(image.ComponentType.JPEG, async (err: BusinessError, imgComponent: image.Component) => {
114.           if (err || imgComponent === undefined) {
115.             console.error('getComponent failed');
116.           }
117.           if (imgComponent.byteBuffer) {
118.             // 请参考步骤7解析buffer数据，本示例以方式一为例。
119.             let width = nextImage.size.width; // 获取图片的宽。
120.             let height = nextImage.size.height; // 获取图片的高。
121.             let stride = imgComponent.rowStride; // 获取图片的stride。
122.             let imageFormat = nextImage.format; // 获取图片的format。
123.             let pixelMapFormat = this.formatToPixelMapFormatMap.get(imageFormat) ?? image.PixelMapFormat.NV21;
124.             let mSize =  this.pixelMapFormatToSizeMap.get(pixelMapFormat) ?? 1.5;
125.             console.info(`getComponent with width:${width} height:${height} stride:${stride}`);
126.             // pixelMap创建时使用的size、srcPixelFormat需要与相机预览输出流previewProfile中的size、format保持一致。此处format以NV21格式为例。
127.             // stride与width一致。
128.             let pixelMap: image.PixelMap;
129.             if (stride == width) {
130.               pixelMap = await image.createPixelMap(imgComponent.byteBuffer, {
131.                 size: { height: height, width: width },
132.                 srcPixelFormat: pixelMapFormat,
133.               })
134.             } else {
135.               // stride与width不一致。
136.               const dstBufferSize = width * height * mSize // 以NV21为例（YUV_420_SP格式的图片）YUV_420_SP内存计算公式：长x宽+(长x宽)/2。
137.               const dstArr = new Uint8Array(dstBufferSize)
138.               for (let j = 0; j < height * mSize; j++) {
139.                 const srcBuf = new Uint8Array(imgComponent.byteBuffer, j * stride, width)
140.                 dstArr.set(srcBuf, j * width)
141.               }
142.               pixelMap = await image.createPixelMap(dstArr.buffer, {
143.                 size: { height: height, width: width },
144.                 srcPixelFormat: pixelMapFormat,
145.               })
146.             }
147.             // 确保当前pixelMap没有在使用的情况下，注意要进行资源释放。
148.             if (pixelMap != undefined) {
149.               await pixelMap.release().then(() => {
150.                 console.info('Succeeded in releasing pixelMap object.');
151.               }).catch((error: BusinessError) => {
152.                 console.error(`Failed to release pixelMap object. code is ${error.code}, message is ${error.message}`);
153.               })
154.             }
155.           } else {
156.             console.error('byteBuffer is null');
157.           }
158.           // 确保当前buffer没有在使用的情况下，可进行资源释放。
159.           // 如果对buffer进行异步操作，需要在异步操作结束后再释放该资源（nextImage.release()）。
160.           nextImage.release();
161.           console.info('image process done');
162.         })
163.       })
164.     })
165.   }

166.   build() {
167.     Column() {
168.       if (this.isShow) {
169.         XComponent({
170.           id: 'componentId',
171.           type: XComponentType.SURFACE,
172.           controller: this.xComponentCtl
173.         })
174.           .onLoad(async () => {
175.             console.info('onLoad is called');
176.             this.xComponentSurfaceId = this.xComponentCtl.getXComponentSurfaceId(); // 获取组件surfaceId。
177.             // 初始化相机，组件实时渲染每帧预览流数据。
178.             this.initCamera()
179.           })
180.           .width(this.uiContext.px2vp(this.imageHeight))
181.           .height(this.uiContext.px2vp(this.imageWidth))
182.       }
183.     }
184.     .justifyContent(FlexAlign.Center)
185.     .height('100%')
186.     .width('100%')
187.   }

188.   // 初始化相机。
189.   async initCamera(): Promise<void> {
190.     console.info(`initCamera imageReceiverSurfaceId:${this.imageReceiverSurfaceId} xComponentSurfaceId:${this.xComponentSurfaceId}`);
191.     try {
192.       // 获取相机管理器实例。
193.       this.cameraManager = camera.getCameraManager(this.context);
194.       if (!this.cameraManager) {
195.         console.error('getCameraManager call failed');
196.         return;
197.       }
198.       // 获取当前设备支持的相机device列表。
199.       this.cameras = this.cameraManager.getSupportedCameras();
200.       if (!this.cameras || this.cameras.length === 0) {
201.         console.error('getSupportedCameras call failed');
202.         return;
203.       }
204.       // 选择一个相机device，创建cameraInput输出对象。
205.       this.cameraResources.cameraInput = this.cameraManager.createCameraInput(this.cameras[0]);
206.       if (!this.cameraResources.cameraInput) {
207.         console.error('createCameraInput call failed');
208.         return;
209.       }
210.       // 打开相机。
211.       await this.cameraResources.cameraInput.open();
212.       // 获取相机device支持的profile。
213.       let capability: camera.CameraOutputCapability =
214.         this.cameraManager.getSupportedOutputCapability(this.cameras[0], camera.SceneMode.NORMAL_VIDEO);
215.       if (!capability) {
216.         console.error('getSupportedOutputCapability call failed');
217.         this.releaseCamera();
218.         return;
219.       }
220.       let minRatioDiff : number = 0.1;
221.       let surfaceRatio : number = this.imageWidth / this.imageHeight; // 最接近16:9宽高比。
222.       let previewProfile: camera.Profile = capability.previewProfiles[0];
223.       // 应用开发者根据实际业务需求选择一个支持的预览流previewProfile。
224.       // 此处以选择CAMERA_FORMAT_YUV_420_SP（NV21）格式、满足限定条件分辨率的预览流previewProfile为例。
225.       for (let index = 0; index < capability.previewProfiles.length; index++) {
226.         const tempProfile = capability.previewProfiles[index];
227.         let tempRatio = tempProfile.size.width >= tempProfile.size.height ?
228.           tempProfile.size.width / tempProfile.size.height : tempProfile.size.height / tempProfile.size.width;
229.         let currentRatio = Math.abs(tempRatio - surfaceRatio);
230.         if (currentRatio <= minRatioDiff && tempProfile.format == camera.CameraFormat.CAMERA_FORMAT_YUV_420_SP) {
231.           previewProfile = tempProfile;
232.           break;
233.         }
234.       }
235.       this.imageWidth = previewProfile.size.width; // 更新xComponent组件的宽。
236.       this.imageHeight = previewProfile.size.height; // 更新xComponent组件的高。
237.       console.info(`initCamera imageWidth:${this.imageWidth} imageHeight:${this.imageHeight}`);
238.       // 使用imageReceiverSurfaceId创建第一路预览。
239.       this.cameraResources.previewOutput1 = this.cameraManager.createPreviewOutput(previewProfile, this.imageReceiverSurfaceId);
240.       if (!this.cameraResources.previewOutput1) {
241.         console.error('initCamera createPreviewOutput1');
242.         this.releaseCamera();
243.         return;
244.       }
245.       // 使用xComponentSurfaceId创建第二路预览。
246.       this.cameraResources.previewOutput2 = this.cameraManager.createPreviewOutput(previewProfile, this.xComponentSurfaceId);
247.       if (!this.cameraResources.previewOutput2) {
248.         console.error('initCamera createPreviewOutput2');
249.         this.releaseCamera();
250.         return;
251.       }
252.       // 创建录像模式相机会话。
253.       let session = this.cameraManager.createSession(camera.SceneMode.NORMAL_VIDEO)
254.       if (!session) {
255.         console.error('session is null');
256.         this.releaseCamera();
257.         return;
258.       }
259.       this.cameraResources.session = session as camera.VideoSession;
260.       // 开始配置会话。
261.       this.cameraResources.session.beginConfig();
262.       // 添加相机设备输入。
263.       this.cameraResources.session.addInput(this.cameraResources.cameraInput);
264.       // 添加第一路预览流输出。
265.       this.cameraResources.session.addOutput(this.cameraResources.previewOutput1);
266.       // 添加第二路预览流输出。
267.       this.cameraResources.session.addOutput(this.cameraResources.previewOutput2);
268.       // 提交会话配置。
269.       await this.cameraResources.session.commitConfig();
270.       // 开始启动已配置的输入输出流。
271.       await this.cameraResources.session.start();
272.     } catch (error) {
273.       console.error(`initCamera fail: ${JSON.stringify(error)}`);
274.       this.releaseCamera();
275.     }
276.   }

277.   // 释放相机。
278.   async releaseCamera(): Promise<void> {
279.     console.info('releaseCamera E');
280.     try {
281.       // 停止当前会话。
282.       await this.cameraResources.session?.stop();
283.     } catch (error) {
284.       console.error(`session.stop call failed, error: ${JSON.stringify(error)}`);
285.     }
286.     try {
287.       // 释放相机输入流。
288.       await this.cameraResources.cameraInput?.close();
289.     } catch (error) {
290.       console.error(`camera close fail: ${JSON.stringify(error)}`);
291.     }
292.     try {
293.       // 释放预览输出流。
294.       await this.cameraResources.previewOutput1?.release();
295.     } catch (error) {
296.       console.error(`previewOutput1 release fail: ${JSON.stringify(error)}`);
297.     }
298.     try {
299.       // 释放拍照输出流。
300.       await this.cameraResources.previewOutput2?.release();
301.     } catch (error) {
302.       console.error(`previewOutput2 release fail: ${JSON.stringify(error)}`);
303.     }
304.     try {
305.       // 释放会话。
306.       await this.cameraResources.session?.release();
307.     } catch (error) {
308.       console.error(`session release fail: ${JSON.stringify(error)}`);
309.     }
310.   }
311. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-preview "预览(ArkTS)")
# 拍照(ArkTS)

更新时间: 2025-12-16 16:35

拍照是相机的最重要功能之一，拍照模块基于相机复杂的逻辑，为了保证用户拍出的照片质量，在中间步骤可以设置分辨率、闪光灯、焦距、照片质量及旋转角度等信息。

## 开发步骤

详细的API说明请参考[Camera API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera)。

1. 导入image接口。创建拍照输出流的SurfaceId以及拍照输出的数据，都需要用到系统提供的image接口能力，导入image接口的方法如下。
    
    1. import { image } from '@kit.ImageKit';
    2. import { camera } from '@kit.CameraKit';
    3. import { fileIo as fs } from '@kit.CoreFileKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 创建拍照输出流。
    
    通过[CameraOutputCapability](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#cameraoutputcapability)中的photoProfiles属性，可获取当前设备支持的拍照输出流，通过[createPhotoOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#createphotooutput11)方法传入支持的某一个输出流及步骤一获取的SurfaceId创建拍照输出流。
    
    1. function getPhotoOutput(cameraManager: camera.CameraManager, cameraOutputCapability: camera.CameraOutputCapability): camera.PhotoOutput | undefined {
    2.   let photoProfilesArray: Array<camera.Profile> = cameraOutputCapability.photoProfiles;
    3.   if (!photoProfilesArray || photoProfilesArray.length === 0) {
    4.     console.error("photoProfilesArray is null or []");
    5.   }
    6.   let photoOutput: camera.PhotoOutput | undefined = undefined;
    7.   try {
    8.     photoOutput = cameraManager.createPhotoOutput(photoProfilesArray[0]);
    9.   } catch (error) {
    10.     let err = error as BusinessError;
    11.     console.error(`Failed to createPhotoOutput. error: ${err}`);
    12.   }
    13.   return photoOutput;
    14. }
    
3. 设置拍照photoAvailable的回调，并将拍照的buffer保存为图片。
    
    Context获取方式请参考：[获取UIAbility的上下文信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uiability-usage#%E8%8E%B7%E5%8F%96uiability%E7%9A%84%E4%B8%8A%E4%B8%8B%E6%96%87%E4%BF%A1%E6%81%AF)。
    
    如需要在图库中看到所保存的图片、视频资源，需要将其保存到媒体库，保存方式请参考：[保存媒体库资源](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/photoaccesshelper-savebutton)。
    
    需要在[photoOutput.on('photoAvailable')](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-photooutput#onphotoavailable11)接口获取到buffer时，将buffer在安全控件中保存到媒体库。
    
    1. function setPhotoOutputCb(photoOutput: camera.PhotoOutput) {
    2. // 设置回调之后，调用photoOutput的capture方法，就会将拍照的buffer回传到回调中。
    3.   photoOutput.on('photoAvailable', (errCode: BusinessError, photo: camera.Photo): void => {
    4.      console.info('getPhoto start');
    5.      if (errCode || photo === undefined) {
    6.        console.error('getPhoto failed, err: ${errCode}');
    7.        return;
    8.      }
    9.      let imageObj: image.Image = photo.main;
    10.      imageObj.getComponent(image.ComponentType.JPEG, (errCode: BusinessError, component: image.Component): void => {
    11.        console.info('getComponent start');
    12.        if (errCode || component === undefined) {
    13.          console.error('getComponent failed');
    14.          return;
    15.        }
    16.        let buffer: ArrayBuffer;
    17.        if (component.byteBuffer) {
    18.          buffer = component.byteBuffer;
    19.        } else {
    20.          console.error('byteBuffer is null');
    21.          return;
    22.        }
    23.        // 如需要在图库中看到所保存的图片、视频资源，请使用用户无感的安全控件创建媒体资源。
    
    24.       // buffer处理结束后需要释放该资源，如果未正确释放资源会导致后续拍照获取不到buffer。
    25.       imageObj.release();
    26.     });
    27.   });
    28. }
    
4. 参数配置。
    
    配置相机的参数可以调整拍照的一些功能，包括闪光灯、变焦、焦距等。
    
    1. function configuringSession(photoSession: camera.PhotoSession): void {
    2.   // 判断设备是否支持闪光灯。
    3.   let flashStatus: boolean = false;
    4.   try {
    5.     flashStatus = photoSession.hasFlash();
    6.   } catch (error) {
    7.     let err = error as BusinessError;
    8.     console.error(`Failed to hasFlash. error: ${err}`);
    9.   }
    10.   console.info(`Returned with the flash light support status: ${flashStatus}`);
    11.   if (flashStatus) {
    12.     // 判断是否支持自动闪光灯模式。
    13.     let flashModeStatus: boolean = false;
    14.     try {
    15.       flashModeStatus = photoSession?.isFlashModeSupported(camera.FlashMode.FLASH_MODE_AUTO);
    16.     } catch (error) {
    17.       let err = error as BusinessError;
    18.       console.error(`Failed to check whether the flash mode is supported. error: ${err}`);
    19.     }
    20.     if (flashModeStatus) {
    21.       // 设置自动闪光灯模式。
    22.       try {
    23.         photoSession?.setFlashMode(camera.FlashMode.FLASH_MODE_AUTO);
    24.       } catch (error) {
    25.         let err = error as BusinessError;
    26.         console.error(`Failed to set the flash mode. error: ${err}`);
    27.       }
    28.     }
    29.   }
    30.   // 判断是否支持连续自动变焦模式。
    31.   let focusModeStatus: boolean = false;
    32.   try {
    33.     focusModeStatus = photoSession?.isFocusModeSupported(camera.FocusMode.FOCUS_MODE_CONTINUOUS_AUTO);
    34.   } catch (error) {
    35.     let err = error as BusinessError;
    36.     console.error(`Failed to check whether the focus mode is supported. error: ${err}`);
    37.   }
    38.   if (focusModeStatus) {
    39.     // 设置连续自动变焦模式。
    40.     try {
    41.       photoSession?.setFocusMode(camera.FocusMode.FOCUS_MODE_CONTINUOUS_AUTO);
    42.     } catch (error) {
    43.       let err = error as BusinessError;
    44.       console.error(`Failed to set the focus mode. error: ${err}`);
    45.     }
    46.   }
    47.   // 获取相机支持的可变焦距比范围。
    48.   let zoomRatioRange: Array<number> = [];
    49.   try {
    50.     zoomRatioRange = photoSession?.getZoomRatioRange();
    51.   } catch (error) {
    52.     let err = error as BusinessError;
    53.     console.error(`Failed to get the zoom ratio range. error: ${err}`);
    54.   }
    55.   if (zoomRatioRange.length <= 0 ) {
    56.     return;
    57.   }
    58.   // 设置可变焦距比。
    59.   try {
    60.     photoSession?.setZoomRatio(zoomRatioRange[0]);
    61.   } catch (error) {
    62.     let err = error as BusinessError;
    63.     console.error(`Failed to set the zoom ratio value. error: ${err}`);
    64.   }
    65. }
    
5. 触发拍照。
    
    通过photoOutput的[capture](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-photooutput#capture-2)方法，执行拍照任务。该方法有两个参数，第一个参数为拍照设置参数的setting，setting中可以设置照片的质量和旋转角度，第二参数为回调函数。
    
    获取拍照旋转角度的方法为，通过[PhotoOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-photooutput)中的[getPhotoRotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-photooutput#getphotorotation12)方法获取rotation实际的值。
    
    说明
    
    图片地理位置信息[Location](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-geolocationmanager#geolocationmanagergetcurrentlocation)，使用方法可参考[capture](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-photooutput#capture-3)示例。
    
    1. function capture(captureLocation: camera.Location, photoOutput: camera.PhotoOutput): void {
    2.   let settings: camera.PhotoCaptureSetting = {
    3.     quality: camera.QualityLevel.QUALITY_LEVEL_HIGH,  // 设置图片质量高。
    4.     rotation: camera.ImageRotation.ROTATION_0,  // 设置图片旋转角度的camera.ImageRotation.ROTATION_0是通过说明中获取拍照角度的getPhotoRotation方法获取的值进行设置。
    5.     location: captureLocation,  // 设置图片地理位置。
    6.     mirror: false  // 设置镜像使能开关(默认关)。
    7.   };
    8.   try {
    9.     photoOutput.capture(settings, (err: BusinessError) => {
    10.       if (err) {
    11.         console.error(`Failed to capture the photo. error: ${err}`);
    12.         return;
    13.       }
    14.       console.info('Callback invoked to indicate the photo capture request success.');
    15.     });
    16.   } catch (error) {
    17.     console.error(`capture call failed. error: ${error}`);
    18.   }
    19. }
    

## 状态监听

在相机应用开发过程中，可以随时监听拍照输出流状态，包括拍照流开始、拍照帧的开始与结束、拍照输出流的错误。

- 通过注册固定的captureStart回调函数获取监听拍照开始结果，photoOutput创建成功时即可监听，相机设备已经准备开始这次拍照时触发，该事件返回此次拍照的captureId。
    
    1. function onPhotoOutputCaptureStart(photoOutput: camera.PhotoOutput): void {
    2.   photoOutput.on('captureStartWithInfo', (err: BusinessError, captureStartInfo: camera.CaptureStartInfo) => {
    3.     if (err !== undefined && err.code !== 0) {
    4.       return;
    5.     }
    6.     console.info(`photo capture started, captureId : ${captureStartInfo.captureId}`);
    7.   });
    8. }
    
- 通过注册固定的captureEnd回调函数获取监听拍照结束结果，photoOutput创建成功时即可监听，该事件返回结果为拍照完全结束后的相关信息[CaptureEndInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#captureendinfo)。
    
    1. function onPhotoOutputCaptureEnd(photoOutput: camera.PhotoOutput): void {
    2.   photoOutput.on('captureEnd', (err: BusinessError, captureEndInfo: camera.CaptureEndInfo) => {
    3.     if (err !== undefined && err.code !== 0) {
    4.       return;
    5.     }
    6.     console.info(`photo capture end, captureId : ${captureEndInfo.captureId}`);
    7.     console.info(`frameCount : ${captureEndInfo.frameCount}`);
    8.   });
    9. }
    
- 通过注册固定的captureReady回调函数获取监听可拍下一张结果，photoOutput创建成功时即可监听，当下一张可拍时触发，该事件返回结果为下一张可拍的相关信息。
    
    1. function onPhotoOutputCaptureReady(photoOutput: camera.PhotoOutput): void {
    2.   photoOutput.on('captureReady', (err: BusinessError) => {
    3.     if (err !== undefined && err.code !== 0) {
    4.       return;
    5.     }
    6.     console.info(`photo capture ready`);
    7.   });
    8. }
    
- 通过注册固定的error回调函数获取监听拍照输出流的错误结果。回调返回拍照输出接口使用错误时的对应错误码，错误码类型参见[Camera错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraerrorcode)。
    
    1. function onPhotoOutputError(photoOutput: camera.PhotoOutput): void {
    2.   photoOutput.on('error', (error: BusinessError) => {
    3.     console.error(`Photo output error code: ${error.code}`);
    4.   });
    5. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-dual-channel-preview "双路预览(ArkTS)")
# 录像(ArkTS)

更新时间: 2025-12-16 16:35

在开发相机应用时，需要先[申请相关权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-preparation)。

相机应用可通过调用和控制相机设备，完成预览、拍照和录像等基础操作。

录像也是相机应用的最重要功能之一，录像是循环帧的捕获。对于录像的流畅度，开发者可以参考[拍照](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-shooting)中的步骤4，设置分辨率、闪光灯、焦距、照片质量及旋转角度等信息。

## 开发步骤

详细的API说明请参考[Camera API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera)。

1. 导入media模块。
    
    创建录像输出流的SurfaceId以及录像输出的数据，都需要用到系统提供的[media接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media)能力，导入media接口的方法如下。
    
    1. import { BusinessError } from '@kit.BasicServicesKit';
    2. import { camera } from '@kit.CameraKit';
    3. import { media } from '@kit.MediaKit';
    
2. 创建Surface。
    
    系统提供的media接口可以创建一个录像[AVRecorder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media-avrecorder)实例，通过该实例的[getInputSurface](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media-avrecorder#getinputsurface9)方法获取SurfaceId，与录像输出流做关联，处理录像输出流输出的数据。
    
    1. async function getVideoSurfaceId(aVRecorderConfig: media.AVRecorderConfig): Promise<string | undefined> {  // aVRecorderConfig可参考步骤3.创建录像输出流。
    2.   let avRecorder: media.AVRecorder | undefined = undefined;
    3.   let videoSurfaceId: string | undefined = undefined;
    4.   try {
    5.     avRecorder = await media.createAVRecorder();
    6.     if (avRecorder === undefined) {
    7.       return videoSurfaceId;
    8.     }
    9.     await avRecorder.prepare(aVRecorderConfig);
    10.     videoSurfaceId = await avRecorder.getInputSurface();
    11.   } catch (error) {
    12.     let err = error as BusinessError;
    13.     console.error(`createAVRecorder call failed. error code: ${err.code}`);
    14.   }
    15.   return videoSurfaceId;
    16. }
    
3. 创建录像输出流。
    
    通过[CameraOutputCapability](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#cameraoutputcapability)中的videoProfiles属性，可获取当前设备支持的录像输出流。然后，定义创建录像的参数，通过[createVideoOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#createvideooutput)方法创建录像输出流。
    
    说明
    
    1.预览流与录像输出流的分辨率的宽高比要保持一致，如示例代码中宽高比为640:480 = 4:3，则需要预览流中的分辨率的宽高比也为4:3，如分辨率选择640:480，或960:720，或1440:1080，以此类推。
    
    2.在设置预览输出流的分辨率宽高前，需要先通过[AVRecorderProfile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media-i#avrecorderprofile9)查询视频帧支持可配置的宽高范围。
    
    3.获取录像旋转角度的方法：通过[VideoOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-videooutput)中的[getVideoRotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-videooutput#getvideorotation12)方法获取rotation实际的值。
    
    4.录像输出流帧率通过[CameraOutputCapability](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#cameraoutputcapability)中的videoProfiles属性，选择[VideoProfile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#videoprofile)中[frameRateRange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#frameraterange)满足实际业务需求的录像输出流videoProfile。
    
    1. async function getVideoOutput(cameraManager: camera.CameraManager, videoSurfaceId: string, cameraOutputCapability: camera.CameraOutputCapability): Promise<camera.VideoOutput | undefined> {
    2.   if (!cameraManager || !videoSurfaceId || !cameraOutputCapability || !cameraOutputCapability.videoProfiles) {
    3.     return;
    4.   }
    5.   let videoProfilesArray: Array<camera.VideoProfile> = cameraOutputCapability.videoProfiles;
    6.   if (!videoProfilesArray || videoProfilesArray.length === 0) {
    7.     console.error("videoProfilesArray is null or []");
    8.     return undefined;
    9.   }
    10.   // AVRecorderProfile。
    11.   let aVRecorderProfile: media.AVRecorderProfile = {
    12.     fileFormat : media.ContainerFormatType.CFT_MPEG_4, // 视频文件封装格式，只支持MP4。
    13.     videoBitrate : 100000, // 视频比特率。
    14.     videoCodec : media.CodecMimeType.VIDEO_AVC, // 视频文件编码格式，支持avc格式。
    15.     videoFrameWidth : 640,  // 视频分辨率的宽。
    16.     videoFrameHeight : 480, // 视频分辨率的高。
    17.     videoFrameRate : 30 // 视频帧率。
    18.   };
    19.   // 创建视频录制的参数，预览流与录像输出流的分辨率的宽(videoFrameWidth)高(videoFrameHeight)比要保持一致。
    20.   let avMetadata: media.AVMetadata = {
    21.    videoOrientation: '90' // rotation的值90，是通过getVideoRotation接口获取到的值，具体请参考说明中获取录像旋转角度的方法。
    22.   }
    
    23.   let aVRecorderConfig: media.AVRecorderConfig = {
    24.     videoSourceType: media.VideoSourceType.VIDEO_SOURCE_TYPE_SURFACE_YUV,
    25.     profile: aVRecorderProfile,
    26.     url: 'fd://35', // 此处为样例示范，需要根据开发需求填写实际的路径。
    27.     metadata: avMetadata
    28.   };
    29.   // 创建avRecorder，设置视频录制的参数。
    30.   let avRecorder: media.AVRecorder | undefined = undefined;
    31.   try {
    32.     avRecorder = await media.createAVRecorder();
    33.     if (avRecorder === undefined) {
    34.       return undefined;
    35.     }
    36.     await avRecorder.prepare(aVRecorderConfig);
    37.   } catch (error) {
    38.     let err = error as BusinessError;
    39.     console.error(`createAVRecorder call failed. error code: ${err.code}`);
    40.     await avRecorder?.release();
    41.     return;
    42.   }
    
    43.   // 创建VideoOutput对象。
    44.   let videoOutput: camera.VideoOutput | undefined = undefined;
    45.   // createVideoOutput传入的videoProfile对象的宽高需要和aVRecorderProfile保持一致。
    46.   let videoProfile: undefined | camera.VideoProfile = videoProfilesArray.find((profile: camera.VideoProfile) => {
    47.     return profile.size.width === aVRecorderProfile.videoFrameWidth && profile.size.height === aVRecorderProfile.videoFrameHeight;
    48.   });
    49.   if (!videoProfile) {
    50.     console.error('videoProfile is not found');
    51.     await avRecorder.release();
    52.     return undefined;
    53.   }
    54.   try {
    55.     videoOutput = cameraManager.createVideoOutput(videoProfile, videoSurfaceId);
    56.   } catch (error) {
    57.     let err = error as BusinessError;
    58.     console.error('Failed to create the videoOutput instance. errorCode = ' + err.code);
    59.     await avRecorder.release();
    60.   }
    61.   return videoOutput;
    62. }
    
4. 开始录像。
    
    说明
    
    - 在设置预览流帧率时，需要先通过[getActiveFrameRate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-previewoutput#getactiveframerate12)查询当前录像流的帧率。
        
    - 当录像流已设置过范围帧率时，预览流帧率必须设置与其相同的范围帧率。
        
    - 当录像流已设置过固定帧率时，预览流帧率要设置成录像帧率的约数，且必须也为固定帧率。
        
    
    先通过videoOutput的[start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-videooutput#start-1)方法启动录像输出流，再通过avRecorder的[start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media-avrecorder#start9)方法开始录像。
    
    1. async function startVideo(videoOutput: camera.VideoOutput, avRecorder: media.AVRecorder): Promise<void> {
    2.  try {
    3.    await videoOutput.start();
    4.  } catch (error) {
    5.    let err = error as BusinessError;
    6.    console.error(`start videoOutput failed, error: ${err.code}`);
    7.  }
    8.  avRecorder.start(async (err: BusinessError) => {
    9.  if (err) {
    10.    console.error(`Failed to start the video output ${err.message}`);
    11.    return;
    12.  }
    13.  console.info('Callback invoked to indicate the video output start success.');
    14.  });
    15. }
    
5. 停止录像。
    
    先通过avRecorder的[stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media-avrecorder#stop9-1)方法停止录像，再通过videoOutput的[stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-videooutput#stop-1)方法停止录像输出流。
    
    1. async function stopVideo(videoOutput: camera.VideoOutput, avRecorder: media.AVRecorder): Promise<void> {
    2.   avRecorder.stop((err: BusinessError) => {
    3.   if (err) {
    4.     console.error(`Failed to stop the video output ${err.message}`);
    5.     return;
    6.   }
    7.   console.info('Callback invoked to indicate the video output stop success.');
    8.   });
    9.   await videoOutput.stop();
    10. }
    

## 状态监听

在相机应用开发过程中，可以随时监听录像输出流状态，包括录像开始、录像结束、录像流输出的错误。

- 通过注册固定的frameStart回调函数获取监听录像开始结果，videoOutput创建成功时即可监听，录像第一次曝光时触发，有该事件返回结果则认为录像开始。
    
    1. function onVideoOutputFrameStart(videoOutput: camera.VideoOutput): void {
    2.   videoOutput.on('frameStart', (err: BusinessError) => {
    3.     if (err !== undefined && err.code !== 0) {
    4.       return;
    5.     }
    6.     console.info('Video frame started');
    7.   });
    8. }
    
- 通过注册固定的frameEnd回调函数获取监听录像结束结果，videoOutput创建成功时即可监听，录像完成最后一帧时触发，有该事件返回结果则认为录像流已结束。
    
    1. function onVideoOutputFrameEnd(videoOutput: camera.VideoOutput): void {
    2.   videoOutput.on('frameEnd', (err: BusinessError) => {
    3.     if (err !== undefined && err.code !== 0) {
    4.       return;
    5.     }
    6.     console.info('Video frame ended');
    7.   });
    8. }
    
- 通过注册固定的error回调函数获取监听录像输出错误结果，callback返回预览输出接口使用错误时对应的错误码，错误码类型参见[Camera错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraerrorcode)。
    
    1. function onVideoOutputError(videoOutput: camera.VideoOutput): void {
    2.   videoOutput.on('error', (error: BusinessError) => {
    3.     console.error(`Video output error code: ${error.code}`);
    4.   });
    5. }
    

## 示例代码

- [基于CameraKit通过AVRecorder录像](https://gitee.com/harmonyos_samples/camera-kit-avrecorder)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-shooting-case "拍照实践(ArkTS)")
# 录像(ArkTS)

更新时间: 2025-12-16 16:35

在开发相机应用时，需要先[申请相关权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-preparation)。

相机应用可通过调用和控制相机设备，完成预览、拍照和录像等基础操作。

录像也是相机应用的最重要功能之一，录像是循环帧的捕获。对于录像的流畅度，开发者可以参考[拍照](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-shooting)中的步骤4，设置分辨率、闪光灯、焦距、照片质量及旋转角度等信息。

## 开发步骤

详细的API说明请参考[Camera API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera)。

1. 导入media模块。
    
    创建录像输出流的SurfaceId以及录像输出的数据，都需要用到系统提供的[media接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media)能力，导入media接口的方法如下。
    
    1. import { BusinessError } from '@kit.BasicServicesKit';
    2. import { camera } from '@kit.CameraKit';
    3. import { media } from '@kit.MediaKit';
    
2. 创建Surface。
    
    系统提供的media接口可以创建一个录像[AVRecorder](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media-avrecorder)实例，通过该实例的[getInputSurface](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media-avrecorder#getinputsurface9)方法获取SurfaceId，与录像输出流做关联，处理录像输出流输出的数据。
    
    1. async function getVideoSurfaceId(aVRecorderConfig: media.AVRecorderConfig): Promise<string | undefined> {  // aVRecorderConfig可参考步骤3.创建录像输出流。
    2.   let avRecorder: media.AVRecorder | undefined = undefined;
    3.   let videoSurfaceId: string | undefined = undefined;
    4.   try {
    5.     avRecorder = await media.createAVRecorder();
    6.     if (avRecorder === undefined) {
    7.       return videoSurfaceId;
    8.     }
    9.     await avRecorder.prepare(aVRecorderConfig);
    10.     videoSurfaceId = await avRecorder.getInputSurface();
    11.   } catch (error) {
    12.     let err = error as BusinessError;
    13.     console.error(`createAVRecorder call failed. error code: ${err.code}`);
    14.   }
    15.   return videoSurfaceId;
    16. }
    
3. 创建录像输出流。
    
    通过[CameraOutputCapability](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#cameraoutputcapability)中的videoProfiles属性，可获取当前设备支持的录像输出流。然后，定义创建录像的参数，通过[createVideoOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#createvideooutput)方法创建录像输出流。
    
    说明
    
    1.预览流与录像输出流的分辨率的宽高比要保持一致，如示例代码中宽高比为640:480 = 4:3，则需要预览流中的分辨率的宽高比也为4:3，如分辨率选择640:480，或960:720，或1440:1080，以此类推。
    
    2.在设置预览输出流的分辨率宽高前，需要先通过[AVRecorderProfile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media-i#avrecorderprofile9)查询视频帧支持可配置的宽高范围。
    
    3.获取录像旋转角度的方法：通过[VideoOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-videooutput)中的[getVideoRotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-videooutput#getvideorotation12)方法获取rotation实际的值。
    
    4.录像输出流帧率通过[CameraOutputCapability](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#cameraoutputcapability)中的videoProfiles属性，选择[VideoProfile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#videoprofile)中[frameRateRange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#frameraterange)满足实际业务需求的录像输出流videoProfile。
    
    1. async function getVideoOutput(cameraManager: camera.CameraManager, videoSurfaceId: string, cameraOutputCapability: camera.CameraOutputCapability): Promise<camera.VideoOutput | undefined> {
    2.   if (!cameraManager || !videoSurfaceId || !cameraOutputCapability || !cameraOutputCapability.videoProfiles) {
    3.     return;
    4.   }
    5.   let videoProfilesArray: Array<camera.VideoProfile> = cameraOutputCapability.videoProfiles;
    6.   if (!videoProfilesArray || videoProfilesArray.length === 0) {
    7.     console.error("videoProfilesArray is null or []");
    8.     return undefined;
    9.   }
    10.   // AVRecorderProfile。
    11.   let aVRecorderProfile: media.AVRecorderProfile = {
    12.     fileFormat : media.ContainerFormatType.CFT_MPEG_4, // 视频文件封装格式，只支持MP4。
    13.     videoBitrate : 100000, // 视频比特率。
    14.     videoCodec : media.CodecMimeType.VIDEO_AVC, // 视频文件编码格式，支持avc格式。
    15.     videoFrameWidth : 640,  // 视频分辨率的宽。
    16.     videoFrameHeight : 480, // 视频分辨率的高。
    17.     videoFrameRate : 30 // 视频帧率。
    18.   };
    19.   // 创建视频录制的参数，预览流与录像输出流的分辨率的宽(videoFrameWidth)高(videoFrameHeight)比要保持一致。
    20.   let avMetadata: media.AVMetadata = {
    21.    videoOrientation: '90' // rotation的值90，是通过getVideoRotation接口获取到的值，具体请参考说明中获取录像旋转角度的方法。
    22.   }
    
    23.   let aVRecorderConfig: media.AVRecorderConfig = {
    24.     videoSourceType: media.VideoSourceType.VIDEO_SOURCE_TYPE_SURFACE_YUV,
    25.     profile: aVRecorderProfile,
    26.     url: 'fd://35', // 此处为样例示范，需要根据开发需求填写实际的路径。
    27.     metadata: avMetadata
    28.   };
    29.   // 创建avRecorder，设置视频录制的参数。
    30.   let avRecorder: media.AVRecorder | undefined = undefined;
    31.   try {
    32.     avRecorder = await media.createAVRecorder();
    33.     if (avRecorder === undefined) {
    34.       return undefined;
    35.     }
    36.     await avRecorder.prepare(aVRecorderConfig);
    37.   } catch (error) {
    38.     let err = error as BusinessError;
    39.     console.error(`createAVRecorder call failed. error code: ${err.code}`);
    40.     await avRecorder?.release();
    41.     return;
    42.   }
    
    43.   // 创建VideoOutput对象。
    44.   let videoOutput: camera.VideoOutput | undefined = undefined;
    45.   // createVideoOutput传入的videoProfile对象的宽高需要和aVRecorderProfile保持一致。
    46.   let videoProfile: undefined | camera.VideoProfile = videoProfilesArray.find((profile: camera.VideoProfile) => {
    47.     return profile.size.width === aVRecorderProfile.videoFrameWidth && profile.size.height === aVRecorderProfile.videoFrameHeight;
    48.   });
    49.   if (!videoProfile) {
    50.     console.error('videoProfile is not found');
    51.     await avRecorder.release();
    52.     return undefined;
    53.   }
    54.   try {
    55.     videoOutput = cameraManager.createVideoOutput(videoProfile, videoSurfaceId);
    56.   } catch (error) {
    57.     let err = error as BusinessError;
    58.     console.error('Failed to create the videoOutput instance. errorCode = ' + err.code);
    59.     await avRecorder.release();
    60.   }
    61.   return videoOutput;
    62. }
    
4. 开始录像。
    
    说明
    
    - 在设置预览流帧率时，需要先通过[getActiveFrameRate](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-previewoutput#getactiveframerate12)查询当前录像流的帧率。
        
    - 当录像流已设置过范围帧率时，预览流帧率必须设置与其相同的范围帧率。
        
    - 当录像流已设置过固定帧率时，预览流帧率要设置成录像帧率的约数，且必须也为固定帧率。
        
    
    先通过videoOutput的[start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-videooutput#start-1)方法启动录像输出流，再通过avRecorder的[start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media-avrecorder#start9)方法开始录像。
    
    1. async function startVideo(videoOutput: camera.VideoOutput, avRecorder: media.AVRecorder): Promise<void> {
    2.  try {
    3.    await videoOutput.start();
    4.  } catch (error) {
    5.    let err = error as BusinessError;
    6.    console.error(`start videoOutput failed, error: ${err.code}`);
    7.  }
    8.  avRecorder.start(async (err: BusinessError) => {
    9.  if (err) {
    10.    console.error(`Failed to start the video output ${err.message}`);
    11.    return;
    12.  }
    13.  console.info('Callback invoked to indicate the video output start success.');
    14.  });
    15. }
    
5. 停止录像。
    
    先通过avRecorder的[stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-media-avrecorder#stop9-1)方法停止录像，再通过videoOutput的[stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-videooutput#stop-1)方法停止录像输出流。
    
    1. async function stopVideo(videoOutput: camera.VideoOutput, avRecorder: media.AVRecorder): Promise<void> {
    2.   avRecorder.stop((err: BusinessError) => {
    3.   if (err) {
    4.     console.error(`Failed to stop the video output ${err.message}`);
    5.     return;
    6.   }
    7.   console.info('Callback invoked to indicate the video output stop success.');
    8.   });
    9.   await videoOutput.stop();
    10. }
    

## 状态监听

在相机应用开发过程中，可以随时监听录像输出流状态，包括录像开始、录像结束、录像流输出的错误。

- 通过注册固定的frameStart回调函数获取监听录像开始结果，videoOutput创建成功时即可监听，录像第一次曝光时触发，有该事件返回结果则认为录像开始。
    
    1. function onVideoOutputFrameStart(videoOutput: camera.VideoOutput): void {
    2.   videoOutput.on('frameStart', (err: BusinessError) => {
    3.     if (err !== undefined && err.code !== 0) {
    4.       return;
    5.     }
    6.     console.info('Video frame started');
    7.   });
    8. }
    
- 通过注册固定的frameEnd回调函数获取监听录像结束结果，videoOutput创建成功时即可监听，录像完成最后一帧时触发，有该事件返回结果则认为录像流已结束。
    
    1. function onVideoOutputFrameEnd(videoOutput: camera.VideoOutput): void {
    2.   videoOutput.on('frameEnd', (err: BusinessError) => {
    3.     if (err !== undefined && err.code !== 0) {
    4.       return;
    5.     }
    6.     console.info('Video frame ended');
    7.   });
    8. }
    
- 通过注册固定的error回调函数获取监听录像输出错误结果，callback返回预览输出接口使用错误时对应的错误码，错误码类型参见[Camera错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraerrorcode)。
    
    1. function onVideoOutputError(videoOutput: camera.VideoOutput): void {
    2.   videoOutput.on('error', (error: BusinessError) => {
    3.     console.error(`Video output error code: ${error.code}`);
    4.   });
    5. }
    

## 示例代码

- [基于CameraKit通过AVRecorder录像](https://gitee.com/harmonyos_samples/camera-kit-avrecorder)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-shooting-case "拍照实践(ArkTS)")
# 元数据(ArkTS)

更新时间: 2025-12-16 16:35

在开发相机应用时，需要先[申请相关权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-preparation)。

元数据（Metadata）是对相机返回的图像信息的描述和上下文。针对图像信息，提供更详细的数据，如照片或视频中，识别人像的取景框坐标的信息等。

Metadata主要是通过一个TAG（Key），去找对应的Data，用于传递参数和配置信息，减少内存拷贝操作。

## 适用场景

检测图片中的人脸，返回高精度的人脸矩形框坐标。应用可基于人脸定位结果，灵活集成后处理算法，将其应用于多样化场景。

## 开发步骤

详细的API说明请参考[Camera API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera)。

1. 导入相关接口，导入方法如下。
    
    1. import { camera } from '@kit.CameraKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 调用[CameraOutputCapability](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#cameraoutputcapability)中的supportedMetadataObjectTypes属性，获取当前设备支持的元数据类型，并通过[createMetadataOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#createmetadataoutput)方法创建元数据输出流。
    
    1. function getMetadataOutput(cameraManager: camera.CameraManager, cameraOutputCapability: camera.CameraOutputCapability): camera.MetadataOutput | undefined {
    2.   let metadataObjectTypes: Array<camera.MetadataObjectType> = cameraOutputCapability.supportedMetadataObjectTypes;
    3.   let metadataOutput: camera.MetadataOutput | undefined = undefined;
    4.   try {
    5.     metadataOutput = cameraManager.createMetadataOutput(metadataObjectTypes);
    6.   } catch (error) {
    7.     let err = error as BusinessError;
    8.     console.error(`Failed to createMetadataOutput, error code: ${err.code}`);
    9.   }
    10.   return metadataOutput;
    11. }
    
3. 调用[Session.start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#start11)方法开启metadata数据输出，再通过监听事件metadataObjectsAvailable回调拿到数据，接口调用失败时，会返回相应错误码，错误码类型参见[Camera错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraerrorcode)。
    
    previewOutput获取方式请参考[相机预览开发步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-preview#%E5%BC%80%E5%8F%91%E6%AD%A5%E9%AA%A4)。
    
    1. async function startMetadataOutput(previewOutput: camera.PreviewOutput, metadataOutput: camera.MetadataOutput, cameraManager: camera.CameraManager): Promise<void> {
    2.   let cameraArray: Array<camera.CameraDevice> = [];
    3.   try {
    4.     cameraArray = cameraManager.getSupportedCameras();
    5.     if (cameraArray.length == 0) {
    6.       console.error('no camera.');
    7.       return;
    8.     }
    9.     // 示例代码默认选择第一个镜头，实际开发需根据所需镜头。
    10.     const cameraDevice: camera.CameraDevice = cameraArray[0];
    11.     // 获取支持的模式类型。
    12.     let sceneModes: Array<camera.SceneMode> = cameraManager.getSupportedSceneModes(cameraDevice);
    13.     let isSupportPhotoMode: boolean = sceneModes.indexOf(camera.SceneMode.NORMAL_PHOTO) >= 0;
    14.     if (!isSupportPhotoMode) {
    15.       console.error('photo mode not support');
    16.       return;
    17.     }
    18.     let cameraInput: camera.CameraInput | undefined = undefined;
    19.     cameraInput = cameraManager.createCameraInput(cameraDevice);
    20.     if (cameraInput === undefined) {
    21.       console.error('cameraInput is undefined');
    22.       return;
    23.     }
    24.     // 打开相机。
    25.     await cameraInput.open();
    26.     let session = cameraManager.createSession(camera.SceneMode.NORMAL_PHOTO);
    27.     if (!session) {
    28.       console.error('session is null');
    29.       return;
    30.     }
    31.     let photoSession: camera.PhotoSession = session as camera.PhotoSession;
    32.     photoSession.beginConfig();
    33.     photoSession.addInput(cameraInput);
    34.     photoSession.addOutput(previewOutput);
    35.     photoSession.addOutput(metadataOutput);
    36.     await photoSession.commitConfig();
    37.     await photoSession.start();
    38.   } catch (error) {
    39.     console.error('startMetadataOutput call failed');
    40.   }
    41. }
    
4. 调用[Session.stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#stop11)方法停止输出metadata数据，接口调用失败会返回相应错误码，错误码类型参见[Camera错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraerrorcode)。
    
    1. function stopMetadataOutput(session: camera.Session): void {
    2.   session.stop().then(() => {
    3.     console.info('Callback returned with session stopped.');
    4.   }).catch((err: BusinessError) => {
    5.     console.error(`Failed to session stop, error code: ${err.code}`);
    6.   });
    7. }
    

## 状态监听

在相机应用开发过程中，可以随时监听metadata数据以及输出流的状态。

- 通过注册监听获取metadata对象，监听事件固定为metadataObjectsAvailable。检测到有效metadata数据时，callback返回相应的metadata数据信息，metadataOutput创建成功时可监听。
    
    1. function onMetadataObjectsAvailable(metadataOutput: camera.MetadataOutput): void {
    2.   metadataOutput.on('metadataObjectsAvailable', (err: BusinessError, metadataObjectArr: Array<camera.MetadataObject>) => {
    3.     if (err !== undefined && err.code !== 0) {
    4.       return;
    5.     }
    6.     console.info('metadata output metadataObjectsAvailable');
    7.   });
    8. }
    
    说明
    
    当前的元数据类型仅支持人脸检测（FACE_DETECTION）功能。元数据信息对象为识别到的人脸区域的矩形信息（Rect），包含矩形区域的左上角x坐标、y坐标和矩形的宽高数据。
    
- 通过注册回调函数，获取监听metadata流的错误结果，callback返回metadata输出接口使用错误时返回的错误码，错误码类型参见[Camera错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraerrorcode)。
    
    1. function onMetadataError(metadataOutput: camera.MetadataOutput): void {
    2.   metadataOutput.on('error', (metadataOutputError: BusinessError) => {
    3.     console.error(`Metadata output error code: ${metadataOutputError.code}`);
    4.   });
    5. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-recording-case "录像实践(ArkTS)")
# 元数据(ArkTS)

更新时间: 2025-12-16 16:35

在开发相机应用时，需要先[申请相关权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-preparation)。

元数据（Metadata）是对相机返回的图像信息的描述和上下文。针对图像信息，提供更详细的数据，如照片或视频中，识别人像的取景框坐标的信息等。

Metadata主要是通过一个TAG（Key），去找对应的Data，用于传递参数和配置信息，减少内存拷贝操作。

## 适用场景

检测图片中的人脸，返回高精度的人脸矩形框坐标。应用可基于人脸定位结果，灵活集成后处理算法，将其应用于多样化场景。

## 开发步骤

详细的API说明请参考[Camera API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera)。

1. 导入相关接口，导入方法如下。
    
    1. import { camera } from '@kit.CameraKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 调用[CameraOutputCapability](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#cameraoutputcapability)中的supportedMetadataObjectTypes属性，获取当前设备支持的元数据类型，并通过[createMetadataOutput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#createmetadataoutput)方法创建元数据输出流。
    
    1. function getMetadataOutput(cameraManager: camera.CameraManager, cameraOutputCapability: camera.CameraOutputCapability): camera.MetadataOutput | undefined {
    2.   let metadataObjectTypes: Array<camera.MetadataObjectType> = cameraOutputCapability.supportedMetadataObjectTypes;
    3.   let metadataOutput: camera.MetadataOutput | undefined = undefined;
    4.   try {
    5.     metadataOutput = cameraManager.createMetadataOutput(metadataObjectTypes);
    6.   } catch (error) {
    7.     let err = error as BusinessError;
    8.     console.error(`Failed to createMetadataOutput, error code: ${err.code}`);
    9.   }
    10.   return metadataOutput;
    11. }
    
3. 调用[Session.start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#start11)方法开启metadata数据输出，再通过监听事件metadataObjectsAvailable回调拿到数据，接口调用失败时，会返回相应错误码，错误码类型参见[Camera错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraerrorcode)。
    
    previewOutput获取方式请参考[相机预览开发步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-preview#%E5%BC%80%E5%8F%91%E6%AD%A5%E9%AA%A4)。
    
    1. async function startMetadataOutput(previewOutput: camera.PreviewOutput, metadataOutput: camera.MetadataOutput, cameraManager: camera.CameraManager): Promise<void> {
    2.   let cameraArray: Array<camera.CameraDevice> = [];
    3.   try {
    4.     cameraArray = cameraManager.getSupportedCameras();
    5.     if (cameraArray.length == 0) {
    6.       console.error('no camera.');
    7.       return;
    8.     }
    9.     // 示例代码默认选择第一个镜头，实际开发需根据所需镜头。
    10.     const cameraDevice: camera.CameraDevice = cameraArray[0];
    11.     // 获取支持的模式类型。
    12.     let sceneModes: Array<camera.SceneMode> = cameraManager.getSupportedSceneModes(cameraDevice);
    13.     let isSupportPhotoMode: boolean = sceneModes.indexOf(camera.SceneMode.NORMAL_PHOTO) >= 0;
    14.     if (!isSupportPhotoMode) {
    15.       console.error('photo mode not support');
    16.       return;
    17.     }
    18.     let cameraInput: camera.CameraInput | undefined = undefined;
    19.     cameraInput = cameraManager.createCameraInput(cameraDevice);
    20.     if (cameraInput === undefined) {
    21.       console.error('cameraInput is undefined');
    22.       return;
    23.     }
    24.     // 打开相机。
    25.     await cameraInput.open();
    26.     let session = cameraManager.createSession(camera.SceneMode.NORMAL_PHOTO);
    27.     if (!session) {
    28.       console.error('session is null');
    29.       return;
    30.     }
    31.     let photoSession: camera.PhotoSession = session as camera.PhotoSession;
    32.     photoSession.beginConfig();
    33.     photoSession.addInput(cameraInput);
    34.     photoSession.addOutput(previewOutput);
    35.     photoSession.addOutput(metadataOutput);
    36.     await photoSession.commitConfig();
    37.     await photoSession.start();
    38.   } catch (error) {
    39.     console.error('startMetadataOutput call failed');
    40.   }
    41. }
    
4. 调用[Session.stop](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-session#stop11)方法停止输出metadata数据，接口调用失败会返回相应错误码，错误码类型参见[Camera错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraerrorcode)。
    
    1. function stopMetadataOutput(session: camera.Session): void {
    2.   session.stop().then(() => {
    3.     console.info('Callback returned with session stopped.');
    4.   }).catch((err: BusinessError) => {
    5.     console.error(`Failed to session stop, error code: ${err.code}`);
    6.   });
    7. }
    

## 状态监听

在相机应用开发过程中，可以随时监听metadata数据以及输出流的状态。

- 通过注册监听获取metadata对象，监听事件固定为metadataObjectsAvailable。检测到有效metadata数据时，callback返回相应的metadata数据信息，metadataOutput创建成功时可监听。
    
    1. function onMetadataObjectsAvailable(metadataOutput: camera.MetadataOutput): void {
    2.   metadataOutput.on('metadataObjectsAvailable', (err: BusinessError, metadataObjectArr: Array<camera.MetadataObject>) => {
    3.     if (err !== undefined && err.code !== 0) {
    4.       return;
    5.     }
    6.     console.info('metadata output metadataObjectsAvailable');
    7.   });
    8. }
    
    说明
    
    当前的元数据类型仅支持人脸检测（FACE_DETECTION）功能。元数据信息对象为识别到的人脸区域的矩形信息（Rect），包含矩形区域的左上角x坐标、y坐标和矩形的宽高数据。
    
- 通过注册回调函数，获取监听metadata流的错误结果，callback返回metadata输出接口使用错误时返回的错误码，错误码类型参见[Camera错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-e#cameraerrorcode)。
    
    1. function onMetadataError(metadataOutput: camera.MetadataOutput): void {
    2.   metadataOutput.on('error', (metadataOutputError: BusinessError) => {
    3.     console.error(`Metadata output error code: ${metadataOutputError.code}`);
    4.   });
    5. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-recording-case "录像实践(ArkTS)")
