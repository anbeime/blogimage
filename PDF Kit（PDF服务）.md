# PDF Kit简介

更新时间: 2025-12-16 16:35

PDF Kit（PDF服务）包含pdfService和PdfView组件。

pdfService提供了加载和保存PDF文档、在PDF页面中添加文本内容、图片、批注、页眉页脚、水印、背景图片、书签、判断PDF文档是否加密及删除文档加密等相关的功能，对PDF文档的操作有更多的应用场景。

PdfView组件提供了文档预览功能，如：PDF文档预览、高亮显示、搜索关键字，批注等场景。

PDF Kit更多的示例代码请参考[CodeLab](https://developer.huawei.com/consumer/cn/codelabsPortal/carddetails/tutorials_PDFKit-Codelab-Clientdemo-ArkTS)和[SampleCode](https://gitcode.com/harmonyos_samples/pdfkit_-sample-code_-arkts)。

## pdfService与PdfView能力比较

|PDF Kit能力|pdfService是否支持|PdfView预览组件是否支持|
|:--|:--|:--|
|打开和保存文档|支持|支持|
|释放文档|支持|支持|
|PDF文档转图片|支持|支持|
|添加、删除批注|支持|支持|
|管理书签|支持|不支持|
|添加、编辑、删除PDF页|支持|不支持|
|添加、删除文本内容|支持|不支持|
|添加、删除图片内容|支持|不支持|
|编辑页眉页脚、水印、背景|支持|不支持|
|判断PDF文档是否加密|支持|不支持|
|删除文档加密|支持|不支持|
|PDF文档预览|不支持|支持|
|搜索关键字|不支持|支持|
|PDF文档监听回调|不支持|支持|

## 约束与限制

### 支持的国家和地区

当前PDF Kit仅中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。

### 支持的设备

PDF Kit相关能力支持在Phone、Tablet和PC/2in1设备上运行。

### 模拟器支持的情况

本Kit支持模拟器开发，但与真机存在部分能力差异，详情请参见“[模拟器与真机的差异](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-emulator-specification#section38231424133213)”。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-kit-guide "PDF Kit（PDF服务）")
# 打开和保存PDF文档

更新时间: 2025-12-16 16:36

对PDF文档[添加内容](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-add-txt-img-annot)、[页眉页脚](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-add-headerfooter)、[水印](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-add-watermark)、[背景图片](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-add-background)或[书签](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-add-bookmark)等操作前，需要打开文档，并且在文档操作完成后，保存PDF文档。

pdfService和PdfView都可实现打开和保存文档，使用场景上有如下区别：

- 需要对PDF文档做相关的编辑和操作，建议使用pdfService的能力打开和保存文档。
- 需要预览、搜索关键字、监听PDF文档回调和批注等操作，推荐使用PdfView打开。

## 接口说明

|接口名|描述|
|:--|:--|
|[loadDocument](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section167288392229)(path: string, password?: string, onProgress?: (progress: number) => number): ParseResult|加载指定文档路径。|
|[saveDocument](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section660833016157)(path: string, onProgress?: (progress: number) => number): boolean|保存文档。|

## 示例代码

1. 调用loadDocument方法，加载PDF文档。
2. 在【Save As】和【Save】两个按钮中调用saveDocument方法，分别实现了另存为PDF文档和保存覆盖源PDF文档的两种方式。

3. import { pdfService } from '@kit.PDFKit';
4. import { hilog } from '@kit.PerformanceAnalysisKit';
5. import { fileIo } from '@kit.CoreFileKit';
6. import { BusinessError } from '@kit.BasicServicesKit';

7. @Entry
8. @Component
9. struct PdfPage {
10.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
11.   private context = this.getUIContext().getHostContext() as Context;
12.   private filePath = '';
13.   @State saveEnable: boolean = false;

14.   aboutToAppear(): void {
15.     this.filePath = this.context.filesDir + '/input.pdf';
16.     try {
17.       let res = fileIo.accessSync(this.filePath);
18.       if(!res) {
19.         // 确保在工程目录src/main/resources/rawfile里有input.pdf文档
20.         let content: Uint8Array = this.context.resourceManager.getRawFileContentSync('rawfile/input.pdf');
21.         let fdSand =
22.           fileIo.openSync(this.filePath, fileIo.OpenMode.WRITE_ONLY | fileIo.OpenMode.CREATE | fileIo.OpenMode.TRUNC);
23.         fileIo.writeSync(fdSand.fd, content.buffer);
24.         fileIo.closeSync(fdSand.fd);
25.       }
26.       this.pdfDocument.loadDocument(this.filePath);
27.     } catch (e) {
28.       let error: BusinessError = e as BusinessError;
29.       hilog.error(0x0000, 'PdfPage', `Failed to loadDocument. Code: ${error.code}, message: ${error.message} `);
30.     }
31.   }

32.   build() {
33.     Column() {
34.       // 另存为一份PDF文档
35.       Button('Save As').onClick(() => {
36.         // 可以对PDF文档添加页眉页脚，水印，背景等一些内容，然后另存文档
37.         let outPdfPath = this.context.filesDir + '/testSaveAsPdf.pdf';
38.         let result = this.pdfDocument.saveDocument(outPdfPath);
39.         this.saveEnable = true;
40.         hilog.info(0x0000, 'PdfPage', 'saveAsPdf %{public}s!', result ? 'success' : 'fail');
41.       })
42.       // 保存覆盖源PDF文档
43.       Button('Save').enabled(this.saveEnable).onClick(() => {
44.         // 这里可以对PDF文档添加内容、页眉页脚、水印、背景等一些内容，然后保存文档
45.         let tempDir = this.context.tempDir;
46.         let tempFilePath = tempDir + `/temp${Math.random()}.pdf`;
47.         try {
48.           fileIo.copyFileSync(this.filePath, tempFilePath);
49.         } catch (e) {
50.           let error: BusinessError = e as BusinessError;
51.           hilog.error(0x0000, 'PdfPage', `Failed to copyFileSync. Code: ${error.code}, message: ${error.message} `);
52.         }
53.         let pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
54.         // 加载临时文档
55.         let loadResult = pdfDocument.loadDocument(tempFilePath, '');
56.         if (loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
57.           let result = pdfDocument.saveDocument(this.filePath);
58.           hilog.info(0x0000, 'PdfPage', 'savePdf %{public}s!', result ? 'success' : 'fail');
59.         }
60.       })
61.     }
62.   }
63. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-pdfservice-implements "pdfService能力")
# 添加、删除PDF页

更新时间: 2025-12-16 16:36

在PDF文档中添加或删除页面，包括：

- 添加单个、多个空白页到PDF文档。
- 删除PDF文档中单个、多个指定页。
- 将其他PDF文档页添加到本PDF文档。

## 接口说明

|接口名|描述|
|:--|:--|
|[insertBlankPage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section18418154319159)(index: number, width: number, height: number): PdfPage|在指定位置插入空白PDF页。|
|[getPage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section1221013163209)(index: number): PdfPage|获取指定页的对象。|
|[insertPageFromDocument](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section7656515132015)(document: PdfDocument, fromIndex: number, pageCount: number, index: number): PdfPage|将其他文档的页添加到当前文档。|
|[deletePage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section1472716318565)(index: number, count: number): void|删除指定的PDF页。|

## 示例代码

1. 调用loadDocument方法，加载PDF文档。
2. 调用getPage方法获取当前页，用于获取页面宽高。
3. 调用insertBlankPage和insertPageFromDocument方法实现如下功能。
    1. 插入单个空白页。
    2. 插入多个空白页。
    3. 将input2.pdf文档的索引1、2、3页插入到input.pdf索引0的位置，并另存文档。
4. 调用deletePage方法删除单个或多个索引页。

5. import { pdfService } from '@kit.PDFKit';
6. import { hilog } from '@kit.PerformanceAnalysisKit';

7. @Entry
8. @Component
9. struct PdfPage {
10.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
11.   private context = this.getUIContext().getHostContext() as Context;

12.   aboutToAppear(): void {
13.     // 确保沙箱目录有input.pdf文档
14.     let filePath = this.context.filesDir + '/input.pdf';
15.     this.pdfDocument.loadDocument(filePath);
16.   }

17.   build() {
18.     Column() {
19.       // 插入单个空白页
20.       Button('insertBlankPage').onClick(async () => {
21.         let page: pdfService.PdfPage = this.pdfDocument.getPage(0);
22.         let page2: pdfService.PdfPage = this.pdfDocument.insertBlankPage(2, page.getWidth(), page.getHeight());
23.         let outPdfPath = this.context.filesDir + '/testInsertBlankPage.pdf';
24.         let result = this.pdfDocument.saveDocument(outPdfPath);
25.         hilog.info(0x0000, 'PdfPage', 'insertBlankPage %{public}s!', result ? 'success' : 'fail');
26.       })
27.       // 插入多个空白页
28.       Button('insertSomeBlankPage').onClick(async () => {
29.         let page: pdfService.PdfPage = this.pdfDocument.getPage(0);
30.         for (let i = 0; i < 3; i++) {
31.           this.pdfDocument.insertBlankPage(2, page.getWidth(), page.getHeight());
32.         }
33.         let outPdfPath = this.context.filesDir + '/testInsertSomeBlankPage.pdf';
34.         let result = this.pdfDocument.saveDocument(outPdfPath);
35.         hilog.info(0x0000, 'PdfPage', 'insertSomeBlankPage %{public}s!', result ? 'success' : 'fail');
36.       })
37.       // 将input2.pdf文档的索引1,2,3页插入到input.pdf索引0的位置，并另存文档
38.       Button('insertPageFromDocument').onClick(async () => {
39.         let pdfDoc: pdfService.PdfDocument = new pdfService.PdfDocument();
40.         // 确保该沙箱目录下有 input2.pdf文档
41.         pdfDoc.loadDocument(this.context.filesDir + '/input2.pdf');
42.         this.pdfDocument.insertPageFromDocument(pdfDoc, 1, 3, 0);
43.         let outPdfPath = this.context.filesDir + '/testInsertPageFromDocument.pdf';
44.         let result = this.pdfDocument.saveDocument(outPdfPath);
45.         hilog.info(0x0000, 'PdfPage', 'insertPageFromDocument %{public}s!', result ? 'success' : 'fail');
46.       })
47.       // 删除单个或多个索引页
48.       Button('deletePage').onClick(async () => {
49.         this.pdfDocument.deletePage(2, 2);
50.         let outPdfPath = this.context.filesDir + '/testDeletePage.pdf';
51.         let result = this.pdfDocument.saveDocument(outPdfPath);
52.         hilog.info(0x0000, 'PdfPage', 'deletePage %{public}s!', result ? 'success' : 'fail');
53.       })      
54.     }
55.   }
56. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-open-document "打开和保存PDF文档")
# PDF页面文本、图片和批注

更新时间: 2025-12-16 16:37

支持编辑PDF页面内容，包括：

- 添加、删除文本。
- 添加、删除图片。
- 添加、修改、删除批注。
    
    通过索引指定PDF页面添加批注，并对批注在页面中的位置，字体、批注边框等设置，批注提供了多种风格样式，包括：文本批注[TextAnnotationInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section31971811203120)、下划线批注[LineAnnotationInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section19125125519345)、高亮批注[HighlightAnnotationInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section42937218352)、删除线批注[StrikethroughAnnotationInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section1079774919358)等共13种。
    

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163702.44863519399791193268917657793623:50001231000000:2800:C2DABAC72C7E53B4251D6AF58B5EDE2F225E02B32575A6476E293B5D062AEFB4.png "点击放大")

## 接口说明

|接口名|描述|
|:--|:--|
|[addTextObject](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section67811517143913)(text: string, x: number, y: number, style: TextStyle): void|添加文本内容，只可按行添加。|
|[addImageObject](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section699712112399)(path: string, x: number, y: number, width: number, height: number): void|在PDF文档的页面中添加图片。|
|[deleteGraphicsObject](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section5391931153910)(object: GraphicsObject): void|删除指定的GraphicsObject。|
|[addAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section8253013193814)(annotationInfo: PdfAnnotationInfo): PdfAnnotation|在当前页添加批注。|

## 添加文本和图片

1. 调用loadDocument方法，加载PDF文档。
2. 在【addText】按钮中调用addTextObject的方法插入文本。
3. 在【delText】按钮中调用deleteGraphicsObject方法来删除相应的页面文本。
4. 在【addImage】按钮中调用addImageObject的方法插入图片。

5. import { pdfService } from '@kit.PDFKit';
6. import { hilog } from '@kit.PerformanceAnalysisKit';
7. import { Font } from '@kit.ArkUI';

8. @Entry
9. @Component
10. struct PdfPage {
11.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
12.   private context = this.getUIContext().getHostContext() as Context;

13.   aboutToAppear(): void {
14.     // 确保沙箱目录有input.pdf文档
15.     let filePath = this.context.filesDir + '/input.pdf';
16.     this.pdfDocument.loadDocument(filePath);
17.   }

18.   build() {
19.     Column() {
20.       // 添加文本
21.       Button('addText').onClick(async () => {
22.         let page: pdfService.PdfPage = this.pdfDocument.getPage(0);
23.         let str = 'This is add text object!';
24.         let fontInfo = new pdfService.FontInfo();
25.         // 确保字体路径存在
26.         let font: Font = new Font()
27.         fontInfo.fontPath = font.getFontByName('HarmonyOS Sans')?.path;
28.         fontInfo.fontName = '';
29.         let style: pdfService.TextStyle = { textColor: 0x000000, textSize: 30, fontInfo: fontInfo };
30.         page.addTextObject(str, 10, 10, style);
31.         let outPdfPath = this.context.filesDir + '/testAddText.pdf';
32.         let result = this.pdfDocument.saveDocument(outPdfPath);
33.         hilog.info(0x0000, 'PdfPage', 'addText %{public}s!', result ? 'success' : 'fail');
34.       })
35.       // 删除文本
36.       Button('delText').onClick(async () => {
37.         let page: pdfService.PdfPage = this.pdfDocument.getPage(0);
38.         let graphicsObjects = page.getGraphicsObjects();
39.         // 找到第一个要删除的文本
40.         let index = graphicsObjects.findIndex(item => item.type === pdfService.GraphicsObjectType.OBJECT_TEXT);
41.         if (index > -1) {
42.           // 删除第一个文本
43.           page.deleteGraphicsObject(graphicsObjects[index]);
44.         }
45.         let outPdfPath = this.context.filesDir + '/testDelText.pdf';
46.         let result = this.pdfDocument.saveDocument(outPdfPath);
47.         hilog.info(0x0000, 'PdfPage', 'delText %{public}s!', result ? 'success' : 'fail');
48.       })
49.       // 添加图片
50.       Button('addImage').onClick(async () => {
51.         let page: pdfService.PdfPage = this.pdfDocument.getPage(0);
52.         // 插入图片，确保沙箱目录有img.jpg图片
53.         let imagePath = this.context.filesDir + '/img.jpg';
54.         page.addImageObject(imagePath, 100, 100, 100, 120);
55.         let outPdfPath = this.context.filesDir + '/testAddImage.pdf';
56.         let result = this.pdfDocument.saveDocument(outPdfPath);
57.         hilog.info(0x0000, 'PdfPage', 'addImage %{public}s!', result ? 'success' : 'fail');
58.       })
59.     }
60.   }
61. }

## 添加文本批注

1. 调用loadDocument方法，加载PDF文档。
2. 调用getPage方法获取指定页。
3. 实例化TextAnnotationInfo文本批注，并设置相关属性。
4. 调用addAnnotation或setAnnotation方法添加或修改批注。
5. 调用removeAnnotation方法删除批注。

6. import { pdfService } from '@kit.PDFKit';
7. import { hilog } from '@kit.PerformanceAnalysisKit';

8. @Entry
9. @Component
10. struct PdfPage {
11.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
12.   private context = this.getUIContext().getHostContext() as Context;

13.   build() {
14.     Column() {
15.       // 添加批注
16.       Button('addTextAnnotation').onClick(async () => {
17.         // 确保沙箱目录有input.pdf文档
18.         let filePath = this.context.filesDir + '/input.pdf';
19.         this.pdfDocument.loadDocument(filePath);
20.         let page: pdfService.PdfPage = this.pdfDocument.getPage(0);
21.         let aInfo = new pdfService.TextAnnotationInfo();
22.         aInfo.iconName = 'cument Format';
23.         aInfo.content = 'this is a content';
24.         aInfo.subject = 'Annotation';
25.         aInfo.title = 'this is a title';
26.         aInfo.state = pdfService.TextAnnotationState.MARKED;
27.         aInfo.x = 200;
28.         aInfo.y = 200;
29.         aInfo.color = 0xf9b1b1;
30.         aInfo.flag = pdfService.AnnotationFlag.PRINTED;
31.         let annotation: pdfService.PdfAnnotation = page.addAnnotation(aInfo);
32.         let outPdfPath = this.context.filesDir + '/testAddTextAnnotation.pdf';
33.         let result = this.pdfDocument.saveDocument(outPdfPath);
34.         this.pdfDocument.releaseDocument();
35.         hilog.info(0x0000, 'PdfPage', 'addTextAnnotation %{public}s!', result ? 'success' : 'fail');
36.       })
37.       // 修改批注
38.       Button('setAnnotation').onClick(async () => {
39.         let filePath = this.context.filesDir + '/testAddTextAnnotation.pdf';
40.         let result = this.pdfDocument.loadDocument(filePath);
41.         if (result === pdfService.ParseResult.PARSE_SUCCESS) {
42.           let page: pdfService.PdfPage = this.pdfDocument.getPage(0);
43.           let annotations = page.getAnnotations();
44.           if (annotations.length > 0 && annotations[0].type === pdfService.AnnotationType.TEXT) {
45.             let newAnno = annotations[0];
46.             page.removeAnnotation(newAnno);
47.             let annotation = page.addAnnotation(newAnno);
48.             let newInfo = new pdfService.TextAnnotationInfo();
49.             newInfo.title = "new Title";
50.             newInfo.content = "new Info";
51.             newInfo.state = pdfService.TextAnnotationState.MARKED;
52.             newInfo.x = 100;
53.             newInfo.y = 100;
54.             page.setAnnotation(annotation, newInfo);
55.             let outPdfPath = this.context.filesDir + '/testSetAnnotation.pdf';
56.             let result = this.pdfDocument.saveDocument(outPdfPath);
57.             this.pdfDocument.releaseDocument();
58.             hilog.info(0x0000, 'PdfPage', 'setAnnotation %{public}s!', result ? 'success' : 'fail');
59.           }
60.         }
61.       })
62.       // 删除批注
63.       Button('removeAnnotation').onClick(async () => {
64.         let filePath = this.context.filesDir + '/testAddTextAnnotation.pdf';
65.         let result = this.pdfDocument.loadDocument(filePath);
66.         if (result === pdfService.ParseResult.PARSE_SUCCESS) {
67.           let page: pdfService.PdfPage = this.pdfDocument.getPage(0);
68.           let annotations = page.getAnnotations();
69.           if (annotations.length > 0 && annotations[0].type === pdfService.AnnotationType.TEXT) {
70.             page.removeAnnotation(annotations[0]);
71.             let outPdfPath = this.context.filesDir + '/testRemoveAnnotation.pdf';
72.             let result = this.pdfDocument.saveDocument(outPdfPath);
73.             this.pdfDocument.releaseDocument();
74.             hilog.info(0x0000, 'PdfPage', 'removeAnnotation %{public}s!', result ? 'success' : 'fail');
75.           }
76.         }
77.       })
78.     }
79.   }
80. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-add-delete-page "添加、删除PDF页")
# 转换指定页面或指定区域为图片

更新时间: 2025-12-16 16:37

## 场景介绍

PDF文档页面转换为图片，或将页面的指定区域转换为图片时使用。

## 接口说明

|接口名|描述|
|:--|:--|
|[getPagePixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section894811388610)(): image.PixelMap|获取当前页的图片。|
|[getCustomPagePixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section146346515368)(matrix: PdfMatrix, isGray: boolean, drawAnnotations: boolean): image.PixelMap|获取指定PdfPage区域的图片内容。|
|[getAreaPixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section76461612123920)(matrix: PdfMatrix, bitmapwidth: number, bitmapHeight: number, isGray: boolean, drawAnnotations: boolean): image.PixelMap|获取指定PdfPage区域的图片内容，并指定图片的宽和高。|
|[getAreaPixelMapWithOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section5838210143810)(matrix: PdfMatrix, bitmapwidth: number, bitmapHeight: number, options?: PixelOptions): image.PixelMap|获取指定PdfPage区域的图片内容，并指定图片的宽和高等参数。|

## 示例代码

1. 调用loadDocument方法加载PDF文档。
2. 调用getPage方法获取某个页面。
3. 调用getPagePixelMap，getAreaPixelMapWithOptions或getCustomPagePixelMap方法获取当前页面或者页面区域，这时获取的是image.PixelMap图像类型。
4. 将image.PixelMap图像类型转化为二进制图片文件并保存，参考以下方法pixelMap2Buffer。
    
    1. import { pdfService } from '@kit.PDFKit';
    2. import { image } from '@kit.ImageKit';
    3. import { fileIo as fs } from '@kit.CoreFileKit';
    4. import { BusinessError } from '@kit.BasicServicesKit';
    5. import { hilog } from '@kit.PerformanceAnalysisKit';
    
    6. @Entry
    7. @Component
    8. struct PdfPage {
    9.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
    10.   private context = this.getUIContext().getHostContext() as Context;
    11.   private loadResult: pdfService.ParseResult = pdfService.ParseResult.PARSE_ERROR_FORMAT;
    
    12.   aboutToAppear(): void {
    13.     // 确保沙箱目录有input.pdf文档
    14.     let filePath = this.context.filesDir + '/input.pdf';
    15.     this.loadResult = this.pdfDocument.loadDocument(filePath);
    16.   }
    
    17.   // 将 pixelMap 转成图片格式
    18.   pixelMap2Buffer(pixelMap: image.PixelMap): Promise<ArrayBuffer> {
    19.     return new Promise((resolve, reject) => {
    20.       /**
    21.        设置打包参数
    22.        format：图片打包格式
    23.        quality：JPEG 编码输出图片质量
    24.        bufferSize：图片大小
    25.        */
    26.       let packOpts: image.PackingOption = { format: 'image/jpeg', quality: 98 }
    27.       // 创建ImagePacker实例
    28.       const imagePackerApi = image.createImagePacker()
    29.       imagePackerApi.packToData(pixelMap, packOpts).then((buffer: ArrayBuffer) => {
    30.         resolve(buffer)
    31.       }).catch((err: BusinessError) => {
    32.         reject()
    33.       })
    34.     })
    35.   }
    
    36.   build() {
    37.     Column() {
    38.       // 获取为图片并保存到应用沙箱
    39.       Button('getPagePixelMap').onClick(async () => {
    40.         if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
    41.           let page = this.pdfDocument.getPage(0)
    42.           let pixmap: image.PixelMap = page.getPagePixelMap();
    43.           if (!pixmap) {
    44.             return
    45.           }
    46.           const imgBuffer = await this.pixelMap2Buffer(pixmap)
    47.           try {
    48.             const file =
    49.               fs.openSync(this.context.filesDir + `/${Date.now()}.png`, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
    50.             await fs.write(file.fd, imgBuffer)
    51.             // 关闭文档
    52.             await fs.close(file.fd)
    53.           } catch (e) {
    54.             let error: BusinessError = e as BusinessError;
    55.             hilog.error(0x0000, 'PdfPage', `Code: ${error.code}, message: ${error.message} `);
    56.           }
    57.         }
    58.       })
    59.       // 获取指定PdfPage区域的图片内容。
    60.       Button('getCustomPagePixelMap').onClick(async () => {
    61.         if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
    62.           let page = this.pdfDocument.getPage(0);
    63.           let matrix = new pdfService.PdfMatrix();
    64.           matrix.x = 100;
    65.           matrix.y = 100;
    66.           matrix.width = 500;
    67.           matrix.height = 500;
    68.           matrix.rotate = 0;
    69.           let pixmap: image.PixelMap = page.getCustomPagePixelMap(matrix, false, false);
    70.           if (!pixmap) {
    71.             return;
    72.           }
    73.           const imgBuffer = await this.pixelMap2Buffer(pixmap);
    74.           try {
    75.             const file =
    76.               fs.openSync(this.context.filesDir + `/${Date.now()}.jpeg`, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
    77.             await fs.write(file.fd, imgBuffer);
    78.             // 关闭文件
    79.             await fs.close(file.fd);
    80.           } catch (e) {
    81.             let error: BusinessError = e as BusinessError;
    82.             hilog.error(0x0000, 'PdfPage', `Code: ${error.code}, message: ${error.message} `);
    83.           }
    84.         }
    85.       })
    86.       // 获取指定PdfPage区域的图片内容
    87.       Button('getAreaPixelMap').onClick(async () => {
    88.         if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
    89.           //获取对应的page
    90.           let page = this.pdfDocument.getPage(0);
    91.           let matrix = new pdfService.PdfMatrix();
    92.           //设置matrix来控制需要获取的区域
    93.           matrix.x = 100;
    94.           matrix.y = 100;
    95.           matrix.width = 500;
    96.           matrix.height = 500;
    97.           matrix.rotate = 0;
    98.           let pixmap: image.PixelMap = page.getAreaPixelMap(matrix, 400, 400, true, false);
    99.           if (!pixmap) {
    100.             return
    101.           }
    102.           const imgBuffer = await this.pixelMap2Buffer(pixmap)
    103.           try {
    104.             const file =
    105.               fs.openSync(this.context.filesDir + `/${Date.now()}.bmp`, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
    106.             await fs.write(file.fd, imgBuffer)
    107.             // 关闭文件
    108.             await fs.close(file.fd);
    109.           } catch (e) {
    110.             let error: BusinessError = e as BusinessError;
    111.             hilog.error(0x0000, 'PdfPage', `Code: ${error.code}, message: ${error.message} `);
    112.           }
    113.         }
    114.       })
    115.       // 获取指定PdfPage区域的图片内容
    116.       Button('getAreaPixelMapWithOptions').onClick(async () => {
    117.         if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
    118.           //获取对应page
    119.           let page = this.pdfDocument.getPage(0);
    120.           let matrix = new pdfService.PdfMatrix();
    121.           //设置matrix来控制需要获取的区域
    122.           matrix.x = 100;
    123.           matrix.y = 100;
    124.           matrix.width = 500;
    125.           matrix.height = 500;
    126.           matrix.rotate = 0;
    127.           //设置pixelmap是否黑白，背景是否透明等参数
    128.           let options = new pdfService.PixelOptions();
    129.           options.isGray = false;
    130.           options.drawAnnotations = true;
    131.           options.isTransparent = true;
    132.           let pixmap: image.PixelMap = page.getAreaPixelMapWithOptions(matrix, 400, 400, options);
    133.           if (!pixmap) {
    134.             return
    135.           }
    136.           const imgBuffer = await this.pixelMap2Buffer(pixmap)
    137.           try {
    138.             const file =
    139.               fs.openSync(this.context.filesDir + `/${Date.now()}.bmp`, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
    140.             await fs.write(file.fd, imgBuffer)
    141.             // 关闭文件
    142.             await fs.close(file.fd);
    143.           } catch (e) {
    144.             let error: BusinessError = e as BusinessError;
    145.             hilog.error(0x0000, 'PdfPage', `Code: ${error.code}, message: ${error.message} `);
    146.           }
    147.         }
    148.       })
    149.     }
    150.   }
    151. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-doc-to-imgs "转换PDF文档为图片")
# 转换整个PDF文档为图片

更新时间: 2025-12-16 16:38

## 场景介绍

将整个PDF文档的页面转换为图片，每页为一张图片，并且所有图片存放在指定的同一个文件夹下。

当前支持的图片格式请参考[ImageFormat](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section1713111745313)。

## 接口说明

|接口名|描述|
|:--|:--|
|[convertToImage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section1029783924311)(path: string, format: ImageFormat, onProgress?: (progress: number) => number): boolean|转换PDF文档为图片。|

## 示例代码

1. 调用loadDocument方法，加载PDF文档。
2. 设置要输出图片的文件夹，调用convertToImage方法转化PDF文档所有页面为图片。

3. import { fileIo as fs } from '@kit.CoreFileKit';
4. import { hilog } from '@kit.PerformanceAnalysisKit';
5. import { pdfService } from '@kit.PDFKit';

6. @Entry
7. @Component
8. struct PdfPage {
9.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
10.   private context = this.getUIContext().getHostContext() as Context;
11.   private loadResult: pdfService.ParseResult = pdfService.ParseResult.PARSE_ERROR_FORMAT;

12.   aboutToAppear(): void {
13.     // 确保沙箱目录有input.pdf文档
14.     let filePath = this.context.filesDir + '/input.pdf';
15.     this.loadResult = this.pdfDocument.loadDocument(filePath);
16.   }

17.   build() {
18.     Column() {
19.       // 获取为图片并保存到应用沙箱
20.       Button('convertToImage').onClick(async () => {
21.         if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
22.           let outputPath = this.getUIContext().getHostContext()?.filesDir + '/output/';
23.           fs.mkdir(outputPath);
24.           // 将所有的页面转化为png图片，并存储在output文件夹里，确保output文件夹目录存在
25.           let res = this.pdfDocument.convertToImage(outputPath, pdfService.ImageFormat.PNG);
26.           hilog.info(0x0000, 'PdfPage', 'convertToImage %{public}s!', res ? 'success' : 'fail');
27.         }
28.       })
29.     }
30.   }
31. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-get-img "转换指定页面或指定区域为图片")
# 判断PDF文档是否加密及删除加密

