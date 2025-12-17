# Image Kit简介

更新时间: 2025-12-16 16:35

开发者通过调用Image Kit（图片处理服务）提供的接口，可以实现图片的解码、编码、编辑、元数据处理和图片接收等功能。

## 亮点/特征

- 编解码支持HEIF、JPEG、PNG、WebP等主流图片格式。
- 支持HDR图片编解码，给用户带来更高质量的色彩体验，还可以使用AI能力将SDR图片转换成HDR图片。
- 提供丰富的图片编辑和处理的能力，包括：图像变换、位图操作、滤镜效果等。
- 采用了高效的算法和优化策略，提高了图片处理的速度和效率。

## 基础概念

在开发前，需要了解以下基础概念：

- PixelMap
    
    位图对象。可用于读取或写入像素数据，可以进行裁剪、缩放、平移、旋转、镜像等操作，并可直接传给[Image组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-graphics-display)用于显示。还提供了获取图片信息、获取和设置图片色域、HDR元数据的方法。
    
- Picture
    
    多图对象。包含主图、辅助图和元数据。其中，主图包含了主要图像信息；辅助图用于存储与主图相关的附加信息；元数据用于存储与图片相关的其他信息。Picture提供获取主图、合成HDR图、获取辅助图、设置辅助图、获取元数据、设置元数据等方法。
    
- 图片解码
    
    将所支持格式的图片文件解码成PixelMap或Picture，以便在应用或系统中进行图片显示或图片处理。
    
- 图片编辑和处理
    
    对PixelMap进行相关的操作，如旋转、缩放、设置透明度、获取图片信息、读写像素数据等，操作时坐标系原点为左上角。
    
- 图片编码
    
    将PixelMap（或Picture）编码成不同格式的图片文件，用于后续处理，如保存、传输等。
    

## 使用方式

Image Kit提供了丰富的图片处理能力，开发者可按需灵活使用。既可以完整调用图片解码、编辑处理、编码的全流程；也可以图片解码后不做处理，直接将解码得到的PixelMap传给[Image组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-graphics-display)显示。解码、编码过程中均提供了丰富的选项参数，可以满足各种实际开发场景的需求。

Image Kit支持对解码得到的PixelMap进行[位图操作](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-pixelmap-operation)，对目标图片中的部分区域进行处理；实现[图像变换](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-transformation)，可以对图片做裁剪、缩放、偏移、旋转、翻转、设置透明度等变换。

还可以通过[ImageEffect](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-effect-guidelines)为图片添加滤镜效果；使用ImageProcessing进行图片细节增强，色彩空间转换以及HDR图片处理。

Image Kit还提供了读取和编辑图片EXIF信息的能力，可以获取和配置图片文件中的附加属性，如：宽、高、旋转方向等图片基本信息，光圈、焦距等图片拍照参数，经度、纬度等图片GPS信息等。

图片解码和图片编码的流程如图1和图2所示。图片解码得到的PixelMap可以直接用于图片显示、图片编辑和处理。

**图1** 图片解码流程示意图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163516.69277008891736786155115752329478:50001231000000:2800:78E0D837D4119E61F872CA6ABABE54641E81DF9E583B2204E9ED90AD585829FA.png)

**图2** 图片编码流程示意图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163516.79537096947207741494949097178884:50001231000000:2800:2F8B9F49280111F680FFFA4112DB2E2079294E1D2635A6814D82B204CAC5AF5F.png)

## 约束与限制

- **读写权限限制：**
    
    在图片处理中，可能需要使用用户图片，应用需要向用户申请对应的读写操作权限才能保证功能的正常运行，申请方式请参考[向用户申请授权](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/request-user-authorization)。
    
- **选择合适的C API接口：**
    
    Image Kit当前提供了两套C API接口，分别为[依赖于JS对象的C API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-image)和[不依赖于JS对象的C API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-image-nativemodule)。
    
    - 依赖于JS对象的C接口
        
        这类接口可以完成图片编解码，图片接收器，处理图像数据等功能，相关示例代码可以参考[图片开发指导(依赖JS对象)(C/C++)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-decoding-native)节点下的内容。开发者可查看[Image](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-image)模块下的C API，确认API范围。这部分API在API version 11之前发布，在后续的版本不再增加新功能，**不再推荐使用**。
        
    - 不依赖于JS对象的C接口
        
        这类接口除了提供上述图片框架基础功能，还可以完成多图编解码等新特性，相关开发指导请参考[图片开发指导(C/C++)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-source-c)节点下的内容。开发者可查看[Image_NativeModule](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-image-nativemodule)模块下的C API，确认API范围。这部分API从API version 12开始支持，并将持续演进，**推荐开发者使用**。
        
    
    注意
    
    两套C API不建议同时使用，在部分场景下存在不兼容的问题。
    

## 与相关Kit的关系

Image Kit提供图片编解码、图片接收、图片编辑和处理等能力，为Image组件、图库以及其他有图片相关需求的应用提供支撑。图片解码得到的PixelMap可以传给[Image组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-graphics-display)显示。通过ImageReceiver（图片接收）可以实现[相机预览流二次处理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/native-camera-preview-imagereceiver)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-kit "Image Kit（图片处理服务）")
# 使用ImageSource完成图片解码

更新时间: 2025-12-16 16:35

将所支持格式的图片文件解码成[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)，以便在应用或系统中显示或处理图片。当前支持的图片文件格式包括JPEG、PNG、GIF、WebP、BMP、SVG、ICO、DNG、HEIC。不同硬件设备的支持情况可能不同 。

## 开发步骤

图片解码相关API的详细介绍请参见：[图片解码接口说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource)。

1. 全局导入Image模块。
    
    1. import { image } from '@kit.ImageKit';
    
