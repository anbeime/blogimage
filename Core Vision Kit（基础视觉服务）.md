# Core Vision Kit简介

更新时间: 2025-12-16 16:27

Core Vision Kit（基础视觉服务）提供了机器视觉相关的基础能力，例如通用文字识别（即OCR，Optical Character Recognition，也称为光学字符识别）、人脸检测、人脸比对以及主体分割等能力。

开发者可以结合[Vision Kit](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-introduction)的UI控件能力（例如：人脸活体检测），提升应用的智能化、便捷化交互体验。

## 场景介绍

Core Vision Kit可应用于各种场景，提升用户体验和应用效率。以下是一些典型的应用场景：

- [通用文字识别](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-text-recognition)：可用于扫描和识别文档、名片、票据等印刷品中的文字内容，方便用户快速录入和存储信息。
- [人脸检测](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-face-detector)：应用于相册管理、照片美化等功能中，也可以用于自动检测和定位照片中的人脸。
- [人脸比对](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-face-comparator)：常用于人脸认证、考勤打卡、门禁系统等需要验证用户身份的场景。
- [主体分割](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-subject-segmentation)：可以检测出图片中区别于背景的前景物体或区域（即“显著主体”），并将其从背景中分离出来，适用于需要识别和提取图像主要信息的场景，广泛使用于前景目标检测和前景主体分离的场景。
- [多目标识别](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-object-detection)：帮助开发者从图片中识别常见的目标对象（动物、植物、建筑物、人、人脸、文本、表格等）并给出位置信息。通常用于端到端业务场景的前置检测功能，根据检测结果完成后续功能业务的入口提示，比如视觉搜索，文本检测。
- [骨骼点检测](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-skeleton-detection)：人体骨骼关键点检测，主要检测人体的一些关键点，通过关键点描述人体骨骼信息。具体应用主要集中在智能视频监控，病人监护系统，人机交互，虚拟现实，人体动画，智能家居，智能安防，运动员辅助训练等等。

## 约束与限制

### 支持的设备

Phone、Tablet、PC/2in1。

### 支持的国家/地区

仅适用于中国境内（不包含中国香港、中国澳门、中国台湾）。

### 能力限制

|AI能力|约束|
|:--|:--|
|文字识别|- 支持的图片格式：JPEG、JPG、PNG。<br>- 支持的语言：简体中文、英文、日文、韩文、繁体中文。<br>- 文本长度：不超过10000字符。<br>- 支持文档印刷体识别，在识别手写字体方面能力有所欠缺。<br>- 输入图像具有合适成像的质量（建议720p以上），100px<高度<15210px，100px<宽度<10000px，高宽比例建议10:1以下（高度小于宽度的10倍），接近手机屏幕高宽比例为宜。<br>- 拍摄角度与文本所在平面垂直方向的夹角应小于30度。|
|人脸检测|- 输入图像具有合适的成像质量（建议720p以上），224px<高度<15210px，100px<宽度<10000px，高宽比例建议10:1以下（高度小于宽度的10倍），接近手机屏幕高宽比例为宜。<br>- 接口调用耗时较久，不适合在需要实时检测的场景下使用。|
|人脸比对|- 当前功能只支持1v1人脸比对。<br>- 输入的两张图像都需要合适的成像质量（建议720p以上），224px<高度<15210px，100px<宽度<10000px，高宽比例建议10:1以下（高度小于宽度的10倍），接近手机屏幕高宽比例为宜。|
|主体分割|- 某个物体占比不小于原图大小的千分之五才会被认定为“主体”，才会支持分割。<br>- 不建议用于处理包含较多文字内容的图片分析场景。<br>- 输入图像具有合适成像的质量（建议720p以上），20px<高度<9000px，20px<宽度<9000px，高宽比例建议3:1以下（高度小于宽度的3倍），接近手机屏幕高宽比例为宜。|
|多目标识别|- 输入图像具有合适成像的质量（建议720p以上），100px<高度<10000px，100px<宽度<10000px，高宽比例建议5:1以下（高度小于宽度的5倍），接近手机屏幕高宽比例为宜。<br>- 图片中的物体占比需要大于0.1%。|
|骨骼点检测|- 输入图像具有合适成像的质量（建议720p以上），100px<高度<10000px，100px<宽度<10000px，高宽比例建议5:1以下（高度小于宽度的5倍），接近手机屏幕高宽比例为宜。|

说明

Core Vision Kit的特性支持多用户同时接入，但是不支持同一用户并发调用同一个特性，如同一个特性被同一进程同一时间多次调用，则返回系统繁忙错误，不同进程调用同一特性，则同一时间只有一个进程业务在处理，其他进程进入队列排队。

## 模拟器支持情况

本kit暂不支持模拟器。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-kit-guide "Core Vision Kit（基础视觉服务）")
# 通用文字识别

更新时间: 2025-12-16 16:27

## 适用场景

通用文字识别，是通过拍照、扫描等光学输入方式，将各种票据、卡证、表格、报刊、书籍等印刷品文字转化为图像信息，再利用文字识别技术将图像信息转化为计算机等设备可以使用的字符信息的技术。

- 可以对文档翻拍、街景翻拍等图片进行文字检测和识别，也可以集成于其他应用中，提供文字检测、识别的功能，并根据识别结果提供翻译、搜索等相关服务。
- 可以处理来自相机、图库等多种来源的图像数据，提供一个自动检测文本、识别图像中文本位置以及文本内容功能的开放能力。
- 支持特定角度范围内的文本倾斜、拍摄角度倾斜、复杂光照条件以及复杂文本背景等场景的文字识别。

效果如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162746.87429070175652717554419374237072:50001231000000:2800:6B908BC0B3607360943E73653ADDA8291A7CE04C767C6EEBE2B021CF51179C20.png)

## 约束与限制

该能力当前不支持模拟器。

|AI能力|约束|
|:--|:--|
|文字识别|- 支持的图片格式：JPEG、JPG、PNG。<br>- 支持的语言：简体中文、英文、日文、韩文、繁体中文。<br>- 文本长度：不超过10000字符。<br>- 支持文档印刷体识别，在识别手写字体方面能力有所欠缺。<br>- 输入图像具有合适成像的质量（建议720p以上），100px<高度<15210px，100px<宽度<10000px，高宽比例建议10:1以下（高度小于宽度的10倍），接近手机屏幕高宽比例为宜。<br>- 拍摄角度与文本所在平面垂直方向的夹角应小于30度。|

## 开发步骤

1. 在使用通用文字识别时，将实现文字识别的相关的类添加至工程。
    
    1. import { textRecognition } from '@kit.CoreVisionKit'
    2. import { image } from '@kit.ImageKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    5. import { fileIo } from '@kit.CoreFileKit';
    6. import { photoAccessHelper } from '@kit.MediaLibraryKit';
    
2. 简单配置页面的布局，并在Button组件添加点击事件，拉起图库，选择图片。
    
    1. Button('选择图片')
    2.   .type(ButtonType.Capsule)
    3.   .fontColor(Color.White)
    4.   .alignSelf(ItemAlign.Center)
    5.   .width('80%')
    6.   .margin(10)
    7.   .onClick(() => {
    8.     // 拉起图库，获取图片资源
    9.     this.selectImage();
    10.   })
    