更新时间: 2025-12-16 16:37

PDF Kit支持判断PDF文档是否加密及删除PDF加密锁。

## 接口说明

|接口名|描述|
|:--|:--|
|[isEncrypted](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section8613112012)(path: string): boolean|判断当前文档是否已加密。|
|[removeSecurity](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section0716101115205)(): boolean|删除文档加密锁。|

## 示例代码

1. 调用isEncrypted方法，判断PDF文档是否加密。
2. 如果是加密PDF文档，调用removeSecurity方法移除PDF文档的加密锁。

3. import { pdfService } from '@kit.PDFKit';
4. import { hilog } from '@kit.PerformanceAnalysisKit';

5. @Entry
6. @Component
7. struct PdfPage {
8.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
9.   private context = this.getUIContext().getHostContext() as Context;

10.   build() {
11.     Column() {
12.       // 判断文档是否加密，并删除加密
13.       Button('isEncryptedAndRemoveSecurity').onClick(async () => {
14.         // 确保沙箱目录有input.pdf文档
15.         let filePath = this.context.filesDir + '/input.pdf';
16.         let isEncrypt = this.pdfDocument.isEncrypted(filePath);
17.         if (isEncrypt) {
18.           let hasRemoveEncrypt = this.pdfDocument.removeSecurity();
19.           hilog.info(0x0000, 'PdfPage', 'isEncryptedAndRemoveSecurity %{public}s!',
20.             hasRemoveEncrypt ? 'success' : 'fail');
21.         }
22.       })
23.     }
24.   }
25. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-convert-img "转换整个PDF文档为图片")
# 添加、删除页眉页脚

