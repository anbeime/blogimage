# Preview Kit简介

更新时间: 2025-12-16 16:35

Preview Kit（文件预览服务）为应用提供便捷的文件快速预览和文件打开加速能力。

- 应用可以通过Preview Kit提供的预览API，快速启动预览界面，实现对各类文件的预览。
    
    通过Preview Kit，用户可以对用户文件（包括图片、视频、音频、文本、html等）进行内容查看。同时用户还可以通过点击右上角的“使用其他应用打开”的按钮跳转到具体的应用进行展示，从而进行其他操作，如图片的旋转、放大等。
    
    目前，Preview Kit实现Office的预览能力，主要是借助WPS的能力实现的，预览界面会有WPS提供的技术支持，并展示WPS的入口，统一按照文件预览的风格进行页面布局。
    
- Preview Kit还提供了文件打开加速功能，通常用户打开一个较大文件通常要花费几秒甚至十几秒，文件打开加速服务提供了预加载机制提前加载文件，缩短用户打开文件时间，给用户提供流畅顺滑的爽感体验。详见[文件打开加速功能](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-openfileboost)。

## 文件预览场景介绍

Preview Kit能够对图片、视频、音频、文本、html进行预览查看，满足绝大多数办公开发的需求，包括：

- 预览展示：呈现文件的基本内容，如文本、图片等，支持选中多文件，在预览列表切换显示。
- 文件分享：将文件以分享的形式传给另一个软件。
- 使用其他软件打开：使用预览打开时，会获取到该文件类型的默认打开软件，然后点击“使用其他应用打开”进行跳转。
- 图片翻转放大：在非2in1设备时，预览能够对图片进行旋转放大等处理。

## 文件打开加速场景介绍

文档类应用接入后，文件打开加速服务会根据算法推荐用户可能打开的文件信息给应用，应用可提前在后台对文件进行预加载， 一旦用户打开已经预加载的文件，则整个打开过程可以在很短时间内完成。给用户提供顺滑流畅的文件打开体验。

## 约束与限制

### 支持的国家和地区

当前Preview Kit仅支持中国境内（不包含中国香港、中国澳门、中国台湾）。

### 支持的设备

当前Preview Kit支持模拟器开发，但与真机存在部分能力差异，详情请参考[模拟器与真机的差异](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-specification#section38231424133213)列表。

文件预览功能支持华为Phone、Tablet和2in1，文件打开加速功能仅支持2in1设备。

## 文件预览支持的文件类型

Preview Kit支持图片、视频、音频、文本、html进行查看，表中提供的为常见的部分格式类型，实际支持情况可采用[canPreview](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/preview-arkts#section3643113161616)接口进行判断文件是否支持预览。

|类型|文件后缀|mimeType类型|
|:--|:--|:--|
|文本|txt、cpp、c、h、java、xhtml、xml|text/plain、text/x-c++src、text/x-csrc、text/x-chdr、text/x-java、application/xhtml+xml、text/xml|
|网页|html、htm|text/html|
|图片|jpg、png、gif、webp、bmp、svg|image/jpeg、image/png、image/gif、image/webp、image/bmp、image/svg+xml|
|音频|m4a、aac、mp3、ogg、wav|audio/mp4a-latm、audio/aac、audio/mpeg、audio/ogg、audio/x-wav|
|视频|mp4、mkv、ts|video/mp4、video/x-matroska、video/mp2ts|
|文件夹|无|无|
|文档|pdf|application/pdf|
|Office文档|doc、docx、xls、xlsx、ppt、pptx、csv、ofd|application/msword、application/vnd.openxmlformats-officedocument.wordprocessingml.document、application/vnd.ms-excel、application/vnd.openxmlformats-officedocument.spreadsheetml.sheet、application/vnd.ms-powerpoint、application/vnd.openxmlformats-officedocument.presentationml.presentation、text/csv、general.ofd|

## 文件打开加速支持的文件类型

后缀为doc、docx、xls、xlsx、ppt、pptx的文件。

## 文件预览基本概念

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163559.61882688712714544470200463997956:50001231000000:2800:886C1582C204D4AA63AB41367E033A42DC49FD5C88C331BBD27A30A7689E4745.png)

- 模态窗：和父窗口绑定，模态窗存在时父窗口不可移动，不可操作，模态窗永远置于父窗口前面。
- 应用窗：应用窗口，可以通过AMS启动。
- AMS：AbilityManagerService，用于协调各Ability运行关系、及对生命周期进行调度的系统服务。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-kit-guide "Preview Kit（文件预览服务）")
# 文件预览