3. 通过图库获取图片资源，将图片转换为[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)，并添加初始化和释放方法。
    
    1. async aboutToAppear(): Promise<void> {
    2.   const initResult = await textRecognition.init();
    3.   hilog.info(0x0000, 'OCRDemo', `OCR service initialization result:${initResult}`);
    4. }
    
    5. async aboutToDisappear(): Promise<void> {
    6.   await textRecognition.release();
    7.   hilog.info(0x0000, 'OCRDemo', 'OCR service released successfully');
    8. }
    
    9. private async selectImage() {
    10.   let uri = await this.openPhoto();
    11.   if (uri === undefined) {
    12.     hilog.error(0x0000, 'OCRDemo', "Failed to get uri.");
    13.     return;
    14.   }
    15.   this.loadImage(uri);
    16. }
    
    17. private openPhoto(): Promise<string> {
    18.   return new Promise<string>((resolve) => {
    19.     let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
    20.     photoPicker.select({
    21.       MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE,
    22.       maxSelectNumber: 1
    23.     }).then((res: photoAccessHelper.PhotoSelectResult) => {
    24.       resolve(res.photoUris[0]);
    25.     }).catch((err: BusinessError) => {
    26.       hilog.error(0x0000, 'OCRDemo', `Failed to get photo image uri. code: ${err.code}, message: ${err.message}`);
    27.       resolve('');
    28.     })
    29.   })
    30. }
    
    31. private loadImage(name: string) {
    32.   setTimeout(async () => {
    33.     let imageSource: image.ImageSource | undefined = undefined;
    34.     let fileSource = await fileIo.open(name, fileIo.OpenMode.READ_ONLY);
    35.     imageSource = image.createImageSource(fileSource.fd);
    36.     this.chooseImage = await imageSource.createPixelMap();
    37.   }, 100)
    38. }
    