更新时间: 2025-12-16 16:37

PDF Kit支持对指定页面添加、删除页眉页脚。页眉页脚信息包含文字、日期和页码等相关内容，并可设置字体大小、颜色和间距等相关样式，具体属性参考[HeaderFooterInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section3237995481)。如下图：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163740.09170055181936285608077646621692:50001231000000:2800:1B33773A75A6D106C13DBDB218A7E3367E8A5F06D98745FAA401260F92263DDD.jpg "点击放大")

## 接口说明

|接口名|描述|
|:--|:--|
|[addHeaderFooter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section4211341401)(info: HeaderFooterInfo, startIndex: number, endIndex: number, oddPages: boolean, evenPages: boolean): void|插入PDF文档页眉页脚。|
|[removeHeaderFooter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section19996123722218)(): boolean|删除PDF文档页眉页脚。|

注意

[addHeaderFooter](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section4211341401)方法属于耗时业务，需要遍历每一页去添加页眉页脚，添加页面较多时建议放到线程里去处理。

## 示例代码

**添加页眉页脚：**

1. 调用loadDocument方法，加载PDF文档。
2. 实例化页眉页脚HeaderFooterInfo类，并设置相关属性，包括字体大小、颜色和间距等。
3. 调用addHeaderFooter方法，添加页眉页脚到页面中。
4. 保存PDF文档到应用沙箱。