更新时间: 2025-12-16 16:36

当前Preview Kit的文件预览能力采用拉起新窗口的方式来实现，在新的窗口中展示需要预览的文件，并按照统一设计的界面进行展示，如果开发者需要使用Preview Kit的文件预览能力，需要注意以下事项：

- 当前Preview Kit仅支持跳出应用进行文件的预览，暂不支持应用内预览。
- Office类型文档预览借助WPS提供的能力来实现，在预览文档类型文件时会存在”WPS提供技术支持”、”使用WPS Office打开”等相关字样。
- 当前Preview Kit暂不支持安全定制能力，包括禁止截录屏、屏蔽其他应用打开入口、屏蔽分享入口等安全预览能力。
- 当前Preview Kit需要调用方存在对应uri的转授权能力，从而让预览获得该文件的访问权限来正常读取文件，具体问题可以参考[Preview Kit常见问题2](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-faq-2)。

## 接口说明

接口返回值有两种返回形式：callback和promise，promise和callback只是返回值方式不一样，功能相同。具体API说明详见[接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/preview-arkts)。

**表1** Preview Kit的接口介绍
|接口名|描述|
|:--|:--|
|openPreview(context: Context, file: PreviewInfo, info?: DisplayInfo): Promise<void>|打开预览功能。通过传入单个文件预览信息以及悬浮窗口属性信息，打开预览窗口。1秒内重复调用无效。使用Promise方式异步返回结果。|
|openPreview(context: Context, file: PreviewInfo, info: DisplayInfo, callback: AsyncCallback<void>): void|打开预览功能。通过传入单个文件预览信息以及悬浮窗口属性信息，打开预览窗口。1秒内重复调用无效。传入callback进行异步回调。|
|openPreview(context: Context, files: Array<PreviewInfo>, index?: number): Promise<void>|打开预览功能。通过传入多个文件预览信息以及选择展示的文件信息下标，打开预览窗口。1秒内重复调用无效。使用Promise方式异步返回结果。仅移动端可用。|
|canPreview(context: Context, uri: string): Promise<boolean>|根据文件的uri判断文件是否可预览。<br><br>- 当传入支持的文件类型（图片、视频、音频、文本、html）并且文件存在时，会返回true。<br>- 当传入不可预览的文件uri时，返回false。|
|hasDisplayed(context: Context): Promise<boolean>|判断预览窗口是否已经存在。预览窗口是单例的形式。<br><br>- 如果预览窗口已经打开过并且没关闭，那会返回true。<br>- 如果没打开或者打开后已关闭，那将返回false。|
|closePreview(context: Context): Promise<void>|关闭预览窗口，仅当预览窗口存在时起效。|
|loadData(context: Context, file: PreviewInfo): Promise<void>|加载预览文件信息。仅当预览窗口存在时生效。100毫秒内重复调用无效。<br><br>- 传入可预览文件时展示对应预览界面。<br>- 传入不可预览文件显示不支持预览界面。|

## 开发步骤

1. 导入相关模块。
    
    1. import { filePreview } from '@kit.PreviewKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 判断是否可以预览。
    
    1. let uri = 'file://docs/storage/Users/currentUser/Documents/1.txt';  
    2. let uiContext = this.getUIContext().getHostContext() as Context;
    3. filePreview.canPreview(uiContext, uri).then((result) => {    // 传入支持的文件类型且文件存在时会返回true
    4.   console.info(`Succeeded in obtaining the result of whether it can be previewed. result = ${result}`);
    5. }).catch((err: BusinessError) => {
    6.   console.error(`Failed to obtain the result of whether it can be previewed, err.code = ${err.code}, err.message = ${err.message}`);
    7. });
    