4. 实例化[VisionInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/core-vision-text-recognition-api#section674171818172)对象，并传入待检测图片的[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)。
    
    VisionInfo为待OCR检测识别的入参项，目前仅支持[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)类型的视觉信息。
    
    1. let visionInfo: textRecognition.VisionInfo = {
    2.   pixelMap: this.chooseImage
    3. };
    
5. 配置通用文本识别的配置项[TextRecognitionConfiguration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/core-vision-text-recognition-api#section1081123302517)，用于配置是否支持朝向检测。
    
    1. let textConfiguration: textRecognition.TextRecognitionConfiguration = {
    2.   isDirectionDetectionSupported: false
    3. };
    
6. 调用textRecognition的[recognizeText](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/core-vision-text-recognition-api#section1446761711464)接口，对识别到的结果进行处理。
    
    当调用成功时，获取文字识别的结果；调用失败时，将返回对应错误码。
    
    recognizeText接口提供了三种调用形式，当前以其中一种作为示例，其他方式可参考[API文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/core-vision-text-recognition-api)。
    
    1. textRecognition.recognizeText(visionInfo, textConfiguration)
    2.   .then((data: textRecognition.TextRecognitionResult) => {
    3.     // 识别成功，获取对应的结果
    4.     let recognitionString = JSON.stringify(data);
    5.     hilog.info(0x0000, 'OCRDemo', `Succeeded in recognizing text: ${recognitionString}`);
    6.     // 将结果更新到Text中显示
    7.     this.dataValues = data.value;
    8.   })
    9.   .catch((error: BusinessError) => {
    10.     hilog.error(0x0000, 'OCRDemo', `Failed to recognize text. Code: ${error.code}, message: ${error.message}`);
    11.     this.dataValues = `Error: ${error.message}`;
    12.   });
    

## 开发实例

点击按钮，识别一张图片的文字内容，并通过日志打印。

### Index.ets

1. import { textRecognition } from '@kit.CoreVisionKit'
2. import { image } from '@kit.ImageKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';
4. import { BusinessError } from '@kit.BasicServicesKit';
5. import { fileIo } from '@kit.CoreFileKit';
6. import { photoAccessHelper } from '@kit.MediaLibraryKit';

7. @Entry
8. @Component
9. struct Index {
10.   private imageSource: image.ImageSource | undefined = undefined;
11.   @State chooseImage: PixelMap | undefined = undefined;
12.   @State dataValues: string = '';

13.   async aboutToAppear(): Promise<void> {
14.     const initResult = await textRecognition.init();
15.     hilog.info(0x0000, 'OCRDemo', `OCR service initialization result:${initResult}`);
16.   }

17.   async aboutToDisappear(): Promise<void> {
18.     await textRecognition.release();
19.     hilog.info(0x0000, 'OCRDemo', 'OCR service released successfully');
20.   }

21.   build() {
22.     Column() {
23.       Image(this.chooseImage)
24.         .objectFit(ImageFit.Fill)
25.         .height('60%')

26.       Text(this.dataValues)
27.         .copyOption(CopyOptions.LocalDevice)
28.         .height('15%')
29.         .margin(10)
30.         .width('60%')

31.       Button('选择图片')
32.         .type(ButtonType.Capsule)
33.         .fontColor(Color.White)
34.         .alignSelf(ItemAlign.Center)
35.         .width('80%')
36.         .margin(10)
37.         .onClick(() => {
38.           // 拉起图库，获取图片资源
39.           this.selectImage();
40.         })

41.       Button('开始识别')
42.         .type(ButtonType.Capsule)
43.         .fontColor(Color.White)
44.         .alignSelf(ItemAlign.Center)
45.         .width('80%')
46.         .margin(10)
47.         .onClick(async () => {
48.           this.textRecognitionTest();
49.         })
50.     }
51.     .width('100%')
52.     .height('100%')
53.     .justifyContent(FlexAlign.Center)
54.   }

55.   private textRecognitionTest() {
56.     if (!this.chooseImage) {
57.       return;
58.     }
59.     // 调用文本识别接口
60.     let visionInfo: textRecognition.VisionInfo = {
61.       pixelMap: this.chooseImage
62.     };
63.     let textConfiguration: textRecognition.TextRecognitionConfiguration = {
64.       isDirectionDetectionSupported: false
65.     };
66.     textRecognition.recognizeText(visionInfo, textConfiguration)
67.       .then((data: textRecognition.TextRecognitionResult) => {
68.         // 识别成功，获取对应的结果
69.         let recognitionString = JSON.stringify(data);
70.         hilog.info(0x0000, 'OCRDemo', `Succeeded in recognizing text: ${recognitionString}`);
71.         // 将结果更新到Text中显示
72.         this.dataValues = data.value;
73.       })
74.       .catch((error: BusinessError) => {
75.         hilog.error(0x0000, 'OCRDemo', `Failed to recognize text. Code: ${error.code}, message: ${error.message}`);
76.         this.dataValues = `Error: ${error.message}`;
77.       });
78.   }

79.   private async selectImage() {
80.     let uri = await this.openPhoto();
81.     if (uri === undefined) {
82.       hilog.error(0x0000, 'OCRDemo', "Failed to get uri.");
83.       return;
84.     }
85.     this.loadImage(uri);
86.   }

87.   private openPhoto(): Promise<string> {
88.     return new Promise<string>((resolve) => {
89.       let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
90.       photoPicker.select({
91.         MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE,
92.         maxSelectNumber: 1
93.       }).then((res: photoAccessHelper.PhotoSelectResult) => {
94.         resolve(res.photoUris[0]);
95.       }).catch((err: BusinessError) => {
96.         hilog.error(0x0000, 'OCRDemo', `Failed to get photo image uri. code: ${err.code}, message: ${err.message}`);
97.         resolve('');
98.       })
99.     })
100.   }

101.   private loadImage(name: string) {
102.     setTimeout(async () => {
103.       try {
104.         let fileSource = await fileIo.open(name, fileIo.OpenMode.READ_ONLY);
105.         this.imageSource = image.createImageSource(fileSource.fd);
106.         this.chooseImage = await this.imageSource.createPixelMap();
107.         await fileIo.close(fileSource);
108.       } catch (error) {
109.         hilog.error(0x0000, 'OCRDemo', `Failed to open file. Error: ${error}`);
110.       }
111.     }, 100)
112.   }
113. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-introduction "Core Vision Kit简介")
# 人脸检测

更新时间: 2025-12-16 16:27

## 适用场景

检测图片中的人脸，返回高精度人脸矩形框坐标、人脸五官位置、人脸朝向、人脸置信度。可通过对人脸的定位，实现对人脸特定位置的美化修饰。广泛应用于各类人脸识别场景，如人脸聚类、美颜等场景中。

效果如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162747.86099192346891690876783851066669:50001231000000:2800:23B4F3AB398D883533B116763643644BF0427490DFF598B09D3128BE3596062E.png)

## 约束与限制

该能力当前不支持模拟器。

|AI能力|约束|
|:--|:--|
|人脸检测|- 输入图像具有合适的成像质量（建议720p以上），224px<高度<15210px，100px<宽度<10000px，高宽比例建议10:1以下（高度小于宽度的10倍），接近手机屏幕高宽比例为宜。<br>- 接口调用耗时较久，不适合在需要实时检测的场景下使用。<br>- 不支持同一用户启用多个线程。|

## 世界坐标系

以下方图片指示坐标系辅助表示人脸朝向。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162747.89948635126402158244657351463714:50001231000000:2800:181BD970D7BA3196B2464A46E10939B045C1BA127CC7E8B838E74F3406D34DF6.png)

## 开发步骤

1. 在使用人脸检测时，将实现人脸检测相关的类添加至工程。
    
    1. import { faceDetector } from '@kit.CoreVisionKit';
    2. import { image } from '@kit.ImageKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    5. import { fileIo } from '@kit.CoreFileKit';
    6. import { photoAccessHelper } from '@kit.MediaLibraryKit';
    
2. 简单配置页面的布局，并在Button组件添加点击事件，拉起图库，选择图片。
    
    1. Button('选择图片')
    2.   .type(ButtonType.Capsule)
    3.   .fontColor(Color.White)
    4.   .alignSelf(ItemAlign.Center)
    5.   .width('80%')
    6.   .margin(10)
    7.   .onClick(() => {
    8.     // 拉起图库，获取图片资源
    9.     this.selectImage();
    10.   })
    
3. 通过图库获取图片资源，将图片转换为[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)。
    
    1. private async selectImage() {
    2.   let uri = await this.openPhoto()
    3.   if (uri === undefined) {
    4.     hilog.error(0x0000, 'faceDetector', "Failed to get uri.");
    5.   }
    6.   this.loadImage(uri)
    7. }
    
    8. private openPhoto(): Promise<string> {
    9.   return new Promise<string>((resolve) => {
    10.     let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
    11.     photoPicker.select({
    12.       MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE, 
    13.       maxSelectNumber: 1
    14.     }).then(res => {
    15.       resolve(res.photoUris[0])
    16.     }).catch((err: BusinessError) => {
    17.       hilog.error(0x0000, 'faceDetector', `Failed to get photo image uri.code: ${err.code}, message: ${err.message}`);
    18.       resolve('');
    19.     })
    20.   })
    21. }
    
    22. private loadImage(name: string) {
    23.   setTimeout(async () => {
    24.     let imageSource: image.ImageSource | undefined = undefined;
    25.     let fileSource = await fileIo.open(name, fileIo.OpenMode.READ_ONLY);
    26.     imageSource = image.createImageSource(fileSource.fd);
    27.     this.chooseImage = await imageSource.createPixelMap();
    28.     this.dataValues = "";
    29.   }, 100
    30.   )
    31. }
    
4. 实例化[VisionInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/core-vision-face-detector-api#section14488135133518)对象，并传入待检测图片的[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)，实现人脸检测功能。
    
    1. // 初始化并调用人脸检测接口
    2. faceDetector.init();
    3. let visionInfo: faceDetector.VisionInfo = {
    4.   pixelMap: this.chooseImage,
    5. };
    6. let data:faceDetector.Face[] = await faceDetector.detect(visionInfo);
    
5. （可选）如果需要将结果展示在界面上，可以使用下列代码。
    
    1. let data:faceDetector.Face[] = await faceDetector.detect(visionInfo);
    2. if (data.length === 0) {
    3.   this.dataValues = "No face is detected in the image. Select an image that contains a face.";
    4. } else {
    5.   let faceString = JSON.stringify(data);
    6.   hilog.info(0x0000, 'testTag', "faceString data is " + faceString);
    7.   this.dataValues = faceString;
    8. }
    

## 开发实例

### Index.ets

1. import { faceDetector } from '@kit.CoreVisionKit';
2. import { image } from '@kit.ImageKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';
4. import { BusinessError } from '@kit.BasicServicesKit';
5. import { fileIo } from '@kit.CoreFileKit';
6. import { photoAccessHelper } from '@kit.MediaLibraryKit';

7. @Entry
8. @Component
9. struct Index {
10.   @State chooseImage: PixelMap | undefined = undefined
11.   @State dataValues: string = ''

12.   build() {
13.     Column() {
14.       Image(this.chooseImage)
15.         .objectFit(ImageFit.Fill)
16.         .height('60%')
17.       Text(this.dataValues)
18.         .copyOption(CopyOptions.LocalDevice)
19.         .height('15%')
20.         .margin(10)
21.         .width('60%')
22.       Button('选择图片')
23.         .type(ButtonType.Capsule)
24.         .fontColor(Color.White)
25.         .alignSelf(ItemAlign.Center)
26.         .width('80%')
27.         .margin(10)
28.         .onClick(() => {
29.           // 拉起图库
30.           this.selectImage()
31.         })
32.       Button('人脸检测')
33.         .type(ButtonType.Capsule)
34.         .fontColor(Color.White)
35.         .alignSelf(ItemAlign.Center)
36.         .width('80%')
37.         .margin(10)
38.         .onClick(() => {
39.           if(!this.chooseImage) {
40.             hilog.error(0x0000, 'faceDetectorSample', "Failed to detect face.");
41.             return;
42.           }
43.           // 调用人脸检测接口
44.           faceDetector.init();
45.           let visionInfo: faceDetector.VisionInfo = {
46.             pixelMap: this.chooseImage,
47.           };
48.           faceDetector.detect(visionInfo)
49.             .then((data: faceDetector.Face[]) => {
50.               if (data.length === 0) {
51.                 this.dataValues = "No face is detected in the image. Select an image that contains a face.";
52.               } else {
53.                 let faceString = JSON.stringify(data);
54.                 hilog.info(0x0000, 'faceDetectorSample', "faceString data is " + faceString);
55.                 this.dataValues = faceString;
56.               }
57.             })
58.             .catch((error: BusinessError) => {
59.               hilog.error(0x0000, 'faceDetectorSample', `Face detection failed. Code: ${error.code}, message: ${error.message}`);
60.               this.dataValues = `Error: ${error.message}`;
61.             });
62.           faceDetector.release();
63.         })
64.     }
65.     .width('100%')
66.     .height('100%')
67.     .justifyContent(FlexAlign.Center)
68.   }

69.   private async selectImage() {
70.     let uri = await this.openPhoto()
71.     if (uri === undefined) {
72.       hilog.error(0x0000, 'faceDetectorSample', "Failed to get uri.");
73.     }
74.     this.loadImage(uri);
75.   }

76.   private openPhoto(): Promise<string> {
77.     return new Promise<string>((resolve) => {
78.       let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
79.       photoPicker.select({
80.         MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE,
81.         maxSelectNumber: 1
82.       }).then(res => {
83.         resolve(res.photoUris[0])
84.       }).catch((err: BusinessError) => {
85.         hilog.error(0x0000, 'faceDetectorSample', `Failed to get photo image uri.code: ${err.code}, message: ${err.message}`);
86.         resolve('');
87.       })
88.     })
89.   }

90.   private loadImage(name: string) {
91.     setTimeout(async () => {
92.       let imageSource: image.ImageSource | undefined = undefined;
93.       try {
94.         let fileSource = await fileIo.open(name, fileIo.OpenMode.READ_ONLY);
95.         imageSource = image.createImageSource(fileSource.fd);
96.         this.chooseImage = await imageSource.createPixelMap();
97.         this.dataValues = "";
98.         await fileIo.close(fileSource);
99.       } catch (error) {
100.         hilog.error(0x0000, 'faceDetectorSample', `Failed to open file. Error: ${error}`);
101.       }
102.     }, 100
103.     )
104.   }
105. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-text-recognition "通用文字识别")
# 人脸比对

更新时间: 2025-12-16 16:27

## 适用场景

输入的两张比对图片是同一个人的照片时，系统返回的比对结果为"同一个人"，置信分数比较高；当两张比对图片不是同一个人的照片时，系统返回的比对结果为"非同一个人"，置信分数很低。可以用于APP中需要用到人脸比对功能的场景，比如娱乐类APP中比较两个人的相似度、与明星的相似度等。

效果如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162748.73000281969938087512543694561890:50001231000000:2800:F0BA6FDD2BB31C1544631936C1B97F27C75DF30B979D4A3B57E9F899788562BA.png)

## 约束与限制

该能力当前不支持模拟器。

|AI能力|约束|
|:--|:--|
|人脸比对|- 当前功能只支持1v1人脸比对。<br>- 输入的两张图像都需要合适的成像质量（建议720p以上），224px<高度<15210px，100px<宽度<10000px，高宽比例建议10:1以下（高度小于宽度的10倍），接近手机屏幕高宽比例为宜。|

## 开发步骤

1. 在使用人脸比对时，将实现人脸比对相关的类添加至工程。
    
    import { faceComparator } from '@kit.CoreVisionKit';
    import { image } from '@kit.ImageKit';
    import { hilog } from '@kit.PerformanceAnalysisKit';
    import { BusinessError } from '@kit.BasicServicesKit';
    import { fileIo } from '@kit.CoreFileKit';
    import { photoAccessHelper } from '@kit.MediaLibraryKit';
    
2. 简单配置页面的布局，并在Button组件添加点击事件，拉起图库，选择图片。
    
    Button('选择图片')
      .type(ButtonType.Capsule)
      .fontColor(Color.White)
      .alignSelf(ItemAlign.Center)
      .width('80%')
      .margin(10)
      .onClick(() => {
        // 拉起图库，获取图片资源
        this.selectImage();
      })
    
3. 通过图库获取图片资源，将图片转换为[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)，并添加初始化和释放方法。
    
    async aboutToAppear(): Promise<void> {
      const initResult = await faceComparator.init();
      hilog.info(0x0000, TAG, `Face comparator initialization result:${initResult}`);
    }
    
    async aboutToDisappear(): Promise<void> {
      await faceComparator.release();
      hilog.info(0x0000, TAG, 'Face comparator released successfully');
    }
    
    private async selectImage() {
      let uri = await this.openPhoto()
      if (uri === undefined) {
        hilog.error(0x0000, 'faceCompare', "Failed to get two image uris.");
      }
      this.loadImage(uri);
    }
    
    private openPhoto(): Promise<string[]> {
      return new Promise<string[]>((resolve, reject) => {
        let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
        photoPicker.select({
          MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE,
          maxSelectNumber: 2
        }).then(res => {
          resolve(res.photoUris);
        }).catch((err: BusinessError) => {
          hilog.error(0x0000, TAG, `Failed to get photo image uris. code: ${err.code}, message: ${err.message}`);
          reject();
        });
      });
    }
    
    private loadImage(names: string[]) {
      setTimeout(async () => {
        let imageSource: image.ImageSource | undefined = undefined;
        let fileSource = await fileIo.open(names[0], fileIo.OpenMode.READ_ONLY);
        imageSource = image.createImageSource(fileSource.fd);
        this.chooseImage = await imageSource.createPixelMap();
        fileSource = await fileIo.open(names[1], fileIo.OpenMode.READ_ONLY);
        imageSource = image.createImageSource(fileSource.fd);
        this.chooseImage1 = await imageSource.createPixelMap();
      }, 100
      )
    }
    
4. 实现人脸比对功能。实例化[VisionInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/core-vision-facecomparator-api#section674171818172)对象，传入两张图片的[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)，调用[faceComparator.compareFaces](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/core-vision-facecomparator-api#section16178105410532)方法进行人脸比对。
    
    // 调用人脸比对接口
    let visionInfo: faceComparator.VisionInfo = {
      pixelMap: this.chooseImage,
    };
    let visionInfo1: faceComparator.VisionInfo = {
      pixelMap: this.chooseImage1,
    };
    let data:faceComparator.FaceCompareResult = await faceComparator.compareFaces(visionInfo, visionInfo1);
    
5. （可选）如果需要将结果展示在界面上，可以用下列代码。
    
    let data:faceComparator.FaceCompareResult = await faceComparator.compareFaces(visionInfo, visionInfo1);
    let faceString = "degree of similarity: "+ this.toPercentage(data.similarity)+((data.isSamePerson)?". is":". no")+ " same person";
    hilog.info(0x0000, 'testTag', "faceString data is " + faceString);
    this.dataValues = faceString;
    

## 开发实例

### Index.ets

import { faceComparator } from '@kit.CoreVisionKit';
import { image } from '@kit.ImageKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { fileIo } from '@kit.CoreFileKit';
import { photoAccessHelper } from '@kit.MediaLibraryKit';

const TAG: string = "FaceCompareSample";

@Entry
@Component
struct Index {
  @State chooseImage: PixelMap | undefined = undefined
  @State chooseImage1: PixelMap | undefined = undefined
  @State dataValues: string = ''

  async aboutToAppear(): Promise<void> {
    const initResult = await faceComparator.init();
    hilog.info(0x0000, TAG, `Face comparator initialization result:${initResult}`);
  }

  async aboutToDisappear(): Promise<void> {
    await faceComparator.release();
    hilog.info(0x0000, TAG, 'Face comparator released successfully');
  }

  build() {
    Column() {
      Image(this.chooseImage)
        .objectFit(ImageFit.Fill)
        .height('30%')
        .accessibilityDescription("默认图片1")
      Image(this.chooseImage1)
        .objectFit(ImageFit.Fill)
        .height('30%')
        .accessibilityDescription("默认图片2")
      Text(this.dataValues)
        .copyOption(CopyOptions.LocalDevice)
        .height('15%')
        .margin(10)
        .width('60%')
      Button('选择图片')
        .type(ButtonType.Capsule)
        .fontColor(Color.White)
        .alignSelf(ItemAlign.Center)
        .width('80%')
        .margin(10)
        .onClick(() => {
          // 拉起图库
          this.selectImage()
        })
      Button('人脸比对')
        .type(ButtonType.Capsule)
        .fontColor(Color.White)
        .alignSelf(ItemAlign.Center)
        .width('80%')
        .margin(10)
        .onClick(() => {
          if(!this.chooseImage || !this.chooseImage1) {
            hilog.error(0x0000, TAG, "Failed to choose image");
            return;
          }
          // 调用人脸比对接口
          let visionInfo: faceComparator.VisionInfo = {
            pixelMap: this.chooseImage,
          };
          let visionInfo1: faceComparator.VisionInfo = {
            pixelMap: this.chooseImage1,
          };
          faceComparator.compareFaces(visionInfo, visionInfo1)
            .then((data: faceComparator.FaceCompareResult) => {
              let faceString = "degree of similarity: "+ this.toPercentage(data.similarity)+((data.isSamePerson)?". is":". no")+ " same person";
              hilog.info(0x0000, TAG, "faceString data is " + faceString);
              this.dataValues = faceString;
            })
            .catch((error: BusinessError) => {
              hilog.error(0x0000, TAG, `Face comparison failed. Code: ${error.code}, message: ${error.message}`);
              this.dataValues = `Error: ${error.message}`;
            });
        })
    }
    .width('100%')
    .height('100%')
    .justifyContent(FlexAlign.Center)
  }

  private toPercentage(num: number): string {
    return `${(num * 100).toFixed(2)}%`;
  }

  private async selectImage() {
    let uri = await this.openPhoto()
    if (uri === undefined) {
      hilog.error(0x0000, TAG, "Failed to get two image uris.");
    }
    this.loadImage(uri);
  }

  private openPhoto(): Promise<string[]> {
    return new Promise<string[]>((resolve, reject) => {
      let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
      photoPicker.select({
        MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE,
        maxSelectNumber: 2
      }).then(res => {
        resolve(res.photoUris);
      }).catch((err: BusinessError) => {
        hilog.error(0x0000, TAG, `Failed to get photo image uris. code: ${err.code}, message: ${err.message}`);
        reject();
      });
    });
  }

  private loadImage(names: string[]) {
    setTimeout(async () => {
      let imageSource: image.ImageSource | undefined = undefined;
      let fileSource: fileIo.File
      try {
        fileSource = await fileIo.open(names[0], fileIo.OpenMode.READ_ONLY);
        imageSource = image.createImageSource(fileSource.fd);
        this.chooseImage = await imageSource.createPixelMap();
      } catch (error) {
        hilog.error(0x0000, TAG, `Failed to open file. Error: ${error}`);
      }
      try {
        fileSource = await fileIo.open(names[1], fileIo.OpenMode.READ_ONLY);
        imageSource = image.createImageSource(fileSource.fd);
        this.chooseImage1 = await imageSource.createPixelMap();
        await fileIo.close(fileSource);
      } catch (error) {
        hilog.error(0x0000, TAG, `Failed to open the second file. Error: ${error}`);
      }
    }, 100
    )
  }
}

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-face-detector "人脸检测")
# 主体分割

更新时间: 2025-12-16 16:27

## 适用场景

主体分割，可以检测出图片中区别于背景的前景物体或区域（即“显著主体”），并将其从背景中分离出来，适用于需要识别和提取图像主要信息的场景，广泛使用于前景目标检测和前景主体分离的场景。例如：

- 主体贴纸，从图片中提取显著性的主体，去掉背景。
- 背景替换，替换并提取出主体对象的背景。
- 显著性检测，快速定位图片中显著性区域。
- 辅助图片编辑，例如单独对主体进行美化处理。

效果如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162748.66848167217586112920524506200830:50001231000000:2800:99A641E58F536C217B45434F0F053206A67B7752E35D385B81B7F222671C90AE.png)