**删除页眉页脚：**

1. 调用loadDocument方法，加载PDF文档。
2. 调用removeHeaderFooter方法，删除页眉页脚。
3. 保存PDF文档到应用沙箱。

4. import { pdfService } from '@kit.PDFKit';
5. import { hilog } from '@kit.PerformanceAnalysisKit';
6. import { Font } from '@kit.ArkUI';

7. @Entry
8. @Component
9. struct PdfPage {
10.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
11.   private context = this.getUIContext().getHostContext() as Context;

12.   build() {
13.     Column() {
14.       Button('addHeaderFooter').onClick(async () => {
15.         // 确保沙箱目录有input.pdf文档
16.         let filePath = this.context.filesDir + '/input.pdf';
17.         let res = this.pdfDocument.loadDocument(filePath);
18.         if (res === pdfService.ParseResult.PARSE_SUCCESS) {
19.           let hfInfo: pdfService.HeaderFooterInfo = new pdfService.HeaderFooterInfo();
20.           hfInfo.fontInfo = new pdfService.FontInfo();
21.           // 确保字体路径存在
22.           let font: Font = new Font()
23.           hfInfo.fontInfo.fontPath = font.getFontByName('HarmonyOS Sans')?.path;
24.           // 如果不知道字体的具体名称，可以为空字符串
25.           hfInfo.fontInfo.fontName = '';
26.           hfInfo.textSize = 10;
27.           hfInfo.charset = pdfService.CharsetType.PDF_FONT_DEFAULT_CHARSET;
28.           hfInfo.underline = false;
29.           hfInfo.textColor = 0x00000000;
30.           hfInfo.leftMargin = 1.0;
31.           hfInfo.topMargin = 40.0;
32.           hfInfo.rightMargin = 1.0;
33.           hfInfo.bottomMargin = 40.0;
34.           hfInfo.headerLeftText = 'left H <<dd.mm.yyyy>> <<1/n>>';
35.           hfInfo.headerCenterText = 'center H <<m/d/yyyy>> <<1/n>>';
36.           hfInfo.headerRightText = 'right H <<m/d>><<1>>';
37.           hfInfo.footerLeftText = 'left F <<m/d>><<1>>';
38.           hfInfo.footerCenterText = 'center F <<m/d>><<1>>';
39.           hfInfo.footerRightText = 'right F <<dd.mm.yyyy>><<1>>';
40.           this.pdfDocument.addHeaderFooter(hfInfo, 1, 5, true, true);
41.           let outPdfPath = this.context.filesDir + '/testAddHeaderFooter.pdf';
42.           let result = this.pdfDocument.saveDocument(outPdfPath);
43.           hilog.info(0x0000, 'PdfPage', 'addHeaderFooter %{public}s!', result ? 'success' : 'fail');
44.         }
45.         this.pdfDocument.releaseDocument();
46.       })
47.       Button('removeHeaderFooter').onClick(async () => {
48.         let filePath = this.context.filesDir + '/testAddHeaderFooter.pdf';
49.         let res = this.pdfDocument.loadDocument(filePath);
50.         if (res === pdfService.ParseResult.PARSE_SUCCESS && this.pdfDocument.hasHeaderFooter()) {
51.           let removeResult = this.pdfDocument.removeHeaderFooter();
52.           if (removeResult) {
53.             let outPdfPath = this.context.filesDir + '/removeHeaderFooter.pdf';
54.             let result = this.pdfDocument.saveDocument(outPdfPath);
55.             hilog.info(0x0000, 'PdfPage', 'removeHeaderFooter %{public}s!', result ? 'success' : 'fail');
56.           }
57.         }
58.         this.pdfDocument.releaseDocument();
59.       })
60.     }
61.   }
62. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-add-bookmark "添加、删除书签")
# 添加、删除水印

更新时间: 2025-12-16 16:37

对指定页面添加水印，包括文本水印或图片水印。

- 文本水印可以设置字体、大小、旋转，位置等属性。
- 图片水印可以设置缩放、旋转、透明度和位置等属性。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163741.63673377512831047517601989065568:50001231000000:2800:93203007FEE581948398439E1E0BB60949C8866439A0ED0F819FB212D0044942.png)

## 接口说明