3. 调用openPreview，实现打开文件预览的功能。
    
    - 通过Promise方式打开文件
        
        1. let uiContext = this.getUIContext().getHostContext() as Context;
        2. let displayInfo: filePreview.DisplayInfo = {
        3.   x: 100,
        4.   y: 100,
        5.   width: 800,
        6.   height: 800
        7. };
        8. let fileInfo: filePreview.PreviewInfo = {
        9.   title: '1.txt',
        10.   uri: 'file://docs/storage/Users/currentUser/Documents/1.txt',
        11.   mimeType: 'text/plain'
        12. };
        13. filePreview.openPreview(uiContext, fileInfo, displayInfo).then(() => {
        14.   console.info('Succeeded in opening preview');
        15. }).catch((err: BusinessError) => {
        16.   console.error(`Failed to open preview, err.code = ${err.code}, err.message = ${err.message}`);
        17. });
        
    
    - 通过CallBack回调函数方式打开文件
        
        1. let uiContext = this.getUIContext().getHostContext() as Context;
        2. let displayInfo: filePreview.DisplayInfo = {
        3.   x: 100,
        4.   y: 100,
        5.   width: 800,
        6.   height: 800
        7. };
        8. let fileInfo: filePreview.PreviewInfo = {
        9.   title: '1.txt',
        10.   uri: 'file://docs/storage/Users/currentUser/Documents/1.txt',
        11.   mimeType: 'text/plain'
        12. };
        13. filePreview.openPreview(uiContext, fileInfo, displayInfo, (err) => {
        14.   if (err && err.code) {
        15.     console.error(`Failed to open preview, err.code = ${err.code}, err.message = ${err.message}`);    
        16.     return;
        17.   }
        18.   console.info('Succeeded in opening preview');
        19. });
        
    - 传入多个文件打开预览，仅移动端可用。
        
        1. let uiContext = this.getUIContext().getHostContext() as Context;
        2. let fileInfo: filePreview.PreviewInfo = {
        3.   title: '1.txt',
        4.   uri: 'file://docs/storage/Users/currentUser/Documents/1.txt',
        5.   mimeType: 'text/plain'
        6. };
        7. let fileInfo1: filePreview.PreviewInfo = {
        8.   title: '2.txt',
        9.   uri: 'file://docs/storage/Users/currentUser/Documents/2.txt',
        10.   mimeType: 'text/plain'
        11. };
        12. let files: Array<filePreview.PreviewInfo> = new Array();
        13. files.push(fileInfo);
        14. files.push(fileInfo1);
        15. filePreview.openPreview(uiContext, files, 0).then(() => {
        16.   console.info('Succeeded in opening preview');
        17. }).catch((err: BusinessError) => {
        18.   console.error(`Failed to open preview, err.code = ${err.code}, err.message = ${err.message}`);
        19. });
        
4. （可选）如果已经打开过预览窗口，需要重新加载页面，需要调用loadData接口，加载文件。
    
    1. let uiContext = this.getUIContext().getHostContext() as Context;
    2. let fileInfo: filePreview.PreviewInfo = {
    3.   title: '2.txt',
    4.   uri: 'file://docs/storage/Users/currentUser/Documents/2.txt',
    5.   mimeType: 'text/plain'
    6. };
    7. filePreview.loadData(uiContext, fileInfo).then(() => {   // 仅当预览窗口存在时起效
    8.   console.info('Succeeded in loading data.');
    9. }).catch((err: BusinessError) => {
    10.   console.error(`Failed to load data, err.code = ${err.code}, err.message = ${err.message}`);
    11. });
    
5. （可选）如果想要关闭预览窗口，需要调用closePreview。
    
    1. let uiContext = this.getUIContext().getHostContext() as Context;
    2. filePreview.closePreview(uiContext).then(() => {   // 仅当预览窗口存在时起效
    3.   console.info('Succeeded in closing preview');
    4. }).catch((err: BusinessError) => {
    5.   console.error(`Failed to close preview, err.code = ${err.code}, err.message = ${err.message}`);
    6. });
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-introduction "Preview Kit简介")
# 文件打开加速状态感知

更新时间: 2025-12-16 16:36