## 约束与限制

该能力当前不支持模拟器。

|AI能力|约束|
|:--|:--|
|主体分割|- 某个物体占比不小于原图大小的千分之五才会被认定为“主体”，才会支持分割。<br>- 不建议用于处理包含较多文字内容的图片分析场景。<br>- 输入图像具有合适成像的质量（建议720p以上），20px<高度<9000px，20px<宽度<9000px，高宽比例建议3:1以下（高度小于宽度的3倍），接近手机屏幕高宽比例为宜。|

## 开发步骤

1. 引用相关类添加至工程。
    
    1. import { subjectSegmentation } from '@kit.CoreVisionKit';
    2. import { image } from '@kit.ImageKit';
    3. import { hilog } from '@kit.PerformanceAnalysisKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    5. import { fileIo } from '@kit.CoreFileKit';
    6. import { photoAccessHelper } from '@kit.MediaLibraryKit';
    
2. 准备预处理的图片资源，将图片转换为[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)，并添加初始化和释放方法。
    
    1. async aboutToAppear(): Promise<void> {
    2.   const initResult = await subjectSegmentation.init();
    3.   hilog.info(0x0000, 'subjectSegmentationSample', `Subject segmentation initialization result:${initResult}`);
    4. }
    
    5. async aboutToDisappear(): Promise<void> {
    6.   await subjectSegmentation.release();
    7.   hilog.info(0x0000, 'subjectSegmentationSample', 'Subject segmentation released successfully');
    8. }
    
    9. private async selectImage() {
    10.   let uri = await this.openPhoto()
    11.   if (uri === undefined) {
    12.     hilog.error(0x0000, TAG, "uri is undefined");
    13.   }
    14.   this.loadImage(uri);
    15. }
    
    16. private openPhoto(): Promise<Array<string>> {
    17.   return new Promise<Array<string>>((resolve, reject) => {
    18.     let PhotoSelectOptions = new photoAccessHelper.PhotoSelectOptions();
    19.     PhotoSelectOptions.MIMEType = photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE;
    20.     PhotoSelectOptions.maxSelectNumber = 1;
    21.     let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
    22.     hilog.info(0x0000, TAG, 'PhotoViewPicker.select successfully, PhotoSelectResult uri: ');
    23.     photoPicker.select(PhotoSelectOptions).then((PhotoSelectResult) => {
    24.       hilog.info(0x0000, TAG, `PhotoViewPicker.select successfully, PhotoSelectResult uri: ${PhotoSelectResult.photoUris}`);
    25.       resolve(PhotoSelectResult.photoUris)
    26.     }).catch((err: BusinessError) => {
    27.       hilog.error(0x0000, TAG, `PhotoViewPicker.select failed with errCode: ${err.code}, errMessage: ${err.message}`);
    28.       reject();
    29.     });
    30.   })
    31. }
    
    32. private loadImage(names: string[]) {
    33.   setTimeout(async () => {
    34.     let imageSource: image.ImageSource | undefined = undefined
    35.     let fileSource = await fileIo.open(names[0], fileIo.OpenMode.READ_ONLY)
    36.     imageSource = image.createImageSource(fileSource.fd)
    37.     this.chooseImage = await imageSource.createPixelMap()
    38.   }, 100
    39.   )
    40. }
    