|接口名|描述|
|:--|:--|
|[addWatermark](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section206080386472)(info: WatermarkInfo, startIndex: number, endIndex: number, oddPages: boolean, evenPages: boolean): void|插入水印到PDF文档。如果插入的是图片，支持的图片格式参考[ImageFormat](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section1713111745313)，文本字符无限制。|
|[removeWatermark](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section18585132044815)(): boolean|删除PDF文档水印。|

注意

[addWatermark](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section206080386472)方法属于耗时业务，需要遍历每一页去添加水印，添加页面较多时建议放到线程里去处理。

## 示例代码

### 添加文本水印

**添加文本水印：**

1. 调用loadDocument方法，加载PDF文档。
2. 实例化文本水印TextWatermarkInfo类，并设置相关属性，包括字体、大小、旋转，位置等。
3. 调用addWatermark，添加文本水印。
4. 保存PDF文档到应用沙箱。

**删除文本水印：**

1. 调用loadDocument方法，加载PDF文档。
2. 调用removeWatermark，删除文本水印。
3. 保存PDF文档到应用沙箱。

4. import { pdfService } from '@kit.PDFKit';
5. import { hilog } from '@kit.PerformanceAnalysisKit';
6. import { Font } from '@kit.ArkUI';

7. @Entry
8. @Component
9. struct PdfPage {
10.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
11.   private context = this.getUIContext().getHostContext() as Context;

12.   build() {
13.     Column() {
14.       Button('addTextWatermark').onClick(async () => {
15.         // 确保沙箱目录有input.pdf文档
16.         let filePath = this.context.filesDir + '/input.pdf';
17.         let res = this.pdfDocument.loadDocument(filePath);
18.         if (res === pdfService.ParseResult.PARSE_SUCCESS) {
19.           let wminfo: pdfService.TextWatermarkInfo = new pdfService.TextWatermarkInfo();
20.           wminfo.watermarkType = pdfService.WatermarkType.WATERMARK_TEXT;
21.           wminfo.content = 'This is Watermark';
22.           wminfo.textSize = 30;
23.           wminfo.textColor = 200;
24.           wminfo.fontInfo = new pdfService.FontInfo();
25.           // 确保字体路径存在
26.           let font: Font = new Font()
27.           wminfo.fontInfo.fontPath = font.getFontByName('HarmonyOS Sans').path;
28.           wminfo.opacity = 0.5;
29.           wminfo.isOnTop = true;
30.           wminfo.rotation = 45;
31.           wminfo.scale = 1.5;
32.           wminfo.opacity = 0.5;
33.           wminfo.verticalAlignment = pdfService.WatermarkAlignment.WATERMARK_ALIGNMENT_TOP;
34.           wminfo.horizontalAlignment = pdfService.WatermarkAlignment.WATERMARK_ALIGNMENT_LEFT;
35.           wminfo.horizontalSpace = 1.0;
36.           wminfo.verticalSpace = 1.0;
37.           this.pdfDocument.addWatermark(wminfo, 0, 5, true, true);
38.           let outPdfPath = this.context.filesDir + '/testTextWatermark.pdf';
39.           let result = this.pdfDocument.saveDocument(outPdfPath);
40.           hilog.info(0x0000, 'PdfPage', 'addTextWatermark %{public}s!', result ? 'success' : 'fail');
41.         }
42.         this.pdfDocument.releaseDocument();
43.       })
44.       Button('removeTextWatermark').onClick(async () => {
45.         let filePath = this.context.filesDir + '/testTextWatermark.pdf';
46.         let res = this.pdfDocument.loadDocument(filePath);
47.         if (res === pdfService.ParseResult.PARSE_SUCCESS && this.pdfDocument.hasWatermark()) {
48.           let removeResult = this.pdfDocument.removeWatermark();
49.           if (removeResult) {
50.             let outPdfPath = this.context.filesDir + '/removeWatermark.pdf';
51.             let result = this.pdfDocument.saveDocument(outPdfPath);
52.             hilog.info(0x0000, 'PdfPage', 'removeWatermark %{public}s!', result ? 'success' : 'fail');
53.           }
54.         }
55.         this.pdfDocument.releaseDocument();
56.       })
57.     }
58.   }
59. }

### 添加图片水印

**添加图片水印：**

1. 调用loadDocument方法加载PDF文档。
2. 实例化图片水印ImageWatermarkInfo类，并设置相关属性，包括缩放、旋转、透明度和位置等。
3. 调用addWatermark添加图片水印。
4. 保存PDF文档到应用沙箱。

**删除图片水印：**

1. 调用loadDocument方法加载PDF文档。
2. 调用removeWatermark删除图片水印。
3. 保存PDF文档到应用沙箱。

4. import { pdfService } from '@kit.PDFKit';
5. import { hilog } from '@kit.PerformanceAnalysisKit';

6. @Entry
7. @Component
8. struct PdfPage {
9.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
10.   private context = this.getUIContext().getHostContext() as Context;

11.   build() {
12.     Column() {
13.       Button('addImageWatermark').onClick(async () => {
14.         let filePath = this.context.filesDir + '/input.pdf';
15.         let res = this.pdfDocument.loadDocument(filePath);
16.         if (res === pdfService.ParseResult.PARSE_SUCCESS) {
17.           let wminfo: pdfService.ImageWatermarkInfo = new pdfService.ImageWatermarkInfo();
18.           wminfo.watermarkType = pdfService.WatermarkType.WATERMARK_IMAGE;
19.           // 确保沙箱目录有img.jpg文档
20.           wminfo.imagePath = this.context.filesDir + '/img.jpg';
21.           wminfo.opacity = 0.5;
22.           wminfo.isOnTop = true;
23.           wminfo.rotation = 45;
24.           wminfo.scale = 0.5;
25.           wminfo.opacity = 0.5;
26.           wminfo.verticalAlignment = pdfService.WatermarkAlignment.WATERMARK_ALIGNMENT_TOP;
27.           wminfo.horizontalAlignment = pdfService.WatermarkAlignment.WATERMARK_ALIGNMENT_LEFT;
28.           wminfo.horizontalSpace = 1.0;
29.           wminfo.verticalSpace = 1.0;
30.           this.pdfDocument.addWatermark(wminfo, 0, 5, true, true);
31.           let outPdfPath = this.context.filesDir + '/testImageWatermark.pdf';
32.           let result = this.pdfDocument.saveDocument(outPdfPath);
33.           hilog.info(0x0000, 'PdfPage', 'addImageWatermark %{public}s!', result ? 'success' : 'fail');
34.         }
35.         this.pdfDocument.releaseDocument();
36.       })
37.       Button('removeImageWatermark').onClick(async () => {
38.         let filePath = this.context.filesDir + '/testImageWatermark.pdf';
39.         let res = this.pdfDocument.loadDocument(filePath);
40.         if (res === pdfService.ParseResult.PARSE_SUCCESS && this.pdfDocument.hasWatermark()) {
41.           let removeResult = this.pdfDocument.removeWatermark();
42.           if (removeResult) {
43.             let outPdfPath = this.context.filesDir + '/removeImageWatermark.pdf';
44.             let result = this.pdfDocument.saveDocument(outPdfPath);
45.             hilog.info(0x0000, 'PdfPage', 'removeImageWatermark %{public}s!', result ? 'success' : 'fail');
46.           }
47.         }
48.         this.pdfDocument.releaseDocument();
49.       })
50.     }
51.   }
52. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-add-headerfooter "添加、删除页眉页脚")
# 添加、删除背景

更新时间: 2025-12-16 16:37

对指定页面添加背景图片或背景颜色，并设置大小、旋转、透明度和位置等属性，支持图片格式：PNG、BMP、JPEG。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163742.58702586740004184494753458327290:50001231000000:2800:959AEF0F5ACE6014FA5E1F3279DA9884A62BA32A3A6EBAE8B57C284C24061851.png)

## 接口说明

|接口名|描述|
|:--|:--|
|[addBackground](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section13641714101419)(info: BackgroundInfo, startIndex: number, endIndex: number, oddPages: boolean, evenPages: boolean): void|插入PDF文档背景。|
|[removeBackground](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section16476184082314)(): boolean|删除PDF文档背景。|

注意

[addBackground](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section13641714101419)方法属于耗时业务，需要遍历每一页去添加背景，添加页面较多时建议放到线程里去处理。

## 示例代码

**添加背景：**

1. 调用loadDocument方法，加载PDF文档。
2. 实例化背景BackgroundInfo类，并设置相关属性，包括大小、旋转、透明度和位置等。
3. 调用addBackground方法，添加背景。
4. 保存PDF文档到应用沙箱。

**删除背景：**

1. 调用loadDocument方法，加载PDF文档。
2. 调用removeBackground方法，去除背景。
3. 保存PDF文档到应用沙箱。

4. import { pdfService } from '@kit.PDFKit';
5. import { hilog } from '@kit.PerformanceAnalysisKit';

