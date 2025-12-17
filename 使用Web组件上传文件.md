# 使用Web组件上传文件

更新时间: 2025-12-16 16:38

Web组件支持前端页面选择文件上传功能，应用开发者可以使用[onShowFileSelector()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onshowfileselector9)接口来处理前端页面文件上传的请求，如果应用开发者不做任何处理，Web会提供默认行为来处理前端页面文件上传的请求。

## 使用onShowFileSelector拉起文件管理器

下面的示例中，当用户在前端页面点击文件上传按钮，应用侧在[onShowFileSelector()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onshowfileselector9)接口中收到文件上传请求，在此接口中开发者将上传的本地文件路径设置给前端页面。

- 应用侧代码。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { picker } from '@kit.CoreFileKit';
    
    5. @Entry
    6. @Component
    7. struct WebComponent {
    8.   controller: webview.WebviewController = new webview.WebviewController();
    
    9.   build() {
    10.     Column() {
    11.       Web({ src: $rawfile('local.html'), controller: this.controller })
    12.         .onShowFileSelector((event) => {
    13.           console.info('MyFileUploader onShowFileSelector invoked');
    14.           const documentSelectOptions = new picker.DocumentSelectOptions();
    15.           let uri: string | null = null;
    16.           const documentViewPicker = new picker.DocumentViewPicker();
    17.           documentViewPicker.select(documentSelectOptions).then((documentSelectResult) => {
    18.             uri = documentSelectResult[0];
    19.             console.info('documentViewPicker.select to file succeed and uri is:' + uri);
    20.             if (event) {
    21.               event.result.handleFileList([uri]);
    22.             }
    23.           }).catch((err: BusinessError) => {
    24.             console.error(`Invoke documentViewPicker.select failed, code is ${err.code}, message is ${err.message}`);
    25.           })
    26.           return true;
    27.         })
    28.     }
    29.   }
    30. }
    
- local.html页面代码。
    
    1. <!DOCTYPE html>
    2. <html>
    3. <head>
    4.     <meta charset="utf-8">
    5.     <meta name="viewport" content="width=device-width" />
    6.     <title>Document</title>
    7. </head>
    
    8. <body>
    9. <!-- 点击上传文件按钮 -->
    10. <input type="file"><br>
    11. </body>
    12. </html>
    

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163827.11533442547526673834794939386706:50001231000000:2800:A42FCB19C018CDCFCAC975B2AFF8A93B2D4A80DCF7B231AD7D7A310C8D1DDDA5.gif)

## 使用onShowFileSelector拉起图库

下面的示例中，当用户在前端页面点击文件上传按钮，应用侧在[onShowFileSelector()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onshowfileselector9)接口中收到文件上传请求，在此接口中开发者将上传的本地图片路径设置给前端页面。

- 应用侧代码。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { photoAccessHelper } from '@kit.MediaLibraryKit';
    
    4. @Entry
    5. @Component
    6. struct WebComponent {
    7.   controller: webview.WebviewController = new webview.WebviewController();
    
    8.   async selectFile(result: FileSelectorResult): Promise<void> {
    9.     let photoSelectOptions = new photoAccessHelper.PhotoSelectOptions();
    10.     let photoPicker = new photoAccessHelper.PhotoViewPicker();
    11.     // 过滤选择媒体文件类型为IMAGE_VIDEO
    12.     photoSelectOptions.MIMEType = photoAccessHelper.PhotoViewMIMETypes.IMAGE_VIDEO_TYPE;
    13.     // 设置最大选择数量
    14.     photoSelectOptions.maxSelectNumber = 5;
    15.     let chooseFile: photoAccessHelper.PhotoSelectResult = await photoPicker.select(photoSelectOptions);
    16.     // 获取选择的文件列表
    17.     result.handleFileList(chooseFile.photoUris);
    18.   }
    
    19.   build() {
    20.     Column() {
    21.       Web({ src: $rawfile('local.html'), controller: this.controller })
    22.         .onShowFileSelector((event) => {
    23.           if (event) {
    24.             this.selectFile(event.result);
    25.           }
    26.           return true;
    27.         })
    28.     }
    29.   }
    30. }
    
- local.html页面代码。
    
    1. <!DOCTYPE html>
    2. <html>
    3. <head>
    4.     <meta charset="utf-8">
    5.     <meta name="viewport" content="width=device-width" />
    6.     <title>Document</title>
    7. </head>
    
    8. <body>
    9. <!-- 点击上传文件按钮 -->
    10. <input type="file"><br>
    11. </body>
    12. </html>
    

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.81137244292651520512552027277292:50001231000000:2800:FFFEB6720542B80D7B0683DFB2EA62A3089DEABC8467A25079B0AB965E1886B0.gif)

## 使用onShowFileSelector拉起相机

Web组件支持前端页面上传图片文件时调用相机即时拍照，应用开发者可以使用[onShowFileSelector()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onshowfileselector9)接口来处理前端页面文件上传的请求并自行拉起相机，如果应用开发者不做任何处理，Web会提供默认行为来处理前端页面调用相机的请求。

此示例中，应用侧通过监听[onShowFileSelector](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onshowfileselector9)事件并返回true拦截ArkWeb默认弹窗,并调用系统CameraPicker拉起相机。

应用可以通过获取AcceptType对不同类型的目标文件做更精细的筛选。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { camera, cameraPicker } from '@kit.CameraKit';
4. import { BusinessError } from '@kit.BasicServicesKit';
5. import { common } from '@kit.AbilityKit';

6. async function openCamera(callback: Callback<string>, uiContext: UIContext) {
7.   let mContext = uiContext.getHostContext() as common.Context;
8.   try {
9.     let pickerProfile: cameraPicker.PickerProfile = {
10.       cameraPosition: camera.CameraPosition.CAMERA_POSITION_BACK
11.     };
12.     let pickerResult: cameraPicker.PickerResult = await cameraPicker.pick(mContext,
13.       [cameraPicker.PickerMediaType.PHOTO, cameraPicker.PickerMediaType.VIDEO], pickerProfile);
14.     callback(pickerResult.resultUri);
15.   } catch (error) {
16.     let err = error as BusinessError;
17.     console.error(`the pick call failed. error code: ${err.code}`);
18.   }
19. }

20. @Entry
21. @Component
22. struct Index {
23.   webviewController: webview.WebviewController = new webview.WebviewController();

24.   build() {
25.     Column() {
26.       Web({ src: $rawfile("webCamera.html"), controller: this.webviewController })
27.         .onShowFileSelector((event) => {
28.             //开发者可以通过event.fileSelector.getAcceptType()和event.fileSelector.isCapture()判断文件类型，并有选择地做出筛选以拉起不同的文件选择器
29.             openCamera((result) => {
30.                 if (event) {
31.                 console.info('Title is ' + event.fileSelector.getTitle());
32.                 console.info('Mode is ' + event.fileSelector.getMode());
33.                 console.info('Accept types are ' + event.fileSelector.getAcceptType());
34.                 console.info('Capture is ' + event.fileSelector.isCapture());
35.                 event.result.handleFileList([result]);
36.                 }
37.             }, this.getUIContext())
38.             return true;
39.         })
40.     }
41.     .height('100%')
42.     .width('100%')
43.   }
44. }

html页面代码

1. <!DOCTYPE html>
2. <html lang="en">
3. <head>
4.     <meta charset="UTF-8">
5.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
6.     <title>WebCamera</title>
7. </head>
8. <body>
9.     <input type="file" name="photo" id="photo"><br>
10.     <img style="display: none;width:200px;" id="img">
11.     <script>
12.         let photo = document.getElementById("photo");
13.         photo.addEventListener("change", preViewImg)

14.         function preViewImg(event) {
15.             let fileReader = new FileReader();
16.             let img = document.getElementById("img");
17.             fileReader.addEventListener(
18.                 "load",
19.                 () => {
20.                     // 将图像文件转换为 Base64 字符串
21.                     img.src = fileReader.result;
22.                     img.style.display = "block";
23.                 },
24.                 false
25.             );
26.             if (event.target.files && event.target.files[0]) {
27.               fileReader.readAsDataURL(event.target.files[0]);
28.             } else {
29.               console.error("File not exist.");
30.             }
31.         }
32.     </script>
33. </body>
34. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.56837460456339123773600331597716:50001231000000:2800:360B3FD238A14761F77DF604A991334FED894F829CE802EAEC223416B0E9D701.gif)

## 使用ArkWeb默认的方式处理文件上传请求

accept 属性是一个字符串，它定义了文件 input 应该接受的文件类型。这个字符串是一个以逗号为分隔的唯一文件类型说明符列表。由于给定的文件类型可以用多种方式指定，因此当你需要给定格式的文件时，提供一组完整的类型指定符是非常有用的。

capture 属性是一个字符串，如果 accept 属性指出了 input 是图片或者视频类型，则它指定了使用哪个摄像头去获取这些数据。值 user 表示应该使用前置摄像头和（或）麦克风。值 environment 表示应该使用后置摄像头和（或）麦克风。如果缺少此属性，则用户代理可以自由决定做什么。如果请求的前置模式不可用，则用户代理可能退回到其首选的默认模式。

当指定布尔类型属性 multiple 时，文件 input 允许用户选择多个文件。

示例页面内有数个文件选择器，分别设置了不同的accept及capture属性，这两个属性对相机的影响如下：

|accept|capture|文件选择器行为|
|:--|:--|:--|
|仅包含图片类型|设置为"environment"或"user"|直接拉起相机拍照模式。|
|仅包含图片类型|不设置|先拉起弹窗，用户选择拍照后拉起相机拍照模式。|
|仅包含视频类型|设置为"environment"或"user"|直接拉起相机录像模式。|
|仅包含视频类型|不设置|先拉起弹窗，用户选择拍照后拉起相机录像模式。|
|包含图片和视频类型|设置为"environment"或"user"|直接拉起相机拍照模式，可录像。|
|包含图片和视频类型|不设置|先拉起弹窗，用户选择拍照后拉起相机拍照模式，可录像。|
|不设置图片或视频类型|设置为"environment"或"user"|直接拉起相机拍照模式，可录像。|
|不设置图片或视频类型|不设置|先拉起弹窗，用户选择拍照后拉起相机拍照模式，可录像。|
|不包含图片或视频类型|设置为"environment"或"user"|直接拉起文件选择，不可拉起相机。|
|不包含图片或视频类型|不设置|直接拉起文件选择，不可拉起相机。|

当前ArkWeb识别的文件类型有

- 图片：tif, xbm, tiff, pjp, jfif, bmp, avif, apng, ico, webp, svg, gif, svgz, jpg, jpeg, png, pjpeg
- 视频：mp4, mpg, mpeg, m4v, ogm, ogv, webm

说明

ArkWeb默认仅拉起相机后置摄像头，值 'user'不会被处理成拉起前置摄像头。如有需要，请在应用侧通过[onShowFileSelector()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onshowfileselector9)接口另行处理

html页面代码

1. <!DOCTYPE html>
2. <html lang="en">
3. <head>
4.     <meta charset="UTF-8">
5.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
6.     <title>WebCamera</title>
7. </head>
8. <body>
9.     <input type="file" name="picture" id="picture" accept="image/*"><br>
10.     <img style="display: none;width:200px" id="img">
11.     <script>
12.         let picture = document.getElementById("picture");
13.         picture.addEventListener("change", preViewImg)

14.         function preViewImg(event) {
15.             let fileReader = new FileReader();
16.             let img = document.getElementById("img");
17.             fileReader.addEventListener(
18.                 "load",
19.                 () => {
20.                     // 将图像文件转换为 Base64 字符串
21.                     img.src = fileReader.result;
22.                     img.style.display = "block";
23.                 },
24.                 false
25.             );
26.             if (event.target.files && event.target.files[0]) {
27.               fileReader.readAsDataURL(event.target.files[0]);
28.             } else {
29.               console.error("File not exist.");
30.             }
31.         }
32.     </script>
33. </body>
34. </html>

应用侧代码

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct Index {
6.   webviewController: webview.WebviewController = new webview.WebviewController();

7.   build() {
8.     Column() {
9.       Web({ src: $rawfile("webCamera.html"), controller: this.webviewController })
10.     }
11.     .height('100%')
12.     .width('100%')
13.   }
14. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163828.10436971365051070025372358290098:50001231000000:2800:F3CA2EA9A9B77917EE36AB95DD69E0F4C8933F7A3769748E5C1DC24610D9571F.gif)

## 常见问题

### onShowFileSelector配合ArkWeb默认弹窗使用

用户点击文件上传按钮后，程序优先执行onShowFileSelector中的回调进行逻辑处理，应用开发者可以根据处理结果选择 return false; ，进而拉起ArkWeb默认弹窗，此时不推荐同时拉起应用侧各Picker。

### 回调中getAcceptType和getMimeTypes的区别

getAcceptType返回的是 accept 属性值全量转换为文件扩展名所组成的字符串数组，getMimeTypes返回的是 accept 属性值用逗号拆分后所组成的字符串数组。

如若 accept 属性值为 video/mp4, .png ，则getAcceptType返回 .mp4, .m4v; .png ，getMimeTypes返回 video/mp4; .png 。

### ArkWeb默认弹窗的说明

选项“图片”会拉起图库，根据 accept 属性值不同，用户可以选择上传图片或视频；选项“拍照”会拉起相机，根据 accept 属性值不同，用户可以选择拍照或录像；选项“文件”会拉起文件管理器，用户可以上传任意内容。

### handleFileList的使用说明

该函数将选择的文件路径提交给ArkWeb，入参主要有两种类型：

1. file协议路径，目前只支持前缀为 file://media/ 、file://docs/ 的公共路径和 file://<packageName>/ 的应用包名路径，其他file协议路径无权限。
2. 沙箱目录，具体参考[应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-manage-upload-download "管理网页文件上传与下载")
# 使用Web组件的下载能力

更新时间: 2025-12-16 16:38

当需要通过Web页面进行文件下载时，可以通过此方式调用Web接口。

## 监听页面触发的下载

通过[setDownloadDelegate()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#setdownloaddelegate11)向Web组件注册一个DownloadDelegate来监听页面触发的下载任务。资源由Web组件来下载，Web组件会通过DownloadDelegate将下载的进度通知给应用。

下面的示例中，在应用的rawfile中创建index.html以及download.html。应用启动后会创建一个Web组件并加载index.html，点击setDownloadDelegate按钮向Web组件注册一个DownloadDelegate，点击页面里的下载按钮的时候会触发一个下载任务，在DownloadDelegate中可以监听到下载的进度。

默认路径在应用沙箱的web目录内，用户无法查看。如果希望用户能够查看，需要将下载路径修改到有访问权限的目录，比如Download目录，请参考[使用Web组件发起一个下载任务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-download#%E4%BD%BF%E7%94%A8web%E7%BB%84%E4%BB%B6%E5%8F%91%E8%B5%B7%E4%B8%80%E4%B8%AA%E4%B8%8B%E8%BD%BD%E4%BB%BB%E5%8A%A1)。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct WebComponent {
7.   controller: webview.WebviewController = new webview.WebviewController();
8.   delegate: webview.WebDownloadDelegate = new webview.WebDownloadDelegate();

9.   build() {
10.     Column() {
11.       Button('setDownloadDelegate')
12.         .onClick(() => {
13.           try {
14.             this.delegate.onBeforeDownload((webDownloadItem: webview.WebDownloadItem) => {
15.               console.info("will start a download.");
16.               // 传入一个下载路径，并开始下载。
17.               // 如果传入一个不存在的路径，则会下载到默认/data/storage/el2/base/cache/web/目录。
18.               webDownloadItem.start("/data/storage/el2/base/cache/web/" + webDownloadItem.getSuggestedFileName());
19.             })
20.             this.delegate.onDownloadUpdated((webDownloadItem: webview.WebDownloadItem) => {
21.               // 下载任务的唯一标识。
22.               console.info("download update guid: " + webDownloadItem.getGuid());
23.               // 下载的进度。
24.               console.info("download update percent complete: " + webDownloadItem.getPercentComplete());
25.               // 当前的下载速度。
26.               console.info("download update speed: " + webDownloadItem.getCurrentSpeed())
27.             })
28.             this.delegate.onDownloadFailed((webDownloadItem: webview.WebDownloadItem) => {
29.               console.error("download failed guid: " + webDownloadItem.getGuid());
30.               // 下载任务失败的错误码。
31.               console.error("download failed last error code: " + webDownloadItem.getLastErrorCode());
32.             })
33.             this.delegate.onDownloadFinish((webDownloadItem: webview.WebDownloadItem) => {
34.               console.info("download finish guid: " + webDownloadItem.getGuid());
35.             })
36.             this.controller.setDownloadDelegate(this.delegate);
37.           } catch (error) {
38.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
39.           }
40.         })
41.       Web({ src: $rawfile('index.html'), controller: this.controller })
42.     }
43.   }
44. }

加载的html文件。

1. <!-- index.html -->
2. <!DOCTYPE html>
3. <html>
4. <body>
5. // 点击视频右下方菜单的下载按钮会触发下载任务。
6. <video controls="controls" width="800px" height="580px"
7.        src="http://vjs.zencdn.net/v/oceans.mp4"
8.        type="video/mp4">
9. </video>
10. <a href='data:text/html,%3Ch1%3EHello%2C%20World%21%3C%2Fh1%3E' download='download.html'>下载download.html</a>
11. </body>
12. </html>

待下载的html文件。

1. <!-- download.html -->
2. <!DOCTYPE html>
3. <html>
4. <body>
5. <h1>download test</h1>
6. </body>
7. </html>

## 使用Web组件发起一个下载任务

使用[startDownload()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#startdownload11)接口发起一个下载。

Web组件发起的下载会根据当前显示的url以及Web组件默认的Referrer Policy来计算referrer。

在下面的示例中，先点击setDownloadDelegate按钮向Web注册一个监听类，然后点击startDownload主动发起了一个下载，该下载任务也会通过设置的DownloadDelegate来通知app下载的进度。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct WebComponent {
7.   controller: webview.WebviewController = new webview.WebviewController();
8.   delegate: webview.WebDownloadDelegate = new webview.WebDownloadDelegate();

9.   build() {
10.     Column() {
11.       Button('setDownloadDelegate')
12.         .onClick(() => {
13.           try {
14.             this.delegate.onBeforeDownload((webDownloadItem: webview.WebDownloadItem) => {
15.               console.info("will start a download.");
16.               // 传入一个下载路径，并开始下载。
17.               // 如果传入一个不存在的路径，则会下载到默认/data/storage/el2/base/cache/web/目录。
18.               webDownloadItem.start("/data/storage/el2/base/cache/web/" + webDownloadItem.getSuggestedFileName());
19.             })
20.             this.delegate.onDownloadUpdated((webDownloadItem: webview.WebDownloadItem) => {
21.               console.info("download update guid: " + webDownloadItem.getGuid());
22.             })
23.             this.delegate.onDownloadFailed((webDownloadItem: webview.WebDownloadItem) => {
24.               console.error("download failed guid: " + webDownloadItem.getGuid());
25.             })
26.             this.delegate.onDownloadFinish((webDownloadItem: webview.WebDownloadItem) => {
27.               console.info("download finish guid: " + webDownloadItem.getGuid());
28.             })
29.             this.controller.setDownloadDelegate(this.delegate);
30.           } catch (error) {
31.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
32.           }
33.         })
34.       Button('startDownload')
35.         .onClick(() => {
36.           try {
37.             // 这里指定下载地址为 https://www.example.com/，Web组件会发起一个下载任务将该页面下载下来。
38.             // 开发者需要替换为自己想要下载的内容的地址。
39.             this.controller.startDownload('https://www.example.com/');
40.           } catch (error) {
41.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
42.           }
43.         })
44.       Web({ src: 'www.example.com', controller: this.controller })
45.     }
46.   }
47. }

使用[DocumentViewPicker()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-picker#documentviewpicker)获取当前示例的默认下载目录，将该目录设置为下载目录。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';
4. import { picker, fileUri } from  '@kit.CoreFileKit';
5. @Entry
6. @Component
7. struct WebComponent {
8.   controller: webview.WebviewController = new webview.WebviewController();
9.   delegate: webview.WebDownloadDelegate = new webview.WebDownloadDelegate();

10.   build() {
11.     Column() {
12.       Button('setDownloadDelegate')
13.         .onClick(() => {
14.           try {
15.             this.delegate.onBeforeDownload((webDownloadItem: webview.WebDownloadItem) => {
16.               console.info("will start a download.");
17.               // 使用DocumentViewPicker()获取当前示例的默认下载目录，将该目录设置为下载目录
18.               getDownloadPathFromPicker().then((downloadPath) => {
19.                 webDownloadItem.start(downloadPath + '/' + webDownloadItem.getSuggestedFileName());
20.               });

21.             })
22.             this.delegate.onDownloadUpdated((webDownloadItem: webview.WebDownloadItem) => {
23.               // 下载任务的唯一标识。
24.               console.info("download update guid: " + webDownloadItem.getGuid());
25.               // 下载的进度。
26.               console.info("download update percent complete: " + webDownloadItem.getPercentComplete());
27.               // 当前的下载速度。
28.               console.info("download update speed: " + webDownloadItem.getCurrentSpeed())
29.             })
30.             this.delegate.onDownloadFailed((webDownloadItem: webview.WebDownloadItem) => {
31.               console.error("download failed guid: " + webDownloadItem.getGuid());
32.               // 下载任务失败的错误码。
33.               console.error("download failed last error code: " + webDownloadItem.getLastErrorCode());
34.             })
35.             this.delegate.onDownloadFinish((webDownloadItem: webview.WebDownloadItem) => {
36.               console.info("download finish guid: " + webDownloadItem.getGuid());
37.             })
38.             this.controller.setDownloadDelegate(this.delegate);
39.           } catch (error) {
40.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
41.           }
42.         })
43.       Web({ src: $rawfile('index.html'), controller: this.controller })
44.     }
45.   }

46. }
47. function getDownloadPathFromPicker(): Promise<string> {
48.   return new Promise<string>(resolve => {
49.     try {
50.       const documentSaveOptions = new picker.DocumentSaveOptions();
51.       documentSaveOptions.pickerMode = picker.DocumentPickerMode.DOWNLOAD
52.       const documentPicker = new picker.DocumentViewPicker();
53.       documentPicker.save(documentSaveOptions).then(async (documentSaveResult: Array<string>) => {
54.         if (documentSaveResult.length <= 0) {
55.           resolve('');
56.           return;
57.         }
58.         const uriString = documentSaveResult[0];
59.         if (!uriString) {
60.           resolve('');
61.           return;
62.         }
63.         const uri = new fileUri.FileUri(uriString);
64.         resolve(uri.path);
65.       }).catch((err: BusinessError) => {
66.         console.error(`ErrorCode: ${err.code},  Message: ${err.message}`);
67.         resolve('');
68.       });
69.     } catch (error) {
70.       resolve('');
71.     }
72.   })
73. }

说明

Web组件的下载功能要求应用通过调用[WebDownloadItem.start](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webdownloaditem#start11)来指定下载文件的保存路径。

值得注意的是，WebDownloadItem.start并非启动下载，下载过程实际上在用户点击页面链接时即已开始。WebDownloadItem.start的作用是将已经下载到临时文件的部分移动到指定目标路径，后续未完成的下载的内容将直接保存到指定目标路径，临时目录位于/data/storage/el2/base/cache/web/Temp/。如果决定取消当前下载，应调用[WebDownloadItem.cancel](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webdownloaditem#cancel11)，此时临时文件将被删除。

如果不希望在WebDownloadItem.start之前将文件下载到临时目录，可以通过WebDownloadItem.cancel中断下载，后续可通过[WebDownloadManager.resumeDownload](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webdownloadmanager#resumedownload11)恢复中断的下载。

## 使用Web组件恢复进程退出时未下载完成的任务

在Web组件启动时，可通过[resumeDownload()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webdownloadmanager#resumedownload11)接口恢复未完成的下载任务。

在以下示例中，通过“record”按钮将当前下载任务保存至持久化文件中，应用重启后，可借助“recovery”按钮恢复持久化的下载任务。示例代码实现了将当前下载任务持久化保存至文件的功能，若需保存多个下载任务，应用可根据需求调整持久化的时机与方式。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';
4. import { downloadUtil, fileName, filePath } from './downloadUtil'; // downloadUtil.ets 见下文

5. @Entry
6. @Component
7. struct WebComponent {
8.   controller: webview.WebviewController = new webview.WebviewController();
9.   delegate: webview.WebDownloadDelegate = new webview.WebDownloadDelegate();
10.   download: webview.WebDownloadItem = new webview.WebDownloadItem();
11.   // 用于记录失败的下载任务。
12.   failedData: Uint8Array = new Uint8Array();

13.   aboutToAppear(): void {
14.     downloadUtil.init(this.getUIContext());
15.   }

16.   build() {
17.     Column() {
18.       Button('setDownloadDelegate')
19.         .onClick(() => {
20.           try {
21.             this.delegate.onBeforeDownload((webDownloadItem: webview.WebDownloadItem) => {
22.               console.info("will start a download.");
23.               // 传入一个下载路径，并开始下载。
24.               // 如果传入一个不存在的路径，则会下载到默认/data/storage/el2/base/cache/web/目录。
25.               webDownloadItem.start("/data/storage/el2/base/cache/web/" + webDownloadItem.getSuggestedFileName());
26.             })
27.             this.delegate.onDownloadUpdated((webDownloadItem: webview.WebDownloadItem) => {
28.               console.info("download update percent complete: " + webDownloadItem.getPercentComplete());
29.               this.download = webDownloadItem;
30.             })
31.             this.delegate.onDownloadFailed((webDownloadItem: webview.WebDownloadItem) => {
32.               console.error("download failed guid: " + webDownloadItem.getGuid());
33.               // 序列化失败的下载任务到一个字节数组。
34.               this.failedData = webDownloadItem.serialize();
35.             })
36.             this.delegate.onDownloadFinish((webDownloadItem: webview.WebDownloadItem) => {
37.               console.info("download finish guid: " + webDownloadItem.getGuid());
38.             })
39.             this.controller.setDownloadDelegate(this.delegate);
40.             webview.WebDownloadManager.setDownloadDelegate(this.delegate);
41.           } catch (error) {
42.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
43.           }
44.         })
45.       Button('startDownload')
46.         .onClick(() => {
47.           try {
48.             // 这里指定下载地址为 https://www.example.com/，Web组件会发起一个下载任务将该页面下载下来。
49.             // 开发者需要替换为自己想要下载的内容的地址。
50.             this.controller.startDownload('https://www.example.com/');
51.           } catch (error) {
52.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
53.           }
54.         })
55.       // 将当前的下载任务信息序列化保存，用于后续恢复下载任务。
56.       // 当前用例仅展示下载一个任务的场景，多任务场景请按需扩展。
57.       Button('record')
58.         .onClick(() => {
59.           try {
60.             // 保存当前下载数据到持久化文档中。
61.             downloadUtil.saveDownloadInfo(downloadUtil.uint8ArrayToStr(this.download.serialize()));
62.           } catch (error) {
63.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
64.           }
65.         })
66.       // 从序列化的下载任务信息中，恢复下载任务。
67.       // 按钮触发时必须保证WebDownloadManager.setDownloadDelegate设置完成。
68.       Button('recovery')
69.         .onClick(() => {
70.           try {
71.             // 当前默认持久化文件存在，用户根据实际情况增加判断。
72.             let webDownloadItem =
73.               webview.WebDownloadItem.deserialize(downloadUtil.strToUint8Array(downloadUtil.readFileSync(filePath, fileName)));
74.             webview.WebDownloadManager.resumeDownload(webDownloadItem);
75.           } catch (error) {
76.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
77.           }
78.         })

79.       Web({ src: 'www.example.com', controller: this.controller })
80.     }
81.   }
82. }

下载任务信息持久化工具类文件。

1. // downloadUtil.ets
2. import { util } from '@kit.ArkTS';
3. import fileStream from '@ohos.file.fs';

4. const helper = new util.Base64Helper();

5. export let filePath : string;
6. export const fileName = 'demoFile.txt';
7. export namespace  downloadUtil {

8.   export function init(context: UIContext): void {
9.     filePath = context.getHostContext()!.filesDir;
10.   }

11.   export function uint8ArrayToStr(uint8Array: Uint8Array): string {
12.     return helper.encodeToStringSync(uint8Array);
13.   }

14.   export function strToUint8Array(str: string): Uint8Array {
15.     return helper.decodeSync(str);
16.   }

17.   export function saveDownloadInfo(downloadInfo: string): void {
18.     if (!fileExists(filePath)) {
19.       mkDirectorySync(filePath);
20.     }

21.     writeToFileSync(filePath, fileName, downloadInfo);
22.   }

23.   export function fileExists(filePath: string): boolean {
24.     try {
25.       return fileStream.accessSync(filePath);
26.     } catch (error) {
27.       return false;
28.     }
29.   }

30.   export function mkDirectorySync(directoryPath: string, recursion?: boolean): void {
31.     try {
32.       fileStream.mkdirSync(directoryPath, recursion ?? false);
33.     } catch (error) {
34.       console.error(`mk dir error. err message: ${error.message}, err code: ${error.code}`);
35.     }
36.   }

37.   export function writeToFileSync(dir: string, fileName: string, msg: string): void {
38.     let file = fileStream.openSync(dir + '/' + fileName, fileStream.OpenMode.WRITE_ONLY | fileStream.OpenMode.CREATE);
39.     fileStream.writeSync(file.fd, msg);
40.   }

41.   export function readFileSync(dir: string, fileName: string): string {
42.     return fileStream.readTextSync(dir + '/' + fileName);
43.   }

44. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-file-upload "使用Web组件上传文件")
# 在Web中打开摄像头和麦克风

更新时间: 2025-12-16 16:38

WebRTC（Web Real-Time Communications）是一项实时通讯技术，它允许网络应用或站点在无需中间媒介的情况下建立浏览器之间的点对点（Peer-to-Peer）连接，实现视频流、音频流或其他任意数据的传输。WebRTC所包含的标准使得用户无需安装任何插件或第三方软件即可创建点对点（Peer-to-Peer）的数据共享与电话会议。WebRTC技术适用于所有现代浏览器和主要平台的本机客户端，其背后的技术作为开放的Web标准实现，并在所有主要浏览器中作为常规JavaScript API提供。

Web组件可以通过W3C标准协议接口拉起摄像头和麦克风，通过[onPermissionRequest](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onpermissionrequest9)接口接收权限请求通知，需在配置文件中声明相应的音频权限。

- 使用摄像头和麦克风功能前请在module.json5中添加音频相关权限，权限的添加方法请参考[在配置文件中声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。
    
    1.  // src/main/resources/base/element/string.json
    2.  {
    3.    "name": "reason_for_camera",
    4.    "value": "reason_for_camera"
    5.  },
    6.  {
    7.    "name": "reason_for_microphone",
    8.    "value": "reason_for_microphone"
    9.  }
    
    10.   // src/main/module.json5
    11.   "requestPermissions":[
    12.     {
    13.       "name" : "ohos.permission.CAMERA",
    14.       "reason": "$string:reason_for_camera",
    15.       "usedScene": {
    16.         "abilities": [
    17.           "EntryAbility"
    18.         ],
    19.         "when":"inuse"
    20.       }
    21.     },
    22.     {
    23.       "name" : "ohos.permission.MICROPHONE",
    24.       "reason": "$string:reason_for_microphone",
    25.       "usedScene": {
    26.         "abilities": [
    27.           "EntryAbility"
    28.         ],
    29.         "when":"inuse"
    30.       }
    31.     }
    32.   ]
    

通过在JavaScript中调用W3C标准协议接口navigator.mediaDevices.getUserMedia()，该接口用于拉起摄像头和麦克风。constraints参数是一个包含了video和audio两个成员的MediaStreamConstraints对象，用于说明请求的媒体类型。

在下面的示例中，点击前端页面中的开启摄像头按钮再点击onConfirm，打开摄像头和麦克风。

- 应用侧代码。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { abilityAccessCtrl } from '@kit.AbilityKit';
    
    5. @Entry
    6. @Component
    7. struct WebComponent {
    8.   controller: webview.WebviewController = new webview.WebviewController();
    9.   uiContext: UIContext = this.getUIContext();
    
    10.   aboutToAppear() {
    11.     // 配置Web开启调试模式
    12.     webview.WebviewController.setWebDebuggingAccess(true);
    13.     // 获取权限请求通知，点击onConfirm按钮后，拉起摄像头和麦克风。
    14.     let atManager = abilityAccessCtrl.createAtManager();
    15.     atManager.requestPermissionsFromUser(this.uiContext.getHostContext(), ['ohos.permission.CAMERA', 'ohos.permission.MICROPHONE'])
    16.       .then((data) => {
    17.         console.info('data:' + JSON.stringify(data));
    18.         console.info('data permissions:' + data.permissions);
    19.         console.info('data authResults:' + data.authResults);
    20.       }).catch((error: BusinessError) => {
    21.       console.error(`Failed to request permissions from user. Code is ${error.code}, message is ${error.message}`);
    22.     })
    23.   }
    
    24.   build() {
    25.     Column() {
    26.       Web({ src: $rawfile('index.html'), controller: this.controller })
    27.         .onPermissionRequest((event) => {
    28.           if (event) {
    29.             this.uiContext.showAlertDialog({
    30.               title: 'title',
    31.               message: 'text',
    32.               primaryButton: {
    33.                 value: 'deny',
    34.                 action: () => {
    35.                   event.request.deny();
    36.                 }
    37.               },
    38.               secondaryButton: {
    39.                 value: 'onConfirm',
    40.                 action: () => {
    41.                   event.request.grant(event.request.getAccessibleResource());
    42.                 }
    43.               },
    44.               cancel: () => {
    45.                 event.request.deny();
    46.               }
    47.             })
    48.           }
    49.         })
    50.     }
    51.   }
    52. }
    
- 前端页面index.html代码。
    
    1. <!-- index.html -->
    2. <!DOCTYPE html>
    3. <html>
    4. <head>
    5.   <meta charset="UTF-8">
    6. </head>
    7. <body>
    8. <video id="video" width="500px" height="500px" autoplay></video>
    9. <canvas id="canvas" width="500px" height="500px"></canvas>
    10. <br>
    11. <input type="button" title="HTML5摄像头" value="开启摄像头" onclick="getMedia()"/>
    12. <script>
    13.   function getMedia()
    14.   {
    15.     let constraints = {
    16.       video: {width: 500, height: 500},
    17.       audio: true
    18.     };
    19.     // 获取video摄像头区域
    20.     let video = document.getElementById("video");
    21.     // 返回的Promise对象
    22.     let promise = navigator.mediaDevices.getUserMedia(constraints);
    23.     // then()异步，调用MediaStream对象作为参数
    24.     promise.then(function(MediaStream) {
    25.       video.srcObject = MediaStream;
    26.       video.play();
    27.     }).catch(function(err) {
    28.         console.info(err.name + ": " + err.message);
    29.     });
    30.   }
    31. </script>
    32. </body>
    33. </html>
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-use-multimedia "使用网页多媒体")
# 托管网页中的媒体播放

更新时间: 2025-12-16 16:38

Web组件提供了应用接管网页中媒体播放的能力，用来支持应用增强网页的媒体播放，如画质增强等。

## 使用场景

网页播放媒体时，存在以下问题：网页清晰度低、网页播放器播放控件功能有限、某些视频无法播放。

应用开发者可以使用该功能，通过自己或者第三方播放器接管网页媒体播放，从而改善播放体验。

## 实现原理

### ArkWeb内核播放媒体的框架

不开启该功能时，ArkWeb内核的播放架构如下所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163835.35430990552473955059595696160282:50001231000000:2800:2AB4EE6C0C6FC509DA46C6DF5B611AC17D4887CEE7112C15A9443804156088CB.png)

说明

- 上图中1表示ArkWeb内核创建WebMediaPlayer来播放网页中的媒体资源。
- 上图中2表示WebMediaPlayer使用系统解码器来渲染媒体数据。

开启该功能后，ArkWeb内核的播放架构如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163835.59081235908944484050910802929746:50001231000000:2800:1442EEDE4A492A10E8D2DBB4589640AC4B39297BCEAA3347BF757A7F46860F31.png)

说明

- 上图中1表示ArkWeb内核创建WebMediaPlayer来播放网页中的媒体资源。
- 上图中2表示WebMediaPlayer使用应用提供的本地播放器（NativeMediaPlayer）来渲染媒体数据。

### ArkWeb内核与应用的交互

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163835.52900261194593180233742781451285:50001231000000:2800:0214CDC4181BC347E14ACBB26EDDE54DE71EFDCEA9BF49352F58CB3E6036A604.png)

说明

- 上图中1的详细说明见[开启接管网页媒体播放](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-takeovers-web-media#%E5%BC%80%E5%90%AF%E6%8E%A5%E7%AE%A1%E7%BD%91%E9%A1%B5%E5%AA%92%E4%BD%93%E6%92%AD%E6%94%BE)。
- 上图中2的详细说明见[创建本地播放器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-takeovers-web-media#%E5%88%9B%E5%BB%BA%E6%9C%AC%E5%9C%B0%E6%92%AD%E6%94%BE%E5%99%A8nativemediaplayer)。
- 上图中3的详细说明见[绘制本地播放器组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-takeovers-web-media#%E7%BB%98%E5%88%B6%E6%9C%AC%E5%9C%B0%E6%92%AD%E6%94%BE%E5%99%A8%E7%BB%84%E4%BB%B6)。
- 上图中4的详细说明见[执行 ArkWeb 内核发送给本地播放器的播控指令](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-takeovers-web-media#%E6%89%A7%E8%A1%8Carkweb%E5%86%85%E6%A0%B8%E5%8F%91%E9%80%81%E7%BB%99%E6%9C%AC%E5%9C%B0%E6%92%AD%E6%94%BE%E5%99%A8%E7%9A%84%E6%92%AD%E6%8E%A7%E6%8C%87%E4%BB%A4)。
- 上图中5的详细说明见[将本地播放器的状态信息通知给 ArkWeb 内核](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-takeovers-web-media#%E5%B0%86%E6%9C%AC%E5%9C%B0%E6%92%AD%E6%94%BE%E5%99%A8%E7%9A%84%E7%8A%B6%E6%80%81%E4%BF%A1%E6%81%AF%E9%80%9A%E7%9F%A5%E7%BB%99arkweb%E5%86%85%E6%A0%B8)。

## 开发指导

### 开启接管网页媒体播放

需要先通过[enableNativeMediaPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#enablenativemediaplayer12)接口开启接管网页媒体播放的功能。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct WebComponent {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   build() {
8.     Column() {
9.       Web({ src: 'www.example.com', controller: this.controller })
10.         .enableNativeMediaPlayer({ enable: true, shouldOverlay: false })
11.     }
12.   }
13. }

### 创建本地播放器(NativeMediaPlayer)

该功能开启后，网页中有媒体需要播放时，ArkWeb内核会触发[onCreateNativeMediaPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#oncreatenativemediaplayer12)注册的回调函数。

应用则需要调用 onCreateNativeMediaPlayer 来注册一个创建本地播放器的回调函数。

该回调函数需要根据媒体信息来判断是否要创建一个本地播放器来接管当前的网页媒体资源。

- 如果应用不接管当前的网页媒体资源， 需在回调函数里返回 null 。
- 如果应用接管当前的网页媒体资源， 需在回调函数里返回一个本地播放器实例。

本地播放器需要实现[NativeMediaPlayerBridge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-nativemediaplayerbridge)接口，以便ArkWeb内核对本地播放器进行播控操作。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. // 实现 webview.NativeMediaPlayerBridge 接口。
4. // ArkWeb 内核调用该类的方法来对 NativeMediaPlayer 进行播控。
5. class NativeMediaPlayerImpl implements webview.NativeMediaPlayerBridge {
6.   // ... 实现 NativeMediaPlayerBridge 里的接口方法 ...
7.   constructor(handler: webview.NativeMediaPlayerHandler, mediaInfo: webview.MediaInfo) {}
8.   updateRect(x: number, y: number, width: number, height: number) {}
9.   play() {}
10.   pause() {}
11.   seek(targetTime: number) {}
12.   release() {}
13.   setVolume(volume: number) {}
14.   setMuted(muted: boolean) {}
15.   setPlaybackRate(playbackRate: number) {}
16.   enterFullscreen() {}
17.   exitFullscreen() {}
18. }

19. @Entry
20. @Component
21. struct WebComponent {
22.   controller: webview.WebviewController = new webview.WebviewController();

23.   build() {
24.     Column() {
25.       Web({ src: 'www.example.com', controller: this.controller })
26.         .enableNativeMediaPlayer({ enable: true, shouldOverlay: false })
27.         .onPageBegin((event) => {
28.           this.controller.onCreateNativeMediaPlayer((handler: webview.NativeMediaPlayerHandler, mediaInfo: webview.MediaInfo) => {
29.             // 判断需不需要接管当前的媒体。
30.             if (!shouldHandle(mediaInfo)) {
31.               // 本地播放器不接管该媒体。
32.               // 返回 null 。ArkWeb 内核将用自己的播放器来播放该媒体。
33.               return null;
34.             }
35.             // 接管当前的媒体。
36.             // 返回一个本地播放器实例给 ArkWeb 内核。
37.             let nativePlayer: webview.NativeMediaPlayerBridge = new NativeMediaPlayerImpl(handler, mediaInfo);
38.             return nativePlayer;
39.           });
40.         })
41.     }
42.   }
43. }

44. // stub
45. function shouldHandle(mediaInfo: webview.MediaInfo) {
46.   return true;
47. }

### 绘制本地播放器组件

应用接管网页媒体后，应用需要将本地播放器组件及视频画面绘制到ArkWeb内核提供的Surface上。ArkWeb内核再将Surface与网页进行合成并显示。

该流程与[同层渲染](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-same-layer)绘制一致。

1. 在应用启动阶段，应用应保存UIContext，以便后续的同层渲染绘制流程能够使用该UIContext。
    
    1. // xxxAbility.ets
    
    2. import { UIAbility } from '@kit.AbilityKit';
    3. import { window } from '@kit.ArkUI';
    
    4. export default class EntryAbility extends UIAbility {
    5.   onWindowStageCreate(windowStage: window.WindowStage): void {
    6.     windowStage.loadContent('pages/Index', (err, data) => {
    7.       if (err && err.code) {
    8.         return;
    9.       }
    
    10.       let mainWindow = windowStage.getMainWindowSync();
    11.       if (mainWindow) {
    12.         // 保存UIContext， 在后续的同层渲染绘制中使用。
    13.         AppStorage.setOrCreate<UIContext>("UIContext", mainWindow.getUIContext());
    14.       } else {
    15.         console.error("Failed to get the main window");
    16.       }
    17.     });
    18.   }
    
    19.   // ... 其他需要重写的方法 ...
    20. }
    
2. 应用使用ArkWeb内核创建的Surface进行同层渲染绘制。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BuilderNode, FrameNode, NodeController, NodeRenderType } from '@kit.ArkUI';
    
    4. interface ComponentParams {}
    
    5. class MyNodeController extends NodeController {
    6.   private rootNode: BuilderNode<[ComponentParams]> | undefined;
    
    7.   constructor(surfaceId: string, renderType: NodeRenderType) {
    8.     super();
    
    9.     // 获取之前保存的 UIContext 。
    10.     let uiContext = AppStorage.get<UIContext>("UIContext");
    11.     this.rootNode = new BuilderNode(uiContext as UIContext, { surfaceId: surfaceId, type: renderType });
    12.   }
    
    13.   makeNode(uiContext: UIContext): FrameNode | null {
    14.     if (this.rootNode) {
    15.       return this.rootNode.getFrameNode() as FrameNode;
    16.     }
    17.     return null;
    18.   }
    
    19.   build() {
    20.     // 构造本地播放器组件
    21.   }
    22. }
    
    23. @Entry
    24. @Component
    25. struct WebComponent {
    26.   node_controller?: MyNodeController;
    27.   controller: webview.WebviewController = new webview.WebviewController();
    28.   @State show_native_media_player: boolean = false;
    
    29.   build() {
    30.     Column() {
    31.       Stack({ alignContent: Alignment.TopStart }) {
    32.         if (this.show_native_media_player) {
    33.           NodeContainer(this.node_controller)
    34.             .width(300)
    35.             .height(150)
    36.             .backgroundColor(Color.Transparent)
    37.             .border({ width: 2, color: Color.Orange })
    38.         }
    39.         Web({ src: 'www.example.com', controller: this.controller })
    40.           .enableNativeMediaPlayer({ enable: true, shouldOverlay: false })
    41.           .onPageBegin((event) => {
    42.             this.controller.onCreateNativeMediaPlayer((handler: webview.NativeMediaPlayerHandler, mediaInfo: webview.MediaInfo) => {
    43.               // 接管当前的媒体。
    44.               // 使用同层渲染流程提供的 surface 来构造一个本地播放器组件。
    45.               this.node_controller = new MyNodeController(mediaInfo.surfaceInfo.id, NodeRenderType.RENDER_TYPE_TEXTURE);
    46.               this.node_controller.build();
    
    47.               // 展示本地播放器组件。
    48.               this.show_native_media_player = true;
    
    49.               // 返回一个本地播放器实例给 ArkWeb 内核。
    50.               let nativePlayer: webview.NativeMediaPlayerBridge = new NativeMediaPlayerImpl(handler, mediaInfo);
    51.               return nativePlayer;
    52.             });
    53.           })
    54.       }
    55.     }
    56.   }
    57. }
    

动态创建组件并绘制到Surface上的详细介绍见[同层渲染](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-same-layer)。

### 执行ArkWeb内核发送给本地播放器的播控指令

为了方便ArkWeb内核对本地播放器进行播控操作，应用需要令本地播放器实现[NativeMediaPlayerBridge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-nativemediaplayerbridge)接口，并根据每个接口方法的功能对本地播放器进行相应操作。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. class ActualNativeMediaPlayerListener {
4.   constructor(handler: webview.NativeMediaPlayerHandler) {}
5. }

6. class NativeMediaPlayerImpl implements webview.NativeMediaPlayerBridge {
7.   constructor(handler: webview.NativeMediaPlayerHandler, mediaInfo: webview.MediaInfo) {
8.     // 1. 创建一个本地播放器的状态监听。
9.     let listener: ActualNativeMediaPlayerListener = new ActualNativeMediaPlayerListener(handler);
10.     // 2. 创建一个本地播放器。
11.     // 3. 监听该本地播放器。
12.     // ...
13.   }

14.   updateRect(x: number, y: number, width: number, height: number) {
15.     // <video> 标签的位置和大小发生了变化。
16.     // 根据该信息变化，作出相应的改变。
17.   }

18.   play() {
19.     // 启动本地播放器播放。
20.   }

21.   pause() {
22.     // 暂停本地播放器播放。
23.   }

24.   seek(targetTime: number) {
25.     // 本地播放器跳转到指定的时间点。
26.   }

27.   release() {
28.     // 销毁本地播放器。
29.   }

30.   setVolume(volume: number) {
31.     // ArkWeb 内核要求调整本地播放器的音量。
32.     // 设置本地播放器的音量。
33.   }

34.   setMuted(muted: boolean) {
35.     // 将本地播放器静音或取消静音。
36.   }

37.   setPlaybackRate(playbackRate: number) {
38.     // 调整本地播放器的播放速度。
39.   }

40.   enterFullscreen() {
41.     // 将本地播放器设置为全屏播放。
42.   }

43.   exitFullscreen() {
44.     // 将本地播放器退出全屏播放。
45.   }
46. }

### 将本地播放器的状态信息通知给ArkWeb内核

ArkWeb内核需要本地播放器的状态信息来更新到网页（例如：视频的宽高、播放时间、缓存时间等），因此，应用需要将本地播放器的状态信息通知给ArkWeb内核。

在[onCreateNativeMediaPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#oncreatenativemediaplayer12)接口中， ArkWeb内核传递一个[NativeMediaPlayerHandler](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-nativemediaplayerhandler)对象给应用。应用需要通过该对象，将本地播放器的最新状态信息通知给ArkWeb内核。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. class ActualNativeMediaPlayerListener {
4.   handler: webview.NativeMediaPlayerHandler;

5.   constructor(handler: webview.NativeMediaPlayerHandler) {
6.     this.handler = handler;
7.   }

8.   onPlaying() {
9.     // 本地播放器开始播放。
10.     this.handler.handleStatusChanged(webview.PlaybackStatus.PLAYING);
11.   }
12.   onPaused() {
13.     // 本地播放器暂停播放。
14.     this.handler.handleStatusChanged(webview.PlaybackStatus.PAUSED);
15.   }
16.   onSeeking() {
17.     // 本地播放器开始执行跳转到目标时间点。
18.     this.handler.handleSeeking();
19.   }
20.   onSeekDone() {
21.     // 本地播放器 seek 完成。
22.     this.handler.handleSeekFinished();
23.   }
24.   onEnded() {
25.     // 本地播放器播放完成。
26.     this.handler.handleEnded();
27.   }
28.   onVolumeChanged() {
29.     // 获取本地播放器的音量。
30.     let volume: number = getVolume();
31.     this.handler.handleVolumeChanged(volume);
32.   }
33.   onCurrentPlayingTimeUpdate() {
34.     // 更新播放时间。
35.     let currentTime: number = getCurrentPlayingTime();
36.     // 将时间单位换算成秒。
37.     let currentTimeInSeconds = convertToSeconds(currentTime);
38.     this.handler.handleTimeUpdate(currentTimeInSeconds);
39.   }
40.   onBufferedChanged() {
41.     // 缓存发生了变化。
42.     // 获取本地播放器的缓存时长。
43.     let bufferedEndTime: number = getCurrentBufferedTime();
44.     // 将时间单位换算成秒。
45.     let bufferedEndTimeInSeconds = convertToSeconds(bufferedEndTime);
46.     this.handler.handleBufferedEndTimeChanged(bufferedEndTimeInSeconds);

47.     // 检查缓存状态。
48.     // 如果缓存状态发生了变化，则向 ArkWeb 内核通知缓存状态。
49.     let lastReadyState: webview.ReadyState = getLastReadyState();
50.     let currentReadyState: webview.ReadyState = getCurrentReadyState();
51.     if (lastReadyState != currentReadyState) {
52.       this.handler.handleReadyStateChanged(currentReadyState);
53.     }
54.   }
55.   onEnterFullscreen() {
56.     // 本地播放器进入了全屏状态。
57.     let isFullscreen: boolean = true;
58.     this.handler.handleFullscreenChanged(isFullscreen);
59.   }
60.   onExitFullscreen() {
61.     // 本地播放器退出了全屏状态。
62.     let isFullscreen: boolean = false;
63.     this.handler.handleFullscreenChanged(isFullscreen);
64.   }
65.   onUpdateVideoSize(width: number, height: number) {
66.     // 当本地播放器解析出视频宽高时， 通知 ArkWeb 内核。
67.     this.handler.handleVideoSizeChanged(width, height);
68.   }
69.   onDurationChanged(duration: number) {
70.     // 本地播放器解析到了新的媒体时长， 通知 ArkWeb 内核。
71.     this.handler.handleDurationChanged(duration);
72.   }
73.   onError(error: webview.MediaError, errorMessage: string) {
74.     // 本地播放器出错了，通知 ArkWeb 内核。
75.     this.handler.handleError(error, errorMessage);
76.   }
77.   onNetworkStateChanged(state: webview.NetworkState) {
78.     // 本地播放器的网络状态发生了变化， 通知 ArkWeb 内核。
79.     this.handler.handleNetworkStateChanged(state);
80.   }
81.   onPlaybackRateChanged(playbackRate: number) {
82.     // 本地播放器的播放速率发生了变化， 通知 ArkWeb 内核。
83.     this.handler.handlePlaybackRateChanged(playbackRate);
84.   }
85.   onMutedChanged(muted: boolean) {
86.     // 本地播放器的静音状态发生了变化， 通知 ArkWeb 内核。
87.     this.handler.handleMutedChanged(muted);
88.   }

89.   // ... 监听本地播放器其他的状态 ...
90. }
91. @Entry
92. @Component
93. struct WebComponent {
94.   controller: webview.WebviewController = new webview.WebviewController();
95.   @State show_native_media_player: boolean = false;

96.   build() {
97.     Column() {
98.       Web({ src: 'www.example.com', controller: this.controller })
99.         .enableNativeMediaPlayer({enable: true, shouldOverlay: false})
100.         .onPageBegin((event) => {
101.           this.controller.onCreateNativeMediaPlayer((handler: webview.NativeMediaPlayerHandler, mediaInfo: webview.MediaInfo) => {
102.             // 接管当前的媒体。

103.             // 创建一个本地播放器实例。
104.             // let nativePlayer: NativeMediaPlayerImpl = new NativeMediaPlayerImpl(handler, mediaInfo);

105.             // 创建一个本地播放器状态监听对象。
106.             let nativeMediaPlayerListener: ActualNativeMediaPlayerListener = new ActualNativeMediaPlayerListener(handler);
107.             // 监听本地播放器状态。
108.             // nativePlayer.setListener(nativeMediaPlayerListener);

109.             // 返回这个本地播放器实例给 ArkWeb 内核。
110.             return null;
111.           });
112.         })
113.     }
114.   }
115. }

116. // stub
117. function getVolume() {
118.   return 1;
119. }
120. function getCurrentPlayingTime() {
121.   return 1;
122. }
123. function getCurrentBufferedTime() {
124.   return 1;
125. }
126. function convertToSeconds(input: number) {
127.   return input;
128. }
129. function getLastReadyState() {
130.   return webview.ReadyState.HAVE_NOTHING;
131. }
132. function getCurrentReadyState() {
133.   return webview.ReadyState.HAVE_NOTHING;
134. }

## 完整示例

- 涉及网页媒体播放，需在配置文件中配置网络访问权限。添加方法请参考[在配置文件中声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。
    
    1. // src/main/module.json5
    2. "requestPermissions":[
    3.     {
    4.       "name" : "ohos.permission.INTERNET"
    5.     }
    6.   ]
    
- 在应用启动阶段保存UIContext。
    
    1. // xxxAbility.ets
    
    2. import { UIAbility } from '@kit.AbilityKit';
    3. import { window } from '@kit.ArkUI';
    
    4. export default class EntryAbility extends UIAbility {
    5.   onWindowStageCreate(windowStage: window.WindowStage): void {
    6.     windowStage.loadContent('pages/Index', (err, data) => {
    7.       if (err && err.code) {
    8.         return;
    9.       }
    
    10.       let mainWindow = windowStage.getMainWindowSync();
    11.       if (mainWindow) {
    12.         // 保存UIContext， 在后续的同层渲染绘制中使用。
    13.         AppStorage.setOrCreate<UIContext>("UIContext", mainWindow.getUIContext());
    14.       } else {
    15.         console.error("Failed to get the main window");
    16.       }
    17.     });
    18.   }
    
    19.   // ... 其他需要重写的方法 ...
    20. }
    
- 应用侧代码，视频托管使用示例。通过[AVPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/media-kit-intro#avplayer)托管Web媒体的播放。
    
    1. // Index.ets
    2. import { webview } from '@kit.ArkWeb';
    3. import { BuilderNode, FrameNode, NodeController, NodeRenderType } from '@kit.ArkUI';
    4. import { AVPlayerDemo, AVPlayerListener } from './PlayerDemo';
    
    5. // 实现 webview.NativeMediaPlayerBridge 接口。
    6. // ArkWeb 内核调用该类的方法来对 NativeMediaPlayer 进行播控。
    7. class NativeMediaPlayerImpl implements webview.NativeMediaPlayerBridge {
    8.   private surfaceId: string;
    9.   mediaSource: string;
    10.   private mediaHandler: webview.NativeMediaPlayerHandler;
    11.   nativePlayerInfo: NativePlayerInfo;
    12.   nativePlayer: AVPlayerDemo;
    13.   httpHeaders: Record<string, string>;
    14.   uiContext?: UIContext;
    
    15.   constructor(nativePlayerInfo: NativePlayerInfo, handler: webview.NativeMediaPlayerHandler, mediaInfo: webview.MediaInfo, uiContext: UIContext) {
    16.     this.uiContext = uiContext;
    17.     console.info(`NativeMediaPlayerImpl.constructor, surface_id[${mediaInfo.surfaceInfo.id}]`);
    18.     this.nativePlayerInfo = nativePlayerInfo;
    19.     this.mediaHandler = handler;
    20.     this.surfaceId = mediaInfo.surfaceInfo.id;
    21.     this.mediaSource = mediaInfo.mediaSrcList.find((item) => item.source.indexOf('.mp4') > 0)?.source
    22.       || mediaInfo.mediaSrcList[0].source;
    23.     this.httpHeaders = mediaInfo.headers;
    24.     this.nativePlayer = new AVPlayerDemo();
    
    25.     // 使用同层渲染功能，将视频及其播控组件绘制到网页中
    26.     this.nativePlayerInfo.node_controller = new MyNodeController(
    27.       this.nativePlayerInfo, this.surfaceId, this.mediaHandler, this, NodeRenderType.RENDER_TYPE_TEXTURE);
    28.     this.nativePlayerInfo.node_controller.build();
    29.     this.nativePlayerInfo.show_native_media_player = true;
    
    30.     console.info(`NativeMediaPlayerImpl.mediaSource: ${this.mediaSource}, headers: ${JSON.stringify(this.httpHeaders)}`);
    31.   }
    
    32.   updateRect(x: number, y: number, width: number, height: number): void {
    33.     let width_in_vp = this.uiContext!.px2vp(width);
    34.     let height_in_vp = this.uiContext!.px2vp(height);
    35.     console.info(`updateRect(${x}, ${y}, ${width}, ${height}), vp:{${width_in_vp}, ${height_in_vp}}`);
    
    36.     this.nativePlayerInfo.updateNativePlayerRect(x, y, width, height);
    37.   }
    
    38.   play() {
    39.     console.info('NativeMediaPlayerImpl.play');
    40.     this.nativePlayer.play();
    41.   }
    42.   pause() {
    43.     console.info('NativeMediaPlayerImpl.pause');
    44.     this.nativePlayer.pause();
    45.   }
    46.   seek(targetTime: number) {
    47.     console.info(`NativeMediaPlayerImpl.seek(${targetTime})`);
    48.     this.nativePlayer.seek(targetTime);
    49.   }
    50.   setVolume(volume: number) {
    51.     console.info(`NativeMediaPlayerImpl.setVolume(${volume})`);
    52.     this.nativePlayer.setVolume(volume);
    53.   }
    54.   setMuted(muted: boolean) {
    55.     console.info(`NativeMediaPlayerImpl.setMuted(${muted})`);
    56.   }
    57.   setPlaybackRate(playbackRate: number) {
    58.     console.info(`NativeMediaPlayerImpl.setPlaybackRate(${playbackRate})`);
    59.     this.nativePlayer.setPlaybackRate(playbackRate);
    60.   }
    61.   release() {
    62.     console.info('NativeMediaPlayerImpl.release');
    63.     this.nativePlayer?.release();
    64.     this.nativePlayerInfo.show_native_media_player = false;
    65.     this.nativePlayerInfo.node_width = 300;
    66.     this.nativePlayerInfo.node_height = 150;
    67.     this.nativePlayerInfo.destroyed();
    68.   }
    69.   enterFullscreen() {
    70.     console.info('NativeMediaPlayerImpl.enterFullscreen');
    71.   }
    72.   exitFullscreen() {
    73.     console.info('NativeMediaPlayerImpl.exitFullscreen');
    74.   }
    75. }
    
    76. // 监听NativeMediaPlayer的状态，然后通过 webview.NativeMediaPlayerHandler 将状态上报给 ArkWeb 内核。
    77. class AVPlayerListenerImpl implements AVPlayerListener {
    78.   handler: webview.NativeMediaPlayerHandler;
    79.   component: NativePlayerComponent;
    
    80.   constructor(handler: webview.NativeMediaPlayerHandler, component: NativePlayerComponent) {
    81.     this.handler = handler;
    82.     this.component = component;
    83.   }
    84.   onPlaying() {
    85.     console.info('AVPlayerListenerImpl.onPlaying');
    86.     this.handler.handleStatusChanged(webview.PlaybackStatus.PLAYING);
    87.   }
    88.   onPaused() {
    89.     console.info('AVPlayerListenerImpl.onPaused');
    90.     this.handler.handleStatusChanged(webview.PlaybackStatus.PAUSED);
    91.   }
    92.   onDurationChanged(duration: number) {
    93.     console.info(`AVPlayerListenerImpl.onDurationChanged(${duration})`);
    94.     this.handler.handleDurationChanged(duration);
    95.   }
    96.   onBufferedTimeChanged(buffered: number) {
    97.     console.info(`AVPlayerListenerImpl.onBufferedTimeChanged(${buffered})`);
    98.     this.handler.handleBufferedEndTimeChanged(buffered);
    99.   }
    100.   onTimeUpdate(time: number) {
    101.     this.handler.handleTimeUpdate(time);
    102.   }
    103.   onEnded() {
    104.     console.info('AVPlayerListenerImpl.onEnded');
    105.     this.handler.handleEnded();
    106.   }
    107.   onError() {
    108.     console.info('AVPlayerListenerImpl.onError');
    109.     this.component.has_error = true;
    110.     setTimeout(()=>{
    111.       this.handler.handleError(1, "Oops!");
    112.     }, 200);
    113.   }
    114.   onVideoSizeChanged(width: number, height: number) {
    115.     console.info(`AVPlayerListenerImpl.onVideoSizeChanged(${width}, ${height})`);
    116.     this.handler.handleVideoSizeChanged(width, height);
    117.     this.component.onSizeChanged(width, height);
    118.   }
    119.   onDestroyed(): void {
    120.     console.info('AVPlayerListenerImpl.onDestroyed');
    121.   }
    122. }
    
    123. interface ComponentParams {
    124.   text: string;
    125.   text2: string;
    126.   playerInfo: NativePlayerInfo;
    127.   handler: webview.NativeMediaPlayerHandler;
    128.   player: NativeMediaPlayerImpl;
    129. }
    
    130. // 自定义的播放器组件
    131. @Component
    132. struct NativePlayerComponent {
    133.   params?: ComponentParams;
    134.   @State bgColor: Color = Color.Red;
    135.   mXComponentController: XComponentController = new XComponentController();
    
    136.   videoController: VideoController = new VideoController();
    137.   offset_x: number = 0;
    138.   offset_y: number = 0;
    139.   @State video_width_percent: number = 100;
    140.   @State video_height_percent: number = 100;
    141.   view_width: number = 0;
    142.   view_height: number = 0;
    143.   video_width: number = 0;
    144.   video_height: number = 0;
    
    145.   fullscreen: boolean = false;
    146.   @State has_error: boolean = false;
    
    147.   onSizeChanged(width: number, height: number) {
    148.     this.video_width = width;
    149.     this.video_height = height;
    150.     let scale: number = this.view_width / width;
    151.     let scaled_video_height: number = scale * height;
    152.     this.video_height_percent = scaled_video_height / this.view_height * 100;
    153.     console.info(`NativePlayerComponent.onSizeChanged(${width},${height}), video_height_percent[${this.video_height_percent }]`);
    154.   }
    
    155.   build() {
    156.     Column() {
    157.       Stack() {
    158.         XComponent({ id: 'video_player_id', type: XComponentType.SURFACE, controller: this.mXComponentController })
    159.           .width(this.video_width_percent + '%')
    160.           .height(this.video_height_percent + '%')
    161.           .onLoad(()=>{
    162.             if (!this.params) {
    163.               console.info('this.params is null');
    164.               return;
    165.             }
    166.             console.info('NativePlayerComponent.onLoad, params[' + this.params
    167.               + '], text[' + this.params.text + '], text2[' + this.params.text2
    168.               + '], web_tab[' + this.params.playerInfo + '], handler[' + this.params.handler + ']');
    169.             this.params.player.nativePlayer.setSurfaceID(this.mXComponentController.getXComponentSurfaceId());
    
    170.             this.params.player.nativePlayer.avPlayerLiveDemo({
    171.               url: this.params.player.mediaSource,
    172.               listener: new AVPlayerListenerImpl(this.params.handler, this),
    173.               httpHeaders: this.params.player.httpHeaders,
    174.             });
    175.           })
    176.         Column() {
    177.           Row() {
    178.             Button(this.params?.text)
    179.               .height(50)
    180.               .border({ width: 2, color: Color.Red })
    181.               .backgroundColor(this.bgColor)
    182.               .onClick(()=>{
    183.                 console.info(`NativePlayerComponent.Button[${this.params?.text}] is clicked`);
    184.                 this.params?.player.nativePlayer?.play();
    185.               })
    186.               .onTouch((event: TouchEvent) => {
    187.                 event.stopPropagation();
    188.               })
    189.             Button(this.params?.text2)
    190.               .height(50)
    191.               .border({ width: 2, color: Color.Red })
    192.               .onClick(()=>{
    193.                 console.info(`NativePlayerComponent.Button[${this.params?.text2}] is clicked`);
    194.                 this.params?.player.nativePlayer?.pause();
    195.               })
    196.               .onTouch((event: TouchEvent) => {
    197.                 event.stopPropagation();
    198.               })
    199.           }
    200.           .width('100%')
    201.           .justifyContent(FlexAlign.SpaceEvenly)
    202.         }
    203.         if (this.has_error) {
    204.           Column() {
    205.             Text('Error')
    206.               .fontSize(30)
    207.           }
    208.           .backgroundColor('#eb5555')
    209.           .width('100%')
    210.           .height('100%')
    211.           .justifyContent(FlexAlign.Center)
    212.         }
    213.       }
    214.     }
    215.     .width('100%')
    216.     .height('100%')
    217.     .onAreaChange((oldValue: Area, newValue: Area) => {
    218.       console.info(`NativePlayerComponent.onAreaChange(${JSON.stringify(oldValue)}, ${JSON.stringify(newValue)})`);
    219.       this.view_width = new Number(newValue.width).valueOf();
    220.       this.view_height = new Number(newValue.height).valueOf();
    221.       this.onSizeChanged(this.video_width, this.video_height);
    222.     })
    223.   }
    224. }
    
    225. @Builder
    226. function NativePlayerComponentBuilder(params: ComponentParams) {
    227.   NativePlayerComponent({ params: params })
    228.     .backgroundColor(Color.Green)
    229.     .border({ width: 1, color: Color.Brown })
    230.     .width('100%')
    231.     .height('100%')
    232. }
    
    233. // 通过 NodeController 动态创建自定义的播放器组件， 并将组件内容绘制到 surface 上。
    234. class MyNodeController extends NodeController {
    235.   private rootNode: BuilderNode<[ComponentParams]> | undefined;
    236.   playerInfo: NativePlayerInfo;
    237.   listener: webview.NativeMediaPlayerHandler;
    238.   player: NativeMediaPlayerImpl;
    
    239.   constructor(playerInfo: NativePlayerInfo,
    240.               surfaceId: string,
    241.               listener: webview.NativeMediaPlayerHandler,
    242.               player: NativeMediaPlayerImpl,
    243.               renderType: NodeRenderType) {
    244.     super();
    245.     this.playerInfo = playerInfo;
    246.     this.listener = listener;
    247.     this.player = player;
    248.     let uiContext = AppStorage.get<UIContext>("UIContext");
    249.     this.rootNode = new BuilderNode(uiContext as UIContext, { surfaceId: surfaceId, type: renderType });
    250.     console.info(`MyNodeController, rootNode[${this.rootNode}], playerInfo[${playerInfo}], listener[${listener}], surfaceId[${surfaceId}]`);
    251.   }
    
    252.   makeNode(): FrameNode | null {
    253.     if (this.rootNode) {
    254.       return this.rootNode.getFrameNode() as FrameNode;
    255.     }
    256.     return null;
    257.   }
    
    258.   build() {
    259.     let params: ComponentParams = {
    260.       "text": "play",
    261.       "text2": "pause",
    262.       playerInfo: this.playerInfo,
    263.       handler: this.listener,
    264.       player: this.player
    265.     };
    266.     if (this.rootNode) {
    267.       this.rootNode.build(wrapBuilder(NativePlayerComponentBuilder), params);
    268.     }
    269.   }
    
    270.   postTouchEvent(event: TouchEvent) {
    271.     return this.rootNode?.postTouchEvent(event);
    272.   }
    273. }
    
    274. class Rect {
    275.   x: number = 0;
    276.   y: number = 0;
    277.   width: number = 0;
    278.   height: number = 0;
    
    279.   static toNodeRect(rectInPx: webview.RectEvent, uiContext: UIContext) : Rect {
    280.     let rect = new Rect();
    281.     rect.x = uiContext.px2vp(rectInPx.x);
    282.     rect.y = uiContext.px2vp(rectInPx.y);
    283.     rect.width = uiContext.px2vp(rectInPx.width);
    284.     rect.height = uiContext.px2vp(rectInPx.height);
    285.     return rect;
    286.   }
    287. }
    
    288. @Observed
    289. class NativePlayerInfo {
    290.   public web: WebComponent;
    291.   public embed_id: string;
    292.   public player: webview.NativeMediaPlayerBridge;
    293.   public node_controller?: MyNodeController;
    294.   public show_native_media_player: boolean = false;
    295.   public node_pos_x: number;
    296.   public node_pos_y: number;
    297.   public node_width: number;
    298.   public node_height: number;
    
    299.   playerComponent?: NativeMediaPlayerComponent;
    
    300.   constructor(web: WebComponent, handler: webview.NativeMediaPlayerHandler, videoInfo: webview.MediaInfo, uiContext: UIContext) {
    301.     this.web = web;
    302.     this.embed_id = videoInfo.embedID;
    
    303.     let node_rect = Rect.toNodeRect(videoInfo.surfaceInfo.rect, uiContext);
    304.     this.node_pos_x = node_rect.x;
    305.     this.node_pos_y = node_rect.y;
    306.     this.node_width = node_rect.width;
    307.     this.node_height = node_rect.height;
    
    308.     this.player = new NativeMediaPlayerImpl(this, handler, videoInfo, uiContext);
    309.   }
    
    310.   updateNativePlayerRect(x: number, y: number, width: number, height: number) {
    311.     this.playerComponent?.updateNativePlayerRect(x, y, width, height);
    312.   }
    
    313.   destroyed() {
    314.     let info_list = this.web.native_player_info_list;
    315.     console.info(`NativePlayerInfo[${this.embed_id}] destroyed, list.size[${info_list.length}]`);
    316.     this.web.native_player_info_list = info_list.filter((item) => item.embed_id != this.embed_id);
    317.     console.info(`NativePlayerInfo after destroyed, new_list.size[${this.web.native_player_info_list.length}]`);
    318.   }
    319. }
    
    320. @Component
    321. struct NativeMediaPlayerComponent {
    322.   @ObjectLink playerInfo: NativePlayerInfo;
    
    323.   aboutToAppear() {
    324.     this.playerInfo.playerComponent = this;
    325.   }
    
    326.   build() {
    327.     NodeContainer(this.playerInfo.node_controller)
    328.       .width(this.playerInfo.node_width)
    329.       .height(this.playerInfo.node_height)
    330.       .offset({x: this.playerInfo.node_pos_x, y: this.playerInfo.node_pos_y})
    331.       .backgroundColor(Color.Transparent)
    332.       .border({ width: 2, color: Color.Orange })
    333.       .onAreaChange((oldValue, newValue) => {
    334.         console.info(`NodeContainer[${this.playerInfo.embed_id}].onAreaChange([${oldValue.width} x ${oldValue.height}]->[${newValue.width} x ${newValue.height}]`);
    335.       })
    336.   }
    
    337.   updateNativePlayerRect(x: number, y: number, width: number, height: number) {
    338.     let node_rect = Rect.toNodeRect({x, y, width, height}, this.getUIContext());
    339.     this.playerInfo.node_pos_x = node_rect.x;
    340.     this.playerInfo.node_pos_y = node_rect.y;
    341.     this.playerInfo.node_width = node_rect.width;
    342.     this.playerInfo.node_height = node_rect.height;
    343.   }
    344. }
    
    345. @Entry
    346. @Component
    347. struct WebComponent {
    348.   controller: WebviewController = new webview.WebviewController();
    349.   page_url: Resource = $rawfile('main.html');
    
    350.   @State native_player_info_list: NativePlayerInfo[] = [];
    
    351.   area?: Area;
    
    352.   build() {
    353.     Column() {
    354.       Stack({alignContent: Alignment.TopStart}) {
    355.         ForEach(this.native_player_info_list, (item: NativePlayerInfo) => {
    356.           if (item.show_native_media_player) {
    357.             NativeMediaPlayerComponent({ playerInfo: item })
    358.           }
    359.         }, (item: NativePlayerInfo) => {
    360.           return item.embed_id;
    361.         })
    362.         Web({ src: this.page_url, controller: this.controller })
    363.           .enableNativeMediaPlayer({ enable: true, shouldOverlay: true })
    364.           .onPageBegin(() => {
    365.             this.controller.onCreateNativeMediaPlayer((handler: webview.NativeMediaPlayerHandler, mediaInfo: webview.MediaInfo) => {
    366.               console.info('onCreateNativeMediaPlayer(' + JSON.stringify(mediaInfo) + ')');
    367.               let nativePlayerInfo = new NativePlayerInfo(this, handler, mediaInfo, this.getUIContext());
    368.               this.native_player_info_list.push(nativePlayerInfo);
    369.               return nativePlayerInfo.player;
    370.             });
    371.           })
    372.           .onNativeEmbedGestureEvent((event)=>{
    373.             if (!event.touchEvent || !event.embedId) {
    374.               event.result?.setGestureEventResult(false);
    375.               return;
    376.             }
    377.             console.info(`WebComponent.onNativeEmbedGestureEvent, embedId[${event.embedId}]`);
    378.             let native_player_info = this.getNativePlayerInfoByEmbedId(event.embedId);
    379.             if (!native_player_info) {
    380.               console.info(`WebComponent.onNativeEmbedGestureEvent, embedId[${event.embedId}], no native_player_info`);
    381.               event.result?.setGestureEventResult(false);
    382.               return;
    383.             }
    384.             if (!native_player_info.node_controller) {
    385.               console.info(`WebComponent.onNativeEmbedGestureEvent, embedId[${event.embedId}], no node_controller`);
    386.               event.result?.setGestureEventResult(false);
    387.               return;
    388.             }
    389.             let ret = native_player_info.node_controller.postTouchEvent(event.touchEvent);
    390.             console.info(`WebComponent.postTouchEvent, ret[${ret}], touchEvent[${JSON.stringify(event.touchEvent)}]`);
    391.             event.result?.setGestureEventResult(ret);
    392.           })
    393.           .width('100%')
    394.           .height('100%')
    395.           .onAreaChange((oldValue: Area, newValue: Area) => {
    396.             oldValue;
    397.             this.area = newValue;
    398.           })
    399.       }
    400.     }
    401.   }
    
    402.   getNativePlayerInfoByEmbedId(embedId: string) : NativePlayerInfo | undefined {
    403.     return this.native_player_info_list.find((item)=> item.embed_id == embedId);
    404.   }
    405. }
    
- 应用侧代码，视频播放示例, ./PlayerDemo.ets。
    
    1. import { media } from '@kit.MediaKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
    3. export interface AVPlayerListener {
    4.   onPlaying() : void;
    5.   onPaused() : void;
    6.   onDurationChanged(duration: number) : void;
    7.   onBufferedTimeChanged(buffered: number) : void;
    8.   onTimeUpdate(time: number) : void;
    9.   onEnded() : void;
    10.   onError() : void;
    11.   onVideoSizeChanged(width: number, height: number): void;
    12.   onDestroyed(): void;
    13. }
    
    14. interface PlayerParam {
    15.   url: string;
    16.   listener?: AVPlayerListener;
    17.   httpHeaders?: Record<string, string>;
    18. }
    
    19. interface PlayCommand {
    20.   func: Function;
    21.   name?: string;
    22. }
    
    23. interface CheckPlayCommandResult {
    24.   ignore: boolean;
    25.   index_to_remove: number;
    26. }
    
    27. export class AVPlayerDemo {
    28.   private surfaceID: string = ''; // surfaceID用于播放画面显示，具体的值需要通过Xcomponent接口获取，相关文档链接见上面Xcomponent创建方法
    
    29.   avPlayer?: media.AVPlayer;
    30.   prepared: boolean = false;
    
    31.   commands: PlayCommand[] = [];
    
    32.   setSurfaceID(surface_id: string) {
    33.     console.info(`AVPlayerDemo.setSurfaceID : ${surface_id}`);
    34.     this.surfaceID = surface_id;
    35.   }
    36.   // 注册avplayer回调函数
    37.   setAVPlayerCallback(avPlayer: media.AVPlayer, listener?: AVPlayerListener) {
    38.     // seek操作结果回调函数
    39.     avPlayer.on('seekDone', (seekDoneTime: number) => {
    40.       console.info(`AVPlayer seek succeeded, seek time is ${seekDoneTime}`);
    41.     });
    42.     // error回调监听函数,当avPlayer在操作过程中出现错误时调用reset接口触发重置流程
    43.     avPlayer.on('error', (err: BusinessError) => {
    44.       console.error(`Invoke avPlayer failed, code is ${err.code}, message is ${err.message}`);
    45.       listener?.onError();
    46.       avPlayer.reset(); // 调用reset重置资源，触发idle状态
    47.     });
    48.     // 状态机变化回调函数
    49.     avPlayer.on('stateChange', async (state: string, reason: media.StateChangeReason) => {
    50.       switch (state) {
    51.         case 'idle': // 成功调用reset接口后触发该状态机上报
    52.           console.info('AVPlayer state idle called.');
    53.           avPlayer.release(); // 调用release接口销毁实例对象
    54.           break;
    55.         case 'initialized': // avplayer 设置播放源后触发该状态上报
    56.           console.info('AVPlayer state initialized called.');
    57.           avPlayer.surfaceId = this.surfaceID; // 设置显示画面，当播放的资源为纯音频时无需设置
    58.           avPlayer.prepare();
    59.           break;
    60.         case 'prepared': // prepare调用成功后上报该状态机
    61.           console.info('AVPlayer state prepared called.');
    62.           this.prepared = true;
    63.           this.schedule();
    64.           break;
    65.         case 'playing': // play成功调用后触发该状态机上报
    66.           console.info('AVPlayer state playing called.');
    67.           listener?.onPlaying();
    68.           break;
    69.         case 'paused': // pause成功调用后触发该状态机上报
    70.           console.info('AVPlayer state paused called.');
    71.           listener?.onPaused();
    72.           break;
    73.         case 'completed': // 播放结束后触发该状态机上报
    74.           console.info('AVPlayer state completed called.');
    75.           avPlayer.stop(); //调用播放结束接口
    76.           break;
    77.         case 'stopped': // stop接口成功调用后触发该状态机上报
    78.           console.info('AVPlayer state stopped called.');
    79.           listener?.onEnded();
    80.           break;
    81.         case 'released':
    82.           this.prepared = false;
    83.           listener?.onDestroyed();
    84.           console.info('AVPlayer state released called.');
    85.           break;
    86.         default:
    87.           console.info('AVPlayer state unknown called.');
    88.           break;
    89.       }
    90.     });
    91.     avPlayer.on('durationUpdate', (duration: number) => {
    92.       console.info(`AVPlayer state durationUpdate success,new duration is :${duration}`);
    93.       listener?.onDurationChanged(duration/1000);
    94.     });
    95.     avPlayer.on('timeUpdate', (time:number) => {
    96.       listener?.onTimeUpdate(time/1000);
    97.     });
    98.     avPlayer.on('bufferingUpdate', (infoType: media.BufferingInfoType, value: number) => {
    99.       console.info(`AVPlayer state bufferingUpdate success,and infoType value is:${infoType}, value is : ${value}`);
    100.       listener?.onBufferedTimeChanged(value);
    101.     })
    102.     avPlayer.on('videoSizeChange', (width: number, height: number) => {
    103.       console.info(`AVPlayer state videoSizeChange success,and width is:${width}, height is : ${height}`);
    104.       listener?.onVideoSizeChanged(width, height);
    105.     })
    106.   }
    
    107.   // 以下示例通过URL设置网络地址来播放直播码流
    108.   async avPlayerLiveDemo(playerParam: PlayerParam) {
    109.     // 创建avPlayer实例对象
    110.     this.avPlayer = await media.createAVPlayer();
    111.     // 创建状态机变化回调函数
    112.     this.setAVPlayerCallback(this.avPlayer, playerParam.listener);
    
    113.     let mediaSource: media.MediaSource = media.createMediaSourceWithUrl(playerParam.url, playerParam.httpHeaders);
    114.     let strategy: media.PlaybackStrategy = {
    115.       preferredWidth: 100,
    116.       preferredHeight: 100,
    117.       preferredBufferDuration: 100,
    118.       preferredHdr: false
    119.     };
    120.     this.avPlayer.setMediaSource(mediaSource, strategy);
    121.     console.info(`AVPlayer url:[${playerParam.url}]`);
    122.   }
    
    123.   schedule() {
    124.     if (!this.avPlayer) {
    125.       return;
    126.     }
    127.     if (!this.prepared) {
    128.       return;
    129.     }
    130.     if (this.commands.length > 0) {
    131.       let command = this.commands.shift();
    132.       if (command) {
    133.         command.func();
    134.       }
    135.       if (this.commands.length > 0) {
    136.         setTimeout(() => {
    137.           this.schedule();
    138.         });
    139.       }
    140.     }
    141.   }
    
    142.   private checkCommand(selfName: string, oppositeName: string) {
    143.     let index_to_remove = -1;
    144.     let ignore_this_action = false;
    145.     let index = this.commands.length - 1;
    146.     while (index >= 0) {
    147.       if (this.commands[index].name == selfName) {
    148.         ignore_this_action = true;
    149.         break;
    150.       }
    151.       if (this.commands[index].name == oppositeName) {
    152.         index_to_remove = index;
    153.         break;
    154.       }
    155.       index--;
    156.     }
    
    157.     let result : CheckPlayCommandResult = {
    158.       ignore: ignore_this_action,
    159.       index_to_remove: index_to_remove,
    160.     };
    161.     return result;
    162.   }
    
    163.   play() {
    164.     let commandName = 'play';
    165.     let checkResult = this.checkCommand(commandName, 'pause');
    166.     if (checkResult.ignore) {
    167.       console.info(`AVPlayer ${commandName} ignored.`);
    168.       this.schedule();
    169.       return;
    170.     }
    171.     if (checkResult.index_to_remove >= 0) {
    172.       let removedCommand = this.commands.splice(checkResult.index_to_remove, 1);
    173.       console.info(`AVPlayer ${JSON.stringify(removedCommand)} removed.`);
    174.       return;
    175.     }
    176.     this.commands.push({ func: ()=>{
    177.       console.info('AVPlayer.play()');
    178.       this.avPlayer?.play();
    179.     }, name: commandName});
    180.     this.schedule();
    181.   }
    182.   pause() {
    183.     let commandName = 'pause';
    184.     let checkResult = this.checkCommand(commandName, 'play');
    185.     console.info(`checkResult:${JSON.stringify(checkResult)}`);
    186.     if (checkResult.ignore) {
    187.       console.info(`AVPlayer ${commandName} ignored.`);
    188.       this.schedule();
    189.       return;
    190.     }
    191.     if (checkResult.index_to_remove >= 0) {
    192.       let removedCommand = this.commands.splice(checkResult.index_to_remove, 1);
    193.       console.info(`AVPlayer ${JSON.stringify(removedCommand)} removed.`);
    194.       return;
    195.     }
    196.     this.commands.push({ func: ()=>{
    197.       console.info('AVPlayer.pause()');
    198.       this.avPlayer?.pause();
    199.     }, name: commandName});
    200.     this.schedule();
    201.   }
    202.   release() {
    203.     this.commands.push({ func: ()=>{
    204.       console.info('AVPlayer.release()');
    205.       this.avPlayer?.release();
    206.     }});
    207.     this.schedule();
    208.   }
    209.   seek(time: number) {
    210.     this.commands.push({ func: ()=>{
    211.       console.info(`AVPlayer.seek(${time})`);
    212.       this.avPlayer?.seek(time * 1000);
    213.     }});
    214.     this.schedule();
    215.   }
    216.   setVolume(volume: number) {
    217.     this.commands.push({ func: ()=>{
    218.       console.info(`AVPlayer.setVolume(${volume})`);
    219.       this.avPlayer?.setVolume(volume);
    220.     }});
    221.     this.schedule();
    222.   }
    223.   setPlaybackRate(playbackRate: number) {
    224.     let speed = media.PlaybackSpeed.SPEED_FORWARD_1_00_X;
    225.     let delta = 0.05;
    226.     playbackRate += delta;
    227.     if (playbackRate < 1) {
    228.       speed = media.PlaybackSpeed.SPEED_FORWARD_0_75_X;
    229.     } else if (playbackRate < 1.25) {
    230.       speed = media.PlaybackSpeed.SPEED_FORWARD_1_00_X;
    231.     } else if (playbackRate < 1.5) {
    232.       speed = media.PlaybackSpeed.SPEED_FORWARD_1_25_X;
    233.     } else if (playbackRate < 2) {
    234.       speed = media.PlaybackSpeed.SPEED_FORWARD_1_75_X;
    235.     } else {
    236.       speed = media.PlaybackSpeed.SPEED_FORWARD_2_00_X;
    237.     }
    238.     this.commands.push({ func: ()=>{
    239.       console.info(`AVPlayer.setSpeed(${speed})`);
    240.       this.avPlayer?.setSpeed(speed);
    241.     }});
    242.     this.schedule();
    243.   }
    244. }
    
- 前端页面示例。通过[AVPlayer](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/media-kit-intro#avplayer)托管Web媒体的播放，支持的媒体资源可以参考AVPlayer[支持的格式与协议](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/media-kit-intro#%E6%94%AF%E6%8C%81%E7%9A%84%E6%A0%BC%E5%BC%8F%E4%B8%8E%E5%8D%8F%E8%AE%AE)。
    
    1. <!-- main.html -->
    2. <html>
    3. <head>
    4.     <title>视频托管测试html</title>
    5.     <meta name="viewport" content="width=device-width">
    6. </head>
    7. <body>
    8. <div>
    9.     <!-- 使用时需要自行替换视频链接 -->
    10.     <video src='https://xxx.xxx/demo.mp4' style='width: 100%'></video>
    11. </div>
    12. </body>
    13. </html>
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-rtc "在Web中打开摄像头和麦克风")
# Web组件支持视频沉浸式全屏播放

更新时间: 2025-12-16 16:38

Web组件提供了视频进入全屏和退出全屏的事件功能，应用可通过监听这些事件实现进入和退出沉浸式全屏模式。

Web组件引用第三方H5页面加载的视频，当点击视频全屏时，视频仅扩展至整个Web组件区域，无法实现系统全屏显示（如图2所示）。若要达到系统全屏的沉浸式视频播放效果（如图3所示），则需应用监听进入全屏的事件并调整页面其他组件的属性。

|图1 退出全屏模式|图2 非沉浸式全屏模式|图3 沉浸式全屏模式|
|:--|:--|:--|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163844.29076053124377883152795357403158:50001231000000:2800:624EE4DBD4D4A6323467B90C5C96164A4461368BED0C04409B066F5AB465BB07.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163844.45632429296801875004455961969337:50001231000000:2800:F7A3107ADA033EF774432A03EDE7B8E15FFC32EFD2350F0CB70B5BFEE80CF140.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163844.08027203312272779559243139798576:50001231000000:2800:8C18F773C00AC3D1C883FAF60F53C8C2F0F8B5DDC09B6F52C09B8B139F50F384.png)|

Web组件可通过[onFullScreenEnter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onfullscreenenter9)和[onFullScreenExit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onfullscreenexit9)回调监听全屏按键的点击事件。其中，onFullScreenEnter表示Web组件进入全屏模式，onFullScreenExit表示Web组件退出全屏模式。在这两个监听事件中，可根据具体业务场景调整某些全局变量，例如组件的显隐状态、组件的margin属性等，以实现退出和进入沉浸式全屏模式的页面效果，如图1和图3所示。

显隐控制[visibility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-visibility#visibility)是ArkUI开发框架提供的组件通用属性。开发者可通过设置组件属性visibility的不同值，控制组件的显隐状态。

1. import { webview } from '@kit.ArkWeb';

2. @Entry
3. @Component
4. struct ShortWebPage {
5.   controller: webview.WebviewController = new webview.WebviewController()
6.   CONSTANT_HEIGHT = 100;
7.   @State marginTop: number = this.CONSTANT_HEIGHT;
8.   @State isVisible: boolean = true; // 自定义标志位isVisible，来控制是否需要显示组件

9.   build() {
10.     Column() {
11.       Text('TextTextTextText')
12.         .width('100%')
13.         .height(this.CONSTANT_HEIGHT)
14.         .backgroundColor('#e1dede') // 当isVisible标志位为true的时候，组件状态为可见，否则组件状态为不可见，不参与布局、不进行占位
15.         .visibility(this.isVisible ? Visibility.Visible :
16.         Visibility.None)
17.       Web({
18.         src: "http://www.example.com", // 示例网址
19.         controller: this.controller
20.       })
21.         .onFullScreenEnter((event) => {
22.           console.info("onFullScreenEnter...")
23.           // 当全屏的时候，isVisible标志位为false，组件状态为不可见，不参与布局、不进行占位
24.           this.isVisible = false;
25.         })
26.         .onFullScreenExit(() => {
27.           console.info("onFullScreenExit...")
28.           // 当退出全屏的时候，isVisible标志位为true，组件状态为可见
29.           this.isVisible = true;
30.         })
31.         .width('100%')
32.         .height("100%")
33.         .zIndex(10)
34.         .zoomAccess(true)
35.     }.width('100%').height('100%')
36.   }
37. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-picture-in-picture "Web组件支持画中画")
# Web组件支持视频沉浸式全屏播放

更新时间: 2025-12-16 16:38

Web组件提供了视频进入全屏和退出全屏的事件功能，应用可通过监听这些事件实现进入和退出沉浸式全屏模式。

Web组件引用第三方H5页面加载的视频，当点击视频全屏时，视频仅扩展至整个Web组件区域，无法实现系统全屏显示（如图2所示）。若要达到系统全屏的沉浸式视频播放效果（如图3所示），则需应用监听进入全屏的事件并调整页面其他组件的属性。

|图1 退出全屏模式|图2 非沉浸式全屏模式|图3 沉浸式全屏模式|
|:--|:--|:--|
|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163844.29076053124377883152795357403158:50001231000000:2800:624EE4DBD4D4A6323467B90C5C96164A4461368BED0C04409B066F5AB465BB07.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163844.45632429296801875004455961969337:50001231000000:2800:F7A3107ADA033EF774432A03EDE7B8E15FFC32EFD2350F0CB70B5BFEE80CF140.png)|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163844.08027203312272779559243139798576:50001231000000:2800:8C18F773C00AC3D1C883FAF60F53C8C2F0F8B5DDC09B6F52C09B8B139F50F384.png)|

Web组件可通过[onFullScreenEnter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onfullscreenenter9)和[onFullScreenExit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onfullscreenexit9)回调监听全屏按键的点击事件。其中，onFullScreenEnter表示Web组件进入全屏模式，onFullScreenExit表示Web组件退出全屏模式。在这两个监听事件中，可根据具体业务场景调整某些全局变量，例如组件的显隐状态、组件的margin属性等，以实现退出和进入沉浸式全屏模式的页面效果，如图1和图3所示。

显隐控制[visibility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-visibility#visibility)是ArkUI开发框架提供的组件通用属性。开发者可通过设置组件属性visibility的不同值，控制组件的显隐状态。

1. import { webview } from '@kit.ArkWeb';

2. @Entry
3. @Component
4. struct ShortWebPage {
5.   controller: webview.WebviewController = new webview.WebviewController()
6.   CONSTANT_HEIGHT = 100;
7.   @State marginTop: number = this.CONSTANT_HEIGHT;
8.   @State isVisible: boolean = true; // 自定义标志位isVisible，来控制是否需要显示组件

9.   build() {
10.     Column() {
11.       Text('TextTextTextText')
12.         .width('100%')
13.         .height(this.CONSTANT_HEIGHT)
14.         .backgroundColor('#e1dede') // 当isVisible标志位为true的时候，组件状态为可见，否则组件状态为不可见，不参与布局、不进行占位
15.         .visibility(this.isVisible ? Visibility.Visible :
16.         Visibility.None)
17.       Web({
18.         src: "http://www.example.com", // 示例网址
19.         controller: this.controller
20.       })
21.         .onFullScreenEnter((event) => {
22.           console.info("onFullScreenEnter...")
23.           // 当全屏的时候，isVisible标志位为false，组件状态为不可见，不参与布局、不进行占位
24.           this.isVisible = false;
25.         })
26.         .onFullScreenExit(() => {
27.           console.info("onFullScreenExit...")
28.           // 当退出全屏的时候，isVisible标志位为true，组件状态为可见
29.           this.isVisible = true;
30.         })
31.         .width('100%')
32.         .height("100%")
33.         .zIndex(10)
34.         .zoomAccess(true)
35.     }.width('100%').height('100%')
36.   }
37. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-picture-in-picture "Web组件支持画中画")
# 使用Web组件打印前端页面

更新时间: 2025-12-16 16:38

Web组件打印html页面时可通过W3C标准协议接口和应用接口两种方式实现。

使用打印功能前，请在module.json5中配置相关权限，添加方法请参考[在配置文件中声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。

1. "requestPermissions":[
2.     {
3.       "name" : "ohos.permission.PRINT"
4.     }
5.   ]

## 使用W3C标准协议接口拉起打印

通过创建打印适配器，拉起打印应用，并对当前Web页面内容进行渲染，渲染后生成的PDF文件信息通过fd传递给打印框架。W3C标准协议接口window.print()方法用于打印当前页面或弹出打印对话框。该方法没有任何参数，只需要在JavaScript中调用即可。

可通过前端css样式控制是否打印，例如@media print。再通过web加载该html页面的方式运行。

- print.html页面代码。
    
    示例一：
    
    1. <!DOCTYPE html>
    2. <html>
    
    3. <head>
    4.     <meta charset="utf-8">
    5.     <title>printTest</title>
    6.     <style>
    7.         @media print {
    8.             h1 {
    9.                 display: none;
    10.             }
    11.         }
    12.     </style>
    13. </head>
    
    14. <body>
    15.     <div>
    16.         <h1><b>
    17.                 <p style="text-align: center;">This is a test page for printing</p>
    18.             </b>
    19.             <hr color="#00cc00" width="95%">
    20.         </h1>
    21.         <button class="Button Button--outline" onclick="window.print();">Print</button>
    22.         <p> content content content </p>
    23.         <div id="printableTable">
    24.             <table>
    25.                 <thead>
    26.                     <tr>
    27.                         <td>Thing</td>
    28.                         <td>Chairs</td>
    29.                     </tr>
    30.                 </thead>
    31.                 <tbody>
    32.                     <tr>
    33.                         <td>1</td>
    34.                         <td>blue</td>
    35.                     </tr>
    36.                     <tr>
    37.                         <td>2</td>
    38.                         <td>green</td>
    39.                     </tr>
    40.                 </tbody>
    41.             </table>
    42.         </div>
    43.         <p> content content content </p>
    44.         <p> content content content </p>
    45.     </div>
    46. </body>
    
    示例二（iframe嵌套页面的方式）：
    
    47. <!DOCTYPE html>
    48. <html lang="en">
    49. <head>
    50.     <meta charset="UTF-8">
    51.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
    52.     <title>iframe嵌套页面打印</title>
    53. </head>
    54. <body>
    55.     <button id="printIframe">打印iframe嵌套页面</button>
    56.     <iframe id="contentIframe" hidden></iframe>
    
    57.     <script>
    58.         document.getElementById("printIframe").addEventListener("click", () => {
    59.             var ctIframe = document.getElementById("contentIframe");
    60.             if(!ctIframe.contentWindow || !ctIframe.contentWindow.document) {
    61.               console.error("iframe页面初始化失败");
    62.               return;
    63.             }
    64.             var ctIframeDoc = ctIframe.contentWindow.document;
    65.             ctIframeDoc.write("嵌套页面");
    66.             ctIframeDoc.close();
    67.             ctIframe.contentWindow.print();
    68.         });
    69.     </script>
    70. </body>
    71. </html>
    
- 应用侧代码。
    
    1. import { webview } from '@kit.ArkWeb';
    
    2. @Entry
    3. @Component
    4. struct Index {
    5.   controller: webview.WebviewController = new webview.WebviewController();
    
    6.   build() {
    7.     Row() {
    8.       Column() {
    9.         Web({ src: $rawfile("print.html"), controller: this.controller })
    10.           .javaScriptAccess(true)
    11.       }
    12.       .width('100%')
    13.     }
    14.     .height('100%')
    15.   }
    16. }
    

## 通过调用应用侧接口拉起打印

应用侧通过调用[createWebPrintDocumentAdapter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#createwebprintdocumentadapter11)创建打印适配器，通过将适配器传入打印的print接口调起打印。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError, print } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct WebComponent {
7.   controller: webview.WebviewController = new webview.WebviewController();

8.   build() {
9.     Column() {
10.       Button('createWebPrintDocumentAdapter')
11.         .onClick(() => {
12.           try {
13.             let webPrintDocadapter = this.controller.createWebPrintDocumentAdapter('example.pdf');
14.             print.print('example_job_id', webPrintDocadapter, null, this.getUIContext().getHostContext());
15.           } catch (error) {
16.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
17.           }
18.         })
19.       Web({ src: 'www.example.com', controller: this.controller })
20.     }
21.   }
22. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-process-page-content "处理网页内容")
# 使用Web组件保存前端页面为PDF

更新时间: 2025-12-16 16:38

从API version 14开始，支持使用Web组件的[createPdf](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#createpdf14)方法，为应用提供了保存前端页面为PDF的功能。

通过[createPdf](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#createpdf14)生成实例后，调用pdfArrayBuffer方法获取二进制数据流，再使用fileIo方法将二进制数据流保存为PDF文件。用户可以将前端页面内容保存为PDF以便分享或保存。例如，生成报告、发票等，方便用户保存和传输。

## 需要权限

若涉及网络文档获取，需在module.json5中配置网络访问权限。具体添加方法请参考[在配置文件中声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。

1. "requestPermissions":[
2.     {
3.       "name" : "ohos.permission.INTERNET"
4.     }
5.   ]

## callback方式保存PDF

通过callback方式调用createPdf接口，获取到的result通过pdfArrayBuffer接口取得PDF二进制数据流，最后使用fileIo方法将二进制数据流保存为PDF文件。

1. import { fileIo as fs } from '@kit.CoreFileKit';
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';
4. import { common } from '@kit.AbilityKit';

5. @Entry
6. @Component
7. struct Index {
8.   controller: webview.WebviewController = new webview.WebviewController();
9.   pdfConfig: webview.PdfConfiguration = {
10.     width: 8.27,
11.     height: 11.69,
12.     marginTop: 0,
13.     marginBottom: 0,
14.     marginRight: 0,
15.     marginLeft: 0,
16.     shouldPrintBackground: true
17.   }

18.   build() {
19.     Column() {
20.       Button('SavePDF')
21.         .onClick(() => {
22.           // 触发PDF生成，需要确保页面渲染完成，可使用onPageEnd事件监听
23.           this.controller.createPdf(
24.             this.pdfConfig,
25.             (error, result: webview.PdfData) => {
26.               try {
27.                 // 获取到的result通过`pdfArrayBuffer`接口取得PDF二进制数据流，最后使用`fileIo`方法将二进制数据流保存为PDF文件
28.                 let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
29.                 let filePath = context.filesDir + "/test.pdf";
30.                 let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
31.                 fs.write(file.fd, result.pdfArrayBuffer().buffer).then((writeLen: number) => {
32.                   console.info("createPDF write data to file succeed and size is:" + writeLen);
33.                 }).catch((err: BusinessError) => {
34.                   console.error("createPDF write data to file failed with error message: " + err.message +
35.                     ", error code: " + err.code);
36.                 }).finally(() => {
37.                   // 关闭file
38.                   fs.closeSync(file);
39.                 });
40.               } catch (resError) {
41.                 console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
42.               }
43.             });
44.         })
45.       Web({ src: "www.example.com", controller: this.controller })
46.     }
47.   }
48. }

## Promise方式保存PDF

通过Promise方式调用createPdf接口，获取到的result通过pdfArrayBuffer接口取得PDF二进制数据流，最后使用fileIo方法将二进制数据流保存为PDF文件。

1. import { fileIo as fs } from '@kit.CoreFileKit';
2. import { webview } from '@kit.ArkWeb';
3. import { BusinessError } from '@kit.BasicServicesKit';
4. import { common } from '@kit.AbilityKit';

5. @Entry
6. @Component
7. struct Index {
8.   controller: webview.WebviewController = new webview.WebviewController();
9.   pdfConfig: webview.PdfConfiguration = {
10.     width: 8.27,
11.     height: 11.69,
12.     marginTop: 0,
13.     marginBottom: 0,
14.     marginRight: 0,
15.     marginLeft: 0,
16.     shouldPrintBackground: true
17.   }

18.   build() {
19.     Column() {
20.       Button('SavePDF')
21.         .onClick(() => {
22.           // 触发PDF生成，需要确保页面渲染完成，可使用onPageEnd事件监听
23.           this.controller.createPdf(this.pdfConfig)
24.             .then((result: webview.PdfData) => {
25.               try {
26.                 // 获取到的result通过`pdfArrayBuffer`接口取得PDF二进制数据流，最后使用`fileIo`方法将二进制数据流保存为PDF文件
27.                 let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
28.                 let filePath = context.filesDir + "/test.pdf";
29.                 let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
30.                 fs.write(file.fd, result.pdfArrayBuffer().buffer).then((writeLen: number) => {
31.                   console.info("createPDF write data to file succeed and size is:" + writeLen);
32.                 }).catch((err: BusinessError) => {
33.                   console.error("createPDF write data to file failed with error message: " + err.message +
34.                     ", error code: " + err.code);
35.                 }).finally(() => {
36.                   // 关闭file
37.                   fs.closeSync(file);
38.                 });
39.               } catch (resError) {
40.                 console.error(`ErrorCode: ${(resError as BusinessError).code},  Message: ${(resError as BusinessError).message}`);
41.               }
42.             })
43.         })
44.       Web({ src: "www.example.com", controller: this.controller })
45.     }
46.   }
47. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-print "使用Web组件打印前端页面")
# 使用Web组件菜单处理网页内容

更新时间: 2025-12-16 16:38

菜单作为用户交互的关键组件，其作用是构建清晰的导航体系，通过结构化布局展示功能入口，使用户能够迅速找到目标内容或执行操作。作为人机交互的重要枢纽，它显著提升了Web组件的可访问性和用户体验，是应用设计中必不可少的部分。Web组件菜单类型包括[文本选中菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E6%96%87%E6%9C%AC%E9%80%89%E4%B8%AD%E8%8F%9C%E5%8D%95)、[上下文菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E4%B8%8A%E4%B8%8B%E6%96%87%E8%8F%9C%E5%8D%95)和[自定义菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%8F%9C%E5%8D%95)，应用可根据具体需求灵活选择。

|菜单类型|目标元素|响应类型|是否支持自定义|
|:--|:--|:--|:--|
|[文本选中菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E6%96%87%E6%9C%AC%E9%80%89%E4%B8%AD%E8%8F%9C%E5%8D%95)|文本|手势长按|可增减菜单项，菜单样式不可自定义|
|[上下文菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E4%B8%8A%E4%B8%8B%E6%96%87%E8%8F%9C%E5%8D%95)|超链接、图片、文字|手势长按、鼠标右键|支持通过菜单组件自定义|
|[自定义菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%8F%9C%E5%8D%95)|图片|手势长按|支持通过菜单组件自定义|

## 文本选中菜单

Web组件的文本选中菜单是一种通过自定义元素实现的上下文交互组件，当用户选中文本时会动态显示，提供复制、分享、标注等语义化操作，具备标准化功能与可扩展性，是移动端文本操作的核心功能。文本选中菜单在用户长按选中文本或编辑状态下长按出现单手柄时弹出，菜单项横向排列。系统提供默认的菜单实现。应用可通过[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)接口对文本选中菜单进行自定义操作。

1. 通过onCreateMenu方法自定义菜单项，通过操作Array<[TextMenuItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-text-common#textmenuitem12%E5%AF%B9%E8%B1%A1%E8%AF%B4%E6%98%8E)>数组可对显示菜单项进行增减操作，在[TextMenuItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-text-common#textmenuitem12%E5%AF%B9%E8%B1%A1%E8%AF%B4%E6%98%8E)中定义菜单项名称、图标、ID等内容。
2. 通过onMenuItemClick方法处理菜单项点击事件，当返回false时会执行系统默认逻辑。
3. 创建一个[EditMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-text-common#editmenuoptions)对象，包含onCreateMenu和onMenuItemClick两个方法，通过Web组件的[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)方法与Web组件绑定。

4. // xxx.ets
5. import { webview } from '@kit.ArkWeb';

6. @Entry
7. @Component
8. struct WebComponent {
9.   controller: webview.WebviewController = new webview.WebviewController();

10.   onCreateMenu(menuItems: Array<TextMenuItem>): Array<TextMenuItem> {
11.     let items = menuItems.filter((menuItem) => {
12.       // 过滤用户需要的系统按键
13.       return (
14.         menuItem.id.equals(TextMenuItemId.CUT) ||
15.         menuItem.id.equals(TextMenuItemId.COPY) ||
16.         menuItem.id.equals(TextMenuItemId.PASTE)
17.       );
18.     });
19.     let customItem1: TextMenuItem = {
20.       content: 'customItem1',
21.       id: TextMenuItemId.of('customItem1'),
22.       icon: $r('app.media.startIcon')
23.     };
24.     let customItem2: TextMenuItem = {
25.       content: $r('app.string.EntryAbility_label'),
26.       id: TextMenuItemId.of('customItem2'),
27.       icon: $r('app.media.startIcon')
28.     };
29.     items.push(customItem1); // 在选项列表后添加新选项
30.     items.unshift(customItem2); // 在选项列表前添加选项
31.     items.push(customItem1);
32.     items.push(customItem1);
33.     items.push(customItem1);
34.     items.push(customItem1);
35.     items.push(customItem1);
36.     return items;
37.   }

38.   onMenuItemClick(menuItem: TextMenuItem, textRange: TextRange): boolean {
39.     if (menuItem.id.equals(TextMenuItemId.CUT)) {
40.       // 用户自定义行为
41.       console.info("拦截 id：CUT")
42.       return true; // 返回true不执行系统回调
43.     } else if (menuItem.id.equals(TextMenuItemId.COPY)) {
44.       // 用户自定义行为
45.       console.info("不拦截 id：COPY")
46.       return false; // 返回false执行系统回调
47.     } else if (menuItem.id.equals(TextMenuItemId.of('customItem1'))) {
48.       // 用户自定义行为
49.       console.info("拦截 id：customItem1")
50.       return true; // 用户自定义菜单选项返回true时点击后不关闭菜单，返回false时关闭菜单
51.     } else if (menuItem.id.equals(TextMenuItemId.of('customItem2'))) {
52.       // 用户自定义行为
53.       console.info("拦截 id：customItem2")
54.       return true;
55.     }
56.     return false; // 返回默认值false
57.   }

58.   @State EditMenuOptions: EditMenuOptions = { onCreateMenu: this.onCreateMenu, onMenuItemClick: this.onMenuItemClick }

59.   build() {
60.     Column() {
61.       Web({ src: $rawfile("index.html"), controller: this.controller })
62.         .editMenuOptions(this.EditMenuOptions)
63.     }
64.   }
65. }

66. <!--index.html-->
67. <!DOCTYPE html>
68. <html>
69.   <head>
70.       <title>测试网页</title>
71.   </head>
72.   <body>
73.     <h1>editMenuOptions Demo</h1>
74.     <span>edit menu options</span>
75.   </body>
76. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.74683493357399651917983596502008:50001231000000:2800:5C244201AEDBD0BBE0E393950817D83405FFC2A941DB3153458274C6BA40BF7D.gif)

## 上下文菜单

上下文菜单是用户通过特定操作（如右键点击或长按富文本）触发的快捷菜单，用于提供与当前操作对象或界面元素相关的功能选项。菜单项纵向排列。系统未提供默认实现，若应用未实现，则不显示上下文菜单。应用需要创建一个[Menu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-menu)组件并与Web绑定，在菜单弹出时可通过Web组件的[onContextMenuShow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#oncontextmenushow9)回调接口获取上下文菜单的详细信息，包括点击位置的HTML元素信息及点击位置信息。

1. [Menu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-menu)组件作为弹出的菜单，包含所有菜单项行为与样式。
2. 使用bindPopup方法将Menu组件与Web组件绑定。当上下文菜单弹出时，将显示创建的Menu组件。
3. 在onContextMenuShow回调中获取上下文菜单事件信息[onContextMenuShowEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-i#oncontextmenushowevent12)。其中param为[WebContextMenuParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-webcontextmenuparam)类型，包含点击位置对应HTML元素信息和位置信息，result为[WebContextMenuResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-webcontextmenuresult)类型，提供常见的菜单能力。

4. // xxx.ets
5. import { webview } from '@kit.ArkWeb';
6. import { pasteboard } from '@kit.BasicServicesKit';

7. const TAG = 'ContextMenu';

8. @Entry
9. @Component
10. struct WebComponent {
11.   controller: webview.WebviewController = new webview.WebviewController();
12.   private result: WebContextMenuResult | undefined = undefined;
13.   @State linkUrl: string = '';
14.   @State offsetX: number = 0;
15.   @State offsetY: number = 0;
16.   @State showMenu: boolean = false;
17.   uiContext: UIContext = this.getUIContext();

18.   @Builder
19.   // 构建自定义菜单及触发功能接口
20.   MenuBuilder() {
21.     // 以垂直列表形式显示的菜单。
22.     Menu() {
23.       // 展示菜单Menu中具体的item菜单项。
24.       MenuItem({
25.         content: '复制图片',
26.       })
27.         .width(100)
28.         .height(50)
29.         .onClick(() => {
30.           this.result?.copyImage();
31.           this.showMenu = false;
32.         })
33.       MenuItem({
34.         content: '剪切',
35.       })
36.         .width(100)
37.         .height(50)
38.         .onClick(() => {
39.           this.result?.cut();
40.           this.showMenu = false;
41.         })
42.       MenuItem({
43.         content: '复制',
44.       })
45.         .width(100)
46.         .height(50)
47.         .onClick(() => {
48.           this.result?.copy();
49.           this.showMenu = false;
50.         })
51.       MenuItem({
52.         content: '粘贴',
53.       })
54.         .width(100)
55.         .height(50)
56.         .onClick(() => {
57.           this.result?.paste();
58.           this.showMenu = false;
59.         })
60.       MenuItem({
61.         content: '复制链接',
62.       })
63.         .width(100)
64.         .height(50)
65.         .onClick(() => {
66.           let pasteData = pasteboard.createData('text/plain', this.linkUrl);
67.           pasteboard.getSystemPasteboard().setData(pasteData, (error) => {
68.             if (error) {
69.               return;
70.             }
71.           })
72.           this.showMenu = false;
73.         })
74.       MenuItem({
75.         content: '全选',
76.       })
77.         .width(100)
78.         .height(50)
79.         .onClick(() => {
80.           this.result?.selectAll();
81.           this.showMenu = false;
82.         })
83.     }
84.     .width(150)
85.     .height(300)
86.   }

87.   build() {
88.     Column() {
89.       Web({ src: $rawfile("index.html"), controller: this.controller })
90.         // 触发自定义弹窗
91.         .onContextMenuShow((event) => {
92.           if (event) {
93.             this.result = event.result
94.             console.info("x coord = " + event.param.x());
95.             console.info("link url = " + event.param.getLinkUrl());
96.             this.linkUrl = event.param.getLinkUrl();
97.           }
98.           console.info(TAG, `x: ${this.offsetX}, y: ${this.offsetY}`);
99.           this.showMenu = true;
100.           this.offsetX = 0;
101.           this.offsetY = Math.max(this.uiContext!.px2vp(event?.param.y() ?? 0) - 0, 0);
102.           return true;
103.         })
104.         .bindPopup(this.showMenu,
105.           {
106.             builder: this.MenuBuilder(),
107.             enableArrow: false,
108.             placement: Placement.LeftTop,
109.             offset: { x: this.offsetX, y: this.offsetY },
110.             mask: false,
111.             onStateChange: (e) => {
112.               if (!e.isVisible) {
113.                 this.showMenu = false;
114.                 this.result!.closeContextMenu();
115.               }
116.             }
117.           })
118.     }
119.   }
120. }

121. <!-- index.html -->
122. <!DOCTYPE html>
123. <html lang="en">
124. <body>
125.   <h1>onContextMenuShow</h1>
126.   <a href="http://www.example.com" style="font-size:27px">超链接www.example.com</a>
127.   <!--example.png为html同目录下图片-->
128.   <div><img src="example.png"></div>
129.   <p>选中文字鼠标右键弹出菜单</p>
130. </body>
131. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.29451072078178417578416765697859:50001231000000:2800:3A77588D209390352CED6A77358F1BB92F86D7587F33E8FE5723170BA62D6076.gif)

## 自定义菜单

自定义菜单赋予开发者灵活控制菜单触发时机与视觉呈现的能力，使应用能够根据用户操作场景动态匹配功能入口，显著简化开发过程中的界面适配工作，同时让交互体验更贴近用户直觉。

开发者可通过[bindSelectionMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#bindselectionmenu13)接口实现自定义菜单功能。目前，已额外支持通过长按图片、链接和文本，触发自定义菜单及自定义文本菜单。

1. 创建[Menu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-menu)组件作为菜单弹窗。
2. 通过Web组件的[bindSelectionMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#bindselectionmenu13)方法绑定MenuBuilder菜单弹窗。将[WebElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webelementtype13)设置为WebElementType.IMAGE，[responseType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webresponsetype13)设置为WebResponseType.LONG_PRESS，表示长按图片时弹出菜单。在[options](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-i#selectionmenuoptionsext13)中定义菜单显示回调onAppear、菜单消失回调onDisappear、预览窗口preview和菜单类型menuType。

3. // xxx.ets
4. import { webview } from '@kit.ArkWeb';

5. interface PreviewBuilderParam {
6.   previewImage: Resource | string | undefined;
7.   width: number;
8.   height: number;
9. }

10. @Builder function PreviewBuilderGlobal($$: PreviewBuilderParam) {
11.   Column() {
12.     Image($$.previewImage)
13.       .objectFit(ImageFit.Fill)
14.       .autoResize(true)
15.   }.width($$.width).height($$.height)
16. }

17. @Entry
18. @Component
19. struct WebComponent {
20.   controller: webview.WebviewController = new webview.WebviewController();

21.   private result: WebContextMenuResult | undefined = undefined;
22.   @State previewImage: Resource | string | undefined = undefined;
23.   @State previewWidth: number = 0;
24.   @State previewHeight: number = 0;
25.   uiContext: UIContext = this.getUIContext();

26.   @Builder
27.   MenuBuilder() {
28.     Menu() {
29.       MenuItem({ content: '复制', })
30.         .onClick(() => {
31.           this.result?.copy();
32.           this.result?.closeContextMenu();
33.         })
34.       MenuItem({ content: '全选', })
35.         .onClick(() => {
36.           this.result?.selectAll();
37.           this.result?.closeContextMenu();
38.         })
39.     }
40.   }
41.   build() {
42.     Column() {
43.       Web({ src: $rawfile("index.html"), controller: this.controller })
44.         .bindSelectionMenu(WebElementType.IMAGE, this.MenuBuilder, WebResponseType.LONG_PRESS,
45.           {
46.             onAppear: () => {},
47.             onDisappear: () => {
48.               this.result?.closeContextMenu();
49.             },
50.             preview: PreviewBuilderGlobal({
51.               previewImage: this.previewImage,
52.               width: this.previewWidth,
53.               height: this.previewHeight
54.             }),
55.             menuType: MenuType.PREVIEW_MENU
56.           })
57.         .onContextMenuShow((event) => {
58.             if (event) {
59.               this.result = event.result;
60.               if (event.param.getLinkUrl()) {
61.                 return false;
62.               }
63.               this.previewWidth = this.uiContext!.px2vp(event.param.getPreviewWidth());
64.               this.previewHeight = this.uiContext!.px2vp(event.param.getPreviewHeight());
65.               if (event.param.getSourceUrl().indexOf("resource://rawfile/") == 0) {
66.                 this.previewImage = $rawfile(event.param.getSourceUrl().substr(19));
67.               } else {
68.                 this.previewImage = event.param.getSourceUrl();
69.               }
70.               return true;
71.             }
72.             return false;
73.           })
74.     }
75.   }
76. }

77. <!--index.html-->
78. <!DOCTYPE html>
79. <html>
80.   <head>
81.       <title>测试网页</title>
82.   </head>
83.   <body>
84.     <h1>bindSelectionMenu Demo</h1>
85.     <!--img.png为html同目录下图片-->
86.     <img src="./img.png" >
87.   </body>
88. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.59434873944830234144482178513845:50001231000000:2800:1B04AF1C73E70FDF30D79EF1FE13DCFD9AA0AC6DC2DC838A7687153EADBA00DB.gif)

自API version 20起，支持绑定长按超链接菜单。可以为图片和链接绑定不同的自定义菜单。

以下示例中，PreviewBuilder定义了超链接对应菜单的弹出内容，用Web组件加载了超链接内容，使用[Progress组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-progress-indicator)展示了加载进度。

1. import { webview } from '@kit.ArkWeb';
2. import { pasteboard } from '@kit.BasicServicesKit';

3. interface PreviewBuilderParam {
4.   width: number;
5.   height: number;
6.   url:Resource | string | undefined;
7. }

8. interface PreviewBuilderParamForImage {
9.   previewImage: Resource | string | undefined;
10.   width: number;
11.   height: number;
12. }

13. @Builder function PreviewBuilderGlobalForImage($$: PreviewBuilderParamForImage) {
14.   Column() {
15.     Image($$.previewImage)
16.       .objectFit(ImageFit.Fill)
17.       .autoResize(true)
18.   }.width($$.width).height($$.height)
19. }

20. @Entry
21. @Component
22. struct SelectionMenuLongPress {
23.   controller: webview.WebviewController = new webview.WebviewController();
24.   previewController: webview.WebviewController = new webview.WebviewController();
25.   @Builder PreviewBuilder($$: PreviewBuilderParam){
26.     Column() {
27.       Stack(){
28.         Text("") // 可选择是否展示url
29.           .padding(5)
30.           .width('100%')
31.           .textAlign(TextAlign.Start)
32.           .backgroundColor(Color.White)
33.           .copyOption(CopyOptions.LocalDevice)
34.           .maxLines(1)
35.           .textOverflow({overflow:TextOverflow.Ellipsis})
36.         Progress({ value: this.progressValue, total: 100, type: ProgressType.Linear }) // 展示进度条
37.           .style({ strokeWidth: 3, enableSmoothEffect: true })
38.           .backgroundColor(Color.White)
39.           .opacity(this.progressVisible?1:0)
40.           .backgroundColor(Color.White)
41.       }.alignContent(Alignment.Bottom)
42.       Web({src:$$.url,controller: new webview.WebviewController()})
43.         .javaScriptAccess(true)
44.         .fileAccess(true)
45.         .onlineImageAccess(true)
46.         .imageAccess(true)
47.         .domStorageAccess(true)
48.         .onPageBegin(()=>{
49.           this.progressValue = 0;
50.           this.progressVisible = true;
51.         })
52.         .onProgressChange((event)=>{
53.           this.progressValue = event.newProgress;
54.         })
55.         .onPageEnd(()=>{
56.           this.progressVisible = false;
57.         })
58.         .hitTestBehavior(HitTestMode.None) // 使预览Web不响应手势
59.     }.width($$.width).height($$.height) // 设置预览宽高
60.   }

61.   private result: WebContextMenuResult | undefined = undefined;
62.   @State previewImage: Resource | string | undefined = undefined;
63.   @State previewWidth: number = 1;
64.   @State previewHeight: number = 1;
65.   @State previewWidthImage: number = 1;
66.   @State previewHeightImage: number = 1;
67.   @State linkURL:string = "";
68.   @State progressValue:number = 0;
69.   @State progressVisible:boolean = true;
70.   uiContext: UIContext = this.getUIContext();

71.   @Builder
72.   LinkMenuBuilder() {
73.     Menu() {
74.       MenuItem({ content: '复制链接', })
75.         .onClick(() => {
76.           const pasteboardData = pasteboard.createData(pasteboard.MIMETYPE_TEXT_PLAIN, this.linkURL);
77.           const systemPasteboard = pasteboard.getSystemPasteboard();
78.           systemPasteboard.setData(pasteboardData);
79.         })
80.       MenuItem({content:'打开链接'})
81.         .onClick(()=>{
82.           this.controller.loadUrl(this.linkURL);
83.         })
84.     }
85.   }
86.   @Builder
87.   ImageMenuBuilder() {
88.     Menu() {
89.       MenuItem({ content: '复制图片', })
90.         .onClick(() => {
91.           this.result?.copyImage();
92.           this.result?.closeContextMenu();
93.         })
94.     }
95.   }
96.   build() {
97.     Column() {
98.       Web({ src: $rawfile("index.html"), controller: this.controller })
99.         .javaScriptAccess(true)
100.         .fileAccess(true)
101.         .onlineImageAccess(true)
102.         .imageAccess(true)
103.         .domStorageAccess(true)
104.         .bindSelectionMenu(WebElementType.LINK, this.LinkMenuBuilder, WebResponseType.LONG_PRESS,
105.           {
106.             onAppear: () => {},
107.             onDisappear: () => {
108.               this.result?.closeContextMenu();
109.             },
110.             preview: this.PreviewBuilder({
111.               width: 500,
112.               height: 400,
113.               url:this.linkURL
114.             }),
115.             menuType: MenuType.PREVIEW_MENU,
116.           })
117.         .bindSelectionMenu(WebElementType.IMAGE, this.ImageMenuBuilder, WebResponseType.LONG_PRESS,
118.           {
119.             onAppear: () => {},
120.             onDisappear: () => {
121.               this.result?.closeContextMenu();
122.             },
123.             preview: PreviewBuilderGlobalForImage({
124.               previewImage: this.previewImage,
125.               width: this.previewWidthImage,
126.               height: this.previewHeightImage,
127.             }),
128.             menuType: MenuType.PREVIEW_MENU,
129.           })
130.         .zoomAccess(true)
131.         .onContextMenuShow((event) => {
132.           if (event) {
133.             this.result = event.result;
134.             this.previewWidthImage = this.uiContext!.px2vp(event.param.getPreviewWidth());
135.             this.previewHeightImage = this.uiContext!.px2vp(event.param.getPreviewHeight());
136.             if (event.param.getSourceUrl().indexOf("resource://rawfile/") == 0) {
137.               this.previewImage = $rawfile(event.param.getSourceUrl().substring(19));
138.             } else {
139.               this.previewImage = event.param.getSourceUrl();
140.             }
141.             this.linkURL = event.param.getLinkUrl()
142.             return true;
143.           }
144.           return false;
145.         })
146.     }

147.   }
148.   // 侧滑返回
149.   onBackPress(): boolean | void {
150.     if (this.controller.accessStep(-1)) {
151.       this.controller.backward();
152.       return true;
153.     } else {
154.       return false;
155.     }
156.   }
157. }

html示例

1. <html lang="zh-CN"><head>
2.     <meta charset="UTF-8">
3.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
4.     <title>综合信息页面</title>
5. </head>
6. <body>
7. <div>
8.     <h1>综合信息与联系详情</h1>
9.     <section>
10.         <a href="https://www.example.com">EXAMPLE</a>
11.         <br>
12.         <a href="https://www.example1.com/">EXAMPLE1</a>
13.     </section>
14. </div>
15. <footer>
16.     <p>请注意，以上提供的所有网址仅供演示之用。</p>
17. </footer>
18. </body>
19. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.33633664762060583012395909481144:50001231000000:2800:97E9A8B860230A665F2CCF3AC4A76042856DEE862F832DC6609FA7C77DD7037A.gif)

## Web菜单保存图片

1. 创建MenuBuilder组件作为菜单弹窗，使用[SaveButton](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-security-components-savebutton)组件实现图片保存，通过bindContextMenu将MenuBuilder与Web绑定。
2. 在onContextMenuShow中获取图片url，通过copyLocalPicToDir或copyUrlPicToDir将图片保存至应用沙箱。
3. 通过photoAccessHelper将应用沙箱中的图片保存至图库。

4. import { webview } from '@kit.ArkWeb';
5. import { common } from '@kit.AbilityKit';
6. import { fileIo as fs } from '@kit.CoreFileKit';
7. import { systemDateTime } from '@kit.BasicServicesKit';
8. import { http } from '@kit.NetworkKit';
9. import { photoAccessHelper } from '@kit.MediaLibraryKit';

10. @Entry
11. @Component
12. struct WebComponent {
13.   saveButtonOptions: SaveButtonOptions = {
14.     icon: SaveIconStyle.FULL_FILLED,
15.     text: SaveDescription.SAVE_IMAGE,
16.     buttonType: ButtonType.Capsule
17.   }
18.   controller: webview.WebviewController = new webview.WebviewController();
19.   @State showMenu: boolean = false;
20.   @State imgUrl: string = '';
21.   context = this.getUIContext().getHostContext() as common.UIAbilityContext;

22.   copyLocalPicToDir(rawfilePath: string, newFileName: string): string {
23.     let srcFileDes = this.context.resourceManager.getRawFdSync(rawfilePath);
24.     let dstPath = this.context.filesDir + "/" + newFileName;
25.     let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
26.     let bufsize = 4096;
27.     let buf = new ArrayBuffer(bufsize);
28.     let off = 0, len = 0, readedLen = 0;
29.     while (len = fs.readSync(srcFileDes.fd, buf, { offset: srcFileDes.offset + off, length: bufsize })) {
30.       readedLen += len;
31.       fs.writeSync(dest.fd, buf, { offset: off, length: len });
32.       off = off + len;
33.       if ((srcFileDes.length - readedLen) < bufsize) {
34.         bufsize = srcFileDes.length - readedLen;
35.       }
36.     }
37.     fs.close(dest.fd);
38.     return dest.path;
39.   }

40.   async copyUrlPicToDir(picUrl: string, newFileName: string): Promise<string> {
41.     let uri = '';
42.     let httpRequest = http.createHttp();
43.     let data: http.HttpResponse = await (httpRequest.request(picUrl) as Promise<http.HttpResponse>);
44.     if (data?.responseCode == http.ResponseCode.OK) {
45.       let dstPath = this.context.filesDir + "/" + newFileName;
46.       let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
47.       let writeLen: number = fs.writeSync(dest.fd, data.result as ArrayBuffer);
48.       uri = dest.path;
49.     }
50.     return uri;
51.   }

52.   @Builder
53.   MenuBuilder() {
54.     Column() {
55.       Row() {
56.         SaveButton(this.saveButtonOptions)
57.           .onClick(async (event, result: SaveButtonOnClickResult) => {
58.             if (result == SaveButtonOnClickResult.SUCCESS) {
59.               try {
60.                 let context = this.context;
61.                 let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);
62.                 let uri = '';
63.                 if (this.imgUrl?.includes('rawfile')) {
64.                   let rawFileName: string = this.imgUrl.substring(this.imgUrl.lastIndexOf('/') + 1);
65.                   uri = this.copyLocalPicToDir(rawFileName, 'copyFile.png');
66.                 } else if (this.imgUrl?.includes('http') || this.imgUrl?.includes('https')) {
67.                   uri = await this.copyUrlPicToDir(this.imgUrl, `onlinePic${systemDateTime.getTime()}.png`);
68.                 }
69.                 let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest =
70.                   photoAccessHelper.MediaAssetChangeRequest.createImageAssetRequest(context, uri);
71.                 await phAccessHelper.applyChanges(assetChangeRequest);
72.               } catch (err) {
73.                 console.error(`create asset failed with error: ${err.code}, ${err.message}`);
74.               }
75.             } else {
76.               console.error(`SaveButtonOnClickResult create asset failed`);
77.             }
78.             this.showMenu = false;
79.           })
80.       }
81.       .margin({ top: 20, bottom: 20 })
82.       .justifyContent(FlexAlign.Center)
83.     }
84.     .width('80')
85.     .backgroundColor(Color.White)
86.     .borderRadius(10)
87.   }

88.   build() {
89.     Column() {
90.       Web({ src: $rawfile("index.html"), controller: this.controller })
91.         .onContextMenuShow((event) => {
92.           if (event) {
93.             let hitValue = this.controller.getLastHitTest();
94.             this.imgUrl = hitValue.extra;
95.           }
96.           this.showMenu = true;
97.           return true;
98.         })
99.         .bindContextMenu(this.MenuBuilder, ResponseType.LongPress)
100.         .fileAccess(true)
101.         .javaScriptAccess(true)
102.         .domStorageAccess(true)
103.     }
104.   }
105. }

106. <!--index.html-->
107. <!DOCTYPE html>
108. <html>
109. <head>
110.     <title>SavePicture</title>
111. </head>
112. <body>
113. <h1>SavePicture</h1>
114. <br>
115. <br>
116. <br>
117. <br>
118. <br>
119. <!--startIcon.png为html同目录下图片-->
120. <img src="./startIcon.png">
121. </body>
122. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.97123562329824553018833148527255:50001231000000:2800:A32D115F0EF0E90D398B8AFB85EB09F317F303FBFAA0E7B554847ACBB1F69663.gif)

## Web菜单获取选中文本

Web组件的[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)接口中没有提供获取选中文本的方式。开发者可通过[javaScriptProxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#javascriptproxy)获取到JavaScript的选中文本，实现自定义菜单的逻辑。

1. 创建SelectClass类，通过[javaScriptProxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#javascriptproxy)将SelectClass对象注册到Web组件中。
2. 在Html侧注册选区变更监听器，在选区变更时通过SelectClass对象将选区设置到ArkTS侧。

3. import { webview } from '@kit.ArkWeb';
4. let selectText = '';

5. class SelectClass {
6.   constructor() {
7.   }

8.   setSelectText(param: String) {
9.     selectText = param.toString();
10.   }
11. }

12. @Entry
13. @Component
14. struct WebComponent {
15.   webController: webview.WebviewController = new webview.WebviewController();
16.   @State selectObj: SelectClass = new SelectClass();
17.   @State textStr: string = '';

18.   build() {
19.     Column() {
20.       Web({ src: $rawfile('index.html'), controller: this.webController})
21.         .javaScriptProxy({
22.           object: this.selectObj,
23.           name: 'selectObjName',
24.           methodList: ['setSelectText'],
25.           controller: this.webController
26.         })
27.         .height('40%')
28.       Text('Click here to get the selected text.')
29.         .fontSize(20)
30.         .onClick(() => {
31.           this.textStr = selectText;
32.         })
33.         .height('10%')
34.       Text('Selected text is ' + this.textStr)
35.         .fontSize(20)
36.         .height('10%')
37.     }
38.   }
39. }

40. <!DOCTYPE html>
41. <html>
42. <head>
43.     <title>Test Get Select</title>
44.     <style>
45.         body {
46.           margin: 40px;
47.           background-color: #f4f4f4;
48.         }
49.         .edit-container {
50.           padding: 20px;
51.           background-color: #fff;
52.           border-radius: 8px;
53.           box-shadow: 0 0 10px rgba(0,0,0,0.1);
54.           margin: auto;
55.         }
56.         textarea {
57.           width: 100%;
58.           height: 400px;
59.           font-size: 16px;
60.           padding: 10px;
61.           border: 1px solid #ccc;
62.           border-radius: 4px;
63.         }
64.     </style>
65. </head>
66. <body>
67. <div class="edit-container">
68.     <textarea placeholder="Enter the text here and select it by long pressing."></textarea>
69. </div>
70. <script>
71.     document.addEventListener('selectionchange', () => {
72.       var selection = window.getSelection();
73.       if(selection.rangeCount > 0) {
74.         var selectedText = selection.toString();
75.         selectObjName.setSelectText(selectedText);
76.       }
77.     })
78. </script>
79. </body>
80. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.94129462790581123369363129678496:50001231000000:2800:93E1A114511A7F2292811E9A6BCB58148AE5F5D439EBC45E71F51FF9AE7A5B22.gif)

## Web菜单识别图片二维码

在二维码跳转页面或者付款场景中，开发者可通过实现上下文菜单，获取到[onContextMenuShow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#oncontextmenushow9)接口中的二维码图片信息进行处理，提供给用户扫描二维码入口。

1. 创建MenuBuilder组件作为菜单弹窗，通过bindContextMenu将MenuBuilder与Web绑定。
2. 在onContextMenuShow中获取图片url，通过copyLocalPicToDir或copyUrlPicToDir将图片保存至应用沙箱。
3. 通过detectBarcode.decode解析保存在沙箱中的图片，获取到结果。

4. import { webview } from '@kit.ArkWeb';
5. import { common } from '@kit.AbilityKit';
6. import { fileIo as fs } from '@kit.CoreFileKit';
7. import { systemDateTime } from '@kit.BasicServicesKit';
8. import { http } from '@kit.NetworkKit';
9. import { scanCore, scanBarcode, detectBarcode } from '@kit.ScanKit';
10. import { BusinessError } from '@kit.BasicServicesKit';

11. @Entry
12. @Component
13. struct WebComponent {
14.   saveButtonOptions: SaveButtonOptions = {
15.     icon: SaveIconStyle.FULL_FILLED,
16.     text: SaveDescription.SAVE_IMAGE,
17.     buttonType: ButtonType.Capsule
18.   }
19.   controller: webview.WebviewController = new webview.WebviewController();
20.   private result: WebContextMenuResult | undefined = undefined;
21.   @State showMenu: boolean = false;
22.   @State imgUrl: string = '';
23.   @State decodeResult: string = '';
24.   context = this.getUIContext().getHostContext() as common.UIAbilityContext;

25.   copyLocalPicToDir(rawfilePath: string, newFileName: string): string {
26.     let srcFileDes = this.context.resourceManager.getRawFdSync(rawfilePath);
27.     let dstPath = this.context.filesDir + "/" + newFileName;
28.     let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
29.     let bufsize = 4096;
30.     let buf = new ArrayBuffer(bufsize);
31.     let off = 0, len = 0, readedLen = 0;
32.     while (len = fs.readSync(srcFileDes.fd, buf, { offset: srcFileDes.offset + off, length: bufsize })) {
33.       readedLen += len;
34.       fs.writeSync(dest.fd, buf, { offset: off, length: len });
35.       off = off + len;
36.       if ((srcFileDes.length - readedLen) < bufsize) {
37.         bufsize = srcFileDes.length - readedLen;
38.       }
39.     }
40.     fs.close(dest.fd);
41.     return dest.path;
42.   }

43.   async copyUrlPicToDir(picUrl: string, newFileName: string): Promise<string> {
44.     let uri = '';
45.     let httpRequest = http.createHttp();
46.     let data: http.HttpResponse = await (httpRequest.request(picUrl) as Promise<http.HttpResponse>);
47.     if (data?.responseCode == http.ResponseCode.OK) {
48.       let dstPath = this.context.filesDir + "/" + newFileName;
49.       let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
50.       let writeLen: number = fs.writeSync(dest.fd, data.result as ArrayBuffer);
51.       uri = dest.path;
52.     }
53.     return uri;
54.   }

55.   @Builder
56.   MenuBuilder() {
57.     Menu() {
58.       MenuItem({
59.         content: "Scan QR Code",
60.       })
61.         .width(200)
62.         .height(50)
63.         .onClick(async () => {
64.           try {
65.             let uri = '';
66.             if (this.imgUrl?.includes('rawfile')) {
67.               let rawFileName: string = this.imgUrl.substring(this.imgUrl.lastIndexOf('/') + 1);
68.               uri = this.copyLocalPicToDir(rawFileName, 'copyFile.png');
69.             } else if (this.imgUrl?.includes('http') || this.imgUrl?.includes('https')) {
70.               uri = await this.copyUrlPicToDir(this.imgUrl, `onlinePic${systemDateTime.getTime()}.png`);
71.             }
72.             let options: scanBarcode.ScanOptions =
73.               { scanTypes: [scanCore.ScanType.ALL], enableMultiMode: true, enableAlbum: true }
74.             let inputImage: detectBarcode.InputImage = { uri: uri };
75.             try {
76.               // 调用图片识码接口
77.               detectBarcode.decode(inputImage, options,
78.                 (error: BusinessError, result: Array<scanBarcode.ScanResult>) => {
79.                   if (error && error.code) {
80.                     console.error(`create asset failed with error: ${error.code}, ${error.message}`);
81.                     return;
82.                   }
83.                   this.decodeResult = JSON.stringify(result);
84.                 });
85.             } catch (err) {
86.               console.error(`Failed to detect Barcode. Code: ${err.code}, ${err.message}`);
87.             }
88.           } catch (err) {
89.             console.error(`create asset failed with error: ${err.code}, ${err.message}`);
90.           }
91.         })
92.     }
93.   }

94.   build() {
95.     Column() {
96.       Web({ src: $rawfile("index.html"), controller: this.controller })
97.         .onContextMenuShow((event) => {
98.           if (event) {
99.             let hitValue = this.controller.getLastHitTest();
100.             this.imgUrl = hitValue.extra;
101.           }
102.           this.showMenu = true;
103.           return true;
104.         })
105.         .bindContextMenu(this.MenuBuilder, ResponseType.LongPress)
106.         .fileAccess(true)
107.         .javaScriptAccess(true)
108.         .domStorageAccess(true)
109.         .height('40%')
110.       Text('Decode result is ' + this.decodeResult)
111.         .fontSize(20)
112.         .height('10%')
113.     }
114.   }
115. }

116. <!--index.html-->
117. <!DOCTYPE html>
118. <html>
119. <head>
120.     <title>test QR code</title>
121. </head>
122. <body>
123. <h1>Long press and click to scan the QR code</h1>
124. <!--img.png为二维码图片-->
125. <img src="img.png" >
126. </body>
127. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.06270991606947428599641497908057:50001231000000:2800:97D8807984201C3212A665587CF9F7A5A11AF6B44C1A4C37BB47527FBF41FB8B.gif)

## 常见问题

### 如何禁用长按选择时弹出菜单

可通过[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)接口将系统默认菜单全部过滤，此时无菜单项，则不会显示菜单。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct WebComponent {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   onCreateMenu(menuItems: Array<TextMenuItem>): Array<TextMenuItem> {
8.     let items = menuItems.filter((menuItem) => {
9.       // 过滤用户需要的系统按键
10.       return false;
11.     });
12.     return items;
13.   }

14.   onMenuItemClick(menuItem: TextMenuItem, textRange: TextRange): boolean {
15.     return false; // 返回默认值false
16.   }

17.   @State EditMenuOptions: EditMenuOptions = { onCreateMenu: this.onCreateMenu, onMenuItemClick: this.onMenuItemClick }

18.   build() {
19.     Column() {
20.       Web({ src: $rawfile("index.html"), controller: this.controller })
21.         .editMenuOptions(this.EditMenuOptions)
22.     }
23.   }
24. }

25. <!--index.html-->
26. <!DOCTYPE html>
27. <html>
28.   <head>
29.       <title>测试网页</title>
30.   </head>
31.   <body>
32.     <h1>editMenuOptions Demo</h1>
33.     <span>edit menu options</span>
34.   </body>
35. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.19330739680792383411363668468450:50001231000000:2800:2DA5BE11178E1B6384FC9FFE78DAC381DB88BD8FC74656B3CC0418D7C01C52FB.gif)

### 出现选区时手柄菜单不显示

可排查是否通过JS的[selection-api](https://www.w3.org/TR/selection-api/)对选区进行了操作，目前通过这种方式改变选区会导致手柄菜单不显示。

### 如何修改文本选中菜单的样式

从API version 21开始，应用可通过[bindSelectionMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#bindselectionmenu13)接口，实现自定义文本菜单。

**示例代码**

1. import { webview } from '@kit.ArkWeb';
2. import { BusinessError } from '@kit.BasicServicesKit';

3. @Entry
4. @Component
5. struct WebComponent {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   clearSelection() {
8.     try {
9.       this.controller.runJavaScript(
10.         'clearSelection()',
11.         (error, result) => {
12.           if (error) {
13.             console.error(`run clearSelection JavaScript error, ErrorCode: ${(error as BusinessError).code},  Message: $  {(error as BusinessError).message}`);
14.             return;
15.           }
16.           if (result) {
17.             console.info(`The clearSelection() return value is: ${result}`);
18.           }
19.         });
20.     } catch (error) {
21.       console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
22.     }
23.   }

24.   @Builder
25.   TextMenuBuilder() {
26.     Menu() {
27.       MenuItem({ content: 'Copy', })
28.         .onClick(() => {
29.           try {
30.             this.controller.runJavaScript(
31.               'copySelectedText()',
32.               (error, result) => {
33.                 if (error) {
34.                   console.error(`run copySelectedText JavaScript error, ErrorCode: ${(error as BusinessError).code},    Message: ${(error as BusinessError).message}`);
35.                   return;
36.                 }
37.                 if (result) {
38.                   console.info(`The copySelectedText() return value is: ${result}`);
39.                 }
40.               });
41.           } catch (error) {
42.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
43.           }
44.           this.clearSelection()
45.         }).backgroundColor(Color.Pink)
46.     }
47.   }
48.   build() {
49.     Column() {
50.       Web({ src: $rawfile('bindSelectionMenuText.html'), controller: this.controller })
51.         .javaScriptAccess(true)
52.         .fileAccess(true)
53.         .onlineImageAccess(true)
54.         .imageAccess(true)
55.         .domStorageAccess(true)
56.         .zoomAccess(true)
57.         .bindSelectionMenu(WebElementType.TEXT, this.TextMenuBuilder, WebResponseType.LONG_PRESS,
58.           {
59.             onAppear: () => {},
60.             onDisappear: () => {},
61.             menuType: MenuType.SELECTION_MENU,
62.           })
63.     }
64.   }
65.   onBackPress(): boolean | void {
66.     if (this.controller.accessStep(-1)) {
67.       this.controller.backward();
68.       return true;
69.     } else {
70.       return false;
71.     }
72.   }
73. }

74. <!--bindSelectionMenuText.html-->
75. <!DOCTYPE html>
76. <html lang="zh-CN">
77. <head>
78.     <meta charset="UTF-8">
79.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
80.     <title>自定义文本菜单</title>
81.     <style>
82.         .container {
83.             background-color: white;
84.             padding: 30px;
85.             margin: 20px 0;
86.         }

87.         .context {
88.             line-height: 1.8;
89.             font-size: 18px;
90.         }

91.         .context span {
92.             border-radius: 8px;
93.             background-color: #f8f9fa;
94.         }
95.     </style>
96. </head>
97. <body>
98. <div class="container">
99.     <div class="context">
100.         <span>在这个数字时代，文本复制功能变得日益重要。无论是引用名言、保存重要信息，还是分享有趣的内容，复制文本都是我们日常操作的  一部分。</span>
101.     </div>
102. </div>

103. <script>
104.   function copySelectedText() {
105.       const selectedText = window.getSelection().toString();
106.       if (selectedText.length > 0) {
107.           // 使用Clipboard API复制文本
108.           navigator.clipboard.writeText(selectedText)
109.               .then(() => {
110.                   showNotification();
111.               })
112.               .catch(err => {
113.                   console.error('copy failed:', err);
114.               });
115.       }
116.   }
117.   function clearSelection() {
118.     if (window.getSelection) {
119.       window.getSelection().removeAllRanges();
120.     }
121.   }
122. </script>
123. </body>
124. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.70221801701384901506701052920143:50001231000000:2800:704F509ECFEBC24550C0F3C204FCA88122F73B934B99E2B26EA35EEAD25F3F21.gif)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-safe-area-insets "网页中安全区域计算和避让适配")
# 使用Web组件菜单处理网页内容

更新时间: 2025-12-16 16:38

菜单作为用户交互的关键组件，其作用是构建清晰的导航体系，通过结构化布局展示功能入口，使用户能够迅速找到目标内容或执行操作。作为人机交互的重要枢纽，它显著提升了Web组件的可访问性和用户体验，是应用设计中必不可少的部分。Web组件菜单类型包括[文本选中菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E6%96%87%E6%9C%AC%E9%80%89%E4%B8%AD%E8%8F%9C%E5%8D%95)、[上下文菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E4%B8%8A%E4%B8%8B%E6%96%87%E8%8F%9C%E5%8D%95)和[自定义菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%8F%9C%E5%8D%95)，应用可根据具体需求灵活选择。

|菜单类型|目标元素|响应类型|是否支持自定义|
|:--|:--|:--|:--|
|[文本选中菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E6%96%87%E6%9C%AC%E9%80%89%E4%B8%AD%E8%8F%9C%E5%8D%95)|文本|手势长按|可增减菜单项，菜单样式不可自定义|
|[上下文菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E4%B8%8A%E4%B8%8B%E6%96%87%E8%8F%9C%E5%8D%95)|超链接、图片、文字|手势长按、鼠标右键|支持通过菜单组件自定义|
|[自定义菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%8F%9C%E5%8D%95)|图片|手势长按|支持通过菜单组件自定义|

## 文本选中菜单

Web组件的文本选中菜单是一种通过自定义元素实现的上下文交互组件，当用户选中文本时会动态显示，提供复制、分享、标注等语义化操作，具备标准化功能与可扩展性，是移动端文本操作的核心功能。文本选中菜单在用户长按选中文本或编辑状态下长按出现单手柄时弹出，菜单项横向排列。系统提供默认的菜单实现。应用可通过[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)接口对文本选中菜单进行自定义操作。

1. 通过onCreateMenu方法自定义菜单项，通过操作Array<[TextMenuItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-text-common#textmenuitem12%E5%AF%B9%E8%B1%A1%E8%AF%B4%E6%98%8E)>数组可对显示菜单项进行增减操作，在[TextMenuItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-text-common#textmenuitem12%E5%AF%B9%E8%B1%A1%E8%AF%B4%E6%98%8E)中定义菜单项名称、图标、ID等内容。
2. 通过onMenuItemClick方法处理菜单项点击事件，当返回false时会执行系统默认逻辑。
3. 创建一个[EditMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-text-common#editmenuoptions)对象，包含onCreateMenu和onMenuItemClick两个方法，通过Web组件的[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)方法与Web组件绑定。

4. // xxx.ets
5. import { webview } from '@kit.ArkWeb';

6. @Entry
7. @Component
8. struct WebComponent {
9.   controller: webview.WebviewController = new webview.WebviewController();

10.   onCreateMenu(menuItems: Array<TextMenuItem>): Array<TextMenuItem> {
11.     let items = menuItems.filter((menuItem) => {
12.       // 过滤用户需要的系统按键
13.       return (
14.         menuItem.id.equals(TextMenuItemId.CUT) ||
15.         menuItem.id.equals(TextMenuItemId.COPY) ||
16.         menuItem.id.equals(TextMenuItemId.PASTE)
17.       );
18.     });
19.     let customItem1: TextMenuItem = {
20.       content: 'customItem1',
21.       id: TextMenuItemId.of('customItem1'),
22.       icon: $r('app.media.startIcon')
23.     };
24.     let customItem2: TextMenuItem = {
25.       content: $r('app.string.EntryAbility_label'),
26.       id: TextMenuItemId.of('customItem2'),
27.       icon: $r('app.media.startIcon')
28.     };
29.     items.push(customItem1); // 在选项列表后添加新选项
30.     items.unshift(customItem2); // 在选项列表前添加选项
31.     items.push(customItem1);
32.     items.push(customItem1);
33.     items.push(customItem1);
34.     items.push(customItem1);
35.     items.push(customItem1);
36.     return items;
37.   }

38.   onMenuItemClick(menuItem: TextMenuItem, textRange: TextRange): boolean {
39.     if (menuItem.id.equals(TextMenuItemId.CUT)) {
40.       // 用户自定义行为
41.       console.info("拦截 id：CUT")
42.       return true; // 返回true不执行系统回调
43.     } else if (menuItem.id.equals(TextMenuItemId.COPY)) {
44.       // 用户自定义行为
45.       console.info("不拦截 id：COPY")
46.       return false; // 返回false执行系统回调
47.     } else if (menuItem.id.equals(TextMenuItemId.of('customItem1'))) {
48.       // 用户自定义行为
49.       console.info("拦截 id：customItem1")
50.       return true; // 用户自定义菜单选项返回true时点击后不关闭菜单，返回false时关闭菜单
51.     } else if (menuItem.id.equals(TextMenuItemId.of('customItem2'))) {
52.       // 用户自定义行为
53.       console.info("拦截 id：customItem2")
54.       return true;
55.     }
56.     return false; // 返回默认值false
57.   }

58.   @State EditMenuOptions: EditMenuOptions = { onCreateMenu: this.onCreateMenu, onMenuItemClick: this.onMenuItemClick }

59.   build() {
60.     Column() {
61.       Web({ src: $rawfile("index.html"), controller: this.controller })
62.         .editMenuOptions(this.EditMenuOptions)
63.     }
64.   }
65. }

66. <!--index.html-->
67. <!DOCTYPE html>
68. <html>
69.   <head>
70.       <title>测试网页</title>
71.   </head>
72.   <body>
73.     <h1>editMenuOptions Demo</h1>
74.     <span>edit menu options</span>
75.   </body>
76. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.74683493357399651917983596502008:50001231000000:2800:5C244201AEDBD0BBE0E393950817D83405FFC2A941DB3153458274C6BA40BF7D.gif)

## 上下文菜单

上下文菜单是用户通过特定操作（如右键点击或长按富文本）触发的快捷菜单，用于提供与当前操作对象或界面元素相关的功能选项。菜单项纵向排列。系统未提供默认实现，若应用未实现，则不显示上下文菜单。应用需要创建一个[Menu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-menu)组件并与Web绑定，在菜单弹出时可通过Web组件的[onContextMenuShow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#oncontextmenushow9)回调接口获取上下文菜单的详细信息，包括点击位置的HTML元素信息及点击位置信息。

1. [Menu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-menu)组件作为弹出的菜单，包含所有菜单项行为与样式。
2. 使用bindPopup方法将Menu组件与Web组件绑定。当上下文菜单弹出时，将显示创建的Menu组件。
3. 在onContextMenuShow回调中获取上下文菜单事件信息[onContextMenuShowEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-i#oncontextmenushowevent12)。其中param为[WebContextMenuParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-webcontextmenuparam)类型，包含点击位置对应HTML元素信息和位置信息，result为[WebContextMenuResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-webcontextmenuresult)类型，提供常见的菜单能力。

4. // xxx.ets
5. import { webview } from '@kit.ArkWeb';
6. import { pasteboard } from '@kit.BasicServicesKit';

7. const TAG = 'ContextMenu';

8. @Entry
9. @Component
10. struct WebComponent {
11.   controller: webview.WebviewController = new webview.WebviewController();
12.   private result: WebContextMenuResult | undefined = undefined;
13.   @State linkUrl: string = '';
14.   @State offsetX: number = 0;
15.   @State offsetY: number = 0;
16.   @State showMenu: boolean = false;
17.   uiContext: UIContext = this.getUIContext();

18.   @Builder
19.   // 构建自定义菜单及触发功能接口
20.   MenuBuilder() {
21.     // 以垂直列表形式显示的菜单。
22.     Menu() {
23.       // 展示菜单Menu中具体的item菜单项。
24.       MenuItem({
25.         content: '复制图片',
26.       })
27.         .width(100)
28.         .height(50)
29.         .onClick(() => {
30.           this.result?.copyImage();
31.           this.showMenu = false;
32.         })
33.       MenuItem({
34.         content: '剪切',
35.       })
36.         .width(100)
37.         .height(50)
38.         .onClick(() => {
39.           this.result?.cut();
40.           this.showMenu = false;
41.         })
42.       MenuItem({
43.         content: '复制',
44.       })
45.         .width(100)
46.         .height(50)
47.         .onClick(() => {
48.           this.result?.copy();
49.           this.showMenu = false;
50.         })
51.       MenuItem({
52.         content: '粘贴',
53.       })
54.         .width(100)
55.         .height(50)
56.         .onClick(() => {
57.           this.result?.paste();
58.           this.showMenu = false;
59.         })
60.       MenuItem({
61.         content: '复制链接',
62.       })
63.         .width(100)
64.         .height(50)
65.         .onClick(() => {
66.           let pasteData = pasteboard.createData('text/plain', this.linkUrl);
67.           pasteboard.getSystemPasteboard().setData(pasteData, (error) => {
68.             if (error) {
69.               return;
70.             }
71.           })
72.           this.showMenu = false;
73.         })
74.       MenuItem({
75.         content: '全选',
76.       })
77.         .width(100)
78.         .height(50)
79.         .onClick(() => {
80.           this.result?.selectAll();
81.           this.showMenu = false;
82.         })
83.     }
84.     .width(150)
85.     .height(300)
86.   }

87.   build() {
88.     Column() {
89.       Web({ src: $rawfile("index.html"), controller: this.controller })
90.         // 触发自定义弹窗
91.         .onContextMenuShow((event) => {
92.           if (event) {
93.             this.result = event.result
94.             console.info("x coord = " + event.param.x());
95.             console.info("link url = " + event.param.getLinkUrl());
96.             this.linkUrl = event.param.getLinkUrl();
97.           }
98.           console.info(TAG, `x: ${this.offsetX}, y: ${this.offsetY}`);
99.           this.showMenu = true;
100.           this.offsetX = 0;
101.           this.offsetY = Math.max(this.uiContext!.px2vp(event?.param.y() ?? 0) - 0, 0);
102.           return true;
103.         })
104.         .bindPopup(this.showMenu,
105.           {
106.             builder: this.MenuBuilder(),
107.             enableArrow: false,
108.             placement: Placement.LeftTop,
109.             offset: { x: this.offsetX, y: this.offsetY },
110.             mask: false,
111.             onStateChange: (e) => {
112.               if (!e.isVisible) {
113.                 this.showMenu = false;
114.                 this.result!.closeContextMenu();
115.               }
116.             }
117.           })
118.     }
119.   }
120. }

121. <!-- index.html -->
122. <!DOCTYPE html>
123. <html lang="en">
124. <body>
125.   <h1>onContextMenuShow</h1>
126.   <a href="http://www.example.com" style="font-size:27px">超链接www.example.com</a>
127.   <!--example.png为html同目录下图片-->
128.   <div><img src="example.png"></div>
129.   <p>选中文字鼠标右键弹出菜单</p>
130. </body>
131. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.29451072078178417578416765697859:50001231000000:2800:3A77588D209390352CED6A77358F1BB92F86D7587F33E8FE5723170BA62D6076.gif)

## 自定义菜单

自定义菜单赋予开发者灵活控制菜单触发时机与视觉呈现的能力，使应用能够根据用户操作场景动态匹配功能入口，显著简化开发过程中的界面适配工作，同时让交互体验更贴近用户直觉。

开发者可通过[bindSelectionMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#bindselectionmenu13)接口实现自定义菜单功能。目前，已额外支持通过长按图片、链接和文本，触发自定义菜单及自定义文本菜单。

1. 创建[Menu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-menu)组件作为菜单弹窗。
2. 通过Web组件的[bindSelectionMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#bindselectionmenu13)方法绑定MenuBuilder菜单弹窗。将[WebElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webelementtype13)设置为WebElementType.IMAGE，[responseType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webresponsetype13)设置为WebResponseType.LONG_PRESS，表示长按图片时弹出菜单。在[options](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-i#selectionmenuoptionsext13)中定义菜单显示回调onAppear、菜单消失回调onDisappear、预览窗口preview和菜单类型menuType。

3. // xxx.ets
4. import { webview } from '@kit.ArkWeb';

5. interface PreviewBuilderParam {
6.   previewImage: Resource | string | undefined;
7.   width: number;
8.   height: number;
9. }

10. @Builder function PreviewBuilderGlobal($$: PreviewBuilderParam) {
11.   Column() {
12.     Image($$.previewImage)
13.       .objectFit(ImageFit.Fill)
14.       .autoResize(true)
15.   }.width($$.width).height($$.height)
16. }

17. @Entry
18. @Component
19. struct WebComponent {
20.   controller: webview.WebviewController = new webview.WebviewController();

21.   private result: WebContextMenuResult | undefined = undefined;
22.   @State previewImage: Resource | string | undefined = undefined;
23.   @State previewWidth: number = 0;
24.   @State previewHeight: number = 0;
25.   uiContext: UIContext = this.getUIContext();

26.   @Builder
27.   MenuBuilder() {
28.     Menu() {
29.       MenuItem({ content: '复制', })
30.         .onClick(() => {
31.           this.result?.copy();
32.           this.result?.closeContextMenu();
33.         })
34.       MenuItem({ content: '全选', })
35.         .onClick(() => {
36.           this.result?.selectAll();
37.           this.result?.closeContextMenu();
38.         })
39.     }
40.   }
41.   build() {
42.     Column() {
43.       Web({ src: $rawfile("index.html"), controller: this.controller })
44.         .bindSelectionMenu(WebElementType.IMAGE, this.MenuBuilder, WebResponseType.LONG_PRESS,
45.           {
46.             onAppear: () => {},
47.             onDisappear: () => {
48.               this.result?.closeContextMenu();
49.             },
50.             preview: PreviewBuilderGlobal({
51.               previewImage: this.previewImage,
52.               width: this.previewWidth,
53.               height: this.previewHeight
54.             }),
55.             menuType: MenuType.PREVIEW_MENU
56.           })
57.         .onContextMenuShow((event) => {
58.             if (event) {
59.               this.result = event.result;
60.               if (event.param.getLinkUrl()) {
61.                 return false;
62.               }
63.               this.previewWidth = this.uiContext!.px2vp(event.param.getPreviewWidth());
64.               this.previewHeight = this.uiContext!.px2vp(event.param.getPreviewHeight());
65.               if (event.param.getSourceUrl().indexOf("resource://rawfile/") == 0) {
66.                 this.previewImage = $rawfile(event.param.getSourceUrl().substr(19));
67.               } else {
68.                 this.previewImage = event.param.getSourceUrl();
69.               }
70.               return true;
71.             }
72.             return false;
73.           })
74.     }
75.   }
76. }

77. <!--index.html-->
78. <!DOCTYPE html>
79. <html>
80.   <head>
81.       <title>测试网页</title>
82.   </head>
83.   <body>
84.     <h1>bindSelectionMenu Demo</h1>
85.     <!--img.png为html同目录下图片-->
86.     <img src="./img.png" >
87.   </body>
88. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.59434873944830234144482178513845:50001231000000:2800:1B04AF1C73E70FDF30D79EF1FE13DCFD9AA0AC6DC2DC838A7687153EADBA00DB.gif)

自API version 20起，支持绑定长按超链接菜单。可以为图片和链接绑定不同的自定义菜单。

以下示例中，PreviewBuilder定义了超链接对应菜单的弹出内容，用Web组件加载了超链接内容，使用[Progress组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-progress-indicator)展示了加载进度。

1. import { webview } from '@kit.ArkWeb';
2. import { pasteboard } from '@kit.BasicServicesKit';

3. interface PreviewBuilderParam {
4.   width: number;
5.   height: number;
6.   url:Resource | string | undefined;
7. }

8. interface PreviewBuilderParamForImage {
9.   previewImage: Resource | string | undefined;
10.   width: number;
11.   height: number;
12. }

13. @Builder function PreviewBuilderGlobalForImage($$: PreviewBuilderParamForImage) {
14.   Column() {
15.     Image($$.previewImage)
16.       .objectFit(ImageFit.Fill)
17.       .autoResize(true)
18.   }.width($$.width).height($$.height)
19. }

20. @Entry
21. @Component
22. struct SelectionMenuLongPress {
23.   controller: webview.WebviewController = new webview.WebviewController();
24.   previewController: webview.WebviewController = new webview.WebviewController();
25.   @Builder PreviewBuilder($$: PreviewBuilderParam){
26.     Column() {
27.       Stack(){
28.         Text("") // 可选择是否展示url
29.           .padding(5)
30.           .width('100%')
31.           .textAlign(TextAlign.Start)
32.           .backgroundColor(Color.White)
33.           .copyOption(CopyOptions.LocalDevice)
34.           .maxLines(1)
35.           .textOverflow({overflow:TextOverflow.Ellipsis})
36.         Progress({ value: this.progressValue, total: 100, type: ProgressType.Linear }) // 展示进度条
37.           .style({ strokeWidth: 3, enableSmoothEffect: true })
38.           .backgroundColor(Color.White)
39.           .opacity(this.progressVisible?1:0)
40.           .backgroundColor(Color.White)
41.       }.alignContent(Alignment.Bottom)
42.       Web({src:$$.url,controller: new webview.WebviewController()})
43.         .javaScriptAccess(true)
44.         .fileAccess(true)
45.         .onlineImageAccess(true)
46.         .imageAccess(true)
47.         .domStorageAccess(true)
48.         .onPageBegin(()=>{
49.           this.progressValue = 0;
50.           this.progressVisible = true;
51.         })
52.         .onProgressChange((event)=>{
53.           this.progressValue = event.newProgress;
54.         })
55.         .onPageEnd(()=>{
56.           this.progressVisible = false;
57.         })
58.         .hitTestBehavior(HitTestMode.None) // 使预览Web不响应手势
59.     }.width($$.width).height($$.height) // 设置预览宽高
60.   }

61.   private result: WebContextMenuResult | undefined = undefined;
62.   @State previewImage: Resource | string | undefined = undefined;
63.   @State previewWidth: number = 1;
64.   @State previewHeight: number = 1;
65.   @State previewWidthImage: number = 1;
66.   @State previewHeightImage: number = 1;
67.   @State linkURL:string = "";
68.   @State progressValue:number = 0;
69.   @State progressVisible:boolean = true;
70.   uiContext: UIContext = this.getUIContext();

71.   @Builder
72.   LinkMenuBuilder() {
73.     Menu() {
74.       MenuItem({ content: '复制链接', })
75.         .onClick(() => {
76.           const pasteboardData = pasteboard.createData(pasteboard.MIMETYPE_TEXT_PLAIN, this.linkURL);
77.           const systemPasteboard = pasteboard.getSystemPasteboard();
78.           systemPasteboard.setData(pasteboardData);
79.         })
80.       MenuItem({content:'打开链接'})
81.         .onClick(()=>{
82.           this.controller.loadUrl(this.linkURL);
83.         })
84.     }
85.   }
86.   @Builder
87.   ImageMenuBuilder() {
88.     Menu() {
89.       MenuItem({ content: '复制图片', })
90.         .onClick(() => {
91.           this.result?.copyImage();
92.           this.result?.closeContextMenu();
93.         })
94.     }
95.   }
96.   build() {
97.     Column() {
98.       Web({ src: $rawfile("index.html"), controller: this.controller })
99.         .javaScriptAccess(true)
100.         .fileAccess(true)
101.         .onlineImageAccess(true)
102.         .imageAccess(true)
103.         .domStorageAccess(true)
104.         .bindSelectionMenu(WebElementType.LINK, this.LinkMenuBuilder, WebResponseType.LONG_PRESS,
105.           {
106.             onAppear: () => {},
107.             onDisappear: () => {
108.               this.result?.closeContextMenu();
109.             },
110.             preview: this.PreviewBuilder({
111.               width: 500,
112.               height: 400,
113.               url:this.linkURL
114.             }),
115.             menuType: MenuType.PREVIEW_MENU,
116.           })
117.         .bindSelectionMenu(WebElementType.IMAGE, this.ImageMenuBuilder, WebResponseType.LONG_PRESS,
118.           {
119.             onAppear: () => {},
120.             onDisappear: () => {
121.               this.result?.closeContextMenu();
122.             },
123.             preview: PreviewBuilderGlobalForImage({
124.               previewImage: this.previewImage,
125.               width: this.previewWidthImage,
126.               height: this.previewHeightImage,
127.             }),
128.             menuType: MenuType.PREVIEW_MENU,
129.           })
130.         .zoomAccess(true)
131.         .onContextMenuShow((event) => {
132.           if (event) {
133.             this.result = event.result;
134.             this.previewWidthImage = this.uiContext!.px2vp(event.param.getPreviewWidth());
135.             this.previewHeightImage = this.uiContext!.px2vp(event.param.getPreviewHeight());
136.             if (event.param.getSourceUrl().indexOf("resource://rawfile/") == 0) {
137.               this.previewImage = $rawfile(event.param.getSourceUrl().substring(19));
138.             } else {
139.               this.previewImage = event.param.getSourceUrl();
140.             }
141.             this.linkURL = event.param.getLinkUrl()
142.             return true;
143.           }
144.           return false;
145.         })
146.     }

147.   }
148.   // 侧滑返回
149.   onBackPress(): boolean | void {
150.     if (this.controller.accessStep(-1)) {
151.       this.controller.backward();
152.       return true;
153.     } else {
154.       return false;
155.     }
156.   }
157. }

html示例

1. <html lang="zh-CN"><head>
2.     <meta charset="UTF-8">
3.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
4.     <title>综合信息页面</title>
5. </head>
6. <body>
7. <div>
8.     <h1>综合信息与联系详情</h1>
9.     <section>
10.         <a href="https://www.example.com">EXAMPLE</a>
11.         <br>
12.         <a href="https://www.example1.com/">EXAMPLE1</a>
13.     </section>
14. </div>
15. <footer>
16.     <p>请注意，以上提供的所有网址仅供演示之用。</p>
17. </footer>
18. </body>
19. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.33633664762060583012395909481144:50001231000000:2800:97E9A8B860230A665F2CCF3AC4A76042856DEE862F832DC6609FA7C77DD7037A.gif)

## Web菜单保存图片

1. 创建MenuBuilder组件作为菜单弹窗，使用[SaveButton](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-security-components-savebutton)组件实现图片保存，通过bindContextMenu将MenuBuilder与Web绑定。
2. 在onContextMenuShow中获取图片url，通过copyLocalPicToDir或copyUrlPicToDir将图片保存至应用沙箱。
3. 通过photoAccessHelper将应用沙箱中的图片保存至图库。

4. import { webview } from '@kit.ArkWeb';
5. import { common } from '@kit.AbilityKit';
6. import { fileIo as fs } from '@kit.CoreFileKit';
7. import { systemDateTime } from '@kit.BasicServicesKit';
8. import { http } from '@kit.NetworkKit';
9. import { photoAccessHelper } from '@kit.MediaLibraryKit';

10. @Entry
11. @Component
12. struct WebComponent {
13.   saveButtonOptions: SaveButtonOptions = {
14.     icon: SaveIconStyle.FULL_FILLED,
15.     text: SaveDescription.SAVE_IMAGE,
16.     buttonType: ButtonType.Capsule
17.   }
18.   controller: webview.WebviewController = new webview.WebviewController();
19.   @State showMenu: boolean = false;
20.   @State imgUrl: string = '';
21.   context = this.getUIContext().getHostContext() as common.UIAbilityContext;

22.   copyLocalPicToDir(rawfilePath: string, newFileName: string): string {
23.     let srcFileDes = this.context.resourceManager.getRawFdSync(rawfilePath);
24.     let dstPath = this.context.filesDir + "/" + newFileName;
25.     let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
26.     let bufsize = 4096;
27.     let buf = new ArrayBuffer(bufsize);
28.     let off = 0, len = 0, readedLen = 0;
29.     while (len = fs.readSync(srcFileDes.fd, buf, { offset: srcFileDes.offset + off, length: bufsize })) {
30.       readedLen += len;
31.       fs.writeSync(dest.fd, buf, { offset: off, length: len });
32.       off = off + len;
33.       if ((srcFileDes.length - readedLen) < bufsize) {
34.         bufsize = srcFileDes.length - readedLen;
35.       }
36.     }
37.     fs.close(dest.fd);
38.     return dest.path;
39.   }

40.   async copyUrlPicToDir(picUrl: string, newFileName: string): Promise<string> {
41.     let uri = '';
42.     let httpRequest = http.createHttp();
43.     let data: http.HttpResponse = await (httpRequest.request(picUrl) as Promise<http.HttpResponse>);
44.     if (data?.responseCode == http.ResponseCode.OK) {
45.       let dstPath = this.context.filesDir + "/" + newFileName;
46.       let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
47.       let writeLen: number = fs.writeSync(dest.fd, data.result as ArrayBuffer);
48.       uri = dest.path;
49.     }
50.     return uri;
51.   }

52.   @Builder
53.   MenuBuilder() {
54.     Column() {
55.       Row() {
56.         SaveButton(this.saveButtonOptions)
57.           .onClick(async (event, result: SaveButtonOnClickResult) => {
58.             if (result == SaveButtonOnClickResult.SUCCESS) {
59.               try {
60.                 let context = this.context;
61.                 let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);
62.                 let uri = '';
63.                 if (this.imgUrl?.includes('rawfile')) {
64.                   let rawFileName: string = this.imgUrl.substring(this.imgUrl.lastIndexOf('/') + 1);
65.                   uri = this.copyLocalPicToDir(rawFileName, 'copyFile.png');
66.                 } else if (this.imgUrl?.includes('http') || this.imgUrl?.includes('https')) {
67.                   uri = await this.copyUrlPicToDir(this.imgUrl, `onlinePic${systemDateTime.getTime()}.png`);
68.                 }
69.                 let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest =
70.                   photoAccessHelper.MediaAssetChangeRequest.createImageAssetRequest(context, uri);
71.                 await phAccessHelper.applyChanges(assetChangeRequest);
72.               } catch (err) {
73.                 console.error(`create asset failed with error: ${err.code}, ${err.message}`);
74.               }
75.             } else {
76.               console.error(`SaveButtonOnClickResult create asset failed`);
77.             }
78.             this.showMenu = false;
79.           })
80.       }
81.       .margin({ top: 20, bottom: 20 })
82.       .justifyContent(FlexAlign.Center)
83.     }
84.     .width('80')
85.     .backgroundColor(Color.White)
86.     .borderRadius(10)
87.   }

88.   build() {
89.     Column() {
90.       Web({ src: $rawfile("index.html"), controller: this.controller })
91.         .onContextMenuShow((event) => {
92.           if (event) {
93.             let hitValue = this.controller.getLastHitTest();
94.             this.imgUrl = hitValue.extra;
95.           }
96.           this.showMenu = true;
97.           return true;
98.         })
99.         .bindContextMenu(this.MenuBuilder, ResponseType.LongPress)
100.         .fileAccess(true)
101.         .javaScriptAccess(true)
102.         .domStorageAccess(true)
103.     }
104.   }
105. }

106. <!--index.html-->
107. <!DOCTYPE html>
108. <html>
109. <head>
110.     <title>SavePicture</title>
111. </head>
112. <body>
113. <h1>SavePicture</h1>
114. <br>
115. <br>
116. <br>
117. <br>
118. <br>
119. <!--startIcon.png为html同目录下图片-->
120. <img src="./startIcon.png">
121. </body>
122. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.97123562329824553018833148527255:50001231000000:2800:A32D115F0EF0E90D398B8AFB85EB09F317F303FBFAA0E7B554847ACBB1F69663.gif)

## Web菜单获取选中文本

Web组件的[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)接口中没有提供获取选中文本的方式。开发者可通过[javaScriptProxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#javascriptproxy)获取到JavaScript的选中文本，实现自定义菜单的逻辑。

1. 创建SelectClass类，通过[javaScriptProxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#javascriptproxy)将SelectClass对象注册到Web组件中。
2. 在Html侧注册选区变更监听器，在选区变更时通过SelectClass对象将选区设置到ArkTS侧。

3. import { webview } from '@kit.ArkWeb';
4. let selectText = '';

5. class SelectClass {
6.   constructor() {
7.   }

8.   setSelectText(param: String) {
9.     selectText = param.toString();
10.   }
11. }

12. @Entry
13. @Component
14. struct WebComponent {
15.   webController: webview.WebviewController = new webview.WebviewController();
16.   @State selectObj: SelectClass = new SelectClass();
17.   @State textStr: string = '';

18.   build() {
19.     Column() {
20.       Web({ src: $rawfile('index.html'), controller: this.webController})
21.         .javaScriptProxy({
22.           object: this.selectObj,
23.           name: 'selectObjName',
24.           methodList: ['setSelectText'],
25.           controller: this.webController
26.         })
27.         .height('40%')
28.       Text('Click here to get the selected text.')
29.         .fontSize(20)
30.         .onClick(() => {
31.           this.textStr = selectText;
32.         })
33.         .height('10%')
34.       Text('Selected text is ' + this.textStr)
35.         .fontSize(20)
36.         .height('10%')
37.     }
38.   }
39. }

40. <!DOCTYPE html>
41. <html>
42. <head>
43.     <title>Test Get Select</title>
44.     <style>
45.         body {
46.           margin: 40px;
47.           background-color: #f4f4f4;
48.         }
49.         .edit-container {
50.           padding: 20px;
51.           background-color: #fff;
52.           border-radius: 8px;
53.           box-shadow: 0 0 10px rgba(0,0,0,0.1);
54.           margin: auto;
55.         }
56.         textarea {
57.           width: 100%;
58.           height: 400px;
59.           font-size: 16px;
60.           padding: 10px;
61.           border: 1px solid #ccc;
62.           border-radius: 4px;
63.         }
64.     </style>
65. </head>
66. <body>
67. <div class="edit-container">
68.     <textarea placeholder="Enter the text here and select it by long pressing."></textarea>
69. </div>
70. <script>
71.     document.addEventListener('selectionchange', () => {
72.       var selection = window.getSelection();
73.       if(selection.rangeCount > 0) {
74.         var selectedText = selection.toString();
75.         selectObjName.setSelectText(selectedText);
76.       }
77.     })
78. </script>
79. </body>
80. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.94129462790581123369363129678496:50001231000000:2800:93E1A114511A7F2292811E9A6BCB58148AE5F5D439EBC45E71F51FF9AE7A5B22.gif)

## Web菜单识别图片二维码

在二维码跳转页面或者付款场景中，开发者可通过实现上下文菜单，获取到[onContextMenuShow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#oncontextmenushow9)接口中的二维码图片信息进行处理，提供给用户扫描二维码入口。

1. 创建MenuBuilder组件作为菜单弹窗，通过bindContextMenu将MenuBuilder与Web绑定。
2. 在onContextMenuShow中获取图片url，通过copyLocalPicToDir或copyUrlPicToDir将图片保存至应用沙箱。
3. 通过detectBarcode.decode解析保存在沙箱中的图片，获取到结果。

4. import { webview } from '@kit.ArkWeb';
5. import { common } from '@kit.AbilityKit';
6. import { fileIo as fs } from '@kit.CoreFileKit';
7. import { systemDateTime } from '@kit.BasicServicesKit';
8. import { http } from '@kit.NetworkKit';
9. import { scanCore, scanBarcode, detectBarcode } from '@kit.ScanKit';
10. import { BusinessError } from '@kit.BasicServicesKit';

11. @Entry
12. @Component
13. struct WebComponent {
14.   saveButtonOptions: SaveButtonOptions = {
15.     icon: SaveIconStyle.FULL_FILLED,
16.     text: SaveDescription.SAVE_IMAGE,
17.     buttonType: ButtonType.Capsule
18.   }
19.   controller: webview.WebviewController = new webview.WebviewController();
20.   private result: WebContextMenuResult | undefined = undefined;
21.   @State showMenu: boolean = false;
22.   @State imgUrl: string = '';
23.   @State decodeResult: string = '';
24.   context = this.getUIContext().getHostContext() as common.UIAbilityContext;

25.   copyLocalPicToDir(rawfilePath: string, newFileName: string): string {
26.     let srcFileDes = this.context.resourceManager.getRawFdSync(rawfilePath);
27.     let dstPath = this.context.filesDir + "/" + newFileName;
28.     let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
29.     let bufsize = 4096;
30.     let buf = new ArrayBuffer(bufsize);
31.     let off = 0, len = 0, readedLen = 0;
32.     while (len = fs.readSync(srcFileDes.fd, buf, { offset: srcFileDes.offset + off, length: bufsize })) {
33.       readedLen += len;
34.       fs.writeSync(dest.fd, buf, { offset: off, length: len });
35.       off = off + len;
36.       if ((srcFileDes.length - readedLen) < bufsize) {
37.         bufsize = srcFileDes.length - readedLen;
38.       }
39.     }
40.     fs.close(dest.fd);
41.     return dest.path;
42.   }

43.   async copyUrlPicToDir(picUrl: string, newFileName: string): Promise<string> {
44.     let uri = '';
45.     let httpRequest = http.createHttp();
46.     let data: http.HttpResponse = await (httpRequest.request(picUrl) as Promise<http.HttpResponse>);
47.     if (data?.responseCode == http.ResponseCode.OK) {
48.       let dstPath = this.context.filesDir + "/" + newFileName;
49.       let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
50.       let writeLen: number = fs.writeSync(dest.fd, data.result as ArrayBuffer);
51.       uri = dest.path;
52.     }
53.     return uri;
54.   }

55.   @Builder
56.   MenuBuilder() {
57.     Menu() {
58.       MenuItem({
59.         content: "Scan QR Code",
60.       })
61.         .width(200)
62.         .height(50)
63.         .onClick(async () => {
64.           try {
65.             let uri = '';
66.             if (this.imgUrl?.includes('rawfile')) {
67.               let rawFileName: string = this.imgUrl.substring(this.imgUrl.lastIndexOf('/') + 1);
68.               uri = this.copyLocalPicToDir(rawFileName, 'copyFile.png');
69.             } else if (this.imgUrl?.includes('http') || this.imgUrl?.includes('https')) {
70.               uri = await this.copyUrlPicToDir(this.imgUrl, `onlinePic${systemDateTime.getTime()}.png`);
71.             }
72.             let options: scanBarcode.ScanOptions =
73.               { scanTypes: [scanCore.ScanType.ALL], enableMultiMode: true, enableAlbum: true }
74.             let inputImage: detectBarcode.InputImage = { uri: uri };
75.             try {
76.               // 调用图片识码接口
77.               detectBarcode.decode(inputImage, options,
78.                 (error: BusinessError, result: Array<scanBarcode.ScanResult>) => {
79.                   if (error && error.code) {
80.                     console.error(`create asset failed with error: ${error.code}, ${error.message}`);
81.                     return;
82.                   }
83.                   this.decodeResult = JSON.stringify(result);
84.                 });
85.             } catch (err) {
86.               console.error(`Failed to detect Barcode. Code: ${err.code}, ${err.message}`);
87.             }
88.           } catch (err) {
89.             console.error(`create asset failed with error: ${err.code}, ${err.message}`);
90.           }
91.         })
92.     }
93.   }

94.   build() {
95.     Column() {
96.       Web({ src: $rawfile("index.html"), controller: this.controller })
97.         .onContextMenuShow((event) => {
98.           if (event) {
99.             let hitValue = this.controller.getLastHitTest();
100.             this.imgUrl = hitValue.extra;
101.           }
102.           this.showMenu = true;
103.           return true;
104.         })
105.         .bindContextMenu(this.MenuBuilder, ResponseType.LongPress)
106.         .fileAccess(true)
107.         .javaScriptAccess(true)
108.         .domStorageAccess(true)
109.         .height('40%')
110.       Text('Decode result is ' + this.decodeResult)
111.         .fontSize(20)
112.         .height('10%')
113.     }
114.   }
115. }

116. <!--index.html-->
117. <!DOCTYPE html>
118. <html>
119. <head>
120.     <title>test QR code</title>
121. </head>
122. <body>
123. <h1>Long press and click to scan the QR code</h1>
124. <!--img.png为二维码图片-->
125. <img src="img.png" >
126. </body>
127. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.06270991606947428599641497908057:50001231000000:2800:97D8807984201C3212A665587CF9F7A5A11AF6B44C1A4C37BB47527FBF41FB8B.gif)

## 常见问题

### 如何禁用长按选择时弹出菜单

可通过[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)接口将系统默认菜单全部过滤，此时无菜单项，则不会显示菜单。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct WebComponent {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   onCreateMenu(menuItems: Array<TextMenuItem>): Array<TextMenuItem> {
8.     let items = menuItems.filter((menuItem) => {
9.       // 过滤用户需要的系统按键
10.       return false;
11.     });
12.     return items;
13.   }

14.   onMenuItemClick(menuItem: TextMenuItem, textRange: TextRange): boolean {
15.     return false; // 返回默认值false
16.   }

17.   @State EditMenuOptions: EditMenuOptions = { onCreateMenu: this.onCreateMenu, onMenuItemClick: this.onMenuItemClick }

18.   build() {
19.     Column() {
20.       Web({ src: $rawfile("index.html"), controller: this.controller })
21.         .editMenuOptions(this.EditMenuOptions)
22.     }
23.   }
24. }

25. <!--index.html-->
26. <!DOCTYPE html>
27. <html>
28.   <head>
29.       <title>测试网页</title>
30.   </head>
31.   <body>
32.     <h1>editMenuOptions Demo</h1>
33.     <span>edit menu options</span>
34.   </body>
35. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.19330739680792383411363668468450:50001231000000:2800:2DA5BE11178E1B6384FC9FFE78DAC381DB88BD8FC74656B3CC0418D7C01C52FB.gif)

### 出现选区时手柄菜单不显示

可排查是否通过JS的[selection-api](https://www.w3.org/TR/selection-api/)对选区进行了操作，目前通过这种方式改变选区会导致手柄菜单不显示。

### 如何修改文本选中菜单的样式

从API version 21开始，应用可通过[bindSelectionMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#bindselectionmenu13)接口，实现自定义文本菜单。

**示例代码**

1. import { webview } from '@kit.ArkWeb';
2. import { BusinessError } from '@kit.BasicServicesKit';

3. @Entry
4. @Component
5. struct WebComponent {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   clearSelection() {
8.     try {
9.       this.controller.runJavaScript(
10.         'clearSelection()',
11.         (error, result) => {
12.           if (error) {
13.             console.error(`run clearSelection JavaScript error, ErrorCode: ${(error as BusinessError).code},  Message: $  {(error as BusinessError).message}`);
14.             return;
15.           }
16.           if (result) {
17.             console.info(`The clearSelection() return value is: ${result}`);
18.           }
19.         });
20.     } catch (error) {
21.       console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
22.     }
23.   }

24.   @Builder
25.   TextMenuBuilder() {
26.     Menu() {
27.       MenuItem({ content: 'Copy', })
28.         .onClick(() => {
29.           try {
30.             this.controller.runJavaScript(
31.               'copySelectedText()',
32.               (error, result) => {
33.                 if (error) {
34.                   console.error(`run copySelectedText JavaScript error, ErrorCode: ${(error as BusinessError).code},    Message: ${(error as BusinessError).message}`);
35.                   return;
36.                 }
37.                 if (result) {
38.                   console.info(`The copySelectedText() return value is: ${result}`);
39.                 }
40.               });
41.           } catch (error) {
42.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
43.           }
44.           this.clearSelection()
45.         }).backgroundColor(Color.Pink)
46.     }
47.   }
48.   build() {
49.     Column() {
50.       Web({ src: $rawfile('bindSelectionMenuText.html'), controller: this.controller })
51.         .javaScriptAccess(true)
52.         .fileAccess(true)
53.         .onlineImageAccess(true)
54.         .imageAccess(true)
55.         .domStorageAccess(true)
56.         .zoomAccess(true)
57.         .bindSelectionMenu(WebElementType.TEXT, this.TextMenuBuilder, WebResponseType.LONG_PRESS,
58.           {
59.             onAppear: () => {},
60.             onDisappear: () => {},
61.             menuType: MenuType.SELECTION_MENU,
62.           })
63.     }
64.   }
65.   onBackPress(): boolean | void {
66.     if (this.controller.accessStep(-1)) {
67.       this.controller.backward();
68.       return true;
69.     } else {
70.       return false;
71.     }
72.   }
73. }

74. <!--bindSelectionMenuText.html-->
75. <!DOCTYPE html>
76. <html lang="zh-CN">
77. <head>
78.     <meta charset="UTF-8">
79.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
80.     <title>自定义文本菜单</title>
81.     <style>
82.         .container {
83.             background-color: white;
84.             padding: 30px;
85.             margin: 20px 0;
86.         }

87.         .context {
88.             line-height: 1.8;
89.             font-size: 18px;
90.         }

91.         .context span {
92.             border-radius: 8px;
93.             background-color: #f8f9fa;
94.         }
95.     </style>
96. </head>
97. <body>
98. <div class="container">
99.     <div class="context">
100.         <span>在这个数字时代，文本复制功能变得日益重要。无论是引用名言、保存重要信息，还是分享有趣的内容，复制文本都是我们日常操作的  一部分。</span>
101.     </div>
102. </div>

103. <script>
104.   function copySelectedText() {
105.       const selectedText = window.getSelection().toString();
106.       if (selectedText.length > 0) {
107.           // 使用Clipboard API复制文本
108.           navigator.clipboard.writeText(selectedText)
109.               .then(() => {
110.                   showNotification();
111.               })
112.               .catch(err => {
113.                   console.error('copy failed:', err);
114.               });
115.       }
116.   }
117.   function clearSelection() {
118.     if (window.getSelection) {
119.       window.getSelection().removeAllRanges();
120.     }
121.   }
122. </script>
123. </body>
124. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.70221801701384901506701052920143:50001231000000:2800:704F509ECFEBC24550C0F3C204FCA88122F73B934B99E2B26EA35EEAD25F3F21.gif)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-safe-area-insets "网页中安全区域计算和避让适配")
# 使用Web组件菜单处理网页内容

更新时间: 2025-12-16 16:38

菜单作为用户交互的关键组件，其作用是构建清晰的导航体系，通过结构化布局展示功能入口，使用户能够迅速找到目标内容或执行操作。作为人机交互的重要枢纽，它显著提升了Web组件的可访问性和用户体验，是应用设计中必不可少的部分。Web组件菜单类型包括[文本选中菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E6%96%87%E6%9C%AC%E9%80%89%E4%B8%AD%E8%8F%9C%E5%8D%95)、[上下文菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E4%B8%8A%E4%B8%8B%E6%96%87%E8%8F%9C%E5%8D%95)和[自定义菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%8F%9C%E5%8D%95)，应用可根据具体需求灵活选择。

|菜单类型|目标元素|响应类型|是否支持自定义|
|:--|:--|:--|:--|
|[文本选中菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E6%96%87%E6%9C%AC%E9%80%89%E4%B8%AD%E8%8F%9C%E5%8D%95)|文本|手势长按|可增减菜单项，菜单样式不可自定义|
|[上下文菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E4%B8%8A%E4%B8%8B%E6%96%87%E8%8F%9C%E5%8D%95)|超链接、图片、文字|手势长按、鼠标右键|支持通过菜单组件自定义|
|[自定义菜单](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web_menu#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%8F%9C%E5%8D%95)|图片|手势长按|支持通过菜单组件自定义|

## 文本选中菜单

Web组件的文本选中菜单是一种通过自定义元素实现的上下文交互组件，当用户选中文本时会动态显示，提供复制、分享、标注等语义化操作，具备标准化功能与可扩展性，是移动端文本操作的核心功能。文本选中菜单在用户长按选中文本或编辑状态下长按出现单手柄时弹出，菜单项横向排列。系统提供默认的菜单实现。应用可通过[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)接口对文本选中菜单进行自定义操作。

1. 通过onCreateMenu方法自定义菜单项，通过操作Array<[TextMenuItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-text-common#textmenuitem12%E5%AF%B9%E8%B1%A1%E8%AF%B4%E6%98%8E)>数组可对显示菜单项进行增减操作，在[TextMenuItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-text-common#textmenuitem12%E5%AF%B9%E8%B1%A1%E8%AF%B4%E6%98%8E)中定义菜单项名称、图标、ID等内容。
2. 通过onMenuItemClick方法处理菜单项点击事件，当返回false时会执行系统默认逻辑。
3. 创建一个[EditMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-text-common#editmenuoptions)对象，包含onCreateMenu和onMenuItemClick两个方法，通过Web组件的[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)方法与Web组件绑定。

4. // xxx.ets
5. import { webview } from '@kit.ArkWeb';

6. @Entry
7. @Component
8. struct WebComponent {
9.   controller: webview.WebviewController = new webview.WebviewController();

10.   onCreateMenu(menuItems: Array<TextMenuItem>): Array<TextMenuItem> {
11.     let items = menuItems.filter((menuItem) => {
12.       // 过滤用户需要的系统按键
13.       return (
14.         menuItem.id.equals(TextMenuItemId.CUT) ||
15.         menuItem.id.equals(TextMenuItemId.COPY) ||
16.         menuItem.id.equals(TextMenuItemId.PASTE)
17.       );
18.     });
19.     let customItem1: TextMenuItem = {
20.       content: 'customItem1',
21.       id: TextMenuItemId.of('customItem1'),
22.       icon: $r('app.media.startIcon')
23.     };
24.     let customItem2: TextMenuItem = {
25.       content: $r('app.string.EntryAbility_label'),
26.       id: TextMenuItemId.of('customItem2'),
27.       icon: $r('app.media.startIcon')
28.     };
29.     items.push(customItem1); // 在选项列表后添加新选项
30.     items.unshift(customItem2); // 在选项列表前添加选项
31.     items.push(customItem1);
32.     items.push(customItem1);
33.     items.push(customItem1);
34.     items.push(customItem1);
35.     items.push(customItem1);
36.     return items;
37.   }

38.   onMenuItemClick(menuItem: TextMenuItem, textRange: TextRange): boolean {
39.     if (menuItem.id.equals(TextMenuItemId.CUT)) {
40.       // 用户自定义行为
41.       console.info("拦截 id：CUT")
42.       return true; // 返回true不执行系统回调
43.     } else if (menuItem.id.equals(TextMenuItemId.COPY)) {
44.       // 用户自定义行为
45.       console.info("不拦截 id：COPY")
46.       return false; // 返回false执行系统回调
47.     } else if (menuItem.id.equals(TextMenuItemId.of('customItem1'))) {
48.       // 用户自定义行为
49.       console.info("拦截 id：customItem1")
50.       return true; // 用户自定义菜单选项返回true时点击后不关闭菜单，返回false时关闭菜单
51.     } else if (menuItem.id.equals(TextMenuItemId.of('customItem2'))) {
52.       // 用户自定义行为
53.       console.info("拦截 id：customItem2")
54.       return true;
55.     }
56.     return false; // 返回默认值false
57.   }

58.   @State EditMenuOptions: EditMenuOptions = { onCreateMenu: this.onCreateMenu, onMenuItemClick: this.onMenuItemClick }

59.   build() {
60.     Column() {
61.       Web({ src: $rawfile("index.html"), controller: this.controller })
62.         .editMenuOptions(this.EditMenuOptions)
63.     }
64.   }
65. }

66. <!--index.html-->
67. <!DOCTYPE html>
68. <html>
69.   <head>
70.       <title>测试网页</title>
71.   </head>
72.   <body>
73.     <h1>editMenuOptions Demo</h1>
74.     <span>edit menu options</span>
75.   </body>
76. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.74683493357399651917983596502008:50001231000000:2800:5C244201AEDBD0BBE0E393950817D83405FFC2A941DB3153458274C6BA40BF7D.gif)

## 上下文菜单

上下文菜单是用户通过特定操作（如右键点击或长按富文本）触发的快捷菜单，用于提供与当前操作对象或界面元素相关的功能选项。菜单项纵向排列。系统未提供默认实现，若应用未实现，则不显示上下文菜单。应用需要创建一个[Menu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-menu)组件并与Web绑定，在菜单弹出时可通过Web组件的[onContextMenuShow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#oncontextmenushow9)回调接口获取上下文菜单的详细信息，包括点击位置的HTML元素信息及点击位置信息。

1. [Menu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-menu)组件作为弹出的菜单，包含所有菜单项行为与样式。
2. 使用bindPopup方法将Menu组件与Web组件绑定。当上下文菜单弹出时，将显示创建的Menu组件。
3. 在onContextMenuShow回调中获取上下文菜单事件信息[onContextMenuShowEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-i#oncontextmenushowevent12)。其中param为[WebContextMenuParam](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-webcontextmenuparam)类型，包含点击位置对应HTML元素信息和位置信息，result为[WebContextMenuResult](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-webcontextmenuresult)类型，提供常见的菜单能力。

4. // xxx.ets
5. import { webview } from '@kit.ArkWeb';
6. import { pasteboard } from '@kit.BasicServicesKit';

7. const TAG = 'ContextMenu';

8. @Entry
9. @Component
10. struct WebComponent {
11.   controller: webview.WebviewController = new webview.WebviewController();
12.   private result: WebContextMenuResult | undefined = undefined;
13.   @State linkUrl: string = '';
14.   @State offsetX: number = 0;
15.   @State offsetY: number = 0;
16.   @State showMenu: boolean = false;
17.   uiContext: UIContext = this.getUIContext();

18.   @Builder
19.   // 构建自定义菜单及触发功能接口
20.   MenuBuilder() {
21.     // 以垂直列表形式显示的菜单。
22.     Menu() {
23.       // 展示菜单Menu中具体的item菜单项。
24.       MenuItem({
25.         content: '复制图片',
26.       })
27.         .width(100)
28.         .height(50)
29.         .onClick(() => {
30.           this.result?.copyImage();
31.           this.showMenu = false;
32.         })
33.       MenuItem({
34.         content: '剪切',
35.       })
36.         .width(100)
37.         .height(50)
38.         .onClick(() => {
39.           this.result?.cut();
40.           this.showMenu = false;
41.         })
42.       MenuItem({
43.         content: '复制',
44.       })
45.         .width(100)
46.         .height(50)
47.         .onClick(() => {
48.           this.result?.copy();
49.           this.showMenu = false;
50.         })
51.       MenuItem({
52.         content: '粘贴',
53.       })
54.         .width(100)
55.         .height(50)
56.         .onClick(() => {
57.           this.result?.paste();
58.           this.showMenu = false;
59.         })
60.       MenuItem({
61.         content: '复制链接',
62.       })
63.         .width(100)
64.         .height(50)
65.         .onClick(() => {
66.           let pasteData = pasteboard.createData('text/plain', this.linkUrl);
67.           pasteboard.getSystemPasteboard().setData(pasteData, (error) => {
68.             if (error) {
69.               return;
70.             }
71.           })
72.           this.showMenu = false;
73.         })
74.       MenuItem({
75.         content: '全选',
76.       })
77.         .width(100)
78.         .height(50)
79.         .onClick(() => {
80.           this.result?.selectAll();
81.           this.showMenu = false;
82.         })
83.     }
84.     .width(150)
85.     .height(300)
86.   }

87.   build() {
88.     Column() {
89.       Web({ src: $rawfile("index.html"), controller: this.controller })
90.         // 触发自定义弹窗
91.         .onContextMenuShow((event) => {
92.           if (event) {
93.             this.result = event.result
94.             console.info("x coord = " + event.param.x());
95.             console.info("link url = " + event.param.getLinkUrl());
96.             this.linkUrl = event.param.getLinkUrl();
97.           }
98.           console.info(TAG, `x: ${this.offsetX}, y: ${this.offsetY}`);
99.           this.showMenu = true;
100.           this.offsetX = 0;
101.           this.offsetY = Math.max(this.uiContext!.px2vp(event?.param.y() ?? 0) - 0, 0);
102.           return true;
103.         })
104.         .bindPopup(this.showMenu,
105.           {
106.             builder: this.MenuBuilder(),
107.             enableArrow: false,
108.             placement: Placement.LeftTop,
109.             offset: { x: this.offsetX, y: this.offsetY },
110.             mask: false,
111.             onStateChange: (e) => {
112.               if (!e.isVisible) {
113.                 this.showMenu = false;
114.                 this.result!.closeContextMenu();
115.               }
116.             }
117.           })
118.     }
119.   }
120. }

121. <!-- index.html -->
122. <!DOCTYPE html>
123. <html lang="en">
124. <body>
125.   <h1>onContextMenuShow</h1>
126.   <a href="http://www.example.com" style="font-size:27px">超链接www.example.com</a>
127.   <!--example.png为html同目录下图片-->
128.   <div><img src="example.png"></div>
129.   <p>选中文字鼠标右键弹出菜单</p>
130. </body>
131. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.29451072078178417578416765697859:50001231000000:2800:3A77588D209390352CED6A77358F1BB92F86D7587F33E8FE5723170BA62D6076.gif)

## 自定义菜单

自定义菜单赋予开发者灵活控制菜单触发时机与视觉呈现的能力，使应用能够根据用户操作场景动态匹配功能入口，显著简化开发过程中的界面适配工作，同时让交互体验更贴近用户直觉。

开发者可通过[bindSelectionMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#bindselectionmenu13)接口实现自定义菜单功能。目前，已额外支持通过长按图片、链接和文本，触发自定义菜单及自定义文本菜单。

1. 创建[Menu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-menu)组件作为菜单弹窗。
2. 通过Web组件的[bindSelectionMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#bindselectionmenu13)方法绑定MenuBuilder菜单弹窗。将[WebElementType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webelementtype13)设置为WebElementType.IMAGE，[responseType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#webresponsetype13)设置为WebResponseType.LONG_PRESS，表示长按图片时弹出菜单。在[options](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-i#selectionmenuoptionsext13)中定义菜单显示回调onAppear、菜单消失回调onDisappear、预览窗口preview和菜单类型menuType。

3. // xxx.ets
4. import { webview } from '@kit.ArkWeb';

5. interface PreviewBuilderParam {
6.   previewImage: Resource | string | undefined;
7.   width: number;
8.   height: number;
9. }

10. @Builder function PreviewBuilderGlobal($$: PreviewBuilderParam) {
11.   Column() {
12.     Image($$.previewImage)
13.       .objectFit(ImageFit.Fill)
14.       .autoResize(true)
15.   }.width($$.width).height($$.height)
16. }

17. @Entry
18. @Component
19. struct WebComponent {
20.   controller: webview.WebviewController = new webview.WebviewController();

21.   private result: WebContextMenuResult | undefined = undefined;
22.   @State previewImage: Resource | string | undefined = undefined;
23.   @State previewWidth: number = 0;
24.   @State previewHeight: number = 0;
25.   uiContext: UIContext = this.getUIContext();

26.   @Builder
27.   MenuBuilder() {
28.     Menu() {
29.       MenuItem({ content: '复制', })
30.         .onClick(() => {
31.           this.result?.copy();
32.           this.result?.closeContextMenu();
33.         })
34.       MenuItem({ content: '全选', })
35.         .onClick(() => {
36.           this.result?.selectAll();
37.           this.result?.closeContextMenu();
38.         })
39.     }
40.   }
41.   build() {
42.     Column() {
43.       Web({ src: $rawfile("index.html"), controller: this.controller })
44.         .bindSelectionMenu(WebElementType.IMAGE, this.MenuBuilder, WebResponseType.LONG_PRESS,
45.           {
46.             onAppear: () => {},
47.             onDisappear: () => {
48.               this.result?.closeContextMenu();
49.             },
50.             preview: PreviewBuilderGlobal({
51.               previewImage: this.previewImage,
52.               width: this.previewWidth,
53.               height: this.previewHeight
54.             }),
55.             menuType: MenuType.PREVIEW_MENU
56.           })
57.         .onContextMenuShow((event) => {
58.             if (event) {
59.               this.result = event.result;
60.               if (event.param.getLinkUrl()) {
61.                 return false;
62.               }
63.               this.previewWidth = this.uiContext!.px2vp(event.param.getPreviewWidth());
64.               this.previewHeight = this.uiContext!.px2vp(event.param.getPreviewHeight());
65.               if (event.param.getSourceUrl().indexOf("resource://rawfile/") == 0) {
66.                 this.previewImage = $rawfile(event.param.getSourceUrl().substr(19));
67.               } else {
68.                 this.previewImage = event.param.getSourceUrl();
69.               }
70.               return true;
71.             }
72.             return false;
73.           })
74.     }
75.   }
76. }

77. <!--index.html-->
78. <!DOCTYPE html>
79. <html>
80.   <head>
81.       <title>测试网页</title>
82.   </head>
83.   <body>
84.     <h1>bindSelectionMenu Demo</h1>
85.     <!--img.png为html同目录下图片-->
86.     <img src="./img.png" >
87.   </body>
88. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.59434873944830234144482178513845:50001231000000:2800:1B04AF1C73E70FDF30D79EF1FE13DCFD9AA0AC6DC2DC838A7687153EADBA00DB.gif)

自API version 20起，支持绑定长按超链接菜单。可以为图片和链接绑定不同的自定义菜单。

以下示例中，PreviewBuilder定义了超链接对应菜单的弹出内容，用Web组件加载了超链接内容，使用[Progress组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-common-components-progress-indicator)展示了加载进度。

1. import { webview } from '@kit.ArkWeb';
2. import { pasteboard } from '@kit.BasicServicesKit';

3. interface PreviewBuilderParam {
4.   width: number;
5.   height: number;
6.   url:Resource | string | undefined;
7. }

8. interface PreviewBuilderParamForImage {
9.   previewImage: Resource | string | undefined;
10.   width: number;
11.   height: number;
12. }

13. @Builder function PreviewBuilderGlobalForImage($$: PreviewBuilderParamForImage) {
14.   Column() {
15.     Image($$.previewImage)
16.       .objectFit(ImageFit.Fill)
17.       .autoResize(true)
18.   }.width($$.width).height($$.height)
19. }

20. @Entry
21. @Component
22. struct SelectionMenuLongPress {
23.   controller: webview.WebviewController = new webview.WebviewController();
24.   previewController: webview.WebviewController = new webview.WebviewController();
25.   @Builder PreviewBuilder($$: PreviewBuilderParam){
26.     Column() {
27.       Stack(){
28.         Text("") // 可选择是否展示url
29.           .padding(5)
30.           .width('100%')
31.           .textAlign(TextAlign.Start)
32.           .backgroundColor(Color.White)
33.           .copyOption(CopyOptions.LocalDevice)
34.           .maxLines(1)
35.           .textOverflow({overflow:TextOverflow.Ellipsis})
36.         Progress({ value: this.progressValue, total: 100, type: ProgressType.Linear }) // 展示进度条
37.           .style({ strokeWidth: 3, enableSmoothEffect: true })
38.           .backgroundColor(Color.White)
39.           .opacity(this.progressVisible?1:0)
40.           .backgroundColor(Color.White)
41.       }.alignContent(Alignment.Bottom)
42.       Web({src:$$.url,controller: new webview.WebviewController()})
43.         .javaScriptAccess(true)
44.         .fileAccess(true)
45.         .onlineImageAccess(true)
46.         .imageAccess(true)
47.         .domStorageAccess(true)
48.         .onPageBegin(()=>{
49.           this.progressValue = 0;
50.           this.progressVisible = true;
51.         })
52.         .onProgressChange((event)=>{
53.           this.progressValue = event.newProgress;
54.         })
55.         .onPageEnd(()=>{
56.           this.progressVisible = false;
57.         })
58.         .hitTestBehavior(HitTestMode.None) // 使预览Web不响应手势
59.     }.width($$.width).height($$.height) // 设置预览宽高
60.   }

61.   private result: WebContextMenuResult | undefined = undefined;
62.   @State previewImage: Resource | string | undefined = undefined;
63.   @State previewWidth: number = 1;
64.   @State previewHeight: number = 1;
65.   @State previewWidthImage: number = 1;
66.   @State previewHeightImage: number = 1;
67.   @State linkURL:string = "";
68.   @State progressValue:number = 0;
69.   @State progressVisible:boolean = true;
70.   uiContext: UIContext = this.getUIContext();

71.   @Builder
72.   LinkMenuBuilder() {
73.     Menu() {
74.       MenuItem({ content: '复制链接', })
75.         .onClick(() => {
76.           const pasteboardData = pasteboard.createData(pasteboard.MIMETYPE_TEXT_PLAIN, this.linkURL);
77.           const systemPasteboard = pasteboard.getSystemPasteboard();
78.           systemPasteboard.setData(pasteboardData);
79.         })
80.       MenuItem({content:'打开链接'})
81.         .onClick(()=>{
82.           this.controller.loadUrl(this.linkURL);
83.         })
84.     }
85.   }
86.   @Builder
87.   ImageMenuBuilder() {
88.     Menu() {
89.       MenuItem({ content: '复制图片', })
90.         .onClick(() => {
91.           this.result?.copyImage();
92.           this.result?.closeContextMenu();
93.         })
94.     }
95.   }
96.   build() {
97.     Column() {
98.       Web({ src: $rawfile("index.html"), controller: this.controller })
99.         .javaScriptAccess(true)
100.         .fileAccess(true)
101.         .onlineImageAccess(true)
102.         .imageAccess(true)
103.         .domStorageAccess(true)
104.         .bindSelectionMenu(WebElementType.LINK, this.LinkMenuBuilder, WebResponseType.LONG_PRESS,
105.           {
106.             onAppear: () => {},
107.             onDisappear: () => {
108.               this.result?.closeContextMenu();
109.             },
110.             preview: this.PreviewBuilder({
111.               width: 500,
112.               height: 400,
113.               url:this.linkURL
114.             }),
115.             menuType: MenuType.PREVIEW_MENU,
116.           })
117.         .bindSelectionMenu(WebElementType.IMAGE, this.ImageMenuBuilder, WebResponseType.LONG_PRESS,
118.           {
119.             onAppear: () => {},
120.             onDisappear: () => {
121.               this.result?.closeContextMenu();
122.             },
123.             preview: PreviewBuilderGlobalForImage({
124.               previewImage: this.previewImage,
125.               width: this.previewWidthImage,
126.               height: this.previewHeightImage,
127.             }),
128.             menuType: MenuType.PREVIEW_MENU,
129.           })
130.         .zoomAccess(true)
131.         .onContextMenuShow((event) => {
132.           if (event) {
133.             this.result = event.result;
134.             this.previewWidthImage = this.uiContext!.px2vp(event.param.getPreviewWidth());
135.             this.previewHeightImage = this.uiContext!.px2vp(event.param.getPreviewHeight());
136.             if (event.param.getSourceUrl().indexOf("resource://rawfile/") == 0) {
137.               this.previewImage = $rawfile(event.param.getSourceUrl().substring(19));
138.             } else {
139.               this.previewImage = event.param.getSourceUrl();
140.             }
141.             this.linkURL = event.param.getLinkUrl()
142.             return true;
143.           }
144.           return false;
145.         })
146.     }

147.   }
148.   // 侧滑返回
149.   onBackPress(): boolean | void {
150.     if (this.controller.accessStep(-1)) {
151.       this.controller.backward();
152.       return true;
153.     } else {
154.       return false;
155.     }
156.   }
157. }

html示例

1. <html lang="zh-CN"><head>
2.     <meta charset="UTF-8">
3.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
4.     <title>综合信息页面</title>
5. </head>
6. <body>
7. <div>
8.     <h1>综合信息与联系详情</h1>
9.     <section>
10.         <a href="https://www.example.com">EXAMPLE</a>
11.         <br>
12.         <a href="https://www.example1.com/">EXAMPLE1</a>
13.     </section>
14. </div>
15. <footer>
16.     <p>请注意，以上提供的所有网址仅供演示之用。</p>
17. </footer>
18. </body>
19. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.33633664762060583012395909481144:50001231000000:2800:97E9A8B860230A665F2CCF3AC4A76042856DEE862F832DC6609FA7C77DD7037A.gif)

## Web菜单保存图片

1. 创建MenuBuilder组件作为菜单弹窗，使用[SaveButton](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-security-components-savebutton)组件实现图片保存，通过bindContextMenu将MenuBuilder与Web绑定。
2. 在onContextMenuShow中获取图片url，通过copyLocalPicToDir或copyUrlPicToDir将图片保存至应用沙箱。
3. 通过photoAccessHelper将应用沙箱中的图片保存至图库。

4. import { webview } from '@kit.ArkWeb';
5. import { common } from '@kit.AbilityKit';
6. import { fileIo as fs } from '@kit.CoreFileKit';
7. import { systemDateTime } from '@kit.BasicServicesKit';
8. import { http } from '@kit.NetworkKit';
9. import { photoAccessHelper } from '@kit.MediaLibraryKit';

10. @Entry
11. @Component
12. struct WebComponent {
13.   saveButtonOptions: SaveButtonOptions = {
14.     icon: SaveIconStyle.FULL_FILLED,
15.     text: SaveDescription.SAVE_IMAGE,
16.     buttonType: ButtonType.Capsule
17.   }
18.   controller: webview.WebviewController = new webview.WebviewController();
19.   @State showMenu: boolean = false;
20.   @State imgUrl: string = '';
21.   context = this.getUIContext().getHostContext() as common.UIAbilityContext;

22.   copyLocalPicToDir(rawfilePath: string, newFileName: string): string {
23.     let srcFileDes = this.context.resourceManager.getRawFdSync(rawfilePath);
24.     let dstPath = this.context.filesDir + "/" + newFileName;
25.     let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
26.     let bufsize = 4096;
27.     let buf = new ArrayBuffer(bufsize);
28.     let off = 0, len = 0, readedLen = 0;
29.     while (len = fs.readSync(srcFileDes.fd, buf, { offset: srcFileDes.offset + off, length: bufsize })) {
30.       readedLen += len;
31.       fs.writeSync(dest.fd, buf, { offset: off, length: len });
32.       off = off + len;
33.       if ((srcFileDes.length - readedLen) < bufsize) {
34.         bufsize = srcFileDes.length - readedLen;
35.       }
36.     }
37.     fs.close(dest.fd);
38.     return dest.path;
39.   }

40.   async copyUrlPicToDir(picUrl: string, newFileName: string): Promise<string> {
41.     let uri = '';
42.     let httpRequest = http.createHttp();
43.     let data: http.HttpResponse = await (httpRequest.request(picUrl) as Promise<http.HttpResponse>);
44.     if (data?.responseCode == http.ResponseCode.OK) {
45.       let dstPath = this.context.filesDir + "/" + newFileName;
46.       let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
47.       let writeLen: number = fs.writeSync(dest.fd, data.result as ArrayBuffer);
48.       uri = dest.path;
49.     }
50.     return uri;
51.   }

52.   @Builder
53.   MenuBuilder() {
54.     Column() {
55.       Row() {
56.         SaveButton(this.saveButtonOptions)
57.           .onClick(async (event, result: SaveButtonOnClickResult) => {
58.             if (result == SaveButtonOnClickResult.SUCCESS) {
59.               try {
60.                 let context = this.context;
61.                 let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);
62.                 let uri = '';
63.                 if (this.imgUrl?.includes('rawfile')) {
64.                   let rawFileName: string = this.imgUrl.substring(this.imgUrl.lastIndexOf('/') + 1);
65.                   uri = this.copyLocalPicToDir(rawFileName, 'copyFile.png');
66.                 } else if (this.imgUrl?.includes('http') || this.imgUrl?.includes('https')) {
67.                   uri = await this.copyUrlPicToDir(this.imgUrl, `onlinePic${systemDateTime.getTime()}.png`);
68.                 }
69.                 let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest =
70.                   photoAccessHelper.MediaAssetChangeRequest.createImageAssetRequest(context, uri);
71.                 await phAccessHelper.applyChanges(assetChangeRequest);
72.               } catch (err) {
73.                 console.error(`create asset failed with error: ${err.code}, ${err.message}`);
74.               }
75.             } else {
76.               console.error(`SaveButtonOnClickResult create asset failed`);
77.             }
78.             this.showMenu = false;
79.           })
80.       }
81.       .margin({ top: 20, bottom: 20 })
82.       .justifyContent(FlexAlign.Center)
83.     }
84.     .width('80')
85.     .backgroundColor(Color.White)
86.     .borderRadius(10)
87.   }

88.   build() {
89.     Column() {
90.       Web({ src: $rawfile("index.html"), controller: this.controller })
91.         .onContextMenuShow((event) => {
92.           if (event) {
93.             let hitValue = this.controller.getLastHitTest();
94.             this.imgUrl = hitValue.extra;
95.           }
96.           this.showMenu = true;
97.           return true;
98.         })
99.         .bindContextMenu(this.MenuBuilder, ResponseType.LongPress)
100.         .fileAccess(true)
101.         .javaScriptAccess(true)
102.         .domStorageAccess(true)
103.     }
104.   }
105. }

106. <!--index.html-->
107. <!DOCTYPE html>
108. <html>
109. <head>
110.     <title>SavePicture</title>
111. </head>
112. <body>
113. <h1>SavePicture</h1>
114. <br>
115. <br>
116. <br>
117. <br>
118. <br>
119. <!--startIcon.png为html同目录下图片-->
120. <img src="./startIcon.png">
121. </body>
122. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.97123562329824553018833148527255:50001231000000:2800:A32D115F0EF0E90D398B8AFB85EB09F317F303FBFAA0E7B554847ACBB1F69663.gif)

## Web菜单获取选中文本

Web组件的[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)接口中没有提供获取选中文本的方式。开发者可通过[javaScriptProxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#javascriptproxy)获取到JavaScript的选中文本，实现自定义菜单的逻辑。

1. 创建SelectClass类，通过[javaScriptProxy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#javascriptproxy)将SelectClass对象注册到Web组件中。
2. 在Html侧注册选区变更监听器，在选区变更时通过SelectClass对象将选区设置到ArkTS侧。

3. import { webview } from '@kit.ArkWeb';
4. let selectText = '';

5. class SelectClass {
6.   constructor() {
7.   }

8.   setSelectText(param: String) {
9.     selectText = param.toString();
10.   }
11. }

12. @Entry
13. @Component
14. struct WebComponent {
15.   webController: webview.WebviewController = new webview.WebviewController();
16.   @State selectObj: SelectClass = new SelectClass();
17.   @State textStr: string = '';

18.   build() {
19.     Column() {
20.       Web({ src: $rawfile('index.html'), controller: this.webController})
21.         .javaScriptProxy({
22.           object: this.selectObj,
23.           name: 'selectObjName',
24.           methodList: ['setSelectText'],
25.           controller: this.webController
26.         })
27.         .height('40%')
28.       Text('Click here to get the selected text.')
29.         .fontSize(20)
30.         .onClick(() => {
31.           this.textStr = selectText;
32.         })
33.         .height('10%')
34.       Text('Selected text is ' + this.textStr)
35.         .fontSize(20)
36.         .height('10%')
37.     }
38.   }
39. }

40. <!DOCTYPE html>
41. <html>
42. <head>
43.     <title>Test Get Select</title>
44.     <style>
45.         body {
46.           margin: 40px;
47.           background-color: #f4f4f4;
48.         }
49.         .edit-container {
50.           padding: 20px;
51.           background-color: #fff;
52.           border-radius: 8px;
53.           box-shadow: 0 0 10px rgba(0,0,0,0.1);
54.           margin: auto;
55.         }
56.         textarea {
57.           width: 100%;
58.           height: 400px;
59.           font-size: 16px;
60.           padding: 10px;
61.           border: 1px solid #ccc;
62.           border-radius: 4px;
63.         }
64.     </style>
65. </head>
66. <body>
67. <div class="edit-container">
68.     <textarea placeholder="Enter the text here and select it by long pressing."></textarea>
69. </div>
70. <script>
71.     document.addEventListener('selectionchange', () => {
72.       var selection = window.getSelection();
73.       if(selection.rangeCount > 0) {
74.         var selectedText = selection.toString();
75.         selectObjName.setSelectText(selectedText);
76.       }
77.     })
78. </script>
79. </body>
80. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163847.94129462790581123369363129678496:50001231000000:2800:93E1A114511A7F2292811E9A6BCB58148AE5F5D439EBC45E71F51FF9AE7A5B22.gif)

## Web菜单识别图片二维码

在二维码跳转页面或者付款场景中，开发者可通过实现上下文菜单，获取到[onContextMenuShow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#oncontextmenushow9)接口中的二维码图片信息进行处理，提供给用户扫描二维码入口。

1. 创建MenuBuilder组件作为菜单弹窗，通过bindContextMenu将MenuBuilder与Web绑定。
2. 在onContextMenuShow中获取图片url，通过copyLocalPicToDir或copyUrlPicToDir将图片保存至应用沙箱。
3. 通过detectBarcode.decode解析保存在沙箱中的图片，获取到结果。

4. import { webview } from '@kit.ArkWeb';
5. import { common } from '@kit.AbilityKit';
6. import { fileIo as fs } from '@kit.CoreFileKit';
7. import { systemDateTime } from '@kit.BasicServicesKit';
8. import { http } from '@kit.NetworkKit';
9. import { scanCore, scanBarcode, detectBarcode } from '@kit.ScanKit';
10. import { BusinessError } from '@kit.BasicServicesKit';

11. @Entry
12. @Component
13. struct WebComponent {
14.   saveButtonOptions: SaveButtonOptions = {
15.     icon: SaveIconStyle.FULL_FILLED,
16.     text: SaveDescription.SAVE_IMAGE,
17.     buttonType: ButtonType.Capsule
18.   }
19.   controller: webview.WebviewController = new webview.WebviewController();
20.   private result: WebContextMenuResult | undefined = undefined;
21.   @State showMenu: boolean = false;
22.   @State imgUrl: string = '';
23.   @State decodeResult: string = '';
24.   context = this.getUIContext().getHostContext() as common.UIAbilityContext;

25.   copyLocalPicToDir(rawfilePath: string, newFileName: string): string {
26.     let srcFileDes = this.context.resourceManager.getRawFdSync(rawfilePath);
27.     let dstPath = this.context.filesDir + "/" + newFileName;
28.     let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
29.     let bufsize = 4096;
30.     let buf = new ArrayBuffer(bufsize);
31.     let off = 0, len = 0, readedLen = 0;
32.     while (len = fs.readSync(srcFileDes.fd, buf, { offset: srcFileDes.offset + off, length: bufsize })) {
33.       readedLen += len;
34.       fs.writeSync(dest.fd, buf, { offset: off, length: len });
35.       off = off + len;
36.       if ((srcFileDes.length - readedLen) < bufsize) {
37.         bufsize = srcFileDes.length - readedLen;
38.       }
39.     }
40.     fs.close(dest.fd);
41.     return dest.path;
42.   }

43.   async copyUrlPicToDir(picUrl: string, newFileName: string): Promise<string> {
44.     let uri = '';
45.     let httpRequest = http.createHttp();
46.     let data: http.HttpResponse = await (httpRequest.request(picUrl) as Promise<http.HttpResponse>);
47.     if (data?.responseCode == http.ResponseCode.OK) {
48.       let dstPath = this.context.filesDir + "/" + newFileName;
49.       let dest: fs.File = fs.openSync(dstPath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
50.       let writeLen: number = fs.writeSync(dest.fd, data.result as ArrayBuffer);
51.       uri = dest.path;
52.     }
53.     return uri;
54.   }

55.   @Builder
56.   MenuBuilder() {
57.     Menu() {
58.       MenuItem({
59.         content: "Scan QR Code",
60.       })
61.         .width(200)
62.         .height(50)
63.         .onClick(async () => {
64.           try {
65.             let uri = '';
66.             if (this.imgUrl?.includes('rawfile')) {
67.               let rawFileName: string = this.imgUrl.substring(this.imgUrl.lastIndexOf('/') + 1);
68.               uri = this.copyLocalPicToDir(rawFileName, 'copyFile.png');
69.             } else if (this.imgUrl?.includes('http') || this.imgUrl?.includes('https')) {
70.               uri = await this.copyUrlPicToDir(this.imgUrl, `onlinePic${systemDateTime.getTime()}.png`);
71.             }
72.             let options: scanBarcode.ScanOptions =
73.               { scanTypes: [scanCore.ScanType.ALL], enableMultiMode: true, enableAlbum: true }
74.             let inputImage: detectBarcode.InputImage = { uri: uri };
75.             try {
76.               // 调用图片识码接口
77.               detectBarcode.decode(inputImage, options,
78.                 (error: BusinessError, result: Array<scanBarcode.ScanResult>) => {
79.                   if (error && error.code) {
80.                     console.error(`create asset failed with error: ${error.code}, ${error.message}`);
81.                     return;
82.                   }
83.                   this.decodeResult = JSON.stringify(result);
84.                 });
85.             } catch (err) {
86.               console.error(`Failed to detect Barcode. Code: ${err.code}, ${err.message}`);
87.             }
88.           } catch (err) {
89.             console.error(`create asset failed with error: ${err.code}, ${err.message}`);
90.           }
91.         })
92.     }
93.   }

94.   build() {
95.     Column() {
96.       Web({ src: $rawfile("index.html"), controller: this.controller })
97.         .onContextMenuShow((event) => {
98.           if (event) {
99.             let hitValue = this.controller.getLastHitTest();
100.             this.imgUrl = hitValue.extra;
101.           }
102.           this.showMenu = true;
103.           return true;
104.         })
105.         .bindContextMenu(this.MenuBuilder, ResponseType.LongPress)
106.         .fileAccess(true)
107.         .javaScriptAccess(true)
108.         .domStorageAccess(true)
109.         .height('40%')
110.       Text('Decode result is ' + this.decodeResult)
111.         .fontSize(20)
112.         .height('10%')
113.     }
114.   }
115. }

116. <!--index.html-->
117. <!DOCTYPE html>
118. <html>
119. <head>
120.     <title>test QR code</title>
121. </head>
122. <body>
123. <h1>Long press and click to scan the QR code</h1>
124. <!--img.png为二维码图片-->
125. <img src="img.png" >
126. </body>
127. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.06270991606947428599641497908057:50001231000000:2800:97D8807984201C3212A665587CF9F7A5A11AF6B44C1A4C37BB47527FBF41FB8B.gif)

## 常见问题

### 如何禁用长按选择时弹出菜单

可通过[editMenuOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#editmenuoptions12)接口将系统默认菜单全部过滤，此时无菜单项，则不会显示菜单。

1. // xxx.ets
2. import { webview } from '@kit.ArkWeb';

3. @Entry
4. @Component
5. struct WebComponent {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   onCreateMenu(menuItems: Array<TextMenuItem>): Array<TextMenuItem> {
8.     let items = menuItems.filter((menuItem) => {
9.       // 过滤用户需要的系统按键
10.       return false;
11.     });
12.     return items;
13.   }

14.   onMenuItemClick(menuItem: TextMenuItem, textRange: TextRange): boolean {
15.     return false; // 返回默认值false
16.   }

17.   @State EditMenuOptions: EditMenuOptions = { onCreateMenu: this.onCreateMenu, onMenuItemClick: this.onMenuItemClick }

18.   build() {
19.     Column() {
20.       Web({ src: $rawfile("index.html"), controller: this.controller })
21.         .editMenuOptions(this.EditMenuOptions)
22.     }
23.   }
24. }

25. <!--index.html-->
26. <!DOCTYPE html>
27. <html>
28.   <head>
29.       <title>测试网页</title>
30.   </head>
31.   <body>
32.     <h1>editMenuOptions Demo</h1>
33.     <span>edit menu options</span>
34.   </body>
35. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.19330739680792383411363668468450:50001231000000:2800:2DA5BE11178E1B6384FC9FFE78DAC381DB88BD8FC74656B3CC0418D7C01C52FB.gif)

### 出现选区时手柄菜单不显示

可排查是否通过JS的[selection-api](https://www.w3.org/TR/selection-api/)对选区进行了操作，目前通过这种方式改变选区会导致手柄菜单不显示。

### 如何修改文本选中菜单的样式

从API version 21开始，应用可通过[bindSelectionMenu](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#bindselectionmenu13)接口，实现自定义文本菜单。

**示例代码**

1. import { webview } from '@kit.ArkWeb';
2. import { BusinessError } from '@kit.BasicServicesKit';

3. @Entry
4. @Component
5. struct WebComponent {
6.   controller: webview.WebviewController = new webview.WebviewController();

7.   clearSelection() {
8.     try {
9.       this.controller.runJavaScript(
10.         'clearSelection()',
11.         (error, result) => {
12.           if (error) {
13.             console.error(`run clearSelection JavaScript error, ErrorCode: ${(error as BusinessError).code},  Message: $  {(error as BusinessError).message}`);
14.             return;
15.           }
16.           if (result) {
17.             console.info(`The clearSelection() return value is: ${result}`);
18.           }
19.         });
20.     } catch (error) {
21.       console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
22.     }
23.   }

24.   @Builder
25.   TextMenuBuilder() {
26.     Menu() {
27.       MenuItem({ content: 'Copy', })
28.         .onClick(() => {
29.           try {
30.             this.controller.runJavaScript(
31.               'copySelectedText()',
32.               (error, result) => {
33.                 if (error) {
34.                   console.error(`run copySelectedText JavaScript error, ErrorCode: ${(error as BusinessError).code},    Message: ${(error as BusinessError).message}`);
35.                   return;
36.                 }
37.                 if (result) {
38.                   console.info(`The copySelectedText() return value is: ${result}`);
39.                 }
40.               });
41.           } catch (error) {
42.             console.error(`ErrorCode: ${(error as BusinessError).code},  Message: ${(error as BusinessError).message}`);
43.           }
44.           this.clearSelection()
45.         }).backgroundColor(Color.Pink)
46.     }
47.   }
48.   build() {
49.     Column() {
50.       Web({ src: $rawfile('bindSelectionMenuText.html'), controller: this.controller })
51.         .javaScriptAccess(true)
52.         .fileAccess(true)
53.         .onlineImageAccess(true)
54.         .imageAccess(true)
55.         .domStorageAccess(true)
56.         .zoomAccess(true)
57.         .bindSelectionMenu(WebElementType.TEXT, this.TextMenuBuilder, WebResponseType.LONG_PRESS,
58.           {
59.             onAppear: () => {},
60.             onDisappear: () => {},
61.             menuType: MenuType.SELECTION_MENU,
62.           })
63.     }
64.   }
65.   onBackPress(): boolean | void {
66.     if (this.controller.accessStep(-1)) {
67.       this.controller.backward();
68.       return true;
69.     } else {
70.       return false;
71.     }
72.   }
73. }

74. <!--bindSelectionMenuText.html-->
75. <!DOCTYPE html>
76. <html lang="zh-CN">
77. <head>
78.     <meta charset="UTF-8">
79.     <meta name="viewport" content="width=device-width, initial-scale=1.0">
80.     <title>自定义文本菜单</title>
81.     <style>
82.         .container {
83.             background-color: white;
84.             padding: 30px;
85.             margin: 20px 0;
86.         }

87.         .context {
88.             line-height: 1.8;
89.             font-size: 18px;
90.         }

91.         .context span {
92.             border-radius: 8px;
93.             background-color: #f8f9fa;
94.         }
95.     </style>
96. </head>
97. <body>
98. <div class="container">
99.     <div class="context">
100.         <span>在这个数字时代，文本复制功能变得日益重要。无论是引用名言、保存重要信息，还是分享有趣的内容，复制文本都是我们日常操作的  一部分。</span>
101.     </div>
102. </div>

103. <script>
104.   function copySelectedText() {
105.       const selectedText = window.getSelection().toString();
106.       if (selectedText.length > 0) {
107.           // 使用Clipboard API复制文本
108.           navigator.clipboard.writeText(selectedText)
109.               .then(() => {
110.                   showNotification();
111.               })
112.               .catch(err => {
113.                   console.error('copy failed:', err);
114.               });
115.       }
116.   }
117.   function clearSelection() {
118.     if (window.getSelection) {
119.       window.getSelection().removeAllRanges();
120.     }
121.   }
122. </script>
123. </body>
124. </html>

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163848.70221801701384901506701052920143:50001231000000:2800:704F509ECFEBC24550C0F3C204FCA88122F73B934B99E2B26EA35EEAD25F3F21.gif)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-safe-area-insets "网页中安全区域计算和避让适配")
# 同层渲染

更新时间: 2025-12-16 16:38

在系统中，应用可以使用Web组件加载Web网页。当非系统框架的UI组件功能或性能不如系统组件时，可使用同层渲染技术，通过ArkUI组件渲染这些组件（简称为同层组件）。

## 使用场景

### Web网页

小程序的地图组件，可以使用ArkUI的XComponent组件渲染来提升性能。小程序的输入框组件，可以使用ArkUI的TextInput组件渲染，达到与系统应用一致的输入体验。

- 在网页侧，应用开发者可将<embed>、<object>的网页UI组件（简称为同层标签），按一定规则进行同层渲染，详细规格见同层渲染规格小节。
    
- 在应用侧，应用开发者可以通过Web组件的同层渲染事件上报接口，感知到H5同层标签的生命周期以及输入事件，进行同层渲染组件的相应业务逻辑处理。
    
- 在应用侧，应用开发者可以使用ArkUI的NodeContainer等接口，构建H5同层标签对应的同层渲染组件。可支持同层渲染的ArkUI常用组件包括：[TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput), [XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent), [Canvas](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-canvas-canvas), [Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video), [Web](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)。具体规格可参见[同层渲染规格小节](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-same-layer#%E8%A7%84%E6%A0%BC%E7%BA%A6%E6%9D%9F)。
    

### 三方UI框架

Flutter提供了PlatformView与Texture抽象组件，这些组件可使用系统组件渲染，用于支持Flutter组件功能不足的部分。Weex2.0框架的Camera、Video和Canvas组件可以使用系统组件渲染，以增强功能和性能。

- 在三方框架页面侧，由于Flutter、Weex等三方框架不在操作系统范围内，本文不列举可被同层渲染的三方框架UI组件的范围与使用方式。
    
- 在应用侧，应用开发者可以使用ArkUI的NodeContainer等接口，构建三方框架同层标签对应的同层渲染组件。可支持同层渲染的ArkUI常用组件包括：[TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput), [XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent), [Canvas](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-canvas-canvas), [Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video), [Web](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)。具体规格可参见[同层渲染规格](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-same-layer#%E8%A7%84%E6%A0%BC%E7%BA%A6%E6%9D%9F)。
    

## 整体架构

ArkWeb同层渲染特性主要提供两种能力：同层标签生命周期和事件命中转发处理。

同层标签生命周期主要关联前端标签（<embed>/<object>），同时命中到同层标签的事件会被上报到开发者侧，由开发者分发到对应组件树。整体框架如下图所示：

**图1** 同层渲染整体架构

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.39410890836484253361083841709687:50001231000000:2800:6C89848D97E0DC98FDAEED734576663B8B0268882EE5205B6F2205A0F127BB09.png)

## 规格约束

### 可被同层渲染的ArkUI组件

以下规格对Web网页和三方框架场景均生效。

**支持的组件范围:**

- 基础组件：[AlphabetIndexer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-alphabet-indexer), [Blank](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-blank), [Button](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-button), [CalendarPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-calendarpicker), [Checkbox](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-checkbox), [CheckboxGroup](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-checkboxgroup), [ContainerSpan](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-containerspan), [DataPanel](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-datapanel), [DatePicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-datepicker), [Divider](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-divider), [Gauge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-gauge), [Hyperlink](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-hyperlink), [Image](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-image), [ImageAnimator](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-imageanimator), [ImageSpan](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-imagespan), [LoadingProgress](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-loadingprogress), [Marquee](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-marquee), [PatternLock](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-patternlock), [Progress](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-progress), [QRCode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-qrcode), [Radio](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-radio), [Rating](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-rating), [Refresh](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-refresh), [ScrollBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-scroll), [Search](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-search), [Span](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-span), [Select](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-select), [Slider](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-slider), [Text](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-text), [TextArea](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textarea), [TextClock](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textclock), [TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput), [TextPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textpicker), [TextTimer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-texttimer), [TimePicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-timepicker), [Toggle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-toggle)
    
- 容器类组件：[Badge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-badge), [Column](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-column), [ColumnSplit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-columnsplit), [Counter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-counter), [Flex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-flex), [GridCol](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-gridcol), [GridRow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-gridrow), [Grid](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-grid), [GridItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-griditem)，[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-list), [ListItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-listitem), [ListItemGroup](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-listitemgroup), [RelativeContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-relativecontainer), [Row](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-row), [RowSplit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-rowsplit), [Scroll](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-scroll), [Stack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-stack), [Swiper](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-swiper), [Tabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabs), [TabContent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabcontent), [NodeContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-nodecontainer), [SideBarContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-sidebarcontainer), [Stepper](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-stepper), [StepperItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-stepperitem), [WaterFlow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-waterflow), [FlowItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-flowitem)
    
- 自绘制类组件：[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent), [Canvas](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-canvas-canvas), [Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video), [Web](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)
    
- 命令式自定义绘制节点：[BuilderNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-buildernode), [ComponentContent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-componentcontent), [ContentSlot](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-contentslot), [FrameNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-framenode), [Graphics](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-graphics), [NodeController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-nodecontroller), [RenderNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-rendernode), [XComponentNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-xcomponentnode), [AttributeUpdater](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-attributeupdater), [CAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-arkui-nativemodule)（支持同层渲染的组件范围同ArkTS）
    

**支持的组件通用属性与事件:**

- 不支持的通用属性：[分布式迁移标识](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-restoreid)，[特效绘制合并](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-use-effect)。
    
- 其他未明确标注不支持的属性与事件及组件能力，均默认支持。
    

### Web网页的同层渲染标签

此规格仅针对Web网页，不适用于三方框架场景。

如果应用需要在Web组件加载的网页中使用同层渲染，需要按照以下规格将网页中的<embed>、<object>标签指定为同层渲染组件。

**支持的H5标签：**

- 支持<embed>标签：在开启同层渲染后，仅支持type类型为native前缀的标签识别为同层组件，不支持自定义属性。
    
- 支持<object>标签：在开启同层渲染后，支持将非标准MIME type的object标签识别为同层组件，支持通过param/value的自定义属性解析。
    
- 不支持W3C规范标准标签（如<input>、<video>）定义为同层标签。
    
- 不支持同时配置<object>标签和<embed>标签作为同层标签。
    
- 标签类型只支持英文字符，不区分大小写。
    

**同层标签支持的css属性：**

display，position，z-index，visibility，opacity, background-color，background-image，width，height，padding，padding-left，padding-top，padding-right，padding-bottom，margin，margin-left，margin-top，margin-right，margin-bottom，border-width，border-style，border-color，border-left-width，border-left-style，border-left-color，border-top-width，border-top-style，border-top-color，border-right-width，border-right-style，border-right-color，border-bottom-width，border-bottom-style，border-bottom-color，border-left，border-right，border-top，border-bottom，border，border-top-left-radius，border-top-right-radius，border-bottom-left-radius，border-bottom-right-radius，border-radius，transition，transform（仅支持translate/scale，scale对应参数只支持大于等于0的值）

除上面支持的css属性范围，其他的css属性均不保证符合预期，比如transform属性中的rotate，skew等。

**同层标签的生命周期管理：**

当同层标签生命周期变化时触发[onNativeEmbedLifecycleChange()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedlifecyclechange11)回调。

- 支持创建、销毁、位置宽高变化。
    
- 支持同层组件所在Web页面进入前进后退缓存。
    

**同层标签的输入事件分发处理：**

- 支持触摸事件TouchEvent的DOWN/UP/MOVE/CANCEL。支持[配置触摸事件消费结果](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedgestureevent11)，默认为应用侧消费。
    
- 不支持同层标签所在的应用页面缩放和[initialScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#initialscale9)、[zoom](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#zoom)、[zoomIn](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#zoomin)、[zoomOut](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#zoomout)等缩放接口。
    
- 暂不支持鼠标、键盘、触摸板事件上报。
    
- 支持默认将鼠标和触摸板左键事件（MousePress/MouseRelease/MouseMOVE）转换为触摸事件（TouchDOWN/TouchUP/TouchMOVE）上报。
    

**同层标签的可见状态变化：**

当同层标签可见状态变化时触发[onNativeEmbedVisibilityChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedvisibilitychange12)回调。

- 支持同层标签相对于视口的可见状态上报。
    
- 默认不支持由于同层标签CSS样式或尺寸变化导致的可见状态变化上报，具体规格参考[onNativeEmbedVisibilityChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedvisibilitychange12)。
    

**同层渲染<object>标签内嵌param元素状态变化：**

当同层渲染<object>内嵌标签param元素变化时触发[onNativeEmbedObjectParamChange()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedobjectparamchange21)回调。

- 支持上报param元素的增加、修改、删除三种状态变化。
    
- 接口每次最多上报500个param元素变化信息，超出部分将分多次上报。
    
- 详细上报信息参考[NativeEmbedParamDataInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-i#nativeembedparamdatainfo21)。
    

**约束限制：**

- Web页面内同层标签数量应控制在5个以内。超过5个，渲染性能将会下降。
    
- 受GPU限制，同层标签最大高度不超过8000px，最大纹理大小为8000px。
    
- 开启同层渲染后，Web组件打开的所有Web页面将不支持同步渲染模式[RenderMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#rendermode12)。
    
- Video组件：在非全屏Video变为全屏时，Video组件变为非纹理导出模式，视频播放状态保持延续；恢复为非全屏时，变为纹理导出模式，视频播放状态保持延续。
    
- Web组件：仅支持一层同层渲染嵌套，不支持多层同层渲染嵌套。输入事件只支持滑动、点击、长按，不支持拖拽、旋转、缩放。
    
- 涉及界面交互的ArkUI组件（如TextInput等）：建议在页面布局中使用Stack包裹同层组件容器与BuilderNode，并使两者位置一致，NodeContainer要与<embed>/<object>标签对齐，以保障组件正常交互。如两者位置不一致，可能出现的问题有：TextInput/TextArea等附属的文本选择框位置错位（如下图）、LoadingProgress/Marquee等组件的动画启停与组件可见状态不匹配。
    
    **图2** 未使用Stack包裹，TextInput的位置错位
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.83659815536941758218255870630249:50001231000000:2800:2DF8EFA2ECC43F8D29A1B340A2DDD7F0D18E4BA0959C8B74C8A2E140E207DFDC.png)
    
    **图3** 使用Stack包裹，TextInput的位置正常
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.99416238214956841185269338927042:50001231000000:2800:0CC8EBF4568814B454ECF1C19B0740351F24C92088FFE630FAA656FB2C2D20C8.png)
    

## Web页面中同层渲染输入框

在Web页面中，可以使用ArkUI系统的TextInput组件进行同层渲染。此处利用同层渲染展示三个输入框，渲染效果图如下：

**图4** 同层渲染输入框

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.64649427145049818214449563250542:50001231000000:2800:14959B3CEB3EAE584B8D691B4A2F57E4621BFBF925419AE2FBFC012B465AFAFE.png)

1. 在Web页面中标记需要同层渲染的HTML标签。
    
    同层渲染支持<embed>/<object>两种标签。type类型可任意指定，两个字符串参数均不区分大小写，ArkWeb内核将会统一转换为小写。其中，tag字符串使用全字符串匹配，type使用字符串前缀匹配。
    
    若开发者不使用该接口或该接口接收的为非法字符串（空字符串）时，ArkWeb内核将使用默认设置，即"embed" + "native/"前缀模式。若指定类型与w3c定义的<embed>或<object>标准类型重合，如registerNativeEmbedRule("object", "application/pdf")，ArkWeb将遵循w3c标准行为，不会将其识别为同层标签。
    
    - 采用<embed>标签。
        
        1. <!--HAP's src/main/resources/rawfile/text.html-->
        2. <!DOCTYPE html>
        3. <html>
        4. <head>
        5.     <title>同层渲染html</title>
        6.     <meta name="viewport">
        7. </head>
        
        8. <body style="background:white">
        
        9. <embed id = "input1" type="native/view" style="width: 100%; height: 100px; margin: 30px; margin-top: 600px"/>
        
        10. <embed id = "input2" type="native/view2" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"/>
        
        11. <embed id = "input3" type="native/view3" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"/>
        
        12. </body>
        13. </html>
        
    - 采用<object>标签。
        
        需要使用registerNativeEmbedRule注册object标签。
        
        1. // ...
        2. Web({src: $rawfile("text.html"), controller: this.browserTabController})
        3.   // 注册同层标签为"object"，类型为"test"前缀。
        4.   .registerNativeEmbedRule("object", "test")
        5.   // ...
        
        与registerNativeEmbedRule相对应的前端页面代码，类型可使用"test"及以"test"为前缀的字串。
        
        6. <!--HAP's src/main/resources/rawfile/text.html-->
        7. <!DOCTYPE html>
        8. <html>
        9. <head>
        10.     <title>同层渲染html</title>
        11.     <meta name="viewport">
        12. </head>
        
        13. <body style="background:white">
        
        14. <object id = "input1" type="test/input" style="width: 100%; height: 100px; margin: 30px; margin-top: 600px"></object>
        
        15. <object id = "input2" type="test/input" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"></object>
        
        16. <object id = "input3" type="test/input" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"></object>
        
        17. </body>
        18. </html>
        
2. 在应用侧开启同层渲染功能。
    
    同层渲染功能默认不开启，如果要使用同层渲染的功能，可通过[enableNativeEmbedMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#enablenativeembedmode11)来开启。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller: webview.WebviewController = new webview.WebviewController();
    
    7.   build() {
    8.     Column() {
    9.       Web({ src: 'www.example.com', controller: this.controller })
    10.         // 配置同层渲染开关开启。
    11.         .enableNativeEmbedMode(true)
    12.     }
    13.   }
    14. }
    
3. 创建自定义组件。
    
    同层渲染功能开启后，展示在对应区域的系统组件。
    
    1. @Component
    2. struct TextInputComponent {
    3.   @Prop params: Params
    4.   @State bkColor: Color = Color.White
    
    5.   build() {
    6.     Column() {
    7.       TextInput({text: '', placeholder: 'please input your word...'})
    8.         .placeholderColor(Color.Gray)
    9.         .id(this.params?.elementId)
    10.         .placeholderFont({size: 13, weight: 400})
    11.         .caretColor(Color.Gray)
    12.         .width(this.params?.width)
    13.         .height(this.params?.height)
    14.         .fontSize(14)
    15.         .fontColor(Color.Black)
    16.     }
    17.     //自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    18.     .width(this.params.width)
    19.     .height(this.params.height)
    20.   }
    21. }
    
    22. @Builder
    23. function TextInputBuilder(params:Params) {
    24.   TextInputComponent({params: params})
    25.     .width(params.width)
    26.     .height(params.height)
    27.     .backgroundColor(Color.White)
    28. }
    
4. 创建节点控制器。
    
    用于控制和反馈对应NodeContainer上的节点行为。
    
    1. class MyNodeController extends NodeController {
    2.   private rootNode: BuilderNode<[Params]> | undefined | null;
    3.   private embedId_: string = "";
    4.   private surfaceId_: string = "";
    5.   private renderType_: NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
    6.   private width_: number = 0;
    7.   private height_: number = 0;
    8.   private type_: string = "";
    9.   private isDestroy_: boolean = false;
    
    10.   setRenderOption(params: NodeControllerParams) {
    11.     this.surfaceId_ = params.surfaceId;
    12.     this.renderType_ = params.renderType;
    13.     this.embedId_ = params.embedId;
    14.     this.width_ = params.width;
    15.     this.height_ = params.height;
    16.     this.type_ = params.type;
    17.   }
    
    18.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
    19.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
    20.   makeNode(uiContext: UIContext): FrameNode | null {
    21.     if (this.isDestroy_) { // rootNode为null。
    22.       return null;
    23.     }
    24.     if (!this.rootNode) {// rootNode 为undefined时。
    25.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_ });
    26.       if(this.rootNode) {
    27.         this.rootNode.build(wrapBuilder(TextInputBuilder), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
    28.         return this.rootNode.getFrameNode();
    29.       }else{
    30.         return null;
    31.       }
    32.     }
    33.     // 返回FrameNode节点。
    34.     return this.rootNode.getFrameNode();
    35.   }
    
    36.   updateNode(arg: Object): void {
    37.     this.rootNode?.update(arg);
    38.   }
    
    39.   getEmbedId(): string {
    40.     return this.embedId_;
    41.   }
    
    42.   setDestroy(isDestroy: boolean): void {
    43.     this.isDestroy_ = isDestroy;
    44.     if (this.isDestroy_) {
    45.       this.rootNode = null;
    46.     }
    47.   }
    
    48.   postEvent(event: TouchEvent | undefined): boolean {
    49.     return this.rootNode?.postTouchEvent(event) as boolean
    50.   }
    51. }
    
5. 监听同层渲染的生命周期变化。
    
    开启该功能后，当网页中存在同层渲染支持的标签时，ArkWeb内核会触发由[onNativeEmbedLifecycleChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedlifecyclechange11)注册的回调函数。
    
    开发者则需要调用[onNativeEmbedLifecycleChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedlifecyclechange11)来监听同层渲染标签的生命周期变化。
    
    1. build() {
    2.   Row() {
    3.     Column() {
    4.       Stack() {
    5.         ForEach(this.componentIdArr, (componentId: string) => {
    6.           NodeContainer(this.nodeControllerMap.get(componentId))
    7.             .position(this.positionMap.get(componentId))
    8.             .width(this.widthMap.get(componentId))
    9.             .height(this.heightMap.get(componentId))
    10.         }, (embedId: string) => embedId)
    11.         // Web组件加载本地text.html页面。
    12.         Web({src: $rawfile("text.html"), controller: this.browserTabController})
    13.           // 配置同层渲染开关开启。
    14.           .enableNativeEmbedMode(true)
    15.             // 注册同层标签为<object>，类型为"test"前缀。
    16.           .registerNativeEmbedRule("object", "test")
    17.             // 获取<embed>标签的生命周期变化数据。
    18.           .onNativeEmbedLifecycleChange((embed) => {
    19.             console.info("NativeEmbed surfaceId" + embed.surfaceId);
    20.             // 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
    21.             const componentId = embed.info?.id?.toString() as string
    22.             if (embed.status == NativeEmbedStatus.CREATE) {
    23.               console.info("NativeEmbed create" + JSON.stringify(embed.info));
    24.               // 创建节点控制器、设置参数。
    25.               let nodeController = new MyNodeController()
    26.               // embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
    27.               nodeController.setRenderOption({surfaceId : embed.surfaceId as string,
    28.                 type : embed.info?.type as string,
    29.                 renderType : NodeRenderType.RENDER_TYPE_TEXTURE,
    30.                 embedId : embed.embedId as string,
    31.                 width : this.uiContext.px2vp(embed.info?.width),
    32.                 height : this.uiContext.px2vp(embed.info?.height)})
    33.               this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    34.               nodeController.setDestroy(false);
    35.               //根据web传入的embed的id属性作为key，将nodeController存入Map。
    36.               this.nodeControllerMap.set(componentId, nodeController);
    37.               this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    38.               this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    39.               this.positionMap.set(componentId, this.edges);
    40.               // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器,需要将push动作放在set之后。
    41.               this.componentIdArr.push(componentId)
    42.             } else if (embed.status == NativeEmbedStatus.UPDATE) {
    43.               let nodeController = this.nodeControllerMap.get(componentId);
    44.               console.info("NativeEmbed update" + JSON.stringify(embed));
    45.               this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    46.               this.positionMap.set(componentId, this.edges);
    47.               this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    48.               this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    49.               nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
    50.             } else if (embed.status == NativeEmbedStatus.DESTROY) {
    51.               console.info("NativeEmbed destroy" + JSON.stringify(embed));
    52.               let nodeController = this.nodeControllerMap.get(componentId);
    53.               nodeController?.setDestroy(true);
    54.               this.nodeControllerMap.delete(componentId);
    55.               this.positionMap.delete(componentId);
    56.               this.widthMap.delete(componentId);
    57.               this.heightMap.delete(componentId);
    58.               this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
    59.             } else {
    60.               console.info("NativeEmbed status" + embed.status);
    61.             }
    62.           })
    63.       }.height("80%")
    64.     }
    65.   }
    66. }
    
6. 同层渲染手势事件。
    
    开启该功能后，每当在同层渲染的区域进行触摸操作时，ArkWeb内核会触发[onNativeEmbedGestureEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedgestureevent11)注册的回调函数。
    
    开发者则需要调用[onNativeEmbedGestureEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedgestureevent11)来监听同层渲染区域的手势事件。
    
    1. build() {
    2.   Row() {
    3.     Column() {
    4.       Stack() {
    5.         ForEach(this.componentIdArr, (componentId: string) => {
    6.           NodeContainer(this.nodeControllerMap.get(componentId))
    7.             .position(this.positionMap.get(componentId))
    8.             .width(this.widthMap.get(componentId))
    9.             .height(this.heightMap.get(componentId))
    10.         }, (embedId: string) => embedId)
    11.         // Web组件加载本地text.html页面。
    12.         Web({src: $rawfile("text.html"), controller: this.browserTabController})
    13.           // 配置同层渲染开关开启。
    14.           .enableNativeEmbedMode(true)
    15.             // 获取<embed>标签的生命周期变化数据。
    16.           .onNativeEmbedLifecycleChange((embed) => {
    17.             // 生命周期变化实现。
    18.           })
    19.           .onNativeEmbedGestureEvent((touch) => {
    20.             console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
    21.             this.componentIdArr.forEach((componentId: string) => {
    22.               let nodeController = this.nodeControllerMap.get(componentId);
    23.               // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    24.               if(nodeController?.getEmbedId() == touch.embedId) {
    25.                 let ret = nodeController?.postEvent(touch.touchEvent)
    26.                 if(ret) {
    27.                   console.info("onNativeEmbedGestureEvent success " + componentId);
    28.                 } else {
    29.                   console.info("onNativeEmbedGestureEvent fail " + componentId);
    30.                 }
    31.                 if(touch.result) {
    32.                   // 通知Web组件手势事件消费结果。
    33.                   touch.result.setGestureEventResult(ret);
    34.                 }
    35.               }
    36.             })
    37.           })
    38.       }
    39.     }
    40.   }
    41. }
    
7. 同层渲染鼠标事件
    
    开启该功能后，在同层渲染的区域进行下述动作时，ArkWeb内核会触发[onNativeEmbedMouseEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedmouseevent20)注册的回调函数：
    
    - 使用鼠标左键、中键、右键进行点击或长按。
    - 使用触摸板进行对应鼠标左键、中键、右键点击长按的操作。
    
    开发者则需要调用[onNativeEmbedMouseEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedmouseevent20)来监听同层渲染区域的鼠标事件。
    
    1. build() {
    2.   Row() {
    3.     Column() {
    4.       Stack() {
    5.         ForEach(this.componentIdArr, (componentId: string) => {
    6.           NodeContainer(this.nodeControllerMap.get(componentId))
    7.             .position(this.positionMap.get(componentId))
    8.             .width(this.widthMap.get(componentId))
    9.             .height(this.heightMap.get(componentId))
    10.         }, (embedId: string) => embedId)
    11.         // Web组件加载本地text.html页面。
    12.         Web({src: $rawfile("text.html"), controller: this.browserTabController})
    13.           // 配置同层渲染开关开启。
    14.           .enableNativeEmbedMode(true)
    15.             // 获取<embed>标签的生命周期变化数据。
    16.           .onNativeEmbedLifecycleChange((embed) => {
    17.             // 生命周期变化实现。
    18.           })
    19.           .onNativeEmbedGestureEvent((touch) => {
    20.             // 处理同层渲染手势事件。
    21.           })
    22.           .onNativeEmbedMouseEvent((mouse) => {
    23.             console.info("NativeEmbed onNativeEmbedMouseEvent" + JSON.stringify(mouse.mouseEvent));
    24.             this.componentIdArr.forEach((componentId: string) => {
    25.               let nodeController = this.nodeControllerMap.get(componentId);
    26.               // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    27.               if(nodeController?.getEmbedId() == mouse.embedId) {
    28.                 let ret = nodeController?.postInputEvent(mouse.mouseEvent)
    29.                 if(ret) {
    30.                   console.info("onNativeEmbedMouseEvent success " + componentId);
    31.                 } else {
    32.                   console.info("onNativeEmbedMouseEvent fail " + componentId);
    33.                 }
    34.                 if(mouse.result) {
    35.                   // 通知Web组件鼠标事件消费结果。
    36.                   mouse.result.setMouseEventResult(ret);
    37.                 }
    38.               }
    39.             })
    40.           })
    41.       }
    42.     }
    43.   }
    44. }
    

**完整示例：**

使用前请在module.json5中添加网络权限，添加方法请参考[在配置文件中声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。

1. "requestPermissions":[
2.     {
3.       "name" : "ohos.permission.INTERNET"
4.     }
5.   ]

应用侧代码。

1. // 创建NodeController
2. import { webview } from '@kit.ArkWeb';
3. import { UIContext } from '@kit.ArkUI';
4. import { NodeController, BuilderNode, NodeRenderType, FrameNode } from '@kit.ArkUI';

5. @Observed
6. declare class Params{
7.   elementId: string
8.   textOne: string
9.   textTwo: string
10.   width: number
11.   height: number
12. }

13. declare class NodeControllerParams {
14.   surfaceId: string
15.   type: string
16.   renderType: NodeRenderType
17.   embedId: string
18.   width: number
19.   height: number
20. }

21. // 用于控制和反馈对应的NodeContainer上的节点的行为，需要与NodeContainer一起使用。
22. class MyNodeController extends NodeController {
23.   private rootNode: BuilderNode<[Params]> | undefined | null;
24.   private embedId_: string = "";
25.   private surfaceId_: string = "";
26.   private renderType_: NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
27.   private width_: number = 0;
28.   private height_: number = 0;
29.   private type_: string = "";
30.   private isDestroy_: boolean = false;

31.   setRenderOption(params: NodeControllerParams) {
32.     this.surfaceId_ = params.surfaceId;
33.     this.renderType_ = params.renderType;
34.     this.embedId_ = params.embedId;
35.     this.width_ = params.width;
36.     this.height_ = params.height;
37.     this.type_ = params.type;
38.   }

39.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
40.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
41.   makeNode(uiContext: UIContext): FrameNode | null {
42.     if (this.isDestroy_) { // rootNode为null。
43.       return null;
44.     }
45.     if (!this.rootNode) {// rootNode 为undefined时。
46.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_ });
47.       if(this.rootNode) {
48.         this.rootNode.build(wrapBuilder(TextInputBuilder), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
49.         return this.rootNode.getFrameNode();
50.       }else{
51.         return null;
52.       }
53.     }
54.     // 返回FrameNode节点。
55.     return this.rootNode.getFrameNode();
56.   }

57.   updateNode(arg: Object): void {
58.     this.rootNode?.update(arg);
59.   }

60.   getEmbedId(): string {
61.     return this.embedId_;
62.   }

63.   setDestroy(isDestroy: boolean): void {
64.     this.isDestroy_ = isDestroy;
65.     if (this.isDestroy_) {
66.       this.rootNode = null;
67.     }
68.   }

69.   postEvent(event: TouchEvent | undefined): boolean {
70.     return this.rootNode?.postTouchEvent(event) as boolean
71.   }

72.   postInputEvent(event: MouseEvent | undefined): boolean {
73.     return this.rootNode?.postInputEvent(event) as boolean
74.   }
75. }

76. @Component
77. struct TextInputComponent {
78.   @Prop params: Params
79.   @State bkColor: Color = Color.White

80.   build() {
81.     Column() {
82.       TextInput({text: '', placeholder: 'please input your word...'})
83.         .placeholderColor(Color.Gray)
84.         .id(this.params?.elementId)
85.         .placeholderFont({size: 13, weight: 400})
86.         .caretColor(Color.Gray)
87.         .fontSize(14)
88.         .fontColor(Color.Black)
89.     }
90.     //自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
91.     .width(this.params.width)
92.     .height(this.params.height)
93.   }
94. }

95. // @Builder中为动态组件的具体组件内容。
96. @Builder
97. function TextInputBuilder(params:Params) {
98.   TextInputComponent({params: params})
99.     .width(params.width)
100.     .height(params.height)
101.     .backgroundColor(Color.White)
102. }

103. @Entry
104. @Component
105. struct Page{
106.   browserTabController: WebviewController = new webview.WebviewController()
107.   private nodeControllerMap: Map<string, MyNodeController> = new Map();
108.   @State componentIdArr: Array<string> = [];
109.   @State widthMap: Map<string, number> = new Map();
110.   @State heightMap: Map<string, number> = new Map();
111.   @State positionMap: Map<string, Edges> = new Map();
112.   @State edges: Edges = {};
113.   uiContext: UIContext = this.getUIContext();

114.   build() {
115.     Row() {
116.       Column() {
117.         Stack() {
118.           ForEach(this.componentIdArr, (componentId: string) => {
119.             NodeContainer(this.nodeControllerMap.get(componentId))
120.               .position(this.positionMap.get(componentId))
121.               .width(this.widthMap.get(componentId))
122.               .height(this.heightMap.get(componentId))
123.           }, (embedId: string) => embedId)
124.           // Web组件加载本地text.html页面。
125.           Web({src: $rawfile("text.html"), controller: this.browserTabController})
126.             // 配置同层渲染开关开启。
127.             .enableNativeEmbedMode(true)
128.             // 获取<embed>标签的生命周期变化数据。
129.             .onNativeEmbedLifecycleChange((embed) => {
130.                console.info("NativeEmbed surfaceId" + embed.surfaceId);
131.                // 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
132.                const componentId = embed.info?.id?.toString() as string
133.                if (embed.status == NativeEmbedStatus.CREATE) {
134.                  console.info("NativeEmbed create" + JSON.stringify(embed.info));
135.                  // 创建节点控制器、设置参数。
136.                  let nodeController = new MyNodeController()
137.                  // embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
138.                  nodeController.setRenderOption({surfaceId : embed.surfaceId as string,
139.                    type : embed.info?.type as string,
140.                    renderType : NodeRenderType.RENDER_TYPE_TEXTURE,
141.                    embedId : embed.embedId as string,
142.                    width : this.uiContext.px2vp(embed.info?.width),
143.                    height : this.uiContext.px2vp(embed.info?.height)})
144.                  this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
145.                  nodeController.setDestroy(false);
146.                  //根据web传入的embed的id属性作为key，将nodeController存入Map。
147.                  this.nodeControllerMap.set(componentId, nodeController);
148.                  this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
149.                  this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
150.                  this.positionMap.set(componentId, this.edges);
151.                  // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器,需要将push动作放在set之后。
152.                  this.componentIdArr.push(componentId)
153.                } else if (embed.status == NativeEmbedStatus.UPDATE) {
154.                  let nodeController = this.nodeControllerMap.get(componentId);
155.                  console.info("NativeEmbed update" + JSON.stringify(embed));
156.                  this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
157.                  this.positionMap.set(componentId, this.edges);
158.                  this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
159.                  this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
160.                  nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
161.                } else if (embed.status == NativeEmbedStatus.DESTROY) {
162.                  console.info("NativeEmbed destroy" + JSON.stringify(embed));
163.                  let nodeController = this.nodeControllerMap.get(componentId);
164.                  nodeController?.setDestroy(true);
165.                  this.nodeControllerMap.delete(componentId);
166.                  this.positionMap.delete(componentId);
167.                  this.widthMap.delete(componentId);
168.                  this.heightMap.delete(componentId);
169.                  this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
170.                } else {
171.                  console.info("NativeEmbed status" + embed.status);
172.                }
173.              })// 获取同层渲染组件触摸事件信息。
174.             .onNativeEmbedGestureEvent((touch) => {
175.               console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
176.               this.componentIdArr.forEach((componentId: string) => {
177.                 let nodeController = this.nodeControllerMap.get(componentId);
178.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
179.                 if(nodeController?.getEmbedId() == touch.embedId) {
180.                   let ret = nodeController?.postEvent(touch.touchEvent)
181.                   if(ret) {
182.                     console.info("onNativeEmbedGestureEvent success " + componentId);
183.                   } else {
184.                     console.info("onNativeEmbedGestureEvent fail " + componentId);
185.                   }
186.                   if(touch.result) {
187.                     // 通知Web组件手势事件消费结果。
188.                     touch.result.setGestureEventResult(ret);
189.                   }
190.                 }
191.               })
192.             })
193.             .onNativeEmbedMouseEvent((mouse) => {
194.               console.info("NativeEmbed onNativeEmbedMouseEvent" + JSON.stringify(mouse.mouseEvent));
195.               this.componentIdArr.forEach((componentId: string) => {
196.                 let nodeController = this.nodeControllerMap.get(componentId);
197.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
198.                 if(nodeController?.getEmbedId() == mouse.embedId) {
199.                   let ret = nodeController?.postInputEvent(mouse.mouseEvent)
200.                   if(ret) {
201.                     console.info("onNativeEmbedMouseEvent success " + componentId);
202.                   } else {
203.                     console.info("onNativeEmbedMouseEvent fail " + componentId);
204.                   }
205.                   if(mouse.result) {
206.                     // 通知Web组件鼠标事件消费结果。
207.                     mouse.result.setMouseEventResult(ret);
208.                   }
209.                 }
210.               })
211.             })
212.         }
213.       }
214.     }
215.   }
216. }

## 绘制XComponent+AVPlayer和Button组件

- 应用侧代码组件使用示例。
    
    1. // HAP's src/main/ets/pages/Index.ets
    2. // 创建NodeController
    3. import { webview } from '@kit.ArkWeb';
    4. import { UIContext, NodeController, BuilderNode, NodeRenderType, FrameNode } from "@kit.ArkUI";
    5. import { AVPlayerDemo } from './PlayerDemo';
    
    6. @Observed
    7. declare class Params {
    8.   textOne : string
    9.   textTwo : string
    10.   width : number
    11.   height : number
    12. }
    
    13. declare class NodeControllerParams {
    14.   surfaceId : string
    15.   type : string
    16.   renderType : NodeRenderType
    17.   embedId : string
    18.   width : number
    19.   height : number
    20. }
    
    21. // 用于控制和反馈对应的NodeContainer上的节点的行为，需要与NodeContainer一起使用。
    22. class MyNodeController extends NodeController {
    23.   private rootNode: BuilderNode<[Params]> | undefined | null;
    24.   private embedId_ : string = "";
    25.   private surfaceId_ : string = "";
    26.   private renderType_ :NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
    27.   private width_ : number = 0;
    28.   private height_ : number = 0;
    29.   private type_ : string = "";
    30.   private isDestroy_ : boolean = false;
    
    31.   setRenderOption(params : NodeControllerParams) {
    32.     this.surfaceId_ = params.surfaceId;
    33.     this.renderType_ = params.renderType;
    34.     this.embedId_ = params.embedId;
    35.     this.width_ = params.width;
    36.     this.height_ = params.height;
    37.     this.type_ = params.type;
    38.   }
    39.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
    40.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
    41.   makeNode(uiContext: UIContext): FrameNode | null{
    42.     if (this.isDestroy_) { // rootNode为null。
    43.       return null;
    44.     }
    45.     if (!this.rootNode) { // rootNode 为undefined时。
    46.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_});
    47.       if (this.type_ === 'native/video') {
    48.         this.rootNode.build(wrapBuilder(VideoBuilder), {textOne: "myButton", width : this.width_, height : this.height_});
    49.       } else {
    50.         // other
    51.       }
    52.     }
    53.     // 返回FrameNode节点。
    54.     return this.rootNode.getFrameNode();
    55.   }
    
    56.   updateNode(arg: Object): void {
    57.     this.rootNode?.update(arg);
    58.   }
    59.   getEmbedId() : string {
    60.     return this.embedId_;
    61.   }
    
    62.   setDestroy(isDestroy : boolean) : void {
    63.     this.isDestroy_ = isDestroy;
    64.     if (this.isDestroy_) {
    65.       this.rootNode = null;
    66.     }
    67.   }
    
    68.   postEvent(event: TouchEvent | undefined) : boolean {
    69.     return this.rootNode?.postTouchEvent(event) as boolean
    70.   }
    
    71.   postInputEvent(event: MouseEvent | undefined): boolean {
    72.     return this.rootNode?.postInputEvent(event) as boolean
    73.   }
    74. }
    
    75. @Component
    76. struct VideoComponent {
    77.   @ObjectLink params: Params
    78.   @State bkColor: Color = Color.Red
    79.   mXComponentController: XComponentController = new XComponentController();
    80.   @State player_changed: boolean = false;
    81.   player?: AVPlayerDemo;
    
    82.   build() {
    83.     Column() {
    84.       Button(this.params.textOne)
    
    85.       XComponent({ id: 'video_player_id', type: XComponentType.SURFACE, controller: this.mXComponentController})
    86.         .border({width: 1, color: Color.Red})
    87.         .onLoad(() => {
    88.           this.player = new AVPlayerDemo();
    89.           this.player.setSurfaceID(this.mXComponentController.getXComponentSurfaceId());
    90.           this.player_changed = !this.player_changed;
    91.           this.player.avPlayerLiveDemo()
    92.         })
    93.         .width(300)
    94.         .height(200)
    95.     }
    96.     //自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    97.     .width(this.params.width)
    98.     .height(this.params.height)
    99.   }
    100. }
    101. // @Builder中为动态组件的具体组件内容。
    102. @Builder
    103. function VideoBuilder(params: Params) {
    104.   VideoComponent({ params: params })
    105.     .backgroundColor(Color.Gray)
    106. }
    
    107. @Entry
    108. @Component
    109. struct WebIndex {
    110.   browserTabController: WebviewController = new webview.WebviewController()
    111.   private nodeControllerMap: Map<string, MyNodeController> = new Map();
    112.   @State componentIdArr: Array<string> = [];
    113.   @State widthMap: Map<string, number> = new Map();
    114.   @State heightMap: Map<string, number> = new Map();
    115.   @State positionMap: Map<string, Edges> = new Map();
    116.   @State edges: Edges = {};
    117.   uiContext: UIContext = this.getUIContext();
    
    118.   aboutToAppear() {
    119.     // 配置web开启调试模式。
    120.     webview.WebviewController.setWebDebuggingAccess(true);
    121.   }
    
    122.   build(){
    123.     Row() {
    124.       Column() {
    125.         Stack() {
    126.           ForEach(this.componentIdArr, (componentId: string) => {
    127.             NodeContainer(this.nodeControllerMap.get(componentId))
    128.               .position(this.positionMap.get(componentId))
    129.               .width(this.widthMap.get(componentId))
    130.               .height(this.heightMap.get(componentId))
    131.           }, (embedId: string) => embedId)
    132.           // Web组件加载本地test.html页面。
    133.           Web({ src: $rawfile("test.html"), controller: this.browserTabController })
    134.             // 配置同层渲染开关开启。
    135.             .enableNativeEmbedMode(true)
    136.               // 获取<embed>标签的生命周期变化数据。
    137.             .onNativeEmbedLifecycleChange((embed) => {
    138.               console.info("NativeEmbed surfaceId" + embed.surfaceId);
    139.               // 1. 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
    140.               const componentId = embed.info?.id?.toString() as string
    141.               if (embed.status == NativeEmbedStatus.CREATE) {
    142.                 console.info("NativeEmbed create" + JSON.stringify(embed.info))
    143.                 // 创建节点控制器，设置参数。
    144.                 let nodeController = new MyNodeController()
    145.                 // 1. embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
    146.                 nodeController.setRenderOption({surfaceId : embed.surfaceId as string, type : embed.info?.type as string,
    147.                   renderType : NodeRenderType.RENDER_TYPE_TEXTURE, embedId : embed.embedId as string,
    148.                   width : this.uiContext.px2vp(embed.info?.width), height : this.uiContext.px2vp(embed.info?.height)})
    149.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    150.                 nodeController.setDestroy(false);
    151.                 // 根据web传入的embed的id属性作为key，将nodeController存入map。
    152.                 this.nodeControllerMap.set(componentId, nodeController)
    153.                 this.widthMap.set(componentId,  this.uiContext.px2vp(embed.info?.width));
    154.                 this.heightMap.set(componentId,  this.uiContext.px2vp(embed.info?.height));
    155.                 this.positionMap.set(componentId, this.edges);
    156.                 // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器，需要将push动作放在set之后。
    157.                 this.componentIdArr.push(componentId)
    158.               } else if (embed.status == NativeEmbedStatus.UPDATE) {
    159.                 let nodeController = this.nodeControllerMap.get(componentId)
    160.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    161.                 this.positionMap.set(componentId, this.edges);
    162.                 this.widthMap.set(componentId,  this.uiContext.px2vp(embed.info?.width));
    163.                 this.heightMap.set(componentId,  this.uiContext.px2vp(embed.info?.height));
    164.                 nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
    165.               } else if (embed.status == NativeEmbedStatus.DESTROY) {
    166.                 let nodeController = this.nodeControllerMap.get(componentId);
    167.                 nodeController?.setDestroy(true);
    168.                 this.nodeControllerMap.delete(componentId);
    169.                 this.positionMap.delete(componentId);
    170.                 this.widthMap.delete(componentId);
    171.                 this.heightMap.delete(componentId);
    172.                 this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
    173.               } else {
    174.                 console.info("NativeEmbed status" + embed.status);
    175.               }
    176.             })// 获取同层渲染组件触摸事件信息。
    177.             .onNativeEmbedGestureEvent((touch) => {
    178.               console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
    179.               this.componentIdArr.forEach((componentId: string) => {
    180.                 let nodeController = this.nodeControllerMap.get(componentId)
    181.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    182.                 if (nodeController?.getEmbedId() === touch.embedId) {
    183.                   let ret = nodeController?.postEvent(touch.touchEvent)
    184.                   if (ret) {
    185.                     console.info("onNativeEmbedGestureEvent success " + componentId)
    186.                   } else {
    187.                     console.info("onNativeEmbedGestureEvent fail " + componentId)
    188.                   }
    189.                   if (touch.result) {
    190.                     // 通知Web组件手势事件消费结果。
    191.                     touch.result.setGestureEventResult(ret);
    192.                   }
    193.                 }
    194.               })
    195.             })
    196.             .onNativeEmbedMouseEvent((mouse) => {
    197.               console.info("NativeEmbed onNativeEmbedMouseEvent" + JSON.stringify(mouse.mouseEvent));
    198.               this.componentIdArr.forEach((componentId: string) => {
    199.                 let nodeController = this.nodeControllerMap.get(componentId);
    200.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    201.                 if(nodeController?.getEmbedId() == mouse.embedId) {
    202.                   let ret = nodeController?.postInputEvent(mouse.mouseEvent)
    203.                   if(ret) {
    204.                     console.info("onNativeEmbedMouseEvent success " + componentId);
    205.                   } else {
    206.                     console.info("onNativeEmbedMouseEvent fail " + componentId);
    207.                   }
    208.                   if(mouse.result) {
    209.                     // 通知Web组件鼠标事件消费结果。
    210.                     mouse.result.setMouseEventResult(ret);
    211.                   }
    212.                 }
    213.               })
    214.             })
    215.         }
    216.       }
    217.     }
    218.   }
    219. }
    
- 应用侧代码示例，视频播放，使用时需替换为正确的视频链接地址。
    
    1. // HAP's src/main/ets/pages/PlayerDemo.ets
    2. import { media } from '@kit.MediaKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. export class AVPlayerDemo {
    5.   private count: number = 0;
    6.   private surfaceID: string = ''; // surfaceID用于播放画面显示，具体的值需要通过Xcomponent接口获取，相关文档链接见上面Xcomponent创建方法。
    7.   private isSeek: boolean = true; // 用于区分模式是否支持seek操作。
    
    8.   setSurfaceID(surface_id: string){
    9.     console.info('setSurfaceID : ' + surface_id);
    10.     this.surfaceID = surface_id;
    11.   }
    12.   // 注册avplayer回调函数。
    13.   setAVPlayerCallback(avPlayer: media.AVPlayer) {
    14.     // seek操作结果回调函数。
    15.     avPlayer.on('seekDone', (seekDoneTime: number) => {
    16.       console.info(`AVPlayer seek succeeded, seek time is ${seekDoneTime}`);
    17.     })
    18.     // error回调监听函数，当avplayer在操作过程中出现错误时，调用reset接口触发重置流程。
    19.     avPlayer.on('error', (err: BusinessError) => {
    20.       console.error(`Invoke avPlayer failed, code is ${err.code}, message is ${err.message}`);
    21.       avPlayer.reset();
    22.     })
    23.     // 状态机变化回调函数。
    24.     avPlayer.on('stateChange', async (state: string, reason: media.StateChangeReason) => {
    25.       switch (state) {
    26.         case 'idle': // 成功调用reset接口后触发该状态机上报。
    27.           console.info('AVPlayer state idle called.');
    28.           avPlayer.release(); // 调用release接口销毁实例对象。
    29.           break;
    30.         case 'initialized': // avplayer 设置播放源后触发该状态上报。
    31.           console.info('AVPlayer state initialized called.');
    32.           avPlayer.surfaceId = this.surfaceID; // 设置显示画面，当播放的资源为纯音频时无需设置。
    33.           avPlayer.prepare();
    34.           break;
    35.         case 'prepared': // prepared调用成功后上报该状态机。
    36.           console.info('AVPlayer state prepared called.');
    37.           avPlayer.play(); // 调用播放接口开始播放。
    38.           break;
    39.         case 'playing': // play成功调用后触发该状态机上报。
    40.           console.info('AVPlayer state playing called.');
    41.           if(this.count !== 0) {
    42.             if (this.isSeek) {
    43.               console.info('AVPlayer start to seek.');
    44.               avPlayer.seek(avPlayer.duration); // seek到视频末尾。
    45.             } else {
    46.               // 当播放模式不支持seek操作时继续播放到结尾。
    47.               console.info('AVPlayer wait to play end.');
    48.             }
    49.           } else {
    50.             avPlayer.pause(); // 调用暂停接口暂停播放。
    51.           }
    52.           this.count++;
    53.           break;
    54.         case 'paused': // pause成功调用后触发该状态机上报。
    55.           console.info('AVPlayer state paused called.');
    56.           avPlayer.play(); // 再次播放接口开始播放。
    57.           break;
    58.         case 'completed': //播放接口后触发该状态机上报。
    59.           console.info('AVPlayer state completed called.');
    60.           avPlayer.stop(); // 调用播放接口。
    61.           break;
    62.         case 'stopped': // stop接口后触发该状态机上报。
    63.           console.info('AVPlayer state stopped called.');
    64.           avPlayer.reset(); // 调用reset接口初始化avplayer状态。
    65.           break;
    66.         case 'released': //播放接口后触发该状态机上报。
    67.           console.info('AVPlayer state released called.');
    68.           break;
    69.         default:
    70.           break;
    71.       }
    72.     })
    73.   }
    
    74.   // 通过url设置网络地址来实现播放直播码流。
    75.   async avPlayerLiveDemo(){
    76.     // 创建avPlayer实例对象。
    77.     let avPlayer: media.AVPlayer = await media.createAVPlayer();
    78.     // 创建状态机变化回调函数。
    79.     this.setAVPlayerCallback(avPlayer);
    80.     this.isSeek = false; // 不支持seek操作。
    81.     // 使用时需要自行替换视频链接。
    82.     avPlayer.url = 'https://xxx.xxx/demo.mp4';
    83.   }
    84. }
    
- 前端页面示例。
    
    1. <!--HAP's src/main/resources/rawfile/test.html-->
    2. <!DOCTYPE html>
    3. <html>
    4. <head>
    5.     <title>同层渲染测试html</title>
    6.     <meta name="viewport">
    7. </head>
    8. <body>
    9. <div>
    10.     <div id="bodyId">
    11.         <embed id="nativeVideo" type = "native/video" width="1000" height="1500" src="test" style = "background-color:red"/>
    12.     </div>
    13. </div>
    14. </body>
    15. </html>
    
- 实现效果：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.00295511658418628925105587767525:50001231000000:2800:0CFDD88168381CD70C6C15BAF9CDF5E0236275B71020AF9ED3E1771C0179C7A3.png)
    

## 同层标签设置为最高层级

同层渲染支持私有属性arkwebnativestyle，该属性仅在开启同层渲染后的<embed>和<object>中生效，该属性的display属性用于控制同层标签的显示层级，使其高于其他Web元素。如果多个同层标签都设置了arkwebnativestyle的display属性，并且属性相同，则它们的层级顺序将遵循W3C标准层级排序规则：先比较z-index属性值，当z-index相同时，按照元素在DOM中的先后顺序排序。display属性取值说明如下：

|display取值|说明|
|:--|:--|
|overlay|设置同层标签层级高于其他Web元素。|
|overlay-infinity|设置同层标签层级高于其他Web元素和设置overlay的同层标签。|

- 应用侧代码：
    
    1. import { webview } from '@kit.ArkWeb';
    2. import { UIContext } from '@kit.ArkUI';
    3. import { NodeController, BuilderNode, NodeRenderType, FrameNode } from '@kit.ArkUI';
    
    4. @Observed
    5. declare class Params{
    6.   elementId: string
    7.   textOne: string
    8.   textTwo: string
    9.   width: number
    10.   height: number
    11. }
    
    12. declare class NodeControllerParams {
    13.   surfaceId: string
    14.   type: string
    15.   renderType: NodeRenderType
    16.   embedId: string
    17.   width: number
    18.   height: number
    19. }
    
    20. // 用于控制和反馈对应的NodeContainer上的节点的行为，需要与NodeContainer一起使用。
    21. class MyNodeController extends NodeController {
    22.   private rootNode: BuilderNode<[Params]> | undefined | null;
    23.   private embedId_: string = "";
    24.   private surfaceId_: string = "";
    25.   private renderType_: NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
    26.   private width_: number = 0;
    27.   private height_: number = 0;
    28.   private type_: string = "";
    29.   private isDestroy_: boolean = false;
    
    30.   setRenderOption(params: NodeControllerParams) {
    31.     this.surfaceId_ = params.surfaceId;
    32.     this.renderType_ = params.renderType;
    33.     this.embedId_ = params.embedId;
    34.     this.width_ = params.width;
    35.     this.height_ = params.height;
    36.     this.type_ = params.type;
    37.   }
    
    38.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
    39.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
    40.   makeNode(uiContext: UIContext): FrameNode | null {
    41.     if (this.isDestroy_) { // rootNode为null。
    42.       return null;
    43.     }
    44.     if (!this.rootNode) {// rootNode 为undefined时。
    45.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_ });
    46.       if (this.type_ == 'native/view1') {
    47.         this.rootNode.build(wrapBuilder(TextInputBuilder1), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
    48.         return this.rootNode.getFrameNode();
    49.       } else if (this.type_ == 'native/view2') {
    50.         this.rootNode.build(wrapBuilder(TextInputBuilder2), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
    51.         return this.rootNode.getFrameNode();
    52.       } else{
    53.         return null;
    54.       }
    55.     }
    56.     // 返回FrameNode节点。
    57.     return this.rootNode.getFrameNode();
    58.   }
    
    59.   updateNode(arg: Object): void {
    60.     this.rootNode?.update(arg);
    61.   }
    
    62.   getEmbedId(): string {
    63.     return this.embedId_;
    64.   }
    
    65.   setDestroy(isDestroy: boolean): void {
    66.     this.isDestroy_ = isDestroy;
    67.     if (this.isDestroy_) {
    68.       this.rootNode = null;
    69.     }
    70.   }
    
    71.   postEvent(event: TouchEvent | undefined): boolean {
    72.     return this.rootNode?.postTouchEvent(event) as boolean
    73.   }
    74. }
    
    75. @Component
    76. struct TextInputComponent1 {
    77.   @Prop params: Params;
    78.   @State bkColor: Color = Color.White;
    
    79.   build() {
    80.     Column() {
    81.       Text("display:overlay-infinity")
    82.       TextInput({text: '', placeholder: 'please input your word...'})
    83.         .placeholderColor(Color.Gray)
    84.         .id(this.params?.elementId)
    85.         .placeholderFont({size: 13, weight: 400})
    86.         .caretColor(Color.Gray)
    87.         .fontSize(14)
    88.         .fontColor(Color.Black)
    89.     }
    90.     // 自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    91.     .width(this.params.width)
    92.     .height(this.params.height)
    93.   }
    94. }
    
    95. // @Builder中为动态组件的具体组件内容。
    96. @Builder
    97. function TextInputBuilder1(params:Params) {
    98.   TextInputComponent1({params: params})
    99.     .width(params.width)
    100.     .height(params.height)
    101.     .backgroundColor(Color.Pink)
    102. }
    
    103. @Component
    104. struct TextInputComponent2 {
    105.   @Prop params: Params;
    106.   @State bkColor: Color = Color.White;
    
    107.   build() {
    108.     Column() {
    109.       Text("display:overlay")
    110.       TextInput({text: '', placeholder: 'please input your word...'})
    111.         .placeholderColor(Color.Gray)
    112.         .id(this.params?.elementId)
    113.         .placeholderFont({size: 13, weight: 400})
    114.         .caretColor(Color.Gray)
    115.         .fontSize(14)
    116.         .fontColor(Color.Black)
    117.     }
    118.     // 自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    119.     .width(this.params.width)
    120.     .height(this.params.height)
    121.   }
    122. }
    
    123. // @Builder中为动态组件的具体组件内容。
    124. @Builder
    125. function TextInputBuilder2(params:Params) {
    126.   TextInputComponent2({params: params})
    127.     .width(params.width)
    128.     .height(params.height)
    129.     .backgroundColor(Color.Gray)
    130. }
    
    131. @Entry
    132. @Component
    133. struct Page{
    134.   browserTabController: webview.WebviewController = new webview.WebviewController();
    135.   private nodeControllerMap: Map<string, MyNodeController> = new Map();
    136.   @State componentIdArr: Array<string> = [];
    137.   @State widthMap: Map<string, number> = new Map();
    138.   @State heightMap: Map<string, number> = new Map();
    139.   @State positionMap: Map<string, Edges> = new Map();
    140.   @State edges: Edges = {};
    141.   uiContext: UIContext = this.getUIContext();
    
    142.   build() {
    143.     Row() {
    144.       Column() {
    145.         Stack() {
    146.           ForEach(this.componentIdArr, (componentId: string) => {
    147.             NodeContainer(this.nodeControllerMap.get(componentId))
    148.               .position(this.positionMap.get(componentId))
    149.               .width(this.widthMap.get(componentId))
    150.               .height(this.heightMap.get(componentId))
    151.           }, (embedId: string) => embedId)
    152.           // Web组件加载本地text.html页面。
    153.           Web({src: $rawfile("overlay.html"), controller: this.browserTabController})
    154.             // 配置同层渲染开关开启。
    155.             .enableNativeEmbedMode(true)
    156.               // 获取<embed>标签的生命周期变化数据。
    157.             .onNativeEmbedLifecycleChange((embed) => {
    158.               console.info("NativeEmbed surfaceId" + embed.surfaceId);
    159.               // 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
    160.               const componentId = embed.info?.id?.toString() as string
    161.               if (embed.status == NativeEmbedStatus.CREATE) {
    162.                 console.info("NativeEmbed create" + JSON.stringify(embed.info));
    163.                 // 创建节点控制器、设置参数。
    164.                 let nodeController = new MyNodeController()
    165.                 // embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
    166.                 nodeController.setRenderOption({surfaceId : embed.surfaceId as string,
    167.                   type : embed.info?.type as string,
    168.                   renderType : NodeRenderType.RENDER_TYPE_TEXTURE,
    169.                   embedId : embed.embedId as string,
    170.                   width : this.uiContext.px2vp(embed.info?.width),
    171.                   height : this.uiContext.px2vp(embed.info?.height)})
    172.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    173.                 nodeController.setDestroy(false);
    174.                 // 根据web传入的embed的id属性作为key，将nodeController存入Map。
    175.                 this.nodeControllerMap.set(componentId, nodeController);
    176.                 this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    177.                 this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    178.                 this.positionMap.set(componentId, this.edges);
    179.                 // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器,需要将push动作放在set之后。
    180.                 this.componentIdArr.push(componentId)
    181.               } else if (embed.status == NativeEmbedStatus.UPDATE) {
    182.                 let nodeController = this.nodeControllerMap.get(componentId);
    183.                 console.info("NativeEmbed update" + JSON.stringify(embed));
    184.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    185.                 this.positionMap.set(componentId, this.edges);
    186.                 this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    187.                 this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    188.                 nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
    189.               } else if (embed.status == NativeEmbedStatus.DESTROY) {
    190.                 console.info("NativeEmbed destroy" + JSON.stringify(embed));
    191.                 let nodeController = this.nodeControllerMap.get(componentId);
    192.                 nodeController?.setDestroy(true);
    193.                 this.nodeControllerMap.delete(componentId);
    194.                 this.positionMap.delete(componentId);
    195.                 this.widthMap.delete(componentId);
    196.                 this.heightMap.delete(componentId);
    197.                 this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
    198.               } else {
    199.                 console.info("NativeEmbed status" + embed.status);
    200.               }
    201.             })// 获取同层渲染组件触摸事件信息。
    202.             .onNativeEmbedGestureEvent((touch) => {
    203.               console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
    204.               this.componentIdArr.forEach((componentId: string) => {
    205.                 let nodeController = this.nodeControllerMap.get(componentId);
    206.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    207.                 if(nodeController?.getEmbedId() == touch.embedId) {
    208.                   let ret = nodeController?.postEvent(touch.touchEvent)
    209.                   if(ret) {
    210.                     console.info("onNativeEmbedGestureEvent success " + componentId);
    211.                   } else {
    212.                     console.info("onNativeEmbedGestureEvent fail " + componentId);
    213.                   }
    214.                   if(touch.result) {
    215.                     // 通知Web组件手势事件消费结果。
    216.                     touch.result.setGestureEventResult(ret);
    217.                   }
    218.                 }
    219.               })
    220.             })
    221.             .border({width: 2, color: Color.Gray})
    222.             .height("50%")
    223.         }
    224.       }
    225.     }
    226.   }
    227. }
    
- 前端页面示例：
    
    示例代码使用<embed>标签，若使用<object>标签，请在ets侧注册<object>标签及type类型。
    
    1. <!--HAP's src/main/resources/rawfile/overlay.html-->
    2. <!DOCTYPE html>
    3. <html>
    4. <head>
    5.     <title>同层渲染html</title>
    6.     <meta name="viewport" content="initial-scale=1.0">
    7. </head>
    8. <body>
    9. <div>
    10.     <div id = "test" style = "position: absolute; z-index: 9999; text-align: center; background-color: rgb(61, 157, 180); top: 40px; left: 30px; width: 300px; height: 120px">
    11.         z-index: 9999
    12.     </div>
    
    13.     <embed id = "input1" type = "native/view1" arkwebnativestyle = "display:overlay-infinity" style = "position: absolute; top: 60px; left: 50px; width: 300px; height: 100px">
    
    14.     <embed id = "input2" type = "native/view2" arkwebnativestyle = "display:overlay" style = "position: absolute; top: 150px; left: 40px; width: 300px; height: 100px">
    15. </div>
    16. </body>
    17. </html>
    
- 实现效果：
    
    未设置arkwebnativestyle的display属性：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.85292742076939813175949351475763:50001231000000:2800:9B6F3259AB7E58279A343B2B510E836CC06121C5F7078AFF9A8F78803C4D93A5.png)
    
    设置arkwebnativestyle的display属性：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.19737308615704125441553207620616:50001231000000:2800:621D5728E84211C8BC104F987F79AC0CA8071962CF0D6418F339B5978651B465.png)
    

## 常见问题

### 同层渲染组件被拉伸该如何解决？

- 组件高度过大
    
    受GPU限制，同层标签存在8000px的高度限制，如果html5中同层标签高度过高，会存在组件被拉伸的情况，这时需要将同层标签的高度设为8000px以下。
    
- 自定义组件宽高未指定为同层渲染标签的宽高
    
    自定义的同层渲染组件宽高需要与同层标签的宽高保持一致，示例如下：
    
    1.   @Component
    2.   struct TextInputComponent {
    3.     @Prop params: Params
    4.     @State bkColor: Color = Color.White
    
    5.     build() {
    6.       Column() {
    7.         TextInput({text: '', placeholder: 'please input your word...'})
    8.           .fontColor(Color.Black)
    9.       }
    10.       // 自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    11.       .width(this.params.width)
    12.       .height(this.params.height)
    13.     }
    14.   }
    

### 如何将同层渲染组件捕获到的事件透传到web前端？

同层渲染手势事件通过[setGestureEventResult()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-eventresult#setgestureeventresult14)设置手势事件消费结果，可以选择系统组件侧或ArkWeb侧消费手势事件。如果要实现系统组件侧和ArkWeb侧同时消费手势事件，可以在[setGestureEventResult()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-eventresult#setgestureeventresult14)中将stopPropagation设置为false，即系统组件侧消费的同时可以将手势事件向上冒泡给ArkWeb。

### 同层渲染页面显示该插件不支持该如何解决？

- 同层渲染开关[enableNativeEmbedMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#enablenativeembedmode11)未开启
    
    使用同层渲染技术需要显式开启同层渲染开关
    
    1. Web({ src: $rawfile("text.html"), controller: this.controller })
    2.   // 配置同层渲染开关开启。
    3.   .enableNativeEmbedMode(true)
    
- 同层标签使用有误
    
    如果使用<embed>标签，需要显式书写embed，并且type类型以"native/"开头；如果使用<object>标签，需要注册<object>标签及type类型。
    

### 涉及界面交互的ArkUI组件（如TextInput等）光标与输入框错位该如何解决？

首先，需使用Stack包裹同层组件容器和BuilderNode。其次，同层组件容器NodeContainer应与同层标签的位置绑定。示例如下：

1. ForEach(this.componentIdArr, (componentId: string) => {
2.   NodeContainer(this.nodeControllerMap.get(componentId))
3.     // 同层组件容器应与同层标签的宽高和位置绑定。
4.     .position(this.positionMap.get(componentId))
5.     .width(this.widthMap.get(componentId))
6.     .height(this.heightMap.get(componentId))
7. }, (embedId: string) => embedId)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-data-detector "使用Web组件的智能分词能力")
# 同层渲染

更新时间: 2025-12-16 16:38

在系统中，应用可以使用Web组件加载Web网页。当非系统框架的UI组件功能或性能不如系统组件时，可使用同层渲染技术，通过ArkUI组件渲染这些组件（简称为同层组件）。

## 使用场景

### Web网页

小程序的地图组件，可以使用ArkUI的XComponent组件渲染来提升性能。小程序的输入框组件，可以使用ArkUI的TextInput组件渲染，达到与系统应用一致的输入体验。

- 在网页侧，应用开发者可将<embed>、<object>的网页UI组件（简称为同层标签），按一定规则进行同层渲染，详细规格见同层渲染规格小节。
    
- 在应用侧，应用开发者可以通过Web组件的同层渲染事件上报接口，感知到H5同层标签的生命周期以及输入事件，进行同层渲染组件的相应业务逻辑处理。
    
- 在应用侧，应用开发者可以使用ArkUI的NodeContainer等接口，构建H5同层标签对应的同层渲染组件。可支持同层渲染的ArkUI常用组件包括：[TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput), [XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent), [Canvas](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-canvas-canvas), [Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video), [Web](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)。具体规格可参见[同层渲染规格小节](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-same-layer#%E8%A7%84%E6%A0%BC%E7%BA%A6%E6%9D%9F)。
    

### 三方UI框架

Flutter提供了PlatformView与Texture抽象组件，这些组件可使用系统组件渲染，用于支持Flutter组件功能不足的部分。Weex2.0框架的Camera、Video和Canvas组件可以使用系统组件渲染，以增强功能和性能。

- 在三方框架页面侧，由于Flutter、Weex等三方框架不在操作系统范围内，本文不列举可被同层渲染的三方框架UI组件的范围与使用方式。
    
- 在应用侧，应用开发者可以使用ArkUI的NodeContainer等接口，构建三方框架同层标签对应的同层渲染组件。可支持同层渲染的ArkUI常用组件包括：[TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput), [XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent), [Canvas](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-canvas-canvas), [Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video), [Web](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)。具体规格可参见[同层渲染规格](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-same-layer#%E8%A7%84%E6%A0%BC%E7%BA%A6%E6%9D%9F)。
    

## 整体架构

ArkWeb同层渲染特性主要提供两种能力：同层标签生命周期和事件命中转发处理。

同层标签生命周期主要关联前端标签（<embed>/<object>），同时命中到同层标签的事件会被上报到开发者侧，由开发者分发到对应组件树。整体框架如下图所示：

**图1** 同层渲染整体架构

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.39410890836484253361083841709687:50001231000000:2800:6C89848D97E0DC98FDAEED734576663B8B0268882EE5205B6F2205A0F127BB09.png)

## 规格约束

### 可被同层渲染的ArkUI组件

以下规格对Web网页和三方框架场景均生效。

**支持的组件范围:**

- 基础组件：[AlphabetIndexer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-alphabet-indexer), [Blank](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-blank), [Button](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-button), [CalendarPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-calendarpicker), [Checkbox](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-checkbox), [CheckboxGroup](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-checkboxgroup), [ContainerSpan](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-containerspan), [DataPanel](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-datapanel), [DatePicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-datepicker), [Divider](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-divider), [Gauge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-gauge), [Hyperlink](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-hyperlink), [Image](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-image), [ImageAnimator](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-imageanimator), [ImageSpan](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-imagespan), [LoadingProgress](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-loadingprogress), [Marquee](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-marquee), [PatternLock](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-patternlock), [Progress](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-progress), [QRCode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-qrcode), [Radio](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-radio), [Rating](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-rating), [Refresh](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-refresh), [ScrollBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-scroll), [Search](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-search), [Span](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-span), [Select](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-select), [Slider](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-slider), [Text](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-text), [TextArea](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textarea), [TextClock](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textclock), [TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput), [TextPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textpicker), [TextTimer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-texttimer), [TimePicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-timepicker), [Toggle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-toggle)
    
- 容器类组件：[Badge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-badge), [Column](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-column), [ColumnSplit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-columnsplit), [Counter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-counter), [Flex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-flex), [GridCol](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-gridcol), [GridRow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-gridrow), [Grid](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-grid), [GridItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-griditem)，[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-list), [ListItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-listitem), [ListItemGroup](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-listitemgroup), [RelativeContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-relativecontainer), [Row](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-row), [RowSplit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-rowsplit), [Scroll](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-scroll), [Stack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-stack), [Swiper](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-swiper), [Tabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabs), [TabContent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabcontent), [NodeContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-nodecontainer), [SideBarContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-sidebarcontainer), [Stepper](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-stepper), [StepperItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-stepperitem), [WaterFlow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-waterflow), [FlowItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-flowitem)
    
- 自绘制类组件：[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent), [Canvas](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-canvas-canvas), [Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video), [Web](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)
    
- 命令式自定义绘制节点：[BuilderNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-buildernode), [ComponentContent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-componentcontent), [ContentSlot](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-contentslot), [FrameNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-framenode), [Graphics](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-graphics), [NodeController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-nodecontroller), [RenderNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-rendernode), [XComponentNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-xcomponentnode), [AttributeUpdater](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-attributeupdater), [CAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-arkui-nativemodule)（支持同层渲染的组件范围同ArkTS）
    

**支持的组件通用属性与事件:**

- 不支持的通用属性：[分布式迁移标识](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-restoreid)，[特效绘制合并](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-use-effect)。
    
- 其他未明确标注不支持的属性与事件及组件能力，均默认支持。
    

### Web网页的同层渲染标签

此规格仅针对Web网页，不适用于三方框架场景。

如果应用需要在Web组件加载的网页中使用同层渲染，需要按照以下规格将网页中的<embed>、<object>标签指定为同层渲染组件。

**支持的H5标签：**

- 支持<embed>标签：在开启同层渲染后，仅支持type类型为native前缀的标签识别为同层组件，不支持自定义属性。
    
- 支持<object>标签：在开启同层渲染后，支持将非标准MIME type的object标签识别为同层组件，支持通过param/value的自定义属性解析。
    
- 不支持W3C规范标准标签（如<input>、<video>）定义为同层标签。
    
- 不支持同时配置<object>标签和<embed>标签作为同层标签。
    
- 标签类型只支持英文字符，不区分大小写。
    

**同层标签支持的css属性：**

display，position，z-index，visibility，opacity, background-color，background-image，width，height，padding，padding-left，padding-top，padding-right，padding-bottom，margin，margin-left，margin-top，margin-right，margin-bottom，border-width，border-style，border-color，border-left-width，border-left-style，border-left-color，border-top-width，border-top-style，border-top-color，border-right-width，border-right-style，border-right-color，border-bottom-width，border-bottom-style，border-bottom-color，border-left，border-right，border-top，border-bottom，border，border-top-left-radius，border-top-right-radius，border-bottom-left-radius，border-bottom-right-radius，border-radius，transition，transform（仅支持translate/scale，scale对应参数只支持大于等于0的值）

除上面支持的css属性范围，其他的css属性均不保证符合预期，比如transform属性中的rotate，skew等。

**同层标签的生命周期管理：**

当同层标签生命周期变化时触发[onNativeEmbedLifecycleChange()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedlifecyclechange11)回调。

- 支持创建、销毁、位置宽高变化。
    
- 支持同层组件所在Web页面进入前进后退缓存。
    

**同层标签的输入事件分发处理：**

- 支持触摸事件TouchEvent的DOWN/UP/MOVE/CANCEL。支持[配置触摸事件消费结果](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedgestureevent11)，默认为应用侧消费。
    
- 不支持同层标签所在的应用页面缩放和[initialScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#initialscale9)、[zoom](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#zoom)、[zoomIn](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#zoomin)、[zoomOut](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#zoomout)等缩放接口。
    
- 暂不支持鼠标、键盘、触摸板事件上报。
    
- 支持默认将鼠标和触摸板左键事件（MousePress/MouseRelease/MouseMOVE）转换为触摸事件（TouchDOWN/TouchUP/TouchMOVE）上报。
    

**同层标签的可见状态变化：**

当同层标签可见状态变化时触发[onNativeEmbedVisibilityChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedvisibilitychange12)回调。

- 支持同层标签相对于视口的可见状态上报。
    
- 默认不支持由于同层标签CSS样式或尺寸变化导致的可见状态变化上报，具体规格参考[onNativeEmbedVisibilityChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedvisibilitychange12)。
    

**同层渲染<object>标签内嵌param元素状态变化：**

当同层渲染<object>内嵌标签param元素变化时触发[onNativeEmbedObjectParamChange()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedobjectparamchange21)回调。

- 支持上报param元素的增加、修改、删除三种状态变化。
    
- 接口每次最多上报500个param元素变化信息，超出部分将分多次上报。
    
- 详细上报信息参考[NativeEmbedParamDataInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-i#nativeembedparamdatainfo21)。
    

**约束限制：**

- Web页面内同层标签数量应控制在5个以内。超过5个，渲染性能将会下降。
    
- 受GPU限制，同层标签最大高度不超过8000px，最大纹理大小为8000px。
    
- 开启同层渲染后，Web组件打开的所有Web页面将不支持同步渲染模式[RenderMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#rendermode12)。
    
- Video组件：在非全屏Video变为全屏时，Video组件变为非纹理导出模式，视频播放状态保持延续；恢复为非全屏时，变为纹理导出模式，视频播放状态保持延续。
    
- Web组件：仅支持一层同层渲染嵌套，不支持多层同层渲染嵌套。输入事件只支持滑动、点击、长按，不支持拖拽、旋转、缩放。
    
- 涉及界面交互的ArkUI组件（如TextInput等）：建议在页面布局中使用Stack包裹同层组件容器与BuilderNode，并使两者位置一致，NodeContainer要与<embed>/<object>标签对齐，以保障组件正常交互。如两者位置不一致，可能出现的问题有：TextInput/TextArea等附属的文本选择框位置错位（如下图）、LoadingProgress/Marquee等组件的动画启停与组件可见状态不匹配。
    
    **图2** 未使用Stack包裹，TextInput的位置错位
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.83659815536941758218255870630249:50001231000000:2800:2DF8EFA2ECC43F8D29A1B340A2DDD7F0D18E4BA0959C8B74C8A2E140E207DFDC.png)
    
    **图3** 使用Stack包裹，TextInput的位置正常
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.99416238214956841185269338927042:50001231000000:2800:0CC8EBF4568814B454ECF1C19B0740351F24C92088FFE630FAA656FB2C2D20C8.png)
    

## Web页面中同层渲染输入框

在Web页面中，可以使用ArkUI系统的TextInput组件进行同层渲染。此处利用同层渲染展示三个输入框，渲染效果图如下：

**图4** 同层渲染输入框

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.64649427145049818214449563250542:50001231000000:2800:14959B3CEB3EAE584B8D691B4A2F57E4621BFBF925419AE2FBFC012B465AFAFE.png)

1. 在Web页面中标记需要同层渲染的HTML标签。
    
    同层渲染支持<embed>/<object>两种标签。type类型可任意指定，两个字符串参数均不区分大小写，ArkWeb内核将会统一转换为小写。其中，tag字符串使用全字符串匹配，type使用字符串前缀匹配。
    
    若开发者不使用该接口或该接口接收的为非法字符串（空字符串）时，ArkWeb内核将使用默认设置，即"embed" + "native/"前缀模式。若指定类型与w3c定义的<embed>或<object>标准类型重合，如registerNativeEmbedRule("object", "application/pdf")，ArkWeb将遵循w3c标准行为，不会将其识别为同层标签。
    
    - 采用<embed>标签。
        
        1. <!--HAP's src/main/resources/rawfile/text.html-->
        2. <!DOCTYPE html>
        3. <html>
        4. <head>
        5.     <title>同层渲染html</title>
        6.     <meta name="viewport">
        7. </head>
        
        8. <body style="background:white">
        
        9. <embed id = "input1" type="native/view" style="width: 100%; height: 100px; margin: 30px; margin-top: 600px"/>
        
        10. <embed id = "input2" type="native/view2" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"/>
        
        11. <embed id = "input3" type="native/view3" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"/>
        
        12. </body>
        13. </html>
        
    - 采用<object>标签。
        
        需要使用registerNativeEmbedRule注册object标签。
        
        1. // ...
        2. Web({src: $rawfile("text.html"), controller: this.browserTabController})
        3.   // 注册同层标签为"object"，类型为"test"前缀。
        4.   .registerNativeEmbedRule("object", "test")
        5.   // ...
        
        与registerNativeEmbedRule相对应的前端页面代码，类型可使用"test"及以"test"为前缀的字串。
        
        6. <!--HAP's src/main/resources/rawfile/text.html-->
        7. <!DOCTYPE html>
        8. <html>
        9. <head>
        10.     <title>同层渲染html</title>
        11.     <meta name="viewport">
        12. </head>
        
        13. <body style="background:white">
        
        14. <object id = "input1" type="test/input" style="width: 100%; height: 100px; margin: 30px; margin-top: 600px"></object>
        
        15. <object id = "input2" type="test/input" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"></object>
        
        16. <object id = "input3" type="test/input" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"></object>
        
        17. </body>
        18. </html>
        
2. 在应用侧开启同层渲染功能。
    
    同层渲染功能默认不开启，如果要使用同层渲染的功能，可通过[enableNativeEmbedMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#enablenativeembedmode11)来开启。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller: webview.WebviewController = new webview.WebviewController();
    
    7.   build() {
    8.     Column() {
    9.       Web({ src: 'www.example.com', controller: this.controller })
    10.         // 配置同层渲染开关开启。
    11.         .enableNativeEmbedMode(true)
    12.     }
    13.   }
    14. }
    
3. 创建自定义组件。
    
    同层渲染功能开启后，展示在对应区域的系统组件。
    
    1. @Component
    2. struct TextInputComponent {
    3.   @Prop params: Params
    4.   @State bkColor: Color = Color.White
    
    5.   build() {
    6.     Column() {
    7.       TextInput({text: '', placeholder: 'please input your word...'})
    8.         .placeholderColor(Color.Gray)
    9.         .id(this.params?.elementId)
    10.         .placeholderFont({size: 13, weight: 400})
    11.         .caretColor(Color.Gray)
    12.         .width(this.params?.width)
    13.         .height(this.params?.height)
    14.         .fontSize(14)
    15.         .fontColor(Color.Black)
    16.     }
    17.     //自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    18.     .width(this.params.width)
    19.     .height(this.params.height)
    20.   }
    21. }
    
    22. @Builder
    23. function TextInputBuilder(params:Params) {
    24.   TextInputComponent({params: params})
    25.     .width(params.width)
    26.     .height(params.height)
    27.     .backgroundColor(Color.White)
    28. }
    
4. 创建节点控制器。
    
    用于控制和反馈对应NodeContainer上的节点行为。
    
    1. class MyNodeController extends NodeController {
    2.   private rootNode: BuilderNode<[Params]> | undefined | null;
    3.   private embedId_: string = "";
    4.   private surfaceId_: string = "";
    5.   private renderType_: NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
    6.   private width_: number = 0;
    7.   private height_: number = 0;
    8.   private type_: string = "";
    9.   private isDestroy_: boolean = false;
    
    10.   setRenderOption(params: NodeControllerParams) {
    11.     this.surfaceId_ = params.surfaceId;
    12.     this.renderType_ = params.renderType;
    13.     this.embedId_ = params.embedId;
    14.     this.width_ = params.width;
    15.     this.height_ = params.height;
    16.     this.type_ = params.type;
    17.   }
    
    18.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
    19.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
    20.   makeNode(uiContext: UIContext): FrameNode | null {
    21.     if (this.isDestroy_) { // rootNode为null。
    22.       return null;
    23.     }
    24.     if (!this.rootNode) {// rootNode 为undefined时。
    25.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_ });
    26.       if(this.rootNode) {
    27.         this.rootNode.build(wrapBuilder(TextInputBuilder), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
    28.         return this.rootNode.getFrameNode();
    29.       }else{
    30.         return null;
    31.       }
    32.     }
    33.     // 返回FrameNode节点。
    34.     return this.rootNode.getFrameNode();
    35.   }
    
    36.   updateNode(arg: Object): void {
    37.     this.rootNode?.update(arg);
    38.   }
    
    39.   getEmbedId(): string {
    40.     return this.embedId_;
    41.   }
    
    42.   setDestroy(isDestroy: boolean): void {
    43.     this.isDestroy_ = isDestroy;
    44.     if (this.isDestroy_) {
    45.       this.rootNode = null;
    46.     }
    47.   }
    
    48.   postEvent(event: TouchEvent | undefined): boolean {
    49.     return this.rootNode?.postTouchEvent(event) as boolean
    50.   }
    51. }
    
5. 监听同层渲染的生命周期变化。
    
    开启该功能后，当网页中存在同层渲染支持的标签时，ArkWeb内核会触发由[onNativeEmbedLifecycleChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedlifecyclechange11)注册的回调函数。
    
    开发者则需要调用[onNativeEmbedLifecycleChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedlifecyclechange11)来监听同层渲染标签的生命周期变化。
    
    1. build() {
    2.   Row() {
    3.     Column() {
    4.       Stack() {
    5.         ForEach(this.componentIdArr, (componentId: string) => {
    6.           NodeContainer(this.nodeControllerMap.get(componentId))
    7.             .position(this.positionMap.get(componentId))
    8.             .width(this.widthMap.get(componentId))
    9.             .height(this.heightMap.get(componentId))
    10.         }, (embedId: string) => embedId)
    11.         // Web组件加载本地text.html页面。
    12.         Web({src: $rawfile("text.html"), controller: this.browserTabController})
    13.           // 配置同层渲染开关开启。
    14.           .enableNativeEmbedMode(true)
    15.             // 注册同层标签为<object>，类型为"test"前缀。
    16.           .registerNativeEmbedRule("object", "test")
    17.             // 获取<embed>标签的生命周期变化数据。
    18.           .onNativeEmbedLifecycleChange((embed) => {
    19.             console.info("NativeEmbed surfaceId" + embed.surfaceId);
    20.             // 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
    21.             const componentId = embed.info?.id?.toString() as string
    22.             if (embed.status == NativeEmbedStatus.CREATE) {
    23.               console.info("NativeEmbed create" + JSON.stringify(embed.info));
    24.               // 创建节点控制器、设置参数。
    25.               let nodeController = new MyNodeController()
    26.               // embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
    27.               nodeController.setRenderOption({surfaceId : embed.surfaceId as string,
    28.                 type : embed.info?.type as string,
    29.                 renderType : NodeRenderType.RENDER_TYPE_TEXTURE,
    30.                 embedId : embed.embedId as string,
    31.                 width : this.uiContext.px2vp(embed.info?.width),
    32.                 height : this.uiContext.px2vp(embed.info?.height)})
    33.               this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    34.               nodeController.setDestroy(false);
    35.               //根据web传入的embed的id属性作为key，将nodeController存入Map。
    36.               this.nodeControllerMap.set(componentId, nodeController);
    37.               this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    38.               this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    39.               this.positionMap.set(componentId, this.edges);
    40.               // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器,需要将push动作放在set之后。
    41.               this.componentIdArr.push(componentId)
    42.             } else if (embed.status == NativeEmbedStatus.UPDATE) {
    43.               let nodeController = this.nodeControllerMap.get(componentId);
    44.               console.info("NativeEmbed update" + JSON.stringify(embed));
    45.               this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    46.               this.positionMap.set(componentId, this.edges);
    47.               this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    48.               this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    49.               nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
    50.             } else if (embed.status == NativeEmbedStatus.DESTROY) {
    51.               console.info("NativeEmbed destroy" + JSON.stringify(embed));
    52.               let nodeController = this.nodeControllerMap.get(componentId);
    53.               nodeController?.setDestroy(true);
    54.               this.nodeControllerMap.delete(componentId);
    55.               this.positionMap.delete(componentId);
    56.               this.widthMap.delete(componentId);
    57.               this.heightMap.delete(componentId);
    58.               this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
    59.             } else {
    60.               console.info("NativeEmbed status" + embed.status);
    61.             }
    62.           })
    63.       }.height("80%")
    64.     }
    65.   }
    66. }
    
6. 同层渲染手势事件。
    
    开启该功能后，每当在同层渲染的区域进行触摸操作时，ArkWeb内核会触发[onNativeEmbedGestureEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedgestureevent11)注册的回调函数。
    
    开发者则需要调用[onNativeEmbedGestureEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedgestureevent11)来监听同层渲染区域的手势事件。
    
    1. build() {
    2.   Row() {
    3.     Column() {
    4.       Stack() {
    5.         ForEach(this.componentIdArr, (componentId: string) => {
    6.           NodeContainer(this.nodeControllerMap.get(componentId))
    7.             .position(this.positionMap.get(componentId))
    8.             .width(this.widthMap.get(componentId))
    9.             .height(this.heightMap.get(componentId))
    10.         }, (embedId: string) => embedId)
    11.         // Web组件加载本地text.html页面。
    12.         Web({src: $rawfile("text.html"), controller: this.browserTabController})
    13.           // 配置同层渲染开关开启。
    14.           .enableNativeEmbedMode(true)
    15.             // 获取<embed>标签的生命周期变化数据。
    16.           .onNativeEmbedLifecycleChange((embed) => {
    17.             // 生命周期变化实现。
    18.           })
    19.           .onNativeEmbedGestureEvent((touch) => {
    20.             console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
    21.             this.componentIdArr.forEach((componentId: string) => {
    22.               let nodeController = this.nodeControllerMap.get(componentId);
    23.               // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    24.               if(nodeController?.getEmbedId() == touch.embedId) {
    25.                 let ret = nodeController?.postEvent(touch.touchEvent)
    26.                 if(ret) {
    27.                   console.info("onNativeEmbedGestureEvent success " + componentId);
    28.                 } else {
    29.                   console.info("onNativeEmbedGestureEvent fail " + componentId);
    30.                 }
    31.                 if(touch.result) {
    32.                   // 通知Web组件手势事件消费结果。
    33.                   touch.result.setGestureEventResult(ret);
    34.                 }
    35.               }
    36.             })
    37.           })
    38.       }
    39.     }
    40.   }
    41. }
    
7. 同层渲染鼠标事件
    
    开启该功能后，在同层渲染的区域进行下述动作时，ArkWeb内核会触发[onNativeEmbedMouseEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedmouseevent20)注册的回调函数：
    
    - 使用鼠标左键、中键、右键进行点击或长按。
    - 使用触摸板进行对应鼠标左键、中键、右键点击长按的操作。
    
    开发者则需要调用[onNativeEmbedMouseEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedmouseevent20)来监听同层渲染区域的鼠标事件。
    
    1. build() {
    2.   Row() {
    3.     Column() {
    4.       Stack() {
    5.         ForEach(this.componentIdArr, (componentId: string) => {
    6.           NodeContainer(this.nodeControllerMap.get(componentId))
    7.             .position(this.positionMap.get(componentId))
    8.             .width(this.widthMap.get(componentId))
    9.             .height(this.heightMap.get(componentId))
    10.         }, (embedId: string) => embedId)
    11.         // Web组件加载本地text.html页面。
    12.         Web({src: $rawfile("text.html"), controller: this.browserTabController})
    13.           // 配置同层渲染开关开启。
    14.           .enableNativeEmbedMode(true)
    15.             // 获取<embed>标签的生命周期变化数据。
    16.           .onNativeEmbedLifecycleChange((embed) => {
    17.             // 生命周期变化实现。
    18.           })
    19.           .onNativeEmbedGestureEvent((touch) => {
    20.             // 处理同层渲染手势事件。
    21.           })
    22.           .onNativeEmbedMouseEvent((mouse) => {
    23.             console.info("NativeEmbed onNativeEmbedMouseEvent" + JSON.stringify(mouse.mouseEvent));
    24.             this.componentIdArr.forEach((componentId: string) => {
    25.               let nodeController = this.nodeControllerMap.get(componentId);
    26.               // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    27.               if(nodeController?.getEmbedId() == mouse.embedId) {
    28.                 let ret = nodeController?.postInputEvent(mouse.mouseEvent)
    29.                 if(ret) {
    30.                   console.info("onNativeEmbedMouseEvent success " + componentId);
    31.                 } else {
    32.                   console.info("onNativeEmbedMouseEvent fail " + componentId);
    33.                 }
    34.                 if(mouse.result) {
    35.                   // 通知Web组件鼠标事件消费结果。
    36.                   mouse.result.setMouseEventResult(ret);
    37.                 }
    38.               }
    39.             })
    40.           })
    41.       }
    42.     }
    43.   }
    44. }
    

**完整示例：**

使用前请在module.json5中添加网络权限，添加方法请参考[在配置文件中声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。

1. "requestPermissions":[
2.     {
3.       "name" : "ohos.permission.INTERNET"
4.     }
5.   ]

应用侧代码。

1. // 创建NodeController
2. import { webview } from '@kit.ArkWeb';
3. import { UIContext } from '@kit.ArkUI';
4. import { NodeController, BuilderNode, NodeRenderType, FrameNode } from '@kit.ArkUI';

5. @Observed
6. declare class Params{
7.   elementId: string
8.   textOne: string
9.   textTwo: string
10.   width: number
11.   height: number
12. }

13. declare class NodeControllerParams {
14.   surfaceId: string
15.   type: string
16.   renderType: NodeRenderType
17.   embedId: string
18.   width: number
19.   height: number
20. }

21. // 用于控制和反馈对应的NodeContainer上的节点的行为，需要与NodeContainer一起使用。
22. class MyNodeController extends NodeController {
23.   private rootNode: BuilderNode<[Params]> | undefined | null;
24.   private embedId_: string = "";
25.   private surfaceId_: string = "";
26.   private renderType_: NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
27.   private width_: number = 0;
28.   private height_: number = 0;
29.   private type_: string = "";
30.   private isDestroy_: boolean = false;

31.   setRenderOption(params: NodeControllerParams) {
32.     this.surfaceId_ = params.surfaceId;
33.     this.renderType_ = params.renderType;
34.     this.embedId_ = params.embedId;
35.     this.width_ = params.width;
36.     this.height_ = params.height;
37.     this.type_ = params.type;
38.   }

39.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
40.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
41.   makeNode(uiContext: UIContext): FrameNode | null {
42.     if (this.isDestroy_) { // rootNode为null。
43.       return null;
44.     }
45.     if (!this.rootNode) {// rootNode 为undefined时。
46.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_ });
47.       if(this.rootNode) {
48.         this.rootNode.build(wrapBuilder(TextInputBuilder), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
49.         return this.rootNode.getFrameNode();
50.       }else{
51.         return null;
52.       }
53.     }
54.     // 返回FrameNode节点。
55.     return this.rootNode.getFrameNode();
56.   }

57.   updateNode(arg: Object): void {
58.     this.rootNode?.update(arg);
59.   }

60.   getEmbedId(): string {
61.     return this.embedId_;
62.   }

63.   setDestroy(isDestroy: boolean): void {
64.     this.isDestroy_ = isDestroy;
65.     if (this.isDestroy_) {
66.       this.rootNode = null;
67.     }
68.   }

69.   postEvent(event: TouchEvent | undefined): boolean {
70.     return this.rootNode?.postTouchEvent(event) as boolean
71.   }

72.   postInputEvent(event: MouseEvent | undefined): boolean {
73.     return this.rootNode?.postInputEvent(event) as boolean
74.   }
75. }

76. @Component
77. struct TextInputComponent {
78.   @Prop params: Params
79.   @State bkColor: Color = Color.White

80.   build() {
81.     Column() {
82.       TextInput({text: '', placeholder: 'please input your word...'})
83.         .placeholderColor(Color.Gray)
84.         .id(this.params?.elementId)
85.         .placeholderFont({size: 13, weight: 400})
86.         .caretColor(Color.Gray)
87.         .fontSize(14)
88.         .fontColor(Color.Black)
89.     }
90.     //自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
91.     .width(this.params.width)
92.     .height(this.params.height)
93.   }
94. }

95. // @Builder中为动态组件的具体组件内容。
96. @Builder
97. function TextInputBuilder(params:Params) {
98.   TextInputComponent({params: params})
99.     .width(params.width)
100.     .height(params.height)
101.     .backgroundColor(Color.White)
102. }

103. @Entry
104. @Component
105. struct Page{
106.   browserTabController: WebviewController = new webview.WebviewController()
107.   private nodeControllerMap: Map<string, MyNodeController> = new Map();
108.   @State componentIdArr: Array<string> = [];
109.   @State widthMap: Map<string, number> = new Map();
110.   @State heightMap: Map<string, number> = new Map();
111.   @State positionMap: Map<string, Edges> = new Map();
112.   @State edges: Edges = {};
113.   uiContext: UIContext = this.getUIContext();

114.   build() {
115.     Row() {
116.       Column() {
117.         Stack() {
118.           ForEach(this.componentIdArr, (componentId: string) => {
119.             NodeContainer(this.nodeControllerMap.get(componentId))
120.               .position(this.positionMap.get(componentId))
121.               .width(this.widthMap.get(componentId))
122.               .height(this.heightMap.get(componentId))
123.           }, (embedId: string) => embedId)
124.           // Web组件加载本地text.html页面。
125.           Web({src: $rawfile("text.html"), controller: this.browserTabController})
126.             // 配置同层渲染开关开启。
127.             .enableNativeEmbedMode(true)
128.             // 获取<embed>标签的生命周期变化数据。
129.             .onNativeEmbedLifecycleChange((embed) => {
130.                console.info("NativeEmbed surfaceId" + embed.surfaceId);
131.                // 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
132.                const componentId = embed.info?.id?.toString() as string
133.                if (embed.status == NativeEmbedStatus.CREATE) {
134.                  console.info("NativeEmbed create" + JSON.stringify(embed.info));
135.                  // 创建节点控制器、设置参数。
136.                  let nodeController = new MyNodeController()
137.                  // embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
138.                  nodeController.setRenderOption({surfaceId : embed.surfaceId as string,
139.                    type : embed.info?.type as string,
140.                    renderType : NodeRenderType.RENDER_TYPE_TEXTURE,
141.                    embedId : embed.embedId as string,
142.                    width : this.uiContext.px2vp(embed.info?.width),
143.                    height : this.uiContext.px2vp(embed.info?.height)})
144.                  this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
145.                  nodeController.setDestroy(false);
146.                  //根据web传入的embed的id属性作为key，将nodeController存入Map。
147.                  this.nodeControllerMap.set(componentId, nodeController);
148.                  this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
149.                  this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
150.                  this.positionMap.set(componentId, this.edges);
151.                  // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器,需要将push动作放在set之后。
152.                  this.componentIdArr.push(componentId)
153.                } else if (embed.status == NativeEmbedStatus.UPDATE) {
154.                  let nodeController = this.nodeControllerMap.get(componentId);
155.                  console.info("NativeEmbed update" + JSON.stringify(embed));
156.                  this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
157.                  this.positionMap.set(componentId, this.edges);
158.                  this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
159.                  this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
160.                  nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
161.                } else if (embed.status == NativeEmbedStatus.DESTROY) {
162.                  console.info("NativeEmbed destroy" + JSON.stringify(embed));
163.                  let nodeController = this.nodeControllerMap.get(componentId);
164.                  nodeController?.setDestroy(true);
165.                  this.nodeControllerMap.delete(componentId);
166.                  this.positionMap.delete(componentId);
167.                  this.widthMap.delete(componentId);
168.                  this.heightMap.delete(componentId);
169.                  this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
170.                } else {
171.                  console.info("NativeEmbed status" + embed.status);
172.                }
173.              })// 获取同层渲染组件触摸事件信息。
174.             .onNativeEmbedGestureEvent((touch) => {
175.               console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
176.               this.componentIdArr.forEach((componentId: string) => {
177.                 let nodeController = this.nodeControllerMap.get(componentId);
178.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
179.                 if(nodeController?.getEmbedId() == touch.embedId) {
180.                   let ret = nodeController?.postEvent(touch.touchEvent)
181.                   if(ret) {
182.                     console.info("onNativeEmbedGestureEvent success " + componentId);
183.                   } else {
184.                     console.info("onNativeEmbedGestureEvent fail " + componentId);
185.                   }
186.                   if(touch.result) {
187.                     // 通知Web组件手势事件消费结果。
188.                     touch.result.setGestureEventResult(ret);
189.                   }
190.                 }
191.               })
192.             })
193.             .onNativeEmbedMouseEvent((mouse) => {
194.               console.info("NativeEmbed onNativeEmbedMouseEvent" + JSON.stringify(mouse.mouseEvent));
195.               this.componentIdArr.forEach((componentId: string) => {
196.                 let nodeController = this.nodeControllerMap.get(componentId);
197.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
198.                 if(nodeController?.getEmbedId() == mouse.embedId) {
199.                   let ret = nodeController?.postInputEvent(mouse.mouseEvent)
200.                   if(ret) {
201.                     console.info("onNativeEmbedMouseEvent success " + componentId);
202.                   } else {
203.                     console.info("onNativeEmbedMouseEvent fail " + componentId);
204.                   }
205.                   if(mouse.result) {
206.                     // 通知Web组件鼠标事件消费结果。
207.                     mouse.result.setMouseEventResult(ret);
208.                   }
209.                 }
210.               })
211.             })
212.         }
213.       }
214.     }
215.   }
216. }

## 绘制XComponent+AVPlayer和Button组件

- 应用侧代码组件使用示例。
    
    1. // HAP's src/main/ets/pages/Index.ets
    2. // 创建NodeController
    3. import { webview } from '@kit.ArkWeb';
    4. import { UIContext, NodeController, BuilderNode, NodeRenderType, FrameNode } from "@kit.ArkUI";
    5. import { AVPlayerDemo } from './PlayerDemo';
    
    6. @Observed
    7. declare class Params {
    8.   textOne : string
    9.   textTwo : string
    10.   width : number
    11.   height : number
    12. }
    
    13. declare class NodeControllerParams {
    14.   surfaceId : string
    15.   type : string
    16.   renderType : NodeRenderType
    17.   embedId : string
    18.   width : number
    19.   height : number
    20. }
    
    21. // 用于控制和反馈对应的NodeContainer上的节点的行为，需要与NodeContainer一起使用。
    22. class MyNodeController extends NodeController {
    23.   private rootNode: BuilderNode<[Params]> | undefined | null;
    24.   private embedId_ : string = "";
    25.   private surfaceId_ : string = "";
    26.   private renderType_ :NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
    27.   private width_ : number = 0;
    28.   private height_ : number = 0;
    29.   private type_ : string = "";
    30.   private isDestroy_ : boolean = false;
    
    31.   setRenderOption(params : NodeControllerParams) {
    32.     this.surfaceId_ = params.surfaceId;
    33.     this.renderType_ = params.renderType;
    34.     this.embedId_ = params.embedId;
    35.     this.width_ = params.width;
    36.     this.height_ = params.height;
    37.     this.type_ = params.type;
    38.   }
    39.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
    40.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
    41.   makeNode(uiContext: UIContext): FrameNode | null{
    42.     if (this.isDestroy_) { // rootNode为null。
    43.       return null;
    44.     }
    45.     if (!this.rootNode) { // rootNode 为undefined时。
    46.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_});
    47.       if (this.type_ === 'native/video') {
    48.         this.rootNode.build(wrapBuilder(VideoBuilder), {textOne: "myButton", width : this.width_, height : this.height_});
    49.       } else {
    50.         // other
    51.       }
    52.     }
    53.     // 返回FrameNode节点。
    54.     return this.rootNode.getFrameNode();
    55.   }
    
    56.   updateNode(arg: Object): void {
    57.     this.rootNode?.update(arg);
    58.   }
    59.   getEmbedId() : string {
    60.     return this.embedId_;
    61.   }
    
    62.   setDestroy(isDestroy : boolean) : void {
    63.     this.isDestroy_ = isDestroy;
    64.     if (this.isDestroy_) {
    65.       this.rootNode = null;
    66.     }
    67.   }
    
    68.   postEvent(event: TouchEvent | undefined) : boolean {
    69.     return this.rootNode?.postTouchEvent(event) as boolean
    70.   }
    
    71.   postInputEvent(event: MouseEvent | undefined): boolean {
    72.     return this.rootNode?.postInputEvent(event) as boolean
    73.   }
    74. }
    
    75. @Component
    76. struct VideoComponent {
    77.   @ObjectLink params: Params
    78.   @State bkColor: Color = Color.Red
    79.   mXComponentController: XComponentController = new XComponentController();
    80.   @State player_changed: boolean = false;
    81.   player?: AVPlayerDemo;
    
    82.   build() {
    83.     Column() {
    84.       Button(this.params.textOne)
    
    85.       XComponent({ id: 'video_player_id', type: XComponentType.SURFACE, controller: this.mXComponentController})
    86.         .border({width: 1, color: Color.Red})
    87.         .onLoad(() => {
    88.           this.player = new AVPlayerDemo();
    89.           this.player.setSurfaceID(this.mXComponentController.getXComponentSurfaceId());
    90.           this.player_changed = !this.player_changed;
    91.           this.player.avPlayerLiveDemo()
    92.         })
    93.         .width(300)
    94.         .height(200)
    95.     }
    96.     //自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    97.     .width(this.params.width)
    98.     .height(this.params.height)
    99.   }
    100. }
    101. // @Builder中为动态组件的具体组件内容。
    102. @Builder
    103. function VideoBuilder(params: Params) {
    104.   VideoComponent({ params: params })
    105.     .backgroundColor(Color.Gray)
    106. }
    
    107. @Entry
    108. @Component
    109. struct WebIndex {
    110.   browserTabController: WebviewController = new webview.WebviewController()
    111.   private nodeControllerMap: Map<string, MyNodeController> = new Map();
    112.   @State componentIdArr: Array<string> = [];
    113.   @State widthMap: Map<string, number> = new Map();
    114.   @State heightMap: Map<string, number> = new Map();
    115.   @State positionMap: Map<string, Edges> = new Map();
    116.   @State edges: Edges = {};
    117.   uiContext: UIContext = this.getUIContext();
    
    118.   aboutToAppear() {
    119.     // 配置web开启调试模式。
    120.     webview.WebviewController.setWebDebuggingAccess(true);
    121.   }
    
    122.   build(){
    123.     Row() {
    124.       Column() {
    125.         Stack() {
    126.           ForEach(this.componentIdArr, (componentId: string) => {
    127.             NodeContainer(this.nodeControllerMap.get(componentId))
    128.               .position(this.positionMap.get(componentId))
    129.               .width(this.widthMap.get(componentId))
    130.               .height(this.heightMap.get(componentId))
    131.           }, (embedId: string) => embedId)
    132.           // Web组件加载本地test.html页面。
    133.           Web({ src: $rawfile("test.html"), controller: this.browserTabController })
    134.             // 配置同层渲染开关开启。
    135.             .enableNativeEmbedMode(true)
    136.               // 获取<embed>标签的生命周期变化数据。
    137.             .onNativeEmbedLifecycleChange((embed) => {
    138.               console.info("NativeEmbed surfaceId" + embed.surfaceId);
    139.               // 1. 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
    140.               const componentId = embed.info?.id?.toString() as string
    141.               if (embed.status == NativeEmbedStatus.CREATE) {
    142.                 console.info("NativeEmbed create" + JSON.stringify(embed.info))
    143.                 // 创建节点控制器，设置参数。
    144.                 let nodeController = new MyNodeController()
    145.                 // 1. embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
    146.                 nodeController.setRenderOption({surfaceId : embed.surfaceId as string, type : embed.info?.type as string,
    147.                   renderType : NodeRenderType.RENDER_TYPE_TEXTURE, embedId : embed.embedId as string,
    148.                   width : this.uiContext.px2vp(embed.info?.width), height : this.uiContext.px2vp(embed.info?.height)})
    149.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    150.                 nodeController.setDestroy(false);
    151.                 // 根据web传入的embed的id属性作为key，将nodeController存入map。
    152.                 this.nodeControllerMap.set(componentId, nodeController)
    153.                 this.widthMap.set(componentId,  this.uiContext.px2vp(embed.info?.width));
    154.                 this.heightMap.set(componentId,  this.uiContext.px2vp(embed.info?.height));
    155.                 this.positionMap.set(componentId, this.edges);
    156.                 // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器，需要将push动作放在set之后。
    157.                 this.componentIdArr.push(componentId)
    158.               } else if (embed.status == NativeEmbedStatus.UPDATE) {
    159.                 let nodeController = this.nodeControllerMap.get(componentId)
    160.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    161.                 this.positionMap.set(componentId, this.edges);
    162.                 this.widthMap.set(componentId,  this.uiContext.px2vp(embed.info?.width));
    163.                 this.heightMap.set(componentId,  this.uiContext.px2vp(embed.info?.height));
    164.                 nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
    165.               } else if (embed.status == NativeEmbedStatus.DESTROY) {
    166.                 let nodeController = this.nodeControllerMap.get(componentId);
    167.                 nodeController?.setDestroy(true);
    168.                 this.nodeControllerMap.delete(componentId);
    169.                 this.positionMap.delete(componentId);
    170.                 this.widthMap.delete(componentId);
    171.                 this.heightMap.delete(componentId);
    172.                 this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
    173.               } else {
    174.                 console.info("NativeEmbed status" + embed.status);
    175.               }
    176.             })// 获取同层渲染组件触摸事件信息。
    177.             .onNativeEmbedGestureEvent((touch) => {
    178.               console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
    179.               this.componentIdArr.forEach((componentId: string) => {
    180.                 let nodeController = this.nodeControllerMap.get(componentId)
    181.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    182.                 if (nodeController?.getEmbedId() === touch.embedId) {
    183.                   let ret = nodeController?.postEvent(touch.touchEvent)
    184.                   if (ret) {
    185.                     console.info("onNativeEmbedGestureEvent success " + componentId)
    186.                   } else {
    187.                     console.info("onNativeEmbedGestureEvent fail " + componentId)
    188.                   }
    189.                   if (touch.result) {
    190.                     // 通知Web组件手势事件消费结果。
    191.                     touch.result.setGestureEventResult(ret);
    192.                   }
    193.                 }
    194.               })
    195.             })
    196.             .onNativeEmbedMouseEvent((mouse) => {
    197.               console.info("NativeEmbed onNativeEmbedMouseEvent" + JSON.stringify(mouse.mouseEvent));
    198.               this.componentIdArr.forEach((componentId: string) => {
    199.                 let nodeController = this.nodeControllerMap.get(componentId);
    200.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    201.                 if(nodeController?.getEmbedId() == mouse.embedId) {
    202.                   let ret = nodeController?.postInputEvent(mouse.mouseEvent)
    203.                   if(ret) {
    204.                     console.info("onNativeEmbedMouseEvent success " + componentId);
    205.                   } else {
    206.                     console.info("onNativeEmbedMouseEvent fail " + componentId);
    207.                   }
    208.                   if(mouse.result) {
    209.                     // 通知Web组件鼠标事件消费结果。
    210.                     mouse.result.setMouseEventResult(ret);
    211.                   }
    212.                 }
    213.               })
    214.             })
    215.         }
    216.       }
    217.     }
    218.   }
    219. }
    
- 应用侧代码示例，视频播放，使用时需替换为正确的视频链接地址。
    
    1. // HAP's src/main/ets/pages/PlayerDemo.ets
    2. import { media } from '@kit.MediaKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. export class AVPlayerDemo {
    5.   private count: number = 0;
    6.   private surfaceID: string = ''; // surfaceID用于播放画面显示，具体的值需要通过Xcomponent接口获取，相关文档链接见上面Xcomponent创建方法。
    7.   private isSeek: boolean = true; // 用于区分模式是否支持seek操作。
    
    8.   setSurfaceID(surface_id: string){
    9.     console.info('setSurfaceID : ' + surface_id);
    10.     this.surfaceID = surface_id;
    11.   }
    12.   // 注册avplayer回调函数。
    13.   setAVPlayerCallback(avPlayer: media.AVPlayer) {
    14.     // seek操作结果回调函数。
    15.     avPlayer.on('seekDone', (seekDoneTime: number) => {
    16.       console.info(`AVPlayer seek succeeded, seek time is ${seekDoneTime}`);
    17.     })
    18.     // error回调监听函数，当avplayer在操作过程中出现错误时，调用reset接口触发重置流程。
    19.     avPlayer.on('error', (err: BusinessError) => {
    20.       console.error(`Invoke avPlayer failed, code is ${err.code}, message is ${err.message}`);
    21.       avPlayer.reset();
    22.     })
    23.     // 状态机变化回调函数。
    24.     avPlayer.on('stateChange', async (state: string, reason: media.StateChangeReason) => {
    25.       switch (state) {
    26.         case 'idle': // 成功调用reset接口后触发该状态机上报。
    27.           console.info('AVPlayer state idle called.');
    28.           avPlayer.release(); // 调用release接口销毁实例对象。
    29.           break;
    30.         case 'initialized': // avplayer 设置播放源后触发该状态上报。
    31.           console.info('AVPlayer state initialized called.');
    32.           avPlayer.surfaceId = this.surfaceID; // 设置显示画面，当播放的资源为纯音频时无需设置。
    33.           avPlayer.prepare();
    34.           break;
    35.         case 'prepared': // prepared调用成功后上报该状态机。
    36.           console.info('AVPlayer state prepared called.');
    37.           avPlayer.play(); // 调用播放接口开始播放。
    38.           break;
    39.         case 'playing': // play成功调用后触发该状态机上报。
    40.           console.info('AVPlayer state playing called.');
    41.           if(this.count !== 0) {
    42.             if (this.isSeek) {
    43.               console.info('AVPlayer start to seek.');
    44.               avPlayer.seek(avPlayer.duration); // seek到视频末尾。
    45.             } else {
    46.               // 当播放模式不支持seek操作时继续播放到结尾。
    47.               console.info('AVPlayer wait to play end.');
    48.             }
    49.           } else {
    50.             avPlayer.pause(); // 调用暂停接口暂停播放。
    51.           }
    52.           this.count++;
    53.           break;
    54.         case 'paused': // pause成功调用后触发该状态机上报。
    55.           console.info('AVPlayer state paused called.');
    56.           avPlayer.play(); // 再次播放接口开始播放。
    57.           break;
    58.         case 'completed': //播放接口后触发该状态机上报。
    59.           console.info('AVPlayer state completed called.');
    60.           avPlayer.stop(); // 调用播放接口。
    61.           break;
    62.         case 'stopped': // stop接口后触发该状态机上报。
    63.           console.info('AVPlayer state stopped called.');
    64.           avPlayer.reset(); // 调用reset接口初始化avplayer状态。
    65.           break;
    66.         case 'released': //播放接口后触发该状态机上报。
    67.           console.info('AVPlayer state released called.');
    68.           break;
    69.         default:
    70.           break;
    71.       }
    72.     })
    73.   }
    
    74.   // 通过url设置网络地址来实现播放直播码流。
    75.   async avPlayerLiveDemo(){
    76.     // 创建avPlayer实例对象。
    77.     let avPlayer: media.AVPlayer = await media.createAVPlayer();
    78.     // 创建状态机变化回调函数。
    79.     this.setAVPlayerCallback(avPlayer);
    80.     this.isSeek = false; // 不支持seek操作。
    81.     // 使用时需要自行替换视频链接。
    82.     avPlayer.url = 'https://xxx.xxx/demo.mp4';
    83.   }
    84. }
    
- 前端页面示例。
    
    1. <!--HAP's src/main/resources/rawfile/test.html-->
    2. <!DOCTYPE html>
    3. <html>
    4. <head>
    5.     <title>同层渲染测试html</title>
    6.     <meta name="viewport">
    7. </head>
    8. <body>
    9. <div>
    10.     <div id="bodyId">
    11.         <embed id="nativeVideo" type = "native/video" width="1000" height="1500" src="test" style = "background-color:red"/>
    12.     </div>
    13. </div>
    14. </body>
    15. </html>
    
- 实现效果：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.00295511658418628925105587767525:50001231000000:2800:0CFDD88168381CD70C6C15BAF9CDF5E0236275B71020AF9ED3E1771C0179C7A3.png)
    

## 同层标签设置为最高层级

同层渲染支持私有属性arkwebnativestyle，该属性仅在开启同层渲染后的<embed>和<object>中生效，该属性的display属性用于控制同层标签的显示层级，使其高于其他Web元素。如果多个同层标签都设置了arkwebnativestyle的display属性，并且属性相同，则它们的层级顺序将遵循W3C标准层级排序规则：先比较z-index属性值，当z-index相同时，按照元素在DOM中的先后顺序排序。display属性取值说明如下：

|display取值|说明|
|:--|:--|
|overlay|设置同层标签层级高于其他Web元素。|
|overlay-infinity|设置同层标签层级高于其他Web元素和设置overlay的同层标签。|

- 应用侧代码：
    
    1. import { webview } from '@kit.ArkWeb';
    2. import { UIContext } from '@kit.ArkUI';
    3. import { NodeController, BuilderNode, NodeRenderType, FrameNode } from '@kit.ArkUI';
    
    4. @Observed
    5. declare class Params{
    6.   elementId: string
    7.   textOne: string
    8.   textTwo: string
    9.   width: number
    10.   height: number
    11. }
    
    12. declare class NodeControllerParams {
    13.   surfaceId: string
    14.   type: string
    15.   renderType: NodeRenderType
    16.   embedId: string
    17.   width: number
    18.   height: number
    19. }
    
    20. // 用于控制和反馈对应的NodeContainer上的节点的行为，需要与NodeContainer一起使用。
    21. class MyNodeController extends NodeController {
    22.   private rootNode: BuilderNode<[Params]> | undefined | null;
    23.   private embedId_: string = "";
    24.   private surfaceId_: string = "";
    25.   private renderType_: NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
    26.   private width_: number = 0;
    27.   private height_: number = 0;
    28.   private type_: string = "";
    29.   private isDestroy_: boolean = false;
    
    30.   setRenderOption(params: NodeControllerParams) {
    31.     this.surfaceId_ = params.surfaceId;
    32.     this.renderType_ = params.renderType;
    33.     this.embedId_ = params.embedId;
    34.     this.width_ = params.width;
    35.     this.height_ = params.height;
    36.     this.type_ = params.type;
    37.   }
    
    38.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
    39.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
    40.   makeNode(uiContext: UIContext): FrameNode | null {
    41.     if (this.isDestroy_) { // rootNode为null。
    42.       return null;
    43.     }
    44.     if (!this.rootNode) {// rootNode 为undefined时。
    45.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_ });
    46.       if (this.type_ == 'native/view1') {
    47.         this.rootNode.build(wrapBuilder(TextInputBuilder1), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
    48.         return this.rootNode.getFrameNode();
    49.       } else if (this.type_ == 'native/view2') {
    50.         this.rootNode.build(wrapBuilder(TextInputBuilder2), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
    51.         return this.rootNode.getFrameNode();
    52.       } else{
    53.         return null;
    54.       }
    55.     }
    56.     // 返回FrameNode节点。
    57.     return this.rootNode.getFrameNode();
    58.   }
    
    59.   updateNode(arg: Object): void {
    60.     this.rootNode?.update(arg);
    61.   }
    
    62.   getEmbedId(): string {
    63.     return this.embedId_;
    64.   }
    
    65.   setDestroy(isDestroy: boolean): void {
    66.     this.isDestroy_ = isDestroy;
    67.     if (this.isDestroy_) {
    68.       this.rootNode = null;
    69.     }
    70.   }
    
    71.   postEvent(event: TouchEvent | undefined): boolean {
    72.     return this.rootNode?.postTouchEvent(event) as boolean
    73.   }
    74. }
    
    75. @Component
    76. struct TextInputComponent1 {
    77.   @Prop params: Params;
    78.   @State bkColor: Color = Color.White;
    
    79.   build() {
    80.     Column() {
    81.       Text("display:overlay-infinity")
    82.       TextInput({text: '', placeholder: 'please input your word...'})
    83.         .placeholderColor(Color.Gray)
    84.         .id(this.params?.elementId)
    85.         .placeholderFont({size: 13, weight: 400})
    86.         .caretColor(Color.Gray)
    87.         .fontSize(14)
    88.         .fontColor(Color.Black)
    89.     }
    90.     // 自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    91.     .width(this.params.width)
    92.     .height(this.params.height)
    93.   }
    94. }
    
    95. // @Builder中为动态组件的具体组件内容。
    96. @Builder
    97. function TextInputBuilder1(params:Params) {
    98.   TextInputComponent1({params: params})
    99.     .width(params.width)
    100.     .height(params.height)
    101.     .backgroundColor(Color.Pink)
    102. }
    
    103. @Component
    104. struct TextInputComponent2 {
    105.   @Prop params: Params;
    106.   @State bkColor: Color = Color.White;
    
    107.   build() {
    108.     Column() {
    109.       Text("display:overlay")
    110.       TextInput({text: '', placeholder: 'please input your word...'})
    111.         .placeholderColor(Color.Gray)
    112.         .id(this.params?.elementId)
    113.         .placeholderFont({size: 13, weight: 400})
    114.         .caretColor(Color.Gray)
    115.         .fontSize(14)
    116.         .fontColor(Color.Black)
    117.     }
    118.     // 自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    119.     .width(this.params.width)
    120.     .height(this.params.height)
    121.   }
    122. }
    
    123. // @Builder中为动态组件的具体组件内容。
    124. @Builder
    125. function TextInputBuilder2(params:Params) {
    126.   TextInputComponent2({params: params})
    127.     .width(params.width)
    128.     .height(params.height)
    129.     .backgroundColor(Color.Gray)
    130. }
    
    131. @Entry
    132. @Component
    133. struct Page{
    134.   browserTabController: webview.WebviewController = new webview.WebviewController();
    135.   private nodeControllerMap: Map<string, MyNodeController> = new Map();
    136.   @State componentIdArr: Array<string> = [];
    137.   @State widthMap: Map<string, number> = new Map();
    138.   @State heightMap: Map<string, number> = new Map();
    139.   @State positionMap: Map<string, Edges> = new Map();
    140.   @State edges: Edges = {};
    141.   uiContext: UIContext = this.getUIContext();
    
    142.   build() {
    143.     Row() {
    144.       Column() {
    145.         Stack() {
    146.           ForEach(this.componentIdArr, (componentId: string) => {
    147.             NodeContainer(this.nodeControllerMap.get(componentId))
    148.               .position(this.positionMap.get(componentId))
    149.               .width(this.widthMap.get(componentId))
    150.               .height(this.heightMap.get(componentId))
    151.           }, (embedId: string) => embedId)
    152.           // Web组件加载本地text.html页面。
    153.           Web({src: $rawfile("overlay.html"), controller: this.browserTabController})
    154.             // 配置同层渲染开关开启。
    155.             .enableNativeEmbedMode(true)
    156.               // 获取<embed>标签的生命周期变化数据。
    157.             .onNativeEmbedLifecycleChange((embed) => {
    158.               console.info("NativeEmbed surfaceId" + embed.surfaceId);
    159.               // 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
    160.               const componentId = embed.info?.id?.toString() as string
    161.               if (embed.status == NativeEmbedStatus.CREATE) {
    162.                 console.info("NativeEmbed create" + JSON.stringify(embed.info));
    163.                 // 创建节点控制器、设置参数。
    164.                 let nodeController = new MyNodeController()
    165.                 // embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
    166.                 nodeController.setRenderOption({surfaceId : embed.surfaceId as string,
    167.                   type : embed.info?.type as string,
    168.                   renderType : NodeRenderType.RENDER_TYPE_TEXTURE,
    169.                   embedId : embed.embedId as string,
    170.                   width : this.uiContext.px2vp(embed.info?.width),
    171.                   height : this.uiContext.px2vp(embed.info?.height)})
    172.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    173.                 nodeController.setDestroy(false);
    174.                 // 根据web传入的embed的id属性作为key，将nodeController存入Map。
    175.                 this.nodeControllerMap.set(componentId, nodeController);
    176.                 this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    177.                 this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    178.                 this.positionMap.set(componentId, this.edges);
    179.                 // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器,需要将push动作放在set之后。
    180.                 this.componentIdArr.push(componentId)
    181.               } else if (embed.status == NativeEmbedStatus.UPDATE) {
    182.                 let nodeController = this.nodeControllerMap.get(componentId);
    183.                 console.info("NativeEmbed update" + JSON.stringify(embed));
    184.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    185.                 this.positionMap.set(componentId, this.edges);
    186.                 this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    187.                 this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    188.                 nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
    189.               } else if (embed.status == NativeEmbedStatus.DESTROY) {
    190.                 console.info("NativeEmbed destroy" + JSON.stringify(embed));
    191.                 let nodeController = this.nodeControllerMap.get(componentId);
    192.                 nodeController?.setDestroy(true);
    193.                 this.nodeControllerMap.delete(componentId);
    194.                 this.positionMap.delete(componentId);
    195.                 this.widthMap.delete(componentId);
    196.                 this.heightMap.delete(componentId);
    197.                 this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
    198.               } else {
    199.                 console.info("NativeEmbed status" + embed.status);
    200.               }
    201.             })// 获取同层渲染组件触摸事件信息。
    202.             .onNativeEmbedGestureEvent((touch) => {
    203.               console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
    204.               this.componentIdArr.forEach((componentId: string) => {
    205.                 let nodeController = this.nodeControllerMap.get(componentId);
    206.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    207.                 if(nodeController?.getEmbedId() == touch.embedId) {
    208.                   let ret = nodeController?.postEvent(touch.touchEvent)
    209.                   if(ret) {
    210.                     console.info("onNativeEmbedGestureEvent success " + componentId);
    211.                   } else {
    212.                     console.info("onNativeEmbedGestureEvent fail " + componentId);
    213.                   }
    214.                   if(touch.result) {
    215.                     // 通知Web组件手势事件消费结果。
    216.                     touch.result.setGestureEventResult(ret);
    217.                   }
    218.                 }
    219.               })
    220.             })
    221.             .border({width: 2, color: Color.Gray})
    222.             .height("50%")
    223.         }
    224.       }
    225.     }
    226.   }
    227. }
    
- 前端页面示例：
    
    示例代码使用<embed>标签，若使用<object>标签，请在ets侧注册<object>标签及type类型。
    
    1. <!--HAP's src/main/resources/rawfile/overlay.html-->
    2. <!DOCTYPE html>
    3. <html>
    4. <head>
    5.     <title>同层渲染html</title>
    6.     <meta name="viewport" content="initial-scale=1.0">
    7. </head>
    8. <body>
    9. <div>
    10.     <div id = "test" style = "position: absolute; z-index: 9999; text-align: center; background-color: rgb(61, 157, 180); top: 40px; left: 30px; width: 300px; height: 120px">
    11.         z-index: 9999
    12.     </div>
    
    13.     <embed id = "input1" type = "native/view1" arkwebnativestyle = "display:overlay-infinity" style = "position: absolute; top: 60px; left: 50px; width: 300px; height: 100px">
    
    14.     <embed id = "input2" type = "native/view2" arkwebnativestyle = "display:overlay" style = "position: absolute; top: 150px; left: 40px; width: 300px; height: 100px">
    15. </div>
    16. </body>
    17. </html>
    
- 实现效果：
    
    未设置arkwebnativestyle的display属性：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.85292742076939813175949351475763:50001231000000:2800:9B6F3259AB7E58279A343B2B510E836CC06121C5F7078AFF9A8F78803C4D93A5.png)
    
    设置arkwebnativestyle的display属性：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.19737308615704125441553207620616:50001231000000:2800:621D5728E84211C8BC104F987F79AC0CA8071962CF0D6418F339B5978651B465.png)
    

## 常见问题

### 同层渲染组件被拉伸该如何解决？

- 组件高度过大
    
    受GPU限制，同层标签存在8000px的高度限制，如果html5中同层标签高度过高，会存在组件被拉伸的情况，这时需要将同层标签的高度设为8000px以下。
    
- 自定义组件宽高未指定为同层渲染标签的宽高
    
    自定义的同层渲染组件宽高需要与同层标签的宽高保持一致，示例如下：
    
    1.   @Component
    2.   struct TextInputComponent {
    3.     @Prop params: Params
    4.     @State bkColor: Color = Color.White
    
    5.     build() {
    6.       Column() {
    7.         TextInput({text: '', placeholder: 'please input your word...'})
    8.           .fontColor(Color.Black)
    9.       }
    10.       // 自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    11.       .width(this.params.width)
    12.       .height(this.params.height)
    13.     }
    14.   }
    

### 如何将同层渲染组件捕获到的事件透传到web前端？

同层渲染手势事件通过[setGestureEventResult()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-eventresult#setgestureeventresult14)设置手势事件消费结果，可以选择系统组件侧或ArkWeb侧消费手势事件。如果要实现系统组件侧和ArkWeb侧同时消费手势事件，可以在[setGestureEventResult()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-eventresult#setgestureeventresult14)中将stopPropagation设置为false，即系统组件侧消费的同时可以将手势事件向上冒泡给ArkWeb。

### 同层渲染页面显示该插件不支持该如何解决？

- 同层渲染开关[enableNativeEmbedMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#enablenativeembedmode11)未开启
    
    使用同层渲染技术需要显式开启同层渲染开关
    
    1. Web({ src: $rawfile("text.html"), controller: this.controller })
    2.   // 配置同层渲染开关开启。
    3.   .enableNativeEmbedMode(true)
    
- 同层标签使用有误
    
    如果使用<embed>标签，需要显式书写embed，并且type类型以"native/"开头；如果使用<object>标签，需要注册<object>标签及type类型。
    

### 涉及界面交互的ArkUI组件（如TextInput等）光标与输入框错位该如何解决？

首先，需使用Stack包裹同层组件容器和BuilderNode。其次，同层组件容器NodeContainer应与同层标签的位置绑定。示例如下：

1. ForEach(this.componentIdArr, (componentId: string) => {
2.   NodeContainer(this.nodeControllerMap.get(componentId))
3.     // 同层组件容器应与同层标签的宽高和位置绑定。
4.     .position(this.positionMap.get(componentId))
5.     .width(this.widthMap.get(componentId))
6.     .height(this.heightMap.get(componentId))
7. }, (embedId: string) => embedId)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-data-detector "使用Web组件的智能分词能力")
# 同层渲染

更新时间: 2025-12-16 16:38

在系统中，应用可以使用Web组件加载Web网页。当非系统框架的UI组件功能或性能不如系统组件时，可使用同层渲染技术，通过ArkUI组件渲染这些组件（简称为同层组件）。

## 使用场景

### Web网页

小程序的地图组件，可以使用ArkUI的XComponent组件渲染来提升性能。小程序的输入框组件，可以使用ArkUI的TextInput组件渲染，达到与系统应用一致的输入体验。

- 在网页侧，应用开发者可将<embed>、<object>的网页UI组件（简称为同层标签），按一定规则进行同层渲染，详细规格见同层渲染规格小节。
    
- 在应用侧，应用开发者可以通过Web组件的同层渲染事件上报接口，感知到H5同层标签的生命周期以及输入事件，进行同层渲染组件的相应业务逻辑处理。
    
- 在应用侧，应用开发者可以使用ArkUI的NodeContainer等接口，构建H5同层标签对应的同层渲染组件。可支持同层渲染的ArkUI常用组件包括：[TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput), [XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent), [Canvas](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-canvas-canvas), [Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video), [Web](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)。具体规格可参见[同层渲染规格小节](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-same-layer#%E8%A7%84%E6%A0%BC%E7%BA%A6%E6%9D%9F)。
    

### 三方UI框架

Flutter提供了PlatformView与Texture抽象组件，这些组件可使用系统组件渲染，用于支持Flutter组件功能不足的部分。Weex2.0框架的Camera、Video和Canvas组件可以使用系统组件渲染，以增强功能和性能。

- 在三方框架页面侧，由于Flutter、Weex等三方框架不在操作系统范围内，本文不列举可被同层渲染的三方框架UI组件的范围与使用方式。
    
- 在应用侧，应用开发者可以使用ArkUI的NodeContainer等接口，构建三方框架同层标签对应的同层渲染组件。可支持同层渲染的ArkUI常用组件包括：[TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput), [XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent), [Canvas](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-canvas-canvas), [Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video), [Web](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)。具体规格可参见[同层渲染规格](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-same-layer#%E8%A7%84%E6%A0%BC%E7%BA%A6%E6%9D%9F)。
    

## 整体架构

ArkWeb同层渲染特性主要提供两种能力：同层标签生命周期和事件命中转发处理。

同层标签生命周期主要关联前端标签（<embed>/<object>），同时命中到同层标签的事件会被上报到开发者侧，由开发者分发到对应组件树。整体框架如下图所示：

**图1** 同层渲染整体架构

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.39410890836484253361083841709687:50001231000000:2800:6C89848D97E0DC98FDAEED734576663B8B0268882EE5205B6F2205A0F127BB09.png)

## 规格约束

### 可被同层渲染的ArkUI组件

以下规格对Web网页和三方框架场景均生效。

**支持的组件范围:**

- 基础组件：[AlphabetIndexer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-alphabet-indexer), [Blank](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-blank), [Button](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-button), [CalendarPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-calendarpicker), [Checkbox](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-checkbox), [CheckboxGroup](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-checkboxgroup), [ContainerSpan](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-containerspan), [DataPanel](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-datapanel), [DatePicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-datepicker), [Divider](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-divider), [Gauge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-gauge), [Hyperlink](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-hyperlink), [Image](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-image), [ImageAnimator](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-imageanimator), [ImageSpan](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-imagespan), [LoadingProgress](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-loadingprogress), [Marquee](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-marquee), [PatternLock](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-patternlock), [Progress](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-progress), [QRCode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-qrcode), [Radio](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-radio), [Rating](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-rating), [Refresh](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-refresh), [ScrollBar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-scroll), [Search](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-search), [Span](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-span), [Select](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-select), [Slider](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-slider), [Text](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-text), [TextArea](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textarea), [TextClock](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textclock), [TextInput](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textinput), [TextPicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-textpicker), [TextTimer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-texttimer), [TimePicker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-timepicker), [Toggle](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-toggle)
    
- 容器类组件：[Badge](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-badge), [Column](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-column), [ColumnSplit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-columnsplit), [Counter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-counter), [Flex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-flex), [GridCol](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-gridcol), [GridRow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-gridrow), [Grid](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-grid), [GridItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-griditem)，[List](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-list), [ListItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-listitem), [ListItemGroup](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-listitemgroup), [RelativeContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-relativecontainer), [Row](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-row), [RowSplit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-rowsplit), [Scroll](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-scroll), [Stack](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-stack), [Swiper](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-swiper), [Tabs](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabs), [TabContent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-tabcontent), [NodeContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-nodecontainer), [SideBarContainer](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-sidebarcontainer), [Stepper](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-stepper), [StepperItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-stepperitem), [WaterFlow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-waterflow), [FlowItem](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-container-flowitem)
    
- 自绘制类组件：[XComponent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-xcomponent), [Canvas](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-canvas-canvas), [Video](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-media-components-video), [Web](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web)
    
- 命令式自定义绘制节点：[BuilderNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-buildernode), [ComponentContent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-componentcontent), [ContentSlot](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-components-contentslot), [FrameNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-framenode), [Graphics](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-graphics), [NodeController](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-nodecontroller), [RenderNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-rendernode), [XComponentNode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-xcomponentnode), [AttributeUpdater](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-arkui-attributeupdater), [CAPI](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-arkui-nativemodule)（支持同层渲染的组件范围同ArkTS）
    

**支持的组件通用属性与事件:**

- 不支持的通用属性：[分布式迁移标识](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-restoreid)，[特效绘制合并](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-use-effect)。
    
- 其他未明确标注不支持的属性与事件及组件能力，均默认支持。
    

### Web网页的同层渲染标签

此规格仅针对Web网页，不适用于三方框架场景。

如果应用需要在Web组件加载的网页中使用同层渲染，需要按照以下规格将网页中的<embed>、<object>标签指定为同层渲染组件。

**支持的H5标签：**

- 支持<embed>标签：在开启同层渲染后，仅支持type类型为native前缀的标签识别为同层组件，不支持自定义属性。
    
- 支持<object>标签：在开启同层渲染后，支持将非标准MIME type的object标签识别为同层组件，支持通过param/value的自定义属性解析。
    
- 不支持W3C规范标准标签（如<input>、<video>）定义为同层标签。
    
- 不支持同时配置<object>标签和<embed>标签作为同层标签。
    
- 标签类型只支持英文字符，不区分大小写。
    

**同层标签支持的css属性：**

display，position，z-index，visibility，opacity, background-color，background-image，width，height，padding，padding-left，padding-top，padding-right，padding-bottom，margin，margin-left，margin-top，margin-right，margin-bottom，border-width，border-style，border-color，border-left-width，border-left-style，border-left-color，border-top-width，border-top-style，border-top-color，border-right-width，border-right-style，border-right-color，border-bottom-width，border-bottom-style，border-bottom-color，border-left，border-right，border-top，border-bottom，border，border-top-left-radius，border-top-right-radius，border-bottom-left-radius，border-bottom-right-radius，border-radius，transition，transform（仅支持translate/scale，scale对应参数只支持大于等于0的值）

除上面支持的css属性范围，其他的css属性均不保证符合预期，比如transform属性中的rotate，skew等。

**同层标签的生命周期管理：**

当同层标签生命周期变化时触发[onNativeEmbedLifecycleChange()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedlifecyclechange11)回调。

- 支持创建、销毁、位置宽高变化。
    
- 支持同层组件所在Web页面进入前进后退缓存。
    

**同层标签的输入事件分发处理：**

- 支持触摸事件TouchEvent的DOWN/UP/MOVE/CANCEL。支持[配置触摸事件消费结果](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedgestureevent11)，默认为应用侧消费。
    
- 不支持同层标签所在的应用页面缩放和[initialScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#initialscale9)、[zoom](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#zoom)、[zoomIn](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#zoomin)、[zoomOut](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#zoomout)等缩放接口。
    
- 暂不支持鼠标、键盘、触摸板事件上报。
    
- 支持默认将鼠标和触摸板左键事件（MousePress/MouseRelease/MouseMOVE）转换为触摸事件（TouchDOWN/TouchUP/TouchMOVE）上报。
    

**同层标签的可见状态变化：**

当同层标签可见状态变化时触发[onNativeEmbedVisibilityChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedvisibilitychange12)回调。

- 支持同层标签相对于视口的可见状态上报。
    
- 默认不支持由于同层标签CSS样式或尺寸变化导致的可见状态变化上报，具体规格参考[onNativeEmbedVisibilityChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedvisibilitychange12)。
    

**同层渲染<object>标签内嵌param元素状态变化：**

当同层渲染<object>内嵌标签param元素变化时触发[onNativeEmbedObjectParamChange()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedobjectparamchange21)回调。

- 支持上报param元素的增加、修改、删除三种状态变化。
    
- 接口每次最多上报500个param元素变化信息，超出部分将分多次上报。
    
- 详细上报信息参考[NativeEmbedParamDataInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-i#nativeembedparamdatainfo21)。
    

**约束限制：**

- Web页面内同层标签数量应控制在5个以内。超过5个，渲染性能将会下降。
    
- 受GPU限制，同层标签最大高度不超过8000px，最大纹理大小为8000px。
    
- 开启同层渲染后，Web组件打开的所有Web页面将不支持同步渲染模式[RenderMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-e#rendermode12)。
    
- Video组件：在非全屏Video变为全屏时，Video组件变为非纹理导出模式，视频播放状态保持延续；恢复为非全屏时，变为纹理导出模式，视频播放状态保持延续。
    
- Web组件：仅支持一层同层渲染嵌套，不支持多层同层渲染嵌套。输入事件只支持滑动、点击、长按，不支持拖拽、旋转、缩放。
    
- 涉及界面交互的ArkUI组件（如TextInput等）：建议在页面布局中使用Stack包裹同层组件容器与BuilderNode，并使两者位置一致，NodeContainer要与<embed>/<object>标签对齐，以保障组件正常交互。如两者位置不一致，可能出现的问题有：TextInput/TextArea等附属的文本选择框位置错位（如下图）、LoadingProgress/Marquee等组件的动画启停与组件可见状态不匹配。
    
    **图2** 未使用Stack包裹，TextInput的位置错位
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.83659815536941758218255870630249:50001231000000:2800:2DF8EFA2ECC43F8D29A1B340A2DDD7F0D18E4BA0959C8B74C8A2E140E207DFDC.png)
    
    **图3** 使用Stack包裹，TextInput的位置正常
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.99416238214956841185269338927042:50001231000000:2800:0CC8EBF4568814B454ECF1C19B0740351F24C92088FFE630FAA656FB2C2D20C8.png)
    

## Web页面中同层渲染输入框

在Web页面中，可以使用ArkUI系统的TextInput组件进行同层渲染。此处利用同层渲染展示三个输入框，渲染效果图如下：

**图4** 同层渲染输入框

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.64649427145049818214449563250542:50001231000000:2800:14959B3CEB3EAE584B8D691B4A2F57E4621BFBF925419AE2FBFC012B465AFAFE.png)

1. 在Web页面中标记需要同层渲染的HTML标签。
    
    同层渲染支持<embed>/<object>两种标签。type类型可任意指定，两个字符串参数均不区分大小写，ArkWeb内核将会统一转换为小写。其中，tag字符串使用全字符串匹配，type使用字符串前缀匹配。
    
    若开发者不使用该接口或该接口接收的为非法字符串（空字符串）时，ArkWeb内核将使用默认设置，即"embed" + "native/"前缀模式。若指定类型与w3c定义的<embed>或<object>标准类型重合，如registerNativeEmbedRule("object", "application/pdf")，ArkWeb将遵循w3c标准行为，不会将其识别为同层标签。
    
    - 采用<embed>标签。
        
        1. <!--HAP's src/main/resources/rawfile/text.html-->
        2. <!DOCTYPE html>
        3. <html>
        4. <head>
        5.     <title>同层渲染html</title>
        6.     <meta name="viewport">
        7. </head>
        
        8. <body style="background:white">
        
        9. <embed id = "input1" type="native/view" style="width: 100%; height: 100px; margin: 30px; margin-top: 600px"/>
        
        10. <embed id = "input2" type="native/view2" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"/>
        
        11. <embed id = "input3" type="native/view3" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"/>
        
        12. </body>
        13. </html>
        
    - 采用<object>标签。
        
        需要使用registerNativeEmbedRule注册object标签。
        
        1. // ...
        2. Web({src: $rawfile("text.html"), controller: this.browserTabController})
        3.   // 注册同层标签为"object"，类型为"test"前缀。
        4.   .registerNativeEmbedRule("object", "test")
        5.   // ...
        
        与registerNativeEmbedRule相对应的前端页面代码，类型可使用"test"及以"test"为前缀的字串。
        
        6. <!--HAP's src/main/resources/rawfile/text.html-->
        7. <!DOCTYPE html>
        8. <html>
        9. <head>
        10.     <title>同层渲染html</title>
        11.     <meta name="viewport">
        12. </head>
        
        13. <body style="background:white">
        
        14. <object id = "input1" type="test/input" style="width: 100%; height: 100px; margin: 30px; margin-top: 600px"></object>
        
        15. <object id = "input2" type="test/input" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"></object>
        
        16. <object id = "input3" type="test/input" style="width: 100%; height: 100px; margin: 30px; margin-top: 50px"></object>
        
        17. </body>
        18. </html>
        
2. 在应用侧开启同层渲染功能。
    
    同层渲染功能默认不开启，如果要使用同层渲染的功能，可通过[enableNativeEmbedMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#enablenativeembedmode11)来开启。
    
    1. // xxx.ets
    2. import { webview } from '@kit.ArkWeb';
    3. @Entry
    4. @Component
    5. struct WebComponent {
    6.   controller: webview.WebviewController = new webview.WebviewController();
    
    7.   build() {
    8.     Column() {
    9.       Web({ src: 'www.example.com', controller: this.controller })
    10.         // 配置同层渲染开关开启。
    11.         .enableNativeEmbedMode(true)
    12.     }
    13.   }
    14. }
    
3. 创建自定义组件。
    
    同层渲染功能开启后，展示在对应区域的系统组件。
    
    1. @Component
    2. struct TextInputComponent {
    3.   @Prop params: Params
    4.   @State bkColor: Color = Color.White
    
    5.   build() {
    6.     Column() {
    7.       TextInput({text: '', placeholder: 'please input your word...'})
    8.         .placeholderColor(Color.Gray)
    9.         .id(this.params?.elementId)
    10.         .placeholderFont({size: 13, weight: 400})
    11.         .caretColor(Color.Gray)
    12.         .width(this.params?.width)
    13.         .height(this.params?.height)
    14.         .fontSize(14)
    15.         .fontColor(Color.Black)
    16.     }
    17.     //自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    18.     .width(this.params.width)
    19.     .height(this.params.height)
    20.   }
    21. }
    
    22. @Builder
    23. function TextInputBuilder(params:Params) {
    24.   TextInputComponent({params: params})
    25.     .width(params.width)
    26.     .height(params.height)
    27.     .backgroundColor(Color.White)
    28. }
    
4. 创建节点控制器。
    
    用于控制和反馈对应NodeContainer上的节点行为。
    
    1. class MyNodeController extends NodeController {
    2.   private rootNode: BuilderNode<[Params]> | undefined | null;
    3.   private embedId_: string = "";
    4.   private surfaceId_: string = "";
    5.   private renderType_: NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
    6.   private width_: number = 0;
    7.   private height_: number = 0;
    8.   private type_: string = "";
    9.   private isDestroy_: boolean = false;
    
    10.   setRenderOption(params: NodeControllerParams) {
    11.     this.surfaceId_ = params.surfaceId;
    12.     this.renderType_ = params.renderType;
    13.     this.embedId_ = params.embedId;
    14.     this.width_ = params.width;
    15.     this.height_ = params.height;
    16.     this.type_ = params.type;
    17.   }
    
    18.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
    19.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
    20.   makeNode(uiContext: UIContext): FrameNode | null {
    21.     if (this.isDestroy_) { // rootNode为null。
    22.       return null;
    23.     }
    24.     if (!this.rootNode) {// rootNode 为undefined时。
    25.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_ });
    26.       if(this.rootNode) {
    27.         this.rootNode.build(wrapBuilder(TextInputBuilder), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
    28.         return this.rootNode.getFrameNode();
    29.       }else{
    30.         return null;
    31.       }
    32.     }
    33.     // 返回FrameNode节点。
    34.     return this.rootNode.getFrameNode();
    35.   }
    
    36.   updateNode(arg: Object): void {
    37.     this.rootNode?.update(arg);
    38.   }
    
    39.   getEmbedId(): string {
    40.     return this.embedId_;
    41.   }
    
    42.   setDestroy(isDestroy: boolean): void {
    43.     this.isDestroy_ = isDestroy;
    44.     if (this.isDestroy_) {
    45.       this.rootNode = null;
    46.     }
    47.   }
    
    48.   postEvent(event: TouchEvent | undefined): boolean {
    49.     return this.rootNode?.postTouchEvent(event) as boolean
    50.   }
    51. }
    
5. 监听同层渲染的生命周期变化。
    
    开启该功能后，当网页中存在同层渲染支持的标签时，ArkWeb内核会触发由[onNativeEmbedLifecycleChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedlifecyclechange11)注册的回调函数。
    
    开发者则需要调用[onNativeEmbedLifecycleChange](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedlifecyclechange11)来监听同层渲染标签的生命周期变化。
    
    1. build() {
    2.   Row() {
    3.     Column() {
    4.       Stack() {
    5.         ForEach(this.componentIdArr, (componentId: string) => {
    6.           NodeContainer(this.nodeControllerMap.get(componentId))
    7.             .position(this.positionMap.get(componentId))
    8.             .width(this.widthMap.get(componentId))
    9.             .height(this.heightMap.get(componentId))
    10.         }, (embedId: string) => embedId)
    11.         // Web组件加载本地text.html页面。
    12.         Web({src: $rawfile("text.html"), controller: this.browserTabController})
    13.           // 配置同层渲染开关开启。
    14.           .enableNativeEmbedMode(true)
    15.             // 注册同层标签为<object>，类型为"test"前缀。
    16.           .registerNativeEmbedRule("object", "test")
    17.             // 获取<embed>标签的生命周期变化数据。
    18.           .onNativeEmbedLifecycleChange((embed) => {
    19.             console.info("NativeEmbed surfaceId" + embed.surfaceId);
    20.             // 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
    21.             const componentId = embed.info?.id?.toString() as string
    22.             if (embed.status == NativeEmbedStatus.CREATE) {
    23.               console.info("NativeEmbed create" + JSON.stringify(embed.info));
    24.               // 创建节点控制器、设置参数。
    25.               let nodeController = new MyNodeController()
    26.               // embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
    27.               nodeController.setRenderOption({surfaceId : embed.surfaceId as string,
    28.                 type : embed.info?.type as string,
    29.                 renderType : NodeRenderType.RENDER_TYPE_TEXTURE,
    30.                 embedId : embed.embedId as string,
    31.                 width : this.uiContext.px2vp(embed.info?.width),
    32.                 height : this.uiContext.px2vp(embed.info?.height)})
    33.               this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    34.               nodeController.setDestroy(false);
    35.               //根据web传入的embed的id属性作为key，将nodeController存入Map。
    36.               this.nodeControllerMap.set(componentId, nodeController);
    37.               this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    38.               this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    39.               this.positionMap.set(componentId, this.edges);
    40.               // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器,需要将push动作放在set之后。
    41.               this.componentIdArr.push(componentId)
    42.             } else if (embed.status == NativeEmbedStatus.UPDATE) {
    43.               let nodeController = this.nodeControllerMap.get(componentId);
    44.               console.info("NativeEmbed update" + JSON.stringify(embed));
    45.               this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    46.               this.positionMap.set(componentId, this.edges);
    47.               this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    48.               this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    49.               nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
    50.             } else if (embed.status == NativeEmbedStatus.DESTROY) {
    51.               console.info("NativeEmbed destroy" + JSON.stringify(embed));
    52.               let nodeController = this.nodeControllerMap.get(componentId);
    53.               nodeController?.setDestroy(true);
    54.               this.nodeControllerMap.delete(componentId);
    55.               this.positionMap.delete(componentId);
    56.               this.widthMap.delete(componentId);
    57.               this.heightMap.delete(componentId);
    58.               this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
    59.             } else {
    60.               console.info("NativeEmbed status" + embed.status);
    61.             }
    62.           })
    63.       }.height("80%")
    64.     }
    65.   }
    66. }
    
6. 同层渲染手势事件。
    
    开启该功能后，每当在同层渲染的区域进行触摸操作时，ArkWeb内核会触发[onNativeEmbedGestureEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedgestureevent11)注册的回调函数。
    
    开发者则需要调用[onNativeEmbedGestureEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedgestureevent11)来监听同层渲染区域的手势事件。
    
    1. build() {
    2.   Row() {
    3.     Column() {
    4.       Stack() {
    5.         ForEach(this.componentIdArr, (componentId: string) => {
    6.           NodeContainer(this.nodeControllerMap.get(componentId))
    7.             .position(this.positionMap.get(componentId))
    8.             .width(this.widthMap.get(componentId))
    9.             .height(this.heightMap.get(componentId))
    10.         }, (embedId: string) => embedId)
    11.         // Web组件加载本地text.html页面。
    12.         Web({src: $rawfile("text.html"), controller: this.browserTabController})
    13.           // 配置同层渲染开关开启。
    14.           .enableNativeEmbedMode(true)
    15.             // 获取<embed>标签的生命周期变化数据。
    16.           .onNativeEmbedLifecycleChange((embed) => {
    17.             // 生命周期变化实现。
    18.           })
    19.           .onNativeEmbedGestureEvent((touch) => {
    20.             console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
    21.             this.componentIdArr.forEach((componentId: string) => {
    22.               let nodeController = this.nodeControllerMap.get(componentId);
    23.               // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    24.               if(nodeController?.getEmbedId() == touch.embedId) {
    25.                 let ret = nodeController?.postEvent(touch.touchEvent)
    26.                 if(ret) {
    27.                   console.info("onNativeEmbedGestureEvent success " + componentId);
    28.                 } else {
    29.                   console.info("onNativeEmbedGestureEvent fail " + componentId);
    30.                 }
    31.                 if(touch.result) {
    32.                   // 通知Web组件手势事件消费结果。
    33.                   touch.result.setGestureEventResult(ret);
    34.                 }
    35.               }
    36.             })
    37.           })
    38.       }
    39.     }
    40.   }
    41. }
    
7. 同层渲染鼠标事件
    
    开启该功能后，在同层渲染的区域进行下述动作时，ArkWeb内核会触发[onNativeEmbedMouseEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedmouseevent20)注册的回调函数：
    
    - 使用鼠标左键、中键、右键进行点击或长按。
    - 使用触摸板进行对应鼠标左键、中键、右键点击长按的操作。
    
    开发者则需要调用[onNativeEmbedMouseEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-events#onnativeembedmouseevent20)来监听同层渲染区域的鼠标事件。
    
    1. build() {
    2.   Row() {
    3.     Column() {
    4.       Stack() {
    5.         ForEach(this.componentIdArr, (componentId: string) => {
    6.           NodeContainer(this.nodeControllerMap.get(componentId))
    7.             .position(this.positionMap.get(componentId))
    8.             .width(this.widthMap.get(componentId))
    9.             .height(this.heightMap.get(componentId))
    10.         }, (embedId: string) => embedId)
    11.         // Web组件加载本地text.html页面。
    12.         Web({src: $rawfile("text.html"), controller: this.browserTabController})
    13.           // 配置同层渲染开关开启。
    14.           .enableNativeEmbedMode(true)
    15.             // 获取<embed>标签的生命周期变化数据。
    16.           .onNativeEmbedLifecycleChange((embed) => {
    17.             // 生命周期变化实现。
    18.           })
    19.           .onNativeEmbedGestureEvent((touch) => {
    20.             // 处理同层渲染手势事件。
    21.           })
    22.           .onNativeEmbedMouseEvent((mouse) => {
    23.             console.info("NativeEmbed onNativeEmbedMouseEvent" + JSON.stringify(mouse.mouseEvent));
    24.             this.componentIdArr.forEach((componentId: string) => {
    25.               let nodeController = this.nodeControllerMap.get(componentId);
    26.               // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    27.               if(nodeController?.getEmbedId() == mouse.embedId) {
    28.                 let ret = nodeController?.postInputEvent(mouse.mouseEvent)
    29.                 if(ret) {
    30.                   console.info("onNativeEmbedMouseEvent success " + componentId);
    31.                 } else {
    32.                   console.info("onNativeEmbedMouseEvent fail " + componentId);
    33.                 }
    34.                 if(mouse.result) {
    35.                   // 通知Web组件鼠标事件消费结果。
    36.                   mouse.result.setMouseEventResult(ret);
    37.                 }
    38.               }
    39.             })
    40.           })
    41.       }
    42.     }
    43.   }
    44. }
    

**完整示例：**

使用前请在module.json5中添加网络权限，添加方法请参考[在配置文件中声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions#%E5%9C%A8%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%B8%AD%E5%A3%B0%E6%98%8E%E6%9D%83%E9%99%90)。

1. "requestPermissions":[
2.     {
3.       "name" : "ohos.permission.INTERNET"
4.     }
5.   ]

应用侧代码。

1. // 创建NodeController
2. import { webview } from '@kit.ArkWeb';
3. import { UIContext } from '@kit.ArkUI';
4. import { NodeController, BuilderNode, NodeRenderType, FrameNode } from '@kit.ArkUI';

5. @Observed
6. declare class Params{
7.   elementId: string
8.   textOne: string
9.   textTwo: string
10.   width: number
11.   height: number
12. }

13. declare class NodeControllerParams {
14.   surfaceId: string
15.   type: string
16.   renderType: NodeRenderType
17.   embedId: string
18.   width: number
19.   height: number
20. }

21. // 用于控制和反馈对应的NodeContainer上的节点的行为，需要与NodeContainer一起使用。
22. class MyNodeController extends NodeController {
23.   private rootNode: BuilderNode<[Params]> | undefined | null;
24.   private embedId_: string = "";
25.   private surfaceId_: string = "";
26.   private renderType_: NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
27.   private width_: number = 0;
28.   private height_: number = 0;
29.   private type_: string = "";
30.   private isDestroy_: boolean = false;

31.   setRenderOption(params: NodeControllerParams) {
32.     this.surfaceId_ = params.surfaceId;
33.     this.renderType_ = params.renderType;
34.     this.embedId_ = params.embedId;
35.     this.width_ = params.width;
36.     this.height_ = params.height;
37.     this.type_ = params.type;
38.   }

39.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
40.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
41.   makeNode(uiContext: UIContext): FrameNode | null {
42.     if (this.isDestroy_) { // rootNode为null。
43.       return null;
44.     }
45.     if (!this.rootNode) {// rootNode 为undefined时。
46.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_ });
47.       if(this.rootNode) {
48.         this.rootNode.build(wrapBuilder(TextInputBuilder), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
49.         return this.rootNode.getFrameNode();
50.       }else{
51.         return null;
52.       }
53.     }
54.     // 返回FrameNode节点。
55.     return this.rootNode.getFrameNode();
56.   }

57.   updateNode(arg: Object): void {
58.     this.rootNode?.update(arg);
59.   }

60.   getEmbedId(): string {
61.     return this.embedId_;
62.   }

63.   setDestroy(isDestroy: boolean): void {
64.     this.isDestroy_ = isDestroy;
65.     if (this.isDestroy_) {
66.       this.rootNode = null;
67.     }
68.   }

69.   postEvent(event: TouchEvent | undefined): boolean {
70.     return this.rootNode?.postTouchEvent(event) as boolean
71.   }

72.   postInputEvent(event: MouseEvent | undefined): boolean {
73.     return this.rootNode?.postInputEvent(event) as boolean
74.   }
75. }

76. @Component
77. struct TextInputComponent {
78.   @Prop params: Params
79.   @State bkColor: Color = Color.White

80.   build() {
81.     Column() {
82.       TextInput({text: '', placeholder: 'please input your word...'})
83.         .placeholderColor(Color.Gray)
84.         .id(this.params?.elementId)
85.         .placeholderFont({size: 13, weight: 400})
86.         .caretColor(Color.Gray)
87.         .fontSize(14)
88.         .fontColor(Color.Black)
89.     }
90.     //自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
91.     .width(this.params.width)
92.     .height(this.params.height)
93.   }
94. }

95. // @Builder中为动态组件的具体组件内容。
96. @Builder
97. function TextInputBuilder(params:Params) {
98.   TextInputComponent({params: params})
99.     .width(params.width)
100.     .height(params.height)
101.     .backgroundColor(Color.White)
102. }

103. @Entry
104. @Component
105. struct Page{
106.   browserTabController: WebviewController = new webview.WebviewController()
107.   private nodeControllerMap: Map<string, MyNodeController> = new Map();
108.   @State componentIdArr: Array<string> = [];
109.   @State widthMap: Map<string, number> = new Map();
110.   @State heightMap: Map<string, number> = new Map();
111.   @State positionMap: Map<string, Edges> = new Map();
112.   @State edges: Edges = {};
113.   uiContext: UIContext = this.getUIContext();

114.   build() {
115.     Row() {
116.       Column() {
117.         Stack() {
118.           ForEach(this.componentIdArr, (componentId: string) => {
119.             NodeContainer(this.nodeControllerMap.get(componentId))
120.               .position(this.positionMap.get(componentId))
121.               .width(this.widthMap.get(componentId))
122.               .height(this.heightMap.get(componentId))
123.           }, (embedId: string) => embedId)
124.           // Web组件加载本地text.html页面。
125.           Web({src: $rawfile("text.html"), controller: this.browserTabController})
126.             // 配置同层渲染开关开启。
127.             .enableNativeEmbedMode(true)
128.             // 获取<embed>标签的生命周期变化数据。
129.             .onNativeEmbedLifecycleChange((embed) => {
130.                console.info("NativeEmbed surfaceId" + embed.surfaceId);
131.                // 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
132.                const componentId = embed.info?.id?.toString() as string
133.                if (embed.status == NativeEmbedStatus.CREATE) {
134.                  console.info("NativeEmbed create" + JSON.stringify(embed.info));
135.                  // 创建节点控制器、设置参数。
136.                  let nodeController = new MyNodeController()
137.                  // embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
138.                  nodeController.setRenderOption({surfaceId : embed.surfaceId as string,
139.                    type : embed.info?.type as string,
140.                    renderType : NodeRenderType.RENDER_TYPE_TEXTURE,
141.                    embedId : embed.embedId as string,
142.                    width : this.uiContext.px2vp(embed.info?.width),
143.                    height : this.uiContext.px2vp(embed.info?.height)})
144.                  this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
145.                  nodeController.setDestroy(false);
146.                  //根据web传入的embed的id属性作为key，将nodeController存入Map。
147.                  this.nodeControllerMap.set(componentId, nodeController);
148.                  this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
149.                  this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
150.                  this.positionMap.set(componentId, this.edges);
151.                  // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器,需要将push动作放在set之后。
152.                  this.componentIdArr.push(componentId)
153.                } else if (embed.status == NativeEmbedStatus.UPDATE) {
154.                  let nodeController = this.nodeControllerMap.get(componentId);
155.                  console.info("NativeEmbed update" + JSON.stringify(embed));
156.                  this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
157.                  this.positionMap.set(componentId, this.edges);
158.                  this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
159.                  this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
160.                  nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
161.                } else if (embed.status == NativeEmbedStatus.DESTROY) {
162.                  console.info("NativeEmbed destroy" + JSON.stringify(embed));
163.                  let nodeController = this.nodeControllerMap.get(componentId);
164.                  nodeController?.setDestroy(true);
165.                  this.nodeControllerMap.delete(componentId);
166.                  this.positionMap.delete(componentId);
167.                  this.widthMap.delete(componentId);
168.                  this.heightMap.delete(componentId);
169.                  this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
170.                } else {
171.                  console.info("NativeEmbed status" + embed.status);
172.                }
173.              })// 获取同层渲染组件触摸事件信息。
174.             .onNativeEmbedGestureEvent((touch) => {
175.               console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
176.               this.componentIdArr.forEach((componentId: string) => {
177.                 let nodeController = this.nodeControllerMap.get(componentId);
178.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
179.                 if(nodeController?.getEmbedId() == touch.embedId) {
180.                   let ret = nodeController?.postEvent(touch.touchEvent)
181.                   if(ret) {
182.                     console.info("onNativeEmbedGestureEvent success " + componentId);
183.                   } else {
184.                     console.info("onNativeEmbedGestureEvent fail " + componentId);
185.                   }
186.                   if(touch.result) {
187.                     // 通知Web组件手势事件消费结果。
188.                     touch.result.setGestureEventResult(ret);
189.                   }
190.                 }
191.               })
192.             })
193.             .onNativeEmbedMouseEvent((mouse) => {
194.               console.info("NativeEmbed onNativeEmbedMouseEvent" + JSON.stringify(mouse.mouseEvent));
195.               this.componentIdArr.forEach((componentId: string) => {
196.                 let nodeController = this.nodeControllerMap.get(componentId);
197.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
198.                 if(nodeController?.getEmbedId() == mouse.embedId) {
199.                   let ret = nodeController?.postInputEvent(mouse.mouseEvent)
200.                   if(ret) {
201.                     console.info("onNativeEmbedMouseEvent success " + componentId);
202.                   } else {
203.                     console.info("onNativeEmbedMouseEvent fail " + componentId);
204.                   }
205.                   if(mouse.result) {
206.                     // 通知Web组件鼠标事件消费结果。
207.                     mouse.result.setMouseEventResult(ret);
208.                   }
209.                 }
210.               })
211.             })
212.         }
213.       }
214.     }
215.   }
216. }

## 绘制XComponent+AVPlayer和Button组件

- 应用侧代码组件使用示例。
    
    1. // HAP's src/main/ets/pages/Index.ets
    2. // 创建NodeController
    3. import { webview } from '@kit.ArkWeb';
    4. import { UIContext, NodeController, BuilderNode, NodeRenderType, FrameNode } from "@kit.ArkUI";
    5. import { AVPlayerDemo } from './PlayerDemo';
    
    6. @Observed
    7. declare class Params {
    8.   textOne : string
    9.   textTwo : string
    10.   width : number
    11.   height : number
    12. }
    
    13. declare class NodeControllerParams {
    14.   surfaceId : string
    15.   type : string
    16.   renderType : NodeRenderType
    17.   embedId : string
    18.   width : number
    19.   height : number
    20. }
    
    21. // 用于控制和反馈对应的NodeContainer上的节点的行为，需要与NodeContainer一起使用。
    22. class MyNodeController extends NodeController {
    23.   private rootNode: BuilderNode<[Params]> | undefined | null;
    24.   private embedId_ : string = "";
    25.   private surfaceId_ : string = "";
    26.   private renderType_ :NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
    27.   private width_ : number = 0;
    28.   private height_ : number = 0;
    29.   private type_ : string = "";
    30.   private isDestroy_ : boolean = false;
    
    31.   setRenderOption(params : NodeControllerParams) {
    32.     this.surfaceId_ = params.surfaceId;
    33.     this.renderType_ = params.renderType;
    34.     this.embedId_ = params.embedId;
    35.     this.width_ = params.width;
    36.     this.height_ = params.height;
    37.     this.type_ = params.type;
    38.   }
    39.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
    40.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
    41.   makeNode(uiContext: UIContext): FrameNode | null{
    42.     if (this.isDestroy_) { // rootNode为null。
    43.       return null;
    44.     }
    45.     if (!this.rootNode) { // rootNode 为undefined时。
    46.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_});
    47.       if (this.type_ === 'native/video') {
    48.         this.rootNode.build(wrapBuilder(VideoBuilder), {textOne: "myButton", width : this.width_, height : this.height_});
    49.       } else {
    50.         // other
    51.       }
    52.     }
    53.     // 返回FrameNode节点。
    54.     return this.rootNode.getFrameNode();
    55.   }
    
    56.   updateNode(arg: Object): void {
    57.     this.rootNode?.update(arg);
    58.   }
    59.   getEmbedId() : string {
    60.     return this.embedId_;
    61.   }
    
    62.   setDestroy(isDestroy : boolean) : void {
    63.     this.isDestroy_ = isDestroy;
    64.     if (this.isDestroy_) {
    65.       this.rootNode = null;
    66.     }
    67.   }
    
    68.   postEvent(event: TouchEvent | undefined) : boolean {
    69.     return this.rootNode?.postTouchEvent(event) as boolean
    70.   }
    
    71.   postInputEvent(event: MouseEvent | undefined): boolean {
    72.     return this.rootNode?.postInputEvent(event) as boolean
    73.   }
    74. }
    
    75. @Component
    76. struct VideoComponent {
    77.   @ObjectLink params: Params
    78.   @State bkColor: Color = Color.Red
    79.   mXComponentController: XComponentController = new XComponentController();
    80.   @State player_changed: boolean = false;
    81.   player?: AVPlayerDemo;
    
    82.   build() {
    83.     Column() {
    84.       Button(this.params.textOne)
    
    85.       XComponent({ id: 'video_player_id', type: XComponentType.SURFACE, controller: this.mXComponentController})
    86.         .border({width: 1, color: Color.Red})
    87.         .onLoad(() => {
    88.           this.player = new AVPlayerDemo();
    89.           this.player.setSurfaceID(this.mXComponentController.getXComponentSurfaceId());
    90.           this.player_changed = !this.player_changed;
    91.           this.player.avPlayerLiveDemo()
    92.         })
    93.         .width(300)
    94.         .height(200)
    95.     }
    96.     //自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    97.     .width(this.params.width)
    98.     .height(this.params.height)
    99.   }
    100. }
    101. // @Builder中为动态组件的具体组件内容。
    102. @Builder
    103. function VideoBuilder(params: Params) {
    104.   VideoComponent({ params: params })
    105.     .backgroundColor(Color.Gray)
    106. }
    
    107. @Entry
    108. @Component
    109. struct WebIndex {
    110.   browserTabController: WebviewController = new webview.WebviewController()
    111.   private nodeControllerMap: Map<string, MyNodeController> = new Map();
    112.   @State componentIdArr: Array<string> = [];
    113.   @State widthMap: Map<string, number> = new Map();
    114.   @State heightMap: Map<string, number> = new Map();
    115.   @State positionMap: Map<string, Edges> = new Map();
    116.   @State edges: Edges = {};
    117.   uiContext: UIContext = this.getUIContext();
    
    118.   aboutToAppear() {
    119.     // 配置web开启调试模式。
    120.     webview.WebviewController.setWebDebuggingAccess(true);
    121.   }
    
    122.   build(){
    123.     Row() {
    124.       Column() {
    125.         Stack() {
    126.           ForEach(this.componentIdArr, (componentId: string) => {
    127.             NodeContainer(this.nodeControllerMap.get(componentId))
    128.               .position(this.positionMap.get(componentId))
    129.               .width(this.widthMap.get(componentId))
    130.               .height(this.heightMap.get(componentId))
    131.           }, (embedId: string) => embedId)
    132.           // Web组件加载本地test.html页面。
    133.           Web({ src: $rawfile("test.html"), controller: this.browserTabController })
    134.             // 配置同层渲染开关开启。
    135.             .enableNativeEmbedMode(true)
    136.               // 获取<embed>标签的生命周期变化数据。
    137.             .onNativeEmbedLifecycleChange((embed) => {
    138.               console.info("NativeEmbed surfaceId" + embed.surfaceId);
    139.               // 1. 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
    140.               const componentId = embed.info?.id?.toString() as string
    141.               if (embed.status == NativeEmbedStatus.CREATE) {
    142.                 console.info("NativeEmbed create" + JSON.stringify(embed.info))
    143.                 // 创建节点控制器，设置参数。
    144.                 let nodeController = new MyNodeController()
    145.                 // 1. embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
    146.                 nodeController.setRenderOption({surfaceId : embed.surfaceId as string, type : embed.info?.type as string,
    147.                   renderType : NodeRenderType.RENDER_TYPE_TEXTURE, embedId : embed.embedId as string,
    148.                   width : this.uiContext.px2vp(embed.info?.width), height : this.uiContext.px2vp(embed.info?.height)})
    149.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    150.                 nodeController.setDestroy(false);
    151.                 // 根据web传入的embed的id属性作为key，将nodeController存入map。
    152.                 this.nodeControllerMap.set(componentId, nodeController)
    153.                 this.widthMap.set(componentId,  this.uiContext.px2vp(embed.info?.width));
    154.                 this.heightMap.set(componentId,  this.uiContext.px2vp(embed.info?.height));
    155.                 this.positionMap.set(componentId, this.edges);
    156.                 // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器，需要将push动作放在set之后。
    157.                 this.componentIdArr.push(componentId)
    158.               } else if (embed.status == NativeEmbedStatus.UPDATE) {
    159.                 let nodeController = this.nodeControllerMap.get(componentId)
    160.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    161.                 this.positionMap.set(componentId, this.edges);
    162.                 this.widthMap.set(componentId,  this.uiContext.px2vp(embed.info?.width));
    163.                 this.heightMap.set(componentId,  this.uiContext.px2vp(embed.info?.height));
    164.                 nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
    165.               } else if (embed.status == NativeEmbedStatus.DESTROY) {
    166.                 let nodeController = this.nodeControllerMap.get(componentId);
    167.                 nodeController?.setDestroy(true);
    168.                 this.nodeControllerMap.delete(componentId);
    169.                 this.positionMap.delete(componentId);
    170.                 this.widthMap.delete(componentId);
    171.                 this.heightMap.delete(componentId);
    172.                 this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
    173.               } else {
    174.                 console.info("NativeEmbed status" + embed.status);
    175.               }
    176.             })// 获取同层渲染组件触摸事件信息。
    177.             .onNativeEmbedGestureEvent((touch) => {
    178.               console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
    179.               this.componentIdArr.forEach((componentId: string) => {
    180.                 let nodeController = this.nodeControllerMap.get(componentId)
    181.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    182.                 if (nodeController?.getEmbedId() === touch.embedId) {
    183.                   let ret = nodeController?.postEvent(touch.touchEvent)
    184.                   if (ret) {
    185.                     console.info("onNativeEmbedGestureEvent success " + componentId)
    186.                   } else {
    187.                     console.info("onNativeEmbedGestureEvent fail " + componentId)
    188.                   }
    189.                   if (touch.result) {
    190.                     // 通知Web组件手势事件消费结果。
    191.                     touch.result.setGestureEventResult(ret);
    192.                   }
    193.                 }
    194.               })
    195.             })
    196.             .onNativeEmbedMouseEvent((mouse) => {
    197.               console.info("NativeEmbed onNativeEmbedMouseEvent" + JSON.stringify(mouse.mouseEvent));
    198.               this.componentIdArr.forEach((componentId: string) => {
    199.                 let nodeController = this.nodeControllerMap.get(componentId);
    200.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    201.                 if(nodeController?.getEmbedId() == mouse.embedId) {
    202.                   let ret = nodeController?.postInputEvent(mouse.mouseEvent)
    203.                   if(ret) {
    204.                     console.info("onNativeEmbedMouseEvent success " + componentId);
    205.                   } else {
    206.                     console.info("onNativeEmbedMouseEvent fail " + componentId);
    207.                   }
    208.                   if(mouse.result) {
    209.                     // 通知Web组件鼠标事件消费结果。
    210.                     mouse.result.setMouseEventResult(ret);
    211.                   }
    212.                 }
    213.               })
    214.             })
    215.         }
    216.       }
    217.     }
    218.   }
    219. }
    
- 应用侧代码示例，视频播放，使用时需替换为正确的视频链接地址。
    
    1. // HAP's src/main/ets/pages/PlayerDemo.ets
    2. import { media } from '@kit.MediaKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. export class AVPlayerDemo {
    5.   private count: number = 0;
    6.   private surfaceID: string = ''; // surfaceID用于播放画面显示，具体的值需要通过Xcomponent接口获取，相关文档链接见上面Xcomponent创建方法。
    7.   private isSeek: boolean = true; // 用于区分模式是否支持seek操作。
    
    8.   setSurfaceID(surface_id: string){
    9.     console.info('setSurfaceID : ' + surface_id);
    10.     this.surfaceID = surface_id;
    11.   }
    12.   // 注册avplayer回调函数。
    13.   setAVPlayerCallback(avPlayer: media.AVPlayer) {
    14.     // seek操作结果回调函数。
    15.     avPlayer.on('seekDone', (seekDoneTime: number) => {
    16.       console.info(`AVPlayer seek succeeded, seek time is ${seekDoneTime}`);
    17.     })
    18.     // error回调监听函数，当avplayer在操作过程中出现错误时，调用reset接口触发重置流程。
    19.     avPlayer.on('error', (err: BusinessError) => {
    20.       console.error(`Invoke avPlayer failed, code is ${err.code}, message is ${err.message}`);
    21.       avPlayer.reset();
    22.     })
    23.     // 状态机变化回调函数。
    24.     avPlayer.on('stateChange', async (state: string, reason: media.StateChangeReason) => {
    25.       switch (state) {
    26.         case 'idle': // 成功调用reset接口后触发该状态机上报。
    27.           console.info('AVPlayer state idle called.');
    28.           avPlayer.release(); // 调用release接口销毁实例对象。
    29.           break;
    30.         case 'initialized': // avplayer 设置播放源后触发该状态上报。
    31.           console.info('AVPlayer state initialized called.');
    32.           avPlayer.surfaceId = this.surfaceID; // 设置显示画面，当播放的资源为纯音频时无需设置。
    33.           avPlayer.prepare();
    34.           break;
    35.         case 'prepared': // prepared调用成功后上报该状态机。
    36.           console.info('AVPlayer state prepared called.');
    37.           avPlayer.play(); // 调用播放接口开始播放。
    38.           break;
    39.         case 'playing': // play成功调用后触发该状态机上报。
    40.           console.info('AVPlayer state playing called.');
    41.           if(this.count !== 0) {
    42.             if (this.isSeek) {
    43.               console.info('AVPlayer start to seek.');
    44.               avPlayer.seek(avPlayer.duration); // seek到视频末尾。
    45.             } else {
    46.               // 当播放模式不支持seek操作时继续播放到结尾。
    47.               console.info('AVPlayer wait to play end.');
    48.             }
    49.           } else {
    50.             avPlayer.pause(); // 调用暂停接口暂停播放。
    51.           }
    52.           this.count++;
    53.           break;
    54.         case 'paused': // pause成功调用后触发该状态机上报。
    55.           console.info('AVPlayer state paused called.');
    56.           avPlayer.play(); // 再次播放接口开始播放。
    57.           break;
    58.         case 'completed': //播放接口后触发该状态机上报。
    59.           console.info('AVPlayer state completed called.');
    60.           avPlayer.stop(); // 调用播放接口。
    61.           break;
    62.         case 'stopped': // stop接口后触发该状态机上报。
    63.           console.info('AVPlayer state stopped called.');
    64.           avPlayer.reset(); // 调用reset接口初始化avplayer状态。
    65.           break;
    66.         case 'released': //播放接口后触发该状态机上报。
    67.           console.info('AVPlayer state released called.');
    68.           break;
    69.         default:
    70.           break;
    71.       }
    72.     })
    73.   }
    
    74.   // 通过url设置网络地址来实现播放直播码流。
    75.   async avPlayerLiveDemo(){
    76.     // 创建avPlayer实例对象。
    77.     let avPlayer: media.AVPlayer = await media.createAVPlayer();
    78.     // 创建状态机变化回调函数。
    79.     this.setAVPlayerCallback(avPlayer);
    80.     this.isSeek = false; // 不支持seek操作。
    81.     // 使用时需要自行替换视频链接。
    82.     avPlayer.url = 'https://xxx.xxx/demo.mp4';
    83.   }
    84. }
    
- 前端页面示例。
    
    1. <!--HAP's src/main/resources/rawfile/test.html-->
    2. <!DOCTYPE html>
    3. <html>
    4. <head>
    5.     <title>同层渲染测试html</title>
    6.     <meta name="viewport">
    7. </head>
    8. <body>
    9. <div>
    10.     <div id="bodyId">
    11.         <embed id="nativeVideo" type = "native/video" width="1000" height="1500" src="test" style = "background-color:red"/>
    12.     </div>
    13. </div>
    14. </body>
    15. </html>
    
- 实现效果：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.00295511658418628925105587767525:50001231000000:2800:0CFDD88168381CD70C6C15BAF9CDF5E0236275B71020AF9ED3E1771C0179C7A3.png)
    

## 同层标签设置为最高层级

同层渲染支持私有属性arkwebnativestyle，该属性仅在开启同层渲染后的<embed>和<object>中生效，该属性的display属性用于控制同层标签的显示层级，使其高于其他Web元素。如果多个同层标签都设置了arkwebnativestyle的display属性，并且属性相同，则它们的层级顺序将遵循W3C标准层级排序规则：先比较z-index属性值，当z-index相同时，按照元素在DOM中的先后顺序排序。display属性取值说明如下：

|display取值|说明|
|:--|:--|
|overlay|设置同层标签层级高于其他Web元素。|
|overlay-infinity|设置同层标签层级高于其他Web元素和设置overlay的同层标签。|

- 应用侧代码：
    
    1. import { webview } from '@kit.ArkWeb';
    2. import { UIContext } from '@kit.ArkUI';
    3. import { NodeController, BuilderNode, NodeRenderType, FrameNode } from '@kit.ArkUI';
    
    4. @Observed
    5. declare class Params{
    6.   elementId: string
    7.   textOne: string
    8.   textTwo: string
    9.   width: number
    10.   height: number
    11. }
    
    12. declare class NodeControllerParams {
    13.   surfaceId: string
    14.   type: string
    15.   renderType: NodeRenderType
    16.   embedId: string
    17.   width: number
    18.   height: number
    19. }
    
    20. // 用于控制和反馈对应的NodeContainer上的节点的行为，需要与NodeContainer一起使用。
    21. class MyNodeController extends NodeController {
    22.   private rootNode: BuilderNode<[Params]> | undefined | null;
    23.   private embedId_: string = "";
    24.   private surfaceId_: string = "";
    25.   private renderType_: NodeRenderType = NodeRenderType.RENDER_TYPE_DISPLAY;
    26.   private width_: number = 0;
    27.   private height_: number = 0;
    28.   private type_: string = "";
    29.   private isDestroy_: boolean = false;
    
    30.   setRenderOption(params: NodeControllerParams) {
    31.     this.surfaceId_ = params.surfaceId;
    32.     this.renderType_ = params.renderType;
    33.     this.embedId_ = params.embedId;
    34.     this.width_ = params.width;
    35.     this.height_ = params.height;
    36.     this.type_ = params.type;
    37.   }
    
    38.   // 必须要重写的方法，用于构建节点数、返回节点数挂载在对应NodeContainer中。
    39.   // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新。
    40.   makeNode(uiContext: UIContext): FrameNode | null {
    41.     if (this.isDestroy_) { // rootNode为null。
    42.       return null;
    43.     }
    44.     if (!this.rootNode) {// rootNode 为undefined时。
    45.       this.rootNode = new BuilderNode(uiContext, { surfaceId: this.surfaceId_, type: this.renderType_ });
    46.       if (this.type_ == 'native/view1') {
    47.         this.rootNode.build(wrapBuilder(TextInputBuilder1), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
    48.         return this.rootNode.getFrameNode();
    49.       } else if (this.type_ == 'native/view2') {
    50.         this.rootNode.build(wrapBuilder(TextInputBuilder2), {  textOne: "myTextInput", width: this.width_, height: this.height_  })
    51.         return this.rootNode.getFrameNode();
    52.       } else{
    53.         return null;
    54.       }
    55.     }
    56.     // 返回FrameNode节点。
    57.     return this.rootNode.getFrameNode();
    58.   }
    
    59.   updateNode(arg: Object): void {
    60.     this.rootNode?.update(arg);
    61.   }
    
    62.   getEmbedId(): string {
    63.     return this.embedId_;
    64.   }
    
    65.   setDestroy(isDestroy: boolean): void {
    66.     this.isDestroy_ = isDestroy;
    67.     if (this.isDestroy_) {
    68.       this.rootNode = null;
    69.     }
    70.   }
    
    71.   postEvent(event: TouchEvent | undefined): boolean {
    72.     return this.rootNode?.postTouchEvent(event) as boolean
    73.   }
    74. }
    
    75. @Component
    76. struct TextInputComponent1 {
    77.   @Prop params: Params;
    78.   @State bkColor: Color = Color.White;
    
    79.   build() {
    80.     Column() {
    81.       Text("display:overlay-infinity")
    82.       TextInput({text: '', placeholder: 'please input your word...'})
    83.         .placeholderColor(Color.Gray)
    84.         .id(this.params?.elementId)
    85.         .placeholderFont({size: 13, weight: 400})
    86.         .caretColor(Color.Gray)
    87.         .fontSize(14)
    88.         .fontColor(Color.Black)
    89.     }
    90.     // 自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    91.     .width(this.params.width)
    92.     .height(this.params.height)
    93.   }
    94. }
    
    95. // @Builder中为动态组件的具体组件内容。
    96. @Builder
    97. function TextInputBuilder1(params:Params) {
    98.   TextInputComponent1({params: params})
    99.     .width(params.width)
    100.     .height(params.height)
    101.     .backgroundColor(Color.Pink)
    102. }
    
    103. @Component
    104. struct TextInputComponent2 {
    105.   @Prop params: Params;
    106.   @State bkColor: Color = Color.White;
    
    107.   build() {
    108.     Column() {
    109.       Text("display:overlay")
    110.       TextInput({text: '', placeholder: 'please input your word...'})
    111.         .placeholderColor(Color.Gray)
    112.         .id(this.params?.elementId)
    113.         .placeholderFont({size: 13, weight: 400})
    114.         .caretColor(Color.Gray)
    115.         .fontSize(14)
    116.         .fontColor(Color.Black)
    117.     }
    118.     // 自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    119.     .width(this.params.width)
    120.     .height(this.params.height)
    121.   }
    122. }
    
    123. // @Builder中为动态组件的具体组件内容。
    124. @Builder
    125. function TextInputBuilder2(params:Params) {
    126.   TextInputComponent2({params: params})
    127.     .width(params.width)
    128.     .height(params.height)
    129.     .backgroundColor(Color.Gray)
    130. }
    
    131. @Entry
    132. @Component
    133. struct Page{
    134.   browserTabController: webview.WebviewController = new webview.WebviewController();
    135.   private nodeControllerMap: Map<string, MyNodeController> = new Map();
    136.   @State componentIdArr: Array<string> = [];
    137.   @State widthMap: Map<string, number> = new Map();
    138.   @State heightMap: Map<string, number> = new Map();
    139.   @State positionMap: Map<string, Edges> = new Map();
    140.   @State edges: Edges = {};
    141.   uiContext: UIContext = this.getUIContext();
    
    142.   build() {
    143.     Row() {
    144.       Column() {
    145.         Stack() {
    146.           ForEach(this.componentIdArr, (componentId: string) => {
    147.             NodeContainer(this.nodeControllerMap.get(componentId))
    148.               .position(this.positionMap.get(componentId))
    149.               .width(this.widthMap.get(componentId))
    150.               .height(this.heightMap.get(componentId))
    151.           }, (embedId: string) => embedId)
    152.           // Web组件加载本地text.html页面。
    153.           Web({src: $rawfile("overlay.html"), controller: this.browserTabController})
    154.             // 配置同层渲染开关开启。
    155.             .enableNativeEmbedMode(true)
    156.               // 获取<embed>标签的生命周期变化数据。
    157.             .onNativeEmbedLifecycleChange((embed) => {
    158.               console.info("NativeEmbed surfaceId" + embed.surfaceId);
    159.               // 如果使用embed.info.id作为映射nodeController的key，请在h5页面显式指定id。
    160.               const componentId = embed.info?.id?.toString() as string
    161.               if (embed.status == NativeEmbedStatus.CREATE) {
    162.                 console.info("NativeEmbed create" + JSON.stringify(embed.info));
    163.                 // 创建节点控制器、设置参数。
    164.                 let nodeController = new MyNodeController()
    165.                 // embed.info.width和embed.info.height单位是px格式，需要转换成ets侧的默认单位vp。
    166.                 nodeController.setRenderOption({surfaceId : embed.surfaceId as string,
    167.                   type : embed.info?.type as string,
    168.                   renderType : NodeRenderType.RENDER_TYPE_TEXTURE,
    169.                   embedId : embed.embedId as string,
    170.                   width : this.uiContext.px2vp(embed.info?.width),
    171.                   height : this.uiContext.px2vp(embed.info?.height)})
    172.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    173.                 nodeController.setDestroy(false);
    174.                 // 根据web传入的embed的id属性作为key，将nodeController存入Map。
    175.                 this.nodeControllerMap.set(componentId, nodeController);
    176.                 this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    177.                 this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    178.                 this.positionMap.set(componentId, this.edges);
    179.                 // 将web传入的embed的id属性存入@State状态数组变量中，用于动态创建nodeContainer节点容器,需要将push动作放在set之后。
    180.                 this.componentIdArr.push(componentId)
    181.               } else if (embed.status == NativeEmbedStatus.UPDATE) {
    182.                 let nodeController = this.nodeControllerMap.get(componentId);
    183.                 console.info("NativeEmbed update" + JSON.stringify(embed));
    184.                 this.edges = {left: `${embed.info?.position?.x as number}px`, top: `${embed.info?.position?.y as number}px`}
    185.                 this.positionMap.set(componentId, this.edges);
    186.                 this.widthMap.set(componentId, this.uiContext.px2vp(embed.info?.width));
    187.                 this.heightMap.set(componentId, this.uiContext.px2vp(embed.info?.height));
    188.                 nodeController?.updateNode({textOne: 'update', width: this.uiContext.px2vp(embed.info?.width), height: this.uiContext.px2vp(embed.info?.height)} as ESObject)
    189.               } else if (embed.status == NativeEmbedStatus.DESTROY) {
    190.                 console.info("NativeEmbed destroy" + JSON.stringify(embed));
    191.                 let nodeController = this.nodeControllerMap.get(componentId);
    192.                 nodeController?.setDestroy(true);
    193.                 this.nodeControllerMap.delete(componentId);
    194.                 this.positionMap.delete(componentId);
    195.                 this.widthMap.delete(componentId);
    196.                 this.heightMap.delete(componentId);
    197.                 this.componentIdArr = this.componentIdArr.filter((value: string) => value !== componentId);
    198.               } else {
    199.                 console.info("NativeEmbed status" + embed.status);
    200.               }
    201.             })// 获取同层渲染组件触摸事件信息。
    202.             .onNativeEmbedGestureEvent((touch) => {
    203.               console.info("NativeEmbed onNativeEmbedGestureEvent" + JSON.stringify(touch.touchEvent));
    204.               this.componentIdArr.forEach((componentId: string) => {
    205.                 let nodeController = this.nodeControllerMap.get(componentId);
    206.                 // 将获取到的同层区域的事件发送到该区域embedId对应的nodeController上。
    207.                 if(nodeController?.getEmbedId() == touch.embedId) {
    208.                   let ret = nodeController?.postEvent(touch.touchEvent)
    209.                   if(ret) {
    210.                     console.info("onNativeEmbedGestureEvent success " + componentId);
    211.                   } else {
    212.                     console.info("onNativeEmbedGestureEvent fail " + componentId);
    213.                   }
    214.                   if(touch.result) {
    215.                     // 通知Web组件手势事件消费结果。
    216.                     touch.result.setGestureEventResult(ret);
    217.                   }
    218.                 }
    219.               })
    220.             })
    221.             .border({width: 2, color: Color.Gray})
    222.             .height("50%")
    223.         }
    224.       }
    225.     }
    226.   }
    227. }
    
- 前端页面示例：
    
    示例代码使用<embed>标签，若使用<object>标签，请在ets侧注册<object>标签及type类型。
    
    1. <!--HAP's src/main/resources/rawfile/overlay.html-->
    2. <!DOCTYPE html>
    3. <html>
    4. <head>
    5.     <title>同层渲染html</title>
    6.     <meta name="viewport" content="initial-scale=1.0">
    7. </head>
    8. <body>
    9. <div>
    10.     <div id = "test" style = "position: absolute; z-index: 9999; text-align: center; background-color: rgb(61, 157, 180); top: 40px; left: 30px; width: 300px; height: 120px">
    11.         z-index: 9999
    12.     </div>
    
    13.     <embed id = "input1" type = "native/view1" arkwebnativestyle = "display:overlay-infinity" style = "position: absolute; top: 60px; left: 50px; width: 300px; height: 100px">
    
    14.     <embed id = "input2" type = "native/view2" arkwebnativestyle = "display:overlay" style = "position: absolute; top: 150px; left: 40px; width: 300px; height: 100px">
    15. </div>
    16. </body>
    17. </html>
    
- 实现效果：
    
    未设置arkwebnativestyle的display属性：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.85292742076939813175949351475763:50001231000000:2800:9B6F3259AB7E58279A343B2B510E836CC06121C5F7078AFF9A8F78803C4D93A5.png)
    
    设置arkwebnativestyle的display属性：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163823.19737308615704125441553207620616:50001231000000:2800:621D5728E84211C8BC104F987F79AC0CA8071962CF0D6418F339B5978651B465.png)
    

## 常见问题

### 同层渲染组件被拉伸该如何解决？

- 组件高度过大
    
    受GPU限制，同层标签存在8000px的高度限制，如果html5中同层标签高度过高，会存在组件被拉伸的情况，这时需要将同层标签的高度设为8000px以下。
    
- 自定义组件宽高未指定为同层渲染标签的宽高
    
    自定义的同层渲染组件宽高需要与同层标签的宽高保持一致，示例如下：
    
    1.   @Component
    2.   struct TextInputComponent {
    3.     @Prop params: Params
    4.     @State bkColor: Color = Color.White
    
    5.     build() {
    6.       Column() {
    7.         TextInput({text: '', placeholder: 'please input your word...'})
    8.           .fontColor(Color.Black)
    9.       }
    10.       // 自定义组件中的最外层容器组件宽高应该为同层标签的宽高。
    11.       .width(this.params.width)
    12.       .height(this.params.height)
    13.     }
    14.   }
    

### 如何将同层渲染组件捕获到的事件透传到web前端？

同层渲染手势事件通过[setGestureEventResult()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-eventresult#setgestureeventresult14)设置手势事件消费结果，可以选择系统组件侧或ArkWeb侧消费手势事件。如果要实现系统组件侧和ArkWeb侧同时消费手势事件，可以在[setGestureEventResult()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-eventresult#setgestureeventresult14)中将stopPropagation设置为false，即系统组件侧消费的同时可以将手势事件向上冒泡给ArkWeb。

### 同层渲染页面显示该插件不支持该如何解决？

- 同层渲染开关[enableNativeEmbedMode](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web-attributes#enablenativeembedmode11)未开启
    
    使用同层渲染技术需要显式开启同层渲染开关
    
    1. Web({ src: $rawfile("text.html"), controller: this.controller })
    2.   // 配置同层渲染开关开启。
    3.   .enableNativeEmbedMode(true)
    
- 同层标签使用有误
    
    如果使用<embed>标签，需要显式书写embed，并且type类型以"native/"开头；如果使用<object>标签，需要注册<object>标签及type类型。
    

### 涉及界面交互的ArkUI组件（如TextInput等）光标与输入框错位该如何解决？

首先，需使用Stack包裹同层组件容器和BuilderNode。其次，同层组件容器NodeContainer应与同层标签的位置绑定。示例如下：

1. ForEach(this.componentIdArr, (componentId: string) => {
2.   NodeContainer(this.nodeControllerMap.get(componentId))
3.     // 同层组件容器应与同层标签的宽高和位置绑定。
4.     .position(this.positionMap.get(componentId))
5.     .width(this.widthMap.get(componentId))
6.     .height(this.heightMap.get(componentId))
7. }, (embedId: string) => embedId)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-data-detector "使用Web组件的智能分词能力")
# 使用WebNativeMessagingExtensionAbility组件实现浏览器扩展和原生应用通信场景

更新时间: 2025-12-16 16:38

## 概述

浏览器的扩展程序（extension）支持与系统上安装的原生应用交换消息，原生应用向扩展提供服务，帮助扩展实现一些原生应用才具备的能力，常见的例子是密码管理器：原生应用负责存储和加密你的密码信息，以便浏览器扩展程序自动填充网页中的表单字段。

从API version 21开始，支持开发者在原生应用中使用[WebNativeMessagingExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability)组件，为浏览器扩展提供后台服务能力。

浏览器扩展通过[WebExtensions runtime API](https://developer.mozilla.org/zh-CN/docs/Mozilla/Add-ons/WebExtensions/API/runtime)连接WebNativeMessagingExtensionAbility，双方通信是通过共享pipe文件描述符后调用IO接口实现。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163824.79433999748953361262655217619945:50001231000000:2800:2833A669D96554917295932336F684D1A286BC3023112261A4B136A66D85A585.png)

说明

本文将浏览器扩展调用WebExtension接口runtime.connectNative建立的连接称为NativeMessaging连接。

NativeMessaging面向两类开发者：原生应用开发者和浏览器应用开发者。两者均需要了解WebNativeMessagingExtensionAbility运作机制，但关注的场景和接口不同。原生应用开发者关注[WebNativeMessagingExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability)组件的使用，负责相关业务开发；浏览器应用开发者负责建立NativeMessaging连接，关注[WebNativeMessagingExtensionManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionmanager)相关接口。

本文会在具体的描述中，特意标注需要哪类开发者关注。

## 约束与限制

### 设备限制

WebNativeMessagingExtensionAbility组件当前仅支持2in1设备。

### 规格限制

- WebNativeMessagingExtensionAbility组件无需额外权限，允许任意三方应用集成使用，但拉起方（浏览器）需申请ACL权限（ohos.permission.WEB_NATIVE_MESSAGING）。此权限仅对浏览器类应用开放。
    
- WebNativeMessagingExtensionAbility组件内不支持调用[Window](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window)相关API。
    
- WebNativeMessagingExtensionAbility仅支持拉起本应用的UIAbility，不支持拉起其他应用UIAbility或者其他类型ExtensionAbility。
    
- WebNativeMessagingExtensionAbility仅用于浏览器扩展与原生应用通信场景，不支持如后台服务等其他场景使用。
    

## 运作机制

### 整体流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163824.07740783318678855624717107601073:50001231000000:2800:784152FA2AD36B58215690B7B9E64F13EF5D14C05AA21DFB5329A6F776BD6749.png)

- **流程：**

1. **浏览器扩展**调用runtime.connectNative接口传入原生应用包名，来创建NativeMessaging连接。
2. **浏览器应用**调用[dataShare](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/share-config)获取原生应用配置信息，包括WebNativeMessagingExtension的名称，和限制访问规则（是否允许某个扩展访问该WebNativeMessagingExtension）。
3. **浏览器应用**创建两组pipe作为收发双向通道，调用[WebNativeMessagingExtensionManager.connectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionmanager#webnativemessagingextensionmanagerconnectnative)接口，拉起WebNativeMessagingExtension并创建一条NativeMessaging连接，并将pipe的收发文件描述符作为参数传输过去。
4. **原生应用**WebNativeMessagingExtensionAbility被拉起，[WebNativeMessagingExtensionAbility.onConnectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability#onconnectnative)生命周期回调触发，获取pipe的文件描述符。
5. **原生应用**监听读端的文件描述符，获取浏览器扩展发过来的消息指令，并通过写端的文件描述符发送回去。
6. **原生应用**使用[WebNativeMessagingExtensionContext.startAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensioncontext#startability)拉起本应用的UIAbility图形界面。

说明

WebNativeMessagingExtensionAbility为单实例独立进程，多次调用connectNative接口仅拉起一个实例，同时触发多次onConnectNative回调，需要**原生应用**管理多会话场景。

### dataShare存放原生应用extension配置信息

原生应用集成WebNativeMessagingExtensionAbility时，需要通过dataShare能力向浏览器应用提供extension配置。该配置用于浏览器应用判断允许访问的扩展及指定要拉起的WebNativeMessagingExtensionAbility名称。

extension配置采用json字符串格式

- extensionAbility属性：字符串，WebNativeMessagingExtensionAbility名称，用于填充want中abilityName字段，一个原生应用仅有一个WebNativeMessagingExtensionAbility。
- allowed_origins属性：数组，允许访问该WebNativeMessagingExtensionAbility的浏览器扩展url信息，可以配置多条，不同浏览器的扩展有不同的scheme协议，例如华为浏览器使用chrome-extension协议头。

extension配置格式：

1. {
2.   // 原生应用包名
3.   "name": "com.example.myapplication",
4.   // 具体描述
5.   "description": "Send message to native app.",
6.   /*
7.    * WebNativeMessagingExtensionAbility名称，用于元能力want填充abilityName，一个应用应只有一个
8.    * WebNativeMessagingExtensionAbility
9.    */
10.   "abilityName": "webExtensionAbility",
11.   /*
12.    * 允许访问该WebNativeMessagingExtensionAbility的浏览器扩展url信息，不同的浏览器的扩展有不同的scheme协议，华为浏览器使用chrome-extension协议头
13.    */
14.   "allowed_origins":[
15.     "chrome-extension://knldjmfmopnpolahpmmgbagdohdnhkik/"
16.   ]
17. }

extension配置存放在[dataShare配置项](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/share-config#modulejson5-%E9%85%8D%E7%BD%AE)，uri为固定格式：datashardporxy://[包名]/browserNativeMessagingHosts。

### WebNativeMessagingExtensionAbility生命周期管理

- [onConnectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability#onconnectnative)：当浏览器扩展调用一次runtime.connectNative时触发，如果WebNativeMessagingExtensionAbility尚未运行，调用runtime.connectNative会拉起WebNativeMessagingExtensionAbility，并触发该回调。
- [onDisconnectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability#ondisconnectnative)：当浏览器扩展销毁runtime.port时，会触发一次该回调，每条nativeMessaging连接的断开，都会触发一次该回调，当全部连接都断开时，会触发onDestroy的回调后关闭WebNativeMessagingExtensionAbility。
- [onDestroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability#ondestroy)：当WebNativeMessagingExtensionAbility销毁前触发该回调，全部NativeMessaging连接断开会触发WebNativeMessagingExtensionAbility的销毁。
- [stopNativeConnection](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensioncontext#stopnativeconnection)：WebNativeMessagingExtensionAbility可以主动断开一条NativeMessaging连接，如果断开的是最后一条连接，则会触发WebNativeMessagingExtensionAbility的销毁。
- [terminateSelf](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensioncontext#terminateself)：WebNativeMessagingExtensionAbility可以主动退出，触发后会销毁所有NativeMessaging连接。

### 消息格式和限制

NativeMessaging连接使用的具体格式，每个消息都使用 JSON 进行序列化，编码为 UTF-8，并在前面附加 32 位消息长度（采用原生字节顺序）。来自WebNativeMessagingExtensionAbility的单个消息的大小上限为 1 MB，这主要是为了保护浏览器免受行为异常的原生应用影响。发送到WebNativeMessagingExtensionAbility的消息大小上限为 64 MB。

### 实现一个connectNative的扩展（原生应用开发者）

说明

需按w3c标准配置manifest.json和background.js实现通信。

支持使用chrome.runtime.connectNative或chrome.runtime.sendNativeMessage进行连接。

配置插件内容，发送ping字符串并接收pong响应的插件代码，示例如下：

**实现配置manifest.json**

1. {
2.   "name": "com.example.myapplication",
3.   "version": "1.0.1",
4.   "description": "Launch APP",
5.   "manifest_version": 3,
6.   "permissions": ["nativeMessaging", "tabs", "scripting"], //根据实际场景是否需要进行选择
7.   "host_permissions": ["http://*/*", "https://*/*", "ftp://*/*", "file://*/*"], //根据实际场景选择
8.   "background": {
9.     "service_worker": "background.js" //用于运行插件runtime命令
10.   },
11.   "content_scripts": [
12.     {
13.       "matches": ["http://*/*", "https://*/*", "ftp://*/*", "file://*/*"], //根据实际场景选择
14.       "js": ["main.js"] //用于运行插件js命令
15.     }
16.   ],
17.   "action": {
18.     "default_popup": "index.html" //插件页面展示
19.   }
20. }

**实现main.js**

1. // 从html中触发调用
2. function sendMessageToNative() {
3.   var message = "ping"; // 发送ping
4.   chrome.runtime.sendMessage({
5.     type: "sendMessage",
6.     message: message
7.   }, function (response) {});
8. }

**实现配置background.js**

1. 使用chrome.runtime.connectNative链接

2. var port = null;
3. //监听来自main.js的信息
4. chrome.runtime.onMessage.addListener(
5.   function (request, sender, sendResponse) {
6.     if (request.type == "sendMessage") {
7.       if (port == null) {
8.         connectToNativeHost();
9.       }
10.       port.postMessage(request.message); //向应用程序发送信息
11.     }
12.     return true; //保持消息通道开放
13. });
14. function connectToNativeHost() {
15.   var bundleName = "com.example.app"; //插件对应应用的bundleName
16.   port = chrome.runtime.connectNative(bundleName); //根据bundleName名得到通信端口port
17.   port.onMessage.addListener(onNativeMessage); //监听native应用程序是否发来消息
18.   port.onDisconnect.addListener(onDisconnected); //监听是否断开连接
19. }
20. //接收到来自native程序的消息时触发
21. async function onNativeMessage(message) {
22.   console.info('接收到从本地应用程序发送来的消息：' + JSON.stringify(message)); //示例中的pong
23. }
24. //断开连接时触发
25. function onDisconnected() {
26.   port = null;
27. }

28. 使用chrome.runtime.sendNativeMessage链接

29. function sendNativeMessage() {
30.   var bundleName = "com.example.app"; //插件对应应用的bundleName
31.   var nativeMessage = "ping"; //插件要发给应用的内容
32.   chrome.runtime.sendNativeMessage(
33.     bundleName,
34.     {message: nativeMessage},
35.     function(response) {
36.       // 收到一次应用回复的信息后断开链接
37.       console.info("sendNativeMessage收到原生应用程序响应:", JSON.stringify(response));
38.     }
39.   )
40. }

### 实现一个WebNativeMessagingExtensionAbility（原生应用开发者）

在DevEco Studio工程中手动新建一个WebNativeMessagingExtensionAbility组件，具体步骤如下：

1. 在工程Module对应的ets目录下，右键选择“New > Directory”，新建一个目录并命名为MyWebNativeMessageExtAbility。
    
2. 在MyWebNativeMessageExtAbility目录，右键选择“New > ArkTS File”，新建一个文件并命名为MyWebNativeMessageExtAbility.ets。
    
    其目录结构如下所示：
    
    1. ├── ets
    2. │ ├── MyWebNativeMessageExtAbility
    3. │ │   ├── MyWebNativeMessageExtAbility.ets
    4. └
    
3. 在MyWebNativeMessageExtAbility.ets文件中，增加导入[WebNativeMessagingExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability)的依赖包，自定义类继承WebNativeMessagingExtensionAbility组件并实现生命周期回调。
    

4.   import { WebNativeMessagingExtensionAbility, ConnectionInfo } from '@kit.ArkWeb';
5.   import { hilog } from '@kit.PerformanceAnalysisKit';
6.   import {buffer, util} from '@kit.ArkTS';
7.   import { fileIo as fs } from '@kit.CoreFileKit';

8.   const TAG: string = '[MyWebNativeMessageExtAbility]';
9.   const DOMAIN_NUMBER: number = 0xFF00;

10.   export default class MyWebNativeMessageExtAbility extends WebNativeMessagingExtensionAbility {
11.     // 读取扩展发来的消息，并回复
12.     async ReadAsync(fdRead:number, fdWrite:number) : Promise<void> {
13.       try {
14.         // read
15.         let arrayBuffer = new ArrayBuffer(1024);
16.         let readLen = await fs.read(fdRead, arrayBuffer);
17.         if (readLen <= 4) {
18.           hilog.error(DOMAIN_NUMBER, TAG, 'read pipe length failed');
19.           return;
20.         }
21.         hilog.info(DOMAIN_NUMBER, TAG, 'read pipe %{public}s', buffer.from(arrayBuffer, 4, readLen - 4).toString());

22.         // write
23.         let strResponse : string = "pong";
24.         const encoder = new util.TextEncoder("utf-8");
25.         const strBytes = encoder.encodeInto(strResponse);
26.         let bufferLen = strBytes.length;
27.         const lenBytes = new Uint8Array(4);
28.         lenBytes[0] = (bufferLen >> 0) & 0xFF;
29.         lenBytes[1] = (bufferLen >> 8) & 0xFF;
30.         lenBytes[2] = (bufferLen >> 16) & 0xFF;
31.         lenBytes[3] = (bufferLen >> 24) & 0xFF;
32.         const writeBuffer = new Uint8Array(4 + bufferLen);
33.         writeBuffer.set(lenBytes, 4);
34.         writeBuffer.set(strBytes, 4);
35.         let writeLen = await fs.write(fdWrite, writeBuffer.buffer);
36.         hilog.info(DOMAIN_NUMBER, TAG, 'write pipe length %{public}d', writeLen);
37.       } catch (err) {
38.         hilog.error(DOMAIN_NUMBER, TAG, 'fs io failed, error code: ' + err.code + " message: " + err.code);
39.       }
40.     }

41.     onConnectNative(info: ConnectionInfo): void {
42.       hilog.info(DOMAIN_NUMBER, TAG,
43.         `onConnectNative, connectionId ${info.connectionId} caller bundle: ${info.bundleName}, extension origin: ${info.extensionOrigin}, pipe Read: ${info.fdRead}, pipe write ${info.fdWrite}  `);
44.       this.ReadAsync(info.fdRead, info.fdWrite)
45.     }

46.     onDisconnectNative(info: ConnectionInfo): void {
47.       hilog.info(DOMAIN_NUMBER, TAG, `onDisconnectNative, connectionId: ${info.connectionId}`);
48.     }

49.     onDestroy(): void {
50.       hilog.info(DOMAIN_NUMBER, TAG, 'onDestroy');
51.     }
52.   };

53. 在工程Module的[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中注册WebNativeMessagingExtensionAbility组件。设置type标签为“webNativeMessaging”，srcEntry标签指向组件代码路径。
    
    1. {
    2.   "module": {
    3.     // ...
    4.     "extensionAbilities": [
    5.       {
    6.         "name": "MyWebNativeMessageExtAbility",
    7.         "description": "webNativeMessaging",
    8.         "type": "webNativeMessaging",
    9.         "exported": true,
    10.         "srcEntry": "./ets/MyWebNativeMessageExtAbility/MyWebNativeMessageExtAbility.ets"
    11.       }
    12.     ]
    13.   }
    14. }
    
54. 在工程Module对应的[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中配置crossAppSharedConfig，定义共享配置项，共享配置文件需放置在工程resources/base/profile目录下，并通过$资源访问方式引用。
    

55.   {
56.     "module": {
57.       "crossAppSharedConfig": "$profile:shared_config"
58.     }
59.   }

6.在shared_config.json添加[extension配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-native-messaging#datashare%E5%AD%98%E6%94%BE%E5%8E%9F%E7%94%9F%E5%BA%94%E7%94%A8extension%E9%85%8D%E7%BD%AE%E4%BF%A1%E6%81%AF)

1.   {
2.     "crossAppSharedConfig": [
3.       // ...
4.       {
5.         // uri固定格式，datashardporxy://[包名]/browserNativeMessagingHosts，浏览器应用通过该uri获取的value，即extension配置。
6.         "uri": "datashareproxy://com.example.app/browserNativeMessagingHosts",
7.         // extension配置，格式参考extension配置章节的格式，注意转义字符
8.         "value": "{\"name\": \"com.example.myapplication\",\"description\": \"Send message to native app.\",\"abilityName\": \"MyWebNativeMessageExtAbility\", \"allowed_origins\":[\"chrome-extension://knldjmfmopnpolahpmmgbagdohdnhkik/\"]}",
9.         "allowList": [
10.           // 允许访问的应用appIdentifier, 这里加入具体浏览器的appIdentifier
11.           "1234567890123456789"
12.         ]
13.       }
14.     ]
15.   }

### 实现拉起WebNativeMessagingExtensionAbility（浏览器开发者）

浏览器负责实现扩展runtime接口，拉起WebNativeMessagingExtensionAbility，建立和管理NativeMessaging连接。需要申请权限：ohos.permission.WEB_NATIVE_MESSAGING

1. 当接收到创建NativeMessaging连接时，先通过[应用间配置共享接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-data-datashare#get20)获取目标应用的extension配置。然后读取WebNativeMessagingExtensionAbility名称和允许访问的扩展列表。最后校验是否允许访问。

2.   import { dataShare } from '@kit.ArkData';

3.   interface ExtensionConfig {
4.     abilityName:string;
5.     allowed_origins:string[];
6.   }

7.   async function getManifestData(bundleName:string, connectExtensionOrigin:string) {
8.     try {
9.       // 调用dataShare接口获取extension配置
10.       const dsProxyHelper = await dataShare.createDataProxyHandle();
11.       const urisToGet = [`datashareproxy://${bundleName}/browserNativeMessagingHosts`];
12.       const config : dataShare.DataProxyConfig = {
13.         type: dataShare.DataProxyType.SHARED_CONFIG,
14.       };
15.       const results = await dsProxyHelper.get(urisToGet, config);
16.       let foundValid = false;
17.       for (let i = 0; i < results.length; i++) {
18.         try {
19.           const result = results[i];
20.           const json = result.value;
21.           if (typeof json !== "string") {
22.             continue;
23.           }
24.           let jsonStr:string = json as string;
25.           let info:ExtensionConfig = JSON.parse(jsonStr);
26.           if (info.abilityName) {
27.             console.info('Native message json info is ok');
28.             if (!Array.isArray(info.allowed_origins)) {
29.               info.allowed_origins = [info.allowed_origins];
30.             }
31.             if (!info.allowed_origins.includes(connectExtensionOrigin)) {
32.               console.error('Origin not allowed, continue searching');
33.               continue;
34.             }
35.             foundValid = true;
36.             break;
37.           }
38.         } catch (error) {
39.           console.error('NativeMessage JSON parse error:', error);
40.         }
41.       }
42.       if (!foundValid) {
43.         console.error('NativeMessage JSON no valid manifest found');
44.       } else {
45.         console.info('NativeMessage allowed_origins match ok');
46.       }
47.     } catch (error) {
48.       console.error('Error getting config:', error);
49.     }
50.   }

51. 调用[webNativeMessagingExtensionManager.connectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionmanager#webnativemessagingextensionmanagerconnectnative)创建NativeMessage，如WebNativeMessagingExtensionAbility尚未运行，该接口则会拉起ExtensionAbility并触发。

52.   import { UIAbility, Want, common } from '@kit.AbilityKit';
53.   import { webNativeMessagingExtensionManager } from '@kit.ArkWeb'

54.   class ConnectionCallback implements webNativeMessagingExtensionManager.WebExtensionConnectionCallback {
55.     onConnect(connection:webNativeMessagingExtensionManager.ConnectionNativeInfo) {
56.       // connected
57.       console.error(`onConnect id ${connection.connectionId} is connected`);
58.     }
59.     onDisconnect(connection:webNativeMessagingExtensionManager.ConnectionNativeInfo) {
60.       // disconnect
61.       console.error(`onDisconnect id ${connection.connectionId} is connected`);
62.     }
63.     onFailed(code:webNativeMessagingExtensionManager.NmErrorCode, errMsg:string) {
64.       console.error(`onFailed error code is ${code}, errMsg is ${errMsg}`);
65.     }
66.   }

67.   function connectNative(abilityContext: common.UIAbilityContext, bundleName: string, abilityName: string,
68.     connectExtensionOrigin: string, readPipe: number, writePipe: number) : void {
69.     try {
70.       let wantInfo:Want = {
71.         bundleName: bundleName,
72.         abilityName: abilityName,
73.         parameters: {
74.           'ohos.arkweb.messageReadPipe': { 'type': 'FD', 'value': readPipe },
75.           'ohos.arkweb.messageWritePipe': { 'type': 'FD', 'value': writePipe },
76.           'ohos.arkweb.extensionOrigin': connectExtensionOrigin
77.         },
78.       };

79.       let options : ConnectionCallback = new ConnectionCallback;
80.       let connectId = webNativeMessagingExtensionManager.connectNative(abilityContext, wantInfo, options);
81.       console.info(`innerWebNativeMessageManager  connectionId : ${connectId}` );
82.     } catch (error) {
83.       console.info(`inner callback error Message: ${JSON.stringify(error)}`);
84.     }
85.   }

86. 需要销毁NativeMessaging连接时，调用[webNativeMessagingExtensionManager.disconnectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionmanager#webnativemessagingextensionmanagerdisconnectnative)。

87.   import { webNativeMessagingExtensionManager } from '@kit.ArkWeb'

88.   function disconnencNative(connectId: number) : void {
89.     console.info(`NativeMessageDisconnect start connectionId is ${connectId}`);
90.     webNativeMessagingExtensionManager.disconnectNative(connectId);
91.   }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-offline-mode "使用离线Web组件")
# 使用WebNativeMessagingExtensionAbility组件实现浏览器扩展和原生应用通信场景

更新时间: 2025-12-16 16:38

## 概述

浏览器的扩展程序（extension）支持与系统上安装的原生应用交换消息，原生应用向扩展提供服务，帮助扩展实现一些原生应用才具备的能力，常见的例子是密码管理器：原生应用负责存储和加密你的密码信息，以便浏览器扩展程序自动填充网页中的表单字段。

从API version 21开始，支持开发者在原生应用中使用[WebNativeMessagingExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability)组件，为浏览器扩展提供后台服务能力。

浏览器扩展通过[WebExtensions runtime API](https://developer.mozilla.org/zh-CN/docs/Mozilla/Add-ons/WebExtensions/API/runtime)连接WebNativeMessagingExtensionAbility，双方通信是通过共享pipe文件描述符后调用IO接口实现。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163824.79433999748953361262655217619945:50001231000000:2800:2833A669D96554917295932336F684D1A286BC3023112261A4B136A66D85A585.png)

说明

本文将浏览器扩展调用WebExtension接口runtime.connectNative建立的连接称为NativeMessaging连接。

NativeMessaging面向两类开发者：原生应用开发者和浏览器应用开发者。两者均需要了解WebNativeMessagingExtensionAbility运作机制，但关注的场景和接口不同。原生应用开发者关注[WebNativeMessagingExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability)组件的使用，负责相关业务开发；浏览器应用开发者负责建立NativeMessaging连接，关注[WebNativeMessagingExtensionManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionmanager)相关接口。

本文会在具体的描述中，特意标注需要哪类开发者关注。

## 约束与限制

### 设备限制

WebNativeMessagingExtensionAbility组件当前仅支持2in1设备。

### 规格限制

- WebNativeMessagingExtensionAbility组件无需额外权限，允许任意三方应用集成使用，但拉起方（浏览器）需申请ACL权限（ohos.permission.WEB_NATIVE_MESSAGING）。此权限仅对浏览器类应用开放。
    
- WebNativeMessagingExtensionAbility组件内不支持调用[Window](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-window)相关API。
    
- WebNativeMessagingExtensionAbility仅支持拉起本应用的UIAbility，不支持拉起其他应用UIAbility或者其他类型ExtensionAbility。
    
- WebNativeMessagingExtensionAbility仅用于浏览器扩展与原生应用通信场景，不支持如后台服务等其他场景使用。
    

## 运作机制

### 整体流程

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163824.07740783318678855624717107601073:50001231000000:2800:784152FA2AD36B58215690B7B9E64F13EF5D14C05AA21DFB5329A6F776BD6749.png)

- **流程：**

1. **浏览器扩展**调用runtime.connectNative接口传入原生应用包名，来创建NativeMessaging连接。
2. **浏览器应用**调用[dataShare](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/share-config)获取原生应用配置信息，包括WebNativeMessagingExtension的名称，和限制访问规则（是否允许某个扩展访问该WebNativeMessagingExtension）。
3. **浏览器应用**创建两组pipe作为收发双向通道，调用[WebNativeMessagingExtensionManager.connectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionmanager#webnativemessagingextensionmanagerconnectnative)接口，拉起WebNativeMessagingExtension并创建一条NativeMessaging连接，并将pipe的收发文件描述符作为参数传输过去。
4. **原生应用**WebNativeMessagingExtensionAbility被拉起，[WebNativeMessagingExtensionAbility.onConnectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability#onconnectnative)生命周期回调触发，获取pipe的文件描述符。
5. **原生应用**监听读端的文件描述符，获取浏览器扩展发过来的消息指令，并通过写端的文件描述符发送回去。
6. **原生应用**使用[WebNativeMessagingExtensionContext.startAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensioncontext#startability)拉起本应用的UIAbility图形界面。

说明

WebNativeMessagingExtensionAbility为单实例独立进程，多次调用connectNative接口仅拉起一个实例，同时触发多次onConnectNative回调，需要**原生应用**管理多会话场景。

### dataShare存放原生应用extension配置信息

原生应用集成WebNativeMessagingExtensionAbility时，需要通过dataShare能力向浏览器应用提供extension配置。该配置用于浏览器应用判断允许访问的扩展及指定要拉起的WebNativeMessagingExtensionAbility名称。

extension配置采用json字符串格式

- extensionAbility属性：字符串，WebNativeMessagingExtensionAbility名称，用于填充want中abilityName字段，一个原生应用仅有一个WebNativeMessagingExtensionAbility。
- allowed_origins属性：数组，允许访问该WebNativeMessagingExtensionAbility的浏览器扩展url信息，可以配置多条，不同浏览器的扩展有不同的scheme协议，例如华为浏览器使用chrome-extension协议头。

extension配置格式：

1. {
2.   // 原生应用包名
3.   "name": "com.example.myapplication",
4.   // 具体描述
5.   "description": "Send message to native app.",
6.   /*
7.    * WebNativeMessagingExtensionAbility名称，用于元能力want填充abilityName，一个应用应只有一个
8.    * WebNativeMessagingExtensionAbility
9.    */
10.   "abilityName": "webExtensionAbility",
11.   /*
12.    * 允许访问该WebNativeMessagingExtensionAbility的浏览器扩展url信息，不同的浏览器的扩展有不同的scheme协议，华为浏览器使用chrome-extension协议头
13.    */
14.   "allowed_origins":[
15.     "chrome-extension://knldjmfmopnpolahpmmgbagdohdnhkik/"
16.   ]
17. }

extension配置存放在[dataShare配置项](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/share-config#modulejson5-%E9%85%8D%E7%BD%AE)，uri为固定格式：datashardporxy://[包名]/browserNativeMessagingHosts。

### WebNativeMessagingExtensionAbility生命周期管理

- [onConnectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability#onconnectnative)：当浏览器扩展调用一次runtime.connectNative时触发，如果WebNativeMessagingExtensionAbility尚未运行，调用runtime.connectNative会拉起WebNativeMessagingExtensionAbility，并触发该回调。
- [onDisconnectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability#ondisconnectnative)：当浏览器扩展销毁runtime.port时，会触发一次该回调，每条nativeMessaging连接的断开，都会触发一次该回调，当全部连接都断开时，会触发onDestroy的回调后关闭WebNativeMessagingExtensionAbility。
- [onDestroy](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability#ondestroy)：当WebNativeMessagingExtensionAbility销毁前触发该回调，全部NativeMessaging连接断开会触发WebNativeMessagingExtensionAbility的销毁。
- [stopNativeConnection](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensioncontext#stopnativeconnection)：WebNativeMessagingExtensionAbility可以主动断开一条NativeMessaging连接，如果断开的是最后一条连接，则会触发WebNativeMessagingExtensionAbility的销毁。
- [terminateSelf](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensioncontext#terminateself)：WebNativeMessagingExtensionAbility可以主动退出，触发后会销毁所有NativeMessaging连接。

### 消息格式和限制

NativeMessaging连接使用的具体格式，每个消息都使用 JSON 进行序列化，编码为 UTF-8，并在前面附加 32 位消息长度（采用原生字节顺序）。来自WebNativeMessagingExtensionAbility的单个消息的大小上限为 1 MB，这主要是为了保护浏览器免受行为异常的原生应用影响。发送到WebNativeMessagingExtensionAbility的消息大小上限为 64 MB。

### 实现一个connectNative的扩展（原生应用开发者）

说明

需按w3c标准配置manifest.json和background.js实现通信。

支持使用chrome.runtime.connectNative或chrome.runtime.sendNativeMessage进行连接。

配置插件内容，发送ping字符串并接收pong响应的插件代码，示例如下：

**实现配置manifest.json**

1. {
2.   "name": "com.example.myapplication",
3.   "version": "1.0.1",
4.   "description": "Launch APP",
5.   "manifest_version": 3,
6.   "permissions": ["nativeMessaging", "tabs", "scripting"], //根据实际场景是否需要进行选择
7.   "host_permissions": ["http://*/*", "https://*/*", "ftp://*/*", "file://*/*"], //根据实际场景选择
8.   "background": {
9.     "service_worker": "background.js" //用于运行插件runtime命令
10.   },
11.   "content_scripts": [
12.     {
13.       "matches": ["http://*/*", "https://*/*", "ftp://*/*", "file://*/*"], //根据实际场景选择
14.       "js": ["main.js"] //用于运行插件js命令
15.     }
16.   ],
17.   "action": {
18.     "default_popup": "index.html" //插件页面展示
19.   }
20. }

**实现main.js**

1. // 从html中触发调用
2. function sendMessageToNative() {
3.   var message = "ping"; // 发送ping
4.   chrome.runtime.sendMessage({
5.     type: "sendMessage",
6.     message: message
7.   }, function (response) {});
8. }

**实现配置background.js**

1. 使用chrome.runtime.connectNative链接

2. var port = null;
3. //监听来自main.js的信息
4. chrome.runtime.onMessage.addListener(
5.   function (request, sender, sendResponse) {
6.     if (request.type == "sendMessage") {
7.       if (port == null) {
8.         connectToNativeHost();
9.       }
10.       port.postMessage(request.message); //向应用程序发送信息
11.     }
12.     return true; //保持消息通道开放
13. });
14. function connectToNativeHost() {
15.   var bundleName = "com.example.app"; //插件对应应用的bundleName
16.   port = chrome.runtime.connectNative(bundleName); //根据bundleName名得到通信端口port
17.   port.onMessage.addListener(onNativeMessage); //监听native应用程序是否发来消息
18.   port.onDisconnect.addListener(onDisconnected); //监听是否断开连接
19. }
20. //接收到来自native程序的消息时触发
21. async function onNativeMessage(message) {
22.   console.info('接收到从本地应用程序发送来的消息：' + JSON.stringify(message)); //示例中的pong
23. }
24. //断开连接时触发
25. function onDisconnected() {
26.   port = null;
27. }

28. 使用chrome.runtime.sendNativeMessage链接

29. function sendNativeMessage() {
30.   var bundleName = "com.example.app"; //插件对应应用的bundleName
31.   var nativeMessage = "ping"; //插件要发给应用的内容
32.   chrome.runtime.sendNativeMessage(
33.     bundleName,
34.     {message: nativeMessage},
35.     function(response) {
36.       // 收到一次应用回复的信息后断开链接
37.       console.info("sendNativeMessage收到原生应用程序响应:", JSON.stringify(response));
38.     }
39.   )
40. }

### 实现一个WebNativeMessagingExtensionAbility（原生应用开发者）

在DevEco Studio工程中手动新建一个WebNativeMessagingExtensionAbility组件，具体步骤如下：

1. 在工程Module对应的ets目录下，右键选择“New > Directory”，新建一个目录并命名为MyWebNativeMessageExtAbility。
    
2. 在MyWebNativeMessageExtAbility目录，右键选择“New > ArkTS File”，新建一个文件并命名为MyWebNativeMessageExtAbility.ets。
    
    其目录结构如下所示：
    
    1. ├── ets
    2. │ ├── MyWebNativeMessageExtAbility
    3. │ │   ├── MyWebNativeMessageExtAbility.ets
    4. └
    
3. 在MyWebNativeMessageExtAbility.ets文件中，增加导入[WebNativeMessagingExtensionAbility](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionability)的依赖包，自定义类继承WebNativeMessagingExtensionAbility组件并实现生命周期回调。
    

4.   import { WebNativeMessagingExtensionAbility, ConnectionInfo } from '@kit.ArkWeb';
5.   import { hilog } from '@kit.PerformanceAnalysisKit';
6.   import {buffer, util} from '@kit.ArkTS';
7.   import { fileIo as fs } from '@kit.CoreFileKit';

8.   const TAG: string = '[MyWebNativeMessageExtAbility]';
9.   const DOMAIN_NUMBER: number = 0xFF00;

10.   export default class MyWebNativeMessageExtAbility extends WebNativeMessagingExtensionAbility {
11.     // 读取扩展发来的消息，并回复
12.     async ReadAsync(fdRead:number, fdWrite:number) : Promise<void> {
13.       try {
14.         // read
15.         let arrayBuffer = new ArrayBuffer(1024);
16.         let readLen = await fs.read(fdRead, arrayBuffer);
17.         if (readLen <= 4) {
18.           hilog.error(DOMAIN_NUMBER, TAG, 'read pipe length failed');
19.           return;
20.         }
21.         hilog.info(DOMAIN_NUMBER, TAG, 'read pipe %{public}s', buffer.from(arrayBuffer, 4, readLen - 4).toString());

22.         // write
23.         let strResponse : string = "pong";
24.         const encoder = new util.TextEncoder("utf-8");
25.         const strBytes = encoder.encodeInto(strResponse);
26.         let bufferLen = strBytes.length;
27.         const lenBytes = new Uint8Array(4);
28.         lenBytes[0] = (bufferLen >> 0) & 0xFF;
29.         lenBytes[1] = (bufferLen >> 8) & 0xFF;
30.         lenBytes[2] = (bufferLen >> 16) & 0xFF;
31.         lenBytes[3] = (bufferLen >> 24) & 0xFF;
32.         const writeBuffer = new Uint8Array(4 + bufferLen);
33.         writeBuffer.set(lenBytes, 4);
34.         writeBuffer.set(strBytes, 4);
35.         let writeLen = await fs.write(fdWrite, writeBuffer.buffer);
36.         hilog.info(DOMAIN_NUMBER, TAG, 'write pipe length %{public}d', writeLen);
37.       } catch (err) {
38.         hilog.error(DOMAIN_NUMBER, TAG, 'fs io failed, error code: ' + err.code + " message: " + err.code);
39.       }
40.     }

41.     onConnectNative(info: ConnectionInfo): void {
42.       hilog.info(DOMAIN_NUMBER, TAG,
43.         `onConnectNative, connectionId ${info.connectionId} caller bundle: ${info.bundleName}, extension origin: ${info.extensionOrigin}, pipe Read: ${info.fdRead}, pipe write ${info.fdWrite}  `);
44.       this.ReadAsync(info.fdRead, info.fdWrite)
45.     }

46.     onDisconnectNative(info: ConnectionInfo): void {
47.       hilog.info(DOMAIN_NUMBER, TAG, `onDisconnectNative, connectionId: ${info.connectionId}`);
48.     }

49.     onDestroy(): void {
50.       hilog.info(DOMAIN_NUMBER, TAG, 'onDestroy');
51.     }
52.   };

53. 在工程Module的[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中注册WebNativeMessagingExtensionAbility组件。设置type标签为“webNativeMessaging”，srcEntry标签指向组件代码路径。
    
    1. {
    2.   "module": {
    3.     // ...
    4.     "extensionAbilities": [
    5.       {
    6.         "name": "MyWebNativeMessageExtAbility",
    7.         "description": "webNativeMessaging",
    8.         "type": "webNativeMessaging",
    9.         "exported": true,
    10.         "srcEntry": "./ets/MyWebNativeMessageExtAbility/MyWebNativeMessageExtAbility.ets"
    11.       }
    12.     ]
    13.   }
    14. }
    
54. 在工程Module对应的[module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)中配置crossAppSharedConfig，定义共享配置项，共享配置文件需放置在工程resources/base/profile目录下，并通过$资源访问方式引用。
    

55.   {
56.     "module": {
57.       "crossAppSharedConfig": "$profile:shared_config"
58.     }
59.   }

6.在shared_config.json添加[extension配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-native-messaging#datashare%E5%AD%98%E6%94%BE%E5%8E%9F%E7%94%9F%E5%BA%94%E7%94%A8extension%E9%85%8D%E7%BD%AE%E4%BF%A1%E6%81%AF)

1.   {
2.     "crossAppSharedConfig": [
3.       // ...
4.       {
5.         // uri固定格式，datashardporxy://[包名]/browserNativeMessagingHosts，浏览器应用通过该uri获取的value，即extension配置。
6.         "uri": "datashareproxy://com.example.app/browserNativeMessagingHosts",
7.         // extension配置，格式参考extension配置章节的格式，注意转义字符
8.         "value": "{\"name\": \"com.example.myapplication\",\"description\": \"Send message to native app.\",\"abilityName\": \"MyWebNativeMessageExtAbility\", \"allowed_origins\":[\"chrome-extension://knldjmfmopnpolahpmmgbagdohdnhkik/\"]}",
9.         "allowList": [
10.           // 允许访问的应用appIdentifier, 这里加入具体浏览器的appIdentifier
11.           "1234567890123456789"
12.         ]
13.       }
14.     ]
15.   }

### 实现拉起WebNativeMessagingExtensionAbility（浏览器开发者）

浏览器负责实现扩展runtime接口，拉起WebNativeMessagingExtensionAbility，建立和管理NativeMessaging连接。需要申请权限：ohos.permission.WEB_NATIVE_MESSAGING

1. 当接收到创建NativeMessaging连接时，先通过[应用间配置共享接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-data-datashare#get20)获取目标应用的extension配置。然后读取WebNativeMessagingExtensionAbility名称和允许访问的扩展列表。最后校验是否允许访问。

2.   import { dataShare } from '@kit.ArkData';

3.   interface ExtensionConfig {
4.     abilityName:string;
5.     allowed_origins:string[];
6.   }

7.   async function getManifestData(bundleName:string, connectExtensionOrigin:string) {
8.     try {
9.       // 调用dataShare接口获取extension配置
10.       const dsProxyHelper = await dataShare.createDataProxyHandle();
11.       const urisToGet = [`datashareproxy://${bundleName}/browserNativeMessagingHosts`];
12.       const config : dataShare.DataProxyConfig = {
13.         type: dataShare.DataProxyType.SHARED_CONFIG,
14.       };
15.       const results = await dsProxyHelper.get(urisToGet, config);
16.       let foundValid = false;
17.       for (let i = 0; i < results.length; i++) {
18.         try {
19.           const result = results[i];
20.           const json = result.value;
21.           if (typeof json !== "string") {
22.             continue;
23.           }
24.           let jsonStr:string = json as string;
25.           let info:ExtensionConfig = JSON.parse(jsonStr);
26.           if (info.abilityName) {
27.             console.info('Native message json info is ok');
28.             if (!Array.isArray(info.allowed_origins)) {
29.               info.allowed_origins = [info.allowed_origins];
30.             }
31.             if (!info.allowed_origins.includes(connectExtensionOrigin)) {
32.               console.error('Origin not allowed, continue searching');
33.               continue;
34.             }
35.             foundValid = true;
36.             break;
37.           }
38.         } catch (error) {
39.           console.error('NativeMessage JSON parse error:', error);
40.         }
41.       }
42.       if (!foundValid) {
43.         console.error('NativeMessage JSON no valid manifest found');
44.       } else {
45.         console.info('NativeMessage allowed_origins match ok');
46.       }
47.     } catch (error) {
48.       console.error('Error getting config:', error);
49.     }
50.   }

51. 调用[webNativeMessagingExtensionManager.connectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionmanager#webnativemessagingextensionmanagerconnectnative)创建NativeMessage，如WebNativeMessagingExtensionAbility尚未运行，该接口则会拉起ExtensionAbility并触发。

52.   import { UIAbility, Want, common } from '@kit.AbilityKit';
53.   import { webNativeMessagingExtensionManager } from '@kit.ArkWeb'

54.   class ConnectionCallback implements webNativeMessagingExtensionManager.WebExtensionConnectionCallback {
55.     onConnect(connection:webNativeMessagingExtensionManager.ConnectionNativeInfo) {
56.       // connected
57.       console.error(`onConnect id ${connection.connectionId} is connected`);
58.     }
59.     onDisconnect(connection:webNativeMessagingExtensionManager.ConnectionNativeInfo) {
60.       // disconnect
61.       console.error(`onDisconnect id ${connection.connectionId} is connected`);
62.     }
63.     onFailed(code:webNativeMessagingExtensionManager.NmErrorCode, errMsg:string) {
64.       console.error(`onFailed error code is ${code}, errMsg is ${errMsg}`);
65.     }
66.   }

67.   function connectNative(abilityContext: common.UIAbilityContext, bundleName: string, abilityName: string,
68.     connectExtensionOrigin: string, readPipe: number, writePipe: number) : void {
69.     try {
70.       let wantInfo:Want = {
71.         bundleName: bundleName,
72.         abilityName: abilityName,
73.         parameters: {
74.           'ohos.arkweb.messageReadPipe': { 'type': 'FD', 'value': readPipe },
75.           'ohos.arkweb.messageWritePipe': { 'type': 'FD', 'value': writePipe },
76.           'ohos.arkweb.extensionOrigin': connectExtensionOrigin
77.         },
78.       };

79.       let options : ConnectionCallback = new ConnectionCallback;
80.       let connectId = webNativeMessagingExtensionManager.connectNative(abilityContext, wantInfo, options);
81.       console.info(`innerWebNativeMessageManager  connectionId : ${connectId}` );
82.     } catch (error) {
83.       console.info(`inner callback error Message: ${JSON.stringify(error)}`);
84.     }
85.   }

86. 需要销毁NativeMessaging连接时，调用[webNativeMessagingExtensionManager.disconnectNative](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-web-webnativemessagingextensionmanager#webnativemessagingextensionmanagerdisconnectnative)。

87.   import { webNativeMessagingExtensionManager } from '@kit.ArkWeb'

88.   function disconnencNative(connectId: number) : void {
89.     console.info(`NativeMessageDisconnect start connectionId is ${connectId}`);
90.     webNativeMessagingExtensionManager.disconnectNative(connectId);
91.   }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-offline-mode "使用离线Web组件")