3. 实例化待分割的入参项[VisionInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/core-vision-subjectsegmentation-api#section674171818172)，并传入待检测图片的[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)。
    
    1. let visionInfo: subjectSegmentation.VisionInfo = {
    2.   pixelMap: this.chooseImage,
    3. };
    
4. 配置通用文本识别的配置项[SegmentationConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/core-vision-subjectsegmentation-api#section1268211401742)，包括最大分割主体个数、是否输出每个主体的分割信息，以及是否输出分割后的前景图。
    
    1. let config: subjectSegmentation.SegmentationConfig = {
    2.   maxCount: parseInt(this.maxNum),
    3.   enableSubjectDetails: true,
    4.   enableSubjectForegroundImage: true,
    5. };
    
5. 调用subjectSegmentation的[subjectSegmentation.doSegmentation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/core-vision-subjectsegmentation-api#section3410243584)接口，实现主体分割。
    
    1. let data: subjectSegmentation.SegmentationResult = await subjectSegmentation.doSegmentation(visionInfo, config);
    2. let outputString = `Subject count: ${data.subjectCount}\n`;
    3. outputString += `Max subject count: ${config.maxCount}\n`;
    4. outputString += `Enable subject details: ${config.enableSubjectDetails ? 'Yes' : 'No'}\n\n`;
    5. let segBox : subjectSegmentation.Rectangle = data.fullSubject.subjectRectangle;
    6. let segBoxString = `Full subject box:\nLeft: ${segBox.left}, Top: ${segBox.top}, Width: ${segBox.width}, Height: ${segBox.height}\n\n`;
    7. outputString += segBoxString;
    
    8. if (config.enableSubjectDetails) {
    9.   outputString += 'Individual subject boxes:\n';
    10.   if (data.subjectDetails) {
    11.     for (let i = 0; i < data.subjectDetails.length; i++) {
    12.       let detailSegBox: subjectSegmentation.Rectangle = data.subjectDetails[i].subjectRectangle;
    13.       outputString += `Subject ${i + 1}:\nLeft: ${detailSegBox.left}, Top: ${detailSegBox.top}, Width: ${detailSegBox.width}, Height: ${detailSegBox.height}\n\n`;
    14.     }
    15.   }
    16. }
    

## 开发实例

### Index.ets

1. import { subjectSegmentation } from '@kit.CoreVisionKit';
2. import { image } from '@kit.ImageKit';
3. import { hilog } from '@kit.PerformanceAnalysisKit';
4. import { BusinessError } from '@kit.BasicServicesKit';
5. import { fileIo } from '@kit.CoreFileKit';
6. import { photoAccessHelper } from '@kit.MediaLibraryKit';

7. const TAG: string = "ImageSegmentationSample";

8. @Entry
9. @Component
10. struct Index {
11.   @State chooseImage: PixelMap | undefined = undefined
12.   @State dataValues: string = ''
13.   @State segmentedImage: PixelMap | undefined = undefined
14.   @State maxNum: string = '20'

15.   build() {
16.     Column() {
17.       Image(this.chooseImage)
18.         .objectFit(ImageFit.Fill)
19.         .height('30%')
20.         .accessibilityDescription("Image to be segmented")

21.       Scroll() {
22.         Text(this.dataValues)
23.           .copyOption(CopyOptions.LocalDevice)
24.           .margin(10)
25.           .width('100%')
26.       }
27.       .height('20%')

28.       Image(this.segmentedImage)
29.         .objectFit(ImageFit.Fill)
30.         .height('30%')
31.         .accessibilityDescription("Segmented subject image")

32.       Row() {
33.         Text('Max subject count:')
34.           .fontSize(16)
35.         TextInput({ placeholder: 'Enter max subject count', text: this.maxNum })
36.           .type(InputType.Number)
37.           .placeholderColor(Color.Gray)
38.           .fontSize(16)
39.           .backgroundColor(Color.White)
40.           .onChange((value: string) => {
41.             this.maxNum = value
42.           })
43.       }
44.       .width('80%')
45.       .margin(10)

46.       Button('Select Image')
47.         .type(ButtonType.Capsule)
48.         .fontColor(Color.White)
49.         .alignSelf(ItemAlign.Center)
50.         .width('80%')
51.         .margin(10)
52.         .onClick(() => {
53.           this.selectImage()
54.         })

55.       Button('Image Segmentation')
56.         .type(ButtonType.Capsule)
57.         .fontColor(Color.White)
58.         .alignSelf(ItemAlign.Center)
59.         .width('80%')
60.         .margin(10)
61.         .onClick(() => {
62.           if (!this.chooseImage) {
63.             hilog.error(0x0000, TAG, "imageSegmentation not have chooseImage");
64.             return
65.           }
66.           let visionInfo: subjectSegmentation.VisionInfo = {
67.             pixelMap: this.chooseImage,
68.           };
69.           let config: subjectSegmentation.SegmentationConfig = {
70.             maxCount: parseInt(this.maxNum),
71.             enableSubjectDetails: true,
72.             enableSubjectForegroundImage: true,
73.           };
74.           subjectSegmentation.doSegmentation(visionInfo, config)
75.             .then((data: subjectSegmentation.SegmentationResult) => {
76.               let outputString = `Subject count: ${data.subjectCount}\n`;
77.               outputString += `Max subject count: ${config.maxCount}\n`;
78.               outputString += `Enable subject details: ${config.enableSubjectDetails ? 'Yes' : 'No'}\n\n`;
79.               let segBox : subjectSegmentation.Rectangle = data.fullSubject.subjectRectangle;
80.               let segBoxString = `Full subject box:\nLeft: ${segBox.left}, Top: ${segBox.top}, Width: ${segBox.width}, Height: ${segBox.height}\n\n`;
81.               outputString += segBoxString;

82.               if (config.enableSubjectDetails) {
83.                 outputString += 'Individual subject boxes:\n';
84.                 if (data.subjectDetails) {
85.                   for (let i = 0; i < data.subjectDetails.length; i++) {
86.                     let detailSegBox: subjectSegmentation.Rectangle = data.subjectDetails[i].subjectRectangle;
87.                     outputString += `Subject ${i + 1}:\nLeft: ${detailSegBox.left}, Top: ${detailSegBox.top}, Width: ${detailSegBox.width}, Height: ${detailSegBox.height}\n\n`;
88.                   }
89.                 }
90.               }

91.               hilog.info(0x0000, TAG, "Segmentation result: " + outputString);
92.               this.dataValues = outputString;

93.               if (data.fullSubject && data.fullSubject.foregroundImage) {
94.                 this.segmentedImage = data.fullSubject.foregroundImage;
95.               } else {
96.                 hilog.warn(0x0000, TAG, "No foreground image in segmentation result");
97.               }
98.             })
99.             .catch((error: BusinessError) => {
100.               hilog.error(0x0000, TAG, `Image segmentation failed errCode: ${error.code}, errMessage: ${error.message}`);
101.               this.dataValues = `Error: ${error.message}`;
102.               this.segmentedImage = undefined;
103.             });
104.         })
105.     }
106.     .width('100%')
107.     .height('80%')
108.     .justifyContent(FlexAlign.Center)
109.   }

110.   private async selectImage() {
111.     let uri = await this.openPhoto()
112.     if (uri === undefined) {
113.       hilog.error(0x0000, TAG, "uri is undefined");
114.     }
115.     this.loadImage(uri);
116.   }

117.   private openPhoto(): Promise<Array<string>> {
118.     return new Promise<Array<string>>((resolve, reject) => {
119.       let PhotoSelectOptions = new photoAccessHelper.PhotoSelectOptions();
120.       PhotoSelectOptions.MIMEType = photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE;
121.       PhotoSelectOptions.maxSelectNumber = 1;
122.       let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
123.       photoPicker.select(PhotoSelectOptions).then((PhotoSelectResult) => {
124.         hilog.info(0x0000, TAG, `PhotoViewPicker.select successfully, PhotoSelectResult uri: ${PhotoSelectResult.photoUris}`);
125.         resolve(PhotoSelectResult.photoUris)
126.       }).catch((err: BusinessError) => {
127.         hilog.error(0x0000, TAG, `PhotoViewPicker.select failed with errCode: ${err.code}, errMessage: ${err.message}`);
128.         reject();
129.       });
130.     })
131.   }

132.   private loadImage(names: string[]) {
133.     setTimeout(async () => {
134.       let imageSource: image.ImageSource | undefined = undefined
135.       try {
136.         let fileSource = await fileIo.open(names[0], fileIo.OpenMode.READ_ONLY)
137.         imageSource = image.createImageSource(fileSource.fd)
138.         this.chooseImage = await imageSource.createPixelMap()
139.         await fileIo.close(fileSource);
140.       } catch (error) {
141.         hilog.error(0x0000, TAG, `Failed to open file. Error: ${error}`);
142.       }
143.     }, 100
144.     )
145.   }
146. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-face-comparator "人脸比对")
# 多目标识别

更新时间: 2025-12-16 16:27

## 适用场景

可同时检测出给定图片中的各种物体，包括风景、动物、植物、建筑、人脸、表格、文本等位置，并框选出物体。

效果如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162749.02929202139841424418633025372128:50001231000000:2800:2A790278758420F43704C4A265B00FDA50CA630B019421860C6F08C047A1F53D.png)

## 约束与限制

该能力当前不支持模拟器。

|AI能力|约束|
|:--|:--|
|多目标识别|- 输入图像具有合适成像的质量（建议720p以上），100px<高度<10000px，100px<宽度<10000px，高宽比例建议5:1以下（高度小于宽度的5倍），接近手机屏幕高宽比例为宜。<br>- 图片中的物体占比需要大于0.1%。|

## 开发步骤

1. 在使用多目标识别时，将实现多目标识别相关的类添加至工程。
    
    1. import { image } from '@kit.ImageKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { fileIo } from '@kit.CoreFileKit';
    5. import { objectDetection, visionBase } from '@kit.CoreVisionKit';
    6. import { photoAccessHelper } from '@kit.MediaLibraryKit';
    
2. 简单配置页面的布局，并在Button组件添加点击事件，拉起图库，选择图片。
    
    1. Button('选择图片')
    2.   .type(ButtonType.Capsule)
    3.   .fontColor(Color.White)
    4.   .alignSelf(ItemAlign.Center)
    5.   .width('80%')
    6.   .margin(10)
    7.   .onClick(() => {
    8.     // 拉起图库，获取图片资源
    9.     this.selectImage();
    10.   })
    
3. 通过图库获取图片资源，将图片转换为[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)。
    
    1. private async selectImage() {
    2.   let uri = await this.openPhoto()
    3.   if (uri === undefined) {
    4.     hilog.error(0x0000, 'objectDetectSample', "Failed to define uri.");
    5.   }
    6.   this.loadImage(uri)
    7. }
    
    8. private openPhoto(): Promise<string> {
    9.   return new Promise<string>((resolve, reject) => {
    10.     let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
    11.     photoPicker.select({
    12.       MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE, maxSelectNumber: 1
    13.     }).then(res => {
    14.       resolve(res.photoUris[0])
    15.     }).catch((err: BusinessError) => {
    16.       hilog.error(0x0000, 'objectDetectSample', `Failed to get photo image uri. code: ${err.code}, message: ${err.message}`);
    17.       reject('')
    18.     })
    19.   })
    20. }
    
    21. private loadImage(name: string) {
    22.   setTimeout(async () => {
    23.     let fileSource = await fileIo.open(name, fileIo.OpenMode.READ_ONLY);
    24.     this.imageSource = image.createImageSource(fileSource.fd);
    25.     this.chooseImage = await this.imageSource.createPixelMap();
    26.   }, 100)
    27. }
    
4. 实例化Request对象，并传入待检测图片的[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)，调用多目标识别的实现多目标识别功能。
    
    1. // 调用多目标检测接口
    2. let request: visionBase.Request = {
    3.   inputData: { pixelMap: this.chooseImage }
    4. };
    5. let data: objectDetection.ObjectDetectionResponse = await (await objectDetection.ObjectDetector.create()).process(request);
    
5. （可选）如果需要将结果展示在界面上，可以使用下列代码。
    
    1. let objectJson = JSON.stringify(data);
    2. hilog.info(0x0000, 'objectDetectSample', `Succeeded in object detection: ${objectJson}`);
    3. this.dataValues = objectJson;
    

## 开发实例

### Index.ets

1. import { image } from '@kit.ImageKit';
2. import { hilog } from '@kit.PerformanceAnalysisKit';
3. import { BusinessError } from '@kit.BasicServicesKit';
4. import { fileIo } from '@kit.CoreFileKit';
5. import { objectDetection, visionBase } from '@kit.CoreVisionKit';
6. import { photoAccessHelper } from '@kit.MediaLibraryKit';

7. @Entry
8. @Component
9. struct Index {
10.   private imageSource: image.ImageSource | undefined = undefined;
11.   @State chooseImage: PixelMap | undefined = undefined
12.   @State dataValues: string = ''

13.   build() {
14.     Column() {
15.       Image(this.chooseImage)
16.         .objectFit(ImageFit.Fill)
17.         .height('60%')

18.       Text(this.dataValues)
19.         .copyOption(CopyOptions.LocalDevice)
20.         .height('15%')
21.         .margin(10)
22.         .width('60%')

23.       Button('选择图片')
24.         .type(ButtonType.Capsule)
25.         .fontColor(Color.White)
26.         .alignSelf(ItemAlign.Center)
27.         .width('80%')
28.         .margin(10)
29.         .onClick(() => {
30.           // 拉起图库
31.           this.selectImage()
32.         })

33.       Button('开始多目标识别')
34.         .type(ButtonType.Capsule)
35.         .fontColor(Color.White)
36.         .alignSelf(ItemAlign.Center)
37.         .width('80%')
38.         .margin(10)
39.         .onClick(async () => {
40.           if(!this.chooseImage) {
41.             hilog.error(0x0000, 'objectDetectSample', `Failed to choose image.`);
42.             return;
43.           }
44.           let request: visionBase.Request = {
45.             inputData: { pixelMap: this.chooseImage }
46.           };
47.           try {
48.             let data: objectDetection.ObjectDetectionResponse =
49.               await (await objectDetection.ObjectDetector.create()).process(request);
50.             let objectJson = JSON.stringify(data);
51.             hilog.info(0x0000, 'objectDetectSample', `Succeeded in object detection: ${objectJson}`);
52.             this.dataValues = objectJson;
53.           } catch (error) {
54.             hilog.error(0x0000, 'objectDetectSample', `Failed to get result. Error: ${error}`);
55.           }
56.         })
57.     }
58.     .width('100%')
59.     .height('100%')
60.     .justifyContent(FlexAlign.Center)
61.   }

62.   private async selectImage() {
63.     try {
64.       let uri = await this.openPhoto();
65.       if (uri === undefined) {
66.         hilog.error(0x0000, 'objectDetectSample', "Failed to define uri.");
67.         return;
68.       }
69.       this.loadImage(uri);
70.     } catch (err) {
71.       hilog.error(0x0000, 'objectDetectSample', `Failed to get photo image uri. code: ${err.code}, message: ${err.message}`);
72.     }
73.   }

74.   private openPhoto(): Promise<string> {
75.     return new Promise<string>((resolve, reject) => {
76.       let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
77.       photoPicker.select({
78.         MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE, maxSelectNumber: 1
79.       }).then(res => {
80.         resolve(res.photoUris[0]);
81.       }).catch((err: BusinessError) => {
82.         hilog.error(0x0000, 'objectDetectSample', `Failed to get photo image uri. code: ${err.code}, message: ${err.message}`);
83.         reject(err);
84.       })
85.     })
86.   }

87.   private loadImage(name: string) {
88.     setTimeout(async () => {
89.       try {
90.         let fileSource = await fileIo.open(name, fileIo.OpenMode.READ_ONLY);
91.         this.imageSource = image.createImageSource(fileSource.fd);
92.         this.chooseImage = await this.imageSource.createPixelMap();
93.         await fileIo.close(fileSource);
94.       } catch (error) {
95.         hilog.error(0x0000, 'objectDetectSample', `Failed to open file. Error: ${error}`);
96.       }
97.     }, 100)
98.   }
99. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-subject-segmentation "主体分割")
# 骨骼点检测

更新时间: 2025-12-16 16:27

## 适用场景

人体骨骼关键点检测，主要检测人体的一些关键点，通过关键点描述人体骨骼信息。具体应用主要集中在智能视频监控，病人监护系统，人机交互，虚拟现实，人体动画，智能家居，智能安防，运动员辅助训练等等。

支持17个关键点的识别，具体为鼻子，左右眼，左右耳，左右肩，左右肘、左右手腕、左右髋、左右膝、左右脚踝。

效果如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216162749.76379533680793961182289006053748:50001231000000:2800:0281AA92EDEEBF75C48F9310B49AFAAEF665CAD4EF78E15185CF77F13DB1ABCD.png)

## 约束与限制

该能力当前不支持模拟器。

|AI能力|约束|
|:--|:--|
|骨骼点检测|- 输入图像具有合适成像的质量（建议720p以上），100px<高度<10000px，100px<宽度<10000px，高宽比例建议5:1以下（高度小于宽度的5倍），接近手机屏幕高宽比例为宜。|

## 开发步骤

1. 在使用骨骼点检测时，将实现骨骼点检测相关的类添加至工程。
    
    1. import { image } from '@kit.ImageKit';
    2. import { hilog } from '@kit.PerformanceAnalysisKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { fileIo } from '@kit.CoreFileKit';
    5. import { skeletonDetection, visionBase } from '@kit.CoreVisionKit';
    6. import { photoAccessHelper } from '@kit.MediaLibraryKit';
    
2. 简单配置页面的布局，并在Button组件添加点击事件，拉起图库，选择图片。
    
    1. Button('选择图片')
    2.   .type(ButtonType.Capsule)
    3.   .fontColor(Color.White)
    4.   .alignSelf(ItemAlign.Center)
    5.   .width('80%')
    6.   .margin(10)
    7.   .onClick(() => {
    8.     // 拉起图库，获取图片资源
    9.     this.selectImage();
    10.   })
    
3. 通过图库获取图片资源，将图片转换为[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)。
    
    1. private async selectImage() {
    2.   let uri = await this.openPhoto()
    3.   if (uri === undefined) {
    4.     hilog.error(0x0000, 'skeletonDetectSample', "Failed to define uri.");
    5.   }
    6.   this.loadImage(uri)
    7. }
    
    8. private openPhoto(): Promise<string> {
    9.   return new Promise<string>((resolve, reject) => {
    10.     let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
    11.     photoPicker.select({
    12.       MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE, maxSelectNumber: 1
    13.     }).then(res => {
    14.       resolve(res.photoUris[0])
    15.     }).catch((err: BusinessError) => {
    16.       hilog.error(0x0000, 'skeletonDetectSample', `Failed to get photo image uri. code: ${err.code}, message: ${err.message}`);
    17.       reject('')
    18.     })
    19.   })
    20. }
    
    21. private loadImage(name: string) {
    22.   setTimeout(async () => {
    23.     let fileSource = await fileIo.open(name, fileIo.OpenMode.READ_ONLY);
    24.     this.imageSource = image.createImageSource(fileSource.fd);
    25.     this.chooseImage = await this.imageSource.createPixelMap();
    26.   }, 100)
    27. }
    
4. 实例化Request对象，并传入待检测图片的[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)，实现骨骼点检测功能。
    
    1. // 调用骨骼点识别接口
    2. let request: visionBase.Request = {
    3.   inputData: { pixelMap: this.chooseImage }
    4. };
    5. let data: skeletonDetection.SkeletonDetectionResponse = await (await skeletonDetection.SkeletonDetector.create()).process(request);
    
5. （可选）如果需要将结果展示在界面上，可以用下列代码。
    
    1. let data: skeletonDetection.SkeletonDetectionResponse = await (await skeletonDetection.SkeletonDetector.create()).process(request);
    2. let poseJson = JSON.stringify(data);
    3. hilog.info(0x0000, 'skeletonDetectSample', `Succeeded in skeleton detection: ${poseJson}`);
    4. this.dataValues = poseJson;
    

## 开发实例

### Index.ets

1. import { image } from '@kit.ImageKit';
2. import { hilog } from '@kit.PerformanceAnalysisKit';
3. import { BusinessError } from '@kit.BasicServicesKit';
4. import { fileIo } from '@kit.CoreFileKit';
5. import { skeletonDetection, visionBase } from '@kit.CoreVisionKit';
6. import { photoAccessHelper } from '@kit.MediaLibraryKit';

7. @Entry
8. @Component
9. struct Index {
10.   private imageSource: image.ImageSource | undefined = undefined;
11.   @State chooseImage: PixelMap | undefined = undefined
12.   @State dataValues: string = ''

13.   build() {
14.     Column() {
15.       Image(this.chooseImage)
16.         .objectFit(ImageFit.Fill)
17.         .height('60%')

18.       Text(this.dataValues)
19.         .copyOption(CopyOptions.LocalDevice)
20.         .height('15%')
21.         .margin(10)
22.         .width('60%')

23.       Button('选择图片')
24.         .type(ButtonType.Capsule)
25.         .fontColor(Color.White)
26.         .alignSelf(ItemAlign.Center)
27.         .width('80%')
28.         .margin(10)
29.         .onClick(() => {
30.           // 拉起图库
31.           this.selectImage()
32.         })

33.       Button('开始骨骼点识别')
34.         .type(ButtonType.Capsule)
35.         .fontColor(Color.White)
36.         .alignSelf(ItemAlign.Center)
37.         .width('80%')
38.         .margin(10)
39.         .onClick(async () => {
40.           if(!this.chooseImage) {
41.             hilog.error(0x0000, 'skeletonDetectSample', `Failed to choose image.`);
42.             return;
43.           }
44.           // 调用骨骼点识别接口
45.           let request: visionBase.Request = {
46.             inputData: { pixelMap: this.chooseImage }
47.           };
48.           try {
49.             let data: skeletonDetection.SkeletonDetectionResponse =
50.               await (await skeletonDetection.SkeletonDetector.create()).process(request);
51.             let poseJson = JSON.stringify(data);
52.             hilog.info(0x0000, 'skeletonDetectSample', `Succeeded in skeleton detection: ${poseJson}`);
53.             this.dataValues = poseJson;
54.           } catch (error) {
55.             hilog.error(0x0000, 'skeletonDetectSample', `Failed to get result. Error: ${error}`);
56.           }
57.         })
58.     }
59.     .width('100%')
60.     .height('100%')
61.     .justifyContent(FlexAlign.Center)
62.   }

63.   private async selectImage() {
64.     let uri = await this.openPhoto()
65.     if (uri === undefined) {
66.       hilog.error(0x0000, 'skeletonDetectSample', "Failed to define uri.");
67.     }
68.     this.loadImage(uri)
69.   }

70.   private openPhoto(): Promise<string> {
71.     return new Promise<string>((resolve, reject) => {
72.       let photoPicker: photoAccessHelper.PhotoViewPicker = new photoAccessHelper.PhotoViewPicker();
73.       photoPicker.select({
74.         MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE, maxSelectNumber: 1
75.       }).then(res => {
76.         resolve(res.photoUris[0])
77.       }).catch((err: BusinessError) => {
78.         hilog.error(0x0000, 'skeletonDetectSample', `Failed to get photo image uri. code: ${err.code}, message: ${err.message}`);
79.         reject('')
80.       })
81.     })
82.   }

83.   private loadImage(name: string) {
84.     setTimeout(async () => {
85.       try {
86.         let fileSource = await fileIo.open(name, fileIo.OpenMode.READ_ONLY);
87.         this.imageSource = image.createImageSource(fileSource.fd);
88.         this.chooseImage = await this.imageSource.createPixelMap();
89.         await fileIo.close(fileSource);
90.       } catch (error) {
91.         hilog.error(0x0000, 'skeletonDetectSample', `Failed to open file. Error: ${error}`);
92.       }
93.     }, 100)
94.   }
95. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-object-detection "多目标识别")