6. @Entry
7. @Component
8. struct PdfPage {
9.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
10.   private context = this.getUIContext().getHostContext() as Context;

11.   build() {
12.     Column() {
13.       Button('addBackground').onClick(async () => {
14.         // 确保沙箱目录有input.pdf文档
15.         let filePath = this.context.filesDir + '/input.pdf';
16.         let res = this.pdfDocument.loadDocument(filePath);
17.         if (res === pdfService.ParseResult.PARSE_SUCCESS) {
18.           let bginfo: pdfService.BackgroundInfo = new pdfService.BackgroundInfo();
19.           // 确保沙箱目录有img.jpg文档
20.           bginfo.imagePath = this.context.filesDir + '/img.jpg';
21.           bginfo.backgroundColor = 50;
22.           bginfo.isOnTop = true;
23.           bginfo.rotation = 45;
24.           bginfo.scale = 0.5;
25.           bginfo.opacity = 0.3;
26.           bginfo.verticalAlignment = pdfService.BackgroundAlignment.BACKGROUND_ALIGNMENT_TOP;
27.           bginfo.horizontalAlignment = pdfService.BackgroundAlignment.BACKGROUND_ALIGNMENT_LEFT;
28.           bginfo.horizontalSpace = 1.0;
29.           bginfo.verticalSpace = 1.0;
30.           this.pdfDocument.addBackground(bginfo, 0, 2, true, true);
31.           let outPdfPath = this.context.filesDir + '/testAddBackground.pdf';
32.           let result = this.pdfDocument.saveDocument(outPdfPath);
33.           hilog.info(0x0000, 'PdfPage', 'addBackground %{public}s!', result ? 'success' : 'fail');
34.         }
35.         this.pdfDocument.releaseDocument();
36.       })
37.       Button('removeBackground').onClick(async () => {
38.         let filePath = this.context.filesDir + '/testAddBackground.pdf';
39.         let res = this.pdfDocument.loadDocument(filePath);
40.         if (res === pdfService.ParseResult.PARSE_SUCCESS && this.pdfDocument.hasBackground()) {
41.           let removeResult = this.pdfDocument.removeBackground();
42.           if (removeResult) {
43.             let outPdfPath = this.context.filesDir + '/removeBackground.pdf';
44.             let result = this.pdfDocument.saveDocument(outPdfPath);
45.             hilog.info(0x0000, 'PdfPage', 'removeBackground %{public}s!', result ? 'success' : 'fail');
46.           }
47.         }
48.         this.pdfDocument.releaseDocument();
49.       })
50.     }
51.   }
52. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-add-watermark "添加、删除水印")
# 添加、删除背景

更新时间: 2025-12-16 16:37

对指定页面添加背景图片或背景颜色，并设置大小、旋转、透明度和位置等属性，支持图片格式：PNG、BMP、JPEG。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163742.58702586740004184494753458327290:50001231000000:2800:959AEF0F5ACE6014FA5E1F3279DA9884A62BA32A3A6EBAE8B57C284C24061851.png)

## 接口说明

|接口名|描述|
|:--|:--|
|[addBackground](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section13641714101419)(info: BackgroundInfo, startIndex: number, endIndex: number, oddPages: boolean, evenPages: boolean): void|插入PDF文档背景。|
|[removeBackground](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section16476184082314)(): boolean|删除PDF文档背景。|

注意

[addBackground](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfservice#section13641714101419)方法属于耗时业务，需要遍历每一页去添加背景，添加页面较多时建议放到线程里去处理。

## 示例代码

**添加背景：**

1. 调用loadDocument方法，加载PDF文档。
2. 实例化背景BackgroundInfo类，并设置相关属性，包括大小、旋转、透明度和位置等。
3. 调用addBackground方法，添加背景。
4. 保存PDF文档到应用沙箱。

**删除背景：**

1. 调用loadDocument方法，加载PDF文档。
2. 调用removeBackground方法，去除背景。
3. 保存PDF文档到应用沙箱。

4. import { pdfService } from '@kit.PDFKit';
5. import { hilog } from '@kit.PerformanceAnalysisKit';

6. @Entry
7. @Component
8. struct PdfPage {
9.   private pdfDocument: pdfService.PdfDocument = new pdfService.PdfDocument();
10.   private context = this.getUIContext().getHostContext() as Context;

11.   build() {
12.     Column() {
13.       Button('addBackground').onClick(async () => {
14.         // 确保沙箱目录有input.pdf文档
15.         let filePath = this.context.filesDir + '/input.pdf';
16.         let res = this.pdfDocument.loadDocument(filePath);
17.         if (res === pdfService.ParseResult.PARSE_SUCCESS) {
18.           let bginfo: pdfService.BackgroundInfo = new pdfService.BackgroundInfo();
19.           // 确保沙箱目录有img.jpg文档
20.           bginfo.imagePath = this.context.filesDir + '/img.jpg';
21.           bginfo.backgroundColor = 50;
22.           bginfo.isOnTop = true;
23.           bginfo.rotation = 45;
24.           bginfo.scale = 0.5;
25.           bginfo.opacity = 0.3;
26.           bginfo.verticalAlignment = pdfService.BackgroundAlignment.BACKGROUND_ALIGNMENT_TOP;
27.           bginfo.horizontalAlignment = pdfService.BackgroundAlignment.BACKGROUND_ALIGNMENT_LEFT;
28.           bginfo.horizontalSpace = 1.0;
29.           bginfo.verticalSpace = 1.0;
30.           this.pdfDocument.addBackground(bginfo, 0, 2, true, true);
31.           let outPdfPath = this.context.filesDir + '/testAddBackground.pdf';
32.           let result = this.pdfDocument.saveDocument(outPdfPath);
33.           hilog.info(0x0000, 'PdfPage', 'addBackground %{public}s!', result ? 'success' : 'fail');
34.         }
35.         this.pdfDocument.releaseDocument();
36.       })
37.       Button('removeBackground').onClick(async () => {
38.         let filePath = this.context.filesDir + '/testAddBackground.pdf';
39.         let res = this.pdfDocument.loadDocument(filePath);
40.         if (res === pdfService.ParseResult.PARSE_SUCCESS && this.pdfDocument.hasBackground()) {
41.           let removeResult = this.pdfDocument.removeBackground();
42.           if (removeResult) {
43.             let outPdfPath = this.context.filesDir + '/removeBackground.pdf';
44.             let result = this.pdfDocument.saveDocument(outPdfPath);
45.             hilog.info(0x0000, 'PdfPage', 'removeBackground %{public}s!', result ? 'success' : 'fail');
46.           }
47.         }
48.         this.pdfDocument.releaseDocument();
49.       })
50.     }
51.   }
52. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-add-watermark "添加、删除水印")
# 打开和保存PDF文档

更新时间: 2025-12-16 16:36

## 场景介绍

通过加载本地路径的PDF文档，实现打开PDF文档的预览功能。当PDF文档做了批注等相关的信息时，可以使用保存功能。

和pdfService的打开和保存能力相同，具体区别查看pdfService的[打开和保存PDF文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-open-document)的场景介绍。

## 接口说明

|接口名|描述|
|:--|:--|
|[loadDocument](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section073321844615)(path: string, password?: string, initPageIndex?: number, onProgress?: Callback<number>): Promise<pdfService.ParseResult>|加载PDF文档。|
|[saveDocument](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section1641615224414)(path: string, onProgress?: Callback<number>): Promise<number>|保存PDF文档，使用Promise异步回调。|

## 示例代码

1. 在aboutToAppear函数里面加载PDF文档。
2. 调用PdfView预览组件，渲染显示。
3. 在【savePdfDocument】按钮中调用saveDocument方法另存PDF文档。

4. import { pdfService, PdfView, pdfViewManager } from '@kit.PDFKit';
5. import { hilog } from '@kit.PerformanceAnalysisKit';

6. @Entry
7. @Component
8. struct PdfPage {
9.   private controller: pdfViewManager.PdfController = new pdfViewManager.PdfController();
10.   private context = this.getUIContext().getHostContext() as Context;
11.   private loadResult: pdfService.ParseResult = pdfService.ParseResult.PARSE_ERROR_FORMAT;

12.   aboutToAppear(): void {
13.     // 确保沙箱目录有input.pdf文档
14.     let filePath = this.context.filesDir + '/input.pdf';
15.     (async () => {
16.       this.loadResult = await this.controller.loadDocument(filePath);     
17.     })()
18.   }

19.   build() {
20.     Column() {    
21.       // 保存Pdf文档
22.       Button('savePdfDocument').onClick(async () => {
23.         if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
24.           let savePath = this.context.filesDir + '/savePdfDocument.pdf';
25.           let result = await this.controller.saveDocument(savePath);
26.           hilog.info(0x0000, 'PdfPage', 'savePdfDocument %{public}s!', result ? 'success' : 'fail');
27.         }
28.       })
29.       PdfView({
30.         controller: this.controller,
31.         pageFit: pdfService.PageFit.FIT_WIDTH,
32.         showScroll: true
33.       })
34.         .id('pdfview_app_view')
35.         .layoutWeight(1);
36.     }
37.     .width('100%')
38.     .height('100%')
39.   }
40. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-pdfview-component "预览PDF文档")
# 打开和保存PDF文档

更新时间: 2025-12-16 16:36

## 场景介绍

通过加载本地路径的PDF文档，实现打开PDF文档的预览功能。当PDF文档做了批注等相关的信息时，可以使用保存功能。

和pdfService的打开和保存能力相同，具体区别查看pdfService的[打开和保存PDF文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-open-document)的场景介绍。

## 接口说明

|接口名|描述|
|:--|:--|
|[loadDocument](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section073321844615)(path: string, password?: string, initPageIndex?: number, onProgress?: Callback<number>): Promise<pdfService.ParseResult>|加载PDF文档。|
|[saveDocument](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section1641615224414)(path: string, onProgress?: Callback<number>): Promise<number>|保存PDF文档，使用Promise异步回调。|