2. 获取图片。
    
    - 方法一：通过沙箱路径直接获取。该方法仅适用于应用沙箱中的图片。更多细节请参考[获取应用文件路径](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-context-stage#%E8%8E%B7%E5%8F%96%E5%BA%94%E7%94%A8%E6%96%87%E4%BB%B6%E8%B7%AF%E5%BE%84)。应用沙箱的介绍及如何向应用沙箱推送文件，请参考[文件管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)。
        
        1. function getFilePath(context: Context): string {
        2.   const filePath: string = context.cacheDir + '/test.jpg';
        3.   return filePath;
        4. }
        
    - 方法二：通过沙箱路径获取图片的文件描述符。具体请参考[file.fs API参考文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs)。该方法需要导入@kit.CoreFileKit模块。
        
        1. import { fileIo as fs } from '@kit.CoreFileKit';
        
        2. function getFileFd(context: Context): number | undefined {
        3.   const filePath: string = context.cacheDir + '/test.jpg';
        4.   const file: fs.File = fs.openSync(filePath, fs.OpenMode.READ_WRITE);
        5.   const fd: number = file?.fd;
        6.   return fd;
        7. }
        
    - 方法三：通过资源管理器获取资源文件的ArrayBuffer。具体请参考[资源管理器API参考文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resource-manager#getrawfilecontent9-1)。该方法需要导入@kit.LocalizationKit模块。
        
        1. import { resourceManager } from '@kit.LocalizationKit';
        
        2. async function getFileBuffer(context: Context): Promise<ArrayBuffer | undefined> {
        3.   try {
        4.     const resourceMgr: resourceManager.ResourceManager = context.resourceManager;
        5.     // 获取资源文件内容，返回Uint8Array。
        6.     const fileData: Uint8Array = await resourceMgr.getRawFileContent('test.jpg');
        7.     console.info('Successfully got RawFileContent');
        8.     // 转为ArrayBuffer并返回。
        9.     const buffer: ArrayBuffer = fileData.buffer.slice(0);
        10.     return buffer;
        11.   } catch (error) {
        12.     console.error("Failed to get RawFileContent");
        13.     return undefined;
        14.   }
        15. }
        
    - 方法四：通过资源管理器获取资源文件的RawFileDescriptor。具体请参考[资源管理器API参考文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resource-manager#getrawfd9-1)。该方法需要导入@kit.LocalizationKit模块。
        
        1. import { resourceManager } from '@kit.LocalizationKit';
        
        2. async function getRawFd(context: Context): Promise<resourceManager.RawFileDescriptor | undefined> {
        3.   try {
        4.     const resourceMgr: resourceManager.ResourceManager = context.resourceManager;
        5.     const rawFileDescriptor: resourceManager.RawFileDescriptor = await resourceMgr.getRawFd('test.jpg');
        6.     console.info('Successfully got RawFileDescriptor');
        7.     return rawFileDescriptor;
        8.   } catch (error) {
        9.     console.error('Failed to get RawFileDescriptor:');
        10.     return undefined;
        11.   }
        12. }
        
3. 创建ImageSource实例。
    
    - 方法一：通过沙箱路径创建ImageSource。沙箱路径可以通过步骤2的方法一获取。
        
        1. // path为已获得的沙箱路径。
        2. const imageSource : image.ImageSource = image.createImageSource(filePath);
        
    - 方法二：通过文件描述符fd创建ImageSource。文件描述符可以通过步骤2的方法二获取。
        
        1. // fd为已获得的文件描述符。
        2. const imageSource : image.ImageSource = image.createImageSource(fd);
        
    - 方法三：通过缓冲区数组创建ImageSource。缓冲区数组可以通过步骤2的方法三获取。
        
        1. const imageSource : image.ImageSource = image.createImageSource(buffer);
        
    - 方法四：通过资源文件的RawFileDescriptor创建ImageSource。RawFileDescriptor可以通过步骤2的方法四获取。
        
        1. const imageSource : image.ImageSource = image.createImageSource(rawFileDescriptor);
        
4. 设置解码参数DecodingOptions，解码获取pixelMap图片对象。
    
    - 设置期望的format进行解码：
        
        1. import { BusinessError } from '@kit.BasicServicesKit';
        2. import { image } from '@kit.ImageKit';
        
        3. // 创建ImageSource，请选择3中合适的方法替换。
        4. let fd : number = 0;
        5. let imageSource : image.ImageSource = image.createImageSource(fd);
        6. // 配置解码选项参数。
        7. let decodingOptions : image.DecodingOptions = {
        8.    editable: true,
        9.    desiredPixelFormat: image.PixelMapFormat.RGBA_8888,
        10. };
        11. // 创建pixelMap。
        12. imageSource.createPixelMap(decodingOptions).then((pixelMap : image.PixelMap) => {
        13.    console.info("Succeeded in creating PixelMap");
        14. }).catch((err : BusinessError) => {
        15.    console.error("Failed to create PixelMap");
        16. });
        
    - HDR图片解码
        
        1. import { BusinessError } from '@kit.BasicServicesKit';
        2. import { image } from '@kit.ImageKit';
        
        3. // 创建ImageSource，请选择3中合适的方法替换。
        4. let fd : number = 0;
        5. let imageSource : image.ImageSource = image.createImageSource(fd);
        6. // 配置解码选项参数。
        7. let decodingOptions : image.DecodingOptions = {
        8.    //设置为AUTO会根据图片资源格式解码，如果图片资源为HDR资源则会解码为HDR的pixelMap。
        9.    desiredDynamicRange: image.DecodingDynamicRange.AUTO,
        10. };
        11. // 创建pixelMap。
        12. imageSource.createPixelMap(decodingOptions).then((pixelMap : image.PixelMap) => {
        13.    console.info("Succeeded in creating PixelMap");
        14.    // 判断pixelMap是否为hdr内容。
        15.    let info = pixelMap.getImageInfoSync();
        16.    console.info("pixelMap isHdr:" + info.isHdr);
        17. }).catch((err : BusinessError) => {
        18.    console.error("Failed to create PixelMap");
        19. });
        
    
    解码完成，获取到pixelMap对象后，可以进行后续[图片处理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-transformation)。
    
5. 释放pixelMap和imageSource。
    
    确认pixelMap和imageSource的异步方法已经执行完成，不再使用该变量后，可按需手动调用下面方法释放。
    
    1. // 请务必在确认pixelMap不需要再使用时，再进行释放。
    2. // pixelMap.release();
    3. // 请务必在确认imageSource不需要再使用时，再进行释放。
    4. // imageSource.release();
    
    说明
    
    1. 释放imageSource的合适时机：createPixelMap执行完成，成功获取pixelMap后，如果确定不再使用imageSource的其他方法，可以手动释放imageSource。由于解码得到的pixelMap是一个独立的实例，imageSource的释放不会导致pixelMap不可用。
    2. 释放pixelMap的合适时机：如果使用系统的[Image组件](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-basic-components-image)进行图片显示，无需手动释放，Image组件会自动管理传递给它的pixelMap；如果应用自行处理pixelMap，则推荐在页面切换、应用退后台等场景下手动释放老页面pixelMap；在内存资源紧张的场景，推荐释放除当前页面外其他不可见页面的PixelMap。
    

## 示例代码

- [实现图片获取与保存功能](https://gitee.com/harmonyos_samples/ImageGetAndSave)
- [水印添加能力](https://gitee.com/harmonyos_samples/watermark)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-decoding-arts "图片解码")
# 使用ImageSource完成多图对象解码

更新时间: 2025-12-16 16:35

将所支持格式的图片文件解码成[Picture](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-overview#%E5%9F%BA%E7%A1%80%E6%A6%82%E5%BF%B5)。当前支持的图片文件格式包括JPEG、HEIF。

## 开发步骤

图片解码相关API的详细介绍请参见：[图片解码接口说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource)。

1. 全局导入Image模块。
    
    1. import { image } from '@kit.ImageKit';
    
2. 获取图片。
    
    - 方法一：通过沙箱路径直接获取。该方法仅适用于应用沙箱中的图片。更多细节请参考[获取应用文件路径](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-context-stage#%E8%8E%B7%E5%8F%96%E5%BA%94%E7%94%A8%E6%96%87%E4%BB%B6%E8%B7%AF%E5%BE%84)。应用沙箱的介绍及如何向应用沙箱推送文件，请参考[文件管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)。
        
        1. function getFilePath(context: Context): string {
        2.   const filePath: string = context.cacheDir + '/test.jpg';
        3.   return filePath;
        4. }
        
    - 方法二：通过沙箱路径获取图片的文件描述符。具体请参考[file.fs API参考文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs)。该方法需要导入@kit.CoreFileKit模块。
        
        1. import { fileIo as fs } from '@kit.CoreFileKit';
        
        2. function getFileFd(context: Context): number | undefined {
        3.   const filePath: string = context.filesDir + '/test.jpg';
        4.   const file: fs.File = fs.openSync(filePath, fs.OpenMode.READ_WRITE);
        5.   if (file != undefined) {
        6.     const fd: number = file.fd;
        7.     return fd;
        8.   }
        9.   return undefined;
        10. }
        
    - 方法三：通过资源管理器获取资源文件的ArrayBuffer。具体请参考[资源管理器API参考文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resource-manager#getrawfilecontent9-1)。该方法需要导入@kit.LocalizationKit模块。
        
        1. import { resourceManager } from '@kit.LocalizationKit';
        
        2. async function getFileBuffer(context: Context): Promise<ArrayBuffer | undefined> {
        3.   try {
        4.     const resourceMgr: resourceManager.ResourceManager = context.resourceManager;
        5.     // 获取资源文件内容，返回Uint8Array。
        6.     const fileData: Uint8Array = await resourceMgr.getRawFileContent('test.jpg');
        7.     console.info('Successfully got RawFileContent');
        8.     // 转为ArrayBuffer并返回。
        9.     const buffer: ArrayBuffer = fileData.buffer.slice(0);
        10.     return buffer;
        11.   } catch (error) {
        12.     console.error("Failed to get RawFileContent");
        13.     return undefined;
        14.   }
        15. }
        
    - 方法四：通过资源管理器获取资源文件的RawFileDescriptor。具体请参考[资源管理器API参考文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-resource-manager#getrawfd9-1)。该方法需要导入@kit.LocalizationKit模块。
        
        1. import { resourceManager } from '@kit.LocalizationKit';
        
        2. async function getRawFd(context: Context): Promise<resourceManager.RawFileDescriptor | undefined> {
        3.   try {
        4.     const resourceMgr: resourceManager.ResourceManager = context.resourceManager;
        5.     const rawFileDescriptor: resourceManager.RawFileDescriptor = await resourceMgr.getRawFd('test.jpg');
        6.     console.info('Successfully got RawFileDescriptor');
        7.     return rawFileDescriptor;
        8.   } catch (error) {
        9.     console.error('Failed to get RawFileDescriptor:');
        10.     return undefined;
        11.   }
        12. }
        
3. 创建ImageSource实例。
    
    - 方法一：通过沙箱路径创建ImageSource。沙箱路径可以通过步骤2的方法一获取。
        
        1. // path为已获得的沙箱路径。
        2. const imageSource : image.ImageSource = image.createImageSource(filePath);
        
    - 方法二：通过文件描述符fd创建ImageSource。文件描述符可以通过步骤2的方法二获取。
        
        1. // fd为已获得的文件描述符。
        2. const imageSource : image.ImageSource = image.createImageSource(fd);
        
    - 方法三：通过缓冲区数组创建ImageSource。缓冲区数组可以通过步骤2的方法三获取。
        
        1. const imageSource : image.ImageSource = image.createImageSource(buffer);
        
    - 方法四：通过资源文件的RawFileDescriptor创建ImageSource。RawFileDescriptor可以通过步骤2的方法四获取。
        
        1. const imageSource : image.ImageSource = image.createImageSource(rawFileDescriptor);
        
4. 设置解码参数DecodingOptions，解码获取picture多图对象。并对picture进行操作，如获取辅助图等。对于picture和辅助图的操作具体请参考[Image API参考文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-picture)。
    
    设置期望的format进行解码：
    
    1. import { BusinessError } from '@kit.BasicServicesKit';
    2. import { image } from '@kit.ImageKit';
    
    3. // 创建ImageSource，请选择3中合适的方法替换。
    4. let fd: number = 0;
    5. let imageSource: image.ImageSource = image.createImageSource(fd);
    6. // 配置解码选项参数。
    7. let options: image.DecodingOptionsForPicture = {
    8.   desiredAuxiliaryPictures: [image.AuxiliaryPictureType.GAINMAP] // GAINMAP为需要解码的辅助图类型。
    9. };
    10. // 创建picture。
    11. imageSource.createPicture(options).then((picture: image.Picture) => {
    12.   console.info("Create picture succeeded.");
    13.   let type: image.AuxiliaryPictureType = image.AuxiliaryPictureType.GAINMAP;
    14.   let auxPicture: image.AuxiliaryPicture | null = picture.getAuxiliaryPicture(type);
    15.   // 获取辅助图信息。
    16.   if (auxPicture != null) {
    17.     let auxInfo: image.AuxiliaryPictureInfo = auxPicture.getAuxiliaryPictureInfo();
    18.     console.info('GetAuxiliaryPictureInfo Type: ' + auxInfo.auxiliaryPictureType +
    19.       ' height: ' + auxInfo.size.height + ' width: ' + auxInfo.size.width +
    20.       ' rowStride: ' + auxInfo.rowStride + ' pixelFormat: ' + auxInfo.pixelFormat +
    21.       ' colorSpace: ' + auxInfo.colorSpace);
    22.     // 将辅助图数据读到ArrayBuffer。
    23.     auxPicture.readPixelsToBuffer().then((pixelsBuffer: ArrayBuffer) => {
    24.       console.info('Read pixels to buffer success.');
    25.     }).catch((error: BusinessError) => {
    26.       console.error(`Read pixels to buffer failed, error.code: ${error.code}, error.message: ${error.message}`);
    27.     });
    28.     auxPicture.release();
    29.   }
    30. }).catch((err: BusinessError) => {
    31.   console.error("Create picture failed.");
    32. });
    
5. 释放picture。
    
    确认picture的异步方法已经执行完成，不再使用该变量后，可按需手动调用下面方法释放。
    
    1. // 请务必在确认picture不需要再使用时，再进行释放。
    2. // picture.release();
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-decoding "使用ImageSource完成图片解码")
# 申请图片解码内存(ArkTS)

更新时间: 2025-12-16 16:35

应用在进行图片解码操作时，需要申请对应内存。当前指导将介绍不同的内存类型，以及如何进行申请。

应用侧通过解码API接口获取PixelMap，并将其传递给Image组件以进行显示。

当PixelMap较大且使用共享内存时，RS主线程将经历较长的纹理上传时间，导致卡顿现象。图形侧提供了DMA内存零拷贝功能，可在绘制图片时避免纹理上传时间消耗。

## 内存类型介绍

当前PixelMap的内存类型包括以下两种。

- SHARE_MEMORY：共享内存。需要进行纹理上传。
- DMA_ALLOC：DMA内存。无需纹理上传。

系统提供了[createPixelMapUsingAllocator](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource#createpixelmapusingallocator15)接口，以便用户能够自定义内存分配类型进行解码。接口定义及使用示例详见[图片解码接口说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource)。

### SHARE_MEMORY和DMA_ALLOC的区别

|名称|SHARE_MEMORY|DMA_ALLOC|
|:--|:--|:--|
|定义|操作系统提供的共享内存（如ashmem/匿名共享），便于在同一物理页上读写。|使用可被外设/GPU/显示管线直接DMA访问的缓冲区（常见形态是dmabuf/SurfaceBuffer），用于零拷贝链路。|
|工作原理|进程共享同一段内存，通过CPU进行读写。若要给GPU/显示使用，通常需进行拷贝。|解码器通过DMA将数据写入dmabuf；GPU/显示直接使用该dmabuf，无需拷贝。|
|使用场景|用于进程或线程间的数据共享，如后处理、算法中间结果交换等场景。|视频/图片硬解、预览、显示等高带宽数据传输场景。|
|CPU占用|CPU需参与共享内存的管理和同步（如加锁、解锁），会造成额外开销。|占用极低，CPU仅参与DMA控制器的配置，实际数据传输无需CPU干预。|
|硬件依赖|依赖操作系统支持的共享内存机制。|强依赖硬件DMA控制器。|
|内存分配与访问权限|系统为共享内存分配物理或虚拟内存区域，访问需通过用户或内核映射操作。|DMA控制器直接操作物理内存，需预先分配DMA缓冲区（通常是连续内存）。|
|优势|灵活性强。支持多线程或多进程同时共享数据，便于图像后处理和协作。|高效、低延迟；适合大数据量、连续数据块的传输。|
|缺点|共享内存操作需要额外的同步机制，增加编程复杂度和CPU负担。|需要硬件支持，数据传输范围受DMA地址空间限制（通常需要连续物理内存）。|

### 使用DMA_ALLOC的优势

- **减少纹理上传时间**
    
    当使用SHARE_MEMORY时，图片数据需通过CPU复制到GPU显存，增加了纹理上传的时间。而采用DMA_ALLOC后，数据直接保存在GPU可访问的内存中，避免了耗时的复制过程。
    
    - SHARE_MEMORY耗时：4K图片单帧渲染耗时约为20ms。
    - DMA_ALLOC耗时：4K图片单帧渲染时间可降至约4ms。此项优化在大尺寸图片显示和高频动态图片加载场景中效果尤为显著。
- **减轻CPU负载**
    
    DMA_ALLOC允许GPU直接访问解码后数据，减少了内存复制带来的负载。
    

## 系统默认的内存分配方式

在使用[createPixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource#createpixelmap7)接口进行解码时，不同场景下会采取不同的内存分配类型。

以下场景将使用DMA_ALLOC。

- 解码HDR图片。
- 解码HEIF格式图片。
- 解码JPEG格式图片，当原图的宽和高均在1024像素至8192像素之间，[desiredPixelFormat](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-i#decodingoptions7)为RGBA_8888或NV21，同时硬件不繁忙（并发数为3）。
- 解码其他格式图片。要求[desiredSize](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-i#decodingoptions7)大于等于512像素 * 512像素（未设置desiredSize时按原图尺寸考虑），并且宽度为64的倍数。

除上述场景外，其余情况均使用SHARE_MEMORY。

## 自定义内存分配方式

默认场景下，由系统选择性能最优的内存分配方式。特定场景支持应用使用指定的内存分配方式。

开发者使用接口[createPixelMapUsingAllocator](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource#createpixelmapusingallocator15)进行解码时，系统会根据传入的[解码参数](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-i#decodingoptions7)和[内存申请类型](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-e#allocatortype15)，自动选择硬件解码和软件解码。

在创建像素图时，将根据用户指定的分配器类型来决定采用DMA_ALLOC分配机制还是SHARE_MEMORY分配机制。

### 使用限制

当前图片解码功能针对内存分配模式有如下限制。

- HDR图片解码仅支持DMA_ALLOC的内存模式。
- 硬件解码仅支持DMA_ALLOC的内存模式。
- SVG格式图片解码仅支持SHARE_MEMORY的内存模式。

使用接口[createPixelMapUsingAllocator](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource#createpixelmapusingallocator15)进行解码时，若设置的内存分配模式，与图片格式或解码方式不匹配，则会抛出内存分配失败的异常。

如果用户选择的分配类型为AUTO，系统将根据解码和渲染的时间综合评估，以决定使用DMA_ALLOC还是SHARE_MEMORY分配机制。

不同的内存分配策略会导致图片的stride（步幅）有所差异。对于通过DMA_ALLOC申请的内存，在对PixelMap执行编辑等操作时，必须使用stride。接下来将介绍如何获取stride。

### 获取stride

stride（步幅）描述了图片在内存中每一行像素数据的存储宽度。它是图片绘制过程中的重要参数，用于正确定位图片数据在内存中的布局。

使用DMA分配机制分配内存时，stride必须满足硬件对齐要求。

- stride值需为硬件平台要求字节数的整数倍。
- 当stride值不满足对齐要求时，系统会自动补齐填充数据（padding）。
    
    stride的值可以通过[getImageInfo()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource#getimageinfo-1) 接口获取。
    

1. 调用[getImageInfo()](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource#getimageinfo-1)方法，获取ImageInfo对象。
2. 从ImageInfo对象中访问stride值：info.stride。

3. import { image } from '@kit.ImageKit';

4. async function CreatePixelMapUsingAllocator(context: Context) {
5.   const resourceMgr = context.resourceManager;
6.   const rawFile = await resourceMgr.getRawFileContent("test.jpg"); // 测试图片。
7.   let imageSource: image.ImageSource = image.createImageSource(rawFile.buffer as ArrayBuffer);
8.   let options: image.DecodingOptions = {};
9.   let pixelmap = await imageSource.createPixelMapUsingAllocator(options, image.AllocatorType.AUTO);
10.   if (pixelmap != undefined) {
11.     let info = await pixelmap.getImageInfo();
12.     // 用DMA_ALLOC内存申请出的pixelmap的stride与SHARE_MEMORY内存申请出的pixelmap的stride不同。
13.     console.info("stride = " + info.stride);
14.     let region: image.Region = {
15.       x: 0,
16.       y: 0,
17.       size: { height: 100, width: 35 }
18.     }; // 在(0, 0)位置，裁剪100 * 35的pixelMap，用于DMA_ALLOC的stride和SHARE_MEMORY的stride对齐方式不同。
19.     if (pixelmap != undefined) {
20.       await pixelmap.crop(region);
21.       let imageInfo = await pixelmap.getImageInfo();
22.       if (imageInfo != undefined) {
23.         console.info("stride =", imageInfo.stride);
24.       }
25.     }
26.   }
27. }

## 解码单张图片的内存限制

为了防止内存溢出导致系统崩溃，系统对进程内存做了限制，详细说明请参考[应用被查杀问题检测方法](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-stability-runtime-appkilled-detection)。

图片框架对解码单张图片设置了2GB的内存限制。进程需要主动管理自身内存，建议在不使用[PixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)时及时释放，以避免进程被系统终止。

应用可使用[onMemoryLevel](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-abilitystage#onmemorylevel)监听系统内存变化情况。

PixelMap申请像素内存的计算规则如下所示。

1. pixels_size(像素内存大小) = stride(图片像素存储宽度) * height(图片像素高度)

对于原始像素内存超过2GB且支持下采样的图片，建议开发者使用[createPixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource#createpixelmap7)或[createPixelMapUsingAllocator](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource#createpixelmapusingallocator15)接口，并在[DecodingOptions（解码参数）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-i#decodingoptions7)中设置desiredSize（期望输出大小）进行下采样解码。

从API version 21开始，对于支持下采样解码的图片，设置desiredSize（期望输出大小）后，解码器将以基准梯度为1/8的最优下采样率计算PixelMap的像素内存，即按照7/8、6/8、...、1/8的采样率，逐次递减取一个清晰度最高的采样数。

图片框架内，不同图片格式的下采样解码支持情况如下所示。

|是否支持下采样|图片格式|
|:--|:--|
|支持|.jpg .png .heic12+（具体支持情况请参考设备规格文档。）|
|不支持|.gif .bmp .webp .dng [.svg10+](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-f#svg%E6%A0%87%E7%AD%BE%E8%AF%B4%E6%98%8E) .ico11+|

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-picture-decoding "使用ImageSource完成多图对象解码")
# 使用ImagePacker完成图片编码

更新时间: 2025-12-16 16:35

图片编码指将PixelMap压缩成不同格式的图片文件，用于保存和传输。

支持使用[PackToData](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagepacker#packtodata13-1)和[PackToFile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagepacker#packtofile11-2)将PixelMap编码为JPEG、WebP、PNG和HEIC格式。

从API version 18开始，支持使用[PackToDataFromPixelmapSequence](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagepacker#packtodatafrompixelmapsequence18)和[PackToFileFromPixelmapSequence](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagepacker#packtofilefrompixelmapsequence18)将多个PixelMap编码为GIF格式。

## 开发步骤

图片编码相关API的详细介绍请参见：[图片编码接口说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagepacker)。

### 图片编码进文件流

1. 创建图像编码ImagePacker对象。
    
    1. // 导入相关模块包。
    2. import { image } from '@kit.ImageKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    
    4. const imagePackerApi = image.createImagePacker();
    
2. 设置编码输出流和编码参数。
    
    - format为图像的编码格式；quality为图像质量，范围从0-100，100为最佳质量。
        
        说明
        
        根据MIME标准，标准编码格式为image/jpeg。当使用image编码时，PackingOption.format设置为image/jpeg，image编码后的文件扩展名可设为.jpg或.jpeg，可在支持image/jpeg解码的平台上使用。
        
        1. let packOpts : image.PackingOption = { format:"image/jpeg", quality:98 };
        
    - 编码为hdr内容(需要资源本身为hdr，支持jpeg格式)。
        
        1. packOpts.desiredDynamicRange = image.PackingDynamicRange.AUTO;
        
3. 进行图片编码，并保存编码后的图片。
    
    方法一：通过PixelMap进行编码。
    
    1. function packToDataFromPixelMap(context : Context, pixelMap : image.PixelMap) {
    2.   const imagePackerApi = image.createImagePacker();
    3.   let packOpts : image.PackingOption = { format:"image/jpeg", quality:98 };
    4.   imagePackerApi.packToData(pixelMap, packOpts).then( (data : ArrayBuffer) => {
    5.     // data 为编码获取到的文件流，写入文件保存即可得到一张图片。
    6.   }).catch((error : BusinessError) => {
    7.     console.error('Failed to pack the image. And the error is: ' + error);
    8.   })
    9. }
    
    方法二：通过imageSource进行编码。
    
    10. function packToDataFromImageSource(context : Context, imageSource : image.ImageSource) {
    11.   const imagePackerApi = image.createImagePacker();
    12.   let packOpts : image.PackingOption = { format:"image/jpeg", quality:98 };
    13.   imagePackerApi.packToData(imageSource, packOpts).then( (data : ArrayBuffer) => {
    14.     // data 为编码获取到的文件流，写入文件保存即可得到一张图片。
    15.   }).catch((error : BusinessError) => {
    16.     console.error('Failed to pack the image. And the error is: ' + error);
    17.   })
    18. }
    

### 图片编码进文件

在编码时，开发者可以传入对应的文件路径，编码后的内存数据将直接写入文件。

方法一：通过PixelMap编码进文件。

1. import { BusinessError } from '@kit.BasicServicesKit';
2. import { fileIo as fs } from '@kit.CoreFileKit';
3. import { image } from '@kit.ImageKit';

4. function packToFile(context : Context, pixelMap : image.PixelMap) {
5.   const imagePackerApi = image.createImagePacker();
6.   let packOpts : image.PackingOption = { format:"image/jpeg", quality:98 };
7.   const path : string = context.cacheDir + "/pixel_map.jpg";
8.   let file = fs.openSync(path, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
9.   imagePackerApi.packToFile(pixelMap, file.fd, packOpts).then(() => {
10.       // 直接编码进文件。
11.   }).catch((error : BusinessError) => {
12.     console.error('Failed to pack the image. And the error is: ' + error);
13.   }).finally(() => {
14.     fs.closeSync(file.fd);
15.   })
16. }

方法二：通过imageSource编码进文件。

1. import { BusinessError } from '@kit.BasicServicesKit';
2. import { fileIo as fs } from '@kit.CoreFileKit';
3. import { image } from '@kit.ImageKit';

4. function packToFile(context : Context, imageSource : image.ImageSource) {
5.   const imagePackerApi = image.createImagePacker();
6.   let packOpts : image.PackingOption = { format:"image/jpeg", quality:98 };
7.   const filePath : string = context.cacheDir + "/image_source.jpg";
8.   let file = fs.openSync(filePath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
9.   imagePackerApi.packToFile(imageSource, file.fd, packOpts).then(() => {
10.       // 直接编码进文件。
11.   }).catch((error : BusinessError) => {
12.     console.error('Failed to pack the image. And the error is: ' + error);
13.   }).finally(() => {
14.     fs.closeSync(file.fd);
15.   })
16. }

### 图片编码保存进图库

可以将图片编码保存到应用沙箱，然后使用媒体文件管理相关接口[保存媒体库资源](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/photoaccesshelper-savebutton)。

## 示例代码

- [图片压缩](https://gitee.com/harmonyos_samples/image-compression)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-encoding-arts "图片编码")
# 使用ImagePacker完成多图对象编码

更新时间: 2025-12-16 16:35

图片编码指将Picture多图对象编码成不同格式的图片文件（当前仅支持编码为JPEG 和 HEIF 格式），用于后续处理，如保存、传输等。

## 开发步骤

图片编码相关API的详细介绍请参见：[图片编码接口说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagepacker)。

### 图片编码进文件流

1. 创建图像编码ImagePacker对象。
    
    1. // 导入相关模块包。
    2. import { image } from '@kit.ImageKit';
    
    3. const imagePackerApi = image.createImagePacker();
    
2. 设置编码输出流和编码参数。
    
    format为图像的编码格式；quality为图像质量，范围从0-100，100为最佳质量
    
    说明
    
    根据MIME标准，标准编码格式为image/jpeg。当使用image编码时，PackingOption.format设置为image/jpeg，image编码后的文件扩展名可设为.jpg或.jpeg，可在支持image/jpeg解码的平台上使用。
    
    1. let packOpts: image.PackingOption = {
    2.   format: "image/jpeg",
    3.   quality: 98,
    4.   bufferSize: 10,
    5.   desiredDynamicRange: image.PackingDynamicRange.AUTO,
    6.   needsPackProperties: true
    7. };
    
3. 进行图片编码，并保存编码后的图片。在进行编码前，需要先通过解码获取picture，可参考[使用ImageSource完成多图对象解码](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-picture-decoding)。
    
    1. import { BusinessError } from '@kit.BasicServicesKit';
    
    2. function packing(picture: image.Picture, packOpts: image.PackingOption) {
    3.   const imagePackerApi = image.createImagePacker();
    4.   imagePackerApi.packing(picture, packOpts).then( (data : ArrayBuffer) => {
    5.     console.info('Succeeded in packing the image.'+ data);
    6.   }).catch((error : BusinessError) => {
    7.     console.error(`Failed to pack the image, error.code: ${error.code}, error.message: ${error.message}`);
    8.   })
    9. }
    

### 图片编码进文件

在编码时，开发者可以传入对应的文件路径，编码后的内存数据将直接写入文件。在进行编码前，需要先通过解码获取picture，可参考[使用ImageSource完成多图对象解码](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-picture-decoding)。

1. import { BusinessError } from '@kit.BasicServicesKit';
2. import { fileIo } from '@kit.CoreFileKit';
3. import { image } from '@kit.ImageKit';

4. function packToFile(picture: image.Picture, packOpts: image.PackingOption, context: Context) {
5. const path : string = context.cacheDir + "/picture.jpg";
6. let file = fileIo.openSync(path, fileIo.OpenMode.CREATE | fileIo.OpenMode.READ_WRITE);
7. const imagePackerApi = image.createImagePacker();
8. imagePackerApi.packToFile(picture, file.fd, packOpts).then(() => {
9.   console.info('Succeeded in packing the image to file.');
10. }).catch((error : BusinessError) => {
11.   console.error('Failed to pack the image. And the error is: ' + error);
12. })
13. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-encoding "使用ImagePacker完成图片编码")
# 使用PixelMap完成图像变换

更新时间: 2025-12-16 16:35

图片处理指对PixelMap进行相关的操作，如获取图片信息、裁剪、缩放、偏移、旋转、翻转、设置透明度、读写像素数据等。图片处理主要包括图像变换、[位图操作](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-pixelmap-operation)，本文介绍图像变换。

## 开发步骤

图像变换相关API的详细介绍请参见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)。

1. 完成[图片解码](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-decoding)，获取PixelMap对象。
    
2. 获取图片信息。
    
    1. import { BusinessError } from '@kit.BasicServicesKit';
    2. // 获取图片大小。
    3. pixelMap.getImageInfo().then( (info : image.ImageInfo) => {
    4.   console.info('info.width = ' + info.size.width);
    5.   console.info('info.height = ' + info.size.height);
    6. }).catch((err : BusinessError) => {
    7.   console.error("Failed to obtain the image pixel map information.And the error is: " + err);
    8. });
    
3. 进行图像变换操作。
    
    原图：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163545.03858405611837201883219980797133:50001231000000:2800:F3B94782CDB905A2A7D48C9C39470F19F14E9C3C14BD358A05347482367EDF35.jpeg)
    
    - 裁剪
        
        1. // x：裁剪起始点横坐标0。
        2. // y：裁剪起始点纵坐标0。
        3. // height：裁剪高度400，方向为从上往下（裁剪后的图片高度为400）。
        4. // width：裁剪宽度400，方向为从左到右（裁剪后的图片宽度为400）。
        5. pixelMap.crop({x: 0, y: 0, size: { height: 400, width: 400 } });
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163545.20693089305952385043867888195944:50001231000000:2800:508F0C617C0C6F76EEAE60A0CBDD9EDEAE675331B08AFC70AFAF80C99F0A7E3F.jpeg)
        
    - 缩放
        
        1. // 宽为原来的0.5。
        2. // 高为原来的0.5。
        3. pixelMap.scale(0.5, 0.5);
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163545.71535887437128571078088674911732:50001231000000:2800:48E9E495FC2F0A0C0C8EEE91E082E040FC2B5C96575BE96F1D5D22B2EB3C28C1.jpeg)
        
    - 偏移
        
        1. // 向下偏移100。
        2. // 向右偏移100。
        3. pixelMap.translate(100, 100);
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163545.19050989502583841336107334121834:50001231000000:2800:CEDBFD794D677B9C8BBAAD4E7B438AE0052C7E3B13D16DD68A45CBC5DD562F42.jpeg)
        
    - 旋转
        
        1. // 顺时针旋转90°。
        2. pixelMap.rotate(90);
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163545.64398502561416559630071243553105:50001231000000:2800:0CED7468AB7A94334D043130AC358B8E80742333B3BCFC172FDED4C7A2C08426.jpeg)
        
    - 翻转
        
        1. // 垂直翻转。
        2. pixelMap.flip(false, true);
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163545.29061954405106654039489553774315:50001231000000:2800:5A4A868C2BA7C0B580DD91FD68D58B939E4BAA442BFFB1FE4CC3137F743D4FB4.jpeg)
        
        1. // 水平翻转。
        2. pixelMap.flip(true, false);
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163545.44293032431456115935293168642499:50001231000000:2800:82908CC247449A9EB437722C2080234E92F023B841FC2B4AF2383437CD2294C8.jpeg)
        
    - 透明度
        
        1. // 透明度0.5。
        2. pixelMap.opacity(0.5);
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163545.74294337270659952496713758550614:50001231000000:2800:120E032F57EA466A9027CB90B0392B375FC25789DADE20FAF9065E8B6E62E5DC.png)
        

## 示例代码

- [拼图](https://gitee.com/harmonyos_samples/game-puzzle)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-editing-arkts "图片编辑和处理")
# 使用PixelMap完成位图操作

更新时间: 2025-12-16 16:35

当需要对目标图片中的部分区域进行处理时，可以使用位图操作功能。此功能常用于图片美化等操作。

如下图所示，一张图片中，将指定的矩形区域像素数据读取出来，进行修改后，再写回原图片对应区域。

**图1** 位图操作示意图

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163549.11404681731468169621623493644455:50001231000000:2800:843CBB5AA1089605449958E620806921E70745519713B685BEEB6CD2E1FF3798.png)

## 开发步骤

位图操作相关API的详细介绍请参见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-pixelmap)。

1. 完成[图片解码](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-decoding)，获取PixelMap位图对象。
    
2. 从PixelMap位图对象中获取信息。
    
    1. import { image } from '@kit.ImageKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    3. // 获取图像像素的总字节数。
    4. let pixelBytesNumber: number = pixelMap.getPixelBytesNumber();
    5. // 获取图像像素每行字节数。
    6. let rowBytes: number = pixelMap.getBytesNumberPerRow();
    7. // 获取当前图像像素密度。像素密度是指每英寸图片所拥有的像素数量。像素密度越大，图片越精细。
    8. let density: number = pixelMap.getDensity();
    
3. 读取并修改目标区域像素数据，写回原图。
    
    说明
    
    建议readPixelsToBuffer和writeBufferToPixels成对使用，readPixels和writePixels成对使用，避免因图像像素格式不一致，造成PixelMap图像出现异常。
    
    1. import { image } from '@kit.ImageKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    3. // 场景一：读取并修改整张图片数据。
    4. // 按照PixelMap的像素格式，读取PixelMap的图像像素数据，并写入缓冲区中。
    5. const buffer = new ArrayBuffer(pixelBytesNumber);
    6. pixelMap.readPixelsToBuffer(buffer).then(() => {
    7.   console.info('Succeeded in reading image pixel data.');
    8. }).catch((error : BusinessError) => {
    9.   console.error('Failed to read image pixel data. The error is: ' + error);
    10. })
    11. // 按照PixelMap的像素格式，读取缓冲区中的图像像素数据，并写入PixelMap。
    12. pixelMap.writeBufferToPixels(buffer).then(() => {
    13.   console.info('Succeeded in writing image pixel data.');
    14. }).catch((error : BusinessError) => {
    15.   console.error('Failed to write image pixel data. The error is: ' + error);
    16. })
    
    17. // 场景二：读取并修改指定区域内的图片数据。
    18. // 固定按照BGRA_8888格式，读取PixelMap指定区域内的图像像素数据，并写入PositionArea.pixels缓冲区中，该区域由PositionArea.region指定。
    19. const area : image.PositionArea = {
    20.   pixels: new ArrayBuffer(8),
    21.   offset: 0,
    22.   stride: 8,
    23.   region: { size: { height: 1, width: 2 }, x: 0, y: 0 }
    24. }
    25. pixelMap.readPixels(area).then(() => {
    26.   console.info('Succeeded in reading the image data in the area.');
    27. }).catch((error : BusinessError) => {
    28.   console.error('Failed to read the image data in the area. The error is: ' + error);
    29. })
    30. // 固定按照BGRA_8888格式，读取PositionArea.pixels缓冲区中的图像像素数据，并写入PixelMap指定区域内，该区域由PositionArea.region指定。
    31. pixelMap.writePixels(area).then(() => {
    32.   console.info('Succeeded in writing the image data in the area.');
    33. }).catch((error : BusinessError) => {
    34.   console.error('Failed to write the image data in the area. The error is: ' + error);
    35. })
    

## 开发示例-复制（深拷贝）新的PixelMap

1. 完成[图片解码](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-decoding)，获取PixelMap位图对象。
    
2. 复制（深拷贝）一个新的PixelMap。
    
    说明
    
    创建新PixelMap时，必须将srcPixelFormat指定为原PixelMap的像素格式，否则新PixelMap的图像会出现异常。
    
    1. /**
    2.  *  复制（深拷贝）一个新的PixelMap
    3.  *
    4.  * @param pixelMap - 被复制的PixelMap。
    5.  * @param desiredPixelFormat - 新PixelMap的像素格式。如果不指定，则仍使用原PixelMap的像素格式。
    6.  * @returns 新PixelMap。
    7.  **/
    8. clonePixelMap(pixelMap: PixelMap, desiredPixelFormat?: image.PixelMapFormat): PixelMap {
    9.   // 获取当前PixelMap的图片信息。
    10.   const imageInfo = pixelMap.getImageInfoSync();
    11.   // 读取当前PixelMap的图像像素数据，并按照当前PixelMap的像素格式写入缓冲区数组。
    12.   const buffer = new ArrayBuffer(pixelMap.getPixelBytesNumber());
    13.   pixelMap.readPixelsToBufferSync(buffer);
    14.   // 根据当前PixelMap的图片信息，生成初始化选项。
    15.   const options: image.InitializationOptions = {
    16.     // 当前PixelMap的像素格式。
    17.     srcPixelFormat: imageInfo.pixelFormat,
    18.     // 新PixelMap的像素格式。
    19.     pixelFormat: desiredPixelFormat ?? imageInfo.pixelFormat,
    20.     // 当前PixelMap的尺寸大小。
    21.     size: imageInfo.size
    22.   };
    23.   // 根据初始化选项和缓冲区数组，生成新PixelMap。
    24.   return image.createPixelMapSync(buffer, options);
    25. }
    

## 示例代码

- [PixelMap深拷贝案例](https://gitee.com/harmonyos_samples/image-depth-copy)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-transformation "使用PixelMap完成图像变换")
# 使用VideoProcessingEngine完成图片超分

更新时间: 2025-12-16 16:35

本模块提供图片细节增强的[ArkTS接口](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-videoprocessingengine)，通过调用本模块，可以实现图片内容的清晰度增强及缩放功能，处理后的数据可以用于送显和输出。

典型应用场景如：从URL获取图片源 > 图片细节增强 > 显示。

## 约束与限制

1. 当前仅支持处理同时满足以下条件的图片：
    - 图片为SDR（Standard dynamic range）图片。
    - 图片的像素格式为RGBA、BGRA、NV12、NV21，输出格式与输入格式一致。
    - 处理的PixelMap对象需为[DMA内存](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-allocator-type#%E5%86%85%E5%AD%98%E7%B1%BB%E5%9E%8B%E4%BB%8B%E7%BB%8D)。
2. 本模块提供4个质量档位的算法，处理效果逐渐变优，但性能也会逐渐下降。
    
    |质量档位|输入分辨率要求<br><br>（单位：像素）|输出分辨率要求<br><br>（单位：像素）|说明|
    |:--|:--|:--|:--|
    |NONE|宽：[32,3000]<br><br>高：[32,3000]|宽：[32,3000]<br><br>高：[32,3000]|仅适用于缩放场景，支持改变宽高比例，无清晰度增强效果。|
    |LOW|宽：[32,3000]<br><br>高：[32,3000]|宽：[32,3000]<br><br>高：[32,3000]|仅适用于缩放场景，支持改变宽高比例。<br><br>缩放时会对图像进行低质量的清晰度增强，处理效率较高。<br><br>此质量档位为默认设置。|
    |MEDIUM|宽：[32,3000]<br><br>高：[32,3000]|宽：[32,3000]<br><br>高：[32,3000]|仅适用于缩放场景，支持改变宽高比例。<br><br>缩放时会对图像进行中等质量的清晰度增强，处理效率适中。|
    |HIGH|宽：[512,2000]<br><br>高：[512,2000]|宽：[512,2000]<br><br>高：[512,2000]|适用于缩放及清晰度增强场景，支持改变宽高比例。<br><br>缩放时会对图像进行高质量的清晰度增强，处理效率相对较低。|
    

## 开发步骤

1. 添加引用文件。
    
    1. import { image, videoProcessingEngine } from '@kit.ImageKit';
    
2. 初始化环境。
    
    1. let promise: Promise<void> = videoProcessingEngine.initializeEnvironment();
    
3. （可选）配置输入。
    
    1. let scale: number = 0.5;
    2. let width: number = 512; // 示例代码，配置宽为512。
    3. let height: number = 512;// 示例代码，配置高为512。
    4. const color: ArrayBuffer = new ArrayBuffer(width * height * 4); // width * height * 4为需要创建的像素buffer大小。
    5. let opts: image.InitializationOptions = { editable: true, pixelFormat: image.PixelMapFormat.RGBA_8888, size: { height, width } }
    6. let sourceImage : image.PixelMap = image.createPixelMapSync(color, opts);
    7. let level : videoProcessingEngine.QualityLevel = videoProcessingEngine.QualityLevel.LOW;
    
4. 创建图像处理模块。
    
    预期返回值：videoProcessingEngine.ImageProcessor，图片处理模块实例。
    
    1. // 创建图片细节增强模块实例
    2. let imageProcessor = videoProcessingEngine.create() as videoProcessingEngine.ImageProcessor;
    
5. 启动细节增强处理。当输入图片srcImage和输出图片dstImage分辨率不一致时，进行缩放。
    
    示例中的变量说明如下：
    
    sourceImage：PixelMap类型的输入图像，必填。
    
    width：目标宽度（单位px），当没有配置目标缩放比例时必填。
    
    height：目标高度（单位px），当没有配置目标缩放比例时必填。
    
    scale：目标缩放比例，当没有配置目标分辨率时必填。目标分辨率即宽*高。
    
    level：[质量算法档位](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-processing-arkts#section74721331358)，默认为LOW。
    
    - 方式一：指定原图、目标分辨率。
        
        1. // 同步方法
        2. let enhancedPixelmap: image.PixelMap = imageProcessor.enhanceDetailSync(
        3. sourceImage, width, height, level);
        
        4. // 异步方法
        5. let enhancedPixelmap: Promise<image.PixelMap> = imageProcessor.enhanceDetail(sourceImage, width, height, level);
        
    - 方式二：指定原图、缩放比例。
        
        1. // 同步方法
        2. let enhancedPixelmap: image.PixelMap = imageProcessor.enhanceDetailSync(
        3. sourceImage, scale, level);
        
        4. // 异步方法
        5. let enhancedPixelmap: Promise<image.PixelMap> = imageProcessor.enhanceDetail(
        6. sourceImage, scale, level);
        
6. 释放处理资源。
    
    1. videoProcessingEngine.deinitializeEnvironment();
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-pixelmap-operation "使用PixelMap完成位图操作")
# 编辑图片EXIF信息

更新时间: 2025-12-16 16:35

Image Kit提供图片EXIF信息的读取与编辑能力。

EXIF（Exchangeable image file format）是专门为数码相机的照片设定的文件格式，可以记录数码照片的属性信息和拍摄数据。当前支持JPEG、PNG、HEIF格式，且需要图片包含EXIF信息。

在图库等应用中，需要查看或修改数码照片的Exif信息。当摄像机的手动镜头参数无法自动写入到Exif信息中，或者相机断电等原因会导致拍摄时间出错时，可手动修改错误的Exif数据。

HarmonyOS目前仅支持对部分EXIF信息的查看和修改，具体支持的范围请参见：[Exif信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-e#propertykey7)。

## 开发步骤

EXIF信息的读取与编辑相关API的详细介绍请参见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource#getimageproperty11)。

获取图片，创建ImageSource。读取、编辑EXIF信息。示例代码如下：

1. // 导入相关模块包。
2. import { image } from '@kit.ImageKit';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. // 获取沙箱路径创建ImageSource。
5. const fd : number = 0; // 获取需要被处理的图片的fd。
6. const imageSourceApi : image.ImageSource = image.createImageSource(fd);

7. // 读取EXIF信息，BitsPerSample为每个像素比特数。
8. let options : image.ImagePropertyOptions = { index: 0, defaultValue: 'This key has no value!' };
9. imageSourceApi.getImageProperty(image.PropertyKey.BITS_PER_SAMPLE, options).then((data : string) => {
10.   console.info('Succeeded in getting the value of the specified attribute key of the image.');
11. }).catch((error : BusinessError) => {
12.   console.error(`Failed to get the value of the specified attribute key of the image, error.code: ${error.code}, error.message: ${error.message}`);
13. })

14. // 编辑EXIF信息。
15. imageSourceApi.modifyImageProperty(image.PropertyKey.IMAGE_WIDTH, "120").then(() => {
16.   imageSourceApi.getImageProperty(image.PropertyKey.IMAGE_WIDTH).then((width : string) => {
17.     console.info('The new imageWidth is ' + width);
18.   }).catch((error : BusinessError) => {
19.     console.error(`Failed to get the Image Width, error.code: ${error.code}, error.message: ${error.message}`);
20.   })
21. }).catch((error : BusinessError) => {
22.   console.error(`Failed to modify the Image Width, error.code: ${error.code}, error.message: ${error.message}`);
23. })

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-processing-arkts "使用VideoProcessingEngine完成图片超分")
# 使用ImageReceiver完成图片接收

更新时间: 2025-12-16 16:35

图片接收类ImageReceiver用于获取组件surface id，接收最新的图片和读取下一张图片，以及释放ImageReceiver实例。

说明

Receiver作为消费者，需要有对应的生产者提供数据才能实现完整功能。常见的生产者是相机的拍照流或预览流。ImageReceiver只作为图片的接收方、消费者，在ImageReceiver设置的size、format等属性实际上并不会生效，图片createImageReceiver时传入的参数不产生实际影响。图片属性需要在发送方、生产者进行设置，如[相机创建预览流](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-cameramanager#createpreviewoutput)时配置[profile](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-camera-i#profile)。

ImageReceiver可以接收相机预览流中的图片，实现[双路预览](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-dual-channel-preview)。

ImageReceiver信息相关API的详细介绍请参见[API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagereceiver)。

## 开发步骤

创建ImageReceiver对象，获取SurfaceId创建预览流，注册图像监听，按需处理预览流每帧图像。

1. 创建ImageReceiver对象，通过ImageReceiver对象可获取预览流SurfaceId。
    
    1. import { image } from '@kit.ImageKit';
    
    2. let imageWidth: number = 1920; // 请使用设备支持profile的size的宽。
    3. let imageHeight: number = 1080; // 请使用设备支持profile的size的高。
    
    4. async function initImageReceiver(): Promise<void> {
    5.   // 创建ImageReceiver对象。createImageReceiver的参数不会对接收到的数据产生实际影响。
    6.   let size: image.Size = { width: imageWidth, height: imageHeight };
    7.   let imageReceiver = image.createImageReceiver(size, image.ImageFormat.JPEG, 8);
    8.   // 获取预览流SurfaceId。
    9.   let imageReceiverSurfaceId = await imageReceiver.getReceivingSurfaceId();
    10.   console.info(`initImageReceiver imageReceiverSurfaceId:${imageReceiverSurfaceId}`);
    11. }
    
2. 注册监听处理预览流每帧图像数据：通过ImageReceiver组件中imageArrival事件监听获取底层返回的图像数据，详细的API说明请参考[Image API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagereceiver)。
    
    1. import { BusinessError } from '@kit.BasicServicesKit';
    2. import { image } from '@kit.ImageKit';
    
    3. function onImageArrival(receiver: image.ImageReceiver): void {
    4.   // 注册imageArrival监听。
    5.   receiver.on('imageArrival', () => {
    6.     // 获取图像。
    7.     receiver.readNextImage((err: BusinessError, nextImage: image.Image) => {
    8.       if (err || nextImage === undefined) {
    9.         console.error('readNextImage failed');
    10.         return;
    11.       }
    12.       // 解析图像内容。
    13.       nextImage.getComponent(image.ComponentType.JPEG, async (err: BusinessError, imgComponent: image.Component) => {
    14.         if (err || imgComponent === undefined) {
    15.           console.error('getComponent failed');
    16.         }
    17.         if (imgComponent.byteBuffer) {
    18.           // 详情见下方解析图片buffer数据参考，本示例以方式一为例。
    19.           let width = nextImage.size.width; // 获取图片的宽。
    20.           let height = nextImage.size.height; // 获取图片的高。
    21.           let stride = imgComponent.rowStride; // 获取图片的stride。
    22.           console.debug(`getComponent with width:${width} height:${height} stride:${stride}`);
    23.           // stride与width一致。
    24.           if (stride == width) {
    25.             let pixelMap = await image.createPixelMap(imgComponent.byteBuffer, {
    26.               size: { height: height, width: width },
    27.               srcPixelFormat: 8,
    28.             })
    29.           } else {
    30.             // stride与width不一致。
    31.             const dstBufferSize = width * height * 1.5
    32.             const dstArr = new Uint8Array(dstBufferSize)
    33.             for (let j = 0; j < height * 1.5; j++) {
    34.               const srcBuf = new Uint8Array(imgComponent.byteBuffer, j * stride, width)
    35.               dstArr.set(srcBuf, j * width)
    36.             }
    37.             let pixelMap = await image.createPixelMap(dstArr.buffer, {
    38.               size: { height: height, width: width },
    39.               srcPixelFormat: 8,
    40.             })
    41.           }
    42.         } else {
    43.           console.error('byteBuffer is null');
    44.         }
    45.         // 确保当前buffer没有在使用的情况下，可进行资源释放。
    46.         // 如果对buffer进行异步操作，需要在异步操作结束后再释放该资源（nextImage.release()）。
    47.         nextImage.release();
    48.       })
    49.     })
    50.   })
    51. }
    
    通过 [image.Component](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-i#component9) 解析图片buffer数据参考：
    
    注意
    
    需要确认图像的宽width是否与行距rowStride一致，如果不一致可参考以下方式处理：
    
    方式一：去除imgComponent.byteBuffer中stride数据，拷贝得到新的buffer，调用不支持stride的接口处理buffer。
    
    52. // 以NV21为例（YUV_420_SP格式的图片）YUV_420_SP内存计算公式：长x宽+(长x宽)/2。
    53. const dstBufferSize = width * height * 1.5;
    54. const dstArr = new Uint8Array(dstBufferSize);
    55. // 逐行读取buffer数据。
    56. for (let j = 0; j < height * 1.5; j++) {
    57.   // imgComponent.byteBuffer的每行数据拷贝前width个字节到dstArr中。
    58.   const srcBuf = new Uint8Array(imgComponent.byteBuffer, j * stride, width);
    59.   dstArr.set(srcBuf, j * width);
    60. }
    61. let pixelMap = await image.createPixelMap(dstArr.buffer, {
    62.   size: { height: height, width: width }, srcPixelFormat: 8
    63. });
    
    方式二：根据stride*height创建pixelMap，然后调用pixelMap的cropSync方法裁剪掉多余的像素。
    
    64. // 创建pixelMap，width宽传行距stride的值。
    65. let pixelMap = await image.createPixelMap(imgComponent.byteBuffer, {
    66.   size:{height: height, width: stride}, srcPixelFormat: 8});
    67. // 裁剪多余的像素。
    68. pixelMap.cropSync({size:{width:width, height:height}, x:0, y:0});
    
    方式三：将原始imgComponent.byteBuffer和stride信息一起传给支持stride的接口处理。
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-receiving-arkts "图片接收")
# 如何处理HEIF图片

更新时间: 2025-12-16 16:35

## HEIF图片介绍

HEIF图片（High Efficiency Image File Format，HEIF，也称高效图像文件格式），是一个用于单张图像或图像序列的文件格式。它由动态影像专家小组（MPEG）开发，并在MPEG-H Part 12（ISO/IEC 23008-12）中定义。

目前主流的HEIF图片均使用HEVC(H.265)编码，这也是系统当前支持的HEIF图片。HEIF图片在压缩效率上具有明显优势，能够在保证图像质量的同时显著减小文件体积，通常比JPEG节省约50%的存储空间。

系统从API12开始支持HEIF图片的编解码与显示，如果应用基于系统Image Kit、ArkUI Image组件、ArkWeb等模块实现图片处理功能，则可以像处理JPEG、PNG等格式的图片一样，处理HEIF图片。

HEIF图片解码可参考：[图片解码指南（ArkTS）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-decoding)和[图片解码指南（C/C++）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-source-c)。

HEIF图片显示可参考：[ArkUI Image组件图片显示](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-graphics-display)。

HEIF图片编码可参考：[图片编码指南（ArkTS）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-encoding)和[图片编码指南（C/C++）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-packer-c)。

ArkWeb图片上传可参考：[使用Web组件上传文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-file-upload)。

## 常见问题

### 上传HEIF图片时提示：“不支持的格式”

可以使用[ImageSource](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagesource#%E5%B1%9E%E6%80%A7)的supportedFormats属性和[ImagePacker](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-imagepacker#%E5%B1%9E%E6%80%A7)的supportedFormats属性，来查看系统支持编解码的图片格式。只要查询到的结果中包含"image/heic"，即代表该设备支持HEIF图片编解码。

在支持HEIF图片编解码的设备上，系统不会对HEIF图片处理施加限制。

一般是由于应用对后缀名为.heic、.heif、.HEIC、.HEIF的图片文件做了过滤限制。

对于使用系统图片处理能力的应用，只需要解除过滤限制，即可正常上传、显示HEIF图片。

如果应用没有使用系统提供的图片处理能力，则可能需要做更多适配，一个可选的方案是将HEIF图片转码成JPEG图片。

### 担心使用HEIF格式图片存在兼容性问题，需使用JPEG或PNG格式的图片，如何操作

可以借助Image Kit的图片编解码能力，将HEIF图片转码成JPEG图片，示例代码如下：

1. import { BusinessError } from '@kit.BasicServicesKit';
2. import { fileIo as fs } from '@kit.CoreFileKit';
3. import { image } from '@kit.ImageKit';

4. async function reEncoding(context : Context, fd : number) {
5.     // 首先获取图片文件的fd，创建ImageSource。
6.     const imageSource : image.ImageSource = image.createImageSource(fd);
7.     // 创建ImagePacker，以便调用图片编码接口。
8.     const imagePackerApi = image.createImagePacker();
9.     // 配置图片编码选项：
10.     // format应使用标准的mimetype格式，如："image/jpeg"、"image/png"、"image/heic"；
11.     // quality推荐设置为80，在保证较好的图片质量的同时，可以使编码后的图片文件体积更小；
12.     // needsPackProperties参数，用于控制编码时是否保存图片属性信息。默认值为false，即不保存。
13.     let packOpts : image.PackingOption = { format:"image/jpeg", quality:80, needsPackProperties:false };
14.     // 指定图片编码文件的存放路径。
15.     const filePath : string = context.cacheDir + "/result.jpg";
16.     let file = fs.openSync(filePath, fs.OpenMode.CREATE | fs.OpenMode.READ_WRITE);
17.     imagePackerApi.packToFile(imageSource, file.fd, packOpts).then(() => {
18.         console.info('Succeed to pack the image.');
19.     }).catch((error : BusinessError) => {
20.         console.error('Failed to pack the image. And the error is: ' + error);
21.     }).finally(()=>{
22.         fs.closeSync(file.fd);
23.     })
24. }

使用CAPI完成图片转码的流程也是类似的，首先创建ImageSource和ImagePacker示例，然后指定编码参数，调用图片编码接口完成转码。详细示例代码可参考[使用Image_NativeModule完成图片编码](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-packer-c)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-faqs "Image Kit常见问题")
# 如何获取图片的旋转角度信息

更新时间: 2025-12-16 16:35

## 图片旋转角度介绍

在数码摄影中，拍摄设备（如手机、相机）会将图片的旋转角度（方向）信息保存在图片的Exif（Exchangeable image file format）数据的Orientation字段。

该信息不会直接改变图片的像素内容，但会告诉图像查看器如何正确地显示图像方向。

Exif标准中定义了8个Orientation值和它们的字符串表示。

要将图片正确显示需要执行与之对应的特定的操作，如下表所示：

|值|字符串表示|要将图片正确显示需要执行的操作|
|:--|:--|:--|
|1|"Top-left"|正常方向（无需旋转）。|
|2|"Top-right"|水平镜像翻转。|
|3|"Bottom-right"|旋转180°。|
|4|"Bottom-left"|垂直镜像翻转。|
|5|"Left-top"|先水平镜像翻转，再顺时针旋转270°。|
|6|"Right-top"|顺时针旋转90°。|
|7|"Right-bottom"|先水平镜像翻转，再顺时针旋转90°。|
|8|"Left-bottom"|顺时针旋转270°。|

ArkTS场景下读取和编辑图片的旋转角度信息，可参考：[编辑图片EXIF信息(ArkTs)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-tool)，对应的propertyKey需要设置为：ORIENTATION。

C/C++场景下读取和编辑图片的旋转角度信息，可参考：[使用Image_NativeModule编辑图片EXIF信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-tool-c)，对应的key需要设置为：OHOS_IMAGE_PROPERTY_ORIENTATION。

## 常见问题

### 读取图片旋转角度为空怎么办

部分图片可能没有EXIF数据，或者EXIF数据中没有写入Orientation字段，这些图片无需旋转（与Orientation值为1的情况保持一致）。

### 为什么会出现EXIF数据丢失

与图片来源有关，网络传输的图片可能进行了二次编码，在编码时未保存EXIF数据，导致无法获取旋转角度。

### 图片编码时，如何保存EXIF数据

在调用图片编码接口时，需要设置[packingOption](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-image-i#packingoption)的needsPackProperties属性为true（该属性的默认值为false）。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/heif-adapter-faq "如何处理HEIF图片")
# Image Kit异常处理

更新时间: 2025-12-16 16:35

Image Kit提供**ArkTS接口**和**C接口**。在遇到特殊情况时（例如输入参数无效、内存不足或函数无法处理请求等），系统会通过异常（ArkTS）或错误码（C接口）来反馈错误。开发者需要在应用层合理捕获和处理这些错误，以避免应用崩溃或出现未定义行为。在[Image错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/errorcode-image)中给出了Image Kit错误码对应的错误信息、可能原因、处理步骤。但由于部分场景引发错误的原因较为复杂，还需要开发者结合日志进一步定位。例如：401参数错误，可能是函数入参存在问题，也可能是由于缺少特定的文件读写权限导致无法访问或修改图片文件（Image Kit不感知权限，表现为传入文件异常的参数错误）。

## ArkTS接口异常处理

ArkTS接口调用时，如果传入的参数不符合要求，或者底层执行过程中出现不可恢复的错误，系统会返回或抛出[BusinessError](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-base#businesserror)异常，又或者在异步场景中返回一个[Promise](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/async-concurrency-overview#promise)的rejected状态。如果开发者忽略了异常处理，可能会出现功能问题或数据丢失，甚至直接导致应用崩溃。

典型的ArkTS接口形态及API示例和处理方法如下所示。

|接口形态|示例API|处理方式|
|:--|:--|:--|
|**Promise异步接口**|getImageInfo(): Promise<ImageInfo>、modifyImageProperty(key: PropertyKey, value: string): Promise<void>|使用await+try/catch，或promise.catch捕获BusinessError。|
|**AsyncCallback异步接口**|getImageInfo(callback: AsyncCallback<ImageInfo>): void|使用回调函数[AsyncCallback](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-base#asynccallback)的参数获取BusinessError。|
|**同步接口**|getImageInfoSync(): ImageInfo|使用try/catch捕获同步BusinessError。|

1. AsyncCallback异步接口示例。
    
    1. import { image } from '@kit.ImageKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
    3. function getImageInfoByCallback(pixelMap: image.PixelMap): void {
    4.   if (!pixelMap) {
    5.     console.error("pixelMap is null or undefined");
    6.     return;
    7.   }
    8.   pixelMap.getImageInfo((err: BusinessError, info: image.ImageInfo) => {
    9.     if (err) {
    10.       console.error(`getImageInfo callback failed, code=${err.code}, msg=${err.message}`);
    11.       return;
    12.     }
    13.     console.info(`Image width=${info.size.width}, height=${info.size.height}`);
    14.   });
    15. }
    
2. Promise异步接口示例。
    
    1. import { image } from '@kit.ImageKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
    3. // getImageInfo(): Promise<ImageInfo>
    4. async function getImageInfoByPromise(pixelMap: image.PixelMap): Promise<void> {
    5.   try {
    6.     const info = await pixelMap.getImageInfo();
    7.     console.info(`Image width=${info.size.width}, height=${info.size.height}`);
    8.   } catch (err) {
    9.     const e = err as BusinessError;
    10.     console.error(`getImageInfo promise failed, code=${e.code}, msg=${e.message}`);
    11.   }
    12. }
    
    13. // modifyImageProperty(key: PropertyKey, value: string): Promise<void>
    14. function modifyImagePropertyPromise(imageSource: image.ImageSource): void {
    15.   imageSource.modifyImageProperty(image.PropertyKey.ORIENTATION, 'Top-left').then(() => {
    16.     console.info('modifyImageProperty success');
    17.   }).catch((err: BusinessError) => {
    18.     console.error(`modifyImageProperty failed, code=${err.code}, msg=${err.message}`);
    19.   });
    20. }
    
3. 同步型示例。
    
    1. import { image } from '@kit.ImageKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
    3. function getImageInfoBySync(pixelMap: image.PixelMap): void {
    4.   try {
    5.     const info = pixelMap.getImageInfoSync();
    6.     console.info(`Image width=${info.size.width}, height=${info.size.height}`);
    7.   } catch (err) {
    8.     const e = err as BusinessError;
    9.     console.error(`getImageInfoSync failed, code=${e.code}, msg=${e.message}`);
    10.   }
    11. }
    

## C接口异常处理

C接口统一通过[Image错误码](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/errorcode-image)来表示函数执行结果。返回IMAGE_SUCCESS（0）表示执行成功，返回非零值表示发生错误。开发者应在调用后立即检查返回值，并进行必要的错误处理，如日志记录、资源释放等。C接口异常处理的典型示例如下所示。

1. 通过ImageInfo获取图像信息。

Image_ErrorCode OH_PixelmapNative_GetImageInfo(OH_PixelmapNative *pixelmap, OH_Pixelmap_ImageInfo *imageInfo)

1. // 需要在src/main/cpp/CMakeLists.txt文件中链接so库文件：target_link_libraries(entry PUBLIC libhilog_ndk.z.so libpixelmap.so)。
2. #include <hilog/log.h>
3. #include <multimedia/image_framework/image/pixelmap_native.h>

4. #undef LOG_DOMAIN
5. #undef LOG_TAG
6. #define LOG_DOMAIN 0x02b6
7. #define LOG_TAG "ImageKitDemo"

8. void GetImageInfoExample(OH_PixelmapNative *pixelmap) {
9.     if (!pixelmap) {
10.         OH_LOG_ERROR(LOG_APP, "GetImageInfoExample: pixelmap is nullptr");
11.         return;
12.     }
13.     OH_Pixelmap_ImageInfo *imageInfo;
14.     Image_ErrorCode errCode = OH_PixelmapImageInfo_Create(&imageInfo);
15.     if (errCode != IMAGE_SUCCESS) {
16.         OH_LOG_ERROR(LOG_APP, "OH_PixelmapNative_Create failed, errCode: %{public}d.", errCode);
17.         return;
18.     }
19.     OH_PixelmapNative_GetImageInfo(pixelmap, imageInfo);
20.     if (errCode != IMAGE_SUCCESS) {
21.         OH_LOG_ERROR(LOG_APP, "OH_PixelmapNative_GetImageInfo failed, errCode: %{public}d.", errCode);
22.         return;
23.     }

24.     // 获取图片的宽、高、像素格式和透明度等信息。
25.     uint32_t width, height, rowStride;
26.     int32_t pixelFormat, alphaType;
27.     OH_PixelmapImageInfo_GetWidth(imageInfo, &width);
28.     OH_PixelmapImageInfo_GetHeight(imageInfo, &height);
29.     OH_PixelmapImageInfo_GetRowStride(imageInfo, &rowStride);
30.     OH_PixelmapImageInfo_GetPixelFormat(imageInfo, &pixelFormat);
31.     OH_PixelmapImageInfo_GetAlphaType(imageInfo, &alphaType);
32.     OH_PixelmapImageInfo_Release(imageInfo);
33.     OH_LOG_INFO(LOG_APP,
34.                 "GetImageInfo success, width: %{public}d, height: %{public}d, "
35.                 "rowStride: %{public}d, pixelFormat: %{public}d, alphaType: %{public}d.",
36.                 width, height, rowStride, pixelFormat, alphaType);
37. }

38. 修改EXIF信息。

Image_ErrorCode OH_ImageSourceNative_ModifyImageProperty(OH_ImageSourceNative *source, Image_String *key, Image_String *value)

1. // 需要在src/main/cpp/CMakeLists.txt文件中链接so库文件：target_link_libraries(entry PUBLIC libhilog_ndk.z.so libimage_source.so)。
2. #include <string>
3. #include <hilog/log.h>
4. #include <multimedia/image_framework/image/image_source_native.h>

5. #undef LOG_DOMAIN
6. #undef LOG_TAG
7. #define LOG_DOMAIN 0x02b6
8. #define LOG_TAG "ImageKitDemo"

9. void ModifyImagePropertyExample(OH_ImageSourceNative *source) {
10.     if (!source) {
11.         OH_LOG_ERROR(LOG_APP, "ModifyImagePropertyExample: source is nullptr");
12.         return;
13.     }
14.     const std::string keyStr = OHOS_IMAGE_PROPERTY_ORIENTATION;
15.     const std::string valueStr = "Top-left";
16.     Image_String key{const_cast<char *>(keyStr.c_str()), keyStr.length()};
17.     Image_String value{const_cast<char *>(valueStr.c_str()), valueStr.length()};

18.     Image_ErrorCode ret = OH_ImageSourceNative_ModifyImageProperty(source, &key, &value);
19.     if (ret != IMAGE_SUCCESS) {
20.         OH_LOG_ERROR(LOG_APP, "ModifyImageProperty failed, code=%{public}d", ret);
21.         return;
22.     }

23.     OH_LOG_INFO(LOG_APP, "ModifyImageProperty success, key=%{public}s, value=%{public}s", keyStr.c_str(),
24.                 valueStr.c_str());
25. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-rotate-faq "如何获取图片的旋转角度信息")
# 设置铃声

更新时间: 2025-12-16 16:35

1. 导入ringtone模块和相关公共模块。
    
    1. import { common } from '@kit.AbilityKit';
    2. import { ringtone } from '@kit.RingtoneKit'
    3. import { uniformTypeDescriptor } from '@kit.ArkData';
    4. import { JSON } from '@kit.ArkTS';
    5. import { hilog } from '@kit.PerformanceAnalysisKit';
    6. const APP_TAG = "Msc_Demo"
    7. const DOMAIN = 0x0001
    
2. 调用[ringtone.getSupportedRingtoneTypes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ringtone-ringtone#section81796536265)接口，查询支持设置的铃声类型。
    
    1. let ringtoneTypeList: Array<ringtone.RingtoneType> = ringtone.getSupportedRingtoneTypes();
    2. hilog.info(DOMAIN, APP_TAG,'getSupportedRingtoneTypes : ' + JSON.stringify(ringtoneTypeList));
    
3. 调用[ringtone.getSupportedDataTypes](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ringtone-ringtone#section1858041418291)接口，查询支持的数据类型。当前支持格式：MP3，OGG，FLAC，AAC，MP2，M4A。
    
    1. // 其中 ringtone.RingtoneType.NOTIFICATION 为通知铃声
    2. let dataTypeList: Array<uniformTypeDescriptor.UniformDataType> = ringtone.getSupportedDataTypes(ringtone.RingtoneType.NOTIFICATION);
    3. hilog.info(DOMAIN, APP_TAG,'getSupportedDataTypes: ' + JSON.stringify(dataTypeList));
    
4. 调用[ringtone.startRingtoneSetting](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ringtone-ringtone#section5949453189)接口拉起设置弹窗，用户设置铃声后返回设置的铃声类型。
    
    通过promise异步方式：
    
    1. // 详细代码参考API参考
    2. let prefixUri: string = '';
    3. let audioPath: string = prefixUri + '/' + this.buttonText;
    4. let fileName: string = audioPath.substring(audioPath.lastIndexOf('/') + 1, audioPath.lastIndexOf('.'));
    5. await ringtone.startRingtoneSetting(this.context, audioPath, fileName).then(res => {
    6.   hilog.info(DOMAIN, APP_TAG,'setFlag :' + res);
    7. });
    
    通过callback异步方式：
    
    8. // 详细代码参考API参考
    9. let prefixUri: string = '';
    10. let audioPath: string = prefixUri + '/' + this.buttonText;
    11. let fileName: string = audioPath.substring(audioPath.lastIndexOf('/') + 1, audioPath.lastIndexOf('.'));
    12. ringtone.startRingtoneSetting(this.context, audioPath, fileName, (err, data) => {
    13.   hilog.info(DOMAIN, APP_TAG,'setFlag :' + data);
    14. }); 
    
5. 调用[ringtone.getSupportedMaxDuration](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ringtone-ringtone#section759192934316)接口，获取当前铃声支持的最大时长。
    
    1. // 其中 ringtone.RingtoneType.MESSAGE 为短信铃声
    2. let maxDuration: number =
    3.   ringtone.getSupportedMaxDuration(ringtone.RingtoneType.MESSAGE, uniformTypeDescriptor.UniformDataType.MP3)
    4. hilog.info(DOMAIN, APP_TAG,'getSupportedMaxDuration: ' + maxDuration);
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ringtone-introduction "Ringtone Kit简介")