从5.0.5(17)版本开始，如浏览器等支持下载文件的应用，可以接入文件预加载状态感知接口，动态感知文件预加载状态，通过UI（user interface）标识对加速文件进行显性化提示，进一步提升用户体验。

## 接口说明

具体API说明详见[预加载状态感知接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/preview-arkts-openfileboost-api)。

**表1** 文件预加载状态感知接口介绍（ArkTS API）
|接口名|描述|
|:--|:--|
|on(type: 'filePreloadStateChanged', callback: Callback<FilePreloadStatusInfo>): void|文件预加载状态回调，应用通过注册回调函数获取文件预加载的状态变化。|
|off(type: 'filePreloadStateChanged', callback?: Callback<FilePreloadStatusInfo>): void|文件预加载状态注销回调，通过注销回调函数取消获取文件预加载的状态变化。|
|addFile(file: string): void|监听一个文件的预加载状态，传入文件路径开始监听该文件的预加载状态。后续该文件状态有变化通过'filePreloadStateChanged'事件回调应用。<br><br>注意需要先调用openFileBoost.on('filePreloadStateChanged')接口后再调用该接口添加文件。<br><br>当前支持加速的文件类型见[文件打开加速支持的文件类型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-introduction#section7910758192912)， 不支持的文件类型默认为未预加载状态，不需要调用该接口监听文件预加载状态变更。|
|removeFile(file: string): void|取消监听一个文件的预加载状态，取消后文件的预加载状态变化不会通过回调再通知业务。|
|queryFilePreloadStatusInfo(file: string): FilePreloadStatusInfo|查询文件预加载状态，传入文件路径，通过返回值返回该文件当前的预加载状态。|

## 开发准备

需要先通过[Syscap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/syscap#%E5%88%A4%E6%96%AD-api-%E6%98%AF%E5%90%A6%E5%8F%AF%E4%BB%A5%E4%BD%BF%E7%94%A8)查询您的目标设备是否支持SystemCapability.PCService.OpenFileBoost系统能力，当前仅在2in1设备上支持该能力。

## 开发步骤

1. 导入相关模块。
    
    1. import { openFileBoost } from '@kit.PreviewKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    
2. 注册文件预加载状态感知回调函数。
    
    1. // 文件预加载状态变更的回调函数定义，若有文件预加载状态变更，则通过该回调函数通知
    2. function callback(filePreloadStatusInfo: openFileBoost.FilePreloadStatusInfo): void {
    3.   if (filePreloadStatusInfo.state === openFileBoost.FilePreloadState.PRELOADING) {
    4.     // 预加载过程中，应用可以根据自己设计对应UX
    5.     hilog.info(0x0000, 'testTag', `file is PRELOADING, suggest to show loading animation`);
    6.   }
    7.   if (filePreloadStatusInfo.state === openFileBoost.FilePreloadState.PRELOADED) {
    8.     // 预加载完成，应用可以通过UX显示提示用户加速完成
    9.     hilog.info(0x0000, 'testTag', `file is PRELOADED, suggest to show loaded animation`);
    10.   }
    11.   if (filePreloadStatusInfo.state === openFileBoost.FilePreloadState.NOT_PRELOADED) {
    12.     // 没有预加载，应用可以不显示任何额外UX
    13.     hilog.info(0x0000, 'testTag', `file is UNPRELOADED, suggest do not show animation `);
    14.   }
    15. }
    16. // 调用register函数可以注册预加载状态感知回调
    17. function register(): void {
    18.   try {
    19.     openFileBoost.on('filePreloadStateChanged', callback);
    20.   } catch(error) {
    21.     let code = (error as BusinessError).code;
    22.     let message = (error as BusinessError).message;
    23.     hilog.error(0x0000, 'testTag', `register filePreloadStateChanged failed, error code: ${code}, message: ${message}.`);
    24.   }
    25. }
    
3. 调用addFile接口传入想要监听的文件的沙箱路径。典型场景比如应用下载某个文件完成，可将该文件路径注册进来，若文件后续状态变更，系统会通过[2](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-openfileboost-stateawareness#zh-cn_topic_0000002232379348_li13424101995516)中的回调函数通知应用。
    
    1. // 为10MB_file.docx文件添加文件预加载状态监听
    2. function testAddFile(): void {
    3.   try {
    4.     const file:string = "/storage/Users/currentUser/Desktop/10MB_file.docx";
    5.     openFileBoost.addFile(file);
    6.   } catch(error) {
    7.     let code = (error as BusinessError).code;
    8.     let message = (error as BusinessError).message;
    9.     hilog.error(0x0000, 'testTag', `addFile failed, error code: ${code}, message: ${message}.`);
    10.   }
    11. }
    
4. 通过addFile接口监听的文件个数有上限（50个文件），不再需要监听的文件可以通过removeFile接口取消监听。
    
    1. const file:string = "/storage/Users/currentUser/Desktop/10MB_file.docx";
    2. try {
    3.   openFileBoost.removeFile(file);
    4. } catch(error) {
    5.   let code = (error as BusinessError).code;
    6.   let message = (error as BusinessError).message;
    7.   hilog.error(0x0000, 'testTag', `removeFile failed, error code: ${code}, message: ${message}.`);
    8. }
    
5. 如果不需要再监听任何文件的预加载状态变更，可注销预加载状态感知回调函数。如果传入具体的回调函数，则只取消该函数； 如果不传入具体的回调函数，则取消该进程的所有回调。
    
    1. // 假设之前在进程的不同业务逻辑中已经注册了callback1、callback2、callback3总共3个回调函数
    2. openFileBoost.on('filePreloadStateChanged', callback1);
    3. openFileBoost.on('filePreloadStateChanged', callback2);
    4. openFileBoost.on('filePreloadStateChanged', callback3);
    
    5. function testUnregister(): void {
    6.   try {
    7.     // 单独取消callback1的监听，传入callback1作为参数，后续不会再调用callback1的回调做通知
    8.     openFileBoost.off('filePreloadStateChanged', callback1);
    9.     // 取消所有callback的监听，不传第二个可选参数，后续不会再调用callback2和callback3做通知
    10.     openFileBoost.off('filePreloadStateChanged');
    11.   } catch(error) {
    12.     let code = (error as BusinessError).code;
    13.     let message = (error as BusinessError).message;
    14.     hilog.error(0x0000, 'testTag', `off filePreloadStateChanged failed, error code: ${code}, message: ${message}.`);
    15.   }
    16. }
    
6. 应用还可通过查询接口查询某个文件的实时的预加载状态，一般在应用刚启动时可以查询一遍相关文件的预加载状态。每次调用接口传入一个文件的沙箱路径。
    
    1. function testQuery(): void {
    2. try {
    3.   const file:string = "/storage/Users/currentUser/Desktop/10MB_file.docx";
    4.   let statusInfo : openFileBoost.FilePreloadStatusInfo = openFileBoost.queryFilePreloadStatusInfo(file);
    5.   hilog.info(0x0000, 'testTag', 'file, %{public}s, progress:%{public}d  preloadState:%{public}d',
    6.     statusInfo.sandboxPath, statusInfo.progress, statusInfo.state);
    7. } catch(error) {
    8.   let code = (error as BusinessError).code;
    9.   let message = (error as BusinessError).message;
    10.   hilog.error(0x0000, 'testTag', `query failed, error code: ${code}, message: ${message}.`);
    11. }
    12. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-openfileboost "文件打开加速（C/C++）")
# openPreview打开显示预览失败

更新时间: 2025-12-16 16:36

Preview Kit的[openPreview](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/preview-arkts#section144826162913)接口在传入文件预览信息时，当前仅支持传入文件的[uri](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/user-file-uri-intro)，不支持传入文件的沙箱路径。

如果调用openPreview接口后，显示预览失败，请检查传入的是否为uri并且检查传入的uri是否存在。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-faq "Preview Kit常见问题")
# 使用DocumentViewPicker拿到的uri通过openPreview打开显示预览失败

更新时间: 2025-12-16 16:36

DocumentViewPicker拿到的文件uri应用仅有临时权限，该权限无法分享给预览，导致预览失败。可先对uri[持久化权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/file-persistpermission)，然后再采用openPreview打开文件；或者可以先将文件拷贝至应用沙箱内，再预览沙箱内文件。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-faq-1 "openPreview打开显示预览失败")