## 示例代码

1. 在aboutToAppear函数里面加载PDF文档。
2. 调用PdfView预览组件，渲染显示。
3. 在【savePdfDocument】按钮中调用saveDocument方法另存PDF文档。

4. import { pdfService, PdfView, pdfViewManager } from '@kit.PDFKit';
5. import { hilog } from '@kit.PerformanceAnalysisKit';

6. @Entry
7. @Component
8. struct PdfPage {
9.   private controller: pdfViewManager.PdfController = new pdfViewManager.PdfController();
10.   private context = this.getUIContext().getHostContext() as Context;
11.   private loadResult: pdfService.ParseResult = pdfService.ParseResult.PARSE_ERROR_FORMAT;

12.   aboutToAppear(): void {
13.     // 确保沙箱目录有input.pdf文档
14.     let filePath = this.context.filesDir + '/input.pdf';
15.     (async () => {
16.       this.loadResult = await this.controller.loadDocument(filePath);     
17.     })()
18.   }

19.   build() {
20.     Column() {    
21.       // 保存Pdf文档
22.       Button('savePdfDocument').onClick(async () => {
23.         if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
24.           let savePath = this.context.filesDir + '/savePdfDocument.pdf';
25.           let result = await this.controller.saveDocument(savePath);
26.           hilog.info(0x0000, 'PdfPage', 'savePdfDocument %{public}s!', result ? 'success' : 'fail');
27.         }
28.       })
29.       PdfView({
30.         controller: this.controller,
31.         pageFit: pdfService.PageFit.FIT_WIDTH,
32.         showScroll: true
33.       })
34.         .id('pdfview_app_view')
35.         .layoutWeight(1);
36.     }
37.     .width('100%')
38.     .height('100%')
39.   }
40. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-pdfview-component "预览PDF文档")
# 设置PDF文档预览效果

更新时间: 2025-12-16 16:37

pdfViewManager为PDF文档提供了丰富的预览特性。

- 单双页布局，是否连续滚动和页面适配方式。
- 页面跳转，如上一页，下一页，跳转到指定页。
- 页面放大、缩小。

**图1**：提供了双页预览布局，页面宽度适配和连续滚动的预览方式

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163702.06114726764460660874420278644562:50001231000000:2800:9220A81ACB9A9E0B9EF8CFDEDCB60EBE9004E8D48A6FFD19B14DECA6AC886DFB.jpg "点击放大")

## 接口说明

|接口名|描述|
|:--|:--|
|[setPageLayout](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section113581457158)(columnCount: pdfService.PageLayout): void|设置页面布局模式。其中“columnCount”取值如下：<br><br>- 1：单页面<br>- 2：双页面|
|[setPageContinuous](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section32161930132611)(isContinuous: boolean): void|设置页面滚动是否连续排列。|
|[setPageFit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section347455378)(pageFit: pdfService.PageFit): void|设置页面的适配模式。|
|[goToPage](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section9554132275317)(pageIndex: number): void|跳转到指定页。|
|[setPageZoom](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section2693181014192)(zoom: number): void|设置视图的缩放比例。|

## 示例代码

1. 先加载PDF文档。
2. 调用PdfView预览组件，渲染显示。
3. 在按钮【setPreviewMode】里，调用setPageLayout、setPageContinuous等方法，设置文档预览效果。
4. 在按钮【goTopage】里，调用goToPage方法，设置页面跳转。
5. 在按钮【zoomPage2】里，调用setPageZoom方法，将页面放大2倍。

6. import { pdfService, PdfView, pdfViewManager } from '@kit.PDFKit';

7. @Entry
8. @Component
9. struct PdfPage {
10.   private controller: pdfViewManager.PdfController = new pdfViewManager.PdfController();
11.   private context = this.getUIContext().getHostContext() as Context;
12.   private loadResult: pdfService.ParseResult = pdfService.ParseResult.PARSE_ERROR_FORMAT;

13.   aboutToAppear(): void {
14.     // 确保沙箱目录有input.pdf文档
15.     let filePath = this.context.filesDir + '/input.pdf';
16.     (async () => {
17.       this.loadResult = await this.controller.loadDocument(filePath);
18.       // 注意：这里刚加载文档，请不要在这里立即设置PDF文档的预览方法。
19.     })()
20.   }

21.   build() {
22.     Column() {
23.       Row() {
24.         // 设置预览方式
25.         Button('setPreviewMode').onClick(() => {
26.           if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
27.             // 单页布局
28.             this.controller.setPageLayout(pdfService.PageLayout.LAYOUT_SINGLE);
29.             // 是否连续滚动预览
30.             this.controller.setPageContinuous(true);
31.             // 适配页的预览方式
32.             this.controller.setPageFit(pdfService.PageFit.FIT_PAGE);
33.           }
34.         })
35.         // 跳转到第11页
36.         Button('goTopage').onClick(() => {
37.           if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
38.             this.controller.goToPage(10);
39.           }
40.         })
41.         // 页面放大2倍
42.         Button('zoomPage2').onClick(() => {
43.           if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
44.             this.controller.setPageZoom(2);
45.           }
46.         })
47.       }

48.       PdfView({
49.         controller: this.controller,
50.         pageFit: pdfService.PageFit.FIT_WIDTH,
51.         showScroll: true
52.       })
53.         .id('pdfview_app_view')
54.         .layoutWeight(1);
55.     }
56.   }
57. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-pdfview-open "打开和保存PDF文档")
# 搜索关键字

更新时间: 2025-12-16 16:37

预览PDF文档时，可以对页面的关键词（英文字符不区分大小写）进行搜索并高亮显示，同时使用[setSearchIndex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section7253141182617)方法高亮显示指定的搜索结果。

使用[getSearchIndex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section10557163718239)方法获取当前高亮的索引，可以使用[clearSearch](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section773545002018)方法清除所有搜索结果。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163727.67762142968686783162316819053529:50001231000000:2800:F0C73E14D36C408F7BE0560217C31892BBD4791A283F316F01BD0EAA85B493C6.jpg "点击放大")

## 接口说明

|接口名|描述|
|:--|:--|
|[searchKey](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section117864247160)(text: string, listener: Callback<number>): void|搜索文本并返回匹配的总数。|
|[clearSearch](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section773545002018)(): void|清除搜索文本的高亮，等价于搜索空字符串 。|
|[setSearchIndex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section7253141182617)(index: number): void|设置搜索匹配结果的索引，页面会跳转到索引对应搜索结果处。|
|[getSearchIndex](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section10557163718239)(): number|获取当前命中搜索关键字匹配结果的索引，执行搜索接口后默认命中索引为0。|

## 示例代码

1. 先加载PDF文档。
2. 调用PdfView预览组件，渲染显示。
3. 在按钮【searchKey】里，调用searchKey方法，搜索指定关键字。
4. 上一个、下一个搜索按钮跳转到对应的结果。
5. 在按钮【getSearchIndex】里，调用getSearchIndex方法，获取当前的搜索结果索引。
6. 在按钮【clearSearch】里，调用clearSearch方法，清除搜索结果。

7. import { pdfService, PdfView, pdfViewManager } from '@kit.PDFKit';
8. import { hilog } from '@kit.PerformanceAnalysisKit';

9. @Entry
10. @Component
11. struct Index {
12.   private controller: pdfViewManager.PdfController = new pdfViewManager.PdfController();
13.   private context = this.getUIContext().getHostContext() as Context;
14.   private loadResult: pdfService.ParseResult = pdfService.ParseResult.PARSE_ERROR_FORMAT;
15.   private searchIndex = 0;
16.   private charCount = 0;

17.   aboutToAppear(): void {
18.     // 确保沙箱目录有input.pdf文档
19.     let filePath = this.context.filesDir + '/input.pdf';
20.     (async () => {
21.       this.loadResult = await this.controller.loadDocument(filePath);
22.     })()
23.   }

24.   build() {
25.     Column() {
26.       Scroll() {
27.         Row() {
28.           // 搜索关键字
29.           Button('searchKey').onClick(async () => {
30.             if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
31.               this.controller.searchKey('C++', (index: number) => {
32.                 this.charCount = index;
33.                 hilog.info(0x0000, 'PdfPage', 'searchKey %{public}s!', index + '');
34.               })
35.             }
36.           })
37.             .width(100)
38.           // 上一个
39.           Button('setSearchPrevIndex').onClick(async () => {
40.             if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
41.               if(this.searchIndex > 0) {
42.                 this.controller.setSearchIndex(--this.searchIndex);
43.               }
44.             }
45.           })
46.             .width(200)
47.           // 下一个
48.           Button('setSearchNextIndex').onClick(async () => {
49.             if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
50.               if(this.searchIndex < this.charCount) {
51.                 this.controller.setSearchIndex(++this.searchIndex);
52.               }
53.             }
54.           })
55.             .width(200)
56.           // 获取当前页索引
57.           Button('getSearchIndex').onClick(async () => {
58.             if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
59.               let curSearchIndex = this.controller.getSearchIndex();
60.               hilog.info(0x0000, 'PdfPage', 'curSearchIndex %{public}s!', curSearchIndex + '');
61.             }
62.           })
63.             .width(150)
64.           // 清除搜索文本的高亮
65.           Button('clearSearch').onClick(async () => {
66.             if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
67.               this.controller.clearSearch();
68.             }
69.           })
70.             .width(150)
71.         }
72.       }
73.       .scrollable(ScrollDirection.Horizontal)

74.       PdfView({
75.         controller: this.controller,
76.         pageFit: pdfService.PageFit.FIT_WIDTH,
77.         showScroll: true
78.       })
79.         .id('pdfview_app_view')
80.         .layoutWeight(1);
81.     }
82.   }
83. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-pdfview-preview-method "设置PDF文档预览效果")
# 批注

更新时间: 2025-12-16 16:37

进入批注模式，目前支持高亮、下划线和删除线类型批注。

## 接口说明

|接口名|描述|
|:--|:--|
|[enableAnnotation](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section1771517381253)(annotationType: SupportedAnnotationType, color?: number): void|在常用操作之间切换并添加批注。|

## 示例代码

1. 先加载PDF文档。
2. 调用PdfView预览组件，渲染显示。
3. 调用enableAnnotation方法，进入批注模式。

4. import { pdfService, pdfViewManager, PdfView } from '@kit.PDFKit';

5. @Entry
6. @Component
7. struct PdfPage {
8.   private pdfController = new pdfViewManager.PdfController();
9.   private context = this.getUIContext().getHostContext() as Context;

10.   aboutToAppear(): void {
11.     // 确保沙箱目录有input.pdf文档
12.     let filePath = this.context.filesDir + '/input.pdf';
13.     (async () => {
14.       let loadResult: pdfService.ParseResult = await this.pdfController.loadDocument(filePath);
15.       if (pdfService.ParseResult.PARSE_SUCCESS === loadResult) {
16.         // 添加删除线批注
17.         this.pdfController.enableAnnotation(pdfViewManager.SupportedAnnotationType.STRIKETHROUGH, 0xAAEEEEEE);
18.       }
19.     })()
20.   }

21.   build() {
22.     Column() {
23.       // 加载PdfView组件进行预览
24.       PdfView({
25.         controller: this.pdfController,
26.         pageFit: pdfService.PageFit.FIT_WIDTH,
27.         showScroll: true
28.       })
29.         .id('pdfview_app_view')
30.         .layoutWeight(1);
31.     }
32.   }
33. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-pdfview-highlight "高亮显示PDF文档")
# PDF缩略图转换为图片

更新时间: 2025-12-16 16:37

## 场景介绍

调用[getPagePixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section858145014542)方法，将指定PDF缩略图转化为图片。

## 接口说明

|接口名|描述|
|:--|:--|
|[getPagePixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section858145014542)(pageIndex: number, isSync?: boolean): Promise<image.PixelMap>|获取对应PDF页面的缩略图，使用Promise异步回调。|

## 示例代码

1. 调用loadDocument方法，加载PDF文档。
2. 调用getPagePixelMap方法，获取image.PixelMap对象。
3. 将image.PixelMap转化为二进制图片文件并保存。

4. import { pdfService, pdfViewManager } from '@kit.PDFKit';
5. import { image } from '@kit.ImageKit';
6. import { fileIo as fs } from '@kit.CoreFileKit';
7. import { BusinessError } from '@kit.BasicServicesKit';
8. import { hilog } from '@kit.PerformanceAnalysisKit';

9. @Entry
10. @Component
11. struct PdfPage {
12.   private controller: pdfViewManager.PdfController = new pdfViewManager.PdfController();
13.   private context = this.getUIContext().getHostContext() as Context;
14.   private loadResult: pdfService.ParseResult = pdfService.ParseResult.PARSE_ERROR_FORMAT;

15.   aboutToAppear(): void {
16.     // 确保沙箱目录有input.pdf文档
17.     let filePath = this.context.filesDir + '/input.pdf';
18.     (async () => {
19.       this.loadResult = await this.controller.loadDocument(filePath);
20.     })()
21.   }

22.   // 将 pixelMap 转成图片格式
23.   pixelMap2Buffer(pixelMap: image.PixelMap): Promise<ArrayBuffer> {
24.     return new Promise((resolve, reject) => {
25.       /**
26.        设置打包参数
27.        format：图片打包格式
28.        quality：JPEG 编码输出图片质量
29.        */
30.       let packOpts: image.PackingOption = { format: 'image/jpeg', quality: 98 }
31.       // 创建ImagePacker实例
32.       const imagePackerApi = image.createImagePacker()
33.       imagePackerApi.packToData(pixelMap, packOpts).then((buffer: ArrayBuffer) => {
34.         resolve(buffer)
35.       }).catch((err: BusinessError) => {
36.         reject()
37.       })
38.     })
39.   }

40.   build() {
41.     Column() {
42.       // 转换为图片并保存到应用沙箱
43.       Button('getPagePixelMap').onClick(async () => {
44.         if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
45.           let pixmap: image.PixelMap = await this.controller.getPagePixelMap(0, true);
46.           if (!pixmap) {
47.             return
48.           }
49.           const imgBuffer = await this.pixelMap2Buffer(pixmap)
50.           try {
51.             const file =
52.               fs.openSync(this.context.filesDir + `/${Date.now()}.png`, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
53.             await fs.write(file.fd, imgBuffer);
54.             // 关闭文件
55.             await fs.close(file.fd)
56.           } catch (e) {
57.             let error: BusinessError = e as BusinessError;
58.             hilog.error(0x0000, 'getPagePixelMap-', `Code: ${error.code}, message: ${error.message} `);
59.           }
60.         }
61.       })
62.     }
63.   }
64. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-pdfview-annotation "批注")
# PDF缩略图转换为图片

更新时间: 2025-12-16 16:37

## 场景介绍

调用[getPagePixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section858145014542)方法，将指定PDF缩略图转化为图片。

## 接口说明

|接口名|描述|
|:--|:--|
|[getPagePixelMap](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-arkts-pdfviewmanage#section858145014542)(pageIndex: number, isSync?: boolean): Promise<image.PixelMap>|获取对应PDF页面的缩略图，使用Promise异步回调。|

## 示例代码

1. 调用loadDocument方法，加载PDF文档。
2. 调用getPagePixelMap方法，获取image.PixelMap对象。
3. 将image.PixelMap转化为二进制图片文件并保存。

4. import { pdfService, pdfViewManager } from '@kit.PDFKit';
5. import { image } from '@kit.ImageKit';
6. import { fileIo as fs } from '@kit.CoreFileKit';
7. import { BusinessError } from '@kit.BasicServicesKit';
8. import { hilog } from '@kit.PerformanceAnalysisKit';

9. @Entry
10. @Component
11. struct PdfPage {
12.   private controller: pdfViewManager.PdfController = new pdfViewManager.PdfController();
13.   private context = this.getUIContext().getHostContext() as Context;
14.   private loadResult: pdfService.ParseResult = pdfService.ParseResult.PARSE_ERROR_FORMAT;

15.   aboutToAppear(): void {
16.     // 确保沙箱目录有input.pdf文档
17.     let filePath = this.context.filesDir + '/input.pdf';
18.     (async () => {
19.       this.loadResult = await this.controller.loadDocument(filePath);
20.     })()
21.   }

22.   // 将 pixelMap 转成图片格式
23.   pixelMap2Buffer(pixelMap: image.PixelMap): Promise<ArrayBuffer> {
24.     return new Promise((resolve, reject) => {
25.       /**
26.        设置打包参数
27.        format：图片打包格式
28.        quality：JPEG 编码输出图片质量
29.        */
30.       let packOpts: image.PackingOption = { format: 'image/jpeg', quality: 98 }
31.       // 创建ImagePacker实例
32.       const imagePackerApi = image.createImagePacker()
33.       imagePackerApi.packToData(pixelMap, packOpts).then((buffer: ArrayBuffer) => {
34.         resolve(buffer)
35.       }).catch((err: BusinessError) => {
36.         reject()
37.       })
38.     })
39.   }

40.   build() {
41.     Column() {
42.       // 转换为图片并保存到应用沙箱
43.       Button('getPagePixelMap').onClick(async () => {
44.         if (this.loadResult === pdfService.ParseResult.PARSE_SUCCESS) {
45.           let pixmap: image.PixelMap = await this.controller.getPagePixelMap(0, true);
46.           if (!pixmap) {
47.             return
48.           }
49.           const imgBuffer = await this.pixelMap2Buffer(pixmap)
50.           try {
51.             const file =
52.               fs.openSync(this.context.filesDir + `/${Date.now()}.png`, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
53.             await fs.write(file.fd, imgBuffer);
54.             // 关闭文件
55.             await fs.close(file.fd)
56.           } catch (e) {
57.             let error: BusinessError = e as BusinessError;
58.             hilog.error(0x0000, 'getPagePixelMap-', `Code: ${error.code}, message: ${error.message} `);
59.           }
60.         }
61.       })
62.     }
63.   }
64. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-pdfview-annotation "批注")
# PDF文档支持在线预览吗？

更新时间: 2025-12-16 16:36

PDF Kit不支持在线预览，需要把文档下载到本地，才能预览，具体可参见[预览PDF文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-pdfview-component)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-faq-4 "PDF Kit可以移除具体页面的页眉页脚、水印、背景吗？")
# PDF文档支持在线预览吗？

更新时间: 2025-12-16 16:36

PDF Kit不支持在线预览，需要把文档下载到本地，才能预览，具体可参见[预览PDF文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-pdfview-component)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-faq-4 "PDF Kit可以移除具体页面的页眉页脚、水印、背景吗？")
